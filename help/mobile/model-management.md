---
title: Modeller - översikt
seo-title: Models Overview
description: Modeller - översikt
seo-description: null
uuid: e09dac52-9515-43f7-9d3b-6637e2283d59
contentOwner: Jyotika Syal
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
discoiquuid: c8281f98-9811-42f7-9a31-f82dd0f09319
exl-id: 50785534-5784-4354-b123-5e640b7c0242
source-git-commit: 259f257964829b65bb71b5a46583997581a91a4e
workflow-type: tm+mt
source-wordcount: '784'
ht-degree: 0%

---

# Modeller - översikt{#models-overview}

>[!NOTE]
>
>Adobe rekommenderar att du använder SPA Editor för projekt som kräver ramverksbaserad klientåtergivning för en sida (till exempel React). [Läs mer](/help/sites-developing/spa-overview.md).

Modellhantering innefattar att skapa och hantera modeller för att kunna kopplas till dataobjekt. Varje modell innehåller alla egenskaper och fältdefinitioner som behövs för att det ska bli enklare att skapa och återge objekt.

Modellhantering innefattar skapande av **modeller**, **enheter** och **mellanslag**. I följande diagram visas förhållandet mellan AEM och modellerna.

![chlimage_1-81](assets/chlimage_1-81.png)

## Innehållsmodellen {#the-content-model}

En modell beskriver innehållstypen och vilken information som blir tillgänglig för det ursprungliga programmet. Det är en beskrivning av vad som utgör en del av innehållet. En innehållsmodell är reglerna för hur du skapar en del av innehållet. Innehållsmodellen innehåller vilka data som är tillgängliga, vilka resurser som kan användas, relationen mellan resurser och data, relationen till andra innehållsmodeller och tillgängliga metadata.

Modeller fungerar också som ett sätt att omvandla befintligt AEM till objekt som enkelt kan användas av inbyggda mobilappar.

Content Services kommer att innehålla några färdiga modeller för vanliga objekt som resurser, resurssamlingar, HTML-sidor, appkonfigurationer och kanaloberoende sidor. Dessa kommer att kunna konfigureras så att de uppfyller specifika kundbehov utan att det krävs en AEM utvecklingsinsats.

Användaren kan skapa egna modeller. Detta gör att nya innehållstyper som inte redan hanteras av AEM kan skapas. Modellskapandet görs via ett användargränssnitt med befintliga primitiva typer.

I följande diagram visas innehållsmodellen för AEM Mobile-appar och hur entiteter, mappar och blanksteg tilldelas till ett program.

![chlimage_1-82](assets/chlimage_1-82.png)

### Modeller {#the-models}

Modeller används för att avgöra hur enheter skapas. De definierar vad som är tillgängligt i en enhet och hur data genereras från AEM. Innan du börjar arbeta med Spaces, Folders och Entities bör du känna till hur du skapar och hanterar modeller.

>[!NOTE]
>
>Det finns en modell utanför en app eftersom mer än en app kan använda den.
>

Se **[Modeller](/help/mobile/administer-mobile-apps.md)** för att skapa och hantera modeller på kontrollpanelen och i databasen.

### Enheter i innehållsmodell {#entities-in-content-model}

En entitet är en instans av en innehållsmodell. En enhet exponeras via innehållstjänstens API för klientsidans bibliotek och ger ett sätt för en inbyggd app att komma åt innehåll på ett kanaloberoende sätt.

När det gäller befintligt AEM genereras en entitet med hjälp av en modell och den AEM innehållskällan. En sidenhet är till exempel ett kanal- och layoutoberoende objekt som genereras från en AEM och sidmodellen.

Ändringar av det refererade innehållet i en entitet resulterar i en ändring av entiteten. Om t.ex. en *cq:sida* uppdateras, så kommer alla enheter som är baserade på den sidan också att uppdateras.

Se **[Arbeta med entiteter](/help/mobile/spaces-and-entities.md)** för att skapa anpassade entiteter från modeller.

>[!NOTE]
>
>Om modellen inte motsvarar ett befintligt AEM, t.ex. om kunden har skapat en ny modell, finns det ett användargränssnitt så att kunden kan skapa en ny enhet.
>

### Blanksteg i innehållsmodellen {#spaces-in-content-model}

Ett blanksteg används för att ordna enheter så att de blir lätta att komma åt. Ett blanksteg kan innehålla en eller flera enhetstyper och kan innehålla undermappar.

På AEM sida är ett space ett bekvämt sätt att hantera enheter som är relaterade. Den kan också användas för att tilldela behörigheter. Auktorisering kan göras på ett utrymme, vilket sedan skyddar de enheter som finns i det utrymmet.

*Till exempel*,

En användare har tre allmänna klassificeringar av enheter. Den ena är enbart avsedd för internt bruk, den andra är godkänd för allmänt bruk och den andra är för vanliga enheter som används av många appar. För att förenkla hanteringen skapar användaren tre blanksteg: *internal*, *public* (med både engelskt och franskt innehåll), och *vanlig* för att förvalta de berörda enheterna enligt nedan:

* /content/entities/internal
* /content/entities/public/en
* /content/entities/public/fr
* /content/entities/common

En tjänstslutpunkt kommer att anges för utrymmet så att det inbyggda klientbiblioteket kan begära en lista över innehållet i ett utrymme. Denna &quot;lista&quot; returneras som ett JSON-objekt.

Se **[Blanksteg och entiteter](/help/mobile/spaces-and-entities.md)** för att skapa och publicera platser.

>[!NOTE]
>
>Ett mellanslag kan användas av många appar och ett program kan använda många mellanslag.

### Mappar i innehållsmodellen {#folders-in-content-model}

Med mappar kan användarna ordna enheter efter behov och underlätta finare ACL-kontroll. Blanksteg kan innehålla mappar för att ytterligare ordna utrymmets innehåll och resurser. En användare kan skapa sin egen hierarki under ett space.

Se **[Arbeta med mappar i ett space](/help/mobile/spaces-and-entities.md)** för att skapa och hantera mappar inom ett space.
