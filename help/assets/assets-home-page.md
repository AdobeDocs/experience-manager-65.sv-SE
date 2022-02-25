---
title: '"[!DNL Assets] Home Page experience"'
description: Anpassa [!DNL Experience Manager Assets] Startsida för en rik välkomstskärm, inklusive en ögonblicksbild av nyligen gjorda aktiviteter kring resurser.
contentOwner: AG
feature: Developer Tools, Asset Management
role: Admin, User
exl-id: 042bd959-256a-4794-a34d-0848a6b8840d
source-git-commit: e24316cb9495a552960ae0620e4198f10a08b691
workflow-type: tm+mt
source-wordcount: '507'
ht-degree: 1%

---

# [!DNL Adobe Experience Manager Assets] Home Page Experience {#aem-assets-home-page-experience}

Anpassa [!DNL Adobe Experience Manager Assets] startsida för en rik välkomstskärm, inklusive en ögonblicksbild av nyligen gjorda aktiviteter kring resurser.

[!DNL Assets] startsidan ger en rik och personlig välkomstskärm, som innehåller en ögonblicksbild av de senaste aktiviteterna, till exempel resurser som nyligen har visats eller överförts.

The [!DNL Assets] hemsidan är inaktiverad som standard. Så här aktiverar du den:

1. Öppna [!DNL Experience Manager] Konfigurationshanteraren `https://[aem_server]:[port]/system/console/configMgr`.
1. Öppna **[!UICONTROL Day CQ DAM Event Recorder]** service.
1. Välj **[!UICONTROL Enable this service]** för att aktivera aktivitetsinspelning.

   ![chlimage_1-250](assets/chlimage_1-250.png)

1. Från **[!UICONTROL Event Types]** markerar du de händelser som ska spelas in och sparar ändringarna.

   >[!CAUTION]
   >
   >Om du aktiverar alternativen Visa, Visa projekt och Samlingar, ökar antalet inspelade händelser avsevärt.

1. Öppna **[!UICONTROL DAM Asset Home Page Feature Flag]** tjänst från Configuration Manager `https://[aem_server]:[port]/system/console/configMgr`.
1. Välj `isEnabled.name` för att aktivera [!DNL Assets] Funktion på startsidan. Spara ändringarna.

   ![chlimage_1-251](assets/chlimage_1-251.png)

1. Öppna **[!UICONTROL User Preferences]** och väljer **[!UICONTROL Enable Assets Home Page]**. Spara ändringarna.

   ![Aktivera startsidan för resurser i dialogrutan Användarinställningar](assets/Annotation-color.png)

När du har aktiverat [!DNL Assets] Startsida, navigera till [!DNL Assets] -användargränssnittet antingen från navigeringssidan eller direkt från webbadressen `https://[aem_server]:[port]/aem/assetshome.html/content/dam`.

![konfigurera Experience link i Assets-användargränssnittet](assets/config-experience-link.png)

Klicka på **[!UICONTROL Click here to configure your experience link]** för att lägga till ditt användarnamn, din bakgrundsbild och din profilbild.

The [!DNL Assets] Hemsidan innehåller följande avsnitt:

* Välkomstavsnitt
* Widget Section

**Välkomstavsnitt**

Om din profil finns visas ett välkomstmeddelande adresserat till dig i välkomstavsnittet. Dessutom visas din profilbild och en välkomstbild (om den redan är konfigurerad).

Om din profil är ofullständig visas ett allmänt välkomstmeddelande och en platshållare för din profilbild i välkomstavsnittet.

**Widget Section**

Det här avsnittet visas under välkomstavsnittet och visar widgetar som inte finns i kartongen under följande avsnitt:

* Aktivitet
* Senaste
* Upptäck

**Aktivitet**: Under det här avsnittet **[!UICONTROL My Activity]** widgeten visar de senaste aktiviteterna som den inloggade användaren har utfört med resurser (inklusive resurser utan återgivningar), till exempel överföringar av resurser, hämtningar, skapande av resurser, redigeringar, kommentarer, anteckningar och delningar.

**Senaste**: The **[!UICONTROL Recently Viewed]** widgeten under det här avsnittet visar nyligen använda entiteter av den inloggade användaren, inklusive mappar, samlingar och projekt.

**Upptäck**: The **[!UICONTROL New]** visas resurser och återgivningar som nyligen har överförts till [!DNL Assets] distribution.

Aktivera alternativet **[!UICONTROL DAM Event Purge Service]** från Configuration Manager. När du har aktiverat den här tjänsten tas aktiviteter av den inloggade användaren som överskrider ett angivet nummer bort av systemet.

Välkomstskärmen innehåller enkla navigeringshjälpmedel, t.ex. ikoner i verktygsfältet för att komma åt mappar, samlingar och kataloger.

>[!NOTE]
>
>Aktivera [!UICONTROL Day CQ DAM Event Recorder] och [!UICONTROL DAM Event Purge] tjänster ökar skrivåtgärder till JCR och sökindexering, vilket ökar belastningen på [!DNL Experience Manager] server. Ytterligare belastning på [!DNL Experience Manager] kan påverka serverns prestanda.

>[!CAUTION]
>
>Hämta, filtrera och rensa användaraktiviteter som krävs för [!DNL Assets] startsidan medför höga prestanda. Därför bör administratörer konfigurera hemsidan effektivt för målanvändare.
>
>Adobe rekommenderar att administratörer och användare som utför gruppåtgärder undviker att använda funktionen Startsida för resurser för att förhindra att användaraktiviteter ökar. Dessutom kan administratörer utesluta inspelningsaktiviteter för specifika användare genom att konfigurera [!UICONTROL Day CQ DAM Event Recorder] från [!UICONTROL Configuration Manager].
>
>Om du använder funktionen rekommenderar Adobe att du schemalägger tömningsfrekvensen baserat på serverinläsningen.
