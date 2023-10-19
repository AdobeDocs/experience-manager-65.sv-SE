---
title: Bloggfunktion
description: Lär dig hur bloggfunktionen kan ge communityinformation i journalformat. Posterna görs i publiceringsmiljön av behöriga användare.
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
docset: aem65
exl-id: 4650ac36-5506-4efc-be35-fac9e5a58f3d
source-git-commit: b8887b4a6f757352e9dbfdf074c10e9ccd6dbd4f
workflow-type: tm+mt
source-wordcount: '1670'
ht-degree: 0%

---

# Bloggfunktion {#blog-feature}

## Introduktion {#introduction}

Bloggfunktionen för AEM Communities har transformerats från en redigeringsaktivitet till en verklig community-aktivitet som äger rum i publiceringsmiljön.

Bloggfunktionen har stöd för att tillhandahålla communityinformation i journalformat. Bloggposterna görs i publiceringsmiljön av behöriga medlemmar (registrerade, inloggade användare).

Bloggfunktionen innehåller:

* Publicera och skapa bloggartiklar och kommentarer
* Redigera avancerad text
* Textbundna bilder (med stöd för dra och släpp)
* Inbäddat innehåll i sociala nätverk ([Stöd för inbäddning](/help/communities/blog-developer-basics.md#allowing-rich-media))
* Utkastläge
* Schemalagd publicering
* Skapa för räkning (en [behörig medlem](/help/communities/users.md#privileged-members-group) kan skapa innehåll för en annan community-medlem)
* [Kontext- och gruppmoderering](/help/communities/moderate-ugc.md) bloggartiklar och kommentarer

I det här avsnittet av dokumentationen beskrivs:

* Lägga till bloggfunktionen på en AEM webbplats
* Konfigurationsinställningar för bloggkomponenter

>[!NOTE]
>
>Komponenterna `Journal` och `Journal Sidebar` är namngivna `Blog` och `Blog Sidebar`.
>
>Bloggfunktionen i AEM 6.0 och tidigare versioner har nu tagits bort. Det baserades på en mall och tilläts endast författare att skapa innehåll i författarmiljön.

## Lägga till bloggkomponenter på en sida {#adding-blog-components-to-a-page}

Om du vill lägga till en blogg på en sida i redigeringsläge använder du komponentwebbläsaren för att hitta

* `Communities / Blog`
* `Communities / Blog Sidebar`

Dra dem till en plats på en sida där bloggen ska visas.

Nödvändig information finns på [Grunderna för communitykomponenter](/help/communities/basics.md).

När [nödvändiga bibliotek på klientsidan](/help/communities/blog-developer-basics.md#essentials-for-client-side) ingår `Blog` visas här:

![add-blog-component](assets/add-blog-component.png)

### Konfigurerar blogg {#configuring-blog}

Markera den monterade `Blog` så att du kan komma åt och välja `Configure` -ikonen som öppnar dialogrutan för redigering.

![konfigurera](assets/configure-new.png)

![Blogginställningar](assets/blog-configure.png)

#### Fliken Inställningar {#settings-tab}

Under **Inställningar** anger du bloggens grundläggande funktioner:

* **Tillåt miniatyrbild för bifogad fil**

  Om du markerar det här alternativet skapas en miniatyrbild av den bifogade bilden.

* **Maximal storlek på miniatyrbild**

  Maximal storlek (i pixlar) för miniatyrbilden för den bifogade filen. Standardvärdet är 800 x 800.

* **Minsta bildstorlek för miniatyrbild**

  Minsta bildstorlek (i byte) för generering av miniatyrbilder för textbundna bilder. Standardvärdet är 100000 byte (100 kB).

* **Maximal miniatyrstorlek**

  Maximal storlek (i pixlar) för miniatyrbilden för textbunden bild. Standardvärdet är 800 x 800.

* **Tillåt behöriga medlemmar**

  Om det här alternativet är markerat kan endast behöriga medlemmar skapa innehåll.

* **Tillåtna behöriga medlemmar**

  Lägg till de behöriga medlemmar som har behörighet att skapa innehåll.

* **Blockera användargenererat innehåll i redigeringsläge för författare**

  Om det här alternativet är aktiverat blockeras användargenererat innehåll när du redigerar i redigeringsläge.

* **Journaltitel**

  Den bloggtitel som ska visas på sidan.

>[!NOTE]
>
>Journaltiteln används för att automatiskt skapa en URL för bloggen.
>
>Maximalt 50 tecken (med ytterligare 5 tecken för unikt utseende) används från journaltiteln som du anger här för att skapa en URL för bloggen.

* **Journalbeskrivning**

  Bloggbeskrivningen.

* **Ämnen per sida**

  Definierar antalet blogginlägg/kommentarer som visas per sida. Standardvärdet är 10.

* **Kontrollerad**

  Om du markerar det här alternativet måste du godkänna att blogginlägg och kommentarer skickas innan de visas på en publicerad webbplats. Standardvärdet är avmarkerat.

* **Stängd**

  Om du markerar det här alternativet stängs bloggen för nya blogginlägg och kommentarer. Standard är avmarkerat.

* **RTF-redigerare**

  Om du markerar det här alternativet kan blogginlägg och kommentarer skrivas in med kod. Standard är markerat.

* **Tillåt taggning**

  Tillåt medlemmar att lägga till taggetiketter i sina inlägg (se **Taggfält** -fliken). Standard är avmarkerat.

* **Tillåt filöverföringar**

  Om du markerar det här alternativet kan du tillåta att bifogade filer läggs till i ett blogginlägg eller en kommentar. Standard är avmarkerat.

* **Maximal filstorlek**

  Endast relevant om `Allow File Uploads` är markerad. Det här fältet begränsar storleken (i byte) på en överförd fil. Standardvärdet är 104857600 (10 MB).

* **Tillåtna filtyper**

  Endast relevant om `Allow File Uploads` är markerad. En kommaavgränsad lista med filtillägg med punktavgränsaren. Exempel: .jpg, .jpeg, .png, .doc, .docx, .pdf. Om någon filtyp anges går det inte att överföra de filtyper som inte har angetts. Ingen standard har angetts så att alla filtyper tillåts.

* **Maximal filstorlek för bifogad bild**

  Endast relevant om Tillåt filöverföringar är markerat. Maximalt antal byte som en överförd bildfil kan ha. Standardvärdet är 2097152 (2 MB).

* **Tillåt svar**

  Om det här alternativet är markerat tillåts svar på kommentarer som har skickats till blogginlägget. Standard är avmarkerat.

* **Tillåt röstning**

  Om du markerar det här alternativet inkluderas röstningsfunktionen med ett blogginlägg. Standard är avmarkerat.

* **Tillåt användare att ta bort kommentarer och ämnen**

  Om det här alternativet är markerat kan medlemmarna ta bort de kommentarer och blogginlägg som de har skickat. Standard är avmarkerat.

* **Tillåt följande**

  Om du markerar det här alternativet inkluderar du följande funktion för bloggartiklar, som gör att medlemmar kan [meddelad](/help/communities/notifications.md) av nya tjänster. Standard är avmarkerat.

* **Tillåt e-postprenumerationer**

  Om det här alternativet är markerat, tillåt medlemmar att meddelas om nya inlägg via e-post ([prenumeration](/help/communities/subscriptions.md)). Kräver `Allow Following` ska kontrolleras och [e-post konfigurerad](/help/communities/email.md). Standard är avmarkerat.

* **Visa emblem**

  Om det här alternativet är markerat visas intjänad och tilldelad [emblem](/help/communities/implementing-scoring.md) med en medlems blogginlägg. Standard är avmarkerat.

* **Hämta inte svar på listsidan**

* **Tillåt innehåll**

  Om det här alternativet är markerat identifieras idén som [presenterat innehåll](/help/communities/featured.md). Standard är avmarkerat.

* **Aktivera omnämns**

  Om det här alternativet är aktiverat kan registrerade communityanvändare identifiera andra registrerade medlemmar (med förnamn, efternamn, användarnamn) och tagga dem med den vanliga @användarnamnssyntaxen. De taggade användarna får meddelanden om sina egna omnämnanden.

* **Max. omnämnanden**

  Begränsa det maximala antalet omnämnanden som tillåts i ett inlägg. Standardvärdet är 10.

* **Mönster för användargränssnittets omnämnande**

  Ange den tillåtna mönstersträngen för att tagga (@mention) den registrerade användaren i ett inlägg. Till exempel, `~{{familyName}}{{givenName}}`.

#### Fliken Användarmoderering {#user-moderation-tab}

Under **Användarmoderering** anger du modereringsinställningar:

* **Neka inlägg**

  Om det här alternativet är markerat kan pålitliga medlemsmoderatorer neka inlägg och förhindra att posten visas på det offentliga forumet. Standard är avmarkerat.

* **Stäng/öppna avsnitt igen**

  Om det här alternativet är markerat kan pålitliga medlemsmoderatorer stänga ett ämne för ytterligare redigeringar och kommentarer, och kan även öppna ett avsnitt på nytt. Standard är avmarkerat.

* **Flagga inlägg**

  Om det här alternativet är markerat kan medlemmar flagga andras ämnen eller kommentarer som olämpliga. Standard är avmarkerat.

* **Flaggorsakslista**

  Om det här alternativet är markerat kan medlemmarna välja, från en nedrullningsbar lista, orsaken till att ett ämne eller en kommentar har flaggats som olämplig. Standard är avmarkerat.

* **Anledning till anpassad flagga**

  Om det här alternativet är markerat kan medlemmarna ange en egen orsak till att ett ämne eller en kommentar flaggas som olämplig. Standard är avmarkerat.

* **Modereringströskel**

  Ange hur många gånger ett ämne eller en kommentar måste flaggas av medlemmar innan moderatorerna meddelas. Standardvärdet är 1 (en gång).

* **Flaggningsgräns**

  Ange hur många gånger ett ämne eller en kommentar måste flaggas innan det döljs för den offentliga vyn. Om värdet är -1 döljs aldrig det flaggade ämnet eller kommentaren från den offentliga vyn. Annars måste talet vara större än eller lika med modereringströskeln. Standardvärdet är 5.

#### Fliken Taggfält {#tag-field-tab}

Under **Taggfält** anger du vilka taggar som kan användas om **Tillåt taggning** är markerad på **Inställningar** tab :

* **Tillåtna namnutrymmen**

  Relevant om `Allow Tagging` kontrolleras under **Inställningar** -fliken. De taggar som kan användas är begränsade till de taggar som finns i de namnutrymmeskategorier som är markerade. Listan med namnutrymmen innehåller&quot;Standardtaggar&quot; (standardnamnutrymmet) och&quot;Inkludera alla taggar&quot;. Standardvärdet är inget markerat, vilket betyder att alla namnutrymmen är tillåtna.

* **Förslagsgräns**

  Ange antalet taggar som ska visas som ett förslag till medlemmens inlägg i forumet. Värdet -1 betyder inga gränser. Standardvärdet är 0.

### Konfigurerar bloggmarginallist {#configuring-blog-sidebar}

När du dubbelklickar på `Blog Sidebar` öppnas en redigeringsdialogruta.

Under **Inställningar för journalmarginallist** anger du datumformatet för arkiv och vilken typ av poster som ska visas i sidofältet:

![blog-component-sidebar](assets/blog-component-sidebar.png)

* **Datumformat**

  Det format som används för att visa arkiv för blogginlägg. Formatet använder platshållare enligt Java™-konventionen.

   * yyyy : hela året, till exempel 2015
   * yy: kort år, som &#39;15&#39;
   * MMMMM : hel månad, till exempel juni
   * MMM: kort månad, som Jun
   * MM : månadsnummer, t.ex. 06

  Standardvärdet är&quot;yyyy MMMM&quot;, som skulle visas t.ex.&quot;2015 Juni&quot;

* **Vytyp**

  Titel och typ av blogginlägg som ska visas i sidlisten. Valet är mellan

   * Författare
   * Kategorier
   * Arkiv

* **Bloggkomponentsökväg**

  *(Valfritt)* Platsen för bloggresursen som bloggartiklar ska listas från. Om det lämnas tomt används komponenten för resourceType `social/journal/components/hbs/journal` som visas på samma sida.

   * Till exempel, `/content/sites/engage/en/blog/jcr:content/content/primary/blog`

* **Förslagsgräns**

  Antalet bloggartiklar som ska visas. Värdet -1 betyder ingen gräns. Standardvärdet är -1.

## Site Visitor Experience {#site-visitor-experience}

I publiceringsmiljön visar bloggfunktionen den senaste bloggartikeln följt av äldre bloggartiklar i fallande ordning. Bloggsidofälten gör att besökare kan använda filter för att begränsa urvalet av bloggartiklar.

Bloggartikeln följs av en länk för att skicka eller visa kommentarer.

När en bloggartikel är markerad visas bloggartikeln och kommentarerna (om den är aktiverad).

Andra funktioner beror på om besökaren är en moderator, administratör, community-medlem, privilegierad medlem eller anonym.

### Arbeta med artiklar {#working-with-articles}

När du skapar en bloggartikel kan du göra följande:

1. Publicera omedelbart
1. Publicera ett utkast
1. Publicera vid ett schemalagt datum och en schemalagd tidpunkt

Bloggartiklarna visas under lämplig flik (Publicerad, Utkast eller Schemalagd) för medlemmar som kan skriva vid publicering.

#### Styrelsemedlemmar och administratörer {#moderators-and-administrators}

När den inloggade användaren har moderator- eller administratörsbehörighet kan de utföra [modereringsuppgifter](/help/communities/moderate-ugc.md) (enligt komponentens konfiguration) på alla bloggartiklar och kommentarer som har skickats till en blogg.

![moderator-hemsida](assets/moderator-homepage.png)

#### Medlemmar {#members}

När den inloggade användaren är en community-medlem eller [behörig medlem](/help/communities/users.md#privileged-members-group) (beroende på konfiguration) kan de välja `New Article` för att skapa och publicera en ny bloggartikel.

De får särskilt

* Skapa en bloggartikel
* Skicka en ny bloggartikel för en annan medlem
* Skicka en kommentar till en bloggartikel
* Redigera en egen bloggartikel eller kommentar
* Ta bort en egen bloggartikel eller kommentar
* Flagga andras blogginlägg eller kommentarer

![medlemshemsida](assets/member-homepage.png)

![create-blog](assets/create-blog.png)

#### Anonym {#anonymous}

Besökare som inte är inloggade kan endast läsa inlagda bloggartiklar och kommentarer, översätta dem om de stöds, men kan inte lägga till en bloggartikel eller kommentar eller flagga andras artiklar eller kommentarer.

![anonym användarvy](assets/anonymous-user-view.png)

## Ytterligare information {#additional-information}

Mer information finns på [Blog Essentials](/help/communities/blog-developer-basics.md) för utvecklare.

Mer information om moderering av blogginlägg och kommentarer finns i [Modererar användargenererat innehåll](/help/communities/moderate-ugc.md).

Information om hur du taggar blogginlägg och kommentarer finns i [Tagga användargenererat innehåll](/help/communities/tag-ugc.md).

Information om översättning av blogginlägg och kommentarer finns i [Översätter användargenererat innehåll](/help/communities/translate-ugc.md).
