---
title: Bevilja regelredigeraråtkomst för valda användargrupper
description: Bevilja begränsad åtkomst till regelredigeraren för att välja användargrupper.
content-type: reference
topic-tags: adaptive_forms, develop
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
feature: Adaptive Forms
exl-id: a1a2b277-3133-404b-a7fc-337cedddb12c
source-git-commit: fd8bb7d3d9040e0a7a6b2f65751445f41aeab73e
workflow-type: tm+mt
source-wordcount: '362'
ht-degree: 0%

---

# Bevilja regelredigeraråtkomst för valda användargrupper{#grant-rule-editor-access-to-select-user-groups}

<span class="preview"> Adobe rekommenderar att man använder modern och utbyggbar datainhämtning [Kärnkomponenter](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html) for [skapa ny Adaptive Forms](/help/forms/using/create-an-adaptive-form-core-components.md) eller [lägga till adaptiv Forms på AEM Sites-sidor](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). De här komponenterna utgör ett betydande framsteg när det gäller att skapa adaptiva Forms-filer, vilket ger imponerande användarupplevelser. I den här artikeln beskrivs ett äldre sätt att skapa adaptiva Forms med baskomponenter. </span>

## Översikt {#overview}

Du kan ha olika typer av användare med olika kunskaper som fungerar med Adaptive Forms. Expertanvändare kan ha rätt kunskaper för att arbeta med skript och komplexa regler, men det kan finnas grundläggande användare som bara behöver arbeta med layout och grundläggande egenskaper i anpassade formulär.

Med AEM Forms kan du begränsa regelredigeringsåtkomsten till användare baserat på deras roll eller funktion. I inställningarna för Adaptive Forms Configuration Service kan du ange [användargrupper](/help/sites-administering/security.md) som kan visa och komma åt regelredigeraren.

## Ange användargrupper som kan komma åt regelredigeraren {#specify-user-groups-that-can-access-rule-editor}

1. Logga in på AEM Forms som administratör.
1. Klicka på i författarinstansen ![adobeexperienceManager](assets/adobeexperiencemanager.png)Adobe Experience Manager > Verktyg ![hammare](assets/hammer.png) > Åtgärder > Webbkonsol. Webbkonsolen öppnas i ett nytt fönster.

   ![1-2](assets/1-2.png)

1. I webbkonsolfönstret letar du upp och klickar på **[!UICONTROL Adaptive Form and Interactive Communication Web Channel Configuration]**. **[!UICONTROL Adaptive Form and Interactive Communication Web Channel Configuration]** visas. Ändra inga värden och klicka **Spara**.

   Filen /apps/system/config/com.adobe.aemds.guide.service.impl.AdaptiveFormConfigurationServiceImpl.config skapas i CRX-databasen.

1. Logga in på CRXDE som administratör. Öppna filen /apps/system/config/com.adobe.aemds.guide.service.impl.AdaptiveFormConfigurationServiceImpl.config för redigering.
1. Använd följande egenskap för att ange namnet på en grupp som kan komma åt regelredigeraren (till exempel RuleEditorsUserGroup) och klicka på **Spara alla**.

   `af.ruleeditor.custom.groups=["RuleEditorsUserGroup"]`

   Om du vill aktivera åtkomst för flera grupper anger du en lista med kommaseparerade värden:

   `af.ruleeditor.custom.groups=["RuleEditorsUserGroup", "PermittedUserGroup"]`

   ![Skapa användare](assets/create_user_new.png)

   När en användare som inte är en del av den angivna användargruppen (här trycker RuleEditorsUserGroup) på ett fält visas nu ikonen Redigera regel ( ![edit-rules1](assets/edit-rules1.png)) är inte tillgängligt för dem i komponentverktygsfältet:

   ![componentsstoolbarwithre](assets/componentstoolbarwithre.png)

   Komponentverktygsfältet så som det visas för en användare med regelredigeringsåtkomst

   ![componentsstoolbarwithout](assets/componentstoolbarwithoutre.png)

   Komponentverktygsfältet så synligt som det är för en användare utan regelredigeringsåtkomst

   Instruktioner om hur du lägger till användare i grupper finns i [Användaradministration och -säkerhet](/help/sites-administering/security.md).
