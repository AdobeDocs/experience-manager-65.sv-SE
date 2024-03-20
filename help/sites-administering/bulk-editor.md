---
title: Massredigeraren
description: Lär dig hur du använder gruppredigeraren för effektiv redigering när den visuella sidkontexten inte behövs.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
docset: aem65
exl-id: c63e044c-4d2a-44d3-853b-8e7337e1ee03
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '1160'
ht-degree: 0%

---


# Massredigeraren{#the-bulk-editor}

Med gruppredigeraren kan du redigera effektivt när den visuella sidkontexten inte behövs så som du kan:

* söka efter (och visa) innehåll från flera sidor; detta görs med GQL (Google Query Language)
* redigera det här innehållet direkt i gruppredigeraren
* spara ändringarna (på originalsidorna)
* exportera det här innehållet till en tabbavgränsad (.tsv) kalkylbladsfil

>[!NOTE]
>
>Du kan även importera innehåll till databasen, men som standard är detta inaktiverat för gruppredigeraren så som det är tillgängligt i **verktyg** konsol.

I det här avsnittet beskrivs hur du arbetar med gruppredigeraren i **verktyg** konsol. Vanligtvis använder administratörer gruppredigeraren för att söka efter och redigera flera objekt. Det gör du genom att fylla i tabellen med en GQL-fråga och sedan genom att markera innehållsobjekten som du vill arbeta med. Författare använder vanligtvis gruppredigeraren som en del av ett anpassat gruppredigeringsprogram som är tillgängligt via [produktlista](/help/sites-authoring/default-components.md#productlist) -komponenten.

>[!CAUTION]
>
>Med [borttagning av det klassiska användargränssnittet](/help/release-notes/deprecated-removed-features.md) i AEM 6.4 har gruppredigeraren också tagits bort och därför planerar Adobe inte att ytterligare förbättra gruppredigeraren.

## Exempel på användningsfall för den grupperade redigeraren {#example-use-case-for-the-bulk-editor}

Om du t.ex. behöver alla namn och e-postadresser för användare som fyllt i en viss enkät, kan gruppredigeraren ange den informationen och du kan exportera den till ett kalkylblad.

Ett exempel som illustrerar en sådan användning finns på Geometrixx webbplats:

1. Navigera till **Support** sidan och sedan till **Nöjd kundtjänst** enkät.
1. **Redigera** den **Formulärets början** stycke. Klicka på **Avancerat** -fliken, expandera **Åtgärdskonfiguration** och sedan klicka **Visa data...**.

   ![Exempel på enkät om kundnöjdhet](assets/custsatsurvey.png)

1. Massredigeraren är helt anpassningsbar, men i det här exemplet tillåter inte gruppredigeraren att användare redigerar innehållet, utan bara att de kan exportera informationen till ett kalkylblad.

   ![Konsol för massredigering](assets/bulkeditor.png)

## Så här använder du gruppredigeraren {#how-to-use-the-bulk-editor}

Med gruppredigeraren kan du

* [söka efter innehåll baserat på frågeparametrar, för att visa angivna egenskaper för resultaten i kolumner, för att redigera innehållet och spara ändringarna](#searching-and-editing-content)
* [om du vill exportera det här innehållet till ett tabbseparerat kalkylblad](#exporting-content)

* [importera innehåll från ett tabbseparerat kalkylblad](#importing-content)

### Söka och redigera innehåll {#searching-and-editing-content}

Så här använder du gruppredigeraren för att redigera flera objekt samtidigt:

1. I **verktyg** klickar du på **Importörer** för att expandera den.
1. Dubbelklicka på **Massredigerare**.
1. Ange dina urvalskrav:

<table>
 <tbody>
  <tr>
   <td>Fält</td>
   <td>Egenskap</td>
  </tr>
  <tr>
   <td>Rotsökväg</td>
   <td>Anger den rotsökväg som den gruppredigeraren söker efter.<br /> Till exempel: <code>/content/geometrixx/en</code>. I gruppredigeraren söks alla underordnade noder igenom.</td>
  </tr>
  <tr>
   <td>Frågeparametrar</td>
   <td>Använd GQL-parametrar för att ange söksträngen som du vill att den gruppredigerade ska söka efter i databasen. Till exempel: <code>type:Page</code> söker efter alla sidor i rotsökvägen, <code>text:professional</code> söker efter alla sidor som innehåller ordet "professionell", och <code>"jcr:title":English</code> söker efter alla sidor som har "engelska" som titel. Du kan bara söka efter strängar.</td>
  </tr>
  <tr>
   <td>Kryssrutan Innehållsläge</td>
   <td>Markera den här kryssrutan så att du kan läsa egenskaperna i <code>jcr:content</code> undernod till sökresultatet om sådan finns. Använd endast för sidor. Egenskapsnamn har prefixet <code>"jcr:content/"</code></td>
  </tr>
  <tr>
   <td>Egenskaper/kolumner</td>
   <td>Markera kryssrutorna för de egenskaper som du vill att gruppredigeraren ska returnera. De egenskaper du väljer är kolumnrubrikerna i resultatrutan. Som standard visas nodsökvägen i resultatet.</td>
  </tr>
  <tr>
   <td>Anpassade egenskaper/kolumner</td>
   <td>Ange andra egenskaper som inte finns med i listan <strong>Egenskaper/kolumner</strong> fält. Dessa anpassade egenskaper visas i resultatrutan. Du kan lägga till flera egenskaper genom att använda kommatecken för att skilja egenskaperna åt. <i>Obs!</i> Om du lägger till en anpassad egenskap som inte finns än visas en tom cell AEM WCM. När du ändrar den tomma cellen och sparar den läggs egenskapen till i noden. Den nya egenskapen måste respektera nodtypsbegränsningar och egenskapsnamnutrymmen.</td>
  </tr>
 </tbody>
</table>

Till exempel:

![Alternativ för filtret Massredigering](assets/searchfilter.png)

1. Klicka **Sök**. Resultaten visas i gruppredigeraren.
I exemplet ovan returneras alla sidor som uppfyller dina sökvillkor och visas med de begärda kolumnerna.

   ![Resultat av gruppredigering](assets/chlimage_1-39.png)

1. Dubbelklicka på en cell så att du kan göra eventuella ändringar.

   ![Gruppredigering](assets/srchresultedit.png)

1. Klicka **Spara** för att spara dina ändringar **Spara** aktiveras när du har redigerat en cell).

   >[!CAUTION]
   >
   >De ändringar du gör här skrivs till databasinnehållet, till exempel sidan som refereras i **Bana**.

#### Ytterligare GQL-frågeparametrar {#additional-gql-query-parameters}

* **sökväg:** bara söknoder under den här sökvägen. Om du anger mer än en term med ett sökvägsprefix beaktas endast den sista termen.
* **typ:** bara returnera noder av den angivna nodtypen. Detta inkluderar primära och blandade typer. Du kan ange flera kommaavgränsade nodtyper. GQL returnerar noder som är av någon av de angivna typerna.
* **beställning:** sortera resultatet efter de angivna egenskaperna. Du kan ange flera kommaavgränsade egenskapsnamn. Om du vill ordna resultatet i fallande ordning lägger du bara till ett minustecken som prefix för egenskapsnamnet. Till exempel order:-name. Om du använder ett plustecken returneras resultatet i stigande ordning, vilket också är standard.
* **gräns:** begränsar antalet resultat med ett intervall. Till exempel limit:10..20 Intervallet är nollbaserat, start är inkluderat och slut är exklusivt. Du kan också ange en öppen `interval:limit:10..` eller `limit:..20`
Om punkterna utelämnas och endast ett värde anges, returnerar GQL högst detta antal resultat. Till exempel: `limit:10` (returnerar de första tio resultaten).

### Exporterar innehåll {#exporting-content}

Exportera vid behov innehållet till ett Excel-kalkylblad för att göra eventuella ändringar. Du kan till exempel vilja exportera en utskickslista och ändra riktnummer för alla telefonnummer som visas direkt i Excel, eller lägga till ytterligare rader.

Så här exporterar du innehåll:

1. Sök efter innehåll enligt beskrivningen i [Söka och redigera innehåll](#searching-and-editing-content).
1. Klicka **Exportera** så att du kan exportera ändringarna till ett tabbseparerat Excel-kalkylblad. AEM frågar var du vill hämta filen.

   >[!NOTE]
   >
   >Som standard kodas ändringar i [Windows-1252](https://en.wikipedia.org/wiki/Windows-1252) (kallas även CP-1252). Du kan markera UTF-8 om du vill exportera ändringarna i UTF-8.

   ![Exporterar resultat](assets/srchrsesultexport.png)

1. Markera platsen och bekräfta att du vill hämta filen.
1. När du har laddat ned filen kan du öppna den från kalkylprogrammet, till exempel Microsoft® Excel. Kalkylbladsprogrammet importerar filen och konverterar den till ett kalkylbladsformat.

   ![Exporterade resultat i ett kalkylblad](assets/exportinexcel.png)

### Importera innehåll {#importing-content}

Som standard är importfunktionen dold när du öppnar gruppredigeraren. Lägg bara till parametern `hib=false` till webbadressen visas **Importera** på sidan Massredigeraren. Du kan importera innehåll från valfri tabbavgränsad ( `.tsv`). För att importen ska fungera på rätt sätt måste kolumnrubrikerna (den första cellraden) matcha kolumnrubrikerna i tabellen som du importerar till.

>[!NOTE]
>
>När du återimporterar innehåll raderar du allt tidigare innehåll för de noderna. Se till att inte skriva över viktig information.

Så här importerar du innehåll:

1. Öppna gruppredigeraren.
1. Lägg till `?hib=false` till URL-adressen, till exempel:
   `https://localhost:4502/etc/importers/bulkeditor.html?hib=false`
1. Klicka **Importera**.
1. Välj `.tsv` -fil. Data importeras till databasen.
