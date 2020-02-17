---
title: Konfigurerar e-post
seo-title: Konfigurerar e-post
description: E-postkonfiguration för Communities
seo-description: E-postkonfiguration för Communities
uuid: e8422cc2-1594-43b0-b587-82825636cec1
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: b4d38e45-eaa0-4ace-a885-a2e84fdfd5a1
pagetitle: Configuring Email
translation-type: tm+mt
source-git-commit: 58fa0f05bae7ab5ba51491be3171b5c6ffbe870d

---


# Konfigurerar e-post {#configuring-email}

AEM Communities använder e-post för

* [Communities-meddelanden](notifications.md)
* [Communities-prenumerationer](subscriptions.md)

E-postfunktionen fungerar inte som standard eftersom den kräver en specifikation av en SMTP-server och en SMTP-användare.

>[!CAUTION]
>
>E-post för meddelanden och prenumerationer får bara konfigureras på den [primära utgivaren](deploy-communities.md#primary-publisher).

## Standardkonfiguration för e-posttjänst {#default-mail-service-configuration}

Standardtjänsten för e-post krävs för både meddelanden och prenumerationer.

* På den primära utgivaren
* Inloggad med administratörsbehörighet
* Åtkomst till [webbkonsolen](../../help/sites-deploying/configuring-osgi.md)

   * Till exempel [http://localhost:4503/system/console/configMgr](http://localhost:4503/system/console/configMgr)

* Leta reda på `Day CQ Mail Service`
* Markera redigeringsikonen

Detta baseras på dokumentationen för [konfigurering av e-postmeddelanden](../../help/sites-administering/notification.md), men med en skillnad i att fältet `"From" address` inte ** är obligatoriskt och ska lämnas tomt.

Till exempel (ifylld med värden endast för illustrationsändamål):

![chlimage_1-98](assets/chlimage_1-98.png)

* **[!UICONTROL SMTP-serverns värdnamn]**: *(obligatoriskt)* SMTP-servern som ska användas.

* **[!UICONTROL SMTP-serverport]** *(krävs)* SMTP-serverporten måste vara 25 eller högre.

* **[!UICONTROL SMTP-användare]**: *(obligatoriskt)* SMTP-användaren.

* **[!UICONTROL SMTP-lösenord]**: *(obligatoriskt)* SMTP-användarens lösenord.

* **[!UICONTROL &quot;Från&quot;-adress]**: Lämna tomt
* **[!UICONTROL SMTP använder SSL]**: Om det här alternativet är markerat skickas säker e-post. Kontrollera att porten är inställd på 465 eller som krävs för SMTP-servern.
* **[!UICONTROL Felsök e-post]**: Om det här alternativet är markerat aktiveras loggning av SMTP-serverinteraktioner.

## E-postkonfiguration för AEM Communities {#aem-communities-email-configuration}

När [standardtjänsten](#default-mail-service-configuration) för e-post har konfigurerats fungerar de två befintliga instanserna av `AEM Communities Email Reply Configuration` OSGi-konfigurationen som ingår i versionen.

Endast prenumerationsinstansen behöver konfigureras ytterligare när svar tillåts via e-post.

1. ` [email](#configuration-for-notifications)` instance

   för meddelanden, som inte har stöd för e-post med svar, och som inte ska ändras

1. ` [subscriptions-email](#configuration-for-subscriptions)` instance

   kräver konfiguration för att fullständigt aktivera skapande av post från svars-e-post

Så här når du instanserna för webbgruppskonfigurationen:

* På den primära utgivaren
* Inloggad med administratörsbehörighet
* Åtkomst till [webbkonsolen](../../help/sites-deploying/configuring-osgi.md)

   * Till exempel [http://localhost:4503/system/console/configMgr](http://localhost:4503/system/console/configMgr)

* Sök `AEM Communities Email Reply Configuration`

![chlimage_1-99](assets/chlimage_1-99.png)

### Konfiguration för meddelanden {#configuration-for-notifications}

Instansen av `AEM Communities Email Reply Configuration` OSGi-konfigurationen med e-postmeddelandet Namn är funktionen för meddelanden. Den här funktionen inkluderar inte e-postsvar.

Den här konfigurationen bör inte ändras.

* Leta reda på `AEM Communities Email Reply Configuration`
* Markera redigeringsikonen
* Kontrollera att **namnet** är `email`

* Verifiera att **Skapa inlägg från svarsmeddelanden** är `unchecked`

![chlimage_1-100](assets/chlimage_1-100.png)

### Konfiguration för prenumerationer {#configuration-for-subscriptions}

För webbgruppsprenumerationer är det möjligt att aktivera eller inaktivera möjligheten för en medlem att publicera innehåll genom att svara på ett e-postmeddelande.

* Leta reda på `AEM Communities Email Reply Configuration`
* Markera redigeringsikonen
* Kontrollera att **namnet** är `subscriptions-email`

![chlimage_1-101](assets/chlimage_1-101.png)

* **[!UICONTROL Namn]** : *(obligatoriskt)* `subscriptions-email`. Redigera inte.

* **[!UICONTROL Skapa inlägg från svarsmejl]**: Om det här alternativet är markerat kan den som tar emot e-postprenumerationen posta innehåll genom att skicka ett svar. Standard är markerat.
* **[!UICONTROL Lägg till spårat ID i sidhuvud]**:Standardvärdet är `Reply-To`.

* **[!UICONTROL Maximal längd på ämne]**: Om spårar-ID läggs till på ämnesraden är detta den maximala längden för motivet, exklusive spårade ID, efter vilken det trimmas. Observera att detta bör vara så litet som möjligt för att undvika att spårad ID-information går förlorad. Standardvärdet är 200.
* **[!UICONTROL E-postadress]** från: *(obligatoriskt)* Adress som e-postmeddelanden ska levereras från. Sannolikt samma **SMTP-användare** som angetts för [standardtjänsten](#configuredefaultmailservice)för e-post. Standardvärdet är `no-reply@example.com`.

* **[!UICONTROL Svar till avgränsare]**: Om spårar-ID läggs till i svarshuvudet används den här avgränsaren. Standardvärdet är `+` (plustecken).

* **[!UICONTROL Spårar-ID-prefix i ämne]**: Om spårar-ID läggs till på ämnesraden används det här prefixet. Standardvärdet är `post#`.

* **[!UICONTROL Spårar-ID-prefix i meddelandetexten]**: Om spårar-ID läggs till i meddelandetexten används det här prefixet. Standardvärdet är `Please do not remove this:`.

* **[!UICONTROL Mejla som HTML]**: Om det här alternativet är markerat anges innehållstypen för e-post som `"text/html;charset=utf-8"`. Standard är markerat.

* **[!UICONTROL Standardanvändarnamn]**: Det här namnet används för användare utan namn. Standardvärdet är `no-reply@example.com`.

* **[!UICONTROL Mallens rotsökväg]**: E-postmeddelandet skapas med en mall som lagras på den här rotsökvägen. Standardvärdet är `/etc/community/templates/subscriptions-email`.

## Konfigurera avsökningsimporteraren {#configure-polling-importer}

För att e-postmeddelandet ska kunna hämtas till databasen måste du konfigurera en avsökningsimportör och konfigurera dess egenskaper i databasen manuellt.

### Lägg till ny avsökningsimportör {#add-new-polling-importer}

* På den primära utgivaren
* Inloggad med administratörsbehörighet
* Bläddra till avsökningsimportkonsolenTill exempel [http://localhost:4503/etc/importers/polling.html](http://localhost:4503/etc/importers/polling.html)
* Välj **[!UICONTROL Lägg till]**

![chlimage_1-102](assets/chlimage_1-102.png)

* **[!UICONTROL Typ]**: *(obligatoriskt)* Välj `POP3 (over SSL).`

* **[!UICONTROL URL]**: *(obligatoriskt)* Servern för utgående e-post. Exempel, `pop.gmail.com:995/INBOX?username=community-emailgmail.com&password=****`

* **[!UICONTROL Importera till bana]**&amp;stämpel;ast;: *(obligatoriskt)* Ange till `/content/usergenerated/mailFolder/postEmails`genom att bläddra till `postEmails`mappen och välja **OK**

* **[!UICONTROL Uppdateringsintervall i sekunder]**: *(valfritt)* E-postservern som är konfigurerad för standardtjänsten för e-post kan ha krav på uppdateringsintervallvärdet. Gmail kan till exempel kräva ett intervall av `300`.

* **[!UICONTROL Inloggning]**: *(valfritt)*

* **[!UICONTROL Lösenord]**: *(valfritt)*

* Välj **[!UICONTROL OK]**

### Justera protokoll för ny avsökningsimportör {#adjust-protocol-for-new-polling-importer}

När den nya avsökningskonfigurationen har sparats är det nödvändigt att ändra egenskaperna för prenumerationens e-postimportör ytterligare för att ändra protokollet från `POP3` till `emailreply`

Använda [CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md):

* På den primära utgivaren
* Inloggad med administratörsbehörighet
* Gå till [https://&lt;server>:&lt;port>/crx/de/index.jsp#/etc/importer/polling](http://localhost:4503/crx/de/index.jsp#/etc/importers/polling)
* Välj den nya konfigurationen
* Ändra följande egenskaper

   * **feedType**: ersätt `pop3s` med **`emailreply`**
   * **källa**: ersätt källans protokoll `pop3s://` med **`emailreply://`**

![chlimage_1-103](assets/chlimage_1-103.png)

De röda trianglarna anger de ändrade egenskaperna. Spara ändringarna:

* Välj **[!UICONTROL Spara alla]**

