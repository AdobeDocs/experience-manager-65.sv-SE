---
title: Webbkonsol i Adobe Experience Manager
seo-title: Web Console
description: Lär dig hur du använder AEM webbkonsol.
seo-description: Learn how to use the AEM web console.
uuid: 7856b2b3-4216-421d-a315-cd9a55936362
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: configuring
discoiquuid: 4a33fddd-0399-40e4-8687-564fb6765b76
feature: Configuring
exl-id: 9acbf61f-73a8-4998-9421-dd933f30ac8a
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '719'
ht-degree: 0%

---

# Webbkonsol{#web-console}

Webbkonsolen i AEM baseras på [Apache Felix Web Management Console](https://felix.apache.org/documentation/subprojects/apache-felix-web-console.html). Apache Felix är en community-satsning för att implementera OSGi R4 Service Platform, som innehåller OSGi-ramverket och standardtjänster.

>[!NOTE]
>
>På webbkonsolen finns beskrivningar som anger standardinställningar för Sling.
>
>AEM har sina egna standardinställningar, så standarduppsättningen kan skilja sig från dem som finns dokumenterade på konsolen.

Webbkonsolen erbjuder ett urval flikar för underhåll av OSGi-paketen, bland annat:

* [Konfiguration](#configuration): används för att konfigurera OSGi-paketen och är därför den underliggande mekanismen för att konfigurera AEM systemparametrar
* [Paket](#bundles): används för att installera paket
* [Komponenter](#components): används för att kontrollera status för komponenter som krävs för AEM

Alla ändringar som görs tillämpas omedelbart på det system som körs. Ingen omstart krävs.

Konsolen kan nås från `../system/console`; till exempel:

`http://localhost:4502/system/console/components`

## Konfiguration {#configuration}

The **Konfiguration** -fliken används för att konfigurera OSGi-paket och är därför den underliggande mekanismen för att konfigurera AEM systemparametrar.

>[!NOTE]
>
>Se [OSGi-konfiguration med webbkonsolen](/help/sites-deploying/configuring-osgi.md) för mer information.

The **Konfiguration** -fliken kan nås av antingen:

* Listrutan:

  **OSGi >**

* URL-adressen, till exempel:

  `http://localhost:4502/system/console/configMgr`

En lista över konfigurationer visas:

![screen_shot_2012-02-15at52308pm](assets/screen_shot_2012-02-15at52308pm.png)

Det finns två typer av konfigurationer tillgängliga i listrutorna på den här skärmen:

* **Konfigurationer**
Gör att du kan uppdatera befintliga konfigurationer. Dessa har en Persistent Identity (PID) och kan antingen vara:

   * standard och integral till AEM. Dessa är obligatoriska, om de tas bort, återgår värdena till standardinställningarna.
   * instanser skapade från fabrikskonfigurationer. De här instanserna skapas av användaren och tas bort.

* **Fabrikskonfigurationer**
Gör att du kan skapa en instans av det nödvändiga funktionsobjektet.

  Detta tilldelas en beständig identitet och visas sedan i listrutan Konfigurationer.

Om du väljer en post i listorna visas de parametrar som är kopplade till den konfigurationen:

![chlimage_1-21](assets/chlimage_1-21a.png)

Du kan sedan uppdatera parametrarna efter behov och:

* **Spara**

  Spara ändringarna.

  För en fabrikskonfiguration skapas en ny instans med en beständig identitet. Den nya instansen visas sedan under Konfigurationer.

* **Återställ**

  Återställ parametrarna som visas på skärmen till de som senast sparades.

* **Ta bort**

  Ta bort den aktuella konfigurationen. Om det är standard återställs parametrarna till standardinställningarna. Om den skapas från en fabrikskonfiguration tas den specifika instansen bort.

* **Lås upp**

  Lås upp den aktuella konfigurationen från paketet.

* **Avbryt**

  Avbryt alla aktuella ändringar.

## Paket {#bundles}

The **Paket** är den mekanism som används för att installera OSGi-paket som krävs för AEM. Du kommer åt fliken på något av följande sätt:

* Listrutan:

  **OSGi >**

* URL-adressen, till exempel:

  `http://localhost:4502/system/console/bundles`

En lista över paket visas:

![screen_shot_2012-02-15at44740pm](assets/screen_shot_2012-02-15at44740pm.png)

På den här fliken kan du:

* **Installera eller uppdatera**

  Du kan **Bläddra** för att hitta filen som innehåller ditt paket och ange om det ska **Starta** omedelbart och **Startnivå**.

* **Läs in igen**

  Uppdaterar listan som visas.

* **Uppdatera paket**

  Detta kontrollerar referenserna för alla paket och uppdaterar vid behov.

  Efter en uppdatering kan till exempel både den gamla och den nya versionen fortfarande köras på grund av tidigare referenser. Med det här alternativet kontrolleras och flyttas alla referenser till den nya versionen så att den gamla versionen kan stoppas.

* **Starta**

  Startar ett paket enligt den angivna startnivån.

* **Stoppa**

  Stoppar paketet.

* **Avinstallera**

  Avinstallerar paketet från systemet.

* **visa status**

  Listan anger paketets aktuella status. Klicka på namnet på ett specifikt paket och visa mer information.

>[!NOTE]
>
>Efter **Uppdatera** vi rekommenderar att du utför en **Uppdatera paket**.

## Komponenter {#components}

The **Komponenter** På -fliken kan du aktivera och/eller inaktivera de olika komponenterna. Den kan nås av antingen:

* Listrutan:

  **Main >**

* URL-adressen, till exempel:

  `http://localhost:4502/system/console/components`

En lista med komponenter visas. Det finns olika ikoner som du kan använda för att aktivera, inaktivera eller (där det är lämpligt) öppna konfigurationsinformation för en viss komponent.

![screen_shot_2012-02-15at52144pm](assets/screen_shot_2012-02-15at52144pm.png)

Om du klickar på namnet på en viss komponent visas mer information om dess status. Här kan du även aktivera, inaktivera eller läsa in komponenten igen.

![chlimage_1-22](assets/chlimage_1-22a.png)

>[!NOTE]
>
>Om du aktiverar, eller inaktiverar, en komponent gäller det bara tills AEM/CRX startas om.
>
>Startläget definieras i komponentbeskrivningen, som genereras under utveckling och lagras i paketet när paketet skapas.
