---
title: Krypteringsstöd för konfigurationsegenskaper
seo-title: Encryption Support for Configuration Properties
description: Lär dig mer om krypteringsstöd för konfigurationsegenskaper i AEM.
seo-description: null
uuid: 26dc5e46-9332-4d9b-8874-895b90391e8c
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: security
discoiquuid: 4e08c297-aa4b-44cf-84c8-1e11582d9ebb
exl-id: 3c3db1c8-5b22-45dd-aeaf-5cf830a9486b
source-git-commit: e54c1d422f2bf676e8a7b0f50a101e495c869c96
workflow-type: tm+mt
source-wordcount: '283'
ht-degree: 0%

---

# Krypteringsstöd för konfigurationsegenskaper{#encryption-support-for-configuration-properties}

## Översikt {#overview}

Med den här funktionen kan alla OSGi-konfigurationsegenskaper lagras i en skyddad krypterad form i stället för i klartext. Formuläret i webbkonsolens användargränssnitt används för att skapa krypterad text från klartext med hjälp av den systemomfattande krypteringsnyckeln.

Stöd för OSGi Configuration Plugin har lagts till för att dekryptera egenskapen innan den används av en tjänst.

>[!NOTE]
>
>Tjänster som förväntar sig ett krypterat värde måste använda kontrollen IsProtected för att se om värdet är krypterat innan det försöker dekryptera det, eftersom det redan kan ha dekrypterats.

## Aktivera krypteringsstöd {#enabling-encryption-support}

De här stegen visar hur du krypterar SMTP-lösenordet för e-posttjänsten. Du kan slutföra de här stegen för en OSGI-egenskap som du vill kryptera.

1. Gå till AEM webbkonsol på *https://&lt;serveraddress>:&lt;serverport>/system/console/configMgr*
1. I det övre vänstra hörnet går du till **Main - Crypto Support**

   ![chlimage_1-325](assets/chlimage_1-325.png)

1. The **Stöd för Adobe Experience Manager Web Console-kryptering** visas.

   ![screen_shot_2018-08-01at113417am](assets/screen_shot_2018-08-01at113417am.png)

1. I **Oformaterad text** anger du texten i de känsliga data som du vill skydda.
1. Välj **Protect**. Den skyddade texten visas som krypterad text.

   ![screen_shot_2018-08-01at113844am](assets/screen_shot_2018-08-01at113844am.png)

1. Kopiera den skyddade texten från steg 5 och klistra in den i OSGI-formulärvärdet. I det här exemplet krypteras **SMTP-lösenord** läggs till i *Dagens CQ-tjänst för e-post*.

   ![screen_shot_2016-12-18at105809pm](assets/screen_shot_2016-12-18at105809pm.png)

1. Spara egenskaperna för daglig CQ Mail Service. SMTP-lösenordet skickas nu som ett krypterat värde.

## Stöd för dekryptering {#decryption-support}

AEM tillhandahåller nu ett konfigurations-plugin-program för att dekryptera konfigurationsegenskaper. Den här AEM-plugin-programmet dekrypterar och hämtar textegenskaperna automatiskt.
