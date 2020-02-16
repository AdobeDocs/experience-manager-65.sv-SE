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

---


# Köra AEM i produktionsklart läge{#running-aem-in-production-ready-mode}

Med AEM 6.1 introducerar Adobe det nya `"nosamplecontent"` runmode som syftar till att automatisera de steg som krävs för att förbereda en AEM-instans för driftsättning i en produktionsmiljö.

Det nya körningsläget konfigurerar inte bara instansen automatiskt så att den följer de säkerhetspraxis som beskrivs i checklistan för säkerhet, utan tar även bort alla exempelgeometrixprogram och -konfigurationer i processen.

>[!NOTE]
>
>Eftersom AEM Production Ready Mode av praktiska skäl endast omfattar de flesta uppgifter som behövs för att skydda en instans rekommenderar vi att du läser [säkerhetschecklistan](/help/sites-administering/security-checklist.md) innan du publicerar i produktionsmiljön.
>
>Observera också att om du kör AEM i Production Ready Mode inaktiveras åtkomsten till CRXDE Lite. Om du behöver det för felsökning läser du [Aktivera CRXDE Lite i AEM](/help/sites-administering/enabling-crxde-lite.md).

![chlimage_1-83](assets/chlimage_1-83a.png)

Om du vill köra AEM i produktionsklar läge behöver du bara lägga till `nosamplecontent` filen via `-r` runmode-växeln till dina befintliga startargument:

```shell
java -jar aem-quickstart.jar -r nosamplecontent
```

Du kan t.ex. använda den produktion som är klar för att starta en författarinstans med MongoDB-beständighet så här:

```shell
java -jar aem-quickstart.jar -r author,crx3,crx3mongo,nosamplecontent -Doak.mongo.uri=mongodb://remoteserver:27017 -Doak.mongo.db=aem-author
```

## Ändrar en del av produktionsklart läge {#changes-part-of-the-production-ready-mode}

Mer specifikt kommer följande konfigurationsändringar att utföras när AEM körs i produktionsklart läge:

1. Supportpaketet för **CRXDE** ( `com.adobe.granite.crxde-support`) är inaktiverat som standard i produktionsklar läge. Den kan installeras när som helst från Adobe Public Maven-databasen. Version 3.0.0 krävs för AEM 6.1.

1. Paketet med **Apache Sling Simple WebDAV Access till databaser** ( `org.apache.sling.jcr.webdav`) är bara tillgängligt för **författarinstanser** .

1. Användare som skapats nyligen måste ändra lösenordet vid den första inloggningen. Detta gäller inte administratörsanvändaren.
1. **Generera felsökningsinformation** är inaktiverat för **Apache Java Script Handler**.

1. **Mappat innehåll** och **genererad felsökningsinformation** är inaktiverade för JSP-skripthanteraren för **Apache Sling**.

1. CQ WCM-filtret **för** dag är inställt på `edit` författare **och** vid `disabled` publicering **** .

1. **Adobe Granite HTML Library Manager** har konfigurerats med följande inställningar:

   1. **** Minimera: `enabled`
   1. **** Felsök: `disabled`
   1. **** Gzip: `enabled`
   1. **** Timing: `disabled`

1. Apache **Sling GET-servern** är inställd på att som standard stödja säkra konfigurationer enligt följande:

| **Konfiguration** | **Författare** | **Publicera** |
|---|---|---|
| TXT-rendering | inaktiverat | inaktiverat |
| HTML-återgivning | inaktiverat | inaktiverat |
| JSON-rendering | aktiverad | aktiverad |
| XML-rendering | inaktiverat | inaktiverat |
| json.maximiumresults | 1000 | 100 |
| Automatiskt index | inaktiverat | inaktiverat |

