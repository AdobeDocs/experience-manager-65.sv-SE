---
title: Använda automatiskt sparade i AEM Forms-appen
seo-title: Använda automatiskt sparade i AEM Forms-appen
description: Lär dig hur du använder funktionen Spara automatiskt i AEM Forms-appen för att undvika dataförlust.
seo-description: Lär dig hur du använder funktionen Spara automatiskt i AEM Forms-appen för att undvika dataförlust.
uuid: 00fe6a10-1a72-443d-a840-0415dc769199
contentOwner: sashanka
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 2c71cc28-b7c8-4785-9fc2-b47fa80cbd70
docset: aem65
translation-type: tm+mt
source-git-commit: d9975c0dcc02ae71ac64aadb6b4f82f7c993f32c
workflow-type: tm+mt
source-wordcount: '316'
ht-degree: 0%

---


# Använda automatiskt sparade i AEM Forms-app{#using-autosave-in-aem-forms-app}

När en användare matar in data i Adobe Experience Manager Forms-appen sparar funktionen automatiskt dem med regelbundna intervall. Funktionen Spara automatiskt i AEM Forms-appen hjälper dig att undvika dataförluster om appen stängs av misstag.

Ditt program kan stängas av misstag:

* Om enheten stängs av på grund av för lite batteri
* Om användaren dödar appen
* Om en oväntad krasch inträffar

Du kan ange de intervall efter vilka appen sparar de angivna data.

>[!NOTE]
>
>Välj autosparfrekvens med omdöme. Automatiska åtgärder som sparas ofta kan ha en märkbar inverkan på enhetens prestanda.

Så här använder du funktionen Spara automatiskt i AEM Forms-appen:

1. Logga in på appen och gå till **Inställningar > Allmänt**.
1. På skärmen Allmänt använder du alternativet **Spara frekvens automatiskt** för att välja de intervall där du vill att appen ska spara angivna data.
   [ ![Ställa in autosparfrekvens](assets/using-autosave-freq-07.png)](assets/using-autosave-freq-07-1.png)

1. När du startar om programmet och loggar in med samma användare uppmanas du att återställa uppgiften i dialogrutan Återställ osparad uppgift. Klicka på **OK** i dialogrutan Återställ osparad uppgift för att fortsätta arbeta med den sparade uppgiften. Du kan klicka på **Avbryt** om du vill ta bort sparade data som motsvarar den senast aktiverade autosparfunktionen och börja arbeta med en ny uppgift.

   När du klickar på **OK** återställs uppgiften med de data som motsvarar den senaste autosparfunktionen som utlöstes innan appen kraschade. Den innehåller formulärdata och alla bilagor som är associerade med uppgiften.
   [ ![Hämtning av en uppgift ](assets/autosave-flow.png)](assets/using-autosave-freq-06.png)**har återställtsA.** Ett pågående arbetsformulär  **B.** Programmet har stängts  **C.** Programmet har startats om med dialogrutan Återställ osparad uppgift  **D.** Formuläret har återställts med originaldata

