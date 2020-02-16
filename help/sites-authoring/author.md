---
title: Redigering
seo-title: Redigering
description: Begrepp att skapa i AEM
seo-description: Begrepp att skapa i AEM
uuid: eaa5f613-a138-4215-8f84-dfc962fe7fa7
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: 81ff6f6f-11b3-4f8e-80e6-b3e104158394
docset: aem65
translation-type: tm+mt
source-git-commit: 44eb94b917fe88b7c90c29ec7da553e15be391db

---


# Redigering{#authoring}

## Begreppet redigering (och publicering) {#concept-of-authoring-and-publishing}

AEM ger dig två miljöer:

* Författare
* Publicera

Dessa interagerar så att ni kan göra innehåll tillgängligt på er webbplats så att besökarna kan läsa det.

I redigeringsmiljön finns mekanismer för att skapa, uppdatera och granska innehållet innan det publiceras:

* En författare skapar och granskar innehållet (detta kan vara av flera typer); till exempel sidor, resurser, publikationer osv.)
* som någon gång kommer att publiceras på er webbplats.

![chlimage_1-132](assets/chlimage_1-132.png)

I redigeringsmiljön är AEM-funktionaliteten tillgänglig via två användargränssnitt. För publiceringsmiljön utformar du hela det gränssnitt som är tillgängligt för användarna.

>[!NOTE]
>
>AEM används för att skapa AEM-dokumentationen.
>
>Tillsammans med Dispatcher används den också för publicering.

### Författarmiljö {#author-environment}

Författaren arbetar i det som kallas **författarmiljö**. Detta ger ett användarvänligt gränssnitt (grafiskt användargränssnitt (GUI eller UI)) för att skapa innehållet. Det ligger vanligtvis bakom ett företags brandvägg som ger fullständigt skydd och som kräver att författaren loggar in med ett konto som tilldelats rätt åtkomstbehörighet.

>[!NOTE]
>
>Ditt konto behöver rätt behörighet för att skapa, redigera eller publicera innehåll.

Beroende på hur din instans och dina personliga åtkomsträttigheter är konfigurerade kan du utföra många åtgärder på ditt innehåll, bland annat:

* generera nytt innehåll, eller redigera befintligt innehåll, på en sida
* använda fördefinierade mallar för att skapa nya innehållssidor
* skapa, redigera och hantera dina resurser och samlingar
* skapa, redigera och hantera publikationer
* utveckla era kampanjer och relaterade resurser
* utveckla och hantera communitysajter
* flytta, kopiera eller ta bort innehållssidor, resurser osv.
* publicera (eller avpublicera) sidor, resurser osv

Det finns dessutom administrativa uppgifter som hjälper dig att hantera ditt innehåll:

* arbetsflöden som styr hur ändringar hanteras, till exempel. genomföra en granskning före publicering
* projekt som koordinerar enskilda uppgifter

>[!NOTE]
>
>AEM [administreras](/help/sites-administering/home.md) också (för de flesta uppgifter) från författarmiljön.

#### Publiceringsmiljö {#publish-environment}

När det är klart publiceras AEM-webbplatsens innehåll i **publiceringsmiljön**. Här blir webbplatsens sidor tillgängliga för den avsedda publiken i enlighet med det gränssnitt som har utformats.

Normalt ligger publiceringsmiljön innanför den demilitariserade zonen. med andra ord, tillgängliga för Internet, men inte längre till fullständigt skydd för det interna nätverket.

När AEM-webbplatsen är en [communitywebbplats](/help/communities/overview.md), eller innehåller [communitykomponenter](/help/communities/author-communities.md), kan besökare (medlemmar) som är inloggade interagera med communityfunktioner. De kan till exempel publicera på ett forum, publicera en kommentar eller följa andra medlemmar. Medlemmar kan ges behörighet att utföra åtgärder som normalt bara är avsedda för författarmiljön, t.ex. skapa nya sidor (communitygrupper), bloggartiklar och moderata inlägg från andra medlemmar.

>[!NOTE]
>
>Tyvärr förekommer ibland en överlappning i den terminologi som används. Detta kan inträffa med:
>
>* **Publicera/avpublicera**
   >  Detta är de primära villkoren för de åtgärder som gör innehållet tillgängligt för allmänheten i publiceringsmiljön (eller inte).
   >
   >
* **Aktivera/inaktivera**
   >  Dessa termer är synonyma med publicera/avpublicera.
   >
   >
* **Replikering/replikering**
   >  Detta är de tekniska termer som används för att ange dataförflyttning (t.ex. sidinnehåll, filer, kod, användarkommentarer) från en miljö till en annan. t.ex. vid publicering, eller vid omvänd replikering av användarkommentarer.
>



#### Dispatcher {#dispatcher}

För att optimera prestanda för besökare på webbplatsen **[implementerar dispatchern](https://helpx.adobe.com/experience-manager/dispatcher/user-guide.html)**belastningsfördelning och cachning.
