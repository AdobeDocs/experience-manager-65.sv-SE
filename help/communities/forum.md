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
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '1226'
ht-degree: 0%

---


# Forumfunktion{#forum-feature}

## Introduktion {#introduction}

Forumfunktionen tillhandahåller ett område där besökare (community-medlemmar) som loggat in kan besöka webbplatsen i publiceringsmiljön:

* Skapa nya ämnen
* Visa och svara på ämnen
* Följ ett avsnitt
* Sök i ett forum
* Hjälp till att moderera foruminnehållet
* Flytta forumämnen från en sida till en annan

I det här avsnittet av dokumentationen beskrivs:

* Lägga till forumfunktionen på en AEM webbplats.
* Konfigurationsinställningar för `Forum` komponenten.

### Lägga till ett forum på en sida {#adding-a-forum-to-a-page}

Om du vill lägga till en `Forum` komponent på en sida i redigeringsläge använder du komponentwebbläsaren för att leta reda på

* `Communities / Forum`

och dra den till rätt plats på en sida där forumet ska visas.

Mer information finns i Grunderna för [communitykomponenter](/help/communities/basics.md).

När de [nödvändiga klientbiblioteken](/help/communities/essentials-forum.md#essentials-for-client-side) inkluderas visas `Forum` komponenten så här:

![chlimage_1-60](assets/chlimage_1-60.png)

### Konfigurera ett forum {#configuring-a-forum}

Markera den monterade `Forum` komponent som du vill öppna och välj den `Configure` ikon som öppnar redigeringsdialogrutan.

![chlimage_1-61](assets/chlimage_1-61.png)

![forum-config](assets/forum-config.png)

#### Fliken Inställningar {#settings-tab}

Ange inställningar för ämnen och svar på fliken **Inställningar** :

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

   Om det här alternativet är markerat måste publicering av ämnen och kommentarer godkännas innan de visas på en publiceringsplats. Standard är avmarkerat.

* **Stängd**

   Om det här alternativet är markerat stängs forumet för nya ämnen och kommentarer. Standard är avmarkerat.

* **RTF-redigerare**

   Om det här alternativet är markerat kan du skriva in ämnen och kommentarer med markeringar. Standard är avmarkerat.

* **Tillåt taggning**

   Om det här alternativet är markerat kan medlemmar lägga till taggetiketter i sina inlägg (se fliken **Taggfält** ). Standard är avmarkerat.

* **Tillåt filöverföringar**

   Om du markerar det här alternativet kan du tillåta att bifogade filer läggs till i ämnet eller kommentaren. Standard är avmarkerat.

* **Tillåt följande**

   Om det här alternativet är markerat kan du inkludera följande funktion för foruminlägg, som gör att medlemmar kan [informeras](/help/communities/notifications.md) om nya inlägg. Standard är avmarkerat.

* **Tillåt fästa**

   Om det här alternativet är markerat kan forumämnen fästas överst i ämneslistan. Standard är avmarkerat.

* **Tillåt innehåll**

   Om du markerar det här alternativet kan idén identifieras som [aktuellt innehåll](/help/communities/featured.md). Standard är avmarkerat.

* **Tillåt e-postprenumerationer**

   Om det här alternativet är markerat kan medlemmar meddelas om nya inlägg via e-post ([prenumeration](/help/communities/subscriptions.md)). Kräver `Allow Following` att kontrolleras och att [e-post konfigureras](/help/communities/email.md). Standard är avmarkerat.

* **Maximal filstorlek**

   Relevant endast om `Allow File Uploads` är markerat. Det här fältet begränsar storleken (i byte) på en överförd fil. Standardvärdet är 104857600 (10 MB).

* **Tillåtna filtyper**

   Relevant endast om `Allow File Uploads` är markerat. En kommaavgränsad lista med filtillägg med&quot;punktavgränsaren&quot;. Till exempel: .jpg, .jpeg, .png, .doc, .docx, .pdf. Om någon filtyp har angetts kan de som inte har angetts inte överföras. Ingen standard har angetts så att alla filtyper tillåts.

* **Max Attach Image File Size** Relevant only if Allow File Uploads is checked. Maximalt antal byte som en överförd bildfil kan ha. Standardvärdet är 2097152 (2 MB).

* **Tillåt kopplade svar**

   Om det här alternativet är markerat tillåts svar på kommentarer som har publicerats i ämnet. Standard är avmarkerat.

* **Tillåt röstning**

   Inkludera röstfunktionen med ett ämne om det är markerat. Standard är avmarkerat.

* **Tillåt användare att ta bort kommentarer och ämnen**

   Om det här alternativet är markerat kan medlemmarna ta bort kommentarer och ämnen som de har skickat in. Standard är avmarkerat.

* **Visa vägbeskrivningar**

   Om du markerar det här alternativet visas navigeringsbeskrivningar på ämnessidor. Standard är markerat.

* **Visa emblem**

   Om det här alternativet är markerat visas färdiga och tilldelade [märken](/help/communities/implementing-scoring.md) med en medlems blogginlägg. Standard är avmarkerat.

* **Tillåt behöriga medlemmar**

   Om det här alternativet är markerat kan endast behöriga medlemmar skapa innehåll.

* **Tillåtna behöriga medlemmar**

   Lägg till de behöriga medlemmar som har behörighet att skapa innehåll.

* **Blockera användargenererat innehåll i redigeringsläge för författare**

   Om det här alternativet är aktiverat blockeras användargenererat innehåll när redigering i redigeringsläge.

* **Aktivera omnämnande**

   Om det här alternativet är aktiverat kan registrerade communityanvändare identifiera andra registrerade medlemmar (med förnamn, efternamn, användarnamn) och tagga dem med den vanliga @användarnamnssyntaxen. De taggade användarna får meddelanden om sina omnämnanden.

* **Max. omnämnanden**

   Begränsa det maximala antalet omnämnanden som tillåts i ett inlägg. Standardvärdet är 10.

* **Mönster för användargränssnittets omnämnande**

   Ange den tillåtna mönstersträngen för att tagga (@mention) den registrerade användaren i ett inlägg. Till exempel `~{{familyName}}{{givenName}}`.

>[!NOTE]
>
>Det kan vara nödvändigt att kontrollera både `AllowThreaded Replies` och `Allow users to Delete Comments and Topics` aktivera kommentarer om ett ämne.

#### Fliken Användarmoderering {#user-moderation-tab}

På fliken **Användarmoderering** anger du hur publicerade ämnen och svar (användargenererat innehåll) ska hanteras. Mer information finns i [Hantera användargenererat innehåll](/help/communities/moderate-ugc.md).

* **Neka inlägg**

   Om det här alternativet är markerat kan pålitliga medlemsmoderatorer neka inlägg och förhindra att posten visas på det offentliga forumet. Standard är avmarkerat.

* **Stäng/öppna avsnitt igen**

   Om det här alternativet är markerat kan pålitliga medlemsmoderatorer stänga ett ämne för ytterligare redigeringar och kommentarer, och kan även öppna ett avsnitt på nytt. Standard är avmarkerat.

* **Flytta ämnen**

   Om det här alternativet är markerat kan du tillåta moderatorer på publiceringssidan att flytta ämnen. Standard är markerat.

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

Under fliken **Tagg** begränsas de taggar som kan användas, om de tillåts under fliken **Inställningar** , enligt de namnutrymmen som valts.

* **Tillåtna namnutrymmen**

   Relevant om `Allow Tagging` är markerat under fliken **Inställningar** . De taggar som kan användas är begränsade till de inom de namnutrymmeskategorier som kontrolleras. Listan med namnutrymmen innehåller &quot;Standardtaggar&quot; (standardnamnutrymmet) och &quot;Inkludera alla taggar&quot;. Standardvärdet är inget markerat, vilket betyder att alla namnutrymmen är tillåtna.

* **Förslagsgräns**

   Ange antalet taggar som ska visas som ett förslag till medlemmens inlägg i forumet. Standardvärdet är **-**1 (inga gränser).

#### Fliken Översättning {#translation-tab}

Om översättning är aktiverat för communitywebbplatsen på fliken **Översättning** kan översättning ställas in för att översätta hela ämnet eller valda inlägg.

* **Översätt alla**

   Om det här alternativet är markerat översätts forumtråden till användarens önskade språk. Standard är avmarkerat.

#### Fliken Sorteringsinställningar {#sort-settings-tab}

På fliken **Sorteringsinställningar** anger du hur de skickade kommentarerna ska sorteras när de visas.

* **Sortera efter**

   Kontrollera alla tillåtna sorteringsval: `Newest, Oldest, Last Updated, Most Viewed, Most Active, Most Followed and Most Liked`. Standardvärdet är `Newest, Oldest, Last Updated`.

* **Ange som standard**

   Dra nedåt om du vill välja något av de markerade sorteringsalternativen som ska visas som standard. Standardvärdet är `Newest`.

* **Välj tidsalternativ för Analytics-sortering**

   Dra nedåt för att välja något av följande alternativ: `All, Last 24 Hours, Last 7 Days, Last 30 Days`.

   Standardvärdet är `All`.

### Additional Information {#additional-information}

Mer information finns på sidan [Forum Essentials](/help/communities/essentials-forum.md) för utvecklare.

Mer information om moderering av publicerade ämnen och kommentarer finns i [Hantera användargenererat innehåll](/help/communities/moderate-ugc.md).

Information om hur du taggar publicerade ämnen och kommentarer finns i [Tagga användargenererat innehåll](/help/communities/tag-ugc.md).

Översättning av publicerade ämnen och kommentarer finns i [Översätta användargenererat innehåll](/help/communities/translate-ugc.md).
