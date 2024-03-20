---
title: Ställa in dagens meddelande
description: Med dagens meddelande kan du ange att ett meddelande ska visas på välkomstsidan i gränssnittet för arbetsytan.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_workspace
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: d8bab1c4-b830-4491-9486-d7e7f4dc2c99
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '173'
ht-degree: 0%

---

# Ställa in dagens meddelande {#setting-the-message-of-the-day}

Du kan ange att ett meddelande ska visas på välkomstsidan i användargränssnittet för arbetsytan.

Om det behövs kan du använda HTML-taggarna som stöds av Adobe Flash® Player för att formatera textens utseende:

* &lt;a> Ankarmärke
* &lt;b> Fet tagg
* &lt;br> Bryttagg
* &lt;font> Teckensnittstagg
* &lt;img> Bild-tagg
* &lt;i> Kursiv tagg
* &lt;li> Tagg för listobjekt
* &lt;p> Stycketagg
* &lt;span> Spänn tagg
* &lt;textformat> Tagg för textformat
* &lt;u> Understrykningstagg

Mer information om taggarna som stöds finns i definitionen av `htmlText` egenskapen för klassen TextField i [Flex språkreferens](https://flex.apache.org/).

## Ange dagens meddelande {#set-the-message-of-the-day}

1. I administrationskonsolen klickar du på Tjänster > Arbetsyta > Dagens meddelande.
1. Ange texten som ska visas på välkomstskärmen i rutan Dagens meddelande.
1. Klicka på Spara.

>[!NOTE]
>
>Flex Workspace används inte AEM formulärreleasen.
