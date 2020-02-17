---
title: JCR-integrering
seo-title: JCR-integrering
description: Tips för när du måste integrera på JCR-nivå
seo-description: Tips för när du måste integrera på JCR-nivå
uuid: 11518baf-521e-471d-ad4f-2baa76075cfa
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: e6647a11-a36e-4808-bb61-29b2895c6b1d
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# JCR-integrering{#jcr-integration}

## Föredra Sling Resource API till JCR API {#prefer-the-sling-resource-api-to-jcr-api}

Sling API fungerar på en högre och mer abstrakt nivå än JCR API. Detta gör att koden kan återanvändas mer och vara oberoende av den underliggande lagringen. Detta gör det enklare att inkludera externa virtuella data via ResourceProvider-mekanismen om det behövs.

## Undvik frågor där det är möjligt {#avoid-queries-wherever-possible}

Det är alltid snabbare att navigera i databasen för att hämta data än att köra en fråga. Det finns tillfällen då frågor är nödvändiga, t.ex. en slutanvändarfråga eller behöver hitta strukturerat innehåll från hela databasen, men i alla andra fall är det bäst att navigera till de noder som behövs. Frågor bör alltid undvikas i återgivningslogik som navigeringskomponenter,&quot;lista över nyligen använda objekt&quot;, antal objekt och så vidare. I dessa fall är det bättre att gå igenom hierarkin eller cachelagra resultatet i förväg så att det kan användas direkt när det återges.

## Begränsa omfattningen av JCR-observation {#restrict-the-scope-of-jcr-observation}

När du lyssnar efter händelser i databasen är det viktigt att begränsa omfattningen så mycket som möjligt. Det är till exempel mycket bättre att lyssna efter en händelse på `/etc/mycompany` än att lyssna på `/etc`. Lyssna aldrig efter händelser i databasroten. Kontrollera dessutom att återkallningsmetoderna körs så snabbt som möjligt när det inte finns något att göra.

## Eliminera användningen av JCR-administratörsåtkomst {#eliminate-use-of-jcr-admin-access}

Från och med AEM 6 används inte inloggningsadministration eftersom en administrativ session har hämtats från ResourceResolverFactory. Tjänstkonton ska i stället skapas för back office-åtgärder som skulle kräva den här typen av åtkomst och ResourceResolverFactory kan användas för att hämta en ResourceResolver för det här kontot.
