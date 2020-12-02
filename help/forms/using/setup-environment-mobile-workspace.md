---
title: Konfigurera miljö för AEM Forms-program
seo-title: Konfigurera miljö för AEM Forms-program
description: Maskinvara, programvara och licenser för att bygga och driftsätta AEM Forms-appen.
seo-description: Maskinvara, programvara och licenser för att bygga och driftsätta AEM Forms-appen.
uuid: 4123a6b7-5766-476c-9afb-f57029b148ad
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: e6b01ade-7ea3-42a7-872d-cc35a3d2782a
docset: aem65
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 0%

---


# Konfigurera miljö för AEM Forms app{#set-up-environment-for-aem-forms-app}

Du behöver följande maskinvara, programvara och licenser för att skapa och distribuera AEM Forms-appen:

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
* Om ADT är installerat på någon annan plats på MAC, eller om miljön är konfigurerad på ett Windows-system, måste ADT SDK-sökvägen uppdateras i `local.properties`-filen som är tillgänglig i mappen `src\android` i det extraherade källarkivet `mobileworkspace-src.zip`. I den här filen pekar du på variabeln `sdk.dir` till ADT SDK-platsen på skrivbordet.

>[!NOTE]
>
>Adobe-lc-mobileworkspace-src.zip innehåller PhoneGap SDK 5.0. Kontrollera att PhoneGap SDK inte är förinstallerat.
