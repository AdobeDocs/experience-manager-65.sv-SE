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
source-git-commit: 570c970c328ded828680baeb1b04ab4361a36226
workflow-type: tm+mt
source-wordcount: '750'
ht-degree: 1%

---


# Konfigurerar e-post {#configuring-email}

AEM Communities använder e-post för:

* [Communities-meddelanden](notifications.md)
* [Communities-prenumerationer](subscriptions.md)

E-postfunktionen fungerar inte som standard eftersom den kräver en specifikation av en SMTP-server och en SMTP-användare.

>[!CAUTION]
>
>E-post för meddelanden och prenumerationer får bara konfigureras på den [primära utgivaren](deploy-communities.md#primary-publisher).


## Standardkonfiguration för e-posttjänst {#default-mail-service-configuration}

Standardtjänsten för e-post krävs för både meddelanden och prenumerationer.

* Logga in på den primära utgivaren med administratörsbehörighet och få tillgång till [webbkonsolen](../../help/sites-deploying/configuring-osgi.md):

   * Till exempel [http://localhost:4503/system/console/configMgr](http://localhost:4503/system/console/configMgr)

* Leta rätt på `Day CQ Mail Service`.
* Välj redigeringsikonen.

Detta baseras på dokumentationen för [konfigurering av e-postmeddelanden](../../help/sites-administering/notification.md), men med en skillnad i att fältet `"From" address` inte ** är obligatoriskt och ska lämnas tomt.

Till exempel (ifylld med värden endast för illustrationsändamål):

![email-config](assets/email-config.png)

* **[!UICONTROL SMTP server host name]**

   *(Obligatoriskt)* SMTP-servern som ska användas.

* **[!UICONTROL SMTP server port]**

   *(Obligatoriskt)* SMTP-serverporten måste vara 25 eller högre.

* **[!UICONTROL SMTP user]**

   *(Obligatoriskt)* SMTP-användaren.

* **[!UICONTROL SMTP password]**

   *(Obligatoriskt)* SMTP-användarens lösenord.

* **[!UICONTROL "From" address]**

   Lämna tomt
* **[!UICONTROL SMTP use SSL]**

   Om det här alternativet är markerat skickas säker e-post. Kontrollera att porten är inställd på 465 eller som krävs för SMTP-servern.
* **[!UICONTROL Debug email]**

   Om det här alternativet är markerat aktiveras loggning av SMTP-serverinteraktioner.

## AEM Communities e-postkonfiguration {#aem-communities-email-configuration}

När [standardtjänsten](#default-mail-service-configuration) för e-post har konfigurerats fungerar de två befintliga instanserna av `AEM Communities Email Reply Configuration` OSGi-konfigurationen som ingår i versionen.

Endast prenumerationsinstansen behöver konfigureras ytterligare när svar tillåts via e-post.

1. [E-postinstans](#configuration-for-notifications) :

   För meddelanden, som inte har stöd för svarsmeddelanden via e-post, och bör inte ändras.

1. [Subscriptions-email](#configuration-for-subscriptions) instance:

   Kräver konfiguration för att fullständigt aktivera skapande av inlägg från svarsmeddelanden via e-post.

Så här når du instanserna för webbgruppskonfigurationen:

* Logga in på den primära utgivaren med administratörsbehörighet och åtkomst till [webbkonsolen](../../help/sites-deploying/configuring-osgi.md)

   * Till exempel [http://localhost:4503/system/console/configMgr](http://localhost:4503/system/console/configMgr)

* Hitta `AEM Communities Email Reply Configuration`.

![email-reply-config](assets/email-reply-config.png)

### Konfiguration för meddelanden {#configuration-for-notifications}

Instansen av `AEM Communities Email Reply Configuration` OSGi-konfigurationen med e-postmeddelandet Namn är funktionen för meddelanden. Den här funktionen inkluderar inte e-postsvar.

Den här konfigurationen bör inte ändras.

* Leta rätt på `AEM Communities Email Reply Configuration`.
* Välj redigeringsikonen.
* Kontrollera att **namnet** är `email`.

* Kontrollera att **Skapa inlägg från svarsmeddelanden** är `unchecked`.

![configure-email-reply](assets/configure-email-reply.png)

### Konfiguration för prenumerationer {#configuration-for-subscriptions}

För webbgruppsprenumerationer är det möjligt att aktivera eller inaktivera möjligheten för en medlem att publicera innehåll genom att svara på ett e-postmeddelande.

* Leta rätt på `AEM Communities Email Reply Configuration`.
* Välj redigeringsikonen.
* Kontrollera att **namnet** är `subscriptions-email`.

   ![configure-email-subscription](assets/configure-email-subscriptions.png)

* **[!UICONTROL Name]**

   *(Krävs)* `subscriptions-email`. Redigera inte.

* **[!UICONTROL Create post from reply email]**

   Om det här alternativet är markerat kan den som tar emot e-postprenumerationen posta innehåll genom att skicka ett svar. Standard är markerat.
* **[!UICONTROL Add tracked id to header]**

   Standardvärdet är `Reply-To`.

* **[!UICONTROL Maximum length of Subject]**

   Om spårar-ID läggs till på ämnesraden är detta den maximala längden för motivet, exklusive spårade ID, efter vilken det trimmas. Observera att detta bör vara så litet som möjligt för att undvika att spårad ID-information går förlorad. Standardvärdet är 200.

* **[!UICONTROL "Reply-To" email address]**

   Adress som används som e-postadress för Svara till. Standardvärdet är `no-reply@example.com`.

* **[!UICONTROL Reply-to-Delimiter]**

   Om spårar-ID läggs till i svarshuvudet används den här avgränsaren. Standardvärdet är `+` (plustecken).

* **[!UICONTROL Tracker Id prefix in subject]**

   Om spårar-ID läggs till på ämnesraden används det här prefixet. Standardvärdet är `post#`.

* **[!UICONTROL Tracker id prefix in message body]**

   Om spårar-ID läggs till i meddelandetexten används det här prefixet. Standardvärdet är `Please do not remove this:`.

* **[!UICONTROL Email as HTML]**: Om det här alternativet är markerat anges innehållstypen för e-post som `"text/html;charset=utf-8"`. Standard är markerat.

* **[!UICONTROL Default user name]**

   Det här namnet används för användare utan namn. Standardvärdet är `no-reply@example.com`.

* **[!UICONTROL Templates root path]**

   E-postmeddelandet skapas med en mall som lagras på den här rotsökvägen. Standardvärdet är `/etc/community/templates/subscriptions-email`.

## Konfigurera avsökningsimporteraren {#configure-polling-importer}

För att e-postmeddelandet ska kunna hämtas till databasen måste du konfigurera en avsökningsimportör och konfigurera dess egenskaper i databasen manuellt.

### Lägg till ny avsökningsimportör {#add-new-polling-importer}

* Logga in på den primära utgivaren med administratörsbehörighet och bläddra till avsökningsimportkonsolen:

   Till exempel [http://localhost:4503/etc/importers/polling.html](http://localhost:4503/etc/importers/polling.html)

* Välj **[!UICONTROL Add]**

   ![avsökare](assets/polling-importer.png)

* **[!UICONTROL Type]**

   *(Obligatoriskt)* Välj genom att dra nedåt `POP3 (over SSL)`.

* **[!UICONTROL URL]**

   *(Obligatoriskt)* Servern för utgående e-post. Till exempel, `pop.gmail.com:995/INBOX?username=community-emailgmail.com&password=****`.

* **[!UICONTROL Import to Path]**&amp;ast;

   *(Obligatoriskt)* Ange till `/content/usergenerated/mailFolder/postEmails`genom att bläddra till `postEmails`mappen och välj **OK**.

* **[!UICONTROL Update Interval in Seconds]**

   *(Valfritt)* E-postservern som är konfigurerad för standardtjänsten för e-post kan ha krav på uppdateringsintervallvärdet. Gmail kan till exempel kräva ett intervall av `300`.

* **[!UICONTROL Login]**

   *(Valfritt)*

* **[!UICONTROL Password]**

   *(Valfritt)*

* Välj **[!UICONTROL OK]**.

### Justera protokoll för ny avsökningsimportör {#adjust-protocol-for-new-polling-importer}

När den nya avsökningskonfigurationen har sparats är det nödvändigt att ändra egenskaperna för prenumerationens e-postimporterare ytterligare för att ändra protokollet från `POP3` till `emailreply`.

Använda [CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md):

* Logga in på den primära utgivaren med administratörsbehörighet och gå till [https://&lt;server>:&lt;port>/crx/de/index.jsp#/etc/importer/polling](http://localhost:4503/crx/de/index.jsp#/etc/importers/polling).
* Markera den nya konfigurationen och ändra följande egenskaper:

   * **feedType**: Ersätt `pop3s` med **`emailreply`**
   * **källa**: Ersätt källans protokoll `pop3s://` med **`emailreply://`**

![polling-protocol](assets/polling-protocol.png)

De röda trianglarna anger de ändrade egenskaperna. Spara ändringarna:

* Välj **[!UICONTROL Save All]**.

