---
title: Aktivera CRXDE Lite i AEM
description: Lär dig hur du aktiverar CRXDE Lite i Adobe Experience Manager.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
exl-id: bf51def2-1dd4-4bd3-b989-685058f0ead8
source-git-commit: 1807919078996b1cf1cbd1f2d90c3b14cb660e2c
workflow-type: tm+mt
source-wordcount: '254'
ht-degree: 0%

---

# Aktivera CRXDE Lite i AEM{#enabling-crxde-lite-in-aem}

För att säkerställa att AEM installationer är så säkra som möjligt rekommenderar checklistan [inaktivera WebDAV](/help/sites-administering/security-checklist.md#disable-webdav) i produktionsmiljöer.

CRXDE Lite är dock beroende av `org.apache.sling.jcr.davex` så att WebDAV-paketet fungerar som det ska, så att även CRXDE Lite inaktiveras om du inaktiverar det.

När det händer går du till `https://serveraddress:4502/crx/de/index.jsp` visar en tom rotnod och alla HTTP-begäranden till CRXDE Lite-resurser misslyckas:

```xml
404 Resource at '/crx/server/crx.default/jcr:root/.1.json' not found: No resource found
```

Den här rekommendationen är avsedd att minska attackytan så mycket som möjligt, men systemadministratörer kan ibland behöva åtkomst till CRXDE Lite för att kunna bläddra bland innehåll eller felsöka problem i produktionsinstanser.

Du kan aktivera CRXDE Lite med antingen [OSGi-inställningar](#enabling-crxde-lite-osgi) eller med [cURL, kommando](#enabling-crxde-lite-curl).

>[!WARNING]
>
>På grund av små skillnader i hur dessa metoder fungerar bör du använda ***antingen*** OSGI ***eller*** cURL.
>
>De två metoderna är ***not*** utbytbart.

## Aktivera CRXDE Lite med OSGI {#enabling-crxde-lite-osgi}

Om du avaktiverar det här alternativet kan du aktivera CRXDE Lite genom att följa nedanstående procedur:

1. Gå till OSGi Components-konsolen på `http://localhost:4502/system/console/components`
1. Sök efter följande komponent:

   * `org.apache.sling.jcr.davex.impl.servlets.SlingDavExServlet`

1. Klicka på skiftnyckelsikonen bredvid den för att visa dess konfigurationsalternativ:

   ![chlimage_1-80](assets/chlimage_1-80a.png)

1. Skapa följande konfiguration:

   * **Rotsökväg:** `/crx/server`
   * Fäst lådan under **Använd absoluta URI:er**.

1. När du är klar med CRXDE Lite måste du inaktivera WebDAV igen.

## Aktivera CRXDE Lite med cURL {#enabling-crxde-lite-curl}

Du kan även aktivera CRXDE Lite via cURL genom att köra det här kommandot:

```shell
curl -u admin:admin -F "jcr:primaryType=sling:OsgiConfig" -F "alias=/crx/server" -F "dav.create-absolute-uri=true" -F "dav.create-absolute-uri@TypeHint=Boolean" http://localhost:4502/apps/system/config/org.apache.sling.jcr.davex.impl.servlets.SlingDavExServlet
```

## Andra resurser {#other-resources}

Mer information om säkerhetsfunktionerna i AEM 6 finns på följande sidor:

* [AEM checklista](/help/sites-administering/security-checklist.md)
* [Köra AEM i produktionsklart läge](/help/sites-administering/production-ready.md)
