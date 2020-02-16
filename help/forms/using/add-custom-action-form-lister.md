---
title: Lägga till anpassad åtgärd för formulärlisteobjekt
seo-title: Lägga till anpassad åtgärd för formulärlisteobjekt
description: Formulärutvecklare kan lägga till fler åtgärder i formulärportalsidan. Som standard kan du använda formulärlistan för att öppna formuläret, fylla i det och skicka det.
seo-description: Formulärutvecklare kan lägga till fler åtgärder i formulärportalsidan. Som standard kan du använda formulärlistan för att öppna formuläret, fylla i det och skicka det.
uuid: 5703ba27-7fb8-482e-b933-a060574165dc
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
discoiquuid: c34dd4c2-5fff-4355-b86d-cc8a956dd8af
docset: aem65
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65

---


# Lägga till anpassad åtgärd för formulärlisteobjekt{#adding-custom-action-on-form-lister-items}

I AEM Forms kan du skapa en portalsida med de tillgängliga formulären. Som standard kan du söka efter och visa formulär på en portalsida. Du kan öppna formulär för att fylla i och skicka in dina uppgifter. Endast återgivningsåtgärder anges i rutan för formulär som visas på en portalsida. Mer information om tillgängliga åtgärder på en portalsida finns i [Skapa en formulärportalsida](../../forms/using/creating-form-portal-page.md).

Du kan lägga till andra alternativ på portalsidan. Dessa alternativ eller åtgärder kan anpassas genom att du anpassar mallen för formulärportalen.

I den här artikeln beskrivs hur du skapar en knapp för att skicka länken till ett formulär direkt från en formulärportalsida. För den här anpassningen krävs att mallen för komponenten Sök efter och visa uppdateras.

Nedan finns den kod som krävs för att lägga till åtgärden i mallen. Attributet `onclick` i kodfragmentet har ett skript som skickar en länk till ett formulär via e-post.

```mxml
<div class="__FP_boxes-container __FP_single-color">
    <div class="boxes __FP_boxes __FP_single-color" data-repeatable="true">
  <div class="__FP_boxes-thumbnail">
            <img src ="${contextPath}${path}/jcr:content/renditions/cq5dam.thumbnail.319.319.png">
        </div>
        <h3 class="__FP_single-color" title="${name}" tabindex="0">${name}</h3>
        <p>${description}</p>
        <div class="boxes-icon-cont __FP_boxes-icon-cont">
            <div class="op-dow">
                <a href="${formUrl}" target="_blank" class="__FP_button ${htmlStyle}" title="${config-htmlLinkText}">Apply</a>
                <a class="__FP_button" title="Email a friend" href="#" onclick="javascript:window.location=&apos;mailto:?subject=Interesting information&body=I thought you might find {name} form helpful :  &apos;+window.location.protocol+window.location.host+&apos;${formUrl}&apos; ;">Email</a>
                <a href="${pdfUrl}" class="__FP_button ${pdfStyle}" title="${config-pdfLinkText}">Download</a>
            </div>
        </div>
    </div>
</div>
```

Du kan lägga till liknande åtgärder i den anpassade mallen. Om du vill definiera en JavaScript-funktion lägger du till funktionen på ett skript på sidnivå och länkar den med det HTML-element som krävs. I exemplet ovan är `onclick` uttrycket den länkade funktionen.

När du har redigerat mallen innehåller exempelportalsidan en knapp för att skicka länken till formuläret via e-post, vilket visas nedan.

![e-post](assets/email.png)

