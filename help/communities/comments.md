---
title: Använda kommentarer
seo-title: Använda kommentarer
description: Med kommentarsfunktionen kan besökare på den inloggade webbplatsen dela med sig av sina åsikter och kunskaper
seo-description: Med kommentarsfunktionen kan besökare på den inloggade webbplatsen dela med sig av sina åsikter och kunskaper
uuid: 40acd962-846c-483c-b789-aab3a7d2b31b
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 216cfb3e-777e-4773-afba-749debdca000
docset: aem65
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65

---


# Använda kommentarer{#using-comments}

## Introduktion {#introduction}

Kommentarsfunktionen används för att låta besökare (medlemmar) på den inloggade webbplatsen dela med sig av sina åsikter och kunskaper om innehållet på webbplatsen. Den här funktionen finns ofta redan i andra funktioner, men kan läggas till på alla webbplatser.

Dokumentet beskriver:

* lägga `Comments`till på en sida.
* konfigurationsinställningar för `Comments`komponenten.

>[!NOTE]
>
>Anonym publicering av en kommentar stöds inte. Besökare måste registrera sig (bli medlem) och logga in för att kunna delta.

### Lägga till kommentarer på en sida {#adding-comments-to-a-page}

Om du vill lägga till en `Comments`komponent på en sida i redigeringsläge använder du komponentwebbläsaren för att leta reda på

* `Communities / Comments`

och dra den till rätt plats på en sida, t.ex. en position i förhållande till funktionen som användarna kan kommentera på, eller helt enkelt längst ned på sidan.

Mer information finns i Grunderna för [communitykomponenter](/help/communities/basics.md).

När de [nödvändiga klientbiblioteken](/help/communities/essentials-comments.md#essentials-for-client-side) inkluderas visas `Comments`komponenten på det här sättet.

![chlimage_1-143](assets/chlimage_1-143.png)

>[!NOTE]
>
>Det får bara finnas en `Comments`komponent på en sida. Observera att flera communityfunktioner redan innehåller kommentarer, t.ex. en blogg, kalender, forum, QnA och recensioner.

### Konfigurera kommentarer {#configuring-comments}

Markera den monterade `Comments` komponent som du vill öppna och välj den `Configure` ikon som öppnar redigeringsdialogrutan.

![konfigurera](assets/configure.png) inställningar för ikonkommentarer ![](assets/commentssettings.png)

#### Fliken Kommentarer {#comments-tab}

Under fliken **Kommentarer** anger du hur besökare ska ange kommentarer.

* **Tillåt svar**

   Om det här alternativet är markerat kan medlemmarna svara på befintliga kommentarer. Standard är avmarkerat.

* **Kommentarer per sida**

   Begränsar antalet kommentarer som visas per sida och antalet svar som visas. Standardvärdet är 10.

* **Tillåt filöverföringar**

   Om du markerar det här alternativet visas textrutan för alternativet att överföra en fil. Standard är avmarkerat.

* **Maximal filstorlek**

   Endast relevant om Tillåt filöverföringar är markerat. Det här värdet begränsar storleken på den överförda filen. Standardgränsen är 10 MB.

* **Maximal meddelandelängd**

   Maximalt antal tecken som kan anges i textrutan. Standardvärdet är 4 096 tecken.

* **Tillåtna filtyper**

   Endast relevant om Tillåt filöverföringar är markerat. En kommaavgränsad lista med filnamnstillägg med punktavgränsaren. Till exempel: .jpg, .jpeg, .png, .doc, .docx, .pdf. Om någon filtyp anges tillåts inte den som inte anges. Standard är inte angivet så att** **alla filtyper tillåts.

* **RTF-redigerare**

   Om det här alternativet är markerat infogas kommentarerna med kod. Standard är avmarkerat.

* **Tillåt röstning**

   Om det här alternativet är markerat visas textrutan med alternativet att rösta upp eller ned. Standard är avmarkerat.

* **Tillåt följande**

   Om det här alternativet är markerat kan medlemmarna följa kommentarerna. Standard är avmarkerat.

* **Visa emblem**

   Om du markerar det här alternativet tillåts visning av färdiga och tilldelade märken. Standard är avmarkerat.

#### Fliken Användarmoderering {#user-moderation-tab}

Under fliken **Användarmoderering **anger du hur de skickade kommentarerna ska hanteras. Mer information finns i [Hantera användargenererat innehåll](/help/communities/moderate-ugc.md).

* **Förhandsmoderering** Om det här alternativet är markerat måste kommentarerna godkännas innan de visas på en publiceringsplats. Standard är avmarkerat.

* **Ta bort kommentarer**

   Om det här alternativet är markerat kan den medlem som publicerade kommentaren ta bort den. Standard är avmarkerat.

* **Neka kommentarer**

   Om det här alternativet är markerat tillåter du moderatorerna att neka kommentarer. Standard är avmarkerat.

* **Stäng/öppna kommentarer igen**

   Om det här alternativet är markerat kan moderatorerna stänga och öppna kommentarerna igen. Standard är avmarkerat.

* **Flagga kommentarer**

   Om alternativet är markerat kan medlemmarna flagga kommentarer som olämpliga. Standard är avmarkerat.

* **Flaggorsakslista**

   Om det här alternativet är markerat kan medlemmarna i en nedrullningsbar lista välja orsaken till att en kommentar flaggas som olämplig. Standard är avmarkerat.

* **Anledning till anpassad flagga**

   Om det här alternativet är markerat kan medlemmarna ange en egen orsak till att en kommentar flaggas som olämplig. Standard är avmarkerat.

* **Modereringströskel**

   Ange hur många gånger en kommentar måste flaggas av medlemmarna innan moderatorerna meddelas. Standard är en gång (1).

* **Flaggningsgräns**

   Ange hur många gånger en kommentar måste flaggas innan den döljs för den offentliga vyn. Talet måste vara större än eller lika med **modereringströskeln**. Standardvärdet är 5.

#### Fliken Sorteringsinställningar {#sort-settings-tab}

Under fliken **Sorteringsinställningar **anger du hur de bokförda kommentarerna ska sorteras när de visas.

* **Sorteringsfält**

   Dra nedåt för att välja ett av `Newest, Oldest, Last Updated, Most Viewed, Most Active, Most Followed`eller `Most Liked`.

* **Sorteringsordning**

   Dra nedåt för att välja ett av `Ascending` eller `Descending`.

### Ändra till en anpassad kommentarstyp {#changing-to-a-custom-comment-type}

Genom att ändra kommentarsresurstypen genererar inte längre kommentarsystemet en instans av en kommentar med standardinställningen, utan en som har anpassats (utökats) av utvecklarna.

När du känner till de anpassade resurstyperna anger du [designläge](/help/sites-authoring/default-components-designmode.md) och dubbelklickar på den monterade `Comments` komponenten för att öppna en dialogruta med en extra flik.

Under fliken **Resurstyper **anger du anpassad resourceType för nya instanser av `Comments or Voting`komponenterna:

![chlimage_1-144](assets/chlimage_1-144.png)

* **Resurstyp för kommentar**

   Navigera till resourceType för en utökad `comment`komponent (en kommentar) i /apps. Exempel, `/apps/social/commons/components/hbs/comments/comment`

   Den här resursen identifierar den resourceType för den UGC som skapas när en besökare publicerar en kommentar.

* **Typ av röstningsresurs**

   Navigera till resourceType för en utökad `voting`komponent i /apps. Exempel, `/apps/social/components/hbs/voting`

   Den här resursen identifierar resurstypen för användargenererat innehåll som skapas när en besökare publicerar en röst.

* **Resurstyp för kommentarsystem**

   Navigera till resourceType för en utökad `comments`komponent (kommentarsystemet) i /apps. Lämna tomt om inte sidmallen [dynamiskt inkluderar](/help/communities/scf.md#add-or-include-a-communities-component) kommentarsystemet i det underliggande skriptet i stället för att läggas till på sidan som en resurs (kommentarsnod). Läs mer om [{{include}}-hjälpen](/help/communities/handlebars-helpers.md#include).

### Site Visitor Experience {#site-visitor-experience}

#### Styrelsemedlemmar och administratörer {#moderators-and-administrators}

När den inloggade användaren har moderator- eller administratörsbehörighet kan de utföra de modereringsåtgärder som tillåts av komponentens konfiguration, oavsett vem som skapade kommentaren.

#### Medlemmar {#members}

När besökaren är inloggad, beroende på konfigurationen, kan de

* publicera en ny kommentar
* redigera sin egen kommentar
* ta bort sin egen kommentar
* flagga andras kommentarer

#### Anonym {#anonymous}

Besökare som inte är inloggade kan endast läsa publicerade kommentarer, översätta dem om de stöds, men kan inte lägga till en kommentar eller flagga andras kommentarer.

### Additional Information {#additional-information}

Mer information finns på sidan [Comments Essentials](/help/communities/essentials-comments.md) för utvecklare.

Mer information om moderering av publicerade kommentarer finns i [Hantera användargenererat innehåll](/help/communities/moderate-ugc.md).

Information om översättning av bokförda kommentarer finns i [Översätta användargenererat innehåll](/help/communities/translate-ugc.md).
