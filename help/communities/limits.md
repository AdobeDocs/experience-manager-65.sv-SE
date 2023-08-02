---
title: Gränser för medlemsbidrag
description: Med funktionen för bidragsgränser kan du begränsa vilka bidrag som ska skyddas mot skräppost
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
role: Admin
exl-id: d00a8eb2-47ce-425a-a312-f043f82912be
source-git-commit: f0dd1ac3ab9c17a8b331f5048d84ec97dd23924f
workflow-type: tm+mt
source-wordcount: '418'
ht-degree: 0%

---

# Gränser för medlemsbidrag {#member-contribution-limits}

## Översikt {#overview}

Med funktionen för begränsning av bidrag kan du begränsa bidragen från communitymedlemmar som ett sätt att skydda dig mot skräppost.

När en medlem är begränsad kommer alla inlägg som överskrider det tillåtna antalet bidrag att resultera i en varning om att gränsen har överskridits och att inlägget avvisas. Community-medlemmen kan sedan gå till communitymeddelandecentret och kontakta en community-ansvarig som kan ta bort begränsningarna om det är lämpligt.

Bidragsgränser kan aktiveras individuellt från [Medlemskonsol](members.md) och/eller konfigureras att aktiveras automatiskt när besökarna blir nya medlemmar.

Med hjälp av medlemskonsolen kan bidragsgränser tas bort proaktivt för en medlem av en community-chef när som helst, eller tas bort reaktivt när en medlem skickar ett meddelande till en community-administratör som gör en sådan begäran.

## Konfiguration av AEM Communities användargenererade innehållsbidragsgränser {#aem-communities-user-generated-content-contribution-limits-configuration}

Den här OSGi-konfigurationen:

* Definierar egenskaperna för bidragsgränserna (antalet tjänster inom en tidsperiod).
* Identifierar vem medlemmen kan meddela när gränsen har nåtts.
* Identifierar domäner som aldrig behöver begränsas.

Så här når du OSGi-konfigurationen:

* På den primära utgivaren:
* Logga in med administratörsbehörighet.
* Öppna [Webbkonsol](../../help/sites-deploying/configuring-osgi.md).

   * Till exempel: [http://localhost:4503/system/console/configMgr](http://localhost:4503/system/console/configMgr)

* Sök `AEM Communities User Generated Content Contribution Limits Configuration`.
* Välj redigeringsikonen.

![configure-limits](assets/configure-limits.png)

* **[!UICONTROL Automatically Apply UGC Contribution Limits]**

  Om det här alternativet är markerat anger automatiskt bidragsgränser för användare när de registrerar sig som community-medlemmar. Detta återspeglas i communitymedlemmens profil och kan aktiveras/inaktiveras från [medlemskonsol](members.md). Nya medlemmar med en e-postadress från ett tillåtelselista av domäner begränsas aldrig.

  Standard är avmarkerat.

* **[!UICONTROL UGC Limit]**

  Högsta antal bidrag.

  Standard är tio inlägg.

* **[!UICONTROL UGC Limit Frequency]**

  Den tidsperiod som begränsar UGC-gränsen.

  Standardvärdet är 60 minuter.

* **[!UICONTROL Domains]**

  En lista med tillåtelselista i en eller flera e-postdomäner. Markera +-ikonen om du vill göra fler poster.

  Användare med e-postadresser tillåtelselista i domäner påverkas inte när UGC-bidragsgränser tillämpas automatiskt. Exempel: om domän `mycompany.com` läggs till i listan över domäner och sedan en medlem med e-postadress `me@mycompany.com` begränsas aldrig från publicering.

  Standard är en tom tillåtelselista.

* **[!UICONTROL Messaging Recipients]**

  Lista över ett eller flera auktoriserbara ID:n för medlemmar som kan ändra bidragsgränserna för medlemmar. Markera +-ikonen om du vill göra fler poster.

  Medlemmar får endast nå ut till angivna medlemmar när deras gräns har nåtts.

  Standardvärdet är inga meddelandemottagare.

Obs! Standardkonfigurationen ger högst tio inlägg inom en timme.
