---
title: Kryptera och dekryptera PDF-dokument
seo-title: Encrypting and Decrypting PDF Documents
description: Använd krypteringstjänsten för att kryptera och dekryptera dokument. Krypteringstjänsten innefattar att kryptera ett PDF-dokument med ett lösenord, kryptera ett PDF-dokument med ett certifikat, ta bort lösenordsbaserad kryptering från ett PDF-dokument, ta bort certifikatbaserad kryptering från ett PDF-dokument, låsa upp PDF-dokumentet så att andra serviceåtgärder kan utföras samt att bestämma krypteringstypen för ett säkert PDF-dokument.
seo-description: Use the Encryption service to encrypt and decrypt documents. The Encryption service tasks include encrypting a PDF document with a password, encrypting a PDF document with a certificate, removing password-based encryption from a PDF document, removing certificate-based encryption from a PDF document, unlocking the PDF document so that other service operations can be performed, and determining the encryption type of a secured PDF document.
uuid: 4e4e2716-c21f-4bfe-ae7a-7e91442414ef
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 5e4bda3a-5648-4c0f-b2f8-bdbebb88f537
role: Developer
exl-id: d3cbca7f-9277-4d61-b198-abf4bb008f15
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '8184'
ht-degree: 0%

---

# Kryptera och dekryptera PDF-dokument {#encrypting-and-decrypting-pdf-documents}

**Exempel och exempel i det här dokumentet är bara för AEM Forms i JEE-miljö.**

**Om krypteringstjänsten**

Med krypteringstjänsten kan du kryptera och dekryptera dokument. När ett dokument är krypterat blir innehållet oläsligt. En behörig användare kan dekryptera dokumentet för att få åtkomst till innehållet. Om ett PDF-dokument är krypterat med ett lösenord måste användaren ange det öppna lösenordet innan dokumentet kan visas i Adobe Reader eller Adobe Acrobat. Om ett PDF-dokument är krypterat med ett certifikat måste användaren dekryptera PDF-dokumentet med den offentliga nyckel som motsvarar det certifikat (privat nyckel) som användes för att kryptera PDF-dokumentet.

Du kan utföra följande uppgifter med krypteringstjänsten:

* Kryptera ett PDF-dokument med ett lösenord. (Se [Kryptera PDF-dokument med ett lösenord](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password).)
* Kryptera ett PDF-dokument med ett certifikat. (Se [Kryptera PDF-dokument med certifikat](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-certificates).)
* Ta bort lösenordsbaserad kryptering från ett PDF-dokument. (Se [Tar bort lösenordskryptering](encrypting-decrypting-pdf-documents.md#removing-password-encryption).)
* Ta bort certifikatbaserad kryptering från ett PDF-dokument. (Se [Tar bort certifikatbaserad kryptering](encrypting-decrypting-pdf-documents.md#removing-certificate-based-encryption).)
* Lås upp PDF-dokumentet så att andra serviceåtgärder kan utföras. När ett lösenordskrypterat PDF-dokument är olåst kan du till exempel använda en digital signatur på det. (Se [Låsa upp krypterade PDF-dokument](encrypting-decrypting-pdf-documents.md#unlocking-encrypted-pdf-documents).)
* Bestäm krypteringstypen för ett skyddat PDF-dokument. (Se [Bestämmer krypteringstyp](encrypting-decrypting-pdf-documents.md#determining-encryption-type).)

>[!NOTE]
>
>Mer information om krypteringstjänsten finns i [Tjänstreferens för AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Kryptera PDF-dokument med ett lösenord {#encrypting-pdf-documents-with-a-password}

När du krypterar ett PDF-dokument med ett lösenord måste användaren ange lösenordet för att kunna öppna PDF-dokumentet i Adobe Reader eller Acrobat. Innan en annan AEM Forms-åtgärd, som att signera PDF-dokumentet digitalt, kan utföras på dokumentet, måste dessutom ett lösenordskrypterat PDF-dokument låsas upp.

>[!NOTE]
>
>Om du överför ett krypterat PDF-dokument till AEM Forms-databasen kan det inte dekryptera PDF-dokumentet och extrahera XDP-innehållet. Du bör inte kryptera ett dokument innan du skickar det till AEM Forms-databasen. (Se [Skriver resurser](/help/forms/developing/aem-forms-repository.md#writing-resources).)

>[!NOTE]
>
>Mer information om krypteringstjänsten finns i [Tjänstreferens för AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Sammanfattning av steg {#summary-of-steps}

Så här krypterar du ett PDF-dokument med ett lösenord:

1. Inkludera projektfiler.
1. Skapa ett API-objekt för krypteringsklient.
1. Få ett PDF-dokument att kryptera.
1. Ange alternativ för kryptering vid körning.
1. Lägg till lösenordet.
1. Spara det krypterade PDF-dokumentet som en PDF-fil.

**Inkludera projektfiler**

Inkludera nödvändiga filer i utvecklingsprojektet. Om du skapar ett klientprogram med Java, inkluderar du de JAR-filer som behövs. Om du använder webbtjänster måste du inkludera proxyfilerna.

Följande JAR-filer måste läggas till i projektets klasssökväg:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-encryption-client.jar
* adobe-utilities.jar (krävs om AEM Forms används i JBoss)
* jbossall-client.jar (krävs om AEM Forms används i JBoss)

**Skapa ett API-objekt för krypteringsklient**

Om du vill utföra en krypteringstjänståtgärd programmatiskt måste du skapa en krypteringstjänstklient.

**Få ett PDF-dokument att kryptera**

Du måste skaffa ett okrypterat PDF-dokument för att kunna kryptera dokumentet med ett lösenord. Om du försöker skydda ett PDF-dokument som redan är krypterat orsakar du ett undantag.

**Ange alternativ för kryptering vid körning**

Om du vill kryptera ett PDF-dokument med ett lösenord anger du fyra värden, inklusive två lösenordsvärden. Det första lösenordsvärdet används för att kryptera PDF-dokumentet och måste anges när dokumentet öppnas i PDF. Det andra lösenordsvärdet, som heter huvudlösenordsvärdet, används för att ta bort kryptering från PDF-dokumentet. Lösenordsvärdena är skiftlägeskänsliga och dessa två lösenordsvärden kan inte vara samma.

Ange vilka dokumentresurser i PDF som ska krypteras. Du kan kryptera hela PDF-dokumentet, allt utom dokumentets metadata eller bara dokumentets bilagor. Om du bara krypterar dokumentets bilagor uppmanas användaren att ange ett lösenord när de försöker få åtkomst till de bifogade filerna.

När du krypterar ett PDF-dokument kan du ange behörigheter som är kopplade till det skyddade dokumentet. Genom att ange behörigheter kan du styra vilka åtgärder en användare som öppnar ett lösenordskrypterat PDF-dokument får utföra. Om du till exempel vill extrahera formulärdata måste du ange följande behörigheter:

* PASSWORD_EDIT_ADD
* PASSWORD_EDIT_MODIFY

>[!NOTE]
>
>Behörigheter anges som `PasswordEncryptionPermission` uppräkningsvärden.

**Lägg till lösenordet**

När du har hämtat ett oskyddat PDF-dokument och angett krypteringsvärden för körtid kan du lägga till ett lösenord i PDF-dokumentet.

**Spara det krypterade PDF-dokumentet som en PDF-fil**

Du kan spara det lösenordskrypterade PDF-dokumentet som en PDF-fil.

**Se även**

[Kryptera ett PDF-dokument med Java API](encrypting-decrypting-pdf-documents.md#encrypt-a-pdf-document-using-the-java-api)

[Kryptera ett PDF-dokument med hjälp av webbtjänstens API](encrypting-decrypting-pdf-documents.md#encrypting-a-pdf-document-using-the-web-service-api)

[Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[API-snabbstart för krypteringstjänst](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

[Kryptera PDF-dokument med certifikat](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-certificates)

### Kryptera ett PDF-dokument med Java API {#encrypt-a-pdf-document-using-the-java-api}

Kryptera ett PDF-dokument med ett lösenord med hjälp av krypterings-API (Java):

1. Inkludera projektfiler.

   Inkludera JAR-klientfiler, t.ex. adobe-encryption-client.jar, i Java-projektets klassökväg.

1. Skapa ett API för krypteringsklient.

   * Skapa en `ServiceClientFactory` objekt som innehåller anslutningsegenskaper.
   * Skapa en `EncryptionServiceClient` genom att använda konstruktorn och skicka `ServiceClientFactory` -objekt.

1. Få ett PDF-dokument att kryptera.

   * Skapa en `java.io.FileInputStream` objekt som representerar PDF-dokumentet som ska krypteras med hjälp av konstruktorn och som skickar ett strängvärde som anger platsen för PDF-dokumentet.
   * Skapa en `com.adobe.idp.Document` genom att använda konstruktorn och skicka `java.io.FileInputStream` -objekt.

1. Ange alternativ för kryptering vid körning.

   * Skapa en `PasswordEncryptionOptionSpec` genom att anropa dess konstruktor.
   * Ange vilka PDF-dokumentresurser som ska krypteras genom att anropa `PasswordEncryptionOptionSpec` objektets `setEncryptOption` metod och skicka en `PasswordEncryptionOption` uppräkningsvärde som anger vilka dokumentresurser som ska krypteras. Om du till exempel vill kryptera hela PDF-dokumentet, inklusive dess metadata och bilagor, anger du `PasswordEncryptionOption.ALL`.
   * Skapa en `java.util.List` som lagrar krypteringsbehörigheterna med `ArrayList` konstruktor.
   * Ange en behörighet genom att anropa `java.util.List` objekt&quot;s `add` och skickar ett uppräkningsvärde som motsvarar den behörighet som du vill ange. Om du till exempel vill ange den behörighet som gör att en användare kan kopiera data i PDF-dokumentet, anger du `PasswordEncryptionPermission.PASSWORD_EDIT_COPY`. (Upprepa det här steget för varje behörighet att ange).
   * Ange kompatibilitetsalternativet för Acrobat genom att anropa `PasswordEncryptionOptionSpec` objektets `setCompatability` och skickar ett uppräkningsvärde som anger kompatibilitetsnivån för Acrobat. Du kan till exempel ange `PasswordEncryptionCompatability.ACRO_7`.
   * Ange det lösenordsvärde som gör att en användare kan öppna det krypterade PDF-dokumentet genom att anropa `PasswordEncryptionOptionSpec` objektets `setDocumentOpenPassword` och skickar ett strängvärde som representerar det öppna lösenordet.
   * Ange det huvudlösenordsvärde som gör att en användare kan ta bort kryptering från PDF-dokumentet genom att anropa `PasswordEncryptionOptionSpec` objektets `setPermissionPassword` och skickar ett strängvärde som representerar huvudlösenordet.

1. Lägg till lösenordet.

   Kryptera PDF genom att anropa `EncryptionServiceClient` objektets `encryptPDFUsingPassword` och skicka följande värden:

   * The `com.adobe.idp.Document` som innehåller det PDF-dokument som ska krypteras med lösenordet.
   * The `PasswordEncryptionOptionSpec` objekt som innehåller alternativ för kryptering vid körning.

   The `encryptPDFUsingPassword` returnerar en `com.adobe.idp.Document` objekt som innehåller ett lösenordskrypterat PDF-dokument.

1. Spara det krypterade PDF-dokumentet som en PDF-fil.

   * Skapa en `java.io.File` och se till att filtillägget är .pdf.
   * Anropa `com.adobe.idp.Document` objektets `copyToFile` metod för att kopiera innehållet i `com.adobe.idp.Document` till filen. Se till att du använder `com.adobe.idp.Document` objekt som returneras av `encryptPDFUsingPassword` -metod.

**Se även**

[Sammanfattning av steg](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[Snabbstart (SOAP-läge): Kryptera ett PDF-dokument med Java API](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-encrypting-a-pdf-document-using-the-java-api)

[Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Kryptera ett PDF-dokument med hjälp av webbtjänstens API {#encrypting-a-pdf-document-using-the-web-service-api}

Kryptera ett PDF-dokument med ett lösenord med hjälp av krypterings-API:t (webbtjänsten):

1. Inkludera projektfiler.

   Skapa ett Microsoft .NET-projekt som använder MTOM. Kontrollera att du använder följande WSDL-definition: `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Ersätt `localhost` med IP-adressen till den server där AEM Forms finns.

1. Skapa ett API-objekt för krypteringsklient.

   * Skapa en `EncryptionServiceClient` genom att använda dess standardkonstruktor.
   * Skapa en `EncryptionServiceClient.Endpoint.Address` genom att använda `System.ServiceModel.EndpointAddress` konstruktor. Skicka ett strängvärde som anger WSDL till AEM Forms-tjänsten (till exempel `http://localhost:8080/soap/services/EncryptionService?WSDL`.) Du behöver inte använda `lc_version` -attribut. Detta attribut används när du skapar en tjänstreferens.)
   * Skapa en `System.ServiceModel.BasicHttpBinding` genom att hämta värdet för `EncryptionServiceClient.Endpoint.Binding` fält. Skicka returvärdet till `BasicHttpBinding`.
   * Ange `System.ServiceModel.BasicHttpBinding` objektets `MessageEncoding` fält till `WSMessageEncoding.Mtom`. Detta värde garanterar att MTOM används.
   * Aktivera grundläggande HTTP-autentisering genom att utföra följande åtgärder:

      * Tilldela AEM formuläranvändarnamn till fältet `EncryptionServiceClient.ClientCredentials.UserName.UserName`.
      * Tilldela motsvarande lösenordsvärde till fältet `EncryptionServiceClient.ClientCredentials.UserName.Password`.
      * Tilldela konstantvärdet `HttpClientCredentialType.Basic` till fältet `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Tilldela konstantvärdet `BasicHttpSecurityMode.TransportCredentialOnly` till fältet `BasicHttpBindingSecurity.Security.Mode`.

1. Få ett PDF-dokument att kryptera.

   * Skapa en `BLOB` genom att använda dess konstruktor. The `BLOB` används för att lagra ett PDF-dokument som är krypterat med ett lösenord.
   * Skapa en `System.IO.FileStream` genom att anropa dess konstruktor och skicka ett strängvärde som representerar filplatsen för det PDF-dokument som ska krypteras och läget i vilket filen ska öppnas.
   * Skapa en bytearray som lagrar innehållet i `System.IO.FileStream` -objekt. Du kan bestämma storleken på bytearrayen genom att hämta `System.IO.FileStream` objektets `Length` -egenskap.
   * Fylla i bytearrayen med strömdata genom att anropa `System.IO.FileStream` objektets `Read` och skickar bytearrayen, startpositionen och den flödeslängd som ska läsas.
   * Fyll i `BLOB` genom att tilldela innehållet i bytearrayen till `BLOB` objektets `MTOM` datamedlem.

1. Ange alternativ för kryptering vid körning.

   * Skapa en `PasswordEncryptionOptionSpec` genom att använda dess konstruktor.
   * Ange vilka PDF-dokumentresurser som ska krypteras genom att tilldela en `PasswordEncryptionOption` uppräkningsvärde till `PasswordEncryptionOptionSpec` objektets `encryptOption` datamedlem. Om du vill kryptera hela PDF, inklusive dess metadata och bilagor, tilldelar du `PasswordEncryptionOption.ALL` till denna datamedlem.
   * Ange kompatibilitetsalternativet för Acrobat genom att tilldela en `PasswordEncryptionCompatability` uppräkningsvärde till `PasswordEncryptionOptionSpec` objektets `compatability` datamedlem. Tilldela till exempel `PasswordEncryptionCompatability.ACRO_7` till denna datamedlem.
   * Ange det lösenordsvärde som gör att en användare kan öppna det krypterade PDF-dokumentet genom att tilldela ett strängvärde som representerar det öppna lösenordet till `PasswordEncryptionOptionSpec` objektets `documentOpenPassword` datamedlem.
   * Ange det lösenordsvärde som gör att en användare kan ta bort kryptering från PDF-dokumentet genom att tilldela ett strängvärde som representerar huvudlösenordet till `PasswordEncryptionOptionSpec` objektets `permissionPassword` datamedlem.

1. Lägg till lösenordet.

   Kryptera PDF genom att anropa `EncryptionServiceClient` objektets `encryptPDFUsingPassword` och skicka följande värden:

   * The `BLOB` som innehåller det PDF-dokument som ska krypteras med lösenordet.
   * The `PasswordEncryptionOptionSpec` objekt som innehåller alternativ för kryptering vid körning.

   The `encryptPDFUsingPassword` returnerar en `BLOB` objekt som innehåller ett lösenordskrypterat PDF-dokument.

1. Spara det krypterade PDF-dokumentet som en PDF-fil.

   * Skapa en `System.IO.FileStream` genom att anropa dess konstruktor och skicka ett strängvärde som representerar filplatsen för det skyddade PDF-dokumentet.
   * Skapa en bytearray som lagrar datainnehållet i `BLOB` objekt som returneras av `encryptPDFUsingPassword` -metod. Fylla i bytearrayen genom att hämta värdet för `BLOB` objektets `MTOM` datamedlem.
   * Skapa en `System.IO.BinaryWriter` genom att anropa dess konstruktor och skicka `System.IO.FileStream` -objekt.
   * Skriv bytearrayens innehåll till en PDF-fil genom att anropa `System.IO.BinaryWriter` objektets `Write` och skicka bytearrayen.

**Se även**

[Sammanfattning av steg](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[Anropa AEM Forms med MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Anropa AEM Forms med SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Kryptera PDF-dokument med certifikat {#encrypting-pdf-documents-with-certificates}

Med certifikatbaserad kryptering kan du kryptera ett dokument för specifika mottagare med hjälp av teknik för offentlig nyckel. Olika mottagare kan få olika behörigheter för dokumentet. Många krypteringsaspekter blir möjliga med hjälp av teknik med publika nycklar. En algoritm används för att generera två stora tal, så kallade *tangenter*, som har följande egenskaper:

* En nyckel används för att kryptera en datauppsättning. Därefter kan bara den andra nyckeln användas för att dekryptera data.
* Det är omöjligt att skilja på den ena nyckeln och den andra.

En av nycklarna fungerar som en användares privata nyckel. Det är viktigt att bara användaren har tillgång till den här nyckeln. Den andra nyckeln är användarens offentliga nyckel, som kan delas med andra.

Ett certifikat för offentlig nyckel innehåller en användares offentliga nyckel och identifieringsinformation. X.509-formatet används för att lagra certifikat. Certifikat utfärdas och signeras vanligtvis digitalt av en certifikatutfärdare (CA), som är en erkänd enhet som kan mäta förtroendet för certifikatets giltighet. Certifikat har ett förfallodatum och är inte längre giltiga. Dessutom innehåller listor över återkallade certifikat information om certifikat som återkallats före förfallodatumet. CRL-listor publiceras regelbundet av certifikatutfärdare. Återkallningsstatusen för ett certifikat kan också hämtas via OCSP (Online Certificate Status Protocol) via nätverket.

>[!NOTE]
>
>Om du överför ett krypterat PDF-dokument till AEM Forms-databasen kan det inte dekryptera PDF-dokumentet och extrahera XDP-innehållet. Du bör inte kryptera ett dokument innan du skickar det till AEM Forms-databasen. (Se [Skriver resurser](/help/forms/developing/aem-forms-repository.md#writing-resources).)

>[!NOTE]
>
>Innan du kan kryptera ett PDF-dokument med ett certifikat måste du se till att du lägger till certifikatet i AEM Forms. Ett certifikat läggs till med administrationskonsolen eller programmatiskt med Trust Manager API. (Se [Importera autentiseringsuppgifter med Trust Manager API](/help/forms/developing/credentials.md#importing-credentials-by-using-the-trust-manager-api).)

>[!NOTE]
>
>Mer information om krypteringstjänsten finns i [Tjänstreferens för AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Sammanfattning av steg {#summary_of_steps-1}

Så här krypterar du ett PDF-dokument med ett certifikat:

1. Inkludera projektfiler.
1. Skapa ett API-objekt för krypteringsklient.
1. Få ett PDF-dokument att kryptera.
1. Referera till certifikatet.
1. Ange alternativ för kryptering vid körning.
1. Skapa ett certifikatkrypterat PDF-dokument.
1. Spara det krypterade PDF-dokumentet som en PDF-fil.

**Inkludera projektfiler**

Inkludera nödvändiga filer i utvecklingsprojektet. Om du skapar ett klientprogram med Java, inkluderar du de JAR-filer som behövs. Om du använder webbtjänster måste du inkludera proxyfilerna.

Följande JAR-filer måste läggas till i projektets klasssökväg:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-encryption-client.jar
* adobe-utilities.jar (krävs om AEM Forms körs på JBoss Application Server)
* jbossall-client.jar (krävs om AEM Forms körs på JBoss Application Server)

**Skapa ett API-objekt för krypteringsklient**

Om du vill utföra en krypteringstjänståtgärd programmatiskt måste du skapa en krypteringstjänstklient. Om du använder Java-krypteringstjänstens API skapar du en `EncrytionServiceClient` -objekt. Om du använder webbtjänstens API för krypteringstjänst skapar du en `EncryptionServiceService` -objekt.

**Få ett PDF-dokument att kryptera**

Du måste få ett okrypterat PDF-dokument för att kunna kryptera. Om du försöker skydda ett PDF-dokument som redan är krypterat genereras ett undantag.

**Referera till certifikatet**

Om du vill kryptera ett PDF-dokument med ett certifikat refererar du till ett certifikat som används för att kryptera ett PDF-dokument. Certifikatet är en .cer-fil, en .crt-fil eller en .pem-fil. En PKCS#12-fil används för att lagra privata nycklar med motsvarande certifikat.

När du krypterar ett PDF-dokument med ett certifikat anger du de behörigheter som är kopplade till det skyddade dokumentet. Genom att ange behörigheter kan du styra vilka åtgärder en användare som öppnar ett certifikatkrypterat PDF-dokument kan utföra.

**Ange alternativ för kryptering vid körning**

Ange vilka dokumentresurser i PDF som ska krypteras. Du kan kryptera hela PDF-dokumentet, allt utom dokumentets metadata eller bara dokumentets bilagor.

**Skapa ett certifikatkrypterat PDF-dokument**

När du har hämtat ett oskyddat PDF-dokument, refererat till certifikatet och angett körningsalternativ, kan du skapa ett certifikatkrypterat PDF-dokument. När PDF-dokumentet har krypterats behöver du motsvarande publika nyckel för att dekryptera det.

**Spara det krypterade PDF-dokumentet som en PDF-fil**

Du kan spara det krypterade PDF-dokumentet som en PDF-fil.

**Se även**

[Kryptera ett PDF-dokument med ett certifikat med Java API](encrypting-decrypting-pdf-documents.md#encrypt-a-pdf-document-with-a-certificate-using-the-java-api)

[Kryptera ett PDF-dokument med ett certifikat med hjälp av webbtjänstens API](encrypting-decrypting-pdf-documents.md#encrypt-a-pdf-document-with-a-certificate-using-the-web-service-api)

[Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[API-snabbstart för krypteringstjänst](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

[Kryptera PDF-dokument med ett lösenord](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)

### Kryptera ett PDF-dokument med ett certifikat med Java API {#encrypt-a-pdf-document-with-a-certificate-using-the-java-api}

Kryptera ett PDF-dokument med ett certifikat med hjälp av krypterings-API (Java):

1. Inkludera projektfiler.

   Inkludera JAR-klientfiler, t.ex. adobe-encryption-client.jar, i Java-projektets klassökväg.

1. Skapa ett API-objekt för krypteringsklient.

   * Skapa en `ServiceClientFactory` objekt som innehåller anslutningsegenskaper.
   * Skapa en `EncryptionServiceClient` genom att använda konstruktorn och skicka `ServiceClientFactory` -objekt.

1. Få ett PDF-dokument att kryptera.

   * Skapa en `java.io.FileInputStream` objekt som representerar PDF-dokumentet som ska krypteras med hjälp av konstruktorn och som skickar ett strängvärde som anger platsen för PDF-dokumentet.
   * Skapa en `com.adobe.idp.Document` genom att använda konstruktorn och skicka `java.io.FileInputStream` -objekt.

1. Referera till certifikatet.

   * Skapa en `java.util.List` objekt som lagrar behörighetsinformation med hjälp av dess konstruktor.
   * Ange behörigheten för det krypterade dokumentet genom att anropa `java.util.List` objektets `add` metod och skicka en `CertificateEncryptionPermissions` uppräkningsvärde som representerar behörigheter som beviljas den användare som öppnar det skyddade PDF-dokumentet. Om du till exempel vill ange alla behörigheter skickar du `CertificateEncryptionPermissions.PKI_ALL_PERM`.
   * Skapa en `Recipient` genom att använda dess konstruktor.
   * Skapa en `java.io.FileInputStream` objekt som representerar certifikatet som används för att kryptera PDF-dokumentet med hjälp av dess konstruktor och skicka ett strängvärde som anger platsen för certifikatet.
   * Skapa en `com.adobe.idp.Document` genom att använda konstruktorn och skicka `java.io.FileInputStream` objekt som representerar certifikatet.
   * Anropa `Recipient` objektets `setX509Cert` och skicka `com.adobe.idp.Document` som innehåller certifikatet. (Dessutom har `Recipient`-objektet kan ha ett förvaltarcertifikatalias eller en LDAP-URL som certifikatkälla.)
   * Skapa en `CertificateEncryptionIdentity` objekt som lagrar behörighet och certifikatinformation med hjälp av dess konstruktor.
   * Anropa `CertificateEncryptionIdentity` objektets `setPerms` och skicka `java.util.List` objekt som lagrar behörighetsinformation.
   * Anropa `CertificateEncryptionIdentity` objektets `setRecipient` och skicka `Recipient` objekt som lagrar certifikatinformation.
   * Skapa en `java.util.List` objekt som lagrar certifikatinformation med hjälp av dess konstruktor.
   * Anropa `java.util.List` objektets add-metod och skicka `CertificateEncryptionIdentity` -objekt. (Den `java.util.List` objektet skickas som en parameter till `encryptPDFUsingCertificates` metod.)

1. Ange alternativ för kryptering vid körning.

   * Skapa en `CertificateEncryptionOptionSpec` genom att anropa dess konstruktor.
   * Ange vilka PDF-dokumentresurser som ska krypteras genom att anropa `CertificateEncryptionOptionSpec` objektets `setOption` metod och skicka en `CertificateEncryptionOption` uppräkningsvärde som anger vilka dokumentresurser som ska krypteras. Om du till exempel vill kryptera hela PDF-dokumentet, inklusive dess metadata och bilagor, anger du `CertificateEncryptionOption.ALL`.
   * Ange kompatibilitetsalternativet för Acrobat genom att anropa `CertificateEncryptionOptionSpec` objektets `setCompat` metod och skicka en `CertificateEncryptionCompatibility` uppräkningsvärde som anger kompatibilitetsnivån för Acrobat. Du kan till exempel ange `CertificateEncryptionCompatibility.ACRO_7`.

1. Skapa ett certifikatkrypterat PDF-dokument.

   Kryptera PDF-dokumentet med ett certifikat genom att anropa `EncryptionServiceClient` objektets `encryptPDFUsingCertificates` och skicka följande värden:

   * The `com.adobe.idp.Document` som innehåller det PDF-dokument som ska krypteras.
   * The `java.util.List` objekt som lagrar certifikatinformation.
   * The `CertificateEncryptionOptionSpec` objekt som innehåller alternativ för kryptering vid körning.

   The `encryptPDFUsingCertificates` returnerar en `com.adobe.idp.Document` objekt som innehåller ett certifikatkrypterat PDF-dokument.

1. Spara det krypterade PDF-dokumentet som en PDF-fil.

   * Skapa en `java.io.File` och se till att filnamnstillägget är .pdf.
   * Anropa `com.adobe.idp.Document` objektets `copyToFile` metod för att kopiera innehållet i `com.adobe.idp.Document` till filen. Se till att du använder `com.adobe.idp.Document` objekt som returneras av `encryptPDFUsingCertificates` -metod.

**Se även**

[Sammanfattning av steg](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[Snabbstart (SOAP-läge): Kryptera ett PDF-dokument med ett certifikat med Java API](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-encrypting-a-pdf-document-with-a-certificate-using-the-java-api)

[Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Kryptera ett PDF-dokument med ett certifikat med hjälp av webbtjänstens API {#encrypt-a-pdf-document-with-a-certificate-using-the-web-service-api}

Kryptera ett PDF-dokument med ett certifikat med hjälp av krypterings-API:t (webbtjänsten):

1. Inkludera projektfiler.

   Skapa ett Microsoft .NET-projekt som använder MTOM. Kontrollera att du använder följande WSDL-definition: `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Ersätt `localhost` med IP-adressen till den server där AEM Forms finns.

1. Skapa ett API-objekt för krypteringsklient.

   * Skapa en `EncryptionServiceClient` genom att använda dess standardkonstruktor.
   * Skapa en `EncryptionServiceClient.Endpoint.Address` genom att använda `System.ServiceModel.EndpointAddress` konstruktor. Skicka ett strängvärde som anger WSDL till AEM Forms-tjänsten (till exempel `http://localhost:8080/soap/services/EncryptionService?WSDL`.) Du behöver inte använda `lc_version` -attribut. Detta attribut används när du skapar en tjänstreferens.)
   * Skapa en `System.ServiceModel.BasicHttpBinding` genom att hämta värdet för `EncryptionServiceClient.Endpoint.Binding` fält. Skicka returvärdet till `BasicHttpBinding`.
   * Ange `System.ServiceModel.BasicHttpBinding` objektets `MessageEncoding` fält till `WSMessageEncoding.Mtom`. Detta värde garanterar att MTOM används.
   * Aktivera grundläggande HTTP-autentisering genom att utföra följande åtgärder:

      * Tilldela AEM formuläranvändarnamn till fältet `EncryptionServiceClient.ClientCredentials.UserName.UserName`.
      * Tilldela motsvarande lösenordsvärde till fältet `EncryptionServiceClient.ClientCredentials.UserName.Password`.
      * Tilldela konstantvärdet `HttpClientCredentialType.Basic` till fältet `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Tilldela konstantvärdet `BasicHttpSecurityMode.TransportCredentialOnly` till fältet `BasicHttpBindingSecurity.Security.Mode`.

1. Få ett PDF-dokument att kryptera.

   * Skapa en `BLOB` genom att använda dess konstruktor. The `BLOB` används för att lagra ett PDF-dokument som är krypterat med ett certifikat.
   * Skapa en `System.IO.FileStream` genom att anropa dess konstruktor och skicka ett strängvärde som representerar filplatsen för det PDF-dokument som ska krypteras och läget i vilket filen ska öppnas.
   * Skapa en bytearray som lagrar innehållet i `System.IO.FileStream` -objekt. Du kan bestämma storleken på bytearrayen genom att hämta `System.IO.FileStream` objektets `Length` -egenskap.
   * Fylla i bytearrayen med strömdata genom att anropa `System.IO.FileStream` objektets `Read` och skickar bytearrayen, startpositionen och den flödeslängd som ska läsas.
   * Fyll i `BLOB` genom att tilldela `MTOM` med bytearrayens innehåll.

1. Referera till certifikatet.

   * Skapa en `Recipient` genom att använda dess konstruktor. Det här objektet lagrar certifikatinformation.
   * Skapa en `BLOB` genom att använda dess konstruktor. Detta `BLOB` -objektet kommer att lagra certifikatet som krypterar PDF-dokumentet.
   * Skapa en `System.IO.FileStream` genom att anropa dess konstruktor och skicka ett strängvärde som representerar certifikatets filplats och läget som filen ska öppnas i.
   * Skapa en bytearray som lagrar innehållet i `System.IO.FileStream` -objekt. Du kan bestämma storleken på bytearrayen genom att hämta `System.IO.FileStream` objektets `Length` -egenskap.
   * Fylla i bytearrayen med strömdata genom att anropa `System.IO.FileStream` objektets `Read` och skickar bytearrayen, startpositionen och den flödeslängd som ska läsas.
   * Fyll i `BLOB` genom att tilldela innehållet i bytearrayen till `BLOB` objektets `MTOM` datamedlem.
   * Tilldela `BLOB` det objekt som lagrar certifikatet till `Recipient` objektets `x509Cert` datamedlem.
   * Skapa en `CertificateEncryptionIdentity` objekt som lagrar certifikatinformation med hjälp av dess konstruktor.
   * Tilldela `Recipient` det objekt som lagrar certifikatet till `CertificateEncryptionIdentity`objektets mottagande datamedlem.
   * Skapa en `Object` arrayen och tilldela `CertificateEncryptionIdentity` -objektet till det första elementet i `Object` array. Detta `Object` arrayen skickas som en parameter till `encryptPDFUsingCertificates` -metod.

1. Ange alternativ för kryptering vid körning.

   * Skapa en `CertificateEncryptionOptionSpec` genom att använda dess konstruktor.
   * Ange vilka PDF-dokumentresurser som ska krypteras genom att tilldela en `CertificateEncryptionOption` uppräkningsvärde till `CertificateEncryptionOptionSpec` objektets `option` datamedlem. Om du vill kryptera hela PDF-dokumentet, inklusive dess metadata och bilagor, tilldelar du `CertificateEncryptionOption.ALL` till denna datamedlem.
   * Ange kompatibilitetsalternativet för Acrobat genom att tilldela en `CertificateEncryptionCompatibility` uppräkningsvärde till `CertificateEncryptionOptionSpec` objektets `compat` datamedlem. Tilldela till exempel `CertificateEncryptionCompatibility.ACRO_7` till denna datamedlem.

1. Skapa ett certifikatkrypterat PDF-dokument.

   Kryptera PDF-dokumentet med ett certifikat genom att anropa `EncryptionServiceService` objektets `encryptPDFUsingCertificates` och skicka följande värden:

   * The `BLOB` som innehåller det PDF-dokument som ska krypteras.
   * The `Object` array som lagrar certifikatinformation.
   * The `CertificateEncryptionOptionSpec` objekt som innehåller alternativ för kryptering vid körning.

   The `encryptPDFUsingCertificates` returnerar en `BLOB` objekt som innehåller ett certifikatkrypterat PDF-dokument.

1. Spara det krypterade PDF-dokumentet som en PDF-fil.

   * Skapa en `System.IO.FileStream` genom att anropa dess konstruktor och skicka ett strängvärde som representerar filplatsen för det skyddade PDF-dokumentet.
   * Skapa en bytearray som lagrar datainnehållet i `BLOB` objekt som returneras av `encryptPDFUsingCertificates` -metod. Fylla i bytearrayen genom att hämta värdet för `BLOB` objektets `binaryData` datamedlem.
   * Skapa en `System.IO.BinaryWriter` genom att anropa dess konstruktor och skicka `System.IO.FileStream` -objekt.
   * Skriv bytearrayens innehåll till en PDF-fil genom att anropa `System.IO.BinaryWriter` objektets `Write` och skicka bytearrayen.

**Se även**

[Sammanfattning av steg](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[Anropa AEM Forms med MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Anropa AEM Forms med SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Tar bort certifikatbaserad kryptering {#removing-certificate-based-encryption}

Certifikatbaserad kryptering kan tas bort från ett PDF-dokument så att användare kan öppna PDF-dokumentet i Adobe Reader eller Acrobat. Om du vill ta bort kryptering från ett PDF-dokument som är krypterat med ett certifikat måste du referera till en offentlig nyckel. När krypteringen har tagits bort från ett PDF-dokument är den inte längre säker.

>[!NOTE]
>
>Mer information om krypteringstjänsten finns i [Tjänstreferens för AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Sammanfattning av steg {#summary_of_steps-2}

Så här tar du bort certifikatbaserad kryptering från ett PDF-dokument:

1. Inkludera projektfiler.
1. Skapa en krypteringstjänstklient.
1. Hämta det krypterade PDF-dokumentet.
1. Ta bort kryptering.
1. Spara PDF-dokumentet som en PDF-fil.

**Inkludera projektfiler**

Inkludera nödvändiga filer i utvecklingsprojektet. Om du skapar ett klientprogram med Java, inkluderar du de JAR-filer som behövs. Om du använder webbtjänster måste du inkludera proxyfilerna.

Följande JAR-filer måste läggas till i projektets klasssökväg:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-encryption-client.jar
* adobe-utilities.jar (krävs om AEM Forms körs på JBoss Application Server)
* jbossall-client.jar (krävs om AEM Forms körs på JBoss Application Server)

**Skapa en krypteringstjänstklient**

Om du vill utföra en krypteringstjänståtgärd programmatiskt måste du skapa en krypteringstjänstklient. Om du använder Java-krypteringstjänstens API skapar du en `EncrytionServiceClient` -objekt. Om du använder webbtjänstens API för krypteringstjänst skapar du en `EncryptionServiceService` -objekt.

**Hämta det krypterade PDF-dokumentet**

Du måste skaffa ett krypterat PDF-dokument för att kunna ta bort certifikatbaserad kryptering. Om du försöker ta bort kryptering från ett PDF-dokument som inte är krypterat genereras ett undantag. På samma sätt inträffar ett undantag om du försöker ta bort certifikatbaserad kryptering från ett lösenordskrypterat dokument.

**Ta bort kryptering**

Om du vill ta bort certifikatbaserad kryptering från ett krypterat PDF-dokument måste du ha både ett krypterat PDF-dokument och den privata nyckel som motsvarar den nyckel som användes för att kryptera PDF-dokumentet. Aliasvärdet för den privata nyckeln anges när certifikatbaserad kryptering tas bort från ett krypterat PDF-dokument. Mer information om den offentliga nyckeln finns i [Kryptera PDF-dokument med certifikat](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-certificates).

>[!NOTE]
>
>En privat nyckel lagras i AEM Forms Trust Store. När ett certifikat placeras där anges ett aliasvärde.

**Spara PDF-dokumentet**

När certifikatbaserad kryptering har tagits bort från ett krypterat PDF-dokument kan du spara PDF-dokumentet som en PDF-fil. Användare kan öppna PDF-dokumentet i Adobe Reader eller Acrobat.

**Se även**

[Ta bort certifikatbaserad kryptering med Java API](encrypting-decrypting-pdf-documents.md#remove-certificate-based-encryption-using-the-java-api)

[Ta bort certifikatbaserad kryptering med webbtjänstens API](encrypting-decrypting-pdf-documents.md#remove-certificate-based-encryption-using-the-web-service-api)

[Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[API-snabbstart för krypteringstjänst](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

### Ta bort certifikatbaserad kryptering med Java API {#remove-certificate-based-encryption-using-the-java-api}

Ta bort certifikatbaserad kryptering från ett PDF-dokument med krypterings-API (Java):

1. Inkludera projektfiler.

   Inkludera JAR-klientfiler, t.ex. adobe-encryption-client.jar, i Java-projektets klassökväg.

1. Skapa en krypteringstjänstklient.

   * Skapa en `ServiceClientFactory` objekt som innehåller anslutningsegenskaper.
   * Skapa en `EncryptionServiceClient` genom att använda konstruktorn och skicka `ServiceClientFactory` -objekt.

1. Hämta det krypterade PDF-dokumentet.

   * Skapa en `java.io.FileInputStream` som representerar det krypterade PDF-dokumentet med hjälp av dess konstruktor och skickar ett strängvärde som anger platsen för det krypterade PDF-dokumentet.
   * Skapa en `com.adobe.idp.Document` genom att använda konstruktorn och skicka `java.io.FileInputStream` -objekt.

1. Ta bort kryptering.

   Ta bort certifikatbaserad kryptering från PDF genom att anropa `EncryptionServiceClient` objektets `removePDFCertificateSecurity` och skicka följande värden:

   * The `com.adobe.idp.Document` som innehåller det krypterade PDF-dokumentet.
   * Ett strängvärde som anger aliasnamnet för den privata nyckel som motsvarar nyckeln som används för att kryptera PDFf-dokumentet.

   The `removePDFCertificateSecurity` returnerar en `com.adobe.idp.Document` objekt som innehåller ett oskyddat PDF-dokument.

1. Spara dokumentet PDF.

   * Skapa en `java.io.File` och se till att filtillägget är .pdf.
   * Anropa `com.adobe.idp.Document` objektets `copyToFile` metod för att kopiera innehållet i `Document` till filen. Se till att du använder `com.adobe.idp.Document` objekt som returneras av `removePDFCredentialSecurity` -metod.

**Se även**

[Sammanfattning av steg](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[Snabbstart (SOAP-läge): Tar bort certifikatbaserad kryptering med Java API](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-removing-certificate-based-encryption-using-the-java-api)

[Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Ta bort certifikatbaserad kryptering med webbtjänstens API {#remove-certificate-based-encryption-using-the-web-service-api}

Ta bort certifikatbaserad kryptering med hjälp av krypterings-API:t (webbtjänsten):

1. Inkludera projektfiler.

   Skapa ett Microsoft .NET-projekt som använder MTOM. Kontrollera att du använder följande WSDL-definition: `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Ersätt `localhost` med IP-adressen till den server där AEM Forms finns.

1. Skapa en krypteringstjänstklient.

   * Skapa en `EncryptionServiceClient` genom att använda dess standardkonstruktor.
   * Skapa en `EncryptionServiceClient.Endpoint.Address` genom att använda `System.ServiceModel.EndpointAddress` konstruktor. Skicka ett strängvärde som anger WSDL till AEM Forms-tjänsten (till exempel `http://localhost:8080/soap/services/EncryptionService?WSDL`.) Du behöver inte använda `lc_version` -attribut. Detta attribut används när du skapar en tjänstreferens.)
   * Skapa en `System.ServiceModel.BasicHttpBinding` genom att hämta värdet för `EncryptionServiceClient.Endpoint.Binding` fält. Skicka returvärdet till `BasicHttpBinding`.
   * Ange `System.ServiceModel.BasicHttpBinding` objektets `MessageEncoding` fält till `WSMessageEncoding.Mtom`. Detta värde garanterar att MTOM används.
   * Aktivera grundläggande HTTP-autentisering genom att utföra följande åtgärder:

      * Tilldela AEM formuläranvändarnamn till fältet `EncryptionServiceClient.ClientCredentials.UserName.UserName`.
      * Tilldela motsvarande lösenordsvärde till fältet `EncryptionServiceClient.ClientCredentials.UserName.Password`.
      * Tilldela konstantvärdet `HttpClientCredentialType.Basic` till fältet `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Tilldela konstantvärdet `BasicHttpSecurityMode.TransportCredentialOnly` till fältet `BasicHttpBindingSecurity.Security.Mode`.

1. Hämta det krypterade PDF-dokumentet.

   * Skapa en `BLOB` genom att använda dess konstruktor. The `BLOB` -objektet används för att lagra det krypterade PDF-dokumentet.
   * Skapa en `System.IO.FileStream` genom att anropa dess konstruktor och skicka ett strängvärde som representerar filplatsen för det krypterade PDF-dokumentet och läget som filen ska öppnas i.
   * Skapa en bytearray som lagrar innehållet i `System.IO.FileStream` -objekt. Du kan bestämma storleken på bytearrayen genom att hämta `System.IO.FileStream` objektets `Length` -egenskap.
   * Fylla i bytearrayen med strömdata genom att anropa `System.IO.FileStream` objektets `Read` och skickar bytearrayen, startpositionen och den flödeslängd som ska läsas.
   * Fyll i `BLOB` genom att tilldela innehållet i bytearrayen till `BLOB` objektets `MTOM` datamedlem.

1. Ta bort kryptering.

   Anropa `EncryptionServiceClient` objektets `removePDFCertificateSecurity` och skicka följande värden:

   * The `BLOB` -objekt som innehåller filströmsdata som representerar ett krypterat PDF-dokument.
   * Ett strängvärde som anger aliasnamnet för den offentliga nyckeln som motsvarar den privata nyckel som används för att kryptera PDFf-dokumentet.

   The `removePDFCredentialSecurity` returnerar en `BLOB` objekt som innehåller ett oskyddat PDF-dokument.

1. Spara dokumentet PDF.

   * Skapa en `System.IO.FileStream` genom att anropa dess konstruktor och skicka ett strängvärde som representerar filplatsen för det oskyddade PDF-dokumentet.
   * Skapa en bytearray som lagrar innehållet i `BLOB` objekt som returneras av `removePDFPasswordSecurity` -metod. Fylla i bytearrayen genom att hämta värdet för `BLOB` objektets `MTOM` datamedlem.
   * Skapa en `System.IO.BinaryWriter` genom att anropa dess konstruktor och skicka `System.IO.FileStream` -objekt.
   * Skriv bytearrayens innehåll till en PDF-fil genom att anropa `System.IO.BinaryWriter` objektets `Write` och skicka bytearrayen.

**Se även**

[Sammanfattning av steg](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[Anropa AEM Forms med MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Anropa AEM Forms med SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Tar bort lösenordskryptering {#removing-password-encryption}

Lösenordsbaserad kryptering kan tas bort från ett PDF-dokument så att användare kan öppna PDF-dokumentet i Adobe Reader eller Acrobat utan att behöva ange något lösenord. När lösenordsbaserad kryptering har tagits bort från ett PDF-dokument är dokumentet inte längre säkert.

>[!NOTE]
>
>Mer information om krypteringstjänsten finns i [Tjänstreferens för AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Sammanfattning av steg {#summary_of_steps-3}

Så här tar du bort lösenordsbaserad kryptering från ett PDF-dokument:

1. Inkludera projektfiler
1. Skapa en krypteringstjänstklient.
1. Hämta det krypterade PDF-dokumentet.
1. Ta bort lösenordet.
1. Spara PDF-dokumentet som en PDF-fil.

**Inkludera projektfiler**

Inkludera nödvändiga filer i utvecklingsprojektet. Om du skapar ett klientprogram med Java, inkluderar du de JAR-filer som behövs. Om du använder webbtjänster måste du ta med proxyfilerna.

Följande JAR-filer måste läggas till i projektets klasssökväg:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-encryption-client.jar
* adobe-utilities.jar (krävs om AEM Forms används i JBoss)
* jbossall-client.jar (krävs om AEM Forms används i JBoss)

**Skapa en krypteringstjänstklient**

Om du vill utföra en krypteringstjänståtgärd programmatiskt måste du skapa en krypteringstjänstklient. Om du använder Java-krypteringstjänstens API skapar du en `EncrytionServiceClient` -objekt. Om du använder webbtjänstens API för krypteringstjänst skapar du en `EncryptionServiceService` -objekt.

**Hämta det krypterade PDF-dokumentet**

Du måste få ett krypterat PDF-dokument för att kunna ta bort lösenordsbaserad kryptering. Om du försöker ta bort kryptering från ett PDF-dokument som inte är krypterat genereras ett undantag.

**Ta bort lösenordet**

Om du vill ta bort lösenordsbaserad kryptering från ett krypterat PDF-dokument måste du ha både ett krypterat PDF-dokument och ett huvudlösenordsvärde som används för att ta bort kryptering från PDF-dokumentet. Lösenordet som används för att öppna ett lösenordskrypterat PDF-dokument kan inte användas för att ta bort kryptering. Ett huvudlösenord anges när PDF-dokumentet krypteras med ett lösenord. (Se [Kryptera PDF-dokument med ett lösenord](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password).)

**Spara PDF-dokumentet**

När krypteringstjänsten har tagit bort lösenordsbaserad kryptering från ett PDF-dokument kan du spara PDF-dokumentet som en PDF-fil. Användare kan öppna PDF-dokumentet i Adobe Reader eller Acrobat utan att ange ett lösenord.

**Se även**

[Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[API-snabbstart för krypteringstjänst](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

[Kryptera PDF-dokument med ett lösenord](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)

### Ta bort lösenordsbaserad kryptering med Java API {#remove-password-based-encryption-using-the-java-api}

Ta bort lösenordsbaserad kryptering från ett PDF-dokument med krypterings-API (Java):

1. Inkludera projektfiler.

   Inkludera JAR-klientfiler, till exempel adobe-encryption-client.jar, i Java-projektets klassökväg.

1. Skapa en krypteringstjänstklient.

   * Skapa en `ServiceClientFactory` objekt som innehåller anslutningsegenskaper.
   * Skapa en `EncryptionServiceClient` genom att använda konstruktorn och skicka `ServiceClientFactory` -objekt.

1. Hämta det krypterade PDF-dokumentet.

   * Skapa en `java.io.FileInputStream` objekt som representerar det krypterade PDF-dokumentet med hjälp av dess konstruktor och som skickar ett strängvärde som anger platsen för PDF-dokumentet.
   * Skapa en `com.adobe.idp.Document` genom att använda konstruktorn och skicka `java.io.FileInputStream` -objekt.

1. Ta bort lösenordet.

   Ta bort lösenordsbaserad kryptering från PDF-dokumentet genom att anropa `EncryptionServiceClient` objektets `removePDFPasswordSecurity` och skicka följande värden:

   * A `com.adobe.idp.Document` som innehåller det krypterade PDF-dokumentet.
   * Ett strängvärde som anger det huvudlösenordsvärde som används för att ta bort kryptering från PDF-dokumentet.

   The `removePDFPasswordSecurity` returnerar en `com.adobe.idp.Document` objekt som innehåller ett oskyddat PDF-dokument.

1. Spara dokumentet PDF.

   * Skapa en `java.io.File` och se till att filnamnstillägget är .pdf.
   * Anropa `com.adobe.idp.Document` objektets `copyToFile` metod för att kopiera innehållet i `Document` till filen. Se till att du använder `Document` objekt som returneras av `removePDFPasswordSecurity` -metod.

**Se även**

[Snabbstart (SOAP-läge): Ta bort lösenordsbaserad kryptering med Java API](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-removing-password-based-encryption-using-the-java-api)

### Ta bort lösenordsbaserad kryptering med webbtjänstens API {#remove-password-based-encryption-using-the-web-service-api}

Ta bort lösenordsbaserad kryptering med hjälp av krypterings-API:t (webbtjänsten):

1. Inkludera projektfiler.

   Skapa ett Microsoft .NET-projekt som använder MTOM. Kontrollera att du använder följande WSDL-definition: `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Ersätt `localhost` med IP-adressen till den server där AEM Forms finns.

1. Skapa en krypteringstjänstklient.

   * Skapa en `EncryptionServiceClient` genom att använda dess standardkonstruktor.
   * Skapa en `EncryptionServiceClient.Endpoint.Address` genom att använda `System.ServiceModel.EndpointAddress` konstruktor. Skicka ett strängvärde som anger WSDL till AEM Forms-tjänsten (till exempel `http://localhost:8080/soap/services/EncryptionService?WSDL`.) Du behöver inte använda `lc_version` -attribut. Detta attribut används när du skapar en tjänstreferens.)
   * Skapa en `System.ServiceModel.BasicHttpBinding` genom att hämta värdet för `EncryptionServiceClient.Endpoint.Binding` fält. Skicka returvärdet till `BasicHttpBinding`.
   * Ange `System.ServiceModel.BasicHttpBinding` objektets `MessageEncoding` fält till `WSMessageEncoding.Mtom`. Detta värde garanterar att MTOM används.
   * Aktivera grundläggande HTTP-autentisering genom att utföra följande åtgärder:

      * Tilldela AEM formuläranvändarnamn till fältet `EncryptionServiceClient.ClientCredentials.UserName.UserName`.
      * Tilldela motsvarande lösenordsvärde till fältet `EncryptionServiceClient.ClientCredentials.UserName.Password`.
      * Tilldela konstantvärdet `HttpClientCredentialType.Basic` till fältet `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Tilldela konstantvärdet `BasicHttpSecurityMode.TransportCredentialOnly` till fältet `BasicHttpBindingSecurity.Security.Mode`.

1. Hämta det krypterade PDF-dokumentet.

   * Skapa en `BLOB` genom att använda dess konstruktor. The `BLOB` används för att lagra ett lösenordskrypterat PDF-dokument.
   * Skapa en `System.IO.FileStream` genom att anropa dess konstruktor och skicka ett strängvärde som representerar filplatsen för det krypterade PDF-dokumentet och läget som filen ska öppnas i.
   * Skapa en bytearray som lagrar innehållet i `System.IO.FileStream` -objekt. Du kan bestämma storleken på bytearrayen genom att hämta `System.IO.FileStream` objektets `Length` -egenskap.
   * Fylla i bytearrayen med strömdata genom att anropa `System.IO.FileStream` objektets `Read` och skickar bytearrayen, startpositionen och den flödeslängd som ska läsas.
   * Fyll i `BLOB` genom att tilldela innehållet i bytearrayen till `BLOB` objektets `MTOM` datamedlem.

1. Ta bort lösenordet.

   Anropa `EncryptionServiceService` objektets `removePDFPasswordSecurity` och skicka följande värden:

   * The `BLOB` -objekt som innehåller filströmsdata som representerar ett krypterat PDF-dokument.
   * Ett strängvärde som anger det lösenordsvärde som används för att ta bort kryptering från PDF-dokumentet. Det här värdet anges när du krypterar PDF-dokumentet med ett lösenord.

   The `removePDFPasswordSecurity` returnerar en `BLOB` objekt som innehåller ett oskyddat PDF-dokument.

1. Spara dokumentet PDF.

   * Skapa en `System.IO.FileStream` genom att anropa dess konstruktor och skicka ett strängvärde som representerar filplatsen för det oskyddade PDF-dokumentet.
   * Skapa en bytearray som lagrar innehållet i `BLOB` objekt som returneras av `removePDFPasswordSecurity` -metod. Fylla i bytearrayen genom att hämta värdet för `BLOB` objektets `MTOM` datamedlem.
   * Skapa en `System.IO.BinaryWriter` genom att anropa dess konstruktor och skicka `System.IO.FileStream` -objekt.
   * Skriv bytearrayens innehåll till en PDF-fil genom att anropa `System.IO.BinaryWriter` objektets `Write` och skicka bytearrayen.

**Se även**

[Anropa AEM Forms med MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Anropa AEM Forms med SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Låsa upp krypterade PDF-dokument {#unlocking-encrypted-pdf-documents}

Ett lösenordskrypterat eller certifikatkrypterat PDF-dokument måste låsas upp innan en annan AEM Forms-åtgärd kan utföras på det. Om du försöker utföra en åtgärd på ett krypterat PDF-dokument genereras ett undantag. När du har låst upp ett krypterat PDF-dokument kan du utföra en eller flera åtgärder på det. De här åtgärderna kan tillhöra andra tjänster, t.ex. Acrobat Reader DC-tilläggstjänsten.

>[!NOTE]
>
>Mer information om krypteringstjänsten finns i [Tjänstreferens för AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Sammanfattning av steg {#summary_of_steps-4}

Så här låser du upp ett krypterat PDF-dokument:

1. Inkludera projektfiler.
1. Skapa en krypteringstjänstklient.
1. Hämta det krypterade PDF-dokumentet.
1. Lås upp dokumentet.
1. Utför en AEM Forms-åtgärd.

**Inkludera projektfiler**

Inkludera nödvändiga filer i utvecklingsprojektet. Om du skapar ett klientprogram med Java, inkluderar du de JAR-filer som behövs. Om du använder webbtjänster måste du ta med proxyfilerna.

Följande JAR-filer måste läggas till i projektets klasssökväg:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-encryption-client.jar
* adobe-utilities.jar (krävs om AEM Forms körs på JBoss Application Server)
* jbossall-client.jar (krävs om AEM Forms körs på JBoss Application Server)

**Skapa en krypteringstjänstklient**

Om du vill utföra en krypteringstjänståtgärd programmatiskt måste du skapa en krypteringstjänstklient. Om du använder Java-krypteringstjänstens API skapar du en `EncrytionServiceClient` -objekt. Om du använder webbtjänstens API för krypteringstjänst skapar du en `EncryptionServiceService` -objekt.

**Hämta det krypterade PDF-dokumentet**

Du måste skaffa ett krypterat PDF-dokument för att kunna låsa upp det. Om du försöker låsa upp ett PDF-dokument som inte är krypterat genereras ett undantag.

**Lås upp dokumentet**

Om du vill låsa upp ett lösenordskrypterat PDF-dokument måste du ha både ett krypterat PDF-dokument och ett lösenordsvärde som används för att öppna ett lösenordskrypterat PDF-dokument. Det här värdet anges när du krypterar PDF-dokumentet med ett lösenord. (Se [Kryptera PDF-dokument med ett lösenord](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password).)

Om du vill låsa upp ett certifikatkrypterat PDF-dokument måste du ha både ett krypterat PDF-dokument och aliasvärdet för den offentliga nyckeln som motsvarar den privata nyckel som användes för att kryptera PDF-dokumentet.

**Utför en AEM Forms-åtgärd**

När ett krypterat PDF-dokument har låsts upp kan du utföra en annan tjänståtgärd på det, t.ex. tillämpa användarbehörighet på det. Den här åtgärden tillhör tjänsten Acrobat Reader DC Extensions.

**Se även**

[Lås upp ett krypterat PDF-dokument med Java API](encrypting-decrypting-pdf-documents.md#unlock-an-encrypted-pdf-document-using-the-java-api)

[Lås upp ett krypterat PDF-dokument med hjälp av webbtjänstens API](encrypting-decrypting-pdf-documents.md#unlock-an-encrypted-pdf-document-using-the-web-service-api)

[Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[API-snabbstart för krypteringstjänst](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

### Lås upp ett krypterat PDF-dokument med Java API {#unlock-an-encrypted-pdf-document-using-the-java-api}

Lås upp ett krypterat PDF-dokument med hjälp av krypterings-API (Java):

1. Inkludera projektfiler.

   Inkludera JAR-klientfiler, t.ex. adobe-encryption-client.jar, i Java-projektets klassökväg.

1. Skapa en krypteringstjänstklient.

   * Skapa en `ServiceClientFactory` objekt som innehåller anslutningsegenskaper.
   * Skapa en `EncryptionServiceClient` genom att använda konstruktorn och skicka `ServiceClientFactory` -objekt.

1. Hämta det krypterade PDF-dokumentet.

   * Skapa en `java.io.FileInputStream` som representerar det krypterade PDF-dokumentet med hjälp av dess konstruktor och skickar ett strängvärde som anger platsen för det krypterade PDF-dokumentet.
   * Skapa en `com.adobe.idp.Document` genom att använda konstruktorn och skicka `java.io.FileInputStream` -objekt.

1. Lås upp dokumentet.

   Lås upp ett krypterat PDF-dokument genom att anropa `EncryptionServiceClient` objektets `unlockPDFUsingPassword` eller `unlockPDFUsingCredential` -metod.

   Om du vill låsa upp ett PDF-dokument som är krypterat med ett lösenord anropar du `unlockPDFUsingPassword` och skicka följande värden:

   * A `com.adobe.idp.Document` som innehåller det lösenordskrypterade PDF-dokumentet.
   * Ett strängvärde som anger det lösenordsvärde som används för att öppna ett lösenordskrypterat PDF-dokument. Det här värdet anges när du krypterar PDF-dokumentet med ett lösenord.

   Om du vill låsa upp ett PDF-dokument som är krypterat med ett certifikat anropar du `unlockPDFUsingCredential` och skicka följande värden:

   * A `com.adobe.idp.Document` som innehåller det certifikatkrypterade PDF-dokumentet.
   * Ett strängvärde som anger aliasnamnet för den offentliga nyckeln som motsvarar den privata nyckel som används för att kryptera PDF-dokumentet.

   The `unlockPDFUsingPassword` och `unlockPDFUsingCredential` metoderna returnerar båda `com.adobe.idp.Document` objekt som du skickar till en annan AEM Forms Java-metod för att utföra en åtgärd.

1. Utför en AEM Forms-åtgärd.

   Utför en AEM Forms-åtgärd på det olåsta PDF-dokumentet för att uppfylla dina affärskrav. Om du t.ex. vill använda användarrättigheter för ett olåst PDF-dokument skickar du `com.adobe.idp.Document` objekt som returneras av antingen `unlockPDFUsingPassword` eller `unlockPDFUsingCredential` metoder till `ReaderExtensionsServiceClient` objektets `applyUsageRights` -metod.

**Se även**

[Sammanfattning av steg](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[Snabbstart (SOAP-läge): Låsa upp ett krypterat PDF-dokument med Java API](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-unlocking-an-encrypted-pdf-document-using-the-java-api) (SOAP-läge)

[Använda användningsbehörighet för PDF-dokument](/help/forms/developing/assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)

[Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Lås upp ett krypterat PDF-dokument med hjälp av webbtjänstens API {#unlock-an-encrypted-pdf-document-using-the-web-service-api}

Lås upp ett krypterat PDF-dokument med hjälp av krypterings-API:t (webbtjänsten):

1. Inkludera projektfiler.

   Skapa ett Microsoft .NET-projekt som använder MTOM. Kontrollera att du använder följande WSDL-definition: `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Ersätt `localhost` med IP-adressen till den server där AEM Forms finns.

1. Skapa en krypteringstjänstklient.

   * Skapa en `EncryptionServiceClient` genom att använda dess standardkonstruktor.
   * Skapa en `EncryptionServiceClient.Endpoint.Address` genom att använda `System.ServiceModel.EndpointAddress` konstruktor. Skicka ett strängvärde som anger WSDL till AEM Forms-tjänsten (till exempel `http://localhost:8080/soap/services/EncryptionService?WSDL`.) Du behöver inte använda `lc_version` -attribut. Detta attribut används när du skapar en tjänstreferens.)
   * Skapa en `System.ServiceModel.BasicHttpBinding` genom att hämta värdet för `EncryptionServiceClient.Endpoint.Binding` fält. Skicka returvärdet till `BasicHttpBinding`.
   * Ange `System.ServiceModel.BasicHttpBinding` objektets `MessageEncoding` fält till `WSMessageEncoding.Mtom`. Detta värde garanterar att MTOM används.
   * Aktivera grundläggande HTTP-autentisering genom att utföra följande åtgärder:

      * Tilldela AEM formuläranvändarnamn till fältet `EncryptionServiceClient.ClientCredentials.UserName.UserName`.
      * Tilldela motsvarande lösenordsvärde till fältet `EncryptionServiceClient.ClientCredentials.UserName.Password`.
      * Tilldela konstantvärdet `HttpClientCredentialType.Basic` till fältet `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Tilldela konstantvärdet `BasicHttpSecurityMode.TransportCredentialOnly` till fältet `BasicHttpBindingSecurity.Security.Mode`.

1. Få ett krypterat PDF-dokument.

   * Skapa en `BLOB` genom att använda dess konstruktor.
   * Skapa en `System.IO.FileStream` genom att anropa dess konstruktor och skicka ett strängvärde som representerar filplatsen för det krypterade PDF-dokumentet och läget som filen ska öppnas i.
   * Skapa en bytearray som lagrar innehållet i `System.IO.FileStream` -objekt. Du kan bestämma storleken på bytearrayen genom att hämta `System.IO.FileStream` objektets `Length` -egenskap.
   * Fylla i bytearrayen med strömdata genom att anropa `System.IO.FileStream` objektets `Read` och skickar bytearrayen, startpositionen och den flödeslängd som ska läsas.
   * Fyll i `BLOB` genom att tilldela innehållet i bytearrayen till `BLOB` objektets `MTOM` datamedlem.

1. Lås upp dokumentet.

   Lås upp ett krypterat PDF-dokument genom att anropa `EncryptionServiceClient` objektets `unlockPDFUsingPassword` eller `unlockPDFUsingCredential` -metod.

   Om du vill låsa upp ett PDF-dokument som är krypterat med ett lösenord anropar du `unlockPDFUsingPassword` och skicka följande värden:

   * A `BLOB` som innehåller det lösenordskrypterade PDF-dokumentet.
   * Ett strängvärde som anger det lösenordsvärde som används för att öppna ett lösenordskrypterat PDF-dokument. Det här värdet anges när du krypterar PDF-dokumentet med ett lösenord.

   Om du vill låsa upp ett PDF-dokument som är krypterat med ett certifikat anropar du `unlockPDFUsingCredential` och skicka följande värden:

   * A `BLOB` som innehåller det certifikatkrypterade PDF-dokumentet.
   * Ett strängvärde som anger aliasnamnet för den offentliga nyckeln som motsvarar den privata nyckel som används för att kryptera PDFf-dokumentet.

   The `unlockPDFUsingPassword` och `unlockPDFUsingCredential` metoderna returnerar båda `com.adobe.idp.Document` objekt som du skickar till en annan AEM Forms-metod för att utföra en åtgärd.

1. Utför en AEM Forms-åtgärd.

   Utför en AEM Forms-åtgärd på det olåsta PDF-dokumentet för att uppfylla dina affärskrav. Om du t.ex. vill lägga till användarrättigheter i det olåsta PDF-dokumentet skickar du `BLOB` objekt som returneras av antingen `unlockPDFUsingPassword` eller `unlockPDFUsingCredential` metoder till `ReaderExtensionsServiceClient` objektets `applyUsageRights` -metod.

**Se även**

[Sammanfattning av steg](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[Anropa AEM Forms med MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Anropa AEM Forms med SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Bestämmer krypteringstyp {#determining-encryption-type}

Du kan programmässigt avgöra vilken typ av kryptering som skyddar ett PDF-dokument med hjälp av Java-krypteringstjänstens API eller webbtjänstens krypteringstjänsts API. Ibland är det nödvändigt att dynamiskt avgöra om ett PDF-dokument är krypterat och i så fall krypteringstypen. Du kan t.ex. ange om ett PDF-dokument är lösenordsbaserat eller om en Rights Management-profil ska användas.

Ett PDF-dokument kan skyddas med följande krypteringstyper:

* Lösenordsbaserad kryptering
* Certifikatbaserad kryptering
* En policy som skapas av tjänsten Rights Management
* En annan typ av kryptering

>[!NOTE]
>
>Mer information om krypteringstjänsten finns i [Tjänstreferens för AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Sammanfattning av steg {#summary_of_steps-5}

Så här avgör du vilken typ av kryptering som skyddar ett PDF-dokument:

1. Inkludera projektfiler.
1. Skapa en krypteringstjänstklient.
1. Hämta det krypterade PDF-dokumentet.
1. Bestäm krypteringstypen.

**Inkludera projektfiler**

Inkludera nödvändiga filer i utvecklingsprojektet. Om du skapar ett klientprogram med Java, inkluderar du de JAR-filer som behövs. Om du använder webbtjänster måste du inkludera proxyfilerna.

Följande JAR-filer måste läggas till i projektets klasssökväg:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-encryption-client.jar
* adobe-utilities.jar (krävs om AEM Forms körs på JBoss Application Server)
* jbossall-client.jar (krävs om AEM Forms körs på JBoss Application Server)

**Skapa en tjänstklient**

Om du vill utföra en krypteringstjänståtgärd programmatiskt måste du skapa en krypteringstjänstklient. Om du använder Java-krypteringstjänstens API skapar du en `EncrytionServiceClient` -objekt. Om du använder webbtjänstens API för krypteringstjänst skapar du en `EncryptionServiceService` -objekt.

**Hämta det krypterade PDF-dokumentet**

Du måste skaffa ett PDF-dokument för att kunna avgöra vilken typ av kryptering som skyddar det.

**Bestämma krypteringstypen**

Du kan ange vilken typ av kryptering som skyddar ett PDF-dokument. Om dokumentet från PDF inte är skyddat visas ett meddelande om att dokumentet från PDF inte är skyddat av krypteringstjänsten.

**Se även**

[Identifiera krypteringstypen med Java API](encrypting-decrypting-pdf-documents.md#determine-the-encryption-type-using-the-java-api)

[Identifiera krypteringstypen med hjälp av webbtjänstens API](encrypting-decrypting-pdf-documents.md#determine-the-encryption-type-using-the-web-service-api)

[Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[API-snabbstart för krypteringstjänst](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

[Skydda dokument med regler](/help/forms/developing/protecting-documents-policies.md#protecting-documents-with-policies)

### Identifiera krypteringstypen med Java API {#determine-the-encryption-type-using-the-java-api}

Bestäm vilken typ av kryptering som skyddar ett PDF-dokument med hjälp av krypterings-API (Java):

1. Inkludera projektfiler.

   Inkludera JAR-klientfiler, t.ex. adobe-encryption-client.jar, i Java-projektets klassökväg.

1. Skapa en tjänstklient.

   * Skapa en `ServiceClientFactory` objekt som innehåller anslutningsegenskaper.
   * Skapa en `EncryptionServiceClient` genom att använda konstruktorn och skicka `ServiceClientFactory` -objekt.

1. Hämta det krypterade PDF-dokumentet.

   * Skapa en `java.io.FileInputStream` objekt som representerar PDF-dokumentet genom att använda dess konstruktor och skicka ett strängvärde som anger platsen för PDF-dokumentet.
   * Skapa en `com.adobe.idp.Document` genom att använda konstruktorn och skicka `java.io.FileInputStream` -objekt.

1. Bestäm krypteringstypen.

   * Kontrollera krypteringstypen genom att anropa `EncryptionServiceClient` objektets `getPDFEncryption` metoden och skicka `com.adobe.idp.Document` -objekt som innehåller dokumentet PDF. Den här metoden returnerar en `EncryptionTypeResult` -objekt.
   * Anropa `EncryptionTypeResult` objektets `getEncryptionType` -metod. Den här metoden returnerar en `EncryptionType` enum-värde som anger krypteringstypen. Om PDF-dokumentet till exempel skyddas med lösenordsbaserad kryptering returnerar den här metoden `EncryptionType.PASSWORD`.

**Se även**

[Sammanfattning av steg](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[Snabbstart (SOAP-läge): Bestämma krypteringstyp med Java API](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-determining-encryption-type-using-the-java-api)

[Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Identifiera krypteringstypen med hjälp av webbtjänstens API {#determine-the-encryption-type-using-the-web-service-api}

Bestäm vilken typ av kryptering som skyddar ett PDF-dokument med hjälp av krypterings-API:t (webbtjänsten):

1. Inkludera projektfiler.

   Skapa ett Microsoft .NET-projekt som använder MTOM. Kontrollera att du använder följande WSDL-definition: `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Ersätt `localhost` med IP-adressen till den server där AEM Forms finns.

1. Skapa en tjänstklient.

   * Skapa en `EncryptionServiceClient` genom att använda dess standardkonstruktor.
   * Skapa en `EncryptionServiceClient.Endpoint.Address` genom att använda `System.ServiceModel.EndpointAddress` konstruktor. Skicka ett strängvärde som anger WSDL till AEM Forms-tjänsten (till exempel `http://localhost:8080/soap/services/EncryptionService?WSDL`.) Du behöver inte använda `lc_version` -attribut. Detta attribut används när du skapar en tjänstreferens.)
   * Skapa en `System.ServiceModel.BasicHttpBinding` genom att hämta värdet för `EncryptionServiceClient.Endpoint.Binding` fält. Skicka returvärdet till `BasicHttpBinding`.
   * Ange `System.ServiceModel.BasicHttpBinding` objektets `MessageEncoding` fält till `WSMessageEncoding.Mtom`. Detta värde garanterar att MTOM används.
   * Aktivera grundläggande HTTP-autentisering genom att utföra följande åtgärder:

      * Tilldela AEM formuläranvändarnamn till fältet `EncryptionServiceClient.ClientCredentials.UserName.UserName`.
      * Tilldela motsvarande lösenordsvärde till fältet `EncryptionServiceClient.ClientCredentials.UserName.Password`.
      * Tilldela konstantvärdet `HttpClientCredentialType.Basic` till fältet `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Tilldela konstantvärdet `BasicHttpSecurityMode.TransportCredentialOnly` till fältet `BasicHttpBindingSecurity.Security.Mode`.

1. Hämta det krypterade PDF-dokumentet.

   * Skapa en `BLOB` genom att använda dess konstruktor.
   * Skapa en `System.IO.FileStream` genom att anropa dess konstruktor och skicka ett strängvärde som representerar filplatsen för det krypterade PDF-dokumentet och läget som filen ska öppnas i.
   * Skapa en bytearray som lagrar innehållet i `System.IO.FileStream` -objekt. Du kan bestämma storleken på bytearrayen genom att hämta `System.IO.FileStream` objektets `Length` -egenskap.
   * Fylla i bytearrayen med strömdata genom att anropa `System.IO.FileStream` objektets `Read` och skickar bytearrayen, startpositionen och den flödeslängd som ska läsas.
   * Fyll i `BLOB` genom att tilldela innehållet i bytearrayen till `BLOB` objektets `MTOM` datamedlem.

1. Bestäm krypteringstypen.

   * Anropa `EncryptionServiceClient` objektets `getPDFEncryption` och skicka `BLOB` -objekt som innehåller dokumentet PDF. Den här metoden returnerar en `EncryptionTypeResult` -objekt.
   * Hämta värdet för `EncryptionTypeResult` objektets `encryptionType` datametod. Om PDF-dokumentet till exempel skyddas med lösenordsbaserad kryptering är värdet för den här datamedlemmen `EncryptionType.PASSWORD`.

**Se även**

[Sammanfattning av steg](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[Anropa AEM Forms med MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Anropa AEM Forms med SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
