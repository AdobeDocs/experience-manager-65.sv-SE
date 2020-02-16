---
title: Konfigurera en PDFG-nätverksskrivare (endast Windows)
seo-title: Konfigurera en PDFG-nätverksskrivare (endast Windows)
description: Lär dig hur du konfigurerar en PDFG-nätverksskrivare (endast Windows)
seo-description: Lär dig hur du konfigurerar en PDFG-nätverksskrivare (endast Windows)
uuid: 13b8481e-5ef0-4a07-9602-7bc4d9e05dd4
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_pdf_generator
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 7620e5e4-022e-49b2-8cfe-d5eec8ab99d7
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Konfigurera en PDFG-nätverksskrivare (endast Windows) {#setting-up-a-pdfg-network-printer-windows-only}

Med PDFG Network Printer kan man generera ett PDF-dokument från alla program som stöder utskrift. När en användare har installerat PDFG Network Printer visas en ny skrivare med namnet *PDF-generator* i skrivaravsnittet på Kontrollpanelen i Windows. Om det redan finns en skrivare med samma namn uppmanas användaren att ange ett annat namn.

Om du skriver ut på den här skrivaren från ett program skickas dokumentet (i PostScript-format) till PDF Generator, som konverterar PostScript-filen till PDF. Beroende på hur du har konfigurerat PDF Generator skickas PDF-dokumentet till användaren som en bifogad fil i ett e-postmeddelande, PDF-dokumentet vidarebefordras till en angiven AEM-formulärtjänst eller -process, eller båda åtgärderna utförs.

Följande steg krävs för att konfigurera en PDFG-nätverksskrivare:

1. Konfigurera e-postinställningar. (Se [Konfigurera e-postinställningar för PDFG-nätverksskrivare](setting-pdfg-network-printer-windows.md#configure-email-settings-for-pdfg-network-printer).)
1. Konfigurera inställningarna för PDFG Network Printer i administrationskonsolen. (Se [Konfigurera inställningar](setting-pdfg-network-printer-windows.md#configure-the-pdfg-network-printer-settings)för PDFG-nätverksskrivare.)
1. Se till att dina användare är konfigurerade med en giltig e-postadress i AEM-formulärdatabasen och tilldela PDFGUserPermission till varje användare. <!-- Fix broken link See Setting up and organizing users -->
1. Kontrollera att 32-bitars JRE6 är installerat på användarnas datorer.
1. Installera skrivaren på användarnas datorer. (Se [Installera PDFG Network Printer på användarens dator](setting-pdfg-network-printer-windows.md#install-pdfg-network-printer-on-a-user-s-computer).)

## Konfigurera e-postinställningar för PDFG-nätverksskrivare {#configure-email-settings-for-pdfg-network-printer}

1. I administrationskonsolen klickar du på Tjänster > Program och tjänster > Tjänsthantering.
1. På sidan Tjänsthantering klickar du på provider.email_sendmail_service, anger SMTP-inställningarna och klickar på Spara.

## Konfigurera inställningar för PDFG-nätverksskrivare {#configure-the-pdfg-network-printer-settings}

1. I administrationskonsolen klickar du på Tjänster > PDF Generator > PDFG Network Printer
1. I listorna Adobe PDF-inställningar och Skyddsinställningar väljer du de alternativ som ska gälla för den genererade PDF-filen. Mer information om de här inställningarna finns i [Konfigurera Adobe PDF-inställningar](/help/forms/using/admin-help/configuring-pdf-settings.md#configuring-adobe-pdf-settings) och [Konfigurera säkerhetsinställningar](/help/forms/using/admin-help/configuring-security-settings.md#configuring-security-settings).
1. Om du vill skicka tillbaka de konverterade PDF-filerna till användarna markerar du alternativet E-posta den konverterade PDF-filen tillbaka till användaren och anger följande information:

   * E-postadressen som ska användas för att skicka PDF-filer till användarna
   * Ämnet för e-postmeddelandet
   * E-postmeddelandets sidhuvud, brödtext och sidfot. I e-postmeddelandet ersätts &lt;receiverName> med det fullständiga namnet på den användare som skrev ut dokumentet.

1. Om du vill skicka de konverterade PDF-filerna till en AEM-formulärtjänst eller -process väljer du alternativet Vidarebefordra den konverterade PDF-filen till den angivna AEM-formulärtjänsten eller -processen och anger följande information:

   * Namnet på tjänsten som ska anropas
   * Namnet på åtgärden för tjänsten som ska anropas
   * Namnet på indataparametern, enligt specifikationen i filen component.xml för tjänsten eller processen. PDF-dokumentet används som ett värde för den indataparametern.

1. Klicka på Spara.

Om du vill återgå till den ursprungliga standardtexten för e-post klickar du på Återställ e-postinnehåll.

## Installera PDFG Network Printer på användarens dator {#install-pdfg-network-printer-on-a-user-s-computer}

Användare som har rollen PDFG-administratör eller PDFG-användare kan installera en PDFG-nätverksskrivare. Du måste ha en 32-bitars JDK installerad på datorn.

1. (PDFG-administratörer) I administrationskonsolen klickar du på Tjänster > PDF Generator > PDFG Network Printer.

   (PDFG-användare) Gå till `http(s)://[host]:[port]/pdfgui` och klicka på länken under PDFG Network Printer Installation.

1. Klicka på länken under Installation av PDFG-nätverksskrivare. När du uppmanas att ange användarkontouppgifter anger du användarnamnet och lösenordet som du använde i steg 1 för att logga in. Ett meddelande om att skrivaren har installerats visas.

   ***Obs **! Om användarens lösenord ändras måste användarna installera om PDFG-nätverksskrivaren på sina datorer. Du kan inte uppdatera lösenordet från administrationskonsolen.*

1. Klicka på OK.

