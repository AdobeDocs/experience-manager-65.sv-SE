---
title: Migrering till Touch UI
seo-title: Migrering till Touch UI
description: Migrering till Touch UI
seo-description: Migrering till Touch UI
uuid: 47c43b56-532b-4ada-8503-04d66bab3564
contentOwner: aheimoz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: introduction
discoiquuid: b315720f-e9b8-4063-99e2-1b9aa6bba460
docset: aem65
translation-type: tm+mt
source-git-commit: 5597fb39500ac1f85d03263bfa1e5239d35d2a2c

---


# Migrering till Touch UI{#migration-to-the-touch-ui}

Från och med version 6.0 har Adobe Experience Manager (AEM) introducerat ett nytt användargränssnitt som kallas *pekaktiverat användargränssnitt* (kallas även *pekgränssnittet*). Det är anpassat till Adobe Marketing Cloud och till de allmänna riktlinjerna för Adobes användargränssnitt. Det här har blivit standardgränssnittet i AEM med det äldre, skrivbordsorienterade gränssnittet, som kallas det *klassiska gränssnittet*.

Om du har använt AEM med klassiskt gränssnitt måste du vidta åtgärder för att migrera instansen. Den här sidan är avsedd att fungera som en språngbräda genom länkar till enskilda resurser.

>[!NOTE]
>
>Ett sådant migreringsprojekt kan få stor effekt på din instans. Se [Hantera projekt - Bästa metoder](/help/managing/best-practices.md) för rekommenderade riktlinjer.

## Grunderna {#the-basics}

När du migrerar bör du vara medveten om följande (stora) skillnader mellan det klassiska gränssnittet och det pekande gränssnittet:

<table>
 <tbody>
  <tr>
   <td>Klassiskt användargränssnitt</td>
   <td>Pekaktiverat användargränssnitt</td>
  </tr>
  <tr>
   <td>Beskrivs i JCR-databasen som en nodstruktur. Alla noder som representerar ett element i användargränssnittet kallas för en <em>ExtJS-widget</em> och återges på klientsidan av <code>ExtJS</code>.</td>
   <td>Beskrivs också i JCR-databasen som en nodstruktur. I det här fallet refererar alla noder till en Sling-resurstyp (Sling-komponent), som ansvarar för återgivningen. Gränssnittet renderas alltså (i stort) på serversidan.</td>
  </tr>
  <tr>
   <td><p><code>sling:resourceType</code></p>
    <ul>
     <li>används inte</li>
    </ul> </td>
   <td><code>sling:resourceType</code>
    <ul>
     <li>används</li>
     <li>for example<br /> <code>cq/gui/components/authoring/dialog</code><br /> </li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>Dialognoder:</p>
    <ul>
     <li>Namn: <code>dialog</code></li>
     <li>jcr:primärTyp: <code>cq:Dialog</code></li>
    </ul> </td>
   <td><p>Dialognoder:</p>
    <ul>
     <li>Namn: <code>cq:dialog</code></li>
     <li>jcr:primärTyp: <code>nt:unstructured</code></li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>Javascript-plats:</p>
    <ul>
     <li>Imperativa delar bäddas in direkt med avlyssnare eller hanteras i klientlibs.</li>
    </ul> </td>
   <td><p>Javascript-plats:</p>
    <ul>
     <li>Imperativa delar kan inte bäddas in i dialogdefinitionen. olika ansvarsområden.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>Händelsehantering:</p>
    <ul>
     <li>Dialogrutewidgetar refererar direkt till Javascript-kod.</li>
    </ul> </td>
   <td><p>Händelsehantering:</p>
    <ul>
     <li>Javascript observerar dialoghändelser.</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Återgivning utförd av klienten:
    <ul>
     <li>Klienten skapar gränssnittskomponenterna dynamiskt.</li>
     <li>Klientförfrågningar (Pull) komponentdefinition (som JSON) från servern.</li>
    </ul> </td>
   <td>Återgivning utförd av servern:
    <ul>
     <li>Klienten begär sidor tillsammans med det relaterade användargränssnittet.</li>
     <li>Servern skickar (push) gränssnittet som HTML-dokument. med Coral UI-komponenter.<br /> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

Att migrera ett avsnitt i användargränssnittet från det klassiska gränssnittet till pekgränssnittet innebär med andra ord att en *ExtJS-widget* porteras till en *Sling-komponent*. För att underlätta detta baseras pekgränssnittet på GRE-ramverket (Granite UI Framework), som redan innehåller vissa Sling-komponenter för användargränssnittet (kallas GRE UI-komponenter).

Kontrollera status och relaterade rekommendationer innan du börjar:

* [Status för Touch UI-funktioner](/help/release-notes/touch-ui-features-status.md)
* [Rekommendationer för användargränssnitt för kunder](/help/sites-deploying/ui-recommendations.md)

Grundläggande information om hur du utvecklar användargränssnittet för pekskärmar ger en solid grund:

* [AEM Touch-aktiverat användargränssnitt](/help/sites-developing/touch-ui-concepts.md)
* [Struktur för det AEM Touch-aktiverade gränssnittet](/help/sites-developing/touch-ui-structure.md)

## Migrerar sidredigering {#migrating-page-authoring}

Dialogrutor är en viktig faktor när du migrerar komponenter:

* [Utveckla AEM-komponenter](/help/sites-developing/developing-components.md) (med det pekaktiverade användargränssnittet)
* [Migrera från en klassisk komponent](/help/sites-developing/developing-components.md#migrating-from-a-classic-component)
* [Verktyget](/help/sites-developing/dialog-conversion.md) Dialogkonvertering - hjälper dig att konvertera dialogrutorna för dina klassiska användargränssnittskomponenter till användargränssnitt

   * Det finns ett kompatibilitetslager med pekfunktion för att öppna en klassisk användargränssnittsdialogruta i en&quot;Touch UI wrapper&quot;, men det har begränsad funktionalitet och rekommenderas inte på lång sikt.

* [Anpassa dialogrutefält i Touch UI](https://helpx.adobe.com/experience-manager/kt/eseminars/gems/aem-customizing-dialog-fields-in-touch-ui.html)
* [Skapa en ny GRE-fältkomponent](/help/sites-developing/granite-ui-component.md)
* [Anpassa sidredigering](/help/sites-developing/customizing-page-authoring-touch.md) (med det beröringsaktiverade användargränssnittet)

## Migrera konsoler {#migrating-consoles}

Du kan också anpassa konsolerna:

* [Anpassa konsolerna](/help/sites-developing/customizing-consoles-touch.md) (för det beröringsaktiverade användargränssnittet)

## Relaterade överväganden {#related-considerations}

Även om det inte är direkt relaterat till en migrering till pekgränssnittet finns det relaterade problem som är värda att ta hänsyn till samtidigt, eftersom de också rekommenderas:

* [Mallar](/help/sites-developing/templates.md) - [Redigerbara mallar](/help/sites-developing/page-templates-editable.md)
* [Kärnkomponenter](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/introduction.html)
* [HTL](https://docs.adobe.com/content/help/en/experience-manager-htl/using/overview.html)

>[!NOTE]
>
>Se även [Utveckla - Bästa metoder](/help/sites-developing/best-practices.md).

## Ytterligare resurser {#further-resources}

Mer information om hur du utvecklar AEM finns i samlingen av resurser under:

* [Utveckla användarhandbok](/help/sites-developing/home.md)
* [Bevilja gränssnittsdokumentation](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/index.html)
* [Självstudiekurser och videoklipp för AEM 6.5-webbplatser](https://docs.adobe.com/content/help/en/experience-manager-learn/sites/overview.html)
* [Komma igång med utveckling av AEM-webbplatser - WKND-självstudiekurs](/help/sites-developing/getting-started.md)
* [AEM Gems](https://helpx.adobe.com/experience-manager/kt/eseminars/gems/aem-index.html)
* [AEM Modernization Tools](https://opensource.adobe.com/aem-modernize-tools/)

>[!CAUTION]
>
>AEM Modernization Tools är en community-åtgärd som inte stöds eller garanteras av Adobe.

