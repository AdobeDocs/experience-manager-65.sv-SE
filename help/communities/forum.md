---
title: Forumfunktion
seo-title: Forumfunktion
description: Lägga till och konfigurera forumfunktionen
seo-description: Lägga till och konfigurera forumfunktionen
uuid: e69be4e1-c9d5-4d51-8e7e-609e5460e378
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: d936cef5-ad76-482d-97bf-c40137185812
docset: aem65
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65

---


# Forumfunktion{#forum-feature}

## Introduktion {#introduction}

Forumfunktionen tillhandahåller ett område för inloggade webbplatsbesökare (community-medlemmar) i publiceringsmiljön till :

* skapa nya ämnen
* visa och svara på ämnen
* följa ett ämne
* sök i forum
* bidra till att moderera foruminnehållet
* flytta forumämnen från en sida till en annan

Detta avsnitt i dokumentationen beskriver

* lägga till forumfunktionen på en AEM-webbplats
* konfigurationsinställningar för `Forum`komponenten

### Lägga till ett forum på en sida {#adding-a-forum-to-a-page}

Om du vill lägga till en `Forum` komponent på en sida i redigeringsläge använder du komponentwebbläsaren för att leta reda på

* `Communities / Forum`

och dra den till rätt plats på en sida där forumet ska visas.

Mer information finns i Grunderna för [communitykomponenter](/help/communities/basics.md).

När de [nödvändiga klientbiblioteken](/help/communities/essentials-forum.md#essentials-for-client-side) inkluderas visas `Forum`komponenten så här:

![chlimage_1-104](assets/chlimage_1-104.png)

### Konfigurera ett forum {#configuring-a-forum}

Markera den monterade `Forum` komponent som du vill öppna och välj den `Configure` ikon som öppnar redigeringsdialogrutan.

![chlimage_1-105](assets/chlimage_1-105.png) ![forum-config](assets/forum-config.png)

#### Fliken Inställningar {#settings-tab}

Under fliken **Settings **anger du inställningar för ämnen och svar:

* **Tillåt miniatyrbild för bifogad fil**Om det här alternativet är markerat skapas en miniatyrbild av den bifogade bilden.
* **Maximal storlek** för miniatyrbildsminiatyr för bifogad miniatyrbild (i pixlar). Standardvärdet är 800 x 800.

* **Minsta bildstorlek för miniatyrbild**
* **Maximal miniatyrbildsstorlek** Maximal storlek (i pixlar) för miniatyrbilden för textbunden bild. Standardvärdet är 800 x 800.

* **Ämnen per sida**Definierar antalet ämnen/inlägg som visas per sida. Standardvärdet är 10.
* **Moderated** Om det här alternativet är markerat måste publicering av ämnen och kommentarer godkännas innan de visas på en publiceringswebbplats. Standard är avmarkerat.

* **Stängt** Om det här alternativet är markerat stängs forumet för nya ämnen och kommentarer. Standard är avmarkerat.

* **RTF-redigeraren** Om det här alternativet är markerat kan du skriva in ämnen och kommentarer med markeringar. Standard är avmarkerat.

* **Tillåt taggning** Om det här alternativet är markerat tillåter du medlemmar att lägga till taggetiketter i sitt inlägg (se fliken **Taggfält** ). Standard är avmarkerat.

* **Tillåt filöverföringar** Om det här alternativet är markerat tillåter du att bifogade filer läggs till i ämnet eller kommentaren. Standard är avmarkerat.

* **Tillåt följande** om det är markerat, inkludera följande funktion för foruminlägg, som gör att medlemmar kan [meddelas](/help/communities/notifications.md) om nya inlägg. Standard är avmarkerat.

* **Tillåt fästa** Om det här alternativet är markerat kan forumämnen fästas överst i ämneslistan. Standard är avmarkerat.

* **Tillåt innehåll** om det är markerat kan idén identifieras som [aktuellt innehåll](/help/communities/featured.md). Standard är avmarkerat.

* **Tillåt e-postprenumerationer** Om det här alternativet är markerat tillåter du medlemmar att meddelas om nya inlägg via e-post ([prenumeration](/help/communities/subscriptions.md)). Kräver `Allow Following` att kontrolleras och att [e-post konfigureras](/help/communities/email.md). Standard är avmarkerat.

* **Maximal filstorlek** relevant endast om `Allow File Uploads` markeras. Det här fältet begränsar storleken (i byte) på en överförd fil. Standardvärdet är 104857600 (10 MB).

* **Tillåtna filtyper**&#x200B;är bara relevanta om `Allow File Uploads` markeras. En kommaavgränsad lista med filtillägg med&quot;punktavgränsaren&quot;. Till exempel: .jpg, .jpeg, .png, .doc, .docx, .pdf. Om någon filtyp har angetts kan de som inte har angetts inte överföras. Standard är inte angivet så att** **alla filtyper tillåts.

* **Max Attach Image File Size** Relevant only if Allow File Uploads is checked. Maximalt antal byte som en överförd bildfil kan ha. Standardvärdet är 2097152** **(2 MB).

* **Tillåt kopplade svar** Om det här alternativet är markerat tillåter du svar på kommentarer som publicerats i ämnet. Standard är avmarkerat.

* **Tillåt röstning** Om det här alternativet är markerat inkluderar du röstfunktionen med ett ämne. Standard är avmarkerat.

* **Tillåt användare att ta bort kommentarer och ämnen** Tillåt medlemmar att ta bort kommentarer och ämnen som de har skickat in om de är markerade. Standard är avmarkerat.

* **Visa vägbeskrivningar** Om det här alternativet är markerat visas vägbeskrivningar av navigeringsinformation på ämnessidor. Standard är markerat.

* **Visa emblem** Om det här alternativet är markerat visar du [märken](/help/communities/implementing-scoring.md) som tagits emot och tilldelats av en medlem i ett blogginlägg. Standard är avmarkerat.

* **Tillåt behöriga medlemmar** Om det här alternativet är markerat tillåts endast behöriga medlemmar att skapa innehåll.

* **Tillåtna behöriga medlemmar**Lägg till behöriga medlemmar som kan skapa innehåll.
* **Blockera användargenererat innehåll i redigeringsläge** Om det är aktiverat blockerar användargenererat innehåll när redigering pågår i redigeringsläget.

* **Aktivera omnämnande** om det är aktiverat gör att registrerade communityanvändare kan identifiera andra registrerade medlemmar (med förnamn, efternamn, användarnamn) och tagga dem med den vanliga @user-name-syntaxen. De taggade användarna får meddelanden om sina omnämnanden.

* **Max Mentions** Begränsa det maximala antalet omnämnanden som tillåts i ett inlägg. Standardvärdet är 10.

* **Mönster** för användargränssnittets omnämnande Ange den tillåtna mönstersträngen till taggen (@mention) för den registrerade användaren i ett inlägg. Exempel `~{{familyName}}{{givenName}}`.

>[!NOTE]
>
>Det kan vara nödvändigt att kontrollera både `AllowThreaded Replies` och `Allow users to Delete Comments and Topics` aktivera kommentarer om ett ämne.

#### Fliken Användarmoderering {#user-moderation-tab}

Under fliken **Användarmoderering **anger du hur publicerade ämnen och svar (användargenererat innehåll) ska hanteras. Mer information finns i [Hantera användargenererat innehåll](/help/communities/moderate-ugc.md).

* **Neka inlägg** Om det här alternativet är markerat kan pålitliga medlemsmoderatorer neka inlägg och förhindra att posten visas på det offentliga forumet. Standard är avmarkerat.

* **Stäng/öppna ämnen** igen Om det här alternativet är markerat kan pålitliga medlemsmoderatorer stänga ett avsnitt för ytterligare redigeringar och kommentarer och även öppna ett avsnitt på nytt. Standard är avmarkerat.

* **Flytta ämnen** Om det är markerat tillåter du moderatorer på publiceringssidan att flytta ämnen. Standard är markerat.

* **Flagga inlägg** Om det är markerat kan medlemmar flagga andras ämnen eller kommentarer som olämpliga. Standard är avmarkerat.

* **Flagga orsakslista** Om det här alternativet är markerat kan medlemmarna välja, från en nedrullningsbar lista, orsaken till att ett ämne eller en kommentar flaggas som olämplig. Standard är avmarkerat.

* **Anledning till anpassad flagga** Om den är markerad kan medlemmar ange en egen orsak till att ett ämne eller en kommentar flaggas som olämplig. Standard är avmarkerat.

* **Moderationströskel** Ange hur många gånger ett ämne eller en kommentar måste flaggas av medlemmar innan moderatorerna meddelas. Standardvärdet är 1 (en gång).

* **Flaggningsgräns** Ange hur många gånger ett ämne eller en kommentar måste flaggas innan det döljs för den offentliga vyn. Om värdet är -1 döljs aldrig det flaggade ämnet eller kommentaren från den offentliga vyn. Annars måste talet vara större än eller lika med modereringströskeln. Standardvärdet är 5.

#### Fliken Taggfält {#tag-field-tab}

Under fliken **Taggfält** är de taggar som kan användas, om de tillåts under fliken **Inställningar **begränsade enligt de namnutrymmen som har valts.

* **Tillåtna** relevanta namnutrymmen om `Allow Tagging` är markerat under fliken **Inställningar **. De taggar som kan användas är begränsade till de inom de namnutrymmeskategorier som kontrolleras. Listan med namnutrymmen innehåller &quot;Standardtaggar&quot; (standardnamnutrymmet) och &quot;Inkludera alla taggar&quot;. Standardvärdet är inget markerat, vilket betyder att alla namnutrymmen är tillåtna.

* **Förslagsgräns** Ange antalet taggar som ska visas som ett förslag till medlemmen som publicerar i forumet. Standardvärdet är **-**1 (inga gränser).

#### Fliken Översättning {#translation-tab}

Om översättning är aktiverat för communitywebbplatsen kan översättning ställas in för att översätta hela ämnet eller valda inlägg på fliken **Translation **.

* **Översätt alla** Om det här alternativet är markerat översätts forumtråden till användarens önskade språk. Standard är avmarkerat.

#### Fliken Sorteringsinställningar {#sort-settings-tab}

Under fliken **Sorteringsinställningar **anger du hur de bokförda kommentarerna ska sorteras när de visas.

* **Sortera efter** Kontrollera alla tillåtna sorteringsval: `Newest, Oldest, Last Updated, Most Viewed, Most Active, Most Followed and Most Liked`. Standardvärdet är `Newest, Oldest, Last Updated`.

* **Ange som standard** Dra nedåt om du vill välja något av de markerade sorteringsalternativen som ska visas som standard. Standardvärdet är `Newest`.

* **Välj Tidsalternativ för sortering** i listrutan Analytics (Analyssortering) för att välja ett av `All, Last 24 Hours, Last 7 Days, Last 30 Days`. Standardvärdet är `All`.

### Additional Information {#additional-information}

Mer information finns på sidan [Forum Essentials](/help/communities/essentials-forum.md) för utvecklare.

Mer information om moderering av publicerade ämnen och kommentarer finns i [Hantera användargenererat innehåll](/help/communities/moderate-ugc.md).

Information om hur du taggar publicerade ämnen och kommentarer finns i [Tagga användargenererat innehåll](/help/communities/tag-ugc.md).

Översättning av publicerade ämnen och kommentarer finns i [Översätta användargenererat innehåll](/help/communities/translate-ugc.md).
