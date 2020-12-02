---
title: Köra AEM i produktionsklart läge
seo-title: Köra AEM i produktionsklart läge
description: Lär dig hur du kör AEM i produktionsklart läge.
seo-description: Lär dig hur du kör AEM i produktionsklart läge.
uuid: f48c8bae-c72f-4772-967e-f1526f096399
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: 32da99f0-f058-40ae-95a8-2522622438ce
translation-type: tm+mt
source-git-commit: 1c1ade947f2cbd26b35920cfd10b1666b132bcbd
workflow-type: tm+mt
source-wordcount: '397'
ht-degree: 3%

---


# Kör AEM i produktionsklart läge{#running-aem-in-production-ready-mode}

I AEM 6.1 introducerar Adobe det nya `"nosamplecontent"`-körningsläget som automatiserar de steg som krävs för att förbereda en AEM instans för driftsättning i en produktionsmiljö.

Det nya körningsläget konfigurerar inte bara instansen automatiskt så att den följer de säkerhetspraxis som beskrivs i checklistan för säkerhet, utan tar även bort alla exempelgeometrixprogram och -konfigurationer i processen.

>[!NOTE]
>
>Eftersom AEM produktionsklart läge av praktiska skäl endast omfattar de flesta uppgifter som krävs för att skydda en instans rekommenderar vi att du läser [säkerhetschecklistan](/help/sites-administering/security-checklist.md) innan du publicerar i produktionsmiljön.
>
>Observera också att om du kör AEM i produktionsklart läge inaktiveras åtkomsten till CRXDE Lite. Om du behöver det för felsökning läser du [Aktivera CRXDE Lite i AEM](/help/sites-administering/enabling-crxde-lite.md).

![chlimage_1-83](assets/chlimage_1-83a.png)

För att kunna köra AEM i produktionsklar läge behöver du bara lägga till `nosamplecontent` via körningsväxeln `-r` till dina befintliga startargument:

```shell
java -jar aem-quickstart.jar -r nosamplecontent
```

Du kan t.ex. använda den produktion som är klar för att starta en författarinstans med MongoDB-beständighet så här:

```shell
java -jar aem-quickstart.jar -r author,crx3,crx3mongo,nosamplecontent -Doak.mongo.uri=mongodb://remoteserver:27017 -Doak.mongo.db=aem-author
```

## Ändrar en del av produktionsklart läge {#changes-part-of-the-production-ready-mode}

Mer specifikt kommer följande konfigurationsändringar att utföras när AEM körs i produktionsklar läge:

1. **CRXDE-stödpaketet** ( `com.adobe.granite.crxde-support`) är inaktiverat som standard i produktionsklart läge. Den kan installeras när som helst från Adobe offentliga Maven-databasen. Version 3.0.0 krävs för AEM 6.1.

1. **Apache Sling Simple WebDAV Access till databaser** ( `org.apache.sling.jcr.webdav`)-paketet är bara tillgängligt för **författare**-instanser.

1. Användare som skapats nyligen måste ändra lösenordet vid den första inloggningen. Detta gäller inte administratörsanvändaren.
1. **Generate debug** info är inaktiverad för  **Apache Java Script Handler**.

1. **Mappat** innehåll och  **genererad felsökningsinformation är** inaktiverade för JSP-skripthanteraren för  **Apache Sling**.

1. **Dag CQ WCM-filtret** är inställt på `edit` på **författare** och `disabled` på **publiceringsinstanser**.

1. **HTML Library** Manager för Adobe Granite har konfigurerats med följande inställningar:

   1. **Minimera:** `enabled`
   1. **Felsök:** `disabled`
   1. **Gzip:** `enabled`
   1. **Timing:** `disabled`

1. **Apache Sling GET-servern** är inställd på att stödja säkra konfigurationer som standard enligt följande:

| **Konfiguration** | **Författare** | **Publicera** |
|---|---|---|
| TXT-rendering | inaktiverat | inaktiverat |
| HTML-återgivning | inaktiverat | inaktiverat |
| JSON-rendering | aktiverad | aktiverad |
| XML-rendering | inaktiverat | inaktiverat |
| json.maximumresults | 1000 | 100 |
| Automatiskt index | inaktiverat | inaktiverat |

