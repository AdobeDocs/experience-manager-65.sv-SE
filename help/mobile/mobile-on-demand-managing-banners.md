---
title: Hantera banners
seo-title: Hantera banners
description: Banderoller representerar vanligtvis grafiska marknadsföringslänkar. Följ den här sidan om du vill veta mer.
seo-description: Banderoller representerar vanligtvis grafiska marknadsföringslänkar. Följ den här sidan om du vill veta mer.
uuid: 593fe2ef-84df-42e2-8a03-897fb67a896d
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-on-demand-services-app
discoiquuid: fb1abaa0-9c02-4f20-aa7c-073def067452
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Hantera banners{#managing-banners}

>[!NOTE]
>
>Adobe rekommenderar att du använder SPA Editor för projekt som kräver ramverksbaserad klientåtergivning för en sida (t.ex. Reagera). [Läs mer](/help/sites-developing/spa-overview.md).

Innehållshanteringsåtgärder är byggstenar som används för att skapa och hantera innehåll i ett program. Följande åtgärder utförs på innehåll i programmet.

## Banners - översikt {#banners-overview}

Banderoller representerar vanligtvis grafiska marknadsföringslänkar.

>[!NOTE]
>
>Läs följande resurser i onlinehjälpen om du vill veta mer om följande ämnen i AEM-mobilappar:
>
>* [Att tänka på vid design](https://helpx.adobe.com/digital-publishing-solution/help/design-app.html)
   >
   >
* [Skapa banners](https://helpx.adobe.com/digital-publishing-solution/help/creating-banners.html)
>



## Skapa en banderoll {#creating-a-banner}

Det allmänna arbetsflödet för att skapa en artikel är följande:

1. Välj **Mobil** från sidospåret.
1. Välj mobilappen i katalogen i Mobile On-Demand.
1. Klicka på nedpilen i det övre högra hörnet av rutan **Hantera banderoller** .
1. Gå igenom varje steg i guiden för att fortsätta skapa din nya banderoll.
1. När du är klar klickar du på **Skapa**.
1. Din nya banderoll visas i rutan **Hantera banderoller** .

![chlimage_1-6](assets/chlimage_1-6.gif)

## Importera en ny banderoll {#importing-a-new-banner}

Befintligt mobilt On-Demand-innehåll kan hämtas (importeras) från Mobile On-Demand till AEM. På så sätt kan du redigera och visa lokalt innehåll.

>[!NOTE]
>
>Importen inkluderar inte bilder.

Arbetsflödet för att importera en ny artikel

1. Välj mobilapp i katalogen i Mobile On-Demand-appen.
1. Klicka på nedpilen i det övre högra hörnet av rutan **Hantera banderoller** och välj Importera banderoller.
1. Klicka på **Importera banderoll** i dialogrutan och sedan på Stäng.
1. Dina artiklar för mobil on demand visas nu i panelen **Hantera banners** .

>[!CAUTION]
>
>Du måste associera en mobil On Demand-anslutning först.

## Redigera en banderoll {#editing-a-banner}

Använd den inbyggda dra och släpp-redigeraren i AEM för att lägga till eller ändra en artikel. Komponenter som text och bilder kan läggas till/tas bort. Bilder från DAM-resurser kan infogas.

>[!CAUTION]
>
>Endast banners som skapats i AEM kan öppnas i redigeraren.

Arbetsflödet för att redigera en artikel:

1. Välj mobilappen i katalogen i Mobile On-Demand.
1. Välj en banderoll från AEM-källa i rutan** Hantera banners**.
1. Klicka på den markerade banderollen i listvyn för att öppna den i innehållsredigeraren.
1. Använd innehållsredigeraren för att dra banderollinnehåll (manuskript, bilder, text osv.).

### Visa och redigera metadata i en banderoll {#viewing-and-editing-the-metadata-within-a-banner}

Banderoller har flera egenskaper som titlar, beskrivningar och bilder. Den här åtgärden används för att visa och ändra sådana egenskaper. Dessa ändringar kan även överföras till Mobile On-Demand när de sparas.

Det allmänna arbetsflödet för att visa/redigera en artikel:

1. Välj mobilappen i katalogen i Mobile On-Demand.
1. Välj en banderoll i rutan **Hantera banderoller** .

1. Välj **Egenskaper** i åtgärdsfältet.
1. Visa alla tillgängliga metadata för artikeln.
1. Redigera metadata om du vill och klicka på **Spara** när du är klar.
1. Du kan också ladda upp ändringarna direkt till Mobile On-Demand.

## Överföra en banderoll {#uploading-a-banner}

Överföringsåtgärden kopierar det markerade innehållet och lägger till det i ett Mobile On-Demand-projekt. Redan befintligt Mobile On-Demand-innehåll ersätts av den nya versionen.

Det allmänna arbetsflödet för att överföra en banderoll:

1. I **Mobile** väljer du appen Mobile On-Demand i katalogen.
1. Välj en banderoll för överföring till Mobile On-Demand i rutan **Hantera banderoller** .
1. Lägg till fler banners om det behövs från listvyn.
1. Välj **Överför** i åtgärdsfältet och klicka sedan på Överför i dialogrutan.
1. Din banderoll har nu överförts till Mobile On-Demand.

![chlimage_1-7](assets/chlimage_1-7.gif)

## Ta bort en banderoll {#deleting-a-banner}

Den här åtgärden tar bort den markerade banderollen från Mobile On-Demand och eventuellt från den lokala AEM-instansen.

Det allmänna arbetsflödet för att ta bort en banderoll:

1. Välj mobilappen i katalogen i Mobile On-Demand.
1. Markera den banderoll som ska tas bort i rutan **Hantera banderoller** .
1. Se till att det är markerat i listan (markera andra att ta bort efter behov).
1. Klicka på **Ta bort** i åtgärdsfältet.
1. Kontrollera om du vill ta bort från både AEM och Mobile On-Demand.
1. Click **Delete**.
1. Din banderoll har nu tagits bort från listan.

### Nästa steg {#the-next-steps}

En av de saker du lär dig om banners finns på

* [Hantera artiklar](/help/mobile/mobile-on-demand-managing-articles.md)
* [Hantera samlingar](/help/mobile/mobile-on-demand-managing-collections.md)
* [Överför delade resurser](/help/mobile/mobile-on-demand-shared-resources.md)
* [Publicera/avpublicera innehållet](/help/mobile/mobile-on-demand-publishing-unpublishing.md)
* [Förhandsgranska med Preflight](/help/mobile/aem-mobile-manage-ondemand-services.md)
