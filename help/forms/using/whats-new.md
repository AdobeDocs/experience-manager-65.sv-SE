---
title: Sammanfattning av nya funktioner| AEM 6.5-formulär
seo-title: Sammanfattning av nya funktioner| AEM 6.5-formulär
description: De senaste funktionerna och förbättringarna i formulär och dokument i världens mest avancerade lösning för hantering av digitala upplevelser.
seo-description: De senaste funktionerna och förbättringarna i formulär och dokument i världens mest avancerade lösning för hantering av digitala upplevelser.
uuid: 179d372d-b7f6-4771-8349-fc6b7854efac
topic-tags: introduction
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 0e949429-cd5f-4301-aa72-14803cdfab00
docset: aem65
translation-type: tm+mt
source-git-commit: eb6ecc224c4fdd8c1af6f7800dc30de419f5ef68

---


# Sammanfattning av nya funktioner| AEM 6.5-formulär{#new-features-summary-aem-forms}

## Transaktionsrapporter {#transaction-reports}

Med transaktionsrapporter kan du samla in och spåra antalet skickade formulär, bearbetade dokument och återgivna dokument. Målet med att spåra dessa transaktioner är att fatta ett välgrundat beslut om produktanvändningen och att balansera investeringar i maskinvara och programvara. Några exempel på transaktioner är:

* Skicka in ett adaptivt formulär, ett HTML5-formulär eller en formuläruppsättning
* Återgivning av en utskrift eller webbversion av en interaktiv kommunikation
* Konvertering av ett dokument från ett filformat till ett annat

Mer information om hur du konfigurerar och använder transaktionsrapporter finns i Översikt över [transaktionsrapporter](../../forms/using/transaction-reports-overview.md).

![En exempeltransaktionsrapport](assets/surface_transaction_reporting.png)

## Interaktiv kommunikation {#interactive-communications}

**Definiera visningsmönster för data**

Utvecklare av interaktiv kommunikation kan nu definiera [datavisningsmönster](../../forms/using/create-interactive-communication.md#main-pars-header-1162517146) för fält, variabler och formulärdatamodellelement. Till exempel datum-, valuta- eller telefonformat.

**Använd nya diagramtyper**

Nu kan du lägga till [kvadrantdiagram med flera serier](../../forms/using/chart-component-interactive-communications.md) i Interactive Communications.

**Sortera kolumner i en tabell**

Nu kan du [sortera kolumner i en tabell](../../forms/using/create-interactive-communication.md#sortcolumns) i den interaktiva kommunikationen. Du kan binda och sortera tabellkolumner med statisk text eller datamodellsobjekt.

**Använda nya komponenter i en webbkanal**

Nu kan du lägga till komponenterna Button och Separator i webbkanalen. Mer information finns i [Lägg till Button-komponent i webbkanalen](../../forms/using/create-interactive-communication.md#add-button-component-to-the-web-channel) och [avgränsarkomponenten i webbkanalen](../../forms/using/create-interactive-communication.md#separatorcomponent).

**Layoutläge för att ändra storlek på komponenter**

Nu kan du växla till [layoutläget](../../forms/using/resize-using-layout-mode.md) för att ändra storlek på komponenter i webbkanalen med ett WYSIWYG-gränssnitt.

**Förbättringar av användbarheten**

De som skapar interaktiv kommunikation kan nu använda olika lättanvända funktioner samtidigt som de skapar korrespondenser. Listan över åtgärder omfattar:

* [Utför ångra-gör-om-åtgärder i utskrifts- och webbkanaler](../../forms/using/create-interactive-communication.md#undoredoactions)
* [Lägga till variabler i ett dokumentfragment med symbolen @](../../forms/using/texts-interactive-communications.md#searchvariables)
* [Lägga till datamodellelement i ett dokumentfragment med symbolen @](../../forms/using/texts-interactive-communications.md#searchdatamodelproperties)
* [Ta bort eller lägga till en webbkanal i en befintlig interaktiv kommunikation](../../forms/using/create-interactive-communication.md#edit-interactive-communication-properties)
* [Binda datakällelement med fält och variabler med dra-och-släpp-åtgärder](../../forms/using/create-interactive-communication.md#binddatasourceelements)
* [Markera obundna fält och variabler när du skapar interaktiv kommunikation](../../forms/using/create-interactive-communication.md#distinguishunboundfields)
* [Utför ytterligare åtgärder som kopiera, gruppera eller annat på ärvda komponenter i en webbkanal](../../forms/using/create-interactive-communication.md#componenttoolbar)

**Förbättringar i synkroniseringsprocessen**

Det finns flera förbättringar i den automatiska webbkanalslayouten med hjälp av kanalen Skriv ut.

![Interactive Communications Charts](assets/interactive-communication-charts.png)

## Adaptiva former {#adaptive-forms}

### Använd Adobe Signs molnbaserade digitala signaturer i adaptiva formulär {#use-adobe-sign-s-cloud-based-digital-signatures-in-adaptive-forms}

[Molnbaserade digitala signaturer](https://helpx.adobe.com/sign/kb/digital-certificate-providers.html) eller fjärrsignaturer är en ny generation digitala signaturer som fungerar på både dator, mobil och webben - och som uppfyller de högsta efterlevnads- och säkerhetsnivåerna för autentisering av signerare. Nu kan du [signera ett adaptivt formulär](../../forms/using/working-with-adobe-sign.md) med molnbaserade digitala signaturer.

#### Bädda in ett adaptivt formulär eller interaktiv kommunikation i AEM Sites Single Page Applications {#embed-an-adaptive-form-or-interactive-communcation-in-aem-sites-single-page-applications}

Med AEM Forms kan du [sömlöst bädda in ett adaptivt formulär](../../forms/using/embed-adaptive-form-aem-sites-spa.md) eller interaktiv kommunikation i en AEM Sites single page application (SPA). Det inbäddade adaptiva formuläret och den interaktiva kommunikationen fungerar fullt ut och användarna kan fylla i och skicka formuläret utan att behöva lämna sidan. Det hjälper användaren att hålla sig i rätt kontext för andra element på webbsidan och interagera samtidigt med det adaptiva formuläret eller den interaktiva kommunikationen.

#### Sortera kolumner i tabeller med adaptiva formulär {#sort-columns-of-adaptive-form-tables}

Du kan [sortera valfri kolumn i en tabell](../../forms/using/adaptive-forms-tables.md#sortcolumnstable) med adaptiva formulär i stigande eller fallande ordning. Du kan använda sortering på tabellkolumner med statisk text, datamodellsobjektegenskaper eller en kombination av statiska text- och datamodellsobjektsegenskaper.

#### Begränsa tillgängligheten för adaptiva formulärmallar till specifika sökvägar {#restrict-the-availability-of-adaptive-forms-templates-to-specific-paths}

Anpassade formulär har lagt till stöd för egenskapen cq:allowedPaths. Egenskapen [begränsar tillgängligheten för adaptiva formulärmallar till specifika sökvägar](../../forms/using/creating-adaptive-form.md#main-pars-text).

#### Lägg till kryssrutor i det adaptiva formuläret dynamiskt {#add-check-boxes-to-the-adaptive-form-dynamically}

Nu kan du definiera regler för att [lägga till kryssrutor i det adaptiva formuläret dynamiskt](../../forms/using/rule-editor.md#setpropertyrule) baserat på en anpassad funktion, ett formulärobjekt eller en objektegenskap.

## AEM-arbetsflöden {#aem-workflows}

### Använda variabler i AEM-arbetsflöden {#use-variables-in-aem-workflows}

Variabler möjliggör arbetsflödessteg för att lagra och skicka metadata mellan arbetsflödessteg vid körning. Du kan skapa olika typer av variabler för att lagra olika typer av data. Exempel: heltal, strängar, dokument eller instanser av formulärdatamodell. Vanligtvis använder du en variabel eller en samling variabler när du behöver fatta ett beslut baserat på det värde som den innehåller eller lagra information som du behöver senare i en process.

Variabler är ett tillägg till [MetaDataMap](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/metadata/MetaDataMap.html) -gränssnittet som finns i den tidigare versionen. Det sparar tid när det gäller att utveckla anpassad ECMAScript-kod som används för att hämta och uppdatera metadatavärden. Du fortsätter att använda MetaDataMap-gränssnittet och ECMAScript-koden för att hantera metadata. Några fördelar med att använda variabler framför MetaDataMap och ECMAScript är:

* Dynamisk lagring, uppdatering och användning av värden som lagras i en variabel i hela arbetsflödet utan att vara beroende av anpassad kod
* Hämta och uppdatera värden direkt till en formulärdatamodell och en datafil (XML/JSON) för ett skickat formulär
* Lagra kompletta dokument i en variabel för dokumentbearbetning

Steget Gå till, eller Dela, och alla arbetsflödessteg i AEM Forms stöder variabler. Du kan använda MetaDataMap-gränssnittet för att komma åt variabler i arbetsflödessteg som inte har inbyggt stöd för variabler. Mer information finns i [Variabler i AEM-arbetsflöden](../../forms/using/variable-in-aem-workflows.md).

![Ställa in en variabel i ett arbetsflöde](assets/variable.png)

#### Använda ett arbetsflöde med olika adaptiva formulär {#use-a-workflow-with-different-adaptive-forms}

Du kan [ange ett adaptivt formulär för tilldelningsuppgiften](../../forms/using/aem-forms-workflow-step-reference.md#assign-task-step) och dokumentet för poststeget i formulärcentrerade arbetsflöden under körningen. Det gör att ett arbetsflöde kan fungera med olika adaptiva formulär. Du kan bestämma vilken metod som ska användas för att välja ett anpassat formulär när du utformar arbetsflödet. Det adaptiva formuläret kan placeras på en absolut sökväg, skickas som nyttolast till arbetsflödet eller vara tillgängligt på en sökväg som beräknas med hjälp av en variabel.

#### Använd de förbättrade loggningsfunktionerna i formulärbaserade arbetsflödessteg {#use-enhanced-logging-capabilities-of-forms-centric-workflow-steps}

Loggningsfunktionerna i blankettbaserade arbetsflöden är standardiserade. Nu kan alla formulärbaserade arbetsflödessteg producera loggar som är lika standardiserade. Det hjälper till att förbättra felsökningshastigheten.

## Dataintegrering {#data-integration}

Nu kan du:

* [Validera indata](../../forms/using/work-with-form-data-model.md#automated-validation-of-input-data) baserat på en lista med begränsningar. Det säkerställer att bara giltiga data skickas till datakällan.
* [Åsidosätt standardslutpunkten](../../forms/using/configure-data-sources.md#configure-soap-web-services) som definieras i en WSDL-fil (Web Services Description Language).

* [Åsidosätt standardschema](../../forms/using/configure-data-sources.md#configure-restful-web-services) , [värd och bassökväg](../../forms/using/configure-data-sources.md#configure-restful-web-services) som definierats i Swagger-definitionsfilen.

## Plattforms- och säkerhetsuppdateringar {#platform-and-security-updates}

### Viktiga plattformsuppdateringar {#major-platform-updates}

AEM Forms kan konfigureras med valfri kombination av operativsystem, programservrar, databaser, databasdrivrutiner, JDK, LDAP-servrar och e-postservrar som stöds. Nedan följer de största förändringarna för plattformar som [stöds](../../forms/using/aem-forms-jee-supported-platforms.md):

<table>
 <tbody>
  <tr>
   <td>Komponent</td>
   <td>Stöd borttaget</td>
  </tr>
  <tr>
   <td>Operativsystem</td>
   <td>
    <ul>
     <li>Microsoft Windows Server 2012 R2</li>
     <li>IBM AIX*</li>
     <li>Sun Solaris*</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Programservrar<br /> </td>
   <td>
    <ul>
     <li>Oracle Weblogic</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Databaser</td>
   <td>
    <ul>
     <li>IBM DB2 <br /> </li>
     <li>Oracle RAC</li>
    </ul> </td>
  </tr>
  <tr>
   <td>LDAP-servrar</td>
   <td>
    <ul>
     <li>Microsoft Active Directory 2012</li>
     <li>Novell eDirectory 8.8.7 </li>
     <li>IBM Lotus Domino 8.5.0 </li>
    </ul> </td>
  </tr>
  <tr>
   <td>E-postservrar</td>
   <td>
    <ul>
     <li>IBM Lotus Domino 8.5.0 </li>
    </ul> </td>
  </tr>
  <tr>
   <td>Kopplingar</td>
   <td>
    <ul>
     <li>Koppling för Microsoft Sharepoint 2013</li>
     <li>Connector for EMC Documentum 7.0</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Appen AEM Forms<br /> </td>
   <td>
    <ul>
     <li>Stöd för Windows 8.1</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Java </td>
   <td>
    <ul>
     <li>Java 11</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

* Kontakta Adobe Support för information om migrering till en annan plattform

#### Nya HTML5-baserade användargränssnitt {#new-html-based-uis}

I linje med det planerade EOL-programmet för Adobe Flash Player och den övergripande inriktningen på att migrera Flash-baserat innehåll till öppna standarder har AEM 6.5-formulären ersatt det Flash-baserade gränssnittet för hälsoövervakning, processhantering, Reader-tillägg och gränssnittet för kategorihantering i AEM Forms på JEE Administration Console med HTML5-baserat användargränssnitt.

#### Säkerhetsförbättringar {#security-improvements}

* AEM 6.5 Forms on JEE Administration Console UI baseras nu på Apache Struts 2.5.
* AEM 6.5 Forms använder nu jQuery till 3.2.1 och jQuery UI 1.12.1. Se [uppgraderingsdokumentation](/help/forms/home.md) för ändringens effekt.

#### Förbättringar av hjälpmedel {#accessibility-improvements}

AEM 6.5-formulär har förbättrat tillgängligheten på AEM Forms Workspace.
