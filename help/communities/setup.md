---
title: Inledande konfiguration
description: Lär dig hur du först skapar Adobe Experience Manager Communities.
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: introduction
content-type: reference
exl-id: 6bda0f09-7ae5-4540-b035-9dd249ac3186
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '666'
ht-degree: 0%

---

# Inledande konfiguration {#initial-setup}

## Starta författare och Publish-instanser {#start-author-and-publish-instances}

För utvecklings- och demonstrationssyften är det nödvändigt att köra en författare och en publiceringsinstans.

Om du vill göra det följer du de grundläggande instruktionerna i Adobe Experience Manager (AEM) [Komma igång](../../help/sites-deploying/deploy.md#getting-started) som ger följande resultat:

* Redigeringsmiljö på [localhost:4502](http://localhost:4502/)
* Publish-miljö på [localhost:4503](http://localhost:4503/)

För AEM Communities

* Författarmiljön är avsedd för:

   * Utveckling av webbplatser, mallar och komponenter.
   * Administrations- och konfigureringsuppgifter.

* Publish-miljön är avsedd för:

   * Användarupplevelsen när det gäller publicering och moderering av innehåll.
   * Skapa communitygrupper, medlemmar och medlemsgrupper.

>[!NOTE]
>
>Om du inte känner till AEM kan du läsa dokumentationen om [grundläggande hantering](../../help/sites-authoring/basic-handling.md) och en [snabbguide till redigeringssidor](../../help/sites-authoring/qg-page-authoring.md).

## Installera senaste versionen av Communities {#install-latest-communities-release}

I den här självstudien skapas en [engagemangscommunitywebbplats](overview.md#engagement-community) och den baseras på AEM Communities 6.2 feature pack version 1.10.

Se till att det senaste funktionspaketet är installerat på:

* [Senaste releaser](deploy-communities.md#latest-releases)

## Konfigurera analys {#configure-analytics}

När [Adobe Analytics har konfigurerats för communitywebbplatsen](analytics.md) finns det information om communityaktivitet som förbättrar communitymedlemmens upplevelse och ger feedback till webbplatsens administratörer.

Integrering med Adobe Analytics är valfritt.

## Konfigurera e-post för meddelanden {#configure-email-for-notifications}

Meddelandefunktionen, som är tillgänglig som standard för alla webbplatser som skapats med konsolen `Communities Sites`, erbjuder en e-postkanal för meddelanden.

Det som är nödvändigt är att e-post konfigureras korrekt för webbplatsen.

Se [Konfigurera e-post](email.md).

## Aktivera tunneltjänsten {#enable-the-tunnel-service}

När du skapar en communitywebbplats i redigeringsmiljön gör tunneltjänsten det möjligt att tilldela roller till betrodda communitymedlemmar som är registrerade i Publish-miljön. Tunneltjänsten ger även åtkomst till communitymedlemmar från konsolerna [Medlemmar och Grupper](members.md) i författarmiljön.

Konventionen innebär att medlemmar och medlemsgrupper som skapats i Publish-miljön *inte* återskapas i författarmiljön. Mer information finns i [Hantera användare och användargrupper](users.md).

Mer information om hur du aktiverar tunneltjänsten för en **författare**-instans finns i [Tunneltjänsten](deploy-communities.md#tunnel-service-on-author).

## Rollen Community Administrator {#community-administrator-role}

Medlemmar i gruppen Community Administrators kan skapa communitysajter, hantera webbplatser, hantera medlemmar (de kan förbjuda medlemmar från communityn) och moderera innehåll.

### Skapa användare {#create-user}

Skapa en användare på *författare*, som har tilldelats rollen som Community Administrator:

* På författarinstansen

   * Exempel: [http://localhost:4502/](http://localhost:4503/)

* Logga in med administratörsbehörighet

   * Till exempel användarnamn &#39;admin&#39; / lösenord &#39;admin&#39;

* Gå till **[!UICONTROL Tools]** > **[!UICONTROL Operations]** > **[!UICONTROL Security]** > **[!UICONTROL Users]** från huvudkonsolen.
* Välj **[!UICONTROL Add User]** på menyn **Redigera**

* I dialogrutan `Create New User` anger du:

   * **[!UICONTROL ID]**: sirius
   * **[!UICONTROL Email Address]**: sirius.nilson@mailinator.com
   * **[!UICONTROL Password]**: lösenord
   * **[!UICONTROL Confirm Password&ast;]**: lösenord
   * **[!UICONTROL First Name]**: Sirius
   * **[!UICONTROL Last Name]**: Nilson

### Tilldela Sirius till gruppen Community-administratörer {#assign-sirius-to-community-administrators-group}

Bläddra ned till `Add User to Groups`:

* Ange &quot;C&quot; för att söka

   * Välj `Community Administrators`
   * Välj `Community Enablement Managers`

* Välj **[!UICONTROL Save]**.

![create-user](assets/create-user.png)

## Aktivera social inloggning {#enable-social-login}

Innan demonstrationsversionerna av inloggningen via Facebook och Twitter kan användas måste

1. Installera ett korrigeringspaket eller [det senaste funktionspaketet](deploy-communities.md#latestfeaturepack) (för ändringar i Facebook-API:t från mars 2017).
1. [Aktivera OAuth-providern](social-login.md#adobe-granite-oauth-authentication-handler) i publiceringsmiljön.

För produktionsservrar är det nödvändigt att skapa de molntjänster som krävs för att tillhandahålla social inloggning.

Se [Social inloggning med Facebook och Twitter](social-login.md).

## Skapa självstudietaggar {#create-tutorial-tags}

Skapa taggar så att du kan använda dem för självstudiekurserna för engagemang med hjälp av taggnamnområdet för `Tutorial`.

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
1. [Publish taggarna](../../help/sites-administering/tags.md#publishing-tags).

Exempelpaket med taggar som skapats för Tutorials AEM Communities Getting Started

[Hämta fil](assets/tutorial_tags-v63.zip)

## MongoDB för UGC Common Store {#mongodb-for-ugc-common-store}

Vi rekommenderar, men är valfria, att du anger [MSRP](msrp.md) (MongoDB) som [gemensam lagringsplats](working-with-srp.md) för att få flexibiliteten att moderera all UGC från publicerings- och/eller författarmiljöer.

Instruktioner finns på [Konfigurera MongoDB för demo](demo-mongo.md).

Installationen av författaren och publiceringsinstanserna AEM som standard resulterar i att användargenererat innehåll (UGC) lagras i [JCR-tjärlagring](../../help/sites-deploying/platform.md) som nås med [JSRP](jsrp.md). JSRP är inte en vanlig lagringsplats, vilket innebär att UGC bara visas på den instans där den angavs. Vanligtvis anges UGC i en publiceringsinstans och skulle inte vara synligt i redigeringsmiljön, vilket resulterar i att alla modereringsåtgärder måste använda publiceringsinstansen.
