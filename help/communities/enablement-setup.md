---
title: Inledande inställning för aktivering
seo-title: Inledande konfiguration
description: Inledande inställning för aktivering
seo-description: Inledande inställning för aktivering
uuid: 873ec41d-c088-41d9-a535-de5300661de6
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: introduction
content-type: reference
discoiquuid: f2ac3d66-cc79-498f-83fb-dd96feb88de2
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '857'
ht-degree: 0%

---


# Inledande inställning för aktivering {#initial-setup-for-enablement}

## Starta författare och publiceringsinstanser {#start-author-and-publish-instances}

I utvecklings- och demonstrationssyfte måste du köra en författare och en publiceringsinstans.

Följ de grundläggande AEM [Komma igång](../../help/sites-deploying/deploy.md#getting-started)-instruktionerna som kommer att resultera i

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
>Om du inte känner till AEM kan du läsa dokumentationen om [grundläggande hantering](../../help/sites-authoring/basic-handling.md) och en [snabbguide till redigeringssidor](../../help/sites-authoring/qg-page-authoring.md).

## Installera den senaste versionen av Communities {#install-latest-communities-release}

I den här självstudien skapas en [community-webbplats för aktivering](overview.md#enablement-community). Se till att det senaste funktionspaketet är installerat på:

* [Senaste releaser](deploy-communities.md#latest-releases)

En självstudiekurs som skapar en [community-webbplats för engagemang](overview.md#engagement-community) finns på [Komma igång med AEM Communities](getting-started.md).

## Konfigurera aktiveringsfunktioner {#configure-enablement-features}

Om du vill följa den här självstudiekursen måste du installera och [konfigurera aktivering](enablement.md), vilket kräver produkter från tredje part, som MySQL och FFmpeg.

## Konfigurera analys {#configure-analytics}

När [Adobe Analytics har konfigurerats för communitywebbplatsen](analytics.md) finns mer information i [rapporterna](reports.md) som genererats för aktiveringsresurser och utbildningsvägar som tilldelats communitymedlemmar (studerande).

## Konfigurera e-post för meddelanden {#configure-email-for-notifications}

Meddelandefunktionen, som är tillgänglig som standard för alla webbplatser som skapats med `Communities Sites`-konsolen, erbjuder en e-postkanal för meddelanden.

Det som är nödvändigt är att e-post konfigureras korrekt för webbplatsen.

Se [Konfigurera e-post](email.md).

## Aktivera tunneltjänsten {#enable-the-tunnel-service}

När du skapar en community i författarmiljön gör tunneltjänsten det möjligt att skapa och hantera användare och användargrupper som är registrerade i publiceringsmiljön (medlemmar), tilldela roller till betrodda communitymedlemmar och tilldela innehåll till studerande.

Mer information finns i [Hantera användare och användargrupper](users.md).

Mer information om hur du aktiverar tunneltjänsten finns i [Tunneltjänsten](deploy-communities.md#tunnel-service-on-author).

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

1. [Ange taggbehörigheter](../../help/sites-administering/tags.md#setting-tag-permissions)
1. [Publicera taggarna](../../help/sites-administering/tags.md#publishing-tags)

Exempelpaket med taggar som skapats för Tutorials AEM Communities Getting Started

[Hämta fil](assets/communities_tutorialtags-10.zip)

## Skapa aktiveringsmedlemmar och grupper {#create-enablement-members-and-groups}

För en aktiveringscommunitywebbplats bör webbplatsbesökare inte kunna [självregistrera eller använda social inloggning](sites-console.md#user-management).

När [tunneltjänsten](#enable-the-tunnel-service) är aktiverad används i stället [medlemskonsolen](members.md) för att registrera nya medlemmar i publiceringsmiljön.

I den här självstudiekursen skapas tre medlemmar i publiceringsmiljön. Två medlemmar blir medlemmar i en användargrupp som är tilldelad en utbildningsväg, medan den tredje medlemmen blir en aktiveringsresurskontakt.

En fjärde användare skapas i författarmiljön och tilldelas rollerna Webbgruppsadministratör och Webbgruppshanterare.

>[!NOTE]
>
>Dessa medlemmar skapas innan *självstudiekursen* för aktivering skapas.
>
>Om de skapades efteråt kan de läggas till som medlemmar i gruppen *Deltagare i självstudiekursen* när medlemmar skapas.
>
>I stället tilldelas de [till medlemsgruppen](enablement-create-site.md#assignuserstocommunityenablemembersgroup).

### Riley Taylor - registrerare {#riley-taylor-enrollee}

[Skapa ett ](members.md#create-new-member) medlemskap som ska läggas till i en grupp med elev - Community Ski Class-gruppen.

* **ID**: riley
* **E-post**: riley.taylor@mailinator.com
* **Lösenord**: lösenord
* **Bekräfta lösenord**: lösenord
* **Förnamn**: Riley
* **Efternamn**: Taylor

### Sidney Croft - registrerare {#sidney-croft-enrollee}

[Skapa ett andra ](members.md#create-new-member) medlemskap som ska läggas till i gruppen Community Ski Class.

* **ID**: sidney
* **E-post**: sidney.croft@mailinator.com
* **Lösenord**: lösenord
* **Bekräfta lösenord**: lösenord
* **Förnamn**: Sidney
* **Efternamn**: Beskär

### Quinn Harper - Aktivera resurskontakt och moderator {#quinn-harper-enablement-resource-contact-and-moderator}

[Skapa ett ](members.md#create-new-member) medlemskap som läggs till i medlemsgruppen för communityn när webbplatsen har skapats. Medlemskapet tillåter att medlemmen tilldelas som aktivering [Resurskontakt](resources.md#settings) när en aktiveringsresurs skapas för platsen.

* **ID**: quinn
* **E-post**: quinn.harper@mailinator.com
* **Lösenord**: lösenord
* **Bekräfta lösenord**: lösenord
* **Förnamn**: Quinn
* **Efternamn**: Harper

### Lägg till en användargrupp - Community Ski-klass {#add-a-user-group-community-ski-class}

[Lägg till en ny ](members.md#create-new-group) grupp med namnet Community Ski Class.

* **ID**: community-ski-class
* **Namn**: Klassen Community Ski
* **Beskrivning**: en exempelgrupp för tilldelning av aktiveringsresurser
* **Lägg till medlemmar i gruppen** &quot;add&quot;:

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

Skapa en användare på *författare*, som tilldelas rollen Community Administrator:

* På författarinstansen

   * Till exempel [http://localhost:4502/](http://localhost:4503/)

* Logga in med administratörsbehörighet

   * Till exempel användarnamn &#39;admin&#39; / lösenord &#39;admin&#39;

* Gå till **[!UICONTROL Tools]** > **[!UICONTROL Operations]** > **[!UICONTROL Security]** > **[!UICONTROL Users]** från huvudkonsolen.
* Välj **[!UICONTROL Add User]** på menyn **[!UICONTROL Edit]**.

* I dialogrutan `Create New User` anger du:

   * **&amp;ID:t;**: sirius
   * **E-postadress**: sirius.nilson@mailinator.com
   * **&amp;Lösenord;**: lösenord
   * **Bekräfta lösenord&amp;ast;**: lösenord
   * **Förnamn**: Sirius
   * **&amp;Efternamn;**: Nilson

### Tilldela Sirius till communityadministratörsgruppen {#assign-sirius-to-community-administrators-group}

Bläddra ned till `Add User to Groups`:

* Ange &quot;C&quot; för att söka

   * Välj `Community Administrators`
   * Välj `Community Enablement Managers`

* Välj **[!UICONTROL Save]**

![admin-role](assets/admin-role.png)

