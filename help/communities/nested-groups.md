---
title: Skapar kapslade grupper
seo-title: Skapar kapslade grupper
description: Skapa kapslade grupper
seo-description: Skapa kapslade grupper
uuid: b377dc1b-bbb6-41c9-b0fc-8281e1410685
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: introduction
content-type: reference
discoiquuid: 752235d2-21ac-46d2-82ed-5fec09c645e9
docset: aem65
translation-type: tm+mt
source-git-commit: c9fa5624a59f4b9a6f970628b03bbd8b7a277a73
workflow-type: tm+mt
source-wordcount: '539'
ht-degree: 4%

---


# Skapar kapslade grupper{#authoring-nested-groups}

## Skapar grupper på författare {#creating-groups-on-author}

Från global navigering i AEM Author:

* Välj **[!UICONTROL Communities] > **[!UICONTROL Sites]**.
* Välj **[!UICONTROL engage folder]** att öppna den.
* Välj kortet för den **[!UICONTROL Getting Started Tutorial]** engelska webbplatsen.

   * Välj kortbilden.
   * Markera *inte* en ikon.

Resultatet blir att [gruppkonsolen](/help/communities/groups.md)nås:

![chlimage_1-91](assets/chlimage_1-91.png)

Gruppfunktionen visas som en mapp där instanser av grupper skapas. Markera mappen Grupper för att öppna den. Gruppen som skapades vid publicering visas.

![chlimage_1-92](assets/chlimage_1-92.png)

## Skapa huvudkonst {#create-main-arts-group}

Den här gruppen kan skapas eftersom webbplatsstrukturen för interaktion innehåller en gruppfunktion. Konfigurationen av funktionen i platsens `Reference Template` standardinställningar tillåter val av aktiverad gruppmall. Därför är mallen som väljs för den nya gruppen `Reference Group`.

De här konsolerna liknar konsolen Communities Sites.

* Välj **[!UICONTROL Create Group]**.

* **Community-gruppmall**:

   * **[!UICONTROL Community Group Title]**: Konst.
   * **[!UICONTROL Community Group Description]**: En överordnad grupp för olika konstnärliga grupper.
   * **[!UICONTROL Community Group Root]**: *lämna som standard*.
   * **[!UICONTROL Additional Available Community Group Language(s)]**: Använd listrutan för att välja tillgängliga språk för communitygrupper. Menyn innehåller alla språk som den överordnade communitywebbplatsen skapas i. Användarna kan välja mellan dessa språk för att skapa grupper i flera språkområden i det här steget. Samma grupp skapas på flera angivna språk i gruppkonsolen för respektive communityplats.
   * **[!UICONTROL Community Group Name]**: konst.
   * **[!UICONTROL Template]**: listruta för att välja `Reference Group.`
   * Välj **[!UICONTROL Next]**.

![Kapslade communitygrupper](assets/parent-to-nestedgroup.png)

Fortsätt genom de andra panelerna med följande inställningar:

* **[!UICONTROL Design]**

   * Ändra designen eller tillåt den överordnade standardwebbplatsens design.
   * Välj **[!UICONTROL Next]**.

* **[!UICONTROL Settings]**

   * **[!UICONTROL Moderation]**

      * Lämna tomt (ärv från överordnad plats).
   * **[!UICONTROL Membership]**

      * Använd standard `Optional Membership.`

      * **[!UICONTROL Thumbnail]**
         * `optional.*`
      * **[!UICONTROL Select Next]**.



* Välj **[!UICONTROL Create]**.

### Kapslade grupper inom konst {#nesting-groups-within-arts-group}

Mappen `groups` innehåller nu två grupper (uppdatera sidan).

![Kapsla grupper](assets/create-community-group.png)

#### Publicera grupp {#publish-group}

Innan du skapar grupper som är kapslade i `arts` gruppen håller du pekaren över `arts` kortet och väljer publiceringsikonen för att publicera det.

![liking-component](assets/liking-component.png)

Vänta på bekräftelse på att gruppen publicerades.

![chlimage_1-94](assets/chlimage_1-94.png)

Gruppen bör också innehålla en `arts` `groups` mapp, men en som är tom och där nya grupper kan skapas. Navigera till gruppmappen för konst och skapa 3 kapslade grupper, där var och en har olika medlemsinställningar:

1. **[!UICONTROL Visual]**

   * Titel: `Visual Arts`
   * Namn: `visual`
   * Mall: `Reference Group`
   * Medlemskap: välj `Optional Membership`, en offentlig grupp, öppen för alla medlemmar.

1. **[!UICONTROL Auditory]**

   * Titel: `Auditory Arts`
   * Namn: `auditory`
   * Mall: `Reference Group`
   * Medlemskap: välj `Required Membership`, en öppen grupp, som är tillgänglig för medlemmar att gå med i.

1. **[!UICONTROL History]**

   * Titel: `Art History`
   * Namn: `history`
   * Mall: `Reference Group`
   * Medlemskap: välj `Restricted Membership`, en hemlig grupp, som bara är synlig för inbjudna medlemmar. Du kan till exempel bjuda in [demoanvändare](/help/communities/tutorials.md#demo-users) `emily.andrews@mailinator.com`.

Uppdatera sidan om du vill se alla tre kapslade grupper (undergrupper).

Så här navigerar du till de kapslade grupperna från konsolen Webbplatser för communities:

* Välj **[!UICONTROL engage folder]**
* Välj **[!UICONTROL Getting Started Tutorial card]**
* Välj **[!UICONTROL Groups]** mapp
* Välj **[!UICONTROL arts card]**
* Välj **[!UICONTROL Groups]** mapp

![configure-läning](assets/configure-liking.png)

## Förlagskoncern {#publishing-groups}

![chlimage_1-96](assets/chlimage_1-96.png)

Efter publicering av den huvudsakliga communitywebbplatsen:

* Publicera varje grupp individuellt:

   * Väntar på bekräftelse av att gruppen publicerades.

* Publicera den överordnade gruppen innan du publicerar eventuella grupper som är kapslade i:

   * Alla grupper måste publiceras uppifrån och ned.

![chlimage_1-97](assets/chlimage_1-97.png)

## Experience on Publish {#experience-on-publish}

Det går att uppleva de olika grupperna när de loggas in, till exempel med de [demoanvändare](/help/communities/tutorials.md#demo-users) som används för:

* Medlem i konst-/historikgrupp: emily.andrews@mailinator.com/lösenord
   * Den begränsade (hemliga) gruppen, konst/historik, är synlig:
   * Kan se valfria (offentliga) grupper.
   * Kan förena begränsade (öppna) grupper.

* Gruppansvarig: aaron.mcdonald@mailinator.com/lösenord

   * Kan se valfria (offentliga) grupper.
   * Kan förena begränsade (öppna) grupper.
   * Kan inte se begränsade (hemliga) grupper.

Gå till konsolerna [Communities](/help/communities/members.md) Members and Groups för författare om du vill lägga till andra användare i olika medlemsgrupper som motsvarar communitygrupperna.

