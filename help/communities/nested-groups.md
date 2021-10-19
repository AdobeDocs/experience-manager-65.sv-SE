---
title: Skapar kapslade grupper
seo-title: Authoring Nested Groups
description: Skapa kapslade grupper
seo-description: Create nested groups
uuid: b377dc1b-bbb6-41c9-b0fc-8281e1410685
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: introduction
content-type: reference
discoiquuid: 752235d2-21ac-46d2-82ed-5fec09c645e9
docset: aem65
exl-id: 55803b7a-9064-4392-9cc2-9f113fa8dc29
source-git-commit: 1074843a0105df39382b64defe66fc262986b9c9
workflow-type: tm+mt
source-wordcount: '533'
ht-degree: 3%

---

# Skapar kapslade grupper{#authoring-nested-groups}

## Skapar grupper på författare {#creating-groups-on-author}

Från global navigering i AEM Author-instansen:

* Välj **[!UICONTROL Communities]** > **[!UICONTROL Sites]**.
* Välj **[!UICONTROL engage folder]** för att öppna den.
* Välj kort för **[!UICONTROL Getting Started Tutorial]** Engelsk webbplats.

   * Välj kortbilden.
   * Gör *not* välj en ikon.

Resultatet är att nå [Gruppkonsol](/help/communities/groups.md):

![create-group](assets/create-group.png)

Gruppfunktionen visas som en mapp där instanser av grupper skapas. Markera mappen Grupper för att öppna den. Gruppen som skapades vid publicering visas.

![create-new-group](assets/create-new-group.png)

## Skapa huvudkonst {#create-main-arts-group}

Den här gruppen kan skapas eftersom webbplatsstrukturen för interaktion innehåller en gruppfunktion. Konfigurationen av funktionen i platsens `Reference Template` Som standard tillåts val av aktiverade gruppmallar. Därför är den mall som väljs för den nya gruppen `Reference Group`.

De här konsolerna liknar konsolen Communities Sites.

* Välj **[!UICONTROL Create Group]**

* **Community-gruppmall**:

   * **[!UICONTROL Community Group Title]**: Konstnärliga
   * **[!UICONTROL Community Group Description]**: En överordnad grupp för olika konstgrupper
   * **[!UICONTROL Community Group Root]**: *lämna som standard*
   * **[!UICONTROL Additional Available Community Group Language(s)]**: Använd listrutan för att välja tillgängliga språk för communitygrupper. Menyn innehåller alla språk som den överordnade communitywebbplatsen skapas i. Användarna kan välja mellan dessa språk för att skapa grupper i flera språkområden i det här steget. Samma grupp skapas på flera angivna språk i gruppkonsolen för respektive communityplats.
   * **[!UICONTROL Community Group Name]**: konst
   * **[!UICONTROL Template]**: listruta för att välja `Reference Group`
   * Välj **[!UICONTROL Next]**

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

The `groups` mappen innehåller nu två grupper (uppdatera sidan).

![Kapsla grupper](assets/create-community-group.png)

#### Publicera grupp {#publish-group}

Innan du skapar grupper som är kapslade i `arts` grupp, hovra över `arts` och välj publiceringsikonen för att publicera det.

![publicera-webbplats](assets/publish-site.png)

Vänta på bekräftelse på att gruppen publicerades.

![grupppublicerad](assets/group-published.png)

The `arts` gruppen ska även innehålla `groups` men en som är tom och där nya grupper kan skapas. Navigera till gruppmappen för konst och skapa 3 kapslade grupper, där var och en har olika medlemsinställningar:

1. **[!UICONTROL Visual]**

   * Titel: `Visual Arts`
   * Namn: `visual`
   * Mall: `Reference Group`
   * Medlemskap: välj `Optional Membership`, en offentlig grupp, öppen för alla medlemmar.

1. **[!UICONTROL Auditory]**

   * Titel: `Auditory Arts`
   * Namn: `auditory`
   * Mall: `Reference Group`
   * Medlemskap: välj `Required Membership`, en öppen grupp, tillgänglig för medlemmar att gå med i.

1. **[!UICONTROL History]**

   * Titel: `Art History`
   * Namn: `history`
   * Mall: `Reference Group`
   * Medlemskap: välj `Restricted Membership`, en hemlig grupp, endast synlig för inbjudna medlemmar. Som ett exempel kan du bjuda in [demoanvändare](/help/communities/tutorials.md#demo-users) `emily.andrews@mailinator.com`.

Uppdatera sidan om du vill se alla tre kapslade grupper (undergrupper).

Så här navigerar du till de kapslade grupperna från konsolen Webbplatser för communities:

* Välj **[!UICONTROL engage folder]**
* Välj **[!UICONTROL Getting Started Tutorial card]**
* Välj **[!UICONTROL Groups]** mapp
* Välj **[!UICONTROL arts card]**
* Välj **[!UICONTROL Groups]** mapp

![create-new-group2](assets/create-new-group2.png)

## Förlagskoncern {#publishing-groups}

![publicera-webbplats](assets/publish-site.png)

Efter publicering av den huvudsakliga communitywebbplatsen:

* Publicera varje grupp individuellt:

   * Väntar på bekräftelse av att gruppen publicerades.

* Publicera den överordnade gruppen innan du publicerar eventuella grupper som är kapslade i:

   * Alla grupper måste publiceras uppifrån och ned.

![grupppublicerad](assets/group-published.png)

## Experience on Publish {#experience-on-publish}

Det går att uppleva de olika grupperna när de loggas in, till exempel med [demoanvändare](/help/communities/tutorials.md#demo-users) används för:

* Medlem i konst-/historikgrupp: emily.andrews@mailinator.com/lösenord
   * Den begränsade (hemliga) gruppen, konst/historik, är synlig:
   * Kan se valfria (offentliga) grupper.
   * Kan förena begränsade (öppna) grupper.

* Gruppansvarig: aaron.mcdonald@mailinator.com/lösenord

   * Kan se valfria (offentliga) grupper.
   * Kan förena begränsade (öppna) grupper.
   * Kan inte se begränsade (hemliga) grupper.

Åtkomst till webbgrupper [Konsoler för medlemmar och grupper](/help/communities/members.md) om författare för att lägga till andra användare i olika medlemsgrupper som motsvarar communitygrupperna.
