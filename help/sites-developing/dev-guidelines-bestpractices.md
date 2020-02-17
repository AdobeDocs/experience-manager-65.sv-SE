---
title: AEM Development - Guidelines and Best Practices
seo-title: AEM Development - Guidelines and Best Practices
description: Riktlinjer och bästa praxis för utveckling på AEM
seo-description: Riktlinjer och bästa praxis för utveckling på AEM
uuid: a67de085-4441-4a1d-bec3-2f27892a67ff
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: b4cf0ffc-973a-473b-80c8-7f530d111435
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# AEM Development - Guidelines and Best Practices{#aem-development-guidelines-and-best-practices}

## Riktlinjer för användning av mallar och komponenter {#guidelines-for-using-templates-and-components}

AEM-komponenter och -mallar utgör en mycket kraftfull verktygslåda. De kan användas av utvecklare för att ge användare, redaktörer och administratörer på webbplatser den funktionalitet de behöver för att anpassa sina webbplatser till föränderliga affärsbehov (innehållsflexibilitet) samtidigt som webbplatsernas enhetliga layout (varumärkesskydd) bibehålls.

En typisk utmaning för en person som ansvarar för en webbplats, eller en uppsättning webbplatser (till exempel på ett globalt företags kontor) är att presentera en ny typ av innehållspresentation på deras webbplatser.

Låt oss anta att det finns ett behov av att lägga till en nyhetslistsida på webbplatserna, som listar utdrag från andra artiklar som redan har publicerats. Sidan ska ha samma design och struktur som resten av webbplatsen.

Det rekommenderade sättet att hantera en sådan utmaning är att

* Återanvänd en befintlig mall för att skapa en ny typ av sida. Mallen definierar en sidstruktur (navigeringselement, paneler och så vidare) som finjusteras ytterligare av dess design (CSS, grafik).
* Använd styckesystemet (parsys/iparsys) på de nya sidorna.
* Definiera direkt åtkomst till styckesystemens designläge, så att endast behöriga personer (vanligtvis administratören) kan ändra dem.
* Definiera de komponenter som tillåts i det angivna styckesystemet så att redigerare sedan kan placera de nödvändiga komponenterna på sidan. I det här fallet kan det vara en listkomponent som kan gå igenom ett underträd med sidor och extrahera informationen enligt fördefinierade regler.
* Redigerare lägger till och konfigurerar de tillåtna komponenterna, på de sidor som de ansvarar för, för att leverera den begärda funktionen (information) till företaget.

Detta visar hur detta tillvägagångssätt gör det möjligt för de medverkande användarna och administratörerna på webbplatsen att snabbt reagera på affärsbehov, utan att utvecklingsteamen behöver vara engagerade. Alternativa metoder, till exempel att skapa en ny mall, är vanligtvis en kostsam övning som kräver en ändringshanteringsprocess och att utvecklingsteamet är engagerat. Detta gör hela processen mycket längre och kostsam.

Utvecklarna av AEM-baserade system bör därför använda

* mallar och åtkomstkontroll för styckesystemdesign för enhetligt varumärke och varumärkesskydd
* styckesystem inklusive dess konfigurationsalternativ för flexibilitet.

Följande allmänna regler för utvecklare är bra för de flesta vanliga projekt:

* Behåll lågt antal mallar - lika lite som antalet helt olika sidstrukturer på webbplatserna.
* Erbjud nödvändig flexibilitet och konfigurationsfunktioner till dina anpassade komponenter.
* Maximera användningen av det kraftfulla och flexibla AEM-styckesystemet - parsys- och iparsys-komponenterna.

### Anpassa komponenter och andra element {#customizing-components-and-other-elements}

När du skapar egna komponenter eller anpassar en befintlig komponent är det oftast enklast (och säkraste) att återanvända befintliga definitioner. Samma principer gäller även andra element i AEM, till exempel felhanteraren.

Detta kan du göra genom att kopiera och ersätta den befintliga definitionen. Med andra ord kopierar du definitionen från `/libs` till `/apps/<your-project>`. Den nya definitionen `/apps`kan uppdateras enligt dina önskemål.

>[!NOTE]
>
>Mer information finns i [Använda övertäckningar](/help/sites-developing/overlays.md) .

Exempel:

* [Anpassa en komponent](/help/sites-developing/components.md)

   Detta innebar att en komponentdefinition skulle ersättas:

   * Skapa en ny komponentmapp i `/apps/<website-name>/components/<MyComponent>` genom att kopiera en befintlig komponent:

      * Så här anpassar du komponentkopian Text:

         * from `/libs/foundation/components/text`
         * to `/apps/myProject/components/text`

* [Anpassa sidor som visas av felhanteraren](/help/sites-developing/customizing-errorhandler-pages.md#how-to-customize-pages-shown-by-the-error-handler)

   Det här fallet handlar om att täcka över en serverdel:

   * Kopiera standardskripten i databasen:

      * from `/libs/sling/servlet/errorhandler/`
      * to `/apps/sling/servlet/errorhandler/`

>[!CAUTION]
>
>Du **får inte** ändra något i `/libs` banan.
>
>Detta beror på att innehållet i `/libs` skrivs över nästa gång du uppgraderar din instans (och kan mycket väl skrivas över när du använder en snabbkorrigering eller ett funktionspaket).
>
>För konfiguration och andra ändringar:
>
>1. kopiera objektet i `/libs` till `/apps`
>1. gör ändringar i `/apps`


## När JCR-frågor ska användas och när de inte ska användas {#when-to-use-jcr-queries-and-when-not-to-use-them}

JCR-frågor är ett kraftfullt verktyg när de används på rätt sätt. De är lämpliga för

* riktiga slutanvändarfrågor, t.ex. fulltextsökningar i innehåll.
* tillfällen då strukturerat innehåll måste hittas i hela databasen.

   I sådana fall ska du se till att frågor endast körs när det är absolut nödvändigt, t.ex. vid komponentaktivering eller cacheogiltigförklaring (till skillnad från t.ex. arbetsflödessteg, händelsehanterare som utlöser vid innehållsändringar, filter etc.).

JCR-frågor ska aldrig användas för renderingsbegäranden. JCR-frågor passar till exempel inte för

* återgivningsnavigering
* skapa en översikt över de 10 senaste nyhetsobjekten
* visa antal innehållsobjekt

Använd navigeringsåtkomst till innehållsträdet i stället för att utföra en JCR-fråga när du återger innehåll.

>[!NOTE]
>
>Om du använder [Query Builder](/help/sites-developing/querybuilder-api.md)använder du JCR-frågor eftersom Query Builder genererar JCR-frågor under huven.


## Säkerhetsaspekter {#security-considerations}

>[!NOTE]
>
>Det är också värt att referera till [checklistan](/help/sites-administering/security-checklist.md)för säkerhet.

### JCR-sessioner (databas) {#jcr-repository-sessions}

Du bör använda användarsessionen, inte den administrativa sessionen. Detta innebär att du bör använda:

```java
slingRequest.getResourceResolver().adaptTo(Session.class);
```

### Skydda mot XSS (Cross-Site Scripting) {#protect-against-cross-site-scripting-xss}

Med XSS (Cross-site scripting) kan angripare lägga in kod på webbsidor som visas av andra användare. Säkerhetsluckan kan utnyttjas av skadliga webbanvändare för att kringgå åtkomstkontroller.

AEM tillämpar principen att filtrera allt innehåll som användaren tillhandahåller vid utskrift. Förhindrande av XSS har högsta prioritet under både utveckling och testning.

Dessutom kan en brandvägg för ett webbprogram, till exempel [mod_security för Apache](https://modsecurity.org), ge tillförlitlig, central kontroll över säkerheten i distributionsmiljön och skydda mot tidigare oidentifierade serveröverskridande skriptattacker (cross-site scripting).

>[!CAUTION]
>
>Exempelkod som tillhandahålls med AEM kanske inte själv skyddar mot sådana attacker och är vanligtvis beroende av begärandefiltrering från en brandvägg för webbprogram.

Lathund för XSS API innehåller information som du behöver känna till för att kunna använda XSS API:t och göra en AEM-app säkrare. Du kan ladda ned den här:

XSSAPI-kalkylbladet.

[Hämta fil](assets/xss_cheat_sheet_2016.pdf)

### Skydda kommunikation för konfidentiell information {#securing-communication-for-confidential-information}

Liksom för alla Internetprogram ska du se till att konfidentiella uppgifter skickas

* trafiken säkras via SSL
* HTTP POST används om tillämpligt

Detta gäller information som är konfidentiell för systemet (t.ex. konfiguration eller administrativ åtkomst) samt information som är konfidentiell för användarna (t.ex. personuppgifter)

## Distinkta utvecklingsuppgifter {#distinct-development-tasks}

### Anpassa felsidor {#customizing-error-pages}

Felsidor kan anpassas för AEM. Detta är tillrådligt så att instansen inte visar slingspår på interna serverfel.

Mer information finns i [Anpassa felsidor som visas av felhanteraren](/help/sites-developing/customizing-errorhandler-pages.md) .

### Öppna filer i Java-processen {#open-files-in-the-java-process}

Eftersom AEM kan komma åt ett stort antal filer rekommenderar vi att antalet [öppna filer för en Java-process](/help/sites-deploying/configuring.md#open-files-in-the-java-process) konfigureras explicit för AEM.

För att minimera problemet bör du se till att alla öppnade filer stängs korrekt så snart som (meningsfullt) möjligt.
