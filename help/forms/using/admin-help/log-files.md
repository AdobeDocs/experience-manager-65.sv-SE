---
title: Loggfiler
seo-title: Log files
description: Händelser som körnings- eller startfel registreras i programserverns loggfiler, som kan öppnas med valfri textredigerare.
seo-description: Events such as run-time or startup errors are recorded to the application server log files, which can be  opened using any text editor.
uuid: 6ed9fdcd-ff02-4b35-893f-09261a6a557a
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_aem_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: cf140483-470f-4bff-8870-304207508aab
exl-id: 23a65be4-3277-4c73-9189-a9b4d7be73cd
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '115'
ht-degree: 0%

---

# Loggfiler {#log-files}

Händelser som körnings- eller startfel registreras i programserverns loggfiler. Om du har problem med att distribuera till programservern kan du använda loggfilerna för att hitta problemet. Du kan öppna loggfilerna med valfri textredigerare.

(JBoss) Följande loggfiler finns i `[appserver root]/server/'server'/log` katalog:

* boot.log
* server.log.*[yyyy-mm-dd]*
* server.log

(WebLogic) Domänloggfiler finns i `[appserverdomain]` katalogen och serverloggfilerna finns i `[appserverdomain]/servers/[appserver name]/logs` katalog:

* `access.log`
* `[appserver name].log`
* `[appserver name].out.[incremental number]`

(WebSphere) Följande loggfiler finns i `[appserver root]/profiles/default/logs/[appserver name]` katalog:

* SystemErr.log
* SystemOut.log
* StartServer.log
