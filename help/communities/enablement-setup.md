---
title: Inledande inställning för aktivering
seo-title: Initial Setup
description: Inledande inställning för aktivering
seo-description: Initial Setup for Enablement
uuid: 873ec41d-c088-41d9-a535-de5300661de6
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: introduction
content-type: reference
discoiquuid: f2ac3d66-cc79-498f-83fb-dd96feb88de2
exl-id: ed494922-3e15-4778-84c1-35c8846ce980
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '851'
ht-degree: 0%

---

# Inledande inställning för aktivering  {#initial-setup-for-enablement}

## Starta författare- och publiceringsinstanser {#start-author-and-publish-instances}

I utvecklings- och demonstrationssyfte måste du köra en författare och en publiceringsinstans.

Följ de grundläggande AEM [Komma igång](../../help/sites-deploying/deploy.md#getting-started) instruktioner som resulterar i

* Redigeringsmiljö på [localhost:4502](http://localhost:4502/)
* Publiceringsmiljö på [localhost:4503](http://localhost:4503/)

För AEM Communities

* Författarmiljön är till för:

   * Utveckling av webbplatser, mallar, komponenter, hjälpmedel och utbildningsvägar.
   * Tilldelning av medlemmar och grupper av medlemmar för att aktivera resurser och utbildningsvägar.
   * Generera rapporter om uppdrag, vyer och inlägg.
   * Administrations- och konfigureringsuppgifter.

* Publiceringsmiljön är avsedd för:

   * Utbildning baserad på ämnen som hanteras av Enablement Manager.
   * Kommenterings- och klassificeringsresurser och utbildningsvägar.
   * Få kontakt med resurskontakterna.

>[!NOTE]
>
>Om du inte känner till AEM kan du läsa dokumentationen om [grundläggande hantering](../../help/sites-authoring/basic-handling.md) och [snabbguide till framtagning av sidor](../../help/sites-authoring/qg-page-authoring.md).

## Installera senaste versionen av Communities {#install-latest-communities-release}

Den här självstudiekursen skapar en [communitywebbplats för aktivering](overview.md#enablement-community). Se till att det senaste funktionspaketet är installerat på:

* [Senaste releaser](deploy-communities.md#latest-releases)

För en självstudiekurs som skapar en [community för engagemang](overview.md#engagement-community), besök [Komma igång med AEM Communities](getting-started.md).

## Konfigurera aktiveringsfunktioner {#configure-enablement-features}

Om du vill följa den här självstudiekursen måste du installera och [konfigurera aktivering](enablement.md), som kräver produkter från tredje part, som MySQL och FFmpeg.

## Konfigurera analys {#configure-analytics}

När [Adobe Analytics är konfigurerat för communitywebbplatsen](analytics.md)finns mer information i [rapporter](reports.md) genereras på aktiveringsresurser och utbildningsvägar som tilldelats communitymedlemmar (studerande).

## Konfigurera e-post för meddelanden {#configure-email-for-notifications}

Meddelandefunktionen, som är tillgänglig som standard för alla webbplatser som skapas med `Communities Sites` konsol, innehåller en e-postkanal för meddelanden.

Det som är nödvändigt är att e-post konfigureras korrekt för webbplatsen.

Se [Konfigurerar e-post](email.md).

## Aktivera tunneltjänsten {#enable-the-tunnel-service}

När du skapar en community i författarmiljön gör tunneltjänsten det möjligt att skapa och hantera användare och användargrupper som är registrerade i publiceringsmiljön (medlemmar), tilldela roller till betrodda communitymedlemmar och tilldela innehåll till studerande.

Mer information finns i [Hantera användare och användargrupper](users.md).

Mer information om hur du aktiverar tunneltjänsten finns i [Tunneltjänst](deploy-communities.md#tunnel-service-on-author).

## Skapa självstudietaggar {#create-tutorial-tags}

Skapa taggar som du kan använda för interaktions- och aktiveringssjälvstudiekurserna med hjälp av taggnamnutrymmet för `Tutorial`.

Använd [Taggningskonsol](../../help/sites-administering/tags.md#tagging-console) för att skapa följande taggar:

* `Tutorial: Sports / Baseball`
* `Tutorial: Sports / Gymnastics`
* `Tutorial: Sports / Skiing`
* `Tutorial: Arts / Visual`
* `Tutorial: Arts / Auditory`
* `Tutorial: Arts / History`

![självstudiekurstaggar](assets/tutorial-tags.png)

Följ sedan instruktionerna för att:

1. [Ange taggbehörigheter](../../help/sites-administering/tags.md#setting-tag-permissions)
1. [Publicera taggarna](../../help/sites-administering/tags.md#publishing-tags)

Exempelpaket med taggar som skapats för Tutorials AEM Communities Getting Started

[Hämta fil](assets/communities_tutorialtags-10.zip)

## Skapa aktiveringsmedlemmar och grupper {#create-enablement-members-and-groups}

För en aktiveringscommunitywebbplats bör webbplatsbesökare inte kunna [självregistrering eller använd social inloggning](sites-console.md#user-management).

I stället med [tunneltjänst](#enable-the-tunnel-service) aktiverad, [Medlemskonsol](members.md) används för att registrera nya medlemmar i publiceringsmiljön.

I den här självstudiekursen skapas tre medlemmar i publiceringsmiljön. Två medlemmar blir medlemmar i en användargrupp som är tilldelad en utbildningsväg, medan den tredje medlemmen blir en aktiveringsresurskontakt.

En fjärde användare skapas i författarmiljön och tilldelas rollerna Webbgruppsadministratör och Webbgruppshanterare.

>[!NOTE]
>
>Dessa medlemmar skapas innan *Självstudiekurs om aktivering* communitysajt.
>
>Om de skapades efteråt kan de läggas till som medlemmar i *Grupp med medlemmar i självstudiekursen om aktivering* när medlemmar skapas.
>
>I stället blir de [som tilldelats medlemsgruppen](enablement-create-site.md#assignuserstocommunityenablemembersgroup).

### Riley Taylor - anmälare {#riley-taylor-enrollee}

[Skapa en medlem](members.md#create-new-member) som ska läggas till i en grupp med elev - gruppen Community Ski Class.

* **ID**: riley
* **E-post**: riley.taylor@mailinator.com
* **Lösenord**: lösenord
* **Bekräfta lösenord**: lösenord
* **Förnamn**: Riley
* **Efternamn**: Taylor

### Sidney Croft - Uppgiftslämnare {#sidney-croft-enrollee}

[Skapa en andra medlem](members.md#create-new-member) som läggs till i gruppen Community Ski Class.

* **ID**: sidney
* **E-post**: sidney.croft@mailinator.com
* **Lösenord**: lösenord
* **Bekräfta lösenord**: lösenord
* **Förnamn**: Sidney
* **Efternamn**: Beskär

### Quinn Harper - Aktivera resurskontakt och moderator {#quinn-harper-enablement-resource-contact-and-moderator}

[Skapa en medlem](members.md#create-new-member) som läggs till i communityplatsens medlemsgrupp när webbplatsen har skapats. Det här medlemskapet tillåter att medlemmen tilldelas som aktivering [Resurskontakt](resources.md#settings) när en aktiveringsresurs skapas för platsen.

* **ID**: quinn
* **E-post**: quinn.harper@mailinator.com
* **Lösenord**: lösenord
* **Bekräfta lösenord**: lösenord
* **Förnamn**: Quinn
* **Efternamn**: Harper

### Lägg till en användargrupp - Community Ski-klass {#add-a-user-group-community-ski-class}

[Lägg till en ny grupp](members.md#create-new-group) med namnet Community Ski Class.

* **ID**: community-ski-class
* **Namn**: Klassen Community Ski
* **Beskrivning**: en exempelgrupp för tilldelning av aktiveringsresurser
* **Lägg till medlemmar i grupp** &#39;add&#39;:

   * riley
   * sidney

* Välj **[!UICONTROL Save]**

### Egenskaper för Community-skalklassen {#community-ski-class-properties}

![ski-class-properties](assets/ski-class-properties.png)

>[!NOTE]
>
>När en community-webbplats skapas kan befintliga medlemmar och grupper läggas till i communityplatsens medlemsgrupp.

## Rollen Community Administrator {#community-administrator-role}

Medlemmar i gruppen Community Administrators kan skapa communitysajter, hantera webbplatser, hantera medlemmar (de kan förbjuda medlemmar från communityn) och moderera innehåll.

### Skapa användare {#create-user}

Skapa en användare på *författare*, som har tilldelats rollen som gemenskapsadministratör:

* På författarinstansen

   * Till exempel: [http://localhost:4502/](http://localhost:4503/)

* Logga in med administratörsbehörighet

   * Till exempel användarnamn &#39;admin&#39; / lösenord &#39;admin&#39;

* Navigera från huvudkonsolen till **[!UICONTROL Tools]** > **[!UICONTROL Operations]** > **[!UICONTROL Security]** > **[!UICONTROL Users]**.
* Från **[!UICONTROL Edit]** meny, välja **[!UICONTROL Add User]**.

* I `Create New User` dialogruta:

   * **ID&amp;ast;**: sirius
   * **E-postadress**: sirius.nilson@mailinator.com
   * **Lösenord&amp;ast;**: lösenord
   * **Bekräfta lösenord&amp;ast;**: lösenord
   * **Förnamn**: Sirius
   * **&amp;Efternamn;**: Nilson

### Tilldela Sirius till gruppen Community-administratörer {#assign-sirius-to-community-administrators-group}

Bläddra nedåt till `Add User to Groups`:

* Ange &quot;C&quot; för att söka

   * Välj `Community Administrators`
   * Välj `Community Enablement Managers`

* Välj **[!UICONTROL Save]**

![admin-role](assets/admin-role.png)
