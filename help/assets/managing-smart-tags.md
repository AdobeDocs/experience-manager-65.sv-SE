---
title: Hantera smarta taggar och sökningar
description: Uppdatera eller ta bort felaktiga smarta taggar för att förbättra taggarnas relevans
contentOwner: AG
translation-type: tm+mt
source-git-commit: a39ee0f435dc43d2c2830b2947e91ffdcf11c7f6

---


# Hantera smarta taggar och sökningar {#manage-smart-tags-and-searches}

<!--
TBD: This article should be merged into a new, uber article for Smart Tags. Delete this article then. Cloud service article is merged.
-->

Du kan strukturera smarta taggar om du vill ta bort felaktiga taggar som kan ha tilldelats dina varumärkesbilder så att endast de mest relevanta taggarna visas.

Genom att moderera smarta taggar kan du också förbättra taggbaserade sökningar efter bilder genom att se till att bilden visas i sökresultaten för de mest relevanta taggarna. I grund och botten eliminerar det riskerna för att bilder som inte är relaterade visas i sökresultaten.

Du kan också tilldela en tagg en högre rankning för att öka dess relevans i förhållande till en bild. Om du befordrar en tagg för en bild ökar risken för att bilden visas i sökresultatet när en sökning utförs baserat på den aktuella taggen.

1. I rutan OmniSearch söker du efter resurser baserat på en tagg.
1. Granska sökresultaten för att identifiera en bild som du inte tycker är relevant för sökningen.
1. Markera bilden och tryck sedan på **[!UICONTROL Hantera taggar]** i verktygsfältet.
1. Granska taggarna på sidan **[!UICONTROL Hantera taggar]** . Om du inte vill att bilden ska sökas igenom baserat på en viss tagg markerar du taggen och trycker sedan på **[!UICONTROL Ta bort]** i verktygsfältet. Du kan också klicka/trycka på `X` symbolen som visas bredvid etiketten.
1. Om du vill tilldela en högre rankning till en tagg markerar du taggen och trycker på **[!UICONTROL Befordra]** i verktygsfältet. Taggen som du befordrar flyttas till **[!UICONTROL taggavsnittet]** .
1. Klicka/tryck på **[!UICONTROL Spara]** och sedan på/klicka på **[!UICONTROL OK]** för att stänga dialogrutan Slutfört.
1. Navigera till egenskapssidan för bilden. Observera att taggen som du befordrade har hög relevans och därför visas högre i sökresultaten.

## Förstå AEM-sökresultat med smarta taggar {#understandsearch}

Som standard kombineras söktermerna med en `AND` sats i AEM-sökningen. Om du använder smarta taggar ändras inte standardbeteendet. Om du använder smarta taggar läggs ytterligare en `OR` sats till för att hitta någon av söktermerna i de använda smarta taggarna. Du kan till exempel söka efter `woman running`. Resurser med bara `woman` eller bara `running` nyckelord i metadata visas inte som standard i sökresultaten. En resurs som du taggar med antingen `woman` eller `running` med smarta taggar visas i en sådan sökfråga. Sökresultaten är en kombination av

* resurser med `woman` och `running` nyckelord i metadata.

* resurser som är smarta taggade med något av nyckelorden.

Sökresultaten som matchar alla söktermer i metadatafält visas först, följt av sökresultaten som matchar någon av söktermerna i de smarta taggarna. I ovanstående exempel är den ungefärliga visningsordningen för sökresultat:

1. matchningar av `woman running` i de olika metadatafälten.
1. matchar `woman running` i smarta taggar.
1. matchar `woman` eller i `running` smarta taggar.
