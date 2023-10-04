---
title: Ställning
description: Ibland kan du behöva skapa en stor uppsättning sidor som har samma struktur men olika innehåll. Med hjälp av ställningar kan du skapa ett formulär (en struktur) med fält som återspeglar den struktur du vill ha för sidorna och sedan använda det här formuläret för att enkelt skapa sidor som baseras på den strukturen.
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
docset: aem65
exl-id: 58e61302-cfb4-4a3d-98d4-3c92baa2ad42
source-git-commit: 5bdf42d1ce7b2126bfb2670049deec4b6eaedba2
workflow-type: tm+mt
source-wordcount: '1429'
ht-degree: 0%

---

# Ställning{#scaffolding}

Ibland kan du behöva skapa en stor uppsättning sidor som har samma struktur men olika innehåll. Genom det vanliga Adobe Experience Manager-gränssnittet (AEM) måste du skapa varje sida, dra lämpliga komponenter till sidan och fylla i varje sida separat.

Med hjälp av ställningar kan du skapa ett formulär (en struktur) med fält som återspeglar den struktur du vill ha för sidorna och sedan använda det här formuläret för att enkelt skapa sidor som baseras på den strukturen.

>[!NOTE]
>
>Skällning (i det klassiska användargränssnittet) [respekterar MSM-arv](#scaffolding-with-msm-inheritance).

## Så fungerar Scaffolding {#how-scaffolding-works}

Scaffäler lagras i **verktyg** konsol för webbplatsadministratören.

* Öppna **verktyg** konsol och klicka **Standardsidans placering**.
* Klicka på **Geometrixx**.
* Under **Geometrixx** hittar du en *avskalad sida* anropad **Nyheter**. Dubbelklicka för att öppna den här sidan.

![howscafels_work](assets/howscaffolds_work.png)

Ställningen består av ett formulär med ett fält för varje innehållspunkt som utgör den sida som ska skapas och fyra viktiga parametrar som är tillgängliga via **Sidegenskaper** på sidan med ställningar.

![pageprops](assets/pageprops.png)

Skolningssidans egenskaper är:

* **Titeltext**: Det här är namnet på själva byggnadssidan. I det här exemplet kallas det&quot;News&quot;.
* **Beskrivning**: Detta visas under rubriken på byggnadssidan.
* **Målmall**: Det här är den mall som det här skalet använder när en sida skapas. I det här exemplet är det en *Geometrixx innehållssida* mall.
* **Målsökväg**: Det här är sökvägen till den överordnade sidan under vilken den här strukturen skapar sidor. I det här exemplet är sökvägen */content/geometrixx/en/news*.

Skaffets brödtext är formen. När en användare vill skapa en sida med hjälp av skalet fyller han i formuläret och klickar *Skapa*, längst ned. I **Nyheter** exemplet ovan innehåller följande fält:

* **Titel**: Det här är namnet på sidan som ska skapas. Det här fältet finns alltid på alla ställningar.
* **Text**: Det här fältet motsvarar en textkomponent på den resulterande sidan.
* **Bild**: Det här fältet motsvarar en bildkomponent på den slutliga sidan.
* **Bild/Avancerat**: **Titel**: Bildens titel.
* **Bild/Avancerat**: **Alt-text**: Alt-texten för bilden.
* **Bild/Avancerat**: **Beskrivning**: Beskrivning av bilden.
* **Bild/Avancerat**: **Storlek**: Bildens storlek.
* **Taggar/nyckelord**: Metadata som ska tilldelas den här sidan. Det här fältet finns alltid på alla ställningar.

### Skapa ett ställningar {#creating-a-scaffold}

Om du vill skapa ett nytt ställningar går du till **verktyg** konsol, sedan **Standardsidans placering** och skapa en sida. Det finns en malltyp för en sida, *Ställningsmall.*

Gå till **Sidegenskaper** på den nya sidan och ange *Titeltext*, *Beskrivning*, *Målmall* och *Målsökväg*, enligt beskrivningen ovan.

Därefter måste du definiera strukturen för sidan som det här skalet ska skapa. För att göra detta, gå till **[designläge](/help/sites-authoring/page-authoring.md#sidekick)** på scensidan. En länk visas där du kan redigera skalet i **dialogruteredigerare**.

![cq5_dialog_editor](assets/cq5_dialog_editor.png)

I dialogruteredigeraren anger du de egenskaper som ska skapas varje gång en ny sida skapas med det här skalet.

Dialogrutedefinitionen för ett ställningar fungerar på liknande sätt som för en komponent (se [Komponenter](/help/sites-developing/components.md)). Det finns dock några viktiga skillnader:

* Komponentdialogrutans definitioner återges som vanliga dialogrutor (som i t.ex. den mittersta rutan i dialogruteredigeraren) medan definitioner i dialogrutan för att ställa in skala, trots att de visas som vanliga dialogrutor i dialogruteredigeraren, återges som ett ställningar på den skalbara sidan (som visas i **Nyheter** ställningar ovan).
* Komponentdialogrutor innehåller endast fält för de värden som behövs för att definiera innehållet i en enskild specifik komponent. En strukturdialogruta måste innehålla fält för varje egenskap i varje stycke på sidan som ska skapas.
* I komponentdialogrutor är komponenten som används för att återge det angivna innehållet implicit och därför är `sling:resourceType` styckets egenskap fylls i automatiskt när stycket skapas. I ett schackmönster måste all information som definierar både innehållet och den tilldelade komponenten för ett visst stycke anges i själva dialogrutan. I schackold-dialogrutor måste den här informationen anges med *Dold* fält för att skicka den här informationen när sidor skapas.

En titt på exemplet **Nyheter** i dialogrutan kan du förklara hur det fungerar. Gå till designläge på scensidan och klicka på länken för dialogruteredigeraren.

Klicka nu på dialogrutan **Dialog > Tab Panel > Text > Text**, så här:

![textedit](assets/textedit.png)

Egenskapslistan för det här fältet visas till höger i dialogruteredigeraren enligt följande:

![list_of_properties](assets/list_of_properties.png)

Observera namnegenskapen för det här fältet. Det har värdet

`./jcr:content/par/text/text`

Det här är namnet på den egenskap som innehållet i det här fältet ska skrivas till när skalet används för att skapa en sida. Egenskapen anges som en relativ sökväg från noden som representerar sidan som ska skapas. Den anger egenskapstexten, under nodtexten, som är under nodparentesen, som i sin tur är underordnad noden jcr:content under sidnoden.

Detta definierar platsen för innehållslagringen för texten som ska infogas i det här fältet. Men vi måste också specificera ytterligare två egenskaper för detta innehåll:

* Att strängen som lagras här måste tolkas som *RTF* och
* vilken komponent som ska användas för att återge innehållet till den resulterande sidan.

I en normal komponentdialogruta behöver du inte ange den här informationen eftersom den är implicit eftersom dialogrutan redan är bunden till en viss komponent.

Om du vill ange dessa två informationsdelar använder du dolda fält. Klicka på det första dolda fältet **Dialog > Tab Panel > Text > Hidden**, så här:

![dold](assets/hidden.png)

Egenskaperna för det här dolda fältet är följande:

![hidden_list_props](assets/hidden_list_props.png)

Egenskapen name för det här dolda fältet är

`./jcr:content/par/text/textIsRich`

Det här är en boolesk egenskap som används för att tolka textsträngen som lagras på `./jcr:content/par/text/text`.

Eftersom vi vet att texten ska tolkas som en RTF-text kan vi specificera `value` egenskap för det här fältet som `true`.

>[!CAUTION]
>
>I dialogruteredigeraren kan användaren ändra värdena för *befintlig* egenskaper i dialogdefinitionen. Användaren måste använda för att lägga till en ny egenskap [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md). När ett nytt dolt fält läggs till i en dialogrutedefinition med dialogruteredigeraren har det inte något *value* -egenskap (det vill säga en egenskap med namnet&quot;value&quot;). Om det dolda fältet i fråga kräver att en standardvärdeegenskap ställs in, måste den här egenskapen läggas till manuellt med något av CRX-verktygen. Värdet kan inte läggas till med själva dialogruteredigeraren. Men när egenskapen finns kan dess värde redigeras med dialogruteredigeraren.

Det andra dolda fältet visas om du klickar på det så här:

![hidden2](assets/hidden2.png)

Egenskaperna för det här dolda fältet är följande:

![hidden_list_props2](assets/hidden_list_props2.png)

Egenskapen name för det här dolda fältet är

`./jcr:content/par/text/sling:resourceType`

Och det fasta värdet som anges för den här egenskapen är

`foundation/components/textimage`

Detta anger att komponenten som ska användas för att återge textinnehållet i det här stycket är *Textbild* -komponenten. Använda med `isRichText` booleskt, som anges i det andra dolda fältet, kan komponenten återge den faktiska textsträngen som lagras på `./jcr:content/par/text/text` på önskat sätt.

### Skällning med MSM-arv {#scaffolding-with-msm-inheritance}

I det klassiska användargränssnittet är ställningar helt integrerade med MSM-arv (om tillämpligt).

När du öppnar en sida i **Ställning** läge (med ikonen längst ned i sidosparken) alla komponenter som är föremål för arv indikeras av:

* en låssymbol (för de flesta komponenter, till exempel Text och Titel)
* en mask med texten **Klicka för att avbryta arv** (för bildkomponenter)

Dessa visar att komponenten inte kan redigeras - förrän arvet avbryts.

![chlimage_1](assets/chlimage_1.jpeg)

>[!NOTE]
>
>Detta är jämförbart med [ärvda komponenter vid redigering av sidinnehåll](/help/sites-authoring/editing-content.md#inheritedcomponentsclassicui).

Om du klickar på låssymbolen eller bildikonen kan du bryta arvet:

* symbolen ändras till ett öppet hänglås.
* när innehållet är olåst kan du redigera det.

![chlimage_1-1](assets/chlimage_1-1.jpeg)

När du har låst upp kan du återställa arvet genom att klicka på den olåsta hänglåssymbolen. Då försvinner alla ändringar du har gjort.

>[!NOTE]
>
>Om arvet avbryts på sidnivå (från fliken Livecopy i Sidegenskaper) kan alla komponenter redigeras i **Ställning** (de visas i olåst läge).
