---
title: Anpassa vyer av Sidegenskaper
seo-title: Anpassa vyer av Sidegenskaper
description: Varje sida har en uppsättning egenskaper som du kan redigera efter behov
seo-description: Varje sida har en uppsättning egenskaper som du kan redigera efter behov
uuid: cbfca6e6-cb9e-43b1-8889-09a7cc9f8a51
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: 6f8e08d1-831e-441a-ad1a-f5c8788f32d7
translation-type: tm+mt
source-git-commit: c38c27d6f7172734f80735dd2f42cfa7bf58ad1d

---


# Anpassa vyer av Sidegenskaper{#customizing-views-of-page-properties}

Varje sida har en uppsättning [egenskaper](/help/sites-authoring/editing-page-properties.md) som kan visas och redigeras av användare. vissa krävs när du skapar sidan (skapar vy), andra kan visas och redigeras (redigeringsvy) i ett senare skede. Dessa sidegenskaper definieras och görs tillgängliga genom dialogrutan ( `cq:dialog`) för den aktuella sidkomponenten.

>[!CAUTION]
>
>Det klassiska användargränssnittet gör det inte möjligt att anpassa vyn för sidegenskaper.

Standardläget för varje sidegenskap är:

* dolda i vyn Skapa (t.ex. guiden **Skapa sida** )

* som finns i redigeringsvyn (t.ex. **Visa egenskaper**)

Fälten måste vara specifikt konfigurerade om någon ändring krävs. Detta görs med lämpliga nodegenskaper:

* Page property to be available in the create view (t.ex. **Create Page** wizard):

   * Namn: `cq:showOnCreate`
   * Typ: `Boolean`

* Sidegenskap som ska vara tillgänglig i redigeringsvyn (t.ex. **Visa**/**redigera**) **Egenskaper** ):

   * Namn: `cq:hideOnEdit`
   * Typ: `Boolean`

Se t.ex. inställningarna för fält som är grupperade under **Fler rubriker och beskrivning** på fliken **Grundläggande** för bassidkomponenten. De här alternativen visas i guiden **Skapa sida** som `cq:showOnCreate` har ställts in på `true`:

```xml
/libs/foundation/components/page/cq:dialog/content/items/tabs/items/basic/items/column/items/moretitles
```

>[!TIP]
>
>I självstudiekursen [](https://docs.adobe.com/content/help/en/experience-manager-learn/sites/developing/page-properties-technical-video-develop.html) Utöka sidegenskaper finns en guide om hur du anpassar sidegenskaper.

## Konfigurera dina sidegenskaper {#configuring-your-page-properties}

Du kan också konfigurera fälten som är tillgängliga genom att konfigurera dialogrutan för sidkomponenten och använda lämpliga nodegenskaper.

Som standard visar guiden [****Skapa sida](/help/sites-authoring/managing-pages.md#creating-a-new-page)de fält som är grupperade under** Fler rubriker och beskrivning **. Så här döljer du dessa konfigurationer:

1. Skapa sidkomponenten under `/apps`.
1. Skapa en åsidosättning (med *dialogrutan* som tillhandahålls av [Sling Resource Merger](/help/sites-developing/sling-resource-merger.md)) för `basic` delen av sidkomponenten; till exempel:

   ```xml
   <your-page-component>/cq:dialog/content/items/tabs/items/basic
   ```

   >[!NOTE]
   >
   >Se följande som referens:
   >
   >    `/libs/wcm/foundation/components/basicpage/v1/basicpage/cq:dialog`
   Du ***får*** dock inte ändra något i `/libs` banan.
   Detta beror på att innehållet i `/libs` skrivs över nästa gång du uppgraderar din instans (och kan mycket väl skrivas över när du använder en snabbkorrigering eller ett funktionspaket).
   Den rekommenderade metoden för konfiguration och andra ändringar är:
   1. Återskapa önskat objekt (t.ex. som det finns i `/libs`) under `/apps`
   1. Gör ändringar i `/apps`


1. Ställ in egenskapen på `path` `basic` att peka på åsidosättningen av grundfliken (se även nästa steg). Exempel:

   ```xml
   /apps/demos/components/page/tabs/basic
   ```

1. Skapa en åsidosättning av avsnittet `basic` - `moretitles` på motsvarande sökväg. till exempel:

   ```xml
   /apps/demos/components/page/tabs/basic/items/column/items/moretitles
   ```

1. Använd lämplig nodegenskap:

   * **Namn**: `cq:showOnCreate`
   * **Typ**: `Boolean`
   * **Värde**: `false`
   Avsnittet **Fler rubriker och beskrivning** visas inte längre i guiden **Skapa sida** .

>[!NOTE]
Mer information finns i [Konfigurera MSM-lås på Sidegenskaper](/help/sites-developing/extending-msm.md#configuring-msm-locks-on-page-properties-touch-enabled-ui) när du konfigurerar sidegenskaper för användning med live-kopior.

## Exempelkonfiguration av sidegenskaper {#sample-configuration-of-page-properties}

Detta exempel visar tekniken för dialog i [Sling Resource Merger](/help/sites-developing/sling-resource-merger.md). inklusive användning av [`sling:orderBefore`](/help/sites-developing/sling-resource-merger.md#properties). Den visar också användningen av både `cq:showOnCreate` och `cq:hideOnEdit`.

KOD PÅ GITHUB

Koden för den här sidan finns på GitHub

* [Öppna aem-authoring-extension-page-dialog-projekt på GitHub](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-page-dialog)
