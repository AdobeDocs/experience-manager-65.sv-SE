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
feature: Konfigurerar
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '538'
ht-degree: 0%

---


# Resursmappning{#resource-mapping}

Resursmappning används för att definiera omdirigeringar, tillfälliga URL:er och virtuella värdar för AEM.

Du kan till exempel använda dessa mappningar för:

* Använd `/content` som prefix för alla förfrågningar så att den interna strukturen döljs för besökarna på webbplatsen.
* Definiera en omdirigering så att alla begäranden till `/content/en/gateway`-sidan på webbplatsen omdirigeras till `https://gbiv.com/`.

En möjlig HTTP-mappning prefix för alla begäranden till `localhost:4503` med `/content`. En sådan här mappning kan användas för att dölja den interna strukturen för besökarna på webbplatsen så som den tillåter:

`localhost:4503/content/we-retail/en/products.html`

ska nås med:

`localhost:4503/we-retail/en/products.html`

eftersom mappningen automatiskt lägger till prefixet `/content` till `/we-retail/en/products.html`.

>[!CAUTION]
>
>Vanity-URL:er stöder inte regex-mönster.

>[!NOTE]
>
>Mer information finns i Samling-dokumentationen och [Mappningar för resursupplösning](https://sling.apache.org/site/resources.html) och [Resurser](https://sling.apache.org/site/mappings-for-resource-resolution.html).

## Visa mappningsdefinitioner {#viewing-mapping-definitions}

Mappningarna består av två listor som JCR-resurslösaren utvärderar (högst upp) för att hitta en matchning.

Dessa listor kan visas (tillsammans med konfigurationsinformation) under alternativet **JCR ResourceResolver** i Felix-konsolen. till exempel `https://<*host*>:<*port*>/system/console/jcrresolver`:

* Konfiguration
Visar den aktuella konfigurationen (enligt definition för [Resurslösaren för Apache Sling](/help/sites-deploying/osgi-configuration-settings.md#apacheslingresourceresolver)).

* Konfigurationstest
På så sätt kan du ange en URL eller resurssökväg. Klicka på **Lös** eller **Karta** för att bekräfta hur systemet ska omforma posten.

* **Matcha**
mappningsposterListan med poster som används av metoderna ResourceResolver.resolve för att mappa URL:er till Resources.

* **Mappa**
mappningsposterListan med poster som används av metoderna ResourceResolver.map för att mappa resurssökvägar till URL:er.

De två listorna visar olika poster, inklusive de som definieras som standardvärden av programmen. Dessa syftar ofta till att förenkla URL:er för användaren.

Listparet är ett **mönster**, ett reguljärt uttryck som matchar begäran, med en **ersättning** som definierar den omdirigering som ska skjutas upp.

Till exempel:

**Mönster** `^[^/]+/[^/]+/welcome$`

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

### Skapar mappningsdefinitioner i AEM {#creating-mapping-definitions-in-aem}

I en standardinstallation av AEM finns mappen:

`/etc/map/http`

Detta är den struktur som används för att definiera mappningar för HTTP-protokollet. Andra mappar ( `sling:Folder`) kan skapas under `/etc/map` för alla andra protokoll som du vill mappa.

#### Konfigurera en intern omdirigering till /content {#configuring-an-internal-redirect-to-content}

Så här skapar du en mappning som prefixar en begäran till https://localhost:4503/ med `/content`:

1. Navigera till `/etc/map/http` med CRXDE.

1. Skapa en ny nod:

   * **** `sling:Mapping`
TypeDen här nodtypen är avsedd för sådana mappningar, men det är inte obligatoriskt att använda den.

   * **Namn** `localhost_any`

1. Klicka på **Spara alla**.
1. **Lägg** till följande egenskaper för den här noden:

   * **Namn** `sling:match`

      * **Typ** `String`

      * **Värde** `localhost.4503/`
   * **Namn** `sling:internalRedirect`

      * **Typ** `String`

      * **Värde** `/content/`


1. Klicka på **Spara alla**.

Detta kommer att hantera en begäran som:
`localhost:4503/geometrixx/en/products.html`
som if:
`localhost:4503/content/geometrixx/en/products.html`
hade blivit ombedd.

>[!NOTE]
>
>Mer information om tillgängliga sling-egenskaper och hur de kan konfigureras finns i [Resources](https://sling.apache.org/site/mappings-for-resource-resolution.html) i Sling Documentation.

>[!NOTE]
>
>Du kan använda `/etc/map.publish` för att hålla konfigurationerna för publiceringsmiljön. Dessa måste sedan replikeras och den nya platsen ( `/etc/map.publish`) konfigureras för **mappningsplatsen** för [Apache Sling Resource Resolver](/help/sites-deploying/osgi-configuration-settings.md#apacheslingresourceresolver) för publiceringsmiljön.

