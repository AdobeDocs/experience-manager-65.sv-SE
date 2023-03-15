---
title: Granska åtgärder för användarhantering i AEM
seo-title: How to Audit User Management Operations in AEM
description: Lär dig hur du granskar åtgärder för användarhantering i AEM.
seo-description: Learn how to audit User Management Operations in AEM.
uuid: 9d177afb-172c-4858-a678-254c97cfa472
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: ba6a56e5-b91c-4779-9154-d4300b2827f8
docset: aem65
exl-id: 7a4406c9-2f98-4bf8-b32c-1ec1e7ff36f0
feature: Operations
source-git-commit: 9134130f349c6c7a06ad9658a87f78a86b7dbf9c
workflow-type: tm+mt
source-wordcount: '308'
ht-degree: 0%

---

# Granska åtgärder för användarhantering i AEM{#how-to-audit-user-management-operations-in-aem}

## Introduktion {#introduction}

AEM har infört möjligheten att logga behörighetsändringar så att de kan granskas vid ett senare tillfälle.

Förbättringen möjliggör granskning av CRUD-åtgärder (Skapa, Läs, Uppdatera, Ta bort) för behörigheter och grupptilldelningar av användare. Mer specifikt loggas:

* En ny användare skapas
* En användare läggs till i en grupp
* Behörighetsändringar för en befintlig användare eller grupp

Som standard skrivs posterna till `error.log` -fil. För att underlätta övervakningen rekommenderar vi att de dirigeras om till en separat loggfil. Mer information om hur du gör detta i stycket nedan.

## Omdirigera utdata till en separat loggfil {#redirecting-the-output-to-a-separate-log-file}

Om du vill omdirigera loggningsutdata till en separat loggfil måste du skapa en ny **Loggningsloggare för Apache Sling** konfiguration. Vi använder `useraudit.log` som namnet på den separata filen i exemplet nedan.

1. Gå till webbkonsolen genom att bläddra till *https://serveraddress:serverport/system/console/configMgr*
1. Sök efter **Konfiguration av loggningsloggare för Apache Sling**. Tryck sedan på + till höger om posten för att skapa en ny fabrikskonfiguration.
1. Skapa följande konfiguration:

   * **Loggnivå:** Information
   * **Loggfil:** logs/useraudit.log
   * **Meddelandemönster:** standardnivå
   * **Logger:** com.adobe.granite.security.user.internal.audit, com.adobe.granite.security.user.internal.servlets.AuthorizableServlet

   För att kunna ange båda loggarna i **Logger** måste du ange namnet på den första, sedan skapa ett annat fält genom att trycka på plusknappen (+) och ange namnet på den andra loggaren.

## Exempelutdata {#example-output}

Om utdata är korrekt konfigurerade bör de se ut så här:

```xml
19.05.2017 15:15:08.933 *INFO* [0:0:0:0:0:0:0:1 [1495196108932] POST /libs/granite/security/post/authorizables.html HTTP/1.1] com.adobe.granite.security.user.internal.servlets.AuthorizableServlet Create Group 'group1' operation initiated by User 'admin' (administrator)
19.05.2017 15:15:08.934 *INFO* [0:0:0:0:0:0:0:1 [1495196108932] POST /libs/granite/security/post/authorizables.html HTTP/1.1] com.adobe.granite.security.user.internal.audit.AuditAuthorizableAction Group 'group1' was created

19.05.2017 15:16:25.698 *INFO* [0:0:0:0:0:0:0:1 [1495196185696] POST /libs/granite/security/post/authorizables.html HTTP/1.1] com.adobe.granite.security.user.internal.servlets.AuthorizableServlet Create User 'user1' operation initiated by User 'admin' (administrator)
19.05.2017 15:16:25.700 *INFO* [0:0:0:0:0:0:0:1 [1495196185696] POST /libs/granite/security/post/authorizables.html HTTP/1.1] com.adobe.granite.security.user.internal.audit.AuditAuthorizableAction User 'user1' was created

19.05.2017 15:16:25.728 *INFO* [0:0:0:0:0:0:0:1 [1495196185726] POST /home/groups/d/dGf7f7vGrZRLs6HS3AK-.rw.userprops.html HTTP/1.1] com.adobe.granite.security.user.internal.servlets.AuthorizableServlet Edit Membership for Group 'group1' operation initiated by User 'admin' (administrator)
19.05.2017 15:16:25.729 *INFO* [0:0:0:0:0:0:0:1 [1495196185726] POST /home/groups/d/dGf7f7vGrZRLs6HS3AK-.rw.userprops.html HTTP/1.1] com.adobe.granite.security.user.internal.audit.AuditGroupAction User 'user1' was added to the group 'group1'

19.05.2017 15:17:29.830 *INFO* [0:0:0:0:0:0:0:1 [1495196249828] POST /home/users/5/5dI6iK4HkZmrfTjcLBoI.rw.userprops.html HTTP/1.1] com.adobe.granite.security.user.internal.servlets.AuthorizableServlet Password Change for User 'user2' operation initiated by User 'admin' (administrator)
19.05.2017 15:17:29.832 *INFO* [0:0:0:0:0:0:0:1 [1495196249828] POST /home/users/5/5dI6iK4HkZmrfTjcLBoI.rw.userprops.html HTTP/1.1] com.adobe.granite.security.user.internal.audit.AuditAuthorizableAction Password for User 'user2' was changed

19.05.2017 15:17:54.906 *INFO* [0:0:0:0:0:0:0:1 [1495196274904] POST /home/users/5/5dI6iK4HkZmrfTjcLBoI.rw.html HTTP/1.1] com.adobe.granite.security.user.internal.servlets.AuthorizableServlet Delete User 'user2' operation initiated by User 'admin' (administrator)
19.05.2017 15:17:54.906 *INFO* [0:0:0:0:0:0:0:1 [1495196274904] POST /home/users/5/5dI6iK4HkZmrfTjcLBoI.rw.html HTTP/1.1] com.adobe.granite.security.user.internal.audit.AuditAuthorizableAction User 'user2' was removed

19.05.2017 15:19:11.050 *INFO* [0:0:0:0:0:0:0:1 [1495196351049] POST /libs/granite/security/post/authorizables.html HTTP/1.1] com.adobe.granite.security.user.internal.servlets.AuthorizableServlet Create User 'user3' operation initiated by User 'admin' (administrator)
19.05.2017 15:19:11.052 *INFO* [0:0:0:0:0:0:0:1 [1495196351049] POST /libs/granite/security/post/authorizables.html HTTP/1.1] com.adobe.granite.security.user.internal.audit.AuditAuthorizableAction User 'user3' was created
19.05.2017 15:19:36.899 *INFO* [0:0:0:0:0:0:0:1 [1495196376898] POST /home/groups/d/dGf7f7vGrZRLs6HS3AK-.rw.userprops.html HTTP/1.1] com.adobe.granite.security.user.internal.servlets.AuthorizableServlet Edit Membership for Group 'group1' operation initiated by User 'admin' (administrator)

19.05.2017 15:19:36.916 *INFO* [0:0:0:0:0:0:0:1 [1495196376915] POST /home/groups/d/dGf7f7vGrZRLs6HS3AK-.rw.userprops.html HTTP/1.1] com.adobe.granite.security.user.internal.servlets.AuthorizableServlet Edit Membership for Group 'group1' operation initiated by User 'admin' (administrator)
19.05.2017 15:19:36.917 *INFO* [0:0:0:0:0:0:0:1 [1495196376915] POST /home/groups/d/dGf7f7vGrZRLs6HS3AK-.rw.userprops.html HTTP/1.1] com.adobe.granite.security.user.internal.audit.AuditGroupAction User 'user1' was removed from the group 'group1'

19.05.2017 15:21:34.419 *INFO* [0:0:0:0:0:0:0:1 [1495196494417] POST /home/groups/d/dGf7f7vGrZRLs6HS3AK-.rw.html HTTP/1.1] com.adobe.granite.security.user.internal.servlets.AuthorizableServlet Delete Group 'group1' operation initiated by User 'admin' (administrator)
19.05.2017 15:21:34.419 *INFO* [0:0:0:0:0:0:0:1 [1495196494417] POST /home/groups/d/dGf7f7vGrZRLs6HS3AK-.rw.html HTTP/1.1] com.adobe.granite.security.user.internal.audit.AuditAuthorizableAction Group 'group1' was removed

19.05.2017 15:44:10.404 *INFO* [0:0:0:0:0:0:0:1 [1495197850401] POST /home/users/3/35XVpVtLRx4a5J9gKrVG.rw.userprops.html HTTP/1.1] com.adobe.granite.security.user.internal.servlets.AuthorizableServlet Password Change for User 'john' operation initiated by User 'john' (not administrator)
19.05.2017 15:44:10.405 *INFO* [0:0:0:0:0:0:0:1 [1495197850401] POST /home/users/3/35XVpVtLRx4a5J9gKrVG.rw.userprops.html HTTP/1.1] com.adobe.granite.security.user.internal.audit.AuditAuthorizableAction Password for User 'john' was changed
```

## Klassiskt användargränssnitt {#classic-ui}

I det klassiska användargränssnittet är information om CRUD-åtgärder som registreras i granskningsloggen för att lägga till och ta bort användare begränsad till ID:t för den användare som påverkas och när ändringen inträffade.

Till exempel:

```
10.05.2019 18:01:09.123 INFO [0:0:0:0:0:0:0:1 [1557491469096] POST /libs/cq/security/authorizables/POST HTTP/1.1] com.adobe.granite.security.user.internal.audit.AuditAuthorizableAction User 'test' was created
```
