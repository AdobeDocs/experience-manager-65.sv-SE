---
title: Använd HSM för att digitalt signera eller certifiera dokument
seo-title: Använd HSM för att certifiera e-signerade dokument
description: Använd HSM- eller tokenenheter för att certifiera e-signerade dokument
seo-description: Använd HSM- eller tokenenheter för att certifiera e-signerade dokument
uuid: bbe057c1-6150-41f9-9c82-4979d31d305d
contentOwner: vishgupt
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: document_services
discoiquuid: 536bcba4-b754-4799-b0d2-88960cc4c44a
translation-type: tm+mt
source-git-commit: 94472fad34fe97740e4711d2cb35beb884db52ce

---


# Använd HSM för att digitalt signera eller certifiera dokument {#use-hsm-to-digitally-sign-or-certify-documents}

HSM-moduler (Hardware Security Modules) och -telefoner är dedikerade, härdade och manipuleringssäkra datorenheter som är utformade för att hantera, bearbeta och lagra digitala nycklar på ett säkert sätt. Dessa enheter är direktanslutna till en dator eller en nätverksserver.

Adobe Experience Manager Forms kan använda inloggningsuppgifter som lagras på en HSM eller token för att e-signera eller använda serverbaserade digitala signaturer i ett dokument. Så här använder du en HSM- eller tokenenhet med AEM Forms:

1. Aktivera tjänsten DocAssurance.
1. Konfigurera certifikat för Reader-tillägg.
1. Skapa ett alias för HSM- eller tokenenheten i AEM Web Console.
1. Använd API:erna för DocAssurance-tjänsten för att signera eller certifiera dokument med digitala nycklar lagrade på enheten.

## Innan du konfigurerar HSM- eller tokenenheter med AEM Forms {#configurehsmetoken}

* Installera tilläggspaketet [för](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html) AEM Forms.
* Installera och konfigurera HSM- eller tokenklientprogramvara på samma dator som AEM-servern. Klientprogramvaran krävs för att kommunicera med HSM- och tokenenheterna.
* (Endast Microsoft Windows) Ställ in miljövariabeln JAVA_HOME_32 så att den pekar på den katalog där 32-bitarsversionen av Java 8 Development Kit (JDK 8) är installerad. Standardsökvägen för katalogen är C:\Program Files(x86)\Java\jdk&lt;version>
* (Endast AEM Forms på OSGi) Installera rotcertifikatet i förtroendearkivet. Du måste verifiera den signerade PDF-filen

>[!NOTE]
>
>I Microsoft Windows stöds endast 32-bitars LunaSA- eller EToken-klienter.

## Aktivera tjänsten DocAssurance {#configuredocassurance}

Tjänsten DocAssurance är inte aktiverad som standard. Aktivera tjänsten genom att utföra följande steg:

1. Stoppa författarinstansen av AEM Forms-miljön.

1. Öppna filen [AEM_root]\crx-quickstart\conf\sling.properties för redigering.

   >[!NOTE]
   >
   >Om du har använt [AEM_root]\crx-quickstart\bin\start.bat för att starta AEM-instansen öppnar du [AEM_root]\crx-quickstart\sling.properties för redigering.

1. Lägg till eller ersätt följande egenskaper i sling.properties-filen:

   ```shell
   sling.bootdelegation.sun=sun.*,com.sun.*,sun.misc.*
   sling.bootdelegation.ibm=com.ibm.xml.*,com.ibm.*
   sling.bootdelegation.class.com.rsa.jsafe.provider.JsafeJCE=com.rsa.*
   sling.bootdelegation.class.org.bouncycastle.jce.provider.BouncyCastleProvider=org.bouncycastle.*
   ```

1. Spara och stäng filen sling.properties.
1. Starta om AEM-instansen.

## Konfigurera certifikat för Reader-tillägg {#set-up-certificates-for-reader-extensions}

Utför följande steg för att konfigurera certifikat:

1. Logga in på AEM Author-instansen som administratör.

1. **Klicka på Adobe Experience Manager** i det globala navigeringsfältet. Gå till **Verktyg** > **Dokumentskydd** > **Användare**.
1. Klicka på användarkontots **namnfält** . Sidan **Redigera användarinställningar** öppnas.
1. På AEM Author-instansen finns certifikat i KeyStore. Om du inte har skapat en KeyStore tidigare klickar du på **Create KeyStore** och anger ett nytt lösenord för KeyStore. Om servern redan innehåller en KeyStore hoppar du över det här steget.

1. På sidan **Redigera användarinställningar** klickar du på **Hantera KeyStore**.

1. Expandera alternativet **Lägg till privat nyckel från nyckelarkivfilen** och ange ett alias i dialogrutan KeyStore-hantering. Aliaset används för att utföra Reader Extensions-åtgärden.
1. Om du vill överföra certifikatfilen klickar du på **Välj nyckelarkivfil** och överför en `.pfx` fil.
1. Lägg till lösenordet **för** nyckelarkivet, lösenordet **för** den privata nyckeln och det alias **för den** privata nyckeln som är kopplat till certifikatet i respektive fält. Klicka på **Skicka**.

   >[!NOTE]
   >
   >Du kan använda kommandot Java-nyckelverktyg för att fastställa **alias** för privat nyckel för ett certifikat: `keytool -list -v -keystore [keystore-file] -storetype pkcs12`

   >[!NOTE]
   >
   >I fälten Lösenord **för** nyckelarkiv och Lösenord **för** privat nyckel anger du lösenordet som medföljde certifikatfilen.

>[!NOTE]
>
>För AEM Forms på OSGi, för att verifiera den signerade PDF-filen, är rotcertifikatet som är installerat i Trust Store.

>[!NOTE]
>
>När du går över till produktionsmiljön ska du ersätta utvärderingsinformationen med produktionsuppgifter. Se till att du tar bort dina gamla inloggningsuppgifter för Reader Extensions innan du uppdaterar en inloggningsuppgift som har gått ut eller utvärderar den.

## Skapa ett alias för enheten {#configuredeviceinaemconsole}

Aliaset innehåller alla parametrar som krävs för en HSM eller token. Följ instruktionerna nedan för att skapa ett alias för varje HSM- eller tokenautentiseringsuppgift som eSign eller digitala signaturer använder:

1. Öppna AEM-konsolen. Standardwebbadressen för AEM-konsolen är https://&lt;host>:&lt;port>/system/console/configMgr
1. Öppna konfigurationstjänsten **för** HSM-autentiseringsuppgifter och ange värden för följande fält:

   * **Alias** för autentiseringsuppgifter: Ange en sträng som används för att identifiera aliaset. Det här värdet används som en egenskap för vissa åtgärder för digitala signaturer, till exempel åtgärden Signera signaturfält.
   * **DLL-sökväg**: Ange den fullständiga sökvägen till HSM- eller tokenklientbiblioteket på servern. Exempel: C:\Program Files\LunaSA\cryptoki.dll. I en klustrad miljö måste sökvägen vara identisk för alla servrar i klustret.
   * **HSM-stift**: Ange lösenordet som krävs för att komma åt enhetsnyckeln.
   * **HSM-kortplats-ID**: Ange en platsidentifierare av typen heltal. Kortplats-ID anges klient för klient. Om du registrerar en andra dator till en annan partition (till exempel HSMPART2 på samma HSM-enhet), kopplas fack 1 till HSMPART2-partitionen för klienten.
   **** Obs! *När du konfigurerar Etoken anger du ett numeriskt värde för fältet HSM-kortplats-ID. Ett numeriskt värde krävs för att signeringsåtgärderna ska fungera.*

   * **Certifikat SHA1**: Ange SHA1-värdet (tumavtryck) för filen med den offentliga nyckeln (.cer) för de autentiseringsuppgifter som du använder. Kontrollera att inga blanksteg används i SHA1-värdet. Om du använder ett fysiskt certifikat krävs det inte.
   * **HSM-enhetstyp**: Välj tillverkaren av HSM-enheten (Luna eller annan) eller eToken-enheten.
   Click **Save**. Maskinvarusäkerhetsmodulen är konfigurerad för AEM Forms. Nu kan du använda maskinvarusäkerhetsmodulen med AEM Forms för att signera eller certifiera dokument.

## Använd API:erna för DocAssurance-tjänsten för att signera eller certifiera ett dokument med digitala nycklar lagrade på enheten {#programatically}

I följande exempelkod används en HSM eller en token för att signera eller certifiera ett dokument.

```java
/*************************************************************************
 *
 * ADOBE CONFIDENTIAL
 * ___________________
 *
 * Copyright 2014 Adobe Systems Incorporated
 * All Rights Reserved.
 *
 * NOTICE:  All information contained herein is, and remains
 * the property of Adobe Systems Incorporated and its suppliers,
 * if any.  The intellectual and technical concepts contained
 * herein are proprietary to Adobe Systems Incorporated and its
 * suppliers and are protected by trade secret or copyright law.
 * Dissemination of this information or reproduction of this material
 * is strictly forbidden unless prior written permission is obtained
 * from Adobe Systems Incorporated.
 **************************************************************************/
package com.adobe.docassurance.samples;

import java.io.ByteArrayInputStream;
import java.io.IOException;
import java.io.InputStream;

import javax.jcr.Binary;
import javax.jcr.Node;
import javax.jcr.RepositoryException;
import javax.jcr.Session;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Reference;
import org.apache.felix.scr.annotations.Service;
import org.apache.sling.api.resource.ResourceResolver;
import org.apache.sling.jcr.api.SlingRepository;
import org.apache.sling.jcr.resource.JcrResourceResolverFactory;

import com.adobe.aemfd.docmanager.Document;
import com.adobe.fd.docassurance.client.api.DocAssuranceException;
import com.adobe.fd.docassurance.client.api.DocAssuranceService;
import com.adobe.fd.docassurance.client.api.DocAssuranceServiceOperationTypes;
import com.adobe.fd.docassurance.client.api.SignatureOptions;
import com.adobe.fd.signatures.client.types.exceptions.InvalidArgumentException;
import com.adobe.fd.signatures.pdf.inputs.CredentialContext;
import com.adobe.fd.signatures.pdf.inputs.DSSPreferences;
import com.adobe.fd.signatures.pdf.inputs.DSSPreferencesImpl;
import com.adobe.fd.signatures.pdf.inputs.PDFSignatureAppearenceOptions;
import com.adobe.fd.signatures.pdf.inputs.UnlockOptions;
import com.adobe.fd.signatures.pdf.inputs.PDFSignatureAppearenceOptions.PDFSignatureAppearanceType;
import com.adobe.fd.signatures.pdf.inputs.PDFSignatureAppearenceOptions.TextDirection;
import com.adobe.fd.signatures.pki.client.types.common.HashAlgorithm;
import com.adobe.fd.signatures.pki.client.types.common.RevocationCheckStyle;
import com.adobe.fd.signatures.pki.client.types.prefs.CRLPreferences;
import com.adobe.fd.signatures.pki.client.types.prefs.CRLPreferencesImpl;
import com.adobe.fd.signatures.pki.client.types.prefs.GeneralPreferencesImpl;
import com.adobe.fd.signatures.pki.client.types.prefs.PKIPreferences;
import com.adobe.fd.signatures.pki.client.types.prefs.PKIPreferencesImpl;
import com.adobe.fd.signatures.pki.client.types.prefs.PathValidationPreferences;
import com.adobe.fd.signatures.pki.client.types.prefs.PathValidationPreferencesImpl;

/**
 * Digital signatures can be applied to PDF documents to provide a level of security. Digital signatures, like handwritten signatures, provide a means by which signers
 * identify themselves and make statements about a document. The technology used to digitally sign documents helps to ensure that both the signer and recipients are clear
 * about what was signed and confident that the document was not altered since it was signed.
 *
 * PDF documents are signed by means of public-key technology. A signer has two keys: a public key and a private key. The private key is stored in a user's credential that
 * must be available at the time of signing. The public key is stored in the user's certificate that must be available to recipients to validate the signature. Information
 * about revoked certificates is found in certificate revocation lists (CRLs) and Online Certificate Status Protocol (OCSP) responses distributed by Certificate Authorities (CAs).
 * The time of signing can be obtained from a trusted source known as a Timestamping Authority.
 *
 * The following Java code example digitally signs a PDF document that is based on a PDF file.
 * The alias that is specified for the security credential is secure, and revocation checking is performed.
 * Because no CRL or OCSP server information is specified, the server information is obtained from the certificate used to
 * digitally sign the PDF document
 *
 * PreRequisites - Digital certificate for signing the document has to be uploaded on Granite Key Store
 */

@Component
@Service(value=Sign.class)
public class Sign{
 @Reference
 private DocAssuranceService docAssuranceService;

 @Reference
    private SlingRepository slingRepository;

 @Reference
    private JcrResourceResolverFactory jcrResourceResolverFactory ;

 /**
  *
  * @param inputFile - path to the pdf document stored at JCR node
  * @param outputFile - path to the pdf document where the output needs to be stored
  * @throws IOException
  * @throws RepositoryException
  * @throws InvalidArgumentException
  * @throws DocAssuranceException
  */
 public void signExtend(String inputFile, String outputFile, String alias) throws IOException, RepositoryException, InvalidArgumentException, DocAssuranceException{

  Document inDoc = new Document(inputFile);
  Document outDoc = null;

  Session adminSession = null;
        ResourceResolver resourceResolver = null;
        try {

          /** resourceResolver with admin privileges to be passed to SignatureServiceAPI and Reader Extensions
          the resource resolver for signature options has to be corresponding to the user who has the signing certificate in his granite key store
          the resource resolver for signature options has to be corresponding to the user who has the credential for reader extension in his granite key store
          here we are using the same resource resolver
          */
          adminSession = slingRepository.loginAdministrative(null);
             resourceResolver = jcrResourceResolverFactory.getResourceResolver(adminSession);

             //retrieve specifications for each of the services, you may pass null if you don't want to use that service
             //as we don't want encryption in this case, passing null for Encryption Options
             //for encrypted document pass Unlock Options - see the method getUnlockOptions() below
    outDoc = docAssuranceService.secureDocument(inDoc, null, getSignatureOptions(alias,resourceResolver),null,null);
        }
  catch(Exception e){
   e.printStackTrace();
  }
        finally{
            /**
             * always close the PDFDocument object after your processing is done.
             */
            if(inDoc != null){
                inDoc.close();
            }
            if(adminSession != null && adminSession.isLive()){
                if(resourceResolver != null){
                    resourceResolver.close();
                }
                adminSession.logout();
            }
        }

        //flush the output document contents to JCR Node
  flush(outDoc, outputFile);

 }

 /**
  *
  * @param rr resource resolver corresponding to the user with the access to signing credential for the
  * given alias "allcertificatesanypolicytest11ee_new" in this case
  * @return SignatureOptions
  */
 private SignatureOptions getSignatureOptions(String alias, ResourceResolver rr){

  //create an instance of SignatureOptions
  SignatureOptions signatureOptions = SignatureOptions.getInstance();

  //set the operation you want to perform - SIGN/CERTIFY
  signatureOptions.setOperationType(DocAssuranceServiceOperationTypes.SIGN);

  //field to sign
  String fieldName = "Signature1" ;

        //Hash Algo to be used to compute digest the PDF document
        HashAlgorithm algo = HashAlgorithm.SHA384;

        //Reason for signing/certifying
        String reason = "Test Reason";

        //location of the signer
        String location = "Test Location";

        //contact info of the signer
        String contactInfo = "Test Contact";

        //Create a PDFSignatureAppearanceOptions object
        //and show date information
        PDFSignatureAppearenceOptions appOptions = new PDFSignatureAppearenceOptions(
                PDFSignatureAppearanceType.NAME, null, 1.0d, null, true, true,
                true, true, true, true, true, TextDirection.AUTO);

        signatureOptions.setSignatureFieldName(fieldName);
        signatureOptions.setAlgo(algo);
        signatureOptions.setContactInfo(contactInfo);
        signatureOptions.setLocation(location);
        signatureOptions.setSigAppearence(appOptions);
        signatureOptions.setReason(reason);
        signatureOptions.setDssPref(getDSSPreferences(rr));
        signatureOptions.setCredential(new CredentialContext(alias, rr, true));
  return signatureOptions;
 }

 private DSSPreferences getDSSPreferences(ResourceResolver rr){
  //sets the DSS Preferences
        DSSPreferencesImpl prefs = DSSPreferencesImpl.getInstance();
        prefs.setPKIPreferences(getPKIPreferences());
        GeneralPreferencesImpl gp = (GeneralPreferencesImpl) prefs.getPKIPreferences().getGeneralPreferences();
        gp.setDisableCache(true);
        return prefs;
    }

    private PKIPreferences getPKIPreferences(){
     //sets the PKI Preferences
        PKIPreferences pkiPref = new PKIPreferencesImpl();
        pkiPref.setCRLPreferences(getCRLPreferences());
        pkiPref.setPathPreferences(getPathValidationPreferences());
        return pkiPref;
    }

    private CRLPreferences getCRLPreferences(){
        //specifies the CRL Preferences
        CRLPreferencesImpl crlPrefs = new CRLPreferencesImpl();
        crlPrefs.setRevocationCheck(RevocationCheckStyle.CheckIfAvailable);
        crlPrefs.setGoOnline(true);
        return crlPrefs;
    }

    private PathValidationPreferences getPathValidationPreferences(){
     //sets the path validation preferences
        PathValidationPreferencesImpl pathPref = new PathValidationPreferencesImpl();
        pathPref.setDoValidation(false);
        return pathPref;

    }

    /**
     * sets Unlock Options for encrypted PDF
     */
    private UnlockOptions getUnlockOptions(){
        UnlockOptions unlockOptions = new UnlockOptions();
        //sets the Open Password for password encrypted PDF
        unlockOptions.setPassword("OpenPassword");

        //for Certificate Encrypted Document, set the alias of the credential uploaded in the user's key store
        //and corresponding resource resolver

        return unlockOptions;

    }
    /**
     * This method copies the data from {@code Document}, to the specified file at the given resourcePath.
     * @param doc
     * @param resourcePath
     * @throws IOException
     */
    private void flush(Document doc, String resourcePath) throws IOException {
   //extracts the byte data from Document
   byte[] output = doc.getInlineData();
   Binary opBin;
   Session adminSession = null;
      try {
         adminSession = slingRepository.loginAdministrative(null);

         //get access to the specific node
         //here we are assuming that node exists
           Node node = adminSession.getNode(resourcePath);

           //convert byte[] to Binary
           opBin = adminSession.getValueFactory().createBinary((InputStream)new ByteArrayInputStream(output));

           //set the Binary data value to node's jcr:data
           node.getNode("jcr:content").getProperty("jcr:data").setValue(opBin);
      } catch (RepositoryException e) {

      }
      finally{

       if(adminSession != null && adminSession.isLive()){
        try {
      adminSession.save();
      adminSession.logout();
     } catch (RepositoryException e) {

     }

             }
      }

  }
}
```

Om du har uppgraderat från AEM 6.0 Form eller AEM 6.1 Forms och du använde tjänsten DocAssurance i den tidigare versionen:

* Om du vill använda tjänsten DocAssurance utan en NMI- eller tokenenhet fortsätter du använda den befintliga koden.
* Om du vill använda DocAssurance-tjänsten med en HSM- eller tokenenhet ersätter du din befintliga CredentialContext-objektkod med API:t som listas nedan.

```java
/**
  *
  * @param credentialAlias alias of the PKI Credential stored in CQ Key Store or
  * the alias of the HSM Credential configured using HSM Credentials Configuration Service.
  * @param resourceResolver corresponding to the user with the access to the key store and trust store.
  * @param isHSMCredential if the alias is corresponding to HSM Credential.
  */
 public CredentialContext(String credentialAlias, ResourceResolver resourceResolver, boolean isHSMCredential);
```

Mer information om API:er och exempelkod för DocAssurance-tjänsten finns i [Använda AEM Document Services programmatiskt](/help/forms/using/aem-document-services-programmatically.md).
