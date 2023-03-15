---
title: Forms Service
seo-title: Forms Service
description: Artikeln beskriver Forms-tjänsten och de formulärrelaterade uppgifter du kan utföra med tjänsten Forms.
seo-description: The article describes Forms service and the form-related tasks you can perform using Forms service.
uuid: 3258d3c2-8755-4815-8c97-b2cfb9a9dfd4
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: document_services
discoiquuid: a9695d10-43ec-40eb-942f-7720abaa0973
exl-id: bd1216e4-2248-484b-a3c1-c209da4ff94f
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '685'
ht-degree: 5%

---

# Forms Service {#forms-service}

## Översikt {#overview}

Med tjänsten Forms kan du skapa interaktiva klientapplikationer för datainhämtning som validerar, bearbetar, omvandlar och levererar blanketter som vanligtvis skapas i Designer. Forms-tjänsten återger alla formulärdesigner som du utvecklar som PDF-dokument.

Med Forms tjänster kan man också utöka sina intelligenta datainhämtningsprocesser genom att använda elektroniska blanketter som Adobe PDF. Du kan också använda tjänsten för att importera och exportera data till och från befintliga PDF forms.

Använd tjänsten Forms för att göra följande:

* Rendera PDF forms baserat på mall- och XML-data.
* Möjliggör integrering av formulärdata för import av data till och extrahering av data från PDF forms.
* Rendera formulär baserat på fragment.

## Skapar PDF forms  {#creating-pdf-forms-nbsp}

Använd formulärtjänsten för att skapa PDF forms för datainhämtning. Vanligtvis börjar du med en AEM Forms Designer-mall. Använd `renderPDFForm` (länk till Javadoc) Hur Forms-tjänsten ska konvertera den här mallen till ett PDF-formulär.

Den första parametern i `renderPDFForm` operation är namnet på mallfilen (till exempel `ExpenseClaim.xdp`). Du kan lagra mallfilen i ett lokalt filsystem, i en CRX-databas eller på en HTTP- eller FTP-plats. Du kan ange platsen för mallfilen genom att ange innehållsroten i `PDFFormRenderOptions` parametern för `renderPDFForm` operation. I Javadoc finns mer information om andra alternativ som du kan ange för `PDFFormRenderOptions` parameter.

The `renderPDFForm` -åtgärden kan också acceptera XML-data. XML-data sammanfogas med mallen när du skapar ett PDF-formulär så att det genererade PDF-formuläret innehåller angivna data. Den andra parametern för `renderPDFForm` kan acceptera ett Document-objekt (Javadoc) som innehåller XML-data.

## Extrahera data från PDF forms  {#extracting-data-from-pdf-forms-nbsp}

Använd `exportData` (Javadoc) Forms-tjänstens åtgärd för att extrahera data-XML från ett PDF-formulär. Den här åtgärden accepterar ett dokument som sin första parameter. Du kan exportera data antingen som ett XDP-dokument eller som en XML-fil. Om du exporterar data som en XML-fil tar exporterade data bort XDP-kuvertet och returnerar en vanlig XML-fil. Du kan ange den här ordningen med den andra parametern.

## Importera data till PDF forms {#importing-data-into-pdf-forms}

Med tjänsten Forms kan du även sammanfoga formulär i PDF som skapats med antingen AEM Forms Designer eller `renderPDFForm` med XML-data. The `importData` (Javadoc) Forms-tjänsten godkänner PDF-blanketten och XML-data och returnerar ett PDF-formulär med data-XML.

## Återge formulär som bygger på fragment {#rendering-forms-based-on-fragments}

Forms kan återge formulär baserat på fragment som du skapar med AEM Forms Designer. Ett fragment är en återanvändbar del av ett formulär. Den sparas som en separat XDP-fil som kan infogas i flera formulärdesigner. Ett fragment kan t.ex. innehålla ett adressblock eller juridisk text.

Med fragment blir det enklare och snabbare att skapa och underhålla stora mängder formulär. När du skapar ett formulär infogar du en referens till det fragment som krävs för att fragmentet ska visas i formuläret. Fragmentreferensen innehåller ett delformulär som pekar på den fysiska XDP-filen.

Nedan följer några fördelar med att använda fragment:

* **Återanvändning av innehåll**: Du kan återanvända innehåll i flera formulärdesigner. Om du snabbt vill återanvända delar av samma innehåll i flera formulär skapar du ett fragment. Det tar längre tid att kopiera eller återskapa innehållet. Att använda fragment innebär att ofta använda delar av en formulärdesign har konsekvent innehåll och utseende i alla refererande formulär.
* **Globala uppdateringar**: Du kan bara göra globala ändringar i flera formulär en gång i en fil. Du kan ändra innehåll, skriptobjekt, databindningar, layout eller format i ett fragment. Alla XDP-formulär som refererar till fragmentet återspeglar ändringarna.
* **Skapa delade formulär**: Du kan dela skapandet av formulär med flera resurser. Blankettutvecklare med expertkunskaper inom skript eller andra avancerade funktioner i AEM Forms Designer kan utveckla och dela fragment som använder skript och dynamiska egenskaper. Formulärdesigners kan använda fragmenten för att utforma formulär. Dessutom kan de använda fragmenten för att säkerställa att alla delar av ett formulär har ett konsekvent utseende och funktion i flera formulär.
