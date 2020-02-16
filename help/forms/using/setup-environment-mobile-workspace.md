---
title: Konfigurera miljö för appen AEM Forms
seo-title: Konfigurera miljö för appen AEM Forms
description: Maskinvara, programvara och licenser för att bygga och driftsätta appen AEM Forms.
seo-description: Maskinvara, programvara och licenser för att bygga och driftsätta appen AEM Forms.
uuid: 4123a6b7-5766-476c-9afb-f57029b148ad
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: e6b01ade-7ea3-42a7-872d-cc35a3d2782a
docset: aem65
translation-type: tm+mt
source-git-commit: d9975c0dcc02ae71ac64aadb6b4f82f7c993f32c

---


# Konfigurera miljö för appen AEM Forms{#set-up-environment-for-aem-forms-app}

Du behöver följande maskinvara, programvara och licenser för att skapa och distribuera appen AEM Forms:

## För Windows-enheter {#for-windows-devices}

* Microsoft Windows 10
* Microsoft Visual Studio 2015
* Microsoft Visual Studio Tools for Apache Cordova

## För iOS-enheter {#for-ios-devices}

* Intel-baserad Apple Mac med Mac OS X 10.9.5 eller senare
* iOS SDK 8.4 eller senare
* Xcode-version: Xcode 6.4 för OS X eller senare
* Medlemskap i iOS Developer Enterprise Program
* Enterprise-certifikat för distribution av interna iOS-appar
* Apple iPad med iOS 8.4 eller senare

## För Android-enheter {#for-android-devices}

* Android Development Toolkit (ADT bundle) som kan hämtas från [https://developer.android.com/sdk/index.html](https://developer.android.com/sdk/index.html)
* Om miljön är konfigurerad på ett MAC-system bör ADT installeras i mappen Program.
* Om ADT är installerat på någon annan plats på MAC, eller om miljön är konfigurerad på ett Windows-system, måste ADT SDK-sökvägen uppdateras i `local.properties` filen som är tillgänglig i `src\android` mappen i det extraherade källarkivet `mobileworkspace-src.zip`. I den här filen pekar du på `sdk.dir` variabeln på ADT SDK-platsen på skrivbordet.

>[!NOTE]
>
>Adobe-lc-mobileworkspace-src.zip innehåller PhoneGap SDK 5.0. Kontrollera att PhoneGap SDK inte är förinstallerat.

[Kontakta supporten](https://www.adobe.com/account/sign-in.supportportal.html)
