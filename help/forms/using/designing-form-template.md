---
title: Utforma formulärmallar för HTML5-formulär
seo-title: Utforma formulärmallar för HTML5-formulär
description: AEM Forms erbjuder återgivning av XFA-formulärmallar till HTML5-format. Formulärdesigners kan utforma formulärmallar med Designer och använda HTML5-återgivningsfunktionen.
seo-description: AEM Forms erbjuder återgivning av XFA-formulärmallar till HTML5-format. Formulärdesigners kan utforma formulärmallar med Designer och använda HTML5-återgivningsfunktionen.
uuid: 4f6b7231-4479-400a-adcd-c68064f06b4e
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: f2e9dbe4-e210-41f3-8878-2fc4d166e63c
docset: aem65
translation-type: tm+mt
source-git-commit: 147c50adb02b48be8e3aba760dbac309ab49badf

---


# Utforma formulärmallar för HTML5-formulär{#designing-form-templates-for-html-forms}

HTML5-formulärkomponenten i AEM erbjuder återgivning av XFA-formulärmallar till HTML5-format. Formulärdesigners kan utforma formulärmallar med [Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63) och använda HTML5-återgivningsfunktionen. Dessa formulärmallar, tillsammans med deras resurser, kan finnas i AEM-databasen, filsystemet eller visas via http. Men om du tänker hantera dina formulär med Forms Manager bör mallarna och resurserna finnas i AEM-databasen.

Även om HTML5-formulär i stor utsträckning matchar beteendet i PDF-formulären finns det vissa funktioner i båda formaten som inte kan användas i det andra formatet. Hur streckkoder tillämpas på ett PDF-formulär i Adobe Reader varierar till exempel från ett mobilformulär eller hur ett formulär signeras digitalt varierar också mellan formaten. Mer information om sådana variationer finns i [Funktionsdifferentiering mellan HTML5-formulär och PDF-formulär](../../forms/using/feature-differentiation-html5-forms-pdf-forms.md).

Vanliga XFA-funktioner finns i följande metodtips och riktlinjer för att utforma ett formulär som fungerar i båda formaten.

## God praxis {#best-practices}

De flesta stegen för att utforma en formulärmall, som schemabindningar eller skrivning av formulärlogik, är desamma. På grund av skillnader mellan återgivnings- och skriptmotorn i en tjock klient som Adobe Reader och webbläsarbaserade formulär finns det dock rekommendationer som beskrivs i artikeln om [god praxis](/help/forms/using/design-accessible-html5-forms.md) . De bästa sätten att utforma formulärmallar så att de fungerar som förväntat i båda formaten.

### Funktioner i AEM Forms Designer för HTML5-formulär {#capabilities-in-aem-forms-designer-for-html-forms}

#### Förhandsgranska HTML {#preview-html}

Fliken Förhandsgranska HTML läggs till i designläget för formulärdesigners för att förhandsgranska formulär i HTML5-format under designprocessen. Mer information om hur du aktiverar och konfigurerar den här funktionen i AEM Forms Designer finns i [Förhandsgranska HTML](../../forms/using/preview-xdp-forms-html.md).

#### Klottra signaturer {#scribble-signature}

Huvudmålet för HTML5-formulär är pekenheter. Därför har en ny kontroll för signering i klotter lagts till i AEM Forms Designer. Du kan klicka på eller dra och släppa kontrollen för signering av skript på formulärmallen och konfigurera den. Det återges som ett klottrigt fält i HTML5-rendering och kan användas för att klottra signaturer på enheter med pekskärm. På stationära datorer kan den användas som ett klotterfält med hjälp av muskontroll. Mer information om hur du använder den här funktionen finns i [XFA-skriptfält](../../forms/using/scribble-signature.md).

![4](assets/4.png)

#### RTF-format {#rich-text-format}

Definiera ett RTF-fältformat för textfältet i Forms Designer om du vill lägga till en lista med formateringsalternativ för fältet i det återgivna HTML5-formuläret. Tillämpa inställningarna genom att trycka på textfältet i **[!UICONTROL designvyn]**. Välj **[!UICONTROL RTF]** i listrutan **[!UICONTROL Fältformat]** på fliken **[!UICONTROL Fält]** . Textfältet visar formateringsalternativ när det återges i ett HTML5-formulär.

[Kontakta supporten](https://www.adobe.com/account/sign-in.supportportal.html)
