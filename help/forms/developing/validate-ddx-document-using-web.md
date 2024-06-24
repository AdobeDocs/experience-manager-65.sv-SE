---
title: Validera ett DX-dokument med webbtjänstens API
description: Använd Assembler Service API för att validera ett DX-dokument.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/validating_ddx_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
role: Developer
exl-id: 069e5b10-ab93-4492-a70d-6a0d462105a6
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Services,APIs & Integrations
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '634'
ht-degree: 0%

---

# Validera ett DX-dokument med webbtjänstens API {#validate-a-ddx-document-using-theweb-service-api}

**Exempel och exempel i det här dokumentet är bara för AEM Forms i JEE-miljö.**

Validera ett DX-dokument med Assembler Service API (webbtjänsten):

1. Inkludera projektfiler.

   Skapa ett Microsoft .NET-projekt som använder MTOM. Kontrollera att du använder följande WSDL-definition: `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Ersätt localhost med IP-adressen för Forms Server.

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
   * Fylla i bytearrayen med strömdata genom att anropa `System.IO.FileStream` objektets `Read` och skickar bytearrayen, startpositionen och den flödeslängd som ska läsas.
   * Fyll i `BLOB` genom att tilldela `MTOM` med bytearrayens innehåll.

1. Ange körningsalternativ för att validera DDX-dokumentet.

   * Skapa en `AssemblerOptionSpec` objekt som lagrar körningsalternativ med hjälp av dess konstruktor.
   * Ange det körningsalternativ som instruerar Assembler-tjänsten att validera DDX-dokumentet genom att tilldela värdet true till `AssemblerOptionSpec` objektets `validateOnly` datamedlem.
   * Ange mängden information som Assembler-tjänsten skriver till loggfilen genom att tilldela ett strängvärde till `AssemblerOptionSpec` objektets `logLevel` datamedlem. -metod När du validerar ett DX-dokument vill du att mer information ska skrivas till loggfilen som ska vara till hjälp vid valideringsprocessen. Därför kan du ange värdet `FINE` eller `FINER`. Mer information om alternativ för körning som du kan ange finns i `AssemblerOptionSpec` klassreferens i [AEM Forms API-referens](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

1. Utför valideringen.

   Anropa `AssemblerServiceClient` objektets `invokeDDX` och skicka följande värden:

   * A `BLOB` -objekt som representerar DDX-dokumentet.
   * Värdet `null` för `Map` objekt som vanligtvis lagrar PDF-dokument.
   * An `AssemblerOptionSpec` objekt som anger körningsalternativ.

   The `invokeDDX` returnerar en `AssemblerResult` -objekt som innehåller information som anger om DDX-dokumentet är giltigt.

1. Spara valideringsresultaten i en loggfil.

   * Skapa en `System.IO.FileStream` genom att anropa dess konstruktor och skicka ett strängvärde som representerar filplatsen för loggfilen och läget som filen ska öppnas i. Kontrollera att filnamnstillägget är .xml.
   * Skapa en `BLOB` objekt som lagrar logginformation genom att hämta värdet för `AssemblerResult` objektets `jobLog` datamedlem.
   * Skapa en bytearray som lagrar innehållet i `BLOB` -objekt. Fylla i bytearrayen genom att hämta värdet för `BLOB` objektets `MTOM` fält.
   * Skapa en `System.IO.BinaryWriter` genom att anropa dess konstruktor och skicka `System.IO.FileStream` -objekt.
   * Skriv bytearrayens innehåll till en PDF-fil genom att anropa `System.IO.BinaryWriter` objektets `Write` och skicka bytearrayen.

   >[!NOTE]
   >
   >Om DDX-dokumentet är ogiltigt kan du `OperationException` kastas. I catch-satsen kan du hämta värdet för `OperationException` objektets `jobLog` medlem.

**Se även**

[Validerar DDX-dokument](/help/forms/developing/validating-ddx-documents.md#validating-ddx-documents)

[Anropa AEM Forms med MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
