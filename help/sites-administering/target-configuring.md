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
source-git-commit: baacb6623757c4a7a67ae2be4232a36c4a509b69
workflow-type: tm+mt
source-wordcount: '2196'
ht-degree: 0%

---

# Konfigurera integreringen med Adobe Target manuellt {#manually-configuring-the-integration-with-adobe-target}

Du kan antingen ändra inställningarna för guiden för deltagande som du gjorde när du använde guiden, eller så kan du integrera manuellt med Adobe Target utan att använda guiden.

## Ändra konfiguration för guiden för anmälan {#modifying-the-opt-in-wizard-configurations}

[Opt-in-guiden](/help/sites-administering/opt-in.md) som [integrerar AEM med Adobe Target](/help/sites-administering/target.md) skapar automatiskt en Target-molnkonfiguration med namnet Provisioned Target Configuration. Guiden skapar också ett Target-ramverk för molnkonfigurationen med namnet Provisioned Target Framework. Du kan ändra egenskaperna för molnkonfigurationen och ramverket om det behövs.

Du kan också konfigurera Adobe Target att använda Adobe Target som rapportkälla när du riktar in innehåll genom att konfigurera A4T Analytics Cloud-konfigurationen.

Navigera till **Cloud Services** via **Verktyg** > **Distribution** > **Cloud** för att hitta molnkonfigurationen och ramverket. ([http://localhost:4502/libs/cq/core/content/tools/cloudservices.html](http://localhost:4502/libs/cq/core/content/tools/cloudservices.html))
Klicka eller tryck på **Visa konfigurationer** nedan för Adobe Target.

### Etablerade egenskaper för målkonfiguration {#provisioned-target-configuration-properties}

Följande egenskapsvärden används i den konfiguration av molnet för konfiguration av etablerat mål som Opt-in-guiden skapar:

* **Klientkod:** Som anges i guiden för anmälan.
* **E-post:** Som du angett i guiden för anmälan.
* **Lösenord:** Som du angett i guiden för anmälan.
* **API-typ:** REST
* **Synkronisera segment från Adobe Target:** Markerat.

* **Klientbibliotek:** mbox.js.
* **Använd DTM för att leverera klientbiblioteket:** Inte markerat. Välj det här alternativet om du [använder DTM](/help/sites-administering/dtm.md) eller något annat tagghanteringssystem för att vara värd för filen mbox.js eller AT.js. Adobe rekommenderar att du använder DTM i stället för AEM för att leverera biblioteket.

* **Custom mbox.js:** None specified so that the default mbox.js file is used. Ange en anpassad mbox.js-fil som ska användas efter behov. Visas bara om du har valt mbox.js.
* **Anpassad AT.js:** None har angetts så att standardfilen AT.js används. Ange en anpassad AT.js-fil som ska användas efter behov. Visas bara om du har valt AT.js.

>[!NOTE]
>
>I AEM 6.3 kan du välja målbiblioteksfilen [AT.JS](https://docs.adobe.com/content/help/en/target/using/implement-target/client-side/mbox-implement/mbox-download.html), som är ett nytt implementeringsbibliotek för Adobe Target som är utformat för både vanliga webbimplementeringar och enkelsidiga program.
>
>AT.js har flera förbättringar jämfört med mbox.js-biblioteket:
>
>* Förbättrade sidladdningstider för webbimplementeringar
>* Förbättrad säkerhet
>* Bättre implementeringsalternativ för single-page-applikationer
>* AT.js innehåller komponenterna som ingick i target.js, så det finns inte längre något anrop till target.js


### Etablerade egenskaper för målramverk {#provisioned-target-framework-properties}

Det provisionerade målramverk som Opt-in-guiden skapar är konfigurerat att skicka kontextdata från profildatalagret. Lagringens ålder och könsposter skickas som standard till Target. Din lösning kräver förmodligen ytterligare parametrar för att skickas.

![chlimage_1-158](assets/chlimage_1-158.png)

Du kan konfigurera ramverket så att ytterligare kontextinformation skickas till Target enligt beskrivningen i [Lägga till ett målramverk](/help/sites-administering/target-configuring.md#adding-a-target-framework).

### Konfigurera A4T Analytics Cloud-konfiguration {#configuring-a-t-analytics-cloud-configuration}

Du kan konfigurera Adobe Target att använda Adobe Analytics som rapportkälla när du riktar in dig på innehåll.

>[!NOTE]
>
>Autentisering med användarautentiseringsuppgifter (äldre) fungerar inte med A4T (för både Target och Analytics). Kunder bör därför använda IMS-autentisering i stället för autentisering med användarautentiseringsuppgifter.

För att göra detta måste du ange vilken A4T-molnkonfiguration som ska ansluta din Adobe Target-molnkonfiguration med:

1. Navigera till **Cloud Services** via **AEM logotyp** > **Verktyg** > **Distribution** > **Cloud Services**.
1. I avsnittet **Adobe Target** klickar du på **Konfigurera nu**.
1. Återanslut till din Adobe Target-konfiguration.
1. I listrutan **A4T Analytics Cloud Configuration** väljer du ramverket.

   >[!NOTE]
   >
   >Endast analyskonfigurationer som är aktiverade för A4T är tillgängliga.
   >
   >När du konfigurerar A4T med AEM kan du se att en Configuration-referens saknas. Så här kan du välja analysramverket:
   >
   >1. Navigera till **Verktyg** > **Allmänt** > **CRXDE Lite**.
   1. Navigera till `/libs/cq/analytics/components/testandtargetpage/dialog/items/tabs/items/tab1_general/items/a4tAnalyticsConfig`
   1. Ange egenskapen **disable** till **false**.
   1. Tryck eller klicka på **Spara alla**.


   ![chlimage_1-159](assets/chlimage_1-159.png)

   Klicka på **OK**. När du skapar innehåll med Adobe Target kan du [välja rapportkälla](/help/sites-authoring/content-targeting-touch.md).

## Integrera manuellt med Adobe Target {#manually-integrating-with-adobe-target}

Integrera manuellt med Adobe Target i stället för att använda anmälningsguiden.

>[!NOTE]
Målbiblioteksfilen, [AT.JS](https://docs.adobe.com/content/help/en/target/using/implement-target/client-side/mbox-implement/mbox-download.html), är ett nytt implementeringsbibliotek för Adobe Target som är utformat för både vanliga webbimplementeringar och enkelsidiga program. Adobe rekommenderar att du använder AT.js i stället för mbox.js som klientbibliotek.
AT.js har flera förbättringar jämfört med mbox.js-biblioteket:
* Förbättrade sidladdningstider för webbimplementeringar
* Förbättrad säkerhet
* Bättre implementeringsalternativ för single-page-applikationer
* AT.js innehåller komponenterna som ingick i target.js, så det finns inte längre något anrop till target.js
Du kan välja AT.js eller mbox.js i listrutan **Klientbibliotek**.

### Skapa en målmolnkonfiguration {#creating-a-target-cloud-configuration}

Om du vill att AEM ska kunna interagera med Adobe Target skapar du en Target-molnkonfiguration. Om du vill skapa konfigurationen anger du Adobe Target klientkod och inloggningsuppgifter.

Du skapar bara målmolnkonfigurationen en gång eftersom du kan associera konfigurationen med flera AEM kampanjer. Om du har flera Adobe Target-klientkoder skapar du en konfiguration för varje klientkod.

Du kan konfigurera molnkonfigurationen så att segment från Adobe Target synkroniseras. Om du aktiverar synkronisering importeras segment från Target i bakgrunden så snart molnkonfigurationen har sparats.

Använd följande procedur för att skapa en Target-molnkonfiguration i AEM:

1. Navigera till **Cloud Services** via **AEM logotyp** > **Verktyg** > **Distribution** > **Cloud Services**. ([http://localhost:4502/libs/cq/core/content/tools/cloudservices.html](http://localhost:4502/libs/cq/core/content/tools/cloudservices.html))

   Översiktssidan för **Adobe Marketing Cloud** öppnas.

1. I avsnittet **Adobe Target** klickar du på **Konfigurera nu**.
1. I dialogrutan **Skapa konfiguration**:

   1. Ge konfigurationen en **titel**.
   1. Välj mallen **Adobe Target Configuration**.
   1. Klicka på **Skapa**.

   Dialogrutan Redigera öppnas.

   ![chlimage_1-160](assets/chlimage_1-160.png)

   >[!NOTE]
   När du konfigurerar A4T med AEM kan du se att en Configuration-referens saknas. Så här kan du välja analysramverket:
   1. Navigera till **Verktyg** > **Allmänt** > **CRXDE Lite**.
   1. Navigera till **/libs/cq/analytics/components/the standtarget page/dialog/items/tabs/items/tab1_general/items/a4tAnalyticsConfig**
   1. Ange egenskapen **disable** till **false**.
   1. Tryck eller klicka på **Spara alla**.


1. Ange värden för de här egenskaperna i dialogrutan.

   * **Klientkod**: målkontots klientkod
   * **E-post**: Målkontots e-postadress.
   * **Lösenord**: lösenordet för målkontot.
   * **API-typ**: antingen REST eller XML
   * **A4T Analytics Cloud-konfiguration**: Välj den Analytics-molnkonfiguration som används för målaktivitetsmål och -mått. Du behöver detta om du använder Adobe Analytics som rapportkälla när du skapar innehåll för målgruppsanpassning. Om du inte ser din molnkonfiguration läser du i [Konfigurera A4T Analytics Cloud Configuration](#configuring-a-t-analytics-cloud-configuration).

   * **Använd korrekt målinriktning:** Som standard är den här kryssrutan markerad. Om du väljer det här alternativet väntar molntjänstkonfigurationen på att kontexten ska läsas in innan innehållet läses in. Se följande.
   * **Synkronisera segment från Adobe Target:** Välj det här alternativet om du vill hämta segment som har definierats i Target för att använda dem i AEM. Du måste välja det här alternativet när API-typegenskapen är REST, eftersom infogade segment inte stöds och du alltid måste använda segment från Target. (Observera att den AEM termen segment motsvarar målgruppen.)
   * **Klientbibliotek:** Välj om du vill ha mbox.js- eller AT.js-klientbiblioteket.
   * **Använd DTM för att leverera klientbibliotek**  - Välj det här alternativet om du vill använda AT.js eller mbox.js från DTM eller något annat tagghanteringssystem. Du måste [konfigurera DTM-integreringen](/help/sites-administering/dtm.md) för att kunna använda det här alternativet. Adobe rekommenderar att du använder DTM i stället för AEM för att leverera biblioteket.
   * **Custom mbox.js**: Lämna tomt om du har markerat DTM-rutan eller om du vill använda mbox.js som standard. Du kan även överföra din anpassade mbox.js. Visas bara om du har valt mbox.js.
   * **Custom AT.js**: Lämna tomt om du har markerat DTM-rutan eller om du vill använda AT.js som standard. Du kan även överföra dina anpassade AT.js. Visas bara om du har valt AT.js.

   >[!NOTE]
   Som standard aktiveras korrekt målgruppsanpassning när du väljer att använda konfigurationsguiden för Adobe Target.
   Korrekt målinriktning innebär att molntjänstkonfigurationen väntar på att kontexten ska läsas in innan innehållet läses in. Därför kan en korrekt målinriktning i fråga om prestanda skapa en fördröjning på några millisekunder innan innehållet läses in.
   Korrekt målinriktning är alltid aktiverat på författarinstansen. På publiceringsinstansen kan du dock välja att inaktivera korrekt målinriktning globalt genom att avmarkera kryssrutan intill Accurate Targeting i molntjänstkonfigurationen (**http://localhost:4502/etc/cloudservices.html**). Du kan även aktivera och inaktivera exakt målinriktning för enskilda komponenter, oavsett vilken inställning du har i molntjänstkonfigurationen.
   Om du har ***redan*** skapat målkomponenter och du ändrar den här inställningen påverkar inte ändringarna dessa komponenter. Du måste göra ändringar i den komponenten direkt.

1. Klicka på **Anslut till mål** för att initiera anslutningen till mål. Om anslutningen lyckas visas meddelandet **Anslutningen lyckades**. Klicka på **OK** i meddelandet och **OK** i dialogrutan.

   Om du inte kan ansluta till Target kan du läsa avsnittet [felsökning](/help/sites-administering/target-configuring.md#troubleshooting-target-connection-problems).

### Lägga till ett målramverk {#adding-a-target-framework}

När du har konfigurerat molnkonfigurationen för Target lägger du till ett Target-ramverk. Ramverket identifierar de standardparametrar som skickas till Adobe Target från de tillgängliga [klientkontexterna](/help/sites-administering/client-context.md) eller [ContextHub](/help/sites-developing/ch-configuring.md)-komponenterna. Target använder parametrarna för att fastställa vilka segment som gäller för den aktuella kontexten.

Du kan skapa flera ramverk för en enda Target-konfiguration. Flera ramverk är användbara när du behöver skicka en annan uppsättning parametrar till Target för olika delar av webbplatsen. Skapa ett ramverk för varje uppsättning parametrar som du måste skicka. Associera varje avsnitt på webbplatsen med rätt ramverk. Observera att en webbsida bara kan använda ett ramverk åt gången.

1. På målkonfigurationssidan klickar du på **+** (plustecknet) bredvid Tillgängliga ramverk.
1. I dialogrutan Skapa ramverk anger du en **titel**, väljer **Adobe Target Framework** och klickar på **Skapa**.

   ![chlimage_1-161](assets/chlimage_1-161.png)

   Ramverkssidan öppnas. Sidekick innehåller komponenter som representerar information från [klientkontexten](/help/sites-administering/client-context.md) eller [ContextHub](/help/sites-developing/ch-configuring.md) som du kan mappa.

   ![chlimage_1-162](assets/chlimage_1-162.png)

1. Dra den klientkontextkomponent som representerar de data som du vill använda för mappning till släppmålet. Du kan också dra komponenten **ContextHub Store** till ramverket.

   >[!NOTE]
   Vid mappning skickas parametrar till en mbox via enkla strängar. Du kan inte mappa arrayer från ContextHub.

   Om du till exempel vill använda **Profildata** om webbplatsbesökarna för att styra målkampanjen drar du komponenten **Profildata** till sidan. De profildatavariabler som är tillgängliga för mappning till Target-parametrar visas.

   ![chlimage_1-163](assets/chlimage_1-163.png)

1. Markera de variabler som du vill göra synliga för Adobe Target-systemet genom att markera kryssrutan **Dela** i lämpliga kolumner.

   ![chlimage_1-164](assets/chlimage_1-164.png)

   >[!NOTE]
   Synkronisering av parametrar är bara ett sätt - från AEM till Adobe Target.

Ditt ramverk skapas. Om du vill replikera ramverket till publiceringsinstansen använder du alternativet **Aktivera ramverk** från sidosparken.

### Associera aktiviteter med målmolnkonfigurationen  {#associating-activities-with-the-target-cloud-configuration}

Associera dina [AEM aktiviteter](/help/sites-authoring/activitylib.md) med din Target-molnkonfiguration så att du kan spegla aktiviteterna i [Adobe Target](https://docs.adobe.com/content/help/en/target/using/experiences/offers/manage-content.html).

>[!NOTE]
Vilka typer av aktiviteter som är tillgängliga bestäms av följande:
* Om alternativet **xt_only** är aktiverat på Adobe Target-klienten (clientcode) som används på AEM för att ansluta till Adobe Target, kan du bara skapa **XT-aktiviteter i AEM.**
* Om alternativen **xt_only** är **inte** aktiverade för Adobe Target-klienten (klientkod) kan du skapa **både** XT- och A/B-aktiviteter i AEM.
**Ytterligare information:** **xt_** onlyoptions är en inställning som används för en viss målklient (clientcode) och kan bara ändras direkt i Adobe Target. Du kan inte aktivera eller inaktivera det här alternativet i AEM.

### Koppla målramverket till din webbplats {#associating-the-target-framework-with-your-site}

När du har skapat ett Target-ramverk i AEM kopplar du dina webbsidor till ramverket. Målkomponenterna på sidorna skickar ramverksdefinierade data till Adobe Target för spårning. (Se [Innehållsmål](/help/sites-authoring/content-targeting-touch.md).)

När du associerar en sida med ramverket ärver de underordnade sidorna associationen.

1. I konsolen **Platser** navigerar du till platsen som du vill konfigurera.
1. Välj [Visa egenskaper med antingen ](/help/sites-authoring/basic-handling.md#quick-actions) eller [markeringsläge](/help/sites-authoring/basic-handling.md).**Visa egenskaper.**
1. Markera fliken **Cloud Services**.
1. Tryck/klicka på **Redigera**.
1. Tryck/klicka på **Lägg till konfiguration** under **Konfigurationskonfigurationer** och välj **Adobe Target**.

   ![chlimage_1-165](assets/chlimage_1-165.png)

1. Välj det ramverk du vill använda under **Konfigurationsreferens**.

   >[!NOTE]
   Se till att du väljer det specifika **ramverket** som du skapade och inte den målmolnkonfiguration som det skapades under.

1. Tryck/klicka på **Klar**.
1. Aktivera webbplatsens rotsida för att replikera den till publiceringsservern. (Se [Publicera sidor](/help/sites-authoring/publishing-pages.md).)

   >[!NOTE]
   Om ramverket som du kopplade till sidan inte har aktiverats ännu öppnas en guide där du även kan publicera det.

## Felsöka problem med målanslutning {#troubleshooting-target-connection-problems}

Utför följande åtgärder för att felsöka problem som uppstår vid anslutning till Target:

* Kontrollera att de användaruppgifter du anger är korrekta.
* Kontrollera att AEM kan ansluta till målservern. Kontrollera till exempel att brandväggsreglerna inte blockerar utgående AEM eller att AEM har konfigurerats att använda nödvändiga proxy.
* Sök efter användbara meddelanden i AEM fellogg. Filen error.log finns i katalogen **crx-quickstart/logs** där AEM är installerad.
* När du redigerar aktiviteten i Adobe Target pekar URL:en mot localhost. Du kan undvika detta genom att ange rätt URL för AEM externalizer.
