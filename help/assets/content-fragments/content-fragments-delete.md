---
title: Innehållsfragment - Ta bort överväganden
description: Granska dessa viktiga aspekter innan du definierar dina regler för borttagning av innehållsfragment i AEM. Content Fragments är ett kraftfullt verktyg för att leverera headless-innehåll, och konsekvenserna av att ta bort dem måste noggrant övervägas.
feature: Content Fragments
role: User
exl-id: 6212457e-a171-4c33-8d19-54c26516e981
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '510'
ht-degree: 7%

---

# Innehållsfragment - Ta bort överväganden {#content-fragments-delete-considerations}

Granska dessa viktiga aspekter innan du definierar dina regler för borttagning av innehållsfragment i AEM. Content Fragments är ett kraftfullt verktyg för att leverera headless-innehåll, och konsekvenserna av att ta bort dem måste noggrant övervägas.

## Behörigheter - ta bort eller inte ta bort {#permissions-delete-or-not-delete}

Möjligheten att ta bort innehåll är kraftfull, men potentiellt känslig, och många branscher måste begränsa och styra hur dessa behörigheter distribueras.

När det gäller borttagningsbehörigheter måste innehållsfragment beaktas på två nivåer:

1. **Innehållsfragmentet som en enskild enhet.**

   * **Använd skiftläge**: En användare som behöver redigera/uppdatera ett innehållsfragment - **och ta bort ett helt fragment**.
   * **Behörigheter**: [Ta bort](/help/sites-administering/security.md#actions) behörighet kan [som tilldelats via användar- och/eller grupphantering](/help/sites-administering/security.md#managing-permissions).

2. **De flera underenheter som utgör ett innehållsfragment, till exempel variationer, undernoder.**

   Den grundläggande åtgärden i innehållsfragmentredigeraren kräver att sådana tillfälliga underelement kan tas bort. Till exempel när du ändrar variationer, även när du redigerar metadata eller hanterar associerat innehåll.

   * **Använd skiftläge**: En användare som behöver redigera/uppdatera ett innehållsfragment - **utan tillstånd att ta bort ett helt fragment**.
   * **Behörigheter**: Se [Behörigheter krävs endast för redigeringsfunktionen](#permissions-required-for-editor-functionality-only).

>[!NOTE]
>
>När en användare inte har någon [Ta bort](/help/sites-administering/security.md#actions) behörigheter, används redigeraren för innehållsfragment i *skrivskyddad* läge.

>[!NOTE]
>
>Se även [Granska åtgärder för användarhantering i AEM](/help/sites-administering/audit-user-management-operations.md).

## Behörigheter krävs endast för redigeringsfunktionen {#permissions-required-for-editor-functionality-only}

Användare som behöver redigera/uppdatera ett innehållsfragment, **utan att kunna ta bort ett helt fragment**, måste tilldelas specifika behörigheter, eftersom grundläggande användning av redigeraren för innehållsfragment kräver att tillfälliga underelement kan tas bort.

Till exempel när du ändrar variationer, även när du redigerar metadata eller hanterar associerat innehåll.

>[!NOTE]
>
>De borttagningsbehörigheter som krävs för att redigera/uppdatera ett innehållsfragment ingår i borttagningsbehörigheten [som tilldelats via användar- och/eller grupphantering](/help/sites-administering/security.md#managing-permissions).

Behörigheterna som behövs för att redigera/uppdatera ett fragment måste tillämpas på antingen noden som innehåller innehållsfragmentet eller en lämplig överordnad nod (på alla nivåer under `/content/dam`). När den tilldelas till en sådan överordnad nod tillämpas behörigheterna på alla noder i den grenen.

En mapp som till exempel kommer att innehålla alla innehållsfragment, till exempel:

* `/content/dam/contentfragments`

>[!CAUTION]
>
>Ange behörigheter för `/content/dam` är också möjligt eftersom alla innehållsfragment lagras här.
>
>Den här åtgärden använder dock samma borttagningsbehörigheter för *alla* även andra tillgångstyper.

Behörigheten som krävs för att en viss användare och/eller grupp ska kunna redigera/uppdatera ett innehållsfragment är:

>[!NOTE]
>
>I den här listan visas alla behörigheter som krävs, inte bara borttagningsbehörighet.

* För noderna eller mapparna för innehållsfragment:

   * `jcr:addChildNodes`, `jcr:modifyProperties`

* För `jcr:content`nod för alla innehållsfragment:

   * `jcr:addChildNodes`, `jcr:modifyProperties` och `jcr:removeChildNodes`

* För alla noder nedan `jcr:content` av alla innehållsfragment:

   * `jcr:addChildNodes`, `jcr:modifyProperties` och `jcr:removeChildNodes`, `jcr:removeNode`

Dessa `remove` behörighet måste [administreras med Access Control Lists, inom CRXDE Lite](/help/sites-administering/user-group-ac-admin.md#access-right-management).

The `add` och `modify` kan även administreras i CRXDE Lite eller med användarhanteringskonsolen.

Definitionen av `remove` behörighet för en grupp `content-authors-no-delete`:

![cf-delete-03](assets/cf-delete-03.png)
