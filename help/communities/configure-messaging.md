---
title: Meddelandefunktion
seo-title: Meddelandefunktion
description: Konfigurera meddelandekomponenter
seo-description: Konfigurera meddelandekomponenter
uuid: 8b99ded1-aec2-40c9-82d5-e2e404f614ca
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 9d952604-f9ef-498f-937b-871817c80226
docset: aem65
translation-type: tm+mt
source-git-commit: e8d8bf89971d3d9d5ec150308dda247aa53c77bb

---


# Meddelandefunktion {#messaging-feature}

Förutom de allmänt synliga interaktioner som förekommer i forum och kommentarer, gör meddelandefunktionen i AEM Communities det möjligt för communitymedlemmar att interagera med varandra mer privat.

Den här funktionen kan inkluderas när en [communitywebbplats](/help/communities/overview.md#communitiessites) skapas.

Med meddelandefunktionen kan du:

**A** - skicka ett meddelande till en eller flera communitymedlemmar **B** - skicka direktmeddelanden i [grupp till communitymedlemsgrupper](/help/communities/messaging.md#group-messaging)**C** - skicka ett meddelande med bilagor **D** - vidarebefordra ett meddelande ************ E - svara på ett meddelandeF¥ - ta bort ett meddelande✔GUnder - återställ ett borttaget meddelande

![messaging-section](assets/messaging-section.png) ![restore-message](assets/restore-message.png)

Information om hur du aktiverar och ändrar meddelandefunktionen finns i:

* [Konfigurera meddelanden](/help/communities/messaging.md) för administratörer
* [Meddelandefunktioner](/help/communities/essentials-messaging.md) för utvecklare

>[!NOTE]
>
>Det går inte att lägga till `Compose Message, Message, or Message List` komponenter (finns i `Communities`komponentgruppen) på en sida i redigeringsläge för författare.

## Konfigurera meddelandekomponenter {#configure-messaging-components}

När meddelanden har aktiverats för en community-webbplats konfigureras den utan någon ytterligare konfiguration. Informationen tillhandahålls om det finns behov av att ändra standardkonfigurationen.

### Konfigurera meddelandelista (meddelanderuta) {#configure-message-list-message-box}

Om du vill ändra konfigurationen för listan med meddelanden för **sidorna Inkorgen**, **Skickat** och **Papperskorgen** i meddelandefunktionen öppnar du webbplatsen i [redigeringsläge](/help/communities/sites-console.md#authoring-site-content).

1. I `Preview`läget väljer du länken **Meddelanden** för att öppna huvudmeddelandesidan. Välj sedan **Inkorg**, **Skickat** eller **Papperskorgen** för att konfigurera komponenten för den meddelandelistan.

1. Markera komponenten på sidan i `Edit` läget.
1. Om du vill öppna konfigurationsdialogrutan avbryter du arv genom att markera `link`ikonen.
När arvet har avbrutits går det att välja konfigurationsikonen för att öppna konfigurationsdialogrutan.

1. När konfigurationen är klar är det nödvändigt att återställa arvet genom att markera `broken link` -ikonen.

![configure-message-list](assets/configure-message-list.png)

#### Fliken Grundläggande {#basic-tab}

![basic-tab-messagelist](assets/basic-tab-messagelist.png)

* **Tjänstväljare**

   (*Obligatoriskt*) Ange det här värdet för egenskapen **`serviceSelector.name`** från tjänsten [AEM](/help/communities/messaging.md#messaging-operations-service)Communities Messaging Operations.

* **Skapa sida**

   (*Obligatoriskt*) Den sida som ska öppnas när en medlem klickar på **`Reply`** . Målsidan ska innehålla **formuläret Dispositionsmeddelande** .

* **Svara/visa som resurs**

   Om det här alternativet är markerat refererar URL:en för svar och vy till en resurs, annars skickas data som frågeparametrar i URL:en.

* **Profilvisningsformulär**

   Det profilformulär som ska användas för att visa avsändarprofilen.

* **Pappersmapp**

   Om den här meddelandelistekomponenten är markerad visas endast meddelanden som har flaggats som borttagna (papperskorg).

* **Mappsökvägar**

   (*Obligatoriskt*) Refererar till de värden som angetts för **inbox.path.name** och **sentitems.path.name** i [AEM Communities Messaging Operations Service](/help/communities/messaging.md#messaging-operations-service). När du konfigurerar för en `Inbox`post lägger du till en post med värdet för **inbox.path.name**. När du konfigurerar för en `Outbox`post lägger du till en post med värdet för **sentitems.path.name**. När du konfigurerar för `Trash`lägger du till två poster med båda värdena.

#### Fliken Visa {#display-tab}

![display-tab-message-list](assets/display-tab-message-list.png)

* **Markera läsknapp**

   Om det här alternativet är markerat visas en `Read`knapp som gör att ett meddelande kan markeras som läst.

* **Markera som oläst-knapp**

   Om det här alternativet är markerat visas en `Mark Unread` knapp som gör att ett meddelande kan markeras som läst.

* **Ta bort-knapp**

   Om det här alternativet är markerat visas en `Delete`knapp som gör att ett meddelande kan markeras som läst. Duplicerar borttagningsfunktionen om **`Message Options`** även den är markerad.

* **Meddelandealternativ**

   Om du markerar det här alternativet visas **`Reply`** knappar **`Reply All`****`Forward`** **`Delete`** och knappar som gör att ett meddelande kan skickas igen eller tas bort. Duplicerar borttagningsfunktionen om **`Delete Button`** även den är markerad.

* **Meddelanden per sida**

   Det angivna antalet är det högsta antalet meddelanden som visas per sida i ett sidnumreringsschema. Om inget tal anges (vänster tomt) visas alla meddelanden och ingen sidnumrering visas.

* **Tidsstämpelmönster**

   Ange tidsstämpelmönster för ett eller flera språk. Standard är för en, de, fr, it, es, ja, zh_CN, ko_KR.

* **Visa användare**

   Välj antingen **`Sender`** eller **`Recipients`** för att bestämma om avsändaren eller mottagarna ska visas.

### Konfigurera dispositionsmeddelande {#configure-compose-message}

Om du vill ändra konfigurationen för den sammansatta meddelandesidan öppnar du webbplatsen i [redigeringsläge](/help/communities/sites-console.md#authoring-site-content).

* I `Preview` läget väljer du länken **Meddelanden** för att öppna huvudmeddelandesidan. Klicka sedan på knappen Nytt meddelande för att öppna `Compose Message` sidan.

* I `Edit` läget markerar du huvudkomponenten på sidan som innehåller meddelandetexten.
* Om du vill få åtkomst till konfigurationsdialogrutan avbryter du arv genom att markera `link` -ikonen.
När arvet har avbrutits går det att välja konfigurationsikonen för att öppna konfigurationsdialogrutan.

* När konfigurationen är klar är det nödvändigt att återställa arvet genom att markera `broken link` -ikonen.

![config-compose-message](assets/config-compose-message.png)

#### Fliken Grundläggande {#basic-tab-1}

![basic-tab-compose](assets/basic-tab-compose.png)

* **Omdirigerings-URL**

   Ange URL-adressen till sidan som visas när meddelandet har skickats. Exempel, `../messaging.html`.

* **Avbryt URL**

   Ange URL-adressen till sidan som visas om avsändaren avbryter meddelandet. Exempel, `../messaging.html`.

* **Maximal längd för meddelandets ämne**

   Det maximala antalet tecken som tillåts i fältet Ämne. Till exempel 500. Standard är ingen gräns.

* **Maximal längd för meddelandetext**

   Det högsta antalet tecken som tillåts i fältet Innehåll. Exempel: 10000. Standard är ingen gräns.

* **Tjänstväljare**

   (*Obligatoriskt*) Ange det här värdet för egenskapen **`serviceSelector.name`** från tjänsten [AEM](/help/communities/messaging.md#messaging-operations-service)Communities Messaging Operations.

#### Fliken Visa {#display-tab-1}

![display-tab-compose](assets/display-tab-compose.png)

* **Visa ämnesfält**

   Om du markerar det här alternativet visas `Subject` fältet och det går att lägga till ett ämne i meddelandet. Standard är inte markerat.

* **Ämnesetikett**

   Ange den text som ska visas bredvid `Subject` fältet. Standardvärdet är `Subject`.

* **Visa fält för bifogad fil**

   Om du markerar det här alternativet visas `Attachment` fältet och det går att lägga till bifogade filer i meddelandet. Standard är inte markerat.

* **Bifoga filetikett**

   Ange den text som ska visas bredvid `Attachment` fältet. Standardvärdet är **`Attach File`**.

* **Visa innehållsfält**

   Om du markerar det här alternativet visas `Content` fältet och det går att lägga till meddelandetexten. Standard är inte markerat.

* **Innehållsetikett**

   Ange den text som ska visas bredvid `Content` fältet. Standardvärdet är **`Body`**.

* **Med RTF-redigerare**

   Om det här alternativet är markerat används en anpassad innehållstextruta med en egen RTF-redigerare. Standard är inte markerat.

* **Tidsstämpelmönster**

   Ange tidsstämpelmönster för ett eller flera språk. Standard är för en, de, fr, it, es, ja, zh_CN, ko_KR.

