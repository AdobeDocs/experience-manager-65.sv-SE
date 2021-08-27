---
title: Innehållsfragment – ta bort överväganden
description: Granska dessa viktiga aspekter innan du definierar dina regler för borttagning av innehållsfragment i AEM. Content Fragments är ett kraftfullt verktyg för att leverera headless-innehåll, och konsekvenserna av att ta bort dem måste noggrant övervägas.
feature: Content Fragments
role: User
source-git-commit: 94145c6428f61e31f6784a3d6ea67aa8d81cedd6
workflow-type: tm+mt
source-wordcount: '509'
ht-degree: 9%

---

# Innehållsfragment – ta bort överväganden {#content-fragments-delete-considerations}

Granska dessa viktiga aspekter innan du definierar dina regler för borttagning av innehållsfragment i AEM. Content Fragments är ett kraftfullt verktyg för att leverera headless-innehåll, och konsekvenserna av att ta bort dem måste noggrant övervägas.

## Behörigheter - ta bort eller inte ta bort {#permissions-delete-or-not-delete}

Möjligheten att ta bort innehåll är kraftfull, men potentiellt känslig, och många branscher måste begränsa och styra hur dessa behörigheter distribueras.

När det gäller borttagningsbehörigheter måste innehållsfragment beaktas på två nivåer:

1. **Innehållsfragmentet som en enskild enhet.**

   * **Användningsfall**: En användare som behöver redigera/uppdatera ett innehållsfragment -  **och ta bort ett helt fragment**.
   * **Behörigheter**: Behörigheten  [](/help/sites-administering/security.md#actions) Ta bort kan  [tilldelas via användar- och/eller grupphantering](/help/sites-administering/security.md#managing-permissions).

2. **De flera underenheter som utgör ett innehållsfragment. till exempel variationer, undernoder.**

   Den grundläggande åtgärden i redigeraren för innehållsfragment kräver att sådana tillfälliga underelement kan tas bort. t.ex. vid manipulering av variationer, även när du redigerar metadata eller hanterar associerat innehåll.

   * **Användningsfall**: En användare som behöver redigera/uppdatera ett innehållsfragment -  **utan att kunna ta bort ett helt fragment**.
   * **Behörigheter**: Se  [Behörigheter krävs endast](#permissions-required-for-editor-functionality-only) för redigeringsfunktionen.

>[!NOTE]
>
>När en användare inte har någon [Ta bort](/help/sites-administering/security.md#actions)-behörighet fungerar redigeraren för innehållsfragment i läget *skrivskyddad*.

>[!NOTE]
>
>Se även [Granska åtgärder för användarhantering i AEM](/help/sites-administering/audit-user-management-operations.md).

## Behörigheter krävs endast för redigeringsfunktionen {#permissions-required-for-editor-functionality-only}

Användare som behöver redigera/uppdatera ett innehållsfragment, **utan att kunna ta bort ett helt fragment**, måste tilldelas specifika behörigheter, eftersom grundläggande användning av redigeraren för innehållsfragment kräver att tillfälliga underelement kan tas bort.

t.ex. vid manipulering av variationer, även när du redigerar metadata eller hanterar associerat innehåll.

>[!NOTE]
>
>Borttagningsbehörigheterna, som krävs för att redigera/uppdatera ett innehållsfragment, ingår i behörigheten Ta bort [som tilldelats via Användare och/eller Grupphantering](/help/sites-administering/security.md#managing-permissions).

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

* För noden `jcr:content`för alla innehållsfragment:

   * `jcr:addChildNodes`,  `jcr:modifyProperties` och  `jcr:removeChildNodes`

* För alla noder under `jcr:content` i alla innehållsfragment:

   * `jcr:addChildNodes`,  `jcr:modifyProperties` och  `jcr:removeChildNodes`,  `jcr:removeNode`

Dessa `remove`-privilegier måste vara [administrerade med åtkomstkontrollistor i CRXDE Lite](/help/sites-administering/user-group-ac-admin.md#access-right-management).

Behörigheterna `add` och `modify` kan också administreras i CRXDE Lite eller med användarhanteringskonsolen.

Definitionen av `remove`-behörigheten för en grupp `content-authors-no-delete`:

![cf-delete-03](assets/cf-delete-03.png)
