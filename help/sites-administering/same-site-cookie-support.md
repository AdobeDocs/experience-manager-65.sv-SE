---
title: Stöd för samma webbplats-cookie för AEM 6.5
description: Läs mer om stöd för cookie-filer för samma webbplats för AEM 6.5.
topic-tags: security
exl-id: e1616385-0855-4f70-b787-b01701929bbc
solution: Experience Manager, Experience Manager Sites
feature: Security
role: Admin
source-git-commit: a28883778c5e8fb90cbbd0291ded17059ab2ba7e
workflow-type: tm+mt
source-wordcount: '221'
ht-degree: 0%

---

# Stöd för samma webbplats-cookie för AEM 6.5 {#same-site-cookie-support-for-aem-65}

Sedan version 80 har Chrome och senare Safari infört en ny modell för cookie-säkerhet. Det här läget är utformat för att införa säkerhetskontroller för tillgänglighet av cookies till tredjepartswebbplatser, via en inställning som kallas `SameSite`. Mer detaljerad information finns i den här [artikeln](https://web.dev/samesite-cookies-explained/).

Standardvärdet för den här inställningen (`SameSite=Lax`) kan göra att autentisering mellan AEM instanser eller tjänster inte fungerar. Detta beror på att domänerna eller URL-strukturerna för dessa tjänster kanske inte omfattas av begränsningarna i den här cookie-principen.

Du måste ange cookie-attributet `SameSite` till `None` för inloggningstoken för att undvika detta.

>[!CAUTION]
>
>Inställningen `SameSite=None` används bara om protokollet är säkert (HTTPS).
>
>Om protokollet inte är säkert (HTTP) ignoreras inställningen och det här WARN-meddelandet visas på servern:
>
>`WARN com.day.crx.security.token.TokenCookie Skip 'SameSite=None'`

Du kan lägga till inställningen genom att följa stegen nedan:

1. Gå till webbkonsolen på `http://serveraddress:serverport/system/console/configMgr`
1. Sök efter och klicka på autentiseringshanteraren **Adobe Granite**
1. Ange attributet **SameSite för cookien** för inloggningstoken till `None`, vilket visas i bilden nedan
   ![samesite](assets/samesite1.png)
1. Klicka på Spara
1. När den här inställningen har uppdaterats och användarna har loggats ut och loggat in igen, kommer `login-token`-cookies att ha attributet `None` inställt och kommer att inkluderas i förfrågningar mellan webbplatser.
