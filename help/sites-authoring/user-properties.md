---
title: Konfigurerar din kontomiljö
seo-title: Configuring Your Account Environment
description: AEM ger dig möjlighet att konfigurera ditt konto och vissa aspekter av författarmiljön
seo-description: AEM provides you with the capability to configure your account and certain aspects of the author environment
uuid: ef31be29-5c18-4dc9-ad51-fb001588b31e
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: b610e19c-f8d9-4ae2-b056-9fd5cf541261
docset: aem65
exl-id: 6079431d-7d08-4973-8bb4-a8d10626a795
source-git-commit: 259f257964829b65bb71b5a46583997581a91a4e
workflow-type: tm+mt
source-wordcount: '519'
ht-degree: 4%

---

# Konfigurerar din kontomiljö{#configuring-your-account-environment}

AEM ger dig möjlighet att konfigurera ditt konto och vissa aspekter av författarmiljön.

Med alternativet [Användare](/help/sites-authoring/user-properties.md#user-settings) i [sidhuvudet](/help/sites-authoring/basic-handling.md#the-header) och den tillhörande dialogrutan [Mina inställningar](#userpreferences) kan du ändra dina användaralternativ.

Börja med att öppna [Användare](/help/sites-authoring/user-properties.md#user-settings) i sidhuvudet.

## Användarinställningar {#user-settings}

The **Användare** dialogrutan ger dig tillgång till:

* Personifiera som

   * Med [Personifiera som](/help/sites-administering/security.md#impersonating-another-user) funktioner som en användare kan arbeta för en annan användares räkning.

* Profil

   * En praktisk länk till [användarinställningar](/help/sites-administering/security.md))

* [Mina inställningar](/help/sites-authoring/user-properties.md#my-preferences)

   * Ange olika inställningar som är unika för din användare

![screen_shot_2018-03-20at103808](assets/screen_shot_2018-03-20at103808.png)

### Mina inställningar {#my-preferences}

The **Mina inställningar** öppnas via [Användare](/help/sites-authoring/user-properties.md#user-settings) i sidhuvudet.

Varje användare kan ange vissa egenskaper för sig själv.

![screen-shot_2019-03-05at100322](assets/screen-shot_2019-03-05at100322.png)

* **Språk**

  Detta definierar vilket språk som ska användas för redigeringsmiljöns användargränssnitt. Välj önskat språk i listan.

  Den här konfigurationen används även för det klassiska användargränssnittet.

* **Fönsterhantering**

  Detta definierar beteendet för att öppna fönster. Välj något av följande:

   * **Flera fönster** (Standard)

      * Sidorna öppnas i ett nytt fönster.

   * **Ett fönster**

      * Sidorna öppnas i det aktuella fönstret.

* **Visa skrivbordsåtgärder för Assets**

  Det här alternativet kräver AEM datorprogram.

* **Anteckningsfärg**

  Detta definierar den standardfärg som används när anteckningar görs.

   * Klicka på färgblocket för att öppna väljaren för färgrutor och markera en färg.
   * Du kan också ange hexkoden för önskad färg i fältet.

* **Relativ datumpresentation**

  För att förbättra läsbarheten kommer AEM att återge datum inom de senaste sju dagarna som relativa datum (till exempel för tre dagar sedan) och äldre datum som exakta datum (till exempel den 20 mars 2017).

  Det här alternativet definierar hur datum i systemet visas. Följande alternativ är tillgängliga:

   * **Visa alltid exakt datum**: Det exakta datumet visas alltid (aldrig ett relativt datum).
   * **1 dag**: Det relativa datumet visas för datum inom en dag, annars visas ett exakt datum.

   * **7 dagar (standard)**: Det relativa datumet visas för datum inom sju dagar, i annat fall visas ett exakt datum.

   * **1 månad**: Det relativa datumet visas för datum inom en månad, annars visas ett exakt datum.

   * **1 år**: Det relativa datumet visas för datum inom ett år, annars visas ett exakt datum.

   * **Visa alltid relativt datum**: Exakta datum visas aldrig och endast relativa datum visas.

* **Aktivera kortkommandon**

  AEM stöder ett antal kortkommandon som gör redigeringen effektivare.

   * [Kortkommandon för att redigera sidor](/help/sites-authoring/page-authoring-keyboard-shortcuts.md)
   * [Kortkommandon för konsoler](/help/sites-authoring/keyboard-shortcuts.md)

  Det här alternativet aktiverar kortkommandon. Som standard är de aktiverade, men kan inaktiveras om en användare har vissa tillgänglighetskrav.

* **Använd klassisk redigeringsmiljö**

  Det här alternativet aktiverar [klassiskt användargränssnitt](/help/sites-classic-ui-authoring/home.md)-baserad framtagning av sidor. Standardgränssnittet används som standard.

* **Aktivera startsidan för resurser**

  Det här alternativet är endast tillgängligt om systemadministratören har aktiverat Assets Home Page Experience för hela organisationen.

* **Stock-konfiguration**

  Med det här alternativet kan du ange önskad Adobe Stock-konfiguration och det är bara tillgängligt om systemadministratören har aktiverat [Integrering med Adobe Stock](/help/assets/aem-assets-adobe-stock.md).
