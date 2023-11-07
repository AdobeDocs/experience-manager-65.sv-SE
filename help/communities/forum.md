---
title: Forumfunktion
description: Lär dig hur du lägger till och konfigurerar en forumfunktion som ger ett område där inloggade communitymedlemmar kan skapa, visa, följa, söka eller svara på ämnen.
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
docset: aem65
exl-id: 2b1a4917-9db6-436a-a5fd-c102fe41fb9d
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '1219'
ht-degree: 0%

---

# Forumfunktion{#forum-feature}

## Introduktion {#introduction}

I forumfunktionen finns ett område där besökare på den inloggade webbplatsen (community-medlemmar) i publiceringsmiljön kan:

* Skapa ämnen
* Visa och svara på ämnen
* Följ ett avsnitt
* Sök i ett forum
* Hjälp till att moderera foruminnehållet
* Flytta forumämnen mellan sidor

I det här avsnittet av dokumentationen beskrivs:

* Lägga till forumfunktionen på en AEM webbplats.
* Konfigurationsinställningar för `Forum` -komponenten.

### Lägga till ett forum på en sida {#adding-a-forum-to-a-page}

Lägga till en `Forum` -komponent till en sida i redigeringsläge använder du komponentwebbläsaren för att leta upp

* `Communities / Forum`

Och dra den till rätt plats på en sida där forumet ska visas.

Nödvändig information finns på [Grunderna för communitykomponenter](/help/communities/basics.md).

När [nödvändiga bibliotek på klientsidan](/help/communities/essentials-forum.md#essentials-for-client-side) ingår så här `Forum` visas:

![forumkomponent](assets/forum-component.png)

### Konfigurera ett forum {#configuring-a-forum}

Markera den monterade `Forum` så att du kan komma åt och välja `Configure` -ikonen som öppnar redigeringsdialogrutan.

![configure-new](assets/configure-new.png)

![forum-config](assets/forum-config.png)

#### Fliken Inställningar {#settings-tab}

Under **Inställningar** -fliken, ange inställningar för ämnen och svar:

* **Tillåt miniatyrbild för bifogad fil**

  Om du markerar det här alternativet skapas en miniatyrbild av den bifogade bilden.

* **Maximal storlek på miniatyrbild**

  Maximal storlek (i pixlar) för miniatyrbilden för den bifogade filen. Standardvärdet är 800 x 800.

* **Minsta bildstorlek för miniatyrbild**
* **Maximal miniatyrstorlek**

  Maximal storlek (i pixlar) för miniatyrbilden för textbunden bild. Standardvärdet är 800 x 800.

* **Ämnen per sida**

  Definierar antalet ämnen/inlägg som visas per sida. Standardvärdet är 10.

* **Kontrollerad**

  Om det här alternativet är markerat måste publicering av ämnen och kommentarer godkännas innan de kan visas på en publiceringsplats. Standard är avmarkerat.

* **Stängd**

  Om det här alternativet är markerat stängs forumet för nya ämnen och kommentarer. Standard är avmarkerat.

* **RTF-redigerare**

  Om det här alternativet är markerat kan du skriva in ämnen och kommentarer med markeringar. Standard är avmarkerat.

* **Tillåt taggning**

  Tillåt medlemmar att lägga till taggetiketter i sina inlägg (se **Taggfält** -fliken). Standard är avmarkerat.

* **Tillåt filöverföringar**

  Om du markerar det här alternativet kan du tillåta att bifogade filer läggs till i ämnet eller kommentaren. Standard är avmarkerat.

* **Tillåt följande**

  Om du markerar det här alternativet inkluderas följande funktion för foruminlägg, som gör att medlemmar kan [meddelad](/help/communities/notifications.md) av nya tjänster. Standard är avmarkerat.

* **Tillåt fästa**

  Om det här alternativet är markerat kan forumämnen fästas överst i ämneslistan. Standard är avmarkerat.

* **Tillåt innehåll**

  Idén kan identifieras som om den är markerad [presenterat innehåll](/help/communities/featured.md). Standard är avmarkerat.

* **Tillåt e-postprenumerationer**

  Om det här alternativet är markerat, tillåt medlemmar att meddelas om nya inlägg via e-post ([prenumeration](/help/communities/subscriptions.md)). Kräver `Allow Following` ska kontrolleras och [e-post konfigurerad](/help/communities/email.md). Standard är avmarkerat.

* **Maximal filstorlek**

  Endast relevant om `Allow File Uploads` är markerad. Det här fältet begränsar storleken (i byte) på en överförd fil. Standardvärdet är 104857600 (10 MB).

* **Tillåtna filtyper**

  Endast relevant om `Allow File Uploads` är markerad. En kommaavgränsad lista med filtillägg med punktavgränsaren. Exempel: .jpg, .jpeg, .png, .doc, .docx, .pdf. Om någon filtyp har angetts kan de inte överföras. Ingen standard har angetts så att alla filtyper tillåts.

* **Maximal filstorlek för bifogad bild**
Endast relevant om Tillåt filöverföringar är markerat. Maximalt antal byte som en överförd bildfil kan ha. Standardvärdet är 2097152 (2 MB).

* **Tillåt kopplade svar**

  Om det här alternativet är markerat tillåts svar på kommentarer som har publicerats i ämnet. Standard är avmarkerat.

* **Tillåt röstning**

  Inkludera röstfunktionen med ett ämne om det är markerat. Standard är avmarkerat.

* **Tillåt användare att ta bort kommentarer och ämnen**

  Om det här alternativet är markerat kan medlemmar ta bort kommentarer och ämnen som de har skickat in. Standard är avmarkerat.

* **Visa vägbeskrivningar**

  Om du markerar det här alternativet visas navigeringsbeskrivningar på ämnessidor. Standard är markerat.

* **Visa emblem**

  Om det här alternativet är markerat visas intjänad och tilldelad [emblem](/help/communities/implementing-scoring.md) med en medlems blogginlägg. Standard är avmarkerat.

* **Tillåt behöriga medlemmar**

  Om det här alternativet är markerat kan endast behöriga medlemmar skapa innehåll.

* **Tillåtna behöriga medlemmar**

  Lägg till de behöriga medlemmar som har behörighet att skapa innehåll.

* **Blockera användargenererat innehåll i redigeringsläge för författare**

  Om det här alternativet är aktiverat blockeras användargenererat innehåll när du redigerar i redigeringsläge.

* **Aktivera omnämns**

  Om det här alternativet är aktiverat kan registrerade communityanvändare identifiera andra registrerade medlemmar (med förnamn, efternamn, användarnamn) och tagga dem med den vanliga @användarnamnssyntaxen. De taggade användarna får meddelanden om sina omnämnanden.

* **Max. omnämnanden**

  Begränsa det maximala antalet omnämnanden som tillåts i ett inlägg. Standardvärdet är 10.

* **Mönster för användargränssnittets omnämnande**

  Ange den tillåtna mönstersträngen för att tagga (@mention) den registrerade användaren i ett inlägg. Till exempel, `~{{familyName}}{{givenName}}`.

>[!NOTE]
>
>Det kan vara nödvändigt att kontrollera båda `AllowThreaded Replies` och `Allow users to Delete Comments and Topics` för att aktivera kommentarer om ett ämne.

#### Fliken Användarmoderering {#user-moderation-tab}

Under **Användarmoderering** anger du hur publicerade ämnen och svar (användargenererat innehåll) ska hanteras. Mer information finns i [Modererar användargenererat innehåll](/help/communities/moderate-ugc.md).

* **Neka inlägg**

  Om det här alternativet är markerat kan pålitliga medlemsmoderatorer neka inlägg och förhindra att posten visas på det offentliga forumet. Standard är avmarkerat.

* **Stäng/öppna avsnitt igen**

  Om det här alternativet är markerat kan pålitliga medlemsmoderatorer stänga ett ämne för ytterligare redigeringar och kommentarer, och kan även öppna ett avsnitt på nytt. Standard är avmarkerat.

* **Flytta ämnen**

  Om det här alternativet är markerat kan moderatorer på publiceringssidan flytta ämnen. Standard är markerat.

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

Under **Taggfält** -fliken, de taggar som kan användas, om de tillåts under **Inställningar** är begränsade enligt de namnutrymmen som har valts.

* **Tillåtna namnutrymmen**

  Relevant om `Allow Tagging` kontrolleras under **Inställningar** -fliken. De taggar som kan användas är begränsade till de inom de namnutrymmeskategorier som kontrolleras. Listan med namnutrymmen innehåller&quot;Standardtaggar&quot; (standardnamnutrymmet) och&quot;Inkludera alla taggar&quot;. Standardvärdet är inget markerat, vilket betyder att alla namnutrymmen är tillåtna.

* **Förslagsgräns**

  Ange antalet taggar som ska visas som ett förslag till medlemmens inlägg i forumet. Standardvärdet är **-**1 (inga gränser).

#### Fliken Översättning {#translation-tab}

Under **Översättning** om översättning är aktiverat för communitywebbplatsen kan översättning ställas in för att översätta hela ämnet eller valda inlägg.

* **Översätt alla**

  Om det här alternativet är markerat översätts forumtråden till användarens önskade språk. Standard är avmarkerat.

#### Fliken Sorteringsinställningar {#sort-settings-tab}

Under **Sorteringsinställningar** anger du hur de bokförda kommentarerna ska sorteras när de visas.

* **Sortera efter**

  Kontrollera alla tillåtna sorteringsval: `Newest, Oldest, Last Updated, Most Viewed, Most Active, Most Followed and Most Liked`. Standard är `Newest, Oldest, Last Updated`.

* **Ange som standard**

  Dra nedåt om du vill välja något av de markerade sorteringsalternativen som ska visas som standard. Standard är `Newest`.

* **Välj tidsalternativ för Analytics-sortering**

  Dra nedåt för att välja något av följande alternativ: `All, Last 24 Hours, Last 7 Days, Last 30 Days`.

  Standard är `All`.

### Ytterligare information {#additional-information}

Mer information finns på [Grundläggande om forum](/help/communities/essentials-forum.md) för utvecklare.

moderering av inlägg och kommentarer finns i [Modererar användargenererat innehåll](/help/communities/moderate-ugc.md).

Information om hur du taggar publicerade ämnen och kommentarer finns i [Tagga användargenererat innehåll](/help/communities/tag-ugc.md).

För översättning av publicerade ämnen och kommentarer, se [Översätter användargenererat innehåll](/help/communities/translate-ugc.md).
