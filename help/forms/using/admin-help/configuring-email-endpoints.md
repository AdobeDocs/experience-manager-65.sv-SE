---
title: Konfigurera e-postslutpunkter
seo-title: Konfigurera e-postslutpunkter
description: Lär dig hur du konfigurerar e-postslutpunkter.
seo-description: Lär dig hur du konfigurerar e-postslutpunkter.
uuid: d47bb45b-0e0e-43ca-9e25-e347d0e60206
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_endpoints
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: dcf15c42-9ec6-4d1c-ad41-083aa0b8c7ae
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f

---


# Konfigurera e-postslutpunkter {#configuring-email-endpoints}

Med e-postslutpunkter kan användare anropa en tjänst genom att skicka ett eller flera dokument (som e-postbilagor) till ett angivet e-postkonto. Inkorgen för e-post fungerar som en samlingspunkt för de bifogade filerna. Tjänsten övervakar inkorgen och bearbetar de bifogade filerna. Resultatet av konverteringen vidarebefordras till den användare som är definierad i slutpunkten.

För e-postslutpunkter kan behöriga användare anropa en process genom att skicka filer till rätt konto. Resultatet returneras till den avsändande användaren (som standard) eller till den användare som definierats i slutpunktsinställningarna.

Innan du konfigurerar en e-postslutpunkt skapar du ett POP3- eller IMAP-e-postkonto som ska användas av slutpunkten. Skapa ett separat konto för varje typ av konvertering. Ett konto kan till exempel konfigureras för att generera standarddokument i PDF-format från inkommande bifogade filer, och ett annat konto kan konfigureras för att generera säkra PDF-dokument.

>[!NOTE]
>
>Varje e-postadress får bara mappas till en e-postslutpunkt. Du kan inte konfigurera flera e-postslutpunkter till en enda e-postadress, även om de ytterligare e-postslutpunkterna är inaktiverade.

Alla e-postslutpunkter har konfigurerats med ett auktoriserat användarnamn och lösenord för e-postinkorgen, vilket krävs när tjänsten anropas. E-postkontot skyddas av e-postserversystemet som det är konfigurerat på.

Om dina användare skickar dokument med västerländska europeiska språktecken i namn på fil- och konverteringssökvägar måste de använda ett e-postprogram som har stöd för de kodningstyper som krävs (Latin1 [ISO-8859-1], Västerländsk [Windows]eller UTF-8). Mer information finns i dokumentet *Installera och distribuera AEM-formulär* för programservern.

Konfigurera e-posttjänsten innan du konfigurerar en e-postslutpunkt. (Se [Konfigurera standardinställningar](configuring-email-endpoints.md#configure-default-email-endpoint-settings)för e-postslutpunkter.) E-posttjänstens konfigurationsparametrar har två syften:

* Konfigurera attribut som är gemensamma för alla e-postslutpunkter
* Ange standardvärden för alla e-postslutpunkter

## Konfigurera SSL för en e-postslutpunkt {#configure-ssl-for-an-email-endpoint}

Du kan konfigurera POP3, IMAP eller SMTP så att Secure Sockets Layer (SSL) används för en e-postslutpunkt.

1. På e-postservern aktiverar du SSL för POP3, IMAP eller SMTP enligt tillverkarens dokumentation.
1. Exportera ett klientcertifikat från e-postservern.
1. Använd nyckelverktygsprogrammet för att importera klientcertifikatfilen till programserverns JVM-certifikatarkiv (Java Virtual Machine). Hur det här steget utförs beror på sökvägarna till JVM och klientinstallation.

   Om du till exempel använder en standardinstallation av Oracle WebLogic Server med JDK 1.5.0 i Microsoft Windows Server® 2003 skriver du följande text i en kommandotolk:

   `keytool -import -file client_certificate -alias myalias -keystore BEA_HOME\jdk150_04\jre\security\cacerts`

1. Ange lösenordet när du uppmanas till det (för Java är standardlösenordet `changeit`). Du får ett meddelande om att certifikatet har importerats.
1. Använd administrationskonsolen för att lägga till e-postslutpunkten till tjänsten.
1. Skapa e-postslutpunkten i administrationskonsolen. När du konfigurerar slutpunktsinställningarna väljer du POP3/IMAP SSL aktiverat för inkommande meddelanden och SMTP SSL aktiverat för utgående meddelanden, och ändrar portegenskaperna därefter.

>[!NOTE]
>
>Tips: Om du får problem när du använder SSL kan du använda en e-postklient som Microsoft Outlook för att kontrollera om den kan komma åt e-postservern med SSL. Om e-postklienten inte har åtkomst till e-postservern är problemet relaterat till konfigurationen av antingen ditt certifikat eller e-postservern.

## Konfigurera standardinställningar för e-postslutpunkt {#configure-default-email-endpoint-settings}

Du kan använda sidan Tjänsthantering för att konfigurera attribut som är gemensamma för alla e-postslutpunkter och för att ange standardvärden för alla e-postslutpunkter.

För att formulärarbetsflöden ska kunna ta emot och hantera inkommande e-postmeddelanden från användare måste du skapa en e-postslutpunkt för tjänsten Complete Task. Den här e-postslutpunkten kräver ytterligare inställningar, vilket beskrivs i [Skapa en e-postslutpunkt för tjänsten](configuring-email-endpoints.md#create-an-email-endpoint-for-the-complete-task-service)Fullständig aktivitet.

### Ändra standardvärden för e-postslutpunkter {#change-the-default-values-for-email-endpoints}

1. I administrationskonsolen klickar du på Tjänster > Program och tjänster > Tjänsthantering.
1. Klicka på E-post på sidan Tjänsthantering: 1.0 (komponent-ID:t är com.adobe.idp.dsc.provider.service.email.Email).
1. Ange standardinställningarna för e-postslutpunkten på fliken Konfiguration och klicka sedan på Spara.

### Standardinställningar för e-postslutpunkt {#default-email-endpoint-settings}

**Cron-uttryck:** Kronuttrycket som används av kvarts för att schemalägga avsökningen av indatakatalogen.

**Upprepa intervall:** Antalet gånger som katalogavsökningen upprepas. Standardintervallet för upprepning är i sekunder om det här värdet inte anges i slutpunktskonfigurationen. Standardvärdet är 10. Värdet får inte vara mindre än 10.

**Antal upprepningar:** Antalet gånger som indatakatalogen avsöks. Standardantalet för upprepning som ska användas om det här värdet inte anges i slutpunktskonfigurationen. Värdet -1 anger att katalogen genomsöks oändligt. Standardvärdet är -1.

**Fördröjning när jobbet startar:** Standardvärdet, i sekunder, för fördröjningen innan jobbet börjar skanna slutpunkten. Standardvärdet är 0.

**Batchstorlek:** Antalet e-postmeddelanden som mottagarprocesserna utför per sökning för optimala prestanda. Värdet -1 anger alla e-postmeddelanden. Standardvärdet är 2.

**Asynkron:** Identifierar anropstypen som asynkron eller synkron. Övergående och synkrona processer kan bara anropas synkront. Standardvärdet är asynkront.

**Domänmönster:** Det domännamnsmönster som används för att filtrera inkommande e-post. Om du till exempel använder adobe.com kommer endast e-post från adobe.com att bearbetas; e-post från andra domäner ignoreras.

**Filmönster:** Inkommande mönster för bifogade filer som accepteras av providern. Detta inkluderar filer som har specifika tillägg (&amp;ast;.dat, &amp;ast;.xml), specifika namn (data) och sammansatta uttryck i namnet och tillägget (.[d][aA]&#39;port&#39;). Standardvärdet är &amp;ast;.&amp;ast;..

**Jobbmottagare:** En eller flera e-postadresser som används för att skicka e-post för att ange slutförda jobb. Som standard skickas alltid ett meddelande om att jobbet lyckades till avsändaren av det ursprungliga jobbet. Stöd för upp till 100 mottagare. Om du vill inaktivera den här inställningen lämnar du det här fältet tomt.

**Jobbmottagare misslyckades:** En eller flera e-postadresser som används för att skicka e-post för att ange misslyckade jobb. Som standard skickas alltid ett meddelande om misslyckat jobb till avsändaren som skickade det ursprungliga jobbet. Stöd för upp till 100 mottagare. Om du vill inaktivera den här inställningen lämnar du det här fältet tomt.

**Inkorgsvärd:** Inkorgens värdnamn eller IP-adress som e-postprovidern ska skanna.

**Inkorgsport:** Inkorgsportnumret som e-postleverantören ska skanna. Om värdet är 0 används IMAP- eller POP3-standardporten.

**Inkorgsprotokoll:** E-postprotokollet för e-postslutpunkten som ska användas för att skanna inkorgen. Alternativen är IMAP eller POP3. Inkorgens värdserver för e-post måste ha stöd för dessa protokoll.

**Inkorgens timeout:** Anger hur lång tid slutpunkten ska vänta innan den avbryts när den försöker ansluta till inkorgen. Om ingen anslutning hämtas innan timeout-värdet har nåtts avsöks inte inkorgen.

**Inkorgsanvändare:** Användarnamnet som krävs för att logga in på e-postkontot. Beroende på e-postservern och konfigurationen kan det här namnet endast vara användarnamnsdelen i e-postmeddelandet eller den fullständiga e-postadressen.

**Inkorgslösenord:** Lösenordet för Inkorgen-användaren.

**POP3/IMAP SSL aktiverat:** När det här alternativet är markerat aktiveras SSL.

**SMTP-värd:** Värdnamnet för den e-postserver som e-postleverantören använder för att skicka resultat och felmeddelanden. Till exempel mail.corp.example.com.

**SMTP-port:** Den port som används för att ansluta till e-postservern. Standardvärdet är 25.

**SMTP-användare:** Användarkontot som e-postleverantören ska använda när den skickar e-post för resultat och fel.

**SMTP-lösenord:** Lösenordet för SMTP-kontot. Vissa e-postservrar kräver inget SMTP-lösenord.

**Skicka från:** E-postadressen (till exempel user@company.com) som används för att skicka e-postmeddelanden om resultat och fel. Om du inte anger något Skicka från-värde försöker e-postservern att fastställa e-postadressen genom att kombinera värdet som anges i inställningen SMTP-användare med en standarddomän som konfigurerats på e-postservern. Om e-postservern inte har någon standarddomän och du inte anger något värde för Skicka från, kan fel uppstå. Om du vill vara säker på att e-postmeddelandena har rätt från-adress anger du ett värde för inställningen Skicka från.

**SMTP SSL aktiverat:** När det här alternativet är markerat aktiveras SSL över SMTP.

**Inkludera den ursprungliga e-postmeddelandetexten som en bifogad fil:** När du skickar ett e-postmeddelande till formulärservern inkluderas som standard meddelandets ursprungliga text i meddelandetexten. Välj det här alternativet om du i stället vill ta med texten som en bifogad fil.

**Använd den ursprungliga ämnesraden för resultatmeddelanden:** Som standard använder Forms-servern de värden som anges i inställningarna Ämne för lyckad e-post och Ämne för fele-post som ämnesrad när resultatmeddelanden skickas. Välj det här alternativet om du i stället vill använda samma ämnesrad som det ursprungliga e-postmeddelandet som skickades till servern.

**Ämne för e-post:** När du har skickat ett e-postmeddelande till en e-postslutpunkt för att starta eller fortsätta en process får du ett returmeddelande från AEM-formulärservern. Om e-postmeddelandet lyckas får du ett e-postmeddelande om att det lyckades. Om e-postmeddelandet misslyckas får du ett felmeddelande som informerar om varför det misslyckades. Med den här inställningen kan du ange ämnesraden för e-postmeddelanden om lyckade åtgärder som skickas för den här slutpunkten.

**E-postbrödtext:** Gör att du kan ange brödtexten i e-postmeddelanden om lyckade åtgärder som skickats för den här slutpunkten.

**Ämnesprefix för e-postfel:** Gör att du kan ange texten som ska användas i början av ämnesraden med e-postmeddelanden om fel som skickas för den här slutpunkten.

**E-postämne för fel:** Gör att du kan ange ämnesraden för felmeddelanden som skickas för den här slutpunkten. Den här texten visas efter Error Email Subject Prefix.

**E-postbrödtext för fel:** Gör att du kan ange den första raden i brödtexten för felmeddelanden som skickas för den här slutpunkten.

**E-postsammanfattning:** Varje meddelande om att åtgärden lyckades eller misslyckades innehåller ett avsnitt med den ursprungliga e-posttexten som du skickade till formulärservern. Den här inställningen anger texten som visas ovanför avsnittet.

**Validera inkorgen innan den här slutpunkten skapas/uppdateras:** När det här alternativet är markerat kontrollerar formulärservern om SMTP/POP3-inställningarna är korrekta innan slutpunkten skapas. När du klickar på Lägg till visas ett meddelande som anger om inkorgskontot är giltigt. Om det här alternativet inte är markerat skapas slutpunkten av AEM-formulärservern utan att inkorgen valideras.

**Teckenuppsättningskodning:** Det kodningsformat som ska användas för e-postmeddelandet. Standardvärdet är UTF-8, som de flesta användare utanför Japan kommer att använda. Användare i en japansk miljö kan välja ISO2022-JP.

**Mapp för e-post som skickades misslyckades:** Anger en katalog där resultat ska lagras om SMTP-e-postservern inte fungerar.

## Inställningar för e-postslutpunkt {#email-endpoint-settings}

Använd följande inställningar för att konfigurera en e-postslutpunkt.

**Namn:** En obligatorisk inställning som identifierar slutpunkten. Ta inte med ett &lt;-tecken eftersom det kortar av namnet som visas i Arbetsyta. Om du anger en URL som namn på slutpunkten kontrollerar du att den överensstämmer med de syntaxregler som anges i RFC1738.

**Beskrivning:** En beskrivning av slutpunkten. Ta inte med ett &lt;-tecken eftersom det kortar av beskrivningen som visas i Arbetsyta.

**Cron-uttryck:** Ange ett cron-uttryck om e-postmeddelandet måste schemaläggas med ett cron-uttryck.

**Antal upprepningar:** Antal gånger som e-postslutpunkten skannar mappen eller katalogen. Värdet -1 anger obestämd skanning. Standardvärdet är -1.

**Upprepa intervall:** Den skanningsfrekvens som mottagaren använder för att kontrollera inkommande e-post.

**Fördröjning när jobbet startar:** Den tid det tar att vänta på genomsökningen efter att schemaläggaren har startats.

**Batchstorlek:** Antalet e-postmeddelanden som mottagarprocesserna utför per sökning för optimala prestanda. Värdet -1 anger alla e-postmeddelanden. Standardvärdet är 2.

**Användarnamn:** En obligatorisk inställning, som är det användarnamn som används när en måltjänst anropas från e-post. Standardvärdet är SuperAdmin.

**Domännamn:** En obligatorisk inställning, som är användarens domän. Standardvärdet är DefaultDom.

**Domänmönster:** Anger domänmönster för inkommande e-post som accepteras av providern. Om du till exempel använder adobe.com behandlas endast e-post från adobe.com; e-post från andra domäner ignoreras.

**Filmönster:** Anger mönster för inkommande bifogade filer som accepteras av providern. Detta inkluderar filer som har specifika tillägg (&amp;ast;.dat, &amp;ast;.xml), specifika namn (data) eller sammansatta uttryck i namnet och tillägget (&amp;ast;.[d][aA]&#39;port&#39;).

**Jobbmottagare:** En e-postadress dit meddelanden skickas för att ange slutförda jobb. Som standard skickas alltid ett meddelande om att jobbet lyckades till avsändaren. Om du skriver avsändare skickas e-postresultaten till avsändaren. Stöd för upp till 100 mottagare. Ange ytterligare mottagare med e-postadresser, avgränsade med kommatecken (,).

Om du vill inaktivera den här inställningen lämnar du inställningen tom. I vissa fall vill du utlösa en process och inte få ett e-postmeddelande om resultatet.

**Jobbmottagare misslyckades:** En e-postadress dit meddelanden skickas för att ange misslyckade jobb. Som standard skickas alltid ett felmeddelande till avsändaren. Om du skriver avsändare skickas e-postresultaten till avsändaren. Stöd för upp till 100 mottagare. Ange ytterligare mottagare med e-postadresser, avgränsade med kommatecken (,).

Om du vill inaktivera den här inställningen lämnar du inställningen tom. I vissa fall vill du utlösa en process och inte få ett e-postmeddelande om resultatet.

**Inkorgsvärd:** Inkorgens värdnamn eller IP-adress som e-postprovidern ska skanna.

**Inkorgsport:** Den port som e-postservern använder. Standardvärdet för POP3 är 110 och standardvärdet för IMAP är 143. Om SSL är aktiverat är standardvärdet för POP3 995 och standardvärdet för IMAP är 993.

**Inkorgsprotokoll:** E-postprotokollet för e-postslutpunkten som ska användas för att skanna inkorgen. Värdena är IMAP eller POP3. Inkorgens värdserver för e-post måste ha stöd för dessa protokoll.

**Inkorgens timeout:** Tidsgränsen i sekunder för e-postprovidern att vänta på inkorgssvar.

**Inkorgsanvändare:** Användarnamnet som krävs för att logga in på e-postkontot. Beroende på e-postservern och konfigurationen kan det här värdet vara endast användarnamnsdelen i e-postmeddelandet eller den fullständiga e-postadressen.

**Inkorgslösenord:** Lösenordet för inkorgsanvändaren.

**POP3/IMAP SSL aktiverat:** Välj den här inställningen för att tvinga e-postleverantören att använda SSL för att skanna inkorgen. Kontrollera att e-postservern har stöd för SSL.

**SMTP-värd:** Värdnamnet på den e-postserver som e-postleverantören använder för att skicka resultat och felmeddelanden.

**SMTP-port:** Standardvärdet för SMTP-porten är 25.

**SMTP-användare:** Användarkontot som e-postleverantören ska använda när den skickar e-postmeddelanden om resultat och fel.

**SMTP-lösenord:** Lösenordet för SMTP-kontot. Vissa e-postservrar kräver inget SMTP-lösenord.

**Skicka från:** E-postadressen (till exempel user@company.com) som används för att skicka e-postmeddelanden om resultat och fel. Om du inte anger något Skicka från-värde försöker e-postservern att fastställa e-postadressen genom att kombinera värdet som anges i inställningen SMTP-användare med en standarddomän som konfigurerats på e-postservern. Om e-postservern inte har någon standarddomän och du inte anger något värde för Skicka från, kan fel uppstå. Om du vill vara säker på att e-postmeddelandena har rätt från-adress anger du ett värde för inställningen Skicka från.

**SMTP SSL aktiverat:** Välj den här inställningen för att tvinga e-postleverantören att använda SSL för att skanna inkorgen. Kontrollera att e-postservern har stöd för SSL.

**Mapp för e-post som skickades misslyckades:** Anger en katalog där resultat ska lagras om SMTP-e-postservern inte fungerar.

**asynkron:** När det är synkront bearbetas alla indatadokument och ett enda svar returneras. När inställningen är asynkron skickas ett svar för varje dokument som bearbetas.

En e-postslutpunkt skapas till exempel för en tjänst som tar ett enstaka Word-dokument och returnerar det dokumentet som en PDF-fil. Ett e-postmeddelande kan skickas till slutpunktens inkorg som innehåller flera (3) Word-dokument. När alla tre dokument har bearbetats och slutpunkten har konfigurerats som synkron, skickas ett e-postmeddelande med alla tre bifogade dokument. Om slutpunkten är asynkron skickas ett e-postmeddelande när varje Word-dokument har konverterats till PDF. Resultatet är tre e-postmeddelanden, vart och ett med en enda bifogad PDF-fil.

Standardvärdet är asynkront.

**Inkludera den ursprungliga e-posttexten som en bifogad fil:** När du skickar ett e-postmeddelande till formulärservern inkluderas som standard meddelandets ursprungliga text i meddelandetexten. Välj det här alternativet om du i stället vill ta med texten som en bifogad fil.

**Använd den ursprungliga ämnesraden för resultatmeddelanden:** Som standard använder Forms-servern de värden som anges i inställningarna Ämne för lyckad e-post och Ämne för fele-post som ämnesrad när resultatmeddelanden skickas. Välj det här alternativet om du i stället vill använda samma ämnesrad som det ursprungliga e-postmeddelandet som skickades till servern.

**Ämne för e-post:** När du har skickat ett e-postmeddelande till en e-postslutpunkt för att starta eller fortsätta en process får du ett returmeddelande från AEM-formulärservern. Om e-postmeddelandet lyckas får du ett e-postmeddelande om att det lyckades. Om e-postmeddelandet misslyckas får du ett felmeddelande som informerar om varför det misslyckades. Med den här inställningen kan du ange ämnesraden för e-postmeddelanden om lyckade åtgärder som skickas för den här slutpunkten.

**E-postbrödtext:** Gör att du kan ange brödtexten i e-postmeddelanden om lyckade åtgärder som skickats för den här slutpunkten.

**Ämnesprefix för e-postfel:** Gör att du kan ange texten som ska användas i början av ämnesraden med e-postmeddelanden om fel som skickas för den här slutpunkten.

**E-postämne för fel:** Gör att du kan ange ämnesraden för felmeddelanden som skickas för den här slutpunkten. Den här texten visas efter Error Email Subject Prefix.

**E-postbrödtext för fel:** Gör att du kan ange den första raden i brödtexten för felmeddelanden som skickas för den här slutpunkten.

**E-postsammanfattning:** Varje meddelande om att åtgärden lyckades eller misslyckades innehåller ett avsnitt med den ursprungliga e-posttexten som du skickade till formulärservern. Den här inställningen anger texten som visas ovanför avsnittet.

**Validera inkorgen innan du skapar/uppdaterar den här slutpunkten:** När det här alternativet är markerat kontrollerar formulärservern om SMTP/POP3-inställningarna är korrekta innan slutpunkten skapas. När du klickar på Lägg till visas ett meddelande som anger om inkorgskontot är giltigt. Om det här alternativet inte är markerat skapas slutpunkten av AEM-formulärservern utan att inkorgen valideras.

**Åtgärdsnamn:** Den här inställningen är obligatorisk. En lista över åtgärder som kan tilldelas e-postslutpunkten. Den åtgärd som du väljer här avgör vilka fält som visas i avsnitten Mappningar av indataparameter och Utdataparameter.

**Mappningar av indataparameter:** Används för att konfigurera de indata som krävs för att bearbeta tjänsten och åtgärden. De två typerna av indata är literala och variabla:

**Literal:** I e-postmeddelandet används det värde som anges i fältet när det visas.

**Variabel:** Du kan mappa en sträng från e-postens ämne, brödtext, rubrik eller avsändarens e-postadress. Om du vill göra det använder du något av följande nyckelord: %SUBJECT%, %BODY%, %HEADER% eller %SENDER%. Om du till exempel använder %SUBJECT% används innehållet i e-postämnet som indataparameter. Om du vill hämta bifogade filer anger du ett filmönster som e-postslutpunkten kan använda för att välja bifogade dokument. Om du till exempel anger &amp;ast;.pdf väljs alla bifogade dokument som har filnamnstillägget .pdf. Ingående &amp;stämpel;ast; markerar alla bifogade dokument. Om du anger example.pdf väljs alla bifogade dokument som heter example.pdf.

**Mappningar av utdataparameter:** Används för att konfigurera tjänstens och åtgärdens utdata. Följande tecken i mappningsvärdena för utdataparametrar utökas i filnamnet för den bifogade filen:

**%F** Representerar källfilens filnamn (inte ett tillägg).

**%E** Representerar källfilens filtillägg.

Alla förekomster av det omvända snedstrecket (\) ersätts med %%.

***Obs **! Om tjänstbegärandemeddelandet innehåller flera bifogade filer kan du inte använda parametrarna %F och %E för egenskapen Mappningar av utdataparameter för slutpunkten. Om tjänstsvaret returnerar flera bifogade filer kan du inte ange samma filnamn för fler än en bifogad fil. Om du inte följer dessa rekommendationer skapar den anropade tjänsten namnen för de returnerade filerna, och namnen är inte förutsägbara.*

Följande värden är tillgängliga:

**Ett objekt:** E-postleverantören har inte källmappens mål; resultaten returneras som bilagor. Mönstret är Result/%F.ps och returnerar Result%%sourcefilename.ps som bifogad fil.

**Lista:** Mönstret är Result/%F/ och returnerar Result%%sourcefilename%%file1 som bifogad fil.

**Karta:** Mönstret är Result/%F/ och källmålet är Result%%sourcefilename%%file1 och Result%%sourcefilename%%file2. Om kartan innehåller mer än ett objekt och mönstret är Result/%F.ps, är de bifogade svarsfilerna Result%%sourcefilename1.ps (output 1) och Result%%sourcefilename2.ps (output 2).

## Skapa en e-postslutpunkt för tjänsten Slutför uppgift {#create-an-email-endpoint-for-the-complete-task-service}

För att formulärarbetsflöden ska kunna ta emot och hantera inkommande e-postmeddelanden från användare måste du skapa en e-postslutpunkt för tjänsten Complete Task.

1. I administrationskonsolen klickar du på Tjänster > Program och tjänster > Tjänsthantering.
1. På sidan Tjänsthantering klickar du på tjänsten Complete Task.
1. Välj E-post i listrutan på fliken Slutpunkter och klicka på Lägg till.
1. Ange värdnamnet eller IP-adressen för e-postservern i rutan Inkorgsvärd.
1. I rutan Inkorgsanvändare skriver du det användarnamn som krävs för att logga in på det e-postkonto som du skapade för att hantera formuläröverföringar. Beroende på e-postservern och konfigurationen kan det här namnet endast vara användarnamnsdelen i e-postmeddelandet eller den fullständiga e-postadressen.
1. Skriv lösenordet för Inkorgen-användaren i rutan Inkorgslösenord.
1. I rutan SMTP-värd anger du värdnamnet eller IP-adressen för den e-postserver som e-postleverantören skickar resultat- och felmeddelanden från.
1. I rutan SMTP-användare anger du användarkontot för e-postprovidern som ska användas när den skickar e-post för resultat och fel. Det här användarkontot kan vara samma värde som du använde för Inkorgen.
1. Ange lösenordet för SMTP-kontot i rutan SMTP-lösenord.
1. Välj Anropa i listan Åtgärdsnamn.
1. Välj Variabel i listan attachmentMap och skriv `*.*` i den intilliggande rutan. Detta skickar alla bilagor från inkommande e-postmeddelanden till en mappningsvariabel för processen Slutför uppgift.
1. I listan mailBody väljer du variabel och skriver `%BODY%` i rutan intill.
1. Välj Variabel i listan mailFrom och skriv `%SENDER%` i rutan intill. Detta mappar avsändaradressen till processdata för en fullständig uppgift.
1. Skriv i resultatrutan `results`. Detta gör att en resultatsträng returneras av den fullständiga uppgiften eller Starta process.
1. Klicka på Lägg till

