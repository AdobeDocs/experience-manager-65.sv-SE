---
title: Aktivera komponenterna i formulärportalen
description: Forms Portal-komponenter är inaktiverade. Aktivera grupper med Document Services och Document Services Predicates för att aktivera Forms Portal-komponenter.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
feature: Forms Portal
exl-id: 572194b7-063b-4c38-af43-aba78e9c51c6
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '324'
ht-degree: 1%

---

# Aktivera komponenterna i formulärportalen {#enabling-forms-portal-components}

| Version | Artikellänk |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Klicka här](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-forms-portal.html) |
| AEM 6.5 | Den här artikeln |

Komponenterna i formulärportalen är inte tillgängliga för användning. Gör så här för att visa komponenterna i listan över tillgängliga komponenter i AEM.

1. Logga in på webbplatsens författarinstans och öppna en AEM Sites-sida.

1. Utför följande steg för de sidor som använder en statisk mall:

   1. I sidhuvudet väljer du ![listrutan för arbetsyta](assets/canvas-drop-down.png) > **Design** för att öppna sidan i designläge.
   1. Markera en komponent (med en blå kant) och välj sedan ![fältnivå](assets/field-level.png) för att välja det styckesystem som innehåller den aktuella komponenten.
   1. I styckesystemet väljer du ![settings_icon](assets/settings_icon.png) för att öppna dialogrutan Redigera för styckesystemet.
   1. Aktivera kryssrutor för komponenterna **[!UICONTROL Document Services]** och **[!UICONTROL Document Services Predicates]** i listan med **[!UICONTROL Allowed Components]**. Välj **[!UICONTROL OK]**.

1. Utför följande steg för de sidor som använder en dynamisk mall:

   1. I sidhuvudet väljer du ![egenskaper](assets/properties.png) > **Redigera mall** för att öppna sidans mall.
   1. Välj **Layoutbehållare** och välj ![FeedManagement](/help/forms/using/assets/feedmanagement.png). På fliken **Tillåtna komponenter** aktiverar du alternativen **Document Services och Document Services Predicates** och väljer ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

>[!NOTE]
>
>Du kan också aktivera specifika komponenter från dessa kategorier genom att markera komponenterna. Mer information om komponenterna och hur de används finns i [Skapa en formulärportalsida](/help/forms/using/creating-form-portal-page.md) och [Bädda in länkkomponent på en sida](/help/forms/using/embedding-link-component-page.md).

Nu är komponentkategorierna Document Services och Document Services Predicates tillgängliga i komponentwebbläsaren. Komponenterna aktiveras för alla sidor som använder samma mall.

## Relaterade artiklar

* [Aktivera komponenter i formulärportalen](/help/forms/using/enabling-forms-portal-components.md)
* [Skapa portalsida för formulär](/help/forms/using/creating-form-portal-page.md)
* [Visa formulär på en webbsida med API:er](/help/forms/using/listing-forms-webpage-using-apis.md)
* [Använda komponenten Utkast och inskickat material](/help/forms/using/draft-submission-component.md)
* [Anpassa lagring av utkast och inskickade formulär](/help/forms/using/draft-submission-component.md)
* [Exempel för att integrera komponent för utkast och inlämning med databas](/help/forms/using/integrate-draft-submission-database.md)
* [Anpassa mallar för komponenter i formulärportalen](/help/forms/using/customizing-templates-forms-portal-components.md)
* [Introduktion till att publicera formulär på en portal](/help/forms/using/introduction-publishing-forms.md)
