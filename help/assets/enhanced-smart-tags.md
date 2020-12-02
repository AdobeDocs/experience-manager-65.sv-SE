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

Smart Content Service är en molntjänst som tillhandahålls av Adobe I/O. Om du vill använda den i [!DNL Adobe Experience Manager] måste systemadministratören integrera din [!DNL Experience Manager]-distribution med Adobe I/O.

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
* Grundpaketet för smarta innehållstjänster kan endast läggas till i en distribution där ett [!DNL Sites]-baspaket och [!DNL Assets]-tillägg har licensierats.

## Introduktion till {#onboarding}

Tjänsten Smart Content Service kan köpas som tillägg till [!DNL Experience Manager]. När du har köpt programmet skickas ett e-postmeddelande med en länk till Adobe I/O till administratören i organisationen.

Administratören kan följa länken för att integrera Smart Content Service med [!DNL Experience Manager]. Information om hur du integrerar tjänsten med [!DNL Experience Manager Assets] finns i [Konfigurera smarta taggar](config-smart-tagging.md).

Startprocessen är klar när administratören konfigurerar tjänsten och lägger till användare i [!DNL Experience Manager].

>[!NOTE]
>
>Om du använder [!DNL Experience Manager] 6.3 eller tidigare version och behöver en taggningstjänst för dina resurser kan du läsa [Smarta taggar](https://helpx.adobe.com/experience-manager/6-3/assets/using/touch-ui-smart-tags.html). Smarta taggar använder inte de senaste AI-funktionerna och är därför mindre exakta än den förbättrade smarta taggningstjänsten.

## Granska resurser och taggar {#reviewing-assets-and-tags}

Det första du vill göra när du är ombord är att identifiera en uppsättning taggar som bäst beskriver bilderna i ditt företags sammanhang.

Granska sedan bilderna för att identifiera en uppsättning bilder som bäst motsvarar din produkt för ett visst affärsbehov. Kontrollera att resurserna i din aktuella uppsättning uppfyller [riktlinjerna för utbildning i smarta innehållstjänster](/help/assets/config-smart-tagging.md#training-the-smart-content-service).

Lägg till resurserna i en mapp och använd taggarna på varje resurs från egenskapssidan. Kör sedan utbildningsarbetsflödet i den här mappen. Den välstrukturerade uppsättningen resurser gör det möjligt för Smart Content Service att effektivt utbilda fler resurser med hjälp av dina taxonomidefinitioner.

>[!NOTE]
>
>1. Utbildning är en oåterkallelig process. Adobe rekommenderar att du granskar taggarna i den välstrukturerade resursuppsättningen innan du utbildar Smart Content Service på taggarna.
>1. Innan du utbildar dig för en tagg ska du läsa [Riktlinjer för utbildning i smarta innehållstjänster](/help/assets/config-smart-tagging.md#training-the-smart-content-service).
>1. När du utbildar Smart Content Service för första gången rekommenderar Adobe att du utbildar den på minst två distinkta taggar.


## Förstå [!DNL Experience Manager]-sökresultat med smarta taggar {#understandsearch}

Som standard kombineras söktermerna i [!DNL Experience Manager]-sökningen med en `AND`-sats. Om du använder smarta taggar ändras inte standardbeteendet. Om du använder smarta taggar läggs ytterligare en `OR`-sats till för att hitta någon av söktermerna i de använda smarta taggarna. Du kan till exempel söka efter `woman running`. Resurser med bara `woman` eller bara `running` nyckelord i metadata visas inte som standard i sökresultaten. En resurs som är taggad med antingen `woman` eller `running` med smarta taggar visas i en sådan sökfråga. Sökresultaten är en kombination av

* resurser med `woman` och `running` nyckelord i metadata.

* resurser som är smarta taggade med något av nyckelorden.

Sökresultaten som matchar alla söktermer i metadatafält visas först, följt av sökresultaten som matchar någon av söktermerna i de smarta taggarna. I ovanstående exempel är den ungefärliga visningsordningen för sökresultat:

1. matchar `woman running` i de olika metadatafälten.
1. matchar `woman running` i smarta taggar.
1. matchar `woman` eller `running` i smarta taggar.

>[!CAUTION]
>
>Om Lucene-indexeringen görs av [!DNL Adobe Experience Manager] fungerar inte sökningen baserat på smarta taggar som förväntat.

## Tagga resurser automatiskt {#tagging-assets-automatically}

När du har utbildat tjänsten för smart innehåll kan du utlösa taggningsarbetsflödet för att automatiskt tillämpa lämpliga taggar på en annan uppsättning med liknande resurser.

Du kan köra taggningsarbetsflödet periodiskt eller när det behövs.

>[!NOTE]
>
>Arbetsflödet för taggning körs både på resurser och mappar.

### Periodisk taggning {#periodic-tagging}

Du kan aktivera tjänsten Smart Content Service för att regelbundet tagga resurser i en mapp. Öppna egenskapssidan för resursmappen, välj **[!UICONTROL Enable Smart Tags]** under fliken **[!UICONTROL Details]** och spara ändringarna.

När det här alternativet har valts för en mapp taggar tjänsten Smart Content Service automatiskt resurserna i mappen. Som standard körs taggningsarbetsflödet varje dag kl. 12.00.

### On demand-taggning {#on-demand-tagging}

Du kan utlösa taggningsarbetsflödet från arbetsflödeskonsolen eller från tidslinjen för att omedelbart tagga dina resurser.

>[!NOTE]
>
>Om du kör taggningsarbetsflödet från tidslinjen kan du använda taggar på högst 15 resurser i taget.

#### Tagga resurser från arbetsflödeskonsolen {#tagging-assets-from-the-workflow-console}

1. I gränssnittet [!DNL Experience Manager] går du till **[!UICONTROL Tools]** > **[!UICONTROL Workflow]** > **[!UICONTROL Models]**.
1. På sidan **[!UICONTROL Workflow Models]** väljer du arbetsflödet för **[!UICONTROL DAM Smart Tags Assets]** och klickar sedan på **[!UICONTROL Start Workflow]** i verktygsfältet.

   ![dam_smart_tag_workflow](assets/dam_smart_tag_workflow.png)

1. I dialogrutan **[!UICONTROL Run Workflow]** bläddrar du till nyttolastmappen som innehåller resurser som du vill använda dina taggar på automatiskt.
1. Ange en rubrik för arbetsflödet och en valfri kommentar. Klicka på **[!UICONTROL Run]**.

   ![tagging_dialog](assets/tagging_dialog.png)

   Navigera till resursmappen och granska taggarna för att kontrollera om Smart Content Service taggade dina resurser på rätt sätt.

#### Tagga resurser från tidslinjen {#tagging-assets-from-the-timeline}

1. I [!DNL Assets]-användargränssnittet väljer du den mapp som innehåller resurser eller specifika resurser som du vill använda smarta taggar på.
1. Öppna **[!UICONTROL Timeline]** i det övre vänstra hörnet.
1. Öppna funktionsmakron längst ned i den vänstra sidopanelen och klicka på **[!UICONTROL Start Workflow]**.

   ![start_workflow](assets/start_workflow.png)

1. Välj arbetsflödet **[!UICONTROL DAM Smart Tag Assets]** och ange en rubrik för arbetsflödet.
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
1. Markera bilden och klicka på **[!UICONTROL Manage Tags]** i verktygsfältet.
1. Granska taggarna på sidan **[!UICONTROL Manage Tags]**. Om du inte vill att bilden ska sökas igenom baserat på en viss tagg markerar du taggen och klickar sedan på **[!UICONTROL Delete]** i verktygsfältet. Du kan också klicka på symbolen `x` som visas bredvid en tagg.
1. Om du vill tilldela en tagg en högre rankning markerar du taggen och klickar på **[!UICONTROL Promote]** i verktygsfältet. Taggen som du befordrar flyttas till avsnittet **[!UICONTROL Tags]**.
1. Klicka på **[!UICONTROL Save]** och sedan på **[!UICONTROL OK]**
1. Navigera till sidan **[!UICONTROL Properties]** för bilden. Observera att taggen som du befordrade är mer relevant och visas tidigare i sökresultatet.

## Tips och begränsningar {#tips-best-practices-limitations}

* Användningen av smarta innehållstjänster är begränsad till upp till 2 miljoner taggade bilder per år. Alla duplicerade bilder som bearbetas och taggas räknas som taggade bilder.
* Om du kör taggningsarbetsflödet från tidslinjen kan du använda taggar på högst 15 resurser i taget.
