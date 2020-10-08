---
title: Installera och konfigurera dokumenttjänster
seo-title: Installera och konfigurera dokumenttjänster
description: Installera AEM Forms dokumenttjänster för att skapa, sammanställa, distribuera, arkivera PDF-dokument, lägga in digitala signaturer för att begränsa åtkomsten till dokument samt avkoda streckkodsblanketter.
seo-description: Installera AEM Forms dokumenttjänster för att skapa, sammanställa, distribuera, arkivera PDF-dokument, lägga in digitala signaturer för att begränsa åtkomsten till dokument samt avkoda streckkodsblanketter.
uuid: 908806a9-b0d4-42d3-9fe4-3eae44cf4326
topic-tags: installing
discoiquuid: b53eae8c-16ba-47e7-9421-7c33e141d268
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '4122'
ht-degree: 0%

---


# Installera och konfigurera dokumenttjänster {#installing-and-configuring-document-services}

AEM Forms tillhandahåller en uppsättning OSGi-tjänster för att utföra olika åtgärder på dokumentnivå, till exempel tjänster för att skapa, sammanställa, distribuera och arkivera PDF-dokument, lägga till digitala signaturer för att begränsa åtkomst till dokument och avkoda streckkodsformulär. Dessa tjänster ingår i AEM Forms tilläggspaket. Tillsammans kallas dessa tjänster dokumenttjänster. Listan över tillgängliga dokumenttjänster och deras viktigaste funktioner är följande:

* **Assembler:** Gör att du kan kombinera, ordna om och förstärka PDF- och XDP-dokument och få information om PDF-dokument. Det hjälper även till att konvertera och validera PDF-dokument till PDF/A-standard, omformar PDF forms, XML-formulär och PDF forms till PDF/A-1b, PDF/A-2b och PDFA/A-3b. Mer information finns i [Assembler Service](/help/forms/using/assembler-service.md).

* **ConvertPDF-tjänst:** Gör att du kan konvertera PDF-dokument till PostScript- eller bildfiler (JPEG, JPEG 2000, PNG och TIFF). Mer information finns i [Konvertera PDF-tjänst](/help/forms/using/using-convertpdf-service.md).

* **Barcoded Forms service:** Ger möjlighet att extrahera data från elektroniska bilder av streckkoder. Tjänsten accepterar TIFF- och PDF-filer som innehåller en eller flera streckkoder som indata och extraherar streckkodsdata. Mer information finns i [Barcoded Forms Service](/help/forms/using/using-barcoded-forms-service.md).

* **DocAssurance-tjänst:** Gör att du kan kryptera och dekryptera dokument, utöka funktionaliteten i Adobe Reader med ytterligare användarrättigheter och lägga till digitala signaturer i dina dokument. Tjänsten Doc Assurance innehåller tre tjänster: signatur-, krypterings- och läsartillägg. Mer information finns i [DocAssurance-tjänsten](/help/forms/using/overview-aem-document-services.md).

* **Krypteringstjänst:** Gör att du kan kryptera och dekryptera dokument. När ett dokument är krypterat blir innehållet oläsligt. En behörig användare kan dekryptera dokumentet för att få åtkomst till dess innehåll. Mer information finns i [Krypteringstjänst](/help/forms/using/overview-aem-document-services.md#encryption-service).

* **Forms:** Gör att du kan skapa interaktiva klientprogram för datainhämtning som validerar, bearbetar, omformar och levererar formulär som vanligtvis skapas i Forms Designer. Forms-tjänsten återger alla formulärdesigner som du utvecklar till PDF-dokument. Mer information finns i [Forms Service](/help/forms/using/forms-service.md).

* **Utdatatjänst:** Gör att du kan skapa dokument i olika format, bland annat PDF, laserskrivarformat och etikettskrivarformat. Laserskrivarformat är PostScript och Printer Control Language (PCL). Mer information finns i [Utdatatjänst](/help/forms/using/output-service.md).

* **Tjänsten PDF Generator:** Tjänsten PDF Generator innehåller API:er för konvertering av interna filformat till PDF. Den konverterar även PDF-filer till andra filformat och optimerar storleken på PDF-dokument. Mer information finns i [PDF Generator Service](aem-document-services-programmatically.md#pdfgeneratorservice).

* **Reader Extension Service:** Möjliggör för er organisation att enkelt dela interaktiva PDF-dokument genom att utöka funktionaliteten i Adobe Reader med ytterligare användarrättigheter. Tjänsten aktiverar funktioner som inte är tillgängliga när ett PDF-dokument öppnas med Adobe Reader, t.ex. för att lägga till kommentarer i ett dokument, fylla i formulär och spara dokumentet. Mer information finns i [Reader Extension Service](/help/forms/using/overview-aem-document-services.md#reader-extension-service).

* **Signaturtjänst:** Gör att du kan arbeta med digitala signaturer och dokument på AEM. Signaturtjänsten används till exempel vanligtvis i följande situationer:

   * AEM certifierar ett formulär innan det skickas till en användare för att öppnas med Acrobat eller Adobe Reader.
   * AEM validerar en signatur som lagts till i ett formulär med Acrobat eller Adobe Reader.
   * Den AEM servern signerar ett formulär för en offentlig notarius publicus.

   Signaturtjänsten får åtkomst till certifikat och autentiseringsuppgifter som lagras i förtroendearkivet. Mer information finns i [Signaturtjänst](/help/forms/using/aem-document-services-programmatically.md).

AEM Forms är en kraftfull plattform för större företag och dokumenttjänsterna är bara en av AEM Forms funktioner. En fullständig lista över funktioner finns i [Introduktion till AEM Forms](/help/forms/using/introduction-aem-forms.md).

## Distributionstopologi {#deployment-topology}

AEM Forms tilläggspaket är ett program som distribueras till AEM. I allmänhet behöver du bara en AEM (författare eller publicerad) för att köra AEM Forms Document Services. Följande topologi rekommenderas för att köra AEM Forms Document Services. Mer information om topologier finns i [Arkitektur och distributionstopologier för AEM Forms](/help/forms/using/aem-forms-architecture-deployment.md).

![Arkitektur och driftsättningstopologier för AEM Forms](do-not-localize/document-services.png)

>[!NOTE]
>
>Även om du kan använda AEM Forms för att konfigurera och köra alla funktioner från en enda server, bör du göra kapacitetsplanering, lastbalansering och konfigurera dedikerade servrar för specifika funktioner i en produktionsmiljö. Om du till exempel använder tjänsten PDF Generator för att konvertera tusentals sidor om dagen och flera adaptiva formulär för att hämta in data, kan du skapa separata AEM Forms-servrar för tjänsten PDF Generator och funktioner för adaptiva formulär. Det ger optimala prestanda och skalar servrarna oberoende av varandra.

## Systemkrav {#system-requirements}

Innan du börjar installera och konfigurera AEM Forms Document Services bör du kontrollera att:

* Maskinvaru- och programvaruinfrastruktur finns på plats. En detaljerad lista över maskin- och programvara som stöds finns i [tekniska krav](/help/sites-deploying/technical-requirements.md).

* Installationssökvägen för AEM-instansen innehåller inte blanksteg.
* En AEM körs. I AEM är &quot;instance&quot; en kopia av AEM som körs på en server i författar- eller publiceringsläge. I allmänhet behöver du bara en AEM (författare eller publicerad) för att köra AEM Forms Document Services:

   * **Författare**: En AEM som används för att skapa, överföra och redigera innehåll och för att administrera webbplatsen. När innehållet är klart att publiceras replikeras det till publiceringsinstansen.
   * **Publicera**: En AEM som skickar det publicerade innehållet till allmänheten via Internet eller ett internt nätverk.

* Minneskraven uppfylls. AEM Forms tilläggspaket kräver:

   * 15 GB temporärt utrymme för Microsoft Windows-baserade installationer.
   * 6 GB temporärt utrymme för UNIX-baserade installationer.

* Klientprogramvara som krävs för att skapa PDF för konvertering i Microsoft Windows och Linux installeras:

   * **Microsoft Windows**: Installera [Microsoft](/help/forms/using/aem-forms-jee-supported-platforms.md#p-software-support-for-pdf-generator-p)Office eller [Apache OpenOffice](/help/forms/using/aem-forms-jee-supported-platforms.md#software-support-for-pdf-generator)
   * **Linux**: Installera [Apache OpenOffice](/help/forms/using/aem-forms-jee-supported-platforms.md#p-software-support-for-pdf-generator-p)

>[!NOTE]
>
>* I Microsoft Windows stöder PDF Generator konverteringsvägar för WebKit, Acrobat WebCapture och PhantomJS för att konvertera HTML-filer till PDF-dokument.
>* På UNIX-baserade operativsystem stöder PDF Generator konverteringsvägar för WebKit och PhantomJS för att konvertera HTML-filer till PDF-dokument.

>



### Extra krav för UNIX-baserat operativsystem {#extrarequirements}

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

## Konfigurationer före installation {#preinstallationconfigurations}

Konfigurationer som listas i avsnittet med förinstallationskonfigurationer gäller endast för PDF Generator-tjänsten. Om du inte konfigurerar tjänsten PDF Generator kan du hoppa över konfigurationsavsnittet före installation.

### Installera Adobe Acrobat och tredjepartsprogram {#install-adobe-acrobat-and-third-party-applications}

Om du ska använda tjänsten PDF Generator för att konvertera filformat som Microsoft Word, Microsoft Excel, Microsoft PowerPoint, OpenOffice, WordPerfect X7 och Adobe Acrobat till PDF-dokument måste du kontrollera att de programmen är installerade på AEM Forms-servern.

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
>* Om du använder OpenOffice på en UNIX-baserad plattform kör du följande kommando för att ange variabeln path:

>
>  
`export OpenOffice_PATH=/opt/openoffice.org4`

### (Endast för IBM WebSphere) Konfigurera IBM SSL-socketprovider {#only-for-ibm-websphere-configure-ibm-ssl-socket-provider}

Utför följande steg för att konfigurera IBM SSL-socketprovidern:

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

1. Om du vill att AEM Forms-servern ska kunna använda den uppdaterade java.security-filen lägger du till följande java-argument när AEM Forms-servern startas:

   `-Djava.security.properties= [path of newly created Java.security file].`

### (Endast Windows) Konfigurera tjänsten Installera bläck och handskrift {#configure-install-ink-and-handwriting-service}

Om du kör Microsoft Windows Server konfigurerar du bläck- och handskriftstjänsten. Tjänsten krävs för att öppna Microsoft PowerPoint-filer som använder bläckfunktioner i Microsoft Office:

1. Öppna Serverhanteraren. Klicka på **[!UICONTROL Server Manager]** ikonen i snabbstartsfältet.
1. Klicka **[!UICONTROL Add Features]** på **[!UICONTROL Features]** menyn. Select the **[!UICONTROL Ink and Handwriting Services]** check box.
1. **[!UICONTROL Select Features]** med **[!UICONTROL Ink and Handwriting Services]** markerat. Klicka **[!UICONTROL Install]** så installeras tjänsten.

### (Endast Windows) Konfigurera inställningarna för filblock för Microsoft Office {#configure-the-file-block-settings-for-microsoft-office}

Ändra inställningarna för Microsoft Office Trust Center så att tjänsten PDF Generator kan konvertera filer som skapats med äldre versioner av Microsoft Office.

1. Öppna ett Microsoft Office-program. Exempel: Microsoft Word. Navigera till **[!UICONTROL File]**> **[!UICONTROL Options]**. Dialogrutan Alternativ visas.

1. Klicka **[!UICONTROL Trust Center]** och klicka på **[!UICONTROL Trust Center Settings]**.
1. In the **[!UICONTROL Trust Center settings]**, click **[!UICONTROL File Block Settings]**.
1. Avmarkera den filtyp **[!UICONTROL File Type]** som PDF Generator-tjänsten ska kunna konvertera till PDF-dokument i **[!UICONTROL Open]** listan.

### (Endast Windows) Bevilja privilegiet Ersätt en token på processnivå {#grant-the-replace-a-process-level-token-privilege}

Användarkontot som används för att starta programservern kräver privilegiet **Ersätt en token** på processnivå. Det lokala systemkontot har som standard privilegiet **Ersätt en token** på processnivå. För servrar som körs med en användare i gruppen Lokala administratörer måste privilegiet ges uttryckligen. Utför följande steg för att bevilja privilegiet:

1. Öppna grupprincipredigeraren för Microsoft Windows. Om du vill öppna grupprincipredigeraren klickar du på **[!UICONTROL Start]**, skriver **gpedit.msc** i rutan Starta sökning och klickar på **[!UICONTROL Group Policy Editor]**.
1. Navigera till **[!UICONTROL Local Computer Policy]** > **[!UICONTROL Computer Configuration]** > **[!UICONTROL Windows Settings]** > **[!UICONTROL Security Settings]** > **[!UICONTROL Local Policies]** > **[!UICONTROL User Rights Assignment]** och redigera **[!UICONTROL Replace a process level token]** profilen och inkludera gruppen Administratörer.
1. Lägg till användaren i posten Ersätt en processnivåtoken.

### (Endast Windows) Aktivera tjänsten PDF Generator för icke-administratörer {#enable-the-pdf-generator-service-for-non-administrators}

Du kan göra det möjligt för en icke-administratörsanvändare att använda PDF Generator-tjänsten. Normalt kan endast användare med administratörsbehörighet använda tjänsten:

1. Skapa en miljövariabel, PDFG_NON_ADMIN_ENABLED.
1. Ange värdet för miljövariabeln till TRUE.
1. Starta om AEM Forms-instansen.

### (Endast Windows) Inaktivera Kontroll av användarkonto (UAC) {#disable-user-account-control-uac}

1. Du öppnar verktyget Systemkonfiguration genom att gå till **[!UICONTROL Start > Run]** och sedan ange **[!UICONTROL MSCONFIG]**.
1. Klicka på **[!UICONTROL Tools]** fliken och rulla nedåt och välj **[!UICONTROL Change UAC Settings]**. Klicka **[!UICONTROL Launch]** för att köra kommandot i ett nytt fönster.
1. Justera skjutreglaget till nivån för Aldrig meddelande. När du är klar stänger du kommandofönstret och stänger fönstret Systemkonfiguration.
1. Kontrollera att registerinställningen för UAC är inställd på 0 (noll). Verifiera genom att utföra följande steg:

   1. Microsoft rekommenderar att du säkerhetskopierar registret innan du ändrar det. Detaljerade anvisningar finns i [Säkerhetskopiera och återställa registret i Windows](https://support.microsoft.com/en-us/help/322756).
   1. Öppna Microsoft Windows Registereditor. Öppna Registereditorn genom att gå till Start > Kör, skriva regedit och klicka på OK.
   1. Navigera till `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\policies\system\`. Kontrollera att värdet för EnableLUA är 0 (noll).
   1. Kontrollera att värdet för **EnableLUA** är 0 (noll). Om värdet inte är 0 ändrar du värdet till 0. Stäng Registereditorn.

1. Starta om datorn.

### (Endast Windows) Inaktivera felrapporteringstjänsten {#disable-error-reporting-service}

När du konverterar ett dokument till PDF med PDF Generator-tjänsten på Windows Server rapporterar Windows Server ibland att den körbara filen har stött på ett problem och måste stängas. PDF-konverteringen påverkas dock inte eftersom den fortsätter i bakgrunden.

Du kan undvika att få felmeddelanden genom att inaktivera Windows-felrapportering. Mer information om hur du inaktiverar felrapportering finns på [https://technet.microsoft.com/en-us/library/cc754364.aspx](https://technet.microsoft.com/en-us/library/cc754364.aspx).

### (Endast Windows) Konfigurera konvertering av HTML till PDF {#configure-html-to-pdf-conversion}

Tjänsten PDF Generator tillhandahåller vägar eller metoder för WebKit, WebCapture och PhantomJS för att konvertera HTML-filer till PDF-dokument. Om du vill aktivera konvertering för WebKit- och Acrobat WebCapture-vägar i Windows kopierar du Unicode-teckensnittet till katalogen %windir%\fonts.

>[!NOTE]
>
>När du installerar nya teckensnitt i teckensnittsmappen startar du om AEM Forms-instansen.

### (Endast UNIX-baserade plattformar) Extra konfigurationer för konvertering från HTML till PDF  {#extra-configurations-for-html-to-pdf-conversion}

På UNIX-baserade plattformar stöder PDF Generator-tjänsten WebKit- och PhantomJS-vägar för konvertering av HTML-filer till PDF-dokument. Om du vill aktivera konvertering från HTML till PDF utför du följande konfigurationer, som gäller för den konverteringsväg du föredrar:

### (Endast UNIX-baserade plattformar) Aktivera stöd för Unicode-teckensnitt (endast WebKit) {#enable-support-for-unicode-fonts-webkit-only}

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



## Installera AEM Forms tilläggspaket {#install-aem-forms-add-on-package}

AEM Forms tilläggspaket är ett program som distribueras till AEM. Paketet innehåller AEM Forms Document Services och andra AEM Forms-funktioner. Så här installerar du paketet:

1. Öppna [programvarudistribution](https://experience.adobe.com/downloads). Du behöver en Adobe ID för att logga in på Software Distribution.
1. Tryck **[!UICONTROL Adobe Experience Manager]** på rubrikmenyn.
1. I **[!UICONTROL Filters]** avsnittet:
   1. Välj **[!UICONTROL Forms]** i **[!UICONTROL Solution]** listrutan.
   2. Välj version och typ för paketet. Du kan också använda alternativet **[!UICONTROL Search Downloads]** för att filtrera resultaten.
1. Tryck på det paketnamn som gäller för ditt operativsystem, markera **[!UICONTROL Accept EULA Terms]** och tryck **[!UICONTROL Download]**.
1. Öppna [Pakethanteraren](https://docs.adobe.com/content/help/en/experience-manager-65/administering/contentmanagement/package-manager.html) och klicka **[!UICONTROL Upload Package]** för att överföra paketet.
1. Markera paketet och klicka på **[!UICONTROL Install]**.

   Du kan även hämta paketet via länken i artikeln om [AEM Forms-utgåvor](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html) .

1. När paketet har installerats uppmanas du att starta om AEM. **Stoppa inte servern omedelbart.** Innan du stoppar AEM Forms-servern väntar du tills meddelandena ServiceEvent REGISTERED och ServiceEvent UNREGISTERED inte visas i filen `[AEM-Installation-Directory]/crx-quickstart/logs/error`.log och loggen är stabil.

## Konfiguration efter installation {#post-installation-configurations}

### Konfigurera Boot Delegation för RSA/BouncyCastle-bibliotek  {#configure-boot-delegation-for-rsa-bouncycastle-libraries}

1. Stoppa AEM. Gå till [AEM installationskatalog]\crx-quickstart\conf\ folder. Öppna filen sling.properties för redigering.

   Om du använder `[AEM installation directory]\crx-quickstart\bin\start.bat` för att starta en AEM ska du redigera sling.properties som finns på `[AEM_root]\crx-quickstart\`.

1. Lägg till följande egenskaper i filen sling.properties:

   ```shell
   sling.bootdelegation.class.com.rsa.jsafe.provider.JsafeJCE=com.rsa.*
   ```

1. (Endast AIX) Lägg till följande egenskaper i filen sling.properties:

   ```shell
   sling.bootdelegation.xerces=org.apache.xerces.*
   ```

1. Spara och stäng filen.

### Konfigurera teckensnittshanterartjänsten  {#configuring-the-font-manager-service}

1. Logga in på [AEM Configuration Manager](http://localhost:4502/system/console/configMgr) som administratör.
1. Leta reda på och öppna **[!UICONTROL CQ-DAM-Handler-Gibson Font Managers]** tjänsten. Ange sökvägen till katalogerna System Fonts, Adobe Server Fonts och Customer Fonts. Klicka på **[!UICONTROL Save]**.

   >[!NOTE]
   >
   >Din rätt att använda teckensnitt som tillhandahålls av andra parter än Adobe regleras av de licensavtal som dessa parter ger dig med dessa teckensnitt och omfattas inte av din licens att använda Adobe. Adobe rekommenderar att du granskar och kontrollerar att du följer alla tillämpliga licensavtal som inte är Adobe innan du använder teckensnitt som inte är Adobe med Adobe, särskilt när det gäller användning av teckensnitt i servermiljöer.
   > När du installerar nya teckensnitt i teckensnittsmappen startar du om AEM Forms-instansen.

### Konfigurera ett lokalt användarkonto för att köra PDF Generator-tjänsten  {#configure-a-local-user-account-to-run-the-pdf-generator-service}

Det krävs ett lokalt användarkonto för att köra PDF Generator-tjänsten. Anvisningar om hur du skapar en lokal användare finns i [Skapa ett användarkonto i Windows](https://support.microsoft.com/en-us/help/13951/windows-create-user-account) eller [skapa ett användarkonto på UNIX-baserade plattformar](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/4/html/Step_by_Step_Guide/s1-starting-create-account.html).

1. Öppna konfigurationssidan för [AEM Forms PDF Generator](http://localhost:4502/libs/fd/pdfg/config/ui.html) .

1. Ange autentiseringsuppgifter för ett lokalt användarkonto på **[!UICONTROL User Accounts]** fliken och klicka på **[!UICONTROL Submit]**. Tillåt åtkomst till användaren om Microsoft Windows tillfrågas. När den konfigurerade användaren läggs till visas den under **[!UICONTROL Your user accounts]** avsnittet på **[!UICONTROL User Accounts]** fliken.

### Konfigurera timeout-inställningar {#configure-the-time-out-settings}

1. Leta [AEM och öppna](http://localhost:4502/system/console/configMgr)tjänsten i konfigurationshanteraren **[!UICONTROL Jacorb ORB Provider]** .

   Lägg till följande i **[!UICONTROL Custom Properties.name]** fältet och klicka på **[!UICONTROL Save]**. Tidsgränsen för väntande svar (kallas även CORBA-klienttimeout) anges till 600 sekunder.

   `jacorb.connection.client.pending_reply_timeout=600000`

1. Logga in på AEM författarinstans och navigera till **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Tools]** > **[!UICONTROL Forms]** > **[!UICONTROL Configure PDF Generator]**. Standardwebbadressen är http://localhost:4502/libs/fd/pdfg/config/ui.html.

   Öppna **[!UICONTROL General Configuration]** fliken och ändra värdet för följande fält för din miljö:

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

### (Endast Windows) Konfigurera Acrobat för tjänsten PDF Generator {#configure-acrobat-for-the-pdf-generator-service}

I Microsoft Windows använder PDF Generator-tjänsten Adobe Acrobat för att konvertera filformat som stöds till PDF-dokument. Så här konfigurerar du Adobe Acrobat för tjänsten PDF Generator:

1. Öppna Acrobat och välj **[!UICONTROL Edit]**> **[!UICONTROL Preferences]**> **[!UICONTROL Updater]**. I Leta efter uppdateringar avmarkerar du **[!UICONTROL Automatically install updates]** och klickar på **[!UICONTROL OK]**. Stäng Acrobat.
1. Dubbelklicka på ett PDF-dokument på datorn. När Acrobat startas för första gången visas dialogrutorna för inloggning, välkomstskärm och licensavtal. Stäng de här dialogrutorna för alla användare som har konfigurerats att använda PDF Generator.
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

### (Endast Windows) Konfigurera primär väg för konvertering från HTML till PDF {#configure-primary-route-for-html-to-pdf-conversion-windows-only}

Tjänsten PDF Generator erbjuder flera vägar för att konvertera HTML-filer till PDF-dokument: Webkit, Acrobat WebCapture (endast Windows) och PhantomJS. Adobe rekommenderar att du använder PhantomJS-vägen eftersom den kan hantera dynamiskt innehåll och inte har några beroenden till 32-bitars bibliotek, 32-bitars JDK eller inte kräver några extra teckensnitt. Inte heller PhantomJS-vägen kräver sudo- eller root-åtkomst för att köra konverteringen.

Den primära standardvägen för konvertering från HTML till PDF är Webkit. Så här ändrar du konverteringsflödet:

1. Navigera AEM författarinstansen till **[!UICONTROL Tools]**> **[!UICONTROL Forms]**> **[!UICONTROL Configure PDF Generator]**.

1. Välj önskat konverteringsflöde i listrutan på **[!UICONTROL General Configuration]** fliken **[!UICONTROL Primary Route for HTML to PDF conversions]** .

### Initiera Global Trust Store {#intialize-global-trust-store}

Med pålitlighetslagerhanteringen kan du importera, redigera och ta bort certifikat som du litar på på servern för validering av digitala signaturer och certifikatautentisering. Du kan importera och exportera valfritt antal certifikat. När ett certifikat har importerats kan du redigera pålitlighetsinställningarna och förtroendearkivets typ. Så här initierar du ett förtroendearkiv:

1. Logga in på AEM Forms som administratör.
1. Gå till **[!UICONTROL Tools]** > **[!UICONTROL Security]** > **[!UICONTROL Trust Store]**.
1. Klicka på  **[!UICONTROL Create TrustStore]**. Ange lösenord och tryck **[!UICONTROL Save]**.

### Konfigurera certifikat för Reader-tilläggs- och krypteringstjänsten {#set-up-certificates-for-reader-extension-and-encryption-service}

DocAssurance-tjänsten kan tillämpa användningsrättigheter på PDF-dokument. Konfigurera certifikaten om du vill tillämpa användningsbehörighet för PDF-dokument.

Innan du konfigurerar certifikaten bör du kontrollera att du har en:

* Certifikatfil (.pfx).

* Lösenordet för den privata nyckeln som tillhandahålls med certifikatet.

* Alias för privat nyckel. Du kan köra kommandot för Java-nyckelverktyget för att visa alias för den privata nyckeln:
   `keytool -list -v -keystore [keystore-file] -storetype pkcs12`

* Lösenord för nyckelbehållarfil. Om du använder certifikatet för Adobe Reader Extensions är lösenordet för nyckelfilen alltid detsamma som lösenordet för den privata nyckeln.

Utför följande steg för att konfigurera certifikaten:

1. Logga in på AEM Author-instansen som administratör. Gå till **[!UICONTROL Tools]** > **[!UICONTROL Security]** > **[!UICONTROL Users]**.
1. Klicka på **[!UICONTROL name]** fältet för användarkontot. The **[!UICONTROL Edit User Settings]** page opens. På AEM Author-instansen finns certifikat i KeyStore. Om du inte har skapat en KeyStore tidigare klickar du på **[!UICONTROL Create KeyStore]** och anger ett nytt lösenord för KeyStore. Om servern redan innehåller en KeyStore hoppar du över det här steget.  Om du använder certifikatet för Adobe Reader Extensions är lösenordet för nyckelfilen alltid detsamma som lösenordet för den privata nyckeln.
1. Markera **[!UICONTROL Edit User Settings]** fliken på **[!UICONTROL KeyStore]** sidan. Expandera **[!UICONTROL Add Private Key from Key Store file]** alternativet och ange ett alias. Aliaset används för att utföra Reader-tilläggsåtgärden.
1. Om du vill överföra certifikatfilen klickar du på **[!UICONTROL Select Key Store File]** och överför en .pfx-fil.

   Lägg till **[!UICONTROL Key Store Password]**, **[!UICONTROL Private Key Password]** och **[!UICONTROL Private Key Alias]** det som är kopplat till certifikatet i respektive fält. Klicka på **[!UICONTROL Submit]**.

   >[!NOTE]
   >
   >I produktionsmiljön ersätter du dina utvärderingsreferenser med produktionsuppgifter. Se till att du tar bort dina gamla inloggningsuppgifter för Reader Extensions innan du uppdaterar en inloggningsuppgift som har gått ut eller utvärderar den.

1. Klicka på **[!UICONTROL Save & Close]** på sidan **[!UICONTROL Edit User Settings]**.

### Aktivera AES-256 {#enable-aes}

Om du vill använda AES 256-kryptering för PDF-filer hämtar och installerar du Java Cryptography Extension (JCE) Unlimited Strength Jurisdential Policy-filer. Ersätt filerna local_policy.jar och US_export_policy.jar i mappen jre/lib/security. Om du till exempel använder Sun JDK kopierar du de hämtade filerna till `[JAVA_HOME]/jre/lib/security` mappen.

Assembler-tjänsten är beroende av tjänsten Reader Extensions, tjänsten Signature, Forms och Output. Utför följande steg för att verifiera att de tjänster som krävs är igång:

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
   <td>com.adobe.livecycle.adobe-lc-forms-bedrock-connector<br /> </td> 
  </tr> 
  <tr> 
   <td>Utdatatjänst</td> 
   <td>com.adobe.livecycle.adobe-lc-forms-bedrock-connector</td> 
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

Du har en fungerande AEM Forms Document Services-miljö. Du kan använda dokumenttjänster via:

* [Formulärbaserade arbetsflöden i OSGi](/help/forms/using/aem-forms-workflow.md)
* [Bevakade mappar](/help/forms/using/watched-folder-in-aem-forms.md)
* [API:er för dokumenttjänster](/help/forms/using/aem-document-services-programmatically.md)

