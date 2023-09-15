---
title: Välja användargränssnitt i AEM
description: Konfigurera vilket gränssnitt du använder för att arbeta i AEM.
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
docset: aem65
exl-id: 01cab3c3-4c0d-44d9-b47c-034de9a08cb1
source-git-commit: 4e2ee7da5424ac6677eaa2392de7803e7543d13c
workflow-type: tm+mt
source-wordcount: '733'
ht-degree: 1%

---

# Välja användargränssnitt{#selecting-your-ui}

Adobe Experience Manager (AEM) touch-enabled UI är nu standardgränssnitt och funktionsparitet har nästan uppnåtts när det gäller administration och redigering av webbplatser. Det kan dock finnas tillfällen då användaren vill växla till [klassiskt användargränssnitt](/help/sites-classic-ui-authoring/classicui.md). Det finns flera alternativ för att göra detta.

>[!NOTE]
>
>Mer information om status för funktionsparitet med det klassiska användargränssnittet finns i [Touch UI Feature Parity](/help/release-notes/touch-ui-features-status.md) -dokument.

Det finns olika platser där du kan definiera vilket användargränssnitt som ska användas:

* [Konfigurera standardgränssnittet för instansen](#configuring-the-default-ui-for-your-instance)
Detta anger standardgränssnittet som ska visas vid användarinloggning. Användaren kan åsidosätta detta och välja ett annat användargränssnitt för sitt konto eller den aktuella sessionen.

* [Ange klassisk gränssnittsredigering för ditt konto](/help/sites-authoring/select-ui.md#setting-classic-ui-authoring-for-your-account)
Detta anger att användargränssnittet ska vara standard när sidor redigeras, men användaren kan åsidosätta detta och välja ett annat användargränssnitt för sitt konto eller den aktuella sessionen.

* [Växla till det klassiska användargränssnittet för den aktuella sessionen](#switching-to-classic-ui-for-the-current-session)
Växlar till det klassiska användargränssnittet för den aktuella sessionen.

* För [vid redigering av sidor gör systemet vissa åsidosättningar i relation till användargränssnittet](#ui-overrides-for-the-editor).

>[!CAUTION]
>
>Olika alternativ för att växla till det klassiska användargränssnittet är inte omedelbart tillgängliga. De måste konfigureras för din instans.
>
>Se [Aktivera åtkomst till klassiskt gränssnitt](/help/sites-administering/enable-classic-ui.md) för mer information.

>[!NOTE]
>
>Instanser som uppgraderats från en tidigare version behåller det klassiska användargränssnittet för sidredigering.
>
>Efter uppgraderingen växlas inte sidredigering automatiskt till det beröringsaktiverade användargränssnittet, men du kan konfigurera detta med [OSGi-konfiguration](/help/sites-deploying/configuring-osgi.md) i **Tjänsten WCM för användargränssnittsläge vid redigering** ( `AuthoringUIMode` service). Se [Gränssnittsåsidosättningar för redigeraren](#ui-overrides-for-the-editor).

## Konfigurera standardgränssnittet för din instans {#configuring-the-default-ui-for-your-instance}

En systemadministratör kan konfigurera användargränssnittet som visas vid start och inloggning med [Rotmappning](/help/sites-deploying/osgi-configuration-settings.md#daycqrootmapping).

Detta kan åsidosättas av användarens standardinställningar eller sessionsinställningar.

## Ange klassisk gränssnittsredigering för ditt konto {#setting-classic-ui-authoring-for-your-account}

Varje användare har åtkomst till sina egna [användarinställningar](/help/sites-authoring/user-properties.md#userpreferences) för att definiera om de vill använda det klassiska användargränssnittet för sidredigering, i stället för standardgränssnittet.

Detta kan åsidosättas av sessionsinställningarna.

## Växla till Classic UI för den aktuella sessionen {#switching-to-classic-ui-for-the-current-session}

När du använder det beröringsaktiverade användargränssnittet kanske datoranvändare vill återgå till det klassiska användargränssnittet (endast datorer). Det finns flera metoder för att växla till det klassiska användargränssnittet för den aktuella sessionen:

* **Navigeringslänkar**

  >[!CAUTION]
  >
  >Det här alternativet för att växla till det klassiska användargränssnittet är inte omedelbart tillgängligt. Det måste konfigureras för din instans.
  >
  >
  >Se [Aktivera åtkomst till klassiskt gränssnitt](/help/sites-administering/enable-classic-ui.md) för mer information.

  Om det här alternativet är aktiverat visas en ikon (en bildskärmssymbol) när du för musen över en tillämplig konsol. Om du trycker/klickar på det här alternativet öppnas rätt plats i det klassiska användargränssnittet.

  Länkarna från **Webbplatser** till **siteadmin**:

  ![syui-01](assets/syui-01.png)

* **URL**

  Det klassiska användargränssnittet kan nås via webbadressen för välkomstskärmen på `welcome.html`. Till exempel:

  `https://localhost:4502/welcome.html`

  >[!NOTE]
  >
  >Det beröringskänsliga användargränssnittet är tillgängligt via `sites.html`. Till exempel:
  >
  >
  >`https://localhost:4502/sites.html`

### Växla till Classic UI när du redigerar en sida {#switching-to-classic-ui-when-editing-a-page}

>[!CAUTION]
>
>Det här alternativet för att växla till det klassiska användargränssnittet är inte omedelbart tillgängligt. Det måste konfigureras för din instans.
>
>Se [Aktivera åtkomst till klassiskt gränssnitt](/help/sites-administering/enable-classic-ui.md) för mer information.

Om den är aktiverad **Öppna det klassiska gränssnittet** är tillgängligt från **Sidinformation** dialog:

![syui-02](assets/syui-02.png)

### Gränssnittsåsidosättningar för redigeraren {#ui-overrides-for-the-editor}

De inställningar som definieras av en användare eller systemadministratör kan åsidosättas av systemet om det finns sidredigering.

* När du redigerar sidor:

   * Den klassiska redigeraren måste användas när sidan används `cf#` i webbadressen. Till exempel:
     `https://localhost:4502/cf#/content/geometrixx/en/products/triangle.html`

   * Den pekaktiverade redigeraren måste användas `/editor.html` i webbadressen eller när du använder en touchenhet. Till exempel:
     `https://localhost:4502/editor.html/content/geometrixx/en/products/triangle.html`

* Alla tvång är tillfälliga och gäller endast för webbläsarsessionen

   * En cookie-uppsättning är inställd beroende på om pekfunktionen är aktiverad ( `editor.html`) eller klassisk ( `cf#`) används.

* När sidor öppnas igenom `siteadmin`kontrolleras förekomsten av följande:

   * Kakan
   * En användarinställning
   * Om ingen av dem finns används de definitioner som anges i [OSGi-konfiguration](/help/sites-deploying/configuring-osgi.md) i **Tjänsten WCM för användargränssnittsläge vid redigering** ( `AuthoringUIMode` service).

>[!NOTE]
>
>If [en användare redan har definierat en inställning för sidredigering](#settingthedefaultauthoringuiforyouraccount), som inte åsidosätts genom att OSGi-egenskapen ändras.

>[!CAUTION]
>
>På grund av användningen av cookies, vilket redan har beskrivits, rekommenderas inte att du antingen:
>
>* Redigera URL:en manuellt - En URL som inte är standard kan resultera i en okänd situation och bristande funktionalitet.
>* Ha båda redigerarna öppna samtidigt - till exempel i separata fönster.
