---
title: Återgivningsformulär
seo-title: Återgivningsformulär
description: 'null'
seo-description: 'null'
uuid: 68d7b7bc-7730-4a83-b7b9-ebe2a29d6c51
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/performing_service_operations_using_apis
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: operations
discoiquuid: f8749793-e53f-4812-a093-8278f480e6a8
translation-type: tm+mt
source-git-commit: 687cdacc2868de16a4df968dddedd330ce3317bb

---


# Återgivningsformulär {#rendering-forms}

**Om Forms-tjänsten**

Med Forms-tjänsten kan du skapa interaktiva klientprogram för datainhämtning som validerar, bearbetar, omvandlar och levererar formulär som vanligtvis skapas i Designer. Formulärförfattare kan utveckla en enda formulärdesign som Forms-tjänsten återger i PDF, SWF eller HTML i olika webbläsarmiljöer.

När en slutanvändare begär ett formulär skickar ett klientprogram begäran till Forms-tjänsten, som returnerar formuläret i lämpligt format. Så snart Forms-tjänsten tar emot en begäran sammanfogar den data med en formulärdesign och skickar sedan formuläret i önskat format. Utdata från formulärtjänsten är ett interaktivt formulär, vanligtvis ett PDF-dokument. Med ett interaktivt formulär kan användarna fylla i fält som finns i formuläret.

Beroende på vilken typ av klientprogram du använder kan du skriva formuläret till en webbläsare eller spara formuläret som en PDF-fil. Ett webbaserat program kan skriva formuläret till webbläsaren. Ett skrivbordsprogram kan spara formuläret som en PDF-fil. För att visa hur du skriver till en webbläsare och en PDF-fil ordnas snabbstarterna i delen *Återgivningsformulär* på följande sätt:

* Exemplen med Java API med stark typ (SOAP-läge) är en Java-servlet.
* Webbtjänstens (Java Base64) exempel är en Java-server.
* Webbtjänstexemplen (MTOM) är ett konsolprogram (alla snabbstarter har inte ett MTOM-exempel).

***Obs **: Mer information om hur du skapar ett webbprogram som använder java-servrar för att anropa Forms-tjänsten finns i[Skapa webbprogram som återger formulär](/help/forms/developing/creating-web-applications-renders-forms.md).*


Du kan skicka en formulärdesign (en XDP-fil) eller ett PDF-dokument till Forms-tjänsten på något av två sätt:

* Du kan referera till formulärdesignen med ett URL-värde. Detta innebär att använda ett `URLSpec` objekt. Innehållsroten skickas till Forms-tjänsten med hjälp av `URLSpec` objektets `setContentRootURI` metod. Formulärdesignnamnet ( `formQuery`) skickas som en separat parameter. De två värdena sammanfogas för att få den absoluta referensen till formulärdesignen. (De flesta av snabbstarterna som finns i avsnittet *Återgivningsformulär* använder den här metoden.)
* Du kan skicka en `com.adobe.idp.Document` som innehåller formulärdesignen till Forms-tjänsten. Två nya metoder som heter `renderPDFForm2` och `renderHTMLForm2` godkänner ett `com.adobe.idp.Document` objekt som innehåller en formulärdesign. (Se [Skicka dokument till formulärtjänsten](/help/forms/developing/passing-documents-forms-service.md)

Du kan utföra följande uppgifter med hjälp av Forms-tjänsten:

* Återge interaktiva PDF-formulär. (Se [Återge interaktiva PDF-formulär](/help/forms/developing/rendering-interactive-pdf-forms.md).)
* Återge formulär på klienten. (Se [Återge formulär på klienten](/help/forms/developing/rendering-forms-client.md).)
* Rendera formulär baserat på fragment. (Se [Återge formulär baserat på fragment](/help/forms/developing/rendering-forms-based-fragments.md).)
* Återge rättighetsaktiverade formulär. (Se [Rendering Rights-Enabled Forms](/help/forms/developing/rendering-rights-enabled-forms.md).)
* Återge formulär som HTML. (Se [Återge formulär som HTML](/help/forms/developing/rendering-forms-html.md).)
* Återge HTML-formulär med anpassade CSS-filer ([återge HTML-formulär med anpassade CSS-filer](/help/forms/developing/rendering-html-forms-using-custom.md)).
* Hantera skickade formulär. (Se [Hantera skickade formulär](/help/forms/developing/handling-submitted-forms.md).)
* Skapa PDF-dokument med skickade XML-data. (Se [Skapa PDF-dokument med skickade XML-data](/help/forms/developing/creating-pdf-documents-submitted-xml.md).)
* Fyll i formulär i förväg. (Se [Fylla i formulär i förväg med flödeslayouter](/help/forms/developing/prepopulating-forms-flowable-layouts.md).)
* Skicka dokument. (Se [Skicka dokument till formulärtjänsten](/help/forms/developing/passing-documents-forms-service.md)
* Beräkna formulärdata. (Se [Beräkna formulärdata](/help/forms/developing/calculating-form-data.md).)
* Optimera ett program. (Se [Optimera formulärtjänstens](/help/forms/developing/optimizing-performance-forms-service.md)prestanda.)

   ***Tips **: Adobe Developer-webbplatsen innehåller följande artikel som handlar om hur du skapar ett ASP.NET-program som anropar Forms-tjänsten och återger formulär. Se[Skapa ASP.NET-program](https://www.adobe.com/devnet/livecycle/articles/asp_net.html)för formuläråtergivning.*

