---
title: Översikt över lagringsresursprovider
description: Lär dig hur användargenererat innehåll (UGC) lagras i en enkel, gemensam lagringsplats från en leverantör av lagringsresurser.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 5f313274-1a2a-4e83-9289-60a4729b99b4
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '1135'
ht-degree: 0%

---

# Översikt över lagringsresursprovider {#storage-resource-provider-overview}

## Introduktion {#introduction}

Från och med Adobe Experience Manager (AEM) Communities 6.1 lagras communityinnehåll, som ofta kallas användargenererat innehåll (UGC), i en enda gemensam butik som tillhandahålls av en [lagringsresursleverantör](working-with-srp.md) (SRP).

Det finns flera SRP-alternativ, som alla har tillgång till UGC via ett nytt AEM Communities-gränssnitt, [SRP API](srp-and-ugc.md) (SocialResourceProvider API), som omfattar alla CRUD-åtgärder (create, read, update).

Alla SCF-komponenter implementeras med SRP API, vilket gör att kod kan utvecklas utan kunskap om den [underliggande topologin](topologies.md) eller platsen för UGC.

***API:t SocialResourceProvider är bara tillgängligt för licensierade kunder till AEM Communities.***

>[!NOTE]
>
>**Anpassade komponenter**: För licensierade kunder med AEM Communities är SRP API tillgängligt för utvecklare av anpassade komponenter för åtkomst till UGC, utan hänsyn till den underliggande topologin. Se [SRP och UGC Essentials](srp-and-ugc.md).

Se även:

* [SRP och UGC Essentials](srp-and-ugc.md) - SRP-verktygsmetoder och exempel.
* [Åtkomst till UGC med SRP](accessing-ugc-with-srp.md) - riktlinjer för kodning.
* [Omfaktorisering för SocialUtils](socialutils.md) - Mappar borttagna verktygsmetoder till aktuella SRP-verktygsmetoder.

## Om databasen {#about-the-repository}

För att förstå SRP är det bra att förstå hur AEM (Oak) fungerar på en AEM community-webbplats.

**Java™ Content Repository (JCR)**
Den här standarden definierar en datamodell och ett programprogrammeringsgränssnitt ([JCR API ](https://jackrabbit.apache.org/jcr/jcr-api.html)) för innehållsdatabaser. Det kombinerar egenskaper i vanliga filsystem med egenskaper i relationsdatabaser och lägger till flera funktioner som innehållsprogram ofta behöver.

En implementering av JCR är AEM, Oak.

**Apache Jackrabbit Oak**
[Oak](../../help/sites-deploying/platform.md) är en implementering av JCR 2.0 som är ett datalagringssystem som är utformat för innehållscentrerade program. Det är en typ av hierarkisk databas som är utformad för ostrukturerade eller halvstrukturerade data. I databasen lagras inte bara användarriktat innehåll utan även all kod, mallar och interna data som används av programmet. Gränssnittet för åtkomst av innehåll är [CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md).

Både JCR och Oak används vanligtvis för att referera till AEM.

När du har utvecklat webbplatsinnehåll i den privata redigeringsmiljön måste det kopieras till den offentliga publiceringsmiljön. Detta görs ofta genom en åtgärd som kallas *[replikering](deploy-communities.md#replication-agents-on-author)*. Detta sker under kontroll av författaren/utvecklaren/administratören.

För UGC anges innehållet av registrerade webbplatsbesökare (community-medlemmar) i den offentliga publiceringsmiljön. Detta sker slumpmässigt.

För hantering och rapportering är det praktiskt att ha tillgång till användargenererat innehåll från den privata redigeringsmiljön. Med SRP är åtkomst till UGC från författare mer konsekvent och prestandaförbättrande eftersom omvänd replikering från Publish till författare inte behövs.

## Om SRP {#about-srp}

När UGC sparas i delad lagring finns det en enda instans av medlemsinnehåll som i de flesta distributioner kan nås både från författaren och publiceringsmiljöer. Oavsett vad SRP väljer (MSRP, ASRP, JSRP) måste alla nås via programmering med SRP API.

>[!NOTE]
>
>Se [SRP och UGC Essentials](srp-and-ugc.md) för exempelkod och ytterligare information.
>
>Mer information om de effektivaste strategierna vid kodning finns i [Åtkomst till UGC med SRP](accessing-ugc-with-srp.md).

### ASRP {#asrp}

Om det finns ASRP lagras UGC inte i JCR, utan lagras i en molntjänst som hanteras av Adobe. UGC som lagras i ASRP kan inte visas med CRXDE Lite eller nås via JCR-API:t.

Se [ASRP - Adobe-lagringsresursprovider](asrp.md).

Det är inte möjligt för utvecklare att få tillgång till användargenererat innehåll direkt.

ASRP använder Adobe cloud för frågor.

### MSRP {#msrp}

Om det finns MSRP lagras inte UGC i JCR, utan lagras det i MongoDB. UGC som lagras i MSRP kan inte visas med CRXDE Lite eller nås via JCR-API:t.

Se [MSRP - MongoDB-lagringsresursprovider](msrp.md).

Även om MSRP är jämförbart med ASRP är det möjligt att använda vanliga verktyg för direktåtkomst till UGC som lagras i MongoDB eftersom alla AEM serverinstanser använder samma UGC.

MSRP använder Solr för frågor.

### JSRP {#jsrp}

JSRP är standardprovider för åtkomst till all UGC i en enda AEM. Med den kan du snabbt uppleva AEM Communities 6.1 utan att behöva konfigurera MSRP eller ASRP.

Se [JSRP - JCR-lagringsresursprovider](jsrp.md).

Om det finns JSRP när UGC lagras i JCR, och den är tillgänglig i API:t för CRXDE Lite och JCR, rekommenderar Adobe att du aldrig använder JCR API för att göra det. Om du gör det kan framtida ändringar påverka den anpassade koden.

Dessutom delas inte databasen för redigerings- och Publish-miljöerna. Även om ett kluster med publiceringsinstanser resulterar i en delad publiceringsdatabas är den UGC som anges på Publish inte synlig på författaren, vilket innebär att UGC inte kan hanteras från författaren. UGC sparas bara i den AEM databasen (JCR) för instansen som den angavs för.

JSRP använder Oak-index för frågor.

## Om skuggnoder i JCR {#about-shadow-nodes-in-jcr}

Skuggnoder, som påminner om sökvägen till UGC, finns i den lokala databasen för två syften:

1. [Åtkomstkontroll (ACL)](#for-access-control-acls)
1. [Icke-befintliga resurser](#for-non-existing-resources-ners)

Oavsett SRP-implementering är den faktiska UGC *inte* synlig på samma plats som skuggnoden.

### För åtkomstkontroll (ACL) {#for-access-control-acls}

Vissa SRP-implementeringar, som ASRP och MSRP, lagrar communityinnehåll i databaser som inte ger någon ACL-verifiering. Skuggnoder är en plats i den lokala databasen som ACL-listor kan användas på.

Med SRP API utför alla SRP-alternativ samma kontroll av skuggplatsen före alla CRUD-åtgärder.

ACL-kontrollen använder en verktygsmetod som returnerar en sökväg som är lämplig för att kontrollera de behörigheter som används för resursens UGC.

Se [SRP och UGC Essentials](srp-and-ugc.md) för exempelkod.

### För icke-befintliga resurser {#for-non-existing-resources-ners}

Vissa Communities-komponenter kan ingå i ett skript och kräver därför en Sling-adresserbar nod som stöder Communities-funktioner. [Inkluderade komponenter](scf.md#add-or-include-a-communities-component) kallas icke-befintliga resurser (NER).

Skuggnoder är en adresserbar plats för Sling i databasen.

>[!CAUTION]
>
>Eftersom skuggnoden har flera användningar innebär en skuggnod *inte* att komponenten är en NER.

### Lagringsplats {#storage-location}

Följande är ett exempel på en skuggnod som använder komponenten [Comments](http://localhost:4502/content/community-components/en/comments.html) i [Community Components Guide](components-guide.md):

* Komponenten finns i den lokala databasen på:

  `/content/community-components/en/comments/jcr:content/content/includable/comments`

* Motsvarande skuggnod finns i den lokala databasen på:

  `/content/usergenerated/content/community-components/en/comments/jcr:content/content/includable/comments`

Ingen UGC hittades under skuggnoden.

Standardbeteendet är att ställa in skuggnoder i en publiceringsinstans när det refereras till det relevanta underträdet för läsning eller skrivning.

Anta till exempel att distributionen är [MSRP](msrp.md) med en TargetMK-publiceringsgrupp.

När en [medlem](users.md) skickar UGC på pub1 (lagras i MongoDB) skapas skuggnoder i JCR på pub1.

Första gången som UGC läses på pub2, om inget är inställt, är standardbeteendet att skapa skuggnoderna.

Om du vill ha något annat än standardbeteendet måste det ställas in på författarinstansen och läggas fram för alla publiceringsinstanser, vilket vanligtvis är en manuell process.
