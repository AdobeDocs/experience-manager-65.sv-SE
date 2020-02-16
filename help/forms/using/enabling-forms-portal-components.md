---
title: Aktivera komponenterna i formulärportalen
seo-title: Aktivera komponenterna i formulärportalen
description: Komponenterna i Forms Portal är inaktiverade. Aktivera grupper med Document Services och Document Services Predicates för att aktivera komponenter för Forms Portal.
seo-description: Komponenterna i Forms Portal är inaktiverade. Aktivera grupper med Document Services och Document Services Predicates för att aktivera komponenter för Forms Portal.
uuid: 92d25da6-f1df-4ac0-bf84-2edf9e2722b3
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: 4d318908-c724-4582-a82b-6e9b1c55705b
translation-type: tm+mt
source-git-commit: a209b2dda04985a3f2d7c6838f11f0b5dc62d520

---


# Aktivera komponenterna i formulärportalen {#enabling-forms-portal-components}

Komponenterna i formulärportalen är inte tillgängliga för användning. Gör så här för att visa komponenterna i listan över tillgängliga komponenter i AEM-sidosparken:

1. Logga in på webbplatsens författarinstans och öppna en AEM Sites-sida.

1. Utför följande steg för de sidor som använder en statisk mall:

   1. I sidhuvudet trycker du på ![listrutan](assets/canvas-drop-down.png) Canvas > **Design** för att öppna sidan i designläge.
   1. Tryck på en komponent (med en blå kant) och tryck sedan på ![fältnivån](assets/field-level.png) för att välja det styckesystem som innehåller den aktuella komponenten.
   1. Tryck på ![settings_icon](assets/settings_icon.png) i styckesystemet för att öppna dialogrutan Redigera för styckesystemet.
   1. Aktivera kryssrutor för komponenterna **[!UICONTROL Tillåtna komponenter]** i listan över tillåtna komponenter för **[!UICONTROL Document Services]** och **[!UICONTROL Document Services Predicates]** . Tryck på **[!UICONTROL OK]**.

1. Utför följande steg för de sidor som använder en dynamisk mall:

   1. I sidhuvudet trycker du på ![egenskaper](assets/properties.png) > **Redigera mall** för att öppna sidans mall.
   1. Tryck på **Layoutbehållare** och tryck på ![FeedManagement](/help/forms/using/assets/feedmanagement.png). På fliken **Tillåtna komponenter** aktiverar du alternativen **Document Services och Document Services Predicates** och trycker på ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

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
