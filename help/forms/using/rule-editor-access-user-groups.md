---
title: Bevilja regelredigeraråtkomst för valda användargrupper
seo-title: Bevilja regelredigeraråtkomst för valda användargrupper
description: Bevilja begränsad åtkomst till regelredigeraren för att välja användargrupper.
seo-description: Bevilja begränsad åtkomst till regelredigeraren för att välja användargrupper.
uuid: efa2570a-20ac-4b43-8a0e-38247f84d02f
content-type: reference
topic-tags: develop
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: ab694a93-00d2-44d7-8ded-68ab2ad50693
docset: aem65
translation-type: tm+mt
source-git-commit: 44eb94b917fe88b7c90c29ec7da553e15be391db

---


# Bevilja regelredigeraråtkomst för valda användargrupper{#grant-rule-editor-access-to-select-user-groups}

## Översikt {#overview}

Du kan ha olika typer av användare med olika kunskaper som fungerar med adaptiva formulär. Expertanvändare kan ha rätt kunskaper för att arbeta med skript och komplexa regler, men det kan finnas grundläggande användare som bara behöver arbeta med layout och grundläggande egenskaper i anpassade formulär.

Med AEM Forms kan du begränsa regelredigeringsåtkomsten till användare baserat på deras roll eller funktion. I inställningarna för tjänsten Adaptive Forms Configuration kan du ange vilka [användargrupper](/help/sites-administering/security.md) som kan visa och få åtkomst till regelredigeraren.

## Ange användargrupper som kan komma åt regelredigeraren {#specify-user-groups-that-can-access-rule-editor}

1. Logga in på AEM Forms som administratör.
1. I författarinstansen klickar du på ![](assets/adobeexperiencemanager.png)adobeexperienceManagerAdobe Experience Manager > Tools ![hammer](assets/hammer.png) > Operations > Web Console. Webbkonsolen öppnas i ett nytt fönster.

   ![1-2](assets/1-2.png)

1. I webbkonsolfönstret letar du reda på och klickar på **tjänsten** Adaptiv formulärkonfiguration. **Dialogrutan för tjänsten** Adaptive Form Configuration visas. Ändra inget värde och klicka på **Spara**.

   Filen /apps/system/config/com.adobe.aemds.guide.service.impl.AdaptiveFormConfigurationServiceImpl.config skapas i CRX-databasen.

1. Logga in på CRXDE som administratör. Öppna filen /apps/system/config/com.adobe.aemds.guide.service.impl.AdaptiveFormConfigurationServiceImpl.config för redigering.
1. Använd följande egenskap för att ange namnet på en grupp som kan komma åt regelredigeraren (till exempel RuleEditorsUserGroup) och klicka på **Spara alla**.

   `af.ruleeditor.custom.groups=["RuleEditorsUserGroup"]`

   Om du vill aktivera åtkomst för flera grupper anger du en lista med kommasepererade värden:

   `af.ruleeditor.custom.groups=["RuleEditorsUserGroup", "PermittedUserGroup"]`

   ![Skapa användare](assets/create_user_new.png)

   När en användare som inte är en del av en angiven användargrupp (här trycker RuleEditorsUserGroup) på ett fält är ikonen Redigera regel ( ![edit-rules1](assets/edit-rules1.png)) inte tillgänglig för henne i komponentverktygsfältet:

   ![componentsstoolbarwithre](assets/componentstoolbarwithre.png)

   Komponentverktygsfältet så som det visas för en användare med regelredigeringsåtkomst

   ![componentsstoolbarwithout](assets/componentstoolbarwithoutre.png)

   Komponentverktygsfältet så synligt som det är för en användare utan åtkomst till regelredigeraren

   Instruktioner om hur du lägger till användare i grupper finns i [Användaradministration och -säkerhet](/help/sites-administering/security.md).

