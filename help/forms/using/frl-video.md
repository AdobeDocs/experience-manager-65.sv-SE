---
source-git-commit: b5e44b78659f0cb1b8b0025be30143b98c0bf8df
workflow-type: tm+mt
source-wordcount: '1065'
ht-degree: 0%

---
# Videoskript: Konfigurera funktionsbegränsad licensiering (FRL) för Adobe Acrobat i AEM Forms

| Visual | Titel | Föredragshållarskript |
|--------|-------|---------------|
| Titelskärm med AEM Forms logotyp och FRL-grafik | Introduktion | Välkommen till den här självstudiekursen om hur du konfigurerar funktionen begränsad licensiering, eller FRL, för Adobe Acrobat på din AEM Forms-server. Detta är en viktig process eftersom Adobe övergår från permanenta licenser till den nya FRL-modellen. |
| Tidslinje som visar EOL-datum med pilar som pekar på övergången FRL | Bakgrund | Adobe Acrobat Classic-versioner med permanenta licenser har nått slutet av livscykeln, vilket kräver en övergång till nyare versioner. AEM Forms PDF Generator förlitar sig på Adobe Acrobat för dokumentkonverteringsfunktioner. Modellen med begränsad licens ger samma funktionalitet men med en modern licensieringsmetod som hanteras via Adobe Admin Console. |
| Checklista med obligatoriska objekt med kryssrutor och ikoner | Förutsättningar | Innan vi börjar ska vi se till att du har allt du behöver: Först får du Adobe Admin Console-åtkomst med systemadministratörsbehörighet. För det andra ett användarkonto med rollen Distributionsadministratör i Admin Console. För det tredje, lokal administratörsbehörighet på den server som kör AEM Forms. För det fjärde ett 64-bitars operativsystem för Windows på din AEM Forms-server. 5) En stabil internetanslutning för licensaktivering. Du bör också känna till Adobe Admin Console gränssnitt och förstå AEM Forms driftsättningsarkitektur. |
| Varningsikon med grafik för säkerhetskopiering | Viktigt | Kom ihåg att säkerhetskopiera anpassade Acrobat-inställningar innan du startar, eftersom du måste avinstallera befintliga Acrobat-installationer under den här processen. |
| Flödesdiagram med numrerade steg från 1 till 7 | Processöversikt | Detta inbegriper flera viktiga steg: förbereda ett FRL-paket i Admin Console, bevilja hämtningsbehörighet, avinstallera tidigare Acrobat-versioner, installera nya Acrobat Pro, distribuera FRL-paketet och verifiera installationen. Låt oss gå igenom varje steg. |
| Skärmbild från Adobe Admin Console med fliken Paket markerad | Steg 1: Förberedelser för Admin Console | Logga först in på Adobe Admin Console med systemadministratörsbehörighet. Gå till fliken Paket och välj &quot;Funktionen begränsad licens&quot;. Klicka på knappen &quot;Kom igång&quot; för att börja skapa paketet. |
| Skapa konfigurationsskärmen för paket med inställningarna markerade | Paketkonfiguration | Konfigurera ditt paket med följande rekommenderade inställningar: Välj Offline för aktiveringsmetod, PDF Generation för berättigande och Windows 64-bitars för plattformen. Om du väljer ett program ska du bara spara licensfilen i de valda programmen. Ge paketet ett beskrivande namn som&quot;Acrobat FRL AEM Forms&quot; och skapa paketet. |
| Fliken Admin Console-användare med dialogrutan Behörigheter | Steg 2: Bevilja hämtningsbehörigheter | Därefter måste du skapa eller identifiera en användare som ska hämta paketet. I Admin Console går du till fliken Användare, markerar din användare och tilldelar dem rollen Distributionsadministratör. På så sätt kan de hämta det FRL-paket som du har skapat. |
| Kontrollpanelen i Windows med appar och funktioner som visar Acrobat | Steg 3: Avinstallera tidigare Acrobat | Innan du installerar den nya versionen måste du ta bort alla befintliga Acrobat-installationer helt. Öppna Kontrollpanelen i Windows, gå till Program, leta upp Adobe Acrobat och välj Avinstallera. Om du vill ta bort mer noggrant bör du överväga att använda Adobe Acrobat Cleaner Tool, särskilt om du stöter på problem senare under processen. |
| Adobe Acrobat DC - nedladdningssida med installationsavsnitt markerat | Steg 4: Hämta och installera Adobe Acrobat Pro | När du har avinstallerat hämtar du rätt Acrobat Pro-installationsprogram från hämtningssidan för Adobe Acrobat DC. För kompatibilitet med PDF Generator rekommenderas 32-bitars Windows-installationsprogrammet. |
| Installationsprocess som visar extraherings- och konfigurationssteg | Installationsprocess | Extrahera den hämtade zip-filen till en mapp, leta upp Setup.exe och kör den som administratör. Följ instruktionerna på skärmen för att slutföra installationen. Efter installationen kan du öppna Acrobat Pro en gång för att stänga alla välkomstdialogrutor och slutföra den första installationen. |
| Fliken Admin Console Packages med hämtningsknappen markerad | Steg 5: Hämta FRL-paketet | Logga nu in på Adobe Admin Console med det konto som du tidigare har gett hämtningsbehörighet till. Gå till fliken Paket, leta upp ditt FRL-paket och hämta det till din AEM Forms-server. |
| Kommandotolk som administratör med kommandon som skrivs | Steg 6: Distribuera paketet | Extrahera det hämtade paketet till en katalog på servern. Öppna Kommandotolken som administratör och navigera till extraheringskatalogen. |
| Kommandorad som visar aktiveringskommandot med syntaxen markerad | Aktiveringskommando | Kör aktiveringskommandot med följande syntax: `adobe-licensing-toolkit.exe -p -i -f ngl-preconditioning-data.json`. Ersätt JSON-filnamnet med det exakta filnamnet från paketet. Kommandoparametrarna är: -p för plattformen, -i för att installera licensen och -f för att ange sökvägen till JSON-filen. När det är klart visas meddelandet&quot;Åtgärden har slutförts&quot;. |
| Tabell som visar kommandoparametrar och beskrivningar | Kommandoparametrar | Parametern -p anger plattformen och identifierar automatiskt operativsystemet. Parametern -i instruerar verktyget att installera och aktivera licensen. Parametern -f anger sökvägen till JSON-licensfilen. |
| AEM Forms administratörsgränssnitt som visar tjänsten PDF Generator | Steg 7: Testa och verifiera | Slutligen testar du installationen genom att öppna AEM Forms administratörsgränssnitt och konvertera ett enkelt dokument till PDF med hjälp av PDF Generator. Kontrollera också Acrobat-installationen genom att öppna Acrobat Pro, gå till Hjälp → Om och bekräfta versionsnumret och licensstatusen. |
| Delad skärm: Dialogrutan Acrobat Om och den lyckade konverteringen av PDF | Verifiering | Kontrollera att licensen är aktiverad i Acrobat och att PDF Generator kan konvertera dokument. |
| Vanliga fel och lösningar med ikoner | Felsökning - tips | Om du råkar ut för problem ska du kontrollera följande vanliga problem: Kontrollera att du kör kommandotolken som administratör, kontrollera att JSON-filnamnet är korrekt, söka efter installationer som står i konflikt och kontrollera att servern har rätt Internetanslutning för aktivering. |
| Ytterligare felsökningsobjekt med bockar | Fler felsökningsfunktioner | Kontrollera också om det finns brandväggsbegränsningar, skadade paket eller Adobe ID:n som är i konflikt på servern. Om inget annat fungerar kontaktar du Adobe Support med detaljerade felmeddelanden. |
| Skärmen lyckades med bockmarkeringsikon och kontaktinformation | Slutsats | Du har nu konfigurerat funktionen begränsad licensiering för Adobe Acrobat på din AEM Forms-server. Om du behöver mer hjälp kan du kontakta Adobe Support eller läsa den detaljerade dokumentationen som finns på Experience League. |
| Stänger skärmen med Adobe logotyp och eftertexter | Tack | Tack för att du tittar på den här självstudiekursen. Mer information finns i Experience League dokumentation. |

**Anteckningar för produktion:**

- Varje rad i tabellen representerar en scen eller ett huvudavsnitt i videon
- Beräknad total varaktighet: 6-7 minuter
- Inkludera skärminspelningar i de faktiska processerna där det är möjligt
- Använd bildtexter och markeringar för att framhäva viktiga gränssnittselement
- Inkludera bildtexter som hjälpmedel
- Överväg att lägga till kapitelmarkörer så att visningsprogrammen kan hoppa till specifika avsnitt