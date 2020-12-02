---
title: Konfigurera meddelanden
seo-title: Konfigurerar meddelanden
description: Communities messaging
seo-description: Communities messaging
uuid: 159dcf9d-7948-4a3d-9f51-a5b4d03e172b
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 232a0ec1-8dfc-41ec-84cc-69f9db494ea0
docset: aem65
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '826'
ht-degree: 0%

---


# Konfigurera meddelanden {#configure-messaging}

## Översikt {#overview}

Meddelandefunktionen för AEM Communities gör det möjligt för besökare på den inloggade webbplatsen (medlemmar) att skicka meddelanden till varandra som är tillgängliga när de loggar in på webbplatsen.

Meddelanden aktiveras för en community-webbplats genom att en kryssruta markeras när [communitywebbplatsen skapas](/help/communities/sites-console.md).

Den här sidan innehåller information om standardkonfigurationen och eventuella justeringar.

Mer information för utvecklare finns i [Messaging Essentials](/help/communities/essentials-messaging.md).

## Tjänsten Meddelandeåtgärder {#messaging-operations-service}

Konfigurationen [AEM Communities Messaging Operations Service](https://localhost:4502/system/console/configMgr/com.adobe.cq.social.messaging.client.endpoints.impl.MessagingOperationsServiceImpl) identifierar slutpunkten som hanterar meddelanderelaterade begäranden, mapparna som tjänsten ska använda för att lagra meddelanden och, om meddelanden kan innehålla bifogade filer, vilka filtyper som tillåts.

För communitysajter som skapats med `Communities Sites console` finns det redan en instans av tjänsten med inkorgen inställd på `/mail/inbox`.

### Tjänsten Community Messaging Operations {#community-messaging-operations-service}

Som framgår nedan finns det en konfiguration av tjänsten för webbplatser som skapats med [guiden Skapa plats](/help/communities/sites-console.md). Du kan visa eller redigera konfigurationen genom att välja pennikonen bredvid konfigurationen.

![meddelandeåtgärder](assets/messaging-operations.png)

### Lägg till ny konfiguration {#add-new-configuration}

Om du vill lägga till en ny konfiguration väljer du plusikonen **+** bredvid tjänstens namn:

* **Meddelandefält Tillåtslista**

   Anger egenskaperna för den Compose Message-komponent som användare kan redigera och behålla. Om nya formulärelement läggs till måste element-ID läggas till om det ska lagras i SRP. Standard är två poster: *subject* och *content*.

* **Storleksgräns för meddelanderuta**

   Maximalt antal byte i varje användares meddelanderuta. Standardvärdet är *1073741824* (1 GB).

* **Antal meddelanden**

   Det totala antalet meddelanden som tillåts per användare. Värdet -1 anger att ett obegränsat antal meddelanden tillåts, enligt storleksgränsen för meddelanderutan. Standardvärdet är *10000* (10k).

* **Meddela leveransfel**

   Om du markerar det här alternativet ska du meddela avsändaren om meddelandeleveransen misslyckas för vissa mottagare. Standardvärdet är *checked*.

* **Avsändarens ID för felleverans**

   Namnet på den avsändare som visas i meddelandet som inte kunde levereras. Standardvärdet är *errorNotifier*.

* **Mallsökväg för felmeddelande**

   Absolut sökväg till leveransmallroten för misslyckade meddelanden. Standardvärdet är */etc/notification/messaging/default*.

* **Antal återförsök**

   Antal försök att skicka om meddelande som inte kan levereras. Standardvärdet är *3*.

* **Vänta mellan återförsök**

   Antal sekunder mellan försök att skicka meddelandet igen om det inte går att skicka. Standardvärdet är *100* (sekunder).

* **Antal poolstorlekar för uppdatering**

   Antal samtidiga trådar som används för att räkna uppdatering. Standardvärdet är *10*.

* **Inkorgsbana**

   (*Obligatoriskt*) Sökvägen i förhållande till användarens nod (/home/users/*användarnamn*) som ska användas för mappen `inbox`. Sökvägen får INTE avslutas med ett avslutande snedstreck (/). Standardvärdet är */mail/inbox*.

* **Sökväg för skickade objekt**

   (*Obligatoriskt*) Sökvägen i förhållande till användarens nod (/home/users/*användarnamn*) som ska användas för mappen `sent items`. Sökvägen får INTE avslutas med ett avslutande snedstreck (/). Standardvärdet är */mail/sentitems*.

* **Supportbilagor**

   Om det här alternativet är markerat kan användare lägga till bilagor i sina meddelanden. Standardvärdet är *checked*.

* **Aktivera gruppmeddelanden**

   Om det här alternativet är markerat kan registrerade användare skicka massmeddelanden till en grupp medlemmar. Standardvärdet är *avmarkerat*.

* **Högsta antal av totalt antal mottagare**

   Om gruppmeddelanden är aktiverat anger du det högsta antal mottagare som gruppmeddelanden kan skickas till åt gången. Standardvärdet är *100*.

* **Batchstorlek**

   Antal meddelanden som ska grupperas tillsammans för en sändning när den skickas till en stor grupp mottagare. Standardvärdet är *100*.

* **Sammanlagd storlek för bifogade filer**

   Om supportAttachments är markerat anger det här värdet den största tillåtna totala storleken (i byte) för alla bilagor. Standardvärdet är *104857600* (100 MB).

* **Bilagetyp blockeringslista**

   En blockeringslista med filnamnstillägg, prefix med **.**&#39;, som kommer att refuseras av systemet. Om tillägget inte blocklist tillåts det. Tillägg kan läggas till eller tas bort med ikonerna **+** och **-**.

* **Tillåtna bilagetyper**

   **(*Åtgärd krävs*)** En tillåtelselista med filnamnstillägg, motsatsen till blockeringslista. Om du vill tillåta alla filnamnstillägg, förutom de som blocklist, använder du ikonen **-** för att ta bort den tomma posten.

* **Tjänstväljare**

   (*Obligatorisk*) En absolut sökväg (slutpunkt) genom vilken tjänsten anropas (en virtuell resurs). Roten för den valda sökvägen måste finnas med i konfigurationsinställningen *Körningssökvägar* för OSGi config [ `Apache Sling Servlet/Script Resolver and Error Handler`](https://localhost:4502/system/console/configMgr/org.apache.sling.servlets.resolver.SlingServletResolver), till exempel `/bin/`, `/apps/` och `/services/`. Om du vill välja den här konfigurationen för en webbplats meddelandefunktion anges den här slutpunkten som **`Service selector`**-värde för `Message List and Compose Message components` (se [Meddelandefunktion](/help/communities/configure-messaging.md)).

   Standardvärdet är */bin/messaging*.

* **Tillåtelselista i fält**

   Använd **Meddelandefält Tillåtelselista**.

>[!CAUTION]
>
>Varje gång en `Messaging Operations Service`-konfiguration öppnas för redigering, om `allowedAttachmentTypes.name` har tagits bort, läggs en tom post till så att egenskapen kan konfigureras. En enda tom post inaktiverar effektivt bifogade filer.
>
>Om du vill tillåta alla filnamnstillägg, förutom de som blocklist, använder du ikonen **-** för att (igen) ta bort den tomma posten innan du klickar på **Spara**.

## Gruppmeddelanden {#group-messaging}

Om du vill tillåta registrerade användare att skicka direktmeddelanden i grupp till användargrupper, ska du **Aktivera gruppmeddelanden** i följande två instanser av **Messaging Operation Services**-konfigurationen:

* `com.adobe.cq.social.messaging.client.endpoints.impl.MessagingOperationsServiceImpl~social-console`
* `com.adobe.cq.social.messaging.client.endpoints.impl.MessagingOperationsServiceImpl~social-messaging`

**Tjänsten Meddelandeåtgärder: social konsol**

![social-console-op-service](assets/social-console-op-service.png)

**Tjänsten Meddelandeåtgärder: sociala meddelanden**

![social-message-op-service](assets/social-message-op-service.png)

## Felsökning {#troubleshooting}

Ett sätt att felsöka problem är att aktivera [felsökningsmeddelanden i loggen.](/help/sites-administering/troubleshooting.md)

Se även [Loggare and Writers for Individual Services](/help/sites-deploying/configure-logging.md#loggers-and-writers-for-individual-services).

Paketet som ska övervakas är `com.adobe.cq.social.messaging`.
