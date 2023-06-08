---
title: Versionsinformation för [!DNL Adobe Experience Manager] 6.5
description: Hitta versionsinformation, nyheter, installationsanvisningar och en detaljerad ändringslista för [!DNL Adobe Experience Manager] 6.5.
mini-toc-levels: 3
exl-id: fed4e110-9415-4740-aba1-75da522039a9
source-git-commit: 36edc2507d9acd7d5f94e433a654ccc1647bb58a
workflow-type: tm+mt
source-wordcount: '3556'
ht-degree: 0%

---

# [!DNL Adobe Experience Manager] 6.5 Versionsinformation om senaste Service Pack {#aem-service-pack-release-notes}

<!-- For an itemized list of all issues found in these release notes, see the following spreadsheet: https://adobe-my.sharepoint.com/:x:/r/personal/anujkapo_adobe_com/Documents/issue_tracker_sp_cfp_updates.xlsx?d=w3ea81ae4e6054153b132f2698c86f84e&csf=1&web=1&e=7yhrWb&nav=MTVfe0U0RjdDQUM3LTZCQ0EtNDk1Qy04Mjc1LTM2MUJEMzE1OEVGN30 -->

<!-- DO NOT DELETE THIS HIDDEN NOTE      DO NOT DELETE THIS HIDDEN NOTE
>[!NOTE]
>
>Fixes in [!DNL Experience Manager] Forms are delivered through a separate add-on package one week after the scheduled [!DNL Experience Manager] Service Pack release date. In this case, the add-on packages release Thursday, June 1, 2023. In addition, a list of Forms fixes and enhancements is added to this section. -->

## Versionsinformation {#release-information}

| Produkt | [!DNL Adobe Experience Manager] 6.5 |
| -------- | ---------------------------- |
| Version | 6.5.17.0 <!-- UPDATE FOR EACH NEW RELEASE --> |
| Typ | Service Pack-version |
| Datum | Torsdagen den 25 maj 2023 <!-- UPDATE FOR EACH NEW RELEASE --> |
| Hämta URL | [Programvarudistribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.17.0.zip) <!-- UPDATE FOR EACH NEW RELEASE --> |

## Vad ingår i [!DNL Experience Manager] 6.5.17.0 {#what-is-included-in-aem-6517}

[!DNL Experience Manager] 6.5.17.0 innehåller nya funktioner, viktiga förbättringar som kunderna efterfrågat, felkorrigeringar, prestanda, stabilitet och säkerhetsförbättringar som har släppts sedan den första tillgängligheten av 6.5 i april 2019. [Installera detta Service Pack](#install) på [!DNL Experience Manager] 6.5.

<!-- UPDATE FOR EACH NEW RELEASE -->

<!-- Some of the key features and improvements are the following:

* _REVIEWERS: WHAT ARE THE KEY FEATURES AND ENHANCEMENTS YOU WANT TO HIGHLIGHT IN THIS RELEASE?_ -->

Några av de viktigaste funktionerna och förbättringarna i den här versionen är följande:

* **Förbättrade sökupplevelser** - Du kan nu snabbt utföra följande åtgärder på resurserna som visas i sökresultaten:
   * Skapa ett arbetsflöde
   * Skapa en version
   * Relatera eller inte relatera tillgångar

   Du behöver inte navigera till resursplatsen och visa dess egenskaper för att utföra dessa åtgärder.
* **Dynamic Media _Ögonblicksbild_**- Experimentera med testbilder eller Dynamic Media-URL:er för att se utdata från olika bildmodifierare och optimering av Smart Imaging för filstorlek (med WebP- och AVIF-leverans), nätverksbandbredd och Device Pixel Ratio. Se [Dynamic Media Snapshot](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/images/dynamic-media-snapshot.html).
* **DASH-strömning med Dynamic Media** - Stöd för nya protokoll (DASH - Dynamic Adaptive Streaming over HTTP) har startats för Adaptive streaming i Dynamic Media (med CMAF aktiverat). Finns nu för alla regioner, [aktiveras via en supportanmälan](/help/assets/video.md#enable-dash-on-your-account-enable-dash).
* **Integrering av Experience Manager Sites- och Content Fragments med Assets Next-Generation Dynamic Media** - Användare av Experience Manager Assets as a Cloud Service Next-Generation Dynamic Media kan nu använda dessa molnbaserade resurser för att skapa och leverera med lokala eller Managed Services-instanser av Experience Manager Sites 6.5.
* **Integration av Adaptive Forms på Experience Manager Sites-sidor**: Skapa smidigt digitala registreringsupplevelser genom att använda adaptiva Forms-komponenter i Experience Manager Sites Editor med: - Adaptiv Forms-behållare och adaptiv Forms - Bädda in (v2) komponenter.
* **Stöd för reCAPTCHA Enterprise i Experience Manager Forms**: Stöd för reCAPTCHA Enterprise i Experience Manager Forms har lagts till, vilket ger bättre skydd mot bedräglig aktivitet och skräppost utöver det befintliga stödet för Google reCAPTCHA v2.
* **Stöd för Adobe Acrobat Sign for Government med Experience Manager Forms**: Gör det möjligt att integrera Experience Manager Forms säkert och kompatibelt med Adobe Sign för myndigheter (FedRAMP-kompatibelt).
* **Aktivera Salesforce-integrering med Experience Manager Forms för datautbyte**: Konfigurera integreringen mellan Experience Manager Forms och Salesforce med hjälp av inloggningsflödet för OAuth 2.0-klienten. Denna funktion möjliggör säker och direkt autentisering och behörighet av programmet och möjliggör smidig kommunikation utan användarinblandning.
* **Optimering och förbättrad funktionalitet i arbetsflödesmotorn**: Öka arbetsflödesmotorernas prestanda genom att minimera antalet arbetsflödesinstanser. Förutom `COMPLETED` och `RUNNING` statusvärden, arbetsflödet stöder även tre nya statusvärden: `ABORTED`, `SUSPENDED`och `FAILED`.


<!-- UPDATE BELOW FOR EACH NEW RELEASE -->

## [!DNL Assets]{#assets-6517}

* När du publicerar mer än 40 PDF samtidigt [!DNL Experience Manager] slutar svara och blir otillgänglig en tid. (ASSETS-21789)
* Om du är inloggad som testanvändare kan du inte se resurser som hör till en viss resurs när du klickar på egenskaper för en resurs. (ASSETS-21648)
* När resurser redigeras med `Desktop Actions`om du försöker checka in fler än fem resurser samtidigt, `Limit Reached` visas och de markerade resurserna checkas ut. (ASSETS-21121)
* Det går inte att sortera resurser efter namn i en samling. (ASSETS-20924)
* Det går inte att ange dimensioner för resurser av en bildformattyp. (ASSETS-20835)
* Verktygstipstexten och dess bakgrund i fältet Sök/lägg till e-postadress visar inte rätt kontrastförhållande när en länk delas. (ASSETS-17347)
* När du expanderar `Notifications`visas texten inte korrekt på grund av styckemellanrum. (ASSETS-17345)
* När du kopierar en resurs i samlingen `Public Collection` kryssrutan inte visas korrekt. (ASSETS-17343)
* Elements använder ARIA-attribut utan roll. (ASSETS-17325,ASSETS-17323)
* Länken är inte beskrivande när du expanderar `Notifications`. (ASSETS-17283)
* När du navigerar och expanderar [!DNL Smart Crop] visas innehållet som en lista men inte som en osorterad lista. Därför känner skärmläsaren inte igen den osorterade listan och läser den som oformaterad text. (ASSETS-17247)
* The `Sort By` Etiketten är inte associerad med respektive listruta. Därför känner skärmläsaren inte igen de nedrullningsbara alternativen. (ASSETS-17239)
* Det går inte att flytta framåt eller bakåt med tangentbordsfliken eller piltangenterna när du försöker lägga till en användare med `Add user` kombinationsruta. (ASSETS-17233)
* Skärmläsaren förmedlar inte informationen för arbetsflödessteget korrekt (ASSETS-17285).
* När du navigerar till `Saved Searches` kombinationsruta, både namn och roll har inga tilldelade etiketter. (ASSETS-17329)
* När du navigerar `Collection` och hovra till texten *Medlemmar* visas texten inte som markerad. Skärmläsaren känner därför inte igen rubriktexten och läser den som oformaterad text. (ASSETS-17245)
* Det går inte att komma åt `View Settings` med hjälp av rullningslist och uppåtpil från tangentbordet. (ASSETS-17257)
* Det går inte att utlösa ett arbetsflöde för flera valda resurser som hittas med sökfilter. (ASSETS-7689)
* När du väljer en resurs (eller flera resurser) bland sökresultaten visas inte alternativet Relatera eller Ej relaterat. Men alternativet är tillgängligt, annars. (ASSETS-7679)
* Sökfilterpanelen öppnas bara en gång efter inloggningen och öppnas inte om du avslutar söksidan och kör sökningen igen. (ASSETS-7671)
* Kombinationsrutan för e-post visar inte rätt kontrastförhållande när en länk delas. (ASSETS-17349)

<!-- REMOVED BY ENGINEERING FROM TOTAL RELEASE CANDIDATE LIST 
* When you select any file in a Collection and click `Download`, and then navigate to the email checkbox and expand it, regular text and email link is not recognizable due to background color. (ASSETS-17349) 
* When you navigate to `Smart Crop` option, the screen reader does not announce the expand or collapse state of the button. (ASSETS-17335)-->

## [!DNL Assets] - [!DNL Dynamic Media]{#dm-6517}

* Anslutningen till Dynamic Media bryts när det redan finns en Dynamic Media Cloud-konfiguration. (ASSETS-23057)
* Förbättrade prestanda när du bläddrar bland mappar med många Dynamic Media-videor och lösta problem kan inte läsas in i mappkortsvyn. (ASSETS-23016)
* Förhandsgranskningstoken tas bort från `error.log` som kan användas för att begära säkert innehåll från säkra testservrar. (ASSETS-22685)
* Miniatyrbildsrendering i PDF lägger till en skugga. Uppgraderade Gibson lib version 4.0.1680232194 för att lösa problemet med återgivning av miniatyrbilder i PDF. (ASSETS-22585)
* Dynamic Media hybridläge är nu kompatibelt med New Relic Agent version 8.0.1 (ASSETS-22578).
* Åtkomstkontrollistor i Experience Manager respekteras nu när Dynamic Media-filer förhandsgranskas på Experience Manager. (ASSETS-21628)
* Skärmläsare navigerar inte till dolda element när användaren försöker navigera med hjälp av nedpilen eller tabbtangenten. (ASSETS-5617)
* Användargränssnittet Bildprofil är begränsat för smarta beskärningar med samma namn, dimension eller både och. (ASSETS-16997)
* Standardbredden och -höjden har nu angetts till 50 pixlar för Smart beskärning i användargränssnittet för bildprofil. (ASSETS-16997)

## [!DNL Commerce]{#commerce-6517}

* Flyttade taggar är skräpinsamlade men refereras fortfarande till av produkter under `/var`. (CQ-4351337)

## [!DNL Forms]{#forms-6517}

* När du har uppdaterat till AEM 6.5.15.0 Service Pack, fungerar inte HTML5-formulären eller läses in korrekt i Edge-webbläsaren med kompatibilitetsläget IE. (FORMS-8526, FORMS-8523)
* När en användare använder AEM Service Pack 6.5.16.0 kan regelredigeraren inte öppnas. (FORMS-8290)
* När det maximala antalet siffror för valideringen tillämpas på en Numeric Box-komponent misslyckas den. (FORMS-7938)
* När du skapar interaktiva kommunikationssatser genereras inte diagramkomponenten i PDF korrekt. (FORMS-7827, FORMS-8297)
* Java™-skräpinsamlingen kan inte rensa gammal generheap på en Experience Manager Forms OSGi-server. (FORMS-8207)
* När en användare uppgraderar till Service Pack för Experience Manager 6.5.16.0 saknas CRX-metadataegenskaperna efter överföringen. (FORMS-8205)
* När en användare inaktiverar datumväljarkomponenten i ett adaptivt formulär går det fortfarande att redigera den. (FORMS-7804)
* I Forms Service Pack för Experience Manager 6.5.16.0 är Document Publisher alltid avmarkerat när en användare försöker redigera koordinatorerna för principuppsättningen. (FORMS-7775, FORMS-8599)
* När en användare uppgraderar till Experience Manager 6.5.16.0 Service Pack slutar metoden &quot;GuideNode.externalize&quot; som hanterar strängar som måste översättas att fungera. (FORMS-7709)
* I `Assign task` när en användare väljer&quot;Skicka e-post för meddelande&quot; och anropar arbetsflödet visas texten inte korrekt i det mottagna e-postmeddelandet. Frågetecknen tas emot i stället för texten i det mottagna e-postmeddelandet. (FORMS-7675)
* Dokumentet översätts delvis. (FORMS-7674, FORMS-7573)
* En användare kan inte redigera principuppsättningar, även om de tilldelats specifika behörigheter. (FORMS-7665)
* När en användare i `forms-users` gruppen försöker skapa ett formulär, Experience Manager Forms-instansen kraschar. (FORMS-7629)
* När användaren klickar på knapparna Återställ, Spara eller Skicka i ett anpassat formulär visas inget meddelande på skärmen. (FORMS-7524)
* För att förbättra prestanda vid PDFG-konvertering på ett Service Pack för Experience Manager 6.5.16.0 görs vilolägesintervallet konfigurerbart. (FORMS-6752)
* Växlingsalternativet är detsamma, men fältets synlighet ändras även när användaren drar markören något. (FORMS-6728)
* När användaren uppgraderar till Experience Manager 6.5.15.0 Service Pack slutar omdirigeringen att fungera när en anpassad form renderas i Internet Explorer. (FORMS-6725)
* PAC 2021-verktyget för alla bakgrundsobjekt i ett PDF-formulär som skapats av en Experience Manager Designer returnerar ett fel som `Path object not tagged`. (FORMS-6707)
* När en användare använder ett filter i inkorgen skapas en `NullPointerException` fel. (FORMS-6706)
* När en användare importerar en mallfil (.tds) med refererade fragment kraschar Experience Manager Designer. (FORMS-6702)
* Om användaren skapar ett statiskt PDF med hjälp av utdatatjänsten i Experience Manager Forms Designer 6.5 inträffar ett fel `OCCD (optional content configuration dictionary) contains AS key`. (FORMS-6691)
* När användaren skapar ett enkelt arbetsflöde och lägger till en enkel variabel, `set variable mapping` fel inträffar. (FORMS-5819)
* När en användare försöker generera ett PDF med hjälp av utdatatjänsten, trots att den är markerad som `PDF/A-1a`, en kompatibilitetskontroll med`Preflight` tjänsten misslyckas. (LC-3920837)
* När du har installerat Service Pack för Experience Manager 6.5.16.0 går det inte att öppna Experience Manager Designer. (LC-3921000)
* När en användare lägger till en kryssruta och alternativknapp genereras inte strukturen för ett taggträd enligt PDF-standard. (LC-3920838)
* Om en användare genererar ett statiskt PDF genom att använda inbäddning och deluppsättning av teckensnitt via utdatatjänsten, innehåller det resulterande PDF bara de inbäddade teckensnitten. (LC-3920963)
* Den hebreiska texten visas felaktigt i RTL-format. (LC-3919632)
* När en användare uppgraderar till Experience Manager 6.5.16.0 Service Pack på en JBoss®-turnkey-server kan signaturtjänsten inte anropas. Det påträffade felet är: `java.lang.ClassCastException: com.adobe.xfa.TextNode cannot be cast to com.adobe.xfa.Element`. (FORMS-7833)
* Efter uppgradering till Service Pack för Experience Manager 6.5.14.0 fungerar inte arbetsbyteprocesserna för att flytta en CRX-nod från en plats till en annan. Felet inträffar som `ALC-CRX-30000-000: com.adobe.ep.crx.client.exceptions.CRCException: ALC-CRX-030-000-[Internal Server Error]`. (FORMS-7713)
* När en användare uppdaterar till Service Pack för Experience Manager 6.5.16.0 `Usage Rights` inte kan tillämpas. (FORMS-7892)
* När en användare försöker generera ett PDF-dokument misslyckas valideringen av PDF/A-1b. (FORMS-7615)
* När en användare klickar på `Configure` för `Form Container` blir webbläsaren inte responsiv. (FORMS-7605)
* När en användare uppdaterar till Experience Manager Forms 6.5.16.0 Service Pack och försöker ändra `LicenseType` till `Production`, återspeglas inte ändringarna. (FORMS-7594)
* När en användare försöker anropa en LCA-process med ett PDF som innehåller `Chinese Full Width Characters`uppstår ett problem med `ValidateForm` -processen. (FORMS-7464)
* I Experience Manager Forms Designer genererar XMLFM ZPL-utdata med olika pappersstorlekar, som A4 och A5, för XDP-baserade mallar. (FORMS-7898)

## Integreringar{#integrations-6517}

* När du konverterar en Adobe Target IMS-konfiguration till en användarautentiseringsuppgift i äldre molnkonfigurationer visas `connectedWhen` egenskapen ändras inte. Detta gör att alla anrop går som om konfigurationen fortfarande var IMS-baserad. (CQ-4352810)
* Lägger till `modifyProperties` behörighet att `fd-cloudservice` systemanvändare för Adobe Sign-konfiguration. (FORMS-6164)
* När du skapar en AB-testaktivitet, som är integrerad med Adobe Target, synkroniseras inte de målgrupper som är kopplade till den med Target. (NPR-40085)

## Oak{#oak-6517}

Från Service Pack 13 och senare har följande fellogg börjat visas som påverkar persistencecachen:

```shell
org.h2.mvstore.MVStoreException: The write format 1 is smaller than the supported format 2 [2.0.202/5]
at org.h2.mvstore.DataUtils.newMVStoreException(DataUtils.java:1004)
    at org.h2.mvstore.MVStore.getUnsupportedWriteFormatException(MVStore.java:1059)
    at org.h2.mvstore.MVStore.readStoreHeader(MVStore.java:878)
    at org.h2.mvstore.MVStore.<init>(MVStore.java:455)
    at org.h2.mvstore.MVStore$Builder.open(MVStore.java:4052)
    at org.h2.mvstore.db.Store.<init>(Store.java:129)
```

eller

```shell
org.h2.mvstore.MVStoreException: The write format 1 is smaller than the supported format 2 [2.1.214/5].
```

Så här löser du det här undantaget:

1. Ta bort följande två mappar från `crx-quickstart/repository/`

   * `cache`
   * `diff-cache`

1. Installera Service Pack eller starta om Experience Manager as a Cloud Service.
Nya mappar med `cache` och `diff-cache` skapas automatiskt och du får inte längre något undantag relaterat till `mvstore` i `error.log`.

## Plattform{#platform-6517}

* I användargränssnittet för Experience Manager Tag Management (/aem/tags/) visas namnutrymmen och taggar i den ordning de skapas. Men om det finns många namnutrymmen och taggar är det svårt att visa och hantera dem. Problemet beror på att de inte kan sorteras på något annat sätt. (NPR-39620)
* Google-versionen behöver uppdateras eftersom Minification JS inte fungerar för vissa klientbibliotek. (NPR-40043)

## [!DNL Sites]{#sites-6517}

* Prestandaminskning i LinkCheckerTransformer. (SITES-11661)
* Språkkopior av en sida uppdaterades inte som förväntat. (SITES-11191)
* Öppnar samtal för icke-kampanjsidor `targeteditor.html` i onödan. Ta bort `targeteditor` ring när det inte behövs. (SITES-12469)
* Live-kopior kan inte skapas för sidor med anteckningar. (SITES-12154)
* Sidutrullning fungerar inte på Experience Manager 6.5.16. (SITES-12008)
* Slut på minne. hög skräpinsamling på grund av `NotificationManagerImpl`. `NotificationManager` uppgradera till Experience Manager 6.5. (SITES-11440)
* Korrigerade IT-tester för WCM som blockerade Service Pack 17. (SITES-13089)
* Det går inte att hämta platsreferenser på en server. (SITES-10901)

### [!DNL Sites] - Administratörsgränssnitt{#sites-adminui-6517}

* Det går inte att stänga förhandsgranskningsfönstret för miniatyrbildsväljaren. (SITES-10459)

### [!DNL Sites] - [!DNL Content Fragments]{#sites-contentfragments-6517}

* Konfiguration för anslutning till Polaris-tjänstobjekt (URL, autentiseringsuppgifter, återanrop och så vidare). (SITES-12149)
* Användning av `SemanticDataType.REFERENCE` ska ha stöd för &quot;Remote-Asset-ID&quot;. (SITES-12127)
* Integrera Polaris resursväljare i Content Fragment editor. (SITES-12125)
* Ett obligatoriskt http-huvud krävs för att komma åt metadatatjänstens slutpunkt. (SITES-13068)
* GraphQL implementering av 6.5 var inte i linje med Cloud Service (primär). identifierade problem har åtgärdats. (SITES-13096)
* GraphQL paging/sorting och hybridfiltrering bör finnas på Experience Manager 6.5/AMS. (SITES-9154)

### [!DNL Sites] - Kärnkomponenter{#sites-core-components-6517}

* Egenskapen `cq-msm-lockable` har fel omdirigeringsvärde i komponenten Foundation page. (SITES-10904)
* Väljaren för fjärrresurser dirigeras alltid om till IMS-scenmiljön. (SITES-13433)

### [!DNL Sites] - [!DNL Experience Fragments]{#sites-experiencefragments-6517}

* Om du väljer en Externalizer-konfiguration i ett Experience Fragment när du exporterar till Adobe Target skickas den felaktiga externa URL:en. (SITES-12402)
* Ta bort villkor som inte är inkluderande; tillämpa riktlinjer för inkluderande villkor. (SITES-11244)

### [!DNL Sites] - sidredigeraren{#sites-pageeditor-6517}

* Ingen miniatyrbild visas för en karuselluppsättning i Experience Manager innehållssökarens sidospår. (SITES-8593)

## Sling{#sling-6517}

* Sling `ResourceMerger` förbrukar en stor mängd CPU när den tillhandahålls med en fiktiv sökväg, vilket leder till denial of service. (NPR-40338)

## Översättningsprojekt{#translation-6517}

<!-- REMOVED BY ENGINEERING FROM TOTAL RELEASE CANDIDATE LIST * The `translationrules.xml` is sorted poorly when adding a rule to a property by way of the translation configuration user interface. (NPR-40431) -->
* Språkkopia skapas inte när användaren inte konfigurerar icke-obligatoriska fält. (NPR-40036)

## Användargränssnitt{#ui-6517}

* Knappen Avbryt i sidegenskaperna är inaktiv; det ska ta dig till användargränssnittet för platsadministratören. (NPR-40501)

<!-- ## WCM{#wcm-6517}

* TEXT -->

## Arbetsflöde{#workflow-6517}

* Ändringar i arbetsflödeskonsolen. (NPR-40502)
* `SegmentNotfound errors` i loggarna på en produktionsförfattarinstans, orsakad av en oavslutad resurshanterare i klassen `com.day.cq.workflow.impl.email.EMailNotificationServic`. (NPR-40187)
* En stängd oavslutad `ResourceResolver` undantagsfel loggas. (ASSETS-22495)
* Experience Manager-författaren kraschar när PSD/PDF har stora `DocumentAncestors` metadataattribut överförs. (ASSETS-22966)
* Sessionsläcka i klass `InboxSharingCache` med `user-reader-service`. (CQ-4352513)
* Ofullständig lista över användare och grupper visas när steget&quot;Deltagare i arbetsflödesinitierare&quot; visar användare och grupper för deltagarsteget. Problemet uppstod när en grupp också var medlem i en annan grupp. (NPR-40055)
* Förbättrad rensning av arbetsflöden. (NPR-40459)

## Installera [!DNL Experience Manager] 6.5.17.0{#install}

<!-- Remaining content from here to bottom stays the same except for version updating as needed as per update team feedback. -->

* [!DNL Experience Manager] 6.5.17.0 kräver [!DNL Experience Manager] 6.5. Se [uppgraderingsdokumentation](/help/sites-deploying/upgrade.md) för detaljerade anvisningar. <!-- UPDATE FOR EACH NEW RELEASE -->
* Service Pack-nedladdning finns på Adobe [Programvarudistribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.17.0.zip).
* På en distribution med MongoDB och flera instanser installerar du [!DNL Experience Manager] 6.5.17.0 på en av författarinstanserna med hjälp av Package Manager.<!-- UPDATE FOR EACH NEW RELEASE -->

>[!IMPORTANT]
>
> Adobe rekommenderar inte att du tar bort eller avinstallerar [!DNL Experience Manager] 6.5.17.0-paket. Innan du installerar paketet bör du skapa en säkerhetskopia av `crx-repository` om du måste rulla tillbaka den. <!-- UPDATE FOR EACH NEW RELEASE -->
<!-- For instructions to install Service Pack for Experience Manager Forms, see [Experience Manager Forms Service Pack installation instructions](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md). -->


### Installera Service Pack på [!DNL Experience Manager] 6.5{#install-service-pack}

1. Starta om instansen innan installationen om instansen är i uppdateringsläge (när instansen uppdaterades från en tidigare version). Adobe rekommenderar att du startar om om den aktuella upptiden för en instans är hög.

1. Ta en ögonblicksbild eller en ny säkerhetskopia av din [!DNL Experience Manager] -instans.

1. Hämta Service Pack från [Programvarudistribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.17.0.zip). <!-- UPDATE FOR EACH NEW RELEASE -->

1. Öppna Pakethanteraren och välj **[!UICONTROL Upload Package]** för att överföra paketet. Mer information finns på [Pakethanteraren](/help/sites-administering/package-manager.md).

1. Markera paketet och välj **[!UICONTROL Install]**.

1. Om du vill uppdatera S3-anslutningen stoppar du instansen efter installationen av Service Pack, byter ut den befintliga kopplingen mot en ny binär fil som finns i installationsmappen och startar om instansen. Se [Amazon S3 - datalager](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector).

>[!NOTE]
>
>Dialogrutan för pakethanterarens gränssnitt avslutas ibland när Service Pack installeras. Adobe rekommenderar att du väntar på att felloggarna ska stabiliseras innan du får åtkomst till distributionen. Vänta på de specifika loggarna för avinstallationen av uppdateringspaketet innan du försäkrar dig om att installationen lyckas. Vanligtvis inträffar detta problem i [!DNL Safari] webbläsare, men kan ibland inträffa i vilken webbläsare som helst.

**Automatisk installation**

Det finns två olika metoder som du kan använda för att installera automatiskt [!DNL Experience Manager] 6.5.17.0<!-- UPDATE FOR EACH NEW RELEASE -->

* Placera paketet i `../crx-quickstart/install` när servern är tillgänglig online. Paketet installeras automatiskt.
* Använd [HTTP-API från Package Manager](/help/sites-administering/package-manager.md#package-share). Använd `cmd=install&recursive=true` så att de kapslade paketen installeras.

>[!NOTE]
>
>Experience Manager 6.5.17.0 stöder inte installation av Bootstrap. <!-- UPDATE FOR EACH NEW RELEASE -->

**Validera installationen**

Om du vill veta vilka plattformar som är certifierade för att fungera med den här versionen kan du läsa [tekniska krav](/help/sites-deploying/technical-requirements.md).

1. Produktinformationssidan (`/system/console/productinfo`) visar den uppdaterade versionssträngen `Adobe Experience Manager (6.5.17.0)` under [!UICONTROL Installed Products]. <!-- UPDATE FOR EACH NEW RELEASE -->

1. Alla OSGi-paket är antingen **[!UICONTROL ACTIVE]** eller **[!UICONTROL FRAGMENT]** i OSGi Console (Use Web Console: `/system/console/bundles`).

1. OSGi-paketet `org.apache.jackrabbit.oak-core` är version 1.2.2.15 eller senare (Använd webbkonsol: `/system/console/bundles`). <!-- NPR-40398 for 6.5.17.0 --> <!-- OAK Oak oak VERSION -MAY- NEED TO BE UPDATED FOR EACH NEW RELEASE -->

### Installera Service Pack för [!DNL Experience Manager] Forms{#install-aem-forms-add-on-package}

Anvisningar om hur du installerar Service Pack på Experience Manager Forms finns i [Installationsanvisningar för Experience Manager Forms Service Pack](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md).

### Installera GraphQL Index Package för Experience Manager Content Fragments{#install-aem-graphql-index-add-on-package}

Kunder som använder GraphQL måste installera [Experience Manager Content Fragment with GraphQL Index Package 1.1.1](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/cfm-graphql-index-def-1.1.1.zip).

På så sätt kan du lägga till den indexdefinition som krävs baserat på de funktioner som de faktiskt använder.

Om du inte installerar det här paketet kan GraphQL-frågor bli långsamma eller misslyckas.

>[!NOTE]
>
>Installera endast det här paketet en gång per instans; den behöver inte installeras om med varje Service Pack.

### UberJar{#uber-jar}

UberJar för [!DNL Experience Manager] 6.5.17.0 finns i [Maven Central-arkivet](https://repo.maven.apache.org/maven2/com/adobe/aem/uber-jar/6.5.17/). <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

Information om hur du använder UberJar i ett Maven-projekt finns i [använda UberJar](/help/sites-developing/ht-projects-maven.md) och inkludera följande beroende i projektens POM: <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

```shell
<dependency>
     <groupId>com.adobe.aem</groupId>
     <artifactId>uber-jar</artifactId>
     <version>6.5.17</version>
     <scope>provided</scope>
</dependency>
```

>[!NOTE]
>
>UberJar och andra tillhörande artefakter finns tillgängliga i Maven Central Repository i stället för i Adobe Public Maven-arkivet (`repo.adobe.com`). Huvudfilen för UberJar har bytt namn till `uber-jar-<version>.jar`. Så det finns ingen `classifier`, med `apis` som värdet, för `dependency` -tagg.

## Föråldrade funktioner{#removed-deprecated-features}

Nedan finns en lista över funktioner som är markerade som borttagna [!DNL Experience Manager] 6.5.7.0 Funktioner markeras som borttagna från början och senare i en framtida version. Ett alternativt alternativ anges.

Granska om du använder en funktion eller en funktion i en distribution. Planera också att ändra implementeringen så att ett alternativt alternativ används.

| Yta | Funktion | Ersättning |
|---|---|---|
| Integreringar | Skärmen **[!UICONTROL Experience Manager Cloud Services Opt-In]** har tagits bort sedan [!DNL Experience Manager] och [!DNL Adobe Target] integreringen uppdateras i [!DNL Experience Manager] 6.5. Integreringen stöder Adobe Target Standard API. API:t använder autentisering via Adobe IMS och [!DNL Adobe I/O Runtime]. Det stöder den växande rollen för Adobe Launch till instrument [!DNL Experience Manager] för analys och personalisering är anmälningsguiden funktionellt irrelevant. | Konfigurera systemanslutningar, Adobe IMS-autentisering och [!DNL Adobe I/O Runtime] integreringar via respektive [!DNL Experience Manager] molntjänster. |
| Anslutningar | Adobe JCR Connector för Microsoft® SharePoint 2010 och Microsoft® SharePoint 2013 är föråldrad för [!DNL Experience Manager] 6.5. | Ej tillämpligt |

## Kända fel{#known-issues}

<!-- THESE KNOWN ISSUES CARRY OVER EACH RELEASE. THE "PRODUCT UPDATES TEAM" IS SUPPOSED TO VERIFY EACH ISSUE AND LET YOU KNOW IF ANYTHING NEEDS TO BE ADDED, DELETED, OR CHANGED IN THIS LIST.
 -->
<!-- REMOVED AS PER CQDOC-20022, JANUARY 23, 2023 * If you install [!DNL Experience Manager] 6.5 Service Pack 10 or a previous service pack on [!DNL Experience Manager] 6.5, the runtime copy of your assets custom workflow model (created in `/var/workflow/models/dam`) is deleted.
To retrieve your runtime copy, Adobe recommends to synchronize the design-time copy of the custom workflow model with its runtime copy using the HTTP API:
`<designModelPath>/jcr:content.generate.json`. -->

* Uppdatera dina GraphQL-frågor som kan ha använt ett anpassat API-namn för innehållsmodellen till att i stället använda standardnamnet för innehållsmodellen.

* En GraphQL-fråga kan använda `damAssetLucene` index i stället för `fragments` index. Den här åtgärden kan leda till att GraphQL-frågor misslyckas eller tar lång tid att köra.

   För att åtgärda problemet `damAssetLucene` måste konfigureras så att följande två egenskaper ingår:

   * `contentFragment`
   * `model`

   När indexdefinitionen har ändrats krävs en omindexering (`reindex` = `true`).

   Efter dessa steg bör GraphQL-frågorna gå snabbare.

* Som [!DNL Microsoft® Windows Server 2019] stöder inte [!DNL MySQL 5.7] och [!DNL JBoss® EAP 7.1], [!DNL Microsoft® Windows Server 2019] stöder inte körklara installationer för [!DNL Experience Manager Forms 6.5.10.0].

* Om du uppgraderar [!DNL Experience Manager] från 6.5.0 till 6.5.4 till senaste Service Pack på Java™ 11, se `RRD4JReporter` undantag i `error.log` -fil. Starta om instansen av [!DNL Experience Manager]. <!-- THIS BULLET POINT WAS UPDATED AS PER CQDOC-20021, JANUARY 23, 2023 -->

* Användare kan byta namn på en mapp i en hierarki i [!DNL Assets] och publicera en kapslad mapp i [!DNL Brand Portal]. Mappens namn uppdateras dock inte i [!DNL Brand Portal] tills rotmappen publiceras på nytt.

* När en användare väljer att konfigurera ett fält för första gången i ett adaptivt formulär visas inte alternativet att spara en konfiguration i egenskapsläsaren. Om du väljer att konfigurera ett annat fält i det adaptiva formuläret i samma redigerare åtgärdas problemet.

* Följande fel och varningsmeddelanden kan visas under installationen av [!DNL Experience Manager] 6.5.x.x:
   * &quot;När Adobe Target-integreringen är konfigurerad i [!DNL Experience Manager] med Target Standard API (IMS-autentisering) och sedan exportera Experience Fragments till Target så att fel erbjudandetyper skapas. I stället för att skriva&quot;Experience Fragment&quot;/källa&quot;Adobe Experience Manager&quot; skapar Target flera erbjudanden med typen&quot;HTML&quot;/källa&quot;Adobe Target Classic&quot;.
   * `com.adobe.granite.maintenance.impl.TaskScheduler`: Inga underhållsfönster hittades vid granit/drift/underhåll.
   * Validering på serversidan av adaptiva formulär misslyckas när sammanställningsfunktioner som SUM, MAX och MIN används (CQ-4274424).
   * `com.adobe.granite.maintenance.impl.TaskScheduler` - Inga underhållsfönster hittades vid granit/drift/underhåll.
   * Aktiveringspunkten i en interaktiv Dynamic Media-bild syns inte när du förhandsvisar mediefilen via Shoppable Banner Viewer.
   * `com.adobe.cq.social.cq-social-jcr-provider bundle com.adobe.cq.social.cq-social-jcr-provider:1.3.5 (395)[com.adobe.cq.social.provider.jcr.impl.SpiSocialJcrResourceProviderImpl(2302)]` : Tidsgränsen överskreds i väntan på att registerändringen skulle slutföras utan registrering.

* När du försöker flytta, ta bort eller publicera antingen innehållsfragment, platser eller sidor uppstår ett problem när referenser till innehållsfragment hämtas, eftersom bakgrundsfrågan misslyckas. Funktionen fungerar alltså inte.
Du måste lägga till följande egenskaper i indexdefinitionsnoden för att få en korrekt åtgärd `/oak:index/damAssetLucene` (ingen omindexering krävs):

   ```xml
   "tags": [
       "visualSimilaritySearch"
     ]
   "refresh": true
   ```

* På JBoss® 7.1.4-plattformen när användaren installerar Experience Manager 6.5.16.0 eller senare Service Pack, `adobe-livecycle-jboss.ear` distributionen misslyckas.
* JDK-version senare än 1.8.0_281 stöds inte för WebLogic JEE-server.

## OSGi-paket och innehållspaket som ingår{#osgi-bundles-and-content-packages-included}

Följande textdokument listar de OSGi-paket och innehållspaket som ingår i [!DNL Experience Manager] 6.5.17.0: <!-- UPDATE FOR EACH NEW RELEASE -->

* [Förteckning över OSGi-paket som ingår i Experience Manager 6.5.17.0](/help/release-notes/assets/65170_bundles.txt) <!-- UPDATE FOR EACH NEW RELEASE -->
* [Förteckning över innehållspaket som ingår i Experience Manager 6.5.17.0](/help/release-notes/assets/65170_packages.txt) <!-- UPDATE FOR EACH NEW RELEASE -->

## Begränsade webbplatser{#restricted-sites}

Dessa webbplatser är bara tillgängliga för kunder. Om du är kund och behöver åtkomst kontaktar du din kontoansvarige på Adobe.

* [Nedladdning av produkt på licensing.adobe.com](https://licensing.adobe.com/)
* [Kontakta Adobe kundsupport](https://experienceleague.adobe.com/docs/customer-one/using/home.html).

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] produktsida](https://business.adobe.com/products/experience-manager/adobe-experience-manager.html)
>* [[!DNL Experience Manager] 6.5-dokumentation](https://experienceleague.adobe.com/docs/experience-manager-65.html)
>* [Prenumerera på produktuppdateringar med Adobe prioritet](https://www.adobe.com/subscription/priority-product-update.html)

