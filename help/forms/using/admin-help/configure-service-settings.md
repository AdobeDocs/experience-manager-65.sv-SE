---
title: Konfigurera tjänstinställningar
seo-title: Konfigurera tjänstinställningar
description: Lär dig hur du konfigurerar tjänstinställningar.
seo-description: Lär dig hur du konfigurerar tjänstinställningar.
uuid: e95425a4-62f6-473e-b21b-d081c432e02d
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_services
products: SG_EXPERIENCEMANAGER/6.4/FORMS
discoiquuid: 2fab4b0c-e5db-47cd-b85a-4ff5ad6eb178
translation-type: tm+mt
source-git-commit: d3719a9ce2fbb066f99445475af8e1f1e7476f4e

---


# Konfigurera tjänstinställningar {#configure-service-settings}

Du kan använda sidan Tjänsthantering för att konfigurera inställningar för var och en av de tjänster som ingår i AEM-formulär. De tillgängliga inställningarna varierar beroende på vilken tjänst som konfigureras.

1. I administrationskonsolen klickar du på Tjänster > Program och tjänster > Tjänsthantering.
1. Stoppa tjänsten innan du ändrar den. (Se [Starta och stoppa tjänster](/help/forms/using/admin-help/starting-stopping-services.md#starting-and-stopping-services).)
1. Klicka på namnet på den tjänst som du vill konfigurera.
1. Om tjänsten har en konfigurationsflik använder du den för att ändra inställningarna för tjänsten. Se listan med länkar nedan för mer information.

   >[!NOTE]
   >
   >Alla tjänster som listas på sidan Tjänsthantering har inte fliken Konfiguration. För processer som du har skapat visas bara fliken Konfiguration om du har lagt till en konfigurationsparameter till processen i Workbench. (Se&quot;Konfigurationsparametrar&quot; i [Workbench-hjälpen](https://www.adobe.com/go/learn_aemforms_workbench_63) .)


1. Klicka på fliken Säkerhet och ange säkerhetsinställningarna för tjänsten. Se [Ändra skyddsinställningar för en tjänst](configure-service-settings.md#modifying-security-settings-for-a-service).
1. Om tjänsten har en fliken Slutpunkter använder du den för att ändra slutpunktsinställningarna. Se [Hantera slutpunkter](/help/forms/using/admin-help/adding-enabling-modifying-or-removing.md).
1. Klicka på fliken Pooling och ange poolinställningar. Se [Konfigurera poolning för en tjänst](configure-service-settings.md#configuring-pooling-for-a-service).
1. Klicka på Spara om du vill spara ändringarna eller klicka på Avbryt om du vill ignorera dem.
1. Markera kryssrutan bredvid tjänstnamnet och klicka på Starta för att starta om tjänsten.

## Granska inställningar för arbetsflödestjänst {#audit-workflow-service-settings}

Workbench ger möjlighet att spela in processinstanser när de körs under körning och sedan spela upp dem för att observera processens beteende. (Se [Workbench-hjälpen](https://www.adobe.com/go/learn_aemforms_workbench_63).) För att spara utrymme i formulärserverns filsystem kan du begränsa mängden lagrade processinspelningsdata. Du kan konfigurera följande egenskaper för tjänsten Granskningsarbetsflöde ( `AuditWorkflowService`):

**** maxNumberOfRecordingInstances: Det maximala antalet inspelningar som lagras. När det högsta antalet lagras tas den äldsta inspelningen bort från filsystemet när en ny inspelning skapas. Den här egenskapen är användbar om du tenderar att skapa många inspelningar och vill ta bort gamla inspelningar automatiskt. Standardvärdet är 50.

**** MaxNumberOfRecordingPoster: Maximalt antal dataposter som kan lagras för varje inspelning. Dataposter är information om åtgärder som utförs i processen. Flera poster lagras för varje körning av en åtgärd, till exempel om åtgärden har startats, om åtgärden har slutförts och om den väg som leder till åtgärden är slutförd. Den här egenskapen är användbar när processer kan innehålla många körningar av åtgärder, till exempel när en oändlig slinga påträffas. Standardvärdet är 50.

## streckkodsinställningar för formulärtjänst {#barcoded-forms-service-settings}

Streckkodsblanketttjänsten extraherar `(BarcodedFormsService)` streckkodsdata från skannade bilder. Tjänsten accepterar ett streckkodsformulär (TIFF eller PDF) som indata och extraherar maskinvaruåtergivningen av data som är kodade med streckkoden.

Följande inställningar är tillgängliga för den streckkodade formulärtjänsten.

**** Läs åt vänster: När du väljer det här alternativet skannas streckkodsbilder vågrätt från höger till vänster.

**** Läs åt höger: När du väljer det här alternativet skannas streckkodsbilder vågrätt från vänster till höger.

**** Uppläsning: När du väljer det här alternativet skannas streckkodsbilder lodrätt nedifrån och upp.

**** Uppläsning: När du väljer det här alternativet skannas streckkodsbilder lodrätt uppifrån och ned.

***Obs **: Som standard är alla alternativ markerade. Avmarkera bara ett alternativ om du är säker på att inga streckkoder visas på det sättet i formulären.*

**** Bas filsökväg: Den filsökväg som är relativ till vilka parametrarna för gruppindata och utdata för åtgärderna Kör XML-filjobb och Kör Flat File-jobb tolkas. I klustrade konfigurationer måste sökvägen till basfilen vara en delad filsystemplats som alla klusternoder har läs-/skrivåtkomst till.

**** Namn på datakälla: Namnet på datakällan som används för att underhålla status- och historikinformation om batchbearbetningsjobb. Den angivna datakällan måste ha stöd för globala (XA) transaktioner.

## Inställningar för tjänsten Central Migration Bridge (inaktuellt) {#central-migration-bridge-service-settings}

Tjänsten Central Migration Bridge ( `CentralMigrationBridge`) anropar en delmängd av funktionerna i Adobe Central Pro Output Server (Central), som innehåller kommandona JFMERGE, JFTRANS och XMLIMPORT. Med tjänståtgärderna för central migreringsbrygga kan du återanvända följande centrala resurser i AEM-formulär:

* malldesign (&amp;ast;.ifd)
* utdatamallar (&amp;ast;.mdf)
* datafiler (&amp;ast;.dat-filer)
* inledningsfiler (&amp;ast;.pre-filer)
* datadefinitionsfiler (&amp;ast;.tdf)

Följande inställning är tillgänglig för tjänsten Central Migration Bridge.

**** Katalog för central installation: Katalogen där Adobe Central 5.7 är installerat.

## Content Repository Connector for EMC Documentum-tjänstinställningar {#content-repository-connector-for-emc-documentum-service-settings}

Med tjänsten Content Repository Connector for EMC Documentum ( `EMCDocumentumContentRepositoryConnector`) kan du skapa processer som interagerar med innehåll som lagras i en Documentum-databas.

Följande inställning är tillgänglig för tjänsten Content Repository Connector for EMC Documentum.

**** Standardsökväg för resurslänksobjekt: Standarddelen av sökvägen i Documentum-databasen för lagring av objektet Resurslänk. Den faktiska sökvägen består av standardsökvägen och platsen för formulärmallen i AEM-formulärdatabasen.

Om standardsökvägen till exempel är inställd på `/LiveCycleES/ConnectorforEMCDocumentum/AssetLinkObjects`och formulärmallen lagras i en mapp `/Docbase/forms/`, lagras objektet Resurslänk på följande plats:

`/LiveCycleES/ConnectorforEMCDocumentum/AssetLinkObjects/Docbase/forms/`

Standardvärdet för den här inställningen är `/LiveCycleES/ConnectorforEMCDocumentum/AssetLinkObjects`.

## Content Repository Connector for IBM FileNet service settings {#content-repository-connector-for-ibm-filenet-service-settings}

Med Content Repository Connector för IBM FileNet kan du skapa processer som interagerar med innehåll som lagras i en IBM FileNet-databas.

Följande inställning är tillgänglig för Content Repository Connector för tjänsten IBM FileNet.

**** Standardsökväg för resurslänksobjekt: Standarddelen av sökvägen i IBM FileNet-databasen för lagring av objektet Asset Link. Den faktiska sökvägen består av standardsökvägen och platsen för formulärmallen i AEM-formulärdatabasen.

Om standardsökvägen till exempel är inställd på `/LiveCycleES/ConnectorforIBMFileNet/AssetLinkObjects`och formulärmallen lagras i en mapp `/Docbase/forms/`, lagras objektet Resurslänk på följande plats:

`/LiveCycleES/ConnectorforIBMFileNet/AssetLinkObjects/Docbase/forms/`

Standardvärdet för den här inställningen är `/LiveCycleES/ConnectorforIBMFileNet/AssetLinkObjects`.

## Konvertera PDF-tjänstinställningar {#convert-pdf-service-settings}

Tjänsten Konvertera PDF ( `ConvertPdfService`) konverterar PDF-dokument till PostScript och till ett antal bildformat (JPEG, JPEG 2000, PNG och TIFF). Att konvertera ett PDF-dokument till PostScript är användbart för oövervakad serverbaserad utskrift på en PostScript-skrivare. Att konvertera ett PDF-dokument till en flersidig TIFF-fil är praktiskt när man arkiverar dokument i content management-system som saknar stöd för PDF-dokument.

Följande inställningar är tillgängliga för tjänsten Konvertera PDF.

**** Transaktionstyp: Anger hur en transaktionskontext ska spridas till en åtgärd.

**** Obligatoriskt: Stöder en transaktionskontext om en sådan finns. i annat fall skapas en ny transaktionskontext. Detta är standardvärdet.

**** Kräver nytt: Skapar alltid en ny transaktionskontext. Om det finns en aktiv transaktionskontext pausas den.

**** Timeout för transaktion (i sek): Antalet sekunder som den underliggande transaktionsprovidern ska vänta innan en transaktion som omsluter den här åtgärden återställs. Det här värdet ignoreras om en befintlig transaktionskontext sprids. Standardvärdet är 180.

**** Tröskelupplösning för utjämning (i dpi): Den bildupplösning under vilken utjämning (eller kantutjämning) tillämpas på text, teckningar och bilder, om du har valt alternativet Använd utjämning på för dessa element.

**** Använd utjämning på text: Styr kantutjämning av text. Avmarkera den här kryssrutan om du vill inaktivera utjämning av text och göra texten skarpare och lättare att läsa med en skärmförstorare.

**** Använd utjämning på LineArt: Använder utjämning för att ta bort plötsliga vinklar i linjer.

**** Använd utjämning på bilder: Använder utjämning för att minimera abrupta ändringar i bilder.

## Distiller-tjänstinställningar {#distiller-service-settings}

Distiller-tjänsten ( `DistillerService`) konverterar PostScript-, Encapsulated PostScript- (EPS) och PRN-filer till PDF-filer över ett nätverk.

Följande inställningar är tillgängliga för Distiller-tjänsten.

**** Adobe PDF-inställningar: Följande förkonfigurerade inställningar används för den genererade PDF-filen:

* Högkvalitativ utskrift
* Stora sidor
* PDFA1b 2005 CMYK
* PDFA1b 2005 RGB
* PDFX1a 2001
* PDFX3 2002
* Tryckkvalitet
* Minsta filstorlek
* Standard

Nya inställningar kan skapas med användargränssnittet i PDF Generator.

**** Säkerhetsinställningar: Förkonfigurerade säkerhetsinställningar som används för genererade PDF-dokument. Standardvärdet är Ingen säkerhet. Du måste skapa skyddsinställningar med PDF Generator och sedan ange inställningen här.

**** Poolstorlek: Poolens ursprungliga storlek. När Distiller-tjänsten distribueras, används det här numret för att fastställa antalet instanser för tjänstimplementering som skapas och tilldelas den fripool som väntar på anrop. Tjänstbehållaren kan sedan svara direkt på anropsbegäranden utan att först initiera en tjänstinstans.

## Inställningar för dokumenthanteringstjänsten {#document-management-service-settings}

>[!NOTE]
>
>Adobe® LiveCycle® Content Services ES (utgått) är ett innehållshanteringssystem som installeras med LiveCycle. Det gör det möjligt för användarna att utforma, hantera, övervaka och optimera humancentrerade processer. Supporten för innehållstjänster (borttaget) upphör 2014-12-31. Se [Adobes livscykeldokument](https://www.adobe.com/support/products/enterprise/eol/eol_matrix.html). Mer information om hur du konfigurerar innehållstjänster (borttaget) finns i [Administrera innehållstjänster](https://help.adobe.com/en_US/livecycle/9.0/admin_contentservices.pdf).

Med Document Management Service ( `DocumentManagementService`) kan processer använda innehållshanteringsfunktionen som tillhandahålls av Content Services (Borttagen). Dokumenthanteringsåtgärder innehåller grundläggande uppgifter som krävs för att underhålla utrymme och innehåll i innehållshanteringssystemet. Exempel på sådana uppgifter är kopiera, ta bort, flytta, hämta och lagra innehåll, skapa blanksteg och associationer samt hämta och ange innehållsattribut.

Följande inställningar är tillgängliga för dokumenthanteringstjänsten.

**** Butiksschema: Schemat för den butik där innehållet finns. Standardvärdet är arbetsyta.

**** HTTP-port: Den port som används för åtkomst till innehållstjänster (borttagen). Standardvärdet är 8080.

## Inställningar för e-posttjänst {#email-service-settings}

E-post används ofta för att distribuera innehåll eller tillhandahålla statusinformation som en del av en automatiserad process. Med e-posttjänsten ( `EmailService`) kan processer ta emot e-postmeddelanden från en POP3- eller IMAP-server och skicka e-postmeddelanden till en SMTP-server.

En process använder till exempel e-posttjänsten för att skicka ett e-postmeddelande med en bifogad PDF-formulärfil. E-posttjänsten ansluter till en SMTP-server för att skicka e-postmeddelandet med den bifogade filen. PDF-formuläret är utformat så att mottagaren kan klicka på Skicka när formuläret har fyllts i. Åtgärden gör att formuläret returneras som en bifogad fil till den angivna e-postservern. E-posttjänsten hämtar det returnerade e-postmeddelandet och lagrar det ifyllda formuläret i en processdataformulärvariabel.

Följande inställningar är tillgängliga för e-posttjänsten.

**** SMTP-värd: IP-adressen eller URL:en för SMTP-servern som ska användas för att skicka e-post.

**** SMTP-portnummer: Den port som används för att ansluta till SMTP-servern.

**** SMTP-autentisering: Välj om användarautentisering krävs för att ansluta till SMTP-servern.

**** SMTP-användare: Användarnamnet för det användarkonto som ska användas för att logga in på SMTP-servern.

**** SMTP-lösenord: Lösenordet som är associerat med SMTP-användarkontot.

**** SMTP-transportsäkerhet: Det säkerhetsprotokoll som ska användas för att ansluta till SMTP-servern:

* Välj Ingen om inget protokoll används (data skickas i klartext)
* Välj SSL om Secure Sockets Layer-protokollet används.
* Välj TLS om transportlagersäkerhet används.

**** POP3/IMAP-värd: IP-adressen eller URL:en för POP3- eller IMAP-servern som ska användas för att skicka e-post.

**** POP3/IMAP-användarnamn: Användarnamnet för det användarkonto som ska användas för att logga in på POP3- eller IMAP-servern.

**** POP3/IMAP-lösenord: Lösenordet som är associerat med POP3- eller IMAP-användarkontot.

**** POP3/IMAP-portnummer: Den port som används för att ansluta till POP3- eller IMAP-servern.

**** POP3/IMAP: Det protokoll som ska användas för att skicka och ta emot e-post.

**** Ta emot transportsäkerhet: Det säkerhetsprotokoll som ska användas för att ansluta till SMTP-servern:

* Välj Ingen om inget protokoll används (data skickas i klartext).
* Välj SSL om Secure Sockets Layer-protokollet används.
* Välj TLS om transportlagersäkerhet används.

## Inställningar för krypteringstjänst {#encryption-service-settings}

Med krypteringstjänsten ( `EncryptionService`) kan du kryptera och dekryptera dokument. När ett dokument är krypterat blir innehållet oläsligt. En behörig användare kan dekryptera dokumentet för att få åtkomst till innehållet. Om ett PDF-dokument är krypterat med ett lösenord måste användaren ange det öppna lösenordet innan dokumentet kan visas i Adobe Reader eller Adobe Acrobat. Om ett PDF-dokument är krypterat med ett certifikat måste användaren dekryptera PDF-dokumentet med den offentliga nyckel som motsvarar det certifikat (privat nyckel) som användes för att kryptera PDF-dokumentet.

Följande inställningar är tillgängliga för krypteringstjänsten.

**** LDAP-standardserver att ansluta till: Värdnamn för den LDAP-server som används för att hämta certifikat för dokumentkryptering.

**** LDAP-standardport att ansluta till: LDAP-serverns portnummer.

**** LDAP-standardanvändarnamn: Om LDAP-servern kräver autentisering anger du det användarnamn som ska användas för att ansluta till LDAP-servern.

**** LDAP-standardlösenord: Om LDAP-servern kräver autentisering anger du lösenordet som motsvarar användarnamnet som ska användas för att ansluta till LDAP-servern.

***Obs **: Använd endast enkel autentisering (användarnamn och lösenord) när anslutningen skyddas via SSL (med LDAPS).*

**Kompatibilitetsläge:**

## FTP-tjänstinställningar {#ftp-service-settings}

Med FTP-tjänsten ( `FTP`) kan processer interagera med en FTP-server. FTP-tjänståtgärder kan hämta filer från FTP-servern, skicka filer på FTP-servern och ta bort filer från FTP-servern. Till exempel kan dokument som genereras från en process lagras på en FTP-server för distribution. Eller så kan ett externt system generera filer baserat på tidigare steg i en process. I ett efterföljande steg i processen kan filerna överföras till en fjärrplats.

Följande inställningar är tillgängliga för FTP-tjänsten.

**** Standardvärd: FTP-serverns IP-adress eller URL.

**** Standardport: Den port som används för att ansluta till FTP-servern. Standardvärdet är 21.

**** Standardanvändarnamn: Namnet på det användarkonto som du kan använda för att komma åt FTP-servern. Användarkontot måste ha tillräcklig behörighet för att utföra de FTP-åtgärder som krävs för den här tjänsten.

**** Standardlösenord: Lösenordet som ska användas med det angivna användarnamnet för autentisering med FTP-servern.

## Generera PDF-tjänstinställningar {#generate-pdf-service-settings}

Tjänsten Generate PDF ( `GeneratePDFService`) konverterar filer i olika format till PDF-dokument och konverterar PDF-dokument till ett antal filformat.

Följande inställningar är tillgängliga för tjänsten Generera PDF.

**** Adobe PDF-inställningar: Namnet på de förkonfigurerade Adobe PDF-inställningarna som ska tillämpas på ett konverteringsjobb, om dessa inställningar inte anges som en del av API-anropsparametrarna. Adobe PDF-inställningarna konfigureras i administrationskonsolen genom att klicka på Tjänster > PDF Generator > Adobe PDF-inställningar. De här inställningarna gäller endast för PDFMaker-baserade konverteringar.

**** Säkerhetsinställningar: Namnet på de förkonfigurerade säkerhetsinställningarna som ska tillämpas på ett konverteringsjobb, om dessa inställningar inte anges som en del av API-anropsparametrarna. Säkerhetsinställningarna konfigureras i administrationskonsolen genom att klicka på Tjänster > PDF Generator > Skyddsinställningar.

**** Filtypsinställningar: Namnet på den förkonfigurerade filtypsinställningen som ska användas för ett konverteringsjobb, om dessa inställningar inte anges som en del av API-anropsparametrarna. Filtypsinställningarna konfigureras i administrationskonsolen genom att klicka på Tjänster > PDF Generator > Filtypsinställningar.

**** Använd Acrobat WebCapture (endast Windows): När den här inställningen är true använder tjänsten Generera PDF Acrobat X Pro för alla HTML-till-PDF-konverteringar. Detta kan förbättra kvaliteten på PDF-filer som skapas från HTML, men prestanda kan vara något lägre. Standardvärdet är false.

**** Använd Acrobat Image Conversion (endast Windows): När den här inställningen är true använder tjänsten Generera PDF Acrobat X Pro för alla Image till PDF-konverteringar. Den här inställningen är bara användbar om standardkonverteringsfunktionen för ren Java inte kan konvertera en stor del av indatabilderna korrekt. Standardvärdet är false.

**** Aktivera Acrobat-baserade AutoCAD-konverteringar (endast Windows): När den här inställningen är true använder tjänsten Generera PDF Acrobat X Pro för alla DWG till PDF-konverteringar. Den här inställningen är bara användbar om AutoCAD inte är installerat på servern eller om AutoCAD-konverteringsfunktionen inte kan konvertera filer.

**** Reguljära uttryck för att hitta förbjudna specialtecken i användarnamnet (endast Windows): Anger tecken som stör åtgärderna Exportera PDF och Optimera PDF när tecknen visas i användarens namn.

**** Poolstorlek för ImageToPDF: Poolstorleken för standardkonverteraren (ren Java) för bild till PDF i tjänsten Generera PDF. Den här inställningen kontrollerar det maximala antalet samtidiga Image-to-PDF-konverteringar som tjänsten Generate PDF kan utföra. Standardvärdet för den här inställningen (rekommenderas för enprocessorsystem) är 3, som du kan öka på flerprocessorsystem.

**** Poolstorlek för HTML till PDF: Poolstorleken för HTML-till-PDF-konverteraren i tjänsten Generera PDF. Den här inställningen kontrollerar det maximala antalet samtidiga HTML-till-PDF-konverteringar som tjänsten Generate PDF kan utföra. Standardvärdet för den här inställningen (rekommenderas för enprocessorsystem) är 3, som du kan öka på flerprocessorsystem.

**** OCR-poolstorlek: Poolstorleken för den PaperCaptureService som PDF Generator använder för OCR. Standardvärdet för den här inställningen (rekommenderas för enprocessorsystem) är 3, som du kan öka på flerprocessorsystem. Den här inställningen gäller endast Windows-system.

**** Reservteckensnittsfamilj för konvertering från HTML till PDF: Namnet på den teckensnittsfamilj som ska användas i PDF-dokument när teckensnittet som används i den ursprungliga HTML-koden inte är tillgängligt för AEM-formulärservern. Ange en teckensnittsfamilj om du förväntar dig att konvertera HTML-sidor som använder otillgängliga teckensnitt. På sidor som skapats på regionala språk kan t.ex. otillgängliga teckensnitt användas.

**Återförsökslogik för systemspecifika konverteringar** styr återskapande av PDF-filer om det första konverteringsförsöket har misslyckats:

**Inget nytt försök**

Försök inte konvertera PDF igen om det första konverteringsförsöket har misslyckats

**Försök igen**

Försök konvertera PDF igen oavsett om tidsgränsen har nåtts eller inte. Standardtidsgränsen för det första försöket är 270-tal.

**Försök igen om tiden tillåter**

Försök konvertera PDF igen om den tid som förbrukats för det första konverteringsförsöket var kortare än den angivna tidsgränsen. Om tidsgränsen till exempel är 270 och det första försöket är 200-tal försöker PDF-generatorn konvertera igen. Om det första försöket självt förbrukade 270-talet kommer konverteringen inte att försökas igen.

## Guides ES4 Utilities service settings {#guides-es4-utilities-service-settings}

När du skapar en stödlinje bäddas vissa resurser, till exempel en definition av stödlinjen, in i stödlinjen. Resurser kan också finnas som referenser till programresurser som lagras lokalt eller på AEM-formulärservern. Handboken innehåller inga data, och värdena för sändningsplatsen och indata passar inte för alla externa miljöer.

I de flesta fall räcker standardåtergivningstjänsten för stödlinjer för att förbereda en guide för användning i arbetsytor eller andra externa miljöer. (I vyn Tjänster i Workbench är standardtjänsten Guides (system)/Processes/Render Guide - 1.0.) Med tjänsten Guide Utilities ( `GuidesUtility`) kan du vid behov skapa en anpassad process för återgivning av en guide.

Med guideverktygen kan du lägga till följande guideåtergivningsåtgärder i en process:

* Avgör om det finns data att fylla i guiden med
* Bädda in stödlinjedata eller konvertera dem till en länk
* Konvertera refererat innehåll till URL:er som är externt tillgängliga
* Ersätta värden i ett HTML-dokument eller en annan wrapper, eller konvertera dem till URL:er som är externt tillgängliga
* Ange sändningsplats
* Ange indatavärden
* Skapa en parameter som representerar refererat innehåll
* Om det finns tillgängliga variationer anger du en variant

Standardvärdena för tjänsten Guide Utilities stöder de flesta fall. Om det behövs kan du dock ändra följande värden.

**** publicPaths:Det här alternativet har tagits bort. Använd inte det här alternativet med AEM-formulär.

**** pathInfoExpiryInSeconds: Det intervall efter vilket en begäran om sökvägsinformation från en klient upphör att gälla. Standardvärdet är 1.

**** marginExpiryInSeconds: Det intervall efter vilket en begäran om säkerhet från en kund upphör att gälla. Standardvärdet är 315576000.

**** mismatchExpiryInSeconds: Det intervall efter vilket en begäran om säkerhet från en kund upphör att gälla när eTag (enhetstagg) inte matchar. (En e-tagg är en HTTP-svarshuvud.) Standardvärdet är 1.

**** guideContext: The context root of the Guides web application. Matchar det värde som angetts med webbprogrammet för stödlinjer. Standardvärdet är /Guides/.

**** secureRandomAlgorithm: Den algoritm som ska användas när nycklar och identifierare genereras. Det här värdet skickas till metoden getInstance i klassen SecureRandom Java. Standardvärdet är SHA1PRNG.

**** idBytes: Antalet slumpmässiga byte som ska användas för en nyckelidentifierare. Standardvärdet är 6.

**** macAlgorithm: MAC-algoritmen (Message Authentication Code) som ska användas för verifiering av sammansatt URL. Den här metoden skickas till metoden getInstance i Mac-klassen. Standardvärdet är HmacSHA1.

**** macRefreshIntervalInMinutes: Den tid en nyckel är aktiv. När en nyckel har varit aktiv för det här intervallet genereras en ny nyckel. Den nya tangenten blir aktiv. Den tidigare aktiva nyckeln behålls för 10 % av uppdateringsintervallet. Detta beteende gör att URL:er som genereras med den gamla nyckeln kan fortsätta att fungera i hela nyckelbytet. Standardvärdet är 144000.

**** macOverlapIntervalInMinutes: Den tid som den föregående nyckeln förblir giltig efter att en ny har genererats. Standardvärdet är 1 440 minuter (1 dag).

**** macKeySeed: Ett dirigeringsvärde för generering av säker URL. När det här alternativet är valt uppdateras aldrig nyckeln. Om du anger samma startvärde på olika servrar genereras säkra URL:er som är kompatibla. Detta kan vara användbart om flera formulärservrar används bakom en belastningsutjämnare. Ange en slumpmässig sekvens med tecken och siffror som startvärde.

### Använda stödlinjer i ett serverkluster {#using-guides-in-a-server-cluster}

Rendering a Guide in a server Cluster that does not use sticky sessions fails with a NullPointerException. En begäran om stödlinjer utnyttjar säkra URL:er som som standard är unika för den server som de genereras på. I ett kluster som använder kladdiga sessioner dirigeras alla efterföljande begäranden för den sessionen eller användaren enbart till servern efter att en begäran träffar en nod i klustret, och allt är ok. I ett kluster som inte använder klibbiga sessioner kan efterföljande begäranden påverka alla servrar i klustret. Om servern som begäran träffar på inte är den ursprungliga servern, kan de inte matcha den säkra URL:en.

Om du använder stödlinjer i ett serverkluster som inte använder kladdiga sessioner, anger du värdet macKeySeed för tjänsten GuidesUtility och stoppar och startar sedan klustret.

Värdet macKeySeed är startvärdet för den slumpmässiga talgeneratorn som används för att generera säkra URL:er. Om du anger det här värdet initierar varje klusternod den slumpmässiga talgeneratorn på samma sätt och får tillgång till samma säkra URL:er. Du kan använda valfri slumpmässig sträng för detta dirigerade värde.

Ändra värdet för macKeySeed när du behöver uppdatera säkra URL:er. Uppdatering av säkra URL:er beror på din säkerhetsprincip och liknar uppdateringsprincipen för ändring av huvudrotlösenordet för servern. macSeedValue är detsamma som huvudlösenordet för säkra URL:er, eftersom det används för att generera ett nytt unikt slumpmässigt nummer som kan användas för säker URL-generering och hämtning.

Du måste starta om klustret eftersom macSeedValue är skrivskyddat när datorn startas. Alla noder måste startas om för att kunna läsa värdet, eftersom de använder det oberoende av varandra för att initiera sina interna slumptal med startvärdet.

## JDBC-tjänstinställningar {#jdbc-service-settings}

JDBC-tjänsten ( `JdbcService`) möjliggör för processer att interagera med databaser.

Följande inställning är tillgänglig för JDBC-tjänsten.

**** Datakällans namn: Ett strängvärde som representerar JNDI-namnet på datakällan som ska användas för att ansluta till databasservern. Datakällan måste definieras på den programserver som är värd för formulärservern. Standardvärdet är JNDI-namnet på datakällan för AEM-formulärdatabasen.

## JMS-tjänstinställningar {#jms-service-settings}

JMS-tjänsten ( `JMS`) möjliggör interaktion med Java Messaging System-leverantörer (JMS) som implementerar både peka-till-punkt-meddelanden och publicerar/prenumererar-meddelanden.

Konfigurera JMS-tjänsten med standardegenskaper så att tjänståtgärderna kan ansluta till och interagera med en JMS-provider och en associerad JNDI-tjänst. Värdena för tjänsteegenskaperna ställs in på standardvärden baserat på JBoss Application Server. Ändra dessa värden om du använder en annan programserver som värd för AEM-formulär.

Följande inställningar är tillgängliga för JMS-tjänsten.

**** Provider-URL: URL för JNDI-tjänstprovidern. Standardvärdet baseras på JBoss-programservern. Följande URL är standardvärden för de programservrar som AEM-formulär stöder:

**** JBoss: `<server name>:1099`

**** WebLogic: `<server name>:7001`

**** WebSphere: `<server name>:2809`

**** JNDI-användarnamn: Användarnamnet för det konto som ska användas för autentisering med JNDI-tjänstprovidern som används för att söka efter kö- och ämnesnamn. Standardvärdet är gäst.

**** JNDI-lösenord: Lösenordet som är associerat med det användarnamn som har angetts för JNDI-användarnamn. Standardvärdet är gäst.

**** Initial Context Factory: Den Java-klass som ska användas som inledande kontextfabrik. JMS-tjänsten använder den här klassen för att skapa en inledande kontext, som är utgångspunkten för att matcha namn på ämnen och köer. Standardvärdet är den inledande kontextfabriken för JMS-tjänsten på JBoss. Följande klasser är de inledande kontextfabrikerna för de programservrar som AEM-formulär har stöd för:

**** JBoss: org.jnp.interfaces.NamingContextFactory

**** WebLogic: weblogic.jndi.WLInitialContextFactory

**** WebSphere: com.ibm.websphere.naming.WsnInitialContextFactory

**** Användarnamn för anslutning: Lösenordet som är associerat med användarnamnet som har angetts för anslutningsanvändarnamnet. Standardvärdet är gäst.

**** Lösenord för anslutning: Lösenordet som är associerat med användarnamnet som har angetts för anslutningsanvändarnamnet. Standardvärdet är gäst.

**** Andra egenskaper: Egenskapsnamn och värdepar som du kan skicka till JNDI-tjänstleverantören. Dessa egenskaper beror på implementeringen och konfigurationen av providern som du använder.

Egenskapsnamnet och värdepar avgränsas med semikolon **;**. I följande text visas det värde som skulle ha angetts för två egenskaper med namnen name1 och name2, med värdena value1 och value2:

`name1=value1;name2=value2`

## LDAP-tjänstinställningar {#ldap-service-settings}

LDAP-tjänsten ( `LDAPService`) innehåller åtgärder för att fråga efter LDAP-kataloger. LDAP-kataloger används vanligtvis för att lagra information om personer, grupper och tjänster i en organisation.

Följande inställningar är tillgängliga för LDAP-tjänsten.

**** Initial Context Factory: Den Java-klass som ska användas som kontextfabrik. Den här klassen används för att skapa en anslutning till LDAP-servern. Standardvärdet är com.sun.jndi.ldap.LdapCtxFactory, vilket är lämpligt för de flesta LDAP-servrar.

**** Provider-URL: Den URL som ska användas för att ansluta till LDAP-tjänsten. Värdets format är `ldap://server name:port`

*servernamn* är namnet på den dator som är värd för LDAP-servern

*port* är den kommunikationsport som LDAP-tjänsten använder. Standardvärdet är 389, som är standardporten som används för LDAP-anslutningar.

**** Användarnamn: Användarnamnet för användarkontot som ska användas för att logga in på LDAP-servern. Användarkontot måste ha behörighet att ansluta till servern och läsa informationen i LDAP-katalogen.

Beroende på LDAP-servern kan användarnamnet vara ett enkelt användarnamn, till exempel `myname` eller ett unikt namn, till exempel `cn=myname,cn=users,dc=myorg`.

**** Lösenord: Lösenordet som motsvarar användarnamnet som anges för inställningen Användarnamn.

**** Andra egenskaper: Ett strängvärde som representerar andra egenskaper och deras motsvarande värden som du kan ange för LDAP-servern. Värdet har följande format:

`property=value;property=value;...`

## Inställningar för konfigurationstjänsten för Microsoft SharePoint {#microsoft-sharepoint-configuration-service-settings}

Med konfigurationstjänsten för Microsoft SharePoint `(MSSharePointConfigService)`kan du ange autentiseringsuppgifter för den AEM-formuläranvändare som har personifieringsbehörigheter. Mer information om personifieringsbehörigheter finns i [Konfigurera anslutningsprogrammet för Microsoft SharePoint](https://help.adobe.com/en_US/AEMForms/6.1/SharePointConfig/index.html).

Följande inställningar är tillgängliga för konfigurationstjänsten för Microsoft SharePoint:

* Användarnamn för en användare med personifieringsbehörigheter
* Lösenord för ovanstående användare

**Aktivera SSL (HTTPS):**

**** Live-tid: Hur länge (i sekunder) som den här provisioneringsprofilen är giltig och cachelagras på klienten. Standardvärdet är 86400 (24 timmar). När ett klientprogram synkroniseras med servern och den angivna tiden har gått, begär klientprogrammet en ny provisioneringsprofil från servern.

**** Kryptering: Anger om data som lagras på den mobila enheten ska krypteras.

**** Formulärprogram: Aktiverar formulärfunktionen i mobilklientprogrammen. När det här alternativet är markerat kan användare öppna formulär och initiera processer från sina mobila enheter.

**** Aktivitetsprogram: Aktiverar funktionen Uppgifter i mobilklientprogrammen. När det här alternativet är markerat kan användare komma åt sina uppgiftslistor och slutföra uppgifter från sina mobila enheter.

**** Content Services Application: Aktiverar Content Services-funktionen i mobilklientprogrammet. Den här funktionen är bara tillgänglig för iOS. När det här alternativet är markerat kan iPhone- och iPad-användare komma åt filer som lagras i organisationens WebDAV-server.

**** Offlinesupport: Gör det möjligt för användare att fortsätta använda mobilklientprogrammen även när de inte har någon anslutning till servern (t.ex. när de är utanför cellområdet eller i flygplansläge). Användarna måste även aktivera offlinesupport på sina mobila enheter. Den här funktionen är tillgänglig för Android- och iOS-enheter. Som standard är den här funktionen inaktiverad.

**Obs**: *Om offlinesupport har aktiverats och sedan inaktiveras uppdateras användarnas provisioneringsprofiler omedelbart, eller så snart de är online. Om en användare har arbetat offline återgår alla väntande uppgifter till uppgiftslistan och alla objekt i kön, inklusive väntande formulär, uppgifter och formulär som innehåller valideringsfel, tas bort från kön.*

**** Android: Tillåter Android-enheter att ansluta till servern.

**** Apple iOS: Tillåter iPhone och iPad att ansluta till servern.

**** AIR: Tillåter att enheter som kör program baserade på Adobe AIR® ansluter till servern.

**** BlackBerry: Tillåter BlackBerry-enheter att ansluta till servern.

**** Android Microsoft Exchange ActiveSync krävs: Anger om Microsoft Exchange ActiveSync Policy Manager (EAS) måste vara installerat och aktivt på Android-enheter. När det här alternativet är markerat måste EAS användas på Android-enheten. När det här alternativet inte är markerat utförs ingen kontroll, även om andra krav fortfarande gäller.

**** Minsta PIN-kodslängd för Android: Android-enheter måste ha en global inställning som tvingar PIN-koden eller lösenordet att vara minst så lång. Det räcker inte att bara ha en PIN-kod med den angivna längden. PIN-kodens längd måste framtvingas av systemet så att användarna inte kan ta bort eller korta ned PIN-koden senare. Standardvärdet är 4.

**** Maximalt antal lösenordsförsök för Android innan rensning: Android-enheter har en global inställning som rensar systemet efter ett angivet antal ogiltiga lösenordsförsök. Den här globala inställningen är aktiverad och lika med eller lägre än värdet som anges här. Standardvärdet är 5.

**** Android-rensning vid borttagning: Anger vad som händer när en principöverträdelse inträffar på en Android-enhet. När det här alternativet är markerat tas kontot bort. När det här alternativet inte är markerat tas lösenordet för det lagrade kontot och cachelagrade data bort. Inga fler synkroniseringsförsök görs förrän användaren åtgärdar principöverträdelsen.

## Inställningar för utdatatjänst {#output-service-settings}

Med Output Service `(OutputService)`kan du sammanfoga XML-formulärdata med en formulärdesign som skapats i AEM Forms Designer för att skapa en dokumentutdataström i något av följande format:

* En PDF- eller PDF/A-dokumentutdataström.
* En Adobe PostScript-utdataström.
* En PCL-utdataström (Printer Control Language).
* En ZPL-utdataström (Zebra Programming Language).

Utdataströmmen kan skickas till en nätverksskrivare, en lokal skrivare eller en diskfil. När du använder utdatatjänsten som en del av en process kan du även skicka utdataströmmen till en e-postmottagare som en bifogad fil.

Följande inställningar är tillgängliga för utdatatjänsten.

**** Transaktionstyp: Anger hur en transaktionskontext ska spridas till en åtgärd:

**** Obligatoriskt: stöder en transaktionskontext om en sådan redan finns, i annat fall skapas en ny transaktionskontext. Detta är standardvärdet.

**** Kräver nytt: Skapar alltid en ny transaktionskontext. Om det finns en aktiv transaktionskontext pausas den.

**** Timeout för transaktion (i sek): Antalet sekunder som den underliggande transaktionsprovidern väntar innan en transaktion som omsluter den här åtgärden återställs. Det här värdet ignoreras om en befintlig transaktionskontext sprids.

När du bearbetar stora datafiler eller arbetar på en server med många operativsystem kan det vara nödvändigt att öka tidsgränsen för Output-tjänsten. Om du vill ändra timeout-värdet kontrollerar du att maskinvaruservrarna har tillräckligt med minne och att minnet är tillgängligt för Java Application Server-heap. Standardvärdet är `180`.

## Inställningar för PDFG Config-tjänsten {#pdfg-config-service-settings}

Följande inställningar är tillgängliga för PDFG Config-tjänsten ( `PDFGConfigService`).

**** Katalog för alternativ för användarjobb: Sökvägen till filsystemmappen där c-tjänsten skriver de jobbalternativsfiler som är tillgängliga för Acrobat Pro Extended. Standardvärdet är [user.home]/Application Data/Adobe/Adobe PDF/Settings.

**** PS-startkatalog: Sökvägen till filsystemmappen där de startfiler som krävs av Adobe Acrobat Distiller sparas. Standardvärdet är [user.home]/Application Data/Adobe/Adobe PDF/Distiller/Startup.

**** PS-startfil: Namnet på den startfil som krävs av Adobe Acrobat Distiller. Standardvärdet är example.ps.

**** Timeout för serverkonvertering: Den maximala tidsgränsen för jobbkonvertering (i sekunder) för tjänsten Generera PDF och Distiller. Den här inställningen begränsar den maximala konverteringstimeout som kan anges i filen config.xml och i administrationskonsolsidorna för PDF Generator. Standardvärdet är 270.

**** Serverns globala timeout: Vid PDF-konvertering tar en formulärserver hänsyn till timeoutgränsen. Konfigurera timeout-värdet för att lösa problemet.

**** Prefix för jobbalternativ: Ett prefix som används av tjänsten Generera PDF för att lägga till en kort sträng i jobbalternativsfilerna som skapas temporärt för Acrobat Distiller. Standardvärdet är pdfg.

**** Icke-Unicode-appar: En kommaavgränsad lista med programnamn som är kända för att inte vara Unicode-kompatibla. Listan är förifylld med namnen på flera program, som har stöd för i förväg konfigurerats i PDF Generator. Om du väljer att lägga till stöd för PDF-konverteringar via andra tredjepartsprogram som inte kan hantera Unicode måste du lägga till dem i listan. Standardvärdet är AutoCAD, Excel, PowerPoint, Project, Publisher, Visio, Word, WordPerfect.

**** Antal servertrådpooler: Styr storleken på den trådpool som tjänsten Generate PDF använder internt för att hantera HTML-till-PDF-konverteringsbegäranden som innefattar spikning (konvertering av länkade sidor som är tillgängliga från huvudsidan). Standardvärdet är 20.

**** Sekunder för PDFG-rensningsgenomsökning: Mer information finns i avsnittet Sekunder för jobbförfallodatum.

**** Utgångsdatum i sekunder för jobb: Tjänsten Generate PDF tar bort indatafiler så snart de har konverterats. Utdatafilerna sparas tillfälligt under en tid som bestäms av inställningarna Sekunder för PDFG-rensning och Sekunder för jobbförfallodatum.

Inställningen Sekunder för förfallodatum för jobb anger hur gammal en fil eller tom mapp måste vara innan den kan tas bort. Inställningen Sekunder för PDFG-rensningsgenomsökning anger hur ofta en rensningstråd söker igenom de tillfälliga mapparna efter filer som kan tas bort.

Om t.ex. Förfallotid i sekunder för jobb är inställt på 100 och PDFG-rensningsgenomsökningssekunder är inställt på 200, körs rensningstråden var 200:e sekund och tar bort filer som är 100 sekunder eller äldre.

Standardvärdet för sekundära PDFG-rensningsgenomsökningar är `43200` (12 timmar). Standardvärdet för Förfallotid för jobb är `86400` (24 timmar).

**** Standardspråk: Används för att åsidosätta standardspråkområdet (land + språk) på servern där tjänsten Generera PDF är distribuerad. Om den här parametern inte är angiven bestäms standardspråket av det operativsystem som tjänsten distribueras till. Den här parametern styr vilket språk felmeddelandena returneras till API:erna.

## inställningar för datatjänsttjänst för formulärarbetsflöde {#forms-workflow-data-services-service-settings}

Följande tjänster utökar Data Services och visar sammansättningar som Workspace använder för att kommunicera med servern. Ändra inte konfigurationsalternativen för de här tjänsterna om du inte har fått instruktioner om att göra det av Adobe Support. Dessa tjänster är inte avsedda för direkt åtkomst:

* `ProcessManagementLcdsAttachmentService`
* `ProcessManagementLcdsPropertyService`
* `ProcessManagementLcdsTaskService`

## Fjärrtjänstinställningar {#remoting-service-settings}

De flesta tjänster är konfigurerade så att du kan komma åt dem via (borttaget för AEM-formulär) AEM Forms Remoting. Mer information om (Borttagning för AEM-formulär) AEM-formulär finns i [Programmering med AEM-formulär](https://adobe.com/go/learn_aemforms_programming_63).

Följande inställningar är tillgängliga för tjänsten Remoting.

**** Autentiseringsmetod för Flex-klient: Bestämmer vilken typ av svar som servern skickar tillbaka till klienten när den anropade tjänsten är säkerhetsaktiverad, den anropade åtgärden inte stöder anonyma anrop och klienten skickar antingen inga eller ogiltiga autentiseringsuppgifter. Välj Anpassad eller Grundläggande. Standardvärdet är Grundläggande.

**** Tillåt serialisering av icke-serialiserbara klasser: De flesta slutpunkter för AEM-formulär tillåter endast serialiserbara klasser att användas för anrop. I äldre versioner tillät slutpunkten Remoting icke-serialiserbara klasser att användas för anrop från Flex-baserade klienter. För att förhindra en säkerhetslucka som beskrivs i APS11-15 har detta ändrats. Markera den här kryssrutan om du vill fortsätta använda icke-serialiserbara klasser med slutpunkten för Flex Remoting.

## Inställningar för databastjänst {#repository-service-settings}

Databastjänsten ( `RepositoryService`) tillhandahåller tjänster för lagring och hantering av resurser i AEM-formulär. När utvecklare skapar ett program kan de distribuera resurserna i databasen i stället för i ett filsystem. Materialet kan innehålla alla typer av material, inklusive XML-formulär, PDF-formulär (inklusive Acrobat-formulär), formulärfragment, bilder, profiler, profiler, SWF-filer, DDX-filer, XML-scheman, WSDL-filer och testdata.

Du kan använda standarddatabasen som ingår i AEM-formulär eller en tredjepartsdatabas (EMC Documentum Content Server, IBM FileNet Content Manager eller IBM Content Manager).

Databasprovidertjänsten är en tjänstdelegat som fungerar som gränssnitt till en providertjänst. Detta gör att du kan ansluta till ett vanligt API och inte behöver vara medveten om vilken providertjänst som implementerar lagringsfunktionerna. Databasprovidertjänsten tillhandahåller databaslagring för resurserna för databastjänsten.

Följande inställning är tillgänglig för databastjänsten.

**** Providertjänst: Namnet på den tjänst som används som lagringsprovider. Standardvärdet är RepositoryProviderService.

## Inställningar för signaturtjänst {#signature-service-settings}

Signaturtjänsten ( `SignatureService`) gör det möjligt för er att skydda säkerheten och integriteten i de Adobe PDF-dokument som ni distribuerar och tar emot. Den här tjänsten använder digitala signaturer och certifiering för att säkerställa att dokumenten inte ändras. Om du ändrar ett dokument bryts signaturen. Eftersom säkerhetsfunktionerna tillämpas på själva dokumentet förblir dokumentet säkert och kontrollerat under hela sin livscykel. utanför brandväggen, när den laddas ned offline och när den skickas tillbaka till din organisation.

Följande inställningar är tillgängliga för signaturtjänsten.

**** Namn på fjärr-HSM SPI-tjänsten: Det här alternativet används när HSM är installerat på en fjärrdator. Ange det här alternativet när AEM-formulär installeras i ett 64-bitars Windows och du använder HSM-enheter för signering.

**** URL för fjärr-HSM-webbtjänsten: Ange det här alternativet när AEM-formulär installeras i 64-bitars Windows och du använder HSM-enheter för signering.

**** Certifiering för att inkludera formulärinläsningsändringar: När det här alternativet är markerat certifieras XFA-formulärstatusen utöver XFA-mallen. Observera att aktivering av det här alternativet kan ha en negativ inverkan på prestandan. Standardvärdet är true.

**** Kör JavaScript-skript för dokument: Anger om dokument-JavaScript-skript ska köras under signeringsåtgärder. Standardvärdet är false.

**** Bearbeta dokument med kompatibilitet med Acrobat 9: Anger om Acrobat 9-kompatibilitet ska aktiveras. Om du till exempel väljer det här alternativet aktiveras Synlig certifiering i dynamiska PDF-filer. Standardvärdet är false.

**** Bädda in spärrinformation vid undertecknande: Anger om spärrinformation bäddas in när PDF-dokumentet signeras. Standardvärdet är false.

**** Bädda in återkallningsinformation vid certifiering: Anger om återkallningsinformationen bäddas in när PDF-dokumentet certifieras. Standardvärdet är false.

**** Tvinga inbäddning av återkallningsinformation för alla certifikat vid undertecknande/certifiering: Anger om en signerings- eller certifieringsåtgärd misslyckas om giltig återkallningsinformation för alla certifikat inte bäddas in. Observera att om ett certifikat inte innehåller någon CRL- eller OCSP-information, anses det vara giltigt, även om ingen återkallningsinformation hämtas. Standardvärdet är false.

**** Återkallningskontrollordning: Anger ordningen för spärrkontroll när det är möjligt att kontrollera detta med hjälp av både CRL- (Certificate Revocation List) och OCSP-mekanismer (Online Certificate Status Protocol). Standardvärdet är OCSPFirst.

**** Maximal storlek för information om återkallningsarkivering: Den största tillåtna storleken för arkiveringsinformation för återkallning i kB. AEM-formulär försöker lagra så mycket spärrinformation som möjligt utan att överskrida gränsen. Standardvärdet är 10 kB.

**** Supportsignaturer som skapats i PreRelease-versioner av Adobe-produkter: När det här alternativet är markerat valideras signaturer som skapats med en förhandsversion av Adobe-produkter korrekt. Standardvärdet är false.

**** Alternativ för verifieringstid: Anger tidpunkten för verifiering av en signerares certifikat. Standardvärdet är Säker tid för annan aktuell tid.

**** Använd återkallningsinformation som arkiverats i signaturen under validering: Anger om den spärrinformation som arkiveras med signaturen används för spärrkontroll. Standardvärdet är true.

**** Använd valideringsinformation som lagras i dokumentet för validering av signaturer: När det här alternativet är markerat används den valideringsinformation (inklusive information om återkallning och tidsstämplar) som är inbäddad i dokumentet för att validera signaturer. Standardvärdet är true.

**** Högsta antal tillåtna kapslade verifieringssessioner: Högsta tillåtna antal kapslade verifieringssessioner. AEM-formulär använder det här värdet för att förhindra en oändlig slinga när OCSP- eller CRL-signerarcertifikaten verifieras när OCSP- eller CRL-certifikatet inte är korrekt konfigurerat. Standardvärdet är 10.

**** Maximal låsskevning för verifiering: Den maximala tiden, i minuter, som signeringstiden kan vara efter valideringstiden. Om klockskevningen är större än det här värdet är signaturen inte giltig. Standardvärdet är 65 minuter.

**** Certifikatets livstidscache: Livslängden för ett certifikat som hämtats online eller på annat sätt i cachen. Standardvärdet är 1 dag.

### Transportalternativ {#transport-options}

**** Proxyvärd: URL:en för proxyvärden. Används endast om ett giltigt värde anges. Inget standardvärde.

**** Proxyport: Proxyporten. Ange ett giltigt portnummer mellan 0 och 65535. Standardvärdet är 80.

**** Proxyinloggningsanvändarnamn: Användarnamnet för proxyinloggning. Används bara om ett giltigt värde har angetts för proxyvärden och proxyport. Inget standardvärde.

**** Lösenord för proxyinloggning: Proxyinloggningslösenordet. Används bara om ett giltigt värde anges för proxyvärden, proxyporten och användarnamnet för proxyinloggning. Inget standardvärde.

**** Maximal hämtningsgräns: Den maximala mängden data, i MB, som kan tas emot per anslutning. Det minsta värdet är 1 MB och det högsta värdet är 1 024 MB. Standardvärdet är 16 MB.

**** Anslutningstid ut: Den längsta väntetiden, i sekunder, för att upprätta en ny anslutning. Det minsta värdet är 1 och det högsta värdet är 300. Standardvärdet är 5.

**** Sockettimeout: Maximal väntetid, i sekunder, innan en sockettimeout (i väntan på dataöverföring) inträffar. Det minsta värdet är 1 och det högsta värdet är 3 600. Standardvärdet är 30.

### Alternativ för validering av sökväg {#path-validation-options}

**** Kräv explicit princip: Anger om sökvägen måste vara giltig för minst en av de certifikatprofiler som är kopplade till signerarcertifikatets rotcertifikatsutfärdare. Standardvärdet är false.

**** Hindra alla profiler: Anger om objektidentifieraren för princip (OID) ska behandlas om den ingår i ett certifikat. Standardvärdet är false.

**** Hindra principmappning: Anger om principmappning tillåts i certifieringssökvägen. Standardvärdet är false.

**** Markera alla banor: Anger om alla sökvägar ska valideras eller om valideringen ska avbrytas efter att den första giltiga sökvägen har hittats. Välj true eller false. Standardvärdet är false.

**** LDAP-server: LDAP-servern som används för att söka efter certifikat för sökvägsvalidering. Inget standardvärde.

**** Följ URI:er i AIA-certifikat: Anger om URI:er (Uniform Resource Identifiers) i AIA-certifikat behandlas vid sökvägsidentifiering. Standardvärdet är false.

**** Tillägg för grundläggande begränsningar krävs i certifikatutfärdarcertifikat: Anger om certifikatutfärdarens grundläggande begränsningscertifikattillägg måste finnas för certifikatutfärdarcertifikat. Vissa tidiga tyska certifierade rotcertifikat (7 och tidigare) är inte kompatibla med RFC 3280 och innehåller inte det grundläggande begränsningstillägget. Om det är känt att en användares EE-certifikat kan härledas till en sådan tysk rot avmarkerar du den här kryssrutan. Standardvärdet är true.

**** Kräv giltig certifikatsignatur när kedjan byggs: Anger om kedjebyggaren kräver giltiga signaturer på certifikat som används för att skapa kedjor. När den här kryssrutan är markerad kommer kedjebyggaren inte att skapa kedjor med ogiltiga RSA-signaturer på certifikat. Överväg kedja CA > ICA > EE där certifikatutfärdarens signatur på ett ICA inte är giltig. Om den här inställningen är true stoppas kedjebyggnaden vid ICA och CA inkluderas inte i kedjan. Om den här inställningen är false skapas den fullständiga 3-certifikatskedjan. Den här inställningen påverkar inte DSA-signaturer. Standardvärdet är false.

### Alternativ för tidsstämpelleverantör {#timestamp-provider-options}

**** URL för TSP-server: URL:en för standardtidsstämpelprovidern. Används endast om ett giltigt värde anges. Inget standardvärde.

**** TSP-serveranvändarnamn: Användarnamnet om det krävs av tidsstämpelprovidern. Används bara om ett giltigt värde har angetts för URL:en. Inget standardvärde.

**** TSP-serverlösenord: Lösenordet för ovanstående användarnamn om det krävs av tidsstämpelprovidern. Används bara om ett giltigt värde har angetts för URL:en och användarnamnet. Inget standardvärde.

**** Begär hash-algoritm: Anger den hash-algoritm som ska användas när begäran för tidsstämpelprovidern skapas. Standardvärdet är SHA1.

**** Format för spärrkontroll: Anger det format för spärrkontroll som används för att avgöra pålitlighetsstatus för tidsstämpelproviderns certifikat från den spärrstatus som observerats. Standardvärdet är BestEffort.

**** Send Nonce: Anger om ett nonce skickas med begäran från tidsstämpelprovidern. Ett omedelbart kan vara en tidsstämpel, en besöksräknare på en webbsida eller en speciell markör som är avsedd att begränsa eller förhindra otillåten kopiering eller reproduktion av en fil. Standardvärdet är true.

**** Använd utgångna tidsstämplar vid validering: När det här alternativet är markerat kan utgångna tidsstämplar användas för att hämta valideringstider för signaturer. Standardvärdet är true.

**** TSP-svarsstorlek: Beräknad storlek i byte för TSP-svaret. Det här värdet bör representera den maximala storleken för tidsstämpelsvaret som den konfigurerade tidsstämpelprovidern kan returnera. Ändra inte detta om du inte är helt säker. Det minsta värdet är 60 B och det högsta värdet är 10240 B. Standardvärdet är 4096B.

**Ignorera tidsstämpelservertillägg**: Markera alternativet **Ignorera tidsstämpelservertillägg** om du inte vill att AEM Forms-servern ska kontakta den angivna tidsstämpelservern. Om du väljer det här alternativet undviker du processfel som inträffar på grund av timeout i anslutningen mellan AEM Forms och tidsstämpelservrar.

### Alternativ för listan över spärrade certifikat {#certificate-revocation-list-options}

**** Konsultera lokal URI först: Anger om platsen för listan över återkallade certifikat som anges i lokal URI eller CRL-sökning ska ges företräde framför någon plats som anges i ett certifikat för spärrkontroll. Standardvärdet är false.

**** Lokal URI för CRL-sökning: URL för den lokala CRL-providern. Det här värdet används bara om inställningen Konsult lokal URI första är true. Inget standardvärde.

**** Format för spärrkontroll: Anger det format för spärrkontroll som används för att fastställa pålitlighetsstatusen för CRL-providerns certifikat från den status som observerats för spärrkontroll. Standardvärdet är BestEffort.

**** LDAP-server för CRL-sökning: LDAP-servern använde för att hämta listor över återkallade certifikat (som www.ldap.com). Alla DN-baserade frågor om listor över återkallade certifikat dirigeras till den här servern. Inget standardvärde.

**** Anslut: Anger om du ska ansluta till Internet för att hämta en lista över återkallade certifikat. Om värdet är false genomsöks bara cachelagrade listor över återkallade certifikat (på den lokala hårddisken eller sådana som är inbäddade med signatur). Standardvärdet är true.

**** Ignorera giltighetsdatum: Anger om svarets thisUpdate- och nextUpdate-tider ska ignoreras, vilket förhindrar att dessa tider har en negativ effekt på svarets giltighet. Standardvärdet är false.

**** Kräv AKI-tillägg i CRL: Anger om tillägget för utfärdarens nyckelidentifierare måste inkluderas i en lista över återkallade certifikat. Standardvärdet är false.

### Alternativ för statusprotokoll för onlinecertifikat {#online-certificate-status-protocol-options}

**** URL för OCSP-server: URL för OCSP-standardservern. Om OCSP-servern som anges via den här URL:en används beror på inställningen för alternativet URL till rådgivning. Inget standardvärde.

**** Alternativ för URL till konsult: Styr listan och ordningen för de OCSP-servrar som används för statuskontrollen. Standardvärdet är UseAIAInCert.

**** Format för spärrkontroll: Anger den typ av spärrkontroll som används vid verifiering av OCSP-serverns certifikat. Standardvärdet är CheckIfAvailable.

**** Send Nonce: Anger om ett nonce skickas med OCSP-begäran. Ett omedelbart kan vara en tidsstämpel, en besöksräknare på en webbsida eller en speciell markör som är avsedd att begränsa eller förhindra otillåten kopiering eller reproduktion av en fil. Standardvärdet är true.

**** Maximal tid för skevning av klocka: Maximal tillåten skevning, i minuter, mellan svarstid och lokal tid. Det minsta värdet är 0 och det högsta värdet är 2147483647m. Standardvärdet är 5 m.

**** Svarets varaktighet: Maximal tid, i minuter, för vilken ett förkonstruerat OCSP-svar anses vara giltigt. Det minsta värdet är 1 m och det högsta tillåtna värdet är 2147483647. Standardvärdet är 525600 (ett år).

**** Underteckna OCSP-begäran: Anger om OCSP-begäran ska signeras. Standardvärdet är false.

**** Autentiseringsalias för begärande signerare: Anger det autentiseringsalias som ska användas för att signera OCSP-begäran om signering är aktiverat. Används bara om signering av OCSP-begäran är aktiverat. Inget standardvärde.

**** Anslut: Anger om du ska ansluta till Internet för att utföra spärrkontroll. Standardvärdet är true.

**** Ignorera svarstiderna thisUpdate och nextUpdate: Anger om svarets thisUpdate- och nextUpdate-tider ska ignoreras, vilket förhindrar att dessa tider har en negativ effekt på svarets giltighet. Standardvärdet är false.

**** Tillåt OCSPNoCheck-tillägg: Anger om OCSPNoCheck-tillägget tillåts i svarssigneringscertifikatet. Standardvärdet är true.

**** Kräv OCSP ISIS-MTT CertHash-tillägg: Anger om ett hash-tillägg för certifikatets offentliga nyckel måste inkluderas i OCSP-svar. Standardvärdet är false.

### Felhanteringsalternativ för felsökning {#error-handling-options-for-debugging}

**** Rensa certifikatcache vid nästa API-anrop: Anger om certifikatcachen ska rensas när nästa signaturtjänståtgärd anropas. När åtgärden har anropats återställs det här alternativet till false. Standardvärdet är false.

**** Rensa CRL-cache vid nästa API-anrop: Anger om CRL-cachen ska rensas när nästa signaturtjänståtgärd anropas. När åtgärden har anropats återställs det här alternativet till false. Standardvärdet är false.

**** Rensa OCSP-cache vid nästa API-anrop: Anger om OCSP-cachen ska rensas när nästa signaturtjänståtgärd anropas. När åtgärden har anropats återställs det här alternativet till false. Standardvärdet är false.

## Inställningar för tjänsten Bevakade mappar {#watched-folder-service-settings}

Tjänsten Bevakade mappar ( `WatchedFolder`) konfigurerar attribut som är gemensamma för alla bevakade mappslutpunkter. Det innehåller också standardvärden för bevakade mappslutpunkter. (Se [Konfigurera bevakade mappslutpunkter](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#configuring-watched-folder-endpoints).) Den anropas inte av externa klientprogram eller används i processer som skapats i Workbench.

Följande inställningar är tillgängliga för tjänsten Bevakade mappar.

**** Cron-uttryck: Kronuttrycket som används av kvarts för att schemalägga avsökningen av indatakatalogen.

**** Antal upprepningar: Antalet gånger som indatakatalogen avsöks. Standardantalet för upprepning som ska användas om det här värdet inte anges i slutpunktskonfigurationen. Värdet -1 anger att katalogen genomsöks oändligt. Standardvärdet är -1.

**** Upprepa intervall: Standardvärdet för antal sekunder mellan varje omröstning. Det här värdet används som upprepningsintervall såvida inte ett annat värde anges i konfigurationen för bevakad mappslutpunkt. Standardvärdet är 5. Mer information finns i beskrivningen av inställningen Gruppstorlek.

**** Asynkron: Identifierar anropstypen som asynkron eller synkron. Övergående och synkrona processer kan bara anropas synkront. Standardvärdet är asynkront.

**** Väntetid: Standardvärdet för tid, i sekunder, efter vilken filerna hämtas från indatamapparna. Om filen eller mappen är äldre än den tid som anges i väntetiden hämtas den för bearbetning. Standardvärdet är 0.

**** Batchstorlek: Standardvärdet för antalet filer eller mappar som bearbetas per sökning. Standardvärdet är 2.

Inställningarna Intervall för upprepning och Gruppstorlek avgör hur många filer i Bevakade mappar som tas upp vid varje sökning. Bevakad mapp använder en Quartz-trådpool för att skanna indatamappen. Trådpoolen delas med andra tjänster. Om skanningsintervallet är litet genomsöks indatamappen ofta av trådarna. Om filer ofta placeras i den bevakade mappen bör du hålla sökintervallet litet. Om filerna tas bort sällan bör du använda ett större inläsningsintervall så att de andra tjänsterna kan använda trådarna.

Om det finns en stor mängd filer som tas bort gör du gruppstorleken stor. Om till exempel tjänsten som anropas av den bevakade mappens slutpunkt kan bearbeta 700 filer per minut, och användarna släpper filer i indatamappen med samma hastighet, och du sedan anger värdet 350 för Gruppstorlek och intervallet för upprepning till 30 sekunder, kommer prestandan för bevakad mapp att bli bättre utan att kostnaden för att skanna den bevakade mappen för ofta påverkas.

När filer släpps i den bevakade mappen visas filerna i indata, vilket kan försämra prestanda om skanningen sker varje sekund. Om du ökar skanningsintervallet kan prestandan förbättras. Om volymen för de filer som tas bort är liten justerar du batchstorleken och upprepningsintervallet därefter. Om till exempel 10 filer tas bort varje sekund, kan du försöka med att ange intervallet för upprepning till 1 sekund och gruppstorleken till 10.

I en klusterkonfiguration skalas inte gruppstorleken för en bevakad mappslutpunkt till flera klusternoder. Om batchstorleken till exempel är inställd `2` för ett kluster med två noder och alternativet Begränsning är markerat bearbetar noderna alla filer gruppvis i två istället för i varje nod som bearbetar två filer samtidigt.

**** Skriv över duplicerade filnamn: En boolesk sträng som anger om den bevakade mappen skriver över duplicerade resultatfilnamn och om bevarade dokument med samma namn ska skrivas över.

**** Bevara mapp: Standardvärdet för mappen preserve. Den här mappen används för att kopiera källfilerna till om indata bearbetas korrekt. Värdet kan vara en tom, relativ eller absolut sökväg med ett filmönster enligt beskrivningen för inställningen Resultatmapp.

**** Felmapp: Namnet på den mapp där felfilerna kopieras. Värdet kan vara en tom, relativ eller absolut sökväg med ett filmönster enligt beskrivningen för inställningen Resultatmapp.

**** Resultatmapp: Standardnamnet för resultatmappen. Den här mappen används för att kopiera resultatfilerna till. Värdet kan vara en tom, relativ eller absolut sökväg med följande filmönster.

* %F = filnamnsprefix
* %E = filnamnstillägg
* %Y = år (full)
* %y = år (de två sista siffrorna)
* %M = månad
* %D = dag i månaden
* %d = dag på året
* %H = timme (24-timmars klocka)
* %h = timme (12-timmars klocka)
* %m = minut
* %s = sekund
* %l = millisekund
* %R = slumptal (från 0 till 9)
* %P = process- eller jobb-ID

Om det till exempel är 2009-08-17 och du anger `C:/Test/WF0/failure/%Y/%M/%D/%H/`blir resultatmappen `C:/Test/WF0/failure/2009/07/17/20`.

Om sökvägen inte är absolut men relativ skapas mappen i den bevakade mappen. Mer information om filmönster finns i [Om filmönster](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#about-file-patterns).

***Obs **: Ju mindre resultatmapparna är, desto bättre prestanda blir Bevakade mappar. Om den beräknade inläsningen för den bevakade mappen till exempel är 1 000 filer varje timme kan du testa ett mönster som`result/%Y%M%D%H`så att en ny undermapp skapas varje timme. Om inläsningen är mindre (till exempel 1 000 filer per dag) kan du använda ett mönster som`result/%Y%M%D`.*

**** Scenmapp: Standardnamnet för scenmappen i den bevakade mappen.

**** Indatamapp: Standardnamnet för indatamappen i den bevakade mappen.

**** Bevara vid fel: Om true bevaras originalfilerna i felmappen vid fel.

**** Begränsning: När det här alternativet är markerat begränsas antalet bevakade mappjobb som AEM-formulär bearbetar vid en given tidpunkt. Värdet för Gruppstorlek avgör det maximala antalet jobb (se Om begränsning).

## Inställningar för webbtjänst {#web-service-service-settings}

Med webbtjänsten ( `WebService`) kan processer starta webbtjänståtgärder.

Med webbtjänsten kan processer starta webbtjänståtgärder. En organisation kan till exempel vilja integrera en process för att lagra och hämta information som kontakt- och kontoinformation genom att anropa en tjänsteleverantörs exponerade webbtjänster. Webbtjänsten anropar en angiven webbtjänst och skickar värden för var och en av dess parametrar. Returvärdena från åtgärden sparas sedan i en angiven variabel i en process.

Webbtjänsten interagerar med webbtjänster genom att skicka och ta emot SOAP-meddelanden. Tjänsten stöder även sändning av MIME-, MTOM- och SwaRef-bilagor med SOAP-meddelanden med WS-Attachment-protokollet. Webbtjänstens interaktioner är kompatibla med SAP-system och .NET-webbtjänster.

Följande inställningar är tillgängliga för webbtjänsten.

**** Nyckelarkiv: Den fullständiga sökvägen till nyckelfilen som innehåller den privata nyckel som ska användas för autentisering. Formulärservern måste kunna komma åt filen.

**** Lösenord för nyckelbehållare: Lösenordet för nyckelfilen.

**** Typ av nyckelarkiv: Typ av nyckelbehållare. Ange inget värde för att använda standardnyckelbehållartypen som är konfigurerad för den JVM som kör formulärservern. Annars anger du något av följande värden:

* jks
* pkcs12
* cms
* jceks

**** Trust Store: Den fullständiga sökvägen till förtroendearkivfilen som innehåller den offentliga nyckeln för webbtjänstservern.

**** Lösenord för betrodd lagring: Lösenordet för förvaltarfilen.

**** Typ av förtroendearkiv: Typ av förvaltararkiv. Ange inget värde för att använda standardnyckelbehållartypen som är konfigurerad för den JVM som kör formulärservern. Annars anger du något av följande värden:

* jks
* pkcs12
* cms
* jceks

## Inställningar för XSLT-omvandlingstjänsten {#xslt-transformation-service-settings}

Med XSLT-omvandlingstjänsten ( `XSLTService`) kan processer använda XSLT (Extensible Stylesheet Language Transformations) i XML-dokument.

Följande inställning är tillgänglig för tjänsten XSLT-omvandling.

**** Fabriksnamn: Det fullständiga, kvalificerade namnet på Java-klassen som ska användas för att utföra XSLT-omvandlingar. Om inget värde anges används standardfabriken som är konfigurerad i den Java Virtual Machine som kör formulärservern.

## Ändra säkerhetsinställningar för en tjänst {#modifying-security-settings-for-a-service}

Med formulärservern kan du konfigurera säkerhetsinställningar för varje tjänst, vilket gör att du kan konfigurera detaljerad åtkomstkontroll på en tjänst-för-tjänst-nivå.

Standardsäkerhetsprofiler installeras, som sedan kan konfigureras för att uppfylla dina systembehov. Varje säkerhetsprofil har en associerad domän och skapas antingen på användarnivå eller gruppnivå.

### Ändra säkerhetsinställningar för en tjänst {#modify-security-settings-for-a-service}

1. I administrationskonsolen klickar du på Tjänster > Program och tjänster > Tjänsthantering.
1. Klicka på den tjänst du vill konfigurera på sidan Tjänsthantering.
1. Klicka på fliken Säkerhet.
1. I listan Kräv att anropare autentiserar väljer du antingen Ja eller Nej för att ange om tjänsten kan anropas med eller utan autentiseringsuppgifter.

   Om du väljer Ja måste uppringaren autentiseras och uppringarens huvudnamn måste ha behörighet att anropa tjänsten. I annat fall avvisas anropsförsöket.

   Om du väljer Nej kan anroparen av tjänsten vara autentiserad eller inte. Anropet av tjänsten lyckas alltid eftersom det inte finns någon auktoriseringskontroll.

1. För tjänster som innehåller en eller flera åtgärder som flaggats för anonym åtkomst markerar eller avmarkerar du alternativet Anonym åtkomst tillåten. När anonym åtkomst är aktiverat kan alla användare i systemet anropa åtgärder för tjänsten. Om anonym åtkomst är inaktiverad måste användarna ges behörighet att anropa tjänsten och anropa åtgärder. Användare beviljas dessa behörigheter antingen direkt eller som en del av en grupp som har sådana behörigheter.
1. För vissa tjänster påverkar det användarkonto som utför åtgärden resultatet. I Innehållstjänster (Borttagen) blir till exempel användaren som lagrar innehåll ägare till innehållet, vilket påverkar vem som kan komma åt innehållet senare. Om du använder en process för att lagra innehåll bör du tänka på vilken användare som används för att köra dokumenthanteringstjänsten, eftersom den användaren kommer att äga det lagrade innehållet.

   Om du vill ange den körtidsidentitet som används av en tjänst för att köra åtgärder väljer du Ange Kör som, väljer ett alternativ i den associerade listan och klickar sedan på Spara. Välj bland följande alternativ:

   **** Anropare: Använder samma identitet som användaren som anropade tjänsten.

   **** System: Använder systemanvändaren för att köra tjänsten med fullständig behörighet.

   **** Namngiven användare: Gör att du kan köra tjänsten som en specifik användare. När du väljer det här alternativet klickar du på Välj användare för att visa sidan Välj huvudnamn, där du kan söka efter och välja användaren.

   Om du inte väljer Ange Kör som används standardbeteendet.

   >[!NOTE]
   >
   >Renderings- och skicka-tjänster som används med variablerna xfaForm, Document Form och Form körs alltid med användarkontot i System.

1. Klicka på Lägg till huvudnamn för att ange behörigheter som användare och grupper har för tjänsten.
1. På skärmen Välj huvudnamn visas de användare och grupper som har konfigurerats i Användarhantering. Om användaren eller gruppen som du vill använda inte visas använder du sökfunktionen för att hitta den. Klicka på ett användar- eller gruppnamn.
1. På skärmen Lägg till behörigheter väljer du de behörigheter som ska tilldelas till användaren eller gruppen för den här tjänsten:

   * **** INVOKE_PERM: Så här anropar du alla åtgärder på tjänsten
   * **** MODIFY_CONFIG_PERM: Ändra konfigurationen för en tjänst
   * **** SUPERVISOR_PERM: Så här visar du processinstansdata för en tjänst som skapats från en process
   * **** START_STOP_PERM: Starta och stoppa en tjänst
   * **** ADD_REMOVE_ENDPOINTS_PERM: Lägga till, ta bort och ändra slutpunkter för en tjänst
   * **** CREATE_VERSION_PERM: Skapa en ny version av tjänsten
   * **** DELETE_VERSION_PERM: Så här tar du bort en version av tjänsten
   * **** MODIFY_VERSION_PERM: Ändra en version av tjänsten
   * **** READ_PERM: Så här visar du tjänsten
   * **** PROCESS_OWNER_PERM: För användning i framtida versioner av AEM-formulär. Använd inte den här behörigheten.
   * **** SERVICE_MANAGER_PERM: För användning i framtida versioner av AEM-formulär. Använd inte den här behörigheten.
   * **** SERVICE_AGENT_PERM: För användning i framtida versioner av AEM-formulär. Använd inte den här behörigheten.

1. Klicka på Lägg till

### Ta bort säkerhetsobjektet från en säkerhetsprofil {#remove-the-principal-from-a-security-profile}

1. Välj den tjänst som ska konfigureras på sidan Tjänsthantering.
1. Klicka på fliken **Dokumentskydd** , markera säkerhetsprofilen som ska tas bort och klicka på **Ta bort**.

## Konfigurera poolning för en tjänst {#configuring-pooling-for-a-service}

Varje tjänst kan utnyttja poolfunktionerna för att hantera inkommande anrop. Om du använder en tjänstpool försäkrar du dig om att tjänstinstanser anropas av en enda tråd i taget och återanvänds i alla anropsbegäranden, vilket kan leda till bättre prestanda. Du kan också använda poolning för att ange alternativet Maximalt antal asynkrona tjänstinstanser, som tillåter tjänster att begränsa antalet begäranden som hanteras parallellt.

### Aktivera poolning {#enable-pooling}

1. I administrationskonsolen klickar du på Tjänster > Program och tjänster > Tjänsthantering.
1. Klicka på den tjänst du vill konfigurera på sidan Tjänsthantering.
1. Klicka på fliken Pooling.
1. Välj Sammanslagna instanser för alla begäranden i listan över strategier för behandling av begäranden.
1. Ange poolens inledande storlek i rutan Poolstorlek för initialtjänstinstans. När tjänsten distribueras används det här numret för att fastställa antalet tjänstimplementeringsinstanser som skapas och tilldelas till den kostnadsfria poolen, i väntan på anropsbegäranden. Detta gör att tjänstbehållaren kan svara direkt på anropsbegäranden utan att först behöva initiera en tjänstinstans.
1. I rutan Maximal storlek för tjänstinstanspool anger du maximalt antal instanser i poolen för en viss tjänst. Den här inställningen styr antalet trådar som kan köra en viss tjänst vid en given tidpunkt. Standardvärdet är 0, vilket ger obegränsad poolstorlek.
1. I rutan Maximalt antal asynkrona tjänstinstanser anger du maximalt antal instanser från poolen som kan användas för att hantera asynkrona begäranden vid en given tidpunkt. Med den här inställningen kan tjänsten begränsa antalet begäranden som kan hanteras parallellt.
1. I rutan Timeout för anropsväntetid anger du antalet millisekunder som ska vänta på att en tjänst ska bli tillgänglig för en anropsbegäran. Om du inte anger något värde för den här inställningen är standardvärdet 0, vilket ger ingen väntetid.
1. Klicka på Spara.

### Ta bort poolning {#remove-pooling}

1. I administrationskonsolen klickar du på Tjänster > Program och tjänster > Tjänsthantering.
1. Klicka på den tjänst du vill konfigurera på sidan Tjänsthantering.
1. Klicka på fliken Pooling.
1. Välj antingen Ny instans för varje begäran eller En instans för alla begäranden i listan över strategier för behandling av begäranden.

   **** En instans för alla begäranden: En tjänstinstans skapas och cachelagras när den första begäran kommer in i behållaren. Varje begäran efter den begäran använder samma tjänstinstans för att hantera begäran.

   **** Ny instans för varje begäran: En ny tjänstinstans skapas för varje mottaget anrop.

1. Klicka på Spara.

