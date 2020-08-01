---
title: '[!DNL Adobe Experience Manager Assets] - startsida'
description: Anpassa hemsidan [!DNL Experience Manager Assets] för en rik välkomstskärm, inklusive en ögonblicksbild av nyligen gjorda aktiviteter kring resurser.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 9fc1201db83ae0d3bb902d4dc3ab6d78cc1dc251
workflow-type: tm+mt
source-wordcount: '512'
ht-degree: 1%

---


# [!DNL Adobe Experience Manager Assets] Home Page Experience {#aem-assets-home-page-experience}

Anpassa [!DNL Adobe Experience Manager Assets] hemsidan för en rik välkomstskärm, inklusive en ögonblicksbild av nyligen gjorda aktiviteter kring resurser.

[!DNL Assets] startsidan ger en rik och personlig välkomstskärm, som innehåller en ögonblicksbild av de senaste aktiviteterna, till exempel resurser som nyligen har visats eller överförts.

Hemsidan är som standard inaktiverad [!DNL Assets] . Så här aktiverar du den:

1. Öppna [!DNL Experience Manager] Configuration Manager `https://[aem_server]:[port]/system/console/configMgr`.
1. Öppna **[!UICONTROL Day CQ DAM Event Recorder]** tjänsten.
1. Markera alternativet **[!UICONTROL Enable this service]** för att aktivera aktivitetsinspelning.

   ![chlimage_1-250](assets/chlimage_1-250.png)

1. I **[!UICONTROL Event Types]** listan väljer du vilka händelser som ska spelas in och sparar ändringarna.

   >[!CAUTION]
   >
   >Om du aktiverar alternativen Visa, Visa projekt och Samlingar, ökar antalet inspelade händelser avsevärt.

1. Öppna **[!UICONTROL DAM Asset Home Page Feature Flag]** tjänsten från Configuration Manager `https://[aem_server]:[port]/system/console/configMgr`.
1. Välj `isEnabled.name` alternativet för att aktivera funktionen [!DNL Assets] Hemsida. Spara ändringarna.

   ![chlimage_1-251](assets/chlimage_1-251.png)

1. Öppna **[!UICONTROL User Preferences]** dialogrutan och välj **[!UICONTROL Enable Assets Home Page]**. Spara ändringarna.

   ![Aktivera startsidan för resurser i dialogrutan Användarinställningar](assets/Annotation-color.png)

När du har aktiverat [!DNL Assets] hemsidan navigerar du till [!DNL Assets] användargränssnittet från navigeringssidan eller öppnar det direkt från URL:en `https://[aem_server]:[port]/aem/assetshome.html/content/dam`.

![konfigurera Experience link i Assets-användargränssnittet](assets/config-experience-link.png)

Klicka på **[!UICONTROL Click here to configure your experience link]** för att lägga till ditt användarnamn, din bakgrundsbild och din profilbild.

Hemsidan [!DNL Assets] innehåller följande avsnitt:

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

**Aktivitet**: I det här avsnittet visas de senaste aktiviteterna som har utförts av den inloggade användaren med resurser (inklusive resurser utan återgivningar), till exempel överföringar av resurser, hämtningar, skapande av resurser, redigeringar, kommentarer, anteckningar och delningar. **[!UICONTROL My Activity]**

**Senaste**: Widgeten under det här avsnittet visar nyligen använda enheter som den inloggade användaren har använt, inklusive mappar, samlingar och projekt. **[!UICONTROL Recently Viewed]**

**Upptäck**: Widgeten **[!UICONTROL New]** under det här avsnittet visar resurser och återgivningar som nyligen har överförts till [!DNL Assets] distributionen.

Aktivera alternativet från Configuration Manager om du vill aktivera rensning av användaraktivitetsdata **[!UICONTROL DAM Event Purge Service]** . När du har aktiverat den här tjänsten tas aktiviteter av den inloggade användaren som överskrider ett angivet nummer bort av systemet.

Välkomstskärmen innehåller enkla navigeringshjälpmedel, t.ex. ikoner i verktygsfältet för att komma åt mappar, samlingar och kataloger.

>[!NOTE]
>
>Om du aktiverar [!UICONTROL Day CQ DAM Event Recorder] och [!UICONTROL DAM Event Purge] tjänster ökar skrivåtgärderna till JCR och sökindexering, vilket ökar belastningen på [!DNL Experience Manager] servern avsevärt. Den extra belastningen på [!DNL Experience Manager] servern kan påverka serverns prestanda.

>[!CAUTION]
>
>Att hämta in, filtrera och rensa användaraktiviteter som krävs för hemsidan medför höga prestandaförluster. [!DNL Assets] Därför bör administratörer konfigurera hemsidan effektivt för målanvändare.
>
>Adobe rekommenderar att administratörer och användare som utför gruppåtgärder undviker att använda funktionen Startsida för resurser för att förhindra att användaraktiviteter ökar. Dessutom kan administratörer utesluta inspelningsaktiviteter för specifika användare genom att konfigurera [!UICONTROL Day CQ DAM Event Recorder] från [!UICONTROL Configuration Manager].
>
>Om du använder funktionen rekommenderar Adobe att du schemalägger tömningsfrekvensen baserat på serverinläsningen.
