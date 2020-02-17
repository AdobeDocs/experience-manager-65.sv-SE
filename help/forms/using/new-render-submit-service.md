---
title: Ny renderings- och skicka-tjänst
seo-title: Ny renderings- och skicka-tjänst
description: Definiera renderings- och skicka-tjänster i Workbench för att återge XDP-formulär som HTML eller PDF beroende på vilken enhet det kommer åt.
seo-description: Definiera renderings- och skicka-tjänster i Workbench för att återge XDP-formulär som HTML eller PDF beroende på vilken enhet det kommer åt.
uuid: 7f8348a1-753c-4dab-87d5-4a4a301198dd
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 6a32d240-c6a6-4937-a31f-7a5ec3c60b1f
docset: aem65
translation-type: tm+mt
source-git-commit: d9975c0dcc02ae71ac64aadb6b4f82f7c993f32c

---


# Ny renderings- och skicka-tjänst{#new-render-and-submit-service}

## Introduktion {#introduction}

När du definierar en `AssignTask` åtgärd i Workbench anger du ett visst formulär (XDP- eller PDF-formulär). Ange även en uppsättning renderings- och Skicka-tjänster via en åtgärdsprofil.

En XDP kan återges som ett PDF-formulär eller ett HTML-formulär. Bland de nya funktionerna finns möjligheten att:

* Återge och skicka ett XDP-formulär som HTML
* Rendera och skicka ett XDP-formulär som PDF på datorn och som HTML på mobila enheter (till exempel en iPad)

### Ny HTML Forms-tjänst {#new-html-forms-service}

Den nya tjänsten HTML Forms använder den nya funktionen i Forms för att ge stöd för återgivning av XDP-formulär som HTML. Den nya HTML Forms-tjänsten har följande metoder:

```java
/*
 * Generates a URL (for the HTML Form) to be passed to client, given a TaskContext.
 * The output of this API is something like this - /lc/content/xfaforms/profiles/default.ws.html?ContentRoot=repository://Applications/MyApplication/MyFolder&template=MyForm.xdp
 * @param taskContext task context
 * @param profileName Forms servlet URL.
 * @return form URL string
 */
public String generateFormURL(TaskContext taskContext, String profileName);

/*
 * Render the XDP Form as HTML. Can be used directly for updating the runtimeMap in render.
 * It adds the following keys to the map -
 * hint:new html form = true
 * newHTMLFormURL = the URL returned after calling 'generateFormURL' API.
 * @param TaskContext taskContext
 * @param profileName Forms servlet URL.
 * @param runtimeMap runtime map<string,object> associated with form rendering.
 * return runtimeMap
 */
public Map<String, Object> renderHTMLForm (TaskContext taskContext, String profileName, Map<String,Object> runtimeMap);
```

Mer information om profiler för mobilformulär finns i [Skapa en anpassad profil](/help/forms/using/custom-profile.md).

## Ny HTML-formulärrendering och nya inskickningsprocesser {#new-html-form-render-amp-submit-processes}

För varje AssignTask-åtgärd anger du en renderings- och en Submit-process med formuläret. Dessa processer anropas av TaskManager `renderForm`och API: `submitForm`er för att tillåta anpassad hantering. De här processernas semantik för Nytt HTML-formulär:

### Återge ett nytt HTML-formulär {#render-a-new-html-form}

Den nya processen att återge HTML, precis som vid alla återgivningsprocesser, har följande I/O-parametrar -

Input - `taskContext`

Output - `runtimeMap`

Output - `outFormDoc`

Den här metoden simulerar det exakta beteendet hos API:t för NewHTMLFormsService `renderHTMLForm` . Det anropar API:t för att hämta URL:en för HTML-återgivning av formuläret. `generateFormURL` Därefter fylls runtimeMap i med följande nyckel eller värden:

new html form = true

newHTMLFormURL = den URL som returneras efter anrop av `generateFormURL` API.

### Skicka ett nytt HTML-formulär {#submit-a-new-html-form}

Den här processen för att skicka ett nytt HTML-formulär fungerar med följande I/O-parametrar -

Input - `taskContext`

Output - `runtimeMap`

Output - `outputDocument`

Processen ställer in värdet `outputDocument`till det som `inputDocument`hämtas från `taskContext`.

## Standardprocesser för återgivning och överföring samt åtgärdsprofiler {#default-render-or-submit-processes-and-action-profiles}

Med standardtjänsterna Återgivning och Skicka kan du återge PDF-filer på en dator och HTML på mobila enheter (iPad).

### Standardåtergivningsformulär {#default-render-form}

Den här processen återger ett XDP-formulär på flera plattformar, sömlöst. Processen hämtar användaragenten från `taskContext`och använder data för att anropa processen för att återge antingen HTML eller PDF.

![default-render-form](assets/default-render-form.png)

### Standardformulär för att skicka {#default-submit-form}

Den här processen skickar ett XDP-formulär sömlöst på flera plattformar. Den hämtar användaragenten från `taskContext`och använder data för att anropa processen för att skicka antingen HTML eller PDF.

![default-submit-form](assets/default-submit-form.png)

## Växla återgivning av mobilformulär från PDF till HTML {#switch-the-rendering-of-mobile-forms-from-pdf-to-html}

Webbläsare drar gradvis tillbaka stödet för NPAPI-baserade plugin-program, inklusive plugin-program för Adobe Acrobat och Adobe Acrobat Reader. Du kan ändra återgivning av mobilformulär från PDF till HTML genom att följa följande steg:

1. Logga in i Workbench som en giltig användare.
1. Välj **Arkiv** > **Hämta program**.

   Dialogrutan Hämta program visas.

1. Markera de program som du vill ändra återgivningen av mobilformulär för och klicka på **OK**.
1. Öppna den process som du vill ändra återgivningen för.
1. Öppna startpunkten/aktiviteten som du har som mål, navigera till avsnittet Presentation &amp; Data och klicka på **Hantera åtgärdsprofiler**.

   Dialogrutan Hantera åtgärdsprofiler visas.
1. Ändra standardåtergivningsprofilskonfigurationer från PDF till HTML och klicka på **OK**.
1. Checka in processen.
1. Upprepa stegen för att ändra återgivningen för andra processer.
1. Distribuera det program som är relevant för de processer du har ändrat.

### Standardåtgärdsprofil {#default-action-profile}

Standardåtgärdsprofilen återgav XDP-formuläret som PDF. Det här beteendet har nu ändrats så att standardåtergivningsformuläret och standardskickningsformuläret används.

Några vanliga frågor om åtgärdsprofiler är följande:

![gen_question_b_20](assets/gen_question_b_20.png) **Vilka återgivnings-/sändningsprocesser kommer att vara tillgängliga?**

* Återgivningsguide (stödlinjer är inaktuella)
* Återge formulärguide
* Återge PDF-formulär
* Återge HTML-formulär
* Återge nytt HTML-formulär (nytt)
* Standardåtergivningsformulär (nytt)

Och likvärdiga inskickningsprocesser.

![gen_question_b_20](assets/gen_question_b_20.png) **Vilka åtgärdsprofiler kommer att vara tillgängliga?**

För XDP-formulär:

* Standard (återge/skicka med de nya standardprocesserna för återgivning/sändning)

![gen_question_b_20](assets/gen_question_b_20.png) **Vad behöver processdesignern göra för att formuläret ska kunna återges i HTML på en enhet och i PDF på en dator?**

Ingenting. Standardåtgärdsprofilen väljs automatiskt och återgivningsläget hanteras automatiskt.

![gen_question_b_20](assets/gen_question_b_20.png) **Vad behöver göras för att formuläret ska kunna återges i HTML på en dator?**

Användaren måste välja HTML-alternativknappen för standardprofilen.

![gen_question_b_20](assets/gen_question_b_20.png) **Kommer uppgraderingen att påverka hur standardåtgärdsprofilen fungerar?**

Ja, eftersom de tidigare återgivnings- och skicketjänsterna som är kopplade till standardåtgärdsprofilen var olika, behandlas dessa som en anpassning av befintliga formulär. När du klickar på **Återställ standardvärden** ställs standardtjänsterna för återgivning och sändning in i stället.

Om du har ändrat befintliga tjänster för återgivning eller skickning av PDF-formulär eller skapat anpassade tjänster (till exempel custom1) och nu vill använda samma funktioner för HTML-återgivning. Du måste replikera den nya renderings- eller skicka-tjänsten (till exempel custom2) och tillämpa liknande anpassningar på dessa. Nu kan du ändra åtgärdsprofilen för XDP-filen så att den börjar använda anpassade2-tjänster i stället för custom1 för rendering eller sändning.

Vad behöver processdesignern göra för att formuläret ska kunna återges i HTML på en enhet och i PDF på en dator?
Vad behöver processdesignern göra för att formuläret ska kunna återges i HTML på en enhet och i PDF på en dator?  [Kontakta supporten](https://www.adobe.com/account/sign-in.supportportal.html)
