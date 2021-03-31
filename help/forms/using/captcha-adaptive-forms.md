---
title: Använda CAPTCHA i anpassningsbara formulär
seo-title: Använda CAPTCHA i anpassningsbara formulär
description: Lär dig hur du konfigurerar AEM CAPTCHA- eller Google reCAPTCHA-tjänsten i adaptiva formulär.
seo-description: Lär dig hur du konfigurerar AEM CAPTCHA- eller Google reCAPTCHA-tjänsten i adaptiva formulär.
uuid: 0e11e98a-12ac-484c-b77f-88ebdf0f40e5
contentOwner: vishgupt
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: adaptive_forms, author
discoiquuid: 4c53dfc0-25ca-419d-abfe-cf31fc6ebf61
docset: aem65
feature: Adaptiv Forms
translation-type: tm+mt
source-git-commit: 7a3f54d90769708344e6751756b2a12ac6c962d7
workflow-type: tm+mt
source-wordcount: '1241'
ht-degree: 0%

---


# Använda CAPTCHA i adaptiva former{#using-captcha-in-adaptive-forms}

CAPTCHA (Completely Automated Public Turing test to tell Computers and Humans Apart) är ett program som ofta används vid onlinetransaktioner för att skilja mellan människor och automatiserade program eller organ. Det utgör en utmaning och utvärderar användarens svar för att avgöra om det är en människa eller en robot som interagerar med webbplatsen. Det förhindrar användaren att fortsätta om testet misslyckas och gör onlinetransaktionerna säkra genom att förhindra att skräppost eller skadliga syften publiceras.

AEM Forms stöder CAPTCHA i adaptiva former. Du kan använda tjänsten reCAPTCHA av Google för att implementera CAPTCHA.

>[!NOTE]
>
>* AEM Forms har endast stöd för reCaptcha v2. Andra versioner stöds inte.
>* CAPTCHA i adaptiva formulär stöds inte i offlineläge i AEM Forms-appen.

>



## Konfigurera ReCAPTCHA-tjänsten av Google {#google-recaptcha}

Formulärförfattare kan använda tjänsten reCAPTCHA av Google för att implementera CAPTCHA i anpassningsbara formulär. Den har avancerade CAPTCHA-funktioner för att skydda er webbplats. Mer information om hur reCAPTCHA fungerar finns i [Google reCAPTCHA](https://developers.google.com/recaptcha/).

![Recaptcha](assets/recaptcha_new.png)

Så här implementerar du tjänsten reCAPTCHA i AEM Forms:

1. Hämta [reCAPTCHA API-nyckelpar](https://www.google.com/recaptcha/admin) från Google. Den innehåller en webbplatsnyckel och hemlighet.
1. Skapa konfigurationsbehållare för molntjänster.

   1. Gå till **[!UICONTROL Tools > General > Configuration Browser]**.
      * Mer information finns i [Configuration Browser](/help/sites-administering/configurations.md)-dokumentationen.
   1. Gör följande för att aktivera den globala mappen för molnkonfigurationer eller hoppa över det här steget för att skapa och konfigurera en annan mapp för molntjänstkonfigurationer.

      1. Markera mappen **[!UICONTROL global]** i Configuration Browser och tryck på **[!UICONTROL Properties]**.

      1. Aktivera **[!UICONTROL Cloud Configurations]** i dialogrutan Konfigurationsegenskaper.
      1. Tryck på **[!UICONTROL Save & Close]** för att spara konfigurationen och stänga dialogrutan.
   1. Tryck på **[!UICONTROL Create]** i Configuration Browser.
   1. I dialogrutan Skapa konfiguration anger du en rubrik för mappen och aktiverar **[!UICONTROL Cloud Configurations]**.
   1. Tryck på **[!UICONTROL Create]** för att skapa mappen som är aktiverad för molntjänstkonfigurationer.


1. Konfigurera molntjänsten för reCAPTCHA.

   1. Gå till ![tools-1](assets/tools-1.png) > **Cloud Services** på AEM författarinstans.
   1. Tryck på **[!UICONTROL reCAPTCHA]**. Sidan Konfigurationer öppnas. Välj den konfigurationsbehållare som skapades i föregående steg och tryck på **[!UICONTROL Create]**.
   1. Ange Namn, Webbplatsnyckel och Hemlig nyckel för reCAPTCHA-tjänsten och tryck på **[!UICONTROL Create]** för att skapa molntjänstkonfigurationen.
   1. I dialogrutan Redigera komponent anger du platsen och de hemliga nycklarna som fås i steg 1. Tryck på **Spara inställningar** och tryck sedan på **OK** för att slutföra konfigurationen.

   När reCAPTCHA-tjänsten har konfigurerats är den tillgänglig för användning i adaptiva formulär. Mer information finns i [Använda CAPTCHA i adaptiva formulär](#using-captcha).

## Använd CAPTCHA i anpassningsbara formulär {#using-captcha}

Så här använder du CAPTCHA i adaptiva former:

1. Öppna ett anpassat formulär i redigeringsläge.

   >[!NOTE]
   >
   >Kontrollera att den konfigurationsbehållare som valts när du skapar det adaptiva formuläret innehåller molntjänsten reCAPTCHA. Du kan också redigera adaptiva formuläregenskaper för att ändra konfigurationsbehållaren som är kopplad till formuläret.

1. Dra och släpp komponenten **Captcha** från komponentwebbläsaren till det adaptiva formuläret.

   >[!NOTE]
   >
   >Det går inte att använda mer än en Captcha-komponent i ett adaptivt formulär. Du bör inte heller använda CAPTCHA i en panel som är markerad för lazy loading eller i ett fragment.

   >[!NOTE]
   >
   >Captcha är tidskänsligt och upphör om ungefär en minut. Därför rekommenderar vi att du placerar Captcha-komponenten precis före Skicka-knappen i den anpassade formen.

1. Markera den Captcha-komponent som du har lagt till och tryck på ![cmpr](assets/cmppr.png) för att redigera dess egenskaper.
1. Ange en titel för CAPTCHA-widgeten. Standardvärdet är **Captcha**. Välj **Dölj titel** om du inte vill att titeln ska visas.
1. I listrutan **Captcha service** väljer du **reCaptcha** för att aktivera reCAPTCHA-tjänsten om du har konfigurerat den enligt beskrivningen i [ReCAPTCHA-tjänsten av Google](#google-recaptcha). Välj en konfiguration i listrutan Inställningar. Välj också storleken som **Normal** eller **Compact** för widgeten reCAPTCHA.

   >[!NOTE]
   >
   >Välj inte **[!UICONTROL Default]** i listrutan för Captcha-tjänsten eftersom AEM CAPTCHA-tjänsten är föråldrad.

1. Spara egenskaperna.

Tjänsten reCAPTCHA är aktiverad i det adaptiva formuläret. Du kan förhandsgranska formuläret och se hur CAPTCHA fungerar.

### Visa eller dölj CAPTCHA-komponent baserat på regler {#show-hide-captcha}

Du kan välja att visa eller dölja CAPTCHA-komponenten baserat på regler som du tillämpar på en komponent i ett adaptivt formulär. Tryck på komponenten, välj ![redigera regler](assets/edit-rules-icon.svg) och tryck på **[!UICONTROL Create]** för att skapa en regel. Mer information om hur du skapar regler finns i [Regelredigeraren](rule-editor.md).

CAPTCHA-komponenten måste till exempel bara visas i ett adaptivt formulär om fältet Valutavärde i formuläret har ett värde över 25000.

Tryck på fältet **[!UICONTROL Currency Value]** i formuläret och skapa följande regler:

![Visa eller dölja regler](assets/rules-show-hide-captcha.png)

### Validera CAPTCHA {#validate-captcha}

Du kan validera CAPTCHA i ett adaptivt formulär antingen när du skickar formuläret eller baserar CAPTCHA-valideringen på användaråtgärder och villkor.

#### Validera CAPTCHA när formulär skickas {#validation-form-submission}

Så här validerar du en CAPTCHA automatiskt när du skickar in ett adaptivt formulär:

1. Tryck på CAPTCHA-komponenten och välj ![cmpr](assets/configure-icon.svg) för att visa komponentegenskaperna.
1. I avsnittet **[!UICONTROL Validate CAPTCHA]** väljer du **[!UICONTROL Validate CAPTCHA at form submission]**.
1. Tryck på ![Klar](assets/save_icon.svg) för att spara komponentegenskaperna.

#### Validera CAPTCHA för användaråtgärder och villkor {#validate-captcha-user-action}

Så här validerar du en CAPTCHA baserat på villkor och användaråtgärder:

1. Tryck på CAPTCHA-komponenten och välj ![cmpr](assets/configure-icon.svg) för att visa komponentegenskaperna.
1. I avsnittet **[!UICONTROL Validate CAPTCHA]** väljer du **[!UICONTROL Validate CAPTCHA on a user action]**.
1. Tryck på ![Klar](assets/save_icon.svg) för att spara komponentegenskaperna.

[!DNL Experience Manager Forms] innehåller  `ValidateCAPTCHA` API för att validera CAPTCHA med fördefinierade villkor. Du kan anropa API:t med en anpassad skickaåtgärd eller genom att definiera regler för komponenter i ett anpassat formulär.

Följande är ett exempel på ett `ValidateCAPTCHA`-API för att validera CAPTCHA med fördefinierade villkor:

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

Exemplet visar att API:t `ValidateCAPTCHA` bara validerar CAPTCHA i formuläret om antalet siffror i den numeriska rutan som användaren anger när formuläret fylls i är större än 5.

**Alternativ 1: Använd API:t  [!DNL Experience Manager Forms] ValidateCAPTCHA för att validera CAPTCHA med en anpassad överföringsåtgärd**

Utför följande steg för att använda API:t `ValidateCAPTCHA` för att validera CAPTCHA med en anpassad skickaåtgärd:

1. Lägg till skriptet som innehåller API:t `ValidateCAPTCHA` till en anpassad skickaåtgärd. Mer information om anpassade Skicka-åtgärder finns i [Skapa en anpassad Skicka-åtgärd för adaptiv Forms](custom-submit-action-form.md).
1. Välj namnet på den anpassade skickaåtgärden i listrutan **[!UICONTROL Submit Action]** i **[!UICONTROL Submission]**-egenskaperna för ett anpassat formulär.
1. Tryck på **[!UICONTROL Submit]**. CAPTCHA valideras baserat på villkoren som definieras i `ValidateCAPTCHA` API för den anpassade åtgärden Skicka.

**Alternativ 2: Använd API:t  [!DNL Experience Manager Forms] ValidateCAPTCHA för att validera CAPTCHA på en användaråtgärd innan formuläret skickas**

Du kan också anropa `ValidateCAPTCHA` API genom att tillämpa regler på en komponent i ett adaptivt formulär.

Du kan till exempel lägga till en **[!UICONTROL Validate CAPTCHA]**-knapp i ett adaptivt formulär och skapa en regel som anropar en tjänst genom att klicka på en knapp.

Följande bild visar hur du kan anropa en tjänst genom att klicka på en **[!UICONTROL Validate CAPTCHA]**-knapp:

![Validera CAPTCHA](assets/captcha-validation1.gif)

Du kan anropa den anpassade servern som innehåller `ValidateCAPTCHA` API med regelredigeraren och aktivera eller inaktivera skicka-knappen för det anpassade formuläret baserat på valideringsresultatet.

På samma sätt kan du använda regelredigeraren för att inkludera en anpassad metod för att validera CAPTCHA i ett adaptivt formulär.

### Lägg till anpassade CAPTCHA-tjänster {#add-custom-captcha-service}

[!DNL Experience Manager Forms] tillhandahåller reCAPTCHA som CAPTCHA-tjänst. Du kan dock lägga till en anpassad tjänst som ska visas i listrutan **[!UICONTROL CAPTCHA Service]**.

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

`captchaPropertyNodePath` refererar till resurssökvägen för CAPTCHA-komponenten i Sling-databasen. Använd den här egenskapen om du vill ta med information som är specifik för CAPTCHA-komponenten. `captchaPropertyNodePath` innehåller till exempel information för molnkonfigurationen reCAPTCHA som konfigurerats för CAPTCHA-komponenten. Molnkonfigurationsinformationen innehåller **[!UICONTROL Site Key]**- och **[!UICONTROL Secret Key]**-inställningar för implementering av tjänsten reCAPTCHA.

`userResponseToken` refererar till  `g_recaptcha_response` som genereras efter att en CAPTCHA har lösts i ett formulär.
