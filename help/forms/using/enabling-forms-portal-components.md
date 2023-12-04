---
title: Aktivera komponenterna i formulärportalen
seo-title: Enabling forms portal components
description: Forms Portal-komponenter är inaktiverade. Aktivera grupper med Document Services och Document Services Predicates för att aktivera Forms Portal-komponenter.
seo-description: Out of the box, Forms Portal components are disabled. Enable Document Services and Document Services Predicates groups to enable Forms Portal components.
uuid: 92d25da6-f1df-4ac0-bf84-2edf9e2722b3
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: 4d318908-c724-4582-a82b-6e9b1c55705b
feature: Forms Portal
exl-id: 572194b7-063b-4c38-af43-aba78e9c51c6
source-git-commit: bd86d647fdc203015bc70a0f57d5b94b4c634bf9
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

   1. I sidhuvudet väljer du ![canvas-drop-down](assets/canvas-drop-down.png) > **Design** för att öppna sidan i designläge.
   1. Markera en komponent (med en blå ram) och markera sedan ![fältnivå](assets/field-level.png) för att markera det styckesystem som innehåller den aktuella komponenten.
   1. Välj ![settings_icon](assets/settings_icon.png) för att öppna dialogrutan Redigera för styckesystemet.
   1. I listan över **[!UICONTROL Allowed Components]**, aktivera kryssrutor för **[!UICONTROL Document Services]** och **[!UICONTROL Document Services Predicates]** -komponenter. Välj **[!UICONTROL OK]**.

1. Utför följande steg för de sidor som använder en dynamisk mall:

   1. I sidhuvudet väljer du ![egenskaper](assets/properties.png) > **Redigera mall** för att öppna sidans mall.
   1. Välj **Layoutbehållare** och markera ![FeedManagement](/help/forms/using/assets/feedmanagement.png). I **Tillåtna komponenter** -fliken, aktivera **Document Services och Document Services - predikat** och markera ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

>[!NOTE]
>
>Du kan också aktivera specifika komponenter från dessa kategorier genom att markera komponenterna. Mer information om komponenterna och deras användning finns i [Skapa en formulärportalsida](/help/forms/using/creating-form-portal-page.md) och [Bädda in länkkomponent på en sida](/help/forms/using/embedding-link-component-page.md).

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
