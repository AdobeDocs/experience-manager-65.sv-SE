---
title: Hantera prenumerationer
seo-title: Managing Subscriptions
description: Användare kan uppmanas att prenumerera på e-postleverantörens e-postlistor med hjälp av formulärkomponenten som används på en AEM webbsida. Om du vill förbereda en AEM sida med ett registreringsformulär för prenumeration på e-posttjänstens e-postlistor måste du använda motsvarande tjänstkonfiguration på den AEM sidan som den potentiella prenumeranten kommer att besöka.
seo-description: Users can be asked to subscribe to Email Service Provider's mailing lists with the help of the Form component used on an AEM web page. To prepare an AEM page with a sign-up form for subscription to your e-mail service mailing lists, you must apply the corresponding service configuration to the AEM page that the potential subscriber will visit.
uuid: b2578a3d-dba1-4114-b21a-5f34c0cccc5a
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: 295cb0a6-29db-42aa-824e-9141b37b5086
exl-id: add05d22-3a11-49e9-a554-2315962552d5
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '916'
ht-degree: 0%

---

# Hantera prenumerationer{#managing-subscriptions}

>[!NOTE]
>
>Adobe planerar inte att ytterligare förbättra denna funktion (Hantera leads och listor).
>Rekommendationen är att [Adobe Campaign och dess AEM](/help/sites-administering/campaign.md).

Användare kan uppmanas att prenumerera på **E-postleverantörens** e-postlistor med hjälp av **Formulär** -komponent som används på en AEM webbsida. Om du vill förbereda en AEM sida med ett registreringsformulär för prenumeration på e-posttjänstens e-postlistor måste du använda motsvarande tjänstkonfiguration på den AEM sidan som den potentiella prenumeranten kommer att besöka.

## Tillämpar e-posttjänstkonfiguration på en sida {#applying-email-service-configuration-to-a-page}

Så här konfigurerar du en AEM:

1. Navigera till **Webbplatser** -fliken.
1. Välj den sida som ska konfigureras för tjänsten. Högerklicka på sidan och välj **Egenskaper**.

1. Välj **Cloud Services** sedan **Lägg till tjänst**. Välj en konfiguration i listan över tillgängliga konfigurationer.

   ![chlimage_1-164](assets/chlimage_1-164.png)

1. Klicka **OK**.

## Skapa ett anmälningsformulär på en AEM sida för att prenumerera/avbryta prenumerationer på listor {#creating-a-sign-up-form-on-an-aem-page-for-subscribing-unsubscribing-to-lists}

Så här skapar du ett anmälningsformulär och konfigurerar det för prenumerationer på e-postleverantörens sändlistor:

1. Öppna AEM som användaren ska besöka.
1. Använd e-postleverantörens konfiguration på sidan.

1. Lägg till en **Formulär** till sidan genom att dra komponenten från sidosparken. Om komponenten inte är tillgänglig växlar du till designläge och aktiverar **Formulär** grupp.
1. Klicka **Redigera** i **Formulärets början** och navigera till **Avancerat** -fliken.
1. I **Formulär** nedrullningsbar meny, välja **E-posttjänst: Skapa prenumerant** och lägg till i listan.
1. Längst ned i dialogrutan öppnar du **Åtgärdskonfiguration** som gör att du kan välja en eller flera prenumerationslistor.
1. I **Välj lista** markerar du den lista som du vill att användarna ska prenumerera på. Du kan lägga till flera listor med plusknappen (**Lägg till objekt**).

   ![chlimage_1-10](assets/chlimage_1-10.jpeg)

   >[!NOTE]
   >
   >Dialogrutan kan variera beroende på vilken e-postleverantör du har.

1. I **Formulär** väljer du den tacksida som du vill att användarna ska gå till efter att de har skickat in formuläret (om det lämnas tomt visas formuläret igen när det skickas.) Klicka **OK**. An **E-post-ID** -komponenten visas i formuläret, där du kan skapa ett formulär där användare kan skicka sina e-postadresser för att prenumerera eller avbryta prenumerationen från en e-postlista.
1. Lägg till **Skicka** knappkomponent från **Formulär** i sidesparken.

   Formuläret är klart. Publicera sidan som konfigurerats i stegen ovan tillsammans med **tack** till publiceringsinstansen. Alla potentiella prenumeranter som besöker sidan kan fylla i formuläret och prenumerera på listan som finns i konfigurationen.

   >[!NOTE]
   >
   >Om du vill att formulärprenumerationen ska fungera korrekt [krypteringsnycklar från författaren måste exporteras och importeras till publiceringsinstansen](#exporting-keys-from-author-and-importing-on-publish).

## Exportera nycklar från författaren och importera vid publicering {#exporting-keys-from-author-and-importing-on-publish}

För att e-posttjänsten ska kunna prenumerera och sluta prenumerera via anmälningsformuläret på publiceringsinstansen måste du följa dessa steg:

1. Gå till Package Manager på författarinstansen.
1. Skapa ett nytt paket. Ställ in filtret som `/etc/key`.
1. Bygg och hämta paketet.
1. Navigera till Package Manager på publiceringsinstansen och överför det här paketet.
1. Navigera till Publish SGB-konsolen och starta om paketet med namnet **Stöd för Adobe Granite Crypto**.

## Avbeställa prenumeration för användare från listor {#unsubscribing-users-from-lists}

Så här avbeställer du användare från listor:

1. Öppna sidegenskaperna för den AEM sidan som har registreringsformuläret för att avbryta prenumerationen på ett lead.
1. Använd tjänstkonfigurationen på sidan.
1. Skapa ett anmälningsformulär på sidan.
1. När du konfigurerar komponenten väljer du åtgärden **E-posttjänst**: **Avbeställ användare från listan.**
1. I listrutan väljer du lämplig lista som användaren ska tas bort från när prenumerationen avbryts.

   ![chlimage_1-11](assets/chlimage_1-11.jpeg)

1. Exportera nycklarna från författaren till publiceringen.

## Konfigurera e-postmeddelanden med automatisk svarare för e-posttjänst {#configuring-auto-responder-emails-for-email-service}

Så här konfigurerar du ett e-postmeddelande med automatiskt svar för en prenumerant:

1. Öppna sidegenskaperna för den AEM sidan som har registreringsformuläret för att konfigurera automatisk svarare för en lead.
1. Använd konfigurationen ExactTarget på sidan.

1. Lägg till en **Formulär** till sidan genom att dra komponenten från sidosparken. Om komponenten inte är tillgänglig växlar du till designläge och aktiverar **Formulär** grupp.
1. Klicka **Redigera** i **Formulärets början** och navigera till **Avancerat** -fliken.
1. I **Formulär** nedrullningsbar meny, välja **E-posttjänst: Skicka e-post för automatisk svarare.**
1. **Välj ett e-postmeddelande** (det här är det e-postmeddelande som skickas som ett e-postmeddelande med automatiskt svar).

1. **Välj klassificering** (den här klassificeringen används för att skicka e-postmeddelandet).
1. Välj **Tack** sida (den sida som användarna dirigeras till när de har skickat formuläret).

   I **Formulär** väljer du den tacksida som du vill att användarna ska gå till när de har skickat in formuläret. (Om formuläret lämnas tomt visas det igen när det skickas.) Klicka **OK**.

1. Exportera nycklarna från författaren till publiceringen.
1. Lägg till **Skicka** knappkomponent från **Formulär** i sidesparken.

   Anmälningsformuläret är klart. Publicera sidan som konfigurerats i stegen ovan tillsammans med **tack** till publiceringsinstansen. Alla potentiella abonnenter som besöker sidan kan fylla i formuläret och när de skickar in formuläret ska besökaren få ett e-postmeddelande med automatiskt svar på det e-post-ID som fylls i formuläret.

   >[!NOTE]
   >
   >Så här fungerar prenumerationen på registreringsformulär korrekt: [krypteringsnycklar från författaren måste exporteras och importeras till publiceringsinstansen](#exporting-keys-from-author-and-importing-on-publish).

   ![chlimage_1-12](assets/chlimage_1-12.jpeg)
