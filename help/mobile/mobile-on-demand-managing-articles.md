---
title: Hantera artiklar
seo-title: Hantera artiklar
description: Följ den här sidan om du vill veta mer om hur du skapar och hanterar artiklar.
seo-description: Följ den här sidan om du vill veta mer om hur du skapar och hanterar artiklar.
uuid: 72b86cd7-3016-41b6-a001-9dce4084e9db
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-on-demand-services-app
discoiquuid: b46058f9-4691-4fba-a656-0f8507875a79
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Hantera artiklar{#managing-articles}

>[!NOTE]
>
>Adobe rekommenderar att du använder SPA Editor för projekt som kräver ramverksbaserad klientåtergivning för en sida (t.ex. Reagera). [Läs mer](/help/sites-developing/spa-overview.md).

Innehållshanteringsåtgärder är byggstenar som används för att skapa och hantera artiklar i ett program. Följande åtgärder utförs på artiklar i programmet.

## Artiklar - översikt {#articles-overview}

Artiklar representerar den text som är baserad tillsammans med grafik för att förmedla information.

>[!NOTE]
>
>Läs följande resurser i onlinehjälpen om du vill veta mer om följande ämnen i AEM-mobilappar:
>
>* [Att tänka på vid design](https://helpx.adobe.com/digital-publishing-solution/help/design-app.html)
   >
   >
* [Hantera artiklar](https://helpx.adobe.com/digital-publishing-solution/help/creating-articles.html)
>



## Skapa en artikel {#creating-an-article}

Det allmänna arbetsflödet för att skapa en artikel är följande:

1. Välj **Mobil** från sidospåret.
1. Välj mobilappen i katalogen i Mobile On-Demand.
1. Klicka på nedpilen i det övre högra hörnet av rutan **Hantera artiklar** .
1. Välj en artikelmall och klicka på **Nästa**.
1. Gå igenom varje steg i guiden för att fortsätta skapa din nya artikel.
1. När du är klar klickar du på **Skapa**.
1. Den nya artikeln visas på panelen **Hantera artiklar** .

## Importera en ny artikel {#importing-a-new-article}

Befintligt mobilt On-Demand-innehåll kan hämtas (importeras) från Mobile On-Demand till AEM. På så sätt kan du redigera och visa lokalt innehåll.

>[!NOTE]
>
>Importen inkluderar inte bilder.

Arbetsflödet för att importera en ny artikel

1. Välj mobilapp i katalogen i Mobile On-Demand-appen.
1. Klicka på nedpilen i det övre högra hörnet av rutan **Hantera artiklar** och välj Importera artiklar.
1. Klicka på **Importera artiklar** i dialogrutan och sedan på Stäng.
1. Dina artiklar för mobil on demand visas nu på panelen **Hantera artiklar** .

>[!CAUTION]
>
>Du måste associera en mobil On Demand-anslutning först.

![chlimage_1-3](assets/chlimage_1-3.gif)

## Redigera en artikel {#editing-an-article}

Använd den inbyggda dra och släpp-redigeraren i AEM för att lägga till eller ändra en artikel. Komponenter som text och bilder kan läggas till/tas bort. Bilder från DAM-resurser kan infogas.

>[!CAUTION]
>
>Endast artiklar som har skapats i AEM kan öppnas i redigeraren.

Arbetsflödet för att redigera en artikel:

1. Välj mobilappen i katalogen i Mobile On-Demand.
1. Välj en AEM-källartikel på **panelen Hantera artiklar** .
1. Klicka på den markerade artikeln i listvyn för att öppna den i innehållsredigeraren.
1. Använd innehållsredigeraren för att dra artikelinnehåll (manuskript, bilder, text osv.).

### Visa och redigera metadata i en artikel {#viewing-and-editing-the-metadata-within-an-article}

Innehåll som artiklar, banners osv. har flera egenskaper som titlar, beskrivningar och bilder. Den här åtgärden används för att visa och ändra sådana egenskaper. Dessa ändringar kan även överföras till Mobile On-Demand när de sparas.

Det allmänna arbetsflödet för att visa/redigera en artikel:

1. Välj mobilappen i katalogen i Mobile On-Demand.
1. Välj en artikel på panelen **Hantera artiklar** .

1. Välj **Visa egenskaper** i åtgärdsfältet.
1. Visa alla tillgängliga metadata för artikeln.
1. Redigera metadata om du vill och klicka på **Spara** när du är klar.
1. Du kan också ladda upp ändringarna direkt till Mobile On-Demand.

## Överföra en artikel {#uploading-an-article}

Överföringsåtgärden kopierar det markerade innehållet och lägger till det i ett Mobile On-Demand-projekt. Redan befintligt Mobile On-Demand-innehåll ersätts av den nya versionen.

Det allmänna arbetsflödet för att överföra en artikel:

1. I **Mobile** väljer du appen Mobile On-Demand i katalogen.
1. I rutan **Hantera artiklar** väljer du en artikel för överföring till Mobile On-Demand.
1. Lägg till fler artiklar om det behövs från listvyn.
1. Välj **Överför** i åtgärdsfältet och klicka sedan på Överför i dialogrutan.
1. Dina artiklar har nu överförts till Mobile On-Demand.

![chlimage_1-4](assets/chlimage_1-4.gif)

## Ta bort en artikel {#deleting-an-article}

Den här åtgärden tar bort det markerade innehållet från Mobile On-Demand och eventuellt från den lokala AEM-instansen.

Det allmänna arbetsflödet för att ta bort en artikel:

1. Välj mobilappen i katalogen i Mobile On-Demand.
1. Markera den artikel som ska tas bort i **rutan Hantera artiklar** .
1. Se till att det är markerat i listan (markera andra att ta bort efter behov).
1. Klicka på **Ta bort** i åtgärdsfältet.
1. Kontrollera om du vill ta bort från både AEM och Mobile On-Demand.
1. Click **Delete**.
1. Artikeln har nu tagits bort från listan.

![chlimage_1-5](assets/chlimage_1-5.gif)

### Nästa steg {#the-next-steps}

När du har lärt dig mer om hur du hanterar artiklar, se

* [Hantera banners](/help/mobile/mobile-on-demand-managing-banners.md)
* [Hantera samlingar](/help/mobile/mobile-on-demand-managing-collections.md)
* [Överför delade resurser](/help/mobile/mobile-on-demand-shared-resources.md)
* [Publicera/avpublicera innehållet](/help/mobile/mobile-on-demand-publishing-unpublishing.md)
* [Förhandsgranska med Preflight](/help/mobile/aem-mobile-manage-ondemand-services.md)
