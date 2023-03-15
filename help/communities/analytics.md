---
title: Analyskonfiguration för communityfunktioner
seo-title: Analytics Configuration for Communities Features
description: Konfigurera analys för Communities
seo-description: Configure analytics for Communities
uuid: 5a083645-9de6-4ecd-a94e-a40143f92edf
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: e6fdaf56-402f-418d-96d8-e46bd3ad1e8c
docset: aem65
role: Admin
exl-id: 7d54928b-6512-4da9-a209-eb4488bf2b64
source-git-commit: 0f7d4aba0b8c79039918e1338007a4277a5030f2
workflow-type: tm+mt
source-wordcount: '2717'
ht-degree: 2%

---

# Analyskonfiguration för communityfunktioner {#analytics-configuration-for-communities-features}

## Översikt {#overview}

Adobe Analytics och Adobe Experience Manager (AEM) är båda lösningar för Adobe Marketing Cloud.

Adobe Analytics kan konfigureras för AEM Communities så att händelser skickas till Adobe Analytics från vilka rapporter genereras när en medlem interagerar med funktioner som stöds i Communities.

När en medlem på en community-webbplats för aktivering till exempel visar en videoresurs som tilldelats dem, skickar resursspelaren händelser till Analytics, inklusive data om hjärtslag för video. Från communitywebbplatsen kan administratörer se olika rapporter om videouppspelningen.

Dessutom krävs analyser för att

* I publiceringsmiljön:

   * Rapportering om communityn [trender](/help/communities/trends.md)
   * Tillåter besökare att sortera efter&quot;mest visade&quot;,&quot;mest aktiva&quot;,&quot;mest gillade&quot;
   * Visa antal i UGC-listor

* I redigeringsmiljön:

   * Visning av deltagardata i [administrationskonsol för medlemmar](/help/communities/members.md) (vyer, inlägg, följare, gilla-markeringar)
   * Trend summary, video heartbeat and video device for enable resource [rapporter](/help/communities/reports.md)

Funktioner som stöds för Communities är:

* [Aktivera resurser](/help/communities/resources.md)
* [Forum](/help/communities/forum.md)
* [QnA](/help/communities/working-with-qna.md)
* [Blogg](/help/communities/blog-feature.md)
* [Filbibliotek](/help/communities/file-library.md)
* [Kalender](/help/communities/calendar.md)

I det här avsnittet av dokumentationen beskrivs hur du kopplar samman en Analytics-rapportsserie med communityfunktioner. De grundläggande stegen är:

1. [Replikera krypteringsnyckeln](#replicate-the-crypto-key) för att säkerställa att kryptering/dekryptering sker korrekt på alla AEM instanser
1. Förbered en Adobe Analytics [rapportsvit](#adobe-analytics-report-suite-for-video-reporting)
1. Skapa en AEM Analytics [molntjänst](#aem-analytics-cloud-service-configuration) och [ramverk](#aem-analytics-framework-configuration)

1. [Aktivera analys](#enable-analytics-for-a-community-site) för en community-webbplats
1. [**Verifiera**](#verify-analytics-to-aem-variable-mapping) Analys för AEM variabelmappning
1. Identifiera [primär utgivare](#primary-publisher)
1. [Publicera](#publish-community-site-and-analytics-cloud-service) communitywebbplatsen
1. Konfigurera [import av rapportdata](#obtaining-reports-from-analytics) från Adobe Analytics till communitysajten

## Förutsättningar {#prerequisites}

Om du vill konfigurera funktioner i Analytics for Communities måste du samarbeta med din kontorepresentant för att skapa ett Adobe Analytics-konto och [rapportsvit](#adobe-analytics-report-suite-for-video-reporting). När den är etablerad ska följande information finnas tillgänglig:

* **Företag**

   Det företag som är associerat med Adobe Analytics-kontot.

* **Användarnamn**

   Inloggningsanvändarnamnet för den användare som har behörighet att hantera Analytics-kontot (bör inkludera behörighet för Web Service Access).

* **Lösenord**

   Inloggningslösenordet för den behöriga användaren.

* **Analytics Data Center**

   URL:en till kontots Analytics-datacenter.

* **Report Suite**

   Namnet på analysrapportsviten som ska användas.

## Adobe Analytics Report Suite for Video Reporting {#adobe-analytics-report-suite-for-video-reporting}

Använda Adobe Marketing Clouds [Report Suite Manager](https://experienceleague.adobe.com/docs/analytics/admin/manage-report-suites/new-report-suite/new-report-suite.html)kan Analytics-rapportsviter konfigureras så att en communitywebbplats kan aktiveras för att ge rapporter om communityfunktioner.

Genom att logga in på [Adobe Experience Cloud](https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/home.html) med [Företagsnamn och användarnamn](/help/communities/analytics.md#prerequisites)kan du konfigurera en ny eller befintlig rapportserie så att den har:

* [11 Konverteringsvariabler](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/conversion-variables/conversion-var-admin.html) (Varor)

   * **`evar1`** via **`evar11`** aktiverad

   * Kan återanvända (byta namn på) befintliga e-variabler eller skapa nya som kan användas för webbgruppsfunktioner

* [7 Success Events](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/success-events/success-event.html) (händelser)

   * **`event1`** via **`event7`** aktiverad

   * type **`Counter`**

      * not **`Counter (no subrelations)`**
   * Kan återanvända (byta namn på) befintliga händelser eller skapa nya som kan användas för communityfunktioner


* [Videohantering](https://experienceleague.adobe.com/docs/media-analytics/using/media-overview.html)

   * Videorapportkonsol

      * Aktivera `Video Core`
      * Välj Spara
   * Mätkonsol för videokärna

      * Välj `Use Solution Variables`
      * Välj Spara


Om du använder en **ny rapportsvit** ska du vara medveten om att en ny rapportserie bara kan innehålla 4 variabler och 6 händelsvariabler, medan 11 variabler och 7 händelsvariabler krävs för Communities.

Om du använder en **befintlig rapportsvit** kan det vara nödvändigt att [ändra variabelmappningen](#modifying-analytics-variable-mapping) innan Analytics-ramverket aktiveras för en communitywebbplats.

Kontakta din kontorepresentant om du har några frågor om de variabler som är dedikerade till Communities.

>[!CAUTION]
>
>**Om du använder en befintlig rapportserie som redan använder variabler i**
>
>* **`evar1`** via **`evar11`**
>
>* **`event1`** via **`event7`**
>
>**Innan communitywebbplatsen publiceras** det är viktigt att återställa den befintliga mappningen genom att flytta de AEM variablerna som automatiskt mappades till analysvariabler när Analytics aktiverades för en communitywebbplats.
>
>Om du vill återställa den befintliga mappningen och flytta AEM till andra Analytics-variabler läser du avsnittet om [Ändra variabelmappning för analys](#modifying-analytics-variable-mapping).
>
>Om detta inte görs kan data gå förlorade.

### Analys av pulsslag för video {#video-heartbeat-analytics}

När Video Heartbeat Analytics är licensierad, `Marketing Cloud Org Id` är tilldelad.

Aktivera rapportering av pulsslag för video efter [konfigurera Analytics-rapportsviten för videorapportering](#adobe-analytics-report-suite-for-video-reporting):

* Skapa en [Molntjänst för Analytics](#aem-analytics-cloud-service-configuration)
* Aktivera [Analyser för en community-webbplats](#enable-analytics-for-a-community-site)
* Associera `Marketing Cloud Org Id` med communitywebbplatsen

The `Marketing Cloud Org Id` kan anges vid [communitysajt](/help/communities/sites-console.md#enablement) eller senare av [ändra](/help/communities/sites-console.md#modifying-site-properties) egenskaperna för communitywebbplatsen.

![marketing-org-id](assets/marketing-org-id.png)

När Video Heartbeat Analytics är aktiverat instansierar JavaScript-koden (JS) för videospelaren bibliotekskoden för pulsslag (även i JS), som hanterar all logik för att skicka videostatusuppdateringar till videospårningsservrarna i Analytics var 10:e sekund (inte konfigurerbar) och slutligen skickar en kumulativ rapport om videosessionen till huvudanalysservrarna.

Om det inte är aktiverat instansieras aldrig videons hjärtslagskod och endast videoförloppet och återupptagningspositionsspårning sparas i SRP för rapportering.

## AEM Analytics Cloud-tjänstkonfiguration {#aem-analytics-cloud-service-configuration}

Så här skapar du en ny Analytics-integrering, som integrerar Adobe Analytics med AEM communitywebbplats, med standardgränssnittet i författarinstansen:

* Från global navigering: **[!UICONTROL Tools]** > **[!UICONTROL Deployment]** > **[!UICONTROL Cloud Services]**
* Rulla ned till **[!UICONTROL Adobe Analytics]**
* Välj **[!UICONTROL Configure Now]** eller **[!UICONTROL Show Configurations]**

![cloud-config](assets/cloud-config1.png)

### Dialogrutan Skapa konfiguration {#create-configuration-dialog}

* Välj `[+]` ikon bredvid **[!UICONTROL  Available Configurations]** för att skapa en ny konfiguration

I dialogrutan Skapa konfiguration anger de värden som ska anges konfigurationen.

![create-cloud-config](assets/cloud-config2.png)

* **Titel**

   (Obligatoriskt) En visningsrubrik för konfigurationen.
Skriv till exempel *Aktivera communityanalys*

* **Namn**

   (Valfritt) Om inget anges används som standard ett giltigt nodnamn som härleds från titeln.
Skriv till exempel *communities*

* **Mall**

   Välj `Adobe Analytics Configuration`

* Välj **Skapa**

   * Öppnar konfigurationssidan `Analytics Settings` dialog

### Dialogrutan Analysinställningar {#analytics-settings-dialog}

När en ny Analytics-konfiguration skapas första gången visas konfigurationen och en ny dialogruta där Analytics-inställningarna kan anges. Den här dialogrutan kräver [information om förutsättningskonto](#prerequisites) som erhållits från kontoombudet.

![analytics-settings](assets/analytics-settings.png)

* **Företag**

   Det företag som är associerat med Adobe Analytics-kontot.

* **Användarnamn**

   Inloggningsanvändarnamnet för den användare som har behörighet att hantera Analytics-kontot.

* **Lösenord**

   Inloggningslösenordet för den behöriga användaren.

* **Datacenter**

   Välj det Analytics-datacenter som är värd för rapportsviten.

* **Lägg inte till spårningstagg på sida**

   Låt vara som standard (avmarkerat).

* **Använd AppMeasurement**

   Låt vara som standard (avmarkerat).

* **Importera inte sidvisningar varje kväll (författare)**

   Låt vara som standard (avmarkerat).

* **Importera inte sidvisningar direkt (publicera)**

   Låt vara som standard (avmarkerat).

Så här sparar du inställningarna:

* Välj **Anslut till Analytics**

   * Om det inte lyckas

      * Verifiera att posterna inte innehåller inledande blanksteg.
      * Testa ett annat datacenter.

* Välj **OK**.

   ![analytics-enablement-settings](assets/analytics-settings1.png)

### Skapa ramverk {#create-framework}

När du har konfigurerat den grundläggande anslutningen till Adobe Analytics måste du skapa eller redigera ett ramverk för communitywebbplatsen. Syftet med ramverket är att mappa AEM (Communities feature)-variabler till analysvariabler (report suite).

* Välj `[+]` ikon bredvid **[!UICONTROL  Available Frameworks]** skapa ett nytt ramverk

   ![analytics-framework](assets/analytics-framework.png)

* **Titel**

   (Obligatoriskt) En visningsrubrik för ramverket Skriv t.ex. *Aktivera EU-ramverk*.

* **Namn**

   (Valfritt) Om inget anges används som standard ett giltigt nodnamn som härleds från titeln.
Skriv till exempel *communities*.

* *Mall*

   Välj `Adobe Analytics Framework`.

* Välj **Skapa**.

Om du skapar Analytics Framework öppnas ramverket för konfiguration.

## Konfiguration av AEM Analytics Framework {#aem-analytics-framework-configuration}

Syftet med ramverket är att mappa AEM till analysvariabler (eVars och events). Analysvariablerna som är tillgängliga för mappning är [som definieras i rapportsviten](#adobe-analytics-report-suite-for-video-reporting).

![analytics-enablement-framework](assets/analytics-framework1.png)

### Välj Report Suite {#select-report-suite}

Välj den rapportsvit som har konfigurerats för videorapportering.

Om en rapportsvit ännu inte har skapats eller inte har konfigurerats på rätt sätt, se föregående avsnitt:
[Adobe Analytics Report Suite for Video Reporting](#adobe-analytics-report-suite-for-video-reporting)

Den idekiske behövs inte och kan minimeras så att den inte förhindrar åtkomst till inställningarna för Report Suites.

#### Dialogrutan Rapportsviter före och efter alternativet Lägg till objekt {#report-suites-dialog-before-and-after-selecting-add-item}

![report-suite](assets/report-suite.png)

1. Välj **Lägg till objekt +**.

   Två listrutor visas.

1. Välj en `Report suite.`

   Rapportsviterna som är kopplade till företagskontot kan väljas.

1. Välj **Ja** i dialogrutan som öppnas:

   ```
   Load default server settings?
    Do you want to load the default server settings and overwrite current values in the Server section?
   ```

1. Välj en `Run Mode`.

1. Välj **Publicera**.

![analytics-framework2](assets/analytics-framework2.png)

Molntjänsten och ramverket för Analytics är nu färdiga. Mappningarna definieras när en communitywebbplats har skapats med den här analystjänsten aktiverad.

## Aktivera analys för en communitywebbplats {#enable-analytics-for-a-community-site}

### Aktivera för ny community-plats {#enable-for-new-community-site}

Lägga till molntjänsten Analytics under [skapa en ny communitywebbplats](/help/communities/sites-console.md):

* I steg 3, under [Fliken ANALYTICS](/help/communities/sites-console.md#analytics):
   * Välj **Aktivera analys** kryssruta.
   * Välj ramverket i listrutan.

* Om du vill kan du gå tillbaka till Analytics-ramverkskonfigurationen och justera variabelmappningarna.

### Aktivera för befintlig communitywebbplats {#enable-for-existing-community-site}

Lägga till molntjänsten Analytics i en [befintlig communitywebbplats](/help/communities/sites-console.md#modifying-site-properties):

* Navigera till **Communities > Sites** konsol.
* Välj ikonen Redigera webbplats för communitywebbplatsen.
* Välj INSTÄLLNINGAR.
* I avsnittet Analytics:
   * Välj **Aktivera analys** kryssruta.
   * Välj ramverket i listrutan.

* Om du vill kan du gå tillbaka till Analytics-ramverkskonfigurationen och justera variabelmappningarna.

### Aktivera för anpassade platser {#enable-for-customized-sites}

För att Analytics-spårning och -import ska fungera på rätt sätt för en community-webbplats måste du skapa ett sidelement med `scf-js-site-title` class- och href-attribut måste finnas. Det får bara finnas ett sådant element på sidan, t.ex. i en oförändrad `sitepage.hbs` skript för en communitywebbplats. Värdet för `siteUrl` extraheras och skickas till Adobe Analytics som *webbplatssökväg*.

```xml
# present in default sitepage.hbs
# only one scf-js-site-title class should be included
# this example sets it to be hidden as it serves no visual purpose
<div
    class="navbar-brand scf-js-site-title"
    href="{{siteUrl}}.html"
    style="visibility: hidden;"
>
</div>
```

För **anpassad communitywebbplats** som övertäcker `sitepage.hbs` kontrollerar du att elementet finns. The `siteUrl` variabeln ställs in när den återges på servern innan den skickas till klienten.

För **allmän AEM** som innehåller webbgruppskomponenter, men som inte har skapats med [guide för att skapa webbplatser](/help/communities/sites-console.md)måste elementet läggas till. Värdet för href bör vara sökvägen till platsen. Om platssökvägen till exempel är `/content/my/company/en`och sedan använda:

```xml
<div
    class="navbar-brand scf-js-site-title"
    href="/content/my/company/en.html"
    style="visibility: hidden;"
>
</div>
```

## Funktioner i Analytics for Communities {#analytics-for-communities-features}

Analyser används automatiskt för flera communityfunktioner.

Författarmiljöns [OSGi-konfiguration](/help/sites-deploying/configuring-osgi.md), `AEM Communities Analytics Component Configuration`, innehåller en lista med de komponenter som har instrumenterats för Analytics. Den automatiska mappningen av variabler bestäms av komponenterna i listan.

Om nya anpassade komponenter skapas som är instrumenterade för Analytics, bör de läggas till i den här listan med konfigurerade komponenter.

### Komponentkonfiguration {#component-configuration}

![component-configuration1](assets/component-configuration1.png)

>[!NOTE]
>
>Journalkomponenterna används för att implementera bloggfunktionen.

### Mappade analyser till AEM variabler {#mapped-analytics-to-aem-variables}

När communitywebbplatsen har sparats med Analytics aktiverat och molnkonfigurationsramverket valt mappas AEM automatiskt till eVars och events som börjar med evar1 respektive event1 och ökar med 1.

Om du använder en befintlig rapportserie som har mappat någon av variablerna inom var1 till var11 och event1 till och med event7, måste du [mappa om AEM](#modifying-analytics-variable-mapping) och återställa den ursprungliga mappningen.

Följande är ett exempel på standardmappningar efter följande [komma igång, självstudiekurs](/help/communities/getting-started-enablement.md):

![map-analytics](assets/map-analytics1.png)

#### Karta över eVars som skickas med varje händelse {#map-of-evars-sent-with-each-event}

<table>
 <tbody>
  <tr>
   <td><strong> </strong></td>
   <td><strong>Aktivera<br /> Resurs<br /> Typ</strong></td>
   <td><strong>Plats<br /> Titel</strong></td>
   <td><strong>Funktion<br /> Typ</strong></td>
   <td><strong>Grupp<br /> Titel</strong></td>
   <td><strong>Grupp<br /> Bana</strong></td>
   <td><strong>UGC<br /> Typ</strong></td>
   <td><strong>UGC<br /> Titel</strong></td>
   <td><strong>Användare<br /> (Medlem)</strong></td>
   <td><strong>UGC<br /> Bana</strong></td>
   <td><strong>Plats<br /> Bana</strong></td>
  </tr>
  <tr>
   <td><strong> </strong></td>
   <td><strong>eVar1</strong></td>
   <td><strong>eVar2</strong></td>
   <td><strong>eVar3</strong></td>
   <td><strong>eVar4</strong></td>
   <td><strong>eVar5</strong></td>
   <td><strong>eVar6</strong></td>
   <td><strong>eVar7</strong></td>
   <td><strong>eVar8</strong></td>
   <td><strong>eVar9</strong></td>
   <td><strong>eVar10</strong></td>
  </tr>
  <tr>
   <td><strong>event1<br /> Resurs - uppspelning</strong></td>
   <td><em>(en)</em></td>
   <td><em>-</em></td>
   <td><em>-</em></td>
   <td><em>-</em></td>
   <td><em>-</em></td>
   <td><em>-</em></td>
   <td><em>-</em></td>
   <td><em>-</em></td>
   <td><em>(i)</em></td>
   <td><em>-</em></td>
  </tr>
  <tr>
   <td><strong>event2<br /> SCFView</strong></td>
   <td><em>(en)</em></td>
   <td><em>b)</em></td>
   <td><em>(c)</em></td>
   <td><em>(d)</em></td>
   <td><em>(e)</em></td>
   <td><em>(f)</em></td>
   <td><em>(g)</em></td>
   <td><em>(h)</em></td>
   <td><em>(i)</em></td>
   <td><em>(j)</em></td>
  </tr>
  <tr>
   <td><strong>event3<br /> SCFCreate (Post)</strong></td>
   <td><em>-</em></td>
   <td><em>b)</em></td>
   <td><em>(c)</em></td>
   <td><em>(d)</em></td>
   <td><em>(e)</em></td>
   <td><em>(f)</em></td>
   <td><em>(g)</em></td>
   <td><em>(h)</em></td>
   <td><em>(i)</em></td>
   <td><em>(j)</em></td>
  </tr>
  <tr>
   <td><strong>event4<br /> SCFFollow</strong></td>
   <td><em>-</em></td>
   <td><em>b)</em></td>
   <td><em>(c)</em></td>
   <td><em>(d)</em></td>
   <td><em>(e)</em></td>
   <td><em>(f)</em></td>
   <td><em>(g)</em></td>
   <td><em>(h)</em></td>
   <td><em>(i)</em></td>
   <td><em>(j)</em></td>
  </tr>
  <tr>
   <td><strong>event5<br /> SCFVoteUp</strong></td>
   <td><em>-</em></td>
   <td><em>b)</em></td>
   <td><em>(c)</em></td>
   <td><em>(d)</em></td>
   <td><em>(e)</em></td>
   <td><em>(f)</em></td>
   <td><em>(g)</em></td>
   <td><em>(h)</em></td>
   <td><em>(i)</em></td>
   <td><em>(j)</em></td>
  </tr>
  <tr>
   <td><strong>event6<br /> SCFVoteDown</strong></td>
   <td><em>-</em></td>
   <td><em>b)</em></td>
   <td><em>(c)</em></td>
   <td><em>(d)</em></td>
   <td><em>(e)</em></td>
   <td><em>(f)</em></td>
   <td><em>(g)</em></td>
   <td><em>(h)</em></td>
   <td><em>(i)</em></td>
   <td><em>(j)</em></td>
  </tr>
  <tr>
   <td><strong>event7<br /> SCFRate</strong></td>
   <td><em>-</em></td>
   <td><em>b)</em></td>
   <td><em>(c)</em></td>
   <td><em>(d)</em></td>
   <td><em>(e)</em></td>
   <td><em>(f)</em></td>
   <td><em>(g)</em></td>
   <td><em>(h)</em></td>
   <td><em>(i)</em></td>
   <td><em>(j)</em></td>
  </tr>
 </tbody>
</table>

**Exempel på eVar:**

* *[MIME-typ](https://www.iana.org/assignments/media-types)*: video/mp4
* *[communitytitel](/help/communities/sites-console.md#step13asitetemplate)*: Geometrixx Communities
* *[communityfunktionsnamn](/help/communities/functions.md)*: Forum
* *[communitygruppsnamn](/help/communities/creating-groups.md#creating-a-new-group)*: Vattna
* *sökväg till communitygruppsinnehåll*: `/content/sites/<site name>/en/groups/hiking`
* *[UGC-komponentresurstyp](/help/communities/essentials.md)*: `social/forum/components/hbs/topic`
* *Rubrik för UGC-komponent*: Hiking Topics
* *login (authzableId)*: `aaron.mcdonald@mailinator.com`
* *SRP-sökväg till UGC*: `/content/usergenerated/asi/.../forum/jmtz-topic3`
eller 
*sökväg för komponenten som ska följas*: `/content/sites/<site name>/en/jcr:content/content/primary/forum`

* *sökväg till innehåll på communitysajten*: `/content/sites/<site name>/en`

### Ändra variabelmappning för analys {#modifying-analytics-variable-mapping}

Mappningen av eVars och händelser för Analytics till AEM-variabler visas i ramverkskonfigurationen när Analytics har aktiverats för en community-webbplats.

När Analytics har aktiverats och innan communitywebbplatsen publiceras kan mappningen ändras i ramverket genom att dra önskad Analytics-evar eller -händelse från den vänstra listen och släppa den på den relevanta raden i mappningstabellen.

För att undvika dubblettmappningar måste du se till att ta bort den ersatta Analytics-instansen eller händelsen från raden genom att hålla markören över den och välja &quot;X&quot; som visas till höger om variabelelementet Analytics.

Om Communities eVars och events skriver över mappningar som fanns tidigare i rapportsviten bör du, för att undvika dataförluster, tilldela AEM variabler för Communities-funktioner till andra Analytics eVars eller händelser och återställa de ursprungliga mappningarna.

>[!CAUTION]
>
>Det är viktigt att fortsätta innan communitywebbplatsen är [publicerad](#publishing-the-community-site) med Analytics aktiverat, annars finns det risk för dataförlust.

#### Exempelsteg 1: Dra Analytics evar14 till mappningstabellen {#example-step-dragging-analytics-evar-into-mapping-table}

![analytics-mapping-evar](assets/analytics-mapping-evar.png)

#### Exempelsteg 2: Välja &#39;x&#39; för att ta bort ersatt evar11 {#example-step-selecting-x-to-remove-replaced-evar}

![analytics-mapping-evar1](assets/analytics-mapping-evar1.png)

#### Exempelsteg 3: AEM var eventdata.siteId ommappas till Analytics evar14 {#example-step-aem-var-eventdata-siteid-remapped-to-analytics-evar}

![analytics-mapping-evar2](assets/analytics-mapping-evar2.png)

## Publicera communitywebbplatsen {#publishing-the-community-site}

### Verifiera analyser för att AEM variabelmappning {#verify-analytics-to-aem-variable-mapping}

Det är klokt att verifiera variabelmappningen innan communitywebbplatsen publiceras, som även publicerar molntjänsten och ramverket för Analytics.

Se avsnitt:

* [Mappade analyser till AEM variabler](#mapped-analytics-to-aem-variables)
* [Ändra variabelmappning för analys](#modifying-analytics-variable-mapping)

>[!CAUTION]
>
>**Om du använder en befintlig rapportserie som redan använder variabler i**
>
>* **`evar1`** via **`evar11`**
>
>* **`event1`** via **`event7`**
>
>**Innan communitywebbplatsen publiceras** Det är viktigt att återställa den befintliga mappningen och flytta de Web AEM-variabler som automatiskt mappades (när Analytics aktiverades för communitywebbplatsen) till andra Analytics-variabler. Den här ommappningen bör vara konsekvent för alla webbgruppskomponenter.
>
>Om detta inte görs kan data gå förlorade.

### Primär utgivare {#primary-publisher}

När den valda distributionen är en [publicera servergrupp](/help/communities/topologies.md#tarmk-publish-farm)måste en AEM publiceringsinstans identifieras som primär utgivare för att avfråga Adobe Analytics efter rapportdata att skriva till [SRP](/help/communities/working-with-srp.md).

Som standard är `AEM Communities Publisher Configuration` OSGi-konfigurationen identifierar sin publiceringsinstans som primär utgivare, så att alla publiceringsinstanser i en publiceringsgrupp identifierar sig själva som primär.

Det är därför nödvändigt att redigera konfigurationen på alla sekundära publiceringsinstanser för att avmarkera **Primär utgivare** kryssruta.

Specifika anvisningar finns i avsnittet om primär utgivare i [Distribuera webbgrupper](/help/communities/deploy-communities.md#primary-publisher).

>[!CAUTION]
>
>Det är viktigt att den primära utgivaren är konfigurerad för att förhindra avsökning från flera publiceringsinstanser.

### Replikera krypteringsnyckeln {#replicate-the-crypto-key}

Adobe Analytics-autentiseringsuppgifterna är krypterade. För att underlätta replikering eller överföring av krypterade analysreferenser mellan författare och utgivare måste alla AEM instanser ha samma primära krypteringsnyckel.

Följ instruktionerna på [Replikera krypteringsnyckeln](/help/communities/deploy-communities.md#replicate-the-crypto-key).

### Publicera communitywebbplats och Analytics Cloud-tjänst {#publish-community-site-and-analytics-cloud-service}

När molntjänsten Analytics har aktiverats för en community-webbplats och, om det behövs, för [mappning av analyser till AEM variabler har justerats](#mapped-analytics-to-aem-variables)måste konfigurationen replikeras till publiceringsmiljön med [publicera communitywebbplatsen](/help/communities/sites-console.md#publishing-the-site).

## Få rapporter från Analytics {#obtaining-reports-from-analytics}

### Rapporthantering {#report-management}

Författaren och den primära utgivarens [OSGi-konfiguration](/help/sites-deploying/configuring-osgi.md), `AEM Communities Analytics Report Management`, används för att fråga Analytics.

Frågorna gäller för realtidsrapporter.

På den primära utgivaren används frågorna för att tillhandahålla information som förberedelse för Report-importerarens Analytics-dataimport.

Frågeintervallet är som standard 10 sekunder.

### Rapportimporteraren {#report-importer}

När en webbplats som aktiverats i Analytics har publicerats är den primära utgivarens [OSGi-konfiguration](/help/sites-deploying/configuring-osgi.md), `AEM Communities Analytics Report Importer`, kan konfigureras för att ange standardavsökningsintervallet för de konfigurationer som inte konfigureras individuellt i CRXDE.

Avsökningsintervallet styr hur ofta förfrågningar till Adobe Analytics om data ska hämtas och sparas i [SRP](/help/communities/working-with-srp.md).

När data kan kategoriseras som&quot;big data&quot; kan en mer frekvent undersökning innebära en stor belastning på communitywebbplatsen.

Standardavsökningen **Importintervall** är inställt på 12 timmar.

![rapportör](assets/report-importer.png)

### Anpassning av komponentrapport {#component-report-customization}

För att anpassa mätvärdena för att spåra skapas för närvarande noder i databasen som definierar tidsperioder för vilka en rapport om mätvärdena ska genereras.

Forum-ämnet är för närvarande det enda exemplet på den här anpassningen:

* Logga in med administratörsbehörighet på den primära utgivaren.
* Navigera till [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md). Till exempel: [https://localhost:4503/crx/de](https://localhost:4503/crx/de).

* Under jcr:content-noden i språkroten (till exempel `/content/sites/engage/en/jcr:content),`navigera till komponenten som konfigurerats för Analytics-rapportering.
Till exempel, **`analytics/reportConfigs/social_forum_components_hbs_topic`**

* Observera de skapade tidsperioderna:

   * `last30Days`
   * `last90Days`
   * `thisYear`

* Lägg märke till `total`nod.

   * Ändra **`interval`** egenskapen åsidosätter rapportimporterarens intervall.
   * Värdet anges i sekunder och är inställt på 4 timmar (1 400 sekunder).

![komponentrapport](assets/component-report.png)

## Hantera användardata i Analytics {#manage-user-data-in-analytics}

Adobe Analytics tillhandahåller API:er som gör att du kan komma åt, exportera och ta bort användardata. Mer information finns i [Skicka in begäran om åtkomst och borttagning](https://experienceleague.adobe.com/docs/analytics/admin/data-governance/gdpr-submit-access-delete.html).

## Resurser {#resources}

* Adobe Experience Cloud: [Hjälp och referens för analyser](https://experienceleague.adobe.com/docs/analytics.html)
* AEM: [Integrera med Adobe Analytics](/help/sites-administering/adobeanalytics.md)
* AEM: [Analyser med externa leverantörer](/help/sites-administering/external-providers.md)
