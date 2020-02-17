---
title: Sammanställa krypterade PDF-dokument
seo-title: Sammanställa krypterade PDF-dokument
description: 'null'
seo-description: 'null'
uuid: d0948ec9-ab67-4fe4-9062-1c4938460b43
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 6d75c7b1-9c0e-47f3-bdb1-61acf16b97f9
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Sammanställa krypterade PDF-dokument {#assembling-encrypted-pdf-documents}

Du kan kryptera ett PDF-dokument med ett lösenord med hjälp av tjänsten Assembler. När ett PDF-dokument har krypterats med ett lösenord måste användaren ange lösenordet för att kunna visa PDF-dokumentet i Adobe Reader eller Acrobat. Om du vill kryptera ett PDF-dokument med ett lösenord måste DDX-dokumentet innehålla krypteringselementvärden som krävs för att kryptera ett PDF-dokument.

Anta att följande DDX-dokument används för den här diskussionen.

```as3
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

Observera att källattributet är tilldelat värdet i det här DDX-dokumentet `inDoc`. Om bara ett PDF-indatadokument skickas till Assembler-tjänsten och ett PDF-dokument returneras, och du anropar `invokeOneDocument` åtgärden, tilldelar du värdet `inDoc` till PDF-källattributet. När du anropar `invokeOneDocument` åtgärden är `inDoc` värdet en fördefinierad nyckel som måste anges i DDX-dokumentet.

Om du skickar två eller flera PDF-indatadokument till Assembler-tjänsten kan du däremot anropa `invokeDDX` åtgärden. I så fall tilldelar du filnamnet för PDF-indatadokumentet till `source` -attributet.

Krypteringstjänsten behöver inte vara en del av AEM-formulärsinstallationen för att kunna kryptera ett PDF-dokument med ett lösenord. Se [Kryptera och dekryptera PDF-dokument](/help/forms/developing/encrypting-decrypting-pdf-documents.md).

>[!NOTE]
>
>Mer information om tjänsten Assembler finns i [Tjänstreferens för AEM-formulär](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Mer information om ett DDX-dokument finns i [Assembler Service och DDX Reference](https://www.adobe.com/go/learn_aemforms_ddx_63).

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
* adobe-utilities.jar (krävs om AEM Forms distribueras på JBoss)
* jbossall-client.jar (krävs om AEM Forms distribueras på JBoss)

Om AEM Forms används på en annan J2EE-programserver än JBoss måste du ersätta filerna adobe-utilities.jar och jbossall-client.jar med JAR-filer som är specifika för J2EE-programservern som AEM Forms distribueras på. Information om platsen för alla AEM Forms JAR-filer finns i [Inkludera Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)för AEM Forms.

**Skapa en Assembler-klient**

Innan du programmässigt kan utföra en Assembler-åtgärd måste du skapa en Assembler-tjänstklient.

**Referera till ett befintligt DDX-dokument**

Det måste finnas referenser till ett DDX-dokument för att du ska kunna sammanställa ett PDF-dokument. Ta till exempel det DX-dokument som introducerades i det här avsnittet. Om du vill kryptera ett PDF-dokument måste DDX-dokumentet innehålla `PasswordEncryptionProfile` elementet.

**Referera till ett oskyddat PDF-dokument**

Ett oskyddat PDF-dokument måste refereras till och skickas till Assembler-tjänsten för att kunna kryptera det. Om du refererar till ett PDF-dokument som redan är krypterat genereras ett undantag.

**Ange körningsalternativ**

Du kan ställa in körningsalternativ som styr beteendet för Assembler-tjänsten när den utför ett jobb. Du kan till exempel ange ett alternativ som instruerar Assembler-tjänsten att fortsätta bearbeta ett jobb om ett fel uppstår. Mer information om de körningsalternativ du kan ange finns i klassreferensen `AssemblerOptionSpec` i API-referens [för](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)AEM Forms.

**Kryptera dokumentet**

När du har skapat Assembler-tjänstklienten, refererar till det DDX-dokument som innehåller krypteringsinformation, refererar till ett oskyddat PDF-dokument och anger körningsalternativ, kan du anropa `invokeOneDocument` åtgärden. Eftersom bara ett PDF-indatadokument skickas till Assembler-tjänsten (och ett dokument returneras) kan du använda `invokeOneDocument` åtgärden i stället för `invokeDDX` åtgärden.

**Spara det krypterade PDF-dokumentet**

Om bara ett PDF-dokument skickas till Assembler-tjänsten returnerar Assembler-tjänsten ett enstaka dokument i stället för ett samlingsobjekt. Det innebär att när `invokeOneDocument` åtgärden anropas returneras ett enda dokument. Eftersom det DDX-dokument som det här avsnittet refererar till innehåller krypteringsinformation, returnerar Assembler-tjänsten ett PDF-dokument som är krypterat med ett lösenord.

**Se även**

[Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Programmisk sammanställning av PDF-dokument](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Sammanställa ett krypterat PDF-dokument med Java API {#assemble-an-encrypted-pdf-document-using-the-java-api}

1. Inkludera projektfiler.

   Inkludera JAR-klientfiler, t.ex. adobe-assembler-client.jar, i Java-projektets klassökväg.

1. Skapa en Assembler-klient.

   * Skapa ett `ServiceClientFactory` objekt som innehåller anslutningsegenskaper.
   * Skapa ett `AssemblerServiceClient` objekt med hjälp av dess konstruktor och skicka `ServiceClientFactory` objektet.

1. Referera till ett befintligt DDX-dokument.

   * Skapa ett `java.io.FileInputStream` objekt som representerar DDX-dokumentet med hjälp av dess konstruktor och skicka ett strängvärde som anger platsen för DDX-filen.
   * Skapa ett `com.adobe.idp.Document` objekt med hjälp av dess konstruktor och skicka `java.io.FileInputStream` objektet.

1. Referera till ett oskyddat PDF-dokument.

   * Skapa ett `java.io.FileInputStream` objekt med hjälp av dess konstruktor och skicka platsen för ett oskyddat PDF-dokument.
   * Skapa ett `com.adobe.idp.Document` objekt och skicka `java.io.FileInputStream` objektet som innehåller PDF-dokumentet. Detta `com.adobe.idp.Document` objekt skickas till `invokeOneDocument` metoden.

1. Ange körningsalternativ.

   * Skapa ett `AssemblerOptionSpec` objekt som lagrar körningsalternativ med hjälp av dess konstruktor.
   * Ange körningsalternativ som uppfyller dina affärsbehov genom att anropa en metod som tillhör `AssemblerOptionSpec` objektet. Om du till exempel vill instruera Assembler-tjänsten att fortsätta bearbeta ett jobb när ett fel inträffar, anropar du `AssemblerOptionSpec` objektets `setFailOnError` metod och skickar `false`.

1. Kryptera dokumentet.

   Anropa `AssemblerServiceClient` objektets `invokeOneDocument` metod och skicka följande värden:

   * Ett `com.adobe.idp.Document` objekt som representerar DDX-dokumentet. Kontrollera att det här DDX-dokumentet innehåller värdet `inDoc` för PDF-källelementet.
   * Ett `com.adobe.idp.Document` objekt som innehåller det oskyddade PDF-dokumentet.
   * Ett `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` objekt som anger körningsalternativen, inklusive standardteckensnitt och jobbloggsnivå.
   Metoden returnerar `invokeOneDocument` ett `com.adobe.idp.Document` objekt som innehåller ett lösenordskrypterat PDF-dokument.

1. Spara det krypterade PDF-dokumentet.

   * Skapa ett `java.io.File` objekt och kontrollera att filnamnstillägget är .pdf.
   * Anropa `Document` objektets `copyToFile` metod för att kopiera innehållet i `Document` objektet till filen. Se till att du använder det `Document` objekt som `invokeOneDocument` metoden returnerade.

**Se även**

[Snabbstart (SOAP-läge): Sammanställa ett krypterat PDF-dokument med Java API](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-an-encrypted-pdf-document-using-the-java-api)

## Sammanställa ett krypterat PDF-dokument med hjälp av webbtjänstens API {#assemble-an-encrypted-pdf-document-using-the-web-service-api}

1. Inkludera projektfiler.

   Skapa ett Microsoft .NET-projekt som använder MTOM. Kontrollera att du använder följande WSDL-definition när du anger en tjänstreferens: `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Ersätt `localhost` med IP-adressen för servern som är värd för AEM Forms.

1. Skapa en Assembler-klient.

   * Skapa ett `AssemblerServiceClient` objekt med hjälp av dess standardkonstruktor.
   * Skapa ett `AssemblerServiceClient.Endpoint.Address` objekt med hjälp av `System.ServiceModel.EndpointAddress` konstruktorn. Skicka ett strängvärde som anger WSDL till AEM Forms-tjänsten (till exempel `http://localhost:8080/soap/services/AssemblerService?blob=mtom`). Du behöver inte använda attributet `lc_version` . Det här attributet används när du skapar en tjänstreferens.
   * Skapa ett `System.ServiceModel.BasicHttpBinding` objekt genom att hämta värdet för `AssemblerServiceClient.Endpoint.Binding` fältet. Sänd returvärdet till `BasicHttpBinding`.
   * Ställ in `System.ServiceModel.BasicHttpBinding` objektets `MessageEncoding` fält till `WSMessageEncoding.Mtom`. Detta värde garanterar att MTOM används.
   * Aktivera grundläggande HTTP-autentisering genom att utföra följande åtgärder:

      * Tilldela användarnamnet för AEM-formulär till fältet `AssemblerServiceClient.ClientCredentials.UserName.UserName`.
      * Tilldela motsvarande lösenordsvärde till fältet `AssemblerServiceClient.ClientCredentials.UserName.Password`.
      * Tilldela konstantvärdet `HttpClientCredentialType.Basic` till fältet `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Tilldela konstantvärdet `BasicHttpSecurityMode.TransportCredentialOnly` till fältet `BasicHttpBindingSecurity.Security.Mode`.

1. Referera till ett befintligt DDX-dokument.

   * Skapa ett `BLOB` objekt med hjälp av dess konstruktor. Objektet används `BLOB` för att lagra DDX-dokumentet.
   * Skapa ett `System.IO.FileStream` objekt genom att anropa dess konstruktor och skicka ett strängvärde som representerar filplatsen för DDX-dokumentet och läget som filen ska öppnas i.
   * Skapa en bytearray som lagrar innehållet i `System.IO.FileStream` objektet. Du kan bestämma storleken på bytearrayen genom att hämta `System.IO.FileStream` objektets `Length` egenskap.
   * Fyll bytearrayen med strömdata genom att anropa `System.IO.FileStream` objektets `Read` metod och skicka bytearrayen, startpositionen och den strömlängd som ska läsas.
   * Fyll objektet `BLOB` genom att tilldela dess `MTOM` fält med innehållet i bytearrayen.

1. Referera till ett oskyddat PDF-dokument.

   * Skapa ett `BLOB` objekt med hjälp av dess konstruktor. Objektet används `BLOB` för att lagra PDF-indatadokumentet. Detta `BLOB` objekt skickas till `invokeOneDocument` som ett argument.
   * Skapa ett `System.IO.FileStream` objekt genom att anropa dess konstruktor och skicka ett strängvärde som representerar platsen för PDF-indatadokumentet och läget som filen ska öppnas i.
   * Skapa en bytearray som lagrar innehållet i `System.IO.FileStream` objektet. Du kan bestämma storleken på bytearrayen genom att hämta `System.IO.FileStream` objektets `Length` egenskap.
   * Fyll bytearrayen med strömdata genom att anropa `System.IO.FileStream` objektets `Read` metod och skicka bytearrayen, startpositionen och den strömlängd som ska läsas.
   * Fyll objektet `BLOB` genom att tilldela dess `MTOM` fält med innehållet i bytearrayen.

1. Ange körningsalternativ.

   * Skapa ett `AssemblerOptionSpec` objekt som lagrar körningsalternativ med hjälp av dess konstruktor.
   * Ange körningsalternativ som uppfyller dina affärskrav genom att tilldela ett värde till en datamedlem som tillhör `AssemblerOptionSpec` objektet. Om du till exempel vill instruera Assembler-tjänsten att fortsätta bearbeta ett jobb när ett fel inträffar tilldelar du `false` till `AssemblerOptionSpec` objektets `failOnError` datamedlem.

1. Kryptera dokumentet.

   Anropa `AssemblerServiceClient` objektets `invokeOneDocument` metod och skicka följande värden:

   * Ett `BLOB` objekt som representerar DDX-dokumentet
   * Ett `BLOB` objekt som representerar det oskyddade PDF-dokumentet
   * Ett `AssemblerOptionSpec` objekt som anger körningsalternativ
   Metoden returnerar `invokeOneDocument` ett `BLOB` objekt som innehåller ett krypterat PDF-dokument.

1. Spara det krypterade PDF-dokumentet.

   * Skapa ett `System.IO.FileStream` objekt genom att anropa dess konstruktor och skicka ett strängvärde som representerar filplatsen för det krypterade PDF-dokumentet och läget som filen ska öppnas i.
   * Skapa en bytearray som lagrar innehållet i det `BLOB` objekt som `invokeOneDocument` metoden returnerade. Fyll i bytearrayen genom att hämta värdet för `BLOB` objektets `MTOM` datamedlem.
   * Skapa ett `System.IO.BinaryWriter` objekt genom att anropa dess konstruktor och skicka `System.IO.FileStream` objektet.
   * Skriv bytearrayens innehåll till en PDF-fil genom att anropa `System.IO.BinaryWriter` objektets `Write` metod och skicka bytearrayen.

**Se även**

[Anropa AEM-formulär med MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
