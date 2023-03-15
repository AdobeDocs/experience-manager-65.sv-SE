---
title: Skapa en ny GRE-fältkomponent
seo-title: Creating a New Granite UI Field Component
description: Gränssnittet i Granite innehåller en rad komponenter som är utformade för att användas i formulär, så kallade fält
seo-description: Granite UI provides a range of components designed to be used in forms, called fields
uuid: cf26e057-4b0c-45f4-8975-2c658517f20e
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 94b9eeee-aae3-4b28-9d6f-1be0e4acd982
exl-id: e4820330-2ee6-4eca-83fd-462aa0b83647
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '539'
ht-degree: 0%

---

# Skapa en ny GRE-fältkomponent{#creating-a-new-granite-ui-field-component}

Gränssnittet Granite innehåller ett antal komponenter som är avsedda att användas i formulär. kallas *fält* i GRUND-språket Granite. Standardkomponenterna i Granite finns under:

`/libs/granite/ui/components/foundation/form/*`

>[!NOTE]
>
>Dessa GRÄNSSNITTSformulärfält är av särskilt intresse eftersom de används för [komponentdialogrutor](/help/sites-developing/developing-components.md).

>[!NOTE]
>
>Mer information om fält finns i [Granite UI-dokumentation](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html).

Använd ramverket Granite UI Foundation för att utveckla och/eller utöka Granite-komponenter. Detta har två element:

* serversidan:

   * en samling grundkomponenter

      * grund - modulär, sammansättningsbar, lagerhanterbar, återanvändbar
      * komponenter - Sling-komponenter
   * hjälpmedel för utveckling av ansökningar


* klientsidan:

   * en samling klientlibs som innehåller vissa vokabulära tecken (dvs. en utökning av HTML) för att uppnå generiska interaktionsmönster via ett hypermediedrivet användargränssnitt

Den generiska användargränssnittskomponenten Granite `field` består av två intressanta filer:

* `init.jsp`: hanterar den allmänna behandlingen, etiketter, beskrivning och tillhandahåller formulärvärden som du behöver när du återger fältet.
* `render.jsp`: Det är här som den faktiska återgivningen av fältet utförs och måste åsidosättas för ditt anpassade fält. ingår i `init.jsp`.

Se [Bevilja gränssnittsdokumentation - fält](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/components/foundation/form/field/index.html) om du vill ha mer information.

Se till exempel:

* `cqgems/customizingfield/components/colorpicker`

   * från [Kodexempel](/help/sites-developing/developing-components-samples.md#code-sample-how-to-customize-dialog-fields)

* `granite/ui/components/foundation/form`

>[!NOTE]
>
>Eftersom den här mekanismen använder JSP, ges i18n och XSS inte direkt. Det innebär att du måste internationalisera och undvika dina strängar. Följande katalog innehåller de generiska fälten från en standardinstans och du kan använda dessa som referens:
>
>`/libs/granite/ui/components/foundation/form` katalog

## Skapa serverskriptet för komponenten {#creating-the-server-side-script-for-the-component}

Ditt anpassade fält bör bara åsidosätta `render.jsp` skript, där du anger koden för komponenten. Du kan betrakta JSP (dvs. återgivningsskriptet) som en wrapper för koden.

1. Skapa en ny komponent som använder `sling:resourceSuperType` egenskap att ärva från:

   `/libs/granite/ui/components/foundation/form/field`

1. Åsidosätt skriptet:

   `render.jsp`

   I det här skriptet måste du generera hypermediemarkeringen (d.v.s. berikad kod som innehåller hypermedielagring) så att klienten vet hur man interagerar med det genererade elementet. Detta bör följa kodningsformatet för serversidan Granite.

   När du anpassar, det enda kontrakt som du *måste* fulfill är att läsa formulärvärdet (initierat i `init.jsp`) från begäran med:

   ```
   // Delivers the value of the field (read from the content)
   ValueMap vm = (ValueMap) request.getAttribute(Field.class.getName());
   vm.get("value, String.class");
   ```

   Mer information finns i implementeringen av användargränssnittsfält för Granite som är färdiga att användas. till exempel `/libs/granite/ui/components/foundation/form/textfield`.

   >[!NOTE]
   >
   >För närvarande är JSP den rekommenderade skriptmetoden eftersom det inte är lätt att skicka information från en komponent till en annan (vilket är ganska vanligt i formulärfält) i HTML.

## Skapa klientbiblioteket för komponenten {#creating-the-client-library-for-the-component}

Så här lägger du till specifikt klientbeteende i komponenten:

1. Skapa ett clientlib för kategori `cq.authoring.dialog`.
1. Skapa ett clientlib för kategori `cq.authoring.dialog` och definiera `JS`/ `CSS` inuti.

   Definiera `JS`/ `CSS` inuti klientlib.

   >[!NOTE]
   >
   >För tillfället innehåller GRE-gränssnittet inga avlyssnare eller kopplingar som du kan använda direkt för att lägga till JS-beteende. För att lägga till ytterligare JS-beteende i komponenten måste du implementera en JS-krok i en anpassad klass som du sedan tilldelar till komponenten under kodgenereringen.
