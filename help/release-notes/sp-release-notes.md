---
title: '[!DNL Experience Manager] 6.5 Versionsinformation för Service Pack'
description: Versionsinformation som är specifik för  [!DNL Adobe Experience Manager] 6.5 Service Pack 8
docset: aem65
mini-toc-levels: 1
translation-type: tm+mt
source-git-commit: fb1423b7ae110b8a3cf8e0e389394e9266157a9f
workflow-type: tm+mt
source-wordcount: '3295'
ht-degree: 0%

---


# [!DNL Adobe Experience Manager] 6.5 Versionsinformation för Service Pack  {#aem-service-pack-release-notes}

## Versionsinformation {#release-information}

| Produkter | [!DNL Adobe Experience Manager] 6.5 |
| -------- | ---------------------------- |
| Version | 6.5.8.0 |
| Typ | Service Pack-version |
| Date | 11 mars 2021 |
| Hämta URL | [Programvarudistribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.8.zip) |

<!-- TBD: Update the SD link when SP8 is available. Same link is duplicated below in install -->

## Vad ingår i [!DNL Adobe Experience Manager] 6.5.8.0 {#what-s-included-in-aem}

[!DNL Adobe Experience Manager] 6.5.8.0 innehåller nya funktioner, viktiga förbättringar som kunderna efterfrågat samt prestanda-, stabilitets- och säkerhetsförbättringar som släppts sedan 6.5-versionen släpptes i april 2019. Service Pack är installerat på [!DNL Adobe Experience Manager] 6.5.

De viktigaste funktionerna och förbättringarna i [!DNL Adobe Experience Manager] 6.5.8.0 är:

<!-- TBD:
* Using the Connected Assets functionality, it is now possible to connect up to 3 [!DNL Sites] instances with 1 [!DNL Assets] instances. The configuration user interface now allows the administrators to provide the details of these [!DNL Sites] instances. -->

* När du använder [funktionen Anslutna resurser](/help/assets/use-assets-across-connected-assets-instances.md) kan du nu visa en lista över alla [!DNL Sites] sidor som använder resursen. Dessa referenser till en resurs är tillgängliga på en resurses [!UICONTROL Properties]-sida. På så sätt kan administratörer, marknadsförare och bibliotekarier få en komplett bild av medieanvändningen, vilket ger bättre spårning, hantering och enhetlighet för varumärken.

* När du tar bort en resurs som refereras på en webbsida visas en varning i [!DNL Experience Manager] [](/help/assets/use-assets-across-connected-assets-instances.md#asset-usage-references). Du kan framtvinga borttagning av en refererad resurs eller kontrollera och ändra referenserna som visas på sidan [!DNL Properties] för resursen. När du klickar på referenserna öppnas de lokala sidorna och fjärrsidorna [!DNL Sites].

* Sortera de Live Copy-sidor som är tillgängliga för utrullning med hjälp av egenskaperna [!UICONTROL Name], [!UICONTROL Last modified date,] och [!UICONTROL Last rollout date].

* Den inbyggda databasen (Apache Jackrabbit Oak) uppdateras till 1.22.6. <!-- TBD: Mention the version -->

En fullständig lista över funktioner och förbättringar som introducerats i [!DNL Experience Manager] 6.5.8.0 finns i [vad som är nytt i [!DNL Adobe Experience Manager] 6.5 Service Pack 8](new-features-latest-service-pack.md).

Nedan följer en lista över korrigeringar i [!DNL Experience Manager] 6.5.8.0-versionen.

### [!DNL Sites] {#sites-6580}

* När en sida flyttas till utkast uppdateras inte länkarnas mål (NPR-35724).
* Tizen-baserad spelare kan inte autentiseras i vissa webbläsare. Problemet inträffar med webbläsare som inte har stöd för attributet sameSite=none (NPR-35589).
* En olåst responsiv behållare visar inte tillåtna komponenter (NPR-35565).
* När du skapar en live-kopia av en nyligen tillagd sida skapar överordnad två kopior för varje domän (NPR-35545).
* Deadlock i registret över SCR-komponenter när många trådar blockeras på grund av `org.apache.felix.scr.impl.ComponentRegistry`-timern. Därför slutar [!DNL Experience Manager] svara på obestämd tid (GRANITE-33125,FELIX-6252).
* När du söker efter en viss resurs i sidofältet innehåller resultatet vissa resurser som inte sökts (NPR-35524).
* När du aktiverar SSL för en Experience Manager-instans tas kontextsökvägen bort (NPR-35477).
* När du skapar en lista lägger till text som det första elementet, lägger till en tabell som det andra elementet och lägger till en lista inuti tabellen, förvrängs den överordnade listan (NPR-35465).
* När du använder olika plugin-program för efterföljande listobjekt läggs en extra <br>-tagg till i listobjekten (NPR-35464).
* När en lista placeras mellan två stycken kan du inte lägga till en tabell i listan (NPR-35356).
* När du startar en uppgradering av en AEM instans från AEM 6.3 till AEM 6.5 tar det längre tid att starta uppgraderingsinstansen (NPR-35323).
* När du replikerar en AEM som innehåller en hakparentes (). i namnet misslyckas replikeringen (GRANITE-27004, NPR-35315).
* När du lägger till rubriker i en textredigerare inaktiveras styckeknappen (NPR-35256).
* När du lägger till ett objekt i en befintlig lista tas efterföljande komprimeringsbar lista eller växlingslista bort (NPR-35206).
* När alternativet Utrullningssida är markerat visas en dialogruta med alla tillgängliga live-kopior och automatisk utrullning sker. De publicerade kopiorna av sidorna distribueras till alla platser utan användaråtgärd (NPR-35138).
* När du använder alternativet Inkludera underordnade visas inte alla sidor med alternativet Hantera publikation. Endast 22 sidor listas (NPR-35086).
* När en profil redigeras behåller textkomponenten inte policyändringarna (NPR-35070).
* När du drar in vissa objekt i en numrerad lista behåller alla objekt samma nummer, men numreringen ska börja från 1 för objekt med samma indrag (CQ-4313011).
* När miniatyrbilder är aktiverade kan du inte redigera någon sida eller komponent. Problemet uppstod efter installation av AEM 6.5 Service Pack 7 (CQ-431133).
* Omni sök- och resursfilter returnerar irrelevanta eller inga resultat (CQ-4312322, NPR-35793).
* När flera sidor samtidigt kommer åt ett klientbibliotek, kan HTML-bibliotekshanteraren inte läsa in klientbiblioteket. Det leder till felaktig återgivning av sidor (NPR-35538).
* Kontextsökvägen tas bort automatiskt när du ställer in en SSL i [!DNL Experience Manager] (NPR-35294).
* Pakethanteraren loggar inte ut användare efter att ha klickat på alternativet Logout (NPR-35160).

### [!DNL Assets] {#assets-6580}

[!DNL Adobe Experience Manager] 6.5.8.0  [!DNL Assets] åtgärdar följande och ger följande förbättringar.

* När en tidigare version av en resurs återställs aktiveras inte händelsen DamEvent.Type RESTORED i OSGi-konsolen (NPR-35789).
* `IndexWriter.merge` orsakar  `OutOfMemoryError` fel eftersom funktionen för smart taggning skapar stora  `/oak:index/lucene` och  `/oak:index/ntBaseLucene` indexerade värden (NPR-35651).
* Ett felmeddelande visas när du försöker spara en [!UICONTROL Asset Contribution]-typmapp med multibytetecken i namnet (NPR-35605).
* När överlappande metadataundertypsfält används inträffar ett felaktigt &#39;Fyll i det här fältet&#39;-fel (NPR-35643).
* När en befintlig resurs dras i [!DNL Assets]-användargränssnittet och en ny version skapas, är ändringarna i metadata inte beständiga (NPR-34940).
* När du skapar regler i metadatarammet för en överlappande meny upprepas samma namn med alternativet [!UICONTROL Dependant On] (NPR-35596).
* Likhetssökning fungerar inte efter redigering av [!UICONTROL Assets Admin Search Rail] (NPR-35588).
* Om du öppnar resurssökning i den vänstra listen genom att klicka på [!UICONTROL Filter] i en mapp fungerar inte filtret i [!UICONTROL Status] > [!UICONTROL Checkout] > [!UICONTROL Checked out] (NPR-35530).
* Om du försöker ta bort alla smarta taggar för en resurs och spara ändringarna tas de inte bort. Användargränssnittet anger dock att ändringarna sparas (NPR-35519).
* Användare kan inte ordna om eller sortera resurser i listvyn i en ordningsbar mapp (NPR-35516).
* Om du redigerar standardmetadataschemat ändras taggfältet i resursens [!UICONTROL Properties]-sida till ett textfält. Ändringen gör att okända användare kan lägga till taggar på begäran och taggarna lagras som en sträng i databasen (NPR-35478).
* Om du anger ett namn som inte har en giltig e-postadress när du hämtar en resurs är nedladdningsalternativet inte tillgängligt. Om ett annat alternativ i hämtningsdialogrutan väljs aktiveras knappen, men inget e-postmeddelande skickas (NPR-35365).
* Användare kan inte checka in resurser efter att ha redigerat dem i [!DNL Adobe InDesign] och få felmeddelanden om bristande behörigheter (NPR-35341).
* Hanteringsfält JavaScript-biblioteket uppgraderas till v4.7.6 (NPR-35333).
* Gränssnittet för metadataredigeraren slutar fungera som förväntat när du startar från redigering av massmetadata och avmarkerar objekt tills ett enda objekt förblir markerat (NPR-35144).
* Global navigering öppnar inte rätt konsol när användaren klickar på den på sidan `assets.html` (CQ-4312311).
* [!DNL Assets] RGB-återgivning visas inte för en resurs som har RGB-återgivning (CQ-4310190).
* Alternativet [!UICONTROL Relate] på menyn visas inte korrekt på sidan [!UICONTROL Properties] (CQ-4310188).
* Om filtypsfilter för dokument används för att söka efter resurser och skapa en smart samling används inte filtret när samlingen används. I stället visas alla typer av resurser i sökningen (NPR-35759).
* Du kan inte dra och lägga till resurser i en ljuslåda från användargränssnittet [!DNL Assets] (NPR-35901).
* När en ny version av en befintlig resurs skapas efter att namnkonflikten har lösts, skrivs metadata för den ursprungliga resursen över (CQ-4313594).
* När du filtrerar resurssökningen med ett sökfilter eller predikat, öppnar en resurs för att visa eller redigera den och går tillbaka till sökresultatsidan fungerar inte filtret. Alla sökda resurser listas ofiltrerade (NPR-35913).

#### [!DNL Dynamic Media] {#dynamic-media-6580}

* Alternativet URL för RESS-bildförinställning är aktiverat på sidan med resursinformation. Nu är både URL- och RESS-alternativen tillgängliga på sidan med resursinformation när RESS-bildförinställningen har valts i avsnittet med dynamiska återgivningar. (CQ-4311241)
* Interaktiv mediakomponent - interaktiv video fungerar inte om användaren har [!DNL Experience Manager] med selektiv publiceringskonfiguration (CQ-4311054).
* Om du flyttar resurser mellan mappar är synkroniseringen mellan [!DNL Experience Manager] och [!DNL Dynamic Media–Scene7] via API mycket långsam (CQ-4310001).
* När Omnisearch används ökar loggarnas storlek avsevärt (CQ-4309153).
* När selektiv synkronisering är aktiverat och en resurs kopieras (inte flyttas) till en synkroniseringsmapp synkroniseras den inte som förväntat (CQ-4307122).
* För överförda resurser som automatiskt publiceras till DM visas inte statusen Publicerad på AEM. Dessutom visas inte rätt publiceringsstatus i statuskolumnen för Dynamic Media Publish (CQ-4306415).
* Om en resurs publiceras på [!DNL Experience Manager] och är inställd på att publiceras på [!DNL Dynamic Media] vid aktivering uppdateras inte metadatavärdet för `scene7FileStatus` som förväntat (CQ-4308269).
* När du redigerar videoprofilen visar [!DNL Experience Manager] inte de höjd- och bithastighetsvärden som angetts för videoförinställningen. Fälten visas tomma (CQ-4311828).

### [!DNL Commerce] {#commerce-6580}

* Det går inte att skapa en anpassad tagg för alla produkter i Commerce (CQ-4310682).

* Referensuppdatering av produktresurs gör att replikeringstrådar är i vänteläge tills ProductAssetListener-tråden slutför sina implementeringar av JCR (NPR-35269).

### Plattform {#platform-6580}

* När du använder en Coral Tab View-komponent utan flikar och sedan utlöser en Foundation-validerare inträffar följande fel (NPR-35636):

   ```TXT
    Uncaught TypeError: Cannot set property 'invalid' of undefined
     at enable (foundation.js:10703)
     at foundation.js:10710
   ```

* SCD-framåtreplikering misslyckas för Delete-händelser för noder som innehåller kommatecken i namnet (NPR-35191).

* När du har uppgraderat till AEM 6.5.7 misslyckas byggnaderna. Orsaken är att en gammal version eller ingen jackson-core är inbäddad i uber-jar (GRANITE-33006).

### Användargränssnitt {#ui-6580}

* När du växlar från kortvyn till listvyn för dokument i en mapp i resurskonsolen fungerar inte sorteringen korrekt (NPR-35842).

* När du hyperlänkar text i en textkomponent visas inte rätt resultat i sökfunktionen (NPR-35849).

* När ett värde inte anges för ett dolt fält som är markerat som obligatoriskt, blockerar det dig från att spara en komponent (NPR-35219).

### Integreringar {#integrations-6580}

* När du använder olika värden för IMS-klient-ID och målklientkod kan [!DNL Experience Manager] inte integreras med [!DNL Adobe Target] (NPR-35342).

### Översättningsprojekt {#translation-6580}

* Problem vid export eller import av ett översättningsjobb i [!DNL Experience Manager] (NPR-35259).

### Kampanj {#campaign-6580}

* När du skapar en kampanjsida med hjälp av en färdig mall i Touch-gränssnittet och öppnar fliken E-post i dialogrutan för sidegenskaper, är personaliseringsvariabeln för ämnes- och brödfälten fortfarande inaktiverad (CQ-4312388).

### [!DNL Communities] {#communities-6580}

* När du lägger till en sidstruktur i en community-grupp ändras rubriken [!UICONTROL Group] i den synliga sökvägen till titeln för den första [!UICONTROL Page] (NPR-35803).
* Till skillnad från moderatorer kan en standardmedlem i communityn inte komma åt och redigera utkast (NPR-35339).
* Åtkomstkontroll och denial of service med DSRPReindexServlet, som minskar communitywebbplatsen tills indexeringen är klar (NPR-35591).
* Om du tar bort [!UICONTROL All Users] från fältet [!UICONTROL Administrators] tas de inte bort från serverdelen (NPR-35592, NPR-35611).
* Komponenten [!UICONTROL Compose Message] returnerar inget resultat när den angivna texten är en partiell matchning (NPR-35666).

### [!DNL Brand Portal] {#brandportal-6580}

* Om du lägger till en medlem i en [!UICONTROL Asset Contribution]-typmapp visas [!UICONTROL Add User or Group]-beskrivningen i användargränssnittet, men bara aktiva Brand Portal-användare stöds och inte grupper (NPR-35332).

### [!DNL Forms] {#forms-6580}

>[!NOTE]
>
>[!DNL Experience Manager Forms] släpper tilläggspaketen en vecka efter det schemalagda datumet för  [!DNL Experience Manager] Service Pack.

**Adaptiv Forms**

* När du infogar en tabell med en repeterbar rad på en repeterbar panel som har flera instanser i en adaptiv form, läggs tabellen alltid till i den första instansen av panelen (NPR-35635).

* När tabbfokus når CAPTCHA-komponenten igen efter att ha verifierat den en gång i en adaptiv form, visar [!DNL Experience Manager Forms] felmeddelandet `Provide Captcha phrase to proceed` (NPR-35539).

**Interaktiv kommunikation**

* När du skickar in ett översatt formulär visas inskickningsmeddelandena på engelska och översätts inte till rätt språk (NPR-35808).

* När du inkluderar ett dolt villkor i bifogade XDP-dokument eller dokumentfragment, läses inte den interaktiva kommunikationen in (NPR-35745).

**Korrespondenshantering**

* När du redigerar ett brev tar det längre tid att läsa in moduler med villkor (NPR-35325).

* När du väljer en resurs i den vänstra navigeringsrutan som inte ingår i en bokstav och sedan väljer nästa resurs, tas inte den blå markeringen bort från den tidigare valda resursen (NPR-35851).

* När du redigerar textfält i en bokstav visar [!DNL Experience Manager Forms] felmeddelandet `Text Edit Failed` (CQ-4313770).

**Arbetsflöde**

* När du försöker öppna ett anpassat formulär i ett [!DNL Experience Manager Forms]-mobilprogram för iOS slutar programmet svara (CQ-4314825).

* Fliken [!UICONTROL To-do] på arbetsytan HTML visar HTML-tecken (NPR-35298).

**XMLFM**

* När du genererar ett XML-dokument med hjälp av utdatatjänsten inträffar felet `OutputServiceException` för vissa XML-filer (CQ-4311341, CQ-4313893).

* När du använder upphöjd egenskap på det första tecknet i en punkt blir punktstorleken mindre (CQ-4306476).

* PDF forms som genereras med Output Service innehåller inga kantlinjer (CQ-4312564).

**Designer**

* När du öppnar en XDP-fil i [!DNL Experience Manager Forms] Designer skapas filen designer.log i samma mapp som XDP-filen (CQ-4309427, CQ-4310865).

**HTML5 Forms**

* När du markerar en kryssruta i ett adaptivt formulär i webbläsaren [!DNL Safari] för [!DNL iOS 14.1 or 14.2] visas inte ytterligare fält (NPR-35652).

**Forms Management**

* Inget bekräftelsemeddelande som indikerar slutförd massöverföring av XDP-filer till CRX-databasen (NPR-35546).

**Dokumentsäkerhet**

* Flera problem har rapporterats för alternativet [!UICONTROL Edit Policy] i AdminUI (NPR-35747).

Mer information om säkerhetsuppdateringar finns på [Experience Manager-säkerhetsbulletinsidan](https://helpx.adobe.com/security/products/experience-manager.html).

## Installera 6.5.8.0 {#install}

**Installationskrav och mer information**

* Experience Manager 6.5.8.0 kräver Experience Manager 6.5. Mer information finns i [uppgraderingsdokumentationen](/help/sites-deploying/upgrade.md).
* Service Pack-nedladdningen finns på Adobe [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html).
* Installera Experience Manager 6.5.8.0 på en av Author-instanserna med hjälp av Package Manager på en distribution med MongoDB och flera instanser.

>[!NOTE]
>
>Adobe rekommenderar inte att du tar bort eller avinstallerar paketet [!DNL Adobe Experience Manager] 6.5.8.0.

### Installera Service Pack {#install-service-pack}

Så här installerar du Service Pack på en [!DNL Adobe Experience Manager] 6.5-instans:

1. Starta om instansen innan installationen om instansen är i uppdateringsläge (och så är fallet när instansen uppdaterades från en tidigare version). Adobe rekommenderar också en omstart om den aktuella upptiden för en instans är hög.

1. Ta en ögonblicksbild eller en ny säkerhetskopia av din [!DNL Experience Manager]-instans innan du installerar.

1. Hämta Service Pack från [Programvarudistribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.8.zip).

1. Öppna Pakethanteraren och klicka på **[!UICONTROL Upload Package]** för att överföra paketet. Mer information finns i [Pakethanteraren](/help/sites-administering/package-manager.md).

1. Markera paketet och klicka på **[!UICONTROL Install]**.

1. Om du vill uppdatera S3-anslutningen stoppar du instansen efter installationen av Service Pack, byter ut den befintliga kopplingen mot en ny binär fil som finns i installationsmappen och startar om instansen. Se [Amazon S3-datalager](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector).

>[!NOTE]
>
>Dialogrutan för pakethanterarens gränssnitt avslutas ibland när Service Pack installeras. Adobe rekommenderar att du väntar på att felloggarna ska stabiliseras innan du får åtkomst till distributionen. Vänta på de specifika loggarna för avinstallationen av uppdateringspaketet innan du försäkrar dig om att installationen lyckas. Vanligtvis inträffar detta på [!DNL Safari], men kan inträffa i alla webbläsare.

**Automatisk installation**

Det finns två sätt att installera Adobe Experience Manager 6.5.8.0 automatiskt på en fungerande instans:

S. Placera paketet i mappen `../crx-quickstart/install` när servern är tillgänglig online. Paketet installeras automatiskt.

B. Använd [HTTP-API:t från Package Manager](/help/sites-administering/package-manager.md#package-share). Använd `cmd=install&recursive=true` så att kapslade paket installeras.

>[!NOTE]
>
>Adobe Experience Manager 6.5.8.0 stöder inte installation av Bootstrap.

**Validera installation**

1. Produktinformationssidan (`/system/console/productinfo`) visar den uppdaterade versionssträngen `Adobe Experience Manager (6.5.8.0)` under [!UICONTROL Installed Products].

1. Alla OSGi-paket är antingen **[!UICONTROL ACTIVE]** eller **[!UICONTROL FRAGMENT]** i OSGi Console (Använd webbkonsol: `/system/console/bundles`).

1. OSGi-paketet `org.apache.jackrabbit.oak-core` är version 1.2.3 eller senare (Använd webbkonsol: `/system/console/bundles`).

Information om vilka plattformar som är certifierade för att fungera med den här versionen finns i [tekniska krav](/help/sites-deploying/technical-requirements.md).

### Installera Adobe Experience Manager Forms tilläggspaket {#install-aem-forms-add-on-package}

>[!NOTE]
>
>Hoppa över om du inte använder Experience Manager Forms. Korrigeringar i Experience Manager Forms levereras via ett separat tilläggspaket en vecka efter den schemalagda versionen av [!DNL Experience Manager] Service Pack.

1. Kontrollera att du har installerat Adobe Experience Manager Service Pack.
1. Ladda ned motsvarande tilläggspaket från Forms som finns på [AEM Forms releases](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html) för ditt operativsystem.
1. Installera Forms tilläggspaket enligt beskrivningen i [Installera AEM Forms tilläggspaket](../forms/using/installing-configuring-aem-forms-osgi.md#install-aem-forms-add-on-package).

>[!NOTE]
>
>AEM 6.5.8.0 innehåller en ny version av [AEM Forms-kompatibilitetspaket](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=en#aem-65-forms-releases). Om du använder en äldre version av AEM Forms Compatibility Package och uppdaterar till AEM 6.5.8.0 installerar du den senaste versionen av paketet efter installationen av Forms Add-On Package.

### Installera Adobe Experience Manager Forms på JEE {#install-aem-forms-jee-installer}

>[!NOTE]
>
>Hoppa över om du inte använder AEM Forms på JEE. Korrigeringar i Adobe Experience Manager Forms på JEE levereras via ett separat installationsprogram.

Information om hur du installerar det kumulativa installationsprogrammet för Experience Manager Forms på JEE och konfigurationen efter distributionen finns i [versionsinformationen](jee-patch-installer-65.md).

>[!NOTE]
>
>När du har installerat det kumulativa installationsprogrammet för Experience Manager Forms på JEE installerar du det senaste Forms-tilläggspaketet, tar bort Forms-tilläggspaketet från mappen `crx-repository\install` och startar om servern.

### UberJar {#uber-jar}

UberJar för Experience Manager 6.5.8.0 finns i [Maven Central-databasen](https://repo.maven.apache.org/maven2/com/adobe/aem/uber-jar/6.5.8/).

Om du vill använda UberJar i ett Maven-projekt läser du [hur du använder UberJar](/help/sites-developing/ht-projects-maven.md) och inkluderar följande beroende i projektstrukturen:

```shell
<dependency>
     <groupId>com.adobe.aem</groupId>
     <artifactId>uber-jar</artifactId>
     <version>6.5.8</version>
     <scope>provided</scope>
</dependency>
```

>[!NOTE]
>
>UberJar och andra relaterade artefakter finns tillgängliga i Maven Central Repository i stället för i Adobe Public Maven-databasen (`repo.adobe.com`). Huvudfilen för UberJar har bytt namn till `uber-jar-<version>.jar`. Det finns alltså inget `classifier`, med `apis` som värde, för taggen `dependency`.

## Inaktuella funktioner {#removed-deprecated-features}

Nedan finns en lista över funktioner som är markerade som borttagna med [!DNL Experience Manager] 6.5.7.0. Funktioner markeras som borttagna från början och senare i en framtida version. Ett alternativt alternativ brukar anges.

Granska om du använder en funktion eller en funktion i en distribution. Planera också att ändra implementeringen så att ett alternativt alternativ används.

| Yta | Funktion | Ersättning |
|---|---|---|
| Integreringar | Skärmen **[!UICONTROL AEM Cloud Services Opt-In]** är föråldrad. Tack vare integreringen mellan Experience Manager och Adobe Target som uppdaterades i Experience Manager 6.5 för att stödja Adobe Target Standard API, som använder autentisering via Adobe IMS och I/O, och den växande rollen hos Adobe Launch för att instrumentera Experience Manager sidor för analys och personalisering, har guiden för att välja In blivit funktionellt irrelevant. | Konfigurera systemanslutningar, Adobe IMS-autentisering och [!DNL Adobe I/O]-integreringar via respektive Experience Manager molntjänster. |
| Anslutningar | Adobe JCR Connector för Microsoft SharePoint 2010 och Microsoft SharePoint 2013 är föråldrad för Experience Manager 6.5. | Ej tillämpligt |

## Kända fel {#known-issues}

* Om du uppgraderar din [!DNL Experience Manager]-instans från version 6.5 till version 6.5.8.0 kan du visa `RRD4JReporter`-undantag i `error.log`-filen. Starta om instansen för att lösa problemet.

* Om du installerar [!DNL Experience Manager] 6.5 Service Pack 5 eller ett tidigare Service Pack på [!DNL Experience Manager] 6.5 tas körtidskopian av din resurskräddarsydda arbetsflödesmodell (skapad i `/var/workflow/models/dam`) bort.
Om du vill hämta körtidskopian rekommenderar Adobe att du synkroniserar designtidskopian av den anpassade arbetsflödesmodellen med körtidskopian med hjälp av HTTP API:
   `<designModelPath>/jcr:content.generate.json`.

* Kontakta Adobe kundtjänst om du stöter på problem när du redigerar och skapar överlappande regler i [!UICONTROL Folder Metadata Schema Forms Editor] och [!UICONTROL Metadata Schema Forms Editor] med hjälp av dialogrutan [!UICONTROL Define Rule]. Reglerna som redan har skapats och sparats fungerar som förväntat.

* Om en mapp i hierarkin byter namn i [!DNL Experience Manager Assets] och den kapslade mappen som innehåller en resurs publiceras i [!DNL Brand Portal], uppdateras inte mappens namn i [!DNL Brand Portal] förrän rotmappen publiceras igen.

* När en användare väljer att konfigurera ett fält för första gången i ett adaptivt formulär visas inte alternativet att spara en konfiguration i egenskapsläsaren. Om du väljer att konfigurera ett annat fält i det adaptiva formuläret i samma redigerare åtgärdas problemet.

* Om [!UICONTROL Connected assets configuration]-guiden returnerar ett 404-felmeddelande efter installationen måste du installera om paketen `cq-remotedam-client-ui-content` och `cq-remotedam-client-ui-components` manuellt med hjälp av pakethanteraren.

* Följande fel och varningsmeddelanden kan visas under installationen av Experience Manager 6.5.x.x:
   * &quot;När Adobe Target-integreringen har konfigurerats i Experience Manager med Target Standard API (IMS-autentisering) skapas felaktiga erbjudandetyper när Experience Fragments exporteras till Target. I stället för att skriva&quot;Experience Fragment&quot;/källa&quot;Adobe Experience Manager&quot; skapar Target flera erbjudanden med typen&quot;HTML&quot;/källa&quot;Adobe Target Classic&quot;.
   * `com.adobe.granite.maintenance.impl.TaskScheduler`: Inga underhållsfönster hittades vid granit/drift/underhåll.
   * Validering på serversidan av adaptiva formulär misslyckas när sammanställningsfunktioner som SUM, MAX och MIN används (CQ-4274424).
   * `com.adobe.granite.maintenance.impl.TaskScheduler` - Inga underhållsfönster hittades vid granit/drift/underhåll.
   * Aktiveringspunkten i en interaktiv Dynamic Media-bild syns inte när du förhandsvisar mediefilen via Shoppable Banner Viewer.
   * `com.adobe.cq.social.cq-social-jcr-provider bundle com.adobe.cq.social.cq-social-jcr-provider:1.3.5 (395)[com.adobe.cq.social.provider.jcr.impl.SpiSocialJcrResourceProviderImpl(2302)]` : Tidsgränsen överskreds i väntan på att reg.ändringen skulle slutföras utan registrering.

## OSGi-paket och innehållspaket som ingår {#osgi-bundles-and-content-packages-included}

Följande textdokument listar de OSGi-paket och innehållspaket som ingår i [!DNL Experience Manager] 6.5.8.0:

* [Förteckning över OSGi-paket som ingår i Experience Manager 6.5.8.0](assets/6580_bundles.txt)

* [Förteckning över innehållspaket som ingår i Experience Manager 6.5.8.0](assets/6580_packages.txt)

## Begränsade webbplatser {#restricted-sites}

Dessa webbplatser är bara tillgängliga för kunder. Om du är kund och behöver åtkomst kontaktar du din kontoansvarige på Adobe.

* [Nedladdning av produkt på licensing.adobe.com](https://licensing.adobe.com/)
* Se [hur du kontaktar Adobe kundtjänst](https://experienceleague.adobe.com/docs/customer-one/using/home.html).

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] 6.5 Versionsinformation](/help/release-notes/release-notes.md)
>* [[!DNL Experience Manager] produktsida](https://www.adobe.com/marketing/experience-manager.html)
>* [[!DNL Experience Manager] 6.5-dokumentation](https://experienceleague.adobe.com/docs/experience-manager-65.html)
>* [Prenumerera på produktuppdateringar med Adobe prioritet](https://www.adobe.com/subscription/priority-product-update.html)

