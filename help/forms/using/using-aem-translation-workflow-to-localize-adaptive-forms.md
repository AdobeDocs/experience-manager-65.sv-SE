---
title: Använda arbetsflödet för AEM-översättning för att lokalisera adaptiva formulär och urkunder
seo-title: Använda arbetsflödet för AEM-översättning för att lokalisera adaptiva formulär och urkunder
description: Lär dig använda arbetsflöden för AEM-översättning för att lokalisera adaptiva formulär och urkunder.
seo-description: Lär dig använda arbetsflöden för AEM-översättning för att lokalisera adaptiva formulär och urkunder.
uuid: 6c87a283-0203-4cf7-989a-3770ddbbbd6e
content-type: reference
topic-tags: develop
discoiquuid: f5642571-9657-4ca1-93c5-4ae2eb91e967
noindex: true
translation-type: tm+mt
source-git-commit: 5120bbdefea528ad6d07a9c99df565555b6a8444

---


# Använda arbetsflödet för AEM-översättning för att lokalisera adaptiva formulär och urkunder {#using-aem-translation-workflow-to-localize-adaptive-forms-and-document-of-record}

Lokaliserade formulär hjälper er att nå en större publik över alla länder. Med översättningsarbetsflödet i Adobe Experience Manager kan ni lokalisera adaptiva formulär och deras urkunder. Du kan använda **maskinöversättning** eller **mänskliga översättare** för att lokalisera en adaptiv form.

I den här artikeln förklaras hur man använder arbetsflödet för AEM-översättning med adaptiva formulär och urkunder.

## Lokalisera ett anpassat formulär och dokument med post med maskinöversättning {#localizing-an-adaptive-form-and-document-of-record-using-machine-translation}

Maskinöversättningstjänsten översätter omedelbart ditt innehåll i adaptiv form och i ett urklippsdokument. AEM Forms är förkonfigurerat för att använda en provversion av Microsoft Translator för maskinöversättning. Utför följande steg för att aktivera maskinöversättning för anpassade formulär och registerdokument:

1. Markera ett formulär i användargränssnittet för AEM-formulär och tryck på **Lägg till ordlista** .
1. På skärmen **Lägg till ordlista i översättningsprojekt** väljer du **Skapa ett nytt översättningsprojekt** eller **Lägg till i ett befintligt översättningsprojekt** .
1. Ange titeln i fältet **Projekttitel** . Exempel, `Government Reference Site - German locale.`
1. I fältet **Målspråk** anger du en språkinställning (till exempel `German(de)`) och klickar på **Klar**. Du kan ange flera språkinställningar. Formuläret översätts till alla språk som anges i fältet **Målspråk** .
1. Klicka på **Öppna projekt** i dialogrutan Lexikon tillagd. Öppna det nyskapade projektet på projektskärmen.
1. Klicka på **ellipserna** längst ned i rutan **Översättningssammanfattning** . Skärmen Översättningssammanfattning öppnas.
1. Klicka på ikonen **Redigera** längst upp på skärmen **Översättningssammanfattning** . Öppna fliken **Översättning** och välj Maskinöversättning på skärmen **Översättningsmetod** . Välj lämplig **översättningsprovider** och **molnkonfiguration**. Klicka på ikonen **Klar** längst upp på skärmen.
1. På **översättningsjobbpanelen** klickar du på ![ikonen aem62forms_down](assets/aem62forms_downarrow.png) och sedan på **Start**. Status för rutan ändras till Utkast. När översättningen är klar ändras statusen till **Klar för granskning**. Uppdatera sidan efter några minuter och kontrollera statusen.
1. När statusen har ändrats till **Klar för granskning** på **översättningsjobbpanelen** öppnar du formuläret i ett webbläsarfönster. En lokaliserad version av formuläret visas.

   >[!NOTE]
   >
   >* Innan du öppnar den lokaliserade versionen av formuläret i webbläsarfönstret kontrollerar du att webbläsarens språkområde är inställt så att det matchar formulärets språkområde. Om formuläret t.ex. översätts till tyskt(de)-språk anger du språket för webbläsaren till tyskt(de).
   >* Anpassade formulärkomponenter har inte stöd för höger till vänster-språk. Till exempel hebreiska.


   Tillsammans med det adaptiva formuläret är det automatiskt genererade postdokumentet också lokaliserat.

   Mer information om inställningar och konfiguration för dokument för post finns i:

   [Konfiguration av dokumentmall](/help/forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md#p-document-of-record-template-configuration-p)

   [Dokumentinställningar](/help/forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md#p-document-of-record-settings-p)

1. [Anpassa profileringsinformationen i urkunder](/help/forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md) och se till att webbläsarens språkområde är inställt på samma språk som du har lokaliserat det adaptiva formuläret på maskinspråket. Webbläsarens språkområde hjälper till att lokalisera varumärkesinformationen i urkunder.
1. Om du vill visa det lokaliserade postdokumentet trycker du på Generera förhandsgranskning. Dokumentet med post-PDF genereras och öppnas på en ny flik i webbläsaren.

## Lokalisera en anpassningsbar form och dess urkunder med mänsklig översättning {#localizing-an-adaptive-form-and-its-document-of-record-using-human-translation}

I Personlig översättning skickas innehållet till en översättningsleverantör och översätts av professionella översättare. När det är klart returneras det översatta innehållet och importeras till AEM. När din översättningsleverantör är integrerad med AEM skickas innehåll automatiskt mellan AEM och översättningsleverantören.

För översättning delas en ordlista som innehåller filer i XLIFF-format med de professionella översättarna. Ordlistan innehåller en separat XLIFF-fil för varje språkområde. Varje XLIFF-fil innehåller text som visas för slutanvändarna och platshållarna för motsvarande lokaliserad text.

Utför följande steg för att lokalisera ett formulär och dess urkunder med personalöversättare:

1. [Anslut AEM till din översättningstjänst](/help/sites-administering/tc-tic.md) och [skapa konfigurationer](/help/sites-administering/tc-tic.md)för översättningsintegrering.

1. [Associera sidorna på din språkinställning](/help/sites-administering/tc-tic.md) med översättningstjänsten och ramverkskonfigurationerna.

1. [Identifiera vilken typ av innehåll](/help/sites-administering/tc-rules.md) som ska översättas.

1. [Förbered innehållet för översättning](/help/sites-administering/tc-prep.md) genom att skapa språkinställningen och skapa rotsidorna för språkkopior.

1. [Skapa översättningsprojekt](/help/sites-administering/tc-manage.md) för att samla in innehållet som ska översättas och förbereda översättningsprocessen.

1. Använd översättningsprojekten för att [hantera innehållsöversättningsprocessen](/help/sites-administering/tc-manage.md).

>[!NOTE]
>
>* Anpassade formulärkomponenter har inte stöd för höger till vänster-språk. Till exempel hebreiska.
>



