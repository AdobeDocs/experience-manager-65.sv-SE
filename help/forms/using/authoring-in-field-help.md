---
title: Sammanhangsberoende hjälp för formulärfält
seo-title: Sammanhangsberoende hjälp för formulärfält
description: Med AEM Forms kan du lägga till sammanhangsberoende hjälp till anpassningsbara formulärfält och paneler, som text eller multimedia, inklusive videor.
seo-description: Med AEM Forms kan du lägga till sammanhangsberoende hjälp till anpassningsbara formulärfält och paneler, som text eller multimedia, inklusive videor.
uuid: 1865bf7b-66fc-4f89-bd98-904daa409320
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 78000342-a6a7-4c2e-acab-a88851b82c2a
docset: aem65
translation-type: tm+mt
source-git-commit: 8bc99ed3817398ae358d439a5c1fcc90bbd24327

---


# Sammanhangsberoende hjälp för formulärfält{#authoring-in-context-help-for-form-fields}

## Introduktion {#introduction}

Det finns situationer när slutanvändare som fyller i ett formulär inte vet hur de ska fylla i information i ett visst formulärfält. För att åtgärda sådana problem har adaptiva formulär stöd för att lägga till text eller sammanhangsberoende hjälp i ett formulärfält. Det underlättar ifyllandet av formulär och undviker eventuella tvetydigheter för slutanvändarna.

I den här artikeln beskrivs hur formulärförfattare kan lägga till sammanhangsberoende hjälp när de skapar adaptiva formulär.

## Lägg till sammanhangsberoende hjälp {#add-in-context-help}

Du kan ange sammanhangsberoende hjälp med följande alternativ i hjälpavsnittet på egenskapsfliken i sidofältet.

* [Kort beskrivning](../../forms/using/authoring-in-field-help.md#p-short-description-p)
* [Lång beskrivning](../../forms/using/authoring-in-field-help.md#p-long-description-p)

![Kontexthjälp för formulärfält](assets/descriptions.png)

>[!NOTE]
>
>Lång beskrivning åsidosätter den korta beskrivningen. Om du har angett båda visas bara Lång beskrivning.

### Kort beskrivning {#short-description}

Fältet Kort beskrivning ger snabba och korta tips om hur du fyller i ett formulärfält. Texten som anges i fältet Kort beskrivning visas som ett verktygstips när du håller muspekaren över fältet.

![Kort beskrivning för att lägga till sammanhangsberoende hjälp för formulärfält](assets/tooltip.png)

>[!NOTE]
>
>Markera **Visa alltid kort beskrivning** för att permanent visa hjälptexten under fältet.

![Permanent kort sammanhangsberoende hjälp nedanför fältet](assets/short1.png)

### Lång beskrivning {#long-description}

Du kan använda fältet Lång beskrivning för att ange lång text eller bädda in multimedieinnehåll, inklusive videor, som sammanhangsberoende hjälp. I följande bild visas hur du kan bädda in en video som sammanhangsberoende hjälp.

![Lägga till multimedia som sammanhangsberoende hjälp för formulärfält](assets/long-descriptions.png)

Om du lägger till lång beskrivning visas en **?** -ikonen bredvid fältet. När du klickar på ikonen visas det innehåll som lagts till i avsnittet med lång beskrivning.

![Exempel på sammanhangsberoende multimediahjälp](assets/photoshop.png)

### Hjälp på panelnivå {#panel-level-help}

Utöver sammanhangsberoende hjälp för formulärfält kan du ange hjälp på panelnivå på fliken Hjälpinnehåll i dialogrutan Redigera i panelen.

![Lägga till sammanhangsberoende hjälp för en formulärpanel](assets/panel-level-help.png)

Vill du lägga till hjälp för panelen visas en **?** -ikonen bredvid panelbeskrivningen. När du klickar på ikonen visas det innehåll som lagts till i hjälpdelen i dialogrutan Redigera i panelen.

![Exempel på sammanhangsberoende hjälp på formulärpanelsnivå](assets/photoshop-1.png)

