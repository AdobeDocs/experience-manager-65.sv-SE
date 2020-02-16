---
title: Så här arbetar du med paket
seo-title: Så här arbetar du med paket
description: Lär dig grunderna i hur du arbetar med paket i AEM.
seo-description: Lär dig grunderna i hur du arbetar med paket i AEM.
uuid: cba76a5f-5d75-4d63-a0f4-44c13fa1baf2
contentOwner: Chiradeep Majumdar
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: content
content-type: reference
discoiquuid: 6694a135-d1e1-4afb-9f5b-23991ee70eee
docset: aem65
translation-type: tm+mt
source-git-commit: 5e10ddb0e5cf24e1915d0840cd380520374e93ea

---


# Så här arbetar du med paket{#how-to-work-with-packages}

Med paket kan du importera och exportera databasinnehåll. Du kan till exempel använda paket för att installera nya funktioner, överföra innehåll mellan instanser och säkerhetskopiera databasinnehåll.

Paket kan öppnas och/eller underhållas från följande sidor:

* [Package Manager](#package-manager), som du använder för att hantera paketen i din lokala AEM-instans.

* [Paketresurs](#package-share), en centraliserad server som innehåller både offentligt tillgängliga paket och de som är privata för ditt företag. De publika paketen kan innehålla snabbkorrigeringar, nya funktioner, dokumentation m.m.

Du kan överföra paket mellan Package Manager, Package Share och ditt filsystem.

## Vad är paket? {#what-are-packages}

Ett paket är en zip-fil som innehåller databasinnehåll i form av en filsystemserialisering (kallas vault-serialisering). Detta ger en lättanvänd och redigerbar representation av filer och mappar.

Paket innehåller innehåll, både sidinnehåll och projektrelaterat innehåll, som väljs med filter.

Ett paket innehåller även vaultmetainformation, inklusive filterdefinitioner och importkonfigurationsinformation. Ytterligare innehållsegenskaper (som inte används för paketextrahering) kan inkluderas i paketet, till exempel en beskrivning, en visuell bild eller en ikon. dessa egenskaper är avsedda för innehållspaketkonsumenten och endast för informationsändamål.

>[!NOTE]
>
>Paket representerar den aktuella versionen av innehållet när paketet skapas. De innehåller inga tidigare versioner av det innehåll som AEM sparar i databasen.

Du kan utföra följande åtgärder på eller med paket:

* Skapa nya paket; definiera paketinställningar och filter efter behov
* Förhandsgranska paketinnehåll (före bygge)
* Skapa paket
* Visa paketinformation
* Visa paketinnehåll (efter bygget)
* Ändra definitionen för befintliga paket
* Återskapa befintliga paket
* Radbryt paket
* Hämta paket från AEM till ditt filsystem
* Överför paket från filsystemet till den lokala AEM-instansen
* Validera paketinnehåll före installation
* Utför en torr installation
* Installera paket (AEM installerar inte paket automatiskt efter överföring)
* Ta bort paket
* Hämta paket, till exempel snabbkorrigeringar, från paketdelningsbiblioteket
* Överför paket till den företagsinterna sektionen i biblioteket Paketresurs

## Paketinformation {#package-information}

En paketdefinition består av olika typer av information:

* [Paketinställningar](#package-settings)
* [Paketfilter](#package-filters)
* [Paketskärmbilder](#package-screenshots)
* [Paketikoner](#package-icons)

### Paketinställningar {#package-settings}

Du kan redigera olika paketinställningar för att definiera aspekter som paketbeskrivning, relaterade fel, beroenden och providerinformation.

Dialogrutan **Paketinställningar** är tillgänglig via knappen **Redigera** när du [skapar](#creating-a-new-package) eller [redigerar](#viewing-and-editing-package-information) ett paket och innehåller tre flikar för konfiguration. Klicka på **OK** för att spara ändringarna när du har gjort dem.

![packagenredigera](assets/packagesedit.png)

| **Fält** | **Beskrivning** |
|---|---|
| Namn | Paketets namn. |
| Grupp | Namnet på gruppen som paketet ska läggas till i, för att organisera paket. Skriv namnet på en ny grupp eller markera en befintlig grupp. |
| Version | Text som ska användas för den anpassade versionen. |
| Beskrivning | En kort beskrivning av paketet. HTML-kod kan användas för formatering. |
| Miniatyrbild | Ikonen som visas med paketlistan. Klicka på Bläddra för att välja en lokal fil. |

![chlimage_1-108](assets/chlimage_1-108.png)

<table>
 <tbody>
  <tr>
   <th><strong>Fält</strong></th>
   <th><strong>Beskrivning</strong></th>
   <th><strong>Format/exempel</strong></th>
  </tr>
  <tr>
   <td>Namn</td>
   <td>Namnet på providern.</td>
   <td><em>AEM Geometrixx<br /> </em></td>
  </tr>
  <tr>
   <td>Webbadress</td>
   <td>URL för providern.</td>
   <td><em>https://www.aem-geometrixx.com</em></td>
  </tr>
  <tr>
   <td>Länk</td>
   <td>Paketspecifik länk till en providersida.</td>
   <td><em>https://www.aem-geometrixx.com/mypackage.html</em></td>
  </tr>
  <tr>
   <td>Kräver<br /> </td>
   <td>
    <ul>
     <li>Administratör: Välj när paketet bara kan installeras av ett konto med administratörsbehörighet.</li>
     <li>Starta om: Välj när servern måste startas om efter att paketet har installerats.</li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td>AC-hantering</td>
   <td><p>Ange hur åtkomstkontrollsinformationen som definieras i paketet ska hanteras när paketet importeras:</p>
    <ul>
     <li><strong>Ignorera</strong></li>
     <li><strong>Skriv över</strong></li>
     <li><strong>Sammanfoga</strong></li>
     <li><strong>Radera</strong></li>
     <li><strong>MergePreserve</strong></li>
    </ul> <p>The default value is <strong>Ignore</strong>.</p> </td>
   <td>
    <ul>
     <li><strong>Ignorera</strong> - bevara åtkomstkontrollistor i databasen</li>
     <li><strong>Skriv över</strong> - skriv över ACL:er i databasen</li>
     <li><strong>Sammanfoga</strong> - sammanfoga båda uppsättningarna med åtkomstkontrollistor</li>
     <li><strong>Rensa</strong> - rensa ACL:er</li>
     <li><strong>MergePreserve</strong> - sammanfoga åtkomstkontrollen i innehållet med den som ingår i paketet genom att lägga till åtkomstkontrollposterna för objekt som inte finns i innehållet</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

![paketerberoenden](assets/packagesdependencies.png)

| **Fält** | **Beskrivning** | **Format/exempel** |
|---|---|---|
| Testad med | Det produktnamn och den version som det här paketet har eller är kompatibelt med. | *AEM6* |
| Åtgärdade fel | Ett textfält där du kan visa information om fel som har åtgärdats i det här paketet. Visa varje fel på en separat rad. | bug-nr summary |
| Beroende på | Visar beroendeinformation som måste respekteras när andra paket är nödvändiga för att det aktuella paketet ska kunna köras som förväntat. Det här fältet är viktigt när du använder snabbkorrigeringar. | groupId:name:version |
| Ersätter | En lista över borttagna paket som det här paketet ersätter. Innan du installerar kontrollerar du att det här paketet innehåller allt nödvändigt innehåll från de föråldrade paketen, så att inget innehåll skrivs över. | groupId:name:version |

### Paketfilter {#package-filters}

Filter identifierar databasnoderna som ska inkluderas i paketet. En **filterdefinition** anger följande information:

* Rotsökvägen **till** innehållet som ska inkluderas.
* **Regler** som innehåller eller exkluderar specifika noder under rotsökvägen.

Filter kan innehålla noll eller flera regler. När inga regler har definierats innehåller paketet allt innehåll under rotsökvägen.

Du kan definiera en eller flera filterdefinitioner för ett paket. Använd mer än ett filter för att inkludera innehåll från flera rotsökvägar.

![chlimage_1-109](assets/chlimage_1-109.png)

Följande tabell beskriver dessa regler och innehåller exempel:

<table>
 <tbody>
  <tr>
   <th> Regeltyp</th>
   <th>Beskrivning </th>
   <th>Exempel </th>
  </tr>
  <tr>
   <td> include</td>
   <td>Du kan definiera en sökväg eller använda ett reguljärt uttryck för att ange alla noder som du vill ta med.<br /> <br /> Om du tar med en katalog kommer:
    <ul>
     <li>ta med den katalogen <i>och</i> alla filer och mappar i den katalogen (dvs hela underträdet)</li>
     <li><strong>inte</strong> inkludera andra filer eller mappar från den angivna rotsökvägen</li>
    </ul> </td>
   <td>/libs/sling/install(/.*)? </td>
  </tr>
  <tr>
   <td> exclude</td>
   <td>Du kan ange en sökväg eller använda ett reguljärt uttryck för att ange alla noder som du vill utesluta.<br /> Om du <br /> exkluderar en katalog exkluderas den katalogen <i>och</i> alla filer och mappar i den katalogen (dvs. hela underträdet).<br /> </td>
   <td>/libs/wcm/foundation/components(/.*)?</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Ett paket kan innehålla flera filterdefinitioner, så att noder från olika platser enkelt kan kombineras till ett paket.

Paketfilter definieras oftast när du först [skapar paketet](#creating-a-new-package), men de kan redigeras vid ett senare tillfälle (efter vilket paketet ska återskapas).

### Paketskärmbilder {#package-screenshots}

Du kan bifoga skärmbilder till ditt paket för att få en visuell representation av hur innehållet ser ut; genom att t.ex. tillhandahålla skärmbilder av nya funktioner.

### Paketikoner {#package-icons}

Du kan även bifoga en ikon till paketet för att få en snabb visuell representation av vad paketet innehåller. Detta visas sedan i paketlistan och kan hjälpa dig att enkelt identifiera paketet eller paketklassen.

Eftersom ett paket kan innehålla en ikon används följande konventioner för officiella paket:

>[!NOTE]
>
>Undvik förvirring genom att använda en beskrivande ikon för paketet och använd inte någon av de officiella ikonerna.

Officiellt snabbkorrigeringspaket:

![](do-not-localize/chlimage_1-28.png)

Officiell AEM-installation eller tilläggspaket:

Officiella funktionspaket:

![](do-not-localize/chlimage_1-29.png)

## Pakethanteraren {#package-manager}

Pakethanteraren hanterar paketen i din lokala AEM-installation. När du har [tilldelat nödvändiga behörigheter](#permissions-needed-for-using-the-package-manager) kan du använda pakethanteraren för olika åtgärder, bland annat för att konfigurera, bygga, hämta och installera dina paket. Nyckelelementen som ska konfigureras är:

* [Paketinställningar](#package-settings)
* [Paketfilter](#package-filters)

### Behörigheter som krävs för att använda Pakethanteraren {#permissions-needed-for-using-the-package-manager}

Om du vill ge användarna rätt att skapa, ändra, överföra och installera paket måste du ge dem rätt behörighet på följande platser:

* **/etc/paket** (fullständig behörighet exklusive radering)
* noden som innehåller paketets innehåll

Se [Ange behörigheter](/help/sites-administering/security.md#setting-page-permissions) för instruktioner om hur du ändrar behörigheter.

### Skapa ett nytt paket {#creating-a-new-package}

Så här skapar du en ny paketdefinition:

1. På välkomstskärmen i AEM klickar du på **Paket** (eller från **verktygskonsolen** dubbelklickar du på **Paket**).

1. Välj sedan **Pakethanteraren**.
1. Klicka på **Skapa paket**.

   >[!NOTE]
   >
   >Om din instans har många paket kan det finnas en mappstruktur på plats, så du kan navigera till den önskade målmappen innan du skapar det nya paketet.

1. I dialogrutan:

   ![paketernyhet](assets/packagesnew.png)

   Ange följande:

   * **Gruppnamn**

      Målgruppens (eller mappens) namn. Grupper är avsedda att användas för att hjälpa dig att ordna dina paket.

      En mapp skapas för gruppen om den inte redan finns. Om du lämnar gruppnamnet tomt skapas paketet i huvudpaketlistan (Hem > Paket).

   * **Paketnamn**

      Namnet på det nya paketet. Välj ett beskrivande namn som hjälper dig (och andra) att enkelt identifiera innehållet i paketet.

   * **Version**

      Ett textfält där du kan ange en version. Detta läggs till paketnamnet för att bilda zip-filens namn.
   Skapa paketet genom att klicka på **OK** .

1. AEM listar det nya paketet i lämplig gruppmapp.

   ![packagesitem](assets/packagesitem.png)

   Klicka på ikonen eller paketnamnet som du vill öppna.

   ![packagesiklickad](assets/packagesitemclicked.png)

   >[!NOTE]
   >
   >Du kan vid behov gå tillbaka till den här sidan senare.

1. Klicka på **Redigera** för att redigera [paketinställningarna](#package-settings).

   Här kan du lägga till information och/eller definiera vissa inställningar. till exempel innehåller de en beskrivning, [ikon](#package-icons), relaterade fel och lägger till providerinformation.

   Klicka på **OK** när du är klar med redigeringen av inställningarna.

1. Lägg till **[skärmbilder](#package-screenshots)**i paketet efter behov. En instans är tillgänglig när paketet skapas. Lägg till fler om det behövs med **Package Screenshot**från sidespark.

   Lägg till den faktiska bilden genom att dubbelklicka på bildkomponenten i området **Skärmbilder** , lägga till en bild och klicka på **OK**.

1. Definiera **[paketfiltren](#package-filters)**genom att dra instanser av **filterdefinitionen**från sidosparken och sedan dubbelklicka för att öppna dem för redigering:

   ![paketerfilter](assets/packagesfilter.png)

   Ange:

   * **Rotsökväg** Innehållet som ska paketeras. kan vara roten i ett underträd.
   * **Regler**&#x200B;är frivilliga. för enkla paketdefinitioner är det inte nödvändigt att ange inkluderings- eller exkluderingsregler.

      Om det behövs kan du definiera reglerna [****Inkludera** eller **Uteslut](#package-filters)för att definiera paketets innehåll exakt.

      Lägg till regler med **+** -symbolen, eller ta bort regler med **-** -symbolen. Regler tillämpas efter deras ordning så att de kan placeras efter behov med knapparna **Upp** och **Ned** .
   Klicka sedan på **OK** för att spara filtret.

   >[!NOTE]
   >
   >Du kan använda så många filterdefinitioner du behöver, men du måste se till att de inte hamnar i konflikt. Använd **Förhandsgranska** för att bekräfta vad paketinnehållet ska vara.

1. Du kan använda **Förhandsgranska** för att bekräfta vad paketet innehåller. Detta utför en torr körning av byggprocessen och visar allt som kommer att läggas till i paketet när det byggs.
1. Nu kan du [skapa](#building-a-package) ditt paket.

   >[!NOTE]
   >
   >Det är inte obligatoriskt att bygga paketet just nu, det kan göras vid en senare tidpunkt.

### Bygga ett paket {#building-a-package}

Ett paket skapas ofta samtidigt som du [skapar paketdefinitionen](#creating-a-new-package), men du kan gå tillbaka vid ett senare tillfälle för att antingen skapa eller återskapa paketet. Detta kan vara användbart om innehållet i databasen har ändrats.

>[!NOTE]
>
>Innan du skapar paketet kan det vara användbart att förhandsgranska innehållet i paketet. Det gör du genom att klicka på **Förhandsgranska**.

1. Öppna paketdefinitionen från **pakethanteraren** (klicka på paketikonen eller paketnamnet).

1. Klicka på **Skapa**. En dialogruta där du uppmanas bekräfta att du vill skapa paketet.

   >[!NOTE]
   >
   >Detta är särskilt viktigt när du återskapar ett paket eftersom paketinnehållet skrivs över.

1. Click **OK**. AEM kommer att bygga paketet med allt innehåll som läggs till i paketet. När AEM är klart visas en bekräftelse på att paketet har skapats och (när du stänger dialogrutan) information om paketlistan uppdateras.

### Rewrapping a Package {#rewrapping-a-package}

När ett paket har byggts kan det vid behov rewrappas.

När du återställer paket ändras paketinformationen *utan* att paketinnehållet ändras. Paketinformationen är miniatyrbilden, beskrivningen osv., vilket innebär att allt du kan redigera i dialogrutan **Paketinställningar** (för att öppna den här klickningen på **Redigera**).

Ett viktigt användningsområde för ombrytning är när du förbereder ett paket för paketresursen. Du kan till exempel ha ett befintligt paket och bestämma dig för att dela det med andra. För det vill du lägga till en miniatyrbild och lägga till en beskrivning. I stället för att återskapa hela paketet med alla dess funktioner (vilket kan ta en stund och innebär att paketet inte längre är identiskt med originalpaketet) kan du kapsla in det och bara lägga till miniatyrbilden och beskrivningen.

1. Öppna paketdefinitionen från **pakethanteraren** (klicka på paketikonen eller paketnamnet).

1. Klicka på **Redigera** och uppdatera **[paketinställningarna](#package-settings)**efter behov. Spara genom att klicka på&#x200B;**OK**.

1. Klicka på **Radbryt**, så visas en dialogruta där du får bekräfta.

### Visa och redigera paketinformation {#viewing-and-editing-package-information}

Så här visar eller redigerar du information om en paketdefinition:

1. Gå till det paket du vill visa i Pakethanteraren.
1. Klicka på paketikonen för det paket som du vill visa. Paketsidan med information om paketdefinitionen öppnas:

   ![packagesiklickad-1](assets/packagesitemclicked-1.png)

   >[!NOTE]
   >
   >Du kan även redigera och utföra vissa åtgärder på paketet från den här sidan.
   >
   >Vilka knappar som är tillgängliga beror på om paketet redan har skapats eller inte.

1. Om paketet redan har byggts klickar du på **Innehåll**, så öppnas ett fönster där allt innehåll i paketet visas:

### Innehåll och testinstallation för visning av paket {#viewing-package-contents-and-testing-installation}

När ett paket har skapats kan du visa innehållet:

1. Gå till det paket du vill visa i Pakethanteraren.
1. Klicka på paketikonen för det paket som du vill visa. Detta öppnar paketsidan med information om paketdefinitionen.

1. Om du vill visa innehållet klickar du på **Innehåll** i ett fönster och visar hela innehållet i paketet:

   ![packningar](assets/packgescontents.png)

1. Om du vill utföra en torr installation klickar du på **Testinstallation**. När du har bekräftat åtgärden öppnas ett fönster där resultatet visas som om installationen utfördes:

   ![paketestestinstallera](assets/packagestestinstall.png)

### Hämtar paket till filsystemet {#downloading-packages-to-your-file-system}

I det här avsnittet beskrivs hur du hämtar ett paket från AEM till ditt filsystem med hjälp av **Package Manager**.

>[!NOTE]
>
>Se [Paketdelning](#package-share) för information om hur du hämtar snabbkorrigeringar, funktionspaket och paket från den offentliga delen och företagets interna del av paketdelningen.
>
>Från paketresurs kan du:
>
>* hämta paket från [Package Share direkt till din lokala AEM-instans](#downloading-and-installing-packages-from-package-share).
   >  När du laddar ned paketet importeras det till din databas, varefter du omedelbart kan installera det på din lokala instans med **Pakethanteraren**. Dessa paket innehåller snabbkorrigeringar och andra delade paket.
   >
   >
* hämta paket från [Package Share till filsystemet](#downloading-packages-to-your-file-system-from-package-share).
>



1. På välkomstskärmen i AEM klickar du på **Paket** och väljer sedan **Pakethanteraren**.
1. Navigera till paketet som du vill hämta.

   ![paketerladda ned](assets/packagesdownload.png)

1. Klicka på länken som utgörs av zip-filens namn (understruken) för paketet som du vill hämta; till exempel `export-for-offline.zip`.

   AEM hämtar paketet till din dator (med en standarddialogruta för hämtning av webbläsare).

### Överför paket från filsystemet {#uploading-packages-from-your-file-system}

Med en paketöverföring kan du överföra ett paket från filsystemet till AEM Package Manager.

>[!NOTE]
>
>Se [Överföra paket till företagets interna paketresurs](#uploading-packages-to-the-company-internal-package-share) för att överföra ett paket till företagets privata område i paketresursen.

Så här överför du ett paket:

1. Navigera till **Pakethanteraren**. Till den gruppmapp som du vill att paketet ska överföras till.

   ![paketerupload, knapp](assets/packagesuploadbutton.png)

1. Klicka på **Överför paket**.

   ![paketeruploaddialog](assets/packagesuploaddialog.png)

   * **Arkiv**

      **Du kan antingen skriva filnamnet direkt eller använda** Bläddra.. för att välja det paket som krävs från det lokala filsystemet (efter att du har valt **OK**).

   * **Tvinga överföring**

      Om det redan finns ett paket med det här namnet kan du klicka på det här om du vill framtvinga en överföring (och skriva över det befintliga paketet).
   Klicka på **OK** så att det nya paketet överförs och visas i pakethanterarlistan.

   >[!NOTE]
   >
   >Om du vill göra innehållet tillgängligt för AEM måste du [installera paketet](#installing-packages).

### Verifierar paket {#validating-packages}

Innan du installerar ett paket kanske du vill verifiera dess innehåll. Eftersom paket kan ändra överlagrade filer under `/apps` och/eller lägga till, ändra och ta bort åtkomstkontrollistor, är det ofta användbart att validera dessa ändringar innan du installerar.

#### Valideringsalternativ {#validation-options}

Valideringsmekanismen kan kontrollera följande egenskaper hos paketet:

* OSGi-paketimporter
* Övertäckningar
* ACL

Dessa alternativ beskrivs nedan.

* **Validera OSGi-paketimporter**

   **Vad är markerat**

   Den här valideringen undersöker paketet för alla JAR-filer (OSGi-paket), extraherar deras `manifest.xml` (som innehåller de versionshanteringsberoenden som OSGi-paketet är beroende av) och verifierar AEM-instansens export av dessa beroenden med rätt versioner.

   **Hur det rapporteras**

   Versionsberoenden som inte kan uppfyllas av AEM-instansen visas i **aktivitetsloggen** för pakethanteraren.

   **Fellägen**

   Om beroenden inte uppfylls startar inte OSGi-paketen med dessa beroenden. Detta resulterar i en trasig programdistribution eftersom allt som förlitar sig på det OSGi-paket som inte startats i sin tur inte fungerar som det ska.

   **Felupplösning**

   För att åtgärda fel på grund av att OSGi-paketen inte är nöjd måste beroendeversionen i paketet med otillfredsställande importer justeras.

* **Validera övertäckningar**

   **Vad är markerat**

   Valideringen avgör om paketet som installeras innehåller en fil som redan finns i AEM-målinstansen.

   Om det till exempel finns en övertäckning på `/apps/sling/servlet/errorhandler/404.jsp`är det ett paket som innehåller `/libs/sling/servlet/errorhandler/404.jsp`så att den ändrar den befintliga filen på `/libs/sling/servlet/errorhandler/404.jsp`.

   **Hur det rapporteras**

   Alla sådana övertäckningar beskrivs i **aktivitetsloggen** i pakethanteraren.

   **Fellägen**

   Ett feltillstånd innebär att paketet försöker distribuera en fil som redan är överlagrad, vilket innebär att ändringarna i paketet åsidosätts (och därmed&quot;döljs&quot;) av övertäckningen och inte börjar gälla.

   **Felupplösning**

   För att lösa det här problemet måste den som ansvarar för övertäckningsfilens struktur i `/apps` granska ändringarna i den överliggande filen i `/libs` och införliva ändringarna efter behov i övertäckningen ( `/apps`) samt distribuera den överliggande filen på nytt.

   >[!NOTE]
   >
   >Observera att valideringsfunktionen inte kan stämma av om det överlagda innehållet har integrerats korrekt i överläggsfilen. Valideringen fortsätter därför att rapportera om konflikter även efter att nödvändiga ändringar har gjorts.

* **Validera åtkomstkontrollistor**

   **Vad är markerat**

   Valideringen kontrollerar vilka behörigheter som läggs till, hur de hanteras (sammanfoga/ersätt) och om de aktuella behörigheterna påverkas.

   **Hur det rapporteras**

   Behörigheterna beskrivs i **aktivitetsloggen** för Package Manager.

   **Fellägen**

   Inga explicita fel kan anges. Valideringen anger bara om nya ACL-behörigheter kommer att läggas till eller påverkas av att paketet installeras.

   **Felupplösning**

   Med hjälp av den information som valideringen ger kan de påverkade noderna granskas i CRXDE och åtkomstkontrollistorna kan justeras i paketet efter behov.

   >[!CAUTION]
   >
   >Vi rekommenderar att paketen inte påverkar AEM-tillhandahållna ACL:er eftersom detta kan leda till oväntade produktbeteenden.

#### Utför validering {#performing-validation}

Paketvalidering kan göras på två olika sätt:

* Via pakethanterarens gränssnitt
* Via HTTP POST-begäran, till exempel med cURL

>[!NOTE]
>
>Validering ska alltid ske efter att paketet har överförts, men innan det installeras.

**Paketvalidering via Pakethanteraren**

1. Öppna packningshanteraren på `https://<server>:<port>/crx/packmgr`
1. Markera paketet i listan och välj sedan **Mer** i listrutan och **Validera** i listrutan.

   >[!NOTE]
   >
   >Detta bör göras efter att du har överfört innehållspaketet, men innan du installerar paketet.

1. I den modala dialogrutan som visas använder du kryssrutorna för att välja valideringstyp(er) och börja valideringen genom att klicka på **Validera**. Du kan också klicka på **Avbryt**.

1. De valda valideringarna körs sedan. Resultaten visas i aktivitetsloggen för Package Manager.

**Paketvalidering via HTTP POST-begäran**

POST-begäran har följande format.

```
https://<host>:<port>/crx/packmgr/service.jsp?cmd=validate&type=osgiPackageImports,overlays,acls
```

>[!NOTE]
>
>Parametern kan vara vilken kommaseparerad, osorterad lista som helst som består av: `type`
>
>* `osgiPackageImports`
>* `overlays`
>* `acls`
>
>
Standardvärdet är `type``osgiPackageImports` om det inte skickas.

Följande är ett exempel på hur du använder cURL för att köra en paketvalidering.

1. Om du använder cURL kör du en programsats som liknar följande:

   ```shell
   curl -v -X POST --user admin:admin -F file=@/Users/SomeGuy/Desktop/core.wcm.components.all-1.1.0.zip 'http://localhost:4502/crx/packmgr/service.jsp?cmd=validate&type=osgiPackageImports,overlays,acls'
   ```

1. Den begärda valideringen körs och svaret skickas tillbaka som ett JSON-objekt.

>[!NOTE]
>
>Svaret på en HTTP POST-begäran för validering är ett JSON-objekt med valideringsresultatet.

### Installerar paket {#installing-packages}

När du har överfört ett paket måste du installera innehållet. Om paketinnehållet ska vara installerat och fungera måste det vara både:

* inläst i AEM (antingen [överförd från filsystemet](#uploading-packages-from-your-file-system) eller [hämtad från paketresursen](#downloading-and-installing-packages-from-package-share))

* installerat

>[!CAUTION]
>
>Om du installerar ett paket kan befintligt innehåll skrivas över eller tas bort. Överför bara ett paket om du är säker på att det inte tar bort eller skriver över innehåll som du behöver.
>
>Om du vill se innehållet i ett paket, eller hur det påverkar det, kan du:
>
>* Gör en testinstallation av paketet utan att ändra något av innehållet:
   >  Öppna paketet (klicka på paketikonen eller paketnamnet) och klicka på **Testa installation**.
   >
   >
* Se en lista med paketets innehåll:
   >  Öppna paketet och klicka på **Innehåll**.
>



>[!NOTE]
>
>Omedelbart innan du installerar ditt paket skapas ett ögonblicksbildspaket med det innehåll som ska skrivas över.
>
>Den här ögonblicksbilden installeras om/när du avinstallerar paketet.

>[!CAUTION]
>
>Om du installerar digitala resurser måste du:
>
>* Inaktivera först WorkflowLauncher.
   >  Använd menyalternativet Komponenter i OSGi-konsolen för att inaktivera `com.day.cq.workflow.launcher.impl.WorkflowLauncherImpl`.
   >
   >
* När installationen är klar återaktiverar du WorkflowLauncher.
>
>
Genom att inaktivera WorkflowLauncher säkerställer du att Assets-importimeringsramverket inte (oavsiktligt) manipulerar resurserna vid installationen.

1. Gå till det paket du vill installera i Pakethanteraren.

   En **installationsknapp** visas vid de paket som ännu inte har installerats.

   >[!NOTE]
   >
   >Du kan också öppna paketet genom att klicka på dess ikon för att öppna knappen **Installera** där.

1. Klicka på **Installera** för att starta installationen. En dialogruta begär bekräftelse och visar alla ändringar som görs. Klicka på **Stäng** i dialogrutan när du är klar.

   Ordet **Installerad** visas bredvid paketet när det har installerats.

### Filsystembaserad överföring och installation {#file-system-based-upload-and-installation}

Det finns ett annat sätt att överföra och installera paket till din instans. I filsystemet har du en mapp tillsammans med en burk och en `crx-quicksart` `license.properties` fil. Du måste skapa en mapp med namnet `install` under `crx-quickstart`. Du kommer då att få något sådant: `<aem_home>/crx-quickstart/install`

I den här installationsmappen kan du lägga till dina paket direkt. De laddas automatiskt upp och installeras på din instans. När du är klar kan du se paketen i Package Manager.

Om instansen körs och du lägger till ett paket till `install` mappen startar överföringen direkt och installationen på instansen. Om instansen inte körs installeras paketen som du placerar i `install` mappen i alfabetisk ordning vid start.

>[!NOTE]
>
>Du kan också göra detta innan du ens startar instansen för första gången. Om du vill göra det måste du skapa `crx-quickstart` mappen manuellt, skapa `install` mappen under den och placera paketen där. När du sedan startar instansen första gången installeras paketen i alfabetisk ordning.

### Avinstallerar paket {#uninstalling-packages}

Med AEM kan du avinstallera paket. Den här åtgärden återställer innehållet i databasen som påverkas av ögonblicksbilden som skapades omedelbart före paketinstallationen.

>[!NOTE]
>
>Vid installationen skapas ett ögonblicksbildspaket med det innehåll som ska skrivas över.
>
>Paketet installeras om när du avinstallerar paketet.

1. Gå till det paket som du vill avinstallera i Pakethanteraren.
1. Klicka på paketikonen för det paket som du vill avinstallera.
1. Klicka på **Avinstallera** för att ta bort innehållet i det här paketet från databasen. En dialogruta begär bekräftelse och visar alla ändringar som görs. Klicka på **Stäng** i dialogrutan när du är klar.

### Ta bort paket {#deleting-packages}

Så här tar du bort ett paket från pakethanterarlistan:

>[!NOTE]
>
>De installerade filerna/noderna från paketet tas **inte** bort.

1. Utöka mappen **Packages** i **** verktygskonsolen så att paketet visas i den högra rutan.

1. Klicka på det paket som du vill ta bort så att det är markerat och sedan antingen:

   * Klicka på **Ta bort** i verktygsfältmenyn.
   * Högerklicka och välj **Ta bort**.
   ![paket:ta bort](assets/packagesdelete.png)

1. AEM ber om en bekräftelse på att du vill ta bort paketet. Bekräfta borttagningen genom att klicka på **OK** .

>[!CAUTION]
>
>Om det här paketet redan har installerats tas det *installerade* innehållet **inte** bort.

### Replikerar paket {#replicating-packages}

Replikera innehållet i ett paket för att installera det på publiceringsinstansen:

1. Gå till det paket som du vill replikera i **Pakethanteraren**.

1. Klicka på ikonen eller på namnet på det paket som du vill replikera för att expandera det.
1. Välj **Replikera** i listrutan **Mer** i verktygsfältet.

## Paketresurs {#package-share}

Paketresursen är en centraliserad server som är allmänt tillgänglig för delning av innehållspaket.

Med Paketdelning kan du hämta dessa paket, som kan innehålla officiella snabbkorrigeringar, funktionsuppsättningar, uppdateringar eller exempelinnehåll som genererats av andra användare.

Du kan också överföra och dela paket inom företaget.

### Åtkomst till paketresurs {#access-to-package-share}

Det finns ingen anonym åtkomst till paketresursen. dvs. endast registrerade användare får visa, hämta och överföra paket.

Våra partners och kunder har tillgång till paketresursen. Registreringsinformation måste skickas för att du ska kunna tilldela åtkomsträttigheter.

Så här får du åtkomst till Paketresurs:

* Använda [inloggningssidan](#signing-in-to-package-share)
* Första gången du använder inloggningssidan måste du:

   * [Registrera dig för ett Adobe-ID](#registering-for-package-share) och/eller [validera ditt befintliga Adobe-ID](#validating-your-adobe-id)
   * så att ditt [paketdelningskonto](#package-share-account) kan skapas

>[!NOTE]
>
>Alla användare för paketdelning som inte har tilldelats någon kund måste gå med i en community för att se resurserna genom att klicka på **Gå med** bredvid inloggningen för paketresursen.

#### Logga in på paketresurs {#signing-in-to-package-share}

1. Klicka på **Verktyg** på välkomstskärmen i AEM.
1. Välj sedan **Paketresurs**. Du måste antingen:

   * logga in med ditt Adobe ID
   * [Skapa ett Adobe-ID](#registering-for-package-share)
   >[!NOTE]
   >
   >Första gången du loggar in med ditt Adobe ID måste du slutföra [valideringen av din e-postadress](#validating-your-adobe-id).

   >[!NOTE]
   >
   >Om du har glömt lösenordet kan du använda länken [Hjälpsidor](https://enterprise-dev.adobe.com/content/edev/en/registration/account.html) (även i inloggningsdialogrutan).

#### Validerar ditt Adobe-ID {#validating-your-adobe-id}

Första gången du loggar in på Package Share med ditt Adobe ID valideras din e-postadress.

1. Du får ett e-postmeddelande med en länk.
1. Du måste klicka på den här länken.
1. En webbsida öppnas.

   Åtgärden att öppna den här webbsidan utförs som validering.

1. Inloggningen fortsätter.

1. Du får ett e-postmeddelande med en länk.
1. Du måste klicka på den här länken.
1. En webbsida öppnas. Åtgärden att öppna den här webbsidan utförs som validering.
1. Inloggningen fortsätter.

#### Registrerar för paketresurs {#registering-for-package-share}

Om du behöver ha tillgång till Package Share måste du registrera dig för ett Adobe ID:

* Inloggningssidan [för](#signing-in-to-package-share) paketdelning innehåller en länk för att registrera ett Adobe-ID.
* Du kan registrera dig för ett Adobe ID från vissa Adobe-program.
* Du kan även registrera dig online på [Adobe Sign-sidan](https://www.adobe.com/cfusion/membership/index.cfm?nf=1&nl=1).

Du kan skapa ett Adobe-ID genom att ange:

* din e-postadress
* ett valfritt lösenord
* ytterligare information, t.ex. ditt namn och land där du bor

#### Paketdelningskonto {#package-share-account}

Programmets giltighet kontrolleras före:

* Ditt användarkonto har skapats med nödvändig/tillåten behörighet.
* Ditt konto läggs till i din företagsgrupp.

>[!NOTE]
>
>En användare från ett av våra partnerföretag kan också vara medlem i sina kundgrupper.

#### Nätverksfrågor {#network-considerations}

**IPv6**

Det kan uppstå problem när du försöker få åtkomst till paketresursen från en ren IPv6-miljö.

Detta beror på att paketresursen är en tjänst på en server, vilket innebär att anslutningen görs via olika nätverk på Internet. Det kan inte säkerställas att alla anslutande nätverk stöder IPv6. om inte anslutningen kan misslyckas.

För att undvika det här problemet kan du få åtkomst till paketresursen från ett IPv4-nätverk, hämta paketet och sedan överföra det till IPv6-miljön.

**HTTP-proxy**

Paketresursen är för närvarande inte tillgänglig om ditt företag kör en http-proxy som kräver autentisering.

Paketresursen är bara tillgänglig när din AEM-server har åtkomst till Internet utan att någon autentisering krävs. Om du vill konfigurera proxyn för alla tjänster som använder http-klienten (inklusive paketresursen) använder du [OSGi-konfigurationen för Day Commons HTTP Client 3.1-paketet](/help/sites-deploying/osgi-configuration-settings.md).

### Delning i insida {#inside-package-share}

Paket i paketresurspaket är ordnade i trädunderträd:

* Adobe-paket från Adobe.
* Delade paket som har tillhandahållits av andra företag och har offentliggjorts av Adobe.
* Företagspaket som är privata.

![chlimage_1-110](assets/chlimage_1-110.png)

### Söka och filtrera paket {#searching-and-filtering-packages}

Med Paketdelning kan du söka efter särskilda nyckelord eller/och taggar i ett sökfält. Både nyckelord och taggar har stöd för flera värden.

* Om du vill söka efter flera nyckelord måste du separera varje nyckelord med ett mellanslag.
* Om du vill söka efter flera taggar måste du markera var och en av dem i paketträden.

Du kan också ändra villkorsoperatorn från OR till AND till höger om filtersammanfattningsfältet.

### Hämta och installera paket från paketresurs {#downloading-and-installing-packages-from-package-share}

Om du vill hämta paket från Package Share och installera dem på din lokala instans är det enklare att få åtkomst till Package Share från din AEM-instans. Paketet laddas ned och registreras omedelbart i pakethanteraren där det kan installeras.

1. På AEM-välkomstskärmen klickar du på **Verktyg** och väljer sedan **Paketdelning** för att öppna sidan Paketdelning.
1. Logga in på Paketresurs med din kontoinformation. Landningssidan visas med en lista över Adobe-mappen, den delade mappen och en som är specifik för ditt företag.

   >[!NOTE]
   >
   >Innan du börjar hämta paket från paketresursen måste du se till att du har [nödvändig åtkomst](#access-to-package-share).

1. Navigera till paketet som du vill hämta och klicka på **Hämta**.

1. Gå tillbaka eller navigera till **Package Manager** på din AEM-instans. Navigera sedan till det paket du just laddat ned.

   >[!NOTE]
   >
   >Om du vill hitta det paket du har laddat ned följer du samma sökväg som i Paketresurs. Om du till exempel hämtade ett paket från följande sökväg i paketresursen:
   >
   >**Paket** > **Allmänt** > **Programfixar**
   I Package Manager på den lokala instansen visas paketet också under:
   **Paket** > **Allmänt** > **Programfixar**

1. Klicka på **Installera** för att installera paketet i den lokala AEM-installationen.

   >[!NOTE]
   Om paketet redan har installerats på din instans visas indikatorn för **installerad** bredvid paketet i stället för knappen **Installera** .

   >[!CAUTION]
   Om du installerar ett paket kan befintligt innehåll i databasen skrivas över. Därför rekommenderar vi att du först utför en **testinstallation** . På så sätt kan du kontrollera om innehållet som paketet innehåller står i konflikt med ditt befintliga innehåll.

### Hämtar paket till filsystemet från paketresursen {#downloading-packages-to-your-file-system-from-package-share}

[Det är mycket bekvämt att hämta och installera](#downloading-and-installing-packages-from-package-share) , men om det behövs kan du även hämta paketet och spara det i det lokala filsystemet:

1. Klicka på paketets ikon eller namn i Paketdelning.
1. Klicka på fliken **Resurser** .
1. Klicka på **Hämta till disk**.

### Överföra ett paket {#uploading-a-package}

Med Paketdelning kan du överföra paket till företagets interna del av paketresursen. Detta gör dem tillgängliga för delning inom företaget.

Dessa paket är *inte* tillgängliga för den allmänna AEM-communityn, men är tillgängliga för alla användare som är registrerade hos ditt företag.

Så här överför du paket till företagets interna paketresurs:

>[!CAUTION]
Om du vill överföra ett paket till paketresursen måste du först skapa en gruppmapp som heter efter ditt företag i den lokala pakethanteraren. Till exempel geometrixx. Alla paket som ska överföras för delning måste placeras i den här gruppmappen.
Paket i pakethanterarens hemlista eller i andra mappar kan inte delas.

1. Öppna **pakethanteraren** och navigera till det paket som du vill överföra.

1. Klicka på paketikonen för att öppna den.
1. Klicka på **Dela** för att öppna dialogrutan för att överföra paketet till paketresursen.
1. Om du inte redan är inloggad på Package Share måste du ange dina inloggningsuppgifter.

   När du är inloggad visar AEM information om det paket som ska överföras:

   ![chlimage_1-111](assets/chlimage_1-111.png)

1. Klicka på **Dela** för att överföra paketet till företagets interna paketresurs.

   AEM visar status och anger när paketet har överförts. Sedan kan du klicka på **x** (övre högra hörnet) för att stänga fönstret **Dela paket** .

1. När överföringen är klar kan du navigera till företagets interna mapp och se det paket du just delade.

>[!NOTE]
Om du vill ändra ett paket som är tillgängligt på paketresursen måste du hämta det, återskapa det och sedan överföra det igen till paketresursen.

### Ta bort ett paket {#deleting-a-package}

Du kan bara ta bort paket som du har överfört genom att göra så här:

1. Kontrollera den paketgrupp som innehåller paketet i företagsträdet.
1. Klicka på paketet.
1. Klicka på knappen Ta bort.

   ![chlimage_1-18](do-not-localize/chlimage_1-30.png)

1. Bekräfta att du vill ta bort paketet genom att klicka på **Ta bort** .

### Göra paket halvprivata {#making-packages-semi-private}

Du kan dela paket utanför organisationen, men inte offentligt. Dessa paket betraktas som semiprivata. Om du vill dela dessa halvprivata paket behöver du hjälp från Adobe Support. Du kan göra detta genom att öppna en biljett där Adobe Support begär att ett paket ska vara tillgängligt utanför din organisation. De kommer att be dig om en lista över de Adobe ID:n som du vill ge åtkomst till dina paket.

## Programvarudistribution (beta) {#software-distribution-beta}

[Programvarudistribution](https://downloads.experiencecloud.adobe.com) är det nya användargränssnittet som är utformat för att förenkla sökning och hämtning av AEM-paket. Den är för närvarande i betaversion och är endast tillgänglig för Adobe Managed Services och AEM som kunder av molntjänster samt för Adobes anställda.

>[!NOTE]
* [Paketresursen](#package-share) är kvar tills alla kunder har tillgång till programvarudistribution.
* Alla paket är tillgängliga från både Paketresurs och Programvarudistribution.


>[!CAUTION]
AEM-pakethanteraren kan för tillfället inte användas med programvarudistribution. Du hämtar dina paket till den lokala hårddisken.

