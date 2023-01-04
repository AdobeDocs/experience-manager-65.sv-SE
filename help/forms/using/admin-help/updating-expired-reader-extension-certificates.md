---
title: Utgångsdatum för Reader Extensions-certifikat och dess effekt
description: Utgångsdatum för Reader Extensions-certifikat och dess effekt
exl-id: 4e14e0dc-f248-4f6e-a075-6012b6792d9d
source-git-commit: 6e9a7f3307ed05f887d60c7c7310100cd4596b23
workflow-type: tm+mt
source-wordcount: '1121'
ht-degree: 0%

---


# Utgångsdatum för Reader Extensions-certifikat och dess effekt {#expiration-of-reader-extensions-certificates-and-its-impact}

Adobe Experience Manager Forms (AEM Forms)-kunder med Adobe Managed Services eller On-Local Enterprise Base-licenser har rätt att använda tjänsten Acrobat Reader DC Extensions. Med tjänsten kan man enkelt utbyta interaktiva PDF-dokument genom att utöka Acrobat Reader funktionalitet med ytterligare användarrättigheter. Tjänsten lägger till användarrättigheter i ett PDF-dokument och aktiverar funktioner som inte är tillgängliga när ett PDF-dokument öppnas med Adobe Acrobat Reader, till exempel för att lägga till kommentarer i ett dokument, fylla i formulär och spara dokumentet. Tredjepartsanvändare behöver inte ytterligare programvara eller plugin-program för att kunna arbeta med upphovsrättsaktiverade dokument. PDF-dokument som har användarrättigheter tillagda kallas för rättighetsaktiverade dokument. En användare som öppnar ett rättighetsaktiverat PDF-dokument i Acrobat Reader kan utföra de åtgärder som är aktiverade för det dokumentet.

Adobe utnyttjar en infrastruktur för publika nycklar (PKI) för att utfärda digitala certifikat för användning vid licensiering och aktivering av funktioner. Adobe har utfärdat certifikat under certifikatutfärdaren **Adobe Root CA**, som upphör den 7 januari 2023. Certifikatets giltighetstid påverkar inte PDF-dokument som har utökats med hjälp av tillverkningscertifikat som utfärdats från **Adobe Root CA** baserade certifikat (gamla certifikat). Alla PDF-dokument som har utökats med hjälp av de gamla certifikaten före den 7 januari 2023, inklusive de som hämtats av dina kunder, fortsätter att arbeta med alla användningsrättigheter som gäller för dem och behöver inte uppdateras.

En ny certifikatutfärdare, **Adobe Root CA G2** och certifikat som baseras på den nya certifikatutfärdaren är nu tillgängliga. Från och med den 7 januari 2023 börjar man använda de nya certifikaten - de som bygger på **Adobe Root CA G2** - för att Reader ska kunna lägga ut dina nya PDF-dokument.  Du kan [skaffa nya certifikat från Adobe licenswebbplats](https://licensing.adobe.com/) eller Adobe Support.

## Vanliga frågor

**Fråga. Vad är skillnaden mellan ett Adobe-rotcertifikat och ett Acrobat Reader Extensions-certifikat? Är rotcertifikatet för Adobe beroende av ett Acrobat Reader Extensions-certifikat? Upphör båda dessa certifikat att gälla i januari 2023?**

S. Adobe Root CA är den certifikatutfärdare från vilken ett Acrobat Reader Extensions-certifikat utfärdas. Den 7 januari 2023 upphör&quot;Adobe Root CA&quot; och alla certifikat som utfärdas från den att gälla.

**Fråga. Det fanns ett tidigare meddelande från Adobe om att certifikaten skulle upphöra att gälla och om hur de påverkat användningen/öppnandet av dokument i PDF. Ska den kommunikationen ignoreras?**

S. På grundval av den nya bedömningen av situationen fortsätter alla dokument från PDF som byggts ut med hjälp av tillverkningscertifikat som utfärdats från det gamla&quot;Adobe Root CA&quot; före den 7 januari 2023 att fungera utan ändringar efter den 7 januari 2023. Om du redan har uppdaterat dina PDF-dokument förändras inte upplevelsen.

**Fråga. Vem ska jag kontakta om jag har ytterligare frågor?**

S. Du kan kontakta [Stöd för Adobe](https://experienceleague.adobe.com/?support-solution=Experience+Manager#support) eller skaffa en supportanmälan.

**Fråga. Vad händer om jag inte uppdaterar mitt certifikat före 7 januari 2023?**

S. Alla PDF-dokument som byggts ut med hjälp av produktionscertifikat som utfärdats från den gamla Adobe Root CA före den 7 januari 2023 fortsätter att fungera utan ändringar efter den 7 januari 2023. PDF som utökats med utvärderingscertifikat fungerar inte efter förfallodatumet.

**Fråga. Skiljer sig beskrivningen av nya certifikat från gamla?**

S. Beskrivningen av de nya Acrobat Reader Extensions-certifikaten **G3-P24** som programnamn. I beskrivningen av äldre certifikat (certifikat baserade på &quot;Adobe Root CA&quot;) **P24** anges som programnamn.

**Fråga. Hur får jag tag i de senaste certifikaten?**

S. Alla berättigade Forms-kunder (med aktiv licens) kan hämta de nya certifikaten (certifikat som baseras på&quot;Adobe Root CA G2&quot;) från [Adobe licenswebbplats](https://licensing.adobe.com/). Om du inte kan hitta certifikatet på Adobe licenswebbplats kontaktar du [Stöd för Adobe](https://experienceleague.adobe.com/?support-solution=Experience+Manager&amp;lang=en#support) eller skaffa en supportanmälan.

**Fråga. Fortsätter mina PDF-dokument som utökats med certifikat som utfärdats av&quot;Adobe Root CA&quot; (den gamla certifikatutfärdaren) att fungera efter den 7 januari 2023?**

S. Ja, alla dokument från PDF som har utökats med hjälp av produktionscertifikat som utfärdats av&quot;Adobe Root CA&quot; (den gamla certifikatutfärdaren) före den 7 januari 2023 fortsätter att fungera utan ändringar efter den 7 januari 2023. PDF-dokument som har förlängts med utvärderingscertifikat slutar att fungera efter förfallodatumet.

**Fråga. Vilken version av Adobe Acrobat Reader krävs för att fortsätta använda PDF-dokument som har utökats med certifikat som har utfärdats från&quot;Adobe Root CA&quot; (den gamla certifikatutfärdaren)?**

S. Adobe Acrobat Reader 2020 eller senare krävs för att använda PDF-dokument som har utökats med Adobe Root CA (den gamla certifikatutfärdaren). Det är den version av Acrobat Reader som stöds när det här dokumentet publiceras. Om du använder en [version av Adobe Acrobat som inte stöds](https://helpx.adobe.com/support/programs/eol-matrix.html), Adobe rekommenderar att du [ladda ned och installera den senaste versionen av Adobe Acrobat Reader](https://get.adobe.com/reader/).

**Fråga. Vilken version av Adobe Acrobat Reader krävs för att fortsätta använda PDF-dokument som har utökats med certifikat som har utfärdats från&quot;Adobe Root CA 2&quot; (den nya certifikatutfärdaren)?**

S. Adobe Acrobat Reader 2020 eller senare krävs för att använda PDF-dokument som har utökats med Adobe Root CA 2 (den nya certifikatutfärdaren). Om du använder en [version av Adobe Acrobat Reader som inte stöds](https://helpx.adobe.com/support/programs/eol-matrix.html), Adobe rekommenderar att du [ladda ned och installera den senaste versionen av Adobe Acrobat Reader](https://get.adobe.com/reader/).

**Fråga. Kan jag ta bort ett gammalt Acrobat Reader Extensions-certifikat och lägga till ett nytt på en Adobe Experience Manager Forms Server samtidigt som jag fortsätter att använda det befintliga aliaset?**

S. Ja, du kan ta bort ett gammalt Acrobat Reader Extensions-certifikat och lägga till ett nytt med det befintliga aliaset till en Adobe Experience Manager Forms Server.

**Fråga. Kan jag behålla både nya och gamla Acrobat Reader Extensions-certifikat på en Adobe Experience Manager Forms-server?**

S. Ja, du kan behålla båda certifikaten men med olika alias på en Adobe Experience Manager Forms Server. Efter 7 januari 2023 kan du bara använda det nya certifikatet för att Reader utöka ett PDF-dokument.

**Fråga. Kan jag importera samma Acrobat Reader Extensions-certifikat till alla Adobe Experience Manager Forms-miljöer?**

S. Ja, samma Acrobat Reader Extensions-certifikat kan användas i flera miljöer.

**Fråga. Hur kontrollerar jag användningsrättigheterna för ett PDF-dokument?**

S. Du kan använda [getDocumentUsageRights](https://experienceleague.adobe.com/docs/experience-manager-65/forms/developer-reference/programming-aem-forms-jee/java-api-quick-start-code-examples/acrobat-reader-dc-extensions-service.html?lang=en#quick-start-soap-mode-retrieving-credential-information-using-the-java-api) API för att hämta information om användningsrättigheterna för ett PDF-dokument.

**Fråga. Hur ändrar jag lösenordet för en Acrobat Reader Extensions-certifikatfil?**

S. Om du vill ändra certifikatlösenordet i Microsoft Windows installerar du certifikatet med hjälp av Microsoft Management Console (MMC) och väljer **Markera nyckeln som exporterbar**. När du har installerat det exporterar du certifikatet med en privat nyckel och använder ett annat lösenord för PFX-filen.


<!-- 
## Applying the certificates {#obtaning-and-applying-the-certificates} 

You can choose one of the following paths to apply latest certificates:

* [Updating certificates for an AEM Forms on JEE environment](#Updating-and-Applying-certificates-for-an-AEM-Forms-on-JEE-environment) 
* [Updating certificates for an AEM Forms on OSGi environment](#Updating-and-applying-certificates-for-an-AEM-Forms-on-OSGi-environment)

>[!NOTE]
>
>The document uses the term certificates and credentials interchangeably.

### Pre-requisites {#Pre-requisites}

Updating the certificates requires using actions available on AEM Forms administrator console and Reader Extension APIs provided by AEM Forms. The document is intended for users and administrators with knowledge of using Adobe Experience Manger Forms APIs. Before you start, ensure that: 

* the user has administrator rights on underlying AEM Forms environment. 
* the user has setup the [development environment](https://experienceleague.adobe.com/docs/experience-manager-65/developing/devtools/howto-projects-eclipse.html) and has access to it.
* [obtain the certificates](#obtain-the-certificates).


### Obtain the certificates {#obtain-the-certificates}

The Rights credential is delivered as a digital certificate that contains the public key, the private key, and the password used to access the credential.

If your organization purchases a production version of Reader Extensions, the production Rights credential is delivered by Adobe Licensing Website (LWS). A production Rights credential is unique to your organization and can enable the specific usage rights that you require.

If you obtained Reader Extensions through a partner or software provider who integrated Reader Extensions into their software, the Rights credential is provided to you by that partner who, in turn, receives this credential from Adobe.

>[!NOTE]
>
>The Rights credential cannot be used for typical document signing or assertion of identity. For these applications, you can use a self-sign certificate or acquire an identity certificate from a Certificate Authority (CA).

The following types of Rights credentials are available:

**Customer Evaluation**: A credential with a short validity period that is provided to customers who want to evaluate Reader Extensions. Usage rights applied to documents using this credential expire when the credential expires. This type of credential is valid only for two to three months.

**Production**: A credential with a long validity period that is provided to customers who purchased the full product. Production credentials are unique to each customer but can be installed on multiple systems.

If you have already used certificates to reader extend PDF files, download a production certificate from [Adobe Licensing Website (LWS)](https://licensing.adobe.com/).

### Applying certificates for an AEM Forms on JEE environment {#Updating-and-Applying-certificates-for-an-AEM-Forms-on-JEE-environment} 

Applying new certificates on AEM Forms on JEE stack requires importing new credentials and applying usage rights. You can use admin console to import credentials and AEM Forms Reader Extension APIs to apply usage rights. 

#### Import and configure credentials 

You can use the Trust Store Management pages to import a new credential. The Trust Store may contain more than one Reader Extensions credential. You must designate one of those credentials as the default Reader Extensions credential. The default credential is used when a Workbench user is unable to determine which credential to use during process creation. These rules apply to default credentials:

* If you import a Reader Extensions credential and the Trust Store contains no other Reader Extensions credentials, it is set as the default.
* If you import a Reader Extensions credential with the Default option selected, the default type is removed from an existing default credential. The imported credential becomes the default.
* You cannot delete a default Reader Extensions credential. To delete the default credential, first set another credential as the default. An exception to this rule is that if there is only one credential, you can delete it even though it is the default.
* You cannot update a default Reader Extensions credential.

To import the credentials: 

1. In administration console, click Settings > Trust Store Management > Local Credentials.
1. Click Import and, under Trust Store Type, select Acrobat Reader DC extensions Credential.
1. (Optional) To indicate that this credential is the default credential to use with Acrobat Reader DC extensions, select Default.
1. In the Alias box, type an identifier for the credential. This identifier is used as the display name for the credential in Acrobat Reader DC extensions. This alias is also used to access the credential programmatically using the AEM forms SDK.
1. Click Choose File to locate the credential, type the password of the credential, and then click OK.

If the error message "Failed to import credential due to either incorrect file format, or incorrect password" appears, verify that the password is valid.

You can also import and delete credentials programmatically. (See [Programming with AEM forms](../../developing/credentials.md).)

<!-- ### Remove usage rights from existing rights-enabled PDF documents

Remove usage rights from existing rights-enabled PDF documents before applying usage rights with latest credentials. AEM Forms on JEE provides APIs to remove usage rights. For detailed instructions, see [Removing Usage Rights from PDF Documents](../../developing/assigning-usage-rights.md#removing-usage-rights-from-pdf-documents).

To remove usage rights for AEM Forms on JEE processes developed in Workbench, see [Workbench Help](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/pdf/WorkbenchHelp.pdf). 

#### Apply the usage rights to PDF documents 

After importing new credentials, you can apply usage rights to PDF documents using the Acrobat Reader DC extensions Java Client API and web service.  For details, see [Applying Usage Rights to PDF Documents](../../developing/assigning-usage-rights.md#applying-usage-rights-to-pdf-documents). 


### Applying certificates for an AEM Forms on OSGi environment {#Updating-and-applying-certificates-for-an-AEM-Forms-on-OSGi-environment}

Applying new certificates on AEM Forms on OSGi stack requires importing new credentials and applying usage rights. You can use admin console to import credentials and AEM Forms Reader Extension APIs to apply usage rights. 

#### Import credentials {#Import-credentials}

In an AEM Forms on OSGi environment, a Reader Extension credential is associated with fd-service user. Before adding credentials for fd-user key store, perform the following steps to create a key store: 

1. Log in to your AEM Author instance as an Administrator.
1. Go to **[!UICONTROL Tools]**> **[!UICONTROL Security]**>**[!UICONTROL Users]**.
1. Scroll down the list of users until you find fd-service user account.
1. Click **[!UICONTROL fd-service]** user.
1. Click keystore tab.
1. Click **[!UICONTROL Create KeyStore]**.
1. Set the KeyStore Access Password and save your settings to create the KeyStore password.

After creating the key-store, add credentials to fd-service user. The following video explains the steps: 

>[!VIDEO](https://images-tv.adobe.com/mpcv3/5577/8db8e554-f04b-4fae-8108-b9b5e0eb03ad_1627925794.854x480at800_h264.mp4)

The following command list the details of the pfx file. Before running the command, navigate to the directory that contains the .pfx file.

`keytool -v -list -storetype pkcs12 -keystore [name of your .pfx file]`

For example keytool -v -list -storetype pkcs12 -keystore 1005566.pfx where 1005566.pfx is the name of my pfx file

<!-- ### Remove usage rights from existing rights-enabled PDF documents

Remove usage rights from existing rights-enabled PDF documents before applying usage rights with latest credentials. You can remove the usage rights for a document by invoking the removeUsageRights API from within the docAssuranceServiceAPI. For detailed information, see [Remove Usage Rights](/help/forms/using/aem-document-services-programmatically.md#removing-usage-rights) document.

#### Apply the usage rights to PDF documents 

To apply usage rights in an AEM Forms on OSGi environment, Create custom OSGi service to usage rights to the documents. You can also create a servlet with a POST method to return the reader extended PDF to the user. For detailed instructions, see [Applying Reader Extensions](https://experienceleague.adobe.com/docs/experience-manager-learn/forms/document-services/apply-reader-extension-rights-to-pdf.html).  -->
