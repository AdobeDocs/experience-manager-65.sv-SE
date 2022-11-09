---
title: Komponenter - översikt
seo-title: Components
description: Komponenter är modulära enheter som har vissa funktioner för att presentera ditt innehåll på din webbplats
seo-description: Components are modular units which realize specific functionality to present your content on your website
uuid: fb39aeb8-8f43-4091-8083-ebfab89e6e63
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
discoiquuid: 45efff93-2fe5-4313-83a0-0e23a540da93
exl-id: 9e30c969-2692-4380-943a-b022ee900ce8
source-git-commit: b886844dc80482ae4aae5fc7ce09e466efecc3bd
workflow-type: tm+mt
source-wordcount: '581'
ht-degree: 0%

---

# Komponenter - översikt{#components-overview}

På den här sidan finns en översikt över Adobe Experience Manager (AEM) komponenter som [används för att skapa sidor](/help/sites-authoring/default-components-foundation.md).

## Vad är komponenter? {#what-exactly-is-a-component}

* Modulära enheter som utnyttjar specifika funktioner för att presentera innehållet på webbplatsen.
* Kan återanvändas.
* Utvecklas som självständiga enheter i en mapp i databasen.
* Har inga dolda konfigurationsfiler.
* Kan innehålla andra komponenter.
* Kan köras var som helst i vilket AEM som helst. De kan också begränsas till att köras under specifika komponenter.
* ha ett standardiserat användargränssnitt.
* Har redigeringsbeteende som kan konfigureras.
* Använda dialogrutor som är byggda med delelement som är baserade på GRÄNSSNITTSkomponenter i Granite
* utvecklas med [HTL](https://experienceleague.adobe.com/docs/experience-manager-htl/content/overview.html) (rekommenderas) eller JSP.
* Kan utvecklas för att skapa anpassade komponenter som utökar standardfunktionerna.

Eftersom komponenterna är modulära kan du:

* Utveckla en ny komponent på den lokala instansen.
* Driftsätt den i testmiljön.
* Distribuera det till redigeringsmiljön där författare och/eller administratörer kan lägga till och konfigurera innehåll.
* Distribuera den i publiceringsmiljön där de används för att återge innehåll för besökare på webbplatsen. Vissa komponenter, till exempel för Communities, accepterar även indata från dina användare.

Varje AEM:

* Är en resurstyp.
* Är en samling skript som helt och hållet realiserar en viss funktion.
* Kan fungera i *isolering*, det vill säga antingen i AEM eller i en portal.

## Färdiga komponenter i AEM {#out-of-the-box-components-within-aem}

AEM har en mängd olika [färdiga komponenter](/help/sites-authoring/default-components.md) som ger omfattande funktionalitet, bland annat:

* Styckesystem ( `parsys`)
* Sida ( `responsivegrid` - endast användargränssnitt med pekfunktion)
* Text
* Bild, med medföljande text
* Verktygsfält

Komponenterna som tillhandahålls och deras användning i [exempel på webbsidor för webbbutiker](/help/sites-developing/we-retail.md) illustrera hur du implementerar och använder komponenter. Komponenterna levereras med all källkod och kan användas som de är eller som startpunkter för ändrade eller utökade komponenter.

### Kärnkomponenter och grundkomponenter {#core-components-and-foundation-components}

Det finns två uppsättningar AEM komponenterna som tillhandahålls av Adobe:

* [Kärnkomponenter](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html)
* [Foundation Components](/help/sites-authoring/default-components-foundation.md)

**Kärnkomponenter** introducerades med AEM 6.3 och erbjuder flexibla och funktionsrika redigeringsfunktioner. The [Referensplats för Vi.butik](/help/sites-developing/we-retail.md) visar hur kärnkomponenterna kan användas och visar de bästa metoderna för komponentutveckling.

**Foundation Components** har varit tillgängliga med AEM i många versioner och finns i en AEM standardinstallation. Även om de flesta fortfarande stöds har de tagits bort, förbättrats inte längre och baseras på äldre tekniker.

>[!NOTE]
>
>[Kärnkomponenter](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html) är de bästa metoderna för komponentdesign och -utveckling och fungerar som referensimplementationer.
>
>[AEM](modernization-tools.md) kan hjälpa dig att migrera till kärnkomponenter.

### Visa tillgängliga komponenter {#viewing-available-components}

Använd kommandot [Komponentkonsol](/help/sites-authoring/default-components-console.md).

Du kan också använda CRXDE Lite för att få en lista över alla komponenter som är tillgängliga i databasen.

1. I **[!UICONTROL CRXDE Lite]**, markera **[!UICONTROL Tools]** från verktygsfältet och sedan **[!UICONTROL Query]** som öppnar **[!UICONTROL Query]** -fliken.

1. I **[!UICONTROL Query]** flik, välja `XPath` as **[!UICONTROL Type]**.

1. I **[!UICONTROL Query]** indatafält, ange följande sträng:

   `//element(*, cq:Component)`

1. Klicka **[!UICONTROL Execute]** och komponenterna visas.

## Ytterligare resurser {#further-reading}

På följande sidor finns mer detaljerad information om hur du utvecklar dessa - och andra - komponenter:

* [AEM - Grunderna](/help/sites-developing/components-basics.md)
* [Utveckla AEM](/help/sites-developing/developing-components.md)
* [Utveckla AEM - kodexempel](/help/sites-developing/developing-components-samples.md)
* [Konfigurera flera redigerare på plats](/help/sites-developing/multiple-inplace-editors.md)
* [Utvecklarläge](/help/sites-developing/developer-mode.md)
* [Testa användargränssnittet](/help/sites-developing/hobbes.md)
* [Komponenter för innehållsfragment](/help/sites-developing/components-content-fragments.md)
* [Hämta sidinformation i JSON-format](/help/sites-developing/pageinfo.md)
* [Internationalisering av komponenter](/help/sites-developing/i18n.md)
* [Kärnkomponenter](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html)
* [Använda Dölj villkor](/help/sites-developing/hide-conditions.md)
* Klassiskt användargränssnitt

   * [AEM (Classic UI)](/help/sites-developing/developing-components-classic.md)
   * [Använda och utöka widgetar (Classic UI)](/help/sites-developing/widgets.md)
   * [Använda xtypes (Classic UI)](/help/sites-developing/xtypes.md)
   * [Utveckla Forms (Classic UI)](/help/sites-developing/developing-forms.md)
