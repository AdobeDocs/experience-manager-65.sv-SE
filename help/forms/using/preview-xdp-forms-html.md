---
title: Generera HTML5-förhandsgranskning av ett XDP-formulär
seo-title: Generera HTML5-förhandsgranskning av ett XDP-formulär
description: Fliken Förhandsgranska HTML i LiveCycle Designer kan användas för att förhandsgranska formulär så som de visas i en webbläsare.
seo-description: Fliken Förhandsgranska HTML i LiveCycle Designer kan användas för att förhandsgranska formulär så som de visas i en webbläsare.
uuid: cbee956f-bf2d-40c5-8e03-58fce0fa215b
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 34e6d1bc-4eca-42dc-9ae5-9a2107fbefce
docset: aem65
translation-type: tm+mt
source-git-commit: 19299fb5fc764d0e71c0ea3a5ec2286183dd6861

---


# Generera HTML5-förhandsgranskning av ett XDP-formulär{#generate-html-preview-of-an-xdp-form}

När du utformar ett formulär i AEM Forms Designer kan du, förutom att förhandsgranska PDF-återgivningen av ett formulär, även förhandsgranska en HTML5-återgivning av det. Du kan använda fliken **Förhandsgranska HTML** för att förhandsgranska ett formulär så som det skulle visas i en webbläsare.

## Aktivera HTML-förhandsgranskning för XDP-formulär i Designer {#html-preview-of-forms-in-forms-designer}

Utför följande konfigurationer om du vill att Designer ska kunna generera HTML-förhandsgranskning av XDP-formulär:

* Konfigurera autentiseringstjänsten för Apache Sling
* Inaktivera skyddat läge
* Ange information om AEM Forms-servern

### Konfigurera autentiseringstjänsten för Apache Sling {#configure-apache-sling-authentication-service}

1. Gå till `https://[server]:[port]/system/console/configMgr` AEM Forms som körs på OSGi eller
   `https://[server]:[port]/lc/system/console/configMgr` på AEM Forms som körs på JEE.
1. Leta reda på och klicka på konfigurationen för **Apache Sling Authentication Service** för att öppna den i redigeringsläge.

1. Beroende på om du kör AEM Forms på OSGi eller JEE lägger du till följande i fältet **Autentiseringskrav** :

   * AEM Forms on JEE

      * -/content/xfaforms
      * -/etc/clientlibs
   * AEM Forms on OSGi

      * -/content/xfaforms
      * -/etc/clientlibs/fd/xfaforms
   >[!NOTE]
   >
   >Kopiera inte och klistra in det angivna värdet i fältet Autentiseringskrav eftersom det kan skada specialtecknen i värdet. Skriv i stället det angivna värdet i fältet.

1. Ange ett användarnamn och lösenord i fälten **[!UICONTROL Anonymt användarnamn]** och **[!UICONTROL Anonymt användarlösenord]** . De angivna autentiseringsuppgifterna används för att hantera anonym autentisering och ge åtkomst till anonyma användare.
1. Klicka på **Spara** för att spara konfigurationen.

### Inaktivera skyddat läge {#disable-protected-mode}

Som standard är [skyddat läge](../../forms/using/get-xdp-pdf-documents-aem.md) aktiverat. Låt det vara aktiverat för produktionsmiljöerna. Du kan inaktivera det för en utvecklingsmiljö och förhandsgranska HTML5-formulär i Designer. Utför följande steg för att inaktivera den:

1. Logga in på AEM Web Console som administratör.

   * URL för AEM Forms på OSGi är `https://[server]:[port]/system/console/configMgr`
   * URL för AEM Forms på JEE är `https://[server]:[port]/lc/system/console/configMgr`

1. Öppna **[!UICONTROL Mobile Forms Configurations]** för redigering.
1. Avmarkera alternativet **[!UICONTROL Skyddat läge]** och klicka på **[!UICONTROL Spara]**.

### Ange information om AEM Forms-servern {#provide-details-of-aem-forms-server}

1. Gå till **Verktyg** > **Alternativ** i Designer.
1. I fönstret Alternativ väljer du sidan **Serveralternativ** , anger följande och klickar på **OK**.

   * **Server-URL**: URL till AEM Forms-server.

   * **HTTP-portnummer**: AEM-serverport. Standardvärdet är 4502.
   * **** HTML-förhandsgranskningskontext: Sökväg till profilen för återgivning av XFA-formulär. Följande standardprofiler används för att förhandsgranska formuläret i Designer. Du kan också ange sökvägen till en anpassad profil.

      * `/content/xfaforms/profiles/default.html` (AEM Forms on OSGi)

      * `/lc/content/xfaforms/profiles/default.html` (AEM Forms on JEE)
   * **** Forms Manager-kontext: Kontextsökväg som Forms Manager-gränssnittet distribueras till. Standardvärdena är:

      * `/aem/forms` (AEM Forms on OSGi)
      * `/lc/forms` (AEM Forms on JEE)
   **** Obs! Kontrollera att AEM Forms-servern körs. The HTML preview connects to the CRX server to *generate* a preview.

   ![Alternativ för AEM Forms Designer ](assets/server_options.png)

   Alternativ för AEM Forms Designer

1. Om du vill förhandsgranska ett formulär i HTML klickar du på fliken **Förhandsgranska HTML** .

   >[!NOTE]
   >
   >
   >
   >
   >    * Om fliken HTML-förhandsgranskning är stängd trycker du på F4 för att öppna fliken Förhandsgranska HTML. Du kan också välja Förhandsgranska HTML på Visa-menyn för att öppna fliken Förhandsgranska HTML.
   >    * HTML-förhandsvisningen stöder inte PDF-dokument, HTML-förhandsvisningen gäller bara XDP-dokument.


   >[!CAUTION]
   >
   >Om du vill testa den verkliga användarupplevelsen kan du även förhandsgranska formulären i externa webbläsare (Google Chrome, Microsoft Edge, Mozilla Firefox med flera). I varje webbläsare används en separat motor för att återge HTML, så det kan finnas vissa skillnader i hur ett formulär förhandsvisas i Designer och i en extern webbläsare.

## Testa formuläret med exempeldata {#to-preview-a-form-using-sample-data}

Designer låter dig förhandsgranska och testa formuläret med XML-exempeldata. Vi rekommenderar att du löpande testar formuläret med exempeldata och kontrollerar att ditt formulär renderas korrekt.

Om du inte har några exempeldata kan Designer skapa dem, eller så kan du skapa dem själv. (Se [Generera exempeldata för förhandsgranskning av ett formulär automatiskt](https://help.adobe.com/en_US/AEMForms/6.1/DesignerHelp/WS107c29ade9134a2c136ae6f212a1f379c94-8000.2.html#WS92d06802c76abadb-728f46ac129b395660c-7efe.2) och [Skapa exempeldata för förhandsgranskning av ett formulär](https://help.adobe.com/en_US/AEMForms/6.1/DesignerHelp/WS107c29ade9134a2c136ae6f212a1f379c94-8000.2.html#WS92d06802c76abadb-728f46ac129b395660c-7eff.2).)

Om du testar formulären med exempeldata kan du kontrollera att data och fält mappas och att upprepade delformulär upprepas som det är tänkt. Du kan skapa en balanserad formulärlayout som ger rätt utrymme för varje objekt för att visa data.

1. Select **File > Form Properties**.

1. Click the **Preview** tab and, in the Data File box, type the full path to your test data file. Du kan också använda knappen Bläddra för att navigera till filen.

1. Click **OK**. The next time you preview the form in the **Preview HTML** tab, the data values from the sample XML file will appear in the respective objects.

## Förhandsgranska formulär som finns i en databas {#html-preview-of-forms-in-forms-manager}

I AEM Forms kan du förhandsgranska formulär och dokument i en databas. Med Förhandsgranska vet du exakt hur formulären ser ut och fungerar som de kommer att användas av slutanvändarna.

[Kontakta supporten](https://www.adobe.com/account/sign-in.supportportal.html)
