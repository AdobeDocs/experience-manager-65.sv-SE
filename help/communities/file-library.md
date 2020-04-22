---
title: Filbiblioteksfunktion
seo-title: Filbiblioteksfunktion
description: Med funktionen Filbibliotek kan besökare på den inloggade webbplatsen överföra, hantera och hämta filer
seo-description: Med funktionen Filbibliotek kan besökare på den inloggade webbplatsen överföra, hantera och hämta filer
uuid: e78a90bd-f1d3-44f8-98eb-1498a55e8217
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: ea2b23af-49c3-409b-a041-43c42d846f21
docset: aem65
translation-type: tm+mt
source-git-commit: 58a06c1a16c62bffad2893fbec0b32d2ce7267a7

---


# Filbiblioteksfunktion{#file-library-feature}

## Introduktion {#introduction}

Filbiblioteksfunktionen är en plats där besökare på den inloggade webbplatsen (community-medlemmar) kan överföra, hantera och hämta filer inom communitywebbplatsen.

I det här avsnittet av dokumentationen beskrivs:

* Lägga till filbiblioteksfunktionen på en AEM-webbplats.
* Konfigurationsinställningar för `File Library` komponenten.

### Lägga till ett filbibliotek på en sida {#adding-a-file-library-to-a-page}

Om du vill lägga till en `File Library` komponent på en sida i redigeringsläge letar du reda på komponenten

* `Communities / File Library`

och dra den till rätt plats på en sida.

Mer information finns i Grunderna för [communitykomponenter](/help/communities/basics.md).

När de [nödvändiga klientbiblioteken](/help/communities/essentials-file-library.md#essentials-for-client-side) inkluderas visas `File Library` komponenten så här:

![chlimage_1-145](assets/chlimage_1-145.png)

### Konfigurerar filbibliotek {#configuring-file-library}

Markera den monterade `File Library` komponent som du vill öppna och välj den `Configure` ikon som öppnar redigeringsdialogrutan.

![chlimage_1-146](assets/chlimage_1-146.png) ![forum-config-1](assets/forum-config-1.png)

#### Fliken Kommentarer {#comments-tab}

Under fliken **Kommentarer** anger du om och hur kommentarer för överförda filer ska visas:

* **Tillåt kommentarer om filer**

   Om det här alternativet är markerat tillåts kommentarer för överförda filer. Standard är avmarkerat.

* **Kommentarer per sida**

   Begränsar antalet kommentarer som visas per sida samt antalet svar som visas. Standardvärdet är **10**.

* **Maximal filstorlek**

   Det här värdet begränsar storleken på den överförda filen. Standardgränsen är 104857600 (10 MB).

* **Maximal meddelandelängd**

   Maximalt antal tecken som kan anges i textrutan. Standardvärdet är 4 096 tecken.

* **Tillåtna filtyper**

   En kommaavgränsad lista med filtillägg med&quot;punktavgränsaren&quot;. Till exempel: .jpg, .jpeg, .png, .doc, .docx, .pdf. Om någon filtyp anges tillåts inte den som inte anges. Standardvärdet har inte angetts så att alla filtyper tillåts.

* **RTF-redigerare**

   Om det här alternativet är markerat kan kommentarer skrivas in med markeringar. Standard är avmarkerat.

* **Ta bort kommentarer**

   Om det här alternativet är markerat kan användarna ta bort sina egna kommentarer. Standard är markerat.

* **Tillåt taggning**

   Om du markerar det här alternativet aktiveras möjligheten att lägga till en tagg i filen. Standard är avmarkerat.

* **Tillåtna namnutrymmen**

   Om Tillåt taggning är markerat begränsas de tillgängliga taggarna till de namnutrymmen som är markerade. Om inga är markerade tillåts alla. Standard är alla namnutrymmen.

* **Förslagsgräns**

   Om Tillåt taggning är markerat begränsas det antal föreslagna taggar som ska visas med den här inställningen. Om värdet är -1 finns det ingen gräns. Standardvärdet är -1.

* **Tillåt röstning**

   Om det här alternativet är markerat aktiveras möjligheten att rösta efter en fil. Standard är avmarkerat.

* **Tillåt följande**

   Om det här alternativet är markerat kan du inkludera följande funktion för bloggartiklar, som gör att medlemmar kan [meddelas](/help/communities/notifications.md) om nya inlägg. Standard är avmarkerat.

* **Aktivera omnämnande**

   Om det här alternativet är aktiverat kan registrerade communityanvändare identifiera andra registrerade medlemmar (med förnamn, efternamn, användarnamn) och tagga dem med den vanliga @användarnamnssyntaxen. De taggade användarna får meddelanden om sina omnämnanden.

* **Max. omnämnanden**

   Begränsa det maximala antalet omnämnanden som tillåts i ett inlägg. Standardvärdet är 10.

* **Mönster för användargränssnittets omnämnande**

   Ange den tillåtna mönstersträngen för att tagga (@mention) den registrerade användaren i ett inlägg. Till exempel ~{{familyName}}{{givenName}}.

* **Tillåt kopplade svar**

   Om det här alternativet är markerat tillåts svar på publicerade kommentarer. Standard är avmarkerat.

#### Fliken Användarmoderering {#user-moderation-tab}

Konfigurera moderering av kommentarer under fliken **Användarmoderering** , om kommentarer tillåts:

* **Före moderering**

   Om det här alternativet är markerat måste kommentarerna godkännas innan de visas på en publiceringsplats. Standard är avmarkerat.

* **Ta bort kommentarer**

   Om det här alternativet är markerat kan den besökare som publicerade kommentaren ta bort den. Standard är markerat.

* **Neka kommentarer**

   Om det här alternativet är markerat tillåter du att pålitliga medlemsmoderatorer nekar kommentarer. Standard är avmarkerat.

* **Stäng/öppna kommentarer igen**

   Om det här alternativet är markerat kan du tillåta att pålitliga medlemsmoderatorer stänger och öppnar kommentarer igen. Standard är avmarkerat.

* **Flagga kommentarer**

   Om det här alternativet är markerat kan besökarna flagga kommentarer som olämpliga. Standard är avmarkerat.

* **Flaggorsakslista**

   Om det här alternativet är markerat kan besökare välja, från en nedrullningsbar lista, orsaken till att en kommentar flaggas som olämplig. Standard är avmarkerat.

* **Anledning till anpassad flagga**

   Om det här alternativet är markerat kan besökarna ange en egen orsak till att en kommentar flaggas som olämplig. Standard är avmarkerat.

* **Modereringströskel**

   Ange hur många gånger en kommentar måste flaggas av besökare innan moderatorerna meddelas. Standard är en gång (**1**).

* **Flaggningsgräns**

   Ange hur många gånger en kommentar måste flaggas innan den döljs för den offentliga vyn. Talet måste vara större än eller lika med **modereringströskeln**. Standardvärdet är 5.

### Fliken Sorteringsinställningar {#sort-settings-tab}

Sortera efter

Ange som standard

### Additional Information {#additional-information}

Mer information finns på sidan [File Library Essentials](/help/communities/essentials-file-library.md) för utvecklare.

Mer information om moderering av publicerade ämnen och kommentarer finns i [Hantera användargenererat innehåll](/help/communities/moderate-ugc.md).

Information om hur du taggar publicerade ämnen och kommentarer finns i [Tagga användargenererat innehåll](/help/communities/tag-ugc.md).
