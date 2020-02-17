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
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Hanterare för enkel inloggning och timeout {#single-sign-on-and-timeout-handlers}

AEM Forms-arbetsytan är enkel inloggning aktiverad. Om en användare har loggat in på ett AEM Forms-program som Forms Manager eller PDF Generator-användargränssnitt och har åtkomst till arbetsytan i AEM Forms i samma webbläsarsession, loggas användaren in på AEM Forms-arbetsytan och vice versa.

## Hantera servertimeout i arbetsytan för AEM Forms {#handling-server-timeout-in-nbsp-aem-forms-workspace}

Sessionstimeout för en användare kan konfigureras i administrationskonsolen.

Om du vill ange tidsgränsen loggar du in `https://[server]:[port]/adminui`på, går till **Inställningar > Användarhantering > Konfiguration > Konfigurera avancerade systemattribut** och gör önskade inställningar.

I AEM Forms-arbetsytan hanteras timeout som:

* Sessionstiden för en användare är tillgänglig som svar på ett anrop som initierar en användarsession. `initialize`
* En popup-dialogruta meddelar användaren om att sessionen kommer att upphöra 15 sekunder innan sessionen går ut.

I den här popup-dialogrutan:

* Klicka på OK för att avsluta användarsessionen.
* Klicka på Avbryt för att initiera om användarsessionen.

>[!NOTE]
>
>Om ingen åtgärd vidtas loggas användaren automatiskt ut från AEM Forms-arbetsytan tre sekunder innan sessionen upphör.

**[Kontakta supporten](https://www.adobe.com/account/sign-in.supportportal.html)**
