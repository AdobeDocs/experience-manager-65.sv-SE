---
title: Komponentsidladdning
seo-title: Komponentsidladdning
description: Webbgruppskomponentsideloading är användbart när en webbsida är utformad som en enkel enkelsidig app som dynamiskt ändrar vad som visas beroende på vad som valts av webbplatsbesökaren
seo-description: Webbgruppskomponentsideloading är användbart när en webbsida är utformad som en enkel enkelsidig app som dynamiskt ändrar vad som visas beroende på vad som valts av webbplatsbesökaren
uuid: 8c9a5fde-26a3-4610-bc14-f8b665059015
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: a9cb5294-e5ab-445b-b7c2-ffeecda91c50
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Komponentsidladdning {#component-sideloading}

## Översikt {#overview}

Webbgruppskomponentsideloading är användbart när en webbsida är utformad som en enkel app för en sida som dynamiskt ändrar vad som visas beroende på vad besökaren väljer.

Detta görs när komponenterna i Communities inte finns i sidmallen, utan läggs till dynamiskt efter en besökares val.

Eftersom det sociala ramverket (SCF) har en liten närvaro registreras endast SCF-komponenter som finns vid den första sidinläsningen. För att en dynamiskt tillagd SCF-komponent ska kunna registreras efter sidinläsningen måste SCF anropas för att komponenten ska kunna&quot;sidläsas in&quot;.

När en sida är utformad för att läsa in webbgruppskomponenter sida vid sida går det att cachelagra hela sidan.

Stegen för att lägga till SCF-komponenter dynamiskt är:

1. [Lägg till komponenten i DOM](#dynamically-add-component-to-dom)

1. [Läs in komponenten](#sideload-by-invoking-scf) separat med en av två metoder:

* [Dynamisk inkludering](#dynamic-inclusion)
   * Boostrap alla dynamiskt tillagda komponenter
* [Dynamisk inläsning](#dynamic-loading)
   * Lägg till en specifik komponent på begäran

>[!NOTE]
>
>Inläsning av [icke-befintliga resurser](scf.md#add-or-include-a-communities-component) stöds inte.

## Lägg till komponent dynamiskt i DOM {#dynamically-add-component-to-dom}

Om komponenten inkluderas dynamiskt eller läses in dynamiskt måste den först läggas till i DOM.

När du lägger till SCF-komponenten är den vanligaste taggen DIV-taggen, men även andra taggar kan användas. Eftersom SCF endast undersöker DOM när sidan läses in första gången, kommer detta tillägg i DOM att passera obemärkt tills SCF anropas explicit.

Oavsett vilken tagg som används måste elementet åtminstone överensstämma med det vanliga SCF-rotelementmönstret genom att innehålla dessa två attribut:

* **data-component-id** Den effektiva sökvägen till den tillagda komponenten

* **data-scf-component** Komponentens resourceType

Här följer ett exempel på en kommenteringskomponent:

```xml
<div
    class="scf-commentsystem scf translation-commentsystem"
    data-component-id="<%= currentPage.getPath()%>/jcr:content/content-left/comments"
    data-scf-component="social/commons/components/hbs/comments"
>
</div>
```

## Inläsning via anrop av SCF {#sideload-by-invoking-scf}

### Dynamisk inkludering {#dynamic-inclusion}

Dynamisk inkludering använder en boostrap-begäran som resulterar i att SCF undersöker DOM och startar alla SCF-komponenter som finns på sidan.

Om du vill initiera SCF-komponenter när som helst efter sidinläsningen startar du en JQuery-händelse som den här:

$(document).trigger(SCF.events.BOOTSTRAP_REQUEST);

### Dynamisk inläsning {#dynamic-loading}

Dynamisk inläsning ger kontroll över inläsningen av SCF-komponenter.

I stället för att starta alla SCF-komponenter som finns i DOM kan du ange en specifik SCF-komponent som ska läsas in med den här JavaScript-metoden:

SCF.addComponent(document.getElementById(*someId*));

Där *someId* är värdet för attributet **data-component-id** .
