---
title: Forms Service
seo-title: Forms Service
description: Artikeln beskriver Forms-tjänsten och de formulärrelaterade åtgärder du kan utföra med hjälp av Forms-tjänsten.
seo-description: Artikeln beskriver Forms-tjänsten och de formulärrelaterade åtgärder du kan utföra med hjälp av Forms-tjänsten.
uuid: 3258d3c2-8755-4815-8c97-b2cfb9a9dfd4
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: document_services
discoiquuid: a9695d10-43ec-40eb-942f-7720abaa0973
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Forms Service {#forms-service}

## Översikt {#overview}

Med Forms-tjänsten kan du skapa interaktiva klientprogram för datainhämtning som validerar, bearbetar, omvandlar och levererar formulär som vanligtvis skapas i Designer. Forms-tjänsten återger alla formulärdesigner som du utvecklar som PDF-dokument.

Med Forms-tjänsten kan man också utöka sina intelligenta datainhämtningsprocesser genom att använda elektroniska blanketter som Adobe PDF-filer. Du kan också använda tjänsten för att importera och exportera data till och från befintliga PDF-formulär.

Använd Forms-tjänsten för att göra följande:

* Återge PDF-formulär baserade på mallar och XML-data.
* Möjliggör integrering av formulärdata för import av data till och extrahering av data från PDF-formulär.
* Rendera formulär baserat på fragment.

## Skapa PDF-formulär {#creating-pdf-forms-nbsp}

Använd Form Service för att skapa PDF-blanketter för datainhämtning. Vanligtvis börjar du med en AEM Forms Designer-mall. Använd `renderPDFForm` åtgärden (länk till Javadoc) för Forms-tjänsten för att konvertera den här mallen till ett PDF-formulär.

Den första parametern i `renderPDFForm` åtgärden är namnet på mallfilen (till exempel `ExpenseClaim.xdp`). Du kan lagra mallfilen i ett lokalt filsystem, i en CRX-databas eller på en HTTP- eller FTP-plats. Du kan ange platsen för mallfilen genom att ange innehållsroten i `PDFFormRenderOptions` parametern för `renderPDFForm` åtgärden. Se Javadoc för mer information om andra alternativ som du kan ange för `PDFFormRenderOptions` parametern.

XML-data kan också accepteras i `renderPDFForm` åtgärden. XML-data sammanfogas med mallen när du skapar ett PDF-formulär så att det genererade PDF-formuläret innehåller angivna data. Den andra parametern för `renderPDFForm` åtgärden kan acceptera ett Document-objekt (Javadoc) som innehåller XML-data.

## Extrahera data från PDF-formulär {#extracting-data-from-pdf-forms-nbsp}

Använd `exportData` Javadoc-åtgärden i Forms-tjänsten för att extrahera data-XML från ett PDF-formulär. Den här åtgärden accepterar ett dokument som sin första parameter. Du kan exportera data antingen som ett XDP-dokument eller som en XML-fil. Om du exporterar data som en XML-fil tar exporterade data bort XDP-kuvertet och returnerar en vanlig XML-fil. Du kan ange den här ordningen med den andra parametern.

## Importera data till PDF-formulär {#importing-data-into-pdf-forms}

Med Forms-tjänsten kan du även sammanfoga ett PDF-formulär som har skapats med antingen AEM Forms Designer eller med XML-data. `renderPDFForm` Forms-tjänstens `importData` (Javadoc) åtgärd godkänner PDF-formuläret och XML-data och returnerar ett PDF-formulär med data-XML.

## Återge formulär som bygger på fragment {#rendering-forms-based-on-fragments}

Forms-tjänsten kan återge formulär baserat på fragment som du skapar med hjälp av AEM Forms Designer. Ett fragment är en återanvändbar del av ett formulär. Den sparas som en separat XDP-fil som kan infogas i flera formulärdesigner. Ett fragment kan t.ex. innehålla ett adressblock eller juridisk text.

Med fragment blir det enklare och snabbare att skapa och underhålla stora mängder formulär. När du skapar ett formulär infogar du en referens till det fragment som krävs för att fragmentet ska visas i formuläret. Fragmentreferensen innehåller ett delformulär som pekar på den fysiska XDP-filen.

Nedan följer några fördelar med att använda fragment:

* **Återanvändning** av innehåll: Du kan återanvända innehåll i flera formulärdesigner. Om du snabbt vill återanvända delar av samma innehåll i flera formulär skapar du ett fragment. Det tar längre tid att kopiera eller återskapa innehållet. Att använda fragment innebär att ofta använda delar av en formulärdesign har konsekvent innehåll och utseende i alla refererande formulär.
* **Globala uppdateringar**: Du kan bara göra globala ändringar i flera formulär en gång i en fil. Du kan ändra innehåll, skriptobjekt, databindningar, layout eller format i ett fragment. Alla XDP-formulär som refererar till fragmentet återspeglar ändringarna.
* **Skapa** delade formulär: Du kan dela skapandet av formulär med flera resurser. Formulärutvecklare med expertis inom skript eller andra avancerade funktioner i AEM Forms Designer kan utveckla och dela fragment som använder skript och dynamiska egenskaper. Formulärdesigners kan använda fragmenten för att utforma formulär. Dessutom kan de använda fragmenten för att säkerställa att alla delar av ett formulär har ett konsekvent utseende och funktion i flera formulär.

