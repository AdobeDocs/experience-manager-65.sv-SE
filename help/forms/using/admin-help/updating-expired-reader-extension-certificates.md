---
title: Uppdaterar tjänstcertifikat för Reader Extension som upphört att gälla
description: 'Reader utökade dokument fungerar inte, uppdatera certifikat '
source-git-commit: a26e4fb53458beae9b259e5ee5dc74a95264f9e1
workflow-type: tm+mt
source-wordcount: '1575'
ht-degree: 0%

---


# Uppdaterar tjänstcertifikat för Reader Extension som upphört att gälla {#Updating-expired-Reader-Extension-service-certificates}

Adobe Experience Manager Forms (AEM Forms)-kunder med Adobe Managed Services eller On-Local Enterprise Base-licenser har rätt att använda Reader Extension Service. Med tjänsten kan man enkelt utbyta interaktiva PDF-dokument genom att utöka Adobe Reader funktionalitet med ytterligare användarrättigheter. Tjänsten lägger till användarrättigheter i ett PDF-dokument och aktiverar funktioner som vanligtvis inte är tillgängliga när ett PDF-dokument öppnas med Adobe Acrobat Reader DC, till exempel för att lägga till kommentarer i ett dokument, fylla i formulär och spara dokumentet. Tredjepartsanvändare behöver inte ytterligare programvara eller plugin-program för att kunna arbeta med upphovsrättsaktiverade dokument. PDF-dokument som har användarrättigheter tillagda kallas för rättighetsaktiverade dokument. En användare som öppnar ett rättighetsaktiverat PDF-dokument i Adobe Reader kan utföra de åtgärder som är aktiverade för det dokumentet.

Adobe använder en PKI (Public Key Infrastructure) för att utfärda digitala certifikat för användning vid licensiering och funktionshantering. Adobe har utfärdat certifikat under certifikatutfärdaren&quot;Adobe Root CA&quot;, som enligt planerna ska upphöra att gälla den 7 januari 2023. Det kommer att leda till att alla certifikat som utfärdas under den här certifikatutfärdaren upphör att gälla. När certifikatet har upphört att gälla fungerar inte längre alla funktioner som är beroende av certifikatet. Ett läsarutökat PDF-dokument som tillåter att du lägger till kommentarer med Adobe Acrobat Reader slutar fungera för kunder efter 7 januari 2023. För att lösa problemet bör administratören för Reader Extension Service, som använder gamla certifikat, erhålla och återanvända nya certifikat som utfärdas av nya Adobe Root CA G2 i sina PDF-dokument (läsaren utökar PDF-dokumenten med nya certifikat).

Certifikatets förfallodatum påverkar både AEM Forms på JEE och AEM Forms på OSGi-stackar. Båda högarna har olika instruktioner. När du har mött [krav](#Pre-requisites) och [skaffa nya certifikat](#obtain-the-certificates)Välj en av följande sökvägar, beroende på vilken hög du har:

* [Uppdatera certifikat för en AEM Forms i JEE-miljö](#Updating-and-Applying-certificates-for-an-AEM-Forms-on-JEE-environment)
* [Uppdatera certifikat för en AEM Forms i OSGi-miljö](#Updating-and-applying-certificates-for-an-AEM-Forms-on-OSGi-environment)

>[!NOTE]
>
>I dokumentet används termcertifikat och autentiseringsuppgifter som kan bytas ut.

## Krav {#Pre-requisites}

För att uppdatera certifikaten krävs åtgärder som är tillgängliga på AEM Forms administratörskonsol och API:er för tillägg i Reader som tillhandahålls av AEM Forms. Dokumentet är avsett för användare och administratörer som har kunskap om att använda Forms-API:er i Adobe Experience Manager. Innan du börjar ser du till att:

* användaren har administratörsbehörighet för den underliggande AEM Forms-miljön.
* användaren har konfigurerat [utvecklingsmiljö](https://experienceleague.adobe.com/docs/experience-manager-65/developing/devtools/howto-projects-eclipse.html) och har tillgång till den.
* hämta certifikaten.

### Hämta certifikaten {#obtain-the-certificates}

Behörighetsinformationen levereras som ett digitalt certifikat som innehåller den offentliga nyckeln, den privata nyckeln och det lösenord som används för att komma åt inloggningsuppgifterna.

Om din organisation köper en produktionsversion av Reader Extensions levereras behörighetsuppgifterna om via Adobe Licensing Website (LWS). En behörighetsinformation för produktion är unik för din organisation och kan aktivera de specifika användarrättigheter som du behöver.

Om du har köpt Reader Extensions via en partner eller en programvaruleverantör som har integrerat Reader Extensions i sina program, får du rättighetsinformationen från den partnern som i sin tur får denna inloggningsinformation från Adobe.

>[!NOTE]
>
>Autentiseringsuppgifterna för rättigheter kan inte användas för typisk dokumentsignering eller identitetsförsäkran. För dessa program kan du använda ett självsigneringscertifikat eller hämta ett identitetscertifikat från en certifikatutfärdare (CA).

Följande typer av rättighetsuppgifter är tillgängliga:

**Kundutvärdering**: En autentiseringsuppgift med en kort giltighetsperiod som tillhandahålls kunder som vill utvärdera Reader-tillägg. Användningsrättigheter som tillämpas på dokument som använder den här inloggningsuppgifterna förfaller när inloggningsuppgifterna förfaller. Den här typen av autentiseringsuppgifter är bara giltig i två till tre månader.

**Produktion**: En autentiseringsuppgift med en lång giltighetsperiod som tillhandahålls kunder som har köpt den fullständiga produkten. Produktionsautentiseringsuppgifterna är unika för varje kund men kan installeras på flera system.

Om du redan har använt certifikat för läsaren för att utöka PDF-filer hämtar du ett produktionscertifikat från [Adobe licenswebbplats (LWS)](https://licensing.adobe.com/).

## Uppdatera och använda certifikat för en AEM Forms i JEE-miljö {#Updating-and-Applying-certificates-for-an-AEM-Forms-on-JEE-environment}

Uppdatering och tillämpning av nya certifikat på AEM Forms i JEE-stacken kräver import av nya autentiseringsuppgifter, borttagning av användningsrättigheter från befintliga PDF-dokument och användning av användningsrättigheter. Du kan använda Admin Console för att importera autentiseringsuppgifter och AEM Forms Reader Extension API:er för att ta bort och tillämpa användningsrättigheter.

### Importera och konfigurera autentiseringsuppgifter

Du kan använda hanteringssidorna för Trust Store för att importera nya eller nya autentiseringsuppgifter. Trust Store kan innehålla fler än en Reader-autentiseringsuppgift. Du måste ange en av dessa autentiseringsuppgifter som standardautentiseringsuppgifter för Reader Extensions. Standardautentiseringsuppgifterna används när en Workbench-användare inte kan avgöra vilka autentiseringsuppgifter som ska användas när processen skapas. Dessa regler gäller för standardautentiseringsuppgifter:

* Om du importerar en autentiseringsuppgift för Reader Extensions och Trust Store inte innehåller några andra autentiseringsuppgifter för Reader Extensions, anges den som standard.
* Om du importerar autentiseringsuppgifter för Reader-tillägg med standardalternativet markerat tas standardtypen bort från en befintlig standardautentiseringsuppgift. De importerade autentiseringsuppgifterna blir standard.
* Du kan inte ta bort en standardautentiseringsuppgift för Reader-tillägg. Om du vill ta bort standardautentiseringsuppgifterna anger du först en annan autentiseringsuppgift som standard. Ett undantag till den här regeln är att om det bara finns en autentiseringsuppgift kan du ta bort den även om den är standard.
* Du kan inte uppdatera en standardautentiseringsuppgift för Reader Extensions.

Så här importerar du autentiseringsuppgifterna:

1. I administrationskonsolen klickar du på Inställningar > Lita på arkivhantering > Lokala autentiseringsuppgifter.
1. Klicka på Importera och välj Acrobat Reader DC extensions Credential under Trust Store Type.
1. (Valfritt) Om du vill ange att den här autentiseringsuppgiften är standardautentiseringsuppgiften som används med Acrobat Reader DC-tillägg väljer du Standard.
1. Ange en identifierare för autentiseringsuppgifterna i rutan Alias. Den här identifieraren används som visningsnamn för autentiseringsuppgifterna i Acrobat Reader DC-tillägg. Det här aliaset används även för att få åtkomst till autentiseringsuppgifter via programmering med AEM formulär SDK.
1. Klicka på Välj fil för att leta upp autentiseringsuppgifterna, skriv lösenordet för autentiseringsuppgifterna och klicka sedan på OK.

Om felmeddelandet&quot;Det gick inte att importera autentiseringsuppgifter på grund av felaktigt filformat eller felaktigt lösenord&quot; visas kontrollerar du att lösenordet är giltigt.

Du kan också importera och ta bort autentiseringsuppgifter via programmering. (Se [Programmera med AEM](../../developing/credentials.md).)

### Ta bort användningsrättigheter från befintliga PDF-dokument med aktiverade rättigheter

Ta bort användningsrättigheter från befintliga rättighetsaktiverade PDF-dokument innan du lägger till användningsrättigheter med de senaste inloggningsuppgifterna. AEM Forms på JEE innehåller API:er för att ta bort användningsrättigheter. Detaljerade anvisningar finns i [Ta bort användningsrättigheter från PDF-dokument](../../developing/assigning-usage-rights.md#removing-usage-rights-from-pdf-documents).

Information om hur du tar bort användningsrättigheter för AEM Forms i JEE-processer som utvecklats i Workbench finns i [Workbench - hjälp](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/pdf/WorkbenchHelp.pdf).

### Använda användarrättigheter i PDF-dokument

När du har importerat nya inloggningsuppgifter och tagit bort användningsrättigheter från befintliga PDF-dokument med aktiverade rättigheter, lägger du till användningsrättigheter i PDF-dokument med de nya inloggningsuppgifterna. Du kan lägga till användarrättigheter i PDF-dokument med Acrobat Reader DC-tilläggens Java Client API och webbtjänst.  Mer information finns i [Använda användningsbehörighet för PDF-dokument](../../developing/assigning-usage-rights.md#applying-usage-rights-to-pdf-documents).


## Uppdatera och använda certifikat för en AEM Forms i OSGi-miljö {#Updating-and-applying-certificates-for-an-AEM-Forms-on-OSGi-environment}

Uppdatering och tillämpning av nya certifikat på AEM Forms i OSGi-stacken kräver import av nya autentiseringsuppgifter, borttagning av användningsrättigheter från befintliga PDF-dokument och användning av användningsrättigheter. Du kan använda Admin Console för att importera autentiseringsuppgifter och AEM Forms Reader Extension API:er för att ta bort och tillämpa användningsrättigheter.

### Importera autentiseringsuppgifter {#Import-credentials}

I en AEM Forms-miljö på OSGi är autentiseringsuppgifter för Reader Extension associerade med fd-service-användare. Innan du lägger till autentiseringsuppgifter för nyckelbehållaren för fd-användare gör du så här för att skapa en nyckelbehållare:

1. Logga in på din AEM Author-instans som administratör.
1. Gå till **[!UICONTROL Tools]**> **[!UICONTROL Security]**>**[!UICONTROL Users]**.
1. Bläddra nedåt i listan över användare tills du hittar användarkontot för tjänsten.
1. Klicka **[!UICONTROL fd-service]** användare.
1. Klicka på fliken för nyckelbehållare.
1. Klicka på **[!UICONTROL Create KeyStore]**.
1. Ange lösenordet för KeyStore-åtkomst och spara inställningarna för att skapa KeyStore-lösenordet.

När du har skapat nyckelbehållaren lägger du till autentiseringsuppgifter till användaren för fd-service. I följande video förklaras stegen:

>[!VIDEO](https://images-tv.adobe.com/mpcv3/5577/8db8e554-f04b-4fae-8108-b9b5e0eb03ad_1627925794.854x480at800_h264.mp4)

Följande kommando visar information om pfx-filen. Navigera till katalogen som innehåller pfx-filen innan du kör kommandot.

`keytool -v -list -storetype pkcs12 -keystore <name of your .pfx file>`

Exempel: keytool -v -list -storetype pkcs12 -keystore 1005566.pfx där 1005566.pfx är namnet på min pfx-fil

### Ta bort användningsrättigheter från befintliga PDF-dokument med aktiverade rättigheter

Ta bort användningsrättigheter från befintliga rättighetsaktiverade PDF-dokument innan du lägger till användningsrättigheter med de senaste inloggningsuppgifterna. Du kan ta bort användningsrättigheterna för ett dokument genom att anropa API:t removeUsageRights inifrån docAssuranceServiceAPI. Mer information finns i [Ta bort användningsbehörighet](/help/forms/using/aem-document-services-programmatically.md#removing-usage-rights) -dokument.

### Använda användarrättigheter i PDF-dokument

Om du vill lägga till användarrättigheter i en AEM Forms on OSGi-miljö skapar du en anpassad OSGi-tjänst för användningsrättigheter för dokumenten. Du kan också skapa en serverlet med en POST-metod för att returnera läsaren extended PDF till användaren. Detaljerade anvisningar finns i [Använder Reader-tillägg](https://experienceleague.adobe.com/docs/experience-manager-learn/forms/document-services/apply-reader-extension-rights-to-pdf.html).

## Frågor och svar

**Vem ska jag kontakta om jag har ytterligare frågor?**

Du kan kontakta [Stöd för Adobe](https://experienceleague.adobe.com/?support-solution=Experience+Manager#support) eller skaffa en supportanmälan.

**Vad händer om jag inte uppdaterar mitt certifikat före 7 januari 2023?**

När man försöker öppna PDF-dokument Reader Extended med gamla certifikat får man ett felmeddelande och kan inte längre komma åt de utökade läsarfunktionerna. Ett exempelfel är.

`The document has been changed since it was created and use of extended features in no longer available. Please contact the author for the orignal version of this document.`

**Har namnet på den nya beskrivningen ändrats?**

Nya tilläggscertifikat för Reader anger G3-P24 som programnamn i beskrivningen. I de äldre certifikaten nämndes programnamnet P24 i beskrivningen.