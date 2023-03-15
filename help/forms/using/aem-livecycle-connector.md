---
title: Ansluta AEM Forms till Adobe LiveCycle
seo-title: Connecting AEM Forms with Adobe LiveCycle
description: Med AEM LiveCycle Connector kan du starta LiveCycle ES4 Document Services inifrån AEM program och arbetsflöden.
seo-description: AEM LiveCycle connector allows you to start LiveCycle ES4 Document Services from within AEM apps and workflows.
uuid: 7dc9d5ec-7b19-4d93-936d-81ceb45dfffa
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
discoiquuid: 7e404b45-1302-4dd1-b3c9-3f47fedb5f94
role: Admin
exl-id: 562f8a22-cbab-4915-bc0d-da9bea7d18fa
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '1006'
ht-degree: 0%

---

# Ansluta AEM Forms till Adobe LiveCycle {#connecting-aem-forms-with-adobe-livecycle}

Adobe Experience Manager (AEM) LiveCycle Connector gör det möjligt att smidigt anropa Adobe LiveCycle ES4 Document Services inifrån AEM webbprogram och arbetsflöden. LiveCycle har ett omfattande klient-SDK som gör att klientapplikationer kan starta LiveCycle-tjänster med Java API:er. AEM LiveCycle Connector förenklar användningen av dessa API:er i OSGi-miljön.

## Ansluta AEM till Adobe LiveCycle {#connecting-aem-server-to-adobe-livecycle}

AEM LiveCycle Connector är en del av [AEM Forms tilläggspaket](/help/forms/using/installing-configuring-aem-forms-osgi.md). När du har installerat AEM Forms-tilläggspaketet utför du följande steg för att lägga till information om LiveCycle-servern AEM webbkonsolen.

1. Gå AEM konfigurationshanteraren för webbkonsolen och leta reda på konfigurationskomponenten för Adobe-klient-SDK.
1. Klicka på komponenten för att redigera konfigurationsserverns URL-adress, användarnamn och lösenord.
1. Granska inställningarna och klicka på **Spara**.

Även om egenskaperna är självförklarande är de viktiga följande:

* **Server-URL** - Anger URL till LiveCycle-servern. Om du vill att LiveCycle och AEM ska kommunicera via https, kan du starta AEM med följande JVM

   ```java
   argument
    -Djavax.net.ssl.trustStore=<<em>path to LC keystore</em>>
   ```

   alternativ.

* **Användarnamn**- Anger användarnamnet för kontot som används för att upprätta kommunikation mellan AEM och LiveCycle. Kontot är ett LiveCycle-användarkonto som har behörighet att starta Document Services.
* **Lösenord**- Anger lösenordet.
* **Tjänstnamn** - Anger vilka tjänster som startas med de inloggningsuppgifter som anges i fälten Användarnamn och Lösenord. Som standard skickas inga autentiseringsuppgifter när LiveCycle-tjänster startas.

## Startar dokumenttjänster {#starting-document-services}

Klientprogram kan starta LiveCycle-tjänster med hjälp av ett Java API, Web Services, Remoting och REST. För Java-klienter kan programmet använda LiveCycle SDK. LiveCycle SDK tillhandahåller ett Java-API för fjärrstart av dessa tjänster. Om du till exempel vill konvertera ett Microsoft Word-dokument till PDF startar klienten GeneratePDFService. Anropsflödet består av följande steg:

1. Skapa en ServiceClientFactory-instans.
1. Varje tjänst tillhandahåller en klientklass. Om du vill starta en tjänst skapar du en klientinstans av tjänsten.
1. Starta tjänsten och bearbeta resultatet.

AEM LiveCycle Connector förenklar flödet genom att visa dessa klientinstanser som OSGi-tjänster som kan nås med vanliga OSGi-metoder. Kopplingen LiveCycle har följande funktioner:

* Klientinstanser som OSGi-tjänst: Klienterna som paketerats som OSGI-paket listas i [Dokumenttjänstlista](/help/forms/using/aem-livecycle-connector.md#p-document-services-list-p) -avsnitt. Varje klientjar registrerar klientinstansen som OSGi-tjänst med OSGi-tjänstregistret.
* Spridning av användarautentiseringsuppgifter: Den anslutningsinformation som krävs för att ansluta till LiveCycle-servern hanteras på en central plats.
* ServiceClientFactory-tjänst: Klientprogrammet kan starta processerna genom att komma åt ServiceClientFactory-instansen.

### Starta via tjänstreferenser från OSGi-tjänstregistret {#starting-via-service-references-from-osgi-service-registry}

Så här startar du en exponerad tjänst inifrån AEM:

1. Fastställ maven-beroenden. Lägg till beroende till klientens jar i filen maven pom.xml. Lägg till minst beroende i jars för adobe-livecycle-client och adobe-usermanager-client.

   ```xml
   <dependency>
     <groupId>com.adobe.livecycle</groupId>
     <artifactId>adobe-livecycle-client</artifactId>
     <version>11.0.0</version>
   </dependency>
   <dependency>
     <groupId>com.adobe.livecycle</groupId>
     <artifactId>adobe-usermanager-client</artifactId>
     <version>11.0.0</version>
   </dependency>
   <dependency>
     <groupId>com.adobe.livecycle</groupId>
     <artifactId>adobe-cq-integration-api</artifactId>
     <version>11.0.0</version>
   </dependency>
   ```

   Om du vill starta en tjänst lägger du till motsvarande Maven-beroende för tjänsten. En lista över beroenden finns i [Dokumenttjänstlista](/help/forms/using/aem-livecycle-connector.md#p-document-services-list-p). Lägg till exempel till följande beroende för tjänsten Generate PDF:

   ```xml
   <dependency>
     <groupId>com.adobe.livecycle</groupId>
     <artifactId>adobe-generatepdf-client</artifactId>
     <version>11.0.0</version>
   </dependency>
   ```

1. Hämta tjänstreferensen. Hämta en referens till tjänstinstansen. Om du skriver en Java-klass kan du använda kommentarerna för deklarativa tjänster.

   ```java
   import com.adobe.livecycle.generatepdf.client.GeneratePdfServiceClient;
   import com.adobe.livecycle.generatepdf.client.CreatePDFResult;
   import com.adobe.idp.Document;
   
   @Reference
   GeneratePdfServiceClient generatePDF;
   ...
   
   Resource r = resourceResolver.getResource("/path/tp/docx");
   Document sourceDoc = new Document(r.adaptTo(InputStream.class));
   CreatePDFResult result = generatePDF.createPDF2(
                       sourceDoc,
                       extension, //inputFileExtension
                       null, //fileTypeSettings
                       null, //pdfSettings
                       null, //securitySettings
                       settingsDoc, //settingsDoc
                       null //xmpDoc
               );
   ```

   Ovanstående kodfragment startar createPDF API för GeneratePdfServiceClient för konvertering av ett dokument till PDF. Du kan utföra liknande anrop i en JSP med följande kod. Den största skillnaden är att följande kod använder Sling ScriptHelper för att komma åt GeneratePdfServiceClient.

   ```jsp
   <%@ page import="com.adobe.livecycle.generatepdf.client.GeneratePdfServiceClient" %>
   <%@ page import="com.adobe.livecycle.generatepdf.client.CreatePDFResult" %>
   <%@ page import="com.adobe.idp.Document" %>
   
   GeneratePdfServiceClient generatePDF = sling.getService(GeneratePdfServiceClient.class);
   Document sourceDoc = ...
   CreatePDFResult result = generatePDF.createPDF2(
                       sourceDoc,
                       extension, //inputFileExtension
                       null, //fileTypeSettings
                       null, //pdfSettings
                       null, //securitySettings
                       settingsDoc, //settingsDoc
                       null //xmpDoc
               );
   ```

### Startar via ServiceClientFactory {#starting-via-serviceclientfactory}

Klassen ServiceClientFactory krävs i vissa fall. Du behöver till exempel ServiceClientFactory för att anropa processer.

```java
import com.adobe.livecycle.dsc.clientsdk.ServiceClientFactoryProvider;
import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;

@Reference
ServiceClientFactoryProvider scfProvider;

...
ServiceClientFactory scf = scfProvider.getDefaultServiceClientFactory();
...
```

## Stöd för RunAs {#runas-support}

Nästan alla dokumenttjänster i LiveCycle kräver autentisering. Du kan använda något av följande alternativ för att starta de här tjänsterna utan att ange specifika autentiseringsuppgifter i koden:

### Tillåtelselista-konfiguration {#allowlist-configuration}

SDK-konfigurationen för LiveCycle-klienten innehåller en inställning för tjänstnamn. Den här konfigurationen är en lista över tjänster som anropslogiken använder administratörsautentiseringsuppgifter för. Om du till exempel lägger till DirectoryManager-tjänster (som ingår i API:t för användarhantering) i den här listan, kan all klientkod använda tjänsten direkt och anropslagret skickar automatiskt de konfigurerade autentiseringsuppgifterna som en del av den begäran som skickas till LiveCycle-servern

### RunAsManager {#runasmanager}

Som en del av integreringen tillhandahålls en ny tjänst, RunAsManager. Det gör att du kan programmässigt styra de autentiseringsuppgifter som ska användas vid anrop till LiveCycle-servern.

```java
import com.adobe.livecycle.dsc.clientsdk.security.PasswordCredential;
import com.adobe.livecycle.dsc.clientsdk.security.PrivilegedAction;
import com.adobe.livecycle.dsc.clientsdk.security.RunAsManager;
import com.adobe.idp.dsc.registry.component.ComponentRegistry;

@Reference
private RunAsManager runAsManager;

List<Component> components = runAsManager.doPrivileged(new PrivilegedAction<List<Component>>() {
            public List<Component> run() {
                return componentRegistry.getComponents();
            }
        });
assertNotNull(components);
```

Om du vill skicka olika autentiseringsuppgifter kan du använda den överlagrade metoden som tar en PasswordCredential-instans.

```java
PasswordCredential credential = new PasswordCredential("administrator","password");
List<Component> components = runAsManager.doPrivileged(new PrivilegedAction<List<Component>>() {
    public List<Component> run() {
        return componentRegistry.getComponents();
    }
},credential);
```

### InvocationRequest, egenskap {#invocationrequest-property}

Om du anropar en process eller använder klassen ServiceClientFactory direkt och skapar en InvocationRequest, kan du ange en egenskap som anger att anropslagret ska använda konfigurerade autentiseringsuppgifter.

```java
import com.adobe.idp.dsc.InvocationResponse
import com.adobe.idp.dsc.InvocationRequest
import com.adobe.livecycle.dsc.clientsdk.ServiceClientFactoryProvider
import com.adobe.idp.dsc.clientsdk.ServiceClientFactory
import com.adobe.livecycle.dsc.clientsdk.InvocationProperties

ServiceClientFactoryProvider scfp = sling.getService(ServiceClientFactoryProvider.class)
ServiceClientFactory serviceClientFactory = scfp.getDefaultServiceClientFactory()
InvocationRequest ir = serviceClientFactory.createInvocationRequest("sample/LetterSubmissionProcess", "invoke", new HashMap(), true);

//Here we are invoking the request with system user
ir.setProperty(InvocationProperties.INVOKER_TYPE,InvocationProperties.INVOKER_TYPE_SYSTEM)

InvocationResponse response = serviceClientFactory.getServiceClient().invoke(ir);
```

## Dokumenttjänstlista {#document-services-list}

### Adobe LiveCycle Client SDK API bundle {#adobe-livecycle-client-sdk-api-bundle}

Följande tjänster är tillgängliga:

* com.adobe.idp.um.api.AuthenticationManager
* com.adobe.idp.um.api.DirectoryManager
* com.adobe.idp.um.api.AuthorizationManager
* com.adobe.idp.dsc.registry.service.ServiceRegistry
* com.adobe.idp.dsc.registry.component.ComponentRegistry

#### Maven-beroenden {#maven-dependencies}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-livecycle-client</artifactId>
  <version>11.0.0</version>
</dependency>
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-usermanager-client</artifactId>
  <version>11.0.0</version>
</dependency>
```

### Adobe LiveCycle Client SDK Bundle {#adobe-livecycle-client-sdk-bundle}

Följande tjänster är tillgängliga:

* com.adobe.livecycle.dsc.clientsdk.security.RunAsManager
* com.adobe.livecycle.dsc.clientsdk.ServiceClientFactoryProvider

#### Maven-beroenden {#maven-dependencies-1}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-livecycle-cq-integration-api</artifactId>
  <version>1.1.10</version>
</dependency>
```

### Klientpaket för Adobe TaskManager LiveCycle {#adobe-livecycle-taskmanager-client-bundle}

Följande tjänster är tillgängliga:

* com.adobe.idp.taskmanager.dsc.client.task.TaskManager
* com.adobe.idp.taskmanager.dsc.client.TaskManagerQueryService
* com.adobe.idp.taskmanager.dsc.client.queuemanager.QueueManager
* com.adobe.idp.taskmanager.dsc.client.emailsettings.EmailSettingService
* com.adobe.idp.taskmanager.dsc.client.endpoint.TaskManagerEndpointClient
* com.adobe.idp.taskmanager.dsc.client.userlist.UserlistService

#### Maven-beroenden {#maven-dependencies-2}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-taskmanager-client</artifactId>
  <version>11.0.0</version>
</dependency>
```

### Klientpaketet Adobe LiveCycle Workflow {#adobe-livecycle-workflow-client-bundle}

Följande tjänst är tillgänglig:

* com.adobe.idp.workflow.client.WorkflowServiceClient

#### Maven-beroenden {#maven-dependencies-3}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-workflow-client-sdk</artifactId>
  <version>11.0.0</version>
</dependency>
```

### Adobe LiveCycle PDF Generator Client bundle {#adobe-livecycle-pdf-generator-client-bundle}

Följande tjänst är tillgänglig:

* com.adobe.livecycle.generatepdf.client.GeneratePdfServiceClient

#### Maven-beroenden {#maven-dependencies-4}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-generatepdf-client</artifactId>
  <version>11.0.0</version>
</dependency>
```

### Klientpaket för Adobe LiveCycle Application Manager {#adobe-livecycle-application-manager-client-bundle}

Följande tjänster är tillgängliga:

* com.adobe.idp.applicationmanager.service.ApplicationManager
* com.adobe.livecycle.applicationmanager.client.ApplicationManager
* com.adobe.livecycle.design.service.DesigntimeService

#### Maven-beroenden {#maven-dependencies-5}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-applicationmanager-client-sdk</artifactId>
  <version>11.0.0</version>
</dependency>
```

### Adobe LiveCycle Assembler Client bundle {#adobe-livecycle-assembler-client-bundle}

Följande tjänst är tillgänglig:

* com.adobe.livecycle.assembler.client.AssemblerServiceClient

#### Maven-beroenden {#maven-dependencies-6}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-assembler-client</artifactId>
  <version>11.0.0</version>
</dependency>
```

### Klientpaket för dataintegrering för Adobe LiveCycle {#adobe-livecycle-form-data-integration-client-bundle}

Följande tjänst är tillgänglig:

* com.adobe.livecycle.formdataintegration.client.FormDataIntegrationClient

#### Maven-beroenden {#maven-dependencies-7}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-formdataintegration-client</artifactId>
  <version>11.0.0</version>
</dependency>
```

### Adobe LiveCycle Forms Client bundle {#adobe-livecycle-forms-client-bundle}

Följande tjänst är tillgänglig:

* com.adobe.livecycle.formsservice.client.FormsServiceClient

#### Maven-beroenden {#maven-dependencies-8}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-forms-client</artifactId>
  <version>11.0.0</version>
</dependency>
```

### Adobe LiveCycle Output Client bundle {#adobe-livecycle-output-client-bundle}

Följande tjänst är tillgänglig:

* com.adobe.livecycle.output.client.OutputClient

#### Maven-beroenden {#maven-dependencies-9}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-output-client</artifactId>
  <version>11.0.0</version>
</dependency>
```

### Adobe LiveCycle Reader Extensions Client bundle {#adobe-livecycle-reader-extensions-client-bundle}

Följande tjänst är tillgänglig:

* com.adobe.livecycle.readerextensions.client.ReaderExtensionsServiceClient

#### Maven-beroenden {#maven-dependencies-10}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-reader-extensions-client</artifactId>
  <version>11.0.0</version>
</dependency>
```

### Klientpaket för Adobe LiveCycle Rights Manager {#adobe-livecycle-rights-manager-client-bundle}

Följande tjänster är tillgängliga:

* com.adobe.livecycle.rightsmanagement.client.DocumentManager
* com.adobe.livecycle.rightsmanagement.client.EventManager
* com.adobe.livecycle.rightsmanagement.client.ExternalUserManager
* com.adobe.livecycle.rightsmanagement.client.LicenseManager
* com.adobe.livecycle.rightsmanagement.client.WatermarkManager
* com.adobe.livecycle.rightsmanagement.client.PolicyManager
* com.adobe.livecycle.rightsmanagement.client.AbstractPolicyManager

#### Maven-beroenden {#maven-dependencies-11}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-rightsmanagement-client</artifactId>
  <version>11.0.0</version>
</dependency>
```

### Klientpaket för Adobe LiveCycle Signatures {#adobe-livecycle-signatures-client-bundle}

Följande tjänst är tillgänglig:

* com.adobe.livecycle.signatures.client.SignatureServiceClientInterface

#### Maven-beroenden {#maven-dependencies-12}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-signatures-client</artifactId>
  <version>11.0.0</version>
</dependency>
```

### Klientpaket för Adobe LiveCycle-butik {#adobe-livecycle-truststore-client-bundle}

Följande tjänster är tillgängliga:

* com.adobe.truststore.dsc.TrustConfigurationService
* com.adobe.truststore.dsc.CRLService
* com.adobe.truststore.dsc.CredentialService
* com.adobe.truststore.dsc.CertificateService

#### Maven-beroenden {#maven-dependencies-13}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-truststore-client</artifactId>
  <version>11.0.0</version>
</dependency>
```

### Adobe LiveCycle Repository Client bundle {#adobe-livecycle-repository-client-bundle}

Följande tjänster är tillgängliga:

* com.adobe.repository.bindings.ResourceRepository
* com.adobe.repository.bindings.ResourceSynchronizer

#### Maven-beroenden {#maven-dependencies-14}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-repository-client</artifactId>
  <version>11.0.0</version>
</dependency>
```
