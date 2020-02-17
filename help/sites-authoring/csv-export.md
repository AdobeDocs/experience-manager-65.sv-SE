---
title: Exportera till CSV
seo-title: Exportera till CSV
description: Exportera information om sidorna till en CSV-fil på det lokala systemet
seo-description: Exportera information om sidorna till en CSV-fil på det lokala systemet
uuid: 6eee607b-3510-4f6a-ba82-b27480a4fbe1
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: 7be506fb-f5c4-48dd-bec2-a3ea3ea19397
docset: aem65
translation-type: tm+mt
source-git-commit: 2d7492cdee9f7f730dfa6ad2ffae396b3a737b15

---


# Exportera till CSV{#export-to-csv}

**Med Skapa CSV-rapport** kan du exportera information om dina sidor till en CSV-fil på ditt lokala system.

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

Den resulterande `export.csv` filen kan öppnas i Excel eller något annat kompatibelt program.

![]() ![etc-01](assets/etc-01.png)

Alternativet Skapa **CSV-rapport** är tillgängligt när du bläddrar i **webbplatskonsolen** (i listvyn): det är ett alternativ i listrutan **Skapa** :

![etc-02](assets/etc-02.png)

Så här skapar du en CSV-export:

1. Öppna konsolen **Platser** och navigera till önskad plats om det behövs.
1. I verktygsfältet väljer du **Skapa** och sedan **CSV-rapport** för att öppna guiden:

   ![etc-03](assets/etc-03.png)

1. Välj de egenskaper som ska exporteras.
1. Välj **Skapa**.
