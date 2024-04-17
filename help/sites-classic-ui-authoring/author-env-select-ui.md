---
title: Välja användargränssnitt
description: För att underlätta för redigeringsanvändarna går det att växla till det klassiska användargränssnittet med det pekaktiverade gränssnittet när det behövs.
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
exl-id: 57d45b06-e76e-420c-8cd0-389bd9f811af
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 0%

---

# Välja användargränssnitt{#selecting-your-ui}

Eftersom det beröringskänsliga användargränssnittet ersätter det klassiska användargränssnittet måste användaren eller administratören för den AEM instansen fatta ett aktivt beslut om att fortsätta använda det klassiska användargränssnittet. Eftersom det klassiska användargränssnittet inte längre underhålls går det inte att helt enkelt växla från det klassiska användargränssnittet till motsvarande i det beröringskänsliga användargränssnittet.

För att underlätta för redigeringsanvändarna går det att växla till det klassiska användargränssnittet med det pekaktiverade gränssnittet när det behövs. Se [Välja användargränssnitt](/help/sites-authoring/select-ui.md) i standarddokumentationen.

>[!NOTE]
>
>Instanser som uppgraderats från en tidigare version behåller det klassiska användargränssnittet för sidredigering.
>
>Efter uppgraderingen växlas inte sidredigering automatiskt till det beröringsaktiverade användargränssnittet, men du kan konfigurera detta med[OSGi-konfiguration](/help/sites-deploying/configuring-osgi.md) i **Tjänsten WCM för användargränssnittsläge vid redigering** ( `AuthoringUIMode` service). Se [Gränssnittsåsidosättningar för redigeraren](#uioverridesfortheeditor).

## Konfigurera standardgränssnittet för din instans {#configuring-the-default-ui-for-your-instance}

En systemadministratör kan konfigurera användargränssnittet som visas vid start och inloggning med [Rotmappning](/help/sites-deploying/osgi-configuration-settings.md#daycqrootmapping).

Detta kan åsidosättas av användarens standardinställningar eller sessionsinställningar.
