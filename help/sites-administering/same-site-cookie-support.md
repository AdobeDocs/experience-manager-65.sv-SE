---
title: Stöd för samma webbplats-cookie för AEM 6.5
description: Stöd för samma webbplats-cookie för AEM 6.5
topic-tags: security
translation-type: tm+mt
source-git-commit: ac2f3d69fd20d7779120a194c698d6f0dd6e6a84
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 1%

---


# Stöd för samma webbplats-cookie i AEM 6.5 {#same-site-cookie-support-for-aem-65}

Sedan version 80 har Chrome och senare Safari introducerat en ny modell för cookie-säkerhet. Det här läget är utformat för att införa säkerhetskontroller runt tillgängligheten av cookies till tredjepartswebbplatser, via en inställning som heter `SameSite`. Mer information finns i den här [artikeln](https://web.dev/samesite-cookies-explained/).

Standardvärdet för den här inställningen (`SameSite=Lax`) kan göra att autentisering mellan AEM instanser eller tjänster inte fungerar. Detta beror på att domänerna eller URL-strukturerna för dessa tjänster kanske inte omfattas av begränsningarna i den här cookie-principen.

För att komma runt detta måste du ange attributet SameSite cookie till `None` för inloggningstoken.

Du kan göra detta genom att följa stegen nedan:

1. Gå till webbkonsolen på `http://serveraddress:serverport/system/console/configMgr`
1. Sök efter och klicka på **Autentiseringshanteraren för Adobe Granite-token**
1. Ange **SameSite-attributet för cookie** för inloggningstoken till `None`, vilket visas i bilden nedan
   ![samma webbplats](assets/samesite1.png)
1. Klicka på Spara
1. När den här inställningen har uppdaterats och användarna har loggats ut och loggat in igen har `login-token`-cookies attributuppsättningen `None` och kommer att inkluderas i begäranden mellan webbplatser.
