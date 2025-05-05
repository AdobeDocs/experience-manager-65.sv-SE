---
title: Analyskonfiguration för communityfunktioner
description: Lär dig hur du konfigurerar Adobe Analytics för AEM Communities så att händelser skickas till Adobe Analytics när en medlem interagerar med funktioner som stöds i Communities.
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
docset: aem65
role: Admin
exl-id: 7d54928b-6512-4da9-a209-eb4488bf2b64
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '2644'
ht-degree: 0%

---

# Analyskonfiguration för communityfunktioner {#analytics-configuration-for-communities-features}

## Ökning {#overview}

Adobe Analytics och Adobe Experience Manager (AEM) är båda lösningar för Adobe Experience Cloud.

Adobe Analytics kan konfigureras för AEM Communities så att händelser skickas till Adobe Analytics från vilka rapporter genereras när en medlem interagerar med funktioner som stöds i Communities.

Administratörer kan t.ex. se olika rapporter om videouppspelningen på communitywebbplatsen.

Dessutom krävs analyser för att

* I Publish-miljön:

   * Rapportering om [communitytrender](/help/communities/trends.md)
   * Tillåter besökare att sortera efter&quot;mest visade&quot;,&quot;mest aktiva&quot;,&quot;mest gillade&quot;
   * Visa antal i UGC-listor (användargenererat innehåll)

* I redigeringsmiljön:

   * Visning av deltagardata i [medlemskonsolen](/help/communities/members.md) (vyer, inlägg, följare, gilla-markeringar)
   * Trendsammanfattning, videominnesslag och videoenhet för aktiveringsresursen [reports](/help/communities/reports.md)

Funktioner som stöds för Communities är:

* [Forum](/help/communities/forum.md)
* [QnA](/help/communities/working-with-qna.md)
* [Blogg](/help/communities/blog-feature.md)
* [Filbibliotek](/help/communities/file-library.md)
* [Kalender](/help/communities/calendar.md)

I det här avsnittet av dokumentationen beskrivs hur du kopplar samman en Analytics-rapportsserie med communityfunktioner. De grundläggande stegen är:

1. [Replikera krypteringsnyckeln](#replicate-the-crypto-key) så att du kan säkerställa att kryptering/dekryptering sker korrekt på alla AEM instanser
1. Förbered en Adobe Analytics [rapportserie](#adobe-analytics-report-suite-for-video-reporting)
1. Skapa en AEM Analytics [Cloud-tjänst](#aem-analytics-cloud-service-configuration) och [ramverk](#aem-analytics-framework-configuration)

1. [Aktivera analys](#enable-analytics-for-a-community-site) för en community-webbplats
1. [**Verifiera**](#verify-analytics-to-aem-variable-mapping)-analys för att AEM variabelmappning
1. Identifiera [primär utgivare](#primary-publisher)
1. [Publish](#publish-community-site-and-analytics-cloud-service) - communitywebbplatsen
1. Konfigurera [import av rapportdata](#obtaining-reports-from-analytics) från Adobe Analytics till communitywebbplatsen

## Förutsättningar {#prerequisites}

Om du vill konfigurera Analytics för communityfunktioner måste du arbeta med din kontorepresentant för att skapa ett Adobe Analytics-konto och [rapporteringsprogramsvit](#adobe-analytics-report-suite-for-video-reporting). När den är etablerad ska följande information finnas tillgänglig:

* **Företagsnamn**

  Det företag som är associerat med Adobe Analytics-kontot.

* **Användarnamn**

  Inloggningsanvändarnamnet för den användare som har behörighet att hantera Analytics-kontot
(bör inkludera behörighet för webbtjänståtkomst).

* **Lösenord**

  Inloggningslösenordet för den behöriga användaren.

* **Analytics-datacenter**

  URL:en till kontots Analytics-datacenter.

* **Report Suite**

  Namnet på analysrapportsviten som ska användas.

## Adobe Analytics Report Suite for Video Reporting {#adobe-analytics-report-suite-for-video-reporting}

Med Adobe Experience Cloud [Report Suite Manager](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/manage-report-suites/c-new-report-suite/new-report-suite.html?lang=sv-SE) kan Analytics-rapportsviter konfigureras så att en communitywebbplats kan aktiveras för att tillhandahålla rapporter om communityfunktioner.

Genom att logga in på [Adobe Experience Cloud](https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/home.html?lang=sv-SE) med [Företagsnamn och användarnamn](/help/communities/analytics.md#prerequisites) kan du konfigurera en ny eller befintlig rapportserie så att den har:

* [11 Konverteringsvariabler](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/conversion-variables/conversion-var-admin.html?lang=sv-SE) (eVars)

   * **`evar1`** till och med **`evar11`** aktiverat

   * Kan återanvända (byta namn på) befintliga e-variabler eller skapa sådana som kan användas för webbgruppsfunktioner

* [7 lyckade händelser](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/conversion-variables/success-events/success-event.html?lang=sv-SE) (händelser)

   * **`event1`** till och med **`event7`** aktiverat

   * typ **`Counter`**

      * inte **`Counter (no subrelations)`**

   * Kan återanvända (byta namn på) befintliga händelser eller skapa händelser som ska användas för communityfunktioner

* [Videohantering](https://experienceleague.adobe.com/docs/media-analytics/using/media-overview.html?lang=sv-SE)

   * Videorapportkonsol

      * Aktivera `Video Core`
      * Välj Spara

   * Mätkonsol för videokärna

      * Välj `Use Solution Variables`
      * Välj Spara

Om du använder en **ny rapportserie** kan en ny rapportserie endast innehålla 4 variabler och 6 händelsvariabler, medan 11 variabler och 7 händelsvariabler krävs för Communities.

Om du använder en **befintlig rapportserie** kan det vara nödvändigt att [ändra variabelmappningen](#modifying-analytics-variable-mapping) innan Analytics-ramverket aktiveras för en community-webbplats.

Kontakta din kontorepresentant om du har några frågor om de variabler som är dedikerade till Communities.

>[!CAUTION]
>
>**Om du använder en befintlig rapportserie som redan använder variabler inom**
>
>* **`evar1`** till **`evar11`**
>
>* **`event1`** till **`event7`**
>
>**Innan communitywebbplatsen publiceras** är det viktigt att återställa den befintliga mappningen genom att flytta de AEM variablerna som automatiskt mappades till Analytics-variabler när Analytics aktiverades för en community-webbplats.
>
>Om du vill återställa den befintliga mappningen och flytta AEM till andra analysvariabler läser du avsnittet [Ändra analysvariabelmappning](#modifying-analytics-variable-mapping).
>
>Om detta inte görs kan data gå förlorade.

### Analys av pulsslag för video {#video-heartbeat-analytics}

När Video Heartbeat Analytics licensieras tilldelas en `Marketing Cloud Org Id`.

Så här aktiverar du rapporter om pulsslag för video efter [att Analytics-rapportsviten har konfigurerats för videorapportering](#adobe-analytics-report-suite-for-video-reporting):

* Skapa en [Analytics Cloud-tjänst](#aem-analytics-cloud-service-configuration)
* Aktivera [Analyser för en communitywebbplats](#enable-analytics-for-a-community-site)
* Associera `Marketing Cloud Org Id` med communitywebbplatsen

`Marketing Cloud Org Id` kan anges när [en community-webbplats skapas](/help/communities/sites-console.md) eller senare genom att [ändra](/help/communities/sites-console.md#modifying-site-properties) community-webbplatsegenskaperna.

![marketing-org-id](assets/marketing-org-id.png)

När videohjärtslagsanalys är aktiverat instansierar JS-koden (JavaScript) för videospelaren bibliotekskoden för pulsslag (även i JS). Koden hanterar all logik för att skicka videostatusuppdateringar till videospårningsservrarna i Analytics var 10:e sekund (kan inte konfigureras). Till slut skickas en kumulativ rapport från videosessionen till huvudanalysservrarna.

Om det inte är aktiverat instansieras aldrig videons hjärtslagskod och endast videoförloppet och återupptagningspositionsspårning sparas i SRP för rapportering.

## AEM Analytics Cloud-tjänstkonfiguration {#aem-analytics-cloud-service-configuration}

Så här skapar du en Analytics-integrering, som integrerar Adobe Analytics med AEM communitywebbplats, med standardgränssnittet i författarinstansen:

* Från global navigering: **[!UICONTROL Tools]** > **[!UICONTROL Deployment]** > **[!UICONTROL Cloud Services]**
* Rulla ned till **[!UICONTROL Adobe Analytics]**
* Välj **[!UICONTROL Configure Now]** eller **[!UICONTROL Show Configurations]**

![cloud-config](assets/cloud-config1.png)

### Dialogrutan Skapa konfiguration {#create-configuration-dialog}

* Välj ikonen `[+]` bredvid **[!UICONTROL Available Configurations]** så att du kan skapa en konfiguration.

I dialogrutan Skapa konfiguration anger de värden som ska anges konfigurationen.

![create-cloud-config](assets/cloud-config2.png)

* **Titel**

  (Obligatoriskt) En visningsrubrik för konfigurationen.
Ange till exempel *Community Analytics*

* **Namn**

  (Valfritt) Om inget anges blir namnet som standard ett giltigt nodnamn som härleds från titeln.
Ange till exempel *communities*

* **Mall**

  Välj `Adobe Analytics Configuration`

* Välj **Skapa**

   * Startar konfigurationssidan och öppnar dialogrutan `Analytics Settings`

### Dialogrutan Analysinställningar {#analytics-settings-dialog}

När en ny Analytics-konfiguration skapas första gången visas konfigurationen och en ny dialogruta där Analytics-inställningarna kan anges. Den här dialogrutan kräver den [nödvändiga kontoinformationen](#prerequisites) från kontoombudet.

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

* Välj **Anslut till analys**

   * Om det inte lyckas

      * Kontrollera att posterna inte innehåller inledande blanksteg.
      * Testa ett annat datacenter.

* Välj **OK**.

  ![analytics-settings](assets/analytics-settings1.png)

### Skapa ramverk {#create-framework}

När du har konfigurerat den grundläggande anslutningen till Adobe Analytics måste du skapa eller redigera ett ramverk för communitywebbplatsen. Syftet med ramverket är att mappa AEM (Communities feature)-variabler till analysvariabler (report suite).

* Välj ikonen `[+]` bredvid **[!UICONTROL &#x200B; Available Frameworks]** så att du kan skapa ett ramverk.

  ![analytics-framework](assets/analytics-framework.png)

* **Titel**

  (Obligatoriskt) En visningsrubrik för ramverket
Ange till exempel *Community Framework*.

* **Namn**

  (Valfritt) Om inget anges blir namnet som standard ett giltigt nodnamn som härleds från titeln.
Ange till exempel *communities*.

* *Mall*

  Välj `Adobe Analytics Framework`.

* Välj **Skapa**.

Om du skapar Analytics Framework öppnas ramverket för konfiguration.

## Konfiguration av AEM Analytics Framework {#aem-analytics-framework-configuration}

Syftet med ramverket är att mappa AEM till analysvariabler (eVars och events). Analysvariablerna som är tillgängliga för mappning är [definierade i rapportsviten](#adobe-analytics-report-suite-for-video-reporting).

![analytics-framework](assets/analytics-framework1.png)

### Välj Report Suite {#select-report-suite}

Välj den rapportsvit som har konfigurerats för videorapportering.

Om en rapportsvit ännu inte har skapats eller inte har konfigurerats på rätt sätt, se föregående avsnitt:
[Adobe Analytics Report Suite for Video Reporting](#adobe-analytics-report-suite-for-video-reporting)

Sidekick behövs inte och kan minimeras så att det inte förhindrar åtkomst till inställningarna för rapportsviterna.

#### Dialogrutan Rapportsviter före och efter alternativet Lägg till objekt {#report-suites-dialog-before-and-after-selecting-add-item}

![report-suite](assets/report-suite.png)

1. Välj **Lägg till objekt +**.

   Två listrutor visas.

1. Välj en `Report suite.`

   Rapportsviterna som är kopplade till företagskontot kan väljas.

1. Välj **Ja** i den dialogruta som öppnas:

   ```
   Load default server settings?
    Do you want to load the default server settings and overwrite current values in the Server section?
   ```

1. Välj en `Run Mode`.

1. Välj **Publish**.

![analytics-framework2](assets/analytics-framework2.png)

Molntjänsten och ramverket för Analytics är nu färdiga. Mappningarna definieras efter att en communitywebbplats har skapats med den här analystjänsten aktiverad.

## Aktivera analys för en communitywebbplats {#enable-analytics-for-a-community-site}

### Aktivera för ny community-plats {#enable-for-new-community-site}

Så här lägger du till Analytics Cloud-tjänsten när [en community-webbplats skapas](/help/communities/sites-console.md):

* I steg 3, under fliken [ANALYTICS](/help/communities/sites-console.md#analytics):
   * Markera kryssrutan **Aktivera analys**.
   * Välj ramverket i listrutan.

* Om du vill kan du gå tillbaka till Analytics-ramverkskonfigurationen och justera variabelmappningarna.

### Aktivera för befintlig communitywebbplats {#enable-for-existing-community-site}

Så här lägger du till Analytics Cloud-tjänsten på en [befintlig communitywebbplats](/help/communities/sites-console.md#modifying-site-properties):

* Navigera till konsolen **Communities > Sites**.
* Välj ikonen Redigera webbplats för communitywebbplatsen.
* Välj INSTÄLLNINGAR.
* I avsnittet Analytics (Analyser):
   * Markera kryssrutan **Aktivera analys**.
   * Välj ramverket i listrutan.

* Om du vill kan du gå tillbaka till Analytics-ramverkskonfigurationen och justera variabelmappningarna.

### Aktivera för anpassade platser {#enable-for-customized-sites}

För att Analytics-spårning och -import ska fungera korrekt för en community-webbplats måste det finnas ett sidelement med attributen `scf-js-site-title` och href. Det får bara finnas ett sådant element på sidan, t.ex. det i ett `sitepage.hbs`-skript som inte ändrats för en community-webbplats. Värdet för `siteUrl` extraheras och skickas till Adobe Analytics som *webbplatssökväg*.

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

Kontrollera att elementet finns för en **anpassad communitywebbplats** som täcker över `sitepage.hbs`-skriptet. Variabeln `siteUrl` anges när den återges på servern innan den används på klienten.

För en **allmän AEM** som innehåller webbgruppskomponenter, men som inte har skapats med guiden [Skapa webbplats](/help/communities/sites-console.md), måste elementet läggas till. Värdet för href bör vara sökvägen till platsen. Om till exempel platssökvägen är `/content/my/company/en` använder du:

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

Författarmiljöns [OSGi-konfiguration](/help/sites-deploying/configuring-osgi.md), `AEM Communities Analytics Component Configuration`, innehåller en lista över de komponenter som har instrumenterats för Analytics. Den automatiska mappningen av variabler bestäms av komponenterna i listan.

Om nya anpassade komponenter skapas som är instrumenterade för Analytics, bör de läggas till i den här listan med konfigurerade komponenter.

### Komponentkonfiguration {#component-configuration}

![component-configuration1](assets/component-configuration1.png)

>[!NOTE]
>
>Journalkomponenterna används för att implementera bloggfunktionen.

### Mappade analyser till AEM variabler {#mapped-analytics-to-aem-variables}

När communitywebbplatsen har sparats, Analytics är aktiverat och Cloud Config-ramverket valt, mappas AEM-variablerna automatiskt till eVars och händelser för Analytics. Det börjar med var1 respektive event1 och ökar med 1.

Om du använder en befintlig rapportserie som har mappat någon av variablerna inom var1 till var11 och event1 till och med event7, blir det nödvändigt att [mappa om AEM variabler](#modifying-analytics-variable-mapping) och återställa den ursprungliga mappningen.

Här följer ett exempel på standardmappningar:

![map-analytics](assets/map-analytics1.png)

#### Karta över eVars som skickas med varje händelse {#map-of-evars-sent-with-each-event}

<table>
 <tbody>
  <tr>
   <td><strong> </strong></td>
   <td><strong>Aktivera <br /> resurs<br />-typ</strong></td>
   <td><strong>Platsens <br />-titel</strong></td>
   <td><strong>Funktion <br />, typ</strong></td>
   <td><strong>Grupp<br /> - titel</strong></td>
   <td><strong>Grupp<br /> - sökväg</strong></td>
   <td><strong>UGC<br />-typ</strong></td>
   <td><strong>UGC<br />-titel</strong></td>
   <td><strong>Användare<br /> (medlem)</strong></td>
   <td><strong>UGC<br />-sökväg</strong></td>
   <td><strong>Sökväg till platsen <br /></strong></td>
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
   <td><em>(a)</em></td>
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
   <td><em>(a)</em></td>
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

**Exempel på eVar-värden:**

* *[MIME-typ](https://www.iana.org/assignments/media-types/media-types.xhtml)*: video/mp4
* *[communityplatsens titel](/help/communities/sites-console.md#step13asitetemplate)*: Geometrixx Communities
* *[communityfunktionsnamn](/help/communities/functions.md)*: Forum
* *[community-gruppnamn](/help/communities/creating-groups.md#creating-a-new-group)*: Söker
* *sökväg till communitygruppsinnehåll*: `/content/sites/<site name>/en/groups/hiking`
* *[UGC-komponentresurstyp](/help/communities/essentials.md)*: `social/forum/components/hbs/topic`
* *UGC-komponenttitel*: Hiking Topics (Dölja ämnen)
* *login (authorizedId)*: `aaron.mcdonald@mailinator.com`
* *SRP-sökväg till UGC*: `/content/usergenerated/asi/.../forum/jmtz-topic3`
eller *komponentens sökväg som ska följas*: `/content/sites/<site name>/en/jcr:content/content/primary/forum`

* *sökväg till innehåll för communitywebbplats*: `/content/sites/<site name>/en`

### Ändra variabelmappning för analys {#modifying-analytics-variable-mapping}

Mappningen av eVars och händelser för Analytics till AEM-variabler är synlig från ramverkskonfigurationen när Analytics har aktiverats för en communitywebbplats.

När Analytics är aktiverat och innan communitywebbplatsen publiceras kan mappningen ändras i ramverket. Dra bara Analytics-evar eller -händelse från den vänstra listen och släpp den på rätt rad i mappningstabellen.

För att undvika dubblettmappningar måste du se till att ta bort den ersatta Analytics-instansen eller händelsen från raden genom att hålla markören över den och välja &quot;X&quot; som visas till höger om variabelelementet Analytics.

Om Communities eVars och events skriver över mappningar som fanns tidigare i rapportsviten bör du, för att undvika dataförluster, tilldela AEM variabler för Communities-funktioner till andra Analytics eVars eller händelser och återställa de ursprungliga mappningarna.

>[!CAUTION]
>
>Det är viktigt att fortsätta innan communitywebbplatsen [publiceras](#publishing-the-community-site) med Analytics aktiverat, annars finns det risk för dataförlust.

#### Exempel steg 1: Dra Analytics evar14 till mappningstabellen {#example-step-dragging-analytics-evar-into-mapping-table}

![analytics-mapping-evar](assets/analytics-mapping-evar.png)

#### Exempelsteg 2: Markera &#39;x&#39; för att ta bort ersatt evar11 {#example-step-selecting-x-to-remove-replaced-evar}

![analytics-mapping-evar1](assets/analytics-mapping-evar1.png)

#### Exempelsteg 3: AEM var eventdata.siteId ommappades till Analytics evar14 {#example-step-aem-var-eventdata-siteid-remapped-to-analytics-evar}

![analytics-mapping-evar2](assets/analytics-mapping-evar2.png)

## Publicera communitywebbplatsen {#publishing-the-community-site}

### Verifiera analyser för att AEM variabelmappning {#verify-analytics-to-aem-variable-mapping}

Det är klokt att verifiera variabelmappningen innan communitywebbplatsen publiceras, som även publicerar Analytics Cloud tjänst och ramverk.

Se avsnitt:

* [Mappade analyser till AEM variabler](#mapped-analytics-to-aem-variables)
* [Ändra variabelmappning för analys](#modifying-analytics-variable-mapping)

>[!CAUTION]
>
>**Om du använder en befintlig rapportserie som redan använder variabler inom**
>
>* **`evar1`** till **`evar11`**
>
>* **`event1`** till **`event7`**
>
>**Återställer sedan den befintliga mappningen innan communitywebbplatsen publiceras.** Flytta AEM som automatiskt mappades (när Analytics var aktiverat för communitywebbplatsen) till andra Analytics-variabler. Denna ommappning bör vara konsekvent för alla komponenter i Communities.
>
>Om detta inte görs kan data gå förlorade.

### Primär utgivare {#primary-publisher}

När den valda distributionen är en [publiceringsgrupp](/help/communities/topologies.md#tarmk-publish-farm) måste en AEM publiceringsinstans identifieras som primär utgivare för att avfråga Adobe Analytics för rapportdata som ska skrivas till [SRP](/help/communities/working-with-srp.md).

Som standard identifierar OSGi-konfigurationen `AEM Communities Publisher Configuration` sin publiceringsinstans som primär utgivare, så att alla publiceringsinstanser i en publiceringsgrupp identifierar sig själva som primär.

Det är därför nödvändigt att redigera konfigurationen för alla sekundära publiceringsinstanser för att avmarkera kryssrutan **Primär utgivare**.

Specifika anvisningar finns i den primära utgivardelen av [Distribuera communities](/help/communities/deploy-communities.md#primary-publisher).

>[!CAUTION]
>
>Det är viktigt att den primära utgivaren är konfigurerad för att förhindra avsökning från flera publiceringsinstanser.

### Replikera krypteringsnyckeln {#replicate-the-crypto-key}

Adobe Analytics-autentiseringsuppgifterna är krypterade. För att underlätta replikering eller överföring av krypterade autentiseringsuppgifter för analys mellan författare och utgivare måste alla AEM instanser ha samma primära krypteringsnyckel.

Följ instruktionerna på [Replikera krypteringsnyckeln](/help/communities/deploy-communities.md#replicate-the-crypto-key) om du vill göra det.

### Publish Community Site och Analytics Cloud Service {#publish-community-site-and-analytics-cloud-service}

När Analytics Cloud-tjänsten har aktiverats för en community-webbplats och, om det behövs, [mappningen av Analytics till AEM-variabler har justerats](#mapped-analytics-to-aem-variables), replikerar du konfigurationen till publiceringsmiljön genom att [(publicera om)communitywebbplatsen](/help/communities/sites-console.md#publishing-the-site).

## Få rapporter från Analytics {#obtaining-reports-from-analytics}

### Rapporthantering {#report-management}

Författaren och den primära utgivarens [OSGi-konfiguration](/help/sites-deploying/configuring-osgi.md), `AEM Communities Analytics Report Management`, används för att fråga Analytics.

Frågorna gäller för realtidsrapporter.

På den primära utgivaren används frågorna för att tillhandahålla information som förberedelse för Report-importerarens Analytics-dataimport.

Frågeintervallet är som standard 10 sekunder.

### Rapportimporteraren {#report-importer}

När en communitywebbplats aktiverad med Analytics har publicerats kan den primära utgivarens [OSGi-konfiguration](/help/sites-deploying/configuring-osgi.md), `AEM Communities Analytics Report Importer`, konfigureras för att ange standardavsökningsintervallet för de konfigurationer som inte konfigureras individuellt i CRXDE.

Avsökningsintervallet styr frekvensen av förfrågningar till Adobe Analytics om data som ska hämtas och sparas i [SRP](/help/communities/working-with-srp.md).

När data kan kategoriseras som&quot;big data&quot; kan en mer frekvent undersökning innebära en stor belastning på communitywebbplatsen.

Standardavsökningsintervallet **för import** är 12 timmar.

![report-importer](assets/report-importer.png)

### Anpassning av komponentrapport {#component-report-customization}

För att anpassa mätvärdena för att spåra skapas för närvarande noder i databasen som definierar tidsperioder för vilka en rapport om mätvärdena ska genereras.

Forum-ämnet är för närvarande det enda exemplet på den här anpassningen:

* Logga in med administratörsbehörighet på den primära utgivaren.
* Gå till [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md). Exempel: [https://localhost:4503/crx/de](https://localhost:4503/crx/de).

* Under noden `jcr:content` i språkroten (till exempel `/content/sites/engage/en/jcr:content`) navigerar du till komponenten som konfigurerats för Analytics-rapportering.
Exempel: **`analytics/reportConfigs/social_forum_components_hbs_topic`**

* Observera de skapade tidsperioderna:

   * `last30Days`
   * `last90Days`
   * `thisYear`

* Observera noden `total`.

   * Om du ändrar egenskapen **`interval`** åsidosätts intervallet för rapportimporteraren.
   * Värdet anges i sekunder och är fyra timmar (1 400 sekunder).

![komponent-rapport](assets/component-report.png)

## Hantera användardata i Analytics {#manage-user-data-in-analytics}

Adobe Analytics tillhandahåller API:er som gör att du kan komma åt, exportera och ta bort användardata. Mer information finns i [Skicka in begäran om åtkomst och borttagning](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/data-governance/an-gdpr-workflow.html?lang=sv-SE).

## Resurser {#resources}

* Adobe Experience Cloud: [Hjälp och referens för analyser](https://experienceleague.adobe.com/docs/analytics.html?lang=sv-SE)
* AEM: [Integrera med Adobe Analytics](/help/sites-administering/adobeanalytics.md)
* AEM: [Analyser med externa leverantörer](/help/sites-administering/external-providers.md)
