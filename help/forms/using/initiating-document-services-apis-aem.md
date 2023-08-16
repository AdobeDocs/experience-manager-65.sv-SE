---
title: Initiera API:er för dokumenttjänster från AEM
seo-title: Initiate Document Services APIs from AEM Workflow
description: Lär dig hur du anropar AEM dokumenttjänster på DDX eller angivna indata. Se även hur du konverterar PDF till PDF/A
seo-description: Learn how to invoke AEM Document services on DDX or supplied inputs. Also see hwo to convert PDF to PDF/A
uuid: aacec2df-1ad6-4ff2-a99d-ef206efcdc09
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: document_services
discoiquuid: 8b85bdc7-3864-49c9-81b0-cf15b8e986d9
exl-id: 123087a2-9d09-4579-9185-2ccd7d25bf8d
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '1160'
ht-degree: 0%

---

# Initiera API:er för dokumenttjänster från AEM  {#initiate-document-services-apis-from-aem-workflow}

## Assembler {#assembler}

AEM Forms tillhandahåller anpassade arbetsflöden för att anropa följande API:er för Assembler-tjänster:

* **invoke**: Anropar åtgärder som anges i indata-DDX för angivna indata.
* **toPDFA**: Konverterar indatadokument från PDF till PDF/A-dokument.

### Anropa DDX-arbetsflöde {#invoke-ddx-workflow}

The **Anropa DDX** arbetsflödet anropar `Invoke` Tjänst-API:t för Assembler, som du kan använda för att montera eller dela upp dokument, lägga till vattenstämpel i en PDF och så vidare.

1. Dra **[!UICONTROL Invoke DDX]** arbetsflödessteg på fliken Forms Workflow i Sidekick.
1. Dubbelklicka på det tillagda arbetsflödessteget för att redigera komponenten.
1. Konfigurera indatadokument, miljöalternativ och utdatadokument i dialogrutan Redigera komponent och klicka på **[!UICONTROL OK]**.

#### Indatadokument {#input-documents}

Anropa DDX-arbetsflödet kräver följande indatadokument:

* **DDX**: Det är en obligatorisk inmatning för steget Anropa DDX-arbetsflöde och kan anges genom att välja något av följande alternativ i den nedrullningsbara menyn DX-inmatning.

   * *Relativt till nyttolast*: DDX-indatafilen är relativ till arbetsflödesobjektets nyttolastmapp.
   * *Använd nyttolast*: Nyttolasten för arbetsflödesobjektet används som indata-DDX-dokument.
   * *Absolut sökväg*: Den absoluta sökvägen till DDX-dokumentet i CRX-databasen.

* **Skapa karta från PayLoad**: När du väljer det här alternativet läggs alla dokument under nyttolastmappen till i Input Document-kartan för `invoke` API i Assembler. Nodnamnet för varje dokument används som en nyckel på kartan.

* **Karta för indatadokument**: Anger kartan för indatadokumentet. Du kan lägga till valfritt antal poster, där varje post anger dokumentets nyckel på kartan och dokumentets källa.

#### Miljöalternativ {#environment-options}

På fliken Miljöalternativ kan du ange olika bearbetningsalternativ för anrops-API:t.

* *Jobbloggnivå*: Anger loggnivån för bearbetningsloggarna.
* *Validera endast*: Kontrollerar giltigheten för indata-DDX.

* *Fel vid fel*: Anger om anropet till Assembler-tjänsten ska misslyckas om ett fel inträffar. Standardvärdet är Falskt.

#### Utdatadokument {#output-documents}

Beroende på indata-DDX kan invoke-API:t generera flera utdatadokument. På fliken Utdatadokument kan du välja var utdatadokumentet ska sparas.

1. *Spara utdata i nyttolast*: Sparar utdatadokument under nyttolastmappen, eller skriver över nyttolasten, om nyttolasten är en fil.
1. *Karta för utdatadokument*: Gör att du uttryckligen kan ange var varje utdatadokument ska sparas genom att lägga till en post per utdatadokument. Varje post anger dokumentet och var det ska sparas. Ett utdatadokument kan skriva över nyttolasten eller sparas under nyttolastmappen. Det är användbart när det finns flera utdatadokument.

1. *Jobblogg*: Anger var jobbloggdokumentet ska sparas, vilket är praktiskt vid felsökning.

### Konvertera till PDF/A-arbetsflöde {#convert-to-pdf-a-workflow}

Arbetsflödessteget Konvertera till PDF/A anropar `toPDFA` Tjänst-API för Assembler. Det används för att konvertera dokument från PDF till dokument som överensstämmer med PDF/A.

1. Dra **[!UICONTROL ConvertToPDFA]** arbetsflödessteg på fliken Forms Workflow i Sidekick.

1. Dubbelklicka på det tillagda arbetsflödessteget för att redigera komponenten.
1. Konfigurera indatadokument, konverteringsalternativ och utdatadokument i dialogrutan Redigera komponent och klicka på **[!UICONTROL OK]**.

#### Indatadokument {#input-documents-1}

Ange källan till dokumentet som ska konverteras till ett PDF/A-kompatibelt dokument på något av följande sätt.

* *Relativt till nyttolast*: Indatadokumentet är relativt till arbetsflödesobjektets nyttolastmapp.
* *Använd nyttolast*: Nyttolasten för arbetsflödesobjektet används som indatadokument.
* *Absolut sökväg*: Den absoluta sökvägen för indatadokumentet i CRX-databasen.

#### Konverteringsalternativ {#conversion-options}

Med konverteringsalternativen kan du ange alternativ som ändrar konverteringsprocessen för PDF/A.

* *Regelefterlevnad* : Anger den PDF/A-standard som utdata från PDF/A måste uppfylla.
* *Resultatnivå* : Anger loggnivån som ska användas för konverteringsloggarna PDF/A.
* *Signaturer* : Anger hur signaturerna i indatadokumentet måste bearbetas under konverteringen.
* *Färgmodell* : Anger den fördefinierade färgrymd som ska användas för utdata i PDF/A-dokument.
* *Verifiera* Konvertering: Anger om det konverterade PDF/A-dokumentet ska verifieras för PDF/A-kompatibilitet efter konvertering.
* *Jobbloggnivå* : Anger loggnivån som ska användas för bearbetning av loggar.

* *Metadata Extension Schema* : Anger sökvägen till metadatatilläggsschemat som ska användas för XMP i PDF-dokumentets metadata.

#### Utdatadokument {#output-documents-1}

På fliken Utdatadokument kan du ange mål för utdatadokumenten

* *PDFA-dokument*: Anger platsen där det konverterade PDF/A-dokumentet sparas. Det kan antingen skriva över nyttolastdokumentet eller sparas under nyttolastmappen.
* *Konverteringslogg*: Anger platsen där konverteringsloggarna sparas. Det kan antingen skriva över nyttolastdokumentet eller sparas under nyttolastmappen.

## Forms {#forms}

Arbetsflödet Återge formulär i PDF är en wrapper runt `renderPDFForm` Forms tjänst-API för att skapa ett PDF-formulär med en XDP-mall och data-xml.

### Arbetsflödet Återge formulär i PDF {#render-pdf-form-workflow}

1. Dra arbetsflödessteget Återge formulär i PDF under fliken Forms Workflow i Sidekick.
1. Dubbelklicka på det tillagda arbetsflödessteget för att redigera komponenten.
1. Konfigurera indatadokument, utdatadokument och andra parametrar i dialogrutan Redigera komponent och klicka på **[!UICONTROL OK]**.

#### Indatadokument {#input-documents-2}

* *Mallfil*: Anger platsen för XDP-mallen. Det är ett obligatoriskt fält.

* *Datadokument*: Anger platsen för data-XML som behöver sammanfogas med mallen.

#### Utdatadokument {#output-documents-2}

* *Utdatadokument*: - Anger namnet på det genererade PDF-formuläret.

#### Ytterligare parametrar {#additional-parameters}

* *Innehållsrot*: Anger sökvägen till mappen i databasen där fragment eller bilder som används i XDP-indatamallen lagras.
* *Skicka URL*: Anger standardwebbadressen för sändning för det genererade PDF-formuläret.
* *Språk*: Anger standardspråkområdet för det genererade PDF-formuläret.
* *Acrobat Version*: Anger Acrobat-målversionen för det genererade PDF-formuläret.
* *Tagged PDF*: Anger om den genererade PDF ska vara tillgänglig.
* *XCI-dokument*: Anger sökvägen till XCI-filen.

## Utdata {#output}

Arbetsflödet Generera icke-interaktiv PDF är en wrapper runt `generatePDFOutput` API för utdatatjänst. Den används för att generera icke-interaktiva PDF-dokument från XDP-mallar och data-xml.

### Skapa icke-interaktivt arbetsflöde för utdata från PDF   {#generate-non-interactive-pdf-output-workflow-nbsp}

1. Dra arbetsflödet Generera icke-interaktiv PDF-utdata på fliken Forms Workflow i Sidekick.
1. Dubbelklicka på det tillagda arbetsflödessteget för att redigera komponenten.
1. Konfigurera indatadokument, utdatadokument och andra parametrar i dialogrutan Redigera komponent och klicka på **[!UICONTROL OK]**.

#### Indatadokument {#input-documents-3}

* *Mallfil*: Anger platsen för XDP-mallen. Det är ett obligatoriskt fält.

* *Datadokument*: Anger platsen för den data-XML som behöver sammanfogas med mallen.

#### Utdatadokument {#output-document}

*Utdatadokument*: Anger namnet på det genererade PDF-formuläret.

#### Ytterligare parametrar {#additional-parameters-1}

* *Innehållsrot*: Anger sökvägen till mappen i databasen där fragment eller bilder som används i XDP-indatamallen lagras.
* *Språk*: Anger standardspråkområdet för det genererade PDF-formuläret.
* *Acrobat Version*: Anger Acrobat-målversionen för det genererade PDF-formuläret.
* Linjäriserad PDF: Anger om den genererade PDF ska optimeras för webbvisning.
* *Tagged PDF*: Anger om den genererade PDF ska vara tillgänglig.
* *XCI-dokument*: Anger sökvägen till XCI-filen.
