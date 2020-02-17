---
title: Konfigurerar filtypsinställningar
seo-title: Konfigurerar filtypsinställningar
description: Lär dig hur du konfigurerar filtypsinställningar.
seo-description: Lär dig hur du konfigurerar filtypsinställningar.
uuid: 58a05500-ffbb-4fa2-8ae1-8ac80ab2d099
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_pdf_generator
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 89f4d3cf-eb2e-4d55-8209-16ecbba03792
translation-type: tm+mt
source-git-commit: 01c93d2ef344b1ce36fddd21b634b8fa4e7aebe0

---


# Konfigurerar filtypsinställningar {#configuring-file-type-settings}

I PDF Generator kan du ange programinställningar för filtyper som stöds. I Windows kan du ange programinställningar för varje filtyp som stöds. På UNIX och Linux kan du ange programinställningar för HTML-till-PDF och OpenOffice.

På sidan Filtypsinställningar kan du utföra följande uppgifter:

* [Skapa eller redigera en filtypsinställning](/help/forms/using/admin-help/configuring-file-type-settings1.md#main-pars-heading-0)
* Ange vilka filtypsinställningar som ska användas som standard (se [Importera och exportera PDF Generator-konfigurationsfiler](https://helpx.adobe.com/aem-forms/6-2/admin-help/importing-exporting-pdf-generator-configuration.html))
* [Ändra standardinställningarna](/help/forms/using/admin-help/configuring-file-type-settings1.md#change-the-default-settings)
* [Aktivera stöd för PDF/A](https://helpx.adobe.com/aem-forms/6-2/admin-help/enable-pdf-a-support.html)
* [Ta bort en filtypsinställning](https://helpx.adobe.com/aem-forms/6-2/admin-help/enable-pdf-a-support.html)

>[!NOTE]
>
>Filtypsinställningarna är inte tillgängliga för reservkonverterare som Acrobat för HTML till PDF-konvertering, Microsoft PowerPoint, Microsoft Word och Microsoft Excel.

## Skapa eller redigera filtypsinställningar {#create-or-edit-file-type-settings}

Skapa eller redigera en filtypsinställning för att ange hur konverteringen av filtyper som stöds ska hanteras i programmet. I Windows kan du ange programinställningar för varje filtyp som stöds. På UNIX och Linux kan du ange programinställningar för HTML-till-PDF och OpenOffice.

1. I administrationskonsolen klickar du på **[!UICONTROL Tjänster]** > **[!UICONTROL PDF Generator]** > **[!UICONTROL Filtypsinställningar]**.
1. Klicka på Ny eller klicka på namnet på en inställning.
1. I rutan Filnamnstillägg skriver du filnamnstilläggen, avgränsade med kommatecken, för filtyper som stöds för det här programmet. Ta inte med punkten före eller ett mellanrum mellan tilläggen. The default is `bmp,gif,jpeg,jpg,tif,tiff,png`.
1. (Valfritt) Om du vill använda optisk kodigenkänning (OCR) av text i bilder eller bilder markerar du Använd OCR och anger följande alternativ:

**** Primärt OCRLanguage: Det språk som OCR-motorn ska använda för att identifiera tecknen. Standardvärdet är engelska (USA).

**** PDF-utdatastil: Välj Sökbar bild om du vill att en bitmappsbild av sidorna i förgrunden och den skannade texten ska visas på ett osynligt lager under. Utseendet på sidan ändras inte, men texten kan markeras och läsas. Markera Formaterad text och grafik om du vill rekonstruera originalsidan med hjälp av identifierad text, teckensnitt, bilder och andra grafiska element. Standardinställningen är Sökbar bild (exakt).

**** Nedsampla bilder: Minskar antalet pixlar i färgbilder, gråskalebilder och monokroma bilder. Nedsampling av skannade bilder utförs när OCR har slutförts. Standardvärdet är Lägsta (600 dpi). Det här alternativet är inte tillgängligt om du anger PDF-utdataformatet till Sökbar bild (exakt).

1. Fyll i nödvändig information i dessa avsnitt:

   [Importera och exportera PDF Generator-konfigurationsfiler](https://helpx.adobe.com/aem-forms/6-2/admin-help/importing-exporting-pdf-generator-configuration.html)

   [Exportinställningar för Adobe PDF (endast Windows)](/help/forms/using/admin-help/configuring-file-type-settings1.md#main-pars-heading-2)

   [Inställningar för HTML-till-PDF](/help/forms/using/admin-help/configuring-file-type-settings1.md#main-pars-heading-3)

   [Inställningar för Flash-videor till PDF](/help/forms/using/admin-help/configuring-file-type-settings1.md#main-pars-heading-9)

   [Inställningar för XPS till PDF](/help/forms/using/admin-help/configuring-file-type-settings1.md#main-pars-heading-10)

   [Inställningar för PDF-optimering](/help/forms/using/admin-help/configuring-file-type-settings1.md#main-pars-heading-11)

   [Inställningar för Microsoft Excel (endast Windows)](/help/forms/using/admin-help/configuring-file-type-settings1.md#microsoft-excel-settings-windows-only)

   [Inställningar för Microsoft PowerPoint (endast Windows)](/help/forms/using/admin-help/configuring-file-type-settings1.md#microsoft-powerpoint-settings-windows-only)

   [Inställningar för Microsoft Project (endast Windows)](/help/forms/using/admin-help/configuring-file-type-settings1.md#microsoft-project-settings-windows-only)

   [Inställningar för Microsoft Word (endast Windows)](/help/forms/using/admin-help/configuring-file-type-settings1.md#microsoft-word-settings-windows-only)

   [Inställningar för Microsoft Visio (endast Windows)](/help/forms/using/admin-help/configuring-file-type-settings1.md#main-pars-header-1354428557)

   [Inställningar för Microsoft Publisher (endast Windows)](/help/forms/using/admin-help/configuring-file-type-settings1.md#microsoft-publisher-settings-windows-only)

   [AutoCAD-inställningar (endast Windows)](/help/forms/using/admin-help/configuring-file-type-settings1.md#autocad-settings-windows-only)

   [OpenOffice-inställningar](/help/forms/using/admin-help/configuring-file-type-settings1.md#openoffice-settings)

   [Inställningar för andra program (endast Windows)](#other-applications-settings-windows-only)

   Om du vill gå till ett annat avsnitt klickar du på länken på webbsidan eller använder knapparna **[!UICONTROL Nästa]**eller **[!UICONTROL Föregående]** .

1. När du är klar med alla avsnitt klickar du på **[!UICONTROL Spara]** eller **[!UICONTROL Spara som]** och anger ett namn för inställningen.

Stöd för olika filtyper kan anpassas. (Se&quot; [Lägga till stöd för fler inbyggda filformat](https://help.adobe.com/en_US/AEMForms/6.1/ProgramLC/WS624e3cba99b79e12e69a9941333732bac8-7756.2.html)&quot; i [Programmering med AEM-formulär](https://www.adobe.com/go/learn_lc_programming_11).)

## Ändra standardinställningarna {#change-the-default-settings}

Du kan ändra standardvärdet för de Adobe PDF-inställningar, skyddsinställningar och filtypsinställningar som gäller för nya källor. Om du ändrar standardinställningarna påverkas inte inställningarna för befintliga källor.

1. I administrationskonsolen klickar du på **[!UICONTROL Tjänster > PDF Generator]**.
1. På sidan **[!UICONTROL Adobe PDF-inställningar]**, **[!UICONTROL Filtypsinställningar]** eller **[!UICONTROL Dokumentskyddsinställningar]** klickar du på **[!UICONTROL Ange standardinställningar]**.
1. Välj standardinställningar. En eller flera av följande inställningar är tillgängliga på sidan Ange standardinställningar:

   **[!UICONTROL Adobe PDF-inställning]**: Det ursprungliga standardvärdet är Standard (Acrobat 6).

   **[!UICONTROL Säkerhetsinställningar]**: Det ursprungliga standardvärdet är Ingen säkerhet (Acrobat 5).

   **[!UICONTROL Filtypsinställningar]**: Det ursprungliga standardvärdet är Standard.

1. Click **[!UICONTROL Save]**.

## Ta bort en filtypsinställning {#delete-a-file-type-setting}

Du kan ta bort en filtypsinställning som inte längre används.

1. I administrationskonsolen klickar du på **[!UICONTROL Tjänster > PDF Generator > Filtypsinställningar]**.
1. Markera kryssrutan bredvid inställningen som ska tas bort. Du kan välja flera källor. Inställningar som inte har någon kryssruta bredvid sig inkluderas alltid i PDF Generator och kan inte tas bort.
1. Klicka på **[!UICONTROL Ta bort]** och klicka på **[!UICONTROL Ta bort]** på bekräftelsesidan.

## Inställningar för bild till PDF {#image-to-pdf-settings}

Följande alternativ bestämmer hur bildfiler konverteras till PDF. Instruktioner om hur du använder de här inställningarna finns i [Skapa eller redigera filtypsinställningar](configuring-file-type-settings.md#create-or-edit-file-type-settings).

**** Filnamnstillägg: Kommaavgränsad lista med filnamnstillägg som kan konverteras.

**** Prova Fallback Converter: PDF Generator kan konvertera bildfiler till PDF med Java™ eller Acrobat. När det här alternativet är markerat och konverteringen misslyckas eller når den angivna tidsgränsen, försöker PDF Generator konvertera med den alternativa metoden. Om den alternativa metoden misslyckas eller når den angivna tidsgränsen, skrivs ett undantag till loggfilen.

***Obs **: JPEG 2000-filer kan bara konverteras med Acrobat.*

**** Använd OCR: Anger om OCR (optisk teckenigenkänning) ska användas på PDF-filen. Med OCR kan du söka efter, korrigera och kopiera texten i PDF-filen.

***Obs **! Funktionen OCR PDF (sökbar PDF) stöds bara i Microsoft Windows.*

**** Primärt OCR-språk: Anger språket som OCR-motorn ska använda för att identifiera tecknen.

**** PDF-utdatastil: Bestämmer vilken typ av PDF som ska skapas. Alla format tillämpar OCR och teckensnitts- och sidigenkänning på textbilderna och konverterar dem till normal text.

**** Sökbar bild: Gör texten sökbar och markeringsbar. Med det här alternativet behålls originalbilden, den skevas efter behov och ett osynligt textlager placeras över den. Alternativet Nedsampla bilder avgör om bilden nedsamplas och i vilken utsträckning.

**** Sökbar bild (exakt): Gör texten sökbar och markeringsbar. Med det här alternativet behålls originalbilden och ett osynligt textlager placeras över den. Rekommenderas för fall där originalbilden kräver maximal återgivning.

**** ClearScan: Syntetiserar ett nytt Type 3-teckensnitt som är snarlikt originalteckensnittet och bevarar sidbakgrunden med hjälp av en lågupplöst kopia.

**** Nedsampla bilder: Minskar antalet pixlar i färgbilder, gråskalebilder och monokroma bilder när OCR är klart. Välj den nedsamplingsgrad som ska användas. Alternativ med högre nummer gör mindre nedsampling, vilket ger PDF-filer med högre upplösning.

## Exportinställningar för Adobe PDF (endast Windows) {#adobe-pdf-export-settings-windows-only}

Inställningen Exportera filtyp i avsnittet Adobe PDF-exportinställningar används för att konvertera en PDF-fil till ett annat format. Standardvärdet är HTML 4.01 med CSS (Cascading Style Sheets) 1.0(&amp;ast;.htm, &amp;ast;.html).

Instruktioner om hur du använder den här inställningen finns i [Skapa eller redigera filtypsinställningar](configuring-file-type-settings.md#create-or-edit-file-type-settings).

## Inställningar för HTML-till-PDF {#html-to-pdf-settings}

Följande alternativ avgör hur HTML-filer konverteras till PDF. Instruktioner om hur du använder dessa alternativ finns i [Skapa eller redigera filtypsinställningar](configuring-file-type-settings.md#create-or-edit-file-type-settings).

**** Prova Fallback Converter: PDF Generator kan konvertera HTML-filer till PDF med Java™ eller Acrobat. När det här alternativet är markerat och konverteringen misslyckas eller når den angivna tidsgränsen, försöker PDF Generator konvertera med den alternativa metoden. Om den alternativa metoden misslyckas eller når den angivna tidsgränsen, skrivs ett undantag till loggfilen.

**** Standardkodning: Anger indatakodningen för filtexten från en meny med operativsystem och alfabet. Använder bara det som har valts och visas i alternativet Standardkodning om HTML-källfilen inte anger någon typ av kodning.

**** Tvinga markerad kodning: Ignorerar kodning som har angetts i HTML-källfilen och använder den som har valts och visas i alternativet Standardkodning.

### Spindelningsinställningar {#spidering-settings}

*Vid inpassning* skannas webbsidor efter länkar till andra webbsidor. När en länk till en annan webbsida påträffas hämtas målsidan och inkluderas i det PDF-dokument som skapas. Aktivera de här alternativen för att ange hur många nivåer som ska hämtas och konverteras till PDF:

**** Hämta endast X-nivåer: Spindlar och konverterar sidor upp till ett djup på den angivna nivån från bassidans URL. Värdet 1 konverterar bara den angivna URL:en.

**** Hämta hela webbplatsen: Konverterar hela platsen med början från angiven URL.

**** Stanna på samma sökväg: Länkar som pekar på sidor som inte finns på samma relativa sökväg som bas-URL:en konverteras inte under spikning.

**** Stanna på samma server: Länkar som pekar på sidor på olika servrar konverteras inte under spikning. Endast länkar som pekar på samma server som den angivna URL:en konverteras.

### Inställningar för sidkonvertering {#page-conversion-settings}

Aktivera dessa alternativ för att ange hur HTML-sidorna ska konverteras. Baserat på sidstorleken justeras bredd-, höjd- och marginalvärdena därefter.

**** Sidstorlek: Välj anpassad och ange bredd och höjd, eller välj fördefinierade mått.

**** Orientering: Välj antingen stående eller liggande för det konverterade PDF-dokumentet.

**** Marginaler: Anger marginaler (Överkant, Underkant, Vänster och Höger) i det genererade PDF-dokumentet.

**** Lägg till bokmärken i PDF: Lägger till bokmärken i PDF-dokumentet.

**** Aktivera PDF med märkord: Bäddar in taggar i PDF-dokumentet.

**** Ange inställningar för inledande vy: Här kan du konfigurera dokumentalternativ, fönsteralternativ och alternativ för användargränssnitt. De här inställningarna bestämmer hur innehållet visas från början.

### Dokumentalternativ {#document-options}

Aktivera de här alternativen för att ange hur innehåll ska visas, hur sidor ska visas i PDF-dokumentet och hur förstoringsnivån ska anges:

**** Visa: Markera de rutor som ska öppnas i Acrobat när PDF-dokumentet öppnas.

**** Sidlayout: Välj typ av sidlayout för PDF-dokumentet.

**** Förstoring: Välj förinställd förstoring för den inledande vyn av PDF-dokumentet eller välj ett anpassat värde. Om du väljer en standardinställning används standardförstoringen i Acrobat.

**** Öppna på sidnummer: Ange det sidnummer som PDF-filen öppnas på.

### Fönsteralternativ {#window-options}

Aktivera de här alternativen för att ange hur fönstret ska storleksändras och visas.

**** Ändra fönstrets storlek till startsidan: Ändrar storleken på Acrobat-fönstret till den inledande sidans storlek.

**** Centrera fönstret på skärmen: Öppnar fönstret mitt på skärmen.

**** Öppna i helskärmsläge: Öppnar fönstret i helskärmsläge.

**** Visa: Visar dokumentets namn eller filnamn i fönstret.

### Alternativ för användargränssnitt {#user-interface-options}

Aktivera dessa alternativ för att ange fönstrets utseende:

**** Dölj menyrad: Döljer menyraden i PDF-dokumentet.

**** Dölj verktygsfält: Döljer verktygsfälten i PDF-dokumentet.

**** Dölj fönsterkontroller: Döljer fönsterkontrollerna i PDF-dokumentet.

## Inställningar för Flash-videor till PDF {#flash-videos-to-pdf-settings}

PDF Generator stöder möjligheten att skicka en video för Adobe Flash (SWF- eller FLV-fil) och skapa en PDF-fil med en inbäddad video för Adobe Flash. Den här konverteringen kräver inte att Adobe Flash Player är installerat på formulärservern. Instruktioner om hur du använder det här alternativet finns i [Skapa eller redigera filtypsinställningar](configuring-file-type-settings.md#create-or-edit-file-type-settings).

**** Filnamnstillägg: Kommaavgränsad lista med filnamnstillägg som kan konverteras.

## Inställningar för XPS till PDF {#xps-to-pdf-settings}

XML Paper Specification (XPS) används i en Windows-utskriftsmaskin. Det här är ett Microsoft-format och kan skapas från alla Microsoft Office-program. Med AEM-formulär kan du konvertera XPS-filer till PDF.

**** Filnamnstillägg: En kommaavgränsad lista över alla XPS-filnamnstillägg som kan konverteras. Det finns för närvarande ett format: .xps.

## Inställningar för PDF-optimering {#pdf-optimizer-settings}

PDF Generator stöder möjligheten att minska storleken på PDF-filer. Om du använder alla dessa inställningar eller bara ett fåtal beror på hur du tänker använda filerna och på de viktigaste egenskaperna som en fil måste ha. I de flesta fall är standardinställningarna lämpliga för maximal effektivitet. Du sparar utrymme genom att ta bort inbäddade teckensnitt, komprimera bilder och ta bort objekt från filer som inte längre behövs.

>[!NOTE]
>
>När du optimerar ett digitalt signerat dokument tas de digitala signaturerna bort och blir ogiltiga.

Instruktioner om hur du använder den här inställningen finns i [Skapa eller redigera filtypsinställningar](configuring-file-type-settings.md#create-or-edit-file-type-settings).

**** PDF-målversion: Anger den version av Acrobat som PDF-filen är kompatibel med.

### Teckensnitt {#fonts}

1. Välj **Teckensnitt.**
1. Välj något av följande alternativ:

   **** Ångra inbäddning av alla teckensnitt: Tar bort inbäddade teckensnitt.

   **** Ångra inte inbäddning av teckensnitt: Tar inte bort inbäddning av teckensnitt.

   **** Ångra inbäddning av vissa teckensnitt: Tar endast bort inbäddning av de angivna teckensnitten. Följ de här stegen för att ange de teckensnitt som du vill frigöra:

   * Om det behövs väljer du en annan teckensnittskatalog i listrutan **Teckensnittskälla** . I den här listrutan visas teckensnittskataloger som anges i **Hem > Inställningar > Kärnsystem > Huvudkonfigurationer**.
   * Markera ett eller flera teckensnitt i listan **Tillgängliga teckensnitt** och klicka på **Lägg till**. De här teckensnitten läggs till i listan **Teckensnitt som inte ska bäddas in** .
   * Om du vill ta bort inbäddningen för vissa teckensnitt som inte finns på formulärservern anger du namnen på teckensnitten i rutan **Lägg till teckensnitt för att ta bort inbäddning** . Click **Add**.
   >[!NOTE]
   >
   >*Om du vill ta bort inbäddningen för vissa teckensnitt vars deluppsättningar är inbäddade i dokumentet, ska du lägga till +-tecknet som prefix för teckensnittsnamnet. Till exempel &quot;+Helvetica&quot;.*

1. Om du bara vill bädda in deluppsättningarna av de inbäddade teckensnitten som är i bruk, markerar du **Skapa delmängd av alla inbäddade teckensnitt**.

   >[!NOTE]
   >
   >*Om du använder det här alternativet i kombination med **Ångra inbäddning av vissa teckensnitt**, frigörs fortfarande fullständigt inbäddade teckensnitt i listan ****Lägg till teckensnitt i.*

   >[!NOTE]
   >
   >*Delinställning av teckensnitt är en teknik som används för att bädda in en del av ett teckensnitt. En teckensnittsdeluppsättning innehåller bara de tecken som används i dokumentet.*

### Öppenhet {#transparency}

Om PDF-dokumentet innehåller bilder som innehåller genomskinlighet kan du använda inställningarna för PDF-optimering för att förenkla genomskinligheten och minska filstorleken.

>[!NOTE]
>
>Om Acrobat 4.0 och senare väljs som PDF-målversion förenklas alla genomskinliga objekt. För andra Target PDF-versioner stöds genomskinlighet och du kan konfigurera genomskinlighetsinställningarna.

Välj **Genomskinlighet** om du vill konfigurera genomskinlighetsinställningarna när du optimerar PDF-dokument.

**Genomskinlighetsnivå** Anger mängden vektorinformation som ska bevaras. Högre inställningar bevarar fler vektorobjekt medan lägre inställningar rastrerar fler vektorobjekt. mellanliggande inställningar bevarar enkla områden i vektorform och rastrerar komplexa. Välj den lägsta inställningen om du vill rastrera hela teckningen.

>[!NOTE]
>
>Hur mycket rastrering som görs beror på sidans komplexitet och vilka typer av överlappande objekt som finns.

**Konturtecknings- och** textupplösning som alla objekt rastreras till, inklusive bilder, vektorgrafik, text och övertoningar. Värdena som stöds är 1 pixlar per tum (ppi) till 9 600 ppi.

>[!NOTE]
>
>Upplösningen för konturteckning och text bör i allmänhet anges till 600-1200 ppi för att ge rastrering av hög kvalitet, särskilt för serif-text och liten teckenstorlek.

**Upplösning för övertoning och nät** som övertoningar och nätövertoningar rastreras till. Värdena som stöds är 1 ppi till 1 200 ppi.

>[!NOTE]
>
>Övertonings- och nätupplösningen bör i allmänhet vara 150-300 ppi eftersom kvaliteten på övertoningar, skuggor och ludd inte förbättras med högre upplösningar, men utskriftstiden och filstorleken ökar.

**Konvertera all text till konturer** Konverterar alla textobjekt (punkttext, text i figur och bantyp) till konturer och tar bort all teckeninformation på sidor som innehåller genomskinlighet. Med det här alternativet ser du till att textbredden förblir konsekvent vid förenkling. Observera att om du aktiverar det här alternativet ser små teckensnitt något tjockare ut när de visas i Acrobat eller skrivs ut på skrivare med låg upplösning. Det påverkar inte kvaliteten på text som skrivs ut på högupplösta skrivare eller fotosättare.

**Konvertera alla linjer till konturer** Konverterar alla linjer till enkla fyllda banor på sidor som innehåller genomskinlighet. Med det här alternativet ser du till att linjebredden förblir konsekvent vid förenkling. Observera att om du aktiverar det här alternativet ser tunna linjer lite tjockare ut och förenklingsprestanda kan försämras.

**Beskär komplexa områden** Ser till att gränserna mellan vektorbilder och rastrerade bilder hamnar längs objektbanor. Med det här alternativet minskas sammanfogningsartefakter som uppstår när en del av en logg] &quot;>

>[!NOTE]
>
>Vissa skrivardrivrutiner bearbetar raster- och vektorbilder på olika sätt, vilket ibland leder till färgojämnheter. Du kan eventuellt minimera problem med färghantering genom att inaktivera vissa inställningar för färghantering som är specifika för skrivardrivrutinen. De här inställningarna varierar beroende på vilken skrivare som används, så mer information finns i dokumentationen som medföljde skrivaren.

Bevara övertryck: Blandar färgen i genomskinliga teckningar med bakgrundsfärgen för att skapa en övertryckningseffekt.

I följande tabell visas vanliga typer av skrivare och deras upplösning mätt i dpi, deras standardrastertäthet mätt i linjer per tum (lpi) och en omsamplingsupplösning för bilder mätt i pixlar per tum (ppi). Om du till exempel skriver ut på en laserskrivare med 600 dpi anger du 170 som upplösning för omsampling av bilder.

**Bilder** Välj Bilder om du vill ange komprimerings- och omsamplingsalternativ för färgbilder, gråskalebilder och monokroma bilder. Du kan experimentera med dessa alternativ för att hitta en lämplig balans mellan filstorlek och bildkvalitet. Upplösningen för färg- och gråskalebilder bör vara 1,5 till 2 gånger rastertätheten som filen skrivs ut med. Upplösningen för monokroma bilder bör vara densamma som för utdataenheten, men tänk på att om du sparar en monokrom bild med en upplösning på över 1 500 dpi ökar filstorleken utan att bildkvaliteten förbättras nämnvärt. Bilder som ska förstoras, t.ex. kartor, kan kräva högre upplösningar.

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

* Markera **Ignorera objekt** om du vill ange vilka objekt som ska tas bort från PDF-filen och optimera kurvformade linjer i CAD-ritningar.
* **Ignorera alla formulärinskicknings-, import- och återställningsåtgärder**: Inaktiverar alla åtgärder som är relaterade till att skicka eller importera formulärdata, och återställer formulärfält. Det här alternativet behåller formulärobjekt som åtgärder är länkade till.
* **Ignorera alla JavaScript-åtgärder**: Tar bort alla åtgärder som använder JavaScript från PDF-filen.
* **Ignorera inbäddade sidminiatyrer**: Tar bort inbäddade sidminiatyrer. Det här alternativet är användbart för stora dokument, som kan ta lång tid att rita sidminiatyrer när du har klickat på sidknappen.
* **Konvertera jämna linjer till kurvor**: Minskar antalet kontrollpunkter som används för att skapa kurvor i CAD-ritningar, vilket ger mindre PDF-filer och snabbare skärmåtergivning.
* **Ignorera inbäddade utskriftsinställningar**: Tar bort inbäddade utskriftsinställningar, t.ex. sidskalning och duplexläge, från dokumentet.
* **Ignorera bokmärken**: Tar bort alla bokmärken från dokumentet.
* **Förenkla formulärfält**: Gör formulärfält oanvändbara utan att deras utseende ändras. Formulärdata sammanfogas med sidan för att bli sidinnehåll.
* **Ignorera alla alternativa bilder**: Tar bort alla versioner av en bild utom den version som ska visas på skärmen. En del PDF-filer innehåller flera versioner av samma bild för olika syften, till exempel skärmvisning med låg upplösning och högupplösta utskrifter.
* **Ignorera dokumenttaggar**: Tar bort taggar från dokumentet, vilket också tar bort textens tillgänglighet och flödesomformning.
* **Identifiera och sammanfoga bildfragment**: Söker efter bilder eller masker som är fragmenterade i tunna segment och försöker sammanfoga segmenten till en enda bild eller mask.
* **Ignorera inbäddat sökindex**: Tar bort inbäddade sökindex, vilket minskar filstorleken.

#### Ignorera användardata {#discard-user-data}

Markera **Ignorera användardata** om du vill ta bort all personlig information som du inte vill distribuera eller dela med andra användare.

* **Ignorera alla kommentarer, formulär och multimedia**: Tar bort alla kommentarer, formulär, formulärfält och multimedia från PDF-filen.
* **Ignorera alla objektdata**: Tar bort alla objekt från PDF-filen.
* **Ignorera externa korsreferenser**: Tar bort länkar till andra dokument. Länkar som hoppar till andra platser i PDF-filen tas inte bort.
* **Ignorera dolt lagerinnehåll och förenkla synliga lager**: Minskar filstorleken. Det optimerade dokumentet ser ut som den ursprungliga PDF-filen, men innehåller ingen lagerinformation.
* **Ignorera dokumentinformation och metadata**: Tar bort information i dokumentinformationsordlistan och alla metadataströmmar. (Använd kommandot Spara som för att återställa metadataströmmar till en kopia av PDF-filen.)
* **Ignorera bifogade filer**: Tar bort alla bifogade filer, inklusive bilagor som lagts till i PDF-filen som kommentarer. (PDF-optimering optimerar inte bifogade filer.)
* **Ignorera privata data från andra program**: Tar bort information från ett PDF-dokument som bara är användbar i det program som dokumentet skapades i. Den här inställningen påverkar inte PDF-filens funktioner, men den minskar filstorleken.

### Rensa {#clean-up}

Välj **Rensa** om du vill ta bort onödiga objekt från dokumentet.
Dessa objekt innehåller element som är föråldrade eller inte behövs för den avsedda användningen av dokumentet. Om du tar bort vissa element kan det allvarligt påverka PDF-filens funktion. Som standard markeras bara element som inte påverkar funktionen. Om du är osäker på vad borttagningen av andra alternativ innebär kan du använda standardmarkeringarna.

**Komprimering**

Välj något av följande alternativ för Flate-komprimering i listrutan:

* Komprimera hela filen
* Komprimera dokumentstruktur
* Ta bort komprimering
* Lämna komprimeringen orörd

**Använd Flate för att koda strömmar som inte är kodade**: Tillämpar Flate-komprimering på alla strömmar som inte är kodade.

**Ignorera ogiltiga bokmärken**: Tar bort bokmärken som pekar på sidor i dokumentet som tas bort.

**Ignorera namngivna destinationer** utan referenser: Tar bort namngivna mål som inte refereras internt från PDF-dokumentet. Det här alternativet söker inte efter länkar från andra PDF-filer eller webbplatser.

**Optimera PDF-filen för snabb webbvisning**: Omstrukturerar ett PDF-dokument för sidvis hämtning (byte-hämtning) från webbservrar.

**Använd Flate i strömmar som använder LZW-kodning i stället**: Tillämpar Flate-komprimering på alla innehållsströmmar och bilder som använder LZW-kodning.

**Ignorera ogiltiga länkar**: Tar bort länkar som hoppar till ogiltiga mål.

**Optimera sidinnehåll**: Konverterar alla radslutstecken till blankstegstecken, vilket förbättrar Flate-komprimeringen.

## Inställningar för Microsoft Excel (endast Windows) {#microsoft-excel-settings-windows-only}

De här alternativen avgör hur Microsoft Excel-filer konverteras. Instruktioner om hur du använder dessa alternativ finns i [Skapa eller redigera filtypsinställningar](/help/forms/using/admin-help/configuring-file-type-settings1.md#main-pars-heading-0).

**Prova OpenOffice som återställningskonverterare**: När det här alternativet är markerat och konverteringen med Microsoft Excel misslyckas eller når den angivna tidsgränsen, försöker PDF Generator konvertera med OpenOffice. Om konverteringen med OpenOffice misslyckas eller når den angivna tidsgränsen, skrivs ett undantag till loggfilen.

**Filnamnstillägg**: Anger filnamnstilläggen för filtyper, avgränsade med kommatecken, som accepteras för det här programmet. The default is `xls,xlsx`. Ta inte med en punkt före eller ett blanksteg mellan tilläggen.

**Skapa en PDF/A-1a-kompatibel fil**: Tvingar fram användningen av Adobe PDF-inställningen PDF/A-1b:2005 RGB.

**Lägg in bokmärken i Adobe PDF**: Konverterar Excel-kalkylbladsnamn till bokmärken. Det här alternativet är markerat som standard.

**Anpassa kalkylblad till en sida**: Minskar textstorleken så att den passar kalkylbladet på en sida.

**Konvertera hela arbetsboken**: Konverterar alla kalkylblad i Excel-filen. Om det här alternativet inte är markerat konverteras bara den aktuella sidan.

**Kör makron automatiskt**: Kör eventuella makron i Excel-dokumentet (t.ex. ett makro som infogar den aktuella tiden) innan du konverterar dokumentet.

**Konvertera dokumentinformation**: Lägger till PDF-dokumentegenskaper baserat på dokumentinformationen i källfilen. Detta inkluderar information som dokumenttitel, författare, ämne och nyckelord.

**Lägg till länkar i Adobe PDF**: Konverterar hyperlänkar i källfilen till hyperlänkar i PDF-dokumentet.

**Bifoga källfil till Adobe PDF**: När det här alternativet är markerat infogas det ursprungliga Excel-kalkylbladet som en bifogad fil i det genererade PDF-dokumentet.

**Aktivera tillgänglighet och flödesomformning med taggad Adobe PDF**: Bäddar in taggar i PDF-dokumentet för att aktivera tillgänglighet och flödesomformning.

**Lista över Excel-tillägg som ska läsas in**: Som standard (av säkerhetsskäl) körs inga Excel-tillägg när en Excel-fil konverteras till PDF. Om du vill tillåta vissa Excel-tillägg att köras under konverteringen anger du en kommaavgränsad lista med tilläggens namn.

**Lista över kalkylblad som ska konverteras**: När den här rutan är tom inkluderas alla kalkylblad i Excel-kalkylbladet i den genererade PDF-filen. Om du vill konvertera en delmängd av kalkylbladet selektivt anger du en kommaavgränsad lista med kalkylbladsnamn.

## Inställningar för Microsoft PowerPoint (endast Windows) {#microsoft-powerpoint-settings-windows-only}

De här alternativen avgör hur Microsoft PowerPoint-filer konverteras. Instruktioner om hur du använder dessa alternativ finns i [Skapa eller redigera filtypsinställningar](/help/forms/using/admin-help/configuring-file-type-settings1.md#create-or-edit-file-type-settings).

**[!UICONTROL Prova OpenOffice som återställningskonverterare]**: När det här alternativet är markerat och konverteringen med Microsoft PowerPoint misslyckas eller når den angivna tidsgränsen, försöker PDF Generator konvertera med OpenOffice. Om konverteringen med OpenOffice misslyckas eller når den angivna tidsgränsen, skrivs ett undantag till loggfilen.

**[!UICONTROL Filnamnstillägg]**: Anger filnamnstilläggen för filtyper, avgränsade med kommatecken, som accepteras för det här programmet. Standardvärdet är ppt,pptx. Ta inte med en punkt före eller ett blanksteg mellan tilläggen.

**[!UICONTROL Konvertera dokumentinformation]**: Lägger till dokumentinformation från egenskapsdialogrutan för källfilen, inklusive titel, ämne, författare, nyckelord, hanterare, företag, kategori och kommentarer. Det här alternativet är markerat som standard.

**[!UICONTROL Lägg in bokmärken i Adobe PDF]**: Konverterar PowerPoint-titlar till bokmärken. Det här alternativet är markerat som standard.

**[!UICONTROL Bifoga källfil till Adobe PDF]**: Lägger till källfilen i PDF-filen som en bifogad fil. Det här alternativet är avmarkerat som standard.

**[!UICONTROL Aktivera tillgänglighet och flödesomformning med taggad Adobe PDF]**: Bäddar in taggar i PDF-filen. Det här alternativet är avmarkerat som standard.

**[!UICONTROL Konvertera multimedia till PDF-multimedia]**: Konverterar multimedia till PDF-multimedia där det är möjligt. Det här alternativet är markerat som standard.

**[!UICONTROL Konvertera stödanteckningar]**: Konverterar stödanteckningar till PDF.

**[!UICONTROL Kör makron automatiskt]**: Kör eventuella makron i PowerPoint-dokumentet (t.ex. ett makro som infogar den aktuella tiden) innan dokumentet konverteras.

**[!UICONTROL PDF-layout baserad på skrivarinställningar]** i PowerPoint: Använder PowerPoint-skrivarinställningar för att utforma PDF-dokumentet.

**[!UICONTROL Lägg till länkar i Adobe PDF]**: Bevarar befintliga länkar när filen konverteras. Länkarnas utseende ändras i allmänhet inte. Länkar kan bara skapas om alternativet Aktivera hjälpmedel också är markerat. Det här alternativet är avmarkerat som standard.

**[!UICONTROL Spara bildövergångar i Adobe PDF]**: Konverterar bildövergångar. Det här alternativet är markerat som standard.

**[!UICONTROL Spara animeringar i Adobe PDF]**: Sparar konverterade animeringar i PDF-filen.

**[!UICONTROL Konvertera dolda bilder till PDF-sidor]**: Konverterar dolda bilder.

**[!UICONTROL Skapa en PDF/A-1a-kompatibel fil]**: Tvingar fram användningen av Adobe PDF-inställningen PDF/A-1b:2005 RGB. Vissa PowerPoint-funktioner konverteras inte när du skapar en PDF-fil. Om en PowerPoint-övergång inte har en motsvarande övergång i Acrobat ersätts en liknande övergång. Om det finns flera animeringseffekter i samma bildruta används en effekt. Sidövergångar och insticksprogram för punkter konverteras.

## Inställningar för Microsoft Project (endast Windows) {#microsoft-project-settings-windows-only}

De här alternativen avgör hur Microsoft Project-filer konverteras. Instruktioner om hur du använder dessa alternativ finns i [Skapa eller redigera filtypsinställningar](/help/forms/using/admin-help/configuring-file-type-settings1.md#main-pars-heading-0).

1. **** Filnamnstillägg: Anger filnamnstilläggen för filtyper, avgränsade med kommatecken, som accepteras för det här programmet. The default is `mpp`. Ta inte med en punkt före eller ett blanksteg mellan tilläggen.

1. **[!UICONTROL Konvertera dokumentinformation]**: Lägger till dokumentinformation från egenskapsdialogrutan för källfilen, inklusive titel, ämne, författare, nyckelord, hanterare, företag, kategori och kommentarer. Det här alternativet är markerat som standard.
1. **[!UICONTROL Bifoga källfil till Adobe PDF]**: Lägger till källfilen i PDF-filen som en bifogad fil.
1. **[!UICONTROL Skapa en PDF/A-1a-kompatibel fil]**: Tvingar fram användningen av Adobe PDF-inställningen PDF/A-1b:2005 RGB.
1. **[!UICONTROL Kör makron automatiskt]**: Kör eventuella makron i Microsoft Project-dokumentet (t.ex. ett makro som infogar den aktuella tiden) innan du konverterar dokumentet.

## Inställningar för Microsoft Word (endast Windows) {#microsoft-word-settings-windows-only}

De här alternativen avgör hur Microsoft Word-filer konverteras. Instruktioner om hur du använder dessa alternativ finns i [Skapa eller redigera filtypsinställningar](/help/forms/using/admin-help/configuring-file-type-settings1.md#main-pars-heading-0).

**[!UICONTROL Prova OpenOffice som återställningskonverterare]**: När det här alternativet är markerat och konverteringen med Microsoft Word misslyckas eller når den angivna tidsgränsen, försöker PDF Generator konvertera med OpenOffice. Om konverteringen med OpenOffice misslyckas eller når den angivna tidsgränsen, skrivs ett undantag till loggfilen.

**[!UICONTROL Filnamnstillägg]**: Anger filnamnstilläggen för filtyper, avgränsade med kommatecken, som accepteras för det här programmet. The default is `doc,docx,rtf,txt`. Ta inte med en punkt före eller ett blanksteg mellan tilläggen.

**[!UICONTROL Konvertera dokumentinformation]**: Lägger till dokumentinformation från egenskapsdialogrutan för källfilen, inklusive titel, ämne, författare, nyckelord, hanterare, företag, kategori och kommentarer. Det här alternativet är markerat som standard.

**[!UICONTROL Lägg in bokmärken i Adobe PDF]**: Konverterar rubriker till bokmärken. Det här alternativet är markerat som standard.

**[!UICONTROL Bifoga källfil till Adobe PDF]**: Lägger till källfilen i PDF-filen som en bifogad fil.

**[!UICONTROL Konvertera korsreferenser och innehållsförteckning till länkar]**: Konverterar alla korsreferenser och innehållsförteckningsposter till länkar. Det här alternativet är markerat som standard.

**[!UICONTROL Aktivera tillgänglighet och flödesomformning med taggad Adobe PDF]**: Bäddar in taggar i PDF-filen. Det här alternativet är markerat som standard.

**[!UICONTROL Skapa en PDF/A-1a-kompatibel fil]**: Om det här alternativet är markerat används Adobe PDF-inställningen PDF/A-1b:2005 RGB.

**[!UICONTROL Kör makron automatiskt]**: Kör eventuella makron i Word-dokumentet (t.ex. ett makro som infogar den aktuella tiden) innan du konverterar dokumentet.

**[!UICONTROL Bevara dokumentmarkeringar i Adobe PDF]**: Konverterar markeringar i Word-dokumentet till anteckningar i PDF-filen.

**[!UICONTROL Lägg till länkar i Adobe PDF]**: Konverterar hyperlänkar i källfilen till hyperlänkar i PDF-dokumentet.

**[!UICONTROL Konvertera fotnots- och slutkommentarslänkar]**: Skapar länkar från fotnots- och slutkommentarscitat till anteckningar i PDF-dokumentet.

**[!UICONTROL Konvertera visade kommentarer till anteckningar i Adobe PDF]**: Konverterar kommentarer i Word-dokumentet till textanteckningar i PDF-dokumentet.

**[!UICONTROL Aktivera avancerad taggning]**: Lägger till avancerade taggar för förbättrad tillgänglighet.

**[!UICONTROL Konvertera alla format till bokmärken]**: Konverterar alla format i Word-dokumentet till bokmärken i PDF-dokumentet.

**[!UICONTROL Format med nivåer]**: Anger vilka format i Word-dokumentet som ska konverteras till bokmärken i PDF-dokumentet. Anger också nivån på bokmärkena. Om du vill använda den här funktionen avmarkerar du alternativet **[!UICONTROL Konvertera alla format till bokmärken]** och anger formatnamnen i följande format:

styleName1=level1[,styleName2=level2...]

Om ett Microsoft Word-formatnamn innehåller ett komma (,) eller likhetstecken (=), skriver du ett escape-tecken (&quot;\_) före specialtecknen. Ange till exempel ett format med namnet &quot;Rubrik, 1&quot; som Rubrik\, 1.

## Inställningar för Microsoft Visio (endast Windows) {#visio}

**Konvertera dokumentinformation**: Lägger till dokumentinformation från egenskapsdialogrutan för källfilen, inklusive titel, ämne, författare, nyckelord, hanterare, företag, kategori och kommentarer. Det här alternativet är markerat som standard. Det här alternativet är aktiverat som standard.

**Lägg till länkar i Adobe PDF**: Bevarar alla länkar. Det här alternativet är markerat som standard.

**Lägg in bokmärken i Adobe PDF**: Konverterar rubriker till bokmärken. Det här alternativet är markerat som standard.

**Bifoga källfil till Adobe PDF**: Lägger till källfilen i PDF-filen som en bifogad fil.

**Lägg alltid samman lager i Adobe PDF**: Förenklar alla Visio-lager.

**Konvertera alla sidor**: Konverterar alla sidor i Visio-filen.

**Öppna panelen Lager när den visas i Adobe Acrobat**: Om Visio-lagren inte förenklas öppnas ett fönster där du kan ange vilka lager som ska bevaras i PDF-filen när den öppnas med Acrobat. Det här alternativet är markerat som standard.

**Skapa en PDF/A-1b-kompatibel fil**: Tvingar fram användningen av Adobe PDF-inställningen PDF/A-1b:2005 (RGB).

**Konvertera kommentarer till Adobe PDF-kommentarer**: Konverterar Visio-anteckningar till PDF-kommentarer.

## Inställningar för Microsoft Publisher (endast Windows) {#microsoft-publisher-settings-windows-only}

De här alternativen avgör hur Microsoft Publisher-filer konverteras. Instruktioner om hur du använder dessa alternativ finns i [Skapa eller redigera filtypsinställningar](/help/forms/using/admin-help/configuring-file-type-settings1.md#main-pars-heading-0).

**[!UICONTROL Filnamnstillägg]**: Anger filnamnstilläggen för filtyper, avgränsade med kommatecken, som accepteras för det här programmet. The default is `pub`. Ta inte med en punkt före eller ett blanksteg mellan tilläggen.

## AutoCAD-inställningar (endast Windows) {#autocad-settings-windows-only}

Dessa alternativ avgör hur AutoCAD-filer konverteras. Instruktioner om hur du använder dessa alternativ finns i [Skapa eller redigera filtypsinställningar](/help/forms/using/admin-help/configuring-file-type-settings1.md#create-or-edit-file-type-settings).

**[!UICONTROL Filnamnstillägg]**: Anger filnamnstilläggen för filtyper, avgränsade med kommatecken, som accepteras för det här programmet. The default is `dwg`. Ta inte med en punkt före eller ett blanksteg mellan tilläggen.

**[!UICONTROL Konvertera dokumentinformation]**: Lägger till dokumentinformation från egenskapsdialogrutan för källfilen, inklusive titel, ämne, författare, nyckelord, hanterare, företag, kategori och kommentarer. Det här alternativet är markerat som standard.

**[!UICONTROL Lägg in bokmärken i Adobe PDF]**: Konverterar rubriker till bokmärken.

**[!UICONTROL Lägg alltid samman lager i Adobe PDF]**: Förenklar alla AutoCAD-lager.

**[!UICONTROL Öppna lagerrutan vid visning i Adobe Acrobat]**: Visar lagerstrukturen när PDF-filen öppnas i Acrobat.

**[!UICONTROL Skapa en PDF/E-1-kompatibel fil]**: Skapar en fil som är PDF/E-1-kompatibel. PDF/E är en ISO-standard för utbyte av tekniska och tekniska dokument. Mer information om PDF/E-1 finns i [Adobe och branschstandarder](https://www.adobe.com/enterprise/standards/index.html).

**[!UICONTROL Konvertera alla layouter]**: Inkluderar alla layouter i PDF-filen.

**[!UICONTROL Konvertera modellområde till 3D]**: När du väljer det här alternativet konverteras modellområdeslayouten till en 3D-anteckning i PDF-filen.

**[!UICONTROL Lägg till länkar i Adobe PDF]**: Om det här alternativet är markerat bevaras alla länkar.

**[!UICONTROL Bifoga källfil till Adobe PDF]**: Lägger till källfilen i PDF-filen som en bifogad fil.

**[!UICONTROL Skapa en PDF/A-1b-kompatibel fil]**: Tvingar fram användningen av Adobe PDF-inställningen PDF/A-1b.

**[!UICONTROL Konvertera alla lager]**: Som standard konverterar PDF Generator bara standardlagret för AutoCAD-filer till PDF i stället för alla lager i filen. Välj det här alternativet om du vill konvertera alla lager i filen.

**[!UICONTROL Bädda in skalinformation]**: Bevarar information om ritskalan.

**[!UICONTROL Konvertera aktuell layout]**: Inkluderar endast den aktuella layouten i PDF-filen.

**[!UICONTROL Lista över AutoCAD-layouter som ska konverteras]**: En AutoCAD-ritning kan ha flera layouter. När den här rutan är tom inkluderas alla layouter i AutoCAD-ritningen i det genererade PDF-dokumentet. Om du vill konvertera en delmängd av layouterna selektivt anger du en kommaavgränsad lista med layoutnamn.

## OpenOffice-inställningar {#openoffice-settings}

De här alternativen avgör hur OpenOffice-filer konverteras. Instruktioner om hur du använder dessa alternativ finns i [Skapa eller redigera filtypsinställningar](/help/forms/using/admin-help/configuring-file-type-settings1.md#create-or-edit-file-type-settings).

**Prova PDFMaker som återställningskonverterare**: När det här alternativet är valt och en konvertering med OpenOffice misslyckas eller når den angivna tidsgränsen, försöker PDF Generator konvertera med PDFMaker. Om konverteringen med PDFMaker misslyckas eller når den angivna tidsgränsen, skrivs ett undantag till loggfilen.

**Filnamnstillägg**: Ange filnamnstilläggen för filtyper, avgränsade med kommatecken, som kan användas i det här programmet. The default is `odt,odp,ods,odg,odf,sxw,sxi,sxd`. Ta inte med en punkt före eller ett blanksteg mellan tilläggen.

**Intervall**: Konvertera alla sidor eller ange vissa sidor eller ett sidintervall. Om inget sidintervall är definierat konverteras alla sidor. Om du vill exportera ett sidintervall använder du formatet 3-6. Om du vill exportera enstaka sidor använder du formatet 7;9;11. Du kan exportera en kombination av sidintervall och enstaka sidor med ett format som 3-6;8;10;12.

**Sidorientering**: För oformaterade textfiler väljer du antingen stående eller liggande för det konverterade PDF-dokumentet.

**Bilder**: Konfigurera hur bilder konverteras. EPS-bilder med inbäddade förhandsvisningar exporteras endast som förhandsvisningar. EPS-bilder utan inbäddade förhandsvisningar exporteras som tomma platshållare. Med förlustfri komprimering av bilder bevaras alla pixlar. Med JPEG-komprimering av bilder och en hög kvalitetsnivå bevaras nästan alla pixlar. Med en låg kvalitetsnivå försvinner vissa pixlar och artefakter uppstår, men filstorleken minskar.

**Allmänt**: Aktivera alternativen för att konvertera en taggad PDF-fil eller för att exportera anteckningar i Writer- och FormCalc-dokument, Impress-bildövergångseffekter eller tomma sidor till PDF-filen. När du exporterar märkord kan filstorleken öka med mycket. Vissa märkord som exporteras är innehållsförteckningar, hyperlänkar och kontroller.

Du kan också ange hur formulär ska skickas. Alternativen är XML, FDF, PDF eller HTML. Den här inställningen åsidosätter kontrollens URL-egenskap som du anger i dokumentet. Endast en gemensam inställning kan väljas för PDF-dokumentet:

* PDF (skickar hela dokumentet)
* FDF (skickar kontrollinnehållet)
* HTML
* XML

**Taggad PDF**: Gör att du kan skapa taggade PDF-filer från OpenOffice-dokument. Taggad PDF innehåller information om strukturen för dokumentinnehållet. Detta kan vara till hjälp när du visar dokumentet på enheter med olika skärmar och när du använder skärmläsarprogram. Det hjälper även tillgänglighetsprogram att utföra olika användbara åtgärder med PDF-dokumentet, t.ex. läsa upp innehållet i PDF-dokumentet.

**Exportera anteckningar**: Konverterar anteckningarna i OpenOffice-dokument till anteckningar i det genererade PDF-dokumentet.

**Använd övergångseffekter**: Konverterar bildruteövergångseffekterna i OpenOffice-presentationer till motsvarande PDF-övergångseffekter.

**Skicka formulär i format**: Skapar ett PDF-formulär som kan fyllas i och skrivas ut av användaren av PDF-dokumentet.

**Exportera automatiskt infogade tomma sidor**: När det här alternativet är markerat inkluderas automatiskt tomma sidor i det genererade PDF-dokumentet. Detta är praktiskt om du skriver ut ett PDF-dokument dubbelsidigt. En bok kan till exempel konfigureras så att den första sidan i kapitlet alltid börjar på en sida med udda nummer. Om det föregående kapitlet slutar på en sida med ojämnt nummer infogar OpenOffice en tom sida med jämnt nummer. Det här alternativet styr om den jämna sidan ska inkluderas i den genererade PDF-filen.

## Andra programinställningar (endast Windows) {#other-applications-settings-windows-only}

Du kan inte ändra inställningarna för andra program via administrationskonsolen; visas filnamnstilläggen för de filtyper som stöds. Instruktioner om hur du använder de här inställningarna finns i [Skapa eller redigera filtypsinställningar](https://help.adobe.com/en_US/AEMForms/6.1/AdminHelp/WS92d06802c76abadb-5145d5d12905ce07e7-7e42.2.html).

* Corel WordPerfect: `wpd`
* Adobe PageMaker: `pmd, pm6, p65, pm`
* Adobe FrameMaker: `fm`
* Adobe Photoshop: `psd`

Stöd för dessa filtyper kan behöva anpassas. Mer information finns i&quot;Adding Support for Additional Native File Formats&quot; (Lägga till stöd för fler inbyggda filformat) i [Programmering med AEM-formulär](https://www.adobe.com/go/learn_aemforms_programming_62).

Hjälp om hur du konfigurerar en PDFG-nätverksskrivare finns i [Konfigurera en PDFG-nätverksskrivare (endast Windows)](/help/forms/using/admin-help/setting-pdfg-network-printer-windows.md).
