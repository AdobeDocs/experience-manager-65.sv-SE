---
title: Lärare och strategier
seo-title: Lärare och strategier
description: Kampanjerna använder ofta teasers som en mekanism för att locka ett visst segment av besökspopulationen till innehåll som fokuserar på deras intressen. En eller flera lärare definieras för en viss kampanj.
seo-description: Kampanjerna använder ofta teasers som en mekanism för att locka ett visst segment av besökspopulationen till innehåll som fokuserar på deras intressen. En eller flera lärare definieras för en viss kampanj.
uuid: c78ec858-4b0a-48d5-99b2-5ddd9e15183d
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: 7f378b94-5233-4358-8d93-a7b3386df00b
docset: aem65
translation-type: tm+mt
source-git-commit: dc1985c25c797f7b994f30195d0586f867f9b3ee

---


# Lärare och strategier{#teasers-and-strategies}

Kampanjerna använder ofta teasers som en mekanism för att locka ett visst segment av besökspopulationen till innehåll som fokuserar på deras intressen. En eller flera lärare definieras för en viss kampanj.

>[!NOTE]
>
> Teaser-komponenten har ersatts i AEM 6.2. Använd [målkomponenten](/help/sites-authoring/content-targeting-touch.md) i stället.

* **Varumärkessidor** lagras i Campaigns-delen av webbplatsen. Ett varumärke innehåller de enskilda kampanjerna.
* **Kampanjsidor** lagras i Campaigns-avsnittet på webbplatsen. Varje kampanj har en egen sida, där de mer detaljerade definitionerna finns. Behållaren, eller översikten, innehåller också viss information och statistik om de enskilda sidorna för teaser.

Teaser inom AEM består av flera delar:

* **Teaser pages** are stored under the appropriate campaign page and hold the definition of the teaser paragraphs available for each specific campaign. Dessa definitioner används när de teaser-styckena visas. inklusive innehållsvariationer, det segment som ska användas för att välja variations- och förstärkningsfaktor.
* Med **Teaser-komponenten** kan du skapa en instans av ditt specifika teaser-stycke på en innehållssida. Du kan dra teaserkomponenten från sidosparken och sedan ange din teaserdefinition för att skapa ett eget teaserstycke. **** Obs! Teaser-komponenten har ersatts i AEM 6.2. Använd [målkomponenten](/help/sites-authoring/content-targeting-touch.md) i stället.
* **Teaser paragraphs** are actual instances of your teaser within a content page. Dessa locka fram ett segment av besökare till innehåll som fokuserar på deras intressen.
* Sidor där kampanjinnehållet är inriktat på ett specifikt besökarsegment. Vanligtvis leder de smalare styckena besökaren till sådana sidor.

## Strategier {#strategies}

När du lägger till ett teaser-stycke på en sida måste du definiera **strategin**.

Detta gäller om flera scener är tillgängliga för markering när deras tilldelade segment tolkas som de ska. I **strategin** anges sedan ett extra kriterium som används för att välja det teaser som visas:

* **Clickstream-bakgrundsmusik** baseras på de taggar och relaterade taggträffar som finns i besökarens klientkontext (visa hur ofta en besökare har klickat på sidor som innehåller respektive tagg). Träffarna för de taggar som definieras på scensidan jämförs.
* **Slumpmässigt**, för &quot;slumpmässigt&quot; urval. använder den slumpmässiga faktorn som genereras för en sida, som kan ses med [klientkontexten](/help/sites-administering/client-context.md).
* **Först** i listan över lösta segment. Ordningen är densamma som för teasers på kampanjbehållarsidan.

Segmentets [förstärkningsfaktor](/help/sites-administering/campaign-segmentation.md#boost-factor) påverkar även markeringen. Detta är en viktningsfaktor som läggs till i en segmentdefinition för att öka eller minska den relativa sannolikheten för att den väljs.

Processen och de inbördes förhållandena mellan de olika urvalskriterierna illustreras bäst med ett exempel (en metod som också kan användas för att säkerställa att dina lärare når rätt målgrupp).

Om följande segment redan har skapats och tilldelats respektive startfaktor:

| Segment | Förstärkningsfaktor |
|---|---|
| S1 | 0 |
| S2 | 0 |
| S3 | 10 |
| S4 | 30 |
| S5 | 0 |
| S6 | 100 |

Och vi använder följande definitioner av teaser:

<table>
 <tbody>
  <tr>
   <td>Campaign</td>
   <td>Teaser</td>
   <td>Tilldelade segment</td>
   <td>Tilldelade taggar </td>
  </tr>
  <tr>
   <td>C1</td>
   <td>T1</td>
   <td>S1, S2</td>
   <td>Näringsliv, marknadsföring</td>
  </tr>
  <tr>
   <td>C1</td>
   <td>T2 </td>
   <td>S1</td>
   <td><br /> </td>
  </tr>
  <tr>
   <td>C1 </td>
   <td>T3</td>
   <td>S3, S4</td>
   <td><br /> </td>
  </tr>
  <tr>
   <td>C1 </td>
   <td>T4</td>
   <td>S2, S5</td>
   <td><br /> </td>
  </tr>
  <tr>
   <td>C1 </td>
   <td>T5</td>
   <td>S1, S2, S6</td>
   <td>Marknadsföring</td>
  </tr>
  <tr>
   <td>C1 </td>
   <td>T6</td>
   <td>S6</td>
   <td>Företag<br /> </td>
  </tr>
 </tbody>
</table>

Om vi sedan tillämpar detta på en besökare där:

* **S1**, **S2** och **S6** har matchats

* taggen **marketing** har tre träffar
* tagghanteringsföretaget **har 6** träffar

Vi kan se resultatet:

* matchar framgång - kan något av de segment som tilldelats till teaser matchas för den aktuella besökaren?
* förstärkningsfaktor - den högsta förstärkningsfaktorn för alla tillämpliga segment
* clickstream score - den ackumulerade summan för alla tillämpliga taggträffar

som beräknas innan lämplig strategi tillämpas:

<table>
 <tbody>
  <tr>
   <td>Campaign</td>
   <td>Teaser</td>
   <td>Tilldelade segment</td>
   <td>Taggar </td>
   <td>Lyckad matchning?</td>
   <td>Resultatförstärkningsfaktor</td>
   <td>Resultat av Clickstream-bakgrundsmusik </td>
  </tr>
  <tr>
   <td>C1</td>
   <td>T1</td>
   <td>S1, S2</td>
   <td>Näringsliv, marknadsföring</td>
   <td>Ja</td>
   <td>0</td>
   <td>9</td>
  </tr>
  <tr>
   <td>C1</td>
   <td>T2 </td>
   <td>S1</td>
   <td><br /> </td>
   <td>Ja</td>
   <td>0</td>
   <td><br /> </td>
  </tr>
  <tr>
   <td>C1 </td>
   <td>T3</td>
   <td>S3, S4</td>
   <td><br /> </td>
   <td>Nej</td>
   <td><br /> </td>
   <td><br /> </td>
  </tr>
  <tr>
   <td>C1 </td>
   <td>T4</td>
   <td>S2, S5</td>
   <td><br /> </td>
   <td>Ja<br /> </td>
   <td>0<br /> </td>
   <td><br /> </td>
  </tr>
  <tr>
   <td>C1 </td>
   <td>T5</td>
   <td>S1, S2, S6</td>
   <td>Marknadsföring</td>
   <td>Ja</td>
   <td>100</td>
   <td>3</td>
  </tr>
  <tr>
   <td>C1 </td>
   <td>T6</td>
   <td>S6</td>
   <td>Företag</td>
   <td>Ja</td>
   <td>100</td>
   <td>6 </td>
  </tr>
 </tbody>
</table>

Dessa värden används för att bestämma vilka teaser besökaren ska se, beroende på vilken **strategi** som tillämpas på teaserstycket:

<table>
 <tbody>
  <tr>
   <td>Strategi</td>
   <td>Resulterande Teaser</td>
   <td>Kommentarer</td>
  </tr>
  <tr>
   <td>Första</td>
   <td>T5</td>
   <td>Det är bara T5 och T6 som deras segment alla löser sig <i>och</i> de har den högsta förstärkningsfaktorn. Den returnerade listan är i ordningen T5, T6. så att T5 markeras och visas.</td>
  </tr>
  <tr>
   <td>Slumpmässig</td>
   <td>T5 eller T6</td>
   <td>Båda teasers har segment som alla löser sig och samma förstärkningsfaktor. De två teasrarna visas därför i samma proportion.</td>
  </tr>
  <tr>
   <td>ClickStream-bakgrundsmusik</td>
   <td>T6</td>
   <td><p>Segmenten för T1, T4, T5 och T6 kan alla lösas för besökaren. De högre förstärkningsfaktorerna för T5 och T6 utesluter sedan T1 och T4. Det högre klickströms-poängen i T6 resulterar slutligen i att detta väljs.</p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Om det efter upplösningsteknikerna ovan finns flera mätare tillgängliga för markering kommer ett internt urval (slumpmässigt) att markera ett enskilt teaser för visning.
>
>Om strategin till exempel var Clickstream-bakgrundsmusik och T5 hade samma Clickstream-bakgrundsmusik som T6 (dvs. 6 i stället för 3), skulle det interna urvalet (slumpmässigt) användas för att välja en av dessa båda.

Teaser Pages/Paragraphs används för att styra specifika besökarsegment till innehåll som är inriktat på deras intressen. De kan presentera en rad olika alternativ som besökaren kan välja mellan eller visa endast ett steg baserat på det specifika besökarsegmentet. Det streckade stycket kan t.ex. vara beroende av besökarens ålder.

Vanligtvis är en&quot;teaser&quot;-sida en tillfällig åtgärd som varar en viss tid tills den ersätts av nästa&quot;teaser&quot;-sida.

När ni har skapat ert varumärke och er kampanj kan ni skapa och skapa en läroupplevelse.

### Skapa en kontaktyta för din Teaser {#creating-a-touchpoint-for-your-teaser}

>[!NOTE]
>
> Teaser-komponenten har ersatts i AEM 6.2. Använd [målkomponenten](/help/sites-authoring/content-targeting-touch.md) i stället.

1. Navigera till innehållssidan där du vill placera det steg som ska leda till kampanjsidan.
1. Lägg till en **Teaser** -komponent (tillgänglig i delen **Personalisering** i sidosparken) i önskad position. När den skapades visas att kampanjsökvägen ännu inte har konfigurerats:

   ![chlimage_1](assets/chlimage_1.png)

1. Redigera teaserkomponenten för att lägga till:

   * **Campaign Path** to the campaign page that contains the individual teaser page; segment avgör exakt vilken teaser som visas.

   * **[Strategisk](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#strategies)**metod som används för markering när flera segment kan matchas.
   ![chlimage_1-1](assets/chlimage_1-1.png)

1. Spara genom att klicka på **OK** . Beroende på vilka segment du har angett för teaser och profilen för den användare du är inloggad som, visas rätt innehåll:

   ![chlimage_1-2](assets/chlimage_1-2.png)

1. För musen över det trasiga stycket för att visa frågetecknet (komponentens nedre högra hörn). Klicka här om du vill visa de segment som används och om de för närvarande löses.

   ![chlimage_1-3](assets/chlimage_1-3.png)

### Teaser Overview {#teaser-overview}

Förutom kampanjvyn i MCM ger kampanjsidan även information om de lärare som är kopplade till den:

1. Öppna kampanjsidan från **webbplatskonsolen** ; till exempel:

   `https://localhost:4502/content/campaigns/geometrixx-outdoors/storefront/summer.html`

   Här visas en översikt över definitioner och visningsstatistik för teaser:

   ![chlimage_1-4](assets/chlimage_1-4.png)
