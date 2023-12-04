---
title: Använda arbetsflöde för AEM översättning för att lokalisera anpassningsbara formulär och urkunder
seo-title: Using AEM translation workflow to localize adaptive forms and document of record
description: Lär dig använda AEM arbetsflöden för översättning för att lokalisera adaptiva formulär och urkunder.
seo-description: Learn to use AEM translation workflows to localize adaptive forms and document of record.
uuid: 6c87a283-0203-4cf7-989a-3770ddbbbd6e
content-type: reference
topic-tags: develop
discoiquuid: f5642571-9657-4ca1-93c5-4ae2eb91e967
noindex: true
feature: Adaptive Forms
exl-id: ebec03a3-67a0-4ecd-84bb-8580388e048a
source-git-commit: bd86d647fdc203015bc70a0f57d5b94b4c634bf9
workflow-type: tm+mt
source-wordcount: '802'
ht-degree: 0%

---

# Använda arbetsflöde för AEM översättning för att lokalisera anpassningsbara formulär och urkunder {#using-aem-translation-workflow-to-localize-adaptive-forms-and-document-of-record}

<span class="preview"> Adobe rekommenderar att man använder modern och utbyggbar datainhämtning [Kärnkomponenter](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html) for [skapa ny Adaptive Forms](/help/forms/using/create-an-adaptive-form-core-components.md) eller [lägga till adaptiv Forms på AEM Sites-sidor](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). De här komponenterna utgör ett betydande framsteg när det gäller att skapa adaptiva Forms-filer, vilket ger imponerande användarupplevelser. I den här artikeln beskrivs det äldre sättet att skapa Adaptiv Forms med baskomponenter. </span>

Lokaliserade formulär hjälper er att nå en större publik över alla länder. Adobe Experience Manager arbetsflöde för översättning hjälper dig att lokalisera anpassningsbara formulär och deras urkunder. Du kan använda **maskinöversättning** eller **mänskliga översättare** för att lokalisera ett anpassat formulär.

I den här artikeln förklaras hur du använder AEM arbetsflöde för översättning med anpassningsbara formulär och urkunder.

## Lokalisera ett anpassat formulär och dokument med post med maskinöversättning {#localizing-an-adaptive-form-and-document-of-record-using-machine-translation}

Maskinöversättningstjänsten översätter omedelbart ditt innehåll i adaptiv form och i ett urklippsdokument. AEM Forms är förkonfigurerat för att använda en testversion av Microsoft Translator för maskinöversättning. Utför följande steg för att aktivera maskinöversättning för anpassade formulär och registerdokument:

1. Markera ett formulär i användargränssnittet för AEM Forms och välj **Lägg till ordlista** alternativ.
1. I **Lägg till ordlista i översättningsprojekt** väljer du **Skapa ett nytt översättningsprojekt** eller **Lägg till i ett befintligt översättningsprojekt** alternativ.
1. I **Projektets titel** anger du rubriken. Exempel: `Government Reference Site - German locale.`
1. I **Målspråk** anger du nationella inställningar (till exempel `German(de)`) och klicka på **Klar**. Du kan ange flera språkinställningar. Formuläret översätts till alla språkområden som anges i **Målspråk** fält.
1. I dialogrutan Lexikon tillagd klickar du på **Öppna projekt**. Öppna det nyskapade projektet på projektskärmen.
1. Klicka på **ellipser** längst ned i **Översättningssammanfattning** platta. Skärmen Översättningssammanfattning öppnas.
1. Klicka på **Redigera** ikonen längst upp på **Översättningssammanfattning** skärm. Öppna **Översättning** och välj Maskinöversättning i **Översättningsmetod** skärm. Välj lämplig **Översättningsprovider** och **Molnkonfiguration**. Klicka på **Klar** ikonen längst upp på skärmen.
1. På **Översättningsjobb** platta, klicka på ![aem62forms_down](assets/aem62forms_downarrow.png) och klicka på **Starta**. Status för rutan ändras till Utkast. När översättningen är klar ändras statusen till **Klar för granskning**. Uppdatera sidan efter några minuter och kontrollera statusen.
1. Efter statusändringen ändras till **Klar för granskning** på **Översättningsjobb** öppnar du formuläret i ett webbläsarfönster. En lokaliserad version av formuläret visas.

   >[!NOTE]
   >
   >* Innan du öppnar den lokaliserade versionen av formuläret i webbläsarfönstret kontrollerar du att webbläsarens språkområde är inställt så att det matchar formulärets språkområde. Om formuläret t.ex. översätts till tyskt(de)-språk anger du språket för webbläsaren till tyskt(de).
   >* Anpassade formulärkomponenter har inte stöd för RTL-språk (right to left). Till exempel hebreiska.

   Tillsammans med det adaptiva formuläret är det automatiskt genererade postdokumentet också lokaliserat.

   Mer information om inställningar och konfiguration för dokument för post finns i:

[Konfiguration av dokumentmall](/help/forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md#p-document-of-record-template-configuration-p)

[Dokumentinställningar](/help/forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md#p-document-of-record-settings-p)

1. [Anpassa varumärkesinformationen i urkunder](/help/forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md) och se till att webbläsarens språkområde är inställt på samma språk som du har lokaliserat det adaptiva formuläret med hjälp av datorspråket. Webbläsarens språkområde hjälper till att lokalisera varumärkesinformationen i urkunder.
1. Om du vill visa det lokaliserade postdokumentet väljer du Generera förhandsgranskning. Dokumentet med posten PDF skapas och öppnas på en ny flik i webbläsaren.

## Lokalisera en anpassningsbar form och dess urkunder med mänsklig översättning {#localizing-an-adaptive-form-and-its-document-of-record-using-human-translation}

I Personlig översättning skickas innehållet till en översättningsleverantör och översätts av professionella översättare. När det är klart returneras det översatta innehållet och importeras till AEM. När översättningsleverantören är integrerad med AEM skickas innehåll automatiskt mellan AEM och översättningsleverantören.

För översättning delas en ordlista som innehåller filer i XLIFF-format med de professionella översättarna. Ordlistan innehåller en separat XLIFF-fil för varje språkområde. Varje XLIFF-fil innehåller text som visas för slutanvändarna och platshållarna för motsvarande lokaliserad text.

Utför följande steg för att lokalisera ett formulär och dess urkunder med personalöversättare:

1. [Anslut AEM till översättningstjänstleverantören](/help/sites-administering/tc-tic.md) och [skapa konfigurationer för översättningsintegreringsramverk](/help/sites-administering/tc-tic.md).

1. [Associera sidorna i din språkinställning](/help/sites-administering/tc-tic.md) med översättningstjänsten och ramverkskonfigurationerna.

1. [Identifiera innehållstypen](/help/sites-administering/tc-rules.md) att översätta.

1. [Förbered innehållet för översättning](/help/sites-administering/tc-prep.md) genom att skapa språkinställningarna och skapa rotsidorna för språkkopior.

1. [Skapa översättningsprojekt](/help/sites-administering/tc-manage.md) för att samla det innehåll som ska översättas och förbereda översättningsprocessen.

1. Använd översättningsprojekt för att [hantera innehållsöversättningsprocessen](/help/sites-administering/tc-manage.md).

>[!NOTE]
>
>* Anpassade formulärkomponenter har inte stöd för RTL-språk (right to left). Till exempel hebreiska.
>
