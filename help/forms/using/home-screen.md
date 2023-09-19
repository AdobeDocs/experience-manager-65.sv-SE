---
title: Hemskärm
description: Beskrivning av komponenterna i startskärmen för AEM Forms-appen
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
docset: aem65
exl-id: 6c6fb516-1b11-4da4-b638-4388a070e397
source-git-commit: 65c5a4442f17e6bc52deaa1588f535a05698083f
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 0%

---

# Hemskärm{#home-screen}

När du loggar in på AEM Forms omdirigeras du till hemskärmen.

## Standardhemskärm {#default-home-screen}

Som standard visas alla formulär, inklusive startpunkter och uppgifter, på startskärmen (om den anslutna servern är AEM Forms Workflow aktiverad) tillsammans med tillhörande miniatyrbilder. Du kan ange miniatyrbilder i AEM Forms Server.

Följande bild är kommenterad med utanrop till de viktigaste komponenterna på startskärmen.

![Forms app - startskärm](assets/home-screen-1.png)

<!--Click to enlarge

![home-screen-1-1](assets/home-screen-1-1.png)-->

1. **Menyknapp**: Tryck på **Meny** för att navigera till Uppgifter, Forms, Utkorgen och Inställningar. Om din AEM Forms-app är ansluten till en AEM Forms JEE-server kan du se alternativet Åtgärder. Alternativet Uppgifter lagrar även utkast som skapats från uppgifter i en process. För AEM Forms OSGi-servrar är alternativet Åtgärder dolt. I Outbox lagras de sparade formulären och utkasten innan de synkroniseras med servern. Alla sparade formulär och utkast i Utkorgen överförs till AEM Forms Server när appen [synkroniserad med servern](../../forms/using/sync-app.md). Mer information om inställningar finns i [Uppdatera allmänna inställningar](../../forms/using/update-general-settings.md).
1. **Uppgift eller formulär**: Tryck på uppgiften eller formuläret som du vill arbeta med.
1. **Vågrät ellips**: Anger att åtgärder är tillgängliga för formuläret. När du trycker på ellipsen visas de åtgärder och den beskrivning som författaren har angett. The **Ta bort utkast** och **Complete** är synligt när du trycker på ellipsen.
1. **Ikonen Uppdatera**: Tryck på uppdateringsikonen så att du kan synkronisera appen med AEM Forms Server.

### Anpassa hemskärmen {#customizing-the-home-screen}

![Allmänna inställningar](assets/gen-settings.png)

Du kan ändra standardhemskärmen för programmet antingen från **[Allmänna inställningar](../../forms/using/update-general-settings.md)** från appen eller från **Inställningar** på arbetsytan i HTML.

Ändringen av inställningen för startskärmen i appen påverkar startskärmen för den inloggade användaren eller användaren på den aktuella mobila enheten.

Ändringen i HTML Workspace påverkar dock alla AEM Forms-appanvändare som är inloggade på AEM Forms Server.
