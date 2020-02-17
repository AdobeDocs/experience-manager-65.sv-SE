---
title: Metodtips för e-postmallar
seo-title: Metodtips för e-postmallar
description: Lär dig de bästa sätten att skapa e-postmallar i AEM.
seo-description: Lär dig de bästa sätten att skapa e-postmallar i AEM.
uuid: 07417a63-7ca6-484c-b55d-57b319428329
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 2418777e-4eb2-4d82-aa9e-8d1b0bf740f3
docset: aem65
translation-type: tm+mt
source-git-commit: bd0cb6abe024bc4ff77c9932c99b816c832377f5

---


# Metodtips för e-postmallar {#best-practices-for-email-templates}

>[!CAUTION]
>
>AEM-e-postkomponenterna har tagits bort. På grund av e-postens natur, som sammanfogar innehåll och format, kommer de e-postkomponenter som tillhandahålls av AEM att ha begränsad återanvändning för kunderna eftersom de måste implementera anpassade format i de komponenter som behövs för projekten.
>
>E-postkomponenter kan implementeras på projektnivå och de inaktuella AEM-e-postkomponenterna visar hur man kan uppnå detta. Dessa inaktuella komponenter bör dock inte användas i projekt.

I det här dokumentet beskrivs några av de bästa sätten att arbeta med e-postdesign, vilket resulterar i en välutvecklad mall för e-postkampanjer.

Demokampanjen i AEM följer alla dessa bästa metoder. Hur de bästa metoderna implementeras i demokampanjen beskrivs för varje bästa praxis.

Använd dessa rutiner när du skapar ett eget nyhetsbrev.

>[!NOTE]
>
>Allt kampanjinnehåll ska skapas under en `master` sida av typen `cq/personalization/components/ambitpage`.
>
>Exempel: Den planerade kampanjstrukturen ser ut ungefär som
>
>`/content/campaigns/teasers/en/campaign-promotion-global`
>
>Du bör se till att den finns under en `master` sida
>
>`/content/campaigns/teasers/master/en/campaign-promotion-global`

>[!NOTE]
>
>När du skapar en e-postmall för Adobe Campaign måste du inkludera egenskapen **acMapping** med värdet **mapRecipient** i **jcr:content** -noden i mallen, annars kan du inte välja Adobe Campaign-mallen i **Sidegenskaper** för AEM (fältet är inaktiverat).

## Komponenten Mall/sida {#template-page-component}

***/libs/mcm/campaign/components/campaign_newsletterpage***

<table>
 <tbody>
  <tr>
   <td><strong>Bästa praxis</strong></td>
   <td><strong>Implementering</strong></td>
  </tr>
  <tr>
   <td><p>Ange dokumenttyp för att säkerställa enhetlig återgivning.</p> <p>Lägg till DOCTYPE i början (HTML eller XHTML)</p> </td>
   <td><p>Kan konfigureras genom att designen ändrar egenskapen <i>cq:doctype</i> i<i>"/etc/designs/default/jcr:content/campaign_newsletterpage"</i></p> <p>Standardvärdet är "XHTML":</p> <p>&lt;!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "https://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd"&gt;</p> <p>Kan ändras till "HTML_5":</p> <p>&lt;!DOCTYPE HTML&gt;</p> </td>
  </tr>
  <tr>
   <td><p>Ange teckendefinition för att säkerställa korrekt återgivning av specialtecken.</p> <p>Lägg till CHARSET-deklaration (t.ex. iso-8859-15, UTF-8) till &lt;head&gt;</p> </td>
   <td><p>Är inställd på UTF-8.</p> <p>&lt;meta http-equiv="content-type" content="text/html; charset=UTF-8"&gt;</p> </td>
  </tr>
  <tr>
   <td><p>Koda all struktur med &lt;table&gt;elementet. För mer komplicerade layouter bör du kapsla tabeller för att skapa komplexa strukturer.</p> <p>E-post ska se bra ut även utan CSS.</p> </td>
   <td><p>Tabeller används i hela mallen för att strukturera innehåll. Använder för närvarande maximalt fyra kapslade tabeller (1 bastabell + max). 3 kapslingsnivåer)</p> <p>&lt;div&gt;-taggar används bara i redigeringsläge för att säkerställa korrekt komponentredigering.</p> </td>
  </tr>
  <tr>
   <td>Använd elementattribut (t.ex. cellfyllnad, justering och bredd) för att ange tabelldimensioner. Detta framtvingar en kartongmodellstruktur.</td>
   <td><p>Alla tabeller innehåller nödvändiga attribut som <i>kantlinje</i>, <i>cellfyllnad</i>, <i>cellmellanrum</i> och <i>bredd</i>.</p> <p>För att harmonisera elementplaceringen i tabeller har alla tabellceller attributet <i>valign="top"</i> angetts.</p> </td>
  </tr>
  <tr>
   <td><p>Konto för mobilvänlighet, om möjligt. Använd mediefrågor om du vill öka textstorleken på små skärmar, ange träffområden i ministorlek för länkar.</p> <p>Gör ett e-postmeddelande responsivt om designen tillåter det.</p> </td>
   <td>När det gäller CSS-format som används för att illustrera demodesign används mediefrågor för att erbjuda en mobilvänlig version.</td>
  </tr>
  <tr>
   <td>Inline CSS är bättre än att placera all CSS i början.</td>
   <td><p>För att bättre demonstrera den underliggande HTML-strukturen och förenkla möjligheten att anpassa nyhetsbrevsstrukturen har bara vissa CSS-definitioner infogats.</p> <p>Basformat och mallvarianter har extraherats till ett formatblock på &lt;head&gt; på sidan. När nyhetsbrevet är färdigt ska dessa CSS-definitioner infogas i HTML-koden. En automatisk infogningsmekanism planeras, men är för närvarande inte tillgänglig.</p> </td>
  </tr>
  <tr>
   <td>Gör din CSS enkel. Undvik sammansatta formatdeklarationer, kodförkortningar, CSS-layoutegenskaper, komplexa väljare och pseudoelement.</td>
   <td>När det gäller CSS-format som används för att illustrera demodesign följs CSS-rekommendationerna.</td>
  </tr>
  <tr>
   <td>E-postmeddelanden ska vara högst 600-800 pixlar breda. Detta gör att de beter sig bättre i den storlek på förhandsgranskningsfönstret som många klienter har.</td>
   <td>Innehållstabellens <i>bredd</i> är begränsad till 600 px i demodesign.</td>
  </tr>
 </tbody>
</table>

### Bilder {#images}

/libs/mcm/campaign/components/image

| **Bästa praxis** | **Implementering** |
|---|---|
| Lägg till *alt* -attribut i bilder | Attributet *alt* har definierats som obligatoriskt för bildkomponenten. |
| Använd *jpg* i stället för *png* -format för bilder | Bilderna hanteras alltid som JPG-bilder av bildkomponenten. |
| Använd <img> element i stället för bakgrundsbilder i en tabell. | Inga bakgrundsbilddata används i mallarna. |
| Lägg till attributet style=&quot;display block&quot; i bilder. Tillåter visning bra på Gmail. | Alla bilder innehåller som standard attributet *style=&quot;display block&quot;* . |

### Text och länkar {#text-and-links}

/libs/mcm/campaign/components/heading, /libs/mcm/campaign/components/textimage

<table>
 <tbody>
  <tr>
   <td><strong>Bästa praxis</strong></td>
   <td><strong>Implementering</strong></td>
  </tr>
  <tr>
   <td>Använd html &lt;font&gt; i stället för format i CSS (font-family)</td>
   <td>RichTextEditor (t.ex. i textimagekomponenten) har nu stöd för att välja och använda teckensnittsfamiljer och teckensnittsstorlekar på markerade texter. De återges som &lt;font&gt;-taggar.</td>
  </tr>
  <tr>
   <td>Använd grundläggande plattformsoberoende teckensnitt som <i>Arial, Verdana, Georgia</i> och <i>Times New Roman</i>.</td>
   <td><p>Används för att skapa nyhetsbrev.</p> <p>För demodesignen används teckensnittet "Helvetica", men kommer att återgå till det generiska sans-serif-teckensnittet, om det inte finns något.</p> </td>
  </tr>
 </tbody>
</table>

### Allmän {#generic}

| **Bästa praxis** | **Implementering** |
|---|---|
| Använd W3C-valideraren för att korrigera HTML-koden. Se till att alla öppna taggar stängs ordentligt. | Koden har validerats. För XHTML-övergångsdokument är det bara det saknade xmlns-attributet för <html> element saknas. |
| Stör inte JavaScript eller Flash - teknologierna stöds i stort sett inte av e-postklienter. | Varken JavaScript eller Flash används i nyhetsbrevmallen. |
| Lägg till en oformaterad textversion för att skicka flera delar. | En ny widget skapades i sidegenskaperna för att enkelt extrahera en textversion från sidinnehållet. Detta kan användas som startpunkt för den slutliga versionen av plaintext. |

## Mallar och exempel för kampanjnyhetsbrev {#campaign-newsletter-templates-and-examples}

AEM innehåller flera mallar och komponenter som du kan använda för att skapa nyhetsbrev om kampanjer. Du kan använda de här mallarna och komponenterna för att skapa anpassade nyhetsbrev.

### Templates {#templates}

Det finns tre något olika malltyper att välja mellan för att få en heltäckande bas och för att bredda möjligheterna för innehållsflöde. Du kan enkelt använda dessa för att skapa anpassade nyhetsbrev.

Alla har ett **sidhuvud**, en **sidfot** och ett **textavsnitt** . Under brödavsnittet skiljer sig varje mall i **kolumndesign** (1, 2 eller 3 kolumner).

![](assets/chlimage_1-69.png)

### Komponenter {#components}

Det finns för närvarande [sju komponenter som kan användas i kampanjmallar](/help/sites-authoring/adobe-campaign-components.md). Dessa komponenter är alla baserade på Adobes **HTML-kod**.

| **Komponentnamn** | **Komponentsökväg** |
|---|---|
| Rubrik | /libs/mcm/campaign/components/heading |
| Bild | /libs/mcm/campaign/components/image |
| Text&amp;personalisering | /libs/mcm/campaign/components/personalization |
| Textimage | /libs/mcm/campaign/components/textimage |
| Länk | /libs/mcm/campaign/components/reference |
| Scene7 Image Template | /libs/mcm/campaign/s7image |
| Riktad referens | /libs/mcm/campaign/components/reference |

>[!NOTE]
>
>Dessa komponenter är optimerade för e-postinnehåll; dvs. de följer de bästa praxis som beskrivs i detta dokument. Om du använder andra komponenter som inte finns installerade i systemet bryter det vanligtvis mot dessa regler.

Dessa komponenter beskrivs i detalj i [Adobe Campaign-komponenterna](/help/sites-authoring/adobe-campaign-components.md).