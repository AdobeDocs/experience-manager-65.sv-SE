---
title: Skapa hjälpmedelsanpassade komplexa tabeller i HTML5-formulär
seo-title: Skapa hjälpmedelsanpassade komplexa tabeller i HTML5-formulär
description: Lär dig hur du skapar tillgängliga tabeller i HTML5-formulär.
seo-description: Lär dig hur du skapar tillgängliga tabeller i HTML5-formulär.
uuid: e52562d2-4dc3-4359-9dbb-c18614921808
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 3504afe1-abf5-4fbf-a0d2-e093361764bd
feature: Mobile Forms
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '285'
ht-degree: 0%

---


# Skapa hjälpmedelsanpassade komplexa tabeller i HTML5-formulär {#create-accessible-complex-tables-in-html-forms}

Standardimplementeringen av tabeller i HTML5 Forms använder HTML DIV-element för att återge en tabell. Återgivning innebär att ARIA-roller används för att uppfylla tillgänglighetskraven.

För att undvika tillgänglighetsproblem med skärmläsare som inte har fullt stöd för de ARIA-roller som används med datatabeller, erbjuder HTML5 Forms en alternativ återgivning för tabellerna. Tabellerna är baserade på det nya tabellformatet som introducerades i Designer och som även stöder:

* Radrubriker
* Radomfång

Om du vill använda det nya formatet i HTML5 Forms markerar du tabellen som komplex. Om du vill markera tabellen som komplex lägger du till taggen `extras` i XML-källan för tabelldelformuläret enligt följande:

```xml
</extras>
 <text name="complexTable">1</text>
 </extras>
```

Tabellerna som är markerade som *complexTable* följer den inbyggda HTML-återgivningen och ger bättre stöd för tillgänglighet för vissa skärmläsare.  Om du vill skapa ett radintervall markerar du celler i en tabell i följd i samma kolumn, högerklickar på markeringen och klickar sedan på **[!UICONTROL Merge Cells]**.

>[!NOTE]
>
>Det går bara att skapa ett radintervall för celler längst till vänster.

Om du vill markera en rad som radrubrik markerar du alla celler i raden, högerklickar på markeringen och klickar sedan på **[!UICONTROL Mark Header]**.

Om du vill markera en cell som kolumnrubrik markerar du en cell i kolumnen, högerklickar på markeringen och klickar sedan på **[!UICONTROL Mark Header]**.

Begränsningar i det nya *AccessibleTable*-formatet:

* Brist på stöd för utökningsbara fält om rowspan används i tabellen
* Inget stöd för kapslade tabeller (tabeller i tabellceller)
* Stödet för radutvidgning är begränsat till rubrikrader och rubrikceller
* Stödet begränsas till vanliga tabeller
* Inget stöd för dataförifyllningar i tabeller med radutvidgning > 1

