---
title: Konfigurera integreringen med Adobe Target manuellt
seo-title: Manually Configuring the Integration with Adobe Target
description: Lär dig hur du konfigurerar integreringen med Adobe Target manuellt.
seo-description: Learn how to manually configure the integration with Adobe Target.
uuid: 0bb76a65-f981-4cc5-bee8-5feb3297137c
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 20c8eb1d-5847-4902-b7d3-4c3286423b46
exl-id: 0f710685-dc4f-4333-9847-d002b2637d08
source-git-commit: c96f83b84ed1473aee0ddcca08a0e585ec088aa1
workflow-type: tm+mt
source-wordcount: '2192'
ht-degree: 0%

---

# Konfigurera integreringen med Adobe Target manuellt {#manually-configuring-the-integration-with-adobe-target}

Du kan antingen ändra inställningarna för guiden för deltagande som du gjorde när du använde guiden, eller så kan du integrera manuellt med Adobe Target utan att använda guiden.

## Ändra konfiguration för guiden för anmälan {#modifying-the-opt-in-wizard-configurations}

The [Guiden Anmäl dig](/help/sites-administering/opt-in.md) att [integrerar AEM med Adobe Target](/help/sites-administering/target.md) skapar automatiskt en målmolnkonfiguration med namnet Provisioned Target Configuration. Guiden skapar också ett Target-ramverk för molnkonfigurationen med namnet Provisioned Target Framework. Du kan ändra egenskaperna för molnkonfigurationen och ramverket om det behövs.

Du kan också konfigurera Adobe Target att använda Adobe Target som rapportkälla när du riktar in innehåll genom att konfigurera A4T Analytics Cloud-konfigurationen.

Leta reda på molnkonfigurationen och ramverket genom att navigera till **Cloud Services** via **verktyg** > **Distribution** > **Cloud**. ([http://localhost:4502/libs/cq/core/content/tools/cloudservices.html](http://localhost:4502/libs/cq/core/content/tools/cloudservices.html)) Klicka eller tryck nedan på Adobe Target **Visa konfigurationer**.

### Etablerade egenskaper för målkonfiguration {#provisioned-target-configuration-properties}

Följande egenskapsvärden används i den konfiguration av molnet för konfiguration av etablerat mål som Opt-in-guiden skapar:

* **Klientkod:** Som du angett i guiden för anmälan.
* **E-post:** Som du angett i guiden för anmälan.
* **Lösenord:** Som du angett i guiden för anmälan.
* **API-typ:** REST
* **Synkronisera segment från Adobe Target:** Markerad.

* **Klientbibliotek:** mbox.js.
* **Använd DTM för att leverera klientbibliotek:** Inte markerat. Välj det här alternativet om du [använd DTM](/help/sites-administering/dtm.md) eller ett annat tagghanteringssystem som ska vara värd för filen mbox.js eller AT.js. Adobe rekommenderar att du använder DTM i stället för AEM för att leverera biblioteket.

* **Custom mbox.js:** Ingen har angetts så att standardfilen mbox.js används. Ange vid behov en anpassad mbox.js-fil som du vill använda. Visas bara om du har valt mbox.js.
* **Custom AT.js:** Ingen har angetts så att AT.js-standardfilen används. Ange en anpassad AT.js-fil som du vill använda efter behov. Visas bara om du har valt AT.js.

>[!NOTE]
>
>I AEM 6.3 kan du välja målbiblioteksfilen, [AT.JS](https://developer.adobe.com/target/implement/client-side/atjs/atjs-functions/mboxcreate-atjs/), som är ett nytt implementeringsbibliotek för Adobe Target som är utformat för både vanliga webbimplementeringar och ensidiga program.
>
>AT.js har flera förbättringar jämfört med mbox.js-biblioteket:
>
>* Förbättrade sidladdningstider för webbimplementeringar
>* Förbättrad säkerhet
>* Bättre implementeringsalternativ för single-page-applikationer
>* AT.js innehåller komponenterna som ingick i target.js, så det finns inte längre något anrop till target.


<!-- OLD URL WHICH IS 404 https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/mbox-implement/mbox-download.html -->

### Etablerade egenskaper för målramverk {#provisioned-target-framework-properties}

Det provisionerade målramverk som Opt-in-guiden skapar är konfigurerat att skicka kontextdata från profildatalagret. Lagringens ålder och könsposter skickas som standard till Target. Din lösning kräver förmodligen ytterligare parametrar för att skickas.

![chlimage_1-158](assets/chlimage_1-158.png)

Du kan konfigurera ramverket så att ytterligare kontextinformation skickas till Target enligt beskrivningen i [Lägga till ett målramverk](/help/sites-administering/target-configuring.md#adding-a-target-framework).

### Konfigurera A4T Analytics Cloud-konfiguration {#configuring-a-t-analytics-cloud-configuration}

Du kan konfigurera Adobe Target att använda Adobe Analytics som rapportkälla när du riktar in dig på innehåll.

>[!NOTE]
>
>Autentisering med användarautentiseringsuppgifter (äldre) fungerar inte med A4T (för både Target och Analytics). Kunder bör därför använda IMS-autentisering i stället för autentisering med användarautentiseringsuppgifter.

För att göra det anger du vilken A4T-molnkonfiguration som ska ansluta din Adobe Target-molnkonfiguration till:

1. Navigera till **Cloud Services** via **AEM logotyp** > **verktyg** > **Distribution** > **Cloud Services**.
1. I **Adobe Target** avsnitt, klicka **Konfigurera nu**.
1. Återanslut till din Adobe Target-konfiguration.
1. I **A4T Analytics Cloud-konfiguration** väljer du ramverket.

   >[!NOTE]
   >
   >Endast analyskonfigurationer som är aktiverade för A4T är tillgängliga.
   >
   >När du konfigurerar A4T med AEM kan du se att en Configuration-referens saknas. Så här kan du välja analysramverket:
   >
   >1. Navigera till **verktyg** > **Allmänt** > **CRXDE Lite**.
   1. Navigera till [Dialogrutan Konfiguration av A4T Analytics](#a4t-analytics-config-dialog) (se nedan)
   1. Ange egenskapen **disable** till **false**.
   1. Tryck eller klicka **Spara alla**.


#### Dialogrutan Konfiguration av A4T Analytics {#a4t-analytics-config-dialog}

```xml
/libs/cq/analytics/components/testandtargetpage/dialog/items/tabs/items/tab1_general/items/a4tAnalyticsConfig
```

![AdobeTargetSettings](assets/adobe-target-settings.jpg)

Klicka **OK**. När du skapar innehåll med Adobe Target kan du [välj rapportkälla](/help/sites-authoring/content-targeting-touch.md).

## Integrera manuellt med Adobe Target {#manually-integrating-with-adobe-target}

Integrera manuellt med Adobe Target i stället för att använda anmälningsguiden.

>[!NOTE]
Målbiblioteksfilen, [AT.JS](https://developer.adobe.com/target/implement/client-side/atjs/atjs-functions/mboxcreate-atjs/), är ett nytt implementeringsbibliotek för Adobe Target som är utformat för både vanliga webbimplementeringar och ensidiga program. Adobe rekommenderar att du använder AT.js i stället för mbox.js som klientbibliotek.
AT.js har flera förbättringar jämfört med mbox.js-biblioteket:
* Förbättrade sidladdningstider för webbimplementeringar
* Förbättrad säkerhet
* Bättre implementeringsalternativ för single-page-applikationer
* AT.js innehåller komponenterna som ingick i target.js, så det finns inte längre något anrop till target.js
>
Du kan välja AT.js eller mbox.js i **Klientbibliotek** nedrullningsbar meny.

<!-- OLD URL from above was 404 https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/mbox-implement/mbox-download.html -->

### Skapa en målmolnkonfiguration {#creating-a-target-cloud-configuration}

Om du vill att AEM ska kunna interagera med Adobe Target skapar du en Target-molnkonfiguration. Om du vill skapa konfigurationen anger du Adobe Target klientkod och inloggningsuppgifter.

Du skapar bara målmolnkonfigurationen en gång eftersom du kan associera konfigurationen med flera AEM kampanjer. Om du har flera Adobe Target-klientkoder skapar du en konfiguration för varje klientkod.

Du kan konfigurera molnkonfigurationen så att segment från Adobe Target synkroniseras. Om du aktiverar synkronisering importeras segment från Target i bakgrunden när molnkonfigurationen sparas.

Använd följande procedur för att skapa en Target-molnkonfiguration i AEM:

1. Navigera till **Cloud Services** via **AEM logotyp** > **verktyg** > **Cloud Services** > **Äldre Cloud Services**. ([http://localhost:4502/libs/cq/core/content/tools/cloudservices.html](http://localhost:4502/libs/cq/core/content/tools/cloudservices.html))

   The **Cloud Services** översiktssidan öppnas.

1. I **Adobe Target** avsnitt, klicka **Konfigurera nu**.
1. I **Skapa konfiguration** dialog:

   1. Ge konfigurationen en **Titel**.
   1. Välj **Adobe Target Configuration** mall.
   1. Klicka **Skapa**.

   Dialogrutan Redigera öppnas.

   ![AdobeTargetSettings](assets/adobe-target-settings.jpg)

   >[!NOTE]
   När du konfigurerar A4T med AEM kan du se att en Configuration-referens saknas. Så här kan du välja analysramverket:
   1. Navigera till **verktyg** > **Allmänt** > **CRXDE Lite**.
   1. Navigera till **/libs/cq/analytics/components/testandtarget page/dialog/items/tabs/items/tab1_general/items/a4tAnalyticsConfig**
   1. Ange egenskapen **disable** till **false**.
   1. Tryck eller klicka **Spara alla**.


1. Ange värden för de här egenskaperna i dialogrutan.

   * **Klientkod**: målkontots klientkod
   * **E-post**: Målkontots e-postadress.
   * **Lösenord**: lösenordet för målkontot.
   * **API-typ**: antingen REST eller XML
   * **A4T Analytics Cloud-konfiguration**: Välj den Analytics Cloud-konfiguration som används för mål och mått för aktivitet. Du behöver den här konfigurationen om du använder Adobe Analytics som rapportkälla när du riktar in innehåll. Om du inte ser din molnkonfiguration kan du läsa mer i [Konfigurera A4T Analytics Cloud-konfiguration](#configuring-a-t-analytics-cloud-configuration).

   * **Använd exakt målgruppsanpassning:** Som standard är den här kryssrutan markerad. Om du väljer det här alternativet väntar molntjänstkonfigurationen på att kontexten ska läsas in innan innehållet läses in. Se följande.
   * **Synkronisera segment från Adobe Target:** Välj det här alternativet så att du kan hämta segment som är definierade i Target för att använda dem i AEM. Välj det här alternativet när API-typegenskapen är REST, eftersom textbundna segment inte stöds och du måste använda segment från Target. (Den AEM termen segment motsvarar målgruppen.)
   * **Klientbibliotek:** Välj om du vill ha mbox.js- eller AT.js-klientbiblioteket.
   * **Använd DTM för att leverera klientbibliotek** - Välj det här alternativet om du vill använda AT.js eller mbox.js från DTM eller något annat tagghanteringssystem. Konfigurera [DTM-integrering](/help/sites-administering/dtm.md) om du vill använda det här alternativet. Adobe rekommenderar att du använder DTM i stället för AEM för att leverera biblioteket.
   * **Anpassad mbox.js**: Lämna tomt om du har markerat DTM-rutan eller om du vill använda mbox.js som standard. Du kan även överföra din anpassade mbox.js. Visas bara om du har valt mbox.js.
   * **Anpassad AT.js**: Lämna tomt om du har markerat DTM-rutan eller om du vill använda AT.js som standard. Du kan även överföra dina anpassade AT.js. Visas bara om du har valt AT.js.

   >[!NOTE]
   Som standard aktiveras korrekt målgruppsanpassning när du väljer att använda konfigurationsguiden för Adobe Target.
   Korrekt målinriktning innebär att molntjänstkonfigurationen väntar på att kontexten ska läsas in innan innehållet läses in. Därför kan en korrekt målinriktning i fråga om prestanda skapa en fördröjning på några millisekunder innan innehållet läses in.
   Korrekt målinriktning är alltid aktiverat på författarinstansen. På publiceringsinstansen kan du dock välja att inaktivera korrekt målanpassning globalt genom att avmarkera kryssrutan bredvid Korrekt målanpassning i molntjänstkonfigurationen (**http://localhost:4502/etc/cloudservices.html**). Du kan även aktivera och inaktivera exakt målinriktning för enskilda komponenter, oavsett vilken inställning du har i molntjänstkonfigurationen.
   Om du har ***redan*** har skapat riktade komponenter och du ändrar den här inställningen påverkar inte ändringarna dessa komponenter. Ändra dessa komponenter direkt.

1. Klicka **Anslut till mål** för att initiera anslutningen med Target. Om anslutningen lyckas visas meddelandet **Anslutningen lyckades** visas. Klicka **OK** i meddelandet och sedan **OK** i dialogrutan.

   Om du inte kan ansluta till Target kan du läsa [felsökning](/help/sites-administering/target-configuring.md#troubleshooting-target-connection-problems) -avsnitt.

### Lägga till ett målramverk {#adding-a-target-framework}

När du har konfigurerat molnkonfigurationen för Target lägger du till ett Target-ramverk. Ramverket identifierar de standardparametrar som skickas till Adobe Target från de tillgängliga [Klientkontext](/help/sites-administering/client-context.md) eller [ContextHub](/help/sites-developing/ch-configuring.md) -komponenter. Target använder parametrarna för att fastställa vilka segment som gäller för den aktuella kontexten.

Du kan skapa flera ramverk för en enda Target-konfiguration. Flera ramverk är användbara när du måste skicka en annan uppsättning parametrar till Target för olika delar av webbplatsen. Skapa ett ramverk för varje uppsättning parametrar som du skickar. Associera varje avsnitt på webbplatsen med rätt ramverk. En webbsida kan bara använda ett ramverk åt gången.

1. Klicka på knappen **+** (plustecken) bredvid Tillgängliga ramverk.
1. I dialogrutan Skapa ramverk anger du en **Titel** väljer du **Adobe Target Framework** och klicka **Skapa**.

   ![chlimage_1-161](assets/chlimage_1-161.png)

   Ramverkssidan öppnas. Sidekick innehåller komponenter som representerar information från [Klientkontext](/help/sites-administering/client-context.md) eller [ContextHub](/help/sites-developing/ch-configuring.md) som du kan mappa.

   ![chlimage_1-162](assets/chlimage_1-162.png)

1. Dra den klientkontextkomponent som representerar de data som du vill använda för mappning till släppmålet. Du kan också dra i **ContextHub Store** till ramverket.

   >[!NOTE]
   Vid mappning skickas parametrar till en mbox via enkla strängar. Du kan inte mappa arrayer från ContextHub.

   Använd till exempel **Profildata** om besökarna på er webbplats för att styra er Target-kampanj, dra **Profildata** till sidan. De profildatavariabler som är tillgängliga för mappning till Target-parametrar visas.

   ![chlimage_1-163](assets/chlimage_1-163.png)

1. Markera variablerna som du vill göra synliga för Adobe Target-systemet genom att markera **Dela** -kryssrutan i rätt kolumner.

   ![chlimage_1-164](assets/chlimage_1-164.png)

   >[!NOTE]
   Synkronisering av parametrar är bara ett sätt - från AEM till Adobe Target.

Ditt ramverk skapas. Om du vill replikera ramverket till publiceringsinstansen använder du **Aktivera ramverk** från sidosparken.

### Associera aktiviteter med målmolnkonfigurationen  {#associating-activities-with-the-target-cloud-configuration}

Associera dina [AEM](/help/sites-authoring/activitylib.md) med din Target-molnkonfiguration så att du kan spegla aktiviteterna i [Adobe Target](https://experienceleague.adobe.com/docs/target/using/experiences/offers/manage-content.html).

>[!NOTE]
Vilka typer av aktiviteter som är tillgängliga bestäms av följande:
* Om **xt_only** alternativet är aktiverat på Adobe Target-klienten (klientkod) som används på AEM för att ansluta till Adobe Target, så kan du skapa **endast** XT-aktiviteter inom AEM.
* Om **xt_only** option is **not** som är aktiverat på Adobe Target-klienten (klientkod) kan du skapa **båda** XT- och A/B-aktiviteter inom AEM.
>
**Ytterligare information:** **xt_only** är en inställning som används för en viss målklient (klientkod) och kan bara ändras direkt i Adobe Target. Du kan inte aktivera eller inaktivera det här alternativet i AEM.

### Koppla målramverket till din webbplats {#associating-the-target-framework-with-your-site}

När du har skapat ett Target-ramverk i AEM kopplar du dina webbsidor till ramverket. Målkomponenterna på sidorna skickar ramverksdefinierade data till Adobe Target för spårning. (Se [Målinriktat innehåll](/help/sites-authoring/content-targeting-touch.md).)

När du associerar en sida med ramverket ärver de underordnade sidorna associationen.

1. I **Webbplatser** navigera till platsen som du vill konfigurera.
1. Använda antingen [snabbåtgärder](/help/sites-authoring/basic-handling.md#quick-actions) eller [markeringsläge](/help/sites-authoring/basic-handling.md), markera **Visa egenskaper.**
1. Välj **Cloud Services** -fliken.
1. Tryck/klicka **Redigera**.
1. Tryck/klicka **Lägg till konfiguration** under **Cloud Service Configurations** och markera **Adobe Target**.

   ![chlimage_1-165](assets/chlimage_1-165.png)

1. Välj ramverket som du vill använda under **Konfigurationsreferens**.

   >[!NOTE]
   Se till att du väljer den specifika **ramverk** som du skapade och inte målmolnkonfigurationen som den skapades med.

1. Tryck/klicka **Klar**.
1. Aktivera webbplatsens rotsida så att du replikerar den till publiceringsservern. (Se [Publicera sidor](/help/sites-authoring/publishing-pages.md).)

   >[!NOTE]
   Om ramverket som du kopplade till sidan inte har aktiverats ännu öppnas en guide där du även kan publicera det.

## Felsöka problem med målanslutning {#troubleshooting-target-connection-problems}

Om du vill felsöka problem som uppstår vid anslutning till Target kan du utföra följande åtgärder:

* Kontrollera att de användaruppgifter du anger är korrekta.
* Kontrollera att AEM kan ansluta till målservern. Kontrollera till exempel att brandväggsreglerna inte blockerar utgående AEM eller att AEM har konfigurerats att använda nödvändiga proxy.
* Sök efter användbara meddelanden i AEM fellogg. Filen error.log finns i **crx-quickstart/logs** katalog där AEM är installerad.
* När du redigerar aktiviteten i Adobe Target pekar URL:en mot localhost. Undvik den här förståelsen genom att ange rätt URL för AEM Externalizer.
