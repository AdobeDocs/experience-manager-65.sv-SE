---
title: Stängda användargrupper i AEM
description: Läs mer om stängda användargrupper i AEM.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
docset: aem65
exl-id: 39e35a07-140f-4853-8f0d-8275bce27a65
feature: Security
source-git-commit: 71b3f7c6ad2c7712762a29518de6cf0639081cb7
workflow-type: tm+mt
source-wordcount: '6845'
ht-degree: 0%

---

# Stängda användargrupper i AEM{#closed-user-groups-in-aem}

## Introduktion {#introduction}

Sedan AEM 6.3 finns det en ny implementering av en stängd användargrupp som är avsedd att åtgärda de problem med prestanda, skalbarhet och säkerhet som den befintliga implementeringen innebär.

>[!NOTE]
>
>För enkelhetens skull kommer förkortningen CUG att användas i denna dokumentation.

Målet med den nya implementeringen är att vid behov ta med befintliga funktioner samtidigt som man åtgärdar problem och designbegränsningar från äldre versioner. Resultatet blir en ny CUG-design med följande egenskaper:

* Tydlig separation av autentiserings- och auktoriseringselement, som kan användas var för sig eller i kombination.
* Dedikerad tillståndsmodell som återspeglar den begränsade läsåtkomsten vid de konfigurerade CUG-träden utan att påverka andra åtkomstkontrollinställningar och behörighetskrav.
* Åtkomstkontrollinställningarna för den begränsade läsåtkomsten, som vanligtvis behövs för redigeringsförekomster, skiljer sig åt och behörighetsutvärderingen som vanligtvis bara önskas vid publicering.
* Redigering av begränsad läsbehörighet utan eskalering av behörigheter.
* Dedikerat nodtypstillägg för att markera autentiseringskravet.
* Valfri inloggningssökväg som är associerad med autentiseringskravet.

### Implementering av ny anpassad användargrupp {#the-new-custom-user-group-implementation}

En CUG som den är känd i AEM består av följande steg:

* Begränsa läsåtkomst för trädet som behöver skyddas och endast tillåta läsning för objekt som antingen listas med en viss CUG-instans eller exkluderas från CUG-utvärderingen. Detta kallas för **auktorisation** -element.
* Tvinga autentisering för ett visst träd och ange eventuellt en dedikerad inloggningssida för det trädet som sedan utesluts. Detta kallas för **autentisering** -element.

Den nya implementeringen har utformats för att skapa en gräns mellan autentiserings- och auktoriseringselementen. Från och med AEM 6.3 är det möjligt att begränsa läsåtkomst utan att explicit lägga till ett autentiseringskrav. Om till exempel en viss instans kräver autentisering helt eller ett visst träd redan finns i ett underträd som redan kräver autentisering.

På samma sätt kan ett visst träd markeras med ett autentiseringskrav utan att ändra den gällande behörighetsinställningen. Kombinationerna och resultaten visas i [Kombinera CUG-principer och autentiseringskrav](/help/sites-administering/closed-user-groups.md#combining-cug-policies-and-the-authentication-requirement) -avsnitt.

## Översikt {#overview}

### Behörighet: Begränsa läsåtkomst {#authorization-restricting-read-access}

Nyckelfunktionen i en CUG-fil är att begränsa läsåtkomst för ett visst träd i innehållsdatabasen för alla utom valda huvuden. I stället för att manipulera standardinnehållet för åtkomstkontroll på direkten har den nya implementeringen en annan metod genom att definiera en dedikerad typ av åtkomstkontrollprincip som representerar en CUG.

#### Åtkomstkontrollprincip för CUG {#access-control-policy-for-cug}

Den nya typen av policy har följande egenskaper:

* Åtkomstkontrollprincip av typen org.apache.jackrabbit.api.security.permission.PrincipalSetPolicy (definieras av API:t för Apache Jackrabbit).
* PrincipalSetPolicy ger behörighet till en uppsättning av huvudkonton som kan ändras.
* De privilegier som ges och åtgärdens omfattning är en genomförandedetalj.

Implementeringen av PrincipalSetPolicy som används för att representera CUG:er definierar dessutom följande:

* CUG-principer ger endast läsåtkomst till vanliga JCR-objekt (till exempel utelämnas åtkomstkontrollinnehåll).
* Omfånget definieras av den åtkomststyrda nod som innehåller CUG-principen.
* CUG-principer kan kapslas, en kapslad CUG startar en ny CUG utan att ärva huvuduppsättningen i CUG-filen för överordnad.
* Om utvärdering är aktiverat ärvs effekten av principen till hela underträdet ned till nästa kapslade CUG.

Dessa CUG-principer distribueras till en AEM instans via en separat autentiseringsmodul som kallas ekaauktoriseringskug. Den här modulen har en egen åtkomststyrningshantering och behörighetsutvärdering. Standardkonfigurationen AEM med andra ord en konfiguration för Oak-innehållsdatabas som kombinerar flera auktoriseringsmekanismer. Mer information finns på [den här sidan på Apache Oak Documentation](https://jackrabbit.apache.org/oak/docs/security/authorization/composite.html).

I den här sammansatta konfigurationen ersätter inte en ny CUG det befintliga åtkomstkontrollsinnehållet som är kopplat till målnoden, utan är utformat som ett tillägg som också kan tas bort senare utan att den ursprungliga åtkomstkontrollen påverkas. Som standard är AEM en åtkomstkontrollista.

Till skillnad från den tidigare implementeringen identifieras och behandlas de nya CUG-reglerna alltid som innehåll för åtkomstkontroll. Det innebär att de skapas och redigeras med JCR-API:t för åtkomstkontroll. Mer information finns i [Hantera CUG-principer](#managing-cug-policies) -avsnitt.

#### Behörighetsutvärdering av CUG-principer {#permission-evaluation-of-cug-policies}

Förutom en dedikerad åtkomstkontrollshantering för CUG:er kan du med den nya auktoriseringsmodellen villkorligt aktivera behörighetsutvärdering för dess principer. Detta gör att du kan konfigurera CUG-principer i en staging-miljö och endast aktivera utvärdering av de gällande behörigheterna när de har replikerats till produktionsmiljön.

Behörighetsutvärderingen för CUG-profiler och interaktionen med standardauktoriseringen eller eventuella ytterligare auktoriseringsmodeller följer det mönster som utformats för flera auktoriseringsmekanismer i Apache Jackrabbit Oak: en given uppsättning behörigheter beviljas om och endast om alla modeller tillåter åtkomst. Se [den här sidan](https://jackrabbit.apache.org/oak/docs/security/authorization/composite.html) för mer information.

Följande egenskaper gäller för behörighetsutvärderingen som är kopplad till behörighetsmodellen som är utformad för att hantera och utvärdera CUG-principer:

* Det hanterar bara läsbehörigheter för vanliga noder och egenskaper, men inte läsåtkomstkontrollinnehåll
* Det hanterar inte skrivbehörigheter eller andra typer av behörigheter som krävs för att ändra skyddat JCR-innehåll (åtkomstkontroll, nodtypsinformation, versionshantering, låsning eller användarhantering bland annat). Dessa behörigheter påverkas inte av en CUG-princip och utvärderas inte av den associerade auktoriseringsmodellen. Huruvida dessa behörigheter beviljas eller inte beror på de andra modellerna som har konfigurerats i säkerhetsinställningarna.

Effekten av en enda CUG-princip vid utvärdering av tillstånd kan sammanfattas enligt följande:

* Läsåtkomst nekas för alla utom för ämnen som innehåller uteslutna principer eller principer som anges i policyn.
* Principen får verkan på den åtkomststyrda nod som innehåller policyn och dess egenskaper.
* Effekten ärvs dessutom nedåt i hierarkin, dvs. det objektträd som definieras av den åtkomststyrda noden.
* Den påverkar dock varken syskon eller överordnade noder för den åtkomststyrda noden.
* Arvet av en viss CUG stoppas vid en kapslad CUG.

#### Bästa praxis {#best-practices}

Följande bästa metoder bör beaktas vid definition av begränsad läsåtkomst via användargränssnitten:

* Fatta ett medvetet beslut om huruvida ditt behov av en CUG handlar om att begränsa läsåtkomst eller autentiseringskrav. Om det senare, eller om det finns ett behov av båda, finns mer information om autentiseringskrav i avsnittet Bästa metoder
* Skapa en hotmodell för de data eller det innehåll som behöver skyddas för att identifiera hotgränser och få en tydlig bild av känsligheten hos data och de roller som är kopplade till auktoriserad åtkomst
* Modellera databasinnehållet och kundupplevelsegrupperna med hänsyn till allmänna aspekter av auktorisering och bästa praxis:

   * Kom ihåg att läsbehörighet endast beviljas om en viss användargränssnittsenhet och utvärderingen av andra moduler som distribueras i konfigurationsbidraget tillåter att ett visst ämne läser ett visst databasobjekt
   * Undvik att skapa redundanta användargrupper där läsåtkomst redan är begränsad av andra auktoriseringsmoduler
   * För stort behov av kapslade CUG:er kan potentiellt markera problem i innehållsdesignen
   * Mycket stort behov av kundengagemang (t.ex. på varje sida) kan tyda på att det behövs en anpassad behörighetsmodell som eventuellt är bättre anpassad för att passa de specifika säkerhetsbehoven i den aktuella tillämpningen och det aktuella innehållet.

* Begränsa sökvägarna som stöds för CUG-principer till några få träd i databasen för optimerade prestanda. Tillåt t.ex. bara CUG:er under noden /content som levererats som standardvärde sedan AEM 6.3.
* CUG-profiler är utformade för att ge läsåtkomst till en liten uppsättning huvudobjekt. Behovet av ett stort antal huvudansvariga kan lyfta fram frågor i innehållet eller programdesignen och bör omprövas.

### Autentisering: Definiera autentiseringskrav {#authentication-defining-the-auth-requirement}

De autentiseringsrelaterade delarna av CUG-funktionen gör att du kan markera träd som kräver autentisering och eventuellt ange en dedikerad inloggningssida. I enlighet med den tidigare versionen kan du med den nya implementeringen markera träd som kräver autentisering i innehållsdatabasen och som villkorligt aktiverar synkronisering med `Sling org.apache.sling.api.auth.Authenticator`ansvarar för att slutligen genomdriva kravet och omdirigera till en inloggningsresurs.

Dessa krav registreras hos autentiseraren med hjälp av en OSGi-tjänst som tillhandahåller `sling.auth.requirements` registration-egenskap. Dessa egenskaper används sedan för att dynamiskt utöka autentiseringskraven. Mer information finns i [Sling-dokumentation](https://sling.apache.org/apidocs/sling7/org/apache/sling/auth/core/AuthConstants.html#AUTH_REQUIREMENTS).

#### Definiera autentiseringskravet med en dedikerad blandningstyp {#defining-the-authentication-requirement-with-a-dedicated-mixin-type}

Av säkerhetsskäl ersätter den nya implementeringen användningen av en kvarvarande JCR-egenskap med en dedikerad blandningstyp som kallas `granite:AuthenticationRequired`, som definierar en valfri egenskap av typen STRING för inloggningssökvägen `granite:loginPath`. Endast innehållsändringar som är relaterade till den här mixin-typen kommer att leda till en uppdatering av de krav som registrerats med Apache Sling Authenticator. Ändringarna spåras vid beständiga tillfälliga ändringar och kräver därför en `javax.jcr.Session.save()` kräva att bli effektiva.

Samma sak gäller för `granite:loginPath` -egenskap. Den kommer endast att respekteras om den definieras av den autenticeringsrelaterade blandningstypen. Om du lägger till en restegenskap med det här namnet i en ostrukturerad JCR-nod visas inte den önskade effekten och egenskapen ignoreras av hanteraren som ansvarar för uppdateringen av OSGi-registreringen.

>[!NOTE]
>
>Inställningen av inloggningssökvägsegenskapen är valfri och behövs bara om trädet som kräver autentisering inte kan återgå till standardsidan eller en på annat sätt ärvd inloggningssida. Se [Utvärdering av inloggningssökväg](/help/sites-administering/closed-user-groups.md#evaluation-of-login-path) nedan.

#### Registrerar autentiseringskravet och inloggningssökvägen med SSLING-autentiseraren {#registering-the-authentication-requirement-and-login-path-with-the-sling-authenticator}

Eftersom den här typen av autentiseringskrav förväntas begränsas till vissa körningslägen och till en liten delmängd av träd i innehållsdatabasen, är spårning av den obligatoriska blandningstypen och inloggningssökvägsegenskaperna villkorliga och bundna till en motsvarande konfiguration som definierar de sökvägar som stöds (se Konfigurationsalternativ nedan). Följaktligen kommer endast ändringar inom omfånget för de här sökvägarna som stöds att utlösa en uppdatering av OSGi-registreringen, i andra delar kommer både mixin-typen och egenskapen att ignoreras.

Standardinställningen för AEM använder nu den här konfigurationen genom att tillåta att mixinen ställs in i författarens körningsläge, men att den endast får effekt vid replikering till publiceringsinstansen. Se [den här sidan](https://sling.apache.org/documentation/the-sling-engine/authentication/authenticationframework.html) om du vill ha mer information om hur Sling uppfyller autentiseringskravet.

Lägga till `granite:AuthenticationRequired` blandningstypen i de konfigurerade sökvägarna som stöds gör att OSGi-registreringen av den ansvariga hanteraren uppdateras med en ny, extra post med `sling.auth.requirements` -egenskap. Om ett givet autentiseringskrav anger det valfria `granite:loginPath` -egenskapen registreras värdet dessutom med autentiseraren med ett &#39;-&#39;-prefix för att undantas från autentiseringskravet.

#### Utvärdering och arv av autentiseringskrav {#evaluation-and-inheritance-of-the-authentication-requirement}

Autentiseringskraven för Apache Sling förväntas ärvas genom sid- eller nodhierarkin. Själva detaljerna om arvet och utvärderingen av autentiseringskrav som ordning och prioritet betraktas som en implementeringsdetalj och kommer inte att dokumenteras i den här artikeln.

#### Utvärdering av inloggningssökväg {#evaluation-of-login-path}

Utvärderingen av inloggningssökvägen och omdirigeringen till motsvarande resurs vid autentisering är för närvarande en implementeringsdetalj i autentiseringshanteraren för Adobe Granite-inloggningsväljaren ( `com.day.cq.auth.impl.LoginSelectorHandler`), som är en Apache Sling AuthenticationHandler som har konfigurerats med AEM som standard.

Vid samtal `AuthenticationHandler.requestCredentials` den här hanteraren gör ett försök att avgöra vilken inloggningssida för mappning som användaren ska omdirigeras till. Detta inkluderar följande steg:

* Skilja mellan utgångna lösenord och behovet av regelbunden inloggning som orsak till omdirigeringen.
* Om en vanlig inloggning används testas om en inloggningssökväg kan hämtas i följande ordning:

   * från LoginPathProvider som implementeras av den nya `com.adobe.granite.auth.requirement.impl.RequirementService`,
   * från den gamla inaktuella CUG-implementeringen,
   * från Inloggningssidmappningar, enligt definition i `LoginSelectorHandler`,
   * och slutligen, återgå till standardinloggningssidan, som den definieras med `LoginSelectorHandler`.

* Så snart en giltig inloggningssökväg har erhållits via de samtal som listas ovan, kommer användarens begäran att omdirigeras till den sidan.

Målet för den här dokumentationen är att utvärdera inloggningssökvägen så som den visas av den interna `LoginPathProvider` gränssnitt. Implementeringen som skickats sedan AEM 6.3 fungerar på följande sätt:

* Registrering av inloggningssökvägar beror på skillnaden mellan lösenord som har upphört att gälla och behovet av regelbunden inloggning som orsak till omdirigeringen
* Om du loggar in regelbundet kontrolleras om en inloggningssökväg kan hämtas i följande ordning:

   * från `LoginPathProvider` som implementerats av den nya `com.adobe.granite.auth.requirement.impl.RequirementService`,
   * från den gamla inaktuella CUG-implementeringen,
   * från Inloggningssidmappningar som definierats med `LoginSelectorHandler`,
   * och slutligen återgå till standardinloggningssidan enligt definitionen med `LoginSelectorHandler`.

* Så snart en giltig inloggningssökväg har erhållits via de samtal som listas ovan, kommer användarens begäran att omdirigeras till den sidan.

The `LoginPathProvider` som implementerats av det nya stödet för krav på autentisering i Granite visar inloggningssökvägar som definieras av `granite:loginPath` egenskaper, som i sin tur definieras av blandningstypen enligt beskrivningen ovan. Mappningen av resurssökvägen som innehåller inloggningssökvägen och egenskapsvärdet behålls i minnet och utvärderas för att hitta en lämplig inloggningssökväg för andra noder i hierarkin.

>[!NOTE]
>
>Utvärderingen utförs endast för begäranden som är kopplade till resurser som finns i de konfigurerade sökvägarna som stöds. För andra förfrågningar utvärderas de alternativa sätten att bestämma inloggningssökvägen.

#### Bästa praxis {#best-practices-1}

Följande bästa metoder bör beaktas när autentiseringskrav definieras:

* Undvik inkapslade autentiseringskrav: det bör räcka att placera en enda auth-required-markör i början av ett träd och den ärvs till hela det underträd som definieras av målnoden. Ytterligare autentiseringskrav inom det trädet ska betraktas som redundanta och kan leda till prestandaproblem när autentiseringskraven utvärderas i Apache Sling. I och med separationen av behörighets- och autentiseringsrelaterade CUG-områden är det möjligt att begränsa läsåtkomst med hjälp av CUG eller andra typer av policyer samtidigt som autentisering för hela trädet upprätthålls.
* Modelldatabasinnehåll så att autentiseringskraven gäller för hela trädet utan att kapslade underträd behöver uteslutas från kravet igen.
* Så här undviker du att ange och därefter registrera redundanta inloggningssökvägar:

   * förlita sig på arv och undvika att definiera kapslade inloggningssökvägar,
   * anger inte den valfria inloggningssökvägen till ett värde som motsvarar standardvärdet eller ett ärvt värde,
   * programutvecklare bör identifiera vilka inloggningssökvägar som ska konfigureras i de globala konfigurationerna för inloggningssökväg (både standard och mappningar) som är kopplade till `LoginSelectorHandler`.

## Representation i databasen {#representation-in-the-repository}

### CUG-principrepresentation i databasen {#cug-policy-representation-in-the-repository}

Oak-dokumentationen beskriver hur de nya CUG-profilerna återspeglas i databasinnehållet. Mer information finns i [den här sidan](https://jackrabbit.apache.org/oak/docs/security/authorization/cug.html#Representation_in_the_Repository).

### Autentiseringskrav i databasen {#authentication-requirement-in-the-repository}

Behovet av en separat autentiseringskrav återspeglas i databasinnehållet med en dedikerad mixin-nodtyp som placeras på målnoden. MixIn-typen definierar en valfri egenskap som anger en dedikerad inloggningssida för trädet som definieras av målnoden.

Sidan som är kopplad till inloggningssökvägen kan finnas inuti eller utanför det trädet. Det kommer att uteslutas från autentiseringskravet.

```java
[granite:AuthenticationRequired]
      mixin
      - granite:loginPath (STRING)
```

## Hantera CUG-principer och autentiseringskrav {#managing-cug-policies-and-authentication-requirement}

### Hantera CUG-principer {#managing-cug-policies}

Den nya typen av åtkomstkontrollprinciper för att begränsa läsåtkomst för en CUG hanteras med hjälp av JCR-API:t för åtkomstkontroll och följer de mekanismer som beskrivs i [JCR 2.0-specifikation](https://www.adobe.io/experience-manager/reference-materials/spec/jcr/2.0/16_Access_Control_Management.html).

#### Ange en ny CUG-princip {#set-a-new-cug-policy}

Kod för att tillämpa en ny CUG-princip på en nod som inte hade en CUG-inställning tidigare. Observera att `getApplicablePolicies` returnerar bara nya profiler som inte har angetts tidigare. I slutet måste principen skrivas tillbaka och ändringarna måste sparas.

```java
String path = [...] // needs to be a supported, absolute path

Principal toAdd1 = [...]
Principal toAdd2 = [...]
Principal toRemove = [...]

AccessControlManager acMgr = session.getAccessControlManager();
PrincipalSetPolicy cugPolicy = null;

AccessControlPolicyIterator it = acMgr.getApplicablePolicies(path);
while (it.hasNext()) {
        AccessControlPolicy policy = it.nextAccessControlPolicy();
        if (policy instanceof PrincipalSetPolicy) {
           cugPolicy = (PrincipalSetPolicy) policy;
           break;
        }
}

if (cugPolicy == null) {
   log.debug("no applicable policy"); // path not supported or no applicable policy (for example,
                                                   // the policy was set before)
   return;
}

cugPolicy.addPrincipals(toAdd1, toAdd2);
cugPolicy.removePrincipals(toRemove));

acMgr.setPolicy(path, cugPolicy); // as of this step the policy can be edited/removed
session.save();
```

#### Redigera en befintlig CUG-princip {#edit-an-existing-cug-policy}

Följande steg krävs för att redigera en befintlig CUG-princip. Observera att den ändrade profilen måste skrivas tillbaka och att ändringarna måste sparas med `javax.jcr.Session.save()`.

```java
String path = [...] // needs to be a supported, absolute path

Principal toAdd1 = [...]
Principal toAdd2 = [...]
Principal toRemove = [...]

AccessControlManager acMgr = session.getAccessControlManager();
PrincipalSetPolicy cugPolicy = null;

for (AccessControlPolicy policy : acMgr.getPolicies(path)) {
     if (policy instanceof PrincipalSetPolicy) {
        cugPolicy = (PrincipalSetPolicy) policy;
        break;
     }
}

if (cugPolicy == null) {
   log.debug("no policy to edit"); // path not supported or policy not set before
   return;
}

if (cugPolicy.addPrincipals(toAdd1, toAdd2) || cugPolicy.removePrincipals(toRemove)) {
   acMgr.setPolicy(path, cugPolicy);
   session.save();
} else {
     log.debug("cug policy not modified");
}
```

### Hämta effektiva CUG-principer {#retrieve-effective-cug-policies}

Hanteringen av JCR-åtkomstkontroll definierar en metod för bästa förmåga att hämta principer som börjar gälla vid en viss sökväg. Eftersom utvärderingen av CUG-principer är villkorlig och beroende av vilken konfiguration som ska aktiveras, anropar du `getEffectivePolicies` är ett praktiskt sätt att kontrollera om en viss CUG-princip börjar gälla i en viss installation.

>[!NOTE]
>
>Observera skillnaden mellan `getEffectivePolicies` och det efterföljande kodexemplet som går upp i hierarkin för att hitta om en angiven sökväg redan ingår i en befintlig CUG.

```java
String path = [...] // needs to be a supported, absolute path

AccessControlManager acMgr = session.getAccessControlManager();
PrincipalSetPolicy cugPolicy = null;

// log an debug message of all CUG policies that take effect at the given path
// there could be zero, one or many (creating nested CUGs is possible)
for (AccessControlPolicy policy : acMgr.getEffectivePolicies(path) {
     if (policy instanceof PrincipalSetPolicy) {
        String policyPath = "-";
        if (policy instanceof JackrabbitAccessControlPolicy) {
           policyPath = ((JackrabbitAccessControlPolicy) policy).getPath();
        }
        log.debug("Found effective CUG for path '{}' at '{}', path, policyPath);
     }
}
```

#### Hämta ärvda CUG-principer {#retrieve-inherited-cug-policies}

Söker efter alla kapslade CUG:er som har definierats på en viss sökväg oavsett om de börjar gälla eller inte. Mer information finns i [Konfigurationsalternativ](/help/sites-administering/closed-user-groups.md#configuration-options) -avsnitt.

```java
String path = [...]

List<AccessControlPolicy> cugPolicies = new ArrayList<AccessControlPolicy>();
while (isSupportedPath(path)) {
     for (AccessControlPolicy policy : acMgr.getPolicies(path)) {
         if (policy instanceof PrincipalSetPolicy) {
            cugPolicies.add(policy);
         }
      }
      path = (PathUtils.denotesRoot(path)) ? null : PathUtils.getAncestorPath(path, 1);
}
```

#### Hantera CUG-principer efter huvudnamn {#managing-cug-policies-by-pincipal}

De tillägg som definieras av `JackrabbitAccessControlManager` som tillåter redigering av åtkomstkontrollprinciper efter huvudnamn inte implementeras med CUG-åtkomstkontrollhantering, eftersom en CUG-princip per definition alltid påverkar alla huvudkonton: de som anges med `PrincipalSetPolicy` får läsåtkomst medan alla andra huvudobjekt inte kan läsa innehåll i trädet som definieras av målnoden.

Motsvarande metoder returnerar alltid en tom principarray, men genererar inga undantag.

### Hantera autentiseringskrav {#managing-the-authentication-requirement}

Ett nytt autentiseringskrav skapas, ändras eller tas bort genom att målnodens effektiva nodtyp ändras. Egenskapen för den valfria inloggningssökvägen kan sedan skrivas med det vanliga JCR-API:t.

>[!NOTE]
>
>Ändringarna i en angiven målnod som nämns ovan återspeglas endast i Apache Sling Authenticator om `RequirementHandler` har konfigurerats och målet finns i de träd som definieras av de sökvägar som stöds (se avsnittet Konfigurationsalternativ).
>
>Mer information finns på [Tilldela blandade nodtyper](https://docs.adobe.com/docs/en/spec/jcr/2.0/10_Writing.html#10.10.3 Mixin Node Types) och [Lägga till noder och ange egenskaper](https://docs.adobe.com/docs/en/spec/jcr/2.0/10_Writing.html#10.4 Lägga till noder och ange egenskaper)

#### Lägga till ett nytt verifieringskrav {#adding-a-new-auth-requirement}

Steg för att skapa ett nytt autentiseringskrav beskrivs nedan. Observera att kravet bara registreras med Apache Sling Authenticator om `RequirementHandler` har konfigurerats för trädet som innehåller målnoden.

```java
Node targetNode = [...]

targetNode.addMixin("granite:AuthenticationRequired");
session.save();
```

#### Lägg till ett nytt autentiseringskrav med inloggningssökväg {#add-a-new-auth-requirement-with-login-path}

Steg för att skapa ett nytt autentiseringskrav, inklusive en inloggningssökväg. Observera att kravet och undantaget för inloggningssökvägen endast registreras hos Apache Sling Authenticator om `RequirementHandler` har konfigurerats för trädet som innehåller målnoden.

```java
Node targetNode = [...]
String loginPath = [...] // STRING property

Node targetNode = session.getNode(path);
targetNode.addMixin("granite:AuthenticationRequired");

targetNode.setProperty("granite:loginPath", loginPath);
session.save();
```

#### Ändra en befintlig inloggningssökväg {#modify-an-existing-login-path}

Stegen för att ändra en befintlig inloggningssökväg beskrivs nedan. Ändringen registreras endast med Apache Sling Authenticator om `RequirementHandler` har konfigurerats för trädet som innehåller målnoden. Det tidigare värdet för inloggningssökvägen tas bort från registreringen. Autentiseringskravet som är associerat med målnoden påverkas inte av den här ändringen.

```java
Node targetNode = [...]
String newLoginPath = [...] // STRING property

if (targetNode.isNodeType("granite:AuthenticationRequired")) {
   targetNode.setProperty("granite:loginPath", newLoginPath);
   session.save();
} else {
     log.debug("cannot modify login path property; mixin type missing");
}
```

#### Ta bort en befintlig inloggningssökväg {#remove-an-existing-login-path}

Steg för att ta bort en befintlig inloggningssökväg. Inloggningssökvägsposten avregistreras endast från Apache Sling Authenticator om `RequirementHandler` har konfigurerats för trädet som innehåller målnoden. Autentiseringskravet som är associerat med målnoden påverkas inte.

```java
Node targetNode = [...]

if (targetNode.hasProperty("granite:loginPath") &&
   targetNode.isNodeType("granite:AuthenticationRequired")) {
   targetNode.setProperty("granite:loginPath", null);
   session.save();
} else {
     log.debug("cannot remove login path property; mixin type missing");
}
```

Du kan också använda metoden nedan för att uppnå samma syfte:

```java
String path = [...] // absolute path to target node

String propertyPath = PathUtils.concat(path, "granite:loginPath");
if (session.propertyExists(propertyPath)) {
    session.getProperty(propertyPath).remove();
    // or: session.removeItem(propertyPath);
    session.save();
}
```

#### Ta bort ett autenticeringskrav {#remove-an-auth-requirement}

Steg för att ta bort ett befintligt autentiseringskrav. Kravet avregistreras endast från Apache Sling Authenticator om `RequirementHandler` har konfigurerats för trädet som innehåller målnoden.

```java
Node targetNode = [...]
targetNode.removeMixin("granite:AuthenticationRequired");

session.save();
```

#### Hämta effektiva autentiseringskrav {#retrieve-effective-auth-requirements}

Det finns inget dedikerat offentligt API för att läsa alla effektiva autentiseringskrav som registrerats med Apache Sling Authenticator. Listan visas dock i systemkonsolen på `https://<serveraddress>:<serverport>/system/console/slingauth` under &quot;**Konfiguration av autentiseringskrav**&quot;.

Följande bild visar autentiseringskraven för en AEM publiceringsinstans med demoinnehåll. Den markerade sökvägen på communitysidan visar hur ett krav som lagts till av implementeringen som beskrivs i det här dokumentet återspeglas i Apache Sling Authenticator.

>[!NOTE]
>
>I det här exemplet har den valfria egenskapen för inloggningssökväg inte angetts. Följaktligen har ingen andra post registrerats hos autentiseraren.

![chlimage_1-24](assets/chlimage_1-24.jpeg)

#### Hämta den effektiva inloggningssökvägen {#retrieve-the-effective-login-path}

Det finns för närvarande inget offentligt API för att hämta inloggningssökvägen som börjar gälla anonymt när en resurs som kräver autentisering används. Se avsnittet Utvärdering av inloggningssökväg för implementeringsinformation om hur inloggningssökvägen hämtas.

Observera dock att utöver inloggningssökvägarna som definieras med den här funktionen finns det andra sätt att ange omdirigering till inloggningen, vilket bör beaktas när innehållsmodellen och autentiseringskraven för en viss AEM designas.

#### Hämta det ärvda autentiseringsbehovet {#retrieve-the-inherited-auth-requirement}

Precis som med inloggningssökvägen finns det inget offentligt API för att hämta de ärvda autentiseringskrav som definierats i innehållet. Följande exempel visar hur du listar alla autentiseringskrav som har definierats med en viss hierarki oavsett om de börjar gälla eller inte. Mer information finns på [Konfigurationsalternativ](/help/sites-administering/closed-user-groups.md#configuration-options).

>[!NOTE]
>
>Vi rekommenderar att du förlitar dig på arvsmekanismen både för autentiseringskrav och inloggningssökväg och undviker att skapa kapslade autentiseringskrav.
>
>Mer information finns i [Utvärdering och arv av autentiseringskrav](#evaluation-and-inheritance-of-the-authentication-requirement), [Utvärdering av inloggningssökväg](#evaluation-of-login-path) och [Bästa praxis](#best-practices).

```java
String path = [...]
Node node = session.getNode(path);

Map<String, String> authRequirements = new ArrayList<String, String>();
while (isSupported(node)) {
     if (node.isNodeType("granite:AuthenticationRequired")) {
         String loginPath = (node.hasProperty("granite:loginPath") ?
                                     node.getProperty("granite:loginPath").getString() :
                                     "";
        authRequirements.put(node.getPath(), loginPath);
        node = node.getParent();
     }
}
```

### Kombinera CUG-principer och autentiseringskrav {#combining-cug-policies-and-the-authentication-requirement}

I följande tabell visas giltiga kombinationer av CUG-principer och autentiseringskrav i en AEM som har båda modulerna aktiverade via konfigurationen.

| **Autentisering krävs** | **Inloggningssökväg** | **Begränsad läsåtkomst** | **Förväntad effekt** |
|---|---|---|---|
| Ja | Ja | Ja | En viss användare kan bara visa det underträd som är markerat med CUG-principen om en effektiv behörighetsutvärdering ger åtkomst. En oautentiserad användare omdirigeras till den angivna inloggningssidan. |
| Ja | Nej | Ja | En viss användare kan bara visa det underträd som är markerat med CUG-principen om en effektiv behörighetsutvärdering ger åtkomst. En oautentiserad användare omdirigeras till en ärvd standardinloggningssida. |
| Ja | Ja | Nej | En oautentiserad användare omdirigeras till den angivna inloggningssidan. Huruvida det är tillåtet att visa trädet som är markerat med auth-required beror på de faktiska behörigheterna för de enskilda objekten i det underträdet. Det finns ingen dedikerad CUG som begränsar läsåtkomst på plats. |
| Ja | Nej | Nej | En oautentiserad användare omdirigeras till en ärvd standardinloggningssida. Huruvida det är tillåtet att visa trädet som är markerat med behörighetskraven beror på de faktiska behörigheterna för de enskilda objekten i det underträdet. Det finns ingen dedikerad CUG som begränsar läsåtkomst på plats. |
| Nej | Nej | Ja | En given autentiserad eller oautentiserad användare kan bara visa det underträd som är markerat med CUG-principen om en effektiv behörighetsutvärdering beviljar åtkomst. En oautentiserad användare kommer att behandlas likadant och kommer inte att omdirigeras till inloggning. |

>[!NOTE]
>
>Kombinationen av Verifieringskrav = Nej och Inloggningssökväg = Ja anges inte ovan eftersom Inloggningssökväg är ett valfritt attribut som är associerat med ett Autentiseringskrav. Om du anger en JCR-egenskap med det namnet utan att lägga till den definierande mixin-typen får det ingen effekt och ignoreras av motsvarande hanterare.

## OSGi-komponenter och konfiguration {#osgi-components-and-configuration}

I det här avsnittet finns en översikt över OSGi-komponenterna och de enskilda konfigurationsalternativen som introducerades i den nya CUG-implementeringen.

Se även dokumentationen för CUG-mappning för en omfattande mappning av konfigurationsalternativen mellan den gamla och den nya implementeringen.

### Auktorisering: Installation och konfiguration {#authorization-setup-and-configuration}

De nya, auktoriseringsrelaterade delarna finns i **Oak CUG Authorization** bundle ( `org.apache.jackrabbit.oak-authorization-cug`), som ingår i AEM standardinstallation. Paketet definierar en separat auktoriseringsmodell som ska användas som ett ytterligare sätt att hantera läsåtkomst.

#### Konfigurera CUG-auktorisering {#setting-up-cug-authorization}

Hur du konfigurerar CUG-auktorisering beskrivs i detalj i [relevant Apache-dokumentation](https://jackrabbit.apache.org/oak/docs/security/authorization/cug.html#pluggability). AEM har som standard CUG-auktorisering i alla körningslägen. Stegvisa instruktioner kan också användas för att inaktivera CUG-auktorisering i de installationer som kräver en annan auktoriseringsinställning.

#### Konfigurera referensfiltret {#configuring-the-referrer-filter}

Du måste också konfigurera [Sling-referensfilter](/help/sites-administering/security-checklist.md#the-sling-referrer-filter) med alla värdnamn som kan användas för att komma åt AEM, till exempel via CDN, belastningsutjämnare och andra.

Om referensfiltret inte är konfigurerat visas fel, som följande, när en användare försöker logga in på en CUG-plats:

```shell
31.01.2017 13:49:42.321 *INFO* [qtp1263731568-346] org.apache.sling.security.impl.ReferrerFilter Rejected referrer header for POST request to /libs/granite/core/content/login.html/j_security_check : https://hostname/libs/granite/core/content/login.html?resource=%2Fcontent%2Fgeometrixx%2Fen%2Ftest-site%2Ftest-page.html&$$login$$=%24%24login%24%24&j_reason=unknown&j_reason_code=unknown
```

#### Egenskaper hos OSGi-komponenter {#characteristics-of-osgi-components}

Följande två OSGi-komponenter har introducerats för att definiera autentiseringskrav och ange dedikerade inloggningssökvägar:

* `org.apache.jackrabbit.oak.spi.security.authorization.cug.impl.CugConfiguration`
* `org.apache.jackrabbit.oak.spi.security.authorization.cug.impl.CugExcludeImpl`

**org.apache.jackrabbit.oak.spi.security.permission.cug.impl.CugConfiguration**

<table>
 <tbody>
  <tr>
   <td>Etikett</td>
   <td>Konfiguration av Apache Jackrabbit Oak CUG</td>
  </tr>
  <tr>
   <td>Beskrivning</td>
   <td>Auktoriseringskonfiguration som är dedikerad för att konfigurera och utvärdera CUG-behörigheter.</td>
  </tr>
  <tr>
   <td>Konfigurationsegenskaper</td>
   <td>
    <ul>
     <li><code>cugSupportedPaths</code></li>
     <li><code>cugEnabled</code></li>
     <li><code>configurationRanking</code></li>
    </ul> <p>Se även <a href="#configuration-options">Konfigurationsalternativ</a> nedan.</p> </td>
  </tr>
  <tr>
   <td>Konfigurationsprincip</td>
   <td><code>ConfigurationPolicy.REQUIRE</code></td>
  </tr>
  <tr>
   <td>Referenser</td>
   <td><code>CugExclude (ReferenceCardinality.OPTIONAL_UNARY)</code></td>
  </tr>
 </tbody>
</table>

**org.apache.jackrabbit.oak.spi.security.permission.cug.impl.CugExcludeImpl**

<table>
 <tbody>
  <tr>
   <td>Etikett</td>
   <td>Apache Jackrabbit Oak CUG Exclude List</td>
  </tr>
  <tr>
   <td>Beskrivning</td>
   <td>Gör att du kan exkludera huvudobjekt med konfigurerade namn från CUG-utvärderingen.</td>
  </tr>
  <tr>
   <td>Konfigurationsegenskaper</td>
   <td>
    <ul>
     <li><code>principalNames</code></li>
    </ul> <p>Se även avsnittet Konfigurationsalternativ nedan.</p> </td>
  </tr>
  <tr>
   <td>Konfigurationsprincip</td>
   <td><code>ConfigurationPolicy.REQUIRE</code></td>
  </tr>
  <tr>
   <td>Referenser</td>
   <td>NA</td>
  </tr>
 </tbody>
</table>

#### Konfigurationsalternativ {#configuration-options}

Konfigurationsalternativen är:

* `cugSupportedPaths`: Ange de underträd som kan innehålla CUG. Inget standardvärde har angetts
* `cugEnabled`: konfigurationsalternativ för att aktivera behörighetsutvärdering för aktuella CUG-principer.

De tillgängliga konfigurationsalternativen som är kopplade till modulen CUG-auktorisering listas och beskrivs mer ingående i [Apache Oak-dokumentation](https://jackrabbit.apache.org/oak/docs/security/authorization/cug.html#configuration).

#### Utesluta huvudkonton från CUG-utvärderingen {#excluding-principals-from-cug-evaluation}

Undantaget av enskilda huvudkonton från CUG-utvärderingen har antagits från den tidigare tillämpningen. Den nya CUG-auktoriseringen täcker detta med ett dedikerat gränssnitt som heter CugExclude. Apache Jackrabbit Oak 1.4 levereras med en standardimplementering som utesluter en fast uppsättning huvuduppgifter samt en utökad implementering som tillåter konfigurering av enskilda huvudnamn. Den senare konfigureras i AEM publiceringsinstanser.

Standardvärdet eftersom AEM 6.3 förhindrar att följande objekt påverkas av CUG-principer:

* administratörsobjekt (admin-användare, administratörsgrupp)
* användarkonton för tjänst
* intern systemsäkerhetsobjekt

Mer information finns i tabellen i [Standardkonfiguration sedan AEM 6.3](#default-configuration-since-aem) nedan.

Exkluderingen av gruppen &#39;administratörer&#39; kan ändras eller utökas i systemkonsolen i konfigurationsavsnittet i **Apache Jackrabbit Oak CUG Exclude List**.

Det går också att tillhandahålla och distribuera en anpassad implementering av gränssnittet CugExclude för att justera uppsättningen med uteslutna principer om det finns särskilda behov. Läs dokumentationen om [CUG-plug](https://jackrabbit.apache.org/oak/docs/security/authorization/cug.html#pluggability) om du vill ha mer information och ett exempel på implementering.

### Autentisering: Installation och konfiguration {#authentication-setup-and-configuration}

De nya, autentiseringsrelaterade delarna finns i **Autentiseringshanterare för Adobe Granite** bundle ( `com.adobe.granite.auth.authhandler` version 5.6.48). Det här paketet ingår i AEM standardinstallation.

För att ställa in autentiseringskravsersättning för det inaktuella CUG-stödet måste vissa OSGi-komponenter finnas och vara aktiva i en viss AEM. Mer information finns i **Egenskaper hos OSGi-komponenter** nedan.

>[!NOTE]
>
>På grund av det obligatoriska konfigurationsalternativet med RequirementHandler är de autentiseringsrelaterade delarna bara aktiva om funktionen har aktiverats genom att ange en uppsättning sökvägar som stöds. Med en AEM är funktionen inaktiverad i redigeringsläge och aktiverad för /content i publiceringskörningsläge.

**Egenskaper hos OSGi-komponenter**

Följande två OSGi-komponenter har introducerats för att definiera autentiseringskrav och ange dedikerade inloggningssökvägar:

* `com.adobe.granite.auth.requirement.impl.RequirementService`
* `com.adobe.granite.auth.requirement.impl.DefaultRequirementHandler`

**com.adobe.granite.auth.requirements.impl.RequirementService**

<table>
 <tbody>
  <tr>
   <td>Etikett</td>
   <td>-</td>
  </tr>
  <tr>
   <td>Beskrivning</td>
   <td>Dedikerad OSGi-tjänst för autentiseringskrav som registrerar en observatör för innehållsändringar som påverkar auth-kraven (via <code>granite:AuthenticationRequirement</code> blandningstyp) och inloggningssökvägar med visas för <code>LoginSelectorHandler</code>. </td>
  </tr>
  <tr>
   <td>Konfigurationsegenskaper</td>
   <td>-</td>
  </tr>
  <tr>
   <td>Konfigurationsprincip</td>
   <td><code>ConfigurationPolicy.OPTIONAL</code></td>
  </tr>
  <tr>
   <td>Referenser</td>
   <td>
    <ul>
     <li><code>RequirementHandler (ReferenceCardinality.MANDATORY_UNARY)</code></li>
     <li><code>Executor (ReferenceCardinality.MANDATORY_UNARY)</code></li>
    </ul> </td>
  </tr>
 </tbody>
</table>

**com.adobe.granite.auth.requirements.impl.DefaultRequirementHandler**

| Etikett | Autentiseringskrav och hanterare för inloggningssökväg för Adobe Granite |
|---|---|
| Beskrivning | `RequirementHandler` implementering som uppdaterar autentiseringskraven för Apache Sling och motsvarande undantag för de associerade inloggningssökvägarna. |
| Konfigurationsegenskaper | `supportedPaths` |
| Konfigurationsprincip | `ConfigurationPolicy.REQUIRE` |
| Referenser | NA |

#### Konfigurationsalternativ {#configuration-options-1}

De autentiseringsrelaterade delarna av CUG-omskrivningen levereras endast med ett konfigurationsalternativ som är kopplat till Adobe Granite-autentiseringskravet och inloggningssökvägshanteraren:

**&quot;Autentiseringskrav och inloggningssökvägshanterare&quot;**

<table>
 <tbody>
  <tr>
   <td>Egenskap</td>
   <td>Typ</td>
   <td>Standardvärde</td>
   <td>Beskrivning</td>
  </tr>
  <tr>
   <td><p>Etikett = Sökvägar som stöds</p> <p>Namn = 'supportedPaths'</p> </td>
   <td>Ange&lt;string&gt;</td>
   <td>-</td>
   <td>Sökvägar som autentiseringskraven gäller för den här hanteraren. Lämna konfigurationen inaktiverad om du vill lägga till <code>granite:AuthenticationRequirement</code> blanda text till noder utan att tvinga dem (till exempel på författarinstanser). Funktionen är inaktiverad om den saknas. </td>
  </tr>
 </tbody>
</table>

## Standardkonfiguration sedan AEM 6.3 {#default-configuration-since-aem}

Nya installationer av AEM använder som standard de nya implementeringarna både för auktoriserings- och autentiseringsrelaterade delar av CUG-funktionen. Den gamla implementeringen &quot;Adobe Granite Closed User Group (CUG) Support&quot; har tagits bort och kommer som standard att inaktiveras i alla AEM installationer. De nya implementeringarna aktiveras i stället enligt följande:

### Författarinstanser {#author-instances}

| **&quot;Konfiguration av Apache Jackrabbit Oak CUG&quot;** | **Förklaring** |
|---|---|
| Banor som stöds `/content` | Åtkomststyrningshantering för CUG-principer är aktiverat. |
| CUG-utvärdering aktiverad FALSE | Utvärdering av behörighet är inaktiverad. CUG-profiler träder inte i kraft. |
| Rankning | 200 | Mer information finns i Oak-dokumentation. |

>[!NOTE]
>
>Ingen konfiguration för **Apache Jackrabbit Oak CUG Exclude List** och **Autentiseringskrav och hanterare för inloggningssökväg för Adobe Granite** finns i standardinstanser för redigering.

### Publicera instanser {#publish-instances}

| **&quot;Konfiguration av Apache Jackrabbit Oak CUG&quot;** | **Förklaring** |
|---|---|
| Banor som stöds `/content` | Åtkomststyrningshantering för CUG-principer aktiveras under de konfigurerade sökvägarna. |
| CUG Evaluation Enabled TRUE | Behörighetsutvärderingen aktiveras under de konfigurerade sökvägarna. CUG-profiler börjar gälla `Session.save()`. |
| Rankning | 200 | Mer information finns i Oak-dokumentation. |

| **&quot;Apache Jackrabbit Oak CUG Exclude List&quot;** | **Förklaring** |
|---|---|
| Administratörer för huvudnamn | Exkluderar administratörsobjekt från CUG-utvärderingen. |

| **&quot;Autentiseringskrav för Adobe Granite och hanterare för inloggningssökväg&quot;** | **Förklaring** |
|---|---|
| Banor som stöds  `/content` | Autentiseringskrav som definieras i databasen med hjälp av `granite:AuthenticationRequired` blandningstyp börjar gälla nedan `/content` den `Session.save()`. Sling Authenticator uppdateras. Att lägga till blandningstypen utanför de banor som stöds ignoreras. |

## Inaktiverar CUG-auktoriserings- och autentiseringskrav {#disabling-cug-authorization-and-authentication-requirement}

Den nya implementeringen kan inaktiveras helt om en viss installation inte använder användargränssnitten eller använder olika metoder för autentisering och auktorisering.

### Inaktivera CUG-auktorisering {#disable-cug-authorization}

Läs [CUG-plug](https://jackrabbit.apache.org/oak/docs/security/authorization/cug.html#pluggability) dokumentation som innehåller information om hur du tar bort CUG-auktoriseringsmodellen från den sammansatta auktoriseringsinställningen.

### Inaktivera autentiseringskravet {#disable-the-authentication-requirement}

För att inaktivera stödet för autentiseringskraven enligt `granite.auth.authhandler` modul som det räcker att ta bort konfigurationen som är kopplad till **Autentiseringskrav och hanterare för inloggningssökväg för Adobe Granite**.

>[!NOTE]
>
>Observera dock att om du tar bort konfigurationen avregistreras inte blandningstypen, som fortfarande gällde för noder utan att börja gälla.

## Interaktion med andra moduler {#interaction-with-other-modules}

### Apache Jackrabbit API {#apache-jackrabbit-api}

För att återspegla den nya typen av åtkomstkontrollprincip som används av CUG-auktoriseringsmodellen har API:t som definieras av Apache Jackrabbit utökats. Sedan version 2.11.0 av `jackrabbit-api` module definierar ett nytt gränssnitt som kallas `org.apache.jackrabbit.api.security.authorization.PrincipalSetPolicy`som sträcker sig från `javax.jcr.security.AccessControlPolicy`.

### Apache Jackrabbit FileVault {#apache-jackrabbit-filevault}

Importmekanismen för Apache Jackrabbit FileVault har justerats för att hantera åtkomstkontrollprinciper av typen `PrincipalSetPolicy`.

### Distribution av Apache Sling-innehåll {#apache-sling-content-distribution}

Se ovanstående [Apache Jackrabbit FileVault](/help/sites-administering/closed-user-groups.md#apache-jackrabbit-filevault) -avsnitt.

### Adobe Granite-replikering {#adobe-granite-replication}

Replikeringsmodulen har justerats något för att kunna replikera CUG-principer mellan olika AEM instanser:

* `DurboImportConfiguration.isImportAcl()` tolkas ordagrant och påverkar endast regler för åtkomstkontroll som implementerar `javax.jcr.security.AccessControlList`

* `DurboImportTransformer` respekterar endast den här konfigurationen för äkta ACL:er
* Andra policyer som `org.apache.jackrabbit.api.security.authorization.PrincipalSetPolicy` instanser som skapas av CUG-auktoriseringsmodellen replikeras alltid och konfigurationsalternativet `DurboImportConfiguration.isImportAcl`() ignoreras.

Det finns en begränsning för replikering av CUG-principer. Om en viss CUG-princip tas bort utan att motsvarande mixin-nodtyp tas bort `rep:CugMixin,` borttagningen återspeglas inte vid replikering. Detta har åtgärdats genom att man alltid har tagit bort blandningen när man har tagit bort policyn. Begränsningen kan dock visa sig om blandningstypen läggs till manuellt.

### Autentiseringshanterare för Adobe Granite {#adobe-granite-authentication-handler}

Autentiseringshanteraren **Autentiseringshanterare för Adobe Granite HTTP Header** levererade med `com.adobe.granite.auth.authhandler` paket innehåller en referens till `CugSupport` gränssnitt som definieras av samma modul. Den används för att beräkna &quot;sfären&quot; under vissa omständigheter och återgår till sfären som konfigurerats med hanteraren.

Detta har justerats för att referera till `CugSupport` valfritt för att säkerställa maximal bakåtkompatibilitet om en viss konfiguration bestämmer sig för att återaktivera den borttagna implementeringen. Installationer som använder implementeringen kommer inte längre att få den sfär som extraheras från CUG-implementeringen, men den kommer alltid att visa sfären som den definierats med **Autentiseringshanterare för Adobe Granite HTTP Header**.

>[!NOTE]
>
>Som standard är **Autentiseringshanterare för Adobe Granite HTTP Header** är endast konfigurerad i publiceringskörningsläge med &quot;Inaktivera inloggningssida&quot; ( `auth.http.nologin`) aktiverat.

### AEM LiveCopy {#aem-livecopy}

Om du konfigurerar CUG:er i kombination med LiveCopy representeras de i databasen av en extra nod och en extra egenskap enligt följande:

* `/content/we-retail/us/en/blueprint/rep:cugPolicy`
* `/content/we-retail/us/en/LiveCopy@granite:loginPath`

Båda dessa element skapas under `cq:Page`. I den aktuella designen hanterar MSM bara noder och egenskaper som finns under `cq:PageContent` (`jcr:content`)-nod.

Därför kan CUG-grupper inte rullas ut till Live-kopior från utkast. Se till att du undviker detta när du konfigurerar Live Copy.

## Ändringar i den nya CUG-implementeringen {#changes-with-the-new-cug-implementation}

Syftet med detta avsnitt är att ge en översikt över de ändringar som gjorts i CUG-funktionen samt en jämförelse mellan den gamla och den nya implementeringen. Här listas de ändringar som påverkar hur CUG-stöd konfigureras och hur och av vilka CUG-grupper hanteras i databasinnehållet.

### Skillnader i CUG-inställningar och konfiguration {#differences-in-cug-setup-and-configuration}

Den borttagna OSGi-komponenten **Stöd för CUG (Adobe Granite Closed User Group)** ( `com.day.cq.auth.impl.cug.CugSupportImpl`) har ersatts av nya komponenter för att separat kunna hantera auktoriserings- och autentiseringsrelaterade delar av den tidigare CUG-funktionen.

## Skillnader i hantering av kundupplevelser i databasinnehållet {#differences-in-managing-cugs-in-the-repository-content}

I följande avsnitt beskrivs skillnaderna mellan den gamla och den nya implementeringen i implementerings- och säkerhetsperspektiven. Den nya implementeringen har samma funktionalitet, men det finns små förändringar som är viktiga att känna till när den nya CUG-filen används.

### Skillnader i fråga om tillstånd {#differences-with-regards-to-authorization}

De viktigaste skillnaderna från ett auktoriseringsperspektiv sammanfattas i listan nedan:

**Innehåll för dedikerad åtkomstkontroll för användargränssnitten**

I den gamla implementeringen användes standardauktoriseringsmodellen för att ändra åtkomstkontrollistans principer vid publicering och ersätta befintliga ACE:n med de inställningar som krävs av CUG:n. Detta utlöstes av att vanliga, kvarvarande JCR-egenskaper som tolkades vid publicering skrevs.

I och med den nya implementeringen påverkas inte åtkomstkontrollinställningen för standardauktoriseringsmodellen av någon CUG som skapas, ändras eller tas bort. Istället anropas en ny typ av princip `PrincipalSetPolicy` används som extra åtkomstkontrollinnehåll för målnoden. Den här extra principen kommer att placeras som underordnad till målnoden och kommer att vara jämställd med standardprincipnoden om en sådan finns.

**Redigera CUG-principer i åtkomststyrningshantering**

Den här förändringen från kvarvarande JCR-egenskaper till en dedikerad åtkomstkontrollprincip påverkar behörigheten som behövs för att skapa eller ändra auktoriseringsdelen av CUG-funktionen. Eftersom detta anses vara en ändring av innehållet i kontrollpanelen krävs det `jcr:readAccessControl` och `jcr:modifyAccessControl` behörighet för att kunna skrivas till databasen. Därför kan bara innehållsförfattare som har behörighet att ändra innehållet i åtkomstkontrollen på en sida konfigurera eller ändra det här innehållet. Detta står i kontrast till den gamla implementeringen där möjligheten att skriva vanliga JCR-egenskaper var tillräcklig, vilket resulterar i eskalering av behörigheter.

**Målnod definierad av princip**

CUG-principer förväntas skapas vid JCR-noden som definierar det underträd som ska ha begränsad läsåtkomst. Detta är sannolikt en AEM sida om CUG förväntas påverka hela trädet.

Observera att om du bara placerar CUG-principen på jcr:content-noden under en viss sida begränsas åtkomsten till innehållet s.str för en viss sida, men det kommer inte att gälla för några jämställda eller underordnade sidor. Detta kan vara ett giltigt användningsexempel och det är möjligt att göra detta med en databasredigerare som kan använda detaljerat åtkomstinnehåll. Den kontrasterar emellertid den tidigare implementeringen där placeringen av en cq:cugEnabled-egenskap på jcr:content-noden mappades om internt till sidnoden. Mappningen utförs inte längre.

**Behörighetsutvärdering med CUG-principer**

Genom att gå från det gamla CUG-stödet till en ytterligare behörighetsmodell ändras det sätt på vilket effektiva läsbehörigheter utvärderas. Enligt beskrivningen i [Jackrabbits dokumentation](https://jackrabbit.apache.org/oak/docs/security/authorization/composite.html), en angiven användare som kan visa `CUGcontent` beviljas läsåtkomst endast om behörighetsutvärderingen för alla modeller som är konfigurerade i Oak-databasen ger läsåtkomst.

Med andra ord, för utvärderingen av de gällande behörigheterna, `CUGPolicy` och standardposterna för åtkomstkontroll kommer att beaktas och läsåtkomst för CUG-innehållet kommer endast att beviljas om det beviljas av båda typerna av profiler. I en AEM publiceringsinstallation där läsåtkomst till den fullständiga `/content` Trädet beviljas för alla, effekten av CUG-policyer blir densamma som med den gamla implementeringen.

**On-Demand Evaluation**

CUG-auktoriseringsmodellen gör att du kan aktivera åtkomstkontroll och behörighetsutvärdering separat:

* åtkomststyrningshantering är aktiverad om modulen har en eller flera sökvägar som stöds där CUG kan skapas
* behörighetsutvärdering är bara aktiverat om alternativet **CUG-utvärdering aktiverad** är även markerad.

I den nya AEM standardutvärderingen av CUG-principer är det bara aktiverat med körläget&quot;publish&quot;. Läs mer om [standardkonfiguration sedan AEM 6.3](#default-configuration-since-aem) för mer information. Detta kan verifieras genom att man jämför effektiva profiler för en viss sökväg med de profiler som lagras i innehållet. Effektiva profiler visas bara om behörighetsutvärdering för användargränssnitten är aktiverat.

Som förklaras ovan lagras CUG-åtkomstkontrollprinciper nu alltid i innehållet, men utvärdering av de gällande behörigheterna som följer av dessa principer kommer endast att genomföras om **CUG-utvärdering aktiverad** är påslagen i systemkonsolen vid Apache Jackrabbit Oak **CUG-konfiguration.** Som standard aktiveras det endast med körningsläget &#39;publish&#39;.

### Skillnader i fråga om autentisering {#differences-with-regards-to-authentication}

Skillnaderna när det gäller autentisering beskrivs nedan.

#### Dedikerad blandningstyp för autentiseringskrav {#dedicated-mixin-type-for-authentication-requirement}

I den tidigare implementeringen utlöstes både auktoriserings- och autentiseringsaspekterna för en CUG av en enda JCR-egenskap ( `cq:cugEnabled`). När det gäller autentisering resulterade detta i en uppdaterad lista över autentiseringskrav som lagrats med implementeringen av Apache Sling Authenticator. I och med den nya implementeringen uppnås samma resultat genom att målnoden markeras med en dedikerad blandningstyp ( `granite:AuthenticationRequired`).

#### Egenskap för att exkludera inloggningssökväg {#property-for-excluding-login-path}

Med mixin-typen definieras en enda valfri egenskap som kallas `granite:loginPath`, som i stort sett motsvarar `cq:cugLoginPage` -egenskap. Till skillnad från den tidigare implementeringen kommer egenskapen för inloggningssökväg endast att respekteras om dess deklarerande nodtyp är den ovannämnda mixin. Om du lägger till en egenskap med det namnet utan att ange blandningstypen får det ingen effekt och varken ett nytt krav eller ett undantag för inloggningssökvägen rapporteras till autentiseraren.

#### Privilegium för autentiseringskrav {#privilege-for-authentication-requirement}

Du måste lägga till eller ta bort en blandningstyp `jcr:nodeTypeManagement` privilegium beviljas. I den tidigare implementeringen är `jcr:modifyProperties` Privilegium används för att redigera den kvarvarande egenskapen.

Till `granite:loginPath` gäller att samma behörighet krävs för att lägga till, ändra eller ta bort egenskapen.

#### Målnod definierad av blandningstyp {#target-node-defined-by-mixin-type}

Autentiseringskrav förväntas skapas på JCR-noden som definierar det underträd som ska genomgå obligatorisk inloggning. Detta är sannolikt en AEM sida om CUG förväntas påverka hela trädet och användargränssnittet för den nya implementeringen kommer därför att lägga till blandningstypen för auth-krav på sidnoden.

Om du bara placerar CUG-principen vid jcr:content-noden som finns under en viss sida begränsas bara åtkomsten till innehållet, men det påverkar inte själva sidnoden eller underordnade sidor.

Detta kan vara ett giltigt scenario och är möjligt med en databasredigerare som tillåter att mixin placeras på valfri nod. Beteendet står dock i kontrast till den tidigare implementeringen, där en cq:cugEnabled- eller cq:cugLoginPage-egenskap placerades internt på jcr:content-noden. Mappningen utförs inte längre.

#### Konfigurerade sökvägar som stöds {#configured-supported-paths}

Båda `granite:AuthenticationRequired` blandningstyp och egenskapen granite:loginPath respekteras endast inom det omfång som definieras av uppsättningen **Banor som stöds** konfigurationsalternativ finns med **Autentiseringskrav och hanterare för inloggningssökväg för Adobe Granite**. Om inga sökvägar anges är funktionen för autentiseringskrav inaktiverad helt. I det här fallet börjar blandningstyp eller -egenskap gälla när den läggs till eller ställs in på en viss JCR-nod.

### Mappning av JCR-innehåll, OSGi-tjänster och konfigurationer {#mapping-of-jcr-content-osgi-services-and-configurations}

Dokumentet nedan innehåller en omfattande mappning av OSGi-tjänster, konfigurationer och databasinnehåll mellan den gamla och den nya implementeringen.

CUG-mappning sedan AEM 6.3

[Hämta fil](assets/cug-mapping.pdf)

## Uppgradera CUG {#upgrade-cug}

### Befintliga installationer som använder den inaktuella CUG-filen {#existing-installations-using-the-deprecated-cug}

Den gamla CUG-supportimplementeringen har tagits bort och kommer att tas bort i framtida versioner. Vi rekommenderar att du går över till de nya implementeringarna när du uppgraderar från versioner äldre än AEM 6.3.

Vid uppgradering AEM installation är det viktigt att se till att endast en CUG-implementering är aktiverad. Kombinationen av det nya och det gamla, föråldrade CUG-stödet testas inte och kommer troligen att orsaka oönskat beteende:

* kollisioner i Sling Authenticator med avseende på autentiseringskrav
* nekad läsåtkomst när ACL-inställningen som är kopplad till en gammal CUG kolliderar med en ny CUG-princip.

### Migrerar befintligt CUG-innehåll {#migrating-existing-cug-content}

Adobe tillhandahåller ett verktyg för migrering till den nya CUG-implementeringen. Utför följande steg om du vill använda den:

1. Gå till `https://<serveraddress>:<serverport>/system/console/cug-migration` för att komma åt verktyget.
1. Ange den rotsökväg som du vill kontrollera användargränssnitten för och tryck på **Utför torr körning** -knappen. Detta söker efter kundenheter som är berättigade till konvertering på den valda platsen.
1. När du har granskat resultatet trycker du på **Utför migrering** för att migrera till den nya implementeringen.

>[!NOTE]
>
>Om du stöter på problem är det möjligt att konfigurera en specifik loggare på **FELSÖKNING** nivå på `com.day.cq.auth.impl.cug` för att få fram resultatet av migreringsverktyget. Se [Loggning](/help/sites-deploying/configure-logging.md) om du vill ha mer information om hur du gör detta.
