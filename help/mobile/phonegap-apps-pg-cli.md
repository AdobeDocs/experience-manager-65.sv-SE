---
title: Utveckla appar med PhoneGap CLI
description: Lär dig hur du utvecklar appar för mobiler med PhoneGap CLI i en startad utvecklingsmiljö.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
exl-id: fbeceb70-b199-478b-907b-253ed212ff99
solution: Experience Manager
feature: Mobile
role: Admin
source-git-commit: 2dae56dc9ec66f1bf36bbb24d6b0315a5f5040bb
workflow-type: tm+mt
source-wordcount: '637'
ht-degree: 1%

---

# Utveckla appar med PhoneGap CLI{#developing-apps-with-phonegap-cli}

{{ue-over-mobile}}

Som utvecklare kan du när som helst köra programmet på en enhet eller i en emulator, förutsatt att du har konfigurerat utvecklingsmiljön.

För att köra följande exempel behöver du ett system som kör macOS X med Xcode, eller ett Mac/Win/Linux-system med Android™ SDK installerat.

## Bootstrap din utvecklingsmiljö {#bootstrap-your-development-environment}

Konfigurera PhoneGap CLI (`https://docs.phonegap.com/en/4.0.0/guide_cli_index.md.html#The%20Command-Line%20Interface`)

För iOS: För att utveckla för iPhone och iPad behöver du Apple Xcode IDE.

* Hämta den kostnadsfritt [här](https://idmsa.apple.com/IDMSWebAuth/signin?appIdKey=891bd3417a7776362562d2197f89480a8547b108fd934911bcbea0110d07f757&amp;path=%2Fdownload%2F&amp;rv=1).
* Plattformshandbok för PhoneGap iOS (`https://docs.phonegap.com/en/4.0.0/guide_platforms_ios_index.md.html#iOS%20Platform%20Guide`)

För Android™: För att utveckla för iPhone och iPad behöver du Google Android™ Studio IDE.

* Hämta den kostnadsfritt [här](https://developer.android.com/studio).
* Plattformshandbok för PhoneGap Android™ (`https://docs.phonegap.com/en/4.0.0/guide_platforms_android_index.md.html#Android%20Platform%20Guide`)

## Ladda ned Source {#download-the-source}

När du har startat utvecklingsmiljön hämtar du källan från AEM App Build Tile:

* Klicka på den nedrullningsbara menyn PhoneGap Build.

![chlimage_1-45](assets/chlimage_1-45.png)

* Klicka på Hämta Source.
* Välj önskad källa i Ladda ned Source modal.

![chlimage_1-46](assets/chlimage_1-46.png)

>[!NOTE]
>
>Utvecklingskällan innehåller det senaste läget för din app, med ändringar som inte har mellanlagrats. Använd mellanlagringskällan för att skapa releaseförslag för att skicka till appbutiksleverantörer.
>
>Om du aldrig testar din app aktiveras mellanlagringsarbetsflödet när du väljer Förproduktion (tips: visas som en mellanlagrad app i PhoneGap Enterprise Viewer App som finns i AppStore och Google PlayStore).

* Klicka på Hämta och spara ZIP-filen på datorn.
* Extrahera den hämtade ZIP-filen till arbetsytan.

## Skapa och läsa in appen (från källa) {#build-and-load-the-app-from-source}

PhoneGap CLI kan skapa ett plattformsprojekt, kompilera källan och distribuera appen med ett enda kommando.

>[!NOTE]
>
>Du kan göra alla dessa steg separat, se PhoneGap CLI-dokument (`https://phonegap.com/blog/2014/11/13/phonegap-cli-3-6-3/`).

1. Kontrollera att du har installerat PhoneGap CLI, se ovan.
1. I ett konsolfönster (eller terminalfönster) går du till rotkatalogen för den extraherade källan.
1. Ange följande kommando:

```xml
phonegap run android

// -- or -- //

phonegap run ios
```

>[!NOTE]
>
>Om du har problem kan du gå tillbaka till grunderna för felsökning -
>
>1. Skapa en mapp (mkdir test)
>1. Navigera till den nya mappen (cd test)
>1. Kör `phonegap create helloWorld`
>1. Navigera till helloWorld (cd helloWorld)
>1. Kör `phonegap run android` (eller ersätt Android™ med iOS enligt ovan).
>1. Emulatorn öppnar och kör din nya PhoneGap-app med texten&quot;Device Ready&quot; om JavaScript Bridge till native fungerar.
>
>Denna felsökning verifierar att PhoneGap CLI-utvecklingsmiljön körs korrekt.

## Felsöka JavaScript med Safari och IOS-felsökning {#debug-javascripts-with-safari-and-ios-debug}

Du kan felsöka appens JavaScript med utvecklarverktygen i Safari, på samma sätt som med ett webbprogram.

## Aktivera Safari Developer Tools {#enable-safari-developer-tools}

Så här aktiverar du utvecklarverktygen:

* Öppna Safaris inställningar

   * Klicka på Safari i menyraden
   * Klicka på Inställningar

* Klicka på Avancerat i inställningsfönstret

![chlimage_1-47](assets/chlimage_1-47.png)

* Markera &quot;Visa menyn Framkalla i menyraden&quot;
* Stäng inställningsfönstret

## Ansluta Safari till iOS {#connect-safari-to-ios}

Du kan ansluta Safari till en iOS-enhet eller emulator.

* Navigera till rotkatalogen för den extraherade källan i ett konsolfönster.
* Ange följande kommando så att du kan starta programmet på enheten eller emulatorn.

```xml
phonegap run <platform> --device

// -- or -- //

phonegap run <platform> --emulator
```

* Öppna Safari
* Klicka på Utveckla på menyraden
* Välj undermenyn iOS Simulator
* Klicka på home.html

![chlimage_1-48](assets/chlimage_1-48.png)

## Felsöka JavaScript med Safaris webbinspektör {#debug-javascript-with-safari-s-web-inspector}

Du kan ange brytpunkter var som helst i källan. När du interagerar med emulatorn eller enheten slutar appen att köras vid dessa brytpunkter. Du kan stega dig igenom körningen och kontrollera värdena i variabler.

* Klicka på Resurser i webbinspektören
* Navigera i källträdet och klicka på den önskade källfilen
* Klicka på radnumret bredvid för att lägga till en brytpunkt
* Interagera med enhet eller emulator

![chlimage_1-49](assets/chlimage_1-49.png)

* Använd kontrollknapparna för att fortsätta köra, stega över, stega in i och ta bort metoder:

![Fem olika funktionskontrollknappar är justerade i en vågrät rad.](do-not-localize/chlimage_1-4.png)

>[!NOTE]
>
>Håll musen om du vill se variabelvärdena i den aktuella metoden.

## Nästa steg {#the-next-steps}

När du har lärt dig mer om hur du utvecklar appar med PhoneGap CLI läser du [Åtkomst till enhetsfunktioner](/help/mobile/phonegap-access-device-features.md).
