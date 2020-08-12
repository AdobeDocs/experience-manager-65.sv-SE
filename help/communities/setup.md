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
source-git-commit: 6ab91667ad668abf80ccf1710966169b3a187928
workflow-type: tm+mt
source-wordcount: '678'
ht-degree: 0%

---


# Inledande konfiguration {#initial-setup}

## Starta författare- och publiceringsinstanser {#start-author-and-publish-instances}

I utvecklings- och demonstrationssyfte måste du köra en författare och en publiceringsinstans.

Gör detta genom att följa de grundläggande AEM [Komma igång](../../help/sites-deploying/deploy.md#getting-started) -instruktionerna, som ger följande resultat:

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
>Om du inte känner till AEM kan du läsa dokumentationen om [grundläggande hantering](../../help/sites-authoring/basic-handling.md) och en [snabbguide till hur du skapar sidor](../../help/sites-authoring/qg-page-authoring.md).


## Installera senaste versionen av Communities {#install-latest-communities-release}

Den här självstudiekursen skapar en [engagemangscommunitywebbplats](overview.md#engagement-community) och baseras på AEM Communities 6.2 feature pack version 1.10.

Se till att det senaste funktionspaketet är installerat på:

* [Senaste releaser](deploy-communities.md#latest-releases)

En självstudiekurs om hur du skapar en [aktiveringscommunitywebbplats](overview.md#enablement-community)finns på [Komma igång med AEM Communities för aktivering](getting-started-enablement.md).

## Konfigurera analys {#configure-analytics}

När [Adobe Analytics har konfigurerats för communitywebbplatsen](analytics.md)finns det information om communityaktiviteter som förbättrar communitymedlemmens upplevelse samt ger feedback till administratörer av webbplatsen.

Integrering med Adobe Analytics är valfritt.

## Konfigurera e-post för meddelanden {#configure-email-for-notifications}

Meddelandefunktionen, som är tillgänglig som standard för alla webbplatser som skapas med `Communities Sites` konsolen, erbjuder en e-postkanal för meddelanden.

Det som är nödvändigt är att e-post konfigureras korrekt för webbplatsen.

Se [Konfigurera e-post](email.md).

## Aktivera tunneltjänsten {#enable-the-tunnel-service}

När du skapar en community-webbplats i författarmiljön gör tunneltjänsten det möjligt att tilldela roller till betrodda communitymedlemmar som är registrerade i publiceringsmiljön. Tunneltjänsten ger även åtkomst till communitymedlemmar från konsolerna [Medlemmar och Grupper](members.md) i författarmiljön.

Konventionen är avsedd för medlemmar och medlemsgrupper som skapats i publiceringsmiljön och som *inte* kan återskapas i författarmiljön. Mer information finns i [Hantera användare och användargrupper](users.md).

Mer information om hur du aktiverar tunneltjänsten på en **författarinstans** finns i [Tunneltjänsten](deploy-communities.md#tunnel-service-on-author).

## Rollen Community Administrator {#community-administrator-role}

Medlemmar i gruppen Community Administrators kan skapa communitysajter, hantera webbplatser, hantera medlemmar (de kan förbjuda medlemmar från communityn) och moderera innehåll.

### Skapa användare {#create-user}

Skapa en användare på *författaren* som får rollen som Community Administrator:

* På författarinstansen

   * Till exempel [http://localhost:4502/](http://localhost:4503/)

* Logga in med administratörsbehörighet

   * Till exempel användarnamn &#39;admin&#39; / lösenord &#39;admin&#39;

* Navigera från huvudkonsolen till **[!UICONTROL Tools]** > **[!UICONTROL Operations]** > **[!UICONTROL Security]** > **[!UICONTROL Users]**.
* På menyn **Redigera **väljer du **[!UICONTROL Add User]**

* In the `Create New User` dialog enter:

   * **[!UICONTROL ID]**: sirius
   * **[!UICONTROL Emai Address]**: sirius.nilson@mailinator.com
   * **[!UICONTROL Password]**: password
   * **[!UICONTROL Confirm Password&ast;]**: password
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

Innan demonstrationsversionerna av social inloggning med Facebook och Twitter kan användas är det nödvändigt att

1. Installera ett korrigeringspaket eller [det senaste funktionspaketet](deploy-communities.md#latestfeaturepack) (för ändringar i Facebook-API:t från mars 2017).
1. [Aktivera OAuth-providern](social-login.md#adobe-granite-oauth-authentication-handler) i publiceringsmiljön.

För produktionsservrar är det nödvändigt att skapa de molntjänster som krävs för att tillhandahålla social inloggning.

Se [Social Login med Facebook och Twitter](social-login.md).

## Skapa självstudietaggar {#create-tutorial-tags}

Skapa taggar som du kan använda för interaktions- och aktiveringssjälvstudiekurserna med hjälp av taggnamnutrymmet för `Tutorial`.

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

Vi rekommenderar, men är valfria, att du ställer in [MSRP](msrp.md) (MongoDB) som [gemensam lagringsplats](working-with-srp.md) för att kunna hantera all UGC från publicerings- och/eller författarmiljöer på ett flexibelt sätt.

Instruktioner finns i [Konfigurera MongoDB för demo](demo-mongo.md).

Om du installerar författaren och publicerar AEM kommer användargenererat innehåll (UGC) att lagras i [JCR-tjärlagring](../../help/sites-deploying/platform.md) som nås med [JSRP](jsrp.md). JSRP är inte en vanlig lagringsplats, vilket innebär att UGC bara visas på den instans där den angavs. Vanligtvis anges UGC i en publiceringsinstans och skulle inte vara synligt i redigeringsmiljön, vilket resulterar i att alla modereringsåtgärder måste använda publiceringsinstansen.