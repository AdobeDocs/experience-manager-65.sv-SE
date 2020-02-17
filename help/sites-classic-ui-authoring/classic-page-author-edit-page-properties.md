---
title: Redigera sidegenskaper
seo-title: Redigera sidegenskaper
description: En sidas egenskaper kan variera beroende på sidans beskaffenhet. Vissa sidor kan till exempel vara kopplade till en live-kopia medan andra inte är det och live-kopieringsinformationen är tillgänglig efter behov.
seo-description: En sidas egenskaper kan variera beroende på sidans beskaffenhet. Vissa sidor kan till exempel vara kopplade till en live-kopia medan andra inte är det och live-kopieringsinformationen är tillgänglig efter behov.
uuid: 63d37d1b-52da-489d-b02b-e8b3d17571d1
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: 23768c73-ac64-4727-8313-160c8c131b05
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Redigera sidegenskaper{#editing-page-properties}

Du kan definiera de egenskaper som krävs för en sida. Dessa kan variera beroende på sidans beskaffenhet. Vissa sidor kan till exempel vara kopplade till en live-kopia medan andra inte är det och live-kopieringsinformationen är tillgänglig efter behov.

## Sidegenskaper {#page-properties}

Egenskaperna fördelas på flera flikar:

### Grundläggande {#basic}

* **Titel**

   Sidans rubrik visas på olika platser. Till exempel fliklistan **Webbplatser** och vyerna **Webbplatser** .

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

   Du kan ange en separat rubrik som ska användas i navigeringen (om du till exempel vill ha något mer koncist). Om den är tom används **rubriken** .

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

   Om Vanity-URL:en till exempel är inställd på w `elcome`till sidan som identifieras av sökvägen / `v1.0/startpage`för webbplatsen h `ttp://example.com,` så `ttp://example.com/welcome`blir han standardwebbadressen för h `ttp://example.com/content/v1.0/startpage`

   >[!CAUTION]
   >
   >Vanity URL:er:
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

   Ange vilken [design](/help/sites-developing/designer.md) som ska användas för den här sidan.

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

### Molntjänster {#cloud-services}

* **Molntjänster**

   Definiera egenskaper för [molntjänster](/help/sites-developing/extending-cloud-config.md).

### Personalisering {#personalization}

* **Personalisering**

   Välj ett [varumärke om du vill ange ett omfång för målgruppsanpassning](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md).

### Permissions {#permissions}

* **Behörigheter** (pekoptimerat användargränssnitt)

   Visa de [gällande behörigheterna och lägg till nya behörigheter](/help/sites-administering/user-group-ac-admin.md).

### Blueprint {#blueprint}

* **Blueprint**

   Definiera egenskaper för en designsida inom hantering [av](/help/sites-administering/msm.md)flera webbplatser. Styr under vilka omständigheter ändringar ska spridas till Live Copy.

### Live Copy {#live-copy}

* **Livecopy**

   Definiera egenskaper för en Live Copy-sida inom hantering [av](/help/sites-administering/msm.md)flera webbplatser. Styr under vilka omständigheter ändringar ska spridas från utkast.

### Webbplatsstruktur {#site-structure}

* Tillhandahåll länkar till sidor som innehåller funktioner för hela webbplatsen, till exempel **Registreringssida** och **Offlinesida**.

## Redigera sidegenskaper {#editing-page-properties-2}

### Redigera sidegenskaper för en viss sida {#editing-page-properties-for-a-specific-page}

Sidegenskaper definierar de olika egenskaperna för sidan, till exempel rubriker, när de visas på webbplatsen och andra.

1. Öppna sidan som du vill redigera.

1. Öppna fliken **Sida** och välj sedan **Sidegenskaper...**

   Då öppnas en dialogruta med flera flikar.

1. Gör de ändringar du vill och klicka sedan på **OK** för att spara.

