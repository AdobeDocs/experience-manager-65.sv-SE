---
title: Bevilja regelredigeraråtkomst för valda användargrupper
seo-title: Bevilja regelredigeraråtkomst för valda användargrupper
description: Bevilja begränsad åtkomst till regelredigeraren för att välja användargrupper.
seo-description: Bevilja begränsad åtkomst till regelredigeraren för att välja användargrupper.
uuid: efa2570a-20ac-4b43-8a0e-38247f84d02f
content-type: reference
topic-tags: adaptive_forms, develop
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: ab694a93-00d2-44d7-8ded-68ab2ad50693
docset: aem65
feature: Adaptive Forms
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '322'
ht-degree: 0%

---


# Bevilja regelredigeringsåtkomst för valda användargrupper{#grant-rule-editor-access-to-select-user-groups}

## Översikt {#overview}

Du kan ha olika typer av användare med olika kunskaper som fungerar med Adaptive Forms. Expertanvändare kan ha rätt kunskaper för att arbeta med skript och komplexa regler, men det kan finnas grundläggande användare som bara behöver arbeta med layout och grundläggande egenskaper i anpassade formulär.

Med AEM Forms kan du begränsa regelredigeringsåtkomsten till användare baserat på deras roll eller funktion. I inställningarna för den adaptiva Forms-konfigurationstjänsten kan du ange de [användargrupper](/help/sites-administering/security.md) som kan visa och komma åt regelredigeraren.

## Ange användargrupper som kan komma åt regelredigeraren {#specify-user-groups-that-can-access-rule-editor}

1. Logga in på AEM Forms som administratör.
1. I författarinstansen klickar du på ![adobeexperienceManager](assets/adobeexperiencemanager.png)Adobe Experience Manager > Verktyg ![hammer](assets/hammer.png) > Åtgärder > Webbkonsol. Webbkonsolen öppnas i ett nytt fönster.

   ![1-2](assets/1-2.png)

1. I webbkonsolfönstret letar du reda på och klickar på **[!UICONTROL Adaptive Form and Interactive Communication Web Channel Configuration]**. **[!UICONTROL Adaptive Form and Interactive Communication Web Channel Configuration]** visas. Ändra inga värden och klicka på **Spara**.

   Filen /apps/system/config/com.adobe.aemds.guide.service.impl.AdaptiveFormConfigurationServiceImpl.config skapas i CRX-databasen.

1. Logga in på CRXDE som administratör. Öppna filen /apps/system/config/com.adobe.aemds.guide.service.impl.AdaptiveFormConfigurationServiceImpl.config för redigering.
1. Använd följande egenskap för att ange namnet på en grupp som har åtkomst till regelredigeraren (till exempel RuleEditorsUserGroup) och klicka på **Spara alla**.

   `af.ruleeditor.custom.groups=["RuleEditorsUserGroup"]`

   Om du vill aktivera åtkomst för flera grupper anger du en lista med kommasepererade värden:

   `af.ruleeditor.custom.groups=["RuleEditorsUserGroup", "PermittedUserGroup"]`

   ![Skapa användare](assets/create_user_new.png)

   När en användare som inte är en del av en angiven användargrupp (här trycker RuleEditorsUserGroup) på ett fält är ikonen Redigera regel ( ![edit-rules1](assets/edit-rules1.png)) inte tillgänglig för henne i komponentens verktygsfält:

   ![componentsstoolbarwithre](assets/componentstoolbarwithre.png)

   Komponentverktygsfältet så som det visas för en användare med regelredigeringsåtkomst

   ![componentsstoolbarwithout](assets/componentstoolbarwithoutre.png)

   Komponentverktygsfältet så synligt som det är för en användare utan åtkomst till regelredigeraren

   Instruktioner om hur du lägger till användare i grupper finns i [Användaradministration och -säkerhet](/help/sites-administering/security.md).

