---
title: Arbeta med AEM Forms-databasen
seo-title: Arbeta med AEM Forms-databasen
description: 'null'
seo-description: 'null'
uuid: 6ead49f9-ca0d-4ee4-86a6-0a9ced6ec4f8
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: d2c95881-6c02-4e34-85af-84607df54287
translation-type: tm+mt
source-git-commit: 67ea825215d1ca7cc2e350ed1c128c3146de45ec

---


# Arbeta med AEM Forms-databasen {#working-with-aem-forms-repository}

**Om databastjänsten**

Databastjänsten tillhandahåller tjänster för lagring och hantering av resurser till AEM Forms. När utvecklare skapar ett *AEM Forms* -program kan de distribuera resurserna i databasen i stället för i filsystemet. Materialet kan innehålla alla typer av material, inklusive XML-formulär, PDF-formulär (inklusive Acrobat-formulär), formulärfragment, bilder, profiler, profiler, SWF-filer, DDX-filer, XML-scheman, WSDL-filer och testdata.

Ta till exempel följande Forms-program som heter *Applications/FormsApplication*:

![ww_ww_formdatabase](assets/ww_ww_formrepository.png)

Observera att det finns en fil med namnet Loan.xdp i FormsFolder. Du öppnar den här formulärdesignen genom att ange den fullständiga sökvägen (inklusive version): `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.

>[!NOTE]
>
>Mer information om hur du skapar ett formulärprogram med Workbench finns i [Workbench-hjälpen](https://www.adobe.com/go/learn_aemforms_workbench_63).

Sökvägen till en resurs i AEM Forms-databasen är:

`Applications/Application-name/Application-version/Folder.../Filename`

Följande värden visar några exempel på URI-värden:

* Applications/AppraisalReport/1.0/Forms/FullForm.xdp
* Applications/AnotherApp/1.1/Assets/picture.jpg
* Applications/SomeApp/2.0/Resources/Data/XSDs/MyData.xsd

>[!NOTE]
>
>Du kan bläddra i AEM Forms-databasen med en webbläsare. Om du vill bläddra i databasen anger du följande URL-adress i en webbläsare `https://[server name]:[server port]/repository`. Du kan verifiera snabbstartsresultat som är kopplade till avsnittet Arbeta med AEM Forms-databas med en webbläsare. Om du till exempel lägger till innehåll i AEM Forms-databasen kan du se innehållet i en webbläsare. (Se [Snabbstart (SOAP-läge): Skriva en resurs med Java API](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-writing-a-resource-using-the-java-api).)

Databas-API:t innehåller ett antal åtgärder som du kan använda för att lagra och hämta information från databasen. Du kan till exempel få en lista med resurser eller hämta särskilda resurser som lagras i databasen när en resurs behövs som en del av bearbetningen av ett program.

>[!NOTE]
>
>Databas-API:t kan inte användas för att interagera med innehållstjänster (borttaget). Om du vill interagera med innehållstjänster (borttaget) använder du API:t för dokumenthantering.

Med hjälp av API:t för databastjänsten kan du utföra följande uppgifter:

* Skapa mappar. Se [Skapa mappar](aem-forms-repository.md#creating-folders).
* Skriv resurser och deras egenskaper. Se [Skriva resurser](aem-forms-repository.md#writing-resources).
* Visa resurser i en viss samling eller som är relaterade till andra resurser. Se [Lista resurser](aem-forms-repository.md#listing-resources).
* Läs resurser och deras egenskaper. Se [Läsresurser](aem-forms-repository.md#reading-resources).
* Uppdatera resurser och deras egenskaper. Se [Uppdatera resurser](aem-forms-repository.md#updating-resources).
* Sök efter resurser, inklusive historik, relaterade resurser och egenskaper. Se [Söka efter resurser](aem-forms-repository.md#searching-for-resources).
* Ange relationer mellan resurser. Se [Skapa resursrelationer](aem-forms-repository.md#creating-resource-relationships).
* Hantera resursåtkomstkontroll, inklusive låsning och upplåsning av resurser, samt läs- och skrivåtkomstkontrollistor. Se [Låsa resurser](aem-forms-repository.md#locking-resources).
* Ta bort resurser och deras egenskaper. Se [Ta bort resurser](aem-forms-repository.md#deleting-resources).

>[!NOTE]
>
>Med databas-API:t kan du inte hantera resursåtkomstkontroll, söka efter resurser eller ange resursrelationer med en ECM-databas.

>[!NOTE]
>
>När en krypterad PDF-fil skrivs till databasen går det inte att använda den automatiska relationsextraheringsfunktionen. Annars kan en krypterad PDF lagras i databasen och senare hämtas. Hämtaren kan välja att dekryptera PDF-filen när den har hämtats från databasen.

>[!NOTE]
>
>Mer information om databastjänsten finns i [Tjänstreferens för AEM-formulär](https://www.adobe.com/go/learn_aemforms_services_63).

## Skapar mappar {#creating-folders}

Mappar (resurssamlingar) används för att lagra objekt (filer eller resurser) i ordnade grupperingar. Mappar kan innehålla resurser och andra mappar, som också kallas undermappar. Resurser kan bara lagras i en mapp i taget.

Filerna ärver åtkomstkontrollistor (ACL:er) från mappar, och undermappar ärver åtkomstkontrollistor från sina överordnade mappar. Därför måste de överordnade mapparna finnas innan du kan skapa underordnade mappar. Med IDE kan du bara interagera mappvis, inte fil för fil. Du kan inte versionsmappar och du behöver inte göra det. en mapp inte innehåller själva data. I stället är det bara en behållare för resurser som innehåller data. Standard-ACL är behörighet på systemnivå, vilket innebär att användare måste ha behörighet på systemnivå (läsa, skriva, bläddra, hantera åtkomstkontrollistor) tills någon ger dem behörighet för en viss mapp. ACL-listor fungerar bara i den integrerade utvecklingsmiljön.

>[!NOTE]
>
>Mer information om databastjänsten finns i [Tjänstreferens för AEM-formulär](https://www.adobe.com/go/learn_aemforms_services_63).

### Sammanfattning av steg {#summary-of-steps}

Så här skapar du en mapp:

1. Inkludera projektfiler.
1. Skapa tjänstklienten.
1. Skapa mappen.
1. Skriv mappen till databasen.

**Inkludera projektfiler**

Inkludera nödvändiga filer i utvecklingsprojektet. Om du skapar ett klientprogram med Java, inkluderar du de JAR-filer som behövs. Om du använder webbtjänster inkluderar du proxyfilerna.

**Skapa tjänstklienten**

Innan du kan skapa en resurssamling programmatiskt måste du skapa en anslutning och ange autentiseringsuppgifter. Detta uppnås genom att en tjänstklient skapas.

**Skapa mappen**

Anropa databastjänstmetoden för att skapa resurssamlingen och fylla i resurssamlingen med identifieringsinformation, inklusive dess UUID, mappnamn och beskrivning.

**Skriv mappen till databasen**

Anropa databastjänstmetoden för att skriva resurssamlingen och ange målmappens URI.

**Se även**

[Skapa mappar med Java API](aem-forms-repository.md#create-folders-using-the-java-api)

[Skapa mappar med webbtjänstens API](aem-forms-repository.md#create-folders-using-the-web-service-api)

[Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Snabbstart för databastjänst-API](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Skapa mappar med Java API {#create-folders-using-the-java-api}

Skapa en mapp med hjälp av Repository Service API (Java):

1. Inkludera projektfiler

   Inkludera projektfiler i Java-projektets klassökväg.

1. Skapa tjänstklienten

   Skapa ett `ResourceRepositoryClient` objekt med hjälp av dess konstruktor och skicka ett `ServiceClientFactory` objekt som innehåller anslutningsegenskaper.

1. Skapa mappen

   Om du vill skapa en resurssamling måste du först skapa ett `com.adobe.repository.infomodel.bean.RepositoryInfomodelFactoryBean` objekt.

   Anropa `repositoryInfomodelFactoryBean` objektets `newResourceCollection` metod och skicka följande parametrar:

   * En `com.adobe.repository.infomodel.Id` UUID-identifierare som ska tilldelas resursen.
   * En `com.adobe.repository.infomodel.Lid` UUID-identifierare som ska tilldelas resursen.
   * En `java.lang.String` som innehåller resurssamlingens namn. Exempel, `FormsFolder`.
   Metoden returnerar ett `com.adobe.repository.infomodel.bean.ResourceCollection` objekt som representerar den nya mappen.

   Ange mappens beskrivning med hjälp av metoden `setDescription` och skicka följande parameter:

   * A `String` som beskriver resurssamlingen. I det här exemplet `"test Folder"` används `.`


1. Skriv mappen till databasen

   Anropa `ResourceRepositoryClient` objektets `writeResource` metod och skicka URI:n för mappen och `ResourceCollection` objektet. URI:n till mappen kan till exempel vara följande värde `/Applications/FormsApplication/1.0/`.

   Metoden returnerar en instans av det nyskapade `com.adobe.repository.infomodel.bean.Resource` objektet. Du kan till exempel hämta identifierarvärdet för den nya resursen genom att anropa `com.adobe.repository.infomodel.bean.Resource` objektets `getId` metod.

**Se även**

[Skapar mappar](aem-forms-repository.md#creating-folders)

[Snabbstart (SOAP-läge): Skapa en mapp med Java API](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-creating-a-folder-using-the-java-api)

[Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Skapa mappar med webbtjänstens API {#create-folders-using-the-web-service-api}

Skapa en mapp med hjälp av Repository-tjänstens API (webbtjänst):

1. Inkludera projektfiler

   * Skapa en Microsoft .NET-klientsammansättning som använder databasen WSDL med base64.
   * Referera till Microsoft .NET-klientsammansättningen.

1. Skapa tjänstklienten

   Skapa ett objekt med Microsoft .NET-klientsammansättningen genom att anropa dess standardkonstruktor. `RepositoryServiceService` Ange dess `Credentials` egenskap med ett `System.Net.NetworkCredential` objekt som innehåller användarnamnet och lösenordet.

1. Skapa mappen

   Skapa mappen med standardkonstruktorn för `ResourceCollection` klassen och skicka följande parametrar:

   * Ett `Id` objekt som skapas genom att standardkonstruktorn för `Id` klassen anropas och tilldelas till `Resource` objektets `id` fält.
   * Ett `Lid` objekt som skapas genom att standardkonstruktorn för `Lid` klassen anropas och tilldelas till `Resource` objektets `lid` fält.
   * En sträng som innehåller namnet på resurssamlingen, som tilldelas `Resource` objektets `name` fält. Namnet som används i det här exemplet är `"testfolder"`.
   * En sträng som innehåller beskrivningen av resurssamlingen, som tilldelas `Resource` objektets `description` fält. Beskrivningen som används i det här exemplet är `"test folder"`.

1. Skriv mappen till databasen

   Anropa `RepositoryServiceService` objektets `writeResource` metod och skicka följande parametrar:

   * Sökvägen till den mapp som ska skapas.
   * Det objekt som `ResourceCollection` representerar mappen.
   * Skicka `null` de andra två parametrarna.

**Se även**

[Skapar mappar](aem-forms-repository.md#creating-folders)

[Anropa AEM-formulär med Base64-kodning](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## Skriver resurser {#writing-resources}

Du kan skapa resurser på en viss plats i databasen. Den naturliga filstorleken kan begränsas av databasen och tidsgränsen för sessioner kan överskridas. För standardkonfigurationen är filerna begränsade till 25 MB. Om du vill öka eller minska den maximala filstorleken måste du ändra databaskonfigurationen.

Att skriva resurser motsvarar att lagra data i databasen. När du har skrivit en resurs till databasen blir den tillgänglig för alla klienter i databasens ekosystem. När du skriver resurser, t.ex. XML-scheman, XDP-filer och XSD-filer, till databasen analyseras innehållet baserat på MIME-typen. Om MIME-typen stöds avgör parsern om det finns en underförstådd relation till annat innehåll. Om en CSS (Cascading Style Sheet) till exempel har en relativ URL som refererar till en vanlig CSS-formatmall förväntas du att du även ska skicka den vanliga CSS-koden till databasen. Relationen mellan de två resurserna lagras som en väntande relation under en icke-justerbar period på 30 dagar. När du skickar den vanliga CSS-koden till databasen inom 30 dagar skapas relationen.

När du skapar en resurs ärvs åtkomstkontrollistan (ACL) från den överordnade mappen. Rotmappen har behörighet på systemnivå tills en ursprunglig resurs eller mapp skapas. Då får resursen eller mappen standardbehörigheter för åtkomstkontrollista.

Du kan skriva resurser programmatiskt med hjälp av Java API:t för databastjänsten eller webbtjänstens API.

>[!NOTE]
>
>Mer information om databastjänsten finns i [Tjänstreferens för AEM-formulär](https://www.adobe.com/go/learn_aemforms_services_63).

### Sammanfattning av steg {#summary_of_steps-1}

Så här skriver du en resurs:

1. Inkludera projektfiler.
1. Skapa en databastjänstklient.
1. Ange URI för resursen som ska läsas.
1. Läs resursen.

**Inkludera projektfiler**

Inkludera nödvändiga filer i utvecklingsprojektet. Om du skapar ett klientprogram med Java, inkluderar du de JAR-filer som behövs. Om du använder webbtjänster inkluderar du proxyfilerna.

**Skapa tjänstklienten**

Innan du kan läsa en resurs programmatiskt måste du skapa en anslutning och ange autentiseringsuppgifter. Detta uppnås genom att en tjänstklient skapas.

**Ange URI för målmappen för resursen**

Skapa en sträng som innehåller URI:n för resursen som ska läsas. Syntaxen innehåller snedstreck, som i det här exemplet: &quot;/*path*/*folder*&quot;.

**Skapa resursen**

Anropa databastjänstmetoden för att skapa resursen och fylla resursen med identifieringsinformation, inklusive dess UUID, resursnamn och beskrivning.

**Ange resursinnehållet**

Anropa databastjänstmetoden för att skapa resursinnehåll och lagra innehållet i resursen.

**Skriv resursen till målmappen**

Anropa databastjänstmetoden för att skriva resursen och ange målmappens URI.

**Se även**

[Skriv resurser med Java API](aem-forms-repository.md#write-resources-using-the-java-api)

[Skriv resurser med webbtjänstens API](aem-forms-repository.md#write-resources-using-the-web-service-api)

[Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Snabbstart för databastjänst-API](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Skriv resurser med Java API {#write-resources-using-the-java-api}

Skriv en resurs med hjälp av Repository Service API (Java):

1. Inkludera projektfiler

   Inkludera JAR-klientfiler i Java-projektets klassökväg.

1. Skapa tjänstklienten

   Skapa ett `ResourceRepositoryClient` objekt med hjälp av dess konstruktor och skicka ett `ServiceClientFactory` objekt som innehåller anslutningsegenskaper.

1. Ange URI för målmappen för resursen

   Ange URI för målmappen för resursen. I det här fallet, eftersom resursen med namnet `testResource` lagras i mappen `testFolder`med namnet, är mappens URI `"/testFolder"`. URI:n lagras som ett `java.lang.String` objekt.

1. Skapa resursen

   Om du vill skapa en resurs måste du först skapa ett `com.adobe.repository.infomodel.bean.RepositoryInfomodelFactoryBean` objekt.

   Anropa `RepositoryInfomodelFactoryBean` objektets `newResource` metod, som skapar ett `com.adobe.repository.infomodel.bean.Resource` objekt. I det här exemplet anges följande parametrar:

   * Ett `com.adobe.repository.infomodel.Id` objekt som skapas genom att standardkonstruktorn för `Id` klassen anropas.
   * Ett `com.adobe.repository.infomodel.Lid` objekt som skapas genom att standardkonstruktorn för `Lid` klassen anropas.
   * En `java.lang.String` som innehåller resursens filnamn.
   Om du vill ange resursens beskrivning anropar du `Resource` objektets `setDescription` metod och skickar en sträng som innehåller beskrivningen. I det här exemplet är beskrivningen `"test resource"`.

1. Ange resursinnehållet

   Om du vill skapa innehåll för resursen anropar du `RepositoryInfomodelFactoryBean` objektets `newResourceContent` metod som returnerar ett `com.adobe.repository.infomodel.bean.ResourceContent` objekt. Lägg till innehåll i `ResourceContent` objektet. I det här exemplet genomförs detta genom följande åtgärder:

   * Anropa `ResourceContent` objektets `setDataDocument` metod och skicka ett `com.adobe.idp.Document` objekt
   * Anropa `ResourceContent` objektets `setSize` metod och ange storleken i byte för `Document` objektet
   Lägg till innehållet i resursen genom att anropa `Resource` objektets `setContent` metod och skicka in `ResourceContent` objektet. Mer information finns i API-referens för [AEM-formulär](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

1. Skriv resursen till målmappen

   Anropa `ResourceRepositoryClient` objektets `writeResource` metod och skicka URI:n för mappen samt `Resource` objektet.

**Se även**

[Skriver resurser](aem-forms-repository.md#writing-resources)

[Snabbstart (SOAP-läge): Skriva en resurs med Java API](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-writing-a-resource-using-the-java-api)

[Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Skriv resurser med webbtjänstens API {#write-resources-using-the-web-service-api}

Skriv en resurs med hjälp av Repository-tjänstens API (webbtjänst):

1. Inkludera projektfiler

   * Skapa en Microsoft .NET-klientsammansättning som använder databasen WSDL med base64.
   * Referera till Microsoft .NET-klientsammansättningen.

1. Skapa tjänstklienten

   Skapa ett objekt med Microsoft .NET-klientsammansättningen genom att anropa dess standardkonstruktor. `RepositoryServiceService` Ange dess `Credentials` egenskap med ett `System.Net.NetworkCredential` objekt som innehåller användarnamnet och lösenordet.

1. Ange URI för målmappen för resursen

   Ange URI för målmappen för resursen. I det här fallet, eftersom resursen med namnet `testResource` lagras i mappen `testFolder`med namnet, är mappens URI `"/testFolder"`. När du använder ett språk som är kompatibelt med Microsoft .NET Framework (till exempel C#), ska du lagra URI:n i ett `System.String` objekt.

1. Skapa resursen

   Om du vill skapa en resurs anropar du standardkonstruktorn för `Resource` klassen. I det här exemplet lagras följande information i `Resource` objektet:

   * Ett `com.adobe.repository.infomodel.Id` objekt som skapas genom att standardkonstruktorn för `Id` klassen anropas och tilldelas till `Resource` objektets `id` fält.
   * Ett `com.adobe.repository.infomodel.Lid` objekt som skapas genom att standardkonstruktorn för `Lid` klassen anropas och tilldelas till `Resource` objektets `lid` fält.
   * En sträng som innehåller resursens filnamn, som tilldelas `Resource` objektets `name` fält. Namnet som används i det här exemplet är `"testResource"`.
   * En sträng som innehåller beskrivningen av resursen, som tilldelas `Resource` objektets `description` fält. Beskrivningen som används i det här exemplet är `"test resource"`.

1. Ange resursinnehållet

   Om du vill skapa innehåll för resursen anropar du `ResourceContent` klassens standardkonstruktor. Lägg sedan till innehåll i `ResourceContent` objektet. I det här exemplet genomförs detta genom följande åtgärder:

   * Tilldela ett `BLOB` objekt som innehåller ett dokument till `ResourceContent` objektets `dataDocument` fält.
   * Tilldela storleken i byte för `BLOB` objektet till `ResourceContent` objektets `size` fält.
   Lägg till innehållet i resursen genom att tilldela `ResourceContent` objektet till `Resource` objektets `content` fält.

1. Skriv resursen till målmappen

   Anropa `RepositoryServiceService` objektets `writeResource` metod och skicka URI:n för mappen samt `Resource` objektet. Skicka `null` de andra två parametrarna.

**Se även**

[Skriver resurser](aem-forms-repository.md#writing-resources)

[Anropa AEM-formulär med Base64-kodning](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## Resurser listas {#listing-resources}

Du kan identifiera resurser genom att lista resurser. En fråga utförs mot databasen för att hitta alla resurser som är relaterade till en given resurssamling.

När du har organiserat dina resurser kan du inspektera strukturen som du skapade genom att se en viss gren av strukturen, precis som i ett operativsystem.

Listresurser hanteras efter relation: är medlemmar i mappar. Medlemskapet representeras av en relation av typen&quot;medlem av&quot;. När du listar resurser i en viss mapp frågar du efter resurser som är relaterade till en viss mapp av relationen &quot;medlem i&quot;. Relationer är riktade: en medlem i en relation har en källa som är medlem i målet. Källan är resursen. målet är den överordnade mappen.

>[!NOTE]
>
>Mer information om databastjänsten finns i [Tjänstreferens för AEM-formulär](https://www.adobe.com/go/learn_aemforms_services_63).

### Sammanfattning av steg {#summary_of_steps-2}

Följ de här stegen för att visa resurser:

1. Inkludera projektfiler.
1. Skapa tjänstklienten.
1. Ange mappsökvägen.
1. Hämta listan med resurser.

**Inkludera projektfiler**

Inkludera nödvändiga filer i utvecklingsprojektet. Om du skapar ett klientprogram med Java, inkluderar du de JAR-filer som behövs. Om du använder webbtjänster inkluderar du proxyfilerna.

**Skapa tjänstklienten**

Innan du kan skapa en resurssamling programmatiskt måste du skapa en anslutning och ange autentiseringsuppgifter. Detta uppnås genom att en tjänstklient skapas.

**Ange mappsökväg**

Skapa en sträng som innehåller sökvägen till mappen som innehåller resurserna. Syntaxen innehåller snedstreck, som i det här exemplet: &quot;/*path*/*folder*&quot;.

**Hämta listan över resurser**

Anropa databastjänstmetoden för att hämta listan över resurser och ange målmappens sökväg.

**Se även**

[Visa resurser med Java API](aem-forms-repository.md#list-resources-using-the-java-api)

[Visa resurser som använder webbtjänstens API](aem-forms-repository.md#list-resources-using-the-web-service-api)

[Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Snabbstart för databastjänst-API](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Visa resurser med Java API {#list-resources-using-the-java-api}

Visa resurser med hjälp av Repository Service API (Java):

1. Inkludera projektfiler

   Inkludera JAR-klientfiler i Java-projektets klassökväg.

1. Skapa tjänstklienten

   Skapa ett `ResourceRepositoryClient` objekt med hjälp av dess konstruktor och skicka ett `ServiceClientFactory` objekt som innehåller anslutningsegenskaper.

1. Ange mappsökväg

   Ange URI:n för den resurssamling som ska efterfrågas. I det här fallet är dess URI `"/testFolder"`. URI:n lagras som ett `java.lang.String` objekt.

1. Hämta listan över resurser

   Anropa `ResourceRepositoryClient` objektets `listMembers` metod och skicka mappens URI.

   Metoden returnerar ett `java.util.List` antal `com.adobe.repository.infomodel.bean.Resource` objekt som är källan till en `com.adobe.repository.infomodel.bean.Relation` typ `Relation.TYPE_MEMBER_OF` och som har resurssamlings-URI som mål. Du kan iterera genom detta `List` för att hämta varje resurs. I det här exemplet visas namn och beskrivning för varje resurs.

**Se även**

[Resurser](aem-forms-repository.md#listing-resources)listas.

[Snabbstart (SOAP-läge): Visa resurser med Java API](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-listing-resources-using-the-java-api)

[Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Visa resurser som använder webbtjänstens API {#list-resources-using-the-web-service-api}

Visa resurser med hjälp av Repository-tjänstens API (webbtjänst):

1. Inkludera projektfiler

   * Skapa en Microsoft .NET-klientsammansättning som använder WSDL för databasen.
   * Referera till Microsoft .NET-klientsammansättningen.

1. Skapa tjänstklienten

   Skapa ett objekt med Microsoft .NET-klientsammansättningen genom att anropa dess standardkonstruktor. `RepositoryServiceService` Ange dess `Credentials` egenskap med ett `System.Net.NetworkCredential` objekt som innehåller användarnamnet och lösenordet.

1. Ange mappsökväg

   Ange en sträng som innehåller URI:n för mappen som ska efterfrågas. I det här fallet är dess URI `"/testFolder"`. När du använder ett språk som är kompatibelt med Microsoft .NET Framework (till exempel C#), ska du lagra URI:n i ett `System.String` objekt.

1. Hämta listan över resurser

   Anropa `RepositoryServiceService` objektets `listMembers` metod och skicka URI:n för mappen som den första parametern. Skicka `null` de andra två parametrarna.

   Metoden returnerar en array med objekt som kan bytas ut mot `Resource` objekt. Du kan iterera genom objektarrayen för att hämta de relaterade resurserna. I det här exemplet visas namn och beskrivning för varje resurs.

**Se även**

[Resurser](aem-forms-repository.md#listing-resources)listas.

[Anropa AEM-formulär med Base64-kodning](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## Läser resurser {#reading-resources}

Du kan hämta resurser från en viss plats i databasen för att kunna läsa deras innehåll och metadata. Arbetsflödet avslutas av ett initieringsformulär. Processen har alla behörigheter som krävs för att läsa formuläret. Systemet hämtar dataformuläret och läser innehållet från databasen. Databasen ger åtkomst till innehållet och metadata (möjlighet att ens veta att resursen finns).

Databasen har följande fyra behörighetstyper:

* **gå igenom**: gör att du kan lista resurser, d.v.s. för att läsa resursmetadata, men inte resursinnehåll
* **read**: gör att du kan läsa resursinnehåll
* **write**: gör att du kan skriva resursinnehåll
* **hantera åtkomstkontrollistor**: gör att du kan hantera åtkomstkontrollistor på resurser

Användare kan bara köra processer om de har behörighet att köra processen. IDE-användare behöver gå igenom och läsa behörigheter för att synkronisera med databasen. ACL-listor används endast i designläge eftersom körning sker i systemkontexten.

Du kan läsa resurser programmatiskt med hjälp av Java API:t för databastjänsten eller webbtjänstens API.

>[!NOTE]
>
>Mer information om databastjänsten finns i [Tjänstreferens för AEM-formulär](https://www.adobe.com/go/learn_aemforms_services_63).

### Sammanfattning av steg {#summary_of_steps-3}

Så här läser du en resurs:

1. Inkludera projektfiler.
1. Skapa en databastjänstklient.
1. Ange URI för resursen som ska läsas.
1. Läs resursen.

**Inkludera projektfiler**

Inkludera nödvändiga filer i utvecklingsprojektet. Om du skapar ett klientprogram med Java, inkluderar du de JAR-filer som behövs. Om du använder webbtjänster inkluderar du proxyfilerna.

**Skapa tjänstklienten**

Innan du kan läsa en resurs programmatiskt måste du skapa en anslutning och ange autentiseringsuppgifter. Detta uppnås genom att en tjänstklient skapas.

**Ange URI för resursen som ska läsas**

Skapa en sträng som innehåller URI:n för resursen som ska läsas. Syntaxen innehåller snedstreck, som i det här exemplet: &quot;/*path*/*resource*&quot;.

**Läs resursen**

Anropa databastjänstmetoden för att läsa resursen och ange URI:n.

**Se även**

[Läs resurser med Java API](aem-forms-repository.md#read-resources-using-the-java-api)

[Läsa resurser med hjälp av webbtjänstens API](aem-forms-repository.md#reading-resources-using-the-web-service-api)

[Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Snabbstart för databastjänst-API](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Läs resurser med Java API {#read-resources-using-the-java-api}

Läs en resurs med hjälp av Repository Service API (Java):

1. Inkludera projektfiler

   Inkludera JAR-klientfiler i Java-projektets klassökväg.

1. Skapa tjänstklienten

   Skapa ett `ResourceRepositoryClient` objekt med hjälp av dess konstruktor och skicka ett `ServiceClientFactory` objekt som innehåller anslutningsegenskaper.

1. Ange URI för resursen som ska läsas

   Ange ett strängvärde som representerar URI:n för resursen som ska hämtas. Om resursen till exempel heter *testResource* som finns i en mapp med namnet *testFolder* anger du `/testFolder/testResource`.

1. Läs resursen

   Anropa `ResourceRepositoryClient` objektets `readResource` metod och skicka URI:n för resursen som en parameter. Den här metoden returnerar en `Resource` instans som representerar resursen.

**Se även**

[Läser resurser](aem-forms-repository.md#reading-resources)

[Snabbstart (SOAP-läge): Läsa en resurs med Java API](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-reading-a-resource-using-the-java-api)

[Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Läsa resurser med hjälp av webbtjänstens API {#reading-resources-using-the-web-service-api}

Läs en resurs med hjälp av Repository Service API (webbtjänsten):

1. Inkludera projektfiler

   * Skapa en Microsoft .NET-klientsammansättning som använder WSDL för databasen. (Se [Skapa en .NET-klientsammansättning som använder Base64-kodning](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding).)
   * Referera till Microsoft .NET-klientsammansättningen. (Se [Skapa en .NET-klientsammansättning som använder Base64-kodning](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding).)

1. Skapa tjänstklienten

   Skapa ett objekt med Microsoft .NET-klientsammansättningen genom att anropa dess standardkonstruktor. `RepositoryServiceService` Ange dess `Credentials` egenskap med ett `System.Net.NetworkCredential` objekt som innehåller användarnamnet och lösenordet.

1. Ange URI för resursen som ska läsas

   Ange en sträng som innehåller URI:n för resursen som ska hämtas. I det här fallet, eftersom resursen med namnet `testResource` finns i mappen med namnet `testFolder`, är dess URI `"/testFolder/testResource"`. När du använder ett språk som är kompatibelt med Microsoft .NET Framework (till exempel C#), ska du lagra URI:n i ett `System.String` objekt.

1. Läs resursen

   Anropa `RepositoryServiceService` objektets `readResource` metod och skicka URI:n för resursen som den första parametern. Skicka `null` de andra två parametrarna.

**Se även**

[Läser resurser](aem-forms-repository.md#reading-resources)

[Anropa AEM-formulär med Base64-kodning](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## Uppdaterar resurser {#updating-resources}

Du kan hämta och uppdatera innehållet för resurser i databasen. När du uppdaterar resurser ändras inte åtkomstkontrollen för dessa resurser mellan versionerna. När du utför en uppdatering kan du välja att öka huvudversionen. Om du inte väljer att öka den större versionen uppdateras den mindre versionen automatiskt.

När du uppdaterar en resurs skapas den nya versionen baserat på de angivna resursattributen. När du uppdaterar en resurs anger du två viktiga parametrar: mål-URI och en resursinstans som innehåller alla uppdaterade metadata. Observera att om du inte ändrar ett visst attribut (till exempel namnet), krävs fortfarande attributet i den instans som du skickar in. De relationer som skapas när innehållet tolkas läggs till i den specifika versionen och överförs inte framåt om inte annat anges.

Om du till exempel uppdaterar en XDP-fil och den innehåller referenser till andra resurser, spelas även dessa ytterligare referenser in. Anta att form.xdp version 1.0 har två externa referenser: en logotyp och en formatmall, och du uppdaterar sedan form.xdp så att det nu finns tre referenser: en logotyp, en formatmall och en schemafil. Under uppdateringen lägger databasen till den tredje relationen (till schemafilen) i den väntande relationstabellen. När schemafilen finns i databasen kommer relationen automatiskt att formas. Om form.xdp version 2.0 inte längre använder logotypen kommer form.xdp version 2.0 inte att ha något samband med logotypen.

Alla uppdateringsåtgärder är atomiska och transaktionella. Om två användare till exempel läser samma resurs och båda beslutar att uppdatera version 1.0 till version 2.0, kommer en av dem att lyckas och en av dem kommer att misslyckas, databasens integritet kommer att bevaras och båda får ett meddelande som bekräftar att åtgärden lyckades eller misslyckades. Om transaktionen inte genomförs återställs den vid databasfel och timeout eller återställning inträffar beroende på programservern.

Du kan uppdatera resurser programmatiskt med hjälp av Java API:t för databastjänsten eller webbtjänstens API.

>[!NOTE]
>
>Mer information om databastjänsten finns i [Tjänstreferens för AEM-formulär](https://www.adobe.com/go/learn_aemforms_services_63).

### Sammanfattning av steg {#summary_of_steps-4}

Så här uppdaterar du en resurs:

1. Inkludera projektfiler.
1. Skapa en databastjänstklient.
1. Hämta resursen som ska uppdateras.
1. Uppdatera resursen.

**Inkludera projektfiler**

Inkludera nödvändiga filer i utvecklingsprojektet. Om du skapar ett klientprogram med Java, inkluderar du de JAR-filer som behövs. Om du använder webbtjänster inkluderar du proxyfilerna.

**Skapa tjänstklienten**

Innan du kan läsa en resurs programmatiskt måste du skapa en anslutning och ange autentiseringsuppgifter. Detta uppnås genom att en tjänstklient skapas.

**Hämta resursen som ska uppdateras**

Läs resursen. Mer information finns i [Läsresurser](aem-forms-repository.md#reading-resources).

**Uppdatera resursen**

Ange den nya informationen i resursen och anropa databastjänstmetoden för att uppdatera resursen, ange URI, den uppdaterade resursen och hur versionsinformationen ska uppdateras.

**Se även**

[Uppdatera resurser med Java API](aem-forms-repository.md#update-resources-using-the-java-api)

[Uppdatera resurser med webbtjänstens API](aem-forms-repository.md#update-resources-using-the-web-service-api)

[Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Snabbstart för databastjänst-API](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Uppdatera resurser med Java API {#update-resources-using-the-java-api}

Uppdatera en resurs med hjälp av Repository Service API (Java):

1. Inkludera projektfiler

   Inkludera JAR-klientfiler i Java-projektets klassökväg.

1. Skapa tjänstklienten

   Skapa ett `ResourceRepositoryClient` objekt med hjälp av dess konstruktor och skicka ett `ServiceClientFactory` objekt som innehåller anslutningsegenskaper.

1. Hämta resursen som ska uppdateras

   Ange URI för resursen som ska hämtas och läsas. I det här exemplet är resursens URI `"/testFolder/testResource"`.

1. Uppdatera resursen

   Uppdatera `Resource` objektinformationen. I det här exemplet uppdaterar du beskrivningen genom att anropa `Resource` objektets `setDescription` metod och skicka den nya beskrivningssträngen som en parameter.

   Anropa sedan `ServiceClientFactory` objektets `updateResource` metod och skicka följande parametrar:

   * Ett `java.lang.String` objekt som innehåller resursens URI.
   * Objektet `Resource` som innehåller den uppdaterade resursinformationen.
   * Ett `boolean` värde som anger om huvudversionen eller delversionen ska uppdateras. I det här exemplet skickas värdet `true` för att ange att huvudversionen ska ökas.

**Se även**

[Uppdaterar resurser](aem-forms-repository.md#updating-resources)

[Snabbstart (SOAP-läge): Uppdatera en resurs med Java API](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-updating-a-resource-using-the-java-api)

[Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Uppdatera resurser med webbtjänstens API {#update-resources-using-the-web-service-api}

Uppdatera en resurs med hjälp av Repository API (webbtjänsten):

1. Inkludera projektfiler

   * Skapa en Microsoft .NET-klientsammansättning som använder WSDL för databasen.
   * Referera till Microsoft .NET-klientsammansättningen.

1. Skapa tjänstklienten

   Skapa ett objekt med Microsoft .NET-klientsammansättningen genom att anropa dess standardkonstruktor. `RepositoryServiceService` Ange dess `Credentials` egenskap med ett `System.Net.NetworkCredential` objekt som innehåller användarnamnet och lösenordet.

1. Hämta resursen som ska uppdateras

   Ange URI:n för resursen som ska hämtas och läsa resursen. I det här exemplet är resursens URI `"/testFolder/testResource"`. Mer information finns i [Läsresurser](aem-forms-repository.md#reading-resources).

1. Uppdatera resursen

   Uppdatera `Resource` objektinformationen. I det här exemplet uppdaterar du beskrivningen genom att tilldela ett nytt värde till `Resource` objektets `description` fält.

1. Anropa `RepositoryServiceService` objektets `updateResource` metod och skicka följande parametrar:

   * Ett `System.String` objekt som innehåller resursens URI.
   * Objektet `Resource` som innehåller den uppdaterade resursinformationen.
   * Ett `boolean` värde som anger om huvudversionen eller delversionen ska uppdateras. I det här exemplet skickas värdet `true` för att ange att huvudversionen ska ökas.
   * Skicka `null` för de återstående två parametrarna.

**Se även**

[Uppdaterar resurser](aem-forms-repository.md#updating-resources)

[Anropa AEM-formulär med Base64-kodning](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## Söker efter resurser {#searching-for-resources}

Du kan skapa frågor som används för att söka efter resurser i databasen, inklusive historik, relaterade resurser och egenskaper.

Du kan hämta relaterade resurser för att fastställa beroenden mellan ett formulär och dess fragment. Om du till exempel har ett formulär kan du avgöra vilka fragment eller externa resurser som används. Om du har en bild kan du även ta reda på vilka formulär som använder bilden. Du kan också söka efter relaterade resurser med filtrering baserat på egenskaper. Du kan t.ex. söka efter alla formulär som använder en bild med ett visst namn, eller hitta en bild som används av ett formulär med ett visst namn. Du kan också söka med hjälp av resursegenskaper. Du kan till exempel utföra en fråga för att hitta alla formulär eller resurser vars namn börjar med en sträng som kan innehålla jokertecknen&quot;%&quot; och&quot;_&quot;. Kom ihåg att sökningar som baseras på egenskaper inte baseras på relationer, sökningarna baseras på antagandet att du har specifik kunskap om en viss resurs.

**Frågesatser**

En *fråga* innehåller en eller flera satser som är logiskt kopplade med villkor. En *programsats* består av en vänster operand, en operator och en höger operand. Dessutom kan du ange den sorteringsordning som ska användas för sökresultaten. Sorteringsordningen ** innehåller information som motsvarar en SQL- `ORDER BY` sats och består av element som innehåller de attribut som sökningen baserades på, samt ett värde som anger om stigande eller fallande ordning ska användas.

Du kan programmässigt söka efter resurser med Java API:t för databastjänsten. För närvarande går det inte att använda webbtjänstens API för att söka efter resurser.

**Sorteringsbeteende**

Sorteringsordningen respekteras inte när `ResourceRepositoryClient` objektets `searchProperties` metod anropas och en sorteringsordning anges. Anta till exempel att du skapar en resurs med tre anpassade egenskaper, där attributnamnen är `name`, `secondName`och `asecondName`. Sedan skapar du ett sorteringsordselement i attributnamnet och anger `ascending` värdet till `true`.

Sedan anropar du `ResourceRepositoryClient` objektets `searchProperties` metod och skickar i sorteringsordningen. Sökningen returnerar rätt resurs med de tre egenskaperna. Egenskaperna sorteras dock inte efter attributnamn. De returneras i den ordning de lades till: `name`, `secondName`och `asecondName`.

>[!NOTE]
>
>Mer information om databastjänsten finns i [Tjänstreferens för AEM-formulär](https://www.adobe.com/go/learn_aemforms_services_63).

### Sammanfattning av steg {#summary_of_steps-5}

Så här söker du efter resurser:

1. Inkludera projektfiler.
1. Skapa en databastjänstklient.
1. Ange målmappen för sökningen.
1. Ange de attribut som används i sökningen.
1. Skapa frågan som används i sökningen.
1. Skapa sorteringsordningen för sökresultaten.
1. Sök efter resurserna.
1. Hämta resurserna från sökresultatet.

**Inkludera projektfiler**

Inkludera nödvändiga filer i utvecklingsprojektet. Om du skapar ett klientprogram med Java, inkluderar du de JAR-filer som behövs. Om du använder webbtjänster inkluderar du proxyfilerna.

**Skapa tjänstklienten**

Innan du kan läsa en resurs programmatiskt måste du skapa en anslutning och ange autentiseringsuppgifter. Detta uppnås genom att en tjänstklient skapas.

**Ange målmapp för sökningen**

Skapa en sträng som innehåller den grundsökväg som sökningen ska utföras från. Syntaxen innehåller snedstreck, som i det här exemplet: &quot;/*path*/*folder*&quot;.

**Ange de attribut som används i sökningen**

Du kan basera sökningen på attributen i resurserna. Ange värdena för attributen som sökningen ska utföras på.

**Skapa frågan som används i sökningen**

Skapa en fråga med hjälp av satser och villkor. Varje programsats anger vilket attribut sökningen ska baseras på, vilket villkor som ska användas och vilket attributvärde som ska användas i sökningen.

**Skapa sorteringsordningen för sökresultaten**

Sorteringsordningen består av element, som vart och ett innehåller ett av attributen som används i sökningen och ett värde som anger om stigande eller fallande ordning ska användas.

**Sök efter resurser**

Sök efter resurser med hjälp av mappen, frågan och sorteringsordningen. Ange dessutom sökningens djup och en övre gräns för hur många resultat som ska returneras.

**Hämta resurserna från sökresultatet**

Iterera genom den returnerade resurslistan och extrahera informationen för vidare bearbetning.

**Se även**

[Sök efter resurser med Java API](aem-forms-repository.md#search-for-resources-using-the-java-api)

[Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Snabbstart för databastjänst-API](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Sök efter resurser med Java API {#search-for-resources-using-the-java-api}

Sök efter en resurs med hjälp av Repository Service API (Java):

1. Inkludera projektfiler

   Inkludera JAR-klientfiler i Java-projektets klassökväg.

1. Skapa tjänstklienten

   Skapa ett `ResourceRepositoryClient` objekt med hjälp av dess konstruktor och skicka ett `ServiceClientFactory` objekt som innehåller anslutningsegenskaper.

1. Ange målmapp för sökningen

   Ange URI:n för bassökvägen som sökningen ska utföras från. I det här exemplet är resursens URI `/testFolder`.

1. Ange de attribut som används i sökningen

   Ange värdena för attributen som sökningen ska utföras på. Attributen finns i ett `com.adobe.repository.infomodel.bean.Resource` objekt. I detta exempel kommer sökningen att utföras på namnattributet. Därför används en `java.lang.String` som innehåller `Resource` objektets namn, vilket är `testResource` i det här fallet.

1. Skapa frågan som används i sökningen

   Om du vill skapa en fråga skapar du ett `com.adobe.repository.query.Query` objekt genom att anropa standardkonstruktorn för `Query` klassen och lägger till satser i frågan.

   Om du vill skapa en -programsats anropar du konstruktorn för `com.adobe.repository.query.Query.Statement` klassen och skickar följande parametrar:

   * En vänsteroperand som innehåller resursattributskonstanten. I det här exemplet `Resource.ATTRIBUTE_NAME` används det statiska värdet eftersom resursens namn används som grund för sökningen.
   * En operator som innehåller villkoret som används i sökningen efter attributet. Operatorn måste vara en av de statiska konstanterna i `Query.Statement` klassen. I det här exemplet `Query.Statement.OPERATOR_BEGINS_WITH` används det statiska värdet.
   * En högeroperand som innehåller attributvärdet som sökningen ska utföras på. I det här exemplet används name-attributet, som `String` innehåller värdet `"testResource"`.
   Ange namnutrymmet för den vänstra operanden genom att anropa `Query.Statement` objektets `setNamespace` metod och ange ett av de statiska värdena i `com.adobe.repository.infomodel.bean.ResourceProperty` klassen. I det här exemplet `ResourceProperty.RESERVED_NAMESPACE_REPOSITORY` används .

   Lägg till varje sats i frågan genom att anropa `Query` objektets `addStatement` metod och skicka in `Query.Statement` objektet.

1. Skapa sorteringsordningen för sökresultaten

   Om du vill ange den sorteringsordning som används i sökresultaten skapar du ett `com.adobe.repository.query.sort.SortOrder` objekt genom att anropa standardkonstruktorn för `SortOrder` klassen och lägger till element i sorteringsordningen.

   Om du vill skapa ett element för sorteringsordningen anropar du en av konstruktorerna för `com.adobe.repository.query.sort.SortOrder.Element` klassen. I det här exemplet används det statiska värdet som första parameter eftersom resursens namn används som bas för sökningen, och stigande ordning ( `Resource.ATTRIBUTE_NAME` värdet `boolean` `true`) anges som den andra parametern.

   Lägg till varje element i sorteringsordningen genom att anropa `SortOrder` objektets `addSortElement` metod och skicka in `SortOrder.Element` objektet.

1. Sök efter resurser

   Om du vill söka efter `resources` baserat på attributegenskaper anropar du `ResourceRepositoryClient` objektets `searchProperties` metod och skickar följande parametrar:

   * En `String` som innehåller den grundsökväg som sökningen ska utföras från. I det här fallet används `"/testFolder"` .
   * Frågan som används i sökningen.
   * Djupet på sökningen. I det här fallet används `com.adobe.repository.infomodel.bean.ResourceCollection.DEPTH_INFINITE` för att ange att bassökvägen och alla dess mappar ska användas.
   * Ett `int` värde som anger den första raden från vilken den ej växlade resultatmängden ska väljas. I det här exemplet `0` anges.
   * Ett `int` värde som anger det maximala antalet resultat som ska returneras. I det här exemplet `10` anges.
   * Sorteringsordningen som används i sökningen.
   Metoden returnerar ett `java.util.List` antal `Resource` objekt i den angivna sorteringsordningen.

1. Hämta resurserna från sökresultatet

   Om du vill hämta resurserna som finns i sökresultatet itererar du genom `List` och konverterar varje objekt till ett objekt `Resource` för att kunna extrahera informationen. I det här exemplet visas namnet på varje resurs.

**Se även**

[Söker efter resurser](aem-forms-repository.md#searching-for-resources)

[Snabbstart (SOAP-läge): Söka efter resurser med Java API](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-searching-for-resources-using-the-java-api)

[Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Skapar resursrelationer {#creating-resource-relationships}

Du kan ange relationer mellan resurser i databasen. Det finns tre typer av relationer:

* **Beroende**: en relation där en resurs är beroende av andra resurser, vilket innebär att alla relaterade resurser behövs i databasen.
* **Medlemskap (filsystem)**: en relation där en resurs finns i en viss mapp.
* **Anpassad**: en relation som du anger mellan resurser. Om till exempel en resurs har tagits bort och en annan resurs har lagts till i databasen, kan du ange en egen ersättningsrelation.

Du kan skapa egna anpassade relationer. Om du t.ex. lagrar en HTML-fil i databasen och använder en bild, kan du ange en anpassad relation som relaterar HTML-filen till bilden (eftersom vanligtvis bara XML-filer associeras med bilder som använder en databasdefinierad beroenderelation). Ett annat exempel på en anpassad relation är om du vill skapa en annan vy av databasen med en cyklisk diagramstruktur i stället för en trädstruktur. Du kan definiera ett cirkeldiagram tillsammans med ett visningsprogram för att gå igenom dessa relationer. Slutligen kan du ange att en resurs ersätter en annan resurs trots att de två resurserna är helt olika. I så fall kan du definiera en relationstyp utanför det reserverade intervallet och skapa en relation mellan dessa två resurser. Ditt program skulle vara den enda klienten som kunde identifiera och bearbeta relationen och det skulle kunna användas för att utföra sökningar i relationen.

Du kan programmatiskt ange relationer mellan resurser med Java API:t för databastjänsten eller webbtjänstens API.

>[!NOTE]
>
>Mer information om databastjänsten finns i [Tjänstreferens för AEM-formulär](https://www.adobe.com/go/learn_aemforms_services_63).

### Sammanfattning av steg {#summary_of_steps-6}

Så här anger du en relation mellan två resurser:

1. Inkludera projektfiler.
1. Skapa en databastjänstklient.
1. Ange URI:erna för resurserna som ska relateras.
1. Skapa relationen.

**Inkludera projektfiler**

Inkludera nödvändiga filer i utvecklingsprojektet. Om du skapar ett klientprogram med Java, inkluderar du de JAR-filer som behövs. Om du använder webbtjänster inkluderar du proxyfilerna.

**Skapa tjänstklienten**

Innan du kan läsa en resurs programmatiskt måste du skapa en anslutning och ange autentiseringsuppgifter. Detta uppnås genom att en tjänstklient skapas.

**Ange URI:erna för resurserna som ska relateras**

Skapa strängar som innehåller URI:erna för resursen som ska relateras. Syntaxen innehåller snedstreck, som i det här exemplet: &quot;/*path*/*resource*&quot;.

**Skapa relationen**

Anropa databastjänstmetoden för att skapa och ange relationstypen.

**Se även**

[Skapa relationsresurser med Java API](aem-forms-repository.md#create-relationship-resources-using-the-java-api)

[Skapa relationsresurser med hjälp av webbtjänstens API](aem-forms-repository.md#create-relationship-resources-using-the-web-service-api)

[Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Snabbstart för databastjänst-API](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Skapa relationsresurser med Java API {#create-relationship-resources-using-the-java-api}

Skapa relationsresurser genom att använda Java API för databastjänsten och utföra följande uppgifter:

1. Inkludera projektfiler

   Inkludera JAR-klientfiler i Java-projektets klassökväg.

1. Skapa tjänstklienten

   Skapa ett `ResourceRepositoryClient` objekt med hjälp av dess konstruktor och skicka ett `ServiceClientFactory` objekt som innehåller anslutningsegenskaper.

1. Ange URI:erna för resurserna som ska relateras

   Ange URI:erna för resurserna som ska relateras. I det här fallet är URI:erna `testResource1` och `testResource2` eftersom resurserna har namn `testFolder`och `"/testFolder/testResource1"` finns i mappen `"/testFolder/testResource2"`med namnet. URI:erna lagras som ett `java.lang.String` objekt. I det här exemplet skrivs resurserna först till databasen och deras URI:er hämtas. Mer information om hur du skriver en resurs finns i [Skriva resurser](aem-forms-repository.md#writing-resources).

1. Skapa relationen

   Anropa `ResourceRepositoryClient` objektets `createRelationship` metod och skicka följande parametrar:

   * Källresursens URI.
   * Målresursens URI.
   * Relationstypen, som är en av de statiska konstanterna i `com.adobe.repository.infomodel.bean.Relation` klassen. I det här exemplet skapas ett beroendeförhållande genom att ange värdet `Relation.TYPE_DEPENDANT_OF`.
   * Ett `boolean` värde som anger om målresursen automatiskt uppdateras till den `com.adobe.repository.infomodel.Id`baserade identifieraren för den nya huvudresursen. I det här exemplet `true` anges värdet på grund av beroendeförhållandet.
   Du kan också hämta en lista över relaterade resurser för en viss resurs genom att anropa `ResourceRepositoryClient` objektets `getRelated` metod och skicka följande parametrar:

   * URI för resursen som relaterade resurser ska hämtas för. I det här exemplet anges källresursen ( `"/testFolder/testResource1"`).
   * Ett `boolean` värde som anger om den angivna resursen är källresursen i relationen. I det här exemplet `true` anges värdet eftersom så är fallet.
   * Relationstypen, som är en av de statiska konstanterna i `Relation` klassen. I det här exemplet anges en beroenderelation med samma värde som användes tidigare: `Relation.TYPE_DEPENDANT_OF`.
   Metoden returnerar ett `getRelated` antal `java.util.List` objekt som du kan använda för att iterera från de relaterade resurserna och omvandla objekten i `Resource` till `List` `Resource` på samma sätt. I det här exemplet `testResource2` förväntas finnas i listan över returnerade resurser.

**Se även**

[Skapar resursrelationer](aem-forms-repository.md#creating-resource-relationships)

[Snabbstart (SOAP-läge): Skapa relationer mellan resurser med Java API](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-creating-relationships-between-resources-using-the-java-api)

[Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Skapa relationsresurser med hjälp av webbtjänstens API {#create-relationship-resources-using-the-web-service-api}

Skapa relationsresurser med hjälp av Repository API (webbtjänsten):

1. Inkludera projektfiler

   * Skapa en Microsoft .NET-klientsammansättning som använder WSDL för databasen.
   * Referera till Microsoft .NET-klientsammansättningen.

1. Skapa tjänstklienten

   Skapa ett objekt med Microsoft .NET-klientsammansättningen genom att anropa dess standardkonstruktor. `RepositoryServiceService` Ange dess `Credentials` egenskap med ett `System.Net.NetworkCredential` objekt som innehåller användarnamnet och lösenordet.

1. Ange URI:erna för resurserna som ska relateras

   Ange URI:erna för resurserna som ska relateras. I det här fallet är URI:erna `testResource1` och `testResource2` eftersom resurserna har namn `testFolder`och `"/testFolder/testResource1"` finns i mappen `"/testFolder/testResource2"`med namnet. När du använder ett språk som är kompatibelt med Microsoft .NET Framework (till exempel C#), lagras URI:erna som ett `System.String` objekt. I det här exemplet skrivs resurserna först till databasen och deras URI:er hämtas. Mer information om hur du skriver en resurs finns i [Skriva resurser](aem-forms-repository.md#writing-resources).

1. Skapa relationen

   Anropa `RepositoryServiceService` objektets `createRelationship` metod och skicka följande parametrar:

   * Källresursens URI.
   * Målresursens URI.
   * Relationstypen. I det här exemplet skapas ett beroendeförhållande genom att ange värdet `3`.
   * Ett `boolean` värde som anger om relationstypen har angetts. I det här exemplet `true` anges värdet.
   * Ett `boolean` värde som anger om målresursen automatiskt uppdateras till den `Id`baserade identifieraren för den nya huvudresursen. I det här exemplet `true` anges värdet på grund av beroendeförhållandet.
   * Ett `boolean` värde som anger om målhuvudet har angetts. I det här exemplet `true` anges värdet.
   * Skicka `null` för den sista parametern.
   Du kan också hämta en lista över relaterade resurser för en viss resurs genom att anropa `RepositoryServiceService` objektets `getRelated` metod och skicka följande parametrar:

   * URI för resursen som relaterade resurser ska hämtas för. I det här exemplet anges källresursen ( `"/testFolder/testResource1"`).
   * Ett `boolean` värde som anger om den angivna resursen är källresursen i relationen. I det här exemplet `true` anges värdet eftersom så är fallet.
   * Ett `boolean` värde som anger om källresursen har angetts. I det här exemplet `true` anges värdet.
   * En array med heltal som innehåller relationstyperna. I det här exemplet anges en beroenderelation med samma värde i arrayen som tidigare: `3`.
   * Skicka `null` för de återstående två parametrarna.
   Metoden returnerar en array med objekt som kan bytas ut mot `getRelated` `Resource` objekt, genom vilka du kan iterera för att hämta de relaterade resurserna. I det här exemplet `testResource2` förväntas finnas i listan över returnerade resurser.

**Se även**

[Skapar resursrelationer](aem-forms-repository.md#creating-resource-relationships)

[Anropa AEM-formulär med Base64-kodning](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## Låser resurser {#locking-resources}

Du kan låsa en resurs eller en uppsättning resurser så att de bara kan användas av en viss användare eller för delad användning av flera användare. Ett delat lås är en indikation på att något kommer att hända med resursen, men det förhindrar inte någon annan från att vidta åtgärder med den resursen. Ett delat lås bör betraktas som en signaleringsmekanism. Ett exklusivt lås innebär att den användare som låste resursen kommer att ändra resursen och låset garanterar att ingen annan kan göra det förrän användaren inte längre behöver åtkomst till resursen och har släppt låset. Om en databasadministratör låser upp en resurs tas alla exklusiva och delade lås bort automatiskt för den resursen. Den här typen av åtgärd är avsedd för situationer där en användare inte längre är tillgänglig och inte har låst upp resursen.

När en resurs är låst visas en låsikon när du visar fliken Resurser i Workbench, vilket visas på följande bild.

![lr_lr_lockdatabase](assets/lr_lr_lockrepository.png)

Du kan programmässigt styra åtkomsten till resurser med hjälp av Java API:t för databastjänsten eller webbtjänstens API.

>[!NOTE]
>
>Mer information om databastjänsten finns i [Tjänstreferens för AEM-formulär](https://www.adobe.com/go/learn_aemforms_services_63).

### Sammanfattning av steg {#summary_of_steps-7}

Så här låser du och låser upp resurser:

1. Inkludera projektfiler.
1. Skapa en databastjänstklient.
1. Ange URI för resursen som ska låsas.
1. Lås resursen.
1. Hämta låsen för resursen.
1. Lås upp resursen

**Inkludera projektfiler**

Inkludera nödvändiga filer i utvecklingsprojektet. Om du skapar ett klientprogram med Java, inkluderar du de JAR-filer som behövs. Om du använder webbtjänster inkluderar du proxyfilerna.

**Skapa tjänstklienten**

Innan du kan läsa en resurs programmatiskt måste du skapa en anslutning och ange autentiseringsuppgifter. Detta uppnås genom att en tjänstklient skapas.

**Ange URI för resursen som ska låsas**

Skapa en sträng som innehåller URI:n för resursen som ska låsas. Syntaxen innehåller snedstreck, som i det här exemplet: &quot;/*path*/*resource*&quot;.

**Lås resursen**

Anropa databastjänstmetoden för att låsa resursen, ange URI, typ av lås och låsningsdjup.

**Hämta låsen för resursen**

Anropa databastjänstmetoden för att hämta låsen för resursen och ange URI:n.

**Lås upp resursen**

Anropa databastjänstmetoden för att låsa upp resursen och ange URI:n.

**Se även**

[Lås resurser med Java API](aem-forms-repository.md#lock-resources-using-the-java-api)

[Lås resurser med webbtjänstens API](aem-forms-repository.md#lock-resources-using-the-web-service-api)

[Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Snabbstart för databastjänst-API](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Lås resurser med Java API {#lock-resources-using-the-java-api}

Lås resurser med hjälp av Repository Service API (Java):

1. Inkludera projektfiler

   Inkludera JAR-klientfiler i Java-projektets klassökväg.

1. Skapa tjänstklienten

   Skapa ett `ResourceRepositoryClient` objekt med hjälp av dess konstruktor och skicka ett `ServiceClientFactory` objekt som innehåller anslutningsegenskaper.

1. Ange URI för resursen som ska låsas

   Ange URI för resursen som ska låsas. I det här fallet, eftersom resursen med namnet `testResource` finns i mappen med namnet `testFolder`, är dess URI `"/testFolder/testResource"`. URI:n lagras som ett `java.lang.String` objekt.

1. Lås resursen

   Anropa `ResourceRepositoryClient` objektets `lockResource` metod och skicka följande parametrar:

   * Resursens URI.
   * Låsomfånget. I det här exemplet anges låsomfånget som `com.adobe.repository.infomodel.bean.Lock.SCOPE_EXCLUSIVE`eftersom resursen kommer att låsas exklusivt.
   * Låsdjupet. I det här exemplet anges låsningsdjupet som `Lock.DEPTH_ZERO`eftersom låsning endast gäller för den aktuella resursen och ingen av dess medlemmar eller underordnade.
   >[!NOTE]
   >
   >Den överlagrade versionen av metoden som kräver fyra parametrar genererar ett undantag. `lockResource` Se till att du använder den `lockResource` metod som kräver tre parametrar som visas i genomgången.

1. Hämta låsen för resursen

   Anropa `ResourceRepositoryClient` objektets `getLocks` metod och skicka URI:n för resursen som en parameter. Metoden returnerar en List med Lock-objekt som du kan iterera igenom. I det här exemplet skrivs låsägaren, djupet och omfånget ut för varje objekt genom att varje Lock-objekts `getOwnerUserId`-, `getDepth`respektive `getType` -metoder anropas.

1. Lås upp resursen

   Anropa `ResourceRepositoryClient` objektets `unlockResource` metod och skicka URI:n för resursen som en parameter. Mer information finns i API-referens för [AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**Se även**

[Låser resurser](aem-forms-repository.md#locking-resources)

[Snabbstart (SOAP-läge): Låsa en resurs med Java API](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-locking-a-resource-using-the-java-api)

[Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Lås resurser med webbtjänstens API {#lock-resources-using-the-web-service-api}

Lås resurser med hjälp av Repository-tjänstens API (webbtjänst):

1. Inkludera projektfiler

   * Skapa en Microsoft .NET-klientsammansättning som förbrukar WSDL för databasen med Base64.
   * Referera till Microsoft .NET-klientsammansättningen.

1. Skapa tjänstklienten

   Skapa ett objekt med Microsoft .NET-klientsammansättningen genom att anropa dess standardkonstruktor. `RepositoryServiceService` Ange dess `Credentials` egenskap med ett `System.Net.NetworkCredential` objekt som innehåller användarnamnet och lösenordet.

1. Ange URI för resursen som ska låsas

   Ange en sträng som innehåller URI:n för resursen som ska låsas. I det här fallet, eftersom resursen med namnet `testResource` finns i mappen, `testFolder`är dess URI `"/testFolder/testResource"`. När du använder ett språk som är kompatibelt med Microsoft .NET Framework (till exempel C#), ska du lagra URI:n i ett `System.String` objekt.

1. Lås resursen

   Anropa `RepositoryServiceService` objektets `lockResource` metod och skicka följande parametrar:

   * Resursens URI.
   * Låsomfånget. I det här exemplet anges låsomfånget som `11`eftersom resursen kommer att låsas exklusivt.
   * Låsdjupet. I det här exemplet anges låsningsdjupet som `2`eftersom låsning endast gäller för den aktuella resursen och ingen av dess medlemmar eller underordnade.
   * Ett `int` värde som anger antalet sekunder innan låset förfaller. I det här exemplet används värdet för `1000` .
   * Skicka `null` för den sista parametern.

1. Hämta låsen för resursen

   Anropa `RepositoryServiceService` objektets `getLocks` -metod och skicka URI:n för resursen som den första parametern och `null` för den andra parametern. Metoden returnerar en `object` array som innehåller `Lock` objekt som du kan iterera igenom. I det här exemplet skrivs låsägaren, djupet och omfånget ut för varje objekt genom att gå till varje `Lock` objekts `ownerUserId`-, `depth`- respektive `type` -fält.

1. Lås upp resursen

   Anropa `RepositoryServiceService` objektets `unlockResource` -metod och skicka URI:n för resursen som den första parametern och `null` för den andra parametern.

**Se även**

[Låser resurser](aem-forms-repository.md#locking-resources)

[Anropa AEM-formulär med Base64-kodning](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## Resurser tas bort {#deleting-resources}

Du kan ta bort resurser från en viss plats i databasen med hjälp av Java API(SOAP) för databastjänsten.

När du tar bort en resurs är borttagningen vanligtvis permanent, men i vissa fall kan ECM-databaser lagra resursens versioner enligt deras historikmekanismer. När du tar bort en resurs är det därför viktigt att du aldrig behöver den igen. De vanligaste skälen till att en resurs tas bort är behovet av att öka det tillgängliga utrymmet i databasen. Du kan ta bort en version av en resurs, men om du gör det måste du ange resursidentifieraren och inte dess logiska identifierare (LID) eller sökväg. Om du tar bort en mapp tas allt i den mappen, inklusive undermappar och resurser, bort automatiskt.

Relaterade resurser tas inte bort. Om du till exempel har ett formulär som använder filen logo.gif och du tar bort logo.gif, lagras en relation i den väntande relationstabellen. Du kan också ange att objektstatusen för den senaste versionen är inaktuell för borttagning av version.

En raderingsåtgärd är inte transaktionssäker i ECM-system. Om du till exempel försöker ta bort 100 resurser och åtgärden misslyckas på den 50:e resursen, tas de första 49 instanserna bort, men inte resten. I annat fall är standardbeteendet återställning (ej åtagande).

>[!NOTE]
>
>När du använder metoden med ECM-databasen (EMC Documentum Content Server och IBM FileNet P8 Content Manager) återställs inte transaktionen om borttagningen misslyckas för en av de angivna resurserna, vilket innebär att de filer som har tagits bort inte kan återställas. `com.adobe.repository.bindings.dsc.client.ResourceRepositoryClient.deleteResources()`

>[!NOTE]
>
>Mer information om databastjänsten finns i [Tjänstreferens för AEM-formulär](https://www.adobe.com/go/learn_aemforms_services_63).

### Sammanfattning av steg {#summary_of_steps-8}

Så här tar du bort en resurs:

1. Inkludera projektfiler.
1. Skapa en databastjänstklient.
1. Ange URI för resursen som ska tas bort.
1. Ta bort resursen.

**Inkludera projektfiler**

Inkludera nödvändiga filer i utvecklingsprojektet. Om du skapar ett klientprogram med Java, inkluderar du de JAR-filer som behövs. Om du använder webbtjänster inkluderar du proxyfilerna.

**Skapa tjänstklienten**

Innan du kan läsa en resurs programmatiskt måste du skapa en anslutning och ange autentiseringsuppgifter. Detta uppnås genom att en tjänstklient skapas.

**Ange URI för resursen som ska tas bort**

Skapa en sträng som innehåller URI:n för resursen som ska tas bort. Syntaxen innehåller snedstreck, som i det här exemplet: &quot;/*path*/*resource*&quot;. Om resursen som ska tas bort är en mapp kommer borttagningen att vara rekursiv.

**Ta bort resursen**

Anropa databastjänstmetoden för att ta bort resursen och ange URI:n.

**Se även**

[Ta bort resurser med Java API](aem-forms-repository.md#delete-resources-using-the-java-api-soap)

[Ta bort resurser med webbtjänstens API](aem-forms-repository.md#delete-resources-using-the-web-service-api)

[Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Snabbstart för databastjänst-API](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Ta bort resurser med Java API(SOAP) {#delete-resources-using-the-java-api-soap}

Ta bort en resurs med Repository API (Java):

1. Inkludera projektfiler

   Inkludera JAR-klientfiler i Java-projektets klassökväg.

1. Skapa tjänstklienten

   Skapa ett `ResourceRepositoryClient` objekt med hjälp av dess konstruktor och skicka ett `ServiceClientFactory` objekt som innehåller anslutningsegenskaper.

1. Ange URI för resursen som ska tas bort

   Ange URI för resursen som ska hämtas. I det här fallet, eftersom resursen med namnet testResourceToBeDeleted finns i mappen testFolder, är resursens URI `/testFolder/testResourceToBeDeleted`. URI:n lagras som ett `java.lang.String` objekt. I det här exemplet skrivs resursen först till databasen och dess URI hämtas. Mer information om hur du skriver en resurs finns i [Skriva resurser](aem-forms-repository.md#writing-resources).

1. Ta bort resursen

   Anropa `ResourceRepositoryClient` objektets `deleteResource` metod och skicka URI:n för resursen som en parameter.

**Se även**

[Resurser tas bort](aem-forms-repository.md#deleting-resources)

[Snabbstart (SOAP-läge): Söka efter resurser med Java API](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-searching-for-resources-using-the-java-api)

[Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Ta bort resurser med webbtjänstens API {#delete-resources-using-the-web-service-api}

Ta bort en resurs med Repository API (webbtjänsten):

1. Inkludera projektfiler

   * Skapa en Microsoft .NET-klientsammansättning som förbrukar WSDL för databasen med Base64.
   * Referera till Microsoft .NET-klientsammansättningen.

1. Skapa tjänstklienten

   Skapa ett objekt med Microsoft .NET-klientsammansättningen genom att anropa dess standardkonstruktor. `RepositoryServiceService` Ange dess `Credentials` egenskap med ett `System.Net.NetworkCredential` objekt som innehåller användarnamnet och lösenordet.

1. Ange URI för resursen som ska tas bort

   Ange URI för resursen som ska hämtas. I det här fallet, eftersom resursen med namnet `testResourceToBeDeleted` finns i mappen med namnet `testFolder`, är dess URI `"/testFolder/testResourceToBeDeleted"`. I det här exemplet skrivs resursen först till databasen och dess URI hämtas. Mer information om hur du skriver en resurs finns i [Skriva resurser](aem-forms-repository.md#writing-resources).

1. Ta bort resursen

   Anropa `RepositoryServiceService` objektets `deleteResources` metod och skicka en `System.String` array som innehåller resursens URI som första parameter. Skicka `null` för den andra parametern.

**Se även**

[Resurser tas bort](aem-forms-repository.md#deleting-resources)

[Anropa AEM-formulär med Base64-kodning](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
