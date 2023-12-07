---
title: Egen vattenstämpel i PDF förhandsvisning
description: Lär dig hur du skapar en anpassad vattenstämpel i PDF-förhandsvisningen.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
docset: aem65
feature: Correspondence Management
exl-id: 7d90fade-1ca4-41d8-bbf9-45490465784a
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '327'
ht-degree: 0%

---

# Egen vattenstämpel i PDF förhandsvisning{#custom-watermark-in-letter-pdf-preview}

## Ökning {#overview}

I användargränssnittet Skapa korrespondens förhandsgranskar agentanvändare korrespondensen i den slutliga form som den skickas till efterbearbetning, till exempel för e-post eller utskrift.

För att förhindra obehörig användning av dessa data kan man lägga in en vattenstämpel på förhandsgranskningen PDF. Standardvattenstämpeln är&quot;PREVIEW&quot;, som visas över PDF.

Om du vill aktivera vattenstämpeln i förhandsvisningsfönstret PDF väljer du **[!UICONTROL Apply Watermark]** Alternativet Under förhandsgranskning i **[!UICONTROL Correspondence Management Configurations]** på https://&#39;[server]:[port]&#39;/system/console/configMgr.

![default-watermark](assets/default-watermark.png)

Följ de här stegen för att anpassa texten och utseendet på vattenstämpeln:

## Anpassa vattenstämpeln i förhandsvisningen av PDF i användargränssnittet för Skapa korrespondens {#customizewatermark-}

1. Gå till `https://'[server]:[port]'/[ContextPath]/crx/de` och logga in som administratör.
1. Skapa en mapp med namnet i appmappen **[!UICONTROL previewwatermark]** med en sökväg/struktur som liknar mappen med förhandsvattenstämpeln i mappen libs:

   1. Högerklicka på **förhandsgranskningsvattenstämpel** mapp på följande sökväg och välj **Överläggsnod**:

      `/libs/fd/cm/configFiles/previewwatermark`

   1. Kontrollera att dialogrutan Overlay Node har följande värden:

      **Sökväg:** /libs/fd/cm/configFiles/previewwatermark

      **Plats för övertäckning:** /apps/

      **Matcha nodtyper:** Markerad

      >[!NOTE]
      >
      >Gör inga ändringar i grenen /libs. Alla ändringar du gör kan gå förlorade eftersom den här grenen kan ändras när du:
      >
      >    
      >    
      >    * Uppgradera till din instans
      >    * Använd en snabbkorrigering
      >    * Installera ett funktionspaket
      >    
      >

   1. Klicka **OK** och sedan klicka **Spara alla**. The **[!UICONTROL previewwatermark]** mappen skapas i den angivna sökvägen.

1. Kopiera och klistra in ddx-filen från mappen &quot;/libs/fd/cm/configFiles/previewwatermark&quot; till mappen &quot;/apps/fd/cm/configFiles/previewwatermark&quot; och klicka på **[!UICONTROL Save All]**.
1. Gör önskade ändringar i ddx-filen under /apps/fd/cm/configFiles/previewwatermark/.

   ```xml
   <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
    <PDF result="output.pdf">
     <PDF source="input.pdf"/>
           <Watermark opacity="15%" rotation="45">
            <StyledText>
                     <p font-family="Georgia" font-size="70pt" color="black" font-weight="bold">
                         PREVIEW
                    </p>
            </StyledText>
           </Watermark>
    </PDF>
   </DDX>
   ```

   Mer information om hur du anpassar vattenstämpelns utseende, text och justering finns i Lägga till och ta bort vattenstämplar och bakgrunder i dialogrutan [Assembler Service och DDX Reference](https://help.adobe.com/en_US/livecycle/11.0/ddxRef.pdf) -dokument.

   >[!NOTE]
   >
   >I ddx-filen ska referenserna till result och source inte ändras till output.pdf och input.pdf. Namnet på filen ddx ska inte heller ändras.

1. Klicka **Spara alla**.
