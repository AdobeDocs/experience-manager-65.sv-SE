---
title: Sammanställa krypterade PDF-dokument
description: Sammanställ krypterade PDF-dokument med Java API och Web Service API.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: 2caaca74-640a-4257-a81b-3e8b295cd182
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Services
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '1641'
ht-degree: 0%

---

# Sammanställa krypterade PDF-dokument {#assembling-encrypted-pdf-documents}

**Exempel och exempel i det här dokumentet är bara för AEM Forms i JEE-miljö.**

Du kan kryptera ett PDF-dokument med ett lösenord med hjälp av Assembler-tjänsten. När ett PDF-dokument har krypterats med ett lösenord måste användaren ange lösenordet för att kunna visa PDF-dokumentet i Adobe Reader eller Acrobat. Om du vill kryptera ett PDF-dokument med ett lösenord måste DDX-dokumentet innehålla krypteringselementvärden som krävs för att kryptera ett PDF-dokument.

Anta att följande DDX-dokument används för den här diskussionen.

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
        <PDF result="EncryptLoan.pdf" encryption="userProtect">
         <PDF source="inDoc" />
     </PDF>
     <PasswordEncryptionProfile name="userProtect" compatibilityLevel="Acrobat7">
         <OpenPassword>AdobeOpen</OpenPassword>
        </PasswordEncryptionProfile>
 </DDX>
```

Observera att källattributet är tilldelat värdet i det här DDX-dokumentet `inDoc`. I situationer där endast ett indatadokument i PDF skickas till Assembler-tjänsten och ett PDF-dokument returneras, och du anropar `invokeOneDocument` åtgärd, tilldela värdet `inDoc` till källattributet PDF. Vid anrop av `invokeOneDocument` operation, `inDoc` värde är en fördefinierad nyckel som måste anges i DDX-dokumentet.

Om du skickar två eller flera indatadokument till PDF till Assembler-tjänsten kan du däremot anropa `invokeDDX` operation. I det här fallet tilldelar du filnamnet för indata-PDF-dokumentet till `source` -attribut.

Krypteringstjänsten behöver inte vara en del av installationen av AEM formulär för att kunna kryptera ett PDF-dokument med ett lösenord. Se [Kryptera och dekryptera PDF-dokument](/help/forms/developing/encrypting-decrypting-pdf-documents.md).

>[!NOTE]
>
>Mer information om Assembler-tjänsten finns i [Tjänstreferens för AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Mer information om ett DX-dokument finns i [Assembler Service och DDX Reference](https://www.adobe.com/go/learn_aemforms_ddx_63).

## Sammanfattning av steg {#summary-of-steps}

Så här sätter du ihop ett krypterat PDF-dokument:

1. Inkludera projektfiler.
1. Skapa en PDF Assembler-klient.
1. Referera till ett befintligt DDX-dokument.
1. Referera till ett oskyddat PDF-dokument.
1. Ange körningsalternativ.
1. Kryptera dokumentet.
1. Spara det krypterade PDF-dokumentet.

**Inkludera projektfiler**

Inkludera nödvändiga filer i utvecklingsprojektet. Om du skapar ett klientprogram med Java, inkluderar du de JAR-filer som behövs. Om du använder webbtjänster måste du inkludera proxyfilerna.

Följande JAR-filer måste läggas till i projektets klasssökväg:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar (krävs om AEM Forms används i JBoss)
* jbossall-client.jar (krävs om AEM Forms används i JBoss)

Om AEM Forms körs på en annan J2EE-programserver än JBoss måste du ersätta filerna adobe-utilities.jar och jbossall-client.jar med JAR-filer som är specifika för J2EE-programservern som AEM Forms är distribuerad på. Information om platsen för alla AEM Forms JAR-filer finns i [Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Skapa en Assembler-klient**

Innan du programmässigt kan utföra en Assembler-åtgärd måste du skapa en Assembler-tjänstklient.

**Referera till ett befintligt DDX-dokument**

Ett DDX-dokument måste refereras till för att du ska kunna montera ett PDF-dokument. Ta till exempel det DX-dokument som introducerades i det här avsnittet. Om du vill kryptera ett PDF-dokument måste DDX-dokumentet innehålla `PasswordEncryptionProfile` -element.

**Referera till ett oskyddat PDF-dokument**

Ett oskyddat PDF-dokument måste refereras och skickas till Assembler-tjänsten för att kunna kryptera det. Om du refererar till ett PDF-dokument som redan är krypterat genereras ett undantag.

**Ange körningsalternativ**

Du kan ställa in körningsalternativ som styr beteendet för Assembler-tjänsten när den utför ett jobb. Du kan till exempel ange ett alternativ som instruerar Assembler-tjänsten att fortsätta bearbeta ett jobb om ett fel uppstår. Mer information om alternativ för körning som du kan ange finns i `AssemblerOptionSpec` klassreferens i [AEM Forms API-referens](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**Kryptera dokumentet**

När du har skapat Assembler-tjänstklienten, refererar till DDX-dokumentet som innehåller krypteringsinformation, refererar till ett oskyddat PDF-dokument och anger körningsalternativ, kan du anropa `invokeOneDocument` operation. Eftersom bara ett indatadokument i PDF skickas till Assembler-tjänsten (och ett dokument returneras) kan du använda `invokeOneDocument` i stället för `invokeDDX` operation.

**Spara det krypterade PDF-dokumentet**

Om bara ett enda PDF-dokument skickas till Assembler-tjänsten returnerar Assembler-tjänsten ett enda dokument i stället för ett samlingsobjekt. Det vill säga när du anropar `invokeOneDocument` returneras ett enda dokument. Eftersom DDX-dokumentet som refereras i det här avsnittet innehåller krypteringsinformation, returnerar Assembler-tjänsten ett PDF-dokument som är krypterat med ett lösenord.

**Se även**

[Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Programmisk sammanställning av PDF-dokument](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Sammanställa ett krypterat PDF-dokument med Java API {#assemble-an-encrypted-pdf-document-using-the-java-api}

1. Inkludera projektfiler.

   Inkludera JAR-klientfiler, som adobe-assembler-client.jar, i Java-projektets klassökväg.

1. Skapa en Assembler-klient.

   * Skapa en `ServiceClientFactory` objekt som innehåller anslutningsegenskaper.
   * Skapa en `AssemblerServiceClient` genom att använda konstruktorn och skicka `ServiceClientFactory` -objekt.

1. Referera till ett befintligt DDX-dokument.

   * Skapa en `java.io.FileInputStream` -objekt som representerar DDX-dokumentet genom att använda dess konstruktor och skicka ett strängvärde som anger platsen för DDX-filen.
   * Skapa en `com.adobe.idp.Document` genom att använda konstruktorn och skicka `java.io.FileInputStream` -objekt.

1. Referera till ett oskyddat PDF-dokument.

   * Skapa en `java.io.FileInputStream` genom att använda dess konstruktor och skicka platsen för ett oskyddat PDF-dokument.
   * Skapa en `com.adobe.idp.Document` -objektet och skicka `java.io.FileInputStream` -objekt som innehåller dokumentet PDF. Detta `com.adobe.idp.Document` objektet skickas till `invokeOneDocument` -metod.

1. Ange körningsalternativ.

   * Skapa en `AssemblerOptionSpec` objekt som lagrar körningsalternativ med hjälp av dess konstruktor.
   * Ange körningsalternativ som uppfyller dina affärsbehov genom att anropa en metod som tillhör `AssemblerOptionSpec` -objekt. Om du till exempel vill instruera tjänsten Assembler att fortsätta bearbeta ett jobb när ett fel inträffar, ska du anropa `AssemblerOptionSpec` objektets `setFailOnError` metod och skicka `false`.

1. Kryptera dokumentet.

   Anropa `AssemblerServiceClient` objektets `invokeOneDocument` och skicka följande värden:

   * A `com.adobe.idp.Document` -objekt som representerar DDX-dokumentet. Kontrollera att det här DDX-dokumentet innehåller värdet `inDoc` för källelementet PDF.
   * A `com.adobe.idp.Document` objekt som innehåller det oskyddade PDF-dokumentet.
   * A `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` -objekt som anger körningsalternativ, inklusive standardteckensnitt och jobbloggsnivå.

   The `invokeOneDocument` returnerar en `com.adobe.idp.Document` objekt som innehåller ett lösenordskrypterat PDF-dokument.

1. Spara det krypterade PDF-dokumentet.

   * Skapa en `java.io.File` och se till att filnamnstillägget är .pdf.
   * Anropa `Document` objektets `copyToFile` metod för att kopiera innehållet i `Document` till filen. Se till att du använder `Document` det objekt som `invokeOneDocument` returnerad metod.

**Se även**

[Snabbstart (SOAP): Sammanställa ett krypterat PDF-dokument med Java API](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-an-encrypted-pdf-document-using-the-java-api)

## Sammanställa ett krypterat PDF-dokument med hjälp av webbtjänstens API {#assemble-an-encrypted-pdf-document-using-the-web-service-api}

1. Inkludera projektfiler.

   Skapa ett Microsoft .NET-projekt som använder MTOM. Kontrollera att du använder följande WSDL-definition när du anger en tjänstreferens: `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Ersätt `localhost` med IP-adressen till den server där AEM Forms finns.

1. Skapa en Assembler-klient.

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
   * Fyll i `BLOB` genom att tilldela `MTOM` fält med bytearrayens innehåll.

1. Referera till ett oskyddat PDF-dokument.

   * Skapa en `BLOB` genom att använda dess konstruktor. The `BLOB` -objektet används för att lagra indatadokumentet i PDF. Detta `BLOB` objektet skickas till `invokeOneDocument` som ett argument.
   * Skapa en `System.IO.FileStream` genom att anropa dess konstruktor och skicka ett strängvärde som representerar filplatsen för indata-PDF-dokumentet och läget som filen ska öppnas i.
   * Skapa en bytearray som lagrar innehållet i `System.IO.FileStream` -objekt. Du kan bestämma storleken på bytearrayen genom att hämta `System.IO.FileStream` objektets `Length` -egenskap.
   * Fylla i bytearrayen med strömdata genom att anropa `System.IO.FileStream` objektets `Read` och skickar bytearrayen, startpositionen och den flödeslängd som ska läsas.
   * Fyll i `BLOB` genom att tilldela `MTOM` fält med bytearrayens innehåll.

1. Ange körningsalternativ.

   * Skapa en `AssemblerOptionSpec` objekt som lagrar körningsalternativ med hjälp av dess konstruktor.
   * Ange körningsalternativ som uppfyller dina affärskrav genom att tilldela ett värde till en datamedlem som tillhör `AssemblerOptionSpec` -objekt. Om du till exempel vill instruera Assembler-tjänsten att fortsätta bearbeta ett jobb när ett fel inträffar tilldelar du `false` till `AssemblerOptionSpec` objektets `failOnError` datamedlem.

1. Kryptera dokumentet.

   Anropa `AssemblerServiceClient` objektets `invokeOneDocument` och skicka följande värden:

   * A `BLOB` objekt som representerar DDX-dokumentet
   * A `BLOB` objekt som representerar det oskyddade PDF-dokumentet
   * An `AssemblerOptionSpec` objekt som anger körningsalternativ

   The `invokeOneDocument` returnerar en `BLOB` objekt som innehåller ett krypterat PDF-dokument.

1. Spara det krypterade PDF-dokumentet.

   * Skapa en `System.IO.FileStream` genom att anropa dess konstruktor och skicka ett strängvärde som representerar filplatsen för det krypterade PDF-dokumentet och läget som filen ska öppnas i.
   * Skapa en bytearray som lagrar innehållet i `BLOB` det objekt som `invokeOneDocument` returnerad metod. Fylla i bytearrayen genom att hämta värdet för `BLOB` objektets `MTOM` datamedlem.
   * Skapa en `System.IO.BinaryWriter` genom att anropa dess konstruktor och skicka `System.IO.FileStream` -objekt.
   * Skriv bytearrayens innehåll till en PDF-fil genom att anropa `System.IO.BinaryWriter` objektets `Write` och skicka bytearrayen.

**Se även**

[Anropa AEM Forms med MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
