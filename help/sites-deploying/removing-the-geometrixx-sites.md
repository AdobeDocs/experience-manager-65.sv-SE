---
title: Ta bort Geometrixx
description: Lär dig hur du tar bort exempelinnehållet i Geometrixx.
uuid: 07d20837-3375-4e64-bb07-3e4d10452335
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
discoiquuid: 56761a36-ce21-46e1-856f-75a7e94acae9
source-git-commit: 78c584db8c35ea809048580fe5b440a0b73c8eea
workflow-type: tm+mt
source-wordcount: '126'
ht-degree: 0%

---


# Ta bort Geometrixx{#removing-the-geometrixx-sites}

AEM innehåller ett antal exempelwebbplatser för Geometrixx. Du kan ta bort det här exempelinnehållet via **Pakethanteraren**.

De enskilda geometrixx-relaterade paketen är:

* `cq-geometrixx-outdoors-ugc-pkg-<version>.zip`
* `cq-geometrixx-pkg-<version>.zip`
* `cq-content-mac-<version>.zip`
* `cq-geometrixx-login-pkg-<version>.zip`
* `cq-geometrixx-users-pkg-<version>.zip`
* `cq-geometrixx-workflow-pkg-<version>.zip`
* `cq-geometrixx-outdoors-pkg-<version>.zip`
* `cq-geometrixx-commons-pkg-<version>.zip`
* `cq-geometrixx-media-pkg-<version>.zip`

Om du vill ta bort ett enskilt paket klickar du på **Avinstallera** på det paketet.

Det finns också ett superpaket:

* `cq-geometrixx-all-pkg-5.6.12.zip`

Detta paket innehåller alla ovanstående individuella paket. Om du vill ta bort allt geometrixrelaterat innehåll samtidigt klickar du på **Avinstallera** på det här paketet. Superpaketet försätts i avinstallerat läge och alla enskilda paket försvinner från pakethanterarvyn.

Du har nu en tom AEM utan några demonstrationssajter.

>[!NOTE]
>
>Vid uppgradering installeras Geometrixx om automatiskt. Ta bort Geometrixx webbplatser efter uppgraderingen om du inte vill ha dessa exempel.

