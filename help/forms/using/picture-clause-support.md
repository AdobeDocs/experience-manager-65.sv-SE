---
title: Stöd för Picture-sats i HTML5-formulär
seo-title: Stöd för Picture-sats i HTML5-formulär
description: HTML5-formulär har stöd för XFA Picture-satsen för visningsvärde och formaterat värde för datum, text och numeriska symboler.
seo-description: HTML5-formulär har stöd för XFA Picture-satsen för visningsvärde och formaterat värde för datum, text och numeriska symboler.
uuid: ca5074ce-8219-4f27-a37c-b1f0dca4ce03
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 5e344be7-46cd-4e1f-ae3a-1f89c645cffe
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Stöd för Picture-sats i HTML5-formulär {#picture-clause-support-for-html-forms}

HTML5-formulär har stöd för XFA Picture-satsen för visningsvärde och formaterat värde för datum, text och numeriska symboler. Följande Picture-satsuttryck stöds:

* category(locale){picture-clause}| category(locale){picture-clause}| category(locale){picture-clause}
* category.subcategory{{}

>[!NOTE]
>
>För närvarande stöder inte Mobile Forms Redigera bild-satsen. Symboler för DateTime- och Time Picture-satser stöds inte heller.

## Symboler för datumfält som stöds {#supported-date-field-symbols}

Uttryck som stöds för satsen Date Picture:

* date.long{}
* date.short{}
* date.medium{}
* date.full{}
* date.short{}
* date{date Picture Clause symbols}

>[!NOTE]
>
>Standardmönstret för bildsatsen är mönstret {MMM D, YYYY} . Om inget mönster används används standardmönstret.

<table>
 <tbody>
  <tr>
   <th><strong>Symbol</strong></th>
   <th>Tolkning</th>
  </tr>
  <tr>
   <td>D</td>
   <td>Dag i månaden med en eller två siffror (1-31)</td>
  </tr>
  <tr>
   <td>DD</td>
   <td>Zero-padded two digit (01-31) day of the month.<br /> </td>
  </tr>
  <tr>
   <td>M</td>
   <td>1- or 2-digit (1-12) month of the year.<br /> </td>
  </tr>
  <tr>
   <td>MM</td>
   <td>Månad med två siffror (01-12) med inledande nolla vid behov.<br /> </td>
  </tr>
  <tr>
   <td>MMM</td>
   <td>Förkortat månadsnamn för aktuell språkinställning<br /> </td>
  </tr>
  <tr>
   <td>MMMM</td>
   <td>Fullständigt månadsnamn för det aktuella språkområdet<br /> </td>
  </tr>
  <tr>
   <td>EEE</td>
   <td>Förkortat veckodagsnamn för aktuell språkinställning<br /> </td>
  </tr>
  <tr>
   <td>EEEE</td>
   <td>Fullständigt veckodagsnamn för det aktuella språkområdet<br /> </td>
  </tr>
  <tr>
   <td>YY</td>
   <td>Tvåsiffrigt årtal, där 00 = 2000, 29 = 2029, 30 = 1930 och 99 = 1999<br /> </td>
  </tr>
  <tr>
   <td>YYYY</td>
   <td>Fyrsiffrigt årtal<br /> </td>
  </tr>
 </tbody>
</table>

## Numerisk bildsats {#numeric-picture-clause}

HTML5-formulär har stöd för numeriska bildsymboler. Det finns dock en skillnad i stöd mellan PDF-formulär och HTML-formulär.

I **PDF-formulär** formateras ett tal oavsett antalet symboler i Picture-satsen har

I **HTML-formulär** formateras ett tal bara om talet har siffror som är mindre än antalet symboler i Picture-satsen.

**Exempel**: Överväg en Picture-sats: num{zzz,zzz,zz9}.

Talet **10000** formateras som **10 000** i både HTML- och PDF-formulär.

Talet 1000000 formateras som 1 000 000 i PDF-formulär. I HTML-formulär förblir dock talet oformaterat som 100000.

Uttrycken som stöds för Numeric Picture-satsen i **HTML-formulär** är:

* num.integer{}
* num.decimal{}
* num.currency{}
* num.percent{}
* num{Numeric Picture Clause Symbols}

<table>
 <tbody>
  <tr>
   <th><strong>Symbol</strong></th>
   <th><strong>Tolkning</strong></th>
   <th>Indataparsning</th>
  </tr>
  <tr>
   <td>9</td>
   <td><strong>Utdataformatering</strong>: en enda siffra. Eller för siffran noll om indata är tomma eller ett blanksteg i motsvarande position.<br /> </td>
   <td>Enstaka siffra</td>
  </tr>
  <tr>
   <td>Z</td>
   <td><strong>Utdataformatering</strong>: en enda siffra. Eller för ett blanksteg om indata är tomma, ett blanksteg eller siffran noll i motsvarande position.<br /> </td>
   <td>Ensiffrigt eller mellanslag</td>
  </tr>
  <tr>
   <td>z</td>
   <td><strong>Utdataformatering</strong>: en enda siffra. Eller för ingenting om indata är tomma, ett blanksteg eller siffran noll i motsvarande position.<br /> </td>
   <td>En siffra eller ingenting</td>
  </tr>
  <tr>
   <td>E</td>
   <td><strong>Utdataformatering</strong>: exponentdelen av ett flyttal bestående av exponentialsymbolen (E). Följd av ett valfritt plustecken eller minustecken. Följs av exponentvärdet.<br /> </td>
   <td>Samma som för utdataformatering</td>
  </tr>
  <tr>
   <td>CR eller cr<br /> </td>
   <td>Kreditsymbol (CR) om talet är negativt. Annars ingenting.</td>
   <td><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>S eller s<br /> </td>
   <td>Utdataformatering: ett minustecken om talet är negativt. Annars utrymme.<br /> </td>
   <td>Minustecken om talet är negativt. Plustecken om talet är positivt</td>
  </tr>
  <tr>
   <td>V</td>
   <td>Decimalradix för den aktuella språkinställningen. Tillåter att decimalbasen används vid indataparsning.</td>
   <td><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>v</td>
   <td>Decimalradix för den aktuella språkinställningen. Det är tillåtet att använda decimalbasen vid indataparsning och utdataformatering.</td>
   <td><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>.</td>
   <td>Decimalradix för den aktuella språkinställningen.</td>
   <td><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>, (U+FF0C)</td>
   <td>Grupperingsavgränsare för den aktuella språkinställningen</td>
   <td><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>$ (U+FF04)</td>
   <td>Valutasymbol för det aktuella språkområdet.</td>
   <td><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>% (U+FF05)</td>
   <td>Procentsymbol för det aktuella språkområdet.</td>
   <td><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>( (U+FF08)</td>
   <td>Vänsterparentes om talet är negativt. Annars utrymme.</td>
   <td><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>) (U+FF09)</td>
   <td>Högerparentes om talet är negativt. Annars utrymme.</td>
   <td><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>t</td>
   <td>Tabbtecken</td>
   <td><br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

## Textbildsats {#text-picture-clause}

HTML5-formulär har stöd för följande Text Picture-satsuttryck:

* text{text Picture-satssymboler}

| **Symbol** | **Tolkning** |
|---|---|
| A | Enstaka alfabetiskt tecken. |
| X | Enstaka tecken. |
| O | Enstaka alfanumeriskt tecken. |
| 0 (noll) | Enstaka alfanumeriskt tecken. |
| 9 | Enstaka siffra. |

**[Kontakta supporten](https://www.adobe.com/account/sign-in.supportportal.html)**
