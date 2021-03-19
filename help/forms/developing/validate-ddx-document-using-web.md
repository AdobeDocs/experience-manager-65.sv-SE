---
title: Validera ett DX-dokument med webbtjänstens API
seo-title: Validera ett DX-dokument med webbtjänstens API
description: Använd Assembler Service API för att validera ett DX-dokument.
seo-description: Använd Assembler Service API för att validera ett DX-dokument.
uuid: f6125746-6138-4e46-a1c4-fb24fd7399c5
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/validating_ddx_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: a6fe91ab-3aa0-4b3d-87c0-6cf69a2c4cc4
role: Developer
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '659'
ht-degree: 0%

---


# Validera ett DX-dokument med webbtjänstens API {#validate-a-ddx-document-using-theweb-service-api}

**Exempel och exempel i det här dokumentet är bara för AEM Forms i JEE-miljö.**

Validera ett DX-dokument med Assembler Service API (webbtjänsten):

1. Inkludera projektfiler.

   Skapa ett Microsoft .NET-projekt som använder MTOM. Kontrollera att du använder följande WSDL-definition: `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Ersätt localhost med formulärserverns IP-adress.

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
   * Fyll i bytearrayen med strömdata genom att anropa `System.IO.FileStream`-objektets `Read`-metod och skicka bytearrayen, startpositionen och strömlängden som ska läsas.
   * Fyll i `BLOB`-objektet genom att tilldela dess `MTOM`-egenskap med innehållet i bytearrayen.

1. Ange körningsalternativ för att validera DDX-dokumentet.

   * Skapa ett `AssemblerOptionSpec`-objekt som lagrar körningsalternativ med hjälp av dess konstruktor.
   * Ange det körningsalternativ som instruerar Assembler-tjänsten att validera DDX-dokumentet genom att tilldela värdet true till `AssemblerOptionSpec`-objektets `validateOnly`-datamedlem.
   * Ange den mängd information som Assembler-tjänsten skriver till loggfilen genom att tilldela ett strängvärde till `AssemblerOptionSpec`-objektets `logLevel`-datamedlem. -metod När du validerar ett DX-dokument vill du att mer information ska skrivas till loggfilen som ska vara till hjälp vid valideringsprocessen. Du kan därför ange värdet `FINE` eller `FINER`. Mer information om de körningsalternativ du kan ange finns i `AssemblerOptionSpec` klassreferens i [AEM Forms API Reference](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

1. Utför valideringen.

   Anropa `AssemblerServiceClient`-objektets `invokeDDX`-metod och skicka följande värden:

   * Ett `BLOB`-objekt som representerar DDX-dokumentet.
   * Värdet `null` för `Map`-objektet som vanligtvis lagrar PDF-dokument.
   * Ett `AssemblerOptionSpec`-objekt som anger körningsalternativ.

   Metoden `invokeDDX` returnerar ett `AssemblerResult`-objekt som innehåller information som anger om DDX-dokumentet är giltigt.

1. Spara valideringsresultaten i en loggfil.

   * Skapa ett `System.IO.FileStream`-objekt genom att anropa dess konstruktor och skicka ett strängvärde som representerar platsen för loggfilen och läget som filen ska öppnas i. Kontrollera att filnamnstillägget är .xml.
   * Skapa ett `BLOB`-objekt som lagrar logginformation genom att hämta värdet för `AssemblerResult`-objektets `jobLog`-datamedlem.
   * Skapa en bytearray som lagrar innehållet i `BLOB`-objektet. Fyll i bytearrayen genom att hämta värdet för `BLOB`-objektets `MTOM`-fält.
   * Skapa ett `System.IO.BinaryWriter`-objekt genom att anropa dess konstruktor och skicka `System.IO.FileStream`-objektet.
   * Skriv bytearrayens innehåll till en PDF-fil genom att anropa `System.IO.BinaryWriter`-objektets `Write`-metod och skicka bytearrayen.

   >[!NOTE]
   >
   >Om DDX-dokumentet är ogiltigt genereras ett `OperationException`. I catch-satsen kan du hämta värdet för `OperationException`-objektets `jobLog`-medlem.

**Se även**

[Validerar DDX-dokument](/help/forms/developing/validating-ddx-documents.md#validating-ddx-documents)

[Anropa AEM Forms med MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
