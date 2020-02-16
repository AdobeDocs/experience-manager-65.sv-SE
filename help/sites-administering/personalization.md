---
title: Personalisering
seo-title: Personalisering
description: Läs mer om personalisering i AEM.
seo-description: Läs mer om personalisering i AEM.
uuid: 5790a3e0-f0ec-4785-b915-330a10dea30c
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: 03ebc494-8baa-4741-b8de-dac5ace743c8
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Personalisering{#personalization}

## Vad är personalisering? {#what-is-personalization}

Det finns en allt större mängd innehåll idag, oavsett om det gäller webbplatser på internet, extranät eller intranät.

Personalisering handlar om att ge användaren en skräddarsydd miljö med dynamiskt innehåll som väljs ut utifrån deras specifika behov. baseras på fördefinierade profiler, användarval eller interaktivt användarbeteende.

Personaliseringen består av tre huvuddelar:

**Användare**

* har profiler, både enskilda och grupper. Dessa profiler innehåller egenskaper (t.ex. jobbbeskrivning, plats, intressen) som kan användas för att anpassa innehållet som de kan se.
* vidta åtgärder. Dessa kan sedan analyseras och matchas mot beteenderegler för att skräddarsy det innehåll de ser.

**Innehåll**

* är vad användaren vill se. Innehåll av intresse och användning för dem när de utför sina uppgifter.
* kan kategoriseras och därför göras tillgängliga för användare enligt fördefinierade regler.måste vara dynamiska, med andra ord innehållet
* måste på något sätt vara beroende av användaren - om alla användare ser samma innehåll blir personaliseringen överflödig.

**Regler**

* definiera hur personalisering faktiskt sker - vilket innehåll användaren kan se och när.

Personalisering kan antingen vara:

**Specifik**

* Anpassning: där användaren gör val från ett urval av innehållskällor.

**Implicit**

* Regelbaserade: Företagsledare definierar specifika regler för åtgärder baserat på specifika profiler och/eller beteenden.
* Enkel filtrering: val görs utifrån fördefinierade profiler på användar- och/eller gruppnivå.
* Samverkande/rekommendationsfiltrering: användarbeteendet registreras enligt fördefinierade regler. Dessa regler bygger på beteenden som observeras med likasinnade individer. Den insamlade informationen används för att anpassa den information som visas för användaren, särskilt i form av rekommendationer.

## Hur och när kan personalisering användas? {#how-and-when-can-personalization-be-used}

Personalisering kan användas i många fall, till exempel:

**Intranätsidor**

* Innehåll kan erbjudas baserat på en användares plats, avdelning och/eller roll, som redan definierats i ett internt nätverk.
* Beroende på vilket alternativ som är tillgängligt kan användaren göra fler val.

**Specifika, begränsade målanvändargrupper (extranät)**

* Användarna måste logga in för att kunna godkänna. Detta kommer att kopplas till en profil som tillhandahåller den information som krävs för personalisering. möjliga detaljer som plats, relation till produkten, användningshistorik, budgeteringsansvar osv.
* Sådana instanser kan variera mellan webbplatser som:
* Företag som tillhandahåller webbplatser till en mycket specialiserad del av sin marknad, t.ex. ett läkemedelsföretag som tillhandahåller en specialiserad webbplats för läkare.
* Företag som tillhandahåller webbplatser som gör det möjligt för sina kunder att se aktuell konto- och faktureringsinformation. till exempel telefonleverantörer.

**Försäljnings- och distributionswebbplatsen**

* Försäljnings- och distributionswebbplatser, som Amazon, kan kombinera en användarprofil, användarens försäljningshistorik och användarens webbhistorik för att ge förslag på vad som kan intressera användaren härnäst.

**Sök på webbplatser**

* Många av de stora sökmotorwebbplatserna har mycket kraftfulla analysverktyg som registrerar användarbeteende, söktermer de använder och de webbplatser de faktiskt besöker. Det används sedan för att anpassa innehållet - särskilt när det gäller att visa annonser.

### Styrka personalisering och punkter att tänka på {#strengths-of-personalization-and-points-to-consider}

Följande är skäl till att personalisering bör användas:

* En användare kan uppleva en bekväm och fokuserad webbplats.
* Personalisering kan användas för att automatiskt sprida åtkomst till den senaste versionen av innehåll.
* Funktioner för socialt samarbete är tillgängliga så att användarna kan kommunicera med varandra, eftersom de kan identifieras av sina profiler.
* En användare kan få det innehåll de behöver för att utföra en viss uppgift. I ett företags intranät kan detta vara ett värdefullt verktyg för att sprida information.
* Användarna kan få det innehåll de behöver/vill ha, vilket minskar tiden de behöver utföra sökåtgärder.
* Innehållsleverantören kan styra innehållet så att det kan ses av specifika användarkategorier.
* Regler kan definieras för att leverera innehåll baserat på kombinationer av både användaregenskaper och -beteende. Detta är en sofistikerad mekanism för att personalisera sin webbupplevelse.

Tänk på följande när du använder personalisering:

**Prestanda**

* Den extra analysen och utvärderingen påverkar naturligtvis resultatet. De metoder som används är dock mycket avancerade och kan optimeras för att minimera påverkan.

**Behörighet**

* Personalisering kräver en inloggningsfunktion eftersom webbplatsen måste kunna identifiera användaren.

**Cachelagring**

* Cachelagring är en aspekt som användaren kommer att se när det gäller prestanda och precision - hur snabbt levererar webbplatsen personaliserat innehåll, och är det alltid aktuellt.
* Cachelagring är en viktig faktor när personalisering konfigureras och man måste se till att rätt implementering används. Detta kommer att diskuteras mer ingående senare.

**Regelernas exakthet**

* Personalisering som uppnås genom att spåra användarens beteende, eller genom att ställa in regler som baseras på användarens profil, måste vara korrekt och logiskt.
* Det finns inget som är mer frustrerande för användaren än att ha innehåll som tvingats på eller nekats till dem på grund av den felaktiga logiken i en regel.
* Därför måste regler vara väl genomtänkta - med användarens krav i förgrunden. Detta kan kräva mycket arbete och ska inte underskattas. Att definiera affärsreglerna uppväger ofta den tekniska ansträngningen vid personalisering.

**När ska användas**

* Precis som många andra funktioner på webben bör personalisering användas med försiktighet. Kommer användandet verkligen att gynna användaren? ska alltid vara det första övervägandet - eller om det önskade målet kan uppnås med mindre ansträngning med en annan metod. Personalisering kan innebära en risk att användaren konfigurerar en funktion (för att se hur den fungerar) och bara en gång - eftersom den inte ger några verkliga fördelar.
* Personalisering är bara meningsfullt när innehållet är dynamiskt - beroende på användaren på något sätt. Om alla användare ser samma innehåll är personaliseringen överflödig.

**Sekretess**

* Många användare är oroade över dataskydd och -säkerhet. Särskilt när det gäller data som hämtats när de spåras när de surfar på webben.

## Personalisering och åtkomst {#personalization-and-access}

Personalisering bör beaktas separat från åtkomstkontroll, men de har en inbördes relation.

Personalisering i sig skapar inte någon form av åtkomstkontroll. Det är helt enkelt ett sätt att styra vad användaren ser. det förhindrar inte användaren från att få åtkomst till annat innehåll, och precis som med allt innehåll måste de ha rätt åtkomstkontroller tilldelade.

Åtkomstkontroll kan dock användas för att skapa en form av personalisering. Om du tillåter eller nekar en användare åtkomst till innehåll påverkar detta oundvikligen valet av innehåll som han/hon har tillgängligt, vilket innebär att hans/hennes webbupplevelse anpassas.

## Komponenter tillgängliga för personalisering {#components-available-for-personalization}

Olika komponenter ingår i AEM för personalisering. Vissa tillåter användare att logga in och redigera sina profiler, andra (som Mina gadgets) tillåter användarna att konfigurera en viss sida:

| Title in Sidekick | Syfte |
|---|---|
| Kontrollerat lösenordsfält | Begär lösenord och bekräftelse av lösenord. |
| Kombinerad inloggningsregistrering | Låter användaren antingen logga in på ett befintligt konto eller registrera sig för ett nytt konto. |
| Formuläradressfält | Ett komplext fält som tillåter inmatning av en internationell adress. |
| Formulär börjar | Startar en formulärdefinition |
| Forms Captcha | Ett fält som består av ett alfanumeriskt ord som uppdateras automatiskt. Captcha-komponenten skyddar webbplatser mot stötar. |
| Kryssrutegrupp för formulär | Flera objekt ordnade i en lista och föregås av kryssrutor. Användarna kan markera flera kryssrutor. |
| Listruta för formulär | Flera objekt är ordnade i en nedrullningsbar lista. Växeln Flervalbar anger om flera element kan väljas i listan. |
| Formulärslut | Avslutar formulärdefinitionen. |
| Filöverföring med formulär | An upload element that allows the user to upload a file to the server. |
| Formulär - dolt fält | Det här fältet visas inte för användaren. Den kan användas för att överföra ett värde till klienten och tillbaka till servern. Fältet ska inte ha några begränsningar. |
| Knappen Formulärbild | En extra Skicka-knapp för formuläret som återges som en bild. |
| Formulärlösenordsfält | Samma som textfält, men bara en rad tillåts och textinmatningen från användaren visas inte i fältet. |
| Formuläralternativknappar | Flera objekt ordnade i en lista föregås av en alternativknapp. Användare får bara välja en alternativknapp. |
| Knappen Skicka formulär | En extra Skicka-knapp för formuläret där titeln visas som text på knappen. |
| Formulärtextfält | Textfält där användarna kan ange information. |
| Mina gadgets | Gör att du kan ta med en av flera tillgängliga gadgets. |
| Profil Avatar Photo | Tillåter indata från ett Avatar-foto. |
| Detaljerat profilnamn | Ange namndetaljer, inklusive element som titel, mellannamn och suffix om det behövs. |
| Profilvisningsnamn | Namn som ska visas. |
| Profil-e-post | Ange en e-postadress. |
| Profilkön | Tillåter indata för kön. |
| Primärt telefonnummer för profil | Tillåter inmatning av ett telefonnummer. |
| Primär URL för profil | Tillåter indata för en URL. |
| Profil, allmän text, egenskap | Profilegenskaper. |
| Logga in | Gör att du kan skicka ett användarnamn och lösenord när du loggar in. |
| Logga ut | Anger användaren som är inloggad och ger dig en länk för att logga ut. |
| Tag Cloud | Ett taggmoln som visar ett grafiskt presenterat urval av taggar på webbplatsen |
| Teaser | Ett innehåll (vanligtvis en bild) som visas på en huvudsida för att&quot;lura&quot; användarna att komma åt det underliggande innehållet. |

## Personalisering och communityinnehåll {#personalization-and-community-content}

Community-funktioner som bloggar, forum och kalendrar resulterar i att användargenererat innehåll skapas, vilket ofta kallas användargenererat innehåll (UGC). När UGC anges i en publiceringsmiljö som består av flera AEM-instanser (en [publiceringsgrupp](/help/communities/topologies.md)) har ett stort problem varit hur UGC ska synkroniseras i alla instanser.

Med tillägget [AEM Communities 6.1](/help/communities/overview.md) löses problemet genom att en [gemensam butik för UGC](/help/communities/working-with-srp.md)används. När det gäller personalisering omfattar Communities [Social Login](/help/communities/social-login.md) - möjlighet att ge besökare möjlighet att logga in med Facebook och Twitter.

Utan Communities-tillägg kan olika metoder för att undersöka frågan om enhetlighet i användargenererat innehåll vara:

* synkronisera flera publiceringsinstanser vid behov
* skicka användargenererat innehåll från publiceringsinstansen till författarmiljön, varifrån det kan publiceras på ett sätt som liknar publicering av sidinnehåll

Den metod som används för att uppnå enhetlighet i användargenererat innehåll i en publiceringsmiljö som består av flera publiceringsinstanser bör utformas noggrant och testas med avseende på prestanda och konsekvens.
