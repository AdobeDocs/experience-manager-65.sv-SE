---
title: Generera arkivdokument för anpassningsbara formulär
seo-title: Generate Document of Record for adaptive forms
description: Beskriver hur du kan generera en mall för ett postdokument (DoR) för adaptiva formulär.
seo-description: Explains how you can generate a template for a document of record (DoR) for adaptive forms.
uuid: 2dc7e0de-fff9-43fa-9426-e9b047eb2595
content-type: reference
topic-tags: adaptive_forms, develop
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: ce65cb5f-94ec-4423-9fa9-d617e9703091
docset: aem65
feature: Adaptive Forms
exl-id: 7240897f-6b3a-427a-abc6-66310c2998f3
source-git-commit: 85189a4c35d1409690cbb93946369244e8848340
workflow-type: tm+mt
source-wordcount: '3337'
ht-degree: 1%

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

* [Formulärmallar](../../forms/using/creating-adaptive-form.md#create-an-adaptive-form-based-on-an-xfa-form-template)
Gör att du kan välja en XFA-mall för ditt adaptiva formulär. När du väljer en XFA-mall kan du använda den associerade XDP-filen för postdokument enligt beskrivningen ovan.

* [XML-schema](../../forms/using/creating-adaptive-form.md#create-an-adaptive-form-based-on-xml-or-json-schema)
Gör att du kan välja en XML-schemadefinition för ditt adaptiva formulär. När du väljer ett XML-schema för det anpassade formuläret kan du:

   * Associera en XFA-mall för postdokument. Se till att associerad XFA-mall använder samma XML-schema som ditt adaptiva formulär
   * Generera urkunder automatiskt

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

De adaptiva formulärtabellkomponenterna som sidhuvud, sidfot och radmappning till motsvarande XFA-komponenter. Du kan mappa upprepningsbara paneler till tabeller i ett postdokument.

## Basmall för ett postdokument {#base-template-of-a-document-of-record}

Basmallen innehåller formaterings- och utseendeinformation för urkunder. Du kan anpassa standardutseendet för automatiskt genererade postdokument. Du vill till exempel lägga till företagets logotyp i sidhuvudet och copyrightinformation i sidfoten i postdokumentet. Den överordnad sidan från basmallen används som en överordnad sida för postmalldokument. Den överordnad sidan kan innehålla information som sidhuvud, sidfot och sidnummer som du kan använda på postdokument. Du kan använda sådan information för att dokumentera med hjälp av basmallen för automatisk generering av postdokument. Med hjälp av basmallen kan du ändra standardegenskaperna för fält.

Följ [Grundmallskonventioner](#base-template-conventions) när du utformar en basmall.

## Grundmallskonventioner {#base-template-conventions}

En basmall används för att definiera sidhuvud, sidfot, format och utseende för ett postdokument. Sidhuvudet och sidfoten kan innehålla information som företagets logotyp och copyrighttext. Den första överordnad sidan i basmallen kopieras och används som en överordnad sida för postdokumentet, som innehåller sidhuvud, sidfot, sidnummer eller annan information som ska visas på alla sidor i postdokumentet. Om du använder en basmall som inte överensstämmer med basmallskonventioner, används den första överordnad sidan från basmallen fortfarande i postmalldokumentet. Vi rekommenderar att du utformar din basmall enligt dess konventioner och använder den för automatisk generering av arkivdokument.

**Överordnad sidkonventioner**

* I basmallen ska du namnge rotdelformuläret som `AF_METATEMPLATE` och den överordnad sidan som `AF_MASTERPAGE`.

* Den överordnad sidan med namnet `AF_MASTERPAGE` som finns under `AF_METATEMPLATE` rotdelformulär används som inställning för att extrahera sidhuvud, sidfot och formateringsinformation.

* If `AF_MASTERPAGE` saknas används den första överordnad sidan i basmallen.

**Formatkonventioner för fält**

* Om du vill använda format på fälten i postdokumentet innehåller basmallen fält som finns i `AF_FIELDSSUBFORM` under `AF_METATEMPLATE` rotdelformulär.

* Egenskaperna för dessa fält används för fälten i postdokumentet. Dessa fält ska följa `AF_<name of field in all caps>_XFO` namnkonvention. Fältnamnet för kryssrutan bör till exempel vara `AF_CHECKBOX_XFO`.

Så här skapar du en basmall i AEM Designer.

1. Klicka **Arkiv > Nytt**.
1. Välj **Baserat på en mall** alternativ.

1. Välj **Forms - arkivdokument** kategori.
1. Välj **DoR-basmall**.
1. Klicka **Nästa** och tillhandahålla den information som krävs.

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

1. I AEM författarinstans klickar du på **Forms > Forms och dokument.**
1. Markera ett formulär och klicka på **Visa egenskaper**.
1. I fönstret Egenskaper trycker du på **Formulärmodell**.
Du kan också välja en formulärmodell när du skapar ett formulär.

   >[!NOTE]
   >
   >På fliken Formulärmodell väljer du **Schema** eller **Ingen** från **Välj från** nedrullningsbar meny. **[!UICONTROL Document of record is not supported for XFA-based or adaptive forms with Form Template as form model.]**

1. Välj något av följande alternativ i avsnittet Dokumentmall på fliken Formulärmodell.

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
   >    * Du använder **Associera formulärmall som dokumentmall** alternativ för urkunder


1. Klicka **Klart.**

## Anpassa varumärkesinformationen i urkunder {#customize-the-branding-information-in-document-of-record}

När du genererar ett postdokument kan du ändra profileringsinformationen för postdokumentet på fliken Dokument av post. Fliken Dokument för post innehåller alternativ som logotyp, utseende, layout, sidhuvud och sidfot, ansvarsfriskrivning och huruvida du vill ta med omarkerade kryssrutor och alternativknappar eller inte.

Om du vill lokalisera den varumärkesinformation som du anger på fliken Dokument av post måste du se till att webbläsarens språkområde är korrekt inställt. Följ de här stegen för att anpassa profileringsinformationen för urkunder:

1. Markera en panel (rotpanelen) i postdokumentet och tryck sedan på ![konfigurera](assets/configure.png).
1. Tryck ![dortab](/help/forms/using/assets/dortab.png). Fliken Dokument för post visas.
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
   * **Teckensnittsfamilj**: Teckensnittsfamilj för texten i det registrerade PDF
   * **Visa endast de valda värdena för komponenterna Kryssruta och Alternativknapp**
   * **Avgränsare för flera markerade värden**
   * **Inkludera formulärobjekt som inte är bundna till datamodell**
   * **Uteslut dolda fält från postdokumentet**
   * **Dölj beskrivning av paneler**

   Om den anpassade XDP-mallen som du väljer innehåller flera överordnad sidor visas egenskaperna för dessa sidor i **[!UICONTROL content]** i **[!UICONTROL Document of Record]** -fliken.

   ![Överordnad sidegenskaper](assets/master-page-properties.png)

   De överordnad sidegenskaperna är logotypbild, rubriktext, Formulärtitel, Ansvarsfriskrivning och Ansvarsfriskrivning. Du kan använda anpassningsbara formulär- eller XDP-mallegenskaper på postdokumentet. I AEM Forms används mallegenskaperna som standard på postdokumentet. Du kan också definiera egna värden för de överordnad sidegenskaperna. Mer information om hur du använder flera överordnad sidor i ett postdokument finns i [Använda flera överordnad sidor i ett postdokument](#apply-multiple-master-pages-dor).

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

1. Om du vill spara varumärkeändringen trycker du på Klar.

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

* **Exkludera från dokument i post**: Om du anger egenskapen true utesluts fältet från postdokumentet. Det här är en skriptbar egenskap med namnet `excludeFromDoR`. Dess beteende beror på **Uteslut fält från DoR om de är dolda** formulärnivåegenskap.

* **Visa panelen som tabell:** Om du ställer in egenskapen visas panelen som en tabell i postdokumentet om panelen innehåller färre än 6 fält. Gäller endast för panelen.
* **Exkludera rubrik från arkivdokument:** Om du anger egenskapen utesluts panelens/tabellens namn från postdokumentet. Gäller endast för panel och tabell.
* **Exkludera beskrivning från postdokument:** Om du ställer in egenskapen utesluts beskrivningen av panelen/tabellen från postdokumentet. Gäller endast för panel och tabell.
* **[!UICONTROL Pagination]** > **[!UICONTROL Place]**: Anger var du väljer att placera panelen.
   * **[!UICONTROL Place]** > **[!UICONTROL Following Previous]**: Placerar panelen efter föregående objekt på den överordnade panelen.
   * **[!UICONTROL Place]** > **[!UICONTROL In Content Area]** > Innehållsområdets namn: Placerar panelen i det angivna innehållsområdet.
   * **[!UICONTROL Place]** > **[!UICONTROL Top of Next Content Area]**: Placerar panelen högst upp i nästa innehållsområde.
   * **[!UICONTROL Place]** > **[!UICONTROL Top of Content Area]** > Innehållsområdets namn: Placerar panelen högst upp i det angivna innehållsområdet.
   * **[!UICONTROL Place]** > **[!UICONTROL On Page]** > Namn på överordnad sida: Placerar panelen på den angivna sidan. Om en sidbrytning inte infogas automatiskt [!DNL AEM Forms] lägger till en sidbrytning.
   * **[!UICONTROL Place]** > **[!UICONTROL Top of Next Page]**: Placerar panelen överst på nästa sida. Om en sidbrytning inte infogas automatiskt [!DNL AEM Forms] lägger till en sidbrytning.
   * **[!UICONTROL Place]** > **[!UICONTROL Top of Page]** > Namn på överordnad sida: Placerar panelen överst på sidan när den angivna sidan återges. Om en sidbrytning inte infogas automatiskt [!DNL AEM Forms] lägger till en sidbrytning.
* **[!UICONTROL Pagination]** > **[!UICONTROL After]**: Avgör vilket område som ska fyllas när en panel har placerats ut.Följande fält är tillgängliga i **[!UICONTROL After]** avsnitt:
   * **[!UICONTROL After]** > **[!UICONTROL Continue Filling Parent]**: Fortsätter sammanfogning av data för alla återstående objekt som ska fyllas i på den överordnade panelen.
   * **[!UICONTROL After]** > **[!UICONTROL Go to Next Content Area]**: Börjar fylla nästa innehållsområde när panelen har placerats ut.
   * **[!UICONTROL After]** > **[!UICONTROL Go To Content Area]** > Innehållsområdets namn: Börjar fylla det angivna innehållsområdet efter att panelen har monterats.
   * **[!UICONTROL After]** > **[!UICONTROL Go To Next Page]**: Börjar fylla nästa sida efter att panelen har monterats.
   * **[!UICONTROL After]** > **[!UICONTROL Go To Page]** > Sidans namn: Börjar fylla den angivna sidan efter att panelen har monterats.
* **[!UICONTROL Pagination]** > **[!UICONTROL Overflow]**: Anger ett spill för en panel eller tabell som sträcker sig över flera sidor. Följande fält är tillgängliga i **[!UICONTROL Overflow]** avsnitt:
   * **[!UICONTROL Overflow]** > **[!UICONTROL None]**: Börjar fylla nästa sida. Om en sidbrytning inte infogas automatiskt [!DNL AEM Forms] lägger till en sidbrytning.
   * **[!UICONTROL Overflow]** > **[!UICONTROL Go to Content Area]** > Innehållsområdets namn: Börjar fylla det angivna innehållsområdet.
   * **[!UICONTROL Overflow]** > **[!UICONTROL Go To Page]** > Sidans namn: Börjar fylla den angivna sidan.

Mer information om hur du använder sidbrytningar och använder flera överordnad sidor i ett postdokument finns i [Använda sidbrytning i ett postdokument](#apply-page-breaks-in-dor) och [Använda flera överordnad sidor i ett postdokument](#apply-multiple-master-pages-dor).

**Inställningar för formulärnivå**

* **Inkludera obundna fält i DoR:** När du anger egenskapen inkluderas obundna fält från schemabaserade adaptiva formulär i postdokumentet. Som standard är det sant.
* **Uteslut fält från DoR om de är dolda:** Ange egenskapen för att exkludera dolda fält från [!UICONTROL Document of Record] när formulär skickas. När du aktiverar [Återvalidera på servern](/help/forms/using/configuring-submit-actions.md#server-side-revalidation-in-adaptive-form-server-side-revalidation-in-adaptive-form)beräknas de dolda fälten på nytt innan de utesluts från [!UICONTROL Document of Record].

## Använda en sidbrytning i ett postdokument {#apply-page-breaks-in-dor}

Du kan använda flera metoder för att tillämpa sidbrytningar i ett postdokument.

Så här använder du en sidbrytning på ett postdokument:

1. Tryck på panelen och välj ![Konfigurera](/help/forms/using/assets/configure.png)
1. Expandera **[!UICONTROL Document of Record]** för att visa egenskaperna.

1. I **[!UICONTROL Pagination]** sektion, trycka ![Mapp](/help/forms/using/assets/folder-icon.png) i **[!UICONTROL Place]** fält.
1. Tryck **[!UICONTROL Top of Next page]** och trycka **[!UICONTROL Select]**. Du kan också trycka **[!UICONTROL Top of Page]**, markerar den överordnad sidan och trycker på **[!UICONTROL Select]** för att använda sidbrytningen.
1. Tryck ![Spara](/help/forms/using/assets/save_icon.png) för att spara egenskaperna.

Den valda panelen flyttas till nästa sida.

## Använda flera överordnad sidor i ett postdokument {#apply-multiple-master-pages-dor}

Om den anpassade XDP-mallen som du väljer innehåller flera överordnad sidor visas egenskaperna för dessa sidor i [!UICONTROL content] i [!UICONTROL Document of Record] -fliken. Mer information finns i [Anpassa varumärkesinformationen i urkunder](#customize-the-branding-information-in-document-of-record).

Du kan använda flera överordnad sidor på ett postdokument genom att använda olika överordnad sidor på komponenterna i ett anpassat formulär. Använd [Sidnumrering](#document-of-record-settings) i dokumentegenskaperna om du vill använda flera överordnad sidor.

Följande är ett exempel på hur du använder flera överordnad sidor i ett postdokument: Du överför en XDP-mall som innehåller fyra överordnad sidor till [!DNL AEM Forms] server. [!DNL AEM Forms] I används mallegenskaperna som standard på postdokumentet. [!DNL AEM Forms] använder också de första överordnad sidegenskaperna i mallen på postdokumentet.

Om du vill använda den andra överordnad sidegenskapen på en panel och den tredje överordnad sidegenskapen på de paneler som följer, ska du utföra följande steg:

1. Tryck på panelen för att använda den andra överordnad sidan och markera ![Konfigurera](assets/cmppr.png).
1. I **[!UICONTROL Pagination]** sektion, trycka ![Mapp](/help/forms/using/assets/folder-icon.png) i **[!UICONTROL Place]** fält.
1. Tryck **[!UICONTROL On page]** markerar du den andra överordnad sidan och trycker på **[!UICONTROL Select]**.
AEM Forms använder den andra överordnad sidan på panelen och alla efterföljande paneler i det anpassade formuläret.
1. I **[!UICONTROL Pagination]** sektion, trycka ![Mapp](/help/forms/using/assets/folder-icon.png) i **[!UICONTROL After]** fält.
1. Tryck **[!UICONTROL Go To page]**, markerar den tredje överordnad sidan och trycker på **[!UICONTROL Select]**.
1. Tryck ![Spara](/help/forms/using/assets/save_icon.png) för att spara egenskaperna.
AEM Forms lägger till den tredje överordnad sidan på panelen och alla efterföljande paneler i det anpassade formuläret.


## Viktiga saker att tänka på när du arbetar med postdokument {#key-considerations-when-working-with-document-of-record}

Tänk på följande när du arbetar med urkunder för anpassade formulär.

* Postmallar för dokument stöder inte RTF-text. Därför visas all formaterad text i det statiska adaptiva formuläret eller i den information som fylls i av slutanvändaren som oformaterad text i postdokumentet.
* Dokumentfragment i ett anpassat formulär visas inte i postdokumentet. Däremot stöds adaptiva formulärfragment.
* Det finns inte stöd för innehållsbindning i dokument med poster som genererats för XML-schemabaserade adaptiva formulär.
* Lokaliserad version av postdokument skapas på begäran för en språkinställning när användaren begär återgivningen av postdokumentet. Lokalisering av postdokument sker tillsammans med lokalisering av anpassat formulär. Mer information om lokalisering av dokument med post och adaptiva formulär finns i [Använda arbetsflöde för AEM översättning för att lokalisera anpassningsbara formulär och urkunder](/help/forms/using/using-aem-translation-workflow-to-localize-adaptive-forms.md).
