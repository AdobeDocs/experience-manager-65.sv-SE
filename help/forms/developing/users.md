---
title: Hantera användare
description: Använd API:t för användarhantering för att skapa klientprogram som kan hantera roller, behörigheter och huvudkonton (som kan vara användare eller grupper) och autentisera användare.
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: d7c5bb84-a988-4b2e-a587-f4e5b50fea58
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '6218'
ht-degree: 0%

---

# Hantera användare {#managing-users}

**Exempel och exempel i det här dokumentet är bara för AEM Forms i JEE-miljö.**

**Om användarhantering**

Du kan använda API:t för användarhantering för att skapa klientprogram som kan hantera roller, behörigheter och principer (som kan vara användare eller grupper) och autentisera användare. API:t för användarhantering består av följande AEM Forms-API:er:

* API för kataloghanterartjänst
* Tjänst-API för Autentiseringshanteraren
* Tjänst-API för auktoriseringshanteraren

Med Hantering av användare kan du tilldela, ta bort och bestämma roller och behörigheter. Du kan också tilldela, ta bort och fråga domäner, användare och grupper. Slutligen kan du använda Hantering av användare för att autentisera användare.

I [Lägga till användare](users.md#adding-users) du kommer att förstå hur du programmässigt lägger till användare. I det här avsnittet används API:t för kataloghanterartjänsten.

I [Ta bort användare](users.md#deleting-users) du kommer att förstå hur du tar bort användare programmatiskt. I det här avsnittet används API:t för kataloghanterartjänsten.

I [Hantera användare och grupper](users.md#managing-users-and-groups) du kommer att förstå skillnaden mellan en lokal användare och en kataloganvändare och se exempel på hur du använder Java- och webbtjänstens API:er för att programmässigt hantera användare och grupper. I det här avsnittet används API:t för kataloghanterartjänsten.

I [Hantera roller och behörigheter](users.md#managing-roles-and-permissions) du får lära dig mer om systemroller och behörigheter och vad du kan göra med programmering för att förstärka dem, och se exempel på hur du använder Java- och webbtjänstens API:er för att programmässigt hantera roller och behörigheter. I det här avsnittet används både API:t för kataloghanterarens tjänst och API:t för auktoriseringshanterarens tjänst.

I [Autentiserar användare](users.md#authenticating-users) finns exempel på hur du använder Java- och webbtjänstens API:er för att programmässigt autentisera användare. I det här avsnittet används API:t för tjänsten Authorization Manager.

**Om autentiseringsprocessen**

Användarhantering har inbyggda autentiseringsfunktioner och ger dig även möjlighet att ansluta den till din egen autentiseringsleverantör. När Hantering av användare tar emot en autentiseringsbegäran (t.ex. en användare försöker logga in) skickas användarinformation till autentiseringsprovidern. Användarhantering får resultaten från autentiseringsprovidern efter att användaren har autentiserats.

I följande diagram visas interaktionen mellan en slutanvändare som försöker logga in, användarhantering och autentiseringsprovidern.

![mu_mu_umauth_process](assets/mu_mu_umauth_process.png)

I följande tabell beskrivs varje steg i autentiseringsprocessen.

<table>
 <thead>
  <tr>
   <th><p>Steg</p></th>
   <th><p>Beskrivning</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>1</p></td>
   <td><p>En användare försöker logga in på en tjänst som anropar Användarhantering. Användaren anger ett användarnamn och lösenord. </p></td>
  </tr>
  <tr>
   <td><p>2</p></td>
   <td><p>Användarhantering skickar användarnamn, lösenord och konfigurationsinformation till autentiseringsprovidern.</p></td>
  </tr>
  <tr>
   <td><p>3</p></td>
   <td><p>Autentiseringsprovidern ansluter till användararkivet och autentiserar användaren.</p></td>
  </tr>
  <tr>
   <td><p>4</p></td>
   <td><p>Autentiseringsprovidern returnerar resultaten till Användarhantering.</p></td>
  </tr>
  <tr>
   <td><p>5</p></td>
   <td><p>Med användarhantering kan användaren antingen logga in eller neka åtkomst till produkten.</p></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Om serverns tidszon inte är densamma som klientens tidszon kan följande autentiseringsfel uppstå när WSDL för tjänsten AEM Forms Generate PDF används i en inbyggd SOAP-stack med en .NET-klient i ett WebSphere Application Server-kluster:

`[com.adobe.idp.um.webservices.WSSecurityHandler] errorCode:12803 errorCodeHEX:0x3203 message:WSSecurityHandler: UM authenticate returns exception : An error was discovered processing the <wsse:Security> header. (WSSecurityEngine: Invalid timestamp The security semantics of message have expired).`

**Om kataloghantering**

Användarhantering paketeras med en katalogtjänstleverantör (DirectoryManagerService) som stöder anslutningar till LDAP-kataloger. Om din organisation använder en annan databas än LDAP för att lagra användarposter, kan du skapa en egen katalogtjänstleverantör som fungerar med din databas.

Katalogtjänstleverantörer hämtar poster från ett användararkiv på begäran av användarhantering. Användarhantering cachelagrar regelbundet användar- och gruppposter i databasen för att förbättra prestandan.

Katalogtjänstprovidern kan användas för att synkronisera användarhanteringsdatabasen med användararkivet. Det här steget ser till att all användarkataloginformation och alla användar- och gruppposter är uppdaterade.

Dessutom kan du med DirectoryManagerService skapa och hantera domäner. Domäner definierar olika användarbaser. Gränsen för en domän definieras vanligtvis utifrån hur din organisation är strukturerad eller hur ditt användararkiv är konfigurerat. Användarhanteringsdomäner innehåller konfigurationsinställningar som autentiseringsproviders och katalogtjänstleverantörer använder.

I den konfigurations-XML som användarhantering exporterar är rotnoden som har attributvärdet `Domains` innehåller ett XML-element för varje domän som definierats för användarhantering. Var och en av dessa element innehåller andra element som definierar aspekter av domänen som är kopplad till specifika tjänsteleverantörer.

**Om objectSID-värden**

När du använder Active Directory är det viktigt att du förstår att `objectSID` värdet är inte ett unikt attribut i flera domäner. Det här värdet lagrar ett objekts säkerhetsidentifierare. I en miljö med flera domäner (till exempel ett träd med domäner) `objectSID` värdet kan vara ett annat.

An `objectSID` värdet ändras om ett objekt flyttas från en Active Directory-domän till en annan. Vissa objekt har samma `objectSID` var som helst i domänen. Grupper som BUILTIN\Administrators, BUILTIN\Power Users osv. har samma `objectSID` värde oavsett domäner. Dessa `objectSID` är välkända.

## Lägga till användare {#adding-users}

Du kan använda kataloghanterarens tjänst-API (Java och webbtjänst) för att lägga till användare i AEM Forms via programkod. När du har lagt till en användare kan du använda den användaren när du utför en tjänståtgärd som kräver en användare. Du kan till exempel tilldela en uppgift till den nya användaren.

### Sammanfattning av steg {#summary-of-steps}

Så här lägger du till en användare:

1. Inkludera projektfiler.
1. Skapa en DirectoryManagerService-klient.
1. Definiera användarinformation.
1. Lägg till användaren i AEM Forms.
1. Kontrollera att användaren har lagts till.

**Inkludera projektfiler**

Inkludera nödvändiga filer i utvecklingsprojektet. Om du skapar ett klientprogram med Java, inkluderar du de JAR-filer som behövs. Om du använder webbtjänster inkluderar du proxyfilerna.

**Skapa en DirectoryManagerService-klient**

Innan du programmässigt kan utföra en kataloghanterartjänståtgärd måste du skapa en katalog Manager-tjänste-API-klient.

**Definiera användarinformation**

När du lägger till en ny användare med hjälp av kataloghanterarens tjänst-API, definierar du information för den användaren. När du lägger till en ny användare anger du vanligtvis följande värden:

* **Domännamn**: Den domän som användaren tillhör (till exempel `DefaultDom`).
* **Användaridentifierarvärde**: Användarens identifierarvärde (till exempel `wblue`).
* **Huvudtyp**: Typen av användare (du kan till exempel ange `USER)`.
* **Förnamn**: Ett angivet namn för användaren (till exempel `Wendy`).
* **Efternamn**: Användarens familjenamn (till exempel `Blue)`.
* **Språk**: Språkinformation för användaren.

**Lägg till användaren i AEM Forms**

När du har definierat användarinformationen kan du lägga till användaren i AEM Forms. Om du vill lägga till en användare anropar du `DirectoryManagerServiceClient` objektets `createLocalUser` -metod.

**Verifiera att användaren har lagts till**

Du kan verifiera att användaren har lagts till för att säkerställa att inga problem uppstod. Hitta den nya användaren med användaridentifierarvärdet.

**Se även**

[Lägga till användare med Java API](users.md#add-users-using-the-java-api)

[Lägga till användare med API:t för webbtjänster](users.md#add-users-using-the-web-service-api)

[Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Ta bort användare](users.md#deleting-users)

### Lägga till användare med Java API {#add-users-using-the-java-api}

Lägg till användare med hjälp av kataloghanterarens tjänst-API (Java):

1. Inkludera projektfiler.

   Inkludera JAR-klientfiler, t.ex. adobe-usermanager-client.jar, i Java-projektets klassökväg.

1. Skapa en DirectoryManagerServices-klient.

   Skapa en `DirectoryManagerServiceClient` genom att använda konstruktorn och skicka ett `ServiceClientFactory` objekt som innehåller anslutningsegenskaper.

1. Definiera användarinformation.

   * Skapa en `UserImpl` genom att använda dess konstruktor.
   * Ange huvudnamnet genom att anropa `UserImpl` objektets `setDomainName` -metod. Skicka ett strängvärde som anger domännamnet.
   * Ange huvudtypen genom att anropa `UserImpl` objektets `setPrincipalType` -metod. Skicka ett strängvärde som anger användartypen. Du kan till exempel ange `USER`.
   * Ange användaridentifierarvärdet genom att anropa `UserImpl` objektets `setUserid` -metod. Skicka ett strängvärde som anger användaridentifierarvärdet. Du kan till exempel ange `wblue`.
   * Ange det kanoniska namnet genom att anropa `UserImpl` objektets `setCanonicalName` -metod. Skicka ett strängvärde som anger användarens kanoniska namn. Du kan till exempel ange `wblue`.
   * Ange det angivna namnet genom att anropa `UserImpl` objektets `setGivenName` -metod. Skicka ett strängvärde som anger användarens angivna namn. Du kan till exempel ange `Wendy`.
   * Ange familjenamnet genom att anropa `UserImpl` objektets `setFamilyName` -metod. Skicka ett strängvärde som anger användarens familjenamn. Du kan till exempel ange `Blue`.

   >[!NOTE]
   >
   >Anropa en metod som tillhör `UserImpl` för att ange andra värden. Du kan till exempel ställa in språkvärdet genom att anropa `UserImpl` objektets `setLocale` -metod.

1. Lägg till användaren i AEM Forms.

   Anropa `DirectoryManagerServiceClient` objektets `createLocalUser` och skicka följande värden:

   * The `UserImpl` objekt som representerar den nya användaren
   * Ett strängvärde som representerar användarens lösenord

   The `createLocalUser` returnerar ett strängvärde som anger det lokala användaridentifierarvärdet.

1. Kontrollera att användaren har lagts till.

   * Skapa en `PrincipalSearchFilter` genom att använda dess konstruktor.
   * Ange användaridentifierarvärdet genom att anropa `PrincipalSearchFilter` objektets `setUserId` -metod. Skicka ett strängvärde som representerar användaridentifierarvärdet.
   * Anropa `DirectoryManagerServiceClient` objektets `findPrincipals` och skicka `PrincipalSearchFilter` -objekt. Den här metoden returnerar en `java.util.List` -instans, där varje element är en `User` -objekt. Iterera genom `java.util.List` -instans för att hitta användaren.

**Se även**

[Sammanfattning av steg](users.md#summary-of-steps)

[Snabbstart (SOAP-läge): Lägga till användare med Java API](/help/forms/developing/user-manager-java-api-quick.md#quick-start-soap-mode-adding-users-using-the-java-api)

[Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Lägga till användare med API:t för webbtjänster {#add-users-using-the-web-service-api}

Lägg till användare med hjälp av kataloghanterarens tjänst-API (webbtjänst):

1. Inkludera projektfiler.

   Skapa ett Microsoft .NET-projekt som använder MTOM. Kontrollera att du använder följande WSDL-definition för tjänstreferensen: `http://localhost:8080/soap/services/DirectoryManagerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Ersätt `localhost` med IP-adressen till den server där AEM Forms finns.

1. Skapa en DirectoryManagerService-klient.

   * Skapa en `DirectoryManagerServiceClient` genom att använda dess standardkonstruktor.
   * Skapa en `DirectoryManagerServiceClient.Endpoint.Address` genom att använda `System.ServiceModel.EndpointAddress` konstruktor. Skicka ett strängvärde som anger WSDL till AEM Forms-tjänsten (till exempel `http://localhost:8080/soap/services/DirectoryManagerService?blob=mtom`). Du behöver inte använda `lc_version` -attribut. Det här attributet används när du skapar en tjänstreferens. Se till att du anger `?blob=mtom`.
   * Skapa en `System.ServiceModel.BasicHttpBinding` genom att hämta värdet för `DirectoryManagerServiceClient.Endpoint.Binding` fält. Skicka returvärdet till `BasicHttpBinding`.
   * Ange `System.ServiceModel.BasicHttpBinding` objektets `MessageEncoding` fält till `WSMessageEncoding.Mtom`. Detta värde garanterar att MTOM används.
   * Aktivera grundläggande HTTP-autentisering genom att utföra följande åtgärder:

      * Tilldela AEM formuläranvändarnamn till fältet `DirectoryManagerServiceClient.ClientCredentials.UserName.UserName`.
      * Tilldela motsvarande lösenordsvärde till fältet `DirectoryManagerServiceClient.ClientCredentials.UserName.Password`.
      * Tilldela konstantvärdet `HttpClientCredentialType.Basic` till fältet `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Tilldela konstantvärdet `BasicHttpSecurityMode.TransportCredentialOnly` till fältet `BasicHttpBindingSecurity.Security.Mode`.

1. Definiera användarinformation.

   * Skapa en `UserImpl` genom att använda dess konstruktor.
   * Ange standardnamnet genom att tilldela ett strängvärde till `UserImpl` objektets `domainName` fält.
   * Ange huvudtypen genom att tilldela ett strängvärde till `UserImpl` objektets `principalType` fält. Du kan till exempel ange `USER`.
   * Ange användaridentifierarvärdet genom att tilldela ett strängvärde till `UserImpl` objektets `userid` fält.
   * Ange det kanoniska namnvärdet genom att tilldela ett strängvärde till `UserImpl` objektets `canonicalName` fält.
   * Ange det angivna namnvärdet genom att tilldela ett strängvärde till `UserImpl` objektets `givenName` fält.
   * Ange familjenamnvärdet genom att tilldela ett strängvärde till `UserImpl` objektets `familyName` fält.

1. Lägg till användaren i AEM Forms.

   Anropa `DirectoryManagerServiceClient` objektets `createLocalUser` och skicka följande värden:

   * The `UserImpl` objekt som representerar den nya användaren
   * Ett strängvärde som representerar användarens lösenord

   The `createLocalUser` returnerar ett strängvärde som anger det lokala användaridentifierarvärdet.

1. Kontrollera att användaren har lagts till.

   * Skapa en `PrincipalSearchFilter` genom att använda dess konstruktor.
   * Ange användaridentifierarvärdet för användaren genom att tilldela ett strängvärde som representerar användaridentifierarvärdet till `PrincipalSearchFilter` objektets `userId` fält.
   * Anropa `DirectoryManagerServiceClient` objektets `findPrincipals` och skicka `PrincipalSearchFilter` -objekt. Den här metoden returnerar en `MyArrayOfUser` samlingsobjekt, där varje element är ett `User` -objekt. Iterera genom `MyArrayOfUser` för att hitta användaren.

**Se även**

[Sammanfattning av steg](users.md#summary-of-steps)

[Anropa AEM Forms med MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Anropa AEM Forms med SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Ta bort användare {#deleting-users}

Du kan använda kataloghanterarens tjänst-API (Java och webbtjänst) för att ta bort användare från AEM Forms programmatiskt. När du har tagit bort en användare kan användaren inte längre användas för att utföra en tjänståtgärd som kräver en användare. Du kan till exempel inte tilldela en uppgift till en borttagen användare.

### Sammanfattning av steg {#summary_of_steps-1}

Så här tar du bort en användare:

1. Inkludera projektfiler.
1. Skapa en DirectoryManagerService-klient.
1. Ange vilken användare som ska tas bort.
1. Ta bort användaren från AEM Forms.

**Inkludera projektfiler**

Inkludera nödvändiga filer i utvecklingsprojektet. Om du skapar ett klientprogram med Java, inkluderar du de JAR-filer som behövs. Om du använder webbtjänster inkluderar du proxyfilerna.

**Skapa en DirectoryManagerService-klient**

Skapa en kataloghanterartjänstklient innan du programmässigt utför en API-åtgärd för en kataloghanterartjänst.

**Ange vilken användare som ska tas bort**

Du kan ange en användare som ska tas bort med användarens identifierarvärde.

**Ta bort användaren från AEM Forms**

Om du vill ta bort en användare anropar du `DirectoryManagerServiceClient` objektets `deleteLocalUser` -metod.

**Se även**

[Ta bort användare med Java API](users.md#delete-users-using-the-java-api)

[Ta bort användare med webbtjänstens API](users.md#delete-users-using-the-web-service-api)

[Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Lägga till användare](users.md#adding-users)

### Ta bort användare med Java API {#delete-users-using-the-java-api}

Ta bort användare med hjälp av kataloghanterarens tjänst-API (Java):

1. Inkludera projektfiler.

   Inkludera JAR-klientfiler, t.ex. adobe-usermanager-client.jar, i Java-projektets klassökväg.

1. Skapa en DirectoryManagerService-klient.

   Skapa en `DirectoryManagerServiceClient` genom att använda konstruktorn och skicka ett `ServiceClientFactory` objekt som innehåller anslutningsegenskaper.

1. Ange vilken användare som ska tas bort.

   * Skapa en `PrincipalSearchFilter` genom att använda dess konstruktor.
   * Ange användaridentifierarvärdet genom att anropa `PrincipalSearchFilter` objektets `setUserId` -metod. Skicka ett strängvärde som representerar användaridentifierarvärdet.
   * Anropa `DirectoryManagerServiceClient` objektets `findPrincipals` och skicka `PrincipalSearchFilter` -objekt. Den här metoden returnerar en `java.util.List` -instans, där varje element är en `User` -objekt. Iterera genom `java.util.List` -instans för att hitta användaren som ska tas bort.

1. Ta bort användaren från AEM Forms.

   Anropa `DirectoryManagerServiceClient` objektets `deleteLocalUser` och skicka värdet för `User` objektets `oid` fält. Anropa `User` objektets `getOid` -metod. Använd `User` objektet har hämtats från `java.util.List` -instans.

**Se även**

[Sammanfattning av steg](users.md#summary-of-steps)

[Snabbstart (EJB-läge): Ta bort användare med Java API](/help/forms/developing/user-manager-java-api-quick.md#quick-start-soap-mode-deleting-users-using-the-java-api)

[Snabbstart (SOAP-läge): Ta bort användare med Java API](/help/forms/developing/user-manager-java-api-quick.md#quick-start-soap-mode-deleting-users-using-the-java-api)

[Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Ta bort användare med webbtjänstens API {#delete-users-using-the-web-service-api}

Ta bort användare med hjälp av kataloghanterarens tjänst-API (webbtjänst):

1. Inkludera projektfiler.

   Inkludera JAR-klientfiler, t.ex. adobe-usermanager-client.jar, i Java-projektets klassökväg.

1. Skapa en DirectoryManagerService-klient.

   * Skapa en `DirectoryManagerServiceClient` genom att använda dess standardkonstruktor.
   * Skapa en `DirectoryManagerServiceClient.Endpoint.Address` genom att använda `System.ServiceModel.EndpointAddress` konstruktor. Skicka ett strängvärde som anger WSDL till AEM Forms-tjänsten (till exempel `http://localhost:8080/soap/services/DirectoryManagerService?blob=mtom`). Du behöver inte använda `lc_version` -attribut. Det här attributet används när du skapar en tjänstreferens. Se till att du anger `blob=mtom.`
   * Skapa en `System.ServiceModel.BasicHttpBinding` genom att hämta värdet för `DirectoryManagerServiceClient.Endpoint.Binding` fält. Skicka returvärdet till `BasicHttpBinding`.
   * Ange `System.ServiceModel.BasicHttpBinding` objektets `MessageEncoding` fält till `WSMessageEncoding.Mtom`. Detta värde garanterar att MTOM används.
   * Aktivera grundläggande HTTP-autentisering genom att utföra följande åtgärder:

      * Tilldela AEM formuläranvändarnamn till fältet `DirectoryManagerServiceClient.ClientCredentials.UserName.UserName`.
      * Tilldela motsvarande lösenordsvärde till fältet `DirectoryManagerServiceClient.ClientCredentials.UserName.Password`.
      * Tilldela konstantvärdet `HttpClientCredentialType.Basic` till fältet `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Tilldela konstantvärdet `BasicHttpSecurityMode.TransportCredentialOnly` till fältet `BasicHttpBindingSecurity.Security.Mode`.

1. Ange vilken användare som ska tas bort.

   * Skapa en `PrincipalSearchFilter` genom att använda dess konstruktor.
   * Ange användaridentifierarvärdet genom att tilldela ett strängvärde till `PrincipalSearchFilter` objektets `userId` fält.
   * Anropa `DirectoryManagerServiceClient` objektets `findPrincipals` och skicka `PrincipalSearchFilter` -objekt. Den här metoden returnerar en `MyArrayOfUser` samlingsobjekt, där varje element är ett `User` -objekt. Iterera genom `MyArrayOfUser` för att hitta användaren. The `User` objektet har hämtats från `MyArrayOfUser` samlingsobjekt används för att ta bort användaren.

1. Ta bort användaren från AEM Forms.

   Ta bort användaren genom att skicka `User` objektets `oid` fältvärde till `DirectoryManagerServiceClient` objektets `deleteLocalUser` -metod.

**Se även**

[Sammanfattning av steg](users.md#summary-of-steps)

[Anropa AEM Forms med MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Anropa AEM Forms med SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Skapa grupper {#creating-groups}

Du kan använda API:t för kataloghanteringstjänsten (Java och webbtjänst) för att skapa AEM Forms-grupper programmatiskt. När du har skapat en grupp kan du använda den gruppen för att utföra en tjänståtgärd som kräver en grupp. Du kan till exempel tilldela en användare till den nya gruppen. (Se [Hantera användare och grupper](users.md#managing-users-and-groups).)

### Sammanfattning av steg {#summary_of_steps-2}

Så här skapar du en grupp:

1. Inkludera projektfiler.
1. Skapa en DirectoryManagerService-klient.
1. Kontrollera att gruppen inte finns.
1. Skapa gruppen.
1. Utför en åtgärd med gruppen.

**Inkludera projektfiler**

Inkludera nödvändiga filer i utvecklingsprojektet. Om du skapar ett klientprogram med Java, inkluderar du de JAR-filer som behövs.

Följande JAR-filer måste läggas till i projektets klassökväg:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar (krävs om AEM Forms används i JBoss)
* jbossall-client.jar (krävs om AEM Forms distribueras på JBoss)

Mer information om var dessa JAR-filer finns i [Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Skapa en DirectoryManagerService-klient**

Innan du programmässigt kan utföra en kataloghanterartjänståtgärd måste du skapa en katalog Manager-tjänste-API-klient.

**Kontrollera om gruppen finns**

När du skapar en grupp kontrollerar du att gruppen inte finns i samma domän. Två grupper kan alltså inte ha samma namn inom samma domän. Om du vill utföra den här åtgärden gör du en sökning och filtrerar sökresultaten baserat på två värden. Ställ in huvudtypen till `com.adobe.idp.um.api.infomodel.Principal.PRINCIPALTYPE_GROUP` för att säkerställa att endast grupper returneras. Se även till att du anger domännamnet.

**Skapa gruppen**

När du har fastställt att gruppen inte finns i domänen skapar du gruppen och anger följande attribut:

* **CommonName**: Namnet på gruppen.
* **Domän**: Den domän som gruppen läggs till i.
* **Beskrivning**: En beskrivning av gruppen.

**Utför en åtgärd med gruppen**

När du har skapat en grupp kan du utföra en åtgärd med gruppen. Du kan till exempel lägga till en användare i gruppen. Om du vill lägga till en användare i en grupp hämtar du det unika identifieringsvärdet för både användaren och gruppen. Skicka dessa värden till `addPrincipalToLocalGroup` -metod.

**Se även**

[Skapa grupper med Java API](users.md#create-groups-using-the-java-api)

[Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Lägga till användare](users.md#adding-users)

[Ta bort användare](users.md#deleting-users)

### Skapa grupper med Java API {#create-groups-using-the-java-api}

Skapa en grupp med hjälp av kataloghanterarens tjänst-API (Java):

1. Inkludera projektfiler.

   Inkludera JAR-klientfiler, t.ex. adobe-usermanager-client.jar, i Java-projektets klassökväg.

1. Skapa en DirectoryManagerService-klient.

   Skapa en `DirectoryManagerServiceClient` genom att använda konstruktorn och skicka ett `ServiceClientFactory` objekt som innehåller anslutningsegenskaper.

1. Avgör om gruppen finns.

   * Skapa en `PrincipalSearchFilter` genom att använda dess konstruktor.
   * Ange huvudtypen genom att anropa `PrincipalSearchFilter` objektets `setPrincipalType` -objekt. Skicka värdet `com.adobe.idp.um.api.infomodel.Principal.PRINCIPALTYPE_GROUP`.
   * Ange domänen genom att anropa `PrincipalSearchFilter` objektets `setSpecificDomainName` -objekt. Skicka ett strängvärde som anger domännamnet.
   * Om du vill söka efter en grupp anropar du `DirectoryManagerServiceClient` objektets `findPrincipals` metod (ett huvudnamn kan vara en grupp). Skicka `PrincipalSearchFilter` objekt som anger huvudtypen och domännamnet. Den här metoden returnerar en `java.util.List` instans där varje element är en `Group` -instans. Varje gruppinstans följer det filter som anges med `PrincipalSearchFilter` -objekt.
   * Iterera genom `java.util.List` -instans. Hämta gruppnamnet för varje element. Kontrollera att gruppnamnet inte är lika med det nya gruppnamnet.

1. Skapa gruppen.

   * Om gruppen inte finns, anropar du `Group` objektets `setCommonName` och skicka ett strängvärde som anger gruppnamnet.
   * Anropa `Group` objektets `setDescription` och skicka ett strängvärde som anger gruppbeskrivningen.
   * Anropa `Group` objektets `setDomainName` och skicka ett strängvärde som anger domännamnet.
   * Anropa `DirectoryManagerServiceClient` objektets `createLocalGroup` och skicka `Group` -instans.

   The `createLocalUser` returnerar ett strängvärde som anger det lokala användaridentifierarvärdet.

1. Utför en åtgärd med gruppen.

   * Skapa en `PrincipalSearchFilter` genom att använda dess konstruktor.
   * Ange användaridentifierarvärdet genom att anropa `PrincipalSearchFilter` objektets `setUserId` -metod. Skicka ett strängvärde som representerar användaridentifierarvärdet.
   * Anropa `DirectoryManagerServiceClient` objektets `findPrincipals` och skicka `PrincipalSearchFilter` -objekt. Den här metoden returnerar en `java.util.List` -instans, där varje element är en `User` -objekt. Iterera genom `java.util.List` -instans för att hitta användaren.
   * Lägg till en användare i gruppen genom att anropa `DirectoryManagerServiceClient` objektets `addPrincipalToLocalGroup` -metod. Skicka returvärdet för `User` objektets `getOid` -metod. Skicka returvärdet för `Group` objekt `getOid` metod (använd `Group` -instans som representerar den nya gruppen).

**Se även**

[Sammanfattning av steg](users.md#summary-of-steps)

[Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Hantera användare och grupper {#managing-users-and-groups}

I det här avsnittet beskrivs hur du kan använda (Java) för att programmässigt tilldela, ta bort och fråga domäner, användare och grupper.

>[!NOTE]
>
>När du konfigurerar en domän måste du ange den unika identifieraren för grupper och användare. Attributet som väljs får inte bara vara unikt i LDAP-miljön, utan måste också vara oföränderligt och kan inte ändras i katalogen. Attributet måste också vara av en enkel strängdatatyp (det enda undantag som för närvarande tillåts för Active Directory 2000/2003 är `"objectsid"`, som är ett binärvärde). Novell eDirectory-attributet `"GUID"`är till exempel inte en enkel strängdatatyp och kommer därför inte att fungera.

* För Active Directory använder du `"objectsid"`.
* För SunOne, använd `"nsuniqueid"`.

>[!NOTE]
>
>Det går inte att skapa flera lokala användare och grupper medan en LDAP-katalogsynkronisering pågår. Om du försöker utföra den här processen kan det leda till fel.

### Sammanfattning av steg {#summary_of_steps-3}

Så här hanterar du användare och grupper:

1. Inkludera projektfiler.
1. Skapa en DirectoryManagerService-klient.
1. Anropa lämpliga användar- eller gruppåtgärder.

**Inkludera projektfiler**

Inkludera nödvändiga filer i utvecklingsprojektet. Om du skapar ett klientprogram med Java inkluderar du de JAR-filer som behövs. Om du använder webbtjänster måste du inkludera proxyfilerna.

**Skapa en DirectoryManagerService-klient**

Innan du programmässigt kan utföra en kataloghanterartjänståtgärd måste du skapa en kataloghanterartjänstklient. Med Java API kan du uppnå detta genom att skapa en `DirectoryManagerServiceClient` -objekt. Med webbtjänste-API:t uppnås detta genom att skapa en `DirectoryManagerServiceService` -objekt.

**Anropa lämpliga användar- eller gruppåtgärder**

När du har skapat tjänstklienten kan du sedan anropa användar- eller grupphanteringsåtgärderna. Med tjänstklienten kan du tilldela, ta bort och fråga domäner, användare och grupper. Observera att det går att lägga till ett katalogobjekt eller ett lokalt säkerhetsobjekt i en lokal grupp, men det går inte att lägga till ett lokalt säkerhetsobjekt i en kataloggrupp.

**Se även**

[Hantera användare och grupper med Java API](users.md#managing-users-and-groups-using-the-java-api)

[Hantera användare och grupper med webbtjänstens API](users.md#managing-users-and-groups-using-the-web-service-api)

[Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[API-snabbstart för användarhanteraren](/help/forms/developing/user-manager-java-api-quick.md#user-manager-java-api-quick-start-soap)

### Hantera användare och grupper med Java API {#managing-users-and-groups-using-the-java-api}

Utför följande uppgifter för att programmässigt hantera användare, grupper och domäner med (Java):

1. Inkludera projektfiler.

   Inkludera JAR-klientfiler, t.ex. adobe-usermanager-client.jar, i Java-projektets klassökväg. Information om platsen för dessa filer finns i [Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

1. Skapa en DirectoryManagerService-klient.

   Skapa en `DirectoryManagerServiceClient` genom att använda konstruktorn och skicka ett `ServiceClientFactory` objekt som innehåller anslutningsegenskaper. Mer information finns i [Ange anslutningsegenskaper ](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)*.*

1. Anropa lämpliga användar- eller gruppåtgärder.

   Om du vill hitta en användare eller grupp anropar du en av `DirectoryManagerServiceClient` objektets metoder för att söka efter objekt (eftersom ett huvudnamn kan vara en användare eller en grupp). I exemplet nedan är `findPrincipals` metoden anropas med ett sökfilter (en `PrincipalSearchFilter` -objekt).

   Eftersom returvärdet i det här fallet är `java.util.List` innehållande `Principal` objekt, iterera genom resultatet och byta `Principal` objekt till antingen `User` eller `Group` objekt.

   Använda resultatet `User` eller `Group` objekt (som båda ärver från `Principal` -gränssnitt), hämta den information du behöver i dina arbetsflöden. Domännamnet och kanoniska namnvärden är i kombination unika för ett huvudnamn. Dessa hämtas genom att anropa `Principal` objektets `getDomainName` och `getCanonicalName` -metoder.

   Om du vill ta bort en lokal användare anropar du `DirectoryManagerServiceClient` objektets `deleteLocalUser` och skicka användarens identifierare.

   Om du vill ta bort en lokal grupp anropar du `DirectoryManagerServiceClient` objektets `deleteLocalGroup` och skicka gruppens identifierare.

**Se även**

[Sammanfattning av steg](users.md#summary-of-steps)

[Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Hantera användare och grupper med webbtjänstens API {#managing-users-and-groups-using-the-web-service-api}

Utför följande uppgifter för att programmässigt hantera användare, grupper och domäner med hjälp av kataloghanterarens tjänst-API (webbtjänst):

1. Inkludera projektfiler.

   * Skapa en Microsoft .NET-klientsammansättning som använder kataloghanterarens WSDL. (Se [Anropa AEM Forms med Base64-kodning](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding).)
   * Referera till Microsoft .NET-klientsammansättningen. (Se [Skapa en .NET-klientsammansättning som använder Base64-kodning](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding).)

1. Skapa en DirectoryManagerService-klient.

   Skapa en `DirectoryManagerServiceService` genom att använda konstruktorn för klassen proxy.

1. Anropa lämpliga användar- eller gruppåtgärder.

   Om du vill hitta en användare eller grupp anropar du en av `DirectoryManagerServiceService` objektets metoder för att söka efter objekt (eftersom ett huvudnamn kan vara en användare eller en grupp). I exemplet nedan är `findPrincipalsWithFilter` metoden anropas med ett sökfilter (en `PrincipalSearchFilter` -objekt). När en `PrincipalSearchFilter` objekt, lokala huvudobjekt returneras bara om `isLocal` egenskapen är inställd på `true`. Detta beteende skiljer sig från vad som skulle hända med Java API.

   >[!NOTE]
   >
   >Om det maximala antalet resultat inte anges i sökfiltret (via `PrincipalSearchFilter.resultsMax` ) returneras maximalt 1000 resultat. Detta är ett annat beteende än det som inträffar med Java API, där 10 resultat är standardvärdet. Sökmetoder som `findGroupMembers` kommer inte att ge några resultat såvida inte det maximala antalet resultat anges i sökfiltret (till exempel genom `GroupMembershipSearchFilter.resultsMax` fält). Detta gäller alla sökfilter som ärver från `GenericSearchFilter` klassen. Mer information finns i [AEM Forms API-referens](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

   Eftersom returvärdet i det här fallet är ett `object[]` innehållande `Principal` objekt, iterera genom resultatet och byta `Principal` objekt till antingen `User` eller `Group` objekt.

   Använda resultatet `User` eller `Group` objekt (som båda ärver från `Principal` -gränssnitt), hämta den information du behöver i dina arbetsflöden. Domännamnet och kanoniska namnvärden är i kombination unika för ett huvudnamn. Dessa hämtas genom att anropa `Principal` objektets `domainName` och `canonicalName` fält.

   Om du vill ta bort en lokal användare anropar du `DirectoryManagerServiceService` objektets `deleteLocalUser` och skicka användarens identifierare.

   Om du vill ta bort en lokal grupp anropar du `DirectoryManagerServiceService` objektets `deleteLocalGroup` och skicka gruppens identifierare.

**Se även**

[Sammanfattning av steg](users.md#summary-of-steps)

[Anropa AEM Forms med MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

## Hantera roller och behörigheter {#managing-roles-and-permissions}

I det här avsnittet beskrivs hur du kan använda Java (Authorization Manager Service API) för att programmässigt tilldela, ta bort och fastställa roller och behörigheter.

I AEM FORMS *roll* är en grupp behörigheter för åtkomst till en eller flera resurser på systemnivå. Dessa behörigheter skapas med hjälp av användarhantering och används av tjänstkomponenterna. En administratör kan t.ex. tilldela rollen &quot;Principuppsättningens författare&quot; till en grupp användare. Rights Management skulle sedan tillåta användare i den gruppen med den rollen att skapa principuppsättningar via administrationskonsolen.

Det finns två typer av roller: *standardroller* och *anpassade roller*. Standardroller (*systemroller)* redan bor i AEM Forms. Det antas att standardroller inte kan tas bort eller ändras av administratören och därför inte kan ändras. Anpassade roller som skapas av administratören, som senare kan ändra eller ta bort dem, kan därför ändras.

Roller gör det enklare att hantera behörigheter. När en roll tilldelas till ett huvudkonto tilldelas automatiskt en uppsättning behörigheter till det huvudkontot, och alla specifika åtkomstrelaterade beslut för huvudkontot baseras på den övergripande uppsättningen tilldelade behörigheter.

### Sammanfattning av steg {#summary_of_steps-4}

Så här hanterar du roller och behörigheter:

1. Inkludera projektfiler.
1. Skapa en AuthorizationManagerService-klient.
1. Anropa lämpliga roll- eller behörighetsåtgärder.

**Inkludera projektfiler**

Inkludera nödvändiga filer i utvecklingsprojektet. Om du skapar ett klientprogram med Java inkluderar du de JAR-filer som behövs. Om du använder webbtjänster måste du inkludera proxyfilerna.

**Skapa en AuthorizationManagerService-klient**

Innan du programmässigt kan utföra en AuthorizationManagerService-åtgärd måste du skapa en AuthorizationManagerService-klient. Med Java API kan du uppnå detta genom att skapa en `AuthorizationManagerServiceClient` -objekt.

**Anropa lämpliga roll- eller behörighetsåtgärder**

När du har skapat tjänstklienten kan du sedan anropa rollen eller behörighetsåtgärderna. Med tjänstklienten kan du tilldela, ta bort och fastställa roller och behörigheter.

**Se även**

[Hantera roller och behörigheter med Java API](users.md#managing-roles-and-permissions-using-the-java-api)

[Hantera roller och behörigheter med webbtjänstens API](users.md#managing-roles-and-permissions-using-the-web-service-api)

[Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[API-snabbstart för användarhanteraren](/help/forms/developing/user-manager-java-api-quick.md#user-manager-java-api-quick-start-soap)

### Hantera roller och behörigheter med Java API {#managing-roles-and-permissions-using-the-java-api}

Så här hanterar du roller och behörigheter med Java (Authorization Manager Service API):

1. Inkludera projektfiler.

   Inkludera JAR-klientfiler, t.ex. adobe-usermanager-client.jar, i Java-projektets klassökväg.

1. Skapa en AuthorizationManagerService-klient.

   Skapa en `AuthorizationManagerServiceClient` genom att använda konstruktorn och skicka ett `ServiceClientFactory` objekt som innehåller anslutningsegenskaper.

1. Anropa lämpliga roll- eller behörighetsåtgärder.

   Om du vill tilldela en roll till ett huvudkonto anropar du `AuthorizationManagerServiceClient` objektets `assignRole` och skicka följande värden:

   * A `java.lang.String` objekt som innehåller rollidentifieraren
   * En array med `java.lang.String` objekt som innehåller huvudidentifierare.

   Om du vill ta bort en roll från ett huvudkonto anropar du `AuthorizationManagerServiceClient` objektets `unassignRole` och skicka följande värden:

   * A `java.lang.String` objekt som innehåller rollidentifieraren.
   * En array med `java.lang.String` objekt som innehåller huvudidentifierare.

**Se även**

[Sammanfattning av steg](users.md#summary-of-steps)

[Snabbstart (SOAP-läge): Hantera roller och behörigheter med Java API](/help/forms/developing/user-manager-java-api-quick.md#quick-start-soap-mode-managing-roles-and-permissions-using-the-java-api)

[Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Hantera roller och behörigheter med webbtjänstens API {#managing-roles-and-permissions-using-the-web-service-api}

Hantera roller och behörigheter med hjälp av API:t för tjänsten Authorization Manager (webbtjänst):

1. Inkludera projektfiler.

   Skapa ett Microsoft .NET-projekt som använder MTOM. Kontrollera att du använder följande WSDL-definition: `http://localhost:8080/soap/services/AuthorizationManagerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Ersätt `localhost` med IP-adressen till den server där AEM Forms finns.

1. Skapa en AuthorizationManagerService-klient.

   * Skapa en `AuthorizationManagerServiceClient` genom att använda dess standardkonstruktor.
   * Skapa en `AuthorizationManagerServiceClient.Endpoint.Address` genom att använda `System.ServiceModel.EndpointAddress` konstruktor. Skicka ett strängvärde som anger WSDL till AEM Forms-tjänsten (till exempel `http://localhost:8080/soap/services/AuthorizationManagerService?blob=mtom`.) Du behöver inte använda `lc_version` -attribut. Det här attributet används när du skapar en tjänstreferens.
   * Skapa en `System.ServiceModel.BasicHttpBinding` genom att hämta värdet för `AuthorizationManagerServiceClient.Endpoint.Binding` fält. Skicka returvärdet till `BasicHttpBinding`.
   * Ange `System.ServiceModel.BasicHttpBinding` objektets `MessageEncoding` fält till `WSMessageEncoding.Mtom`. Detta värde garanterar att MTOM används.
   * Aktivera grundläggande HTTP-autentisering genom att utföra följande åtgärder:

      * Tilldela AEM formuläranvändarnamn till fältet `AuthorizationManagerServiceClient.ClientCredentials.UserName.UserName`.
      * Tilldela motsvarande lösenordsvärde till fältet `AuthorizationManagerServiceClient.ClientCredentials.UserName.Password`.
      * Tilldela konstantvärdet `HttpClientCredentialType.Basic` till fältet `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Tilldela konstantvärdet `BasicHttpSecurityMode.TransportCredentialOnly` till fältet `BasicHttpBindingSecurity.Security.Mode`.

1. Anropa lämpliga roll- eller behörighetsåtgärder.

   Om du vill tilldela en roll till ett huvudkonto anropar du `AuthorizationManagerServiceClient` objektets `assignRole` och skicka följande värden:

   * A `string` objekt som innehåller rollidentifieraren
   * A `MyArrayOf_xsd_string` objekt som innehåller huvudidentifierare.

   Om du vill ta bort en roll från ett huvudkonto anropar du `AuthorizationManagerServiceService` objektets `unassignRole` och skicka följande värden:

   * A `string` objekt som innehåller rollidentifieraren.
   * En array med `string` objekt som innehåller huvudidentifierare.

**Se även**

[Sammanfattning av steg](users.md#summary-of-steps)

[Anropa AEM Forms med MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

## Autentiserar användare {#authenticating-users}

I det här avsnittet beskrivs hur du kan använda tjänstAPI:t för Autentiseringshanteraren (Java) för att göra det möjligt för dina klientprogram att autentisera användare via programkod.

Användarautentisering kan krävas för interaktion med en företagsdatabas eller andra företagsdatabaser där säkra data lagras.

Tänk dig till exempel ett scenario där en användare anger ett användarnamn och lösenord på en webbsida och skickar värdena till en J2EE-programserver som är värd för Forms. Ett anpassat Forms-program kan autentisera användaren med tjänsten Autentiseringshanteraren.

Om autentiseringen lyckas får programmet åtkomst till en skyddad företagsdatabas. Annars skickas ett meddelande till användaren om att användaren inte är en behörig användare.

I följande diagram visas programmets logikflöde.

![au_au_umauth_process](assets/au_au_umauth_process.png)

I följande tabell beskrivs stegen i det här diagrammet

<table>
 <thead>
  <tr>
   <th><p>Steg</p></th>
   <th><p>Beskrivning</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>1</p></td>
   <td><p>Användaren kommer åt en webbplats och anger användarnamn och lösenord. Den här informationen skickas till en J2EE-programserver som är värd för AEM Forms.</p></td>
  </tr>
  <tr>
   <td><p>2</p></td>
   <td><p>Autentiseringsuppgifterna autentiseras med tjänsten Autentiseringshanteraren. Om inloggningsuppgifterna är giltiga fortsätter arbetsflödet till steg 3. Annars skickas ett meddelande till användaren om att användaren inte är en behörig användare.</p></td>
  </tr>
  <tr>
   <td><p>3</p></td>
   <td><p>Användarinformation och formulärdesign hämtas från en skyddad företagsdatabas. </p></td>
  </tr>
  <tr>
   <td><p>4</p></td>
   <td><p>Användarinformationen sammanfogas med en formulärdesign och formuläret återges för användaren. </p></td>
  </tr>
 </tbody>
</table>

### Sammanfattning av steg {#summary_of_steps-5}

Så här autentiserar du en användare programmatiskt:

1. Inkludera projektfiler.
1. Skapa en AuthenticationManagerService-klient.
1. Anropa autentiseringsåtgärden.
1. Hämta vid behov kontexten så att klientprogrammet kan vidarebefordra den till en annan AEM Forms-tjänst för autentisering.

**Inkludera projektfiler**

Inkludera nödvändiga filer i utvecklingsprojektet. Om du skapar ett klientprogram med Java inkluderar du de JAR-filer som behövs. Om du använder webbtjänster måste du inkludera proxyfilerna.

**Skapa en AuthenticationManagerService-klient**

Innan du kan autentisera en användare programmatiskt måste du skapa en AuthenticationManagerService-klient. Skapa en `AuthenticationManagerServiceClient` -objekt.

**Aktivera autentiseringsåtgärden**

När du har skapat tjänstklienten kan du sedan anropa autentiseringsåtgärden. Den här åtgärden kräver information om användaren, t.ex. användarens namn och lösenord. Om användaren inte autentiserar genereras ett undantag.

**Hämta autentiseringskontexten**

När du har autentiserat användaren kan du skapa en kontext baserad på den autentiserade användaren. Sedan kan du använda innehållet för att anropa andra AEM Forms-tjänster. Du kan till exempel använda kontexten för att skapa en `EncryptionServiceClient` och kryptera ett PDF-dokument med ett lösenord. Kontrollera att den autentiserade användaren har rollen namngiven `Services User` som krävs för att anropa en AEM Forms-tjänst.

**Se även**

[Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[API-snabbstart för användarhanteraren](/help/forms/developing/user-manager-java-api-quick.md#user-manager-java-api-quick-start-soap)

[Kryptera PDF-dokument med ett lösenord](/help/forms/developing/encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)

### Autentisera en användare med Java API {#authenticate-a-user-using-the-java-api}

Autentisera en användare med tjänstens API (Java) för Autentiseringshanteraren:

1. Inkludera projektfiler.

   Inkludera JAR-klientfiler, t.ex. adobe-usermanager-client.jar, i Java-projektets klassökväg.

1. Skapa en AuthenticationManagerServices-klient.

   Skapa en `AuthenticationManagerServiceClient` genom att använda konstruktorn och skicka ett `ServiceClientFactory` objekt som innehåller anslutningsegenskaper.

1. Anropa autentiseringsåtgärden.

   Anropa `AuthenticationManagerServiceClient` objektets `authenticate` och skicka följande värden:

   * A `java.lang.String` som innehåller användarens namn.
   * En bytearray (en `byte[]` -objekt) som innehåller användarens lösenord. Du kan få `byte[]` genom att anropa `java.lang.String` objektets `getBytes` -metod.

   Metoden authenticate returnerar en `AuthResult` -objekt som innehåller information om den autentiserade användaren.

1. Hämta autentiseringskontexten.

   Anropa `ServiceClientFactory` objektets `getContext` som returnerar en `Context` -objekt.

   Anropa sedan `Context` objektets `initPrincipal` och skicka `AuthResult`.

### Autentisera en användare med webbtjänstens API {#authenticate-a-user-using-the-web-service-api}

Autentisera en användare med Authentication Manager Service API (webbtjänst):

1. Inkludera projektfiler.

   * Skapa en Microsoft .NET-klientsammansättning som använder WSDL för autentiseringshanteraren. (Se [Anropa AEM Forms med Base64-kodning](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding).)
   * Referera till Microsoft .NET-klientsammansättningen. (Se &quot;Referera till .NET-klientsammansättningen&quot; i [Anropa AEM Forms med Base64-kodning](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding).)

1. Skapa en AuthenticationManagerService-klient.

   Skapa en `AuthenticationManagerServiceService` genom att använda konstruktorn för klassen proxy.

1. Anropa autentiseringsåtgärden.

   Anropa `AuthenticationManagerServiceClient` objektets `authenticate` och skicka följande värden:

   * A `string` objekt som innehåller användarens namn
   * En bytearray (en `byte[]` -objekt) som innehåller användarens lösenord. Du kan få `byte[]` objekt genom att konvertera ett `string` objekt som innehåller lösenordet till ett `byte[]` arrayen med hjälp av den logik som visas i exemplet nedan.
   * Det returnerade värdet blir ett `AuthResult` -objekt, som kan användas för att hämta information om användaren. I exemplet nedan hämtas användarens information genom att först hämta `AuthResult` objektets `authenticatedUser` och därefter hämta resultatet `User` objektets `canonicalName` och `domainName` fält.

**Se även**

[Anropa AEM Forms med MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Anropa AEM Forms med SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Synkronisera användare programmatiskt {#programmatically-synchronizing-users}

Du kan synkronisera användare programmatiskt med API:t för användarhantering. När du synkroniserar användare uppdaterar du AEM Forms med användardata som finns i din användardatabas. Anta till exempel att du lägger till nya användare i din användardatabas. När du har utfört en synkroniseringsåtgärd blir de nya användarna AEM formuläranvändare. Även användare som inte längre finns i din användardatabas tas bort från AEM Forms.

I följande diagram visas AEM Forms-synkronisering med en användardatabas.

![ps_ps_umauth_sync](assets/ps_ps_umauth_sync.png)

I följande tabell beskrivs stegen i det här diagrammet

<table>
 <thead>
  <tr>
   <th><p>Steg</p></th>
   <th><p>Beskrivning</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>1</p></td>
   <td><p>Ett klientprogram begär att AEM Forms utför en synkroniseringsåtgärd.</p></td>
  </tr>
  <tr>
   <td><p>2</p></td>
   <td><p>AEM Forms utför en synkroniseringsåtgärd.</p></td>
  </tr>
  <tr>
   <td><p>3</p></td>
   <td><p>Användarinformationen uppdateras.</p></td>
  </tr>
  <tr>
   <td><p>4</p></td>
   <td><p>En användare kan visa den uppdaterade användarinformationen. </p></td>
  </tr>
 </tbody>
</table>

### Sammanfattning av steg {#summary_of_steps-6}

Så här synkroniserar du användare programmatiskt:

1. Inkludera projektfiler.
1. Skapa en UserManagerUtilServiceClient-klient.
1. Ange företagsdomänen.
1. Anropa autentiseringsåtgärden.
1. Kontrollera om synkroniseringsåtgärden är slutförd

**Inkludera projektfiler**

Inkludera nödvändiga filer i utvecklingsprojektet. Om du skapar ett klientprogram med Java inkluderar du de JAR-filer som behövs. Om du använder webbtjänster måste du inkludera proxyfilerna.

**Skapa en UserManagerUtilServiceClientclient**

Innan du kan synkronisera användare programmatiskt måste du skapa en `UserManagerUtilServiceClient` -objekt.

**Ange företagsdomänen**

Innan du utför en synkroniseringsåtgärd med API:t för användarhantering anger du den företagsdomän som användarna tillhör. Du kan ange en eller flera företagsdomäner. Innan du programmässigt kan utföra en synkroniseringsåtgärd måste du konfigurera en företagsdomän med hjälp av administrationskonsolen. (Se [administrationshjälp](https://www.adobe.com/go/learn_aemforms_admin_63).)

**Aktivera synkroniseringsåtgärden**

När du har angett en eller flera företagsdomäner kan du utföra synkroniseringsåtgärden. Hur lång tid det tar att utföra den här åtgärden beror på antalet användarposter som finns i användardatabasen.

**Kontrollera om synkroniseringsåtgärden är slutförd**

När du har utfört en synkroniseringsåtgärd programmatiskt kan du avgöra om åtgärden är slutförd.

**Se även**

[Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[API-snabbstart för användarhanteraren](/help/forms/developing/user-manager-java-api-quick.md#user-manager-java-api-quick-start-soap)

[Kryptera PDF-dokument med ett lösenord](/help/forms/developing/encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)

### Synkronisera användare programmatiskt med Java API {#programmatically-synchronizing-users-using-the-java-api}

Synkronisera användare med hjälp av API:t för användarhantering (Java):

1. Inkludera projektfiler.

   Inkludera JAR-klientfiler, t.ex. adobe-usermanager-client.jar och adobe-usermanager-util-client.jar, i Java-projektets klassökväg.

1. Skapa en UserManagerUtilServiceClient-klient.

   Skapa en `UserManagerUtilServiceClient` genom att använda konstruktorn och skicka ett `ServiceClientFactory` objekt som innehåller anslutningsegenskaper.

1. Ange företagsdomänen.

   * Anropa `UserManagerUtilServiceClient` objektets `scheduleSynchronization` metod för att starta användarsynkroniseringen.
   * Skapa en `java.util.Set` instans med hjälp av en `HashSet` konstruktor. Se till att du anger `String` som datatyp. Detta `Java.util.Set` -instansen lagrar de domännamn som synkroniseringsåtgärden gäller för.
   * För varje domännamn som ska läggas till anropar du `java.util.Set` objektets add-metod och skicka domännamnet.

1. Anropa synkroniseringsåtgärden.

   Anropa `ServiceClientFactory` objektets `getContext` som returnerar en `Context` -objekt.

   Anropa sedan `Context` objektets `initPrincipal` och skicka `AuthResult`.

**Se även**

[Synkronisera användare programmatiskt](users.md#programmatically-synchronizing-users)

[Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)
