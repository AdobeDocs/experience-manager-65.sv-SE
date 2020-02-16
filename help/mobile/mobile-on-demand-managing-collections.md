---
title: Hantera samlingar
seo-title: Hantera samlingar
description: Samlingar är en väldefinierad bucket som fylls med innehåll som artiklar eller banderoller som passar omslagets tema. Följ den här sidan om du vill veta mer.
seo-description: Samlingar är en väldefinierad bucket som fylls med innehåll som artiklar eller banderoller som passar omslagets tema. Följ den här sidan om du vill veta mer.
uuid: 1d2e9769-d2cc-4d43-a428-e962a51eb5d0
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-on-demand-services-app
discoiquuid: 64c6d198-983f-4a52-9c83-560206363868
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Hantera samlingar{#managing-collections}

>[!NOTE]
>
>Adobe rekommenderar att du använder SPA Editor för projekt som kräver ramverksbaserad klientåtergivning för en sida (t.ex. Reagera). [Läs mer](/help/sites-developing/spa-overview.md).

Innehållshanteringsåtgärder är byggstenar som används för att skapa och hantera innehåll i ett program. Följande åtgärder utförs på innehåll i programmet.

## Samlingar - översikt {#collections-overview}

Samlingar är en väldefinierad *bucket* som fylls med innehåll som artiklar eller banderoller som passar omslagets tema.

>[!NOTE]
>
>Läs följande resurser i onlinehjälpen om du vill veta mer om följande ämnen i AEM-mobilappar:
>
>* [Att tänka på vid design](https://helpx.adobe.com/digital-publishing-solution/help/design-app.html)
   >
   >
* [Hantera samlingar](https://helpx.adobe.com/digital-publishing-solution/help/creating-collections.html)
>



## Skapa en samling {#creating-a-collection}

Det allmänna arbetsflödet för att skapa en samling är följande:

1. Välj **Mobil** från sidospåret.
1. Välj mobilappen i katalogen i Mobile On-Demand.
1. Klicka på nedåtpilen i det övre högra hörnet av rutan **Hantera samlingar** .
1. Gå igenom varje steg i guiden för att fortsätta skapa din nya artikel.
1. När du är klar klickar du på **Skapa**.
1. Den nya artikeln visas på panelen **Hantera samlingar** .

![chlimage_1-1](assets/chlimage_1-1.gif)

## Importera en ny samling {#importing-a-new-collection}

Befintligt mobilt On-Demand-innehåll kan hämtas (importeras) från Mobile On-Demand till AEM. På så sätt kan du redigera och visa lokalt innehåll.

>[!NOTE]
>
>Importen inkluderar inte bilder.

Arbetsflödet för att importera en ny samling

1. Välj mobilapp i katalogen i Mobile On-Demand-appen.
1. Klicka på nedåtpilen i det övre högra hörnet av rutan **Hantera samlingar** och välj Importera samlingar.
1. Klicka på **Importera samlingar** i dialogrutan och sedan på Stäng.
1. Dina Mobile On-Demand-samlingar visas nu på panelen **Hantera samlingar** .

>[!CAUTION]
>
>Du måste associera en mobil On Demand-anslutning först.

## Redigera en samling {#editing-a-collection}

Använd den inbyggda dra och släpp-redigeraren i AEM för att lägga till eller ändra en artikel. Komponenter som text och bilder kan läggas till/tas bort. Bilder från DAM-resurser kan infogas.

Arbetsflödet för att redigera en samling:

1. Välj mobilappen i katalogen i Mobile On-Demand.
1. Välj en AEM-källartikel på panelen **Hantera samlingar** .
1. Klicka på den markerade samlingen i listvyn för att öppna den i innehållsredigeraren.
1. Använd innehållsredigeraren för att dra innehåll i samlingen (manuskript, bilder, text osv.).

### Visa och redigera metadata i en samling {#viewing-and-editing-the-metadata-within-a-collection}

Samlingar har flera egenskaper som titlar, beskrivningar och bilder. Den här åtgärden används för att visa och ändra sådana egenskaper. Dessa ändringar kan även överföras till Mobile On-Demand när de sparas.

Det allmänna arbetsflödet för att visa/redigera en samling:

1. Välj mobilappen i katalogen i Mobile On-Demand.
1. Välj en samling på panelen **Hantera samlingar** .

1. Välj **Egenskaper** i åtgärdsfältet.
1. Visa alla tillgängliga metadata för artikeln.
1. Redigera metadata om du vill och klicka på **Spara** när du är klar.
1. Du kan också ladda upp ändringarna direkt till Mobile On-Demand.

## Överföra en samling {#uploading-a-collection}

Överföringsåtgärden kopierar det markerade innehållet och lägger till det i ett Mobile On-Demand-projekt. Redan befintligt Mobile On-Demand-innehåll ersätts av den nya versionen.

Det allmänna arbetsflödet för att överföra en samling:

1. I **Mobile** väljer du appen Mobile On-Demand i katalogen.
1. I rutan **Hantera samlingar** väljer du en artikel för överföring till Mobile On-Demand.
1. Lägg till fler samlingar om det behövs från listvyn.
1. Välj **Överför** i åtgärdsfältet och klicka sedan på Överför i dialogrutan.
1. Dina samlingar överförs nu till Mobile On-Demand.

## Ta bort en samling {#deleting-a-collection}

Den här åtgärden tar bort den valda samlingen från Mobile On-Demand och eventuellt från den lokala AEM-instansen.

Det allmänna arbetsflödet för att ta bort en samling:

1. Välj mobilappen i katalogen i Mobile On-Demand.
1. Markera den artikel som ska tas bort på panelen **Hantera samlingar** .
1. Se till att det är markerat i listan (markera andra att ta bort efter behov).
1. Klicka på **Ta bort** i åtgärdsfältet.
1. Kontrollera om du vill ta bort från både AEM och Mobile On-Demand.
1. Click **Delete**.
1. Din samling har nu tagits bort från listan.

## Lägga till innehåll i samlingar {#adding-content-to-collections}

Samlingar är i princip en kategori med relaterat innehåll.  De samlar ihop innehåll som artiklar, banners i paket som definierar navigeringsstrukturen i ditt program. Samlingar kan kapslas.

>[!NOTE]
>
>Innehållet måste överföras till Mobile On-Demand innan det kan läggas till i en samling.

Samlingar är i princip en kategori med relaterat innehåll: De samlar ihop innehåll som artiklar, banners i paket som definierar navigeringsstrukturen i ditt program. Samlingar kan kapslas.

1. Välj mobilappen i katalogen i Mobile On-Demand.
1. Välj en tidigare överförd artikel (eller banner/samling)
1. Välj Lägg till i åtgärdsfältet.
1. Välj en tidigare överförd samling i dialogrutan.
1. Klicka på **Uppdatera** för att lägga till innehåll i samlingen.

![chlimage_1-2](assets/chlimage_1-2.gif)

### Nästa steg {#the-next-steps}

En del om hur du hanterar samlingar finns på

* [Hantera banners](/help/mobile/mobile-on-demand-managing-banners.md)
* [Hantera artiklar](/help/mobile/mobile-on-demand-managing-articles.md)
* [Överför delade resurser](/help/mobile/mobile-on-demand-shared-resources.md)
* [Publicera/avpublicera innehållet](/help/mobile/mobile-on-demand-publishing-unpublishing.md)
* [Förhandsgranska med Preflight](/help/mobile/aem-mobile-manage-ondemand-services.md)
