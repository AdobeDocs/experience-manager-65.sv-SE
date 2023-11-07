---
title: AEM - riktlinjer och bästa praxis
description: Riktlinjer och bästa metoder för att utveckla AEM
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
exl-id: 8eef7e4d-a6f2-4b87-a995-0761447283c6
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '1084'
ht-degree: 0%

---

# AEM - riktlinjer och bästa praxis{#aem-development-guidelines-and-best-practices}

## Riktlinjer för användning av mallar och komponenter {#guidelines-for-using-templates-and-components}

Adobe Experience Manager (AEM) komponenter och mallar utgör en kraftfull verktygslåda. De kan användas av utvecklare för att ge användare, redaktörer och administratörer på webbplatser möjlighet att anpassa sina webbplatser efter förändrade affärsbehov (innehållsflexibilitet). Allt detta med bibehållen enhetlig layout för webbplatserna (varumärkesskydd).

En typisk utmaning för en person som ansvarar för en webbplats, eller en uppsättning webbplatser (till exempel på ett lokalkontor i ett globalt företag) är att presentera en ny typ av innehållspresentation på sina webbplatser.

Låt oss anta att det finns ett behov av att lägga till en nyhetslistsida på webbplatserna, som listar utdrag från andra artiklar som redan har publicerats. Sidan ska ha samma design och struktur som resten av webbplatsen.

Det rekommenderade sättet att hantera en sådan utmaning är att

* Återanvänd en befintlig mall så att du kan skapa en typ av sida. Mallen definierar en sidstruktur (navigeringselement, paneler och så vidare) som finjusteras ytterligare av dess design (CSS, grafik).
* Använd styckesystemet (parsys/iparsys) på de nya sidorna.
* Definiera direkt åtkomst till styckesystemens designläge, så att endast behöriga personer (vanligtvis administratören) kan ändra dem.
* Definiera de komponenter som tillåts i det angivna styckesystemet så att redigerare sedan kan placera de nödvändiga komponenterna på sidan. I det här fallet kan det vara en listkomponent som kan gå igenom ett underträd med sidor och extrahera informationen enligt fördefinierade regler.
* Redigerare lägger till och konfigurerar de tillåtna komponenterna på de sidor som de ansvarar för för för att leverera den begärda funktionen (information) till företaget.

Detta visar hur detta tillvägagångssätt gör det möjligt för de medverkande användarna och administratörerna på webbplatsen att snabbt reagera på affärsbehov, utan att utvecklingsteamen behöver vara engagerade. Alternativa metoder, till exempel att skapa en mall, är vanligtvis en kostsam övning som kräver en ändringshanteringsprocess och att utvecklingsteamet är engagerat. Detta gör hela processen längre och kostsam.

Utvecklarna av AEM bör därför använda

* mallar och åtkomstkontroll för styckesystemdesign för enhetligt varumärke och varumärkesskydd
* styckesystem inklusive dess konfigurationsalternativ för flexibilitet.

Följande allmänna regler för utvecklare passar bäst i de vanligaste projekten:

* Behåll lågt antal mallar - lika lite som antalet helt olika sidstrukturer på webbplatserna.
* Ge de anpassade komponenterna den flexibilitet och de konfigurationsfunktioner som behövs.
* Maximera användningen av kraften och flexibiliteten i det AEM styckesystemet - parsys- och iparsys-komponenterna.

### Anpassa komponenter och andra element {#customizing-components-and-other-elements}

När du skapar egna komponenter eller anpassar en befintlig komponent är det oftast enklast (och säkraste) att återanvända befintliga definitioner. Samma principer gäller även andra element i AEM, till exempel felhanteraren.

Detta kan du göra genom att kopiera och ersätta den befintliga definitionen. Med andra ord, kopiera definitionen från `/libs` till `/apps/<your-project>`. Den här nya definitionen, i `/apps`, kan uppdateras efter dina behov.

>[!NOTE]
>
>Se [Använda övertäckningar](/help/sites-developing/overlays.md) för mer information.

Till exempel:

* [Anpassa en komponent](/help/sites-developing/components.md)

  Detta innebar att en komponentdefinition skulle ersättas:

   * Skapa en komponentmapp i `/apps/<website-name>/components/<MyComponent>` genom att kopiera en befintlig komponent:

      * Så här anpassar du komponentkopian Text:

         * från `/libs/foundation/components/text`
         * till `/apps/myProject/components/text`

* [Anpassa sidor som visas av felhanteraren](/help/sites-developing/customizing-errorhandler-pages.md#how-to-customize-pages-shown-by-the-error-handler)

  Det här fallet handlar om att täcka över en serverdel:

   * Kopiera ett eller flera standardskript i databasen:

      * från `/libs/sling/servlet/errorhandler/`
      * till `/apps/sling/servlet/errorhandler/`

>[!CAUTION]
>
>**Gör inte** ändra något i `/libs` bana.
>
>Orsaken är att innehållet i `/libs` skrivs över nästa gång du uppgraderar din instans (och kan mycket väl skrivas över när du installerar en snabbkorrigering eller ett funktionspaket).
>
>För konfiguration och andra ändringar:
>
>1. kopiera objektet i `/libs` till `/apps`
>1. gör ändringar i `/apps`

## När JCR-frågor ska användas och när de inte ska användas {#when-to-use-jcr-queries-and-when-not-to-use-them}

JCR-frågor är ett kraftfullt verktyg när de används på rätt sätt. De är lämpliga för

* riktiga slutanvändarfrågor, t.ex. fulltextsökningar i innehåll.
* tillfällen då strukturerat innehåll måste hittas i hela databasen.

  I så fall måste du se till att frågor bara körs när det behövs. Till exempel vid komponentaktivering eller cacheogiltigförklaring (till skillnad från till exempel arbetsflöden, händelsehanterare som aktiveras vid innehållsändringar och filter).

Använd aldrig JCR-frågor för renderingsbegäranden. JCR-frågor passar till exempel inte för följande:

* återgivningsnavigering
* skapa en översikt över de 10 senaste nyhetsartiklarna
* visa antal innehållsobjekt

Använd navigeringsåtkomst till innehållsträdet i stället för att utföra en JCR-fråga när du återger innehåll.

>[!NOTE]
>
>Om du använder [Frågebyggaren](/help/sites-developing/querybuilder-api.md)använder du JCR-frågor när Query Builder genererar JCR-frågor under huven.
>

## Säkerhetsaspekter {#security-considerations}

>[!NOTE]
>
>Det är även värt att hänvisa till [checklista för säkerhet](/help/sites-administering/security-checklist.md).

### JCR-sessioner (databas) {#jcr-repository-sessions}

Använd användarsessionen, inte den administrativa sessionen. Detta innebär att du bör använda:

```java
slingRequest.getResourceResolver().adaptTo(Session.class);
```

### Protect mot XSS (Cross-Site Scripting) {#protect-against-cross-site-scripting-xss}

Med XSS (Cross-site scripting) kan angripare lägga in kod på webbsidor som visas av andra användare. Säkerhetsluckan kan utnyttjas av skadliga webbanvändare för att kringgå åtkomstkontroller.

AEM tillämpar principen om att filtrera allt innehåll som användaren tillhandahåller vid utskrift. Förhindrande av XSS har högsta prioritet under både utveckling och testning.

En brandvägg för webbprogram, som [mod_security för Apache](https://modsecurity.org), kan ge tillförlitlig och central kontroll över distributionsmiljöns säkerhet och skydda mot tidigare oidentifierade serveröverskridande skriptattacker (cross-site scripting).

>[!CAUTION]
>
>Exempelkod som medföljer AEM kan inte skydda sig mot sådana attacker och är vanligtvis beroende av att en webbprogrambrandvägg filtrerar begäranden.

XSS API-databladet innehåller information som du måste känna till för att kunna använda XSS API:t och göra en AEM säkrare. Du kan ladda ned den här:

XSSAPI-kalkylblad.

[Hämta fil](assets/xss_cheat_sheet_2016.pdf)

### Säkra kommunikation för konfidentiell information {#securing-communication-for-confidential-information}

Liksom för alla Internetprogram ska du se till att konfidentiella uppgifter skickas

* trafiken säkras via SSL
* HTTP-POST används om tillämpligt

Detta gäller information som är konfidentiell för systemet (som konfiguration eller administrativ åtkomst) och information som är konfidentiell för användarna (som deras personuppgifter)

## Distinkta utvecklingsuppgifter {#distinct-development-tasks}

### Anpassa felsidor {#customizing-error-pages}

Felsidor kan anpassas för AEM. Detta är tillrådligt så att instansen inte visar slingspår på interna serverfel.

Se [Anpassa felsidor som visas av felhanteraren](/help/sites-developing/customizing-errorhandler-pages.md) för fullständig information.

### Öppna filer i Java™-processen {#open-files-in-the-java-process}

Eftersom AEM kan få åtkomst till många filer bör du ange antalet [öppna filer för en Java™-process](/help/sites-deploying/configuring.md#open-files-in-the-java-process) vara explicit konfigurerad för AEM.

För att minimera problemet bör utvecklingsverktyget se till att alla öppna filer stängs korrekt när det är möjligt (meningsfullt).
