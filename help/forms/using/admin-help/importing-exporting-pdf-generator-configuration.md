---
title: Importera och exportera PDF Generator-konfigurationsfiler
seo-title: Importera och exportera PDF Generator-konfigurationsfiler
description: Lär dig hur du importerar och exporterar PDF Generator-konfigurationsfiler.
seo-description: Lär dig hur du importerar och exporterar PDF Generator-konfigurationsfiler.
uuid: 3367253b-d222-4c5f-9455-a1810d96112e
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_pdf_generator
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e25c1b35-73eb-4353-8e39-a2d4cdccd101
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Importera och exportera PDF Generator-konfigurationsfiler {#importing-and-exporting-pdf-generator-configuration-files}

Konfigurationsfilen innehåller PDF-generatorns konverteringsinformation, inklusive PDF-filen, filtypen och säkerhetsinställningarna.

>[!NOTE]
>
>Du kan inte ändra timeout-inställningen för PDF Generator genom att importera en anpassad native2pdfconfig.xml-fil. Tidsgränsen i den filen är endast avsedd som information och den aktuella inställningen visas i PDF Generator. Information om hur du ändrar timeout-inställningen finns i&quot;Setting PDF Generator performance parameters&quot; i [Installera och distribuera AEM-formulär](https://www.adobe.com/go/learn_aemforms_installJBoss_63).

## Exportera den aktuella konfigurationsfilen {#export-your-current-configuration-file}

1. I administrationskonsolen klickar du på Tjänster > PDF-generator > Konfigurationsfiler > Exportera konfiguration.
1. Om du vill exportera inställningarna väljer du lämpligt alternativ:

   * Om du vill exportera alla namngivna inställningar väljer du Hämta hela konfigurationen.
   * Om du bara vill exportera en Adobe PDF-inställning, säkerhetsinställning eller filtypsinställning väljer du Hämta minimal konfiguration.

      Om du exporterar en minimal konfiguration väljer du de Adobe PDF-, säkerhets- och filtypsinställningar som ska exporteras.

1. Klicka på Hämta och spara XML-filen på lämplig plats.

## Importera en konfigurationsfil {#import-a-configuration-file}

>[!NOTE]
>
>Systemet konfigureras om baserat på informationen i den importerade filen.

1. I administrationskonsolen klickar du på Tjänster > PDF-generator > Konfigurationsfiler > Importera konfiguration.
1. Välj Importera en befintlig konfigurationsfil.
1. Om du vill ange filens plats i rutan Konfigurationsfil klickar du på Bläddra för att hitta och markera filen och klickar sedan på **Importera**.

## Konvertera alla lager i AutoCAD-filer {#convert-all-layers-within-autocad-files}

Som standard konverterar PDF Generator bara standardlagret för AutoCAD-filer till PDF i stället för alla lager i filen. Följ den här proceduren om du vill konvertera alla lager.

1. I administrationskonsolen klickar du på Tjänster > PDF-generator > Konfigurationsfiler > Exportera konfiguration.
1. Välj Hämta hela konfigurationen och klicka på Hämta.
1. Öppna den hämtade filen i en textredigerare och lägg till texten under taggen `AutoCAD` i `PDFMaker` -taggen `convertAllPages="true"`.
1. I administrationskonsolen klickar du på Tjänster > PDF-generator > Konfigurationsfiler > Importera konfiguration.
1. Välj Importera en befintlig konfigurationsfil, ange den uppdaterade filen och klicka på Importera.

   Alla AutoCAD-filer som konverteras med den ändrade konfigurationsfilen kommer att konverteras.

## Återställ konfigurationen till de ursprungliga inställningarna som installerades med PDF Generator {#reset-your-configuration-to-the-original-settings-installed-with-pdf-generator}

1. I administrationskonsolen klickar du på Tjänster > PDF-generator > Konfigurationsfiler > Importera konfiguration.
1. Välj Återställ konfiguration till standardinställningar och klicka på Importera.

