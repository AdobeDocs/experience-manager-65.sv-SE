---
title: Anpassa mallar för komponenter i formulärportalen
seo-title: Anpassa mallar för komponenter i formulärportalen
description: Visa anpassade metadata i formulärlistan
seo-description: Visa anpassade metadata i formulärlistan
uuid: 212109ca-85c8-4915-82e5-a18a0443be1b
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
discoiquuid: 7566203f-2f80-4ce7-bff9-073d67119f64
docset: aem65
translation-type: tm+mt
source-git-commit: 13cc8ba8fda8fa0e5fac6bb92d1d4fc4849492eb

---


# Anpassa mallar för komponenter i formulärportalen{#customizing-templates-for-forms-portal-components}

## Förutsättningar {#prerequisites}

[Hantera formulärmetadata](../../forms/using/manage-form-metadata.md)

Arbetskunskaper i HTML och CSS

## Översikt {#overview}

Med användargränssnittet i AEM Forms kan du lägga till metadata i alla formulär. Anpassade metadata kan förbättra användarupplevelsen samtidigt som du listar och söker efter formulär i organisationen.

Med Forms Portal kan du använda anpassade metadata i formulärlistor. När du skapar anpassade mallar för resurser kan du ändra deras layout och använda anpassade metadata med din CSS-formatuppsättning.

Utför följande steg för att skapa en anpassad mall för olika komponenter i Forms Portal.

## Skapa en anpassad mall {#creating-a-nbsp-custom-template}

1. Skapa en slinga:Mappnod under /apps

   Lägg till en fpContentType-egenskap. Ange lämpliga värden för egenskapen beroende på vilken komponent du definierar den anpassade mallen för.

   * Komponenten Search &amp; Lister: &quot;/libs/fd/fp/formTemplate&quot;
   * Komponenten Utkast och inskickat material:

      * Avsnittet Utkast: /libs/fd/fp/draftTemplate
      * Inlämningsavsnitt: /libs/fd/fp/sendingTemplate
   * Länkkomponent: /libs/fd/fp/linkTemplate
   Lägg till en titel som du vill ska visas när du väljer layoutmallar.

   *Obs! Titeln kan skilja sig från nodnamnet för sling:Mapp som du skapade.*
   *I följande bild visas konfigurationen för komponenten Sök och Lister.* ![Skapa en sling:Mapp](assets/1.png)

1. Skapa en filmall.html i den här mappen som ska fungera som anpassad mall.
1. Skriv den anpassade mallen och använd anpassade metadata enligt beskrivningen nedan.

## Exempel {#working-example}

Nedan följer ett exempel på implementering av en anpassad mall där Forms Portal förvärvar en anpassad Geometrixx Gov-kortlayout för komponenten Sök och Lister.

```mxml
<div class="__FP_boxes-container __FP_single-color">
    <div class="boxes __FP_boxes __FP_single-color" data-repeatable="true">
 <div class="__FP_boxes-thumbnail">
     <img src ="${path}/jcr:content/renditions/cq5dam.thumbnail.319.319.png"/>
        </div>
        <h3 class="__FP_single-color" title="${name}" tabindex="0">${name}</h3>
        <p>${description}</p>
        <div class="boxes-icon-cont __FP_boxes-icon-cont">
            <div class="op-dow">
                <a href="${formUrl}" target="_blank" class="__FP_button ${htmlStyle}" title="${config-htmlLinkText}">${localize-Apply}</a>
                <a href="${pdfUrl}" class="__FP_button ${pdfStyle}" title="${config-pdfLinkText}">${localize-Download}</a>
            </div>
        </div>
    </div>
</div>
```

## Tekniska specifikationer för anpassade mallar {#technical-specifications-for-custom-templates}

En anpassad mall för alla Forms Portal-komponenter innehåller repeterbara och icke-repeterbara poster. Repeterbara poster är grundläggande enheter som ska tas upp i förteckningen. Exempel på upprepningsbara poster är komponenterna Sök och Lister, Utkast och överföringar samt Länka.

Forms Portal innehåller en syntax där platshållare kan visa anpassade metadata/OTB-metadata. Platshållarna fylls i när resultatet av formulär, utkast eller inskickade formulär visas.

Om du vill ta med en upprepningsbar post konfigurerar du värdet för attributet **data-repetable** till **true**.

*I det exempel som beskrivs finns två Div-element högst upp i den anpassade mallen. Den första, med CSS-klassen&quot;__FP_boxes-container&quot;, fungerar som ett behållarelement för de formulär som visas. Den andra, med CSS-klassen&quot;__FP_boxes&quot;, är en mall för de grundläggande entiteterna, i det här fallet ett formulär. Attributet **data-repetable**i Div-elementet har värdet **true**.*

Varje platshållare har en exklusiv OTB-metadatauppsättning. Om du vill visa anpassade metadata på en viss plats i formuläret lägger du till egenskapen **** ${metadata_prop} på platsen.

*I exemplet används metadataegenskapen i flera instanser. Det används t.ex. i **description**,**name**,**formUrl**,**htmlStyle**,**pdfUrl**********,¥pdfStyle¥ ochPath¥¥ på föreskrivet sätt.*

## Inga metadata {#out-of-the-box-metadata}

Olika komponenter i Forms Portal innehåller exklusiva uppsättningar OTB-metadata som du kan använda för att visa en lista.

### Komponenten Search &amp; Lister {#search-amp-lister-component}

* **** Titel: Formulärets namn
* **namn**: Formulärets namn (oftast är det samma som titeln)
* **beskrivning**: Beskrivning av formuläret
* **formUrl**: URL för att återge formuläret som HTML
* **pdfUrl**: URL för att återge formuläret som PDF
* **assetType**: Typ av tillgång. Giltiga värden är **Form**,**PDF Form**, **Print Form** och **Adaptive Form**

* **htmlStyle**&amp; **pdfStyle**: Visningsformat för HTML- respektive PDF-ikoner som används för återgivning. Giltiga värden är &quot;**__FP_display_none**&quot; eller blank.

   **** Obs! Kom ihåg att använda klassen __FP_display_none i din anpassade formatmall

* **downloadUrl**: URL för att hämta en resurs.

Stöd för lokalisering, sortering och användning av konfigurationsegenskaper i användargränssnittet (endast sökning och lister):

1. **Lokaliseringsstöd**: Om du vill lokalisera statisk text använder du attributet `${localize-YOUR_TEXT}` och gör det lokaliserade värdet tillgängligt, om det inte redan finns.
   *I exemplet som behandlas används attributen`${localize-Apply}`och`${localize-Download}`för att lokalisera texten Använd och Hämta.*

1. **Stöd för sortering**: Klicka på HTML-elementet för att sortera sökresultaten. Om du vill implementera sortering i en skickad layout lägger du till attributet data-sortKey i den aktuella tabellrubriken. Lägg dessutom till dess värde som de metadata som du vill sortera efter.
För rubrikrubriken i stödrastervyn är värdet för rubriken&quot;data-sortKey&quot; till exempel&quot;title&quot;. Klicka på rubriken om du vill sortera värdena i en viss kolumn.

1. **Använda konfigurationsegenskaper**: Komponenten Sök och visa har flera konfigurationer som du kan använda i användargränssnittet. Om du till exempel vill visa HTML-verktygstips som sparats i redigeringsdialogrutan använder du `${config-htmlLinkText}` attributet . **På samma sätt använder du attributet för** PDF-verktygstipstext `${config-pdfLinkText}` .

### Länkkomponent {#link-component}

* **** Titel: Formulärets namn
* **formUrl**: URL för att återge formuläret som HTML
* **mål**: Länkens målattribut. Giltiga värden är &quot;_blank&quot; och &quot;_self&quot;.
* **linkText**: Länkbeskrivning

### Komponenten Utkast och inskickat material {#drafts-amp-submissions-component}

* **Sökväg**: Sökväg till metadatanoden för utkast/överföringar. Använd det med tillägget .HTML som en URL för att öppna ett utkast eller en sändning.
* **contextPath**: Kontextsökväg för AEM-instansen
* **firstLetter**: Första bokstaven (versaler) i titeln på det adaptiva formuläret, som sparats som utkast eller skickad.
* **formName**: Titeln på det adaptiva formuläret, som har sparats som utkast eller skickats.
* **draftID**: ID för det utkast som visas (Använd bara i mallen för avsnittet Utkast).
* **submitID**: ID för överföringen som visas (Använd bara i mallen för avsnittet Skicka).
* **status**: Status för det skickade formuläret. (Använd endast i mallen för avsnittet Skicka).
* **beskrivning**: Beskrivning av det adaptiva formulär som är kopplat till utkastet eller inlämningen.
* **diffTime**: Skillnaden mellan aktuell tid och den senaste sparåtgärden för utkastet. Alternativt kan det vara en skillnad mellan den aktuella tiden och den senaste sändningsåtgärden för överföringen.
* **iconClass**: CSS-klass som används för att visa den första bokstaven i utkastet/sändningen. Forms Portal innehåller följande klasser som innehåller olika färgade bakgrunder.
* **ägare**: Användare som skapade utkastet/överföringen.
* **Idag**: Datum då utkastet eller inlämningen skapades i formatet DD:MM:YYY.
* **TimeNow**: Tid då utkastet eller inlämningen skapades i HH:MM:SS 24-timmarsformat

*Obs!*

1. Om du vill ta bort alternativet i avsnittet Utkast under komponenten Utkast och överföringar ska du ge CSS-klassen namnet&quot;__FP_deleteDraft&quot;. Inkludera dessutom attributet &quot;draftID&quot; med värdet **${draftID}**, som är utkast-ID för motsvarande utkast.

1. När du skapar länkar till öppna utkast och inskickade dokument kan du ange **${path}.html** som värde för **href** -attributet för ankartaggen.

![Utkast och inskickningsnod](assets/raw-image-with-index.png)

**A**. Behållarelement

**** B. &quot;path&quot;-metadata med en fast hierarki för att få miniatyrbilder lagrade för varje formulär.

**C.** Attribut för upprepning av data som används för mallavsnittet för varje formulär

**** D. För att lokalisera strängen &quot;Använd&quot;

**** E. Använda konfigurationsegenskapen pdfLinkText

**** F. Använda metadata för pdfUrl

## Tips, tricks och kända fel {#tips-tricks-and-known-issues}

1. Använd inte enkla citattecken (&#39;) i någon anpassad mall.
1. Om du vill ha anpassade metadata sparar du den här egenskapen endast på **jcr:content/metadata** -noden. Om du lagrar den på något annat ställe kan inte Forms Portal visa metadata.
1. Kontrollera att namnet på anpassade metadata eller befintliga metadata inte innehåller ett kolon (: ). Om det gör det kan du inte visa det i användargränssnittet.
1. **data-repetable** har ingen betydelse för en **Link** -komponent. Adobe rekommenderar att du undviker att använda den här egenskapen i mallen för en Link-komponent.

## Relaterade artiklar

* [Aktivera komponenter i formulärportalen](/help/forms/using/enabling-forms-portal-components.md)
* [Skapa portalsida för formulär](/help/forms/using/creating-form-portal-page.md)
* [Visa formulär på en webbsida med API:er](/help/forms/using/listing-forms-webpage-using-apis.md)
* [Använda komponenten Utkast och inskickat material](/help/forms/using/draft-submission-component.md)
* [Anpassa lagring av utkast och inskickade formulär](/help/forms/using/draft-submission-component.md)
* [Exempel för att integrera komponent för utkast och inlämning med databas](/help/forms/using/integrate-draft-submission-database.md)
* [Anpassa mallar för komponenter i formulärportalen](/help/forms/using/customizing-templates-forms-portal-components.md)
* [Introduktion till att publicera formulär på en portal](/help/forms/using/introduction-publishing-forms.md)