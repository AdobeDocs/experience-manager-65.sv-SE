---
title: Återanvända adaptiva formulär
description: Du kan återanvända ett befintligt adaptivt formulär för att skapa nya adaptiva formulär.
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: ef564750-f107-41cb-887e-fc6d22b7d32e
feature: Adaptive Forms, Foundation Components
exl-id: d8ee4e82-3137-430e-aa47-b00191f2729c
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '593'
ht-degree: 1%

---

# Återanvända adaptiva formulär {#reusing-adaptive-forms}

<span class="preview"> Adobe rekommenderar att man använder modern och utbyggbar datainhämtning [Kärnkomponenter](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html) for [skapa ny Adaptive Forms](/help/forms/using/create-an-adaptive-form-core-components.md) eller [lägga till adaptiv Forms på AEM Sites-sidor](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). De här komponenterna utgör ett betydande framsteg när det gäller att skapa adaptiva Forms-filer, vilket ger imponerande användarupplevelser. I den här artikeln beskrivs det äldre sättet att skapa Adaptiv Forms med baskomponenter. </span>

| Version | Artikellänk |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Klicka här](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/manage-metadata/reusing-adaptive-forms.html) |
| AEM 6.5 | Den här artikeln |

## Introduktion {#introduction}

Om du vill använda vissa av egenskaperna i ett befintligt adaptivt formulär för att generera ett nytt, behöver du bara använda funktionen för att kopiera och klistra in. Dessutom kan du klistra in det nya adaptiva formuläret i önskad mappsökväg. Alla metadataegenskaper replikeras och XFA- och XSD-värdena för XFA- och XSD-baserade adaptiva formulär kopieras också.

>[!NOTE]
>
>Status och granskningsinformation kopieras inte. Om det adaptiva formuläret till exempel publiceras och sedan kopieras, är det inklistrade adaptiva formuläret inte publicerat. På samma sätt gäller att om en kopierad resurs håller på att granskas är den inklistrade resursen inte under samma granskning.

### Kopiera ett anpassat formulär {#copy-an-adaptive-form}

Kopiera ett anpassat formulär på något av följande sätt:

1. Klicka på Kopiera ![aem6forms_copy](assets/aem6forms_copy.png) -ikon från snabbåtgärder.

   >[!NOTE]
   >
   >Snabbåtgärder är de åtgärdsobjekt som visas över en miniatyrbild när du håller muspekaren.

1. Markera det adaptiva formuläret. Markeringsprocessen är annorlunda för olika vyer.

   Om du arbetar i kortvyn går du till markeringsläget genom att klicka på markeringen ![aem6forms_check-circle](assets/aem6forms_check-circle.png) och klicka på alla adaptiva formulär som du vill kopiera.

   Om du är i listvyn markerar du kryssrutorna för alla adaptiva formulär.

   >[!NOTE]
   >
   >Alla markerade resurser måste vara adaptiva formulär eftersom funktionen kopiera och klistra in bara stöds för adaptiva formulär, och alla resurser som är markerade måste finnas i samma mapp.

   När du har valt resurserna klickar du på kopian ![aem6forms_copy](assets/aem6forms_copy.png) ikon finns i verktygsfältet för att kopiera det markerade adaptiva formuläret.

### Klistra in ett anpassat formulär {#paste-an-adaptive-form}

När du klickar på kopieringsåtgärden avslutas markeringsläget automatiskt och klistra in ![aem6forms_paste](assets/aem6forms_paste.png) -ikonen visas. Gå till önskad mappsökväg och klicka på Klistra in ![aem6forms_paste](assets/aem6forms_paste.png) om du vill klistra in det kopierade adaptiva formuläret.

Om du klistrar in i samma mapp eller en annan fil med samma nodnamn (som den lagras i CRX-databasen med) finns i den här målmappen läggs 1 till i suffixet (till exempel blir myaf1 och om myaf1 finns på samma plats blir myaf2. Alla andra egenskaper är desamma som det ursprungliga adaptiva formuläret.

När du klickat på Klistra in ![aem6forms_paste](assets/aem6forms_paste.png) kommer den att döljas igen. Du kan bara klistra in en gång. Om du vill skapa en kopia av samma resurs kopierar du den igen.

### Ändra innehållet i det nya adaptiva formuläret {#change-contents-of-new-adaptive-form}

Innehållet i en inklistrad adaptiv form kan ändras på följande sätt så att det skiljer sig från det kopierade formuläret:

1. **Ändra metadataegenskaper:**

   Du kan ändra metadataegenskaperna för det adaptiva formuläret, till exempel rubrik och beskrivning. Mer information om metadataegenskaper och hur de kan ändras finns i [Hantera formulärmetadata](/help/forms/using/manage-form-metadata.md)

1. **Ändra XFA/XSD för XFA/XSD-baserad Adaptive Forms:**

   Du kan ändra den XFA/XSD som används i adaptiva formulär. Om du vill veta hur dessa adaptiva formulär kan ändras kan du läsa [Hantera formulärmetadata](/help/forms/using/manage-form-metadata.md)

1. **Publicera igen:**

   Den inklistrade resursen skiljer sig från den kopierade. Du kan publicera den som en ny resurs för att göra den tillgänglig för slutanvändare. Mer information om hur du publicerar en resurs finns i [Publicera och avpublicera formulär](/help/forms/using/publishing-unpublishing-forms.md)
