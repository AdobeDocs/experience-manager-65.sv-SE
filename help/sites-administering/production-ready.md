---
title: Köra AEM i produktionsklart läge
seo-title: Running AEM in Production Ready Mode
description: Lär dig hur du kör AEM i produktionsklart läge.
seo-description: Learn how to run AEM in Production Ready Mode.
uuid: f48c8bae-c72f-4772-967e-f1526f096399
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: 32da99f0-f058-40ae-95a8-2522622438ce
exl-id: 3c342014-f8ec-4404-afe5-514bdb651aae
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '383'
ht-degree: 1%

---

# Köra AEM i produktionsklart läge{#running-aem-in-production-ready-mode}

Med AEM 6.1 introducerar Adobe den nya `"nosamplecontent"` runmode som automatiserar de steg som krävs för att förbereda en AEM instans för driftsättning i en produktionsmiljö.

Det nya körningsläget konfigurerar inte bara instansen automatiskt så att den följer de säkerhetspraxis som beskrivs i checklistan för säkerhet, utan tar även bort alla exempelgeometrixprogram och -konfigurationer i processen.

>[!NOTE]
>
>Eftersom AEM produktionsklart läge av praktiska skäl endast omfattar de flesta uppgifter som krävs för att skydda en instans rekommenderar vi att du läser [Säkerhetschecklista](/help/sites-administering/security-checklist.md) innan du publicerar med produktionsmiljön.
>
>Observera också att om du kör AEM i produktionsklart läge inaktiveras åtkomsten till CRXDE Lite. Om du behöver det för felsökning kan du läsa [Aktivera CRXDE Lite i AEM](/help/sites-administering/enabling-crxde-lite.md).

![chlimage_1-83](assets/chlimage_1-83a.png)

För att kunna köra AEM i produktionsklar läge behöver du bara lägga till `nosamplecontent` via `-r` byt runmode till dina befintliga startargument:

```shell
java -jar aem-quickstart.jar -r nosamplecontent
```

Du kan t.ex. använda den produktion som är klar för att starta en författarinstans med MongoDB-beständighet så här:

```shell
java -jar aem-quickstart.jar -r author,crx3,crx3mongo,nosamplecontent -Doak.mongo.uri=mongodb://remoteserver:27017 -Doak.mongo.db=aem-author
```

## Ändrar en del av produktionsklart läge {#changes-part-of-the-production-ready-mode}

Mer specifikt kommer följande konfigurationsändringar att utföras när AEM körs i produktionsklar läge:

1. The **CRXDE-supportpaket** ( `com.adobe.granite.crxde-support`) är inaktiverat som standard i produktionsklar läge. Den kan installeras när som helst från Adobe offentliga Maven-databasen. Version 3.0.0 krävs för AEM 6.1.

1. The **Apache Sling Simple WebDAV Åtkomst till databaser** ( `org.apache.sling.jcr.webdav`) kommer endast att vara tillgängligt på **författare** -instanser.

1. Användare som skapats nyligen måste ändra lösenordet vid den första inloggningen. Detta gäller inte administratörsanvändaren.
1. **Generera felsökningsinformation** är inaktiverat för **Apache Sling Java Script Handler**.

1. **Mappat innehåll** och **Generera felsökningsinformation** är inaktiverade för **Apache Sling JSP Script Handler**.

1. The **Dag CQ WCM-filter** är inställd på `edit` på **författare** och `disabled` på **publicera** -instanser.

1. The **Bibliotekshanteraren Adobe Granite HTML** har konfigurerats med följande inställningar:

   1. **Minimera:** `enabled`
   1. **Felsök:** `disabled`
   1. **Gzip:** `enabled`
   1. **Timing:** `disabled`

1. The **Apache Sling GET Servlet** är inställt på att stödja säkra konfigurationer som standard enligt följande:

| **Konfiguration** | **Författare** | **Publicera** |
|---|---|---|
| TXT-rendering | inaktiverad | inaktiverad |
| HTML rendering | inaktiverad | inaktiverad |
| JSON-rendering | aktiverad | aktiverad |
| XML-rendering | inaktiverad | inaktiverad |
| json.maximumresults | 1000 | 100 |
| Automatiskt index | inaktiverad | inaktiverad |
