---
title: Installera och konfigurera dokumenttjänster
seo-title: Installera och konfigurera dokumenttjänster
description: Installera AEM Forms dokumenttjänster för att skapa, sammanställa, distribuera, arkivera PDF-dokument, lägga in digitala signaturer för att begränsa åtkomsten till dokument samt avkoda streckkodsformulär.
seo-description: Installera AEM Forms dokumenttjänster för att skapa, sammanställa, distribuera, arkivera PDF-dokument, lägga in digitala signaturer för att begränsa åtkomsten till dokument samt avkoda streckkodsformulär.
uuid: 908806a9-b0d4-42d3-9fe4-3eae44cf4326
topic-tags: installing
discoiquuid: b53eae8c-16ba-47e7-9421-7c33e141d268
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f

---


# Installera och konfigurera dokumenttjänster {#installing-and-configuring-document-services}

## Introduktion {#introduction}

AEM Forms innehåller en uppsättning OSGi-tjänster för att utföra olika åtgärder på dokumentnivå, till exempel tjänster för att skapa, sammanställa, distribuera och arkivera PDF-dokument, lägga till digitala signaturer för att begränsa dokumentåtkomsten samt avkoda streckkodsformulär. Dessa tjänster ingår i tilläggspaketet för AEM Forms. Tillsammans kallas dessa tjänster dokumenttjänster. Listan över tillgängliga dokumenttjänster och deras viktigaste funktioner är följande:

Gör att du kan kombinera, ordna om och förstärka PDF- och XDP-dokument och få information om PDF-dokument. Det hjälper även till att konvertera och validera PDF-dokument till PDF/A-standard, omvandlar PDF-formulär, XML-formulär och PDF-formulär till PDF/A-1b, PDF/A-2b och PDFA/A-3b. Mer information finns i [Assembler Service](/help/forms/using/assembler-service.md).

Gör att du kan konvertera PDF-dokument till PostScript- eller bildfiler (JPEG, JPEG 2000, PNG och TIFF). Mer information finns i [Konvertera PDF-tjänst](/help/forms/using/using-convertpdf-service.md).

Ger möjlighet att extrahera data från elektroniska bilder av streckkoder. Tjänsten accepterar TIFF- och PDF-filer som innehåller en eller flera streckkoder som indata och extraherar streckkodsdata. Mer information finns i [Barcoded Forms Service](/help/forms/using/using-barcoded-forms-service.md).

Gör att du kan kryptera och dekryptera dokument, utöka funktionaliteten i Adobe Reader med ytterligare användarrättigheter och lägga till digitala signaturer i dokumenten. Tjänsten Doc Assurance innehåller tre tjänster: signatur-, krypterings- och läsartillägg. Mer information finns i [DocAssurance-tjänsten](/help/forms/using/overview-aem-document-services.md).

Gör att du kan kryptera och dekryptera dokument. När ett dokument är krypterat blir innehållet oläsligt. En behörig användare kan dekryptera dokumentet för att få åtkomst till dess innehåll. Mer information finns i [Krypteringstjänst](/help/forms/using/overview-aem-document-services.md#p-encryption-service-p).

Gör att du kan skapa interaktiva klientprogram för datainhämtning som validerar, bearbetar, omformar och levererar formulär som vanligtvis skapas i Forms Designer. Forms-tjänsten återger alla formulärdesigner som du utvecklar till PDF-dokument. Mer information finns i [Formulärtjänst](/help/forms/using/forms-service.md).

Gör att du kan skapa dokument i olika format, bland annat PDF, laserskrivarformat och etikettskrivarformat. Laserskrivarformat är PostScript och Printer Control Language (PCL). Mer information finns i [Utdatatjänst](/help/forms/using/output-service.md).

Tjänsten PDF Generator innehåller API:er för konvertering av interna filformat till PDF. Den konverterar även PDF-filer till andra filformat och optimerar storleken på PDF-dokument. Mer information finns i [PDF Generator Service](/help/forms/using/aem-document-services-programmatically.md#main-pars-header-27).

Möjliggör för er organisation att enkelt utbyta interaktiva PDF-dokument genom att utöka funktionaliteten i Adobe Reader med ytterligare användarrättigheter. Tjänsten aktiverar funktioner som inte är tillgängliga när ett PDF-dokument öppnas med Adobe Reader, t.ex. för att lägga till kommentarer i ett dokument, fylla i formulär och spara dokumentet. Mer information finns i [Reader Extension Service](/help/forms/using/overview-aem-document-services.md#p-reader-extension-service-p).

Gör att du kan arbeta med digitala signaturer och dokument på AEM-servern. Signaturtjänsten används till exempel vanligtvis i följande situationer:

* AEM-servern certifierar ett formulär innan det skickas till en användare för att öppnas med Acrobat eller Adobe Reader.
* AEM-servern validerar en signatur som har lagts till i ett formulär med Acrobat eller Adobe Reader.
* AEM-servern signerar ett formulär för en offentlig notarius publicus.

Signaturtjänsten får åtkomst till certifikat och autentiseringsuppgifter som lagras i förtroendearkivet. Mer information finns i [Signaturtjänst](/help/forms/using/aem-document-services-programmatically.md).

AEM Forms är en kraftfull plattform i företagsklass och dokumenttjänsterna är bara en av funktionerna i AEM Forms. En fullständig lista över funktioner finns i [Introduktion till AEM Forms](/help/forms/using/introduction-aem-forms.md).

## Distributionstopologi {#deployment-topology}

AEM Forms-tilläggspaketet är ett program som distribueras till AEM. Vanligtvis krävs endast en AEM-instans (författare eller publicerad) för att köra AEM Forms-dokumenttjänster. Följande topologi rekommenderas för att köra AEM Forms dokumenttjänster. Mer information om topologier finns i [Arkitektur och distributionstopologier för AEM Forms](/help/forms/using/aem-forms-architecture-deployment.md).

![](do-not-localize/document-services.png)

>[!NOTE]
>
>Även om du kan använda AEM Forms för att konfigurera och köra alla funktioner från en enda server, bör du göra kapacitetsplanering, lastbalansering och konfigurera dedikerade servrar för specifika funktioner i en produktionsmiljö. Om du till exempel använder tjänsten PDF Generator för att konvertera tusentals sidor om dagen och flera adaptiva formulär för att hämta in data, kan du skapa separata AEM Forms-servrar för tjänsten PDF Generator och funktioner för adaptiva formulär. Det ger optimala prestanda och skalar servrarna oberoende av varandra.

## Systemkrav {#system-requirements}

Innan du börjar installera och konfigurera dokumenttjänster för AEM Forms måste du se till att:

* Maskinvaru- och programvaruinfrastruktur finns på plats. En detaljerad lista över maskin- och programvara som stöds finns i [tekniska krav](/help/sites-deploying/technical-requirements.md).

* Installationssökvägen för AEM-instansen innehåller inte blanksteg.
* En AEM-instans körs. I AEM-terminologi är &quot;instance&quot; en kopia av AEM som körs på en server i författar- eller publiceringsläge. I allmänhet behöver du bara en AEM-instans (författare eller publicerad) för att köra AEM Forms-dokumenttjänster:

   * **Författare**: En AEM-instans som används för att skapa, överföra och redigera innehåll och för att administrera webbplatsen. När innehållet är klart att publiceras replikeras det till publiceringsinstansen.
   * **Publicera**: En AEM-instans som skickar det publicerade innehållet till allmänheten via internet eller ett internt nätverk.

* Minneskraven uppfylls. AEM Forms-tilläggspaket kräver:

   * 15 GB temporärt utrymme för Microsoft Windows-baserade installationer.
   * 6 GB temporärt utrymme för UNIX-baserade installationer.

* Klientprogramvara som krävs för att skapa PDF för konvertering i Microsoft Windows och Linux installeras:

   * **Microsoft Windows**: Installera [Microsoft](/help/forms/using/aem-forms-jee-supported-platforms.md#p-software-support-for-pdf-generator-p)Office eller [Apache OpenOffice](/help/forms/using/aem-forms-jee-supported-platforms.md#p-software-support-for-pdf-generator-p)
   * **Linux**: Installera [Apache OpenOffice](/help/forms/using/aem-forms-jee-supported-platforms.md#p-software-support-for-pdf-generator-p)

>[!NOTE]
>
>* I Microsoft Windows stöder PDF Generator konverteringsvägar för WebKit, Acrobat WebCapture och PhantomJS för att konvertera HTML-filer till PDF-dokument.
>* På UNIX-baserade operativsystem stöder PDF Generator konverteringsvägar för WebKit och PhantomJS för att konvertera HTML-filer till PDF-dokument.
>



Om du använder det UNIX-baserade operativsystemet installerar du följande paket från installationsmediet för respektive operativsystem:

<table> 
 <tbody> 
  <tr> 
   <td> 
    <ul> 
     <li>exponat</li> 
    </ul> </td> 
   <td> 
    <ul> 
     <li>libxcb</li> 
    </ul> </td> 
   <td> 
    <ul> 
     <li>freetype</li> 
    </ul> </td> 
   <td> 
    <ul> 
     <li>libXau</li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td> 
    <ul> 
     <li>libSM</li> 
    </ul> </td> 
   <td> 
    <ul> 
     <li>zlib</li> 
    </ul> </td> 
   <td> 
    <ul> 
     <li>libICE</li> 
    </ul> </td> 
   <td> 
    <ul> 
     <li>libuuid</li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td> 
    <ul> 
     <li>glibc</li> 
    </ul> </td> 
   <td> 
    <ul> 
     <li>libXext</li> 
    </ul> </td> 
   <td> 
    <ul> 
     <li>nss-softokn-free-bl</li> 
    </ul> </td> 
   <td> 
    <ul> 
     <li>fontconfig</li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td> 
    <ul> 
     <li>libX11</li> 
    </ul> </td> 
   <td> 
    <ul> 
     <li>libXrender</li> 
    </ul> </td> 
   <td> 
    <ul> 
     <li>libXrandr</li> 
    </ul> </td> 
   <td> 
    <ul> 
     <li>libXinerama</li> 
    </ul> </td> 
  </tr> 
 </tbody> 
</table>

* **(Endast** PDF-generator) Installera 32-bitarsversionen av bibliotek för bibliotek, bibliotek och bibliotek och skapa nedanstående symboler. Symbolerna pekar på den senaste versionen av respektive bibliotek:

   * /usr/lib/libcurl.so
   * /usr/lib/libcrypto.so
   * /usr/lib/libssl.so

* **(Endast PDF Generator)** PDF Generator-tjänsten stöder WebKit- och PhantomJS-vägar för konvertering av HTML-filer till PDF-dokument. Installera nedanstående 64-bitarsbibliotek om du vill aktivera konvertering för PhantomJS-vägar. I allmänhet är dessa bibliotek redan installerade. Om något bibliotek saknas installerar du det manuellt:

   * linux-gate.so.1
   * libz.so.1
   * libfontconfig.so.1
   * libfreetype.so.6
   * libdl.so.2
   * librt.so.1
   * libpthread.so.0
   * libstdc++.so.6
   * libm.so.6
   * libgcc_s.so.1
   * libc.so.6
   * ld-linux.so.2
   * libexpat.so.1

### Installera Adobe Acrobat och tredjepartsprogram {#install-adobe-acrobat-and-third-party-applications}

Om du ska använda tjänsten PDF Generator för att konvertera filformat som Microsoft Word, Microsoft Excel, Microsoft PowerPoint, OpenOffice, WordPerfect X7 och Adobe Acrobat till PDF-dokument måste du se till att dessa program är installerade på AEM Forms-servern.

>[!NOTE]
>
>* Adobe Acrobat, Microsoft Word, Excel och PowerPoint finns endast för Microsoft Windows. Om du använder det UNIX-baserade operativsystemet måste du installera OpenOffice för att konvertera RTF-filer och kompatibla Microsoft Office-filer till PDF-dokument.
>* Stäng alla dialogrutor som visas när du har installerat Adobe Acrobat och tredjepartsprogram för alla användare som har konfigurerats att använda PDF Generator-tjänsten.
>* Starta alla installerade program minst en gång. Stäng alla dialogrutor för alla användare som har konfigurerats att använda PDF Generator-tjänsten.
>



När du har installerat Acrobat öppnar du Microsoft Word. På **Acrobat-** fliken klickar du på&#x200B;**Skapa PDF** och konverterar en .doc- eller .docx-fil som finns på datorn till ett PDF-dokument. Om konverteringen lyckas är AEM Forms redo att använda Acrobat med PDF Generator-tjänsten.

### Konfigurera miljövariabler {#setup-environment-variables}

Ange miljövariabler för 32- och 64-bitars Java Development Kit, tredjepartsprogram och Adobe Acrobat. Miljövariablerna ska innehålla den absoluta sökvägen för den körbara fil som används för att starta motsvarande program, till exempel visas miljövariabler för ett fåtal program i tabellen nedan:

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>Program</strong></p> </td> 
   <td><p><strong>Miljövariabel</strong></p> </td> 
   <td><p><strong>Exempel</strong></p> </td> 
  </tr> 
  <tr> 
   <td><p><strong>JDK (64-bitars)</strong></p> </td> 
   <td><p>JAVA_HOME</p> </td> 
   <td><p>C:\Program Files\Java\jdk1.8.0_74</p> </td> 
  </tr> 
  <tr> 
   <td><p><strong>JDK (32-bitars)</strong></p> </td> 
   <td><p>JAVA_HOME_32</p> </td> 
   <td><p>C:\Program Files (x86)\Java\jdk1.8.0_74</p> </td> 
  </tr> 
  <tr> 
   <td><p><strong>Adobe Acrobat</strong></p> </td> 
   <td><p>Acrobat_PATH</p> </td> 
   <td><p>C:\Program Files (x86)\Adobe\Acrobat 2015\Acrobat\Acrobat.exe</p> </td> 
  </tr> 
  <tr> 
   <td><p><strong>Anteckningar</strong></p> </td> 
   <td><p>Notepad_PATH</p> </td> 
   <td><p>C:\WINDOWS\notepad.exe<br /> <strong></strong></p> </td> 
  </tr> 
  <tr> 
   <td><p><strong>OpenOffice</strong></p> </td> 
   <td><p>OpenOffice_PATH</p> </td> 
   <td><p>C:\Program Files (x86)\OpenOffice.org4</p> </td> 
  </tr> 
 </tbody> 
</table>

>[!NOTE]
>
>* Alla miljövariabler och respektive sökvägar är skiftlägeskänsliga.
>* JAVA_HOME, JAVA_HOME_32 och Acrobat_PATH (endast Windows) är obligatoriska miljövariabler.
>* Miljövariabeln OpenOffice_PATH ställs in på installationsmappen i stället för på sökvägen till den körbara filen.
>* Ställ inte in miljövariabler för Microsoft Office-program som Word, PowerPoint, Excel och Project, eller för AutoCAD. Om dessa program är installerade på servern startar tjänsten Generera PDF automatiskt dessa program.
>* Installera OpenOffice som /root på UNIX-baserade plattformar. Om OpenOffice inte är installerat som rot kan inte PDF Generator-tjänsten konvertera OpenOffice-dokument till PDF-dokument. Om du måste installera och köra OpenOffice som en icke-rotanvändare anger du sudo-rättigheter till användaren som inte är rotanvändare.
>* Om du använder OpenOffice på en UNIX-baserad plattform kör du följande kommando för att ange variabeln path:\
   >  `export OpenOffice_PATH=/opt/openoffice.org4`
>



### (Endast för IBM WebSphere) Konfigurera IBM SSL-socketprovider {#only-for-ibm-websphere-configure-ibm-ssl-socket-provider}

* Utför följande steg för att konfigurera IBM SSL-socketprovidern:

1. Skapa en kopia av filen java.security. Filens standardplats är `[WebSphere_installation_directory]\Appserver\java_[version]\jre\lib\security`.
1. Öppna den kopierade java.security-filen för redigering.
1. Ändra standardfabrikerna för SSL-socket så att de använder JSSE2-fabrikerna i stället för standardfabrikerna för IBM WebSphere:

   **Standardinnehåll:**

   ```shell
   #ssl.SocketFactory.provider=com.ibm.jsse2.SSLSocketFactoryImpl
   #ssl.ServerSocketFactory.provider=com.ibm.jsse2.SSLServerSocketFactoryImpl
   #WebSphere socket factories (in cryptosf.jar)
   ssl.SocketFactory.provider=com.ibm.websphere.ssl.protocol.SSLSocketFactory
   ssl.ServerSocketFactory.provider=com.ibm.websphere.ssl.protocol.SSLServerSocketFactory
   ```

   **Ändrat innehåll:**

   ```shell
   ssl.SocketFactory.provider=com.ibm.jsse2.SSLSocketFactoryImpl
   ssl.ServerSocketFactory.provider=com.ibm.jsse2.SSLServerSocketFactoryImpl
   
   #WebSphere socket factories (in cryptosf.jar)
   #ssl.SocketFactory.provider=com.ibm.websphere.ssl.protocol.SSLSocketFactory
   #ssl.ServerSocketFactory.provider=com.ibm.websphere.ssl.protocol.SSLServerSocketFactory
   ```

1. Om du vill att AEM Forms-servern ska kunna använda den uppdaterade java.security-filen när AEM Forms-servern startas lägger du till följande java-argument:

   `-Djava.security.properties= [path of newly created Java.security file].`

### Konfigurera tjänsten Installera bläck och handskrift {#configure-install-ink-and-handwriting-service}

Om du kör Microsoft Windows Server konfigurerar du bläck- och handskriftstjänsten. Tjänsten krävs för att öppna Microsoft PowerPoint-filer som använder bläckfunktioner i Microsoft Office:

1. Öppna Serverhanteraren. Klicka på ikonen **[!UICONTROL Serverhanteraren]** i snabbstartsfältet.
1. Klicka på **[!UICONTROL Lägg till funktioner]** på menyn **[!UICONTROL Funktioner]** . Markera kryssrutan **[!UICONTROL Tryckfärg och handskriftstjänster]** .
1. **[!UICONTROL Välj Funktioner]** , dialogruta där **[!UICONTROL bläck- och handskriftstjänster]** är valt. Klicka på **[!UICONTROL Installera]** så installeras tjänsten.

### Konfigurera inställningar för filblock för Microsoft Office {#configure-the-file-block-settings-for-microsoft-office}

Ändra inställningarna för Microsoft Office Trust Center så att tjänsten PDF Generator kan konvertera filer som skapats med äldre versioner av Microsoft Office.

1. Öppna ett Microsoft Office-program. Exempel: Microsoft Word. Navigera till **[!UICONTROL Arkiv]**> **[!UICONTROL Alternativ]**. Dialogrutan Alternativ visas.

1. Klicka på **[!UICONTROL Trust Center]** och klicka på **[!UICONTROL Trust Center Settings]**.
1. Klicka på Inställningar för **[!UICONTROL filblock i inställningarna]** för **[!UICONTROL Säkerhetscenter]**.
1. I listan **[!UICONTROL Filtyp]** avmarkerar du **[!UICONTROL Öppna]** som filtyp som PDF Generator-tjänsten ska kunna konvertera till PDF-dokument.

### Bevilja privilegium för Ersätt en processnivåtoken {#grant-the-replace-a-process-level-token-privilege}

Användarkontot som används för att starta programservern kräver privilegiet **Ersätt en token** på processnivå. Det lokala systemkontot har som standard privilegiet **Ersätt en token** på processnivå. För servrar som körs med en användare i gruppen Lokala administratörer måste privilegiet ges uttryckligen. Utför följande steg för att bevilja privilegiet:

1. Öppna grupprincipredigeraren för Microsoft Windows. Om du vill öppna grupprincipredigeraren klickar du på **[!UICONTROL Start]**, skriver **gpedit.msc** i rutan Starta sökning och klickar på **[!UICONTROL Grupprincipredigeraren]**.
1. Navigera till **[!UICONTROL Lokal datorprincip]** > **[!UICONTROL Datorkonfiguration]** > **[!UICONTROL Windows-inställningar]** > **[!UICONTROL Säkerhetsinställningar]** > **[!UICONTROL Lokala principer]** **** **** > Tilldelning av användarrättigheter¥ och redigeraErsätt en token på processnivå och inkludera gruppen Administratörer.
1. Lägg till användaren i posten Ersätt en processnivåtoken.

#### Aktivera tjänsten PDF Generator för icke-administratörer {#enable-the-pdf-generator-service-for-non-administrators}

Du kan göra det möjligt för en icke-administratörsanvändare att använda PDF Generator-tjänsten. Normalt kan endast användare med administratörsbehörighet använda tjänsten:

1. Skapa en miljövariabel, PDFG_NON_ADMIN_ENABLED.
1. Ange värdet för miljövariabeln till TRUE.
1. Starta om instansen AEM Forms.

### Inaktivera Kontroll av användarkonto (UAC) {#disable-user-account-control-uac}

1. Gå till **[!UICONTROL Start > Kör]** och ange **[!UICONTROL MSCONFIG]** för att få åtkomst till verktyget Systemkonfiguration.
1. Klicka på fliken **[!UICONTROL Verktyg]** och rulla nedåt och välj **[!UICONTROL Ändra UAC-inställningar]**. Klicka på **[!UICONTROL Starta]** för att köra kommandot i ett nytt fönster.
1. Justera skjutreglaget till nivån för Aldrig meddelande. När du är klar stänger du kommandofönstret och stänger fönstret Systemkonfiguration.
1. Kontrollera att registerinställningen för UAC är inställd på 0 (noll). Verifiera genom att utföra följande steg:

   1. Microsoft rekommenderar att du säkerhetskopierar registret innan du ändrar det. Detaljerade anvisningar finns i [Säkerhetskopiera och återställa registret i Windows](https://support.microsoft.com/en-us/help/322756).
   1. Öppna Microsoft Windows Registereditor. Öppna Registereditorn genom att gå till Start > Kör, skriva regedit och klicka på OK.
   1. Navigera till `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\policies\system\`. Kontrollera att värdet för EnableLUA är 0 (noll).
   1. Kontrollera att värdet för **EnableLUA** är 0 (noll). Om värdet inte är 0 ändrar du värdet till 0. Stäng Registereditorn.

1. Starta om datorn.

### Inaktivera felrapporteringstjänsten {#disable-error-reporting-service}

När du konverterar ett dokument till PDF med PDF Generator-tjänsten på Windows Server rapporterar Windows Server ibland att den körbara filen har stött på ett problem och måste stängas. PDF-konverteringen påverkas dock inte eftersom den fortsätter i bakgrunden.

Du kan undvika att få felmeddelanden genom att inaktivera Windows-felrapportering. Mer information om hur du inaktiverar felrapportering finns på [https://technet.microsoft.com/en-us/library/cc754364.aspx](https://technet.microsoft.com/en-us/library/cc754364.aspx).

### Konfigurera konvertering av HTML till PDF {#configure-html-to-pdf-conversion}

Tjänsten PDF Generator tillhandahåller vägar eller metoder för WebKit, WebCapture och PhantomJS för att konvertera HTML-filer till PDF-dokument. Om du vill aktivera konvertering för WebKit- och Acrobat WebCapture-vägar i Windows kopierar du Unicode-teckensnittet till katalogen %windir%\fonts.

>[!NOTE]
>
> När du installerar nya teckensnitt i teckensnittsmappen startar du om AEM Forms-instansen.


### Extra konfigurationer för konvertering från HTML till PDF {#extra-configurations-for-html-to-pdf-conversion}

På UNIX-baserade plattformar stöder PDF Generator-tjänsten WebKit- och PhantomJS-vägar för konvertering av HTML-filer till PDF-dokument. Om du vill aktivera konvertering från HTML till PDF utför du följande konfigurationer, som gäller för den konverteringsväg du föredrar:

#### Aktivera stöd för Unicode-teckensnitt (endast WebKit) {#enable-support-for-unicode-fonts-webkit-only}

Kopiera Unicode-teckensnittet till någon av följande kataloger som passar ditt system:

* /usr/lib/X11/fonts/TrueType
* /usr/share/fonts/default/TrueType
* /usr/X11R6/lib/X11/fonts/ttf
* /usr/X11R6/lib/X11/fonts/TrueType
* /usr/X11R6/lib/X11/fonts/TrueType
* /usr/X11R6/lib/X11/fonts/TTF
* /usr/openwin/lib/X11/fonts/TrueType (Solaris)

>[!NOTE]
>
>* I RedHat Enterprise Linux 6.x och senare är kurirteckensnitten inte tillgängliga. Hämta arkivet font-ibm-type1-1.0.3.zip för att installera teckensnittet Courier. Extrahera arkivet på /usr/share/fonts. Skapa en symbolisk länk från /usr/share/X11/fonts till /usr/share/fonts.
>* Ta bort alla .lst-teckensnittscachefiler från katalogerna Html2PdfSvc/bin och /usr/share/fonts.
>* Kontrollera att katalogerna /usr/lib/X11/fonts och /usr/share/fonts finns. Om katalogerna inte finns använder du ln-kommandot för att skapa en symbolisk länk från /usr/share/X11/fonts till /usr/lib/X11/fonts och en annan symbolisk länk från /usr/share/fonts till /usr/share/X11/fonts. Se även till att teckensnitten finns på /usr/lib/X11/fonts.
>* Kontrollera att alla teckensnitt (Unicode och icke-unicode) är tillgängliga i katalogen /usr/share/fonts eller /usr/share/X11/fonts.
>* När du kör PDF Generator-tjänsten som en icke-rotanvändare måste du ge icke-rotanvändaren läs- och skrivåtkomst till alla teckensnittskataloger.
>* När du installerar nya teckensnitt i teckensnittsmappen startar du om AEM Forms-instansen.
>



## Installera AEM Forms-tilläggspaket {#install-aem-forms-add-on-package}

AEM Forms-tilläggspaketet är ett program som distribueras till AEM. Paketet innehåller AEM Forms Document Services och andra AEM Forms-funktioner. Så här installerar du paketet:

1. Logga in på [AEM-servern](http://localhost:4502) som administratör och öppna [paketresursen](http://localhost:4502/crx/packageshare). Du måste ha ett Adobe-id för att kunna logga in på paketresursen.

1. I [AEM-paketresursen](http://localhost:4502/crx/packageshare/login.html)söker du efter tilläggspaket **[!UICONTROL för]** AEM 6.4-formulär, klickar på det paket som gäller för ditt operativsystem och klickar på **[!UICONTROL Hämta]**. Läs och godkänn licensavtalet och klicka på **[!UICONTROL OK]**. Nedladdningen startar. När du har hämtat **[!UICONTROL visas ordet Hämtad]** bredvid paketet.

   Du kan också använda versionsnumret för att söka efter ett tilläggspaket. Versionsnummer för det senaste paketet finns i artikeln om [AEM Forms-versioner](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html) .

1. När nedladdningen är klar klickar du på **[!UICONTROL Nedladdad]**. Du omdirigeras till pakethanteraren. I pakethanteraren söker du efter det hämtade paketet och klickar på **[!UICONTROL Installera]**.

   Om du hämtar paketet manuellt via den direktlänk som visas i artikeln [AEM Forms Relases](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html) loggar du in på pakethanteraren, klickar på **[!UICONTROL Överför paket]**, markerar det hämtade paketet och klickar på Överför. När paketet har överförts klickar du på paketnamnet och sedan på **[!UICONTROL Installera]**.

1. När paketet har installerats uppmanas du att starta om AEM-instansen. **Stoppa inte servern omedelbart.** Innan du stoppar AEM Forms-servern väntar du tills ServiceEvent REGISTERED- och ServiceEvent UNREGISTERED-meddelandena inte längre visas i `[AEM-Installation-Directory]/crx-quickstart/logs/error`.log-filen och loggen är stabil.

## Konfiguration efter installation {#post-installation-configurations}

### Konfigurera Boot Delegation för RSA/BouncyCastle-bibliotek {#configure-boot-delegation-for-rsa-bouncycastle-libraries}

1. Stoppa AEM-instansen. Gå till [AEM-installationskatalogen]\crx-quickstart\conf\ folder. Öppna filen sling.properties för redigering.

   Om du använder `[AEM installation directory]\crx-quickstart\bin\start.bat` för att starta en AEM-instans redigerar du sling.properties som finns på `[AEM_root]\crx-quickstart\`.

1. Lägg till följande egenskaper i filen sling.properties:

   ```
   sling.bootdelegation.class.com.rsa.jsafe.provider.JsafeJCE=com.rsa.*
   sling.bootdelegation.class.org.bouncycastle.jce.provider.BouncyCastleProvider=org.bouncycastle.*
   ```

1. (Endast AIX) Lägg till följande egenskaper i filen sling.properties:

   ```
   sling.bootdelegation.xerces=org.apache.xerces.*
   ```
1. Spara och stäng filen.

### Konfigurera teckensnittshanterartjänsten {#configuring-the-font-manager-service}

1. Logga in på [AEM Configuration Manager](http://localhost:4502/system/console/configMgr) som administratör.
1. Leta upp och öppna tjänsten **[!UICONTROL CQ-DAM-Handler-Gibson Font Managers]** . Ange sökvägen till katalogerna System Fonts, Adobe Server Fonts och Customer Fonts. Click **[!UICONTROL Save]**.

   >[!NOTE]
   >
   >Din rätt att använda teckensnitt som tillhandahålls av andra än Adobe regleras av de licensavtal som dessa parter ger dig med dessa teckensnitt och omfattas inte av din licens att använda Adobe-program. Adobe rekommenderar att du granskar och kontrollerar att du följer alla tillämpliga licensavtal från andra tillverkare än Adobe innan du använder teckensnitt från andra tillverkare än Adobe med Adobe-program, särskilt när det gäller användning av teckensnitt i servermiljöer.
   > När du installerar nya teckensnitt i teckensnittsmappen startar du om AEM Forms-instansen.

### Konfigurera ett lokalt användarkonto för att köra PDF Generator-tjänsten {#configure-a-local-user-account-to-run-the-pdf-generator-service}

Det krävs ett lokalt användarkonto för att köra PDF Generator-tjänsten. Anvisningar om hur du skapar en lokal användare finns i [Skapa ett användarkonto i Windows](https://support.microsoft.com/en-us/help/13951/windows-create-user-account) eller [skapa ett användarkonto på UNIX-baserade plattformar](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/4/html/Step_by_Step_Guide/s1-starting-create-account.html).

1. Öppna sidan Konfiguration av [AEM Forms PDF Generator](http://localhost:4502/libs/fd/pdfg/config/ui.html) .

1. Ange autentiseringsuppgifter för ett lokalt användarkonto på fliken **[!UICONTROL Användarkonton]** och klicka på **[!UICONTROL Skicka]**. Tillåt åtkomst till användaren om Microsoft Windows tillfrågas. När den konfigurerade användaren läggs till visas den under avsnittet **[!UICONTROL Dina användarkonton]** på fliken **[!UICONTROL Användarkonton]** .

### Konfigurera timeout-inställningar {#configure-the-time-out-settings}

1. I [AEM-konfigurationshanteraren](http://localhost:4502/system/console/configMgr)letar du reda på och öppnar **[!UICONTROL Jacorb ORB Provider]** -tjänsten.

   Lägg till följande i fältet **[!UICONTROL Custom Properties.name]** och klicka på **[!UICONTROL Save]**. Tidsgränsen för väntande svar (kallas även CORBA-klienttimeout) anges till 600 sekunder.

   `jacorb.connection.client.pending_reply_timeout=600000`

1. Logga in på AEM-författarinstansen och gå till **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Verktyg]** > **[!UICONTROL Formulär]** > **[!UICONTROL Konfigurera PDF-generator]**. Standardwebbadressen är http://localhost:4502/libs/fd/pdfg/config/ui.html.

   Öppna fliken **[!UICONTROL Allmän konfiguration]** och ändra värdet för följande fält för din miljö:

<table> 
 <tbody> 
  <tr> 
   <td>Fält</td> 
   <td>Beskrivning</td> 
   <td>Standardvärde</td> 
  </tr> 
  <tr> 
   <td>Timeout för serverkonvertering</td> 
   <td>En PDFG-konvertering förblir aktiv i det antal sekunder som anges i tidsgränsen för serverkonvertering</td> 
   <td>270 sekunder<br /> </td> 
  </tr> 
  <tr> 
   <td>Sekunder för PDFG-rensningsgenomsökning</td> 
   <td>Antalet sekunder som krävs för att utföra efterkonverteringsåtgärder.<br /> </td> 
   <td>3 600 sekunder</td> 
  </tr> 
  <tr> 
   <td>Utgångsdatum i sekunder för jobb</td> 
   <td>Varaktighet som PDF Generator-tjänsten kan utföra en konvertering för. Kontrollera att värdet för Sekunder för jobbförfallodatum är större än värdet för PDFG-rensningsgenomsökning.</td> 
   <td>7 200 sekunder</td> 
  </tr> 
 </tbody> 
</table>

### Konfigurera Acrobat för tjänsten PDF Generator {#configure-acrobat-for-the-pdf-generator-service}

I Microsoft Windows använder PDF Generator-tjänsten Adobe Acrobat för att konvertera filformat som stöds till PDF-dokument. Så här konfigurerar du Adobe Acrobat för PDF Generator-tjänsten:

1. Öppna Acrobat och välj **[!UICONTROL Redigera]**> **[!UICONTROL Inställningar]**> **[!UICONTROL Updater]**. I Leta efter uppdateringar avmarkerar du **[!UICONTROL Installera uppdateringar]** automatiskt och klickar på **[!UICONTROL OK]**. Stäng Acrobat.
1. Dubbelklicka på ett PDF-dokument på datorn. När Acrobat startar för första gången visas dialogrutorna för inloggning, välkomstskärm och licensavtal. Stäng de här dialogrutorna för alla användare som har konfigurerats att använda PDF Generator.
1. Kör PDF Generator-verktygsbatchfilen för att konfigurera Acrobat för PDF Generator-tjänsten:

   1. Öppna [AEM Package Manager](http://localhost:4502/crx/packmgr/index.jsp) och hämta `adobe-aemfd-pdfg-common-pkg-[version].zip` filen från pakethanteraren.
   1. Zippa upp den nedladdade ZIP-filen. Öppna kommandotolken med administratörsbehörighet.
   1. Navigate to the `[extracted-zip-file]\jcr_root\etc\fd\pdfg\tools\adobe-aemfd-pdfg-utilities-[version]-win.zip\scripts` directory. Kör följande kommandofil:

      `Acrobat_for_PDFG_Configuration.bat`

      Acrobat är konfigurerat att köras med PDF Generator-tjänsten.

1. Kör System Ready Tool (SRT) för att validera Acrobat-installationen. Verktyget kontrollerar om datorn är korrekt konfigurerad för att köra PDF Generator-konverteringar och genererar en rapport på den angivna sökvägen:

   1. Öppna kommandotolken. Navigate to the `[extracted-adobe-aemfd-pdfg-common-pkg]\jcr_root\etc\fd\ pdfg\tools\adobe-aemfd-pdfg-utilities-[version]-win.zip\srt` folder. Kör följande kommando från kommandotolken:

      `cscript SystemReadinessTool.vbs [Path_of_reports_folder] en`

      >[!NOTE]
      >
      >Om systemberedskapsverktyget rapporterar att filen pdfgen.api inte är tillgänglig i plugin-mappen för acrobat kopierar du filen pdfgen.api från `[extracted-adobe-aemfd-pdfg-common-pkg]\plugins\x86_win32` katalogen till `[Acrobat_root]\Acrobat\plug_ins` katalogen.

   1. Navigera till `[Path_of_reports_folder]`. Öppna filen SystemReadinessTool.html. Verifiera rapporten och åtgärda problemen.

### Konfigurera primär väg för konvertering från HTML till PDF (endast Windows) {#configure-primary-route-for-html-to-pdf-conversion-windows-only}

Tjänsten PDF Generator erbjuder flera vägar för att konvertera HTML-filer till PDF-dokument: Webkit, Acrobat WebCapture (endast Windows) och PhantomJS. Adobe rekommenderar att du använder PhantomJS-vägen eftersom den kan hantera dynamiskt innehåll och inte har några beroenden till 32-bitars bibliotek, 32-bitars JDK eller inte kräver några extra teckensnitt. Inte heller PhantomJS-vägen kräver sudo- eller root-åtkomst för att köra konverteringen.

Den primära standardvägen för konvertering från HTML till PDF är Webkit. Så här ändrar du konverteringsflödet:

1. På AEM-författarinstansen går du till **[!UICONTROL Verktyg]**> **[!UICONTROL Formulär]**> **[!UICONTROL Konfigurera PDF-generator]**.

1. På fliken **[!UICONTROL Allmän konfiguration]** väljer du önskad konverteringsväg i listrutan **[!UICONTROL Primär väg för HTML-till-PDF-konverteringar]** .

### Initiera Global Trust Store{#intialize-global-trust-store}

Med pålitlighetslagerhanteringen kan du importera, redigera och ta bort certifikat som du litar på på servern för validering av digitala signaturer och certifikatautentisering. Du kan importera och exportera valfritt antal certifikat. När ett certifikat har importerats kan du redigera pålitlighetsinställningarna och förtroendearkivets typ. Så här initierar du ett förtroendearkiv:

1. Logga in på AEM Forms-instansen som administratör.
1. Gå till **[!UICONTROL Verktyg]** > **[!UICONTROL Dokumentskydd]** > **[!UICONTROL Lita på butik]**.
1. Klicka på **[!UICONTROL Skapa TrustStore]**. Ange lösenord och tryck på **[!UICONTROL Spara]**.

### Konfigurera certifikat för Reader-tilläggs- och krypteringstjänsten {#set-up-certificates-for-reader-extension-and-encryption-service}

Tjänsten DocAssurance kan lägga in användarrättigheter i PDF-dokument. Konfigurera certifikaten om du vill tillämpa användningsbehörighet för PDF-dokument.

Innan du konfigurerar certifikaten bör du kontrollera att du har en:

* Certifikatfil (.pfx).

* Lösenordet för den privata nyckeln som tillhandahålls med certifikatet.

* Alias för privat nyckel. Du kan köra kommandot för Java-nyckelverktyget för att visa alias för den privata nyckeln:
   `keytool -list -v -keystore [keystore-file] -storetype pkcs12`

* Lösenord för nyckelbehållarfil. Om du använder Adobe Reader Extensions-certifikatet är lösenordet för nyckelfilen alltid detsamma som lösenordet för den privata nyckeln.

Utför följande steg för att konfigurera certifikaten:

1. Logga in på AEM Author-instansen som administratör. Gå till **[!UICONTROL Verktyg]** > **[!UICONTROL Dokumentskydd]** > **[!UICONTROL Användare]**.
1. Klicka på användarkontots **[!UICONTROL namnfält]** . Sidan **[!UICONTROL Redigera användarinställningar]** öppnas. På AEM Author-instansen finns certifikat i KeyStore. Om du inte har skapat en KeyStore tidigare klickar du på **[!UICONTROL Create KeyStore]** och anger ett nytt lösenord för KeyStore. Om servern redan innehåller en KeyStore hoppar du över det här steget.  Om du använder Adobe Reader Extensions-certifikatet är lösenordet för nyckelfilen alltid detsamma som lösenordet för den privata nyckeln.
1. På sidan **[!UICONTROL Redigera användarinställningar]** väljer du fliken **[!UICONTROL KeyStore]** . Expandera alternativet **[!UICONTROL Lägg till privat nyckel från nyckelarkivfilen]** och ange ett alias. Aliaset används för att utföra Reader Extensions-åtgärden.
1. Om du vill överföra certifikatfilen klickar du på **[!UICONTROL Välj nyckelarkivfil]** och överför en .pfx-fil.

   Lägg till lösenordet **[!UICONTROL för]** nyckelarkivet, lösenordet för **[!UICONTROL den privata nyckeln]** och det alias **[!UICONTROL för den]** privata nyckeln som är kopplat till certifikatet i respektive fält. Klicka på **[!UICONTROL Skicka]**.

   >[!NOTE]
   >
   >* I produktionsmiljön ersätter du dina utvärderingsreferenser med produktionsuppgifter. Se till att du tar bort dina gamla inloggningsuppgifter för Reader Extensions innan du uppdaterar en inloggningsuppgift som har gått ut eller utvärderar den.


1. Klicka på **[!UICONTROL Spara och stäng]** på sidan **[!UICONTROL Redigera användarinställningar]** .

### Aktivera AES-256 {#enable-aes}

Om du vill använda AES 256-kryptering för PDF-filer hämtar och installerar du Java Cryptography Extension (JCE) Unlimited Strength Jurisdential Policy-filer. Ersätt filerna local_policy.jar och US_export_policy.jar i mappen jre/lib/security. Om du till exempel använder Sun JDK kopierar du de hämtade filerna till `[JAVA_HOME]/jre/lib/security` mappen.

Assembler-tjänsten är beroende av Reader Extensions-tjänsten, signaturtjänsten, Forms-tjänsten och Output-tjänsten. Utför följande steg för att verifiera att de tjänster som krävs är igång:

1. Logga in på URL `https://'[server]:[port]'/system/console/bundles` som administratör.
1. Sök i följande tjänst och kontrollera att tjänsterna körs:

<table> 
 <tbody> 
  <tr> 
   <th>Tjänstnamn</th> 
   <th>Paketnamn</th> 
  </tr> 
  <tr> 
   <td>Signaturtjänst</td> 
   <td>adobe-aemfd-signatures</td> 
  </tr> 
  <tr> 
   <td>Tjänsten Reader Extensions</td> 
   <td>com.adobe.aemfd.adobe-aemfd-readerextensions<br /> </td> 
  </tr> 
  <tr> 
   <td>Forms Service</td> 
   <td>com.adobe.livecycle.adobe-lc-forms-grund-connector<br /> </td> 
  </tr> 
  <tr> 
   <td>Utdatatjänst</td> 
   <td>com.adobe.livecycle.adobe-lc-forms-grund-connector</td> 
  </tr> 
 </tbody> 
</table>

## Kända fel och felsökning {#known-issues-and-troubleshooting}

* Konverteringen från HTML till PDF misslyckas om en zippad indatafil innehåller HTML-filer med dubbelbytetecken i filnamn. Undvik det här problemet genom att inte använda dubbelbytetecken när du namnger HTML-filer.

* På UNIX-baserade operativsystem gör du följande för att hitta bibliotek som saknas:

1. Navigera till `[crx-repository]/bedrock/svcnative/HtmlToPdfSvc/bin/`.

1. Kör följande kommando för att lista alla bibliotek som behövs för att konvertera HTML till PDF i PhantomJS.

   `ldd phantomjs`

   Kör följande kommando för att lista saknade bibliotek.

   `ldd phantomjs | grep not`

1. Installera de saknade biblioteken manuellt.

## Nästa steg {#next-steps}

Du har en fungerande AEM Forms-dokumenttjänstmiljö. Du kan använda dokumenttjänster via:

* [Formulärbaserade arbetsflöden i OSGi](/help/forms/using/aem-forms-workflow.md)
* [Bevakade mappar](/help/forms/using/watched-folder-in-aem-forms.md)
* [API:er för dokumenttjänster](/help/forms/using/aem-document-services-programmatically.md)

