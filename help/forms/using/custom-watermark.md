---
title: Egen vattenstämpel i PDF-förhandsgranskning med bokstav
seo-title: Egen vattenstämpel i PDF-förhandsgranskning med bokstav
description: Lär dig hur du skapar en anpassad vattenstämpel i PDF-förhandsgranskning med bokstav.
seo-description: Lär dig hur du skapar en anpassad vattenstämpel i PDF-förhandsgranskning med bokstav.
uuid: 5adfede3-9b38-4a12-bf14-6d80cfb0a05a
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
discoiquuid: adc7ec13-0675-4071-9c4c-e238202d9d85
docset: aem65
translation-type: tm+mt
source-git-commit: 5a586758da84f467e075adcc33cdcede2fbf09c7

---


# Egen vattenstämpel i PDF-förhandsgranskning med bokstav{#custom-watermark-in-letter-pdf-preview}

## Översikt {#overview}

I användargränssnittet Skapa korrespondens förhandsgranskar agentanvändare korrespondensen i den slutliga form som den skickas till efterbearbetning, till exempel för e-post eller utskrift.

För att förhindra obehörig användning av dessa data kan organisationer lägga in en vattenstämpel i PDF-filen för förhandsgranskning. Standardvattenstämpeln är&quot;PREVIEW&quot;, som visas i hela PDF-filen.

Om du vill aktivera vattenstämpeln i PDF-förhandsgranskning väljer du alternativet **[!UICONTROL Använd vattenstämpel]** vid förhandsgranskning i **[!UICONTROL Correspondence Management Configurations]** på https://[server]:[port]/system/console/configMgr.

![default-watermark](assets/default-watermark.png)

Följ de här stegen för att anpassa texten och utseendet på vattenstämpeln:

## Anpassa vattenstämpeln i PDF-förhandsvisning i användargränssnittet Skapa korrespondens {#customizewatermark-}

1. Gå till `https://[server]:[port]/[ContextPath]/crx/de` och logga in som administratör.
1. I mappen apps skapar du en mapp med namnet **[!UICONTROL previewwatermark]** med en sökväg/struktur som liknar mappen med förhandsvisningsvattenstämpeln i mappen libs:

   1. Högerklicka på mappen **för förhandsvisning av vattenstämpel** i följande sökväg och välj **Overlay Node**:

      `/libs/fd/cm/configFiles/previewwatermark`

   1. Kontrollera att dialogrutan Overlay Node har följande värden:

      **** Sökväg: /libs/fd/cm/configFiles/previewwatermark

      **** Plats för övertäckning: /apps/

      **** Matcha nodtyper:Markerad

      >[!NOTE]
      >
      >Gör inga ändringar i grenen /libs. Alla ändringar du gör kan gå förlorade eftersom den här grenen kan ändras när du:
      >
      >    
      >    
      >    * Uppgradera till din instans
      >    * Använd en snabbkorrigering
      >    * Installera ett funktionspaket


   1. Klicka på **OK** och sedan på **Spara alla**. Mappen med **[!UICONTROL vattenstämplar]** för förhandsgranskning skapas i den angivna sökvägen.



1. Kopiera och klistra in ddx-filen från mappen &quot;/libs/fd/cm/configFiles/previewwatermark&quot; till mappen &quot;/apps/fd/cm/configFiles/previewwatermark&quot; och klicka på **[!UICONTROL Spara alla]**.
1. Gör önskade ändringar i ddx-filen under /apps/fd/cm/configFiles/previewwatermark/.

   ```
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

   Mer information om hur du anpassar vattenstämpelns utseende, text och justering finns i Lägga till och ta bort vattenstämplar och bakgrunder i [Assembler Service och DX Reference](https://help.adobe.com/en_US/livecycle/11.0/ddxRef.pdf) -dokumentet.

   >[!NOTE]
   >
   >I ddx-filen ska referenserna till result och source inte ändras till output.pdf och input.pdf. Namnet på filen ddx ska inte heller ändras.

1. Klicka på **Spara alla**.

