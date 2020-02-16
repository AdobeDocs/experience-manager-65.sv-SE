---
title: Ta bort Geometrixx-platser
seo-title: Ta bort Geometrixx-platser
description: Lär dig hur du tar bort exempelinnehållet i Geometrixx.
seo-description: Lär dig hur du tar bort exempelinnehållet i Geometrixx.
uuid: 07d20837-3375-4e64-bb07-3e4d10452335
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
discoiquuid: 56761a36-ce21-46e1-856f-75a7e94acae9
translation-type: tm+mt
source-git-commit: 1f7a45adc73b407c402a51b061632e72d97ca306

---


# Ta bort Geometrixx-platser{#removing-the-geometrixx-sites}

AEM levereras med en uppsättning exempelwebbplatser för Geometrixx. Du kan ta bort det här exempelinnehållet med **Pakethanteraren**.

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

Om du vill ta bort ett enskilt paket klickar du bara på **Avinstallera** .

Det finns också ett superpaket:

* `cq-geometrixx-all-pkg-5.6.12.zip`

Detta paket innehåller alla ovanstående individuella paket. Om du vill ta bort allt geometrixrelaterat innehåll på en gång klickar du på **Avinstallera** i det här paketet. Superpaketet försätts i det avinstallerade läget och alla enskilda paket försvinner från pakethanterarvyn.

Du har nu en&quot;tom&quot; AEM-instans utan demonstrationssajter.

>[!NOTE]
>
>När du uppgraderar installeras geometrixx-webbplatser om automatiskt. Du kan behöva ta bort geometrixx-webbplatser efter uppgraderingen om du inte vill ha dessa exempel.

