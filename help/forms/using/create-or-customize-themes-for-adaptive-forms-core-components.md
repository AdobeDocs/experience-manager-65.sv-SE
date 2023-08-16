---
title: Hur skapar eller anpassar man adaptiva formulärteman?
seo-title: How to create a theme for Adaptive Forms Core Components?
description: Lär dig att skapa eller anpassa teman för adaptiva Forms Core-komponenter med BEM-specifikationer
seo-description: Learn to create or customize themes for Adaptive Forms Core Components using BEM specifications
keywords: skapa anpassningsbara formulär, skapa ett nytt tema, anpassa tema, ladda upp nytt tema, använda tema i formulär, ta bort ett tema, skapa ett tema i AEM 6.5-formulär
contentOwner: Khushwant Singh
topic-tags: Adaptive Forms
docset: aem65
role: Admin, Developer
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '1967'
ht-degree: 0%

---


# Skapa eller anpassa ett anpassat formulärtema {#introduction-to-theme}

| Version | Artikellänk |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Klicka här](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/using-themes-in-core-components.html) |
| AEM 6.5 | Denna artikel |


**Gäller för:** ✅ adaptiva grundkomponenter ❎ [Komponenter i adaptiv Form Foundation](/help/forms/using/themes.md).

I AEM Forms 6.5 är ett tema ett AEM klientbibliotek som du använder för att definiera format (utseende och känsla) för ett adaptivt formulär. Ett tema innehåller formatinformation för komponenterna och panelerna. Format innehåller egenskaper som bakgrundsfärger, lägesfärger, genomskinlighet, justering och storlek. När du använder ett tema återspeglas det angivna formatet i motsvarande komponenter. Ett tema hanteras separat utan referens till ett adaptivt formulär och kan återanvändas i flera adaptiva Forms.

## Tillgängliga teman {#available-theme}

AEM 6.5-miljön innehåller följande teman för Core Components based Adaptive Forms:

* [Tema Canvas](https://github.com/adobe/aem-forms-theme-canvas)
* [WKND-tema](https://github.com/adobe/aem-forms-theme-wknd)
* [EASEL-tema](https://github.com/adobe/aem-forms-theme-easel)

## Om temats struktur {#understanding-structure-of-theme}

Ett tema är ett paket som omfattar CSS-filen, JavaScript-filer och resurser (som ikoner) som definierar formatet för din adaptiva Forms. Temat Adaptiv form följer en särskild organisation som består av följande komponenter:

* `src/theme.scss`: Den här mappen innehåller CSS-filen som har stor effekt på hela temat. Det fungerar som en central plats för att definiera och hantera temats format och beteende. Genom att redigera den här filen kan du göra ändringar som tillämpas överallt i temat, vilket påverkar både utseendet och funktionaliteten på dina adaptiva Forms- och AEM Sites-sidor.

* `src/site`: Den här mappen innehåller CSS-filer som används på en hel AEM. Dessa filer består av kod och format som påverkar den övergripande funktionen och layouten för AEM webbplats. Alla ändringar som görs här återspeglas på alla sidor på webbplatsen.

* `src/components`: CSS-filerna i den här mappen är utformade för enskilda AEM kärnkomponenter. Varje dedikerad mapp för en komponent innehåller en `.scss` som formaterar en viss komponent i ett adaptivt formulär. Till exempel `/src/components/button/_button.scss` filen innehåller formatinformation för den adaptiva Forms Button-komponenten.

  ![Arbetsytans temastruktur](/help/forms/using/assets/component-based-theme-folder-structure.png)

* `src/resources`: Den här mappen innehåller statiska filer som ikoner, logotyper och teckensnitt. Resurserna används för att förbättra temats visuella element och övergripande design.

## Skapa ett tema

AEM Forms 6.5 innehåller följande teman för Core Components based Adaptive Forms.

* [Tema Canvas](https://github.com/adobe/aem-forms-theme-canvas)
* [WKND-tema](https://github.com/adobe/aem-forms-theme-wknd)
* [EASEL-tema](https://github.com/adobe/aem-forms-theme-easel)

Du kan [anpassa något av dessa teman för att skapa ett tema](#customize-a-theme-core-components).

## Anpassa ett tema {#customize-a-theme-core-components-based-adaptive-forms}

Att anpassa ett tema avser processen att ändra och anpassa utseendet på ett tema. När du anpassar ett tema ändrar du dess designelement, layout, färger, typografi och ibland den underliggande koden. På så sätt kan du skapa ett unikt och skräddarsytt utseende för webbplatsen eller tillämpningen, samtidigt som du bibehåller den grundläggande strukturen och funktionaliteten som temat ger.

>[!NOTE]
>
> * Använd Pakethanteraren för att distribuera ett tema på alla författare- och publiceringsinstanser.
> * Ett temaklientbibliotek importeras eller exporteras via Package Manager precis som andra paket.

### Krav för att anpassa ett tema {#prerequisites}

* [Aktivera adaptiva Forms Core-komponenter](/help/forms/using/enable-adaptive-forms-core-components.md) för din miljö.

* Installera den senaste versionen av [Apache Maven.](https://maven.apache.org/download.cgi) Apache Maven är ett automatiserat byggverktyg som ofta används för Java™-projekt. Genom att installera den senaste versionen får du de beroenden du behöver för att anpassa temat.

* Lär dig skapa en [klientbibliotek i Adobe Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-65/developing/introduction/clientlibs.html). AEM tillhandahåller klientbibliotek, som gör att du kan lagra din klientkod i databasen, ordna den i kategorier och definiera när och hur varje kodkategori ska skickas till klienten.

* Installera en vanlig textredigerare. Exempel: Microsoft® Visual Studio Code. Med en vanlig textredigerare som Microsoft® Visual Studio Code får du en användarvänlig miljö där du kan redigera och ändra temafiler.

* Kontrollera att AEM Forms-miljön är igång.

### Att tänka på när du anpassar ett tema {#consideration}

* Se till att du använder [Arketype-projektet som används för att aktivera adaptiva Forms Core-komponenter](/help/forms/using/enable-adaptive-forms-core-components.md) i din miljö för att anpassa dina teman.

* När du publicerar ett adaptivt formulär publiceras inte klientbiblioteken automatiskt vid publiceringsinstansen. Kontrollera att du manuellt publicerar klientbiblioteket som det hänvisas till i ett adaptivt formulär till dina publiceringsmiljöer.

* Adobe rekommenderar att du inte ändrar klassnamn för klientbibliotek.

### Anpassa ett tema {#customize-a-theme-core-components}

Att skapa eller anpassa ett tema är en process i flera steg. Utför stegen i listan för att skapa/anpassa temat:

1. [Klona ett tema](#clone-git-repo-of-theme)
1. [Anpassa temats utseende](#customize-the-theme)
1. [Förbered temat för lokal driftsättning](#generate-the-clientlib)
1. [Distribuera temat i en lokal miljö](#deploy-the-theme-on-a-local-environment)
1. [Distribuera temat i produktionsmiljön](#5-deploy-a-theme-on-your-production-environment)

<!--
 ![Theme Customization workflow](/help/forms/using/assets/custom-theme-steps.png)
-->

Exemplen i dokumentet är baserade på **Arbetsyta** men du kan klona vilket tema som helst och anpassa det med samma instruktioner. Dessa instruktioner kan användas för alla teman och du kan ändra teman efter dina specifika behov.

#### 1. Klona Git-databasen för temat {#clone-git-repo-of-theme}

Om du vill klona ett tema för Core Components based Adaptive Forms väljer du ett av följande teman:

* [Tema Canvas](https://github.com/adobe/aem-forms-theme-canvas)
* [WKND-tema](https://github.com/adobe/aem-forms-theme-wknd)
* [EASEL-tema](https://github.com/adobe/aem-forms-theme-easel)

Utför följande instruktioner för att klona ett tema:

1. Öppna kommandotolken eller terminalfönstret i den lokala utvecklingsmiljön.

1. Kör `git clone` för att klona ett tema.

   ```
      git clone [Path of Git Repository of the theme]
   ```

   Ersätt [Sökväg till temats Git-databas] med den faktiska URL:en för temats motsvarande Git-databas

   Om du till exempel vill klona arbetsytans tema kör du följande kommando:

   ```
      git clone https://github.com/adobe/aem-forms-theme-canvas
   ```

1. Välj **Författarna av alla filer i den överordnade mappen är betrodda** och klicka **Ja, jag litar på författarna**.

När kommandot har körts har du en lokal kopia av temat på datorn i  `aem-forms-theme-canvas` mapp.

#### 2. Anpassa temat {#customize-the-theme}

Du kan anpassa enskilda komponenter eller göra ändringar på temanivå med hjälp av temats globala variabler. När du ändrar globala variabler får du en överlappande effekt på alla enskilda komponenter. Du kan till exempel använda globala variabler för att ändra kantfärgen på alla komponenter i ett adaptivt formulär eller tillämpa en levande fyllningsfärg på knapparna Call to Action (CTA). Du kan:

* [Ange format för temanivåer](#theme-customization-global-level)

* [Ange format för komponentnivå](#component-based-customization)

##### Ange format för temanivåer {#theme-customization-global-level}

The `variable.scss` filen innehåller temats globala variabler. Genom att uppdatera dessa variabler kan du göra formatrelaterade ändringar på temanivå. Så här använder du format på temanivå:

1. Öppna `<your-theme-sources>/src/site/_variables.scss` fil för redigering.
1. Ändra värdet för alla egenskaper. Standardfelfärgen är t.ex. röd. Om du vill ändra felfärgen från rött till blått ändrar du färghexkoden för `$error`variabel. Till exempel, `$error: #196ee5`.

   ![Exempel: Felfärgen är blå](/help/forms/using/assets/theme-level-changes.png)

1. Spara och stäng filen.


På samma sätt kan du använda `variable.scss` för att ange teckensnittsfamilj och -typ, tema- och teckensnittsfärger, teckenstorlek, temaavstånd, felikoner, temats kantlinjeformat och fler variabler som påverkar flera adaptiva formulärkomponenter.

##### Ange format för komponentnivå {#component-based-customization}

Du kan också anpassa teckensnitt, färg, storlek och andra CSS-egenskaper för specifika komponenter i den adaptiva formulärkärnan, som knappar, kryssrutor, behållare, sidfötter och mycket annat. Genom att redigera den CSS-fil som är kopplad till den specifika komponenten kan du anpassa dess format efter din organisations varumärke. Så här anpassar du en komponents stil:

1. Öppna filen `<your-theme-sources>/src/components/<component>/<component.scss>` för redigering. Om du till exempel vill ändra teckenfärgen för knappkomponenten öppnar du `<your-theme-sources>/src/components/button/button.scss`, fil .
1. Ändra värdet enligt dina önskemål. Om du till exempel vill ändra färgen på knappkomponenten vid muspekaren till Grön, ändrar du värdet på `color: $white` -egenskapen i `cmp-adaptiveform-button__widget:hover` klass som ska hex-kod nr 12b453 eller någon annan grön nyans. Den färdiga koden ser ut så här:

   ```
    .cmp-adaptiveform-button__widget:hover {
    background: $dark-gray;
    color: #12b453;
    }
   ```


1. Spara och stäng filen.

<!--

   ![Example: Hover color set to green](/help/forms/using/assets/button-customization.png)

-->

>[!NOTE]
>
> När ett format definieras både på tema- och komponentnivå prioriteras det format som definieras på komponentnivå.

#### 3. Temat är klart för distribution {#generate-the-clientlib}

Om du vill distribuera ett tema till en AEM måste det konverteras till ett klientbibliotek. Så här konverterar du temat till ett klientbibliotek:

1. Öppna kommandotolken eller terminalfönstret.
1. Navigera till `<your-theme-sources>` mapp. Till exempel, `C:\aem-forms-theme-canvas`
1. Kör följande kommando:

   ```
      npm run create-clientlib --category=adaptiveform.theme.[yourtheme]
   ```

   Ersätt `[yourtheme]` med namnet på det anpassade temat. Om namnet på det anpassade temat till exempel är `customcanvastheme`kör du följande kommando

   ```
       npm run create-clientlib --category=adaptiveform.theme.customcanvastheme
   ```

   När kommandot har körts skapas en klientbiblioteksmapp på `themerepo\theme-clientlibs\[yourtheme]`.

   ![Generering av klientbibliotek](/help/forms/using/assets/clientlib_created.png)


   ![Klientbibliotekets plats](/help/forms/using/assets/adaptiveform.theme.easel.png)

#### 4. Använd temat i en lokal miljö {#deploy-the-theme-on-a-local-environment}

Så här distribuerar du temat till din lokala utvecklings- eller testmiljö:

1. Kopiera klientbiblioteket, som skapades i föregående avsnitt, till ditt Archetype-projekt på följande sökväg:

   `/ui.apps/src/main/content/jcr_root/apps/[AEM Archetype Project Folder]/clientlibs/<yourtheme>`

1. Öppna kommandotolken eller terminalen.
1. Navigera till rotkatalogen för ditt AEM Archetype-projekt, det projekt som används för att aktivera adaptiva Form Core-komponenter.
1. Kör följande kommando för att distribuera det anpassade temat i din miljö:

   `mvn clean install`

   ![Client Library Build](/help/forms/using/assets/mvndeploy.png)

<!--

#### 5. Test the theme with a local Adaptive Form {#test-the-theme-with-a-local-adaptive-form}

To apply and test the customized theme with an Adaptive Form:

**Apply theme while creating an Adaptive Form**

1. Log in to your AEM Forms author instance. 

1. Tap **Adobe Experience Manager** > **Forms** > **Forms & Documents**.

1. Click **Create** > **Adaptive Forms**. The wizard for creating Adaptive Form opens.

1. Select the core component template in the **Source** tab.
1. Select the theme in the **Style** tab.
1. Click **Create**.

An Adaptive Form with the selected theme is created. 

**Apply theme to an existing Adaptive Form**

1. Log in to your AEM Forms author instance. 

1. Tap **Adobe Experience Manager** > **Forms** > **Forms & Documents**.

1. Select an Adaptive Form and click Properties. 

1. For the **Theme Client Library** option, select the theme. 

1. Click **Save & Close**.

The selected theme is applied to the Adaptive Form. 
-->

#### 5. Använd ett tema i produktionsmiljön {#deploy-theme}

När du har testat temat på den lokala utvecklingsmiljön kan du fortsätta att distribuera temat till produktionsmiljöerna, inklusive både författaren och publiceringsinstanser. Så här distribuerar du temat i dina produktionsmiljöer:

1. Logga in i din AEM.
1. Öppna Pakethanteraren. Standardwebbadressen är `https://localhost:4502/crx/packmgr/index.jsp`.
1. Klicka **Överför paket** och klicka **Bläddra**.
1. Navigera till och markera `[AEM Archetype Project Folder]\all\target[appid].all-[version].zip`. Klicka **Öppna**.
1. Klicka på Installera. Upprepa steget i alla produktionsmiljöer.


När paketet har installerats är temat tillgängligt för val.

![Temaklientbibliotek](/help/forms/using/assets/themeclientlibrary.png)

>[!NOTE]
>
>
> Om du får problem med att komma åt inloggningsdialogrutan på en publiceringsinstans för att installera paketet via pakethanteraren kan du försöka med att logga in via följande URL: `http://[Publish Server URL]:[PORT]/system/console`. Detta ger dig åtkomst till att logga in på Publish-instansen, så att du kan fortsätta med installationsprocessen.

## Använda ett tema i ett anpassat formulär {#using-theme-in-adaptive-form}

Steg för att tillämpa ett tema på ett adaptivt formulär är:

1. Logga in på den lokala AEM författarinstansen.
1. Ange dina uppgifter på inloggningssidan för Experience Manager. Tryck **Adobe Experience Manager** > **Forms** > **Forms och dokument**.
1. Klicka **Skapa** > **Adaptiv Forms**.
1. Välj en adaptiv Forms Core Components-mall och klicka på **Nästa**. The **Lägg till egenskaper** visas
1. Ange **Namn** för din adaptiva form.


   >[!NOTE]
   >
   > * Som standard är `adaptiveform.theme.canvas3` -temat är valt.
   > * Du kan välja ett annat tema från **Temaklientbibliotek** listruta.

1. Klicka **Skapa**.

Adaptiva formulärteman används som en del av en adaptiv formulärmall för att definiera format när du skapar ett adaptivt formulär.

## Ta bort ett tema {#delete-a-theme}

Så här tar du bort oanvända eller oönskade teman:

1. Logga in på din Author-instans.
1. Öppna `http://[Publish Server URL]:[PORT]/crx/de/index.jsp`
1. Navigera till `apps/[AEM Archetype Project Folder]/clientlibs/[yourtheme]`.
1. Ta bort temamappen och spara ändringarna.


## Frågor och svar {#faq}

**F:** Vilken anpassning prioriteras när du gör anpassningar i en temamapp på både global nivå och komponentnivå?

**Ans:** När ett format definieras på både tema- och komponentnivå har det format som definieras på komponentnivå företräde.

**F:** Vilka åtgärder ska vidtas om det anpassade temat inte syns i **[!UICONTROL Theme Client Library]**?

**Ans:**  Om ditt anpassade tema inte visas i **[!UICONTROL Theme Client Library]** gör så här:

1. Navigera till den plats där du har lagt till ditt anpassade temaklientbibliotek. Den rekommenderade sökvägen är `/ui.apps/src/main/content/jcr_root/apps[AEM Archetype Project Folder]/clientlibs/<yourtheme>`.

1. Öppna `.content.xml` och inkludera följande metadata:

   ```
       formstheme:true
       allowproxy:true
   ```

1. Spara filen och distribuera temat igen.

## Se även

* [Skapa en grundkomponentbaserad adaptiv form](create-an-adaptive-form-core-components.md)
* [Använd regelredigeraren för att lägga till dynamiskt beteende i formulär](rule-editor.md)
* [Skapa eller anpassa teman för grundkomponentbaserade adaptiva Forms](create-or-customize-themes-for-adaptive-forms-core-components.md)
* [Skapa en mall för Core Components-baserade Adaptive Forms](template-editor.md)
* [Skapa eller lägga till ett anpassat formulär på en AEM Sites-sida eller ett Experience Fragment](create-or-add-an-adaptive-form-to-aem-sites-page.md)
* [Exempelmallar för teman och formulärdatamodeller](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/sample-themes-templates-form-data-models-core-components.html)

