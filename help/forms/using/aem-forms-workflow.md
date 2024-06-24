---
title: Forms-centrerat arbetsflöde i OSGi
description: Använd AEM Forms Workflow för att automatisera och snabbt bygga upp granskningar och godkännanden för att starta dokumenttjänster
topic-tags: publish, document_services
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
exl-id: c3e5f8fc-d2b9-4f76-9a3d-4bc5733f5a5c
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Foundation Components
role: User, Developer
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '3579'
ht-degree: 0%

---

# Forms-centrerat arbetsflöde i OSGi{#forms-centric-workflow-on-osgi}

![hero-image](do-not-localize/header.png)

Företag samlar in data från hundratals och tusentals formulär, olika datasystem samt online- och offlinedatakällor. De har också en dynamisk uppsättning användare som kan fatta beslut om data, vilket innefattar iterativa gransknings- och godkännandeprocesser.

Förutom arbetsflöden för granskning och godkännande för interna och externa målgrupper har stora organisationer och företag repetitiva uppgifter. Du kan till exempel konvertera ett PDF-dokument till ett annat format. När du gör det manuellt tar dessa uppgifter lång tid och tar mycket tid och resurser. Företag har också juridiska krav på att digitalt signera ett dokument och arkivera formulärdata för senare användning i fördefinierade format.

## Introduktion till Forms-centrerat arbetsflöde i OSGi {#introduction-to-forms-centric-workflow-on-osgi}

Du kan använda AEM arbetsflöden för att snabbt skapa anpassningsbara formulärbaserade arbetsflöden. Dessa arbetsflöden kan användas för granskning och godkännande, affärsprocessflöden, för att starta dokumenttjänster, integrera med Adobe Sign signaturarbetsflöde och liknande åtgärder. Till exempel kreditkortsansökningsbehandling, godkännandearbetsflöden för medarbetare och spara ett formulär som ett PDF-dokument. Dessutom kan dessa arbetsflöden användas inom en organisation eller över nätverkets brandvägg.

Med Forms-baserade arbetsflöden i OSGi kan du snabbt skapa och distribuera arbetsflöden för olika uppgifter i OSGi-stacken, utan att behöva installera den fullständiga processhanteringsfunktionen i JEE-stacken. För utveckling och hantering av arbetsflöden används de välbekanta funktionerna för AEM och AEM. Arbetsflöden är grunden för automatisering av affärsprocesser som spänner över flera olika system, nätverk, avdelningar och till och med organisationer.

När du väl har konfigurerat arbetsflödena kan de aktiveras manuellt för att slutföra en definierad process eller köras programmatiskt när användare skickar ett formulär eller [korrespondenshantering](/help/forms/using/cm-overview.md) brev. Med de här förbättrade AEM Workflow-funktionerna erbjuder AEM Forms två distinkta, men likartade, funktioner. Som en del av er distributionsstrategi måste ni bestämma vilken som fungerar för er. Se en [jämförelse](capabilities-osgi-jee-workflows.md) av Forms-centrerade arbetsflöden AEM OSGi och Process Management på JEE. För distributionstopologin finns dessutom följande information: [Arkitektur och driftsättningstopologier för AEM Forms](/help/forms/using/aem-forms-architecture-deployment.md).

Forms-centrerat arbetsflöde i OSGi utökar [AEM](/help/sites-authoring/inbox.md) och innehåller extra komponenter (steg) AEM arbetsflödesredigeraren som kan användas för AEM Forms-centrerade arbetsflöden. Den utökade AEM Inkorgen har funktioner som liknar [AEM Forms Workspace](introduction-html-workspace.md). Förutom att hantera humancentrerade arbetsflöden (godkännande, granskning och så vidare) kan du använda AEM arbetsflöden för att automatisera [dokumenttjänster](/help/sites-developing/workflows-step-ref.md)-relaterade åtgärder (till exempel Generera PDF) och dokument för elektronisk signering (Adobe Sign).

Alla arbetsflödessteg i AEM Forms har stöd för användning av variabler. Variabler möjliggör arbetsflödessteg för att lagra och skicka metadata mellan steg vid körning. Du kan skapa olika typer av variabler för att lagra olika typer av data. Du kan också skapa variabelsamlingar (arrayer) för att lagra flera instanser av relaterade data av samma typ. Vanligtvis använder du en variabel eller en samling variabler när du behöver fatta ett beslut baserat på det värde som den innehåller eller för att lagra information som du behöver senare i en process. Mer information om hur du använder variabler i dessa Forms-centrerade arbetsflödeskomponenter (steg) finns i [Forms-centrerat arbetsflöde i OSGi - stegreferens](../../forms/using/aem-forms-workflow-step-reference.md). Mer information om att skapa och hantera variabler finns i [Variabler i AEM arbetsflöden](../../forms/using/variable-in-aem-workflows.md).

I följande diagram visas hela proceduren för att skapa, köra och övervaka ett Forms-orienterat arbetsflöde i OSGi.

![introduction-to-aem-forms-workflow](assets/introduction-to-aem-forms-workflow.jpg)

## Innan du börjar {#before-you-start}

* Ett arbetsflöde är en representation av en affärsprocess i verkligheten. Håll er verkliga affärsprocess och lista över deltagarna i affärsprocessen klar. Ha också materialet (adaptiva formulär, PDF-dokument med mera) färdigt innan du börjar skapa ett arbetsflöde.
* Ett arbetsflöde kan ha flera steg. De här stegen visas i AEM Inkorg och hjälper till att rapportera arbetsflödets förlopp. Dela upp affärsprocessen i logiska steg.
* Du kan konfigurera tilldelningssteget AEM arbetsflöden för att skicka e-postmeddelanden till användare eller tilldelade användare. Så, [aktivera e-postmeddelanden](#configure-email-service).
* Ett arbetsflöde kan även använda Adobe-signaturer för digitala signaturer. Om du tänker använda Adobe Sign i ett arbetsflöde, [konfigurera Adobe Sign för AEM Forms](../../forms/using/adobe-sign-integration-adaptive-forms.md) innan du använder den i ett arbetsflöde.

## Skapa en arbetsflödesmodell {#create-a-workflow-model}

En arbetsflödesmodell består av logik och flöde i en affärsprocess. Den består av en serie av steg. De här stegen är AEM komponenter. Du kan utöka arbetsflödesstegen med parametrar och skript för att få mer funktionalitet och kontroll efter behov. AEM Forms innehåller några steg utöver AEM steg som är tillgängliga direkt. En detaljerad lista över steg i AEM och AEM Forms finns på [AEM för arbetsflödessteg](/help/sites-developing/workflows-step-ref.md) och [Forms-centrerat arbetsflöde i OSGi - stegreferens](../../forms/using/aem-forms-workflow.md).

AEM tillhandahåller ett intuitivt användargränssnitt för att skapa en arbetsflödesmodell med de angivna arbetsflödesstegen. Stegvisa instruktioner om hur du skapar en arbetsflödesmodell finns i [Skapa arbetsflödesmodeller](/help/sites-developing/workflows-models.md). Följande exempel innehåller stegvisa instruktioner för att skapa en arbetsflödesmodell för ett arbetsflöde för godkännande och granskning:

>[!NOTE]
>
>Du måste vara medlem i arbetsflödets redigeringsgrupp för att kunna skapa eller redigera en arbetsflödesmodell.

### Skapa en modell för ett arbetsflöde för godkännande och granskning {#create-a-model-for-an-approval-and-review-workflow}

Arbetsflödet för godkännande och granskning är avsett för de uppgifter som kräver mänsklig medverkan för att fatta beslut. I följande exempel skapas en arbetsflödesmodell för en låneansökan som ska fyllas av en banktjänsteman. När ansökan är ifylld skickas den för godkännande. Senare skickas den godkända ansökan till den som ansöker om elektroniska signaturer med Adobe Sign.

Exemplet är tillgängligt som ett paket som bifogas nedan. Importera och installera exemplet med hjälp av pakethanteraren. Du kan även utföra följande steg för att manuellt skapa arbetsflödesmodellen för programmet:

I exemplet skapas en arbetsflödesmodell för en låneansökan som ska fyllas av en bankagent på ett bankkontor. När ansökan är ifylld skickas den för godkännande. Senare skickas den godkända ansökan till kunden för elektroniska signaturer med Adobe Sign. Du kan importera och installera exemplet med hjälp av pakethanteraren.

[Hämta fil](assets/example-mortgage-loan-application.zip)

1. Öppna konsolen Arbetsflödesmodeller. Standardwebbadressen är `https://[server]:[port]/libs/cq/workflow/admin/console/content/models.html/etc/workflow/models`
1. Välj **Skapa** sedan **Skapa modell**. Dialogrutan Lägg till arbetsflödesmodell visas.
1. Ange **Titel** och **Namn** (valfritt). Till exempel en låneansökan. Välj **Klar**.
1. Välj den nya arbetsflödesmodellen och välj **Redigera**. Nu kan du lägga till arbetsflödessteg för att skapa affärslogik. När du först skapar en arbetsflödesmodell innehåller den:

   * Stegen: Flödesstart och Flödesslut. De här stegen representerar början och slutet av arbetsflödet. Dessa steg är obligatoriska och kan inte redigeras eller tas bort.
   * Ett exempel på deltagarsteg som heter Steg 1. Det här steget är konfigurerat för att tilldela en arbetsuppgift till administratörsanvändaren. Ta bort steget.

1. Aktivera e-postmeddelanden. Du kan konfigurera ett Forms-orienterat arbetsflöde på OSGi för att skicka e-postmeddelanden till användare eller tilldelade användare. Gör följande konfigurationer för att aktivera e-postmeddelanden:

   1. Gå till AEM konfigurationshanteraren på `https://[server]:[port]/system/console/configMgr`.
   1. Öppna **[!UICONTROL Day CQ Mail Service]** konfiguration. Ange ett värde för **[!UICONTROL SMTP server host name]**, **[!UICONTROL SMTP server port,]** och **[!UICONTROL "From" address]** fält. Klicka på **[!UICONTROL Save]**.
   1. Öppna **[!UICONTROL Day CQ Link Externalizer]** konfiguration. I **[!UICONTROL Domains]** anger du den faktiska värdnamnet/IP-adressen och portnumret för lokala instanser, författare och publiceringsinstanser. Klicka på **[!UICONTROL Save]**.

1. Skapa arbetsflödesfaser. Ett arbetsflöde kan ha flera steg. De här stegen visas i AEM Inkorg och rapporterar arbetsflödets förlopp.

   Om du vill definiera en scen väljer du ![info-circle](assets/info-circle.png) ikon för att öppna arbetsflödesmodellegenskaper, öppna **Steg** lägg till faser för arbetsflödesmodellen och markera **Spara och stäng**. I exemplet med låneansökan kan du skapa faser: låneansökan, status för låneansökan, signerade dokument och signerade lånedokument.

1. Dra och släpp **Tilldela uppgift** steg webbläsare till arbetsflödesmodellen. Gör det till modellens första steg.

   Tilldela en uppgiftskomponent tilldelar uppgiften, som skapas i ett arbetsflöde, till en användare eller grupp. Förutom att tilldela uppgiften kan du använda komponenten för att ange ett adaptivt formulär eller ett icke-interaktivt PDF för uppgiften. Det adaptiva formuläret krävs för att kunna ta emot indata från användare och icke-interaktiva PDF eller ett skrivskyddat anpassat formulär används endast för granskning.

   Du kan också använda steget för att styra aktivitetens beteende. Om du till exempel skapar ett automatiskt postdokument, tilldelar uppgiften till en viss användare eller grupp, sökvägen till skickade data, sökvägen till data som ska fyllas i i i förväg samt standardåtgärder. Detaljerad information om alternativen för tilldelningssteget finns i [Forms-centrerat arbetsflöde i OSGi - stegreferens](../../forms/using/aem-forms-workflow.md) -dokument.

   ![arbetsflödesredigerare](assets/workflow-editor.png)

   I exemplet med låneansökan ska du konfigurera tilldelningssteget så att det använder ett skrivskyddat anpassat formulär och visa PDF-dokument när uppgiften är klar. Välj även en användargrupp som kan godkänna lånebegäran. På **Åtgärder** -flik, inaktivera **Skicka** alternativ. Skapa en **actionTaken** variabeln för datatypen String och ange variabeln som **Flödesvariabel**. Till exempel actionTaken. Lägg även till rutterna Godkänn och Avvisa. Vägarna visas som separata åtgärder (knappar) i AEM. Arbetsflödet väljer en gren baserat på den åtgärd (knapp) som användaren knackar på.

   Du kan importera exempelpaketet, som är tillgängligt för nedladdning i början av avsnittet, för den fullständiga uppsättningen värden för alla fält i tilldelningssteget som konfigurerats, till exempel låneansökan.

1. Dra och släpp OR-komponenten från stegwebbläsaren till arbetsflödesmodellen. Med ELLER-delning skapas en delning i arbetsflödet, varefter endast en gren är aktiv. I det här steget kan du lägga in sökvägar för villkorlig bearbetning i arbetsflödet. Du kan lägga till arbetsflödessteg i varje gren efter behov.

   Du kan definiera routningsuttryck för en gren med en regeldefinition, ett ECMA-skript eller ett externt skript.

   Använd uttrycksredigeraren för att skapa routningsuttryck för Förgrening 1 och Förgrening 2. Dessa routningsuttryck hjälper dig att välja en gren baserat på användaråtgärden i AEM Inbox.

   **Routningsuttryck för gren 1**

   När en användare trycker **Godkänn** AEM Inkorgen är grenen 1 aktiverad.

   ![ELLER Dela exempel](assets/orsplit_branch1_active_new.png)

   **Routningsuttryck för gren 2**

   När en användare trycker **Avvisa** AEM Inkorgen aktiveras grenen 2.

   ![ELLER Dela exempel](assets/orsplit_branch2_active_new.png)

   Mer information om hur du skapar routningsuttryck med variabler finns i [Variabler i AEM Forms arbetsflöden](../../forms/using/variable-in-aem-workflows.md).

1. Lägg till andra arbetsflödessteg för att skapa affärslogiken.

   I hypoteksexemplet lägger du till ett genererat postdokument, två tilldelningar av uppgiftssteg och ett signeringsdokumentsteg i förgrening 1 av modellen, som visas i bilden nedan. Ett tilldelningssteg är att visa och skicka **ska undertecknas av den sökande** och en annan tilldelad uppgiftskomponent är **för att visa signerade dokument**. Lägg också till en tilldelad uppgiftskomponent i gren 2. Den aktiveras när en användare trycker på Avvisa i AEM Inkorg.

   Om du vill visa en komplett uppsättning värden för alla fält i tilldelningsstegen, dokumentsteget och signeringsdokumentsteget, som konfigurerats för exempelvis låneprogram, importerar du exempelpaketet som är tillgängligt för hämtning i början av det här avsnittet.

   Arbetsflödesmodellen är klar. Du kan starta arbetsflödet på olika sätt. Mer information finns i [Starta ett Forms-orienterat arbetsflöde i OSGi](#launch).

   ![arbetsflödeseditor-inteckning](assets/workflow-editor-mortgage.png)

## Skapa ett Forms-centrerat arbetsflödesprogram {#create-a-forms-centric-workflow-application}

Programmet är det adaptiva formulär som är associerat med arbetsflödet. När ett program skickas via Inkorgen startar det tillhörande arbetsflödet. Om du vill göra ett Forms-arbetsflöde tillgängligt som ett program i AEM Inbox och AEM Forms App skapar du ett arbetsflödesprogram på följande sätt:

>[!NOTE]
>
>Du måste vara medlem i gruppen fd-administrator för att kunna skapa och hantera arbetsflödesprogram.

1. Gå till AEM ![verktyg-1](assets/tools-1.png) > **[!UICONTROL Forms]** > **[!UICONTROL Manage Workflow Application]** och **[!UICONTROL Create]**.
1. Ange indata för följande fält och tryck på dem i fönstret Skapa arbetsflödesprogram **Skapa**. Ett nytt program skapas och visas på skärmen Arbetsflödesprogram.

<table>
 <tbody>
  <tr>
   <td>Fält</td>
   <td>Beskrivning</td>
  </tr>
  <tr>
   <td>Titel</td>
   <td>Titeln visas AEM Inkorgen och hjälper användarna att välja ett program. Behåll det beskrivande. Exempel: Öppningsprogram för sparkonto.<br /> </td>
  </tr>
  <tr>
   <td>Namn </td>
   <td>Ange programmets namn. Alla tecken utom alfabet, siffror, bindestreck och understreck ersätts med bindestreck. </td>
  </tr>
  <tr>
   <td>Beskrivning</td>
   <td>Beskrivningen visas i AEM. Ange detaljerad information om programmet i beskrivningsfälten. Till exempel programmets syfte.<br /> </td>
  </tr>
  <tr>
   <td>Adaptiv form</td>
   <td><p>Ange sökvägen till ett anpassat formulär. När en användare startar ett program visas det angivna adaptiva formuläret.</p> <p><strong>Anteckning</strong>: Arbetsflödesprogram stöder inte formulär och PDF-dokument som är längre än en sida eller som behöver rullas i Apple iPad. När ett program öppnas i Apple iPad och det adaptiva formuläret eller PDF-dokumentet är längre än en sida, försvinner formulärfälten och innehållet från den andra sidan.</p> </td>
  </tr>
  <tr>
   <td>Åtkomstgrupp</td>
   <td><p>Markera en grupp. Programmet visas i AEM Inkorg endast för medlemmarna i den markerade gruppen. Med alternativet för åtkomstgrupp blir alla grupper i gruppen för arbetsflödesanvändare tillgängliga för val. </p> <br /> </td>
  </tr>
  <tr>
   <td>Förifyllningstjänst</td>
   <td>Välj en <a href="../../forms/using/prepopulate-adaptive-form-fields.md#aem-forms-custom-prefill-service" target="_blank">förifyllning</a> för den adaptiva formen.<br /> </td>
  </tr>
  <tr>
   <td>Arbetsflödesmodell</td>
   <td>Välj en <a href="../../forms/using/aem-forms-workflow.md#create-a-workflow-model">arbetsflödesmodell</a> för programmet. En arbetsflödesmodell består av logik och flöde i affärsprocessen. </td>
  </tr>
  <tr>
   <td>Sökväg till datafil</td>
   <td>Ange sökvägen till datafilen i crx-databasen. Sökvägen är relativ till adaptiv formulärnyttolast och innehåller datafilens namn. Inkludera alltid filens fullständiga namn, inklusive filnamnstillägget, om tillämpligt. Exempel: [nyttolast]/data.xml. </td>
  </tr>
  <tr>
   <td>Sökväg till bifogad fil</td>
   <td>Ange sökvägen till mappen för bifogade filer i crx-databasen. Sökvägen till den bifogade filen är relativ till nyttolastplatsen. Exempel: [nyttolast]/data.xml. </td>
  </tr>
  <tr>
   <td>Dokumentsökväg</td>
   <td>Ange sökvägen till filen Dokument för post i crx-databasen. Sökvägen är relativ till en variabel formulärnyttolastplats. Inkludera alltid filens fullständiga namn, inklusive filnamnstillägget, om tillämpligt. Exempel: [nyttolast]/DOR/creditcard.pdf.</td>
  </tr>
 </tbody>
</table>

## Starta ett Forms-orienterat arbetsflöde i OSGi {#launch}

Du kan starta eller utlösa ett Forms-centrerat arbetsflöde genom att:

* [Skicka ett program från AEM Inbox](#inbox)
* [Skicka ett program från AEM Forms App](#afa)

* [Skicka ett anpassat formulär](#af)
* [Använda bevakad mapp](#watched)

* [Skicka ett interaktivt meddelande eller ett brev](#letter)

### Skicka ett program från AEM Inbox {#inbox}

Arbetsflödesprogrammet som du skapade är tillgängligt som ett program i Inbox. Användare som är medlemmar i en grupp med arbetsflödesanvändare kan fylla i och skicka programmet som utlöser det associerade arbetsflödet. Mer information om hur du använder AEM Inbox för att skicka program och hantera uppgifter finns i [Hantera Forms-program och -uppgifter i AEM Inkorg](../../forms/using/manage-applications-inbox.md).

### Skicka ett program från AEM Forms App {#afa}

AEM Forms-appen synkroniseras med en AEM Forms-server så att du kan ändra formulärdata, uppgifter, arbetsflödesprogram och sparad information (utkast/mallar) i ditt konto. Mer information finns i [AEM Forms](/help/forms/using/aem-forms-app.md) och relaterade artiklar.

### Skicka ett anpassat formulär {#af}

Du kan konfigurera skicka-åtgärderna för ett adaptivt formulär så att ett arbetsflöde startas när det adaptiva formuläret skickas. Adaptiva formulär ger **Anropa ett AEM** skicka-åtgärd för att starta ett arbetsflöde när ett anpassat formulär skickas. Mer information om åtgärden Skicka finns i [Konfigurera åtgärden Skicka](../../forms/using/configuring-submit-actions.md). Om du vill skicka ett adaptivt formulär via appen AEM Forms aktiverar du Synkronisera med AEM Forms App i de adaptiva formuläregenskaperna.

Du kan konfigurera ett anpassningsbart formulär så att det synkroniserar, skickar och utlöser ett arbetsflöde från AEM Forms-appen. Mer information finns i [arbeta med ett formulär](/help/forms/using/working-with-form.md).

### Använda en bevakad mapp {#watched}

En administratör (medlem i gruppen fd-administratörer) kan konfigurera en nätverksmapp så att den kör ett förkonfigurerat arbetsflöde när en användare placerar en fil (till exempel en PDF-fil) i mappen. När arbetsflödet har slutförts kan resultatfilen sparas i en angiven utdatamapp. En sådan mapp kallas [Bevakad mapp](../../forms/using/watched-folder-in-aem-forms.md). Så här konfigurerar du en bevakad mapp för att starta ett arbetsflöde:

1. Gå till AEM ![verktyg-1](assets/tools-1.png) > **[!UICONTROL Forms]** > **[!UICONTROL Configure Watched Folder]**. En lista över redan konfigurerade bevakade mappar visas.
1. Välj **[!UICONTROL New]**. En lista med fält visas. Ange ett värde för följande fält för att konfigurera en bevakad mapp för ett arbetsflöde:

<table>
 <tbody>
  <tr>
   <td>Fält</td>
   <td>Beskrivning</td>
  </tr>
  <tr>
   <td><span class="uicontrol">Namn</code></td>
   <td>Ange namnet på den bevakade mappen. Det här fältet stöder endast alfanumeriska tecken.</td>
  </tr>
  <tr>
   <td><span class="uicontrol">Bana</code></td>
   <td>Ange den fysiska platsen för den bevakade mappen. I en klustrad miljö använder du en delad nätverksmapp som är tillgänglig från AEM klusternod.</td>
  </tr>
  <tr>
   <td><span class="uicontrol">Bearbeta filer med</code></td>
   <td>Välj <span class="uicontrol">Arbetsflöde </code>alternativ. </td>
  </tr>
  <tr>
   <td><span class="uicontrol">Arbetsflödesmodell</code></td>
   <td>Välj en arbetsflödesmodell.<br /> </td>
  </tr>
  <tr>
   <td><span class="uicontrol">Mönster för utdatafil</code></td>
   <td>Ange katalogstrukturen för utdatafiler och kataloger. Du kan också ange en <a href="/help/forms/using/admin-help/configuring-watched-folder-endpoints.md" target="_blank">mönster för utdatafiler och kataloger</a>.</td>
  </tr>
 </tbody>
</table>

1. Välj **Avancerat**. Ange ett värde för följande fält och tryck **Skapa**. Den bevakade mappen är konfigurerad för att starta ett arbetsflöde. När en fil placeras i indatakatalogen för den bevakade mappen aktiveras nu det angivna arbetsflödet.

   | Fält | Beskrivning |
   |---|---|
   | Nyttolastmappningsfilter | När du skapar en bevakad mapp skapas en mappstruktur i crx-databasen. Mappstrukturen kan fungera som en nyttolast för arbetsflödet. Du kan skriva ett skript för att mappa ett AEM arbetsflöde och acceptera indata från den bevakade mappstrukturen. En out of the box-implementering är tillgänglig och visas i filtret för nyttolastmapparen. Om du inte har någon anpassad implementering väljer du standardimplementeringen. |

   Fliken Avancerat innehåller fler fält. De flesta av dessa fält innehåller ett standardvärde. Mer information om alla fält finns i [Skapa eller konfigurera en bevakad mapp](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md) artikel.

### Skicka ett interaktivt meddelande eller ett brev {#letter}

Du kan associera och köra ett Forms-centrerat arbetsflöde i OSGi när du skickar ett interaktivt meddelande eller ett brev. I arbetsflöden för hantering av korrespondens används för efterbearbetning av interaktiv kommunikation och brev. Du kan till exempel skicka e-post, skriva ut, faxa eller arkivera de slutliga breven. Detaljerade anvisningar finns i [Efterbearbetning av interaktiv kommunikation och interaktiva brev](../../forms/using/submit-letter-topostprocess.md).

## Ytterligare konfigurationer {#additional-configurations}

### Konfigurera e-posttjänst {#configure-email-service}

Du kan använda stegen Tilldela uppgift och Skicka e-post i AEM arbetsflöden för att skicka ett e-postmeddelande. Utför följande steg för att ange e-postservrar och andra konfigurationer som krävs för att skicka e-post:

1. Gå till AEM konfigurationshanteraren på `https://[server]:[port]/system/console/configMgr`.
1. Öppna **[!UICONTROL Day CQ Mail Service]** konfiguration. Ange ett värde för **[!UICONTROL SMTP server host name]**, **[!UICONTROL SMTP server port,]** och **[!UICONTROL "From" address]** fält. Klicka på **[!UICONTROL Save]**.
1. Öppna **[!UICONTROL Day CQ Link Externalizer]** konfiguration. I **[!UICONTROL Domains]** anger du den faktiska värdnamnet/IP-adressen och portnumret för lokala instanser, författare och publiceringsinstanser. Klicka på **[!UICONTROL Save]**.

### Rensa arbetsflödesinstanser {#purge-workflow-instances}

Om du minimerar antalet arbetsflödesinstanser ökas arbetsflödesmotorns prestanda, så att du regelbundet kan rensa avslutade eller pågående arbetsflödesinstanser från databasen. Mer information finns i [Vanlig tömning av arbetsflödesinstanser](/help/sites-administering/workflows-administering.md#regular) rensning av arbetsflödesinstanser.

## Parametrisera känsliga data till arbetsflödesvariabler och lagra i externa datalager {#externalize-wf-variables}

Alla data som skickas från anpassningsbara formulär till [!DNL Experience Manager] arbetsflöden kan ha PII (Personally Identiitable Information) eller SPD (Sensitive Personal Data) för företagets slutanvändare. Det är dock inte obligatoriskt att lagra data i [!DNL Adobe Experience Manager] [JCR-databas](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/underlying-technology/introduction-jcr.html). Du kan externalisera lagringen av slutanvändardata till din hanterade datalagring (till exempel Azure-blob-lagring) genom att parametrisera informationen i [arbetsflödesvariabler](/help/forms/using/variable-in-aem-workflows.md).

I en [!DNL Adobe Experience Manager] Forms arbetsflöde, data bearbetas och skickas genom en serie arbetsflödessteg med hjälp av arbetsflödesvariabler. Dessa variabler är namngivna egenskaper eller nyckelvärdepar som lagras i metadatanoden för arbetsflödesinstanser, till exempel `/var/workflow/instances/<serverid>/<datebucket>/<uniquenameof model>_<id>/data/metaData`. Dessa arbetsflödesvariabler kan läggas ut i en annan databas än JCR och sedan bearbetas av [!DNL Adobe Experience Manager] arbetsflöden. [!DNL Adobe Experience Manager] innehåller API `[!UICONTROL UserMetaDataPersistenceProvider]` för att lagra arbetsflödesvariablerna i din hanterade externa lagring. Mer information om hur du använder arbetsflödesvariabler för kundägda datalager i [!DNL Adobe Experience Manager], se [Administrera arbetsflödesvariabler för externa datalager](/help/sites-administering/workflows-administering.md#using-workflow-variables-customer-datastore).
[!DNL Adobe] innehåller följande [exempel](https://github.com/adobe/workflow-variable-externalizer) för att lagra variabler från arbetsflödets metadatamappning till Azure-blobblagring med hjälp av API [UserMetaDataPersistenceProvider](https://github.com/adobe/workflow-variable-externalizer/blob/master/README.md). På liknande rader kan du använda exemplet som vägledning [UserMetaDataPersistenceProvider] API för att externalisera arbetsflödesvariablerna i andra datalagringsplatser utanför [!DNL Adobe Experience Manager] och hantera samma sak.

>[!NOTE]
>
>När du lagrar arbetsflödesvariablerna i en extern datalagring bör du läsa pekarna i [riktlinjer för arbetsflöden för extern datalagring](#guidelines-workflows-external-data-storage).

### Installera API-exempelimplementeringen för arbetsflödet

Så här lagrar du arbetsflödesvariabler i din hanterade Azure-blobblagring:
1. Installera [exempel](https://github.com/adobe/workflow-variable-externalizer) arbetsflödes-API [UserMetaDataPersistenceProvider](https://github.com/adobe/workflow-variable-externalizer/blob/master/README.md) enligt följande:

   1. Kör i projektets rotkatalog i `mvn clean install` kommando med Maven 3.

   1. Om du vill distribuera paketet och det innehållspaket som ska skapas kör du `mvn clean install -PautoInstallPackage`.

   1. Om du bara vill distribuera paketet till författaren kör du `mvn clean install -PautoInstallBundle`.

1. Initiera följande egenskaper i OSGi-konfigurationsfilen för externalisering i i `ui.config` innehållspaket:

   ```JQL
      accountKey=""
      accountName=""
      endpointSuffix=""
      containerName=""
      protocol=""
   ```

Nedan följer några exempel och syften med dessa egenskaper:

* **accountKey** är den hemliga nyckeln för att auktorisera åtkomst.

* **accountName** är Azure-kontot där data måste lagras.

* **endpointSuffix**, till exempel `core.windows.net`.

* **containerName** är behållaren i kontot där data måste lagras. Exemplet förutsätter att behållaren finns.

* **protocol**, till exempel `https` eller `http`.

1. Konfigurera arbetsflödesmodellen i [!DNL Adobe Experience Manager]. Mer information om hur du konfigurerar arbetsflödesmodellen för en extern lagring finns i [Konfigurera arbetsflödesmodellen](#configure-aem-wf-model).

### Konfigurera arbetsflödesmodell i [!DNL Adobe Experience Manager] för extern datalagring {#configure-aem-wf-model}

Så här konfigurerar du en AEM arbetsflödesmodell för en extern datalagring:

1. Navigera till **[!UICONTROL Tools]** > **[!UICONTROL Workflow]** > **[!UICONTROL Models]**.

1. Välj ett modellnamn och välj **[!UICONTROL Edit]**.

1. Välj ikonen Sidinformation och välj **[!UICONTROL Open Properties]**.

1. Välj **[!UICONTROL Externalize workflow data storage]**.

1. Välj **[!UICONTROL Save & Close]** för att spara egenskaperna.

### Riktlinjer för AEM arbetsflöden för extern datalagring {#guidelines-workflows-external-data-storage}

Följande riktlinjer gäller när du använder [!DNL Adobe Experience Manager] arbetsflöden och lagring av data till externa datalager (till exempel Microsoft Azure-lagringsserver):

* Använd variabler för att lagra data när du definierar in- och utdatafiler och bilagor i arbetsflödesmodellstegen. Markera inte **[!UICONTROL Relative to Payload]** och **[!UICONTROL Available at an absolute path]** alternativ. The **[!UICONTROL Relative to Payload]** och **[!UICONTROL Available at an absolute path]** visas inte automatiskt när du [konfigurera [!DNL Adobe Experience Manager] arbetsflödesmodell för extern datalagring](#configure-aem-wf-model).

* Använd variabler för att lagra datafiler och bilagor när du skickar ett anpassat formulär till ett AEM arbetsflöde. Markera inte **[!UICONTROL Relative to Payload]** när du skickar ett anpassat formulär till en [!DNL Adobe Experience Manager] arbetsflöde. The **[!UICONTROL Relative to Payload]** alternativet visas inte automatiskt när du [konfigurera [!DNL Adobe Experience Manager] arbetsflödesmodell för extern datalagring](#configure-aem-wf-model).

* Använd inte en anpassad [!DNL Adobe Experience Manager] arbetsflödessteg i en arbetsflödesmodell för att lagra data i [!UICONTROL CRX DE] databas.

* När du [konfigurera [!DNL Adobe Experience Manager] arbetsflödesmodell för extern datalagring](#configure-aem-wf-model)skapar du inte anpassade kolumner för [!DNL Adobe Experience Manager] [!UICONTROL Inbox] eftersom värdena i de anpassade kolumnerna inte hämtas om arbetsobjektet i [!DNL Adobe Experience Manager] [!UICONTROL Inbox] tillhör ett arbetsflöde som är markerat för extern lagring.
