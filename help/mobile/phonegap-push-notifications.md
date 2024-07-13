---
title: Push-meddelanden
description: Följ den här sidan om du vill veta mer om hur du använder push-meddelanden i en Adobe Experience Manager Mobile-app.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
exl-id: 375f2f40-1b98-4e21-adee-cbea274e6a2a
solution: Experience Manager
feature: Mobile
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '3156'
ht-degree: 0%

---

# Push-meddelanden{#push-notifications}

>[!NOTE]
>
>Adobe rekommenderar att du använder SPA Editor för projekt som kräver ramverksbaserad klientåtergivning för en sida (till exempel React). [Läs mer](/help/sites-developing/spa-overview.md).

Att omedelbart kunna informera användare av Adobe Experience Manager (AEM) mobilappar om viktiga meddelanden är avgörande för värdet av en mobilapp och dess marknadsföringskampanjer. Här beskrivs de steg som måste vidtas för att din app ska kunna ta emot push-meddelanden. Du får även lära dig hur du konfigurerar och skickar push-meddelanden från AEM Mobile till appen som är installerad på telefonen. I det här avsnittet beskrivs även hur du konfigurerar funktionen [Djuplänkning](#deeplinking) till dina push-meddelanden.

>[!NOTE]
>
>*Push-meddelanden kan inte levereras. De liknar meddelanden. Det bästa görs att se till att alla får dem, men de är inte en garanterad leveransmekanism. Tiden för att leverera en push-funktion kan dessutom variera från mindre än en sekund till upp till en halvtimme.*

Om du vill använda push-meddelanden med AEM måste du använda olika tekniker. Först måste en leverantör av push-meddelandetjänster användas för att hantera meddelanden och enheter (AEM gör inte detta ännu). Två providers har konfigurerats med AEM: [Amazon Simple Notification Service](https://aws.amazon.com/sns/) (eller SNS) och [Pushwoosh](https://www.pushwoosh.com/). För det andra måste push-tekniken för det angivna mobiloperativsystemet gå via rätt tjänst - Apple Push Notification Service (eller APNS) för iOS-enheter och Google Cloud Messaging (eller GCM) för Android™-enheter. Även om AEM inte kommunicerar direkt med dessa plattformsspecifika tjänster måste viss relaterad konfigurationsinformation tillhandahållas av AEM tillsammans med meddelanden om att dessa tjänster ska utföra push-åtgärden.

Så här fungerar den när den har installerats och konfigurerats (se nedan):

1. Ett push-meddelande skapas i AEM och skickas till tjänstleverantören (Amazon SNS eller Pushwoosh).
1. Tjänsteleverantören tar emot den och skickar den till huvudleverantören (APNS eller GCM).
1. Kärnleverantören skickar meddelandet till alla enheter som registrerats för den push-åtgärden. För varje enhet används mobildatanätverket eller WiFi, beroende på vad som är tillgängligt på enheten.
1. Meddelandet visas på enheten om appen som den är registrerad för inte körs. En användare som trycker på meddelandet startar programmet och visar meddelandet i programmet. Om programmet redan körs visas bara meddelandet i appen.

Den här versionen av AEM har stöd för iOS och Android™-mobilenheter.

## Översikt och procedur {#overview-and-procedure}

Om du vill använda push-meddelanden i en AEM Mobile-app måste du utföra följande åtgärder på hög nivå.

En Experience Manager-utvecklare gör vanligtvis följande:

1. Registrera dig hos Apple och Google meddelandetjänster
1. Registrera dig hos en push-meddelandetjänst och konfigurera den
1. Lägg till push-stöd i appen
1. Förbered en telefon för testning

När en Experience Manager-administratör gör följande:

1. Konfigurera push-AEM
1. Skapa och distribuera appen
1. Skicka ett push-meddelande
1. Konfigurera djuplänkning *(valfritt)*

### Steg 1: Registrera dig hos Apple och Google meddelandetjänster {#step-register-with-apple-and-google-messaging-services}

#### Använda Apple Push Notification Service (APNS) {#using-the-apple-push-notification-service-apns}

Gå till Apple-sidan [här](https://developer.apple.com/documentation/usernotifications#//apple_ref/doc/uid/TP40008194-CH8-SW1) om du vill bekanta dig med Apple push-meddelandetjänst.

Om du vill använda APN:er måste du ha en **Certificate**-fil (en .cer-fil), en push **Private Key** (en .p12-fil) och ett **Private Key Password** från Apple. Instruktioner om hur du gör det finns [här](https://developer.apple.com/library/archive/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/).

#### Använda tjänsten Google Cloud Messaging (GCM) {#using-the-google-cloud-messaging-gcm-service}

>[!NOTE]
>
>Google ersätter GCM med en liknande tjänst som kallas Firebase Cloud Messaging (FCM). Klicka [här](https://firebase.google.com/docs/cloud-messaging/) om du vill ha mer information om FCM.

Gå till Google-sidan [här](https://developer.android.com/google/gcm/index.html) och bekanta dig med Google Cloud Messaging för Android™.

[Följ de här stegen](https://developer.android.com/google/gcm/gs.html) för att **skapa ett Google API-projekt**, **Aktivera GCM-tjänsten** och **Hämta en API-nyckel**. Du behöver **API-nyckeln** för att skicka push-meddelanden till Android™-enheter. Registrera även ditt **projektnummer**, som ibland kallas **GCM-avsändar-ID**.

I följande steg visas en annan metod för att skapa GCM API-nycklar:

1. Logga in på Google och gå till [Google Developer-sidan](https://developers.google.com/mobile/add?platform=android&amp;cntapi=gcm).
1. Välj din app i listan (eller skapa en).
1. Ange ditt program-ID under Paketnamn för Android™, det vill säga `com.adobe.cq.mobile.weretail.outdoorsapp`. (Om det inte fungerar kan du försöka igen med &quot;test.test&quot;.)
1. Klicka på **Fortsätt för att välja och konfigurera tjänster**
1. Välj Cloud Messaging och klicka sedan på **Aktivera Google Cloud Messaging**.
1. Den nya API-nyckeln för servern och (ny eller befintlig) avsändar-ID visas.

>[!NOTE]
>
>Registrera Server-API-nyckeln. Det här värdet anges på din push-leverantörs webbplats.

### Steg 2: Registrera och konfigurera en push-meddelandetjänst {#step-register-and-configure-a-push-messaging-service}

AEM är konfigurerad att använda en av tre tjänster för push-meddelanden:

* AMAZON SNS
* Pushwoosh
* Adobe Mobile Services

Med konfigurationerna *Amazon SNS* och *Pushwoosh* kan du skicka push-meddelanden från AEM skärmar.

Med konfigurationen för *Adobe Mobile Services* kan du konfigurera och skicka push-meddelanden från Adobe Mobile Services med ett Adobe Analytics-konto (men appen måste skapas med den här konfigurationsuppsättningen för att AMS-push-meddelanden ska kunna aktiveras).

#### Använda meddelandetjänsten Amazon SNS {#using-the-amazon-sns-messaging-service}

>[!NOTE]
>
>*Information om Amazon SNS och en länk för att skapa ett AWS-konto finns [här](https://aws.amazon.com/sns/). Du kan få ett kostnadsfritt konto för ett år.*

Om du inte vill använda Amazon SNS kan du hoppa över dessa steg.

Så här konfigurerar du Amazon SNS för push-meddelanden:

1. **Registrera dig hos Amazon SNS**

   1. Registrera ditt konto-ID. Formatet ska vara 12 siffror utan blanksteg eller streck, det vill säga &quot;123456789012&quot;.
   1. Se till att du befinner dig i regionen&quot;us-East&quot; eller&quot;eu&quot;, vilket kräver ett av dessa steg (Skapa identitetspool).
   1. När du har registrerat dig loggar du in på hanteringskonsolen och väljer [SNS](https://console.aws.amazon.com/sns/) (Push Notification Service). Klicka på Kom igång om det visas.

1. **Skapa åtkomstnyckel och ID**

   1. Klicka på ditt inloggningsnamn i skärmens övre högra hörn och välj Säkerhetsuppgifter på menyn.
   1. Klicka på Åtkomsttangenter och klicka på **Skapa ny åtkomstnyckel** i utrymmet nedan.
   1. Klicka på **Visa åtkomstnyckel** och kopiera och spara ID:t för åtkomstnyckel och hemlig åtkomstnyckel som visas. Om du väljer att hämta nycklarna får du en CSV-fil som innehåller samma värden.
   1. Andra säkerhetsrelaterade certifikat och andra kan hanteras på den här sidan.

   >[!NOTE]
   >
   >En åtkomstnyckel kan användas för flera appar.

   För organisationer som använder ett&quot;AWS Sandbox&quot;-konto är stegen liknande och beskrivs här:

   1. Klicka på ditt inloggningsnamn längst upp till höger på skärmen och välj Mina inloggningsuppgifter på menyn.
   1. Klicka på Användare i den vänstra listan med åtgärder och välj ditt användarnamn.
   1. Klicka på fliken Säkerhetsuppgifter.
   1. Här ser du dina nycklar och skapar nya nycklar. Spara knapparna för senare bruk.

1. **Skapa ett ämne**

   1. Klicka på **Skapa ämne** och välj ett ämnesnamn. Spela in alla fält, t.ex. Ämnesnamn, Ämnesägare, Region och Visningsnamn.
   1. Klicka på **Andra ämnesåtgärder** > **Redigera ämnesprofil**. Under **Tillåt dessa användare att prenumerera på det här ämnet** väljer du **Alla.**
   1. Klicka på **Uppdatera princip**.

   >[!NOTE]
   >
   >Du kan skapa flera ämnen för olika scenarier, till exempel dev, test och demo. Resten av SNS-konfigurationen kan vara densamma. Bygg appen med det olika ämnet. Push-meddelanden som skickas till det ämnet tas endast emot av appen som skapats med det ämnet.

1. **Skapa plattformsprogram**

   1. Klicka på Program och sedan på Skapa plattformsprogram. Välj ett namn och välj en plattform (APNS för iOS, GCM för Android™). Beroende på plattform. andra fält måste fyllas i:

      1. För APNS måste en P12-fil, ett lösenord, ett certifikat och en privat nyckel anges. Dessa bör ha hämtats i steget *Använda Apple Push Notification Service (APNS)* ovan.
      1. För GCM måste en API-nyckel anges. Detta bör ha hämtats i steget *Använda tjänsten Google Cloud Messaging (GCM)* ovan.

   1. Upprepa ovanstående steg en gång för varje plattform som du stöder. För att kunna använda både iOS och Android™ måste två plattformsprogram skapas.

1. **Skapa en identitetspool**

   1. Använd [Cognito](https://console.aws.amazon.com/cognito) för att skapa en identitetspool som lagrar grundläggande data för oautentiserade användare. Observera att endast områdena&quot;us-east&quot; och&quot;eu&quot; för närvarande stöds av Amazon Cognito.
   1. Ge den ett namn och markera kryssrutan &quot;Aktivera åtkomst till oautentiserade identiteter&quot;.
   1. På nästa sida (&quot;*Dina Cognito-identiteter kräver åtkomst till dina resurser*&quot;) klickar du på Tillåt.
   1. Klicka på länken *Redigera identitetspool* i det övre högra hörnet på sidan. Identitetspoolens ID visas. Spara den här texten till senare.
   1. På samma sida väljer du listrutan bredvid Oautentiserad roll och ser till att rollen Cognito_&lt;poolnamn>UnauthRole är vald. Spara ändringarna.

1. **Konfigurera åtkomst**

   1. Logga in på [Identity and Access Management](https://console.aws.amazon.com/iam/home) (IAM).
   1. Välj Roller.
   1. Klicka på rollen som skapades i föregående steg, med namnet Cognito_&lt;yourIdentityPoolName>Unauth_Role. Spela in&quot;Roll-ARN&quot; som visas.
   1. Öppna Inline Policies om det inte redan är öppet. Du bör se en princip där med ett namn som oneClick_Cognito_&lt;yourIdentityPoolName>Unauth_Role_1234567890123.
   1. Klicka på Redigera profil. Ersätt innehållet i policydokumentet med det här JSON-fragmentet:

   <table>
    <tbody>
     <tr>
     <td><p> </p> <p>{</p> <p> "Version": "2012-10-17",</p> <p> "Programsats": [</p> <p> {</p> <p> "Åtgärd": [</p> <p> "mobileanalytics:PutEvents",</p> <p> "cognito-sync:*",</p> <p> "SNS:CreatePlatformEndpoint",</p> <p> "SNS:Subscribe"</p> <p> ],</p> <p> "Effekt": "Tillåt",</p> <p> "Resurs": [</p> <p> "*"</p> <p> ]</p> <p> }</p> <p> ]</p> <p>}</p> <p> </p> </td>
     </tr>
    </tbody>
    </table>

   1. Klicka på **Använd princip**.

#### Använda meddelandetjänsten Pushwoosh {#using-the-pushwoosh-messaging-service}

Om du inte vill använda Pushwoosh kan du hoppa över det här steget.

Så här använder du Pushwoosh:

1. **Registrera dig hos Pushwoosh**

   1. Gå till pushwoosh.com och skapa ett konto.

1. **Skapa en API-åtkomsttoken**

   1. På Pushwoosh-webbplatsen går du till menyalternativet API Access för att generera en API Access-token. Spela in denna token på ett säkert sätt.

1. **Skapa en app**

   1. För Android™ måste du ange GCM API-nyckeln.
   1. När du konfigurerar programmet väljer du Cordova som ramverk.
   1. För iOS-stöd måste du ange certifikatfilen (.cer), push-certifikatet (.p12) och lösenordet för den privata nyckeln. Dessa bör ha hämtats från Apple APNS-webbplats. Välj Cordova under Framework.
   1. Pushwoosh genererar ett app-ID för den appen, i formatet&quot;XXXXX-XXXXX&quot;, där varje X är ett hexadecimalt värde (0 till F).

>[!NOTE]
>
>*Om en andra app har konfigurerats i AEM med samma app-ID (och andra relaterade värden: API Access-token och GCM-ID), kommer push-meddelanden som skickas via den andra appen på AEM att skickas till andra appar med detta app-ID.*

### Steg 3: Lägg till push-stöd i appen {#step-add-push-support-to-the-app}

#### Lägg till ContentSync-konfiguration {#add-contentsync-configuration}

Skapa två innehållsnoder (en i app-config och en i app-config-dev) som kallas notificationConfig:

* /content/`<your app>`/shell/jcr:content/page-app/app-config-dev/notificationsConfig
* /content/`<your app>`/shell/jcr:content/page-app/app-config/notificationsConfig

Med dessa egenskaper (.content.xml-filer):
&lt;jcr:root xmlns:jcr=&quot; [https://developer.adobe.com/experience-manager/reference-materials/spec/jcr/1.0/index.html](https://developer.adobe.com/experience-manager/reference-materials/spec/jcr/1.0/index.html)&quot; xmlns:nt=&quot; [https://developer.adobe.com/experience-manager/reference-materials/spec/jcr/1.0/index.html](https://developer.adobe.com/experience-manager/reference-materials/spec/jcr/1.0/index.html)&quot;
jcr:primärType=&quot;nt:ostrukturerad&quot;
excludeProperties=&quot;[appAPIAccessToken]&quot;
path=&quot;../../../...&quot;
targetRootDirectory=&quot;www&quot;
type=&quot;notificationskonfiguration&quot;/>

>[!NOTE]
>
>Hanteraren för innehållssynkronisering söker efter dessa noder, och om de inte finns där skrivs inte filen page-notifications-config.json ut.

#### Lägg till klientbibliotek {#add-client-libraries}

Klientbiblioteken för push-meddelanden måste läggas till i programmet genom att följa dessa steg:

I CRXDE Lite:

1. Navigera till */etc/designs/phonegap//clientlibsall.*
1. Dubbelklicka på inbäddningsavsnittet i egenskapsrutan.
1. Lägg till ett klientlib i dialogrutan som visas genom att klicka på plusknappen (+).
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

#### IOS {#ios}

För iOS använder du en macOS-dator och går med i [iOS Developer Program](https://developer.apple.com/programs/ios/). Vissa företag har företagslicenser som kan vara tillgängliga för alla utvecklare.

I XCode 8.1 måste du gå till fliken Funktioner i projektet innan du använder push-meddelanden och växla mellan att aktivera push-meddelanden.

#### Android™ {#android}

Om du vill installera appen på en Android™-telefon med CLI (se **Steg 6 - Bygg och distribuera appen**) måste du först placera telefonen i utvecklarläge. Mer information om hur du gör detta finns i [Aktivera alternativ för utvecklare på enheter](https://developer.android.com/tools/device.html#developer-device-options).

### Steg 5: Konfigurera push-AEM appar {#step-configure-push-on-aem-apps}

Innan du skapar och distribuerar till din konfigurerade mobila enhet måste du konfigurera meddelandeinställningarna för den meddelandetjänst som du valde att använda.

1. Skapa lämpliga auktoriseringsgrupper för push-meddelanden.
1. Logga in AEM lämplig användare och klicka på fliken Appar.
1. Klicka på appen.
1. Hitta rutan Hantera Cloud Service och klicka på pennan för att ändra dina molnkonfigurationer.
1. Välj Amazon SNS Connection, Pushwoosh Connection eller Adobe Mobile Services som meddelandekonfiguration.
1. Ange leverantörsegenskaperna och klicka på Skicka för att spara dem och Klar. De verifieras inte på fjärrbasis i detta skede, utom om det finns AMS.
1. Du bör nu se konfigurationen som du just angav på panelen Hantera Cloud Service.

### Steg 6: Skapa och distribuera appen {#step-build-and-deploy-the-app}

**Obs!** Se instruktionerna [här](/help/mobile/building-app-mobile-phonegap.md) om hur du skapar PhoneGap-program.

Det finns två sätt att skapa och distribuera din app med PhoneGap.

**Obs!** För testning av push-meddelanden räcker det inte med emulatorer eftersom push-meddelanden använder ett distinkt protokoll mellan push-providern (Apple eller Google) och enheten. Den aktuella maskinvaran och emulatorerna för Mac/PC stöder inte detta.

1. *PhoneGap Build* är en tjänst som erbjuds av PhoneGap som skapar din app åt dig på deras servrar och låter dig hämta den direkt till din enhet. Mer information om hur du konfigurerar och använder PhoneGap Build finns i PhoneGap Build-dokumentationen på `https://build.phonegap.com/`.

1. Med *PhoneGap Command Line Interface* (CLI) kan du använda en mängd PhoneGap-kommandon på kommandoraden för att skapa, felsöka och distribuera din app. Mer information om hur du konfigurerar och använder PhoneGap CLI finns i dokumentationen för PhoneGap-utvecklaren (`https://docs.phonegap.com/en/edge/guide_cli_index.md.html#The%20Command-Line%20Interface`).

### Steg 7: Skicka ett push-meddelande {#step-send-a-push-notification}

Följ de här stegen för att skapa ett meddelande och skicka det.

1. Skapa ett meddelande

   * På AEM Mobile-appens kontrollpanel hittar du panelen Push Notifications (Push-meddelanden).
   * Välj &quot;Skapa&quot; på menyn uppe till höger. Den här knappen är inte tillgänglig förrän molnkonfigurationen har ställts in.
   * I guiden Skapa meddelande anger du en titel och ett meddelande och klickar sedan på knappen&quot;Skapa&quot;. Meddelandet är nu klart att skickas omedelbart eller senare. Den kan redigeras och du kan ändra och spara meddelandet och/eller titeln.

1. Skicka meddelandet

   * Leta reda på panelen Push Notifications (Push-meddelanden) på panelen Apps.
   * Markera meddelandet eller klicka på informationsknappen längst ned till höger (.. .) för att visa listan med meddelanden. Den här listan anger också om ett meddelande är klart att skickas, om det redan har skickats eller om ett fel uppstod när meddelandet skickades.
   * Markera kryssrutan för ett meddelande (endast) och klicka på knappen&quot;Skicka meddelande&quot; ovanför listan. Du har en chans att&quot;avbryta&quot; eller&quot;skicka&quot; meddelandet i den dialogruta som visas.

1. Hantera resultaten

   * Om push-meddelandetjänsten (Amazon SNS eller Pushwoosh) tar emot sändningsbegäran, bekräftar att den är giltig och skickar den till ANE-leverantörerna (APNS och GCM) stängs dialogrutan Skicka utan meddelande. Statusen för det meddelandet visas som Skickat i meddelandelistan.
   * Om push-sändningen misslyckas visas ett meddelande i dialogrutan som anger problemet. I meddelandelistan anges meddelandets status som Fel, men om problemet åtgärdas kan meddelandet skickas igen. Om ett fel uppstår bör ytterligare felinformation visas i serverfelloggen.
   * Observera att det finns vissa plattformsskillnader mellan push-meddelanden i iOS och Android™. Bland dem:

      * När appen har distribuerats på Android™ kommer den att startas med CLI. I iOS måste du starta programmet manuellt. Eftersom push-registrering sker vid start kan Android™-appar få push-meddelanden direkt (eftersom de redan har startats och registrerats), medan iOS-appar inte kan det.
      * I Android™ är texten med OK i versaler (och i alla andra knappar som läggs till i meddelandet i appen), medan den inte finns i iOS.

För AMS-push-meddelanden måste meddelanden skapas och skickas från AMS-servern. AMS har ytterligare funktioner för push-meddelanden utöver de som finns i AEM meddelanden med AWS och Pushwoosh.

>[!NOTE]
>
>*Push-meddelanden kan inte levereras. De liknar meddelanden. Det bästa görs att se till att alla hör det, men de är inte en garanterad leveransmekanism. Tiden för att leverera en push-funktion kan dessutom variera från mindre än en sekund till upp till en halvtimme.*

### Konfigurera djup länkning med push-meddelanden {#configuring-deep-linking-with-push-notifications}

Vad är Djuplänkning? I samband med ett push-meddelande är det ett sätt att tillåta att en app öppnas eller dirigeras (om den är öppen) till en viss plats i programmet.

Hur fungerar det? Författaren av ett push-meddelande kan lägga till en knappetikett (d.v.s.&quot;Visa mig!&quot;) till meddelandet och väljer den sida som de vill länka i meddelandet via en visuell sökvägsläsare. När det skickas utförs push-åtgärden som vanligt förutom att knappen OK ersätts av knappen&quot;Stäng&quot; i meddelandet i appen och den nya knappen anges (&quot;Visa mig!&quot;) visas också. När du klickar på den nya knappen kommer programmet till den angivna sidan i programmet. Om du klickar på Stäng stängs meddelandet.

Om appen inte är öppen visas skuggan som vanligt. Om du utför en åtgärd på meddelandet i skuggan öppnas programmet och användaren får sedan tillgång till knapparna för djup länk baserat på vad som konfigurerats i push-meddelandet.

Skapa meddelandet, lägg till en knapptext och länksökväg för den valfria länken:

>[!CAUTION]
>
>Följ stegen nedan för att öppna panelen Push Notification (Push-meddelanden) på din instrumentpanel.

1. Klicka på redigeringen i det övre högra hörnet av rutan **Hantera Cloud Service**.

   ![chlimage_1-108](assets/chlimage_1-108.png)

1. Välj **Pushwoosh-anslutningen**. Klicka på **Nästa**.

   ![chlimage_1-109](assets/chlimage_1-109.png)

1. Ange information om egenskaperna och klicka på **Skicka**.

   ![chlimage_1-110](assets/chlimage_1-110.png)

   När du har skickat konfigurationen visas rutan **Push Notifications** på kontrollpanelen.

   ![chlimage_1-111](assets/chlimage_1-111.png)

### Guiden Skapa meddelande {#create-notification-wizard}

När panelen **Push Notifications** visas på kontrollpanelen använder du guiden Create Notification för att lägga till innehållet:

1. Klicka på Lägg till-symbolen i det övre högra hörnet av rutan **Push Notifications** för att öppna **Create Notification Wizard**.

   ![chlimage_1-112](assets/chlimage_1-112.png)

1. Om du klickar på bläddringsikonen i länksökvägen visas programmets innehållsstruktur för användaren.

   Klicka på bockikonen när du har valt sökvägen.

   ![chlimage_1-113](assets/chlimage_1-113.png)

   >[!NOTE]
   >
   >Länkknappstexten får innehålla högst 20 tecken.
   >
   >Om slutanvändaren inte har den senaste versionen av programmet och den länkade sökvägen inte är tillgänglig kommer användaren att hamna på programmets huvudsida om åtgärden för den djupa länken bekräftas.

1. Ange **textinformation** i guiden **Skapa meddelande** och klicka på **Skapa**.

   ![chlimage_1-114](assets/chlimage_1-114.png)

   Öppna informationen genom att klicka på det push-meddelande som du skapade i rutan **Push Notifications**.

   Du kan redigera egenskaper, skicka meddelanden eller ta bort meddelandet.

   ![chlimage_1-115](assets/chlimage_1-115.png)

>[!NOTE]
>
>**Ytterligare information**:
>
>Pushwoosh och Amazon SNS stöds inte efter version 6.4 och kommer att vara tillgängliga som tillägg från paketresursen.

### Nästa steg {#the-next-steps}

När du har fått mer information om push-meddelanden för din app kan du läsa [AEM Mobile Content Personalization](/help/mobile/phonegap-aem-mobile-content-personalization.md).
