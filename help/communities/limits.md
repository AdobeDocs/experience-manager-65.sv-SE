---
title: Gränser för medlemsbidrag
seo-title: Gränser för medlemsbidrag
description: Med funktionen för bidragsgränser kan du begränsa vilka bidrag som ska skyddas mot skräppost
seo-description: Med funktionen för bidragsgränser kan du begränsa vilka bidrag som ska skyddas mot skräppost
uuid: 99b2a855-3f0d-41a0-9572-517a7f29af9f
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: d855aac2-f34d-402f-9dc3-c7ad494b45f2
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Gränser för medlemsbidrag {#member-contribution-limits}

## Översikt {#overview}

Funktionen för bidragsbegränsning ger möjlighet att begränsa bidrag från communitymedlemmar som ett sätt att skydda sig mot skräppost.

När en medlem är begränsad kommer alla inlägg som överskrider det tillåtna antalet bidrag att resultera i en varning om att gränsen har överskridits och att inlägget avvisas. Community-medlemmen kan sedan gå till communitymeddelandecentret och kontakta en community-ansvarig som kan ta bort begränsningarna om det är lämpligt.

Tilläggsgränser kan aktiveras individuellt från [medlemskonsolen](members.md) och/eller konfigureras så att de aktiveras automatiskt när besökarna blir nya medlemmar.

Med hjälp av medlemskonsolen kan bidragsgränser tas bort proaktivt för en medlem av en community-chef när som helst, eller tas bort reaktivt när en medlem skickar ett meddelande till en community-administratör som gör en sådan begäran.

## Konfiguration av AEM Communities User Generated Content Contribution Limits {#aem-communities-user-generated-content-contribution-limits-configuration}

Den här OSGi-konfigurationen

* Definierar karaktärerna för bidragsgränserna (antal tjänster inom en tidsperiod).
* Identifierar vem medlemmen kan meddela när gränsen har nåtts
* Identifierar domäner som aldrig behöver begränsas

Så här når du OSGi-konfigurationen:

* På den primära utgivaren
* Logga in med administratörsbehörighet
* Åtkomst till [webbkonsolen](../../help/sites-deploying/configuring-osgi.md)

   * Till exempel [http://localhost:4503/system/console/configMgr](http://localhost:4503/system/console/configMgr)

* Sök `AEM Communities User Generated Content Contribution Limits Configuration`
* Markera redigeringsikonen

![chlimage_1-127](assets/chlimage_1-127.png)

* **[!UICONTROL Använd UGC-bidragsgränser automatiskt]**

   Om det här alternativet är markerat anger automatiskt bidragsgränser för användare när de registrerar sig som community-medlemmar. Detta återspeglas i communitymedlemmens profil och kan aktiveras/inaktiveras från [medlemskonsolen](members.md). Nya medlemmar med en e-postadress från en vitlistad domän begränsas aldrig.

   Standard är avmarkerat.

* **[!UICONTROL UGC-gräns]**

   Högsta antal bidrag.

   Standard är 10 inlägg.

* **[!UICONTROL UGC-gränsfrekvens]**

   Den tidsperiod som begränsar UGC-gränsen.

   Standardvärdet är 60 minuter.

* **[!UICONTROL Domäner]**

   En vit lista med en eller flera e-postdomäner. Markera +-ikonen om du vill göra ytterligare inmatningar.

   Användare med e-postadresser i de vita angivna domänerna påverkas inte när UGC-bidragsgränser tillämpas automatiskt. Om till exempel en domän `mycompany.com` läggs till i listan över domäner `me@mycompany.com` begränsas aldrig en medlem med e-postadress från publicering.

   Standard är en tom vit lista.

* **[!UICONTROL Meddelandemottagare]**

   Lista över ett eller flera auktoriserbara ID:n för medlemmar som kan ändra bidragsgränserna för medlemmar. Markera +-ikonen om du vill göra ytterligare inmatningar.

   Medlemmar får endast nå ut till angivna medlemmar när deras gräns har nåtts.

   Standardvärdet är inga meddelandemottagare.

Obs! Standardkonfigurationen resulterar i högst 10 inlägg inom en timme.
