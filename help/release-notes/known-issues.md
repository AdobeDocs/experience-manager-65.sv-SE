---
title: Kända fel
description: Versionsinformation om kända fel i Adobe Experience Manager 6.3
uuid: 8fbdb167-833a-4179-aad1-0a26a4e5b3a7
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5
discoiquuid: d11fc727-f23a-4cde-9fa6-97e2c81b4ad0
docset: aem65
translation-type: tm+mt
source-git-commit: 0ae42d9f81df89a7e1c08fac5cce5240f14e8c60

---


# Kända fel {#known-issues}

På den här sidan finns en lista över kända fel i Adobe Experience Manager 6.5 som släpptes i april 2019.

[Kontakta supporten](https://helpx.adobe.com/support/experience-manager.html) om du behöver mer information om kända fel.

## Platform {#platform}

Ett problem rapporteras där CRX-Quickstart och dess innehåll tas bort.

Kontrollera att egenskapen &quot;*htmllibmanager.fileSystemOutputCacheLocation*&quot; aldrig är en tom sträng för var och en av dessa åtgärder:

1. Anropar&quot;*/libs/granite/ui/content/dumplibs.rebuild.html?invalidate=true*&quot;.
2. Uppgraderar till AEM 6.5.
3. Kör&quot;migrering av lat innehåll&quot; på AEM 6.5.

Det finns en [kunskapsbasartikel](https://helpx.adobe.com/experience-manager/kb/avoid-crx-quickstart-deletion-in-aem-6-5.html) med mer information och en lösning på problemet.

## Assets {#assets}

* **Sök:** Sökningen ger inga resultat om söksträngen innehåller inledande blanksteg ([OAK-4786](https://issues.apache.org/jira/browse/OAK-4786))
* **Mappmetadataschema**: När du har lagt till en alternativknapp återges ID- och Value-fältet inte som förväntat och borttagningsfunktionen fungerar inte. (CQ-4261144)
* När du byter namn på en resurs går det inte att använda ett tomt utrymme i resursnamnet. (CQ-4266403)

## Formulär {#forms}

* När AEM Forms är installerat i Linux fungerar inte den digitala signaturen med maskinvarusäkerhetsmodulen. (CQ-4266721)
* (Endast AEM Forms på WebSphere) Alternativet **Formulärarbetsflöde **> **Uppgiftssökning** returnerar inget resultat om du söker efter en **administratör** med **användarnamn** som sökvillkor. (CQ-4266457)

* AEM Forms kan inte konvertera tif- och tiff-filer med JPEG-komprimering till PDF-dokument. (CQ-4265972)
* Alternativen **AEM Forms Assets Scanner** och **Letter to Interactive Communication Migration** fungerar inte på sidan **AEM Forms Migration** . (CQ-4266572)

* (Endast JBoss 7) När du uppgraderar från en tidigare version till AEM 6.5 Forms och den tidigare versionen hade processer (.lca) som skapade och använde en kopia av standardåtergivningsprocessen, misslyckas HTML5 Forms som använder sådana processer (.lca) att utföra de åtgärder som krävs. (CQ-4243928)
* När en formulärdatamodelltjänst anropas från regelredigeraren för att dynamiskt uppdatera värden för bildvalskomponenten, uppdateras inte värdena för bildvalskomponenten i en adaptiv varifrån. (CQ-4254754)
* Installationsprogrammet för AEM Forms Designer kräver 32-bitarsversionen av omdistribuerbara [Visual C++-miljöpaket 2012](https://support.microsoft.com/en-in/help/2977003/the-latest-supported-visual-c-downloads) och omdistribuerbara [Visual C++-miljöpaket 2013](https://support.microsoft.com/en-in/help/3179560/update-for-visual-c-2013-and-visual-c-redistributable-package). Kontrollera att ovannämnda omdistribuerbara körtidspaket är installerade innan du startar installationen. (CQ-4265668)

* När ett adaptivt formulär har konfigurerats för att dynamiskt uppdatera värden för en komponent och den publiceringsinstans som är värd för formuläret nås via dispatchern, slutar funktionen att dynamiskt uppdatera värden för ett fält att fungera. Du löser problemet genom att öppna CRXDE på publiceringsinstansen, navigera till /libs/fd/af/runtime/clientlibs/guideChartReducer och skapa egenskapen som listas nedan.

   * Namn: allowProxy
   * Typ: Boolean
   * Värde: true
   * Skyddad: Falskt
   * Obligatoriskt: Falskt
   * Flera: Falskt
   * Automatiskt skapad: Fas

Egenskapen gör att klientbiblioteken under körningsmappen kan komma åt proxy. (CQ-4268679)

