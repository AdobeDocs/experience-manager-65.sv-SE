---
title: Tips för att minimera databastillväxt
description: I långvariga processer lagras processdata i AEM. Tillväxten i AEM kan minimeras med några enkla processkonfigurations- och produktkonfigurationsstrategier.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_aem_forms_database
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: f64efb06-815a-4608-ba1c-39e22f344ebb
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '408'
ht-degree: 0%

---

# Tips för att minimera databastillväxt {#tips-for-minimizing-database-growth}

I långvariga processer lagras processdata i AEM. Tillväxten i AEM kan minimeras med några enkla processkonfigurations- och produktkonfigurationsstrategier.

## Processdesigntips {#process-design-tips}

Använd kortvariga processer när det är möjligt. Kortlivade processer lagrar inte processdata i databasen. Nackdelen med kortlivade processer är att deras status och tillstånd inte spåras i administrationskonsolen och att det inte finns någon historik över processen.

Vissa tjänståtgärder, till exempel Tilldela uppgift (användartjänst), kräver att de används i långvariga processer. I det här fallet kan du segmentera processen i flera underprocesser och göra dem kortvariga när det är möjligt. Om du använder den här strategin bör kortlivade underprocesser hantera stora dataobjekt, till exempel dokumentvärden.

Använd variabler sparsamt. När du använder långvariga processer tilldelas utrymme för varje processinstans i databasen för varje variabel i processen. Strategisk användning av variabler kan spara mycket utrymme. Du kan till exempel skriva över variabelvärden när gamla värden inte längre behövs i processen. Och ta bort alla variabler som du har skapat och inte använder. Du kan validera processen för att hitta oanvända variabler.

Använd enkla variabeltyper (till exempel sträng eller int) och undvik att använda komplexa variabeltyper när det är möjligt. Databasutrymme tilldelas för variabler även när de inte innehåller något värde. Komplexa variabler kräver vanligtvis mer utrymme än enkla.

## Tips för produktadministration {#product-administration-tips}

Använd global dokumentlagring (GDS) effektivt. GDS-katalogen på Forms Server används för att lagra bland annat filer som skickas till tjänster som är en del av AEM formulär i processer. För att förbättra prestandan lagras mindre dokument i stället i minnet och sparas i databasen.

administrationskonsolen visar egenskapen Maximal intern dokumentstorlek för standarddokument för att konfigurera den maximala storleken på dokument som lagras i minnet och som finns kvar i databasen. (Se [Konfigurera allmänna inställningar AEM formulär](/help/forms/using/admin-help/configure-general-aem-forms-settings.md#configure-general-aem-forms-settings).) Om du anger den här egenskapen till ett lågt värde sparas de flesta dokument i GDS-katalogen i stället för i databasen. Fördelen är att du enklare kan ta bort filerna när de inte längre behövs när de lagras i GDS-katalogen.
