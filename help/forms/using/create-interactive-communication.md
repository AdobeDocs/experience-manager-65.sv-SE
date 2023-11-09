---
title: Skapa en interaktiv kommunikation
description: Skapa en interaktiv kommunikation med redigeraren för interaktiv kommunikation. Använd dra-och-släpp-funktionen för att bygga den interaktiva kommunikationen och förhandsgranska både utskrift och webb på olika enhetstyper.
topic-tags: interactive-communications
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
feature: Interactive Communication
exl-id: 1f89c3bf-e67e-4d13-9285-3367be1ac8f8
source-git-commit: 941e5d7574d31622f50e50e717c21cd2eba2e602
workflow-type: tm+mt
source-wordcount: '5989'
ht-degree: 0%

---

# Skapa en interaktiv kommunikation{#create-an-interactive-communication}

## Översikt {#overview}

Interactive Communications centraliserar och hanterar framtagning, sammanställning och leverans av personaliserade och interaktiva korrespondenser. Använd utskrift som huvudkanal för webben och minimera arbetet med att duplicera webbutdata i den interaktiva kommunikationen.

### Förutsättningar {#prerequisites}

Nedan följer några förutsättningar för att skapa en interaktiv kommunikation:

* Konfigurera en [Formulärdatamodell](/help/forms/using/data-integration.md) som innehåller testdata eller med en faktisk datakälla, till exempel en instans av Microsoft® Dynamics.
* Se till att du har [Dokumentfragment](/help/forms/using/document-fragments.md).
* Se till att du har [Mallar för tryck och webbkanal](/help/forms/using/web-channel-print-channel.md).
* Kontrollera att du har rätt [tema](/help/forms/using/themes.md) för webbkanalen.

## Skapa interaktiv kommunikation {#createic}

1. Logga in på AEM författarinstans och navigera till **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms & Documents]**.
1. Tryck **[!UICONTROL Create]** och markera **[!UICONTROL Interactive Communication]**. Sidan Skapa interaktiv kommunikation visas.

   ![create-interactive-communication](assets/create-interactive-communication.png)

1. Ange följande information. :

   * **[!UICONTROL Title]**: Ange titeln på interaktiv kommunikation.
   * **[!UICONTROL Name]**: Namnet på den interaktiva kommunikationen hämtas från den titel du anger. Redigera den om det behövs.
   * **[!UICONTROL Description]**: Ange en beskrivning av interaktiv kommunikation.
   * **[!UICONTROL Form Data Model]**: Bläddra och välj formulärdatamodellen. Mer information om formulärdatamodell finns i [AEM Forms dataintegrering](/help/forms/using/data-integration.md).

   * **[!UICONTROL Prefill Service]**: Välj förifyllningstjänsten för att hämta data och fylla i interaktiv kommunikation i förväg.
   * **[!UICONTROL Post Process Type]**: Du kan välja AEM eller Forms-arbetsflöde som ska utlösas när den interaktiva kommunikationen skickas. Välj vilken typ av arbetsflöde som ska utlösas.

   * **[!UICONTROL Post Process]**: Välj namnet på arbetsflödet som ska utlösas. När du väljer AEM arbetsflöde ska du ange bilagesökväg, layoutsökväg, PDF-sökväg, sökväg till utskriftsdata och webbdatasökväg.
   * **[!UICONTROL Tags]**: Markera de taggar som ska användas i den interaktiva kommunikationen. Du kan också skriva in ett nytt/anpassat taggnamn och trycka på Retur för att skapa det.
   * **[!UICONTROL Author]**:Författarnamnet hämtas automatiskt från den inloggade användarens användarnamn.
   * **[!UICONTROL Publish Date:]** Ange det datum då den interaktiva kommunikationen ska publiceras.
   * **[!UICONTROL Unpublish Date]**: Ange det datum då interaktiv kommunikation ska avpubliceras.

1. Tryck på **[!UICONTROL Next]**. Skärmen där du anger utskrifts- och webbkanalsinformation visas.
1. Ange följande:

   * **[!UICONTROL Print]**: Välj det här alternativet om du vill generera tryckkanalen för interaktiv kommunikation.
   * **[!UICONTROL Print Template]**: Bläddra och välj en XDP-fil som utskriftsmall.
   * **[!UICONTROL Web]**: Välj det här alternativet om du vill generera webbkanalen eller responsiva utdata för interaktiv kommunikation.
   * **[!UICONTROL Interactive Communication Web Template]**: Bläddra och välj webbmallen.
   * **[!UICONTROL Theme]** och **[!UICONTROL Select Theme]**: Bläddra och välj temat för att utforma webbkanalen i den interaktiva kommunikationen. Mer information finns i [Teman i AEM Forms](/help/forms/using/themes.md).

   * **[!UICONTROL Use Print As Master for Web Channel]**: Välj det här alternativet om du vill skapa webbkanalen synkroniserad med utskriftskanalen. Om du använder utskriftskanalen som huvudkanal för webbkanalen kan du säkerställa att innehållet och databindningen för webbkanalen hämtas från utskriftskanalen och att ändringarna som görs i utskriftskanalen återspeglas i webbkanalen när du trycker på Synkronisera. Författarna kan dock bryta arvet för specifika komponenter i webbkanalen efter behov. Mer information finns i [Synkronisera webbkanal med utskriftskanal](../../forms/using/create-interactive-communication.md#synchronize).
Om du väljer **[!UICONTROL Use Print As Master for Web Channel]** kan du välja något av följande lägen för att generera webbkanal:

      * **[!UICONTROL Auto layout]**: Välj det här läget om du automatiskt vill generera platshållare, innehåll och databindning för webbkanalen från utskriftskanalen.
      * **[!UICONTROL Manually organize]**: Välj det här läget om du manuellt vill markera och lägga till Print channel-element i webbkanalen med hjälp av huvudinnehållet som finns i **[!UICONTROL Data Sources]** -fliken. Mer information finns i [Välj Skriv ut kanalelement för att skapa webbkanalsinnehåll](#selectprintchannelelements).

   Mer information om utskriftskanaler och webbkanaler finns i [Skriva ut kanal och webbkanal](/help/forms/using/web-channel-print-channel.md).

1. Tryck på **[!UICONTROL Create]**. Interaktiv kommunikation skapas och en varningsruta visas. Tryck **[!UICONTROL Edit]** för att börja bygga innehållet i det interaktiva meddelandet enligt [Lägga till innehåll med hjälp av gränssnittet för utveckling av interaktiv kommunikation](#step2). Du kan också trycka på **[!UICONTROL Done]** och väljer att redigera interaktiv kommunikation senare.

## Lägga till innehåll i interaktiv kommunikation {#step2}

När du har skapat en interaktiv kommunikation kan du använda redigeringsgränssnittet för interaktiv kommunikation för att skapa dess innehåll.

Mer information om gränssnittet för utveckling av interaktiv kommunikation finns i [Introduktion till utveckling av interaktiv kommunikation](/help/forms/using/introduction-interactive-communication-authoring.md).

1. Utvecklingsgränssnittet för interaktiv kommunikation startas när du trycker på Redigera enligt [Skapa interaktiv kommunikation](#createic). Du kan också navigera till en befintlig interaktiv kommunikationsresurs på AEM, markera den och trycka på **[!UICONTROL Edit]** för att öppna utvecklingsgränssnittet för interaktiv kommunikation.

   Som standard visas den tryckta kanalen i den interaktiva kommunikationen, om inte den interaktiva kommunikationen bara är för webbkanaler. I utskriftskanalen i den interaktiva kommunikationen visas målområdena, som de är tillgängliga i den valda XDP/utskriftskanalmallen. I dessa målområden och fält kan du lägga till komponenter eller resurser.

1. Markera utskriftskanalen och välj **[!UICONTROL Components]** -fliken. Följande komponenter är tillgängliga i utskriftskanalen:

   | **Komponent** | **Funktionalitet** |
   |---|---|
   | Diagram | Lägger till ett diagram som du kan använda i interaktiv kommunikation för visuell representation av tvådimensionella data som hämtats från en formulärdatamodellsamling. Mer information finns i [Använda diagram i interaktiv kommunikation](/help/forms/using/chart-component-interactive-communications.md). |
   | Dokumentfragment | Gör att du kan lägga till en återanvändbar komponent, t.ex. text, lista eller villkor, i en interaktiv kommunikation. Komponenten som läggs till kan antingen vara modellbaserad för formulärdata eller utan en formulärdatamodell. |
   | Bild | Infoga en bild. |

   Dra och släpp komponenterna i din interaktiva kommunikation och konfigurera dem efter behov.

   Du kan också använda åtgärderna ångra och gör om när du skapar en interaktiv kommunikation för både utskrifts- och webbkanaler.

   Använd ångra-åtgärden för att ta bort den senast utförda åtgärden och gör om-åtgärden för att ta med den borttagna åtgärden igen. Om du t.ex. har infogat en bild eller skapat en databindning i ett interaktivt meddelande och behöver ta bort den ska du använda åtgärden ångra.

   ![Ångra Gör om-åtgärder](assets/undo_redo_actions_new.png)

   Alternativen Ångra och Gör om visas i verktygsfältet för redigeringsgränssnittets sida. Alternativet Ångra visas bara efter att en åtgärd har utförts. Alternativet gör om visas bara i verktygsfältet på sidan när du har utfört en ångra-åtgärd. Dessa åtgärder återställs när sidan uppdateras.

1. Med utskriftskanalen markerad går du till **[!UICONTROL Assets]** och använda filtret för att visa endast de resurser du vill se.

   Med hjälp av Assets-webbläsaren kan du även dra och släppa resurser direkt till målområdena för interaktiv kommunikation.

   ![assets-documents](assets/assets-docfragments.png)

1. Dra och släpp dokumentfragmenten i interaktiv kommunikation. Här följer de typer av dokumentfragment som du kan använda i tryckkanalen i den interaktiva kommunikationen.

<table>
 <tbody>
  <tr>
   <td><strong>Dokumentfragmenttyp</strong></td>
   <td><strong>Exempelsyfte</strong></td>
  </tr>
  <tr>
   <td><a href="/help/forms/using/texts-interactive-communications.md" target="_blank">Text</a></td>
   <td>Text för att lägga till adress, mottagarens e-postadress och brödtext i brevet </td>
  </tr>
  <tr>
   <td><a href="/help/forms/using/conditions-interactive-communications.md" target="_blank">Villkor</a></td>
   <td>Villkor för att lägga till lämplig rubrikbild i kommunikationen baserat på typen av princip: Standard eller Premium. <br /> </td>
  </tr>
  <tr>
   <td>Lista</td>
   <td>Grupp med dokumentfragment, inklusive text, villkor, andra listor och bilder. <br /> </td>
  </tr>
 </tbody>
</table>

Du kan också ersätta bindningen mellan ett målområde och ett dokumentfragment genom att släppa det nya fragmentet på målområdet med hjälp av **[!UICONTROL Assets]** -fliken. Målområdets blå färgskuggning när fragmentet dras anger att dokumentfragmentet kan släppas till målområdet.

Mer information om dokumentfragment finns i [Dokumentfragment](/help/forms/using/document-fragments.md).

Med hjälp av redigeringsgränssnittet kan du skilja mellan obundna och bundna fält och variabler i en interaktiv kommunikation. Gränssnittet markerar de obundna fälten och variablerna med en orange ram.

![unbound_fields_variables_highlights_dc](assets/unbound_fields_variables_highlights_dc.jpg)

När du håller muspekaren över dessa element visas dessutom ett verktygstips med meddelandet Fält (obundet) eller Variabel (obundet).

En obunden variabel som används i ett dokumentfragment kanske inte visas i redigeringsgränssnittet. Det kan inträffa på grund av en textbunden regel i ett dokumentfragment eller om det finns ett villkorsfragment. I sådana fall visas ett verktygstips, som är markerat med blått, som en del av dokumentfragmentet. Verktygstipset visar antalet obundna variabler som används i ett dokumentfragment.

![Obunden variabel](assets/df_unbound_variable_new.png)

Tryck på dokumentfragmentet, tryck på ![configure_icon](assets/configure_icon.png) (Konfigurera) och tryck sedan på **[!UICONTROL Properties]** från sidan med den interaktiva kommunikationslösningen. The **[!UICONTROL Variables and Data Model Objects]** I listas variablerna, inklusive de dolda variablerna, och datamodellsobjekten som används i dokumentfragmenten. Använd ![redigera](assets/edit.svg) (Redigera) bredvid varje datamodellsobjekt eller variabel för att redigera egenskaperna.

1. Ställ in variabelbindning genom att trycka på en variabel och välja ![configure_icon](assets/configure_icon.png) (Konfigurera) och ange sedan bindningsegenskaperna i panelen Egenskaper i sidofältet.

   * **Ingen**: Agenten fyller i variabelns värde.
   * **Textfragment**: Om du väljer det här alternativet kan du bläddra och markera ett textdokumentfragment vars innehåll återges i fältet. Endast textdokumentfragment kan bindas till variabler som inte har några variabler inuti.
   * **Datamodellsobjekt**: Välj en formulärdatamodellsegenskap vars värde är ifyllt i fältet.
   * **Standardvärde:** I det här fältet kan du definiera ett standardvärde för variabeln. Värdet visas när du förhandsgranskar den interaktiva kommunikationen eller i agentgränssnittet.
   * **Visningsmönster:** Du kan också definiera ett visningsformat för en variabel. Välj något av de fördefinierade alternativen i dialogrutan **Typ** nedrullningsbar lista för att använda ett visningsformat på en variabel. Välj **Egen** för att definiera ett visningsmönster som inte är tillgängligt i listan. Mer information finns i [Visningsmönster](../../forms/using/create-interactive-communication.md#datadisplaypatterns).

   Navigera till [Variabler och datamodellsobjekt](../../forms/using/create-interactive-communication.md#hiddenvariables) för att ställa in bindning av dolda variabler i dokumentfragmentet.

   Du kan också dra och släppa datakällelement eller textdokumentfragment för att ställa in bindning av variabler.  Om du vill skapa en bindning med något av datakällelementen väljer du **Datakällor** och dra och släpp elementet till variabelnamnet. Datakällelementet och variabeln måste vara av samma typ för att bindningen ska kunna konfigureras korrekt. Om du drar och släpper ett datakällelement till en redan bunden variabel, ersätter det nya elementet det föregående och skapar en bindning med variabeln. På samma sätt väljer du **Resurser** och dra och släpp textdokumentfragmentet till variabelnamnet för att ange bindningen mellan dem. Textdokumentfragmentet får inte innehålla några variabler.

1. Om du vill lägga till en tabell med utskriftskanalen markerad går du till **[!UICONTROL Assets]** använder du filtret för att bara visa Layoutfragment. Dra och släpp önskat layoutfragment till Interactive Communication. Ett layoutfragment är baserat på en XDP och kan användas för att skapa grafiska layouter eller statiska och dynamiska tabeller i interaktiv kommunikation som fylls i med dynamiska data.

   Exempel: En layouttabell som visar bruttopremie, förmånsersättning % och tillgänglighet för assistans vid nödsituationer för gamla och nya policyer.

   Mer information om layoutfragment finns i [Dokumentfragment](/help/forms/using/document-fragments.md).

1. Med utskriftskanalen markerad i **[!UICONTROL Assets]** använder du filtret för att visa bilder. Dra-och-släpp de bilder som behövs till Interactive Communication, t.ex. företagslogotyp.

   Hantera dessutom följande i den interaktiva kommunikationen:

   * [Lägga till och konfigurera diagram](/help/forms/using/chart-component-interactive-communications.md)
   * [Synkronisera webbkanalen med utskriftskanalen](../../forms/using/create-interactive-communication.md#synchronize)

      * Automatisk synkronisering
      * Avbryt arv
      * Återaktivera arv
      * Synkronisera

   * [Bifogade filer och biblioteksåtkomst](../../forms/using/create-interactive-communication.md#attachmentslibrary)
   * [Egenskaper för XDP-/layoutfält](../../forms/using/create-interactive-communication.md#xdplayoutfieldproperties)
   * [Lägga till regler i komponenter](../../forms/using/create-interactive-communication.md#rules)

1. Växla till **[!UICONTROL Web Channel]**. Webbkanalen visas i redigeraren för interaktiv kommunikation. När du byter från Print-kanalen till Web channel för första gången sker den automatiska synkroniseringen. Mer information finns i [Synkronisera webbkanal från utskriftskanalen](../../forms/using/create-interactive-communication.md#synchronize).

   Eftersom vi använder Skriv ut som master för webben i det här exemplet synkroniseras platshållarna för utskriftskanalen, innehållet och databindningen till webbkanalen. Du kan dock ändra och anpassa det specifika innehållet i webbkanalen. [Avbryt arv](#cancelinheritance) för målområden och variabler som har genererats med tryckkanalen för att kunna anpassa innehållet.

   ![webbkanalresurser](assets/webchannelassets.png)

   Tryck på dokumentfragmentet, tryck på ![configure_icon](assets/configure_icon.png) (Konfigurera) och tryck sedan på **[!UICONTROL Properties]** från sidan med den interaktiva kommunikationslösningen. The **[!UICONTROL Variables and Data Model Objects]** I listas variablerna, inklusive de dolda variablerna, och datamodellsobjekten som används i dokumentfragmenten. Använd ![redigera](assets/edit.svg) (Redigera) bredvid varje datamodellsobjekt eller variabel för att redigera egenskaperna. Dessutom för dokumentfragment som har [autogenererad](#synchronize) i webbkanalen med Print channel använder du ![avbrytarv](assets/cancelinheritance.png) (Avbryt arv), ikon bredvid varje datamodellsobjekt och variabel till [avbryt arv](#cancelinheritance) och kunna redigera dem.

1. Om du vill lägga till fler komponenter i webbkanalen trycker du på **[!UICONTROL Components]**. Dra och släpp komponenter i webbkanalen i din interaktiva kommunikation efter behov och fortsätt att konfigurera dem.

   | Komponenter | Funktionalitet |
   |---|---|
   | Diagram | Lägger till ett diagram som du kan använda i interaktiv kommunikation för visuell representation av tvådimensionella data som hämtats från en formulärdatamodellsamling. Mer information finns i [Använda diagramkomponent](../../forms/using/chart-component-interactive-communications.md). |
   | Dokumentfragment | Gör att du kan lägga till en återanvändbar komponent, text, lista eller villkor i en interaktiv kommunikation. Den återanvändbara komponenten som du lägger till i en interaktiv kommunikation kan antingen vara modellbaserad i form av formulärdata eller utan någon formulärdatamodell. |
   | Bild | Infoga en bild. |
   | Panel | Gör att du kan lägga till en [Panel](../../forms/using/create-interactive-communication.md#add-panel-component-to-the-web-channel) till interaktiv kommunikation. |
   | Tabell | Lägger till en tabell där du kan ordna data i rader och kolumner. |
   | Målområde | Infogar ett målområde i en webbkanal för att ordna de webbkanalsspecifika komponenterna. Målområdet är en ren behållare som gör att du kan gruppera webbkanalsspecifika komponenter. |
   | Text | Lägger till RTF i webbkanalen i en interaktiv kommunikation. Text kan också använda formulärdatamodellsobjekt för att göra innehållet dynamiskt. |
   | Knapp | Gör att du kan lägga till en [Knapp](../../forms/using/create-interactive-communication.md#add-button-component-to-the-web-channel) till interaktiv kommunikation. Du kan använda komponenten Button för att navigera till annan interaktiv kommunikation, adaptiva formulär, andra resurser som bilder eller dokumentfragment eller en extern URL. |
   | Avgränsare | Gör att du kan infoga en vågrät linje i en interaktiv kommunikation. Använd den här komponenten för att skilja mellan avsnitt i en korrespondens. Du kan till exempel använda avgränsningskomponenten för att skilja mellan kundinformation och kreditkortsinformation i en kreditkortsutdrag. |

1. Infoga resurser i webbkanalen efter behov.

   Du kan [förhandsgranska interaktiv kommunikation](#previewic) för att se hur tryck- och webbutdata för den interaktiva kommunikationen ser ut och fortsätta att göra ändringar efter behov.

## Förhandsgranska interaktiv kommunikation {#previewic}

Du kan använda **Förhandsvisningsalternativ** för att utvärdera hur den interaktiva kommunikationen ser ut. Webbkanalen i Interactive Communication erbjuder också ett alternativ för att emulera upplevelsen av en interaktiv kommunikation för olika enheter. Exempel: iPhone, iPad och Desktop. Du kan använda båda **Förhandsgranska** och **Emulator** ![linjal](assets/ruler.png) tillsammans med varandra för att förhandsgranska webbutdata för enheter med olika skärmstorlekar. Exempeldata i förhandsgranskningen fylls i från den angivna formulärdatamodellen.

1. Markera kanalen (tryck eller webb) om du vill förhandsgranska och trycka på Förhandsgranska. Interaktiv kommunikation visas.

   >[!NOTE]
   >
   >Förhandsgranskningen fylls i med den angivna formulärdatamodellens exempeldata. Mer information om hur du förhandsgranskar interaktiv kommunikation med vissa andra data eller använder förifyllningstjänsten finns i [Använd formulärdatamodell](/help/forms/using/using-form-data-model.md) och [Arbeta med formulärdatamodell](/help/forms/using/work-with-form-data-model.md).

1. Använd ![linjal](assets/ruler.png) för att se hur den interaktiva kommunikationen ser ut på olika enheter.

   ![webchannelPreview](assets/webchannelpreview.png)

Dessutom kan du [Förbereda och skicka interaktiv kommunikation med agentgränssnittet](/help/forms/using/prepare-send-interactive-communication.md).

## Konfigurera egenskaper i interaktiv kommunikation  {#configure-properties-in-interactive-communication}

### Bifogade filer och biblioteksåtkomst {#attachmentslibrary}

I utskriftskanalen kan du konfigurera bilagor och biblioteksåtkomst så att agenten kan hantera bilagor i agentgränssnittet för den interaktiva kommunikationen:

1. Markera dokumentbehållaren i utskriftskanalen och tryck på **Egenskaper**.

   ![dokumentbehållareegenskaper](assets/documentcontainerproperties.png)

   Panelen Egenskaper visas i sidofältet.

   ![egenskaperbilagor](assets/propertiesattachments.png)

1. Expandera **Bifogade filer** och ange följande egenskaper:

   * **[!UICONTROL Allow Library Access]**: Välj det här alternativet om du vill aktivera biblioteksåtkomst för agenten i agentgränssnittet. Om det här alternativet är aktiverat kan agenten lägga till filer från biblioteket när den interaktiva kommunikationen förbereds.
   * **[!UICONTROL Allow Re-Ordering Of Attachments]**: Välj det här alternativet om du vill att agenten ska kunna ändra ordning på de bifogade filerna med interaktiv kommunikation.
   * **[!UICONTROL Max Number Of Attachments Allowed]**: Ange maximalt antal bilagor som tillåts med interaktiv kommunikation.
   * **[!UICONTROL Files To Be Attached]**: Tryck **[!UICONTROL Add]** och bläddra till de filer som ska bifogas och ange följande:

      * **[!UICONTROL Attach This File To Document By Default]**: Du kan ändra det här alternativet om bara bilagan inte är obligatorisk.
      * **[!UICONTROL Mandatory:]** Agenten kan inte ta bort den bifogade filen i agentens användargränssnitt.

   ![bifogade filer](assets/attachfiles.png)

1. Tryck på **[!UICONTROL Done]**.

### Egenskaper för XDP-/layoutfält {#xdplayoutfieldproperties}

1. Håll muspekaren över ett fält som är inbyggt i kanalmallen för utskrift när du redigerar Print-kanalen i en interaktiv kommunikation och välj ![configure_icon](assets/configure_icon.png) (Konfigurera).

   Dialogrutan Egenskaper visas i sidlisten.

   ![data_display_patterns_fields](assets/data_display_patterns_fields.jpg)

1. Ange följande:

   * **[!UICONTROL Name]**: JCR-nodnamn.
   * **[!UICONTROL Title]**: Ange en titel som ska visas för agenten i agentgränssnittet och i dokumentbehållarträdet.
   * **[!UICONTROL Binding Type]**: Välj en av följande bindningstyper för fältet.

      * Ingen: Agenten fyller i egenskapens värde.
      * Textfragment: Om du väljer det här alternativet kan du bläddra och markera ett textdokumentfragment vars innehåll återges i fältet. Du kan också dra och släppa textdokumentfragmentet till fältnamnet för att ange bindningen mellan dem. Textdokumentfragmentet får inte innehålla några variabler.
      * Datamodellobjekt: Välj en formulärdatamodellegenskap vars värde fylls i i fältet. Du kan även välja **Datakällor** och dra och släpp egenskapen till fältet.

   * **[!UICONTROL Default Values]**: Standardvärdet ser till att fältet inte är tomt när det inte finns något värde från det angivna datamodellsobjektet eller textfragmentet. Om databindningstypen inte är någon fylls standardvärdet i i förväg i fältet.
   * **[!UICONTROL Display Pattern]**: Du kan också definiera ett visningsformat för ett fält. Välj något av de fördefinierade alternativen i dialogrutan **Typ** nedrullningsbar lista för att använda ett visningsformat för ett fält. Välj **Egen** för att definiera ett visningsmönster som inte är tillgängligt i listan. Mer information finns i [Visningsmönster](../../forms/using/create-interactive-communication.md#datadisplaypatterns)

   * **[!UICONTROL Editable By Agent]**: Välj det här alternativet om agenten ska kunna redigera värdet i fältet i agentens användargränssnitt. Den här inställningen gäller inte om bindningstypen är Textfragment.
   * **[!UICONTROL Label]**: Ange en textsträng som visas med fältet till agenten i agentgränssnittet. Den här inställningen gäller inte om bindningstypen är Textfragment.
   * **[!UICONTROL Tooltip]**: Ange en textsträng som ska visas när muspekaren förs till agenten i agentgränssnittet. Den här inställningen gäller inte om bindningstypen är Textfragment.
   * **[!UICONTROL Required]**: Välj att göra fältet obligatoriskt för agenten. Den här inställningen gäller inte om bindningstypen är Textfragment.
   * **[!UICONTROL Allow multiple lines]**: Markera det här fältet om du vill tillåta flera textrader som inmatning i fältet. Den här inställningen gäller inte om bindningstypen är Textfragment.

1. Tryck ![ready_icon](assets/done_icon.png).

### Visningsmönster {#datadisplaypatterns}

Med hjälp av redigeringsgränssnittet kan du definiera datavisningsmönster för fält, variabler och formulärdatamodellelement som är tillgängliga när du skapar en interaktiv kommunikation för tryck- och webbkanaler.

Om du vill konfigurera datamönstret trycker du på elementet och väljer ![configure_icon](assets/configure_icon.png) (Konfigurera) och konfigurera visningsmönstret i dialogrutan **[!UICONTROL Properties]** panelen i sidlisten. Välj ett fördefinierat alternativ i dialogrutan **[!UICONTROL Type]** om du vill visa mönstret som är associerat med den valda typen. Välj **[!UICONTROL Custom]** från **[!UICONTROL Type]** i listrutan för att definiera ett mönster som inte är tillgängligt i listan. Redigera värden i **[!UICONTROL Pattern]** fältet ändrar automatiskt typen till **[!UICONTROL Custom]**.

Om du vill använda visningsmönstret måste antalet tecken eller siffror som definieras i fältet Mönster matcha eller överskrida de tecken eller siffror som definieras i värdet för fält, variabler och formulärdatamodellelement. Mer information finns i [exempel](../../forms/using/create-interactive-communication.md#greaternumberofdigits).

![data_display_pattern_example](assets/data_display_patterns_ssn_new.png)

Du kan omdefiniera visningsmönstret för ett fält, en variabel eller ett element i en formulärdatamodell när du har genererat webbinnehåll från utskriftskanalen. Därför kan ett element ha olika visningsmönster definierade för utskrifts- och webbkanaler. Om du inte definierar ett visningsmönster för ett element i en utskriftskanal och automatiskt genererar webbinnehåll med hjälp av en utskriftskanal, definierar databindningen som är definierad för elementet i utskriftskanalen de visningsmönsteralternativ som finns i **[!UICONTROL Type]** listruta. Om ingen bindning har definierats för elementet definierar elementets datatyp de tillgängliga alternativen för visningsmönster. Om du till exempel skapar en databindning av typen Number för ett element i en utskriftskanal, är alternativen för visningsmönster tillgängliga i **[!UICONTROL Type]** nedrullningsbar lista är av typen Number i olika format.

Växla till **Förhandsgranska** eller öppna agentens användargränssnitt för att visa det visningsmönster som används för dessa element.

I följande tabell visas ett exempel på de värden som visas som ett resultat av inställningen av datavisningsmönstret för en variabel:

| Typ | Standardvärde | Visningsmönster | Visningsvärde | Beskrivning |
|---|---|---|---|---|
| SocialSecurityNumber | 123456789 | text{999-99-9999} | 123-45-6789 | Antalet siffror i standardvärdefältet matchar antalet siffror i mönsterfältet. Värdet baserat på mönstret visas. |
| SocialSecurityNumber | 1234567 | text{999-99-9999} | 1-23-4567 | Antalet siffror i standardvärdefältet är mindre än antalet siffror i mönsterfältet. Mönstret används på de 7 tillgängliga siffrorna. |
| SocialSecurityNumber | 1234567890 | text{999-99-9999} | 1234567890 | Antalet siffror i standardvärdefältet är större än antalet siffror i mönsterfältet. Därför ändras inte visningsvärdet. |

Om inget visningsmönster anges för en variabel eller ett element i formulärdatamodellen, [konfiguration av globalt dokumentfragment](https://helpx.adobe.com//experience-manager/6-5/forms/using/interactive-communication-configuration-properties.html) används som standard.

Om du inte använder ett visningsmönster för en variabel med taldatatyp, visas mönstret i förhandsvisningen enligt den globala dokumentfragmentkonfigurationen. Om du tillämpar ändringar i standardkonfigurationen för globala dokumentfragment, visar agentgränssnittet fortfarande mönstret enligt standardavgränsarna som är definierade för språkområdet.

Om inget visningsmönster anges för fält används på samma sätt det mönster som definierades när utskriftsmallen (XDP) skapades för fältet. Om det inte finns något mönster när du skapar utskriftsmallen används standardmönstren som baseras på XFA-specifikationerna i fälten.

Om det angivna visningsmönstret är felaktigt eller inte kan användas, används dessutom standardmönstren som baseras på XFA-specifikationerna för fälten, variablerna eller elementen i formulärdatamodellen.

## Tillämpa regler på komponenter för interaktiv kommunikation {#rules}

Om du vill anpassa komponenter eller innehåll i den interaktiva kommunikationen trycker du på komponenten/delen av innehållet och väljer ![createruleicon](assets/createruleicon.png) (Skapa regel) för att starta regelredigeraren.

Mer information finns i:

* [Regelredigeraren](/help/forms/using/rule-editor.md)
* [Introduktion till utveckling av interaktiv kommunikation](/help/forms/using/introduction-interactive-communication-authoring.md)

## Använda tabeller {#tables}

### Dynamiska tabeller i interaktiv kommunikation {#dynamic-tables-in-interactive-communication}

Du kan lägga till dynamiska tabeller i interaktiv kommunikation med hjälp av layoutfragment. I följande steg används ett exempel på en kreditkortssats för att illustrera hur ett layoutfragment används för att skapa en dynamisk tabell i ett interaktivt meddelande.

1. Kontrollera att det layoutfragment som krävs för att skapa tabellen är tillgängligt i AEM.
1. Dra och släpp ett layoutfragment (med en tabell med flera kolumner) i ett målområde från resursläsaren i utskriftskanalen i din interaktiva kommunikation.

   ![lf_dragdrop](assets/lf_dragdrop.png)

   En tabell visas i layoutområdet Interaktiv kommunikation.

   ![lf_dragdrop_table](assets/lf_dragdrop_table.png)

1. Ange databindning för alla celler i tabellen. Om du vill skapa en repeterbar rad infogar du egenskaper för formulärdatamodell i raden som tillhör en gemensam samlingsegenskap.

   1. Tryck på en cell i tabellen och markera ![configure_icon](assets/configure_icon.png) (Konfigurera).

      Dialogrutan Egenskaper visas i sidlisten.

      ![lf_cell_properties](assets/lf_cell_properties.png)

   1. Konfigurera egenskaperna:

      * **[!UICONTROL Name]**: JCR-nodnamn.
      * **[!UICONTROL Title]**: Ange en titel som ska visas i Interactive Communication Editor.
      * **[!UICONTROL Binding Type]**: Välj en av följande bindningstyper för fältet.

         * **[!UICONTROL None]**
         * **[!UICONTROL Data model object]**: Värdet för en formulärdatamodellegenskap fylls i i fältet. Du kan även välja **Datakällor** och dra och släpp egenskapen till fältet.

      * **[!UICONTROL Data Model Object]**: Den formulärdatamodellsegenskap vars värde är ifyllt i fältet.
      * **[!UICONTROL Default Value]**: Standardvärdet ser till att fältet inte är tomt när det inte finns något värde från det angivna datamodellobjektet. Standardvärdet är förifyllt i fältet.

      * **[!UICONTROL Editable By Agent]**: Välj det här alternativet om agenten ska kunna redigera värdet i fältet i agentens användargränssnitt.

   1. Tryck ![ready_icon](assets/done_icon.png).

1. Förhandsgranska den interaktiva kommunikationen för att se tabellen renderas med data.

   ![lf_preview](assets/lf_preview.png)

### Enbart tabeller för webbkanaler {#webchanneltables}

Tryck på rotpanelen i webbmallen och tryck på **+** för att lägga till **Tabell** till Interactive Communication. En tabell med två rader infogas i interaktiv kommunikation. Tabellens första rad representerar tabellrubriken.

#### Lägga till rader och kolumner i tabellen {#addrowscolumnstable}

**Så här lägger du till eller tar bort kolumner:**

1. Tryck på standardtextrutan i tabellrubrikraden för att visa komponentens verktygsfält.
1. Välj **Lägg till kolumn** eller **Ta bort kolumn** om du vill lägga till eller ta bort tabellkolumner.

![component_toolbar_table1](assets/component_toolbar_table1.png)

**Så här lägger du till eller tar bort rader:**

1. Tryck på någon av tabellraderna för att visa komponentens verktygsfält. Du kan också markera en tabellrad med hjälp av innehållsläsaren i sidokickaren i den interaktiva kommunikationen.
1. Välj **Lägg till rad** eller **Ta bort rad** om du vill lägga till eller ta bort tabellrader. Använd **Flytta uppåt** och **Flytta nedåt** i verktygsfältet för att ordna om rader i tabellen.

![Komponentverktygsfältet](assets/component_toolbar_table_row_new.png)

**S.** Lägg till rad **B.** Radera en rad **C.** Flytta uppåt **D.** Flytta nedåt

#### Lägga till eller redigera text i tabellceller {#addedittexttable}

1. Markera standardtextrutan i tabellcellen och tryck på ![redigera](assets/edit.png) (Redigera).
1. Skriv texten i tabellcellen och tryck på ![ready_icon](assets/done_icon.png) för att spara den.

#### Skapa bindning mellan tabellceller och datamodellobjektselement {#createbindingtablecells}

1. Markera standardtextrutan i tabellraden och tryck på ![redigera](assets/edit.png) (Redigera).
1. Tryck på listrutan Datamodellsobjekt och välj egenskapen.
1. Tryck för att spara och skapa en bindning mellan tabellcellen och datamodellens objektegenskap.

![Skapa databindning](assets/create_data_binding_table_new.png)

#### Skapa en hyperlänk för text i tabellcellen {#createhyperlinktable}

1. Markera standardtextrutan i tabellcellen och tryck på ![redigera](assets/edit.svg) (Redigera).
1. Markera texten i tabellcellen och tryck på ikonen Hyperlänk.
1. Ange URL-adressen i **Bana** fält.
1. Tryck ![ready_icon](assets/done_icon.png) för att spara hyperlänksegenskaperna.

![Skapa hyperlänk](assets/create_hyperlink_table_new.png)

#### Skapa dynamiska tabeller {#createdynamictables}

Du kan skapa en dynamisk tabell bara för webbkanaler i en interaktiv kommunikation med hjälp av en datamodellegenskap av typen samling. En sådan tabell är en representation av en samlingsegenskaps underordnade egenskaper. Du kan bara redigera formateringsegenskaperna för de olika cellerna i tabellen.

1. Växla till webbkanalen och välj sedan att visa webbläsaren Datakällor.
1. Dra en samlingsegenskap till ett delformulär. En tabell skapas i delformuläret.
1. Förhandsgranska tabellen i webbförhandsgranskningen av den interaktiva kommunikationen.

#### Sortera kolumner i en tabell {#sortcolumns}

Du kan sortera data baserat på valfri kolumn i en tabell i den interaktiva kommunikationen. Värdena i kolumnen kan sorteras i stigande eller fallande ordning.

Sortering kan användas för tabellkolumner som innehåller:

* Statisk text
* Egenskaper för datamodellsobjekt
* Kombination av statiska text- och datamodellsobjektsegenskaper

Så här aktiverar du sortering:

1. Markera tabellen och tryck på ![configure_icon](assets/configure_icon.png) (Konfigurera). Du kan också markera tabellen med **Innehåll** webbläsaren i sidospåret av Interactive Communication.
1. Välj **Aktivera sortering.**
1. Tryck ![ready_icon](assets/done_icon.png) om du vill spara tabellegenskaperna. Sorteringsikonerna, uppåt- och nedåtpilarna, i kolumnrubriker representerar att sorteringen har aktiverats.

   ![Aktivera sortering](assets/enable_sorting_new-1.png)

1. Växla till **Förhandsgranska** för att visa utdata. Tabellen sorteras automatiskt baserat på tabellens första kolumn.
1. Klicka på kolumnrubriken om du vill sortera värdena baserat på kolumnen.

   En kolumnrubrik med en uppåtpil representerar:

   * tabellen sorteras utifrån den kolumnen.
   * värden i kolumnen visas i stigande ordning.

   ![Sortering stigande](assets/sorting_ascending_new-1.png)

   På samma sätt visas en kolumnrubrik med en nedpil som värden i kolumnen i fallande ordning.

## Redigera egenskaper för interaktiv kommunikation {#edit-interactive-communication-properties}

När du har skapat en interaktiv kommunikation kan du redigera dess egenskaper i ett senare skede.

Använd **Egenskaper** sida till:

* Redigera värden för de fält som anges när du skapar den interaktiva kommunikationen, till exempel Rubrik och Beskrivning.
* Lägg till eller ta bort webbkanal för en befintlig interaktiv kommunikation.
* Förhandsgranska, ladda ned eller ta bort interaktiv kommunikation
* Öppna [Agentgränssnitt](/help/forms/using/prepare-send-interactive-communication.md).

Så här öppnar du **Egenskaper** sida:

1. Logga in på AEM författarinstans och navigera till **Adobe Experience Manager** > **Forms** > **Forms och dokument**.
1. Välj Interaktiv kommunikation och tryck **Egenskaper**.
1. Välj **Allmänt** för att redigera **Titel** och **Beskrivning** fält.

### Lägga till eller ta bort webbkanalen {#add-or-delete-the-web-channel}

Utför följande steg för att lägga till webbkanalen för en befintlig interaktiv kommunikation:

1. På **Egenskaper** väljer du **Kanaler** -fliken.
1. Välj **Webb** och välj en mall för webbkanalen.
1. Välj **Använd Skriv ut som mallsida för webbkanal** för att aktivera synkronisering mellan webbkanalen och utskriftskanalen.
1. Tryck **Spara och stäng** för att spara ändringarna.

   Du kan också trycka på **Webb** kryssrutan på **Kanaler** för att ta bort webbkanalen från Interactive Communication.

## Lägg till Button-komponent i webbkanalen {#add-button-component-to-the-web-channel}

Du kan lägga till en knapp som en komponent i webbkanalen i den interaktiva kommunikationen. Definiera regler med [regelredigerare](../../forms/using/rule-editor.md) för att kunna navigera till annan interaktiv kommunikation, adaptiva formulär, andra resurser som bilder eller dokumentfragment, eller en extern URL när du trycker på knappen.

Så här lägger du till en knapp och definierar regler för den:

1. Tryck på rotpanelen i webbmallen och tryck på **+** för att lägga till **Knapp** till Interactive Communication.
1. Tryck på knappkomponenten och tryck på ![edit-rules](assets/edit-rules.png) om du vill definiera regler för knapptryckningen.
1. I **När** avsnitt, markera **klickad** från knappens nedrullningsbara lista.
1. I **Sedan** avsnitt:

   1. Välj en åtgärd i listrutan. Välj till exempel **Navigera till** som åtgärdstyp.

   1. Ange URL:en för den interaktiva kommunikationen, adaptiva formulär, en resurs eller en webbsida. Ange till exempel URL:en i följande format för att navigera till en annan interaktiv kommunikation: https://&lt;server-name>:&lt;port>/editor.html/&lt;interactive communication=&quot;&quot; name=&quot;&quot;>/kanaler/&lt;channel name=&quot;&quot; print=&quot;&quot; or=&quot;&quot; web=&quot;&quot;>.html
   1. Ange alternativet för att öppna resursen på samma flik, på en ny flik eller i ett nytt fönster.
   1. Tryck **Klar** och sedan trycka **Stäng** för att spara regeln.

   På samma sätt kan du välja andra tillgängliga alternativ i listrutan för åtgärdstyp, som Anropa tjänst och Skicka formulär. Mer information finns i [regelredigerare](../../forms/using/rule-editor.md).

1. Förhandsgranska interaktiv kommunikation och tryck på knappen för att visa interaktiv kommunikation, adaptiv form, en resurs eller en webbsida som anges i steg 4(b).

## Lägg till panelkomponent i webbkanalen {#add-panel-component-to-the-web-channel}

Panelkomponenten är en platshållare för att gruppera andra komponenter och styr hur en grupp komponenter, som dragspelspanel och tabbar, placeras i det interaktiva meddelandet. Med en panelkomponent kan du också göra en grupp komponenter repeterbara för slutanvändaren, t.ex. i flera poster som krävs för att fylla i inloggningsuppgifter.

Utför följande steg för att lägga till en panelkomponent i webbkanalen:

1. Infoga **Panel** i webbkanalen med något av följande alternativ:

   * Tryck på en komponent, tryck **+** och väljer **Panel** -komponenten.

   * Från **Komponent** webbläsarpanelen, dra och släppa **Panel** i Interactive Communication.

   * Tryck på **Panel** i **Innehåll** webbläsarpanelen och tryck **Lägg till underordnad panel**. Markera **Lägg till underordnad panel** alternativet visar **Lägg till underordnad panel** -dialogrutan. Ange panelkomponentens titel och en valfri beskrivning och namn.

1. Tryck på panelen från **Innehåll** webbläsare för att utföra ytterligare åtgärder på panelen, till exempel konfigurera, redigera regler, kopiera, ta bort och infoga komponent.

   Du kan också dra och släppa en panel i **Innehåll** webbläsaren för att återspegla ändringen i strukturen för den interaktiva kommunikationen i den högra rutan.

## Synkronisera webbkanal med utskriftskanal {#synchronize}

När du väljer Skriv ut som mallsida för webbkanal när du skapar en interaktiv kommunikation skapas webbkanalen synkroniserat med utskriftskanalen och webbkanalens innehåll och databindning härleds från utskriftskanalen och ändringarna som görs i den kan återspeglas i webbkanalen när du trycker på Synkronisera.

Författarna kan dock bryta arvet för komponenter i webbkanalen efter behov.

![Skapa utskriftsmall](assets/create_ic_print_master_new-1.png) ![Print Master Web](assets/create_ic_print_master_web_new-1.png)

### Automatisk synkronisering {#autosync}

Om du väljer **[!UICONTROL Use Print As Master for Web Channel]** kan du välja något av följande lägen för att generera webbkanal:

* **[!UICONTROL Auto layout]**: Välj det här läget om du automatiskt vill generera platshållare, innehåll och databindning för webbkanalen från utskriftskanalen.
* **[!UICONTROL Manually organize]**: Välj det här läget om du manuellt vill markera och lägga till Print channel-element i webbkanalen med huvudinnehållet som finns på fliken Datakällor. Mer information finns i [Välj Skriv ut kanalelement för att skapa webbkanalsinnehåll](#selectprintchannelelements).

![Skapa IC-alternativ](assets/create_ic_options_updated_new.png)

>[!NOTE]
>
>Synkronisering av kanalerna synkroniserar endast dokumentfragment, bilder, villkor, listor och layoutfragment från tryckkanalen till webbkanalen. De delformulär eller överordnade noder som innehåller sådana element synkroniseras inte.

### Välj Skriv ut kanalelement för att skapa webbkanalsinnehåll {#selectprintchannelelements}

Om du väljer Skriv ut som master när du skapar den interaktiva kommunikationen och inte väljer alternativet för automatisk synkronisering, kan du även dra och släppa Print channel-element till webbkanalens redigeringsgränssnitt.

Navigera till **Datakällor** > **Huvudinnehåll** för att visa kanalelementen för utskrift. Dra och släpp målområdena, fälten eller tabellerna i webbkanalens redigeringsgränssnitt. En blå cirkel bredvid elementnamnet anger att elementet för utskriftskanalen redan finns i webbkanalen.

![Huvudinnehåll](assets/master_content.png)

### Avbryt arv {#cancelinheritance}

I webbkanalen är komponenterna inbäddade i målområdena.

Hovra över det relevanta målområdet eller variabeln i webbkanalen och välj ![avbrytarv](assets/cancelinheritance.png) (Avbryt arv) och tryck sedan på Avbryt arv i dialogrutan Avbryt arv **[!UICONTROL Yes]**.

Arvet av komponenterna i målområdet avbryts och nu kan du redigera dem efter behov.

### Återaktivera arv {#re-enable-inheritance}

Om du har avbrutit arvet av en komponent i webbkanalen kan du aktivera den igen. Om du vill återaktivera arv håller du pekaren över gränsen för det relevanta målområdet, som innehåller komponenten, och trycker ![återaktivera arv](assets/reenableinheritance.png).

Dialogrutan Återställ arv visas.

![återarv](assets/revertinheritance.png)

Välj vid behov **[!UICONTROL Synchronize The Page After Reverting Inheritance]**. Välj det här alternativet om du vill synkronisera hela den interaktiva kommunikationen. Om du inte markerar det här alternativet synkroniseras bara det relevanta målområdet när arvet återställs.

Tryck på **[!UICONTROL Yes]**.

### Synkronisera {#synchronize-1}

Om du använder Skriv ut som mallsida för webbkanal och ändrar utskriftskanalen, kan du synkronisera innehållet för att lägga till de nya ändringarna i webbkanalen.

1. Om du vill synkronisera webbkanalen med skrivarkanalen växlar du till webbkanalen och trycker på ikonen Fler alternativ.

   ![Alternativ för automatisk synkronisering](assets/auto_sync_options_new.png)

1. Tryck på något av följande:

   * **[!UICONTROL Sync with Print]**: Synkroniserar endast innehåll för de målområden där arv inte avbryts.
   * **[!UICONTROL Reset]**: Synkroniserar webbkanalsinnehållet med utskriftskanalen och ignorerar alla ändringar som gjorts i webbkanalen.

### Använda komponentens verktygsfält för att utföra åtgärder på ärvda komponenter {#componenttoolbar}

När du har autogenererat innehåll i webbkanalen med alternativet Synkronisera kan du utföra fler åtgärder på komponenter utan att avbryta arv.

![Komponentverktygsfältet](assets/component_toolbar_inherited_web_new.png)

Tryck på komponenten för att visa följande alternativ:

* **Copy:** Kopiera en komponent och klistra in den på andra platser i den interaktiva kommunikationen.
* **Klipp ut:** Flytta en komponent från en plats till en annan i interaktiv kommunikation.
* **Infoga komponent:** Infoga en komponent ovanför den markerade komponenten.
* **Klistra in:** Klistra in komponenten som du klipper ut eller kopierar med alternativen som beskrivs ovan.
* **Grupp:** Markera flera komponenter om du vill klippa ut, kopiera eller klistra in mer än en komponent tillsammans.
* **Överordnad:** Markera den överordnade komponenten för en komponent.
* **Visa SOM-uttryck:** Visa [SOM-uttryck](../../forms/using/using-som-expressions-adaptive-forms.md) för komponenten.

* **Gruppera objekt i panelen:** Gruppera komponenterna på en panel för att kunna utföra åtgärder på dessa komponenter samtidigt. Mer information finns i [Gruppera objekt i panelen](#groupobjectspanel).

* **Avbryt arv:** [Avbryt arvet](#cancelinheritance) av komponenterna i målområdet för att redigera dem.

### Gruppera objekt i panelen {#groupobjectspanel}

Med webbkanalens redigeringsgränssnitt är det lättare att gruppera komponenterna på en panel för att kunna utföra åtgärder på dessa komponenter samtidigt. The **Innehåll** På -fliken visas de grupperade komponenterna som underordnade element för panelen i innehållsträdet.

1. Tryck på en komponent och markera gruppen ( ![grupp](assets/group.jpg)).
1. Markera flera komponenter och tryck **Gruppera objekt i panelen**.

   ![Gruppera objekt](assets/component_toolbar_group_objects_new.png)

1. I **Gruppera objekt i panelen** anger du ett namn för panelen.
1. Ange en valfri titel och beskrivning för panelen.
1. Klicka ![bullet_checkmark](assets/bullet_checkmark.png).

   De grupperade komponenterna visas som underordnade element till panelen i innehållsträdet.

   ![content_tree_grouping](assets/content_tree_grouping.png)

## Utdataformat för utskriftskanal {#output-format-print-channel}

Använd PrintChannel API för att definiera utdataformat för Print-kanalen i en interaktiv kommunikation. Om du inte definierar något utdataformat genereras utdata i AEM Forms-format.

```javascript
//options for rendering print channel of a multi-channel document
PrintChannelRenderOptions renderOptions = new PrintChannelRenderOptions();
PrintDocument printDocument = printChannel.render(renderOptions);
```

Om du vill generera utdata i något annat format anger du typ av utdataformat. Se [PrintChannel API](https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/output/api/PrintConfig.html) om du vill se en lista över de utdataformat som stöds.

Du kan till exempel använda följande exempel för att definiera PCL som utdataformat för en interaktiv kommunikation:

```javascript
//options for rendering print channel of a multi-channel document
PrintChannelRenderOptions renderOptions = new PrintChannelRenderOptions();
renderOptions.setRenderFormat(PrintConfig.HP_PCL_5e);
PrintDocument printDocument = printChannel.render(renderOptions);
```
