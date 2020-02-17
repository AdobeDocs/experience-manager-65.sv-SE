---
title: Reader utöka skyddsskyddade PDF-dokument med hjälp av Portable Protection Library
seo-title: Reader utöka skyddsskyddade PDF-dokument med hjälp av Portable Protection Library
description: Reader-tillägg möjliggör interaktiva funktioner i Adobe PDF-dokument via Acrobat Reader. Du kan använda PPL (Portable Protection Library) för att utöka de DRM-skyddade PDF-dokumenten.
seo-description: Reader-tillägg möjliggör interaktiva funktioner i Adobe PDF-dokument via Acrobat Reader. Du kan använda PPL (Portable Protection Library) för att utöka de DRM-skyddade PDF-dokumenten.
uuid: 0da17641-d24c-43c2-b918-8b5abe1e5473
contentOwner: khsingh
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: document_services
discoiquuid: 83ca522e-d16e-4196-9aa7-84f85de8dee2
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Reader utöka skyddsskyddade PDF-dokument med hjälp av Portable Protection Library {#reader-extending-policy-protected-pdf-documents-using-portable-protection-library}

Du måste känna till begrepp som dokumentsäkerhet, lästillägg och Java Programming Language för att kunna utöka dokumentskyddet i PDF-dokument.

Du kan använda dokumentskydd för att begränsa åtkomsten till specifika PDF-dokument till endast behöriga användare. Du kan också bestämma hur en mottagare ska kunna använda ett skyddat dokument. Du kan till exempel ange om mottagarna ska kunna skriva ut, kopiera eller redigera text i ett dokument som skyddas av dokumentsäkerhetsregler. Mer information om dokumentsäkerhet finns [i Dokumentsäkerhet](/help/forms/using/admin-help/document-security.md).

Du kan använda Reader-tillägg för att aktivera interaktiva funktioner i Adobe PDF-dokument via Acrobat Reader. Dessa interaktiva funktioner som normalt bara är tillgängliga via Adobe Acrobat Professional och Standard. Mer information om de interaktiva funktioner som läsartillägg kan aktivera finns i [Adobe Experience Manager Forms DocAssurance-tjänsten](/help/forms/using/overview-aem-document-services.md)**.**

Du kan använda det portabla skyddsbiblioteket för att tillämpa skyddsprofiler på dokumentet utan att behöva skicka dokumentet via nätverket. Det är bara säkerhetsreferenser och skyddsprofiler som rör sig över nätverket. Det faktiska dokumentet lämnar aldrig klienten och skyddsprofiler tillämpas lokalt på klienten.

## Reader utöka dokumentsäkerhet, profilskyddade PDF-dokument {#reader-extending-document-security-policy-protected-pdf-documents}

Skyddade dokument är krypterade. Du kan inte använda standardAPI:er för läsartillägg för att tillämpa, ta bort och hämta användningsrättigheter för profilskyddade PDF-dokument. Endast tjänsten Reader Extensions i Portable Protection Library tillhandahåller API:er för att lägga in, ta bort och hämta användarrättigheter i säkerhetsskyddade PDF-dokument.

### Tjänsten Reader Extensions {#reader-extensions-service}

Tilläggstjänsten för läsare lägger till användarrättigheter i ett profilskyddat PDF-dokument och aktiverar funktioner som normalt inte är tillgängliga när ett PDF-dokument öppnas med Adobe Acrobat Reader. Den har även API:er för att ta bort och hämta användarrättigheter för ett policyskyddat dokument.

Reader Extensions-tjänsten stöder fullt ut PDF-dokument som är baserade på PDF-standard 1.6 och senare. Förutom Acrobat Reader behöver användare från tredje part inga ytterligare program eller plugin-program för att kunna använda profilskyddade PDF-dokument.

Du kan utföra följande uppgifter med tjänsten Reader Extensions:

* Lägg in användarrättigheter i profilskyddade PDF-dokument.
* Ta bort användningsrättigheterna för ett profilskyddat PDF-dokument.
* Hämta användningsbehörighet för profilskyddade PDF-dokument.

### Tillämpa användningsbehörighet på ett profilskyddat PDF-dokument {#apply-usage-rights-to-a-document-security-policy-protected-pdf-document}

Du kan använda `applyUsageRights`Java-API:t för att tillämpa användningsrättigheter på profilskyddade PDF-dokument. Användningsrättigheterna gäller funktioner som är tillgängliga som standard i Acrobat men inte i Adobe Reader, t.ex. möjligheten att lägga till kommentarer i ett formulär eller att fylla i formulärfält och spara formuläret. PDF-dokument som har användarrättigheter är aktiverade. En användare som öppnar ett rättighetsaktiverat dokument i Adobe Reader kan utföra åtgärder som är aktiverade för det specifika dokumentet.

**** Syntax: `InputStream applyUsageRights(InputStream inputFile, File certFile, String credentialPassword, UsageRights usageRights)`

<table>
 <tbody>
  <tr>
   <td><p><strong>Parameter</strong></p> </td>
   <td><p><strong>Beskrivning</strong></p> </td>
  </tr>
  <tr>
   <td><p>inputFile</p> </td>
   <td><p>Ange InputStream som representerar det PDF-dokument som användningsrättigheterna ska tillämpas på. Du kan använda skyddade dokument som skyddas av LiveCycle Rights Management eller AEM Forms.</p> </td>
  </tr>
  <tr>
   <td><p>certFile</p> </td>
   <td><p>Ange ett File-objekt som representerar en .jks-fil. .jks-filen är en nyckelfil. Det pekar på ett certifikat som ger användarrättigheter.</p> </td>
  </tr>
  <tr>
   <td><p>credentialPassword</p> </td>
   <td><p>Ange lösenordet för nyckelbehållaren. </p> </td>
  </tr>
  <tr>
   <td><p>usageRights</p> </td>
   <td><p>Anger ett objekt av typen <a href="https://help.adobe.com/en_US/livecycle/11.0/ProgramLC/javadoc/com/adobe/livecycle/readerextensions/client/UsageRights.html" target="_blank">UsageRights</a>. Objektet usageRights representerar individuella rättigheter som kan tillämpas på ett policyskyddat PDF-dokument.</p> </td>
  </tr>
 </tbody>
</table>

### Hämta användningsbehörighet för profilskyddade PDF-dokument.   {#retrieve-usage-rights-applied-to-a-policy-protected-pdf-document-nbsp}

Du kan använda `getDocumentUsageRights`Java-API:t för att hämta läsartilläggets användningsrättigheter som tillämpas på ett profilskyddat PDF-dokument. Genom att hämta information om användningsrättigheter kan du lära dig mer om de funktioner som läsartillägget har aktiverat för det profilskyddade PDF-dokumentet.

**** Syntax: `public GetUsageRightsResult getDocumentUsageRights(InputStream inDoc)`

<table>
 <tbody>
  <tr>
   <td><p><strong>Parameter</strong></p> </td>
   <td><p><strong>Beskrivning</strong></p> </td>
  </tr>
  <tr>
   <td><p>inDoc</p> </td>
   <td><p>Ange InputStream som representerar det PDF-dokument som användningsrättigheterna ska hämtas från. Du kan använda skyddade dokument som skyddas av LiveCycle Rights Management eller AEM Forms.</p> </td>
  </tr>
 </tbody>
</table>

#### Kodexempel {#code-sample}

```java
//Create a ServiceClientFactory instance
ServiceClientFactory factory = ServiceClientFactory.createInstance(connectionProps);
//Create a RightsManagementClient object
RightsManagementClient2 rmClient2= new RightsManagementClient2(factory);

String inputFileName = "C:\\Sample\\protected.pdf"; //Input file can be RM protected or unprotected pdf file
File certFile = new File("C:\\Sample\\cert.jks"); //RE certificate file
String password = "password"; //password for RE certificate
UsageRights usageRights = getUsageRights(true,true,false,false,true,true,false,false,false,false,true);

//RE rights to be applied on the file : FormFillIn, FormDataImportExport, SubmitStandalone, OnlineForms, DynamicFormField, DynamicFormPages, BarcodeDecoding, DigitalSignatures, Comments, CommentsOnline, EmbeddedFiles

InputStream inputFileStream = new FileInputStream(inputFileName);
InputStream output = rmClient2.getRightsManagementReaderExtensionService().applyUsageRights(inputFileStream, certFile, credentialPassword, rights);

String outputFileName = "C:\\Sample\\ReAdded.pdf";
//Save the PDF document
File myFile = new File(outputFileName);
FileOutputStream outputStream = new FileOutputStream(myFile);

int read = 0;
byte[] bytes = new byte[1024];

while ((read = output.read(bytes)) != -1) {

    outputStream.write(bytes, 0, read);
}

System.out.println("UsageRights applied successfully to the document. ”);
 outputStream.close();
inputFileStream.close();

//Get Usage Rights for the output pdf document
InputStream fileWithRe = new FileInputStream(myFile);

GetUsageRightsResult usageRights = rmClient2.getRightsManagementReaderExtensionService().getDocumentUsageRights(fileWithRe);

UsageRights rights = usageRights.getRights();
String right1 = rights1.toString();
System.out.println("RE rights for the file are :\n"+right1);
 fileWithRe.close();
```

### Ta bort användningsbehörighet för ett profilskyddat PDF-dokument {#remove-usage-rights-of-a-policy-protected-pdf-document}

Du kan använda `removeUsageRights`Java-API:t för att ta bort användningsrättigheter från ett policyskyddat dokument. Användningsrättigheter måste tas bort från ett profilskyddat PDF-dokument för att andra AEM Forms-åtgärder ska kunna utföras i dokumentet. Du måste till exempel signera (eller certifiera) ett PDF-dokument digitalt innan du anger användningsbehörighet. Om du vill utföra åtgärder på ett policyskyddat dokument måste du därför ta bort användningsbehörighet från PDF-dokumentet, utföra andra åtgärder, t.ex. signera dokumentet digitalt och sedan återanvända användningsbehörighet för dokumentet.

**** Syntax: `InputStream removeUsageRights(InputStream inputFile)`

<table>
 <tbody>
  <tr>
   <td><p><strong>Parameter</strong></p> </td>
   <td><p><strong>Beskrivning</strong></p> </td>
  </tr>
  <tr>
   <td><p> </p> <p>inputFile</p> </td>
   <td>Ange InputStream som representerar det PDF-dokument som användningsrättigheterna<br /> ska tas bort från. Du kan använda skyddade dokument som skyddas av LiveCycle Rights Management eller AEM Forms.</td>
  </tr>
 </tbody>
</table>

#### Kodexempel {#code-sample-1}

```java
//Create a ServiceClientFactory instance
ServiceClientFactory factory = ServiceClientFactory.createInstance(connectionProps);
//Create a RightsManagementClient object
RightsManagementClient2 rmClient2= new RightsManagementClient2(factory);

String inputFileName = "C:\\Sample\\fileWithRe.pdf"; //Input file can be RM protected or unprotected pdf file
InputStream inputFileStream = new FileInputStream(inputFileName);

InputStream fileStream = rmClient2.getRightsManagementReaderExtensionService().removeUsageRights(inputFileStream);

String outputFileName = "C:\\Sample\\ReRemoveded.pdf";
//Save the PDF document
File myFile = new File(outputFileName);
FileOutputStream outputStream = new FileOutputStream(myFile);

int read = 0;
byte[] bytes = new byte[1024];

while ((read = fileStream.read(bytes)) != -1) {

    outputStream.write(bytes, 0, read);
}
System.out.println("RE rights removed successfully from the document.”);
outputStream.close();
inputFileStream.close();
```

