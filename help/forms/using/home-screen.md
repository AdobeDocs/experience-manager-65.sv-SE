---
title: Hemskärm
seo-title: Hemskärm
description: Beskrivning av komponenterna i AEM Forms-appen - startsida
seo-description: Beskrivning av komponenterna i AEM Forms-appen - startsida
uuid: abc95e58-a685-42a9-82ab-4990155945d3
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: ba79479b-4159-4a39-95eb-2285e7ece9d4
docset: aem65
translation-type: tm+mt
source-git-commit: 4a0f3f64095b4726f295a0c1857a1e999353f5f5

---


# Hemskärm{#home-screen}

När du loggar in på appen AEM Forms omdirigeras du till hemskärmen.

## Standardhemskärm {#default-home-screen}

Som standard visas alla formulär, inklusive startpunkter och uppgifter (om den anslutna servern är AEM Forms Workflow aktiverad), tillsammans med tillhörande miniatyrbilder på startskärmen. Du kan ange miniatyrbilder på AEM Forms-servern.

Följande bild är kommenterad med utanrop till de viktigaste komponenterna på startskärmen.

![Startskärmen för appen Formulär](assets/home-screen-1.png)

<!--Click to enlarge

![home-screen-1-1](assets/home-screen-1-1.png)-->

1. **Menyknapp**: Tryck på knappen **Meny** för att navigera till Åtgärder, Formulär, Utkorgen och Inställningar. Om din AEM Forms-app är ansluten till en AEM Forms JEE-server kan du se alternativet Åtgärder. Alternativet Uppgifter lagrar även utkast som skapats från uppgifter i en process. För AEM Forms OSGi-servrar är aktivitetsalternativet dolt. I Outbox lagras de sparade formulären och utkasten innan de synkroniseras med servern. Alla sparade formulär och utkast i Utkorgen överförs till AEM Forms-servern när appen [synkroniseras med servern](../../forms/using/sync-app.md). Mer information om inställningar finns i [Uppdatera allmänna inställningar](../../forms/using/update-general-settings.md).
1. **Uppgift eller formulär**: Tryck på uppgiften eller formuläret som du vill arbeta med.
1. **Vågrät ellips**: Anger att åtgärder är tillgängliga för formuläret. När du trycker på ellipsen visas de åtgärder och den som har skrivit beskrivningen. Alternativet **Ta bort utkast** och **fullständigt** visas när du trycker på ellipsen.
1. **Ikonen** Uppdatera: Tryck på uppdateringsikonen för att synkronisera din app med AEM Forms-servern.

### Anpassa hemskärmen {#customizing-the-home-screen}

![Allmänna inställningar](assets/gen-settings.png)

Du kan ändra programmets standardhemskärm antingen från programmets **[allmänna inställningar](../../forms/using/update-general-settings.md)**eller från fliken **Inställningar**på HTML-arbetsytan.

Ändringen av inställningen för startskärmen i appen påverkar startskärmen för den inloggade användaren eller användaren på den aktuella mobila enheten.

Ändringen i HTML Workspace påverkar dock alla AEM Forms-appanvändare som är inloggade på AEM Forms-servern.

[Kontakta supporten](https://www.adobe.com/account/sign-in.supportportal.html)
