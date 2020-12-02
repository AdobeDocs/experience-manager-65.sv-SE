---
title: Uppdaterar allmänna inställningar
seo-title: Uppdaterar allmänna inställningar
description: Uppdatera inställningar för AEM Forms-appar som hemskärmen och hämta starpunkter och alternativ för bilagor
seo-description: Uppdatera inställningar för AEM Forms-appar som hemskärmen och hämta starpunkter och alternativ för bilagor
uuid: 650d677e-2b3c-498e-9e46-fa659af934ca
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 7fdb9fab-6bae-49b8-86b6-66138a2a6cd3
docset: aem65
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317
workflow-type: tm+mt
source-wordcount: '407'
ht-degree: 0%

---


# Uppdaterar allmänna inställningar{#updating-general-settings}

Med de allmänna inställningarna för AEM Forms-appen kan du ange inställningar som hämtningsbilagor, offlineläge, landningsskärm, standardkategori och frekvens för autosparande.

## Uppdaterar de allmänna inställningarna i din app {#working-with-the-form}

När du synkroniserar din app med AEM Forms-servern hämtas alla formulär och definierade uppgifter till din mobila enhet.

Den färdiga AEM Forms-applösningen hämtar inte de bilagor som är kopplade till varje formulär när appen synkroniseras.

Ändra inställningar för hämtning, offlineläge, landningsskärm, automatiskt sparande och synkronisering på fliken Allmänt. Du kan ändra [startskärmen](../../forms/using/home-screen.md) för din app.

**Navigera till fliken Allmänt på inställningsskärmen**

1. Om du vill gå till inställningsskärmen trycker du på knappen Meny längst upp till vänster på startskärmen och sedan på **Inställningar**.
1. Tryck på fliken Allmänt på skärmen Inställningar.

   ![Allmänna inställningar i AEM Forms-appen](assets/gen-settings-1.png)

   Skärmen Allmänna inställningar

   >[!NOTE]
   >
   >Alternativen kan visas på olika mobila enheter.

### Allmänna inställningar {#general-settings}

Du kan göra följande ändringar i inställningarna för ditt program.

* **Hämta uppgiftsbilagor**: Anger om de associerade bilagorna ska hämtas eller inte när varje uppgift hämtas till din app.
* **Offlineläge**: Om du vill aktivera eller inaktivera offlinetjänsten för AEM Forms-programmet. Mer information finns i [Arbeta i offlineläge](/help/forms/using/work-offline-mode.md).
* **Landningsskärm**: Ange programmets startplats ([hemskärmen](../../forms/using/home-screen.md)).
Tillgängliga alternativ:

   * Forms
   * Uppgifter
   * Favoriter

* **Standardkategori**: Här kan du välja vilken formulärkategori som ska visas på hemskärmen. När du väljer Alla kan du se alla formulär på hemskärmen. Kategorierna fylls i baserat på de formulär som läses in i appen. Forms är tillgängligt i appen baserat på de formulärinställningar som har angetts på AEM Forms-servern.

* **Spara automatiskt**: Anger hur ofta  [mobilappen sparar formuläret ](../../forms/using/autosave-data-app.md) digitalt.
* **Synkroniseringsfrekvens**: Anger hur ofta din  [mobilapp ska ](../../forms/using/sync-app.md) synkroniseras med AEM Forms-servern i online-läge.
   **Rensa lokala data**: Rensa databasen, inklusive inställningar och lokala data för alla användare och fillagring från enheten.

>[!NOTE]
>
>Om du rensar cachen loggas du omedelbart ut från appen.
>
>Du uppmanas dock att bekräfta rensningen av cachen.
