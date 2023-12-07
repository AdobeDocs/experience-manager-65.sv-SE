---
title: Anpassa vyer av Sidegenskaper
description: Varje sida har en uppsättning egenskaper som du kan redigera efter behov
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
exl-id: 292874bf-2ee6-4638-937c-f8f26c93ca65
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '475'
ht-degree: 0%

---

# Anpassa vyer av Sidegenskaper{#customizing-views-of-page-properties}

Varje sida har en uppsättning [egenskaper](/help/sites-authoring/editing-page-properties.md) som kan visas och redigeras av användare. En del krävs när du skapar sidan (skapar vy), andra kan visas och redigeras (redigeringsvy) i ett senare skede. Dessa sidegenskaper definieras och görs tillgängliga i dialogrutan ( `cq:dialog`) för rätt sidkomponent.

>[!CAUTION]
>
>Det klassiska användargränssnittet gör det inte möjligt att anpassa vyn för sidegenskaper.

Standardläget för varje sidegenskap är:

* dolt i vyn Skapa (till exempel **Skapa sida** guide)

* som finns i redigeringsvyn (t.ex. **Visa egenskaper**)

Fälten måste vara specifikt konfigurerade om någon ändring krävs. Detta görs med lämpliga nodegenskaper:

* Page-egenskap som ska vara tillgänglig i vyn create (till exempel **Skapa sida** guide):

   * Namn: `cq:showOnCreate`
   * Typ: `Boolean`

* Page-egenskap som ska vara tillgänglig i redigeringsvyn (till exempel **Visa**/**Redigera**) **Egenskaper** alternativ):

   * Namn: `cq:hideOnEdit`
   * Typ: `Boolean`

Se till exempel inställningarna för fält som grupperats under **Fler rubriker och beskrivning** på **Grundläggande** -fliken för grundsidkomponenten. Dessa visas i **Skapa sida** guide som `cq:showOnCreate` har angetts till `true`:

```xml
/libs/foundation/components/page/cq:dialog/content/items/tabs/items/basic/items/column/items/moretitles
```

>[!TIP]
>
>Se [Utöka Sidegenskaper, genomgång](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/developing/page-properties-technical-video-develop.html) för att få hjälp med att anpassa sidegenskaper.

## Konfigurera dina sidegenskaper {#configuring-your-page-properties}

Du kan också konfigurera fälten som är tillgängliga genom att konfigurera dialogrutan för sidkomponenten och använda lämpliga nodegenskaper.

Som standard är [**Skapa sida** guide](/help/sites-authoring/managing-pages.md#creating-a-new-page) visar fält grupperade under **Fler rubriker och beskrivning**. Så här döljer du dessa konfigurationer:

1. Skapa sidkomponenten under `/apps`.
1. Skapa en åsidosättning (med *dialogruta* tillhandahålls av [Samla resurser](/help/sites-developing/sling-resource-merger.md)) för `basic` del av sidkomponenten, till exempel:

   ```xml
   <your-page-component>/cq:dialog/content/items/tabs/items/basic
   ```

   >[!NOTE]
   >
   >Se följande som referens:
   >
   >    `/libs/wcm/foundation/components/basicpage/v1/basicpage/cq:dialog`
   >
   Du kan dock ***måste*** ändrar ingenting i dialogrutan `/libs` bana.
   >
   Detta beror på innehållet i `/libs` skrivs över nästa gång du uppgraderar din instans (och kan mycket väl skrivas över när du installerar en snabbkorrigering eller ett funktionspaket).
   >
   Den rekommenderade metoden för konfiguration och andra ändringar är:
   >
   1. Återskapa önskat objekt (d.v.s. som det finns i `/libs`) under `/apps`
   1. Gör ändringar i `/apps`

1. Ange `path` egenskap på `basic` för att peka på åsidosättningen av den grundläggande fliken (se även nästa steg). Till exempel:

   ```xml
   /apps/demos/components/page/tabs/basic
   ```

1. Skapa en åsidosättning av `basic` - `moretitles` i motsvarande sökväg, till exempel:

   ```xml
   /apps/demos/components/page/tabs/basic/items/column/items/moretitles
   ```

1. Använd lämplig nodegenskap:

   * **Namn**: `cq:showOnCreate`
   * **Typ**: `Boolean`
   * **Värde**: `false`

   The **Fler rubriker och beskrivning** -avsnittet visas inte längre i **Skapa sida** guide.

>[!NOTE]
>
Information om hur du konfigurerar sidegenskaper för användning med live-kopior finns i [Konfigurera MSM-lås på sidegenskaper](/help/sites-developing/extending-msm.md#configuring-msm-locks-on-page-properties-touch-enabled-ui) för mer information.

## Exempelkonfiguration av sidegenskaper {#sample-configuration-of-page-properties}

I det här exemplet visas tekniken för dialogrutor i [Samla resurser](/help/sites-developing/sling-resource-merger.md), inklusive användning av [`sling:orderBefore`](/help/sites-developing/sling-resource-merger.md#properties). Det visar också hur man använder båda `cq:showOnCreate` och `cq:hideOnEdit`.

KOD PÅ GITHUB

Koden för den här sidan finns på GitHub

* [Öppna aem-authoring-extension-page-dialog-projekt på GitHub](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-page-dialog)
