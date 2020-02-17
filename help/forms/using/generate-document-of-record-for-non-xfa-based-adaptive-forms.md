---
title: Generera arkivdokument för anpassningsbara formulär
seo-title: Generera arkivdokument för anpassningsbara formulär
description: Beskriver hur du kan generera en mall för ett postdokument (DoR) för adaptiva formulär.
seo-description: Beskriver hur du kan generera en mall för ett postdokument (DoR) för adaptiva formulär.
uuid: 2dc7e0de-fff9-43fa-9426-e9b047eb2595
content-type: reference
topic-tags: develop
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: ce65cb5f-94ec-4423-9fa9-d617e9703091
docset: aem65
translation-type: tm+mt
source-git-commit: 14975f409a0e17183b3da6bdc5a42c8073080108

---


# Generera arkivdokument för anpassningsbara formulär{#generate-document-of-record-for-adaptive-forms}

## Översikt {#overview}

Efter att ha skickat in ett formulär vill era kunder vanligtvis registrera, i utskrift eller i dokumentformat, den information de har fyllt i formuläret för framtida referens. Detta kallas för ett urkunder.

I den här artikeln beskrivs hur du kan generera ett postdokument för anpassningsbara formulär.

>[!NOTE]
>
>Automatisk generering av urkunder stöds inte för XFA-baserade adaptiva formulär. Du kan dock använda XDP-filen som används för att skapa det adaptiva formuläret som ett arkivdokument.

## Anpassningsbara formulärtyper och deras urkunder {#adaptive-form-types-and-their-documents-of-record}

När du skapar ett anpassat formulär kan du välja en formulärmodell. Dina alternativ är:

* [Formulärmallar](../../forms/using/creating-adaptive-form.md#create-an-adaptive-form-based-on-an-xfa-form-template)Här kan du välja en XFA-mall för ditt adaptiva formulär. När du väljer en XFA-mall kan du använda den associerade XDP-filen för postdokument enligt beskrivningen ovan.

* [XML-schema](../../forms/using/creating-adaptive-form.md#create-an-adaptive-form-based-on-xml-or-json-schema)Gör att du kan välja en XML-schemadefinition för ditt adaptiva formulär. När du väljer ett XML-schema för det anpassade formuläret kan du:

   * Associera en XFA-mall för postdokument. Se till att associerad XFA-mall använder samma XML-schema som ditt adaptiva formulär
   * Generera urkunder automatiskt

* IngenDu kan skapa ett anpassat formulär utan en formulärmodell. Registerdokumentet genereras automatiskt för ditt anpassningsbara formulär.

När du väljer en formulärmodell konfigurerar du postdokumentet med de alternativ som finns under Dokumentmallskonfiguration. Se [Dokumentmallskonfiguration](#document-of-record-template-configuration).

## Automatiskt genererat arkivdokument {#automatically-generated-document-of-record}

Med ett urkunder kan kunderna spara en kopia av det inskickade formuläret för utskrift. När du automatiskt genererar ett postdokument uppdateras det automatiskt varje gång du ändrar formuläret. Du kan till exempel ta bort åldersfält för kunder som väljer USA som land. När sådana kunder genererar ett postdokument är åldersfältet inte synligt för dem i postdokumentet.

Automatiskt genererade urkunder har följande fördelar:

* Den tar hand om databindning.
* Fälten som är markerade exkluderar från registreringsdokumentet döljs automatiskt när de skickas. Ingen extra ansträngning krävs.
* Det sparar tid när du utformar dokument för postmallar.
* Du kan prova olika format och utseende med olika basmallar och välja bästa format och utseende för Dokument för post. Det är valfritt att formatera utseenden, och om du inte anger någon formatering anges systemformaten som standard.
* Det säkerställer att alla ändringar i formuläret omedelbart återspeglas i urkunder.

## Komponenter som automatiskt genererar ett postdokument {#components-to-automatically-generate-a-document-of-record}

Om du vill generera ett postdokument för adaptiva formulär behöver du följande komponenter:

**Anpassat formulär** Adaptivt formulär som du vill skapa ett postdokument för.

**Basmall (rekommenderad)** XFA-mall (XDP-fil) skapad i AEM Designer. Basmallen används för att ange formaterings- och varumärkesinformation för postmalldokument.

Se [Basmall för ett postdokument](#base-template-of-a-document-of-record)

>[!NOTE]
>
>Basmallen för ett postdokument kallas också metamall för ett postdokument.

**Dokument med postmall** XFA-mall (XDP-fil) som genereras från ett adaptivt formulär.

Se [Dokumentmallskonfiguration](#document-of-record-template-configuration).

**Formulärdata** Information ifylld av en användare i det anpassade formuläret. Den sammanfogas med postmalldokumentet för att generera postdokumentet.

## Mappning av adaptiva formulärelement {#mapping-of-adaptive-form-elements}

I följande avsnitt beskrivs hur anpassningsbara formulärelement visas i postdokumentet.

### fält {#fields}

<table>
 <tbody>
  <tr>
   <th>Adaptiv formkomponent</th>
   <th>Motsvarande XFA-komponent</th>
   <th>Ingår som standard i dokumentet med postmallen?</th>
   <th>Anteckningar</th>
  </tr>
  <tr>
   <td>Knapp</td>
   <td>Knapp</td>
   <td>false</td>
   <td> </td>
  </tr>
  <tr>
   <td>Kryssruta</td>
   <td>Kryssruta</td>
   <td>true</td>
   <td> </td>
  </tr>
  <tr>
   <td>Datumväljaren</td>
   <td>Datum-/tidfält</td>
   <td>true</td>
   <td> </td>
  </tr>
  <tr>
   <td>Nedrullningsbar lista</td>
   <td>Nedrullningsbar lista</td>
   <td>true</td>
   <td> </td>
  </tr>
  <tr>
   <td>Klottersignatur</td>
   <td>Signature Scribble</td>
   <td>true</td>
   <td> </td>
  </tr>
  <tr>
   <td>Numerisk ruta</td>
   <td>Numeriskt fält</td>
   <td>true</td>
   <td> </td>
  </tr>
  <tr>
   <td>Lösenordsruta</td>
   <td>Lösenordsfält</td>
   <td>false</td>
   <td> </td>
  </tr>
  <tr>
   <td>Alternativknapp</td>
   <td>Alternativknapp</td>
   <td>true</td>
   <td> </td>
  </tr>
  <tr>
   <td>Textruta</td>
   <td>Textfält</td>
   <td>true</td>
   <td> </td>
  </tr>
  <tr>
   <td>Knappen Återställ</td>
   <td>Återställningsknapp</td>
   <td>false</td>
   <td> </td>
  </tr>
  <tr>
   <td>Skicka-knapp</td>
   <td><p>Skicka-knapp för e-post</p> <p>Skicka-knapp (HTTP)</p> </td>
   <td>false</td>
   <td> </td>
  </tr>
  <tr>
   <td>Villkor</td>
   <td> </td>
   <td>true</td>
   <td> </td>
  </tr>
  <tr>
   <td>Bifogad fil</td>
   <td> </td>
   <td>false</td>
   <td>Inte tillgängligt i dokumentet för postmallen. Endast tillgängligt i arkivdokument via bilagor.</td>
  </tr>
 </tbody>
</table>

### Containers {#containers}

<table>
 <tbody>
  <tr>
   <th>Adaptiv formkomponent</th>
   <th>Motsvarande XFA-komponent</th>
   <th>Anteckningar</th>
  </tr>
  <tr>
   <td>Panel<br /> </td>
   <td>Delformulär<br /> </td>
   <td>Upprepningsbara panelmappar till repeterbara delformulär.</td>
  </tr>
 </tbody>
</table>

### Statiska komponenter {#static-components}

| Adaptiv formkomponent | Motsvarande XFA-komponent | Anteckningar |
|---|---|---|
| Bild | Bild | TextDraw- och Image-komponenterna, oavsett om de är bundna eller obundna, visas alltid i postdokumentet för ett XSD-baserat anpassningsbart formulär, såvida de inte utelämnas med hjälp av postinställningsdokumentet. |
| Text | Text |

>[!NOTE]
>
>I det klassiska användargränssnittet finns det olika flikar för redigering av fältegenskaper.

### Tabeller {#tables}

De adaptiva formulärtabellkomponenterna som sidhuvud, sidfot och radmappning till motsvarande XFA-komponenter. Du kan mappa upprepningsbara paneler till tabeller i ett postdokument.

## Basmall för ett postdokument {#base-template-of-a-document-of-record}

Basmallen innehåller formaterings- och utseendeinformation för urkunder. Du kan anpassa standardutseendet för automatiskt genererade postdokument. Du vill till exempel lägga till företagets logotyp i sidhuvudet och copyrightinformation i sidfoten i postdokumentet. Mallsidan från basmallen används som mallsida för postmalldokument. Mallsidan kan innehålla information som sidhuvud, sidfot och sidnummer som du kan använda på postdokument. Du kan använda sådan information för att dokumentera med hjälp av basmallen för automatisk generering av postdokument. Med hjälp av basmallen kan du ändra standardegenskaperna för fält.

Följ [Basmallskonventionerna](#base-template-conventions) när du designar basmallen.

## Grundmallskonventioner {#base-template-conventions}

En basmall används för att definiera sidhuvud, sidfot, format och utseende för ett postdokument. Sidhuvudet och sidfoten kan innehålla information som företagets logotyp och copyrighttext. Den första mallsidan i basmallen kopieras och används som mallsida för postdokumentet, som innehåller sidhuvud, sidfot, sidnummer eller annan information som ska visas på alla sidor i postdokumentet. Om du använder en basmall som inte överensstämmer med basmallskonventioner, används den första mallsidan från basmallen fortfarande i postmalldokumentet. Vi rekommenderar att du utformar din basmall enligt dess konventioner och använder den för automatisk generering av arkivdokument.

**Konventioner för mallsidor**

* I basmallen ska du ge rotdelformuläret ett namn som `AF_METATEMPLATE` och mallsidan som `AF_MASTERPAGE`.

* Mallsidan med namnet `AF_MASTERPAGE` under `AF_METATEMPLATE` rotdelformuläret har en inställning för att extrahera sidhuvud, sidfot och formatinformation.

* Om den inte `AF_MASTERPAGE` finns används den första mallsidan i basmallen.

**Formatkonventioner för fält**

* Om du vill använda format på fälten i postdokumentet innehåller basmallen fält som finns i `AF_FIELDSSUBFORM` delformuläret under `AF_METATEMPLATE` rotdelformuläret.

* Egenskaperna för dessa fält används för fälten i postdokumentet. Dessa fält bör följa `AF_<name of field in all caps>_XFO` namnkonventionen. Fältnamnet för kryssrutan ska till exempel vara `AF_CHECKBOX_XFO`.

Så här skapar du en basmall i AEM Designer.

1. Klicka på **Arkiv > Nytt**.
1. Välj alternativet **Baserat på en mall** .

1. Välj kategorin **Formulär - postdokument** .
1. Välj **DoR-basmall**.
1. Klicka på **Nästa** och ange nödvändig information.

1. (Valfritt) Ändra format och utseende på fält som du vill använda i fälten i postdokumentet.
1. Spara formuläret.

Du kan nu använda det sparade formuläret som en basmall för postdokument.
Ändra eller ta inte bort några skript som finns i basmallen.

**Ändra basmall**

* Om du inte använder någon formatering över fält i basmallen bör du ta bort dessa fält från basmallen så att eventuella uppgraderingar av basmallen automatiskt hämtas.
* När du ändrar basmallen ska du inte ta bort, lägga till eller ändra skript.

>[!NOTE]
>
>Utforma en basmall enligt konventioner och följ stegen ovan.

## Konfiguration av dokumentmall {#document-of-record-template-configuration}

Konfigurera dokumentets postmall för formuläret så att kunderna kan hämta en utskriftsvänlig kopia av det skickade formuläret. En XDP-fil fungerar som ett dokument i postmallen. Dokumentet med nedladdade postkunder formateras enligt layouten som anges i XDP-filen.

Utför följande steg för att konfigurera ett postdokument för adaptiva formulär:

1. I AEM-författarinstansen klickar du på **Formulär > Formulär och dokument.**
1. Markera ett formulär och klicka på **Visa egenskaper**.
1. Tryck på **Formulärmodell**i fönstret Egenskaper.
Du kan också välja en formulärmodell när du skapar ett formulär.

   >[!NOTE]
   >
   >På fliken Formulärmodell väljer du **Schema** eller **Inget** i listrutan **Välj från** . **[!UICONTROL Postdokument stöds inte för XFA-baserade eller adaptiva formulär med formulärmall som formulärmodell.]**

1. Välj något av följande alternativ i avsnittet Dokumentmall på fliken Formulärmodell.

   **Ingen** Välj det här alternativet om du inte vill konfigurera postdokument för formuläret.

   **Associera formulärmall som dokumentmall** Välj det här alternativet om du har en XDP-fil som du vill använda som mall för postdokumentet. När du väljer det här alternativet visas alla XDP-filer som är tillgängliga i AEM Forms-databasen. Välj lämplig fil.

   Den valda XDP-filen kopplas till det adaptiva formuläret.

   **Generera postdokument** Välj det här alternativet om du vill använda en XDP-fil som basmall för att definiera format och utseende för postdokumentet. När du väljer det här alternativet visas alla XDP-filer som är tillgängliga i AEM Forms-databasen. Välj lämplig fil.

   **[!UICONTROL Välj det här alternativet om du vill använda en XDP-fil som basmall för att definiera format och utseende för postdokumentet. När du väljer det här alternativet visas alla XDP-filer som är tillgängliga i AEM Forms-databasen. Välj lämplig fil.]**

   **Välj Formulärmall som basmall om du vill generera postdokument** . Välj det här alternativet om du vill använda en XDP-fil som basmall för att definiera format och utseende för postdokumentet. När du väljer det här alternativet visas alla XDP-filer som är tillgängliga i AEM Forms-databasen. Välj lämplig fil.

   >[!NOTE]
   >
   >Se till att schemat som används för att skapa anpassningsbara formulär och schema (databchema) för XFA-formulär är desamma om:
   >
   >
   >
   >    * Ditt adaptiva formulär är schemabaserat
   >    * Du använder **alternativet Koppla formulärmall som dokumentmall** för postdokument


1. Klicka på **Klar.**

## Anpassa varumärkesinformationen i urkunder {#customize-the-branding-information-in-document-of-record}

När du genererar ett postdokument kan du ändra profileringsinformationen för postdokumentet på fliken Dokument av post. Fliken Dokument för post innehåller alternativ som logotyp, utseende, layout, sidhuvud och sidfot, ansvarsfriskrivning och huruvida du vill ta med omarkerade kryssrutor och alternativknappar eller inte.

Om du vill lokalisera den varumärkesinformation som du anger på fliken Dokument av post måste du se till att webbläsarens språkområde är korrekt inställt. Följ de här stegen för att anpassa profileringsinformationen för urkunder:

1. Markera en panel (rotpanelen) i postdokumentet och tryck sedan på ![Konfigurera](assets/configure.png).
1. Tryck på ![dortab](assets/dortab.png). Fliken Dokument för post visas.
1. Välj antingen standardmallen eller en anpassad mall för återgivning av postdokumentet. Om du väljer standardmallen visas en miniatyrförhandsvisning av postdokumentet under listrutan Mall.

   ![brandingtemplate](assets/brandingtemplate.png)

   Om du väljer en egen mall bläddrar du till en XDP-fil på AEM Forms-servern. Om du vill använda en mall som inte redan finns på AEM Forms-servern måste du först överföra XDP-filen till AEM Forms-servern.

1. Beroende på om du väljer en standardmall eller en anpassad mall visas några eller alla följande egenskaper på fliken Dokument för post. Ange dessa korrekt:

   * **Logotypbild**: Du kan antingen välja att använda logotypbilden från det adaptiva formuläret, välja en från DAM eller överföra en från datorn.
   * **Formulärtitel**
   * **Sidhuvudstext**
   * **Ansvarsfriskrivning**
   * **Ansvarsfriskrivning**
   * **Ansvarsfriskrivning**
   * **Dekorfärg**: Den färg i vilken rubriktext och avgränsningslinjer återges i dokumentet eller i PDF-postfilen
   * **Teckensnittsfamilj**: Teckensnittsfamilj för texten i det postade PDF-dokumentet
   * **Visa endast de valda värdena för komponenterna Kryssruta och Alternativknapp**
   * **Avgränsare för flera markerade värden**
   * **Inkludera formulärobjekt som inte är bundna till datamodell**
   * **Uteslut dolda fält från postdokumentet**
   * **Dölj beskrivning av paneler**
   >[!NOTE]
   >
   >Om du använder en adaptiv formulärmall som har skapats med en version av Designer före 6.3, måste du se till att följande finns i din adaptiva formulärmall under rotdelformuläret för att egenskaperna för accentfärg och teckensnittsfamilj ska fungera:

   ```xml
   <proto>
   <font typeface="Arial"/>
   <fill>
   <color value="4,166,203"/>
   </fill>
   <edge>
   <color value="4,166,203"/>
   </edge>
   </proto>
   ```

1. Om du vill spara varumärkeändringen trycker du på Klar.

## Tabell- och kolumnlayouter för paneler i dokumentformat {#table-and-column-layouts-for-panels-in-document-of-record}

Ditt anpassningsbara formulär kan vara långt och innehålla flera formulärfält. Du kanske inte vill spara ett postdokument som en exakt kopia av det anpassade formuläret. Nu kan du välja en tabell- eller kolumnlayout för att spara en eller flera adaptiva formulärpaneler i PDF-postdokumentet.

Innan du genererar ett postdokument väljer du Layout för postdokumentet för den panelen som Tabell eller Kolumn i inställningarna för en panel. Fälten i panelen ordnas därefter i postdokumentet.

![Fält i en panel återges i en tabellayout i postdokumentet](assets/dortablelayout.png)

Fält i en panel återges i en tabellayout i postdokumentet

![Fält i en panel återges i en kolumnlayout i postdokumentet](assets/dorcolumnlayout.png)

Fält i en panel återges i en kolumnlayout i postdokumentet

## Dokumentinställningar {#document-of-record-settings}

Med dokumentinställningar kan du välja vilka alternativ som ska ingå i postdokumentet. En bank godkänner till exempel namn, ålder, personnummer och telefonnummer i ett formulär. Formuläret genererar ett bankkontonummer och filialinformation. Du kan välja att bara visa namn, personnummer, bankkonto och filialinformation i registreringsdokumentet.

Dokumentet med postinställningar för en komponent är tillgängligt under dess egenskaper. Om du vill komma åt egenskaperna för en komponent markerar du komponenten och klickar på ![cmpr](assets/cmppr.png) i övertäckningen. Egenskaperna listas i sidlisten och du hittar följande inställningar i den.

**Fältnivåinställningar**

* **Exkludera från dokument för registrering**: Om du anger egenskapen true utesluts fältet från postdokumentet. Det här är en skriptbar egenskap med namnet `excludeFromDoR`. Dess beteende beror på **Uteslut fält från DoR om egenskapen för dold** formulärnivå är dold.

* **** Visa panelen som tabell: Om du ställer in egenskapen visas panelen som en tabell i postdokumentet om panelen innehåller färre än 6 fält. Gäller endast för panelen.
* **** Exkludera rubrik från arkivdokument: Om du anger egenskapen utesluts panelens/tabellens namn från postdokumentet. Gäller endast för panel och tabell.
* **** Exkludera beskrivning från postdokument: Om du ställer in egenskapen utesluts beskrivningen av panelen/tabellen från postdokumentet. Gäller endast för panel och tabell.

**Inställningar för formulärnivå**

* **** Inkludera obundna fält i DoR: När du anger egenskapen inkluderas obundna fält från schemabaserade adaptiva formulär i postdokumentet. Som standard är det sant.
* **** Uteslut fält från DoR om de är dolda: Om du ställer in egenskapen åsidosätts beteendet för fältnivåegenskapen Exkludera från dokument för post när det inte är sant. Om fälten är dolda när formuläret skickas, kommer de att exkluderas från postdokumentet om egenskapen är true, förutsatt att egenskapen Exkludera från postdokument inte är inställd.

## Viktiga saker att tänka på när du arbetar med postdokument {#key-considerations-when-working-with-document-of-record}

Tänk på följande när du arbetar med urkunder för anpassade formulär:

* Postmallar för dokument stöder inte RTF-text. Därför visas all formaterad text i det statiska adaptiva formuläret eller i den information som fylls i av slutanvändaren som oformaterad text i postdokumentet.
* Dokumentfragment i ett anpassat formulär visas inte i postdokumentet. Däremot stöds adaptiva formulärfragment.
* urkunder används endast för utskrift.
* Det finns inte stöd för innehållsbindning i dokument med poster som genererats för XML-schemabaserade adaptiva formulär.
* Det finns inte stöd för innehållsbindning i dokument med poster som genererats för XML-schemabaserade adaptiva formulär.
* Lokaliserad version av postdokument skapas på begäran för en språkinställning när användaren begär återgivningen av postdokumentet. Lokalisering av postdokument sker tillsammans med lokalisering av anpassat formulär. Mer information om lokalisering av dokument med post och adaptiva formulär finns i [Använda arbetsflöde för AEM-översättning för att lokalisera adaptiva formulär och urkunder med](/help/forms/using/using-aem-translation-workflow-to-localize-adaptive-forms.md)arkivhandlingar.

