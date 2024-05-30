---
title: Förbättrade smarta taggar
description: Förbättrade smarta taggar
contentOwner: AG
feature: Smart Tags, Search
role: User
exl-id: 5eff4a0f-30b1-4753-ad0b-002656eed972
hide: true
solution: Experience Manager, Experience Manager Assets
source-git-commit: 5aff321eb52c97e076c225b67c35e9c6d3371154
workflow-type: tm+mt
source-wordcount: '1545'
ht-degree: 1%

---

# Förstå, använda och strukturera smarta taggar {#enhanced-smart-tags}

| Version | Artikellänk |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Klicka här](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/smart-tags.html?lang=en) |
| AEM 6.5 | Den här artikeln |

Organisationer som hanterar digitalt material använder i allt högre grad taxonomistyrd vokabulär i metadata. Det innehåller i själva verket en lista med nyckelord som anställda, partners och kunder vanligtvis använder för att referera till och söka efter digitala resurser i en viss klass. Genom att tagga resurser med taxonomistyrd vokabulär ser du till att resurserna är lätta att identifiera och hämta.

Jämfört med naturtrogna språkordlistor kan taggning av digitala resurser baserat på företagsklonomi hjälpa dem att anpassa sig till företagets verksamhet och säkerställa att de mest relevanta resurserna visas i sökningar.

En biltillverkare kan t.ex. märka bilderna med modellnamn så att endast relevanta bilder visas när bilder av olika modeller söks igenom för att utforma en kampanj.

För att Smart Content Service ska kunna använda rätt taggar måste du träna den för att identifiera din taxonomi. För att utbilda tjänsten måste du först strukturera en uppsättning resurser och taggar som bäst beskriver dessa resurser. Använd dessa taggar på resurserna och kör ett utbildningsarbetsflöde för att hjälpa tjänsten att lära sig mer.

När en tagg har tränats och är klar kan tjänsten nu använda dessa taggar på resurser via ett taggningsarbetsflöde.

I bakgrunden använder Smart Content Service Adobe Sensei AI-ramverket för att träna sin bildigenkänningsalgoritm i er taggstruktur och affärsklonomi. Den här innehållsintelligensen används sedan för att tillämpa relevanta taggar på en annan uppsättning resurser.

Smart Content Service är en molntjänst som är värd för [!DNL Adobe Developer Console]. Så här använder du det i [!DNL Adobe Experience Manager]måste systemadministratören integrera [!DNL Experience Manager] driftsättning med [!DNL Adobe Developer Console].

Här är sammanfattningsvis de viktigaste stegen för att använda tjänsten Smart Content:

* Onboarding
* Granska resurser och taggar (taxonomidefinition)
* Utbilda Smart Content Service
* Automatisk taggning

![Flödesschema](assets/flowchart.gif)

## Förutsättningar och format som stöds {#prerequisites}

Innan du kan använda tjänsten för smart innehåll bör du kontrollera följande för att skapa en integrering på [!DNL Adobe Developer Console]:

* Ett Adobe ID-konto med administratörsbehörighet för organisationen.
* Aktivera tjänsten Smart Content Service för din organisation.
* Om du vill lägga till baspaketet för smarta innehållstjänster i en distribution, licens [!DNL Adobe Experience Manager Sites] Baspaket och [!DNL Assets] tillägg.

Tjänsten använder smarta taggar för resurser av följande MIME-typer:

* `image/jpeg`
* `image/tiff`
* `image/png`
* `image/bmp`
* `image/gif`
* `image/pjpeg`
* `image/x-portable-anymap`
* `image/x-portable-bitmap`
* `image/x-portable-graymap`
* `image/x-portable-pixmap`
* `image/x-rgb`
* `image/x-xbitmap`
* `image/x-xpixmap`
* `image/x-icon`
* `image/photoshop`
* `image/x-photoshop`
* `image/psd`
* `image/vnd.adobe.photoshop`

Tjänsten använder smarta taggar för resursåtergivningar av följande MIME-typer:

* `image/jpeg`
* `image/pjpeg`
* `image/png`

## Onboarding {#onboarding}

Tjänsten Smart Content Service kan köpas som tillägg till [!DNL Experience Manager]. När du har köpt produkten skickas ett e-postmeddelande till administratören för organisationen med en länk till [!DNL Adobe I/O].

Administratören kan följa länken för att integrera Smart Content Service med [!DNL Experience Manager]. Integrera tjänsten med [!DNL Experience Manager Assets], se [Konfigurera smarta taggar](config-smart-tagging.md).

Startprocessen är klar när administratören konfigurerar tjänsten och lägger till användare i [!DNL Experience Manager].

## Granska resurser och taggar {#reviewing-assets-and-tags}

Det första du vill göra när du är ombord är att identifiera en uppsättning taggar som bäst beskriver bilderna i ditt företags sammanhang.

Granska sedan bilderna för att identifiera en uppsättning bilder som bäst motsvarar din produkt för ett visst affärsbehov. Se till att resurserna i din aktuella uppsättning följer [Utbildningsriktlinjer för smarta innehållstjänster](/help/assets/config-smart-tagging.md#training-the-smart-content-service).

Lägg till resurserna i en mapp och använd taggarna på varje resurs från egenskapssidan. Kör sedan utbildningsarbetsflödet i den här mappen. Den välstrukturerade uppsättningen resurser gör det möjligt för Smart Content Service att effektivt utbilda fler resurser med hjälp av dina taxonomidefinitioner.

>[!NOTE]
>
>1. Utbildning är en oåterkallelig process. Adobe rekommenderar att du granskar taggarna i den välstrukturerade resursuppsättningen innan du utbildar Smart Content Service på taggarna.
>1. Innan du utbildar dig för en tagg, se [Utbildningsriktlinjer för smarta innehållstjänster](/help/assets/config-smart-tagging.md#training-the-smart-content-service).
>1. När du utbildar Smart Content Service för första gången rekommenderar Adobe att du utbildar den på minst två distinkta taggar.

## Förstå [!DNL Experience Manager] sökresultat med smarta taggar {#understandsearch}

Som standard [!DNL Experience Manager] sökningen kombinerar söktermerna med en `AND` -sats. Om du använder smarta taggar ändras inte standardbeteendet. Om du använder smarta taggar läggs en extra `OR` -sats för att hitta något av söktermerna som är relaterade till smarta taggar. Överväg till exempel att söka efter `woman running`. Resurser med bara `woman` eller bara `running` nyckelordet i metadata visas inte som standard i sökresultatet. Men en resurs som är taggad med antingen `woman` eller `running` smarta taggar visas i en sådan sökfråga. Sökresultaten är en kombination av

* Resurser med `woman` och `running` nyckelord i metadata.

* Resurser som är smarta och taggade med något av nyckelorden.

Sökresultaten som matchar alla söktermer i metadatafält visas först, följt av sökresultaten som matchar någon av söktermerna i de smarta taggarna. I ovanstående exempel är den ungefärliga visningsordningen för sökresultat:

1. Matchar med `woman running` i de olika metadatafälten.
1. Matchar med `woman running` i smarta taggar.
1. Matchar med `woman` eller `running` i smarta taggar.

>[!CAUTION]
>
>Om Lucene-indexeringen görs av [!DNL Adobe Experience Manager]fungerar sökningen baserat på smarta taggar inte som förväntat.

## Tagga resurser automatiskt {#tagging-assets-automatically}

När du har utbildat tjänsten Smart Content kan du utlösa taggningsarbetsflödet för att automatiskt tillämpa lämpliga taggar på en annan uppsättning med liknande resurser.

Du kan köra taggningsarbetsflödet periodiskt eller när det behövs.

>[!NOTE]
>
>Arbetsflödet för taggning körs både på resurser och mappar.

### Periodisk taggning {#periodic-tagging}

Du kan aktivera tjänsten Smart Content Service för att regelbundet tagga resurser i en mapp. Öppna egenskapssidan för resursmappen och välj **[!UICONTROL Enable Smart Tags]** under **[!UICONTROL Details]** och spara ändringarna.

När det här alternativet har valts för en mapp taggar tjänsten Smart Content Service automatiskt resurserna i mappen. Som standard körs taggningsarbetsflödet varje dag kl. 12.00.

### On-demand-taggning {#on-demand-tagging}

Du kan utlösa taggningsarbetsflödet från arbetsflödeskonsolen eller från tidslinjen för att omedelbart tagga dina resurser.

>[!NOTE]
>
>Om du kör taggningsarbetsflödet från tidslinjen kan du använda taggar på högst 15 resurser i taget.

#### Tagga resurser från arbetsflödeskonsolen {#tagging-assets-from-the-workflow-console}

1. I [!DNL Experience Manager] gränssnitt, gå till **[!UICONTROL Tools]** > **[!UICONTROL Workflow]** > **[!UICONTROL Models]**.
1. Från **[!UICONTROL Workflow Models]** väljer du **[!UICONTROL DAM Smart Tags Assets]** arbetsflöde och klicka sedan på **[!UICONTROL Start Workflow]** i verktygsfältet.

   ![dam_smart_tag_workflow](assets/dam_smart_tag_workflow.png)

1. I **[!UICONTROL Run Workflow]** bläddrar du till nyttolastmappen som innehåller resurser som du vill använda dina taggar på automatiskt.
1. Ange en rubrik för arbetsflödet och en valfri kommentar. Klicka på **[!UICONTROL Run]**.

   ![tagging_dialog](assets/tagging_dialog.png)

   Kontrollera om Smart Content Service taggade dina resurser på rätt sätt genom att navigera till resursmappen och granska taggarna.

#### Tagga resurser från tidslinjen {#tagging-assets-from-the-timeline}

1. Från [!DNL Assets] -användargränssnittet väljer du den mapp som innehåller resurser eller specifika resurser som du vill använda smarta taggar på.
1. Öppna det övre vänstra hörnet **[!UICONTROL Timeline]**.
1. Öppna funktionsmakron längst ned i den vänstra sidopanelen och klicka på **[!UICONTROL Start Workflow]**.

   ![start_workflow](assets/start_workflow.png)

1. Välj **[!UICONTROL DAM Smart Tag Assets]** arbetsflöde och ange en rubrik för arbetsflödet.
1. Klicka på **[!UICONTROL Start]**. Arbetsflödet använder taggar på resurserna. Om du vill kontrollera om Smart Content Service taggade dina resurser på rätt sätt går du till resursmappen och granskar taggarna.

>[!NOTE]
>
>I de efterföljande taggningscyklerna är det bara de ändrade resurserna som taggas igen med nyligen tränade taggar. Även oförändrade resurser taggas om mellanrummet mellan den sista och den aktuella taggningscykeln för taggningsarbetsflödet överstiger 24 timmar. För periodiska taggningsarbetsflöden taggas oförändrade resurser när tidsintervallet överskrider sex månader.

## Kuratera eller moderera de använda smarta taggarna {#manage-smart-tags}

Du kan strukturera smarta taggar om du vill ta bort felaktiga taggar som har tilldelats dina varumärkesbilder så att endast de mest relevanta taggarna visas.

Genom att moderera smarta taggar kan du också förbättra taggbaserade sökningar efter bilder genom att se till att bilden visas i sökresultaten för de mest relevanta taggarna. I grund och botten eliminerar det riskerna för att bilder som inte är relaterade visas i sökresultaten.

Du kan också tilldela en tagg en högre rankning för att öka dess relevans för en bild. Om du befordrar en tagg för en bild ökar risken för att bilden visas i sökresultaten när du söker efter den aktuella taggen.

1. I sökrutan söker du efter resurser som är baserade med en tagg som nyckelord.
1. Granska sökresultaten för att identifiera en bild som du inte tycker är relevant för din sökning.
1. Markera bilden och klicka på **[!UICONTROL Manage Tags]** i verktygsfältet.
1. Från **[!UICONTROL Manage Tags]** kan du granska taggarna. Om du inte vill att bilden ska genomsökas baserat på en viss tagg, markerar du taggen och klickar sedan på **[!UICONTROL Delete]** i verktygsfältet. Du kan även klicka på `x` symbol som visas bredvid ett märkord.
1. Om du vill tilldela en tagg en högre rankning markerar du taggen och klickar på **[!UICONTROL Promote]** i verktygsfältet. Taggen som du höjer upp flyttas till **[!UICONTROL Tags]** -avsnitt.
1. Klicka **[!UICONTROL Save]** och sedan klicka **[!UICONTROL OK]**
1. Navigera till **[!UICONTROL Properties]** sida för bilden. Observera att taggen som du befordrade har fått större relevans och visas tidigare i sökresultatet.

## Tips och begränsningar {#tips-best-practices-limitations}

* Använd de bilder som passar bäst för att utbilda modellen. Utbildningen kan inte återupptas eller så kan utbildningsmodellen inte tas bort. Hur korrekt taggningen är beror på den aktuella kursen, så gör det med omsorg.
* Användningen av smarta innehållstjänster är begränsad till 2 miljoner taggade bilder per år. Alla duplicerade bilder som bearbetas och taggas räknas som taggade bilder.
* Om du kör taggningsarbetsflödet från tidslinjen kan du använda taggar på högst 15 resurser i taget.
* Smarta taggar fungerar bara för bildformaten PNG och JPG. Resurser som stöds och som har återgivningar skapade i dessa två format taggas med smarta taggar.

>[!MORELIKETHIS]
>
>* [Översikt och utbildning av smarta taggar](enhanced-smart-tags.md)
>* [Konfigurera smart taggning](config-smart-tagging.md)
>* [Felsöka smarta taggar för OAuth-autentiseringsuppgifter](config-oauth.md)
>* [Videosjälvstudiekurs om smarta taggar](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/metadata/image-smart-tags.html)
