---
title: Använda automatiskt sparade i AEM Forms-appen
description: Lär dig hur du använder funktionen Spara automatiskt i AEM Forms-appen för att undvika dataförlust.
contentOwner: sashanka
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
docset: aem65
exl-id: 1603eef1-d7c8-47d3-8cfa-55ec3eaadd64
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '294'
ht-degree: 0%

---

# Använda automatiskt sparade i AEM Forms-appen{#using-autosave-in-aem-forms-app}

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

1. Logga in på appen och navigera till **Inställningar > Allmänt**.
1. På skärmen Allmänt använder du **Spara automatiskt, frekvens** om du vill välja med vilka intervall appen ska spara de angivna data.
   [![Ställa in autosparfrekvens](assets/using-autosave-freq-07.png)](assets/using-autosave-freq-07-1.png)

1. När du startar om programmet och loggar in med samma användare uppmanas du att återställa uppgiften i dialogrutan Återställ osparad uppgift. Klicka **OK** i dialogrutan Återställ osparad uppgift för att fortsätta arbeta med den sparade uppgiften. Klicka **Avbryt** om du vill ta bort de sparade data som motsvarar den senast aktiverade autosparfunktionen och börja arbeta med en ny uppgift.

   När du klickar **OK**återställs aktiviteten med de data som motsvarar den senaste autosparfunktionen som utlöstes innan appen kraschade. Den innehåller formulärdata och alla bilagor som är associerade med uppgiften.
   [![Hämta en uppgift som återställts ](assets/autosave-flow.png)](assets/using-autosave-freq-06.png)**S.** Ett pågående formulär **B.** Appen stängdes med tvång **C.** Programmet har startats om med dialogrutan Återställ osparad uppgift **D.** Formuläret har återställts med ursprungliga data
