---
title: Översätter användargenererat innehåll
seo-title: Översätter användargenererat innehåll
description: Översättningsfunktionen fungerar
seo-description: Översättningsfunktionen fungerar
uuid: 7ee3242c-2aca-4787-a60d-b807161401ad
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: bfaf80c5-448b-47fb-9f22-57ee0eb169b2
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Översätter användargenererat innehåll {#translating-user-generated-content}

Översättningsfunktionen för AEM Communities vidgar begreppet [översättning av sidinnehåll](../../help/sites-administering/translation.md) till det användargenererade innehåll (UGC) som publiceras på communitysajter med hjälp av [komponenter](scf.md)i det sociala ramverket.

Översättningen av UGC gör att besökare och medlemmar kan uppleva en global community genom att ta bort språkhinder.

Anta till exempel att

* En fransk ledamot publicerar ett franskt recept på en internationell matlagningswebbplats
* En annan medlem från Japan använder översättningsfunktionen för att utlösa översättningen av recept från franska till japanska
* Efter att ha läst receptet på japanska lägger medlemmen från Japan sedan in en kommentar på japanska
* Medlemmen från Frankrike använder översättningsfunktionen för att översätta den japanska kommentaren till franska
* Global kommunikation!

## Översikt {#overview}

I det här avsnittet av dokumentationen beskrivs särskilt hur översättningstjänsten fungerar med UGC samtidigt som man antar en förståelse för hur AEM kan anslutas till en [översättningstjänstleverantör](../../help/sites-administering/translation.md#connectingtoatranslationserviceprovider) och integreras i en webbplats genom att konfigurera ett [ramverk](../../help/sites-administering/tc-tic.md)för översättningsintegrering.

När en översättningstjänstleverantör är associerad med webbplatsen behåller varje språkkopia av webbplatsen sina egna UGC-trådar som publicerats via SCF-komponenter, till exempel kommentarer.

När ett ramverk för översättningsintegrering har konfigurerats utöver översättningstjänstleverantören, är det möjligt för varje språkkopia av webbplatsen att dela en enda tråd av UGC, vilket ger global kommunikation över språkversioner. I stället för en diskussionstråd som är uppdelad efter språk gör den konfigurerade [globala delade lagringsplatsen](#global-translation-of-ugc) att hela tråden visas oavsett vilket språk den visas på. Dessutom kan flera översättningsintegrationskonfigurationer konfigureras med olika globala delade arkiv för en logisk gruppering av globala deltagare, t.ex. efter regioner.

## Standardöversättningstjänsten {#the-default-translation-service}

AEM Communities levereras med en [testlicens](../../help/sites-administering/tc-msconf.md#microsoft-translator-trial-license) för en [standardöversättningstjänst](../../help/sites-administering/tc-msconf.md) som är aktiverad för flera språk.

När du [skapar en communitywebbplats](sites-console.md)aktiveras standardöversättningstjänsten när `Allow Machine Translation` markeras från [underpanelen TRANSLATION](sites-console.md#translation) .

>[!CAUTION]
>
>Standardöversättningstjänsten är endast till för demonstration.
>
>För ett produktionssystem krävs en licensierad översättningstjänst. Om den inte är licensierad bör standardöversättningstjänsten [inaktiveras](../../help/sites-administering/tc-msconf.md#microsoft-translator-trial-license-geometrixx-outdoors).

## Global översättning av användargenererat innehåll {#global-translation-of-ugc}

När en webbplats har flera [språkkopior](../../help/sites-administering/tc-prep.md)känner inte standardöversättningstjänsten igen att UGC som anges på en webbplats kan vara relaterat till UGC som anges på en annan, som när UGC i stort sett genereras av samma komponent (språkkopian av sidan som innehåller komponenten).

Det liknar grupper av människor som diskuterar en fråga som inte känner till att kommentarer görs i andra grupper än deras egna, jämfört med alla i en stor grupp som deltar i en konversation.

Om du vill kan du aktivera global översättning för en webbplats med flera språkkopior, så att hela tråden visas oavsett vilket språk den visas på.

Om t.ex. ett forum har skapats på baswebbplatsen, språkkopior har skapats och global översättning har aktiverats, visas ett ämne som publicerats på forumet i en språkkopia på alla språkkopior. Detsamma gäller för alla svar, oavsett vilket språk svaret skrevs från. Resultatet skulle bli att ämnet och dess hela svarstråd skulle vara synliga oavsett vilket språk som ämnet visas från.

>[!CAUTION]
>
>Eventuell UGC som fanns före den globala översättningen är inte längre synlig.
>
>UGC:n finns fortfarande i den [gemensamma lagringsplatsen](working-with-srp.md), men finns under den språkspecifika UGC-platsen, medan nytt innehåll, som lagts till efter att den globala översättningen konfigurerats, hämtas från den globala delade lagringsplatsen.
>
>Det finns inget migreringsverktyg för att flytta eller sammanfoga språkspecifikt innehåll i det globala delade arkivet.

### Konfiguration av översättningsintegrering {#translation-integration-configuration}

Så här skapar du en ny översättningsintegrering, som integrerar en översättningstjänstkoppling med webbplatsen på författarinstansen:

* Logga in som administratör
* Från [huvudmenyn](http://localhost:4502/)
* Välj **[!UICONTROL verktyg]**
* Välj **[!UICONTROL åtgärder]**
* Välj **[!UICONTROL moln]**
* Välj **[!UICONTROL molntjänster]**
* Bläddra ned till **[!UICONTROL Översättningsintegrering]**

![chlimage_1-65](assets/chlimage_1-65.png)

* Välj **[!UICONTROL Visa konfigurationer]**

![chlimage_1-66](assets/chlimage_1-66.png)

* Välj `[+]` ikon bredvid **[!UICONTROL Tillgängliga konfigurationer]** för att skapa en ny konfiguration

#### Dialogrutan Skapa konfiguration {#create-configuration-dialog}

![chlimage_1-67](assets/chlimage_1-67.png)

* **[!UICONTROL Överordnad konfiguration]**(obligatoriskt) finns vanligtvis kvar som standard. Standardvärdet är `/etc/cloudservices/translation`.

* **[!UICONTROL Titel]**(obligatoriskt) Ange en visningsrubrik. Inget standardvärde.

* **[!UICONTROL Namn]**(valfritt) Ange ett namn för konfigurationen. Standard är ett nodnamn som baseras på titeln.

* Välj **[!UICONTROL Skapa]**

#### Dialogrutan Översättningskonfiguration {#translation-config-dialog}

![chlimage_1-68](assets/chlimage_1-68.png)

Detaljerade instruktioner finns på [Skapa en konfiguration för översättningsintegrering](../../help/sites-administering/tc-tic.md#creating-a-translation-integration-configuration)

* **[!UICONTROL Fliken Platser]** : kan lämna som standard
* **[!UICONTROL Fliken Communities]** :
   * **[!UICONTROL Översättningsprovider]** Välj översättningsleverantör i listrutan. Standard är `microsoft`testversionen.

   * **[!UICONTROL Innehållskategori]** Välj en kategori som beskriver innehållet som översätts. Standard är `General.`

   * ****Välj språkinställning...
(Valfritt) Genom att välja en språkinställning för lagring av UGC, visas inlägg från alla språkkopior i en global konversation. Välj språkinställning som [basspråk](sites-console.md#translation) för webbplatsen. Om du väljer `No Common Store` inaktiveras den globala översättningen. Som standard är global översättning inaktiverat.

* **[!UICONTROL Fliken Resurser]** : kan lämna som standard
* Välj **[!UICONTROL OK]**

#### Aktivering {#activation}

Den nya översättningsintegreringens molntjänst måste aktiveras i publiceringsmiljön. Om aktiveringsarbetsflödet är kopplat till en webbplats och ännu inte är aktiverat, uppmanas du att publicera molntjänstkonfigurationen när sidan som den är kopplad till publiceras.

## Hantera översättningsinställningar {#managing-translation-settings}

>[!NOTE]
>
>**Önskat språk**
>
>För att man ska kunna se om posten är på ett annat språk än det språk besökaren föredrar måste det språk som besökaren föredrar fastställas.
>
>Det språk som föredras är språkinställningen som anges i en användarprofil när besökaren är inloggad och har angett en språkinställning.
>
>När besökaren är anonym eller inte har angett någon språkinställning i sin profil är det språk som används som standard i sidmallen.

### Användarinställningar {#user-preference}

#### Användarprofil {#user-profile}

Alla communityplatser har en användarprofil som inloggade medlemmar kan redigera för att identifiera sig för communityn och för att ange sina inställningar.

En sådan inställning är om communityinnehåll alltid ska visas på det språk de föredrar. Som standard är inställningen inte inställd och används som standard för systeminställningen. Användaren kan ändra inställningen till På eller Av och därigenom åsidosätta systeminställningen.

När sidor automatiskt översätts till det språk som användaren föredrar är gränssnittet för att visa originaltexten och förbättra översättningen fortfarande tillgängligt.

![chlimage_1-69](assets/chlimage_1-69.png)

### Inställningar för communityplats {#community-site-setting}

När en Community-webbplats skapas kan översättningsalternativet aktiveras och konfigureras. Översättningsinställningen används för innehåll som anonyma webbplatsbesökare kan visa, men den åsidosätts av användarens profilinställning.
