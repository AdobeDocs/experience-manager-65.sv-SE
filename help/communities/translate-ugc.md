---
title: Översätter användargenererat innehåll
description: Lär dig hur översättningen av UGC-innehåll gör att webbplatsbesökare och medlemmar kan uppleva en global community genom att ta bort språkhinder.
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
role: Admin
exl-id: ac54f06e-1545-44bb-9f8f-970f161ebb72
source-git-commit: b8887b4a6f757352e9dbfdf074c10e9ccd6dbd4f
workflow-type: tm+mt
source-wordcount: '1085'
ht-degree: 0%

---

# Översätter användargenererat innehåll {#translating-user-generated-content}

Översättningsfunktionen för Adobe Experience Manager (AEM) Communities utökar begreppet [översätta sidinnehåll](../../help/sites-administering/translation.md) till det användargenererade innehåll (UGC) som publicerats på communitysajter med [komponenter i ramverket för sociala komponenter (SCF)](scf.md).

Översättningen av UGC gör att besökare och medlemmar kan uppleva en global community genom att ta bort språkhinder.

Anta till exempel:

* En fransk ledamot publicerar ett recept på franska i communityforumet på en internationell matlagningswebbplats.
* En annan medlem från Japan använder översättningsfunktionen för att utlösa översättningen av recept från franska till japanska.
* Efter att ha läst receptet på japanska lägger medlemmen från Japan sedan in en kommentar på japanska.
* Medlemmen från Frankrike använder översättningsfunktionen för att översätta den japanska kommentaren till franska.
* Global kommunikation.

## Översikt {#overview}

I det här avsnittet beskrivs hur översättningstjänsten fungerar med UGC. Det förutsätter också att du har en förståelse för hur du ansluter AEM till en [översättningstjänst](../../help/sites-administering/translation.md#connectingtoatranslationserviceprovider) och integrera tjänsten i en webbplats genom att konfigurera en [översättningsintegreringsramverk](../../help/sites-administering/tc-tic.md).

När en översättningstjänstleverantör är associerad med webbplatsen behåller varje språkkopia av webbplatsen sina egna UGC-trådar som publicerats via SCF-komponenter, till exempel kommentarer.

När en översättningsintegrering har konfigurerats utöver översättningstjänstleverantören, är det möjligt för varje språkkopia av webbplatsen att dela en enda tråd av UGC, vilket ger global kommunikation över språkkopiorna. I stället för en diskussionstråd som är uppdelad efter språk konfigureras den [globalt delat arkiv](#global-translation-of-ugc) gör att hela tråden visas oavsett vilket språk den visas på. Dessutom kan flera översättningsintegrationskonfigurationer konfigureras med olika globala delade arkiv för en logisk gruppering av globala deltagare, t.ex. efter regioner.

## Standardöversättningstjänsten {#the-default-translation-service}

AEM Communities innehåller [testlicens](../../help/sites-administering/tc-msconf.md#microsoft-translator-trial-license) för [standardöversättningstjänst](../../help/sites-administering/tc-msconf.md) aktiveras för flera språk.

När [skapa en communitywebbplats](sites-console.md)är standardöversättningstjänsten aktiverad när `Allow Machine Translation` är markerad från [ÖVERSÄTTNING](sites-console.md#translation) underpanel.

>[!CAUTION]
>
>Standardöversättningstjänsten är endast till för demonstration.
>
>För ett produktionssystem krävs en licensierad översättningstjänst. Om den inte är licensierad bör standardöversättningstjänsten [inaktiverad](../../help/sites-administering/tc-msconf.md#microsoft-translator-trial-license-geometrixx-outdoors).

## Global översättning av användargenererat innehåll {#global-translation-of-ugc}

När en webbplats har flera [språkversioner](../../help/sites-administering/tc-prep.md), känner inte standardöversättningstjänsten igen att den UGC som anges på en plats kan vara relaterad till den UGC som anges på en annan plats. Detta gäller när UGC genereras av samma komponent (språkkopian av sidan som innehåller komponenten).

Det liknar grupper av människor som diskuterar ett ämne. De är inte medvetna om kommentarer som görs i andra grupper än de egna, jämfört med alla som deltar i en konversation i en stor grupp.

Om du vill kan du aktivera global översättning för en webbplats med flera språkkopior, så att hela tråden visas oavsett vilket språk den visas på.

Om ett forum till exempel har skapats på baswebbplatsen, språkkopior som har skapats och global översättning har aktiverats, visas ett ämne som har publicerats på forumet i en språkkopia på alla språkkopior. Detsamma gäller för alla svar, oavsett vilket språk svaret skrevs från. Resultatet skulle bli att ämnet och dess hela svarstråd skulle vara synliga oavsett vilket språk som ämnet visas från.

>[!CAUTION]
>
>Eventuell UGC som fanns före global översättning är inte längre synlig.
>
>Medan användargenerationen fortfarande finns i [gemensam lagringsplats](working-with-srp.md), finns den under den språkspecifika UGC-platsen, medan nytt innehåll, som läggs till efter att global översättning har konfigurerats, hämtas från den globala delade lagringsplatsen.
>
>Det finns inget migreringsverktyg för att flytta eller sammanfoga språkspecifikt innehåll i det globala delade arkivet.

### Konfiguration av översättningsintegrering {#translation-integration-configuration}

Så här skapar du en översättningsintegrering, som integrerar en översättningstjänstkoppling med webbplatsen på författarinstansen:

* Logga in som administratör
* Från [huvudmeny](http://localhost:4502/)
* Välj **[!UICONTROL Tools]**
* Välj **[!UICONTROL Operations]**
* Välj **[!UICONTROL Cloud]**
* Välj **[!UICONTROL Cloud Services]**
* Bläddra nedåt till **[!UICONTROL Translation Integration]**

  ![translation-integration](assets/translation-integration.png)

* Välj **[!UICONTROL Show Configurations]**

  ![show-configuration](assets/translation-integration1.png)

* Välj `[+]` ikon bredvid **[!UICONTROL Available Configurations]** så att du kan skapa en konfiguration.

#### Dialogrutan Skapa konfiguration {#create-configuration-dialog}

![create-configuration](assets/translation-integration2.png)

* **[!UICONTROL Parent Configuration]**

  (Obligatoriskt) Lämna normalt som standard. Standard är `/etc/cloudservices/translation`.

* **[!UICONTROL Title]**

  (Obligatoriskt) Ange en visningsrubrik. Inget standardvärde.

* **[!UICONTROL Name]**

  (Valfritt) Ange ett namn för konfigurationen. Standard är ett nodnamn som baseras på titeln.

* Välj **[!UICONTROL Create]**

#### Dialogrutan Översättningskonfiguration {#translation-config-dialog}

![configuration-dialog](assets/translation-integration3.png)

Detaljerade anvisningar finns i [Skapa en konfiguration för översättningsintegrering](../../help/sites-administering/tc-tic.md#creating-a-translation-integration-configuration).

* **[!UICONTROL Sites]** tab: can leave as default.

* **[!UICONTROL Communities]** tab:
   * **[!UICONTROL Translation Provider]**
Välj översättningsleverantör i listrutan. Standard är `microsoft`, testversionen.

   * **[!UICONTROL Content Category]**
Välj en kategori som beskriver innehållet som översätts. Standard är `General.`

   * **[!UICONTROL Choose A Locale...]**
(Valfritt) Genom att välja en språkinställning för lagring av UGC, visas inlägg från alla språkkopior i en global konversation. Välj språkområde för [basspråk](sites-console.md#translation) för webbplatsen. Välja `No Common Store` inaktiverar global översättning. Som standard är global översättning inaktiverat.

* **[!UICONTROL Assets]** tab: can leave as default.
* Välj **[!UICONTROL OK]**

#### Aktivering {#activation}

Den nya översättningsintegreringens molntjänst måste aktiveras i publiceringsmiljön. Om aktiveringsarbetsflödet är kopplat till en webbplats och ännu inte är aktiverat, uppmanas det att publicera molntjänstkonfigurationen när sidan som den är kopplad till publiceras.

## Hantera översättningsinställningar {#managing-translation-settings}

>[!NOTE]
>
>**Önskat språk**
>
>När man upptäcker om posten är på ett annat språk än det önskade språket måste besökarens föredragna språk fastställas.
>
>Det språk som föredras är språkinställningen som anges i en användarprofil när besökaren är inloggad och har angett en språkinställning.
>
>När besökaren är anonym eller inte har angett någon språkinställning i sin profil är det språk som används som standard i sidmallen.

### Användarinställningar {#user-preference}

#### Användarprofil {#user-profile}

Alla webbgruppsplatser har en användarprofil som inloggade medlemmar kan redigera för att identifiera sig för communityn och för att ange sina inställningar.

En sådan inställning är om communityinnehåll alltid ska visas på det språk de föredrar. Som standard är inställningen inte inställd och standardinställningen är systeminställningen. Användaren kan ändra inställningen till På eller Av för att åsidosätta systeminställningen.

När sidor automatiskt översätts till det språk som användaren föredrar är gränssnittet för att visa originaltexten och förbättra översättningen fortfarande tillgängligt.

![användarprofil](assets/translation-integration4.png)

### Inställningar för communityplats {#community-site-setting}

När en Community-webbplats skapas kan översättningsalternativet aktiveras och konfigureras. Översättningsinställningen används för innehåll som anonyma webbplatsbesökare kan visa, men den åsidosätts av användarens profilinställning.
