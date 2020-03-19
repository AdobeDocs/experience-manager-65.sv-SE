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
source-git-commit: d6c8bbb9aa763a2eb6660b6b6755aba75241e394

---


# Inledande inställning för aktivering {#initial-setup-for-enablement}

## Starta författare- och publiceringsinstanser {#start-author-and-publish-instances}

I utvecklings- och demonstrationssyfte måste du köra en författare och en publiceringsinstans.

Följ de grundläggande [anvisningarna i AEM Getting Started](../../help/sites-deploying/deploy.md#getting-started) som ger

* Redigeringsmiljö på [localhost:4502](http://localhost:4502/)
* Publiceringsmiljö på [localhost:4503](http://localhost:4503/)

För AEM Communities,

* Författarmiljön är till för

   * Utveckling av webbplatser, mallar, komponenter, hjälpmedel och utbildningsvägar
   * Tilldelning av medlemmar och grupper av medlemmar för att aktivera resurser och utbildningsvägar
   * Generera rapporter om uppdrag, vyer och inlägg
   * Administrations- och konfigureringsuppgifter

* Publiceringsmiljön är avsedd för

   * Utbildning baserad på ämnen som hanteras av Enablement Manager
   * Kommentarer och omdömen om aktiveringsresurser och utbildningsvägar
   * Komma i kontakt med resurskontakterna

>[!NOTE]
>
>Om du inte känner till AEM läser du dokumentationen om [grundläggande hantering](../../help/sites-authoring/basic-handling.md) och en [snabbguide till redigeringssidorna](../../help/sites-authoring/qg-page-authoring.md).

## Installera senaste versionen av Communities {#install-latest-communities-release}

Den här självstudiekursen skapar en [aktiveringscommunitywebbplats](overview.md#enablement-community). Se till att det senaste funktionspaketet är installerat på:

* [Senaste releaser](deploy-communities.md#latest-releases)

En självstudiekurs som skapar en [engagemangscommunity](overview.md#engagement-community)finns på [Komma igång med AEM Communities](getting-started.md).

## Konfigurera aktiveringsfunktioner {#configure-enablement-features}

Om du vill följa den här självstudiekursen måste du installera och [konfigurera aktivering](enablement.md)korrekt, vilket kräver produkter från tredje part, som MySQL och FFmpeg.

## Konfigurera analys {#configure-analytics}

När [Adobe Analytics har konfigurerats för communitywebbplatsen](analytics.md)finns mer information i [rapporterna](reports.md) som genereras om aktiveringsresurser och utbildningsvägar som tilldelats communitymedlemmar (studerande).

## Konfigurera e-post för meddelanden {#configure-email-for-notifications}

Meddelandefunktionen, som är tillgänglig som standard för alla webbplatser som skapas med `Communities Sites` konsolen, erbjuder en e-postkanal för meddelanden.

Det som är nödvändigt är att e-post konfigureras korrekt för webbplatsen.

Se [Konfigurera e-post](email.md).

## Aktivera tunneltjänsten {#enable-the-tunnel-service}

När du skapar en community i författarmiljön gör tunneltjänsten det möjligt att skapa och hantera användare och användargrupper som är registrerade i publiceringsmiljön (medlemmar), tilldela roller till betrodda communitymedlemmar och tilldela innehåll till studerande.

Mer information finns i [Hantera användare och användargrupper](users.md).

Mer information om hur du aktiverar tunneltjänsten finns i [Tunneltjänsten](deploy-communities.md#tunnel-service-on-author).

## Skapa självstudietaggar {#create-tutorial-tags}

Skapa taggar som du kan använda för interaktions- och aktiveringssjälvstudiekurserna med hjälp av taggnamnutrymmet för `Tutorial`.

Använd [taggningskonsolen](../../help/sites-administering/tags.md#tagging-console) för att skapa följande taggar:

* `Tutorial: Sports / Baseball`
* `Tutorial: Sports / Gymnastics`
* `Tutorial: Sports / Skiing`
* `Tutorial: Arts / Visual`
* `Tutorial: Arts / Auditory`
* `Tutorial: Arts / History`

![chlimage_1-417](assets/chlimage_1-417.png)

Följ sedan instruktionerna för att

1. [Ange taggbehörigheter](../../help/sites-administering/tags.md#setting-tag-permissions)
1. [Publicera taggarna](../../help/sites-administering/tags.md#publishing-tags)

Exempelpaket med taggar som skapats för självstudiekurserna Komma igång för AEM Communities

[Hämta fil](assets/communities_tutorialtags-10.zip)

## Skapa aktiveringsmedlemmar och grupper {#create-enablement-members-and-groups}

För en aktiveringscommunitywebbplats bör besökare inte kunna [självregistrera sig eller använda social inloggning](sites-console.md#user-management).

När [tunneltjänsten](#enable-the-tunnel-service) är aktiverad används i stället [medlemskonsolen](members.md) för att registrera nya medlemmar i publiceringsmiljön.

I den här självstudiekursen skapas tre medlemmar i publiceringsmiljön. Två medlemmar blir medlemmar i en användargrupp som är tilldelad en utbildningsväg, medan den tredje medlemmen blir en aktiveringsresurskontakt.

En fjärde användare skapas i författarmiljön och tilldelas rollerna Webbgruppsadministratör och Aktivitetshanteraren i användarforumet.

>[!NOTE]
>
>Dessa medlemmar skapas innan communitywebbplatsen för *självstudiekurser* för aktivering skapas.
>
>Om de skapades efteråt kan de läggas till som medlemmar i gruppen *med medlemmar i* självstudiekursen för aktivering när medlemmar skapas.
>
>I stället [tilldelas de medlemsgruppen](enablement-create-site.md#assignuserstocommunityenablemembersgroup)senare.

### Riley Taylor - anmälare {#riley-taylor-enrollee}

[Skapa en medlem](members.md#create-new-member) som ska läggas till i en grupp med elev - Community Ski Class-gruppen.

* **ID**: riley
* **E-post**: riley.taylor@mailinator.com
* **Lösenord**: lösenord
* **Bekräfta lösenord**: lösenord
* **Förnamn**: Riley
* **Efternamn**: Taylor

### Sidney Croft - Uppgiftslämnare {#sidney-croft-enrollee}

[Skapa en andra medlem](members.md#create-new-member) som ska läggas till i gruppen Community Ski Class.

* **ID**: sidney
* **E-post**: sidney.croft@mailinator.com
* **Lösenord**: lösenord
* **Bekräfta lösenord**: lösenord
* **Förnamn**: Sidney
* **Efternamn**: Beskär

### Quinn Harper - Aktivera resurskontakt och moderator {#quinn-harper-enablement-resource-contact-and-moderator}

[Skapa en medlem](members.md#create-new-member) som ska läggas till i medlemsgruppen för communityn när webbplatsen har skapats. Det här medlemskapet tillåter att medlemmen tilldelas som [aktiveringsresurskontakt](resources.md#settings) när en aktiveringsresurs skapas för platsen.

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
* **Lägg till medlemmar i gruppen** &#39;add&#39;:

   * riley
   * sidney

* Välj **[!UICONTROL Spara]**

### Egenskaper för Community-skalklassen {#community-ski-class-properties}

![chlimage_1-418](assets/chlimage_1-418.png)

>[!NOTE]
>
>När en community-webbplats skapas kan befintliga medlemmar och grupper läggas till i communityplatsens medlemsgrupp.

## Rollen Community Administrator {#community-administrator-role}

Medlemmar i gruppen Community Administrators kan skapa communitysajter, hantera webbplatser, hantera medlemmar (de kan förbjuda medlemmar från communityn) och moderera innehåll.

### Skapa användare {#create-user}

Skapa en användare på *författaren* som får rollen som Community Administrator:

* På författarinstansen

   * Till exempel [http://localhost:4502/](http://localhost:4503/)

* Logga in med administratörsbehörighet

   * Till exempel användarnamn &#39;admin&#39; / lösenord &#39;admin&#39;

* Navigera från huvudkonsolen till **[!UICONTROL Verktyg, Åtgärder > Säkerhet > Användare]**
* Välj **[!UICONTROL Lägg till användare på menyn]** Redigera ****

* In the `Create New User` dialog enter

   * **ID&amp;ast;**: sirius
   * **E-postadress**: sirius.nilson@mailinator.com
   * **Lösenords&amp;stämpel;ast;**: lösenord
   * **Bekräfta lösenord&amp;stämpel;ast;**: lösenord
   * **Förnamn**: Sirius
   * **Efternamn&amp;stämpel;ast;**: Nilson

### Tilldela Sirius till gruppen Community-administratörer {#assign-sirius-to-community-administrators-group}

Bläddra ned till `Add User to Groups`:

* Ange &quot;C&quot; för att söka

   * Välj `Community Administrators`
   * Välj `Community Enablement Managers`

* Välj **[!UICONTROL Spara]**

![chlimage_1-419](assets/chlimage_1-419.png)

