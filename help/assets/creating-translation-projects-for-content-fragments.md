---
title: Skapa översättningsprojekt för innehållsfragment
seo-title: Skapa översättningsprojekt för innehållsfragment
description: Lär dig hur du översätter innehållsfragment.
seo-description: Lär dig hur du översätter innehållsfragment.
uuid: 23176e70-4003-453c-af25-6499a5ed3f6d
contentOwner: heimoz
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: managing-assets
content-type: reference
discoiquuid: d2decc31-a04b-4a8e-bb19-65f21cf7107e
feature: Innehållsfragment
role: User, Admin
exl-id: 19bb58da-8220-404e-bddb-34be94a3a7d7
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '931'
ht-degree: 3%

---

# Skapa översättningsprojekt för innehållsfragment {#creating-translation-projects-for-content-fragments}

Förutom resurser har Adobe Experience Manager (AEM) Assets stöd för språkkopieringsarbetsflöden för [innehållsfragment](/help/assets/content-fragments/content-fragments.md) (inklusive variationer). Ingen ytterligare optimering krävs för att köra språkkopieringsarbetsflöden på innehållsfragment. I varje arbetsflöde skickas hela innehållsfragmentet för översättning.

De typer av arbetsflöden som du kan köra på innehållsfragment liknar exakt de arbetsflödestyper som du kör för resurser. Alternativen som är tillgängliga för varje arbetsflödestyp matchar alternativen som är tillgängliga under motsvarande arbetsflödestyper för resurser.

Du kan köra följande typer av arbetsflöden för språkkopiering på innehållsfragment:

**Skapa och översätta**

I det här arbetsflödet kopieras innehållsfragment som ska översättas till språkroten för det språk som du vill översätta till. Beroende på vilka alternativ du väljer skapas dessutom ett översättningsprojekt för innehållsfragmenten i projektkonsolen. Beroende på inställningarna kan översättningsprojektet startas manuellt eller köras automatiskt så fort översättningsprojektet skapas.

**Uppdatera språkkopior**

När källinnehållets fragment uppdateras eller ändras kräver motsvarande språk-/språkspecifika innehållsfragment omöversättning. Arbetsflödet för att uppdatera språkkopior översätter ytterligare en grupp innehållsfragment och inkluderar det i en språkkopia för en viss språkinställning. I det här fallet läggs de översatta innehållsfragmenten till i målmappen som redan innehåller tidigare översatta innehållsfragment.

## Skapa och översätta arbetsflöde {#create-and-translate-workflow}

Arbetsflödet Skapa och översätt innehåller följande alternativ. Procedurstegen som är kopplade till varje alternativ liknar dem som är kopplade till motsvarande alternativ för tillgångar.

* Skapa endast struktur: Anvisningar om procedurer finns i [Skapa struktur endast för resurser](translation-projects.md#create-structure-only).
* Skapa ett nytt översättningsprojekt: Anvisningar om procedurer finns i [Skapa ett nytt översättningsprojekt för resurser](translation-projects.md#create-a-new-translation-project).
* Lägg till i befintligt översättningsprojekt: Om du vill veta mer om procedurer läser du i [Lägg till i det befintliga översättningsprojektet för resurser](translation-projects.md#add-to-existing-translation-project).

## Uppdatera arbetsflödet för språkkopior {#update-language-copies-workflow}

Arbetsflödet för att uppdatera språkkopior innehåller följande alternativ. Procedurstegen som är kopplade till varje alternativ liknar dem som är kopplade till motsvarande alternativ för tillgångar.

* Skapa ett nytt översättningsprojekt: Anvisningar om procedurer finns i [Skapa ett nytt översättningsprojekt för resurser](translation-projects.md#create-a-new-translation-project) (uppdatera arbetsflöde).
* Lägg till i befintligt översättningsprojekt: Anvisningar om procedurer finns i [Lägg till i befintligt översättningsprojekt för resurser](translation-projects.md#add-to-existing-translation-project) (uppdateringsarbetsflöde).

Du kan också skapa tillfälliga språkkopior för fragment som liknar det sätt som du skapar tillfälliga kopior för resurser. Mer information finns i [Skapa tillfälliga språkkopior för resurser](translation-projects.md#creating-temporary-language-copies).

## Översätta blandade mediefragment {#translating-mixed-media-fragments}

Med AEM kan du översätta innehållsfragment som innehåller olika typer av medieresurser och samlingar. Om du översätter ett innehållsfragment som innehåller textbundna resurser lagras de översatta kopiorna av dessa resurser under målspråkets rot.

Om innehållsfragmentet innehåller en samling, översätts resurserna i samlingen tillsammans med innehållsfragmentet. De översatta kopiorna av resurserna lagras i rätt målspråksrot på en plats som matchar den fysiska platsen för källresurserna under källspråkets rot.

Om du vill kunna översätta innehållsfragment som innehåller blandade media måste du först redigera standardöversättningsramverket för att aktivera översättning av textbundna resurser och samlingar som är kopplade till innehållsfragment.

1. Klicka/tryck på AEM logotyp och navigera till **[!UICONTROL Tools > Deployment > Cloud Services]**.
1. Gå till **[!UICONTROL Translation Integration]** under **[!UICONTROL Adobe Marketing Cloud]** och klicka/tryck på **[!UICONTROL Show Configurations]**.

   ![chlimage_1-444](assets/chlimage_1-444.png)

1. Öppna sidan **[!UICONTROL Default configuration]** genom att klicka/trycka på **[!UICONTROL Default configuration (Translation Integration configuration)]** i listan över tillgängliga konfigurationer.

   ![chlimage_1-445](assets/chlimage_1-445.png)

1. Klicka på **[!UICONTROL Edit]** i verktygsfältet för att visa dialogrutan **[!UICONTROL Translation Config]**.

   ![chlimage_1-446](assets/chlimage_1-446.png)

1. Navigera till fliken **[!UICONTROL Assets]** och välj **[!UICONTROL Inline Media Assets and Associated Collections]** i listan **[!UICONTROL Translate Content Fragment Assets]**. Klicka/tryck på **[!UICONTROL OK]** för att spara ändringarna.

   ![chlimage_1-447](assets/chlimage_1-447.png)

1. Öppna ett innehållsfragment i den engelska rotmappen.

   ![chlimage_1-448](assets/chlimage_1-448.png)

1. Klicka/tryck på ikonen **[!UICONTROL Insert Asset]**.

   ![chlimage_1-449](assets/chlimage_1-449.png)

1. Infoga en resurs i innehållsfragmentet.

   ![infoga resurs i innehållsfragment](assets/column-view.png)

1. Klicka/tryck på ikonen **[!UICONTROL Associate Content]**.

   ![chlimage_1-451](assets/chlimage_1-451.png)

1. Klicka/tryck på **[!UICONTROL Associate Content]**.

   ![chlimage_1-452](assets/chlimage_1-452.png)

1. Markera en samling och ta med den i innehållsfragmentet. Klicka/tryck på **[!UICONTROL Save]**.

   ![chlimage_1-453](assets/chlimage_1-453.png)

1. Markera innehållsfragmentet och klicka/tryck på ikonen **[!UICONTROL GlobalNav]**.
1. Välj **[!UICONTROL References]** på menyn för att visa rutan **[!UICONTROL References]**.

   ![chlimage_1-454](assets/chlimage_1-454.png)

1. Klicka/tryck på **[!UICONTROL Language Copies]** under **[!UICONTROL Copies]** för att visa språkkopiorna.

   ![chlimage_1-455](assets/chlimage_1-455.png)

1. Klicka/tryck på **[!UICONTROL Create & Translate]** längst ned på panelen för att visa dialogrutan **[!UICONTROL Create & Translate]**.

   ![chlimage_1-456](assets/chlimage_1-456.png)

1. Välj målspråk i listan **[!UICONTROL Target Languages]**.

   ![chlimage_1-457](assets/chlimage_1-457.png)

1. Välj översättningsprojekttyp i listan **[!UICONTROL Project]**.

   ![chlimage_1-458](assets/chlimage_1-458.png)

1. Ange projektets titel i rutan **[!UICONTROL Project Title]** och klicka/tryck sedan på **Skapa**.

   ![chlimage_1-459](assets/chlimage_1-459.png)

1. Navigera till **[!UICONTROL Projects]**-konsolen och öppna projektmappen för översättningsprojektet som du skapade.

   ![chlimage_1-460](assets/chlimage_1-460.png)

1. Klicka/tryck på projektpanelen för att öppna sidan med projektinformation.

   ![chlimage_1-461](assets/chlimage_1-461.png)

1. Kontrollera antalet resurser som ska översättas i rutan Översättningsjobb.
1. Starta översättningsjobbet från **[!UICONTROL Translation Job]**-panelen.

   ![chlimage_1-462](assets/chlimage_1-462.png)

1. Klicka på ellipserna längst ned i rutan Översättningsjobb för att visa översättningsjobbets status.

   ![chlimage_1-463](assets/chlimage_1-463.png)

1. Klicka på/tryck på innehållsfragmentet för att kontrollera sökvägen för de översatta associerade resurserna.

   ![chlimage_1-464](assets/chlimage_1-464.png)

1. Granska språkkopian för samlingen i konsolen Samlingar.

   ![chlimage_1-465](assets/chlimage_1-465.png)

   Observera att endast innehållet i samlingen översätts. Själva samlingen är inte översatt.

1. Navigera till sökvägen för den översatta associerade resursen. Observera att den översatta resursen lagras under målspråkets rot.

   ![chlimage_1-466](assets/chlimage_1-466.png)

1. Navigera till resurserna i samlingen som är översatta med innehållsfragmentet. Observera att de översatta kopiorna av resurserna lagras i rätt målspråksrot.

   ![chlimage_1-467](assets/chlimage_1-467.png)

   >[!NOTE]
   >
   >Procedurerna för att lägga till ett innehållsfragment i ett befintligt projekt eller för att utföra uppdateringsarbetsflöden liknar motsvarande procedurer för resurser. Vägledning om dessa förfaranden finns i de förfaranden som beskrivs för tillgångar.
