---
title: Skapa riktat innehåll med målläge
description: Målinriktningsläget och Target-komponenten innehåller verktyg för att skapa innehåll för upplevelser
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: personalization
docset: aem65
exl-id: edde225d-0be7-4306-8dda-d18d46fae977
source-git-commit: 7f35fdee9dbca9dfd3992b56579d6d06633f8dec
workflow-type: tm+mt
source-wordcount: '5374'
ht-degree: 5%

---

# Skapa riktat innehåll med målläge{#authoring-targeted-content-using-targeting-mode}

Skapa riktat innehåll med målläget AEM. Målinriktningsläget och Target-komponenten innehåller verktyg för att skapa innehåll för upplevelser:

* Identifiera enkelt målinnehållet på sidan. En prickad linje bildar en kant runt allt innehåll som är avsett för det.
* Välj ett varumärke och en aktivitet för att se upplevelserna.
* Lägg till upplevelser i en aktivitet eller ta bort upplevelser.
* Utför A/B-tester och konvertera vinnare (endast Adobe Target).
* Lägg till erbjudanden till en upplevelse genom att skapa erbjudanden eller använda erbjudanden från ett bibliotek.
* Konfigurera mål och övervaka prestanda.
* Simulera användarupplevelsen.
* Konfigurera Target-komponenten om du vill ha mer anpassning.

Du kan använda antingen AEM eller Adobe Target som målmotor (du måste ha ett giltigt Adobe Target-konto för att kunna använda Adobe Target). Om du använder Adobe Target måste du först konfigurera integreringen. Se [anvisningar för integrering med Adobe Target](/help/sites-administering/target.md).

![chlimage_1-8](assets/chlimage_1-8.png)

De aktiviteter och upplevelser som du ser i målläget speglar de [Aktiverar konsol](/help/sites-authoring/activitylib.md):

* Ändringar som du gör i aktiviteter och upplevelser med målläget visas i aktivitetskonsolen.
* Ändringar som görs i aktivitetskonsolen återspeglas i målläget.

>[!NOTE]
>
>När du skapar en kampanj i Adobe Target tilldelas den en egenskap som kallas `thirdPartyId`till varje kampanj. När du tar bort kampanjen i Adobe Target tas inte thirdPartyId bort. Du kan inte återanvända `thirdPartyId` för kampanjer av olika typer (AB, XT) och kan inte tas bort manuellt. För att undvika det här problemet kan du namnge varje kampanj med ett unikt namn. Kampanjnamn kan inte återanvändas i olika kampanjtyper.
>
>Om du använder samma namn i samma kampanjtyp skriver du över den befintliga kampanjen.
>
>Om du får felmeddelandet&quot;Begäran misslyckades&quot; under synkroniseringen. `thirdPartyId` finns redan&quot;, ändrar namnet på kampanjen och synkroniserar igen.

>[!NOTE]
>
>Vid målgruppsanpassning behålls varumärknings- och aktivitetskombinationen på användarnivå, inte på kanalnivå.

## Växla till målläge {#switching-to-targeting-mode}

Växla till målläget för att komma åt verktygen för att skapa riktat innehåll.

Så här växlar du till målläge:

1. Öppna sidan som du vill skapa riktat innehåll för.
1. Klicka eller tryck på listrutan Läge i verktygsfältet högst upp på sidan för att visa de tillgängliga lägestyperna.

   ![chlimage_1-9](assets/chlimage_1-9.png)

1. Klicka eller tryck **Målinriktning**. Målinställningarna visas högst upp på sidan.

   ![chlimage_1-10](assets/chlimage_1-10.png)

## Lägga till en aktivitet med målläge {#adding-an-activity-using-targeting-mode}

Använd målinriktningsläget för att lägga till en aktivitet till ett varumärke. När du lägger till en aktivitet innehåller den standardupplevelsen. När du har lagt till aktiviteten startar du målprocessen för innehållet för aktiviteten.

Du kan också skapa och hantera Adobe Target-aktiviteter från AEM genom att välja målmotor - antingen AEM eller Adobe Target - och välja aktivitetstyp - Experience Targeting eller A/B Test.

Dessutom kan ni hantera mål och mätvärden för alla Adobe Target-aktiviteter och hantera era Adobe Target-målgrupper. Adobe Target aktivitetsrapportering, inklusive konvertering av vinnare för A/B-tester, ingår också.

När du lägger till en aktivitet visas den även i [Aktivitetskonsol](/help/sites-authoring/activitylib.md).

Så här lägger du till en aktivitet:

1. Använd **Varumärke** i den nedrullningsbara menyn för att välja det varumärke som du vill skapa aktiviteten för.

   >[!NOTE]
   >
   >Adobe rekommenderar att du [skapa varumärken via aktivitetskonsolen](/help/sites-authoring/activitylib.md#creating-a-brand-using-the-activities-console).
   >
   >
   >Om du skapar ett varumärke på något annat sätt måste du se till att noden `/campaigns/<brand>/master` finns eller ett fel uppstår när du försöker skapa en aktivitet.

1. Klicka eller tryck + bredvid **Aktivitet** listruta.
1. Ange ett namn för aktiviteten.

   >[!NOTE]
   >
   >När du skapar en aktivitet och har en Adobe Target-molnkonfiguration kopplad till sidan eller någon av dess överordnade sidor, antar AEM automatiskt Adobe Target som motor.

1. I **Målinriktning** i den nedrullningsbara menyn väljer du målmotor.

   * Om du väljer **ContextHub-AEM**&#x200B;är de återstående fälten nedtonade och inte tillgängliga. Klicka eller tryck **Skapa**.

   * Om du väljer **Adobe Target** kan du välja en konfiguration (som standard är det den konfiguration du tillhandahöll när du [konfigurerade kontot](/help/sites-administering/opt-in.md)) och aktivitetstyp.

   * Om du använder AEM/Adobe Campaign-integreringen och skickar riktat innehåll (nyhetsbrev) väljer du **Adobe Campaign**. Se [Integrera med Adobe Campaign](/help/sites-administering/campaign.md) för mer information.

1. Välj något av följande alternativ på menyn Aktivitet **Experience Targeting** eller **A/B-test**.

   * Målinriktning - hantera Adobe Target-aktiviteter från AEM.
   * A/B-test - skapa/hantera A/B-testaktiviteter i Adobe Target från AEM.

## Målprocessen: Skapa, Mål och Mål och inställningar {#the-targeting-process-create-target-and-goals-settings}

I målinriktningsläget kan du konfigurera flera aspekter av en aktivitet. Använd följande trestegsprocess för att skapa riktat innehåll för en varumärkesaktivitet:

1. [Skapa](#create-authoring-the-experiences): Lägg till eller ta bort upplevelser och lägg till erbjudanden för varje upplevelse.
1. [Mål](#diagramtargetconfiguringtheaudiences): Ange målgruppen för varje upplevelse. Ni kan inrikta er på en viss målgrupp och om ni använder A/B-tester avgör hur stor procentandel av trafiken som går till vilken upplevelse.
1. [Mål och inställningar](#settingsgoalssettingsconfiguringtheactivityandsettinggoals): Schemalägg aktiviteten och ange prioritet. Ni kan också ställa in mätmål för framgång.

Använd följande procedur för att starta innehållsriktningsprocessen för en aktivitet.

>[!NOTE]
>
>Om du vill använda målprocessen måste du vara medlem i användargruppen Författare för målaktivitet.

Så här lägger du till en aktivitet:

1. I **Varumärke** väljer du det varumärke som innehåller den aktivitet du arbetar med.
1. I **Aktivitet** väljer du den aktivitet som du skapar målinnehåll för.
1. Om du vill visa kontrollerna som vägleder dig genom målprocessen klickar eller trycker du **Börja målinrikta**.

   ![chlimage_1-11](assets/chlimage_1-11.png)

   >[!NOTE]
   >
   >Om du vill ändra aktiviteten som du arbetar med klickar eller trycker du **Bakåt**.

## Skapa: Skapa upplevelser {#create-authoring-the-experiences}

Det kreativa steget i innehållsanpassningen innefattar att skapa upplevelser. Under det här steget kan du skapa eller ta bort aktivitetens upplevelser och lägga till erbjudanden för varje upplevelse.

### Upplevelserbjudanden i målinriktat läge {#seeing-experience-offers-in-targeting-mode}

Efter dig [starta målinriktningsprocessen](/help/sites-authoring/content-targeting-touch.md#the-targeting-process-create-target-and-goals-settings)väljer du en upplevelse för att se vilka erbjudanden som finns för den upplevelsen. När du väljer en upplevelse ändras målkomponenterna på sidan så att erbjudandet för den upplevelsen visas.

>[!CAUTION]
>
>Var försiktig när du inaktiverar mål för en komponent som redan har angetts som mål i författarinstansen. Aktiviteten tas automatiskt bort från publiceringsinstansen också.

>[!NOTE]
>
>Ett erbjudande är innehållet i en riktad komponent.

Upplevelserna visas i rutan Målgrupper. I följande exempel finns upplevelserna **Standard**, **Kvinna**, **Kvinna över 30** och **Kvinna under 30**. I det här exemplet visas standarderbjudandet för en riktad **bildkomponent**.

![chlimage_1-12](assets/chlimage_1-12.png)

När en annan upplevelse väljs visas erbjudandet för den upplevelsen i bildkomponenten.

![chlimage_1-13](assets/chlimage_1-13.png)

När en upplevelse väljs och målkomponenten inte innehåller något erbjudande för den upplevelsen, visas **Lägg till erbjudande** ovanpå det halvgenomskinliga standarderbjudandet. När inget erbjudande har skapats för en upplevelse visas **standarderbjudandet** för det segment som är mappat till upplevelsen.

![chlimage_1-14](assets/chlimage_1-14.png)

Standardupplevelsen visas också när besökaregenskaperna inte matchar några segment som är mappade till upplevelserna. Se [Lägga till upplevelser med målläge](#adding-and-removing-experiences-using-targeting-mode).

### Skräddarsydda erbjudanden och bibliotekserbjudanden {#custom-offers-and-library-offers}

Erbjudanden som [som har skapats på sidan](/help/sites-authoring/content-targeting-touch.md#adding-a-custom-offer) och används för en enda upplevelse kallas anpassade erbjudanden. Följande bild läggs ovanpå innehållet i ett anpassat erbjudande:

![chlimage_1-15](assets/chlimage_1-15.png)

Erbjudanden som [som lagts till från ett erbjudandebibliotek](/help/sites-authoring/content-targeting-touch.md#adding-an-offer-from-an-offer-library) läggs ovanpå följande bild:

![chlimage_1-16](assets/chlimage_1-16.png)

Du kan spara anpassade erbjudanden i ett erbjudandebibliotek om du bestämmer dig för att återanvända dem. Du kan också konvertera ett bibliotekserbjudande till ett anpassat erbjudande om du vill ändra innehållet för en upplevelse. Efter redigeringen kan du spara erbjudandet i biblioteket igen.

### Lägga till och ta bort upplevelser med målläge {#adding-and-removing-experiences-using-targeting-mode}

Använda steget Skapa i [målgruppsprocessen](/help/sites-authoring/content-targeting-touch.md#the-targeting-process-create-target-and-goals-settings)kan ni lägga till och ta bort upplevelser. Dessutom kan du duplicera en upplevelse och ändra namn på den.

#### Lägga till upplevelser med målinriktat läge {#adding-experiences-using-targeting-mode}

Lägga till en upplevelse:

1. Klicka eller tryck för att lägga till en upplevelse **+** **Lägg till Experience Targeting** som visas under de befintliga upplevelserna i **Målgrupper** fönster.
1. Välj och få en målgrupp. Som standard är det namnet på upplevelsen. Om du vill kan du skriva ett annat namn. Klicka eller tryck **OK**.

#### Ta bort upplevelser med målläge {#removing-experiences-using-targeting-mode}

Så här tar du bort en upplevelse:

1. Klicka eller tryck på pilen bredvid upplevelsens namn.

   ![chlimage_1-17](assets/chlimage_1-17.png)

1. Klicka **Ta bort**.

#### Byta namn på upplevelser med målläge {#renaming-experiences-using-targeting-mode}

Så här byter du namn på upplevelser med målläget:

1. Klicka eller tryck på pilen bredvid upplevelsens namn.
1. Klicka **Byt namn på upplevelsen** och skriv in det nya namnet.
1. Klicka eller tryck någon annanstans på skärmen för att spara ändringarna.

#### Redigera målgrupper med målläge {#editing-audiences-using-targeting-mode}

Så här redigerar du målgrupper med målläget:

1. Klicka eller tryck på pilen bredvid upplevelsens namn.
1. Klicka **Redigera målgrupp** och välj en ny målgrupp.
1. Klicka **OK**.

#### Duplicera upplevelser med målläge {#duplicating-experiences-using-targeting-mode}

Så här kopierar du upplevelser med målläget:

1. Klicka eller tryck på pilen bredvid upplevelsens namn.
1. Klicka **Duplicera** och välja målgrupp.
1. Byt namn på upplevelsen om så önskas och klicka på **OK**.

### Skapa erbjudanden med målläge {#creating-offers-using-targeting-mode}

Rikta en komponent mot att skapa erbjudanden för upplevelser. Målinriktade komponenter tillhandahåller det innehåll som används som erbjudanden för upplevelser.

* [Aktivera en befintlig komponent](/help/sites-authoring/content-targeting-touch.md#creating-a-default-offer-by-targeting-an-existing-component). Innehållet blir erbjudandet om standardupplevelsen.
* [Lägga till en målkomponent](/help/sites-authoring/content-targeting-touch.md#creating-an-offer-by-adding-a-target-component)och sedan lägga till innehåll i komponenten.

När en komponent har valts kan du lägga till erbjudanden för varje upplevelse:

* [Lägg till anpassade erbjudanden](/help/sites-authoring/content-targeting-touch.md#adding-a-custom-offer).
* [Lägga till erbjudanden från ett bibliotek](/help/sites-authoring/content-targeting-touch.md#adding-an-offer-from-an-offer-library).

Följande verktyg är tillgängliga för att arbeta med erbjudanden:

* [Lägg till ett anpassat erbjudande i ett erbjudandebibliotek](/help/sites-authoring/content-targeting-touch.md#adding-a-custom-offer-to-a-library).
* [Konvertera ett bibliotekserbjudande till ett anpassat erbjudande](/help/sites-authoring/content-targeting-touch.md#converting-a-library-offer-to-a-custom-library).
* [Öppna ett bibliotekserbjudande och redigera innehållet](/help/sites-authoring/content-targeting-touch.md#editing-a-library-offer).

#### Skapa ett standarderbjudande genom att ange en befintlig komponent som mål {#creating-a-default-offer-by-targeting-an-existing-component}

Aktivera en komponent på sidan för att använda den som erbjudande för aktivitetens standardupplevelse. När du riktar in dig på en komponent omges den av en Target-komponent och dess innehåll blir ett erbjudande för standardupplevelsen.

När du har en målkomponent som mål kan bara den komponenten användas i erbjudandet. Du kan inte ta bort komponenten från erbjudandet eller lägga till andra komponenter i erbjudandet.

Utför följande procedur efter [starta målinriktningsprocessen](/help/sites-authoring/content-targeting-touch.md#the-targeting-process-create-target-and-goals-settings).

1. Klicka på eller tryck på den komponent som du vill ha som mål. Verktygsfältet för komponenten visas, ungefär som i följande exempel.

   ![chlimage_1-18](assets/chlimage_1-18.png)

1. Klicka på eller tryck på målikonen.

   ![Mål](do-not-localize/chlimage_1.png)

   Komponentinnehållet är erbjudandet för standardupplevelsen. När en komponent har valts replikeras dess standardnod för varje upplevelse. Detta behövs för att redigera rätt innehållsnod vid upplevelsespecifik redigering. För de här icke-standardupplevelserna är antingen [lägg till ett anpassat erbjudande](/help/sites-authoring/content-targeting-touch.md#adding-a-custom-offer) eller [lägg till ett bibliotekserbjudande](/help/sites-authoring/content-targeting-touch.md#adding-an-offer-from-an-offer-library).

#### Skapa ett erbjudande genom att lägga till en målkomponent {#creating-an-offer-by-adding-a-target-component}

Lägg till en Target-komponent för att skapa erbjudandet för standardupplevelsen. Målkomponenten är en behållare för andra komponenter, och komponenter som placeras i den blir mål. När du använder Target-komponenten kan du lägga till flera komponenter för att skapa ett erbjudande. Ni kan också använda olika komponenter i varje upplevelse för att skapa olika erbjudanden.

Se [Konfigurera alternativ för målkomponent](/help/sites-authoring/content-targeting-touch.md#configuring-target-component-options) om du vill ha information om hur du anpassar den här komponenten.

>[!NOTE]
>
>Erbjudanden som du skapar med [Erbjuder konsol](/help/sites-authoring/offerlib.md) kan också innehålla flera komponenter. Erbjudandena tillhör ett erbjudandebibliotek och kan användas för flera olika upplevelser.

Eftersom Target-komponenten är en behållare visas den som ett släppområde för andra komponenter.

I målläget har Target-komponenten en blå ram och drop-target-meddelandet anger måltypen.

![chlimage_1-19](assets/chlimage_1-19.png)

I redigeringsläget har målkomponenten en punktningsikon.

![Målkomponent i redigeringsläge](do-not-localize/chlimage_1-1.png)

När du drar komponenter till Target-komponenten är de målkomponenter.

![chlimage_1-20](assets/chlimage_1-20.png)

När du lägger till en komponent i Target-komponenten får den innehåll för en viss upplevelse. Du anger upplevelsen genom att välja upplevelsen innan du lägger till komponenterna.

Du kan lägga till en Target-komponent på sidan i redigeringsläge eller i målläge. Du kan bara lägga till komponenter i Target-komponenten i Target-läge. Målkomponenten tillhör komponentgruppen Personalisering.

Om du redigerar målinnehåll måste du klicka eller trycka **Börja målinrikta** innan du kan göra det.

1. Dra Target-komponenten till sidan där du vill att erbjudandet ska visas.
1. Som standard har inget plats-ID angetts. Klicka på eller tryck på konfigurationshjulet för att ange platsen.

   >[!NOTE]
   >
   >Om det anges av administratören kan du behöva ange platsen explicit.
   >
   >
   >Administratörer kan bestämma om den här konfigurationen måste anges på **https://&lt;host>:&lt;port>/system/console/configMgr/com.day.cq.personalization.impl.servlets.TargetingConfigurationServlet**
   >
   >
   Om du vill att användare ska ange en plats markerar du kryssrutan **Tvinga plats **.

1. Välj den upplevelse som du vill skapa erbjudandet för.
1. Skapa erbjudandet:

   * För standardupplevelsen drar du komponenter till målsläppsområdet och redigerar komponentegenskaperna som vanligt för att skapa innehållet för erbjudandet.
   * För upplevelser som inte är standard är antingen [lägg till ett anpassat erbjudande](#adding-a-custom-offer) eller [lägg till ett bibliotekserbjudande](/help/sites-authoring/content-targeting-touch.md#adding-an-offer-from-an-offer-library).

#### Lägga till ett anpassat erbjudande {#adding-a-custom-offer}

Skapa ett erbjudande genom att skapa innehållet i en målkomponent i målinriktningsläget. När du skapar ett anpassat erbjudande används det som ett erbjudande för en enda upplevelse.

Om ni bestämmer er för att erbjudandet kan användas för andra upplevelser kan ni skapa ett anpassat erbjudande och [lägg till det i biblioteket](/help/sites-authoring/content-targeting-touch.md#adding-a-custom-offer-to-a-library). Mer information om hur du använder Offers-konsolen för att skapa ett återanvändbart erbjudande finns i [Lägg till ett erbjudande i ett erbjudandebibliotek](/help/sites-authoring/offerlib.md#add-an-offer-to-an-offer-library).

1. Välj den upplevelse som du lägger till erbjudandet till.
1. Om du vill visa komponentmenyn klickar eller trycker du på den målkomponent som du vill lägga till erbjudandet i.

   ![chlimage_1-21](assets/chlimage_1-21.png)

1. Klicka eller tryck på ikonen +.

   Innehållet i standarderbjudandet används som erbjudande för den aktuella upplevelsen.

1. Klicka på eller tryck på erbjudandet för att visa erbjudandemenyn och klicka eller tryck sedan på redigeringsikonen.

   ![Menyn Erbjudande](do-not-localize/chlimage_1-2.png)

1. Redigera komponentens innehåll.

#### Lägga till ett erbjudande från ett offertbibliotek {#adding-an-offer-from-an-offer-library}

Lägg till ett erbjudande från [erbjudandebibliotek](/help/sites-authoring/offerlib.md) till en upplevelse. Ni kan lägga till alla erbjudanden från varumärkesbiblioteket som ni nu riktar er mot.

Du kan inte lägga till bibliotekserbjudanden i standardupplevelsen.

1. Välj den upplevelse som du lägger till erbjudandet till.
1. Om du vill visa komponentmenyn klickar eller trycker du på den målkomponent som du vill lägga till erbjudandet i.

   ![chlimage_1-22](assets/chlimage_1-22.png)

1. Klicka på eller tryck på mappikonen.

   ![Mappikon](do-not-localize/chlimage_1-3.png)

1. Välj erbjudandet från biblioteket och klicka eller tryck sedan på bockmarkeringsikonen.

   ![chlimage_1-23](assets/chlimage_1-23.png)

   Med erbjudandeväljaren kan du bläddra eller filtrera efter erbjudanden. När du bläddrar eller filtrerar kanske du också vill sortera erbjudandena och ändra hur du ser dem. Siffran i det övre högra hörnet visar hur många erbjudanden som är tillgängliga i det aktuella biblioteket.

   * Klicka eller tryck **Bläddra** för att navigera till en annan mapp. Navigeringsrutan öppnas och du klickar på pilen för att gå ned i mapparna. Klicka eller tryck **Bläddra** igen för att stänga navigeringsrutan.

   ![chlimage_1-24](assets/chlimage_1-24.png)

   * Klicka eller tryck **Filter** om du vill filtrera erbjudandena mot nyckelord eller taggar. Du anger nyckelord och väljer taggar i listrutan. Klicka eller tryck **Filter** igen för att stänga filtreringsrutan.

   ![chlimage_1-25](assets/chlimage_1-25.png)

   * Ändra hur du sorterar erbjudandena genom att klicka eller trycka på pilen bredvid **Nyaste till äldsta**. Erbjudandena kan sorteras från nyaste till äldsta eller äldsta till nyaste.

   ![chlimage_1-26](assets/chlimage_1-26.png)

   Klicka eller tryck på ikonen bredvid **Visa som** för att visa erbjudanden som rutor eller som en lista.

   ![chlimage_1-27](assets/chlimage_1-27.png)

#### Lägga till ett anpassat erbjudande i ett bibliotek {#adding-a-custom-offer-to-a-library}

Lägg till ett anpassat erbjudande i [erbjudandebibliotek](/help/sites-authoring/offerlib.md) när ni vill återanvända det som ett erbjudande för flera upplevelser. Ni kan lägga till erbjudanden i biblioteket för det aktuella varumärket ni riktar er mot.

Mer information om hur du använder Offers-konsolen för att skapa ett återanvändbart erbjudande finns i [Lägg till ett erbjudande i ett erbjudandebibliotek](/help/sites-authoring/offerlib.md#add-an-offer-to-an-offer-library).

1. Välj upplevelsen för att visa det anpassade erbjudandet.
1. Klicka på eller tryck på det anpassade erbjudandet för att visa erbjudandemenyn, klicka eller tryck på **Spara erbjudandet i erbjudandebiblioteket** -ikon.

   ![Spara erbjudandet i Erbjudandebibliotek](do-not-localize/chlimage_1-4.png)

1. Skriv ett namn för erbjudandet, markera det bibliotek som du vill lägga till erbjudandet till och klicka eller tryck sedan på bockmarkeringsikonen.

#### Konvertera ett bibliotekserbjudande till ett anpassat bibliotek {#converting-a-library-offer-to-a-custom-library}

Konvertera ett bibliotekserbjudande till ett anpassat erbjudande för att ändra erbjudandet för den aktuella upplevelsen utan att ändra erbjudandet i andra upplevelser.

1. Välj den upplevelse du vill visa bibliotekserbjudandet.
1. Klicka på eller tryck på bibliotekserbjudandet för att visa erbjudandemenyn och klicka eller tryck sedan på ikonen Konvertera till infogat erbjudande.

   ![Konvertera till infogat erbjudande](do-not-localize/chlimage_1-5.png)

#### Redigera ett bibliotekserbjudande {#editing-a-library-offer}

Öppna ett bibliotekserbjudande från en upplevelse i målläge för att redigera erbjudandet. De ändringar ni gör visas i alla upplevelser som använder erbjudandet.

1. Välj den upplevelse du vill visa bibliotekserbjudandet.
1. Konvertera bibliotekserbjudandet till ett lokalt/anpassat erbjudande. Se [Konvertera ett bibliotekserbjudande till ett anpassat bibliotek](#converting-a-library-offer-to-a-custom-library).
1. Redigera innehållet i erbjudandet.

1. Spara den i biblioteket igen. Se [Lägga till ett anpassat erbjudande i ett bibliotek](#adding-a-custom-offer-to-a-library).

## Mål: Konfigurera publikerna {#target-configuring-the-audiences}

Målsteget i [målgruppsprocessen](/help/sites-authoring/content-targeting-touch.md#the-targeting-process-create-target-and-goals-settings) innebär att kartlägga målgrupper med de upplevelser du arbetade med i steget Skapa. Målsidan visar vilka målgrupper varje upplevelse riktar sig till. Ni kan ange eller ändra målgruppen för varje upplevelse. Om du använder Adobe Target kan du även skapa A/B-tester som gör att du kan ange en procentandel av trafiken för en viss målgrupp för en viss upplevelse.

### Om du använder AEM målinriktning eller Adobe Target (upplevelseanpassning) ... {#if-you-are-using-aem-targeting-or-adobe-target-experience-targeting}

Publiken visas till vänster i mappningsdiagrammet, och upplevelserna visas till höger.

![chlimage_1-28](assets/chlimage_1-28.png)

Definiera en målgrupp med ett segment. Molnkonfigurationen för sidan avgör vilka segment som är tillgängliga för dig. När sidan inte är kopplad till en molnkonfiguration från Adobe Target finns AEM segment tillgängliga för att definiera målgrupper. När sidan är kopplad till en Adobe Target-molnkonfiguration använder du målsegment.

Information om målmotorer finns på [Målmotor](/help/sites-authoring/personalization.md#targeting-engine).

Använd inte en publik mer än en upplevelse. En varningssymbol visas bredvid en upplevelse när den kopplas till en målgrupp som kopplas till en annan upplevelse.

![Varningssymbol när den mappas till en publik som mappas till en annan upplevelse](do-not-localize/chlimage_1-6.png)

### Associera upplevelser med målgrupper (AEM eller Adobe Target) {#associating-experiences-with-audiences-aem-or-adobe-target}

Använd följande procedur för att associera en upplevelse med en målgrupp när du använder AEM (eller Adobe Target Experience targeting):

1. Klicka på eller tryck på den nedrullningsbara pilen bredvid den målgruppsruta som är kopplad till upplevelsen.
1. (Valfritt) Klicka eller tryck **Redigera** och skriv sedan ett nyckelord för att söka efter det önskade segmentet.
1. Välj målgrupp i listan över målgrupper och klicka eller tryck på **OK**.

### Om du använder A/B-testning (Adobe Target) ... {#if-you-are-using-a-b-testing-adobe-target}

Om ni har en A/B-testaktivitet finns målgrupperna till vänster, procentandelen som varje upplevelse visas i mitten och upplevelserna till höger.

Du kan ändra procentsatserna så länge de adderar till 100 procent. En målgrupp kan användas av flera olika upplevelser i A/B-testning.

![chlimage_1-29](assets/chlimage_1-29.png)

### Associera målgrupper och trafikprocent med A/B-tester {#associating-audiences-and-traffic-percentages-with-a-b-testing}

1. Klicka på eller tryck på listrutan bredvid målgruppen som är kopplad till upplevelsen.
1. (Valfritt) Klicka på **Redigera** skriver du ett nyckelord och söker efter det önskade segmentet.
1. Klicka eller tryck **Okej.**
1. Ange i procent för att konfigurera hur målgruppstrafiken dirigeras till varje upplevelse. Det totala talet måste vara lika med 100.
1. (Valfritt) Redigera upplevelsens namn genom att klicka på den nedrullningsbara menyn bredvid upplevelsens namn.

## Mål och inställningar: Konfigurera mål för aktivitet och inställning {#goals-settings-configuring-the-activity-and-setting-goals}

Målet och inställningarna i [målgruppsprocessen](/help/sites-authoring/content-targeting-touch.md#the-targeting-process-create-target-and-goals-settings) innebär att varumärkesaktivitetens beteende konfigureras. Ange när aktiviteten startar och avslutas samt aktivitetsprioriteten. Dessutom håller du också koll på målen. Du kan bestämma vad du vill mäta med dina aktiviteter.

Måttvärden är bara tillgängliga om du använder Adobe Target för målgruppsmotorn. Du måste definiera minst ett målmått. Om du har konfigurerat Adobe Analytics och har en A4T Analytics-molnkonfiguration kan du välja om du vill att rapportkällan ska vara Adobe Target eller Adobe Analytics.

Måtten mäts bara för den publicerade kampanjen.

Om du använder AEM som målmotor:

![chlimage_1-30](assets/chlimage_1-30.png)

Om du använder Adobe Target som målmotor:

![chlimage_1-31](assets/chlimage_1-31.png)

Om du använder Adobe Target som målinriktningsmotor och har A4T Analytics konfigurerat för kontot har du en extra listruta för **Rapportkälla**:

![chlimage_1-32](assets/chlimage_1-32.png)

Följande framgångsmått är tillgängliga (används endast för publicering):

<table>
 <tbody>
  <tr>
   <td><strong>Konvertering</strong></td>
   <td><p>Andelen besökare som klickade på någon del av upplevelsen som testades. En konvertering kan antingen räknas en gång per besökare eller varje gång en besökare slutför en konvertering. Konverteringsmåttet är inställt på något av följande:</p>
    <ul>
     <li><strong>Visad sida</strong> - Du kan definiera vilken sida publiken ska se genom att välja antingen <strong>URL är</strong> och sedan definiera URL:en eller flera URL:er, eller genom att markera <strong>URL innehåller</strong> och sedan lägga till en sökväg eller ett nyckelord.</li>
     <li><strong>Visad mbox</strong> - Du kan definiera vilken mbox publiken ska visa genom att ange namnet på mbox. Du kan ange flera kryssrutor genom att klicka <strong>Lägg till en Mbox</strong>.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Intäkter</strong></td>
   <td><p>Intäkter från besöket. Du kan välja mellan följande intäktsmått:</p>
    <ul>
     <li>Intäkter per besökare</li>
     <li>Genomsnittligt ordervärde (AOV)</li>
     <li>Total försäljning </li>
     <li>Beställningar</li>
    </ul> <p>För något av dessa alternativ anger om en mbox visades att målet har nåtts. Du kan definiera mbox eller flera mbox.</p> </td>
  </tr>
  <tr>
   <td><strong>Engagemang</strong></td>
   <td><p>Ni kan mäta tre typer av engagemang:</p>
    <ul>
     <li>Sidvyer</li>
     <li>Anpassad poängsättning</li>
     <li>Tid på plats</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

Dessutom finns det avancerade inställningar som gör att du kan avgöra hur många framgångsmått som ska räknas. Du kan välja att räkna måtten per intryck eller en gång per besökare och välja om användaren ska vara kvar i aktiviteten eller ta bort dem.

Använd de avancerade inställningarna för att avgöra vad som händer **efter** när en användare påträffar målmåttet. I följande tabell visas de tillgängliga alternativen.

<table>
 <tbody>
  <tr>
   <td><strong>När en användare har påträffat detta målmått..</strong></td>
   <td><strong>Du väljer att följande ska hända..</strong></td>
  </tr>
  <tr>
   <td><strong>Öka antal och behåll användare i aktivitet</strong></td>
   <td>Ange hur antalet ska ökas:
    <ul>
     <li>En gång per deltagare</li>
     <li>Vid varje intryck, exklusive siduppdatering</li>
     <li>På varje intryck</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Ökning, frigör användare och Tillåt återinträde</strong></td>
   <td>Välj den upplevelse besökaren ser om de återupptar aktiviteten:
    <ul>
     <li>Samma upplevelse</li>
     <li>Slumpmässig erfarenhet</li>
     <li>Osynlig upplevelse</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Ökningsantal, frigör återinträde av användare och fält</strong></td>
   <td>Bestäm vad användaren ser i stället för aktivitetsinnehållet:
    <ul>
     <li>Samma upplevelse, utan spårning</li>
     <li>Standardinnehåll eller annat aktivitetsinnehåll</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

Se [Adobe Target-dokumentation](https://experienceleague.adobe.com/docs/target/using/activities/success-metrics/success-metrics.html) för mer information om framgångsmått.

### Konfigurera inställningar (AEM) {#configuring-settings-aem-targeting}

Så här konfigurerar du inställningar om du använder AEM mål:

1. Om du vill ange när aktiviteten ska starta använder du **Starta** i den nedrullningsbara menyn för att välja något av följande värden:

   * **Vid aktivering**: Aktiviteten startar när sidan som innehåller målinnehållet aktiveras.
   * **Angivet datum och tid**: En viss tid. När du väljer det här alternativet klickar eller trycker du på kalenderikonen, väljer ett datum och anger vilken tid aktiviteten ska starta.

1. Om du vill ange när aktiviteten ska sluta använder du **End** i den nedrullningsbara menyn för att välja något av följande värden:

   * **Vid inaktivering**: Aktiviteten avslutas när sidan som innehåller målinnehållet inaktiveras.
   * **Angivet datum och tid**: En viss tid. När du väljer det här alternativet klickar eller trycker du på kalenderikonen, väljer ett datum och anger tidpunkten för att avsluta aktiviteten.

1. Om du vill ange en prioritet för aktiviteten använder du skjutreglaget och väljer antingen **Låg**, **Normal**, eller **Hög**.

### Konfigurera mål och inställningar (Adobe Target) {#configuring-goals-settings-adobe-target}

Så här konfigurerar du mål och inställningar för Adobe Target:

1. Om du vill ange när aktiviteten ska starta använder du **Starta** i den nedrullningsbara menyn för att välja något av följande värden:

   * **Vid aktivering**: Aktiviteten startar när sidan som innehåller målinnehållet aktiveras.
   * **Angivet datum och tid**: En viss tid. När du väljer det här alternativet klickar eller trycker du på kalenderikonen, väljer ett datum och anger vilken tid aktiviteten ska starta.

1. Om du vill ange när aktiviteten ska sluta använder du **End** i den nedrullningsbara menyn för att välja något av följande värden:

   * **Vid inaktivering**: Aktiviteten avslutas när sidan som innehåller målinnehållet inaktiveras.
   * **Angivet datum och tid**: En viss tid. När du väljer det här alternativet klickar eller trycker du på kalenderikonen, väljer ett datum och anger tidpunkten för att avsluta aktiviteten.

1. Om du vill ange en prioritet för aktiviteten använder du skjutreglaget och väljer antingen **Låg**, **Normal**, eller **Hög**.
1. Om du har konfigurerat Adobe Analytics med ditt Adobe Target-konto kan du se **Rapporteringskälla** listruta. Välj **Adobe Target** eller **Adobe Analytics** som källa.

   Om du väljer **Adobe Analytics**, väljer företaget och rapporterar programsviten. Om du väljer **Adobe Target**, ingen åtgärd krävs.

   ![chlimage_1-33](assets/chlimage_1-33.png)

1. I området **Målmått**, under **Mitt primära mål** väljer du det framgångsmått som du vill spåra – som konvertering, intäkter eller engagemang – och anger hur mätningen görs (eller vilka åtgärder målgruppen vidtar för att ange att ett mål har nåtts). Definitioner av målmått anges i föregående tabell och [Adobe Target-dokumentationen](https://experienceleague.adobe.com/docs/target/using/activities/success-metrics/success-metrics.html) innehåller mer information om framgångsmått.

   Du kan byta namn på målet genom att klicka på de tre punkterna i det övre högra hörnet och välja **Byt namn**.

   Om du vill rensa alla fält klickar du på de tre punkterna i det övre högra hörnet och väljer **Rensa alla fält**.

   Alla mätvärden har också avancerade inställningar som du kan definiera. Välj **Avancerade inställningar** för att få tillgång till dem. Se en definition av hur framgångsmått räknas i föregående tabell och se [Adobe Target-dokumentation](https://experienceleague.adobe.com/docs/target/using/activities/success-metrics/success-metrics.html).

   >[!NOTE]
   >
   Du måste ha minst ett definierat mål.

   ![chlimage_1-34](assets/chlimage_1-34.png)

   >[!NOTE]
   >
   Om det saknas information i måttet omges mätningen av en röd linje.

1. Klicka **Lägg till ett nytt mått** för att konfigurera ytterligare framgångsmått.

   ![chlimage_1-35](assets/chlimage_1-35.png)

   >[!NOTE]
   >
   Du kan ta bort ytterligare mål genom att klicka eller trycka på de tre punkterna och klicka eller trycka på **Ta bort**. AEM kräver att du har minst ett definierat mål.

1. Om du vill ha mer kontroll över hur framgångsvärdena räknas klickar du på **Avancerade inställningar** för att få tillgång till dem.
1. Klicka **Spara**.

När du har konfigurerat kan du [visa hur dina aktiviteter fungerar](/help/sites-authoring/activitylib.md#viewing-performance-and-converting-winning-experiences-a-b-test) som använder Adobe Target (antingen upplevelse eller A/B-testmål). Dessutom kan ni med A/B-testanpassning [konvertera vinnarna.](/help/sites-authoring/activitylib.md#viewing-performance-and-converting-winning-experiences-a-b-test)

## Simulera en upplevelse {#simulating-an-experience}

Simulera en besökares upplevelse för att verifiera att sidinnehållet visas som förväntat enligt designen för det valda innehållet. När du simulerar läser du in olika användarprofiler och ser målinnehållet för den användaren.

Följande kriterier avgör vilket innehåll som visas när en besökares upplevelse simuleras:

* Data i användarens sessionsarkiv (via kontextnavet).
* The [Aktiviteter som är på](/help/sites-authoring/activitylib.md).
* The [regler som definierar segment](/help/sites-administering/campaign-segmentation.md).
* Innehållet i upplevelserna i Target-komponenterna.
* The [konfiguration av målmotorn](/help/sites-authoring/activitylib.md).

Om oväntat innehåll visas på sidan när du läser in en profil kontrollerar du konfigurationen för varje objekt i listan.

>[!NOTE]
>
Om ni använder A/B-testning visas upplevelser baserat på trafikprocenten när ni simulerar upplevelser. Detta styrs av Adobe Target, vilket kan leda till oväntade resultat för författare. (Aktiviteten _author synkroniseras med specifika inställningar som tillåter omvärdering under simulering.) Författare kan behöva uppdatera för att se de andra upplevelserna baserat på deras trafikinställningar.

Använd följande verktyg för att simulera besökarens upplevelse:

* Simuleringsaktivitet i målläge: Sidan visar erbjudanden för användaren som är markerad i kontextnavet. Du kan redigera erbjudanden som riktar sig till användaren.
* Förhandsgranskningsläge: Använd kontextnavet för att välja de användare och platser som uppfyller villkoren för de segment som era upplevelser baseras på. När dina kontextnavmarkeringar ändras, ändras målinnehållet i enlighet med detta.

1. Om du vill växla till förhandsgranskningsläget klickar eller trycker du på i verktygsfältet **Förhandsgranska**.
1. Klicka på eller tryck på ikonen för snabbpanelen i verktygsfältet.

   ![Kontextnav](do-not-localize/chlimage_1-7.png)

1. Använd kontextnavet för att ändra kontextegenskaper. Du kan till exempel klicka på eller trycka på egenskapen Persona för att välja en annan användare.

   ![chlimage_1-36](assets/chlimage_1-36.png)

   Sidan ändras för att visa innehållet som är avsett för den aktuella kontexten.

1. Om du vill ändra erbjudandena som visas växlar du till målläget. När simuleringsaktiviteten är markerad redigerar du erbjudandena för den kontext som du konfigurerade i förhandsgranskningsläget.

## Konfigurera alternativ för målkomponent {#configuring-target-component-options}

Du kan anpassa Target-komponenten genom att komma åt komponentens alternativ på ett av två sätt:

1. När du har angett komponenten som mål klickar eller trycker du på komponenten i Target och sedan på inställningsikonen (cog).

   ![Meny för målkomponent](do-not-localize/chlimage_1-8.png)

   AEM visar fönstret Alternativ för målkomponent.

   ![chlimage_1-37](assets/chlimage_1-37.png)

1. Du kan även komma åt dessa inställningar i helskärmsläge genom att klicka på eller trycka på helskärmsikonen i alternativfönstret för målkomponenten.

   ![Alternativ för målkomponent](do-not-localize/chlimage_1-9.png)

   AEM visar alternativfönstret för målkomponenten i helskärmsläge.

   ![chlimage_1-38](assets/chlimage_1-38.png)

1. Konfigurera inställningarna för målkomponenten enligt beskrivningen i följande tabeller.

<table>
 <tbody>
  <tr>
   <td><strong>Alternativ</strong></td>
   <td><strong>Beskrivning</strong></td>
  </tr>
  <tr>
   <td><strong>Plats</strong></td>
   <td><p>Platsen är en sträng som ger målinnehållsplatsen ett namn och kopplar erbjudanden till platser (eller platser eller komponenter) på sidan där erbjudandena ska placeras.</p> <p>Det här fältet är ett generiskt värde.</p> <p>Om du lägger ett erbjudande i en komponent kommer erbjudandet ihåg plats-ID:t. När sidan körs utvärderar motorn användarens segment och utifrån detta löser den upplevelsen från de aktiva kampanjer som ska visas. Sedan kontrolleras plats-ID:n på sidan och försöker matcha erbjudanden med dessa plats-ID:n till dem.</p> </td>
  </tr>
  <tr>
   <td><strong>Motor</strong></td>
   <td>Välj mellan <strong>Regler för klientsidan (utan spårning), Adobe Target, ContextHub, </strong>och<strong> Adobe Campaign </strong>beroende på vilken motor du vill använda.</td>
  </tr>
 </tbody>
</table>

Om du väljer Adobe Target som motor:

![chlimage_1-39](assets/chlimage_1-39.png)

<table>
 <tbody>
  <tr>
   <td><strong>Alternativ</strong></td>
   <td><strong>Beskrivning</strong></td>
  </tr>
  <tr>
   <td><strong>Korrekt målinriktning</strong></td>
   <td><p>Om du aktiverar korrekt målinriktning anger du att komponenten ska vänta på att klientkontext eller kontextnav ska vara tillgängliga innan begäran skickas till Adobe Target. Det kan öka inläsningstiden. För redigering är korrekt målinriktning alltid aktiverat.</p> <p>Om du väljer <strong>Korrekt målinriktning</strong> kryssruta, mbox utför en <code>mboxDefine</code> först och en <code>mboxUpdate</code> resulterar senare i en Ajax-begäran när informationen är tillgänglig.</p> <p>Om du inte markerar <strong>Korrekt målinriktning</strong> kryssruta, mbox utför en <code>mboxCreate</code> vilket resulterar i en synkron begäran direkt (i det här fallet är inte alla kontextdata tillgängliga än).</p> <p><strong>Obs!</strong> Om du aktiverar eller inaktiverar korrekt målinriktning för en viss komponent påverkas inte inställningarna som du har angett globalt. Du kan alltid åsidosätta globala inställningar genom att välja Korrekt målanpassning i komponenten.</p> </td>
  </tr>
  <tr>
   <td><strong>Inkludera lösta segment</strong></td>
   <td><p>Om du markerar den här kryssrutan inkluderas alla lösta segment i mbox-anropet och alla parametrar som har konfigurerats på sidan och i ramverket.</p> <p>Detta fungerar bara i situationer med XML API där du synkroniserar AEM segment. Om du har segment i AEM som inte hanteras av Adobe Target (som skriptsegment) kan du med det här alternativet lösa segmentet i AEM och skicka information till Adobe Target om att segmentet är aktivt.</p> </td>
  </tr>
  <tr>
   <td><strong>Ärvda kontextparametrar</strong></td>
   <td>Visar kontextparametrar som ärvts från Adobe Target-ramverket, om sådana finns, och som är kopplade till den valda sidan.</td>
  </tr>
  <tr>
   <td><strong>Kontextparametrar</strong></td>
   <td>Klicka eller tryck <strong>Lägg till fält</strong> om du vill konfigurera ytterligare kontextparametrar (samma som i Target Framework). Kontextparametrar som lagts till i komponenten används <i>endast</i> till komponenten och inte till andra komponenter, vilket skulle vara fallet om du lade till sammanhangsparametrar direkt i ramverket.</td>
  </tr>
  <tr>
   <td><strong>Statiska parametrar</strong></td>
   <td>Klicka eller tryck <strong>Lägg till fält</strong> för att konfigurera ytterligare statiska parametrar (samma som finns i Target Framework). Statiska parametrar som lagts till i komponenten används <i>endast</i> till komponenten och inte till andra komponenter, vilket skulle vara fallet om du lade till statiska parametrar direkt i ramverket. Statiska parametrar kommer inte från kontext (klientkontext för innehållsnavet).</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
När du markerar en komponent och gör den målbar, ersätter AEM även komponenten och injicerar en Adobe Target-komponent. (Adobe Target-komponenten används inte bara när du lägger till den manuellt på sidan, utan även när du aktiverar en befintlig komponent.)

Om du väljer Klientkontext (klientsidan) som motor:

![chlimage_1-40](assets/chlimage_1-40.png)

<table>
 <tbody>
  <tr>
   <td><strong>Alternativ</strong></td>
   <td><strong>Beskrivning</strong></td>
  </tr>
  <tr>
   <td><strong>Alternativ för kundsidan - strategi</strong></td>
   <td><p>Välj något av följande:</p>
    <ul>
     <li><strong>Första</strong>: Den främsta upplevelsen i listan enligt kampanjens beställning.</li>
     <li><strong>Slumpmässig</strong>: Alla upplevelser används.</li>
     <li><strong>ClickStream-bakgrundsmusik</strong>: Taggarna och tillhörande taggträffar som spåras i klientkontexten används. Träffarna för de taggar som definieras på scensidan jämförs.</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

Du väljer **Adobe Campaign** som motor om du integrerar AEM med Adobe Campaign. Se [Integrera AEM med Adobe Campaign](/help/sites-administering/campaign.md) för mer information.

Välj **ContextHub** som motor om du använder ContextHub för målinriktning. Se [ContextHub konfigureras.](/help/sites-developing/ch-configuring.md)
