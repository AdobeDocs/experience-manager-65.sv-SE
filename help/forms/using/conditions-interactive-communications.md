---
title: Villkor i interaktiv kommunikation
seo-title: Villkor i interaktiv kommunikation
description: Att skapa och redigera villkorsfragment som ska användas i interaktiv kommunikation - villkoret är en av de fyra typer av dokumentfragment som används för att skapa interaktiv kommunikation. De andra tre är texter, listor och layoutfragment.
seo-description: Skapa och redigera villkor som ska användas i interaktiv kommunikation
uuid: c98f02d5-1769-46dd-ab35-6e8145a24939
topic-tags: interactive-communications
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: fe59d260-d392-4d6f-bb7e-2f2a1d701f51
docset: aem65
translation-type: tm+mt
source-git-commit: a326e508a781b3afaba8b5e371aa862a30536740

---


# Villkor i interaktiv kommunikation{#conditions-in-interactive-communications}

Att skapa och redigera villkorsfragment som ska användas i interaktiv kommunikation - villkoret är en av de fyra typer av dokumentfragment som används för att skapa interaktiv kommunikation. De andra tre är texter, listor och layoutfragment.

## Översikt {#overview}

Villkor är ett dokumentfragment som du kan inkludera i en interaktiv kommunikation. De andra dokumentfragmenten är [text](../../forms/using/texts-interactive-communications.md), lista och layoutfragment. Med villkor kan du definiera en eller flera sammanhangsberoende resurser som tas med i ett interaktivt meddelande baserat på angivna data och regler.

Exempel:

* I kreditkortsbeskedet visar du kreditkortets årsavgift och kreditkortsbilden baserat på typen av kundens kreditkort.
* I en påminnelse om försäkringspremier visar du beräkningar av skatt baserat på kundens skatter.

Resurserna i de villkor som återges baserat på de regler som tillämpas och de värden som skickas till regeln. Reglerna i villkoren kan kontrollera värden i följande typer av data:

* Egenskapen för associerad formulärdatamodell
* Alla variabler som du skapar i villkoret
* Strängar
* Nummer
* Matematiska uttryck
* Datum

## Skapa villkor {#createcondition}

1. Välj **[!UICONTROL Formulär]** > **[!UICONTROL Dokumentfragment]**.
1. Välj **[!UICONTROL Skapa]** > **[!UICONTROL Villkor]**.
1. Ange följande information:

   * **[!UICONTROL Titel]**: (Valfritt) Ange villkorets titel. Titlar behöver inte vara unika och kan innehålla specialtecken och tecken som inte är engelska. Villkoren refereras till av deras titlar (om de är tillgängliga), t.ex. i miniatyrbilder och egenskaper.
   * **[!UICONTROL Namn]**: Villkorets unika namn i en mapp. Det får inte finnas två dokumentfragment (text, villkor eller lista) i något läge med samma namn i en mapp. I fältet Namn kan du bara ange engelska tecken, siffror och bindestreck. Fältet Namn fylls i automatiskt baserat på fältet Titel. De specialtecken, blanksteg, siffror och icke-engelska tecken som anges i fältet Titel ersätts med bindestreck i fältet Namn. Även om värdet i fältet Titel automatiskt kopieras till namnet kan du redigera värdet.

   * **[!UICONTROL Beskrivning]**: Skriv en beskrivning av dokumentfragmentet.
   * **[!UICONTROL Formulärdatamodell]**: Alternativknappen Formulärdatamodell kan också användas för att skapa villkoret baserat på en formulärdatamodell. När du väljer alternativknappen för formulärdatamodell visas fältet **[!UICONTROL Formulärdatamodell]** . Bläddra och välj en formulärdatamodell. När du skapar villkor för en interaktiv kommunikation måste du se till att du använder samma datamodell som du tänker använda i den interaktiva kommunikationen. Mer information om formulärdatamodell finns i [Dataintegrering](../../forms/using/data-integration.md).

   * **[!UICONTROL Taggar]**: Om du vill skapa en egen tagg anger du ett värde i textfältet och trycker på Retur. När du sparar det här villkoret skapas de nya taggarna.

1. Tryck på **[!UICONTROL Nästa]**.

   Sidan Skapa villkor visas.

   ![createcondition](assets/createcondition.png)

1. Tryck på **[!UICONTROL Lägg till resurser]**.

   Sidan Välj resurser visas och visar tillgängliga texter, listor, villkor och bilder som kan läggas till i villkoret.

   >[!NOTE]
   >
   >Endast icke-baserade, nyskapade resurser och FDM-baserade resurser (som skapats med samma FDM som villkoret som skapas) visas på sidan Välj resurser.

1. Tryck på lämpliga resurser för att markera de som ska inkluderas i villkoret och tryck sedan på **[!UICONTROL Klar]**.

   Sidan Skapa villkor visas och de tillagda resurserna visas.

   ![createconderresurserLägg till](assets/createconditionassetsadd.png)

   Du kan använda följande alternativ för att hantera resurser i ett villkor:

   ![createconditionscreenassetsaddedannotated](assets/createconditionscreenassetsaddedannotated.png)

   **[En]avvisa ändring.**Tryck på den här ikonen om du vill ignorera de ändringar du kan ha gjort i resursen och regeln i villkoret.   **[B]Acceptera ändring.**Tryck på den här ikonen om du vill acceptera ändringarna som du har gjort i resursen och regeln i villkoret.   **[C]Duplicera resurs.**Tryck på den här ikonen om du vill skapa en kopia av resursen tillsammans med den tillämpade regeln, om någon, i villkoret. Sedan kan du fortsätta redigera regeln och resursen för duplicerad resurs. Att duplicera en resurs är användbart när du vill skapa liknande regler för att visa alternativa resurser baserat på en viss kontext.   **[D]Visa förhandsgranskning.**Tryck på den här ikonen om du vill visa en förhandsvisning av resursen på sidan Skapa\Redigera villkor.   **[E]Ändra ordning.**Tryck och håll ned den här ikonen om du vill dra och släppa resurser för att ändra ordning på dem i ett villkor.

   Du kan välja följande alternativ för att ange hur villkoret fungerar under körning:

   * **Utvärdering av flera resultat har inaktiverats\Utvärdering av flera resultat har aktiverats**: När det här alternativet är aktiverat (visas som&quot;Flera resultatutvärderingar är aktiverade&quot;) utvärderas alla regler och resultatet är summan av alla true-regler. Om det här alternativet är inaktiverat (visas som&quot;Flera resultatutvärderingar är inaktiverade&quot;) utvärderas endast den första regeln som är true och blir villkorets utdata.

   * **Sidbrytning**: Välj det här alternativet ( ![break](assets/break.png)) om du vill lägga till en sidbrytning mellan villkorens resurser. Om det här alternativet inte är markerat ( ![ingen brytning](assets/nobreak.png)), och ett villkor flödar över till nästa sida i utskriften, flyttas hela villkoret till nästa sida i stället för att brytas i sidan mellan resurserna i villkoret.

1. Tryck på **[!UICONTROL Skapa regel]** för att lägga till regler för att visa eller dölja resurserna efter behov. Information om hur du använder variabler i reglerna finns i [Skapa variabler](#variables). Mer information finns i [Lägga till regler i villkor](#ruleeditor).

   De regler som skapas visas i kolumnen RULE på skärmen Skapa villkor.

   ![createconditionscreenrulesadded](assets/createconditionscreenrulesadded.png)

   >[!NOTE]
   >
   >Du kan infoga resurser i villkoret som redan har regler eller upprepningar.

1. Tryck på **[!UICONTROL Spara]**.

   Villkoret skapas. Nu kan du fortsätta använda villkoret som byggsten när du skapar en interaktiv kommunikation.

   >[!NOTE]
   >
   >Om du vill spara ett nytt eller redigerat villkor måste du ha minst en regel för varje resurs som läggs till i villkoret.

## Redigera ett villkor {#edit-a-condition}

Du kan redigera ett villkor med följande steg. Du kan också välja att redigera ett villkor i en interaktiv kommunikation genom att välja Redigera fragment på snabbmenyn.

1. Välj **[!UICONTROL Formulär]** > **[!UICONTROL Dokumentfragment]**.
1. Navigera till villkoret och markera det.
1. Tryck på **[!UICONTROL Redigera]**.
1. Gör de ändringar som krävs i villkoret. Mer information om hur du kan ändra ett villkor finns i [Skapa villkor](#createcondition).
1. Tryck på **[!UICONTROL Spara]** och sedan på **[!UICONTROL Stäng]**.

## Skapa regler i villkor {#ruleeditor}

Med regelredigeraren i ett villkor kan du skapa regler för att visa eller dölja resurser baserat på **förinställda villkor**. Dessa villkor kan utformas utifrån:

* Strängar
* Nummer
* Matematiska uttryck
* Datum
* Egenskaper för associerad formulärdatamodell
* Alla [variabler](#variables) som du har skapat

### Skapa regel i villkor {#create-rule-in-condition}

1. När du skapar eller redigerar ett villkor trycker du på ikonen för ![regelredigeraren](assets/ruleeditoricon.png) (regelredigeraren) för den aktuella resursen.

   Dialogrutan Skapa regel visas. Förutom sträng, tal, matematiskt uttryck och datum finns följande även i regelredigeraren för att skapa satser för reglerna:

   * Egenskaper för associerad formulärdatamodell
   * Alla [variabler](#variables) som du har skapat.
   ![createruledialog](assets/createruledialog.png)

   Välj lämpligt alternativ som ska utvärderas.

   >[!NOTE]
   >
   >Samlingsegenskapen stöds inte för att skapa regler för att visa resurser.

1. Välj lämplig operator för att utvärdera regeln, till exempel Är lika med, Innehåller och Börjar med.
1. Infoga det utvärderande uttrycket, strängen, datamodellens egenskap, variabel eller datum.

   ![Regel som visar en resurs när policytypen är standard](assets/ruleincondition.png)

   Regel som visar en resurs när policytypen är standard

   * När du skapar eller redigerar en regel kan du också trycka på ![icon_resize](assets/icon_resize.png) (Ändra storlek) för att utöka dialogrutan Skapa regel/Redigera regel. I den utökade dialogrutan med hela fönster kan du skapa [variabler](#variables) för att skapa regler. Tryck på Ändra storlek igen för att gå tillbaka till den vanliga dialogrutan Skapa regel.

   * Du kan också skapa flera villkor i en regel.

1. Tryck på **[!UICONTROL Klar]**.

   Regeln tillämpas på resursen.

## Skapa och använda variabler i ett villkor {#variables}

När du skapar eller redigerar en regel i ett villkor kan du trycka på ![icon_resize](assets/icon_resize.png) (Ändra storlek) för att utöka dialogrutan Skapa regel\Redigera regel. I den utökade fullfönsterdialogen kan du:

* Skapa och använda variabler i regeln
* Dra och släpp egenskaper och variabler för formulärdatamodellen i regeln

Tryck på Ändra storlek igen för att gå tillbaka till dialogrutan Skapa regel\Redigera regel.

### Skapa variabler {#create-variables}

1. När du skapar eller redigerar en regel i ett villkor kan du trycka på ![icon_resize](assets/icon_resize.png) (Ändra storlek) för att utöka dialogrutan Skapa regel\Redigera regel.

   Dialogrutan för det utökade fullfönstret visas.

   ![expandededitruledialog](assets/expandededitruledialog.png)

1. Tryck på **[!UICONTROL Variabler]** i den vänstra rutan.

   Rutan Variabler visas.

   ![expandededitrulevariables](assets/expandededitrulevariables.png)

1. Tryck på **[!UICONTROL Skapa]**.

   Rutan Skapa variabler visas.

1. Ange följande information och tryck på **[!UICONTROL Skapa]**:

   * **[!UICONTROL Namn]**: Variabelns namn.
   * **[!UICONTROL Beskrivning]**: Du kan också ange en beskrivning av variabeln.
   * **[!UICONTROL Typ]**: Välj en typ av variabel: Sträng, Nummer, Boolean eller Datum.
   * **[!UICONTROL Tillåt endast]** specifika värden: För String- och Number-variabler kan du se till att agenten väljer från en viss uppsättning värden för en platshållare i agentens användargränssnitt. Om du vill ange värdeuppsättningen markerar du det här alternativet och anger sedan kommaavgränsade värden som tillåts i fältet **[!UICONTROL Värden]** .

1. Tryck på **[!UICONTROL Skapa]**.

   Variabeln skapas och visas i variabelrutan.

1. Om du vill infoga en variabel i regeln drar och släpper du variabeln i en platshållare för ett alternativ i regeln.
1. När du har skapat en giltig regel trycker du på **[!UICONTROL Klar]**.

   Fortsätt att göra ytterligare ändringar, om det behövs, i villkoret och spara det.

