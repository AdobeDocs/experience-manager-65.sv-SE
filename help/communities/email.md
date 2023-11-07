---
title: Konfigurerar e-post
description: Lär dig hur du konfigurerar e-postmeddelanden och prenumerationer för Adobe Experience Manager Communities.
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
pagetitle: Configuring Email
role: Admin
exl-id: bf97d388-f8ca-4e37-88e2-0c536834311e
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '752'
ht-degree: 0%

---

# Konfigurerar e-post {#configuring-email}

AEM Communities använder e-post för:

* [Communities-meddelanden](notifications.md)
* [Communities-prenumerationer](subscriptions.md)

Som standard fungerar inte e-postfunktionen eftersom den kräver att en SMTP-server och SMTP-användare anges.

>[!CAUTION]
>
>E-post för meddelanden och prenumerationer får endast konfigureras på [primär utgivare](deploy-communities.md#primary-publisher).

## Standardkonfiguration för e-posttjänst {#default-mail-service-configuration}

Standardtjänsten för e-post krävs för både meddelanden och prenumerationer.

* Logga in på den primära utgivaren med administratörsbehörighet och åtkomst till [Webbkonsol](../../help/sites-deploying/configuring-osgi.md):

   * Till exempel: [http://localhost:4503/system/console/configMgr](http://localhost:4503/system/console/configMgr)

* Leta reda på `Day CQ Mail Service`.
* Välj redigeringsikonen.

Detta baseras på dokumentationen till [Konfigurerar e-postmeddelande](../../help/sites-administering/notification.md), men med en skillnad i det fältet `"From" address` är *not* krävs och ska lämnas tom.

Exempel (ifylld med värden endast för illustrativa syften):

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

  Om det här alternativet är markerat skickas ett säkert e-postmeddelande. Kontrollera att porten är inställd på 465 eller så som krävs för en SMTP-server.
* **[!UICONTROL Debug email]**

  Om det här alternativet är markerat aktiveras loggning av SMTP-serverinteraktioner.

## AEM Communities e-postkonfiguration {#aem-communities-email-configuration}

När [standardtjänst för e-post](#default-mail-service-configuration) är konfigurerad, de två befintliga instanserna av `AEM Communities Email Reply Configuration` OSGi-konfigurationen, som ingår i versionen, blir funktionell.

Endast prenumerationsinstansen måste konfigureras ytterligare när svar tillåts via e-post.

1. [E-post](#configuration-for-notifications) instans:

   För meddelanden, som inte har stöd för svarsmeddelanden via e-post, och bör inte ändras.

1. [Prenumerationer-e-post](#configuration-for-subscriptions) instans:

   Kräver konfiguration för att fullständigt aktivera skapande av inlägg från svarsmeddelanden via e-post.

Så här når du instanserna för webbgruppskonfigurationen:

* Logga in på den primära utgivaren med administratörsbehörighet och åtkomst till [Webbkonsol](../../help/sites-deploying/configuring-osgi.md)

   * Till exempel: [http://localhost:4503/system/console/configMgr](http://localhost:4503/system/console/configMgr)

* Sök `AEM Communities Email Reply Configuration`.

![email-reply-config](assets/email-reply-config.png)

### Konfiguration för meddelanden {#configuration-for-notifications}

Instansen av `AEM Communities Email Reply Configuration` OSGi-konfigurationen med e-postmeddelandet Namn är en funktion för framtida meddelanden. Den här funktionen inkluderar inte e-postsvar.

Ändra inte den här konfigurationen.

* Leta reda på `AEM Communities Email Reply Configuration`.
* Välj redigeringsikonen.
* Verifiera att **Namn** är `email`.

* Verifiera att **Skapa inlägg från svarsmejl** är `unchecked`.

![configure-email-reply](assets/configure-email-reply.png)

### Konfiguration för prenumerationer {#configuration-for-subscriptions}

För webbgruppsprenumerationer är det möjligt att aktivera eller inaktivera möjligheten för en medlem att publicera innehåll genom att svara på ett e-postmeddelande.

* Leta reda på `AEM Communities Email Reply Configuration`.
* Välj redigeringsikonen.
* Verifiera att **Namn** är `subscriptions-email`.

  ![configure-email-subscription](assets/configure-email-subscriptions.png)

* **[!UICONTROL Name]**

  *(Obligatoriskt)* `subscriptions-email`. Redigera inte.

* **[!UICONTROL Create post from reply email]**

  Om det här alternativet är markerat kan mottagaren av ett prenumerationsmeddelande posta innehåll genom att skicka ett svar. Standard är markerat.
* **[!UICONTROL Add tracked id to header]**

  Standard är `Reply-To`.

* **[!UICONTROL Maximum length of Subject]**

  Om spårar-ID läggs till på ämnesraden är detta den maximala längden för motivet, exklusive spårade ID, efter vilken det beskärs. Detta bör vara så litet som möjligt för att undvika att spårad ID-information går förlorad. Standardvärdet är 200.

* **[!UICONTROL "Reply-To" email address]**

  Adress som används som e-postadress för Svara till. Standard är `no-reply@example.com`.

* **[!UICONTROL Reply-to-Delimiter]**

  Om spårar-ID läggs till i svarshuvudet används den här avgränsaren. Standard är `+` (plustecken)

* **[!UICONTROL Tracker Id prefix in subject]**

  Om spårar-ID läggs till på ämnesraden används det här prefixet. Standard är `post#`.

* **[!UICONTROL Tracker id prefix in message body]**

  Om spårar-ID läggs till i meddelandetexten används det här prefixet. Standard är `Please do not remove this:`.

* **[!UICONTROL Email as HTML]**: Om det här alternativet är markerat anges innehållstypen för e-post som `"text/html;charset=utf-8"`. Standard är markerat.

* **[!UICONTROL Default user name]**

  Det här namnet används för användare utan namn. Standard är `no-reply@example.com`.

* **[!UICONTROL Templates root path]**

  E-postmeddelandet skapas med en mall som lagras på den här rotsökvägen. Standard är `/etc/community/templates/subscriptions-email`.

## Konfigurera avsökningsimporteraren {#configure-polling-importer}

För att e-postmeddelandet ska kunna hämtas till databasen måste du konfigurera en avsökningsimportör och konfigurera dess egenskaper i databasen manuellt.

### Lägg till ny avsökningsimportör {#add-new-polling-importer}

* Logga in på den primära utgivaren med administratörsbehörighet och bläddra till avsökningsimportkonsolen:

  Till exempel: [http://localhost:4503/etc/importers/polling.html](http://localhost:4503/etc/importers/polling.html)

* Välj **[!UICONTROL Add]**

  ![avsökare](assets/polling-importer.png)

* **[!UICONTROL Type]**

  *(Obligatoriskt)* Dra ned för att välja `POP3 (over SSL)`.

* **[!UICONTROL URL]**

  *(Obligatoriskt)* Servern för utgående e-post. Till exempel, `pop.gmail.com:995/INBOX?username=community-emailgmail.com&password=****`.

* **[!UICONTROL Import to Path]**&amp;ast;

  *(Obligatoriskt)* Ange till `/content/usergenerated/mailFolder/postEmails`
genom att gå till `postEmails`mapp och markera **OK**.

* **[!UICONTROL Update Interval in Seconds]**

  *(Valfritt)* E-postservern som konfigurerats för standardtjänsten för e-post kan ha krav på uppdateringsintervallvärdet. Gmail kan till exempel kräva ett intervall av `300`.

* **[!UICONTROL Login]**

  *(Valfritt)*

* **[!UICONTROL Password]**

  *(Valfritt)*

* Välj **[!UICONTROL OK]**.

### Justera protokoll för ny avsökningsimportör {#adjust-protocol-for-new-polling-importer}

När den nya avsökningskonfigurationen har sparats är det nödvändigt att ändra egenskaperna för prenumerationens e-postimporterare ytterligare för att ändra protokollet från `POP3` till `emailreply`.

Använda [CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md):

* Logga in på den primära utgivaren med administratörsbehörighet och bläddra till [https://&lt;server>:&lt;port>/crx/de/index.jsp#/etc/importer/polling](http://localhost:4503/crx/de/index.jsp#/etc/importers/polling).
* Markera den nya konfigurationen och ändra följande egenskaper:

   * **feedType**: Ersätt `pop3s` med **`emailreply`**
   * **källa**: Ersätt källans protokoll `pop3s://` med **`emailreply://`**

![polling-protocol](assets/polling-protocol.png)

De röda trianglarna anger de ändrade egenskaperna. Spara ändringarna:

* Välj **[!UICONTROL Save All]**.
