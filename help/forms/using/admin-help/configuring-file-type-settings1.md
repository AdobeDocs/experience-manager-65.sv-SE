---
title: Konfigurerar filtypsinställningar
description: Lär dig hur du konfigurerar filtypsinställningar.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_pdf_generator
products: SG_EXPERIENCEMANAGER/6.5/FORMS
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '5866'
ht-degree: 0%

---


# Konfigurerar filtypsinställningar {#configuring-file-type-settings}

I PDF Generator kan du ange programinställningar för de filtyper som stöds. I Windows kan du ange programinställningar för varje filtyp som stöds. I UNIX och Linux kan du ange programinställningar för HTML till PDF och OpenOffice.

På sidan Filtypsinställningar kan du utföra följande uppgifter:

* [Skapa eller redigera en filtypsinställning](#create-or-edit-file-type-settings)
* Ange vilka filtypsinställningar som ska användas som standard (se [Importera och exportera konfigurationsfiler för PDF Generator](https://helpx.adobe.com/aem-forms/6-2/admin-help/importing-exporting-pdf-generator-configuration.html))
* [Ändra standardinställningarna](/help/forms/using/admin-help/configuring-file-type-settings1.md#change-the-default-settings)
* [Aktivera stöd för PDF/A](https://helpx.adobe.com/aem-forms/6-2/admin-help/enable-pdf-a-support.html)
* [Ta bort en filtypsinställning](https://helpx.adobe.com/aem-forms/6-2/admin-help/enable-pdf-a-support.html)

>[!NOTE]
>
>Filtypsinställningarna är inte tillgängliga för reservkonverterare som Acrobat för HTML till PDF, Microsoft PowerPoint, Microsoft Word och Microsoft Excel.

## Skapa eller redigera filtypsinställningar {#create-or-edit-file-type-settings}

Skapa eller redigera en filtypsinställning för att ange hur konverteringen av filtyper som stöds ska hanteras i programmet. I Windows kan du ange programinställningar för varje filtyp som stöds. I UNIX och Linux kan du ange programinställningar för HTML till PDF och OpenOffice.

1. I administrationskonsolen klickar du på **[!UICONTROL Services]** > **[!UICONTROL PDF Generator]** > **[!UICONTROL File Type Settings]**.
1. Klicka på Ny eller klicka på namnet på en inställning.
1. I rutan Filnamnstillägg skriver du filnamnstilläggen, avgränsade med kommatecken, för filtyper som stöds för det här programmet. Ta inte med punkten före eller ett mellanrum mellan tilläggen. Standardvärdet är `bmp,gif,jpeg,jpg,tif,tiff,png`.
1. (Valfritt) Om du vill använda optisk kodigenkänning (OCR) av text i bilder eller bilder markerar du Använd OCR och anger följande alternativ:

**Primärt OCRLanguage:** Det språk som OCR-motorn ska använda för att identifiera tecknen. Standardvärdet är engelska (USA).

**Utdataformat för PDF:** Välj Sökbar bild om du vill att en bitmappsbild av sidorna i förgrunden och den skannade texten ska visas på ett osynligt lager under. Utseendet på sidan ändras inte, men texten kan markeras och läsas. Markera Formaterad text och grafik om du vill rekonstruera originalsidan med hjälp av identifierad text, teckensnitt, bilder och andra grafiska element. Standardinställningen är Sökbar bild (exakt).

**Nedsampla bilder:** Minskar antalet pixlar i färgbilder, gråskalebilder och monokroma bilder. Nedsampling av skannade bilder utförs när OCR har slutförts. Standardvärdet är Lägsta (600 dpi). Det här alternativet är inte tillgängligt om du ställer in PDF som sökbar bild (exakt).

1. Fyll i nödvändig information i dessa avsnitt:

   [Importera och exportera konfigurationsfiler för PDF Generator](https://helpx.adobe.com/aem-forms/6-2/admin-help/importing-exporting-pdf-generator-configuration.html)

[Exportinställningar för Adobe PDF (endast Windows)](#adobe-pdf-export-settings-windows-only)

[HTML till PDF](#html-to-pdf-settings)

[Flash videoklipp till PDF](#flash-videos-to-pdf-settings)

[Inställningar för XPS till PDF](#xps-to-pdf-settings)

[Optimeringsinställningar för PDF](#pdf-optimizer-settings)

[Microsoft Excel-inställningar (endast Windows)](/help/forms/using/admin-help/configuring-file-type-settings1.md#microsoft-excel-settings-windows-only)

[Microsoft PowerPoint-inställningar (endast Windows)](/help/forms/using/admin-help/configuring-file-type-settings1.md#microsoft-powerpoint-settings-windows-only)

[Microsoft Project-inställningar (endast Windows)](/help/forms/using/admin-help/configuring-file-type-settings1.md#microsoft-project-settings-windows-only)

[Inställningar för Microsoft Word (endast Windows)](/help/forms/using/admin-help/configuring-file-type-settings1.md#microsoft-word-settings-windows-only)

[Inställningar för Microsoft Visio (endast Windows)](#visio)

[Inställningar för Microsoft Publisher (endast Windows)](/help/forms/using/admin-help/configuring-file-type-settings1.md#microsoft-publisher-settings-windows-only)

[AutoCAD-inställningar (endast Windows)](/help/forms/using/admin-help/configuring-file-type-settings1.md#autocad-settings-windows-only)

[OpenOffice-inställningar](/help/forms/using/admin-help/configuring-file-type-settings1.md#openoffice-settings)

[Inställningar för andra program (endast Windows)](#other-applications-settings-windows-only)

   Om du vill gå till ett annat avsnitt klickar du på länken på webbsidan eller använder **[!UICONTROL Next]**eller **[!UICONTROL Previous]** knappar.

1. När du är klar med alla avsnitt klickar du på **[!UICONTROL Save]** eller **[!UICONTROL Save As]** och ange ett namn för inställningen.

Stöd för olika filtyper kan anpassas. (Se &quot; [Stöd för fler filformat](https://help.adobe.com/en_US/AEMForms/6.1/ProgramLC/WS624e3cba99b79e12e69a9941333732bac8-7756.2.html)&quot; in [Programmera med AEM](https://www.adobe.com/go/learn_lc_programming_11).)

## Ändra standardinställningarna {#change-the-default-settings}

Du kan ändra standardvärdet för de Adobe PDF-inställningar, säkerhetsinställningar och filtypsinställningar som gäller för nya källor. Om du ändrar standardinställningarna påverkas inte inställningarna för befintliga källor.

1. I administrationskonsolen klickar du på **[!UICONTROL Services > PDF Generator]**.
1. På **[!UICONTROL Adobe PDF Settings]**, **[!UICONTROL File Type Settings]**, eller **[!UICONTROL Security Settings]** sida, klicka **[!UICONTROL Set Default Settings]**.
1. Välj standardinställningar. En eller flera av följande inställningar är tillgängliga på sidan Ange standardinställningar:

   **[!UICONTROL Adobe PDF Setting]**: Det ursprungliga standardvärdet är Standard (Acrobat 6).

   **[!UICONTROL Security Settings]**: Det ursprungliga standardvärdet är Ingen säkerhet (Acrobat 5).

   **[!UICONTROL File Type Settings]**: Det ursprungliga standardvärdet är Standard.

1. Klicka på **[!UICONTROL Save]**.

## Ta bort en filtypsinställning {#delete-a-file-type-setting}

Du kan ta bort en filtypsinställning som inte längre används.

1. I administrationskonsolen klickar du på **[!UICONTROL Services > PDF Generator> File Type Settings]**.
1. Markera kryssrutan bredvid inställningen som ska tas bort. Du kan välja flera källor. Inställningar som inte har någon kryssruta bredvid sig tas alltid med i PDF Generator och kan inte tas bort.
1. Klicka **[!UICONTROL Delete]** och på sidan Ta bort bekräftelse klickar du på **[!UICONTROL Delete]**.

## Inställningar för bild till PDF {#image-to-pdf-settings}

Följande alternativ bestämmer hur bildfiler konverteras till PDF. Instruktioner om hur du använder dessa inställningar finns i [Skapa eller redigera filtypsinställningar](configuring-file-type-settings.md#create-or-edit-file-type-settings).

**Filnamnstillägg:** Kommaavgränsad lista med filnamnstillägg som kan konverteras.

**Prova Fallback Converter:** PDF Generator kan använda Java™ eller Acrobat för att konvertera bildfiler till PDF. När det här alternativet är markerat och en konvertering misslyckas eller når den angivna tidsgränsen, försöker PDF Generator konverteringen med den alternativa metoden. Om den alternativa metoden misslyckas eller når den angivna tidsgränsen, skrivs ett undantag till loggfilen.

>[!NOTE]
>
>JPEG 2000-filer kan bara konverteras med Acrobat.

**Använd OCR:** Anger om OCR (optisk teckenigenkänning) ska användas på PDF. Med OCR kan du söka efter, korrigera och kopiera texten i PDF.

***anteckning **: Funktionen OCR PDF (sökbar PDF) stöds bara i Microsoft Windows.*

**Primärt OCR-språk:** Anger språket som OCR-motorn ska använda för att identifiera tecknen.

**Utdataformat för PDF:** Anger vilken typ av PDF som ska produceras. Alla format tillämpar OCR och teckensnitts- och sidigenkänning på textbilderna och konverterar dem till normal text.

**Sökbar bild:** Ser till att texten är sökbar och markeringsbar. Med det här alternativet behålls originalbilden, den skevas efter behov och ett osynligt textlager placeras över den. Alternativet Nedsampla bilder avgör om bilden nedsamplas och i vilken utsträckning.

**Sökbar bild (exakt):** Ser till att texten är sökbar och markeringsbar. Med det här alternativet behålls originalbilden och ett osynligt textlager placeras över den. Rekommenderas för fall där originalbilden kräver maximal återgivning.

**ClearScan:** Syntetiserar ett nytt Type 3-teckensnitt som är snarlikt originalteckensnittet och bevarar sidbakgrunden med hjälp av en lågupplöst kopia.

**Nedsampla bilder:** Minskar antalet pixlar i färgbilder, gråskalebilder och monokroma bilder när OCR är klart. Välj den nedsamplingsgrad som ska användas. Alternativ med högre nummer gör mindre nedsampling, vilket ger PDF med högre upplösning.

## Exportinställningar för Adobe PDF (endast Windows) {#adobe-pdf-export-settings-windows-only}

Inställningen Exportera filtyp i avsnittet Adobe PDF exportinställningar används för att konvertera en PDF-fil till ett annat format. Standardvärdet är HTML 4.01 med CSS (Cascading Style Sheets) 1.0(&amp;ast;.htm, &amp;ast;.html).

Instruktioner om hur du använder den här inställningen finns i [Skapa eller redigera filtypsinställningar](configuring-file-type-settings.md#create-or-edit-file-type-settings).

## HTML till PDF {#html-to-pdf-settings}

Följande alternativ avgör hur HTML-filer konverteras till PDF. Instruktioner om hur du använder dessa alternativ finns i [Skapa eller redigera filtypsinställningar](configuring-file-type-settings.md#create-or-edit-file-type-settings).

**Prova Fallback Converter:** PDF Generator kan använda Java™ eller Acrobat för att konvertera HTML till PDF. När det här alternativet är markerat och en konvertering misslyckas eller når den angivna tidsgränsen, försöker PDF Generator konverteringen med den alternativa metoden. Om den alternativa metoden misslyckas eller når den angivna tidsgränsen, skrivs ett undantag till loggfilen.

**Standardkodning:** Anger indatakodningen för filtexten från en meny med operativsystem och alfabet. Använder bara det som har valts och visas i alternativet Standardkodning om källfilen i HTML inte anger någon kodningstyp.

**Tvinga markerad kodning:** Ignorerar kodning som har angetts i källfilen för HTML och använder den som har valts och visas i alternativet Standardkodning.

### Spindelningsinställningar {#spidering-settings}

*Spindeling* skannar webbsidor efter länkar till andra webbsidor. När en länk till en annan webbsida påträffas hämtas målsidan och inkluderas i det PDF-dokument som genereras. Aktivera de här alternativen för att ange hur många nivåer som ska hämtas och konverteras till PDF:

**Hämta endast X-nivåer:** Spindlar och konverterar sidor upp till ett djup på den angivna nivån från bassidans URL. Värdet 1 konverterar bara den angivna URL:en.

**Hämta hela webbplatsen:** Konverterar hela platsen, med början från angiven URL.

**Stanna på samma sökväg:** Länkar som pekar på sidor som inte finns på samma relativa sökväg som bas-URL:en konverteras inte under spikning.

**Stanna på samma server:** Länkar som pekar på sidor på olika servrar konverteras inte under spikning. Endast länkar som pekar på samma server som den angivna URL:en konverteras.

### Inställningar för sidkonvertering {#page-conversion-settings}

Aktivera de här alternativen om du vill ange hur HTML-sidorna ska konverteras. Baserat på sidstorleken justeras bredd-, höjd- och marginalvärdena därefter.

**Sidstorlek:** Välj anpassad och ange bredd och höjd, eller välj fördefinierade mått.

**Orientering:** Markera antingen stående eller liggande för det konverterade PDF-dokumentet.

**Marginaler:** Anger marginalerna (Överkant, Underkant, Vänster och Höger) i det genererade PDF-dokumentet.

**Lägg till bokmärken i PDF:** Lägger till bokmärken i PDF-dokumentet.

**Aktivera PDF med taggar:** Bäddar in taggar i PDF-dokumentet.

**Ange inställningar för inledande vy:** Här kan du konfigurera dokumentalternativ, fönsteralternativ och alternativ för användargränssnitt. De här inställningarna bestämmer hur innehållet visas från början.

### Dokumentalternativ {#document-options}

Aktivera de här alternativen för att ange hur innehåll ska visas, hur sidor ska visas i PDF-dokumentet och hur förstoringsnivån ska anges:

**Visa:** Markera rutorna som ska öppnas i Acrobat när dokumentet PDF öppnas.

**Sidlayout:** Välj typ av sidlayout för PDF-dokumentet.

**Förstoring:** Välj förinställd förstoring för den inledande vyn i PDF eller välj ett anpassat värde. Om du väljer en standardinställning används standardförstoringen för Acrobat.

**Öppna på sidnummer:** Ange det sidnummer som PDF öppnas i.

### Fönsteralternativ {#window-options}

Aktivera de här alternativen för att ange hur fönstret ska storleksändras och visas.

**Ändra fönstrets storlek till startsidan:** Ändrar storlek på Acrobat-fönstret till den inledande sidans storlek.

**Centrera fönstret på skärmen:** Öppnar fönstret mitt på skärmen.

**Öppna i helskärmsläge:** Öppnar fönstret i helskärmsläge.

**Visa:** Visar dokumentets namn eller filnamn i fönstret.

### Alternativ för användargränssnitt {#user-interface-options}

Aktivera dessa alternativ för att ange fönstrets utseende:

**Dölj menyrad:** Döljer menyraden i dokumentet PDF.

**Dölj verktygsfält:** Döljer verktygsfälten i dokumentet PDF.

**Dölj fönsterkontroller:** Döljer fönsterkontrollerna i PDF-dokumentet.

## Flash videoklipp till PDF {#flash-videos-to-pdf-settings}

PDF Generator stöder möjligheten att skicka en video för Adobe Flash (SWF eller FLV) och skapa en PDF-fil med en inbäddad videofilm för Adobe Flash. Den här konverteringen kräver inte att Adobe Flash Player är installerad på Forms Server. Instruktioner om hur du använder det här alternativet finns i [Skapa eller redigera filtypsinställningar](configuring-file-type-settings.md#create-or-edit-file-type-settings).

**Filnamnstillägg:** Kommaavgränsad lista med filnamnstillägg som kan konverteras.

## Inställningar för XPS till PDF {#xps-to-pdf-settings}

XML Paper Specification (XPS) används i en Windows-utskriftsmaskin. Det här är ett Microsoft-format och kan skapas från alla Microsoft Office-program. AEM formulär ger möjlighet att konvertera XPS-filer PDF.

**Filnamnstillägg:** En kommaavgränsad lista över alla XPS-filnamnstillägg som kan konverteras. Det finns för närvarande ett format: .xps.

## Optimeringsinställningar för PDF {#pdf-optimizer-settings}

PDF Generator stöder möjligheten att minska storleken på PDF-filer. Om du använder alla dessa inställningar eller bara ett fåtal beror på hur du tänker använda filerna och på de viktigaste egenskaperna som en fil måste ha. I de flesta fall är standardinställningarna lämpliga för maximal effektivitet. Du sparar utrymme genom att ta bort inbäddade teckensnitt, komprimera bilder och ta bort objekt från filer som inte längre behövs.

>[!NOTE]
>
>När du optimerar ett digitalt signerat dokument tas de digitala signaturerna bort och blir ogiltiga.

Instruktioner om hur du använder den här inställningen finns i [Skapa eller redigera filtypsinställningar](configuring-file-type-settings.md#create-or-edit-file-type-settings).

**Målversion för PDF:** Anger den version av Acrobat som PDF är kompatibel med.

### Typsnitt {#fonts}

1. Välj **Typsnitt.**
1. Välj något av följande alternativ:

   **Ångra inkludering av alla teckensnitt:** Tar bort inbäddade teckensnitt.

   **Ångra inte inbäddning av teckensnitt:** Tar inte bort inbäddning av teckensnitt.

   **Ångra inbäddning av vissa teckensnitt:** Tar endast bort inbäddning av de angivna teckensnitten. Följ de här stegen för att ange de teckensnitt som du vill frigöra:

   * Om det behövs väljer du en annan teckensnittskatalog i **Teckensnittskälla** listruta. I den här listrutan visas teckensnittskataloger som anges i **Hem > Inställningar > Core System > Core Configurations**.
   * Markera ett eller flera teckensnitt i dialogrutan **Tillgängliga teckensnitt** lista och klicka på **Lägg till**. De här teckensnitten läggs till i **Teckensnitt att ångra inbäddning** lista.
   * Om du vill ta bort inbäddningen för vissa teckensnitt som inte finns på Forms Server anger du namnen på teckensnitten i **Lägg till teckensnitt för att frigöra inbäddning** box. Klicka **Lägg till**.

   >[!NOTE]
   >
   >*Om du vill ta bort inbäddningen för vissa teckensnitt vars deluppsättningar är inbäddade i dokumentet, ska du lägga till +-tecknet som prefix för teckensnittsnamnet. Till exempel &quot;+Helvetica&quot;.*

1. Om du bara vill bädda in deluppsättningarna av de inbäddade teckensnitten som är i bruk väljer du **Dela upp alla inbäddade teckensnitt**.

   >[!NOTE]
   >
   >*Om du använder det här alternativet i kombination med **Ångra inbäddning av vissa teckensnitt**, teckensnitt i **A**Om du lägger till teckensnitt i listan för att frigöra inbäddade teckensnitt tas de fortfarande bort helt.*

   >[!NOTE]
   >
   >*Delinställning av teckensnitt är en teknik som används för att bädda in en del av ett teckensnitt. En teckensnittsdeluppsättning innehåller bara de tecken som används i dokumentet.*

### Öppenhet {#transparency}

Om ditt PDF-dokument innehåller bilder som innehåller genomskinlighet kan du använda inställningarna för optimering av PDF för att förenkla genomskinlighet och minska filstorleken.

>[!NOTE]
>
>Om du väljer Acrobat 4.0 och senare som Target PDF-version förenklas alla genomskinliga objekt. För andra Target PDF-versioner stöds genomskinlighet och du kan konfigurera genomskinlighetsinställningarna.

Välj **Öppenhet** om du vill konfigurera genomskinlighetsinställningarna samtidigt som du optimerar PDF-dokument.

**Genomskinlighetsnivå** Anger mängden vektorinformation som ska bevaras. Högre inställningar bevarar fler vektorobjekt, medan lägre inställningar rastrerar fler vektorobjekt, medan mellanliggande inställningar bevarar enkla områden i vektorformat och rastrerar komplexa. Välj den lägsta inställningen om du vill rastrera hela teckningen.

>[!NOTE]
>
>Hur mycket rastrering som görs beror på sidans komplexitet och vilka typer av överlappande objekt som finns.

**Konturteckning och text** Upplösning som alla objekt, inklusive bilder, vektorgrafik, text och övertoningar, rastreras till. Värdena som stöds är 1 pixlar per tum (ppi) till 9 600 ppi.

>[!NOTE]
>
>Upplösningen för konturteckning och text bör i allmänhet anges till 600-1200 ppi för att ge rastrering av hög kvalitet, särskilt för serif-text och liten teckenstorlek.

**Övertoning och nät** Upplösning som övertoningar och nätövertoningar rastreras till. Värdena som stöds är 1 ppi till 1 200 ppi.

>[!NOTE]
>
>Övertonings- och nätupplösningen bör i allmänhet vara 150-300 ppi eftersom kvaliteten på övertoningar, skuggor och ludd inte förbättras med högre upplösningar, men utskriftstiden och filstorleken ökar.

**Konvertera all text till konturer** Konverterar alla textobjekt (punkttext, text i figur och bantyp) till konturer och tar bort all teckeninformation på sidor som innehåller genomskinlighet. Med det här alternativet ser du till att textbredden förblir konsekvent vid förenkling. Observera att om du aktiverar det här alternativet ser små teckensnitt något tjockare ut när de visas i Acrobat eller skrivs ut på skrivare med låg upplösning. Det påverkar inte kvaliteten på text som skrivs ut på högupplösta skrivare eller fotosättare.

**Konvertera alla linjer till konturer** Konverterar alla linjer till enkla fyllda banor på sidor som innehåller genomskinlighet. Med det här alternativet ser du till att linjebredden förblir konsekvent vid förenkling. Observera att om du aktiverar det här alternativet ser tunna linjer lite tjockare ut och förenklingsprestanda kan försämras.

**Beskär komplexa områden** Ser till att gränserna mellan vektorgrafik och rastrerad grafik hamnar längs objektbanor. Med det här alternativet minskas sammanfogningsartefakter som uppstår när en del av en logg

<!--
NOTE to WRITER: Unfinished sentence above.
-->

>[!NOTE]
>
>Vissa skrivardrivrutiner bearbetar raster- och vektorbilder på olika sätt, vilket ibland leder till färgojämnheter. Du kan eventuellt minimera problem med färghantering genom att inaktivera vissa inställningar för färghantering som är specifika för skrivardrivrutinen. De här inställningarna varierar beroende på vilken skrivare som används, så mer information finns i dokumentationen som medföljde skrivaren.

Bevara övertryck: Blandar färgen i den genomskinliga teckningen med bakgrundsfärgen för att skapa en övertryckningseffekt.

I följande tabell visas vanliga typer av skrivare och deras upplösning mätt i dpi, deras standardrastertäthet mätt i linjer per tum (lpi) och en omsamplingsupplösning för bilder mätt i pixlar per tum (ppi). Om du till exempel skriver ut på en laserskrivare med 600 dpi anger du 170 som upplösning för omsampling av bilder.

**Bilder** Välj Bilder om du vill ange komprimerings- och omsamplingsalternativ för färgbilder, gråskalebilder och monokroma bilder. Du kan experimentera med dessa alternativ för att hitta en lämplig balans mellan filstorlek och bildkvalitet. Upplösningen för färg- och gråskalebilder bör vara 1,5 till 2 gånger rastertätheten som filen skrivs ut med. Upplösningen för monokroma bilder bör vara densamma som för utdataenheten, men om du sparar en monokrom bild med en upplösning på över 1 500 dpi ökar filstorleken utan att bildkvaliteten förbättras nämnvärt. Bilder som ska förstoras, t.ex. kartor, kan kräva högre upplösningar.

>[!NOTE]
>
>Omsampling av monokroma bilder kan ge oväntade visningsresultat, till exempel att ingen bild visas. Om det inträffar stänger du av omsampling och konverterar filen igen. Det här problemet inträffar oftast vid delsampling och är minst sannolikt vid bikubisk nedsampling.

<table>
 <tbody>
  <tr>
   <th><p><strong>Skrivarupplösning</strong></p> </th>
   <th><p><strong>Standardlinjeraster</strong></p> </th>
   <th><p><strong>Bildupplösning</strong></p> </th>
  </tr>
  <tr>
   <td><p>300 dpi (laserskrivare)</p> </td>
   <td><p>60 lpi</p> </td>
   <td><p>120 ppi</p> </td>
  </tr>
  <tr>
   <td><p>600 dpi (laserskrivare)</p> </td>
   <td><p>85 lpi</p> </td>
   <td><p>170 ppi</p> </td>
  </tr>
  <tr>
   <td><p>1 200 dpi (fotosättare)</p> </td>
   <td><p>120 lpi</p> </td>
   <td><p>240 ppi</p> </td>
  </tr>
  <tr>
   <td><p>2 400 dpi (fotosättare)</p> </td>
   <td><p>150 lpi</p> </td>
   <td><p>300 ppi</p> </td>
  </tr>
 </tbody>
</table>

#### Ignorera objekt {#discard-objects}

* Välj **Ignorera objekt** för att ange objekt som ska tas bort från PDF och för att optimera kurvformade linjer i CAD-ritningar.
* **Ignorera formulärskickning, import- och återställningsåtgärder**: Inaktiverar alla åtgärder som är relaterade till att skicka eller importera formulärdata, och återställer formulärfält. Det här alternativet behåller formulärobjekt som åtgärder är länkade till.
* **Ignorera alla JavaScript-åtgärder**: Tar bort alla åtgärder som använder JavaScript från PDF.
* **Ignorera inbäddade sidminiatyrer**: Tar bort inbäddade sidminiatyrer. Det här alternativet är användbart för stora dokument, som kan ta lång tid att rita sidminiatyrer när du har klickat på sidknappen.
* **Konvertera jämna linjer till kurvor**: Minskar antalet kontrollpunkter som används för att skapa kurvor i CAD-ritningar, vilket ger mindre PDF-filer och snabbare skärmåtergivning.
* **Ignorera inbäddade utskriftsinställningar**: Tar bort inbäddade utskriftsinställningar, t.ex. sidskalning och duplexläge, från dokumentet.
* **Ignorera bokmärken**: Tar bort alla bokmärken från dokumentet.
* **Förenkla formulärfält**: Gör formulärfält oanvändbara utan att deras utseende ändras. Formulärdata sammanfogas med sidan för att bli sidinnehåll.
* **Ignorera alla alternativa bilder**: Tar bort alla versioner av en bild utom den version som ska visas på skärmen. I vissa PDF finns flera versioner av samma bild för olika syften, till exempel för skärmvisning med låg upplösning och högupplösta utskrifter.
* **Ignorera dokumenttaggar**: Tar bort taggar från dokumentet, vilket även tar bort textens tillgänglighet och flödesomformningsfunktioner.
* **Identifiera och sammanfoga bildfragment**: Söker efter bilder eller masker som är fragmenterade i tunna segment och försöker sammanfoga segmenten till en enda bild eller mask.
* **Ignorera inbäddat sökindex**: Tar bort inbäddade sökindex, vilket minskar filstorleken.

#### Ignorera användardata {#discard-user-data}

Välj **Ignorera användardata** för att ta bort all personlig information som du inte vill distribuera eller dela med andra användare.

* **Ignorera alla kommentarer, Forms och multimedia**: Tar bort alla kommentarer, formulär, formulärfält och multimedia från PDF.
* **Ignorera alla objektdata**: Tar bort alla objekt från PDF.
* **Ignorera externa korsreferenser**: Tar bort länkar till andra dokument. Länkar som hoppar till andra platser i PDF tas inte bort.
* **Ignorera dolt lagerinnehåll och förenkla synliga lager**: Minskar filstorleken. Det optimerade dokumentet ser ut som PDF men innehåller ingen lagerinformation.
* **Ignorera dokumentinformation och metadata**: Tar bort information i dokumentinformationsordlistan och alla metadataströmmar. (Använd kommandot Spara som för att återställa metadataströmmar till en kopia av PDF.)
* **Ignorera bifogade filer**: Tar bort alla bifogade filer, inklusive bilagor som lagts till i PDF som kommentarer. (Bifogade filer optimeras inte i PDF Optimizer.)
* **Ignorera privata data från andra program**: Tar bort information från ett PDF-dokument som bara är användbar i det program som dokumentet skapades i. Den här inställningen påverkar inte PDF, men den minskar filstorleken.

### Rensa {#clean-up}

Välj **Rensa** om du vill ta bort onödiga objekt från dokumentet.
Dessa objekt innehåller element som är föråldrade eller inte behövs för den avsedda användningen av dokumentet. Om du tar bort vissa element kan det allvarligt påverka PDF funktion. Som standard markeras bara element som inte påverkar funktionen. Om du är osäker på vad borttagningen av andra alternativ innebär kan du använda standardmarkeringarna.

**Komprimering**

Välj något av följande alternativ för Flate-komprimering i listrutan:

* Komprimera hela filen
* Komprimera dokumentstruktur
* Ta bort komprimering
* Låt komprimeringen vara oförändrad

**Använd Flate för att koda strömmar som inte är kodade**: Flate-komprimering används för alla strömmar som inte är kodade.

**Ignorera ogiltiga bokmärken**: Tar bort bokmärken som pekar på sidor i dokumentet som tas bort.

**Ignorera namngivna destinationer utan referenser**: Tar bort namngivna mål som inte refereras internt från PDF-dokumentet. Det här alternativet söker inte efter länkar från andra PDF-filer eller webbplatser.

**Optimera PDF för snabb webbvisning**: Omstrukturerar ett PDF-dokument för sidvis hämtning (byte-hämtning) från webbservrar.

**Använd Flate i strömmar som använder LZW-kodning**: Flate-komprimering används för alla innehållsströmmar och bilder som använder LZW-kodning.

**Ignorera ogiltiga länkar**: Tar bort länkar som hoppar till ogiltiga mål.

**Optimera sidinnehåll**: Konverterar alla radslutstecken till blankstegstecken, vilket förbättrar Flate-komprimeringen.

## Microsoft Excel-inställningar (endast Windows) {#microsoft-excel-settings-windows-only}

Dessa alternativ avgör hur Microsoft Excel-filer konverteras. Instruktioner om hur du använder dessa alternativ finns i [Skapa eller redigera filtypsinställningar](#create-or-edit-file-type-settings).

**Prova OpenOffice som reservalverare**: När det här alternativet är markerat och en konvertering med Microsoft Excel misslyckas eller når den angivna tidsgränsen, försöker PDF Generator konverteringen med OpenOffice. Om konverteringen med OpenOffice misslyckas eller når den angivna tidsgränsen, skrivs ett undantag till loggfilen.

**Filnamnstillägg**: Anger filnamnstilläggen för filtyper, avgränsade med kommatecken, som kan användas i det här programmet. Standardvärdet är `xls,xlsx`. Ta inte med en punkt före eller ett blanksteg mellan tilläggen.

**Skapa PDF/A-1a-kompatibel fil**: Tvingar användning av inställningen PDF/A-1b:2005 RGB Adobe PDF.

**Lägg till bokmärken i Adobe PDF**: Konverterar Excel-kalkylbladsnamn till bokmärken. Det här alternativet är markerat som standard.

**Anpassa kalkylblad till en sida**: Minskar textstorleken så att den passar kalkylbladet på en sida.

**Konvertera hela arbetsboken**: Konverterar alla kalkylblad i Excel-filen. Om det här alternativet inte är markerat konverteras bara den aktuella sidan.

**Kör makron automatiskt**: Kör eventuella makron i Excel-dokumentet (t.ex. ett makro som infogar den aktuella tiden) innan dokumentet konverteras.

**Konvertera dokumentinformation**: Lägger till dokumentegenskaper i PDF baserat på dokumentinformationen i källfilen. Detta inkluderar information som dokumenttitel, författare, ämne och nyckelord.

**Lägg till länkar i Adobe PDF**: Konverterar hyperlänkar i källfilen till hyperlänkar i PDF-dokumentet.

**Bifoga källfil till Adobe PDF**: När det här alternativet är markerat infogas det ursprungliga Excel-kalkylbladet som en bifogad fil i det genererade PDF-dokumentet.

**Aktivera tillgänglighet och Reflow med taggad Adobe PDF**: Bäddar in taggar i PDF-dokumentet för att aktivera tillgänglighet och flödesomformning.

**Lista över Excel-tillägg som ska läsas in**: Som standard (av säkerhetsskäl) körs inga Excel-tillägg när en Excel-fil konverteras till PDF. Om du vill tillåta vissa Excel-tillägg att köras under konverteringen anger du en kommaavgränsad lista med tilläggens namn.

**Lista över kalkylblad som ska konverteras**: När den här rutan är tom inkluderas alla kalkylblad i Excel-kalkylbladet i det genererade PDF. Om du vill konvertera en delmängd av kalkylbladet selektivt anger du en kommaavgränsad lista med kalkylbladsnamn.

## Microsoft PowerPoint-inställningar (endast Windows) {#microsoft-powerpoint-settings-windows-only}

Dessa alternativ avgör hur Microsoft PowerPoint-filer konverteras. Instruktioner om hur du använder dessa alternativ finns i [Skapa eller redigera filtypsinställningar](/help/forms/using/admin-help/configuring-file-type-settings1.md#create-or-edit-file-type-settings).

**[!UICONTROL Try OpenOffice As Fallback Converter]**: När det här alternativet är markerat och en konvertering med Microsoft PowerPoint misslyckas eller når den angivna tidsgränsen, försöker PDF Generator konverteringen med OpenOffice. Om konverteringen med OpenOffice misslyckas eller når den angivna tidsgränsen, skrivs ett undantag till loggfilen.

**[!UICONTROL Filename Extensions]**: Anger filnamnstilläggen för filtyper, avgränsade med kommatecken, som kan användas i det här programmet. Standardvärdet är ppt,pptx. Ta inte med en punkt före eller ett blanksteg mellan tilläggen.

**[!UICONTROL Convert Document Information]**: Lägger till dokumentinformation från egenskapsdialogrutan för källfilen, inklusive titel, ämne, författare, nyckelord, hanterare, företag, kategori och kommentarer. Det här alternativet är markerat som standard.

**[!UICONTROL Add Bookmarks To Adobe PDF]**: Konverterar PowerPoint-titlar till bokmärken. Det här alternativet är markerat som standard.

**[!UICONTROL Attach Source File To Adobe PDF]**: Lägger till källfilen i PDF-filen som en bifogad fil. Det här alternativet är som standard avmarkerat.

**[!UICONTROL Enable Accessibility And Reflow With Tagged Adobe PDF]**: Bäddar in taggar i filen PDF. Det här alternativet är som standard avmarkerat.

**[!UICONTROL Convert Multimedia To PDF Multimedia]**: Konverterar multimedia till PDF-multimedia, där det är möjligt. Det här alternativet är markerat som standard.

**[!UICONTROL Convert Speaker Notes]**: Konverterar stödanteckningar till PDF.

**[!UICONTROL Run Macros Automatically]**: Kör eventuella makron i PowerPoint-dokumentet (t.ex. ett makro som infogar den aktuella tiden) innan dokumentet konverteras.

**[!UICONTROL PDF Layout Based On PowerPoint Printer Settings]**: Använder PowerPoint-skrivarinställningar för att utforma PDF-dokumentet.

**[!UICONTROL Add Links To Adobe PDF]**: Bevarar befintliga länkar när filen konverteras. Länkarnas utseende ändras i allmänhet inte. Länkar kan bara skapas om alternativet Aktivera hjälpmedel också är markerat. Det här alternativet är som standard avmarkerat.

**[!UICONTROL Save Slide Transitions In Adobe PDF]**: Konverterar bildövergångar. Det här alternativet är markerat som standard.

**[!UICONTROL Save Animations In Adobe PDF]**: Sparar konverterade animeringar i filen PDF.

**[!UICONTROL Convert Hidden Slides To PDF Pages]**: Konverterar dolda bilder.

**[!UICONTROL Create PDF/A-1a Compliant File]**: Tvingar användning av inställningen PDF/A-1b:2005 RGB Adobe PDF. Vissa PowerPoint-funktioner konverteras inte när du skapar en PDF-fil. Om en PowerPoint-övergång inte har en motsvarande övergång i Acrobat ersätts en liknande övergång. Om det finns flera animeringseffekter i samma bildruta används en effekt. Sidövergångar och insticksprogram för punkter konverteras.

## Microsoft Project-inställningar (endast Windows) {#microsoft-project-settings-windows-only}

De här alternativen avgör hur Microsoft Project-filer konverteras. Instruktioner om hur du använder dessa alternativ finns i [Skapa eller redigera filtypsinställningar](#create-or-edit-file-type-settings).

1. **[!UICONTROL Filename Extensions:]** Anger filnamnstilläggen för filtyper, avgränsade med kommatecken, som accepteras för det här programmet. Standardvärdet är `mpp`. Ta inte med en punkt före eller ett blanksteg mellan tilläggen.

1. **[!UICONTROL Convert Document Information]**: Lägger till dokumentinformation från egenskapsdialogrutan för källfilen, inklusive titel, ämne, författare, nyckelord, hanterare, företag, kategori och kommentarer. Det här alternativet är markerat som standard.
1. **[!UICONTROL Attach Source File To Adobe PDF]**: Lägger till källfilen i PDF-filen som en bifogad fil.
1. **[!UICONTROL Create PDF/A-1a Compliant File]**: Tvingar användning av inställningen PDF/A-1b:2005 RGB Adobe PDF.
1. **[!UICONTROL Run Macros Automatically]**: Kör eventuella makron i Microsoft Project-dokumentet (t.ex. ett makro som infogar den aktuella tiden) innan du konverterar dokumentet.

## Inställningar för Microsoft Word (endast Windows) {#microsoft-word-settings-windows-only}

De här alternativen avgör hur Microsoft Word-filer konverteras. Instruktioner om hur du använder dessa alternativ finns i [Skapa eller redigera filtypsinställningar](#create-or-edit-file-type-settings).

**[!UICONTROL Try OpenOffice As Fallback Converter]**: När det här alternativet är markerat och en konvertering med Microsoft Word misslyckas eller når den angivna tidsgränsen, försöker PDF Generator konverteringen med OpenOffice. Om konverteringen med OpenOffice misslyckas eller når den angivna tidsgränsen, skrivs ett undantag till loggfilen.

**[!UICONTROL Filename Extensions]**: Anger filnamnstilläggen för filtyper, avgränsade med kommatecken, som kan användas i det här programmet. Standardvärdet är `doc,docx,rtf,txt`. Ta inte med en punkt före eller ett blanksteg mellan tilläggen.

**[!UICONTROL Convert Document Information]**: Lägger till dokumentinformation från egenskapsdialogrutan för källfilen, inklusive titel, ämne, författare, nyckelord, hanterare, företag, kategori och kommentarer. Det här alternativet är markerat som standard.

**[!UICONTROL Add Bookmarks To Adobe PDF]**: Konverterar rubriker till bokmärken. Det här alternativet är markerat som standard.

**[!UICONTROL Attach Source File To Adobe PDF]**: Lägger till källfilen i PDF-filen som en bifogad fil.

**[!UICONTROL Convert Cross-References And Table Of Contents To Links]**: Konverterar alla korsreferenser och innehållsförteckningsposter till länkar. Det här alternativet är markerat som standard.

**[!UICONTROL Enable Accessibility And Reflow With Tagged Adobe PDF]**: Bäddar in taggar i filen PDF. Det här alternativet är markerat som standard.

**[!UICONTROL Create PDF/A-1a Compliant File]**: Om du väljer det här alternativet används inställningen PDF/A-1b:2005 RGB Adobe PDF.

**[!UICONTROL Run Macros Automatically]**: Kör alla makron i Word-dokumentet (t.ex. ett makro som infogar den aktuella tiden) innan du konverterar dokumentet.

**[!UICONTROL Preserve Document Markup In Adobe PDF]**: Konverterar markeringar i Word-dokumentet till anteckningar i filen PDF.

**[!UICONTROL Add Links To Adobe PDF]**: Konverterar hyperlänkar i källfilen till hyperlänkar i PDF-dokumentet.

**[!UICONTROL Convert Footnote And Endnote Links]**: Skapar länkar från fotnots- och slutkommentarscitat till anteckningar i PDF-dokumentet.

**[!UICONTROL Convert Displayed Comments To Notes in Adobe PDF]**: Konverterar kommentarer i Word-dokumentet till textanteckningar i PDF-dokumentet.

**[!UICONTROL Enable Advanced Tagging]**: Lägger till avancerade taggar för förbättrad tillgänglighet.

**[!UICONTROL Convert All Styles To Bookmarks]**: Konverterar alla format i Word-dokumentet till bokmärken i PDF-dokumentet.

**[!UICONTROL Styles With Levels]**: Anger vilka format i Word-dokumentet som ska konverteras till bokmärken i PDF-dokumentet. Anger också nivån på bokmärkena. Avmarkera **[!UICONTROL Convert All Styles To Bookmarks]** och ange formatnamnen i följande format:

styleName1=level1[,styleName2=level2...]

Om ett Microsoft Word-formatnamn innehåller ett komma (,) eller likhetstecken (=), skriver du ett escape-tecken (&quot;\_) före specialtecknen. Ange till exempel ett format med namnet &quot;Rubrik, 1&quot; som Rubrik\, 1.

## Inställningar för Microsoft Visio (endast Windows) {#visio}

**Konvertera dokumentinformation**: Lägger till dokumentinformation från egenskapsdialogrutan för källfilen, inklusive titel, ämne, författare, nyckelord, hanterare, företag, kategori och kommentarer. Det här alternativet är markerat som standard. Det här alternativet är aktiverat som standard.

**Lägg till länkar i Adobe PDF**: Alla länkar bevaras. Det här alternativet är markerat som standard.

**Lägg till bokmärken i Adobe PDF**: Konverterar rubriker till bokmärken. Det här alternativet är markerat som standard.

**Bifoga källfil till Adobe PDF**: Lägger till källfilen i PDF-filen som en bifogad fil.

**Lägg alltid samman lager i Adobe PDF**: Förenklar alla Visio-lager.

**Konvertera alla sidor**: Konverterar alla sidor i Visio-filen.

**Öppna lagerpanelen när den visas i Adobe Acrobat**: Om Visio-lagren inte förenklas öppnas ett fönster där du kan ange vilka lager som ska bevaras i filen PDF när de öppnas i Acrobat. Det här alternativet är markerat som standard.

**Skapa en PDF/A-1b-kompatibel fil**: Tvingar användning av Adobe PDF-inställningen PDF/A-1b:2005 (RGB).

**Konvertera kommentarer till Adobe PDF-kommentarer**: Konverterar Visio-anteckningar till PDF-kommentarer.

## Inställningar för Microsoft Publisher (endast Windows) {#microsoft-publisher-settings-windows-only}

Dessa alternativ avgör hur Microsoft Publisher-filer konverteras. Instruktioner om hur du använder dessa alternativ finns i [Skapa eller redigera filtypsinställningar](#create-or-edit-file-type-settings).

**[!UICONTROL Filename Extensions]**: Anger filnamnstilläggen för filtyper, avgränsade med kommatecken, som kan användas i det här programmet. Standardvärdet är `pub`. Ta inte med en punkt före eller ett blanksteg mellan tilläggen.

## AutoCAD-inställningar (endast Windows) {#autocad-settings-windows-only}

Dessa alternativ avgör hur AutoCAD-filer konverteras. Instruktioner om hur du använder dessa alternativ finns i [Skapa eller redigera filtypsinställningar](/help/forms/using/admin-help/configuring-file-type-settings1.md#create-or-edit-file-type-settings).

**[!UICONTROL Filename Extensions]**: Anger filnamnstilläggen för filtyper, avgränsade med kommatecken, som kan användas i det här programmet. Standardvärdet är `dwg`. Ta inte med en punkt före eller ett blanksteg mellan tilläggen.

**[!UICONTROL Convert Document Information]**: Lägger till dokumentinformation från egenskapsdialogrutan för källfilen, inklusive titel, ämne, författare, nyckelord, hanterare, företag, kategori och kommentarer. Det här alternativet är markerat som standard.

**[!UICONTROL Add Bookmarks To Adobe PDF]**: Konverterar rubriker till bokmärken.

**[!UICONTROL Always Flatten Layers In Adobe PDF]**: Förenklar alla AutoCAD-lager.

**[!UICONTROL Open Layers Pane When Viewed In Adobe Acrobat]**: Visar lagerstrukturen när PDF öppnas i Acrobat.

**[!UICONTROL Create PDF/E-1 Compliant File]**: Skapar en fil som är PDF/E-1-kompatibel. PDF/E är en ISO-standard för utbyte av tekniska och tekniska dokument. Mer information om PDF/E-1 finns i [Adobe och branschstandarder](https://www.adobe.com/enterprise/standards/index.html).

**[!UICONTROL Convert All Layouts]**: Inkluderar alla layouter i PDF.

**[!UICONTROL Convert Model Space to 3D]**: När det här alternativet är markerat konverteras modellområdeslayouten till en 3D-anteckning i PDF.

**[!UICONTROL Add Links To Adobe PDF]**: Om det här alternativet är markerat bevaras alla länkar.

**[!UICONTROL Attach Source File To Adobe PDF]**: Lägger till källfilen i PDF-filen som en bifogad fil.

**[!UICONTROL Create PDF/A-1b Compliant File]**: Tvingar användning av Adobe PDF-inställningen PDF/A-1b.

**[!UICONTROL Convert All Layers]**: Som standard konverterar PDF Generator bara standardlagret med AutoCAD-filer till PDF i stället för alla lager i filen. Välj det här alternativet om du vill konvertera alla lager i filen.

**[!UICONTROL Embed Scale Information]**: Bevarar information om ritskalan.

**[!UICONTROL Convert Current Layout]**: Inkluderar endast den aktuella layouten i PDF.

**[!UICONTROL List Of AutoCAD Layouts To Convert]**: En AutoCAD-ritning kan ha flera layouter. När den här rutan är tom inkluderas alla layouter i AutoCAD-ritningen i det genererade PDF-dokumentet. Om du vill konvertera en delmängd av layouterna selektivt anger du en kommaavgränsad lista med layoutnamn.

## OpenOffice-inställningar {#openoffice-settings}

De här alternativen avgör hur OpenOffice-filer konverteras. Instruktioner om hur du använder dessa alternativ finns i [Skapa eller redigera filtypsinställningar](/help/forms/using/admin-help/configuring-file-type-settings1.md#create-or-edit-file-type-settings).

**Prova PDFMaker som återställningskonverterare**: När det här alternativet är markerat och en konvertering med OpenOffice misslyckas eller når den angivna tidsgränsen, försöker PDF Generator konverteringen med PDFMaker. Om konverteringen med PDFMaker misslyckas eller når den angivna tidsgränsen, skrivs ett undantag till loggfilen.

**Filnamnstillägg**: Ange filnamnstilläggen för de filtyper, avgränsade med kommatecken, som kan användas i det här programmet. Standardvärdet är `odt,odp,ods,odg,odf,sxw,sxi,sxd`. Ta inte med en punkt före eller ett blanksteg mellan tilläggen.

**Intervall**: Konvertera alla sidor eller ange vissa sidor eller ett sidintervall. Om inget sidintervall är definierat konverteras alla sidor. Om du vill exportera ett sidintervall använder du formatet 3-6. Om du vill exportera enstaka sidor använder du formatet 7;9;11. Du kan exportera en kombination av sidintervall och enstaka sidor med ett format som 3-6;8;10;12.

**Sidorientering**: För oformaterade textfiler väljer du antingen stående eller liggande för det konverterade PDF-dokumentet.

**Bilder**: Konfigurera hur bilder konverteras. EPS-bilder med inbäddade förhandsvisningar exporteras endast som förhandsvisningar. EPS-bilder utan inbäddade förhandsvisningar exporteras som tomma platshållare. Med förlustfri komprimering av bilder bevaras alla pixlar. Med JPEG-komprimering och en hög kvalitetsnivå bevaras nästan alla pixlar. Med en låg kvalitetsnivå försvinner vissa pixlar och artefakter uppstår, men filstorleken minskar.

**Allmänt**: Aktivera alternativen för att konvertera ett PDF med märkord eller för att exportera noteringar till Writer- och FormCalc-dokument, Impress-bildruteövergångseffekter eller tomma sidor till PDF. När du exporterar märkord kan filstorleken öka med mycket. Vissa märkord som exporteras är innehållsförteckningar, hyperlänkar och kontroller.

Du kan också ange hur formulär ska skickas. Alternativen är XML, FDF, PDF eller HTML. Den här inställningen åsidosätter kontrollens URL-egenskap som du anger i dokumentet. Endast en gemensam inställning kan väljas för dokumentet PDF:

* PDF (skickar hela dokumentet)
* FDF (skickar kontrollinnehållet)
* HTML
* XML

**Tagged PDF**: Gör att du kan skapa taggade PDF från OpenOffice-dokument. PDF med märkord innehåller information om dokumentinnehållets struktur. Detta kan vara till hjälp när du visar dokumentet på enheter med olika skärmar och när du använder skärmläsarprogram. Det hjälper även hjälpmedelsprogrammet att utföra olika användbara åtgärder med PDF-dokumentet, som att läsa upp innehållet i PDF-dokumentet.

**Exportera anteckningar**: Konverterar anteckningarna i OpenOffice-dokument till anteckningar i det genererade PDF-dokumentet.

**Använd övergångseffekter**: Konverterar bildruteövergångseffekterna i OpenOffice-presentationer till motsvarande PDF-övergångseffekter.

**Skicka in Forms i format**: Skapar ett PDF-formulär som kan fyllas i och skrivas ut av användaren av PDF-dokumentet.

**Exportera automatiskt infogade tomma sidor**: När det här alternativet är markerat inkluderas automatiskt tomma sidor i det genererade PDF-dokumentet. Det här är användbart om du skriver ut ett dubbelsidigt PDF-dokument. En bok kan till exempel konfigureras så att den första sidan i kapitlet alltid börjar på en sida med udda nummer. Om det föregående kapitlet slutar på en sida med ojämnt nummer infogar OpenOffice en tom sida med jämnt nummer. Med det här alternativet anger du om den jämna sidan ska inkluderas i den genererade PDF.

## Andra programinställningar (endast Windows) {#other-applications-settings-windows-only}

Du kan inte ändra inställningarna för andra program via administrationskonsolen, utan de visar filnamnstilläggen för de filtyper som stöds. Instruktioner om hur du använder dessa inställningar finns i [Skapa eller redigera filtypsinställningar](https://help.adobe.com/en_US/AEMForms/6.1/AdminHelp/WS92d06802c76abadb-5145d5d12905ce07e7-7e42.2.html).

* Corel WordPerfect: `wpd`
* PageMakerna Adobe: `pmd, pm6, p65, pm`
* Adobe FrameMaker: `fm`
* Adobe Photoshop: `psd`

Stöd för dessa filtyper kan behöva anpassas. Mer information finns i &quot;Adding Support for Additional Native File Formats&quot; i [Programmera med AEM](https://www.adobe.com/go/learn_aemforms_programming_62).

Hjälp om hur du konfigurerar en PDFG-nätverksskrivare finns i [Konfigurera en PDFG-nätverksskrivare (endast Windows)](/help/forms/using/admin-help/setting-pdfg-network-printer-windows.md).
