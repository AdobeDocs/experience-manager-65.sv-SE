---
title: Aktivera bilagor för ett HTML5-formulär
seo-title: Aktivera bilagor för ett HTML5-formulär
description: Bifogade filer i HTML5-formulär är som standard inaktiverade.
seo-description: Bifogade filer i HTML5-formulär är som standard inaktiverade.
uuid: 2c62ac3e-4b27-46c7-a61d-a805fb5d26fb
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 8eebfcd6-0597-44ed-b718-bf9a1baa6c12
feature: Mobile Forms
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '337'
ht-degree: 0%

---


# Aktivera bilagor för ett HTML5-formulär {#enabling-attachments-for-an-html-form}

Du kan överföra, förhandsgranska och skicka bilagor med HTML5-formulär. Som standard är stöd för bifogade filer inaktiverat. Så här aktiverar du stöd för bifogade filer:

1. Skapa en [anpassad profil](/help/forms/using/custom-profile.md) med multiselect-strängegenskap `mfAttachmentOptions`.
1. I den anpassade profilen anger du egenskaperna `fileSizeLimit`, `multiSelect` och `buttonTex`t för att konfigurera alternativ för widgeten för bifogade filer. Om det behövs kan du även ange fler anpassade egenskaper.

1. Använd följande konfigurationer i den anpassade profilen:

   * **multiSelect** -> true eller false (true som standard)
   * **fileSizeLimit** -> value_in_mb (say 5) (2 MB som standard)
   * **buttonText** -> Button text for pop-up window (&quot;Attach&quot; as default)
   * **acceptera** -> filtyper att acceptera (&quot;audio/&amp;ast;, video/&amp;ast;, image/&amp;ast;, text/&amp;ast;, .pdf&quot; som standard)

   >[!NOTE]
   >
   >I Microsoft Internet Explorer 9 kan användare bifoga filer som är större än den angivna gränsen. Det är ett känt problem.

1. Använd [metadataredigeraren](/help/forms/using/manage-form-metadata.md) för att välja den anpassade profil som du har skapat ovan för HTML 5-formulär.
1. Rendera formulärmallen med en anpassad profil och ikonen för bilagor visas i formulärverktygsfältet.

   >[!NOTE]
   >
   >Formulärportalen har en anpassad profil med funktioner för utkast och bilagor aktiverade. Mer information om profilen **Spara som utkast** finns i [Spara HTML5-formulär som ett utkast](/help/forms/using/saving-html5-form-draft.md).

1. Klicka på ikonen för bifogade filer, så visas en dialogruta för val av bifogade filer. Bläddra och markera den bifogade filen och klicka på **Bifoga**.

   >[!NOTE]
   >
   >Om du vill förhandsgranska en bifogad fil klickar du på namnet på den bifogade filen.

   >[!NOTE]
   >
   >Filförhandsvisningsalternativet är inte tillgängligt för anonyma användare.

## Överföringsformat för bifogad fil {#attachment-submission-format}

När bilagor är aktiverade skickar HTML5-formulär multipart-data. Flerdelsdata har två delar **dataXml** och **bilagor**.

>[!NOTE]
>
>För bakåtkompatibilitet gäller att om `mfAllowAttachments`-alternativet är inaktiverat skickar HTML5-formulären inte multipart-data. Det skickar enkel data-xml i formatet **application/xml**.

Om mfAllowAttachments-flaggan är aktiverad skickar [tjänstproxytjänsten](/help/forms/using/service-proxy.md) även multipart-data med dataXml och bilagor.
