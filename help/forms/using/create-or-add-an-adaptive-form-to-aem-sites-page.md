---
title: Skapa eller lägga till ett anpassat formulär på AEM Sites-sidan
description: Upptäck hur du enkelt kan skapa och lägga till anpassade formulär på din AEM Sites-sida. Lär dig stegvisa tekniker och metodtips för att integrera dynamiska och anpassningsbara formulär på er webbplats och optimera era era digitala upplevelser för maximal effekt.
feature: Adaptive Forms
source-git-commit: 8f2c8964c2a6c2f0fcb446b7bca1f8cb822906f7
workflow-type: tm+mt
source-wordcount: '2810'
ht-degree: 0%

---


# Skapa eller lägga till ett anpassat formulär på AEM Sites-sidan {#create-or-add-an-adaptive-form-to-aem-sites-page}

Med AEM Forms kan du smidigt lägga in anpassningsbara formulär på webbsidorna. På så sätt kan besökarna enkelt fylla i och skicka in formulär utan att lämna den sida de är på. På så sätt kan de enkelt hålla kontakten med andra element på webbplatsen samtidigt som de interagerar aktivt med formuläret.

Du kan använda AEM Page Editor för att snabbt skapa och lägga till flera formulär på dina AEM Sites-sidor. Med AEM Page Editor kan skribenter skapa smidiga datainhämtningsupplevelser på en webbplatssida med hjälp av kraften i adaptiva formulärkomponenter som dynamiskt beteende, validering, dataintegrering, generering av dokument för automatisering av register och affärsprocesser. Det gör det även möjligt att använda olika funktioner på AEM Sites-sidor, som versionshantering, målgruppsanpassning, översättning och hantering av flera webbplatser.

AEM Forms har adaptiv formulärbehållare och adaptiv Forms - inbäddningskomponenter. Du kan använda adaptiv formulärbehållare för att skapa ett nytt formulär på en Experience Fragment- eller AEM Sites-sida, medan adaptiv Forms - Embed-komponent gör att du kan lägga till ett befintligt adaptivt formulär eller skapa ett nytt formulär med Adaptiv Forms Editor.

![](/help/forms/using/assets/adaptive-form-in-sites-page.png)

## Fördelar med att använda komponenten Adaptiv formulärbehållare i AEM Page Editor eller Experience Fragment

Med hjälp av adaptiv formulärbehållare AEM sidredigeraren kan du skapa sömlösa datainhämtningsupplevelser på en sajtsida med hjälp av kraften i adaptiva Forms-komponenter, inklusive dynamiskt beteende, validering, dataintegrering, generering av dokument för post- och affärsprocessautomatisering. Man kan också använda olika funktioner på AEM Sites-sidor, som versionshantering, målgruppsanpassning, översättning och hantering av flera webbplatser, vilket förbättrar den övergripande upplevelsen av att skapa och hantera formulär. Låt oss utforska några av dessa funktioner:

* **Versionshantering:** Erbjudande om AEM Sites-sidor [robust versionshantering](/help/sites-authoring/working-with-page-versions.md), så att du kan spåra och hantera olika versioner av formulären. På så sätt kan du göra ändringar och förbättringar i formulär samtidigt som du behåller möjligheten att vid behov gå tillbaka till tidigare versioner. Versionshantering säkerställer ett kontrollerat och organiserat tillvägagångssätt för blankettutveckling och -utveckling.
* **Målinriktning (integrering med Adobe Target):** Med målgruppsfunktionerna i AEM Sites kan man också [personalisera formulärupplevelsen för olika målgrupper](/help/sites-administering/target.md). Genom att utnyttja användarsegment och kriterier för målinriktning kan du skräddarsy formulärets innehåll, design eller beteende för specifika användargrupper. På så sätt kan ni leverera en personaliserad och relevant formulärupplevelse, vilket ökar engagemanget och konverteringsgraden.
* **Översättning:** AEM Sites [smidig integrering med översättningstjänster](/help/sites-administering/translation.md)så att du enkelt kan översätta formulär till flera språk. Den här funktionen förenklar lokaliseringsprocessen och säkerställer att formulären är tillgängliga för en global publik. Ni kan hantera översättningar effektivt i AEM översättningsprojekt, vilket minskar den tid och det arbete som krävs för stöd av flerspråkiga formulär. Mer information om översättning finns i avsnittet med överväganden.
* **Hantering av flera webbplatser och Live Copy:** AEM Sites ger robusta [Funktioner för hantering av flera webbplatser och Live Copy](/help/sites-administering/msm.md), vilket gör att du kan skapa och hantera flera webbplatser i en och samma miljö. Med den här funktionen kan du nu återanvända formulär på olika webbplatser, vilket ger enhetlighet och minskar dubbelarbetet. Med centraliserad kontroll och hantering kan ni effektivt hantera och uppdatera formulär på flera webbplatser.
* **Teman:** På AEM Sites sidor finns ett ramverk för att utforma och underhålla enhetliga visuella format för flera webbsidor. Dessa definierar färger, teckensnitt, formatmallar och andra visuella element som bidrar till webbplatsens allmänna utseende och känsla. [Du kan använda teman som är utformade för en AEM Sites-sida för ett adaptivt formulär, vilket sparar både tid och arbete](/help/sites-authoring/style-system.md).
* **Taggning:** På AEM Sites sidor kan du [tilldela taggar eller etiketter till en sida, en resurs eller annat innehåll](/help/sites-authoring/tags.md). Taggar är nyckelord eller metadataetiketter som gör det möjligt att kategorisera och ordna innehåll baserat på specifika kriterier. Du kan tilldela en eller flera taggar till sidor, resurser eller andra innehållsobjekt i AEM för att förbättra sökningen och kategorisera resurserna.
* **Låsa och låsa upp innehåll:** AEM Sites tillåter användare att [styra åtkomst till och ändringar av sidor](/help/sites-authoring/editing-content.md#locking-a-page-locking-a-page) i AEM Sites. När en sida är låst innebär det att den skyddas från obehöriga ändringar och redigeringar av andra användare. Endast den användare som har låst innehållet eller en utsedd administratör kan låsa upp det för att tillåta ändringar.


## Olika alternativ för att lägga till ett anpassat formulär AEM sidredigeraren

Du kan utnyttja den här funktionen till fullo genom att använda följande alternativ:

* **Lägg till ett anpassat adaptivt formulär på en AEM Sites-sida:** Skapa ett helt nytt formulär från grunden och skräddarsy det specifikt efter dina behov och designönskemål.

* **Lägg till ett anpassat anpassat formulär i ett Experience Fragments:** Nå ut bättre med formulären genom att lägga till dem i AEM Experience Fragments, vilket möjliggör smidig återanvändning på flera sidor eller webbplatser.

* **Lägga till flera formulär på en AEM Sites-sida eller Experience Fragment:**  Lägg till flera formulär på en sida för att ge användarna olika alternativ beroende på vilka önskemål och önskemål de har. Dessa kan vara en kombination av helt nya formulär från grunden och befintliga formulär.

* **Konvertera ett anpassat formulär till Experience Fragment:** Konvertera ett anpassat formulär som lagts till på en AEM Sites-sida till ett Experience Fragment för återanvändning av formuläret på flera AEM Sites-sidor.

* **Skapa och lägg till formulär baserade på godkända mallar på en AEM Sites-sida:** Använd redan godkända mallar för att snabbt skapa blanketter som är anpassade efter företagets grafiska profil och designstandarder. Alternativet är bara tillgängligt för Adaptiv Forms som har skapats med Adaptiv Forms Editor eller Adaptiv Forms - Bädda in komponent.

* **Lägga till befintliga formulär på en AEM Sites-sida:** Integrera enkelt formulär som du redan har skapat på webbplatserna så att besökarna kan interagera direkt med dem. Alternativet är bara tillgängligt för Adaptiv Forms som har skapats med Adaptiv Forms Editor eller Adaptiv Forms - Bädda in komponent.

## Överväganden {#consideration}

* När du använder den adaptiva formulärbehållaren för att skapa eller lägga till ett formulär, översätts och lokaliseras formulären via AEM Sites översättningsflöde. För varje språk genereras en separat kopia (språkkopia) av webbplatssidan och motsvarande formulär. När en innehållsförfattare ändrar en regel i ett formulär på den överordnade sidan måste samma ändringar göras i alla språkkopior av formuläret. Med adaptiv formulärbehållare kan du även använda olika funktioner på AEM Sites-sidor, som versionshantering, målgruppsanpassning, översättning och hantering av flera webbplatser.

* När du skapar eller lägger till ett formulär med komponenten Adaptiv formulärinbäddning översätts och lokaliseras formulären med hjälp av AEM Forms översättningsflöde. I det här fallet finns det ett enda formulär som du kan referera till på alla språkkopior av webbplatssidorna. Adaptiv Form-embed-komponent ger inte åtkomst till olika funktioner på AEM Sites-sidor som versionshantering, målgruppsanpassning, översättning och hantering av flera webbplatser.


## Innan du börjar {#before-you-start}

+++  Aktivera adaptiva Forms Core-komponenter för din miljö

Se till att [Adaptiva Forms Core-komponenter är aktiverade för din miljö](https://experienceleague.adobe.com/docs/experience-manager-headless-adaptive-forms/using/quick-setup/enable-headless-adaptive-forms-and-core-components.html?lang=en).

+++

+++  Lägg till adaptiva Forms Client Libraries i komponenterna på din AEM Sites-sida och i Experience Fragment-sidan

Om du vill aktivera alla funktioner för den adaptiva Forms-behållarkomponenten lägger du till klientbiblioteken CustomHeaderlibs och CustomFoterlibs på din AEM Sites-sida via distributionsflödet. Så här lägger du till biblioteken:

1. Logga in på din AEM Author-instans och öppna CRX DE. Standardwebbadressen för en Author-instans som körs lokalt är `http://localhost:4502/crx/de`.

1. Öppna `/apps/[your-sites-project]/components/page/customheaderlibs.html` och lägg till följande kod i filen:

       &quot;
       /Customheaderlibs.html
       &lt;sly data-sly-use.clientlib=&quot;core/wcm/components/commons/v1/templates/clientlib.html&quot;>
       &lt;sly data-sly-call=&quot;${clientlib.css @ categories=&amp;#39;core.forms.components.runtime.all&amp;#39;}&quot; />
       &lt;/sly>
       
       &quot;
   
1. Öppna `/apps/[your-sites-project]/components/page/customfooterlibs.html` och lägg till följande kod i filen:

       &quot;
       
       /customfooterlibs.html
       &lt;sly data-sly-use.clientlib=&quot;core/wcm/components/commons/v1/templates/clientlib.html&quot;>
       &lt;sly data-sly-test=&quot;${!wcmmode.edit}&quot; data-sly-call=&quot;${clientlib.js @ categories=&amp;#39;core.forms.components.runtime.all&amp;#39;, async=true}&quot; />
       &lt;/sly>
       &quot;
   
1. Öppna `/apps/[your-sites-project]/components/xfpage/customheaderlibs.html` och lägg till följande kod i filen:

       &quot;
       /Customheaderlibs.html
       &lt;sly data-sly-use.clientlib=&quot;core/wcm/components/commons/v1/templates/clientlib.html&quot;>
       &lt;sly data-sly-call=&quot;${clientlib.css @ categories=&amp;#39;core.forms.components.runtime.all&amp;#39;}&quot; />
       &lt;/sly>
       
       &quot;
   
1. Öppna `/apps/[your-sites-project]/components/customfooterlibs.html` och lägg till följande kod i filen:

       &quot;
       
       /customfooterlibs.html
       &lt;sly data-sly-use.clientlib=&quot;core/wcm/components/commons/v1/templates/clientlib.html&quot;>
       &lt;sly data-sly-test=&quot;${!wcmmode.edit}&quot; data-sly-call=&quot;${clientlib.js @ categories=&amp;#39;core.forms.components.runtime.all&amp;#39;, async=true}&quot; />
       &lt;/sly>
       &quot;
   
1. Upprepa ovanstående steg för alla Author- och Publish-instanser i din miljö.

+++

+++ Aktivera anpassad Forms-behållare

Aktivera [!UICONTROL Adaptive Forms Container] utför följande steg i mallens policy:

1. Öppna AEM Sites eller Experience Fragment för redigering. Om du vill öppna sidan för redigering markerar du sidan och klickar på Redigera.
1. Öppna mallen för webbplatserna eller sidan för Experience Fragment. Öppna mallen genom att gå till [!UICONTROL Page Information] ![Sidinformation](/help/forms/using/assets/Smock_Properties_18_N.svg) > [!UICONTROL Edit Template]. Motsvarande mall öppnas i mallredigeraren.
1. I strukturvyn klickar du på **[!UICONTROL Policy]** ![Policy](/help/forms/using/assets/Smock_FeedManagement_18_N.svg) -ikonen på menyraden. I **[!UICONTROL Allowed Components]** och välj **[!UICONTROL Adaptive Forms Container]**  kryssrutan under **[AEM Archetype Project Name] - Adaptiv form**.
1. Klicka på **[!UICONTROL Done]**.

>[!VIDEO](https://video.tv.adobe.com/v/3419370?quality=12&learn=on)

+++

## Skapa ett adaptivt formulär {#create-an-adaptive-form-in-sites-editor-or-experience-fragment}

Du kan skapa ett helt nytt formulär från grunden och anpassa det specifikt efter dina krav och designönskemål, direkt på en AEM Sites-sida eller i Experience Fragment. För enstaka formulär rekommenderar vi direktredigering till en AEM Sites-sida, medan Experience Fragments är idealiskt för formulär som behöver återanvändas på flera sidor på webbplatsen.

* [Skapa ett formulär på en AEM Sites-sida](#create-an-adaptive-form-in-sites-editor)
* [Skapa ett formulär i ett Experience Fragment](#create-an-adaptive-form-in-experience-fragment)
* [Konvertera ett anpassat formulär på en AEM Sites-sida till ett Experience Fragment](#convert-an-adaptive-form-in-sites-page-to-an-experience-fragment)

### Skapa ett formulär på en AEM Sites-sida {#create-an-adaptive-form-in-sites-editor}

Du kan använda komponenten Adaptiv formulärbehållare AEM sidredigeraren för att skapa ett anpassat formulär. Med komponenten kan du skapa ett formulär genom att dra och släppa formulärkomponenterna. Formulärkomponenterna är baserade på kärnkomponenter. Du kan enkelt anpassa dessa efter organisationens behov.

>[!VIDEO](https://video.tv.adobe.com/v/3419284?quality=12&learn=on)

Så här skapar du ett adaptivt formulär på en webbplatssida:

1. Öppna AEM Sites-sidan i redigeringsläge.
1. Dra och släpp **[!UICONTROL Adaptive Forms Container]** från komponentwebbläsaren till sidan Platser. Det skapar ett blanksteg på sidan för formuläret. Du kan använda layoutläget för att ändra storleken på behållarutrymmet.
1. Dra och släpp adaptiva kärnkomponenter i formulär till behållarutrymmet för att skapa formuläret.
1. Lägg till knappen Skicka.

Nästa [ange åtgärden Skicka](#configure-submit-action-for-form) och avancerade egenskaper.

### Skapa ett formulär i ett Experience Fragment {#create-an-adaptive-form-in-experience-fragment}

Ni kan utöka räckvidden för era formulär genom att lägga till dem i AEM Experience Fragments, vilket möjliggör smidig återanvändning på flera sidor eller webbplatser. Du kan till exempel inkludera ett formulär för anmälan av nyhetsbrev i ett Experience Fragment. På så sätt kan du enkelt återanvända fragmentet på flera sidor på webbplatsen, vilket eliminerar behovet av att återskapa formuläret upprepade gånger. Alla uppdateringar eller ändringar som görs i formuläret för anmälan av nyhetsbrev i Experience Fragment sprids automatiskt till alla sidor där det används. Detta effektiviserar processen och ger en smidig användarupplevelse samtidigt som det förenklar hanteringen av webbplatsens formulär.

Så här skapar du ett anpassat formulär i ett Experience Fragment:

1. Öppna ett Experience Fragment.
1. Dra och släpp **[!UICONTROL Adaptive Forms Container]** -komponenten från komponentwebbläsaren till Experience Fragment.
1. Dra och släpp adaptiva kärnkomponenter i formulär till behållarutrymmet i Experience Fragment för att skapa formuläret.
1. Lägg till knappen Skicka.

Nästa [ange åtgärden Skicka](#configure-submit-action-for-form) och avancerade egenskaper.

### Konvertera ett anpassat formulär på en AEM Sites-sida till ett Experience Fragment {#convert-an-adaptive-form-in-sites-page-to-an-experience-fragment}

Du kan konvertera ett befintligt adaptivt formulär i en webbplatssidredigerare till ett Experience Fragment för att återanvända formuläret på flera sidor eller webbplatser.

Så här konverterar du ett adaptivt formulär på en AEM Sites-sida till ett Experience Fragment:

1. Öppna AEM Sites-sidan som innehåller det adaptiva formuläret (i adaptiva Forms Container-komponenten) i redigeringsläge.
1. Öppna innehållsträdet och välj **[!UICONTROL Adaptive Forms Container]** som är värd för din adaptiva form. En AEM Sites-sida kan vara värd för flera adaptiva Forms. Välj rätt adaptiva Forms-behållare.
1. På menyraden väljer du ![Ikon för att konvertera till upplevelsefragmentvariationer](/help/forms/using/assets/Smock_FilingCabinet_18_N.svg) Konvertera till Experience Fragment-variationsikon.
   ![](/help/forms/using/assets/convert-form-in-sites-page-to-an-experience-fragment.png)

   En dialogruta visas om du vill konvertera behållaren för det adaptiva formuläret till ett nytt Experience Fragment eller lägga till i ett befintligt Experience Fragment
1. I dialogrutan Konvertera till Experience Fragment-variation anger du värden för följande alternativ:

   * **Åtgärd:** Välj om du vill skapa ett nytt Experience Fragment eller Lägg till i ett befintligt Experience Fragment.
   * **Överordnad sökväg:** Ange sökvägen till den mapp där Experience Fragment ska vara värd. Alternativet är bara tillgängligt för att skapa ett nytt Experience Fragment.
   * **Mall:** Ange sökvägen till Experience Fragment-mallen. Om du inte har någon Experience Fragment-mall [skapa](/help/sites-developing/experience-fragments.md). Alternativet är bara tillgängligt för att lägga till adaptiv form till ett befintligt Experience Fragment.
   * **Fragmenttitel:** Ange Experience Fragment-titel. Titeln identifierar en Experience Fragment unikt


## Konfigurera Skicka-åtgärd för formuläret {#configure-submit-action-for-form}

Med en Skicka-åtgärd kan du välja målet för data som har hämtats via ett anpassat formulär. Den aktiveras när en användare klickar på knappen Skicka på ett anpassat formulär. Anpassade formulär innehåller några av de åtgärder som har vidtagits för att skicka in. Du kan också utöka en standardåtgärd för att skicka för att skapa en egen anpassad åtgärd. Så här konfigurerar du en Skicka-åtgärd för formuläret:

1. Öppna AEM Page Editor eller Experience Fragment som innehåller det adaptiva formuläret.
1. Öppna innehållsträdet och välj **[!UICONTROL Adaptive Forms Container]** som är värd för din adaptiva form. En AEM Sites-sida kan vara värd för flera adaptiva Forms. Välj rätt adaptiva Forms-behållare.
1. Klicka på egenskaperna för den adaptiva formulärbehållaren ![Egenskaper för adaptiv formulärbehållare](/help/forms/using/assets/configure-icon.svg) ikon. Dialogrutan Adaptiv formulärbehållare där du kan konfigurera skicka-åtgärder öppnas.
   ![](/help/forms/using/assets/adaptive-forms-container.png)
1. Välj och konfigurera en Skicka-åtgärd utifrån dina krav. Mer information om Skicka åtgärder finns i [Inlämningsåtgärd för anpassat formulär](configuring-submit-actions.md)


## Konfigurera ett schema eller en formulärdatamodell för ett formulär {#configure-schema-or-data-model-for-form}

Du kan använda formulärdatamodellen för att ansluta ett formulär till en datakälla för att skicka och ta emot data baserat på användaråtgärder. Du kan också ansluta ett formulär till ett JSON-schema för att ta emot skickade data i ett fördefinierat format.

Innan du ansluter ett formulär till ett schema eller en formulärdatamodell

* [Skapa ett JSON-schema och överför det till din miljö](adaptive-form-json-schema-form-model.md)
* [Skapa en formulärdatamodell](create-form-data-models.md)

Så här konfigurerar du ett JSON-schema eller en formulärdatamodell för formuläret:

1. Öppna AEM Page Editor eller Experience Fragment som innehåller det adaptiva formuläret.
1. Öppna innehållsträdet och välj **[!UICONTROL Adaptive Forms Container]** som är värd för din adaptiva form. En AEM Sites-sida kan vara värd för flera adaptiva Forms. Välj rätt adaptiva Forms-behållare.
1. Klicka på egenskaperna för den adaptiva formulärbehållaren ![Egenskaper för adaptiv formulärbehållare](/help/forms/using/assets/configure-icon.svg) ikon. Dialogrutan Adaptiv formulärbehållare öppnas för att konfigurera datamodeller.
   ![](/help/forms/using/assets/form-data-model-adaptive-forms-container.png)
1. Välj och konfigurera ett JSON-schema eller en formulärdatamodell utifrån dina behov. Mer information om Skicka åtgärder finns i [Inlämningsåtgärd för anpassat formulär](configuring-submit-actions.md).

   * När du väljer **[!UICONTROL Form Model]** , använd **[!UICONTROL Select Form Data Model]** för att välja en förkonfigurerad formulärdatamodell.
   * När du väljer **[!UICONTROL Schema]** , använd **[!UICONTROL Schema]** för att välja ett JSON-schema för formuläret.

1. Klicka på **[!UICONTROL Done]**.

## Konfigurera en förifyllningstjänst för ett formulär {#configure-prefill-service-for-form}

Du kan använda förifyllningstjänsten för att autofylla fält i ett adaptivt formulär med befintliga data. När en användare öppnar ett formulär är värdena för dessa fält förifyllda. Du kan:

* [Skapa en anpassad förifyllningstjänst](prepopulate-adaptive-form-fields.md)
* [Använd förifyllningstjänsten för formulärdatamodell](#fdm-prefill-service)

### Använd förifyllningstjänsten för formulärdatamodell {#fdm-prefill-service}

Du kan använda förifyllningstjänsten för formulärdatamodell för att fylla i fält i ett formulär i förväg med en konfigurerad formulärdatamodell. Tjänsten för förifyllnad av formulärdatamodell använder [Hämta tjänst för konfigurerad formulärdatamodell](work-with-form-data-model.md#add-data-model-objects-and-services-add-data-model-objects-and-services) för att hämta data. Så här använder du förifyllningstjänsten för formulärdatamodell för ett adaptivt formulär:

1. Öppna AEM Page Editor eller Experience Fragment som innehåller det adaptiva formuläret.
1. Öppna innehållsträdet och välj **[!UICONTROL Adaptive Forms Container]** som är värd för din adaptiva form. En AEM Sites-sida kan vara värd för flera adaptiva Forms. Välj rätt adaptiva Forms-behållare.
1. Klicka på egenskaperna för den adaptiva formulärbehållaren ![Egenskaper för adaptiv formulärbehållare](/help/forms/using/assets/configure-icon.svg) ikon. Dialogrutan Adaptiv formulärbehållare öppnas för att konfigurera datamodeller.
   ![](/help/forms/using/assets/prefill-service-fdm-aem-sites-page-editor.png)
1. Välj en formulärdatamodell. Öppna **[!UICONTROL Basic]** -fliken. I förifyllningstjänsten väljer du **[!UICONTROL Forms Portal Draft Prefill Service]**.
1. Klicka på **[!UICONTROL Done]**.

## Dirigera om användaren till en ny användare när formuläret skickas eller visa ett tackmeddelande

När du skickar ett formulär kan du dirigera om användaren till en annan webbsida eller ett meddelande. Så här omdirigerar du användaren eller konfigurerar tackmeddelandet:

1. Öppna AEM Page Editor eller Experience Fragment som innehåller det adaptiva formuläret.
1. Öppna innehållsträdet och välj **[!UICONTROL Adaptive Forms Container]** som är värd för din adaptiva form. En AEM Sites-sida kan vara värd för flera adaptiva Forms. Välj rätt adaptiva Forms-behållare.
1. Klicka på egenskaperna för den adaptiva formulärbehållaren ![Egenskaper för adaptiv formulärbehållare](/help/forms/using/assets/configure-icon.svg) ikon. Dialogrutan Adaptiv formulärbehållare öppnas för att konfigurera datamodeller.
1. Öppna **[!UICONTROL Submission]** -fliken.

   * Om du vill konfigurera en omdirigerings-URL, för alternativet Skicka, markerar du alternativet Omdirigera till URL och anger en absolut adress eller en omdirigerings-URL eller relativ sökväg för en AEM Sites-sida.

   * Om du vill konfigurera ett anpassat meddelande eller ett tackmeddelande för alternativet Skicka, markerar du alternativet Visa meddelande och anger ett meddelande i rutan Meddelandeinnehåll. Det är en RTF-ruta som du kan använda helskärmsalternativet för att visa alla tillgängliga RTF-objekt.



