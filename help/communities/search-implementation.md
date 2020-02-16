---
title: Sök i Grundläggande
seo-title: Sök i Grundläggande
description: Sök i communities
seo-description: Sök i communities
uuid: 5f35a033-2069-499e-9cdb-db25781312f0
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 300aa9f3-596f-42bc-8d46-e535f2bc4379
translation-type: tm+mt
source-git-commit: 5128a08d4db21cda821de0698b0ac63ceed24379

---


# Sök i Grundläggande {#search-essentials}

## Översikt {#overview}

Sökfunktionen är en viktig funktion i AEM Communities. Förutom sökfunktionerna för [AEM-plattformen](../../help/sites-deploying/queries-and-indexing.md) erbjuder AEM Communities [UGC-söknings-API](#ugc-search-api) för sökning efter användargenererat innehåll (UGC). UGC har unika egenskaper eftersom de anges och lagras separat från annat AEM-innehåll och andra användardata.

För Communities är de två saker som generellt söks igenom:

* Innehåll som publicerats av communitymedlemmar

   * Använder API:t för UGC-sökning i AEM Communities

* Användare och användargrupper (användardata)

   * Använder sökfunktionerna i AEM-plattformen

Det här avsnittet av dokumentationen är av intresse för utvecklare som skapar anpassade komponenter som skapar eller hanterar UGC.

## Säkerhets- och skuggnoder {#security-and-shadow-nodes}

För en anpassad komponent måste du använda [SocialResourceUtilities](socialutils.md#socialresourceutilities-package) -metoderna. Verktygsmetoderna som skapar och söker efter UGC skapar de [skuggnoder](srp.md#about-shadow-nodes-in-jcr) som krävs och ser till att medlemmen har rätt behörigheter för begäran.

Det som inte hanteras via SRP-verktygen är egenskaper som är relaterade till moderering.

Se [SRP och UGC Essentials](srp-and-ugc.md) för information om verktygsmetoder som används för att komma åt UGC- och ACL-skuggnoder.

## API för UGC-sökning {#ugc-search-api}

Den gemensamma lagringsplatsen [för](working-with-srp.md) UGC tillhandahålls av en av flera olika lagringsresursleverantörer (SRP), som båda kan ha olika inbyggda frågespråk. Därför bör anpassad kod, oavsett vald SRP, använda metoder från [UGC API-paketet](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/ugc/api/package-summary.html) (*com.adobe.cq.social.ugc.api*) som anropar det frågespråk som är lämpligt för vald SRP.

### ASRP-sökningar {#asrp-searches}

För [ASRP](asrp.md)lagras UGC i Adobe-molnet. UGC är inte synligt i CRX, men [moderering](moderate-ugc.md) är tillgängligt både från författaren och publiceringsmiljön. Användning av [UGC-söknings-API](#ugc-search-api) fungerar på samma sätt för ASRP som för andra SRP.

Det finns för närvarande inga verktyg för att hantera ASRP-sökningar.

När du skapar anpassade egenskaper som är sökbara måste du följa [namngivningskraven](#naming-of-custom-properties).

### MSRP-sökningar {#msrp-searches}

För [MSRP](msrp.md)lagras UGC i MongoDB som konfigurerats att använda Solr för sökning. UGC visas inte i CRX, men [moderering](moderate-ugc.md) är tillgängligt både från författar- och publiceringsmiljöer.

Om MSRP och Solr:

* Den inbäddade Solr-funktionen för AEM-plattformen används inte för MSRP
* Om du använder en fjärransluten Solr för AEM-plattformen kan den delas med MSRP, men de bör använda olika samlingar
* Solr kan konfigureras för standardsökning eller för flerspråkig sökning (MLS)
* Konfigurationsinformation finns i [Solr Configuration](msrp.md#solr-configuration) for MSRP

Anpassade sökfunktioner bör använda [UGC-söknings-API](#ugc-search-api).

När du skapar anpassade egenskaper som är sökbara måste du följa [namngivningskraven](#naming-of-custom-properties).

### JSRP-sökningar {#jsrp-searches}

För [JSRP](jsrp.md)lagras UGC i [Oak](../../help/sites-deploying/platform.md) och visas bara i databasen för den AEM-författare eller publiceringsinstans som den angavs för.

Eftersom UGC vanligtvis används i publiceringsmiljön måste du konfigurera ett [publiceringskluster](topologies.md), inte en publiceringsgrupp, för produktionssystem med flera utgivare, så att det angivna innehållet visas för alla utgivare.

För JSRP visas aldrig UGC som anges i publiceringsmiljön i författarmiljön. Alla [modereringsuppgifter](moderate-ugc.md) äger alltså rum i publiceringsmiljön.

Anpassade sökfunktioner bör använda [UGC-söknings-API](#ugc-search-api).

#### Oak-indexering {#oak-indexing}

Oak-index skapas inte automatiskt för AEM-plattformssökning, men från och med AEM 6.2 har de lagts till för AEM Communities för att förbättra prestanda och ge stöd för paginering när UGC-sökresultat presenteras.

Om anpassade egenskaper används och sökningarna är långsamma, måste ytterligare index skapas för de anpassade egenskaperna för att de ska bli bättre. Om du vill behålla bärbarheten följer du [namngivningskraven](#naming-of-custom-properties) när du skapar anpassade egenskaper som är sökbara.

Mer information om hur du ändrar befintliga index eller skapar anpassade index finns i [Oak Queries och Indexing](../../help/sites-deploying/queries-and-indexing.md).

Oak Index Manager [är](https://adobe-consulting-services.github.io/acs-aem-commons/features/oak-index-manager.html) tillgängligt från ACS AEM Commons. Den innehåller följande:

* En vy över befintliga index
* Möjlighet att initiera omindexering

Om du vill visa de befintliga ekindexen i [CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md)är platsen:

* `/oak:index/socialLucene`

![chlimage_1-235](assets/chlimage_1-235.png)

## Egenskaper för indexerad sökning {#indexed-search-properties}

### Egenskaper för standardsökning {#default-search-properties}

Nedan följer några av de sökbara egenskaper som används för olika webbgruppsfunktioner:

| **Egenskap** | **Datatyp** |
|---|---|
| isFlagged | *Boolesk* |
| isSpam | *Boolesk* |
| read | *Boolesk* |
| påverka | *Boolesk* |
| bilagor | *Boolesk* |
| känslouttryck | *Lång* |
| flaggad | *Boolesk* |
| tillagd | *Date* |
| modifiedDate | *Date* |
| läge | *Sträng* |
| userIdentifier | *Sträng* |
| svar | *Lång* |
| jcr:title | *Sträng* |
| jcr:description | *Sträng* |
| sling:resourceType | *Sträng* |
| allowThreadedReply | *Boolesk* |
| isDraft | *Boolesk* |
| publishDate | *Date* |
| publishJobId | *Sträng* |
| besvarade | *Boolesk* |
| välj | *Boolesk* |
| tag | *Sträng* |
| cq:Tagg | *Sträng* |
| author_display_name | *Sträng* |
| location_t | *Sträng* |
| parentPath | *Sträng* |
| parentTitle | *Sträng* |

### Namngivning av anpassade egenskaper {#naming-of-custom-properties}

När du lägger till anpassade egenskaper krävs *för att lägga till ett suffix till egenskapsnamnet för att dessa egenskaper ska vara synliga för sortering och sökningar som skapats med [UGC-söknings-API](#ugc-search-api).

Suffixet är för frågespråk som använder ett schema:

* Den identifierar egenskapen som sökbar
* Den identifierar datatypen

Solr är ett exempel på ett frågespråk som använder ett schema.

| **Suffix** | **Datatyp** |
|---|---|
| _b | *Boolesk* |
| dt | *Kalender* |
| _d | *Dubbel* |
| _tl | *Lång* |
| _s | *Sträng* |
| _t | *Text* |

**Anteckningar:**

* *Texten* är en tokeniserad sträng, *String* är inte det. Använd *text* för oskarpa sökningar (ungefär så här).

* För typer med flera värden lägger du till&quot;s&quot; i suffixet, till exempel:

   * `viewDate_dt`: single date, egenskap
   * `viewDates_dts`: list of dates, egenskap

## Filter {#filters}

Komponenter som innehåller [kommentarsystemet](essentials-comments.md) har stöd för filterparametern förutom slutpunkterna.

Filtersyntaxen för AND- och OR-logiken uttrycks enligt följande (visas innan den är URL-kodad):

* Ange eller använd en filterparam med kommaseparerade värden:

   * `filter=name eq 'Jennifer',name eq 'Jen'`

* Så här anger och använder du flera filterparametrar:

   * `filter = name eq 'Jackson'&filter=message eq 'testing'`

Standardimplementeringen av [sökkomponenten](search.md) använder den här syntaxen, vilket visas i den URL som öppnar sökresultatsidan i guiden [för](components-guide.md)communitykomponenter. Om du vill experimentera går du till [http://localhost:4503/content/community-components/en/search.html](http://localhost:4503/content/community-components/en/search.html).

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

Det finns ett Adobe Marketing Cloud GitHub-projekt som innehåller:

[AEM Communities SRP Tools](https://github.com/Adobe-Marketing-Cloud/aem-communities-srp-tools)

Den här databasen innehåller verktyg för att hantera data i SRP.

För närvarande finns det en serverenhet som kan ta bort all UGC från alla SRP.

Om du till exempel vill ta bort all UGC i ASRP:

```shell
curl -X POST http://localhost:4502/services/social/srp/cleanup?path=/content/usergenerated/asi/cloud -uadmin:admin
```

## Felsökning {#troubleshooting}

### Solr-fråga {#solr-query}

Aktivera DEBUG-loggning för att felsöka problem med en Solr-fråga

`com.adobe.cq.social.srp.impl.SocialSolrConnector`.

Den verkliga Solr-frågan visas URL-adress som är kodad i felsökningsloggen:

Frågan som ska tolkas är: `sort=timestamp+desc&bl=en&pl=en&start=0&rows=10 &q=%2Btitle_t:(hello)+%2Bprovider_id:\/content/usergenerated/asi/mongo/content/+%2Bresource_type_s:&df=provider_id&trf=verbatim&fq={!cost%3D100}report_suite:mongo`

Värdet för `q` parametern är frågan. När URL-kodningen har avkodats kan frågan skickas till Solr Admin Query Tool för ytterligare felsökning.

## Relaterade resurser {#related-resources}

* [Community Content Storage](working-with-srp.md) - Diskutera tillgängliga SRP-alternativ för en gemensam UGC-butik
* [Översikt över](srp.md) lagringsresursleverantör - introduktion och databasanvändning - översikt
* [Åtkomst till UGC med SRP](accessing-ugc-with-srp.md) - riktlinjer för kodning
* [Omfaktorisering](socialutils.md) för SocialUtils - verktygsmetoder för SRP som ersätter SocialUtils
* [Komponenter](search.md) för sökning och sökresultat - lägga till UGC-sökfunktion i en mall

