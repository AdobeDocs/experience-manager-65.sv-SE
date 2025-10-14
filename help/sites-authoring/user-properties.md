---
title: Konfigurerar din kontomiljö
description: AEM ger dig möjlighet att konfigurera ditt konto och vissa aspekter av författarmiljön
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
docset: aem65
exl-id: 6079431d-7d08-4973-8bb4-a8d10626a795
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User,Admin,Architect,Developer
source-git-commit: 9a3008553b8091b66c72e0b6c317573b235eee24
workflow-type: tm+mt
source-wordcount: '521'
ht-degree: 4%

---

# Konfigurerar din kontomiljö{#configuring-your-account-environment}

AEM ger dig möjlighet att konfigurera ditt konto och vissa aspekter av författarmiljön.

Med alternativet [Användare](/help/sites-authoring/user-properties.md#user-settings) i [sidhuvudet](/help/sites-authoring/basic-handling.md#the-header) och den tillhörande dialogrutan [Mina inställningar](#userpreferences) kan du ändra dina användaralternativ.

Börja med att gå till alternativet [Användare](/help/sites-authoring/user-properties.md#user-settings) i sidhuvudet.

## Användarinställningar {#user-settings}

Dialogrutan **Användare** ger dig åtkomst till:

* Personifiera som

   * Med funktionen [Personifiera som](/help/sites-administering/security.md#impersonating-another-user) kan en användare arbeta för en annan användares räkning.

* Profil

   * Erbjuder en praktisk länk till dina [användarinställningar](/help/sites-administering/security.md))

* [Mina inställningar](/help/sites-authoring/user-properties.md#my-preferences)

   * Ange olika inställningar som är unika för användaren

![screen_shot_2018-03-20at103808](assets/screen_shot_2018-03-20at103808.png)

### Mina inställningar {#my-preferences}

Dialogrutan **Mina inställningar** är tillgänglig via alternativet [Användare](/help/sites-authoring/user-properties.md#user-settings) i sidhuvudet.

Varje användare kan ange vissa egenskaper för sig själv.

![screen-shot_2019-03-05at100322](assets/screen-shot_2019-03-05at100322.png)

* **Språk**

  Detta definierar vilket språk som ska användas för redigeringsmiljöns användargränssnitt. Välj önskat språk i listan.

  Den här konfigurationen används även för det klassiska användargränssnittet.

* **Fönsterhantering**

  Detta definierar beteendet för att öppna fönster. Välj antingen:

   * **Flera fönster** (standard)

      * Sidorna öppnas i ett nytt fönster.

   * **Ett fönster**

      * Sidorna öppnas i det aktuella fönstret.

* **Visa skrivbordsåtgärder för Assets**

  Det här alternativet kräver ett AEM datorprogram för att kunna användas.

* **Anteckningsfärg**

  Detta definierar den standardfärg som används när anteckningar görs.

   * Klicka på färgblocket så att du kan öppna färgrutevälaren och välja en färg.
   * Du kan också ange hexkoden för önskad färg i fältet.

* **Relativ datumpresentation**

  För att förbättra läsbarheten återges datum inom de senaste sju dagarna som relativa datum (till exempel för tre dagar sedan) och äldre datum som exakta datum (till exempel den 20 mars 2017).

  Det här alternativet definierar hur datum i systemet visas. Följande alternativ är tillgängliga:

   * **Visa alltid exakt datum**: Det exakta datumet visas alltid (aldrig ett relativt datum).
   * **1 Dag**: Det relativa datumet visas för datum inom en dag, annars visas ett exakt datum.

   * **7 dagar (standard)**: Det relativa datumet visas för datum inom sju dagar, annars visas ett exakt datum.

   * **1 Month**: Det relativa datumet visas för datum inom en månad, annars visas ett exakt datum.

   * **1 År**: Det relativa datumet visas för datum inom ett år, annars visas ett exakt datum.

   * **Visa alltid relativt datum**: Exakta datum visas aldrig och endast relativa datum visas.

* **Aktivera kortkommandon**

  AEM har stöd för flera kortkommandon som gör redigeringen effektivare.

   * [Kortkommandon för redigering av sidor](/help/sites-authoring/page-authoring-keyboard-shortcuts.md)
   * [Kortkommandon för konsoler](/help/sites-authoring/keyboard-shortcuts.md)

  Det här alternativet aktiverar kortkommandon. Som standard är de aktiverade, men kan inaktiveras, till exempel om en användare har vissa tillgänglighetskrav.

* **Använd klassisk redigeringsmiljö**

  Med det här alternativet aktiveras [klassisk gränssnittsbaserad &#x200B;](/help/sites-classic-ui-authoring/classic-page-author-first-steps.md)-sidredigering. Standardgränssnittet används som standard.

* **Aktivera Assets hemsida**

  Det här alternativet är endast tillgängligt om systemadministratören har aktiverat Assets hemsida för hela organisationen.

* **Stock-konfiguration**

  Med det här alternativet kan du ange den önskade Adobe Stock-konfigurationen och det är bara tillgängligt om systemadministratören har aktiverat [Adobe Stock-integrering](/help/assets/aem-assets-adobe-stock.md).
