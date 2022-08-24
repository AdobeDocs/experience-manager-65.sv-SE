---
title: Push-meddelanden
seo-title: Push Notifications
description: Följ den här sidan om du vill veta mer om hur du använder push-meddelanden i en AEM Mobile-app.
seo-description: Follow this page to learn about how to use push notifications in an AEM Mobile app.
uuid: 0ed8b183-ef81-487f-8f35-934d74ec82af
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: ed8c51d2-5aac-4fe8-89e8-c175d4ea1374
exl-id: 375f2f40-1b98-4e21-adee-cbea274e6a2a
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '3273'
ht-degree: 0%

---

# Push-meddelanden{#push-notifications}

>[!NOTE]
>
>Adobe rekommenderar att du använder SPA Editor för projekt som kräver ramverksbaserad klientåtergivning för en sida (t.ex. Reagera). [Läs mer](/help/sites-developing/spa-overview.md).

Att omedelbart kunna informera användare av AEM Mobile-appar med viktiga meddelanden är avgörande för värdet av en mobilapp och dess marknadsföringskampanjer. Här beskrivs de steg som måste vidtas för att din app ska kunna ta emot push-meddelanden och hur du konfigurerar och skickar push-meddelanden från AEM Mobile till appen som är installerad på telefonen. I det här avsnittet beskrivs dessutom hur du konfigurerar [Djuplänkning](#deeplinking) till dina push-meddelanden.

>[!NOTE]
>
>*Push-meddelanden garanteras inte. de är mer som meddelanden. Det bästa görs att se till att alla får dem, men de är inte en garanterad leveransmekanism. Tiden för att skicka en push-funktion kan variera från mindre än en sekund till upp till en halvtimme.*

Om du vill använda push-meddelanden med AEM måste du använda olika tekniker. Först måste en leverantör av push-meddelandetjänster användas för att hantera meddelanden och enheter (AEM gör inte detta ännu). Två leverantörer är färdiga att konfigureras med AEM: [Amazon Simple Notification Service](https://aws.amazon.com/sns/) (eller SNS), och [Pushwoosh](https://www.pushwoosh.com/). För det andra måste push-tekniken för det angivna mobiloperativsystemet gå via lämplig tjänst - Apple Push Notification Service (eller APNS) för iOS-enheter. och Google Cloud Messaging (eller GCM) för Android-enheter. Även om AEM inte kommunicerar direkt med dessa plattformsspecifika tjänster måste viss relaterad konfigurationsinformation tillhandahållas av AEM tillsammans med meddelandena för att dessa tjänster ska kunna utföra push-åtgärden.

Så här fungerar den när den har installerats och konfigurerats (se nedan):

1. Ett push-meddelande skapas i AEM och skickas till tjänstleverantören (Amazon SNS eller Pushwoosh).
1. Tjänsteleverantören tar emot den och skickar den till huvudleverantören (APNS eller GCM).
1. Kärnleverantören skickar meddelandet till alla enheter som registrerats för den push-åtgärden. För varje enhet används mobildatanätverket eller WiFi, beroende på vilket som är tillgängligt på enheten.
1. Meddelandet visas på enheten om appen som det är registrerat för inte körs. En användare som trycker på meddelandet startar programmet och visar meddelandet i programmet. Om programmet redan körs visas bara meddelandet i appen.

Den här versionen av AEM har stöd för iOS och Android-mobilenheter.

## Översikt och procedur {#overview-and-procedure}

Om du vill använda push-meddelanden i en AEM Mobile-app måste du utföra följande åtgärder på hög nivå.

En AEM utvecklare brukar:

1. Registrera dig hos Apple och Google meddelandetjänster
1. Registrera dig hos en push-meddelandetjänst och konfigurera den
1. Lägg till push-stöd i appen
1. Förbered en telefon för testning

Medan en AEM gör det:

1. Konfigurera push-AEM
1. Bygg och distribuera appen
1. Skicka ett push-meddelande
1. Konfigurera djuplänkning *(valfritt)*

### Steg 1: Registrera dig hos Apple och Google meddelandetjänster {#step-register-with-apple-and-google-messaging-services}

#### Använda Apple Push Notification Service (APNS) {#using-the-apple-push-notification-service-apns}

Gå till Apple [här](https://developer.apple.com/library/ios/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/Chapters/ApplePushService.html) för att bekanta sig med Apple Push Notification Service.

För att använda APNS behöver du en **Certifikat** -fil (en .cer-fil), en push-fil **Privat nyckel** (en P12-fil) och en **Lösenord för privat nyckel** från Apple. Instruktioner om hur du gör detta finns [här](https://developer.apple.com/library/ios/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/Chapters/ProvisioningDevelopment.html).

#### Använda tjänsten Google Cloud Messaging (GCM) {#using-the-google-cloud-messaging-gcm-service}

>[!NOTE]
>
>Google ersätter GCM med en liknande tjänst som kallas Firebase Cloud Messaging (FCM). Mer information om FCM finns i [här](https://developers.google.com/cloud-messaging/faq).

Gå till Google [här](https://developer.android.com/google/gcm/index.html) för att lära känna Google Cloud Messaging för Android.

Du måste följa stegen [här](https://developer.android.com/google/gcm/gs.html) till **Skapa ett Google API-projekt**, **Aktivera GCM-tjänsten** och **Hämta en API-nyckel**. Du behöver **API-nyckel** för att skicka push-meddelanden till Android-enheter. Du kan även spela in **Projektnummer**, som ibland kallas **GCM-avsändar-ID**.

I följande steg visas ett annat sätt att skapa GCM API-nycklar:

1. Logga in på Google och gå till [Google Developer page](https://developers.google.com/mobile/add?platform=android&amp;cntapi=gcm).
1. Välj din app i listan (eller skapa en ny).
1. Ange ditt program-ID under Android-paketnamn, dvs. `com.adobe.cq.mobile.weretail.outdoorsapp`. (Om det inte fungerar kan du försöka igen med &quot;test.test&quot;.)
1. Klicka **Fortsätt att välja och konfigurera tjänster**
1. Välj Cloud Messaging och klicka sedan på **Aktivera Google Cloud Messaging**.
1. Den nya API-nyckeln för servern och (ny eller befintlig) avsändar-ID visas.

>[!NOTE]
>
>Registrera Server-API-nyckeln. Detta värde anges på din push-leverantörs webbplats.

### Steg 2: Registrera och konfigurera en push-meddelandetjänst {#step-register-and-configure-a-push-messaging-service}

AEM är konfigurerad att använda en av tre tjänster för push-meddelanden:

* Amazon SNS
* Pushwoosh
* Adobe Mobile Services

*Amazon SNS* och *Pushwoosh* konfigurationer gör att du kan skicka push-meddelanden från AEM skärmar.

*Adobe Mobile Services* Med kan du konfigurera och skicka push-meddelanden från Adobe Mobile Services med ett Adobe Analytics-konto (men appen måste skapas med den här konfigurationsuppsättningen för att AMS-push-meddelanden ska kunna aktiveras).

#### Använda meddelandetjänsten Amazon SNS {#using-the-amazon-sns-messaging-service}

>[!NOTE]
>
>*Information om Amazon SNS, och en länk för att skapa ett nytt AWS-konto, finns [här](https://aws.amazon.com/sns/). Du kan få ett kostnadsfritt konto i ett år.*

Om du inte vill använda Amazon SNS kan du hoppa över dessa steg.

Så här konfigurerar du Amazon SNS för push-meddelanden:

1. **Registrera dig hos Amazon SNS**

   1. Registrera ditt konto-ID. Formatet ska vara tolv siffror utan blanksteg eller streck, dvs. &quot;123456789012&quot;.
   1. Se till att du befinner dig i regionen&quot;us-East&quot; eller&quot;eu&quot;, vilket kräver ett av dessa steg i ett senare steg (Skapa identitetspool).
   1. När du har registrerat dig loggar du in på hanteringskonsolen och väljer [SNS](https://console.aws.amazon.com/sns/) (Push Notification Service). Klicka på&quot;Kom igång&quot; om det visas.

1. **Skapa åtkomstnyckel och ID**

   1. Klicka på ditt inloggningsnamn i skärmens övre högra hörn och välj Säkerhetsuppgifter på menyn.
   1. Klicka på Åtkomsttangenter och klicka i utrymmet nedan **Skapa ny åtkomstnyckel**.
   1. Klicka **Visa åtkomstnyckel** och kopiera och spara ID:t för åtkomstnyckeln och den hemliga åtkomstnyckeln som visas. Om du väljer att hämta nycklarna får du en CSV-fil som innehåller samma värden.
   1. Andra säkerhetsrelaterade certifikat, och andra, kan hanteras på den här sidan.

   >[!NOTE]
   >
   >En åtkomstnyckel kan användas för flera appar.

   För organisationer som använder ett&quot;AWS Sandbox&quot;-konto är stegen mycket lika och beskrivs här:

   1. Klicka på ditt inloggningsnamn längst upp till höger på skärmen och välj Mina inloggningsuppgifter på menyn.
   1. Klicka på Användare i den vänstra listan med åtgärder och välj ditt användarnamn.
   1. Klicka på fliken Säkerhetsuppgifter.
   1. Här ser du dina nycklar och skapar nya nycklar. Spara knapparna för senare bruk.


1. **Skapa ett ämne**

   1. Klicka **Skapa ämne** och välj ett ämnesnamn. Spela in alla fält, t.ex. Ämnesnamn, Ämnesägare, Region och Visningsnamn.
   1. Klicka **Övriga ämnesåtgärder** > **Redigera ämnesprofil**. Under **Tillåt dessa användare att prenumerera på det här avsnittet**, markera **Alla.**
   1. Klicka **Uppdatera princip**.

   >[!NOTE]
   >
   >Du kan skapa flera ämnen för olika scenarier, t.ex. dev, test, demo och så vidare. Resten av SNS-konfigurationen kan vara densamma. Bygg appen med olika ämnen; push-meddelanden som skickas till det ämnet tas endast emot av appen som skapats med det ämnet.

1. **Skapa plattformsprogram**

   1. Klicka på Program och sedan på Skapa plattformsprogram. Välj ett namn och välj en plattform (APNS för iOS, GCM för Android). Beroende på vilken plattform som används måste andra fält fyllas i:

      1. För APNS måste en P12-fil, ett lösenord, ett certifikat och en privat nyckel anges. Dessa skulle ha erhållits i steget *Använda Apple Push Notification Service (APNS)* ovan.
      1. För GCM måste en API-nyckel anges. Detta borde ha erhållits i steget *Använda tjänsten Google Cloud Messaging (GCM)* ovan.
   1. Upprepa ovanstående steg en gång för varje plattform som du kommer att stödja. Om du vill kunna skicka till både iOS och Android måste du skapa två plattformsprogram.


1. **Skapa en identitetspool**

   1. Använd [Cognito](https://console.aws.amazon.com/cognito) om du vill skapa en identitetspool som lagrar grundläggande data för oautentiserade användare. Observera att endast områdena&quot;us-east&quot; och&quot;eu&quot; för närvarande stöds av Amazon Cognito.
   1. Ge den ett namn och markera kryssrutan &quot;Aktivera åtkomst till oautentiserade identiteter&quot;.
   1. På nästa sida (&quot;*Dina Cognito-identiteter kräver åtkomst till dina resurser*&quot;) klicka på Tillåt.
   1. Klicka på länken längst upp till höger på sidan *Redigera identitetspool&quot;*. Identitetspoolens ID visas. Spara den här texten till senare.
   1. På samma sida väljer du listrutan bredvid Oautentiserad roll och ser till att den har rollen Cognito_&lt;pool name=&quot;&quot;>UnauthRole har valts. Spara ändringarna.

1. **Konfigurera åtkomst**

   1. Logga in på [Hantering av identitet och åtkomst](https://console.aws.amazon.com/iam/home) (IAM)
   1. Välj roller
   1. Klicka på rollen som skapades i föregående steg, som kallas Cognito_&lt;youridentitypoolname>Unauth_Role. Spela in&quot;Roll-ARN&quot; som visas.
   1. Öppna Inline Policies om det inte redan är öppet. Du bör se en princip där med ett namn som oneClick_Cognito_&lt;youridentitypoolname>Unauth_Role_1234567890123.
   1. Klicka på Redigera profil. Ersätt innehållet i policydokumentet med det här JSON-fragmentet:

   <table>
    <tbody>
     <tr>
     <td><p> </p> <p>{</p> <p> "Version": "2012-10-17",</p> <p> "Programsats": [</p> <p> {</p> <p> "Åtgärd": [</p> <p> "mobileanalytics:PutEvents",</p> <p> "cognito-sync:*",</p> <p> "SNS:CreatePlatformEndpoint",</p> <p> "SNS:Subscribe"</p> <p> ],</p> <p> "Effekt": "Tillåt",</p> <p> "Resurs": [</p> <p> "*"</p> <p> ]</p> <p> }</p> <p> ]</p> <p>}</p> <p> </p> </td>
     </tr>
    </tbody>
    </table>

   1. Klicka på **Använd princip**


#### Använda meddelandetjänsten Pushwoosh {#using-the-pushwoosh-messaging-service}

Om du inte vill använda Pushwoosh kan du hoppa över det här steget.

Så här använder du Pushwoosh:

1. **Registrera dig hos Pushwoosh**

   1. Gå till pushwoosh.com och skapa ett nytt konto.

1. **Skapa en API-åtkomsttoken**

   1. På Pushwoosh-webbplatsen går du till menyalternativet API Access för att generera en API Access-token. Du måste registrera detta säkert.

1. **Skapa en ny app**

   1. För Android-stöd måste du ange GCM API-nyckeln.
   1. När du konfigurerar programmet väljer du Cordova som ramverk.
   1. För iOS support måste du ange certifikatfilen (.cer), push-certifikatet (.p12) och lösenordet för den privata nyckeln. dessa bör ha hämtats från Apple APNS webbplats. Välj Cordova under Framework.
   1. Pushwoosh genererar ett app-ID för den appen, i formatet&quot;XXXXX-XXXXX&quot;, där varje X är ett hexadecimalt värde (0 till F).

>[!NOTE]
>
>*Om en andra app har konfigurerats i AEM med samma app-ID (och andra relaterade värden): API Access Token och GCM-ID), alla push-meddelanden som skickas via den andra appen på AEM, kommer att skickas till andra appar med det app-ID:t.*

### Steg 3: Lägg till push-stöd i appen {#step-add-push-support-to-the-app}

#### Lägg till ContentSync-konfiguration {#add-contentsync-configuration}

Skapa två innehållsnoder (en i app-config och en i app-config-dev) som kallas notificationConfig:

* /content/`<your app>`/shell/jcr:content/page-app/app-config-dev/notificationsConfig
* /content/`<your app>`/shell/jcr:content/page-app/app-config/notificationsConfig

Med dessa egenskaper (.content.xml-filer):
&lt;jcr:root xmlns:jcr=&quot; &lt;span id=&quot; translate=&quot;no&quot; />https://www.jcp.org/jcr/1.0](https://www.jcp.org/jcr/1.0)&quot; xmlns:nt=&quot; [https://www.jcp.org/jcr/nt/1.0](https://www.jcp.org/jcr/nt/1.0)&quot; jcr:primaryType=&quot;nt:unStructed&quot; excludeProperties=&quot;[appAPIAccessToken]&quot; path=&quot;../../../...&quot;
[
targetRootDirectory=&quot;www&quot; type=&quot;notificationsconfig&quot;/>

>[!NOTE]
>
>Hanteraren för innehållssynkronisering söker efter dessa noder, och om de inte finns där skrivs inte filen page-notifications-config.json ut.

#### Lägg till klientbibliotek {#add-client-libraries}

Klientbiblioteken för push-meddelanden måste läggas till i programmet genom att följa dessa steg:

I CRXDE Lite:

1. Navigera till */etc/designs/phonegap/&lt;app name=&quot;&quot;>/clientlibsall.*
1. Dubbelklicka på inbäddningsavsnittet i egenskapsrutan.
1. I dialogrutan som visas lägger du till ett nytt klientlib genom att klicka på plusknappen (+).
1. Lägg till&quot;cq.mobile.push&quot; i det nya textfältet och klicka på OK.
1. Lägg till ytterligare en så kallad cq.mobile.push.amazon och klicka på OK.
1. Spara ändringarna.

>[!NOTE]
>
>Om push-meddelanden tas bort, eller inte används, av utrymmesskäl i appen och för att undvika konsolfelmeddelanden, tar du bort dessa klientlibs från appen.

### Steg 4: Förbered en telefon för testning {#step-prepare-a-phone-for-testing}

>[!NOTE]
>
>*För push-meddelanden måste du testa på en faktisk enhet eftersom emulatorer inte kan ta emot push-meddelanden.*

#### iOS {#ios}

För iOS måste du använda en Mac OS-dator och du måste gå med i [iOS Developer Program](https://developer.apple.com/programs/ios/). Vissa företag har företagslicenser som kan vara tillgängliga för alla utvecklare.

I XCode 8.1 måste du gå till fliken Funktioner i projektet innan du använder push-meddelanden och växla mellan att aktivera push-meddelanden.

#### Android {#android}

Så här installerar du appen på en Android-telefon med CLI (se nedan: **Steg 6 - Bygg och distribuera appen**) måste du först ställa telefonen i&quot;utvecklarläge&quot;. Se [Aktivera alternativ för utvecklare på enheter](https://developer.android.com/tools/device.html#developer-device-options) om du vill ha mer information om hur du gör detta.

### Steg 5: Konfigurera push-AEM {#step-configure-push-on-aem-apps}

Innan du skapar och distribuerar till din konfigurerade mobila enhet måste du konfigurera meddelandeinställningarna för den meddelandetjänst som du valde att använda.

1. Skapa lämpliga auktoriseringsgrupper för push-meddelanden.
1. Logga in AEM lämplig användare och klicka på fliken Appar.
1. Klicka på appen.
1. Hitta rutan Hantera Cloud Services och klicka på pennan för att ändra dina molnkonfigurationer.
1. Välj Amazon SNS Connection, Pushwoosh Connection eller Adobe Mobile Services som meddelandekonfiguration.
1. Ange leverantörsegenskaperna och klicka på Skicka för att spara dem och Klar. De kontrolleras inte på fjärrbasis i detta skede, utom när det gäller AMS.
1. Du bör nu se konfigurationen som du just angav på panelen Hantera Cloud Services.

### Steg 6: Bygg och distribuera appen {#step-build-and-deploy-the-app}

**Obs!** Se även våra instruktioner [här](/help/mobile/building-app-mobile-phonegap.md) om att bygga PhoneGap-program.

Det finns två sätt att skapa och distribuera din app med PhoneGap.

**Obs!** För testning av push-meddelanden räcker det inte med emulatorer eftersom push-meddelanden använder ett distinkt protokoll mellan push-providern (Apple eller Google) och enheten. Den aktuella maskinvaran och emulatorerna för Mac/PC stöder inte detta.

1. *PhoneGap Build* är en tjänst som erbjuds av PhoneGap som skapar din app åt dig på deras servrar och gör att du kan hämta den direkt till din enhet. Se [PhoneGap Build](https://build.phonegap.com/) för att lära dig hur du konfigurerar och använder PhoneGap Build.

1. *Kommandoradsgränssnitt för PhoneGap* (CLI) kan du använda en mängd PhoneGap-kommandon på kommandoraden för att skapa, felsöka och distribuera din app. Se [Dokumentation för PhoneGap-utvecklare](https://docs.phonegap.com/en/edge/guide_cli_index.md.html#The%20Command-Line%20Interface) för att lära dig hur du konfigurerar och använder PhoneGap CLI.

### Steg 7: Skicka ett push-meddelande {#step-send-a-push-notification}

Följ de här stegen för att skapa ett nytt meddelande och skicka det.

1. Skapa ett nytt meddelande

   * På AEM Mobile-appens kontrollpanel hittar du panelen Push Notifications (Push-meddelanden).
   * Välj &quot;Skapa&quot; på menyn uppe till höger. Observera att den här knappen inte är tillgänglig förrän molnkonfigurationen har ställts in.
   * I guiden Skapa meddelande anger du en titel och ett meddelande och klickar sedan på knappen&quot;Skapa&quot;. Meddelandet är nu klart att skickas omedelbart eller senare. Den kan redigeras och du kan ändra och spara meddelandet och/eller titeln.

1. Skicka meddelandet

   * Leta reda på panelen Push Notifications (Push-meddelanden) på panelen Apps.
   * Markera meddelandet eller klicka på informationsknappen längst ned till höger (. . .) för att visa listan med meddelanden. Den här listan anger också om ett meddelande är klart att skickas, om det redan har skickats eller om ett fel uppstod när meddelandet skickades.
   * Markera kryssrutan för ett meddelande (endast) och klicka på knappen&quot;Skicka meddelande&quot; ovanför listan. Du kan välja att&quot;avbryta&quot; eller&quot;skicka&quot; meddelandet i den dialogruta som visas.

1. Hantera resultaten

   * Om tjänsten för push-meddelanden (Amazon SNS eller Pushwoosh) tar emot sändningsbegäran, bekräftar att den är giltig och skickar den till ANE-leverantörerna (APNS och GCM) stängs dialogrutan Skicka utan meddelande. Statusen för det meddelandet visas som Skickat i meddelandelistan.
   * Om push-sändningen misslyckas visas ett meddelande som anger problemet. I meddelandelistan anges meddelandets status som Fel, men om problemet åtgärdas kan meddelandet skickas igen. Om ett fel uppstår bör ytterligare felinformation finnas i serverfelloggen.
   * Observera att det finns vissa plattformsskillnader mellan push-meddelanden för iOS och Android. Bland dem:

      * När appen har distribuerats på Android kommer den att startas med CLI. I iOS måste du starta programmet manuellt. Eftersom push-registreringssteget inträffar vid start kan Android-appar få push-meddelanden direkt (eftersom de har startats och registrerats), medan iOS-appar inte gör det.
      * I Android är texten för knappen OK i versaler (och i alla andra knappar som läggs till i meddelandet i appen), men inte i iOS.

För AMS-push-meddelanden måste meddelanden skapas och skickas från AMS-servern. AMS har ytterligare funktioner för push-meddelanden utöver de som AEM meddelanden med AWS och Pushwoosh ger.

>[!NOTE]
>
>*Push-meddelanden garanteras inte. de är mer som meddelanden. Det bästa görs att se till att alla hör det, men de är inte en garanterad leveransmekanism. Tiden för att skicka en push-funktion kan variera från mindre än en sekund till upp till en halvtimme.*

### Konfigurera djup länkning med push-meddelanden {#configuring-deep-linking-with-push-notifications}

Vad är Djuplänkning? I samband med ett push-meddelande är det ett sätt att tillåta att en app öppnas eller dirigeras (om den är öppen) till en viss plats i programmet.

Hur fungerar det? Författaren av ett push-meddelande kan lägga till en knappetikett (d.v.s. &quot;Visa mig!&quot;) till meddelandet och väljer den sida som de vill länka i meddelandet via en visuell sökvägsläsare. När det skickas utförs push-åtgärden som vanligt förutom att knappen OK ersätts av knappen&quot;Stäng&quot; i meddelandet i appen och den nya knappen anges (&quot;Visa mig!&quot;) visas också. Om du klickar på den nya knappen kommer programmet att gå till den angivna sidan i programmet. Om du klickar på Stäng stängs meddelandet.

Om appen inte är öppen visas skuggan som vanligt. Om du utför en åtgärd på meddelandet i skuggningen öppnas appen och användaren får sedan tillgång till knapparna för djup länk baserat på vad som konfigurerats i push-meddelandet.

Skapa meddelandet, lägg till knapptext och länksökväg för den valfria länken:

>[!CAUTION]
>
>.Följ stegen nedan om du vill öppna panelen Push Notification (Push-meddelanden) på instrumentpanelen.

1. Klicka på redigeringen i det övre högra hörnet av **Hantera Cloud Services** platta.

   ![chlimage_1-108](assets/chlimage_1-108.png)

1. Välj **Pushwoosh Connection**. Klicka på **Nästa**.

   ![chlimage_1-109](assets/chlimage_1-109.png)

1. Ange information om egenskaperna och klicka på **Skicka**.

   ![chlimage_1-110](assets/chlimage_1-110.png)

   När du skickar in konfigurationen, **Push-meddelanden** visas på kontrollpanelen.

   ![chlimage_1-111](assets/chlimage_1-111.png)

### Guiden Skapa meddelande {#create-notification-wizard}

När **Push-meddelanden** visas på kontrollpanelen. Använd guiden för att skapa meddelanden för att lägga till innehållet:

1. Klicka på Lägg till-symbolen i det övre högra hörnet av **Push-meddelanden** för att öppna **Guiden Skapa meddelande**.

   ![chlimage_1-112](assets/chlimage_1-112.png)

1. Om du klickar på bläddringsikonen i länksökvägen visas programmets innehållsstruktur för användaren.

   Klicka på bockikonen när du har valt sökvägen.

   ![chlimage_1-113](assets/chlimage_1-113.png)

   >[!NOTE]
   >
   >Länkknappstexten får innehålla högst 20 tecken.
   >
   >Om slutanvändaren inte har den senaste versionen av programmet och den länkade sökvägen inte är tillgänglig kommer användaren att hamna på programmets huvudsida om åtgärden för den djupa länken bekräftas.

1. Ange **Textinformation** i **Guiden Skapa meddelande** och klicka **Skapa**.

   ![chlimage_1-114](assets/chlimage_1-114.png)

   Öppna informationen genom att klicka på det push-meddelande som du skapade från **Push-meddelanden** platta.

   Du kan redigera egenskaper, skicka meddelanden eller ta bort meddelandet.

   ![chlimage_1-115](assets/chlimage_1-115.png)

>[!NOTE]
>
>**Ytterligare information**:
>
>Pushwoosh och Amazon SNS stöds inte efter version 6.4 och kommer att vara tillgängliga som tillägg från paketresursen.

### Nästa steg {#the-next-steps}

När du har fått mer information om push-meddelanden för din app kan du läsa [AEM Mobile Content Personalization](/help/mobile/phonegap-aem-mobile-content-personalization.md).
