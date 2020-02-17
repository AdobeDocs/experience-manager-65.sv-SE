---
title: Appen AEM Forms
seo-title: Appen AEM Forms
description: Med appen AEM Forms kan era fältarbetare använda adaptiva formulär på sina mobila enheter.
seo-description: Med appen AEM Forms kan era fältarbetare använda adaptiva formulär på sina mobila enheter.
uuid: fac976c8-b713-4492-b153-f567e7a11ceb
contentOwner: sashanka
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: e18aa345-034c-473b-b4c2-01678bb10616
translation-type: tm+mt
source-git-commit: 94472fad34fe97740e4711d2cb35beb884db52ce

---


# Introduktion till appen AEM Forms {#aem-forms-app}

## Översikt {#overview}

Med appen AEM Forms kan du synkronisera adaptiva formulär, mobilformulär och formuläruppsättningar på mobila enheter, baserat på din server. Du kan definiera arbetsflöden som är [formulärbaserade arbetsflöden i OSGi](/help/forms/using/aem-forms-workflow.md) - eller [Forms-arbetsflöden i JEE](/help/forms/using/finance-reference-site-walkthrough.md#approving-the-application). Du ansvarar t.ex. för ett bankföretag och använder AEM Forms för att hantera kundtillämpningar och kommunikation. Era kunder fyller i en blankett och skickar in den för verifiering. Om du aktiverar formuläret på mobila enheter kan dina kunder fylla i formuläret i appen AEM Forms. Du kan också hantera verifieringsarbetsflödet genom att aktivera verifieringsformuläret på mobila enheter. Din fältarbetare kan bära en mobil enhet med sig till kunden, verifiera informationen och skicka formuläret. Appen AEM Forms synkroniseras med AEM Forms-servern och hämtar formulären som är aktiverade för mobila enheter. Om programmet är offline lagras data lokalt.

Källkoden för AEM Forms-appen är tillgänglig för kunder via paketdelning. Källkodspaketet i paketresursen är tillgängligt som: `adobe-aemfd-forms-app-src-pkg-<version>.zip`.

Appen AEM Forms stöds på iOS-, Android- och Windows-enheter. Du kan installera appen AEM Forms för Android från Google Play, iOS från App Store och Windows från Windows Store.

    [ ![google_play](assets/google_play.png)](https://play.google.com/store/apps/details?id=com.adobe.aem.forms)
    
    [ ![app_store](assets/app_store.png)](https://itunes.apple.com/us/app/adobe-experience-manager-forms/id1129625976?ls=1&amp;mt=8)
    
    [ ![microsoft-badge-icon](assets/microsoft-badge-icon.png)](https://www.microsoft.com/en-us/store/p/adobe-experience-manager-forms/9nd12rlxtgtt)

Information om hur du installerar, anpassar och distribuerar programmet på iOS-, Android- eller Windows-enheter finns i [Anpassa, skapa och distribuera appen](#customize-build-distribute)AEM Forms.

## Förutsättningar {#prerequisites}

Appen AEM Forms kräver en AEM Forms-server. Användare kan återge formulär som du skapar i AEM FormsServer, fylla i dem, spara som utkast och skicka dem. Appen ansluter till servern och hämtar aktiverade formulär från den. AEM Forms-appen synkroniseras med servern och så fort formulären har lästs in i appen kan användarna arbeta offline. Om appen är offline sparas data på enheten och data synkroniseras med servern när appen är online.

### Appen AEM Forms med servrar som använder AEM Forms Workflow {#aem-forms-app-with-servers-using-aem-forms-workflow}

Om du har en AEM Forms Workflow-server kan du återge formulär som åtgärder i appen AEM Forms. Du driver t.ex. ett bankföretag och kunden fyller i en ansökan om att använda tjänsterna. Programmet är ett anpassat formulär som tar emot information från dina kunder och lagrar den som en inlämning för granskning. Administratören granskar ett program och vidarebefordrar en verifieringsbegäran till fältarbetaren. Det vidarebefordrade programmet aktiverar ett verifieringsformulär i fältarbetarens app som en uppgift. Din fältarbetare bär den mobila enheten till kunden och verifierar informationen.

### Appen AEM Forms med servrar som använder ett formulärcentrerat arbetsflöde i OSGi {#aem-forms-app-with-servers-using-forms-centric-workflow-on-osgi}

Om du har en AEM Forms-server kan du återge adaptiva formulär som AEM Inbox-program och åtgärder i AEM Forms-appen. Du driver t.ex. ett bankföretag och kunden fyller i en ansökan om att använda tjänsterna. Ansökan är kopplad till ett anpassat formulär som tar emot information från dina kunder och lagrar den som en inlämning för granskning. Administratören granskar uppgiften och godkänner verifieringsbegäran för fältarbetaren. Din fältarbetare bär den mobila enheten till kunden och verifierar informationen.

### Fristående formulär eller appen AEM Forms med servrar utan AEM Forms Workflow {#standalone-forms-or-aem-forms-app-with-servers-without-aem-forms-workflow}

En AEM Forms-server som inte använder AEM Forms Workflow är AEM Forms på OSGi eller ett fristående mobilformulär eller anpassningsbart formulär. Appen AEM Forms fungerar med implementeringen av AEM Forms i [OSGi](/help/sites-deploying/configuring-osgi.md). Formulär som du aktiverar och publicerar för appen AEM Forms är tillgängliga i din app.

Formulären hämtas till din app och är tillgängliga offline. Du driver t.ex. ett bankföretag och en kund fyller i en ansökan på er webbplats. Programmet är ett anpassat formulär som tar emot information från dina kunder och lagrar den för granskning. Administratören granskar formuläret och skapar ett verifieringsformulär i AEM-författarinstansen. Administratören aktiverar synkronisering av formuläret med appen AEM Forms och publicerar det. Om verifieringsformuläret är tillgängligt i appen AEM Forms kan fältagenten använda en mobil enhet för att verifiera kundens information. Den mobila enheten synkroniseras med servern och verifieringsformuläret läses in i appen. Din fältrepresentant kan besöka kunden, verifiera informationen, spara data som utkast eller skicka bekräftelseformuläret. Formuläret synkroniseras med servern när appen är online.

Så här synkroniserar du formuläret i appen AEM Forms:

1. Markera ett formulär i författarinstansen och klicka på **[!UICONTROL Visa egenskaper]**.

1. Klicka på **[!UICONTROL Avancerat]** på egenskapssidan.
1. Aktivera alternativet under Avancerat: **[!UICONTROL Synkronisera med AEM Forms App]** och tryck på **[!UICONTROL Save]**.

När formuläret publiceras synkroniseras programmet med servern och formuläret hämtas. Om du vill synkronisera flera formulär i författarinstansen markerar du flera formulär i formulärhanteraren och trycker på **[!UICONTROL Synkronisera med AEM Forms App]**.

## Stöd för mobila enheter {#mobile-device-support}

Se appen [AEM Forms (tidigare Mobile Workspace)](/help/forms/using/aem-forms-jee-supported-platforms.md#aem-forms-workspace-app)

## Viktiga funktioner i appen AEM Forms {#key-features-of-aem-forms-app}

### Appen AEM Forms med AEM Forms-servrar {#aem-forms-app-with-aem-forms-servers}

Du kan synkronisera din app med AEM Forms-servern och arbeta med formulär på din mobila enhet.

Med AEM Forms Workflow Server kan ett formulär kopplas till en startpunkt i en workbench-process och AEM Inbox-program. Ett AEM Inbox-program kan ha ett associerat adaptivt formulär. En startpunkt kan ha ett adaptivt formulär, ett HTML5-formulär eller en tillhörande formatuppsättning. En startpunkt kan skickas som en uppgift eller så kan uppgiften sparas som ett utkast. Mer information om skillnaderna mellan ett AEM Inbox-program och en startpunkt finns i [Åtgärder och funktioner i formulärbaserade AEM-arbetsflöden i OSGi- och AEM Forms JEE-arbetsflöden](/help/forms/using/capabilities-osgi-jee-workflows.md).

Med AEM Forms-server utan arbetsflöde för AEM Forms återges ett formulär som är aktiverat för synkronisering i appen i appen AEM Forms. Formulär är tillgängliga på fliken Formulär i appen, kan skickas eller sparas som ett utkast. Anpassningsbara formulär och mobilformulär stöds i appen.

1. **Spara en uppgift eller ett formulär som ett utkast**

   Alternativet Spara som utkast sparar en ögonblicksbild av en uppgift eller ett formulär tillsammans med ifyllda data och filer som bifogas i det associerade formuläret. Utkasten sparas på den mobila enheten och synkroniseras med AEM Forms-servern för senare hämtning.

   Se [Spara en uppgift eller ett formulär som ett utkast](/help/forms/using/save-as-draft.md).

1. **Spara formulär som mall**

   När användaren fyller i ett formulär ändras ibland inmatningen i ett fåtal fält. För sådana instanser kan du fylla i fält som kräver identiska värden i varje instans och spara formuläret eller utkastet som en mall. Varje gång du skapar en instans av mallen fylls nu de angivna fälten redan med värden som anges i mallen. Det hjälper dig att spara tid och arbete som krävs för att fylla i formuläret.

   Se [Spara formulär som mallar](/help/forms/using/save-forms-and-start-points-as-templates.md).

### Arbeta med uppgifter och formulär {#working-with-tasks-and-forms}

Du kan synkronisera din app med AEM Forms Workflow-servern och arbeta med uppgifter och formulär på din mobila enhet.

En uppgift på den mobila enheten innehåller ett adaptivt formulär, ett HTML5-formulär eller en formuläruppsättning och kan även innehålla bilagor och [sammanfattande URL](/help/forms/using/getting-task-variables-summary-url.md). Som standard placeras uppgifter som du har tilldelats i mappen **[!UICONTROL Uppgifter]** . När du arbetar med en uppgift kan du ändra uppgiften och spara ett utkast av en uppgift på AEM Forms-servern.

Ett formulär på den mobila enheten kan vara ett adaptivt formulär eller ett mobilt formulär. Formulär som har aktiverats för synkronisering i formulärappen finns i mappen Forms. Du kan synkronisera formulär som är aktiverade på AEM Forms-servern utan arbetsflöde för AEM Forms (AEM Forms on OSGi).

Se:

* [Öppna en uppgift](/help/forms/using/open-task.md)
* [Arbeta med ett formulär](/help/forms/using/working-with-form.md)

### Arbeta offline {#working-offline}

Du kan arbeta på din mobila enhet i offlineläge. Du kan logga in i programmet även om det inte finns någon nätverksanslutning och arbeta med alla formulär som synkroniserades med enheten när du var online senast. Mer information om hur du synkroniserar formulär finns i [Synkronisera appen](/help/forms/using/sync-app.md). Om du väljer att synkronisera de bilagor som är kopplade till ett formulär kan du även öppna de bifogade filerna i offlineläge. Du kan redigera formuläret, lägga till kommentarer och skicka eller spara ett formulär i offlineläge. Formuläret synkroniseras med AEM Forms-servern nästa gång du är online.

Mer information finns i [Arbeta i offlineläge](/help/forms/using/work-offline-mode.md).

### Lägga till anteckningar {#adding-annotations}

Du kan lägga till följande bifogade filer i ett formulär på din mobila enhet

* **Anteckningar**- Du kan använda funktionen Anteckningar för att lägga till ett frihandsskript eller en anteckning i formuläret. Mer information finns i [Lägga till en anteckning](/help/forms/using/add-attachments.md#adding-a-note).

* **Bild**- Appen AEM Forms innehåller en funktion som använder kamerans funktioner eller galleriet på din mobila enhet. Med den bifogade fotot kan du lägga till ett foto med det tillhörande formuläret. Mer information finns i [Lägga till ett foto](/help/forms/using/add-attachments.md#adding-a-photograph).

### Spara automatiskt {#autosave}

När en användare anger data i appen AEM Forms sparar funktionen automatiskt dem med regelbundna intervall. Funktionen för automatiskt sparande i appen AEM Forms hjälper dig att undvika dataförluster om appen stängs på grund av förhållanden som låg batterinivå.

Se [Använda automatiskt sparande i appen](/help/forms/using/autosave-data-app.md)AEM Forms.

## Skillnader mellan funktionerna i AEM Inbox och AEM Forms-appen {#differences-between-aem-inbox-and-aem-forms-app-features}

Två av de framträdande sätten att starta ett formulärcentrerat arbetsflöde är att använda [AEM Inbox](/help/forms/using/manage-applications-inbox.md) och appen AEM Forms. Funktionerna i AEM Inbox och AEM Forms-appen skiljer sig dock åt. AEM Inbox fungerar endast med [formulärcentrerade arbetsflöden](/help/forms/using/aem-forms-workflow.md) medan AEM Forms-appen fungerar med både formulärcentrerade arbetsflöden och processhantering. Mer information om skillnaderna mellan funktionerna i AEM Inbox och AEM Forms finns i [Åtgärder och funktioner i formulärbaserade AEM-arbetsflöden i OSGi- och AEM Forms JEE-arbetsflöden](/help/forms/using/capabilities-osgi-jee-workflows.md).

## Formulär som stöds {#supported-forms}

Formulärtyper som stöds i appen AEM Forms:

### Adaptiv form {#adaptive-form}

Ett anpassningsbart formulär som dynamiskt anpassar sig till användarindata stöds i appen AEM Forms. Lazy-inlästa adaptiva formulär stöds också.

### Mobilformulär {#mobile-form}

Du kan skapa formulär för mobila enheter i AEM Forms. Mobila formulär återges som HTML-formulär på mobila enheter som anpassar sig efter visningsenheter.

### Format {#formset}

Med formuläruppsättningar kan flera formulär som är kopplade till en tjänst eller process grupperas för att automatisera en affärsprocess och presenteras för slutanvändarna. I ett sådant scenario kan användarna fylla i hela uppsättningen som ett och det finns inget behov av att arkivera, skicka och spåra enskilda formulär eller processer.

>[!NOTE]
>
>Kräver AEM Forms Workflow (AEM Forms on JEE).

## Hur appen AEM Forms fungerar {#how-aem-forms-app-works}

Appen AEM Forms erbjuder en mobil lösning där fältarbetare kan arbeta med formulär som de tilldelats. Programmet cachelagrar alla data från servern och ger en effektiv användarupplevelse genom att spara allt arbete lokalt. Data från disken skickas till servern via synkroniseringsuppdateringar som är aktuella.

Appen AEM Forms är ett PhoneGap 5.0-baserat program där Backbone-modellen används effektivt för att presentera data som lagras i modellerna via vyer. Alla inbyggda åtgärder utförs via PhoneGap-plugin-program.

## Anpassa, bygga och distribuera appen AEM Forms {#customize-build-distribute}

>[!NOTE]
>
>Gäller endast om du använder källkoden för AEM Forms-appen för att skapa appen.

Appen AEM Forms är enkel att anpassa för organisationsspecifika behov. Källkoden för programmet tillhandahålls tillsammans med AEM Forms. Ni kan ändra källkoden och bygga en egen mobil personallösning. Du kan också signera appen med din egen företagsnyckel.

### Anpassa {#customize}

Du kan anpassa din app för:

**Varumärke**: Ändra programikonen, appnamnet, startbilder och sidor i appen AEM Forms. Du kan också ändra text för att lokalisera programmet för ett visst område. Mer information om anpassning av varumärket för appen AEM Forms finns i Anpassning [av](/help/forms/using/branding-customization.md)varumärkesprofilering.

**Tema**: Ändra format som färger, teckensnitt och avstånd i användargränssnittet för appen AEM Forms. Mer information finns i Anpassa [teman](/help/forms/using/theme-customization.md).

**Gester**: Ändra gester som att svepa åt höger och svepa åt vänster i användargränssnittet för appen AEM Forms. Mer information finns i [Gestanpassning](/help/forms/using/gesture-customization.md).

Mer information om hur du konfigurerar ett AEM Forms-appprojekt för anpassning finns i:

* [Konfigurera miljö för appen AEM Forms](/help/forms/using/setup-environment-mobile-workspace.md)
* [Konfigurera Visual Studio-projekt och bygg Windows-program](/help/forms/using/setup-visual-studio-project-build-installer.md)
* [Konfigurera Xcode-projekt och bygg en iOS-app](/help/forms/using/setup-xcode-project-build-installer.md)
* [Konfigurera Eclipse-projektet och bygg en Android-app](/help/forms/using/setup-eclipse-project-build-installer.md)

### Bygg och distribuera {#build-and-distribute}

Källkoden för AEM Forms-appen kan extraheras från adobe-lc-mobileworkspace-src.zip som är tillgänglig som en del av AEM Forms-appens källpaket för paketresursen.

Så här hämtar du AEM Forms-appkällan:

1. Navigera till paketresursen

   Webbadress: `https://<server>:<port>/crx/packageshare`.

1. Hämta källpaketet. När du hämtar paketet läggs det till i din AEM Forms-pakethanterare.
1. När nedladdningen är klar går du till: `https://<server>:<port>/crx/packmgr/index.jsp`, och installera `adobe-aemfd-forms-app-src-pkg-<version>.zip`.

1. Om du vill hämta paketet öppnar du det `https://<server>:<port>/crx/de/content/forms/mobileapps/src/adobe-lc-mobileworkspace-src-<version>.zip` i webbläsaren.

   Källpaketet hämtas till din enhet.

**För iOS**:

Mer information om hur du skapar en iOS-app (.ipa) finns i [Konfigurera Xcode-projektet och skapa iOS-appen](/help/forms/using/setup-xcode-project-build-installer.md).

Mer information om hur du signerar AEM Forms-appen med din provisioneringsprofil finns i [iOS Code Signing Setup, Process och Troubleshooting](https://developer.apple.com/support/code-signing/).

**För Android**:

Mer information om hur du skapar en Android-app (.apk) finns i [Konfigurera Eclipse-projektet och skapa Android-appen](/help/forms/using/setup-eclipse-project-build-installer.md).

Mer information om hur du signerar AEM Forms-appen finns i [Signera program](https://developer.android.com/tools/publishing/app-signing.html).

**För Windows**:

Mer information om hur du skapar en Windows-app (.appx) finns i [Konfigurera Visual Studio-projektet och skapa Windows-appen](/help/forms/using/setup-visual-studio-project-build-installer.md).

Mer information om hur du distribuerar appen via MDM finns i [Distribuera appen](/help/forms/using/distribute-mobile-workspace-app.md)AEM Forms. Appdistribution via MDM gäller endast iOS och Android.

## Rekommendationer om att uppgradera Mobile Workspace till appen AEM Forms {#recommendations-to-upgrade-mobile-workspace-to-aem-forms-app}

Om du uppgraderar till den senaste versionen av AEM Forms-appen ska du läsa igenom följande punkter:

* **Om du har installerat en tidigare version av appen från spelbutiken på Android** kan du uppgradera appen direkt från spelbutiken.

* **Om en tidigare version av appen har skapats och installerats med källkoden (gäller för iOS och Android)**:

   Synkronisera alla data med AEM Forms-servern innan du installerar den nya appen. När data har synkroniserats avinstallerar du den tidigare versionen av programmet och installerar den nya appen.

