---
title: Struktur för det AEM användargränssnittet med pekskärm
seo-title: Structure of the AEM Touch-Enabled UI
description: Det pekoptimerade användargränssnittet, som implementeras i AEM, har flera underliggande principer och består av flera nyckelelement
seo-description: The touch-optimized UI, as implemented in AEM, has several underlying principles and is made up of several key elements
uuid: 9a255238-1adc-4a40-9c37-30cb53ffb26c
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: 55dba890-4847-4986-b272-33480bc1d573
exl-id: e562b289-5d8b-4fa8-ad1c-fff5f807a45e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '861'
ht-degree: 1%

---

# Struktur för det AEM användargränssnittet med pekskärm{#structure-of-the-aem-touch-enabled-ui}

Det AEM användargränssnittet med pekskärm har flera underliggande principer och består av flera nyckelelement:

## Konsoler {#consoles}

### Grundläggande layout och storleksändring {#basic-layout-and-resizing}

Gränssnittet fungerar både för mobila och stationära enheter, men i stället för att skapa två format har Adobe valt att använda ett format som fungerar för alla skärmar och enheter.

Alla moduler använder samma grundläggande layout, AEM detta kan ses som:

![chlimage_1-142](assets/chlimage_1-142.png)

Layouten följer en responsiv designstil och anpassas till storleken på enheten/fönstret som du använder.

Om upplösningen till exempel ligger under 1 024 px (som på en mobil enhet) justeras skärmen därefter:

![chlimage_1-143](assets/chlimage_1-143.png)

### Sidhuvudsfält {#header-bar}

![chlimage_1-144](assets/chlimage_1-144.png)

Rubrikraden visar globala element som:

* logotypen och den specifika produkt/lösning som du för närvarande använder, för AEM utgör detta också en länk till den globala navigeringen
* Sökning
* ikon för att komma åt hjälpresurserna
* ikon för att komma åt andra lösningar
* en indikator för (och åtkomst till) alla aviseringar eller inkorgsobjekt som väntar på dig
* användarikonen tillsammans med en länk till din profilhantering

### Verktygsfält {#toolbar}

Det här är kontextuellt för platsen och ytverktygen som är relevanta för att styra vyn eller resurserna på sidan nedan. Verktygsfältet är produktspecifikt, men det finns vissa gemensamma element.

Alla tillgängliga åtgärder visas i verktygsfältet:

![chlimage_1-145](assets/chlimage_1-145.png)

Beroende på om en resurs är markerad:

![chlimage_1-146](assets/chlimage_1-146.png)

### Vänster linje {#left-rail}

Den vänstra listen kan öppnas/döljas efter behov för att visa:

* **Tidslinje**
* **Referenser**
* **Filter**

Standardvärdet är **Endast innehåll** (dold räl).

![chlimage_1-147](assets/chlimage_1-147.png)

## Sidredigering {#page-authoring}

När du skapar sidor är de strukturella områdena följande.

### Innehållsram {#content-frame}

Sidinnehållet återges i innehållsramen. Innehållsramen är helt oberoende av redigeraren för att säkerställa att det inte finns några konflikter på grund av CSS eller javascript.

Innehållsramen finns till höger i fönstret, under verktygsfältet.

![chlimage_1-148](assets/chlimage_1-148.png)

### Redigeringsram {#editor-frame}

Redigeringsramen har redigeringsfunktionerna.

Redigeringsramen är en behållare (abstrakt) för alla *redigeringselement för sidor*. Den ligger ovanpå innehållsramen och innehåller:

* det övre verktygsfältet
* sidopanelen
* alla övertäckningar
* alla andra sidredigeringselement, komponentens verktygsfält

![chlimage_1-149](assets/chlimage_1-149.png)

### Side Panel {#side-panel}

Detta innehåller två standardflikar där du kan välja resurser och komponenter; de kan dras härifrån och släppas på sidan.

Sidpanelen är dold som standard. När det här alternativet är markerat visas det antingen på vänster sida, eller glida över för att täcka hela fönstret (när fönsterstorleken är under bredden 1024px; som på en mobil enhet).

![chlimage_1-150](assets/chlimage_1-150.png)

### Side Panel - Assets {#side-panel-assets}

På fliken Resurser kan du välja bland flera resurser. Du kan också filtrera efter en viss term eller välja en grupp.

![chlimage_1-151](assets/chlimage_1-151.png)

### Sida - Resursgrupper {#side-panel-asset-groups}

På fliken Resurser finns det en listruta där du kan välja specifika resursgrupper.

![chlimage_1-152](assets/chlimage_1-152.png)

### Side Panel - Components {#side-panel-components}

På fliken Komponenter kan du välja bland komponenterna. Du kan också filtrera efter en viss term eller välja en grupp.

![chlimage_1-153](assets/chlimage_1-153.png)

### Övertäckningar {#overlays}

Dessa överlägg innehållsramen och används av [lager](#layer) för att utnyttja mekanismerna i hur du kan interagera (helt transparent) med komponenterna och deras innehåll.

Övertäckningarna finns i redigerarramen (med alla andra sidredigeringselement), även om de faktiskt täcker över rätt komponenter i innehållsramen.

![chlimage_1-154](assets/chlimage_1-154.png)

### Lager {#layer}

Ett lager är ett oberoende funktionspaket som kan aktiveras för att:

* ger en annan vy av sidan
* kan du ändra och/eller interagera med en sida

Lagren har avancerade funktioner för hela sidan, i motsats till specifika åtgärder för en enskild komponent.

AEM innehåller flera lager som redan har implementerats för sidredigering, som till exempel redigering, förhandsgranskning och anteckning.

>[!NOTE]
>
>Lager är ett kraftfullt koncept som påverkar hur användaren ser på och interagerar med sidinnehållet. När du utvecklar egna lager måste du se till att lagret rensas när det avslutas.

### Lagerväxlare {#layer-switcher}

Med lagerväljaren kan du välja det lager som du vill använda. När det är stängt visas det lager som används.

Lagerväljaren är tillgänglig som en listruta från verktygsfältet (längst upp i fönstret, i redigeringsramen).

![chlimage_1-155](assets/chlimage_1-155.png)

### Komponentverktygsfältet {#component-toolbar}

Varje instans av en komponent visar verktygsfältet när användaren klickar på det (antingen en gång eller med ett långsamt dubbelklick). Verktygsfältet innehåller de specifika åtgärder (t.ex. kopiera, klistra in, öppna redigeringsprogram) som är tillgängliga för komponentinstansen (redigerbar) på sidan.

Beroende på vilket utrymme som är tillgängligt placeras komponentens verktygsfält i det övre, eller nedre, högra hörnet av respektive komponent.

![chlimage_1-156](assets/chlimage_1-156.png)

## Ytterligare information {#further-information}

Mer information om begreppen kring det beröringsaktiverade användargränssnittet finns i artikeln [Koncepten i det AEM användargränssnittet med pekskärm](/help/sites-developing/touch-ui-concepts.md).

Mer teknisk information finns i [JS-dokumentationsuppsättning](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/jsdoc/ui-touch/editor-core/index.html) för den pekaktiverade sidredigeraren.
