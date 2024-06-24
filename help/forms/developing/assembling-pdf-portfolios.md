---
title: Samla PDF Portfolio
description: Sammanställ en PDF-portfolio och kombinera flera olika typer av dokument, t.ex. Word-filer, bildfiler och PDF-dokument. Du kan sätta ihop en PDF-portfölj med ett Java API och ett Web Service API.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: d2bd7c3e-4f75-4234-a7aa-ee8524430493
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Services
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '1815'
ht-degree: 0%

---

# Samla PDF Portfolio {#assembling-pdf-portfolios}

**Exempel och exempel i det här dokumentet är bara för AEM Forms i JEE-miljö.**

Du kan sätta ihop ett PDF Portfolio med Assembler Java och webbtjänstens API. En portfölj kan kombinera flera dokument av olika typer, inklusive ordfiler, bildfiler (till exempel en jpeg-fil) och PDF-dokument. Portföljens layout kan anges till olika format som *Stödraster med förhandsvisning*, *På en bild* layout eller jämn *Rotera*.

Följande bild är en skärmbild av en portfölj med *På en bild* stillayout.

![ap_ap_portfolio](assets/ap_ap_portfolio.png)

Att skapa en PDF Portfolio fungerar som ett papperslöst alternativ till att skicka en dokumentsamling. Med AEM Forms kan du skapa portföljer genom att anropa Assembler-tjänsten med ett strukturerat DDX-dokument. Följande DDX-dokument är ett exempel på ett DDX-dokument som skapar ett PDF-Portfolio.

```xml
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
     <PDF result="portfolio1.pdf">
         <Portfolio>
             <Navigator source="myNavigator">
                 <Resource name="navigator/image.xxx" source="myImage.png"/>
             </Navigator>
         </Portfolio>
         <PackageFiles source="dog1"  >
              <FieldData name="X">72</FieldData>
             <FieldData name="Y">72</FieldData>
             <File filename="saint_bernard.jpg" mimetype="image/jpeg"/>
         </PackageFiles>
         <PackageFiles source="dog2"  >
             <FieldData name="X">120</FieldData>
             <FieldData name="Y">216</FieldData>
             <File filename="greyhound.pdf"/>
         </PackageFiles>
     </PDF>
 </DDX>
```

DXX-dokumentet måste innehålla en `Portfolio` tagg med en kapslad `Navigator` -tagg. Lägg märke till taggen `<Resource name="navigator/image.xxx" source="myImage.png"/>` är bara nödvändigt om `myNavigator` är tilldelad som onImage-layoutnavigatorn: `AdobeOnImage.nav`. Med den här taggen kan Assembler-tjänsten välja den bild som ska användas som portföljbakgrund. Inkludera `PackageFiles` och `File` -taggar för att definiera den paketerade filens filnamn och MIME-typ.

>[!NOTE]
>
>Mer information om Assembler-tjänsten finns i [Tjänstreferens för AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Mer information om ett DX-dokument finns i [Assembler Service och DDX Reference](https://www.adobe.com/go/learn_aemforms_ddx_63).

## Sammanfattning av steg {#summary-of-steps}

Så här skapar du en Portfolio i PDF:

1. Inkludera projektfiler.
1. Skapa en PDF Assembler-klient.
1. Referera till ett befintligt DDX-dokument.
1. Referera till önskade dokument.
1. Ange körningsalternativ.
1. Sammanställ portföljen.
1. Spara den monterade portföljen.

**Inkludera projektfiler**

Inkludera nödvändiga filer i utvecklingsprojektet. Om du skapar ett klientprogram med Java, inkluderar du de JAR-filer som behövs. Om du använder webbtjänster måste du inkludera proxyfilerna.

Följande JAR-filer måste läggas till i projektets klasssökväg:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar (krävs om AEM Forms används i JBoss)
* jbossall-client.jar (krävs om AEM Forms används i JBoss)

**Skapa en PDF Assembler-klient**

Skapa en Assembler-tjänstklient innan du programmässigt utför en Assembler-åtgärd.

**Referera till ett befintligt DDX-dokument**

Ett DDX-dokument måste refereras till för att du ska kunna sätta ihop ett PDF Portfolio. Det här DDX-dokumentet måste innehålla `Portfolio`, `Navigator` och `PackageFiles` -element.

**Referera till de dokument som krävs**

Om du vill montera ett PDF Portfolio refererar du till alla filer som representerar de dokument som ska monteras. Skicka till exempel alla bildfiler som har angetts i DDX-dokumentet till Assembler-tjänsten. Observera att det finns referenser till dessa filer i det DDX-dokument som anges i det här avsnittet: *myImage.png* och *saint_bernard.jpg*.

När du sätter ihop en PDF Portfolio skickar du en NAV-fil (en navigatorfil) till Assembler-tjänsten. NAV-filen som du skickar till Assembler-tjänsten beror på vilken typ av PDF Portfolio som ska skapas. Om du till exempel vill skapa en *På en bild* skickar du filen AdobeOnImage.nav. Du kan hitta NAV-filer i följande mapp:

`<Install folder>\Acrobat 9.0\Acrobat\Navigators`

Kopiera NAV-filen från installationskatalogen för Acrobat 9 (eller senare). Placera NAV-filen på en plats där klientprogrammet kan komma åt den. Alla filer skickas till Assembler-tjänsten i ett Map-samlingsobjekt.

>[!NOTE]
>
>Snabbstarterna som är kopplade till Samling av PDF Portfolio använder AdobeOnImage.nav.

**Ange körningsalternativ**

Du kan ställa in körningsalternativ som styr beteendet för Assembler-tjänsten när den utför ett jobb. Du kan till exempel ange ett alternativ som instruerar Assembler-tjänsten att fortsätta bearbeta ett jobb om ett fel uppstår.

**Sammanställa portföljen**

Om du vill montera en PDF Portfolio anropar du `invokeDDX` operation. Assembler-tjänsten returnerar PDF Portfolio i ett samlingsobjekt.

**Spara den monterade portföljen**

PDF Portfolio returneras inom ett samlingsobjekt. Iterera genom samlingsobjektet och spara PDF Portfolio som en PDF-fil.

**Se även**

[Sammanställa en PDF Portfolio med Java API](#assemble-a-pdf-portfolio-using-the-java-api)

[Sammanställa en PDF Portfolio med hjälp av webbtjänstens API](#assemble-a-pdf-portfolio-using-the-web-service-api)

[Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Programmisk sammanställning av PDF-dokument](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Sammanställa en PDF Portfolio med Java API {#assemble-a-pdf-portfolio-using-the-java-api}

Sätt ihop ett PDF Portfolio med hjälp av Assembler Service API (Java):

1. Inkludera projektfiler.

   Inkludera JAR-klientfiler, som adobe-assembler-client.jar, i Java-projektets klassökväg.

1. Skapa en PDF Assembler-klient.

   * Skapa en `ServiceClientFactory` objekt som innehåller anslutningsegenskaper.
   * Skapa en `AssemblerServiceClient` genom att använda konstruktorn och skicka `ServiceClientFactory` -objekt.

1. Referera till ett befintligt DDX-dokument.

   * Skapa en `java.io.FileInputStream` -objekt som representerar DDX-dokumentet genom att använda dess konstruktor och skicka ett strängvärde som anger platsen för DDX-filen.
   * Skapa en `com.adobe.idp.Document` genom att använda konstruktorn och skicka `java.io.FileInputStream` -objekt.

1. Referera till önskade dokument.

   * Skapa en `java.util.Map` objekt som används för att lagra indatadokument i PDF genom att använda en `HashMap` konstruktor.
   * Skapa en `java.io.FileInputStream` genom att använda dess konstruktor. Skicka platsen för den NAV-fil som krävs (upprepa den här uppgiften för varje fil som krävs för att skapa en portfölj).
   * Skapa en `com.adobe.idp.Document` -objektet och skicka `java.io.FileInputStream` objekt som innehåller NAV-filen (upprepa den här uppgiften för varje fil som krävs för att skapa en portfölj).
   * Lägg till en post i `java.util.Map` genom att anropa dess `put` och skicka följande argument:

      * Ett strängvärde som representerar nyckelnamnet. Detta värde måste matcha värdet för källelementet som anges i DDX-dokumentet. (upprepa den här uppgiften för varje fil som krävs för att skapa en portfölj).
      * A `com.adobe.idp.Document` -objekt som innehåller dokumentet PDF. (upprepa den här uppgiften för varje fil som krävs för att skapa en portfölj).

1. Ange körningsalternativ.

   * Skapa en `AssemblerOptionSpec` objekt som lagrar körningsalternativ med hjälp av dess konstruktor.
   * Ange körningsalternativ som uppfyller dina affärsbehov genom att anropa en metod som tillhör `AssemblerOptionSpec` -objekt. Om du till exempel vill instruera tjänsten Assembler att fortsätta bearbeta ett jobb när ett fel inträffar, ska du anropa `AssemblerOptionSpec` objektets `setFailOnError` metod och skicka `false`.

1. Sammanställ portföljen.

   Anropa `AssemblerServiceClient` objektets `invokeDDX` och skicka följande obligatoriska värden:

   * A `com.adobe.idp.Document` objekt som representerar det DDX-dokument som ska användas
   * A `java.util.Map` -objekt som innehåller de filer som krävs för att skapa en PDF Portfolio.
   * A `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` objekt som anger körningsalternativ, inklusive standardteckensnitt och jobbloggsnivå

   The `invokeDDX` returnerar en `com.adobe.livecycle.assembler.client.AssemblerResult` objekt som innehåller det monterade PDF Portfolio och eventuella undantag.

1. Spara den monterade portföljen.

   Utför följande åtgärder om du vill hämta PDF Portfolio:

   * Anropa `AssemblerResult` objektets `getDocuments` -metod. Den här metoden returnerar en `java.util.Map` -objekt.
   * Iterera genom `java.util.Map` tills du hittar resultatet `com.adobe.idp.Document` -objekt.
   * Anropa `com.adobe.idp.Document` objektets `copyToFile` metod för att extrahera PDF Portfolio.

**Se även**

[Snabbstart (SOAP läge): Samla in PDF Portfolio med Java API](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-pdf-portfolios-using-the-java-api)

[Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Sammanställa en PDF Portfolio med hjälp av webbtjänstens API {#assemble-a-pdf-portfolio-using-the-web-service-api}

Sätt ihop ett PDF Portfolio med Assembler Service API (webbtjänst):

1. Inkludera projektfiler.

   Skapa ett Microsoft .NET-projekt som använder MTOM. Kontrollera att du använder följande WSDL-definition när du anger en tjänstreferens: `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Ersätt `localhost` med IP-adressen till den server där AEM Forms finns.

1. Skapa en PDF Assembler-klient.

   * Skapa en `AssemblerServiceClient` genom att använda dess standardkonstruktor.
   * Skapa en `AssemblerServiceClient.Endpoint.Address` genom att använda `System.ServiceModel.EndpointAddress` konstruktor. Skicka ett strängvärde som anger WSDL till AEM Forms-tjänsten (till exempel `http://localhost:8080/soap/services/AssemblerService?blob=mtom`). Du behöver inte använda `lc_version` -attribut. Det här attributet används när du skapar en tjänstreferens.
   * Skapa en `System.ServiceModel.BasicHttpBinding` genom att hämta värdet för `AssemblerServiceClient.Endpoint.Binding` fält. Skicka returvärdet till `BasicHttpBinding`.
   * Ange `System.ServiceModel.BasicHttpBinding` objektets `MessageEncoding` fält till `WSMessageEncoding.Mtom`. Detta värde garanterar att MTOM används.
   * Aktivera grundläggande HTTP-autentisering genom att utföra följande åtgärder:

      * Tilldela AEM formuläranvändarnamn till fältet `AssemblerServiceClient.ClientCredentials.UserName.UserName`.
      * Tilldela motsvarande lösenordsvärde till fältet `AssemblerServiceClient.ClientCredentials.UserName.Password`.
      * Tilldela konstantvärdet `HttpClientCredentialType.Basic` till fältet `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Tilldela konstantvärdet `BasicHttpSecurityMode.TransportCredentialOnly` till fältet `BasicHttpBindingSecurity.Security.Mode`.

1. Referera till ett befintligt DDX-dokument.

   * Skapa en `BLOB` genom att använda dess konstruktor. The `BLOB` -objektet används för att lagra DDX-dokumentet.
   * Skapa en `System.IO.FileStream` genom att anropa dess konstruktor och skicka ett strängvärde som representerar filplatsen för DDX-dokumentet och läget som filen ska öppnas i.
   * Skapa en bytearray som lagrar innehållet i `System.IO.FileStream` -objekt. Du kan bestämma storleken på bytearrayen genom att hämta `System.IO.FileStream` objektets `Length` -egenskap.
   * Fylla i bytearrayen med strömdata genom att anropa `System.IO.FileStream` objektets `Read` -metod. Skicka bytearrayen, startpositionen och strömlängden som ska läsas.
   * Fyll i `BLOB` genom att tilldela `MTOM` med bytearrayens innehåll.

1. Referera till önskade dokument.

   * Skapa en `BLOB` genom att använda dess konstruktor. The `BLOB` -objektet används för att lagra indatafilen.
   * Skapa en `System.IO.FileStream` genom att anropa dess konstruktor och skicka ett strängvärde som representerar indatafilens filplats och det läge i vilket filen ska öppnas.
   * Skapa en bytearray som lagrar innehållet i `System.IO.FileStream` -objekt. Du kan bestämma storleken på bytearrayen genom att hämta `System.IO.FileStream` objektets `Length` -egenskap.
   * Fylla i bytearrayen med strömdata genom att anropa `System.IO.FileStream` objektets `Read` -metod. Skicka bytearrayen, startpositionen och strömlängden som ska läsas.
   * Fyll i `BLOB` genom att tilldela `MTOM` fält med bytearrayens innehåll.
   * Skapa en `MyMapOf_xsd_string_To_xsd_anyType` -objekt. Det här samlingsobjektet används för att lagra indatafiler som krävs för att skapa en PDF Portfolio.
   * Skapa en `MyMapOf_xsd_string_To_xsd_anyType_Item` -objekt.
   * Tilldela ett strängvärde som representerar nyckelnamnet till `MyMapOf_xsd_string_To_xsd_anyType_Item` objektets `key` fält. Detta värde måste matcha värdet för elementet som anges i DDX-dokumentet. (Utför den här åtgärden för varje indatafil.)
   * Tilldela `BLOB` det objekt som lagrar indatafilen till `MyMapOf_xsd_string_To_xsd_anyType_Item` objektets `value` fält. (Utför den här åtgärden för varje dokument i PDF.)
   * Lägg till `MyMapOf_xsd_string_To_xsd_anyType_Item` objekt till `MyMapOf_xsd_string_To_xsd_anyType` -objekt. Anropa `MyMapOf_xsd_string_To_xsd_anyType` objektets `Add` och skicka `MyMapOf_xsd_string_To_xsd_anyType` -objekt. (Utför den här åtgärden för varje dokument i PDF.)

1. Ange körningsalternativ.

   * Skapa en `AssemblerOptionSpec` objekt som lagrar körningsalternativ med hjälp av dess konstruktor.
   * Ange körningsalternativ som uppfyller dina affärskrav genom att tilldela ett värde till en datamedlem som tillhör `AssemblerOptionSpec` -objekt. Om du till exempel vill instruera Assembler-tjänsten att fortsätta bearbeta ett jobb när ett fel inträffar tilldelar du `false` till `AssemblerOptionSpec` objektets `failOnError` datamedlem.

1. Sammanställ portföljen.

   Anropa `AssemblerServiceClient` objektets `invokeDDX` och skicka följande värden:

   * A `BLOB` objekt som representerar DDX-dokumentet
   * The `MyMapOf_xsd_string_To_xsd_anyType` objekt som innehåller de nödvändiga filerna
   * An `AssemblerOptionSpec` objekt som anger körningsalternativ

   The `invokeDDX` returnerar en `AssemblerResult` som innehåller resultatet av jobbet och eventuella undantag som inträffade.

1. Spara den monterade portföljen.

   Utför följande åtgärder för att hämta nya PDF Portfolio:

   * Öppna `AssemblerResult` objektets `documents` fält, vilket är ett `Map` objekt som innehåller de resulterande PDF-dokumenten.
   * Iterera genom `Map` -objekt för att hämta varje resulterande dokument. Sedan måste du byta ut den arraymedlemmens `value` till `BLOB`.
   * Extrahera de binära data som representerar PDF-dokumentet genom att öppna dess `BLOB` objektets `MTOM` -egenskap. Detta returnerar en array med byte som du kan skriva ut till en PDF-fil.

**Se även**

[Anropa AEM Forms med MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Anropa AEM Forms med SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
