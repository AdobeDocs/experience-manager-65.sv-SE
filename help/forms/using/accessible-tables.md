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
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Skapa hjälpmedelsanpassade komplexa tabeller i HTML5-formulär {#create-accessible-complex-tables-in-html-forms}

Standardimplementeringen av tabeller i HTML5-formulär använder HTML DIV-element för att återge en tabell. Återgivning innebär att ARIA-roller används för att uppfylla tillgänglighetskraven.

För att undvika tillgänglighetsproblem med skärmläsare som inte har fullt stöd för de ARIA-roller som används med datatabeller, erbjuder HTML5-formulär en alternativ återgivning för tabellerna. Tabellerna är baserade på det nya tabellformatet som introducerades i Designer och som även stöder:

* Radrubriker
* Radomfång

Om du vill använda det nya formatet i HTML5-formulär markerar du tabellen som komplex. Om du vill markera tabellen som komplex lägger du till `extras` -taggen i XML-källan för tabelldelformuläret enligt följande:

```
</extras>
 <text name="complexTable">1</text>
 </extras>
```

Tabellerna som markeras som *complexTable* följer den inbyggda HTML-återgivningen och ger bättre stöd för tillgänglighet för vissa skärmläsare.  Om du vill skapa ett radintervall markerar du flera celler i en tabell i följd i samma kolumn, högerklickar på markeringen och klickar sedan på **[!UICONTROL Sammanfoga celler]**.

*****Obs! Det går bara att skapa ett radintervall för celler längst till vänster.*

Om du vill markera en rad som en radrubrik markerar du alla celler i raden, högerklickar på markeringen och klickar sedan på **[!UICONTROL Markera rubrik]**.

Om du vill markera en cell som kolumnrubrik markerar du en cell i kolumnen, högerklickar på markeringen och klickar sedan på **[!UICONTROL Markera rubrik]**.

Begränsningar i det nya *AccessibleTable* -formatet:

* Brist på stöd för utökningsbara fält om rowspan används i tabellen
* Inget stöd för kapslade tabeller (tabeller i tabellceller)
* Stödet för radutvidgning är begränsat till rubrikrader och rubrikceller
* Stödet begränsas till vanliga tabeller
* Inget stöd för dataförifyllningar i tabeller med radutvidgning > 1

