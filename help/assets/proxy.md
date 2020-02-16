---
title: Proxyutveckling för resurser
description: En proxy är en AEM-instans som använder proxyarbetare för att bearbeta jobb. Lär dig hur du konfigurerar en AEM-proxy, åtgärder som stöds, proxykomponenter och hur du utvecklar en anpassad proxyarbetare.
contentOwner: AG
translation-type: tm+mt
source-git-commit: a39ee0f435dc43d2c2830b2947e91ffdcf11c7f6

---


# Proxyutveckling för resurser {#assets-proxy-development}

Adobe Experience Manager Assets (AEM) Assets använder en proxy för att distribuera bearbetningen för vissa uppgifter.

En proxy är en specifik (och ibland separat) AEM-instans som använder proxyarbetare som processorer som hanterar ett jobb och skapar ett resultat. En proxyarbetare kan användas för en mängd olika uppgifter. När det gäller en AEM Resurser-proxy kan detta användas för att läsa in resurser för återgivning i AEM Resurser. IDS- [proxyarbetaren](indesign.md) använder till exempel en InDesign-server för att bearbeta filer som ska användas i AEM Resurser.

När proxyn är en separat AEM-instans minskar detta belastningen på AEM-redigeringsinstansen/-instanserna. Som standard kör AEM Resurser resurshanteringsuppgifterna i samma JVM (externaliserat via Proxy) för att minska belastningen på AEM-redigeringsinstansen.

## Proxy (HTTP Access) {#proxy-http-access}

En proxy är tillgänglig via HTTP-servern när den är konfigurerad att acceptera bearbetningsjobb på: `/libs/dam/cloud/proxy`. Den här servern skapar ett snedjobb av de bokförda parametrarna. Detta läggs sedan till i proxyjobbkön och ansluts till lämplig proxyarbetare.

### Åtgärder som stöds {#supported-operations}

* `job`

   **Krav**: parametern `jobevent` måste anges som en serialiserad värdekarta. Detta används för att skapa en `Event` för en jobbprocessor.

   **Resultat**: Lägger till ett nytt jobb. Om det lyckas returneras ett unikt jobb-ID.

```shell
curl -u admin:admin -F":operation=job" -F"someproperty=xxxxxxxxxxxx"
    -F"jobevent=serialized value map" http://localhost:4502/libs/dam/cloud/proxy
```

* `result`

   **Krav**: parametern `jobid` måste anges.

   **Resultat**: Returnerar en JSON-representation av den resulterande noden som skapats av jobbprocessorn.

```shell
curl -u admin:admin -F":operation=result" -F"jobid=xxxxxxxxxxxx"
    http://localhost:4502   /libs/dam/cloud/proxy
```

* `resource`

   **Krav**: parametern jobid måste anges.

   **Resultat**: Returnerar en resurs som är associerad med det angivna jobbet.

```shell
curl -u admin:admin -F":operation=resource" -F"jobid=xxxxxxxxxxxx"
    -F"resourcePath=something.pdf" http://localhost:4502/libs/dam/cloud/proxy
```

* `remove`

   **Krav**: parametern jobid måste anges.

   **Resultat**: Tar bort ett jobb om det hittas.

```shell
curl -u admin:admin -F":operation=remove" -F"jobid=xxxxxxxxxxxx"
    http://localhost:4502/libs/dam/cloud/proxy
```

### Proxyarbetare {#proxy-worker}

En proxyarbetare är en processor som hanterar ett jobb och skapar ett resultat. Arbetare finns i proxyinstansen och måste implementera [snedställande JobProcessor](https://sling.apache.org/site/eventing-and-jobs.html) för att identifieras som en proxyarbetare.

>[!NOTE]
>
>Arbetaren måste implementera [snedställningsjobbbearbetaren](https://sling.apache.org/site/eventing-and-jobs.html) för att kunna identifieras som en proxyarbetare.

### Klient-API {#client-api}

[`JobService`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html) är tillgänglig som en OSGi-tjänst som tillhandahåller metoder för att skapa jobb, ta bort jobb och hämta resultat från dessa jobb. Standardimplementeringen av den här tjänsten (`JobServiceImpl`) använder HTTP-klienten för att kommunicera med fjärrproxyservern.

Här följer ett exempel på API-användning:

```xml
@Reference
 JobService proxyJobService;

 // to create a new job
 final Hashtable props = new Hashtable();
 props.put("someproperty", "some value");
 props.put(JobUtil.PROPERTY_JOB_TOPIC, "myworker/job"); // this is an identifier of the worker
 final String jobId = proxyJobService.addJob(props, new Asset[]{asset});

 // to check status (returns JobService.STATUS_FINISHED or JobService.STATUS_INPROGRESS)
 int status = proxyJobService.getStatus(jobId)

 // to get the result
 final String jsonString = proxyJobService.getResult(jobId);

 // to remove job and cleanup
 proxyJobService.removeJob(jobId);
```

### Konfigurationer av molntjänster {#cloud-service-configurations}

>[!NOTE]
>
>Referensdokumentation för proxy-API:t finns under [`com.day.cq.dam.api.proxy`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/dam/api/proxy/package-summary.html).

Både proxy- och proxyarbetarkonfigurationer är tillgängliga via molntjänster som nås från AEM Assets **Tools** Console eller under `/etc/cloudservices/proxy`. Varje proxyarbetare förväntas lägga till en nod under `/etc/cloudservices/proxy` för arbetarspecifik konfigurationsinformation (till exempel `/etc/cloudservices/proxy/workername`).

>[!NOTE]
>
>Mer information finns i [konfigurationen](indesign.md#configuring-the-proxy-worker-for-indesign-server) av Proxy Worker för InDesign Server och [Cloud Services-konfigurationen](../sites-developing/extending-cloud-config.md) .

Här följer ett exempel på API-användning:

```xml
@Reference(policy = ReferencePolicy.STATIC)
 ProxyConfig proxyConfig;

 // to get proxy config
 Configuration cloudConfig = proxyConfig.getConfiguration();
 final String value = cloudConfig.get("someProperty", "defaultValue");

 // to get worker config
 Configuration cloudConfig = proxyConfig.getConfiguration("workername");
 final String value = cloudConfig.get("someProperty", "defaultValue");
```

### Utveckla en anpassad proxyarbetare {#developing-a-customized-proxy-worker}

IDS- [proxyarbetaren](indesign.md) är ett exempel på en AEM Resurser-proxyarbetare som redan medföljer för att lägga ut bearbetning av InDesign-resurser på entreprenad.

Du kan också utveckla och konfigurera din egen AEM Assets-proxyarbetare för att skapa en specialiserad arbetare som kan skicka och lägga ut AEM Assets-bearbetningsuppgifter på entreprenad.

Om du konfigurerar en egen anpassad proxyarbetare måste du:

* Konfigurera och implementera (med Sling-händelse):

   * ett anpassat jobbämne
   * en anpassad jobbhändelsehanterare

* Använd sedan JobService API för att:

   * skicka ditt anpassade jobb till proxyn
   * hantera ditt jobb

* Om du vill använda utkastet från ett arbetsflöde måste du implementera ett anpassat externt steg med WorkflowExternalProcess API och JobService API.

Följande diagram och steg visar hur du fortsätter:

![chlimage_1-249](assets/chlimage_1-249.png)

>[!NOTE]
>
>I följande steg anges motsvarigheter i InDesign som referensexempel.

1. Ett [delningsjobb](https://sling.apache.org/site/eventing-and-jobs.html) används, så du måste definiera ett jobbämne för ditt användningsfall.

   Ett exempel finns `IDSJob.IDS_EXTENDSCRIPT_JOB` i IDS-proxyarbetaren.

1. Det externa steget används för att utlösa händelsen och sedan vänta tills det är klart. detta görs genom att avfråga ID:t. Du måste utveckla ett eget steg för att implementera nya funktioner.

   Implementera en `WorkflowExternalProcess`, använd sedan JobService API och ditt jobbämne för att förbereda en jobbhändelse och skicka den till JobService (en OSGi-tjänst).

   Se till exempel `INDDMediaExtractProcess`.java för IDS-proxyarbetaren.

1. Implementera en jobbhanterare för ditt ämne. Hanteraren kräver utveckling så att den utför din specifika åtgärd och anses vara implementeringen av arbetaren.

   Ett exempel finns `IDSJobProcessor.java` i IDS-proxyarbetaren.

1. Använda `ProxyUtil.java` i dammråttor. På så sätt kan du skicka jobb till arbetare med dammproxyn.

>[!NOTE]
>
>Det AEM Assets-proxyramverket inte har någon färdig funktion är poolmekanismen.
>
>InDesign-integreringen ger åtkomst till en pool med indesign-servrar (IDSPool). Den här poolen är specifik för InDesign-integrering och ingår inte i AEM Assets-proxyramverket.

>[!NOTE]
>
>Synkronisering av resultat:
>
>Om ingen instans använder samma proxy stannar bearbetningsresultatet kvar hos proxyn. Det är klientens (AEM Author) uppgift att begära resultatet med samma unika jobb-ID som anges för klienten när jobbet skapas. Proxyservern utför jobbet och ser till att resultatet är klart att begäras.
