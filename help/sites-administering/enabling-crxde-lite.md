---
title: Aktivera CRXDE Lite i AEM
seo-title: Aktivera CRXDE Lite i AEM
description: Lär dig hur du aktiverar CRXDE Lite i AEM.
seo-description: Lär dig hur du aktiverar CRXDE Lite i AEM.
uuid: d7a3db67-6384-463b-9aa9-f08ecc6c99c6
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: 72df3ece-badf-466b-8f9a-0ec985d87741
translation-type: tm+mt
source-git-commit: a833a34bbeb938c72cdb851a46b2ffd97aee9f6d

---


# Aktivera CRXDE Lite i AEM{#enabling-crxde-lite-in-aem}

För att säkerställa att AEM-installationerna är så säkra som möjligt rekommenderar checklistan att WebDAV [inaktiveras](/help/sites-administering/security-checklist.md#disable-webdav) i produktionsmiljöer.

CRXDE Lite är dock beroende av att paketet fungerar som det ska, så om du inaktiverar WebDAV inaktiveras även CRXDE Lite. `org.apache.sling.jcr.davex`

När detta inträffar visas en tom rotnod när du bläddrar till `https://serveraddress:4502/crx/de/index.jsp` och alla HTTP-begäranden till CRXDE Lite-resurser misslyckas:

```xml
404 Resource at '/crx/server/crx.default/jcr:root/.1.json' not found: No resource found
```

Den här rekommendationen är avsedd att minska attackytorna så mycket som möjligt, men systemadministratörer kan ibland behöva åtkomst till CRXDE Lite för att kunna söka efter innehåll eller felsöka problem i produktionsinstanser.

Om det är inaktiverat kan du aktivera CRXDE Lite genom att följa nedanstående procedur:

1. Gå till OSGi Components-konsolen på `http://localhost:4502/system/console/components`
1. Sök efter följande komponent:

   * `org.apache.sling.jcr.davex.impl.servlets.SlingDavExServlet`

1. Klicka på skiftnyckelsikonen bredvid den för att visa dess konfigurationsalternativ:

   ![chlimage_1-80](assets/chlimage_1-80a.png)

1. Skapa följande konfiguration:

   * **** Rotsökväg: `/crx/server`
   * Markera rutan under **Använd absoluta URI:er**.

1. När du är klar med CRXDE Lite måste du inaktivera WebDAV igen.

Du kan även aktivera CRXDE Lite via cURL genom att köra följande kommando:

```shell
curl -u admin:admin -F "jcr:primaryType=sling:OsgiConfig" -F "alias=/crx/server" -F "dav.create-absolute-uri=true" -F "dav.create-absolute-uri@TypeHint=Boolean" http://localhost:4502/apps/system/config/org.apache.sling.jcr.davex.impl.servlets.SlingDavExServlet
```

## Andra resurser {#other-resources}

Mer information om säkerhetsfunktionerna i AEM 6 finns på följande sidor:

* [AEM Security Checklist](/help/sites-administering/security-checklist.md)
* [Köra AEM i produktionsklart läge](/help/sites-administering/production-ready.md)

