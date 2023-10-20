---
title: Anpassning på serversidan
description: Läs om hur anpassning på serversidan i Adobe Experience Manager Communities.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 190735bc-1909-4b92-ba4f-a221c0cd5be7
source-git-commit: f03d0ab9d0f491441378e16e1590d33651f064b5
workflow-type: tm+mt
source-wordcount: '886'
ht-degree: 0%

---

# Anpassning på serversidan {#server-side-customization}

| **[⇐ - funktioner](essentials.md)** | **[Anpassning på klientsidan](client-customize.md)** |
|---|---|
|   | **[SCF Handlebars Helpers](handlebars-helpers.md)** |

## Java™-API:er {#java-apis}

>[!NOTE]
>
>Platsen för paket-API:er kan ändras när du uppgraderar från en större version till nästa.

### SocialComponent-gränssnitt {#socialcomponent-interface}

SocialComponents är POJO som representerar en resurs för en AEM Communities-funktion. Helst representerar varje SocialComponent en specifik resourceType med exponerade GETters som tillhandahåller data till klienten så att resursen representeras korrekt. All affärslogik och vylogik är inkapslad i SocialComponent, inklusive webbplatsbesökarens sessionsinformation, om det behövs.

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

En implementering av metoden SocialComponentFactory.getPriority() ska returnera det högsta värdet för fabriken som ska användas för den angivna resourceType som returneras av getResourceType().

### SocialComponentFactoryManager-gränssnitt {#socialcomponentfactorymanager-interface}

SocialComponentFactoryManager (hanterare) hanterar alla SocialComponents som är registrerade i ramverket och ansvarar för att välja den SocialComponentFactory som ska användas för en given resurs (resourceType). Om inga fabriker har registrerats för en viss resourceType returnerar hanteraren en fabrik med den närmast överordnade typen för den angivna resursen.

En SocialComponentFactoryManager är en OSGi-tjänst och har tillgång till andra OSGi-tjänster som kan skickas till SocialComponent via en konstruktor.

En referens till OSGi-tjänsten erhålls genom att anropa `com.adobe.cq.social.scf.SocialComponentFactoryManager`

### HTTP API - POST-begäranden {#http-api-post-requests}

#### Klassen PostOperation {#postoperation-class}

Slutpunkterna för HTTP API-POSTEN är PostOperation-klasser som definieras genom implementering av `SlingPostOperation` interface (package `org.apache.sling.servlets.post`).

The `PostOperation` implementeringsuppsättningar för slutpunkter `sling.post.operation` till ett värde som åtgärden svarar på. Alla POST-begäranden med en:operation-parameter inställd på det värdet delegeras till den här implementeringsklassen.

The `PostOperation` anropar `SocialOperation` som utför de åtgärder som krävs för åtgärden.

The `PostOperation` tar emot resultatet från `SocialOperation` och returnerar rätt svar till klienten.

#### Klassen SocialOperation {#socialoperation-class}

Varje `SocialOperation` slutpunkten utökar klassen AbstractSocialOperation och åsidosätter metoden `performOperation()`. Den här metoden utför alla åtgärder som behövs för att slutföra åtgärden och returnera en `SocialOperationResult` eller i annat fall kasta `OperationException`. I så fall returneras en HTTP-felstatus med ett meddelande, om ett sådant finns, i stället för den vanliga JSON-svarskoden eller HTTP-statuskoden för lyckade åtgärder.

Utöka `AbstractSocialOperation` möjliggör återanvändning av `SocialComponents` för att skicka JSON-svar.

#### Klassen SocialOperationResult {#socialoperationresult-class}

The `SocialOperationResult` klassen returneras som resultatet av `SocialOperation` och består av en `SocialComponent`, HTTP-statuskod och HTTP-statusmeddelande.

The `SocialComponent` representerar den resurs som påverkades av åtgärden.

För en Skapa-åtgärd finns följande i `SocialComponent` som ingår i `SocialOperationResult` representerar den skapade resursen och för en Update-åtgärd representerar den resursen som ändrades av åtgärden. Nej `SocialComponent` returneras för en Delete-åtgärd.

De HTTP-statuskoder som används är:

* 2010 för Create-åtgärder
* 200 för uppdateringsåtgärder
* 204 för raderingsåtgärder

#### Klassen OperationException {#operationexception-class}

An `OperationExcepton` genereras när en åtgärd utförs om begäran inte är giltig eller om något annat fel inträffar. Exempel: interna fel, felaktiga parametervärden eller felaktiga behörigheter. An `OperationException` består av en HTTP-statuskod och ett felmeddelande, som returneras till klienten som svar på `PostOperatoin`.

#### Klassen OperationService {#operationservice-class}

Ramverket för den sociala komponenten rekommenderar att den affärslogik som ansvarar för att utföra åtgärden inte implementeras i `SocialOperation` i stället delegeras till en OSGi-tjänst. Med en OSGi-tjänst för affärslogik kan man `SocialComponent`, som `SocialOperation` -slutpunkt, som ska integreras med annan kod och ha olika affärslogik.

Alla `OperationService` klasser utöka `AbstractOperationService`, vilket tillåter ytterligare tillägg som kan knytas till den åtgärd som utförs. Varje åtgärd i tjänsten representeras av en `SocialOperation` klassen. The `OperationExtensions` klassen kan anropas under körning genom att anropa metoderna

* `performBeforeActions()`

  Tillåter förkontroller/förbehandling och validering
* `performAfterActions()`

  Gör det möjligt att redigera resurser ytterligare eller anropa anpassade händelser, arbetsflöden och så vidare.

#### Klassen OperationExtension {#operationextension-class}

The `OperationExtension` klasser är anpassade koddelar som kan injiceras i en åtgärd som gör det möjligt att anpassa operationer efter affärsbehov. Konsumenterna av komponenten kan dynamiskt och stegvis lägga till funktioner i komponenten. Med hjälp av tilläggs-/krokmönstret kan utvecklare fokusera enbart på själva tilläggen och ta bort behovet av att kopiera och åsidosätta hela åtgärder och komponenter.

## Exempelkod {#sample-code}

Exempelkod finns i [Adobe Experience Cloud GitHub](https://github.com/Adobe-Marketing-Cloud) databas. Sök efter projekt med antingen `aem-communities` eller `aem-scf`.

## Bästa praxis {#best-practices}

Visa [Riktlinjer för kodning](code-guide.md) för olika riktlinjer för kodning och metodtips för AEM Communities-utvecklare.

Se även [Lagringsresursleverantör (SRP) för UGC](srp.md) om du vill veta mer om hur du får åtkomst till användargenererat innehåll.

| **[⇐ - funktioner](essentials.md)** | **[Anpassning på klientsidan](client-customize.md)** |
|---|---|
|   | **[SCF Handlebars Helpers](handlebars-helpers.md)** |
