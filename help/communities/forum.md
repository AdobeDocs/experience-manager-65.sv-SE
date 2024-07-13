---
title: Forumfunktion
description: Lär dig hur du lägger till och konfigurerar en forumfunktion som ger ett område där inloggade communitymedlemmar kan skapa, visa, följa, söka eller svara på ämnen.
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
docset: aem65
exl-id: 2b1a4917-9db6-436a-a5fd-c102fe41fb9d
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '1233'
ht-degree: 0%

---

# Forumfunktion{#forum-feature}

## Introduktion {#introduction}

I forumfunktionen finns ett område där besökare (community-medlemmar) kan logga in på webbplatsen i Publish-miljön:

* Skapa ämnen
* Visa och svara på ämnen
* Följ ett avsnitt
* Sök i ett forum
* Hjälp till att moderera foruminnehållet
* Flytta forumämnen mellan sidor

I det här avsnittet av dokumentationen beskrivs:

* Lägga till forumfunktionen på en AEM webbplats.
* Konfigurationsinställningar för komponenten `Forum`.

### Lägga till ett forum på en sida {#adding-a-forum-to-a-page}

Om du vill lägga till en `Forum`-komponent på en sida i redigeringsläge använder du komponentwebbläsaren för att hitta

* `Communities / Forum`

Och dra den till rätt plats på en sida där forumet ska visas.

Mer information finns på [Grunderna för communitykomponenter](/help/communities/basics.md).

När de [nödvändiga klientbiblioteken](/help/communities/essentials-forum.md#essentials-for-client-side) inkluderas visas `Forum`-komponenten så här:

![forumkomponent](assets/forum-component.png)

### Konfigurera ett forum {#configuring-a-forum}

Markera den monterade `Forum`-komponenten så att du kan komma åt och markera ikonen `Configure` som öppnar redigeringsdialogrutan.

![configure-new](assets/configure-new.png)

![forum-config](assets/forum-config.png)

#### Fliken Inställningar {#settings-tab}

Ange inställningar för ämnen och svar på fliken **Inställningar**:

* **Tillåt miniatyrbild för bifogad fil**

  Om du markerar det här alternativet skapas en miniatyrbild av den bifogade bilden.

* **Maximal storlek för miniatyrbildsanslutning**

  Maximal storlek (i pixlar) för miniatyrbilden för den bifogade filen. Standardvärdet är 800 x 800.

* **Minsta bildstorlek för miniatyrbild**
* **Maximal miniatyrstorlek**

  Maximal storlek (i pixlar) för miniatyrbilden för textbunden bild. Standardvärdet är 800 x 800.

* **Ämnen per sida**

  Definierar antalet ämnen/inlägg som visas per sida. Standardvärdet är 10.

* **Modererad**

  Om det här alternativet är markerat måste publicering av ämnen och kommentarer godkännas innan de kan visas på en publiceringsplats. Standard är avmarkerat.

* **Stängd**

  Om det här alternativet är markerat stängs forumet för nya ämnen och kommentarer. Standard är avmarkerat.

* **RTF-redigerare**

  Om det här alternativet är markerat kan du skriva in ämnen och kommentarer med markeringar. Standard är avmarkerat.

* **Tillåt taggning**

  Om det här alternativet är markerat kan medlemmar lägga till taggetiketter i sina inlägg (se fliken **Taggfält**). Standard är avmarkerat.

* **Tillåt filöverföringar**

  Om du markerar det här alternativet kan du tillåta att bifogade filer läggs till i ämnet eller kommentaren. Standard är avmarkerat.

* **Tillåt följande**

  Om du markerar det här alternativet inkluderas följande funktion för foruminlägg, som gör att medlemmar kan [meddelas](/help/communities/notifications.md) om nya inlägg. Standard är avmarkerat.

* **Tillåt fästa**

  Om det här alternativet är markerat kan forumämnen fästas överst i ämneslistan. Standard är avmarkerat.

* **Tillåt aktuellt innehåll**

  Om det här alternativet är markerat går det att identifiera idén som [aktuellt innehåll](/help/communities/featured.md). Standard är avmarkerat.

* **Tillåt e-postprenumerationer**

  Om det här alternativet är markerat kan medlemmar meddelas om nya inlägg via e-post ([prenumeration](/help/communities/subscriptions.md)). Kräver att `Allow Following` kontrolleras och att [e-post konfigureras](/help/communities/email.md). Standard är avmarkerat.

* **Maximal filstorlek**

  Endast relevant om `Allow File Uploads` är markerat. Det här fältet begränsar storleken (i byte) på en överförd fil. Standardvärdet är 104857600 (10 MB).

* **Tillåtna filtyper**

  Endast relevant om `Allow File Uploads` är markerat. En kommaavgränsad lista med filtillägg med punktavgränsaren. Exempel: .jpg, .jpeg, .png, .doc, .docx, .pdf. Om någon filtyp har angetts kan de inte överföras. Ingen standard har angetts så att alla filtyper tillåts.

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

  Om det här alternativet är markerat visas intjänade och tilldelade [emblem](/help/communities/implementing-scoring.md) med en medlems blogginlägg. Standard är avmarkerat.

* **Tillåt behöriga medlemmar**

  Om det här alternativet är markerat kan endast behöriga medlemmar skapa innehåll.

* **Tillåtna behöriga medlemmar**

  Lägg till de behöriga medlemmar som har behörighet att skapa innehåll.

* **Blockera användargenererat innehåll i redigeringsläge för författare**

  Om det här alternativet är aktiverat blockeras användargenererat innehåll när du redigerar i redigeringsläge.

* **Aktivera omnämnande**

  Om det här alternativet är aktiverat kan registrerade communityanvändare identifiera andra registrerade medlemmar (med förnamn, efternamn, användarnamn) och tagga dem med den vanliga @användarnamnssyntaxen. De taggade användarna får meddelanden om sina omnämnanden.

* **Max antal omnämnanden**

  Begränsa det maximala antalet omnämnanden som tillåts i ett inlägg. Standardvärdet är 10.

* **Mönster för gränssnittets omnämnande**

  Ange den tillåtna mönstersträngen för att tagga (@mention) den registrerade användaren i ett inlägg. Exempel: `~{{familyName}}{{givenName}}`.

>[!NOTE]
>
>Du kan behöva kontrollera både `AllowThreaded Replies` och `Allow users to Delete Comments and Topics` för att kunna aktivera kommentarer om ett ämne.

#### Fliken Användarmoderering {#user-moderation-tab}

Under fliken **Användarmoderering** anger du hur publicerade ämnen och svar (användargenererat innehåll) ska hanteras. Mer information finns i [Moderating User-Generated Content](/help/communities/moderate-ugc.md).

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

Under fliken **Taggfält** är de taggar som kan användas, om de tillåts under fliken **Inställningar** , begränsade enligt de valda namnutrymmena.

* **Tillåtna namnutrymmen**

  Relevant om `Allow Tagging` är markerat under fliken **Inställningar**. De taggar som kan användas är begränsade till de inom de namnutrymmeskategorier som kontrolleras. Listan med namnutrymmen innehåller&quot;Standardtaggar&quot; (standardnamnutrymmet) och&quot;Inkludera alla taggar&quot;. Standardvärdet är inget markerat, vilket betyder att alla namnutrymmen är tillåtna.

* **Förslagsgräns**

  Ange antalet taggar som ska visas som ett förslag till medlemmens inlägg i forumet. Standardvärdet är **-**1 (inga gränser).

#### Fliken Översättning {#translation-tab}

Om översättning är aktiverat för communitywebbplatsen kan översättning ställas in för att översätta hela ämnet eller valda inlägg på fliken **Översättning**.

* **Översätt alla**

  Om det här alternativet är markerat översätts forumtråden till användarens önskade språk. Standard är avmarkerat.

#### Fliken Sorteringsinställningar {#sort-settings-tab}

Under fliken **Sorteringsinställningar** anger du hur de bokförda kommentarerna ska sorteras när de visas.

* **Sortera efter**

  Kontrollera alla tillåtna sorteringsval: `Newest, Oldest, Last Updated, Most Viewed, Most Active, Most Followed and Most Liked`. Standardvärdet är `Newest, Oldest, Last Updated`.

* **Ange som standard**

  Dra nedåt om du vill välja något av de markerade sorteringsalternativen som ska visas som standard. Standardvärdet är `Newest`.

* **Välj tidsalternativ för sortering av analyser**

  Dra ned för att välja ett av följande alternativ: `All, Last 24 Hours, Last 7 Days, Last 30 Days`.

  Standardvärdet är `All`.

### Ytterligare information {#additional-information}

Mer information finns på sidan [Forum Essentials](/help/communities/essentials-forum.md) för utvecklare.

moderering av publicerade ämnen och kommentarer finns i [Moderering av användargenererat innehåll](/help/communities/moderate-ugc.md).

Information om hur du taggar publicerade ämnen och kommentarer finns i [Tagga användargenererat innehåll](/help/communities/tag-ugc.md).

Översättning av publicerade ämnen och kommentarer finns i [Översätta användargenererat innehåll](/help/communities/translate-ugc.md).
