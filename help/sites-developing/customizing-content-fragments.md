---
title: Anpassa och utöka Content Fragments
seo-title: Customizing and Extending Content Fragments
description: Ett innehållsfragment utökar en standardresurs. Lär dig hur du kan anpassa dem.
seo-description: A content fragment extends a standard asset. Learn how you can customize them.
topic-tags: extending-aem
content-type: reference
docset: aem65
exl-id: 08c88e70-4df9-4627-8a66-1fabe3aee50b
source-git-commit: 38f0496d9340fbcf383a2d39dba8efcbdcd20c6f
workflow-type: tm+mt
source-wordcount: '2794'
ht-degree: 0%

---


# Anpassa och utöka Content Fragments{#customizing-and-extending-content-fragments}

Ett innehållsfragment utökar en standardresurs, se:

* [Skapa och hantera innehållsfragment](/help/assets/content-fragments/content-fragments.md) och [Sidredigering med innehållsfragment](/help/sites-authoring/content-fragments.md) för mer information om innehållsfragment.

* [Hantera resurser](/help/assets/manage-assets.md) och [Anpassa och utöka resurser](/help/assets/extending-assets.md) för mer information om standardtillgångar.

## Arkitektur {#architecture}

Grundläggande [beståndsdelar](/help/assets/content-fragments/content-fragments.md#constituent-parts-of-a-content-fragment) för ett innehållsfragment är:

* A *Innehållsfragment,*
* bestående av en eller flera *Innehållselement* s,
* och som kan ha en eller flera *Innehållsvariation* s.

Beroende på fragmenttypen används även modeller eller mallar:

>[!CAUTION]
>
>[Modeller för innehållsfragment](/help/assets/content-fragments/content-fragments-models.md) Vi rekommenderar att du skapar alla nya fragment.
>
>Content Fragment Models används för alla exempel i WKND.

>[!NOTE]
>
>Före AEM 6.3 skapades innehållsfragment baserade på mallar i stället för modeller.
>
>Mallar för innehållsfragment är nu föråldrade. De kan fortfarande användas för att skapa fragment, men du bör använda Content Fragment Models i stället. Inga nya funktioner kommer att läggas till i fragmentmallar och de kommer att tas bort i en framtida version.

* Modeller för innehållsfragment:

   * Används för att definiera innehållsfragment som innehåller strukturerat innehåll.
   * Modeller för innehållsfragment definierar strukturen för ett innehållsfragment när det skapas.
   * Ett fragment refererar till modellen, så ändringar i modellen kan påverka alla beroende fragment.
   * Modeller är inbyggda i datatyper.
   * Funktioner för att lägga till nya varianter, och så vidare, måste uppdatera fragmentet därefter.

  >[!CAUTION]
  >
  >Alla ändringar i en befintlig innehållsfragmentmodell kan påverka beroende fragment, vilket kan leda till överblivna egenskaper i dessa fragment.

* Mallar för innehållsfragment:

   * Används för att definiera enkla innehållsfragment.
   * Mallar definierar (grundläggande, endast text) strukturen för ett innehållsfragment när det skapas.
   * Mallen kopieras till fragmentet när den skapas, så fler ändringar av mallen återspeglas inte i befintliga fragment.
   * Funktioner för att lägga till nya varianter, och så vidare, måste uppdatera fragmentet därefter.
   * [Mallar för innehållsfragment](/help/sites-developing/content-fragment-templates.md) fungerar på ett annat sätt än andra mallfunktioner i det AEM ekosystemet (till exempel sidmallar och så vidare). De bör därför beaktas separat.
   * När MIME-typen för innehållet baseras på en mall hanteras det faktiska innehållet. Det innebär att varje element och variant kan ha olika MIME-typer.

### Integrering med Assets {#integration-with-assets}

Content Fragment Management (CFM) ingår i AEM Assets som:

* Innehållsfragment är resurser.
* De använder befintliga Assets-funktioner.
* De är helt integrerade med Assets (administrationskonsoler och så vidare).

#### Mappa strukturerade innehållsfragment till resurser {#mapping-structured-content-fragments-to-assets}

![fragment-till-tillgångar-strukturerad](assets/fragment-to-assets-structured.png)

Innehållsfragment med strukturerat innehåll (d.v.s. baserat på en innehållsfragmentmodell) mappas till en enda resurs:

* Allt innehåll lagras under `jcr:content/data` resursens nod:

   * Elementdata lagras under huvudundernoden:
     `jcr:content/data/master`

   * Variationer lagras under en undernod som innehåller variantens namn, till exempel: `jcr:content/data/myvariation`

   * Data för varje element lagras i respektive undernod som en egenskap med elementnamnet: till exempel elementets innehåll `text` lagras som egenskap `text` på `jcr:content/data/master`

* Metadata och tillhörande innehåll lagras nedan `jcr:content/metadata`
Förutom rubriken och beskrivningen, som inte betraktas som traditionella metadata och lagras på `jcr:content`

#### Mappa enkla innehållsfragment till resurser {#mapping-simple-content-fragments-to-assets}

![chlimage_1-90](assets/chlimage_1-90.png)

Enkla innehållsfragment (som baseras på en mall) mappas till en sammansatt resurs som består av en huvudresurs och (valfritt) underresurser:

* All icke-innehållsinformation i ett fragment (som titel, beskrivning, metadata, struktur) hanteras exklusivt på huvudresursen.
* Innehållet i det första elementet i ett fragment mappas till huvudresursens ursprungliga återgivning.

   * Variationerna (om det finns några) för det första elementet mappas till andra återgivningar av huvudresursen.

* Ytterligare element (om sådana finns) mappas till deltillgångar i huvudtillgången.

   * Huvudinnehållet i dessa ytterligare element mappas till den ursprungliga återgivningen av respektive underresurs.
   * Andra variationer (om tillämpligt) av eventuella ytterligare element överensstämmer med andra återgivningar av respektive deltillgång.

#### Resursplats {#asset-location}

Precis som med standardresurser finns ett innehållsavdrag under:

`/content/dam`

#### Tillgångsbehörigheter {#asset-permissions}

Mer information finns i [Innehållsfragment - Ta bort överväganden](/help/assets/content-fragments/content-fragments-delete.md).

#### Funktionsintegrering {#feature-integration}

* Funktionen Content Fragment Management (CFM) bygger på Assets core, men bör vara så oberoende som möjligt.
* CFM har sina egna implementeringar för objekt i vyerna kort, kolumn och lista. Dessa plugin finns i befintliga resursåtergivningsimplementationer.
* Flera Assets-komponenter har utökats för att passa innehållsfragment.

### Använda innehållsfragment på sidor {#using-content-fragments-in-pages}

>[!CAUTION]
>
>The [Kärnkomponent för innehållsfragment](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/content-fragment-component.html) rekommenderas nu. Se [Utveckla kärnkomponenter](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/overview.html) för mer information.

Innehållsfragment kan refereras från AEM sidor, precis som andra resurstyper. AEM tillhandahåller [**Innehållsfragment** kärnkomponent](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/content-fragment-component.html) - en [som gör att du kan ta med innehållsfragment på sidorna](/help/sites-authoring/content-fragments.md#adding-a-content-fragment-to-your-page). Du kan också utöka **Innehållsfragment** kärnkomponent.

* Komponenten använder `fragmentPath` -egenskap som refererar till det faktiska innehållsfragmentet. The `fragmentPath` -egenskapen hanteras på samma sätt som liknande egenskaper för andra resurstyper, till exempel när innehållsfragmentet flyttas till en annan plats.

* Med komponenten kan du välja den variant som ska visas.
* Dessutom kan ett styckeintervall markeras för att begränsa utdata. Det kan till exempel användas för utdata med flera kolumner.
* Komponenten tillåter [mellanliggande innehåll](/help/sites-developing/components-content-fragments.md#in-between-content):

   * Här kan du placera andra resurser (bilder och så vidare) mellan styckena i det refererade fragmentet.
   * För det mellanliggande innehållet behöver du:

      * vara medveten om risken för instabila referenser. Mellanliggande innehåll (som läggs till när en sida redigeras) har ingen fast relation till det stycke som det placeras bredvid, infogning av ett nytt stycke (i innehållsfragmentredigeraren) innan placeringen av det mellanliggande innehållet kan förlora den relativa positionen
      * ta hänsyn till ytterligare parametrar (som variation och styckefilter) för att undvika falska positiva resultat i sökresultaten

>[!NOTE]
>
>**Content Fragment Model:**
>
>När du använder ett innehållsfragment som har baserats på en innehållsfragmentmodell på en sida, refereras modellen. Det innebär att om modellen inte har publicerats när du publicerar sidan, kommer den att flaggas och läggas till i resurserna som ska publiceras med sidan.
>
>**Innehållsfragmentmall:**
>
>När du använder ett innehållsfragment som har baserats på en mall för innehållsfragment på en sida, finns det ingen referens när mallen kopierades när fragmentet skapades.

#### Konfiguration med OSGi-konsol {#configuration-using-osgi-console}

Serverdelsimplementeringen av innehållsfragment ansvarar till exempel för att göra instanser av ett fragment som används på en sida sökbara eller för hantering av blandat medieinnehåll. Den här implementeringen behöver veta vilka komponenter som används för att återge fragment och hur återgivningen är parametriserad.

Parametrarna för detta kan konfigureras i [Webbkonsol](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console), för OSGi-paketet **Konfiguration av komponent för innehållsfragment**.

* **Resurstyper**
En lista med `sling:resourceTypes` kan anges för att definiera komponenter som används för att återge innehållsfragment och var bakgrundsbearbetningen ska användas.

* **Referensegenskaper**
En lista med egenskaper kan konfigureras för att ange var referensen till fragmentet lagras för respektive komponent.

>[!NOTE]
>
>Det finns ingen direkt mappning mellan egenskap- och komponenttyp.
>
>AEM tar bara den första egenskapen som finns i ett stycke. Du bör därför välja egenskaperna noggrant.

![screenshot_2019-03-18at100941](assets/screenshot_2019-03-18at100941.png)

Det finns fortfarande några riktlinjer som du måste följa för att se till att komponenten är kompatibel med bakgrundsbearbetningen av innehållsfragment:

* Namnet på egenskapen där elementen som ska återges är antingen `element` eller `elementNames`.

* Namnet på egenskapen där variationen som ska återges är antingen `variation` eller `variationName`.

* Om utdata från flera element stöds (med `elementNames` om du vill ange flera element), definieras det faktiska visningsläget av egenskapen `displayMode`:

   * Om värdet är `singleText` (och bara ett element är konfigurerat) återges elementet som en text med mellanliggande innehåll, layoutstöd osv. Det här är standardinställningen för fragment där endast ett element återges.
   * I annat fall används en mycket enklare metod (kan kallas&quot;formulärvy&quot;), där inget mellanliggande innehåll stöds och fragmentinnehållet återges som det är.

* Om fragmentet återges för `displayMode` == `singleText` (implicit eller explicit) spelas följande ytterligare egenskaper upp:

   * `paragraphScope` definierar om alla stycken, eller bara ett styckeintervall, ska återges (värden: `all` jämfört med `range`)

   * if `paragraphScope` == `range` sedan egenskapen `paragraphRange` definierar det styckeintervall som ska återges

### Integrering med andra ramar {#integration-with-other-frameworks}

Innehållsfragment kan integreras med:

* **Översättningar**

  Innehållsfragment är helt integrerade med [Arbetsflöde för AEM](/help/sites-administering/tc-manage.md). Arkitekturnivå innebär följande:

   * De enskilda översättningarna av ett innehållsfragment är egentligen separata fragment, till exempel:

      * De finns under olika språkrötter:

        `/content/dam/<path>/en/<to>/<fragment>`

        jämfört med

        `/content/dam/<path>/de/<to>/<fragment>`

      * men de delar exakt samma relativa sökväg under språkroten:

        `/content/dam/<path>/en/<to>/<fragment>`

        jämfört med

        `/content/dam/<path>/de/<to>/<fragment>`

   * Förutom de regelbaserade sökvägarna finns det ingen ytterligare koppling mellan de olika språkversionerna av ett innehållsfragment. De hanteras som två separata fragment, även om gränssnittet ger möjlighet att navigera mellan språkvarianterna.

  >[!NOTE]
  >
  >Det AEM arbetsflödet för översättning fungerar med `/content`:
  >
  >* När innehållsfragmentsmodellerna finns i `/conf`, ingår de inte i sådana översättningar. Du kan [Internationalisera gränssnittssträngar](/help/sites-developing/i18n-dev.md).
  >
  >* Mallar kopieras för att skapa fragmentet så detta är implicit.

* **Metadata-scheman**

   * Innehållsfragment (återanvänd) [metadatamodeller](/help/assets/metadata-schemas.md), som kan definieras med standardresurser.
   * CFM har ett eget specifikt schema:

     `/libs/dam/content/schemaeditors/forms/contentfragment`

     detta kan vid behov förlängas.

   * respektive schemaformulär är integrerat med fragmentredigeraren.

## API för hantering av innehållsfragment - serversidan {#the-content-fragment-management-api-server-side}

Du kan använda serversidans API för att komma åt dina innehållsfragment. Se:

[com.adobe.cq.dam.cfm](https://www.adobe.io/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/dam/cfm/package-summary.html)

>[!CAUTION]
>
>Vi rekommenderar att du använder serversidans API i stället för att komma åt innehållsstrukturen direkt.

### Nyckelgränssnitt {#key-interfaces}

Följande tre gränssnitt kan fungera som startpunkter:

* **Fragmentmall** ([FragmentTemplate](https://www.adobe.io/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/dam/cfm/FragmentTemplate.html))

  Använd `FragmentTemplate.createFragment()` för att skapa ett fragment.

  ```
  Resource templateOrModelRsc = resourceResolver.getResource("...");
  FragmentTemplate tpl = templateOrModelRsc.adaptTo(FragmentTemplate.class);
  ContentFragment newFragment = tpl.createFragment(parentRsc, "A fragment name", "A fragment description.");
  ```

  Gränssnittet representerar:

   * antingen en modell för innehållsfragment eller en mall för innehållsfragment från vilken ett innehållsfragment ska skapas,
   * och (efter det att fragmentet har skapats) strukturinformationen

  Denna information kan omfatta:

   * Få tillgång till grundläggande data (titel, beskrivning)
   * Få åtkomst till mallar/modeller för elementen i fragmentet:

      * Mallar för listelement
      * Hämta strukturinformation för ett givet element
      * Åtkomst till elementmallen (se `ElementTemplate`)

   * Åtkomstmallar för variationerna av fragmentet:

      * Lista variantmallar
      * Hämta strukturinformation för en viss variation
      * Åtkomst till variantmallen (se `VariationTemplate`)

   * Hämta initialt associerat innehåll

  Gränssnitt som representerar viktig information:

   * `ElementTemplate`

      * Hämta grundläggande data (namn, titel)
      * Hämta ursprungligt elementinnehåll

   * `VariationTemplate`

      * Hämta grundläggande data (namn, titel, beskrivning)

* **Innehållsfragment** ([ContentFragment](https://www.adobe.io/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/dam/cfm/ContentFragment.html))

  Med det här gränssnittet kan du arbeta med ett innehållsfragment på ett abstrakt sätt.

  >[!CAUTION]
  >
  >Vi rekommenderar starkt att du använder ett fragment via det här gränssnittet. Man bör undvika att ändra innehållsstrukturen direkt.

  Gränssnittet ger dig möjlighet att

   * Hantera grundläggande data (till exempel get name; get/set title/description)
   * Åtkomst till metadata
   * Åtkomstelement:

      * Listelement
      * Hämta element efter namn
      * Skapa nya element (se [Caveats](#caveats))

      * Åtkomst till elementdata (se `ContentElement`)

   * Listvarianter definierade för fragmentet
   * Skapa nya varianter globalt
   * Hantera associerat innehåll:

      * Listsamlingar
      * Lägg till samlingar
      * Ta bort samlingar

   * Åtkomst till fragmentets modell eller mall

  Gränssnitt som representerar de primära elementen i ett fragment är:

   * **Innehållselement** ([ContentElement](https://www.adobe.io/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/dam/cfm/ContentElement.html))

      * Hämta grundläggande data (namn, titel, beskrivning)
      * Hämta/ange innehåll
      * Få åtkomst till varianter av ett element:

         * Listvarianter
         * Hämta varianter efter namn
         * Skapa nya varianter (se [Caveats](#caveats))
         * Ta bort variationer (se [Caveats](#caveats))
         * Åtkomst till variantdata (se `ContentVariation`)

      * Kortkommando för att matcha variationer (tillämpa ytterligare, implementeringsspecifik reservlogik om den angivna varianten inte är tillgänglig för ett element)

   * **Innehållsvariation** ([ContentVariation](https://www.adobe.io/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/dam/cfm/ContentVariation.html))

      * Hämta grundläggande data (namn, titel, beskrivning)
      * Hämta/ange innehåll
      * Enkel synkronisering, baserat på den senast ändrade informationen

  Alla tre gränssnitten ( `ContentFragment`, `ContentElement`, `ContentVariation`) utöka `Versionable` gränssnitt, som lägger till versionsfunktioner, som krävs för innehållsfragment:

   * Skapa en ny version av elementet
   * Lista versioner av elementet
   * Hämta innehållet i en specifik version av det versionshanterade elementet

### Adapting - Using customito() {#adapting-using-adaptto}

Följande kan anpassas:

* `ContentFragment` kan anpassas till

   * `Resource` - den underliggande Sling-resursen, observera att uppdateringen av den underliggande `Resource` direkt, kräver att `ContentFragment` -objekt.

   * `Asset` - DAM `Asset` abstraktion som representerar innehållsfragmentet. Observera att uppdaterar `Asset` direkt, kräver att `ContentFragment` -objekt.

* `ContentElement` kan anpassas till

   * `ElementTemplate` - för åtkomst till elementets strukturinformation.

* `FragmentTemplate` kan anpassas till

   * `Resource` - `Resource` fastställa den refererade modellen eller originalmallen som kopierades,

      * ändringar som gjorts genom `Resource` återspeglas inte automatiskt i `FragmentTemplate`.

* `Resource` kan anpassas till

   * `ContentFragment`
   * `FragmentTemplate`

### Caveats {#caveats}

Det bör noteras att

* API:t implementeras för att tillhandahålla funktioner som stöds av användargränssnittet.
* Hela API:t är utformat för **not** Bevara ändringarna automatiskt (om inget annat anges i API JavaDoc). Därför måste du alltid implementera resurslösaren för respektive begäran (eller den lösare som du använder).
* Uppgifter som kan kräva ytterligare arbete:

   * När du skapar/tar bort nya element uppdateras inte datastrukturen för enkla fragment (baserat på en fragmentmall).
   * Skapa nya varianter från `ContentElement` uppdaterar inte datastrukturen (men skapar dem globalt från) `ContentFragment` will).

   * Om du tar bort befintliga varianter uppdateras inte datastrukturen.

## API:t för hantering av innehållsfragment - klientsidan {#the-content-fragment-management-api-client-side}

>[!CAUTION]
>
>För AEM 6.5 är klientsidans API internt.

### Ytterligare information {#additional-information}

Se följande:

* `filter.xml`

  The `filter.xml` för hantering av innehållsfragment konfigureras så att den inte överlappar det centrala resurspaketet.

## Redigera sessioner {#edit-sessions}

En redigeringssession startas när användaren öppnar ett innehållsfragment på någon av redigeringssidorna. Redigeringssessionen är slut när användaren lämnar redigeraren genom att välja antingen **Spara** eller **Avbryt**.

### Krav {#requirements}

Krav för att styra en redigeringssession är:

* Att redigera ett innehållsfragment, som kan sträcka sig över flera vyer (= HTML-sidor), bör vara atomiskt.
* Redigeringen bör också vara *transaktionsbaserad*; i slutet av redigeringssessionen måste ändringarna antingen verkställas (sparas) eller återställas (avbrytas).
* Kantärenden ska hanteras på rätt sätt, t.ex. när användaren lämnar sidan genom att ange en URL manuellt eller använda global navigering.
* Det bör finnas en periodisk autosparfunktion (var x:e minut) för att förhindra dataförlust.
* Om ett innehållsfragment redigeras av två användare samtidigt bör de inte skriva över varandras ändringar.

#### Processer {#processes}

Processerna är följande:

* Starta en session

   * En ny version av innehållsfragmentet skapas.
   * Spara automatiskt startas.
   * Cookies är inställda. Dessa definierar det redigerade fragmentet och att en redigeringssession är öppen.

* Avsluta en session

   * Autosparande stoppas.
   * Vid implementering:

      * Den senast ändrade informationen uppdateras.
      * Cookies tas bort.

   * Vid återställning:

      * Den version av innehållsfragmentet som skapades när redigeringssessionen startades återställs.
      * Cookies tas bort.

* Redigering

   * Alla ändringar (autosparande ingår) görs på det aktiva innehållsfragmentet - inte i ett avgränsat, skyddat område.
   * Därför återspeglas dessa ändringar direkt på AEM sidor som refererar till respektive innehållsfragment

#### Åtgärder {#actions}

Möjliga åtgärder är:

* Ange en sida

   * Kontrollera om det redan finns en redigeringssession genom att markera respektive cookie.

      * Om det finns någon kontrollerar du att redigeringssessionen startades för det innehållsfragment som redigeras just nu

         * Om det aktuella fragmentet används återupprättar du sessionen.
         * Om inte, försök att avbryta redigeringen för det tidigare redigerade innehållsfragmentet och ta bort cookies (ingen redigeringssession finns efteråt).

      * Om det inte finns någon redigeringssession väntar du på den första ändringen som gjorts av användaren (se nedan).

   * Kontrollera om det redan finns referenser till innehållsfragmentet på en sida och visa lämplig information om så är fallet.

* Innehållsändring

   * När användaren ändrar innehåll och det inte finns någon redigeringssession skapas en ny redigeringssession (se [Starta en session](#processes)).

* Lämna en sida

   * Om det finns en redigeringssession och ändringarna inte har sparats, visas en modal bekräftelsedialogruta som meddelar användaren om potentiellt förlorat innehåll och låter dem stanna kvar på sidan.

## Exempel {#examples}

### Exempel: Åtkomst till ett befintligt innehållsfragment {#example-accessing-an-existing-content-fragment}

För att uppnå detta kan du anpassa resursen som representerar API:t till:

`com.adobe.cq.dam.cfm.ContentFragment`

Till exempel:

```java
// first, get the resource
Resource fragmentResource = resourceResolver.getResource("/content/dam/fragments/my-fragment");
// then adapt it
if (fragmentResource != null) {
    ContentFragment fragment = fragmentResource.adaptTo(ContentFragment.class);
    // the resource is now accessible through the API
}
```

### Exempel: Skapa ett innehållsfragment {#example-creating-a-new-content-fragment}

Om du vill skapa ett innehållsfragment programmatiskt måste du använda:

`com.adobe.cq.dam.cfm.ContentFragmentManager#create`

Till exempel:

```java
Resource templateOrModelRsc = resourceResolver.getResource("...");
FragmentTemplate tpl = templateOrModelRsc.adaptTo(FragmentTemplate.class);
ContentFragment newFragment = tpl.createFragment(parentRsc, "A fragment name", "A fragment description.");
```

### Exempel: Ange intervall för autosparande {#example-specifying-the-auto-save-interval}

Intervallet för att spara automatiskt (anges i sekunder) kan definieras med konfigurationshanteraren (ConfMgr):

* Nod: `<*conf-root*>/settings/dam/cfm/jcr:content`
* Egenskapsnamn: `autoSaveInterval`
* Typ: `Long`

* Standard: `600` (10 minuter); detta definieras på `/libs/settings/dam/cfm/jcr:content`

Om du vill ange ett intervall för automatiskt sparande på 5 minuter måste du definiera egenskapen på noden, till exempel:

* Nod: `/conf/global/settings/dam/cfm/jcr:content`
* Egenskapsnamn: `autoSaveInterval`

* Typ: `Long`

* Värde: `300` (5 minuter motsvarar 300 sekunder)

## Mallar för innehållsfragment {#content-fragment-templates}

Se [Mallar för innehållsfragment](/help/sites-developing/content-fragment-templates.md) för fullständig information.

## Komponenter för sidredigering {#components-for-page-authoring}

Mer information finns i

* [Kärnkomponenter - komponent för innehållsfragment](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/content-fragment-component.html) (rekommenderas)
* [Content Fragment Components - Components for Page Authoring](/help/sites-developing/components-content-fragments.md#components-for-page-authoring)
