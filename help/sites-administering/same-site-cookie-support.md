---
title: Stöd för samma webbplats-cookie för AEM 6.5
description: Läs mer om stöd för cookie-filer för samma webbplats för AEM 6.5.
topic-tags: security
exl-id: e1616385-0855-4f70-b787-b01701929bbc
source-git-commit: e54c1d422f2bf676e8a7b0f50a101e495c869c96
workflow-type: tm+mt
source-wordcount: '222'
ht-degree: 0%

---

# Stöd för samma webbplats-cookie för AEM 6.5 {#same-site-cookie-support-for-aem-65}

Sedan version 80 har Chrome och senare Safari introducerat en ny modell för cookie-säkerhet. Det här läget är utformat för att införa säkerhetskontroller för tillgänglighet av cookies till tredje parters webbplatser via en inställning som kallas `SameSite`. Mer detaljerad information finns i [artikel](https://web.dev/samesite-cookies-explained/).

Standardvärdet för inställningen (`SameSite=Lax`) kan leda till att autentisering mellan AEM instanser eller tjänster inte fungerar. Detta beror på att domänerna eller URL-strukturerna för dessa tjänster kanske inte omfattas av begränsningarna i den här cookie-principen.

För att komma runt detta måste du ange `SameSite` cookie-attribut till `None` för inloggningstoken.

>[!CAUTION]
>
>The `SameSite=None` inställningen används bara om protokollet är säkert (HTTPS).
>
>Om protokollet inte är säkert (HTTP) ignoreras inställningen och det här WARN-meddelandet visas på servern:
>
>`WARN com.day.crx.security.token.TokenCookie Skip 'SameSite=None'`

Du kan lägga till inställningen genom att följa stegen nedan:

1. Gå till webbkonsolen på `http://serveraddress:serverport/system/console/configMgr`
1. Sök efter och klicka på **Autentiseringshanterare för Adobe Granite-token**
1. Ange **Attributet SameSite för cookie-filen för inloggningstoken** till `None`, vilket visas i bilden nedan
   ![samma webbplats](assets/samesite1.png)
1. Klicka på Spara
1. När den här inställningen har uppdaterats och användarna har loggat ut och loggat in igen, `login-token` cookies har `None` och kommer att inkluderas i förfrågningar mellan webbplatser.
