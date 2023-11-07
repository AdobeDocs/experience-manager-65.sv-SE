---
title: Konfigurera reservteckensnitt
description: Lär dig hur du konfigurerar grundteckensnitt för AEM Forms. Du kan använda filen FontManagerResources.properties om du vill mappa standardteckensnitten till grundteckensnitt manuellt.
uuid: 2745541c-8c6d-4bb4-aa14-ec19afd6bc35
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_pdf_generator
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: d997a268-a40a-462d-badd-94f0731f7ba4
feature: PDF Generator
exl-id: 76dd2b0c-9f16-47bf-a565-99277be750fb
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '264'
ht-degree: 0%

---

# Konfigurera reservteckensnitt {#configuring-fallback-fonts}

Du kan konfigurera filen FontManagerResources.properties manuellt för att mappa AEM standardteckensnitt till reserv (eller ersättning) om standardteckensnitten inte är tillgängliga på servern. Den här egenskapsfilen finns i filen adobe-fontmanager.jar.

>[!NOTE]
>
>Konfiguration av reservteckensnitt gäller även för monteringsverktyget.

1. Navigera till adobe-livecycle-*`[appserver]`*.ear-filen i *`[aem-forms root]`*/configurationManager/export katalog, skapa en säkerhetskopia och packa upp originalet.
1. Leta reda på filen adobe-fontmanager.jar och packa upp den.
1. Leta reda på filen FontManagerResources.properties och öppna den i en textredigerare.
1. Ändra teckensnittsplatserna och namnen för generiska och reservalternativ efter behov och spara filen.

   Teckensnittsposterna i filen FontManagerResources.properties är relativa till *`[aem-forms root]`*/fonts-katalog. Om du anger teckensnitt som inte är standard AEM formulärteckensnitt måste du installera dessa teckensnitt i den här katalogstrukturen (antingen i en befintlig katalog eller i en ny).

   >[!NOTE]
   >
   >Om det angivna teckensnittet eller standardteckensnittet inte innehåller ett visst Unicode-tecken, eller om det inte är tillgängligt, hämtas tecknet från ett reservteckensnitt enligt följande prioritet:

   * Språkspecifikt teckensnitt
   * ROOT-teckensnitt om språkområdet inte är inställt
   * Generiskt teckensnitt, söks igenom efter ordningsföljd i reservtabellen

1. Paketera om filen adobe-fontmanager.jar.
1. Paketera om Adobe-livecycle-*`[appserver]`*.ear file and then redeploy it either manual or by running Configuration Manager.

>[!NOTE]
>
>Använd inte Configuration Manager för att paketera om adobe-livecycle-`[appserver]`.ear-filen eftersom den skriver över ändringarna med standardvärdena för AEM formulär.
