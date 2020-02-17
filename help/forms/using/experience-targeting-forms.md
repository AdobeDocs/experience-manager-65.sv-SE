---
title: Skapa riktade upplevelser i AEM-formulär
seo-title: Skapa riktade upplevelser i AEM-formulär
description: Använd Target i AEM Forms för att skapa anpassade upplevelser för riktade kunder.
seo-description: Använd Target i AEM Forms för att skapa anpassade upplevelser för riktade kunder.
uuid: 174b6054-8fe3-4ab2-8afd-435e5dff9044
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: integrations
discoiquuid: 6cf54a08-d429-4a58-8429-a1cb784448d1
translation-type: tm+mt
source-git-commit: 9d90bc5f77f827925e3e1ecd12d56a94a2bbae30

---


# Skapa riktade upplevelser i AEM-formulär {#create-targeted-experiences-in-aem-forms}

## Integrera Adobe Target med AEM Forms {#integrate-adobe-target-with-aem-forms}

Med Adobe Target integrerat med AEM kan ni skapa upplevelser som är anpassade för en viss målgrupp. Med Adobe Target kan ni skapa A/B-tester, mäta användarnas svar och generera anpassat webbinnehåll för målanvändare. Du kan integrera Adobe Target med AEM Forms för att rikta in bildkomponenter i adaptiva formulär och interaktiv kommunikation.

Konfigurera Adobe Target i AEM för att använda det med adaptiva formulär och interaktiv kommunikation, se [Skapa en målkonfiguration i AEM](/help/sites-administering/target.md) och [Lägg till ett ramverk](/help/sites-administering/target.md).

>[!NOTE]
>
>Målsättningen fungerar när din adaptiva form eller interaktiva kommunikation återges med ett värdnamn eller en IP-adress. Det misslyckas när din adaptiva form eller interaktiva kommunikation återges med localhost.

## Skapa en målaktivitet {#creating-a-target-activity}

1. Tryck på **Adobe Experience Manager > Personalisering > Verksamheter**.

   `https://<hostname>:<port>/libs/cq/personalization/touch-ui/content/v2/activities.html`

1. På sidan Aktiviteter trycker du på **Skapa > Skapa varumärke**.
1. Du uppmanas att välja en mall och ange egenskaper.

   Välj en mall och tryck på **Nästa.** Ange namnet på varumärket i egenskapssektionen och tryck på **Skapa.**
Ditt varumärke finns nu med på aktivitetssidan.

1. Tryck på ert varumärke på sidan Verksamheter.
1. Tryck på **Skapa** > **Skapa aktivitet** i ert varumärkes huvudområde.

   När du skapar en aktivitet anger du dess information, mål och inställningar.

   Avsnittet Detaljer innehåller namn, målmotor och mål. När du väljer Adobe Target som målmotor aktiveras konfigurationsalternativet för målmolnet. Välj din molnkonfiguration för Target, välj Activity type, ange målet för aktiviteten och tryck på **Next**. Interaktiv kommunikation har bara stöd för aktivitetstypen Experience Targeting.

   I målavsnittet kan du lägga till en målgruppsupplevelse och namnge den. Klicka på **Lägg till upplevelse** för att aktivera alternativen **Välj publik** och **Namnge upplevelse** . Tryck på **Välj publik** för att visa en lista över målgrupper och deras källa. Välj en målgrupp i listan Målgruppsnamn. Tryck på **Add Experience** (Lägg till upplevelse) för att namnge upplevelsen och tryck sedan på **Next (Nästa**).

   I avsnittet Mål och inställningar kan du schemalägga och prioritera din aktivitet. Ange startdatum, slutdatum och prioritet för aktiviteten, målmått, ytterligare mått och tryck på **Spara**.

   Aktiviteten visas nu på din varumärkessida.

   >[!NOTE]
   >
   >Du kan ignorera felet&quot;Din aktivitet har sparats men den har inte synkroniserats med Target. Orsak: Följande upplevelse har inga erbjudanden&quot;, om den påträffas när aktiviteten sparas.

1. Aktivera målet genom att redigera .jsp-filen så att den innehåller klientbibliotek som din adaptiva formulärmall använder.

   I den färdiga implementeringen klickar du till exempel på **Verktyg** > **CRXDE Lite**.

   I adressfältet i CRXDE Lite skriver du /libs/fd/af/components/page/base/head.jsp för att redigera filen head.jsp.

   Den här implementeringen använder en simpleEnrollment-mall. I den här implementeringen ändrar du filen head.jsp så att den innehåller följande klientbibliotek:

   `<cq:include script="/libs/cq/cloudserviceconfigs/components/servicelibs/servicelibs.jsp"/>`

   `<cq:include path="clientcontext_optimized" resourceType="/libs/cq/personalization/components/clientcontext_optimized"/>`

   `<cq:include path="config" resourceType="cq/personalization/components/clientcontext_optimized/config"/>`

1. Om du vill aktivera målramverket för adaptiva formulär navigerar du till formuläret eller den interaktiva kommunikationen och öppnar det i redigeringsläge.

   Om du vill öppna ett formulär eller en interaktiv kommunikation i redigeringsläge trycker du på **Välj** och sedan på **Öppna**.

   Du kan också använda fyra knappar när du flyttar pekaren över formuläret eller en interaktiv kommunikationsikon utan att markera den. Du kan trycka på knappen **Redigera** som visas för att öppna formuläret i redigeringsläge.

1. Tryck på **Sidinformation** , ![temaalternativ](assets/theme-options.png) > **Öppna egenskaper**, i verktygsfältet för sidan.
1. Välj en konfiguration för fältet **Adobe Target** på fliken Allmänt. Tryck på **Spara och stäng**.

## Använda skapad aktivitet på en adaptiv formulärbild eller en interaktiv kommunikationsbild {#applying-created-activity-to-an-adaptive-form-image-or-an-interactive-communication-image}

1. Öppna det adaptiva formuläret och den interaktiva kommunikationen för redigering. Öppna webbkanalen om du öppnar en interaktiv kommunikation.

1. I redigeringsläget för den interaktiva kommunikationen eller det adaptiva formuläret lägger du till en målbild.

   >[!NOTE]
   >
   >AEM Forms har endast stöd för bildkomponenter. Kontrollera att panelen som är värd för bildkomponenten inte innehåller någon annan komponent och att antalet kolumner för panelen är 1.

1. Växla från **redigering** till **målinriktning** . Alternativet för att växla mellan lägen ligger nära det övre högra hörnet.
1. Välj ett **VARUMÄRKE**, välj **AKTIVITET** och tryck på **Start Targeting**. Menyn **Publiker** visas till höger om redigeraren.

   ![riktad meny](assets/targeting-menu.png)

1. Välj en målgrupp på menyn **Publiker** och tryck på bilden som du vill ha som målgrupp. En meny visas. Tryck på **Target** på menyn. Tryck på bilden och tryck på **Konfigurera**. I egenskapsfönstret väljer du den bild som ska visas för den valda publiken. Upprepa steget för alla målgrupper. Upplevelsens målinriktning aktiveras för bilden i den interaktiva kommunikationen eller adaptiva formen.

## Kontrollera om den skapade aktiviteten synkroniseras med målservern {#check-if-the-created-activity-syncs-with-the-target-server}

En aktivitet som används för målsynkronisering med målservern. Om du vill kontrollera om din aktivitet är synkroniserad med målservern kontrollerar du status för din aktivitet på din varumärkessida.

Kontrollera att aktivitetens status är Synkroniserad.

## Validera Target-beteende {#validate-target-behavior}

Så här validerar du Target-beteende:

* Använd målgruppsanpassning med `wcmmode preview` i redigeringsläget
* Använd målinriktning med `wcmmode preview` och `wcmmode disabled` i publiceringsläge

## Övervaka målinriktning för bildkomponenten {#monitor-targeting-for-the-image-component}

Publicera bilder, aktiviteter och anpassningsbara formulär för att övervaka målanpassning för bildkomponenter i formuläret.

## Öppna ärenden {#open-issues}

Synlighetsuttryck, ange fokus misslyckas för målbilder i adaptiva formulär.
