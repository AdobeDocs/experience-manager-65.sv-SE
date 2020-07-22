---
title: Community Groups Console
seo-title: Community Groups Console
description: Med gruppkonsolen kan du skapa communitygrupper
seo-description: Med gruppkonsolen kan du skapa communitygrupper
uuid: 21e2bde3-7354-4193-bcb3-c672c6342252
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: d381ea40-fe49-4d32-bfad-1379c7a02aba
docset: aem65
pagetitle: Community Groups Console
translation-type: tm+mt
source-git-commit: ee0d4aa07db6f00409cace8664d02c545e7d6550
workflow-type: tm+mt
source-wordcount: '1676'
ht-degree: 0%

---


# Community Groups Console {#community-groups-console}

Konsolen Grupper ger åtkomst till att skapa communitygrupper när en communityplats [mallstruktur](/help/communities/sites-console.md#step1) innehåller funktionen [](/help/communities/functions.md#groups-function)grupper.

* AEM Communities stöder kapsling av grupper inom andra grupper. Gruppinkapsling är möjligt när den nya gruppens [](/help/communities/tools-groups.md) struktur innehåller gruppfunktionen.
* Det finns bara en guide för att skapa grupper i författarmiljön som påminner om guiden Skapa webbplats.
* Oavsett om medlemmar kan skapa grupper i publiceringsmiljön eller inte kan de konfigureras när de lägger till en gruppfunktion i en community-webbplatsstruktur eller en community-gruppstruktur.

Av de tre gruppmallarna som ingår är det bara `Reference Group` mallen som innehåller en gruppfunktion i sin struktur.

De olika delarna av communitygrupper är:

* **Skapande**: ny grupp kan skapas för författaren och eventuellt för publiceringsinstansen.
* **Kontroll**: gruppen kan vara öppen eller hemlig.
* **Kapsling**: kan innehålla noll eller flera grupper.

<!-- This is a 404 on helpx. Please update or remove.
>[!NOTE]
>
>Community groups, created in the publish environment before the [existence of the Community Groups console](/help/communities/version-history.md#featurepack1fp1), will not be listed in the Community Groups console, and thus, are not modifiable using the console.-->

>[!NOTE]
>
>Den här gruppkonsolen, som bara är tillgänglig från webbgruppskonsolen, ska inte blandas ihop med [gruppmedlemskonsolen](/help/communities/members.md) för hantering av medlemsgrupper.
>
>Medlemsgrupper är användargrupper som är registrerade i publiceringsmiljön och som nås från författarmiljön med hjälp av [tunneltjänsten](/help/communities/deploy-communities.md#tunnel-service-on-author).


## Skapa grupp {#group-creation}

Så här kommer du åt gruppkonsolen:

* Logga in med administratörsbehörighet när du är författare.
* Från global navigering: **[!UICONTROL Communities]** > **[!UICONTROL Sites]**.
* Välj en befintlig community-webbplatsmapp för att öppna den.
* Välj en instans av en community-webbplats i mappen.

   * Strukturen på communitywebbplatsen måste innehålla en gruppfunktion.
   * Skärmbilderna kommer från självstudiekursen Komma igång när du har [skapat grupper vid publicering](/help/communities/published-site.md).

   ![create-group](assets/create-group.png)

* Öppna **gruppmappen** .

   När de öppnas visas alla befintliga grupper, oavsett om de har skapats vid författare eller publicering.

   Från den här gruppkonsolen går det att skapa nya grupper.

   ![create-new-group](assets/create-new-group.png)

* Klicka på knappen **Skapa grupp** .

### Steg 1: Community-gruppmall {#step-community-group-template}

![Flerspråkiga communitygrupper](assets/multi-lingual-group.png)

* **Gruppnamn**

   En visningsrubrik för gruppen.
Titeln visas på den publicerade webbplatsen för gruppen.

* **Beskrivning av communitygrupp**

   En beskrivning av gruppen.

* **Grupprot för community**

   Rotsökvägen till gruppen.
Standardroten är den överordnade platsen, men roten kan flyttas till valfri plats på webbplatsen. Vi rekommenderar inte att du ändrar den.

* **Menyn Ytterligare tillgängliga språk för** communitygrupper

   Använd listrutan för att välja tillgängliga språk i communitygruppen. Menyn innehåller alla språk som den överordnade communitywebbplatsen skapas i. Användarna kan välja mellan dessa språk för att skapa grupper i flera språkområden i det här steget. Samma grupp skapas på flera angivna språk i gruppkonsolen för respektive communityplats.

* **Gruppnamn för community**

   Namnet på gruppens rotsida som visas i URL:en.

   * Dubbelkontrollera namnet eftersom det inte är lätt att ändra efter att gruppen har skapats.
   * Bas-URL:en visas under `Community Group Name`.
   * Lägg till &quot;.html&quot; för en giltig URL
      *till exempel*`https://localhost:4502/content/sites/mysight/en/mygroup.html`.

* **Menyn** Gruppmall

   Använd listrutan för att välja en tillgänglig mall för [communitygrupper](/help/communities/tools.md).

### Steg 2: Design {#step-design}

### SAMHÄLLSGRUPPTEMA {#community-group-theme}

![communitygrouptema](assets/communitygrouptheme.png)

Ramverket använder [Twitter Bootstrap](https://twitterbootstrap.org/) för att ge webbplatsen en responsiv, flexibel design. Ett av de många förinlästa Bootstrap-temana kan väljas för att formatera den valda communitygruppsmallen, eller så kan ett Bootstrap-tema överföras.

När du väljer det här alternativet överlagras temat med en ogenomskinlig blå bockmarkering.

Du kan välja ett tema som skiljer sig från den överordnade webbplatsens tema.

När communitywebbplatsen har publicerats går det att [redigera egenskaperna](#modifyinggroupproperties) och välja ett annat tema.

### GEMENSKAPSGRUPPENS VARUMÄRKE {#community-group-branding}

![community-group-branding](assets/community-group-branding.png)

Webbplatsmärkning är en bild som visas som en rubrik högst upp på varje sida. Det går att visa en banderoll för gruppen som skiljer sig från andra webbplatssidor.

Bilden bör storleksändras så att den blir lika bred som den förväntade visningen av sidan i webbläsaren och 120 pixlar hög.

Tänk på följande när du skapar eller markerar en bild:

* Bildens höjd beskärs till 120 pixlar från bildens övre kant
* Bilden är fäst vid webbläsarfönstrets vänstra kant
* Det finns ingen storleksändring av bilden, så att den blir följande när bildbredden är:

   * Bilden upprepas vågrätt om den är mindre än webbläsarens bredd.
   * Bilden kommer att beskäras mer än webbläsarens bredd.

### Steg 3: Inställningar {#step-settings}

**MODERATION**

![välj medlemsroller för community-grupper](assets/group-admin.png)

**Moderatorer för communitygrupper**

Som standard ärvs den överordnade communityplatsens lista över moderatorer.

Det går att lägga till moderatorer som är specifika för gruppen. Sök efter medlemmar (från publiceringsmiljön) för att lägga till dem som moderatorer

**Gruppadministratörer**

Som standard är administratören för den överordnade communitywebbplatsen också för grupper.

Det är dock möjligt att utse oberoende gruppadministratörer. Gruppadministratörer kan hantera sin grupp (till exempel G1) och skapa en undergrupp som är kapslad under G1. De kan dessutom tilldela olika administratörer till undergruppen.

En användare U1 kan därför vara administratör i en grupp G1 och en vanlig användare i den kapslade gruppen G2.

**MEDLEMSKAP**

Med inställningen för medlemskap kan du välja ett av tre sätt att skydda en community-grupp.

![community-group-membership](assets/community-group-membership.png)

* **Valfritt medlemskap**

   Om du väljer det här alternativet är communitygruppen en offentlig grupp. Webbplatsmedlemmar kan delta i gruppen och publicera utan att explicit gå med i gruppen. Standard är valt.

* **Obligatoriskt medlemskap**

   Om du väljer det här alternativet är communitygruppen en öppen grupp. Medlemmar på en community kan visa innehållet i gruppen, men måste gå med i gruppen för att publicera innehållet. Medlemmar går med genom att markera `Join` knappen i publiceringsmiljön. Standard är inte valt.

* **Begränsat medlemskap**

   Om du väljer det här alternativet är communitygruppen en hemlig grupp. Community-medlemmar måste uttryckligen bjudas in. Inbjudna medlemmar anges i sökrutan. Medlemmar kan läggas till senare med konsolerna [Medlemmar och grupper](/help/communities/members.md) i författarmiljön. Standard är inte valt.

**MINIATYRBILD**

![community-group-thumbnail](assets/community-group-thumbnail.png)

Miniatyrbilden är en bild som ska visas för gruppen vid författare och publicering.

Den optimala storleken för en gruppbild är 170 x 90 pixlar i ett bildformat som stöds (till exempel JPG eller PNG).

Om ingen bild läggs till visas en standardbild.

![miniatyrbild](assets/thumbnail-image.png)

### Steg 4: Skapa grupp {#step-create-group}

![community-create-group](assets/community-create-group.png)

Om det behövs justeringar använder du knappen **Bakåt** för att göra dem.

När **Skapa** har valts och startats kan processen att skapa gruppen inte avbrytas.

När processen är klar visas kortet för den nya undercommunitywebbplatsen (gruppen) i konsolen Webbplatsgrupper, där författare kan lägga till sidinnehåll eller så kan administratörer ändra webbplatsens egenskaper.

![skapa community-grupp](assets/create-community-groups.png)

>[!NOTE]
>
>Gruppen skapas på alla språk som anges i [steg 1: Community Group Template](/help/communities/groups.md#step-community-group-template) in Additional Available Community Group Languages, in the Community Groups console of the respective community sites.


## Författargruppinnehåll {#author-group-content}

![öppen webbplats](assets/open-site.png)

Sidinnehållet i en grupp kan redigeras med samma verktyg som andra AEM-sidor. Om du vill öppna gruppen för redigering väljer du ikonen Öppna plats som visas när du håller pekaren över gruppkortet.

## Ändra gruppegenskaper {#modify-group-properties}

Egenskaperna för en befintlig undergruppsplats, som anges när en community-grupp skapas, kan ändras genom att välja ikonen Redigera plats, som visas när du hovrar över gruppkortet:

![edit-site](assets/edit-site.png)

Information om följande egenskaper matchar beskrivningarna i avsnittet Skapa [grupp](#group-creation) . Alla kapslade grupper kan ändras, oavsett om de har skapats i publiceringsmiljön eller författarmiljön.

![community-group-basic](assets/community-group-basic.png)

### Ändra grundläggande {#modify-basic}

På BASIC-panelen kan du ändra

* Gruppnamn
* Beskrivning av communitygrupp

Det går inte att ändra användargruppnamnet.

Om du väljer en annan mall för en community-grupp påverkas inte en befintlig community-gruppwebbplats eftersom det inte finns någon koppling mellan mallar och webbplatser.

I stället kan undergruppens [struktur](#modify-structure) ändras.

### Ändra struktur {#modify-structure}

STRUKTURpanelen gör det möjligt att ändra den struktur som ursprungligen skapades från den community-gruppmall som valdes när undercommunitywebbplatsen skapades från antingen författaren eller publiceringsmiljön. På panelen kan du:

* Dra och släpp ytterligare [communityfunktioner](/help/communities/functions.md) i webbplatsstrukturen.
* En instans av en communityfunktion i webbplatsstrukturen:

   * **`Gear icon`**
Redigera inställningar, inklusive visningsrubrik, URL och [behöriga medlemsgrupper](/help/communities/users.md#privilegedmembersgroups).

   * **`Trashcan icon`**
Ta bort funktioner från platsstrukturen.

   * **`Grid icon`**
Ändra den ordning på funktioner som visas i navigeringsfältet på den översta nivån på webbplatsen.

>[!CAUTION]
>
>Visningsrubriken kan ändras utan biverkningar, men du bör inte redigera URL-namnet för en community-funktion som tillhör en community-webbplats.
>
>Om du t.ex. byter namn på URL:en flyttas inte den befintliga UGC:n, vilket resulterar i&quot;UGC-förlust&quot;.


>[!CAUTION]
>
>Gruppfunktionen får inte *vara den *första eller enda* funktionen i platsstrukturen.
>
>Alla andra funktioner, till exempel [sidfunktionen](/help/communities/functions.md#page-function), måste inkluderas och listas först.


**Exempel: Lägga till en kalenderfunktion i en undergruppsstruktur**

![community-group-add-calendar](assets/community-group-add-calendar.png)

### Ändra design {#modify-design}

På designpanelen kan du ändra temat:

* [Community-grupptema](#community-group-theme)
* [Varumärkning för communitygrupper](#community-group-branding)

   * Bläddra till panelens nedre del för att ändra varumärkesbilden.

### Ändra inställningar {#modify-settings}

På panelen INSTÄLLNINGAR kan du lägga till [moderatorer](#moderation)för communityn.

### Ändra medlemskap {#modify-membership}

Panelen [MEDLEMSKAP](#membership) är endast informativ. Det är inte möjligt att ändra vilken typ av gruppmedlemskap som har upprättats, oavsett om det är valfritt, obligatoriskt eller begränsat.

### Ändra miniatyrbild {#modify-thumbnail}

På panelen [MINIATYRBILD](#thumbnail) kan en bild överföras för att representera communitygruppen för webbplatsbesökare i publiceringsmiljön samt i webbgruppskonsolen i författarmiljön.

## Publicera gruppen {#publish-the-group}

![publicera-webbplats](assets/publish-site.png)

När en communitygrupp har skapats eller ändrats kan du publicera (aktivera) gruppen genom att välja `Publish Site` -ikonen.

När gruppen har publicerats visas ett meddelande:

![grupppublicerad](assets/group-published.png)

>[!CAUTION]
>
>Den överordnade communitywebbplatsen och överordnade grupper ska redan ha publicerats.
>
>Community-webbplatsen och kapslade grupper bör publiceras uppifrån och ned.


## Ta bort gruppen {#delete-the-group}

![ta bort ikon](assets/deleteicon.png)

Ta bort en grupp från gruppkonsolen genom att markera ikonen Ta bort grupp, som visas när du håller muspekaren över gruppen.

Detta tar bort alla objekt som är kopplade till gruppen, till exempel så tas allt innehåll i gruppen bort permanent och användarmedlemskap tas bort från systemet.
