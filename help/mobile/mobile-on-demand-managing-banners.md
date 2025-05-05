---
title: Hantera banners
description: Banderoller representerar vanligtvis grafiska kampanjlänkar. Följ den här sidan om du vill veta mer.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-on-demand-services-app
exl-id: c65a24e6-3041-4774-aeed-8e188ea19b78
solution: Experience Manager
feature: Mobile
role: User
source-git-commit: 2dae56dc9ec66f1bf36bbb24d6b0315a5f5040bb
workflow-type: tm+mt
source-wordcount: '634'
ht-degree: 0%

---

# Hantera banners{#managing-banners}

{{ue-over-mobile}}

Innehållshanteringsåtgärder är byggstenar som används för att skapa och hantera innehåll i ett program. Följande åtgärder utförs på innehåll i programmet.

## Banderoller - översikt {#banners-overview}

Banderoller representerar vanligtvis grafiska kampanjlänkar.

>[!NOTE]
>
>Läs följande resurser i onlinehjälpen om du vill veta mer om följande ämnen i AEM Mobile-program:
>
>* [Designöverväganden](https://helpx.adobe.com/digital-publishing-solution/help/design-app.html)
>
>* [Skapar banderoller](https://helpx.adobe.com/digital-publishing-solution/help/creating-banners.html)
>

## Skapa en banderoll {#creating-a-banner}

Det allmänna arbetsflödet för att skapa en artikel är följande:

1. Välj **Mobil** från sidospåret.
1. Välj mobilappen i katalogen i Mobile On-Demand.
1. Klicka på nedpilen i det övre högra hörnet av rutan **Hantera banderoller** .
1. Gå igenom varje steg i guiden för att fortsätta skapa din nya banderoll.
1. Klicka på **Skapa** när du är klar.
1. Din nya banderoll visas i rutan **Hantera banderoller**.

![chlimage_1-6](assets/chlimage_1-6.gif)

## Importera en ny banderoll {#importing-a-new-banner}

Befintligt mobilt on demand-innehåll kan hämtas (importeras) från Mobile On-Demand till AEM. På så sätt kan du redigera och visa lokalt innehåll.

>[!NOTE]
>
>Importen inkluderar inte bilder.

Arbetsflödet för att importera en ny artikel

1. Välj mobilapp i katalogen i Mobile On-Demand-appen.
1. Klicka på nedpilen i det övre högra hörnet av rutan **Hantera banderoller** och välj Importera banderoller.
1. Klicka på **Importera banderoll** i dialogrutan och sedan på Stäng.
1. Dina artiklar för mobil on demand visas nu i panelen **Hantera banners**.

>[!CAUTION]
>
>Koppla en mobil On Demand-anslutning först.

## Redigera en banderoll {#editing-a-banner}

Använd den inbyggda AEM dra och släpp-redigeraren för att lägga till eller ändra en artikel. Komponenter som text och bilder kan läggas till/tas bort. Bilder från DAM Assets kan infogas.

>[!CAUTION]
>
>Endast banderoller som skapats i AEM kan öppnas i redigeraren.

Arbetsflödet för att redigera en artikel:

1. Välj mobilappen i katalogen i Mobile On-Demand.
1. Välj en banderoll AEM källa i rutan **&#x200B; Hantera banners**.
1. Klicka på den markerade banderollen i listvyn för att öppna den i innehållsredigeraren.
1. Använd innehållsredigeraren för att dra banderollinnehåll (manuskript, bilder, text och så vidare).

### Visa och redigera metadata i en banderoll {#viewing-and-editing-the-metadata-within-a-banner}

Banderoller har flera egenskaper som titlar, beskrivningar och bilder. Den här åtgärden används för att visa och ändra sådana egenskaper. Dessa ändringar kan även överföras till Mobile On-Demand när de sparas.

Det allmänna arbetsflödet för att visa/redigera en artikel:

1. Välj mobilappen i katalogen i Mobile On-Demand.
1. Välj en banderoll i rutan **Hantera banners**.

1. Välj **Egenskaper** i åtgärdsfältet.
1. Visa alla tillgängliga metadata för artikeln.
1. Redigera metadata vid behov och klicka på **Spara** när du är klar.
1. Du kan också ladda upp ändringarna direkt till Mobile On-Demand.

## Överföra en banderoll {#uploading-a-banner}

Överföringsåtgärden kopierar det markerade innehållet och lägger till det i ett Mobile On-Demand-projekt. Redan befintligt Mobile On-Demand-innehåll ersätts av den nya versionen.

Det allmänna arbetsflödet för att överföra en banderoll:

1. Från **Mobile** väljer du appen Mobile On-Demand i katalogen.
1. I rutan **Hantera banners** väljer du en banderoll för överföring till Mobile On-Demand.
1. Lägg till fler banners om det behövs från listvyn.
1. Välj **Överför** i åtgärdsfältet och klicka sedan på Överför i dialogrutan.
1. Din banderoll har nu överförts till Mobile On-Demand.

![chlimage_1-7](assets/chlimage_1-7.gif)

## Ta bort en banderoll {#deleting-a-banner}

Den här åtgärden tar bort den markerade banderollen från Mobile On-Demand och eventuellt från den lokala AEM.

Det allmänna arbetsflödet för att ta bort en banner:

1. Välj mobilappen i katalogen i Mobile On-Demand.
1. Markera den banderoll som ska tas bort i rutan **Hantera banderoller**.
1. Se till att det är markerat i listan (markera andra att ta bort efter behov).
1. Klicka på **Ta bort** i åtgärdsfältet.
1. Kontrollera om du vill ta bort från AEM och Mobile On-Demand.
1. Klicka på **Ta bort**.
1. Din banderoll har nu tagits bort från listan.

### Nästa steg {#the-next-steps}

En av de saker du lär dig om banners finns på

* [Hantera artiklar](/help/mobile/mobile-on-demand-managing-articles.md)
* [Hantera samlingar](/help/mobile/mobile-on-demand-managing-collections.md)
* [Överför delade resurser](/help/mobile/mobile-on-demand-shared-resources.md)
* [Publicera/avpublicera innehållet](/help/mobile/mobile-on-demand-publishing-unpublishing.md)
* [Förhandsgranska med Preflight](/help/mobile/aem-mobile-manage-ondemand-services.md)
