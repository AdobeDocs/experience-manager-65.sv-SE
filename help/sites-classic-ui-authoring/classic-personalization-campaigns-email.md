---
title: E-postmarknadsföring
description: E-postmarknadsföring (till exempel nyhetsbrev) är en viktig del av alla marknadsföringskampanjer när ni använder dem för att förmedla innehåll till era leads. I AEM kan du skapa nyhetsbrev från befintligt AEM och lägga till nytt innehåll, som är specifikt för nyhetsbreven.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
docset: aem65
exl-id: a1d8b74e-67eb-4338-9e8e-fd693b1dbd48
solution: Experience Manager, Experience Manager Sites
feature: Authoring,Personalization
role: User
source-git-commit: 305227eff3c0d6414a5ae74bcf3a74309dccdd13
workflow-type: tm+mt
source-wordcount: '1767'
ht-degree: 0%

---


# E-postmarknadsföring{#e-mail-marketing}

>[!NOTE]
>
>Adobe planerar inte att ytterligare förbättra e-postspårningen av öppna meddelanden/studsar (som inte kan levereras) som skickas av AEM SMTP-tjänst.
>Rekommendationen är att använda [Adobe Campaign och integrationen med AEM](/help/sites-administering/campaign.md).

E-postmarknadsföring (till exempel nyhetsbrev) är en viktig del av alla marknadsföringskampanjer när ni använder dem för att förmedla innehåll till era leads. I AEM kan du skapa nyhetsbrev från befintligt AEM och lägga till nytt innehåll, som är specifikt för nyhetsbreven.

När de har skapats kan du skicka nyhetsbrev till den specifika användargruppen antingen direkt eller vid en annan schemalagd tidpunkt (med hjälp av ett arbetsflöde). Dessutom kan användare prenumerera på nyhetsbrev i det format de väljer.

Dessutom kan du AEM administrera nyhetsbrevets funktionalitet, inklusive att underhålla ämnen, arkivera nyhetsbrev och visa nyhetsbrevets statistik.

>[!NOTE]
>
>I Geometrixx öppnas e-postredigeraren automatiskt i nyhetsbrevmallen. Du kan använda e-postredigeraren i andra mallar som du vill skicka e-postmeddelanden med, till exempel, inbjudningar. E-postredigeraren visas när en sida ärvs från **mcm/components/newsletter/page**.

I det här dokumentet beskrivs grunderna för hur du skapar nyhetsbrev i AEM. Mer detaljerad information om hur du arbetar med e-postmarknadsföring finns i följande dokument:

* [Skapa en startsida för ett effektivt nyhetsbrev](/help/sites-classic-ui-authoring/classic-personalization-campaigns-email-landingpage.md)
* [Hantera prenumerationer](/help/sites-classic-ui-authoring/classic-personalization-campaigns-email-subscriptions.md)
* [Publicera ett e-postmeddelande till e-postleverantörer](/help/sites-classic-ui-authoring/classic-personalization-campaigns-email-newsletters.md)
* [Spåra studsade e-postmeddelanden](/help/sites-classic-ui-authoring/classic-personalization-campaigns-email-tracking-bounces.md)

>[!NOTE]
>
>Om du uppdaterar e-postleverantörer, gör ett flygtest eller skickar ett nyhetsbrev misslyckas dessa åtgärder om nyhetsbrevet inte publiceras till publiceringsinstansen först eller om publiceringsinstansen inte är tillgänglig. Glöm inte att publicera nyhetsbrevet och kontrollera att Publish-instansen körs.

## Skapa en upplevelse av nyhetsbrev {#creating-a-newsletter-experience}

>[!NOTE]
>
>E-postmeddelanden måste konfigureras via SGB-konfigurationen. Se [Konfigurerar e-postmeddelande.](/help/sites-administering/notification.md)

1. Välj din nya kampanj i den vänstra rutan eller dubbelklicka på den i den högra rutan.

1. Markera listvyn med ikonen:

   ![Ikon för listvy](do-not-localize/mcm_icon_listview-1.png)

1. Klicka **Nytt...**

   Du kan ange **Titel**, **Namn** och den typ av upplevelse som ska skapas, i det här fallet nyhetsbrevet.

   ![Dialogrutan Skapa upplevelse](assets/mcm_createnewsletter.png)

1. Klicka **Skapa**.

1. En ny dialogruta öppnas omedelbart. Här kan du ange egenskaper för nyhetsbrevet.

   The **Standardmottagarlista** är ett obligatoriskt fält eftersom detta utgör kontaktytan för nyhetsbrevet (se [Arbeta med listor](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#workingwithlists) om du vill ha mer information om listor).

   ![Dialogrutan Sidegenskaper](assets/mcm_newnewsletterdialog.png)

   * **Från namn**
Namn som ska visas som avsändare av nyhetsbrevet.

   * **Från adress**
E-postadress som ska visas som avsändare av nyhetsbrevet.

   * **Ämne**
Ämne för nyhetsbrevet.

   * **Svara till**
E-postadress som ska användas för svar på skickade nyhetsbrev.

   * **Beskrivning**
Beskrivning av nyhetsbrevet.

   * **I tid**
Tidpunkten när nyhetsbrevet ska skickas.

   * **Standardmottagarlista**
Standardlista som ska ta emot nyhetsbrevet.

   Dessa kan uppdateras i ett senare skede från **Egenskaper...** -dialogrutan.

1. Klicka **OK** att spara.

## Lägga till innehåll i nyhetsbrev {#adding-content-to-newsletters}

Du kan lägga till innehåll, inklusive dynamiskt innehåll, i nyhetsbrevet på samma sätt som i andra AEM. I Geometrixx finns det vissa komponenter i mallen Nyhetsbrev som du kan använda för att lägga till och ändra innehåll i nyhetsbrev.

1. Klicka på **Kampanjer** och dubbelklicka på det nyhetsbrev som du vill lägga till innehåll i eller redigera. Nyhetsbrevet öppnas.

1. Om komponenterna inte visas går du till designvyn och aktiverar de nödvändiga komponenterna (till exempel komponenterna i nyhetsbrevet) innan du börjar redigera.
1. Ange eventuell ny text, bilder eller andra komponenter. I exemplet med Geometrixx finns fyra komponenter: Text, Bild, Rubrik och 2 spalter. Nyhetsbrevet kan ha fler eller färre komponenter beroende på hur du konfigurerar det.

   >[!NOTE]
   >
   >Ni personaliserar nyhetsbrev med hjälp av variabler. I nyhetsbrevet Geometrixx finns variabler i komponenten Text. Värden för variablerna ärvs från informationen i användarprofilen.

   ![Redigera innehåll i nyhetsbrev](assets/mcm_newsletter_content.png)

1. Om du vill infoga variabler väljer du variabeln i listan och klickar på **Infoga**. Variabler fylls i från profilen.

## Personaliserar nyhetsbrev {#personalizing-newsletters}

Du kan personalisera nyhetsbrev genom att infoga fördefinierade variabler i Text-komponenten i nyhetsbreven i Geometrixx. Värden för variablerna ärvs från informationen i användarprofilen.

Du kan också simulera hur ett nyhetsbrev personaliseras genom att använda klientkontexten och läsa in en profil.

Så här anpassar du ett nyhetsbrev och simulerar hur det kommer att se ut:

1. I MCM öppnar du det nyhetsbrev som du vill anpassa inställningarna för.

1. Öppna den textkomponent som du vill anpassa.

1. Placera markören där du vill att variabeln ska visas och välj en variabel i listrutan och klicka på **Infoga**. Gör detta för så många variabler som behövs och klicka på **OK**.

   ![Lägga till variabler](assets/mcm_newsletter_variables.png)

1. Om du vill simulera hur variabeln kommer att se ut när den skickas trycker du på CTRL+ALT+c för att öppna klientkontexten och välja **Läs in**. Markera användaren i listan vars profil du vill läsa in och klicka på **OK**.

   Variablerna har fyllts i med informationen från profilen som du läste in.

   ![Testa variabler](assets/mc_newsletter_testvariables.png)

## Testa nyhetsbrev i olika e-postklienter {#testing-newsletters-in-different-e-mail-clients}

>[!NOTE]
>
>Innan du skickar nyhetsbrev bör du kontrollera OSGi-konfigurationen för Day CQ Link Externalizer på `https://localhost:4502/system/console/configMgr`.
>
>Som standard är parameterns värde `localhost:4502` och åtgärden kan inte slutföras om porten för den instans som körs ändras.

Växla mellan vanliga e-postklienter för att se hur nyhetsbrevet ser ut mot era leads. Som standard öppnas nyhetsbrevet utan att någon av e-postklienterna har valts.

För närvarande kan du visa nyhetsbrev i följande e-postklienter:

* Yahoo-post
* Gmail
* Hotmail
* Thunderfågel
* Microsoft Outlook 2007
* Apple Mail

Klicka på motsvarande ikon för att visa nyhetsbrevet i e-postklienten för att växla mellan olika klienter:

1. I MCM öppnar du det nyhetsbrev som du vill anpassa inställningarna för.

1. Klicka på en e-postklient i det övre fältet för att se hur nyhetsbrevet skulle se ut i klienten.

   ![Byta e-postklienter](assets/chlimage_1-119.png)

1. Upprepa det här steget för alla e-postklienter som du vill se.

   ![Ändra e-postklienter](assets/chlimage_1-120.png)

## Anpassa inställningar för nyhetsbrev {#customizing-newsletter-settings}

Även om bara behöriga användare kan skicka nyhetsbrev bör du anpassa följande:

* Ämnesraden, så att användare kan öppna ditt e-postmeddelande och även försäkra sig om att det inte kommer att sluta som skräppost.
* Från-adressen, till exempel `noreply@geometrixx.com`så att användarna får e-post från en angiven adress.

Så här anpassar du inställningar för nyhetsbrev:

1. I MCM öppnar du det nyhetsbrev som du vill anpassa inställningarna för.

   ![Öppna ett nyhetsbrev](assets/mcm_newsletter_open.png)

1. Överst i nyhetsbrevet klickar du på **Inställningar**.

   ![Redigera inställningar för nyhetsbrev](assets/mcm_newsletter_settings.png)
1. Ange **Från** e-postadress

1. Ändra **Ämne** om e-postmeddelandet, om det behövs.

1. Välj en **Standardmottagarlista** i listrutan.

1. Klicka **OK**.

   När du testar eller skickar nyhetsbrevet får mottagarna e-post med den angivna e-postadressen och det angivna ämnet.

## Nyhetsbrev om flygtestning {#flight-testing-newsletters}

Flygtestning är inte obligatoriskt, men innan du skickar ut ett nyhetsbrev kanske du vill testa det för att vara säker på att det ser ut som du vill ha det.

Med flygtester kan du göra följande:

* Titta på nyhetsbrevet i [alla avsedda klienter](#testing-newsletters-in-different-e-mail-clients).
* Verifiera att e-postservern är korrekt konfigurerad.
* Avgör om ditt e-postmeddelande flaggas som skräppost. (Se till att du tar med dig själv i listan över mottagare.)

>[!NOTE]
>
>Om du uppdaterar e-postleverantörer, gör ett flygtest eller skickar ett nyhetsbrev misslyckas dessa åtgärder om nyhetsbrevet inte publiceras till publiceringsinstansen först eller om publiceringsinstansen inte är tillgänglig. Glöm inte att publicera nyhetsbrevet och kontrollera att Publish-instansen körs.

Så här gör du för att testa nyhetsbrev:

1. Öppna det nyhetsbrev som du vill testa och skicka från MCM.

1. Överst i nyhetsbrevet klickar du på **Testa** att testa innan den skickas.

   ![Inställningar för att testa ett nyhetsbrev](assets/mcm_newsletter_testsettings.png)

1. Ange den testadress dit du vill att nyhetsbrevet ska skickas och klicka på **Skicka**. Om du vill ändra profilen läser du in en annan profil i klientkontexten. Det gör du genom att trycka på CTRL+ALT+c och välja Läs in och läsa in en profil.

## Skickar nyhetsbrev {#sending-newsletters}

>[!NOTE]
>
>Adobe planerar inte att ytterligare förbättra e-postspårningen av öppna meddelanden/studsar (som inte kan levereras) som skickas av AEM SMTP-tjänst.
>Rekommendationen är att använda [Adobe Campaign och integrationen med AEM](/help/sites-administering/campaign.md).

Du kan skicka ut ett nyhetsbrev från nyhetsbrevet eller från listan. Båda procedurerna beskrivs.

>[!NOTE]
>
>Innan du skickar nyhetsbrev bör du kontrollera OSGi-konfigurationen för Day CQ Link Externalizer på `https://localhost:4502/system/console/configMgr`.
>
>Som standard är parameterns värde `localhost:4502` och åtgärden kan inte slutföras om porten för den instans som körs ändras.

>[!NOTE]
>
>Om du uppdaterar e-postleverantörer, gör ett flygtest eller skickar ett nyhetsbrev misslyckas dessa åtgärder om nyhetsbrevet inte publiceras till publiceringsinstansen först eller om publiceringsinstansen inte är tillgänglig. Glöm inte att publicera nyhetsbrevet och kontrollera att Publish-instansen körs.

### Skicka nyhetsbrev från en kampanj {#sending-newsletters-from-a-campaign}

Så här skickar du ut ett nyhetsbrev inifrån kampanjen:

1. Öppna det nyhetsbrev som du vill skicka från MCM.

   >[!NOTE]
   >
   >Innan du skickar iväg nyhetsbrevet bör du kontrollera att du har anpassat ämnet och e-postadressen [anpassa inställningarna](#customizing-newsletter-settings).
   >
   >
   >[Flygtestning](#flight-testing-newsletters) nyhetsbrevet bör skickas innan det skickas.

1. Överst i nyhetsbrevet klickar du på **Skicka**. Guiden Nyhetsbrev öppnas.

1. Välj den lista som du vill få nyhetsbrevet i mottagarlistan och klicka på **Nästa**.

   ![Skicka ett nyhetsbrev](assets/mcm_newslettersend.png)

1. Installationen har slutförts. Klicka **Skicka** för att faktiskt skicka nyhetsbrevet.

   ![Bekräftelse på skickad nyhetsbrev](assets/mcm_newslettersendconfirm.png)

   >[!NOTE]
   >
   >Kontrollera att du är en av mottagarna så att du kan vara säker på att nyhetsbrevet har tagits emot.

### Skicka nyhetsbrev från en lista {#sending-newsletters-from-a-list}

Så här skickar du ut ett nyhetsbrev från en lista:

1. Klicka på **Listor** i den vänstra rutan.

   >[!NOTE]
   >
   >Innan du skickar iväg nyhetsbrevet bör du kontrollera att du har anpassat ämnet och e-postadressen [anpassa inställningarna](#customizing-newsletter-settings). Du kan inte testa ett nyhetsbrev om du skickar det från listan. Du kan [flygprov](#flight-testing-newsletters) om du skickar det från nyhetsbrevet.

1. Markera kryssrutan bredvid listan med leads som du vill skicka ett nyhetsbrev till.

1. I **verktyg** meny, välja **Skicka nyhetsbrev**. The **Skicka nyhetsbrev** öppnas.

   ![Konsol för nyhetsbrev](assets/mcm_newslettersendfromlist.png)

1. I **Nyhetsbrev** markerar du det nyhetsbrev som du vill skicka och klickar på **Nästa**.

   ![Dialogrutan Skicka nyhetsbrev](assets/mcm_newslettersenddialog.png)

1. Installationen har slutförts. Klicka **Skicka** om du vill skicka det markerade nyhetsbrevet till den angivna listan med leads.

   ![Skicka bekräftelse](assets/mcm_newslettersenddialog_confirmation.png)

   Nyhetsbrevet skickas till de valda mottagarna.

## Prenumerera på ett nyhetsbrev {#subscribing-to-a-newsletter}

I det här avsnittet beskrivs hur du prenumererar på ett nyhetsbrev.

### Prenumerera på ett nyhetsbrev {#subscribing-to-a-newsletter-1}

Så här prenumererar du på ett nyhetsbrev (med Geometrixx webbplats som exempel):

1. Klicka **Webbplatser** och navigera till Geometrixx **Verktygsfält** och öppna den.

   ![Exempel på prenumeration](assets/chlimage_1-121.png)

1. I Geometrixx Newsletter **Registrera dig** anger du din e-postadress och klickar på **Registrera dig**. Du prenumererar nu på nyhetsbrevet.
