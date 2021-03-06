---
title: Sidmallar - redigerbara
seo-title: Page Templates - Editable
description: Redigerbara mallar har lagts till, gör det möjligt för icke-utvecklare att skapa och redigera mallar, skapa mallar som behåller en dynamisk anslutning till sidor som skapats av dem och göra sidkomponenten mer generisk
seo-description: Editable templates have been introduced to, allow non-developers to create and edit templates, provide templates that retain a dynamic connection to any pages created from them, and make the page component more generic
uuid: 61791960-fdef-4e49-878a-11fdf1d4f0ab
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 1099cc44-de6d-499e-8b52-f2f5811ae086
docset: aem65
exl-id: dcb66b6d-d731-493e-8936-12d529f6cbde
source-git-commit: 2801ef5ec5ed7b01f4eb046baa439f6d5de56b75
workflow-type: tm+mt
source-wordcount: '3249'
ht-degree: 0%

---

# Sidmallar - redigerbara {#page-templates-editable}

Redigerbara mallar har lagts till:

* Tillåt att specialiserade författare [skapa och redigera mallar](/help/sites-authoring/templates.md).

   * Sådana specialister kallas **mallskapare**
   * Mallförfattare måste vara medlemmar i `template-authors` grupp.

* Tillhandahåll mallar som behåller en dynamisk anslutning till alla sidor som skapas från dem. Detta säkerställer att alla ändringar i mallen återspeglas på själva sidorna.
* Gör sidkomponenten mer generisk så att kärnsideskomponenten kan användas utan anpassning.

Med redigerbara mallar isoleras de delar som utgör en sida inuti komponenterna. Du kan konfigurera nödvändiga kombinationer av komponenter i ett användargränssnitt, vilket eliminerar behovet av att utveckla en ny sidkomponent för varje sidvariant.

>[!NOTE]
>
>[Statiska mallar](/help/sites-developing/page-templates-static.md) finns också.

Det här dokumentet:

* Ger en översikt över hur du skapar redigerbara mallar

   * Mer information finns på [Skapa sidmallar](/help/sites-authoring/templates.md)

* Beskriver de admin-/utvecklaråtgärder som krävs för att skapa redigerbara mallar
* Beskriver de tekniska grunderna för redigerbara mallar

Det här dokumentet förutsätter att du redan är bekant med att skapa och redigera mallar. Se redigeringsdokumentet [Skapa sidmallar](/help/sites-authoring/templates.md), som beskriver funktionerna i redigerbara mallar så som de visas för mallskaparen.

>[!NOTE]
>
>Följande självstudiekurs kan också vara intressant för att konfigurera en redigerbar sidmall i ett nytt projekt:
>[Komma igång med AEM Sites del 2 - Skapa en bassida och mall](https://helpx.adobe.com/experience-manager/kt/sites/using/getting-started-wknd-tutorial-develop/part2.html)

## Skapa en ny mall {#creating-a-new-template}

Skapa redigerbara mallar i första hand med [mallkonsol och mallredigerare](/help/sites-authoring/templates.md) av en mallskapare. I det här avsnittet ges en översikt över processen och en beskrivning av vad som händer på teknisk nivå.

Mer information om hur du använder redigerbara mallar i ett AEM projekt finns i [Skapa ett AEM projekt med Lazybone](https://helpx.adobe.com/experience-manager/using/aem_lazybones.html).

När du skapar en ny redigerbar mall:

1. Skapa en [mapp för mallarna](#template-folders). Detta är inte obligatoriskt, men vi rekommenderar bästa praxis.
1. Välj en [malltyp](#template-type). Detta kopieras för att skapa [malldefinition](#template-definitions).

   >[!NOTE]
   >
   >Ett urval av malltyper finns färdiga. Du kan också [skapa egna webbplatsspecifika malltyper](/help/sites-developing/page-templates-editable.md#creating-template-types) vid behov.

1. Konfigurera den nya mallens struktur, innehållsprinciper, ursprungliga innehåll och layout.

   **Struktur**

   * Strukturen gör att du kan definiera komponenter och innehåll för mallen.
   * Komponenter som definieras i mallstrukturen kan inte flyttas till en resultatsida eller tas bort från eventuella resultatsidor.

      * Om du skapar en mall i en anpassad mapp utanför Web.Retail-exempelinnehållet kan du välja Foundation Components eller använda [Kärnkomponenter](https://helpx.adobe.com/experience-manager/core-components/using/developing.html).
   * Om du vill att sidförfattare ska kunna lägga till och ta bort komponenter lägger du till ett styckesystem i mallen.
   * Komponenter kan låsas upp och låsas igen så att du kan definiera ursprungligt innehåll.

   Mer information om hur en mallskapare definierar strukturen finns i [Skapa sidmallar](/help/sites-authoring/templates.md#editing-a-template-structure-template-author).

   Information om strukturens tekniska detaljer finns i [Struktur](/help/sites-developing/page-templates-editable.md#structure) i det här dokumentet.

   **Profiler**

   * Innehållsprinciperna definierar designegenskaperna för en komponent.

      * Till exempel de tillgängliga komponenterna eller minimi-/maximidimensionerna.
   * Dessa gäller för mallen (och sidor som skapas med mallen).

   Mer information om hur en mallskapare definierar principer finns i [Skapa sidmallar](/help/sites-authoring/templates.md#editing-a-template-structure-template-author).

   Information om policyns tekniska detaljer finns i [Innehållsprofiler](/help/sites-developing/page-templates-editable.md#content-policies) i det här dokumentet.

   **Ursprungligt innehåll**

   * Ursprungligt innehåll definierar innehåll som visas när en sida skapas baserat på mallen.
   * Startinnehållet kan sedan redigeras av sidförfattare.

   Mer information om hur en mallskapare definierar strukturen finns i [Skapa sidmallar](/help/sites-authoring/templates.md#editing-a-template-initial-content-author).

   Teknisk information om ursprungligt innehåll finns på [Ursprungligt innehåll](/help/sites-developing/page-templates-editable.md#initial-content) i det här dokumentet.

   **Layout**

   * Du kan definiera mallayouten för ett antal olika enheter.
   * Responsiv layout för mallar fungerar på samma sätt som för sidredigering.

   Mer information om hur en mallskapare definierar mallayouten finns i [Skapa sidmallar](/help/sites-authoring/templates.md#editing-a-template-layout-template-author).

   Mer teknisk information om mallayout finns i [Layout](/help/sites-developing/page-templates-editable.md#layout) i det här dokumentet.

1. Aktivera mallen och tillåt den sedan för specifika innehållsträd.

   * En mall kan aktiveras eller inaktiveras för att göra den tillgänglig eller inte tillgänglig för sidförfattare.
   * En mall kan göras tillgänglig eller otillgänglig för vissa sidgrenar.

   Mer information om hur en mallskapare aktiverar en mall finns i [Skapa sidmallar](/help/sites-authoring/templates.md#enabling-and-allowing-a-template-template-author).

   Information om hur du aktiverar en mall finns i [Aktivera och tillåta en mall för oss](/help/sites-developing/page-templates-editable.md#enabling-and-allowing-a-template-for-use)e i det här dokumentet

1. Använd det för att skapa innehållssidor.

   * När du använder en mall för att skapa en ny sida finns det ingen synlig skillnad och ingen indikation mellan statiska och redigerbara mallar.
   * För sidförfattaren är processen genomskinlig.

   Mer information om hur en sidförfattare använder mallar för att skapa en sida finns i [Skapa och ordna sidor](/help/sites-authoring/managing-pages.md#templates).

   Teknisk information om hur du skapar sidor med redigerbara mallar finns i [Gällande innehållssidor](/help/sites-developing/page-templates-editable.md#resultant-content-pages) i det här dokumentet.

>[!TIP]
>
>Ange aldrig någon information som behöver internationaliseras i en mall. För internalisering [lokaliseringsfunktion för kärnkomponenterna](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/get-started/localization.html) rekommenderas.

>[!NOTE]
>
>Mallar är kraftfulla verktyg som effektiviserar arbetsflödet för att skapa sidor. Alltför många mallar kan överbelasta författarna och göra det förvirrande att skapa sidor. En bra tumregel är att hålla antalet mallar under 100.
>
>Adobe rekommenderar inte att ha fler än 1 000 mallar på grund av potentiella prestandaeffekter.

>[!NOTE]
>
>Redigerarens klientbibliotek förutsätter att det finns `cq.shared` namnutrymme på innehållssidor och om det inte finns något JavaScript-fel `Uncaught TypeError: Cannot read property 'shared' of undefined` blir resultatet.
>
>Alla exempelinnehållssidor innehåller `cq.shared`så allt innehåll som baseras på dem automatiskt innehåller `cq.shared`. Om du däremot bestämmer dig för att skapa egna innehållssidor från grunden utan att basera dem på exempelinnehåll måste du se till att inkludera `cq.shared` namnutrymme.
>
>Se [Använda bibliotek på klientsidan](/help/sites-developing/clientlibs.md) för ytterligare information.

## Mallmappar {#template-folders}

Du kan använda följande mappar för att ordna dina mallar:

* **globalt**
* Platsspecifika De platsspecifika mappar som du skapar för att ordna dina mallar skapas med kontoadministratörsbehörighet.

>[!NOTE]
>
>Även om du kan kapsla dina mappar när de visas i **Mallar** konsolen som visas som en platt struktur.

I en AEM **global** mappen finns redan i mallkonsolen. Detta innehåller standardmallar och fungerar som reserv om inga principer och/eller malltyper hittas i den aktuella mappen. Du kan lägga till dina standardmallar i den här mappen eller skapa en ny mapp (rekommenderas).

>[!NOTE]
>
>Det är bäst att skapa en ny mapp för dina anpassade mallar och inte använda den globala mappen.

>[!CAUTION]
>
>Mappar måste skapas av en användare med `admin` rättigheter.

Malltyper och profiler ärvs i alla mappar enligt följande prioritetsordning:

1. Den aktuella mappen.
1. Överordnad(e) till den aktuella mappen.
1. `/conf/global`
1. `/apps`
1. `/libs`

En lista över alla tillåtna poster skapas. Om några konfigurationer överlappar ( `path`/ `label`) visas bara den instans som ligger närmast den aktuella mappen för användaren.

Om du vill skapa en ny mapp kan du göra det här:

* Programmerat eller med CRXDE Lite
* Använda Konfigurationsläsaren

## Använda CRXDE Lite {#using-crxde-lite}

1. En ny mapp (under /conf) kan skapas för din instans antingen programmatiskt eller med CRXDE Lite.

   Följande struktur måste användas:

   ```xml
   /conf
       <your-folder-name> [sling:Folder]
           settings [sling:Folder]
               wcm [cq:Page]
                   templates [cq:Page]
                   policies [cq:Page]
   ```

1. Du kan sedan definiera följande egenskaper på mappens rotnod:

   `<your-folder-name> [sling:Folder]`

   Namn: `jcr:title`

   * Typ: `String`

   * Värde: Den rubrik (för mappen) som du vill ska visas i **Mallar** konsol.

1. I *addition* till standardbehörigheter (t.ex. `content-authors`) måste du nu tilldela grupper och definiera de åtkomstbehörigheter som krävs för att författarna ska kunna skapa mallar i den nya mappen.

   The `template-authors` grupp är standardgruppen som måste tilldelas. Se följande avsnitt [Behörighetslistor och grupper](/help/sites-developing/page-templates-editable.md#acls-and-groups) för mer information.

   Se [Behörighetshantering](/help/sites-administering/user-group-ac-admin.md#access-right-management) om du vill ha fullständig information om hur du hanterar och tilldelar åtkomsträttigheter.

### Använda Konfigurationsläsaren {#using-the-configuration-browser}

1. Gå till **Global navigering** -> **verktyg** > **Konfigurationsläsaren**.

   De befintliga mapparna visas till vänster, inklusive **global** mapp.

1. Klicka **Skapa**.
1. I **Skapa konfiguration** måste följande fält konfigureras:

   * **Titel**: Ange en rubrik för konfigurationsmappen
   * **Redigerbara mallar**: Markera för att tillåta redigerbara mallar i den här mappen

1. Klicka **Skapa**

>[!NOTE]
>
>I konfigurationsläsaren kan du redigera den globala mappen och aktivera **Redigerbara mallar** om du vill skapa mallar i den här mappen, men detta är inte den bästa metoden.
>
>Se [Konfigurationsläsaren](/help/sites-administering/configurations.md) mer information.

### Behörighetslistor och grupper {#acls-and-groups}

När mallmapparna har skapats (antingen via CRXDE eller med Configuration Browser) måste åtkomstkontrollistor definieras för rätt grupper för mallmapparna för att säkerställa rätt säkerhet.

Mallmappar för [Referensimplementering för Vi.butik](/help/sites-developing/we-retail.md) kan användas som exempel.

#### Mallförfattargruppen {#the-template-authors-group}

The `template-authors` grupp är den grupp som används för att hantera åtkomst till mallar och levereras som standard med AEM, men är tom. Användare måste läggas till i gruppen för projektet/webbplatsen.

>[!CAUTION]
>
>The `template-authors` gruppen är *endast* för användare som måste kunna skapa nya mallar.
>
>Att redigera mallar är mycket kraftfullt och om det inte görs på rätt sätt kan befintliga mallar brytas. Därför bör denna roll fokuseras och endast omfatta kvalificerade användare.

Följande tabell visar vilka behörigheter som krävs för mallredigering.

<table>
 <tbody>
  <tr>
   <th>Bana</th>
   <th>Roll/grupp</th>
   <th>Behörigheter<br /> </th>
   <th>Beskrivning</th>
  </tr>
  <tr>
   <td rowspan="3"><code>/conf/&lt;<i>your-folder</i>&gt;/settings/wcm/templates</code></td>
   <td>Mallförfattare<br /> </td>
   <td>läsa, skriva, replikera</td>
   <td>Mallförfattare som skapar, läser, uppdaterar, tar bort och replikerar mallar i platsspecifika <code>/conf</code> space</td>
  </tr>
  <tr>
   <td>Anonym webbanvändare</td>
   <td>read</td>
   <td>En anonym webbanvändare måste läsa mallar när en sida återges</td>
  </tr>
  <tr>
   <td>Innehållsförfattare</td>
   <td>replikera</td>
   <td>replikateInnehållsförfattare måste aktivera sidans mallar när en sida aktiveras</td>
  </tr>
  <tr>
   <td rowspan="3"><code>/conf/&lt;<i>your-folder</i>&gt;/settings/wcm/policies</code></td>
   <td><code>Template Author</code></td>
   <td>läsa, skriva, replikera</td>
   <td>Mallförfattare som skapar, läser, uppdaterar, tar bort och replikerar mallar i platsspecifika <code>/conf</code> space</td>
  </tr>
  <tr>
   <td>Anonym webbanvändare</td>
   <td>read</td>
   <td>En anonym webbanvändare måste läsa principer när en sida återges</td>
  </tr>
  <tr>
   <td>Innehållsförfattare</td>
   <td>replikera</td>
   <td>Innehållsförfattare måste aktivera profilerna för en sidmall när de aktiverar en sida</td>
  </tr>
  <tr>
   <td rowspan="2"><code>/conf/&lt;site&gt;/settings/template-types</code></td>
   <td>Mallförfattare</td>
   <td>read</td>
   <td>Mallförfattare skapar en ny mall baserad på en av de fördefinierade malltyperna.</td>
  </tr>
  <tr>
   <td>Anonym webbanvändare</td>
   <td>inga</td>
   <td>En anonym webbanvändare får inte komma åt malltyperna</td>
  </tr>
 </tbody>
</table>

Den här standardinställningen `template-authors` gruppen täcker endast projektinställningarna, där alla `template-authors` -medlemmar har åtkomst till och kan redigera alla mallar. För mer komplexa konfigurationer, där flera mallförfattargrupper behövs för att separera åtkomsten till mallar, måste fler anpassade mallskapargrupper skapas. Behörigheterna för mallförfattargrupperna är dock fortfarande desamma.

#### Äldre mallar under /conf/global {#legacy-templates-under-conf-global}

Mallar bör inte längre lagras i `/conf/global`Men för vissa äldre installationer kan det fortfarande finnas mallar på den här platsen. Endast i sådana äldre situationer bör följande `/conf/global` sökvägar konfigureras explicit.

<table>
 <tbody>
  <tr>
   <th>Bana</th>
   <th>Roll/grupp</th>
   <th>Behörigheter<br /> </th>
   <th>Beskrivning</th>
  </tr>
  <tr>
   <td rowspan="3"><code>/conf/global/settings/wcm/templates</code></td>
   <td>Mallförfattare</td>
   <td>läsa, skriva, replikera</td>
   <td>Mallförfattare som skapar, läser, uppdaterar, tar bort och replikerar mallar i <code>/conf/global</code></td>
  </tr>
  <tr>
   <td>Anonym webbanvändare</td>
   <td>read</td>
   <td>En anonym webbanvändare måste läsa mallar när en sida återges</td>
  </tr>
  <tr>
   <td>Innehållsförfattare</td>
   <td>replikera</td>
   <td>Innehållsförfattare måste aktivera mallarna för en sida när de aktiverar en sida</td>
  </tr>
  <tr>
   <td rowspan="3"><code>/conf/global/settings/wcm/policies</code></td>
   <td><code>Template Author</code></td>
   <td>läsa, skriva, replikera</td>
   <td>Mallförfattare som skapar, läser, uppdaterar, tar bort och replikerar mallar i <code>/conf/global</code></td>
  </tr>
  <tr>
   <td>Anonym webbanvändare</td>
   <td>read</td>
   <td>En anonym webbanvändare måste läsa principer när en sida återges</td>
  </tr>
  <tr>
   <td>Innehållsförfattare</td>
   <td>replikera</td>
   <td>Innehållsförfattare måste aktivera profilerna för en sidmall när de aktiverar en sida</td>
  </tr>
  <tr>
   <td rowspan="2"><code>/conf/global/settings/wcm/template-types</code></td>
   <td>Mallförfattare</td>
   <td>read</td>
   <td>Mallförfattare skapar en ny mall baserad på en av de fördefinierade malltyperna</td>
  </tr>
  <tr>
   <td>Anonym webbanvändare</td>
   <td>inga</td>
   <td>En anonym webbanvändare får inte komma åt malltyperna</td>
  </tr>
 </tbody>
</table>

## Malltyp {#template-type}

När du skapar en ny mall måste du ange en malltyp:

* Malltyper tillhandahåller effektivt mallar för en mall. När du skapar en ny mall används strukturen och det ursprungliga innehållet för den valda malltypen för att skapa till den nya mallen.

   * Malltypen kopieras för att skapa mallen.
   * När kopian är klar är den enda kopplingen mellan mallen och malltypen en statisk referens i informationssyfte.

* Med malltyper kan du definiera:

   * Sidkomponentens resurstyp.
   * Rotnodens princip, som definierar vilka komponenter som tillåts i mallredigeraren.
   * Vi rekommenderar att du definierar brytpunkter för responsiva rutnät och inställningar för mobilemulatorn på malltypen. Detta är valfritt eftersom konfigurationen också kan definieras för den enskilda mallen (se [Malltyp och mobila enhetsgrupper](/help/sites-developing/page-templates-editable.md#p-template-type-and-mobile-device-groups-br-p)).

* AEM innehåller ett litet urval av färdiga malltyper som HTML5 Page och Adaptive Form Page.

   * Ytterligare exempel finns som en del av [Vi.butik](/help/sites-developing/we-retail.md) exempelinnehåll.

* Malltyper definieras vanligtvis av utvecklare.

Malltyperna som inte finns lagrade under:

* `/libs/settings/wcm/template-types`

>[!CAUTION]
>
>Du får inte ändra något i `/libs` bana. Detta beror på innehållet i `/libs` skrivs över nästa gång du uppgraderar din instans (och kan skrivas över när du använder en snabbkorrigering eller ett funktionspaket).

Platsspecifika malltyper bör lagras på samma plats som:

* `/apps/settings/wcm/template-types`

Definitioner för dina anpassade malltyper bör lagras i användardefinierade mappar (rekommenderas) eller alternativt i `global`. Till exempel:

* `/conf/<my-folder-01>/<my-folder-02>/settings/wcm/template-types`
* `/conf/<my-folder>/settings/wcm/template-types`
* `/conf/global/settings/wcm/template-types`

>[!CAUTION]
>
>Malltyperna måste ta hänsyn till rätt mappstruktur (dvs. `/settings/wcm/...`), annars går det inte att hitta malltyperna.

### Malltyp och mobila enhetsgrupper {#template-type-and-mobile-device-groups-br}

The [enhetsgrupper](/help/sites-developing/mobile.md#device-groups) används för en redigerbar mall (anges som relativ sökväg för egenskapen) `cq:deviceGroups`) definierar vilka mobila enheter som är tillgängliga som emulatorer i [layoutläge](/help/sites-authoring/responsive-layout.md) för att skapa sidor. Det här värdet kan anges på två platser:

* På den redigerbara malltypen
* På den redigerbara mallen

När du skapar en ny redigerbar mall kopieras värdet från malltypen till den enskilda mallen. Om värdet inte anges för typen kan det anges i mallen. När en mall har skapats finns det inget arv från typen till mallen.

>[!CAUTION]
>
>Värdet för `cq:deviceGroups` måste anges som en relativ sökväg som `mobile/groups/responsive` och inte som en absolut sökväg som `/etc/mobile/groups/responsive`.

>[!NOTE]
>
>Med [statiska mallar](/help/sites-developing/page-templates-static.md), värdet av `cq:deviceGroups` kan anges i platsens rot.
>
>Med redigerbara mallar lagras det här värdet nu på mallnivå och stöds inte på sidrotnivån.

### Skapa malltyper {#creating-template-types}

Om du har skapat en mall som kan användas som bas för andra mallar kan du kopiera den här mallen som en malltyp.

1. Skapa en mall precis som vilken redigerbar mall som helst [dokumenteras här](/help/sites-authoring/templates.md#creating-a-new-template-template-author), som kommer att fungera som bas för din malltyp.
1. Kopiera den nya mallen från CRXDE Lite med hjälp av `templates` nod till `template-types` noden under [mallmapp](/help/sites-developing/page-templates-editable.md#template-folders).
1. Ta bort mallen från `templates` noden under [mallmapp](/help/sites-developing/page-templates-editable.md#template-folders).
1. I kopian av mallen som finns under `template-types` nod, ta bort alla `cq:template` och `cq:templateType` `jcr:content` egenskaper.

Du kan också utveckla en egen malltyp med en exempelredigerbar mall som bas, som finns på GitHub.

KOD PÅ GITHUB

Koden för den här sidan finns på GitHub

* [Öppna aem-sites-example-custom-template-type-projekt på GitHub](https://github.com/Adobe-Marketing-Cloud/aem-sites-example-custom-template-type)
* Hämta projektet som [en ZIP-fil](https://github.com/Adobe-Marketing-Cloud/aem-sites-example-custom-template-type/archive/master.zip)

## Malldefinitioner {#template-definitions}

Definitioner för redigerbara mallar sparas [användardefinierade mappar](/help/sites-developing/page-templates-editable.md#template-folders) (rekommenderas) eller `global`. Till exempel:

* `/conf/<my-folder>/settings/wcm/templates`
* `/conf/<my-folder-01>/<my-folder-02>/settings/wcm/templates`
* `/conf/global/settings/wcm/templates`

Mallens rotnod är av typen `cq:Template` med en skelettstruktur på

```xml
<template-name>
  initial
    jcr:content
      root
        <component>
        ...
        <component>
  jcr:content
    @property status
  policies
    jcr:content
      root
        @property cq:policy
        <component>
          @property cq:policy
        ...
        <component>
          @property cq:policy
  structure
    jcr:content
      root
        <component>
        ...
        <component>
      cq:responsive
        breakpoints
  thumbnail.png
```

Huvudelementen är:

* `<template-name>`

   * ` [initial](#initial-content)`
   * `jcr:content`
   * ` [structure](#structure)`
   * ` [policies](#policies)`
   * `thumbnail.png`

### jcr:innehåll {#jcr-content}

Den här noden innehåller egenskaper för mallen:

* **Namn**: `jcr:title`

* **Namn**: `status`

   * **Typ**: `String`

   * **Värde**: `draft`, `enabled` eller `disabled`

### Struktur {#structure}

Definierar strukturen för den resulterande sidan:

* Sammanfogas med det ursprungliga innehållet ( `/initial`) när du skapar en ny sida.
* Ändringar som görs i strukturen återspeglas i alla sidor som skapas med mallen.
* The `root` ( `structure/jcr:content/root`)-noden definierar listan med komponenter som ska vara tillgängliga på den resulterande sidan.

   * Komponenter som definieras i mallstrukturen kan inte flyttas eller tas bort från resultatsidor.
   * När en komponent har låsts upp `editable` egenskapen är inställd på `true`.

   * När en komponent som redan innehåller innehåll är olåst flyttas det här innehållet till `initial` förgrening.

* The `cq:responsive` noden innehåller definitioner för den responsiva layouten.

### Ursprungligt innehåll {#initial-content}

Definierar det ursprungliga innehåll som en ny sida kommer att ha när den skapas:

* Innehåller en `jcr:content` nod som kopieras till nya sidor.
* Sammanfogas med strukturen ( `/structure`) när du skapar en ny sida.
* Befintliga sidor uppdateras inte om det ursprungliga innehållet ändras efter att de har skapats.
* The `root` noden innehåller en lista med komponenter för att definiera vad som ska vara tillgängligt på den resulterande sidan.
* Om innehåll läggs till i en komponent i strukturläge och den komponenten sedan låses upp (eller vice versa), används det här innehållet som ursprungligt innehåll.

### Layout {#layout}

När [redigera en mall kan du definiera layouten](/help/sites-authoring/templates.md)används [responsiv standardlayout](/help/sites-authoring/responsive-layout.md) som också kan [konfigurerad](/help/sites-administering/configuring-responsive-layout.md).

### Innehållsprofiler {#content-policies}

Innehållets (eller designens) profiler definierar en komponents designegenskaper. Till exempel de tillgängliga komponenterna eller minimi-/maximidimensionerna. Dessa gäller för mallen (och sidor som skapas med mallen). Du kan skapa och välja innehållsprinciper i mallredigeraren.

* Egenskapen `cq:policy`, på `root` nod
   `/conf/<your-folder>/settings/wcm/templates/<your-template>/policies/jcr:content/root`
Ger en relativ referens till innehållsprincipen för sidans styckesystem.

* Egenskapen `cq:policy`, på de komponentspecifika noderna under `root`, innehåller länkar till profilerna för de enskilda komponenterna.

* De faktiska principdefinitionerna lagras under:
   `/conf/<your-folder>/settings/wcm/policies/wcm/foundation/components`

>[!NOTE]
>
>Sökvägarna för principdefinitioner beror på komponentens sökväg. `cq:policy` innehåller en relativ referens till själva konfigurationen.

>[!NOTE]
>
>Sidor som skapas från redigerbara mallar har inte något designläge i sidredigeraren.
>
>The `policies` -trädet i en redigerbar mall har samma hierarki som designlägeskonfigurationen för en statisk mall under:
>
>`/etc/designs/<my-site>/jcr:content/<component-name>`
>
>Konfiguration av designläge för en statisk mall har definierats per sidkomponent.

### Sidprofiler {#page-policies}

Med sidprofiler kan du definiera [innehållsprincip](#content-policies) för sidan (huvudparametrar), antingen i mallen eller på de resulterande sidorna.

### Aktivera och tillåta en mall för användning {#enabling-and-allowing-a-template-for-use}

1. **Aktivera mallen**

   Innan en mall kan användas måste den aktiveras av något av följande:

   * [Aktivera mallen](/help/sites-authoring/templates.md#enablingatemplateauthor) från **Mallar** konsol.

   * Ställa in egenskapen status på `jcr:content` nod.

      * På:
         `/conf/<your-folder>/settings/wcm/templates/<your-template>/jcr:content`

      * Definiera egenskapen:

         * Namn: status
         * Typ: Sträng
         * Värde: `enabled`

1. **Tillåtna mallar**

   * [Definiera tillåtna mallsökvägar på **Sidegenskaper**](/help/sites-authoring/templates.md#allowing-a-template-author) av rätt sida eller rotsida i en underavdelning.
   * Ange egenskapen:
      `cq:allowedTemplates`
På 
`jcr:content` noden för den begärda grenen.
   Med till exempel värdet:

   `/conf/<your-folder>/settings/wcm/templates/.*`

## Gällande innehållssidor {#resultant-content-pages}

Sidor skapade från redigerbara mallar:

* Skapas med ett underträd som sammanfogas från `structure` och `initial` i mallen

* Har referenser till information som finns i mallen och malltypen. Detta uppnås med en `jcr:content` nod med egenskaperna:

   * `cq:template`
innehåller en dynamisk referens till den faktiska mallen, gör att ändringar i mallen kan återspeglas på de faktiska sidorna.

   * `cq:templateType`
Anger en referens till malltypen.

![chlimage_1-71](assets/chlimage_1-71.png)

Diagrammet ovan visar hur mallar, innehåll och komponenter samverkar:

* Styrenhet - `/content/<my-site>/<my-page>`
Den resulterande sidan som refererar till mallen. Innehållet styr hela processen. Enligt definitionerna har den åtkomst till rätt mall och komponenter.

* Konfiguration - `/conf/<my-folder>/settings/wcm/templates/<my-template>`
The [mallar och relaterade innehållsprinciper](#template-definitions) definiera sidkonfigurationen.

* Modell - OSGi bundles The [OSGI-paket](/help/sites-deploying/osgi-configuration-settings.md) implementera funktionen.

* Visa - `/apps/<my-site>/components`
I både författar- och publiceringsmiljöer återges innehållet av [komponenter](/help/sites-developing/components.md).

Vid återgivning av en sida:

* **Mallar**:

   * The `cq:template` egenskap för dess `jcr:content` Noden kommer att refereras till för att komma åt mallen som motsvarar den sidan.

* **Komponenter**:

   * Sidkomponenten kommer att sammanfoga `structure/jcr:content` mallens träd med `jcr:content` sidans träd.

   * Sidkomponenten tillåter bara författaren att redigera noderna i mallstrukturen som har flaggats som redigerbara (samt eventuella underordnade noder).
   * När du återger en komponent på en sida hämtas komponentens relativa sökväg från `jcr:content` nod; samma bana under `policies/jcr:content` -noden i mallen söks sedan igenom.

      * The `cq:policy` den här nodens egenskap pekar på den faktiska innehållsprincipen (d.v.s. den innehåller komponentens designkonfiguration).

      * På så sätt kan du ha flera mallar som återanvänder samma innehållsprincipkonfigurationer.
