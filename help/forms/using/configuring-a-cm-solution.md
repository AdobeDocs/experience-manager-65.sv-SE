---
title: Konfigurera en Correspondence Management-lösning
seo-title: Configuring a Correspondence Management solution
description: Konfigurera en Correspondence Management-lösning
uuid: 76b25004-fe47-44d7-9bed-7c0fd963306b
topic-tags: correspondence-management
content-type: reference
products: SG_EXPERIENCEMANAGER/6.3/FORMS
discoiquuid: 186ca75c-638b-4057-826e-cd5d56aa0397
feature: Correspondence Management
exl-id: f7f5eb0d-a283-45ea-84d3-d6375d2bb95b
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '276'
ht-degree: 0%

---

# Konfigurera en Correspondence Management-lösning {#configuring-a-correspondence-management-solution}

## Definiera författarinstansens URL för VersionRestoreManagerImpl {#defining-author-instance-url-for-versionrestoremanagerimpl}

Följ de här stegen för att definiera en URL för författarinstansen för återställning av författarinstansversion:

1. Gå till *https://:&lt;publishhost>:&lt;publishport>/lc/system/console/configMgr*. Logga in med autentiseringsuppgifter för OSGi Management Console. Standardautentiseringsuppgifterna är admin/admin.
1. Sök och klicka på **[!UICONTROL Edit]** -ikonen bredvid **[!UICONTROL com.adobe.livecycle.content.activate.impl.VersionRestoreManagerImpl.name]** inställning.
1. I **[!UICONTROL VersionRestoreManager Author URL]** anger du URL:en till författarinstansen av VersionRestoreManager.

   **URL-sträng**:

   `https://<hostname>:<port>:/libs/fd/fdm/content/crud/lc.content.remote.activate.VersionRestoreManager`

   >[!NOTE]
   >
   >Om det finns flera författarinstanser (grupperade) som föregås av en belastningsutjämnare anger du URL:en till belastningsutjämnaren i dialogrutan **[!UICONTROL VersionRestoreManager Author URL]** fält.

1. Klicka på **[!UICONTROL Save]**.

## Definiera publiceringsinstansens URL för ActivationManagerImpl (hanteraren för aktivering av offentlig instans) {#defining-the-publish-instance-url-for-activationmanagerimpl-public-instance-activation-manager}

Följ de här stegen för att definiera publiceringsinstansens URL för aktiveringshanteraren för den offentliga instansen:

1. Gå till *https://:&lt;authorhost>:&lt;authorport>/lc/system/console/configMgr*. Logga in med autentiseringsuppgifter för OSGi Management Console. Standardautentiseringsuppgifterna är admin/admin.
1. Sök och klicka på **[!UICONTROL Edit]** -ikonen bredvid **[!UICONTROL com.adobe.livecycle.content.activate.impl.ActivationManagerImpl.name]** inställning.
1. I **[!UICONTROL ActivationManager Publish URL]** anger du URL:en för åtkomst till Publish-instansen ActivationManager. Du kan ange följande URL:er.

   * **URL för belastningsutjämnare (rekommenderas)**: Ange URL för belastningsutjämnare om du har en webbserver som fungerar som belastningsutjämnare framför publiceringsservergruppen (flera icke-klustrade publiceringsinstanser).
   * **Publicera instans-URL**: Ange en URL för publiceringsinstans. Om du har en enda publiceringsinstans eller webbservern där publiceringsgruppen finns är den inte tillgänglig från författarmiljön på grund av begränsningar. Om den angivna publiceringsinstansen är nere finns det en reservmekanism att hantera på författarsidan.
   * **URL-sträng**:

      `https://<hostname>:<port>:/libs/fd/fdm/content/crud/lc.content.remote.activate.activationManager`

1. Klicka på **[!UICONTROL Save]**.

Mer information om hur du konfigurerar Correspondence Management finns i [Egenskaper för konfiguration av korrespondenshantering](https://helpx.adobe.com/aem-forms/6-2/cm-configuration-properties.html).
