---
title: Arbeta med streckkodade formulär
seo-title: Arbeta med streckkodade formulär
description: 'null'
seo-description: 'null'
uuid: e56c3c94-384d-401f-b418-dd34cdc57eda
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: eb28ac30-265c-4611-8247-1f4bc826f254
translation-type: tm+mt
source-git-commit: 413af4ef9bc3652e05da78d622183bcf20a8bee7

---


# Arbeta med streckkodade formulär {#working-with-barcoded-forms}

## Om tjänsten för streckkodade formulär {#about-the-barcoded-forms-service}

Den streckkodade blanketttjänsten automatiserar inhämtning av data från ifyllda och utskrivna blanketter och integrerar inhämtad information i företagets centrala IT-system.

Med hjälp av den streckkodade formulärtjänsten kan du lägga till endimensionella och tvådimensionella streckkoder i interaktiva PDF-formulär. Du kan sedan publicera streckkodsformulären på en webbplats eller distribuera dem via e-post eller cd. När en användare fyller i ett streckkodsformulär med Adobe Reader, Acrobat Professional eller Acrobat Standard uppdateras streckkoden automatiskt för att koda användarens formulärdata. Användaren kan skicka formuläret elektroniskt eller skriva ut det på papper och skicka det via post, fax eller hand. Du kan senare extrahera användardata som en del av ett automatiserat arbetsflöde och slussa data mellan godkännandeprocesser och affärssystem.

Mer information om tjänsten för streckkodade formulär finns i [Tjänstreferens för AEM-formulär](https://www.adobe.com/go/learn_aemforms_services_63).

## Avkoda streckkodade formulärdata {#decoding-barcoded-form-data}

Du kan använda API:t för streckkodsbaserade formulärtjänster för att avkoda data från ett PDF-formulär eller en bild som innehåller en streckkod. Att avkoda formulärdata innebär att extrahera data som finns i streckkoden. Innan data kan avkodas från ett PDF-formulär (eller bild) måste användaren fylla i formuläret med data.

>[!NOTE]
>
>Mer information om tjänsten för streckkodade formulär finns i [Tjänstreferens för AEM-formulär](https://www.adobe.com/go/learn_aemforms_services_63).

### Sammanfattning av steg {#summary-of-steps}

Så här avkodar du data från ett PDF-formulär:

1. Inkludera projektfiler.
1. Skapa ett streckkodat formulärKlient-API-objekt.
1. Hämta ett PDF-formulär som innehåller streckkodade data.
1. Avkoda data från PDF-formulär.
1. Konvertera data till en XML-datakälla.
1. Bearbeta avkodade data.

**Inkludera projektfiler**

Inkludera nödvändiga filer i utvecklingsprojektet. Om du skapar ett klientprogram med Java inkluderar du de JAR-filer som behövs. Om du använder webbtjänster måste du inkludera proxyfilerna.

Följande JAR-filer måste läggas till i projektets klassökväg:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-barcodedforms-client.jar
* adobe-utilities.jar (krävs om AEM Forms distribueras på JBoss)
* jbossall-client.jar (krävs om AEM Forms distribueras på JBoss)
* xercesImpl.jar (finns i &lt;installationskatalog>/Adobe/Adobe_Experience_Manager_forms/sdk/client-libs\thirdparty)

Om AEM Forms används på en J2EE-programserver som inte är JBOSS måste du ersätta adobe-utilities.jar och jbossall-client.jar med JAR-filer som är specifika för J2EE-programservern där AEM Forms används. Information om platsen för alla AEM Forms JAR-filer finns i [Inkludera Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)för AEM Forms.

**Skapa ett klient-API-objekt för streckkodade formulär**

Innan du programmässigt kan utföra en streckkodad formulärtjänståtgärd måste du skapa en klient för tjänsten Barcoded Forms. Om du använder Java API skapar du ett `BarcodedFormsServiceClient` objekt. Skapa ett `BarcodedFormsServiceService` objekt om du använder API:t för webbtjänsten för streckkodade formulär.

**Hämta ett PDF-formulär som innehåller streckkodsdata**

Du måste skaffa ett PDF-formulär som innehåller en streckkod som har fyllts i med användardata.

**Avkoda data från PDF-formuläret**

När du har fått ett PDF-formulär (eller bild) som innehåller en streckkod kan du avkoda data. Tjänsten Barcoded Forms stöder följande typer av streckkoder:

* PDF417-streckkoder.
* Datamatrisstreckkoder.
* QR-kodstreckkoder.
* Kodabarstreckkoder.
* Code 128 barcodes.
* Code 39 barcodes.
* EAN-13-streckkoder.
* EAN-8-streckkoder.

Teckenuppsättningen som hex i avkodnings-API anger att innehållet i streckkoden är kodat som en hexsträng. Om UTF-8 till exempel anges som teckenkodning i formuläret och Hex anges i avkodningsåtgärden, kodas innehållet i streckkoden som en hexsträng i &lt; `xb:content`>-elementet i avkodade utdata. Du kan konvertera det här hexadecimala värdet för att hämta det ursprungliga innehållet genom att skapa programlogik i klientprogrammet.

**Konvertera data till en XML-datakälla**

När du har avkodat formulärdata kan du konvertera dem till XDP- eller XFDF-data. Anta till exempel att du vill importera data till ett annat formulär. Om du vill importera data till ett XFA-formulär måste du konvertera data till XDP-data. Mer information finns i [Importera formulärdata](/help/forms/developing/importing-exporting-data.md#importing-form-data).

**Bearbeta avkodade data**

Du kan bearbeta konverterade data så att de uppfyller dina affärskrav. När du till exempel har avkodat och konverterat data kan du spara dem i en fil, lagra dem i en företagsdatabas, fylla i ett annat formulär och så vidare. I det här avsnittet beskrivs hur du sparar konverterade data som en XML-fil.

>[!NOTE]
>
>Den streckkodade formulärtjänsten kan inte avkoda streckkodsdata när parametrarna för radavgränsare och fältavgränsare har samma värde

**Se även**

[Avkoda streckkodsdata med Java API](barcoded-forms.md#decode-barcoded-form-data-using-the-java-api)

[Avkoda streckkodade formulärdata med webbtjänstens API](barcoded-forms.md#decode-barcoded-form-data-using-the-web-service-api)

[Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Avkoda streckkodsdata med Java API {#decode-barcoded-form-data-using-the-java-api}

Avkoda formulärdata med hjälp av API:t för streckkodade formulär (Java):

1. Inkludera projektfiler

   Inkludera JAR-klientfiler i Java-projektets klassökväg.

1. Skapa ett klient-API-objekt för streckkodade formulär

   Skapa ett `BarcodedFormsServiceClient` objekt med hjälp av dess konstruktor och skicka ett `ServiceClientFactory` objekt som innehåller anslutningsegenskaper.

1. Hämta ett PDF-formulär som innehåller streckkodsdata

   * Skapa ett `java.io.FileInputStream` objekt som representerar PDF-formuläret som innehåller streckkodade data genom att använda dess konstruktor och skicka ett strängvärde som anger PDF-dokumentets plats.
   * Skapa ett `com.adobe.idp.Document` objekt med hjälp av dess konstruktor och skicka `java.io.FileInputStream` objektet.

1. Avkoda data från PDF-formuläret

   Avkoda formulärdata genom att anropa `BarcodedFormsServiceClient` objektets `decode` metod och skicka följande värden:

   * Det `com.adobe.idp.Document` objekt som innehåller PDF-formuläret.
   * Ett `java.lang.Boolean` objekt som anger om en PDF417-streckkod ska avkodas.
   * Ett `java.lang.Boolean` objekt som anger om en datamatrisstreckkod ska avkodas.
   * Ett `java.lang.Boolean` objekt som anger om en QR-kodstreckkod ska avkodas.
   * Ett `java.lang.Boolean` objekt som anger om en codabar-streckkod ska avkodas.
   * Ett `java.lang.Boolean` objekt som anger om en kod 128-streckkod ska avkodas.
   * Ett `java.lang.Boolean` objekt som anger om en kod med streckkoden 39 ska avkodas.
   * Ett `java.lang.Boolean` objekt som anger om en EAN-13-streckkod ska avkodas.
   * Ett `java.lang.Boolean` objekt som anger om en EAN-8-streckkod ska avkodas.
   * Ett `com.adobe.livecycle.barcodedforms.CharSet` uppräkningsvärde som anger teckenuppsättningens kodningsvärde som används i streckkoden.
   Metoden `decode` returnerar ett `org.w3c.dom.Document` objekt som innehåller avkodade formulärdata.

1. Konvertera data till en XML-datakälla

   Konvertera avkodade data till antingen XDP- eller XFDF-data genom att anropa `BarcodedFormsServiceClient` objektets `extractToXML` metod och skicka följande värden:

   * Det objekt `org.w3c.dom.Document` som innehåller avkodade data (se till att du använder `decode` metodens returvärde).
   * Ett `com.adobe.livecycle.barcodedforms.Delimiter` uppräkningsvärde som anger radavgränsaren. Vi rekommenderar att du anger `Delimiter.Carriage_Return`.
   * Ett `com.adobe.livecycle.barcodedforms.Delimiter` uppräkningsvärde som anger fältavgränsaren. Ange till exempel `Delimiter.Tab`.
   * Ett `com.adobe.livecycle.barcodedforms.XMLFormat` uppräkningsvärde som anger om streckkodsdata ska konverteras till XDP- eller XFDF XML-data. Du kan till exempel ange `XMLFormat.XDP` att data ska konverteras till XDP-data.
   >[!NOTE]
   >
   >Ange inte samma värden för radavgränsaren och fältavgränsarparametrarna.

   Metoden returnerar `extractToXML` ett `java.util.List` objekt där varje element är ett `org.w3c.dom.Document` objekt. Det finns ett separat element för varje streckkod som finns i formuläret. Det vill säga, om det finns fyra streckkoder i formuläret finns det fyra element i det returnerade `java.util.List` objektet.

1. Bearbeta avkodade data

   * Iterera genom objektet `java.util.List` för att hämta varje `org.w3c.dom.Document` objekt som finns i listan.
   * För varje element i listan konverterar du `org.w3c.dom.Document` objektet till ett `com.adobe.idp.Document` objekt. (Den programlogik som konverterar ett `org.w3c.dom.Document` objekt till ett `com.adobe.idp.Document` objekt visas i avkodningsstreckkodade formulärdata med Java API-exemplet).
   * Spara XML-data som en XML-fil genom att anropa `com.adobe.idp.Document` objektets `copyToFile`och skicka ett File-objekt som representerar XML-filen.

**Se även**

[Snabbstart (SOAP-läge): Avkoda streckkodsdata med Java API](/help/forms/developing/barcoded-forms-service-java-api.md#quick-start-soap-mode-decoding-barcoded-form-data-using-the-java-api)

[Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Avkoda streckkodade formulärdata med webbtjänstens API {#decode-barcoded-form-data-using-the-web-service-api}

Avkoda formulärdata med API:t för streckkodade formulär (webbtjänst):

1. Inkludera projektfiler

   * Skapa en Microsoft .NET-klientsammansättning som använder WSDL för den streckkodade formulärtjänsten. Mer information finns i [Anropa AEM-formulär med Base64-kodning](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding).
   * Referera till Microsoft .NET-klientsammansättningen. Mer information finns i&quot;Referera till .NET-klientsammansättningen&quot; i [Anropa AEM-formulär med Base64-kodning](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding).

1. Skapa ett klient-API-objekt för streckkodade formulär

   Skapa ett objekt genom att anropa dess standardkonstruktor med hjälp av den Microsoft .NET-klientsammansättning som använder den streckkodade formulärtjänsten WSDL. `BarcodedFormsServiceService`

1. Hämta ett PDF-formulär som innehåller streckkodsdata

   * Skapa ett `BLOB` objekt med hjälp av dess konstruktor. Objektet används `BLOB` för att lagra ett PDF-dokument som innehåller en streckkod.
   * Skapa ett `System.IO.FileStream` objekt genom att anropa dess konstruktor och skicka ett strängvärde som representerar filplatsen för PDF-dokumentet och läget som filen ska öppnas i.
   * Skapa en bytearray som lagrar innehållet i `System.IO.FileStream` objektet. Du kan bestämma storleken på bytearrayen genom att hämta `System.IO.FileStream` objektets `Length` egenskap.
   * Fyll bytearrayen med strömdata genom att anropa `System.IO.FileStream` objektets `Read` metod och skicka bytearrayen, startpositionen och den strömlängd som ska läsas.
   * Fyll objektet `BLOB` genom att tilldela dess `binaryData` egenskap med innehållet i bytearrayen.

1. Avkoda data från PDF-formuläret

   Avkoda formulärdata genom att anropa `BarcodedFormsServiceService` objektets `decode` metod och skicka följande värden:

   * Det `BLOB` objekt som innehåller PDF-formuläret.
   * Ett `Boolean` objekt som anger om en PDF417-streckkod ska avkodas.
   * Ett `Boolean` objekt som anger om en datamatrisstreckkod ska avkodas.
   * Ett `Boolean` objekt som anger om en QR-kodstreckkod ska avkodas.
   * Ett `Boolean` objekt som anger om en codabar-streckkod ska avkodas.
   * Ett `Boolean` objekt som anger om en kod 128-streckkod ska avkodas.
   * Ett `Bolean` objekt som anger om en kod med streckkoden 39 ska avkodas.
   * Ett `Boolean` objekt som anger om en EAN-13-streckkod ska avkodas.
   * Ett `Boolean` objekt som anger om en EAN-8-streckkod ska avkodas.
   * Ett `CharSet` uppräkningsvärde som anger teckenuppsättningens kodningsvärde som används i streckkoden.
   Metoden returnerar `decode` ett strängvärde som innehåller avkodade formulärdata.

1. Konvertera data till en XML-datakälla

   Konvertera avkodade data till antingen XDP- eller XFDF-data genom att anropa `BarcodedFormsServiceService` objektets `extractToXML` metod och skicka följande värden:

   * Ett strängvärde som innehåller avkodade data (kontrollera att du använder `decode` metodens returvärde).
   * Ett `Delimiter` uppräkningsvärde som anger radavgränsaren. Vi rekommenderar att du anger `Delimiter.Carriage_Return`.
   * Ett `Delimiter` uppräkningsvärde som anger fältavgränsaren. Ange till exempel `Delimiter.Tab`.
   * Ett `XMLFormat` uppräkningsvärde som anger om streckkodsdata ska konverteras till XDP- eller XFDF XML-data. Du kan till exempel ange `XMLFormat.XDP` att data ska konverteras till XDP-data.
   >[!NOTE]
   >
   >Ange inte samma värden för radavgränsaren och fältavgränsarparametrarna.

   Metoden returnerar `extractToXML` en `Object` array där varje element är en `BLOB` instans. Det finns ett separat element för varje streckkod som finns i formuläret. Det vill säga, om det finns fyra streckkoder i formuläret finns det fyra element i den returnerade `Object` arrayen.

1. Bearbeta avkodade data

   * Skapa ett `System.IO.FileStream` objekt genom att anropa dess konstruktor och skicka ett strängvärde som representerar det skyddade PDF-dokumentets filplats.
   * Skapa en bytearray som lagrar datainnehållet i det `BLOB` objekt som returnerades av `encryptPDFUsingPassword` metoden. Fyll i bytearrayen genom att hämta värdet för `BLOB` objektets `binaryData` datamedlem.
   * Skapa ett `System.IO.BinaryWriter` objekt genom att anropa dess konstruktor och skicka `System.IO.FileStream` objektet.
   * Skriv bytearrayens innehåll till en PDF-fil genom att anropa `System.IO.BinaryWriter` objektets `Write` metod och skicka bytearrayen.

**Se även**

[Anropa AEM-formulär med Base64-kodning](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
