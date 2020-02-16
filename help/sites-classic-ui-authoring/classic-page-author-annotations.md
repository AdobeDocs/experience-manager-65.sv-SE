---
title: Anteckningar vid redigering av en sida
seo-title: Anteckningar vid redigering av en sida
description: Om du lägger till innehåll på webbplatsens sidor kan det ofta bli aktuellt med diskussioner innan det faktiskt publiceras. För att underlätta detta kan du lägga till en anteckning i många komponenter som är direkt relaterade till innehållet.
seo-description: Om du lägger till innehåll på webbplatsens sidor kan det ofta bli aktuellt med diskussioner innan det faktiskt publiceras. För att underlätta detta kan du lägga till en anteckning i många komponenter som är direkt relaterade till innehållet.
page-status-flag: de-activated
uuid: d8d6ba76-f2aa-4044-98bf-5d506742d90d
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: 9bee0197-f275-49cc-922d-62cba826c4e5
translation-type: tm+mt
source-git-commit: c8a02ad9fc33e963d2c760840e70c40ede988054

---


# Anteckningar vid redigering av en sida{#annotations-when-editing-a-page}

Om du lägger till innehåll på webbplatsens sidor kan det ofta bli aktuellt med diskussioner innan det faktiskt publiceras. För att underlätta detta kan du lägga till en anteckning i många komponenter som är direkt relaterade till innehåll (till skillnad från till exempel layout).

En anteckning placerar en färgmarkör/anteckning på sidan. Med anteckningen kan du (eller andra användare) lämna kommentarer och/eller frågor till andra författare/granskare.

>[!NOTE]
>
>Definitionen av en enskild komponenttyp avgör om det är möjligt att lägga till en anteckning (eller inte) i instanser av den komponenten.

>[!NOTE]
>
>Anteckningar som skapas i det klassiska användargränssnittet visas också i det pekoptimerade användargränssnittet. Skisser är dock gränssnittsspecifika och visas endast i det användargränssnitt där de skapades.

>[!CAUTION]
>
>Om du tar bort en resurs (t.ex. ett stycke) tas alla anteckningar och skisser som är kopplade till resursen bort. oavsett deras placering på sidan som helhet.

>[!NOTE]
>
>Beroende på dina behov kan du även utveckla ett arbetsflöde för att skicka meddelanden när anteckningar läggs till, uppdateras eller tas bort.

## Anteckningar {#annotations}

Beroende på styckedesignen är anteckningen antingen tillgänglig som ett alternativ på snabbmenyn (vanligtvis högerknappen när den placeras över det önskade stycket) eller som en knapp på styckets redigeringsfält.

I båda fallen väljer du **Anteckning**. En färgad anteckning kommer att användas på stycket. Du är direkt i redigeringsläge, vilket gör att du kan lägga till text direkt:

![chlimage_1-137](assets/chlimage_1-137.png)

Du kan flytta anteckningen till en ny plats på sidan. Klicka på den övre kantlinjens område, håll sedan ned och dra samtidigt anteckningen till den nya positionen. Det kan finnas var som helst på sidan, men det brukar vara praktiskt att hålla det kopplat till stycket på något sätt.

Anteckningar (inklusive tillhörande skisser) ingår också i varje kopierings-, klippnings- eller raderingsåtgärd som utförs på det stycke som de är kopplade till. För kopierings- eller klippåtgärder behåller anteckningens (och tillhörande skisser) position i förhållande till det ursprungliga stycket.

Storleken på anteckningen kan också ökas eller minskas genom att dra i det nedre högra hörnet.

I spårningssyfte anger sidfotsraden användaren som skapade anteckningen och datumet. Efterföljande författare kan redigera samma anteckning (sidfoten uppdateras) eller skapa en ny anteckning för samma stycke.

Bekräftelse kommer att begäras när du väljer att ta bort anteckningen (om du tar bort en anteckning tas även alla skisser som är kopplade till anteckningen bort).

Med de tre ikonerna längst upp till vänster kan du minimera anteckningen (tillsammans med relaterade skisser), ändra färg och lägga till skisser.

>[!NOTE]
>
>Anteckningar visas bara i redigeringsläget i författarmiljön.
>
>De visas inte i en publiceringsmiljö eller i förhandsgransknings- eller designläge som är tillgängliga i en författarmiljö.

>[!NOTE]
>
>Anteckningar kan inte läggas till på en sida som har låsts av en annan användare.

## Anteckningskisser {#annotation-sketches}

>[!NOTE]
>
>Skisser är inte tillgängliga i Internet Explorer så:
>
>* ikonen visas inte.
>* befintliga skisser som skapats i en annan webbläsare visas inte.
>



Skisser är en funktion av anteckningar som gör att du kan skapa enkla linjeregrafik var som helst i webbläsarfönstret (synlig del):

![chlimage_1-138](assets/chlimage_1-138.png)

* Markören ändras till en korstråd när du är i skissläge. Du kan rita flera distinkta linjer.
* Skisslinjen återspeglar anteckningsfärgen och kan vara antingen:

   * frihand

      standardläget, avsluta genom att släppa musknappen.

   * rak:

      hålla ned `ALT` och klicka på start- och slutpunkterna, avsluta med ett dubbelklick.

* När du har avslutat skissläget kan du klicka på en skiss för att markera den.
* Flytta en skiss genom att markera skissen och sedan dra den till önskad plats.
* En skiss täcker över innehållet. Det innebär att du inte kan klicka på det underliggande stycket i skissens fyra hörn. om du till exempel behöver redigera eller komma åt en länk. Om det här blir ett problem (du till exempel har en skiss som täcker ett stort område på sidan) minimerar du sedan lämplig anteckning, eftersom detta även minimerar alla relaterade skisser och ger dig tillgång till det underliggande området.
* Om du vill ta bort en enskild skiss markerar du önskad skiss och trycker sedan på **Delete** (**fn**-**backspace** på en Mac).

* Om du flyttar, eller kopierar, ett stycke kommer alla relaterade anteckningar och skisser också att flyttas, eller kopieras; deras position i förhållande till stycket förblir densamma.
* Om du tar bort en anteckning tas även alla skisser som är kopplade till den anteckningen bort.

