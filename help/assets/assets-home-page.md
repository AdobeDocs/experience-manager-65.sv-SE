---
title: '[!DNL Assets] Startsidans upplevelse'
description: Anpassa startsidan för [!DNL Experience Manager Assets] välkomstskärmen, inklusive en ögonblicksbild av nyligen gjorda aktiviteter kring resurser.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 5069c2cd26e84866d72a61d36de085dadd556cdd
workflow-type: tm+mt
source-wordcount: '507'
ht-degree: 1%

---


# [!DNL Adobe Experience Manager Assets] Home Page Experience  {#aem-assets-home-page-experience}

Anpassa startsidan för [!DNL Adobe Experience Manager Assets] för en rik välkomstskärm, inklusive en ögonblicksbild av nyligen gjorda aktiviteter kring resurser.

[!DNL Assets] startsidan ger en rik och personlig välkomstskärm, som innehåller en ögonblicksbild av de senaste aktiviteterna, till exempel resurser som nyligen har visats eller överförts.

Hemsidan [!DNL Assets] är inaktiverad som standard. Så här aktiverar du den:

1. Öppna [!DNL Experience Manager] Configuration Manager `https://[aem_server]:[port]/system/console/configMgr`.
1. Öppna tjänsten **[!UICONTROL Day CQ DAM Event Recorder]**.
1. Välj **[!UICONTROL Enable this service]** för att aktivera aktivitetsinspelning.

   ![chlimage_1-250](assets/chlimage_1-250.png)

1. I listan **[!UICONTROL Event Types]** väljer du vilka händelser som ska registreras och sparar ändringarna.

   >[!CAUTION]
   >
   >Om du aktiverar alternativen Visa, Visa projekt och Samlingar, ökar antalet inspelade händelser avsevärt.

1. Öppna tjänsten **[!UICONTROL DAM Asset Home Page Feature Flag]** från Configuration Manager `https://[aem_server]:[port]/system/console/configMgr`.
1. Välj alternativet `isEnabled.name` om du vill aktivera funktionen [!DNL Assets] hemsida. Spara ändringarna.

   ![chlimage_1-251](assets/chlimage_1-251.png)

1. Öppna dialogrutan **[!UICONTROL User Preferences]** och välj **[!UICONTROL Enable Assets Home Page]**. Spara ändringarna.

   ![Aktivera startsidan för resurser i dialogrutan Användarinställningar](assets/Annotation-color.png)

När du har aktiverat startsidan för [!DNL Assets] navigerar du till användargränssnittet för [!DNL Assets] från navigeringssidan eller öppnar den direkt från URL:en `https://[aem_server]:[port]/aem/assetshome.html/content/dam`.

![konfigurera Experience link i Assets-användargränssnittet](assets/config-experience-link.png)

Klicka på **[!UICONTROL Click here to configure your experience link]** för att lägga till ditt användarnamn, din bakgrundsbild och din profilbild.

Startsidan för [!DNL Assets] innehåller följande avsnitt:

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

**Aktivitet**: I det här avsnittet visar  **[!UICONTROL My Activity]** widgeten de senaste aktiviteterna som utförts av den inloggade användaren med resurser (inklusive resurser utan återgivningar), till exempel överföringar, hämtningar, skapande av resurser, redigeringar, kommentarer, anteckningar och delningar.

**Senaste**: I  **[!UICONTROL Recently Viewed]** widgeten under det här avsnittet visas nyligen använda enheter som den inloggade användaren har använt, inklusive mappar, samlingar och projekt.

**Upptäck**: I  **[!UICONTROL New]** widgeten under det här avsnittet visas de resurser och återgivningar som nyligen har överförts till  [!DNL Assets] distributionen.

Aktivera alternativet **[!UICONTROL DAM Event Purge Service]** från Configuration Manager om du vill aktivera rensning av användaraktivitetsdata. När du har aktiverat den här tjänsten tas aktiviteter av den inloggade användaren som överskrider ett angivet nummer bort av systemet.

Välkomstskärmen innehåller enkla navigeringshjälpmedel, t.ex. ikoner i verktygsfältet för att komma åt mappar, samlingar och kataloger.

>[!NOTE]
>
>Om du aktiverar tjänsterna [!UICONTROL Day CQ DAM Event Recorder] och [!UICONTROL DAM Event Purge] ökas skrivåtgärderna till JCR och sökindexering, vilket avsevärt ökar inläsningen på [!DNL Experience Manager]-servern. Ytterligare belastning på [!DNL Experience Manager]-servern kan påverka dess prestanda.

>[!CAUTION]
>
>Att hämta, filtrera och rensa användaraktiviteter som krävs för [!DNL Assets]-hemsidan medför höga prestanda. Därför bör administratörer konfigurera hemsidan effektivt för målanvändare.
>
>Adobe rekommenderar att administratörer och användare som utför gruppåtgärder undviker att använda funktionen Startsida för resurser för att förhindra att användaraktiviteter ökar. Dessutom kan administratörer exkludera inspelningsaktiviteter för specifika användare genom att konfigurera [!UICONTROL Day CQ DAM Event Recorder] från [!UICONTROL Configuration Manager].
>
>Om du använder funktionen rekommenderar Adobe att du schemalägger tömningsfrekvensen baserat på serverinläsningen.
