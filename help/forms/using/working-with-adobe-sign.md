---
title: Använda Adobe Sign i ett anpassat formulär
seo-title: Använda Adobe Sign i ett anpassat formulär
description: Möjliggör arbetsflöden för e-signaturer (Adobe Sign) för ett anpassningsbart formulär för att automatisera signeringsarbetsflöden, förenkla processer för enstaka signaturer och för att signera formulär elektroniskt från mobila enheter.
seo-description: Möjliggör arbetsflöden för e-signaturer (Adobe Sign) för ett anpassningsbart formulär för att automatisera signeringsarbetsflöden, förenkla processer för enstaka signaturer och för att signera formulär elektroniskt från mobila enheter.
uuid: cc3012ed-c318-4529-9adc-61aa5b5761a0
contentOwner: khsingh
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: f79828d8-2230-4477-8ffa-eeb6a0413acd
docset: aem65
translation-type: tm+mt
source-git-commit: 14975f409a0e17183b3da6bdc5a42c8073080108

---


# Använda Adobe Sign i ett anpassat formulär{#using-adobe-sign-in-an-adaptive-form}

Adobe Sign möjliggör e-signaturarbetsflöden för anpassningsbara formulär. E-signaturer förbättrar arbetsflödena för att bearbeta dokument inom juridik, försäljning, löneadministration, personaladministration och andra områden.

I ett typiskt Adobe Sign och anpassningsbara formulär fyller en användare i ett anpassat formulär som kan användas för en tjänst. Till exempel kräver en ansökan om inteckning och kreditkort juridiska signaturer från alla låntagare och medsökande. Om du vill aktivera arbetsflöden för elektroniska signaturer för liknande scenarier kan du integrera Adobe Sign med AEM Forms. Några exempel till är:

* Slut avtal från vilken enhet som helst med fullt automatiserade processer för förslag, offerter och kontrakt.
* Slutför HR-processerna snabbare och ge medarbetarna de digitala upplevelserna.
* Minska kontraktscyklerna och anlita era leverantörer snabbare.
* Skapa digitala arbetsflöden som automatiserar vanliga processer.

Adobe Sign-integrering med AEM Forms har stöd för:

* Arbetsflöden för signering för en och flera användare
* Sekventiella och samtidiga signeringsarbetsflöden
* Underteckna i form och i form
* Signera formulär som anonym eller inloggad användare
* Dynamiska signeringsprocesser (integration med arbetsflödet i AEM Forms)
* Autentisering via kunskapsbas, telefon och sociala profiler

## Förutsättningar {#prerequisites}

Innan du använder Adobe Sign i ett anpassat formulär:

* Kontrollera att molntjänsten AEM Forms är konfigurerad att använda Adobe Sign. Mer information finns i [Integrera Adobe Sign med AEM-formulär](../../forms/using/adobe-sign-integration-adaptive-forms.md).
* Håll listan med signerare klar. Du måste ange minst en e-postadress för varje signerare.

## Konfigurera Adobe Sign för ett anpassat formulär {#configure-adobe-sign-for-an-adaptive-form}

Utför följande steg för att konfigurera Adobe Sign för ett anpassat formulär:

1. [Redigera anpassade formuläregenskaper för Adobe Sign](../../forms/using/working-with-adobe-sign.md#enableadobesign)
1. [Lägga till Adobe Sign-fält i ett anpassat formulär](../../forms/using/working-with-adobe-sign.md#addadobesignfieldstoanadaptiveform)
1. [Aktivera Adobe Sign för ett anpassat formulär](../../forms/using/working-with-adobe-sign.md#enableadobsignforanadaptiveform)
1. [Välj Adobe Sign Cloud-tjänsten för ett anpassat formulär](../../forms/using/working-with-adobe-sign.md#selectadobesigncloudserviceforanadaptiveform)

1. [Lägga till Adobe Sign-signerare i ett anpassat formulär](../../forms/using/working-with-adobe-sign.md#addsignerstoanadaptiveform)
1. [Välj Skicka åtgärd för ett anpassat formulär](../../forms/using/working-with-adobe-sign.md#selectsubmitactionforanadaptiveform)

![Information om signerare](assets/signer_details_new.png)

### Redigera anpassade formuläregenskaper för Adobe Sign {#enableadobesign}

Konfigurera anpassningsbara formuläregenskaper för Adobe Sign för ett befintligt eller nytt anpassat formulär.

[Skapa ett anpassningsbart formulär för Adobe Sign](../../forms/using/working-with-adobe-sign.md#create-an-adaptive-form-for-adobe-sign) beskriver stegen för att skapa ett enkelt anpassningsbart formulär. Se [Skapa ett adaptivt formulär](../../forms/using/creating-adaptive-form.md) för andra alternativ som är tillgängliga när du skapar ett adaptivt formulär.

#### Skapa ett anpassat formulär för Adobe Sign {#create-an-adaptive-form-for-adobe-sign}

Så här skapar du ett signeringsaktiverat anpassat formulär:

1. Navigera till **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Formulär]** > **[!UICONTROL Formulär och dokument]**.
1. Tryck på **[!UICONTROL Skapa]** och välj **[!UICONTROL Adaptivt formulär]**. En lista med mallar visas. Markera mallen och tryck på **[!UICONTROL Nästa]**.
1. På fliken **[!UICONTROL Grundläggande]** :

   1. Ange **namn** och **titel** för det anpassade formuläret.

   1. Välj den [konfigurationsbehållare](../../forms/using/adobe-sign-integration-adaptive-forms.md#configure-adobe-sign-with-aem-forms) som skapades när Adobe Sign konfigurerades med AEM Forms.

1. Välj något av följande alternativ på fliken **[!UICONTROL Formulärmodell]** :

   * Välj **[!UICONTROL Koppla formulärmall som dokumentmall]** och välj sedan en dokumentmall. Om du använder ett formulärmallsbaserat adaptivt formulär visar dokumenten som skickas för signering endast de fält som är baserade på den associerade formulärmallen. Alla fält i det adaptiva formuläret visas inte.

   * Välj alternativet **[!UICONTROL Generera postdokument]** . Om du använder ett anpassat formulär med alternativet Dokument för post aktiverat, visas alla fält i det adaptiva formuläret i det dokument som skickats för signering.

1. Tryck på **[!UICONTROL Skapa.]** Ett signeringsaktiverat anpassat formulär skapas, som kan användas för att lägga till Adobe Sign-fält.

#### Redigera ett anpassat formulär för Adobe Sign {#editafsign}

Utför följande steg för att använda Adobe Sign i ett befintligt anpassat formulär:

1. Navigera till **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Formulär]** > **[!UICONTROL Formulär och dokument]**.
1. Markera det adaptiva formuläret och tryck på **[!UICONTROL Egenskaper]**.
1. På fliken **[!UICONTROL Grundläggande]** väljer du den [konfigurationsbehållare](../../forms/using/adobe-sign-integration-adaptive-forms.md#configure-adobe-sign-with-aem-forms) som skapades när Adobe Sign konfigurerades med AEM Forms.
1. Välj något av följande alternativ på fliken **[!UICONTROL Formulärläge]** :

   * Välj **[!UICONTROL Koppla formulärmall som dokumentmall]** och välj sedan en dokumentmall. Om du använder ett formulärmallsbaserat adaptivt formulär visar dokumenten som skickas för signering endast de fält som är baserade på den associerade formulärmallen. Alla fält i det adaptiva formuläret visas inte.

   * Välj alternativet **[!UICONTROL Generera postdokument]** . Om du använder ett anpassat formulär med alternativet Dokument för post aktiverat, visas alla fält i det adaptiva formuläret i det dokument som skickats för signering.

1. Tryck på **[!UICONTROL Spara och stäng]**. Det anpassningsbara formuläret är aktiverat för Adobe Sign.

### Lägga till Adobe Sign-fält i ett anpassat formulär {#addadobesignfieldstoanadaptiveform}

Adobe Sign har olika fält som kan placeras i ett anpassat formulär. Dessa fält accepterar olika typer av data som signaturer, initialer, företag eller titel och hjälper till att samla in extra information vid signering, tillsammans med signaturerna. Du kan använda Adobe Sign-blockkomponenten för att placera Adobe Sign-fält på olika platser i ett anpassat formulär.

Utför följande steg för att lägga till fält i ett adaptivt formulär och anpassa olika alternativ för dessa fält:

1. Dra och släpp **Adobe Sign-blockkomponenten** från komponentwebbläsaren till det adaptiva formuläret. Adobe Sign-blockkomponenten har alla Adobe Sign-fält som stöds. Som standard läggs ett **signaturfält** till i det anpassade formuläret.

   ![Signeringsblock](assets/sign_block_new.png)

   Som standard visas inte Adobe Sign-blocket i det publicerade adaptiva formuläret. Den visas bara i signeringsdokumenten. Du kan ändra synligheten för Adobe Sign-blocket från egenskaperna för Adobe Sign-blockkomponenten.

   >[!NOTE]
   >
   >    * Adobe Sign-block måste inte användas för att använda Adobe Sign i ett anpassat formulär. Om du inte använder Adobe Sign-blocket och lägger till fält för signerare, visas standardsignaturfältet längst ned i signeringsdokumenten.
   >    * Använd endast Adobe Sign-block för de hjälpformulär som automatiskt genererar arkivdokument. Om du använder en anpassad XDP för att generera ett anpassat formulär för arkivhandlingar eller ett formulärmallsbaserat formulär krävs inte Adobe Sign-block.


1. Markera **Adobe Sign-blockkomponenten** och tryck på ikonen **Redigera** ![aem_6_3_edit](assets/aem_6_3_edit.png) . Här visas alternativ för att lägga till fält och formatera utseende för ett fält.

   ![adobe-sign-block-select-fields](assets/adobe-sign-block-select-fields.png)

   **** S. Markera och lägg till Adobe Sign-fält. **** B. Expandera Adobe Sign-blocket till helskärmsläge

1. Tryck på ikonen **Adobe Sign-fält** ![aem_6_3_adobesign](assets/aem_6_3_adobesign.png) . Här visas alternativ för att markera och lägga till Adobe Sign-fält.

   Expandera listrutan **Typ** för att välja ett Adobe Sign-fält och tryck på ikonen Klar ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) för att lägga till det markerade fältet i Adobe Sign-blocket. Listrutan **Typ** innehåller fälttyperna Signatur, Signerarinformation och Data. Adobe Sign-integrering med AEM Forms-supportfält listas endast i listrutan Typ. Mer information om Adobe Sign-fält finns i [Adobe Sign-dokumentationen](https://helpx.adobe.com/sign/help/field-types.html).

   ![adobe-sign-block-fields-options](assets/adobe-sign-block-fields-options.png)

   Du måste ange ett unikt namn för ett fält. Du kan också markera ett obligatoriskt fält genom att välja önskat alternativ. Förutom **Namn** och **** Ersättningsalternativ har vissa Adobe Sign-fält fler alternativ. Till exempel mask och flera rader. Ange dessutom ett unikt namn för varje Adobe Sign-fält oavsett om fälten finns i samma eller olika Adobe Sign-block.

   Om du väljer **Digital signatur** i listrutan kan du använda digitala signaturer i det adaptiva formuläret:

   * Online med molnsignaturer för att signera med ett [digitalt ID](https://helpx.adobe.com/sign/kb/digital-certificate-providers.html) som finns hos en betrodd tjänsteleverantör.
   * Hämta dokumentet lokalt med Adobe Acrobat eller Reader med hjälp av ett smartkort, en USB-token eller ett filbaserat digitalt ID.

### Aktivera Adobe Sign för ett anpassat formulär {#enableadobsignforanadaptiveform}

Adobe Sign är inte aktiverat för ett anpassat formulär. Gör så här för att aktivera den:

1. Tryck på **Formulärbehållare** i innehållsläsaren och tryck på ikonen **Konfigurera** ![konfigurera](assets/configure.png) . Egenskaper öppnas i webbläsaren och egenskaper för behållare för adaptiva formulär visas.
1. Utöka dragspelsfliken **Elektronisk signatur** i egenskapswebbläsaren och välj alternativet **Aktivera Adobe Sign** . Det aktiverar Adobe Sign för ett anpassat formulär.

### Välj Adobe Sign Cloud-tjänsten och signeringsbeställning {#selectadobesigncloudserviceforanadaptiveform}

Du kan konfigurera flera Adobe Sign-tjänster för en instans av AEM Forms. Det är tillrådligt att ha en separat uppsättning tjänster för varje funktion (personal, ekonomi med mera). Det gör det enklare att spåra och rapportera signerade dokument. En bank har till exempel flera avdelningar. Du kan ha en separat konfiguration för varje avdelning för bättre spårning av dokumenten.

Ett dokument kan också ha flera signerare. Ett kreditkortsprogram kan t.ex. ha flera sökande. En bank kräver signaturer från alla sökande innan ansökan behandlas. I scenarier med flera signerare kan du välja att signera dokumentet i sekventiell eller samtidig ordning.

Gör så här för att välja en molntjänst och signeringsordning:

![molntjänst](assets/cloud-service.png)

1. Tryck på **Formulärbehållare** i innehållsläsaren och tryck på ikonen **Konfigurera** ![konfigurera](assets/configure.png) . Egenskaper öppnas i webbläsaren och egenskaper för behållare för adaptiva formulär visas.
1. Utöka dragspelsfliken **Elektronisk signatur** i egenskapswebbläsaren och välj alternativet **Aktivera Adobe Sign** . Det aktiverar Adobe Sign för ett anpassat formulär.
1. Välj en molntjänst i den redan konfigurerade listan över Adobe Sign Cloud-tjänster.

   Om **Adobe Sign-molntjänstlistan** är tom följer du artikeln [Konfigurera Adobe Sign med AEM Forms](../../forms/using/adobe-sign-integration-adaptive-forms.md) för att konfigurera tjänsten.

1. Välj signeringsordning i dialogrutan **Signerare kan signera** . Adobe Sign-signerare kan signera ett adaptivt formulär **sekventiellt** - en efter en annan signerare eller **samtidigt** - i valfri ordning.

   I sekventiell ordning tar en signerare emot formuläret för signering i taget. När en signerare har slutfört signeringen av dokumentet skickas formuläret till nästa signerare och så vidare.

   Flera signerare kan signera ett formulär samtidigt i en och samma ordning.

1. [Lägg till signerare i ett anpassat formulär](../../forms/using/working-with-adobe-sign.md#addsignerstoanadaptiveform) och tryck på ikonen Klar [aem_6_3_forms_save](assets/aem_6_3_forms_save.png) för att spara ändringarna.


### Lägga till signerare i ett anpassat formulär {#addsignerstoanadaptiveform}

Du kan bara ha en eller flera signerare för ett anpassat formulär. När du lägger till en signerare kan du även konfigurera autentiseringsinformation för signeraren. Du kan också välja om formuläranvändaren och signeraren ska vara samma person. Utför följande steg för att lägga till och ange olika detaljer om en signerare:

1. Tryck på **Formulärbehållare** i innehållsläsaren och tryck på ikonen **Konfigurera** ![konfigurera](assets/configure.png) . Egenskapsläsaren öppnas med egenskaper för adaptiv formulärbehållare.
1. Utöka dragspelsfliken **Elektronisk signatur** i egenskapswebbläsaren och välj alternativet **Aktivera Adobe Sign** . Det aktiverar Adobe Sign för ett anpassat formulär.
1. Tryck på **Lägg till signerare** under **Signerarkonfiguration**. Den lägger till en signerare i det adaptiva formuläret. Du kan lägga till flera Adobe Sign-signerare i ett anpassat formulär.
1. ![telefoninformation](assets/phone-details.png)

   Klicka på ikonen **Redigera** ![aem_6_3_edit](assets/aem_6_3_edit.png) för att ange följande information om signeraren:

   * **** Titel: Ange en titel som unikt identifierar en signerare.

   * **** Är signeraren och den person som fyller i formuläret densamma?: Välj **Ja** om formuläranvändaren och den första signeraren är samma person. Om alternativet är inställt på **Nej,** ska du inte använda signaturstegskomponenten i det adaptiva formuläret. Om formuläret innehåller en komponent för signatursteg ställs fältet automatiskt in på Ja.

   * **** Undertecknarens e-postadress: Ange signerarens e-postadress. Signeraren får signerade dokument/formulär på den angivna e-postadressen. Du kan välja att använda en e-postadress som finns i ett formulärfält, i AEM-användarprofilen för den inloggade användaren eller manuellt ange en e-postadress. Det är ett obligatoriskt steg. Kontrollera att e-postadressen till den första signeraren eller den enda signeraren (om det är en signerare) inte är identisk med det Adobe Sign-konto som används för att konfigurera AEM-molntjänster.

   * **** Autentiseringsmetod för signerare: Ange metoden för att autentisera en användare innan ett formulär öppnas för signering. Du kan välja mellan telefon, kunskapsbas och social ID-baserad autentisering.
   >[!NOTE]
   >
   >    * Som standard har den sociala identitetsbaserade autentiseringen ett alternativ för att autentisera med Facebook, Google och LinkedIn. Du kan kontakta Adobe Sign-support för att aktivera andra leverantörer av social autentisering.


   * **** Adobe Sign-fält som ska fyllas i eller signeras: Välj Adobe Sign-fält för signeraren. Ett anpassningsbart formulär kan ha flera Adobe Sign-fält. Du kan välja att aktivera specifika fält för en signerare. I fältet visas alla tillgängliga Adobe Sign-block. När du markerar ett block markeras alla fält i blocket. Du kan använda X-ikonen för att avmarkera ett fält.
   ![signerarinformation](assets/signer-details.png)

   Bilden ovan har två exempel på Adobe Sign-block: Personlig information och kontorsinformation

   Tryck på ![ikonen Klar_6_3_forms_save](assets/aem_6_3_forms_save.png) . Undertecknaren läggs till och konfigureras.

### Välj Skicka åtgärd för ett anpassat formulär {#selectsubmitactionforanadaptiveform}

När du har lagt till Adobe Sign-fält i ett anpassat formulär, aktiverar Adobe Sign från formulärbehållaren, väljer Adobe Sign Cloud-tjänsten och lägger till Adobe Sign-signerare, väljer du en lämplig överföringsåtgärd för det anpassade formuläret. Detaljerad information om hur du skickar formulär med adaptiva format finns i [Konfigurera åtgärden](../../forms/using/configuring-submit-actions.md)Skicka.

Dessutom skickas ett anpassat formulär aktiverat för Adobe Sign endast när alla signerare har signerat formuläret. Du kan hitta delvis signerade formulär i avsnittet Väntande signering på formulärportalen. Konfigurationstjänsten för Adobe Sign fortsätter att avfråga Adobe Sign-servern med [regelbundna intervall](../../forms/using/adobe-sign-integration-adaptive-forms.md) för att verifiera signaturens status. Om alla signerare signerar formuläret, startas tjänsten för att skicka och formuläret skickas. Om du använder en anpassad skickaåtgärd och formuläret använder Adobe Sign, ska du uppdatera din anpassade sändningsåtgärd så att du kan använda åtgärden Skicka.

>[!NOTE]
>
>Data i det anpassningsbara formuläret lagras tillfälligt på Forms Portal. Vi rekommenderar att du använder [anpassad lagring för Forms Portal](/help/forms/using/configuring-draft-submission-storage.md). Den ser till att PII-data (personligt identifierbar information) inte lagras på AEM-servrar.

Din formulärsigneringsupplevelse är klar. Du kan förhandsgranska formuläret för att verifiera signeringsprocessen. På det publicerade formuläret visas blockeringsfält för Adobe Sign när en signerare tar emot formuläret för signering via ett e-postmeddelande. Den här upplevelsen kallas även signeringsupplevelse som inte är i form. Du kan också konfigurera en signeringsupplevelse i formulär för den första signeraren, se [Skapa signeringsupplevelse](../../forms/using/working-with-adobe-sign.md#create-in-form-signing-experience)i formulär.

## Konfigurera molnsignaturer för ett anpassat formulär {#configure-cloud-signatures-for-an-adaptive-form}

Molnbaserade digitala signaturer eller fjärrsignaturer är en ny generation digitala signaturer som fungerar på både dator, mobil och webben - och som uppfyller de högsta efterlevnads- och säkerhetsnivåerna för autentisering av signerare. Du kan signera ett anpassat formulär med molnbaserade digitala signaturer.

När du har [redigerat anpassade formuläregenskaper för Adobe Sign](../../forms/using/working-with-adobe-sign.md#enableadobesign)gör du följande för att lägga till ett molnsignaturfält i ett anpassat formulär:

1. Dra och släpp **Adobe Sign-blockkomponenten** från komponentwebbläsaren till det adaptiva formuläret. Adobe Sign-blockkomponenten har alla Adobe Sign-fält som stöds. Som standard läggs ett **signaturfält** till i det anpassade formuläret.

   ![Signeringsblock](assets/sign-block-new.png)

1. Markera **Adobe Sign-blockkomponenten** och tryck på ikonen **Redigera** ![aem_6_3_edit](assets/aem_6_3_edit.png) . Här visas alternativ för att lägga till fält och formatera utseende för ett fält.

   ![adobe-sign-block-select-fields](assets/adobe-sign-block-select-fields.png)

   **** S. Markera och lägg till Adobe Sign-fält. **** B. Expandera Adobe Sign-blocket till helskärmsläge

1. Tryck på ikonen **Adobe Sign-fält** ![aem_6_3_adobesign](assets/aem_6_3_adobesign.png) . Här visas alternativ för att markera och lägga till Adobe Sign-fält.

   Expandera listrutan **Typ** för att välja **Digital signatur** och tryck på ikonen Klar för att lägga till det valda fältet i Adobe Sign-blocket.

   ![Elektroniska underskrifter](assets/digital_signatures_new.png)

   Du måste ange ett unikt namn för ett fält.

   Använd digitala signaturer på det anpassade formuläret med:

   * Molnsignaturer: Signera med ett [digitalt ID](https://helpx.adobe.com/sign/kb/digital-certificate-providers.html) som finns hos en betrodd tjänsteleverantör.
   * Adobe Acrobat eller Reader: Hämta och öppna dokumentet med Adobe Acrobat eller Reader för att signera med ett smartkort, en USB-token eller ett filbaserat digitalt ID.
   När du har lagt till fältet för molnsignatur i det adaptiva formuläret utför du följande steg för att slutföra konfigurationsprocessen:

   * [Aktivera Adobe Sign för ett anpassat formulär](../../forms/using/working-with-adobe-sign.md#enableadobsignforanadaptiveform)
   * [Välj Adobe Sign Cloud-tjänsten för ett anpassat formulär](../../forms/using/working-with-adobe-sign.md#selectadobesigncloudserviceforanadaptiveform)
   * [Lägga till Adobe Sign-signerare i ett anpassat formulär](../../forms/using/working-with-adobe-sign.md#addsignerstoanadaptiveform)
   * [Välj Skicka åtgärd för ett anpassat formulär](../../forms/using/working-with-adobe-sign.md#selectsubmitactionforanadaptiveform)


## Skapa signeringsupplevelser i form av formulär {#create-in-form-signing-experience}

Användaren kan också signera ett anpassat formulär medan han/hon fyller i formuläret. Den här upplevelsen kallas även signering i form av formulär. Signeringsfunktionen i form är bara tillgänglig för den första signeraren i en miljö med flera signerare. Utför följande steg för att skapa en signeringsupplevelse i ett anpassat formulär:

1. [Lägg till och konfigurera signaturstegskomponenten](../../forms/using/working-with-adobe-sign.md#add-and-configure-the-signature-step-component).
1. [Lägg till komponenten](../../forms/using/working-with-adobe-sign.md#configure-the-thank-you-page-or-summary-step-component)Sammanfattningssteg.

![Signing in-form Experience](assets/in_form_signing_experience_new.png)

### Lägg till och konfigurera komponenten Signatursteg {#add-and-configure-the-signature-step-component}

Använd komponenten Signatursteg för att ange ett område där det ifyllda formuläret ska signeras elektroniskt. När avsnittet med signaturstegskomponenten återges visas en signerbar PDF-version av det ifyllda formuläret. Komponenten Signatursteg får full bredd som är tillgänglig för formuläret. Vi rekommenderar att du inte har någon annan komponent i avsnittet som innehåller komponenten Signatursteg.

Utför följande steg för att konfigurera signaturstegskomponenten:

1. Dra och släpp **signaturstegskomponenten** från komponentwebbläsaren till formuläret.
1. Markera den nya signaturstegskomponenten och tryck på **ikonen** Konfigurera ![](assets/configure.png) konfiguration. Egenskaper öppnas i webbläsaren och egenskaper för signatursteg visas. Konfigurera följande egenskaper:

   * **Elementnamn**: Ange komponentens namn.

   * **** Titel: Ange komponentens unika namn.
   * **** Mallmeddelande: Ange det meddelande som ska visas när signatur-PDF-filen läses in. Adobe Sign-tjänsterna tar lite tid att förbereda och läsa in PDF-signaturer.
   * **** Underteckningstjänst: Välj alternativet **Adobe Sign** .

   * **Använd äldre e-signeringskomponent**: Om du använder respektive adaptiva formulär i [AEM Forms Workspace](../../forms/using/introduction-html-workspace.md), AEM Forms-appen eller det underliggande adaptiva formuläret har en äldre e-signeringskomponent väljer du alternativet **Använd äldre e-signeringskomponent** .

   * **Konfiguration**: Välj en konfiguration (Adobe Sign Cloud-tjänsten). Listrutan är bara tillgänglig om alternativet **Använd äldre e-signeringskomponent** är aktiverat.
   Tryck på ikonen Klar ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) för att spara ändringarna.

   ![Signatursteg](assets/signature_step_new.png)

   >[!NOTE]
   >
   >    * När du drar och släpper **[!UICONTROL signaturstegskomponenten]** i formuläret **[!UICONTROL är signeraren och den person som fyller i formuläret densamma?]** är automatiskt inställt på **Ja**. Det krävs för att formuläret ska fungera.
      >
      >    
   * Anpassningsbara formulär som är aktiverade för Adobe Sign har inte stöd för att använda Skicka-knappen i avsnittet eller panelen med signaturstegskomponenten. Du kan lägga till ett sammanfattningssteg efter signatursteget för manuell överföring eller så aktiveras en automatisk överföring efter det intervall som angetts med hjälp av konfigurationstjänsten [för](../../forms/using/adobe-sign-integration-adaptive-forms.md#configure-adobe-sign-scheduler-to-sync-the-signing-status)Adobe Sign.


### Konfigurera tacksidan eller sammanfattningssteget {#configure-the-thank-you-page-or-summary-step-component}

Komponenten **Sammanfattningssteg** skickar automatiskt formuläret, fyller i informationen på den anpassade sammanfattningssidan och visar sammanfattningen av det skickade formuläret. Den hämtar även den information som krävs i returkartan. Komponenten Sammanfattningssteg får full bredd som är tillgänglig för formuläret. Vi rekommenderar att du inte har någon annan komponent i avsnittet som innehåller komponenten Sammanfattningssteg.

Nu är signeringsupplevelsen i form av formulär klar. Du kan förhandsgranska formuläret för att verifiera signeringsprocessen.

## Frågor och svar {#frequently-asked-questions}

**** Ans: Nej, AEM Forms stöder inte användning av ett adaptivt formulär som bäddar in ett adaptivt formulär aktiverat för Adobe Sign för signering

**** Ans: Anpassningsbart formulär som skapats med den avancerade mallen är konfigurerat att använda Adobe Sign. Lös felet genom att skapa och välja en Adobe Sign-molnkonfiguration och konfigurera en Adobe Sign-signerare för det adaptiva formuläret.

**** Ans: Ja, du kan använda texttaggar i en textkomponent för att lägga till Adobe Sign-fält i ett anpassat formulär som är aktiverat för ett [postdokument](../../forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md) (endast det automatiskt genererade postalternativet). Mer information om proceduren och reglerna för att skapa en texttagg finns i [Adobe Sign-dokumentation](https://helpx.adobe.com/sign/help/text-tags.html). Dessutom har adaptiva formulär begränsat stöd för texttaggar. Du kan använda texttaggarna för att skapa endast de fält som stöds av [Adobe Sign-blocket](../../forms/using/working-with-adobe-sign.md#configure-cloud-signatures-for-an-adaptive-form) .

**** Ans: Du kan använda båda komponenterna samtidigt i ett formulär. Här följer några rekommendationer för hur du använder dessa komponenter:

**** Adobe Sign-block: Du kan använda Adobe Sign-blocket för att lägga till Adobe Sign-fält var som helst i det anpassade formuläret. Det hjälper även till att tilldela specifika fält till signerare. När ett anpassat formulär förhandsgranskas eller publiceras visas inte Adobe Sign-blocket som standard. De här blocken aktiveras bara i signeringsdokumentet. I signeringsdokumentet aktiveras bara de fält som tilldelats en signerare. Adobe Sign-block kan användas med första och efterföljande signerare.

**** Underskriftsstegskomponent: Du kan använda signaturstegskomponenten för att skapa signeringsupplevelser i formulär. Endast den första signeraren kan signera medan formuläret fylls i. När avsnittet som innehåller signaturstegskomponenten återges visas en signerbar PDF-version av formuläret. Det är vanligtvis det sista eller näst sista avsnittet följt av en sammanfattningskomponent i ett formulär.

## Felsökning {#troubleshoot}

### Avtalsfel i Adobe Sign {#adobe-sign-agreement-failures}

**Problem** När Adobe Sign-tjänsten har konfigurerats för ett adaptivt formulär kan tjänsten inte skapa ett Adobe Sign-avtal för det underliggande adaptiva formuläret.

**Upplösning**

* Kontrollera [konfigurationen av Adobe Sign-molntjänsten](../../forms/using/adobe-sign-integration-adaptive-forms.md) som används i det adaptiva formuläret.
* Kontrollera att API-programmet på Adobe Sign-servern som används för att konfigurera Adobe Sign Cloud-tjänsten har nödvändiga behörigheter.
* Om du använder flera Adobe Sign Cloud-tjänster pekar du **[!UICONTROL autentiserings-URL]** för alla tjänster på samma **[!UICONTROL Adobe Sign-kort]**.

* Använd separata e-postadresser för att konfigurera Adobe Sign-kontot och för den första signeraren och den enda signeraren. E-postadressen till den första signeraren eller den enda signeraren (om det är en signerare) kan inte vara identisk med det Adobe Sign-konto som används för att konfigurera AEM-molntjänster.

## Relaterade artiklar {#related-articles}

* [Integrera Adobe Sign med AEM Forms](../../forms/using/adobe-sign-integration-adaptive-forms.md)
* [Använda Adobe Sign i ett anpassat formulär](../../forms/using/working-with-adobe-sign.md)

* [Använda Adobe Sign med AEM-formulär (video)
   ](https://helpx.adobe.com/experience-manager/kt/forms/using/adobe-sign-integration-feature-video.html)
