---
title: Importera och exportera data
description: Använd tjänsten för integrering av formulärdata för att importera data till ett PDF-formulär och exportera data från ett PDF-formulär med Java API och Web Service API.
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: 96310e0a-8e95-4a55-9508-5298b8d67f83
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '2754'
ht-degree: 0%

---

# Importera och exportera data {#importing-and-exporting-data}

**Exempel och exempel i det här dokumentet är bara för AEM Forms i JEE-miljö.**

## Om tjänsten för integrering av formulärdata {#about-the-form-data-integration-service}

Tjänsten för integrering av formulärdata kan importera data till ett PDF-formulär och exportera data från ett PDF-formulär. Import- och exportåtgärderna stöder två typer av PDF forms:

* Ett Acrobat-formulär (skapat i Acrobat) är ett PDF-dokument som innehåller formulärfält.
* Ett Adobe XML-formulär (skapat i Designer) är ett PDF-dokument som överensstämmer med XML Forms Architecture (XFA) för XML Adobe.

Formulärdata kan finnas i något av följande format beroende på vilken typ av PDF-formulär det är:

* En XFDF-fil, som är en XML-version av Acrobat formulärdataformat.
* En XDP-fil, som är en XML-fil som innehåller formulärfältsdefinitioner. Den kan också innehålla formulärfältdata och en inbäddad PDF-fil. En XDP-fil som genererats av Designer kan bara användas om den innehåller ett inbäddat base-64-kodat PDF-dokument.

Du kan utföra dessa uppgifter med hjälp av tjänsten för integrering av formulärdata:

* Importera data till PDF forms. Mer information finns i [Importera formulärdata](importing-exporting-data.md#importing-form-data).
* Exportera data från PDF forms. Mer information finns i [Exporterar formulärdata](importing-exporting-data.md#exporting-form-data).

>[!NOTE]
>
>Mer information om tjänsten för integrering av formulärdata finns i [Tjänstreferens för AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Importera formulärdata {#importing-form-data}

Du kan importera formulärdata till interaktiva PDF forms med hjälp av tjänsten för integrering av formulärdata. Ett interaktivt PDF-formulär är ett PDF-dokument som innehåller ett eller flera fält för att samla in information från en användare eller för att visa anpassad information. Tjänsten Form Data Integration stöder inte formulärberäkningar, validering eller skript.

Om du vill importera data till ett formulär som skapats i Designer måste du referera till en giltig XDP XML-datakälla. Titta på följande exempelformulär för låneansökan.

![ie_ie_loanformdata](assets/ie_ie_loanformdata.png)

Om du vill importera datavärden till det här formuläret måste du ha en giltig XDP XML-datakälla som motsvarar formuläret. Du kan inte använda en godtycklig XML-datakälla för att importera data till ett formulär med hjälp av tjänsten för integrering av formulärdata. Skillnaden mellan en godtycklig XML-datakälla och en XDP XML-datakälla är att en XDP-datakälla överensstämmer med XML Forms Architecture (XFA). Följande XML representerar en XDP XML-datakälla som motsvarar exempelformuläret för låneansökan.

```xml
 <?xml version="1.0" encoding="UTF-8" ?>
 - <xfa:datasets xmlns:xfa="https://www.xfa.org/schema/xfa-data/1.0/">
 - <xfa:data>
 - <data>
     - <Layer>
         <closeDate>1/26/2007</closeDate>
         <lastName>Johnson</lastName>
         <firstName>Jerry</firstName>
         <mailingAddress>JJohnson@NoMailServer.com</mailingAddress>
         <city>New York</city>
         <zipCode>00501</zipCode>
         <state>NY</state>
         <dateBirth>26/08/1973</dateBirth>
         <middleInitials>D</middleInitials>
         <socialSecurityNumber>(555) 555-5555</socialSecurityNumber>
         <phoneNumber>5555550000</phoneNumber>
     </Layer>
     - <Mortgage>
         <mortgageAmount>295000.00</mortgageAmount>
         <monthlyMortgagePayment>1724.54</monthlyMortgagePayment>
         <purchasePrice>300000</purchasePrice>
         <downPayment>5000</downPayment>
         <term>25</term>
         <interestRate>5.00</interestRate>
     </Mortgage>
 </data>
 </xfa:data>
 </xfa:datasets>
```

>[!NOTE]
>
>Mer information om tjänsten för integrering av formulärdata finns i [Tjänstreferens för AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Sammanfattning av steg {#summary-of-steps}

Så här importerar du formulärdata till ett PDF-formulär:

1. Inkludera projektfiler.
1. Skapa en tjänstklient för integrering av formulärdata.
1. Referera till ett PDF-formulär.
1. Referera till en XML-datakälla.
1. Importera data till PDF-formuläret.
1. Spara PDF-formuläret som en PDF-fil.

**Inkludera projektfiler**

Inkludera nödvändiga filer i utvecklingsprojektet. Om du skapar ett klientprogram med Java inkluderar du de JAR-filer som behövs. Om du använder webbtjänster måste du inkludera proxyfilerna.

Följande JAR-filer måste läggas till i projektets klassökväg:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-formdataintegration-client.jar
* adobe-utilities.jar (krävs om AEM Forms används i JBoss)
* jbossall-client.jar (krävs om AEM Forms distribueras på JBoss)

Mer information om var dessa JAR-filer finns i [Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Skapa en tjänstklient för integrering av formulärdata**

Innan du programmässigt kan importera data till ett klient-API i PDF måste du skapa en dataintegreringstjänstklient. När du skapar en tjänstklient definierar du de anslutningsinställningar som krävs för att anropa en tjänst. Mer information finns i [Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).

**Referera till ett PDF-formulär**

Om du vill importera data till ett PDF-formulär måste du referera till antingen ett XML-formulär som har skapats i Designer eller ett Acrobat-formulär som har skapats i Acrobat.

**Referera en XML-datakälla**

Om du vill importera formulärdata måste du referera till en giltig datakälla. Om du vill importera data till ett XFA XML-formulär som skapats i Designer måste du använda en XDP XML-datakälla. Om du refererar till ett Acrobat-formulär måste du använda en XFDF-datakälla. För varje fält som du vill importera data till måste du ange ett värde. Om ett element i XML-datakällan inte motsvarar ett fält i formuläret, ignoreras elementet.

**Importera data till formuläret PDF**

När du har angett en referens för ett PDF-formulär och en giltig XML-datakälla kan du importera data till PDF-formuläret.

**Spara PDF som en PDF-fil**

När du har importerat data till ett formulär kan du spara formuläret som en PDF-fil. När formuläret har sparats som en PDF-fil kan användaren öppna det i Adobe Reader eller Acrobat och se formuläret med importerade data.

**Se även**

[Importera formulärdata med Java API](importing-exporting-data.md#import-form-data-using-the-java-api)

[Importera formulärdata med hjälp av webbtjänstens API](importing-exporting-data.md#import-form-data-using-the-web-service-api)

[Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[API-snabbstart för integrering av formulärdata](/help/forms/developing/form-data-integration-service-java.md#form-data-integration-service-java-api-quick-start-soap)

[Exporterar formulärdata](importing-exporting-data.md#exporting-form-data)

### Importera formulärdata med Java API {#import-form-data-using-the-java-api}

Importera formulärdata med hjälp av API:t för integrering av formulärdata (Java):

1. Inkludera projektfiler.

   Inkludera JAR-klientfiler, t.ex. adobe-formdataintegration-client.jar, i Java-projektets klassökväg.

1. Skapa en tjänstklient för integrering av formulärdata.

   * Skapa en `ServiceClientFactory` objekt som innehåller anslutningsegenskaper.
   * Skapa en `FormDataIntegrationClient` genom att använda konstruktorn och skicka `ServiceClientFactory` -objekt.

1. Referera till ett PDF-formulär.

   * Skapa en `java.io.FileInputStream` genom att använda dess konstruktor. Skicka ett strängvärde som anger platsen för PDF-formuläret.
   * Skapa en `com.adobe.idp.Document` objekt som lagrar PDF-formuläret med `com.adobe.idp.Document` konstruktor. Skicka `java.io.FileInputStream` objekt som innehåller PDF-formen till konstruktorn.

1. Referera till en XML-datakälla.

   * Skapa en `java.io.FileInputStream` genom att använda dess konstruktor och skicka ett strängvärde som anger platsen för XML-filen som innehåller data som ska importeras till formuläret.
   * Skapa en `com.adobe.idp.Document` objekt som lagrar formulärdata med `com.adobe.idp.Document` konstruktor. Skicka `java.io.FileInputStream` objekt som innehåller formulärdata till konstruktorn.

1. Importera data till PDF-formuläret.

   Importera data till PDF genom att anropa `FormDataIntegrationClient` objektets `importData` och skicka följande värden:

   * The `com.adobe.idp.Document` objekt som lagrar PDF-formuläret.
   * The `com.adobe.idp.Document` objekt som lagrar formulärdata.

   The `importData` returnerar en `com.adobe.idp.Document` objekt som lagrar ett PDF-formulär som innehåller data i XML-datakällan.

1. Spara PDF-formuläret som en PDF-fil.

   * Skapa en `java.io.File` och se till att filtillägget är .PDF.
   * Anropa `Document` objektets `copyToFile` metod för att kopiera innehållet i `Document` till filen (se till att du använder `Document` objekt som returneras av `importData` metod).

**Se även**

[Sammanfattning av steg](importing-exporting-data.md#summary-of-steps)

[Snabbstart (SOAP-läge): Importera formulärdata med Java API](/help/forms/developing/form-data-integration-service-java.md#quick-start-soap-mode-importing-form-data-using-the-java-api)

[Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Importera formulärdata med hjälp av webbtjänstens API {#import-form-data-using-the-web-service-api}

Importera formulärdata med hjälp av API:t för integrering av formulärdata (webbtjänst):

1. Inkludera projektfiler.

   Skapa ett Microsoft .NET-projekt som använder MTOM. Kontrollera att du använder följande WSDL-definition: `http://localhost:8080/soap/services/FormDataIntegration?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Ersätt `localhost` med IP-adressen till den server där AEM Forms finns.

1. Skapa en tjänstklient för integrering av formulärdata.

   * Skapa en `FormDataIntegrationClient` genom att använda dess standardkonstruktor.
   * Skapa en `FormDataIntegrationClient.Endpoint.Address` genom att använda `System.ServiceModel.EndpointAddress` konstruktor. Skicka ett strängvärde som anger WSDL till AEM Forms-tjänsten (till exempel `http://localhost:8080/soap/services/FormDataIntegration?blob=mtom`.) Du behöver inte använda `lc_version` -attribut. Det här attributet används när du skapar en tjänstreferens. Ange dock `?blob=mtom` för att använda MTOM.
   * Skapa en `System.ServiceModel.BasicHttpBinding` genom att hämta värdet för `FormDataIntegrationClient.Endpoint.Binding` fält. Skicka returvärdet till `BasicHttpBinding`.
   * Ange `System.ServiceModel.BasicHttpBinding` objektets `MessageEncoding` fält till `WSMessageEncoding.Mtom`. Detta värde garanterar att MTOM används.
   * Aktivera grundläggande HTTP-autentisering genom att utföra följande åtgärder:

      * Tilldela AEM formuläranvändarnamn till fältet `FormDataIntegrationClient.ClientCredentials.UserName.UserName`.
      * Tilldela motsvarande lösenordsvärde till fältet `FormDataIntegrationClient.ClientCredentials.UserName.Password`.
      * Tilldela konstantvärdet `HttpClientCredentialType.Basic` till fältet `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Tilldela konstantvärdet `BasicHttpSecurityMode.TransportCredentialOnly` till fältet `BasicHttpBindingSecurity.Security.Mode`.

1. Referera till ett PDF-formulär.

   * Skapa en `BLOB` genom att använda dess konstruktor. Detta `BLOB` -objektet används för att lagra PDF-formuläret.
   * Skapa en `System.IO.FileStream` genom att anropa dess konstruktor. Skicka ett strängvärde som anger var PDF-formuläret finns och i vilket läge filen ska öppnas.
   * Skapa en bytearray som lagrar innehållet i `System.IO.FileStream` -objekt. Du kan bestämma storleken på bytearrayen genom att hämta `System.IO.FileStream` objektets `Length` -egenskap.
   * Fylla i bytearrayen med strömdata genom att anropa `System.IO.FileStream` objektets `Read` -metod. Skicka bytearrayen, startpositionen och strömlängden som ska läsas.
   * Fyll i `BLOB` genom att tilldela `MTOM` fält med bytearrayens innehåll.

1. Referera till en XML-datakälla.

   * Skapa en `BLOB` genom att använda dess konstruktor. Detta `BLOB` -objektet används för att lagra data som importeras till formuläret.
   * Skapa en `System.IO.FileStream` genom att anropa dess konstruktor. Skicka ett strängvärde som anger platsen för XML-filen som innehåller data som ska importeras och läget som filen ska öppnas i.
   * Skapa en bytearray som lagrar innehållet i `System.IO.FileStream` -objekt. Du kan bestämma storleken på bytearrayen genom att hämta `System.IO.FileStream` objektets `Length` -egenskap.
   * Fylla i bytearrayen med strömdata genom att anropa `System.IO.FileStream` objektets `Read` -metod. Skicka bytearrayen, startpositionen och strömlängden som ska läsas.
   * Fyll i `BLOB` genom att tilldela `MTOM` fält med bytearrayens innehåll.

1. Importera data till PDF-formuläret.

   Importera data till PDF genom att anropa `FormDataIntegrationClient` objektets `importData` och skicka följande värden:

   * The `BLOB` objekt som lagrar PDF-formuläret.
   * The `BLOB` objekt som lagrar formulärdata.

   The `importData` returnerar en `BLOB` objekt som lagrar ett PDF-formulär som innehåller data i XML-datakällan.

1. Spara PDF-formuläret som en PDF-fil.

   * Skapa en `System.IO.FileStream` genom att anropa dess konstruktor och skicka ett strängvärde som representerar filplatsen för filen PDF.
   * Skapa en bytearray som lagrar datainnehållet i `BLOB` objekt som returneras av `importData` -metod. Fylla i bytearrayen genom att hämta värdet för `BLOB` objektets `MTOM` fält.
   * Skapa en `System.IO.BinaryWriter` genom att anropa dess konstruktor och skicka `System.IO.FileStream` -objekt.
   * Skriv bytearrayens innehåll till en PDF-fil genom att anropa `System.IO.BinaryWriter` objektets `Write` och skicka bytearrayen.

**Se även**

[Sammanfattning av steg](importing-exporting-data.md#summary-of-steps)

[Anropa AEM Forms med MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

## Exporterar formulärdata {#exporting-form-data}

Du kan exportera formulärdata från ett interaktivt PDF-formulär med hjälp av tjänsten för integrering av formulärdata. Formatet på de data som exporteras beror på formulärtypen. Om formulärtypen är ett Acrobat-formulär som har skapats i Acrobat är exporterade data XFDF. Om formulärtypen är ett XML-formulär som har skapats i Designer är exporterade data XDP.

>[!NOTE]
>
>Mer information om tjänsten för integrering av formulärdata finns i [Tjänstreferens för AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Sammanfattning av steg {#summary_of_steps-1}

Så här exporterar du formulärdata från ett PDF-formulär:

1. Inkludera projektfiler
1. Skapa en tjänstklient för integrering av formulärdata.
1. Referera till ett PDF-formulär.
1. Exportera data från PDF.
1. Spara exporterade data som en XML-fil.

**Inkludera projektfiler**

Inkludera nödvändiga filer i utvecklingsprojektet. Om du skapar ett klientprogram med Java inkluderar du de JAR-filer som behövs. Om du använder webbtjänster måste du inkludera proxyfilerna.

Följande JAR-filer måste läggas till i projektets klassökväg:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-formdataintegration-client.jar
* adobe-utilities.jar (krävs om AEM Forms används i JBoss)
* jbossall-client.jar (krävs om AEM Forms distribueras på JBoss)

**Skapa en tjänstklient för integrering av formulärdata**

Innan du kan importera data programmatiskt till ett PDF formClient-API måste du skapa en dataintegreringstjänstklient. När du skapar en tjänstklient definierar du de anslutningsinställningar som krävs för att anropa en tjänst. För information, [Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).

**Referera till ett PDF-formulär**

Om du vill exportera data från ett PDF-formulär måste du referera till PDF-formulär som har skapats i Designer eller Acrobat och som innehåller formulärdata. Om du försöker exportera data från ett tomt PDF-formulär får du ett tomt XML-schema.

**Exportera data från PDF**

När du har refererat till ett PDF-formulär som innehåller formulärdata kan du exportera data från formuläret. Data exporteras i ett XML-schema som är baserat på formuläret.

**Spara formulärdata som en XML-fil**

När du har exporterat formulärdata kan du spara data som en XML-fil. När du har sparat den som en XML-fil kan du öppna XML-filen i ett XML-visningsprogram och visa formulärdata.

**Se även**

[Exportera formulärdata med Java API](importing-exporting-data.md#export-form-data-using-the-java-api)

[Exportera formulärdata med hjälp av webbtjänstens API](importing-exporting-data.md#export-form-data-using-the-web-service-api)

[Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[API-snabbstart för integrering av formulärdata](/help/forms/developing/form-data-integration-service-java.md#form-data-integration-service-java-api-quick-start-soap)

[Importera formulärdata](importing-exporting-data.md#importing-form-data)

### Exportera formulärdata med Java API {#export-form-data-using-the-java-api}

Exportera formulärdata med hjälp av API:t för integrering av formulärdata (Java):

1. Inkludera projektfiler.

   Inkludera JAR-klientfiler, t.ex. adobe-formdataintegration-client.jar, i Java-projektets klassökväg.

1. Skapa en tjänstklient för integrering av formulärdata.

   * Skapa en `ServiceClientFactory` objekt som innehåller anslutningsegenskaper.
   * Skapa en `FormDataIntegrationClient` genom att använda konstruktorn och skicka `ServiceClientFactory` -objekt.

1. Referera till ett PDF-formulär.

   * Skapa en `java.io.FileInputStream` genom att använda dess konstruktor och skicka ett strängvärde som anger platsen för det PDF-formulär som innehåller data som ska exporteras.
   * Skapa en `com.adobe.idp.Document` objekt som lagrar PDF-formuläret med `com.adobe.idp.Document` konstruktor. Skicka `java.io.FileInputStream` objekt som innehåller PDF-formen till konstruktorn.

1. Exportera data från PDF.

   Exportera formulärdata genom att anropa `FormDataIntegrationClient` objektets `exportData` och skicka `com.adobe.idp.Document` objekt som lagrar PDF-formuläret. Den här metoden returnerar en `com.adobe.idp.Document` objekt som lagrar formulärdata som ett XML-schema.

1. Spara PDF-formuläret som en PDF-fil.

   * Skapa en `java.io.File` och se till att filtillägget är XML.
   * Anropa `Document` objektets `copyToFile` metod för att kopiera innehållet i `Document` till filen (se till att du använder `Document` objekt som returneras av `exportData` metod).

**Se även**

[Sammanfattning av steg](importing-exporting-data.md#summary-of-steps)

[Snabbstart (SOAP-läge): Exportera formulärdata med Java API](/help/forms/developing/form-data-integration-service-java.md#quick-start-soap-mode-exporting-form-data-using-the-java-api)

[Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Exportera formulärdata med hjälp av webbtjänstens API {#export-form-data-using-the-web-service-api}

Exportera formulärdata med hjälp av API:t för integrering av formulärdata (webbtjänst):

1. Inkludera projektfiler.

   Skapa ett Microsoft .NET-projekt som använder MTOM. Kontrollera att du använder följande WSDL-definition: `http://localhost:8080/soap/services/FormDataIntegration?WSDL&lc_version=9.0.1`.

   * Ersätt `localhost` med IP-adressen till den server där AEM Forms finns.

1. Skapa en tjänstklient för integrering av formulärdata.

   * Skapa en `FormDataIntegrationClient` genom att använda dess standardkonstruktor.
   * Skapa en `FormDataIntegrationClient.Endpoint.Address` genom att använda `System.ServiceModel.EndpointAddress` konstruktor. Skicka ett strängvärde som anger WSDL till AEM Forms-tjänsten (till exempel `http://localhost:8080/soap/services/FormDataIntegration?blob=mtom`.) Du behöver inte använda `lc_version` -attribut. Det här attributet används när du skapar en tjänstreferens. Ange dock `?blob=mtom` för att använda MTOM.
   * Skapa en `System.ServiceModel.BasicHttpBinding` genom att hämta värdet för `FormDataIntegrationClient.Endpoint.Binding` fält. Skicka returvärdet till `BasicHttpBinding`.
   * Ange `System.ServiceModel.BasicHttpBinding` objektets `MessageEncoding` fält till `WSMessageEncoding.Mtom`. Detta värde garanterar att MTOM används.
   * Aktivera grundläggande HTTP-autentisering genom att utföra följande åtgärder:

      * Tilldela AEM formuläranvändarnamn till fältet `FormDataIntegrationClient.ClientCredentials.UserName.UserName`.
      * Tilldela motsvarande lösenordsvärde till fältet `FormDataIntegrationClient.ClientCredentials.UserName.Password`.
      * Tilldela konstantvärdet `HttpClientCredentialType.Basic` till fältet `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Tilldela konstantvärdet `BasicHttpSecurityMode.TransportCredentialOnly` till fältet `BasicHttpBindingSecurity.Security.Mode`.

1. Referera till ett PDF-formulär.

   * Skapa en `BLOB` genom att använda dess konstruktor. Detta `BLOB` -objektet används för att lagra det PDF som data exporteras från.
   * Skapa en `System.IO.FileStream` genom att anropa dess konstruktor. Skicka ett strängvärde som anger var PDF-formuläret finns och i vilket läge filen ska öppnas.
   * Skapa en bytearray som lagrar innehållet i `System.IO.FileStream` -objekt. Du kan bestämma storleken på bytearrayen genom att hämta `System.IO.FileStream` objektets `Length` -egenskap.
   * Fylla i bytearrayen med strömdata genom att anropa `System.IO.FileStream` objektets `Read` och skickar bytearrayen, startpositionen och den flödeslängd som ska läsas.
   * Fyll i `BLOB` genom att tilldela `MTOM` fält med bytearrayens innehåll.

1. Exportera data från PDF.

   Importera data till PDF genom att anropa `FormDataIntegrationClient` objektets `exportData` och skicka `BLOB` objekt som lagrar PDF-formuläret. Den här metoden returnerar en `BLOB` objekt som lagrar formulärdata som ett XML-schema.

1. Spara PDF-formuläret som en PDF-fil.

   * Skapa en `System.IO.FileStream` genom att anropa dess konstruktor och skicka ett strängvärde som representerar platsen för XML-filen.
   * Skapa en bytearray som lagrar datainnehållet i `BLOB` objekt som returneras av `exportData` -metod. Fylla i bytearrayen genom att hämta värdet för `BLOB` objektets `MTOM` fält.
   * Skapa en `System.IO.BinaryWriter` genom att anropa dess konstruktor och skicka `System.IO.FileStream` -objekt.
   * Skriv bytearrayens innehåll till en XML-fil genom att anropa `System.IO.BinaryWriter` objektets `Write` och skicka bytearrayen.

**Se även**

[Sammanfattning av steg](importing-exporting-data.md#summary-of-steps)

[Anropa AEM Forms med MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Anropa AEM Forms med SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
