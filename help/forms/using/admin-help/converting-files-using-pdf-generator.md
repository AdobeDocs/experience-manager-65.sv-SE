---
title: Konvertera filer med PDF Generator
seo-title: Converting files using PDF Generator
description: Lär dig hur du konverterar filer med PDF Generator.
seo-description: Learn how to convert files using PDF Generator.
uuid: 295afb8f-130a-44f5-b0ab-e4c93c0c9e52
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_pdf_generator
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 999ae2be-56ba-48c1-861b-8d4c991a0206
feature: PDF Generator
exl-id: 0e2c12b5-24c8-4aca-8826-cb661051ce4f
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1167'
ht-degree: 0%

---

# Konvertera filer med PDF Generator{#converting-files-using-pdf-generator}

Du kan använda webbsidorna för PDF Generator för att konvertera filer.

## Skapa en PDF-fil {#create-a-pdf-file}

1. I administrationskonsolen klickar du på Tjänster > PDF Generator > Skapa PDF.
1. Klicka på Bläddra för att hitta och markera filen.

   >[!NOTE]
   >
   >PDF Generator kan automatiskt identifiera filtypen för .doc-, .xls-, .ppt- och .rtf-filer, även om filnamnet saknar filtillägget. Den här funktionen fungerar inte med .docx-, .xlsx- och .pptx-filer.

1. Under Konfigurationsinställningar väljer du Använd anpassade inställningar eller Överför inställningsfil.

   * Om du använder anpassade inställningar väljer du en Adobe PDF-inställning, säkerhetsinställning och filtypsinställning och anger en timeout.

      Adobe PDF-inställningarna gäller endast för PS-to-PDF, EPS-to-PDF, PRN-to-PDF, Image-to-PDF med OCR på och Native-to-PDF. Inställningen för timeout anger den maximala tid det tar att slutföra konverteringen. Standardvärdet är 270 sekunder. De här inställningarna används inte vid konvertering mellan Image-to-PDF och OpenOffice-till-PDF.

   * Om du överför en inställningsfil anger du sökvägen och namnet i rutan eller klickar på Bläddra för att hitta och markera filen.

1. (Valfritt) Under XMP Metadatafil skriver du sökvägen och namnet på den XMP filen, eller klickar på Bläddra för att hitta och markera filen. En XMP kan användas för att inkludera standardmetadatainformation. (Se [XMP filer](converting-files-using-pdf-generator.md#about-xmp-files).)
1. Klicka på Skapa. När filen skapas visas en länk till den. Om ett fel inträffar under konverteringen visas en varning. Om du skapar en PostScript-fil innehåller varningen även en länk till loggfilen.
1. Klicka på länken för filen PDF. Filen öppnas i Acrobat.

### XMP filer {#about-xmp-files}

PDF-dokument som skapas i Acrobat 5.0 eller senare med PDF Generator innehåller dokumentmetadata i XML-format. *Metadata* innehåller information om dokumentet och dess innehåll, t.ex. författarens namn, nyckelord och copyrightinformation som sökverktyg kan använda.

Dokumentets metadata innehåller (men är inte begränsade till) information som också visas på fliken Beskrivning i dialogrutan Dokumentegenskaper i Acrobat. Ändringar som görs på fliken Beskrivning återspeglas i dokumentets metadata. Dokumentets metadata kan utökas och ändras med tredjepartsprodukter.

Adobe Extensible Metadata Platform (XMP) ger Adobe-applikationer ett gemensamt XML-ramverk som standardiserar generering, bearbetning och utbyte av dokumentmetadata mellan olika publiceringsarbetsflöden. Du kan spara och importera XML-källkoden för dokumentmetadata i XMP format, vilket gör det enkelt att dela metadata mellan olika dokument. Mer information om XMP finns i [Extensible Metadata Platform (XMP)](https://www.adobe.com/products/xmp/) och [Adobe XMP Developer Center](https://www.adobe.com/devnet/xmp.html).

Du kan skapa XMP filer i Acrobat.

## Konvertera en HTML-fil eller en ZIP-fil till PDF {#convert-an-html-file-or-zip-file-to-pdf}

Du kan använda PDF Generator för att konvertera följande filtyper till Adobe PDF:

* HTML-filer, som du kan konvertera genom att överföra en HTML-fil eller genom att ange webbadressen till en webbsida eller webbplats.
* Arkiverade filer (ZIP), som kan innehålla HTML-filer, bildfiler eller både och.

Om ZIP-filen innehåller mer än en HTML-fil på den lägsta nivån i mapphierarkin måste ZIP-filen också innehålla en index.htm- eller index.html-fil.

>[!NOTE]
>
>* Funktionen HTML till PDF kräver vissa teckensnitt i systemets teckensnittskatalog. I Linux, Solaris och AIX måste systemteckensnittskatalogen innehålla teckensnittet Courier. I Windows måste systemteckensnittskatalogen innehålla Times New Roman.
>
>* (Endast UNIX-baserat system) Ett av följande japanska teckensnitt bör vara tillgängligt på AEM Forms-servern för att konvertera en webbsida med japanskt teckensnitt till ett PDF-dokument.
>
>  * &quot;Sazanami Gothic&quot;
>  * &quot;Kozuka Gothic Pro-VI&quot;
>  * &quot;Kozuka Mincho Pro-VI&quot;
>  * &quot;Sazanami Gothic&quot;
>  * &quot;Kozuka Mincho Pr6N&quot;
>  * &quot;Sazanami Mincho&quot;
>  * &quot;Adobe Heiti Std&quot;
>  * &quot;Adobe Song Std&quot;
>
>* Om du vill överföra en fil från det lokala filsystemet använder du alternativet Överför fil på HTML till PDF.


1. I administrationskonsolen klickar du på Tjänster > PDF Generator > HTML till PDF.
1. Ange vilken fil som ska konverteras genom att göra något av följande:

   * I Överför fil skriver du sökvägen och filnamnet för filen eller ZIP-filen i HTML eller klickar på Bläddra för att leta reda på och markera den.
   * I rutan Ange URL-adress skriver du URL-adressen till sidan eller webbplatsen som ska konverteras.

   >[!NOTE]
   >
   >Filen som du konverterar måste ha filnamnstillägget .html, .htm eller .zip.

1. Ange konfigurationsinställningarna:

   * Om du vill använda anpassade inställningar väljer du Använd anpassade inställningar, anger säkerhets- och filtypsinställningar och anger ett timeout-värde. Standardvärdet är 270 sekunder.
   >[!NOTE]
   >
   >Om du har konfigurerat tjänsten Generate PDF att använda Acrobat WebCapture påverkar inte de filtypsinställningar som du har valt på den här sidan det PDF som skapas. Gör i stället lämpliga ändringar i den version av Acrobat som är installerad på servern.

   * Om du vill använda en befintlig inställningsfil väljer du Överför inställningsfil och klickar på Bläddra för att gå till filplatsen.


1. Om du vill överföra en XMP klickar du på Bläddra och går till filplatsen. En XMP kan användas för att inkludera standardmetadatainformation. (Se [XMP filer](converting-files-using-pdf-generator.md#about-xmp-files).)
1. Klicka på Skapa. När filen skapas visas en länk till filen PDF.
1. Klicka på länken för att visa PDF-dokumentet i Acrobat.

## Exportera en PDF-fil till ett annat filformat (endast Windows) {#export-a-pdf-file-to-another-file-format-windows-only}

Du kan exportera PDF-filer till olika filformat enligt beskrivningen i kapitlet om tjänsten Generera PDF i [Tjänstreferens](https://www.adobe.com/go/learn_aemforms_services_63).

1. I administrationskonsolen klickar du på Tjänster > PDF Generator > Export PDF.
1. Klicka på Bläddra för att leta reda på PDF-filen som ska exporteras.
1. I den Export PDF som du vill visa väljer du det format som du vill exportera filen PDF till.
1. I rutan Ange en timeout anger du väntetiden innan programmet timeout. Standardvärdet är 270 sekunder.

   Konverteringstiden som visas när filen konverteras kan vara större än det värde som du anger här. Konverteringstiden är den tid som har ägnats åt att vänta på tråden eller processen, den tid det tar att konvertera filen och den tid det tar för reservkonverteraren (om tillämpligt). time. Värdet Ange en timeout är bara den tid det tar att konvertera filen.

1. (Valfritt) I dialogrutan **Ange anpassad preflight-profil** , klicka på Bläddra och välj [anpassad preflight-profil](https://helpx.adobe.com/acrobat/using/preflight-profiles-acrobat-pro.html). Preflight-profiler används bara vid konvertering av dokument till PDF-arkivformat (PDF/A).
1. Klicka på Exportera. När konverteringen är klar visas en länk till den exporterade filen.
1. Klicka på länken för att visa den konverterade filen.

## Optimera en PDF (endast Windows) {#optimize-a-pdf}

PDF Generator har stöd för att minska storleken på PDF-filer.

>[!NOTE]
>
>När du optimerar ett digitalt signerat dokument tas de digitala signaturerna bort och blir ogiltiga.

1. I administrationskonsolen klickar du på Tjänster > PDF Generator > Optimize PDF.
1. Klicka på Bläddra för att hitta den PDF-fil som ska optimeras.
1. Ange konfigurationsinställningarna:

   * Om du vill använda anpassade inställningar väljer du Använd anpassade inställningar, anger filtypsinställningar och anger ett timeout-värde. Standardvärdet är 270 sekunder.
   * Om du vill använda en befintlig inställningsfil väljer du Överför inställningsfil och klickar på Bläddra för att gå till filplatsen.

1. Klicka på Skapa.
