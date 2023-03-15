---
title: Redigera sidegenskaper
seo-title: Editing Page Properties
description: En sidas egenskaper kan variera beroende på sidans beskaffenhet. Vissa sidor kan till exempel vara kopplade till en live-kopia medan andra inte är det och live-kopieringsinformationen är tillgänglig efter behov.
seo-description: Properties of a page can vary depending on the nature of the page. For example some pages might be connected to a live copy while others are not and the live copy information will be available as appropriate.
uuid: 63d37d1b-52da-489d-b02b-e8b3d17571d1
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: 23768c73-ac64-4727-8313-160c8c131b05
exl-id: 1a77e4cd-bbf8-4d05-bb35-fd43c02eaf30
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '763'
ht-degree: 1%

---

# Redigera sidegenskaper{#editing-page-properties}

Du kan definiera de egenskaper som krävs för en sida. Dessa kan variera beroende på sidans beskaffenhet. Vissa sidor kan till exempel vara kopplade till en live-kopia medan andra inte är det och live-kopieringsinformationen är tillgänglig efter behov.

## Sidegenskaper {#page-properties}

Egenskaperna fördelas på flera flikar:

### Grundläggande {#basic}

* **Titel**

   Sidans rubrik visas på olika platser. Till exempel **Webbplatser** tabblista och **Webbplatser** kort-/listvyer.

   Detta är ett obligatoriskt fält.

* **Taggar**

   Här kan du lägga till eller ta bort taggar från sidan genom att uppdatera listan i valrutan:

   * När du har valt en tagg visas den under markeringsrutan. Du kan ta bort en tagg från den här listan med hjälp av x.
   * Du kan ange en helt ny tagg genom att skriva namnet i en tom markeringsruta.

      Den nya taggen skapas när du trycker på Enter. Den nya taggen visas sedan i en ruta med en liten stjärna till höger som anger att det är en ny tagg.

   * Med den nedrullningsbara menyn kan du välja bland befintliga taggar.
   * Ett x-tecken visas när du håller muspekaren över en taggpost i markeringsrutan; den här taggen kan användas för att ta bort taggen för den här sidan.

* **Dölj i navigering**

   En växlingsknapp som anger om sidan visas eller döljs i sidnavigeringen.

* **Sidrubrik**

   En rubrik som ska användas på sidan.

* **Navigeringsrubrik**

   Du kan ange en separat rubrik som ska användas i navigeringen (om du till exempel vill ha något mer koncist). Om den är tom visas **Titel** kommer att användas.

* **Underrubrik**

   En underrubrik som ska användas på sidan.

* **Beskrivning**

   Din beskrivning av sidan, dess syfte eller annan information som du vill lägga till.

* **I tid**

   Det datum och den tidpunkt då den publicerade sidan ska aktiveras. När den publiceras kommer den här sidan att vara vilande tills den angivna tiden.

   Lämna dessa fält tomma för sidor som du vill publicera omedelbart (det normala scenariot).

* **Fråntid**

   Den tidpunkt då den publicerade sidan inaktiveras.

   Lämna dessa fält tomma igen för sidor som du vill publicera omedelbart.

* **Vanity URL**

   Gör att du kan ange en fågel-URL för den här sidan. Det gör att du kan ha en kortare och mer uttrycksfull URL.

   Om Vanity-URL:en till exempel är inställd på w `elcome`till den sida som identifieras av sökvägen / `v1.0/startpage`för webbplatsen h `ttp://example.com,` sedan h `ttp://example.com/welcome`skulle vara den vanligaste URL:en för h `ttp://example.com/content/v1.0/startpage`

   >[!CAUTION]
   >
   >Alternativa URL:er:
   >
   >* måste vara unik så du bör vara försiktig med att värdet inte redan används av en annan sida.
   >* stöder inte regex-mönster.


* **URL för omdirigering**

   Anger om du vill att sidan ska använda fågel-URL:en.

### Avancerat {#advanced}

* **Språk:**

   Sidspråket.

* **Omdirigering**

   Ange den sida som den här sidan automatiskt ska omdirigeras till.

* **Design**

   Ange [design](/help/sites-developing/designer.md) som ska användas för den här sidan.

* **Alias**

   Ange ett alias som ska användas med den här sidan.

* **Aktivera stängd användargrupp**

   Aktiverar (eller inaktiverar) användning av [stängda användargrupper](/help/sites-administering/cug.md) (CUG).

* **Inloggningssida**

   Den sida som ska användas för inloggning.

* **Tillåtna grupper**

   Grupper som är berättigade att logga in i CUG.

* **Sfär**

   CUG:ens verkliga namn.

* **Exportera konfiguration**

   Ange en exportkonfiguration.

### Miniatyrbild {#thumbnail}

* **Sidminiatyr**

   Visar sidminiatyrbilden. Du kan:

   * **Generera förhandsgranskning**

      Generera en förhandsgranskning av sidan som ska användas som miniatyrbild.

   * **Överför bild**

      Överför en bild som ska användas som miniatyrbild.

### Cloud Services {#cloud-services}

* **Cloud Services**

   Definiera egenskaper för [molntjänster](/help/sites-developing/extending-cloud-config.md).

### Personanpassning {#personalization}

* **Personanpassning**

   Välj en [Varumärke som anger ett omfång för målanpassning](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md).

### Behörigheter {#permissions}

* **Behörigheter** (pekoptimerat användargränssnitt)

   Visa [effektiva behörigheter och lägga till nya behörigheter](/help/sites-administering/user-group-ac-admin.md).

### Blueprint {#blueprint}

* **Blueprint**

   Definiera egenskaper för en designsida i [hantering av flera webbplatser](/help/sites-administering/msm.md). Styr under vilka omständigheter ändringar ska spridas till Live Copy.

### Live Copy {#live-copy}

* **Livecopy**

   Definiera egenskaper för en Live Copy-sida i [hantering av flera webbplatser](/help/sites-administering/msm.md). Styr under vilka omständigheter ändringar ska spridas från utkast.

### Webbplatsstruktur {#site-structure}

* Tillhandahålla länkar till sidor som innehåller funktioner för hela webbplatsen, som **Registreringssida**, **Offlinesida**, bland annat.

## Redigera sidegenskaper {#editing-page-properties-2}

### Redigera sidegenskaper för en viss sida {#editing-page-properties-for-a-specific-page}

Sidegenskaper definierar de olika egenskaperna för sidan, till exempel rubriker, när de visas på webbplatsen och andra.

1. Öppna sidan som du vill redigera.

1. Öppna **Sida** välj **Sidegenskaper...**

   Då öppnas en dialogruta med flera flikar.

1. Gör de ändringar du vill och klicka sedan på **OK** att spara.
