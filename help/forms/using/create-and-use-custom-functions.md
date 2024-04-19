---
title: Skapa och lägga till anpassade funktioner i ett adaptivt formulär
description: AEM Forms stöder anpassade funktioner som gör att användare kan skapa och använda sina egna funktioner i regelredigeraren.
keywords: Lägg till en anpassad funktion, använd en anpassad funktion, skapa en anpassad funktion, använd anpassad funktion i regelredigeraren.
contentOwner: Ruchita Srivastav
content-type: reference
feature: Adaptive Forms, Core Components
exl-id: a328b4a8-e8dd-42a0-b73b-94e76c7692a8
source-git-commit: a5b48f1f4072f3e10273ec90d6f505815fe584a3
workflow-type: tm+mt
source-wordcount: '1111'
ht-degree: 0%

---


# Anpassade funktioner i Adaptive Forms (Core Components)

| Version | Artikellänk |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Klicka här](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/create-and-use-custom-functions) |
| AEM 6.5 | Den här artikeln |

## Introduktion

I AEM Forms 6.5 introducerades möjligheten att definiera JavaScript-funktioner som kan användas för att definiera komplexa affärsregler med regelredigeraren. AEM Forms har ett antal anpassade funktioner som du kan använda, men du måste definiera egna funktioner och använda dem i flera formulär.

Med de anpassade funktionerna kan man bättre hantera blanketterna genom att underlätta hanteringen och bearbetningen av inmatade data. De möjliggör också dynamisk ändring av formulärbeteende baserat på fördefinierade kriterier.
I Adaptiv Forms kan du använda anpassade funktioner i [regelredigerare för ett anpassat formulär](/help/forms/using/rule-editor.md) för att skapa specifika valideringsregler för formulärfält.
Låt oss förstå hur den anpassade funktionen används där användare anger e-postadressen och du vill se till att den angivna e-postadressen har ett visst format (den innehåller symbolen&quot;@&quot; och ett domännamn). Skapa en anpassad funktion som&quot;ValidateEmail&quot;, som tar e-postadressen som indata och returnerar true om den är giltig och i annat fall false.

```javascript
function ValidateEmail(inputText)
{
    var email = /^\w+([\.-]?\w+)*@\w+([\.-]?\w+)*(\.\w{2,3})+$/;
    if(inputText.value.match(email))
        {
            alert("Valid email address!");
            return true;
        }
    else
    {
        alert("Invalid email address!");
        return false;
    }
}
```

I ovanstående exempel anropas den anpassade funktionen &quot;ValidateEmail&quot; för att kontrollera om den angivna e-postadressen är giltig när användaren försöker skicka formuläret.

## Användning av anpassade funktioner {#uses-of-custom-function}

Fördelarna med att använda anpassade funktioner i Adaptive Forms är:

* **Hantering av data**: Anpassade funktioner hanterar och bearbetar data som anges i formulärfälten.
* **Validering av data**: Med anpassade funktioner kan du utföra anpassade kontroller av formulärindata och tillhandahålla angivna felmeddelanden.
* **Dynamiskt beteende**: Med anpassade funktioner kan du styra formulärens dynamiska beteende baserat på specifika villkor. Du kan till exempel visa/dölja fält, ändra fältvärden eller justera formulärlogiken dynamiskt.
* **Integrering**: Du kan använda anpassade funktioner för att integrera med externa API:er eller tjänster. Det hjälper till att hämta data från externa källor, skicka data till externa Rest-slutpunkter eller utföra anpassade åtgärder baserade på externa händelser.

## JS-anteckningar som stöds

Se till att den anpassade funktionen som du skriver åtföljs av `jsdoc` ovan, om du behöver en anpassad konfiguration och beskrivning. Det finns flera sätt att deklarera en funktion i `JavaScript,` och kommentarer gör att du kan hålla reda på funktionerna. Mer information finns i [usejsdoc.org](https://jsdoc.app/).

Stöds `jsdoc` taggar:

* **Privat**
Syntax: `@private`
En privat funktion ingår inte som en anpassad funktion.

* **Namn**
Syntax: `@name funcName <Function Name>`
Alternativt `,` du kan använda: `@function funcName <Function Name>` **eller** `@func` `funcName <Function Name>`.
  `funcName` är namnet på funktionen (inga blanksteg tillåts).
  `<Function Name>` är funktionens visningsnamn.

* **medlem**
Syntax: `@memberof namespace`
Kopplar ett namnutrymme till funktionen.

* **Parameter**
Syntax: `@param {type} name <Parameter Description>`
Du kan också använda: `@argument` `{type} name <Parameter Description>` **eller** `@arg` `{type}` `name <Parameter Description>`.
Visar parametrar som används av funktionen. En funktion kan ha flera parametertaggar, en tagg för varje parameter i ordningen för förekomst.
  `{type}` representerar parametertyp. Tillåtna parametertyper är:

   1. string
   2. tal
   3. boolesk
   4. omfång

  Omfång används för att referera till fält i ett adaptivt formulär. När ett formulär använder lazy loading kan du använda `scope` för att komma åt fälten. Du kan komma åt fält antingen när fälten har lästs in eller om fälten har markerats som globala.

  Alla andra parametertyper kategoriseras under någon av ovanstående. Ingen stöds inte. Välj en av typerna ovan. Typer är inte skiftlägeskänsliga. Blanksteg tillåts inte i parametern `name`. `<Parameter Descrption>` `<parameter>  can have multiple words. </parameter>`

* **Returtyp**
Syntax: `@return {type}`
Du kan också använda `@returns {type}`.
Lägger till information om funktionen, till exempel dess mål.
{type} representerar funktionens returtyp. Följande returtyper tillåts:

   1. string
   1. tal
   1. boolesk

  Alla andra returtyper kategoriseras under en av ovanstående. Ingen stöds inte. Välj en av typerna ovan. Returtyperna är inte skiftlägeskänsliga.

* **Detta**
Syntax: `@this currentComponent`

  Använd @this för att referera till den adaptiva formulärkomponenten som regeln är skriven för.

  Följande exempel baseras på fältvärdet. I följande exempel döljer regeln ett fält i formuläret. The `this` del av `this.value` refererar till den underliggande adaptiva formulärkomponenten, som regeln är skriven för.

  ```
     /**
     * @function myTestFunction
     * @this currentComponent
     * @param {scope} scope in which code inside function will be executed.
     */
     myTestFunction = function (scope) {
        if(this.value == "O"){
              scope.age.visible = true;
        } else {
           scope.age.visible = false;
        }
     }
  ```

  >[!NOTE]
  >
  >Kommentarer före anpassade funktioner används för sammanfattning. Sammanfattningen kan sträcka sig över flera rader tills en tagg påträffas. Begränsa storleken till en enda storlek om du vill ha en kortfattad beskrivning i regelbyggaren.

## Typer som stöds för funktionsdeklaration {#function-declaration-supported-types}

**Funktionssats**

```javascript
function area(len) {
    return len*len;
}
```

Den här funktionen ingår utan `jsdoc` kommentarer.

**Funktionsuttryck**

```javascript
var area;
//Some codes later
/** */
area = function(len) {
    return len*len;
};
```

**Funktionsuttryck och -programsats**

```javascript
var b={};
/** */
b.area = function(len) {
    return len*len;
}
```

**Funktionsdeklaration som variabel**

```javascript
/** */
var x1,
    area = function(len) {
        return len*len;
    },
    x2 =5, x3 =true;
```

Begränsning: den anpassade funktionen väljer bara den första funktionsdeklarationen från variabellistan, om den används tillsammans. Du kan använda funktionsuttryck för varje deklarerad funktion.

**Funktionsdeklaration som objekt**

```javascript
var c = {
    b : {
        /** */
        area : function(len) {
            return len*len;
        }
    }
};
```

## Skapa anpassad funktion {#create-custom-function}

Så här skapar du en anpassad funktion:

1. Logga in `http://server:port/crx/de/index.jsp#`.
1. Skapa en mapp under `/apps` mapp. Skapa till exempel en mapp med namnet som `experience-league`.
1. Spara ändringarna.
1. Navigera till den skapade mappen och skapa en nod av typen `cq:ClientLibraryFolder` as `clientlibs`.
1. Navigera till den nyskapade `clientlibs` mapp och lägg till `allowProxy` och `categories` egenskaper:

   ![Egenskaper för anpassad biblioteksnod](/help/forms/using/assets/customlibrary-catproperties.png)

   >[!NOTE]
   >
   > Du kan ange valfritt namn i stället för `customfunctionsdemo`.

1. Spara ändringarna.

1. Skapa en mapp med namnet `js` under `clientlibs` mapp.
1. Skapa en JavaScript-fil med namnet `functions.js` under `js` mapp
1. Skapa en fil med namnet `js.txt` under `clientlibs` mapp.
1. Spara ändringarna.
Den skapade mappstrukturen ser ut så här:

   ![Mappstruktur för klientbibliotek har skapats](/help/forms/using/assets/clientlibrary_folderstructure.png)
1. Dubbelklicka på `functions.js` för att öppna redigeraren. Filen innehåller koden för den anpassade funktionen.
Låt oss lägga till följande kod i JavaScript-filen för att beräkna ålder baserat på födelsedatum (ÅÅÅÅ-MM-DD).

   ```javascript
       /**
            * Calculates Age
            * @name calculateAge 
            * @return {string} 
       */
   
       function calculateAge(dateOfBirthString) {
       var dob = new Date(dateOfBirthString);
       var now = new Date();
   
       var age = now.getFullYear() - dob.getFullYear();
       var monthDiff = now.getMonth() - dob.getMonth();
   
       if (monthDiff < 0 || (monthDiff === 0 && now.getDate() < dob.getDate())) {
       age--;
       }
   
       return age;
       }
   ```

1. Spara `function.js`.
1. Navigera till `js.txt` och lägg till följande kod:

   ```javascript
       #base=js
       functions.js
   ```

1. Spara `js.txt` -fil.

Du kan se följande [anpassad funktion](/help/forms/using/assets/customfunction.zip) mapp. Hämta och installera den här mappen i AEM.

Nu kan du använda den anpassade funktionen i ditt adaptiva formulär genom att lägga till klientbiblioteket.

## Lägga till klientbibliotek i ett adaptivt formulär{#use-custom-function}

När du har distribuerat klientbiblioteket till Forms CS-miljön kan du använda funktionerna i ditt adaptiva formulär. Lägga till klientbiblioteket i ditt adaptiva formulär

1. Öppna formuläret i redigeringsläge. Om du vill öppna ett formulär i redigeringsläge markerar du ett formulär och väljer **[!UICONTROL Edit]**.
1. Öppna innehållsläsaren och välj **[!UICONTROL Guide Container]** som ingår i det adaptiva formuläret.
1. Klicka på egenskapsikonen för Guide Container. Dialogrutan Adaptiv formulärbehållare öppnas.
1. Öppna **[!UICONTROL Basic]** och välj namnet på **[!UICONTROL client library category]** från listrutan (i det här fallet väljer `customfunctionscategory`).

   ![Lägga till klientbiblioteket för anpassade funktioner](/help/forms/using//assets/custom-function-category-name-core-component.png)

1. Klicka **[!UICONTROL Done]** .

Nu kan du skapa en regel som använder anpassade funktioner i regelredigeraren:

![Lägga till klientbiblioteket för anpassade funktioner](/help/forms/using//assets/calculateage-customfunction.png)

Nu ska vi förstå hur man konfigurerar och använder en anpassad funktion med [Regelredigerarens anropstjänst i AEM Forms](/help//forms/using/rule-editor.md).
