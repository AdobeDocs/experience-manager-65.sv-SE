---
title: Skapa en formulärportalsida
seo-title: Creating a forms portal page
description: Forms Portal förser webbutvecklare med komponenter för att skapa och anpassa en formulärportal på webbplatser som skapats med Adobe Experience Manager (AEM).
seo-description: Forms Portal equips Web Developers with components to create and customize a forms portal on websites authored using Adobe Experience Manager (AEM).
uuid: a5017de5-616c-4ce4-81aa-f28c741f8e8f
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: 8fff78cb-9ef9-426e-8b30-d70b4f26887f
docset: aem65
feature: Forms Portal
exl-id: 22d7c24e-7a77-4324-afdf-74c1fbf15773
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '1650'
ht-degree: 0%

---

# Skapa en formulärportalsida{#creating-a-forms-portal-page}

| Version | Artikellänk |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Klicka här](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-forms-portal.html) |
| AEM 6.5 | Den här artikeln |

Forms portalkomponenter förser webbutvecklare med komponenter för att skapa och anpassa en formulärportal på webbplatser som skapats med Adobe Experience Manager (AEM). En snabb översikt av formulärportalen finns på [Introduktion till att publicera formulär på en portal](../../forms/using/introduction-publishing-forms.md).

## Förutsättningar {#prerequisites}

Forms portalkomponenter är inte tillgängliga som standard. Kontrollera att följande komponentkategorier för formulärportalen är aktiverade enligt beskrivningen i [Aktivera komponenterna i formulärportalen](/help/forms/using/enabling-forms-portal-components.md).

**Dokumenttjänster** Innehåller komponenterna Sök och Lister, Länk samt Utkast och överföringar.

**Document Services Predicates** Innefattar komponenterna Date Predicate, Full Text Predicate, Properties Predicate och Tags Predicate. De här komponenterna används för att konfigurera sökningar i komponenten Sök efter och visa.

När de har aktiverats på en AEM webbplatssida är de här komponentkategorierna tillgängliga för användning i komponentwebbläsaren.

![AEM Forms portalkomponenter i komponentwebbläsaren](assets/component-categories.png)

Komponentkategorier för Forms Portal

## Komponenten Search &amp; Lister {#search-amp-lister-component}

Komponenten Search &amp; Lister, som finns under komponentkategorin Document Services, används för att lista formulär på en sida och för att implementera sökning i de listade formulären. Komponenten innehåller två rutor:

* Listruta där formulären listas.
* Sökruta där du lägger till sökfunktionen.

Du kan dra och släppa komponenten Sök och Lister från komponentkategorin Document Services i komponentwebbläsaren till sidan. När komponenten läggs till ser den ut ungefär så här.

![Sök efter och visa komponent på en sida](assets/fp-grid-viw.png)

Sök efter och visa komponent på en sida med stödrasterlayout

### Listruta {#list-pane}

Listrutan är ett område där formulären listas. Komponenten Sök och lista innehåller olika konfigurationsalternativ som du kan använda för att styra visningen av formulär i rutan Lista.

Konfigurera listfönstret genom att trycka på komponenten Sök och Lister och sedan trycka på ![settings_icon](assets/settings_icon.png). The **[!UICONTROL  Edit Component]** öppnas.

![Listruta i redigeringsläge](assets/edit-list.png)

Listruta i redigeringsläge

The **Redigera** innehåller flera flikar med konfigurationsalternativ som beskrivs i tabellen nedan. Tryck **OK** för att spara konfigurationen när du är klar.

<table>
 <tbody>
  <tr>
   <th>Tabb</th>
   <th>Konfiguration</th>
   <th>Beskrivning</th>
  </tr>
  <tr>
   <td><span class="uicontrol"><strong>Resursmappar</strong></code></td>
   <td>Lägg till objekt</td>
   <td>Konfigurerar mapparna där resurser överförs med AEM Forms UI. Som standard visas alla överförda resurser. Mer information om användargränssnittet i AEM Forms finns i <a href="../../forms/using/introduction-managing-forms.md" target="_blank">Introduktion till hantering av formulär</a>.</td>
  </tr>
  <tr>
   <td><p><span class="uicontrol"><strong>Visa</strong></code></p> </td>
   <td>Titeltext</td>
   <td>Titel för komponenten Sök efter och visa. Standardtiteln är <strong>Forms Portal.</strong></td>
  </tr>
  <tr>
   <td> </td>
   <td>Layoutmall</td>
   <td>Resursernas layout. </td>
  </tr>
  <tr>
   <td> </td>
   <td>Inaktivera avancerad sökning</td>
   <td>När det här alternativet är aktiverat döljs ikonen för avancerad sökning.</td>
  </tr>
  <tr>
   <td> </td>
   <td>Inaktivera textsökning</td>
   <td>När det här alternativet är aktiverat döljs textsökfältet.</td>
  </tr>
  <tr>
   <td><span class="uicontrol"><strong>Resultat</strong></code></td>
   <td>Antal resultat per sida</td>
   <td>Konfigurerar det maximala antalet formulär som du vill visa på en sida.</td>
  </tr>
  <tr>
   <td> </td>
   <td>Resultattext</td>
   <td><p>Konfigurerar resultattexten (till exempel 1-12 av 601) <strong>Resultat</strong>). Standardvärdet är <strong>Resultat</strong>.</p> <p>Om du till exempel anger <strong>Forms </strong>i det här fältet, och det finns totalt 601 formulär, ändras texten till 1-12 av 601 <strong>Forms.</strong></p> </td>
  </tr>
  <tr>
   <td> </td>
   <td>Sidtext</td>
   <td><p>Konfigurerar sidtexten (till exempel <strong>Sida </strong>1 av 51). Standardvärdet är <strong>Sida</strong>.</p> <p>Om du till exempel anger <strong>Ansökningsblankett </strong>i det här fältet och det finns 51 sidor ändras sidtexten till <strong>Ansökningsblankett </strong>1 av 51.</p> </td>
  </tr>
  <tr>
   <td> </td>
   <td>Av text</td>
   <td><p>Ersätter ordet <strong>av</strong> med den angivna texten (sidan 1 <strong>av </strong>51). Standardvärdet är <strong>av</strong>.</p> <p>Om du till exempel anger <strong>av </strong>i det här fältet ändras texten till Sida 1 <strong>av </strong>51.</p> </td>
  </tr>
  <tr>
   <td><span class="uicontrol"><strong>Formulärlänk</strong></code></td>
   <td>Återgivningstyp</td>
   <td>Styr formulärlistan baserat på den angivna återgivningstypen. De tillgängliga alternativen är PDF och HTML. Om du till exempel bara väljer HTML som återgivningstyp filtreras PDF forms bort.</td>
  </tr>
  <tr>
   <td> </td>
   <td>HTML-profil</td>
   <td>Konfigurerar den HTML-profil som ska användas för återgivning. Alla tillgängliga profiler visas i listrutan.</td>
  </tr>
  <tr>
   <td> </td>
   <td>Skicka URL</td>
   <td><p>Konfigurerar en servett där formulärdata skickas.</p> <p><strong>Obs!</strong> <em>Skicka-URL för ett formulär kan anges på flera ställen och prioritetsordningen är följande:</em></p>
    <ol>
     <li><em>Skicka-URL som är inbäddad i formuläret (med knappen Skicka) har högsta prioritet.</em></li>
     <li><em>Överförings-URL:en i AEM Forms-gränssnittet har den högsta prioriteten.</em></li>
     <li><em>Överförings-URL som anges i formulärportalen har lägst prioritet.</em></li>
    </ol> </td>
  </tr>
  <tr>
   <td> </td>
   <td>Funktionsbeskrivning för återgivning i HTML</td>
   <td>Konfigurerar texten för verktygstipset, som visas när du håller pekaren över den <img height="16" src="assets/aem6forms_panel-html.png" width="13" /> (HTML5-ikonen).</td>
  </tr>
  <tr>
   <td> </td>
   <td>Funktionsbeskrivning för återgivning i PDF</td>
   <td>Konfigurerar texten för verktygstipset, som visas när du håller pekaren över den <img height="16" src="assets/aem6forms_panel-pdf.png" width="14" /> (PDF-ikonen).</td>
  </tr>
  <tr>
   <td><span class="uicontrol"><strong>Stil</strong></code></td>
   <td>Formattyp</td>
   <td>Här kan du ange <strong>Inget format, standardformat</strong>, eller <strong>Eget format </strong>för att lista formulären.</td>
  </tr>
  <tr>
   <td> </td>
   <td>Anpassad formatsökväg</td>
   <td>Om du valde Anpassad som formattyp bläddrar du till den anpassade CSS-formatmallen och väljer Standard.</td>
  </tr>
 </tbody>
</table>

### Sökruta {#search-pane}

I sökrutan kan du lägga till komponenterna Date Predicate (Datumpredikat), Full Text Predicate (Fullständig textpredikat), Properties Predicate (Förutdikat för egenskaper) och Tags Predicate (Förutdikat för dokumenttjänster) i AEM Sidekick. Dessa komponenter implementerar sökfunktionen så att användarna kan söka i de listade formulären.

**Tips:** *Du kan styra listan med formulär som visas på formulärportalen baserat på ett förinställt villkor och dölja sökfunktionen för slutanvändare. Om du vill styra listan med formulär använder du komponenterna Predicate för att använda sökfilter. Du kan också ange standardfiltervärden och inaktivera sökningen på fliken Visning i dialogrutan Redigera komponent.*

![Sökpanel med predikat för datum, fullständig text, egenskaper och taggar](assets/search-with-predicates.png)

Sökpanel med predikat för datum, fullständig text, egenskaper och taggar

#### Datumpredikat {#date-predicate}

När du lägger till komponenten Date Predicate kan du söka i de listade formulär som har ändrats under en viss tid.

Så här konfigurerar du komponenten Date Predicate:

1. Tryck på komponenten och tryck sedan på ![settings_icon](assets/settings_icon.png). Dialogrutan Redigera öppnas.
1. Ange följande:

   * **Typ:** Det enda tillgängliga alternativet är **Senast ändrat den**

   * **Text:** Etikett eller bildtext för komponenten Date Predicate. Standardvärdet är **Senast ändrat den.**

   * **Startdatum - etikett:** Etikett eller bildtext för startdatumfält
   * **Slutdatum - etikett:** Etikett eller bildtext för slutdatumfält
   * **Dölj:** Använda standarddatumfilter för att lista formulär

1. Tryck **OK**

#### Fullständig textpredikat {#full-text-predicate}

Komponenten Full Text Predicate implementerar fullständig textsökning i formulärdata, till exempel namn och beskrivning. Användarna kan söka i valfri textsträng för att returnera formulär som innehåller texten i sitt namn eller sin beskrivning.

Så här konfigurerar du komponenten Full Text Predicate:

1. Tryck på komponenten och tryck sedan på ![settings_icon](assets/settings_icon.png). Dialogrutan Redigera öppnas.
1. Ange rubriken i dialogrutan **Huvudrubrik** fält.
1. Tryck **OK**

#### Egenskapspredikat {#properties-predicate}

Komponenten Predicate för egenskaper implementerar sökning i formulär baserat på formuläregenskaper som titel, författare och beskrivning.

Så här konfigurerar du komponenten Predicate för egenskaper:

1. Tryck på komponenten och tryck sedan på ![settings_icon](assets/settings_icon.png). Dialogrutan Redigera öppnas.
1. På fliken Allmänt anger du söketiketten. Standardvärdet är **Egenskaper**

1. Tryck på **Lägg till objekt.**
1. Välj en egenskap i listrutan och ange en söketikett för den i fältet nedanför listrutan.
1. Upprepa steg 4 om du vill lägga till fler egenskaper. Du kan också ange ett standardfiltervärde för att lista formulär baserat på de angivna villkoren och dölja egenskapen för sökning av slutanvändare. Markera kryssrutan Dölj för en egenskap och ange standardfiltervärdet.
Om du till exempel vill visa formulär som innehåller&quot;Resa&quot; i sina titlar väljer du Dölj bredvid egenskapen Titel. Ange dessutom Travel i standardtextrutan för filtervärde.

1. Tryck **OK**

#### Taggar - predikat {#tags-predicate}

Komponenten för taggprediktion implementerar sökning i formulär baserat på taggar som definieras i Forms Manager.

Så här konfigurerar du komponenten Tagg Predicate:

1. Tryck på komponenten och tryck sedan på ![settings_icon](assets/settings_icon.png). Dialogrutan Redigera öppnas.
1. Tryck på nedpilsknappen bredvid fältet Taggar.
1. Välj lämpliga taggar
1. Tryck **OK**

De markerade taggarna visas i sökrutan tillsammans med kryssrutorna för markering. Användarna kan nu begränsa sökningen baserat på taggarna.

## Visa formulär på en sida {#list-forms-on-a-page-br}

Om du vill visa formulär på en sida lägger du till **[!UICONTROL Search & Lister]** Komponent till sidan och konfigurera **[!UICONTROL List Pane]**. Om du vill att användarna ska kunna söka efter formulär med datum, text och taggar lägger du till en **[!UICONTROL Search Pane]** -komponenten.

Om du vill länka ett formulär var som helst på sidan använder du länkkomponenten. Mer information om länkkomponenten finns i [Bädda in länkkomponent på en sida](../../forms/using/embedding-link-component-page.md).

Använd **[!UICONTROL Drafts and Submissions]** -komponenten. Mer information finns i [Anpassa komponenten Utkast och överföringar](../../forms/using/draft-submission-component.md).

## Mobil enhetsvänlighet {#mobile-device-friendliness}

Komponenten Forms Portal Search &amp; Lister är anpassad för mobila enheter och anpassas därefter. Alla tre standardvyerna: stödraster, kort och panel återlayoutas beroende på vilken enhet som webbplatsen öppnas i, vilket innebär att webbsidan också anpassas. Det enkla är att Sök och lista bara är en komponent och inte styr formateringen på sidnivå.

I följande bild visas komponenten Sök och Lister när den öppnas på en mobil enhet:

![Skärmbild av komponenten Sök och Lister](assets/search_lister.png)

Komponenten Search &amp; Lister

## Anpassa en formulärportalsida {#customizing-a-forms-portal-page-br}

Du kan anpassa en formulärportalsida för att ge sidan ett tydligt utseende. Du kan också lägga till metadata för att förbättra sökupplevelsen, ändra sidans layout och lägga till anpassade CSS-format. Mer information finns i [Anpassa mallar för Forms Portal-komponenter](../../forms/using/customizing-templates-forms-portal-components.md).

Med AEM Forms-gränssnittet kan du lägga till anpassade metadata i formulär. Anpassade metadata är användbara när du vill visa en lista och söka efter formulär för slutanvändarna. Mer information om anpassade metadata finns i [Anpassa mallar för Forms Portal-komponenter](../../forms/using/customizing-templates-forms-portal-components.md).

I själva verket innehåller formulärportalen återgivningsåtgärder. Du kan anpassa formulärportalen för att lägga till fler åtgärder. Mer information finns i [Lägga till anpassad åtgärd för formulärlisteobjekt.](../../forms/using/add-custom-action-form-lister.md)

## Relaterade artiklar

* [Aktivera komponenter i formulärportalen](/help/forms/using/enabling-forms-portal-components.md)
* [Skapa portalsida för formulär](/help/forms/using/creating-form-portal-page.md)
* [Visa formulär på en webbsida med API:er](/help/forms/using/listing-forms-webpage-using-apis.md)
* [Använda komponenten Utkast och inskickat material](/help/forms/using/draft-submission-component.md)
* [Anpassa lagring av utkast och inskickade formulär](/help/forms/using/draft-submission-component.md)
* [Exempel för att integrera komponent för utkast och inlämning med databas](/help/forms/using/integrate-draft-submission-database.md)
* [Anpassa mallar för komponenter i formulärportalen](/help/forms/using/customizing-templates-forms-portal-components.md)
* [Introduktion till att publicera formulär på en portal](/help/forms/using/introduction-publishing-forms.md)
