---
title: Versionsinformation för [!DNL Adobe Experience Manager] 6.5
description: Hitta versionsinformation, nyheter, installationsanvisningar och en detaljerad ändringslista för [!DNL Adobe Experience Manager] 6.5.
mini-toc-levels: 3
exl-id: 0288aa12-8d9d-4cec-9a91-7a4194dd280a
source-git-commit: 48f898a774d2ddd6d2c31f6a4107c71e4032cfc2
workflow-type: tm+mt
source-wordcount: '3206'
ht-degree: 0%

---

# [!DNL Adobe Experience Manager] 6.5 Versionsinformation om senaste Service Pack {#aem-service-pack-release-notes}

<!-- For an itemized list of all issues found in these release notes, see the following spreadsheet: https://adobe-my.sharepoint.com/:x:/r/personal/anujkapo_adobe_com/_layouts/15/Doc.aspx?sourcedoc=%7B3ea81ae4-e605-4153-b132-f2698c86f84e%7D&action=edit&wdinitialsession=d8c7b903-87fc-4f2d-9ef2-542a82169570&wdrldsc=3&wdrldc=1&wdrldr=SessionMemoryQuotaExceededDuringSession&cid=a915e87c-369a-480c-9daf-d13efc766798 -->

## Versionsinformation {#release-information}

| Produkt | [!DNL Adobe Experience Manager] 6.5 |
| -------- | ---------------------------- |
| Version | 6.5.14.0 <!-- UPDATE FOR EACH NEW RELEASE --> |
| Typ | Service Pack-version |
| Date | 25 augusti 2022 <!-- UPDATE FOR EACH NEW RELEASE --> |
| Hämta URL | [Programvarudistribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.14.0.zip) <!-- UPDATE FOR EACH NEW RELEASE --> |

## Vad ingår i [!DNL Experience Manager] 6.5.14.0 {#what-is-included-in-aem-6514}

[!DNL Experience Manager] 6.5.14.0 innehåller nya funktioner, viktiga förbättringar som kunderna efterfrågat, felkorrigeringar, prestanda, stabilitet och säkerhetsförbättringar som släppts sedan den första tillgängligheten av 6.5 i april 2019. [Installera detta Service Pack](#install) på [!DNL Experience Manager] 6.5. <!-- UPDATE FOR EACH NEW RELEASE -->

<!-- Some of the key features and improvements are the following:

* _REVIEWERS: WHAT ARE THE KEY FEATURES AND ENHANCEMENTS YOU WANT TO HIGHLIGHT IN THIS RELEASE?_

* Added support for password reset for Dynamic Media Classic users within Experience Manager. (ASSETS-10298) -->

<!-- UPDATE BELOW FOR EACH NEW RELEASE -->

## [!DNL Assets] {#assets-6514}

* Det går inte att lägga till eller visa taggar för PDF-filer. (NPR-38452)
* När du konfigurerar anslutna resurser, sparar konfigurationen, öppnar konfigurationssidan igen och testar den redan sparade konfigurationen misslyckas testanslutningen. (NPR-38507)
* Det går inte att lägga till användare med numeriskt användar-ID i samlingar. (NPR-38538)
* Experience Manager kan inte bearbeta filen FFmpeg som är installerad på författarinstansen. (NPR-38568)
* Bearbetningen av PDF misslyckas med `NoClassDefFoundError` felmeddelande. (NPR-38741)
* Knappen Lägg till under Anpassade kolumner visas inte korrekt när du skapar en resursrapport för `de_DE` språkinställning. (ASSETS-10641)
* När du överför en duplicerad resurs till Digital Asset Management-databasen och Experience Manager identifierar och tillhandahåller ett alternativ för att ta bort den duplicerade resursen, tas även den ursprungliga resursen bort från databasen. (ASSETS-10826)
* Experience Manager sparar inte mappens metadata korrekt när du anger specialtecken i flera fält. (ASSETS-10721)
* Det går inte att spara resursegenskaper förrän du klickar på **[!UICONTROL Save & Close]** två gånger. (ASSETS-12040)
* Skärmläsaren meddelar bara `Relate` -knappen. Men `Relate` -knappen innehåller även en undermeny och kan expanderas och komprimeras. (ASSETS-6938)
* Attribut som krävs för ARIA (Accessible Rich Internet Applications) `aria-expanded` for `role="combo box"` saknas. (ASSETS-6928)
* I kortvyn, i huvudfilens navigeringsområde, textinnehållet **[!UICONTROL Sort by]** har inte minst kontrastförhållandet 4,5:1 mot bakgrundsfärgen. (ASSETS-6926)
* Experience Manager identifierar inte **[!UICONTROL Select a Workflow model]** listrutan som ett obligatoriskt fält när du skapar en arbetsflödesmodell. (ASSETS-6871)

>[!NOTE]
>
>Smarta innehållstjänster kommer inte att vara tillgängliga för nya Experience Manager Assets On-Premise-kunder från och med den 1 september 2022. Ingen påverkan på befintliga kunder med lokal och Adobe Managed Services som redan har den här funktionen aktiverad.

### [!DNL Dynamic Media] {#dynamic-media-6514}

* Lägg till stöd för lösenordsåterställning för Dynamic Media Classic-användare i Experience Manager. (ASSETS-10298)
* Smarta beskärningar som genereras för bilder med genomskinlig bakgrund har vit bakgrund. (ASSETS-13148)
* Dynamic Media genererar inga miniatyrbilder för EPS-filer. (ASSETS-10959)
* Resurser som inte överförs till Dynamic Media-kontot på grund av att en överföringsparameter saknas. (ASSETS-13165)
* Tillåt att resurser med namn som är längre än 127 tecken överförs till Dynamic Media. (ASSETS-9991)
* Aktivera JavaScript ES6 (ECMAScript 6) för Dynamic Media-visningsprogram på Experience Manager 6.5.14.0. (NPR-38393)
* Konfigurera alternativen i Dynamic Media **[!UICONTROL General Settings]** och **[!UICONTROL Publish Setup]** bör inte vara åtkomligt för icke-administratörsanvändare. (ASSETS-8628)
* Dynamic Media **[!UICONTROL General settings]** sidan visar inte de redan konfigurerade överföringsparametrarna korrekt. (ASSETS-10245)
* Experience Manager-användargränssnittet visar inget felmeddelande om det inte går att skapa/uppdatera uppsättningen. (ASSETS-10264)
* Det går inte att använda en sparad princip på någon av behållarna i en redigerbar mall för att lägga till Dynamic Media-komponenter. (ASSETS-11044)
* Resurser som inte överförs till Dynamic Media-kontot efter att arbetsflödet Dynamic Media Reprocess Assets körs på resurser med felaktig jobbreferens. (ASSETS-12084, ASSETS-9877)
* Skärmläsaranvändare påverkas av `title` attribut har inte angetts `<frame>` och `<iframe>` i **[!UICONTROL Type to Search]** -dialogrutan. (ASSETS-5483)
* I skärmläsare, relaterade och meningsfulla `alt=` ska anges för flera bilder som finns under **[!UICONTROL Assets]** i den vänstra rutan. (ASSETS-5644)
* Skärmläsaren läser inte **[!UICONTROL Mute]** och **[!UICONTROL Unmute]** på video med Dynamic Media. (ASSETS-10169)

## Handel {#commerce-6514}

* Handelsprodukter sorteras inte med kolumnrubriken och använder _fjärr_ sorteringsläge, i stället bör Commerce-produkter sorteras med kolumnrubriker med _lokal_ sorteringsläge. (CQ-4343750, NPR-38498)



## [!DNL Forms] {#forms-6514}

<!--

>[!NOTE]
>
> Fixes in [!DNL Experience Manager] Forms are delivered through a separate add-on package a week after the scheduled [!DNL Experience Manager] Service Pack release.

>[!NOTE]
>
>* [!DNL Experience Manager Forms] releases the add-on packages one week after the scheduled [!DNL Experience Manager] Service Pack release date. In this case, the add-on packages will release Thursday, September 1, 2022. In addition, a list of Forms fixes and enhancements will also be added to this section.

-->

* När en fil bifogas till ett adaptivt formulär med flera paneler och ett utkast av det adaptiva formuläret sparas, inträffar ett fel. (NPR-38978)
* När en användare konverterar RGB-profil till CMYK-profil med createPDF2 Java API med Adobe PDF-inställningar fungerar inte alternativet med Java API. Alternativet fungerar bra med det fristående DistillerClient-programmet. (NPR-38858, CQ-4346181)
* När du har installerat AEM 6.5 Forms Service Pack 12 (6.5.12.0) blir alla alternativ utom att stänga uppgiften otillgängliga i steget Tilldela uppgift AEM Arbetsflöden. (NPR-38743)
* I en DoR (Document of Record) trunkeras vissa värden i en tabell. (NPR-38657)
* När du förhandsgranskar FormSet med Data XML och XDP innehåller ett flytande fält visas inga data när du förhandsgranskar en FormSet, men data visas när alternativet Förhandsgranska PDF används.
* I Adaptiv Forms är alternativknappen och kryssrutan inte i tabbordning. (NPR-38645)
* När du använder `Summary Step` om du vill generera en DoR-fil (Document of Record) för ett översatt anpassat formulär efter att formuläret har skickats, översätts inte till det lokaliserade språket. (NPR-38567)
* Alternativet för att inaktivera återförsök AEM arbetsflödesstegen fungerar inte som förväntat. Problemet uppstår ibland. (NPR-38547)
* När adaptiv form skickas med RTF-fält `an Internal Error while Submitting a Form` fel inträffar. När användaren fokuserar på RTF-fältet inträffar inte felet innan formuläret skickas. (NPR-38542)
* Ett fel `sling-default-3-AdobeSignRefreshTokenScheduleJob com.adobe.forms.foundation.oauth.model.OAuthConfigSlingModel Refresh Token not present for: /conf/gws-eform/cashlite/settings/cloudconfigs/fdm/cashlite/jcr:content occurs` loggas. (NPR-38541)
* När en användare överför ett PDF till ett adaptivt formulär slutar AEM Forms-servern att svara. (NPR-38398)
* När du använder API:t för Document Service för att certifiera PDF i en AEM Forms på OSGi-server misslyckas det med felet: com.adobe.fd.signatures.truststore.errors.exception.CredentialRetrievalException: AEM-DSS-311. (CQ-4346252)
* När du skickar in utkastet till breven `Could not upload asset from xml input` fel inträffar. Det påverkar inte funktionaliteten. När du öppnar ett utkast återges brevet korrekt. (CQ-4345979, CQ-4344418)
* När ett datum anges i tyskt format och `Preview with Data` alternativet används för en bokstav och datumfältet återges inte. (CQ-4345783)
* När du skapar en webbportal och genererar streckkoder baserade på data, avkodas vissa streckkoder inte korrekt. (CQ-4345743)
* PostScript-konvertering till PDF återger inte utdatadokument med förväntade färger. (CQ-4345074)
* Resurslösaren orsakar återkommande misslyckade överföringar och resulterar i samma stackspårning som visas flera gånger för en enda sändning. (CQ-4344764)
* Användarna kan inte öppna de ändrade utkasten som använder `cmDataUrl` parameter. Utkasten öppnas bra för första gången. Utgåvorna börjar visas vid efterföljande försök. (CQ-4344418)
* När användaren skriver `&` -symbolen i ett interaktivt meddelande (IC). Motsvarande IC-kort läses inte in. (CQ-4343969)
* När du använder formatalternativ i AEM Forms Designer för att generera PCL-filer används inte det angivna formatet för genererade filer. (CQ-4339573)
* När sidantalet är över 15 misslyckas automatiserad konvertering av dynamiska XDP-formulär till adaptiv form. Detta fungerar bra när sidantalet är mindre än 15. (NPR-35337)
* När alternativet Lägg till i Favoriter används visas inte statusen för växlingen till skärmläsaren. (NPR-37137)
* I formulärdatamodellen trunkeras värdena efter decimalerna i databasbaserade formulärdatamodeller för datatypen pengar och liten kostnad. . (CQDOC-19509)
* När du väljer en navigeringslänk för arbetsflödet i HTML Workspace visas inte att navigeringslänken är markerad. (NPR-37138)
* Funktionen Klottra signaturer är inte kompatibel med riktlinjerna för hjälpmedel. (NPR-37596)
* AEM Forms använder log4j 1.x. Stöd för log4j 1.x har nått slutet av livscykeln. (NPR-38273)
* När du använder MSSQL-databasen som en datakälla i en formulärdatamodell och hämtar värden, trunkeras siffror efter decimaltalet i de hämtade värdena. (CQ-4346190)
* När du öppnar ett formulär som har skapats med Forms 6.1 Designer i Forms 6.5 Designer och redigerar en textruta överskrider styckeavståndet det angivna utrymmet. Alla tidigare inställningar för utrymmet tas bort och du måste formatera om textrutan manuellt. (CQ-4341899)
* Felaktigt värde visas för streckkoden SSCC-18. Forms-servrar utelämnar värdet till höger om streckkoden. (CQ-4342400)
* För statisk PDF forms som skapats med Forms 6.5 Designer misslyckas tillgängligheten för PDF med fel `Tab order entry in page with annotations not set to "S"`. (CQ-4343117)
* Lagt till möjlighet att ange Reader-text på skärmen för hyperlänkar i Forms Designer.(NPR-36221)
* När du lägger till en upprepningsbar panel i en icke-XFA adaptiv form och antalet upprepningsbara paneler i ett icke-XFA-formulär är mer än 15, kan det ta upp till 7-8 sekunder att lägga till en ny instans. (NPR-37346)

## Integreringar {#integrations-6514}

* Aktivera stöd för JavaScript ES6-kompilering (ECMAScript6-läge eller bättre) för minimering av `/libs/cq/analytics/widgets.js` bibliotek. (NPR-38433)
* Aktivera stöd för JavaScript ES6-kompilering (ESMAScript6-läge eller bättre) för minimering av `/libs/cq/testandtarget/clientlibs/testandtarget/util.js` bibliotek. (NPR-38435)
* Mer innehåll finns i `/content/campaigns`, desto längre blir anropet till `targeteditor.html` (`/libs/cq/personalization/touch-ui/content/targeteditor.html`) tas när du öppnar sidredigeraren. (NPR-38663)

## Plattform {#platform-6514}

* Det går inte att logga in på Package Manager för att distribuera uppdateringar. (NPR-38646)
* I användargränssnittet för resurstaggväljaren visas taggarna i den ordning de skapades. Men om det finns många taggar är det svårt att visa och hantera taggarna eftersom de inte kan sorteras. (CQ-4344279)
* Skapa ett meddelande i användargränssnittet när en användare personifieras av en administratör eller någon annan som använder **[!UICONTROL Impersonate as]** fält. (CQ-4345288)
* I en smart samling visades alla resurser vid filtrering med hjälp av en sparad sökning. (CQ-4345326)
* Ett felaktigt antal valda resurser visas för **[!UICONTROL Add to collection]** när **[!UICONTROL Select All]** är markerat. (CQ-4345424)
* Ett undantagsmeddelande inträffade när **[!UICONTROL Impersonate as]** fält med en grupp eller en användare som inte finns. (CQ-4346098)

## [!DNL Sites] {#sites-6514}

* Oväntade borttagningar av sökvägar inträffade när Experience Manager uppgraderades från 6.5.12.0 till 6.5.13.0. (NPR-38532)

### Tillgänglighet {#access-6514}

* När du expanderar **[!UICONTROL Switch display format and adjust display setting]** knapp, markera **[!UICONTROL List View]**, **[!UICONTROL Drag and Drop]** ett hjälpmedelsnamn saknas för knappen. (SITES-2863, NPR-38760)
* Skärmläsaren måste ange ett hjälpmedelsnamn som `Show description for Archive` eller `Show description for mini shopping cart`. Det aktuella hjälpmedelsnamnet visas dock som `Info Circle button show description` for _alla_ knapparna för information om verktygstipset. (SITES-3104)
* Förbättra ångra för komponenter som inte har funktionen inlineEditing eller dropTarget i `cq:editConfig`. (NPR-38361) <!-- version 2 (old) of the description above * When out of the box components that don't have inlineEditing or dropTarget feature in the _cq_editConfig file (navigation, breadcrumb, embed) are deleted > undeleted (by way of Undo), all configurations are lost and empty placeholder reappears. Component must be reconfigured from scratch. (NPR-38361) -->
* Listrutan Formatsystem kan ha placerats högst upp på sidan i stället för i sitt sammanhang för komponenten - för komponenter som använder `cq:editConfig` &quot;afteredit: REFRESH_PAGE&quot;. (NPR-38384) <!-- version 2 (old) of description above* When selecting a style option on a component, the Styles box shifts to the upper left corner of the screen, rather than staying put below the style icon. Happens for components that have  cq:editConfig "afteredit: REFRESH_PAGE". (NPR-38384) -->
* Textkomponenten är feljusterad när den läggs till i kapslade layoutbehållare. (NPR-38193)
* En tom formatflik visades när det inte fanns någon formatsystemskonfiguration för en komponent. Fliken är nu dold när ingen konfiguration finns. (NPR-38218) <!-- version 2 (old) of description above * Style tab is blank on components without styles/policies. (NPR-38218) -->
* Egenskapen `useLegacyResponsiveBehaviour` fungerar bara när de autentiseras. (NPR-37996)

### [!DNL Content Fragments] {#sites-contentfragments-6514}

* Fältvalidering för uppräkning av innehållsfragment utfärdas första gången som innehållsfragmentet läses in. (SITES-7140)
* Kampanjanpassningsfält måste läggas till i RTF-redigeraren i innehållsfragmentsredigeraren. (NPR-38526)
* När du skapar eller redigerar ett nytt innehållsfragment i Content Fragment-redigeraren sparas inte innehållsfragmentmodellen med Dispatcher. Dessutom stängs inte Content Fragment-redigeraren och ett fel visas i webbläsarloggen. (NPR-38691)
* Valideringsfel för beständig fråga. (NPR-38523)
* I dialogrutan Innehållsfragment, under **[!UICONTROL Properties]**, **[!UICONTROL Content Fragment]** fältet behåller inte den sparade banan i markeringspopup-fönstret. (NPR-38632)
* När du skapar en modell för innehållsfragment och lägger till ett uppräkningsfält av den nedrullningsbara typen, är det den korrekta valideringen för _`is required`_misslyckas. (NPR-38237)

### Kärnkomponenter {#sites-corecomponents-6514}

* Den nya sidans e-postkomponent ska inte tvinga dig till det klassiska användargränssnittet när du redigerar `/etc`. (NPR-38648)

### Page Editor {#sites-pageeditor-6514}

* Användaren kan inte ändra storlek på komponenten till det önskade antalet kolumner. (NPR-38688)

### Mallredigerare {#sites-templateeditor-6514}

* Saknas **[!UICONTROL Delete]** och **[!UICONTROL Cut]** knappar på menyraden i en redigerbar mall efter `cq:actions` egenskapen har anpassats. (NPR-38521)
* Om en komponent innehåller en annan komponent går det inte att ta bort komponenten i mallstrukturen eftersom **[!UICONTROL Delete]** saknas i menyraden. (NPR-38585)

## Sling {#sling-6514}

* Ett ökat antal öppna filer i produktionen uppstod på grund av en minnesläcka i modulen `DiscoveryLiteDescriptor` in `org.apache.sling.discovery.commons`, version 1.0.20. (NPR-38288)
* I Experience Manager, från **[!UICONTROL Operations]** > **[!UICONTROL Diagnosis]** uppstår ett fel när du väljer **[!UICONTROL Download Status ZIP]** > **[!UICONTROL Download]**. (NPR-38514)

## Översättningsprojekt {#translation-6514}

* Start för undersidor som lagts till som en referens på en överordnad sida befordrades inte när `isDeep` egenskapen har angetts till `false`. (NPR-38531)

## Användargränssnitt {#ui-6514}

* När du använder **[!UICONTROL Select All]** > **[!UICONTROL Quick Publish]**, publicerade inte Experience Manager alla resurser och visade inte hur många resurser som skulle publiceras i **[!UICONTROL Card]** visa eller **[!UICONTROL List]** vy. (NPR-38546)
* Felaktigt antal valda resurser visas för **[!UICONTROL Add to collection]** in **[!UICONTROL Select All]** case. (NPR-38633)
* Inaktiverade användare kan fortfarande läggas till i Samlingar och Projekt. (NPR-38651)
* Om du tar bort ett filter utan att spara sökformuläret skapas ett fel. (NPR-38698)
* En användarsession kan inte hämta en `ModifiableValueMap` instans för grupperna för att upprätta det direkta gruppmedlemskapet. (NPR-38710)

## Arbetsflöde {#workflow-6514}

* Aktivera stöd för JavaScript ES6-kompilering (ESMAScript6-läge eller bättre) för minimering av `/libs/cq/inbox/gui/components/inbox/clientlibs/commons.js` bibliotek. (NPR-38304)
* När arbetsflödet har körts och processtegen är slutförda upprepas samma kommentar flera gånger. (NPR-38364)

## Installera [!DNL Experience Manager] 6.5.14.0 {#install}

<!-- Remaining content from here to bottom stays the same except for version updating as needed as per update team feedback. -->

* [!DNL Experience Manager] 6.5.14.0 kräver [!DNL Experience Manager] 6.5. Se [uppgraderingsdokumentation](/help/sites-deploying/upgrade.md) för detaljerade anvisningar. <!-- UPDATE FOR EACH NEW RELEASE -->
* Service Pack-nedladdning finns på Adobe [Programvarudistribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html).
* På en distribution med MongoDB och flera instanser installerar du [!DNL Experience Manager] 6.5.14.0 på en av författarinstanserna med hjälp av Package Manager.<!-- UPDATE FOR EACH NEW RELEASE -->

>[!NOTE]
>
>Adobe rekommenderar inte att du tar bort eller avinstallerar [!DNL Experience Manager] 6.5.14.0-paket. <!-- UPDATE FOR EACH NEW RELEASE -->

### Installera Service Pack på [!DNL Experience Manager] 6.5 {#install-service-pack}

1. Starta om instansen innan installationen om instansen är i uppdateringsläge (när instansen uppdaterades från en tidigare version). Adobe rekommenderar att du startar om om den aktuella upptiden för en instans är hög.

1. Ta en ögonblicksbild eller en ny säkerhetskopia av din [!DNL Experience Manager] -instans.

1. Hämta Service Pack från [Programvarudistribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.14.0.zip). <!-- UPDATE FOR EACH NEW RELEASE -->

1. Öppna Pakethanteraren och välj **[!UICONTROL Upload Package]** för att överföra paketet. Mer information finns på [Pakethanteraren](/help/sites-administering/package-manager.md).

1. Markera paketet och välj **[!UICONTROL Install]**.

1. Om du vill uppdatera S3-anslutningen stoppar du instansen efter installationen av Service Pack, byter ut den befintliga kopplingen mot en ny binär fil som finns i installationsmappen och startar om instansen. Se [Amazon S3 - datalager](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector).

>[!NOTE]
>
>Dialogrutan för pakethanterarens gränssnitt avslutas ibland när Service Pack installeras. Adobe rekommenderar att du väntar på att felloggarna ska stabiliseras innan du får åtkomst till distributionen. Vänta på de specifika loggarna för avinstallationen av uppdateringspaketet innan du försäkrar dig om att installationen lyckas. Vanligtvis inträffar detta problem i [!DNL Safari] webbläsare, men kan ibland inträffa i vilken webbläsare som helst.

**Automatisk installation**

Det finns två olika metoder som du kan använda för att installera automatiskt [!DNL Experience Manager] 6.5.14.0<!-- UPDATE FOR EACH NEW RELEASE -->

* Placera paketet i `../crx-quickstart/install` när servern är tillgänglig online. Paketet installeras automatiskt.
* Använd [HTTP-API från Package Manager](/help/sites-administering/package-manager.md#package-share). Använd `cmd=install&recursive=true` så att de kapslade paketen installeras.

>[!NOTE]
>
>Experience Manager 6.5.14.0 stöder inte installation av Bootstrap. <!-- UPDATE FOR EACH NEW RELEASE -->

**Validera installationen**

Om du vill veta vilka plattformar som är certifierade för att fungera med den här versionen kan du läsa [tekniska krav](/help/sites-deploying/technical-requirements.md).

1. Produktinformationssidan (`/system/console/productinfo`) visar den uppdaterade versionssträngen `Adobe Experience Manager (6.5.14.0)` under [!UICONTROL Installed Products]. <!-- UPDATE FOR EACH NEW RELEASE -->

1. Alla OSGi-paket är antingen **[!UICONTROL ACTIVE]** eller **[!UICONTROL FRAGMENT]** i OSGi Console (Use Web Console: `/system/console/bundles`).

1. OSGi-paketet `org.apache.jackrabbit.oak-core` är version 1.2.2.12 eller senare (Använd webbkonsol: `/system/console/bundles`). <!-- NPR-38747 -->

### Installera [!DNL Experience Manager] Forms tilläggspaket {#install-aem-forms-add-on-package}

>[!NOTE]
>
>Hoppa över om du inte använder [!DNL Experience Manager] Forms.

<!-- 

Fixes in [!DNL Experience Manager] Forms are delivered through a separate add-on package a week after the scheduled [!DNL Experience Manager] Service Pack release.

-->

1. Kontrollera att du har installerat [!DNL Experience Manager] Service Pack.
1. Ladda ned motsvarande tilläggspaket från Forms på [AEM Forms](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html#forms-updates) för ditt operativsystem.
1. Installera Forms tilläggspaket enligt beskrivningen i [Installera AEM Forms tilläggspaket](/help/forms/using/installing-configuring-aem-forms-osgi.md#install-aem-forms-add-on-package).
1. Om du använder bokstäver i Experience Manager 6.5 Forms installerar du [senaste AEMFD-kompatibilitetspaket](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html#forms-updates).

### Installera [!DNL Experience Manager] Forms på JEE {#install-aem-forms-jee-installer}

>[!NOTE]
>
>Hoppa över om du inte använder AEM Forms på JEE. Korrigeringar i [!DNL Experience Manager] Forms på JEE levereras via ett separat installationsprogram.

Mer information om hur du installerar det kumulativa installationsprogrammet för [!DNL Experience Manager] Forms on JEE och konfiguration efter driftsättning finns i [versionsinformation](jee-patch-installer-65.md).

>[!NOTE]
>
>Efter installation av det kumulativa installationsprogrammet för [!DNL Experience Manager] Forms på JEE, installera det senaste Forms-tilläggspaketet, ta bort Forms-tilläggspaketet från `crx-repository\install` och starta om servern.

### UberJar {#uber-jar}

UberJar för [!DNL Experience Manager] 6.5.13.0 finns i [Maven Central-arkivet](https://repo.maven.apache.org/maven2/com/adobe/aem/uber-jar/6.5.13/). <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

>[!NOTE]
>
>I Experience Manager 6.5.14.0 bör du vara medveten om att UberJar-versionen (6.5.13.0) fortfarande är densamma som den tidigare versionen.

Information om hur du använder UberJar i ett Maven-projekt finns i [använda UberJar](/help/sites-developing/ht-projects-maven.md) och inkludera följande beroende i projektens POM: <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

```shell
<dependency>
     <groupId>com.adobe.aem</groupId>
     <artifactId>uber-jar</artifactId>
     <version>6.5.13</version>
     <scope>provided</scope>
</dependency>
```

>[!NOTE]
>
>UberJar och andra tillhörande artefakter finns tillgängliga i Maven Central Repository i stället för i Adobe Public Maven-arkivet (`repo.adobe.com`). Huvudfilen för UberJar har bytt namn till `uber-jar-<version>.jar`. Så det finns ingen `classifier`, med `apis` som värdet, för `dependency` -tagg.

## Föråldrade funktioner {#removed-deprecated-features}

Nedan finns en lista över funktioner som är markerade som borttagna [!DNL Experience Manager] 6.5.7.0 Funktioner markeras som borttagna från början och senare i en framtida version. Ett alternativt alternativ anges.

Granska om du använder en funktion eller en funktion i en distribution. Planera också att ändra implementeringen så att ett alternativt alternativ används.

| Yta | Funktion | Ersättning |
|---|---|---|
| Integreringar | The **[!UICONTROL AEM Cloud Services Opt-In]** skärmen är föråldrad sedan [!DNL Experience Manager] och [!DNL Adobe Target] integreringen uppdateras i [!DNL Experience Manager] 6.5. Integreringen stöder Adobe Target Standard API. API:t använder autentisering via Adobe IMS och [!DNL Adobe I/O Runtime]. Det stöder den växande rollen för Adobe Launch till instrument [!DNL Experience Manager] för analys och personalisering är anmälningsguiden funktionellt irrelevant. | Konfigurera systemanslutningar, Adobe IMS-autentisering och [!DNL Adobe I/O Runtime] integreringar via respektive [!DNL Experience Manager] molntjänster. |
| Anslutningar | Adobe JCR Connector för Microsoft® SharePoint 2010 och Microsoft® SharePoint 2013 är föråldrad för [!DNL Experience Manager] 6.5. | Ej tillämpligt |

## Kända fel {#known-issues}

<!-- THESE KNOWN ISSUES CARRY OVER EACH RELEASE. THE "PRODUCT UPDATES TEAM" IS SUPPOSED TO VERIFY EACH ISSUE AND LET YOU KNOW IF ANYTHING NEEDS TO BE ADDED, DELETED, OR CHANGED IN THE LIST.
 -->

* [AEM innehållsfragment med GraphQL-indexpaket 1.0.5](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Ffeaturepack%2Fcfm-graphql-index-def-1.0.5.zip)
Det här paketet behövs för kunder som använder GraphQL. på så sätt kan de lägga till den indexdefinition som behövs baserat på de funktioner de faktiskt använder.

* Som [!DNL Microsoft® Windows Server 2019] stöder inte [!DNL MySQL 5.7] och [!DNL JBoss® EAP 7.1], [!DNL Microsoft® Windows Server 2019] stöder inte körklara installationer för [!DNL AEM Forms 6.5.10.0].

* Om du uppgraderar dina [!DNL Experience Manager] från version 6.5 till 6.5.10.0 kan du visa `RRD4JReporter` undantag i `error.log` -fil. Starta om instansen för att lösa problemet.

* Om du installerar [!DNL Experience Manager] 6.5 Service Pack 10 eller ett tidigare Service Pack på [!DNL Experience Manager] 6.5, runtime copy of your assets custom workflow model (created in `/var/workflow/models/dam`) tas bort.
Om du vill hämta körtidskopian rekommenderar Adobe att du synkroniserar designtidskopian av den anpassade arbetsflödesmodellen med körtidskopian med hjälp av HTTP API:
   `<designModelPath>/jcr:content.generate.json`.

* Användare kan byta namn på en mapp i en hierarki i [!DNL Assets] och publicera en kapslad mapp i [!DNL Brand Portal]. Mappens namn uppdateras dock inte i [!DNL Brand Portal] tills rotmappen publiceras på nytt.

* När en användare väljer att konfigurera ett fält för första gången i ett adaptivt formulär visas inte alternativet att spara en konfiguration i egenskapsläsaren. Om du väljer att konfigurera ett annat fält i det adaptiva formuläret i samma redigerare åtgärdas problemet.

* Följande fel och varningsmeddelanden kan visas under installationen av [!DNL Experience Manager] 6.5.x.x:
   * &quot;När Adobe Target-integreringen är konfigurerad i [!DNL Experience Manager] med Target Standard API (IMS-autentisering) och sedan exportera Experience Fragments till Target så att fel erbjudandetyper skapas. I stället för att skriva&quot;Experience Fragment&quot;/källa&quot;Adobe Experience Manager&quot; skapar Target flera erbjudanden med typen&quot;HTML&quot;/källa&quot;Adobe Target Classic&quot;.
   * `com.adobe.granite.maintenance.impl.TaskScheduler`: Inga underhållsfönster hittades vid granit/drift/underhåll.
   * Validering på serversidan av adaptiva formulär misslyckas när sammanställningsfunktioner som SUM, MAX och MIN används (CQ-4274424).
   * `com.adobe.granite.maintenance.impl.TaskScheduler` - Inga underhållsfönster hittades vid granit/drift/underhåll.
   * Aktiveringspunkten i en interaktiv Dynamic Media-bild syns inte när du förhandsvisar mediefilen via Shoppable Banner Viewer.
   * `com.adobe.cq.social.cq-social-jcr-provider bundle com.adobe.cq.social.cq-social-jcr-provider:1.3.5 (395)[com.adobe.cq.social.provider.jcr.impl.SpiSocialJcrResourceProviderImpl(2302)]` : Tidsgränsen överskreds i väntan på att registerändringen skulle slutföras utan registrering.

* När du försöker flytta/ta bort/publicera antingen innehållsfragment eller webbplatser/sidor uppstår ett problem när referenser till innehållsfragment hämtas, eftersom bakgrundsfrågan misslyckas. d.v.s. funktionen fungerar inte.
Du måste lägga till följande egenskaper i indexdefinitionsnoden för att få en korrekt åtgärd `/oak:index/damAssetLucene` (ingen omindexering krävs):

   ```xml
   "tags": [
       "visualSimilaritySearch"
     ]
   "refresh": true
   ```

## OSGi-paket och innehållspaket som ingår {#osgi-bundles-and-content-packages-included}

Följande textdokument listar de OSGi-paket och innehållspaket som ingår i [!DNL Experience Manager] 6.5.14.0: <!-- UPDATE FOR EACH NEW RELEASE -->

* [Förteckning över OSGi-paket som ingår i Experience Manager 6.5.14.0](/help/release-notes/assets/65140_bundles.txt) <!-- UPDATE FOR EACH NEW RELEASE -->
* [Förteckning över innehållspaket som ingår i Experience Manager 6.5.14.0](/help/release-notes/assets/65140_packages.txt) <!-- UPDATE FOR EACH NEW RELEASE -->

## Begränsade webbplatser {#restricted-sites}

Dessa webbplatser är bara tillgängliga för kunder. Om du är kund och behöver åtkomst kontaktar du din kontoansvarige på Adobe.

* [Nedladdning av produkt på licensing.adobe.com](https://licensing.adobe.com/)
* [Kontakta Adobe kundsupport](https://experienceleague.adobe.com/docs/customer-one/using/home.html).

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] produktsida](https://business.adobe.com/products/experience-manager/adobe-experience-manager.html)
>* [[!DNL Experience Manager] 6.5-dokumentation](https://experienceleague.adobe.com/docs/experience-manager-65.html)
>* [Prenumerera på produktuppdateringar med Adobe prioritet](https://www.adobe.com/subscription/priority-product-update.html)

