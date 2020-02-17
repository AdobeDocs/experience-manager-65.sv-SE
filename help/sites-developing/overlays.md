---
title: Övertäckningar
seo-title: Övertäckningar
description: AEM använder principen om övertäckningar för att du ska kunna utöka och anpassa konsoler och andra funktioner
seo-description: AEM använder principen om övertäckningar för att du ska kunna utöka och anpassa konsoler och andra funktioner
uuid: d14c08fe-04c0-4925-8c99-c6644357919d
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 0470b74c-2c34-4327-afed-b95eefb1d521
translation-type: tm+mt
source-git-commit: 5128a08d4db21cda821de0698b0ac63ceed24379

---


# Övertäckningar{#overlays}

AEM (och tidigare CQ) har länge använt principen med övertäckningar för att kunna utöka och anpassa [konsoler](/help/sites-developing/customizing-consoles-touch.md) och andra funktioner (till exempel [sidredigering](/help/sites-developing/customizing-page-authoring-touch.md)).

Övertäckning är en term som kan användas i många sammanhang. I det här sammanhanget (utökning av AEM) innebär en övertäckning att du tar de fördefinierade funktionerna och lägger in egna definitioner över dem (för att anpassa standardfunktionerna).

I en standardinstans lagras den fördefinierade funktionen under `/libs` och du rekommenderas att definiera övertäckningen (anpassningar) under `/apps` grenen. AEM använder en söksökväg för att hitta en resurs, söker först i `/apps` grenen och sedan i `/libs` grenen ( [söksökvägen kan konfigureras](#configuring-the-search-paths)). Den här mekanismen innebär att övertäckningen (och de anpassningar som definieras där) kommer att ha prioritet.

Sedan AEM 6.0 har ändringar gjorts i hur övertäckningar implementeras och används:

* AEM 6.0 och senare - för [Granite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html)-relaterade övertäckningar (dvs. det beröringsaktiverade gränssnittet)

   * Metod

      * Rekonstruera lämplig `/libs` struktur under `/apps`.

         Detta kräver ingen 1:1-kopia, [Sling Resource Merger](/help/sites-developing/sling-resource-merger.md) används för att korsreferera till de ursprungliga definitioner som krävs. Med Sling Resource Merger får du tillgång till och kan sammanfoga resurser på olika sätt (differentiering).

      * Gör eventuella ändringar under `/apps`.
   * Fördelar

      * Kraftfullare med förändringar under `/libs`.
      * Definiera bara om vad som faktiskt behövs.


* Övertäckningar och övertäckningar som inte är granitövertäckningar före AEM 6.0

   * Metod

      * Kopiera innehåll från `/libs` till `/apps`

         Du måste kopiera hela undergrenen, inklusive egenskaper.

      * Gör eventuella ändringar under `/apps`.
   * Nackdelar

      * Även om dina ändringar inte går förlorade när något ändras under `/libs`kan du behöva återskapa vissa ändringar som sker i övertäckningen under `/apps`.


>[!CAUTION]
>
>Samlingsresursen för [Sling](/help/sites-developing/sling-resource-merger.md) och de relaterade metoderna kan bara användas med [Granite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html). Det innebär att det bara är lämpligt att skapa en övertäckning med en skelettstruktur för det pekaktiverade standardgränssnittet.
>
>Övertäckningar för andra områden (inklusive det klassiska användargränssnittet) innebär att rätt nod och hela understrukturen kopieras och att nödvändiga ändringar görs.

Övertäckningar är den rekommenderade metoden för många ändringar, som att [konfigurera konsoler](/help/sites-developing/customizing-consoles-touch.md#create-a-custom-console) eller [skapa en markeringskategori för resursläsaren på sidopanelen](/help/sites-developing/customizing-page-authoring-touch.md#add-new-selection-category-to-asset-browser) (används vid redigering av sidor). De krävs enligt följande:

* Du ***får inte *göra ändringar i`/libs`grenen **. Alla ändringar du gör kan gå förlorade eftersom den här grenen kan ändras när du:

   * uppgradera till din instans
   * tillämpa en snabbkorrigering
   * installera ett funktionspaket

* De koncentrerar dina ändringar på ett ställe; gör det enklare för dig att spåra, migrera, säkerhetskopiera och/eller felsöka ändringar efter behov.

## Konfigurera sökvägar {#configuring-the-search-paths}

För övertäckningar är den levererade resursen en sammanställning av resurser och egenskaper som har hämtats, beroende på sökvägar som kan definieras:

* Resurslösarens **söksökväg** enligt definitionen i [OSGi-konfigurationen](/help/sites-deploying/configuring-osgi.md) för **Apache Sling Resource Resolver Factory**.

   * Sökvägarnas övre och nedre ordning anger deras respektive prioriteringar.
   * I en standardinstallation är de primära standardvärdena `/apps`, `/libs` vilket innebär att innehållet i `/apps` har högre prioritet än `/libs` (d.v.s. att det *övertäcker* det).

* Två tjänstanvändare behöver JCR:READ-åtkomst till den plats där skripten lagras. Dessa användare är: components-search-service (används av komponenterna com.day.cq.wcm.coreto access/cache) och sling-scripting (används av org.apache.sling.servlets.resolver för att hitta servrar).
* Följande konfiguration måste även konfigureras efter var du placerade dina skript (i det här exemplet under /etc, /libs eller /apps).

   ```
   PID = org.apache.sling.jcr.resource.internal.JcrResourceResolverFactoryImpl
   resource.resolver.searchpath=["/etc","/apps","/libs"]
   resource.resolver.vanitypath.whitelist=["/etc/","/apps/","/libs/","/content/"]
   ```

* Slutligen måste även Serverlösaren konfigureras (i det här exemplet lägger du till /etc)

   ```
   PID = org.apache.sling.servlets.resolver.SlingServletResolver
   servletresolver.paths=["/bin/","/libs/","/apps/","/etc/","/system/","/index.servlet","/login.servlet","/services/"]
   ```

## Exempel på användning {#example-of-usage}

Några exempel beskrivs när:

* [Anpassa konsolerna](/help/sites-developing/customizing-consoles-touch.md)
* [Anpassa sidredigering](/help/sites-developing/customizing-page-authoring-touch.md)

