---
title: SRP - Community Content Storage
seo-title: SRP - Community Content Storage
description: Från och med AEM Communities 6.1 lagras användargenererat innehåll (UGC) i en enda gemensam butik som tillhandahålls av en leverantör av lagringsresurser (SRP)
seo-description: Från och med AEM Communities 6.1 lagras användargenererat innehåll (UGC) i en enda gemensam butik som tillhandahålls av en leverantör av lagringsresurser (SRP)
uuid: d45e03c4-378b-4510-a6a0-d48c8cb879d9
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 6f13b21a-f4ef-4889-9b8e-4da3f846fa35
docset: aem65
role: Admin
exl-id: e29aae44-67be-43d2-8004-c986412d9e63
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '921'
ht-degree: 0%

---

# SRP - Community Content Storage {#srp-community-content-storage}

## Introduktion {#introduction}

Från och med AEM Communities 6.1 lagras användargenererat innehåll (UGC) i en enda gemensam butik som tillhandahålls av en leverantör av lagringsresurser (SRP). Det finns flera SRP-alternativ att välja mellan, till exempel ASRP, MSRP och JSRP.

Till skillnad från tidigare versioner finns det ingen omvänd/framåtriktad replikering av UGC över AEM instanser. I stället gör SRP att UGC är direkt tillgängligt för att skapa, läsa, uppdatera och ta bort (CRUD) åtgärder från alla författare- och publiceringsinstanser, med undantag för JSRP.

Nedan följer [egenskaperna för varje SRP-alternativ](#characteristics-of-srp-options), som är viktig information för beslutsprocessen när du väljer lämplig SRP och [underliggande distribution](/help/communities/topologies.md).

Mer information om användning av SRP för UGC finns i [Översikt över lagringsresursprovidern](/help/communities/srp.md).

>[!NOTE]
>
>SRP gäller endast för communityinnehåll. Det påverkar inte var webbplatsinnehållet lagras ([nodstore](/help/sites-deploying/data-store-config.md)) och påverkar inte den säkra hanteringen av användarregistrering, användarprofiler och användargrupper mellan AEM instanser (se även [Hantera användardata](#managing-user-data)).

>[!CAUTION]
>
>Från och med AEM 6.1 är [UGC aldrig replikerat](#ugc-never-replicated).
>
>När distributionen inte innehåller någon gemensam lagringsplats, till exempel standardtopologin [JSRP](/help/communities/topologies.md#jsrp), visas bara UGC i den AEM publicerings- eller författarinstansen som den angavs för. Endast om topologin innehåller ett publiceringskluster visas UGC:n på alla publiceringsinstanser.

## Egenskaper för SRP-alternativ {#characteristics-of-srp-options}

[ASRP - Adobe lagringsresursleverantör](/help/communities/asrp.md)

Med det här alternativet lagras användargenererat innehåll på fjärrbasis i en molntjänst som hanteras av Adobe. Det krävs ytterligare en licens och att man samarbetar med en kontorepresentant för att tillhandahålla kontot för den specifika licensen. ASRP kräver:

* En tillhörande molntjänst som tillhandahålls och stöds av Adobe för att lagra communityinnehåll.
* Val av datacenter i en specifik geografi (USA, EMEA, APAC).

* All programmatisk åtkomst till UGC sker via SRP API.

ASRP är lämpligt:

* För TjärMK-publiceringsservergruppen.
* När det inte finns någon avsikt att investera i lokal lagring.

>[!NOTE]
>
>Det finns en gräns för att överföra bilagor till inlägg (eller kommentarer) i ASRP, som är 50 MB.

[MSRP - lagringsresursprovider för MongoDB](/help/communities/msrp.md)

Med det här alternativet sparas UGC direkt i en lokal MongoDB-instans.

MSRP kräver:

* En lokal, licensierad installation av MongoDB för lagring av communityinnehåll.
* En lokal installation av Apache Solr.
* All programmatisk åtkomst till UGC sker via SRP API.

ASRP är lämpligt:

* För en befintlig TjärMK-publiceringsgrupp.
* För ett MongoMK- eller RdbMK-kluster.
* När stora volymer av communityinnehåll förväntas.

[DSRP - Resursprovider för relativ databaslagring](/help/communities/dsrp.md)

Med det här alternativet sparas UGC direkt i en lokal MySQL-databasinstans.

DSRP kräver:

* En lokal installation av MySQL för att lagra communityinnehåll.
* En lokal installation av Apache Solr.
* All programmatisk åtkomst till UGC sker via SRP API.

DSRP är lämpligt:

* För en befintlig TjärMK-publiceringsgrupp.
* För ett MongoMK- eller RdbMK-kluster.
* När stora volymer av communityinnehåll förväntas.

[JSRP - JCR-lagringsresursprovider](/help/communities/jsrp.md)

Det finns ingen gemensam lagringsplats med standardalternativet. UGC:n sparas bara i samma JCR-databas som den AEM där den angavs.

JSRP:

* Lagrar communityinnehåll i JCR-databasen för AEM författare eller publiceringsinstans som det publicerades i.
* Kräver all programmatisk åtkomst till UGC via SRP API.
* Kräver ett publiceringskluster om mer än en publiceringsinstans har distribuerats (det finns ingen replikeringsmekanism bland publiceringsinstanser i en tarMK-servergrupp).
* moderering utförs endast i publiceringsmiljön (det finns ingen omvänd/framåtriktad replikeringsmekanism mellan författaren och publiceringen).
* Passar bäst för utveckling, demonstrationer och utbildning.

## Konfigurerar SRP {#configuring-srp}

Ange standardlagringsalternativet, baserat på den underliggande distributionen, via konsolen [Lagringskonfiguration](/help/communities/srp-config.md).

Konfigurationsinformation om varje alternativ finns i:

* [ASRP - Adobe lagringsresursleverantör](/help/communities/asrp.md)
* [MSRP - lagringsresursprovider för MongoDB](/help/communities/msrp.md)
* [DSRP - Resursprovider för relativ databaslagring](/help/communities/dsrp.md)
* [JSRP - JCR-lagringsresursprovider](/help/communities/jsrp.md)

Om inget lagringsalternativ är aktivt, aktiveras JSRP som standard.

## Ytterligare information {#additional-information}

### UGC har aldrig replikerats {#ugc-never-replicated}

I redigeringsmiljön skapar en författare sidinnehåll och replikerar det till publiceringsmiljön. När en sida innehåller en interaktiv AEM Communities-funktion, till exempel kommentarer, granskningar, forum, blogg eller QnA, resulterar interaktionen mellan medlemmar (inloggade besökare) på en publiceringsinstans i användargenererat innehåll (UGC) som läggs in i publiceringsmiljön.

Tidigare replikerades det här communityinnehållet bakåt till författarinstanser och från författare replikerat till publiceringsinstanser. Det var svårt att bibehålla enhetligheten mellan AEM instanser med omvänd och framåtriktad replikering.

Från och med AEM Communities 6.1 har behovet av UGC-replikering eliminerats genom delad lagring för UGC, vilket beskrivs ovan.

När platsinnehållet replikeras replikeras aldrig UGC.

### Hantera användardata {#managing-user-data}

CommunitIes är [*användare*, *användargrupper* och *användarprofiler*](/help/communities/users.md). Dessa användarrelaterade data, som skapas och uppdateras i publiceringsmiljön, måste göras tillgängliga för andra publiceringsinstanser när topologin är en [publiceringsgrupp](/help/sites-deploying/recommended-deploys.md#tarmk-farm).

Från och med AEM Communities 6.1 synkroniseras användarrelaterade data med Sling-distribution i stället för replikering. Mer information finns på [Användarsynkronisering](/help/communities/sync.md).

### Uppgradera till AEM Communities 6.5 {#upgrading-to-aem-communities}

Vid uppgradering till AEM 6.5 Communities, om befintlig UGC måste behållas, bör åtgärder vidtas beroende på om AEM 5.6.1- eller AEM 6.0-communityn använde Adobe on demand-lagring eller lokal lagring av UGC.

Mer information finns på [Uppgradera till AEM Communities 6.5](/help/communities/upgrade.md).
