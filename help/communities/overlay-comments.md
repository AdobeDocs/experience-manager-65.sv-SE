---
title: Komponenter för överlappande communities
seo-title: Overlay communities components
description: Komponenter för överlappande communities
seo-description: Overlay communities components
uuid: 872f7006-959a-49d2-b025-3a5abb7c6dca
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 502c0916-6c54-440c-be8c-eae56001fa26
docset: aem65
exl-id: 18376805-c2ed-439a-abc7-e9657afe8baf
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '246'
ht-degree: 0%

---

# Komponenter för överlappande communities {#overlay-communities-components}

Avsikten med [överläggning](/help/communities/client-customize.md#overlays) en standardkomponent är att ändra utseendet eller beteendet för en komponent globalt, för alla relativa referenser till komponenten. Det är beroende av vilken typ av sling som du kan lösa till mappen /apps innan du söker i mappen /libs. Sökvägen till komponenten är alltså identisk med sökvägen till standardkomponenten, förutom att den finns i mappen /apps och inte i mappen /libs.

## Exempel {#example}

**Komponenten Overlay-kommentarer**

Anta att du vill ändra kommentarsfunktionen så att den matchar webbplatsens design genom att ändra kommentarsrubriken så att avataren inte längre visas för kommentarer. Lösningarna för att dölja avataren använder antingen CSS eller, som beskrivs här, åsidosätter header.jsp i programmappen så att HTML som innehåller avataren aldrig skickas till klienten.

Om du vill lägga över kommentarer måste du:

1. [Kommentarsida](/help/communities/overlay-create-comments-page.md)
1. [Skapa noder](/help/communities/overlay-create-nodes.md)
1. [Ändra utseendet](/help/communities/overlay-alter-appearance.md)

**E-postmeddelanden om överlägg**

Anta att du vill anpassa e-postmeddelandena genom att [överläggning](/help/communities/client-customize.md#overlays) mallarna på **/libs/settings/community/templates/email/html**.

Om du till exempel vill ändra meddelandena om omnämnanden (för en specifik communitykomponent där ugc skapas) lägger du till en **if** villkor för verb **omnämnande** i mallarna för de komponenter som du har aktiverat **@menations** support.

```java
{{#equals this.verb "mention"}}\
    A new mention <a href="{{objectUrl}}">comment</a> {{#if this.target.properties.[jcr:title]}}to the article "{{{target.displayName}}}" {{/if}}was added by {{{user.name}}} on {{dateUtil this.published format="EEE, d MMM yyyy HH:mm:ss z"}}.\n \
{{/equals}}\
```

Om du vill ändra e-postmeddelandemallen för @mention i bloggkommentarer placerar du ut mallen utanför rutan på: `/libs/settings/community/templates/email/html/social.journal.components.hbs.comment/en`
