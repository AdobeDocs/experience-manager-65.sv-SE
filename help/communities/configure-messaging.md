---
title: Meddelandefunktion
seo-title: Messaging Feature
description: Konfigurera meddelandekomponenter
seo-description: Configuring Messaging components
uuid: 8b99ded1-aec2-40c9-82d5-e2e404f614ca
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 9d952604-f9ef-498f-937b-871817c80226
docset: aem65
exl-id: d121dc05-7d15-44ba-8d2d-b59d6c6480c8
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '927'
ht-degree: 0%

---

# Meddelandefunktion {#messaging-feature}

Förutom den synliga interaktionen som sker i forum och i kommentarer, gör meddelandefunktionen i AEM Communities det möjligt för communitymedlemmar att interagera med varandra mer privat.

Den här funktionen kan inkluderas när en [communitywebbplats](/help/communities/overview.md#communitiessites) skapas.

Med meddelandefunktionen kan du:

**A** - skicka ett meddelande till en eller flera community-medlemmar

**B** - skicka direktmeddelanden i [bulk to community member groups](/help/communities/messaging.md#group-messaging)

**C** - skicka ett meddelande med bilagor

**D** - vidarebefordra ett meddelande

**E** - svara på ett meddelande

**F** - ta bort ett meddelande

**G** - återställ ett borttaget meddelande

![meddelandesektion](assets/messaging-section.png)

![restore-message](assets/restore-message.png)

Information om hur du aktiverar och ändrar meddelandefunktionen finns i:

* [Konfigurera meddelanden](/help/communities/messaging.md) för administratörer
* [Viktiga meddelanden](/help/communities/essentials-messaging.md) för utvecklare

>[!NOTE]
>
>Det går inte att lägga till `Compose Message, Message, or Message List` komponenter (finns i `Communities`till en sida i redigeringsläge.

## Konfigurera meddelandekomponenter {#configure-messaging-components}

När meddelanden har aktiverats för en community-webbplats konfigureras den utan någon ytterligare konfiguration. Informationen tillhandahålls om det finns behov av att ändra standardkonfigurationen.

### Konfigurera meddelandelista (meddelanderuta) {#configure-message-list-message-box}

Så här ändrar du konfigurationen för listan med meddelanden för **Inkorg**, **Skickade objekt** och **Papperskorgen** sidor med meddelandefunktionen, öppna webbplatsen i [redigeringsläge för författare](/help/communities/sites-console.md#authoring-site-content).

1. I `Preview` läge, välj **Meddelanden** för att öppna meddelandesidan. Välj sedan antingen **Inkorg**, **Skickade objekt** eller **Papperskorgen** för att konfigurera komponenten för den meddelandelistan.

1. I `Edit` markerar du komponenten på sidan.
1. Om du vill öppna konfigurationsdialogrutan avbryter du arv genom att välja `link` ikon.
När arvet har avbrutits går det att välja konfigurationsikonen för att öppna konfigurationsdialogrutan.

1. När konfigurationen är klar måste du återställa arvet genom att välja `broken link` ikon.

![configure-message-list](assets/configure-message-list.png)

#### Fliken Grundläggande {#basic-tab}

![basic-tab-messagelist](assets/basic-tab-messagelist.png)

* **Tjänstväljare**

   (*Obligatoriskt*) Ange värdet för egenskapen **`serviceSelector.name`** från [Tjänsten AEM Communities Messaging Operations](/help/communities/messaging.md#messaging-operations-service).

* **Skapa sida**

   (*Obligatoriskt*) Den sida som ska öppnas när en medlem klickar på **`Reply`** -knappen. Målsidan ska innehålla **Skriv meddelande** formulär.

* **Svara/visa som resurs**

   Om det här alternativet är markerat refererar URL:en för svar och vy till en resurs, annars skickas data som frågeparametrar i URL:en.

* **Profilvisningsformulär**

   Det profilformulär som ska användas för att visa avsändarprofilen.

* **Pappersmapp**

   Om den här meddelandelistekomponenten är markerad visas endast meddelanden som har flaggats som borttagna (papperskorg).

* **Mappsökvägar**

   (*Obligatoriskt*) Referera till de värden som angetts för **inbox.path.name** och **sentitems.path.name** i [Tjänsten AEM Communities Messaging Operations](/help/communities/messaging.md#messaging-operations-service). Vid konfigurering för en `Inbox`, lägger till en post med värdet för **inbox.path.name**. Vid konfigurering för en `Outbox`, lägger till en post med värdet för **sentitems.path.name**. Vid konfigurering för `Trash`lägger du till två poster med båda värdena.

#### Fliken Visa {#display-tab}

![display-tab-message-list](assets/display-tab-message-list.png)

* **Markera läsknapp**

   Om det här alternativet är markerat visas en `Read`så att ett meddelande kan markeras som läst.

* **Markera som oläst-knapp**

   Om det här alternativet är markerat visas en `Mark Unread` så att ett meddelande kan markeras som läst.

* **Ta bort-knapp**

   Om det här alternativet är markerat visas en `Delete` så att ett meddelande kan markeras som läst. Duplicerar borttagningsfunktionen om **`Message Options`** också markeras.

* **Meddelandealternativ**

   Om det här alternativet är markerat visas **`Reply`**, **`Reply All`**, **`Forward`** och **`Delete`** -knappar som gör att ett meddelande kan skickas igen eller tas bort. Duplicerar borttagningsfunktionen om **`Delete Button`** också markeras.

* **Meddelanden per sida**

   Det angivna antalet är det högsta antalet meddelanden som visas per sida i ett sidnumreringsschema. Om inget tal anges (vänster tomt) visas alla meddelanden och ingen sidnumrering visas.

* **Tidsstämpelmönster**

   Ange tidsstämpelmönster för ett eller flera språk. Standard är för en, de, fr, it, es, ja, zh_CN, ko_KR.

* **Visa användare**

   Välj antingen **`Sender`** eller **`Recipients`** för att avgöra om avsändaren eller mottagarna ska visas.

### Konfigurera dispositionsmeddelande {#configure-compose-message}

Om du vill ändra konfigurationen för den sammansatta meddelandesidan öppnar du webbplatsen i [redigeringsläge för författare](/help/communities/sites-console.md#authoring-site-content).

* I `Preview` läge, välj **Meddelanden** för att öppna meddelandesidan. Klicka sedan på knappen Nytt meddelande för att öppna dialogrutan `Compose Message` sida.

* I `Edit` markerar du huvudkomponenten på sidan som innehåller meddelandetexten.
* Om du vill öppna konfigurationsdialogrutan avbryter du arv genom att välja `link` ikon.
När arvet har avbrutits går det att välja konfigurationsikonen för att öppna konfigurationsdialogrutan.

* När konfigurationen är klar måste du återställa arvet genom att välja `broken link` ikon.

![config-compose-message](assets/config-compose-message.png)

#### Fliken Grundläggande {#basic-tab-1}

![basic-tab-compose](assets/basic-tab-compose.png)

* **Omdirigerings-URL**

   Ange URL-adressen till sidan som visas när meddelandet har skickats. Till exempel, `../messaging.html`.

* **Avbryt URL**

   Ange URL-adressen till sidan som visas om avsändaren avbryter meddelandet. Till exempel, `../messaging.html`.

* **Maximal längd för meddelandets ämne**

   Det maximala antalet tecken som tillåts i fältet Ämne. Till exempel 500. Standard är ingen gräns.

* **Maximal längd för meddelandetext**

   Det högsta antalet tecken som tillåts i fältet Innehåll. Exempel: 10000. Standard är ingen gräns.

* **Tjänstväljare**

   (*Obligatoriskt*) Ange värdet för egenskapen **`serviceSelector.name`** från [Tjänsten AEM Communities Messaging Operations](/help/communities/messaging.md#messaging-operations-service).

#### Fliken Visa {#display-tab-1}

![display-tab-compose](assets/display-tab-compose.png)

* **Visa ämnesfält**

   Om du markerar det här alternativet visas `Subject` och gör det möjligt att lägga till ett ämne i meddelandet. Standard är inte markerat.

* **Ämnesetikett**

   Ange den text som ska visas intill `Subject` fält. Standard är `Subject`.

* **Visa fält för bifogad fil**

   Om du markerar det här alternativet visas `Attachment` och gör det möjligt att lägga till bifogade filer i meddelandet. Standard är inte markerat.

* **Bifoga filetikett**

   Ange den text som ska visas intill `Attachment` fält. Standard är **`Attach File`**.

* **Visa innehållsfält**

   Om du markerar det här alternativet visas `Content` och aktivera tillägg av meddelandetext. Standard är inte markerat.

* **Innehållsetikett**

   Ange den text som ska visas intill `Content` fält. Standard är **`Body`**.

* **Med RTF-redigerare**

   Om det här alternativet är markerat används en anpassad innehållstextruta med en egen RTF-redigerare. Standard är inte markerat.

* **Tidsstämpelmönster**

   Ange tidsstämpelmönster för ett eller flera språk. Standard är för en, de, fr, it, es, ja, zh_CN, ko_KR.
