---
title: Skapa en anpassad profil för HTML5-formulär
seo-title: Skapa en anpassad profil för HTML5-formulär
description: En HTML5-formulärprofil är en resursnod i Apache Sling. Den representerar en anpassad version av tjänsten HTML5 Forms Render.
seo-description: En HTML5-formulärprofil är en resursnod i Apache Sling. Den representerar en anpassad version av tjänsten HTML5 Forms Render.
uuid: b9938280-a92c-4dde-b465-04372db3ca8d
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 9cd22244-9aa6-4b5f-96cf-c9cb3d6f9c8a
translation-type: tm+mt
source-git-commit: c74d9e86727f2deda62b8d1eb105b28ef4b6d184
workflow-type: tm+mt
source-wordcount: '688'
ht-degree: 0%

---


# Skapa en anpassad profil för HTML5-formulär {#creating-a-custom-profile-for-html-forms}

En profil är en resursnod i [Apache Sling](https://sling.apache.org/). Den representerar en anpassad version av HTML5-formuläråtergivningstjänsten. Du kan använda tjänsten HTML5-formuläråtergivning för att anpassa utseende, beteende och interaktioner för HTML5-formulären. Det finns en profilnod i mappen `/content` i JCR-databasen. Du kan placera noden direkt under mappen `/content` eller en undermapp till mappen `/content`.

Profilnoden har egenskapen **sling:resourceSuperType** och standardvärdet är **xfaforms/profile**. Återgivningsskriptet för noden finns på /libs/xfaforms/profile.

Sling-skripten är JSP-skript. Dessa JSP-skript fungerar som behållare för att sätta ihop HTML för det begärda formuläret och de JS-/CSS-artefakter som krävs. Dessa Sling-skript kallas även **profilåtergivningsskript**. Profilåtergivaren anropar tjänsten Forms OSGi för att återge det begärda formuläret.

Profilskriptet finns i html.jsp och html.POST.jsp för begäranden om GET och POST. Du kan kopiera och ändra en eller flera filer för att åsidosätta och lägga till anpassningar. Gör inga ändringar på plats, så skriver uppdateringen över sådana ändringar.

En profil innehåller olika moduler. Modulerna är formRuntime.jsp, config.jsp, toolbar.jsp, formBody.jsp, nav_footer.jsp och footer.jsp.

## formRuntime.jsp {#formruntime-jsp-br}

Modulerna formRuntime.jsp innehåller referenser till klientbiblioteken. Det visar också metoder för att extrahera språkinformation från begäran och inkludera lokaliserade meddelanden i begäran. Du kan inkludera egna anpassade JavaScript-bibliotek eller -format i formRuntime.jsp.

## config.jsp {#config-jsp}

Modulen config.jsp innehåller olika konfigurationer som loggning, proxytjänster och beteendeversion. Du kan lägga till din egen konfiguration och widgetanpassning i modulen config.jsp. Du kan också lägga till konfigurationer som anpassad widgetregistrering i modulen config.jsp.

## toolbar.jsp {#toolbar-jsp}

toolbar.jsp innehåller kod för att skapa färgade verktygsfält. Om du vill ta bort verktygsfältet tar du bort toolbar.jsp från HTML.jsp

## formBody.jsp {#formbody-jsp}

Modulen formBody.jsp är avsedd för HTML-representationen av XFA-formuläret.

## nav_footer.jsp {#nav-footer-jsp}

Först återges bara formulärets första sida i HTML5-formuläret. När en användare rullar formuläret läses resten av formulären in. Det gör inläsningen snabbare. Komponenten nav_footer.jsp innehåller alla format och nödvändiga element för att underlätta inläsningen av sidorna vid rullning.

## footer.jsp {#footer-jsp}

Modulen footer.jsp är tom. Det gör att du kan lägga till skript som bara används för användarinteraktion.

## Skapar anpassade profiler {#creating-custom-profiles}

Så här skapar du en anpassad profil:

### Skapa profilnod {#create-profile-node}

1. Navigera till CRX DE-gränssnittet på URL:en: `https://'[server]:[port]'/crx/de` och logga in i gränssnittet med administratörsuppgifter.

1. I den vänstra rutan navigerar du till platsen */content/xfaforms/profiles*.

1. Kopiera nodens standardvärde och klistra in noden i en annan mapp (*/content/profiles*) med namnet *hrform*.

1. Markera den nya noden *hrform* och lägg till en strängegenskap: *sling:resourceType* med värdet: *Formulär/demo*.

1. Klicka på Spara alla på verktygsfältmenyn för att spara ändringarna.

### Skapa profilåtergivningsskriptet {#create-the-profile-renderer-script}

När du har skapat en anpassad profil lägger du till återgivningsinformation i den här profilen. När CRX tar emot en begäran om den nya profilen verifierar det att mappen /apps finns för den JSP-sida som ska återges. Skapa JSP-sidan i mappen /apps.

1. Navigera till mappen `/apps` i den vänstra rutan.
1. Högerklicka på mappen `/apps` och välj att skapa en mapp med namnet **hrform**.
1. I mappen **hrform** skapar du en mapp med namnet **demo**.
1. Klicka på knappen **Spara alla**.
1. Navigera till `/libs/xfaforms/profile/html.jsp` och kopiera noden **html.jsp**.
1. Klistra in **html.jsp**-noden i `/apps/hrform/demo`-mappen som skapats ovan med samma namn **html.jsp** och klicka på **Spara**.
1. Om du har andra komponenter i profilskriptet följer du steg 1-6 för att kopiera komponenterna i /apps/hrform/demo-mappen.

1. Verifiera att profilen har skapats genom att öppna URL:en `https://'[server]:[port]'/content/xfaforms/profiles/hrform.html`

Du kan verifiera formulären genom att [importera formulären](/help/forms/using/get-xdp-pdf-documents-aem.md) från det lokala filsystemet till AEM Forms och [förhandsgranska formuläret](/help/forms/using/previewing-forms.md) AEM serverförfattarinstansen.
