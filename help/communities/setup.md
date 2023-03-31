---
title: Inledande konfiguration
seo-title: Initial Setup
description: Konfigurera communities
seo-description: Setting up Communities
uuid: c53d280c-c5ae-47cf-8038-f0dea68e15ff
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: introduction
content-type: reference
discoiquuid: 0d462ad1-5619-4bb6-9609-bc8987c40a0c
exl-id: 6bda0f09-7ae5-4540-b035-9dd249ac3186
source-git-commit: 942db8fe3dad16be53dc6abe0e519d97a659e480
workflow-type: tm+mt
source-wordcount: '654'
ht-degree: 0%

---

# Inledande konfiguration {#initial-setup}

## Starta författare- och publiceringsinstanser {#start-author-and-publish-instances}

I utvecklings- och demonstrationssyfte måste du köra en författare och en publiceringsinstans.

Följ de grundläggande AEM [Komma igång](../../help/sites-deploying/deploy.md#getting-started) instruktioner, som ger

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
>Om du inte känner till AEM kan du läsa dokumentationen om [grundläggande hantering](../../help/sites-authoring/basic-handling.md) och [snabbguide till framtagning av sidor](../../help/sites-authoring/qg-page-authoring.md).

## Installera senaste versionen av Communities {#install-latest-communities-release}

Den här självstudiekursen skapar en [community för engagemang](overview.md#engagement-community) och bygger på AEM Communities 6.2 feature pack version 1.10.

Se till att det senaste funktionspaketet är installerat på:

* [Senaste releaser](deploy-communities.md#latest-releases)

## Konfigurera analys {#configure-analytics}

När [Adobe Analytics är konfigurerat för communitywebbplatsen](analytics.md), finns det information om communityaktiviteter som förbättrar communitymedlemmens upplevelse och ger återkoppling till administratörer av webbplatsen.

Integrering med Adobe Analytics är valfritt.

## Konfigurera e-post för meddelanden {#configure-email-for-notifications}

Meddelandefunktionen, som är tillgänglig som standard för alla webbplatser som skapas med `Communities Sites` konsol, innehåller en e-postkanal för meddelanden.

Det som är nödvändigt är att e-post konfigureras korrekt för webbplatsen.

Se [Konfigurerar e-post](email.md).

## Aktivera tunneltjänsten {#enable-the-tunnel-service}

När du skapar en community-webbplats i författarmiljön gör tunneltjänsten det möjligt att tilldela roller till betrodda communitymedlemmar som är registrerade i publiceringsmiljön. Tunneltjänsten ger även åtkomst till communitymedlemmar från [Konsoler för medlemmar och grupper](members.md) i redigeringsmiljön.

Konventionen riktar sig till medlemmar och medlemsgrupper som skapats i publiceringsmiljön för att *not* återskapas i redigeringsmiljön. Mer information finns i [Hantera användare och användargrupper](users.md).

För enkla instruktioner om hur du aktiverar tunneltjänsten på en **författare** -instans, se [Tunneltjänst](deploy-communities.md#tunnel-service-on-author).

## Rollen Community Administrator {#community-administrator-role}

Medlemmar i gruppen Community Administrators kan skapa communitysajter, hantera webbplatser, hantera medlemmar (de kan förbjuda medlemmar från communityn) och moderera innehåll.

### Skapa användare {#create-user}

Skapa en användare på *författare*, som har tilldelats rollen som gemenskapsadministratör:

* På författarinstansen

   * Till exempel: [http://localhost:4502/](http://localhost:4503/)

* Logga in med administratörsbehörighet

   * Till exempel användarnamn &#39;admin&#39; / lösenord &#39;admin&#39;

* Navigera från huvudkonsolen till **[!UICONTROL Tools]** > **[!UICONTROL Operations]** > **[!UICONTROL Security]** > **[!UICONTROL Users]**.
* Från **Redigera** meny, välja **[!UICONTROL Add User]**

* I `Create New User` dialogruta:

   * **[!UICONTROL ID]**: sirius
   * **[!UICONTROL Emai Address]**: sirius.nilson@mailinator.com
   * **[!UICONTROL Password]**: lösenord
   * **[!UICONTROL Confirm Password&ast;]**: lösenord
   * **[!UICONTROL First Name]**: Sirius
   * **[!UICONTROL Last Name]**: Nilson

### Tilldela Sirius till gruppen Community-administratörer {#assign-sirius-to-community-administrators-group}

Bläddra nedåt till `Add User to Groups`:

* Ange &quot;C&quot; för att söka

   * Välj `Community Administrators`
   * Välj `Community Enablement Managers`

* Välj **[!UICONTROL Save]**.

![create-user](assets/create-user.png)

## Aktivera social inloggning {#enable-social-login}

Innan demonstrationsversionerna av inloggningen på sociala medier med Facebook och Twitter kan användas är det nödvändigt att

1. Installera ett korrigeringspaket eller [senaste funktionspaketet](deploy-communities.md#latestfeaturepack) (för ändringar av Facebook API i mars 2017).
1. [Aktivera OAuth-providern](social-login.md#adobe-granite-oauth-authentication-handler) i publiceringsmiljön.

För produktionsservrar är det nödvändigt att skapa de molntjänster som krävs för att tillhandahålla social inloggning.

Se [Social inloggning med Facebook och Twitter](social-login.md).

## Skapa självstudietaggar {#create-tutorial-tags}

Skapa taggar som ska användas för interaktionskurserna med hjälp av taggnamnutrymmet för `Tutorial`.

Använd [Taggningskonsol](../../help/sites-administering/tags.md#tagging-console) för att skapa följande taggar:

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

Vi rekommenderar att du ställer in [MSRP](msrp.md) (MongoDB) som [gemensam lagringsplats](working-with-srp.md) så att du kan hantera alla användargenererat innehåll från publicerings- och/eller författarmiljöer på ett flexibelt sätt.

Instruktioner finns på [Så här konfigurerar du MongoDB för demo](demo-mongo.md).

Som standard lagras användargenererat innehåll (UGC) när författaren installeras och AEM publiceras [JCR-tjärlagring](../../help/sites-deploying/platform.md) som används [JSRP](jsrp.md). JSRP är inte en vanlig lagringsplats, vilket innebär att UGC bara visas på den instans där den angavs. Vanligtvis anges UGC i en publiceringsinstans och skulle inte vara synligt i redigeringsmiljön, vilket resulterar i att alla modereringsåtgärder måste använda publiceringsinstansen.
