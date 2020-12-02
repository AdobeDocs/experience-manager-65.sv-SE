---
title: Hanterare för enkel inloggning och timeout
seo-title: Hanterare för enkel inloggning och timeout
description: Så här anger du timeout-värdet för sessionen för arbetsytan i AEM Forms.
seo-description: Så här anger du timeout-värdet för sessionen för arbetsytan i AEM Forms.
uuid: 17583fd5-6453-41d3-bb63-a639983fbea9
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 698990a2-dd3f-480f-9d15-d87563860297
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317
workflow-type: tm+mt
source-wordcount: '205'
ht-degree: 0%

---


# Hanterare för enkel inloggning och timeout {#single-sign-on-and-timeout-handlers}

AEM Forms arbetsyta är enkel inloggning aktiverad. Om en användare har loggat in på ett AEM Forms-program som Forms Manager eller PDF Generator och använder AEM Forms arbetsyta i samma webbläsarsession, loggas användaren in på AEM Forms arbetsyta och vice versa.

## Hantera servertimeout i AEM Forms arbetsyta {#handling-server-timeout-in-nbsp-aem-forms-workspace}

Sessionstimeout för en användare kan konfigureras i administrationskonsolen.

Om du vill ange tidsgränsen loggar du in på `https://'[server]:[port]'/adminui`, navigerar till **Inställningar > Användarhantering > Konfiguration > Konfigurera avancerade systemattribut** och gör önskade inställningar.

I AEM Forms-arbetsytan hanteras timeout:

* Sessionstiden för en användare är tillgänglig som svar på `initialize`-anrop som initierar användarsession.
* En popup-dialogruta meddelar användaren om att sessionen kommer att upphöra 15 sekunder innan sessionen går ut.

I den här popup-dialogrutan:

* Klicka på OK för att avsluta användarsessionen.
* Klicka på Avbryt för att initiera om användarsessionen.

>[!NOTE]
>
>Om ingen åtgärd vidtas loggas användaren automatiskt ut från AEM Forms-arbetsytan tre sekunder innan sessionen upphör.
