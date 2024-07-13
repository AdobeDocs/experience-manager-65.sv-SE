---
title: Skapar kapslade grupper
description: Lär dig hur du skapar kapslade grupper för en Adobe Experience Manager Communities-webbplats.
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: introduction
content-type: reference
docset: aem65
exl-id: 55803b7a-9064-4392-9cc2-9f113fa8dc29
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '548'
ht-degree: 0%

---

# Skapar kapslade grupper{#authoring-nested-groups}

## Skapar grupper på författare {#creating-groups-on-author}

Från global navigering AEM Author-instansen:

* Välj **[!UICONTROL Communities]** > **[!UICONTROL Sites]**.
* Välj **[!UICONTROL engage folder]** för att öppna den.
* Välj kortet för webbplatsen **[!UICONTROL Getting Started Tutorial]**.

   * Välj kortbilden.
   * Markera *inte* en ikon.

Resultatet blir att [gruppkonsolen](/help/communities/groups.md) nås:

![create-group](assets/create-group.png)

Gruppfunktionen visas som en mapp där instanser av grupper skapas. Om du vill öppna den väljer du mappen Grupper. Gruppen som skapats på Publish är synlig.

![create-new-group](assets/create-new-group.png)

## Skapa huvudkonst {#create-main-arts-group}

Den här gruppen kan skapas eftersom webbplatsstrukturen för att engagera innehåller en grupps funktion. Konfigurationen av funktionen i platsens `Reference Template` tillåter som standard val av aktiverad gruppmall. Mallen som väljs för den nya gruppen är alltså `Reference Group`.

De här konsolerna liknar konsolen Communities Sites.

* Välj **[!UICONTROL Create Group]**

* **Community-gruppmall**:

   * **[!UICONTROL Community Group Title]**: Konstnärliga
   * **[!UICONTROL Community Group Description]**: En överordnad grupp för olika konstgrupper
   * **[!UICONTROL Community Group Root]**: *lämna som standard*
   * **[!UICONTROL Additional Available Community Group Language(s)]**: använd listrutan för att välja tillgängliga communitygruppsspråk. Menyn innehåller alla språk som den överordnade communitywebbplatsen skapas på. Användarna kan välja mellan dessa språk för att skapa grupper i flera språkområden i det här steget. Samma grupp skapas på flera angivna språk i gruppkonsolen för respektive communityplats.
   * **[!UICONTROL Community Group Name]**: konst
   * **[!UICONTROL Template]**: listruta för att välja `Reference Group`
   * Välj **[!UICONTROL Next]**

![Kapslade communitygrupper](assets/parent-to-nestedgroup.png)

Fortsätt genom de andra panelerna med följande inställningar:

* **[!UICONTROL Design]**

   * Ändra designen eller tillåt den överordnade standardplatsens design.
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

![Kapslar grupperna](assets/create-community-group.png)

#### Publish Group {#publish-group}

Innan du skapar grupper som är kapslade i gruppen `arts` håller du pekaren över kortet `arts` och väljer publiceringsikonen för att publicera det.

![publiceringsplats](assets/publish-site.png)

Vänta på bekräftelse på att gruppen publicerades.

![grupppublicerad](assets/group-published.png)

Gruppen `arts` ska också innehålla en `groups`-mapp, men en som är tom och i vilken nya grupper kan skapas. Navigera till gruppmappen för konst och skapa tre kapslade grupper, där var och en har olika medlemsinställningar:

1. **[!UICONTROL Visual]**

   * Titel: `Visual Arts`
   * Namn: `visual`
   * Mall: `Reference Group`
   * Medlemskap: välj `Optional Membership`, en offentlig grupp, som är öppen för alla medlemmar.

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

Uppdatera sidan så att du kan se alla tre kapslade grupper (undergrupper).

Så här navigerar du till de kapslade grupperna från konsolen Webbplatser för communities:

* Välj **[!UICONTROL engage folder]**
* Välj **[!UICONTROL Getting Started Tutorial card]**
* Välj mappen **[!UICONTROL Groups]**
* Välj **[!UICONTROL arts card]**
* Välj mappen **[!UICONTROL Groups]**

![create-new-group2](assets/create-new-group2.png)

## Förlagskoncern {#publishing-groups}

![publiceringsplats](assets/publish-site.png)

Efter publicering av den huvudsakliga communitywebbplatsen:

* Publish var för sig:

   * Väntar på bekräftelse av att gruppen publicerades.

* Publish är den överordnade gruppen innan någon grupp som är kapslad i publiceras:

   * Alla grupper måste publiceras uppifrån och ned.

![grupppublicerad](assets/group-published.png)

## Upplevelse på Publish {#experience-on-publish}

Det går att uppleva de olika grupperna när de är inloggade, till exempel med [demoanvändarna](/help/communities/tutorials.md#demo-users) som används för:

* Medlem i konst-/historikgrupp: `emily.andrews@mailinator.com/password`
   * Den begränsade (hemliga) gruppen, konst/historik, är synlig:
   * Kan se valfria (offentliga) grupper.
   * Kan förena begränsade (öppna) grupper.

* Grupphanterare: `aaron.mcdonald@mailinator.com/password`

   * Kan se valfria (offentliga) grupper.
   * Kan förena begränsade (öppna) grupper.
   * Det går inte att se begränsade (hemliga) grupper.

Gå till konsolerna [Medlemmar och grupper](/help/communities/members.md) på författaren för att lägga till andra användare i olika medlemsgrupper som motsvarar communitygrupperna.
