---
title: Innehållsfragment - Ta bort överväganden
seo-title: Innehållsfragment - Ta bort överväganden
description: Innehållsfragment - Ta bort överväganden
seo-description: Innehållsfragment - Ta bort överväganden
uuid: e7ac1809-159f-4d02-ad30-dc6c246e8a04
contentOwner: aheimoz
topic-tags: content-fragments
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
content-type: reference
discoiquuid: ec21237f-9186-49b4-8039-99df4db7c14a
docset: aem65
translation-type: tm+mt
source-git-commit: 6edecebec6d64a30fd05887a56d81f80863c5213

---


# Innehållsfragment - Ta bort överväganden{#content-fragments-delete-considerations}

## Behörigheter - ta bort eller inte ta bort {#permissions-delete-or-not-delete}

Möjligheten att ta bort innehåll är kraftfull, men potentiellt känslig, och många branscher måste begränsa och styra hur dessa behörigheter distribueras.

När det gäller borttagningsbehörigheter måste innehållsfragment beaktas på två nivåer:

1. **Innehållsfragmentet som en enskild enhet.**

   * **Användningsfall**: En användare som behöver redigera/uppdatera ett innehållsfragment - **och ta bort ett helt fragment**.
   * **Behörigheter**: Behörigheten [Ta bort](/help/sites-administering/security.md#actions) kan [tilldelas via användar- och/eller grupphantering](/help/sites-administering/security.md#managing-permissions).

1. **De flera underenheter som utgör ett innehållsfragment. till exempel variationer, undernoder.**

   Den grundläggande åtgärden i redigeraren för innehållsfragment kräver att sådana tillfälliga underelement kan tas bort. t.ex. vid manipulering av variationer, även när du redigerar metadata eller hanterar associerat innehåll.

   * **Användningsfall**: En användare som behöver redigera/uppdatera ett innehållsfragment - **utan att kunna ta bort ett helt fragment**.
   * **Behörigheter**: Se [Behörigheter krävs endast](/help/assets/content-fragments-delete.md#permissions-required-for-editor-functionality-only)för redigeringsfunktionen.

>[!NOTE]
>
>När en användare inte har någon [borttagningsbehörighet](/help/sites-administering/security.md#actions) fungerar redigeraren för innehållsfragment i *skrivskyddat* läge.

>[!NOTE]
>
>Se även [Granska åtgärder för användarhantering i AEM](/help/sites-administering/audit-user-management-operations.md).

## Behörigheter krävs endast för redigeringsfunktionen {#permissions-required-for-editor-functionality-only}

För användare som behöver redigera/uppdatera ett innehållsfragment, **utan att tillåta dem att ta bort ett helt fragment**, måste specifika behörigheter tilldelas eftersom grundläggande åtgärder i innehållsfragmentredigeraren kräver att tillfälliga underelement kan tas bort.

t.ex. vid manipulering av variationer, även när du redigerar metadata eller hanterar associerat innehåll.

>[!NOTE]
>
>De borttagningsbehörigheter som krävs för att redigera/uppdatera ett innehållsfragment ingår i borttagningsbehörigheten som [tilldelats via användar- och/eller grupphantering](/help/sites-administering/security.md#managing-permissions).

Behörigheterna som behövs för att redigera/uppdatera ett fragment måste tillämpas på antingen noden som innehåller innehållsfragmentet eller på en lämplig överordnad nod (på alla nivåer under `/content/dam`). När den tilldelas till en sådan överordnad nod tillämpas behörigheterna på alla noder i den grenen.

En mapp som till exempel kommer att innehålla alla innehållsfragment, till exempel:

* `/content/dam/contentfragments`

>[!CAUTION]
>
>Det går också att ange behörigheter för `/content/dam` eftersom alla innehållsfragment lagras här.
>
>Den här åtgärden tillämpar dock samma borttagningsbehörigheter på *alla* andra resurstyper.

Behörigheten som krävs för att en viss användare och/eller grupp ska kunna redigera/uppdatera ett innehållsfragment är:

>[!NOTE]
>
>I den här listan visas alla behörigheter som krävs, inte bara borttagningsbehörighet.

* För noderna eller mapparna för innehållsfragment:

   * `jcr:addChildNodes`, `jcr:modifyProperties`

* För `jcr:content`noden för alla innehållsfragment:

   * `jcr:addChildNodes`, `jcr:modifyProperties` och `jcr:removeChildNodes`

* För alla noder under `jcr:content` alla innehållsfragment:

   * `jcr:addChildNodes`, `jcr:modifyProperties` och `jcr:removeChildNodes`, `jcr:removeNode`

Dessa `remove` behörigheter måste [administreras med åtkomstkontrollistor i CRXDE Lite](/help/sites-administering/user-group-ac-admin.md#access-right-management).

Behörigheterna `add` och `modify` behörigheterna kan också administreras i CRXDE Lite eller med hjälp av användarhanteringskonsolen.

Definitionen av en grupps `remove` behörigheter `content-authors-no-delete`:

![cf-delete-03](assets/cf-delete-03.png)

