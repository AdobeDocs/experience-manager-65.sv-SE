---
title: Bästa praxis för översättning
seo-title: Bästa praxis för översättning
description: Här hittar du de bästa metoderna från Adobes tekniker och konsultteam som hjälper dig att komma igång med översättningsprojekt.
seo-description: Här hittar du de bästa metoderna från Adobes tekniker och konsultteam som hjälper dig att komma igång med översättningsprojekt.
uuid: 3bac1d73-9696-4c9b-8bdd-6f00fac40cf7
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 1554010e-a1d1-4edf-b28f-9eead8f83b4a
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Bästa praxis för översättning{#translation-best-practices}

## Allmänt {#general}

Att skapa eller utöka en global webbnärvaro kan vara en komplex process, men med god planering kan AEM förenkla arbetet och hjälpa er att nå era globala affärsmål.

* **Planera för global expansion** innan du implementerar din första plats. Att anpassa en befintlig webbplats för global täckning när webbplatsen implementerades med kort varsel är vanligtvis svårare än att planera för global expansion i början:

   * Utvärdera det aktuella läget för organisationens lokaliseringslösning. Bestäm om du har **verktyg**, **processer** och **resurser** på plats för att stödja global expansion.
   * Var uppmärksam på **globala regler** och **regionala språkinställningar**. Designa flexibla innehållsstrukturer och processer som kan hantera en föränderlig global affärsmiljö.

* Fastställ en **styrningsmodell** som stöder er globala verksamhet och använd AEM-mekanismer som MSM och användarbehörigheter för att tillämpa den valda modellen. Du kan till exempel avgöra om innehållet ska redigeras centralt och&quot;pushas&quot; eller&quot;hämtas&quot; till regioner/länder. Bestäm vilket innehåll som kan låsas upp och ändras i olika geografiska områden. Bestäm vem som ansvarar för att initiera och hantera översättningar.
* Om resurserna tillåter är det bäst att hantera översättningsaktiviteter från ett centralt team som kan utveckla expertis i de verktyg, processer och leverantörsrelationer som behövs.
* **Planera**, **skapa prototyper** och **testa** er globala struktur och processer för att se till att de stöder verksamheten och att ni har den support som krävs från intressenter i olika länder.

## Webbplatsstruktur {#site-structure}

* När du utformar webbplatsstrukturen börjar du med att undersöka ditt innehåll och avgör var och på vilket språk innehållet skrivs. Platsen bör vara den översta nivån på din plats.
* Det bästa sättet är en **språkbaserad struktur** som inte har mer än tre nivåer mellan den översta nivån och landsplatser.
* Använd en namngivningskonvention för språk/land som följer **W3C-standarder**.
* Bestäm hur innehållet ska distribueras mellan regioner och länder. Tänk på vilka länder som delar språk. Vi rekommenderar att du skapar språkmallsidor, ett lager med oaktiverade sidor, där översatt innehåll kan granskas och ändras och sedan pushas eller dras till en landsplats där det språket delas.
* Det finns två sätt att skapa språkmallar: använda språkkopior och använda MSM/live-kopior.

   * Det är den som används av AEM:s körklara ramverk för översättningsintegrering, och därför är det enklaste sättet att komma igång. Ramverket har ett användargränssnitt som gör det till att börja med enkelt att sprida och översätta innehållsändringar från huvudspråket (t.ex. engelska) till språkmallsidor. I takt med att projektet växer blir det dock allt viktigare att automatisera arbetsflödet för att hantera översättningen av det ökade antalet sidor och/eller språk.
   * Metoden med MSM/live-kopia kan vara ett alternativ för avancerad användning, där webbplatser är större och mer komplexa. Stabil styrning och automatisering av arbetsflöden krävs från början för att hantera komplexa arvsrelationer mellan engelska och språkmallsidor och för att minska risken för att skriva över befintliga översättningar. Den här hanteringen kan utföras med hjälp av vissa översättningskontakter. Mer information finns i [MSM och flerspråkiga webbplatser](/help/sites-administering/msm-best-practices.md#msm-and-multilingual-websites) .

* Om huvudspråket har globala variationer är ett alternativ att använda MSM för att skapa en live-kopia från den globala mallsidan för översättning. Om global redigering till exempel utförs i en amerikansk engelsk master skapar du en internationell engelsk master som en live-kopia och bas för översättning till andra språk.
* Använd MSM för att skapa landsplatser från översatta språkmallar och för att lansera innehåll på webbplatser som delar samma språk. Den franska huvudpersonen kan till exempel läggas ut på webbplatser i Frankrike, Belgien och Schweiz.
* Planera, skapa prototyper och testa först, innan implementeringen startas.

## Översättningsprocesser och metoder {#translation-processes-and-methods}

* Engagera en **lokaliseringstjänsteleverantör (LSP)** med expertis inom översättning och tillhörande lokaliseringsaktiviteter. LSP-leverantörer kan hjälpa er att skalförändra er globala verksamhet genom att tillhandahålla en rad resurser och tekniker som förbättrar effektiviteten och sparar översättningskostnader:

   * Vissa leverantörer av lågprisleverantörer är både tjänste- och teknikleverantörer. Det finns också fristående teknikleverantörer som tillåter många lågprisleverantörer att delta i deras översättningsplattformar.
   * AEM **Translation Framework** stöder integrering med en mängd olika leverantörer av översättningsteknik för både maskinöversättning och mänsklig översättning.
   * Lär dig hur du [integrerar LSP-anslutningar i ditt AEM-system](/help/sites-administering/translation.md) för att automatisera innehållsöversättning, eller hur du manuellt skapar, exporterar och importerar översättningsprojekt för testning och i de fall där det inte finns någon leverantör av LSP- eller översättningsteknik.

* Välj den **översättningsmetod** som bäst passar innehållet.

   * **Översättning** av människor passar bäst för innehåll där meddelanden och kvalitetskrav är höga och där innehållet kommer att finnas kvar en tid på webbplatsen, till exempel på marknadsföringssidor.
   * **Maskinöversättning** kan vara ett bra val för massvolymer av översättning när publiceringstiden är viktig, kvalitetsförväntningarna är avspända eller personalens översättningskostnader är oöverkomliga. Support-kunskapsbasen och användargenererat innehåll är vanligtvis maskinöversatta.

* Använd expertis från lokaliseringsleverantörer, Adobe Consulting och systemintegratörer för att planera, skapa prototyper och testa din flerspråkiga webbplatsstruktur.

