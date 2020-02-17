---
title: Skapa anpassningsbara formulär med JSON-schema
seo-title: Skapa anpassningsbara formulär med JSON-schema
description: Anpassningsbara formulär kan använda JSON-schema som formulärmodell, vilket gör att du kan använda befintliga JSON-scheman för att skapa anpassningsbara formulär.
seo-description: Anpassningsbara formulär kan använda JSON-schema som formulärmodell, vilket gör att du kan använda befintliga JSON-scheman för att skapa anpassningsbara formulär.
uuid: bdeaeae8-65a3-4c46-b27d-fe68481e31f1
topic-tags: develop
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 375ba8fc-3152-4564-aec5-fcff2a95cf4c
docset: aem65
translation-type: tm+mt
source-git-commit: 4ecf5efc568cd21f11801a71d491c3d75ca367fe

---


# Skapa anpassningsbara formulär med JSON-schema{#creating-adaptive-forms-using-json-schema}

## Förutsättningar {#prerequisites}

Om du skapar ett anpassat formulär med ett JSON-schema som formulärmodell måste du ha grundläggande kunskaper i JSON-schemat. Du bör läsa igenom följande innehåll före den här artikeln.

* [Skapa ett anpassat formulär](../../forms/using/creating-adaptive-form.md)
* [JSON-schema](https://json-schema.org/)

## Använda ett JSON-schema som formulärmodell {#using-a-json-schema-as-form-model}

AEM Forms har stöd för att skapa ett anpassningsbart formulär genom att använda ett befintligt JSON-schema som formulärmodell. Detta JSON-schema representerar strukturen i vilken data produceras eller används av det bakomliggande systemet i din organisation. Det JSON-schema som du använder ska vara kompatibelt med [v4-specifikationerna](https://json-schema.org/draft-04/schema).

De viktigaste funktionerna i ett JSON-schema är:

* Strukturen för JSON visas som ett träd på fliken Innehållssökning i redigeringsläget för ett anpassat formulär. Du kan dra och lägga till element från JSON-hierarkin i det adaptiva formuläret.
* Du kan fylla i formuläret i förväg med JSON som är kompatibel med det associerade schemat.
* När data skickas skickas skickas de som anges av användaren som JSON som är anpassad efter det associerade schemat.

Ett JSON-schema består av enkla och komplexa elementtyper. Elementen har attribut som lägger till regler i elementet. När dessa element och attribut dras till ett adaptivt formulär mappas de automatiskt till motsvarande adaptiv formulärkomponent.

Den här mappningen av JSON-element med adaptiva formulärkomponenter är följande:

```
"birthDate": {
              "type": "string",
              "format": "date",
              "pattern": "date{DD MMMM, YYYY}",
              "aem:affKeyword": [
                "DOB",
                "Date of Birth"
              ],
              "description": "Date of birth in DD MMMM, YYYY",
              "aem:afProperties": {
                "displayPictureClause": "date{DD MMMM, YYYY}",
                "displayPatternType": "date{DD MMMM, YYYY}",
                "validationPatternType": "date{DD MMMM, YYYY}",
                "validatePictureClause": "date{DD MMMM, YYYY}",
                "validatePictureClauseMessage": "Date must be in DD MMMM, YYYY format."
              }
```

<table>
 <tbody>
  <tr>
   <th><strong>JSON-element, egenskaper eller attribut</strong></th>
   <th><strong>Adaptiv formkomponent</strong></th>
  </tr>
  <tr>
   <td><p>Strängegenskaper med enum- och enumNames-begränsningen.</p> <p>Syntax,</p> <p> <code>{</code></p> <p><code>"type" : "string",</code></p> <p><code>"enum" : ["M", "F"]</code></p> <p><code>"enumNames" : ["Male", "Female"]</code></p> <p><code>}</code></p> <p> </p> </td>
   <td><p>Nedrullningsbar komponent:</p>
    <ul>
     <li>Värden som anges i enumNames visas i listrutan.</li>
     <li>Värden som anges i uppräkningen används för beräkning.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>Strängegenskap med formatbegränsning. Till exempel e-post och datum.</p> <p>Syntax,</p> <p><code>{</code></p> <p><code>"type" : "string",</code></p> <p><code>"format" : "email"</code></p> <p><code>}</code></p> <p> </p> </td>
   <td>
    <ul>
     <li>E-postkomponenten mappas när typen är sträng och formatet är e-post.</li>
     <li>Textrutekomponent med validering mappas när typen är sträng och formatet är värdnamn.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>{</p> <p>"type" : "string",</p> <p>}</p> </td>
   <td><br /> <br /> Textfält<br /> <br /> <br /> </td>
  </tr>
  <tr>
   <td>number, egenskap<br /> </td>
   <td>Numeriskt fält med undertyp inställd på flytande<br /> </td>
  </tr>
  <tr>
   <td>heltalsegenskap<br /> </td>
   <td>Numeriskt fält med subtyp inställd på heltal<br /> </td>
  </tr>
  <tr>
   <td>boolesk egenskap<br /> </td>
   <td>Switch<br /> </td>
  </tr>
  <tr>
   <td>object, egenskap<br /> </td>
   <td>Panel<br /> </td>
  </tr>
  <tr>
   <td>arrayegenskap</td>
   <td>Upprepningsbar panel med min och max lika med minItems respektive maxItems. Endast homogena arrayer stöds. Objektbegränsningen måste därför vara ett objekt och inte en array.<br /> </td>
  </tr>
 </tbody>
</table>

### Vanliga schemaegenskaper {#common-schema-properties}

Det adaptiva formuläret använder information som finns i JSON-schemat för att mappa varje genererat fält. Särskilt gäller följande:

* Egenskapen title fungerar som etikett för de adaptiva formulärkomponenterna.
* Egenskapen description anges som lång beskrivning för en adaptiv formulärkomponent.
* Egenskapen default fungerar som ett initialt värde i ett adaptivt formulärfält.
* Egenskapen maxLength anges som maxlength-attribut för textfältskomponenten.
* Egenskaperna minimum, maximum, exclusiveMinimum och exclusiveMaximum används för Numeric box-komponenter.
* Ytterligare JSON-schemaegenskaper minDate och maxDate anges som stöd för intervall för DatePicker-komponenten.
* Egenskaperna minItems och maxItems används för att begränsa antalet objekt/fält som kan läggas till eller tas bort från en panelkomponent.
* Egenskapen readOnly anger det skrivskyddade attributet för en adaptiv formulärkomponent.
* Den obligatoriska egenskapen anger att det adaptiva formulärfältet är obligatoriskt, medan det för panel (där typen är objekt) finns fält med tomma värden som motsvarar det objektet i de slutliga skickade JSON-data.
* Egenskapen pattern anges som valideringsmönster (reguljärt uttryck) i adaptiv form.
* Tillägget för JSON-schemafilen måste behållas som .schema.json. Till exempel &lt;filnamn>.schema.json.

## Exempel på JSON-schema {#sample-json-schema}

Här är ett exempel på ett JSON-schema.

```
{
 "$schema": "https://json-schema.org/draft-04/schema#",
 "definitions": {
  "employee": {
   "type": "object",
   "properties": {
    "userName": {
     "type": "string"
    },
    "dateOfBirth": {
     "type": "string",
     "format": "date"
    },
    "email": {
     "type": "string",
     "format": "email"
    },
    "language": {
     "type": "string"
    },
    "personalDetails": {
     "$ref": "#/definitions/personalDetails"
    },
    "projectDetails": {
     "$ref": "#/definitions/projectDetails"
    }
   },
   "required": [
    "userName",
    "dateOfBirth",
    "language"
   ]
  },
  "personalDetails": {
   "type": "object",
   "properties": {
    "GeneralDetails": {
     "$ref": "#/definitions/GeneralDetails"
    },
    "Family": {
     "$ref": "#/definitions/Family"
    },
    "Income": {
     "$ref": "#/definitions/Income"
    }
   }
  },
  "projectDetails": {
   "type": "array",
   "items": {
    "properties": {
     "name": {
      "type": "string"
     },
     "age": {
      "type": "number"
     },
     "projects": {
      "$ref": "#/definitions/projects"
     }
    }
   },
   "minItems": 1,
   "maxItems": 4
  },
  "projects": {
   "type": "array",
   "items": {
    "properties": {
     "name": {
      "type": "string"
     },
     "age": {
      "type": "number"
     },
     "projectsAdditional": {
      "$ref": "#/definitions/projectsAdditional"
     }
    }
   },
   "minItems": 1,
   "maxItems": 4
  },
  "projectsAdditional": {
   "type": "array",
   "items": {
    "properties": {
     "Additional_name": {
      "type": "string"
     },
     "Additional_areacode": {
      "type": "number"
     }
    }
   },
   "minItems": 1,
   "maxItems": 4
  },
  "GeneralDetails": {
   "type": "object",
   "properties": {
    "age": {
     "type": "number"
    },
    "married": {
     "type": "boolean"
    },
    "phone": {
     "type": "number",
     "aem:afProperties": {
      "sling:resourceType": "/libs/fd/af/components/guidetelephone",
      "guideNodeClass": "guideTelephone"
     }
    },
    "address": {
     "type": "string"
    }
   }
  },
  "Family": {
   "type": "object",
   "properties": {
    "spouse": {
     "$ref": "#/definitions/spouse"
    },
    "kids": {
     "$ref": "#/definitions/kids"
    }
   }
  },
  "Income": {
   "type": "object",
   "properties": {
    "monthly": {
     "type": "number"
    },
    "yearly": {
     "type": "number"
    }
   }
  },
  "spouse": {
   "type": "object",
   "properties": {
    "name": {
     "type": "string"
    },
    "Income": {
     "$ref": "#/definitions/Income"
    }
   }
  },
  "kids": {
   "type": "array",
   "items": {
    "properties": {
     "name": {
      "type": "string"
     },
     "age": {
      "type": "number"
     }
    }
   },
   "minItems": 1,
   "maxItems": 4
  }
 },
 "type": "object",
 "properties": {
  "employee": {
   "$ref": "#/definitions/employee"
  }
 }
}
```

### Återanvändbara schemadefinitioner {#reusable-schema-definitions}

Definitionsnycklar används för att identifiera återanvändbara scheman. Återanvändbara schemadefinitioner används för att skapa fragment. Det liknar att identifiera komplexa typer i XSD. Ett exempel på JSON-schema med definitioner ges nedan:

```
{
  "$schema": "https://json-schema.org/draft-04/schema#",

  "definitions": {
    "address": {
      "type": "object",
      "properties": {
        "street_address": { "type": "string" },
        "city":           { "type": "string" },
        "state":          { "type": "string" }
      },
      "required": ["street_address", "city", "state"]
    }
  },

  "type": "object",

  "properties": {
    "billing_address": { "$ref": "#/definitions/address" },
    "shipping_address": { "$ref": "#/definitions/address" }
  }
}
```

Exemplet ovan definierar en kundpost där varje kund har både en leveransadress och en faktureringsadress. Adressernas struktur är densamma - adresserna har en gatuadress, ort och delstat - så det är en bra idé att inte duplicera adresserna. Det gör det också enkelt att lägga till och ta bort fält för framtida ändringar.

## Förkonfigurerar fält i JSON-schemadefinition {#pre-configuring-fields-in-json-schema-definition}

Du kan använda egenskapen **aem:afProperties** för att förkonfigurera JSON-schemafältet för att mappa till en anpassad adaptiv formulärkomponent. Ett exempel visas nedan:

```
{
    "properties": {
        "sizeInMB": {
            "type": "integer",
            "minimum": 16,
            "maximum": 512,
            "aem:afProperties" : {
                 "sling:resourceType" : "/apps/fd/af/components/guideTextBox",
                 "guideNodeClass" : "guideTextBox"
             }
        }
    },
    "required": [ "sizeInMB" ],
    "additionalProperties": false
}
```

## Konfigurera skript eller uttryck för formulärobjekt {#configure-scripts-or-expressions-for-form-objects}

JavaScript är uttrycksspråket i adaptiva formulär. Alla uttryck är giltiga JavaScript-uttryck och använder API:er för skriptmodell för adaptiva formulär. Du kan förkonfigurera formulärobjekt för att [utvärdera ett uttryck](../../forms/using/adaptive-form-expressions.md) i en formulärhändelse.

Använd egenskapen aem:afproperties för att förkonfigurera adaptiva formuläruttryck eller skript för adaptiva formulärkomponenter. När initialize-händelsen till exempel aktiveras, ställer koden nedan in värdet för telefonfältet och skriver ut ett värde till loggen:

```
"telephone": {
  "type": "string",
  "pattern": "/\\d{10}/",
  "aem:affKeyword": ["phone", "telephone","mobile phone", "work phone", "home phone", "telephone number", "telephone no", "phone number"],
  "description": "Telephone Number",
  "aem:afProperties" : {
    "sling:resourceType" : "fd/af/components/guidetelephone",
    "guideNodeClass" : "guideTelephone",
    "events": {
      "Initialize" : "this.value = \"1234567890\"; console.log(\"ef:gh\") "
    }
  }
}
```

Du bör vara medlem i gruppen [](/help/forms/using/forms-groups-privileges-tasks.md) forms-power-user för att konfigurera skript eller uttryck för formulärobjektet. Tabellen nedan visar alla skripthändelser som stöds för en adaptiv formulärkomponent.

<table>
 <tbody>
  <tr>
   <th><strong></strong>Komponent \ Event</th>
   <th>initialize <br /> </th>
   <td>Beräkna</td>
   <td>Synlighet</td>
   <td>Validera</td>
   <td>Aktiverad</td>
   <td>Bekräfta värde</td>
   <td>Klicka </td>
   <td>Alternativ</td>
  </tr>
  <tr>
   <td>Textfält</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Numeriskt fält</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Numerisk stege</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Alternativknapp</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Telefonnummer</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Byt</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Knapp</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
  </tr>
  <tr>
   <td>Kryssruta</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
  </tr>
  <tr>
   <td>Nedrullningsbar</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
  </tr>
  <tr>
   <td>Bildval</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
  </tr>
  <tr>
   <td>Datumindatafält</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Datumväljaren</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>E-post</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Bifogad fil</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Bild</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Rita</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Panel</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td> </td>
  </tr>
 </tbody>
</table>

Några exempel på hur du använder händelser i en JSON är att dölja ett fält vid initialize-händelsen och konfigurera värdet för ett annat fält vid värdestarthändelse. Mer information om hur du skapar uttryck för skripthändelserna finns i [Adaptiva formuläruttryck](../../forms/using/adaptive-form-expressions.md).

Här är JSON-exempelkoden för de tidigare nämnda exemplen.

### Dölja ett fält vid händelsen initialize {#hiding-a-field-on-initialize-event}

```
"name": {
    "type": "string",
    "aem:afProperties": {
        "events" : {
            "Initialize" : "this.visible = false;"
        }
    }
}
```

#### Konfigurera värdet för ett annat fält för värdeimplementeringshändelsen {#configure-value-of-another-field-on-value-commit-event}

```
"Income": {
    "type": "object",
    "properties": {
        "monthly": {
            "type": "number",
            "aem:afProperties": {
                "events" : {
                    "Value Commit" : "IncomeYearly.value = this.value * 12;"
                }
            }
        },
        "yearly": {
            "type": "number",
            "aem:afProperties": {
                "name": "IncomeYearly"
            }
        }
    }
}
```

## Begränsa tillåtna värden för en adaptiv formulärkomponent {#limit-acceptable-values-for-an-adaptive-form-component}

Du kan lägga till följande begränsningar i JSON-schemaelement för att begränsa vilka värden som tillåts för en adaptiv formulärkomponent:

<table>
 <tbody>
  <tr>
   <td><p><strong> Schemaegenskap</strong></p> </td>
   <td><p><strong>Datatyp</strong></p> </td>
   <td><p><strong>Beskrivning</strong></p> </td>
   <td><p><strong>Komponent</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>maximum</code></p> </td>
   <td><p>Sträng</p> </td>
   <td><p>Anger den övre gränsen för numeriska värden och datum. Som standard inkluderas maxvärdet.</p> </td>
   <td>
    <ul>
     <li>Numerisk ruta</li>
     <li>Numerisk stege<br /> </li>
     <li>Datumväljaren</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>minimum</code></p> </td>
   <td><p>Sträng</p> </td>
   <td><p>Anger den nedre gränsen för numeriska värden och datum. Som standard inkluderas minimivärdet.</p> </td>
   <td>
    <ul>
     <li>Numerisk ruta</li>
     <li>Numerisk stege</li>
     <li>Datumväljaren</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>exclusiveMaximum</code></p> </td>
   <td><p>Boolesk</p> </td>
   <td><p>Om true måste det numeriska värdet eller datumet som anges i formulärets komponent vara mindre än det numeriska värdet eller datumet som anges för egenskapen maximum.</p> <p>Om värdet är false måste det numeriska värdet eller datumet som anges i formulärets komponent vara mindre än eller lika med det numeriska värdet eller datumet som anges för egenskapen maximum.</p> </td>
   <td>
    <ul>
     <li>Numerisk ruta</li>
     <li>Numerisk stege</li>
     <li>Datumväljaren</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>exclusiveMinimum</code></p> </td>
   <td><p>Boolesk</p> </td>
   <td><p>Om true måste det numeriska värdet eller datumet som anges i formulärets komponent vara större än det numeriska värdet eller datumet som anges för egenskapen minimum.</p> <p>Om värdet är false måste det numeriska värdet eller datumet som anges i formulärets komponent vara större än eller lika med det numeriska värdet eller datumet som anges för egenskapen minimum.</p> </td>
   <td>
    <ul>
     <li>Numerisk ruta</li>
     <li>Numerisk stege</li>
     <li>Datumväljaren</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>minLength</code></p> </td>
   <td><p>Sträng</p> </td>
   <td><p>Anger det minsta antalet tecken som tillåts i en komponent. Minimilängden måste vara lika med eller större än noll.</p> </td>
   <td>
    <ul>
     <li>Textruta</li>
    </ul> </td>
  </tr>
  <tr>
   <td><code>maxLength</code></td>
   <td>Sträng</td>
   <td>Anger maximalt antal tecken som tillåts i en komponent. Den maximala längden måste vara lika med eller större än noll.</td>
   <td>
    <ul>
     <li>Textruta</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>pattern</code></p> </td>
   <td><p>Sträng</p> </td>
   <td><p>Anger teckensekvensen. En komponent accepterar tecknen om tecknen överensstämmer med det angivna mönstret.</p> <p>Egenskapen pattern mappar till valideringsmönstret för motsvarande adaptiva formulärkomponent.</p> </td>
   <td>
    <ul>
     <li>Alla adaptiva formulärkomponenter som är mappade till ett XSD-schema </li>
    </ul> </td>
  </tr>
  <tr>
   <td>maxItems</td>
   <td>Sträng</td>
   <td>Anger maximalt antal objekt i en array. Det maximala antalet objekt måste vara lika med eller större än noll.</td>
   <td> </td>
  </tr>
  <tr>
   <td>minItems</td>
   <td>Sträng</td>
   <td>Anger det minsta antalet objekt i en array. Minimiobjekten måste vara lika med eller större än noll.</td>
   <td> </td>
  </tr>
 </tbody>
</table>

## Konstruktioner som inte stöds {#non-supported-constructs}

Adaptiva formulär stöder inte följande JSON-schemakonstruktioner:

* Null-typ
* Unionstyper, t.ex., och
* OneOf, AnyOf, AllOf, och NOT
* Endast homogena arrayer stöds. Objektbegränsningen måste därför vara ett objekt och inte en array.

## Frågor och svar {#frequently-asked-questions}

**Varför kan jag inte dra enskilda element i ett delformulär (struktur som genereras från en komplex typ) för repeterbara delformulär (värdena minOcCours och maxOccurs är större än 1)?**

I ett upprepningsbart delformulär måste du använda hela delformuläret. Om du bara vill ha selektiva fält använder du hela strukturen och tar bort de oönskade.

**Jag har en lång komplex struktur i Content Finder. Hur hittar jag ett specifikt element?**

Du har två alternativ:

* Bläddra genom trädstrukturen
* Använd sökrutan för att hitta ett element

**Vad ska tillägget för JSON-schemafilen vara?**

Tillägget för JSON-schemafilen måste vara .schema.json. Till exempel &lt;filnamn>.schema.json.
