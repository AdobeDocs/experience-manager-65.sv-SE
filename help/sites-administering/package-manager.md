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
source-git-commit: 03967fcdc9685c9a8bf1dead4bd5e389603ff91b
workflow-type: tm+mt
source-wordcount: '3934'
ht-degree: 0%

---


# Arbeta med paket{#how-to-work-with-packages}

Med paket kan du importera och exportera databasinnehåll. Du kan till exempel använda paket för att installera nya funktioner, överföra innehåll mellan instanser och säkerhetskopiera databasinnehåll.

Paket kan öppnas och/eller underhållas från följande sidor:

* [Package Manager](#package-manager), som du använder för att hantera paketen i den lokala AEM instansen.

* [Programvarudistribution](#software-distribution), en centraliserad server som innehåller både offentligt tillgängliga paket och de som är privata för ditt företag. De publika paketen kan innehålla snabbkorrigeringar, nya funktioner, dokumentation m.m.

Du kan överföra paket mellan Package Manager, Software Distribution och ditt filsystem.

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
* Hämta paket från AEM till filsystemet
* Överför paket från filsystemet till den lokala AEM
* Validera paketinnehåll före installation
* Utför en torr installation
* Installera paket (AEM installerar inte paket automatiskt efter överföring)
* Ta bort paket
* Hämta paket, till exempel snabbkorrigeringar, från biblioteket för programvarudistribution
* Överför paket till den företagsinterna sektionen i biblioteket för programvarudistribution

## Paketinformation {#package-information}

En paketdefinition består av olika typer av information:

* [Paketinställningar](#package-settings)
* [Paketfilter](#package-filters)
* [Paketskärmbilder](#package-screenshots)
* [Paketikoner](#package-icons)

### Paketinställningar {#package-settings}

Du kan redigera olika paketinställningar för att definiera aspekter som paketbeskrivning, relaterade fel, beroenden och providerinformation.

Dialogrutan **Paketinställningar** är tillgänglig via knappen **Redigera** när [du skapar](#creating-a-new-package) eller [redigerar](#viewing-and-editing-package-information) ett paket och innehåller tre flikar för konfiguration. När du har gjort några ändringar klickar du på **OK** för att spara dessa.

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
    </ul> <p>Standardvärdet är <strong>Ignorera</strong>.</p> </td>
   <td>
    <ul>
     <li><strong>Ignorera</strong>  - bevara åtkomstkontrollistor i databasen</li>
     <li><strong>Skriv över</strong>  - skriv över ACL:er i databasen</li>
     <li><strong>Sammanfoga</strong>  - sammanfoga båda uppsättningarna med åtkomstkontrollistor</li>
     <li><strong>Tydliga</strong>  - klara ACL:er</li>
     <li><strong>MergePreserve</strong> - merge-åtkomstkontroll i innehållet med den som ingår i paketet genom att lägga till åtkomstkontrollposter för objekt som inte finns i innehållet</li>
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

* **Rotsökväg** för innehållet som ska inkluderas.
* **Regler** som inkluderar eller exkluderar specifika noder under rotsökvägen.

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
     <li><strong>ta </strong> inte med andra filer eller mappar från den angivna rotsökvägen</li>
    </ul> </td>
   <td>/libs/sling/install(/.*)? </td>
  </tr>
  <tr>
   <td> exclude</td>
   <td>Du kan ange en sökväg eller använda ett reguljärt uttryck för att ange alla noder som du vill utesluta.<br /> <br /> Om du utesluter en katalog utesluts katalogen  <i></i> och alla filer och mappar i den katalogen (dvs. hela underträdet).<br /> </td>
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

AEM eller tilläggspaket:

Officiella funktionspaket:

![](do-not-localize/chlimage_1-29.png)

## Pakethanteraren {#package-manager}

Pakethanteraren hanterar paketen i din lokala AEM. När du har [tilldelat de nödvändiga behörigheterna](#permissions-needed-for-using-the-package-manager) kan du använda pakethanteraren för olika åtgärder, bland annat för att konfigurera, bygga, hämta och installera dina paket. Nyckelelementen som ska konfigureras är:

* [Paketinställningar](#package-settings)
* [Paketfilter](#package-filters)

### Behörigheter som krävs för att använda pakethanteraren {#permissions-needed-for-using-the-package-manager}

Om du vill ge användarna rätt att skapa, ändra, överföra och installera paket måste du ge dem rätt behörighet på följande platser:

* **/etc/packages** (fullständig behörighet exklusive radering)
* noden som innehåller paketets innehåll

Mer information om hur du ändrar behörigheter finns i [Ange behörigheter](/help/sites-administering/security.md#setting-page-permissions).

### Skapa ett nytt paket {#creating-a-new-package}

Så här skapar du en ny paketdefinition:

1. På välkomstskärmen klickar du på **Paket** (eller från **Verktyg**-konsolen dubbelklickar på **Paket**).

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
   Klicka på **OK** för att skapa paketet.

1. AEM listar det nya paketet i lämplig gruppmapp.

   ![packagesitem](assets/packagesitem.png)

   Klicka på ikonen eller paketnamnet som du vill öppna.

   ![packagesiklickad](assets/packagesitemclicked.png)

   >[!NOTE]
   >
   >Du kan vid behov gå tillbaka till den här sidan senare.

1. Klicka på **Redigera** om du vill redigera [paketinställningarna](#package-settings).

   Här kan du lägga till information och/eller definiera vissa inställningar. dessa innehåller till exempel en beskrivning, ikonen [](#package-icons), relaterade fel och lägger till providerinformation.

   Klicka på **OK** när du är klar med redigeringen av inställningarna.

1. Lägg till **[skärmbilder](#package-screenshots)** i paketet efter behov. En instans är tillgänglig när paketet skapas. Lägg till fler om det behövs med **Package Screenshot** från sidespark.

   Lägg till den faktiska bilden genom att dubbelklicka på bildkomponenten i området **Skärmbilder**, lägga till en bild och klicka på **OK**.

1. Definiera **[paketfiltren](#package-filters)** genom att dra instanser av **filterdefinitionen** från sidosparken och sedan dubbelklicka för att öppna den för redigering:

   ![paketerfilter](assets/packagesfilter.png)

   Ange:

   * **Rotsökväg:**
Innehållet som ska paketeras. kan vara roten i ett underträd.
   * **Regler**
är valfria. för enkla paketdefinitioner är det inte nödvändigt att ange inkluderings- eller exkluderingsregler.

      Om det behövs kan du definiera antingen [**Inkludera** eller **Uteslut**-regler](#package-filters) för att definiera paketets innehåll exakt.

      Lägg till regler med symbolen **+**, eller ta bort regler med symbolen **-**. Regler tillämpas efter deras ordning så att de kan positionera dem efter behov med knapparna **Upp** och **Ned**.
   Klicka sedan på **OK** för att spara filtret.

   >[!NOTE]
   >
   >Du kan använda så många filterdefinitioner du behöver, men du måste se till att de inte hamnar i konflikt. Använd **Förhandsgranska** för att bekräfta vad paketinnehållet ska vara.

1. Du kan använda **Förhandsgranska** för att bekräfta vad paketet innehåller. Detta utför en torr körning av byggprocessen och visar allt som kommer att läggas till i paketet när det byggs.
1. Du kan nu [bygga](#building-a-package) ditt paket.

   >[!NOTE]
   >
   >Det är inte obligatoriskt att bygga paketet just nu, det kan göras vid en senare tidpunkt.

### Bygga ett paket {#building-a-package}

Ett paket skapas ofta samtidigt som du [skapar paketdefinitionen](#creating-a-new-package), men du kan gå tillbaka vid ett senare tillfälle för att antingen skapa eller återskapa paketet. Detta kan vara användbart om innehållet i databasen har ändrats.

>[!NOTE]
>
>Innan du skapar paketet kan det vara användbart att förhandsgranska innehållet i paketet. Klicka på **Förhandsgranska**.

1. Öppna paketdefinitionen från **Pakethanteraren** (klicka på paketikonen eller namnet).

1. Klicka på **Build**. En dialogruta där du uppmanas bekräfta att du vill skapa paketet.

   >[!NOTE]
   >
   >Detta är särskilt viktigt när du återskapar ett paket eftersom paketinnehållet skrivs över.

1. Klicka på **OK**. AEM skapar paketet med allt innehåll som läggs till i paketet. När AEM är klar visas en bekräftelse på att paketet har skapats och (när du stänger dialogrutan) information om paketlistan uppdateras.

### Rewrapping a package {#rewrapping-a-package}

När ett paket har byggts kan det vid behov rewrappas.

När du omsluter paketet ändras paketinformationen - *utan att* paketinnehållet ändras. Paketinformationen är miniatyrbilden, beskrivningen osv., med andra ord allt du kan redigera med dialogrutan **Paketinställningar** (för att öppna den här klickningen **Redigera**).

Ett viktigt användningsområde för ombrytning är när du förbereder ett paket. Du kan till exempel ha ett befintligt paket och bestämma dig för att dela det med andra. För det vill du lägga till en miniatyrbild och lägga till en beskrivning. I stället för att återskapa hela paketet med alla dess funktioner (vilket kan ta en stund och innebär att paketet inte längre är identiskt med originalpaketet) kan du kapsla in det och bara lägga till miniatyrbilden och beskrivningen.

1. Öppna paketdefinitionen från **Pakethanteraren** (klicka på paketikonen eller namnet).

1. Klicka på **Redigera** och uppdatera **[paketinställningarna](#package-settings)** efter behov. Klicka på **OK** för att spara.

1. Klicka på **Radbryt** så uppmanas du bekräfta åtgärden i en dialogruta.

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

1. Om paketet redan har byggts klickar du på **Innehåll** så öppnas ett fönster och hela innehållet i paketet visas:

### Visa paketinnehåll och testinstallation {#viewing-package-contents-and-testing-installation}

När ett paket har skapats kan du visa innehållet:

1. Gå till det paket du vill visa i Pakethanteraren.
1. Klicka på paketikonen för det paket som du vill visa. Detta öppnar paketsidan med information om paketdefinitionen.

1. Om du vill visa innehållet klickar du på **Innehåll** i ett fönster öppnas och hela innehållet i paketet visas:

   ![packningar](assets/packgescontents.png)

1. Om du vill utföra en torr installation klickar du på **Testa installation**. När du har bekräftat åtgärden öppnas ett fönster där resultatet visas som om installationen utfördes:

   ![paketestestinstallera](assets/packagestestinstall.png)

### Hämtar paket till ditt filsystem {#downloading-packages-to-your-file-system}

I det här avsnittet beskrivs hur du hämtar ett paket från AEM till filsystemet med **Package Manager**.

1. Klicka på **Paket** på AEM välkomstskärm och välj sedan **Pakethanteraren**.
1. Navigera till paketet som du vill hämta.

   ![paketerladda ned](assets/packagesdownload.png)

1. Klicka på länken som utgörs av zip-filens namn (understruken) för paketet som du vill hämta; till exempel `export-for-offline.zip`.

   AEM hämtar paketet till datorn (med en standarddialogruta för hämtning av webbläsare).

### Överför paket från filsystemet {#uploading-packages-from-your-file-system}

Med en paketöverföring kan du överföra ett paket från filsystemet till AEM Package Manager.
Så här överför du ett paket:

1. Navigera till **Pakethanteraren**. Till den gruppmapp som du vill att paketet ska överföras till.

   ![paketerupload, knapp](assets/packagesuploadbutton.png)

1. Klicka på **Överför paket**.

   ![paketeruploaddialog](assets/packagesuploaddialog.png)

   * **Arkiv**

      Du kan antingen skriva filnamnet direkt eller använda **Bläddra..Dialogrutan** där du kan välja önskat paket från det lokala filsystemet (efter markeringen klickar du på **OK**).

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

   Den här valideringen undersöker paketet för alla JAR-filer (OSGi-paket), extraherar deras `manifest.xml` (som innehåller de versionshanteringsberoenden som OSGi-paketet är beroende av) och verifierar den AEM instansen exporterar dessa beroenden med rätt versioner.

   **Hur det rapporteras**

   Versionsberoende som inte kan uppfyllas av den AEM instansen visas i **aktivitetsloggen** i pakethanteraren.

   **Fellägen**

   Om beroenden inte uppfylls startar inte OSGi-paketen med dessa beroenden. Detta resulterar i en trasig programdistribution eftersom allt som förlitar sig på det OSGi-paket som inte startats i sin tur inte fungerar som det ska.

   **Felupplösning**

   För att åtgärda fel på grund av att OSGi-paketen inte är nöjd måste beroendeversionen i paketet med otillfredsställande importer justeras.

* **Validera övertäckningar**

   **Vad är markerat**

   Valideringen avgör om det paket som installeras innehåller en fil som redan finns i AEM.

   Med en befintlig övertäckning på `/apps/sling/servlet/errorhandler/404.jsp`, till exempel ett paket som innehåller `/libs/sling/servlet/errorhandler/404.jsp`, så att den ändrar den befintliga filen på `/libs/sling/servlet/errorhandler/404.jsp`.

   **Hur det rapporteras**

   Alla sådana övertäckningar beskrivs i **aktivitetsloggen** i pakethanteraren.

   **Fellägen**

   Ett feltillstånd innebär att paketet försöker distribuera en fil som redan är överlagrad, vilket innebär att ändringarna i paketet åsidosätts (och därmed&quot;döljs&quot;) av övertäckningen och inte börjar gälla.

   **Felupplösning**

   För att lösa det här problemet måste den som ansvarar för att uppdatera övertäckningsfilen i `/apps` granska ändringarna i den övertäckda filen i `/libs` och införliva ändringarna som behövs i övertäckningen ( `/apps`) samt distribuera om den övertäckda filen.

   >[!NOTE]
   >
   >Observera att valideringsfunktionen inte kan stämma av om det överlagda innehållet har integrerats korrekt i överläggsfilen. Valideringen fortsätter därför att rapportera om konflikter även efter att nödvändiga ändringar har gjorts.

* **Validera åtkomstkontrollistor**

   **Vad är markerat**

   Valideringen kontrollerar vilka behörigheter som läggs till, hur de hanteras (sammanfoga/ersätt) och om de aktuella behörigheterna påverkas.

   **Hur det rapporteras**

   Behörigheterna beskrivs i **aktivitetsloggen** i Pakethanteraren.

   **Fellägen**

   Inga explicita fel kan anges. Valideringen anger bara om nya ACL-behörigheter kommer att läggas till eller påverkas av att paketet installeras.

   **Felupplösning**

   Med hjälp av den information som valideringen ger kan de påverkade noderna granskas i CRXDE och åtkomstkontrollistorna kan justeras i paketet efter behov.

   >[!CAUTION]
   >
   >Som god praxis rekommenderas att paket inte påverkar AEM-tillhandahållna åtkomstkontrollistor eftersom detta kan leda till oväntade produktbeteenden.

#### Utför validering {#performing-validation}

Paketvalidering kan göras på två olika sätt:

* Via pakethanterarens gränssnitt
* Via HTTP-POST-begäran, till exempel med cURL

>[!NOTE]
>
>Validering ska alltid ske efter att paketet har överförts, men innan det installeras.

**Paketvalidering via Pakethanteraren**

1. Öppna pakethanteraren på `https://<server>:<port>/crx/packmgr`
1. Markera paketet i listan och välj sedan **Mer** i listrutan och **Validera** i listrutan.

   >[!NOTE]
   >
   >Detta bör göras efter att du har överfört innehållspaketet, men innan du installerar paketet.

1. I den modala dialogrutan som sedan visas använder du kryssrutorna för att välja valideringstyp(er) och börja valideringen genom att klicka på **Validera**. Du kan även klicka på **Avbryt**.

1. De valda valideringarna körs sedan. Resultaten visas i aktivitetsloggen för Package Manager.

**Paketvalidering via HTTP-POST-begäran**

Begäran om POST har följande format.

```
https://<host>:<port>/crx/packmgr/service.jsp?cmd=validate&type=osgiPackageImports,overlays,acls
```

>[!NOTE]
>
>Parametern `type` kan vara en kommaavgränsad, osorterad lista som består av:
>
>* `osgiPackageImports`
>* `overlays`
>* `acls`

>
>
Värdet `type` är som standard `osgiPackageImports` om det inte skickas.

Följande är ett exempel på hur du använder cURL för att köra en paketvalidering.

1. Om du använder cURL kör du en programsats som liknar följande:

   ```shell
   curl -v -X POST --user admin:admin -F file=@/Users/SomeGuy/Desktop/core.wcm.components.all-1.1.0.zip 'http://localhost:4502/crx/packmgr/service.jsp?cmd=validate&type=osgiPackageImports,overlays,acls'
   ```

1. Den begärda valideringen körs och svaret skickas tillbaka som ett JSON-objekt.

>[!NOTE]
>
>Svaret på en begäran om validering av HTTP-POST blir ett JSON-objekt med valideringsresultatet.

### Installerar paket {#installing-packages}

När du har överfört ett paket måste du installera innehållet. Om paketinnehållet ska vara installerat och fungera måste det vara både:

* laddat till AEM (antingen [överfört från ditt filsystem](#uploading-packages-from-your-file-system) eller hämtat från [Programdistribution](#software-distribution))

* installerat

>[!CAUTION]
>
>Om du installerar ett paket kan befintligt innehåll skrivas över eller tas bort. Överför bara ett paket om du är säker på att det inte tar bort eller skriver över innehåll som du behöver.
>
>Om du vill se innehållet i ett paket, eller hur det påverkar det, kan du:
>
>* Gör en testinstallation av paketet utan att ändra något av innehållet:
   >  Öppna paketet (klicka på paketikonen eller paketnamnet) och klicka på **Testa installationen**.
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

   En **Install**-knapp visas på sidan om paket som ännu inte har installerats.

   >[!NOTE]
   >
   >Du kan också öppna paketet genom att klicka på dess ikon för att komma åt knappen **Installera** där.

1. Klicka på **Installera** för att starta installationen. En dialogruta begär bekräftelse och visar alla ändringar som görs. När du är klar klickar du på **Stäng** i dialogrutan.

   Ordet **Installerad** visas bredvid paketet efter att det har installerats.

### Filsystembaserad överföring och installation {#file-system-based-upload-and-installation}

Det finns ett annat sätt att överföra och installera paket till din instans. I filsystemet har du en `crx-quicksart`-mapp tillsammans med din jar- och `license.properties`-fil. Du måste skapa en mapp med namnet `install` under `crx-quickstart`. Du kommer då att få något sådant: `<aem_home>/crx-quickstart/install`

I den här installationsmappen kan du lägga till dina paket direkt. De laddas automatiskt upp och installeras på din instans. När du är klar kan du se paketen i Package Manager.

Om instansen körs och du lägger till ett paket i mappen `install` startar överföringen och installationen direkt på instansen. Om din instans inte körs installeras paketen som du placerar i mappen `install` vid start i alfabetisk ordning.

>[!NOTE]
>
>Du kan också göra detta innan du ens startar instansen för första gången. Om du vill göra det måste du skapa mappen `crx-quickstart` manuellt, skapa mappen `install` under den och placera paketen där. När du sedan startar instansen första gången installeras paketen i alfabetisk ordning.

### Avinstallerar paket {#uninstalling-packages}

AEM kan du avinstallera paket. Den här åtgärden återställer innehållet i databasen som påverkas av ögonblicksbilden som skapades omedelbart före paketinstallationen.

>[!NOTE]
>
>Vid installationen skapas ett ögonblicksbildspaket med det innehåll som ska skrivas över.
>
>Paketet installeras om när du avinstallerar paketet.

1. Gå till det paket som du vill avinstallera i Pakethanteraren.
1. Klicka på paketikonen för det paket som du vill avinstallera.
1. Klicka på **Avinstallera** om du vill ta bort innehållet i det här paketet från databasen. En dialogruta begär bekräftelse och visar alla ändringar som görs. När du är klar klickar du på **Stäng** i dialogrutan.

### Tar bort paket {#deleting-packages}

Så här tar du bort ett paket från pakethanterarlistan:

>[!NOTE]
>
>De installerade filerna/noderna från paketet är **inte** borttagna.

1. Utöka mappen **Paket** i konsolen **Verktyg** så att paketet visas i den högra rutan.

1. Klicka på det paket som du vill ta bort så att det är markerat och sedan antingen:

   * Klicka på **Ta bort** i verktygsfältmenyn.
   * Högerklicka och välj **Ta bort**.

   ![paket:ta bort](assets/packagesdelete.png)

1. AEM ber om en bekräftelse på att du vill ta bort paketet. Klicka på **OK** för att bekräfta borttagningen.

>[!CAUTION]
>
>Om det här paketet redan har installerats tas det *installerade* innehållet **inte** bort.

### Replikerar paket {#replicating-packages}

Replikera innehållet i ett paket för att installera det på publiceringsinstansen:

1. I **Pakethanteraren** navigerar du till det paket som du vill replikera.

1. Klicka på ikonen eller på namnet på det paket som du vill replikera för att expandera det.
1. I listrutan **Mer** i verktygsfältet väljer du **Replikera**.

## Paketdelning {#package-share}

Paketresursen var en centraliserad server som är allmänt tillgänglig för delning av innehållspaket.

Den har ersatts av [Programvarudistribution](#software-distribution).

## Programdistribution {#software-distribution}

[Software ](https://downloads.experiencecloud.adobe.com) Distribution är det nya användargränssnittet som förenklar sökning och hämtning av AEM.

Mer information finns i [Software Distribution documentation](https://experienceleague.adobe.com/docs/experience-cloud/software-distribution/home.html).

>[!CAUTION]
>
>AEM pakethanteraren kan för tillfället inte användas med programvarudistribution, du hämtar dina paket till den lokala hårddisken.

