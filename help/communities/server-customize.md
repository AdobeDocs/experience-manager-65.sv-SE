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
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '896'
ht-degree: 0%

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

En SocialComponentFactory (fabrik) registrerar en SocialComponent med ramverket. Fabriken tillhandahåller ett sätt att meddela ramverket vilka SocialComponents som är tillgängliga för en given resourceType och deras prioritetsordning när flera SocialComponents identifieras.

En SocialComponentFactory ansvarar för att skapa en instans av den valda SocialComponent, vilket gör det möjligt att mata in alla beroenden som behövs av SocialComponent från fabriken med hjälp av DI-metoder.

En SocialComponentFactory är en OSGi-tjänst och har tillgång till andra OSGi-tjänster som kan skickas till SocialComponent via en konstruktor.

Alla SocialComponentFactory-klasser måste implementera gränssnittet `com.adobe.cq.social.scf.SocialComponentFactory`

En implementering av metoden SocialComponentFactory.getPriority() ska returnera det högsta värdet för att fabriken ska användas för den angivna resourceType som returneras av getResourceType().

### SocialComponentFactoryManager-gränssnitt {#socialcomponentfactorymanager-interface}

SocialComponentFactoryManager (hanterare) hanterar alla SocialComponents som är registrerade i ramverket och ansvarar för att välja den SocialComponentFactory som ska användas för en given resurs (resourceType). Om inga fabriker har registrerats för en viss resourceType returnerar hanteraren en fabrik med den närmast överordnade typen för den angivna resursen.

En SocialComponentFactoryManager är en OSGi-tjänst och har tillgång till andra OSGi-tjänster som kan skickas till SocialComponent via en konstruktor.

En referens till OSGi-tjänsten hämtas genom att anropa `com.adobe.cq.social.scf.SocialComponentFactoryManager`

### HTTP API - POST-begäranden {#http-api-post-requests}

#### Klassen PostOperation {#postoperation-class}

Slutpunkterna för HTTP API-POSTEN är PostOperation-klasser som definieras genom implementering av gränssnittet `SlingPostOperation` (paketet `org.apache.sling.servlets.post`).

Slutpunktsimplementeringen `PostOperation` ställer in `sling.post.operation` på ett värde som åtgärden ska svara på. Alla POST-begäranden med en:operation-parameter inställd på det värdet delegeras till den här implementeringsklassen.

`PostOperation` anropar `SocialOperation` som utför de åtgärder som krävs för åtgärden.

`PostOperation` tar emot resultatet från `SocialOperation` och returnerar rätt svar till klienten.

#### Klassen SocialOperation {#socialoperation-class}

Varje `SocialOperation`-slutpunkt utökar klassen AbstractSocialOperation och åsidosätter metoden `performOperation()`. Den här metoden utför alla åtgärder som krävs för att slutföra åtgärden och returnerar en `SocialOperationResult` eller utlöser en `OperationException`. I så fall returneras en HTTP-felstatus med ett meddelande, om tillgängligt, i stället för den vanliga JSON-svarskoden eller HTTP-statuskoden för lyckade åtgärder.

Om du utökar `AbstractSocialOperation` kan du återanvända `SocialComponents` för att skicka JSON-svar.

#### Klassen SocialOperationResult {#socialoperationresult-class}

Klassen `SocialOperationResult` returneras som ett resultat av `SocialOperation` och består av `SocialComponent`, HTTP-statuskoden och HTTP-statusmeddelandet.

`SocialComponent` representerar den resurs som påverkades av åtgärden.

För en Skapa-åtgärd representerar `SocialComponent` som ingår i `SocialOperationResult` den resurs som just har skapats och för en Update-åtgärd representerar den resursen som ändrades av åtgärden. Ingen `SocialComponent` returneras för en Delete-åtgärd.

De HTTP-statuskoder som används är:

* 2010 för Create-åtgärder
* 200 för uppdateringsåtgärder
* 204 för raderingsåtgärder

#### OperationException-klass {#operationexception-class}

Ett `OperationExcepton`-fel kan genereras när en åtgärd utförs om begäran inte är giltig eller om något annat fel inträffar, till exempel interna fel, felaktiga parametervärden, felaktiga behörigheter osv. En `OperationException` består av en HTTP-statuskod och ett felmeddelande, som returneras till klienten som svar på `PostOperatoin`.

#### OperationService-klass {#operationservice-class}

Ramverket för sociala komponenter rekommenderar att den affärslogik som ansvarar för att utföra åtgärden inte implementeras i klassen `SocialOperation`, utan istället delegeras till en OSGi-tjänst. Om du använder en OSGi-tjänst för affärslogik kan en `SocialComponent` som hanteras av en `SocialOperation`-slutpunkt integreras med annan kod och ha en annan affärslogik.

Alla `OperationService`-klasser utökar `AbstractOperationService` och tillåter ytterligare tillägg som kan knytas till den åtgärd som utförs. Varje åtgärd i tjänsten representeras av en `SocialOperation`-klass. Klassen `OperationExtensions` kan anropas under körningen genom att anropa metoderna

* `performBeforeActions()`

   Tillåter förkontroller/förbehandling och validering
* `performAfterActions()`

   Möjliggör ytterligare ändringar av resurser eller anrop av anpassade händelser, arbetsflöden osv.

#### Klassen OperationExtension {#operationextension-class}

`OperationExtension` klasser är anpassade koddelar som kan injiceras i en åtgärd som gör det möjligt att anpassa operationer efter affärsbehov. Konsumenterna av komponenten kan dynamiskt och stegvis lägga till funktioner i komponenten. Med hjälp av tilläggs-/krokmönstret kan utvecklare fokusera enbart på själva tilläggen och ta bort behovet av att kopiera och åsidosätta hela åtgärder och komponenter.

## Exempelkod {#sample-code}

Exempelkod finns i [Adobe Marketing Cloud GitHub](https://github.com/Adobe-Marketing-Cloud)-databasen. Sök efter projekt som har prefixet `aem-communities` eller `aem-scf`.

## Bästa praxis {#best-practices}

I [riktlinjerna för kodning](code-guide.md) finns olika riktlinjer för kodning och metodtips för AEM Communities-utvecklare.

Se även [Storage Resource Provider (SRP) för UGC](srp.md) om du vill veta mer om hur du får åtkomst till användargenererat innehåll.

| **[⇐ - funktioner](essentials.md)** | **[Anpassning på klientsidan](client-customize.md)** |
|---|---|
|  | **[SCF Handlebars Helpers](handlebars-helpers.md)** |

