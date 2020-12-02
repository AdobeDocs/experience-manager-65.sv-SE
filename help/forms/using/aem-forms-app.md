---
title: AEM Forms
seo-title: AEM Forms
description: Med AEM Forms app kan fältarbetarna använda adaptiva formulär på sina mobila enheter.
seo-description: Med AEM Forms app kan fältarbetarna använda adaptiva formulär på sina mobila enheter.
uuid: fac976c8-b713-4492-b153-f567e7a11ceb
contentOwner: sashanka
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: e18aa345-034c-473b-b4c2-01678bb10616
translation-type: tm+mt
source-git-commit: af326f2d2b278fe36df05afc8c172f74c99a064c
workflow-type: tm+mt
source-wordcount: '2440'
ht-degree: 0%

---


# Introduktion till AEM Forms-programmet {#aem-forms-app}

## Översikt {#overview}

Med AEM Forms-appen kan du synkronisera adaptiva formulär, mobilformulär och formuläruppsättningar på mobila enheter, baserat på din server. Du kan definiera arbetsflöden som är [Forms-baserade arbetsflöden i OSGi](/help/forms/using/aem-forms-workflow.md) eller Forms-arbetsflöden i JEE. Du ansvarar t.ex. för ett bankföretag och använder AEM Forms för att hantera kundtillämpningar och kommunikation. Era kunder fyller i en blankett och skickar in den för verifiering. Om du aktiverar formuläret på mobila enheter kan dina kunder fylla i formuläret i AEM Forms-appen. Du kan också hantera verifieringsarbetsflödet genom att aktivera verifieringsformuläret på mobila enheter. Din fältarbetare kan bära en mobil enhet med sig till kunden, verifiera informationen och skicka formuläret. AEM Forms-appen synkroniseras med AEM Forms-servern och hämtar de formulär som är aktiverade för mobila enheter. Om programmet är offline lagras data lokalt.

Källkoden för AEM Forms-appen är tillgänglig för kunder via Software Distribution. Källkodspaketet i Programvarudistribution är tillgängligt som: `adobe-aemfd-forms-app-src-pkg-<version>.zip`.

AEM Forms-appen stöds på iOS-, Android- och Windows-enheter. Du kan installera AEM Forms-appen för Android från Google Play, iOS från App Store och Windows från Windows Store.

    [ ![google_play](assets/google_play.png)](https://play.google.com/store/apps/details?id=com.adobe.aem.forms)
    
    [ ![app_store](assets/app_store.png)](https://itunes.apple.com/us/app/adobe-experience-manager-forms/id1129625976?ls=1&amp;mt=8)
    
    [ ![microsoft-badge-icon](assets/microsoft-badge-icon.png)](https://www.microsoft.com/en-us/store/p/adobe-experience-manager-forms/9nd12rlxtgtt)

Information om hur du installerar, anpassar och distribuerar programmet på iOS-, Android- eller Windows-enheter finns i [Anpassa, skapa och distribuera AEM Forms-programmet](#customize-build-distribute).

## Förutsättningar {#prerequisites}

AEM Forms kräver en AEM Forms-server. Användare kan återge formulär som du skapar i AEM Forms
server, fyll i dem, spara som utkast och skicka dem. Appen ansluter till servern och hämtar aktiverade formulär från den. AEM Forms-appen synkroniseras med servern och så fort formulären har lästs in i appen kan användarna arbeta offline. Om appen är offline sparas data på enheten och data synkroniseras med servern när appen är online.

### AEM Forms-app med servrar som använder AEM Forms Workflow {#aem-forms-app-with-servers-using-aem-forms-workflow}

Om du har en AEM Forms Workflow-server kan du återge formulär som åtgärder i AEM Forms-appen. Du driver t.ex. ett bankföretag och kunden fyller i en ansökan om att använda tjänsterna. Programmet är ett anpassat formulär som tar emot information från dina kunder och lagrar den som en inlämning för granskning. Administratören granskar ett program och vidarebefordrar en verifieringsbegäran till fältarbetaren. Det vidarebefordrade programmet aktiverar ett verifieringsformulär i fältarbetarens app som en uppgift. Din fältarbetare bär den mobila enheten till kunden och verifierar informationen.

### AEM Forms-app med servrar som använder Forms-centrerade arbetsflöden på OSGi {#aem-forms-app-with-servers-using-forms-centric-workflow-on-osgi}

Om du har en AEM Forms-server kan du återge adaptiva formulär som AEM Inkorgsprogram och åtgärder i AEM Forms-appen. Du driver t.ex. ett bankföretag och kunden fyller i en ansökan om att använda tjänsterna. Ansökan är kopplad till ett anpassat formulär som tar emot information från dina kunder och lagrar den som en inlämning för granskning. Administratören granskar uppgiften och godkänner verifieringsbegäran för fältarbetaren. Din fältarbetare bär den mobila enheten till kunden och verifierar informationen.

### Fristående formulär eller AEM Forms-program med servrar utan AEM Forms Workflow {#standalone-forms-or-aem-forms-app-with-servers-without-aem-forms-workflow}

En AEM Forms-server som inte använder AEM Forms Workflow är AEM Forms på OSGi eller ett fristående mobilformulär eller anpassningsbart formulär. AEM Forms-appen fungerar med din AEM Forms-implementering på [OSGi](/help/sites-deploying/configuring-osgi.md). Forms som du aktiverar och publicerar för AEM Forms-appen finns i appen.

Formulären hämtas till din app och är tillgängliga offline. Du driver t.ex. ett bankföretag och en kund fyller i en ansökan på er webbplats. Programmet är ett anpassat formulär som tar emot information från dina kunder och lagrar den för granskning. Administratören granskar formuläret och skapar ett verifieringsformulär AEM författarinstansen. Administratören aktiverar synkronisering av formuläret med AEM Forms-appen och publicerar det. Om verifieringsformuläret finns i AEM Forms-appen kan fältagenten använda en mobilenhet för att verifiera kundens information. Den mobila enheten synkroniseras med servern och verifieringsformuläret läses in i appen. Din fältrepresentant kan besöka kunden, verifiera informationen, spara data som utkast eller skicka bekräftelseformuläret. Formuläret synkroniseras med servern när appen är online.

Så här synkroniserar du formuläret i AEM Forms-appen:

1. Markera ett formulär i författarinstansen och klicka på **[!UICONTROL View Properties]**.

1. Klicka på **[!UICONTROL Advanced]** på egenskapssidan.
1. Aktivera alternativet under Avancerat: **[!UICONTROL Sync with AEM Forms App]** och tryck på **[!UICONTROL Save]**.

När formuläret publiceras synkroniseras programmet med servern och formuläret hämtas. Om du vill synkronisera flera formulär i författarinstansen markerar du flera formulär i formulärhanteraren och trycker på **[!UICONTROL Sync with AEM Forms App]**.

## Stöd för mobila enheter {#mobile-device-support}

Se [AEM Forms-app (tidigare Mobile Workspace)](/help/forms/using/aem-forms-jee-supported-platforms.md#aem-forms-workspace-app)

## Viktiga funktioner i AEM Forms {#key-features-of-aem-forms-app}

### AEM Forms-app med AEM Forms-servrar {#aem-forms-app-with-aem-forms-servers}

Du kan synkronisera din app med AEM Forms-servern och arbeta med formulär på din mobila enhet.

Med AEM Forms Workflow Server kan ett formulär kopplas till en startpunkt i en workbench-process och AEM Inbox-program. Ett AEM Inkorgsprogram kan ha ett associerat adaptivt formulär. En startpunkt kan ha ett adaptivt formulär, ett HTML5-formulär eller en tillhörande formatuppsättning. En startpunkt kan skickas som en uppgift eller så kan uppgiften sparas som ett utkast. Mer information om skillnaderna mellan ett AEM Inkorgsprogram och en startpunkt finns i [Åtgärder och funktioner för formulärbaserade AEM arbetsflöden i OSGi- och AEM Forms JEE-arbetsflöden](capabilities-osgi-jee-workflows.md).

Med en AEM Forms-server utan AEM Forms-arbetsflöde återges ett formulär som är aktiverat för synkronisering i appen i AEM Forms-appen. Forms finns på fliken Forms i programmet, kan skickas eller sparas som ett utkast. Anpassningsbara formulär och mobilformulär stöds i appen.

1. **Spara en uppgift eller ett formulär som ett utkast**

   Alternativet Spara som utkast sparar en ögonblicksbild av en uppgift eller ett formulär tillsammans med ifyllda data och filer som bifogas i det associerade formuläret. Utkasten sparas på den mobila enheten och synkroniseras med AEM Forms-servern så att du kan hämta dem senare.

   Se [Spara en uppgift eller ett formulär som ett utkast](/help/forms/using/save-as-draft.md).

1. **Spara formulär som mall**

   När användaren fyller i ett formulär ändras ibland inmatningen i ett fåtal fält. För sådana instanser kan du fylla i fält som kräver identiska värden i varje instans och spara formuläret eller utkastet som en mall. Varje gång du skapar en instans av mallen fylls nu de angivna fälten redan med värden som anges i mallen. Det hjälper dig att spara tid och arbete som krävs för att fylla i formuläret.

   Se [Spara formulär som mallar](/help/forms/using/save-forms-and-start-points-as-templates.md).

### Arbeta med aktiviteter och formulär {#working-with-tasks-and-forms}

Du kan synkronisera din app med AEM Forms Workflow Server och arbeta med uppgifter och formulär på din mobila enhet.

En åtgärd på den mobila enheten innehåller ett anpassat formulär, ett HTML5-formulär eller en formuläruppsättning och kan även innehålla bifogade filer och [sammanfattande URL](/help/forms/using/getting-task-variables-summary-url.md). Som standard placeras uppgifter som du har tilldelats i mappen **[!UICONTROL Tasks]**. När du arbetar med en uppgift kan du ändra uppgiften och spara ett utkast av en uppgift på AEM Forms-servern.

Ett formulär på den mobila enheten kan vara ett adaptivt formulär eller ett mobilt formulär. Forms som är aktiverat för synkronisering i formulärappen finns i Forms-mappen. Du kan synkronisera formulär som är aktiverade på AEM Forms-servern utan AEM Forms-arbetsflöde (AEM Forms på OSGi).

Se:

* [Öppna en uppgift](/help/forms/using/open-task.md)
* [Arbeta med ett formulär](/help/forms/using/working-with-form.md)

### Arbetar offline {#working-offline}

Du kan arbeta på din mobila enhet i offlineläge. Du kan logga in i programmet även om det inte finns någon nätverksanslutning och arbeta med alla formulär som synkroniserades med enheten när du var online senast. Mer information om hur du synkroniserar formulär finns i [Synkronisera appen](/help/forms/using/sync-app.md). Om du väljer att synkronisera de bilagor som är kopplade till ett formulär kan du även öppna de bifogade filerna i offlineläge. Du kan redigera formuläret, lägga till kommentarer och skicka eller spara ett formulär i offlineläge. Formuläret synkroniseras med AEM Forms-servern nästa gång du är online.

Mer information finns i [Arbeta i offlineläge](/help/forms/using/work-offline-mode.md).

### Lägga till anteckningar {#adding-annotations}

Du kan lägga till följande bifogade filer i ett formulär på din mobila enhet

* **Anteckningar** - Du kan använda funktionen Anteckningar för att lägga till ett frihandsskript eller en anteckning i formuläret. Mer information finns i [Lägga till en anteckning](/help/forms/using/add-attachments.md#adding-a-note).

* **Bild** - AEM Forms-appen innehåller en funktion som använder kamerans funktioner eller galleriet på din mobila enhet. Med den bifogade fotot kan du lägga till ett foto med det tillhörande formuläret. Mer information finns i [Lägga till ett foto](/help/forms/using/add-attachments.md#adding-a-photograph).

### Spara automatiskt {#autosave}

När en användare matar in data i AEM Forms-appen sparar funktionen automatiskt dem med regelbundna intervall. Autosparfunktionen i AEM Forms-appen hjälper dig att undvika dataförluster om appen stängs på grund av förhållanden som låg batterinivå.

Se [Använda automatiskt sparande i AEM Forms-app](/help/forms/using/autosave-data-app.md).

## Skillnader mellan funktionerna AEM Inkorgen och AEM Forms-appen {#differences-between-aem-inbox-and-aem-forms-app-features}

Två av de framträdande sätten att starta ett Forms-centrerat arbetsflöde är att använda [AEM Inbox](/help/forms/using/manage-applications-inbox.md) och AEM Forms-appen. Funktionerna i AEM Inbox och AEM Forms App skiljer sig dock åt. AEM Inkorg fungerar endast med [Forms-centrerade arbetsflöden](/help/forms/using/aem-forms-workflow.md) medan AEM Forms-appen fungerar med både Forms-centrerade arbetsflöden och processhantering. Mer information om skillnaderna mellan AEM Inbox- och AEM Forms-appfunktioner finns i [Åtgärder och funktioner i formulärbaserade AEM arbetsflöden i OSGi- och AEM Forms JEE-arbetsflöden](capabilities-osgi-jee-workflows.md).

## Formulär som stöds {#supported-forms}

Formulärtyper som stöds i AEM Forms-appen:

### Adaptiv form {#adaptive-form}

Ett anpassningsbart formulär som dynamiskt anpassar sig till användarindata stöds i AEM Forms-appen. Lazy-inlästa adaptiva formulär stöds också.

### Mobilformulär {#mobile-form}

Du kan skapa formulär för mobila enheter i AEM Forms. Mobila formulär återges som HTML-formulär på mobila enheter som anpassar sig efter visningsenheter.

### Formuppsättning {#formset}

Med formuläruppsättningar kan flera formulär som är kopplade till en tjänst eller process grupperas för att automatisera en affärsprocess och presenteras för slutanvändarna. I ett sådant scenario kan användarna fylla i hela uppsättningen som ett och det finns inget behov av att arkivera, skicka och spåra enskilda formulär eller processer.

>[!NOTE]
>
>Kräver AEM Forms Workflow (AEM Forms on JEE).

## Så här fungerar AEM Forms-appen {#how-aem-forms-app-works}

AEM Forms-appen är en mobil lösning där fältarbetare kan arbeta med formulär som de tilldelats. Programmet cachelagrar alla data från servern och ger en effektiv användarupplevelse genom att spara allt arbete lokalt. Data från disken skickas till servern via synkroniseringsuppdateringar som är aktuella.

AEM Forms är ett PhoneGap 5.0-baserat program där Backbone-modellen används effektivt för att presentera data som lagras i modellerna via vyer. Alla inbyggda åtgärder utförs via PhoneGap-plugin-program.

## Anpassa, bygg och distribuera AEM Forms-appen {#customize-build-distribute}

>[!NOTE]
>
>Gäller endast om du använder källkoden för AEM Forms-appen för att skapa appen.

AEM Forms-appen är enkel att anpassa för organisationsspecifika behov. Programmets källkod medföljer AEM Forms. Ni kan ändra källkoden och bygga en egen mobil personallösning. Du kan också signera appen med din egen företagsnyckel.

### Anpassa {#customize}

Du kan anpassa din app för:

**Varumärke**: Ändra programikonen, appnamnet, startbilder och sidor i AEM Forms-appen. Du kan också ändra text för att lokalisera programmet för ett visst område. Mer information om anpassning av varumärket för AEM Forms finns i [Anpassning av varumärken](/help/forms/using/branding-customization.md).

**Tema**: Ändra format som färger, teckensnitt och mellanrum i AEM Forms appgränssnitt. Mer information finns i [Temaanpassning](/help/forms/using/theme-customization.md).

**Gester**: Ändra gester som att svepa åt höger och svepa åt vänster i AEM Forms appanvändargränssnitt. Mer information finns i [Gestanpassning](/help/forms/using/gesture-customization.md).

Mer information om hur du konfigurerar ett AEM Forms-appprojekt för anpassning finns i:

* [Konfigurera miljö för AEM Forms-program](/help/forms/using/setup-environment-mobile-workspace.md)
* [Konfigurera Visual Studio-projekt och bygg Windows-program](/help/forms/using/setup-visual-studio-project-build-installer.md)
* [Konfigurera Xcode-projekt och bygg en iOS-app](/help/forms/using/setup-xcode-project-build-installer.md)
* [Konfigurera Eclipse-projektet och bygg en Android-app](/help/forms/using/setup-eclipse-project-build-installer.md)

### Skapa och distribuera {#build-and-distribute}

Källkoden för AEM Forms-appen kan extraheras från `adobe-lc-mobileworkspace-src.zip` som är tillgänglig som en del av AEM Forms appkällpaket för programdistribution.

Så här hämtar du programkällan för AEM Forms:

1. Öppna [Programvarudistribution](https://experience.adobe.com/downloads). Du behöver en Adobe ID för att logga in på Software Distribution.
1. Tryck på **[!UICONTROL Adobe Experience Manager]** som finns i rubrikmenyn.
1. I avsnittet **[!UICONTROL Filters]**:
   1. Välj **[!UICONTROL Forms]** i listrutan **[!UICONTROL Solution]**.
   2. Välj version och typ för paketet. Du kan också använda alternativet **[!UICONTROL Search Downloads]** för att filtrera resultaten.
1. Tryck på det paketnamn som gäller för ditt operativsystem, välj **[!UICONTROL Accept EULA Terms]** och tryck på **[!UICONTROL Download]**.
1. Öppna [Pakethanteraren](https://docs.adobe.com/content/help/en/experience-manager-65/administering/contentmanagement/package-manager.html) och klicka på **[!UICONTROL Upload Package]** för att överföra paketet.
1. Markera paketet och klicka på **[!UICONTROL Install]**.

**För iOS**:

Mer information om hur du skapar en iOS-app (.ipa) finns i [Konfigurera Xcode-projektet och skapa iOS-appen](/help/forms/using/setup-xcode-project-build-installer.md).

Mer information om hur du signerar AEM Forms-appen med din provisioneringsprofil finns i [iOS Code Signing Setup, Process och Troubleshooting](https://developer.apple.com/support/code-signing/).

**För Android**:

Mer information om hur du skapar en Android-app (.apk) finns i [Konfigurera Eclipse-projektet och skapa Android-appen](/help/forms/using/setup-eclipse-project-build-installer.md).

Mer information om hur du signerar AEM Forms-appen finns i [Signera program](https://developer.android.com/tools/publishing/app-signing.html).

**För Windows**:

Mer information om hur du skapar en Windows-app (.appx) finns i [Konfigurera Visual Studio-projektet och skapa Windows-appen](/help/forms/using/setup-visual-studio-project-build-installer.md).

Mer information om hur du distribuerar appen via MDM finns i [Distribuera AEM Forms-app](/help/forms/using/distribute-mobile-workspace-app.md). Appdistribution via MDM gäller endast iOS och Android.

## Recommendations för att uppgradera Mobile Workspace till AEM Forms-appen {#recommendations-to-upgrade-mobile-workspace-to-aem-forms-app}

Om du uppgraderar till den senaste versionen av AEM Forms ska du läsa igenom följande:

* **Om du har installerat en tidigare version av appen från spelbutiken på**
Android kan du uppgradera appen direkt från spelbutiken.

* **Om en tidigare version av appen har skapats och installerats med källkoden (gäller för iOS och Android)**:

   Synkronisera alla data med AEM Forms-servern innan du installerar det nya programmet. När data har synkroniserats avinstallerar du den tidigare versionen av programmet och installerar den nya appen.

