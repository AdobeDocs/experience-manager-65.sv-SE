---
title: Översikt över lagringsresursprovider
seo-title: Översikt över lagringsresursprovider
description: Gemensamt lagringsutrymme för Communities
seo-description: Gemensamt lagringsutrymme för Communities
uuid: abdf4e5a-767b-428f-9aa4-0dc06819a26e
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 63abeda4-6ea1-4b45-b188-f9c6b44ca0cd
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Översikt över lagringsresursprovider {#storage-resource-provider-overview}

## Introduktion {#introduction}

Från och med AEM Communities 6.1 lagras communityinnehåll, som ofta kallas användargenererat innehåll (UGC), i en enda gemensam butik som tillhandahålls av en [lagringsleverantör](working-with-srp.md) (SRP).

Det finns flera SRP-alternativ, som alla har tillgång till UGC via ett nytt AEM Communities-gränssnitt, [SRP API](srp-and-ugc.md) (SocialResourceProvider API), som omfattar alla CRUD-åtgärder (create, read, update).

Alla SCF-komponenter implementeras med SRP API, vilket gör att kod kan utvecklas utan kunskap om den [underliggande topologin](topologies.md) eller platsen för UGC.

***API:t för SocialResourceProvider är bara tillgängligt för licensierade kunder i AEM Communities.***

>[!NOTE]
>
>**Egna komponenter**: För licensierade kunder i AEM Communities är SRP API tillgängligt för utvecklare av anpassade komponenter i syfte att komma åt UGC utan hänsyn till den underliggande topologin. Se [SRP och UGC Essentials](srp-and-ugc.md).

Se även:

* [SRP och UGC Essentials](srp-and-ugc.md) - SRP-verktygsmetoder och -exempel
* [Åtkomst till UGC med SRP](accessing-ugc-with-srp.md) - riktlinjer för kodning
* [Omfaktorisering för SocialUtils](socialutils.md) - Mappar borttagna verktygsmetoder till aktuella SRP-verktygsmetoder

## Om databasen {#about-the-repository}

För att förstå SRP är det praktiskt att förstå vilken roll AEM-databasen (OAK) har på en AEM-communitywebbplats.

**Java Content Repository (JCR)** Den här standarden definierar en datamodell och ett[JCR-API](https://jackrabbit.apache.org/jcr/jcr-api.html)(Application Programming Interface) för innehållsdatabaser. Det kombinerar egenskaper i konventionella filsystem med egenskaper i relationsdatabaser och lägger till ett antal extrafunktioner som innehållsprogram ofta behöver.

En implementering av JCR är AEM-databasen, OAK.

**Apache Jackrabbit Oak (OAK)**[OAK](../../help/sites-deploying/platform.md) är en implementering av JCR 2.0 som är ett datalagringssystem som är särskilt utformat för innehållscentrerade program. Det är en typ av hierarkisk databas som är utformad för ostrukturerade eller halvstrukturerade data. I databasen lagras inte bara användarriktat innehåll utan även all kod, mallar och interna data som används av programmet. Gränssnittet för åtkomst av innehåll är [CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md).

Både JCR och OAK används vanligtvis för att hänvisa till AEM-databasen.

När webbplatsinnehållet har utvecklats i den privata författarmiljön måste det kopieras till den offentliga publiceringsmiljön. Detta sker ofta genom en åtgärd som kallas *[replikering](deploy-communities.md#replication-agents-on-author)*. Detta sker under kontroll av författaren/utvecklaren/administratören.

För UGC anges innehållet av registrerade webbplatsbesökare (community-medlemmar) i den offentliga publiceringsmiljön. Detta sker slumpmässigt.

För hantering och rapportering är det användbart att ha tillgång till UGC från den privata författarmiljön. Med SRP är åtkomst till UGC från författaren mer konsekvent och fungerar eftersom omvänd replikering från publicera till författare inte behövs.

## Om SRP {#about-srp}

När UGC sparas i delad lagring finns det en enda instans av medlemsinnehåll som i de flesta distributioner kan nås både från författaren och publiceringsmiljöer. Oavsett vad SRP väljer (MSRP, ASRP, JSRP) måste alla nås via programmering med SRP API.

>[!NOTE]
>
>Se [SRP och UGC Essentials](srp-and-ugc.md) för exempelkod och ytterligare information.
>
>Mer information om de effektivaste strategierna vid kodning finns i [Åtkomst av UGC med SRP](accessing-ugc-with-srp.md) .

### ASRP {#asrp}

För ASRP lagras UGC inte i JCR, utan lagras i en molntjänst som hanteras av Adobe. UGC som lagras i ASRP kan varken visas med CRXDE Lite eller kommas åt med JCR-API:t.

Se [ASRP - Adobe Storage Resource Provider](asrp.md).

Det är inte möjligt för utvecklare att komma åt användargenererat innehåll direkt.

ASRP använder Adobe cloud för frågor.

### MSRP {#msrp}

För MSRP lagras UGC inte i JCR, utan i MongoDB. UGC som lagras i MSRP kan varken visas med CRXDE Lite eller kommas åt med JCR-API:t.

Se [MSRP - MongoDB-lagringsresursprovider](msrp.md).

Även om MSRP är jämförbart med ASRP är det möjligt att använda vanliga verktyg för direktåtkomst till UGC som lagras i MongoDB eftersom alla AEM-serverinstanser använder samma UGC.

MSRP använder Solr för frågor.

### JSRP {#jsrp}

JSRP är standardprovider för åtkomst till all UGC i en enda AEM-instans. Det gör att du snabbt kan uppleva AEM Communities 6.1 utan att behöva konfigurera MSRP eller ASRP.

Se [JSRP - JCR-lagringsresursprovider](jsrp.md).

När det gäller JSRP rekommenderar vi starkt att JCR-API:t aldrig används, medan UGC lagras i JCR och är åtkomligt via både CRXDE Lite och JCR, annars kan framtida ändringar påverka den anpassade koden.

Dessutom delas inte databasen för författar- och publiceringsmiljöer. Även om ett kluster med publiceringsinstanser resulterar i en delad publiceringsdatabas, kommer den UGC som anges vid publicering inte att vara synlig för författaren, vilket innebär att det inte går att hantera UGC från författaren. UGC sparas bara i AEM-databasen (JCR) för den instans där den angavs.

JSRP använder Oak-index för frågor.

## Om skuggnoder i JCR {#about-shadow-nodes-in-jcr}

Skuggnoder, som påminner om sökvägen till UGC, finns i den lokala databasen för två syften:

1. [Åtkomstkontroll (ACL](#for-access-control-acls))
1. [Icke-befintliga resurser](#for-non-existing-resources-ners)

Oavsett SRP-implementering kommer den faktiska UGC:n att *inte vara synlig på samma plats som skuggnoden.

### För åtkomstkontroll (ACL) {#for-access-control-acls}

Vissa SRP-implementeringar, som ASRP och MSRP, lagrar communityinnehåll i databaser som inte ger någon ACL-verifiering. Skuggnoder är en plats i den lokala databasen som ACL-listor kan användas på.

Med SRP API utför alla SRP-alternativ samma kontroll av skuggplatsen före alla CRUD-åtgärder.

ACL-kontrollen använder en verktygsmetod som returnerar en sökväg som är lämplig för att kontrollera behörigheterna som tillämpas på resursens UGC.

Se [SRP och UGC Essentials](srp-and-ugc.md) för exempelkod.

### För icke-befintliga resurser {#for-non-existing-resources-ners}

Vissa communitykomponenter kan ingå i ett skript och kräver därför en Sling-adresserbar nod för att stödja Communities-funktioner. [Inkluderade komponenter](scf.md#add-or-include-a-communities-component) kallas icke-befintliga resurser.

Skuggnoder är en adresserbar plats för Sling i databasen.

>[!CAUTION]
>
>Eftersom skuggnoden har flera användningar innebär en skuggnod *inte* att komponenten är en NER.

### Lagringsplats {#storage-location}

Här följer ett exempel på en skuggnod där komponenten [](http://localhost:4502/content/community-components/en/comments.html) Comments i [Community Components Guide](components-guide.md)används:

* Komponenten finns i den lokala databasen på:

   /content/community-components/en/comments/jcr:content/content/includable/comments

* Motsvarande skuggnod finns i den lokala databasen på:

   /content/usergenerated/content/community-components/en/comments/jcr:content/indesign/comments

Ingen UGC hittas under skuggnoden.

Standardbeteendet är att ställa in skuggnoder i en publiceringsinstans när det refereras till det relevanta underträdet för läsning eller skrivning.

Anta till exempel att distributionen är [MSRP](msrp.md) med en TargetMK-publiceringsgrupp.

När en [medlem](users.md) skickar UGC på pub1 (lagras i MongoDB) skapas skuggnoder i JCR på pub1.

Första gången som UGC läses på pub2, om inget är inställt, är standardbeteendet att skapa skuggnoderna.

Om du vill ha något annat än standardbeteendet måste det ställas in på författarinstansen och läggas fram för alla publiceringsinstanser, vilket vanligtvis är en manuell process.
