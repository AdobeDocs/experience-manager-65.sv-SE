---
title: Felsökning
seo-title: Felsökning
description: Felsökning av användargrupper, inklusive kända fel
seo-description: Felsökning av användargrupper, inklusive kända fel
uuid: 99225430-fa2a-4393-ae5a-18b19541c358
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: cdb2d80a-2fbf-4ee6-b89b-b5d74e6d3bfc
translation-type: tm+mt
source-git-commit: 5128a08d4db21cda821de0698b0ac63ceed24379

---


# Felsökning {#troubleshooting}

Detta avsnitt innehåller vanliga problem och kända problem.

## Kända fel {#known-issues}

### Dispatcher - uppdatering misslyckades {#dispatcher-refetch-fails}

När du använder Dispatcher 4.1.5 med en nyare version av Jetty kan en uppdatering resultera i&quot;Det går inte att ta emot svar från fjärrservern&quot; efter att begäran har fått timeout.

Du kan lösa problemet genom att använda Dispatcher 4.1.6 eller senare.

### Det går inte att komma åt foruminlägg efter uppgradering från CQ 5.4 {#cannot-access-forum-post-after-upgrading-from-cq}

Om ett forum skapades på CQ 5.4 och ämnen publicerades, och webbplatsen sedan uppgraderades till AEM 5.6.1 eller senare, kan ett försök att visa befintliga inlägg resultera i ett fel på sidan:

ogiltigt mönstertecken &#39;a&#39;Kan inte hantera begäran till /content/demoforums/forum-test.html på den här servern

Loggarna innehåller följande:

```xml
20.03.2014 22:49:35.805 ERROR [10.177.45.32 [1395380975744] GET /content/demoforums/forum-test.html HTTP/1.1] com.day.cq.wcm.tags.IncludeTag Error while executing script content.jsp
org.apache.sling.api.scripting.ScriptEvaluationException:
at org.apache.sling.scripting.core.impl.DefaultSlingScript.call(DefaultSlingScript.java:388)
at org.apache.sling.scripting.core.impl.DefaultSlingScript.eval(DefaultSlingScript.java:171)
```

Problemet är att formatsträngen för com.day.cq.commons.date.RelativeTimeFormat ändrades mellan 5.4 och 5.5 så att&quot;a&quot; för&quot;ago&quot; inte längre accepteras.

All kod som använder API:t RelativeTimeFormat() måste därför ändras

* From: `final RelativeTimeFormat fmt = new RelativeTimeFormat("r a", resourceBundle);`
* Till: `final RelativeTimeFormat fmt = new RelativeTimeFormat("r", resourceBundle);`

Felet skiljer sig åt när det gäller författare och publicering. Skribenten skriver att det inte går att skriva och att forumen helt enkelt inte visas. Vid publicering genereras ett fel på sidan.

Mer information finns i [com.day.cq.commons.date.RelativeTimeFormat](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/date/RelativeTimeFormat.html) API.

## Vanliga problem {#common-concerns}

### Varning i loggar: Borttagna handtag {#warning-in-logs-handlebars-deprecated}

Under start (inte under den första - men efter den) kan följande varning visas i loggarna:

* 11.04.2014 08:38:07.223 **WARN** []FelixStartLevelcom.github.jknack.handlebars.Handlebars Helper &#39;i18n&#39; har ersatts med &#39;com.adobe.cq.social.handlebars.I18nHelper@15bac645&#39;

Denna varning kan ignoreras eftersom jknack.handlebars.Handlebars, som används av [SCF](scf.md#handlebarsjavascripttemplatinglanguage), har ett eget i18n-hjälpverktyg. Från början ersätts den med en AEM-specifik [i18n-hjälpreda](handlebars-helpers.md#i-n). Den här varningen genereras av tredjepartsbiblioteket för att bekräfta åsidosättningen av en befintlig hjälpreda.

### Varning i loggar: OakResourceListener processOsgiEventQueue {#warning-in-logs-oakresourcelistener-processosgieventqueue}

Om du publicerar ett antal forum-ämnen för sociala communityer kan det resultera i stora mängder varnings- och informationsloggar från OakResourceListener processOsgiEventQueue.

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

Uppgradering av AEM 5.6.1 GA till den senaste cq-socialcommunities-pkg-1.4.x eller till AEM 6.0 resulterar i fel i loggfilen under start, vilket ger en problemlösning som visas av felet som inte visas vid omstart.

```xml
14.11.2013 20:52:39.453 ERROR [Apache Sling JCR Resource Event Queue Processor for path '/'] com.adobe.cq.social.storage.index.impl.IndexService Error occurred while processing event java.util.ConcurrentModificationException
14.11.2013 20:52:40.716 ERROR [OsgiInstallerImpl] com.adobe.cq.social.cq-social-commons [CommentListProvider] Error during instantiation of the implementation object (java.lang.NoClassDefFoundError: com/adobe/cq/social/storage/index/IndexElementFactory) java.lang.NoClassDefFoundError: com/adobe/cq/social/storage/index/IndexElementFactory
14.11.2013 20:52:40.717 ERROR [OsgiInstallerImpl] com.adobe.cq.social.cq-social-commons [CommentListProvider] Failed creating the component instance; see log for reason
```
