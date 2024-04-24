---
title: Konfigurera meddelanden
description: Läs om meddelandefunktionen i AEM Communities som gör det möjligt för besökare på den inloggade webbplatsen (medlemmar) att skicka meddelanden till varandra.
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
docset: aem65
role: Admin
exl-id: ee94f093-fd14-49f2-9990-fbe853d924b1
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '840'
ht-degree: 0%

---

# Konfigurera meddelanden {#configure-messaging}

## Ökning {#overview}

Meddelandefunktionen för AEM Communities gör det möjligt för besökare på den inloggade webbplatsen (medlemmar) att skicka meddelanden till varandra som är tillgängliga när de loggar in på webbplatsen.

Meddelanden är aktiverade för en community-webbplats genom att markera en kryssruta under [communitysajt](/help/communities/sites-console.md).

Den här sidan innehåller information om standardkonfigurationen och eventuella justeringar.

Mer information för utvecklare finns i [Viktiga meddelanden](/help/communities/essentials-messaging.md).

## Tjänsten Meddelandeåtgärder {#messaging-operations-service}

Konfigurationen [Tjänsten AEM Communities Messaging Operations](https://localhost:4502/system/console/configMgr/com.adobe.cq.social.messaging.client.endpoints.impl.MessagingOperationsServiceImpl) identifierar slutpunkten som hanterar meddelanderelaterade begäranden, de mappar som tjänsten ska använda för att lagra meddelanden och, om meddelanden kan innehålla bifogade filer, vilka filtyper som tillåts.

För communitysajter som skapats med `Communities Sites console`finns det en instans av tjänsten med inkorgen inställd på `/mail/inbox`.

### Tjänsten Community Messaging Operations {#community-messaging-operations-service}

Så som visas nedan finns det en konfiguration för tjänsten för webbplatser som skapats med [guide för att skapa webbplatser](/help/communities/sites-console.md). Du kan visa eller redigera konfigurationen genom att välja pennikonen bredvid konfigurationen.

![meddelandeåtgärder](assets/messaging-operations.png)

### Lägg till ny konfiguration {#add-new-configuration}

Om du vill lägga till en konfiguration väljer du plustecknet &#39;**+**&#39; -ikon bredvid tjänstens namn :

* **Meddelandefält Tillåtslista**

  Anger egenskaperna för den Compose Message-komponent som användare kan redigera och behålla. Om nya formulärelement läggs till måste element-ID:t läggas till om det ska lagras i SRP. Standard är två poster: *ämne* och *innehåll*.

* **Storleksgräns för meddelanderuta**

  Maximalt antal byte i varje användares meddelanderuta. Standard är *1073741824* (1 GB)

* **Antal meddelanden**

  Det totala antalet meddelanden som tillåts per användare. Värdet -1 anger att ett obegränsat antal meddelanden tillåts, enligt storleksgränsen för meddelanderutan. Standard är *10000* (10 k).

* **Meddela leveransfel**

  Om du markerar det här alternativet ska du meddela avsändaren om meddelandeleveransen misslyckas för vissa mottagare. Standard är *checked*.

* **Avsändarens ID för felleverans**

  Namnet på den avsändare som visas i meddelandet som inte kunde levereras. Standard är *errorNotifier*.

* **Mallsökväg för felmeddelande**

  Absolut sökväg till leveransmallroten för misslyckade meddelanden. Standard är */etc/notification/messaging/default*.

* **Antal återförsök**

  Antal försök att skicka om meddelande som inte kan levereras. Standard är *3*.

* **Vänta mellan återförsök**

  Antal sekunder mellan försök att skicka meddelandet igen om det inte går att skicka. Standard är *100* (sekunder).

* **Antal poolstorlekar för uppdatering**

  Antal samtidiga trådar som används för att räkna uppdatering. Standard är *10*.

* **Inkorgsbana**

  (*Obligatoriskt*) Sökvägen i förhållande till användarens nod (/home/users/*användarnamn*), som används för `inbox` mapp. Sökvägen får INTE avslutas med ett avslutande snedstreck (/). Standard är */mail/inbox*.

* **Sökväg för skickade objekt**

  (*Obligatoriskt*) Sökvägen i förhållande till användarens nod (/home/users/*användarnamn*), som används för `sent items` mapp. Sökvägen får INTE avslutas med ett avslutande snedstreck (/). Standard är */mail/sentitems* .

* **Supportbilagor**

  Om det här alternativet är markerat kan användare lägga till bilagor i sina meddelanden. Standard är *checked*.

* **Aktivera gruppmeddelanden**

  Om det här alternativet är markerat kan registrerade användare skicka massmeddelanden till en grupp medlemmar. Standard är *avmarkerad*.

* **Högsta antal totalt antal mottagare**

  Om gruppmeddelanden är aktiverat anger du det högsta antal mottagare som gruppmeddelanden kan skickas till åt gången. Standard är *100*.

* **Batchstorlek**

  Antal meddelanden som ska grupperas tillsammans för en sändning när den skickas till en stor grupp mottagare. Standard är *100*.

* **Sammanlagd storlek för bifogade filer**

  Om supportAttachments är markerat anger det här värdet den största tillåtna totala storleken (i byte) för alla bilagor. Standard är *104857600* (100 MB).

* **Bilagetyp blockeringslista**

  En blockeringslista med filnamnstillägg, prefix med &#39;**.**&#39;, som inte godkänns av systemet. Om tillägget inte blocklist tillåts det. Tillägg kan läggas till eller tas bort med **+** och **-**&#39; ikoner.

* **Tillåtna bilagetyper**

  **(*Åtgärd krävs*)** En tillåtelselista med filnamnstillägg, motsatsen till blockeringslista. Om du vill tillåta alla filnamnstillägg, förutom de som blocklist, använder du **-**&#39; om du vill ta bort en enskild tom post.

* **Tjänstväljare**

  (*Obligatoriskt*) En absolut sökväg (slutpunkt) genom vilken tjänsten anropas (en virtuell resurs). Roten för den valda sökvägen måste vara en som ingår i *Körningsbanor* konfigurationsinställning för OSGi-konfiguration [`Apache Sling Servlet/Script Resolver and Error Handler`](https://localhost:4502/system/console/configMgr/org.apache.sling.servlets.resolver.SlingServletResolver), till exempel `/bin/`, `/apps/`och `/services/`. Om du vill välja den här konfigurationen för en webbplats meddelandefunktion anges den här slutpunkten som **`Service selector`** värdet för `Message List and Compose Message components` (se [Meddelandefunktion](/help/communities/configure-messaging.md)).

  Standardvärdet är */bin/messaging* .

* **Tillåtelselista i fält**

  Använd **Meddelandefält Tillåtslista**.

>[!CAUTION]
>
>Varje gång `Messaging Operations Service` konfigurationen öppnas för redigering, om `allowedAttachmentTypes.name` om den har tagits bort läses en tom post in så att egenskapen kan konfigureras. En enda tom post inaktiverar effektivt bifogade filer.
>
>Om du vill tillåta alla filnamnstillägg, förutom de som blocklist, använder du **-**&#39; om du vill (igen) ta bort en enskild tom post innan du klickar på **Spara**.

## Gruppmeddelanden {#group-messaging}

Om du vill tillåta registrerade användare att skicka direktmeddelanden i grupp till användargrupper, ska du se till att **Aktivera gruppmeddelanden** i följande två instanser av **Meddelandeåtgärder** konfiguration:

* `com.adobe.cq.social.messaging.client.endpoints.impl.MessagingOperationsServiceImpl~social-console`
* `com.adobe.cq.social.messaging.client.endpoints.impl.MessagingOperationsServiceImpl~social-messaging`

**Tjänsten Meddelandeåtgärder: social konsol**

![social-console-op-service](assets/social-console-op-service.png)

**Tjänsten Meddelandeåtgärder: sociala meddelanden**

![social-message-op-service](assets/social-message-op-service.png)

## Felsökning {#troubleshooting}

Ett sätt att felsöka problem är att aktivera [felsökningsmeddelanden i loggen.](/help/sites-administering/troubleshooting.md)

Se även [Loggare och skribenter för enskilda tjänster](/help/sites-deploying/configure-logging.md#loggers-and-writers-for-individual-services).

Paketet som ska övervakas är `com.adobe.cq.social.messaging`.
