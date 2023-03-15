---
title: Hemskärm
seo-title: Home screen
description: Beskrivning av komponenterna i startskärmen för AEM Forms-appen
seo-description: Description of the components of the AEM Forms app Home screen
uuid: abc95e58-a685-42a9-82ab-4990155945d3
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: ba79479b-4159-4a39-95eb-2285e7ece9d4
docset: aem65
exl-id: 6c6fb516-1b11-4da4-b638-4388a070e397
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '331'
ht-degree: 0%

---

# Hemskärm{#home-screen}

När du loggar in på AEM Forms omdirigeras du till hemskärmen.

## Standardhemskärm {#default-home-screen}

Som standard visas alla formulär, inklusive startpunkter och uppgifter, på startskärmen (om den anslutna servern är AEM Forms Workflow aktiverad) tillsammans med tillhörande miniatyrbilder. Du kan ange miniatyrbilder på AEM Forms-servern.

Följande bild är kommenterad med utanrop till de viktigaste komponenterna på startskärmen.

![Forms app - startskärm](assets/home-screen-1.png)

<!--Click to enlarge

![home-screen-1-1](assets/home-screen-1-1.png)-->

1. **Menyknapp**: Tryck på **Meny** för att navigera till Uppgifter, Forms, Utkorgen och Inställningar. Om din AEM Forms-app är ansluten till en AEM Forms JEE-server kan du se alternativet Åtgärder. Alternativet Uppgifter lagrar även utkast som skapats från uppgifter i en process. För AEM Forms OSGi-servrar är aktivitetsalternativet dolt. I Outbox lagras de sparade formulären och utkasten innan de synkroniseras med servern. Alla sparade formulär och utkast i Utkorgen överförs till AEM Forms-servern när appen [synkroniserad med servern](../../forms/using/sync-app.md). Mer information om inställningar finns i [Uppdatera allmänna inställningar](../../forms/using/update-general-settings.md).
1. **Uppgift eller formulär**: Tryck på uppgiften eller formuläret som du vill arbeta med.
1. **Vågrät ellips**: Anger att åtgärder är tillgängliga för formuläret. När du trycker på ellipsen visas de åtgärder och den som har skrivit beskrivningen. The **Ta bort utkast** och **Slutförd** är synligt när du trycker på ellipsen.
1. **Ikonen Uppdatera**: Tryck på uppdateringsikonen för att synkronisera appen med AEM Forms-servern.

### Anpassa hemskärmen {#customizing-the-home-screen}

![Allmänna inställningar](assets/gen-settings.png)

Du kan ändra standardhemskärmen för programmet antingen från **[Allmänna inställningar](../../forms/using/update-general-settings.md)** från appen eller från **Inställningar** på arbetsytan i HTML.

Ändringen av inställningen för startskärmen i appen påverkar startskärmen för den inloggade användaren eller användaren på den aktuella mobila enheten.

Ändringen i HTML Workspace påverkar dock alla AEM Forms-appanvändare som är inloggade på AEM Forms-servern.
