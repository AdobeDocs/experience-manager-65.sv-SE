---
title: Meddelandefunktion
description: Lär dig konfigurera meddelandefunktionen i AEM Communities så att communitymedlemmarna kan interagera med varandra mer privat.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
docset: aem65
exl-id: d121dc05-7d15-44ba-8d2d-b59d6c6480c8
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '952'
ht-degree: 0%

---

# Meddelandefunktion {#messaging-feature}

Förutom den synliga interaktionen som sker i forum och i kommentarer, gör meddelandefunktionen i AEM Communities det möjligt för communitymedlemmar att interagera med varandra mer privat.

Den här funktionen kan inkluderas när en [communitywebbplats](/help/communities/overview.md#communitiessites) skapas.

Med meddelandefunktionen kan du göra följande:

**A** - skicka ett meddelande till en eller flera community-medlemmar

**B** - skicka direktmeddelanden i [bulk till medlemsgrupper](/help/communities/messaging.md#group-messaging)

**C** - skicka ett meddelande med bifogade filer

**D** - vidarebefordra ett meddelande

**E** - svara på ett meddelande

**F** - ta bort ett meddelande

**G** - återställ ett borttaget meddelande

![messaging-section](assets/messaging-section.png)

![restore-message](assets/restore-message.png)

Information om hur du aktiverar och ändrar meddelandefunktionen finns i:

* [Konfigurera meddelanden](/help/communities/messaging.md) för administratörer
* [Meddelandeverktyg](/help/communities/essentials-messaging.md) för utvecklare

>[!NOTE]
>
>Det går inte att lägga till `Compose Message, Message, or Message List` komponenter (hittades i `Communities`-komponentgruppen) på en sida i redigeringsläge för författare.

## Konfigurera meddelandekomponenter {#configure-messaging-components}

När meddelanden har aktiverats för en community-webbplats konfigureras den utan någon ytterligare konfiguration. Informationen tillhandahålls om det finns behov av att ändra standardkonfigurationen.

### Konfigurera meddelandelista (meddelanderuta) {#configure-message-list-message-box}

Om du vill ändra konfigurationen för listan med meddelanden för sidorna **Inkorg**, **Skickat** och **Papperskorg** i meddelandefunktionen öppnar du webbplatsen i [redigeringsläget för författare](/help/communities/sites-console.md#authoring-site-content) .

1. I `Preview`-läget väljer du länken **Meddelanden** för att öppna huvudmeddelandesidan. Välj sedan antingen **Inkorg**, **Skickat** eller **Papperskorgen** för att konfigurera komponenten för den meddelandelistan.

1. Markera komponenten på sidan i `Edit`-läge.
1. Om du vill komma åt konfigurationsdialogrutan avbryter du arv genom att välja ikonen `link`.
När arvet har avbrutits går det att välja konfigurationsikonen för att öppna konfigurationsdialogrutan.

1. När konfigurationen är klar måste du återställa arvet genom att välja ikonen `broken link`.

![configure-message-list](assets/configure-message-list.png)

#### fliken Grundläggande {#basic-tab}

![basic-tab-messagelist](assets/basic-tab-messagelist.png)

* **Tjänstväljare**

  (*Obligatoriskt*) Ange värdet för egenskapen **`serviceSelector.name`** från [AEM Communities Messaging Operations Service](/help/communities/messaging.md#messaging-operations-service).

* **Disponera sida**

  (*Obligatorisk*) Den sida som ska öppnas när en medlem klickar på knappen **`Reply`**. Målsidan ska innehålla formuläret **Disponera meddelande**.

* **Svara/visa som resurs**

  Om det här alternativet är markerat refererar URL:en för svar och Visa URL till en resurs, annars skickas data som frågeparametrar i URL:en.

* **Profilvisningsformulär**

  Det profilformulär som ska användas för att visa avsändarprofilen.

* **Papperskorgen**

  Om den här meddelandelistekomponenten är markerad visas endast meddelanden som har flaggats som borttagna (papperskorg).

* **Mappsökvägar**

  (*Obligatoriskt*) Refererar till de värden som angetts för **inbox.path.name** och **sentitems.path.name** i [AEM Communities Messaging Operations Service](/help/communities/messaging.md#messaging-operations-service). När du konfigurerar för en `Inbox` lägger du till en post med värdet **inbox.path.name**. När du konfigurerar för en `Outbox` lägger du till en post med värdet för **sentitems.path.name**. När du konfigurerar för `Trash` lägger du till två poster med båda värdena.

#### Fliken Visa {#display-tab}

![display-tab-message-list](assets/display-tab-message-list.png)

* **Markera läsknapp**

  Om det här alternativet är markerat visas en `Read`-knapp som tillåter att ett meddelande markeras som läst.

* **Markera som oläst-knapp**

  Om det här alternativet är markerat visas en `Mark Unread`-knapp som tillåter att ett meddelande markeras som läst.

* **Ta bort-knapp**

  Om det här alternativet är markerat visas en `Delete`-knapp som tillåter att ett meddelande markeras som läst. Duplicerar borttagningsfunktionen om **`Message Options`** också är markerad.

* **Meddelandealternativ**

  Om det här alternativet är markerat visas knapparna **`Reply`**, **`Reply All`**, **`Forward`** och **`Delete`** så att ett meddelande kan skickas igen eller tas bort. Duplicerar borttagningsfunktionen om **`Delete Button`** också är markerad.

* **Meddelanden per sida**

  Det angivna antalet är det högsta antalet meddelanden som visas per sida i ett sidnumreringsschema. Om inget tal anges (vänster tomt) visas alla meddelanden och ingen sidnumrering visas.

* **Tidsstämpelmönster**

  Ange tidsstämpelmönster för ett eller flera språk. Standard är för en, de, fr, it, es, ja, zh_CN, ko_KR.

* **Visa användare**

  Välj antingen **`Sender`** eller **`Recipients`** så att du kan bestämma om du vill visa avsändaren eller mottagarna.

### Konfigurera dispositionsmeddelande {#configure-compose-message}

Om du vill ändra konfigurationen för den sammansatta meddelandesidan öppnar du webbplatsen i [redigeringsläget för författare](/help/communities/sites-console.md#authoring-site-content).

* I `Preview`-läget väljer du länken **Meddelanden** för att öppna huvudmeddelandesidan. Välj sedan knappen Nytt meddelande så att du kan öppna sidan `Compose Message`.

* I läget `Edit` väljer du huvudkomponenten på sidan som innehåller meddelandetexten.
* Om du vill komma åt konfigurationsdialogrutan avbryter du arv genom att välja ikonen `link`.
När arvet har avbrutits går det att välja konfigurationsikonen för att öppna konfigurationsdialogrutan.

* När konfigurationen är klar måste du återställa arvet genom att välja ikonen `broken link`.

![config-compose-message](assets/config-compose-message.png)

#### fliken Grundläggande {#basic-tab-1}

![basic-tab-compose](assets/basic-tab-compose.png)

* **Omdirigerings-URL**

  Ange URL-adressen till sidan som visas när meddelandet har skickats. Exempel: `../messaging.html`.

* **Avbryt URL**

  Ange URL-adressen till sidan som visas om avsändaren avbryter meddelandet. Exempel: `../messaging.html`.

* **Maximal längd för meddelandets ämne**

  Det maximala antalet tecken som tillåts i fältet Ämne. Till exempel 500. Standard är ingen gräns.

* **Maximal längd för meddelandetext**

  Det högsta antalet tecken som tillåts i fältet Innehåll. Exempel: 10000. Standard är ingen gräns.

* **Tjänstväljare**

  (*Obligatoriskt*) Ange värdet för egenskapen **`serviceSelector.name`** från [AEM Communities Messaging Operations Service](/help/communities/messaging.md#messaging-operations-service).

#### Fliken Visa {#display-tab-1}

![display-tab-compose](assets/display-tab-compose.png)

* **Visa ämnesfält**

  Om det här alternativet är markerat visar du fältet `Subject` och aktiverar att du lägger till ett ämne i meddelandet. Standard är inte markerat.

* **Ämnesetikett**

  Ange den text som du vill ska visas bredvid fältet `Subject`. Standardvärdet är `Subject`.

* **Visa fält för bifogad fil**

  Om du markerar det här alternativet visas fältet `Attachment` och det går att lägga till bifogade filer i meddelandet. Standard är inte markerat.

* **Bifoga filetikett**

  Ange den text som du vill ska visas bredvid fältet `Attachment`. Standardvärdet är **`Attach File`**.

* **Visa innehållsfält**

  Om det här alternativet är markerat visar du fältet `Content` och aktiverar att du lägger till en meddelandetext. Standard är inte markerat.

* **Innehållsetikett**

  Ange den text som du vill ska visas bredvid fältet `Content`. Standardvärdet är **`Body`**.

* **Med RTF-redigerare**

  Om det här alternativet är markerat används en anpassad innehållstextruta med en egen RTF-redigerare. Standard är inte markerat.

* **Tidsstämpelmönster**

  Ange tidsstämpelmönster för ett eller flera språk. Standard är för en, de, fr, it, es, ja, zh_CN, ko_KR.
