---
title: Felsökning för användargrupper
description: Felsökning av användargrupper, inklusive kända fel
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: ef4f4108-c485-4e2e-a58f-ff64eee9937e
source-git-commit: 3d80ea6a6fbad05afcdd1f41f4b9de70921ab765
workflow-type: tm+mt
source-wordcount: '350'
ht-degree: 0%

---

# Felsökning för användargrupper {#troubleshooting}

Det här avsnittet innehåller vanliga problem och kända problem vid felsökning av communityn.

## Kända fel {#known-issues}

### Dispatcher - uppdatering misslyckades {#dispatcher-refetch-fails}

När du använder Dispatcher 4.1.5 med en nyare version av Jetty kan en uppdatering resultera i&quot;Det går inte att ta emot svar från fjärrservern&quot; efter att begäran har fått timeout.

Du kan lösa problemet genom att använda Dispatcher 4.1.6 eller senare.

### Det går inte att komma åt foruminlägg efter uppgradering från CQ 5.4 {#cannot-access-forum-post-after-upgrading-from-cq}

Om ett forum skapades på CQ 5.4 och ämnen publicerades, och webbplatsen sedan uppgraderades till AEM 5.6.1 eller senare, kan ett försök att visa befintliga inlägg resultera i ett fel på sidan:

Ogiltigt mönstertecken &#39;a&#39; Kan inte hantera begäran till `/content/demoforums/forum-test.html` på den här servern och loggarna innehåller följande:

```xml
20.03.2014 22:49:35.805 ERROR [10.177.45.32 [1395380975744] GET /content/demoforums/forum-test.html HTTP/1.1] com.day.cq.wcm.tags.IncludeTag Error while executing script content.jsp
org.apache.sling.api.scripting.ScriptEvaluationException:
at org.apache.sling.scripting.core.impl.DefaultSlingScript.call(DefaultSlingScript.java:388)
at org.apache.sling.scripting.core.impl.DefaultSlingScript.eval(DefaultSlingScript.java:171)
```

Problemet är att formatsträngen för com.day.cq.commons.date.RelativeTimeFormat ändrades mellan 5.4 och 5.5 så att&quot;a&quot; för&quot;ago&quot; inte längre accepteras.

All kod som använder API:t RelativeTimeFormat() måste därför ändras:

* Från: `final RelativeTimeFormat fmt = new RelativeTimeFormat("r a", resourceBundle);`
* Till: `final RelativeTimeFormat fmt = new RelativeTimeFormat("r", resourceBundle);`

Felet skiljer sig åt när det gäller författare och publicering. På författaren misslyckas det utan att det märks och forumämnena visas helt enkelt inte. Vid publicering genereras ett fel på sidan.

Se [com.day.cq.commons.date.RelativeTimeFormat](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/commons/date/RelativeTimeFormat.html) API för mer information.

## Vanliga problem {#common-concerns}

### Varning i loggar: Borttagna handtag {#warning-in-logs-handlebars-deprecated}

Under start (inte den första - men var tredje) kan följande varning visas i loggarna:

* `11.04.2014 08:38:07.223 WARN [FelixStartLevel]com.github.jknack.handlebars.Handlebars Helper 'i18n'` har ersatts med `com.adobe.cq.social.handlebars.I18nHelper@15bac645`

Den här varningen kan ignoreras som `jknack.handlebars.Handlebars`, används av [SCF](scf.md#handlebarsjavascripttemplatinglanguage), har ett eget i18n-hjälpverktyg. Vid start ersätts den med en AEM [i18n - hjälp](handlebars-helpers.md#i-n). Den här varningen genereras av tredjepartsbiblioteket för att bekräfta åsidosättningen av en befintlig hjälpreda.

### Varning i loggar: OakResourceListener processOsgiEventQueue {#warning-in-logs-oakresourcelistener-processosgieventqueue}

Om du publicerar flera forum för sociala communityer kan det resultera i stora mängder varnings- och informationsloggar från OakResourceListener processOsgiEventQueue.

Dessa varningar kan ignoreras.

```xml
23.04.2014 14:21:18.900 *WARN* [pool-5-thread-3] org.apache.sling.jcr.resource.internal.OakResourceListener processOsgiEventQueue: Resource at /var/search-collections/ugc-sc/_m.frq/jcr:content not found, which is not expected for an added or modified node
23.04.2014 14:21:18.908 *WARN* [pool-5-thread-3] org.apache.sling.jcr.resource.internal.OakResourceListener processOsgiEventQueue: Resource at /var/search-collections/ugc-sc/_m.prx/jcr:content not found, which is not expected for an added or modified node
23.04.2014 14:21:18.909 *WARN* [pool-5-thread-3] org.apache.sling.jcr.resource.internal.OakResourceListener processOsgiEventQueue: Resource at /var/replication/data/1f799fb4-0aeb-4660-aadb-705657f16048/67/67699ab5-9d57-4c79-a755-2727ba9e6452/jcr:content not found, which is not expected for an added or modified node
23.04.2014 14:21:18.909 *WARN* [pool-5-thread-3] org.apache.sling.jcr.resource.internal.OakResourceListener processOsgiEventQueue: Resource at /var/replication/data/1f799fb4-0aeb-4660-aadb-705657f16048/67/67699ab5-9d57-4c79-a755-2727ba9e6452/jcr:content not found, which is not expected for an added or modified node
23.04.2014 14:21:18.990 *WARN* [pool-5-thread-3] org.apache.sling.jcr.resource.internal.OakResourceListener processOsgiEventQueue: Resource at /var/replication/data/1f799fb4-0aeb-4660-aadb-705657f16048/b9/b91f1690-87e8-41d8-a78e-cd2259f837c8/jcr:content not found, which is not expected for an added or modified node
23.04.2014 14:21:18.990 *WARN* [pool-5-thread-3] org.apache.sling.jcr.resource.internal.OakResourceListener processOsgiEventQueue: Resource at /var/replication/data/1f799fb4-0aeb-4660-aadb-705657f16048/b9/b91f1690-87e8-41d8-a78e-cd2259f837c8/jcr:content not found, which is not expected for an added or modified node
```

### Fel i loggar: NoClassDefFoundError för IndexElementFactory {#error-in-logs-noclassdeffounderror-for-indexelementfactory}

Om du uppgraderar AEM 5.6.1 GA till den senaste cq-socialcommunities-pkg-1.4.x eller till AEM 6.0 uppstår fel i loggfilen under starten, vilket ger en problemlösning som visas av det fel som inte visas vid omstart.

```xml
14.11.2013 20:52:39.453 ERROR [Apache Sling JCR Resource Event Queue Processor for path '/'] com.adobe.cq.social.storage.index.impl.IndexService Error occurred while processing event java.util.ConcurrentModificationException
14.11.2013 20:52:40.716 ERROR [OsgiInstallerImpl] com.adobe.cq.social.cq-social-commons [CommentListProvider] Error during instantiation of the implementation object (java.lang.NoClassDefFoundError: com/adobe/cq/social/storage/index/IndexElementFactory) java.lang.NoClassDefFoundError: com/adobe/cq/social/storage/index/IndexElementFactory
14.11.2013 20:52:40.717 ERROR [OsgiInstallerImpl] com.adobe.cq.social.cq-social-commons [CommentListProvider] Failed creating the component instance; see log for reason
```
