---
title: Resursmappning
description: Lär dig hur du definierar omdirigeringar, tillfälliga URL:er och virtuella värdar för Adobe Experience Manager med hjälp av resursmappning.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
docset: aem65
feature: Configuring
exl-id: 3eebdd38-da5b-4c38-868a-22c3c7a97b66
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '507'
ht-degree: 0%

---

# Resursmappning{#resource-mapping}

Resursmappning används för att definiera omdirigeringar, tillfälliga URL:er och virtuella värdar för Adobe Experience Manager (AEM).

Du kan till exempel använda dessa mappningar för:

* Prefix för alla begäranden med `/content` så att den interna strukturen döljs för besökarna på webbplatsen.
* Definiera en omdirigering så att alla förfrågningar till `/content/en/gateway` webbplatsen omdirigeras till `https://gbiv.com/`.

Ett möjligt HTTP-mappningsprefix för alla begäranden till `localhost:4503` med `/content`. En sådan här mappning kan användas för att dölja den interna strukturen för besökarna på webbplatsen så som den tillåter:

`localhost:4503/content/we-retail/en/products.html`

Ska kommas åt med:

`localhost:4503/we-retail/en/products.html`

När mappningen automatiskt lägger till prefixet `/content` till `/we-retail/en/products.html`.

>[!CAUTION]
>
>Vanity-URL:er stöder inte regex-mönster.

>[!NOTE]
>
>Läs Sling-dokumentationen och [Mappningar för resursupplösning](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html) och [Resurs](https://sling.apache.org/documentation/the-sling-engine/resources.html) för ytterligare information.

## Visa mappningsdefinitioner {#viewing-mapping-definitions}

Mappningarna består av två listor som JCR-resurslösaren utvärderar (högst upp) för att hitta en matchning.

De här listorna kan visas (tillsammans med konfigurationsinformation) under **JCR ResourceResolver** Valet av Felix-konsolen, till exempel `https://<*host*>:<*port*>/system/console/jcrresolver`:

* Konfiguration Visar den aktuella konfigurationen (enligt definition för [Resurslösare för Apache Sling](/help/sites-deploying/osgi-configuration-settings.md#apacheslingresourceresolver)).

* Konfigurationstest Här kan du ange en URL eller resurssökväg. Klicka **Lös** eller **Karta** för att bekräfta hur systemet ska omforma posten.

* **Matcha mappningsposter**
Listan över poster som används av metoderna ResourceResolver.resolve för att mappa URL:er till Resources.

* **Mappa mappningsposter**
Listan över poster som används av metoderna ResourceResolver.map för att mappa resurssökvägar till URL:er.

De två listorna visar olika poster, bland annat de som definierats som standard av programmen. Dessa syftar ofta till att förenkla URL:er för användaren.

Listparet a **Mönster**, ett reguljärt uttryck som matchar begäran, med **Ersättning** som definierar den omdirigering som ska skjutas in.

Till exempel:

**Mönster** `^[^/]+/[^/]+/welcome$`

Startar

**Ersättning** `/libs/cq/core/content/welcome.html`.

Så här omdirigerar du en begäran:

`https://localhost:4503/welcome` &quot;

Till:

`https://localhost:4503/libs/cq/core/content/welcome.html`

Nya mappningsdefinitioner skapas i databasen.

>[!NOTE]
>
>Det finns många tillgängliga resurser som förklarar hur du definierar reguljära uttryck. Till exempel: [https://www.regular-expressions.info/](https://www.regular-expressions.info/).

### Skapar mappningsdefinitioner i AEM {#creating-mapping-definitions-in-aem}

I en standardinstallation av AEM finns mappen:

`/etc/map/http`

Detta är den struktur som används för att definiera mappningar för HTTP-protokollet. Andra mappar ( `sling:Folder`) kan skapas under `/etc/map` för andra protokoll som du vill mappa.

#### Konfigurera en intern omdirigering till /content {#configuring-an-internal-redirect-to-content}

Så här skapar du en mappning som prefixar en begäran till https://localhost:4503/ med `/content`:

1. Använda CRXDE navigera till `/etc/map/http`.

1. Skapa en nod:

   * **Typ** `sling:Mapping`
Den här nodtypen är avsedd för sådana mappningar, men det är inte obligatoriskt att använda den.

   * **Namn** `localhost_any`

1. Klicka **Spara alla**.
1. **Lägg till** följande egenskaper för den här noden:

   * **Namn** `sling:match`

      * **Typ** `String`

      * **Värde** `localhost.4503/`

   * **Namn** `sling:internalRedirect`

      * **Typ** `String[]`

      * **Värde** `/content/`

1. Klicka **Spara alla**.

Detta hanterar en begäran som:
`localhost:4503/geometrixx/en/products.html`
som if:
`localhost:4503/content/geometrixx/en/products.html`
hade blivit ombedd.

>[!NOTE]
>
>Se [Resurs](https://sling.apache.org/documentation/the-sling-engine/resources.html) I Sling Documentation finns mer information om vilka snedsättningsegenskaper som finns och hur de kan konfigureras.

>[!NOTE]
>
>Du kan använda `/etc/map.publish` för att lagra konfigurationerna för publiceringsmiljön. Dessa måste replikeras och den nya platsen ( `/etc/map.publish`) konfigurerad för **Mappningsplats** i [Resurslösare för Apache Sling](/help/sites-deploying/osgi-configuration-settings.md#apacheslingresourceresolver) av publiceringsmiljön.
