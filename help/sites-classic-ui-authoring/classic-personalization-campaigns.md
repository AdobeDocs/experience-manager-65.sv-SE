---
title: Campaign Management
seo-title: Campaign Management
description: Kampanjhantering ger digitala marknadsförare möjlighet att leverera personaliserat innehåll och skapa dedikerade upplevelser för besökare. Ni kan samordna era marknadsföringskampanjer över webben, e-post och mobiltjänster och därmed engagera besökarna.
seo-description: Campaign management provides digital marketers the opportunity to deliver personalized content and so create dedicated experiences for visitors. It allows you to orchestrate your marketing campaigns across the web, email and mobile services and so engage your visitors.
uuid: 202d614b-a607-45de-8c24-1ee66b230315
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: e8b70971-4f23-45f8-8c23-e147413243c2
exl-id: d1741525-a475-4a76-bd16-55318023495e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '628'
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
I AEM är varumärken den översta enheten och utgör en samling 
**Kampanjer**.

* **Kampanjer**
En kampanj är en samling individuella 
**Erfarenheter**.

* **Erfarenheter**
Det fokuserade innehållet utgör de olika upplevelserna, som presenteras för besökaren på 
**Pekpunkter**. Det finns flera olika typer av upplevelser:

   * **Lärare**
      [Teaser Pages / Paragrapes](#teasers) används för att styra specifika besökare **Segment** till innehåll som fokuseras på deras intressen.

      Teaser pages can:

      * har en rad alternativ som besökaren kan välja mellan
      * visa endast ett teaser-stycke som är baserat på det specifika besökarsegmentet, Det streckade stycket kan t.ex. vara beroende av besökarens ålder.

      Vanligtvis är en&quot;teaser&quot;-sida en tillfällig åtgärd som varar en viss tid tills den ersätts av nästa&quot;teaser&quot;-sida.

   * **Nyhetsbrev**

      [E-postkommunikation](#emailmarketing) används för att engagera användare och uppmuntra dem att besöka din webbplats. Dessa kan oftast fås i form av ett nyhetsbrev som skickas till **Leads** (som vanligtvis grupperas i **Listor**). **Obs!** Adobe planerar inte att ytterligare förbättra denna kapacitet. Rekommendationen är att [utnyttja Adobe Campaign och integrationen för att AEM](/help/sites-administering/campaign.md).

   * **Adobe Target**

      Detta möjliggör integrering med Adobe Target (tidigare Test&amp;Target), som ger marknadsförarna ett optimeringsverktyg för konverteringswebbplatser med de funktioner som krävs för att kontinuerligt göra sitt onlineinnehåll mer relevant för sina kunder, vilket ger större konverteringsgrad. Adobe Target har ett intuitivt gränssnitt för att utforma och köra tester, skapa målgruppssegment och målinrikta innehåll - allt från ett och samma program.


* **Pekpunkter**

   Det här är kontaktpunkterna mellan besökaren och kampanjen. Kontaktpunkterna är kopplade till de upplevelser ni har skapat.

   För teasers är det till exempel innehållssidan där det teaserstycke finns, för ett nyhetsbrev är det postlistan.

* **Leads**

   Den information som ni har samlat in om era besökare och hur ni kontaktar dem utgör grunden för era leads. **Obs!** Adobe planerar inte att ytterligare förbättra denna kapacitet.

   Rekommendationen är att [utnyttja Adobe Campaign och integrationen för att AEM](/help/sites-administering/campaign.md).

* **Listor**

   Leads grupperas vanligtvis i listor så att du kan vidta kollektiva åtgärder för dem. Obs! **Obs!** Adobe planerar inte att ytterligare förbättra denna kapacitet.

   Rekommendationen är att [utnyttja Adobe Campaign och integreringen för AEM.](/help/sites-administering/campaign.md)

* **Segment**

   Besökare har olika intressen och mål när de besöker en webbplats. Genom att analysera detta utifrån faktorer som aktivitet på webbplatsen, profilinformation som registrerats och aktivitet på andra webbplatser kan du definiera segment. Innehållet kan sedan specifikt anpassas efter besökarens behov och intressen enligt de segment som de matchar.

* **MCM**

   Marketing Campaign Manager (MCM) är en konsol som ger er tillgång till alla funktioner ni behöver för att skapa och kontrollera kampanjer, varumärken, upplevelser, kontaktytor, leads, listor, segment och rapporter.

   Den kan nås från olika platser (märkta som **Kampanjer**), eller med till exempel URL-adressen:

   `http://localhost:4502/libs/mcm/content/admin.html`
