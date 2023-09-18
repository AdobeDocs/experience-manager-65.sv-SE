---
title: Sök i Grundläggande
description: Sök i communities
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 8af5ee58-19d7-47b6-b45d-e88006703a5d
source-git-commit: ab3d016c7c9c622be361596137b150d8719630bd
workflow-type: tm+mt
source-wordcount: '1170'
ht-degree: 0%

---

# Sök i Grundläggande {#search-essentials}

## Översikt {#overview}

Sökfunktionen är en viktig funktion i Adobe Experience Manager (AEM) Communities. Förutom [AEM](../../help/sites-deploying/queries-and-indexing.md) AEM Communities har [API för UGC-sökning](#ugc-search-api) för sökning av användargenererat innehåll (UGC). UGC har unika egenskaper eftersom de anges och lagras separat från andra AEM och användardata.

För Communities är de två saker som generellt söks igenom:

* Innehåll som publicerats av communitymedlemmar

   * Det använder AEM Communities UGC-söknings-API.

* Användare och användargrupper (användardata)

   * Det använder AEM sökfunktioner för plattformen.

Det här avsnittet av dokumentationen är av intresse för utvecklare som skapar anpassade komponenter som skapar eller hanterar UGC.

## Säkerhets- och skuggnoder {#security-and-shadow-nodes}

För en anpassad komponent måste du använda [Socialresursverktyg](socialutils.md#socialresourceutilities-package) metoder. Verktygsmetoderna som skapar och söker efter UGC skapar de obligatoriska [skuggnoder](srp.md#about-shadow-nodes-in-jcr) och se till att medlemmen har rätt behörigheter för begäran.

Det som inte hanteras via SRP-verktygen är egenskaper som är relaterade till moderering.

Se [SRP och UGC Essentials](srp-and-ugc.md) om du vill ha information om verktygsmetoder som används för att komma åt UGC- och ACL-skuggnoder.

## API för UGC-sökning {#ugc-search-api}

The [UGC-gemensam butik](working-with-srp.md) tillhandahålls av en av olika lagringsresursleverantörer (SRP), som båda kan ha olika inbyggda frågespråk. Därför bör anpassad kod, oavsett vald SRP, använda metoder från [API-paket för UGC](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/ugc/api/package-summary.html) (*com.adobe.cq.social.ugc.api*) som anropar det frågespråk som är lämpligt för den valda SRP.

### ASRP-sökningar {#asrp-searches}

För [ASRP](asrp.md), lagras UGC i molnet Adobe. UGC är inte synligt i CRX, [moderering](moderate-ugc.md) är tillgängligt både från författare och publiceringsmiljöer. Användning av [API för UGC-sökning](#ugc-search-api) fungerar för ASRP på samma sätt som för andra SRP.

Det finns inga verktyg för att hantera ASRP-sökningar.

När du skapar anpassade egenskaper som är sökbara måste du följa [namngivningskrav](#naming-of-custom-properties).

### MSRP-sökningar {#msrp-searches}

För [MSRP](msrp.md), lagras UGC i MongoDB som är konfigurerad att använda Solr för sökning. UGC visas inte i CRX, men [moderering](moderate-ugc.md) är tillgängligt både från författare och publiceringsmiljöer.

Om MSRP och Solr:

* Den inbäddade Solr-funktionen för den AEM plattformen används inte för MSRP.
* Om du använder en fjärransluten Solr för den AEM plattformen kan den delas med MSRP, men de bör använda olika samlingar.
* Solr kan konfigureras för standardsökning eller för flerspråkig sökning (MLS).
* Konfigurationsinformation finns i [Solr-konfiguration](msrp.md#solr-configuration) för MSRP.

Anpassade sökfunktioner bör använda [API för UGC-sökning](#ugc-search-api).

När du skapar anpassade egenskaper som är sökbara måste du följa [namngivningskrav](#naming-of-custom-properties).

### JSRP-sökningar {#jsrp-searches}

För [JSRP](jsrp.md), lagras UGC i [Oak](../../help/sites-deploying/platform.md) och är bara synligt i databasen för den AEM författaren eller publiceringsinstans som den angavs för.

Eftersom UGC vanligtvis används i publiceringsmiljön måste du konfigurera en [publiceringskluster](topologies.md), inte en publiceringsgrupp, så att det angivna innehållet visas för alla utgivare.

För JSRP visas aldrig UGC som anges i publiceringsmiljön i författarmiljön. Därför är alla [moderering](moderate-ugc.md) uppgifter utförs i publiceringsmiljön.

Anpassade sökfunktioner bör använda [API för UGC-sökning](#ugc-search-api).

#### Oak-indexering {#oak-indexing}

Oak-index skapas inte automatiskt för AEM plattformssökning, men från och med AEM 6.2 har de lagts till för AEM Communities för att förbättra prestanda och ge stöd för paginering när UGC-sökresultat presenteras.

Om anpassade egenskaper används och sökningarna är långsamma, måste ytterligare index skapas för de anpassade egenskaperna för att de ska bli bättre. Om du vill behålla bärbarheten följer du [namngivningskrav](#naming-of-custom-properties) när du skapar anpassade egenskaper som är sökbara.

Om du vill ändra befintliga index eller skapa egna index läser du [Fråga och indexering](../../help/sites-deploying/queries-and-indexing.md).

The [Oak Index Manager](https://adobe-consulting-services.github.io/acs-aem-commons/features/oak-index-manager.html) finns på ACS AEM Commons. Den innehåller följande:

* En vy över befintliga index.
* Möjlighet att initiera omindexering.

Så här visar du befintliga ekindexvärden i [CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md), platsen är:

* `/oak:index/socialLucene`

![social-lucene](assets/social-lucene.png)

## Egenskaper för indexerad sökning {#indexed-search-properties}

### Egenskaper för standardsökning {#default-search-properties}

Nedan följer några av de sökbara egenskaper som används för olika webbgruppsfunktioner:

| **Egenskap** | **Datatyp** |
|---|---|
| isFlagged | *Boolean* |
| isSpam | *Boolean* |
| read | *Boolean* |
| påverka | *Boolean* |
| bilagor | *Boolean* |
| känslouttryck | *Lång* |
| flaggad | *Boolean* |
| tillagd | *Datum* |
| modifiedDate | *Datum* |
| läge | *Sträng* |
| userIdentifier | *Sträng* |
| svar | *Lång* |
| jcr:title | *Sträng* |
| jcr:description | *Sträng* |
| sling:resourceType | *Sträng* |
| allowThreadedReply | *Boolean* |
| isDraft | *Boolean* |
| publishDate | *Datum* |
| publishJobId | *Sträng* |
| besvarat | *Boolean* |
| välj | *Boolean* |
| tag | *Sträng* |
| cq:Tagg | *Sträng* |
| author_display_name | *Sträng* |
| location_t | *Sträng* |
| parentPath | *Sträng* |
| parentTitle | *Sträng* |

### Namngivning av anpassade egenskaper {#naming-of-custom-properties}

När du lägger till anpassade egenskaper, så att dessa egenskaper visas för sorteringar och sökningar som skapas med [API för UGC-sökning](#ugc-search-api), det är *obligatoriskt* om du vill lägga till ett suffix till egenskapsnamnet.

Suffixet är för frågespråk som använder ett schema:

* Den identifierar egenskapen som sökbar.
* Den identifierar datatypen.

Solr är ett exempel på ett frågespråk som använder ett schema.

| **Suffix** | **Datatyp** |
|---|---|
| _b | *Boolean* |
| dt | *Kalender* |
| _d | *Dubbel* |
| _tl | *Lång* |
| _s | *Sträng* |
| _t | *Text* |

**Anteckningar:**

* *Text* är en tokeniserad sträng, *Sträng* inte. Använd *Text* för oskarpa (mer som detta) sökningar.

* För typer med flera värden lägger du till &#39;s&#39; i suffixet, till exempel:

   * `viewDate_dt`: egenskapen single date
   * `viewDates_dts`: list of dates property

## Filter {#filters}

Komponenter, som innehåller [kommentarsystem](essentials-comments.md), har stöd för filterparametern förutom slutpunkterna.

Filtersyntaxen för AND- och OR-logiken uttrycks enligt följande (visas innan den är URL-kodad):

* Ange eller använd en filterparam med kommaavgränsade värden:

   * `filter=name eq 'Jennifer',name eq 'Jen'`

* Så här anger och använder du flera filterparametrar:

   * `filter = name eq 'Jackson'&filter=message eq 'testing'`

Standardimplementeringen av [Sökkomponent](search.md) använder den här syntaxen så som den visas i URL:en som öppnar sidan Sökresultat i [Community Components Guide](components-guide.md). Om du vill experimentera går du till [http://localhost:4503/content/community-components/en/search.html](http://localhost:4503/content/community-components/en/search.html).

Filteroperatorer är:

| EQ | är lika med |
|---|---|
| NE | inte lika med |
| LT | mindre än |
| LTE | mindre än eller lika med |
| GE | större än |
| GTE | större än eller lika med |
| LIKE | luddig matchning |

Det är viktigt att URL:en refererar till komponenten Communities (resursen) och inte till sidan som komponenten är placerad på:

* Korrekt: forumkomponent
   * `/content/community-components/en/forum/jcr:content/content/forum.social.json`
* Felaktigt: forumsida
   * `/content/community-components/en/forum.social.json`

## SRP-verktyg {#srp-tools}

Det finns ett Adobe Experience Cloud GitHub-projekt som innehåller

[AEM Communities SRP Tools](https://github.com/Adobe-Marketing-Cloud/aem-communities-srp-tools)

Den här databasen innehåller verktyg för att hantera data i SRP.

För närvarande finns det en servlet som kan ta bort all UGC från alla SRP.

Om du till exempel vill ta bort all UGC i ASRP:

```shell
curl -X POST http://localhost:4502/services/social/srp/cleanup?path=/content/usergenerated/asi/cloud -uadmin:admin
```

## Felsökning {#troubleshooting}

### Solr-fråga {#solr-query}

Aktivera DEBUG-loggning för att felsöka problem med en Solr-fråga

`com.adobe.cq.social.srp.impl.SocialSolrConnector`.

Den verkliga Solr-frågan visas som URL-adress som är kodad i felsökningsloggen:

Frågan som ska löses är: `sort=timestamp+desc&bl=en&pl=en&start=0&rows=10 &q=%2Btitle_t:(hello)+%2Bprovider_id:\/content/usergenerated/asi/mongo/content/+%2Bresource_type_s:&df=provider_id&trf=verbatim&fq={!cost%3D100}report_suite:mongo`

Värdet för `q` -parametern är frågan. När URL-kodningen har avkodats kan frågan skickas till Solr Admin Query Tool för ytterligare felsökning.

## Relaterade resurser {#related-resources}

* [Community-innehåll](working-with-srp.md) - Diskuterar de tillgängliga SRP-alternativen för en gemensam UGC-butik.
* [Översikt över lagringsresursprovider](srp.md) - Översikt över introduktion och databasanvändning.
* [Åtkomst till UGC med SRP](accessing-ugc-with-srp.md) - Riktlinjer för kodning.
* [Omfaktorisering för SocialUtils](socialutils.md) - verktygsmetoder för SRP som ersätter SocialUtils.
* [Komponenter för sökning och sökresultat](search.md) - Lägga till UGC-sökfunktion i en mall.
