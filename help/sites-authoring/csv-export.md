---
title: Exportera till CSV
description: Exportera information om sidorna till en CSV-fil på det lokala systemet
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
docset: aem65
exl-id: 18910143-f2f2-4cfe-88b9-651df90d9cb9
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User,Admin,Architect,Developer
source-git-commit: 9a3008553b8091b66c72e0b6c317573b235eee24
workflow-type: tm+mt
source-wordcount: '192'
ht-degree: 6%

---

# Exportera till CSV{#export-to-csv}

**Skapa CSV-rapport** Med kan du exportera information om sidorna till en CSV-fil på det lokala systemet.

* Den hämtade filen anropas `export.csv`
* Innehållet beror på de egenskaper du väljer.
* Du kan definiera banan tillsammans med exportens djup.

>[!NOTE]
>
>Hämtningsfunktionen och standarddestinationen för webbläsaren används.

The **Skapa CSV-export** kan du välja:

* Egenskaper att exportera
   * Metadata
      * Namn
      * Ändrad
      * Publicerad
      * Mall
      * Arbetsflöde
   * Översättning
      * Översatt
   * Analyser
      * Sidvyer
      * Unika besökare
      * Tid på sidan
* Djup
   * Överordnad sökväg
   * Endast direktunderordnade
   * Ytterligare nivåer av barn
   * Nivåer

Resultatet `export.csv` filen kan öppnas i Excel eller något annat kompatibelt program.

![etc-01](assets/etc-01.png)

Skapa **CSV-rapport** är tillgängligt när du bläddrar bland **Webbplatser** konsol (i listvyn): det är ett alternativ för **Skapa** nedrullningsbar meny:

![etc-02](assets/etc-02.png)

Så här skapar du en CSV-export:

1. Öppna **Webbplatser** navigera till önskad plats om det behövs.
1. I verktygsfältet väljer du **Skapa** och sedan **CSV-rapport** för att öppna guiden:

   ![etc-03](assets/etc-03.png)

1. Välj de egenskaper som ska exporteras.
1. Välj **Skapa**.
