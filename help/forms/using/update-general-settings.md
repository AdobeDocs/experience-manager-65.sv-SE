---
title: Uppdaterar allmänna inställningar
description: Uppdatera inställningar för AEM Forms-appar som hemskärmen och hämta starpunkter och alternativ för bilagor
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
docset: aem65
exl-id: 3e74cda2-ba3e-4ee9-b7d0-76a804232199
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '388'
ht-degree: 0%

---

# Uppdaterar allmänna inställningar{#updating-general-settings}

Med de allmänna inställningarna för AEM Forms-appen kan du ange inställningar som hämtningsbilagor, offlineläge, landningsskärm, standardkategori och frekvens för autosparande.

## Uppdatera de allmänna inställningarna i din app {#working-with-the-form}

När du synkroniserar din app med AEM Forms-servern hämtas alla formulär och definierade uppgifter till din mobila enhet.

Den färdiga AEM Forms-applösningen hämtar inte de bilagor som är kopplade till varje formulär när appen synkroniseras.

Ändra inställningar för hämtning, offlineläge, landningsskärm, automatiskt sparande och synkronisering på fliken Allmänt. Du kan ändra [Hemskärm](../../forms/using/home-screen.md) av appen.

**Navigera till fliken Allmänt på inställningsskärmen**

1. Om du vill gå till inställningsskärmen väljer du menyknappen i det övre vänstra hörnet av hemskärmen och sedan väljer du **Inställningar**.
1. Välj fliken Allmänt på skärmen Inställningar.

   ![Allmänna inställningar i AEM Forms-appen](assets/gen-settings-1.png)

   Skärmen Allmänna inställningar

   >[!NOTE]
   >
   >Alternativen kan visas på olika mobila enheter.

### Allmänna inställningar {#general-settings}

Du kan göra följande ändringar i inställningarna för ditt program.

* **Hämta uppgiftsbilagor**: Anger om de associerade bilagorna ska hämtas eller inte när varje uppgift hämtas till din app.
* **Offlineläge**: Så här aktiverar eller inaktiverar du offlinetjänsten för AEM Forms-programmet. Se [Arbeta i offline-läge](/help/forms/using/work-offline-mode.md) för mer information.
* **Landing screen**: Ange startplats ([Hemskärm](../../forms/using/home-screen.md)) för appen.
Tillgängliga alternativ

   * Forms
   * Uppgifter
   * Favoriter

* **Standardkategori**: Här kan du välja vilken formulärkategori som ska visas på hemskärmen. När du väljer Alla kan du se alla formulär på hemskärmen. Kategorierna fylls i baserat på de formulär som läses in i appen. Forms är tillgängligt i appen baserat på de formulärinställningar som har angetts på AEM Forms-servern.

* **Spara automatiskt, frekvens**: Så här anger du frekvensen för [mobilapp sparar formulärdata](../../forms/using/autosave-data-app.md) lokalt.
* **Synkroniseringsfrekvens**: Så här anger du frekvensen för [mobilappen är synkroniserad](../../forms/using/sync-app.md) med AEM Forms-servern i online-läge.
  **Rensa lokala data**: Rensa databasen, inklusive inställningar och lokala data för alla användare och fillagring från enheten.

>[!NOTE]
>
>Om du rensar cachen loggas du omedelbart ut från appen.
>
>Du uppmanas dock att bekräfta rensningen av cachen.
