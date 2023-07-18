---
title: Campaign Management
description: Kampanjhantering ger digitala marknadsförare möjlighet att leverera personaliserat innehåll och skapa dedikerade upplevelser för besökare. Ni kan samordna era marknadsföringskampanjer över webben, e-post och mobiltjänster och därmed engagera besökarna.
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
exl-id: d1741525-a475-4a76-bd16-55318023495e
source-git-commit: ae08247c7be0824151637d744f17665c3bd82f2d
workflow-type: tm+mt
source-wordcount: '623'
ht-degree: 0%

---


# Campaign Management{#campaign-management}

Kampanjhantering ger digitala marknadsförare möjlighet att leverera personaliserat innehåll och skapa dedikerade upplevelser för besökare.

Ni kan samordna era marknadsföringskampanjer över webben, e-post och mobiltjänster och därmed engagera besökarna. Ni kan skapa innehåll, segmentera besökare, pusha och marknadsföra riktat innehåll för specifika användarprofiler och hantera kampanjer i flera kanaler.

I det här dokumentet beskrivs de olika element som utgör kampanjer. Mer detaljerad information finns i följande dokument:

* [Lärare och strategier](/help/sites-classic-ui-authoring/classic-personalization-campaigns-teasers-strategy.md)
* [E-postmarknadsföring](/help/sites-classic-ui-authoring/classic-personalization-campaigns-email.md)
* [Landningssidor](/help/sites-classic-ui-authoring/classic-personalization-campaigns-landingpage.md)
* [Målerbjudanden](/help/sites-classic-ui-authoring/classic-personalization-campaigns-target-offers.md)
* [Arbeta med Marketing Campaign Manager](/help/sites-classic-ui-authoring/classic-personalization-campaigns-mktg-manager.md)
* [Förstå segmentering](/help/sites-classic-ui-authoring/classic-personalization-campaigns-segmentation.md)
* [Konfigurera kampanjen](/help/sites-classic-ui-authoring/classic-personalization-campaigns-setting-up-your.md)

Kampanjhanteringen består av olika delar:

* **Varumärken**
I Adobe Experience Manager (AEM) är varumärken den viktigaste enheten och utgör en samling av **Kampanjer**.

* **Kampanjer**
En kampanj är en samling individuella **Erfarenheter**.

* **Erfarenheter**
Det fokuserade innehållet utgör de olika upplevelserna, som presenteras för besökaren på **Pekpunkter**. Det finns flera olika typer av upplevelser:

   * **Lärare**
     [Teaser Pages / Paragrapes](#teasers) används för att styra specifika besökare **Segment** till innehåll som fokuseras på deras intressen.

     Teaser pages can:

      * har en rad alternativ som besökaren kan välja mellan
      * visar endast ett steg som baseras på det specifika besökarsegmentet. Det streckade stycket kan till exempel vara beroende av besökarens ålder.

     Vanligtvis är en&quot;teaser&quot;-sida en tillfällig åtgärd som varar en viss tidsperiod tills den ersätts av nästa&quot;teaser&quot;-sida.

   * **Nyhetsbrev**

     [E-postkommunikation](#emailmarketing) används för att engagera användare och uppmuntra dem att besöka din webbplats. Dessa kan oftast fås i form av ett nyhetsbrev som skickas till **Leads** (som grupperas i **Listor**). **Obs!** Adobe planerar inte att ytterligare förbättra denna kapacitet. Rekommendationen är att [använda Adobe Campaign och integrationen för att AEM](/help/sites-administering/campaign.md).

   * **Adobe Target**

     Detta möjliggör integrering med Adobe Target (tidigare Test&amp;Target), som ger marknadsförarna ett optimeringsverktyg för konverteringswebbplatser med de nödvändiga funktionerna för att kontinuerligt göra sitt onlineinnehåll mer relevant för sina kunder, vilket ger större konverteringsgrad. Adobe Target har ett intuitivt gränssnitt för att utforma och köra tester, skapa målgruppssegment och målinrikta innehåll från ett och samma program.

* **Pekpunkter**

  Det här är kontaktpunkterna mellan besökaren och kampanjen. Kontaktpunkterna är kopplade till de upplevelser ni har skapat.

  För teasers är det till exempel innehållssidan där det teaserstycke finns, för ett nyhetsbrev är det postlistan.

* **Leads**

  Den information som ni har samlat in om era besökare och hur ni kontaktar dem utgör grunden för era leads. **Obs!** Adobe planerar inte att ytterligare förbättra denna kapacitet.

  Rekommendationen är att [använda Adobe Campaign och integrationen för att AEM](/help/sites-administering/campaign.md).

* **Listor**

  Leads grupperas i listor så att du kan vidta kollektiva åtgärder för dem. Obs! **Obs!** Adobe planerar inte att ytterligare förbättra denna kapacitet.

  Rekommendationen är att [använder Adobe Campaign och integreringen för att AEM.](/help/sites-administering/campaign.md)

* **Segment**

  Besökare har olika intressen och mål när de besöker en webbplats. Genom att analysera detta utifrån faktorer som aktivitet på webbplatsen, registrerad profilinformation och aktivitet på andra webbplatser kan du definiera segment. Innehållet kan sedan anpassas efter besökarens behov och intressen enligt de segment som de matchar.

* **MCM**

  Marketing Campaign Manager (MCM) är en konsol som ger er tillgång till alla funktioner ni behöver för att skapa och kontrollera kampanjer, varumärken, upplevelser, kontaktytor, leads, listor, segment och rapporter.

  Den kan nås från olika platser (märkta som **Kampanjer**), eller med till exempel URL-adressen:

  `http://localhost:4502/libs/mcm/content/admin.html`
