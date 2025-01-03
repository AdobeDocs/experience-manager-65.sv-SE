---
title: Ställa in dagens meddelande
description: Med dagens meddelande kan du ange att ett meddelande ska visas på välkomstsidan i Workspace användargränssnitt.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_workspace
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: d8bab1c4-b830-4491-9486-d7e7f4dc2c99
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: tm+mt
source-wordcount: '185'
ht-degree: 0%

---

# Ställa in dagens meddelande {#setting-the-message-of-the-day}

>[!NOTE]
> 
> Kontrollera att användaren har administratörsbehörighet för att komma åt administratörskonsolen.

Du kan ange att ett meddelande ska visas på välkomstsidan i Workspace användargränssnitt.

Om det behövs kan du använda HTML-taggarna som stöds av Adobe Flash® Player för att formatera textens utseende:

* &lt;a> Ankartagg
* &lt;b> Fet tagg
* &lt;br> Bryttagg
* Teckensnittstaggen &lt;font>
* Bild-taggen &lt;img>
* Taggen &lt;i> Kursiv
* &lt;li>-tagg för listobjekt
* Taggen &lt;p> Stycke
* &lt;span> Span-tagg
* Tagg för textformat
* &lt;u> Understrykningstagg

Mer information om de taggar som stöds finns i definitionen av egenskapen `htmlText` för klassen TextField i [Flex språkreferens](https://flex.apache.org/).

## Ange dagens meddelande {#set-the-message-of-the-day}

1. I administrationskonsolen klickar du på Tjänster > Workspace > Dagens meddelande.
1. Ange texten som ska visas på välkomstskärmen i rutan Dagens meddelande.
1. Klicka på Spara.

>[!NOTE]
>
>Flex Workspace används inte i AEM.
