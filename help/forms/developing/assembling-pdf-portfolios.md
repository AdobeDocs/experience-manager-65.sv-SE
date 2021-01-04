---
title: Sammanställa PDF-Portfolio
seo-title: Sammanställa PDF-Portfolio
description: Sammanställ en PDF-portfolio och kombinera flera olika typer av dokument, t.ex. Word-filer, bildfiler och PDF-dokument. Du kan sätta ihop en PDF-portfölj med ett Java API och ett Web Service API.
seo-description: Sammanställ en PDF-portfolio och kombinera flera olika typer av dokument, t.ex. Word-filer, bildfiler och PDF-dokument. Du kan sätta ihop en PDF-portfölj med ett Java API och ett Web Service API.
uuid: 1778c90b-9d26-466b-a7c7-401d737395e0
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 023f0d9e-bfde-4879-a839-085fadffb48e
translation-type: tm+mt
source-git-commit: 07889ead2ae402b5fb738ca08c7efe076ef33e44
workflow-type: tm+mt
source-wordcount: '1851'
ht-degree: 0%

---


# Sammanställer PDF-Portfolio {#assembling-pdf-portfolios}

Du kan sätta ihop en PDF-Portfolio med Assembler Java och webbtjänstens API. En portfölj kan kombinera flera dokument av olika typer, inklusive ordfiler, bildfiler (till exempel en jpeg-fil) och PDF-dokument. Layouten för portföljen kan anges till olika format, t.ex. *stödrastret med Preview*, *På en bild*-layout eller till och med *Rotera*.

Följande bild är en skärmbild av en portfölj med *På en bildlayout*.

![ap_ap_portfolio](assets/ap_ap_portfolio.png)

Att skapa en PDF-Portfolio är ett papperslöst alternativ till att skicka en dokumentsamling. Med AEM Forms kan du skapa portföljer genom att anropa Assembler-tjänsten med ett strukturerat DDX-dokument. Följande DDX-dokument är ett exempel på ett DDX-dokument som skapar ett PDF-Portfolio.

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

DXX-dokumentet måste innehålla en `Portfolio`-tagg med en kapslad `Navigator`-tagg. Observera att taggen `<Resource name="navigator/image.xxx" source="myImage.png"/>` bara är nödvändig om `myNavigator` har tilldelats som onImage-layoutnavigator: `AdobeOnImage.nav`. Med den här taggen kan Assembler-tjänsten välja den bild som ska användas som portföljbakgrund. Inkludera `PackageFiles`- och `File`-taggar för att definiera den paketerade filens filnamn och MIME-typ.

>[!NOTE]
>
>Mer information om tjänsten Assembler finns i [Tjänstreferens för AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Mer information om ett DDX-dokument finns i [Assembler Service och DDX Reference](https://www.adobe.com/go/learn_aemforms_ddx_63).

## Sammanfattning av steg {#summary-of-steps}

Så här skapar du en PDF-Portfolio:

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

Det måste finnas en referens till ett DDX-dokument för att du ska kunna sätta ihop ett PDF-Portfolio. Det här DDX-dokumentet måste innehålla elementen `Portfolio`, `Navigator` och `PackageFiles`.

**Referera till önskade dokument**

Om du vill montera ett PDF-Portfolio refererar du till alla filer som representerar de dokument som ska monteras. Skicka till exempel alla bildfiler som har angetts i DDX-dokumentet till Assembler-tjänsten. Observera att det finns referenser till dessa filer i det DDX-dokument som anges i det här avsnittet: *myImage.png* och *saint_bernard.jpg*.

När du sammanställer en PDF-fil Portfolio skickar du en NAV-fil (en navigatorfil) till Assembler-tjänsten. NAV-filen som du skickar till Assembler-tjänsten beror på vilken typ av PDF-Portfolio som skapas. Om du till exempel vill skapa en *På en bild*-layout skickar du filen AdobeOnImage.nav. Du kan hitta NAV-filer i följande mapp:

`<Install folder>\Acrobat 9.0\Acrobat\Navigators`

Kopiera NAV-filen från installationskatalogen för Acrobat 9 (eller senare). Placera NAV-filen på en plats där klientprogrammet kan komma åt den. Alla filer skickas till Assembler-tjänsten i ett Map-samlingsobjekt.

>[!NOTE]
>
>Snabbstarterna som är kopplade till att sätta ihop PDF-Portfolio använder AdobeOnImage.nav.

**Ange körningsalternativ**

Du kan ställa in körningsalternativ som styr beteendet för Assembler-tjänsten när den utför ett jobb. Du kan till exempel ange ett alternativ som instruerar Assembler-tjänsten att fortsätta bearbeta ett jobb om ett fel uppstår.

**Sammanställa portföljen**

Om du vill montera en PDF-Portfolio anropar du åtgärden `invokeDDX`. Assembler-tjänsten returnerar PDF-Portfolio i ett samlingsobjekt.

**Spara den monterade portföljen**

En PDF-Portfolio returneras inom ett samlingsobjekt. Upprepa genom samlingsobjektet och spara PDF Portfolio som en PDF-fil.

**Se även**

[Sammanställa en PDF-Portfolio med Java API](#assemble-a-pdf-portfolio-using-the-java-api)

[Sammanställa en PDF-Portfolio med webbtjänstens API](#assemble-a-pdf-portfolio-using-the-web-service-api)

[Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Programmisk sammanställning av PDF-dokument](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Sammanställa en PDF-Portfolio med Java API {#assemble-a-pdf-portfolio-using-the-java-api}

Sammanställa en PDF-fil Portfolio med Assembler Service API (Java):

1. Inkludera projektfiler.

   Inkludera JAR-klientfiler, t.ex. adobe-assembler-client.jar, i Java-projektets klassökväg.

1. Skapa en PDF Assembler-klient.

   * Skapa ett `ServiceClientFactory`-objekt som innehåller anslutningsegenskaper.
   * Skapa ett `AssemblerServiceClient`-objekt med hjälp av dess konstruktor och skicka `ServiceClientFactory`-objektet.

1. Referera till ett befintligt DDX-dokument.

   * Skapa ett `java.io.FileInputStream`-objekt som representerar DDX-dokumentet genom att använda dess konstruktor och skicka ett strängvärde som anger platsen för DDX-filen.
   * Skapa ett `com.adobe.idp.Document`-objekt med hjälp av dess konstruktor och skicka `java.io.FileInputStream`-objektet.

1. Referera till önskade dokument.

   * Skapa ett `java.util.Map`-objekt som används för att lagra PDF-indatadokument med hjälp av en `HashMap`-konstruktor.
   * Skapa ett `java.io.FileInputStream`-objekt med hjälp av dess konstruktor. Skicka platsen för den NAV-fil som krävs (upprepa den här uppgiften för varje fil som krävs för att skapa en portfölj).
   * Skapa ett `com.adobe.idp.Document`-objekt och skicka `java.io.FileInputStream`-objektet som innehåller NAV-filen (upprepa den här uppgiften för varje fil som krävs för att skapa en portfölj).
   * Lägg till en post i `java.util.Map`-objektet genom att anropa dess `put`-metod och skicka följande argument:

      * Ett strängvärde som representerar nyckelnamnet. Detta värde måste matcha värdet för källelementet som anges i DDX-dokumentet. (upprepa den här uppgiften för varje fil som krävs för att skapa en portfölj).
      * Ett `com.adobe.idp.Document`-objekt som innehåller PDF-dokumentet. (upprepa den här uppgiften för varje fil som krävs för att skapa en portfölj).

1. Ange körningsalternativ.

   * Skapa ett `AssemblerOptionSpec`-objekt som lagrar körningsalternativ med hjälp av dess konstruktor.
   * Ange körningsalternativ som uppfyller dina affärskrav genom att anropa en metod som tillhör `AssemblerOptionSpec`-objektet. Om du till exempel vill instruera Assembler-tjänsten att fortsätta bearbeta ett jobb när ett fel inträffar, anropar du `AssemblerOptionSpec`-objektets `setFailOnError`-metod och skickar `false`.

1. Sammanställ portföljen.

   Anropa `AssemblerServiceClient`-objektets `invokeDDX`-metod och skicka följande obligatoriska värden:

   * Ett `com.adobe.idp.Document`-objekt som representerar det DDX-dokument som ska användas
   * Ett `java.util.Map`-objekt som innehåller de filer som krävs för att skapa en PDF-Portfolio.
   * Ett `com.adobe.livecycle.assembler.client.AssemblerOptionSpec`-objekt som anger körningsalternativen, inklusive standardteckensnittet och jobbloggsnivån

   Metoden `invokeDDX` returnerar ett `com.adobe.livecycle.assembler.client.AssemblerResult`-objekt som innehåller den sammansatta PDF-filen Portfolio och eventuella undantag.

1. Spara den monterade portföljen.

   Utför följande åtgärder för att hämta PDF-Portfolio:

   * Anropa `AssemblerResult`-objektets `getDocuments`-metod. Den här metoden returnerar ett `java.util.Map`-objekt.
   * Iterera genom `java.util.Map`-objektet tills du hittar det resulterande `com.adobe.idp.Document`-objektet.
   * Anropa `com.adobe.idp.Document`-objektets `copyToFile`-metod för att extrahera PDF-Portfolio.

**Se även**

[Snabbstart (SOAP-läge): Sammanställa PDF-Portfolio med Java API](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-pdf-portfolios-using-the-java-api)

[Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Sammanställa en PDF-Portfolio med webbtjänstens API {#assemble-a-pdf-portfolio-using-the-web-service-api}

Sammanställa en PDF-fil Portfolio med Assembler Service API (webbtjänst):

1. Inkludera projektfiler.

   Skapa ett Microsoft .NET-projekt som använder MTOM. Kontrollera att du använder följande WSDL-definition när du anger en tjänstreferens: `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Ersätt `localhost` med IP-adressen för servern som är värd för AEM Forms.

1. Skapa en PDF Assembler-klient.

   * Skapa ett `AssemblerServiceClient`-objekt med hjälp av dess standardkonstruktor.
   * Skapa ett `AssemblerServiceClient.Endpoint.Address`-objekt med konstruktorn `System.ServiceModel.EndpointAddress`. Skicka ett strängvärde som anger WSDL till AEM Forms-tjänsten (till exempel `http://localhost:8080/soap/services/AssemblerService?blob=mtom`). Du behöver inte använda attributet `lc_version`. Det här attributet används när du skapar en tjänstreferens.
   * Skapa ett `System.ServiceModel.BasicHttpBinding`-objekt genom att hämta värdet för fältet `AssemblerServiceClient.Endpoint.Binding`. Sänd returvärdet till `BasicHttpBinding`.
   * Ställ in `System.ServiceModel.BasicHttpBinding`-objektets `MessageEncoding`-fält till `WSMessageEncoding.Mtom`. Detta värde garanterar att MTOM används.
   * Aktivera grundläggande HTTP-autentisering genom att utföra följande åtgärder:

      * Tilldela användarnamnet för AEM formulär till fältet `AssemblerServiceClient.ClientCredentials.UserName.UserName`.
      * Tilldela motsvarande lösenordsvärde till fältet `AssemblerServiceClient.ClientCredentials.UserName.Password`.
      * Tilldela konstantvärdet `HttpClientCredentialType.Basic` till fältet `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Tilldela konstantvärdet `BasicHttpSecurityMode.TransportCredentialOnly` till fältet `BasicHttpBindingSecurity.Security.Mode`.

1. Referera till ett befintligt DDX-dokument.

   * Skapa ett `BLOB`-objekt med hjälp av dess konstruktor. Objektet `BLOB` används för att lagra DDX-dokumentet.
   * Skapa ett `System.IO.FileStream`-objekt genom att anropa dess konstruktor och skicka ett strängvärde som representerar platsen för DDX-dokumentet och läget som filen ska öppnas i.
   * Skapa en bytearray som lagrar innehållet i `System.IO.FileStream`-objektet. Du kan bestämma storleken på bytearrayen genom att hämta `System.IO.FileStream`-objektets `Length`-egenskap.
   * Fyll i bytearrayen med strömdata genom att anropa `System.IO.FileStream`-objektets `Read`-metod. Skicka bytearrayen, startpositionen och strömlängden som ska läsas.
   * Fyll i `BLOB`-objektet genom att tilldela dess `MTOM`-egenskap med innehållet i bytearrayen.

1. Referera till önskade dokument.

   * För varje indatafil skapar du ett `BLOB`-objekt med hjälp av dess konstruktor. Objektet `BLOB` används för att lagra indatafilen.
   * Skapa ett `System.IO.FileStream`-objekt genom att anropa dess konstruktor och skicka ett strängvärde som representerar indatafilens plats och läget som filen ska öppnas i.
   * Skapa en bytearray som lagrar innehållet i `System.IO.FileStream`-objektet. Du kan bestämma storleken på bytearrayen genom att hämta `System.IO.FileStream`-objektets `Length`-egenskap.
   * Fyll i bytearrayen med strömdata genom att anropa `System.IO.FileStream`-objektets `Read`-metod. Skicka bytearrayen, startpositionen och strömlängden som ska läsas.
   * Fyll i `BLOB`-objektet genom att tilldela dess `MTOM`-fält med innehållet i bytearrayen.
   * Skapa ett `MyMapOf_xsd_string_To_xsd_anyType`-objekt. Samlingsobjektet används för att lagra indatafiler som krävs för att skapa en PDF-Portfolio.
   * Skapa ett `MyMapOf_xsd_string_To_xsd_anyType_Item`-objekt för varje indatafil.
   * Tilldela ett strängvärde som representerar nyckelnamnet till `MyMapOf_xsd_string_To_xsd_anyType_Item`-objektets `key`-fält. Detta värde måste matcha värdet för elementet som anges i DDX-dokumentet. (Utför den här åtgärden för varje indatafil.)
   * Tilldela det `BLOB`-objekt som lagrar indatafilen till `MyMapOf_xsd_string_To_xsd_anyType_Item`-objektets `value`-fält. (Utför den här åtgärden för varje PDF-indatadokument.)
   * Lägg till `MyMapOf_xsd_string_To_xsd_anyType_Item`-objektet till `MyMapOf_xsd_string_To_xsd_anyType`-objektet. Anropa `MyMapOf_xsd_string_To_xsd_anyType`-objektets `Add`-metod och skicka `MyMapOf_xsd_string_To_xsd_anyType`-objektet. (Utför den här åtgärden för varje PDF-indatadokument.)

1. Ange körningsalternativ.

   * Skapa ett `AssemblerOptionSpec`-objekt som lagrar körningsalternativ med hjälp av dess konstruktor.
   * Ange körningsalternativ som uppfyller dina affärskrav genom att tilldela ett värde till en datamedlem som tillhör `AssemblerOptionSpec`-objektet. Om du till exempel vill instruera Assembler-tjänsten att fortsätta bearbeta ett jobb när ett fel inträffar tilldelar du `false` till `AssemblerOptionSpec`-objektets `failOnError`-datamedlem.

1. Sammanställ portföljen.

   Anropa `AssemblerServiceClient`-objektets `invokeDDX`-metod och skicka följande värden:

   * Ett `BLOB`-objekt som representerar DDX-dokumentet
   * Det `MyMapOf_xsd_string_To_xsd_anyType`-objekt som innehåller de nödvändiga filerna
   * Ett `AssemblerOptionSpec`-objekt som anger körningsalternativ

   Metoden `invokeDDX` returnerar ett `AssemblerResult`-objekt som innehåller resultatet av jobbet och eventuella undantag som inträffade.

1. Spara den monterade portföljen.

   Utför följande åtgärder för att hämta det nya PDF-Portfolio:

   * Få åtkomst till `AssemblerResult`-objektets `documents`-fält, som är ett `Map`-objekt som innehåller de resulterande PDF-dokumenten.
   * Iterera genom `Map`-objektet för att hämta varje resulterande dokument. Sedan konverterar du den matrismedlemmens `value` till `BLOB`.
   * Extrahera de binära data som representerar PDF-dokumentet genom att gå till dess `BLOB`-objektegenskap `MTOM`. Detta returnerar en array med byte som du kan skriva till en PDF-fil.

**Se även**

[Anropa AEM Forms med MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Anropa AEM Forms med SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
