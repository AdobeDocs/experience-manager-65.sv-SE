---
title: Genomgång av referenswebbplatser för Web.Gov och We.Finance
description: Använd fiktiva användare och grupper för att utföra AEM Forms-uppgifter med demopaketet We.Gov och We.Finance.
contentOwner: anujkapo
docset: aem65
exl-id: 288d5459-bc69-4328-b6c9-4b4960bf4977
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '2478'
ht-degree: 0%

---

# Genomgång av referenswebbplatser för Web.Gov och We.Finance {#we-gov-reference-site-walkthrough}

## Krav {#pre-requisites}

Konfigurera referensplatsen enligt beskrivningen i [Konfigurera referenswebbplatsen för Web.Gov och We.Finance](../../forms/using/forms-install-configure-gov-reference-site.md).

## Användarberättelse {#user-story}

* AEM Forms

   * Automated forms conversion
   * Redigering
   * Formulärdatamodeller/datakällor

* AEM Forms

   * Datainhämtning
   * (Valfritt) Dataintegrering (MS® Dynamics)
   * (Valfritt) Adobe Sign

* Arbetsflöde
* E-postmeddelanden
* (Valfritt) Kundkommunikation

   * Utskriftskanal
   * Webbkanal

* Adobe Analytics
* Integrering av datakällor

### Faktiska användare och grupper {#fictitious-users-and-groups}

Demonspaketet We.Gov innehåller följande inbyggda fiktiva användare:

* **Aya Tan**: Medborgare som är berättigade till en tjänst från en myndighet

![Fantastiska användare](/help/forms/using/assets/aya_tan_new.png)

* **George Lang**: Business Analyst för myndigheter

![Fantastiska användare](/help/forms/using/assets/george_lang.png)

* **Camila Santos**: Vi.Gov Agency CX Lead

![Fantastiska användare](/help/forms/using/assets/camila_santos.png)

Följande grupper ingår också:

* **Vi.Gov Forms-användare**

   * George Lang (medlem)
   * Camila Santos (medlem)

* **We.Gov-användare**

   * George Lang (medlem)
   * Camila Santos (medlem)
   * Aya Tan (medlem)

### Förklaring av termer i demoöversikt {#demo-overview-terms-legend}

1. **Personifiera**: Definierade användare och grupper i AEM.
1. **Knapp**: Färgad rektangel eller inringad pil för navigering.
1. **Klicka**: Så här kör du en åtgärd i användarartikeln.
1. **Länkar**: Högst upp på huvudmenyn på webbsidan We.Gov.
1. **Användarinstruktioner**: En uppsättning numeriska steg som ska följas när användaren navigerar i artikeln.
1. **Forms Portal**: *https://&lt;aemserver>:&lt;port>/content/we-gov/formsportal.html*
1. **Mobilvy**:We.Gov-användare som vill replikera en mobilvy med en webbläsare som har ändrat storlek.
1. **Skrivbordsvy**: We.gov användare kan se filmen på en bärbar eller stationär dator.
1. **Pre-screener Form**: Formulär på startsidan för webbsidan We.Gov.
1. **Adaptiv form**: Registreringsansökningsformulär för We.gov demo.

   *https://&lt;aemserver>:&lt;port>/content/forms/af/adobe-gov-forms/enrollment-application-for-health-benefits.html*

1. **Adobe Web.Gov Site**: *https://&lt;aemserver>:&lt;port>/content/we-gov/home.html*
1. **Inkorgen Adobe**: Placerad övre menyrad [Bell, ikon](assets/bell.svg) i AEM.

   *https://&lt;aemserver>:&lt;port>/aem/start.html*

1. **E-postklient**: Önskat sätt att visa e-postmeddelanden (Gmail, Outlook)
1. **CTA**: Uppmaning
1. **Navigera**: Om du vill hitta en specifik referenspunkt på webbläsarsidan.
1. **AFC**: AUTOMATED FORMS CONVERSION

## Automated forms conversion (Camila) {#automated-forms-conversion}

**Detta avsnitt**: Camila the CX Lead har ett PDF-baserat formulär som användes som en del av en pappersbaserad process. Som en del av en moderniseringssatsning vill Camila använda det här PDF-formuläret för att automatiskt skapa en modern Adaptiv Forms.

### Automated forms conversion - We.GOV (Camila) {#automated-forms-conversion-wegov}

1. Navigera till *https://&lt;aemserver>:&lt;port>/aem/start.html*

1. Logga in med:
   * **Användare**: camila.santos
   * **Lösenord**: lösenord
1. På huvudsidan väljer du Forms > Forms &amp; Documents > AEM Forms We.gov Forms > AFC.
1. Camila överför PDF till AEM Forms.

   ![Överför formulär](assets/aftia-upload-form.jpg)

1. Camilla markerar sedan PDF-formuläret och klickar **Starta automatisk konvertering** för att starta konverteringsprocessen. Du kan behöva klicka **Skriv över konvertering** om du har konverterat formuläret.

   >[!NOTE]
   >
   >Inställningarna i AFC är förkonfigurerade för slutanvändaren, vilket betyder att de inte ska ändras.

   * **Valfritt**: Om du vill använda temat Accessible Ultramarine klickar du bara på Specificera ett adaptivt formulärtema och väljer temat Accessible-Ultramarine som visas i listan med alternativ.

   ![Starta konvertering](assets/aftia-start-conversion.jpg)

   ![Ultramarintema](assets/aftia-upload-conversion-settings.jpg)

   Statusen för Procent färdigt visas under konverteringen. När statusen visas **Konverterad** klickar du på **output** markerar du det anpassade formuläret och klickar på **Redigera** för att öppna det konverterade formuläret.

1. Camilla granskar sedan formuläret och ser till att alla fält finns

   ![Granska konvertering](assets/aftia-review-conversion.jpg)

1. Camilla börjar sedan redigera formuläret och väljer Rotpanel > Redigera (skiftnyckel) > väljer Tabbar överst på panellayoutmenyn > markerar kryssrutan.

   ![Granska egenskaper](assets/aftia-review-properties.jpg)

1. Camilla lägger sedan till alla CSS- och fältändringar som behövs för att producera slutprodukten.

   ![Lägg till CSS](assets/aftia-add-css.jpg)

### Formulärdatamodell och datakällor (Camila) {#data-sources}

**Detta avsnitt**: När dokumentet har konverterats och skapat ett adaptivt formulär måste Camila ansluta det adaptiva formuläret till en datakälla.

1. Camila öppnar egenskaperna för formuläret som har konverterats i [Automated forms conversion - We.GOV](#automated-forms-conversion-wegov).

1. Camila väljer sedan Formulärmodell > Väljer formulärdatamodell i listrutan Välj från > Väljer We.gov för registrering i listan över alternativ.

1. Klicka på Spara och stäng.

   ![FDM-markering](assets/aftia-select-fdm.jpg)

1. Camila klickar på **output** väljer anpassat formulär och klickar på **Redigera** för att öppna det ifyllda formuläret We.Gov.
1. Camila väljer ett anpassat formulärfält och klickar ![Ikonen Konfigurera](assets/configure-icon.svg) och skapar bindning med formulärdatamodellenheter med **Bindningsreferens** fält. Camila upprepar det här steget för alla fält i det adaptiva formuläret.

### Testning av formulärtillgänglighet (Camila) {#form-accessibility-testing}

Camila kontrollerar också att det skapade innehållet är korrekt och fullt tillgängligt enligt företagsstandarder.

1. Camila klickar på **output** väljer anpassat formulär och klickar på **Förhandsgranska** för att öppna det ifyllda formuläret We.Gov.

1. Öppnar fliken Granska i Chrome Developer Tool.

1. Utför en tillgänglighetskontroll för att validera det adaptiva formuläret.

   ![Tillgänglighetskontroll](assets/aftia-accessibility.jpg)

## Demo av mobilvyn Adaptiv form (Aya) {#mobile-view-demo}

**Detta avsnitt måste utföras före demonstrationen.**

**Användarinstruktioner:**

1. Navigera till: *https://&lt;aemserver>:&lt;port>/content/we-gov/home.html*
1. Logga in med:

   1. **Användare**: aya.tan
   1. **Lösenord**: lösenord

1. Ändra storlek på webbläsarfönstret eller använd webbläsarens emulator för att replikera en mobilenhetsstorlek.

### Webbplats för Web.Gov (Aya) {#aya-user-story-we-gov-website}

![Fantastiska användare](/help/forms/using/assets/aya_tan_new-1.png)

**Detta avsnitt**: Aya är medborgare och hör från en vän som kan ha rätt att få en tjänst från en myndighet. Aya navigerar till webbsidan We.Gov från sin mobiltelefon för att lära sig mer om tjänster som hon är berättigad till.

### We.GOV Pre-Screener (Aya) {#aya-user-story-we-gov-pre-screener}

Svar på några frågor som bekräftar hennes behörighet genom att fylla i ett kort anpassningsbart formulär på mobiltelefonen.

**Användarinstruktioner:**

1. Gör ett val i varje listruta.

   >[!NOTE]
   >
   >Om användaren tjänar mer än 200 000 USD/år är de inte berättigade.

1. Klicka **Är jag berättigad?**.
1. Klicka **Använd nu** för att fortsätta.

   ![Länken Använd nu](/help/forms/using/assets/apply_now_link.png)

### Adaptiv form (AYA) {#aya-user-story-we-gov-adaptive-form}

Aya får reda på att hon är berättigad och börjar fylla i sin ansökan för att få service på sin mobila enhet.

Du måste granska vissa dokument hemma innan hon kan fylla i serviceförfrågningen. Hon sparar och avslutar programmet från sin mobila enhet.

**Användarinstruktioner:**

1. Fyll i de grundläggande informationsfälten, följande är obligatoriska fält och listrutor:

   1. Grundläggande information

      1. Förnamn
      1. Efternamn
      1. DOB
      1. E-post

1. Använd följande **dynamisk logik** för att demonstrera den dynamiska funktionen med **Familjestatus** listruta:

   1. **Enkelt**: Visa nästa panel
   1. **Gift**: Visa äktenskapsberoende panel
   1. **Skilt**: Visa nästa panel
   1. **Ändrad**: Visa nästa panel
   1. **Har du barn?**: (Ja/Nej) om du vill visa den underordnade beroende panelen.

      1. (Lägg till/ta bort) om du vill lägga till/ta bort flera underordnade paneler.

1. Klicka på högerpilen i det grå menyfältet.
1. Klicka på knappen Spara längst ned.

   ![Adaptiv formulärinformation](/help/forms/using/assets/adaptive_form.png)

## Demo {#desktop-demo}

**Detta avsnitt:** Hemma har Aya hittat den information hon behövde och återupptar programmet från sin dator. Aya navigerar till Forms-portalen online för att återuppta sin tillämpning. Med viss enkel anpassning kan man också automatiskt generera och mejla en länk för att återuppta ansökningen.

### Fortsatt adaptiv form (AYA) {#aya-user-story-continued-adaptive-form}

**Användarinstruktioner:**

1. Navigera till *https://&lt;aemserver>:&lt;port>/content/we-gov/home.html*
1. Välj **Onlinetjänster**.
1. På panelen Utkast till Forms väljer du det befintliga programmet för hälsoförmåner.

   ![Registreringsprogram för hälsoförmåner](/help/forms/using/assets/enrollment_application.png)

   Utseendet och känslan är desamma, och hon behöver inte skriva in några data igen.

   **Användarinstruktioner:**

1. Högerklicka på Circle CTA för att gå till nästa avsnitt.

   ![CTA för högercirkel](/help/forms/using/assets/right_circle_cta_new.png)

   Formuläret fylls i fram till den punkt där Aya senast anmälde sig. Aya har angett alla hennes uppgifter och är redo att skicka in.

   ![Skicka det anpassade formuläret](/help/forms/using/assets/submit_adaptive_form.png)

   >[!NOTE]
   >
   >När Aya fyller i telefonnummerfältet måste hon fylla i det som ett kontinuerligt 11-siffrigt nummer utan bindestreck, mellanslag eller bindestreck.

   När Aya har skickat in en sida med tack. Aya kan också få ett e-postmeddelande som hon kan öppna för att signera urkunder elektroniskt med Adobe Sign.

### Tillval: Adobe Sign (Aya) {#adobe-sign}

**Användarinstruktioner:**

1. Navigera till din e-postklient och hitta Adobe Sign e-postadress.
1. Klicka på länken till Adobe Sign.

   ![Adobe-signeringslänk](/help/forms/using/assets/adobe_sign_link.png)

**Användarinstruktioner:**

1. Kontrollera **Jag håller med**.
1. Klicka **Acceptera**.
1. Rulla längst ned i det granskade dokumentet.
1. Klicka på den markerade gula fliken så att du kan signera dokumentet.

   ![Signera dokumentet](/help/forms/using/assets/sign_document_new.png) ![Signera testdokumentet](/help/forms/using/assets/sign_test_document.png)

## Statlig agent (George) {#government-agent-george}

![Government Agent George](/help/forms/using/assets/george_lang-1.png)

**Detta avsnitt:** George är affärsanalytiker på den statliga myndigheten Aya begär en tjänst från. George har en enda kontrollpanel där han kan se alla serviceförfrågningar som han har tilldelats för granskning.

### AEM Inkorg (George) {#george-user-story-aem-inbox}

**Användarinstruktioner:**

1. Navigera till *https://&lt;aemserver>:&lt;port>/aem/start.html*
1. Klicka på användarikonen (övre högra hörnet) och använd **Logga ut** eller **Personifiera som** om du är inloggad med en administrativ användare.

   1. Logga in med:

      1. **Användare:** george.lang
      1. **Lösenord:** lösenord

   1. Eller personifiera:

      1. Typ `George` i **Personifiera som** fält.

      1. Klicka OK för att personifiera.

1. Klicka på ikonen Meddelande (klockan) i det övre högra hörnet.
1. Klicka **Visa alla** för att gå till Inkorgen.
1. Öppna den senaste **Granskning av program för hälsoförmåner** uppgift.

   ![Granskning av program för hälsoförmåner](/help/forms/using/assets/health_benefits.png)

### Valfritt: AEM Inbox &amp; MS® Dynamics (George) {#george-user-story-aem-inbox-and-ms-dynamics}

Tack vare dataintegreringar och automatiserade arbetsflöden visas Ayas program tillsammans med en CRM-post som automatiskt har genererats när data skickades.

**Användarinstruktioner:**

1. Öppna och inspektera det skrivskyddade anpassningsbara formuläret.
1. Klicka **Öppna MS® Dynamics** för att öppna MS® Dynamics-posten i ett nytt fönster.
1. I CRM visas all information som kan uppdateras.

   1. Du kan också lägga till några granskningsanteckningar direkt i Dynamics.

1. Stäng och gå tillbaka till AEM Inkorg.

   ![MS Dynamics-post](/help/forms/using/assets/ms_dynamics.png)

### Tillbaka till AEM Inkorg (George) {#george-user-story-back-to-aem-inbox}

George godkänner Ayas ansökan, och tack vare ett befintligt automatiserat arbetsflöde skickas även ett bekräftelsemeddelande via e-post till Aya.

**Användarinstruktioner:**

1. Navigera till det övre vänstra hörnet och klicka **Godkänn** för att godkänna ansökan.
1. I modala medier kan du lämna ett meddelande till CX-leadet.
1. Klicka på Klar.
1. (Medborgarroll) Öppna din e-postklient för att visa e-postmeddelandet som skickats till Aya.

   ![Visa e-postmeddelandet som skickats till Aya](/help/forms/using/assets/email_client.png)

## CX Lead (Camila) {#cx-lead-camila}

![Camila (CX lead)](/help/forms/using/assets/camila_santos-1.png)

**Detta avsnitt:** Camila på CX Lead ringer ett välkomstsamtal med Aya för att förklara hur hon använder de myndighetstjänster hon är godkänd för.

### (Valfritt) AEM Inbox &amp; MS® Dynamics {#camila-user-story-aem-inbox-ms-dynamics}

**Användarinstruktioner:**

1. Navigera till *https://&lt;aemserver>:&lt;port>/aem/start.html*
1. Klicka på användarikonen (övre högra hörnet) och använd **Logga ut** eller **Personifiera som** om du är inloggad med en administrativ användare.

   1. Logga in med:

      1. **Användare**: camila.santos
      1. **Lösenord**: lösenord

   1. Eller personifiera:

      1. Typ `Camila` i **Personifiera som** fält.

      1. Klicka OK för att personifiera.

1. Klicka på ikonen Meddelande (klockan) i det övre högra hörnet.
1. Klicka **Visa alla** för att gå till Inkorgen.
1. Öppna den senaste **Nytt godkännande av kontakt** uppgift.

![Nytt godkännande av kontakt](/help/forms/using/assets/new_contact_approval.png)

**(Valfritt) Användarinstruktioner:**

1. Öppna och inspektera det skrivskyddade anpassningsbara formuläret.
1. Klicka **Öppna MS® Dynamics** för att öppna MS® Dynamics-posten i ett nytt fönster.
1. I CRM kan du se all information som kan uppdateras.

   1. Du kan också lägga till en samtalsaktivitet direkt i Dynamics.
   1. Öppna **Verksamhet** -avsnitt.
   1. Klicka **Nytt telefonsamtal**.
   1. Lägg till telefonsamtalsinformation.
   1. Spara och stäng fönstret.

1. Gå tillbaka i AEM, navigera till det övre vänstra hörnet och klicka på **Skicka** för att lämna in ansökan.
1. I modala medier kan du lämna ett meddelande.
1. Klicka på Klar.

   ![Fliken Aktiviteter](/help/forms/using/assets/activities_tab.png) ![Bekräfta ny kontakt](/help/forms/using/assets/confirm_new_contact.png)

## (Valfritt) Välkomstpaket (Aya) {#welcome-kit-citizen-aya}

**Detta avsnitt:** Aya får ett e-postmeddelande med en länk till ett interaktivt meddelande som sammanfattar hennes fördelar och även innehåller formulärfält som ska fyllas i. Med PDF Benefits Statement bifogat och länk till interaktivt kommunikationsbrev i e-postmeddelandet (med samma tema/varumärke som det interaktiva meddelandet).

### E-postklientmeddelande (AYA) {#aya-user-story-email-client}

**Användarinstruktioner:**

1. Leta reda på och öppna e-postmeddelandet om välkomstpaketet.
1. Bläddra till den bifogade PDF-filen längst ned på sidan.
1. Klicka för att öppna den bifogade filen PDF.
1. Bläddra tillbaka i e-postklienten och klicka **Visa välkomstkit online**.

   1. Då öppnas webbkanalversionen av samma dokument.

1. En snabb referens till PDF direkt:

   *https://&lt;aemserver>:&lt;port>/aem/formdetails.html/content/dam/formsanddocuments/adobe-gov-forms/welcome-handbook/we-gov-welcome-handbook*

1. En snabb referens till IC direkt:

   *https://&lt;aemserver>:&lt;port>/content/dam/formsanddocuments/adobe-gov-forms/welcome-handbook/we-gov-welcome-handbook/jcr:content?channel=web&amp;mode=preview&amp;wcmmode=disabled*

   ![Handbok för välkomstförmåner](/help/forms/using/assets/welcome_benefits_handbook.png) ![Interaktiv kommunikationslänk](/help/forms/using/assets/interactive_communication.png)

## Påminnelse om förnyelse - medborgare (Aya) {#renewal-reminder-citizen-aya}

**Detta avsnitt:** Camila schemalägger också en påminnelse så ett år senare. (Arbetsflödessteg som automatiserar/kör och skickar e-post).

### E-postklientmeddelande (AYA) {#aya-user-story-email-client-updated}

**Användarinstruktioner:**

1. Navigera till din e-postklient.
1. Leta reda på och öppna e-postmeddelandet med en påminnelse om förnyelse.
1. Klicka **Skicka ett nytt program** så att du kan öppna det anpassade formuläret.

   1. Detta avsnitt är avsiktligt tomt för att stödja förifyllning av data i fas 2.

   ![Påminnelse om förnyelse - e-post](/help/forms/using/assets/renewal_reminder_email.png)

## (Valfritt) Formulärdatamodell (Camila) {#form-data-model}

**Detta avsnitt**: Camila navigerar till AEM Forms Data Integrations där hon kan göra ett snabbt test för att se att informationen som skickas till den externa datakällan via integrering med formulärdatamodellen verkligen finns.

### Formulärdatamodell (Camila) {#form-data-model-camila}

**Detta avsnitt**: Camila navigerar till sidan Datakällor för att validera data som servern har replikerat i Derby-databasen.

1. När användarupplevelsen är klar och användarinlämningen är klar går Camila till fliken Datakällor i AEM Forms (**Forms** > **Dataintegrering**)

1. Camila väljer sedan AEM Forms We.gov FDM och redigerar sedan **We.gov Registrering - FDM**.

1. Camila markerar sedan **Kontakt** > **Läs tjänsten** som ska testas.

   ![Läsningstjänst](assets/aftia-contact-read-service.jpg)

1. Camila förser sedan testtjänsten med ett kontakt-ID och klickar sedan **Testa**. Exempel: 1 eller 2, om du har skickat in formuläret. Om du inte har skickat formuläret returneras inga data.

   ![Läsningstjänst](assets/aftia-test-service.jpg)

1. Camila kan sedan validera att data har infogats i datakällan.

   * Uppgifterna i Derby DS liknar följande format:

   ```xml
      [
         {
         "ADDRESS_COUNTRY": "USA",
         "LAST_NAME": "Tan",
         "ADDRESS_CITY": "New York",
         "FIRST_NAME": "Aya",
         "ADDRESS_STATE": "AL",
         "ADDRESS_LINE1": "123 Street crescent",
         "GENDER_CODE": "2",
         "ADDRESS_LINE2": "123 Street crescent",
         "ADDRESS_POSTAL_CODE": "90210",
         "BIRTH_DATE": "1991-12-12",
         "CONTACT_ID": 1,
         "MIDDLE_NAME": "M",
         "HAS_CHILDREN_CODE": "0"
         }
   ]
   ```

## (Valfritt) Analytics (Camila) {#analytics-cx-lead-camila}

**Detta avsnitt:** Camila navigerar till en kontrollpanel där hon kan se nyckeltal för olika myndigheter, t.ex. procent av medborgarna som börjar fylla i ett formulär och överge det, genomsnittlig tid från att begära att få lämna in det till svar på ansökan om godkännande/avslag, och engagemangsstatistik för de förmånsböcker hon har skickat till medborgarna.

### Adobe Analytics Sites Reporting (Camila) {#camila-reviews-sites-reporting-we-gov-adobe-analytics}

1. Navigera till *https://&lt;aemserver>:&lt;port>/sites.html/content*
1. Välj **AEM Forms Web.Gov Site** för att visa webbplatssidorna.
1. Markera en av webbplatssidorna (till exempel Hem) och välj **Analytics och Recommendations**.

   ![Analyser och rekommendationer](/help/forms/using/assets/analytics_recommendation.jpg)

1. På den här sidan ser du hämtad information från Adobe Analytics som gäller för AEM Sites-sidan (Obs! Den här informationen uppdateras regelbundet från Adobe Analytics och visas inte i realtid).

   ![Adobe Analytics key metrics](/help/forms/using/assets/analytics_key_metrics.jpg)

1. Tillbaka på sidan för sidvisning (som du kom åt i steg 3.) kan du även visa sidvisningsinformationen genom att ändra visningsinställningen så att objekt i **Listvy**.
1. Leta reda på **Visa** nedrullningsbar meny och välj **Listvy**.

   ![Listvy i listrutan Visa](/help/forms/using/assets/list_view_view_dropdown.jpg)

1. Välj **Visningsinställning** och välj de kolumner som du vill visa i **Analyser** -avsnitt.

   ![Konfigurera visning av kolumner](/help/forms/using/assets/view_setting_analytics.jpg)

1. Klicka **Uppdatera** för att göra de nya kolumnerna tillgängliga.

   ![Göra nya kolumner tillgängliga](/help/forms/using/assets/new_columns_available.jpg)

### Adobe Analytics Forms Reporting (Camila) {#camila-reviews-forms-reporting-we-gov-adobe-analytics}

1. Navigera till

   *https://&lt;aemserver>:&lt;port>/aem/forms.html/content/dam/formsanddocuments/adobe-gov-forms*

1. Välj **Registreringsprogram för hälsofördelar** adaptiv form och välj **Analysrapport** alternativ.

   ![Registreringsprogram för hälsoförmåner](/help/forms/using/assets/analytics_report_benefits.jpg)

1. Vänta tills sidan har lästs in och visa analysrapportdata.

   ![Data för analysrapport](/help/forms/using/assets/analytics_report_data_updated.jpg)
