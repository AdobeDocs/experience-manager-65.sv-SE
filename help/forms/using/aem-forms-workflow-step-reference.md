---
title: Formulärcentrerat arbetsflöde i OSGi - stegreferens
seo-title: Formulärcentrerat arbetsflöde i OSGi - stegreferens
description: Med formulärbaserat arbetsflöde i OSGi-steg kan du snabbt skapa anpassningsbara formulärbaserade arbetsflöden.
seo-description: Med formulärbaserat arbetsflöde i OSGi-steg kan du snabbt skapa anpassningsbara formulärbaserade arbetsflöden.
uuid: 6f791c45-0e35-4c55-9106-5340caab94b7
contentOwner: null
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: f0a5588d-f210-4f04-bc35-b62834f90ab1
docset: aem65
translation-type: tm+mt
source-git-commit: 489ff793e05e01c59faba63d60cc362e4f26f703

---


# Formulärcentrerat arbetsflöde i OSGi - stegreferens{#forms-centric-workflow-on-osgi-step-reference}

## Arbetsflödessteg för formulär {#forms-workflow-steps}

Blankettstegen utför AEM Forms-specifika åtgärder i ett AEM-arbetsflöde. Med de här stegen kan du snabbt skapa anpassningsbara formulärbaserade formulärbaserade arbetsflöden i OSGi. Dessa arbetsflöden kan användas för att utveckla enkla arbetsflöden för granskning och godkännande, interna och övergripande affärsprocesser. Du kan också använda steg i formulärarbetsflödet för att starta dokumenttjänster, integrera med signaturarbetsflödet i Adobe Sign och utföra andra AEM Forms-åtgärder. Du behöver [tillägget](https://www.adobe.com/go/learn_aemforms_documentation_63) AEM Forms för att kunna använda dessa steg i ett arbetsflöde.

## Tilldela aktivitetssteg {#assign-task-step}

Tilldela ett uppgiftssteg skapar en uppgift och tilldelar den till en användare eller grupp. Förutom att tilldela uppgiften anger komponenten även det adaptiva formuläret eller den icke-interaktiva PDF-filen för uppgiften. Det adaptiva formuläret krävs för att kunna ta emot indata från användare och icke-interaktiva PDF-filer eller ett skrivskyddat anpassat formulär används endast för granskning.

Du kan också använda komponenten för att styra aktivitetens beteende. Du kan till exempel skapa ett automatiskt postdokument, tilldela uppgiften till en viss användare eller grupp, ange sökvägen till skickade data, ange sökvägen till data som ska fyllas i i förväg och ange standardåtgärder. Tilldela uppgift-steget har följande egenskaper:

* **** Titel: Uppgiftens namn. Titeln visas i AEM Inbox.
* **** Beskrivning: Förklaring av de åtgärder som utförs i uppgiften. Den här informationen är användbar för andra processutvecklare när du arbetar i en delad utvecklingsmiljö.

* **** Miniatyrbildssökväg: Sökväg till aktivitetsminiatyrbilden. Om ingen sökväg anges visas en standardminiatyrbild för ett anpassat formulär och en standardikon för Postdokument.
* **** Arbetsflödesfas: Ett arbetsflöde kan ha flera steg. Dessa steg visas i AEM Inbox. Du kan definiera de här stegen i modellens egenskaper (Sidspark > Sida > Sidegenskaper > Steg).
* **** Prioritet: Den valda prioriteten visas i AEM Inbox. De tillgängliga alternativen är Hög, Medel och Låg. Standardvärdet är Medel.
* **** Förfallodatum: Ange antalet dagar eller timmar efter vilka aktiviteten har markerats som försenad. Om du väljer **Av** markeras uppgiften aldrig som försenad. Du kan också ange en uttidshanterare för att utföra vissa åtgärder när åtgärden är försenad.

* **** Dagar: Antalet dagar innan uppgiften ska slutföras. Antalet dagar räknas efter att uppgiften har tilldelats en användare. Om en uppgift inte är fullständig och korsar det antal dagar som anges i fältet Dagar, aktiveras en timeout-hanterare efter förfallodatumet, om detta väljs.
* **** Timmar: Antalet timmar innan uppgiften ska slutföras. Antalet timmar räknas efter att uppgiften har tilldelats en användare. Om en uppgift inte är slutförd och korsar det antal timmar som anges i fältet Timmar, aktiveras en timeout-hanterare efter de timmar som ska förfalla.
* **** Tidsgräns efter förfallodatum: Välj det här alternativet om du vill aktivera markeringsfältet för Timeout-hanteraren.
* **** Timeout-hanterare: Välj det skript som ska köras när tilldelningssteget överskrider förfallodatumet. Skript som placeras i CRX-databasen i [apps]/fd/dashboard/scripts/timeoutHandler kan väljas. Den angivna sökvägen finns inte i crx-databasen. En administratör skapar sökvägen innan den används.
* **** Markera åtgärden och kommentera från den senaste aktiviteten i Uppgiftsinformation: Välj det här alternativet om du vill visa den senaste åtgärden som utfördes och kommentaren som togs emot i aktivitetsinformationsavsnittet för en uppgift.
* **** Typ: Välj vilken typ av dokument som ska fyllas när arbetsflödet startas. Du kan välja ett adaptivt formulär, ett skrivskyddat adaptivt formulär, ett icke-interaktivt PDF-dokument, ett gränssnitt för interaktiv kommunikationsagent eller ett dokument för interaktiv kommunikationskanal.
* **** Använd adaptiv form: Ange den metod som ska användas för att hitta indataadaptiva formulär. Det här alternativet är tillgängligt om du väljer Adaptivt formulär eller Skrivskyddat anpassat formulär i listrutan Typ. Du kan använda det adaptiva formuläret som skickas till arbetsflödet, som finns på en absolut sökväg eller som finns på en sökväg i en variabel. Du kan använda en variabel av typen String för att ange sökvägen.\
   Du kan koppla flera adaptiva formulär till ett arbetsflöde. Det innebär att du kan ange ett anpassningsbart formulär i körningsmiljön med hjälp av de tillgängliga indatametoderna.

* **** Använd interaktiv kommunikation: Ange den metod som ska användas för att hitta den interaktiva indatakommunikationen. Du kan använda den interaktiva kommunikationen som skickas till arbetsflödet, som finns på en absolut sökväg eller som finns på en sökväg i en variabel. Du kan använda en variabel av typen String för att ange sökvägen. Det här alternativet är tillgängligt om du väljer gränssnittet Interactive Communication Agent eller Interactive Communication Web Channel Document i listrutan Typ.\
   **** Obs! Du måste ha grupptilldelningar för cm-agent-users och arbetsflödesanvändare för att få tillgång till gränssnittet för Interactive Communications Agent i AEM-inkorg.

* **Adaptiv form eller interaktiv kommunikationsväg**: Ange sökvägen till det adaptiva formuläret eller interaktiv kommunikation. Du kan använda det adaptiva formuläret eller den interaktiva kommunikationen som skickas till arbetsflödet, som finns på en absolut sökväg, eller hämta det adaptiva formuläret från en sökväg som lagras i en variabel av strängdatatyp.
* **** Välj PDF-indata med: Ange sökvägen till ett icke-interaktivt PDF-dokument. Fältet är tillgängligt när du väljer ett icke-interaktivt PDF-dokument i fältet Typ. Du kan välja PDF-indata med den sökväg som är relativ till nyttolasten, som har sparats med en absolut sökväg eller med en variabel av dokumentdatatypen. Exempel: [Payload_Directory]/Workflow/PDF/credit-card.pdf. Sökvägen finns inte i crx-databasen. En administratör skapar sökvägen innan den används. Du måste aktivera alternativet Dokument för post eller formulärmallsbaserade adaptiva formulär för att kunna använda alternativet PDF-sökväg.
* **Rendera det anpassningsbara formuläret som**: När en uppgift har markerats som slutförd kan du återge det anpassningsbara formuläret som ett skrivskyddat anpassat formulär eller som ett PDF-dokument. Du måste ha alternativet Dokument i post aktiverat eller formulärmallsbaserade adaptiva formulär för att kunna återge det adaptiva formuläret som Dokument i post.
* **** Förifylld: Följande fält i listan nedan fungerar som indata för uppgiften:

   * **** Välj indatafil med: Sökväg till indatafil (.json,). xml, .doc eller formulärdatamodell). Du kan hämta indatafilen med en sökväg som är relativ till nyttolasten eller hämta filen som lagras i en variabel av datatypen Document, XML eller JSON. Filen innehåller till exempel de data som skickats för formuläret via ett AEM Inbox-program. En exempelsökväg är [Payload_Directory]/workflow/data.
   * **** Välj indatabilagor med: Bifogade filer som är tillgängliga på platsen bifogas till formuläret som är kopplat till uppgiften. Sökvägen är alltid relativ till nyttolasten. En exempelsökväg är [Payload_Directory]/attachments/
   * **** Välj JSON-indata: Välj en JSON-indatafil med en sökväg som är relativ till nyttolasten eller som lagras i en variabel av datatypen Document, JSON eller Form Data Model. Det här alternativet är tillgängligt om du väljer gränssnittet Interactive Communication Agent eller Interactive Communication Web Channel Document i listrutan Typ.
   * **** Välj en anpassad förifyllningstjänst: Välj förifyllningstjänsten för att hämta data och fylla i dokumentet för webbkanalen för interaktiv kommunikation eller användargränssnittet för agenten i förväg.

   * **** Använd förifyllningstjänsten för den interaktiva kommunikation som valts ovan: Använd det här alternativet om du vill använda förifyllningstjänsten för interaktiv kommunikation som definieras i listrutan Använd interaktiv kommunikation.
   * **** Attributmappning för begäran: Använd avsnittet Mappning av attribut för begäran för att definiera [namn och värde för attributet](../../forms/using/work-with-form-data-model.md#bindargument)request. Hämta informationen från datakällan baserat på attributnamnet och värdet som anges i begäran. Du kan definiera ett attributvärde för begäran med hjälp av ett literalt värde eller en variabel av datatypen String.\
      Alternativen för förifyllningstjänst och attributmappning för begäran är bara tillgängliga om du väljer Interactive Communication Agent UI eller Interactive Communication Web Channel Document i listrutan Typ.

* **** Skickade uppgifter: Följande fält i listan nedan fungerar som utdataplatser för uppgiften:

   * **** Spara utdatafilen med: Spara datafilen (.json,). xml, .doc eller formulärdatamodell). Datafilen innehåller information som skickas via det associerade formuläret. Du kan spara utdatafilen med en sökväg som är relativ till nyttolasten eller lagra den i en variabel av datatypen Document, XML eller JSON. Exempel: [Payload_Directory]/Workflow/data, där data är en fil.
   * **** Spara bilagor med: Spara formulärbilagorna som ingår i en uppgift. Du kan spara de bifogade filerna med en sökväg som är relativ till nyttolasten eller lagra den i en variabel av dokumentdatatypen.
   * **** Spara postdokument med: Sökväg för att spara en postdokumentfil. Exempel: [Payload_Directory]/DocumentofRecord/credit-card.pdf. Du kan spara postdokumentet med en sökväg som är relativ till nyttolasten eller lagra det i en variabel av dokumentdatatypen. Om du väljer alternativet **Relativt till nyttolast** , genereras inte postdokumentet om sökvägsfältet lämnas tomt. Det här alternativet är bara tillgängligt om du väljer Adaptivt formulär i listrutan Typ.

   * **** Spara webbkanalsdata med: Spara webbkanalsdatafilen med en sökväg som är relativ till nyttolasten eller lagra den i en variabel av datatypen Document, JSON eller Form Data Model. Det här alternativet är bara tillgängligt om du väljer gränssnittet för interaktiv kommunikationsagent i listrutan Typ.
   * **** Spara PDF-dokument med: Spara PDF-dokumentet med en sökväg som är relativ till nyttolasten eller lagra det i en variabel av dokumentdatatypen. Det här alternativet är bara tillgängligt om du väljer gränssnittet för interaktiv kommunikationsagent i listrutan Typ.
   * **** Spara layoutmall med: Spara layoutmallen med en sökväg som är relativ till nyttolasten eller lagra den i en variabel av dokumentdatatypen. Layoutmallen [](../../forms/using/layout-design-details.md) refererar till en XDP-fil som du skapar med Forms Designer. Det här alternativet är bara tillgängligt om du väljer gränssnittet för interaktiv kommunikationsagent i listrutan Typ.

* **** Tilldelning > Tilldelningsalternativ: Ange vilken metod som ska användas för att tilldela en användare uppgiften. Du kan dynamiskt tilldela uppgiften till en användare eller grupp med skriptet för deltagarväljaren eller tilldela uppgiften till en viss AEM-användare eller grupp.
* **** Väljare: Alternativet är tillgängligt när alternativet **Dynamiskt för en användare eller grupp** är markerat i fältet Tilldela alternativ. Du kan använda ett ECMAScript eller en tjänst för att dynamiskt välja en användare eller grupp. Mer information finns i Tilldela användare [ett arbetsflöde](https://helpx.adobe.com/experience-manager/kb/HowToAssignAWorkflowDynamicallyToParticipants.html) dynamiskt och [Skapa ett anpassat Adobe Experience Manager Dynamic Participant-steg.](https://helpx.adobe.com/experience-manager/using/dynamic-steps.html)

* **** Deltagare: Fältet är tillgängligt när alternativet **[!UICONTROL com.adobe.granite.workflow.core.process.RandomParticipantChooser]** är markerat i fältet **Deltagare** . I fältet kan du välja användare eller grupper för alternativet RandomParticipantChooser.

* **** Uppdragare: Fältet är tillgängligt när **[!UICONTROL com.adobe.fd.workspace.step.service.VariableParticipantChooser]** har valts i fältet **Deltagarväljare** . I fältet kan du välja en variabel av datatypen String för att definiera den som tilldelas.

* **** Argument: Fältet är tillgängligt när ett annat skript än skriptet RandomParticipantChoose har valts i fältet för deltagarväljare. I fältet kan du ange en lista med kommaavgränsade argument för det skript som valts i fältet Deltagare.

* **** Användare eller grupp: Uppgiften tilldelas den valda användaren eller gruppen. Alternativet är tillgängligt när alternativet **** Till en viss användare eller grupp är markerat i fältet **Tilldelningsalternativ** . I fältet visas alla användare och grupper i gruppen för arbetsflödesanvändare.\
   I listrutan **Användare eller Grupp** visas de användare och grupper som den inloggade användaren har åtkomst till. Hur användarnamn visas beror på om du har åtkomstbehörighet till **användarnoden** i crx-databasen för den aktuella användaren.

* **** Meddela den tilldelade via e-post: Välj det här alternativet om du vill skicka e-postmeddelanden till den tilldelade personen. Dessa meddelanden skickas när en uppgift tilldelas en användare. Aktivera meddelanden från AEM Web Console innan du använder alternativet. Stegvisa instruktioner finns i [Konfigurera e-postmeddelanden för tilldelningssteget](../../forms/using/aem-forms-workflow.md)

* **HTML-e-postmall**: Välj e-postmall för e-postmeddelandet. Om du vill redigera en mall ändrar du filen på /libs/fd/dashboard/templates/email/htmlEmailTemplate.txt i crx-databasen.
* **** Tillåt delegering till: I AEM Inbox finns ett alternativ för den inloggade användaren att delegera det tilldelade arbetsflödet till en annan användare. Du får delegera inom samma grupp eller till arbetsflödesanvändaren i en annan grupp. Om uppgiften har tilldelats en enskild användare och alternativet **Tillåt delegering till medlemmar i den tilldelade gruppen** har valts, går det inte att delegera uppgiften till en annan användare eller grupp.
* **** Delningsinställningar: I AEM Inbox finns alternativ för att dela en enstaka eller alla uppgifter i inkorgen med andra användare:
   * När alternativet **Tillåt att tilldelad delar explicit i inkorgen** är markerat kan användaren klicka på uppgiften och dela den med en annan AEM-användare.
   * När alternativet **Tillåt att tilldelad kan dela via** delning av inkorgen är markerat och en användare delar sina inkorgsobjekt eller tillåter andra användare att komma åt sina inkorgsobjekt, delas endast uppgifter med andra användare som har det här alternativet aktiverat.

* **** Åtgärder > Standardåtgärder: Det finns färdiga funktioner för att skicka, spara och återställa. Som standard är alla standardåtgärder aktiverade.
* **** Flödesvariabel: Namn på flödesvariabeln. Vägvariabeln hämtar anpassade åtgärder som en användare väljer i AEM Inbox.
* **** Vägar: En aktivitet kan förgrena till olika vägar. När det här alternativet har valts i AEM Inbox returnerar flödet ett värde och arbetsflödesgrenarna baserat på den valda vägen. Du kan antingen lagra flöden i en variabel av datatypen String eller välja **Literal** om du vill lägga till vägar manuellt.

* **Titel**: Ange ruttens titel. Den visas i AEM Inbox.
* **Korallikon**: Ange HTML-attribut för en korallikon. Adobe CorelUI-biblioteket innehåller en mängd ikoner som sätter fokus först. Du kan välja och använda en ikon för rutten. Den visas tillsammans med titeln i AEM Inbox. Om du lagrar rutterna i en variabel använder rutterna en taggikon.
* **Tillåt att den som tilldelats kan lägga till kommentarer**: Välj det här alternativet om du vill aktivera kommentarer för uppgiften. En tilldelad kan lägga till kommentarerna inifrån AEM Inbox när uppgiften skickas.
* **** Spara kommentar i variabel: Spara kommentaren i en variabel av datatypen String. Det här alternativet visas bara om du markerar kryssrutan **Tillåt att den som tilldelas kan lägga till kommentarer** .

* **Tillåt att den som tilldelas kan lägga till bilagor till uppgiften**: Välj det här alternativet om du vill aktivera bilagor för uppgiften. En tilldelad kan lägga till de bifogade filerna inifrån AEM Inbox när uppgiften skickas.
* **Spara bifogade utdatauppgifter med**: Ange platsen för den bifogade mappen. Du kan spara bilagor för utdatauppgifter med en sökväg som är relativ till nyttolasten eller med en variabel av dokumentdatatypen. Det här alternativet visas bara om du markerar kryssrutan **Tillåt att den som tilldelas kan lägga till bifogade filer i uppgiften** och väljer **Adaptiv form**, **Skrivskyddat anpassat formulär** eller **Icke-interaktivt PDF-dokument** i listrutan **Typ** **** på fliken¥Form/Document¥.

>[!NOTE]
>
>Använd fliken Bifogade filer i agentanvändargränssnittet under körning för att koppla de bifogade filerna till en interaktiv kommunikation. De associerade bifogade filerna visas som bifogade uppgifter i sidosparken när arbetsobjektet har öppnats i ett fullständigt läge.

* **** Använd anpassade metadata: Välj det här alternativet om du vill aktivera det anpassade metadatafältet. Anpassade metadata används i e-postmallar.
* **** Anpassade metadata: Välj anpassade metadata för e-postmallarna. Anpassade metadata är tillgängliga i crx-databaser på apparna/fd/dashboard/scripts/metadataScripts. Den angivna sökvägen finns inte i crx-databasen. En administratör skapar sökvägen innan den används. Du kan också använda en tjänst för anpassade metadata. Du kan också utöka gränssnittet WorkitemUserMetadataService för att tillhandahålla anpassade metadata.
* **Visa data från föregående steg**: Välj det här alternativet om du vill att tilldelningar ska kunna visa tidigare tilldelningar, åtgärder som redan har vidtagits för uppgiften, kommentarer som har lagts till i uppgiften och dokument med information om den slutförda uppgiften, om tillgängligt.
* **** Visa data från efterföljande steg: Välj det här alternativet om du vill att den som är tilldelad ska kunna visa den åtgärd som har vidtagits och de kommentarer som har lagts till i uppgiften av efterföljande tilldelningar. Den aktuella personen kan även visa ett dokument med uppgifter om den slutförda uppgiften, om det är tillgängligt.
* **** Synlighet för datatyp: Som standard kan en tilldelad visa ett dokument för registrering, tilldelningar, åtgärd och kommentarer som tidigare och efterföljande tilldelningar har lagt till. Använd datatypsalternativet för synlighet för att begränsa vilken typ av data som är synlig för de tilldelade.

## Skicka e-poststeg {#send-email-step}

Använd e-poststeget för att skicka ett e-postmeddelande, till exempel ett e-postmeddelande med ett arkivdokument, en länk till ett anpassat formulär, en länk till en interaktiv kommunikation eller med ett bifogat PDF-dokument. Steget Skicka e-post stöder [HTML-e-post](https://en.wikipedia.org/wiki/HTML_email). HTML-e-post är responsiva och anpassar sig efter mottagarnas e-postklient och skärmstorlek. Du kan använda en HTML-e-postmall för att definiera utseendet, färgschemat och beteendet för e-postmeddelandet.

I e-poststeget används Day CQ Mail Service för att skicka e-post. Kontrollera att [e-posttjänsten](../../forms/using/aem-forms-workflow.md) är konfigurerad innan du använder e-poststeget. E-poststeget har följande egenskaper:

**** Titel: Stegen är en titel som hjälper dig att identifiera steget i arbetsflödesredigeraren.

**** Beskrivning: Förklaring är användbar för andra processutvecklare när du arbetar i en delad utvecklingsmiljö.

**** Ämne: Ämne kan hämtas från ett arbetsflödes metadata, anges manuellt eller hämtas från värdet som lagras i en variabel. Välj bland följande alternativ:

* **Literal -** Ange ett ämne manuellt.
* **Hämta från arbetsflödesmetadata** - Hämta ämnet från en metadataegenskap.
* **Variabel** - Hämta ämnet från värdet som lagras i en variabel av strängdatatyp.

**HTML-e-postmall**: HTML-mall för e-postmeddelandet. Du kan ange variabler i en e-postmall. E-poststeget extraheras och visar alla variabler som ingår i en mall för indata.

**** Metadata för e-postmall: Värdet för e-postmallvariablerna kan vara ett användarspecificerat värde, sökvägen till en resurs på författaren eller på publiceringsservern, bilden eller en metadataegenskap för arbetsflödet.

* **** Literal: Använd alternativet när du vet exakt vilket värde du ska ange. Till exempel [example@example.com](mailto:example@example.com).

* **** Metadata för arbetsflöde: Använd alternativet när värdet som ska användas sparas i en arbetsflödets metadataegenskap. När du har valt alternativet anger du metadataegenskapens namn i den tomma textrutan under alternativet Metadata för arbetsflöde. Till exempel emailAddress.
* **** Resurs-URL: Använd alternativet för att bädda in en webblänk av en interaktiv kommunikation i e-postmeddelandet. När du har valt alternativet bläddrar du och väljer den interaktiva kommunikation som ska bäddas in. Resursen kan finnas på författaren eller på publiceringsservern.
* **** Bild: Använd alternativet för att bädda in en bild i e-postmeddelandet. När du har valt alternativet bläddrar du och väljer bilden. Bildalternativet är bara tillgängligt för de bildtaggar (&lt;img src=&quot;*&quot;/>) som är tillgängliga i e-postmallen.

**** Avsändarens/mottagarens e-postadress: Välj alternativet **Litteral** om du vill ange en e-postadress manuellt eller markera alternativet **Hämta från arbetsflödets metadata** om du vill hämta e-postadressen från en metadataegenskap. Du kan också ange en lista med egenskapsvektorer för metadata för **alternativet Hämta från arbetsflödesmetadata** . Välj alternativet **Variabel** om du vill hämta e-postadressen från värdet som lagras i en variabel av strängdatatyp.

**** Bifogad fil: Den tillgängliga resursen på den angivna platsen är kopplad till e-postmeddelandet. Resursens sökväg kan vara relativ till nyttolasten eller den absoluta sökvägen. En exempelsökväg är [Payload_Directory]/attachments/.

Välj alternativet **Variabel** om du vill hämta den bifogade filen som lagras i en variabel av datatypen Document, XML eller JSON.

**** Filnamn: Namn på e-postbilagefilen. E-poststeget ändrar det ursprungliga filnamnet för den bifogade filen till det angivna filnamnet. Namnet kan anges manuellt eller hämtas från en metadataegenskap eller variabel i arbetsflödet. Använd alternativet **Literal** när du vet exakt vilket värde du ska ange. Använd alternativet **Variabel** för att hämta filnamnet från värdet som lagras i en variabel av strängdatatyp. Använd alternativet **Hämta från arbetsflödesmetadata** när värdet som ska användas sparas i en metadataegenskap för arbetsflöde.

## Generera dokumentarkivhandlingssteget {#generate-document-of-record-step}

När ett formulär fylls i eller skickas kan du spara en post med formuläret, i utskrift eller i dokumentformat. Detta kallas DOS (Document of Record). Du kan använda steget Skapa dokument för post för att skapa en skrivskyddad eller interaktiv PDF-version av ett anpassat formulär. PDF-versionen innehåller information som är ifylld i formuläret tillsammans med layouten för det adaptiva formuläret.

Dokumentsteget har följande egenskaper:

**Använd adaptiv form**: Ange den metod som ska användas för att hitta indataadaptiva formulär. Du kan använda det adaptiva formuläret som skickas till arbetsflödet, som finns på en absolut sökväg eller som finns på en sökväg i en variabel. Du kan använda en variabel av datatypen String för att ange sökvägen i variabeln **Select som ska tolkas** i fältet.\
Du kan koppla flera adaptiva formulär till ett arbetsflöde. Det innebär att du kan ange ett anpassningsbart formulär i körningsmiljön med hjälp av de tillgängliga indatametoderna.

**Adaptiv formulärsökväg**: Ange sökvägen för det adaptiva formuläret. Fältet är tillgängligt när du väljer alternativet **Tillgängligt med en absolut sökväg** i fältet **Använd anpassat formulär** .

**** Välj Indata med: Sökväg till indata för det adaptiva formuläret. Du kan behålla data på en plats i förhållande till nyttolasten, ange en absolut sökväg till data eller hämta data som lagras i en variabel av datatypen Document, JSON eller XML. Indata sammanfogas med det adaptiva formuläret för att skapa ett postdokument.

**** Välj sökväg för indatabilaga med: Sökväg till de bifogade filerna. De här bifogade filerna ingår i dokumentdokumentet. Du kan behålla de bifogade filerna på en plats i förhållande till nyttolasten, ange en absolut sökväg för de bifogade filerna eller hämta bifogade filer som lagras i en variabel av dokumentdatatypen.

Om du anger sökvägen till en mapp, till exempel bilagor, bifogas alla filer som är direkt tillgängliga i mappen till Dokument för post. Om det finns filer i de mappar som är direkt tillgängliga i den angivna sökvägen inkluderas filerna i Postdokument som bilagor. Om det finns mappar i direkt tillgängliga mappar hoppas de över.

**** Spara genererat postdokument med följande alternativ: Ange platsen där ett dokument med en postfil ska sparas. Du kan välja att skriva över nyttolastmappen, placera postdokumentet på en plats i nyttolastkatalogen eller lagra postdokumentet i en variabel av dokumentdatatypen.

**Språk**: Ange språk för postdokumentet. Välj **Litteral** för att välja språkområde från en nedrullningsbar lista eller välj **Variabel** för att hämta språkområdet från det värde som lagras i en variabel av strängdatatyp. Du måste definiera språkkoden medan du lagrar värdet för språkinställningen i en variabel. Ange till exempel **en_US** för engelska och **fr_FR** för franska.

## Anropa tjänststeg för formulärdatamodell {#invoke-form-data-model-service-step}

Du kan använda [AEM Forms-dataintegrering](../../forms/using/data-integration.md) för att konfigurera och ansluta till olika datakällor. Dessa datakällor kan vara en databas-, webbtjänst-, REST-tjänst-, OData-tjänst- och CRM-lösning. Med dataintegrering i AEM Forms kan du skapa en formulärdatamodell som omfattar olika tjänster som utför datahämtnings-, additions- och uppdateringsåtgärder för den konfigurerade databasen. Du kan använda steget **** Anropa datamodelltjänst för att välja en formulärdatamodell (FDM) och använda tjänsterna i FDM för att hämta, uppdatera eller lägga till data till olika datakällor.

Följande databastabell och JSON-filen används som exempel för att förklara indata för stegfält:

**Exempel på kundinformationsregister**

<table>
 <tbody> 
  <tr> 
   <td>Egenskap</td> 
   <td>Värde<br /> </td> 
  </tr> 
  <tr> 
   <td>FirstName<br /> </td> 
   <td>Sarah<br /> </td> 
  </tr> 
  <tr> 
   <td>LastName</td> 
   <td>ros</td> 
  </tr> 
  <tr> 
   <td>Kund-ID</td> 
   <td>1</td> 
  </tr> 
  <tr> 
   <td>E-postadress<br /> </td> 
   <td>srose@we.info</td> 
  </tr> 
 </tbody> 
</table>

**JSON-exempelfil**

```
{ 
  customer: { 
   firstName: "Sarah", 
   lastName:"Rose", 
   customerId: "1", 
   emailAddress:"srose@we.info" 
 }, 
  insurance: {
   customerId: "1", 
  policyType: "Premium,
  policyNumber: "Premium-521499",
  customerDetails: { 
   firstName: "Sarah",
   lastName: "Rose",
   customerId: "1",
   emailAddress: "srose@we.info" 
  }
 }
}
```

I steget Anropa formulärdatamodelltjänst visas följande fält för att underlätta formulärdatamodellåtgärder:

* **** Titel: Stegets namn. Det hjälper till att identifiera steget i arbetsflödesredigeraren.
* **** Beskrivning: Förklaring är användbar för andra processutvecklare när du arbetar i en delad utvecklingsmiljö.

* **Sökväg till** formulärdatamodell: Bläddra och välj en formulärdatamodell som finns på servern.

* **Tjänst**: Lista över tjänster som den valda formulärdatamodellen tillhandahåller.
* **Indata för tjänster > Ange indata med hjälp av litteral-, variabel- eller arbetsflödesmetadata och en JSON-fil**: En tjänst kan ha flera argument. Välj alternativet för att hämta värdet för tjänstargumenten från en metadataegenskap för arbetsflöde, ett JSON-objekt, en variabel eller ange värdet direkt i textrutan:

   * **** Literal: Använd alternativet när du vet exakt vilket värde du ska ange. Exempel: srose@we.info.
   * **** Variabel: Använd alternativet för att hämta värdet som lagras i en variabel.
   * **** Hämta från arbetsflödesmetadata: Använd alternativet när värdet som ska användas sparas i en arbetsflödets metadataegenskap. Till exempel emailAddress.
   * **** JSON-punktnotation: Använd alternativet när värdet som ska användas finns i en JSON-fil. Till exempel försäkring.customerDetails.emailAddress. Alternativet JSON-punktnotation är bara tillgängligt om du har valt alternativet Mappa inmatningsfält från JSON-inmatningsalternativet.
   * **** Mappa indatafält från JSON-indata: Ange sökvägen till en JSON-fil för att hämta indatavärdet för vissa tjänstargument från JSON-filen. Sökvägen till JSON-filen kan vara relativ till nyttolasten, en absolut sökväg eller så kan du välja ett JSON-inmatningsdokument med hjälp av variabeln JSON eller Form Data Model.

* **** Indata för tjänster > Ange indata med hjälp av variabel eller en JSON-fil: Välj alternativet om du vill hämta värden för alla argument från en JSON-fil som har sparats med en absolut sökväg, med en sökväg som är relativ till nyttolasten eller i en variabel.
* **Välj Indata-JSON-dokument med**: JSON-filen innehåller värden för alla tjänstargument. JSON-filens sökväg kan vara **relativ till nyttolasten** eller en **absolut sökväg.** Du kan även hämta JSON-indata-dokumentet med hjälp av en variabel av datatypen JSON eller Form Data Model.

* **** JSON-punktnotation: Lämna fältet tomt om du vill använda alla objekt i den angivna JSON-filen som indata för tjänstargument. Om du vill läsa ett specifikt JSON-objekt från den angivna JSON-filen som indata för serviceargument anger du punktnotation för JSON-objektet, till exempel, om du har en JSON som liknar den som anges i början av avsnittet, anger du försäkring.customerDetails för att ge all information om en kund som indata till tjänsten.
* **** Utdata för tjänsten > Mappa och skriv utdatavärden till variabel eller metadata: Välj alternativet att spara utdatavärdena som egenskaper för arbetsflödesinstansens metadatanod i crx-databasen. Ange namnet på metadataegenskapen och välj det motsvarande tjänstutdataattribut som ska mappas med metadataegenskapen, till exempel mappa det telefonnummer som returneras av utdatatjänsten med egenskapen phone_number för arbetsflödets metadata. På samma sätt kan du lagra utdata i en variabel med datatypen Long.
* **** Utdata från tjänst > Spara utdata till variabel eller en JSON-fil: Välj alternativet att spara utdatavärdena i en JSON-fil med en absolut sökväg, med en sökväg som är relativ till nyttolasten eller i en variabel.
* **** Spara JSON-utdatadokument med alternativen nedan: Spara JSON-utdatafilen. Sökvägen till JSON-utdatafilen kan vara relativ till nyttolasten eller en absolut sökväg. Du kan också spara JSON-utdatafilen med en variabel av datatypen JSON eller Form Data Model.

## Underteckna dokumentsteg {#sign-document-step}

I steget Signera dokument kan du använda Adobe Sign för att signera dokument. Stegen Signera dokument har följande egenskaper:

* **** Avtalsnamn: Ange avtalets namn. Avtalsnamnet blir en del av ämnet och brödtexten i det e-postmeddelande som skickas till signerarna. Du kan antingen lagra namnet i en variabel av datatypen String eller välja **Literal** om du vill lägga till namnet manuellt.

* **** Språk: Ange språk för alternativen för e-post och verifiering. Du kan antingen lagra språkinställningen i en variabel av datatypen String eller välja **Literal** för att välja språkinställningen i listan med tillgängliga alternativ. Du måste definiera språkkoden medan du lagrar värdet för språkinställningen i en variabel. Ange till exempel **en_US** för engelska och **fr_FR** för franska.

* **Adobe Sign Cloud-konfiguration**: Välj en Adobe Sign Cloud-konfiguration. Om du inte har konfigurerat Adobe Sign för AEM-formulär läser du [Integrera Adobe Sign med AEM-formulär](../../forms/using/adobe-sign-integration-adaptive-forms.md).

* **** Välj dokument som ska signeras med: Du kan välja ett dokument från en plats som är relativ till nyttolasten, använda nyttolasten som dokument, ange en absolut sökväg för dokumentet eller hämta dokumentet som lagras i en variabel av dokumentdatatypen.
* **** Dagar till deadline: Ett dokument markeras som förfallodatum (passerad deadline) efter det att ingen aktivitet har gjorts i aktiviteten för det antal dagar som anges i fältet **Dagar till deadline** . Antalet dagar räknas efter att den dokumenterade har tilldelats en användare för signering.
* **** E-postfrekvens för påminnelse: Du kan skicka en påminnelse via e-post varje dag eller vecka. Veckan räknas från den dag som den dokumenterade tilldelas en användare för signering.
* **** Underskriftsprocess: Du kan välja att signera ett dokument i en sekventiell eller parallell ordning. I sekventiell ordning tar en signerare emot dokumentet i taget för signering. När den första signeraren har slutfört signeringen av dokumentet skickas dokumentet till den andra signeraren och så vidare. Flera signerare kan signera ett dokument samtidigt i parallell ordning.
* **** URL för omdirigering: Ange en URL för omdirigering. När dokumentet har signerats kan du dirigera om den som tilldelats till en URL. Oftast innehåller denna URL ett tackmeddelande eller ytterligare instruktioner.
* **** Arbetsflödesfas: Ett arbetsflöde kan ha flera steg. Dessa steg visas i AEM Inbox. Du kan definiera de här stegen i modellens egenskaper (Sidspark > Sida > Sidegenskaper > Steg).
* **** Välj signerare: Ange metoden för att välja signerare för dokumentet. Du kan dynamiskt tilldela arbetsflödet till en användare eller en grupp eller manuellt lägga till information om en signerare.
* **** Skript eller tjänst för att välja signerare: Alternativet är bara tillgängligt om alternativet Dynamiskt är markerat i fältet Välj signerare. Du kan ange ett ECMAScript eller en tjänst för att välja signerare och verifieringsalternativ för ett dokument.
* **** Signerarinformation: Alternativet är bara tillgängligt om alternativet Manuellt är markerat i fältet Välj signerare. Ange e-postadress och välj en valfri verifieringsmekanism. Innan du väljer en verifieringsmekanism i två steg ska du kontrollera att motsvarande verifieringsalternativ är aktiverat för det konfigurerade Adobe Sign-kontot. Du kan använda en variabel av datatypen String för att definiera värden för fälten **[!UICONTROL E-post]**, **[!UICONTROL Landskod]** och **[!UICONTROL Telefonnummer]** . Fälten **[!UICONTROL Landskod]** och **[!UICONTROL Telefonnummer]** visas endast om du väljer **[!UICONTROL Telefonverifiering]** i den **[!UICONTROL 2-stegsvisa]** verifieringslistan.
* **** Statusvariabel: Ett Adobe Sign-aktiverat dokument lagrar dokumentets signeringsstatus i en variabel av datatypen String. Ange namnet på statusvariabeln (adobeSignStatus). En statusvariabel för en instans finns i CRXDE på /etc/workflow/instances/&lt;server>/&lt;datum-tid>/&lt;instans av arbetsflödesmodell>/workItems/&lt;nod>/metaData innehåller status för en variabel.
* **** Spara signerat dokument med följande alternativ: Ange platsen där signerade dokument ska sparas. Du kan välja att skriva över nyttolastfilen, placera det signerade dokumentet på en plats i nyttolastkatalogen eller lagra det signerade dokumentet i en variabel av Dokumenttyp.

## Steg för Document Services {#document-services-steps}

AEM Document Services är en uppsättning tjänster för att skapa, sammanställa och skydda PDF-dokument. AEM Forms tillhandahåller ett separat AEM Workflow-steg för varje dokumenttjänst.

På samma sätt som andra arbetsflödessteg i AEM Forms, till exempel Tilldela uppgift, Skicka e-post och Signera dokument, kan du använda variabler i alla steg i AEM Document Services. Mer information om att skapa och hantera variabler finns i [Variabler i AEM-arbetsflöden](../../forms/using/variable-in-aem-workflows.md).

### Använd tidsstämpelsteg för dokument {#apply-document-time-stamp-step}

Lägg till tidsstämpel i ett dokument. Du kan ange dokumentinformation, t.ex. indatadokumentsökväg, indatadokumentnamn och plats där exporterade data ska lagras. Du kan välja att skriva över en befintlig nyttolastfil, välja ett annat filnamn för att lagra data i en annan fil under nyttolastmappen, ange en absolut sökväg till data eller lagra data i en variabel av dokumentdatatypen.

### Konvertera till bildsteg {#convert-to-image-step}

Konverterar ett PDF-dokument till en lista med bilder. Bildformat som stöds är JPEG, JPEG2000, PNG och TIFF. Följande information gäller för konvertering till TIFF-bilder:

* En TIFF-fil med flera sidor skapas.
* Vissa anteckningar ingår inte i TIFF-bilder. Anteckningar som kräver att Acrobat genererar sitt utseende inkluderas inte.

### Konvertera till PDF/A-steg {#convert-to-pdf-a-step}

Konverterar ett PDF-dokument till PDF/A-format med de angivna alternativen. PDF/A-versionen av PDF (Portable Document Format) är avsedd för arkivering och långtidsarkivering av dokument.

### Konvertera till PS-steg {#convert-to-ps-step}

Konvertera PDF-dokument till PostScript. När du konverterar till PostScript kan du använda konverteringsåtgärden för att ange källdokumentet och om det ska konverteras till PostScript-nivå 2 eller 3. PDF-dokumentet som du konverterar till en PostScript-fil måste vara icke-interaktivt.

### Skapa PDF från angivet textsteg {#create-pdf-from-specified-type-step}

Generera ett PDF-dokument från en indatafil. Indatadokumentet kan vara relativt till nyttolasten, ha en absolut sökväg, vara nyttolasten själv eller lagras i en variabel av datatypen Document.

### Skapa PDF från URL/HTML/ZIP {#create-pdf-from-url-html-zip-step}

Skapar ett PDF-dokument av den angivna URL-, HTML- och ZIP-filen.

### Steget Exportera data {#export-data-step}

Exporterar data från ett PDF-formulär eller en XDP-fil. Du måste ange filsökvägen för Input Document och Export Data Format. Alternativen för Exportera dataformat är Auto, XDP och XmlData.

### Exportera PDF till angivet textsteg {#export-pdf-to-specified-type-step}

Konverterar ett PDF-dokument till ett valt format.

### Generera icke-interaktiv PDF-steg {#generatenoninteractive}

Skapa en icke-interaktiv PDF. Här finns olika anpassningsalternativ.

>[!NOTE]
>
>Du kan använda variabler för att ange mallfilen för indatadokument. Lagra sökvägen till mallfilen i en variabel av datatypen String.

### Importera datasteg {#import-data-step}

Sammanfogar formulärdata till ett PDF-formulär. Du kan importera formulärdata till ett PDF-formulär.

### Anropa DDX-steg {#invokeddx}

Kör DDX-filen på den angivna kartan över indatadokument och returnerar de manipulerade PDF-dokumenten.

>[!NOTE]
>
>Du kan använda variabler för att ange DDX-filen för indatadokument. Lagra DDX-filen i en variabel av dokumentdatatypen eller XML-datatypen.

### Optimera PDF-steget {#optimize-pdf-step}

Optimerar PDF-filer genom att minska deras storlek. Resultatet av konverteringen är PDF-filer som kan vara mindre än originalversionerna. Den här åtgärden konverterar även PDF-dokument till den PDF-version som anges i optimeringsparametrarna.

Optimeringsinställningarna anger hur filerna optimeras. Här följer några exempelinställningar:

* Målversion för PDF
* Ignorera objekt som JavaScript-åtgärder och inbäddade sidminiatyrer
* Ignorera användardata som kommentarer och bifogade filer
* Ignorerar ogiltiga eller oanvända inställningar
* Komprimera okomprimerade data eller använda mer effektiva komprimeringsalgoritmer
* Ta bort inbäddade teckensnitt
* Ange genomskinlighetsvärden

### Återge PDF-formulär, steg {#renderpdf}

Återger ett formulär som skapats i Form Designer (XDP) till ett PDF-formulär.

>[!NOTE]
>
>Du kan använda variabler för att ange mallfilen för indatadokument. Lagra sökvägen till mallfilen i en variabel av datatypen String.

### Säkra dokument, steg {#secure-document-step}

Kryptera, signera och certifiera ett dokument. AEM Forms stöder både lösenordsbaserad och certifikatbaserad kryptering. Du kan också välja mellan olika algoritmer för signering av dokument. Exempel: SHA-256 och SH-512. Du kan också använda arbetsflödessteget för att läsa utökade PDF-dokument. Arbetsflödessteget innehåller alternativ för att aktivera streckkodsavkodning, digitala signaturer, import och export av PDF-data och andra alternativ.

### Skicka till skrivare, steg {#send-to-printer-step}

Skicka ett dokument direkt till en skrivare. Det har stöd för följande åtkomstmekanismer för utskrift:

* **Direkttillgänglig skrivare**: En skrivare som är installerad på samma dator kallas för en skrivare med direktåtkomst och datorn kallas för skrivarvärd. Den här typen av skrivare kan vara en lokal skrivare som är ansluten direkt till datorn.
* **Indirekt tillgänglig skrivare**: Skrivaren som är installerad på en utskriftsserver är tillgänglig från andra datorer. Teknik som det gemensamma utskriftssystemet UNIX® (CUPS) och protokollet Line Printer Daemon (LPD) är tillgängliga för anslutning till en nätverksskrivare. Om du vill få åtkomst till en indirekt tillgänglig skrivare anger du utskriftsserverns IP-adress eller värdnamn. Med den här funktionen kan du skicka ett dokument till en LPD-URI när nätverket har ett LPD-program öppet. Med hjälp av den här funktionen kan du dirigera dokumentet till en skrivare som är ansluten till nätverket som har ett LPD-program öppet.

