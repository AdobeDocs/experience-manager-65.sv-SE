---
title: Konfigurera reservteckensnitt
seo-title: Konfigurera reservteckensnitt
description: Lär dig hur du konfigurerar reservteckensnitt.
seo-description: Lär dig hur du konfigurerar reservteckensnitt.
uuid: 2745541c-8c6d-4bb4-aa14-ec19afd6bc35
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_pdf_generator
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: d997a268-a40a-462d-badd-94f0731f7ba4
translation-type: tm+mt
source-git-commit: d3719a9ce2fbb066f99445475af8e1f1e7476f4e

---


# Konfigurera reservteckensnitt {#configuring-fallback-fonts}

Du kan konfigurera filen FontManagerResources.properties manuellt så att standardteckensnitten för AEM-formulär mappas till reserv (eller ersättning) om standardteckensnitten inte är tillgängliga på servern. Egenskapsfilen finns i filen adobe-fontmanager.jar.

>[!NOTE]
>
>Konfiguration av reservteckensnitt gäller även för monteringsverktyget.

1. Navigera till filen adobe-livecycle-*`[appserver]`*.ear i katalogen *`[aem-forms root]`*/configurationManager/export, skapa en säkerhetskopia och packa upp originalet.
1. Leta reda på filen adobe-fontmanager.jar och packa upp den.
1. Leta reda på filen FontManagerResources.properties och öppna den i en textredigerare.
1. Ändra teckensnittsplatserna och namnen för generiska och reservalternativ efter behov och spara filen.

   Teckensnittsposterna i filen FontManagerResources.properties är relativa till katalogen *`[aem-forms root]`*/fonts. Om du anger teckensnitt som inte är standard-AEM-formulärteckensnitt måste du installera dessa teckensnitt i den här katalogstrukturen (antingen i en befintlig katalog eller i en ny).

   >[!NOTE]
   >
   >Om det angivna teckensnittet eller standardteckensnittet inte innehåller ett visst Unicode-tecken, eller om det inte är tillgängligt, hämtas tecknet från ett reservteckensnitt enligt följande prioritet:

   * Språkspecifikt teckensnitt
   * ROOT-teckensnitt om språkområdet inte är inställt
   * Generiskt teckensnitt, söks igenom efter ordningsföljd i reservtabellen

1. Paketera om filen adobe-fontmanager.jar.
1. Paketera om filen adobe-livecycle-*`[appserver]`*.ear och distribuera den sedan manuellt eller genom att köra Configuration Manager.

>[!NOTE]
>
>Använd inte Configuration Manager för att paketera om filen adobe-livecycle-`[appserver]`.ear eftersom den kommer att skriva över ändringarna med AEM-formulärens standardvärden.

