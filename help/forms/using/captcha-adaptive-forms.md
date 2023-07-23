---
title: Använda CAPTCHA i anpassningsbara formulär
seo-title: Using CAPTCHA in adaptive forms
description: Lär dig hur du konfigurerar AEM CAPTCHA- eller Google reCAPTCHA-tjänsten i adaptiva formulär.
seo-description: Learn how to configure AEM CAPTCHA or Google reCAPTCHA service in adaptive forms.
uuid: 0e11e98a-12ac-484c-b77f-88ebdf0f40e5
contentOwner: vishgupt
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: adaptive_forms, author
discoiquuid: 4c53dfc0-25ca-419d-abfe-cf31fc6ebf61
docset: aem65
feature: Adaptive Forms
exl-id: 9b4219b8-d5eb-4099-b205-d98d84e0c249
source-git-commit: e7a3558ae04cd6816ed73589c67b0297f05adce2
workflow-type: tm+mt
source-wordcount: '1889'
ht-degree: 0%

---

# Använda CAPTCHA i anpassningsbara formulär{#using-captcha-in-adaptive-forms}

<span class="preview"> Adobe rekommenderar att man använder modern och utbyggbar datainhämtning [Kärnkomponenter](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html) for [skapa ny Adaptive Forms](/help/forms/using/create-an-adaptive-form-core-components.md) eller [lägga till adaptiv Forms på AEM Sites-sidor](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). De här komponenterna utgör ett betydande framsteg när det gäller att skapa adaptiva Forms-program, vilket ger imponerande användarupplevelser. I den här artikeln beskrivs det äldre sättet att skapa Adaptive Forms med grundläggande komponenter. </span>

CAPTCHA (Completely Automated Public Turing test to tell Computers and Humans Apart) är ett program som ofta används vid onlinetransaktioner för att skilja mellan människor och automatiserade program eller organ. Det utgör en utmaning och utvärderar användarens svar för att avgöra om det är en människa eller en robot som interagerar med webbplatsen. Det förhindrar användaren att fortsätta om testet misslyckas och gör onlinetransaktionerna säkra genom att förhindra att skräppost eller skadliga syften publiceras.

AEM Forms har stöd för CAPTCHA i anpassningsbara formulär. Du kan använda tjänsten reCAPTCHA från Google för att implementera CAPTCHA.

>[!NOTE]
>
>* AEM Forms support reCAPTCHA v2 and enterprise. Andra versioner stöds inte.
>* CAPTCHA i adaptiva formulär stöds inte i offlineläge i AEM Forms-appen.

## Konfigurera tjänsten reCAPTCHA från Google för Adaptive Forms {#google-reCAPTCHA}

AEM Forms-användare kan använda tjänsten reCAPTCHA från Google för att implementera CAPTCHA i adaptiva formulär. Den har avancerade CAPTCHA-funktioner för att skydda er webbplats. Mer information om hur reCAPTCHA fungerar finns i [Google reCAPTCHA](https://developers.google.com/recaptcha/). reCAPTCHA-tjänsten, inklusive reCAPTCHA v2 och reCAPTCHA Enterprise, är integrerad i AEM Forms. Beroende på dina behov kan du konfigurera tjänsten reCAPTCHA för att aktivera:

* [reCAPTCHA Enterprise i AEM Forms](#steps-to-implement-reCAPTCHA-enterprise-in-forms)
* [reCAPTCHA v2 i AEM Forms](#steps-to-implement-reCAPTCHA-v2-in-forms)

![reCAPTCHA](/help/forms/using/assets/recaptcha_new.png)

### Konfigurera reCAPTCHA Enterprise  {#steps-to-implement-reCAPTCHA-enterprise-in-forms}

1. Skapa en [reCAPTCHA Enterprise project](https://cloud.google.com/recaptcha-enterprise/docs/set-up-non-google-cloud-environments-api-keys#before-you-begin) aktiverad med [reCAPTCHA Enterprise API](https://cloud.google.com/recaptcha-enterprise/docs/set-up-non-google-cloud-environments-api-keys#enable-the-recaptcha-enterprise-api).
1. [Hämta](https://support.google.com/googleapi/answer/7014113?hl=en#:~:text=To%20locate%20your%20project%20ID,a%20member%20of%20are%20displayed) projekt-ID.
1. Skapa en [API-nyckel](https://cloud.google.com/recaptcha-enterprise/docs/set-up-non-google-cloud-environments-api-keys#create_an_api_key) och [webbplatsnyckel för webbplatser](https://cloud.google.com/recaptcha-enterprise/docs/create-key#create-key).
1. Skapa konfigurationsbehållare för molntjänster.

   1. Gå till **[!UICONTROL Tools > General > Configuration Browser]**. Se [Konfigurationsläsaren](/help/sites-administering/configurations.md) mer information.
   1. Gör följande för att aktivera den globala mappen för molnkonfigurationer eller hoppa över det här steget för att skapa och konfigurera en annan mapp för molntjänstkonfigurationer.
      1. I konfigurationsläsaren väljer du **[!UICONTROL global]** mapp och tryck **[!UICONTROL Properties]**.
      1. Aktivera i dialogrutan Konfigurationsegenskaper **[!UICONTROL Cloud Configurations]**.
      1. Tryck **[!UICONTROL Save & Close]** för att spara konfigurationen och stänga dialogrutan.

   1. Tryck på **[!UICONTROL Create]**.
   1. I dialogrutan Skapa konfiguration anger du en rubrik för mappen och aktiverar **[!UICONTROL Cloud Configurations]**.
   1. Tryck **[!UICONTROL Create]** för att skapa en mapp som är aktiverad för molntjänstkonfigurationer.
1. Konfigurera molntjänsten för reCAPTCHA Enterprise.

   1. Gå till Experience Manager ![verktyg-1](assets/tools-1.png) > **[!UICONTROL Cloud Services]**.
   1. Tryck på **[!UICONTROL reCAPTCHA]**. Sidan Konfigurationer öppnas. Välj den konfigurationsbehållare som skapades i föregående steg och tryck på **[!UICONTROL Create]**.
   1. Välj version som reCAPTCHA Enterprise och ange Namn; Projekt-ID, webbplatsnyckel och API-nyckel (hämtas i steg 2 och 3) för reCAPTCHA Enterprise-tjänsten.
   1. Välj nyckeltyp. Nyckeltypen ska vara densamma som den platsnyckel som konfigurerats i Google Cloud-projektet, till exempel **Platsnyckel för kryssruta** eller **Poängbaserad webbplatsnyckel**.
   1. Ange ett tröskelvärde i intervallet 0 till 1 ([Klicka för mer information om bakgrundsmusik](https://cloud.google.com/recaptcha-enterprise/docs/interpret-assessment#interpret_scores)). Poängvärden som är större än eller lika med tröskelvärdena identifierar mänsklig interaktion, vilket i annat fall omfattar båda interaktioner.

      > Obs!
      >
      > * Formulärförfattare kan ange ett poängvärde i det intervall som passar för att skicka formulär utan avbrott.

   1. Tryck **[!UICONTROL Create]** för att skapa molntjänstkonfigurationen.

   1. I dialogrutan Redigera komponent anger du namn, projekt-ID, platsnyckel, API-nyckel (som du får i steg 2 och 3), väljer nyckeltyp och anger tröskelvärdet. Tryck **[!UICONTROL Save Settings]** och sedan trycka **[!UICONTROL OK]** för att slutföra konfigurationen.

När du har aktiverat tjänsten reCAPTCHA Enterprise kan den användas i anpassningsbara formulär. Se [använda CAPTCHA i anpassningsbara formulär](#using-reCAPTCHA).

![reCAPTCHA Enterprise](/help/forms/using/assets/recaptcha1-enterprise.png)


### Konfigurera Google reCAPTCHA v2 {#steps-to-implement-reCAPTCHA-v2-in-forms}

1. Hämta [API-nyckelpar för reCAPTCHA](https://www.google.com/recaptcha/admin) från Google. Den innehåller **webbplatsnyckel** och **hemlig nyckel**.
1. Skapa konfigurationsbehållare för molntjänster.
   1. Gå till **[!UICONTROL Tools > General > Configuration Browser]**. Se [Konfigurationsläsaren](/help/sites-administering/configurations.md) mer information.
   1. Gör följande för att aktivera den globala mappen för molnkonfigurationer eller hoppa över det här steget för att skapa och konfigurera en annan mapp för molntjänstkonfigurationer.

      1. I konfigurationsläsaren väljer du **[!UICONTROL global]** mapp och tryck **[!UICONTROL Properties]**.

      1. Aktivera i dialogrutan Konfigurationsegenskaper **[!UICONTROL Cloud Configurations]**.
      1. Tryck **[!UICONTROL Save & Close]** för att spara konfigurationen och stänga dialogrutan.

   1. Tryck på **[!UICONTROL Create]**.
   1. I dialogrutan Skapa konfiguration anger du en rubrik för mappen och aktiverar **[!UICONTROL Cloud Configurations]**.
   1. Tryck **[!UICONTROL Create]** för att skapa en mapp som är aktiverad för molntjänstkonfigurationer.

1. Konfigurera molntjänsten för reCAPTCHA v2.

   1. Gå till AEM ![verktyg-1](assets/tools-1.png) > **Cloud Services**.
   1. Tryck på **[!UICONTROL reCAPTCHA]**. Sidan Konfigurationer öppnas. Välj den konfigurationsbehållare som skapades i föregående steg och tryck på **[!UICONTROL Create]**.
   1. Välj version som reCAPTCHA v2, ange Namn; Webbplatsnyckel och Hemlig nyckel för tjänsten reCAPTCHA (hämtas i steg 1) och tryck på **[!UICONTROL Create]** för att skapa molntjänstkonfigurationen.
   1. I dialogrutan Redigera komponent anger du platsen och de hemliga nycklarna som fås i steg 1. Tryck **[!UICONTROL Save Settings]** och sedan trycka **OK** för att slutföra konfigurationen.

   När reCAPTCHA-tjänsten har konfigurerats är den tillgänglig för användning i adaptiva formulär. Mer information finns i [använda CAPTCHA i anpassningsbara formulär](#using-captcha).

![reCAPTCHA v2](/help/forms/using/assets/recaptcha-v2.png)


## Använd reCAPTCHA i anpassningsbara formulär {#using-reCAPTCHA}

Så här använder du reCAPTCHA i adaptiva former:

1. Öppna ett anpassat formulär i redigeringsläge.

   >[!NOTE]
   >
   >Kontrollera att den konfigurationsbehållare som valts när du skapar det adaptiva formuläret innehåller molntjänsten reCAPTCHA. Du kan också redigera adaptiva formuläregenskaper för att ändra konfigurationsbehållaren som är kopplad till formuläret.

1. Dra från komponentwebbläsaren och släpp **Captcha** på den adaptiva formen.

   >[!NOTE]
   >
   >Det går inte att använda mer än en Captcha-komponent i ett adaptivt formulär. Du bör inte heller använda CAPTCHA i en panel som är markerad för lazy loading eller i ett fragment.

   >[!NOTE]
   >
   >Captcha är tidskänsligt och upphör om ungefär en minut. Därför rekommenderar vi att du placerar Captcha-komponenten precis före Skicka-knappen i den anpassade formen.

1. Välj den Captcha-komponent som du har lagt till och tryck på ![cmppr](assets/cmppr.png) om du vill redigera dess egenskaper.
1. Ange en titel för CAPTCHA-widgeten. Standardvärdet är **Captcha**. Välj **Dölj titel** om du inte vill att rubriken ska visas.
1. Från **Captcha-tjänst** nedrullningsbar meny, välja **reCAPTCHA** för att aktivera tjänsten reCAPTCHA om du har konfigurerat den enligt beskrivningen i [reCAPTCHA-tjänst från Google](#google-reCAPTCHA).
1. Välj en konfiguration i listrutan Inställningar.
1. **Om den valda konfigurationen har version reCAPTCHA Enterprise**:
   1. Du kan välja molnkonfigurationen reCAPTCHA med **tangenttyp** as **kryssruta**. I kryssrutenyckeltyp visas det anpassade felmeddelandet som ett textbundet meddelande om captcha-valideringen misslyckas. Du kan välja storlek som **[!UICONTROL Normal]** och **[!UICONTROL Compact]**.
   1. Du kan välja molnkonfigurationen reCAPTCHA med **tangenttyp** as **poängbaserad**. I poängbaserad nyckeltyp visas det anpassade felmeddelandet som ett popup-meddelande om captcha-valideringen misslyckas.
   1. När du väljer en **[!UICONTROL Bind Reference]** de data som skickas är bundna, annars är de obundna data. Nedan finns XML-exempel på obundna data och bundna data (med bind referens som SSN) när ett formulär skickas.

      ```xml
          <?xml version="1.0" encoding="UTF-8" standalone="no"?>
          <afData>
          <afUnboundData>
              <data>
                  <captcha16820607953761>
                      <captchaType>reCAPTCHAEnterprise</captchaType>
                      <captchaScore>0.9</captchaScore>
                  </captcha16820607953761>
              </data>
          </afUnboundData>
          <afBoundData>
              <Root
                  xmlns:xfa="http://www.xfa.org/schema/xfa-data/1.0/"
                  xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
                  <PersonalDetails>
                      <SSN>371237912</SSN>
                      <FirstName>Sarah </FirstName>
                      <LastName>Smith</LastName>
                  </PersonalDetails>
                  <OtherInfo>
                      <City>California</City>
                      <Address>54 Residency</Address>
                      <State>USA</State>
                      <Zip>123112</Zip>
                  </OtherInfo>
              </Root>
          </afBoundData>
          <afSubmissionInfo>
              <stateOverrides/>
              <signers/>
              <afPath>/content/dam/formsanddocuments/captcha-form</afPath>
              <afSubmissionTime>20230608034928</afSubmissionTime>
          </afSubmissionInfo>
          </afData>
      ```


      ```xml
          <?xml version="1.0" encoding="UTF-8" standalone="no"?>
          <afData>
          <afUnboundData>
              <data/>
          </afUnboundData>
          <afBoundData>
              <Root
                  xmlns:xfa="http://www.xfa.org/schema/xfa-data/1.0/"
                  xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
                  <PersonalDetails>
                      <SSN>
                          <captchaType>reCAPTCHAEnterprise</captchaType>
                          <captchaScore>0.9</captchaScore>
                      </SSN>
                      <FirstName>Sarah</FirstName>
                      <LastName>Smith</LastName>
                  </PersonalDetails>
                  <OtherInfo>
                      <City>California</City>
                      <Address>54 Residency</Address>
                      <State>USA</State>
                      <Zip>123112</Zip>
                  </OtherInfo>
              </Root>
          </afBoundData>
          <afSubmissionInfo>
              <stateOverrides/>
              <signers/>
              <afPath>/content/dam/formsanddocuments/captcha-form</afPath>
              <afSubmissionTime>20230608035111</afSubmissionTime>
          </afSubmissionInfo>
          </afData>
      ```


   **Om den valda konfigurationen har version reCAPTCHA v2**:
   1. Välj storlek som **[!UICONTROL Normal]** eller **[!UICONTROL Compact]** för widgeten reCAPTCHA. Du kan också välja **[!UICONTROL Invisible]** möjlighet att visa CAPTCHA-utmaningen endast i händelse av en misstänkt aktivitet. The **skyddat av reCAPTCHA** emblemet, som visas nedan, visas på de skyddade formulären.

      ![Google skyddat av reCAPTCHA-märke](/help/forms/using/assets/google-recaptcha-v2.png)


   Tjänsten reCAPTCHA är aktiverad i det adaptiva formuläret. Du kan förhandsgranska formuläret och se hur CAPTCHA fungerar.

1. Spara egenskaperna.

>[!NOTE]
> 
> Markera inte **[!UICONTROL Default]** från listrutan Captcha-tjänst eftersom AEM CAPTCHA-tjänsten är föråldrad.

### Visa eller dölj CAPTCHA-komponent baserat på regler {#show-hide-captcha}

Du kan välja att visa eller dölja CAPTCHA-komponenten baserat på regler som du tillämpar på en komponent i ett adaptivt formulär. Tryck på komponenten, markera ![redigera regler](assets/edit-rules-icon.svg)och trycka **[!UICONTROL Create]** för att skapa en regel. Mer information om hur du skapar regler finns i [Regelredigeraren](rule-editor.md).

CAPTCHA-komponenten måste till exempel bara visas i ett adaptivt formulär om fältet Valutavärde i formuläret har ett värde över 25000.

Tryck på **[!UICONTROL Currency Value]** i formuläret och skapa följande regler:

![Visa eller dölja regler](assets/rules-show-hide-captcha.png)

>[!NOTE]
>
> * Om du väljer reCAPTCHA v2-konfiguration med storleken **[!UICONTROL Invisible]** eller reCAPTCHA Enterprise score based keys, så alternativet show/hide är inte tillämpligt.

### Validera CAPTCHA {#validate-captcha}

Du kan validera CAPTCHA i ett adaptivt formulär antingen när du skickar formuläret eller baserar CAPTCHA-valideringen på användaråtgärder och villkor.

#### Validera CAPTCHA när formulär skickas {#validation-form-submission}

Så här validerar du en CAPTCHA automatiskt när du skickar in ett adaptivt formulär:

1. Tryck på CAPTCHA-komponenten och välj ![cmppr](assets/configure-icon.svg) för att visa komponentegenskaperna.
1. I **[!UICONTROL Validate CAPTCHA]** avsnitt, markera **[!UICONTROL Validate CAPTCHA at form submission]**.
1. Tryck ![Klar](assets/save_icon.svg) för att spara komponentegenskaperna.

#### Validera CAPTCHA på användaråtgärder och villkor {#validate-captcha-user-action}

Så här validerar du en CAPTCHA baserat på villkor och användaråtgärder:

1. Tryck på CAPTCHA-komponenten och välj ![cmppr](assets/configure-icon.svg) för att visa komponentegenskaperna.
1. I **[!UICONTROL Validate CAPTCHA]** avsnitt, markera **[!UICONTROL Validate CAPTCHA on a user action]**.
1. Tryck ![Klar](assets/save_icon.svg) för att spara komponentegenskaperna.

   >[!NOTE]
   >
   >
   > Om du väljer reCAPTCHA v2-konfiguration med storleken **[!UICONTROL Invisible]** eller reCAPTCHA Enterprise score based keys, så gäller inte giltig Captcha för en användaråtgärd.

[!DNL Experience Manager Forms] innehåller `ValidateCAPTCHA` API för att validera CAPTCHA med fördefinierade villkor. Du kan anropa API:t med en anpassad skickaåtgärd eller genom att definiera regler för komponenter i ett anpassat formulär.

Följande är ett exempel på en `ValidateCAPTCHA` API för att validera CAPTCHA med fördefinierade villkor:

```javascript
if (slingRequest.getParameter("numericbox1614079614831").length() >= 5) {
        GuideCaptchaValidatorProvider apiProvider = sling.getService(GuideCaptchaValidatorProvider.class);
        String formPath = slingRequest.getResource().getPath();
        String captchaData = slingRequest.getParameter(GuideConstants.GUIDE_CAPTCHA_DATA);
        if (!apiProvider.validateCAPTCHA(formPath, captchaData).isCaptchaValid()){
            response.setStatus(400);
            return;
        }
    }
```

Exemplet anger att `ValidateCAPTCHA` API validerar bara CAPTCHA i formuläret om antalet siffror i den numeriska rutan som användaren anger när formuläret fylls i är större än 5.

**Alternativ 1: Använd [!DNL Experience Manager Forms] ValidateCAPTCHA API to validate CAPTCHA using a custom Submit Action**

Utför följande steg för att använda `ValidateCAPTCHA` API för att validera CAPTCHA med en anpassad överföringsåtgärd:

1. Lägg till skriptet som innehåller `ValidateCAPTCHA` API till anpassad skickaåtgärd. Mer information om anpassade överföringsåtgärder finns i [Skapa en anpassad Skicka-åtgärd för Adaptiv Forms](custom-submit-action-form.md).
1. Välj namnet på den anpassade Skicka-åtgärden på menyn **[!UICONTROL Submit Action]** nedrullningsbar lista i **[!UICONTROL Submission]** egenskaper för ett adaptivt formulär.
1. Tryck på **[!UICONTROL Submit]**. CAPTCHA valideras baserat på de villkor som definieras i `ValidateCAPTCHA` API för den anpassade åtgärden Skicka.

**Alternativ 2: Använd [!DNL Experience Manager Forms] Validera CAPTCHA API för att validera CAPTCHA på en användaråtgärd innan formuläret skickas**

Du kan också anropa `ValidateCAPTCHA` API genom att tillämpa regler på en komponent i ett adaptivt formulär.

Du kan till exempel lägga till en **[!UICONTROL Validate CAPTCHA]** i ett adaptivt formulär och skapa en regel som anropar en tjänst genom att klicka på en knapp.

Följande bild visar hur du kan anropa en tjänst genom att klicka på en **[!UICONTROL Validate CAPTCHA]** knapp:

![Validera CAPTCHA](assets/captcha-validation1.gif)

Du kan anropa den anpassade servern som innehåller `ValidateCAPTCHA` API med regelredigeraren och aktivera eller inaktivera skicka-knappen för det adaptiva formuläret baserat på valideringsresultatet.

På samma sätt kan du använda regelredigeraren för att inkludera en anpassad metod för att validera CAPTCHA i ett adaptivt formulär.

### Lägg till anpassade CAPTCHA-tjänster {#add-custom-captcha-service}

[!DNL Experience Manager Forms] tillhandahåller reCAPTCHA som CAPTCHA-tjänst. Du kan dock lägga till en anpassad tjänst som ska visas i **[!UICONTROL CAPTCHA Service]** nedrullningsbar lista.

Nedan följer ett exempel på en implementering av gränssnittet för att lägga till ytterligare CAPTCHA-tjänst i ditt adaptiva formulär:

```javascript
package com.adobe.aemds.guide.service;

import org.osgi.annotation.versioning.ConsumerType;

/**
 * An interface to provide captcha validation at server side in Adaptive Form
 * This interface can be used to provide custom implementation for different captcha services.
 */
@ConsumerType
public interface GuideCaptchaValidator {
    /**
     * This method should define the actual validation logic of the captcha
     * @param captchaPropertyNodePath path to the node with CAPTCHA configurations inside form container
     * @param userResponseToken  The user response token provided by the CAPTCHA from client-side
     *
     * @return  {@link GuideCaptchaValidationResult} validation result of the captcha
     */
     GuideCaptchaValidationResult validateCaptcha(String captchaPropertyNodePath, String userResponseToken);

    /**
     * Returns the name of the captcha validator. This should be unique among the different implementations
     * @return  name of the captcha validator
     */
     String getCaptchaValidatorName();
}
```

`captchaPropertyNodePath` Hänvisar till resurssökvägen för CAPTCHA-komponenten i Sling-databasen. Använd den här egenskapen om du vill ta med information som är specifik för CAPTCHA-komponenten. Till exempel: `captchaPropertyNodePath` innehåller information om reCAPTCHA-molnkonfigurationen som konfigurerats för CAPTCHA-komponenten. Molnkonfigurationsinformationen innehåller **[!UICONTROL Site Key]** och **[!UICONTROL Secret Key]** inställningar för implementering av tjänsten reCAPTCHA.

`userResponseToken` Hänvisar till `g_reCAPTCHA_response` som genereras när en CAPTCHA har lösts i ett formulär.
