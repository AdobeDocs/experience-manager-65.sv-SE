---
title: Konfigurerar e-postmeddelande
seo-title: Konfigurerar e-postmeddelande
description: Lär dig hur du konfigurerar e-postmeddelanden i AEM.
seo-description: Lär dig hur du konfigurerar e-postmeddelanden i AEM.
uuid: 6cbdc312-860b-4a69-8bbe-2feb32204a27
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 6466d7b8-e308-43c5-acdc-dec15f796f64
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Konfigurerar e-postmeddelande{#configuring-email-notification}

AEM skickar e-postmeddelanden till användare som:

* Prenumerera på sidhändelser, t.ex. ändring eller replikering. I avsnittet [Meddelandeinkorgen](/help/sites-classic-ui-authoring/author-env-inbox.md#subscribing-to-notifications) beskrivs hur du prenumererar på sådana händelser.

* Prenumerera på forumevent.
* Måste utföra ett steg i ett arbetsflöde. Avsnittet [Deltagarsteg](/help/sites-developing/workflows-step-ref.md#participant-step) beskriver hur du aktiverar e-postmeddelanden i ett arbetsflöde.

Krav:

* Användaren/användarna måste ha en giltig e-postadress definierad i profilen.
* CQ Mail-tjänsten **för** dag måste vara korrekt konfigurerad.

När en användare meddelas får han eller hon ett e-postmeddelande på det språk som definieras i hans profil. Varje språk har en egen mall som kan anpassas. Nya e-postmallar kan läggas till för nya språk.

>[!NOTE]
>
>När du arbetar med AEM finns det flera metoder för att hantera konfigurationsinställningarna för sådana tjänster. Mer information och rekommendationer finns i [Konfigurera OSGi](/help/sites-deploying/configuring-osgi.md) .

## Konfigurera e-posttjänsten {#configuring-the-mail-service}

För att AEM ska kunna skicka e-postmeddelanden måste **Day CQ Mail Service** konfigureras korrekt. Du kan visa konfigurationen i webbkonsolen. När du arbetar med AEM finns det flera metoder för att hantera konfigurationsinställningarna för sådana tjänster. Mer information och rekommendationer finns i [Konfigurera OSGi](/help/sites-deploying/configuring-osgi.md) .

Följande begränsningar gäller:

* SMTP- **serverporten** måste vara 25 eller senare.

* Värdnamnet **för** SMTP-servern får inte vara tomt.
* Från- **adressen** får inte vara tom.

Du kan felsöka ett problem med **Day CQ Mail Service** genom att titta på tjänstens loggar:

`com.day.cq.mailer.DefaultMailService`

Konfigurationen ser ut så här i webbkonsolen:

![chlimage_1-276](assets/chlimage_1-276.png)

## Konfigurera e-postmeddelandekanalen {#configuring-the-email-notification-channel}

När du prenumererar på en sida eller ett forum-händelsemeddelanden anges e-postadressen som `no-reply@acme.com` standard. Du kan ändra det här värdet genom att konfigurera **tjänsten för e-postkanal** för meddelanden i webbkonsolen.

Om du vill konfigurera från-e-postadressen lägger du till en `sling:OsgiConfig` nod i databasen. Använd följande procedur för att lägga till noden direkt med CRXDE Lite:

1. I CRXDE Lite lägger du till en mapp med namnet `config` under programmappen.
1. Lägg till en nod med namnet:

   `com.day.cq.wcm.notification.email.impl.EmailChannel` av typen `sling:OsgiConfig`

1. Lägg till en `String` egenskap i noden] med namnet `email.from`. Ange den e-postadress som du vill använda som värde.

1. Klicka på **Spara alla**.

Använd följande procedur för att definiera noden i innehållspaketets källmappar:

1. Skapa `jcr_root/apps/*app_name*/config folder`en fil med namnet `com.day.cq.wcm.notification.email.impl.EmailChannel.xml`

1. Lägg till följande XML för att representera noden:

   `<?xml version="1.0" encoding="UTF-8"?> <jcr:root xmlns:sling="https://sling.apache.org/jcr/sling/1.0" xmlns:jcr="https://www.jcp.org/jcr/1.0" jcr:primaryType="sling:OsgiConfig" email.from="name@server.com"/>`
1. Ersätt värdet för `email.from` attributet ( `name@server.com`) med din e-postadress.

1. Spara filen.

## Konfigurera e-postmeddelandetjänsten för arbetsflöde {#configuring-the-workflow-email-notification-service}

När du får e-postmeddelanden om arbetsflöden anges standardvärden för både from-email-adressen och värd-URL-prefixet. Du kan ändra de här värdena genom att konfigurera e-postmeddelandetjänsten **för CQ-arbetsflödet** Dag i webbkonsolen. Om du gör det bör du behålla ändringen i databasen.

Standardkonfigurationen ser ut så här i webbkonsolen:

![chlimage_1-277](assets/chlimage_1-277.png)

### E-postmallar för sidmeddelanden {#email-templates-for-page-notification}

E-postmallar för sidmeddelanden finns nedan:

`/etc/notification/email/default/com.day.cq.wcm.core.page`

Standardmallen för engelska ( `en.txt`) definieras så här:

```xml
subject=[CQ Page Event Notification]: Page Event

header=-------------------------------------------------------------------------------------\n \
Time: ${time}\n \
User: ${userFullName} (${userId})\n \
-------------------------------------------------------------------------------------\n\n

message=The following pages were affected by the event: \n \
 \n \
${modifications} \n \
 \n\n
footer=\n \
-------------------------------------------------------------------------------------\n \
This is an automatically generated message. Please do not reply.
```

#### Anpassa e-postmallar för sidmeddelanden {#customizing-email-templates-for-page-notification}

Så här anpassar du den engelska e-postmallen för sidmeddelanden:

1. Öppna filen i CRXDE:

   `/etc/notification/email/default/com.day.cq.wcm.core.page/en.txt`

1. Ändra filen efter dina behov.
1. Spara ändringarna.

Mallen måste ha följande format:

```
 subject=<text_1>
 header=<text_2>
 message=<text_3>
 footer=<text_4>
```

Där &lt;text_x> kan vara en blandning av statisk text och dynamiska strängvariabler. Följande variabler kan användas i e-postmallen för sidmeddelanden:

* `${time}`, händelsens datum och tid.

* `${userFullName}`, det fullständiga namnet på den användare som utlöste händelsen.

* `${userId}`, ID:t för den användare som utlöste händelsen.
* `${modifications}`, beskriver sidhändelsens typ och sidsökvägen i formatet:

   &lt;page event type> => &lt;page path>

   Exempel:

   PageModified => /content/geometrixx/en/products

### E-postmallar för forummeddelanden {#email-templates-for-forum-notification}

E-postmallar för forummeddelanden finns under:

`/etc/notification/email/default/com.day.cq.collab.forum`

Standardmallen för engelska ( `en.txt`) definieras så här:

```xml
subject=[CQ Forum Notification]

header=-------------------------------------------------------------------------------------\n \
Time: Time: ${time}\n \
Forum Page Path: ${forum.path}\n \
-------------------------------------------------------------------------------------\n\n

message=Page: ${host.prefix}${forum.path}.html\n

footer=\n \
-------------------------------------------------------------------------------------\n \
This is an automatically generated message. Please do not reply.
```

#### Anpassa e-postmallar för forummeddelanden {#customizing-email-templates-for-forum-notification}

Så här anpassar du den engelska e-postmallen för forummeddelanden:

1. Öppna filen i CRXDE:

   `/etc/notification/email/default/com.day.cq.collab.forum/en.txt`

1. Ändra filen efter dina behov.
1. Spara ändringarna.

Mallen måste ha följande format:

```
 subject=<text_1>
 header=<text_2>
 message=<text_3>
 footer=<text_4>
```

Var `<text_x>` kan vara en blandning av statisk text och dynamiska strängvariabler.

Följande variabler kan användas i e-postmallen för forummeddelanden:

* `${time}`, händelsens datum och tid.

* `${forum.path}`, vägen till forumsidan.

### E-postmallar för arbetsflödesmeddelanden {#email-templates-for-workflow-notification}

E-postmallen för arbetsflödesmeddelanden (engelska) finns på:

`/etc/workflow/notification/email/default/en.txt`

Den definieras enligt följande:

```xml
subject=Workflow notification: ${event.EventType}

header=-------------------------------------------------------------------------------------\n \
Time: ${event.TimeStamp}\n \
Step: ${item.node.title}\n \
User: ${participant.name} (${participant.id})\n \
Workflow: ${model.title}\n \
-------------------------------------------------------------------------------------\n\n

message=Content: ${host.prefix}${payload.path.open}\n

footer=\n \
-------------------------------------------------------------------------------------\n \
View the overview in your ${host.prefix}/aem/inbox\n \
-------------------------------------------------------------------------------------\n \
This is an automatically generated message. Please do not reply.
```

#### Anpassa e-postmallar för arbetsflödesmeddelanden {#customizing-email-templates-for-workflow-notification}

Så här anpassar du den engelska e-postmallen för meddelanden om arbetsflödeshändelser:

1. Öppna filen i CRXDE:

   `/etc/workflow/notification/email/default/en.txt`

1. Ändra filen efter dina behov.
1. Spara ändringarna.

Mallen måste ha följande format:

```
subject=<text_1>
 header=<text_2>
 message=<text_3>
 footer=<text_4>
```

>[!NOTE]
>
>Var `<text_x>` kan vara en blandning av statisk text och dynamiska strängvariabler. Varje rad i ett `<text_x>` objekt måste avslutas med ett omvänt snedstreck ( `\`), utom för den sista förekomsten, när frånvaron av omvänt snedstreck anger slutet på `<text_x>` strängvariabeln.
>
>Mer information om mallformatet finns i [javadocs i metoden Properties.load()](https://docs.oracle.com/javase/8/docs/api/java/util/Properties.html#load-java.io.InputStream-) .

Metoden `${payload.path.open}` visar sökvägen till arbetsobjektets nyttolast. För en sida i Sites `payload.path.open` liknar det till exempel `/bin/wcmcommand?cmd=open&path=…`.; detta är utan servernamnet, vilket är orsaken till att mallen lägger till det med `${host.prefix}`.

Följande variabler kan användas i e-postmallen:

* `${event.EventType}`, händelsens typ
* `${event.TimeStamp}`, datum och tid för händelsen
* `${event.User}`, den användare som utlöste händelsen
* `${initiator.home}`, initierarnodens sökväg

* `${initiator.name}`, initierarnamnet

* `${initiator.email}`, initierarens e-postadress
* `${item.id}`, arbetsuppgiftens ID
* `${item.node.id}`, ID för noden i arbetsflödesmodellen som är kopplad till det här arbetsobjektet
* `${item.node.title}`, arbetsuppgiftens titel
* `${participant.email}`, deltagarens e-postadress
* `${participant.name}`, deltagarens namn
* `${participant.familyName}`, deltagarens familjenamn
* `${participant.id}`, deltagarens id
* `${participant.language}`, deltagarspråket
* `${instance.id}`, arbetsflödes-ID
* `${instance.state}`, arbetsflödets status
* `${model.title}`, arbetsflödesmodellens titel
* `${model.id}`, ID:t för arbetsflödesmodellen

* `${model.version}`, arbetsflödesmodellens version
* `${payload.data}`, nyttolasten

* `${payload.type}`, nyttolasttypen
* `${payload.path}`, nyttolastens sökväg
* `${host.prefix}`, värdprefix, t.ex.: http://localhost:4502

### Lägga till en e-postmall för ett nytt språk {#adding-an-email-template-for-a-new-language}

Så här lägger du till en mall för ett nytt språk:

1. Lägg till en fil `<language-code>.txt` nedan i CRXDE:

   * `/etc/notification/email/default/com.day.cq.wcm.core.page` : för sidmeddelanden
   * `/etc/notification/email/default/com.day.cq.collab.forum` : för forummeddelanden
   * `/etc/workflow/notification/email/default` : för arbetsflödesmeddelanden

1. Anpassa filen till språket.
1. Spara ändringarna.

>[!NOTE]
>
>Det `<language-code>` som används som filnamn för e-postmallen måste vara en språkkod med två bokstäver och gemener som känns igen av AEM. För språkkoder använder AEM ISO-639-1.

## Konfigurera e-postmeddelanden för AEM Resurser {#assetsconfig}

När samlingar i AEM Resurser delas eller inte delas kan användarna få e-postmeddelanden från AEM. Följ de här stegen för att konfigurera e-postmeddelanden.

1. Konfigurera e-posttjänsten enligt beskrivningen ovan i [Konfigurera e-posttjänsten](/help/sites-administering/notification.md#configuring-the-mail-service).
1. Logga in på AEM som administratör. Klicka på **Verktyg** > **Åtgärder** > **Webbkonsol** för att öppna Konfiguration för webbkonsol.
1. Redigera **dagars CQ DAM Resource Collection-server**. Välj **Skicka e-post**. Click **Save**.

