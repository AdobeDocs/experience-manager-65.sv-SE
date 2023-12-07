---
title: Generera HTML5-förhandsgranskning av ett XDP-formulär
description: Fliken Förhandsgranska HTML i LiveCycle Designer kan användas för att förhandsgranska formulär så som de visas i en webbläsare.
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
docset: aem65
feature: Mobile Forms
exl-id: 548f302b-57f0-4bdc-8a99-1a4967caa32f
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '769'
ht-degree: 0%

---

# Generera HTML5-förhandsgranskning av ett XDP-formulär{#generate-html-preview-of-an-xdp-form}

När du utformar ett formulär i AEM Forms Designer kan du, förutom att förhandsgranska PDF-återgivningen av ett formulär, även förhandsgranska en HTML 5-återgivning av det. Du kan använda **Förhandsgranska HTML** om du vill förhandsgranska ett formulär så som det skulle visas i en webbläsare.

## Aktivera HTML Preview för XDP-formulär i Designer {#html-preview-of-forms-in-forms-designer}

Gör så här om du vill att Designer ska kunna generera en förhandsgranskning av XDP-formulär i HTML:

* Konfigurera autentiseringstjänsten för Apache Sling
* Inaktivera skyddat läge
* Ange information om AEM Forms-server

### Konfigurera autentiseringstjänsten för Apache Sling {#configure-apache-sling-authentication-service}

1. Gå till `https://'[server]:[port]'/system/console/configMgr` på AEM Forms som körs på OSGi eller
   `https://'[server]:[port]'/lc/system/console/configMgr` på AEM Forms som körs på JEE.
1. Leta reda på och klicka **Autentiseringstjänst för Apache Sling** för att öppna den i redigeringsläge.

1. Beroende på om du kör AEM Forms på OSGi eller JEE lägger du till följande i **Autentiseringskrav** fält:

   * AEM Forms på JEE

      * -/content/xfaforms
      * -/etc/clientlibs

   * AEM Forms on OSGi

      * -/content/xfaforms
      * -/etc/clientlibs/fd/xfaforms

   >[!NOTE]
   >
   >Kopiera inte och klistra in det angivna värdet i fältet Autentiseringskrav eftersom det kan skada specialtecknen i värdet. Skriv i stället det angivna värdet i fältet.

1. Ange ett användarnamn och lösenord i **[!UICONTROL Anonymous User Name]** och **[!UICONTROL Anonymous User Password]** fält. De angivna autentiseringsuppgifterna används för att hantera anonym autentisering och ge åtkomst till anonyma användare.
1. Klicka **Spara** för att spara konfigurationen.

### Inaktivera skyddat läge {#disable-protected-mode}

The [skyddat läge](../../forms/using/get-xdp-pdf-documents-aem.md) är aktiverat som standard. Låt det vara aktiverat för produktionsmiljöerna. Du kan inaktivera det för en utvecklingsmiljö och förhandsgranska HTML5 Forms i Designer. Utför följande steg för att inaktivera den:

1. Logga in på AEM webbkonsol som administratör.

   * URL för AEM Forms på OSGi är `https://'[server]:[port]'/system/console/configMgr`
   * URL för AEM Forms på JEE är `https://'[server]:[port]'/lc/system/console/configMgr`

1. Öppna **[!UICONTROL Mobile Forms Configurations]** för redigering.
1. Avmarkera **[!UICONTROL Protected Mode]** och klicka **[!UICONTROL Save]**.

### Ange information om AEM Forms-server {#provide-details-of-aem-forms-server}

1. Gå till Designer **verktyg** > **Alternativ**.
1. I fönstret Alternativ väljer du **Serveralternativ** sida, ange följande information och klicka på **OK**.

   * **Server-URL**: AEM Forms server-URL.

   * **HTTP-portnummer**: AEM serverport. Standardvärdet är 4502.
   * **Förhandsvisningskontext för HTML:** Sökväg till profilen för återgivning av XFA-formulär. Följande standardprofiler används för att förhandsgranska formuläret i Designer. Du kan också ange sökvägen till en anpassad profil.

      * `/content/xfaforms/profiles/default.html` (AEM Forms on OSGi)

      * `/lc/content/xfaforms/profiles/default.html` (AEM Forms on JEE)

   * **Forms Manager Context:** Den kontextsökväg där användargränssnittet för Forms Manager distribueras. Standardvärdena är:

      * `/aem/forms` (AEM Forms on OSGi)
      * `/lc/forms` (AEM Forms on JEE)

   >[!NOTE]
   >
   >Kontrollera att AEM Forms-servern är igång. HTML-förhandsvisningen ansluter till CRX-servern till *generera* en förhandsgranskning.

   ![AEM Forms Designer-alternativ ](assets/server_options.png)

   AEM Forms Designer-alternativ

1. Om du vill förhandsgranska ett formulär i HTML klickar du på **Förhandsgranska HTML** -fliken.

   >[!NOTE]
   >
   >
   >
   >
   >    * Om fliken Förhandsgranska HTML är stängd trycker du på F4 för att öppna fliken Förhandsgranska HTML. Du kan också välja Förhandsgranska HTML på Visa-menyn för att öppna fliken Förhandsgranska HTML.
   >    * Förhandsgranskningen i HTML stöder inte PDF-dokument, HTML är bara för XDP-dokument.
   >
   >

   >[!CAUTION]
   >
   >Om du vill testa den verkliga användarupplevelsen kan du även förhandsgranska formulären i externa webbläsare (Google Chrome, Microsoft Edge, Mozilla Firefox med flera). I varje webbläsare används en separat motor för att återge HTML. Det kan därför finnas vissa skillnader i hur ett formulär förhandsvisas i Designer och i en extern webbläsare.

## Förhandsgranska ett formulär med exempeldata {#to-preview-a-form-using-sample-data}

I Designer kan du förhandsgranska och testa formuläret med XML-exempeldata. Vi rekommenderar att du ofta testar formuläret med exempeldata för att säkerställa att formuläret återges korrekt.

Om du inte har några exempeldata kan Designer skapa dem, eller så kan du skapa dem själv. (Se [Generera exempeldata automatiskt för att förhandsgranska formuläret](https://help.adobe.com/en_US/AEMForms/6.1/DesignerHelp/WS107c29ade9134a2c136ae6f212a1f379c94-8000.2.html#WS92d06802c76abadb-728f46ac129b395660c-7efe.2) och [Skapa exempeldata för att förhandsgranska formuläret](https://help.adobe.com/en_US/AEMForms/6.1/DesignerHelp/WS107c29ade9134a2c136ae6f212a1f379c94-8000.2.html#WS92d06802c76abadb-728f46ac129b395660c-7eff.2).)

Om du testar formuläret med en exempeldatakälla ser du till att data och fält mappas och att upprepade delformulär upprepas som du förväntade dig. Du kan skapa en balanserad formulärlayout som ger rätt utrymme för varje objekt för att visa sammanfogade data.

1. Välj **Arkiv > Formuläregenskaper**.

1. Klicka på **Förhandsgranska** och skriv den fullständiga sökvägen till testdatafilen i rutan Datafil. Du kan också använda knappen Bläddra för att navigera till filen.

1. Klicka **OK**. Nästa gång du förhandsgranskar formuläret i **Förhandsgranska HTML** -fliken visas datavärdena från XML-exempelfilen i respektive objekt.

## Förhandsgranska formulär i en databas {#html-preview-of-forms-in-forms-manager}

I AEM Forms kan du förhandsgranska formulär och dokument i en databas. Med Förhandsgranska kan du veta exakt hur formulären ser ut och fungerar för slutanvändarna.
