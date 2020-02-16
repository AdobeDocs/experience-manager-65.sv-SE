---
title: Resursmappning
seo-title: Resursmappning
description: Lär dig hur du definierar omdirigeringar, tillfälliga URL:er och virtuella värdar för AEM genom att använda resursmappning.
seo-description: Lär dig hur du definierar omdirigeringar, tillfälliga URL:er och virtuella värdar för AEM genom att använda resursmappning.
uuid: 2ca2d0e4-6f90-4ecc-82db-26991f08c66f
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
discoiquuid: 3582a4d8-a47b-467a-9e25-cb45f969ec93
docset: aem65
translation-type: tm+mt
source-git-commit: 44eb94b917fe88b7c90c29ec7da553e15be391db

---


# Resursmappning{#resource-mapping}

Resursmappning används för att definiera omdirigeringar, tillfälliga URL:er och virtuella värdar för AEM.

Du kan till exempel använda dessa mappningar för:

* Använd prefix för alla förfrågningar `/content` så att den interna strukturen döljs för besökarna på webbplatsen.
* Definiera en omdirigering så att alla begäranden till `/content/en/gateway` sidan på webbplatsen omdirigeras till `https://gbiv.com/`.

En möjlig HTTP-mappning prefix för alla begäranden `localhost:4503` till `/content`. En sådan här mappning kan användas för att dölja den interna strukturen för besökarna på webbplatsen så som den tillåter:

`localhost:4503/content/we-retail/en/products.html`

ska nås med:

`localhost:4503/we-retail/en/products.html`

när mappningen automatiskt lägger till prefixet `/content` i `/we-retail/en/products.html`.

>[!CAUTION]
>
>Vanity-URL:er stöder inte regex-mönster.

>[!NOTE]
>
>Mer information finns i dokumentationen om Sling och [Mappings for Resource Resolution](https://sling.apache.org/site/resources.html) and [Resources](https://sling.apache.org/site/mappings-for-resource-resolution.html) .

## Visa mappningsdefinitioner {#viewing-mapping-definitions}

Mappningarna består av två listor som JCR-resurslösaren utvärderar (högst upp) för att hitta en matchning.

Dessa listor kan visas (tillsammans med konfigurationsinformation) under **JCR ResourceResolver** -alternativet i Felix-konsolen. till exempel `https://<*host*>:<*port*>/system/console/jcrresolver`:

* KonfigurationVisar den aktuella konfigurationen (enligt definition för [Apache Sling Resource Resolver](/help/sites-deploying/osgi-configuration-settings.md#apacheslingresourceresolver)).

* Konfigurationstest Det här gör att du kan ange en URL eller resurssökväg. Klicka på **Lös** eller **Karta** för att bekräfta hur posten ska omformas.

* **Matcha mappningsposter** Listan över poster som används av metoderna ResourceResolver.resolve för att mappa URL:er till Resources.

* **Mappa mappningsposter** Listan med poster som används av metoderna ResourceResolver.map för att mappa resurssökvägar till URL:er.

De två listorna visar olika poster, inklusive de som definieras som standardvärden av programmen. Dessa syftar ofta till att förenkla URL:er för användaren.

Listorna innehåller ett **mönster**, ett reguljärt uttryck som matchar begäran, med en **ersättning** som definierar den omdirigering som ska skjutas upp.

Till exempel:

**Mönster**`^[^/]+/[^/]+/welcome$`

kommer att aktivera:

**Ersättning** `/libs/cq/core/content/welcome.html`.

omdirigera en begäran:

`https://localhost:4503/welcome` ``

till:

`https://localhost:4503/libs/cq/core/content/welcome.html`

Nya mappningsdefinitioner skapas i databasen.

>[!NOTE]
>
>Det finns många resurser som kan förklara hur du definierar reguljära uttryck. till exempel [https://www.regular-expressions.info/](https://www.regular-expressions.info/).

### Skapa mappningsdefinitioner i AEM {#creating-mapping-definitions-in-aem}

I en standardinstallation av AEM hittar du mappen:

`/etc/map/http`

Detta är den struktur som används för att definiera mappningar för HTTP-protokollet. Andra mappar ( `sling:Folder`) kan skapas under `/etc/map` för andra protokoll som du vill mappa.

#### Konfigurera en intern omdirigering till /content {#configuring-an-internal-redirect-to-content}

Så här skapar du en mappning som prefixar en begäran till https://localhost:4503/ med `/content`:

1. Navigera till med CRXDE `/etc/map/http`.

1. Skapa en ny nod:

   * **Typ** `sling:Mapping`Den här nodtypen är avsedd för sådana mappningar, men det är inte obligatoriskt att använda den.

   * **Namn**`localhost_any`

1. Klicka på **Spara alla**.
1. **Lägg till** följande egenskaper i den här noden:

   * **Namn**`sling:match`

      * **Typ**`String`

      * **Värde**`localhost.4503/`
   * **Namn**`sling:internalRedirect`

      * **Typ**`String`

      * **Värde**`/content/`


1. Klicka på **Spara alla**.

Detta kommer att hantera en begäran som:
`localhost:4503/geometrixx/en/products.html`som om:
`localhost:4503/content/geometrixx/en/products.html`hade begärts.

>[!NOTE]
>
>Mer information om tillgängliga [försäljningsalternativ och hur de kan konfigureras finns i Resurser](https://sling.apache.org/site/mappings-for-resource-resolution.html) i Sling Documentation.

>[!NOTE]
>
>Du kan använda `/etc/map.publish` för att hålla konfigurationerna för publiceringsmiljön. Dessa måste sedan replikeras och den nya platsen ( `/etc/map.publish`) konfigureras för **mappningsplatsen** för [Apache Sling Resource Resolver](/help/sites-deploying/osgi-configuration-settings.md#apacheslingresourceresolver) i publiceringsmiljön.

