---
title: Anpassning på serversidan
seo-title: Anpassning på serversidan
description: Anpassa serversidan i AEM Communities
seo-description: Anpassa serversidan i AEM Communities
uuid: 5e9bc6bf-69dc-414c-a4bd-74a104d7bd8f
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: df5416ec-5c63-481b-99ed-9e5a91df2432
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Anpassning på serversidan {#server-side-customization}

| **[⇐ - funktioner](essentials.md)** | **[Anpassning på klientsidan](client-customize.md)** |
|---|---|
|  | **[SCF Handlebars Helpers](handlebars-helpers.md)** |

## Java API:er {#java-apis}

>[!NOTE]
>
>Platsen för paket-API:er kan ändras när du uppgraderar från en större version till nästa.

### SocialComponent-gränssnitt {#socialcomponent-interface}

SocialComponents är POJO som representerar en resurs för en AEM Communities-funktion. Helst representerar varje SocialComponent en specifik resourceType med exponerade GETters som tillhandahåller data till klienten så att resursen representeras korrekt. All affärslogik och visningslogik är inkapslade i SocialComponent, inklusive webbplatsbesökarens sessionsinformation, om det behövs.

Gränssnittet definierar en grundläggande uppsättning GETters som krävs för att representera en resurs. Viktigt är att det i gränssnittet finns metoder för Map&lt;String, Object> getAsMap() och String toJSONString() som krävs för att återge Handlebars-mallar och visa GET JSON-slutpunkter för resurser.

Alla SocialComponent-klasser måste implementera gränssnittet `com.adobe.cq.social.scf.SocialComponent`

### SocialCollectionComponent-gränssnitt {#socialcollectioncomponent-interface}

Gränssnittet SocialCollectionComponent utökar gränssnittet SocialComponent för att bättre representera resurser som är samlingar av andra resurser.

Alla klasser i SocialCollectionComponent måste implementera gränssnittet com.adobe.cq.social.scf.SocialCollectionComponent

### SocialComponentFactory-gränssnitt {#socialcomponentfactory-interface}

En SocialComponentFactory (fabrik) registrerar en SocialComponent med ramverket. Fabriken tillhandahåller ett sätt att meddela ramverket vilka SocialComponents som är tillgängliga för en viss resourceType och deras prioritetsranknings&amp;ast. när flera SocialComponents identifieras.

En SocialComponentFactory ansvarar för att skapa en instans av den valda SocialComponent, vilket gör det möjligt att mata in alla beroenden som behövs av SocialComponent från fabriken med hjälp av DI-metoder.

En SocialComponentFactory är en OSGi-tjänst och har tillgång till andra OSGi-tjänster som kan skickas till SocialComponent via en konstruktor.

Alla SocialComponentFactory-klasser måste implementera gränssnittet `com.adobe.cq.social.scf.SocialComponentFactory`

En implementering av metoden SocialComponentFactory.getPriority() ska returnera det högsta värdet för att fabriken ska användas för den angivna resourceType som returneras av getResourceType().

### SocialComponentFactoryManager-gränssnitt {#socialcomponentfactorymanager-interface}

SocialComponentFactoryManager (hanterare) hanterar alla SocialComponents som är registrerade i ramverket och ansvarar för att välja den SocialComponentFactory som ska användas för en given resurs (resourceType). Om inga fabriker har registrerats för en viss resourceType returnerar hanteraren en fabrik med den närmast överordnade typen för den angivna resursen.

En SocialComponentFactoryManager är en OSGi-tjänst och har tillgång till andra OSGi-tjänster som kan skickas till SocialComponent via en konstruktor.

En referens till OSGi-tjänsten erhålls genom att anropa `com.adobe.cq.social.scf.SocialComponentFactoryManager`

### HTTP API - POST-begäranden {#http-api-post-requests}

#### Klassen PostOperation {#postoperation-class}

HTTP API POST-slutpunkterna är PostOperation-klasser som definieras genom implementering av `SlingPostOperation`gränssnittet (paket `org.apache.sling.servlets.post`).

Slutpunktsimplementeringen anger `PostOperation`ett värde `sling.post.operation`som åtgärden ska svara på. Alla POST-begäranden med en:operation-parameter inställd på det värdet delegeras till den här implementeringsklassen.

Den `PostOperation`anropar den `SocialOperation`som utför de åtgärder som krävs för åtgärden.

Användaren `PostOperation`får resultatet från `SocialOperation`och returnerar det rätta svaret till klienten.

#### Klassen SocialOperation {#socialoperation-class}

Varje `SocialOperation`slutpunkt utökar klassen AbstractSocialOperation och åsidosätter metoden `performOperation().`Den här metoden utför alla åtgärder som krävs för att slutföra åtgärden och returnerar en `SocialOperationResult`eller annan utlöser en `OperationException`åtgärd. I så fall returneras en HTTP-felstatus med ett meddelande i stället för den vanliga JSON-svaret eller HTTP-statuskoden om det är tillgängligt.

Utökning `AbstractSocialOperation`gör det möjligt att återanvända `SocialComponents`för att skicka JSON-svar.

#### Klassen SocialOperationResult {#socialoperationresult-class}

Klassen `SocialOperationResult`returneras som resultatet av `SocialOperation`och består av en `SocialComponent`HTTP-statuskod och ett HTTP-statusmeddelande.

Resursen `SocialComponent`representerar den resurs som påverkades av åtgärden.

För en Skapa-åtgärd, `SocialComponent`som ingår i `SocialOperationResult`representerar den resurs som just har skapats och för en Update-åtgärd representerar den resursen som ändrades av åtgärden. Ingen `SocialComponent`returneras för en Delete-åtgärd.

De HTTP-statuskoder som används är

* 2010 för Create-åtgärder
* 200 för uppdateringsåtgärder
* 204 för raderingsåtgärder

#### Klassen OperationException {#operationexception-class}

Ett fel `OperationExcepton`kan genereras när en åtgärd utförs om begäran inte är giltig eller om något annat fel inträffar, till exempel interna fel, felaktiga parametervärden, felaktiga behörigheter osv. En `OperationException`består av en HTTP-statuskod och ett felmeddelande som returneras till klienten som svar på `PostOperatoin`.

#### Klassen OperationService {#operationservice-class}

Ramverket för sociala komponenter rekommenderar att den affärslogik som ansvarar för att utföra åtgärden inte implementeras i `SocialOperation`klassen, utan istället delegeras till en OSGi-tjänst. Med en OSGi-tjänst för affärslogik kan en `SocialComponent`som agerar på en `SocialOperation`slutpunkt integreras med annan kod och ha en annan affärslogik.

Alla `OperationService`klasser utökas `AbstractOperationService`så att ytterligare tillägg kan anslutas till den åtgärd som utförs. Varje åtgärd i tjänsten representeras av en `SocialOperation`klass. Du kan anropa `OperationExtensions`klassen under körning genom att anropa metoderna

* `performBeforeActions()`
Tillåter förkontroller/förbehandling och validering
* `performAfterActions()`
Möjliggör ytterligare ändringar av resurser eller anrop av anpassade händelser, arbetsflöden osv.

#### Klassen OperationExtension {#operationextension-class}

`OperationExtension`klasser är anpassade koddelar som kan injiceras i en åtgärd som gör det möjligt att anpassa operationer efter affärsbehov. Konsumenterna av komponenten kan dynamiskt och stegvis lägga till funktioner i komponenten. Med hjälp av tilläggs-/krokmönstret kan utvecklare fokusera enbart på själva tilläggen och ta bort behovet av att kopiera och åsidosätta hela åtgärder och komponenter.

## Exempelkod {#sample-code}

Exempelkod finns i [Adobe Marketing Cloud GitHub](https://github.com/Adobe-Marketing-Cloud) -databasen. Sök efter projekt som har prefix med antingen `aem-communities` eller `aem-scf`.

## Bästa praxis {#best-practices}

Se avsnittet [Kodningsriktlinjer](code-guide.md) för olika riktlinjer och bästa praxis för utvecklare av AEM Communities.

Se även [Storage Resource Provider (SRP) för UGC](srp.md) om du vill veta mer om hur du får åtkomst till användargenererat innehåll.

| **[⇐ - funktioner](essentials.md)** | **[Anpassning på klientsidan](client-customize.md)** |
|---|---|
|  | **[SCF Handlebars Helpers](handlebars-helpers.md)** |

