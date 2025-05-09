---
title: Appmallar och komponenter
description: Följ den här sidan om du vill veta mer om appmallar och komponenter. Den innehåller detaljerad information om mallarnas struktur.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
exl-id: 58d95325-7cb1-4204-842d-17add70e1fbf
solution: Experience Manager
feature: Mobile
role: User
source-git-commit: 2dae56dc9ec66f1bf36bbb24d6b0315a5f5040bb
workflow-type: tm+mt
source-wordcount: '387'
ht-degree: 0%

---

# Appmallar och komponenter{#app-templates-and-components}

{{ue-over-mobile}}

En mall används för att skapa en sida och definierar vilka komponenter som kan användas i det valda omfånget. En mall är en hierarki med noder som har samma struktur som den sida som ska skapas, men utan något verkligt innehåll.

Varje mall innehåller ett urval av komponenter som är tillgängliga för användning.

* Mallar består av [komponenter](/help/sites-developing/components.md);
* Komponenterna använder, och tillåter åtkomst till, widgetar och dessa används för att återge innehållet.

>[!NOTE]
>
>Mer information om hur du utvecklar ditt Adobe Experience Manager-program (AEM) med CRXDE Lite finns i [Utveckla med CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md).

En mall är grunden för en sida.

Om du vill skapa en sida måste mallen kopieras (node-tree **/apps/&lt;myapp>/templates/&lt;mytemplate>**) till motsvarande position i webbplatsträdet: det här händer om en sida skapas med fliken **Webbplatser** .

Den här kopieringsåtgärden ger även sidan dess ursprungliga innehåll (vanligtvis innehåll på översta nivån) och egenskapen sling:resourceType, sökvägen till sidkomponenten som används för att återge sidan (allt i den underordnade noden jcr:content).

## Mallens struktur {#structure-of-a-template}

Det finns två aspekter att tänka på:

* mallens struktur
* strukturen för det innehåll som skapas när en mall används

En mall skapas under en nod av typen **cq:Template**.

Du kan ange olika egenskaper, särskilt:

* **jcr:title** - mallens rubrik visas i dialogrutan när du skapar en sida.
* **jcr:description** - beskrivning av mallen; visas i dialogrutan när du skapar en sida.

Den här noden innehåller *en jcr:content (cq:PageContent)*-nod som används som bas för innehållsnoden för de resulterande sidorna. Det här refererar, med *sling:resourceType*, till komponenten som ska användas för att återge det faktiska innehållet på en ny sida.

>[!NOTE]
>
>Mer information om grunderna för mallar och komponenter i AEM finns i resurserna nedan:
>
>* [Mallar](/help/sites-developing/templates.md)
>* [Komponenter](/help/sites-developing/components.md)
>

När du har grundläggande kunskaper om mallar och komponenter kan du läsa följande resurser:

* [Skapa och lägga till mallar och komponenter](/help/mobile/mobile-ondemand-app-templates.md)
* [Exportera innehåll med hjälp av innehållsegenskaper](/help/mobile/on-demand-content-properties-exporting.md)
* [Bästa praxis](/help/mobile/best-practices-aem-mobile.md)
* [Utveckla AEM Mobile Content Services](/help/mobile/developing-content-services.md)

### Ytterligare resurser {#additional-resources}

Länkarna nedan innehåller mer information om mobilappar:

* [Mobil med innehållssynkronisering](/help/mobile/mobile-ondemand-contentsync.md)
* [Testar mobilappar](/help/mobile/develop-mobile-apps-testing.md)
