---
title: Din inkorg
description: Du kan få meddelanden från olika AEM, till exempel meddelanden om arbetsobjekt eller uppgifter som representerar åtgärder som du måste utföra på sidinnehållet.
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
docset: aem65
exl-id: 52ea2ca2-eb1c-4bed-b52d-feef37c6afd6
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '569'
ht-degree: 0%

---

# Din inkorg{#your-inbox}

Du kan få meddelanden från olika AEM, till exempel meddelanden om arbetsobjekt eller uppgifter som representerar åtgärder som du måste utföra på sidinnehållet.

Du får dessa meddelanden i två inkorgar, som avgränsas med typen av meddelanden:

* En inkorg där du kan se meddelanden som du får som ett resultat av prenumerationer beskrivs i följande avsnitt.
* En särskild inkorg för arbetsflödesobjekt beskrivs i [Delta i arbetsflöden](/help/sites-classic-ui-authoring/classic-workflows-participating.md) -dokument.

## Visa meddelanden {#viewing-your-notifications}

Så här visar du dina meddelanden:

1. Öppna meddelandeinkorgen: i **Webbplatser** klickar du på användarknappen i det övre högra hörnet och väljer **Inkorgen för meddelanden**.

   ![screen_shot_2012-02-08at105226am](assets/screen_shot_2012-02-08at105226am.png)

   >[!NOTE]
   >
   >Du kan även komma åt konsolen direkt i webbläsaren, till exempel:
   >
   >
   >` https://<host>:<port>/libs/wcm/core/content/inbox.html`

1. Dina meddelanden visas. Du kan vidta åtgärder efter behov:

   * [Prenumerera på meddelanden](#subscribing-to-notifications)
   * [Bearbetar dina meddelanden](#processing-your-notifications)

   ![chlimage_1-4](assets/chlimage_1-4.jpeg)

## Prenumerera på meddelanden {#subscribing-to-notifications}

Så här prenumererar du på meddelanden:

1. Öppna meddelandeinkorgen: i **Webbplatser** klickar du på användarknappen i det övre högra hörnet och väljer **Inkorgen för meddelanden**.

   ![screen_shot_2012-02-08at105226am-1](assets/screen_shot_2012-02-08at105226am-1.png)

   >[!NOTE]
   >
   >Du kan även komma åt konsolen direkt i webbläsaren, till exempel:
   >
   >
   >`https://<host>:<port>/libs/wcm/core/content/inbox.html`

1. Klicka **Konfigurera...** i det övre vänstra hörnet för att öppna konfigurationsdialogrutan.

   ![screen_shot_2012-02-08at11056am](assets/screen_shot_2012-02-08at111056am.png)

1. Välj meddelandekanal:

   * **Inkorg**: meddelanden visas i AEM Inkorg.
   * **E-post**: meddelanden skickas via e-post till den e-postadress som har definierats i din användarprofil.

   >[!NOTE]
   >
   >Ett fåtal inställningar måste konfigureras för att kunna meddelas via e-post. Det går också att anpassa e-postmallen eller lägga till en e-postmall för ett nytt språk. Se [Konfigurerar e-postmeddelande](/help/sites-administering/notification.md#configuringemailnotification) för att konfigurera e-postmeddelanden i AEM.

1. Välj de sidåtgärder som ska meddelas:

   * Aktiverad: när en sida har aktiverats.
   * Inaktiverad: när en sida har inaktiverats.
   * Borttagen (syndikering): När en sida har tagits bort-replikerats, d.v.s. när en borttagningsåtgärd som har utförts på en sida replikeras.
När en sida tas bort eller flyttas replikeras en borttagningsåtgärd automatiskt: sidan tas bort från källinstansen där borttagningsåtgärden utfördes och på målinstansen som definierats av replikeringsagenterna.

   * Ändrad: när en sida har ändrats.
   * Skapad: när en sida har skapats.
   * Borttagen: När en sida har tagits bort via sidborttagningsåtgärden.
   * Utrullad: när en sida har rullats ut.

1. Definiera sökvägarna för sidorna som du ska meddelas om:

   * Klicka **Lägg till** om du vill lägga till en ny rad i tabellen.
   * Klicka på **Bana** tabellcell och ange sökvägen, till exempel `/content/docs`.

   * Om du vill bli meddelad för alla sidor som tillhör underträdet anger du **Exakt?** till **Nej**.
Om du bara vill bli meddelad om åtgärder på sidan som definieras av sökvägen anger du **Exakt?** till **Ja**.

   * Om du vill tillåta regeln anger du **Regel** till **Tillåt**. Om inställt på **Neka**, nekas regeln men tas inte bort och kan tillåtas senare.

   Om du vill ta bort en definition markerar du raden genom att klicka på en tabellcell och klickar på **Ta bort**.

1. Klicka **OK** för att spara konfigurationen.

## Bearbetar dina meddelanden {#processing-your-notifications}

Om du har valt att ta emot meddelanden i din AEM Inkorg fylls din inkorg i med meddelanden. Du kan [visa dina meddelanden](#viewing-your-notifications)väljer du sedan de meddelanden som krävs för att:

* Godkänn den genom att klicka **Godkänn**: värdet i **Läs** kolumnen är inställd på **true**.

* Ta bort den genom att klicka **Ta bort**.

![chlimage_1-5](assets/chlimage_1-5.jpeg)
