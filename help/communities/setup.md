---
title: Inledande konfiguration
seo-title: Inledande konfiguration
description: Konfigurera communities
seo-description: Konfigurera communities
uuid: c53d280c-c5ae-47cf-8038-f0dea68e15ff
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: introduction
content-type: reference
discoiquuid: 0d462ad1-5619-4bb6-9609-bc8987c40a0c
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '678'
ht-degree: 0%

---


# Inledande inställning {#initial-setup}

## Starta författare och publiceringsinstanser {#start-author-and-publish-instances}

I utvecklings- och demonstrationssyfte måste du köra en författare och en publiceringsinstans.

Om du vill göra det följer du de grundläggande AEM [Komma igång](../../help/sites-deploying/deploy.md#getting-started)-instruktionerna, som resulterar i:

* Redigeringsmiljö på [localhost:4502](http://localhost:4502/)
* Publiceringsmiljö på [localhost:4503](http://localhost:4503/)

För AEM Communities

* Författarmiljön är till för:

   * Utveckling av webbplatser, mallar och komponenter.
   * Administrations- och konfigureringsuppgifter.

* Publiceringsmiljön är avsedd för:

   * Användarupplevelsen när det gäller publicering och moderering av innehåll.
   * Skapa communitygrupper, medlemmar och medlemsgrupper.

>[!NOTE]
>
>Om du inte känner till AEM kan du läsa dokumentationen om [grundläggande hantering](../../help/sites-authoring/basic-handling.md) och en [snabbguide till redigeringssidor](../../help/sites-authoring/qg-page-authoring.md).

## Installera den senaste versionen av Communities {#install-latest-communities-release}

I den här självstudien skapas en [engagemangscommunitywebbplats](overview.md#engagement-community) och den baseras på AEM Communities 6.2 feature pack version 1.10.

Se till att det senaste funktionspaketet är installerat på:

* [Senaste releaser](deploy-communities.md#latest-releases)

En självstudiekurs som skapar en [aktiveringscommunitywebbplats](overview.md#enablement-community) finns på [Komma igång med AEM Communities för Enablement](getting-started-enablement.md).

## Konfigurera analys {#configure-analytics}

När [Adobe Analytics har konfigurerats för communitywebbplatsen](analytics.md) finns det information om communityaktivitet som förbättrar communitymedlemmens upplevelse och ger återkoppling till webbplatsens administratörer.

Integrering med Adobe Analytics är valfritt.

## Konfigurera e-post för meddelanden {#configure-email-for-notifications}

Meddelandefunktionen, som är tillgänglig som standard för alla webbplatser som skapats med `Communities Sites`-konsolen, erbjuder en e-postkanal för meddelanden.

Det som är nödvändigt är att e-post konfigureras korrekt för webbplatsen.

Se [Konfigurera e-post](email.md).

## Aktivera tunneltjänsten {#enable-the-tunnel-service}

När du skapar en community-webbplats i författarmiljön gör tunneltjänsten det möjligt att tilldela roller till betrodda communitymedlemmar som är registrerade i publiceringsmiljön. Tunneltjänsten ger även åtkomst till communitymedlemmar från [Konsolerna Medlemmar och Grupper](members.md) i författarmiljön.

Konventionen gäller för medlemmar och medlemsgrupper som skapats i publiceringsmiljön till *inte* som ska återskapas i författarmiljön. Mer information finns i [Hantera användare och användargrupper](users.md).

Mer information om hur du aktiverar tunneltjänsten på en **författare**-instans finns i [tunneltjänst](deploy-communities.md#tunnel-service-on-author).

## Rollen Community Administrator {#community-administrator-role}

Medlemmar i gruppen Community Administrators kan skapa communitysajter, hantera webbplatser, hantera medlemmar (de kan förbjuda medlemmar från communityn) och moderera innehåll.

### Skapa användare {#create-user}

Skapa en användare på *författare*, som tilldelas rollen Community Administrator:

* På författarinstansen

   * Till exempel [http://localhost:4502/](http://localhost:4503/)

* Logga in med administratörsbehörighet

   * Till exempel användarnamn &#39;admin&#39; / lösenord &#39;admin&#39;

* Gå till **[!UICONTROL Tools]** > **[!UICONTROL Operations]** > **[!UICONTROL Security]** > **[!UICONTROL Users]** från huvudkonsolen.
* Välj **[!UICONTROL Add User]** på menyn **Redigera**

* I dialogrutan `Create New User` anger du:

   * **[!UICONTROL ID]**: sirius
   * **[!UICONTROL Emai Address]**: sirius.nilson@mailinator.com
   * **[!UICONTROL Password]**: password
   * **[!UICONTROL Confirm Password&ast;]**: lösenord
   * **[!UICONTROL First Name]**: Sirius
   * **[!UICONTROL Last Name]**: Nilson

### Tilldela Sirius till communityadministratörsgruppen {#assign-sirius-to-community-administrators-group}

Bläddra ned till `Add User to Groups`:

* Ange &quot;C&quot; för att söka

   * Välj `Community Administrators`
   * Välj `Community Enablement Managers`

* Välj **[!UICONTROL Save]**.

![create-user](assets/create-user.png)

## Aktivera social inloggning {#enable-social-login}

Innan demonstrationsversionerna av social inloggning med Facebook och Twitter kan användas är det nödvändigt att

1. Installera ett korrigeringspaket eller [det senaste funktionspaketet](deploy-communities.md#latestfeaturepack) (för ändringar i Facebook-API:t från mars 2017).
1. [Aktivera OAuth-](social-login.md#adobe-granite-oauth-authentication-handler) providern i publiceringsmiljön.

För produktionsservrar är det nödvändigt att skapa de molntjänster som krävs för att tillhandahålla social inloggning.

Se [Social inloggning på Facebook och Twitter](social-login.md).

## Skapa självstudietaggar {#create-tutorial-tags}

Skapa taggar som ska användas för interaktions- och aktiveringssjälvstudiekurserna med hjälp av taggnamnutrymmet `Tutorial`.

Använd [taggningskonsolen](../../help/sites-administering/tags.md#tagging-console) för att skapa följande taggar:

* `Tutorial: Sports / Baseball`
* `Tutorial: Sports / Gymnastics`
* `Tutorial: Sports / Skiing`
* `Tutorial: Arts / Visual`
* `Tutorial: Arts / Auditory`
* `Tutorial: Arts / History`

![självstudiekurstaggar](assets/tutorial-tags.png)

Följ sedan instruktionerna för att:

1. [Ange taggbehörigheter](../../help/sites-administering/tags.md#setting-tag-permissions).
1. [Publicera taggarna](../../help/sites-administering/tags.md#publishing-tags).

Exempelpaket med taggar som skapats för Tutorials AEM Communities Getting Started

[Hämta fil](assets/tutorial_tags-v63.zip)

## MongoDB för UGC Common Store {#mongodb-for-ugc-common-store}

Vi rekommenderar, men är valfria, att du anger [MSRP](msrp.md) (MongoDB) som [gemensam lagringsplats](working-with-srp.md) för att du ska kunna moderera all UGC från publicerings- och/eller författarmiljöer.

Instruktioner finns på [Så här installerar du MongoDB för demo](demo-mongo.md).

Installationen av författaren och publiceringsinstanserna AEM som standard resulterar i att användargenererat innehåll (UGC) lagras i [JCR-tjärlagring](../../help/sites-deploying/platform.md) som du kommer åt med [JSRP](jsrp.md). JSRP är inte en vanlig lagringsplats, vilket innebär att UGC bara visas på den instans där den angavs. Vanligtvis anges UGC i en publiceringsinstans och skulle inte vara synligt i redigeringsmiljön, vilket resulterar i att alla modereringsåtgärder måste använda publiceringsinstansen.