---
title: Redigering
description: Begrepp som redigering och publicering i Adobe Experience Manager 6.5.
exl-id: dcda537a-1bb2-4ce3-9904-40d158b47556
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User,Admin,Developer
source-git-commit: c77849740fab51377ce60aff5f611e0408dca728
workflow-type: tm+mt
source-wordcount: '547'
ht-degree: 0%

---

# Redigering{#authoring}

## Begreppet redigering (och publicering) {#concept-of-authoring-and-publishing}

AEM har två miljöer:

* Författare
* Publicera

Dessa interagerar så att ni kan göra innehåll tillgängligt på er webbplats så att besökarna kan läsa det.

I redigeringsmiljön finns mekanismer för att skapa, uppdatera och granska innehållet innan det publiceras:

* En författare skapar och granskar innehållet (detta kan vara av flera typer, t.ex. sidor, resurser, publikationer osv.)
* som någon gång kommer att publiceras på er webbplats.

![Översikt över miljöer](assets/chlimage_1-132.png)

I författarmiljön görs AEM-funktionerna tillgängliga via två användargränssnitt. I publiceringsmiljön utformar du hela det gränssnitt som är tillgängligt för användarna.

### Författarmiljö {#author-environment}

Författaren arbetar i det som kallas **författarmiljön**. Detta ger ett användarvänligt gränssnitt (grafiskt användargränssnitt (GUI eller UI)) för att skapa innehållet. Det finns bakom ett företags brandvägg som ger fullständigt skydd och som kräver att författaren loggar in med ett konto som tilldelats rätt åtkomstbehörighet.

>[!NOTE]
>
>Ditt konto behöver rätt behörighet för att skapa, redigera och publicera innehåll.

Beroende på hur din instans och dina personliga åtkomsträttigheter är konfigurerade kan du utföra många åtgärder på ditt innehåll, bland annat:

* generera nytt innehåll eller redigera befintligt innehåll på en sida
* använda fördefinierade mallar för att skapa nya innehållssidor
* skapa, redigera och hantera dina resurser och samlingar
* skapa, redigera och hantera publikationer
* utveckla era kampanjer och relaterade resurser
* utveckla och hantera communitywebbplatser
* flytta, kopiera eller ta bort innehållssidor, resurser och så vidare
* publicera (eller avpublicera) sidor, resurser osv.

Det finns även administrativa uppgifter som hjälper dig att hantera ditt innehåll:

* arbetsflöden som styr hur ändringar hanteras, t.ex. genomdriva en granskning före publicering
* projekt som koordinerar enskilda uppgifter

>[!NOTE]
>
>AEM [administreras](/help/sites-administering/home.md) (för de flesta uppgifter) från författarmiljön.

#### Publiceringsmiljö {#publish-environment}

När det är klart publiceras AEM-webbplatsens innehåll i **publiceringsmiljön**. Här blir webbplatsens sidor tillgängliga för den avsedda publiken i enlighet med det gränssnitt som har utformats.

Normalt ligger publiceringsmiljön innanför den demilitariserade zonen, dvs. är tillgänglig via Internet, men inte längre under det interna nätverkets fulla skydd.

När AEM webbplats är en [communitywebbplats](/help/communities/overview.md), eller innehåller [communitykomponenter](/help/communities/author-communities.md), kan besökare på den inloggade webbplatsen (medlemmar) interagera med communityfunktioner. De kan till exempel publicera på ett forum, publicera en kommentar eller följa andra medlemmar. Medlemmar kan beviljas tillstånd att utföra aktiviteter som normalt bara är begränsade till författarmiljön, t.ex. skapa nya sidor (communitygrupper), bloggartiklar och moderata inlägg från andra medlemmar.

>[!NOTE]
>
>Tyvärr förekommer ibland en överlappning i den terminologi som används. Detta kan inträffa med:
>
>* **Publicera/avpublicera**
>  Detta är de primära villkoren för de åtgärder som gör innehållet tillgängligt för allmänheten i publiceringsmiljön (eller inte).
>
>* **Aktivera/inaktivera**
>  Dessa termer är synonyma med publicera/avpublicera.
>
>* **Replikera/replikera**
>  Detta är de tekniska termer som används för att ange dataförflyttning (till exempel sidinnehåll, filer, kod, användarkommentarer) från en miljö till en annan, det vill säga vid publicering eller omvänd replikering av användarkommentarer.
>

#### Dispatcher {#dispatcher}

**[Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=sv-SE)** implementerar belastningsutjämning och cachning för att optimera prestanda för besökare på din webbplats.
