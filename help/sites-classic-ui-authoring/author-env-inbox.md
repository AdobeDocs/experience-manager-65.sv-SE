---
title: Din inkorg
seo-title: Din inkorg
description: Du kan få meddelanden från olika områden i AEM, till exempel meddelanden om arbetsobjekt eller uppgifter som representerar åtgärder som du måste utföra på sidinnehållet.
seo-description: Du kan få meddelanden från olika områden i AEM, till exempel meddelanden om arbetsobjekt eller uppgifter som representerar åtgärder som du måste utföra på sidinnehållet.
uuid: e7ba9150-957d-4f84-a570-2f3d83792472
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: ce2a1475-49cf-43e6-bfb9-006884ce3881
docset: aem65
translation-type: tm+mt
source-git-commit: bcb1840d23ae538c183eecb0678b6a75d346aa50

---


# Din inkorg{#your-inbox}

Du kan få meddelanden från olika områden i AEM, till exempel meddelanden om arbetsobjekt eller uppgifter som representerar åtgärder som du måste utföra på sidinnehållet.

Du får dessa meddelanden i två inkorgar, som avgränsas med typen av meddelanden:

* En inkorg där du kan se de meddelanden du får som ett resultat av prenumerationer beskrivs i följande avsnitt.
* En särskild inkorg för arbetsflödesobjekt beskrivs i dokumentet [Delta i arbetsflöden](/help/sites-classic-ui-authoring/classic-workflows-participating.md) .

## Visa meddelanden {#viewing-your-notifications}

Så här visar du dina meddelanden:

1. Öppna meddelandeinkorgen: i **webbplatskonsolen** klickar du på användarknappen i det övre högra hörnet och väljer **Meddelandeinkorgen**.

   ![screen_shot_2012-02-08at105226am](assets/screen_shot_2012-02-08at105226am.png)

   >[!NOTE]
   >
   >Du kan även komma åt konsolen direkt i webbläsaren; till exempel:
   >
   >
   >` https://<host>:<port>/libs/wcm/core/content/inbox.html`

1. Dina meddelanden visas. Du kan vidta åtgärder efter behov:

   * [Prenumerera på meddelanden](#subscribing-to-notifications)
   * [Bearbetar dina meddelanden](#processing-your-notifications)
   ![chlimage_1-4](assets/chlimage_1-4.jpeg)

## Prenumerera på meddelanden {#subscribing-to-notifications}

Så här prenumererar du på meddelanden:

1. Öppna meddelandeinkorgen: i **webbplatskonsolen** klickar du på användarknappen i det övre högra hörnet och väljer **Meddelandeinkorgen**.

   ![screen_shot_2012-02-08at105226am-1](assets/screen_shot_2012-02-08at105226am-1.png)

   >[!NOTE]
   >
   >Du kan även komma åt konsolen direkt i webbläsaren; till exempel:
   >
   >
   >`https://<host>:<port>/libs/wcm/core/content/inbox.html`

1. **Klicka på** Konfigurera... i det övre vänstra hörnet för att öppna konfigurationsdialogrutan.

   ![screen_shot_2012-02-08at11056am](assets/screen_shot_2012-02-08at111056am.png)

1. Välj meddelandekanal:

   * **Inkorg**: meddelanden visas i din AEM-inkorg.
   * **E-post**: meddelanden skickas via e-post till den e-postadress som är definierad i din användarprofil.
   >[!NOTE]
   >
   >Ett par inställningar måste konfigureras för att kunna meddelas via e-post. Det går också att anpassa e-postmallen eller lägga till en e-postmall för ett nytt språk. Information om hur du konfigurerar e-postmeddelanden i AEM finns i [Konfigurera e-postmeddelanden](/help/sites-administering/notification.md#configuringemailnotification) .

1. Välj de sidåtgärder som ska meddelas:

   * Aktiverad: när en sida har aktiverats.
   * Inaktiverad: när en sida har inaktiverats.
   * Borttagen (syndikering): när en sida har tagits bort-replikerats, dvs. när en borttagningsåtgärd som har utförts på en sida har replikerats.
När en sida tas bort eller flyttas replikeras en borttagningsåtgärd automatiskt: sidan tas bort på källinstansen där borttagningsåtgärden utfördes och på målinstansen som definierats av replikeringsagenterna.

   * Ändrad: när en sida har ändrats.
   * Skapad: när en sida har skapats.
   * Borttagen: när en sida har tagits bort genom sidborttagningsåtgärden.
   * Utrullad: när en sida har rullats ut.

1. Definiera sökvägarna för sidorna som du ska meddelas om:

   * Klicka på **Lägg till** för att lägga till en ny rad i tabellen.
   * Klicka på tabellcellen **Bana** och ange sökvägen, t.ex. `/content/docs`.

   * Vill du bli meddelad för alla sidor som tillhör underträdet, anger du **Exakt?** till **Nej**.
Vill du bara få meddelanden om åtgärder på sidan som definieras av sökvägen, anger du **Exakt?** till **Ja**.

   * Om du vill tillåta regeln anger du **Regel** till **Tillåt**. Om den är inställd på **Neka**, nekas regeln men tas inte bort och kan tillåtas senare.
   Om du vill ta bort en definition markerar du raden genom att klicka på en tabellcell och klickar på **Ta bort**.

1. Spara konfigurationen genom att klicka på **OK** .

## Bearbetar dina meddelanden {#processing-your-notifications}

Om du har valt att ta emot meddelanden i din AEM-inkorg fyller din inkorg i med meddelanden. Du kan [visa dina meddelanden](#viewing-your-notifications) och sedan välja obligatoriska meddelanden för att:

* Godkänn den genom att klicka på **Godkänn**: värdet i kolumnen **Läs** anges till **true**.

* Ta bort den genom att klicka på **Ta bort**.

![chlimage_1-5](assets/chlimage_1-5.jpeg)
