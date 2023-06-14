---
title: Filbiblioteksfunktion
description: Med funktionen Filbibliotek kan besökare på den inloggade webbplatsen överföra, hantera och hämta filer
uuid: e78a90bd-f1d3-44f8-98eb-1498a55e8217
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: ea2b23af-49c3-409b-a041-43c42d846f21
docset: aem65
exl-id: 05cfaab5-a12d-475f-9095-a9fb13571d0a
source-git-commit: d673a447e9ce2377c8645c87f12be81cbad06238
workflow-type: tm+mt
source-wordcount: '733'
ht-degree: 0%

---

# Filbiblioteksfunktion{#file-library-feature}

## Introduktion {#introduction}

Filbiblioteksfunktionen är en plats där besökare på den inloggade webbplatsen (community-medlemmar) kan överföra, hantera och hämta filer inom communitywebbplatsen.

I det här avsnittet av dokumentationen beskrivs:

* Lägga till filbiblioteksfunktionen på en AEM.
* Konfigurationsinställningar för `File Library` -komponenten.

### Lägga till ett filbibliotek på en sida {#adding-a-file-library-to-a-page}

Lägga till en `File Library` till en sida i redigeringsläge, leta reda på komponenten:

* `Communities / File Library`

Och dra den till rätt plats på en sida.

Nödvändig information finns på [Grunderna för communitykomponenter](/help/communities/basics.md).

När [nödvändiga bibliotek på klientsidan](/help/communities/essentials-file-library.md#essentials-for-client-side) ingår, det är så `File Library` visas:

![file-library1](assets/file-library1.png)

### Konfigurerar filbibliotek {#configuring-file-library}

Markera den monterade `File Library` så att du kan komma åt och välja `Configure` -ikonen som öppnar dialogrutan för redigering.

![configure-new](assets/configure-new.png)

![file-library2](assets/file-library2.png)

#### Fliken Kommentarer {#comments-tab}

Under **Kommentarer** anger du om och hur kommentarer för överförda filer ska visas:

* **Tillåt kommentarer om filer**

  Om det här alternativet är markerat tillåts kommentarer för överförda filer. Standard är avmarkerat.

* **Kommentarer per sida**

  Begränsar antalet kommentarer som visas per sida och antalet svar som visas. Standard är **10**.

* **Maximal filstorlek**

  Det här värdet begränsar storleken på den överförda filen. Standardgränsen är 104857600 (10 MB).

* **Maximal meddelandelängd**

  Maximalt antal tecken som kan anges i textrutan. Standardvärdet är 4 096 tecken.

* **Tillåtna filtyper**

  En kommaavgränsad lista med filtillägg med punktavgränsaren. Exempel: .jpg, .jpeg, .png, .doc, .docx, .pdf. Om någon filtyp anges tillåts inte filtyper som inte har angetts. Standardvärdet har inte angetts så att alla filtyper tillåts.

* **RTF-redigerare**

  Om det här alternativet är markerat kan kommentarer skrivas in med markeringar. Standard är avmarkerat.

* **Ta bort kommentarer**

  Om det här alternativet är markerat kan användarna ta bort sina egna kommentarer. Standard är markerat.

* **Tillåt taggning**

  Om du markerar det här alternativet aktiveras möjligheten att lägga till en tagg i filen. Standard är avmarkerat.

* **Tillåtna namnutrymmen**

  Om Tillåt taggning är markerat begränsas de tillgängliga taggarna till de namnutrymmen som är markerade. Om inga namnutrymmen är markerade tillåts alla. Standard är alla namnutrymmen.

* **Förslagsgräns**

  Om Tillåt taggning är markerat begränsas det antal föreslagna taggar som ska visas med den här inställningen. Om värdet är -1 finns det ingen gräns. Standardvärdet är -1.

* **Tillåt röstning**

  Om du markerar det här alternativet aktiveras möjligheten att rösta på en fil. Standard är avmarkerat.

* **Tillåt följande**

  Om du markerar det här alternativet inkluderar du följande funktion för bloggartiklar, som gör att medlemmar kan [meddelad](/help/communities/notifications.md) av nya tjänster. Standard är avmarkerat.

* **Aktivera omnämnande**

  Om det här alternativet är aktiverat kan registrerade communityanvändare identifiera andra registrerade medlemmar (med förnamn, efternamn, användarnamn) och tagga dem med den vanliga @användarnamnssyntaxen. De taggade användarna får meddelanden om sina omnämnanden.

* **Max. omnämnanden**

  Begränsa det maximala antalet omnämnanden som tillåts i ett inlägg. Standardvärdet är 10.

* **Mönster för användargränssnittets omnämnande**

  Ange den tillåtna mönstersträngen så att du taggar (@mention) den registrerade användaren i ett inlägg. Till exempel, `~{{familyName}}{{givenName}}`.

* **Tillåt kopplade svar**

  Om det här alternativet är markerat tillåts svar på publicerade kommentarer. Standard är avmarkerat.

#### Fliken Användarmoderering {#user-moderation-tab}

Under **Användarmoderering** -fliken, konfigurera moderering av kommentarer, om kommentarer tillåts:

* **Före moderering**

  Om det här alternativet är markerat måste kommentarerna godkännas innan de visas på en publiceringsplats. Standard är avmarkerat.

* **Ta bort kommentarer**

  Om det här alternativet är markerat kan den besökare som publicerade kommentaren ta bort den, om så önskas. Standard är markerat.

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

  Ange hur många gånger en kommentar måste flaggas innan den döljs för den offentliga vyn. Talet måste vara större än eller lika med **Modereringströskel**. Standardvärdet är 5.

### Fliken Sorteringsinställningar {#sort-settings-tab}

Sortera efter

Ange som standard

### Ytterligare information {#additional-information}

Mer information finns på [Grundläggande om filbibliotek](/help/communities/essentials-file-library.md) för utvecklare.

moderering av inlägg och kommentarer finns i [Modererar användargenererat innehåll](/help/communities/moderate-ugc.md).

Information om hur du taggar publicerade ämnen och kommentarer finns i [Tagga användargenererat innehåll](/help/communities/tag-ugc.md).
