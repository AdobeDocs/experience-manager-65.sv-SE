---
title: Komponenter i överläggsgrupper
description: Lär dig mer om att täcka över en standardkomponent så att du kan ändra utseendet eller beteendet för en komponent globalt, för alla relativa referenser till komponenten.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
docset: aem65
exl-id: 18376805-c2ed-439a-abc7-e9657afe8baf
solution: Experience Manager
feature: Communities
role: Developer
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '267'
ht-degree: 0%

---

# Komponenter i överläggsgrupper {#overlay-communities-components}

Avsikten med att [täcka över](/help/communities/client-customize.md#overlays) en standardkomponent är att ändra utseendet eller beteendet för en komponent globalt, för alla relativa referenser till komponenten. Det är beroende av vilken typ av sling som du kan lösa till mappen /apps innan du söker i mappen /libs. Sökvägen till komponenten är alltså identisk med sökvägen till standardkomponenten, förutom att den finns i mappen /apps och inte i mappen /libs.

## Exempel {#example}

**Komponenten för överläggskommentarer**

Anta att du vill ändra kommentarsfunktionen så att den matchar webbplatsens design genom att ändra kommentarsrubriken så att avataren inte längre visas för kommentarer. Lösningarna för att dölja avataren använder antingen CSS eller, som beskrivs här, åsidosätter header.jsp i programmappen så att HTML som innehåller avataren aldrig skickas till klienten.

Om du vill lägga över kommentarer måste du:

1. [Skapa kommentarsida](/help/communities/overlay-create-comments-page.md)
1. [Skapa noder](/help/communities/overlay-create-nodes.md)
1. [Ändra utseendet](/help/communities/overlay-alter-appearance.md)

**Meddelanden om övertäckning**

Anta att du vill anpassa meddelandet med e-postmeddelanden genom att [ersätta](/help/communities/client-customize.md#overlays) mallarna på `/libs/settings/community/templates/email/html`.

Anta till exempel att du vill redigera e-postmeddelandena om omnämnanden (för en specifik webbgruppskomponent där UGC skapas). I sådana fall lägger du till ett **if**-villkor för verb **mention** i mallarna för de komponenter som du aktiverade stödet för **@mentions** för.

```java
{{#equals this.verb "mention"}}\
    A new mention <a href="{{objectUrl}}">comment</a> {{#if this.target.properties.[jcr:title]}}to the article "{{{target.displayName}}}" {{/if}}was added by {{{user.name}}} on {{dateUtil this.published format="EEE, d MMM yyyy HH:mm:ss z"}}.\n \
{{/equals}}\
```

Om du vill ändra e-postmeddelandemallen för @mention i bloggkommentarer placerar du ut mallen utanför rutan på: `/libs/settings/community/templates/email/html/social.journal.components.hbs.comment/en`
