---
title: Förifyll Forms med flödeslayouter
seo-title: Prepopulating Forms with Flowable Layouts
description: Fyll i formulär i förväg med flödeslayout för att visa data för användare i ett återgivet formulär med Java API och Web Service API.
seo-description: Prepopulate forms with flowable layout to display data to users within a rendered form using the Java API and the Web Service API.
uuid: 93ccb496-e1c2-4b79-8e89-7a2abfce1537
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 30a12fc6-07b8-4c7c-b9e2-caa2bec0ac48
role: Developer
exl-id: ff087084-fb1c-43a4-ae54-cc77eb862493
source-git-commit: 10b370fd8f855f71c6d7d791c272137bb5e04d97
workflow-type: tm+mt
source-wordcount: '3478'
ht-degree: 0%

---

# Förifyll Forms med flödeslayouter {#prepopulating-forms-with-flowable-layouts1}

## Förifyll Forms med flödeslayouter {#prepopulating-forms-with-flowable-layouts2}

När du fyller i formulär i förväg visas data för användarna i ett återgivet formulär. Anta till exempel att en användare loggar in på en webbplats med ett användarnamn och lösenord. Om autentiseringen lyckas frågar klientprogrammet om det finns användarinformation i en databas. Informationen sammanfogas i formuläret och sedan återges formuläret för användaren. Det innebär att användaren kan visa anpassade data i formuläret.

Att fylla i ett formulär i förväg har följande fördelar:

* Låter användaren visa anpassade data i ett formulär.
* Minskar mängden inmatning som användaren gör för att fylla i ett formulär.
* Säkerställer dataintegriteten genom att ha kontroll över var data placeras.

Följande två XML-datakällor kan fylla i ett formulär i förväg:

* En XDP-datakälla, som är XML som följer XFA-syntax (eller XFDF-data för att fylla i ett formulär som skapats med Acrobat) i förväg.
* En godtycklig XML-datakälla som innehåller namn/värde-par som matchar formulärets fältnamn (exemplen i det här avsnittet använder en godtycklig XML-datakälla).

Det måste finnas ett XML-element för varje formulärfält som du vill fylla i i i förväg. XML-elementnamnet måste matcha fältnamnet. Ett XML-element ignoreras om det inte motsvarar ett formulärfält eller om XML-elementnamnet inte matchar fältnamnet. Det är inte nödvändigt att matcha den ordning i vilken XML-elementen visas, förutsatt att alla XML-element har angetts.

När du fyller i ett formulär som redan innehåller data i förväg måste du ange de data som redan visas i XML-datakällan. Anta att ett formulär som innehåller 10 fält innehåller data i fyra fält. Anta sedan att du vill fylla i de återstående sex fälten i förväg. I det här fallet måste du ange 10 XML-element i XML-datakällan som används för att fylla i formuläret i förväg. Om du bara anger sex element är de fyra ursprungliga fälten tomma.

Du kan t.ex. fylla i ett formulär i förväg, t.ex. exempelbekräftelseformuläret. (Se&quot;Bekräftelseformulär&quot; i [Återger interaktiv PDF forms](/help/forms/developing/rendering-interactive-pdf-forms.md).)

Om du vill fylla i exempelbekräftelseformuläret i förväg måste du skapa en XML-datakälla som innehåller tre XML-element som matchar de tre fälten i formuläret. Formuläret innehåller följande tre fält: `FirstName`, `LastName`och `Amount`. Det första steget är att skapa en XML-datakälla som innehåller XML-element som matchar fälten i formulärdesignen. Nästa steg är att tilldela datavärden till XML-elementen, vilket visas i följande XML-kod.

```xml
     <Untitled>
         <FirstName>Jerry</FirstName>
         <LastName>Johnson</LastName>
         <Amount>250000</Amount>
     </Untitled>
```

När du har fyllt i bekräftelseformuläret i förväg med den här XML-datakällan och sedan återger formuläret, visas de datavärden som du har tilldelat XML-elementen, vilket visas i följande diagram.

![pf_pf_confirmationxml3](assets/pf_pf_confirmxml3.png)

### Fylla i formulär i förväg med flödeslayouter {#prepopulating_forms_with_flowable_layouts-1}

Forms med flödeslayouter är användbara för att visa en obestämd mängd data för användarna. Eftersom formulärets layout automatiskt anpassas till mängden data som sammanfogas, behöver du inte förbestämma en fast layout eller antal sidor för formuläret som du behöver göra med ett formulär med fast layout.

Ett formulär fylls vanligtvis i med data som hämtas under körning. Det innebär att du kan fylla i ett formulär i förväg genom att skapa en XML-datakälla i minnet och placera data direkt i XML-datakällan i minnet.

Överväg ett webbaserat program, till exempel en onlinebutik. När en onlinekund har slutfört sina inköp placeras alla köpta objekt i en XML-datakälla i minnet som används för att fylla i ett formulär i förväg. I följande diagram visas den här processen, som förklaras i tabellen efter diagrammet.

![pf_pf_finsrv_webapp_v1](assets/pf_pf_finsrv_webapp_v1.png)

I följande tabell beskrivs stegen i det här diagrammet.

<table>
 <thead>
  <tr>
   <th><p>Steg</p></th>
   <th><p>Beskrivning</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>1</p></td>
   <td><p>En användare köper artiklar från en webbaserad webbutik. </p></td>
  </tr>
  <tr>
   <td><p>2</p></td>
   <td><p>När användaren är klar med sina inköp och klickar på Skicka skapas en XML-datakälla i minnet. Köpta objekt och användarinformation placeras i XML-datakällan i minnet. </p></td>
  </tr>
  <tr>
   <td><p>3</p></td>
   <td><p>XML-datakällan används för att fylla i ett inköpsorderformulär i förväg (ett exempel på det här formuläret visas efter tabellen). </p></td>
  </tr>
  <tr>
   <td><p>4</p></td>
   <td><p>Inköpsorderformuläret återges i webbläsaren på klienten. </p></td>
  </tr>
 </tbody>
</table>

I följande diagram visas ett exempel på ett inköpsorderformulär. Informationen i tabellen kan justeras efter antalet poster i XML-data.

![pf_pf_poform](assets/pf_pf_poform.png)

>[!NOTE]
>
>Ett formulär kan förifyllas med data från andra källor, till exempel en företagsdatabas eller externa program.

### Om formulärdesign {#form-design-considerations}

Forms med flödeslayouter är baserade på formulärdesigner som skapats i Designer. En formulärdesign specificerar en uppsättning regler för layout, presentation och datainhämtning, inklusive beräkning av värden baserat på användarens indata. Reglerna används när data anges i ett formulär. Fält som läggs till i ett formulär är delformulär i formulärdesignen. I inköpsorderformuläret som visas i det föregående diagrammet är till exempel varje rad ett delformulär. Mer information om hur du skapar en formulärdesign som innehåller delformulär finns i [Skapa ett inköpsorderformulär med flödeslayout](https://www.adobe.com/go/learn_aemforms_qs_poformflowable_9).

### Förstå undergrupper av data {#understanding-data-subgroups}

En XML-datakälla används för att förifylla formulär med fasta layouter och flödeslayouter. Skillnaden är dock att en XML-datakälla som fyller i ett formulär i förväg med en flödeslayout innehåller upprepade XML-element som används för att fylla i delformulär som upprepas i formuläret i förväg. Dessa upprepade XML-element kallas datagrupper.

En XML-datakälla som används för att fylla i inköpsorderformuläret som visas i det föregående diagrammet innehåller fyra upprepade dataundergrupper. Varje datagrupp motsvarar en inköpt artikel. De köpta produkterna är en skärm, en skrivbordslampa, en telefon och en adressbok.

Följande XML-datakälla används för att fylla i inköpsorderformuläret i förväg.

```xml
     <header>
         <!-- XML elements used to prepopulate non-repeating fields such as address
         <!and city
         <txtPONum>8745236985</txtPONum>
         <dtmDate>2004-02-08</dtmDate>
         <txtOrderedByCompanyName>Any Company Name</txtOrderedByCompanyName>
         <txtOrderedByAddress>555, Any Blvd.</txtOrderedByAddress>
         <txtOrderedByCity>Any City</txtOrderedByCity>
         <txtOrderedByStateProv>ST</txtOrderedByStateProv>
         <txtOrderedByZipCode>12345</txtOrderedByZipCode>
         <txtOrderedByCountry>Any Country</txtOrderedByCountry>
         <txtOrderedByPhone>(123) 456-7890</txtOrderedByPhone>
         <txtOrderedByFax>(123) 456-7899</txtOrderedByFax>
         <txtOrderedByContactName>Contact Name</txtOrderedByContactName>
         <txtDeliverToCompanyName>Any Company Name</txtDeliverToCompanyName>
         <txtDeliverToAddress>7895, Any Street</txtDeliverToAddress>
         <txtDeliverToCity>Any City</txtDeliverToCity>
         <txtDeliverToStateProv>ST</txtDeliverToStateProv>
         <txtDeliverToZipCode>12346</txtDeliverToZipCode>
         <txtDeliverToCountry>Any Country</txtDeliverToCountry>
         <txtDeliverToPhone>(123) 456-7891</txtDeliverToPhone>
         <txtDeliverToFax>(123) 456-7899</txtDeliverToFax>
         <txtDeliverToContactName>Contact Name</txtDeliverToContactName>
     </header>
     <detail>
         <!-- A data subgroup that contains information about the monitor>
         <txtPartNum>00010-100</txtPartNum>
         <txtDescription>Monitor</txtDescription>
         <numQty>1</numQty>
         <numUnitPrice>350.00</numUnitPrice>
     </detail>
     <detail>
         <!-- A data subgroup that contains information about the desk lamp>
         <txtPartNum>00010-200</txtPartNum>
         <txtDescription>Desk lamps</txtDescription>
         <numQty>3</numQty>
         <numUnitPrice>55.00</numUnitPrice>
     </detail>
     <detail>
         <!-- A data subgroup that contains information about the Phone>
             <txtPartNum>00025-275</txtPartNum>
             <txtDescription>Phone</txtDescription>
             <numQty>5</numQty>
             <numUnitPrice>85.00</numUnitPrice>
     </detail>
     <detail>
         <!-- A data subgroup that contains information about the address book>
         <txtPartNum>00300-896</txtPartNum>
         <txtDescription>Address book</txtDescription>
         <numQty>2</numQty>
         <numUnitPrice>15.00</numUnitPrice>
     </detail>
```

Observera att varje datagrupp innehåller fyra XML-element som motsvarar denna information:

* Artikelartikelnummer
* Artikelbeskrivning
* Antal artiklar
* Enhetspris

Namnet på en undergrupps överordnade XML-element måste matcha namnet på delformuläret som finns i formulärdesignen. I föregående diagram kan du till exempel observera att namnet på den överordnade XML-elementet för dataundergruppen är `detail`. Detta motsvarar namnet på delformuläret som är i den formulärdesign som inköpsorderformuläret baseras på. Om namnet på undergruppens överordnade XML-element och delformuläret inte matchar, fylls inte formuläret på serversidan i i förväg.

Varje dataundergrupp måste innehålla XML-element som matchar fältnamnen i delformuläret. The `detail` delformuläret i formulärdesignen innehåller följande fält:

* txtPartNum
* txtDescription
* numQty
* numUnitPrice

>[!NOTE]
>
>Om du försöker fylla i ett formulär i förväg med en datakälla som innehåller upprepade XML-element och du anger `RenderAtClient` alternativ till `No`är det bara den första dataposten som sammanfogas i formuläret. Om du vill vara säker på att alla dataposter sammanfogas i formuläret anger du `RenderAtClient` till `Yes`. Mer information om `RenderAtClient` alternativ, se [Återger Forms på klienten](/help/forms/developing/rendering-forms-client.md).

>[!NOTE]
>
>Mer information om tjänsten Forms finns i [Tjänstreferens för AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Sammanfattning av steg {#summary-of-steps}

Så här fyller du i ett formulär med flödeslayout i förväg:

1. Inkludera projektfiler.
1. Skapa en XML-datakälla i minnet.
1. Konvertera XML-datakällan.
1. Återge ett förifyllt formulär.

**Inkludera projektfiler**

Inkludera nödvändiga filer i utvecklingsprojektet. Om du skapar ett klientprogram med Java, inkluderar du de JAR-filer som behövs. Om du använder webbtjänster måste du inkludera proxyfilerna.

**Inkludera projektfiler**

Inkludera nödvändiga filer i utvecklingsprojektet. Om du skapar ett klientprogram med Java, inkluderar du de JAR-filer som behövs. Om du använder webbtjänster måste du inkludera proxyfilerna.

**Skapa en XML-datakälla i minnet**

Du kan använda `org.w3c.dom` klasser för att skapa en XML-datakälla i minnet för att fylla i ett formulär med flödeslayout i förväg. Placera data i en XML-datakälla som överensstämmer med formuläret. Mer information om relationen mellan ett formulär med flödeslayout och XML-datakällan finns i [Förstå undergrupper av data](#understanding-data-subgroups).

**Konvertera XML-datakällan**

En XML-datakälla i minnet som skapas med `org.w3c.dom` kan konverteras till `com.adobe.idp.Document` -objekt innan det kan användas för att fylla i ett formulär i förväg. En XML-datakälla i minnet kan konverteras med hjälp av Java XML-omformningsklasser.

>[!NOTE]
>
>Om du använder WSDL för Forms-tjänsten för att fylla i ett formulär i förväg måste du konvertera en `org.w3c.dom.Document` objekt till `BLOB` -objekt.

**Återge ett förifyllt formulär**

Du återger ett förifyllt formulär precis som andra formulär. Den enda skillnaden är att du använder `com.adobe.idp.Document` objekt som innehåller XML-datakällan för att fylla i formuläret i förväg.

**Se även**

[Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Snabbstart för Forms Service API](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[Återger interaktiv PDF forms](/help/forms/developing/rendering-interactive-pdf-forms.md)

[Skapa webbprogram som återger Forms](/help/forms/developing/creating-web-applications-renders-forms.md)

### Fylla i formulär i förväg med Java API {#prepopulating-forms-using-the-java-api}

Så här fyller du i ett formulär med flödeslayout med Forms API (Java) i förväg:

1. Inkludera projektfiler

   Inkludera JAR-klientfiler, t.ex. adobe-forms-client.jar, i Java-projektets klassökväg. Information om platsen för dessa filer finns i [Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

1. Skapa en XML-datakälla i minnet

   * Skapa ett Java `DocumentBuilderFactory` genom att anropa `DocumentBuilderFactory` class&#39; `newInstance` -metod.
   * Skapa ett Java `DocumentBuilder` genom att anropa `DocumentBuilderFactory` objektets `newDocumentBuilder` -metod.
   * Ring `DocumentBuilder` objektets `newDocument` metod för att instansiera en `org.w3c.dom.Document` -objekt.
   * Skapa XML-datakällans rotelement genom att anropa `org.w3c.dom.Document` objektets `createElement` -metod. Detta skapar en `Element` som representerar rotelementet. Skicka ett strängvärde som representerar elementets namn till `createElement` -metod. Skicka returvärdet till `Element`. Lägg sedan till rotelementet i dokumentet genom att anropa `Document` objektets `appendChild` och skicka rotelementobjektet som ett argument. Följande kodrader visar den här programlogiken:

     ` Element root = (Element)document.createElement("transaction");  document.appendChild(root);`

   * Skapa XML-datakällans rubrikelement genom att anropa `Document` objektets `createElement` -metod. Skicka ett strängvärde som representerar elementets namn till `createElement` -metod. Skicka returvärdet till `Element`. Lägg sedan till rubrikelementet i rotelementet genom att anropa `root` objektets `appendChild` och skicka rubrikelementobjektet som ett argument. De XML-element som läggs till i rubrikelementet motsvarar den statiska delen av formuläret. Följande kodrader visar den här programlogiken:

     ` Element header = (Element)document.createElement("header");  root.appendChild(header);`

   * Skapa ett underordnat element som tillhör rubrikelementet genom att anropa `Document` objektets `createElement` och skicka ett strängvärde som representerar elementets namn. Skicka returvärdet till `Element`. Ange sedan ett värde för det underordnade elementet genom att anropa dess `appendChild` och skicka `Document` objektets `createTextNode` -metoden som ett argument. Ange ett strängvärde som visas som det underordnade elementets värde. Slutligen lägger du till det underordnade elementet i rubrikelementet genom att anropa rubrikelementets `appendChild` och skicka det underordnade elementobjektet som ett argument. Följande kodrader visar den här programlogiken:

     ` Element poNum= (Element)document.createElement("txtPONum");  poNum.appendChild(document.createTextNode("8745236985"));  header.appendChild(LastName);`


   * Lägg till alla återstående element i rubrikelementet genom att upprepa det sista delsteget för varje fält som visas i den statiska delen av formuläret (i XML-datakälldiagrammet visas dessa fält i avsnitt A. (Se [Förstå undergrupper av data](#understanding-data-subgroups).)
   * Skapa XML-datakällans detail-element genom att anropa `Document` objektets `createElement` -metod. Skicka ett strängvärde som representerar elementets namn till `createElement` -metod. Skicka returvärdet till `Element`. Lägg sedan till detail-elementet i rotelementet genom att anropa `root` objektets `appendChild` och skicka detail-elementobjektet som ett argument. XML-elementen som läggs till i detail-elementet motsvarar den dynamiska delen av formuläret. Följande kodrader visar den här programlogiken:

     ` Element detail = (Element)document.createElement("detail");  root.appendChild(detail);`

   * Skapa ett underordnat element som tillhör detaljelementet genom att anropa `Document` objektets `createElement` och skicka ett strängvärde som representerar elementets namn. Skicka returvärdet till `Element`. Ange sedan ett värde för det underordnade elementet genom att anropa dess `appendChild` och skicka `Document` objektets `createTextNode` -metoden som ett argument. Ange ett strängvärde som visas som det underordnade elementets värde. Slutligen lägger du till det underordnade elementet i detail-elementet genom att anropa detail-elementets `appendChild` och skicka det underordnade elementobjektet som ett argument. Följande kodrader visar den här programlogiken:

     ` Element txtPartNum = (Element)document.createElement("txtPartNum");  txtPartNum.appendChild(document.createTextNode("00010-100"));  detail.appendChild(txtPartNum);`

   * Upprepa det sista delsteget för alla XML-element som ska läggas till i detail-elementet. Om du vill skapa den XML-datakälla som används för att fylla i inköpsorderformuläret måste du lägga till följande XML-element i detail-elementet: `txtDescription`, `numQty`och `numUnitPrice`.
   * Upprepa de två sista delstegen för alla dataobjekt som används för att fylla i formuläret i förväg.

1. Konvertera XML-datakällan

   * Skapa en `javax.xml.transform.Transformer` genom att anropa `javax.xml.transform.Transformer` objektets statiska `newInstance` -metod.
   * Skapa en `Transformer` genom att anropa `TransformerFactory` objektets `newTransformer` -metod.
   * Skapa en `ByteArrayOutputStream` genom att använda dess konstruktor.
   * Skapa en `javax.xml.transform.dom.DOMSource` genom att använda konstruktorn och skicka `org.w3c.dom.Document` objekt som skapades i steg 1.
   * Skapa en `javax.xml.transform.dom.DOMSource` genom att använda konstruktorn och skicka `ByteArrayOutputStream` -objekt.
   * Fyll i Java `ByteArrayOutputStream` genom att anropa `javax.xml.transform.Transformer` objektets `transform` metoden och skicka `javax.xml.transform.dom.DOMSource` och `javax.xml.transform.stream.StreamResult` objekt.
   * Skapa en bytearray och tilldela storleken på `ByteArrayOutputStream` till bytearrayen.
   * Fylla i bytearrayen genom att anropa `ByteArrayOutputStream` objektets `toByteArray` -metod.
   * Skapa en `com.adobe.idp.Document` genom att använda dess konstruktor och skicka bytearrayen.

1. Återge ett förifyllt formulär

   Anropa `FormsServiceClient` objektets `renderPDFForm` och skicka följande värden:

   * Ett strängvärde som anger formulärdesignens namn, inklusive filnamnstillägget.
   * A `com.adobe.idp.Document` objekt som innehåller data som ska sammanfogas med formuläret. Se till att du använder `com.adobe.idp.Document` objekt som skapats i steg ett och två.
   * A `PDFFormRenderSpec` objekt som lagrar körningsalternativ.
   * A `URLSpec` objekt som innehåller URI-värden som krävs av Forms-tjänsten.
   * A `java.util.HashMap` objekt som lagrar bifogade filer. Det här är en valfri parameter och du kan ange `null` om du inte vill bifoga filer till formuläret.

   The `renderPDFForm` returnerar en `FormsResult` objekt som innehåller en formulärdataström som måste skrivas till klientens webbläsare.

   * Skapa en `javax.servlet.ServletOutputStream` som används för att skicka en formulärdataström till klientens webbläsare.
   * Skapa en `com.adobe.idp.Document` genom att anropa `FormsResult` objekt `getOutputContent` -metod.
   * Skapa en `java.io.InputStream` genom att anropa `com.adobe.idp.Document` objektets `getInputStream` -metod.
   * Skapa en bytearray som fyller i den med formulärdataströmmen genom att anropa `InputStream` objektets `read` och skicka bytearrayen som ett argument.
   * Anropa `javax.servlet.ServletOutputStream` objektets `write` metod för att skicka formulärdataströmmen till klientens webbläsare. Skicka bytearrayen till `write` -metod.

**Se även**

[Snabbstart (SOAP-läge): Fylla i Forms i förväg med flödeslayouter med Java API](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-prepopulating-forms-with-flowable-layouts-using-the-java-api)

[Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Fylla i formulär i förväg med webbtjänstens API {#prepopulating-forms-using-the-web-service-api}

Så här fyller du i ett formulär med flödeslayout med Forms API (webbtjänsten) i förväg:

1. Inkludera projektfiler

   * Skapa Java-proxyklasser som använder Forms tjänst-WSDL. (Se [Skapa Java-proxyklasser med Apache-axeln](/help/forms/developing/invoking-aem-forms-using-web.md#creating-java-proxy-classes-using-apache-axis).)
   * Inkludera Java-proxyklasserna i klassökvägen.

1. Skapa en XML-datakälla i minnet

   * Skapa ett Java `DocumentBuilderFactory` genom att anropa `DocumentBuilderFactory` class&#39; `newInstance` -metod.
   * Skapa ett Java `DocumentBuilder` genom att anropa `DocumentBuilderFactory` objektets `newDocumentBuilder` -metod.
   * Ring `DocumentBuilder` objektets `newDocument` metod för att instansiera en `org.w3c.dom.Document` -objekt.
   * Skapa XML-datakällans rotelement genom att anropa `org.w3c.dom.Document` objektets `createElement` -metod. Detta skapar en `Element` som representerar rotelementet. Skicka ett strängvärde som representerar elementets namn till `createElement` -metod. Skicka returvärdet till `Element`. Lägg sedan till rotelementet i dokumentet genom att anropa `Document` objektets `appendChild` och skicka rotelementobjektet som ett argument. Följande kodrader visar den här programlogiken:

     ` Element root = (Element)document.createElement("transaction");  document.appendChild(root);`

   * Skapa XML-datakällans rubrikelement genom att anropa `Document` objektets `createElement` -metod. Skicka ett strängvärde som representerar elementets namn till `createElement` -metod. Skicka returvärdet till `Element`. Lägg sedan till rubrikelementet i rotelementet genom att anropa `root` objektets `appendChild` och skicka rubrikelementobjektet som ett argument. De XML-element som läggs till i rubrikelementet motsvarar den statiska delen av formuläret. Följande kodrader visar den här programlogiken:

     ` Element header = (Element)document.createElement("header");  root.appendChild(header);`

   * Skapa ett underordnat element som tillhör rubrikelementet genom att anropa `Document` objektets `createElement` och skicka ett strängvärde som representerar elementets namn. Skicka returvärdet till `Element`. Ange sedan ett värde för det underordnade elementet genom att anropa dess `appendChild` och skicka `Document` objektets `createTextNode` -metoden som ett argument. Ange ett strängvärde som visas som det underordnade elementets värde. Slutligen lägger du till det underordnade elementet i rubrikelementet genom att anropa rubrikelementets `appendChild` och skicka det underordnade elementobjektet som ett argument. Följande kodrader visar den här programlogiken:

     ` Element poNum= (Element)document.createElement("txtPONum");  poNum.appendChild(document.createTextNode("8745236985"));  header.appendChild(LastName);`

   * Lägg till alla återstående element i rubrikelementet genom att upprepa det sista delsteget för varje fält som visas i den statiska delen av formuläret (i XML-datakälldiagrammet visas dessa fält i avsnitt A. (Se [Förstå undergrupper av data](#understanding-data-subgroups).)
   * Skapa XML-datakällans detail-element genom att anropa `Document` objektets `createElement` -metod. Skicka ett strängvärde som representerar elementets namn till `createElement` -metod. Skicka returvärdet till `Element`. Lägg sedan till detail-elementet i rotelementet genom att anropa `root` objektets `appendChild` och skicka detail-elementobjektet som ett argument. XML-elementen som läggs till i detail-elementet motsvarar den dynamiska delen av formuläret. Följande kodrader visar den här programlogiken:

     ` Element detail = (Element)document.createElement("detail");  root.appendChild(detail);`

   * Skapa ett underordnat element som tillhör detaljelementet genom att anropa `Document` objektets `createElement` och skicka ett strängvärde som representerar elementets namn. Skicka returvärdet till `Element`. Ange sedan ett värde för det underordnade elementet genom att anropa dess `appendChild` och skicka `Document` objektets `createTextNode` -metoden som ett argument. Ange ett strängvärde som visas som det underordnade elementets värde. Slutligen lägger du till det underordnade elementet i detail-elementet genom att anropa detail-elementets `appendChild` och skicka det underordnade elementobjektet som ett argument. Följande kodrader visar den här programlogiken:

     ` Element txtPartNum = (Element)document.createElement("txtPartNum");  txtPartNum.appendChild(document.createTextNode("00010-100"));  detail.appendChild(txtPartNum);`

   * Upprepa det sista delsteget för alla XML-element som ska läggas till i detail-elementet. Om du vill skapa den XML-datakälla som används för att fylla i inköpsorderformuläret måste du lägga till följande XML-element i detail-elementet: `txtDescription`, `numQty`och `numUnitPrice`.
   * Upprepa de två sista delstegen för alla dataobjekt som används för att fylla i formuläret i förväg.

1. Konvertera XML-datakällan

   * Skapa en `javax.xml.transform.Transformer` genom att anropa `javax.xml.transform.Transformer` objektets statiska `newInstance` -metod.
   * Skapa en `Transformer` genom att anropa `TransformerFactory` objektets `newTransformer` -metod.
   * Skapa en `ByteArrayOutputStream` genom att använda dess konstruktor.
   * Skapa en `javax.xml.transform.dom.DOMSource` genom att använda konstruktorn och skicka `org.w3c.dom.Document` objekt som skapades i steg 1.
   * Skapa en `javax.xml.transform.dom.DOMSource` genom att använda konstruktorn och skicka `ByteArrayOutputStream` -objekt.
   * Fyll i Java `ByteArrayOutputStream` genom att anropa `javax.xml.transform.Transformer` objektets `transform` metoden och skicka `javax.xml.transform.dom.DOMSource` och `javax.xml.transform.stream.StreamResult` objekt.
   * Skapa en bytearray och tilldela storleken på `ByteArrayOutputStream` till bytearrayen.
   * Fylla i bytearrayen genom att anropa `ByteArrayOutputStream` objektets `toByteArray` -metod.
   * Skapa en `BLOB` genom att använda dess konstruktor och anropa dess `setBinaryData` och skicka bytearrayen.

1. Återge ett förifyllt formulär

   Anropa `FormsService` objektets `renderPDFForm` och skicka följande värden:

   * Ett strängvärde som anger formulärdesignens namn, inklusive filnamnstillägget.
   * A `BLOB` objekt som innehåller data som ska sammanfogas med formuläret. Se till att du använder `BLOB` objekt som skapades i steg ett och två.
   * A `PDFFormRenderSpecc` objekt som lagrar körningsalternativ. Mer information finns i [AEM Forms API-referens](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).
   * A `URLSpec` objekt som innehåller URI-värden som krävs av Forms-tjänsten.
   * A `java.util.HashMap` objekt som lagrar bifogade filer. Det här är en valfri parameter och du kan ange `null` om du inte vill bifoga filer till formuläret.
   * En tom `com.adobe.idp.services.holders.BLOBHolder` objekt som fylls i av metoden. Det här används för att lagra det återgivna PDF-formuläret.
   * En tom `javax.xml.rpc.holders.LongHolder` objekt som fylls i av metoden. (Det här argumentet lagrar antalet sidor i formuläret).
   * En tom `javax.xml.rpc.holders.StringHolder` objekt som fylls i av metoden. (Det här argumentet lagrar språkets värde).
   * En tom `com.adobe.idp.services.holders.FormsResultHolder` objekt som innehåller resultatet av den här åtgärden.

   The `renderPDFForm` metoden fyller i `com.adobe.idp.services.holders.FormsResultHolder` objekt som skickas som det sista argumentvärdet med en formulärdataström som måste skrivas till klientens webbläsare.

   * Skapa en `FormResult` genom att hämta värdet för `com.adobe.idp.services.holders.FormsResultHolder` objektets `value` datamedlem.
   * Skapa en `BLOB` objekt som innehåller formulärdata genom att anropa `FormsResult` objektets `getOutputContent` -metod.
   * Hämta innehållstypen för `BLOB` genom att anropa dess `getContentType` -metod.
   * Ange `javax.servlet.http.HttpServletResponse` objektets innehållstyp genom att anropa dess `setContentType` metoden och skicka innehållstypen för `BLOB` -objekt.
   * Skapa en `javax.servlet.ServletOutputStream` som används för att skriva formulärdataströmmen till klientens webbläsare genom att anropa `javax.servlet.http.HttpServletResponse` objektets `getOutputStream` -metod.
   * Skapa en bytearray och fylla i den genom att anropa `BLOB` objektets `getBinaryData` -metod. Den här aktiviteten tilldelar innehållet i `FormsResult` till bytearrayen.
   * Anropa `javax.servlet.http.HttpServletResponse` objektets `write` metod för att skicka formulärdataströmmen till klientens webbläsare. Skicka bytearrayen till `write` -metod.

   >[!NOTE]
   >
   >The `renderPDFForm` metoden fyller i `com.adobe.idp.services.holders.FormsResultHolder` objekt som skickas som det sista argumentvärdet med en formulärdataström som måste skrivas till klientens webbläsare.

**Se även**

[Anropa AEM Forms med Base64-kodning](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
