---
title: Skapa riktade upplevelser i AEM Forms
description: Använd Target i AEM Forms för att skapa anpassade upplevelser för riktade kunder.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: integrations
exl-id: fdc91054-3f7e-4cbf-bdfa-7d7a621747f1
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '839'
ht-degree: 0%

---

# Skapa riktade upplevelser i AEM Forms {#create-targeted-experiences-in-aem-forms}

## Integrera Adobe Target med AEM Forms {#integrate-adobe-target-with-aem-forms}

Med Adobe Target som är integrerat med AEM kan ni skapa upplevelser som är anpassade för en viss målgrupp. Med Adobe Target kan du skapa A/B-tester, mäta användarnas svar och generera anpassat webbinnehåll för målanvändare. Du kan integrera Adobe Target med AEM Forms för att anpassa bildkomponenterna i adaptiva formulär och interaktiv kommunikation.

Konfigurera Adobe Target i AEM för användning med adaptiva formulär och interaktiv kommunikation, se [Skapa en målkonfiguration i AEM](/help/sites-administering/target.md) och [Lägg till ett ramverk](/help/sites-administering/target.md).

>[!NOTE]
>
>Målsättningen fungerar när din adaptiva form eller interaktiva kommunikation återges med ett värdnamn eller en IP-adress. Det misslyckas när din adaptiva form eller interaktiva kommunikation återges med localhost.

## Skapa en målaktivitet {#creating-a-target-activity}

1. Välj **Adobe Experience Manager > Personalisering > Verksamheter**.

   `https://<hostname>:<port>/libs/cq/personalization/touch-ui/content/v2/activities.html`

1. Välj på sidan Aktiviteter **Skapa > Skapa varumärke**.
1. Du uppmanas att välja en mall och ange egenskaper.

   Välj en mall och välj **Nästa.** Ange namnet på varumärket i egenskapssektionen och välj **Skapa.**
Ditt varumärke finns nu med på aktivitetssidan.

1. Välj ditt varumärke på sidan Verksamheter.
1. I ert varumärkes huvudområde väljer du **Skapa** > **Skapa aktivitet**.

   När du skapar en aktivitet anger du dess information, mål och inställningar.

   Avsnittet Detaljer innehåller namn, målmotor och mål. När du väljer Adobe Target som målmotor aktiveras konfigurationsalternativet för målmolnet. Välj målmolnkonfigurationen, välj aktivitetstyp, ange målet för aktiviteten och välj **Nästa**. Interaktiv kommunikation har bara stöd för aktivitetstypen Experience Targeting.

   I målavsnittet kan du lägga till en målgruppsupplevelse och namnge den. Klicka **Lägg till upplevelse** för att aktivera **Välj publik** och **Namnge upplevelsen** alternativ. Välj **Välj publik** för att se en lista över målgrupper och deras källa. Välj en målgrupp i listan Målgruppsnamn. Välj **Lägg till upplevelse** för att namnge upplevelsen och välja **Nästa**.

   I avsnittet Mål och inställningar kan du schemalägga och prioritera din aktivitet. Ange startdatum, slutdatum och prioritet för aktiviteten, målmått, ytterligare mått och välj **Spara**.

   Aktiviteten visas nu på din varumärkessida.

   >[!NOTE]
   >
   >Du kan ignorera felet&quot;Din aktivitet har sparats men den har inte synkroniserats med Target. Orsak: Följande upplevelse har inga erbjudanden&quot;, om den påträffas när aktiviteten sparas.

1. Aktivera målet genom att redigera .jsp-filen så att den innehåller klientbibliotek som din adaptiva formulärmall använder.

   I den färdiga implementeringen klickar du på **verktyg** >  **CRXDE Lite**.

   I adressfältet i CRXDE Lite skriver du /libs/fd/af/components/page/base/head.jsp för att redigera filen head.jsp.

   Den här implementeringen använder en simpleEnrollment-mall. I den här implementeringen ändrar du filen head.jsp så att den innehåller följande klientbibliotek:

   `<cq:include script="/libs/cq/cloudserviceconfigs/components/servicelibs/servicelibs.jsp"/>`

   `<cq:include path="clientcontext_optimized" resourceType="/libs/cq/personalization/components/clientcontext_optimized"/>`

   `<cq:include path="config" resourceType="cq/personalization/components/clientcontext_optimized/config"/>`

1. Om du vill aktivera målramverket för adaptiva formulär navigerar du till formuläret eller den interaktiva kommunikationen och öppnar det i redigeringsläge.

   Om du vill öppna ett formulär eller en interaktiv kommunikation i redigeringsläge väljer du **Välj** och sedan **Öppna**.

   Du kan också visa fyra knappar när du flyttar pekaren över formuläret eller en interaktiv kommunikationsikon utan att markera den. Du kan välja **Redigera** som visas för att öppna formuläret i redigeringsläge.

1. Välj **Sidinformation** ![temaalternativ](assets/theme-options.png) > **Öppna egenskaper**.
1. Välj en konfiguration för fliken Allmänt **Adobe Target** fält. Välj **Spara och stäng**.

## Använda skapad aktivitet på en adaptiv formulärbild eller en interaktiv kommunikationsbild {#applying-created-activity-to-an-adaptive-form-image-or-an-interactive-communication-image}

1. Öppna det adaptiva formuläret och den interaktiva kommunikationen för redigering. Öppna webbkanalen om du öppnar en interaktiv kommunikation.

1. I redigeringsläget för den interaktiva kommunikationen eller det adaptiva formuläret lägger du till en målbild.

   >[!NOTE]
   >
   >AEM Forms har bara stöd för bildkomponenter. Kontrollera att panelen som är värd för bildkomponenten inte innehåller någon annan komponent och att antalet kolumner för panelen är 1.

1. Växla från **Redigera** till **Målinriktning** läge. Alternativet för att växla mellan lägen ligger nära det övre högra hörnet.
1. Välj en **VARUMÄRKE**, markera **VERKSAMHET** och markera **Börja målinrikta**. The **Målgrupper** -menyn visas till höger om redigeraren.

   ![riktad meny](assets/targeting-menu.png)

1. Välj en målgrupp i **Målgrupper** och välj den bild som du vill använda som mål. En meny visas. Välj **Mål**. Markera bilden och markera **Konfigurera**. I egenskapsfönstret väljer du den bild som ska visas för den valda publiken. Upprepa steget för alla målgrupper. Upplevelsens målinriktning aktiveras för bilden i den interaktiva kommunikationen eller adaptiva formen.

## Kontrollera om den skapade aktiviteten synkroniseras med målservern {#check-if-the-created-activity-syncs-with-the-target-server}

En aktivitet som används för målsynkronisering med målservern. Om du vill kontrollera om din aktivitet är synkroniserad med målservern kontrollerar du status för din aktivitet på din varumärkessida.

Kontrollera att aktivitetens status är Synkroniserad.

## Validera Target-beteende {#validate-target-behavior}

Så här validerar du Target-beteende:

* Använd målinriktning med `wcmmode preview` i redigeringsläget
* Använd målinriktning med `wcmmode preview` och `wcmmode disabled` i publiceringsläge

## Övervaka målinriktning för bildkomponenten {#monitor-targeting-for-the-image-component}

Publicera bilder, aktiviteter och anpassningsbara formulär för att övervaka målanpassning för bildkomponenter i formuläret.

## Öppna ärenden {#open-issues}

Synlighetsuttryck, ange fokus misslyckas för målbilder i adaptiva formulär.
