---
title: Välja användargränssnitt
seo-title: Välja användargränssnitt
description: För att underlätta för redigeringsanvändarna går det att växla till det klassiska användargränssnittet med det pekaktiverade gränssnittet när det behövs.
seo-description: För att underlätta för redigeringsanvändarna går det att växla till det klassiska användargränssnittet med det pekaktiverade gränssnittet när det behövs.
uuid: 755e513e-990c-4dba-8316-623f17bf5c33
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: dcac2a3a-3241-47de-96ce-982ab0bc05eb
translation-type: tm+mt
source-git-commit: 58fa0f05bae7ab5ba51491be3171b5c6ffbe870d
workflow-type: tm+mt
source-wordcount: '216'
ht-degree: 0%

---


# Välja användargränssnitt{#selecting-your-ui}

Eftersom det beröringskänsliga användargränssnittet ersätter det klassiska användargränssnittet måste användaren eller administratören för den AEM instansen fatta ett aktivt beslut om att fortsätta använda det klassiska användargränssnittet. Eftersom det klassiska användargränssnittet inte längre underhålls går det inte att helt enkelt växla från det klassiska användargränssnittet till motsvarande i det beröringskänsliga användargränssnittet.

För att underlätta för redigeringsanvändarna går det att växla till det klassiska användargränssnittet med det pekaktiverade gränssnittet när det behövs. Mer information finns i [Välja användargränssnittet](/help/sites-authoring/select-ui.md) i standarddokumentationen för redigering.

>[!NOTE]
>
>Instanser som uppgraderats från en tidigare version behåller det klassiska användargränssnittet för sidredigering.
>
>Efter uppgraderingen växlas inte sidredigering automatiskt till det beröringsaktiverade användargränssnittet, men du kan konfigurera detta med [OSGi-konfigurationen](/help/sites-deploying/configuring-osgi.md) för tjänsten **WCM Authoring UI Mode Service** ( `AuthoringUIMode`). Se [Gränssnittsåsidosättningar för redigeraren](#uioverridesfortheeditor).

## Konfigurerar standardgränssnittet för din instans {#configuring-the-default-ui-for-your-instance}

En systemadministratör kan konfigurera användargränssnittet som visas vid start och inloggning med [rotmappning](/help/sites-deploying/osgi-configuration-settings.md#daycqrootmapping).

Detta kan åsidosättas av användarens standardinställningar eller sessionsinställningar.
