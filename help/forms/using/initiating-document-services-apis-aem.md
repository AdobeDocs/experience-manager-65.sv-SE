---
title: Initiera API:er för dokumenttjänster från AEM Workflow
seo-title: Initiera API:er för dokumenttjänster från AEM Workflow
description: Lär dig hur du anropar AEM Document Services på DDX eller angivna indata. Se även hur du konverterar PDF till PDF/A
seo-description: Lär dig hur du anropar AEM Document Services på DDX eller angivna indata. Se även hur du konverterar PDF till PDF/A
uuid: aacec2df-1ad6-4ff2-a99d-ef206efcdc09
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: document_services
discoiquuid: 8b85bdc7-3864-49c9-81b0-cf15b8e986d9
translation-type: tm+mt
source-git-commit: 7caf09f7020c066072eac04a349a19b144dfeb7b

---


# Initiera API:er för dokumenttjänster från AEM Workflow {#initiate-document-services-apis-from-aem-workflow}

## Assembler {#assembler}

AEM Forms innehåller anpassade arbetsflöden för att anropa följande API:er för Assembler-tjänster:

* **invoke**: Anropar åtgärder som anges i in-DDX för angivna indata.
* **toPDFA**: Konverterar PDF-indatadokument till PDF/A-dokument.

### Anropa DDX-arbetsflöde {#invoke-ddx-workflow}

Arbetsflödet **Anropa DDX** anropar API:t för tjänsten `Invoke` Assembler, som du kan använda för att sätta ihop eller dela upp dokument, lägga till vattenstämpel i ett PDF-dokument och så vidare.

1. Dra arbetsflödessteget **[!UICONTROL Anropa DDX]** under fliken Formulärarbetsflöde i Sidekick.
1. Dubbelklicka på det tillagda arbetsflödessteget för att redigera komponenten.
1. Konfigurera indatadokument, miljöalternativ och utdatadokument i dialogrutan Redigera komponent och klicka på **[!UICONTROL OK]**.

#### Indatadokument {#input-documents}

Anropa DDX-arbetsflödet kräver följande indatadokument:

* **DDX**: Det är en obligatorisk inmatning för steget Anropa DDX-arbetsflöde och kan anges genom att välja något av följande alternativ i den nedrullningsbara menyn DX-inmatning.

   * *Relativt till nyttolast*: DDX-indatafilen är relativ till arbetsflödesobjektets nyttolastmapp.
   * *Använd nyttolast*: Nyttolasten för arbetsflödesobjektet används som indata-DDX-dokument.
   * *Absolut sökväg*: Den absoluta sökvägen till DDX-dokumentet i CRX-databasen.

* **Skapa karta från PayLoad**: När du väljer det här alternativet läggs alla dokument under nyttolastmappen till i Input Document Map för API:t i `invoke` Assembler. Nodnamnet för varje dokument används som en nyckel på kartan.

* **Indatadokumentets karta**: Anger indatadokumentets karta. Du kan lägga till valfritt antal poster, där varje post anger dokumentets nyckel på kartan och dokumentets källa.

#### Miljöalternativ {#environment-options}

På fliken Miljöalternativ kan du ange olika bearbetningsalternativ för anrops-API:t.

* *Jobbloggnivå*: Anger loggnivån för bearbetningsloggarna.
* *Endast* validering: Kontrollerar giltigheten för indata-DDX.

* *Fel*: Anger om anropet till Assembler-tjänsten ska misslyckas om ett fel inträffar. Standardvärdet är Falskt.

#### Utdatadokument {#output-documents}

Beroende på indata-DDX kan invoke-API:t generera flera utdatadokument. På fliken Utdatadokument kan du välja var utdatadokumentet ska sparas.

1. *Spara utdata i nyttolast*: Sparar utdatadokument under nyttolastmappen, eller skriver över nyttolasten om nyttolasten är en fil.
1. *Utdatadokumentets karta*: Tillåter att du uttryckligen anger var varje utdatadokument ska sparas genom att lägga till en post per utdatadokument. Varje post anger dokumentet och var det ska sparas. Ett utdatadokument kan skriva över nyttolasten eller sparas under nyttolastmappen. Det är användbart när det finns flera utdatadokument.

1. *Jobblogg*: Anger var jobbloggdokumentet ska sparas, vilket är praktiskt vid felsökning.

### Konvertera till PDF/A-arbetsflöde {#convert-to-pdf-a-workflow}

Arbetsflödessteget Konvertera till PDF/A anropar `toPDFA` Assembler-tjänstens API. Det används för att konvertera PDF-dokument till PDF/A-kompatibla dokument.

1. Dra arbetsflödessteget **[!UICONTROL ConvertToPDFA]** under fliken Formulärarbetsflöde i Sidekick.

1. Dubbelklicka på det tillagda arbetsflödessteget för att redigera komponenten.
1. Konfigurera indatadokument, konverteringsalternativ och utdatadokument i dialogrutan Redigera komponent och klicka på **[!UICONTROL OK]**.

#### Indatadokument {#input-documents-1}

Ange källan till dokumentet som ska konverteras till ett PDF/A-kompatibelt dokument på något av följande sätt.

* *Relativt till nyttolast*: Indatadokumentet är relativt till arbetsflödesobjektets nyttolastmapp.
* *Använd nyttolast*: Nyttolasten för arbetsflödesobjektet används som indatadokument.
* *Absolut sökväg*: Den absoluta sökvägen för indatadokumentet i CRX-databasen.

#### Konverteringsalternativ {#conversion-options}

Med konverteringsalternativen kan du ange alternativ som ändrar PDF/A-konverteringsprocessen.

* *Efterlevnad* : Anger den PDF/A-standard som PDF/A-utdata måste uppfylla.
* *Resultatnivå* : Anger loggnivån som ska användas för PDF/A-konverteringsloggar.
* *Underskrifter* : Anger hur signaturer i indatadokument måste bearbetas under konverteringen.
* *Färgmodell* : Anger den fördefinierade färgrymd som ska användas för PDF/A-utdata.
* *Verifiera* konvertering: Anger om det konverterade PDF/A-dokumentet ska verifieras för PDF/A-kompatibilitet efter konvertering.
* *Jobbloggnivå* : Anger loggnivån som ska användas för bearbetning av loggar.

* *Metadatatilläggsschema* : Anger sökvägen till metadatatilläggsschemat som ska användas för XMP-egenskaper i PDF-dokumentets metadata.

#### Utdatadokument {#output-documents-1}

På fliken Utdatadokument kan du ange mål för utdatadokumenten

* *PDFA-dokument*: Anger platsen där det konverterade PDF/A-dokumentet sparas. Det kan antingen skriva över nyttolastdokumentet eller sparas under nyttolastmappen.
* *Konverteringslogg*: Anger platsen där konverteringsloggarna sparas. Det kan antingen skriva över nyttolastdokumentet eller sparas under nyttolastmappen.

## Formulär {#forms}

Arbetsflödet för att återge PDF-formulär är en wrapper runt `renderPDFForm` Forms tjänst-API:t för att skapa ett PDF-formulär med en XDP-mall och data-xml.

### Arbetsflöde för PDF-formulär {#render-pdf-form-workflow}

1. Dra arbetsflödessteget Återge PDF-formulär under fliken Formulärarbetsflöde i Sidekick.
1. Dubbelklicka på det tillagda arbetsflödessteget för att redigera komponenten.
1. Konfigurera indatadokument, utdatadokument och andra parametrar i dialogrutan Redigera komponent och klicka sedan på **[!UICONTROL OK]**.

#### Indatadokument {#input-documents-2}

* *Mallfil*: Anger XDP-mallens plats. Det är ett obligatoriskt fält.

* *Datadokument*: Anger platsen för data-XML som behöver sammanfogas med mallen.

#### Utdatadokument {#output-documents-2}

* *Utdatadokument*: - Anger namnet på det genererade PDF-formuläret.

#### Ytterligare parametrar {#additional-parameters}

* *Innehållsrot*: Anger sökvägen till mappen i databasen där fragment eller bilder som används i XDP-indatamallen lagras.
* *Skicka URL*: Anger standard-URL för att skicka PDF-formulär som genereras.
* *Språk*: Anger standardspråk för det genererade PDF-formuläret.
* *Acrobat-version*: Anger målversionen av Acrobat för det genererade PDF-formuläret.
* *Taggad PDF*: Anger om den genererade PDF-filen ska vara tillgänglig eller inte.
* *XCI-dokument*: Anger sökvägen till XCI-filen.

## Output {#output}

Arbetsflödet Generera icke-interaktiv PDF är en wrapper runt API:t för `generatePDFOutput` utdatatjänster. Den används för att generera icke-interaktiva PDF-dokument från XDP-mallar och data-xml.

### Generera icke-interaktivt arbetsflöde för PDF-utdata {#generate-non-interactive-pdf-output-workflow-nbsp}

1. Dra arbetsflödet för att generera icke-interaktiva PDF-utdata på fliken Formulärarbetsflöde i Sidekick.
1. Dubbelklicka på det tillagda arbetsflödessteget för att redigera komponenten.
1. Konfigurera indatadokument, utdatadokument och andra parametrar i dialogrutan Redigera komponent och klicka sedan på **[!UICONTROL OK]**.

#### Indatadokument {#input-documents-3}

* *Mallfil*: Anger XDP-mallens plats. Det är ett obligatoriskt fält.

* *Datadokument*: Anger platsen för den data-XML som behöver sammanfogas med mallen.

#### Utdatadokument {#output-document}

*Utdatadokument*: Anger namnet på det genererade PDF-formuläret.

#### Ytterligare parametrar {#additional-parameters-1}

* *Innehållsrot*: Anger sökvägen till mappen i databasen där fragment eller bilder som används i XDP-indatamallen lagras.
* *Språk*: Anger standardspråk för genererade PDF-formulär.
* *Acrobat-version*: Anger målversionen av Acrobat för det genererade PDF-formuläret.
* Linjär PDF: Anger om den genererade PDF-filen ska optimeras för webbvisning.
* *Taggad PDF*: Anger om den genererade PDF-filen ska vara tillgänglig eller inte.
* *XCI-dokument*: Anger sökvägen till XCI-filen.

