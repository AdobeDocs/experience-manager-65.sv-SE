---
title: AEM Assets Home Page Experience
description: Anpassa startsidan för AEM Assets för en rik välkomstskärm, inklusive en ögonblicksbild av nyligen gjorda aktiviteter kring resurser.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 0ff23556444fcb161b0adf744bb72fdc50322d92

---


# AEM Assets Home Page Experience {#aem-assets-home-page-experience}

Anpassa startsidan för Adobe Experience Manager Assets (AEM) för en rik välkomstskärm, inklusive en ögonblicksbild av nyligen gjorda aktiviteter kring resurser.

AEM Assets hemsida ger en rik och personlig välkomstskärm, som innehåller en ögonblicksbild av nyligen gjorda aktiviteter, till exempel resurser som nyligen har visats eller överförts.

Hemsidan Resurser är inaktiverad som standard. Så här aktiverar du den:

1. Öppna AEM Configuration Manager `https://[aem_server]:[port]/system/console/configMgr`.
1. Öppna tjänsten **[!UICONTROL Day CQ DAM Event Recorder]** .
1. Välj **[!UICONTROL Aktivera den här tjänsten]** för att aktivera aktivitetsinspelning.

   ![chlimage_1-250](assets/chlimage_1-250.png)

1. I listan **[!UICONTROL Händelsetyper]** väljer du vilka händelser som ska registreras och sparar ändringarna.

   >[!CAUTION]
   >
   >Om du aktiverar alternativen Visa, Visa projekt och Samlingar, ökar antalet inspelade händelser avsevärt.

1. Öppna **[!UICONTROL DAM-filens flagga]** för funktionsflagga på startsidan för resurser från Configuration Manager `https://[aem_server]:[port]/system/console/configMgr`.
1. Välj alternativet `isEnabled.name` för att aktivera funktionen Assets Home page. Spara ändringarna.

   ![chlimage_1-251](assets/chlimage_1-251.png)

1. Öppna dialogrutan **[!UICONTROL Användarinställningar]** och välj **[!UICONTROL Aktivera startsidan]** för resurser. Spara ändringarna.

   ![Aktivera startsidan för resurser i dialogrutan Användarinställningar](assets/Annotation-color.png)

När du har aktiverat startsidan för Assets navigerar du till användargränssnittet för Assets från navigeringssidan eller öppnar det direkt från URL:en `https://[aem_server]:[port]/aem/assetshome.html/content/dam`.

![konfigurera Experience link i Assets-användargränssnittet](assets/config-experience-link.png)

Tryck/klicka på **[!UICONTROL Klicka här för att konfigurera din upplevelselänk]** för att lägga till ditt användarnamn, din bakgrundsbild och din profilbild.

Hemsidan för Assets innehåller följande avsnitt:

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

**Aktivitet**: I det här avsnittet visas widgeten **[!UICONTROL Min aktivitet]** nyligen utförda aktiviteter som utförts av den inloggade användaren med resurser (inklusive resurser utan återgivningar), till exempel överföringar av resurser, hämtningar, skapande av resurser, redigeringar, kommentarer, anteckningar och delningar.

**Senaste**: Widgeten **[!UICONTROL Senast visade]** under det här avsnittet visar nyligen använda enheter som den inloggade användaren har använt, inklusive mappar, samlingar och projekt.

**Upptäck**: Widgeten **[!UICONTROL Nytt]** under det här avsnittet visar resurser och återgivningar som nyligen har överförts till AEM Assets-instansen.

Om du vill aktivera rensning av användaraktivitetsdata aktiverar du tjänsten **** DAM Event Rensa från Configuration Manager. När du har aktiverat den här tjänsten tas aktiviteter av den inloggade användaren som överskrider ett angivet nummer bort av systemet.

Välkomstskärmen innehåller enkla navigeringshjälpmedel, t.ex. ikoner i verktygsfältet för att komma åt mappar, samlingar och kataloger.

>[!NOTE]
>
>Om du aktiverar tjänsterna [!UICONTROL Dag CQ DAM Event Recorder] och [!UICONTROL DAM Event Purge] (händelsetömning) ökas skrivåtgärderna till JCR och sökindexering, vilket ökar inläsningen på AEM-servern avsevärt. Den extra belastningen på AEM-servern kan påverka dess prestanda.

>[!CAUTION]
>
>Att hämta in, filtrera och rensa användaraktiviteter som krävs för Assets-startsidan medför höga prestanda. Därför bör administratörer konfigurera hemsidan effektivt för målanvändare.
>
>Adobe rekommenderar att administratörer och användare som utför gruppåtgärder undviker att använda funktionen Startsida för resurser för att förhindra att användaraktiviteter ökar. Dessutom kan administratörer exkludera inspelningsaktiviteter för specifika användare genom att konfigurera [!UICONTROL Dag CQ DAM Event Recorder] från [!UICONTROL Configuration Manager].
>
>Om du använder funktionen rekommenderar Adobe att du schemalägger tömningsfrekvensen baserat på serverbelastningen.
