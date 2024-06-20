---
title: Introduktion till hantering av formulär
description: AEM Forms har verktyg för att hantera adaptiva Forms och samhörande resurser. I den här artikeln beskrivs de viktigaste formulärhanteringsfunktionerna och elementen i användargränssnittet.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-manager, introduction
docset: aem65
exl-id: 3e063456-7f96-483d-86a3-6a414746db8a
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: Admin, User
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '1562'
ht-degree: 0%

---

# Introduktion till hantering av formulär {#introduction-to-managing-forms}

AEM [!DNL Forms] har ett förenklat men ändå kraftfullt användargränssnitt för att skapa och hantera formulär, dokument, teman, bokstäver, dokumentfragment, dataordlistor och relaterade resurser. Den hjälper till att hantera hela livscykeln för formulär, dokument och relaterade resurser - från utvecklarens dator till att erbjuda dem på en portalserver för slutanvändarna. Du kan använda AEM [!DNL Forms] användargränssnitt till:

* AEM [!DNL Forms] komponenter
* AEM [!DNL Forms] konfigurationer

>[!NOTE]
>
>Mer information om andra AEM verktyg och alternativ finns i [Redigering](/help/sites-authoring/author.md).

## Öppna AEM Forms-komponenter {#access-aem-forms-components}

Tillsammans med alternativ för att skapa formulär, dokument och relaterade resurser AEM alternativ för att skapa webbplatser, resurser, hantera en AEM och mycket annat. Du kan klicka på ![adobeexperienceManager](assets/adobeexperiencemanager.png) Experience Manager logotyp för att navigera till alla tillgängliga verktyg. Tillsammans med länkar till konsolerna för andra komponenter innehåller den även länkar för AEM [!DNL Forms]. Navigera till AEM [!DNL Forms]klickar du på Experience Manager-logotypen ![adobeexperienceManager](assets/adobeexperiencemanager.png) > navigering ![kompass](assets/compass.png) > **[!UICONTROL Forms]**. Länkar till följande konsoler visas:

* Forms och dokument
* Teman
* Bokstäver
* Dokumentfragment
* Dataordlistor

  ![AEM Forms Console](assets/aem_forms_console_new.png)

### Forms och dokument  {#forms-documents}

Forms &amp; Documents innehåller alternativ för att skapa interaktiv kommunikation, adaptiva formulär, adaptiva formulärfragment och formuläruppsättningar. Endast för AEM [!DNL Forms] i JEE-format kan Forms &amp; Documents importera filer från lokala lager och synkronisera AEM [!DNL Forms] resurser med Workbench.

Knappen Skapa är startpunkten för processen att skapa eller överföra AEM [!DNL Forms] resurs. Här finns alternativ för att skapa:

* **Interaktiv kommunikation**: En interaktiv kommunikation är en skräddarsydd, interaktiv och enhetsvänlig, HTML-baserad digital korrespondens, ett kontoutdrag eller dokument. Interaktiv kommunikation är lyhörd i naturen och ändrar layout och design automatiskt baserat på användarenhet och inställningar. Mer information finns i [Översikt över interaktiv kommunikation](/help/forms/using/interactive-communications-overview.md)

* **Adaptiv form:** En adaptiv form är en engagerande och responsiv form. Du kan skapa ett anpassat formulär som dynamiskt anpassar sig till användarens indata genom att lägga till eller ta bort formuläravsnitt baserat på användarens svar, enhet eller arbetsmiljö. The [Introduktion till utveckling av anpassningsbara formulär](../../forms/using/introduction-forms-authoring.md) i artikeln finns detaljerad information om de adaptiva formulären.

* **Adaptivt formulärfragment:** Alla formulär har utformats för ett specifikt ändamål, men det finns några vanliga segment i de flesta formulär, till exempel för att ge personliga uppgifter som namn och adress, familjeinformation, inkomstinformation och så vidare. Du kan skapa en enskild resurs för sådana avsnitt. Dessa återanvändbara, fristående segment kallas adaptiva formulärfragment. Mer information finns i [adaptiva formulärfragment](../../forms/using/adaptive-form-fragments.md) artikel.

* **Formuläruppsättning:** En formuläruppsättning är en samling HTML5-formulär som grupperats tillsammans och presenteras som en enda formuläruppsättning för slutanvändarna. När användarna börjar fylla i en formuläruppsättning, överförs formulären smidigt från ett formulär till ett annat. Användaren kan sedan skicka alla blanketter, som en enhet, med bara ett klick. Mer information finns i [Formuläruppsättning i AEM Forms](../../forms/using/formset-in-aem-forms.md).

* **Mapp:** AEM [!DNL Forms] -användargränssnittet använder mappar för att ordna resurser. Det har stöd för två typer av mappar:

   * **Allmän mapp:** De här mapparna används för resurser som skapats i AEM [!DNL Forms] användargränssnitt. De här mapparna har ingen strikt mappstruktur. Du kan byta namn på, skapa undermappar och lagra adaptiva formulär, interaktiv kommunikation, adaptiva formulärfragment, formulärmallar (XDP), PDF forms, dokument och relaterade resurser i dessa mappar.
   * **Forms Workflow:** Forms arbetsflödesmappar skapas när Workbench-processer (LiveCyclena arkiv) migreras och synkroniseras med AEM [!DNL Forms] användargränssnitt. Det är inte tillåtet att byta namn, skapa en undermapp, skapa en interaktiv kommunikation, ett adaptivt formulärfragment eller en interaktiv kommunikation. Det är inte heller tillåtet att ta bort en versionsmapp eller skapa och överföra ett adaptivt formulär, ett adaptivt formulärfragment eller en interaktiv kommunikation parallellt med versionsmappen.

  ![mappar](assets/folders.png)

  **S.** Allmän mapp **B.** Forms Workflow

På Forms- och dokumentpanelen finns även alternativ för att:

* **Importera filer från lokal lagring:** Du kan importera PDF forms och dokument, formulärmallar (XFA-formulär) och andra resurser (bild- och XML-schema för XSD-filer). Stegvisa instruktioner finns i [Importera och exportera resurser till AEM Forms](../../forms/using/import-export-forms-templates.md).
* **Synkronisera AEM Forms-resurser med Workbench:** Du kan använda alternativet Filer från Workbench för att synkronisera resurser mellan AEM Forms användargränssnitt och Workbench. Det garanterar att alla resurser är tillgängliga i AEM [!DNL Forms] -användargränssnittet och Workbenchs urval av resurser i crx-databaser.

### Teman  {#themes}

Ett tema innehåller formatinformation för komponenter och paneler. Teman har en oberoende identitet. Du kan återanvända ett tema på flera adaptiva formulär. Du kan ange format för en komponent eller ändra CSS-egenskaper för olika komponenter som används i alla formulär. Format innehåller egenskaper som bakgrundsfärger, lägesfärger, genomskinlighet och storlek. Du kan spara anpassningar i ett tema och portera dem till komponenter i formuläret som en förinställning. När du lägger till temat i formuläret återspeglas det angivna formatet i motsvarande komponenter i formuläret. Med AEM 6.2 [!DNL Forms]kan du skapa teman och använda dem i formulären.

Mer information om hur du skapar och använder teman finns i [Teman i AEM Forms](../../forms/using/themes.md).

### Bokstäver  {#letters}

En AEM [!DNL Forms] brev är en säker, personaliserad och interaktiv korrespondens. Du kan använda AEM [!DNL Forms] att snabbt sammanställa bokstäver (även kallade korrespondenser) från både förgodkänt och skräddarsytt material i en smidig process.

Mer information om hur du skapar och använder bokstäver finns i [Skapa brev](../../forms/using/create-letter.md).

### Dokumentfragment {#document-fragments}

Dokumentfragment är återanvändbara delar eller komponenter av en korrespondens som du kan använda för att skapa brev. Dokumentfragmenten är av typen text, lista, villkor och layoutfragment. Mer information om hur du skapar och använder dokumentfragment finns i [skapa dokumentfragment](/help/forms/using/document-fragments.md).

### Dataordlistor {#data-dictionaries}

Vanligtvis behöver företagsanvändare inte känna till metadata-representationer som XSD (XML-schema) eller Java-klasser. De kräver dock vanligtvis åtkomst till dessa datastrukturer och attribut för att kunna bygga lösningar. AEM [!DNL Forms] använder dataordlista som gör det möjligt för affärsanvändare att använda information från backend-datakällor utan att känna till teknisk information om sina underliggande datamodeller.

Mer information om hur du skapar och använder dataordlistor finns i Skapa [dataordlisteartikel](../../forms/using/data-dictionary.md)

## Åtkomst AEM [!DNL Forms] Konfigurationer {#accessing-aem-forms-configurations}

AEM verktygspanelen innehåller verktyg för olika komponenter. Om du vill navigera till AEM Forms-specifika verktyg klickar du på Experience Manager-logotypen ![adobeexperienceManager](assets/adobeexperiencemanager.png) > verktyg ![hammare](assets/hammer.png) > **[!UICONTROL Forms]**. Verktyg för följande funktioner visas:

* **Konfigurera bevakad mapp:** En administratör kan konfigurera en nätverksmapp, en så kallad bevakad mapp, så att en förkonfigurerad åtgärd startas och filen ändras när en användare placerar en fil (till exempel en PDF-fil) i den bevakade mappen. Mer information finns i [Skapa och konfigurera en bevakad mapp](/help/forms/using/creating-configure-watched-folder.md).
* **Konfigurera Forms App Offline Service:** AEM [!DNL Forms] offline-tjänsten för app cachelagrar sökvägarna eller URL:erna för resurserna som används i ett formulär. Cachelagring av sökvägar eller URL:er för resurserna som används i ett formulär förbättrar prestandan på serversidan. Information om hur du konfigurerar offlinekomponenten på serversidan för AEM Forms-programmet finns i [Arbeta i offline-läge](/help/forms/using/work-offline-mode.md).

  ![AEM Forms](assets/aem_forms_tools_new.png)

* **Konfigurera PDF Generator:** En administratör kan konfigurera AEM [!DNL Forms] PDF Generator, lägg till användarkonton och importera eller exportera konfiguration till PDF Generator.
* **Publish Correspondence Management Assets:** AEM [!DNL Forms] Med kan du publicera alla bokstäver, dokumentfragment, datafält och relaterade beroenden från en författarinstans samtidigt. De publicerade resurserna innehåller alla Correspondence Management-resurser och relaterade beroenden. Mer information finns i [Publicera och avpublicera formulär och dokument](../../forms/using/publishing-unpublishing-forms.md#publishallthecorrespondencemanagementassets).
* **Exportera Correspondence Management-resurser:** Du kan hämta alla Correspondence Management-resurser och relaterade beroenden som ett paket från en AEM [!DNL Forms] -instans. Detaljerade anvisningar finns i [Importera och exportera resurser till AEM Forms](../../forms/using/import-export-forms-templates.md#importandexportassetsincorrespondencemanagement)

## Gemensamma element i användargränssnittet {#commonelements}

* **Vänster räl:** Du kan klicka på ikonen för den vänstra listen ![railleftpng](assets/railleftpng.png) för att visa funktionerna för tidslinje och referenser i AEM [!DNL Forms].

   * **Tidslinje:** Du kan lägga till och visa kommentarer för en resurs som är tillgänglig för granskning på tidslinjen. Detaljerade anvisningar finns i [Skapa och hantera granskningar av resurser i formulär](../../forms/using/create-reviews-forms.md).
   * **Referenser:** En AEM [!DNL Forms] resurs kan användas i flera AEM [!DNL Forms] resurser. Ett dokumentfragment kan till exempel användas i flera bokstäver. Referenser är en lista över resurser (andra former eller resurser) som den valda resursen används i och även en lista över andra resurser som den valda resursen använder.

* **Bläddringar:** En Breadcrumb representerar titeln på den aktuella konsolen eller mappen. Du kan klicka på alternativet Bläddra om du vill navigera mellan mappnivån som är högst upp i hierarkin.
* **Visa växlare:** Du kan klicka på ikonen Visa väljare ![visningslista](assets/viewlist.png) eller ![vykort](assets/viewcard.png) för att snabbt växla mellan list- och kortvyn. Mer information om gemensamma komponenter i användargränssnittet finns i [Redigering](/help/sites-authoring/author.md).
* **Sök:** Sökalternativet ![sök](assets/search.png) ger möjlighet att snabbt hitta och gå till det innehåll och de verktyg du behöver. Skriv namnet på innehållet eller produktfunktionen och välj bland förslagen. Skriv t.ex. &quot;Dokument&quot; för att snabbt hitta och navigera till **[!UICONTROL Forms & Documents]** eller konsolen Dokumentfragment. Mer information om sökning finns i AEM 6.2 [sök](/help/sites-authoring/search.md) artikel

* **Verktygsfältet Åtgärder**: När du väljer en resurs visas åtgärdsverktygsfältet ovanför listan med resurser. Den innehåller alla hanteringsverktyg för den valda resursen. Du kan hålla muspekaren över en verktygsikon om du vill visa verktygstipset som beskriver dess funktioner

>[!NOTE]
>
>När en användare utför en sökning på en konsol med Forms &amp; Documents innehåller spåret bara **Filter och alternativ**. Du kan använda Filter och alternativ för avancerad sökning.

* **Verktygsfältet Åtgärder**: När du väljer en resurs visas åtgärdsverktygsfältet ovanför listan med resurser. Den innehåller alla hanteringsverktyg för den valda resursen. Du kan hålla muspekaren över en verktygsikon om du vill visa verktygstipset som beskriver dess funktioner

  ![Åtgärdsverktygsfältet för ett anpassat formulär](assets/action_toolbar_new.png)

  Åtgärdsverktygsfältet för ett anpassat formulär
