---
title: Kalenderfunktion
description: Lär dig hur kalenderfunktionen tillhandahåller information om communityevent i ett kalenderformat.
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
docset: aem65
exl-id: c9b34b00-525d-4ca3-bd18-11bb7ce66787
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '1158'
ht-degree: 0%

---

# Kalenderfunktion {#calendar-feature}

## Introduktion {#introduction}

Kalenderfunktionen har stöd för att tillhandahålla information om communityevent i ett kalenderformat antingen för alla webbplatsbesökare eller endast för inloggade webbplatsbesökare (community-medlemmar), medan endast behöriga medlemmar kan lägga till händelser.

Detta avsnitt i dokumentationen beskriver

* Lägga till kalenderfunktionen på en AEM webbplats
* Konfigurationsinställningar för `Calendar`-komponenter

## Lägga till en kalender på en sida {#adding-a-calendar-to-a-page}

Om du vill lägga till en `Calendar`-komponent på en sida i redigeringsläge använder du komponentwebbläsaren för att hitta

* `Communities / Calendar`

Och dra den till rätt plats på en sida, till exempel i förhållande till funktionen som användarna kan granska.

Mer information finns på [Grunderna för communitykomponenter](/help/communities/basics.md).

När de [nödvändiga klientbiblioteken](/help/communities/calendar-basics-for-developers.md#essentials-for-client-side) inkluderas visas `Calendar`-komponenten på det här sättet.

![kalenderkomponent](assets/calendar-component.png)

### Konfigurerar kalender {#configuring-calendar}

Markera den monterade `Calendar`-komponenten så att du kan komma åt och markera ikonen `Configure` som öppnar redigeringsdialogrutan.

![konfigurera](assets/configure-new.png)

![configure-calendar](assets/configure-calendar1.png)

#### Fliken Inställningar {#settings-tab}

Under fliken **Inställningar** anger du om du vill tillåta att taggar tillämpas på kalenderposter.

* **Händelser per sida**

  Definierar antalet händelser som visas per sida. Standardvärdet är 10.

* **Modererad**

  Om det här alternativet är markerat måste publicering av kalenderhändelser och kommentarer godkännas innan de visas på en publiceringsplats. Standard är avmarkerat.

* **Stängd**

  Om du markerar det här alternativet stängs kalendern för nya händelseposter och kommentarer. Standard är avmarkerat.

* **RTF-redigerare**

  Om det här alternativet är markerat kan kalenderhändelser och kommentarer infogas med markeringar. Standard är markerat.

* **Tillåt taggning**

  Om det här alternativet är markerat tillåter du medlemmar att lägga till taggetiketter till de händelser som de skickar (se fliken **Taggfält**). Standard är markerat.

* **Tillåt filöverföringar**

  Om du markerar det här alternativet kan du tillåta att bifogade filer läggs till i en kalenderhändelse eller kommentar. Standard är markerat.

* **Tillåt följande**

  Om det här alternativet är markerat tillåter du medlemmar att följa händelser som har bokförts i kalendern. Standard är markerat.

* **Maximal filstorlek**

  Endast relevant om `Allow File Uploads` är markerat. Det här fältet begränsar storleken (i byte) på en överförd fil. Standardvärdet är 104857600 (10 MB).

* **Tillåtna filtyper**

  Endast relevant om `Allow File Uploads` är markerat. En kommaavgränsad lista med filtillägg med punktavgränsaren. Exempel: .jpg, .jpeg, .png, .doc, .docx, .pdf. Om någon filtyp har angetts kan de inte överföras. Ingen standard har angetts så att alla filtyper tillåts.

* **Maximal filstorlek för bifogad bild**

  Endast relevant om Tillåt filöverföringar är markerat. Maximalt antal byte som en överförd bildfil kan ha. Standardvärdet är 2097152** **(2 MB).

* **Tillåtna omslagsbildtyper**

  En kommaavgränsad lista över bildfilstillägg med punktavgränsaren. Standardvärdet är `.jpg,.jpeg,.png,.gif,.bmp`.

* **Tillåt kopplade svar**

  Om det här alternativet är markerat tillåts svar på kommentarer som har bokförts i kalenderhändelsen. Standard är markerat.

* **Tillåt användare att ta bort kommentarer och händelser**

  Om det här alternativet är markerat kan medlemmar ta bort kommentarer och kalenderhändelser som de har bokfört. Standard är markerat.

* **Tillåt röstning**

  Om du markerar det här alternativet inkluderas röstningsfunktionen med en kalenderhändelse. Standard är markerat.

* **Visa vägbeskrivningar**

  Visa vägbeskrivningar på händelsesidan. Standard är markerat.

* **Datumintervallfilter**

  Definierar antalet dagar som läggs till i det aktuella datumet för att beräkna Till-värdet för sidfiltret för kalenderhändelselistan. Standardvärdet är 30.

* **Tillåt aktuellt innehåll**

  Om det här alternativet är markerat går det att identifiera idén som [aktuellt innehåll](/help/communities/featured.md). Standard är avmarkerat.

Under fliken **Användarmoderering** anger du hur publicerade ämnen och svar (användargenererat innehåll) ska hanteras. Mer information finns i [Moderating User Generated Content](/help/communities/moderate-ugc.md).

#### Fliken Användarmoderering {#user-moderation-tab}

* **Neka inlägg**

  Om det här alternativet är markerat kan pålitliga medlemsmoderatorer neka inlägg och förhindra att posten visas på det offentliga forumet. Standard är markerat.

* **Stäng/öppna händelser igen**

  Om det här alternativet är markerat kan pålitliga medlemsmoderatorer stänga en händelse för ytterligare redigeringar och kommentarer och även öppna en händelse igen. Standard är markerat.

* **Flagga inlägg**

  Om det här alternativet är markerat kan medlemmar flagga andras händelser eller kommentarer som olämpliga. Standard är markerat.

* **Flaggorsakslista**

  Om det här alternativet är markerat kan medlemmarna i en nedrullningsbar lista välja orsaken till att en händelse eller kommentar flaggas som olämplig. Standard är avmarkerat.

* **Anledning till anpassad flagga**

  Om det här alternativet är markerat kan medlemmarna ange en egen orsak till att en händelse eller kommentar flaggas som olämplig. Standard är avmarkerat.

* **Modereringströskel**

  Ange hur många gånger en händelse eller kommentar måste flaggas av medlemmar innan moderatorerna meddelas. Standardvärdet är 1 (en gång).

* **Flaggningsgräns**

  Ange hur många gånger en händelse eller kommentar måste flaggas innan den döljs för den offentliga vyn. Om värdet är -1 döljs aldrig det flaggade ämnet eller kommentaren från den offentliga vyn. Annars måste talet vara större än eller lika med modereringströskeln. Standardvärdet är 5.

#### Fliken Taggfält {#tag-field-tab}

Under fliken **Taggfält** är de taggar som kan användas, om de tillåts under fliken **Inställningar** , begränsade enligt de valda namnutrymmena.

* **Tillåtna namnutrymmen**

  Relevant om `Allow Tagging` är markerat under fliken **Inställningar**. De taggar som kan användas är begränsade till de inom de namnutrymmeskategorier som kontrolleras. Listan med namnutrymmen innehåller&quot;Standardtaggar&quot; (standardnamnutrymmet) och&quot;Inkludera alla taggar&quot;. Standardvärdet är inget markerat, vilket betyder att alla namnutrymmen är tillåtna.

* **Förslagsgräns**

  Ange antalet taggar som ska visas som ett förslag till medlemmens inlägg i forumet. Standardvärdet är **-**1 (inga gränser).

>[!NOTE]
>
>Gå till [Administrera taggar](/help/sites-administering/tags.md) där du kan lära dig hur du lägger till ett taggnamnområde (taxonomi).

#### Fliken Översättning {#translation-tab}

Om översättning är aktiverat för communitywebbplatsen på fliken **Översättning** kan översättning ställas in så att hela tråden (händelse och kommentarer) översätts i stället för specifika inlägg.

* **Översätt alla**

  Om det här alternativet är markerat översätts händelsen och kommentarerna till användarens språk. Standard är markerat.

## Site Visitor Experience {#site-visitor-experience}

I publiceringsmiljön visar kalenderfunktionen ett sökfält med ett standarddatumintervall och alla kalenderhändelser som ligger inom det intervallet.

När en kalenderhändelse är markerad visas information om kalenderhändelsen, beskrivning och kommentarer.

Andra funktioner beror på om besökaren är en moderator, administratör, community-medlem, privilegierad medlem eller anonym.

### Styrelsemedlemmar och administratörer {#moderators-and-administrators}

När den inloggade användaren har moderator- eller administratörsbehörighet kan de utföra [modereringsåtgärder](/help/communities/moderate-ugc.md) (som tillåts enligt konfigurationen av komponenten) för alla kalenderhändelser och kommentarer som publiceras till en händelse.

![moderatorvy](assets/moderators-view.png)

#### Medlemmar {#members}

När den inloggade användaren är en community-medlem eller [behörig medlem](/help/communities/users.md#privileged-members-group) (beroende på konfiguration) kan användaren välja `New Event` för att skapa och publicera en ny kalenderhändelse.

De får särskilt

* Skapa en kalenderhändelse
* Post en kommentar till en kalenderhändelse
* Redigera en egen kalenderhändelse eller kommentar
* Ta bort en egen kalenderhändelse eller kommentar
* Flagga andras kalenderhändelser eller kommentarer

![create-event](assets/configure-calendar2.png)

![event-post](assets/configure-calendar3.png)

#### Anonym {#anonymous}

Webbplatsbesökare som inte är inloggade kan bara läsa publicerade kalenderhändelser, översätta dem om de stöds, men kan inte lägga till en händelse eller kommentar eller flagga andras händelser eller kommentarer.

![anonym-användarvy](assets/anonymous-user-view1.png)

## Ytterligare information {#additional-information}

Mer information finns på sidan [Calendar Essentials](/help/communities/calendar-basics-for-developers.md) för utvecklare.

moderering av kalenderhändelser och kommentarer finns i [Moderating User Generated Content](/help/communities/moderate-ugc.md) (modererar användargenererat innehåll).

Information om hur du taggar kalenderhändelser och kommentarer finns i [Tagga användargenererat innehåll](/help/communities/tag-ugc.md).

Mer information om översättning av kalenderhändelser och kommentarer finns i [Översätta användargenererat innehåll](/help/communities/translate-ugc.md).
