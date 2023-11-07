---
title: Integrera AEM 6.5 med Adobe Campaign
description: Läs om AEM stöd för integrering med Adobe Campaign i 6.5.
uuid: 6113279e-d1f5-46c3-ac94-50270fa55060
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: fd96f30c-0616-445e-adb9-050d52862ffc
exl-id: ab41e540-1d43-4fc2-99d4-621ff2290e77
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '335'
ht-degree: 3%

---


# Integrera AEM 6.5 med Adobe Campaign{#integrating-with-adobe-campaign}

Läs om AEM stöd för integrering med Adobe Campaign i 6.5.

Adobe Campaign är en uppsättning lösningar som gör att ni kan personalisera och leverera kampanjer i alla kanaler, både online och offline.

>[!NOTE]
>
>I det här dokumentet beskrivs hur du integrerar Adobe Campaign med AEM 6.5, den lokala AEM eller AMS-.
>
>Mer information om hur du integrerar Adobe Campaign med AEM as a Cloud Service, den AEM molnbaserade lösningen, [se det här dokumentet.](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/integrations/campaign.html)

## Integrera med Adobe Campaign Classic {#acc}

Det finns flera Adobe Campaign Classic-versioner (ACC). Stödet för integrering med AEM beror på vilken ACC-version du har implementerat och om AEM är installerad lokalt i AMS (Adobe Manage Services).

| ACC-version | Integrering med AEM 6.5 <br>On Premises | Integrering med AEM 6.5<br>AMS |
|---|---|---|
| [v7](https://experienceleague.adobe.com/docs/campaign-classic.html) | Stöds | Stöds |
| [v8](https://experienceleague.adobe.com/docs/campaign-v8.html) | Stöds | Stöds |
| Webbgränssnitt* | Stöds | Stöds |

*Webbgränssnittet för Adobe Campaign Classic förväntas vara klart i slutet av 2023.

I följande dokumentation beskrivs hur du integrerar AEM med Adobe Campaign Classic.

* [Integrera med Adobe Campaign Classic](/help/sites-administering/campaignonpremise.md) - Lär dig steg för steg hur du konfigurerar integreringen.

I följande ytterligare dokumentation beskrivs hur du använder integreringen.

* [E-postkärnkomponenter](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/email/introduction.html) - Lär dig mer om de e-postkomponenter som du kan använda för att skapa Campaign-innehåll i AEM.
* [Felsökning av Adobe Campaign Classic-integrering](/help/sites-administering/troubleshooting-campaignintegration.md) - Lär dig hur du åtgärdar de vanligaste problemen med AEM-ACC-integrering.

## Integrera med Adobe Campaign Standard {#acs}

Integrering av [Adobe Campaign Standard](https://experienceleague.adobe.com/docs/campaign-standard.html) (ACS) med AEM beror på om AEM har installerats lokalt på Adobe Manage Services (AMS).

| Integrering med AEM 6.5 <br>On Premises | Integrering med AEM 6.5<br>AMS |
|---|---|
| Stöds | Stöds |
| Stöds | Stöds |

I följande dokumentation beskrivs hur du integrerar AEM med Adobe Campaign Standard.

* [Integrera med Adobe Campaign Standard](/help/sites-administering/campaignstandard.md)

I följande ytterligare dokumentation beskrivs hur du använder integreringen.

* [E-postkärnkomponenter](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/email/introduction.html)
