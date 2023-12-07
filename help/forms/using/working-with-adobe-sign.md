---
title: Använda Adobe Sign i en adaptiv form
description: Möjliggör arbetsflöden för e-signaturer (Adobe Sign) för ett adaptivt formulär för att automatisera signeringsarbetsflöden, förenkla processer för enstaka och flera signaturer samt för att elektroniskt signera formulär från mobila enheter.
contentOwner: khsingh
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
docset: aem65
feature: Adaptive Forms, Acrobat Sign
exl-id: a8decba9-229d-40a2-992a-3cc8ebefdd6d
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '3673'
ht-degree: 0%

---

# Använda [!DNL Adobe Sign] i anpassningsbar form{#using-adobe-sign-in-an-adaptive-form}

<span class="preview"> Adobe rekommenderar att man använder modern och utbyggbar datainhämtning [Kärnkomponenter](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html) for [skapa ny Adaptive Forms](/help/forms/using/create-an-adaptive-form-core-components.md) eller [lägga till adaptiv Forms på AEM Sites-sidor](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). De här komponenterna utgör ett betydande framsteg när det gäller att skapa adaptiva Forms-filer, vilket ger imponerande användarupplevelser. I den här artikeln beskrivs det äldre sättet att skapa Adaptiv Forms med baskomponenter. </span>

| Version | Artikellänk |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Klicka här](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/use-adobe-sign/working-with-adobe-sign.html) |
| AEM 6.5 | Den här artikeln |


[!DNL Adobe Sign] möjliggör arbetsflöden för e-signaturer för anpassningsbara formulär. E-signaturer förbättrar arbetsflödena för att bearbeta dokument inom juridik, försäljning, löneadministration, personaladministration och andra områden.

I en typisk [!DNL Adobe Sign] och anpassningsbara formulärscenarier fyller en användare i ett anpassat formulär för att ansöka om en tjänst. Till exempel kräver en ansökan om inteckning och kreditkort juridiska signaturer från alla låntagare och medsökande. Om du vill aktivera arbetsflöden för elektroniska signaturer för liknande scenarier kan du integrera [!DNL Adobe Sign] med AEM [!DNL Forms]. Några exempel till är: [!DNL Adobe Sign] till:

* Slut avtal från vilken enhet som helst med fullt automatiserade processer för förslag, offerter och kontrakt.
* Slutför HR-processerna snabbare och ge medarbetarna de digitala upplevelserna.
* Minska kontraktscyklerna och anlita era leverantörer snabbare.
* Skapa digitala arbetsflöden som automatiserar vanliga processer.

[!DNL Adobe Sign] integrering med AEM [!DNL Forms] stöder:

* Arbetsflöden för signering för en och flera användare
* Sekventiella och samtidiga signeringsarbetsflöden
* Underteckna i form och i form
* Signera formulär som anonym eller inloggad användare
* Dynamiska signeringsprocesser (integration med AEM [!DNL Forms] arbetsflöde)
* Autentisering via kunskapsbas, telefon och sociala profiler

Lär dig [bästa sättet att använda Adobe Sign med anpassningsbara formulär](https://medium.com/adobetech/using-adobe-sign-to-e-sign-an-adaptive-form-heres-the-best-way-to-do-it-dc3e15f9b684) för att skapa bättre signeringsupplevelser.

## Förutsättningar {#prerequisites}

Innan du använder [!DNL Adobe Sign] i adaptiv form:

* AEM [!DNL Forms] molntjänsten är konfigurerad att använda [!DNL Adobe Sign]. Mer information finns i [Integrera Adobe Sign med AEM Forms](../../forms/using/adobe-sign-integration-adaptive-forms.md).
* Håll listan med signerare klar. Du måste ange minst en e-postadress för varje signerare.

## Konfigurera [!DNL Adobe Sign] för en adaptiv blankett {#configure-adobe-sign-for-an-adaptive-form}

Utför följande steg för att konfigurera [!DNL Adobe Sign] för en adaptiv form:

1. [Redigera anpassningsbara formuläregenskaper för Adobe-signering](../../forms/using/working-with-adobe-sign.md#enableadobesign)
1. [Lägga till Adobe Sign-fält i ett anpassat formulär](../../forms/using/working-with-adobe-sign.md#addadobesignfieldstoanadaptiveform)
1. [Aktivera Adobe Sign för ett anpassat formulär](../../forms/using/working-with-adobe-sign.md#enableadobsignforanadaptiveform)
1. [Välj Adobe Sign Cloud Service för ett anpassat formulär](../../forms/using/working-with-adobe-sign.md#selectadobesigncloudserviceforanadaptiveform)

1. [Lägga till Adobe Sign-signerare i ett anpassat formulär](../../forms/using/working-with-adobe-sign.md#addsignerstoanadaptiveform)
1. [Välj Skicka åtgärd för ett anpassat formulär](../../forms/using/working-with-adobe-sign.md#selectsubmitactionforanadaptiveform)

![Information om signerare](assets/signer_details_new.png)

### Redigera adaptiva formuläregenskaper för [!DNL Adobe Sign] {#enableadobesign}

Konfigurera adaptiva formuläregenskaper för [!DNL Adobe Sign] för en befintlig eller ny anpassningsbar form.

[Skapa ett anpassningsbart formulär för Adobe Sign](../../forms/using/working-with-adobe-sign.md#create-an-adaptive-form-for-adobe-sign) beskriver stegen för att skapa ett grundläggande anpassat formulär. Se [Skapa ett anpassat formulär](../../forms/using/creating-adaptive-form.md) för andra alternativ som är tillgängliga när du skapar ett anpassat formulär.

#### Skapa ett anpassat formulär för [!DNL Adobe Sign] {#create-an-adaptive-form-for-adobe-sign}

Gör så här för att skapa ett signeringsaktiverat anpassat formulär:

1. Navigera till **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms & Documents]**.
1. Välj **[!UICONTROL Create]** och markera **[!UICONTROL Adaptive Form]**. En lista med mallar visas. Markera mallen och välj **[!UICONTROL Next]**.
1. I **[!UICONTROL Basic]** tab:

   1. Ange **[!UICONTROL Name]** och **[!UICONTROL Title]** för den adaptiva formen.

   1. Välj [konfigurationsbehållare](../../forms/using/adobe-sign-integration-adaptive-forms.md#configure-adobe-sign-with-aem-forms) skapades vid konfigurering [!DNL Adobe Sign] med AEM [!DNL Forms].

      >[!NOTE]
      >
      >The **[!UICONTROL Adobe Sign Cloud Service]** listrutan visar de molntjänster som är konfigurerade i den konfigurationsbehållare som du väljer i det här fältet. The **[!UICONTROL Adobe Sign Cloud Service]** listrutan är tillgänglig i **[!UICONTROL Electronic Signature]** när du väljer **[!UICONTROL Enable Adobe Sign]** alternativ.

1. I **[!UICONTROL Form Model]** väljer du något av följande alternativ:

   * Välj **[!UICONTROL Associate form template as the Document of Record template]** och välj en dokumentmall. Om du använder ett formulärmallsbaserat adaptivt formulär visar dokumenten som skickas för signering endast de fält som är baserade på den associerade formulärmallen. Alla fält i det adaptiva formuläret visas inte.

   * Välj **[!UICONTROL Generate Document of Record]** alternativ. Om du använder ett anpassat formulär med alternativet Dokument för post aktiverat, visas alla fält i det adaptiva formuläret i det dokument som skickats för signering.

1. Välj **[!UICONTROL Create.]** Ett signeringsaktiverat adaptivt formulär skapas, som kan användas för att lägga till [!DNL Adobe Sign] fält.

#### Redigera ett anpassat formulär för [!DNL Adobe Sign] {#editafsign}

Utför följande steg för att använda [!DNL Adobe Sign] i en befintlig adaptiv form:

1. Navigera till **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms & Documents]**.
1. Markera det adaptiva formuläret och välj **[!UICONTROL Properties]**.
1. I **[!UICONTROL Basic]** väljer du [konfigurationsbehållare](../../forms/using/adobe-sign-integration-adaptive-forms.md#configure-adobe-sign-with-aem-forms) skapades vid konfigurering [!DNL Adobe Sign] med AEM [!DNL Forms].
1. I **[!UICONTROL Form Model]** väljer du något av följande alternativ:

   * Välj **[!UICONTROL Associate form template as the Document of Record template]** och välj en dokumentmall. Om du använder ett formulärmallsbaserat adaptivt formulär visar dokumenten som skickas för signering endast de fält som är baserade på den associerade formulärmallen. Alla fält i det adaptiva formuläret visas inte.

   * Välj **[!UICONTROL Generate Document of Record]** alternativ. Om du använder ett anpassat formulär med alternativet Dokument för post aktiverat, visas alla fält i det adaptiva formuläret i det dokument som skickats för signering.

1. Välj **[!UICONTROL Save & Close]**. Det adaptiva formuläret är aktiverat för [!DNL Adobe Sign].

### Lägga till Adobe Sign-fält i ett anpassat formulär {#addadobesignfieldstoanadaptiveform}

[!DNL Adobe Sign] har olika fält som kan placeras i ett anpassat formulär. Dessa fält accepterar olika typer av data som signaturer, initialer, företag eller titel och hjälper till att samla in extra information vid signering, tillsammans med signaturerna. Du kan använda [!DNL Adobe Sign] Blockkomponent att montera [!DNL Adobe Sign] fält på olika platser i ett anpassat formulär.

Utför följande steg för att lägga till fält i ett adaptivt formulär och anpassa olika alternativ för dessa fält:

1. Dra och släppa **[!UICONTROL Adobe Sign Block]** från komponentwebbläsaren till det adaptiva formuläret. The [!DNL Adobe Sign] Block-komponenten har alla funktioner som stöds [!DNL Adobe Sign] fält. Som standard läggs en **Signatur** till det anpassningsbara formuläret.

   ![Signeringsblock](assets/sign_block_new.png)

   Som standard är [!DNL Adobe Sign] Blocket visas inte i det publicerade adaptiva formuläret. Den är bara synlig i signeringsdokumenten. Du kan ändra synligheten för [!DNL Adobe Sign] Blockera från egenskaperna för [!DNL Adobe Sign] Blockkomponent.

   >[!NOTE]
   >
   >    * Använda [!DNL Adobe Sign] block är inte obligatoriskt att använda [!DNL Adobe Sign] i adaptiv form. Om du inte [!DNL Adobe Sign] blockera och lägga till fält för signerare, så visas standardsignaturfältet längst ned i signeringsdokumenten.
   >    * Använd [!DNL Adobe Sign] blockera endast för de adaptiva formulär som automatiskt genererar arkivdokument. Om du använder en anpassad XDP för att generera ett anpassat formulär för arkivhandlingar eller ett formulärmallsbaserat formulär, [!DNL Adobe Sign] block stöds inte.
   >
   >

1. Välj **[!UICONTROL Adobe Sign Block]** och väljer **Redigera** ![aem_6_3_edit](assets/aem_6_3_edit.png) -ikon. Här visas alternativ för att lägga till fält och formatera utseende för ett fält.

   ![adobe-sign-block-select-fields](assets/adobe-sign-block-select-fields.png)

   **S.** Markera och lägg till [!DNL Adobe Sign] fält. **B.** Expandera [!DNL Adobe Sign] blockera till helskärmsläge

1. Välj **[!UICONTROL Adobe Sign]Fält** ![aem_6_3_adobesign](assets/aem_6_3_adobesign.png) -ikon. Här visas alternativ för att markera och lägga till [!DNL Adobe Sign] fält.

   Expandera **[!UICONTROL Type]** nedrullningsbart fält där du kan välja ett [!DNL Adobe Sign] och välj Klart ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) ikon för att lägga till det markerade fältet i [!DNL Adobe Sign] -block. The **[!UICONTROL Type]** nedrullningsbara fält innehåller signatur-, signerarinformation- och datafälttyper. [!DNL Adobe Sign] integrering med AEM [!DNL Forms] supportfält som anges i [!UICONTROL Type] endast listrutan. Detaljerad information om [!DNL Adobe Sign] fält, se [Adobe Sign-dokumentation](https://helpx.adobe.com/sign/help/field-types.html).

   ![adobe-sign-block-fields-options](assets/adobe-sign-block-fields-options.png)

   Du måste ange ett unikt namn för ett fält. Du kan också markera ett obligatoriskt fält genom att välja önskat alternativ. Förutom **[!UICONTROL Name]** och **[!UICONTROL Required]** alternativ, vissa [!DNL Adobe Sign] har fler alternativ. Till exempel mask och flera rader. Ange dessutom unika namn för varje [!DNL Adobe Sign] fält om fälten finns i samma eller olika [!DNL Adobe Sign] -block.

   Om du väljer **[!UICONTROL Digital Signature]** från listrutan kan du använda digitala signaturer i det anpassade formuläret:

   * Online med molnsignaturer för att signera med en [digitalt ID](https://helpx.adobe.com/sign/kb/digital-certificate-providers.html) som hanteras av en betrodd tjänsteleverantör.
   * Hämta dokumentet lokalt med Adobe Acrobat eller Reader med ett smartkort, en USB-token eller ett filbaserat digitalt ID.

### Aktivera [!DNL Adobe Sign] för en adaptiv blankett {#enableadobsignforanadaptiveform}

Ut ur lådan, [!DNL Adobe Sign] är inte aktiverat för ett anpassat formulär. Gör så här för att aktivera den:

1. Välj **[!UICONTROL Form Container]** och väljer **[!UICONTROL Configure]** ![konfigurera](assets/configure.png) -ikon. Egenskaper öppnas i webbläsaren och egenskaper för behållare för adaptiva formulär visas.
1. Utöka **[!UICONTROL Electronic Signature]** dragspelspanelen och välj **[!UICONTROL Enable Adobe Sign]** alternativ. Det gör att [!DNL Adobe Sign] för en adaptiv form.

### Välj [!DNL Adobe Sign] Cloud Service och signeringsordning {#selectadobesigncloudserviceforanadaptiveform}

Du kan konfigurera flera [!DNL Adobe Sign] tjänster för en instans av AEM [!DNL Forms]. Det är tillrådligt att ha en separat uppsättning tjänster för varje funktion (personal, ekonomi med mera). Det gör det enklare att spåra och rapportera signerade dokument. En bank har till exempel flera avdelningar. Du kan ha en separat konfiguration för varje avdelning för bättre spårning av dokumenten.

Ett dokument kan också ha flera signerare. En kreditkortsansökan kan t.ex. ha flera sökande. En bank kräver signaturer från alla sökande innan ansökan behandlas. I scenarier med flera signerare kan du välja att signera dokumentet i sekventiell eller samtidig ordning.

Gör så här för att välja en molntjänst och signeringsordning:

![molntjänst](assets/cloud-service.png)

1. Välj **[!UICONTROL Form Container]** och väljer **[!UICONTROL Configure]** ![konfigurera](assets/configure.png) -ikon. Egenskaper öppnas i webbläsaren och egenskaper för behållare för adaptiva formulär visas.
1. Utöka **[!UICONTROL Electronic Signature]** dragspelspanelen och välj **[!UICONTROL Enable Adobe Sign]** alternativ. Det gör att [!DNL Adobe Sign] för en adaptiv form.
1. Välj en molntjänst i den redan konfigurerade listan över [!DNL Adobe Sign] Cloud Service.

   Om **[!UICONTROL Adobe Sign Cloud Service]** listan är tom, följ [Konfigurera Adobe Sign med AEM Forms](../../forms/using/adobe-sign-integration-adaptive-forms.md) artikel för att konfigurera tjänsten.

   I listrutan visas de molntjänster som finns i `global` mapp i Verktyg > **[!UICONTROL Cloud Services]** > **[!UICONTROL Adobe Sign]**. Listrutan innehåller även en lista över de molntjänster som finns i den mapp du har valt i **[!UICONTROL Configuration Container]** när du skapar ett anpassat formulär.

1. Välj signeringsordning på menyn **[!UICONTROL Signers can Sign]** -dialogrutan. [!DNL Adobe Sign] signerare kan signera ett adaptivt formulär **[!UICONTROL Sequentially]** - en efter en annan signerare, eller **[!UICONTROL Simultaneously]** - i vilken ordning som helst.

   I sekventiell ordning tar en signerare emot formuläret för signering i taget. När en signerare har slutfört signeringen av dokumentet skickas formuläret till nästa signerare och så vidare.

   Flera signerare kan signera ett formulär samtidigt i en och samma ordning.

1. [Lägga till signerare i ett anpassat formulär](../../forms/using/working-with-adobe-sign.md#addsignerstoanadaptiveform) och väljer Klar ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) om du vill spara ändringarna.


### Lägga till signerare i ett anpassat formulär {#addsignerstoanadaptiveform}

Du kan bara ha en eller flera signerare för ett anpassat formulär. När du lägger till en signerare kan du även konfigurera autentiseringsinformation för signeraren. Du kan också välja om formuläranvändaren och signeraren ska vara samma person. Utför följande steg för att lägga till och ange olika detaljer om en signerare:

1. Välj **[!UICONTROL Form Container]** och väljer **[!UICONTROL Configure]** ![konfigurera](assets/configure.png) -ikon. Egenskapsläsaren öppnas med egenskaper för adaptiv formulärbehållare.
1. Utöka **[!UICONTROL Electronic Signature]** dragspelspanelen och välj **[!UICONTROL Enable Adobe Sign]** alternativ. Det gör att [!DNL Adobe Sign] för en adaptiv form.
1. Välj **[!UICONTROL Add Signer]** under **[!UICONTROL Signer Configuration]**. Den lägger till en signerare i det adaptiva formuläret. Du kan lägga till flera [!DNL Adobe Sign] signerare till ett adaptivt formulär.
   ![telefoninformation](assets/phone-details.png)

1. Klicka på **Redigera** ![aem_6_3_edit](assets/aem_6_3_edit.png) om du vill ange följande information om signeraren:

   * **[!UICONTROL Title]:** Ange en titel som unikt identifierar en signerare.

   * **[!UICONTROL Is the signer and the person filling the form same?]:** Välj **Ja**, om formuläranvändaren och den första signeraren är samma person. Om alternativet är inställt på **Nej,** ska du inte använda signaturstegskomponenten i det adaptiva formuläret. Om formuläret innehåller en komponent för signatursteg ställs fältet automatiskt in på Ja.

   * **[!UICONTROL Signer Email address]:** Ange signerarens e-postadress. Signeraren får signerade dokument/formulär på den angivna e-postadressen. Du kan välja att använda en e-postadress som finns i ett formulärfält, i AEM användarprofil för den inloggade användaren eller manuellt ange en e-postadress. Det är ett obligatoriskt steg. Kontrollera att e-postadressen för den första signeraren eller den enda signeraren (om det finns en signerare) inte är identisk med [!DNL Adobe Sign] konto som används för att konfigurera AEM molntjänster.

   * **[!UICONTROL Signer Authentication Method]:** Ange metoden för att autentisera en användare innan ett formulär öppnas för signering. Du kan välja mellan telefon, kunskapsbas och social ID-baserad autentisering. För Adobe Acrobat Sign Solutions for Government finns endast telefon- och kunskapsbaserad autentisering.

   >[!NOTE]
   >
   >    * Som standard har den sociala identitetsbaserade autentiseringen ett alternativ för autentisering med Facebook, Google och LinkedIn. Du kan kontakta [!DNL Adobe Sign] stöd för att aktivera andra leverantörer av social autentisering.
   >
   >

   * **[!DNL Adobe Sign]fält som ska fyllas i eller signeras:** Välj [!DNL Adobe Sign] fält för signeraren. Ett anpassningsbart formulär kan ha flera [!DNL Adobe Sign] fält. Du kan välja att aktivera specifika fält för en signerare. Fältet visar alla tillgängliga [!DNL Adobe Sign] Blockar. När du markerar ett block markeras alla fält i blocket. Du kan använda X-ikonen för att avmarkera ett fält.

   ![signerarinformation](assets/signer-details.png)

   Bilden ovan har två exempel [!DNL Adobe Sign] Block: Personlig information och Office-information

   Välj Klar ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) -ikon. Undertecknaren läggs till och konfigureras.

### Välj Skicka åtgärd för ett anpassat formulär {#selectsubmitactionforanadaptiveform}

Efter dig lägger du till [!DNL Adobe Sign] fält till ett anpassat formulär, aktivera [!DNL Adobe Sign] från formulärbehållare, välj [!DNL Adobe Sign] Cloud Service och lägg till [!DNL Adobe Sign] Signerare väljer en lämplig skickaåtgärd för det anpassade formuläret. Detaljerad information om hur du skickar formulär med adaptiva funktioner finns i [Konfigurera åtgärden Skicka](../../forms/using/configuring-submit-actions.md).

Dessutom, en [!DNL Adobe Sign] anpassat formulär skickas bara när alla signerare har signerat formuläret. Du kan hitta delvis signerade formulär i avsnittet Väntande signering på formulärportalen. [!DNL Adobe Sign] Konfigurationstjänsten fortsätter avfråga [!DNL Adobe Sign] server på [regelbundna intervall](../../forms/using/adobe-sign-integration-adaptive-forms.md) för att verifiera signaturernas status. Om alla signerare signerar formuläret, startas tjänsten för att skicka och formuläret skickas. Om du använder en anpassad skicka-åtgärd och formuläret använder [!DNL Adobe Sign]uppdaterar du din anpassade sändningsåtgärd så att den använder åtgärdstjänsten Skicka.

<!-- Remove when forms portal goes live
>[!NOTE]
>
>Data of the adaptive form is stored temporarily on Forms Portal. Use [custom storage for Forms Portal](/help/forms/using/configuring-draft-submission-storage.md). It ensures that the PII (personally identifiable information) data is not stored on AEM servers. 
-->

Din formulärsigneringsupplevelse är klar. Du kan förhandsgranska formuläret för att verifiera signeringsprocessen. På det publicerade formuläret [!DNL Adobe Sign] Blockfält visas när en signerare tar emot formuläret för signering via ett e-postmeddelande. Den här upplevelsen kallas även signeringsupplevelse som inte är i form. Du kan även konfigurera en signeringsupplevelse i formulär för den första signeraren, för detaljerade steg se [Skapa signeringsupplevelser i form av formulär](../../forms/using/working-with-adobe-sign.md#create-in-form-signing-experience).

## Konfigurera molnsignaturer för ett anpassat formulär {#configure-cloud-signatures-for-an-adaptive-form}

Molnbaserade digitala signaturer eller fjärrsignaturer är en ny generation digitala signaturer som fungerar på både dator, mobil och webben - och som uppfyller de högsta efterlevnads- och säkerhetsnivåerna för autentisering av signerare. Du kan signera ett anpassat formulär med molnbaserade digitala signaturer.

Efter [redigera adaptiva formuläregenskaper för Adobe-signering](../../forms/using/working-with-adobe-sign.md#enableadobesign)utför du följande steg för att lägga till molnsignaturfält i ett anpassat formulär:

1. Dra och släppa **[!UICONTROL Adobe Sign Block]** från komponentwebbläsaren till det adaptiva formuläret. The [!UICONTROL Adobe Sign Block] har alla komponenter som stöds [!DNL Adobe Sign] fält. Som standard läggs en **[!UICONTROL Signature]** till det anpassningsbara formuläret.

   ![Signeringsblock](assets/sign-block-new.png)

1. Välj **[!UICONTROL Adobe Sign Block]** och väljer **Redigera** ![aem_6_3_edit](assets/aem_6_3_edit.png) -ikon. Här visas alternativ för att lägga till fält och formatera utseende för ett fält.

   ![adobe-sign-block-select-fields](assets/adobe-sign-block-select-fields.png)

   **S.** Markera och lägg till [!DNL Adobe Sign] fält. **B.** Expandera [!DNL Adobe Sign] blockera till helskärmsläge

1. Välj **[!UICONTROL Adobe Sign Field]** ![aem_6_3_adobesign](assets/aem_6_3_adobesign.png) -ikon. Här visas alternativ för att markera och lägga till [!DNL Adobe Sign] fält.

   Expandera **[!UICONTROL Type]** nedrullningsbart fält att välja **[!UICONTROL Digital Signature]** och väljer **Klar** ikon för att lägga till det markerade fältet i [!DNL Adobe Sign] -block.

   ![Digitala signaturer](assets/digital_signatures_new.png)

   Du måste ange ett unikt namn för ett fält.

   Använd digitala signaturer på det anpassade formuläret med:

   * Molnsignaturer: Signera med en [digitalt ID](https://helpx.adobe.com/sign/kb/digital-certificate-providers.html) som hanteras av en betrodd tjänsteleverantör. Molnsignaturalternativet är inte tillgängligt för Adobe Acrobat Sign Solutions för myndigheter.

   * Adobe Acrobat eller Reader: Hämta och öppna dokumentet med Adobe Acrobat eller Reader för signering med ett smartkort, en USB-token eller ett filbaserat digitalt ID.

   När du har lagt till fältet för molnsignatur i det adaptiva formuläret utför du följande steg för att slutföra konfigurationsprocessen:

   * [Aktivera Adobe Sign för ett anpassat formulär](../../forms/using/working-with-adobe-sign.md#enableadobsignforanadaptiveform)
   * [Välj Adobe Sign Cloud Service för ett anpassat formulär](../../forms/using/working-with-adobe-sign.md#selectadobesigncloudserviceforanadaptiveform)
   * [Lägga till Adobe Sign-signerare i ett anpassat formulär](../../forms/using/working-with-adobe-sign.md#addsignerstoanadaptiveform)
   * [Välj Skicka åtgärd för ett anpassat formulär](../../forms/using/working-with-adobe-sign.md#selectsubmitactionforanadaptiveform)

## Skapa signeringsupplevelser i form av formulär {#create-in-form-signing-experience}

Användaren kan också signera ett anpassat formulär medan han/hon fyller i formuläret. Den här upplevelsen kallas även signering i form av formulär. Signeringsfunktionen i form är bara tillgänglig för den första signeraren i en miljö med flera signerare. Utför följande steg för att skapa en signeringsupplevelse i ett anpassat formulär:

1. [Lägga till och konfigurera komponenten Signatursteg](../../forms/using/working-with-adobe-sign.md#add-and-configure-the-signature-step-component).
1. [Lägg till komponenten Sammanfattningssteg](../../forms/using/working-with-adobe-sign.md#configure-the-thank-you-page-or-summary-step-component).

![Signing in-form Experience](assets/in_form_signing_experience_new.png)

### Lägga till och konfigurera komponenten Signatursteg {#add-and-configure-the-signature-step-component}

Använd signaturstegskomponenten för att ange ett område där det ifyllda formuläret ska signeras elektroniskt. När avsnittet med signaturstegskomponenten återges visas en signerbar PDF-version av det ifyllda formuläret. Komponenten Signatursteg får full bredd som är tillgänglig för formuläret. Vi rekommenderar att du inte har någon annan komponent i avsnittet som innehåller komponenten Signatursteg.

Utför följande steg för att konfigurera signaturstegskomponenten:

1. Dra och släpp **[!UICONTROL Signature Step]** -komponenten från komponentwebbläsaren till formuläret.
1. Markera den nya signaturstegskomponenten och välj **Konfigurera** ![konfigurera](assets/configure.png) -ikon. Egenskaper öppnas i webbläsaren och egenskaper för signatursteg visas. Konfigurera följande egenskaper:

   * **[!UICONTROL Name]**: Ange komponentens namn.

   * **[!UICONTROL Title]:** Ange komponentens unika namn.
   * **[!UICONTROL Template message]:** Ange meddelandet som ska visas medan signaturen PDF läses in. [!DNL Adobe Sign] det tar lite tid att förbereda och läsa in signaturen PDF.
   * **[!UICONTROL Signing Service]:** Välj **[!DNL Adobe Sign]** alternativ.

   * **[!UICONTROL Use legacy E-sign component]**: Om du använder respektive adaptiv form i [AEM Forms Workspace](../../forms/using/introduction-html-workspace.md), AEM [!DNL Forms] eller om det underliggande adaptiva formuläret har en äldre e-signeringskomponent väljer du **Använd äldre e-signeringskomponent** alternativ.

   * **[!UICONTROL Configuration]**: Välj en konfiguration ([!DNL Adobe Sign] Cloud Service). Listrutan är bara tillgänglig om **Använd äldre e-signeringskomponent** är aktiverat.

   * **[!UICONTROL CSS Class]**: Ange CSS-klassen för komponenten.

   Välj Klar ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) om du vill spara ändringarna.

   ![Signatursteg](assets/signature_step_new.png)

   >[!NOTE]
   >
   >* När du drar och släpper **[!UICONTROL Signature Step]** -komponenten till formuläret, **[!UICONTROL Is the signer and the person filling the form same?]** option is automatically set to **Ja**. Det krävs för att formuläret ska fungera.
   >* Använd komponenten Sammanfattningssteg efter signatursteget för att få en så bra upplevelse som möjligt. Sammanfattningssteget skickar automatiskt och omedelbart formuläret när du har signerat ett formulär i signeringssteget. Om du inte använder sammanfattningssteget aktiveras en automatisk överföring endast efter det intervall som angetts med [Konfigurationstjänst för Adobe Sign](../../forms/using/adobe-sign-integration-adaptive-forms.md#configure-adobe-sign-scheduler-to-sync-the-signing-status).
   >
   >Några av de bästa sätten är:
   >
   >* Anpassad formulärpanel som innehåller signeringssteget finns alltid i den sista eller andra panelen i ett anpassat formulär. Det kan bara vara den andra sista panelen när den sista panelen innehåller steget Sammanfattning.
   >* Panelen som innehåller signatur- eller sammanfattningssteget får inte innehålla några andra komponenter.
   >* Anpassningsbara formulär som innehåller signatursteget kan inte ha en skicka-knapp.
   >* Inlämningen av anpassade formulär som innehåller signeringssteget hanteras via en bakgrundstjänst eller sammanfattningssteget. Om det finns en konfigurerad signerare som också fyller i formuläret, är fördelen med att hantera den adaptiva formuläröverföringen med steget Sammanfattning att den omedelbart utvärderar att signeraren har signerat formuläret och anropar åtgärden skicka. En bakgrundstjänst tar längre tid att utvärdera om alla konfigurerade signerare har signerat formuläret och fördröjer överföringen av det adaptiva formuläret.
   >* Utforma formuläret så att användaren inte kan navigera tillbaka från en panel som innehåller signatur- eller sammanfattningssteget.


### Konfigurera tacksidan eller sammanfattningssteget {#configure-the-thank-you-page-or-summary-step-component}

The **Sammanfattningssteg** skickar automatiskt formuläret, fyller i informationen på den anpassade sammanfattningssidan och visar sammanfattningen av det skickade formuläret. Den hämtar även den information som krävs i returkartan. Komponenten Sammanfattningssteg får full bredd som är tillgänglig för formuläret. Vi rekommenderar att du inte har någon annan komponent i avsnittet som innehåller komponenten Sammanfattningssteg.

Nu är signeringsupplevelsen i form av formulär klar. Du kan förhandsgranska formuläret för att verifiera signeringsprocessen.

## Frågor och svar {#frequently-asked-questions}

**F:** Du kan bädda in ett anpassat formulär i ett annat anpassat formulär. Kan det inbäddade adaptiva formuläret [!DNL Adobe Sign] aktiverad?
**Ans:** Nej, AEM [!DNL Forms] har inte stöd för att använda ett anpassningsbart formulär som bäddar in en [!DNL Adobe Sign] anpassat formulär för signering

**F:** När jag skapar ett adaptivt formulär med den avancerade mallen och öppnar det för redigering visas ett felmeddelande om att&quot;elektronisk signatur eller signerare inte är korrekt konfigurerade&quot;. visas. Hur löser jag felmeddelandet?
**Ans:** Anpassningsbart formulär som skapats med den avancerade mallen är konfigurerat att använda [!DNL Adobe Sign]. Lös felet genom att skapa och välja en [!DNL Adobe Sign] molnkonfiguration och konfigurera [!DNL Adobe Sign] signerare för det adaptiva formuläret.

**F:** Kan jag använda [!DNL Adobe Sign] texttaggar i en statisk textkomponent i ett adaptivt formulär?
**Ans:** Ja, du kan lägga till texttaggar i en textkomponent [!DNL Adobe Sign] fält till [Dokument för registrering](../../forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md) (Endast automatiskt genererat dokument med postalternativ) anpassat formulär. Mer information om proceduren och reglerna för att skapa en texttagg finns i [Adobe Sign Documentation](https://helpx.adobe.com/sign/using/text-tag.html). Dessutom har adaptiva formulär begränsat stöd för texttaggar. Du kan använda texttaggarna för att skapa endast de fält som [Adobe Sign Block](../../forms/using/working-with-adobe-sign.md#configure-cloud-signatures-for-an-adaptive-form) stöder.

**F:** AEM [!DNL Forms] ger båda [!UICONTROL Adobe Sign block] och komponenter för signatursteg. Kan dessa användas samtidigt i anpassningsbar form?
**Ans:** Du kan använda båda komponenterna samtidigt i ett formulär. Här följer några rekommendationer för hur du använder dessa komponenter:

**Adobe Sign Block:** Du kan använda [!UICONTROL Adobe Sign Block] att lägga till [!UICONTROL Adobe Sign] fält var som helst i det anpassningsbara formuläret. Det hjälper även till att tilldela specifika fält till signerare. När ett anpassningsbart formulär förhandsgranskas eller publiceras [!UICONTROL Adobe Sign] Blocket är inte synligt som standard. De här blocken aktiveras bara i signeringsdokumentet. I signeringsdokumentet aktiveras bara de fält som tilldelats en signerare. [!UICONTROL Adobe Sign] -block kan användas med första och efterföljande signerare.

**Underskriftsstegskomponent:** Du kan använda signaturstegskomponenten för att skapa signeringsupplevelser i formulär. Endast den första signeraren kan signera medan formuläret fylls i. När avsnittet med signaturstegskomponenten återges visas en signerbar PDF-version av formuläret. Det är vanligtvis det sista eller näst sista avsnittet följt av en sammanfattande komponent i ett formulär.

## Felsökning {#troubleshoot}

### [!DNL Adobe Sign] avtalsfel {#adobe-sign-agreement-failures}

**Problem**
När [!DNL Adobe Sign] tjänsten är konfigurerad för ett adaptivt formulär. Tjänsten kan inte skapa en [!DNL Adobe Sign] avtal för det underliggande adaptiva formuläret.

**Upplösning**

* Kontrollera [konfiguration av Adobe Sign molntjänst](../../forms/using/adobe-sign-integration-adaptive-forms.md) används i anpassningsbar form.
* Kontrollera att API-programmet [!DNL Adobe Sign] server som används för att konfigurera [!DNL Adobe Sign] Molntjänsten har nödvändig behörighet.
* Om du använder flera [!DNL Adobe Sign] Molntjänster, peka på **[!UICONTROL oAuth URL]** av alla tjänster till samma **[!UICONTROL Adobe Sign Shard]**.

* Använd separata e-postadresser för att konfigurera [!DNL Adobe Sign] konto och för den första signeraren och en enda signerare. E-postadressen till den första signeraren eller den enda signeraren (om det finns en signerare) kan inte vara identisk med [!DNL Adobe Sign] konto som används för att konfigurera AEM molntjänster.

### AEM [!DNL Forms] arbetsflöde konfigurerat för [!DNL Adobe Sign] aktiverat adaptivt formulär startar inte {#adobe-sign-aem-form-workflow-failures}

**Problem**
När [!DNL Adobe Sign] är konfigurerad för ett adaptivt formulär, arbetsflödet som konfigurerats med Anropa [!DNL Forms] Arbetsflödesalternativet startar inte.

**Upplösning**

* När du använder [!DNL Adobe Sign] utan signatursteget eller formuläret kräver signaturer från flera personer, AEM [!DNL Forms] servern väntar på att schemaläggaren ska bekräfta att alla personer har signerat formuläret. Schemaläggaren skickar det adaptiva formuläret först när alla personer har slutfört signeringen och arbetsflödet startar först när det adaptiva formuläret har skickats. Du kan korta ned intervallet för [schemaläggare](adobe-sign-integration-adaptive-forms.md) för att kontrollera status för formulärsignering med snabba intervall och snabb inskickning av formulär.


## Relaterade artiklar {#related-articles}

* [Integrera Adobe Sign med AEM Forms](../../forms/using/adobe-sign-integration-adaptive-forms.md)
* [Bästa sättet att använda Adobe Sign med adaptiva formulär](https://medium.com/adobetech/using-adobe-sign-to-e-sign-an-adaptive-form-heres-the-best-way-to-do-it-dc3e15f9b684)
* [Använda Adobe Sign med AEM Forms (video)](https://helpx.adobe.com/experience-manager/kt/forms/using/adobe-sign-integration-feature-video.html)
