---
title: Skapa en anpassad profil för HTML5-formulär
description: En HTML5-formulärprofil är en resursnod i Apache Sling. Den representerar en anpassad version av HTML5-formuläråtergivningstjänsten.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 9cd22244-9aa6-4b5f-96cf-c9cb3d6f9c8a
feature: HTML5 Forms
exl-id: cf86c810-c466-4894-acc2-d4faf49754cc
source-git-commit: 524475c8f9dbd02bae30ecd558a376505fbe0aed
workflow-type: tm+mt
source-wordcount: '656'
ht-degree: 0%

---

# Skapa en anpassad profil för HTML5-formulär {#creating-a-custom-profile-for-html-forms}

En profil är en resursnod i [Apache Sling](https://sling.apache.org/). Den representerar en anpassad version av formuläråtergivningstjänsten HTML5. Du kan använda HTML5-formuläråtergivningstjänsten för att anpassa utseende, beteende och interaktioner för HTML5-formulären. Det finns en profilnod i `/content` i JCR-databasen. Du kan placera noden direkt under `/content` mapp eller undermapp till `/content` mapp.

Profilnoden har **sling:resourceSuperType** egenskapen och standardvärdet är **xfaforms/profile**. Återgivningsskriptet för noden finns på /libs/xfaforms/profile.

Sling-skripten är JSP-skript. Dessa JSP-skript fungerar som behållare för att sätta ihop HTML för det begärda formuläret och nödvändiga JS-/CSS-artefakter. Dessa Sling-skript kallas också **Profilåtergivningsskript**. Profilåtergivaren anropar tjänsten Forms OSGi för att återge det begärda formuläret.

Profilskriptet finns i html.jsp och html.POST.jsp för begäranden om GET och POST. Du kan kopiera och ändra en eller flera filer för att åsidosätta och lägga till anpassningar. Gör inga ändringar på plats, så skriver uppdateringen över sådana ändringar.

En profil innehåller olika moduler. Modulerna är formRuntime.jsp, config.jsp, toolbar.jsp, formBody.jsp, nav_footer.jsp och footer.jsp.

## formRuntime.jsp {#formruntime-jsp-br}

Modulerna formRuntime.jsp innehåller referenser till klientbiblioteken. Det visar också metoder för att extrahera språkinformation från begäran och inkludera lokaliserade meddelanden i begäran. Du kan inkludera egna anpassade JavaScript-bibliotek eller -format i formRuntime.jsp.

## config.jsp {#config-jsp}

Modulen config.jsp innehåller olika konfigurationer som loggning, proxytjänster och beteendeversion. Du kan lägga till din egen konfiguration och widgetanpassning i modulen config.jsp. Du kan också lägga till konfigurationer som anpassad widgetregistrering i modulen config.jsp.

## toolbar.jsp {#toolbar-jsp}

toolbar.jsp innehåller kod för att skapa färgade verktygsfält. Om du vill ta bort verktygsfältet tar du bort toolbar.jsp från HTML.jsp

## formBody.jsp {#formbody-jsp}

Modulen formBody.jsp är till för HTML-representationen av XFA-formuläret.

## nav_footer.jsp {#nav-footer-jsp}

Först återges bara den första sidan i formuläret HTML5. När en användare rullar formuläret läses resten av formulären in. Det gör inläsningen snabbare. Komponenten nav_footer.jsp innehåller alla format och nödvändiga element för att underlätta inläsningen av sidorna vid rullning.

## footer.jsp {#footer-jsp}

Modulen footer.jsp är tom. Här kan du lägga till skript som bara används för användarinteraktion.

## Skapa anpassade profiler {#creating-custom-profiles}

Så här skapar du en anpassad profil:

### Skapa profilnod {#create-profile-node}

1. Navigera till CRX DE-gränssnittet på URL:en: `https://'[server]:[port]'/crx/de` och logga in i gränssnittet med administratörsuppgifter.

1. Navigera till platsen i den vänstra rutan */content/xfaforms/profiles*.

1. Kopiera nodens standardvärde och klistra in noden i en annan mapp (*/content/profiles*) med namn *formulär*.

1. Välj den nya noden, *formulär* och lägga till en strängegenskap: *sling:resourceType* med värde: *Våga/demo*.

1. Klicka på Spara alla på verktygsfältmenyn för att spara ändringarna.

### Skapa profilåtergivningsskriptet {#create-the-profile-renderer-script}

När du har skapat en anpassad profil lägger du till återgivningsinformation i den här profilen. När CRX tar emot en begäran om den nya profilen verifierar det att mappen /apps finns för den JSP-sida som ska återges. Skapa JSP-sidan i mappen /apps.

1. I den vänstra rutan navigerar du till `/apps` mapp.
1. Högerklicka på `/apps` mapp och välj att skapa en mapp med namnet **formulär**.
1. Insider **formulär** mapp skapa en mapp med namnet **demo**.
1. Klicka på **Spara alla** -knappen.
1. Navigera till `/libs/xfaforms/profile/html.jsp` och kopiera noden **html.jsp**.
1. Klistra in **html.jsp** noden i `/apps/hrform/demo` mapp skapad ovan med samma namn **html.jsp** och klicka **Spara**.
1. Om du har andra komponenter i profilskriptet följer du steg 1-6 för att kopiera komponenterna i /apps/hrform/demo-mappen.

1. Kontrollera att profilen har skapats genom att öppna URL `https://'[server]:[port]'/content/xfaforms/profiles/hrform.html`

För att verifiera formulären [Importera formulär](/help/forms/using/get-xdp-pdf-documents-aem.md) från det lokala filsystemet till AEM Forms och [förhandsgranska formuläret](/help/forms/using/previewing-forms.md) AEM serverförfattarinstans.
