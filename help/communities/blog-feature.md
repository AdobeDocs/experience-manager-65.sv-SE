---
title: Bloggfunktion
seo-title: Bloggfunktion
description: Community-information i ett journalformat
seo-description: Community-information i ett journalformat
uuid: 7323063f-81e8-45c3-9035-bf7df6124830
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: cf8b3d72-30ba-40ca-ae48-b61abbb28802
docset: aem65
translation-type: tm+mt
source-git-commit: 272eedc1585dbdea315b49d010e4b1d78cedc360

---


# Bloggfunktion {#blog-feature}

## Introduktion {#introduction}

Bloggfunktionen för AEM Communities har transformerats från en redigeringsaktivitet till en verklig communityaktivitet som äger rum i publiceringsmiljön.

Bloggfunktionen har stöd för att tillhandahålla communityinformation i journalformat. Bloggposterna görs i publiceringsmiljön av behöriga medlemmar (registrerade, inloggade användare).

Bloggfunktionen innehåller:

* Publicera och skapa bloggartiklar och kommentarer
* RTF-redigering
* Textbundna bilder (med stöd för dra och släpp)
* Inbäddat innehåll i sociala nätverk ([inbäddat stöd](/help/communities/blog-developer-basics.md#allowing-rich-media))
* Snabbläge
* Schemalagd publicering
* Disponera för (en [behörig medlem](/help/communities/users.md#privileged-members-group) kan skapa innehåll för en annan community-medlems räkning)
* [Sammanhangsberoende och gruppmoderering](/help/communities/moderate-ugc.md) av bloggartiklar och kommentarer

I det här avsnittet av dokumentationen beskrivs:

* Lägga till bloggfunktionen på en AEM-webbplats
* Konfigurationsinställningar för bloggkomponenter

>[!NOTE]
>
>Komponenterna `Journal`och `Journal Sidebar` kallas `Blog` och `Blog Sidebar`.
>
>Bloggfunktionen i AEM 6.0 och tidigare versioner har nu tagits bort. Det baserades på en mall och tilläts endast författare att skapa innehåll i författarmiljön.

## Lägga till bloggkomponenter på en sida {#adding-blog-components-to-a-page}

Om du vill lägga till en blogg på en sida i redigeringsläge använder du komponentwebbläsaren för att hitta

* `Communities / Blog`
* `Communities / Blog Sidebar`

och dra dem till en plats på en sida där bloggen ska visas.

Mer information finns i Grunderna för [communitykomponenter](/help/communities/basics.md).

När de [nödvändiga klientbiblioteken](/help/communities/blog-developer-basics.md#essentials-for-client-side) inkluderas visas `Blog`komponenten så här:

![chlimage_1-229](assets/chlimage_1-229.png)

Och hur `Blog Sidebar` visas:

![chlimage_1-230](assets/chlimage_1-230.png)

### Konfigurerar blogg {#configuring-blog}

Markera den monterade `Blog` komponent som du vill öppna och välj den `Configure` ikon som öppnar redigeringsdialogrutan.

![chlimage_1-231](assets/chlimage_1-231.png) ![Blog settings](assets/blog-configure.png)

#### Fliken Inställningar {#settings-tab}

Ange bloggens grundläggande funktioner på fliken **Inställningar** :

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

   Om det här alternativet är aktiverat blockeras användargenererat innehåll när redigering i redigeringsläge.

* **Journaltitel**

   Den bloggtitel som ska visas på sidan.

>[!NOTE]
>
>Journaltiteln används för att automatiskt skapa en URL för bloggen.
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

   Om det här alternativet är markerat kan medlemmar lägga till taggetiketter i sina inlägg (se fliken **Taggfält** ). Standard är avmarkerat.

* **Tillåt filöverföringar**

   Om du markerar det här alternativet kan du tillåta att bifogade filer läggs till i ett blogginlägg eller en kommentar. Standard är avmarkerat.

* **Maximal filstorlek**

   Relevant endast om `Allow File Uploads` är markerat. Det här fältet begränsar storleken (i byte) på en överförd fil. Standardvärdet är 104857600 (10 MB).

* **Tillåtna filtyper**

   Relevant endast om `Allow File Uploads` är markerat. En kommaavgränsad lista med filtillägg med&quot;punktavgränsaren&quot;. Till exempel: .jpg, .jpeg, .png, .doc, .docx, .pdf. Om någon filtyp har angetts kan de som inte har angetts inte överföras. Ingen standard har angetts så att alla filtyper tillåts.

* **Maximal filstorlek för bifogad bild**

   Endast relevant om Tillåt filöverföringar är markerat. Maximalt antal byte som en överförd bildfil kan ha. Standardvärdet är 2097152 (2 MB).

* **Tillåt svar**

   Om det här alternativet är markerat tillåts svar på kommentarer som har skickats till blogginlägget. Standard är avmarkerat.

* **Tillåt röstning**

   Om du markerar det här alternativet inkluderas röstningsfunktionen med ett blogginlägg. Standard är avmarkerat.

* **Tillåt användare att ta bort kommentarer och ämnen**

   Om det här alternativet är markerat kan medlemmar ta bort kommentarer och blogginlägg som de har skickat in. Standardvärdet är** **unchecked.

* **Tillåt följande**

   Om det här alternativet är markerat kan du inkludera följande funktion för bloggartiklar, som gör att medlemmar kan [meddelas](/help/communities/notifications.md) om nya inlägg. Standard är avmarkerat.

* **Tillåt e-postprenumerationer**

   Om det här alternativet är markerat kan medlemmar meddelas om nya inlägg via e-post ([prenumeration](/help/communities/subscriptions.md)). Kräver `Allow Following` att kontrolleras och att [e-post konfigureras](/help/communities/email.md). Standard är avmarkerat.

* **Visa emblem**

   Om det här alternativet är markerat visas färdiga och tilldelade [märken](/help/communities/implementing-scoring.md) med en medlems blogginlägg. Standard är avmarkerat.

* **Hämta inte svar på listsidan**

* **Tillåt innehåll**

   Om du markerar det här alternativet kan idén identifieras som [aktuellt innehåll](/help/communities/featured.md). Standard är avmarkerat.

* **Aktivera omnämnande**

   Om det här alternativet är aktiverat kan registrerade communityanvändare identifiera andra registrerade medlemmar (med förnamn, efternamn, användarnamn) och tagga dem med den vanliga @användarnamnssyntaxen. De taggade användarna får meddelanden om sina omnämnanden.

* **Max. omnämnanden**

   Begränsa det maximala antalet omnämnanden som tillåts i ett inlägg. Standardvärdet är 10.

* **Mönster för användargränssnittets omnämnande**

   Ange den tillåtna mönstersträngen för att tagga (@mention) den registrerade användaren i ett inlägg. Till exempel ~{{familyName}}{{givenName}}.

#### Fliken Användarmoderering {#user-moderation-tab}

Under fliken **Användarmoderering** anger du modereringsinställningarna:

* **Neka inlägg**

   Om det här alternativet är markerat kan pålitliga medlemsmoderatorer neka inlägg och förhindra att posten visas på det offentliga forumet. Standard är avmarkerat.

* **Stäng/öppna avsnitt igen**

   Om det här alternativet är markerat kan pålitliga medlemsmoderatorer stänga ett ämne för ytterligare redigeringar och kommentarer, och kan även öppna ett avsnitt på nytt. Standard är avmarkerat.

* **Flagga inlägg**

   Om det här alternativet är markerat kan medlemmar flagga andras ämnen eller kommentarer som olämpliga. Standard är avmarkerat**.**

* **Flaggorsakslista**

   Om det här alternativet är markerat kan medlemmarna välja, från en nedrullningsbar lista, orsaken till att ett ämne eller en kommentar har flaggats som olämplig. Standard är avmarkerat.

* **Anledning till anpassad flagga**

   Om det här alternativet är markerat kan medlemmarna ange en egen orsak till att ett ämne eller en kommentar flaggas som olämplig. Standard är avmarkerat**.**

* **Modereringströskel**

   Ange hur många gånger ett ämne eller en kommentar måste flaggas av medlemmar innan moderatorerna meddelas. Standardvärdet är 1 (en gång).

* **Flaggningsgräns**

   Ange hur många gånger ett ämne eller en kommentar måste flaggas innan det döljs för den offentliga vyn. Om värdet är -1 döljs aldrig det flaggade ämnet eller kommentaren från den offentliga vyn. Annars måste talet vara större än eller lika med modereringströskeln. Standardvärdet är 5.

#### Fliken Taggfält {#tag-field-tab}

Under fliken **Tagg** anger du vilka taggar som kan användas om **Tillåt taggning** är markerat på fliken **Inställningar** :

* **Tillåtna namnutrymmen**

   Relevant om `Allow Tagging` är markerat under fliken **Inställningar **. De taggar som kan användas är begränsade till de inom de namnutrymmeskategorier som kontrolleras. Listan med namnutrymmen innehåller &quot;Standardtaggar&quot; (standardnamnutrymmet) och &quot;Inkludera alla taggar&quot;. Standardvärdet är inget markerat, vilket betyder att alla namnutrymmen är tillåtna.

* **Förslagsgräns**

   Ange antalet taggar som ska visas som ett förslag till medlemmens inlägg i forumet. Värdet -1 betyder inga gränser. Standardvärdet är 0.

### Konfigurerar bloggmarginallist {#configuring-blog-sidebar}

När du dubbelklickar på `Blog Sidebar` komponenten öppnas en redigeringsdialogruta.

Under fliken Inställningar **för** journalmarginaler anger du datumformatet för arkiv och vilken typ av poster som ska visas i sidofältet:

![blog-component-sidebar](assets/blog-component-sidebar.png)

* **Datumformat**

   Det format som används för att visa arkiv för blogginlägg. Formatet använder platshållare enligt Java-konventionen.

   * yyyy: hela året, till exempel 2015
   * yy: kort år, som &quot;15&quot;
   * MMMM : hel månad, som juni
   * MMM: kort månad, som Jun
   * MM: månadsnummer, som 06
   Standardvärdet är&quot;yyyy MMMM&quot;, som skulle visas t.ex.&quot;2015 Juni&quot;

* **Vytyp**

   Titel och typ av blogginlägg som ska visas i sidlisten. Valet är mellan

   * Författare
   * Kategorier
   * Arkiv

* **Bloggkomponentsökväg**

   *(Valfritt)* Platsen för den bloggresurs som bloggartiklar ska listas från. Om det lämnas tomt används komponenten för resourceType `social/journal/components/hbs/journal` som visas på samma sida.

   * Exempel: `/content/sites/engage/en/blog/jcr:content/content/primary/blog`

* **Förslagsgräns**

   Antalet bloggartiklar som ska visas. Värdet -1 betyder ingen gräns. Standardvärdet är -1.

## Site Visitor Experience {#site-visitor-experience}

I publiceringsmiljön kommer bloggfunktionen att visa den senaste bloggartikeln följt av äldre bloggartiklar i fallande ordning. Bloggsidofälten gör att besökare kan använda filter för att begränsa urvalet av bloggartiklar.

Bloggartikeln följs av en länk för att skicka eller visa kommentarer.

När en bloggartikel är markerad visas bloggartikeln och kommentarerna (om den är aktiverad).

Andra funktioner beror på om besökaren är en moderator, administratör, community-medlem, privilegierad medlem eller anonym.

### Arbeta med artiklar {#working-with-articles}

När du skapar en ny bloggartikel kan du välja att:

1. Publicera omedelbart
1. Publicera ett utkast
1. Publicera vid ett schemalagt datum och en schemalagd tidpunkt

Bloggartiklarna visas under lämplig flik (Publicerad, Utkast eller Schemalagd) för medlemmar som kan skriva vid publicering.

#### Styrelsemedlemmar och administratörer {#moderators-and-administrators}

När den inloggade användaren har moderator- eller administratörsbehörighet kan han/hon utföra [modereringsåtgärder](/help/communities/moderate-ugc.md) (som tillåts av komponentens konfiguration) på alla bloggartiklar och kommentarer som publiceras på en blogg.

![chlimage_1-232](assets/chlimage_1-232.png)

#### Medlemmar {#members}

När den inloggade användaren är en community-medlem eller [behörig medlem](/help/communities/users.md#privileged-members-group) (beroende på konfiguration) kan användaren välja `New Article` att skapa och publicera en ny bloggartikel.

De får särskilt

* Skapa en ny bloggartikel
* Skicka en ny bloggartikel för en annan medlem
* Skicka en kommentar till en bloggartikel
* Redigera en egen bloggartikel eller kommentar
* Ta bort en egen bloggartikel eller kommentar
* Flagga andras blogginlägg eller kommentarer

![chlimage_1-233](assets/chlimage_1-233.png) ![chlimage_1-234](assets/chlimage_1-234.png)

#### Anonym {#anonymous}

Besökare som inte är inloggade kan endast läsa inlagda bloggartiklar och kommentarer, översätta dem om de stöds, men kan inte lägga till en bloggartikel eller kommentar eller flagga andras artiklar eller kommentarer.

![chlimage_1-235](assets/chlimage_1-235.png)

## Additional Information {#additional-information}

Mer information finns på [Blog Essentials](/help/communities/blog-developer-basics.md) -sidan för utvecklare.

Mer information om moderering av blogginlägg och kommentarer finns i [Hantera användargenererat innehåll](/help/communities/moderate-ugc.md).

Information om hur du taggar blogginlägg och kommentarer finns i [Tagga användargenererat innehåll](/help/communities/tag-ugc.md).

Information om översättning av blogginlägg och kommentarer finns i [Översätta användargenererat innehåll](/help/communities/translate-ugc.md).
