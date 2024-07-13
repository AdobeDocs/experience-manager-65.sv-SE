---
title: Sök i Grundläggande
description: Läs om sökfunktionen som är en viktig funktion i AEM Communities. Communities innehåller också söknings-API:t för användargenererat innehåll.
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 8af5ee58-19d7-47b6-b45d-e88006703a5d
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '1158'
ht-degree: 0%

---

# Sök i Grundläggande {#search-essentials}

## Ökning {#overview}

Sökfunktionen är en viktig funktion i Adobe Experience Manager (AEM) Communities. Förutom funktionerna för [AEM plattformssökning](../../help/sites-deploying/queries-and-indexing.md) innehåller AEM Communities [UGC-söknings-API ](#ugc-search-api) för sökning efter användargenererat innehåll (UGC). UGC har unika egenskaper eftersom de anges och lagras separat från andra AEM och användardata.

För Communities är de två saker som generellt söks igenom:

* Innehåll som publicerats av communitymedlemmar

   * Det använder AEM Communities UGC-söknings-API.

* Användare och användargrupper (användardata)

   * Det använder AEM sökfunktioner för plattformen.

Det här avsnittet av dokumentationen är av intresse för utvecklare som skapar anpassade komponenter som skapar eller hanterar UGC.

## Säkerhets- och skuggnoder {#security-and-shadow-nodes}

För en anpassad komponent måste du använda metoderna [SocialResourceUtilities](socialutils.md#socialresourceutilities-package). Verktygsmetoderna som skapar och söker efter UGC skapar de [skuggnoder](srp.md#about-shadow-nodes-in-jcr) som krävs och ser till att medlemmen har rätt behörighet för begäran.

Det som inte hanteras via SRP-verktygen är egenskaper som är relaterade till moderering.

Se [SRP och UGC Essentials](srp-and-ugc.md) för information om verktygsmetoder som används för att komma åt UGC- och ACL-skuggnoder.

## API för UGC-sökning {#ugc-search-api}

[Den gemensamma lagringsplatsen ](working-with-srp.md) för UGC tillhandahålls av en av flera olika lagringsresursleverantörer (SRP), som båda kanske har olika inbyggda frågespråk. Därför bör anpassad kod, oavsett vald SRP, använda metoder från [UGC API-paketet](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/ugc/api/package-summary.html) (*com.adobe.cq.social.ugc.api*) som anropar det frågespråk som är lämpligt för vald SRP.

### ASRP-sökningar {#asrp-searches}

För [ASRP](asrp.md) lagras UGC i molnet Adobe. UGC är inte synligt i CRX, men [moderation](moderate-ugc.md) är tillgängligt både från författaren och Publish-miljöer. Användning av [UGC-söknings-API](#ugc-search-api) fungerar för ASRP på samma sätt som för andra SRP.

Det finns inga verktyg för att hantera ASRP-sökningar.

När du skapar anpassade egenskaper som är sökbara måste du följa [namnkraven](#naming-of-custom-properties).

### MSRP-sökningar {#msrp-searches}

För [MSRP](msrp.md) lagras UGC i MongoDB som konfigurerats att använda Solr för sökning. UGC är inte synligt i CRX, men [moderation](moderate-ugc.md) är tillgängligt både från författaren och Publish-miljöer.

Om MSRP och Solr:

* Den inbäddade Solr-funktionen för den AEM plattformen används inte för MSRP.
* Om du använder en fjärransluten Solr för den AEM plattformen kan den delas med MSRP, men de bör använda olika samlingar.
* Solr kan konfigureras för standardsökning eller för flerspråkig sökning (MLS).
* Konfigurationsinformation finns i [Solr Configuration](msrp.md#solr-configuration) för MSRP.

Anpassade sökfunktioner bör använda [UGC-söknings-API](#ugc-search-api).

När du skapar anpassade egenskaper som är sökbara måste du följa [namnkraven](#naming-of-custom-properties).

### JSRP-sökningar {#jsrp-searches}

För [JSRP](jsrp.md) lagras UGC i [Oak](../../help/sites-deploying/platform.md) och visas bara i databasen för den AEM författaren eller Publish-instans som den angavs för.

Eftersom UGC vanligtvis används i Publish-miljön måste du konfigurera ett [publiceringskluster](topologies.md), inte en publiceringsgrupp, för produktionssystem med flera utgivare, så att det angivna innehållet visas för alla utgivare.

För JSRP visas aldrig UGC som anges i Publish-miljön i författarmiljön. Därför utförs alla [modereringsuppgifter](moderate-ugc.md) i Publish-miljön.

Anpassade sökfunktioner bör använda [UGC-söknings-API](#ugc-search-api).

#### Oak Indexing {#oak-indexing}

Oak-index skapas inte automatiskt för AEM plattformssökning, men från och med AEM 6.2 har de lagts till för AEM Communities för att förbättra prestanda och ge stöd för sidnumrering när UGC-sökresultat presenteras.

Om anpassade egenskaper används och sökningarna är långsamma, måste ytterligare index skapas för de anpassade egenskaperna för att de ska bli bättre. Om du vill behålla portabilitet ska du följa [namnkraven](#naming-of-custom-properties) när du skapar anpassade egenskaper som är sökbara.

Mer information om hur du ändrar befintliga index eller skapar anpassade index finns i [Oak-frågor och indexering](../../help/sites-deploying/queries-and-indexing.md).

[Oak Index Manager](https://adobe-consulting-services.github.io/acs-aem-commons/features/oak-index-manager.html) är tillgängligt från ACS AEM Commons. Den innehåller följande:

* En vy över befintliga index.
* Möjlighet att initiera omindexering.

Om du vill visa de befintliga Oak-indexen i [CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md) är platsen:

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

När du lägger till anpassade egenskaper, för att dessa egenskaper ska vara synliga för sortering och sökningar som skapats med [UGC-söknings-API](#ugc-search-api), är det *obligatoriskt* att lägga till ett suffix till egenskapsnamnet.

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

* *Texten* är en tokeniserad sträng, men *String* är inte det. Använd *Text* för oskarpa (mer som detta) sökningar.

* För typer med flera värden lägger du till &#39;s&#39; i suffixet, till exempel:

   * `viewDate_dt`: egenskapen för enstaka datum
   * `viewDates_dts`: lista med datumegenskaper

## Filter {#filters}

Komponenter, som innehåller [kommentarsystemet](essentials-comments.md), stöder filterparametern förutom slutpunkterna.

Filtersyntaxen för AND- och OR-logiken uttrycks enligt följande (visas innan den är URL-kodad):

* Ange eller använd en filterparam med kommaavgränsade värden:

   * `filter=name eq 'Jennifer',name eq 'Jen'`

* Så här anger och använder du flera filterparametrar:

   * `filter = name eq 'Jackson'&filter=message eq 'testing'`

Standardimplementeringen av [sökkomponenten](search.md) använder den här syntaxen, vilket visas i den URL som öppnar sökresultatsidan i [guiden för communitykomponenter](components-guide.md). Om du vill experimentera går du till [http://localhost:4503/content/community-components/en/search.html](http://localhost:4503/content/community-components/en/search.html).

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

[AEM Communities SRP-verktyg](https://github.com/Adobe-Marketing-Cloud/aem-communities-srp-tools)

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

Frågan som ska besvaras är: `sort=timestamp+desc&bl=en&pl=en&start=0&rows=10 &q=%2Btitle_t:(hello)+%2Bprovider_id:\/content/usergenerated/asi/mongo/content/+%2Bresource_type_s:&df=provider_id&trf=verbatim&fq={!cost%3D100}report_suite:mongo`

Värdet för parametern `q` är frågan. När URL-kodningen har avkodats kan frågan skickas till Solr Admin Query Tool för ytterligare felsökning.

## Relaterade resurser {#related-resources}

* [Community Content Storage](working-with-srp.md) - Diskuterar tillgängliga SRP-alternativ för en gemensam UGC-butik.
* [Lagringsresursprovideröversikt](srp.md) - Översikt över introduktion och databasanvändning.
* [Åtkomst till UGC med SRP](accessing-ugc-with-srp.md) - riktlinjer för kodning.
* [Omfaktorisering för SocialUtils](socialutils.md) - Verktygsmetoder för SRP som ersätter SocialUtils.
* [Komponenter för sök- och sökresultat](search.md) - Lägger till UGC-sökfunktion i en mall.
