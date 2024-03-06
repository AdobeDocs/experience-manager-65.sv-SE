---
title: Generera arkivdokument för anpassningsbara formulär
description: Beskriver hur du kan generera en mall för ett postdokument (DoR) för adaptiva formulär.
content-type: reference
topic-tags: adaptive_forms, develop
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
feature: Adaptive Forms, Foundation Components
exl-id: 7240897f-6b3a-427a-abc6-66310c2998f3
source-git-commit: 9d497413d0ca72f22712581cf7eda1413eb8d643
workflow-type: tm+mt
source-wordcount: '4120'
ht-degree: 0%

---

# Generera arkivdokument för adaptiva formulär eller adaptiva formulärfragment {#generate-document-of-record-for-adaptive-forms}

<span class="preview"> Adobe rekommenderar att man använder modern och utbyggbar datainhämtning [Kärnkomponenter](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html) for [skapa ny Adaptive Forms](/help/forms/using/create-an-adaptive-form-core-components.md) eller [lägga till adaptiv Forms på AEM Sites-sidor](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). De här komponenterna utgör ett betydande framsteg när det gäller att skapa adaptiva Forms-filer, vilket ger imponerande användarupplevelser. I den här artikeln beskrivs det äldre sättet att skapa Adaptiv Forms med baskomponenter. </span>

| Version | Artikellänk |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Klicka här](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/generate-document-of-record-for-non-xfa-based-adaptive-forms.html) |
| AEM 6.5 | Den här artikeln |


## Ökning {#overview}

Efter att ha skickat in ett formulär vill era kunder vanligtvis registrera, i utskrift eller i dokumentformat, den information de har fyllt i formuläret för framtida referens. Detta kallas för ett urkunder.

I den här artikeln beskrivs hur du kan generera ett postdokument för Adaptiv Forms eller Adaptiv formulärfragment.

>[!NOTE]
>
> Stödet för att anpassa dina adaptiva formulärfragment och fälten i den adaptiva formulärredigeraren introducerades i AEM 6.5 Forms Service Pack 19 (6.5.19.0).


>[!NOTE]
>
>Automatisk generering av urkunder stöds inte för XFA-baserade adaptiva formulär. Du kan dock använda XDP-filen som används för att skapa det adaptiva formuläret som ett arkivdokument.

## Anpassningsbara formulärtyper och deras urkunder {#adaptive-form-types-and-their-documents-of-record}

När du skapar ett anpassat formulär kan du välja en formulärmodell. Dina alternativ är:

* [Formulärmallar](../../forms/using/creating-adaptive-form.md#create-an-adaptive-form-based-on-an-xfa-form-template)
Gör att du kan välja en XFA-mall för ditt adaptiva formulär. När du väljer en XFA-mall kan du använda den associerade XDP-filen för postdokument enligt beskrivningen ovan.

* [XML-schema](../../forms/using/creating-adaptive-form.md#create-an-adaptive-form-based-on-xml-or-json-schema)
Gör att du kan välja en XML-schemadefinition för ditt adaptiva formulär. När du väljer ett XML-schema för det anpassade formuläret kan du:

   * Associera en XFA-mall för postdokument. Se till att associerad XFA-mall använder samma XML-schema som ditt adaptiva formulär
   * Generera arkivhandlingar automatiskt

* Ingen Gör att du kan skapa ett anpassat formulär utan en formulärmodell. Registerdokumentet genereras automatiskt för ditt anpassningsbara formulär.

När du väljer en formulärmodell konfigurerar du postdokumentet med de alternativ som finns under Dokumentmallskonfiguration. Se [Konfiguration av dokumentmall](#document-of-record-template-configuration).

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

**Adaptiv form** Anpassat formulär som du vill skapa ett postdokument för.

**Adaptivt formulärfragment** Anpassat formulärfragment som du vill generera ett postdokument för.

**Basmall (rekommenderas)** XFA-mall (XDP-fil) skapad i AEM Designer. Basmallen används för att ange formaterings- och varumärkesinformation för postmalldokument.

Se [Basmall för ett postdokument](#base-template-of-a-document-of-record)

>[!NOTE]
>
>Basmallen för ett postdokument kallas också metamall för ett postdokument.

**Dokumentmall** XFA-mall (XDP-fil) genererad från ett adaptivt formulär.

Se [Konfiguration av dokumentmall](#document-of-record-template-configuration).

**Formulärdata** Information som fylls i av en användare i det anpassade formuläret. Den sammanfogas med postmalldokumentet för att generera postdokumentet.

## Mappning av adaptiva formulärelement {#mapping-of-adaptive-form-elements}

I följande avsnitt beskrivs hur anpassningsbara formulärelement visas i postdokumentet.

### Fält {#fields}

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
   <td>Datum-/tidsfält</td>
   <td>true</td>
   <td> </td>
  </tr>
  <tr>
   <td>Nedrullningsbar lista</td>
   <td>Listruta</td>
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
   <td>Återställ knapp</td>
   <td>false</td>
   <td> </td>
  </tr>
  <tr>
   <td>Skicka-knapp</td>
   <td><p>E-postknapp</p> <p>HTTP-sändningsknapp</p> </td>
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

### Behållare {#containers}

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

De adaptiva formulärtabellkomponenterna som sidhuvud, sidfot och radmappning till motsvarande XFA-komponenter. Du kan mappa repeterbara paneler till tabeller i ett postdokument.

## Basmall för ett postdokument {#base-template-of-a-document-of-record}

Basmallen innehåller formaterings- och utseendeinformation för urkunder. Du kan anpassa standardutseendet för automatiskt genererade postdokument. Du vill till exempel lägga till företagets logotyp i sidhuvudet och copyrightinformation i sidfoten i postdokumentet. Mallsidan från basmallen används som mallsida för postmalldokument. Mallsidan kan innehålla information som sidhuvud, sidfot och sidnummer som du kan använda på postdokument. Du kan använda sådan information för att dokumentera med hjälp av basmallen för automatisk generering av postdokument. Med hjälp av basmallen kan du ändra standardegenskaperna för fält.

Se till att du följer [Grundmallskonventioner](#base-template-conventions) när du utformar en basmall.

## Grundmallskonventioner {#base-template-conventions}

En basmall används för att definiera sidhuvud, sidfot, format och utseende för ett postdokument. Sidhuvudet och sidfoten kan innehålla information som företagets logotyp och copyrighttext. Den första mallsidan i basmallen kopieras och används som mallsida för postdokumentet, som innehåller sidhuvud, sidfot, sidnummer eller annan information som ska visas på alla sidor i postdokumentet. Om du använder en basmall som inte överensstämmer med basmallskonventioner, används den första mallsidan från basmallen fortfarande i postmalldokumentet. Vi rekommenderar att du utformar din basmall enligt dess konventioner och använder den för automatisk generering av arkivdokument.

**Konventioner för mallsidor**

* I basmallen ska du namnge rotdelformuläret som `AF_METATEMPLATE` och mallsidan som `AF_MASTERPAGE`.

* Mallsidan med namnet `AF_MASTERPAGE` som finns under `AF_METATEMPLATE` rotdelformulär används som inställning för att extrahera sidhuvud, sidfot och formateringsinformation.

* If `AF_MASTERPAGE` saknas används den första mallsidan i basmallen.

**Formatkonventioner för fält**

* Om du vill använda format på fälten i postdokumentet innehåller basmallen fält i `AF_FIELDSSUBFORM` under `AF_METATEMPLATE` rotdelformulär.

* Egenskaperna för dessa fält används för fälten i postdokumentet. Dessa fält ska följa `AF_<name of field in all caps>_XFO` namnkonvention. Fältnamnet för kryssrutan bör till exempel vara `AF_CHECKBOX_XFO`.

Så här skapar du en basmall i AEM Designer.

1. Klicka **Arkiv > Nytt**.
1. Välj **Baserat på en mall** alternativ.

1. Välj **Forms - dokument** kategori.
1. Välj **DoR-basmall**.
1. Klicka **Nästa** och tillhandahålla den information som krävs.

1. (Valfritt) Ändra format och utseende på fält som du vill använda i fälten i postdokumentet.
1. Spara formuläret.

Du kan nu använda det sparade formuläret som en basmall för postdokument.
Ändra eller ta inte bort några skript i basmallen.

**Ändra basmall**

* Om du inte använder någon formatering över fält i basmallen bör du ta bort dessa fält från basmallen så att eventuella uppgraderingar av basmallen automatiskt hämtas.
* När du ändrar basmallen ska du inte ta bort, lägga till eller ändra skript.

>[!NOTE]
>
>Utforma en basmall enligt konventioner och följ stegen ovan.

## Konfiguration av dokumentmall {#document-of-record-template-configuration}

Konfigurera dokumentets postmall för formuläret så att kunderna kan hämta en utskriftsvänlig kopia av det skickade formuläret. En XDP-fil fungerar som ett dokument i postmallen. Dokumentet med nedladdade postkunder formateras enligt layouten som anges i XDP-filen.

Utför följande steg för att konfigurera ett postdokument för adaptiva formulär:

1. I AEM författarinstans klickar du på **Forms > Forms och dokument.**
1. Markera ett formulär och klicka på **Visa egenskaper**.
1. Välj **Formulärmodell**.
Du kan också välja en formulärmodell när du skapar ett formulär.

   >[!NOTE]
   >
   >På fliken Formulärmodell väljer du **Schema** eller **Ingen** från **Välj från** nedrullningsbar meny. **[!UICONTROL Document of record is not supported for XFA-based or adaptive forms with Form Template as form model.]**

1. Välj något av följande alternativ i avsnittet Dokumentmall på fliken Formulärmodell:

   **Ingen** Välj det här alternativet om du inte vill konfigurera postdokument för formuläret.

   **Associera formulärmall som postdokumentmall** Välj det här alternativet om du har en XDP-fil som du vill använda som mall för postdokumentet. När du väljer det här alternativet visas alla XDP-filer som är tillgängliga i AEM Forms-databasen. Välj lämplig fil.

   Den valda XDP-filen kopplas till det adaptiva formuläret.

   **Generera postdokument** Välj det här alternativet om du vill använda en XDP-fil som basmall för att definiera format och utseende för postdokumentet. När du väljer det här alternativet visas alla XDP-filer som är tillgängliga i AEM Forms-databasen. Välj lämplig fil.

   >[!NOTE]
   >
   >Se till att schemat som används för att skapa anpassningsbara formulär och schema (databchema) för XFA-formulär är desamma om:
   >
   >
   >
   >    * Ditt adaptiva formulär är schemabaserat
   >    * Du använder **Koppla formulärmall till postdokumentmall** alternativ för urkunder
   >
   >

1. Klicka **Klart.**

## Anpassa varumärkesinformationen i urkunder {#customize-the-branding-information-in-document-of-record}

När du genererar ett postdokument kan du ändra profileringsinformationen för postdokumentet på fliken Dokument av post. Fliken Dokument för post innehåller alternativ som logotyp, utseende, layout, sidhuvud och sidfot, ansvarsfriskrivning och huruvida du vill ta med omarkerade kryssrutor och alternativknappar eller inte.

Om du vill lokalisera den varumärkesinformation som du anger på fliken Dokument av post måste du se till att webbläsarens språkområde är korrekt inställt. Följ de här stegen för att anpassa profileringsinformationen för urkunder:

1. Markera en panel (rotpanelen) i postdokumentet och markera sedan ![konfigurera](assets/configure.png).
1. Välj ![dortab](/help/forms/using/assets/dortab.png). Fliken Dokument för post visas.
1. Välj antingen standardmallen eller en anpassad mall för återgivning av postdokumentet. Om du väljer standardmallen visas en miniatyrförhandsvisning av postdokumentet under listrutan Mall.

   ![brandingtemplate](/help/forms/using/assets/brandingtemplate.png)

   Om du väljer en anpassad mall bläddrar du till en XDP-fil på AEM Forms-servern. Om du vill använda en mall som inte redan finns på din AEM Forms-server måste du först överföra XDP-filen till din AEM Forms-server.

1. Beroende på om du väljer en standardmall eller en anpassad mall visas några eller alla följande egenskaper på fliken Dokument för post. Ange dessa korrekt:

   * **Logotypbild**: Du kan antingen välja att använda logotypbilden från det adaptiva formuläret, välja en från DAM eller överföra en från datorn.
   * **Formulärtitel**
   * **Sidhuvudstext**
   * **Ansvarsfriskrivning**
   * **Ansvarsfriskrivning**
   * **Ansvarsfriskrivning**
   * **Dekorfärg**: Den färg i vilken rubriktext och avgränsningslinjer återges i dokumentet eller posten PDF
   * **Font Family**: Teckensnittsfamilj för texten i det registrerade PDF
   * **Visa endast de valda värdena för komponenterna Kryssruta och Alternativknapp**
   * **Avgränsare för flera markerade värden**
   * **Inkludera formulärobjekt som inte är bundna till datamodell**
   * **Uteslut dolda fält från postdokumentet**
   * **Dölj beskrivning av paneler**

   Om den anpassade XDP-mallen som du väljer innehåller flera mallsidor visas egenskaperna för de sidorna i **[!UICONTROL content]** i **[!UICONTROL Document of Record]** -fliken.

   ![Egenskaper för mallsida](assets/master-page-properties.png)

   Mallsidans egenskaper är logotypbild, rubriktext, Formulärtitel, Ansvarsfriskrivning och Ansvarsfriskrivning. Du kan använda anpassningsbara formulär- eller XDP-mallegenskaper på postdokumentet. I AEM Forms används mallegenskaperna som standard på postdokumentet. Du kan också definiera egna värden för mallsidans egenskaper. Mer information om hur du använder flera mallsidor i ett postdokument finns i [Använda flera mallsidor i ett postdokument](#apply-multiple-master-pages-dor).

   >[!NOTE]
   >
   >Om du använder en adaptiv formulärmall som har skapats med en version av Designer före 6.3, för att egenskaperna för accentfärg och teckensnittsfamilj ska fungera, kontrollerar du att följande finns i din adaptiva formulärmall under rotdelformuläret:

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

1. Om du vill spara ändringarna väljer du Klart.

## Tabell- och kolumnlayouter för paneler i dokumentformat {#table-and-column-layouts-for-panels-in-document-of-record}

Ditt anpassningsbara formulär kan vara långt och innehålla flera formulärfält. Du kanske inte vill spara ett postdokument som en exakt kopia av det anpassade formuläret. Nu kan du välja en tabell- eller kolumnlayout för att spara en eller flera adaptiva formulärpaneler i dokumentet med posten PDF.

Innan du genererar ett postdokument väljer du Layout för postdokumentet för den panelen som Tabell eller Kolumn i inställningarna för en panel. Fälten i panelen ordnas därefter i postdokumentet.

![Fält i en panel återges i en tabellayout i postdokumentet](assets/dortablelayout.png)

Fält i en panel återges i en tabellayout i postdokumentet

![Fält i en panel återges i en kolumnlayout i postdokumentet](assets/dorcolumnlayout.png)

Fält i en panel återges i en kolumnlayout i postdokumentet

## Dokumentinställningar {#document-of-record-settings}

Med dokumentinställningar kan du välja vilka alternativ som ska ingå i postdokumentet. En bank godkänner till exempel namn, ålder, personnummer och telefonnummer i ett formulär. Formuläret genererar ett bankkontonummer och filialinformation. Du kan välja att bara visa namn, personnummer, bankkonto och filialinformation i registreringsdokumentet.

Dokumentet med postinställningar för en komponent är tillgängligt under dess egenskaper. Om du vill komma åt egenskaperna för en komponent markerar du komponenten och klickar på ![cmppr](assets/cmppr.png) i övertäckningen. Egenskaperna listas i sidlisten och du hittar följande inställningar i den.

**Fältnivåinställningar**

* **Exkludera från dokument i post**: Om egenskapen true anges utesluts fältet från postdokumentet. Det här är en skriptbar egenskap med namnet `excludeFromDoR`. Dess beteende beror på **Uteslut fält från DoR om de är dolda** formulärnivåegenskap.

* **Visa panelen som tabell:** Om du ställer in egenskapen visas panelen som en tabell i postdokumentet om panelen innehåller färre än 6 fält. Gäller endast för panelen.
* **Exkludera rubrik från arkivdokument:** Om du anger egenskapen utesluts panelens/tabellens namn från postdokumentet. Gäller endast för panel och tabell.
* **Exkludera beskrivning från postdokument:** Om du ställer in egenskapen utesluts beskrivningen av panelen/tabellen från postdokumentet. Gäller endast för panel och tabell.
* **[!UICONTROL Pagination]** > **[!UICONTROL Place]**: Anger var du ska placera panelen.
   * **[!UICONTROL Place]** > **[!UICONTROL Following Previous]**: Placerar panelen efter föregående objekt på den överordnade panelen.
   * **[!UICONTROL Place]** > **[!UICONTROL In Content Area]** > Innehållsområdets namn: Placerar panelen i det angivna innehållsområdet.
   * **[!UICONTROL Place]** > **[!UICONTROL Top of Next Content Area]**: Placerar panelen högst upp i nästa innehållsområde.
   * **[!UICONTROL Place]** > **[!UICONTROL Top of Content Area]** > Innehållsområdets namn: Placerar panelen högst upp i det angivna innehållsområdet.
   * **[!UICONTROL Place]** > **[!UICONTROL On Page]** > Namn på mallsida: Placerar panelen på den angivna sidan. Om en sidbrytning inte infogas automatiskt [!DNL AEM Forms] lägger till en sidbrytning.
   * **[!UICONTROL Place]** > **[!UICONTROL Top of Next Page]**: Placerar panelen överst på nästa sida. Om en sidbrytning inte infogas automatiskt [!DNL AEM Forms] lägger till en sidbrytning.
   * **[!UICONTROL Place]** > **[!UICONTROL Top of Page]** > Namn på mallsida: Placerar panelen överst på sidan när den angivna sidan återges. Om en sidbrytning inte infogas automatiskt [!DNL AEM Forms] lägger till en sidbrytning.
* **[!UICONTROL Pagination]** > **[!UICONTROL After]**: Avgör vilket område som ska fyllas när en panel har placerats ut. Följande fält är tillgängliga i **[!UICONTROL After]** avsnitt:
   * **[!UICONTROL After]** > **[!UICONTROL Continue Filling Parent]**: Fortsätter sammanfogning av data för alla återstående objekt som ska fyllas i på den överordnade panelen.
   * **[!UICONTROL After]** > **[!UICONTROL Go to Next Content Area]**: Börjar fylla nästa innehållsområde efter att panelen har monterats.
   * **[!UICONTROL After]** > **[!UICONTROL Go To Content Area]** > Innehållsområdets namn: Börjar fylla det angivna innehållsområdet efter att panelen har monterats.
   * **[!UICONTROL After]** > **[!UICONTROL Go To Next Page]**: Börjar fylla nästa sida efter att panelen har monterats.
   * **[!UICONTROL After]** > **[!UICONTROL Go To Page]** > Sidans namn: Börjar fylla den angivna sidan efter att panelen har monterats.
* **[!UICONTROL Pagination]** > **[!UICONTROL Overflow]**: Anger ett spill för en panel eller tabell som sträcker sig över flera sidor. Följande fält är tillgängliga i **[!UICONTROL Overflow]** avsnitt:
   * **[!UICONTROL Overflow]** > **[!UICONTROL None]**: Börjar fylla nästa sida. Om en sidbrytning inte infogas automatiskt [!DNL AEM Forms] lägger till en sidbrytning.
   * **[!UICONTROL Overflow]** > **[!UICONTROL Go to Content Area]** > Innehållsområdets namn: Börjar fylla det angivna innehållsområdet.
   * **[!UICONTROL Overflow]** > **[!UICONTROL Go To Page]** > Sidans namn: börjar fylla den angivna sidan.

  >[!NOTE]
  >
  > Pagination-egenskapen är inte tillgänglig för adaptiva formulärfragment.

Mer information om hur du använder sidbrytningar och använder flera mallsidor i ett postdokument finns i [Använda sidbrytning i ett postdokument](#apply-page-breaks-in-dor) och [Använda flera mallsidor i ett postdokument](#apply-multiple-master-pages-dor).

**Inställningar för formulärnivå**

* **Inkludera obundna fält i DoR:** När du anger egenskapen inkluderas obundna fält från schemabaserade adaptiva formulär i postdokumentet. Som standard är det sant.
* **Uteslut fält från DoR om de är dolda:** Ange egenskapen för att exkludera dolda fält från [!UICONTROL Document of Record] när formulär skickas. När du aktiverar [Återvalidera på servern](/help/forms/using/configuring-submit-actions.md#server-side-revalidation-in-adaptive-form-server-side-revalidation-in-adaptive-form)beräknas de dolda fälten på nytt innan de utesluts från [!UICONTROL Document of Record].

## Använda en sidbrytning i ett postdokument {#apply-page-breaks-in-dor}

Du kan använda flera metoder för att tillämpa sidbrytningar i ett postdokument.

Så här använder du en sidbrytning på ett postdokument:

1. Markera panelen och markera ![Konfigurera](/help/forms/using/assets/configure.png)
1. Expandera **[!UICONTROL Document of Record]** för att visa egenskaperna.

1. I **[!UICONTROL Pagination]** avsnitt, markera ![Mapp](/help/forms/using/assets/folder-icon.png) i **[!UICONTROL Place]** fält.
1. Välj **[!UICONTROL Top of Next page]** och markera **[!UICONTROL Select]**. Du kan också välja **[!UICONTROL Top of Page]**, markera mallsidan och markera **[!UICONTROL Select]** om du vill använda sidbrytningen.
1. Välj ![Spara](/help/forms/using/assets/save_icon.png) för att spara egenskaperna.

Den valda panelen flyttas till nästa sida.

## Använda flera mallsidor i ett postdokument {#apply-multiple-master-pages-dor}

Om den anpassade XDP-mallen som du väljer innehåller flera mallsidor visas egenskaperna för de sidorna i [!UICONTROL content] i [!UICONTROL Document of Record] -fliken. Mer information finns i [Anpassa varumärkesinformationen i urkunder](#customize-the-branding-information-in-document-of-record).

Du kan tillämpa flera mallsidor på ett postdokument genom att tillämpa olika mallsidor på komponenterna i ett anpassat formulär. Använd [Sidnumrering](#document-of-record-settings) i dokumentegenskaperna om du vill använda flera mallsidor.

Följande är ett exempel på hur du använder flera mallsidor i ett postdokument: Du överför en XDP-mall som innehåller fyra mallsidor till [!DNL AEM Forms] server. [!DNL AEM Forms] I används mallegenskaperna som standard på postdokumentet. [!DNL AEM Forms] I används också de första mallsidesegenskaperna i mallen på postdokumentet.

Om du vill använda den andra mallsidans egenskaper på en panel och den tredje mallsidans egenskaper på de paneler som följer, ska du utföra följande steg:

1. Markera panelen för att använda den andra mallsidan och markera ![Konfigurera](assets/cmppr.png).
1. I **[!UICONTROL Pagination]** avsnitt, markera ![Mapp](/help/forms/using/assets/folder-icon.png) i **[!UICONTROL Place]** fält.
1. Välj **[!UICONTROL On page]** markerar du den andra mallsidan och väljer **[!UICONTROL Select]**.
AEM Forms lägger till en andra mallsida på panelen och alla efterföljande paneler i det anpassade formuläret.
1. I **[!UICONTROL Pagination]** avsnitt, markera ![Mapp](/help/forms/using/assets/folder-icon.png) i **[!UICONTROL After]** fält.
1. Välj **[!UICONTROL Go To page]** markerar du den tredje mallsidan och väljer **[!UICONTROL Select]**.
1. Välj ![Spara](/help/forms/using/assets/save_icon.png) för att spara egenskaperna.
AEM Forms använder den tredje mallsidan på panelen och alla efterföljande paneler i det anpassade formuläret.

>[!NOTE]
>
> Du kan inte använda flera mallsidor på ett postdokument för ett anpassat formulärfragment.

## Viktiga saker att tänka på när du arbetar med postdokument {#key-considerations-when-working-with-document-of-record}

Tänk på följande när du arbetar med urkunder för anpassade formulär.

* Postmalldokument har inte stöd för RTF-text. Därför visas all formaterad text i det statiska adaptiva formuläret eller i den information som fylls i av slutanvändaren som oformaterad text i postdokumentet.
* Dokumentfragment i ett anpassat formulär visas inte i postdokumentet. Däremot stöds adaptiva formulärfragment.
* Det finns inte stöd för innehållsbindning i dokument med poster som genererats för XML-schemabaserade adaptiva formulär.
* Lokaliserad version av postdokument skapas på begäran för en språkinställning när användaren begär återgivningen av postdokumentet. Lokalisering av postdokument sker tillsammans med lokalisering av anpassat formulär. Mer information om lokalisering av dokument med post och adaptiva formulär finns i [Använda arbetsflöde för AEM översättning för att lokalisera anpassningsbara formulär och urkunder](/help/forms/using/using-aem-translation-workflow-to-localize-adaptive-forms.md).

## Använda en anpassad XCI-fil

En XCI-fil hjälper dig att ange olika egenskaper för ett dokument. <!-- Forms as a Cloud Service has a master XCI file.--> Du kan använda en anpassad XCI-fil för att åsidosätta en eller flera standardegenskaper som anges i den befintliga XCI-filen. Du kan till exempel välja att bädda in ett teckensnitt i ett dokument eller aktivera taggad egenskap för alla dokument. Följande tabell anger XCI-alternativen:

| XCI-alternativ | Beskrivning |
|--- |--- |
| config/present/pdf/creator | Identifierar den som har skapat dokumentet med hjälp av posten Skapare i dokumentinformationsordlistan. Mer information om den här ordlistan finns i [Referenshandbok för PDF](https://opensource.adobe.com/dc-acrobat-sdk-docs/acrobatsdk/). |
| config/present/pdf/producer | Identifierar dokumenttillverkaren med hjälp av posten Producer i dokumentinformationsordlistan. Mer information om den här ordlistan finns i [Referenshandbok för PDF](https://opensource.adobe.com/dc-acrobat-sdk-docs/acrobatsdk/). |
| config/present/layout | Anger om utdata är en enda panel eller sidnumrerad. |
| config/present/pdf/compression/level | Anger den komprimeringsgrad som ska användas när ett PDF-dokument skapas. |
| config/present/pdf/fontInfo/embed | Styr teckensnittsinbäddning i utdatadokumentet. |
| config/present/pdf/scriptModel | Styr om XFA-specifik information ska inkluderas i utdata-PDF-dokumentet. |
| config/present/common/data/adjustData | Kontrollerar om XFA-programmet justerar data efter sammanslagningen. |
| config/present/pdf/renderPolicy | Kontrollerar om genereringen av sidinnehåll görs på servern eller skjuts upp till klienten. |
| config/present/common/locale | Anger den standardspråkinställning som används i utdatadokumentet. |
| config/present/destination | Anger utdataformatet när det finns i ett aktuellt element. Anger vilken åtgärd som ska utföras när dokumentet öppnas i en interaktiv klient när det finns i ett openAction-element. |
| config/present/output/type | Anger vilken typ av komprimering som ska användas för en fil eller vilken typ av utdata som ska skapas. |
| config/present/common/temp/uri | Anger formulär-URI. |
| config/present/common/template/base | Anger en basplats för URI:er i formulärdesignen. När det här elementet saknas eller är tomt används platsen för formulärdesignen som bas. |
| config/present/common/log/to | Styr platsen dit loggdata eller utdata skrivs. |
| config/present/output/to | Styr platsen dit loggdata eller utdata skrivs. |
| config/present/script/currentPage | Anger den inledande sidan när dokumentet öppnas. |
| config/present/script/exclude | Informerar Forms as a Cloud Service om vilka händelser som ska ignoreras. |
| config/present/pdf/linearized | Anger om utdatadokumentet för PDF är linjärt. |
| config/present/script/runScripts | Styr vilken uppsättning skript som Forms as a Cloud Service kör. |
| config/present/pdf/tagged | Styr om taggar ska tas med i utdatadokumentet för PDF. Taggar i PDF är ytterligare information som ingår i ett dokument för att visa dokumentets logiska struktur. Taggar underlättar hjälpmedelsanvändningen och formateringen. Ett sidnummer kan till exempel taggas som en artefakt så att skärmläsaren inte omsluter den mitt i texten. Även om märkord gör ett dokument mer användbart, ökar de även storleken på dokumentet och bearbetningstiden för att skapa det. |
| config/present/pdf/fontInfo/alwaysEmbed | Anger ett teckensnitt som är inbäddat i utdatadokumentet. |
| config/present/pdf/fontInfo/neverEmbed | Anger ett teckensnitt som aldrig får bäddas in i utdatadokumentet. |
| config/present/pdf/pdfa/part | Anger versionsnumret för den PDF/A-specifikation som dokumentet uppfyller. |
| config/present/pdf/pdfa/amd | Anger ändringsnivån för PDF/A-specifikationen. |
| config/present/pdf/pdfa/conformance | Anger överensstämmelsenivå med PDF/A-specifikationen. |
| config/present/pdf/version | Anger vilken version av PDF-dokumentet som ska genereras |
| config/present/pdf/version/map | Anger dokumentets reservteckensnitt |


<!--

### Use a custom XCI file in your AEM Forms environment

  1. Add the custom XCI file to your development project.
  1. Specify the following inline property:(/help/implementing/deploying/configuring-osgi.md)
  1. Deploy the project to your AEM Forms environment. <!--Cloud Service environment
  
-->

### Använd en anpassad XCI-fil i den lokala Forms-utvecklingsmiljön

1. Överför XCI-filen till den lokala utvecklingsmiljön.
1. Öppna <!--Cloud Service SDK--> konfigurationshanteraren. <!--The default URL is: <http://localhost:4502/system/console/configMgr>.-->
1. Leta reda på och öppna **[!UICONTROL Adaptive Forms and Interactive Communication Web Channel]** konfiguration.
1. Ange sökvägen till XCI-filen och klicka på **[!UICONTROL Save]**.


