---
title: Genomgång av vår Gov-referenswebbplats
seo-title: Genomgång av vår Gov-referenswebbplats
description: Använd fiktiva användare och grupper för att utföra AEM Forms-åtgärder med hjälp av demopaketet We.Gov.
seo-description: Använd fiktiva användare och grupper för att utföra AEM Forms-åtgärder med hjälp av demopaketet We.Gov.
uuid: 797e301a-36ed-4bae-9ea8-ee77285c786d
contentOwner: anujkapo
discoiquuid: ddb3778b-be06-4cde-bc6e-0994efa42b18
docset: aem65
translation-type: tm+mt
source-git-commit: 3226edb575de3d9f8bff53f5ca81e2957f37c544

---


# Genomgång av vår Gov-referenswebbplats{#we-gov-reference-site-walkthrough}

## Krav {#pre-requisites}

Konfigurera referenswebbplatsen enligt beskrivningen i [Konfigurera och konfigurera referenswebbplatsen](../../forms/using/forms-install-configure-gov-reference-site.md)Web.Gov.

## Användarberättelse {#user-story}

* AEM-formulär

   * Datainhämtning
   * Dataintegrering (MS Dynamics)
   * Adobe Sign

* Arbetsflöde
* Kundkommunikation

   * Utskriftskanal
   * Webbkanal

* Adobe Analytics

### Faktiska användare och grupper {#fictitious-users-and-groups}

Demonspaketet We.Gov innehåller följande inbyggda fiktiva användare:

* **Aya Tan**: Medborgare som är berättigad till en tjänst från en myndighet

![Fantastiska användare](/help/forms/using/assets/aya_tan_new.png)

* **George Lang**: Business Analyst för myndigheter

![Fantastiska användare](/help/forms/using/assets/george_lang.png)

* **Camila Santos**: Vi.Gov Agency CX Lead

![Fantastiska användare](/help/forms/using/assets/camila_santos.png)

Följande grupper ingår också:

* **Användare av webbformulär**

   * George Lang (medlem)
   * Camila Santos (medlem)

* **We.Gov-användare**

   * George Lang (medlem)
   * Camila Santos (medlem)
   * Aya Tan (medlem)

### Förklaring av termer i demoöversikt {#demo-overview-terms-legend}

1. **Personifiera**: Definierade användare och grupper i AEM-demo.
1. **Knapp**: Färgad rektangel eller inringad pil för navigering.
1. **Klicka**: Så här kör du en åtgärd i användarartikeln.
1. **Länkar**: Finns högst upp på huvudmenyn på webbplatsen We.Gov.
1. **Användarinstruktioner**: En uppsättning numeriska steg som du kan följa när du navigerar i användarens berättelse.
1. **Formulärportal**: *https://&lt;aemserver>:&lt;port>/content/we-gov/formsportal.html*
1. **Mobilvy**:We.Gov-användare som vill replikera en mobilvy med en ny webbläsare.
1. **Skrivbordsvy**: Vi.gov-användare kan se en demo på en bärbar eller stationär dator.
1. **Pre-screener Form**: Formulär på startsidan för webbsidan We.Gov.
1. **Adaptiv form**: Anmälningsansökningsformulär för Web.gov demo.

   *https://&lt;aemserver>:&lt;port>/content/forms/af/adobe-gov-forms/enrollment-application-for-health-benefits.html*

1. **Adobe Web.Gov Site**: *https://&lt;aemserver>:&lt;port>/content/we-gov/home.html*
1. **Adobe Inbox**: Bell-ikon [på den översta menyraden finns] på AEM-serverdelen.

   *https://&lt;aemserver>:&lt;port>/aem/start.html*

1. **E-postklient**: Önskat sätt att visa e-postmeddelanden (Gmail, Outlook)
1. **CTA**: Uppmaning
1. **Navigera**: Om du vill hitta en specifik referenspunkt på webbläsarsidan.

## Mobil vy - demo {#mobile-view-demo}

**Detta avsnitt måste utföras före demonstrationen.**

**Användarinstruktioner:**

1. Navigera till: *https://&lt;aemserver>:&lt;port>/content/we-gov/home.html*
1. Logga in med:

   1. **Användare**: aya.tan
   1. **Lösenord**:lösenord

1. Ändra storlek på webbläsarfönstret eller använd webbläsarens emulator för att replikera en mobilenhetsstorlek.

### Aya User Story (webbsidan We.Gov) {#aya-user-story-we-gov-website}

![Fantastiska användare](/help/forms/using/assets/aya_tan_new-1.png)

**Detta avsnitt**: Aya är medborgare. Hon hör från en vän att hon kan vara berättigad till en tjänst från en myndighet. Aya navigerar till webbsidan We.Gov från sin mobiltelefon för att lära sig mer om tjänster som hon är berättigad till.

### Aya User Story (We.Gov pre-screener) {#aya-user-story-we-gov-pre-screener}

Svar på några frågor som bekräftar hennes behörighet genom att fylla i ett kort anpassningsbart formulär på mobiltelefonen.

**Användarinstruktioner:**

1. Gör ett val i varje listruta.

   1. Obs! Om användaren tjänar mer än 200 000 USD/år är de inte berättigade.

1. Klicka på&quot;**Är jag berättigad?**” button.
1. Klicka på knappen &quot;**Tillämpa nu**&quot; för att fortsätta.

   ![Länken Använd nu](/help/forms/using/assets/apply_now_link.png)

### Aya User Story (anpassningsbart webbformulär) {#aya-user-story-we-gov-adaptive-form}

Aya får reda på att hon är berättigad och börjar fylla i sin ansökan för att få service på sin mobila enhet.

Du måste granska vissa dokument hemma innan hon kan slutföra tjänstbegäran. Hon sparar och avslutar programmet.

**Användarinstruktioner:**

1. Fyll i de grundläggande informationsfälten, följande är obligatoriska fält och listrutor:

   1. Grundläggande information

      1. Förnamn
      1. Mellannamn
      1. Efternamn
      1. Önskat namn
      1. DOB
      1. Kön
   1. Kontaktinformation

      1. Gatuadress
      1. Ort
      1. Telefonnummer
      1. Postnummer
      1. E-post
      1. Läge
   1. Martialstatus

      1. Familjestatus



1. Använd följande **dynamiska logik** för att demonstrera den dynamiska funktionen i listrutan **Familjestatus** :

   1. **En**: Visa nästa dockpanel
   1. **Gift**: Visa äktenskapsberoende panel
   1. **Skilt**: Visa nästa dockpanel
   1. **Ändvis**: Visa nästa dockpanel
   1. **Har du barn?**: (Ja/Nej) om du vill visa den underordnade beroende panelen.

      1. (Lägg till/ta bort) om du vill lägga till/ta bort flera underordnade paneler.

1. Klicka på högerpilen i det grå menyfältet.
1. Klicka på knappen Spara längst ned.

   ![Adaptiv formulärinformation](/help/forms/using/assets/adaptive_form.png)

## Demo {#desktop-demo}

**** Detta avsnitt: Hemma har Aya hittat den information hon behövde och återupptar programmet från sin dator. Gå till onlineformulärportalen och återuppta hennes ansökan. Med viss enkel anpassning kan man också automatiskt generera och mejla en länk för att återuppta ansökningen.

### Aya User Story (forts. adaptive form) {#aya-user-story-continued-adaptive-form}

**Användarinstruktioner:**

1. Gå till *https://&lt;aemserver>:&lt;port>/content/we-gov/home.html*
1. Välj klicka på&#x200B;**Onlinetjänster** i navigeringsfältet.
1. På panelen Utkast till formulär väljer du det befintliga registreringsprogrammet för hälsoförmåner.

   ![Registreringsprogram för hälsoförmåner](/help/forms/using/assets/enrollment_application.png)

   Utseendet och känslan är desamma, och hon behöver inte ange några data igen.

   **Användarinstruktioner:**

1. Klicka på höger cirkel CTA för att gå till nästa avsnitt.

   ![CTA för högercirkel](/help/forms/using/assets/right_circle_cta_new.png)

   Formuläret fylls i fram till den punkt där Aya senast fyllde i. Aya har angett alla hennes uppgifter och är redo att skicka in.

   ![Skicka det anpassade formuläret](/help/forms/using/assets/submit_adaptive_form.png)

   När Aya har skickat in ett e-postmeddelande som hon öppnar och är redo att signera elektroniskt med Adobe Sign.

**Användarinstruktioner:**

1. Efter överföring visas sidan Tack.
1. Navigera till din e-postklient och hitta e-postadressen till Adobe Sign.
1. Klicka på länken till Adobe Sign.

   ![Länk till Adobe Sign](/help/forms/using/assets/adobe_sign_link.png)

**Användarinstruktioner:**

1. Markera rutan &quot;**Jag godkänner**&quot;.
1. Klicka på&#x200B;**Godkänn**.
1. Rulla längst ned i det granskade dokumentet.
1. Klicka på den markerade gula fliken för att signera dokumentet.

   ![Signera dokumentet](/help/forms/using/assets/sign_document_new.png) ![Signera testdokumentet](/help/forms/using/assets/sign_test_document.png)

## Statlig agent (George) {#government-agent-george}

![Government Agent George](/help/forms/using/assets/george_lang-1.png)

**** Detta avsnitt: George är affärsanalytiker på den statliga myndigheten Aya begär en tjänst från. George har en enda kontrollpanel där han kan se alla serviceförfrågningar som han har tilldelats för granskning.

### George User Story (AEM inbox) {#george-user-story-aem-inbox}

**Användarinstruktioner:**

1. Gå till *https://&lt;aemserver>:&lt;port>/aem/start.html*
1. Klicka på användarikonen (övre högra hörnet) och använd menyalternativet **Logga ut** eller **Personifiera som** om du är inloggad med en administrativ användare.

   1. Logga in med:

      1. **** Användare: george.lang
      1. **** Lösenord:lösenord
   1. Eller personifiera:

      1. Skriv&quot;**George**&quot; i fältet&quot;**Personifiera som**&quot;.

      1. Klicka OK för att personifiera.


1. Klicka på ikonen Meddelande (klockan) i det övre högra hörnet.
1. Klicka på&#x200B;**Visa alla** för att gå till Inkorgen.
1. Öppna den senaste aktiviteten &quot;**Health Benefits Application Review**&quot; i Inkorgen.

   ![Granskning av program för hälsoförmåner](/help/forms/using/assets/health_benefits.png)

### George User Story (AEM inbox och MS Dynamics) {#george-user-story-aem-inbox-and-ms-dynamics}

Tack vare dataintegreringar och automatiserade arbetsflöden visas Ayas program tillsammans med en CRM-post som automatiskt har genererats när data skickades.

**Användarinstruktioner:**

1. Öppna och inspektera det skrivskyddade anpassningsbara formuläret.
1. Klicka på knappen &quot;**Öppna MS Dynamics**&quot; för att öppna MS Dynamics-posten i ett nytt fönster.
1. I CRM kan du se att all information kan uppdateras

   1. Du kan också lägga till några granskningsanteckningar direkt i Dynamics.

1. Stäng och gå tillbaka till AEM Inbox.

   ![MS Dynamics-post](/help/forms/using/assets/ms_dynamics.png)

### George User Story (tillbaka till AEM Inbox) {#george-user-story-back-to-aem-inbox}

George godkänner Ayas ansökan, och tack vare ett befintligt automatiserat arbetsflöde skickas även ett bekräftelsemeddelande via e-post till Aya.

**Användarinstruktioner:**

1. Navigera till det övre vänstra hörnet och klicka på&#x200B;**Godkänn** för att godkänna programmet.
1. I modala medier kan du lämna ett meddelande till CX-leadet.
1. Klicka på Klar.
1. (Medborgarroll) Öppna din e-postklient för att visa e-postmeddelandet som skickats till Aya.

   ![Visa e-postmeddelandet som skickats till Aya](/help/forms/using/assets/email_client.png)

## CX Lead (Camila) {#cx-lead-camila}

![Camila (CX lead)](/help/forms/using/assets/camila_santos-1.png)

**** Detta avsnitt: Camila på CX Lead ringer ett välkomstsamtal med Aya för att förklara hur man använder de myndighetstjänster hon har godkänts för.

### Camila User Story (AEM inbox &amp; MS Dynamics) {#camila-user-story-aem-inbox-ms-dynamics}

**Användarinstruktioner:**

1. Gå till *https://&lt;aemserver>:&lt;port>/aem/start.html*
1. Klicka på användarikonen (övre högra hörnet) och använd menyalternativet **Logga ut** eller **Personifiera som** om du är inloggad med en administrativ användare.

   1. Logga in med:

      1. **Användare**: camila.santos
      1. **Lösenord**:lösenord
   1. Eller personifiera:

      1. Skriv&quot;**Camila**&quot; i fältet&quot;**Impersonate as**&quot;.

      1. Klicka OK för att personifiera.


1. Klicka på ikonen Meddelande (klockan) i det övre högra hörnet.
1. Klicka på&#x200B;**Visa alla** för att gå till Inkorgen.
1. Öppna den senaste aktiviteten&quot;**Nytt kontaktgodkännande**&quot; i Inkorgen.

   ![Nytt godkännande av kontakt](/help/forms/using/assets/new_contact_approval.png)

   **Användarinstruktioner:**

1. Öppna och inspektera det skrivskyddade anpassningsbara formuläret.
1. Klicka på knappen &quot;**Öppna MS Dynamics**&quot; för att öppna MS Dynamics-posten i ett nytt fönster.
1. I CRM kan du se att all information kan uppdateras

   1. Du kan också lägga till en ny samtalsaktivitet direkt i Dynamics.
   1. Öppna avsnittet **Verksamheter**.
   1. Klicka på alternativet&quot;**Nytt telefonsamtal**&quot;.
   1. Lägg till telefonsamtalsinformation.
   1. Spara och stäng fönstret.

1. I AEM går du till det övre vänstra hörnet och klickar på&#x200B;**Skicka** för att skicka programmet.
1. I modala medier kan du lämna ett meddelande.
1. Klicka på Klar.

   ![Fliken](/help/forms/using/assets/activities_tab.png) Aktiviteter ![Bekräfta ny kontakt](/help/forms/using/assets/confirm_new_contact.png)

## Welcome Kit-medborgare (Aya) {#welcome-kit-citizen-aya}

**** Detta avsnitt: Aya får ett e-postmeddelande med en länk till ett interaktivt meddelande som sammanfattar hennes fördelar och även innehåller formulärfält som ska fyllas i. Med PDF-förmånsutdrag bifogat och länk till interaktivt brev i e-postmeddelandet (med samma tema/varumärke som det interaktiva meddelandet).

### Aya User Story (e-postklient) {#aya-user-story-email-client}

**Användarinstruktioner:**

1. Leta reda på och öppna e-postmeddelandet om välkomstpaketet.
1. Bläddra till bifogad PDF-fil längst ned på sidan.
1. Klicka för att öppna den bifogade PDF-filen.
1. Bläddra tillbaka i e-postklienten och klicka på&#x200B;**Visa välkomstkit online**.

   1. Då öppnas webbkanalversionen av samma dokument.

1. En snabb referens till PDF:

   *https://&lt;aemserver>:&lt;port>/aem/formdetails.html/content/dam/formsanddocuments/adobe-gov-forms/welcome-handbook/we-gov-welcome-handbook*

1. En snabb referens till IC direkt:

   *https://&lt;port>/content/dam/formsanddocuments/adobe-gov-forms/welcome-handbook/we-gov-welcome-handbook/jcr:content?channel=web&amp;mode=preview&amp;wcmmode=disabled*

   ![Handbok](/help/forms/using/assets/welcome_benefits_handbook.png) för ![interaktiv kommunikationslänk för välkomstförmåner](/help/forms/using/assets/interactive_communication.png)

## Påminnelse om förnyelse - medborgare (Aya) {#renewal-reminder-citizen-aya}

**** Detta avsnitt: Camila schemalägger också en påminnelse så ett år senare. (Arbetsflödessteg som automatiserar/kör och skickar e-post).

### Aya User Story (e-postklient) {#aya-user-story-email-client-1}

**Användarinstruktioner:**

1. Navigera till din e-postklient.
1. Leta reda på och öppna e-postmeddelandet med en påminnelse om förnyelse.
1. Klicka på knappen&quot;**Skicka ett nytt program**&quot; för att öppna det anpassade formuläret.

   1. Detta avsnitt är avsiktligt tomt för att stödja förifyllning av data i fas 2.
   ![Påminnelse om förnyelse - e-post](/help/forms/using/assets/renewal_reminder_email.png)

## Analytics CX Lead (Camila) {#analytics-cx-lead-camila}

**** Detta avsnitt: Camila navigerar till en kontrollpanel där hon kan se nyckeltal från olika myndigheter, t.ex. procent av de medborgare som börjar fylla i ett formulär och överge det, den genomsnittliga tiden från att begära in det till svar på ansökan om godkännande/avslag, och engagemangsstatistik för de förmånsböcker hon har skickat till medborgarna.

### Camila granskar rapporter om webbplatser (Web.Gov Adobe Analytics) {#camila-reviews-sites-reporting-we-gov-adobe-analytics}

1. Gå till *https://&lt;aemserver>:&lt;port>/sites.html/content*
1. Välj&quot;**AEM Forms We.Gov Site**&quot; för att visa webbplatssidorna.
1. Välj en av webbplatssidorna (t.ex. Hem) och välj&quot;**Analys och rekommendationer**&quot;.

   ![Analyser och rekommendationer](/help/forms/using/assets/analytics_recommendation.jpg)

1. På den här sidan ser du hämtad information från Adobe Analytics som gäller AEM Sites-sidan (Obs! den här informationen uppdateras regelbundet från Adobe Analytics och visas inte i realtid).

   ![Nyckeltal för Adobe Analytics](/help/forms/using/assets/analytics_key_metrics.jpg)

1. På sidan för sidvisning (som du kommer åt i steg 3.0) kan du även visa sidvisningsinformationen genom att ändra visningsinställningen så att objekt i **listvyn** visas.
1. Leta upp listrutan **Visa** och välj **Listvy**.

   ![Listvy i listrutan Visa](/help/forms/using/assets/list_view_view_dropdown.jpg)

1. På samma meny väljer du &quot;**Visningsinställning**&quot; och markerar de kolumner som du vill visa under &quot;**Analytics**&quot;.

   ![Konfigurera visning av kolumner](/help/forms/using/assets/view_setting_analytics.jpg)

1. Klicka på&#x200B;**Uppdatera** för att göra de nya kolumnerna tillgängliga.

   ![Gör nya kolumner tillgängliga](/help/forms/using/assets/new_columns_available.jpg)

### Camila granskar Forms-rapportering (Adobe Analytics, Web.Gov) {#camila-reviews-forms-reporting-we-gov-adobe-analytics}

1. Navigera till

   *https://&lt;aemserver>:&lt;port>/aem/forms.html/content/dam/formsanddocuments/adobe-gov-forms*

1. Välj anpassningsformuläret &quot;**Registreringsprogram för hälsoförmåner**&quot; och välj alternativet &quot;**Analysrapport**&quot;.

   ![Registreringsprogram för hälsoförmåner](/help/forms/using/assets/analytics_report_benefits.jpg)

1. Vänta tills sidan har lästs in och visa analysrapportdata.

   ![Data för analysrapport](/help/forms/using/assets/analytics_report_data_updated.jpg)

