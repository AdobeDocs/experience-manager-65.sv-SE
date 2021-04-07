---
title: Tjänstanvändare i AEM
seo-title: Tjänstanvändare i AEM
description: Läs mer om tjänstanvändare i AEM.
seo-description: Läs mer om tjänstanvändare i AEM.
uuid: 4efab5fb-ba11-4922-bd68-43ccde4eb355
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: 9cfe5f11-8a0e-4a27-9681-a8d50835c864
exl-id: ccd8577b-3bbf-40ba-9696-474545f07b84
feature: Dokumentskydd
translation-type: tm+mt
source-git-commit: 9134130f349c6c7a06ad9658a87f78a86b7dbf9c
workflow-type: tm+mt
source-wordcount: '1789'
ht-degree: 0%

---

# Tjänstanvändare i AEM{#service-users-in-aem}

## Översikt {#overview}

Det huvudsakliga sättet att få en administrativ session eller resurslösare i AEM var att använda metoderna `SlingRepository.loginAdministrative()` och `ResourceResolverFactory.getAdministrativeResourceResolver()` i Sling.

Ingen av dessa metoder har dock utformats kring [principen om minst privilegium](https://en.wikipedia.org/wiki/Principle_of_least_privilege) och gör det för enkelt för en utvecklare att inte planera för en lämplig struktur och motsvarande åtkomstkontrollnivåer (ACL) för sitt innehåll tidigt. Om det finns en säkerhetslucka i en sådan tjänst leder det ofta till eskalering av behörigheter till `admin`-användaren, även om själva koden inte behöver administratörsbehörighet för att fungera.

## Så här fasar du ut administratörssessioner {#how-to-phase-out-admin-sessions}

### Prioritet 0: Är funktionen aktiv/nödvändig/borttagen? {#priority-is-the-feature-active-needed-derelict}

Det kan finnas fall där adminsessionen inte används eller där funktionen är helt inaktiverad. Om så är fallet med implementeringen ska du ta bort funktionen helt eller anpassa den till [NOP-koden](https://en.wikipedia.org/wiki/NOP).

### Prioritet 1: Använd begärandesessionen {#priority-use-the-request-session}

När det är möjligt kan du ändra funktionen så att den angivna autentiserade begärandesessionen kan användas för att läsa eller skriva innehåll. Om detta inte är möjligt kan det ofta uppnås genom att man tillämpar de prioriteringar som anges nedan.

### Prioritet 2: Strukturera om innehåll {#priority-restructure-content}

Många problem kan lösas genom att innehållet struktureras om. Tänk på följande enkla regler när du omstrukturerar:

* **Ändra åtkomstkontroll**

   * Se till att de användare eller grupper som verkligen behöver åtkomst faktiskt har åtkomst.

* **Förfina innehållsstruktur**

   * Flytta den till andra platser, t.ex. där åtkomstkontrollen matchar de tillgängliga begärandesessionerna.
   * Ändra innehållets granularitet,

* **Låt koden vara en riktig tjänst**

   * Flytta affärslogiken från JSP-kod till service. Detta möjliggör olika innehållsmodellering.

Se även till att alla nya funktioner du utvecklar följer dessa principer:

* **Säkerhetskrav bör styra innehållsstrukturen**

   * Åtkomstkontroll ska kännas naturlig
   * Åtkomstkontrollen måste verkställas av databasen, inte av programmet

* **Använd nodtyper**

   * Begränsa uppsättningen egenskaper som kan anges

* **Respektera sekretessinställningar**

   * När det gäller privata profiler är ett exempel att inte visa profilbilden, e-postadressen eller det fullständiga namnet som finns på den privata `/profile`-noden.

## Strikta åtkomstkontroll {#strict-access-control}

Vare sig du tillämpar åtkomstkontroll vid innehållsomstrukturering eller när du gör det för en ny användare måste du tillämpa striktaste åtkomstkontrollistor. Använd alla möjliga hjälpmedel för åtkomstkontroll:

* I stället för att använda `jcr:read` på `/apps` bör du bara använda det på `/apps/*/components/*/analytics`

* Använd [begränsningar](https://jackrabbit.apache.org/oak/docs/security/authorization/restriction.html)

* Använd åtkomstkontrollistor för nodtyper
* Begränsa behörigheter

   * Om du till exempel bara behöver skriva egenskaper ska du inte ge `jcr:write` behörighet; använd `jcr:modifyProperties` i stället

## Tjänstanvändare och mappningar {#service-users-and-mappings}

Om ovanstående misslyckas erbjuder Sling 7 en tjänst för Mappning av tjänstanvändare, som gör det möjligt att konfigurera en mappning från paket till användare och två motsvarande API-metoder: ` [SlingRepository.loginService()](https://sling.apache.org/apidocs/sling7/org/apache/sling/jcr/api/SlingRepository.html#loginService-java.lang.String-java.lang.String-)` och ` [ResourceResolverFactory.getServiceResourceResolver()](https://sling.apache.org/apidocs/sling7/org/apache/sling/api/resource/ResourceResolverFactory.html#getServiceResourceResolver-java.util.Map-)` som returnerar en sessions-/resurslösare med endast behörighet för en konfigurerad användare. Dessa metoder har följande egenskaper:

* De tillåter att användare mappar tjänster
* De gör det möjligt att definiera underleverantörer
* Den centrala konfigurationspunkten är: `org.apache.sling.serviceusermapping.impl.ServiceUserMapperImpl`
* `service-id` =  `service-name` [ &quot;:&quot; subservice-name  ] 

* `service-id` mappas till en resurslösare och/eller JCR-databasens användar-ID för autentisering
* `service-name` är det symboliska namnet på det paket som tillhandahåller tjänsten

## Andra Recommendations {#other-recommendations}

### Ersätta administratörssessionen med en service-användare {#replacing-the-admin-session-with-a-service-user}

En tjänstanvändare är en JCR-användare utan lösenord och med en minimisängd behörigheter som krävs för att utföra en viss uppgift. Om du inte anger något lösenord går det inte att logga in med en tjänstanvändare.

Ett sätt att ersätta en administrativ session är att ersätta den med tjänstanvändarsessioner. Den kan vid behov även ersättas av flera undertjänstanvändare.

Om du vill ersätta administratörssessionen med en tjänstanvändare utför du följande steg:

1. Identifiera de behörigheter som krävs för tjänsten, med tanke på principen om minsta behörighet.
1. Kontrollera om det redan finns en användare med exakt den behörighetsinställning du behöver. Skapa en ny systemtjänstanvändare om ingen befintlig användare matchar dina behov. RTC krävs för att skapa en ny tjänstanvändare. Ibland kan det vara bra att skapa flera underleverantörer (t.ex. en för att skriva och en för att läsa) för att dela upp åtkomsten ännu mer.
1. Konfigurera och testa ACE:n för din användare.
1. Lägg till en `service-user`-mappning för tjänsten och för `user/sub-users`

1. Gör tjänsteanvändarens säljfunktion tillgänglig för ditt paket: uppdatera till den senaste versionen av `org.apache.sling.api`.

1. Ersätt `admin-session` i koden med API:erna för `loginService` eller `getServiceResourceResolver`.

## Skapar en ny tjänstanvändare {#creating-a-new-service-user}

När du har verifierat att ingen användare i listan över AEM användare kan användas för ditt användningsfall och att motsvarande RTC-problem har godkänts, kan du lägga till den nya användaren i standardinnehållet.

Rekommenderad metod är att skapa en tjänstanvändare som ska använda databasutforskaren på *https://&lt;server>:&lt;port>/crx/explorer/index.jsp*

Målet är att hämta en giltig `jcr:uuid`-egenskap som är obligatorisk för att skapa användaren via en innehållspaketinstallation.

Du kan skapa tjänstanvändare genom att:

1. Gå till databasutforskaren på *https://&lt;server>:&lt;port>/crx/explorer/index.jsp*
1. Logga in som administratör genom att trycka på länken **Logga in** i skärmens övre vänstra hörn.
1. Skapa och namnge sedan systemanvändaren. Om du vill skapa användaren som ett system anger du den mellanliggande sökvägen som `system` och lägger till valfria undermappar beroende på dina behov:

   ![chlimage_1-102](assets/chlimage_1-102a.png)

1. Kontrollera att systemanvändarnoden ser ut så här:

   ![chlimage_1-103](assets/chlimage_1-103a.png)

   >[!NOTE]
   >
   >Observera att det inte finns några blandningstyper associerade med tjänstanvändare. Det innebär att det inte finns några åtkomstkontrollprinciper för systemanvändare.

När du lägger till motsvarande .content.xml till innehållet i ditt paket måste du ange `rep:authorizableId` och att den primära typen är `rep:SystemUser`. Det borde se ut så här:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<jcr:root xmlns:jcr="https://www.jcp.org/jcr/1.0" xmlns:rep="internal"
    jcr:primaryType="rep:SystemUser"
    jcr:uuid="4917dd68-a0c1-3021-b5b7-435d0044b0dd"
    rep:principalName="authentication-service"
    rep:authorizableId="authentication-service"/>
```

## Lägger till en konfigurationsändring i ServiceUserMapper-konfigurationen {#adding-a-configuration-amendment-to-the-serviceusermapper-configuration}

Om du vill lägga till en mappning från tjänsten till motsvarande systemanvändare måste du skapa en fabrikskonfiguration för tjänsten ` [ServiceUserMapper](https://sling.apache.org/apidocs/sling7/org/apache/sling/serviceusermapping/ServiceUserMapper.html)`. För att behålla denna modulära form kan sådana konfigurationer tillhandahållas med [Ändra ](https://issues.apache.org/jira/browse/SLING-3578). Det rekommenderade sättet att installera sådana konfigurationer med ditt paket är att använda [Sling Initial Content Loading](https://sling.apache.org/documentation/bundles/content-loading-jcr-contentloader.html):

1. Skapa en undermapp SLING-INF/innehåll under mappen src/main/resources i paketet
1. I den här mappen skapar du en fil med namnet org.apache.sling.servicusermapping.impl.ServiceUserMapperImpl.changed-&lt;lite unikt namn för din fabrikskonfiguration>.xml med innehållet i din fabrikskonfiguration (inklusive alla användarmappningar för undertjänster). Exempel:

1. Skapa en `SLING-INF/content`-mapp under `src/main/resources`-mappen för ditt paket;
1. I den här mappen skapar du en fil `named org.apache.sling.serviceusermapping.impl.ServiceUserMapperImpl.amended-<a unique name for your factory configuration>.xml` med innehållet i din fabrikskonfiguration, inklusive alla användarmappningar för undertjänster.

   Ta filen `org.apache.sling.serviceusermapping.impl.ServiceUserMapperImpl.amended-com.adobe.granite.auth.saml.xml` som illustration:

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <node>
       <primaryNodeType>sling:OsgiConfig</primaryNodeType>
       <property>
           <name>user.default</name>
           <value></value>
       </property>
       <property>
           <name>user.mapping</name>
           <values>
               <value>com.adobe.granite.auth.saml=authentication-service</value>
           </values>
       </property>
   </node>
   ```

1. Referera det inledande Sling-innehållet i konfigurationen av `maven-bundle-plugin` i `pom.xml` för ditt paket. Exempel:

   ```xml
   <Sling-Initial-Content>
      SLING-INF/content;path:=/libs/system/config;overwrite:=true;
   </Sling-Initial-Content>
   ```

1. Installera paketet och kontrollera att fabrikskonfigurationen har installerats. Du kan göra detta genom att:

   * Gå till webbkonsolen på *https://serverhost:serveraddress/system/console/configMgr*
   * Sök efter **Tjänsttillägg för Apache Sling-tjänstens användarmappning**
   * Klicka på länken för att se om rätt konfiguration finns på plats.

## Hantera delade sessioner i tjänster {#dealing-with-shared-sessions-in-services}

Anrop till `loginAdministrative()` visas ofta tillsammans med delade sessioner. Dessa sessioner hämtas vid aktivering av tjänsten och loggas bara ut när tjänsten har stoppats. Även om detta är vanligt leder det till två problem:

* **Säkerhet:** Sådana administratörssessioner används för att cachelagra och returnera resurser eller andra objekt som är bundna till den delade sessionen. Senare i anropsstacken kan dessa objekt anpassas till sessioner eller resurslösare med utökad behörighet, och ofta är det inte tydligt för anroparen att det är en administratörssession som de arbetar med.
* **Prestanda:** I Oak-delade sessioner kan orsaka prestandaproblem, och det rekommenderas för närvarande inte att använda dem.

Den mest uppenbara lösningen för säkerhetsrisken är att helt enkelt ersätta `loginAdministrative()`-anropet med ett `loginService()`-anrop till en användare med begränsad behörighet. Detta påverkar dock inte eventuella prestandaförsämringar. En möjlighet att begränsa detta är att kapsla in all begärd information i ett objekt som inte har någon koppling till sessionen. Skapa sedan (eller förstör) sessionen på begäran.

Rekommenderad metod är att ändra funktionens API för att ge anroparen kontroll över skapandet/destruktionen av sessionen.

## Administrativa sessioner i JSP:er {#administrative-sessions-in-jsps}

JSP:er kan inte använda `loginService()` eftersom det inte finns någon associerad tjänst. Administrativa sessioner i JSP:er är dock vanligtvis ett tecken på överträdelse av MVC-paradigmen.

Detta kan åtgärdas på två sätt:

1. Omstrukturera innehållet på ett sätt som gör det möjligt att ändra det med användarsessionen.
1. Extraherar logiken till en tjänst som tillhandahåller ett API som sedan kan användas av JSP:n.

Den första metoden är den önskade.

## Bearbetningshändelser, replikeringsförprocessorer och jobb {#processing-events-replication-preprocessors-and-jobs}

När händelser eller jobb bearbetas, och i vissa fall arbetsflöden, förloras vanligtvis motsvarande session som utlöste händelsen. Detta leder till händelsehanterare och jobbbehandlare som ofta använder administrativa sessioner för att utföra sitt arbete. Det finns olika möjliga strategier för att lösa detta problem, vart och ett med sina fördelar och nackdelar:

1. Skicka `user-id` i händelsens nyttolast och använd personifiering.

   **Fördelar:** Enkelt att använda.

   **Nackdelar:** Använder fortfarande  `loginAdministrative()`. Den autentiserar en begäran som redan har autentiserats.

1. Skapa eller återanvänd en tjänstanvändare som har åtkomst till data.

   **Fördelar:** Konsekvent med den aktuella designen. Behöver minimala förändringar.

   **Nackdelar:** kräver att mycket kraftfulla tjänstanvändare är flexibla, vilket enkelt kan leda till eskalering av behörigheter. Omvandlar säkerhetsmodellen.

1. Skicka en serialisering av `Subject` i händelsenyttolasten och skapa en `ResourceResolver` baserad på det ämnet. Ett exempel är JAAS `doAsPrivileged` i `ResourceResolverFactory`.

   **Fördelar:** Ren implementering ur säkerhetssynpunkt. Det undviker omautentisering och arbetar med de ursprungliga behörigheterna. Kod som är relevant för säkerheten är transparent för händelsens konsument.

   **nackdelar:** behöver omfaktoriseras. Det faktum att den säkerhetsrelaterade koden som är genomskinlig för händelsekonsumenten också kan leda till problem.

Den tredje metoden är för närvarande den bästa behandlingstekniken.

## Arbetsflödesprocesser {#workflow-processes}

I implementeringar av arbetsflödesprocesser förloras vanligtvis motsvarande användarsession som utlöste arbetsflödet. Detta leder till arbetsflödesprocesser som ofta använder administrativa sessioner för att utföra sitt arbete.

För att åtgärda dessa problem rekommenderar vi att samma metoder som anges i [Bearbetningshändelser, Replikeringspreprocessorer och jobb](/help/sites-administering/security-service-users.md#processing-events-replication-preprocessors-and-jobs) används.

## Processorer för Sling-POST och borttagna sidor {#sling-post-processors-and-deleted-pages}

Det finns några administrativa sessioner som används för att skicka POST-processorimplementeringar. Vanligtvis används administrativa sessioner för att komma åt noder som väntar på att tas bort inom den POST som bearbetas. De är därför inte längre tillgängliga via begärandesessionen. En nod som väntar på att tas bort kan nås för att visa metadata som annars inte ska vara tillgängliga.
