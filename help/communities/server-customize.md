---
title: Anpassning på serversidan
seo-title: Server-side Customization
description: Anpassa serversidan i AEM Communities
seo-description: Customizing server-side in AEM Communities
uuid: 5e9bc6bf-69dc-414c-a4bd-74a104d7bd8f
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: df5416ec-5c63-481b-99ed-9e5a91df2432
exl-id: 190735bc-1909-4b92-ba4f-a221c0cd5be7
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '889'
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

Gränssnittet definierar en grundläggande uppsättning GETters som krävs för att representera en resurs. Viktigt är att gränssnittet anger kartan&lt;string object=&quot;&quot;> metoderna getAsMap() och String toJSONString() som behövs för att återge Handlebars-mallar och visa GET JSON-slutpunkter för resurser.

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

En referens till OSGi-tjänsten erhålls genom att anropa `com.adobe.cq.social.scf.SocialComponentFactoryManager`

### HTTP API - POSTER {#http-api-post-requests}

#### Klassen PostOperation {#postoperation-class}

Slutpunkterna för HTTP API-POSTEN är PostOperation-klasser som definieras genom implementering av `SlingPostOperation` interface (package `org.apache.sling.servlets.post`).

The `PostOperation` slutpunktsimplementeringsuppsättningar `sling.post.operation` till ett värde som åtgärden ska svara på. Alla POST-begäranden med en:operation-parameter inställd på det värdet delegeras till den här implementeringsklassen.

The `PostOperation` anropar `SocialOperation` som utför de åtgärder som krävs för åtgärden.

The `PostOperation` tar emot resultatet från `SocialOperation` och returnerar rätt svar till klienten.

#### Klassen SocialOperation {#socialoperation-class}

Varje `SocialOperation` slutpunkten utökar klassen AbstractSocialOperation och åsidosätter metoden `performOperation()`. Den här metoden utför alla åtgärder som behövs för att slutföra åtgärden och returnera en `SocialOperationResult` eller i annat fall kasta en `OperationException`, i så fall returneras en HTTP-felstatus med ett meddelande, om ett sådant finns, i stället för den vanliga JSON-svarskoden eller HTTP-statuskoden för lyckade åtgärder.

Utöka `AbstractSocialOperation` gör det möjligt att återanvända `SocialComponents` för att skicka JSON-svar.

#### Klassen SocialOperationResult {#socialoperationresult-class}

The `SocialOperationResult` klassen returneras som resultatet av `SocialOperation` och består av en `SocialComponent`, HTTP-statuskod och HTTP-statusmeddelande.

The `SocialComponent` representerar den resurs som påverkades av åtgärden.

För en Skapa-åtgärd finns följande i `SocialComponent` ingår i `SocialOperationResult` representerar den resurs som just har skapats och för en Update-åtgärd representerar den resursen som ändrades av åtgärden. Nej `SocialComponent` returneras för en Delete-åtgärd.

De HTTP-statuskoder som används är:

* 2010 för Create-åtgärder
* 200 för uppdateringsåtgärder
* 204 för raderingsåtgärder

#### Klassen OperationException {#operationexception-class}

An `OperationExcepton` kan genereras när en åtgärd utförs om begäran inte är giltig eller om något annat fel inträffar, t.ex. interna fel, felaktiga parametervärden, felaktiga behörigheter osv. An `OperationException` består av en HTTP-statuskod och ett felmeddelande som returneras till klienten som svar på `PostOperatoin`.

#### Klassen OperationService {#operationservice-class}

Ramverket för den sociala komponenten rekommenderar att den affärslogik som ansvarar för att utföra åtgärden inte implementeras i `SocialOperation` i stället delegeras till en OSGi-tjänst. Med en OSGi-tjänst för affärslogik kan man `SocialComponent`, som `SocialOperation` -slutpunkt, som ska integreras med annan kod och ha olika affärslogik.

Alla `OperationService` klasser utöka `AbstractOperationService`, vilket tillåter ytterligare tillägg som kan knytas till den åtgärd som utförs. Varje åtgärd i tjänsten representeras av en `SocialOperation` klassen. The `OperationExtensions` klassen kan anropas under körning genom att anropa metoderna

* `performBeforeActions()`

   Tillåter förkontroller/förbehandling och validering
* `performAfterActions()`

   Möjliggör ytterligare ändringar av resurser eller anrop av anpassade händelser, arbetsflöden osv.

#### Klassen OperationExtension {#operationextension-class}

`OperationExtension` klasser är anpassade koddelar som kan injiceras i en åtgärd som gör det möjligt att anpassa operationer efter affärsbehov. Konsumenterna av komponenten kan dynamiskt och stegvis lägga till funktioner i komponenten. Med hjälp av tilläggs-/krokmönstret kan utvecklare fokusera enbart på själva tilläggen och ta bort behovet av att kopiera och åsidosätta hela åtgärder och komponenter.

## Exempelkod {#sample-code}

Exempelkod finns i [Adobe Marketing Cloud GitHub](https://github.com/Adobe-Marketing-Cloud) databas. Sök efter projekt med antingen `aem-communities` eller `aem-scf`.

## Bästa praxis {#best-practices}

Visa [Riktlinjer för kodning](code-guide.md) för olika riktlinjer för kodning och metodtips för AEM Communities-utvecklare.

Se även [Lagringsresursleverantör (SRP) för UGC](srp.md) om du vill veta mer om hur du får åtkomst till användargenererat innehåll.

| **[⇐ - funktioner](essentials.md)** | **[Anpassning på klientsidan](client-customize.md)** |
|---|---|
|  | **[SCF Handlebars Helpers](handlebars-helpers.md)** |
