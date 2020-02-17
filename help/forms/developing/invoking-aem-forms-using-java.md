---
title: Anropa AEM-formulär med JavaAPI
seo-title: Anropa AEM-formulär med JavaAPI
description: 'null'
seo-description: 'null'
uuid: 5e2fef2a-05f3-4283-8fd3-2d7dca411000
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: coding
discoiquuid: 0e6e7850-6137-42c5-b8e2-d4e352fddae2
translation-type: tm+mt
source-git-commit: 7cbe3e94eddb81925072f68388649befbb027e6d

---


# Anropa AEM-formulär med Java API {#invoking-aem-forms-using-the-javaapi}

AEM Forms kan anropas med AEM Forms Java API. När du använder AEM Forms Java API kan du antingen använda anrops-API eller Java-klientbibliotek. Java-klientbibliotek är tillgängliga för tjänster som Rights Management-tjänsten. Med dessa starkt typbestämda API:er kan du utveckla Java-program som anropar AEM Forms.

Anrops-API:t är klasser som finns i `com.adobe.idp.dsc` paketet. Med dessa klasser kan du skicka en anropsbegäran direkt till en tjänst och hantera ett anropssvar som returneras. Använd anrops-API:t för att anropa kortlivade eller långvariga processer som skapats med Workbench.

Det rekommenderade sättet att programmässigt anropa en tjänst är att använda ett Java-klientbibliotek som motsvarar tjänsten i motsats till anrops-API:t. Om du till exempel vill anropa krypteringstjänsten använder du krypteringstjänstens klientbibliotek. Om du vill utföra en krypteringstjänståtgärd anropar du en metod som tillhör krypteringstjänstens klientobjekt. Du kan kryptera ett PDF-dokument med ett lösenord genom att anropa `EncryptionServiceClient` objektets `encryptPDFUsingPassword` metod.

Java API har stöd för följande funktioner:

* RMI-transportprotokoll för fjärranrop
* VM-transport för lokalt anrop
* SOAP för fjärranrop
* Annan autentisering, till exempel användarnamn och lösenord
* Synkrona och asynkrona anropsbegäranden

**Adobe Developer website**

Adobe Developer-webbplatsen innehåller följande artiklar som beskriver hur du anropar AEM Forms-tjänster med Java API:

[Använda Java-servrar för att anropa AEM Forms-processer](https://www.adobe.com/devnet/livecycle/articles/java_servlets.html)

[Anropa AEM Forms Distiller API från Java](https://www.adobe.com/devnet/livecycle/articles/distiller_java_03.html)

**Se även**

[Inkludera AEM Forms Java-biblioteksfiler](#including-aem-forms-java-library-files)

[Anropa personalcentrerade, långlivade processer](/help/forms/developing/invoking-human-centric-long-lived.md#main-pars-text-0)

[Anropa AEM-formulär med webbtjänster](/help/forms/developing/invoking-aem-forms-using-web.md)

[Ange anslutningsegenskaper](#setting-connection-properties)

[Skicka data till AEM Forms-tjänster med Java API](#passing-data-to-aem-forms-services-using-the-java-api)

[Anropa en tjänst med ett Java-klientbibliotek](#invoking-a-service-using-a-java-client-library)

[Anropa en kort process med anrops-API](#invoking-a-short-lived-process-using-the-invocation-api)

[Skapa ett Java-webbprogram som anropar en mänsklig, lång process](/help/forms/developing/invoking-human-centric-long-lived.md)

## Inkludera AEM Forms Java-biblioteksfiler {#including-aem-forms-java-library-files}

Om du vill anropa en AEM Forms-tjänst med hjälp av Java API:t inkluderar du nödvändiga biblioteksfiler (JAR-filer) i Java-projektets klassökväg. JAR-filerna som du inkluderar i klientprogrammets klassökväg beror på flera faktorer:

* Den AEM Forms-tjänst som ska anropas. Ett klientprogram kan anropa en eller flera tjänster.
* Det läge i vilket du vill anropa en AEM Forms-tjänst. Du kan använda läget EJB eller SOAP. (Se [Ange anslutningsegenskaper](invoking-aem-forms-using-java.md#setting-connection-properties).)
* J2EE-programservern där AEM Forms distribueras.

### Tjänstspecifika JAR-filer {#service-specific-jar-files}

I följande tabell visas de JAR-filer som krävs för att anropa AEM Forms-tjänster.

<table>
 <thead>
  <tr>
   <th><p>Arkiv</p></th>
   <th><p>Beskrivning</p></th>
   <th><p>Plats</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>adobe-livecycle-client.jar</p></td>
   <td><p>Måste alltid ingå i ett Java-klientprograms klassökväg.</p></td>
   <td><p>&lt;<i>installationskatalog</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-usermanager-client.jar</p></td>
   <td><p>Måste alltid ingå i ett Java-klientprograms klassökväg.</p></td>
   <td><p>&lt;<i>installationskatalog</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-utilities.jar</p></td>
   <td><p>Måste alltid ingå i ett Java-klientprograms klassökväg.</p></td>
   <td><p>&lt;<i>installationskatalog</i>&gt;/sdk//client-libs/&lt;programserver&gt;</p></td>
  </tr>
  <tr>
   <td><p>adobe-applicationmanager-client-sdk.jar</p></td>
   <td><p>Krävs för att anropa Application Manager-tjänsten.</p></td>
   <td><p>&lt;<i>installationskatalog</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-assembler-client.jar</p></td>
   <td><p>Krävs för att anropa Assembler-tjänsten. </p></td>
   <td><p>&lt;<i>installationskatalog</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-backup-restore-client-sdk.jar</p></td>
   <td><p>Krävs för att anropa tjänste-API:t för säkerhetskopiering och återställning.</p></td>
   <td><p>&lt;<i>installationskatalog</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-barcodedforms-client.jar</p></td>
   <td><p>Krävs för att anropa den streckkodade formulärtjänsten. </p></td>
   <td><p>&lt;<i>installationskatalog</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-convertpdf-client.jar</p></td>
   <td><p>Krävs för att anropa tjänsten Konvertera PDF. </p></td>
   <td><p>&lt;<i>installationskatalog</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-distiller-client.jar</p></td>
   <td><p>Krävs för att anropa Distiller-tjänsten.</p></td>
   <td><p>&lt;<i>installationskatalog</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-docconverter-client.jar</p></td>
   <td><p>Krävs för att anropa tjänsten DocConverter.</p></td>
   <td><p>&lt;<i>installationskatalog</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-contentservices-client.jar</p></td>
   <td><p>Krävs för att anropa dokumenthanteringstjänsten.</p></td>
   <td><p>&lt;<i>installationskatalog</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-encryption-client.jar</p></td>
   <td><p>Krävs för att anropa krypteringstjänsten.</p></td>
   <td><p>&lt;<i>installationskatalog</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-forms-client.jar</p></td>
   <td><p>Krävs för att anropa Forms-tjänsten.</p></td>
   <td><p>&lt;<i>installationskatalog</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-formdataintegration-client.jar</p></td>
   <td><p>Krävs för att anropa integreringstjänsten för formulärdata.</p></td>
   <td><p>&lt;<i>installationskatalog</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-generatepdf-client.jar</p></td>
   <td><p>Krävs för att anropa tjänsten Generera PDF.</p></td>
   <td><p>&lt;<i>installationskatalog</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-generate3dpdf-client.jar</p></td>
   <td><p>Krävs för att anropa tjänsten Generera 3D PDF.</p></td>
   <td><p>&lt;<i>installationskatalog</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-jobmanager-client-sdk.jar</p></td>
   <td><p>Krävs för att anropa tjänsten Job Manager. </p></td>
   <td><p>&lt;<i>installationskatalog</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-output-client.jar</p></td>
   <td><p>Krävs för att anropa Output-tjänsten.</p></td>
   <td><p>&lt;<i>installationskatalog</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-pdfutility-client.jar</p></td>
   <td><p>Krävs för att anropa PDF-verktygen eller XMP-verktygstjänsten.</p></td>
   <td><p>&lt;<i>installationskatalog</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-reader-extensions-client.jar</p></td>
   <td><p>Krävs för att anropa Acrobat Reader DC-tilläggstjänsten.</p></td>
   <td><p>&lt;<i>installationskatalog</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-database-client.jar</p><p>comons-codec-1.3.jar</p></td>
   <td><p>Krävs för att anropa databastjänsten.</p></td>
   <td><p>&lt;<i>installationskatalog</i>&gt;/sdk/client-libs/common</p><p>&lt;<i>installationskatalog</i>&gt;/sdk/client-libs\thirdparty</p></td>
  </tr>
  <tr>
   <td>
    <ul>
     <li><p>adobe-rightsmanagement-client.jar</p></li>
     <li><p>namespace.jar</p></li>
     <li><p>jaxb-api.jar</p></li>
     <li><p>jaxb-impl.jar</p></li>
     <li><p>jaxb-libs.jar</p></li>
     <li><p>jaxb-xjc.jar</p></li>
     <li><p>relaxngDatatype.jar</p></li>
     <li><p>xsdlib.jar</p></li>
    </ul></td>
   <td><p>Krävs för att anropa Rights Management-tjänsten.</p><p>Om AEM Forms distribueras på JBoss inkluderar du alla dessa filer. </p></td>
   <td><p>&lt;<i>installationskatalog</i>&gt;/sdk/client-libs/common</p><p>JBoss-specifik bibliotekskatalog</p></td>
  </tr>
  <tr>
   <td><p>adobe-signatures-client.jar</p></td>
   <td><p>Krävs för att anropa signaturtjänsten.</p></td>
   <td><p>&lt;<i>installationskatalog</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-taskmanager-client-sdk.jar</p></td>
   <td><p>Krävs för att anropa tjänsten Task Manager. </p></td>
   <td><p>&lt;<i>installationskatalog</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-truststore-client.jar</p></td>
   <td><p>Krävs för att anropa tjänsten Trust Store. </p></td>
   <td><p>&lt;<i>installationskatalog</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
 </tbody>
</table>

### Anslutningsläge och JAR-filer för J2EE-program {#connection-mode-and-j2ee-application-jar-files}

I följande tabell visas de JAR-filer som är beroende av anslutningsläget och J2EE-programservern som AEM Forms distribueras på.

<table>
 <thead>
  <tr>
   <th><p>Arkiv</p> </th>
   <th><p>Beskrivning</p> </th>
   <th><p>Plats</p> </th>
  </tr>
 &lt;/thead align="left"&gt;
 <tbody>
  <tr>
   <td>
    <ul>
     <li><p>activation.jar</p> </li>
     <li><p>axis.jar</p> </li>
     <li><p>comons-codec-1.3.jar</p> </li>
     <li><p>commons-collections-3.1.jar</p> </li>
     <li><p>comons-discovery.jar</p> </li>
     <li><p>commons-log.jar</p> </li>
     <li><p>dom3-xml-apis-2.5.0.jar</p> </li>
     <li><p>jaxen-1.1-beta-9.jar</p> </li>
     <li><p>jaxrpc.jar</p> </li>
     <li><p>log4j.jar</p> </li>
     <li><p>mail.jar</p> </li>
     <li><p>saaj.jar</p> </li>
     <li><p>wsdl4j.jar</p> </li>
     <li><p>xalan.jar</p> </li>
     <li><p>xbean.jar</p> </li>
    </ul>
    <ul>
     <li>xercesImpl.jar<br /> </li>
     <li>commons-httpclient-3.1.jar</li>
    </ul> <p> </p> </td>
   <td><p>Om AEM Forms anropas i SOAP-läge ska du inkludera dessa JAR-filer.</p> </td>
   <td><p>&lt;<em>installationskatalog</em>&gt;/sdk/client-libs/thirdparty</p> </td>
  </tr>
  <tr>
   <td><p> jboss-client.jar</p> </td>
   <td><p>om AEM Forms distribueras på JBoss Application Server, inkludera den här JAR-filen.</p> <p>Klassinläsaren hittar inte nödvändiga klasser om jboss-client.jar och de refererade burkarna inte finns tillsammans.</p> </td>
   <td><p>JBoss-klientbibliotekskatalog</p> <p>Om du distribuerar klientprogrammet på samma J2EE-programserver behöver du inte inkludera den här filen.</p> </td>
  </tr>
  <tr>
   <td><p>wlclient.jar</p> </td>
   <td><p>Om AEM Forms används på BEA WebLogic Server® ska du bifoga den här JAR-filen.</p> </td>
   <td><p>WebLogic-specifik bibliotekskatalog</p> <p>Om du distribuerar klientprogrammet på samma J2EE-programserver behöver du inte inkludera den här filen.</p> </td>
  </tr>
  <tr>
   <td>
    <ul>
     <li><p>com.ibm.ws.admin.client_6.1.0.jar</p> </li>
     <li><p>com.ibm.ws.webservices.thinclient_6.1.0.jar</p> </li>
    </ul> </td>
   <td>
    <ul>
     <li><p>om AEM Forms distribueras på WebSphere Application Server ska du inkludera dessa JAR-filer.</p> </li>
     <li><p>(com.ibm.ws.webservices.thinclient_6.1.0.jar krävs för webbtjänstanrop).</p> </li>
    </ul> </td>
   <td><p>WebSphere-specifik bibliotekskatalog (<em>[WAS_HOME]</em>/runtimes)</p> <p>Om du distribuerar klientprogrammet på samma J2EE-programserver behöver du inte inkludera de här filerna.</p> </td>
  </tr>
 </tbody>
</table>

### Anropa scenarier {#invoking-scenarios}

I följande tabell anges vilka scenarier som anropas och vilka JAR-filer som krävs för att AEM Forms ska kunna anropas.

<table>
 <thead>
  <tr>
   <th><p>Tjänster</p> </th>
   <th><p>Anropsläge</p> </th>
   <th><p>J2EE-programserver</p> </th>
   <th><p>Nödvändiga JAR-filer</p> </th>
  </tr>
 &lt;/thead align="left"&gt;
 <tbody>
  <tr>
   <td><p>Formulärtjänst</p> </td>
   <td><p>EJB</p> </td>
   <td><p>JBoss</p> </td>
   <td>
    <ul>
     <li><p>adobe-livecycle-client.jar</p> </li>
     <li><p>adobe-usermanager-client.jar</p> </li>
    </ul>
    <ul>
     <li>jboss-client.jar</li>
    </ul>
    <ul>
     <li>adobe-forms-client.jar<br /> </li>
     <li>commons-httpclient-3.1.jar</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>Formulärtjänst</p> <p>Tilläggstjänsten Acrobat Reader DC</p> <p>Signaturtjänst</p> </td>
   <td><p>EJB</p> </td>
   <td><p>JBoss</p> </td>
   <td>
    <ul>
     <li><p>adobe-livecycle-client.jar</p> </li>
     <li><p>adobe-usermanager-client.jar</p> </li>
    </ul>
    <ul>
     <li>jboss-client.jar<br /> </li>
     <li>commons-httpclient-3.1.jar</li>
    </ul>
    <ul>
     <li><p>adobe-forms-client.jar</p> </li>
     <li><p>adobe-reader-extensions-client.jar</p> </li>
     <li><p>adobe-signatures-client.jar</p> </li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>Formulärtjänst</p> </td>
   <td><p>SOAP</p> </td>
   <td><p>WebLogic</p> </td>
   <td>
    <ul>
     <li><p>adobe-livecycle-client.jar</p> </li>
     <li><p>adobe-usermanager-client.jar</p> </li>
     <li><p>wlclient.jar</p> </li>
     <li><p>activation.jar</p> </li>
     <li><p>axis.jar</p> </li>
     <li><p>comons-codec-1.3.jar</p> </li>
     <li><p>commons-collections-3.1.jar</p> </li>
     <li><p>comons-discovery.jar</p> </li>
     <li><p>commons-log.jar</p> </li>
     <li><p>dom3-xml-apis-2.5.0.jar</p> </li>
     <li><p>jai_imageio.jar</p> </li>
     <li><p>jaxen-1.1-beta-9.jar</p> </li>
     <li><p>jaxrpc.jar</p> </li>
     <li><p>log4j.jar</p> </li>
     <li><p>mail.jar</p> </li>
     <li><p>saaj.jar</p> </li>
     <li><p>wsdl4j.jar</p> </li>
     <li><p>xalan.jar</p> </li>
     <li><p>xbean.jar</p> </li>
     <li><p>xercesImpl.jar</p> </li>
     <li><p>adobe-forms-client.jar</p> </li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>Formulärtjänst</p> <p>Tilläggstjänsten Acrobat Reader DC</p> <p>Signaturtjänst</p> </td>
   <td><p>SOAP</p> </td>
   <td><p>WebLogic</p> </td>
   <td>
    <ul>
     <li><p>adobe-livecycle-client.jar</p> </li>
     <li><p>adobe-usermanager-client.jar</p> </li>
     <li><p>wlclient.jar</p> </li>
     <li><p>activation.jar</p> </li>
     <li><p>axis.jar</p> </li>
     <li><p>comons-codec-1.3.jar</p> </li>
     <li><p>commons-collections-3.1.jar</p> </li>
     <li><p>comons-discovery.jar</p> </li>
     <li><p>commons-log.jar</p> </li>
     <li><p>dom3-xml-apis-2.5.0.jar</p> </li>
     <li><p>jai_imageio.jar</p> </li>
     <li><p>jaxen-1.1-beta-9.jar</p> </li>
     <li><p>jaxrpc.jar</p> </li>
     <li><p>log4j.jar</p> </li>
     <li><p>mail.jar</p> </li>
     <li><p>saaj.jar</p> </li>
     <li><p>wsdl4j.jar</p> </li>
     <li><p>xalan.jar</p> </li>
     <li><p>xbean.jar</p> </li>
     <li><p>xercesImpl.jar</p> </li>
     <li><p>adobe-forms-client.jar</p> </li>
     <li><p>adobe-reader-extensions-client.jar</p> </li>
     <li><p>adobe-signatures-client.jar</p> </li>
    </ul> </td>
  </tr> xmp-tur
 </tbody>
</table>

### Uppgraderar JAR-filer {#upgrading-jar-files}

Om du uppgraderar från LiveCycle till AEM Forms bör du inkludera AEM Forms JAR-filerna i Java-projektets klassökväg. Om du till exempel använder tjänster som Rights Management, stöter du på ett kompatibilitetsproblem om du inte inkluderar AEM Forms JAR-filer i klassökvägen.

Anta att du uppgraderar till AEM Forms. Om du vill använda ett Java-program som anropar Rights Management-tjänsten inkluderar du AEM Forms-versionerna av följande JAR-filer:

* adobe-rightsmanagement-client.jar
* adobe-livecycle-client.jar
* adobe-usermanager-client.jar

**Se även**

[Anropa AEM-formulär med Java API](invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[Ange anslutningsegenskaper](invoking-aem-forms-using-java.md#setting-connection-properties)

[Skicka data till AEM Forms-tjänster med Java API](invoking-aem-forms-using-java.md#passing-data-to-aem-forms-services-using-the-java-api)

[Anropa en tjänst med ett Java-klientbibliotek](invoking-aem-forms-using-java.md#invoking-a-service-using-a-java-client-library)

## Ange anslutningsegenskaper {#setting-connection-properties}

Du ställer in anslutningsegenskaper för att anropa AEM Forms när du använder Java API. När du anger anslutningsegenskaper anger du om tjänsterna ska anropas från fjärrdatorn eller lokalt, och anger även anslutnings- och autentiseringsvärden. Autentiseringsvärden krävs om tjänstsäkerhet är aktiverat. Om tjänstsäkerhet är inaktiverad behöver du inte ange autentiseringsvärden.

Anslutningsläget kan antingen vara SOAP- eller EJB-läge. I EJB-läget används RMI/IIOP-protokollet, och prestanda för EJB-läget är bättre än för SOAP-läget. SOAP-läget används för att ta bort ett J2EE-serverberoende eller när en brandvägg finns mellan AEM Forms och klientprogrammet. SOAP-läget använder https-protokollet som underliggande transport och kan kommunicera över brandväggsgränserna. Om varken ett J2EE-programserverberoende eller en brandvägg är ett problem rekommenderar vi att du använder EJB-läget.

Om du vill anropa en AEM Forms-tjänst anger du följande anslutningsegenskaper:

* **** DSC_DEFAULT_EJB_ENDPOINT: Om du använder EJB-anslutningsläget representerar det här värdet webbadressen till J2EE-programservern där AEM Forms distribueras. Om du vill fjärranropa AEM Forms anger du det J2EE-programservernamn på vilket AEM Forms distribueras. Om klientprogrammet finns på samma J2EE-programserver kan du ange `localhost`. Beroende på vilken J2EE-programserver AEM Forms distribueras på anger du ett av följande värden:

   * JBoss: `https://<ServerName>:8080 (default port)`
   * WebSphere: `iiop://<ServerName>:2809 (default port)`
   * WebLogic: `t3://<ServerName>:7001 (default port)`

* **DSC_DEFAULT_SOAP_ENDPOINT**: Om du använder SOAP-anslutningsläget representerar det här värdet slutpunkten dit en anropsbegäran skickas. Om du vill fjärranropa AEM Forms anger du det J2EE-programservernamn på vilket AEM Forms distribueras. Om klientprogrammet finns på samma J2EE-programserver kan du ange `localhost` (till exempel `http://localhost:8080`.)

   * Portvärdet `8080` gäller om J2EE-programmet är JBoss. Om J2EE-programservern är IBM® WebSphere® ska du använda port `9080`. Om J2EE-programservern är WebLogic använder du port `7001`. (Dessa värden är standardportvärden. Om du ändrar portvärdet använder du det tillämpliga portnumret.)

* **DSC_TRANSPORT_PROTOCOL**: Om du använder EJB-anslutningsläget anger du `ServiceClientFactoryProperties.DSC_EJB_PROTOCOL` det här värdet. Om du använder SOAP-anslutningsläget anger du `ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL`.
* **DSC_SERVER_TYPE**: Anger den J2EE-programserver där AEM Forms distribueras. Giltiga värden är `JBoss`, `WebSphere`, `WebLogic`.

   * Om du ställer in den här anslutningsegenskapen på `WebSphere`ställs `java.naming.factory.initial` värdet in på `com.ibm.ws.naming.util.WsnInitCtxFactory`.
   * Om du ställer in den här anslutningsegenskapen på `WebLogic`ställs `java.naming.factory.initial` värdet in på `weblogic.jndi.WLInitialContextFactory`.
   * Om du anger den här anslutningsegenskapen som `JBoss`, anges också `java.naming.factory.initial` värdet till `org.jnp.interfaces.NamingContextFactory`.
   * Du kan ställa in egenskapen på ett värde som uppfyller dina krav om du inte vill använda standardvärdena. `java.naming.factory.initial`
   ***Obs**! I stället för att använda en sträng för att ange `DSC_SERVER_TYPE` anslutningsegenskapen kan du använda en statisk medlem av `ServiceClientFactoryProperties` klassen. Följande värden kan användas: `ServiceClientFactoryProperties.DSC_WEBSPHERE_SERVER_TYPE`, `ServiceClientFactoryProperties.DSC_WEBLOGIC_SERVER_TYPE`eller `ServiceClientFactoryProperties.DSC_JBOSS_SERVER_TYPE`.

* **** DSC_CREDENTIAL_USERNAME: Anger användarnamnet för AEM-formulär. För att en användare ska kunna anropa en AEM Forms-tjänst måste användaren ha användarrollen Tjänster. En användare kan även ha en annan roll som inkluderar behörigheten Tjänstanrop. Annars genereras ett undantag när de försöker anropa en tjänst. Om tjänstsäkerhet är inaktiverad behöver du inte ange den här anslutningsegenskapen.
* **** DSC_CREDENTIAL_PASSWORD: Anger motsvarande lösenordsvärde. Om tjänstsäkerhet är inaktiverad behöver du inte ange den här anslutningsegenskapen.
* **** DSC_REQUEST_TIMEOUT: Standardtidsgränsen för begäran för SOAP-begäran är 1200000 millisekunder (20 minuter). Ibland kan en begäran ta längre tid att slutföra åtgärden. En SOAP-begäran som hämtar en stor uppsättning poster kan till exempel kräva en längre tidsgräns. Du kan använda för `ServiceClientFactoryProperties.DSC_REQUEST_TIMEOUT` att öka tidsgränsen för begärandeanrop för SOAP-begäranden.

   **Obs**! Endast SOAP-baserade anrop stöder egenskapen DSC_REQUEST_TIMEOUT.

Utför följande åtgärder för att ange anslutningsegenskaper:

1. Skapa ett `java.util.Properties` objekt med hjälp av dess konstruktor.
1. Om du vill ange egenskapen `DSC_DEFAULT_EJB_ENDPOINT` connection anropar du `java.util.Properties` objektets `setProperty` metod och skickar följande värden:

   * Uppräkningsvärdet `ServiceClientFactoryProperties.DSC_DEFAULT_EJB_ENDPOINT`
   * Ett strängvärde som anger URL:en för J2EE-programservern som är värd för AEM Forms
   >[!NOTE]
   >
   >Om du använder SOAP-anslutningsläget anger du `ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT` uppräkningsvärdet i stället för `ServiceClientFactoryProperties.DSC_DEFAULT_EJB_ENDPOINT` uppräkningsvärdet.

1. Om du vill ange egenskapen `DSC_TRANSPORT_PROTOCOL` connection anropar du `java.util.Properties` objektets `setProperty` metod och skickar följande värden:

   * Uppräkningsvärdet `ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL`
   * Uppräkningsvärdet `ServiceClientFactoryProperties.DSC_EJB_PROTOCOL`
   >[!NOTE]
   >
   >Om du använder SOAP-anslutningsläget anger du `ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL`uppräkningsvärdet i stället för `ServiceClientFactoryProperties.DSC_EJB_PROTOCOL` uppräkningsvärdet.

1. Om du vill ange egenskapen `DSC_SERVER_TYPE` connection anropar du `java.util.Properties` objektets `setProperty` metod och skickar följande värden:

   * Uppräkningsvärdet `ServiceClientFactoryProperties.DSC_SERVER_TYPE`
   * Ett strängvärde som anger den J2EE-programserver som är värd för AEM Forms (om t.ex. AEM Forms distribueras på JBoss anger du `JBoss`).

      1. Om du vill ange egenskapen `DSC_CREDENTIAL_USERNAME` connection anropar du `java.util.Properties` objektets `setProperty` metod och skickar följande värden:
   * Uppräkningsvärdet `ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME`
   * Ett strängvärde som anger det användarnamn som krävs för att anropa AEM Forms

      1. Om du vill ange egenskapen `DSC_CREDENTIAL_PASSWORD` connection anropar du `java.util.Properties` objektets `setProperty` metod och skickar följande värden:
   * Uppräkningsvärdet `ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD`
   * Ett strängvärde som anger motsvarande lösenordsvärde



**Ställa in EJB-anslutningsläget för JBoss**

I följande Java-kodexempel ställs anslutningsegenskaperna in så att AEM Forms anropas som distribueras på JBoss och EJB-anslutningsläget används.

```java
 Properties ConnectionProps = new Properties();
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_EJB_ENDPOINT, "https://<hostname>:8080");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_EJB_PROTOCOL);
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_DOCUMENT_HTTP_ENDPOINT,"https://<hostname>:8080");
```

**Ställa in EJB-anslutningsläget för WebLogic**

I följande Java-kodexempel ställs anslutningsegenskaperna in så att AEM-formulär som distribueras på WebLogic anropas och EJB-anslutningsläget används.

```as3
 Properties ConnectionProps = new Properties();
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_EJB_ENDPOINT, "t3://localhost:7001");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_EJB_PROTOCOL);
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "WebLogic");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
```

**Ställa in EJB-anslutningsläget för WebSphere**

I följande Java-kodexempel ställs anslutningsegenskaperna in så att AEM Forms anropas som distribuerats på WebSphere och som använder EJB-anslutningsläget.

```as3
 Properties ConnectionProps = new Properties();
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_EJB_ENDPOINT, "iiop://localhost:2809");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_EJB_PROTOCOL);
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "WebSphere");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
```

**Ställa in SOAP-anslutningsläget**

I följande Java-kodexempel ställs anslutningsegenskaper in i SOAP-läge så att AEM Forms anropas som distribueras på JBoss.

```as3
 Properties ConnectionProps = new Properties();
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "http://localhost:8080");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
```

>[!NOTE]
>
>Om du väljer SOAP-anslutningsläget måste du ta med ytterligare JAR-filer i klientprogrammets klasssökväg.

**Ange anslutningsegenskaper när tjänstsäkerhet är inaktiverat**

I följande Java-kodexempel ställs anslutningsegenskaper in som krävs för att anropa AEM Forms som distribueras på JBoss Application Server och när tjänstsäkerhet är inaktiverat.

```as3
 Properties ConnectionProps = new Properties();
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_EJB_ENDPOINT, "jnp://localhost:1099");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_EJB_PROTOCOL);
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
```

>[!NOTE]
>
>Alla Java Quick Starts som är kopplade till programmering med AEM Forms visar både EJB- och SOAP-anslutningsinställningar.

**Ställa in SOAP-anslutningsläget med tidsgräns för anpassad begäran**

```as3
 Properties ConnectionProps = new Properties();
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "http://localhost:8080");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_REQUEST_TIMEOUT, "1800000"); // Request timeout limit 30 Minutes
```

**Anropa AEM Forms med ett Context-objekt**

Du kan använda ett `com.adobe.idp.Context` objekt för att anropa en AEM Forms-tjänst med en autentiserad användare (objektet `com.adobe.idp.Context` representerar en autentiserad användare). När du använder ett `com.adobe.idp.Context` objekt behöver du inte ange egenskaperna `DSC_CREDENTIAL_USERNAME` eller `DSC_CREDENTIAL_PASSWORD` . Du kan hämta ett `com.adobe.idp.Context` objekt när du autentiserar användare med hjälp av `AuthenticationManagerServiceClient` objektets `authenticate` metod.

Metoden returnerar `authenticate` ett `AuthResult` objekt som innehåller autentiseringsresultatet. Du kan skapa ett `com.adobe.idp.Context` objekt genom att anropa dess konstruktor. Anropa sedan `com.adobe.idp.Context` objektets `initPrincipal` -metod och skicka `AuthResult` objektet, vilket visas i följande kod:

```as3
 Context myCtx = new Context();
 myCtx.initPrincipal(authResult);
```

I stället för att ställa in `DSC_CREDENTIAL_USERNAME` - eller `DSC_CREDENTIAL_PASSWORD` -egenskaperna kan du anropa `ServiceClientFactory` objektets `setContext` metod och skicka `com.adobe.idp.Context` objektet. När du använder en AEM-formuläranvändare för att anropa en tjänst måste du se till att de har den roll som krävs för `Services User` att anropa en AEM Forms-tjänst.

I följande kodexempel visas hur du använder ett `com.adobe.idp.Context` objekt i anslutningsinställningarna för att skapa ett `EncryptionServiceClient` objekt.

```as3
 //Authenticate a user and use the Context object within connection settings
 // Authenticate the user
 String username = "wblue";
 String password = "password";
 AuthResult authResult = authClient.authenticate(username, password.getBytes());
 
 //Set a Content object that represents the authenticated user
 //Use the Context object to invoke the Encryption service
 Context myCtx = new Context();
 myCtx.initPrincipal(authResult);
 
 //Set connection settings
 Properties connectionProps = new Properties();
 connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_EJB_ENDPOINT, "jnp://<server>:1099");
 connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL, ServiceClientFactoryProperties.DSC_EJB_PROTOCOL);
 connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, ServiceClientFactoryProperties.DSC_JBOSS_SERVER_TYPE);
 connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DOCUMENT_HTTP_ENDPOINT,"jnp://<server>:1099");

 
 //Create a ServiceClientFactory object
 ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 myFactory.setContext(myCtx);
 
 //Create an EncryptionServiceClient object
 EncryptionServiceClient encryptClient  = new EncryptionServiceClient(myFactory);
```

>[!NOTE]
>
>Fullständig information om hur du autentiserar en användare finns i [Autentisera användare](/help/forms/developing/users.md#authenticating-users).

### Anropa scenarier {#invoking_scenarios-1}

Följande scenarier beskrivs i det här avsnittet:

* Ett klientprogram som körs i en egen JVM (Java Virtual Machine) anropar en fristående AEM Forms-instans.
* Ett klientprogram som körs i en egen JVM anropar grupperade AEM Forms-instanser.

### Klientprogram som anropar en fristående AEM Forms-instans {#client-application-invoking-a-stand-alone-aem-forms-instance}

I följande diagram visas ett klientprogram som körs i en egen JVM och som anropar en fristående AEM Forms-instans.

I det här scenariot körs ett klientprogram i sin egen JVM och anropar AEM Forms-tjänster.

>[!NOTE]
>
>Det här scenariot är det scenario som alla snabbstarter baseras på.

### Klientprogram som anropar grupperade AEM Forms-instanser {#client-application-invoking-clustered-aem-forms-instances}

I följande diagram visas ett klientprogram som körs i en egen JVM och som anropar AEM Forms-instanser i ett kluster.

Detta scenario liknar ett klientprogram som anropar en fristående AEM Forms-instans. Leverantörens URL är dock annorlunda. Om ett klientprogram vill ansluta till en specifik J2EE-programserver måste programmet ändra URL:en så att den refererar till den specifika J2EE-programservern.

Att referera till en specifik J2EE-programserver rekommenderas inte eftersom anslutningen mellan klientprogrammet och AEM Forms avbryts om programservern avbryts. Vi rekommenderar att provider-URL refererar till en JNDI-hanterare på cellnivå i stället för en specifik J2EE-programserver.

Klientprogram som använder SOAP-anslutningsläget kan använda HTTP-belastningsutjämnarporten för klustret. Klientprogram som använder EJB-anslutningsläget kan ansluta till EJB-porten för en viss J2EE-programserver. Den här åtgärden hanterar belastningsutjämning mellan klusternoder.

**WebSphere**

I följande exempel visas innehållet i en jndi.properties-fil som används för att ansluta till AEM Forms som distribueras på WebSphere.

```as3
 java.naming.factory.initial=com.ibm.websphere.naming.
 WsnInitialContextFactory
 java.naming.provider.url=corbaloc::appserver1:9810,:appserver2:9810
```

**WebLogic**

I följande exempel visas innehållet i en jndi.properties-fil som används för att ansluta till AEM Forms som distribueras på WebLogic.

```as3
 java.naming.factory.initial=weblogic.jndi.WLInitialContextFactory
 java.naming.provider.url=t3://appserver1:8001, appserver2:8001
```

**JBoss**

I följande exempel visas innehållet i en jndi.properties-fil som används för att ansluta till AEM Forms som distribueras på JBoss.

```as3
 java.naming.factory.initial= org.jnp.interfaces.NamingContextFactory
 java.naming.provider.url= jnp://appserver1:1099, appserver2:1099,
 appserver3:1099
```

>[!NOTE]
>
>Kontakta administratören för att fastställa J2EE-programserverns namn och portnummer.

**Se även**

[Inkludera AEM Forms Java-biblioteksfiler](invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Skicka data till AEM Forms-tjänster med Java API](invoking-aem-forms-using-java.md#passing-data-to-aem-forms-services-using-the-java-api)

[Anropa en tjänst med ett Java-klientbibliotek](invoking-aem-forms-using-java.md#invoking-a-service-using-a-java-client-library)

## Skicka data till AEM Forms-tjänster med Java API {#passing-data-to-aem-forms-services-using-the-java-api}

AEM Forms-tjänster använder eller producerar vanligtvis PDF-dokument. När du anropar en tjänst kan det ibland vara nödvändigt att skicka ett PDF-dokument (eller andra dokumenttyper som XML-data) till tjänsten. Ibland är det också nödvändigt att hantera ett PDF-dokument som returneras från tjänsten. Java-klassen som gör att du kan skicka data till och från AEM Forms-tjänster är `com.adobe.idp.Document`.

AEM Forms-tjänster accepterar inte PDF-dokument som andra datatyper, till exempel ett `java.io.InputStream` objekt eller en bytearray. Ett `com.adobe.idp.Document` objekt kan också användas för att skicka andra typer av data, till exempel XML-data, till tjänster.

Ett `com.adobe.idp.Document` objekt är en Java-serialiserbar typ, så det kan skickas via ett RMI-anrop. Mottagande sida kan sorteras (samma värd, samma klassinläsare), lokal (samma värd, annan klassinläsare) eller fjärransluten (en annan värd). Dokumentinnehållet är optimerat för varje enskilt fall. Om till exempel avsändaren och mottagaren finns på samma värd, överförs innehållet via ett lokalt filsystem. (I vissa fall kan dokument skickas i minnet.)

Beroende på `com.adobe.idp.Document` objektstorleken, överförs data inom `com.adobe.idp.Document` objektet eller lagras i serverns filsystem. Eventuella tillfälliga lagringsresurser som upptas av `com.adobe.idp.Document` objektet tas automatiskt bort när det `com.adobe.idp.Document` kasseras. (Se [Disponera dokumentobjekt](invoking-aem-forms-using-java.md#disposing-document-objects).)

Ibland är det nödvändigt att känna till innehållstypen för ett `com.adobe.idp.Document` objekt innan du kan skicka det till en tjänst. Om en åtgärd t.ex. kräver en viss innehållstyp, `application/pdf`rekommenderar vi att du bestämmer innehållstypen. (Se [Bestämma innehållstypen för ett dokument](invoking-aem-forms-using-java.md#determining-the-content-type-of-a-document).)

Objektet försöker `com.adobe.idp.Document` att bestämma innehållstypen med hjälp av angivna data. Om innehållstypen inte kan hämtas från de data som anges (till exempel när data har angetts som en bytearray), anger du innehållstypen. Om du vill ange innehållstypen anropar du `com.adobe.idp.Document` objektets `setContentType` metod. (Se [Bestämma innehållstypen för ett dokument](invoking-aem-forms-using-java.md#determining-the-content-type-of-a-document))

Om det finns flera filer i samma filsystem går det snabbare att skapa ett `com.adobe.idp.Document` objekt. Om det finns filer som kan användas i fjärranslutna filsystem måste en kopieringsåtgärd utföras, vilket påverkar prestandan.

Ett program kan innehålla både `com.adobe.idp.Document` - och `org.w3c.dom.Document` datatyper. Se dock till att du kvalificerar `org.w3c.dom.Document` datatypen fullständigt. Mer information om hur du konverterar ett `org.w3c.dom.Document` objekt till ett `com.adobe.idp.Document` objekt finns i [Snabbstart (EJB-läge): Fylla i formulär i förväg med flödeslayouter med Java API](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-prepopulating-forms-with-flowable-layouts-using-the-java-api).

>[!NOTE]
>
>Om du vill förhindra en minnesläcka i WebLogic när du använder ett `com.adobe.idp.Document` objekt läser du dokumentinformationen i segment om högst 2 048 byte. Följande kod läser dokumentinformationen i segment om 2 048 byte:

```as3
        // Set up the chunk size to prevent a potential memory leak
        int buffSize = 2048;
 
        // Determine the total number of bytes to read
        int docLength = (int) inDoc.length();
        byte [] byteDoc = new byte[docLength];
 
        // Set up the reading position
        int pos = 0;
 
        // Loop through the document information, 2048 bytes at a time
        while (docLength > 0) {
      // Read the next chunk of information
            int toRead = Math.min(buffSize, docLength);
            int bytesRead = inDoc.read(pos, byteDoc, pos, toRead);
 
            // Handle the exception in case data retrieval failed
            if (bytesRead == -1) {
 
                inDoc.doneReading();
                inDoc.dispose();
                throw new RuntimeException("Data retrieval failed!");
 
            }
 
             // Update the reading position and number of bytes remaining
             pos += bytesRead;
             docLength -= bytesRead;
 
        }
 
        // The document information has been successfully read
        inDoc.doneReading();
        inDoc.dispose();
```

**Se även**

[Anropa AEM-formulär med Java API](invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[Ange anslutningsegenskaper](invoking-aem-forms-using-java.md#setting-connection-properties)

### Skapa dokument {#creating-documents}

Skapa ett `com.adobe.idp.Document` objekt innan du anropar en tjänståtgärd som kräver ett PDF-dokument (eller andra dokumenttyper) som indatavärde. Klassen innehåller konstruktorer som gör att du kan skapa ett dokument av följande innehållstyper: `com.adobe.idp.Document`

* En bytearray
* Ett befintligt `com.adobe.idp.Document` objekt
* Ett `java.io.File` objekt
* Ett `java.io.InputStream` objekt
* Ett `java.net.URL` objekt

#### Skapa ett dokument baserat på en bytearray {#creating-a-document-based-on-a-byte-array}

I följande kodexempel skapas ett `com.adobe.idp.Document` objekt som baseras på en bytearray.

**Skapa ett Document-objekt som baseras på en bytearray**

```as3
 Document myPDFDocument = new Document(myByteArray);
```

#### Skapa ett dokument baserat på ett annat dokument {#creating-a-document-based-on-another-document}

I följande kodexempel skapas ett `com.adobe.idp.Document` objekt som är baserat på ett annat `com.adobe.idp.Document` objekt.

**Skapa ett Document-objekt som baseras på ett annat dokument**

```as3
 //Create a Document object based on a byte array
 InputStream is = new FileInputStream("C:\\Map.pdf");
 int len = is.available();
 byte [] myByteArray = new byte[len];
 int i = 0;
 while (i < len) {
       i += is.read(myByteArray, i, len);
 }
 Document myPDFDocument = new Document(myByteArray);
 
 //Create another Document object
 Document anotherDocument = new Document(myPDFDocument);
```

#### Skapa ett dokument baserat på en fil {#creating-a-document-based-on-a-file}

I följande kodexempel skapas ett `com.adobe.idp.Document` objekt som baseras på en PDF-fil med namnet *map.pdf*. Den här filen finns i roten på hårddisken C. Den här konstruktorn försöker ange MIME-innehållstypen för `com.adobe.idp.Document` objektet med filnamnstillägget.

Konstruktorn som accepterar ett `com.adobe.idp.Document` `java.io.File` objekt accepterar också en Boolean-parameter. Genom att ställa in den här parametern på `true`tar `com.adobe.idp.Document` objektet bort filen. Den här åtgärden innebär att du inte behöver ta bort filen när du har skickat den till `com.adobe.idp.Document` konstruktorn.

Om du ställer in den här parametern på `false` innebär det att du behåller äganderätten till filen. Det `true` är effektivare att ställa in den här parametern på. Orsaken är att `com.adobe.idp.Document` objektet kan flytta filen direkt till det lokala hanterade området i stället för att kopiera den (vilket är långsammare).

**Skapa ett Document-objekt som bygger på en PDF-fil**

```as3
 //Create a Document object based on the map.pdf source file
 File mySourceMap = new File("C:\\map.pdf");
 Document myPDFDocument = new Document(mySourceMap,true);
```

#### Skapa ett dokument baserat på ett InputStream-objekt {#creating-a-document-based-on-an-inputstream-object}

I följande Java-kodexempel skapas ett `com.adobe.idp.Document` objekt som är baserat på ett `java.io.InputStream` objekt.

**Skapa ett dokument baserat på ett InputStream-objekt**

```as3
 //Create a Document object based on an InputStream object
 InputStream is = new FileInputStream("C:\\Map.pdf");
 Document myPDFDocument = new Document(is);
```

#### Skapa ett dokument baserat på innehåll som är tillgängligt från en URL {#creating-a-document-based-on-content-accessible-from-an-url}

I följande Java-kodexempel skapas ett `com.adobe.idp.Document` objekt som är baserat på en PDF-fil med namnet *map.pdf*. Den här filen finns i ett webbprogram med namnet `WebApp` som körs på `localhost`. Den här konstruktorn försöker ange `com.adobe.idp.Document` objektets MIME-innehållstyp med den innehållstyp som returneras med URL-protokollet.

URL:en som anges för `com.adobe.idp.Document` objektet läses alltid vid den sida där det ursprungliga `com.adobe.idp.Document` objektet skapas, vilket visas i det här exemplet:

```as3
     Document doc = new Document(new java.net.URL("file:c:/temp/input.pdf"));
```

Filen c:/temp/input.pdf måste finnas på klientdatorn (inte på serverdatorn). Klientdatorn är där URL:en läses och var `com.adobe.idp.Document` objektet skapades.

**Skapa ett dokument baserat på innehåll som är tillgängligt från en URL**

```as3
 //Create a Document object based on a java.net.URL object
 URL myURL = new URL("http", "localhost", 8080,"/WebApp/map.pdf");
 
 //Create another Document object
 Document myPDFDocument = new Document(myURL);
```

**Se även**

[Anropa AEM-formulär med Java API](invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[Ange anslutningsegenskaper](invoking-aem-forms-using-java.md#setting-connection-properties)

### Hantera returnerade dokument {#handling-returned-documents}

Tjänståtgärder som returnerar ett PDF-dokument (eller andra datatyper som XML-data) som ett utdatavärde returnerar ett `com.adobe.idp.Document` objekt. När du har tagit emot ett `com.adobe.idp.Document` objekt kan du konvertera det till följande format:

* Ett `java.io.File` objekt
* Ett `java.io.InputStream` objekt
* En bytearray

Följande kodrad konverterar ett `com.adobe.idp.Document` objekt till ett `java.io.InputStream` objekt. Anta att det `myPDFDocument` representerar ett `com.adobe.idp.Document` objekt:

```as3
     java.io.InputStream resultStream = myDocument.getInputStream();
```

På samma sätt kan du kopiera innehållet i en fil `com.adobe.idp.Document` till en lokal fil genom att utföra följande åtgärder:

1. Create a `java.io.File` object.
1. Anropa `com.adobe.idp.Document` objektets `copyToFile` metod och skicka `java.io.File`objektet.

I följande kodexempel kopieras innehållet i ett `com.adobe.idp.Document` objekt till en fil med namnet *OtherMap.pdf*.

**Kopiera innehållet i ett dokumentobjekt till en fil**

```as3
 File outFile = new File("C:\\AnotherMap.pdf");
 myDocument.copyToFile (outFile);
```

**Se även**

[Anropa AEM-formulär med Java API](invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[Ange anslutningsegenskaper](invoking-aem-forms-using-java.md#setting-connection-properties)

### Bestämma innehållstypen för ett dokument {#determining-the-content-type-of-a-document}

Bestäm MIME-typen för ett `com.adobe.idp.Document` objekt genom att anropa `com.adobe.idp.Document` objektets `getContentType` metod. Den här metoden returnerar ett strängvärde som anger innehållstypen för `com.adobe.idp.Document` objektet. I följande tabell beskrivs de olika innehållstyper som returneras av AEM Forms.

<table>
 <thead>
  <tr>
   <th><p>MIME-typ</p></th>
   <th><p>Beskrivning</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p><code>application/pdf</code></p></td>
   <td><p>PDF-dokument</p></td>
  </tr>
  <tr>
   <td><p><code>application/vnd.adobe.xdp+xml</code></p></td>
   <td><p>XML Data Packaging (XDP), som används för exporterade XFA-formulär (XML Forms Architecture)</p></td>
  </tr>
  <tr>
   <td><p><code>text/xml</code></p></td>
   <td><p>Bokmärken, bilagor eller andra XML-dokument</p></td>
  </tr>
  <tr>
   <td><p><code>application/vnd.fdf</code></p></td>
   <td><p>Forms Data Format (FDF), som används för exporterade Acrobat-formulär</p></td>
  </tr>
  <tr>
   <td><p><code>application/vnd.adobe.xfdf</code></p></td>
   <td><p>XFDF (XML Forms Data Format), som används för exporterade Acrobat-formulär</p></td>
  </tr>
  <tr>
   <td><p><code>application/rdf+xml</code></p></td>
   <td><p>Rikt dataformat och XML</p></td>
  </tr>
  <tr>
   <td><p><code>application/octet-stream</code></p></td>
   <td><p>Allmänt dataformat</p></td>
  </tr>
  <tr>
   <td><p><code>NULL</code></p></td>
   <td><p>Ospecificerad MIME-typ</p></td>
  </tr>
 </tbody>
</table>

Följande kodexempel avgör innehållstypen för ett `com.adobe.idp.Document` objekt.

**Bestämma innehållstypen för ett Document-objekt**

```as3
 //Determine the content type of the Document object
 String ct = myDocument.getContentType();
 System.out.println("The content type of the Document object is " +ct);
```

**Se även**

[Anropa AEM-formulär med Java API](invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[Ange anslutningsegenskaper](invoking-aem-forms-using-java.md#setting-connection-properties)

### Disponera dokumentobjekt {#disposing-document-objects}

När du inte längre behöver ett `Document` objekt bör du ta bort det genom att anropa dess `dispose` metod. Varje `Document` objekt förbrukar en filbeskrivning och så mycket som 75 MB RAM-utrymme på programmets värdplattform. Om ett `Document` objekt inte tas bort tas det bort av Java Garage-samlingsprocessen. Om du däremot tar bort den tidigare genom att använda `dispose` metoden kan du frigöra det minne som upptas av `Document` objektet.

**Se även**

[Anropa AEM-formulär med Java API](invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[Inkludera AEM Forms Java-biblioteksfiler](invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Anropa en tjänst med ett Java-klientbibliotek](invoking-aem-forms-using-java.md#invoking-a-service-using-a-java-client-library)

## Anropa en tjänst med ett Java-klientbibliotek {#invoking-a-service-using-a-java-client-library}

AEM Forms-tjänståtgärder kan anropas med hjälp av en tjänsts starkt typbestämda API, som kallas Java-klientbibliotek. Ett *Java-klientbibliotek* är en uppsättning konkreta klasser som ger åtkomst till tjänster som distribueras i tjänstbehållaren. Du instansierar ett Java-objekt som representerar tjänsten som ska anropas i stället för att skapa ett `InvocationRequest` objekt med anrops-API:t. Anrops-API:t används för att anropa processer, till exempel långvariga processer, som skapats i Workbench. (Se [Anropa humancentrerade, långvariga processer](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes).)

Om du vill utföra en tjänståtgärd anropar du en metod som tillhör Java-objektet. Ett Java-klientbibliotek innehåller metoder som vanligtvis mappar en-till-en med serviceåtgärder. Ange nödvändiga anslutningsegenskaper när du använder ett Java-klientbibliotek. (Se [Ange anslutningsegenskaper](invoking-aem-forms-using-java.md#setting-connection-properties).)

När du har angett anslutningsegenskaper skapar du ett `ServiceClientFactory` objekt som används för att instansiera ett Java-objekt som gör att du kan anropa en tjänst. Varje tjänst som har ett Java-klientbibliotek har ett motsvarande klientobjekt. Om du till exempel vill anropa tjänsten Databas skapar du ett `ResourceRepositoryClient` objekt med hjälp av dess konstruktor och skickar `ServiceClientFactory` objektet. Objektet ansvarar `ServiceClientFactory` för att upprätthålla de anslutningsinställningar som krävs för att anropa AEM Forms-tjänster.

Även om det oftast går snabbt att få en produkt `ServiceClientFactory` är det en del omkostnader som uppstår när fabriken används för första gången. Objektet är optimerat för återanvändning och därför, när det är möjligt, ska du använda samma `ServiceClientFactory` objekt när du skapar flera Java-klientobjekt. Det vill säga, skapa inte ett separat `ServiceClientFactory` objekt för varje klientbiblioteksobjekt som du skapar.

Det finns en inställning för användarhantering som styr livslängden för SAML-försäkran som finns inuti `com.adobe.idp.Context` objektet som påverkar `ServiceClientFactory` objektet. Den här inställningen styr alla livstider för autentiseringskontext i AEM-formulär, inklusive alla anrop som utförs med Java API. Som standard är den tidsperiod under vilken ett `ServiceCleintFactory` objekt kan användas två timmar.

>[!NOTE]
>
>Databastjänstens åtgärd anropas för att förklara hur en tjänst ska anropas med Java API:t `writeResource` . Den här åtgärden placerar en ny resurs i databasen.

Du kan anropa databastjänsten med hjälp av ett Java-klientbibliotek och genom att utföra följande steg:

1. Inkludera JAR-klientfiler, till exempel adobe-database-client.jar, i Java-projektets klassökväg. Mer information om var dessa filer finns i [Inkludera Java-biblioteksfiler](invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)för AEM Forms.
1. Ange anslutningsegenskaper som krävs för att anropa en tjänst.
1. Skapa ett `ServiceClientFactory` objekt genom att anropa `ServiceClientFactory` objektets statiska `createInstance` metod och skicka `java.util.Properties` objektet som innehåller anslutningsegenskaper.
1. Skapa ett `ResourceRepositoryClient` objekt med hjälp av dess konstruktor och skicka `ServiceClientFactory` objektet. Använd objektet `ResourceRepositoryClient` för att anropa databastjänståtgärder.
1. Skapa ett `RepositoryInfomodelFactoryBean` objekt med hjälp av dess konstruktor och skicka `null`. Med det här objektet kan du skapa ett `Resource` objekt som representerar innehållet som läggs till i databasen.
1. Skapa ett `Resource` objekt genom att anropa `RepositoryInfomodelFactoryBean` objektets `newImage` metod och skicka följande värden:

   * Ett unikt ID-värde genom att ange `new Id()`.
   * Ett unikt UUID-värde genom att ange `new Lid()`.
   * Resursens namn. Du kan ange filnamnet för XDP-filen.
   Sänd returvärdet till `Resource`.

1. Skapa ett `ResourceContent` objekt genom att anropa `RepositoryInfomodelFactoryBean` objektets `newImage` metod och omvandla returvärdet till `ResourceContent`. Det här objektet representerar innehållet som läggs till i databasen.
1. Skapa ett `com.adobe.idp.Document` objekt genom att skicka ett `java.io.FileInputStream` objekt som lagrar XDP-filen som ska läggas till i databasen. (Se [Skapa ett dokument baserat på ett InputStream-objekt](invoking-aem-forms-using-java.md#creating-a-document-based-on-an-inputstream-object).)
1. Lägg till innehållet i `com.adobe.idp.Document` objektet till `ResourceContent` objektet genom att anropa `ResourceContent` objektets `setDataDocument` metod. Skicka `com.adobe.idp.Document` objektet.
1. Ange MIME-typen för XDP-filen som ska läggas till i databasen genom att anropa `ResourceContent` objektets `setMimeType` metod och skicka `application/vnd.adobe.xdp+xml`.
1. Lägg till innehållet i `ResourceContent` objektet till `Resource` objektet genom att anropa `Resource` objektets `setContent` metod och skicka `ResourceContent` objektet.
1. Lägg till en beskrivning av resursen genom att anropa `Resource` objektets `setDescription` metod och skicka ett strängvärde som representerar en beskrivning av resursen.
1. Lägg till formulärdesignen i databasen genom att anropa `ResourceRepositoryClient` objektets `writeResource` metod och skicka följande värden:

   * Ett strängvärde som anger sökvägen till resurssamlingen som innehåller den nya resursen
   * Det `Resource` objekt som skapades

**Se även**

[Snabbstart (EJB-läge): Skriva en resurs med Java API](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-writing-a-resource-using-the-java-api)

[Anropa AEM-formulär med Java API](invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[Inkludera AEM Forms Java-biblioteksfiler](invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

## Anropa en kort process med anrops-API {#invoking-a-short-lived-process-using-the-invocation-api}

Du kan anropa en kort process med Java Anvocation API. När du anropar en kortvarig process med anrops-API:t skickar du obligatoriska parametervärden med hjälp av ett `java.util.HashMap` objekt. För varje parameter som ska skickas till en tjänst anropar du `java.util.HashMap` objektets `put` metod och anger det namn/värde-par som krävs av tjänsten för att utföra den angivna åtgärden. Ange det exakta namnet på parametrarna som tillhör den kortvariga processen.

>[!NOTE]
>
>Mer information om hur du anropar en långvarig process finns i [Anropa humancentrerade, långvariga processer](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes).

Här handlar det om att använda anrops-API för att anropa följande kortlivade AEM Forms-process med namnet `MyApplication/EncryptDocument`.

>[!NOTE]
>
>Den här processen baseras inte på en befintlig AEM Forms-process. Om du vill följa med i kodexemplet skapar du en process med namnet `MyApplication/EncryptDocument` med Workbench. (Se [Använda Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63).)

När den här processen anropas utför den följande åtgärder:

1. Hämtar det oskyddade PDF-dokumentet som skickas till processen. Den här åtgärden baseras på `SetValue` åtgärden. Indataparametern för den här processen är en `document` processvariabel med namnet `inDoc`.
1. Krypterar PDF-dokumentet med ett lösenord. Den här åtgärden baseras på `PasswordEncryptPDF` åtgärden. Lösenordskrypterade PDF-dokument returneras i en processvariabel med namnet `outDoc`.

### Anropa den kortvariga processen MyApplication/EncryptDocument med hjälp av Java-anrops-API {#invoke-the-myapplication-encryptdocument-short-lived-process-using-the-java-invocation-api}

Anropa den `MyApplication/EncryptDocument` kortvariga processen med Java-API:t:

1. Inkludera JAR-klientfiler, t.ex. adobe-livecycle-client.jar, i Java-projektets klassökväg. (Se [Inkludera AEM Forms Java-biblioteksfiler](invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).)
1. Skapa ett `ServiceClientFactory` objekt som innehåller anslutningsegenskaper. (Se [Ange anslutningsegenskaper](invoking-aem-forms-using-java.md#setting-connection-properties).)
1. Skapa ett `ServiceClient` objekt med hjälp av dess konstruktor och skicka `ServiceClientFactory` objektet. Med ett `ServiceClient` objekt kan du anropa en tjänståtgärd. Det hanterar uppgifter som att hitta, skicka och dirigera anropsbegäranden.
1. Skapa ett `java.util.HashMap` objekt med hjälp av dess konstruktor.
1. Anropa `java.util.HashMap` objektets `put` metod för varje indataparameter för att skicka till den långvariga processen. Eftersom den `MyApplication/EncryptDocument` kortvariga processen kräver en indataparameter av typen `Document`, behöver du bara anropa `put` metoden en gång, vilket visas i följande exempel.

   ```as3
    //Create a Map object to store the parameter value for inDoc
    Map params = new HashMap();
    InputStream inFile = new FileInputStream("C:\\Adobe\Loan.pdf");
    Document inDoc = new Document(inFile);
    params.put("inDoc", inDoc);
   ```

1. Skapa ett `InvocationRequest` objekt genom att anropa `ServiceClientFactory` objektets `createInvocationRequest` metod och skicka följande värden:

   * Ett strängvärde som anger namnet på den långvariga process som ska anropas. Om du vill anropa `MyApplication/EncryptDocument` processen anger du `MyApplication/EncryptDocument`.
   * Ett strängvärde som representerar processåtgärdens namn. Vanligtvis är namnet på en kortlivad processåtgärd `invoke`.
   * Det `java.util.HashMap` objekt som innehåller de parametervärden som tjänståtgärden kräver.
   * Ett booleskt värde som anger `true`, vilket skapar en synkron begäran (det här värdet kan användas för att anropa en kortlivad process).

1. Skicka anropsbegäran till tjänsten genom att anropa `ServiceClient` objektets `invoke` metod och skicka `InvocationRequest` objektet. Metoden `invoke` returnerar ett `InvocationReponse` objekt.

   >[!NOTE]
   >
   >En långvarig process kan anropas genom att värdet skickas `false`som den fjärde parametern i `createInvocationRequest` metoden. Om du skickar värdet `false`*skapas en asynkron begäran.*

1. Hämta processens returvärde genom att anropa `InvocationReponse` objektets `getOutputParameter` metod och skicka ett strängvärde som anger utdataparameterns namn. I det här fallet anger du `outDoc` ( `outDoc` är namnet på `MyApplication/EncryptDocument` processens utdataparameter). Sänd returvärdet till `Document`, som i följande exempel.

   ```as3
    InvocationResponse response = myServiceClient.invoke(request);
    Document encryptDoc = (Document) response.getOutputParameter("outDoc");
   ```

1. Skapa ett `java.io.File` objekt och kontrollera att filtillägget är .pdf.
1. Anropa `com.adobe.idp.Document` objektets `copyToFile` metod för att kopiera innehållet i `com.adobe.idp.Document` objektet till filen. Se till att du använder det `com.adobe.idp.Document` objekt som returnerades av `getOutputParameter` metoden.

**Se även**

[Snabbstart:Anropa en kort process med anrops-API](/help/forms/developing/invocation-api-quick-starts.md#quick-start-invoking-a-short-lived-process-using-the-invocation-api)

[Anropa personalcentrerade, långlivade processer](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes)

[Inkludera AEM Forms Java-biblioteksfiler](invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)