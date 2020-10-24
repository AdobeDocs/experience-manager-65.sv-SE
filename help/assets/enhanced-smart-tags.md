---
title: Förbättrade smarta taggar
description: Förbättrade smarta taggar
contentOwner: AG
translation-type: tm+mt
source-git-commit: e124025295f29d6f3999dc52467301d48bceee75
workflow-type: tm+mt
source-wordcount: '1489'
ht-degree: 4%

---


# Förstå, använda och strukturera smarta taggar {#enhanced-smart-tags}

Organisationer som hanterar digitalt material använder i allt högre grad taxonomistyrd vokabulär i metadata. Det innehåller i själva verket en lista med nyckelord som anställda, partners och kunder vanligtvis använder för att referera till och söka efter digitala resurser i en viss klass. Genom att tagga resurser med taxonomistyrd vokabulär kan de enkelt identifieras och hämtas med taggbaserade sökningar.

Jämfört med naturtrogna språkordlistor kan taggning av digitala resurser baserat på företagsklonomi hjälpa dem att anpassa sig till företagets verksamhet och säkerställa att de mest relevanta resurserna visas i sökningar.

En biltillverkare kan t.ex. märka bilderna med modellnamn så att endast relevanta bilder visas när bilder av olika modeller söks igenom för att utforma en kampanj.

För att Smart Content Service ska kunna använda rätt taggar måste du utbilda den så att den känner igen din taxonomi. För att utbilda tjänsten måste du först strukturera en uppsättning resurser och taggar som bäst beskriver dessa resurser. Använd dessa taggar på materialet och kör ett utbildningsarbetsflöde för att hjälpa tjänsten att lära sig.

När en tagg har tränats och är klar kan tjänsten nu använda dessa taggar på resurser via ett taggningsarbetsflöde.

I bakgrunden använder Smart Content Service Adobe Sensei AI-ramverket för att träna sin bildigenkänningsalgoritm i er taggstruktur och affärsklonomi. Den här innehållsintelligensen används sedan för att tillämpa relevanta taggar på en annan uppsättning resurser.

Smart Content Service är en molntjänst som ligger i Adobe I/O. För att kunna använda den i [!DNL Adobe Experience Manager]måste systemadministratören integrera din [!DNL Experience Manager] distribution med Adobe I/O.

Här är sammanfattningsvis de viktigaste stegen för att använda tjänsten Smart Content:

* Onboarding
* Granska resurser och taggar (taxonomidefinition)
* Utbilda Smart Content Service
* Automatisk taggning

![flödesdiagram](assets/flowchart.gif)

## Förutsättningar {#prerequisites}

Innan du kan använda Smart Content Service måste du ha/se till/göra följande för att kunna integrera med Adobe I/O:

* Ett Adobe ID-konto som har administratörsbehörighet för organisationen.
* Att Smart Content Service är aktiverad för din organisation.
* Grundpaketet för smarta innehållstjänster kan endast läggas till i en distribution där ett [!DNL Sites] baspaket och [!DNL Assets] tillägg har licensierats.

## Introduktion till {#onboarding}

Tjänsten Smart Content Service kan köpas som tillägg till [!DNL Experience Manager]. När du har köpt programmet skickas ett e-postmeddelande till administratören för din organisation med en länk till Adobe I/O.

Administratören kan följa länken för att integrera Smart Content Service med [!DNL Experience Manager]. Information om hur du integrerar tjänsten med [!DNL Experience Manager Assets]finns i [Konfigurera smarta taggar](config-smart-tagging.md).

Startprocessen är klar när administratören konfigurerar tjänsten och lägger till användare i [!DNL Experience Manager].

>[!NOTE]
>
>Om du använder [!DNL Experience Manager] 6.3 eller en tidigare version och behöver taggar för dina resurser läser du i [Smarta taggar](https://helpx.adobe.com/experience-manager/6-3/assets/using/touch-ui-smart-tags.html). Smarta taggar använder inte de senaste AI-funktionerna och är därför mindre exakta än den förbättrade smarta taggningstjänsten.

## Granska resurser och taggar {#reviewing-assets-and-tags}

Det första du vill göra när du är ombord är att identifiera en uppsättning taggar som bäst beskriver bilderna i ditt företags sammanhang.

Granska sedan bilderna för att identifiera en uppsättning bilder som bäst motsvarar din produkt för ett visst affärsbehov. Se till att resurserna i din förvaltade uppsättning följer utbildningsriktlinjerna [för](/help/assets/config-smart-tagging.md#training-the-smart-content-service)Smart Content Service.

Lägg till resurserna i en mapp och använd taggarna på varje resurs från egenskapssidan. Kör sedan utbildningsarbetsflödet i den här mappen. Den välstrukturerade uppsättningen resurser gör det möjligt för Smart Content Service att effektivt utbilda fler resurser med hjälp av dina taxonomidefinitioner.

>[!NOTE]
>
>1. Utbildning är en oåterkallelig process. Adobe rekommenderar att du granskar taggarna i den välstrukturerade resursuppsättningen innan du utbildar Smart Content Service på taggarna.
>1. Innan du utbildar dig för en tagg ska du läsa [Riktlinjer](/help/assets/config-smart-tagging.md#training-the-smart-content-service)för utbildning i smarta innehållstjänster.
>1. När du utbildar Smart Content Service för första gången rekommenderar Adobe att du utbildar den på minst två distinkta taggar.


## Förstå [!DNL Experience Manager] sökresultat med smarta taggar {#understandsearch}

Som standard kombineras söktermerna med en [!DNL Experience Manager] `AND` sats i sökningen. Om du använder smarta taggar ändras inte standardbeteendet. Om du använder smarta taggar läggs ytterligare en `OR` sats till för att hitta någon av söktermerna i de använda smarta taggarna. For example, consider searching for `woman running`. Resurser med bara `woman` eller bara `running` nyckelord i metadata visas inte som standard i sökresultaten. En resurs som du taggar med antingen `woman` eller `running` med smarta taggar visas i en sådan sökfråga. Sökresultaten är en kombination av

* resurser med `woman` och `running` nyckelord i metadata.

* resurser som är smarta taggade med något av nyckelorden.

Sökresultaten som matchar alla söktermer i metadatafält visas först, följt av sökresultaten som matchar någon av söktermerna i de smarta taggarna. I ovanstående exempel är den ungefärliga visningsordningen för sökresultat:

1. matchningar av `woman running` i de olika metadatafälten.
1. matchar `woman running` i smarta taggar.
1. matchar `woman` eller i `running` smarta taggar.

>[!CAUTION]
>
>Om Lucene-indexeringen görs från [!DNL Adobe Experience Manager] fungerar inte sökningen som baseras på smarta taggar som förväntat.

## Tagga resurser automatiskt {#tagging-assets-automatically}

När du har utbildat tjänsten för smart innehåll kan du utlösa taggningsarbetsflödet för att automatiskt tillämpa lämpliga taggar på en annan uppsättning med liknande resurser.

Du kan köra taggningsarbetsflödet periodiskt eller när det behövs.

>[!NOTE]
>
>Arbetsflödet för taggning körs både på resurser och mappar.

### Periodisk taggning {#periodic-tagging}

Du kan aktivera tjänsten Smart Content Service för att regelbundet tagga resurser i en mapp. Öppna egenskapssidan för resursmappen, markera **[!UICONTROL Enable Smart Tags]** under **[!UICONTROL Details]** fliken och spara ändringarna.

När det här alternativet har valts för en mapp taggar tjänsten Smart Content Service automatiskt resurserna i mappen. Som standard körs taggningsarbetsflödet varje dag kl. 12.00.

### On-demand-taggning {#on-demand-tagging}

Du kan utlösa taggningsarbetsflödet från arbetsflödeskonsolen eller från tidslinjen för att omedelbart tagga dina resurser.

>[!NOTE]
>
>Om du kör taggningsarbetsflödet från tidslinjen kan du använda taggar på högst 15 resurser i taget.

#### Tagga resurser från arbetsflödeskonsolen {#tagging-assets-from-the-workflow-console}

1. In [!DNL Experience Manager] interface, go to **[!UICONTROL Tools]** > **[!UICONTROL Workflow]** > **[!UICONTROL Models]**.
1. From the **[!UICONTROL Workflow Models]** page, select the **[!UICONTROL DAM Smart Tags Assets]** workflow and then click **[!UICONTROL Start Workflow]** from the toolbar.

   ![dam_smart_tag_workflow](assets/dam_smart_tag_workflow.png)

1. I **[!UICONTROL Run Workflow]** dialogrutan bläddrar du till nyttolastmappen som innehåller resurser som du vill använda dina taggar på automatiskt.
1. Ange en rubrik för arbetsflödet och en valfri kommentar. Klicka på **[!UICONTROL Run]**.

   ![tagging_dialog](assets/tagging_dialog.png)

   Navigera till resursmappen och granska taggarna för att kontrollera om Smart Content Service taggade dina resurser på rätt sätt.

#### Tagga resurser från tidslinjen {#tagging-assets-from-the-timeline}

1. I [!DNL Assets] användargränssnittet väljer du den mapp som innehåller resurser eller specifika resurser som du vill använda smarta taggar på.
1. I det övre vänstra hörnet öppnar du **[!UICONTROL Timeline]**.
1. Öppna funktionsmakron längst ned i den vänstra sidopanelen och klicka på **[!UICONTROL Start Workflow]**.

   ![start_workflow](assets/start_workflow.png)

1. Markera **[!UICONTROL DAM Smart Tag Assets]** arbetsflödet och ange en rubrik för arbetsflödet.
1. Klicka på **[!UICONTROL Start]**. Arbetsflödet använder dina taggar på resurser. Navigera till resursmappen och granska taggarna för att kontrollera om Smart Content Service taggade dina resurser på rätt sätt.

>[!NOTE]
>
>I de efterföljande taggningscyklerna märks bara de ändrade resurserna igen med nyligen tränade taggar. Även oförändrade resurser taggas om mellanrummet mellan den sista och den aktuella taggningscykeln för taggningsarbetsflödet överstiger 24 timmar. För periodiska taggningsarbetsflöden taggas oförändrade resurser när tidsintervallet överskrider sex månader.

## Kuratera eller moderera de använda smarta taggarna {#manage-smart-tags}

Du kan strukturera smarta taggar om du vill ta bort felaktiga taggar som kan ha tilldelats dina varumärkesbilder så att endast de mest relevanta taggarna visas.

Genom att moderera smarta taggar kan du också förbättra taggbaserade sökningar efter bilder genom att se till att bilden visas i sökresultaten för de mest relevanta taggarna. I grund och botten eliminerar det riskerna för att bilder som inte är relaterade visas i sökresultaten.

Du kan också tilldela en tagg en högre rankning för att öka dess relevans i förhållande till en bild. Om du befordrar en tagg för en bild ökar risken för att bilden visas i sökresultatet när en sökning utförs baserat på den aktuella taggen.

1. Sök efter resurser baserade på en tagg i rutan Omnissearch.
1. Inspect sökresultaten för att identifiera en bild som du inte tycker är relevant för sökningen.
1. Select the image, and click **[!UICONTROL Manage Tags]** from the toolbar.
1. Granska taggarna från **[!UICONTROL Manage Tags]** sidan. Om du inte vill att bilden ska genomsökas baserat på en viss tagg, markerar du taggen och klickar sedan på **[!UICONTROL Delete]** i verktygsfältet. Du kan också klicka på `x` symbolen som visas bredvid ett märkord.
1. Om du vill tilldela en tagg en högre rankning markerar du taggen och klickar på **[!UICONTROL Promote]** i verktygsfältet. Taggen som du höjer upp flyttas till **[!UICONTROL Tags]** avsnittet.
1. Click **[!UICONTROL Save]** and then click **[!UICONTROL OK]**
1. Navigera till **[!UICONTROL Properties]** sidan för bilden. Observera att taggen som du befordrade är mer relevant och visas tidigare i sökresultatet.

## Tips och begränsningar {#tips-best-practices-limitations}

* Användningen av smarta innehållstjänster är begränsad till upp till 2 miljoner taggade bilder per år. Alla duplicerade bilder som bearbetas och taggas räknas som taggade bilder.
* Om du kör taggningsarbetsflödet från tidslinjen kan du använda taggar på högst 15 resurser i taget.
