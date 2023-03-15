---
title: Exportera till CSV
seo-title: Export to CSV
description: Exportera information om sidorna till en CSV-fil på det lokala systemet
seo-description: Export information about your pages to a CSV file on your local system
uuid: 6eee607b-3510-4f6a-ba82-b27480a4fbe1
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: 7be506fb-f5c4-48dd-bec2-a3ea3ea19397
docset: aem65
exl-id: 18910143-f2f2-4cfe-88b9-651df90d9cb9
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '191'
ht-degree: 22%

---

# Exportera till CSV{#export-to-csv}

**Skapa CSV-rapport** Med kan du exportera information om sidorna till en CSV-fil på det lokala systemet.

* Den hämtade filen kallas `export.csv`
* Innehållet beror på de egenskaper du väljer.
* Du kan definiera banan tillsammans med exportens djup.

>[!NOTE]
>
>Hämtningsfunktionen och standarddestinationen för webbläsaren används.

I guiden **Skapa CSV-export** kan du välja:

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

Resultatet `export.csv` kan öppnas i Excel eller något annat kompatibelt program.

![etc-01](assets/etc-01.png)

Skapa **CSV-rapport** är tillgängligt när du bläddrar bland **Webbplatser** konsol (i listvyn): det är ett alternativ i **Skapa** nedrullningsbar meny:

![etc-02](assets/etc-02.png)

Så här skapar du en CSV-export:

1. Öppna konsolen **Sites** och navigera till önskad plats om det behövs.
1. I verktygsfältet väljer du **Skapa** och sedan **CSV-rapport** för att öppna guiden:

   ![etc-03](assets/etc-03.png)

1. Välj de egenskaper som ska exporteras.
1. Välj **Skapa**.
