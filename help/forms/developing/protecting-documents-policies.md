---
title: Skydda dokument med regler
description: Använd dokumentsäkerhetstjänsten för att dynamiskt tillämpa sekretessinställningar på Adobe PDF-dokument och behålla kontrollen över dokumenten. Med dokumentsäkerhetstjänsten kan man också styra hur mottagarna använder det profilskyddade PDF-dokumentet.
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: ff42579e-6aaf-433d-8b5d-9e9dd0957250
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '15469'
ht-degree: 0%

---

# Skydda dokument med regler {#protecting-documents-with-policies}

**Exempel och exempel i det här dokumentet är bara för AEM Forms i JEE-miljö.**

**Om Document Security Service**

Med Document Security kan man dynamiskt lägga in sekretessinställningar i Adobe PDF-dokument och styra dokumenten, oavsett hur de distribueras.

Dokumentsäkerhetstjänsten förhindrar att information sprids utanför användarens räckhåll genom att användarna kan behålla kontrollen över hur mottagarna använder det profilskyddade PDF-dokumentet. Användaren kan ange vem som får öppna ett dokument, begränsa hur det får användas och övervaka dokumentet när det har distribuerats. En användare kan också dynamiskt styra åtkomsten till ett policyskyddat dokument och kan till och med dynamiskt återkalla åtkomsten till dokumentet.

Dokumentsäkerhetstjänsten skyddar även andra filtyper, till exempel Microsoft Word-filer (DOC-filer). Du kan använda API:t för dokumentsäkerhetsklienten för att arbeta med dessa filtyper. Följande versioner stöds:

* Microsoft Office 2003-filer (DOC-, XLS-, PPT-filer)
* Microsoft Office 2007-filer (DOCX-, XLSX-, PPTX-filer)
* PTC Pro/E-filer

Följande två avsnitt beskriver tydligt hur du arbetar med Word-dokument:

* [Tillämpa profiler på Word-dokument](protecting-documents-policies.md#applying-policies-to-word-documents)
* [Ta bort profiler från Word-dokument](protecting-documents-policies.md#removing-policies-from-word-documents)

Du kan utföra följande uppgifter med tjänsten Dokumentsäkerhet:

* Skapa profiler. Mer information finns i [Skapa profiler](protecting-documents-policies.md#creating-policies).
* Ändra profiler. Mer information finns i [Ändra principer](protecting-documents-policies.md#modifying-policies).
* Ta bort profiler. Mer information finns i [Ta bort profiler](protecting-documents-policies.md#deleting-policies).
* Använd profiler på PDF-dokument. Mer information finns i [Tillämpa principer på PDF-dokument](protecting-documents-policies.md#applying-policies-to-pdf-documents).
* Ta bort profiler från PDF-dokument. Mer information finns i [Ta bort profiler från PDF-dokument](protecting-documents-policies.md#removing-policies-from-pdf-documents).
* Inspect policyskyddade dokument. Mer information finns i [Inspektera skyddat PDF-dokument](protecting-documents-policies.md#inspecting-policy-protected-pdf-documents).
* Återkalla åtkomst till PDF-dokument. Mer information finns i [Återkalla åtkomst till dokument](protecting-documents-policies.md#revoking-access-to-documents).
* Återskapa åtkomst till återkallade dokument. Mer information finns i [Återställa åtkomst till återkallade dokument](protecting-documents-policies.md#reinstating-access-to-revoked-documents).
* Skapa vattenstämplar. Mer information finns i [Skapa vattenstämplar](protecting-documents-policies.md#creating-watermarks).
* Sök efter händelser. Mer information finns i [Söka efter händelser](protecting-documents-policies.md#searching-for-events).

>[!NOTE]
>
>Mer information om tjänsten Dokumentsäkerhet finns i [Tjänstreferens för AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Skapa profiler {#creating-policies}

Du kan skapa profiler programmatiskt med Java API:t för dokumentsäkerhet eller webbtjänstAPI:t. A *policy* är en samling information som innehåller dokumentskyddsinställningar, behöriga användare och användarrättigheter. Du kan skapa och spara valfritt antal profiler med hjälp av skyddsinställningar som passar olika situationer och användare.

Med hjälp av profiler kan du utföra följande uppgifter:

* Ange vilka personer som kan öppna dokumentet. Mottagarna kan antingen tillhöra eller vara externa till din organisation.
* Ange hur mottagarna kan använda dokumentet. Du kan begränsa åtkomsten till olika funktioner i Acrobat och Adobe Reader. Bland dessa funktioner finns möjligheten att skriva ut och kopiera text, lägga till signaturer och lägga till kommentarer i ett dokument.
* Ändra inställningar för åtkomst och säkerhet när som helst, även efter att du distribuerat det profilskyddade dokumentet.
* Övervaka hur dokumentet används när du har distribuerat det. Du kan se hur dokumentet används och vem som använder det. Du kan till exempel ta reda på när någon har öppnat dokumentet.

### Skapa en profil med hjälp av webbtjänster {#creating-a-policy-using-web-services}

När du skapar en profil med webbtjänstens API ska du referera till en befintlig PDF-fil (Portable Document Rights Language) som beskriver principen. Principbehörigheter och huvudobjekt definieras i PDRL-dokumentet. Följande XML-dokument är ett exempel på ett PDRL-dokument.

```xml
 <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
 <Policy PolicyInstanceVersion="1" PolicyID="5DA3F847-DE76-F9CC-63EA-49A8D59154DE" PolicyCreationTime="2004-08-30T00:02:28.294+00:00" PolicyType="1" PolicySchemaVersion="1.0" PolicyName="SDK Test Policy -4344050357301573237" PolicyDescription="An SDK Test policy" xmlns="https://www.adobe.com/schema/1.0/pdrl">
       <PolicyEntry>
          <ns1:Permission PermissionName="com.adobe.aps.onlineOpen" Access="ALLOW" xmlns:ns1="https://www.adobe.com/schema/1.0/pdrl" xmlns="https://www.adobe.com/schema/1.0/pdrl-ex" />
 
          <ns2:Permission PermissionName="com.adobe.aps.offlineOpen" Access="ALLOW" xmlns:ns2="https://www.adobe.com/schema/1.0/pdrl" xmlns="https://www.adobe.com/schema/1.0/pdrl-ex" />
 
          <ns3:Permission PermissionName="com.adobe.aps.pdf.editNotes" Access="ALLOW" xmlns:ns3="https://www.adobe.com/schema/1.0/pdrl" xmlns="https://www.adobe.com/schema/1.0/pdrl-ex" />
 
          <ns4:Permission PermissionName="com.adobe.aps.pdf.fillAndSign" Access="ALLOW" xmlns:ns4="https://www.adobe.com/schema/1.0/pdrl" xmlns="https://www.adobe.com/schema/1.0/pdrl-ex" />
          <Principal PrincipalNameType="SYSTEM">
             <PrincipalDomain>EDC_SPECIAL</PrincipalDomain>
 
             <PrincipalName>all_internal_users</PrincipalName>
          </Principal>
       </PolicyEntry>
       <PolicyEntry>
          <ns5:Permission PermissionName="com.adobe.aps.onlineOpen" Access="ALLOW" xmlns:ns5="https://www.adobe.com/schema/1.0/pdrl" xmlns="https://www.adobe.com/schema/1.0/pdrl-ex" />
 
          <ns6:Permission PermissionName="com.adobe.aps.offlineOpen" Access="ALLOW" xmlns:ns6="https://www.adobe.com/schema/1.0/pdrl" xmlns="https://www.adobe.com/schema/1.0/pdrl-ex" />
 
          <ns7:Permission PermissionName="com.adobe.aps.pdf.copy" Access="ALLOW" xmlns:ns7="https://www.adobe.com/schema/1.0/pdrl" xmlns="https://www.adobe.com/schema/1.0/pdrl-ex" />
 
          <ns8:Permission PermissionName="com.adobe.aps.pdf.printLow" Access="ALLOW" xmlns="https://www.adobe.com/schema/1.0/pdrl-ex" xmlns:ns8="https://www.adobe.com/schema/1.0/pdrl" />
 
          <ns9:Permission PermissionName="com.adobe.aps.policySwitch" Access="ALLOW" xmlns:ns9="https://www.adobe.com/schema/1.0/pdrl" xmlns="https://www.adobe.com/schema/1.0/pdrl-ex" />
 
          <ns10:Permission PermissionName="com.adobe.aps.revoke" Access="ALLOW" xmlns="https://www.adobe.com/schema/1.0/pdrl-ex" xmlns:ns10="https://www.adobe.com/schema/1.0/pdrl" />
 
          <ns11:Permission PermissionName="com.adobe.aps.pdf.edit" Access="ALLOW" xmlns:ns11="https://www.adobe.com/schema/1.0/pdrl" xmlns="https://www.adobe.com/schema/1.0/pdrl-ex" />
 
          <ns12:Permission PermissionName="com.adobe.aps.pdf.editNotes" Access="ALLOW" xmlns:ns12="https://www.adobe.com/schema/1.0/pdrl" xmlns="https://www.adobe.com/schema/1.0/pdrl-ex" />
 
          <ns13:Permission PermissionName="com.adobe.aps.pdf.fillAndSign" Access="ALLOW" xmlns:ns13="https://www.adobe.com/schema/1.0/pdrl" xmlns="https://www.adobe.com/schema/1.0/pdrl-ex" />
 
          <ns14:Permission PermissionName="com.adobe.aps.pdf.printHigh" Access="ALLOW" xmlns:ns14="https://www.adobe.com/schema/1.0/pdrl" xmlns="https://www.adobe.com/schema/1.0/pdrl-ex" />
 
          <Principal PrincipalNameType="SYSTEM">
             <PrincipalDomain>EDC_SPECIAL</PrincipalDomain>
 
             <PrincipalName>publisher</PrincipalName>
          </Principal>
       </PolicyEntry>
 
       <OfflineLeasePeriod>
          <Duration>P31D</Duration>
       </OfflineLeasePeriod>
 
       <AuditSettings isTracked="true" />
 
       <PolicyValidityPeriod isAbsoluteTime="false">
          <ValidityPeriodRelative>
             <NotBeforeRelative>PT0S</NotBeforeRelative>
 
             <NotAfterRelative>P20D</NotAfterRelative>
          </ValidityPeriodRelative>
       </PolicyValidityPeriod>
 </Policy>
 
```

>[!NOTE]
>
>Mer information om tjänsten Dokumentsäkerhet finns i [Tjänstreferens för AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Sammanfattning av steg {#summary-of-steps}

Så här skapar du en profil:

1. Inkludera projektfiler.
1. Skapa ett API-objekt för Document Security Client.
1. Ange principens attribut.
1. Skapa en princippost.
1. Registrera policyn.

**Inkludera projektfiler**

Inkludera nödvändiga filer i utvecklingsprojektet. Om du skapar ett klientprogram med Java inkluderar du de JAR-filer som behövs. Om du använder webbtjänster måste du inkludera proxyfilerna.

Följande JAR-filer måste läggas till i projektets klassökväg:

* adobe-rightsmanagement-client.jar
* namespace.jar (om AEM Forms distribueras på JBoss)
* jaxb-api.jar (om AEM Forms används på JBoss)
* jaxb-impl.jar (om AEM Forms används på JBoss)
* jaxb-libs.jar (om AEM Forms körs på JBoss)
* jaxb-xjc.jar (om AEM Forms används på JBoss)
* relaxngDatatype.jar (om AEM Forms körs på JBoss)
* xsdlib.jar (om AEM Forms körs på JBoss)
* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar
* jbossall-client.jar (använd en annan JAR-fil om AEM Forms inte är distribuerat på JBoss)

Mer information om var dessa JAR-filer finns i [Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Skapa ett API-objekt för Document Security Client**

Skapa ett klientobjekt för tjänsten Dokumentsäkerhet innan du programmässigt utför en åtgärd.

**Ange profilens attribut**

Om du vill skapa en profil anger du principattribut. Ett obligatoriskt attribut är principnamnet. Principnamnen måste vara unika för varje principuppsättning. En policyuppsättning är bara en samling policyer. Det kan finnas två principer med samma namn om profilerna tillhör separata principuppsättningar. Två principer i en enskild principuppsättning kan dock inte ha samma principnamn.

Ett annat användbart attribut är giltighetsperioden. En giltighetsperiod är den tidsperiod under vilken ett policyskyddat dokument är tillgängligt för behöriga mottagare. Om du inte anger det här attributet är principen alltid giltig.

En giltighetsperiod kan anges till något av följande alternativ:

* Ett visst antal dagar som dokumentet är tillgängligt från den tidpunkt då dokumentet publiceras
* Ett slutdatum efter vilket dokumentet inte är tillgängligt
* Ett visst datumintervall som dokumentet är tillgängligt för
* Alltid giltig

Du kan bara ange ett startdatum, vilket resulterar i att profilen är giltig efter startdatumet. Om du bara anger ett slutdatum gäller profilen fram till slutdatumet. Ett undantag genereras emellertid om både ett startdatum och ett slutdatum inte har definierats.

När du anger attribut som tillhör en profil kan du även ange krypteringsinställningar. Dessa krypteringsinställningar påverkar när profilen tillämpas på ett dokument. Du kan ange följande krypteringsvärden:

* **AES256**: Representerar AES-krypteringsalgoritmen med en 256-bitars nyckel.
* **AES128**: Representerar AES-krypteringsalgoritmen med en 128-bitars nyckel.
* **Ingen kryptering:** Representerar ingen kryptering.

När du anger `NoEncryption` kan du inte ange `PlaintextMetadata` alternativ till `false`. Om du försöker göra det genereras ett undantag.

>[!NOTE]
>
>Mer information om andra attribut som du kan ange finns i `Policy` gränssnittsbeskrivning i [AEM Forms API-referens](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**Skapa en princippost**

En princippost kopplar principer, som är grupper och användare, och behörigheter till en princip. En princip måste ha minst en princippost. Anta till exempel att du utför följande uppgifter:

* Skapa och registrera en princippost som gör det möjligt för en grupp att endast visa ett dokument online och förhindrar mottagarna från att kopiera det.
* Koppla principposten till profilen.
* Skydda ett dokument med profilen med Acrobat.

Dessa åtgärder gör att mottagarna bara kan visa dokumentet online och inte kan kopiera det. Dokumentet förblir säkert tills du har tagit bort skyddet från det.

**Registrera policyn**

En ny princip måste registreras innan den kan användas. När du har registrerat en profil kan du använda den för att skydda dokument.

### Skapa en profil med Java API {#create-a-policy-using-the-java-api}

Skapa en profil med hjälp av API:t för dokumentsäkerhet (Java):

1. Inkludera projektfiler.

   Inkludera JAR-klientfiler, som adobe-rightsmanagement-client.jar, i Java-projektets klassökväg.

1. Skapa ett API-objekt för Document Security Client.

   * Skapa en `ServiceClientFactory` objekt som innehåller anslutningsegenskaper.
   * Skapa en `DocumentSecurityClient` genom att använda konstruktorn och skicka `ServiceClientFactory` -objekt.

1. Ange principens attribut.

   * Skapa en `Policy` genom att anropa `InfomodelObjectFactory` objektets statiska `createPolicy` -metod. Den här metoden returnerar en `Policy` -objekt.
   * Ange principens namnattribut genom att anropa `Policy` objektets `setName` och skickar ett strängvärde som anger principnamnet.
   * Ange profilens beskrivning genom att anropa `Policy` objektets `setDescription` och skickar ett strängvärde som anger principens beskrivning.
   * Ange den principuppsättning som den nya principen tillhör genom att anropa `Policy` objektets `setPolicySetName` och skickar ett strängvärde som anger namnet på principuppsättningen. (Du kan ange `null` för det här parametervärdet som resulterar i att principen läggs till i *Mina policyer* principuppsättning.)
   * Skapa policyns giltighetsperiod genom att anropa `InfomodelObjectFactory` objektets statiska `createValidityPeriod` -metod. Den här metoden returnerar en `ValidityPeriod` -objekt.
   * Ange antalet dagar som ett profilskyddat dokument är tillgängligt genom att anropa `ValidityPeriod` objektets `setRelativeExpirationDays` och skickar ett heltalsvärde som anger antalet dagar.
   * Ange policyns giltighetsperiod genom att anropa `Policy` objektets `setValidityPeriod` metoden och skicka `ValidityPeriod` -objekt.

1. Skapa en princippost.

   * Skapa en policypost genom att anropa `InfomodelObjectFactory` objektets statiska `createPolicyEntry` -metod. Den här metoden returnerar en `PolicyEntry` -objekt.
   * Ange principens behörigheter genom att anropa `InfomodelObjectFactory` objektets statiska `createPermission` -metod. Skicka en statisk datamedlem som tillhör `Permission` -gränssnitt som representerar behörigheten. Den här metoden returnerar en `Permission` -objekt. Om du till exempel vill lägga till en behörighet som gör att användare kan kopiera data från ett principskyddat PDF-dokument, skickar du `Permission.COPY`. (Upprepa det här steget för varje behörighet att lägga till).
   * Lägg till behörigheten till principposten genom att anropa `PolicyEntry` objektets `addPermission` metoden och skicka `Permission` -objekt. (Upprepa det här steget för varje `Permission` objekt som du har skapat).
   * Skapa principobjektet genom att anropa `InfomodelObjectFactory` objektets statiska `createSpecialPrincipal` -metod. Skicka en datamedlem som tillhör `InfomodelObjectFactory` objekt som representerar huvudobjektet. Den här metoden returnerar en `Principal` -objekt. Om du till exempel vill lägga till dokumentets utgivare som huvudnamn skickar du `InfomodelObjectFactory.PUBLISHER_PRINCIPAL`.
   * Lägg till huvudkontot i principposten genom att anropa `PolicyEntry` objektets `setPrincipal`metoden och skicka `Principal` -objekt.
   * Lägg till principposten i principen genom att anropa `Policy` objektets `addPolicyEntry` metoden och skicka `PolicyEntry` -objekt.

1. Registrera policyn.

   * Skapa en `PolicyManager` genom att anropa `DocumentSecurityClient` objektets `getPolicyManager` -metod.
   * Registrera policyn genom att anropa `PolicyManager` objektets `registerPolicy` och skicka följande värden:

      * The `Policy` objekt som representerar principen som ska registreras.

   * Ett strängvärde som representerar den principuppsättning som principen tillhör.

   Om du använder ett AEM administratörskonto i anslutningsinställningarna för att skapa `DocumentSecurityClient` anger du sedan namnet på principuppsättningen när du anropar `registerPolicy` -metod. Om du får en `null` värdet för principuppsättningen. Principen skapas i administratörerna *Mina policyer* principuppsättning.

   Om du använder en dokumentsäkerhetsanvändare i anslutningsinställningarna kan du anropa den överlagrade `registerPolicy` metod som bara accepterar principen. Du behöver alltså inte ange namnet på principuppsättningen. Principen läggs dock till i principuppsättningen med namnet *Mina policyer*. Om du inte vill lägga till den nya principen i den här principinställningen anger du ett principuppsättningsnamn när du anropar den `registerPolicy` -metod.

   >[!NOTE]
   >
   >Referera till en befintlig principuppsättning när du skapar en profil. Om du anger en principuppsättning som inte finns genereras ett undantag.

Följande kodexempel innehåller information om hur du använder Document Security-tjänsten:

* &quot;Snabbstart (SOAP-läge): Skapa en profil med Java API&quot;

### Skapa en profil med webbtjänstens API {#create-a-policy-using-the-web-service-api}

Skapa en profil med hjälp av API:t för dokumentsäkerhet (webbtjänsten):

1. Inkludera projektfiler.

   Skapa ett Microsoft .NET-projekt som använder MTOM. Kontrollera att du använder följande WSDL-definition: `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Ersätt `localhost` med IP-adressen till den server där AEM Forms finns.

1. Skapa ett API-objekt för Document Security Client.

   * Skapa en `DocumentSecurityServiceClient` genom att använda dess standardkonstruktor.
   * Skapa en `DocumentSecurityServiceClient.Endpoint.Address` genom att använda `System.ServiceModel.EndpointAddress` konstruktor. Skicka ett strängvärde som anger WSDL till AEM Forms-tjänsten (till exempel `http://localhost:8080/soap/services/RightsManagementService?WSDL`.) Du behöver inte använda `lc_version` -attribut. Detta attribut används när du skapar en tjänstreferens.)
   * Skapa en `System.ServiceModel.BasicHttpBinding` genom att hämta värdet för `RightsManagementServiceClient.Endpoint.Binding` fält. Skicka returvärdet till `BasicHttpBinding`.
   * Ange `System.ServiceModel.BasicHttpBinding` objektets `MessageEncoding` fält till `WSMessageEncoding.Mtom`. Detta värde garanterar att MTOM används.
   * Aktivera grundläggande HTTP-autentisering genom att utföra följande åtgärder:

      * Tilldela AEM formuläranvändarnamn till fältet `RightsManagementServiceClient.ClientCredentials.UserName.UserName`.
      * Tilldela motsvarande lösenordsvärde till fältet `RightsManagementServiceClient.ClientCredentials.UserName.Password`.
      * Tilldela konstantvärdet `HttpClientCredentialType.Basic` till fältet `BasicHttpBindingSecurity.Transport.ClientCredentialType`.

   * Tilldela konstantvärdet `BasicHttpSecurityMode.TransportCredentialOnly` till fältet `BasicHttpBindingSecurity.Security.Mode`.

1. Ange principens attribut.

   * Skapa en `PolicySpec` genom att använda dess konstruktor.
   * Ange principens namn genom att tilldela ett strängvärde till `PolicySpec` objektets `name` datamedlem.
   * Ange principens beskrivning genom att tilldela ett strängvärde till `PolicySpec` objektets `description` datamedlem.
   * Ange den principuppsättning som principen tillhör genom att tilldela ett strängvärde till `PolicySpec` objektets `policySetName` datamedlem. Ange ett befintligt principuppsättningsnamn. (Du kan ange `null` för det här parametervärdet som resulterar i att principen läggs till i *Mina policyer*.)
   * Ange principens låneperiod offline genom att tilldela ett heltalsvärde till `PolicySpec` objektets `offlineLeasePeriod` datamedlem.
   * Ange `PolicySpec` objektets `policyXml` datamedlem med ett strängvärde som representerar PDRL XML-data. Skapa en .NET-fil om du vill utföra den här åtgärden `StreamReader` genom att använda dess konstruktor. Skicka platsen för en PDRL XML-fil som representerar principen till `StreamReader` konstruktor. Anropa `StreamReader` objektets `ReadLine` och tilldela returvärdet till en strängvariabel. Iterera genom `StreamReader` objektet tills `ReadLine` returnerar null. Tilldela strängvariabeln till `PolicySpec` objektets `policyXml` datamedlem.

1. Skapa en princippost.

   Du behöver inte skapa en princippost när du skapar en profil med webbtjänstens API för dokumentsäkerhet. Posten för profilen definieras i PDRL-dokumentet.

1. Registrera policyn.

   Registrera policyn genom att anropa `DocumentSecurityServiceClient` objektets `registerPolicy` och skicka följande värden:

   * The `PolicySpec` objekt som representerar principen som ska registreras.
   * Ett strängvärde som representerar den principuppsättning som principen tillhör. Du kan ange en `null` vilket resulterar i att profilen läggs till i *MinaPolices* principuppsättning.

   Om du använder ett AEM administratörskonto i anslutningsinställningarna för att skapa `DocumentSecurityClient` anger du namnet på principuppsättningen när du anropar `registerPolicy` -metod.

   Om du använder en Document SecurityDocument Security-användare i anslutningsinställningarna kan du anropa den överlagrade `registerPolicy` metod som bara accepterar principen. Du behöver alltså inte ange namnet på principuppsättningen. Principen läggs dock till i principuppsättningen med namnet *Mina policyer*. Om du inte vill lägga till den nya principen i den här principinställningen anger du ett principuppsättningsnamn när du anropar den `registerPolicy` -metod.

   >[!NOTE]
   >
   >När du skapar en profil och anger en principuppsättning måste du ange en befintlig principuppsättning. Om du anger en principuppsättning som inte finns genereras ett undantag.

Följande snabbstarter innehåller kodexempel på hur du använder dokumentsäkerhetstjänsten:

* &quot;Snabbstart (MTOM): Skapa en princip med hjälp av webbtjänstens API&quot;
* &quot;Snabbstart (SwaRef): Skapa en princip med hjälp av webbtjänstens API&quot;

## Ändra principer {#modifying-policies}

Du kan ändra en befintlig profil med Java API:t för dokumentsäkerhet eller webbtjänstens API. Om du vill ändra en befintlig princip hämtar du den, ändrar den och uppdaterar sedan principen på servern. Anta till exempel att du hämtar en befintlig princip och förlänger dess giltighetsperiod. Du måste uppdatera profilen innan ändringen börjar gälla.

Du kan ändra en profil när affärskraven ändras och profilen inte längre speglar dessa krav. I stället för att skapa en profil kan du helt enkelt uppdatera en befintlig profil.

Om du vill ändra principattribut med en webbtjänst (till exempel med Java-proxyklasser som har skapats med JAX-WS) måste du se till att profilen har registrerats med dokumentsäkerhetstjänsten. Du kan sedan referera till den befintliga profilen med `PolicySpec.getPolicyXml` och ändra principattributen med hjälp av tillämpliga metoder. Du kan till exempel ändra offlineleasingperioden genom att anropa `PolicySpec.setOfflineLeasePeriod` -metod.

>[!NOTE]
>
>Mer information om tjänsten Dokumentsäkerhet finns i [Tjänstreferens för AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Sammanfattning av steg {#summary_of_steps-1}

Så här ändrar du en befintlig princip:

1. Inkludera projektfiler.
1. Skapa ett API-objekt för Document Security Client.
1. Hämta en befintlig princip.
1. Ändra profilattribut.
1. Uppdatera profilen.

**Inkludera projektfiler**

Inkludera nödvändiga filer i utvecklingsprojektet. Om du skapar ett klientprogram med Java inkluderar du de JAR-filer som behövs. Om du använder webbtjänster måste du inkludera proxyfilerna.

**Skapa ett API-objekt för Document Security Client**

Innan du programmässigt kan utföra en Document Security-tjänståtgärd måste du skapa ett klientobjekt för Document Security-tjänsten. Om du använder Java API skapar du en `RightsManagementClient` -objekt. Om du använder webbtjänstens API för dokumentsäkerhet skapar du en `RightsManagementServiceService` -objekt.

**Hämta en befintlig princip**

Hämta en befintlig princip om du vill ändra den. Om du vill hämta en princip anger du principnamnet och den principuppsättning som principen tillhör. Om du anger en `null` värdet för principuppsättningsnamnet hämtas principen från *Mina policyer* principuppsättning.

**Ange profilens attribut**

Om du vill ändra en profil ändrar du värdet för principattributen. Det enda principattribut som du inte kan ändra är namnattributet. Om du till exempel vill ändra principens låneperiod offline kan du ändra värdet på principens attribut för låneperiod offline.

När du ändrar en princips låneperiod offline med hjälp av en webbtjänst är `offlineLeasePeriod` fält på `PolicySpec` -gränssnittet ignoreras. Om du vill uppdatera offlinelåneperioden ändrar du `OfflineLeasePeriod` i PDRL XML-dokumentet. Referera sedan till det uppdaterade PDRL XML-dokumentet med hjälp av `PolicySpec` gränssnitt `policyXML` datamedlem.

>[!NOTE]
>
>Mer information om andra attribut som du kan ange finns i `Policy` gränssnittsbeskrivning i [AEM Forms API-referens](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**Uppdatera profilen**

Innan de ändringar du gör i en profil börjar gälla måste du uppdatera den med tjänsten Dokumentsäkerhet. Ändringar i profiler som skyddar dokument uppdateras nästa gång det profilskyddade dokumentet synkroniseras med dokumentsäkerhetstjänsten.

### Ändra befintliga profiler med Java API {#modify-existing-policies-using-the-java-api}

Ändra en befintlig profil med hjälp av dokumentsäkerhets-API (Java):

1. Inkludera projektfiler.

   Inkludera JAR-klientfiler, som adobe-rightsmanagement-client.jar, i Java-projektets klassökväg.

1. Skapa ett API-objekt för Document Security Client.

   * Skapa en `ServiceClientFactory` objekt som innehåller anslutningsegenskaper.
   * Skapa en `RightsManagementClient` genom att använda konstruktorn och skicka `ServiceClientFactory` -objekt.

1. Hämta en befintlig princip.

   * Skapa en `PolicyManager` genom att anropa `RightsManagementClient` objektets `getPolicyManager` -metod.
   * Skapa en `Policy` objekt som representerar principen som ska uppdateras genom att anropa `PolicyManager` objektets `getPolicy` och skicka följande värden&quot;

      * Ett strängvärde som representerar namnet på den principuppsättning som principen tillhör. Du kan ange `null` som resulterar i `MyPolicies` principuppsättning används.
      * Ett strängvärde som representerar principnamnet.

1. Ange principens attribut.

   Ändra regelns attribut så att de uppfyller företagets krav. Om du till exempel vill ändra principens låneperiod offline anropar du `Policy` objektets `setOfflineLeasePeriod` -metod.

1. Uppdatera profilen.

   Uppdatera profilen genom att anropa `PolicyManager` objektets `updatePolicy` -metod. Skicka `Policy` objekt som representerar principen som ska uppdateras.

**Exempel på koder**

Exempel på kod som använder dokumentsäkerhetstjänsten finns i Snabbstart (SOAP-läge): Ändra en profil med hjälp av Java API-avsnittet.

### Ändra befintliga profiler med webbtjänstens API {#modify-existing-policies-using-the-web-service-api}

Ändra en befintlig profil med hjälp av API:t för dokumentsäkerhet (webbtjänsten):

1. Inkludera projektfiler.

   Skapa ett Microsoft .NET-projekt som använder MTOM. Kontrollera att du använder följande WSDL-definition: `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Ersätt `localhost` med IP-adressen till den server där AEM Forms finns.

1. Skapa ett API-objekt för Document Security Client.

   * Skapa en `RightsManagementServiceClient` genom att använda dess standardkonstruktor.
   * Skapa en `RightsManagementServiceClient.Endpoint.Address` genom att använda `System.ServiceModel.EndpointAddress` konstruktor. Skicka ett strängvärde som anger WSDL till AEM Forms-tjänsten (till exempel `http://localhost:8080/soap/services/RightsManagementService?WSDL`.) Du behöver inte använda `lc_version` -attribut. Detta attribut används när du skapar en tjänstreferens.)
   * Skapa en `System.ServiceModel.BasicHttpBinding` genom att hämta värdet för `RightsManagementServiceClient.Endpoint.Binding` fält. Skicka returvärdet till `BasicHttpBinding`.
   * Ange `System.ServiceModel.BasicHttpBinding` objektets `MessageEncoding` fält till `WSMessageEncoding.Mtom`. Detta värde garanterar att MTOM används.
   * Aktivera grundläggande HTTP-autentisering genom att utföra följande åtgärder:

      * Tilldela AEM formuläranvändarnamn till fältet `RightsManagementServiceClient.ClientCredentials.UserName.UserName`.
      * Tilldela motsvarande lösenordsvärde till fältet `RightsManagementServiceClient.ClientCredentials.UserName.Password`.
      * Tilldela konstantvärdet `HttpClientCredentialType.Basic` till fältet `BasicHttpBindingSecurity.Transport.ClientCredentialType`.

   * Tilldela konstantvärdet `BasicHttpSecurityMode.TransportCredentialOnly` till fältet `BasicHttpBindingSecurity.Security.Mode`.

1. Hämta en befintlig princip.

   Skapa en `PolicySpec` objekt som representerar principen som ska ändras genom att anropa `RightsManagementServiceClient` objektets `getPolicy` och skicka följande värden:

   * Ett strängvärde som anger namnet på den principuppsättning som principen tillhör. Du kan ange `null` som resulterar i `MyPolicies` principuppsättning används.
   * Ett strängvärde som anger principens namn.

1. Ange principens attribut.

   Ändra regelns attribut så att de uppfyller företagets krav.

1. Uppdatera profilen.

   Uppdatera profilen genom att anropa `RightsManagementServiceClient` objektets `updatePolicyFromSDK` metoden och skicka `PolicySpec` objekt som representerar principen som ska uppdateras.

**Exempel på koder**

Följande snabbstarter innehåller kodexempel på hur du använder dokumentsäkerhetstjänsten:

* &quot;Snabbstart (MTOM): Ändra en princip med hjälp av webbtjänstens API&quot;
* &quot;Snabbstart (SwaRef): Ändra en princip med hjälp av webbtjänstens API&quot;

## Ta bort profiler {#deleting-policies}

Du kan ta bort en befintlig princip med Java API:t för dokumentsäkerhet eller webbtjänstens API. När en profil har tagits bort kan den inte längre användas för att skydda dokument. Befintliga principskyddade dokument som använder profilen är dock fortfarande skyddade. Du kan ta bort en profil när en nyare blir tillgänglig.

>[!NOTE]
>
>Mer information om tjänsten Dokumentsäkerhet finns i [Tjänstreferens för AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Sammanfattning av steg {#summary_of_steps-2}

Så här tar du bort en befintlig princip:

1. Inkludera projektfiler
1. Skapa ett API-objekt för Document Security Client.
1. Ta bort profilen.

**Inkludera projektfiler**

Inkludera nödvändiga filer i utvecklingsprojektet. Om du skapar ett klientprogram med Java inkluderar du de JAR-filer som behövs. Om du använder webbtjänster måste du inkludera proxyfilerna.

**Skapa ett API-objekt för Document Security Client**

Innan du programmässigt kan utföra en dokumentsäkerhetstjänståtgärd måste du skapa ett klientobjekt för dokumentsäkerhetstjänsten. Om du använder Java API skapar du en `RightsManagementClient` -objekt. Om du använder webbtjänstens API för dokumentsäkerhet skapar du en `RightsManagementServiceService` -objekt.

**Ta bort profilen**

Om du vill ta bort en profil anger du vilken princip som ska tas bort och vilken principuppsättning som principen tillhör. Den användare vars inställningar används för att anropa AEM Forms måste ha behörighet att ta bort profilen, annars inträffar ett undantag. Om du försöker ta bort en princip som inte finns inträffar ett undantag.

### Ta bort profiler med Java API {#delete-policies-using-the-java-api}

Ta bort en profil med hjälp av dokumentsäkerhets-API (Java):

1. Inkludera projektfiler.

   Inkludera JAR-klientfiler, som adobe-rightsmanagement-client.jar, i Java-projektets klassökväg.

1. Skapa ett API-objekt för Document Security Client.

   * Skapa en `ServiceClientFactory` objekt som innehåller anslutningsegenskaper.
   * Skapa en `RightsManagementClient` genom att använda konstruktorn och skicka `ServiceClientFactory` -objekt.

1. Ta bort profilen.

   * Skapa en `PolicyManager` genom att anropa `RightsManagementClient` objektets `getPolicyManager` -metod.
   * Ta bort profilen genom att anropa `PolicyManager` objektets `deletePolicy` och skicka följande värden:

      * Ett strängvärde som anger namnet på den principuppsättning som principen tillhör. Du kan ange `null` som resulterar i `MyPolicies` principuppsättning används.
      * Ett strängvärde som anger namnet på principen som ska tas bort.

**Exempel på koder**

Följande snabbstarter innehåller kodexempel på hur du använder dokumentsäkerhetstjänsten:

* &quot;Snabbstart (SOAP-läge): Ta bort en princip med Java API&quot;

### Ta bort profiler med webbtjänstens API {#delete-policies-using-the-web-service-api}

Ta bort en profil med hjälp av API:t för dokumentsäkerhet (webbtjänsten):

1. Inkludera projektfiler.

   Skapa ett Microsoft .NET-projekt som använder MTOM. Kontrollera att du använder följande WSDL-definition: `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Ersätt `localhost` med IP-adressen till den server där AEM Forms finns.

1. Skapa ett API-objekt för Document Security Client.

   * Skapa en `RightsManagementServiceClient` genom att använda dess standardkonstruktor.
   * Skapa en `RightsManagementServiceClient.Endpoint.Address` genom att använda `System.ServiceModel.EndpointAddress` konstruktor. Skicka ett strängvärde som anger WSDL till AEM Forms-tjänsten (till exempel `http://localhost:8080/soap/services/RightsManagementService?WSDL`.) Du behöver inte använda `lc_version` -attribut. Detta attribut används när du skapar en tjänstreferens.)
   * Skapa en `System.ServiceModel.BasicHttpBinding` genom att hämta värdet för `RightsManagementServiceClient.Endpoint.Binding` fält. Skicka returvärdet till `BasicHttpBinding`.
   * Ange `System.ServiceModel.BasicHttpBinding` objektets `MessageEncoding` fält till `WSMessageEncoding.Mtom`. Detta värde garanterar att MTOM används.
   * Aktivera grundläggande HTTP-autentisering genom att utföra följande åtgärder:

      * Tilldela AEM formuläranvändarnamn till fältet `RightsManagementServiceClient.ClientCredentials.UserName.UserName`.
      * Tilldela motsvarande lösenordsvärde till fältet `RightsManagementServiceClient.ClientCredentials.UserName.Password`.
      * Tilldela konstantvärdet `HttpClientCredentialType.Basic` till fältet `BasicHttpBindingSecurity.Transport.ClientCredentialType`.

   * Tilldela konstantvärdet `BasicHttpSecurityMode.TransportCredentialOnly` till fältet `BasicHttpBindingSecurity.Security.Mode`.

1. Ta bort profilen.

   Ta bort en profil genom att anropa `RightsManagementServiceClient` objektets `deletePolicy` och skicka följande värden:

   * Ett strängvärde som anger namnet på den principuppsättning som principen tillhör. Du kan ange `null` som resulterar i `MyPolicies` principuppsättning används.
   * Ett strängvärde som anger namnet på principen som ska tas bort.

**Exempel på koder**

Följande snabbstarter innehåller kodexempel på hur du använder dokumentsäkerhetstjänsten:

* &quot;Snabbstart (MTOM): Ta bort en princip med hjälp av webbtjänstens API&quot;
* &quot;Snabbstart (SwaRef): Ta bort en princip med webbtjänstens API&quot;

## Tillämpa principer på PDF-dokument {#applying-policies-to-pdf-documents}

Du kan tillämpa en profil på ett PDF-dokument för att skydda dokumentet. Genom att tillämpa en profil på ett PDF-dokument begränsar du åtkomsten till dokumentet. Du kan inte tillämpa en profil på ett dokument om dokumentet redan är skyddat med en profil.

Medan dokumentet är öppet kan du även begränsa åtkomsten till Acrobat- och Adobe Reader-funktioner, inklusive möjligheten att skriva ut och kopiera text, göra ändringar samt lägga till signaturer och kommentarer i ett dokument. Dessutom kan du återkalla ett profilskyddat PDF-dokument när du inte längre vill att användarna ska få åtkomst till dokumentet.

Du kan övervaka användningen av ett profilskyddat dokument när du har distribuerat det. Det innebär att du kan se hur dokumentet används och vem som använder det. Du kan till exempel ta reda på när någon har öppnat dokumentet.

>[!NOTE]
>
>Mer information om tjänsten Dokumentsäkerhet finns i [Tjänstreferens för AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Sammanfattning av steg {#summary_of_steps-3}

Så här använder du en profil för ett PDF-dokument:

1. Inkludera projektfiler.
1. Skapa ett API-objekt för Document Security Client.
1. Hämta ett PDF-dokument som en profil tillämpas på.
1. Använd en befintlig profil för dokumentet i PDF.
1. Spara det principskyddade PDF-dokumentet.

**Inkludera projektfiler**

Inkludera nödvändiga filer i utvecklingsprojektet. Om du skapar ett klientprogram med Java inkluderar du de JAR-filer som behövs. Om du använder webbtjänster måste du inkludera proxyfilerna.

**Skapa ett API-objekt för dokumentsäkerhetsklienten**

Skapa ett klientobjekt för tjänsten Dokumentsäkerhet innan du programmässigt utför en åtgärd. Om du använder Java API skapar du en `DocumentSecurityClient` -objekt. Om du använder webbtjänstens API för dokumentsäkerhet skapar du en `DocumentSecurityServiceService` -objekt.

**Hämta ett PDF-dokument**

Du kan hämta ett PDF-dokument för att tillämpa en profil. När du har tillämpat en profil på dokumentet i PDF begränsas användare när dokumentet används. Om profilen t.ex. inte aktiverar dokumentet för att öppnas offline måste användarna vara online för att kunna öppna dokumentet.

**Tillämpa en befintlig profil på PDF-dokumentet**

Om du vill tillämpa en profil på ett PDF-dokument refererar du till en befintlig princip och anger vilken principuppsättning som policyn tillhör. Användaren som anger anslutningsegenskaperna måste ha tillgång till den angivna principen. Annars inträffar ett undantag.

**Spara PDF-dokumentet**

När dokumentsäkerhetstjänsten har tillämpat en profil på ett PDF-dokument kan du spara det profilskyddade PDF-dokumentet som en PDF-fil.

**Se även**

[Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Återkalla åtkomst till dokument](protecting-documents-policies.md#revoking-access-to-documents)

### Tillämpa en profil på ett PDF-dokument med Java API {#apply-a-policy-to-a-pdf-document-using-the-java-api}

Tillämpa en profil på ett PDF-dokument med hjälp av dokumentets säkerhets-API (Java):

1. Inkludera projektfiler.

   Inkludera JAR-klientfiler, som adobe-rightsmanagement-client.jar, i Java-projektets klassökväg.

1. Skapa ett API-objekt för Document Security Client.

   * Skapa en `ServiceClientFactory` objekt som innehåller anslutningsegenskaper.
   * Skapa en `RightsManagementClient` genom att använda konstruktorn och skicka `ServiceClientFactory` -objekt.

1. Hämta ett PDF-dokument.

   * Skapa en `java.io.FileInputStream` objekt som representerar PDF-dokumentet med hjälp av dess konstruktor. Skicka ett strängvärde som anger platsen för PDF-dokumentet.
   * Skapa en `com.adobe.idp.Document` genom att använda konstruktorn och skicka `java.io.FileInputStream` -objekt.

1. Använd en befintlig profil för dokumentet i PDF.

   * Skapa en `DocumentManager` genom att anropa `RightsManagementClient` objektets `getDocumentManager` -metod.
   * Tillämpa en profil på PDF-dokumentet genom att anropa `DocumentManager` objektets `protectDocument` och skicka följande värden:

      * The `com.adobe.idp.Document` -objekt som innehåller det PDF-dokument som profilen tillämpas på.
      * Ett strängvärde som anger dokumentets namn.
      * Ett strängvärde som anger namnet på den principuppsättning som principen tillhör. Du kan ange en `null` det värde som resulterar i `MyPolicies` principuppsättning används.
      * Ett strängvärde som anger principnamnet.
      * Ett strängvärde som representerar namnet på användarhanterardomänen för den användare som är dokumentets utgivare. Det här parametervärdet är valfritt och kan vara null (om parametern är null måste nästa parametervärde vara null).
      * Ett strängvärde som representerar namnet på den kanoniska användaren av användarhanteraren som är dokumentets utgivare. Parametervärdet är valfritt och kan `null` (om parametern är null måste det föregående parametervärdet vara `null`).
      * A `com.adobe.livecycle.rightsmanagement.Locale` som representerar det språkområde som används för att välja MS Office-mallen. Det här parametervärdet är valfritt och används inte för PDF-dokument. Om du vill skydda ett PDF-dokument anger du `null`.

     The `protectDocument` returnerar en `RMSecureDocumentResult` objekt som innehåller det principskyddade PDF-dokumentet.

1. Spara dokumentet PDF.

   * Anropa `RMSecureDocumentResult` objektets `getProtectedDoc` metod för att hämta det principskyddade PDF-dokumentet. Den här metoden returnerar en `com.adobe.idp.Document` -objekt.
   * Skapa en `java.io.File` och se till att filtillägget är PDF.
   * Anropa `com.adobe.idp.Document` objektets `copyToFile` metod för att kopiera innehållet i `Document` till filen (se till att du använder `Document` objekt som returneras av `getProtectedDoc` metod).

**Exempel på koder**

Följande snabbstarter innehåller kodexempel på hur du använder dokumentsäkerhetstjänsten:

* &quot;Snabbstart (EJB-läge): Tillämpa en princip på ett PDF-dokument med Java API&quot;
* &quot;Snabbstart (SOAP-läge): Tillämpa en princip på ett PDF-dokument med Java API&quot;

**Se även**

[Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Tillämpa en profil på ett PDF-dokument med hjälp av webbtjänstens API {#apply-a-policy-to-a-pdf-document-using-the-web-service-api}

Tillämpa en profil på ett PDF-dokument med hjälp av API:t för dokumentsäkerhet (webbtjänsten):

1. Inkludera projektfiler.

   Skapa ett Microsoft .NET-projekt som använder MTOM. Kontrollera att du använder följande WSDL-definition: `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Ersätt `localhost` med IP-adressen till den server där AEM Forms finns.

1. Skapa ett API-objekt för Document Security Client.

   * Skapa en `RightsManagementServiceClient` genom att använda dess standardkonstruktor.
   * Skapa en `RightsManagementServiceClient.Endpoint.Address` genom att använda `System.ServiceModel.EndpointAddress` konstruktor. Skicka ett strängvärde som anger WSDL till Forms-tjänsten (till exempel `http://localhost:8080/soap/services/RightsManagementService?WSDL`.) Du behöver inte använda `lc_version` -attribut. Detta attribut används när du skapar en tjänstreferens.)
   * Skapa en `System.ServiceModel.BasicHttpBinding` genom att hämta värdet för `RightsManagementServiceClient.Endpoint.Binding` fält. Skicka returvärdet till `BasicHttpBinding`.
   * Ange `System.ServiceModel.BasicHttpBinding` objektets `MessageEncoding` fält till `WSMessageEncoding.Mtom`. Detta värde garanterar att MTOM används.
   * Aktivera grundläggande HTTP-autentisering genom att utföra följande åtgärder:

      * Tilldela AEM formuläranvändarnamn till fältet `RightsManagementServiceClient.ClientCredentials.UserName.UserName`.
      * Tilldela motsvarande lösenordsvärde till fältet `RightsManagementServiceClient.ClientCredentials.UserName.Password`.
      * Tilldela konstantvärdet `HttpClientCredentialType.Basic` till fältet `BasicHttpBindingSecurity.Transport.ClientCredentialType`.

   * Tilldela konstantvärdet `BasicHttpSecurityMode.TransportCredentialOnly` till fältet `BasicHttpBindingSecurity.Security.Mode`.

1. Hämta ett PDF-dokument.

   * Skapa en `BLOB` genom att använda dess konstruktor. The `BLOB` -objektet används för att lagra ett PDF-dokument som en profil tillämpas på.
   * Skapa en `System.IO.FileStream` genom att anropa dess konstruktor och skicka ett strängvärde som representerar filplatsen för PDF-dokumentet och läget som filen ska öppnas i.
   * Skapa en bytearray som lagrar innehållet i `System.IO.FileStream` -objekt. Ta reda på bytearrayens storlek genom att hämta `System.IO.FileStream` objektets `Length` -egenskap.
   * Fylla i bytearrayen med strömdata genom att anropa `System.IO.FileStream` objektets `Read` -metod. Skicka bytearrayen, startpositionen och strömlängden som ska läsas.
   * Fyll i `BLOB` genom att tilldela `MTOM` fält med bytearrayens innehåll.

1. Använd en befintlig profil för dokumentet i PDF.

   Tillämpa en profil på PDF-dokumentet genom att anropa `RightsManagementServiceClient` objektets `protectDocument` och skicka följande värden:

   * The `BLOB` -objekt som innehåller det PDF-dokument som profilen tillämpas på.
   * Ett strängvärde som anger dokumentets namn.
   * Ett strängvärde som anger namnet på den principuppsättning som principen tillhör. Du kan ange en `null` det värde som resulterar i `MyPolicies` principuppsättning används.
   * Ett strängvärde som anger principnamnet.
   * Ett strängvärde som representerar namnet på användarhanterardomänen för den användare som är dokumentets utgivare. Parametervärdet är valfritt och kan vara null (om parametern är null måste nästa parametervärde vara `null`).
   * Ett strängvärde som representerar namnet på den kanoniska användaren av användarhanteraren som är dokumentets utgivare. Det här parametervärdet är valfritt och kan vara null (om parametern är null måste det föregående parametervärdet vara `null`).
   * A `RMLocale` värde som anger språkvärdet (till exempel `RMLocale.en`).
   * En strängutdataparameter som används för att lagra principens identifierarvärde.
   * En strängutdataparameter som används för att lagra det principskyddade identifierarvärdet.
   * En strängutdataparameter som används för att lagra mime-typen (till exempel `application/pdf`).

   The `protectDocument` returnerar en `BLOB` objekt som innehåller det principskyddade PDF-dokumentet.

1. Spara dokumentet PDF.

   * Skapa en `System.IO.FileStream` genom att anropa dess konstruktor och skicka ett strängvärde som representerar filplatsen för det principskyddade PDF-dokumentet.
   * Skapa en bytearray som lagrar datainnehållet i `BLOB` objekt som returneras av `protectDocument` -metod. Fylla i bytearrayen genom att hämta värdet för `BLOB` objektets `MTOM` datamedlem.
   * Skapa en `System.IO.BinaryWriter` genom att anropa dess konstruktor och skicka `System.IO.FileStream` -objekt.
   * Skriv bytearrayens innehåll till en PDF-fil genom att anropa `System.IO.BinaryWriter` objektets `Write` och skicka bytearrayen.

**Exempel på koder**

Följande snabbstarter innehåller kodexempel på hur du använder dokumentsäkerhetstjänsten:

* &quot;Snabbstart (MTOM): Tillämpa en princip på ett PDF-dokument med hjälp av webbtjänstens API&quot;
* &quot;Snabbstart (SwaRef): Tillämpa en princip på ett PDF-dokument med hjälp av webbtjänstens API &quot;

## Ta bort profiler från PDF-dokument {#removing-policies-from-pdf-documents}

Du kan ta bort en profil från ett profilskyddat dokument om du vill ta bort skyddet från dokumentet. Det vill säga om du inte längre vill att dokumentet ska skyddas av en profil. Om du vill uppdatera ett policyskyddat dokument med en nyare profil är det effektivare att byta profil i stället för att ta bort profilen och lägga till den uppdaterade profilen.

>[!NOTE]
>
>Mer information om tjänsten Dokumentsäkerhet finns i [Tjänstreferens för AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Sammanfattning av steg {#summary_of_steps-4}

Så här tar du bort en profil från ett principskyddat PDF-dokument:

1. Inkludera projektfiler
1. Skapa ett API-objekt för Document Security Client.
1. Hämta ett policyskyddat PDF-dokument.
1. Ta bort profilen från dokumentet PDF.
1. Spara det oskyddade PDF-dokumentet.

**Inkludera projektfiler**

Inkludera nödvändiga filer i utvecklingsprojektet. Om du skapar ett klientprogram med Java inkluderar du de JAR-filer som behövs. Om du använder webbtjänster måste du inkludera proxyfilerna.

**Skapa ett API-objekt för Document Security Client**

Skapa ett klientobjekt för tjänsten Dokumentsäkerhet innan du programmässigt utför en åtgärd.

**Hämta ett profilskyddat PDF-dokument**

Du kan hämta ett principskyddat PDF-dokument om du vill ta bort en profil. Om du försöker ta bort en princip från ett PDF-dokument som inte skyddas av en profil genereras ett undantagsfel.

**Ta bort profilen från dokumentet PDF**

Du kan ta bort en princip från ett principskyddat PDF-dokument under förutsättning att en administratör anges i anslutningsinställningarna. Annars måste profilen som används för att skydda ett dokument innehålla `SWITCH_POLICY` behörighet att ta bort en profil från ett PDF-dokument. Dessutom måste den användare som anges i AEM Forms anslutningsinställningar också ha den behörigheten. Annars genereras ett undantag.

**Spara det oskyddade PDF-dokumentet**

När dokumentskyddstjänsten har tagit bort en profil från ett PDF-dokument kan du spara det oskyddade PDF-dokumentet som en PDF-fil.

**Se även**

[Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Tillämpa principer på PDF-dokument](protecting-documents-policies.md#applying-policies-to-pdf-documents)

### Ta bort en profil från ett PDF-dokument med Java API {#remove-a-policy-from-a-pdf-document-using-the-java-api}

Ta bort en profil från ett principskyddat PDF-dokument med hjälp av dokumentsäkerhets-API (Java):

1. Inkludera projektfiler.

   Inkludera JAR-klientfiler, som adobe-rightsmanagement-client.jar, i Java-projektets klassökväg.

1. Skapa ett API-objekt för Document Security Client.

   * Skapa en `ServiceClientFactory` objekt som innehåller anslutningsegenskaper.
   * Skapa en `DocumentSecurityClient` genom att använda konstruktorn och skicka `ServiceClientFactory` -objekt.

1. Hämta ett policyskyddat PDF-dokument.

   * Skapa en `java.io.FileInputStream` objekt som representerar det principskyddade PDF-dokumentet genom att använda dess konstruktor och skicka ett strängvärde som anger platsen för PDF-dokumentet.
   * Skapa en `com.adobe.idp.Document` genom att använda konstruktorn och skicka `java.io.FileInputStream` -objekt.

1. Ta bort profilen från dokumentet PDF.

   * Skapa en `DocumentManager` genom att anropa `DocumentSecurityClient` objektets `getDocumentManager` -metod.
   * Ta bort en profil från PDF-dokumentet genom att anropa `DocumentManager` objektets `removeSecurity` metoden och skicka `com.adobe.idp.Document` objekt som innehåller det principskyddade PDF-dokumentet. Den här metoden returnerar en `com.adobe.idp.Document` objekt som innehåller ett oskyddat PDF-dokument.

1. Spara det oskyddade PDF-dokumentet.

   * Skapa en `java.io.File` och se till att filtillägget är PDF.
   * Anropa `Document` objektets `copyToFile` metod för att kopiera innehållet i `Document` till filen (se till att du använder `Document` objekt som returneras av `removeSecurity` metod).

**Exempel på koder**

Följande snabbstarter innehåller kodexempel på hur du använder dokumentsäkerhetstjänsten:

* &quot;Snabbstart (SOAP-läge): Ta bort en princip från ett PDF-dokument med Java API&quot;

### Ta bort en princip med webbtjänstens API {#remove-a-policy-using-the-web-service-api}

Ta bort en profil från ett principskyddat PDF-dokument med hjälp av dokumentsäkerhets-API:t (webbtjänsten):

1. Inkludera projektfiler.

   Skapa ett Microsoft .NET-projekt som använder MTOM. Kontrollera att du använder följande WSDL-definition: `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Ersätt `localhost` med IP-adressen till den server där AEM Forms finns.

1. Skapa ett API-objekt för Document Security Client.

   * Skapa en `DocumentSecurityServiceClient` genom att använda dess standardkonstruktor.
   * Skapa en `DocumentSecurityServiceClient.Endpoint.Address` genom att använda `System.ServiceModel.EndpointAddress` konstruktor. Skicka ett strängvärde som anger WSDL till AEM Forms-tjänsten (till exempel `http://localhost:8080/soap/services/RightsManagementService?WSDL`.) Du behöver inte använda `lc_version` -attribut. Detta attribut används när du skapar en tjänstreferens.)
   * Skapa en `System.ServiceModel.BasicHttpBinding` genom att hämta värdet för `DocumentSecurityServiceClient.Endpoint.Binding` fält. Skicka returvärdet till `BasicHttpBinding`.
   * Ange `System.ServiceModel.BasicHttpBinding` objektets `MessageEncoding` fält till `WSMessageEncoding.Mtom`. Detta värde garanterar att MTOM används.
   * Aktivera grundläggande HTTP-autentisering genom att utföra följande åtgärder:

      * Tilldela AEM formuläranvändarnamn till fältet `DocumentSecurityServiceClient.ClientCredentials.UserName.UserName`.
      * Tilldela motsvarande lösenordsvärde till fältet `DocumentSecurityServiceClient.ClientCredentials.UserName.Password`.
      * Tilldela konstantvärdet `HttpClientCredentialType.Basic` till fältet `BasicHttpBindingSecurity.Transport.ClientCredentialType`.

   * Tilldela konstantvärdet `BasicHttpSecurityMode.TransportCredentialOnly` till fältet `BasicHttpBindingSecurity.Security.Mode`.

1. Hämta ett policyskyddat PDF-dokument.

   * Skapa en `BLOB` genom att använda dess konstruktor. The `BLOB` -objektet används för att lagra det principskyddade PDF-dokumentet som principen tas bort från.
   * Skapa en `System.IO.FileStream` genom att anropa dess konstruktor och skicka ett strängvärde som representerar filplatsen för PDF-dokumentet och läget som filen ska öppnas i.
   * Skapa en bytearray som lagrar innehållet i `System.IO.FileStream` -objekt. Du kan bestämma storleken på bytearrayen genom att hämta `System.IO.FileStream` objektets `Length` -egenskap.
   * Fylla i bytearrayen med strömdata genom att anropa `System.IO.FileStream` objektets `Read` och skickar bytearrayen, startpositionen och den flödeslängd som ska läsas.
   * Fyll i `BLOB` genom att tilldela `MTOM` fält med bytearrayens innehåll.

1. Ta bort profilen från dokumentet PDF.

   Ta bort profilen från dokumentet PDF genom att anropa `DocumentSecurityServiceClient` objektets `removePolicySecurity` metoden och skicka `BLOB` objekt som innehåller det principskyddade PDF-dokumentet. Den här metoden returnerar en `BLOB` objekt som innehåller ett oskyddat PDF-dokument.

1. Spara det oskyddade PDF-dokumentet.

   * Skapa en `System.IO.FileStream` genom att anropa dess konstruktor och skicka ett strängvärde som representerar filplatsen för det oskyddade PDF-dokumentet.
   * Skapa en bytearray som lagrar datainnehållet i `BLOB` objekt som returneras av `removePolicySecurity` -metod. Fylla i bytearrayen genom att hämta värdet för `BLOB` objektets `MTOM` fält.
   * Skapa en `System.IO.BinaryWriter` genom att anropa dess konstruktor och skicka `System.IO.FileStream` -objekt.

**Exempel på koder**

Följande snabbstarter innehåller kodexempel på hur du använder dokumentsäkerhetstjänsten:

* &quot;Snabbstart (MTOM): Ta bort en princip från ett PDF-dokument med hjälp av webbtjänstens API &quot;
* &quot;Snabbstart (SwaRef): Ta bort en princip från ett PDF-dokument med hjälp av webbtjänstens API&quot;

**Se även**

[Anropa AEM Forms med MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Anropa AEM Forms med SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Återkalla åtkomst till dokument {#revoking-access-to-documents}

Du kan återkalla åtkomsten till ett profilskyddat PDF-dokument, vilket gör att alla kopior av dokumentet inte är tillgängliga för användarna. När en användare försöker öppna ett återkallat PDF-dokument omdirigeras de till en angiven URL där ett ändrat dokument kan visas. URL:en som användaren omdirigeras till måste anges programmatiskt. När du återkallar åtkomsten till ett dokument träder ändringen i kraft nästa gång användaren synkroniserar med dokumentsäkerhetstjänsten genom att öppna det profilskyddade dokumentet online.

Möjligheten att återkalla åtkomst till ett dokument ger ytterligare säkerhet. Anta till exempel att en nyare version av ett dokument är tillgänglig och att du inte längre vill att någon ska visa den inaktuella versionen. I det här fallet kan åtkomsten till det äldre dokumentet återkallas och ingen kan visa dokumentet om inte åtkomsten återupprättas.

>[!NOTE]
>
>Mer information om tjänsten Dokumentsäkerhet finns i [Tjänstreferens för AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Sammanfattning av steg {#summary_of_steps-5}

Så här återkallar du ett principskyddat dokument:

1. Inkludera projektfiler.
1. Skapa ett API-objekt för Document Security Client.
1. Hämta ett policyskyddat PDF-dokument.
1. Återkalla det profilskyddade dokumentet.

**Inkludera projektfiler**

Inkludera nödvändiga filer i utvecklingsprojektet. Om du skapar ett klientprogram med Java inkluderar du de JAR-filer som behövs. Om du använder webbtjänster måste du inkludera proxyfilerna.

**Skapa ett API-objekt för Document Security Client**

Innan du programmässigt kan utföra en dokumentsäkerhetstjänståtgärd måste du skapa ett klientobjekt för dokumentsäkerhetstjänsten.

**Hämta ett profilskyddat PDF-dokument**

Hämta ett principskyddat PDF-dokument om du vill återkalla det. Du kan inte återkalla ett dokument som redan har återkallats eller som inte är ett principskyddat dokument.

Om du känner till licensvärdet för det profilskyddade dokumentet behöver du inte hämta det profilskyddade PDF-dokumentet. I de flesta fall måste du dock hämta PDF-dokumentet för att få fram värdet för licensidentifieraren.

**Återkalla det profilskyddade dokumentet**

Om du vill återkalla ett profilskyddat dokument anger du ID för licensen för det profilskyddade dokumentet. Du kan dessutom ange URL:en för ett dokument som användaren kan visa när han/hon försöker öppna det återkallade dokumentet. Anta alltså att ett inaktuellt dokument återkallas. När en användare försöker öppna det återkallade dokumentet visas ett uppdaterat dokument i stället för det återkallade dokumentet.

>[!NOTE]
>
>Om du försöker återkalla ett dokument som redan har återkallats genereras ett undantag.

**Se även**

[Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Tillämpa principer på PDF-dokument](protecting-documents-policies.md#applying-policies-to-pdf-documents)

[Återställa åtkomst till återkallade dokument](protecting-documents-policies.md#reinstating-access-to-revoked-documents)

### Återkalla åtkomst till dokument med Java API {#revoke-access-to-documents-using-the-java-api}

Återkalla åtkomst till ett principskyddat PDF-dokument med hjälp av dokumentsäkerhets-API (Java):

1. Inkludera projektfiler

   Inkludera JAR-klientfiler, som adobe-rightsmanagement-client.jar, i Java-projektets klassökväg.

1. Skapa ett API-objekt för Document Security Client

   * Skapa en `ServiceClientFactory` objekt som innehåller anslutningsegenskaper.
   * Skapa en `DocumentSecurityClient` genom att använda konstruktorn och skicka `ServiceClientFactory` -objekt.

1. Hämta ett profilskyddat PDF-dokument

   * Skapa en `java.io.FileInputStream` objekt som representerar det principskyddade PDF-dokumentet genom att använda dess konstruktor och skicka ett strängvärde som anger platsen för PDF-dokumentet.
   * Skapa en `com.adobe.idp.Document` genom att använda konstruktorn och skicka `java.io.FileInputStream` -objekt.

1. Återkalla det profilskyddade dokumentet

   * Skapa en `DocumentManager` genom att anropa `DocumentSecurityClient` objektets `getDocumentManager` -metod.
   * Hämta det profilskyddade dokumentets ID-värde genom att anropa `DocumentManager` objektets `getLicenseId` -metod. Skicka `com.adobe.idp.Document` objekt som representerar det principskyddade dokumentet. Den här metoden returnerar ett strängvärde som representerar licensens identifierarvärde.
   * Skapa en `LicenseManager` genom att anropa `DocumentSecurityClient` objektets `getLicenseManager` -metod.
   * Återkalla det profilskyddade dokumentet genom att anropa `LicenseManager` objektets `revokeLicense` och skicka följande värden:

      * Ett strängvärde som anger det principskyddade dokumentets ID-värde (ange returvärdet för `DocumentManager` objektets `getLicenseId` metod).
      * En statisk datamedlem i `License` gränssnitt som anger orsaken till att dokumentet återkallas. Du kan till exempel ange `License.DOCUMENT_REVISED`.
      * A `java.net.URL` värde som anger platsen där ett reviderat dokument finns. Om du inte vill dirigera om en användare till en annan URL kan du skicka `null`.

**Exempel på koder**

Följande snabbstarter innehåller kodexempel på hur du använder dokumentsäkerhetstjänsten:

* &quot;Snabbstart (SOAP-läge): Återkalla ett dokument med Java API&quot;

### Återkalla åtkomst till dokument med hjälp av webbtjänstens API {#revoke-access-to-documents-using-the-web-service-api}

Återkalla åtkomst till ett principskyddat PDF-dokument med hjälp av API:t för dokumentsäkerhet (webbtjänsten):

1. Inkludera projektfiler

   Skapa ett Microsoft .NET-projekt som använder MTOM. Kontrollera att du använder följande WSDL-definition: `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Ersätt `localhost` med IP-adressen till den server där AEM Forms finns.

1. Skapa ett API-objekt för Document Security Client

   * Skapa en `DocumentSecurityServiceClient` genom att använda dess standardkonstruktor.
   * Skapa en `DocumentSecurityServiceClient.Endpoint.Address` genom att använda `System.ServiceModel.EndpointAddress` konstruktor. Skicka ett strängvärde som anger WSDL till AEM Forms-tjänsten (till exempel `http://localhost:8080/soap/services/RightsManagementService?WSDL`.) Du behöver inte använda `lc_version` -attribut. Detta attribut används när du skapar en tjänstreferens.)
   * Skapa en `System.ServiceModel.BasicHttpBinding` genom att hämta värdet för `DocumentSecurityServiceClient.Endpoint.Binding` fält. Skicka returvärdet till `BasicHttpBinding`.
   * Ange `System.ServiceModel.BasicHttpBinding` objektets `MessageEncoding` fält till `WSMessageEncoding.Mtom`. Detta värde garanterar att MTOM används.
   * Aktivera grundläggande HTTP-autentisering genom att utföra följande åtgärder:

      * Tilldela AEM formuläranvändarnamn till fältet `DocumentSecurityServiceClient.ClientCredentials.UserName.UserName`.
      * Tilldela motsvarande lösenordsvärde till fältet `DocumentSecurityServiceClient.ClientCredentials.UserName.Password`.
      * Tilldela konstantvärdet `HttpClientCredentialType.Basic` till fältet `BasicHttpBindingSecurity.Transport.ClientCredentialType`.

   * Tilldela konstantvärdet `BasicHttpSecurityMode.TransportCredentialOnly` till fältet `BasicHttpBindingSecurity.Security.Mode`.

1. Hämta ett profilskyddat PDF-dokument

   * Skapa en `BLOB` genom att använda dess konstruktor. The `BLOB` används för att lagra ett principskyddat PDF-dokument som har återkallats.
   * Skapa en `System.IO.FileStream` genom att anropa dess konstruktor och skicka ett strängvärde som representerar filplatsen för det principskyddade PDF-dokumentet som ska återkallas samt läget som filen ska öppnas i.
   * Skapa en bytearray som lagrar innehållet i `System.IO.FileStream` -objekt. Du kan bestämma storleken på bytearrayen genom att hämta `System.IO.FileStream` objektets `Length` -egenskap.
   * Fylla i bytearrayen med strömdata genom att anropa `System.IO.FileStream` objektets `Read` och skickar bytearrayen, startpositionen och den flödeslängd som ska läsas.
   * Fyll i `BLOB` genom att tilldela `MTOM` fält med bytearrayens innehåll.

1. Återkalla det profilskyddade dokumentet

   * Hämta det profilskyddade dokumentets ID-värde genom att anropa `DocumentSecurityServiceClient` objektets `getLicenseID` metoden och skicka `BLOB` objekt som representerar det principskyddade dokumentet. Den här metoden returnerar ett strängvärde som representerar licens-ID:t.
   * Återkalla det profilskyddade dokumentet genom att anropa `DocumentSecurityServiceClient` objektets `revokeLicense` och skicka följande värden:

      * Ett strängvärde som anger det principskyddade dokumentets ID-värde (ange returvärdet för `DocumentSecurityServiceService` objektets `getLicenseId` metod).
      * En statisk datamedlem i `Reason` uppräkning som anger orsaken till att dokumentet återkallas. Du kan till exempel ange `Reason.DOCUMENT_REVISED`.
      * A `string` värde som anger den URL-plats där det reviderade dokumentet finns. Om du inte vill dirigera om en användare till en annan URL kan du skicka `null`.

**Exempel på koder**

Följande snabbstarter innehåller kodexempel på hur du använder dokumentsäkerhetstjänsten:

* &quot;Snabbstart (MTOM): Återkalla ett dokument med hjälp av webbtjänstens API&quot;
* &quot;Snabbstart (SwaRef): Återkalla ett dokument med hjälp av webbtjänstens API&quot;

**Se även**

[Ta bort profiler från Word-dokument](protecting-documents-policies.md#removing-policies-from-word-documents)

[Anropa AEM Forms med MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Anropa AEM Forms med SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Återställa åtkomst till återkallade dokument {#reinstating-access-to-revoked-documents}

Du kan återställa åtkomsten till ett återkallat PDF-dokument, vilket gör att alla kopior av det återkallade dokumentet blir tillgängliga för användarna. När en användare öppnar ett återskapat dokument som har återkallats kan användaren visa dokumentet.

>[!NOTE]
>
>Mer information om tjänsten Dokumentsäkerhet finns i [Tjänstreferens för AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Sammanfattning av steg {#summary_of_steps-6}

Så här återställer du åtkomsten till ett återkallat PDF-dokument:

1. Inkludera projektfiler.
1. Skapa ett API-objekt för Document Security Client.
1. Hämta licensidentifieraren för det återkallade PDF-dokumentet.
1. Återställa åtkomst till det återkallade PDF-dokumentet.

**Inkludera projektfiler**

Inkludera nödvändiga filer i utvecklingsprojektet. Om du skapar ett klientprogram med Java inkluderar du de JAR-filer som behövs. Om du använder webbtjänster måste du inkludera proxyfilerna.

**Skapa ett API-objekt för Document Security Client**

Innan du programmässigt kan utföra en dokumentsäkerhetstjänståtgärd måste du skapa ett klientobjekt för dokumentsäkerhetstjänsten. Om du använder Java API skapar du en `DocumentSecurityClient` -objekt. Om du använder webbtjänstens API för dokumentsäkerhet skapar du en `DocumentSecurityServiceService` -objekt.

**Hämta licensidentifieraren för det återkallade PDF-dokumentet**

Hämta licensidentifieraren för det återkallade PDF-dokumentet för att återskapa ett återkallat PDF-dokument. När du har fått fram licensens ID-värde kan du återskapa ett återkallat dokument. Om du försöker återskapa ett dokument som inte har återkallats genereras ett undantag.

**Återställa åtkomst till det återkallade PDF-dokumentet**

Om du vill återupprätta åtkomsten till ett återkallat PDF-dokument måste du ange det återkallade dokumentets Licensidentifierare. Om du försöker återupprätta åtkomsten till ett PDF-dokument som inte har återkallats genereras ett undantagsfel.

**Se även**

[Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Tillämpa principer på PDF-dokument](protecting-documents-policies.md#applying-policies-to-pdf-documents)

[Återkalla åtkomst till dokument](protecting-documents-policies.md#revoking-access-to-documents)

### Återställa åtkomst till återkallade dokument med Java API {#reinstate-access-to-revoked-documents-using-the-java-api}

Återskapa åtkomst till ett återkallat dokument med hjälp av dokumentsäkerhets-API (Java):

1. Inkludera projektfiler.

   Inkludera JAR-klientfiler, som adobe-rightsmanagement-client.jar, i Java-projektets klassökväg.

1. Skapa ett API-objekt för Document Security Client.

   * Skapa en `ServiceClientFactory` objekt som innehåller anslutningsegenskaper.
   * Skapa en `DocumentSecurityClient` genom att använda konstruktorn och skicka `ServiceClientFactory` -objekt.

1. Hämta licensidentifieraren för det återkallade PDF-dokumentet.

   * Skapa en `java.io.FileInputStream` objekt som representerar det spärrade PDF-dokumentet med hjälp av dess konstruktor och som skickar ett strängvärde som anger platsen för PDF-dokumentet.
   * Skapa en `com.adobe.idp.Document` genom att använda konstruktorn och skicka `java.io.FileInputStream` -objekt.
   * Skapa en `DocumentManager` genom att anropa `DocumentSecurityClient` objektets `getDocumentManager` -metod.
   * Hämta det återkallade dokumentets ID-värde genom att anropa `DocumentManager` objektets `getLicenseId` metoden och skicka `com.adobe.idp.Document` som representerar det återkallade dokumentet. Den här metoden returnerar ett strängvärde som representerar licens-ID:t.

1. Återställa åtkomst till det återkallade PDF-dokumentet.

   * Skapa en `LicenseManager` genom att anropa `DocumentSecurityClient` objektets `getLicenseManager` -metod.
   * Återskapa åtkomst till det återkallade PDF-dokumentet genom att anropa `LicenseManager` objektets `unrevokeLicense` och skickar det återkallade dokumentets ID-värde.

**Exempel på koder**

Följande snabbstarter innehåller kodexempel på hur du använder dokumentsäkerhetstjänsten:

* &quot;Snabbstart (SOAP-läge): Återställa åtkomst till ett återkallat dokument med hjälp av webbtjänstens API&quot;

### Återställa åtkomst till återkallade dokument med hjälp av webbtjänstens API {#reinstate-access-to-revoked-documents-using-the-web-service-api}

Återställa åtkomst till ett återkallat dokument med hjälp av API:t för dokumentsäkerhet (webbtjänsten):

1. Inkludera projektfiler.

   Skapa ett Microsoft .NET-projekt som använder MTOM. Kontrollera att du använder följande WSDL-definition: `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Ersätt `localhost` med IP-adressen till den server där AEM Forms finns.

1. Skapa ett API-objekt för Document Security Client.

   * Skapa en `DocumentSecurityServiceClient` genom att använda dess standardkonstruktor.
   * Skapa en `DocumentSecurityServiceClient.Endpoint.Address` genom att använda `System.ServiceModel.EndpointAddress` konstruktor. Skicka ett strängvärde som anger WSDL till AEM Forms-tjänsten (till exempel `http://localhost:8080/soap/services/RightsManagementService?WSDL`.) Du behöver inte använda `lc_version` -attribut. Detta attribut används när du skapar en tjänstreferens.)
   * Skapa en `System.ServiceModel.BasicHttpBinding` genom att hämta värdet för `DocumentSecurityServiceClient.Endpoint.Binding` fält. Skicka returvärdet till `BasicHttpBinding`.
   * Ange `System.ServiceModel.BasicHttpBinding` objektets `MessageEncoding` fält till `WSMessageEncoding.Mtom`. Detta värde garanterar att MTOM används.
   * Aktivera grundläggande HTTP-autentisering genom att utföra följande åtgärder:

      * Tilldela AEM formuläranvändarnamn till fältet `DocumentSecurityServiceClient.ClientCredentials.UserName.UserName`.
      * Tilldela motsvarande lösenordsvärde till fältet `DocumentSecurityServiceClient.ClientCredentials.UserName.Password`.
      * Tilldela konstantvärdet `HttpClientCredentialType.Basic` till fältet `BasicHttpBindingSecurity.Transport.ClientCredentialType`.

   * Tilldela konstantvärdet `BasicHttpSecurityMode.TransportCredentialOnly` till fältet `BasicHttpBindingSecurity.Security.Mode`.

1. Hämta licensidentifieraren för det återkallade PDF-dokumentet.

   * Skapa en `BLOB` genom att använda dess konstruktor. The `BLOB` används för att lagra ett återkallat PDF-dokument som åtkomsten återställs till.
   * Skapa en `System.IO.FileStream` genom att anropa dess konstruktor och skicka ett strängvärde som representerar filplatsen för det spärrade PDF-dokumentet och läget som filen ska öppnas i.
   * Skapa en bytearray som lagrar innehållet i `System.IO.FileStream` -objekt. Du kan bestämma storleken på bytearrayen genom att hämta `System.IO.FileStream` objektets `Length` -egenskap.
   * Fylla i bytearrayen med strömdata genom att anropa `System.IO.FileStream` objektets `Read` och skickar bytearrayen, startpositionen och den flödeslängd som ska läsas.
   * Fyll i `BLOB` genom att tilldela `MTOM` fält med bytearrayens innehåll.

1. Återställa åtkomst till det återkallade PDF-dokumentet.

   * Hämta det återkallade dokumentets ID-värde genom att anropa `DocumentSecurityServiceClient` objektets `getLicenseID` metoden och skicka `BLOB` som representerar det återkallade dokumentet. Den här metoden returnerar ett strängvärde som representerar licens-ID:t.
   * Återskapa åtkomst till det återkallade PDF-dokumentet genom att anropa `DocumentSecurityServiceClient` objektets `unrevokeLicense` och skickar ett strängvärde som anger ID-värdet för det spärrade PDF-dokumentet (skicka returvärdet för `DocumentSecurityServiceClient` objektets `getLicenseId` metod).

**Exempel på koder**

Följande snabbstarter innehåller kodexempel på hur du använder dokumentsäkerhetstjänsten:

* &quot;Snabbstart (MTOM): Återställa åtkomst till ett återkallat dokument med hjälp av webbtjänstens API&quot;
* &quot;Snabbstart (SwaRef): Återställa åtkomst till ett återkallat dokument med hjälp av webbtjänstens API&quot;

**Se även**

[Anropa AEM Forms med MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Anropa AEM Forms med SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Inspektera skyddat PDF-dokument {#inspecting-policy-protected-pdf-documents}

Du kan använda API:t för dokumentsäkerhetstjänsten (Java och webbtjänsten) för att inspektera policyskyddade PDF-dokument. När du inspekterar principskyddade PDF-dokument returneras information om det principskyddade PDF-dokumentet. Du kan till exempel bestämma vilken profil som användes för att skydda dokumentet och datumet då dokumentet var skyddat.

Du kan inte utföra den här åtgärden om LiveCyclet är version 8.x eller tidigare. I AEM Forms finns stöd för att inspektera policyskyddade dokument. Om du försöker inspektera ett principskyddat dokument med LiveCycle 8.x (eller tidigare) genereras ett undantag.

>[!NOTE]
>
>Mer information om tjänsten Dokumentsäkerhet finns i [Tjänstreferens för AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Sammanfattning av steg {#summary_of_steps-7}

Så här inspekterar du ett principskyddat PDF-dokument:

1. Inkludera projektfiler.
1. Skapa ett API-objekt för Document Security Client.
1. Hämta ett profilskyddat dokument som ska inspekteras.
1. Hämta information om det profilskyddade dokumentet.

**Inkludera projektfiler**

Inkludera nödvändiga filer i utvecklingsprojektet. Om du skapar ett klientprogram med Java, inkluderar du de JAR-filer som behövs. Om du använder webbtjänster måste du ta med proxyfilerna.

**Skapa ett API-objekt för Document Security Client**

Skapa ett klientobjekt för tjänsten Dokumentsäkerhet innan du programmässigt utför en åtgärd. Om du använder Java API skapar du en `RightsManagementClient` -objekt. Om du använder webbtjänstens API för dokumentsäkerhet skapar du en `RightsManagementServiceService` -objekt.

**Hämta ett profilskyddat dokument att inspektera**

Hämta ett policyskyddat dokument om du vill inspektera det. Om du försöker inspektera ett dokument som inte är skyddat med en profil eller som har återkallats genereras ett undantag.

**Inspect dokumentet**

När du har hämtat ett policyskyddat dokument kan du inspektera det.

**Hämta information om det profilskyddade dokumentet**

När du har inspekterat ett policyskyddat PDF-dokument kan du få information om det. Du kan till exempel bestämma vilken profil som ska användas för att skydda dokumentet.

Om du skyddar ett dokument med en profil som tillhör Min profil och sedan ringer du `RMInspectResult.getPolicysetName` eller `RMInspectResult.getPolicysetId`, null returneras.

Om dokumentet är skyddat med en profil som finns i en profiluppsättning (annan än Min profil) är det `RMInspectResult.getPolicysetName` och `RMInspectResult.getPolicysetId` returnera giltiga strängar.

**Se även**

[Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Inspect Policy Protected PDF Documents med Java API {#inspect-policy-protected-pdf-documents-using-the-java-api}

Inspect är ett policyskyddat PDF-dokument med hjälp av API:t för dokumentsäkerhetstjänsten (Java):

1. Inkludera projektfiler.

   Inkludera JAR-klientfiler, t.ex. adobe-rightsmanagement-client.jar, i Java-projektets klassökväg. Information om platsen för dessa filer finns i [Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

1. Skapa ett API-objekt för Document Security Client.

   * Skapa en `ServiceClientFactory` objekt som innehåller anslutningsegenskaper. (Se [Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).)
   * Skapa en `RightsManagementClient` genom att använda konstruktorn och skicka `ServiceClientFactory` -objekt.

1. Hämta ett profilskyddat dokument som ska inspekteras.

   * Skapa en `java.io.FileInputStream` objekt som representerar det principskyddade PDF-dokumentet med hjälp av dess konstruktor. Skicka ett strängvärde som anger platsen för PDF-dokumentet.
   * Skapa en `com.adobe.idp.Document` genom att använda konstruktorn och skicka `java.io.FileInputStream` -objekt.

1. Inspect dokumentet.

   * Skapa en `DocumentManager` genom att anropa `RightsManagementClient` objektets `getDocumentManager` -metod.
   * Inspect det policyskyddade dokumentet genom att anropa `LicenseManager` objektets `inspectDocument` -metod. Skicka `com.adobe.idp.Document` objekt som innehåller det principskyddade PDF-dokumentet. Den här metoden returnerar en `RMInspectResult` -objekt som innehåller information om det principskyddade dokumentet.

1. Hämta information om det profilskyddade dokumentet.

   Om du vill få information om det principskyddade dokumentet ska du anropa rätt metod som tillhör `RMInspectResult` -objekt. Om du till exempel vill hämta principnamnet anropar du `RMInspectResult` objektets `getPolicyName` -metod.

**Exempel på koder**

Följande snabbstarter innehåller kodexempel på hur du använder dokumentsäkerhetstjänsten:

* &quot;Snabbstart (SOAP-läge): Inspektera principskyddade PDF-dokument med Java API&quot;

### Inspect Policy Protected PDF Documents med hjälp av webbtjänstens API {#inspect-policy-protected-pdf-documents-using-the-web-service-api}

Inspect är ett policyskyddat PDF-dokument med hjälp av API:t för dokumentsäkerhetstjänsten (webbtjänsten):

1. Inkludera projektfiler.

   Skapa ett Microsoft .NET-projekt som använder MTOM. Kontrollera att du använder följande WSDL-definition: `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Ersätt `localhost` med IP-adressen till den server där AEM Forms finns.

1. Skapa ett API-objekt för Document Security Client.

   * Skapa en `RightsManagementServiceClient` genom att använda dess standardkonstruktor.
   * Skapa en `RightsManagementServiceClient.Endpoint.Address` genom att använda `System.ServiceModel.EndpointAddress` konstruktor. Skicka ett strängvärde som anger WSDL till AEM Forms-tjänsten (till exempel `http://localhost:8080/soap/services/RightsManagementService?WSDL`.) Du behöver inte använda `lc_version` -attribut. Detta attribut används när du skapar en tjänstreferens.)
   * Skapa en `System.ServiceModel.BasicHttpBinding` genom att hämta värdet för `RightsManagementServiceClient.Endpoint.Binding` fält. Skicka returvärdet till `BasicHttpBinding`.
   * Ange `System.ServiceModel.BasicHttpBinding` objektets `MessageEncoding` fält till `WSMessageEncoding.Mtom`. Detta värde garanterar att MTOM används.
   * Aktivera grundläggande HTTP-autentisering genom att utföra följande åtgärder:

      * Tilldela AEM formuläranvändarnamn till fältet `RightsManagementServiceClient.ClientCredentials.UserName.UserName`.
      * Tilldela motsvarande lösenordsvärde till fältet `RightsManagementServiceClient.ClientCredentials.UserName.Password`.
      * Tilldela konstantvärdet `HttpClientCredentialType.Basic` till fältet `BasicHttpBindingSecurity.Transport.ClientCredentialType`.

   * Tilldela konstantvärdet `BasicHttpSecurityMode.TransportCredentialOnly` till fältet `BasicHttpBindingSecurity.Security.Mode`.

1. Hämta ett profilskyddat dokument som ska inspekteras.

   * Skapa en `BLOB` genom att använda dess konstruktor. The `BLOB` -objektet används för att lagra ett PDF-dokument som ska inspekteras.
   * Skapa en `System.IO.FileStream` genom att anropa dess konstruktor. Skicka ett strängvärde som representerar filplatsen för PDF-dokumentet och läget som filen ska öppnas i.
   * Skapa en bytearray som lagrar innehållet i `System.IO.FileStream` -objekt. Du kan bestämma storleken på bytearrayen genom att hämta `System.IO.FileStream` objektets `Length` -egenskap.
   * Fylla i bytearrayen med strömdata genom att anropa `System.IO.FileStream` objektets `Read` -metod. Skicka bytearrayen, startpositionen och strömlängden som ska läsas.
   * Fyll i `BLOB` genom att tilldela `MTOM` fält med bytearrayens innehåll.

1. Inspect dokumentet.

   Inspect det policyskyddade dokumentet genom att anropa `RightsManagementServiceClient` objektets `inspectDocument` -metod. Skicka `BLOB` objekt som innehåller det principskyddade PDF-dokumentet. Den här metoden returnerar en `RMInspectResult` -objekt som innehåller information om det principskyddade dokumentet.

1. Hämta information om det profilskyddade dokumentet.

   Hämta information om det principskyddade dokumentet genom att hämta värdet för rätt fält som tillhör `RMInspectResult` -objekt. Om du till exempel vill hämta principnamnet måste du hämta värdet för `RMInspectResult` objektets `policyName` fält.

**Exempel på koder**

Följande snabbstarter innehåller kodexempel på hur du använder dokumentsäkerhetstjänsten:

* &quot;Snabbstart (MTOM): Inspektera principskyddade PDF-dokument med webbtjänstens API&quot;
* &quot;Snabbstart (SwaRef): Inspektera principskyddade PDF-dokument med webbtjänstens API&quot;

**Se även**

[Anropa AEM Forms med MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Anropa AEM Forms med SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Skapa vattenstämplar {#creating-watermarks}

Vattenstämplar säkerställer dokumentets säkerhet genom att unikt identifiera dokumentet och kontrollera upphovsrättsintrång. Du kan t.ex. skapa och placera en vattenstämpel med statusen Konfidentiellt på alla sidor i ett dokument. När du har skapat en vattenstämpel kan du inkludera den som en del av en profil. Det innebär att du kan ställa in principens vattenstämpelattribut med den nya vattenstämpeln. När en profil som innehåller en vattenstämpel har tillämpats på ett dokument, visas vattenstämpeln i det profilskyddade dokumentet.

>[!NOTE]
>
>Endast användare med administratörsbehörighet för dokumentsäkerhet kan skapa vattenstämplar. Det innebär att du måste ange en sådan användare när du definierar de anslutningsinställningar som krävs för att skapa ett klientobjekt för tjänsten Dokumentsäkerhet.

>[!NOTE]
>
>Mer information om tjänsten Dokumentsäkerhet finns i [Tjänstreferens för AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Sammanfattning av steg {#summary_of_steps-8}

Så här skapar du en vattenstämpel:

1. Inkludera projektfiler.
1. Skapa ett API-objekt för Document Security Client.
1. Ange vattenstämpelattribut.
1. Registrera vattenstämpeln hos Document Security-tjänsten.

**Inkludera projektfiler**

Inkludera nödvändiga filer i utvecklingsprojektet. Om du skapar ett klientprogram med Java inkluderar du de JAR-filer som behövs. Om du använder webbtjänster måste du inkludera proxyfilerna.

**Skapa ett API-objekt för Document Security Client**

Innan du programmässigt kan utföra en dokumentsäkerhetstjänståtgärd måste du skapa ett klientobjekt för dokumentsäkerhetstjänsten. Om du använder Java API skapar du en `RightsManagementClient` -objekt. Om du använder webbtjänstens API för dokumentsäkerhet skapar du en `RightsManagementServiceService` -objekt.

**Ange vattenstämpelattribut**

Om du vill skapa en vattenstämpel måste du ange vattenstämpelattribut. Namnattributet måste alltid definieras. Förutom name-attributet måste du ange minst ett av följande attribut:

* Egen text
* DatumInkluderat
* Användar-IDInkluderat
* AnvändarnamnInkluderat

I följande tabell visas de nyckel- och värdepar som krävs när du skapar en vattenstämpel med hjälp av webbtjänster.

<table>
 <thead>
  <tr>
   <th><p>Nyckelnamn</p></th>
   <th><p>Beskrivning</p></th>
   <th><p>Värde</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p><code>WaterBackCmd:IS_USERNAME_ENABLED</code></p></td>
   <td><p>Anger om användarnamnet för användaren som öppnar dokumentet är en del av vattenstämpeln.</p></td>
   <td><p>Sant eller falskt</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:IS_USERID_ENABLED</code></p></td>
   <td><p>Anger om identifieringen av användaren som öppnar dokumentet är en del av vattenstämpeln.</p></td>
   <td><p>Sant eller falskt</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:IS_CURRENTDATE_ENABLED</code></p></td>
   <td><p>Anger om det aktuella datumet är en del av vattenstämpeln.</p></td>
   <td><p>Sant eller falskt</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:IS_CUSTOMTEXT_ENABLED</code></p></td>
   <td><p>Om det här värdet är true måste värdet för den anpassade texten anges med <code>WaterBackCmd:SRCTEXT</code>.</p></td>
   <td><p>Sant eller falskt</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:OPACITY</code></p></td>
   <td><p>Anger vattenstämpelns opacitet. Standardvärdet är 0,5 om det inte anges.</p></td>
   <td><p>Ett värde mellan 0,0 och 1,0.</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:ROTATION</code></p></td>
   <td><p>Anger vattenstämpelns rotation. Standardvärdet är 0 grader.</p></td>
   <td><p>Ett värde mellan 0 och 359.</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:SCALE</code></p></td>
   <td><p>Om det här värdet anges <code>WaterBackCmd:IS_SIZE_ENABLED</code> måste finnas och värdet måste vara true. Om det här attributet inte anges anpassas standardbeteendet till sidan.</p></td>
   <td><p>Ett värde större än 0,0 och mindre än eller lika med 1,0.</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:HORIZ_ALIGN</code></p></td>
   <td><p>Anger vattenstämpelns vågräta justering. Standardvärdet är center.</p></td>
   <td><p>vänster, mitten eller höger</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:VERT_ALIGN</code></p></td>
   <td><p>Anger vattenstämpelns lodräta justering. Standardvärdet är center.</p></td>
   <td><p>överkant, mitten eller nederkant</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:IS_USE_BACKGROUND</code></p></td>
   <td><p>Anger om vattenstämpeln är en bakgrund. Standardvärdet är false.</p></td>
   <td><p>Sant eller falskt</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:IS_SIZE_ENABLED</code></p></td>
   <td><p>True om en anpassad skala har angetts. Om det här värdet är true måste även SCALE anges. Om det här värdet är false anpassas standardvärdet till sidan.</p></td>
   <td><p>Sant eller falskt</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:SRCTEXT</code></p></td>
   <td><p>Anger den anpassade texten för en vattenstämpel. Om det här värdet finns <code>WaterBackCmd:IS_CUSTOMTEXT_ENABLED</code> måste också finnas och vara inställd på true.</p></td>
   <td><p>Sant eller falskt</p></td>
  </tr>
 </tbody>
</table>

Alla vattenstämplar måste ha något av följande attribut definierade:

* `WaterBackCmd:IS_USERNAME_ENABLED`
* `WaterBackCmd:IS_USERID_ENABLED`
* `WaterBackCmd:IS_CURRENTDATE_ENABLED`
* `WaterBackCmd:IS_CUSTOMTEXT_ENABLED`

Alla andra attribut är valfria.

**Registrera vattenstämpeln**

En ny vattenstämpel måste registreras hos dokumentsäkerhetstjänsten innan den kan användas. När du har registrerat en vattenstämpel kan du använda den inom profiler.

**Se även**

[Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Tillämpa principer på PDF-dokument](protecting-documents-policies.md#applying-policies-to-pdf-documents)

### Skapa vattenstämplar med Java API {#create-watermarks-using-the-java-api}

Skapa en vattenstämpel med API:t för dokumentsäkerhet (Java):

1. Inkludera projektfiler.

   Inkludera klient-JAR-filer, som `adobe-rightsmanagement-client.jar`, i Java-projektets klassökväg.

1. Skapa ett API-objekt för Document Security Client.

   * Skapa en `ServiceClientFactory` objekt som innehåller anslutningsegenskaper.
   * Skapa en `RightsManagementClient` genom att använda konstruktorn och skicka `ServiceClientFactory` -objekt.

1. Ange vattenstämpelattribut

   * Skapa en `Watermark` genom att anropa `InfomodelObjectFactory` objektets statiska `createWatermark` -metod. Den här metoden returnerar en `Watermark` -objekt.
   * Ange vattenstämpelns namnattribut genom att anropa `Watermark` objektets `setName` och skickar ett strängvärde som anger principnamnet.
   * Ange vattenstämpelns bakgrundsattribut genom att anropa `Watermark` objektets `setBackground` metod och att skicka `true`. Om du anger det här attributet visas vattenstämpeln i dokumentets bakgrund.
   * Ange vattenstämpelns anpassade textattribut genom att anropa `Watermark` objektets `setCustomText` och skickar ett strängvärde som representerar vattenstämpelns text.
   * Ange vattenstämpelns opacitetsattribut genom att anropa `Watermark` objektets `setOpacity` och skickar ett heltalsvärde som anger opacitetsnivån. Värdet 100 anger att vattenstämpeln är helt ogenomskinlig och värdet 0 anger att vattenstämpeln är helt genomskinlig.

1. Registrera vattenstämpeln.

   * Skapa en `WatermarkManager` genom att anropa `RightsManagementClient` objektets `getWatermarkManager` -metod. Den här metoden returnerar en `WatermarkManager` -objekt.
   * Registrera vattenstämpeln genom att anropa `WatermarkManager` objektets `registerWatermark` metoden och skicka `Watermark` objekt som representerar vattenstämpeln som ska registreras. Den här metoden returnerar ett strängvärde som representerar vattenstämpelns ID-värde.

**Exempel på koder**

Följande snabbstarter innehåller kodexempel på hur du använder dokumentsäkerhetstjänsten:

* &quot;Snabbstart (SOAP-läge): Skapa en vattenstämpel med Java API&quot;

### Skapa vattenstämplar med webbtjänstens API {#create-watermarks-using-the-web-service-api}

Skapa en vattenstämpel med API:t för dokumentsäkerhet (webbtjänst):

1. Skapa ett API-objekt för Document Security Client.

   Skapa ett Microsoft .NET-projekt som använder MTOM. Kontrollera att du använder följande WSDL-definition: `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Ersätt `localhost` med IP-adressen till den server där AEM Forms finns.

1. Skapa ett API-objekt för Document Security Client.

   * Skapa en `RightsManagementServiceClient` genom att använda dess standardkonstruktor.
   * Skapa en `RightsManagementServiceClient.Endpoint.Address` genom att använda `System.ServiceModel.EndpointAddress` konstruktor. Skicka ett strängvärde som anger WSDL till AEM Forms-tjänsten (till exempel `http://localhost:8080/soap/services/RightsManagementService?WSDL`.) Du behöver inte använda `lc_version` -attribut. Detta attribut används när du skapar en tjänstreferens.)
   * Skapa en `System.ServiceModel.BasicHttpBinding` genom att hämta värdet för `RightsManagementServiceClient.Endpoint.Binding` fält. Skicka returvärdet till `BasicHttpBinding`.
   * Ange `System.ServiceModel.BasicHttpBinding` objektets `MessageEncoding` fält till `WSMessageEncoding.Mtom`. Detta värde garanterar att MTOM används.
   * Aktivera grundläggande HTTP-autentisering genom att utföra följande åtgärder:

      * Tilldela AEM formuläranvändarnamn till fältet `RightsManagementServiceClient.ClientCredentials.UserName.UserName`.
      * Tilldela motsvarande lösenordsvärde till fältet `RightsManagementServiceClient.ClientCredentials.UserName.Password`.
      * Tilldela konstantvärdet `HttpClientCredentialType.Basic` till fältet `BasicHttpBindingSecurity.Transport.ClientCredentialType`.

   * Tilldela konstantvärdet `BasicHttpSecurityMode.TransportCredentialOnly` till fältet `BasicHttpBindingSecurity.Security.Mode`.

1. Ange vattenstämpelattribut.

   * Skapa en `WatermarkSpec` genom att anropa `WatermarkSpec` konstruktor.
   * Ange vattenstämpelns namn genom att tilldela ett strängvärde till `WatermarkSpec` objektets `name` datamedlem.
   * Ange vattenstämpeln `id` genom att tilldela ett strängvärde till `WatermarkSpec` objektets `id` datamedlem.
   * För varje vattenstämpelegenskap som ska anges skapar du en separat `MyMapOf_xsd_string_To_xsd_anyType_Item` -objekt.
   * Ange nyckelvärdet genom att tilldela värdet `MyMapOf_xsd_string_To_xsd_anyType_Item` objektets `key` datamedlem (till exempel `WaterBackCmd:OPACITY)`.
   * Ange värdet genom att tilldela ett värde till `MyMapOf_xsd_string_To_xsd_anyType_Item` objektets `value` datamedlem (till exempel `.25`).
   * Skapa en `MyArrayOf_xsd_anyType` -objekt. För varje `MyMapOf_xsd_string_To_xsd_anyType_Item` objekt, anropa `MyArrayOf_xsd_anyType` objektets `Add` -metod. Skicka `MyMapOf_xsd_string_To_xsd_anyType_Item` -objekt.
   * Tilldela `MyArrayOf_xsd_anyType` objekt till `WatermarkSpec` objektets `values` datamedlem.

1. Registrera vattenstämpeln.

   Registrera vattenstämpeln genom att anropa `RightsManagementServiceClient` objektets `registerWatermark` metoden och skicka `WatermarkSpec` objekt som representerar vattenstämpeln som ska registreras.

**Exempel på koder**

Följande snabbstarter innehåller kodexempel på hur du använder dokumentsäkerhetstjänsten:

* &quot;Snabbstart (MTOM): Skapa en vattenstämpel med hjälp av webbtjänstens API&quot;
* &quot;Snabbstart (SwaRef): Skapa en vattenstämpel med hjälp av webbtjänstens API&quot;

**Se även**

[Anropa AEM Forms med MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Anropa AEM Forms med SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Ändra vattenstämplar {#modifying-watermarks}

Du kan ändra en befintlig vattenstämpel med API:t för dokumentsäkerhet, Java eller webbtjänst. Om du vill ändra en befintlig vattenstämpel hämtar du den, ändrar dess attribut och uppdaterar den sedan på servern. Anta till exempel att du hämtar en vattenstämpel och ändrar dess opacitetsattribut. Du måste uppdatera vattenstämpeln innan ändringen börjar gälla.

När du ändrar en vattenstämpel påverkas framtida dokument med vattenstämpeln. Befintliga PDF-dokument som innehåller vattenstämpeln påverkas alltså inte.

>[!NOTE]
>
>Endast användare med administratörsbehörighet för dokumentsäkerhet kan ändra vattenstämplar. Det innebär att du måste ange en sådan användare när du definierar de anslutningsinställningar som krävs för att skapa ett klientobjekt för tjänsten Dokumentsäkerhet.

>[!NOTE]
>
>Mer information om tjänsten Dokumentsäkerhet finns i [Tjänstreferens för AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Sammanfattning av steg {#summary_of_steps-9}

Så här ändrar du en vattenstämpel:

1. Inkludera projektfiler.
1. Skapa ett API-objekt för Document Security Client.
1. Hämta vattenstämpeln som du vill ändra.
1. Ange vattenstämpelattribut.
1. Uppdatera vattenstämpeln.

**Inkludera projektfiler**

Inkludera nödvändiga filer i utvecklingsprojektet. Om du skapar ett klientprogram med Java inkluderar du de JAR-filer som behövs. Om du använder webbtjänster måste du inkludera proxyfilerna.

**Skapa ett API-objekt för Document Security Client**

Innan du programmässigt kan utföra en dokumentsäkerhetstjänståtgärd måste du skapa ett klientobjekt för dokumentsäkerhetstjänsten. Om du använder Java API skapar du en `DocumentSecurityClient` -objekt. Om du använder webbtjänstens API för dokumentsäkerhet skapar du en `DocumentSecurityServiceService` -objekt.

**Hämta vattenstämpeln som ska ändras**

Om du vill ändra en vattenstämpel måste du hämta en befintlig vattenstämpel. Du kan hämta en vattenstämpel genom att ange dess namn eller genom att ange dess identifierarvärde.

**Ange vattenstämpelattribut**

Om du vill ändra en befintlig vattenstämpel ändrar du värdet för ett eller flera vattenstämpelattribut. När du uppdaterar en vattenstämpel med hjälp av en webbtjänst måste du ange alla de attribut som ursprungligen var angivna, även om värdet inte ändras. Anta till exempel att följande vattenstämpelattribut har angetts: `WaterBackCmd:IS_USERID_ENABLED`, `WaterBackCmd:IS_CUSTOMTEXT_ENABLED`, `WaterBackCmd:OPACITY`och `WaterBackCmd:SRCTEXT`. Även om det enda attribut du vill ändra är `WaterBackCmd:OPACITY`måste du ange att de andra värdena är bra.

>[!NOTE]
>
>När du använder Java API för att ändra en vattenstämpel behöver du inte ange alla attribut. Ange vattenstämpelattributet som du vill ändra.

>[!NOTE]
>
>Mer information om attributnamnen för vattenstämplar finns i [Skapa vattenstämplar](protecting-documents-policies.md#creating-watermarks).

**Uppdatera vattenstämpeln**

När du har ändrat en vattenstämpels attribut måste du uppdatera vattenstämpeln.

**Se även**

[Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Skapa vattenstämplar](protecting-documents-policies.md#creating-watermarks)

### Ändra vattenstämplar med Java API {#modify-watermarks-using-the-java-api}

Ändra en vattenstämpel med API:t för dokumentsäkerhet (Java):

1. Inkludera projektfiler.

   Inkludera JAR-klientfiler, t.ex. adobe-rightsmanagement-client.jar, i Java-projektets klassökväg.

1. Skapa ett API-objekt för Document Security Client.

   * Skapa en `ServiceClientFactory` objekt som innehåller anslutningsegenskaper.
   * Skapa en `DocumentSecurityClient` genom att använda konstruktorn och skicka `ServiceClientFactory` -objekt.

1. Hämta vattenstämpeln som du vill ändra.

   Skapa en `WatermarkManager` genom att anropa `DocumentSecurityClient` objektets `getWatermarkManager` och skicka ett strängvärde som anger vattenstämpelns namn. Den här metoden returnerar en `Watermark` objekt som representerar den vattenstämpel som ska ändras.

1. Ange vattenstämpelattribut.

   Ange vattenstämpelns opacitetsattribut genom att anropa `Watermark` objektets `setOpacity` och skickar ett heltalsvärde som anger opacitetsnivån. Värdet 100 anger att vattenstämpeln är helt ogenomskinlig och värdet 0 anger att vattenstämpeln är helt genomskinlig.

   >[!NOTE]
   >
   >I det här exemplet ändras bara opacitetsattributet.

1. Uppdatera vattenstämpeln.

   * Uppdatera vattenstämpeln genom att aktivera `WatermarkManager` objektets `updateWatermark` och skicka `Watermark` objekt vars attribut har ändrats.

**Exempel på koder**

Exempel på kod som använder dokumentsäkerhetstjänsten finns i Snabbstart (SOAP-läge): Ändra en vattenstämpel med hjälp av Java API-avsnittet.

### Ändra vattenstämplar med webbtjänstens API {#modify-watermarks-using-the-web-service-api}

Ändra en vattenstämpel med hjälp av API:t för dokumentsäkerhet (webbtjänst):

1. Inkludera projektfiler.

   Skapa ett Microsoft .NET-projekt som använder MTOM. Kontrollera att du använder följande WSDL-definition: `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Ersätt `localhost` med IP-adressen till den server där AEM Forms finns.

1. Skapa ett API-objekt för Document Security Client.

   * Skapa en `DocumentSecurityServiceClient` genom att använda dess standardkonstruktor.
   * Skapa en `RightsManagementServiceClient.Endpoint.Address` genom att använda `System.ServiceModel.EndpointAddress` konstruktor. Skicka ett strängvärde som anger WSDL till AEM Forms-tjänsten (till exempel `http://localhost:8080/soap/services/DocumentSecurityService?WSDL`.) Du behöver inte använda `lc_version` -attribut. Detta attribut används när du skapar en tjänstreferens.)
   * Skapa en `System.ServiceModel.BasicHttpBinding` genom att hämta värdet för `DocumentSecurityServiceClient.Endpoint.Binding` fält. Skicka returvärdet till `BasicHttpBinding`.
   * Ange `System.ServiceModel.BasicHttpBinding` objektets `MessageEncoding` fält till `WSMessageEncoding.Mtom`. Detta värde garanterar att MTOM används.
   * Aktivera grundläggande HTTP-autentisering genom att utföra följande åtgärder:

      * Tilldela AEM formuläranvändarnamn till fältet `DocumentSecurityServiceClient.ClientCredentials.UserName.UserName`.
      * Tilldela motsvarande lösenordsvärde till fältet `DocumentSecurityServiceClient.ClientCredentials.UserName.Password`.
      * Tilldela konstantvärdet `HttpClientCredentialType.Basic` till fältet `BasicHttpBindingSecurity.Transport.ClientCredentialType`.

   * Tilldela konstantvärdet `BasicHttpSecurityMode.TransportCredentialOnly` till fältet `BasicHttpBindingSecurity.Security.Mode`.

1. Hämta vattenstämpeln som du vill ändra.

   Hämta vattenstämpeln som ska ändras genom att anropa `DocumentSecurityServiceClient` objektets `getWatermarkByName` -metod. Skicka ett strängvärde som anger vattenstämpelns namn. Den här metoden returnerar en `WatermarkSpec` objekt som representerar den vattenstämpel som ska ändras.

1. Ange vattenstämpelattribut.

   * För varje vattenstämpelegenskap som ska uppdateras skapar du en separat `MyMapOf_xsd_string_To_xsd_anyType_Item` -objekt.
   * Ange nyckelvärdet genom att tilldela värdet `MyMapOf_xsd_string_To_xsd_anyType_Item` objektets `key` datamedlem (till exempel `WaterBackCmd:OPACITY)`.
   * Ange värdet genom att tilldela ett värde till `MyMapOf_xsd_string_To_xsd_anyType_Item` objektets `value` datamedlem (till exempel `.50`).
   * Skapa en `MyArrayOf_xsd_anyType` -objekt. För varje `MyMapOf_xsd_string_To_xsd_anyType_Item` objekt, anropa `MyArrayOf_xsd_anyType` objektets `Add` -metod. Skicka `MyMapOf_xsd_string_To_xsd_anyType_Item` -objekt.
   * Tilldela `MyArrayOf_xsd_anyType` objekt till `WatermarkSpec` objektets `values` datamedlem.

1. Uppdatera vattenstämpeln.

   Uppdatera vattenstämpeln genom att aktivera `DocumentSecurityServiceClient` objektets `updateWatermark` metoden och skicka `WatermarkSpec` objekt som representerar den vattenstämpel som ska ändras.

**Exempel på koder**

Följande snabbstart innehåller kodexempel på hur du använder dokumentsäkerhetstjänsten:

* &quot;Snabbstart (MTOM): Ändra en vattenstämpel med hjälp av webbtjänstens API&quot;

## Söka efter händelser {#searching-for-events}

Tjänsten Rights Management spårar specifika åtgärder när de utförs, t.ex. att tillämpa en profil på ett dokument, öppna ett policyskyddat dokument och återkalla åtkomst till dokument. Händelsegranskning måste aktiveras för tjänsten Rights Management, annars spåras inte händelser.

Händelser faller inom en av följande kategorier:

* Administratörshändelser är åtgärder som är relaterade till en administratör, till exempel att skapa ett administratörskonto.
* Dokumenthändelser är åtgärder som är relaterade till ett dokument, t.ex. stängning av ett policyskyddat dokument.
* Policyhändelser är åtgärder som är relaterade till en profil, till exempel att skapa en profil.
* Tjänstehändelser är åtgärder som är relaterade till tjänsten Rights Management, t.ex. synkronisering med användarkatalogen.

Du kan söka efter specifika händelser genom att använda Java API:t för Rights Management eller webbtjänstens API. Genom att söka efter händelser kan du utföra åtgärder, till exempel skapa en loggfil med vissa händelser.

>[!NOTE]
>
>Mer information om tjänsten Rights Management finns i [Tjänstreferens för AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Sammanfattning av steg {#summary_of_steps-10}

Så här söker du efter en Rights Management-händelse:

1. Inkludera projektfiler.
1. Skapa ett Rights Management Client API-objekt.
1. Ange den händelse som du vill söka efter.
1. Sök efter händelsen.

**Inkludera projektfiler**

Inkludera nödvändiga filer i utvecklingsprojektet. Om du skapar ett klientprogram med Java inkluderar du de JAR-filer som behövs. Om du använder webbtjänster måste du inkludera proxyfilerna.

**Skapa ett Rights Management Client API-objekt**

Innan du programmässigt kan utföra en Rights Management-tjänståtgärd måste du skapa ett klientobjekt för tjänsten Rights Management. Om du använder Java API skapar du en `DocumentSecurityClient` -objekt. Om du använder Rights Management webbtjänste-API:t skapar du en `DocumentSecurityServiceService` -objekt.

**Ange vilka händelser som ska sökas efter**

Ange händelsen som du vill söka efter. Du kan till exempel söka efter händelsen create för principen, som inträffar när en ny princip skapas.

**Sök efter händelsen**

När du har angett vilken händelse du vill söka efter kan du söka efter händelsen med hjälp av Rights Management Java API eller Rights Management webbtjänstAPI.

**Se även**

[Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Söka efter händelser med Java API {#search-for-events-using-the-java-api}

Sök efter händelser med hjälp av Rights Management API (Java):

1. Inkludera projektfiler

   Inkludera JAR-klientfiler, som adobe-rightsmanagement-client.jar, i Java-projektets klassökväg.

1. Skapa ett Rights Management Client API-objekt

   Skapa en `DocumentSecurityClient` genom att använda konstruktorn och skicka ett `ServiceClientFactory` objekt som innehåller anslutningsegenskaper.

1. Ange vilka händelser som ska sökas efter

   * Skapa en `EventManager` genom att anropa `DocumentSecurityClient` objektets `getEventManager` -metod. Den här metoden returnerar en `EventManager` -objekt.
   * Skapa en `EventSearchFilter` genom att anropa dess konstruktor.
   * Ange händelsen som ska sökas igenom genom att anropa `EventSearchFilter` objektets `setEventCode` och skicka en statisk datamedlem som tillhör `EventManager` -klass som representerar händelsen som ska sökas efter. Om du till exempel vill söka efter principskapningshändelsen skickar du `EventManager.POLICY_CREATE_EVENT`.

   >[!NOTE]
   >
   >Du kan definiera ytterligare sökvillkor genom att anropa `EventSearchFilter` objektmetoder. Anropa till exempel `setUserName` för att ange en användare som är associerad med händelsen.

1. Sök efter händelsen

   Sök efter händelsen genom att anropa `EventManager` objektets `searchForEvents` metoden och skicka `EventSearchFilter` objekt som definierar sökvillkoren för händelsen. Den här metoden returnerar en array med `Event` objekt.

**Exempel på koder**

Följande snabbstarter innehåller kodexempel på hur du använder tjänsten Rights Management:

* &quot;Snabbstart (SOAP): Söka efter händelser med Java API&quot;

### Sök efter händelser med hjälp av webbtjänstens API {#search-for-events-using-the-web-service-api}

Sök efter händelser med hjälp av Rights Management API (webbtjänst):

1. Inkludera projektfiler

   Skapa ett Microsoft .NET-projekt som använder MTOM. Kontrollera att du använder följande WSDL-definition: `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Ersätt `localhost` med IP-adressen till den server där AEM Forms finns.

1. Skapa ett Rights Management Client API-objekt

   * Skapa en `DocumentSecurityServiceClient` genom att använda dess standardkonstruktor.
   * Skapa en `DocumentSecurityServiceClient.Endpoint.Address` genom att använda `System.ServiceModel.EndpointAddress` konstruktor. Skicka ett strängvärde som anger WSDL till AEM Forms-tjänsten (till exempel `http://localhost:8080/soap/services/RightsManagementService?WSDL`.) Du behöver inte använda `lc_version` -attribut. Detta attribut används när du skapar en tjänstreferens.)
   * Skapa en `System.ServiceModel.BasicHttpBinding` genom att hämta värdet för `DocumentSecurityServiceClient.Endpoint.Binding` fält. Skicka returvärdet till `BasicHttpBinding`.
   * Ange `System.ServiceModel.BasicHttpBinding` objektets `MessageEncoding` fält till `WSMessageEncoding.Mtom`. Detta värde garanterar att MTOM används.
   * Aktivera grundläggande HTTP-autentisering genom att utföra följande åtgärder:

      * Tilldela AEM formuläranvändarnamn till fältet `DocumentSecurityServiceClient.ClientCredentials.UserName.UserName`.
      * Tilldela motsvarande lösenordsvärde till fältet `DocumentSecurityServiceClient.ClientCredentials.UserName.Password`.
      * Tilldela konstantvärdet `HttpClientCredentialType.Basic` till fältet `BasicHttpBindingSecurity.Transport.ClientCredentialType`.

   * Tilldela konstantvärdet `BasicHttpSecurityMode.TransportCredentialOnly` till fältet `BasicHttpBindingSecurity.Security.Mode`.

1. Ange vilka händelser som ska sökas efter

   * Skapa en `EventSpec` genom att använda dess konstruktor.
   * Ange början på den tidsperiod under vilken händelsen inträffade genom att ange `EventSpec` objektets `firstTime.date` datamedlem med `DataTime` -instans som representerar början på datumintervallet när händelsen inträffade.
   * Tilldela värdet `true` till `EventSpec` objektets `firstTime.dateSpecified` datamedlem.
   * Ange slutet på den tidsperiod under vilken händelsen inträffade genom att ange `EventSpec` objektets `lastTime.date` datamedlem med `DataTime` -instans som representerar slutet på datumintervallet när händelsen inträffade.
   * Tilldela värdet `true` till `EventSpec` objektets `lastTime.dateSpecified` datamedlem.
   * Ange händelsen som du vill söka efter genom att tilldela ett strängvärde till `EventSpec` objektets `eventCode` datamedlem. I följande tabell visas de numeriska värden som du kan tilldela den här egenskapen:

   <table>
    <thead>
    <tr>
    <th><p>Händelsetyp</p></th>
    <th><p>Värde</p></th>
    </tr>
    </thead>
    <tbody>
    <tr>
    <td><p><code>ALL_EVENTS</code></p></td>
    <td><p>999</p></td>
    </tr>
    <tr>
    <td><p><code>USER_CHANGE_PASSWORD_EVENT</code></p></td>
    <td><p>1000</p></td>
    </tr>
    <tr>
    <td><p><code>USER_REGISTER_EVENT</code></p></td>
    <td><p>1001</p></td>
    </tr>
    <tr>
    <td><p><code>USER_PREREGISTER_EVENT</code></p></td>
    <td><p>1002</p></td>
    </tr>
    <tr>
    <td><p><code>USER_ACTIVATE_EVENT</code></p></td>
    <td><p>1003</p></td>
    </tr>
    <tr>
    <td><p><code>USER_DEACTIVATE_EVENT</code></p></td>
    <td><p>1004</p></td>
    </tr>
    <tr>
    <td><p><code>USER_AUTHENTICATE_EVENT</code></p></td>
    <td><p>1005</p></td>
    </tr>
    <tr>
    <td><p><code>USER_AUTHENTICATE_DENY_EVENT </code></p></td>
    <td><p>1006</p></td>
    </tr>
    <tr>
    <td><p><code>USER_ACCOUNT_LOCK_EVENT</code></p></td>
    <td><p>1007</p></td>
    </tr>
    <tr>
    <td><p><code>USER_DELETE_EVENT </code></p></td>
    <td><p>1008</p></td>
    </tr>
    <tr>
    <td><p><code>USER_UPDATE_PROFILE_EVENT </code></p></td>
    <td><p>1009</p></td>
    </tr>
    <tr>
    <td><p><code>DOCUMENT_VIEW_EVENT </code></p></td>
    <td><p>2000</p></td>
    </tr>
    <tr>
    <td><p><code>DOCUMENT_PRINT_LOW_EVENT </code></p></td>
    <td><p>2001</p></td>
    </tr>
    <tr>
    <td><p><code>DOCUMENT_PRINT_HIGH_EVENT </code></p></td>
    <td><p>2002</p></td>
    </tr>
    <tr>
    <td><p><code>DOCUMENT_SIGN_EVENT </code></p></td>
    <td><p>2003</p></td>
    </tr>
    <tr>
    <td><p><code>DOCUMENT_ADD_ANNOTATION_EVENT </code></p></td>
    <td><p>2004</p></td>
    </tr>
    <tr>
    <td><p><code>DOCUMENT_FORM_FILL_EVENT </code></p></td>
    <td><p>2005</p></td>
    </tr>
    <tr>
    <td><p><code>DOCUMENT_CLOSE_EVENT </code></p></td>
    <td><p>2006</p></td>
    </tr>
    <tr>
    <td><p><code>DOCUMENT_MODIFY_EVENT </code></p></td>
    <td><p>2007</p></td>
    </tr>
    <tr>
    <td><p><code>DOCUMENT_CHANGE_SECURITY_HANDLER_EVENT </code></p></td>
    <td><p>2008</p></td>
    </tr>
    <tr>
    <td><p><code>DOCUMENT_SWITCH_POLICY_EVENT </code></p></td>
    <td><p>2009</p></td>
    </tr>
    <tr>
    <td><p><code>DOCUMENT_REVOKE_EVENT </code></p></td>
    <td><p>2010</p></td>
    </tr>
    <tr>
    <td><p><code>$1</code></p></td>
    <td><p>2011</p></td>
    </tr>
    <tr>
    <td><p><code>DOCUMENT_SECURE_EVENT </code></p></td>
    <td><p>2012</p></td>
    </tr>
    <tr>
    <td><p><code>DOCUMENT_UNKNOWN_CLIENT_EVENT </code></p></td>
    <td><p>2013</p></td>
    </tr>
    <tr>
    <td><p><code>DOCUMENT_CHANGE_REVOKE_URL_EVENT </code></p></td>
    <td><p>2014</p></td>
    </tr>
    <tr>
    <td><p><code>POLICY_CHANGE_EVENT </code></p></td>
    <td><p>3000</p></td>
    </tr>
    <tr>
    <td><p><code>POLICY_ENABLE_EVENT </code></p></td>
    <td><p>3001</p></td>
    </tr>
    <tr>
    <td><p><code>POLICY_DISABLE_EVENT </code></p></td>
    <td><p>3002</p></td>
    </tr>
    <tr>
    <td><p><code>POLICY_CREATE_EVENT </code></p></td>
    <td><p>3003</p></td>
    </tr>
    <tr>
    <td><p><code>POLICY_DELETE_EVENT </code></p></td>
    <td><p>3004</p></td>
    </tr>
    <tr>
    <td><p><code>POLICY_CHANGE_OWNER_EVENT </code></p></td>
    <td><p>3005</p></td>
    </tr>
    <tr>
    <td><p><code>SERVER_CLIENT_SYNC_EVENT </code></p></td>
    <td><p>4000</p></td>
    </tr>
    <tr>
    <td><p><code>SERVER_SYNC_DIR_INFO_EVENT </code></p></td>
    <td><p>4001</p></td>
    </tr>
    <tr>
    <td><p><code>SERVER_SYNC_DIR_COMPLETE_EVENT </code></p></td>
    <td><p>4002</p></td>
    </tr>
    <tr>
    <td><p><code>SERVER_VERSION_MISMATCH_EVENT </code></p></td>
    <td><p>4003</p></td>
    </tr>
    <tr>
    <td><p><code>SERVER_CONFIG_CHANGE_EVENT </code></p></td>
    <td><p>4004</p></td>
    </tr>
    <tr>
    <td><p><code>SERVER_ENABLE_OFFLINE_ACCESS_EVENT </code></p></td>
    <td><p>4005</p></td>
    </tr>
    <tr>
    <td><p><code>ADMIN_ADD_EVENT </code></p></td>
    <td><p>5000</p></td>
    </tr>
    <tr>
    <td><p><code>ADMIN_DELETE_EVENT </code></p></td>
    <td><p>5001</p></td>
    </tr>
    <tr>
    <td><p><code>ADMIN_EDIT_EVENT </code></p></td>
    <td><p>5002</p></td>
    </tr>
    <tr>
    <td><p><code>ADMIN_ACTIVATE_EVENT </code></p></td>
    <td><p>5003</p></td>
    </tr>
    <tr>
    <td><p><code>ADMIN_DEACTIVATE_EVENT </code></p></td>
    <td><p>5004</p></td>
    </tr>
    <tr>
    <td><p><code>ERROR_DIRECTORY_SERVICE_EVENT </code></p></td>
    <td><p>6000</p></td>
    </tr>
    <tr>
    <td><p><code>CREATED_POLICYSET_EVENT</code></p></td>
    <td><p>7000</p></td>
    </tr>
    <tr>
    <td><p><code>DELETED_POLICYSET_EVENT</code></p></td>
    <td><p>7001</p></td>
    </tr>
    <tr>
    <td><p><code>MODIFIED_POLICYSET_EVENT</code></p></td>
    <td><p>7002</p></td>
    </tr>
    </tbody>
    </table>

1. Sök efter händelsen

   Sök efter händelsen genom att anropa `DocumentSecurityServiceClient` objektets `searchForEvents` metoden och skicka `EventSpec` -objekt som representerar händelsen som ska sökas efter och det maximala antalet resultat. Den här metoden returnerar en `MyArrayOf_xsd_anyType` samling där varje element är en `AuditSpec` -instans. Använda `AuditSpec` Du kan till exempel få information om händelsen, som när den inträffade. The `AuditSpec` -instansen innehåller en `timestamp` datamedlem som anger den här informationen.

**Exempel på koder**

Följande snabbstarter innehåller kodexempel på hur du använder tjänsten Rights Management:

* &quot;Snabbstart (MTOM): Söka efter händelser med hjälp av webbtjänstens API&quot;
* &quot;Snabbstart (SwaRef): Söka efter händelser med hjälp av webbtjänstens API&quot;

**Se även**

[Anropa AEM Forms med MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Anropa AEM Forms med SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Tillämpa profiler på Word-dokument {#applying-policies-to-word-documents}

Utöver PDF-dokument stöder Rights Management-tjänsten även andra dokumentformat som Microsoft Word-dokument (DOC-filer) och andra Microsoft Office-filformat. Du kan till exempel tillämpa en profil på ett Word-dokument för att skydda det. Genom att tillämpa en profil på ett Word-dokument begränsar du åtkomsten till dokumentet. Du kan inte tillämpa en profil på ett dokument om dokumentet redan är skyddat med en profil.

Du kan övervaka användningen av ett policyskyddat Word-dokument när du har distribuerat det. Det innebär att du kan se hur dokumentet används och vem som använder det. Du kan till exempel ta reda på när någon har öppnat dokumentet.

>[!NOTE]
>
>Mer information om tjänsten Dokumentsäkerhet finns i [Tjänstreferens för AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Sammanfattning av steg {#summary_of_steps-11}

Så här använder du en profil i ett Word-dokument:

1. Inkludera projektfiler.
1. Skapa ett API-objekt för Document Security Client.
1. Hämta ett Word-dokument som en profil tillämpas på.
1. Använd en befintlig profil i Word-dokumentet.
1. Spara det principskyddade Word-dokumentet.

**Inkludera projektfiler**

Inkludera nödvändiga filer i utvecklingsprojektet. Om du skapar ett klientprogram med Java inkluderar du de JAR-filer som behövs. Om du använder webbtjänster måste du inkludera proxyfilerna.

**Skapa ett API-objekt för dokumentsäkerhetsklienten**

Innan du programmässigt kan utföra en dokumentsäkerhetstjänståtgärd måste du skapa ett klientobjekt för dokumentsäkerhetstjänsten.

**Hämta ett Word-dokument**

Hämta ett Word-dokument om du vill tillämpa en profil. När du har tillämpat en profil på Word-dokumentet är användarna begränsade när de använder dokumentet. Om profilen t.ex. inte aktiverar dokumentet för att öppnas offline måste användarna vara online för att kunna öppna dokumentet.

**Tillämpa en befintlig profil på Word-dokumentet**

Om du vill tillämpa en profil på ett Word-dokument måste du referera till en befintlig princip och ange vilken principuppsättning som principen tillhör. Användaren som anger anslutningsegenskaperna måste ha tillgång till den angivna principen. Annars inträffar ett undantag.

**Spara Word-dokumentet**

När dokumentsäkerhetstjänsten har tillämpat en profil på ett Word-dokument kan du spara det principskyddade Word-dokumentet som en DOC-fil.

**Se även**

[Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Återkalla åtkomst till dokument](protecting-documents-policies.md#revoking-access-to-documents)

### Tillämpa en profil på ett Word-dokument med Java API {#apply-a-policy-to-a-word-document-using-the-java-api}

Tillämpa en profil på ett Word-dokument med hjälp av dokumentets säkerhets-API (Java):

1. Inkludera projektfiler.

   Inkludera JAR-klientfiler, som adobe-rightsmanagement-client.jar, i Java-projektets klassökväg.

1. Skapa ett API-objekt för Document Security Client.

   * Skapa en `ServiceClientFactory` objekt som innehåller anslutningsegenskaper.
   * Skapa en `DocumentSecurityClient` genom att använda konstruktorn och skicka `ServiceClientFactory` -objekt.

1. Hämta ett Word-dokument.

   * Skapa en `java.io.FileInputStream` som representerar Word-dokumentet genom att använda dess konstruktor och skicka ett strängvärde som anger platsen för Word-dokumentet.
   * Skapa en `com.adobe.idp.Document` genom att använda konstruktorn och skicka `java.io.FileInputStream` -objekt.

1. Använd en befintlig profil i Word-dokumentet.

   * Skapa en `DocumentManager` genom att anropa `DocumentSecurityClient` objektets `getDocumentManager` -metod.
   * Tillämpa en profil på Word-dokumentet genom att anropa `DocumentManager` objektets `protectDocument` och skicka följande värden:

      * The `com.adobe.idp.Document` som innehåller det Word-dokument som profilen tillämpas på.
      * Ett strängvärde som anger dokumentets namn.
      * Ett strängvärde som anger namnet på den principuppsättning som principen tillhör. Du kan ange en `null` det värde som resulterar i `MyPolicies` principuppsättning används.
      * Ett strängvärde som anger principnamnet.
      * Ett strängvärde som representerar namnet på användarhanterardomänen för den användare som är dokumentets utgivare. Det här parametervärdet är valfritt och kan vara null (om parametern är null måste nästa parametervärde vara null).
      * Ett strängvärde som representerar namnet på den kanoniska användaren av användarhanteraren som är dokumentets utgivare. Parametervärdet är valfritt och kan `null` (om den här parametern `null`måste det föregående parametervärdet vara `null`).
      * A `com.adobe.livecycle.rightsmanagement.Locale` som representerar det språkområde som används för att välja MS Office-mallen. Parametervärdet är valfritt och du kan ange `null`.

     The `protectDocument` returnerar en `RMSecureDocumentResult` som innehåller det principskyddade Word-dokumentet.

1. Spara Word-dokumentet.

   * Anropa `RMSecureDocumentResult` objektets `getProtectedDoc` för att hämta det principskyddade Word-dokumentet. Den här metoden returnerar en `com.adobe.idp.Document` -objekt.
   * Skapa en `java.io.File` och se till att filtillägget är DOC.
   * Anropa `com.adobe.idp.Document` objektets `copyToFile` metod för att kopiera innehållet i `Document` till filen (se till att du använder `Document` objekt som returneras av `getProtectedDoc` metod).

**Exempel på koder**

Följande snabbstart innehåller kodexempel på hur du använder dokumentsäkerhetstjänsten:

* &quot;Snabbstart (SOAP-läge): Tillämpa en princip på ett Word-dokument med Java API&quot;

### Tillämpa en profil på ett Word-dokument med hjälp av webbtjänstens API {#apply-a-policy-to-a-word-document-using-the-web-service-api}

Tillämpa en profil på ett Word-dokument med hjälp av API:t för dokumentsäkerhet (webbtjänsten):

1. Inkludera projektfiler.

   Skapa ett Microsoft .NET-projekt som använder MTOM. Kontrollera att du använder följande WSDL-definition: `http://localhost:8080/soap/services/DocumentSecurityService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Ersätt `localhost` med IP-adressen till den server där AEM Forms finns.

1. Skapa ett API-objekt för Document Security Client.

   * Skapa en `DocumentSecurityServiceClient` genom att använda dess standardkonstruktor.
   * Skapa en `DocumentSecurityServiceClient.Endpoint.Address` genom att använda `System.ServiceModel.EndpointAddress` konstruktor. Skicka ett strängvärde som anger WSDL till AEM Forms-tjänsten (till exempel `http://localhost:8080/soap/services/DocumentSecurityService?WSDL`.) Du behöver inte använda `lc_version` -attribut. Detta attribut används när du skapar en tjänstreferens.)
   * Skapa en `System.ServiceModel.BasicHttpBinding` genom att hämta värdet för `DocumentSecurityServiceClient.Endpoint.Binding` fält. Skicka returvärdet till `BasicHttpBinding`.
   * Ange `System.ServiceModel.BasicHttpBinding` objektets `MessageEncoding` fält till `WSMessageEncoding.Mtom`. Detta värde garanterar att MTOM används.
   * Aktivera grundläggande HTTP-autentisering genom att utföra följande åtgärder:

      * Tilldela AEM formuläranvändarnamn till fältet `DocumentSecurityServiceClient.ClientCredentials.UserName.UserName`.
      * Tilldela motsvarande lösenordsvärde till fältet `DocumentSecurityServiceClient.ClientCredentials.UserName.Password`.
      * Tilldela konstantvärdet `HttpClientCredentialType.Basic` till fältet `BasicHttpBindingSecurity.Transport.ClientCredentialType`.

   * Tilldela konstantvärdet `BasicHttpSecurityMode.TransportCredentialOnly` till fältet `BasicHttpBindingSecurity.Security.Mode`.

1. Hämta ett Word-dokument.

   * Skapa en `BLOB` genom att använda dess konstruktor. The `BLOB` -objektet används för att lagra ett Word-dokument som en profil tillämpas på.
   * Skapa en `System.IO.FileStream` genom att anropa dess konstruktor och skicka ett strängvärde som representerar filplatsen för Word-dokumentet och läget i vilket filen ska öppnas.
   * Skapa en bytearray som lagrar innehållet i `System.IO.FileStream` -objekt. Ta reda på bytearrayens storlek genom att hämta `System.IO.FileStream` objektets `Length` -egenskap.
   * Fylla i bytearrayen med strömdata genom att anropa `System.IO.FileStream` objektets `Read` -metod. Skicka bytearrayen, startpositionen och strömlängden som ska läsas.
   * Fyll i `BLOB` genom att tilldela `MTOM` fält med bytearrayens innehåll.

1. Använd en befintlig profil i Word-dokumentet.

   Tillämpa en profil på Word-dokumentet genom att anropa `DocumentSecurityServiceClient` objektets `protectDocument` och skicka följande värden:

   * The `BLOB` som innehåller det Word-dokument som profilen tillämpas på.
   * Ett strängvärde som anger dokumentets namn.
   * Ett strängvärde som anger namnet på den principuppsättning som principen tillhör. Du kan ange en `null` det värde som resulterar i `MyPolicies` principuppsättning används.
   * Ett strängvärde som anger principnamnet.
   * Ett strängvärde som representerar namnet på användarhanterardomänen för den användare som är dokumentets utgivare. Parametervärdet är valfritt och kan vara null (om parametern är null måste nästa parametervärde vara `null`).
   * Ett strängvärde som representerar namnet på den kanoniska användaren av användarhanteraren som är dokumentets utgivare. Det här parametervärdet är valfritt och kan vara null (om parametern är null måste det föregående parametervärdet vara `null`).
   * A `RMLocale` värde som anger språkvärdet (till exempel `RMLocale.en`).
   * En strängutdataparameter som används för att lagra principens identifierarvärde.
   * En strängutdataparameter som används för att lagra det principskyddade identifierarvärdet.
   * En strängutdataparameter som används för att lagra mime-typen (till exempel `application/doc`).

   The `protectDocument` returnerar en `BLOB` som innehåller det principskyddade Word-dokumentet.

1. Spara Word-dokumentet.

   * Skapa en `System.IO.FileStream` genom att anropa dess konstruktor och skicka ett strängvärde som representerar filplatsen för det principskyddade Word-dokumentet.
   * Skapa en bytearray som lagrar datainnehållet i `BLOB` objekt som returneras av `protectDocument` -metod. Fylla i bytearrayen genom att hämta värdet för `BLOB` objektets `MTOM` datamedlem.
   * Skapa en `System.IO.BinaryWriter` genom att anropa dess konstruktor och skicka `System.IO.FileStream` -objekt.
   * Skriv bytearrayens innehåll till en Word-fil genom att anropa `System.IO.BinaryWriter` objektets `Write` och skicka bytearrayen.

**Exempel på koder**

Följande snabbstart innehåller kodexempel på hur du använder dokumentsäkerhetstjänsten:

* &quot;Snabbstart (MTOM): Tillämpa en princip på ett Word-dokument med hjälp av webbtjänstens API &quot;

## Ta bort profiler från Word-dokument {#removing-policies-from-word-documents}

Du kan ta bort en profil från ett profilskyddat Word-dokument om du vill ta bort skyddet från dokumentet. Det vill säga om du inte längre vill att dokumentet ska skyddas av en profil. Om du vill uppdatera ett principskyddat Word-dokument med en nyare profil är det effektivare att byta profil i stället för att ta bort profilen och lägga till den uppdaterade profilen.

>[!NOTE]
>
>Mer information om tjänsten Dokumentsäkerhet finns i [Tjänstreferens för AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Sammanfattning av steg {#summary_of_steps-12}

Så här tar du bort en profil från ett profilskyddat Word-dokument:

1. Inkludera projektfiler
1. Skapa ett API-objekt för Document Security Client.
1. Hämta ett policyskyddat Word-dokument.
1. Ta bort profilen från Word-dokumentet.
1. Spara oskyddade Word-dokument.s

**Inkludera projektfiler**

Inkludera nödvändiga filer i utvecklingsprojektet. Om du skapar ett klientprogram med Java inkluderar du de JAR-filer som behövs. Om du använder webbtjänster måste du inkludera proxyfilerna.

**Skapa ett API-objekt för Document Security Client**

Skapa ett klientobjekt för tjänsten Dokumentsäkerhet innan du programmässigt utför en åtgärd.

**Hämta ett policyskyddat Word-dokument**

Hämta ett principskyddat Word-dokument om du vill ta bort en profil. Om du försöker ta bort en profil från ett Word-dokument som inte skyddas av en profil genereras ett undantagsfel.

**Ta bort profilen från Word-dokumentet**

Du kan ta bort en princip från ett principskyddat Word-dokument förutsatt att en administratör har angetts i anslutningsinställningarna. Annars måste profilen som används för att skydda ett dokument innehålla `SWITCH_POLICY` behörighet att ta bort en profil från ett Word-dokument. Dessutom måste den användare som anges i AEM Forms anslutningsinställningar också ha den behörigheten. Annars genereras ett undantag.

**Spara det oskyddade Word-dokumentet**

När dokumentskyddstjänsten har tagit bort en profil från ett Word-dokument kan du spara det oskyddade Word-dokumentet som en DOC-fil.

**Se även**

[Inkludera AEM Forms Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Tillämpa profiler på Word-dokument](protecting-documents-policies.md#applying-policies-to-word-documents)

### Ta bort en profil från ett Word-dokument med Java API {#remove-a-policy-from-a-word-document-using-the-java-api}

Ta bort en profil från ett principskyddat Word-dokument med hjälp av dokumentets säkerhets-API (Java):

1. Inkludera projektfiler

   Inkludera JAR-klientfiler, som adobe-rightsmanagement-client.jar, i Java-projektets klassökväg.

1. Skapa ett API-objekt för Document Security Client

   * Skapa en `ServiceClientFactory` objekt som innehåller anslutningsegenskaper.
   * Skapa en `RightsManagementClient` genom att använda konstruktorn och skicka `ServiceClientFactory` -objekt.

1. Hämta ett policyskyddat Word-dokument

   * Skapa en `java.io.FileInputStream` som representerar det principskyddade Word-dokumentet genom att använda dess konstruktor och skicka ett strängvärde som anger platsen för Word-dokumentet.
   * Skapa en `com.adobe.idp.Document` genom att använda konstruktorn och skicka `java.io.FileInputStream` -objekt.

1. Ta bort profilen från Word-dokumentet

   * Skapa en `DocumentManager` genom att anropa `RightsManagementClient` objektets `getDocumentManager` -metod.
   * Ta bort en profil från Word-dokumentet genom att anropa `DocumentManager` objektets `removeSecurity` metoden och skicka `com.adobe.idp.Document` som innehåller det principskyddade Word-dokumentet. Den här metoden returnerar en `com.adobe.idp.Document` objekt som innehåller ett oskyddat Word-dokument.

1. Spara det oskyddade Word-dokumentet

   * Skapa en `java.io.File` och se till att filtillägget är DOC.
   * Anropa `Document` objektets `copyToFile` metod för att kopiera innehållet i `Document` till filen (se till att du använder `Document` objekt som returneras av `removeSecurity` metod).

**Exempel på koder**

Följande snabbstart innehåller kodexempel på hur du använder dokumentsäkerhetstjänsten:

* &quot;Snabbstart (SOAP-läge): Ta bort en princip från ett Word-dokument med Java API &quot;

### Ta bort en profil från ett Word-dokument med hjälp av webbtjänstens API {#remove-a-policy-from-a-word-document-using-the-web-service-api}

Ta bort en profil från ett principskyddat Word-dokument med hjälp av API:t för dokumentsäkerhet (webbtjänsten):

1. Inkludera projektfiler

   Skapa ett Microsoft .NET-projekt som använder MTOM. Kontrollera att du använder följande WSDL-definition: `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Ersätt `localhost` med IP-adressen till den server där AEM Forms finns.

1. Skapa ett API-objekt för Document Security Client

   * Skapa en `RightsManagementServiceClient` genom att använda dess standardkonstruktor.
   * Skapa en `RightsManagementServiceClient.Endpoint.Address` genom att använda `System.ServiceModel.EndpointAddress` konstruktor. Skicka ett strängvärde som anger WSDL till AEM Forms-tjänsten (till exempel `http://localhost:8080/soap/services/RightsManagementService?WSDL`.) Du behöver inte använda `lc_version` -attribut. Detta attribut används när du skapar en tjänstreferens.)
   * Skapa en `System.ServiceModel.BasicHttpBinding` genom att hämta värdet för `RightsManagementServiceClient.Endpoint.Binding` fält. Skicka returvärdet till `BasicHttpBinding`.
   * Ange `System.ServiceModel.BasicHttpBinding` objektets `MessageEncoding` fält till `WSMessageEncoding.Mtom`. Detta värde garanterar att MTOM används.
   * Aktivera grundläggande HTTP-autentisering genom att utföra följande åtgärder:

      * Tilldela AEM formuläranvändarnamn till fältet `RightsManagementServiceClient.ClientCredentials.UserName.UserName`.
      * Tilldela motsvarande lösenordsvärde till fältet `RightsManagementServiceClient.ClientCredentials.UserName.Password`.
      * Tilldela konstantvärdet `HttpClientCredentialType.Basic` till fältet `BasicHttpBindingSecurity.Transport.ClientCredentialType`.

   * Tilldela konstantvärdet `BasicHttpSecurityMode.TransportCredentialOnly` till fältet `BasicHttpBindingSecurity.Security.Mode`.

1. Hämta ett policyskyddat Word-dokument

   * Skapa en `BLOB` genom att använda dess konstruktor. The `BLOB` -objektet används för att lagra det principskyddade Word-dokumentet som profilen tas bort från.
   * Skapa en `System.IO.FileStream` genom att anropa dess konstruktor och skicka ett strängvärde som representerar filplatsen för Word-dokumentet och läget i vilket filen ska öppnas.
   * Skapa en bytearray som lagrar innehållet i `System.IO.FileStream` -objekt. Du kan bestämma storleken på bytearrayen genom att hämta `System.IO.FileStream` objektets `Length` -egenskap.
   * Fylla i bytearrayen med strömdata genom att anropa `System.IO.FileStream` objektets `Read` och skickar bytearrayen, startpositionen och den flödeslängd som ska läsas.
   * Fyll i `BLOB` genom att tilldela `MTOM` fält med bytearrayens innehåll.

1. Ta bort profilen från Word-dokumentet

   Ta bort profilen från Word-dokumentet genom att anropa `RightsManagementServiceClient` objektets `removePolicySecurity` metoden och skicka `BLOB` som innehåller det principskyddade Word-dokumentet. Den här metoden returnerar en `BLOB` objekt som innehåller ett oskyddat Word-dokument.

1. Spara det oskyddade Word-dokumentet

   * Skapa en `System.IO.FileStream` genom att anropa dess konstruktor och skicka ett strängvärde som representerar filplatsen för det oskyddade Word-dokumentet.
   * Skapa en bytearray som lagrar datainnehållet i `BLOB` objekt som returneras av `removePolicySecurity` -metod. Fylla i bytearrayen genom att hämta värdet för `BLOB` objektets `MTOM` fält.
   * Skapa en `System.IO.BinaryWriter` genom att anropa dess konstruktor och skicka `System.IO.FileStream` -objekt.

**Exempel på koder**

Följande snabbstart innehåller kodexempel på hur du använder dokumentsäkerhetstjänsten:

* &quot;Snabbstart (MTOM): Ta bort en princip från ett Word-dokument med hjälp av webbtjänstens API&quot;

**Se även**

[Anropa AEM Forms med MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
