---
title: Använda granskningar och granskningar - sammanfattning (visning)
description: Lär dig hur du lägger till komponenterna Granska och Granska sammanfattning på en sida.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
exl-id: 170414a6-c40b-4ad2-9294-7c2266850c3d
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '1210'
ht-degree: 0%

---

# Använda granskningar och granskningar - sammanfattning (visning) {#using-reviews-and-reviews-summary-display}

Komponenten `Reviews` är en sammansättning av [kommentarer](comments.md) och [klassificeringskomponenter](rating.md) som är klara att användas.

Komponenten `Reviews Summary (Display)` innehåller en sammanfattning av en aktiv eller stängd instans av en `Reviews`-komponent som kan visas någon annanstans på webbplatsen.

>[!NOTE]
>
>Anonym publicering av en granskning stöds inte. Besökarna måste registrera sig (bli medlem) och logga in för att kunna delta. Den inloggade besökaren kan uppdatera sin granskning när som helst.

## Lägga till en granskning på en sida {#adding-a-review-to-a-page}

Om du vill lägga till en `Reviews`-komponent på en sida i redigeringsläge använder du komponentwebbläsaren för att leta reda på `Communities / Reviews` och dra den till rätt plats på en sida, till exempel i förhållande till funktionen som användarna ska granska.

Mer information finns på [Grunderna för communitykomponenter](basics.md).

När de [nödvändiga klientbiblioteken](reviews-basics.md#essentials-for-client-side) inkluderas visas `Reviews`-komponenten på det här sättet.

![create-review](assets/create-review.png)

## Konfigurera granskningar {#configuring-reviews}

Markera den monterade `Reviews`-komponenten så att du kan komma åt och markera ikonen `Configure` som öppnar redigeringsdialogrutan.

![configure-new](assets/configure-new.png)

Under fliken **[!UICONTROL Allowed Ratings]** anger du den fullständiga listan över klassificeringar som ska visas för medlemmarna. Den första graderingen ska vara en generell/generell gradering, eftersom det är graderingen som ger den genomsnittliga graderingen för komponenten `Review Summary (Display)`. De två följande klassificeringarna i standardkonfigurationen bör ha en annan rubrik än &quot;Undergrupp 1&quot; eller &quot;Undergrupp 2&quot;.

![tillåten klassificering](assets/configure-review1.png)

* **[!UICONTROL Allowed Ratings]**

  En lista med klassificeringar som en medlem kan välja från.

  Använd uppilen, nedpilen och borttagningsknapparna för att ändra de synliga markeringarna.

  Klicka på **[!UICONTROL Add Item]** om du vill lägga till ett annat klassificeringsalternativ.

Under fliken **[!UICONTROL Required Ratings]** anger du objekt från listan med **[!UICONTROL Allowed Ratings]** som krävs för omdömen igen. Om ett objekt bara anges på fliken Tillåtna klassificeringar kan det lämnas omarkerat när medlemmen skickar in det.

På webbplatsen markeras nödvändiga klassificeringar med en asterisk. Om ett objekt är obligatoriskt och inte markerat visas ett meddelande för medlemmen och överföringen nekas tills alla nödvändiga klassificeringar har markerats.

![obligatorisk klassificering](assets/configure-review2.png)

* **[!UICONTROL Required Ratings]**

  En delmängd av tillåtna klassificeringar, som anger vilka klassificeringar som krävs.

  Använd uppilen, nedpilen och borttagningsknapparna för att ändra de synliga markeringarna.

  Klicka på **[!UICONTROL Add Item]** om du vill lägga till ett annat svarsalternativ.

>[!NOTE]
>
>Om ett objekt anges på fliken **[!UICONTROL Required Ratings]** som inte anges på fliken **[!UICONTROL Allowed Ratings]**, inkluderas det inte i objekten som ska värderas.

Ange hur granskningar ska hanteras på fliken **[!UICONTROL Reviews]**.

![recensioner](assets/configure-review3.png)

* **[!UICONTROL Allow Replies]**

  Om det här alternativet är markerat tillåts svar på granskningar. Standard är avmarkerat.

* **[!UICONTROL Closed]**

  Om det här alternativet är markerat stängs granskningen av nya granskningar och svar. Standard är avmarkerat.

* **[!UICONTROL Allow File Uploads]**

  Om det här alternativet är markerat tillåter du att bifogade filer överförs för granskningen. Standard är avmarkerat.

* **Maximal filstorlek**

  Endast relevant om **[!UICONTROL Allow File Uploads]** är markerat. Det här fältet begränsar storleken (i byte) på en överförd fil. Standardvärdet är 10 MB.

* **[!UICONTROL Max Message Length]**

  Maximalt antal tecken som kan anges i textrutan. Standardvärdet är 4 096 tecken.

* **[!UICONTROL Allowed File Types]**

  Endast relevant om **[!UICONTROL Allow File Uploads]** är markerat. En kommaavgränsad lista med filtillägg med punktavgränsaren. Exempel: .jpg, .jpeg, .png, .doc, .docx, .pdf. Om någon filtyp anges tillåts inte de som inte anges. Ingen standard har angetts så att alla filtyper tillåts.

* **[!UICONTROL Rich Text Editor]**

  Om det här alternativet är markerat kan inlägg infogas med markeringar. Standard är avmarkerat.

* **[!UICONTROL Allow Voting]**

  Inkludera röstfunktionen för ett ämne om det är markerat. Standard är avmarkerat.

Ange hur de publicerade granskningarna ska hanteras på fliken **[!UICONTROL User Moderation]**. Mer information finns i [Moderating User Generated Content](moderate-ugc.md).

![användarmoderering](assets/configure-review4.png)

* **[!UICONTROL Pre-Moderation]**

  Om du markerar det här alternativet måste granskningarna godkännas innan de visas på en publiceringsplats. Standard är avmarkerat.

* **[!UICONTROL Delete Reviews]**

  Om det här alternativet är markerat kan den medlem som publicerade granskningen ta bort den. Standard är avmarkerat.

* **[!UICONTROL Deny Reviews]**

  Tillåt moderatorerna att neka granskningar om de är markerade. Standard är avmarkerat.

* **[!UICONTROL Close / Reopen Reviews]**

  Om det här alternativet är markerat kan moderatorerna stänga och öppna granskningar igen. Standard är avmarkerat.

* **[!UICONTROL Flag Reviews]**

  Om det här alternativet är markerat kan medlemmarna flagga granskningar som olämpliga. Standard är avmarkerat.

* **[!UICONTROL Flag Reason List]**

  Om det här alternativet är markerat kan medlemmarna välja, från en nedrullningsbar lista, anledningen till att en granskning flaggas som olämplig. Standard är avmarkerat.

* **[!UICONTROL Custom Flag Reason]**

  Om det här alternativet är markerat kan medlemmarna ange en egen orsak till att en granskning har flaggats som olämplig. Standard är avmarkerat.

* **[!UICONTROL Moderation Threshold]**

  Ange hur många gånger en granskning måste flaggas av medlemmar innan moderatorerna meddelas. Standard är en gång (1).

* **[!UICONTROL Flagging Limit]**

  Ange hur många gånger en granskning måste flaggas innan den döljs för den offentliga vyn. Talet måste vara större än eller lika med **[!UICONTROL Moderation Threshold]**. Standardvärdet är 5.

### Lägga till en granskningssammanfattning (visning) på en sida {#adding-a-review-summary-display-to-a-page}

Om du vill lägga till en `Reviews Summary (Display)`-komponent på en sida i redigeringsläge letar du reda på komponenten

* `Communities / Reviews Summary (Display)`

Dra den till en plats på en sida där en sammanfattning av en aktiv eller stängd granskning ska visas.

Mer information finns på [Grunderna för communitykomponenter](basics.md).

När de [nödvändiga klientbiblioteken](reviews-basics.md#essentials-for-client-side) inkluderas visas `Reviews Summary (Display)`-komponenten på det här sättet.

![review-summary](assets/configure-review5.png)

>[!NOTE]
>
>&quot;Jämka&quot; motsvarar rösterna för den första posten på flikarna Tillåtna klassificeringar i den granskning som sammanfattas.

### Konfigurera sammanfattning av granskningar (visning) {#configuring-reviews-summary-display}

Markera den monterade `Reviews Summary (Display)`-komponenten så att du kan komma åt och markera ikonen `Configure` som öppnar redigeringsdialogrutan.

![konfigurera](assets/configure-new.png)

Under fliken **[!UICONTROL Review Summary]**

![review-summary](assets/configure-review6.png)

* `Review Path`

  Ange eller bläddra till den monterade instansen av `reviews`-komponenten så att du kan sammanfatta, om du till exempel har lagt till den på webbsidan för [Geometrixx Engage-webbplatsen &#x200B;](getting-started.md) , så blir sökvägen:

  `/content/sites/engage/en/page/jcr:content/content/primary/reviews`

* `Include histogram`

  Om du markerar det här alternativet visas ett stolpdiagram som anger hur många stjärngraderingar det finns i de sammanfattade granskningarna. Standard är avmarkerat.

### Ändra till en anpassad granskningstyp {#changing-to-a-custom-review-type}

Komponenten Reviews använder kommentarsystemet.

Genom att ändra kommentarsresurstypen genererar inte längre kommentarsystemet en instans av en kommentar med standardinställningen, utan en som har anpassats (utökats) av utvecklarna.

När de anpassade resurstyperna är kända anger du [designläge](../../help/sites-authoring/default-components-designmode.md) och dubbelklickar på den monterade `Comments` -komponenten för att öppna en dialogruta med en extra flik.

Under fliken **[!UICONTROL Resource Types]** anger du anpassad resourceType för nya instanser av komponenterna `Comments or Voting`:

![kommentarer-votering](assets/configure-review7.png)

* **[!UICONTROL Comment Resource Type]**

  Navigera till resourceType för en utökad `comment`-komponent (en kommentar) i /apps. Exempel: `/apps/social/commons/components/hbs/comments/comment`.

  Den här resursen identifierar den resourceType för den UGC som skapas när en besökare publicerar en kommentar.

* **[!UICONTROL Voting Resource Type]**

  Navigera till resourceType för en utökad `voting`-komponent i /apps. Exempel: `/apps/social/components/hbs/voting`.

  Den här resursen identifierar resurstypen för användargenererat innehåll som skapas när en besökare publicerar en röst.

* **[!UICONTROL Comment System Resource Type]**

  Navigera till resourceType för en utökad `comments`-komponent (kommentarsystemet) i /apps. Lämna tomt om inte sidmallen [dynamiskt inkluderar](scf.md#add-or-include-a-communities-component) kommentarsystemet i det underliggande skriptet, i stället för att läggas till på sidan som en resurs (kommentarsnod). Läs mer om [`{{include}}`-hjälpen](handlebars-helpers.md#include).

## Site Visitor Experience {#site-visitor-experience}

### Styrelsemedlemmar och administratörer {#moderators-and-administrators}

När den inloggade användaren har moderator- eller administratörsbehörighet kan de utföra de modereringsåtgärder som tillåts av komponentens konfiguration, oavsett vem som skapade granskningen.

### Medlemmar {#members}

När besökaren är inloggad, beroende på konfigurationen, kan de:

* Post - en ny recension
* Redigera en egen granskning
* Ta bort en egen granskning
* Flagga andras kommentarer

Endast ett omdöme per medlem tillåts. Medlemmen kan när som helst ändra sin klassificering.

### Anonym {#anonymous}

Besökare som inte är inloggade kan endast läsa publicerade granskningar, översätta dem om de stöds, men kan inte lägga till en klassificering eller en granskning eller flagga andras granskningskommentarer.

## Ytterligare information {#additional-information}

Mer information finns på sidan [Granska viktiga](reviews-basics.md) för utvecklare.

Mer information om moderering av publicerade kommentarer finns i [Moderating User Generated Content](moderate-ugc.md) (Moderating User Generated Content).

Mer information om översättning av bokförda kommentarer finns i [Översätta användargenererat innehåll](translate-ugc.md).
