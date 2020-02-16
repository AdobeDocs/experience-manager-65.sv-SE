---
title: Anropa AEM-formulär med webbtjänster
seo-title: Anropa AEM-formulär med webbtjänster
description: 'null'
seo-description: 'null'
uuid: 66bcd010-c476-4b66-831d-a48307d8d67a
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: coding
discoiquuid: d5722281-bea9-4fc7-abdc-e678899e0a15
translation-type: tm+mt
source-git-commit: 7cbe3e94eddb81925072f68388649befbb027e6d

---


# Anropa AEM-formulär med webbtjänster {#invoking-aem-forms-using-web-services}

De flesta AEM Forms-tjänster i tjänstbehållaren är konfigurerade att visa en webbtjänst, med fullständigt stöd för generering av WSDL (Web Service Definition Language). Det innebär att du kan skapa proxyobjekt som använder den inbyggda SOAP-stacken i en AEM Forms-tjänst. Det innebär att AEM Forms-tjänsterna kan utbyta och bearbeta följande SOAP-meddelanden:

* **SOAP-begäran**: Skickat till en Forms-tjänst av ett klientprogram som begär en åtgärd.
* **SOAP-svar**: Skickas till ett klientprogram av en Forms-tjänst efter att en SOAP-begäran har bearbetats.

Med hjälp av webbtjänster kan du utföra samma AEM Forms-åtgärder som du kan med Java API. En fördel med att använda webbtjänster för att anropa AEM Forms-tjänster är att du kan skapa ett klientprogram i en utvecklingsmiljö som stöder SOAP. Ett klientprogram är inte bundet till en specifik utvecklingsmiljö eller programmeringsspråk. Du kan till exempel skapa ett klientprogram med Microsoft Visual Studio .NET och C# som programmeringsspråk.

AEM Forms-tjänster exponeras över SOAP-protokollet och är WSI Basic Profile 1.1-kompatibla. Web Services Interoperability (WSI) är en öppen standardorganisation som främjar interoperabilitet mellan olika plattformar. Mer information finns i [https://www.ws-i.org/](https://www.ws-i.org).

AEM Forms stöder följande webbtjänststandarder:

* **Kodning**: Stöder endast dokument- och literalkodning (vilket är den rekommenderade kodningen enligt WSI Basic-profilen). (Se [Anropa AEM-formulär med Base64-kodning](#invoking-aem-forms-using-base64-encoding).)
* **MTOM**: Representerar ett sätt att koda bilagor med SOAP-begäranden. (Se [Anropa AEM-formulär med MTOM](#invoking-aem-forms-using-mtom).)
* **SwaRef**: Representerar ett annat sätt att koda bilagor med SOAP-begäranden. (Se [Anropa AEM-formulär med SwaRef](#invoking-aem-forms-using-swaref).)
* **SOAP med bilagor**: Stöder både MIME och DIME (Direct Internet Message Encapsulation). Dessa protokoll är standardsätt att skicka bilagor via SOAP. Microsoft Visual Studio .NET-program använder DIME. (Se [Anropa AEM-formulär med Base64-kodning](#invoking-aem-forms-using-base64-encoding).)
* **WS-Security**: Stöder en tokenprofil för användarnamn och lösenord, som är ett standardsätt att skicka användarnamn och lösenord som en del av rubriken WS Security SOAP. AEM Forms stöder även grundläggande HTTP-autentisering. (Se [Skicka inloggningsuppgifter med WS-Security-huvuden](https://www.adobe.com/devnet/livecycle/articles/passing_credentials.html).)

Om du vill anropa AEM Forms-tjänster med en webbtjänst skapar du vanligtvis ett proxybibliotek som använder tjänsten WSDL. Avsnittet *Anropa AEM-formulär med webbtjänster* använder JAX-WS för att skapa Java-proxyklasser för att anropa tjänster. (Se [Skapa Java-proxyklasser med JAX-WS](#creating-java-proxy-classes-using-jax-ws).)

Du kan hämta en tjänst-WDSL genom att ange följande URL-definition (objekt inom hakparenteser är valfria):

```as3
 https://<your_serverhost>:<your_port>/soap/services/<service_name>?wsdl[&version=<version>][&async=true|false][lc_version=<lc_version>]
```

där:

* *your_serverhost* representerar IP-adressen för J2EE-programservern som är värd för AEM Forms.
* *your_port* representerar HTTP-porten som J2EE-programservern använder.
* *service_name* representerar tjänstnamnet.
* *version* representerar målversionen av en tjänst (den senaste tjänstversionen används som standard).
* `async` Anger värdet `true` för att aktivera ytterligare åtgärder för asynkront anrop ( `false` som standard).
* *lc_version* representerar den version av AEM Forms som du vill anropa.

I följande tabell visas WSDL-definitioner för tjänsten (förutsatt att AEM Forms distribueras på den lokala värden och att posten är 8080).

<table>
 <thead>
  <tr>
   <th><p>Tjänst</p></th>
   <th><p>WSDL-definition</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>Assembler</p></td>
   <td><p><code>http://localhost:8080/soap/services/ AssemblerService?wsdl</code></p></td>
  </tr>
  <tr>
   <td><p>Bakåt och återställ</p></td>
   <td><p><code>http://localhost:8080/soap/services/BackupService?wsdl</code></p></td>
  </tr>
  <tr>
   <td><p>streckkodade formulär</p></td>
   <td><p><code>http://localhost:8080/soap/services/ BarcodedFormsService?wsdl</code></p></td>
  </tr>
  <tr>
   <td><p>Konvertera PDF</p></td>
   <td><p><code>http://localhost:8080/soap/services/ ConvertPDFService?wsdl</code></p></td>
  </tr>
  <tr>
   <td><p>Distiller</p></td>
   <td><p><code>http://localhost:8080/soap/services/ DistillerService?wsdl</code></p></td>
  </tr>
  <tr>
   <td><p>DocConverter </p></td>
   <td><p><code>http://localhost:8080/soap/services/DocConverterService?WSDL</code></p></td>
  </tr>
  <tr>
   <td><p>Dokumenthantering</p></td>
   <td><p><code>http://localhost:8080/soap/services/DocumentManagementService?WSDL</code></p></td>
  </tr>
  <tr>
   <td><p>Kryptering </p></td>
   <td><p><code>http://localhost:8080/soap/services/EncryptionService?wsdl</code></p></td>
  </tr>
  <tr>
   <td><p>Formulär</p></td>
   <td><p><code>http://localhost:8080/soap/services/FormsService?wsdl</code></p></td>
  </tr>
  <tr>
   <td><p>Integrering av formulärdata</p></td>
   <td><p><code>http://localhost:8080/soap/services/FormDataIntegration?wsdl</code></p></td>
  </tr>
  <tr>
   <td><p>Generera PDF</p></td>
   <td><p><code>http://localhost:8080/soap/services/ GeneratePDFService?wsdl</code></p></td>
  </tr>
  <tr>
   <td><p>Generera 3D PDF</p></td>
   <td><p><code>http://localhost:8080/soap/services/Generate3dPDFService?WSDL</code></p></td>
  </tr>
  <tr>
   <td><p>Utdata</p></td>
   <td><p><code>http://localhost:8080/soap/services/ OutputService?wsdl</code></p></td>
  </tr>
  <tr>
   <td><p>PDF-verktyg </p></td>
   <td><p><code>http://localhost:8080/soap/services/ PDFUtilityService?wsdl</code></p></td>
  </tr>
  <tr>
   <td><p>Acrobat Reader DC-tillägg</p></td>
   <td><p><code>http://localhost:8080/soap/services/ ReaderExtensionsService?wsdl</code></p></td>
  </tr>
  <tr>
   <td><p>Databas</p></td>
   <td><p><code>http://localhost:8080/soap/services/ RepositoryService?wsdl</code></p></td>
  </tr>
  <tr>
   <td><p>Rights Management </p></td>
   <td><p><code>http://localhost:8080/soap/services/ RightsManagementService?wsdl</code></p></td>
  </tr>
  <tr>
   <td><p>Signatur </p></td>
   <td><p><code>http://localhost:8080/soap/services/ SignatureService?wsdl</code></p></td>
  </tr>
  <tr>
   <td><p>XMP-verktyg</p></td>
   <td><p><code>http://localhost:8080/soap/services/ XMPUtilityService?wsdl</code></p></td>
  </tr>
 </tbody>
</table>

**AEM Forms Process WSDL-definitioner**

Du måste ange programnamnet och processnamnet i WSDL-definitionen för att komma åt en WSDL som tillhör en process som skapats i Workbench. Anta att namnet på programmet är `MyApplication` och att processens namn är `EncryptDocument`. Ange i så fall följande WSDL-definition:

```as3
 http://localhost:8080/soap/services/MyApplication/EncryptDocument?wsdl
```

>[!NOTE]
>
>Mer information om det här exemplet på en `MyApplication/EncryptDocument` kortlivad process finns i [Exempel](/help/forms/developing/aem-forms-processes.md)på kortlivad process.

>[!NOTE]
>
>Ett program kan innehålla mappar. I det här fallet anger du mappnamnen i WSDL-definitionen:

```as3
 http://localhost:8080/soap/services/MyApplication/[<folderA>/.../<folderZ>/]EncryptDocument?wsdl
```

**Åtkomst till nya funktioner med hjälp av webbtjänster**

Den nya funktionaliteten i AEM Forms-tjänsten kan nås via webbtjänster. I AEM Forms introduceras till exempel möjligheten att koda bilagor med hjälp av MTOM. (Se [Anropa AEM-formulär med MTOM](#invoking-aem-forms-using-mtom).)

Om du vill få tillgång till nya funktioner som introducerats i AEM Forms anger du attributet i WSDL-definitionen. `lc_version` Om du till exempel vill få åtkomst till nya tjänstfunktioner (inklusive stöd för MTOM) anger du följande WSDL-definition:

```as3
 http://localhost:8080/soap/services/MyApplication/EncryptDocument?wsdl&lc_version=9.0.1
```

>[!NOTE]
>
>När du ställer in `lc_version` attributet bör du använda tre siffror. 9.0.1 är till exempel lika med version 9.0.

**BLOB-datatyp för webbtjänst**

WSDL:er för tjänsten AEM Forms definierar många datatyper. En av de viktigaste datatyperna som visas i en webbtjänst är en `BLOB` typ. Den här datatypen mappar till `com.adobe.idp.Document` klassen när du arbetar med Java-API:er för AEM Forms. (Se [Skicka data till AEM Forms-tjänster med Java API](/help/forms/developing/invoking-aem-forms-using-java.md#passing-data-to-aem-forms-services-using-the-java-api).)

Ett `BLOB` objekt skickar och hämtar binära data (t.ex. PDF-filer, XML-data o.s.v.) till och från AEM Forms-tjänster. Typen `BLOB` definieras i en tjänst-WSDL enligt följande:

```as3
 <complexType name="BLOB">
     <sequence>
         <element maxOccurs="1" minOccurs="0" name="contentType"
             type="xsd:string"/>
         <element maxOccurs="1" minOccurs="0" name="binaryData"
             type="xsd:base64Binary"/>
         <element maxOccurs="1" minOccurs="0" name="attachmentID"
             type="xsd:string"/>
         <element maxOccurs="1" minOccurs="0" name="remoteURL"
             type="xsd:string"/>
         <element maxOccurs="1" minOccurs="0" name="MTOM"
             type="xsd:base64Binary"
             xmime:expectedContentTypes="*/*"
             xmlns:xmime="https://www.w3.org/2005/05/xmlmime"/>
         <element maxOccurs="1" minOccurs="0" name="swaRef"
             type="tns1:swaRef"/>
         <element maxOccurs="1" minOccurs="0" name="attributes"
             type="impl:MyMapOf_xsd_string_To_xsd_anyType"/>
     </sequence>
 </complexType>
```

Fälten `MTOM` och `swaRef` stöds bara i AEM Forms. Du kan bara använda de nya fälten om du anger en URL-adress som innehåller `lc_version` egenskapen.

**Tillhandahålla BLOB-objekt i serviceförfrågningar**

Om en AEM Forms-tjänståtgärd kräver en `BLOB` typ som indatavärde skapar du en instans av den `BLOB` typen i programlogiken. (Många av webbtjänsternas snabbkommandon finns i *Programmering med AEM-formulär* och visar hur du arbetar med en BLOB-datatyp.)

Tilldela värden till fält som tillhör `BLOB` instansen enligt följande:

* **Base64**: Om du vill skicka data som text som kodats i ett Base64-format anger du data i `BLOB.binaryData` fältet och anger datatypen i MIME-format (till exempel `application/pdf`) i `BLOB.contentType` fältet. (Se [Anropa AEM-formulär med Base64-kodning](#invoking-aem-forms-using-base64-encoding).)
* **MTOM**: Om du vill skicka binära data i en MTOM-bilaga anger du data i `BLOB.MTOM` fältet. Den här inställningen kopplar data till SOAP-begäran med Java JAX-WS-ramverket eller SOAP-ramverkets inbyggda API. (Se [Anropa AEM-formulär med MTOM](#invoking-aem-forms-using-mtom).)
* **SwaRef**: Om du vill skicka binära data i en WS-I SwaRef-bilaga anger du data i `BLOB.swaRef` fältet. Den här inställningen kopplar data till SOAP-begäran med Java JAX-WS-ramverket. (Se [Anropa AEM-formulär med SwaRef](#invoking-aem-forms-using-swaref).)
* **MIME- eller DIME-bilaga**: Om du vill skicka data i en MIME- eller DIME-bilaga måste du bifoga data till SOAP-begäran med SOAP-ramverkets inbyggda API. Ange identifieraren för den bifogade filen i `BLOB.attachmentID` fältet. (Se [Anropa AEM-formulär med Base64-kodning](#invoking-aem-forms-using-base64-encoding).)
* **Fjärr-URL**: Om data lagras på en webbserver och är tillgängliga via en HTTP-URL, anger du HTTP-URL:en i `BLOB.remoteURL` fältet. (Se [Anropa AEM-formulär med BLOB-data via HTTP](#invoking-aem-forms-using-blob-data-over-http).)

**Åtkomst till data i BLOB-objekt som returneras från tjänster**

Överföringsprotokollet för returnerade `BLOB` objekt beror på flera faktorer, som beaktas i följande ordning och som avbryts när huvudvillkoret är uppfyllt:

1. **Mål-URL anger överföringsprotokoll**. Om mål-URL:en som anges vid SOAP-anropet innehåller parametern `blob="`*BLOB_TYPE *avgör* BLOB_TYPE *överföringsprotokollet.* BLOB_TYPE *är en platshållare för base64, dime, mime, http, mtom och swaref.
1. **Tjänstens SOAP-slutpunkt är smart**. Om följande villkor är uppfyllda returneras utdatadokumenten med samma överföringsprotokoll som indatadokumenten:

   * Tjänstens SOAP-slutpunktsparameter Standardprotokoll för utdatablobjekt anges till Smart.

      För varje tjänst med en SOAP-slutpunkt kan du med administrationskonsolen ange överföringsprotokoll för returnerade bloggar. (Se [Administrationshjälp](https://www.adobe.com/go/learn_aemforms_admin_63).)

   * AEM Forms-tjänsten tar ett eller flera dokument som indata.

1. **Tjänstens SOAP-slutpunkt är inte smart**. Det konfigurerade protokollet avgör dokumentöverföringsprotokollet och data returneras i motsvarande `BLOB` fält. Om SOAP-slutpunkten till exempel är inställd på DIME finns den returnerade blobben i `blob.attachmentID` fältet oavsett överföringsprotokollet för något indatadokument.
1. **Annars**. Om en tjänst inte tar dokumenttypen som indata, returneras utdatadokumenten i `BLOB.remoteURL` fältet via HTTP-protokollet.

Som beskrivs i det första villkoret kan du säkerställa överföringstypen för returnerade dokument genom att utöka SOAP-slutpunkts-URL:en med ett suffix enligt följande:

```as3
     https://<your_serverhost>:<your_port>/soap/services/<service
     name>?blob=base64|dime|mime|http|mtom|swaref
```

Här är korrelationen mellan överföringstyper och det fält från vilket du får data:

* **Base64-format**: Ange att suffixet `blob` ska `base64` returnera data i `BLOB.binaryData` fältet.
* **MIME- eller DIME-bilaga**: Ange `blob` suffixet till `DIME` eller `MIME` returnera data som en motsvarande bilagetyp med den bilageidentifierare som returneras i `BLOB.attachmentID` fältet. Använd SOAP-ramverkets egna API för att läsa data från den bifogade filen.
* **Fjärr-URL**: Ange att `blob` suffixet ska `http` behålla data på programservern och returnera URL:en som pekar på data i `BLOB.remoteURL` fältet.
* **MTOM eller SwaRef**: Ange `blob` suffixet till `mtom` eller `swaref` att returnera data som en motsvarande bilagetyp med den bilageidentifierare som returneras i `BLOB.MTOM` - eller `BLOB.swaRef` -fälten. Använd SOAP-ramverkets inbyggda API för att läsa data från den bifogade filen.

>[!NOTE]
>
>Vi rekommenderar att du inte överskrider 30 MB när du fyller i ett `BLOB` objekt genom att anropa dess `setBinaryData` metod. I annat fall kan det finnas en risk för att ett `OutOfMemory` undantag inträffar.

>[!NOTE]
>
>JAX WS-baserade program som använder MTOM-överföringsprotokollet är begränsade till 25 MB skickade och mottagna data. Den här begränsningen beror på ett fel i JAX-WS. Om den kombinerade storleken på skickade och mottagna filer överstiger 25 MB använder du överföringsprotokollet SwaRef i stället för MTOM. Annars finns det en risk för ett `OutOfMemory`*-undantag.*

**MTOM-överföring av base64-kodade bytearrayer**

Utöver `BLOB` objektet stöder MTOM-protokollet alla byte-array-parametrar eller byte-array-fält av komplex typ. Det innebär att klientens SOAP-ramverk som stöder MTOM kan skicka vilket element som helst som en bifogad MTOM-fil (i stället för en base64-kodad text). `xsd:base64Binary` SOAP-slutpunkter för AEM Forms kan läsa den här typen av byte-array-kodning. AEM Forms-tjänsten returnerar emellertid alltid en bytearraytyp som en base64-kodad text. Parametrarna för byte-array i utdata stöder inte MTOM.

AEM Forms-tjänster som returnerar en stor mängd binära data använder typen Dokument/BLOB i stället för bytearraytypen. Dokumenttypen är mycket effektivare när du vill skicka stora mängder data.

## Datatyper för webbtjänster {#web-service-data-types}

I följande tabell visas Java-datatyper och motsvarande webbtjänstdatatyp.

<table>
 <thead>
  <tr>
   <th><p>Java, datatyp</p></th>
   <th><p>Datatyp för webbtjänst</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p><code>java.lang.byte[]</code></p></td>
   <td><p><code>xsd:base64Binary</code></p></td>
  </tr>
  <tr>
   <td><p><code>java.lang.Boolean</code></p></td>
   <td><p><code>xsd:boolean</code></p></td>
  </tr>
  <tr>
   <td><p><code>java.util.Date</code></p></td>
   <td><p>Typen, som definieras i en tjänst-WSDL enligt följande: <code>DATE</code></p><p><code>&lt;complexType name="DATE"&gt;</code></p><p><code>&lt;sequence&gt;</code></p><p><code>&lt;element maxOccurs="1" minOccurs="0" name="date" </code><code>type="xsd:dateTime" /&gt; </code></p><p><code>&lt;element maxOccurs="1" minOccurs="0" name="calendar" </code><code>type="xsd:dateTime" /&gt; </code></p><p><code>&lt;/sequence&gt;</code></p><p><code>&lt;/complexType&gt;</code></p><p>Om en AEM Forms-tjänståtgärd tar ett <code>java.util.Date</code> värde som indata, måste SOAP-klientprogrammet skicka datumet i <code>DATE.date</code> fältet. Om du ställer in <code>DATE.calendar</code> fältet i det här fallet genereras ett körningsundantag. Om tjänsten returnerar ett <code>java.util.Date</code>datum returneras det i <code>DATE.date</code> fältet.</p></td>
  </tr>
  <tr>
   <td><p><code>java.util.Calendar</code></p></td>
   <td><p>Typen, som definieras i en tjänst-WSDL enligt följande: <code>DATE</code></p><p><code>&lt;complexType name="DATE"&gt;</code></p><p><code>&lt;sequence&gt;</code></p><p><code>&lt;element maxOccurs="1" minOccurs="0" name="date" </code><code>type="xsd:dateTime" /&gt; </code></p><p><code>&lt;element maxOccurs="1" minOccurs="0" name="calendar" </code><code>type="xsd:dateTime" /&gt; </code></p><p><code>&lt;/sequence&gt;</code></p><p><code>&lt;/complexType&gt;</code></p><p>Om en AEM Forms-tjänståtgärd tar ett <code>java.util.Calendar</code> värde som indata, måste SOAP-klientprogrammet skicka datumet i <code>DATE.caledendar</code> fältet. Om du ställer in <code>DATE.date</code> fältet i det här fallet genereras ett körningsundantag. Om tjänsten returnerar en <code>java.util.Calendar</code>så returneras datumet i <code>DATE.calendar</code> fältet. </p></td>
  </tr>
  <tr>
   <td><p><code>java.math.BigDecimal</code></p></td>
   <td><p><code>xsd:decimal</code></p></td>
  </tr>
  <tr>
   <td><p><code>com.adobe.idp.Document</code></p></td>
   <td><p><code>BLOB</code></p></td>
  </tr>
  <tr>
   <td><p><code>java.lang.Double</code></p></td>
   <td><p><code>xsd:double</code></p></td>
  </tr>
  <tr>
   <td><p><code>java.lang.Float</code></p></td>
   <td><p><code>xsd:float</code></p></td>
  </tr>
  <tr>
   <td><p><code>java.lang.Integer</code></p></td>
   <td><p><code>xsd:int</code></p></td>
  </tr>
  <tr>
   <td><p><code>java.util.List</code></p></td>
   <td><p><code>MyArrayOf_xsd_anyType</code></p></td>
  </tr>
  <tr>
   <td><p><code>java.lang.Long</code></p></td>
   <td><p><code>xsd:long</code></p></td>
  </tr>
  <tr>
   <td><p><code>java.util.Map</code></p></td>
   <td><p>The <code>apachesoap:Map</code>, which is defined in a service WSDL as following:</p><p><code>&lt;schema elementFormDefault="qualified" targetNamespace="https://xml.apache.org/xml-soap" xmlns="https://www.w3.org/2001/XMLSchema"&gt;</code></p><p><code>&lt;complexType name="mapItem"&gt;</code></p><p><code>&lt;sequence&gt;</code></p><p><code>&lt;element name="key" nillable="true" type="xsd:anyType"/&gt;</code></p><p><code>&lt;element name="value" nillable="true" type="xsd:anyType"/&gt;</code></p><p><code>&lt;/sequence&gt;</code></p><p><code>&lt;/complexType&gt;</code></p><p><code>&lt;complexType name="Map"&gt;</code></p><p><code>&lt;sequence&gt;</code></p><p><code>&lt;element maxOccurs="unbounded" minOccurs="0" name="item" </code><code>type="apachesoap:mapItem"/&gt;</code></p><p><code>&lt;/sequence&gt;</code></p><p><code>&lt;/complexType&gt;</code></p><p><code>&lt;/schema&gt;</code></p><p>Kartan visas som en sekvens av nyckel-/värdepar.</p></td>
  </tr>
  <tr>
   <td><p><code>java.lang.Object</code></p></td>
   <td><p><code>$1</code></p></td>
  </tr>
  <tr>
   <td><p><code>java.lang.Short</code></p></td>
   <td><p><code>xsd:short</code></p></td>
  </tr>
  <tr>
   <td><p><code>java.lang.String</code></p></td>
   <td><p><code>xsd:string</code></p></td>
  </tr>
  <tr>
   <td><p><code>org.w3c.dom.Document</code></p></td>
   <td><p>XML-typen, som definieras i en tjänst-WSDL enligt följande:</p><p><code>&lt;complexType name="XML"&gt;</code></p><p><code>&lt;sequence&gt;</code></p><p><code>&lt;element maxOccurs="1" minOccurs="0" name="document" </code><code>type="xsd:string" /&gt; </code></p><p><code>&lt;element maxOccurs="1" minOccurs="0" name="element" </code><code>type="xsd:string" /&gt; </code></p><p><code>&lt;/sequence&gt;</code></p><p><code>&lt;/complexType&gt;</code></p><p>Om en AEM Forms-åtgärd accepterar ett <code>org.w3c.dom.Document</code> värde skickar du XML-data i <code>XML.document</code> fältet.</p><p>Inställning av <code>XML.element</code> fältet orsakar ett körningsfel. Om tjänsten returnerar en <code>org.w3c.dom.Document</code>returneras XML-data i <code>XML.document</code> fältet.</p></td>
  </tr>
  <tr>
   <td><p><code>org.w3c.dom.Element</code></p></td>
   <td><p>XML-typen, som definieras i en tjänst-WSDL enligt följande:</p><p><code>&lt;complexType name="XML"&gt;</code></p><p><code>&lt;sequence&gt;</code></p><p><code>&lt;element maxOccurs="1" minOccurs="0" name="document" </code><code>type="xsd:string" /&gt; </code></p><p><code>&lt;element maxOccurs="1" minOccurs="0" name="element" </code><code>type="xsd:string" /&gt; </code></p><p><code>&lt;/sequence&gt;</code></p><p><code>&lt;/complexType&gt;</code></p><p>Om en AEM Forms-tjänståtgärd tar en <code>org.w3c.dom.Element</code> inmatning skickar du XML-data i <code>XML.element</code> fältet.</p><p>Inställning av <code>XML.document</code> fältet orsakar ett körningsfel. Om tjänsten returnerar en <code>org.w3c.dom.Element</code>returneras XML-data i <code>XML.element</code> fältet.</p></td>
  </tr>
 </tbody>
</table>

**Adobe Developer website**

Adobe Developer-webbplatsen innehåller följande artikel som behandlar anrop av AEM Forms-tjänster med webbtjänstens API:

[Skapa ASP.NET-program för formuläråtergivning](https://www.adobe.com/devnet/livecycle/articles/asp_net.html)

[Anropa webbtjänster med anpassade komponenter](https://www.adobe.com/devnet/livecycle/articles/extend_webservices.html)

>[!NOTE]
>
>Anrop av webbtjänster med anpassade komponenter beskriver hur du skapar en AEM Forms-komponent som anropar webbtjänster från tredje part.

## Skapa Java-proxyklasser med JAX-WS {#creating-java-proxy-classes-using-jax-ws}

Du kan använda JAX-WS för att konvertera en WSDL för Forms-tjänsten till Java-proxyklasser. Med dessa klasser kan du anropa åtgärder för AEM Forms-tjänster. Med Apache Ant kan du skapa ett byggskript som genererar Java-proxyklasser genom att referera till en AEM Forms-tjänst-WSDL. Du kan generera JAX-WS-proxyfiler genom att utföra följande steg:

1. Installera Apache Ant på klientdatorn. (Se [https://ant.apache.org/bindownload.cgi](https://ant.apache.org/bindownload.cgi).)

   * Lägg till bin-katalogen i klassökvägen.
   * Ställ in systemvariabeln på den katalog där du installerade Ant. `ANT_HOME`

1. Installera JDK 1.6 eller senare.

   * Lägg till bin-katalogen för JDK i klassökvägen.
   * Lägg till JRE-katalogen bin i klassökvägen. Den här behållaren finns i katalogen [*JDK_INSTALL_LOCATION*]/jre.
   * Ställ in systemvariabeln på den katalog där du installerade JDK:n. `JAVA_HOME`
   JDK 1.6 innehåller wimport-programmet som används i filen build.xml. JDK 1.5 innehåller inte det programmet.

1. Installera JAX-WS på klientdatorn. (Se [Java API for XML Web Services](https://jax-ws.dev.java.net/jax-ws-ea3/docs/mtom-swaref.html).)
1. Använd JAX-WS och Apache Ant för att generera Java-proxyklasser. Skapa ett Ant-byggskript för att utföra den här uppgiften. Följande skript är ett exempel på ett Ant-byggskript som heter build.xml:

   ```as3
    <?xml version="1.0" encoding="UTF-8"?>
    
    <project basedir="." default="compile">
    
    <property name="port" value="8080" />
    <property name="host" value="localhost" />
    <property name="username" value="administrator" />
    <property name="password" value="password" />
    <property name="tests" value="all" />
    
    <target name="clean" >
           <delete dir="classes" />
    </target>
    
    <target name="wsdl" depends="clean">
           <mkdir dir="classes"/>
           <exec executable="wsimport" failifexecutionfails="false" failonerror="true" resultproperty="foundWSIMPORT">
               <arg line="-keep -d classes https://${host}:${port}/soap/services/EncryptionService?wsdl&lc_version=9.0.1"/>
           </exec>
           <fail unless="foundWSIMPORT">
              !!! Failed to execute JDK's wsimport tool. Make sure that JDK 1.6 (or later) is on your PATH !!!
           </fail>
    </target>
    
    <target name="compile" depends="clean, wsdl" >
         <javac destdir="./classes" fork="true" debug="true">
            <src path="./src"/>
         </javac>
    </target>
    
    <target name="run">
         <java classname="Client" fork="yes" failonerror="true" maxmemory="200M">
            <classpath>
              <pathelement location="./classes"/>
            </classpath>
            <arg value="${port}"/>
            <arg value="${host}"/>
            <arg value="${username}"/>
            <arg value="${password}"/>
            <arg value="${tests}"/>
         </java>
    </target>
    </project>
   ```

   Observera att egenskapen är inställd på att referera till krypteringstjänsten WSDL som körs på den lokala värden i det här Ant-byggskriptet. `url` Egenskaperna `username` och `password` måste anges till ett giltigt användarnamn och lösenord för AEM-formulär. Observera att URL-adressen innehåller `lc_version` attributet. Utan att ange `lc_version` alternativet kan du inte anropa nya AEM Forms-tjänståtgärder.

   >[!NOTE]
   >
   >Ersätt `EncryptionService`med det AEM Forms-tjänstnamn som du vill anropa med hjälp av Java-proxyklasser. Om du till exempel vill skapa Java-proxyklasser för Rights Management-tjänsten anger du:

   ```as3
    http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1
   ```

1. Skapa en BAT-fil för att köra Ant-byggskriptet. Följande kommando kan finnas i en BAT-fil som ansvarar för att köra Ant-byggskriptet:

   ```as3
    ant -buildfile "build.xml" wsdl
   ```

   Placera ANT-byggskriptet i mappen C:\Program Files\Java\jaxws-ri\bin directory. Skriptet skriver JAVA-filerna till ./classes mapp. Skriptet genererar JAVA-filer som kan anropa tjänsten.

1. Paketera JAVA-filerna i en JAR-fil. Om du arbetar med Eclipse gör du så här:

   * Skapa ett nytt Java-projekt som används för att paketera JAVA-proxyfilerna i en JAR-fil.
   * Skapa en källmapp i projektet.
   * Skapa ett `com.adobe.idp.services` paket i källmappen.
   * Markera paketet och importera sedan JAVA-filerna från mappen adobe/idp/services till `com.adobe.idp.services` paketet.
   * Om det behövs skapar du ett `org/apache/xml/xmlsoap` paket i källmappen.
   * Markera källmappen och importera sedan JAVA-filerna från mappen org/apache/xml/xmlsoap.
   * Ställ in Java-kompilatorns kompatibilitetsnivå till 5.0 eller högre.
   * Bygg projektet.
   * Exportera projektet som en JAR-fil.
   * Importera den här JAR-filen i ett klientprojekts klassökväg. Importera dessutom alla JAR-filer som finns i &lt;Install Directory>\Adobe\Adobe_Experience_Manager_forms\sdk\client-libs\thirdparty.
   >[!NOTE]
   >
   >Alla Java-webbtjänstsnabbstarter (utom Forms-tjänsten) som finns i Programmering med AEM-formulär skapar Java-proxyfiler med JAX-WS. Dessutom startar alla Java-webbtjänstsnabbstarter med SwaRef. (Se [Anropa AEM-formulär med SwaRef](#invoking-aem-forms-using-swaref).)

**Se även**

[Skapa Java-proxyklasser med hjälp av Apache-axeln](#creating-java-proxy-classes-using-apache-axis)

[Anropa AEM-formulär med Base64-kodning](#invoking-aem-forms-using-base64-encoding)

[Anropa AEM-formulär med BLOB-data via HTTP](#invoking-aem-forms-using-blob-data-over-http)

[Anropa AEM-formulär med SwaRef](#invoking-aem-forms-using-swaref)

## Skapa Java-proxyklasser med hjälp av Apache-axeln {#creating-java-proxy-classes-using-apache-axis}

Du kan använda verktyget Apache Axis WSDL2Java för att konvertera en Forms-tjänst till Java-proxyklasser. Med dessa klasser kan du anropa åtgärder för Forms-tjänsten. Med Apache Ant kan du generera axelbiblioteksfiler från en tjänst-WSDL. Du kan hämta Apache-axeln på URL:en [https://ws.apache.org/axis/](https://ws.apache.org/axis/).

>[!NOTE]
>
>Webbtjänstsnabben som är associerad med Forms-tjänsten använder Java-proxyklasser som skapats med Apache Axis. Början av webbtjänsten Forms börjar också använda Base64 som kodningstyp. (Se [Snabbstart för API för Forms Service](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts).)

Du kan generera Axis Java-biblioteksfiler genom att utföra följande steg:

1. Installera Apache Ant på klientdatorn. Den finns på [https://ant.apache.org/bindownload.cgi](https://ant.apache.org/bindownload.cgi).

   * Lägg till bin-katalogen i klassökvägen.
   * Ställ in systemvariabeln på den katalog där du installerade Ant. `ANT_HOME`

1. Installera Apache Axel 1.4 på klientdatorn. Den finns på [https://ws.apache.org/axis/](https://ws.apache.org/axis/.md).
1. Ange klassökvägen för att använda Axis JAR-filerna i webbtjänstklienten, enligt anvisningarna i installationsanvisningarna för Axis på [https://ws.apache.org/axis/java/install.html](https://ws.apache.org/axis/java/install.html).
1. Använd verktyget Apache WSDL2Java i Axel för att generera Java-proxyklasser. Skapa ett Ant-byggskript för att utföra den här uppgiften. Följande skript är ett exempel på ett Ant-byggskript som heter build.xml:

   ```as3
    <?xml version="1.0"?>
    <project name="axis-wsdl2java">
    
    <path id="axis.classpath">
    <fileset dir="C:\axis-1_4\lib" >
        <include name="**/*.jar" />
    </fileset>
    </path>
    
    <taskdef resource="axis-tasks.properties" classpathref="axis.classpath" />
    
    <target name="encryption-wsdl2java-client" description="task">
    <axis-wsdl2java
        output="C:\JavaFiles"
        testcase="false"
        serverside="false"
        verbose="true"
        username="administrator"
        password="password"
        url="http://localhost:8080/soap/services/EncryptionService?wsdl&lc_version=9.0.1" >
    </axis-wsdl2java>
    </target>
    
    </project>
   ```

   Observera att egenskapen är inställd på att referera till krypteringstjänsten WSDL som körs på den lokala värden i det här Ant-byggskriptet. `url` Egenskaperna `username` och `password` måste anges till ett giltigt användarnamn och lösenord för AEM-formulär.

1. Skapa en BAT-fil för att köra Ant-byggskriptet. Följande kommando kan finnas i en BAT-fil som ansvarar för att köra Ant-byggskriptet:

   ```as3
    ant -buildfile "build.xml" encryption-wsdl2java-client
   ```

   JAVA-filerna skrivs till egenskapen C:\JavaFiles folder as specified by the `output` . Om du vill anropa Forms-tjänsten importerar du dessa JAVA-filer till klassökvägen.

   Som standard tillhör dessa filer ett Java-paket med namnet `com.adobe.idp.services`. Vi rekommenderar att du placerar dessa JAVA-filer i en JAR-fil. Importera sedan JAR-filen till klientprogrammets klasssökväg.

   >[!NOTE]
   >
   >Det finns olika sätt att lägga in JAVA-filer i en JAR. Ett sätt är att använda en Java IDE som Eclipse. Skapa ett Java-projekt och skapa ett `com.adobe.idp.services`paket (alla JAVA-filer tillhör det här paketet). Importera sedan alla JAVA-filer till paketet. Exportera projektet som en JAR-fil.

1. Ange kodningstypen genom att ändra URL:en i `EncryptionServiceLocator` klassen. Om du till exempel vill använda base64 anger du `?blob=base64` `BLOB` att objektet ska returnera binära data. Det innebär att du i `EncryptionServiceLocator` klassen hittar följande kodrad:

   ```as3
    http://localhost:8080/soap/services/EncryptionService;
   ```

   och ändra det till:

   ```as3
    http://localhost:8080/soap/services/EncryptionService?blob=base64;
   ```

1. Lägg till följande Axis JAR-filer i Java-projektets klassökväg:

   * activation.jar
   * axis.jar
   * comons-codec-1.3.jar
   * commons-collections-3.1.jar
   * comons-discovery.jar
   * commons-log.jar
   * dom3-xml-apis-2.5.0.jar
   * jai_imageio.jar
   * jaxen-1.1-beta-9.jar
   * jaxrpc.jar
   * log4j.jar
   * mail.jar
   * saaj.jar
   * wsdl4j.jar
   * xalan.jar
   * xbean.jar
   * xercesImpl.jar
   Dessa JAR-filer finns i katalogen *[]* install/Adobe/Adobe Experience Manager Forms/sdk/lib/thirdparty.

**Se även**

[Skapa Java-proxyklasser med JAX-WS](#creating-java-proxy-classes-using-jax-ws)

[Anropa AEM-formulär med Base64-kodning](#invoking-aem-forms-using-base64-encoding)

[Anropa AEM-formulär med BLOB-data via HTTP](#invoking-aem-forms-using-blob-data-over-http)

## Anropa AEM-formulär med Base64-kodning {#invoking-aem-forms-using-base64-encoding}

Du kan anropa en AEM Forms-tjänst med Base64-kodning. Base64-kodning kodar bilagor som skickas med en webbtjänstanrop. Det innebär att `BLOB` data är Base64-kodade, inte hela SOAP-meddelandet.

Anropa AEM Forms med Base64-kodning och anropa följande kortlivade AEM Forms-process `MyApplication/EncryptDocument` med Base64-kodning.

>[!NOTE]
>
>Den här processen baseras inte på en befintlig AEM Forms-process. Om du vill följa med i kodexemplet skapar du en process med namnet `MyApplication/EncryptDocument` med Workbench. (Se [Använda Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63).)

När den här processen anropas utför den följande åtgärder:

1. Hämtar det oskyddade PDF-dokumentet som skickas till processen. Den här åtgärden baseras på `SetValue` åtgärden. Indataparametern för den här processen är en `document` processvariabel med namnet `inDoc`.
1. Krypterar PDF-dokumentet med ett lösenord. Den här åtgärden baseras på `PasswordEncryptPDF` åtgärden. Lösenordskrypterade PDF-dokument returneras i en processvariabel med namnet `outDoc`.

### Skapa en .NET-klientsammansättning som använder Base64-kodning {#creating-a-net-client-assembly-that-uses-base64-encoding}

Du kan skapa en .NET-klientsammansättning för att anropa en Forms-tjänst från ett Microsoft Visual Studio .NET-projekt. Så här skapar du en .NET-klientsammansättning som använder base64-kodning:

1. Skapa en proxyklass baserad på en anrops-URL för AEM Forms.
1. Skapa ett Microsoft Visual Studio .NET-projekt som skapar .NET-klientsammansättningen.

**Skapa en proxyklass**

Du kan skapa en proxyklass som används för att skapa .NET-klientsammansättningen med ett verktyg som medföljer Microsoft Visual Studio. Namnet på verktyget är wsdl.exe och finns i installationsmappen för Microsoft Visual Studio. Om du vill skapa en proxyklass öppnar du kommandotolken och navigerar till mappen som innehåller filen wsdl.exe. Mer information om verktyget wsdl.exe finns i *MSDN-hjälpen*.

Ange följande kommando i kommandotolken:

```as3
 wsdl https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?WSDL&lc_version=9.0.1
```

Som standard skapas en CS-fil i samma mapp som baseras på namnet på WSDL. I så fall skapas en CS-fil med namnet *EncryptDocumentService.cs*. Du använder den här CS-filen för att skapa ett proxyobjekt som gör att du kan anropa tjänsten som angavs i anrops-URL:en.

Ändra URL:en i proxyklassen så att den inkluderar, så att `?blob=base64` `BLOB` objektet returnerar binära data. Leta reda på följande kodrad i klassen proxy:

```as3
 "https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument";
```

och ändra det till:

```as3
 "https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?blob=base64";
```

I avsnittet *Anropa AEM-formulär med Base64-kodning* används `MyApplication/EncryptDocument` som exempel. Om du skapar en .NET-klientsammansättning för en annan Forms-tjänst måste du ersätta `MyApplication/EncryptDocument` med namnet på tjänsten.

**Utveckla .NET-klientsammansättningen**

Skapa ett Visual Studio Class Library-projekt som skapar en .NET-klientsammansättning. CS-filen som du skapade med wsdl.exe kan importeras till det här projektet. Det här projektet skapar en DLL-fil (.NET-klientsammansättningen) som du kan använda i andra Visual Studio .NET-projekt för att anropa en tjänst.

1. Starta Microsoft Visual Studio .NET.
1. Skapa ett klassbiblioteksprojekt och ge det namnet DocumentService.
1. Importera CS-filen som du skapade med wsdl.exe.
1. Välj **Lägg till referens** på menyn **Projekt**.
1. I dialogrutan Lägg till referens väljer du **System.Web.Services.dll**.
1. Click **Select** and then click **OK**.
1. Kompilera och bygg projektet.

>[!NOTE]
>
>Den här proceduren skapar en .NET-klientsammansättning med namnet DocumentService.dll som du kan använda för att skicka SOAP-begäranden till `MyApplication/EncryptDocument` tjänsten.

>[!NOTE]
>
>Se till att du har lagt `?blob=base64` till i URL:en i den proxyklass som används för att skapa .NET-klientsammansättningen. Annars kan du inte hämta binära data från `BLOB` objektet.

**Referera till .NET-klientsammansättningen**

Placera den nyligen skapade .NET-klientsammansättningen på den dator där du utvecklar klientprogrammet. När du har placerat .NET-klientsammansättningen i en katalog kan du referera till den från ett projekt. Referera även till `System.Web.Services` biblioteket från ditt projekt. Om du inte refererar till det här biblioteket kan du inte använda .NET-klientsammansättningen för att anropa en tjänst.

1. Välj **Lägg till referens** på menyn **Projekt**.
1. Klicka på fliken **.NET** .
1. Klicka på **Bläddra** och leta upp filen DocumentService.dll.
1. Click **Select** and then click **OK**.

**Anropa en tjänst med en .NET-klientsammansättning som använder Base64-kodning**

Du kan anropa `MyApplication/EncryptDocument` tjänsten (som skapades i Workbench) med en .NET-klientsammansättning som använder Base64-kodning. Så här anropar du `MyApplication/EncryptDocument` tjänsten:

1. Skapa en Microsoft .NET-klientsammansättning som använder WSDL för tjänsten `MyApplication/EncryptDocument` .
1. Skapa ett Microsoft .NET-klientprojekt. Referera till Microsoft .NET-klientsammansättningen i klientprojektet. Referens `System.Web.Services`.
1. Skapa ett objekt med Microsoft .NET-klientsammansättningen genom att anropa dess standardkonstruktor. `MyApplication_EncryptDocumentService`
1. Ange `MyApplication_EncryptDocumentService` objektets `Credentials` egenskap med ett `System.Net.NetworkCredential` objekt. I konstruktorn anger du ett användarnamn för AEM-formulär och motsvarande lösenord. `System.Net.NetworkCredential` Ange autentiseringsvärden för att .NET-klientprogrammet ska kunna utbyta SOAP-meddelanden med AEM Forms.
1. Skapa ett `BLOB` objekt med hjälp av dess konstruktor. Objektet används `BLOB` för att lagra ett PDF-dokument som skickas till `MyApplication/EncryptDocument` processen.
1. Skapa ett `System.IO.FileStream` objekt genom att anropa dess konstruktor. Skicka ett strängvärde som representerar filplatsen för PDF-dokumentet och läget som filen ska öppnas i.
1. Skapa en bytearray som lagrar innehållet i `System.IO.FileStream` objektet. Du kan bestämma storleken på bytearrayen genom att hämta `System.IO.FileStream` objektets `Length` egenskap.
1. Fyll bytearrayen med strömdata genom att anropa `System.IO.FileStream` objektets `Read` metod. Skicka bytearrayen, startpositionen och strömlängden som ska läsas.
1. Fyll objektet `BLOB` genom att tilldela dess `binaryData` egenskap med innehållet i bytearrayen.
1. Anropa `MyApplication/EncryptDocument` processen genom att anropa `MyApplication_EncryptDocumentService` objektets `invoke` metod och skicka `BLOB` objektet som innehåller PDF-dokumentet. Den här processen returnerar ett krypterat PDF-dokument i ett `BLOB` objekt.
1. Skapa ett `System.IO.FileStream` objekt genom att anropa dess konstruktor och skicka ett strängvärde som representerar filplatsen för det lösenordskrypterade dokumentet.
1. Skapa en bytearray som lagrar datainnehållet i det `BLOB` objekt som returneras av `MyApplicationEncryptDocumentService` objektets `invoke` metod. Fyll i bytearrayen genom att hämta värdet för `BLOB` objektets `binaryData` datamedlem.
1. Skapa ett `System.IO.BinaryWriter` objekt genom att anropa dess konstruktor och skicka `System.IO.FileStream` objektet.
1. Skriv bytearrayinnehållet till en PDF-fil genom att anropa `System.IO.BinaryWriter` objektets `Write` metod och skicka bytearrayen.

### Anropa en tjänst med Java-proxyklasser och Base64-kodning {#invoking-a-service-using-java-proxy-classes-and-base64-encoding}

Du kan anropa en AEM Forms-tjänst med hjälp av Java-proxyklasser och Base64. Så här anropar du `MyApplication/EncryptDocument` tjänsten med Java-proxyklasser:

1. Skapa Java-proxyklasser med JAX-WS som använder tjänsten WSDL `MyApplication/EncryptDocument` . Använd följande WSDL-slutpunkt:

   `https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?WSDL&lc_version=9.0.1`

   >[!NOTE]
   >
   >Ersätt `hiro-xp`med IP-adressen för J2EE-programvaruleverantören som är värd för AEM Forms.

1. Paketera Java-proxyklasserna som skapats med JAX-WS till en JAR-fil.
1. Inkludera JAR-proxyfilen för Java och JAR-filerna som finns i följande sökväg:

   &lt;Install Directory>\Adobe\Adobe_Experience_Manager_forms\sdk\client-libs\thirdparty

   till klassökvägen för ditt Java-klientprojekt.

1. Skapa ett `MyApplicationEncryptDocumentService` objekt med hjälp av dess konstruktor.
1. Skapa ett `MyApplicationEncryptDocument` objekt genom att anropa `MyApplicationEncryptDocumentService` objektets `getEncryptDocument` metod.
1. Ange de anslutningsvärden som krävs för att anropa AEM-formulär genom att tilldela värden till följande datamedlemmar:

   * Tilldela WSDL-slutpunkten och kodningstypen till `javax.xml.ws.BindingProvider` objektets `ENDPOINT_ADDRESS_PROPERTY` fält. Om du vill anropa `MyApplication/EncryptDocument` tjänsten med Base64-kodning anger du följande URL-värde:

      `https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?blob=base64`

   * Tilldela AEM-formuläranvändaren till `javax.xml.ws.BindingProvider` objektets `USERNAME_PROPERTY` fält.
   * Tilldela motsvarande lösenordsvärde till `javax.xml.ws.BindingProvider` objektets `PASSWORD_PROPERTY` fält.
   I följande kodexempel visas den här programlogiken:

   ```as3
    //Set connection values required to invoke AEM Forms
    String url = "https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?blob=base64";
    String username = "administrator";
    String password = "password";
    ((BindingProvider) encryptDocClient).getRequestContext().put(BindingProvider.ENDPOINT_ADDRESS_PROPERTY, url);
    ((BindingProvider) encryptDocClient).getRequestContext().put(BindingProvider.USERNAME_PROPERTY, username);
    ((BindingProvider) encryptDocClient).getRequestContext().put(BindingProvider.PASSWORD_PROPERTY, password);
   ```

1. Hämta PDF-dokumentet som ska skickas till `MyApplication/EncryptDocument` processen genom att skapa ett `java.io.FileInputStream` objekt med hjälp av dess konstruktor. Skicka ett strängvärde som anger platsen för PDF-dokumentet.
1. Skapa en bytearray och fyll i den med innehållet i `java.io.FileInputStream` objektet.
1. Skapa ett `BLOB` objekt med hjälp av dess konstruktor.
1. Fyll i `BLOB` objektet genom att anropa dess `setBinaryData` metod och skicka bytearrayen. Objektets `BLOB` metod `setBinaryData` är den som ska anropas när Base64-kodning används. Se Ange BLOB-objekt i tjänstbegäranden.
1. Anropa `MyApplication/EncryptDocument` processen genom att anropa `MyApplicationEncryptDocument` objektets `invoke` metod. Skicka det `BLOB` objekt som innehåller PDF-dokumentet. Metoden invoke returnerar ett `BLOB` objekt som innehåller det krypterade PDF-dokumentet.
1. Skapa en bytearray som innehåller det krypterade PDF-dokumentet genom att anropa `BLOB` objektets `getBinaryData` metod.
1. Spara det krypterade PDF-dokumentet som en PDF-fil. Skriv bytearrayen till en fil.

**Se även**

[Snabbstart: Anropa en tjänst med Java-proxyfiler och Base64-kodning](/help/forms/developing/invocation-api-quick-starts.md#quick-start-invoking-a-service-using-java-proxy-files-and-base64-encoding)

[Skapa en .NET-klientsammansättning som använder Base64-kodning](#creating-a-net-client-assembly-that-uses-base64-encoding)

## Anropa AEM-formulär med MTOM {#invoking-aem-forms-using-mtom}

Du kan anropa AEM Forms-tjänster med hjälp av webbtjänststandarden MTOM. Den här standarden definierar hur binära data, t.ex. ett PDF-dokument, överförs via Internet eller intranätet. En funktion i MTOM är användningen av `XOP:Include` elementet. Det här elementet definieras i XOP-specifikationen (XML Binary Optimized Packaging) för att referera till binära bilagor i ett SOAP-meddelande.

Diskussionen här handlar om att använda MTOM för att anropa följande kortlivade AEM Forms-process med namnet `MyApplication/EncryptDocument`.

>[!NOTE]
>
>Den här processen baseras inte på en befintlig AEM Forms-process. Om du vill följa med i kodexemplet skapar du en process med namnet `MyApplication/EncryptDocument` med Workbench. (Se [Använda Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63).)

När den här processen anropas utför den följande åtgärder:

1. Hämtar det oskyddade PDF-dokumentet som skickas till processen. Den här åtgärden baseras på `SetValue` åtgärden. Indataparametern för den här processen är en `document` processvariabel med namnet `inDoc`.
1. Krypterar PDF-dokumentet med ett lösenord. Den här åtgärden baseras på `PasswordEncryptPDF` åtgärden. Lösenordskrypterade PDF-dokument returneras i en processvariabel med namnet `outDoc`.

>[!NOTE]
>
>MTOM-stöd lades till i AEM Forms, version 9.

>[!NOTE]
>
>JAX WS-baserade program som använder MTOM-överföringsprotokollet är begränsade till 25 MB skickade och mottagna data. Den här begränsningen beror på ett fel i JAX-WS. Om den kombinerade storleken på skickade och mottagna filer överstiger 25 MB använder du överföringsprotokollet SwaRef i stället för MTOM. I annat fall finns det en risk för ett `OutOfMemory` undantag.

Diskussionen här handlar om att använda MTOM i ett Microsoft .NET-projekt för att anropa AEM Forms-tjänster. Det .NET-ramverk som används är 3.5 och utvecklingsmiljön är Visual Studio 2008. Om du har WSE (Web Service Enhancements) installerat på utvecklingsdatorn tar du bort det. .NET 3.5-ramverket stöder ett SOAP-ramverk med namnet Windows Communication Foundation (WCF). När AEM Forms anropas med hjälp av MTOM stöds endast WCF (inte WSE).

### Skapa ett .NET-projekt som anropar en tjänst med hjälp av MTOM {#creating-a-net-project-that-invokes-a-service-using-mtom}

Du kan skapa ett Microsoft .NET-projekt som kan anropa en AEM Forms-tjänst med hjälp av webbtjänster. Skapa först ett Microsoft .NET-projekt med Visual Studio 2008. Om du vill anropa en AEM Forms-tjänst skapar du en servicereferens till AEM Forms-tjänsten som du vill anropa i ditt projekt. När du skapar en servicereferens anger du en URL till tjänsten AEM Forms:

```as3
 http://localhost:8080/soap/services/MyApplication/EncryptDocument?WSDL&lc_version=9.0.1
```

Ersätt `localhost` med IP-adressen för J2EE-programservern som är värd för AEM Forms. Ersätt `MyApplication/EncryptDocument` med namnet på den AEM Forms-tjänst som ska anropas. Om du till exempel vill anropa en Rights Management-åtgärd anger du:

`http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`

Alternativet gör `lc_version` att AEM Forms-funktionalitet, som MTOM, är tillgänglig. Utan att ange `lc_version` alternativet kan du inte anropa AEM Forms med MTOM.

När du har skapat en servicereferens är datatyper som är kopplade till AEM Forms-tjänsten tillgängliga för användning i ditt .NET-projekt. Så här skapar du ett .NET-projekt som anropar en AEM Forms-tjänst:

1. Skapa ett .NET-projekt med Microsoft Visual Studio 2008.
1. Välj **Lägg till tjänstreferens** på menyn **Projekt**.
1. I dialogrutan **Adress** anger du WSDL till tjänsten AEM Forms. Exempel:

   ```as3
    http://localhost:8080/soap/services/MyApplication/EncryptDocument?WSDL&lc_version=9.0.1
   ```

1. Click **Go** and then click **OK**.

### Anropa en tjänst med MTOM i ett .NET-projekt {#invoking-a-service-using-mtom-in-a-net-project}

Tänk på den `MyApplication/EncryptDocument` process som tar emot ett oskyddat PDF-dokument och returnerar ett lösenordskrypterat PDF-dokument. Så här anropar du `MyApplication/EncryptDocument` processen (som skapades i Workbench) med hjälp av MTOM:

1. Skapa ett Microsoft .NET-projekt.
1. Skapa ett `MyApplication_EncryptDocumentClient` objekt med hjälp av dess standardkonstruktor.
1. Skapa ett `MyApplication_EncryptDocumentClient.Endpoint.Address` objekt med hjälp av `System.ServiceModel.EndpointAddress` konstruktorn. Skicka ett strängvärde som anger WSDL till AEM Forms-tjänsten och kodningstypen:

   ```as3
    https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?blob=mtom
   ```

   Du behöver inte använda attributet `lc_version` . Det här attributet används när du skapar en tjänstreferens. Se dock till att du anger `?blob=mtom`.

   >[!NOTE]
   >
   >Ersätt `hiro-xp`med IP-adressen för J2EE-programvaruleverantören som är värd för AEM Forms.

1. Skapa ett `System.ServiceModel.BasicHttpBinding` objekt genom att hämta värdet för `EncryptDocumentClient.Endpoint.Binding` datamedlemmen. Sänd returvärdet till `BasicHttpBinding`.
1. Ange `System.ServiceModel.BasicHttpBinding` objektets `MessageEncoding` datamedlem till `WSMessageEncoding.Mtom`. Detta värde garanterar att MTOM används.
1. Aktivera grundläggande HTTP-autentisering genom att utföra följande åtgärder:

   * Tilldela användarnamnet för AEM-formulären till datamedlemmen `MyApplication_EncryptDocumentClient.ClientCredentials.UserName.UserName`.
   * Tilldela datamedlemmen motsvarande lösenordsvärde `MyApplication_EncryptDocumentClient.ClientCredentials.UserName.Password`.
   * Tilldela konstantvärdet `HttpClientCredentialType.Basic` till datamedlemmen `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * Tilldela konstantvärdet `BasicHttpSecurityMode.TransportCredentialOnly` till datamedlemmen `BasicHttpBindingSecurity.Security.Mode`.
   I följande kodexempel visas dessa uppgifter.

   ```as3
    //Enable BASIC HTTP authentication
    encryptProcess.ClientCredentials.UserName.UserName = "administrator";
    encryptProcess.ClientCredentials.UserName.Password = "password";
    b.Security.Transport.ClientCredentialType = HttpClientCredentialType.Basic;
    b.Security.Mode = BasicHttpSecurityMode.TransportCredentialOnly;
    b.MaxReceivedMessageSize = 4000000;
    b.MaxBufferSize = 4000000;
    b.ReaderQuotas.MaxArrayLength = 4000000;
   ```

1. Skapa ett `BLOB` objekt med hjälp av dess konstruktor. Objektet används `BLOB` för att lagra ett PDF-dokument som ska skickas till `MyApplication/EncryptDocument` processen.
1. Skapa ett `System.IO.FileStream` objekt genom att anropa dess konstruktor. Skicka ett strängvärde som representerar filplatsen för PDF-dokumentet och läget som filen ska öppnas i.
1. Skapa en bytearray som lagrar innehållet i `System.IO.FileStream` objektet. Du kan bestämma storleken på bytearrayen genom att hämta `System.IO.FileStream` objektets `Length` egenskap.
1. Fyll bytearrayen med strömdata genom att anropa `System.IO.FileStream` objektets `Read` metod. Skicka bytearrayen, startpositionen och strömlängden som ska läsas.
1. Fyll objektet `BLOB` genom att tilldela dess `MTOM` datamedlem innehållet i bytearrayen.
1. Anropa `MyApplication/EncryptDocument` processen genom att anropa `MyApplication_EncryptDocumentClient` objektets `invoke` metod. Skicka det `BLOB` objekt som innehåller PDF-dokumentet. Den här processen returnerar ett krypterat PDF-dokument i ett `BLOB` objekt.
1. Skapa ett `System.IO.FileStream` objekt genom att anropa dess konstruktor och skicka ett strängvärde som representerar det skyddade PDF-dokumentets filplats.
1. Skapa en bytearray som lagrar datainnehållet i det `BLOB` objekt som returnerades av `invoke` metoden. Fyll i bytearrayen genom att hämta värdet för `BLOB` objektets `MTOM` datamedlem.
1. Skapa ett `System.IO.BinaryWriter` objekt genom att anropa dess konstruktor och skicka `System.IO.FileStream` objektet.
1. Skriv bytearrayens innehåll till en PDF-fil genom att anropa `System.IO.BinaryWriter` objektets `Write` metod och skicka bytearrayen.

>[!NOTE]
>
>De flesta åtgärder i AEM Forms-tjänsten har en snabbstart för MTOM. Du kan visa dessa snabbstarter i en tjänsts motsvarande snabbstartsavsnitt. Om du till exempel vill se avsnittet Komma igång med [utdatatjänstens API-snabbstart](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap).

**Se även**

[Snabbstart: Anropa en tjänst med MTOM i ett .NET-projekt](/help/forms/developing/invocation-api-quick-starts.md#quick-start-invoking-a-service-using-mtom-in-a-net-project)

[Åtkomst av flera tjänster via webbtjänster](#accessing-multiple-services-using-web-services)

[Skapa ett ASP.NET-webbprogram som anropar en mänsklig, lång process](/help/forms/developing/invoking-human-centric-long-lived.md#creating-an-asp-net-web-application-that-invokes-a-human-centric-long-lived-process)

## Anropa AEM-formulär med SwaRef {#invoking-aem-forms-using-swaref}

Du kan anropa AEM Forms-tjänster med SwaRef. Innehållet i `wsi:swaRef` XML-elementet skickas som en bifogad fil i ett SOAP-brödtext som lagrar referensen till den bifogade filen. När du anropar en Forms-tjänst med hjälp av SwaRef skapar du Java-proxyklasser med Java API för XML-webbtjänster (JAX-WS). (Se [Java API for XML Web Services](https://jax-ws.dev.java.net/jax-ws-ea3/docs/mtom-swaref.html).)

Diskussionen här handlar om att anropa följande kortlivade Forms-process som heter `MyApplication/EncryptDocument` med SwaRef.

>[!NOTE]
>
>Den här processen baseras inte på en befintlig AEM Forms-process. Om du vill följa med i kodexemplet skapar du en process med namnet `MyApplication/EncryptDocument` med Workbench. (Se [Använda Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63).)

När den här processen anropas utför den följande åtgärder:

1. Hämtar det oskyddade PDF-dokumentet som skickas till processen. Den här åtgärden baseras på `SetValue` åtgärden. Indataparametern för den här processen är en `document` processvariabel med namnet `inDoc`.
1. Krypterar PDF-dokumentet med ett lösenord. Den här åtgärden baseras på `PasswordEncryptPDF` åtgärden. Lösenordskrypterade PDF-dokument returneras i en processvariabel med namnet `outDoc`.

>[!NOTE]
>
>Stöd för SwaRef har lagts till i AEM Forms

Nedan beskrivs hur du anropar Forms-tjänster med hjälp av SwaRef i ett Java-klientprogram. Java-programmet använder proxyklasser som skapats med JAX-WS.

### Anropa en tjänst med JAX-WS-biblioteksfiler som använder SwaRef {#invoke-a-service-using-jax-ws-library-files-that-use-swaref}

Så här anropar du `MyApplication/EncryptDocument` processen med Java-proxyfiler som skapats med JAX-WS och SwaRef:

1. Skapa Java-proxyklasser med JAX-WS som använder tjänsten WSDL `MyApplication/EncryptDocument` . Använd följande WSDL-slutpunkt:

   ```as3
    https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?WSDL&lc_version=9.0.1
   ```

   Mer information finns i [Skapa Java-proxyklasser med JAX-WS](#creating-java-proxy-classes-using-jax-ws).

   >[!NOTE]
   >
   >Ersätt `hiro-xp`* med IP-adressen för J2EE-programservern som är värd för AEM Forms. *

1. Paketera Java-proxyklasserna som skapats med JAX-WS till en JAR-fil.
1. Inkludera JAR-proxyfilen för Java och JAR-filerna som finns i följande sökväg:

   &lt;Install Directory>\Adobe\Adobe_Experience_Manager_forms\sdk\client-libs\thirdparty

   till klassökvägen för ditt Java-klientprojekt.

1. Skapa ett `MyApplicationEncryptDocumentService` objekt med hjälp av dess konstruktor.
1. Skapa ett `MyApplicationEncryptDocument` objekt genom att anropa `MyApplicationEncryptDocumentService` objektets `getEncryptDocument` metod.
1. Ange de anslutningsvärden som krävs för att anropa AEM-formulär genom att tilldela värden till följande datamedlemmar:

   * Tilldela WSDL-slutpunkten och kodningstypen till `javax.xml.ws.BindingProvider` objektets `ENDPOINT_ADDRESS_PROPERTY` fält. Om du vill anropa `MyApplication/EncryptDocument` tjänsten med SwaRef-kodning anger du följande URL-värde:

      ` https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?blob=swaref`

   * Tilldela AEM-formuläranvändaren till `javax.xml.ws.BindingProvider` objektets `USERNAME_PROPERTY` fält.
   * Tilldela motsvarande lösenordsvärde till `javax.xml.ws.BindingProvider` objektets `PASSWORD_PROPERTY` fält.
   I följande kodexempel visas den här programlogiken:

   ```as3
    //Set connection values required to invoke AEM Forms
    String url = "https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?blob=swaref";
    String username = "administrator";
    String password = "password";
    ((BindingProvider) encryptDocClient).getRequestContext().put(BindingProvider.ENDPOINT_ADDRESS_PROPERTY, url);
    ((BindingProvider) encryptDocClient).getRequestContext().put(BindingProvider.USERNAME_PROPERTY, username);
    ((BindingProvider) encryptDocClient).getRequestContext().put(BindingProvider.PASSWORD_PROPERTY, password);
   ```

1. Hämta PDF-dokumentet som ska skickas till `MyApplication/EncryptDocument` processen genom att skapa ett `java.io.File` objekt med hjälp av dess konstruktor. Skicka ett strängvärde som anger platsen för PDF-dokumentet.
1. Skapa ett `javax.activation.DataSource` objekt med hjälp av `FileDataSource` konstruktorn. Skicka `java.io.File` objektet.
1. Skapa ett `javax.activation.DataHandler` objekt med hjälp av dess konstruktor och skicka `javax.activation.DataSource` objektet.
1. Skapa ett `BLOB` objekt med hjälp av dess konstruktor.
1. Fyll i `BLOB` objektet genom att anropa dess `setSwaRef` metod och skicka `javax.activation.DataHandler` objektet.
1. Anropa `MyApplication/EncryptDocument` processen genom att anropa `MyApplicationEncryptDocument` objektets `invoke` metod och skicka `BLOB` objektet som innehåller PDF-dokumentet. Metoden invoke returnerar ett `BLOB` objekt som innehåller ett krypterat PDF-dokument.
1. Fylla i ett `javax.activation.DataHandler` objekt genom att anropa `BLOB` objektets `getSwaRef` metod.
1. Konvertera `javax.activation.DataHandler` objektet till en `java.io.InputSteam` instans genom att anropa `javax.activation.DataHandler` objektets `getInputStream` metod.
1. Skriv instansen `java.io.InputSteam` till en PDF-fil som representerar det krypterade PDF-dokumentet.

>[!NOTE]
>
>De flesta åtgärder i tjänsten AEM Forms har en SwaRef-snabbstart. Du kan visa dessa snabbstarter i en tjänsts motsvarande snabbstartsavsnitt. Om du till exempel vill se avsnittet Komma igång med [utdatatjänstens API-snabbstart](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap).

**Se även**

[Snabbstart: Anropa en tjänst med SwaRef i ett Java-projekt](/help/forms/developing/invocation-api-quick-starts.md#quick-start-invoking-a-service-using-swaref-in-a-java-project)

## Anropa AEM-formulär med BLOB-data via HTTP {#invoking-aem-forms-using-blob-data-over-http}

Du kan anropa AEM Forms-tjänster med webbtjänster och skicka BLOB-data via HTTP. Att skicka BLOB-data via HTTP är en alternativ teknik i stället för att använda base64-kodning, DIME eller MIME. Du kan till exempel skicka data via HTTP i ett Microsoft .NET-projekt som använder Web Service Enhancement 3.0, som inte stöder DIME eller MIME. När du använder BLOB-data över HTTP överförs indata innan AEM Forms-tjänsten anropas.

Anrop av AEM Forms med BLOB Data via HTTP diskuterar anrop av följande kortlivade AEM Forms-process som kallas `MyApplication/EncryptDocument` genom att skicka BLOB-data via HTTP.

>[!NOTE]
>
>Den här processen baseras inte på en befintlig AEM Forms-process. Om du vill följa med i kodexemplet skapar du en process med namnet `MyApplication/EncryptDocument` med Workbench. (Se [Använda Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63).)

När den här processen anropas utför den följande åtgärder:

1. Hämtar det oskyddade PDF-dokumentet som skickas till processen. Den här åtgärden baseras på `SetValue` åtgärden. Indataparametern för den här processen är en `document` processvariabel med namnet `inDoc`.
1. Krypterar PDF-dokumentet med ett lösenord. Den här åtgärden baseras på `PasswordEncryptPDF` åtgärden. Lösenordskrypterade PDF-dokument returneras i en processvariabel med namnet `outDoc`.

>[!NOTE]
>
>Vi rekommenderar att du är bekant med Anropa AEM Forms med SOAP. (Se [Anropa AEM-formulär med webbtjänster](#invoking-aem-forms-using-web-services).)

### Skapa en .NET-klientsammansättning som använder data över HTTP {#creating-a-net-client-assembly-that-uses-data-over-http}

Om du vill skapa en klientsammansättning som använder data över HTTP följer du den process som anges i [Anropa AEM-formulär med Base64-kodning](#invoking-aem-forms-using-base64-encoding). Ändra emellertid URL:en i klassen proxy så att den omfattar `?blob=http` i stället för `?blob=base64`. Den här åtgärden ser till att data skickas via HTTP. Leta reda på följande kodrad i klassen proxy:

```as3
 "http://localhost:8080/soap/services/MyApplication/EncryptDocument";
```

och ändra det till:

```as3
 "http://localhost:8080/soap/services/MyApplication/EncryptDocument?blob=http";
```

**Referera till .NET clienMyApplication/EncryptDocument-sammansättningen**

Placera den nya .NET-klientsammansättningen på den dator där du utvecklar klientprogrammet. När du har placerat .NET-klientsammansättningen i en katalog kan du referera till den från ett projekt. Referera till `System.Web.Services` biblioteket från ditt projekt. Om du inte refererar till det här biblioteket kan du inte använda .NET-klientsammansättningen för att anropa en tjänst.

1. Välj **Lägg till referens** på menyn **Projekt**.
1. Klicka på fliken **.NET** .
1. Klicka på **Bläddra** och leta upp filen DocumentService.dll.
1. Click **Select** and then click **OK**.

**Anropa en tjänst med en .NET-klientsammansättning som använder BLOB-data över HTTP**

Du kan anropa `MyApplication/EncryptDocument` tjänsten (som skapades i Workbench) med en .NET-klientsammansättning som använder data via HTTP. Så här anropar du `MyApplication/EncryptDocument` tjänsten:

1. Skapa .NET-klientsammansättningen.
1. Referera till Microsoft .NET-klientsammansättningen. Skapa ett Microsoft .NET-klientprojekt. Referera till Microsoft .NET-klientsammansättningen i klientprojektet. Referens `System.Web.Services`.
1. Skapa ett objekt med Microsoft .NET-klientsammansättningen genom att anropa dess standardkonstruktor. `MyApplication_EncryptDocumentService`
1. Ange `MyApplication_EncryptDocumentService` objektets `Credentials` egenskap med ett `System.Net.NetworkCredential` objekt. I konstruktorn anger du ett användarnamn för AEM-formulär och motsvarande lösenord. `System.Net.NetworkCredential` Ange autentiseringsvärden för att .NET-klientprogrammet ska kunna utbyta SOAP-meddelanden med AEM Forms.
1. Skapa ett `BLOB` objekt med hjälp av dess konstruktor. Objektet `BLOB` används för att skicka data till `MyApplication/EncryptDocument` processen.
1. Tilldela ett strängvärde till `BLOB` objektets `remoteURL` datamedlem som anger URI-platsen för ett PDF-dokument som ska skickas till `MyApplication/EncryptDocument`tjänsten.
1. Anropa `MyApplication/EncryptDocument` processen genom att anropa `MyApplication_EncryptDocumentService` objektets `invoke` metod och skicka `BLOB` objektet. Den här processen returnerar ett krypterat PDF-dokument i ett `BLOB` objekt.
1. Skapa ett `System.UriBuilder` objekt med hjälp av dess konstruktor och skicka värdet för det returnerade `BLOB` objektets `remoteURL` datamedlem.
1. Konvertera `System.UriBuilder` objektet till ett `System.IO.Stream` objekt. (Den snabbstart på C# som följer den här listan visar hur du utför den här uppgiften.)
1. Skapa en bytearray och fyll i den med data som finns i `System.IO.Stream` objektet.
1. Skapa ett `System.IO.BinaryWriter` objekt genom att anropa dess konstruktor och skicka `System.IO.FileStream` objektet.
1. Skriv bytearrayinnehållet till en PDF-fil genom att anropa `System.IO.BinaryWriter` objektets `Write` metod och skicka bytearrayen.

### Anropa en tjänst med Java-proxyklasser och BLOB-data via HTTP {#invoking-a-service-using-java-proxy-classes-and-blob-data-over-http}

Du kan anropa en AEM Forms-tjänst med hjälp av Java-proxyklasser och BLOB-data via HTTP. Så här anropar du `MyApplication/EncryptDocument` tjänsten med Java-proxyklasser:

1. Skapa Java-proxyklasser med JAX-WS som använder tjänsten WSDL `MyApplication/EncryptDocument` . Använd följande WSDL-slutpunkt:

   ```as3
    https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?WSDL&lc_version=9.0.1
   ```

   Mer information finns i [Skapa Java-proxyklasser med JAX-WS](#creating-java-proxy-classes-using-jax-ws).

   >[!NOTE]
   >
   >Ersätt `hiro-xp`* med IP-adressen för J2EE-programservern som är värd för AEM Forms. *

1. Paketera Java-proxyklasserna som skapats med JAX-WS till en JAR-fil.
1. Inkludera JAR-proxyfilen för Java och JAR-filerna som finns i följande sökväg:

   &lt;Install Directory>\Adobe\Adobe_Experience_Manager_forms\sdk\client-libs\thirdparty

   till klassökvägen för ditt Java-klientprojekt.

1. Skapa ett `MyApplicationEncryptDocumentService` objekt med hjälp av dess konstruktor.
1. Skapa ett `MyApplicationEncryptDocument` objekt genom att anropa `MyApplicationEncryptDocumentService` objektets `getEncryptDocument` metod.
1. Ange de anslutningsvärden som krävs för att anropa AEM-formulär genom att tilldela värden till följande datamedlemmar:

   * Tilldela WSDL-slutpunkten och kodningstypen till `javax.xml.ws.BindingProvider` objektets `ENDPOINT_ADDRESS_PROPERTY` fält. Om du vill anropa `MyApplication/EncryptDocument` tjänsten med BLOB över HTTP-kodning anger du följande URL-värde:

      `https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?blob=http`

   * Tilldela AEM-formuläranvändaren till `javax.xml.ws.BindingProvider` objektets `USERNAME_PROPERTY` fält.
   * Tilldela motsvarande lösenordsvärde till `javax.xml.ws.BindingProvider` objektets `PASSWORD_PROPERTY` fält.
   I följande kodexempel visas den här programlogiken:

   ```as3
    //Set connection values required to invoke AEM Forms
    String url = "https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?blob=http";
    String username = "administrator";
    String password = "password";
    ((BindingProvider) encryptDocClient).getRequestContext().put(BindingProvider.ENDPOINT_ADDRESS_PROPERTY, url);
    ((BindingProvider) encryptDocClient).getRequestContext().put(BindingProvider.USERNAME_PROPERTY, username);
    ((BindingProvider) encryptDocClient).getRequestContext().put(BindingProvider.PASSWORD_PROPERTY, password);
   ```

1. Skapa ett `BLOB` objekt med hjälp av dess konstruktor.
1. Fyll i `BLOB` objektet genom att anropa dess `setRemoteURL` metod. Skicka ett strängvärde som anger URI-platsen för ett PDF-dokument som ska skickas till `MyApplication/EncryptDocument` tjänsten.
1. Anropa `MyApplication/EncryptDocument` processen genom att anropa `MyApplicationEncryptDocument` objektets `invoke` metod och skicka `BLOB` objektet som innehåller PDF-dokumentet. Den här processen returnerar ett krypterat PDF-dokument i ett `BLOB` objekt.
1. Skapa en bytearray för att lagra dataströmmen som representerar det krypterade PDF-dokumentet. Anropa `BLOB` objektets `getRemoteURL` metod (använd det `BLOB` objekt som returneras av `invoke` metoden).
1. Skapa ett `java.io.File` objekt med hjälp av dess konstruktor. Det här objektet representerar det krypterade PDF-dokumentet.
1. Skapa ett `java.io.FileOutputStream` objekt med hjälp av dess konstruktor och skicka `java.io.File` objektet.
1. Anropa `java.io.FileOutputStream` objektets `write` metod. Skicka bytearrayen som innehåller dataströmmen som representerar det krypterade PDF-dokumentet.

## Anropa AEM-formulär med DIME {#invoking-aem-forms-using-dime}

Du kan anropa AEM Forms-tjänster med SOAP med bifogade filer. AEM Forms stöder både MIME- och DIME-webbtjänststandarderna. Med DIME kan du skicka binära bilagor, t.ex. PDF-dokument, tillsammans med anropsbegäranden i stället för att koda bilagan. Avsnittet *Anropa AEM Forms med DIME* handlar om att anropa följande kortvariga AEM Forms-process som heter `MyApplication/EncryptDocument` med DIME.

När den här processen anropas utför den följande åtgärder:

1. Hämtar det oskyddade PDF-dokumentet som skickas till processen. Den här åtgärden baseras på `SetValue` åtgärden. Indataparametern för den här processen är en `document` processvariabel med namnet `inDoc`.
1. Krypterar PDF-dokumentet med ett lösenord. Den här åtgärden baseras på `PasswordEncryptPDF` åtgärden. Lösenordskrypterade PDF-dokument returneras i en processvariabel med namnet `outDoc`.

Den här processen baseras inte på en befintlig AEM Forms-process. Om du vill följa med i kodexemplen skapar du en process med namnet `MyApplication/EncryptDocument`**med Workbench. (Se [Använda Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63).)

>[!NOTE]
>
>Anrop av AEM Forms-tjänståtgärder med DIME är föråldrat. Vi rekommenderar att du använder MTOM. (Se [Anropa AEM-formulär med MTOM](#invoking-aem-forms-using-mtom).)

### Skapa ett .NET-projekt som använder DIME {#creating-a-net-project-that-uses-dime}

Så här skapar du ett .NET-projekt som kan anropa en Forms-tjänst med DIME:

* Installera Web Services Enhancements 2.0 på utvecklingsdatorn.
* I ditt .NET-projekt skapar du en webbreferens till FormsAEM Forms-tjänsten.

**Installerar webbtjänsttillägg 2.0**

Installera Web Services Enhancements 2.0 på utvecklingsdatorn och integrera det med Microsoft Visual Studio .NET. Du kan hämta webbtjänsttillägg 2.0 från [Microsoft Download Center.](https://www.microsoft.com/downloads/search.aspx)

På den här webbsidan söker du efter Web Services Enhancements 2.0 och laddar ned det till utvecklingsdatorn. Den här nedladdningen placerar en fil med namnet Microsoft WSE 2.0 SPI.msi på datorn. Kör installationsprogrammet och följ anvisningarna online.

>[!NOTE]
>
>Web Services Enhancements 2.0 stöder DIME. Den version av Microsoft Visual Studio som stöds är 2003 när du arbetar med Web Services Enhancements 2.0. Web Services Enhancements 3.0 stöder inte DIME; Den stöder dock MTOM.

**Skapa en webbreferens till en AEM Forms-tjänst**

När du har installerat Web Services Enhancements 2.0 på utvecklingsdatorn och skapat ett Microsoft .NET-projekt skapar du en webbreferens till Forms-tjänsten. Om du till exempel vill skapa en webbreferens till `MyApplication/EncryptDocument` processen och anta att Forms är installerat på den lokala datorn anger du följande URL:

```as3
     http://localhost:8080/soap/services/MyApplication/EncryptDocument?WSDL
```

När du har skapat en webbreferens är följande två proxydatatyper tillgängliga som du kan använda i ditt .NET-projekt: `EncryptDocumentService` och `EncryptDocumentServiceWse`. Använd `MyApplication/EncryptDocument` typen om du vill anropa `EncryptDocumentServiceWse` processen med DIME.

>[!NOTE]
>
>Innan du skapar en webbreferens till Forms-tjänsten bör du kontrollera att du har referenser till Web Services Enhancements 2.0 i ditt projekt. (Se &quot;Installera Web Services Enhancements 2.0&quot;.)

**Referera till WSE-biblioteket**

1. Välj Lägg till referens på Projekt-menyn.
1. Välj Microsoft.Web.Services2.dll i dialogrutan Lägg till referens.
1. Välj System.Web.Services.dll.
1. Klicka på Välj och sedan på OK.

**Skapa en webbreferens till en formulärtjänst**

1. Välj Lägg till webbreferens på Projekt-menyn.
1. Ange URL-adressen till Forms-tjänsten i dialogrutan URL.
1. Klicka på Gå och sedan på Lägg till referens.

>[!NOTE]
>
>Se till att du aktiverar ditt .NET-projekt så att det använder WSE-biblioteket. I projektutforskaren högerklickar du på projektnamnet och väljer Aktivera WSE 2.0. Kontrollera att kryssrutan i dialogrutan som visas är markerad.

**Anropa en tjänst med DIME i ett .NET-projekt**

Du kan anropa en Forms-tjänst med DIME. Tänk på den `MyApplication/EncryptDocument` process som tar emot ett oskyddat PDF-dokument och returnerar ett lösenordskrypterat PDF-dokument. Så här anropar du `MyApplication/EncryptDocument` processen med DIME:

1. Skapa ett Microsoft .NET-projekt som gör att du kan anropa en Forms-tjänst med DIME. Se till att du inkluderar Web Services Enhancements 2.0 och skapar en webbreferens till AEM Forms-tjänsten.
1. När du har angett en webbreferens för `MyApplication/EncryptDocument` processen skapar du ett `EncryptDocumentServiceWse` objekt med hjälp av dess standardkonstruktor.
1. Ange `EncryptDocumentServiceWse` objektets `Credentials` datamedlem med ett `System.Net.NetworkCredential` värde som anger användarnamnet och lösenordet för AEM-formulären.
1. Skapa ett `Microsoft.Web.Services2.Dime.DimeAttachment` objekt med hjälp av dess konstruktor och skicka följande värden:

   * Ett strängvärde som anger ett GUID-värde. Du kan få ett GUID-värde genom att anropa `System.Guid.NewGuid.ToString` metoden.
   * Ett strängvärde som anger innehållstypen. Eftersom processen kräver ett PDF-dokument anger du `application/pdf`.
   * Ett `TypeFormat` uppräkningsvärde. Ange `TypeFormat.MediaType`.
   * Ett strängvärde som anger platsen för PDF-dokumentet som ska skickas till AEM Forms-processen.

1. Skapa ett `BLOB` objekt med hjälp av dess konstruktor.
1. Lägg till DIME-bilagan till `BLOB` objektet genom att tilldela `Microsoft.Web.Services2.Dime.DimeAttachment` objektets `Id` datamedlementvärde till `BLOB` objektets `attachmentID` datamedlem.
1. Anropa `EncryptDocumentServiceWse.RequestSoapContext.Attachments.Add` metoden och skicka `Microsoft.Web.Services2.Dime.DimeAttachment` objektet.
1. Anropa `MyApplication/EncryptDocument` processen genom att anropa `EncryptDocumentServiceWse` objektets `invoke` metod och skicka det `BLOB` objekt som innehåller DIME-bilagan. Den här processen returnerar ett krypterat PDF-dokument i ett `BLOB` objekt.
1. Hämta identifierarvärdet för bilagor genom att hämta värdet för det returnerade `BLOB` objektets `attachmentID` datamedlem.
1. Iterera genom de bifogade filerna i `EncryptDocumentServiceWse.ResponseSoapContext.Attachments` och använd bilageidentifierarvärdet för att hämta det krypterade PDF-dokumentet.
1. Hämta ett `System.IO.Stream` objekt genom att hämta värdet för `Attachment` objektets `Stream` datamedlem.
1. Skapa en bytearray och skicka bytearrayen till `System.IO.Stream` objektets `Read` metod. Den här metoden fyller i bytearrayen med en dataström som representerar det krypterade PDF-dokumentet.
1. Skapa ett `System.IO.FileStream` objekt genom att anropa dess konstruktor och skicka ett strängvärde som representerar en plats för en PDF-fil. Det här objektet representerar det krypterade PDF-dokumentet.
1. Skapa ett `System.IO.BinaryWriter` objekt genom att anropa dess konstruktor och skicka `System.IO.FileStream` objektet.
1. Skriv bytearrayens innehåll till PDF-filen genom att anropa `System.IO.BinaryWriter` objektets `Write` metod och skicka bytearrayen.

### Skapa Java-proxyklasser för Apache-axel som använder DIME {#creating-apache-axis-java-proxy-classes-that-use-dime}

Du kan använda verktyget WSDL2Java på Apache-axeln för att konvertera en tjänst-WSDL till Java-proxyklasser så att du kan anropa tjänståtgärder. Med Apache Ant kan du generera axelbiblioteksfiler från en AEM Forms-tjänst-WSDL som gör att du kan anropa tjänsten. (Se [Skapa Java-proxyklasser med hjälp av Apache-axeln](#creating-java-proxy-classes-using-apache-axis).)

Verktyget Apache Axel WSDL2Java genererar JAVA-filer som innehåller metoder som används för att skicka SOAP-begäranden till en tjänst. SOAP-begäranden som tas emot av en tjänst avkodas av de axelgenererade biblioteken och återställs till metoder och argument.

Så här anropar du `MyApplication/EncryptDocument` tjänsten (som skapades i Workbench) med axelgenererade biblioteksfiler och DIME:

1. Skapa Java-proxyklasser som använder tjänsten `MyApplication/EncryptDocument` WSDL med Apache Axis. (Se [Skapa Java-proxyklasser med hjälp av Apache-axeln](#creating-java-proxy-classes-using-apache-axis).)
1. Inkludera Java-proxyklasserna i klassökvägen.
1. Skapa ett `MyApplicationEncryptDocumentServiceLocator` objekt med hjälp av dess konstruktor.
1. Skapa ett `URL` objekt med hjälp av konstruktorn och skicka ett strängvärde som anger WSDL-definitionen för tjänsten AEM Forms. Kontrollera att du anger `?blob=dime` i slutet av SOAP-slutpunkts-URL:en. Använd till exempel

   ```as3
    https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?blob=dime.
   ```

1. Skapa ett `EncryptDocumentSoapBindingStub` objekt genom att anropa dess konstruktor och skicka `MyApplicationEncryptDocumentServiceLocator`objektet och `URL` objektet.
1. Ange användarnamnet och lösenordet för AEM-formulären genom att anropa `EncryptDocumentSoapBindingStub` objektets `setUsername` - och `setPassword` -metoder.

   ```as3
    encryptionClientStub.setUsername("administrator");
    encryptionClientStub.setPassword("password");
   ```

1. Hämta PDF-dokumentet som ska skickas till `MyApplication/EncryptDocument` tjänsten genom att skapa ett `java.io.File` objekt. Skicka ett strängvärde som anger PDF-dokumentets plats.
1. Skapa ett `javax.activation.DataHandler` objekt med hjälp av dess konstruktor och skicka ett `javax.activation.FileDataSource` objekt. Objektet kan `javax.activation.FileDataSource` skapas med hjälp av konstruktorn och genom att skicka det objekt som `java.io.File` representerar PDF-dokumentet.
1. Skapa ett `org.apache.axis.attachments.AttachmentPart` objekt med hjälp av dess konstruktor och skicka `javax.activation.DataHandler` objektet.
1. Bifoga den bifogade filen genom att anropa `EncryptDocumentSoapBindingStub` objektets `addAttachment` metod och skicka `org.apache.axis.attachments.AttachmentPart` objektet.
1. Skapa ett `BLOB` objekt med hjälp av dess konstruktor. Fyll i `BLOB` objektet med värdet för bilageidentifieraren genom att anropa `BLOB` objektets `setAttachmentID` -metod och skicka värdet för bilageidentifieraren. Det här värdet kan du få genom att anropa `org.apache.axis.attachments.AttachmentPart` objektets `getContentId` metod.
1. Anropa `MyApplication/EncryptDocument` processen genom att anropa `EncryptDocumentSoapBindingStub` objektets `invoke` metod. Skicka det `BLOB` objekt som innehåller DIME-bilagan. Den här processen returnerar ett krypterat PDF-dokument i ett `BLOB` objekt.
1. Hämta identifierarvärdet för den bifogade filen genom att anropa det returnerade `BLOB` objektets `getAttachmentID` metod. Den här metoden returnerar ett strängvärde som representerar identifierarvärdet för den returnerade bifogade filen.
1. Hämta de bifogade filerna genom att anropa `EncryptDocumentSoapBindingStub` objektets `getAttachments` metod. Den här metoden returnerar en array med `Objects` som representerar de bifogade filerna.
1. Iterera genom de bifogade filerna ( `Object` arrayen) och använd bilageidentifierarvärdet för att få fram det krypterade PDF-dokumentet. Varje element är ett `org.apache.axis.attachments.AttachmentPart` objekt.
1. Hämta objektet som är kopplat till den bifogade filen genom att anropa `javax.activation.DataHandler` objektets `org.apache.axis.attachments.AttachmentPart` `getDataHandler` metod.
1. Hämta ett `java.io.FileStream` objekt genom att anropa `javax.activation.DataHandler` objektets `getInputStream` metod.
1. Skapa en bytearray och skicka bytearrayen till `java.io.FileStream` objektets `read` metod. Den här metoden fyller i bytearrayen med en dataström som representerar det krypterade PDF-dokumentet.
1. Skapa ett `java.io.File` objekt med hjälp av dess konstruktor. Det här objektet representerar det krypterade PDF-dokumentet.
1. Skapa ett `java.io.FileOutputStream` objekt med hjälp av dess konstruktor och skicka `java.io.File` objektet.
1. Anropa `java.io.FileOutputStream` objektets `write` metod och skicka bytearrayen som innehåller dataströmmen som representerar det krypterade PDF-dokumentet.

**Se även**

[Snabbstart: Anropa en tjänst med DIME i ett Java-projekt](/help/forms/developing/invocation-api-quick-starts.md#quick-start-invoking-a-service-using-dime-in-a-java-project)

## Använda SAML-baserad autentisering {#using-saml-based-authentication}

AEM Forms stöder olika autentiseringslägen för webbtjänster vid anrop av tjänster. Ett autentiseringsläge anger både ett användarnamn och ett lösenordsvärde med hjälp av en grundläggande auktoriseringshuvud i webbtjänstanropet. AEM Forms stöder även SAML-baserad autentisering. När ett klientprogram anropar en AEM Forms-tjänst med hjälp av en webbtjänst kan klientprogrammet tillhandahålla autentiseringsinformation på något av följande sätt:

* Skicka inloggningsuppgifter som en del av den grundläggande auktoriseringen
* Skickar användarnamntoken som en del av WS-Security-huvudet
* Skicka en SAML-försäkran som en del av WS-Security-huvudet
* Kerberos-token skickas som en del av WS-Security-huvudet

AEM Forms stöder inte standardcertifikatbaserad autentisering, men den stöder certifikatbaserad autentisering i en annan form.

>[!NOTE]
>
>Webbtjänstens snabbstart i Programmering med AEM Forms anger användarnamn och lösenord för att utföra auktoriseringen.

Identiteten för AEM-formuläranvändare kan representeras genom en SAML-försäkran som signerats med en hemlig nyckel. Följande XML-kod visar ett exempel på en SAML-försäkran.

```as3
 <Assertion xmlns="urn:oasis:names:tc:SAML:1.0:assertion"
     xmlns:saml="urn:oasis:names:tc:SAML:1.0:assertion"
     xmlns:samlp="urn:oasis:names:tc:SAML:1.0:protocol"
     AssertionID="fd4bd0c87302780e0d9bbfa8726d5bc0" IssueInstant="2008-04-17T13:47:00.720Z" Issuer="LiveCycle"
     MajorVersion="1" MinorVersion="1">
     <Conditions NotBefore="2008-04-17T13:47:00.720Z" NotOnOrAfter="2008-04-17T15:47:00.720Z">
     </Conditions>
     <AuthenticationStatement
         AuthenticationInstant="2008-04-17T13:47:00.720Z"
         AuthenticationMethod="urn:oasis:names:tc:SAML:1.0:am:unspecified">
         <Subject>
             <NameIdentifier NameQualifier="DefaultDom">administrator</NameIdentifier>
             <SubjectConfirmation>
                 <ConfirmationMethod>urn:oasis:names:tc:SAML:1.0:cm:sender-vouches</ConfirmationMethod>
             </SubjectConfirmation>
         </Subject>
     </AuthenticationStatement>
     <ds:Signature >
         <ds:SignedInfo>
             <ds:CanonicalizationMethod Algorithm="https://www.w3.org/2001/10/xml-exc-c14n#"></ds:CanonicalizationMethod>
             <ds:SignatureMethod    Algorithm="https://www.w3.org/2000/09/xmldsig#hmac-sha1"></ds:SignatureMethod>
             <ds:Reference URI="#fd4bd0c87302780e0d9bbfa8726d5bc0">
                 <ds:Transforms>
                     <ds:Transform Algorithm="https://www.w3.org/2000/09/xmldsig#enveloped-signature"></ds:Transform>
                     <ds:Transform Algorithm="https://www.w3.org/2001/10/xml-exc-c14n#">
                         <ec:InclusiveNamespaces
                             PrefixList="code ds kind rw saml samlp typens #default">
                         </ec:InclusiveNamespaces>
                     </ds:Transform>
                 </ds:Transforms>
                 <ds:DigestMethod Algorithm="https://www.w3.org/2000/09/xmldsig#sha1"></ds:DigestMethod>
                 <ds:DigestValue>hVrtqjWr+VzaVUIpQx0YI9lIjaY=</ds:DigestValue>
             </ds:Reference>
         </ds:SignedInfo>
         <ds:SignatureValue>UMbBb+cUcPtcWDCIhXes4n4FxfU=</ds:SignatureValue>
     </ds:Signature>
 </Assertion>
```

Det här exempelbekräftelsen utfärdas för en administratörsanvändare. Påståendet innehåller följande märkbara objekt:

* Den gäller under en viss tid.
* Det utfärdas för en viss användare.
* Det är digitalt signerat. Alla ändringar som görs i det skulle alltså bryta signaturen.
* Den kan presenteras för AEM Forms som en token för användarens identitet som liknar användarnamnet och lösenordet.

Ett klientprogram kan hämta försäkran från alla AEM Forms AuthenticationManager-API:er som returnerar ett `AuthResult` objekt. Du kan hämta en `AuthResult` instans genom att utföra någon av följande två metoder:

* Autentisera användaren med någon av de autentiseringsmetoder som används av AuthenticationManager API. Normalt används användarnamnet och lösenordet; Du kan även använda certifikatautentisering.
* Använda `AuthenticationManager.getAuthResultOnBehalfOfUser` metoden. Med den här metoden kan ett klientprogram hämta ett `AuthResult` objekt för alla AEM-formuläranvändare.

en AEM-formuläranvändare kan autentiseras med en SAML-token som erhålls. Denna SAML-försäkran (xml-fragment) kan skickas som en del av WS-Security-huvudet med webbtjänstanropet för användarautentisering. Vanligtvis har ett klientprogram autentiserat en användare men inte lagrat inloggningsuppgifterna. (Eller så har användaren loggat in på klienten via en annan mekanism än att använda ett användarnamn och lösenord.) I den här situationen måste klientprogrammet anropa AEM Forms och personifiera en specifik användare som får anropa AEM Forms.

Anropa metoden med en webbtjänst om du vill personifiera en viss användare `AuthenticationManager.getAuthResultOnBehalfOfUser` . Den här metoden returnerar en `AuthResult` instans som innehåller SAML-försäkran för den användaren.

Använd sedan SAML-försäkran för att anropa alla tjänster som kräver autentisering. Den här åtgärden innebär att försäkran skickas som en del av SOAP-huvudet. När ett webbtjänstanrop görs med denna försäkran identifierar AEM Forms användaren som den som representeras av försäkran. Användaren som anges i försäkran är alltså den användare som anropar tjänsten.

### Använda Apache-axelklasser och SAML-baserad autentisering {#using-apache-axis-classes-and-saml-based-authentication}

Du kan anropa en AEM Forms-tjänst av Java-proxyklasser som har skapats med axelbiblioteket. (Se [Skapa Java-proxyklasser med hjälp av Apache-axeln](#creating-java-proxy-classes-using-apache-axis).)

När du använder AXIS som använder SAML-baserad autentisering registrerar du hanteraren för begäran och svar med Axel. Hanteraren anropas av Apache-axeln innan en anropsbegäran skickas till AEM Forms. Om du vill registrera en hanterare skapar du en Java-klass som utökas `org.apache.axis.handlers.BasicHandler`.

**Skapa en AssertionHandler med axel**

Följande Java-klass, med namnet `AssertionHandler.java`, visar ett exempel på en Java-klass som utökas `org.apache.axis.handlers.BasicHandler`.

```as3
 public class AssertionHandler extends BasicHandler {
        public void invoke(MessageContext ctx) throws AxisFault {
            String assertion = (String) ctx.getProperty(LC_ASSERTION);
 
            //no assertion hence nothing to insert
            if(assertion == null) return;
 
            try {
                MessageElement samlElement = new MessageElement(convertToXML(assertion));
                SOAPHeader header = (SOAPHeader) ctx.getRequestMessage().getSOAPHeader();
                //Create the wsse:Security element which would contain the SAML element
                SOAPElement wsseHeader = header.addChildElement("Security", "wsse", WSSE_NS);
                wsseHeader.appendChild(samlElement);
                //remove the actor attribute as in LC we do not specify any actor. This would not remove the actor attribute though
                //it would only remove it from the soapenv namespace
                wsseHeader.getAttributes().removeNamedItem("actor");
            } catch (SOAPException e) {
                throw new AxisFault("Error occured while adding the assertion to the SOAP Header",e);
            }
        }
 }
```

**Registrera hanteraren**

Om du vill registrera en hanterare med Axel skapar du en client-config.wsdd-fil. Axeln söker som standard efter en fil med det här namnet. Följande XML-kod är ett exempel på en client-config.wsdd-fil. Mer information finns i Axeldokumentationen.

```as3
 <deployment xmlns="https://xml.apache.org/axis/wsdd/" xmlns:java="https://xml.apache.org/axis/wsdd/providers/java">
     <transport name="http" pivot="java:org.apache.axis.transport.http.HTTPSender"/>
      <globalConfiguration >
       <requestFlow >
        <handler type="java:com.adobe.idp.um.example.AssertionHandler" />
       </requestFlow >
      </globalConfiguration >
 </deployment>
 
```

**Anropa en AEM Forms-tjänst**

I följande kodexempel anropas en AEM Forms-tjänst med SAML-baserad autentisering.

```as3
 public class ImpersonationExample {
        . . .
        public void  authenticateOnBehalf(String superUsername,String password,
                String canonicalName,String domainName) throws UMException, RemoteException{
            ((org.apache.axis.client.Stub) authenticationManager).setUsername(superUsername);
            ((org.apache.axis.client.Stub) authenticationManager).setPassword(password);
 
            //Step 1 - Invoke the Auth manager api to get an assertion for the user to be impersonated
            AuthResult ar = authenticationManager.getAuthResultOnBehalfOfUser(canonicalName, domainName, null);
            String assertion = ar.getAssertion();
            //Step 2 - Setting the assertion here to be picked later by the AssertionHandler. Note that stubs are not threadSafe
            //hence should not be reused. For this simple example we have made them instance variable but care should be taken
            //regarding the thread safety
            ((javax.xml.rpc.Stub) authorizationManager)._setProperty(AssertionHandler.LC_ASSERTION, assertion);
        }
 
        public Role findRole(String roleId) throws UMException, RemoteException{
            //This api would be invoked under bob's user rights
            return authorizationManager.findRole(roleId);
        }
 
        public static void main(String[] args) throws Exception {
            ImpersonationExample ie = new ImpersonationExample("http://localhost:5555");
            //Get the SAML assertion for the user to impersonate and store it in stub
            ie.authenticateOnBehalf(
                    "administrator", //The Super user which has the required impersonation permission
                    "password", // Password of the super user as referred above
                    "bob", //Cannonical name of the user to impersonate
                    "testdomain" //Domain of the user to impersonate
                    );
 
            Role r = ie.findRole("BASIC_ROLE_ADMINISTRATOR");
            System.out.println("Role "+r.getName());
        }
 }
```

### Använda en .NET-klientsammansättning och SAML-baserad autentisering {#using-a-net-client-assembly-and-saml-based-authentication}

Du kan anropa en Forms-tjänst genom att använda en .NET-klientsammansättning och SAML-baserad autentisering. För att göra det måste du använda Web Service Enhancements 3.0 (WSE). Mer information om hur du skapar en .NET-klientsammansättning som använder WSE finns i [Skapa ett .NET-projekt som använder DIME](#creating-a-net-project-that-uses-dime).

>[!NOTE]
>
>DIME-avsnittet använder WSE 2.0. Om du vill använda SAML-baserad autentisering följer du de instruktioner som anges i DIME-avsnittet. Ersätt emellertid WSE 2.0 med WSE 3.0. Installera Web Services Enhancements 3.0 på utvecklingsdatorn och integrera den med Microsoft Visual Studio .NET. Du kan hämta webbtjänsttillägg 3.0 från [Microsoft Download Center](https://www.microsoft.com/downloads/search.aspx).

WSE-arkitekturen använder datatyperna Policies, Assertions och SecurityToken. För ett webbtjänstanrop anger du kort en princip. En princip kan ha flera försäkringar. Varje försäkran kan innehålla filter. Ett filter anropas i vissa steg i ett webbtjänstanrop och kan då ändra SOAP-begäran. Mer information finns i dokumentationen till Web Service Enhancements 3.0.

**Skapa försäkran och filter**

I följande exempel på C#-kod skapas filter- och kontrollklasser. I det här kodexemplet skapas ett SamlAssertionOutputFilter. Det här filtret anropas av WSE-ramverket innan SOAP-begäran skickas till AEM Forms.

```as3
 class LCSamlPolicyAssertion : Microsoft.Web.ServicES4.Design.PolicyAssertion
 {
        public override Microsoft.Web.ServicES4.SoapFilter CreateClientOutputFilter(FilterCreationContext context)
        {
           return new SamlAssertionOutputFilter();
        }
        . . .
 }
 
 
 class SamlAssertionOutputFilter : SendSecurityFilter
 {
        public override void SecureMessage(SoapEnvelope envelope, Security security)
        {
           // Get the SamlToken from the SessionState
           SamlToken samlToken = envelope.Context.Credentials.UltimateReceiver.GetClientToken<SamlToken>();
           security.Tokens.Add(samlToken);
        }
 }
```

**Skapa SAML-token**

Skapa en klass som representerar SAML-försäkran. Huvuduppgiften som den här klassen utför är att konvertera datavärden från sträng till xml och bevara tomt utrymme. Denna XML för försäkran importeras senare till SOAP-begäran.

```as3
 class SamlToken : SecurityToken
 {
        public const string SAMLAssertion = "https://docs.oasis-open.org/wss/oasis-wss-saml-token-profile-1.1#SAMLV1.1";
        private XmlElement _assertionElement;
 
        public SamlToken(string assertion)
             : base(SAMLAssertion)
        {
           XmlDocument xmlDoc = new XmlDocument();
           //The white space has to be preserved else the digital signature would get broken
           xmlDoc.PreserveWhitespace = true;
           xmlDoc.LoadXml(assertion);
           _assertionElement = xmlDoc.DocumentElement;
         }
 
         public override XmlElement GetXml(XmlDocument document)
         {
            return (XmlElement)document.ImportNode(_assertionElement, true);
         }
        . . .
 }
```

**Anropa en AEM Forms-tjänst**

Följande exempel på C#-kod anropar en Forms-tjänst med SAML-baserad autentisering.

```as3
 public class ImpersonationExample
 {
        . . .
        public void AuthenticateOnBehalf(string superUsername, string password, string canonicalName, string domainName)
        {
            //Create a policy for UsernamePassword Token
            Policy usernamePasswordPolicy = new Policy();
            usernamePasswordPolicy.Assertions.Add(new UsernameOverTransportAssertion());
 
            UsernameToken token = new UsernameToken(superUsername, password, PasswordOption.SendPlainText);
            authenticationManager.SetClientCredential(token);
            authenticationManager.SetPolicy(usernamePasswordPolicy);
 
            //Get the SAML assertion for impersonated user
            AuthClient.AuthenticationManagerService.AuthResult ar
                = authenticationManager.getAuthResultOnBehalfOfUser(canonicalName, domainName, null);
            System.Console.WriteLine("Received assertion " + ar.assertion);
 
            //Create a policy for inserting SAML assertion
            Policy samlPolicy = new Policy();
            samlPolicy.Assertions.Add(new LCSamlPolicyAssertion());
            authorizationManager.SetPolicy(samlPolicy);
            //Set the SAML assertion obtained previously as the token
            authorizationManager.SetClientCredential(new SamlToken(ar.assertion));
        }
 
        public Role findRole(string roleId)
        {
            return authorizationManager.findRole(roleId);
        }
 
        static void Main(string[] args)
        {
            ImpersonationExample ie = new ImpersonationExample("http://localhost:5555");
            ie.AuthenticateOnBehalf(
                 "administrator", //The Super user which has the required impersonation permission
                 "password", // Password of the super user as referred above
                 "bob", //Cannonical name of the user to impersonate
                 "testdomain" //Domain of the user to impersonate
                 );
 
         Role r = ie.findRole("BASIC_ROLE_ADMINISTRATOR");
            System.Console.WriteLine("Role "+r.name);
     }
 }
```

## Relaterade överväganden när du använder webbtjänster {#related-considerations-when-using-web-services}

Ibland uppstår problem när vissa AEM Forms-tjänster anropas med hjälp av webbtjänster. Syftet med denna diskussion är att identifiera dessa problem och tillhandahålla en lösning, om en sådan finns tillgänglig.

### Anropa tjänståtgärder asynkront {#invoking-service-operations-asynchronously}

Om du försöker anropa en AEM Forms-tjänståtgärd asynkront, till exempel `htmlToPDF` åtgärden Generera PDF, `SoapFaultException` inträffar en. Du löser det här problemet genom att skapa en XML-fil med anpassad bindning som mappar elementet och andra element till olika klasser `ExportPDF_Result` . Följande XML representerar en anpassad bindningsfil.

```as3
 <bindings
        xmlns:xsd="https://www.w3.org/2001/XMLSchema"
        xmlns:jxb="https://java.sun.com/xml/ns/jaxb" jxb:version="1.0"
        xmlns:wsdl="https://schemas.xmlsoap.org/wsdl/"
      wsdlLocation="http://localhost:8080/soap/services/GeneratePDFService?wsdl&async=true&lc_version=9.0.0"
        xmlns="https://java.sun.com/xml/ns/jaxws">
        <enableAsyncMapping>false</enableAsyncMapping>
        <package name="external_customize.client"/>
        <enableWrapperStyle>true</enableWrapperStyle>
        <bindings node="/wsdl:definitions/wsdl:types/xsd:schema[@targetNamespace='https://adobe.com/idp/services']/xsd:element[@name='ExportPDF_Result']">
            <jxb:class name="ExportPDFAsyncResult">
            </jxb:class>
        </bindings>
        <bindings node="/wsdl:definitions/wsdl:types/xsd:schema[@targetNamespace='https://adobe.com/idp/services']/xsd:element[@name='CreatePDF_Result']">
            <jxb:class name="CreatePDFAsyncResult">
            </jxb:class>
        </bindings>
        <bindings node="/wsdl:definitions/wsdl:types/xsd:schema[@targetNamespace='https://adobe.com/idp/services']/xsd:element[@name='HtmlToPDF_Result']">
            <jxb:class name="HtmlToPDFAsyncResult">
            </jxb:class>
        </bindings>
        <bindings node="/wsdl:definitions/wsdl:types/xsd:schema[@targetNamespace='https://adobe.com/idp/services']/xsd:element[@name='OptimizePDF_Result']">
            <jxb:class name="OptimizePDFAsyncResult">
            </jxb:class>
        </bindings>
        <!--bindings node="//wsdl:portType[@name='GeneratePDFService']/wsdl:operation[@name='HtmlToPDF_Result']">
            <jxb:class name="HtmlToPDFAsyncResult"/>
        </bindings-->
 </bindings>
```

Använd den här XML-filen när du skapar Java-proxyfiler med JAX-WS. (Se [Skapa Java-proxyklasser med JAX-WS](#creating-java-proxy-classes-using-jax-ws).)

Referera den här XML-filen när du kör JAX-WS-verktyget (wsimport.exe) med hjälp av kommandoradsalternativet - `b` . Uppdatera elementet `wsdlLocation` i XML-bindningsfilen för att ange URL:en för AEM Forms.

Om du vill vara säker på att asynkrona anrop fungerar ändrar du slutpunktens URL-värde och anger `async=true`. För Java-proxyfiler som skapas med JAX-WS anger du till exempel följande för `BindingProvider.ENDPOINT_ADDRESS_PROPERTY`.

`https://server:port/soap/services/ServiceName?wsdl&async=true&lc_version=9.0.0`

I följande lista anges andra tjänster som behöver en anpassad bindningsfil när den anropas asynkront:

* PDFG3D
* Aktivitetshanteraren
* Application Manager
* Kataloghanteraren
* Distiller
* Rights Management
* Dokumenthantering

### Skillnader i J2EE-servrar {#differences-in-j2ee-application-servers}

Ibland kan ett proxybibliotek som skapats med en specifik J2EE-programserver inte anropa AEM Forms som finns på en annan J2EE-programserver. Överväg ett proxybibliotek som genereras med AEM Forms som distribueras på WebSphere. Proxybiblioteket kan inte anropa AEM Forms-tjänster som är distribuerade på JBoss Application Server.

Vissa avancerade datatyper i AEM Forms, till exempel `PrincipalReference`, definieras annorlunda när AEM Forms distribueras på WebSphere jämfört med JBoss Application Server. Skillnader i de JDK:er som används av de olika J2EE-programtjänsterna är orsaken till varför det finns skillnader i WSDL-definitioner. Använd därför proxybibliotek som genereras från samma J2EE-programserver.

### Åtkomst av flera tjänster via webbtjänster {#accessing-multiple-services-using-web-services}

På grund av namnområdeskonflikter kan dataobjekt inte delas mellan flera tjänst-WSDL:er. Olika tjänster kan dela datatyper och därför delar tjänsterna definitionen av dessa typer i WSDL:erna. Du kan till exempel inte lägga till två .NET-klientsammansättningar som innehåller en datatyp till samma .NET-klientprojekt `BLOB` . Om du försöker göra det inträffar ett kompileringsfel.

I följande lista anges datatyper som inte kan delas mellan flera tjänst-WSDL:er:

* `User`
* `Principals`
* `PrincipalReference`
* `Groups`
* `Roles`
* `BLOB`

Du bör kvalificera datatyperna fullständigt för att undvika det här problemet. Ta till exempel ett .NET-program som refererar både till Forms-tjänsten och signaturtjänsten med hjälp av en tjänstreferens. Båda tjänstreferenserna innehåller en `BLOB` klass. Om du vill använda en `BLOB` instans kvalificerar du objektet fullständigt när du deklarerar det `BLOB` . Den här metoden visas i följande kodexempel. Mer information om det här kodexemplet finns i [Digitalt signera interaktiva formulär](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-interactive-forms).

Följande exempel på C#-kod signerar ett interaktivt formulär som återges av Forms-tjänsten. Klientprogrammet har två tjänstreferenser. Den instans `BLOB` som är associerad med Forms-tjänsten tillhör `SignInteractiveForm.ServiceReference2` namnutrymmet. På samma sätt tillhör den `BLOB` instans som är associerad med signaturtjänsten `SignInteractiveForm.ServiceReference1` namnutrymmet. Det signerade interaktiva formuläret sparas som en PDF-fil med namnet *LoanXFASigned.pdf*.

```as3
 ???/**
     * Ensure that you create a .NET project that uses
     * MS Visual Studio 2008 and version 3.5 of the .NET
     * framework. This is required to invoke a
     * AEM Forms service using MTOM.
     *
     * For information, see "Invoking AEM Forms using MTOM" in Programming with AEM forms
     */
 using System;
 using System.Collections.Generic;
 using System.Linq;
 using System.Text;
 using System.ServiceModel;
 using System.IO;
 
 //A reference to the Signature service
 using SignInteractiveForm.ServiceReference1;
 
 //A reference to the Forms service
 using SignInteractiveForm.ServiceReference2;
 
 namespace SignInteractiveForm
 {
        class Program
        {
            static void Main(string[] args)
            {
                try
                {
                    //Because BLOB objects are used in both service references
                    //it is necessary to fully-qualify the BLOB objects
 
                    //Retrieve the form -- invoke the Forms service
                    SignInteractiveForm.ServiceReference2.BLOB formData = GetForm();
 
                    //Create a BLOB object associated with the Signature service
                    SignInteractiveForm.ServiceReference1.BLOB sigData = new SignInteractiveForm.ServiceReference1.BLOB();
 
                    //Transfer the byte stream from one Forms BLOB object to the
                    //Signature BLOB object
                    sigData.MTOM = formData.MTOM;
 
                    //Sign the Form -- invoke the Signature service
                    SignForm(sigData);
                }
                catch (Exception ee)
                {
                    Console.WriteLine(ee.Message);
                }
            }
 
            //Creates an interactive PDF form based on a XFA form - invoke the Forms service
            private static SignInteractiveForm.ServiceReference2.BLOB GetForm()
            {
 
                try
                {
                    //Create a FormsServiceClient object
                    FormsServiceClient formsClient = new FormsServiceClient();
                    formsClient.Endpoint.Address = new System.ServiceModel.EndpointAddress("https://hiro-xp:8080/soap/services/FormsService?blob=mtom");
 
                    //Enable BASIC HTTP authentication
                    BasicHttpBinding b = (BasicHttpBinding)formsClient.Endpoint.Binding;
                    b.MessageEncoding = WSMessageEncoding.Mtom;
                    formsClient.ClientCredentials.UserName.UserName = "administrator";
                    formsClient.ClientCredentials.UserName.Password = "password";
                    b.Security.Transport.ClientCredentialType = HttpClientCredentialType.Basic;
                    b.Security.Mode = BasicHttpSecurityMode.TransportCredentialOnly;
                    b.MaxReceivedMessageSize = 2000000;
                    b.MaxBufferSize = 2000000;
                    b.ReaderQuotas.MaxArrayLength = 2000000;
 
                    //Create a BLOB to store form data
                    SignInteractiveForm.ServiceReference2.BLOB formData = new SignInteractiveForm.ServiceReference2.BLOB();
                    SignInteractiveForm.ServiceReference2.BLOB pdfForm = new SignInteractiveForm.ServiceReference2.BLOB();
 
                    //Specify a XML form data
                    string path = "C:\\Adobe\Loan.xml";
                    FileStream fs = new FileStream(path, FileMode.Open);
 
                    //Get the length of the file stream
                    int len = (int)fs.Length;
                    byte[] ByteArray = new byte[len];
 
                    fs.Read(ByteArray, 0, len);
                    formData.MTOM = ByteArray;
 
                    //Specify a XML form data
                    string path2 = "C:\\Adobe\LoanSigXFA.pdf";
                    FileStream fs2 = new FileStream(path2, FileMode.Open);
 
                    //Get the length of the file stream
                    int len2 = (int)fs2.Length;
                    byte[] ByteArray2 = new byte[len2];
 
                    fs2.Read(ByteArray2, 0, len2);
                    pdfForm.MTOM = ByteArray2;
 
                    PDFFormRenderSpec renderSpec = new PDFFormRenderSpec();
                    renderSpec.generateServerAppearance = true;
 
                    //Set out parameter values
                    long pageCount = 1;
                    String localValue = "en_US";
                    FormsResult result = new FormsResult();
 
                    //Render an interactive PDF form
                    formsClient.renderPDFForm2(
                        pdfForm,
                        formData,
                        renderSpec,
                        null,
                        null,
                        out pageCount,
                        out localValue,
                        out result);
 
                    //Write the data stream to the BLOB object
                    SignInteractiveForm.ServiceReference2.BLOB outForm = result.outputContent;
                    return outForm;
                }
                catch (Exception ee)
                {
                    Console.WriteLine(ee.Message);
                }
                return null;
            }
 
            //Sign the form -- invoke the Signature service
            private static void SignForm(SignInteractiveForm.ServiceReference1.BLOB inDoc)
            {
 
                try
                {
                    //Create a SignatureServiceClient object
                    SignatureServiceClient signatureClient = new SignatureServiceClient();
                    signatureClient.Endpoint.Address = new System.ServiceModel.EndpointAddress("https://hiro-xp:8080/soap/services/SignatureService?blob=mtom");
 
                    //Enable BASIC HTTP authentication
                    BasicHttpBinding b = (BasicHttpBinding)signatureClient.Endpoint.Binding;
                    b.MessageEncoding = WSMessageEncoding.Mtom;
                    signatureClient.ClientCredentials.UserName.UserName = "administrator";
                    signatureClient.ClientCredentials.UserName.Password = "password";
                    b.Security.Transport.ClientCredentialType = HttpClientCredentialType.Basic;
                    b.Security.Mode = BasicHttpSecurityMode.TransportCredentialOnly;
                    b.MaxReceivedMessageSize = 2000000;
                    b.MaxBufferSize = 2000000;
                    b.ReaderQuotas.MaxArrayLength = 2000000;
 
                    //Specify the name of the signature field
                    string fieldName = "form1[0].grantApplication[0].page1[0].SignatureField1[0]";
 
                    //Create a Credential object
                    Credential myCred = new Credential();
                    myCred.alias = "secure";
 
                    //Specify the reason to sign the document
                    string reason = "The document was reviewed";
 
                    //Specify the location of the signer
                    string location = "New York HQ";
 
                    //Specify contact information
                    string contactInfo = "Tony Blue";
 
                    //Create a PDFSignatureAppearanceOptions object
                    //and show date information
                    PDFSignatureAppearanceOptionSpec appear = new PDFSignatureAppearanceOptionSpec();
                    appear.showDate = true;
 
                    //Sign the PDF document
                    SignInteractiveForm.ServiceReference1.BLOB signedDoc = signatureClient.sign(
                        inDoc,
                        fieldName,
                        myCred,
                        HashAlgorithm.SHA1,
                        reason,
                        location,
                        contactInfo,
                        appear,
                        true,
                        null,
                        null,
                        null);
 
                    //Populate a byte array with BLOB data that represents the signed form
                    byte[] outByteArray = signedDoc.MTOM;
 
                    //Save the signed PDF document
                    string fileName = "C:\\Adobe\LoanXFASigned.pdf";
                    FileStream fs2 = new FileStream(fileName, FileMode.OpenOrCreate);
 
                    //Create a BinaryWriter object
                    BinaryWriter w = new BinaryWriter(fs2);
                    w.Write(outByteArray);
                    w.Close();
                    fs2.Close();
                }
 
                catch (Exception ee)
                {
                    Console.WriteLine(ee.Message);
                }
            }
        }
 }
 
 
```

### Tjänster som börjar med bokstaven I skapar ogiltiga proxyfiler {#services-starting-with-the-letter-i-produce-invalid-proxy-files}

Namnet på vissa AEM Forms-genererade proxyklasser är felaktigt när Microsoft .Net 3.5 och WCF används. Problemet inträffar när proxyklasser skapas för IBMFilenetContentRepositoryConnector, IDPSchedulerService eller någon annan tjänst vars namn börjar med bokstaven I. Namnet på den genererade klienten i fallet IBMFileNetContentRepositoryConnector är till exempel `BMFileNetContentRepositoryConnectorClient`. Bokstaven I saknas i den genererade proxyklassen.

