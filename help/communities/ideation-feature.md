---
title: Idéfunktion
description: Lär dig hur du lägger till och konfigurerar funktionen Ideation som gör att communitymedlemmar kan skapa, visa, följa, rösta och kommentera idéer som delas med communityn.
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
docset: aem65
exl-id: e130bab4-524d-4413-ba8b-53d0ed9e8623
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '1111'
ht-degree: 0%

---

# Idéfunktion {#ideation-feature}

## Introduktion {#introduction}

Idéfunktionen är ett område där besökare på den inloggade webbplatsen (community-medlemmar) i publiceringsmiljön kan:

* Skapa idéer att dela med communityn.
* Visa och kommentera idéer.
* Följ en idé.
* Rösta på en idé.

I det här avsnittet av dokumentationen beskrivs:

* Lägga till idéfunktionen på en AEM webbplats.
* Konfigurationsinställningar för Ideation-komponenten.

### Lägga till en idé på en sida {#adding-a-ideation-to-a-page}

Lägga till en `Ideation` -komponent till en sida i redigeringsläge använder du komponentwebbläsaren för att leta upp

* `Communities / Ideation`

Dra den till en plats på en sida där idén ska visas.

Nödvändig information finns på [Grunderna för communitykomponenter](/help/communities/basics.md).

När [nödvändiga bibliotek på klientsidan](/help/communities/ideation.md#essentials-for-client-side) ingår så här `Ideation` visas:

![idéskiss](assets/ideation.png)

### Konfigurera en idé {#configuring-an-ideation}

Markera den monterade `Ideation` så att du kan komma åt och välja `Configure` -ikonen som öppnar redigeringsdialogrutan.

![configure-new](assets/configure-new.png)

![ideation-settings](assets/ideation-settings.png)

#### Fliken Inställningar {#settings-tab}

Under **[!UICONTROL Settings]** -fliken, ange inställningar för idéer och kommentarer:

* **Tillåt miniatyrbild för bifogad fil**
* **Maximal storlek på miniatyrbild**
* **Minsta bildstorlek för miniatyrbild**
* **Maximal miniatyrstorlek**
* **Tillåt behöriga medlemmar**
* **Tillåtna behöriga medlemmar**
* **Blockera användargenererat innehåll i redigeringsläge för författare**
* **Idétitel**

* Idéns visningsrubrik. Standard är `Ideation`.
* **Ideationsbeskrivning**

  En beskrivning som ska visas som underrubrik till idén. Standardvärdet är ingen beskrivning.

* **Ämnen per sida**

  Definierar antalet idéer/inlägg som visas per sida. Standardvärdet är 10.

* **Kontrollerad**

  Om det här alternativet är markerat måste publicering av idéer och kommentarer godkännas innan de kan visas på en publiceringsplats. Standard är avmarkerat.

* **Stängd**

  Om det här alternativet är markerat är idéforumet stängt för nya idéer och kommentarer. Standard är avmarkerat.

* **RTF-redigerare**

  Om du markerar det här alternativet kan du lägga in kommentarer och idéer. Standard är avmarkerat.

* **Tillåt taggning**

  Tillåt medlemmar att lägga till taggetiketter i sina inlägg (se **[!UICONTROL Tag field]** -fliken). Standard är avmarkerat.

* **Tillåt filöverföringar**

  Om du markerar det här alternativet kan du tillåta att bifogade filer läggs till i idén eller kommentaren. Standard är avmarkerat.

* **Maximal filstorlek**

  Endast relevant om `Allow File Uploads` är markerad. Det här fältet begränsar storleken (i byte) på en överförd fil. Standardvärdet är 104857600 (10 MB).

* **Tillåtna filtyper**

  Endast relevant om `Allow File Uploads` är markerad. En kommaavgränsad lista med filtillägg med punktavgränsaren. Exempel: .jpg, .jpeg, .png, .doc, .docx, .pdf. Om någon filtyp har angetts kan de inte överföras. Ingen standard har angetts så att alla filtyper tillåts.

* **Maximal filstorlek för bifogad bild**

  Endast relevant om Tillåt filöverföringar är markerat. Maximalt antal byte som en överförd bildfil kan ha. Standardvärdet är 2097152 (2 MB).

* **Tillåt svar**

  Om det här alternativet är markerat tillåts svar på kommentarer som har lagts till i idén. Standard är avmarkerat.

* **Tillåt röstning**

  Om det här alternativet är markerat tillåts omröstning om en idés kommentarer. Standard är avmarkerat.

* **Tillåt användare att ta bort kommentarer och ämnen**

  Om det här alternativet är markerat kan medlemmarna ta bort de kommentarer och idéer som de publicerade. Standard är avmarkerat.

* **Tillåt följande**

  Om du markerar det här alternativet inkluderas följande funktion för idéinlägg, som gör att medlemmar kan [meddelad](/help/communities/notifications.md) av nya tjänster. Standard är avmarkerat.

* **Tillåt e-postprenumerationer**

  Om det här alternativet är markerat, tillåt medlemmar att meddelas om nya inlägg via e-post ([prenumeration](/help/communities/subscriptions.md)). Kräver `Allow Following` ska kontrolleras och [e-post konfigurerad](/help/communities/email.md). Standard är avmarkerat.

* **Tillåt röstning**

  Om det här alternativet är markerat tillåts omröstning om en idés kommentarer. Standard är avmarkerat.

* **Visa emblem**

  Om det här alternativet är markerat visas intjänad och tilldelad [emblem](/help/communities/implementing-scoring.md) med en medlems idé. Standard är avmarkerat.

* **Hämta inte svar på listsidan**

* **Tillåt innehåll**

  Idén kan identifieras som om den är markerad [presenterat innehåll](/help/communities/featured.md). Standard är avmarkerat.

* **Aktivera omnämns**
* **Max. omnämnanden**
* **Mönster för användargränssnittets omnämnande**

#### Fliken Användarmoderering {#user-moderation-tab}

Under **[!UICONTROL User Moderation]** anger du hur publicerade idéer och kommentarer (användargenererat innehåll) ska hanteras. Mer information finns i [Modererar användargenererat innehåll](/help/communities/moderate-ugc.md).

* **Neka inlägg**

  Om det här alternativet är markerat kan pålitliga medlemsmoderatorer neka inlägg och förhindra att de visas på det offentliga forumet. Standard är avmarkerat.

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

Under **[!UICONTROL Tag field]** -fliken, de taggar som kan användas, om de tillåts under **[!UICONTROL Settings]** är begränsade enligt de namnutrymmen som har valts.

* **Tillåtna namnutrymmen**

  Relevant om `Allow Tagging` kontrolleras under **[!UICONTROL Settings]** -fliken. De taggar som kan användas är begränsade till de inom de namnutrymmeskategorier som kontrolleras. Listan med namnutrymmen innehåller&quot;Standardtaggar&quot; (standardnamnutrymmet) och&quot;Inkludera alla taggar&quot;. Standardvärdet är inget markerat, vilket betyder att alla namnutrymmen är tillåtna.

* **Förslagsgräns**

  Ange antalet taggar som ska visas som ett förslag till medlemmens inlägg i forumet. Värdet för **-1** betyder ingen gräns. Standardvärdet är 0.

#### Fliken Sorteringsinställningar {#sort-settings-tab}

Under **[!UICONTROL Sort Settings]** anger du hur de bokförda kommentarerna ska sorteras när de visas.

* **Sortera efter**

  Markera alla tillåtna sorteringsval: `Newest, Oldest, Last Updated, Most Viewed, Most Active, Most Followed and Most Liked`. Standard är `Newest, Oldest, Last Updated`.

* **Ange som standard**

  Dra nedåt om du vill välja något av de markerade sorteringsalternativen som ska visas som standard. Standard är `Newest`.

* **Välj tidsalternativ för Analytics-sortering**

  Dra ned för att välja något av `All, Last 24 Hours, Last 7 Days, Last 30 Days`. Standard är `All`.

## Site Visitor Experience {#site-visitor-experience}

### Skapar Idea {#creating-idea}

Precis som med alla communityfunktioner kan en besökare på webbplatsen endast läsa idéer och se andra åsikter (genom kommentarer och röstning/gilla-markeringar).

När medlemmen har loggat in kan han eller hon skapa en idé.

![create-new-idé](assets/create-new-idea.png)

Innan du skickar in en idé kan medlemmen spara ett utkast.

Genom att välja `Save as Draft` sparas ett utkast.

![save-ideas](assets/save-idea.png)

När du visar sparade utkast i `My Drafts` flik, välja `Read More` för att gå tillbaka till redigeringsläget:

![edit-ideas](assets/edit-idea.png)

#### Ge feedback {#providing-feedback}

När idén har publicerats kan andra medlemmar logga in, öppna idén ( `Read More`) och gillar idén, vilket ökar antalet röster och gör kommentarer.

![feedback](assets/feedback-idea.png)

### Ytterligare information {#additional-information}

Mer information finns på [Grundläggande om identifiering](/help/communities/ideation.md) för utvecklare.

moderering av inlägg och kommentarer finns i [Modererar användargenererat innehåll](/help/communities/moderate-ugc.md).

Information om hur du taggar publicerade ämnen och kommentarer finns i [Tagga användargenererat innehåll](/help/communities/tag-ugc.md).
