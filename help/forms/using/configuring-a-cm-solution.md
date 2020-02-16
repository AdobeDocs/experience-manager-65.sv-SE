---
title: Konfigurera en Correspondence Management-lösning
seo-title: Konfigurera en Correspondence Management-lösning
description: 'null'
seo-description: 'null'
uuid: 76b25004-fe47-44d7-9bed-7c0fd963306b
topic-tags: correspondence-management
content-type: reference
products: SG_EXPERIENCEMANAGER/6.3/FORMS
discoiquuid: 186ca75c-638b-4057-826e-cd5d56aa0397
translation-type: tm+mt
source-git-commit: 5120bbdefea528ad6d07a9c99df565555b6a8444

---


# Konfigurera en Correspondence Management-lösning {#configuring-a-correspondence-management-solution}

## Definiera författarinstansens URL för VersionRestoreManagerImpl {#defining-author-instance-url-for-versionrestoremanagerimpl}

Följ de här stegen för att definiera en URL för författarinstansen för återställning av författarinstansversion:

1. Gå till *https://:&lt;PublishHost>:&lt;PublishPort>/lc/system/console/configMgr*. Logga in med autentiseringsuppgifter för OSGi Management Console. Standardautentiseringsuppgifterna är admin/admin.
1. Sök efter och klicka på **[!UICONTROL Redigera]** -ikonen bredvid **[!UICONTROL inställningen]** com.adobe.livecycle.content.activate.impl.VersionRestoreManagerImpl.name.
1. Ange URL:en för författarinstansen av VersionRestoreManager i fältet **[!UICONTROL VersionRestoreManagers författar-URL]** .

   **URL-sträng**:

   `https://<hostname>:<port>:/libs/fd/fdm/content/crud/lc.content.remote.activate.VersionRestoreManager`

   >[!NOTE]
   >
   >Om det finns flera författarinstanser (grupperade) som föregås av en belastningsutjämnare anger du URL:en till belastningsutjämnaren i **[!UICONTROL fältet VersionRestoreManagers författar-URL]** .

1. Click **[!UICONTROL Save]**.

## Definiera publiceringsinstansens URL för ActivationManagerImpl (hanteraren för aktivering av offentlig instans) {#defining-the-publish-instance-url-for-activationmanagerimpl-public-instance-activation-manager}

Följ de här stegen för att definiera publiceringsinstansens URL för aktiveringshanteraren för den offentliga instansen:

1. Gå till *https://:&lt;authorHost>:&lt;authorPort>/lc/system/console/configMgr*. Logga in med autentiseringsuppgifter för OSGi Management Console. Standardautentiseringsuppgifterna är admin/admin.
1. Leta reda på och klicka på **[!UICONTROL ikonen Redigera]** bredvid inställningen **[!UICONTROL com.adobe.livecycle.content.activate.impl.ActivationManagerImpl.name]** .
1. I fältet **[!UICONTROL ActivationManager Publish URL (Publicerings-URL]** ) anger du URL:en för åtkomst till Publish-instansen ActivationManager. Du kan ange följande URL:er.

   * **URL för belastningsutjämnare (rekommenderas)**: Ange URL för belastningsutjämnare om du har en webbserver som fungerar som belastningsutjämnare framför publiceringsservergruppen (flera icke-klustrade publiceringsinstanser).
   * **Publiceringsinstans-URL**: Ange en URL för publiceringsinstans. Om du har en enda publiceringsinstans eller webbservern där publiceringsgruppen finns är den inte tillgänglig från författarmiljön på grund av begränsningar. Om den angivna publiceringsinstansen är nere finns det en reservmekanism att hantera på författarsidan.
   * **URL-sträng**:

      `https://<hostname>:<port>:/libs/fd/fdm/content/crud/lc.content.remote.activate.activationManager`

1. Click **[!UICONTROL Save]**.

Mer information om hur du konfigurerar Correspondence Management finns i Konfigurationsegenskaper för [Correspondence Management](https://helpx.adobe.com/aem-forms/6-2/cm-configuration-properties.html).
