---
title: Kända fel
description: Versionsinformation om kända fel i Adobe Experience Manager 6.5
exl-id: 736037cf-af8c-4ce2-969e-c100a939a038
source-git-commit: d87e48070329518117f84252ea0cab0471d74a29
workflow-type: tm+mt
source-wordcount: '661'
ht-degree: 0%

---

# Kända fel {#known-issues}

På den här sidan finns en lista med kända fel från Adobe Experience Manager 6.5 som släpptes i april 2019.

[Kontakta support](https://helpx.adobe.com/support/experience-manager.html) om du behöver mer information om kända fel.

## Plattform {#platform}

* Ett problem rapporteras där CRX-Quickstart och dess innehåll tas bort.

   Kontrollera att egenskapen `htmllibmanager.fileSystemOutputCacheLocation` är inte en tom sträng:

   1. Anropar `/libs/granite/ui/content/dumplibs.rebuild.html?invalidate=true`.
   2. Uppgraderar till AEM 6.5.
   3. Kör migrering av&quot;lat innehåll&quot; på AEM 6.5.

   A [Knowledge Base](https://helpx.adobe.com/experience-manager/kb/avoid-crx-quickstart-deletion-in-aem-6-5.html) det finns mer information och en lösning på problemet i artikeln.

* Om du använder JDK 11 med AEM 6.5-instansen kan vissa sidor visas som tomma efter distributionen av vissa paket. Följande felmeddelande visas i loggfilen:

   ```java
   *ERROR* [OsgiInstallerImpl] org.apache.sling.scripting.sightly bundle org.apache.sling.scripting.sightly:1.1.2.1_4_0 (558)[org.apache.sling.scripting.sightly.impl.engine.extension.use.JavaUseProvider(3345)] : Error during instantiation of the implementation object (java.lang.NoClassDefFoundError: jdk/internal/reflect/ConstructorAccessorImpl)
   java.lang.NoClassDefFoundError: jdk/internal/reflect/ConstructorAccessorImpl
   ```

Så här löser du felet:

1. Stoppa AEM. Gå till `<aem_server_path_on_server>crx-quickstart\conf` och öppna `sling.properties` -fil. Adobe rekommenderar att du säkerhetskopierar den här filen.

1. Sök efter `org.osgi.framework.bootdelegation=`. Lägg till `jdk.internal.reflect,jdk.internal.reflect.*` egenskaper för att visa resultatet som.

```java
org.osgi.framework.bootdelegation=sun.*,com.sun.*,jdk.internal.reflect,jdk.internal.reflect.*
```

1. Spara filen och starta om AEM.

## Sites {#sites}

* **Arbeta med sidversioner**: Om en sida har flyttats kan du inte längre förhandsgranska versioner som gjorts före flyttningen.

## Assets {#assets}

* **Sök:** Sökningen ger inga resultat om söksträngen innehåller inledande blanksteg ([OAK-4786](https://issues.apache.org/jira/browse/OAK-4786))
* **Metadataschema för mapp**: När du har lagt till en alternativknapp återges ID- och Value-fältet inte som förväntat och borttagningsfunktionen fungerar inte. (CQ-4261144)
* När du byter namn på en resurs går det inte att använda ett tomt utrymme i resursnamnet. (CQ-4266403)

## Forms {#forms}

* När AEM Forms är installerat i Linux fungerar inte den digitala signaturen med maskinvarusäkerhetsmodulen. (CQ-4266721)
* (Endast AEM Forms på WebSphere) **Forms Workflow** > **Uppgiftssökning** alternativet returnerar inget resultat om du söker efter **Administratör** med **Användarnamn** som sökvillkor. (CQ-4266457)

* AEM Forms kan inte konvertera TIF- och TIFF-filer med JPEG-komprimering till PDF-dokument. (CQ-4265972)
* The **AEM Forms Assets Scanner** och **Letter to Interactive Communication Migration** alternativ fungerar inte på **AEM Forms Migration** sida. (CQ-4266572)

* (Endast JBoss 7) När du uppgraderar från en tidigare version till AEM 6.5 Forms och den tidigare versionen hade processer (.lca) som skapade och använde en kopia av standardåtergivningsprocessen eller standardåtergivningsprocessen, kan HTML5 Forms som använder sådana processer (.lca) inte utföra de åtgärder som krävs. (CQ-4243928)
* När en formulärdatamodelltjänst anropas från regelredigeraren för att dynamiskt uppdatera värden för bildvalskomponenten, uppdateras inte värdena för bildvalskomponenten i en adaptiv varifrån. (CQ-4254754)
* AEM Forms Designer-installationsprogrammet kräver 32-bitarsversionen av [Visual C++ redistributable runtime package 2012](https://support.microsoft.com/en-in/help/2977003/the-latest-supported-visual-c-downloads) och [Omdistribuerbara Visual C++-körtidspaket 2013](https://support.microsoft.com/en-in/help/3179560/update-for-visual-c-2013-and-visual-c-redistributable-package). Kontrollera att ovannämnda omdistribuerbara körtidspaket är installerade innan du startar installationen. (CQ-4265668)

* PDF Generator stöder inte autentisering med smartkort.  När en administratör aktiverar grupprincipen `Interactive Logon: Require Smart card` på en Windows-server blir alla användare av PDF Generator ogiltiga.

* När ett adaptivt formulär har konfigurerats för att dynamiskt uppdatera värden för en komponent och den publiceringsinstans som är värd för formuläret nås via dispatchern, slutar funktionen att dynamiskt uppdatera värden för ett fält att fungera. Du löser problemet genom att öppna CRXDE på publiceringsinstansen och navigera till `/libs/fd/af/runtime/clientlibs/guideChartReducer`och skapa den egenskap som anges nedan.

   * Namn: allowProxy
   * Typ: Boolean
   * Värde: true
   * Skyddad: Falskt
   * Obligatoriskt: Falskt
   * Flera: Falskt
   * Automatiskt skapad: Falskt

   Egenskapen gör att klientbiblioteken under körningsmappen kan komma åt proxies. (CQ-4268679)

* När AEM Forms startas `SAX Security Manager could not be setup` visas.
* När du öppnar ett PDF som är skyddat med AEM Forms Document Security på en Apple iOS eller iPadOS som kör Adobe Acrobat Reader version 20.10.00.
* När du skickar ett formulär som innehåller ett standardfält för överföring av HTML från en Apple iOS-enhet skickas ibland inte filens innehåll och en 0-byte-fil tas emot i den andra änden. Apple iOS 15.1 åtgärdar problemet.
