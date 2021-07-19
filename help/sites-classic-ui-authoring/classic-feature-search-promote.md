---
title: Lägga till Search & Promote på sidan
seo-title: Lägga till Search & Promote på sidan
description: När du integrerar Search & Promote på din webbplats kan du använda komponenterna i Search & Promote för att lägga till funktioner på dina sidor, t.ex. nyckelordssökning, förfining av sökresultatsidor och banners.
seo-description: När du integrerar Search & Promote på din webbplats kan du använda komponenterna i Search & Promote för att lägga till funktioner på dina sidor, t.ex. nyckelordssökning, förfining av sökresultatsidor och banners.
uuid: 8cd3c143-cb0b-4eb0-931d-9d447ea3c950
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 968b9131-ccdf-4856-b504-bc1a44974980
docset: aem65
exl-id: cf5849c7-1c6a-46d8-9cc4-f1f20a507a0c
source-git-commit: f4b7566abfa0a8dbb490baa0e849de6c355a3f06
workflow-type: tm+mt
source-wordcount: '1218'
ht-degree: 0%

---

# Lägga till Search &amp; Promote på sidan{#adding-search-promote-features-to-your-page}

Om du vill integrera Search &amp; Promote på din webbplats använder du komponenterna i Search &amp; Promote för att lägga till följande funktioner på dina sidor:

* Nyckelordssökning
* Sökresultatsida
* Sökförfining
* Banderoller

Du kan bara använda Search &amp; Promote om Adobe Experience Manager-administratören har aktiverat dem. Se [Integrera med Adobe Search &amp; Promote](/help/sites-administering/search-and-promote.md).

Ansikten konfigureras på Search &amp; Promote, liksom den information som varje komponent tillhandahåller. Följande tabell innehåller en kort beskrivning av varje komponent. Efterföljande avsnitt innehåller detaljerad information om hur de används.

<table>
 <tbody>
  <tr>
   <th>Search &amp; Promote-komponent</th>
   <th>Beskrivning</th>
  </tr>
  <tr>
   <td>Banderoller</td>
   <td>Visar banderollannonser. Banderoller väljs baserat på data som samlats in via Search &amp; Promote.<br /> </td>
  </tr>
  <tr>
   <td>Breadcrumbs</td>
   <td>Visar söknyckelordet och den filtersekvens som användaren har tillämpat på sökresultaten.</td>
  </tr>
  <tr>
   <td>Kryssrutelista-Fasett</td>
   <td>En lista med kryssrutor för att välja aspekter för filtrering av sökresultat.</td>
  </tr>
  <tr>
   <td>Listrutefrekvens</td>
   <td>En nedrullningsbar lista med aspekter för filtrering av sökresultat.</td>
  </tr>
  <tr>
   <td>Länklistefaktor</td>
   <td>En lista med facet-länkar för filtrering av sökresultat.</td>
  </tr>
  <tr>
   <td>Sidnumrering</td>
   <td>Kontroller för navigering i sökresultatsidor.</td>
  </tr>
  <tr>
   <td>Resultat</td>
   <td>Visar resultatet av en nyckelordssökning.</td>
  </tr>
  <tr>
   <td>Sökning</td>
   <td>Lägger till ett sökfält på sidan.</td>
  </tr>
 </tbody>
</table>

## Skapa sidan med sökresultat {#creating-the-search-results-page}

Använd WCM-webbplatskonsolen för att skapa en sida för att visa sökresultat. Resultatet av en sökning från en sökkomponent kan visas på den här sidan om samma Search &amp; Promote används.

De komponenter som gör det möjligt för användare att granska sökresultat är Resultat och Sidnumrering. Komponenten **[!UICONTROL Results]** har inga konfigurerbara egenskaper i redigerings- eller designläge. Komponenten Results visar bara sökresultaten, som innehåller länkar till andra sidor, och visar antalet resultat för söknyckelordet.

![srchresultatscomp](assets/srchresultscomp.png)

Med komponenten **[!UICONTROL Pagination]** kan användare navigera i flera sidor med sökresultat. Användaren kan se antalet sidor, gå till nästa eller föregående sida, välja en sida som ska öppnas eller sammanställa alla resultat på en sida.

![sidnumrering](assets/srchpagination.png)

Du kan konfigurera följande komponentegenskaper i redigeringsläget för att styra körningsbeteendet:

* Dölj enstaka resultatsida: Välj det här alternativet om du vill dölja sidnavigeringskontrollerna när sökningen returnerar en enda resultatsida.
* Dölj första/sista: Välj det här alternativet om du vill förhindra att användare hoppar till första eller sista resultatsidan.
* Dölj föregående/nästa: Avgör om användare kan navigera på resultatsidor i förhållande till den aktuella sidan.
* Dölj vy för alla: Avgör om användaren kan konsolidera alla sökresultat på en enda sida. Vanligtvis blir användningen av serverresurser effektivare om du tillhandahåller växlingsdata. Välj det här alternativet om du vill förhindra överföring av stora datauppsättningar i ett svarsmeddelande.

### Aktivera filtrering av resultat efter aspekter {#enabling-the-filtering-of-results-by-facets}

Du kan göra det möjligt för användare att filtrera sökresultat efter aspekter. Med komponenterna **[!UICONTROL Checkbox List Facet]**, **[!UICONTROL Dropdown Facet]** och **[!UICONTROL Link List Facet]** kan användarna välja en eller flera aspekter för filtrering. När du använder de här komponenterna bör du även ta med komponenten **Breadcrumbs**. Bläddringarna anger vilka filter som används.

Komponenterna **[!UICONTROL Checkbox List Facet]**, **[!UICONTROL Dropdown Facet]** och **[!UICONTROL Link List Facet]** har båda följande egenskaper som du konfigurerar i läget **Redigera**:

* **Fasettnamn**: Namnet på det facet som används för filter.

Komponenten **[!UICONTROL Checkbox List Facet]** visar en lista med ansikten med en medföljande kryssruta. Använd en **[!UICONTROL Checkbox List Facet]** så att användarna kan visa en delmängd av resultaten som innehåller objekt från flera aspekter. Metoden **Brand** är lämplig eftersom flera varumärken använder samma typ av produkt.

En kryssruta visas för varje aspekt som är associerad med ett sökresultat. När en användare markerar en kryssruta, läses sidan in igen med en uppdaterad resultatuppsättning. Alla kryssrutor finns kvar på sidan så att kunderna kan lägga till eller ta bort ansikten i filtret när som helst:

![sandpcheckbox comp](assets/sandpcheckboxcomp.png)

Med komponenten **[!UICONTROL Dropdown Facet]** kan kunderna välja ett sidobjekt i en nedrullningsbar lista. Den här komponenten är användbar när du vill att kunderna ska fokusera på ett enda sidobjekt samtidigt. Avdelningsaspekten är till exempel lämplig för att göra det möjligt för kunderna att begränsa produktsökningar efter kön. John söker efter *jeans* och filtrerar sedan på Män-avdelningen.

Listrutan fylls i med de aspekter som är associerade med alla sökresultat. När du väljer ett objekt i listrutan läses sidan in igen med en uppdaterad resultatuppsättning. Objekten i listrutan ändras inte så att kunderna när som helst kan växla från aspekten till aspekten.

![sandpdropdown-avdelning](assets/sandpdropdowndepartment.png)

Med **[!UICONTROL Link List Facet]**-komponenten kan kunderna stegvis begränsa sitt fokus till objekt som är kategoriserade under flera fasmedlemmar eller facets.

Fasettmedlemmar visas som en lista med länkar. Texten för varje länk är namnet på en fasmedlem som är associerad med det aktuella sökresultatet. När en kund klickar på en facet-länk läses sidan in igen och en delmängd av sökresultaten visas. Listan med länkar uppdateras för att ge ännu mindre fokus.

![sandplinklistcomp](assets/sandplinklistcomp.png)

Länkarna i listan ändras också när ett filter tillämpas från en annan typ av Search &amp; Promote-komponent. Användning av flera typer av filterkomponenter kan ge effektiva filterkombinationer.

Komponenten **[!UICONTROL Breadcrumbs]** gör det möjligt för kunder att se de filter som för närvarande tillämpas på sökresultaten i den ordning som de tillämpades. Kunder kan klicka på objekten i den synliga sökvägen för att återgå till den filterkombinationen.

![sandpbreadcrumbcomp](assets/sandpbreadcrumbcomp.png)

Du kan konfigurera följande egenskaper för vägbeskrivningar i redigeringsläget för att anpassa komponentens utseende:

* Avgränsare: Definiera det tecken eller den teckensträng som ska fungera som avgränsare mellan varje vägbeskrivningsknapp. I fältet **[!UICONTROL Delimiter]** accepteras alla teckensträngar som indata. Standardinställningen är: &quot;>&quot; (utan citattecken)
* Avgränsare: Definiera ett tecken eller en teckensträng som ska visas i slutet av kolumnmarginalerna. I fältet **[!UICONTROL Trailing Delimiter]** accepteras alla teckensträngar som indata. Standardinställningen för det här fältet är *blank* (d.v.s. inget visas i slutet av den synliga raden)

### Lägg till sökrutor {#adding-search-boxes}

Med komponenten **[!UICONTROL Search]** kan kunderna utföra nyckelordssökningar. Lägg till **[!UICONTROL Search]**-komponenter på varje sida där du vill ge åtkomst till sökning.

Konfigurera följande egenskaper i redigeringsläget så att du kan styra körningsbeteendet:

* Sökväg till resultatsida: Sökvägen till sidan som visar sökresultaten.
* Aktivera Komplettera automatiskt: Välj det här alternativet om du vill att föreslagna söknyckelord ska visas när kunden börjar skriva i sökrutan.

![sandpsearchcomp](assets/sandpsearchcomp.png)

### Lägg till banners {#adding-banners}

Komponenten **[!UICONTROL Banners]** visar banderollannonser enligt kundens sökningar efter Search &amp; Promote. Logiken på Search&amp;Replace-servern avgör vilken banderoll som ska visas. En sökning på jeans kan till exempel få en moderelaterad banderoll att visas. Filtrering på Men&#39;s Department kan ytterligare förfina valet av banderoll.

Komponenten **[!UICONTROL Banners]** innehåller en konfigurerbar egenskap med namnet Banner Area. I redigeringsläget väljer du ett av egenskapsvärdena för att ange hur banderollen ska visas. Search &amp; Promote avgör vilka värden du kan välja från.

### Exempel på söksida för Search &amp; Promote {#example-search-promote-search-page}

I följande diagram visas de komponenter som har lagts till på en Search &amp; Promote för att skapa den fullt fungerande resultatsidan nedan.

![1328213789109](assets/1328213789109.png) ![Exempel på sandpapper](assets/sandppageexample.png)
