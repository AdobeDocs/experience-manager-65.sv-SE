---
title: Anpassa och utöka [!DNL Assets]
description: Lär dig hur du kan anpassa och utöka Resursresurs- och Resursredigeraren, som ger användarna ett särskilt skräddarsytt gränssnitt och en uppsättning funktioner.
contentOwner: AG
role: Developer
feature: Developer Tools
exl-id: 0271c528-23b0-4a3a-b5e8-5baf6cdeecc7
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 0%

---

# Anpassa och utöka [!DNL Assets] {#customizing-and-extending-assets}

Resursredigeraren är den primära åtkomstpunkten som användare på en Adobe Enterprise Manager-webbplats kommer att använda för att hitta, visa och ändra digitala resurser i din databas.

Som en [!DNL Experience Manager] kan du anpassa och utöka Resursredigeraren på flera olika sätt och ge användarna ett särskilt skräddarsytt gränssnitt och en uppsättning funktioner.

Följande funktionalitetsaspekter kan anpassas eller förbättras:

* [Utöka resursredigeraren](asseteditorx.md)
* [Utöka resurssökning](searchx.md)
* [Bearbeta resurser med mediehanterare och arbetsflöden](media-handlers.md)
* [Integrera resurser med aktivitetsströmmen](extending-activity-stream.md)
* [Proxyutveckling för resurser](proxy.md)
* [Bästa tillvägagångssätt för att konfigurera ImageMagick](best-practices-for-imagemagick.md)

## Anpassa utseendet {#customizing-the-look-and-feel}

Följande aspekter av utseendet och känslan i resursredigeraren kan anpassas:

* Logotyp: Du kan lägga till din egen organisations logotyp i gränssnittet.
* Färger och teckensnitt: Du kan ändra de färger och teckensnitt som används i gränssnittet.
* HTML-kod: Om du vill göra en mer detaljerad anpassning kan du ändra den underliggande HTML-koden som definierar gränssnitten.

## Anpassa återgivningar {#customizing-renditions}

I [!DNL Experience Manager Assets] terminologi en återgivning är den form i vilken en resurs presenteras. I allmänhet kan en viss resurs ha flera renderingar. Fullfärgsbilder kan till exempel ha en återgivning i sin ursprungliga storlek, en annan i en nedskalad storlek och en annan som både är nedskalad och konverterad till gråskala.

De återgivningar som en viss resurs är tillgänglig i kan anpassas och nya återgivningar skapas.
