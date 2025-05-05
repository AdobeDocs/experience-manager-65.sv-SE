---
title: Cumulative Key Features and Enhancements in Adobe Experience Manager 6.5.
description: En kumulativ lista över viktiga funktioner och förbättringar som gjorts i Adobe Experience Manager 6.5 från de tidigare åtta Service Pack-versionerna.
content-type: reference
docset: aem65
feature: Release Information
role: User,Admin,Architect,Developer
exl-id: 01fe5b53-2244-445f-a4d0-bd58ea38b611
solution: Experience Manager
source-git-commit: 54b508809733ed86798558aee50f8c7b5de00af9
workflow-type: tm+mt
source-wordcount: '2308'
ht-degree: 0%

---

# Kumulativa nyckelfunktioner och förbättringar

En kumulativ lista med viktiga funktioner och förbättringar i Adobe Experience Manager 6.5 för de föregående åtta Service Pack-versionerna.

Se även [Versionsinformation om Adobe Experience Manager 6.5 Senaste Service Pack](/help/release-notes/release-notes.md).

## AEM 6.5, Service Pack 18-7 december 2023

* Användare av sidredigeraren/bildkomponenten har aktiverat Sites för att referera till resurser från Assets Cloud Service. (SITES-13448, SITES-13433)
* AEM har nu stöd för sortering på serversidan för snabbare projektnavigering i listvyn. Projektnoder sorteras baserat på den användarvalda kolumnen innan de visas i gränssnittet.

### [!DNL Forms]

* **Nya kärnkomponenter för adaptiva formulär**: Lodräta flikar, villkor och kryssruta läggs till för att öka formulärens skalbarhet.
   * **[Kryssrutekomponent](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/checkbox.html?lang=sv-SE)**: Adaptiv Forms baserad på kärnkomponenter kan nu innehålla en kryssrutekomponent. Det gör att användare kan göra binära val, markera eller avmarkera ett visst alternativ. Det visas vanligtvis som en liten ruta som du kan klicka på eller peka på för att växla mellan två lägen: markerad och avmarkerad. Kryssrutan är ett vanligt formulärelement som används för att ange ett ja/nej- eller sant/falskt-val.

   * **[Villkorskomponent](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/terms-and-conditions.html?lang=sv-SE)**: Adaptiv Forms baserad på kärnkomponenter kan nu innehålla en villkorskomponent. Det gör det möjligt för Forms-författare att införa ett specifikt avsnitt i formuläret där användarna presenteras med de villkor eller juridiska avtal som är kopplade till användningen av en tjänst, produkt eller plattform. Den här komponenten är utformad för att informera användare om de regler, bestämmelser och skyldigheter som de godkänner genom att skicka in formuläret.

     ![Lodräta flikar, villkor och kryssrutekomponenter](/help/forms/using/assets/forms-components.png)

   * **[Komponent för lodräta flikar](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/vertical-tabs.html?lang=sv-SE)**: Adaptiv Forms baserad på kärnkomponenter kan nu ordna formulärinnehåll i en lodrät lista med flikar, vilket ger en strukturerad och navigeringsbar layout. Om du använder vertikala flikar i ett formulär kan det förbättra användarupplevelsen genom att förenkla navigeringen och förbättra organisationen av formulärinnehållet, särskilt i situationer där ett formulär innehåller flera avsnitt eller komplex information.

* **[64-bitarsversionen av AEM Forms Designer](/help/forms/using/installing-configuring-designer.md)**: 64-bitarsversionen av AEM Forms Designer ger bättre prestanda, skalbarhet och minneshantering så att du kan skapa formulär. Med 64-bitarsarkitekturen kan du enkelt hantera ännu större och mer komplexa projekt, vilket ger smidiga designarbetsflöden och optimerad effektivitet. Förbättra dina formulärdesignmöjligheter och ta till vara framtiden för AEM Forms Designer med denna banbrytande release.

* **[Anslut en adaptiv Forms med Microsoft® SharePoint List](/help/forms/using/configuring-submit-actions.md#submit-to-microsoft&reg;-sharepoint-list)**: AEM Forms erbjuder en körklar integrering för att skicka formulärdata direkt till SharePoint List, så att du kan använda funktionerna i SharePoint Lists. Du kan konfigurera Microsoft® SharePoint List som en datakälla för en formulärdatamodell och använda Skicka med formulärdatamodellen för att ansluta ett anpassat formulär med SharePoint List.

* **[Stöd för att konfigurera dokumentegenskaper för adaptiva formulärfragment](/help/forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md)**: Nu kan du enkelt anpassa dina adaptiva formulärfragment och dess fält i den adaptiva formulärredigeraren.

* **64-bitars XMLFM**: Med 64-bitarsitereringen av XMLFM får du bättre prestanda, skalbarhet och förbättrad minneshantering. Det är den första inbyggda 64-bitarstjänsten som körs på serversidan. Genom att utnyttja sin inneboende förmåga att få tillgång till större minnesresurser jämfört med sin 32-bitars motsvarighet, ger XMLFM 64-bitars smidig hantering av större återgivningsarbetsbelastningar. Denna milstolpe innebär inte bara ett prestandasprång utan även viktiga förbättringar av det systemspecifika tjänstramverket i AEM Forms Server. Den här uppdateringen gör att AEM Forms Server stöder alla inbyggda 64-bitarstjänster.

## AEM 6.5, Service Pack 18-24 augusti 2023

* Assets, Dynamic Media - [Stöd för flera bildtexter och ljudspår för videofilmer i Dynamic Media](/help/assets/video.md#about-msma) - Nu kan du enkelt lägga till flera undertexter och flera ljudspår i en primär video. Detta innebär att videoklippen är tillgängliga för alla mottagare världen över. Du kan anpassa en enda publicerad primär video till en global publik på flera språk och följa riktlinjer för tillgänglighet för olika geografiska regioner. Författare kan också hantera undertexter och ljudspår från en enda flik i användargränssnittet.
* Assets - Från sökresultaten kan du nu navigera till den mapplats som innehåller en resurs så att du kan utföra olika resurshanteringsåtgärder.
* Sites Polaris Picker i Content Fragments har förbättrat prestandan.
* Användare av sidredigeraren/bildkomponenten har aktiverat Sites för att referera till resurser från Assets Cloud Service.
* För att snabbt hitta ett projekt i listvyn, där du kan ha många projekt i systemet, har Adobe nu stöd för sortering på serversidan. Projektnoder sorteras på serverdelen baserat på den kolumn som valts av användaren innan de återges i användargränssnittet.
* AEM 6.5.18.0 stöder MongoDB 5.0 till 6.0.

### [!DNL Forms]

* **[Förbättrad felhantering med anpassade felhanterare i regelredigeraren](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-advanced-authoring/standard-validation-error-messages-adaptive-forms.html?lang=sv-SE)** - Du kan nu anropa en anpassad funktion (med klientbibliotek) som svar på ett fel som returnerats av en extern tjänst. Och ni kan ge slutanvändarna ett skräddarsytt svar. Du kan också vidta specifika åtgärder för fel som returneras av en tjänst. Du kan till exempel anropa ett anpassat arbetsflöde i serverdelen för specifika felkoder eller informera kunden om att tjänsten är nere

* **[Förbättrat arbetsflödessteg i Adobe Sign](https://experienceleague.adobe.com/docs/experience-manager-65/forms/workflows/aem-forms-workflow-step-reference.html?lang=sv-SE#sign-document-step)** - Arbetsflödessteget i Adobe Sign i AEM-arbetsflöden är tillgängligt med följande förbättringar.

   * **Förbättrad säkerhet med offentlig ID-baserad autentisering för Adobe Sign** - Adobe Acrobat Sign ID-baserad autentisering för myndigheter erbjuder ytterligare ett verifieringslager. Det gör det möjligt för användare att autentisera sin identitet med hjälp av ett foto-ID (körkort, nationellt ID, pass). Genom att använda pålitliga identifieringsdokument ger den här förbättringen ytterligare tillförlitlighet i signeringsprocessen, vilket gör den idealisk för scenarier som kräver högre säkerhet, regelefterlevnad och användarvalidering.

   * **Förbättrad genomskinlighet med granskningsspår för Adobe Sign-dokument** - Använd funktionen Granskningsspår för att få detaljerade insikter om livscykeln för dina Adobe Sign-dokument. Med granskningsspåret kan du nu föra ett omfattande register över alla åtgärder och interaktioner som rör dina dokument. Detta inkluderar information som vem som visade, redigerade eller signerade dokumentet, tillsammans med tidsstämplar för varje händelse. Den här förbättringen är avgörande för att upprätthålla regelefterlevnaden, lösa tvister och säkerställa integriteten för dina digitala avtal.


   * **Utökade roller för avtalsmottagare utöver bara signeraren** - Med Adobe Acrobat Sign kan du utöka rollerna för avtalsmottagare till andra än bara signeraren för att bättre matcha deras arbetsflödesbehov. När det här alternativet är aktiverat kan varje mottagare i ett avtal konfigureras individuellt, med signerare som standard.


* **[AEM Forms i JEE med fullständigt installationsprogram](https://experienceleague.adobe.com/docs/experience-manager-65/forms/install-aem-forms/jee-installation/aem-forms-jee-supported-platforms.html?lang=sv-SE)** - Service Pack har ett fullständigt installationsprogram för AEM Forms i JEE som har stöd för flera nya programkombinationer, inklusive:
   * Microsoft® Windows Server 2022
   * Microsoft® Active Directory 2022
   * Oracle WebLogic 14C i Windows Server 2022
   * Red Hat® JBoss® 7.4.10
   * MongoDB 6.0 <!-- it was previously MongoDB 4.4 -->
   * MySQL JDBC Connector 8

Om du installerar eller planerar att använda den senaste programvaran för din AEM 6.5 Forms i JEE-miljö rekommenderar Adobe att du använder AEM 6.5.18.0 Forms i JEE-fullversionen. En fullständig lista över nyligen tillagda och ersatta program finns i dokumentationen för AEM Forms on JEE eller AEM Forms on OSGi.

## AEM 6.5, Service Pack 17 - 25 maj 2023

* **Förbättringar av sökupplevelsen** - Nu kan du snabbt utföra följande åtgärder på resurserna som visas i sökresultaten:
   * Skapa ett arbetsflöde
   * Skapa en version
   * Relatera eller inte relatera tillgångar

  Du behöver inte navigera till resursplatsen och visa dess egenskaper för att utföra dessa åtgärder.
* **Dynamiska medier _ögonblicksbild_**- Experimentera med testbilder eller dynamiska medie-URL:er för att se utdata från olika bildmodifierare och optimering av smarta bilder för filstorlek (med WebP- och AVIF-leverans), nätverksbandbredd och enhetspixelproportioner. Se [Dynamisk medieögonblicksbild](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/images/dynamic-media-snapshot.html?lang=sv-SE).
* **DASH-direktuppspelning med dynamiska media** - nytt protokoll (DASH - Dynamic Adaptive Streaming over HTTP) startades för adaptiv direktuppspelning i Dynamic Media-leverans (med CMAF aktiverat). Finns nu för alla regioner.
* **Integrering av Experience Manager Sites- och innehållsfragment med Assets nästa generation av dynamiska media** - Användare av Experience Manager Assets as a Cloud Service nästa generation av dynamiska media kan nu använda dessa molnbaserade resurser för redigering och leverans med lokala eller Managed Services-instanser av Experience Manager Sites 6.5.

### [!DNL Forms]

* **[Adaptiv Forms i AEM sidredigerare](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md)**: Nu kan du använda AEM sidredigerare för att snabbt skapa och lägga till flera formulär på webbplatsens sidor. Med den här funktionen kan skribenter skapa sömlösa datainhämtningsmöjligheter på webbplatssidor med hjälp av kraften i adaptiva formulärkomponenter, inklusive dynamiskt beteende, validering, dataintegrering, generering av dokument för post- och affärsprocessautomatisering. Du kan:
   * Skapa ett anpassat formulär genom att dra och släppa formulärkomponenter i den adaptiva Forms Container-komponenten i AEM Sites Editor eller Experience Fragments.
   * Använd Adaptive Forms Wizard i AEM Sites Editor för att skapa formulär oberoende av sajtsidor, vilket ger dig frihet att återanvända sådana formulär på flera sidor.
   * Lägg till flera formulär på en webbplatssida, effektivisera användarupplevelsen och ge större flexibilitet.
* **[Stöd för reCAPTCHA Enterprise i Experience Manager Forms](/help/forms/using/captcha-adaptive-forms.md)**: Stöd för reCAPTCHA Enterprise i Experience Manager Forms har lagts till, vilket ger förbättrat skydd mot bedräglig aktivitet och skräppost, utöver det befintliga stödet för Google reCAPTCHA v2.
* **[Stöd för Adobe Acrobat Sign för offentlig sektor med Experience Manager Forms](/help/forms/using/adobe-sign-integration-adaptive-forms.md)**: AEM Forms är nu integrerat med Adobe Acrobat Sign för offentlig sektor (FedRAMP-kompatibelt). Integreringen ger en avancerad nivå av regelefterlevnad och säkerhet för e-signaturer med inskickade adaptiva formulär för myndighetskonton (myndigheter och myndigheter). Integreringen med Adobe Acrobat Sign for Government gör det möjligt för Adobe partners och myndighetskunder att använda elektroniska signaturer i Adaptive Forms för några av de mest verksamhetskritiska och känsliga verksamhetsområdena. Detta extra säkerhetsskikt säkerställer att alla e-signaturer är helt kompatibla med FedRAMP Moderate och ger Adobe myndighetskunder sinnesro.
* **Aktivera Salesforce-integrering med Experience Manager Forms för datautbyte**: Konfigurera integreringen mellan Experience Manager Forms och Salesforce-programmet med hjälp av inloggningsflödet för OAuth 2.0-klienten. Den här funktionen möjliggör säker och direkt autentisering och behörighet av programmet och möjliggör smidig kommunikation utan användarinblandning.
* **Optimering och förbättrad funktionalitet för arbetsflödesmotorn**: Öka arbetsflödesmotorernas prestanda genom att minimera antalet arbetsflödesinstanser. Förutom statusvärdena `COMPLETED` och `RUNNING` stöder arbetsflödet även tre nya statusvärden: `ABORTED`, `SUSPENDED` och `FAILED`.

## AEM 6.5, Service Pack 16 - 23 februari 2023

Det nya protokollet DASH (Dynamic Adaptive Streaming over HTTP) startades för strömning med adaptiv bithastighet i Dynamic Media Video-leverans (med CMAF [Common Media Application Format] aktiverat).

* Adaptiv direktuppspelning (DASH/HLS) ger en bättre tittarupplevelse för videor.
* DASH är det internationella standardprotokollet för strömning av adaptiv video och är en vida spridd bransch.
* Finns nu i Asien-Stillahavsområdet och Nordamerika och kommer snart i Europa-Mellanöstern-Afrika.

### [!DNL Forms]

* Med [Headless Adaptive Forms](https://experienceleague.adobe.com/docs/experience-manager-headless-adaptive-forms/using/overview.html?lang=sv-SE) kan dina utvecklare skapa, publicera och hantera interaktiva formulär som kan nås och interagera med via API:er, i stället för via ett traditionellt grafiskt användargränssnitt.

* [Adaptiva Forms Core-komponenter](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=sv-SE#features) är en uppsättning med 24 BEM-kompatibla komponenter med öppen källkod som bygger på grundvalen för Adobe Experience Manager WCM Core-komponenter. Dessa komponenter har öppen källkod och ger utvecklare möjlighet att enkelt anpassa och utöka komponenterna så att de passar organisationens specifika behov. Alla som har befintliga kunskaper för att anpassa [WCM Core-komponenter](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/get-started/authoring.html?lang=sv-SE) kan enkelt anpassa och formatera de här komponenterna.

* Reader Extension-tjänsten på OSGi har nu olika alternativ för att aktivera import- och exportanvändningsrättigheter för en PDF för import eller export av data i Adobe Acrobat Reader.

## AEM 6.5, Service Pack 15 - 24 november 2022

### [!DNL Forms]

* AEM Forms Designer finns nu på [spanska](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=sv-SE).
* Du kan nu använda [OAuth2 för att autentisera med e-postserverprotokoll för Microsoft® Office 365 (SMTP och IMAP)](/help/forms/using/oauth2-support-for-mail-service.md).
* Du kan ställa in egenskapen [Revalidate på server](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-submit-actions-and-metadata-submission/configuring-submit-actions.html?lang=sv-SE#enabling-server-side-validation-br) på true om du vill identifiera dolda fält som ska uteslutas från ett postdokument på serversidan.
* AEM Forms Designer kräver 32-bitarsversionen av Visual C++ 2019 Redistributable (x86).

## AEM 6.5, Service Pack 14-25 augusti 2022

Endast felkorrigeringar.

## AEM 6.5, Service Pack 13 - 26 maj 2022

* Använd osynlig CAPTCHA i adaptiv form: nu kan du använda en osynlig CAPTCHA för att visa CAPTCHA-utmaningen endast om det finns misstänkt aktivitet. Om ingen misstänkt aktivitet hittas visas inte CAPTCHA-utmaningen. Det gör det lättare att bedöma om formulär ska fyllas i av människor utan att det behövs kryssrutor, minska anpassningsarbetet och förbättra slutanvändarens upplevelse.

* Stöd har lagts till för att hämta svarshuvuden i efterbearbetningen av formulärdatamodellen för REST-slutpunkter.

* När du genererar en adaptiv formuläröversättningsfil är nu samma textsekvens som den genererade XLIFF-filen identisk med komponentsekvensen i motsvarande adaptiva formulär.

* När du lokaliserar ett adaptivt formulär och gör en liten ändring av texten i basspråket, saknas den fullständiga översättningen för alla andra språk. Problemet har åtgärdats i [!DNL Experience Manager] 6.5.13.0.

* Tillgänglighetsförbättringar för Forms:

   * Stöd för skärmläsare har lagts till för att identifiera tabellens rubrik och brödtext som fortsätter och anslutna enheter. Det hjälper skärmläsare att navigera i tabellerna på rätt sätt. (NPR-37139)
   * Stöd för att skärmläsare ska sluta navigera på HTML arbetsyta tills en dialogruta är öppen har lagts till.

## AEM 6.5, Service Pack 12 - 24 februari 2022

* När du har konfigurerat en anslutning mellan distributioner av fjärr-DAM och platser, blir resurserna på fjärr-DAM tillgängliga i Sites-distributionen. Nu kan du uppdatera, ta bort, byta namn på och flytta resurser eller mappar i fjärr-DAM. Uppdateringarna, med viss fördröjning, är automatiskt tillgängliga i Sites-distributionen.
* Det går nu som standard att överföra en live-kopieringskälla till flera live-kopior, utan att en ritningskonfiguration krävs.
* Status för pågående asynkrona åtgärder visas nu i användargränssnittet för att förhindra att användare av misstag utlöser flera asynkrona åtgärder på samma sökväg.
* Stöd för IMS-baserad autentisering finns för API:er i Analytics 2.0.
* API-stöd för JSON-erbjudandetypsfragment.
* Erbjudandet gäller nu för Delete-erbjudandet (Experience Fragment API) i IMS.
* Den inbyggda databasen (Apache Jackrabbit Oak) är fortfarande 1.2.9.
