---
title: Hantera [!DNL Adobe Stock] resurser
description: Sök, hämta, licensiera och hantera [!DNL Adobe Stock] resurser inifrån [!DNL Adobe Experience Manager]. Använd de licensierade mediefilerna som andra digitala resurser.
contentOwner: Vishabh Gupta
feature: Search, Adobe Stock
role: User, Admin
exl-id: 8ec597df-bb64-4768-bf9c-e8cca4fea25b
source-git-commit: 6d1073003c1b78be848652be0b387889eedbc193
workflow-type: tm+mt
source-wordcount: '2288'
ht-degree: 3%

---

# Använd [!DNL Adobe Stock]-resurser i [!DNL Adobe Experience Manager Assets] {#use-adobe-stock-assets-in-aem-assets}

<!-- old content

[!DNL Experience Manager Assets] provides users the ability to search, preview, save, and license [!DNL Adobe Stock] assets directly from [!DNL Experience Manager]. 

Organizations can integrate their [!DNL Adobe Stock] enterprise plan with [!DNL Experience Manager Assets] to ensure that licensed assets are broadly available for their creative and marketing projects, with the powerful asset management capabilities of [!DNL Experience Manager].

[!DNL Adobe Stock] service provides designers and businesses with access to millions of high-quality, curated, royalty-free photos, vectors, illustrations, videos, templates, and 3D assets for all their creative projects. [!DNL Experience Manager] users are able to quickly find, preview, and license [!DNL Adobe Stock] assets that are saved in [!DNL Experience Manager], without leaving the [!DNL Experience Manager] interface.
-->

<!-- New overview content
-->

[!DNL Adobe Stock] ger designers och företag tillgång till miljontals utvalda och royaltyfria foton, vektorer, illustrationer, videor, mallar och 3D-resurser av hög kvalitet för alla kreativa projekt.

[!DNL Adobe Stock] som standard inkluderar Enterprise-erbjudanden delningsrättigheter i hela organisationen. När en mediefil har hämtats av en användare i organisationen kan andra användare i organisationen identifiera, hämta och använda den här mediefilen utan att behöva licensiera den igen. När en mediefil har licensierats av din organisation är rätten att använda den evig.

Organisationer kan integrera sin företagsplan [!DNL Adobe Stock] med [!DNL Experience Manager Assets] för att säkerställa att licensierade mediefiler finns tillgängliga i stor omfattning för kreativa projekt och marknadsföringsprojekt, med de kraftfulla resurshanteringsfunktionerna i [!DNL Experience Manager]. [!DNL Experience Manager] -användare kan snabbt hitta, förhandsgranska och licensiera Adobe Stock-resurser som har sparats i  [!DNL Experience Manager]utan att lämna  [!DNL Experience Manager] gränssnittet.

<!-- Old content
## Prerequisites {#prerequisites}

The integration requires an [enterprise [!DNL Adobe Stock] plan](https://stockenterprise.adobe.com/).
-->

## Integrera [!DNL Experience Manager] och [!DNL Adobe Stock] {#integrate-aem-and-adobe-stock}

[!DNL Experience Manager Assets] ger användarna möjlighet att söka, förhandsgranska, spara och licensiera  [!DNL Adobe Stock] resurser direkt från  [!DNL Experience Manager].

**Förutsättningar**

Integreringen kräver:
* En [Enterprise [!DNL Adobe Stock] plan](https://stockenterprise.adobe.com/)
* En användare med behörigheter i Admin Console till standardproduktprofilen för Stock
* En användare med behörighet till Developer Access-profilen för att skapa integrering i Adobe Developer Console

En företagsplan [!DNL Adobe Stock],
* Ger produktberättigande för [!DNL Adobe Stock] (Stocks som är anslutna till Experience Manager)
* Krediter som köpts till [!DNL Adobe Admin Console] för ditt aktieberättigande
* Aktiverar JWT-autentisering (Service Account) inom [!DNL Adobe Developer Console] för ditt Stock-berättigande
* Aktiverar hantering av krediter och licenser globalt inifrån [!DNL Adobe Admin Console]

I berättigandet finns en standardproduktprofil för [!DNL Adobe Stock] i [!DNL Admin Console]. Det går att skapa flera profiler, och de här profilerna avgör vem som kan licensiera Stock-mediefiler. En användare som har direkt åtkomst till produktprofilen har tillgång till [https://stock.adobe.com/](https://stock.adobe.com/) och kan licensiera Stock-mediefiler. Det finns ett annat sätt att använda Developer Access för att skapa integrerings-API:t för att autentisera kommunikationen mellan [!DNL Experience Manager] och [!DNL Adobe Stock].

>[!NOTE]
>
>Verifieringen av Stock-tjänstkontot (JWT) följer med Enterprise Stock-berättigandet.
>
>Integreringen stöder inte Oauth-autentisering för Enterprise Stock-berättigande.

<!-- old content
To allow communication between [!DNL Experience Manager] and [!DNL Adobe Stock], create an IMS configuration and an [!DNL Adobe Stock] configuration in [!DNL Experience Manager].

>[!NOTE]
>
>Only [!DNL Experience Manager] administrators and [!DNL Admin Console] administrators for an organization can perform the integration as it requires administrator privileges.
-->

## Steg för att integrera [!DNL Experience Manager] och [!DNL Adobe Stock] {#integration-steps}

Om du vill integrera [!DNL Experience Manager] och [!DNL Adobe Stock] utför du följande steg i den listade sekvensen:

1. [Hämta ett offentligt certifikat](#public-certificate)

   I [!DNL Experience Manager] skapar du ett IMS-konto och skapar ett offentligt certifikat (offentlig nyckel).

1. [Skapa JWT-anslutning (Service Account)](#createnewintegration)

   Skapa ett projekt för din [!DNL Adobe Stock]-organisation i [!DNL Adobe Developer Console]. Under projektet konfigurerar du ett API med den offentliga nyckeln för att skapa en JWT-anslutning (Service Account). Hämta tjänstkontots autentiseringsuppgifter och information om JWT-nyttolast.

1. [Konfigurera IMS-konto](#create-ims-account-configuration)

   I [!DNL Experience Manager] konfigurerar du IMS-kontot med hjälp av tjänstkontots autentiseringsuppgifter och JWT-nyttolasten.

1. [Konfigurera molntjänsten](#configure-the-cloud-service)

   Konfigurera en [!DNL Adobe Stock]-molntjänst med hjälp av IMS-kontot i [!DNL Experience Manager].


### Skapa en IMS-konfiguration {#create-an-ims-configuration}

IMS-konfigurationen autentiserar din [!DNL Experience Manager Assets]-författarinstans med [!DNL Adobe Stock]-berättigandet.

IMS-konfigurationen har två steg:

* [Hämta ett offentligt certifikat](#public-certificate)
* [Konfigurera IMS-konto](#create-ims-account-configuration)

### Hämta ett offentligt certifikat {#public-certificate}

Den offentliga nyckeln (certifikatet) autentiserar din produktprofil i Adobe Developer Console.

1. Logga in på din [!DNL Experience Manager Assets]-författarinstans. Standardwebbadressen är `http://localhost:4502/aem/start.html`.

1. Navigera till **[!UICONTROL Security]** > **[!UICONTROL Adobe IMS Configurations]** från panelen **[!UICONTROL Tools]**.

1. Klicka på **[!UICONTROL Create]** på sidan Adobe IMS-konfigurationer. Sidan **[!UICONTROL Adobe IMS Technical Account Configuration]** öppnas.

1. På fliken **[!UICONTROL Certificate]** väljer du **[!UICONTROL Adobe Stock]** i listrutan **[!UICONTROL Cloud Solution]**.

1. Du kan skapa ett certifikat eller återanvända ett befintligt certifikat för konfigurationen.

   Om du vill skapa ett certifikat markerar du kryssrutan **[!UICONTROL Create new certificate]** och anger ett **alias** för den offentliga nyckeln. Aliaset används som namn på den offentliga nyckeln.

1. Klicka på **[!UICONTROL Create certificate]**. Klicka sedan på **[!UICONTROL OK]** för att generera den offentliga nyckeln.

1. Klicka på ikonen **[!UICONTROL Download Public Key]** och spara filen med den offentliga nyckeln (.crt) på datorn. Den offentliga nyckeln används senare för att konfigurera API för din Brand Portal-klient och generera autentiseringsuppgifter för tjänstkontot i Adobe Developer Console.

   Klicka på **[!UICONTROL Next]**.

   ![generate-certificate](assets/stock-integration-ims-account.png)

1. På fliken **Konto** skapas ett Adobe IMS-konto som kräver inloggningsuppgifterna för tjänstkontot.

   Öppna en ny flik och [skapa en JWT-anslutning i Adobe Developer Console](#createnewintegration).

### Skapa JWT-anslutning (Service Account) {#createnewintegration}

I Adobe Developer Console konfigureras projekt och API:er på organisationsnivå. När du konfigurerar ett API skapas en JWT-anslutning (Service Account). Det finns två metoder för att konfigurera API, genom att generera ett nyckelpar (privata och offentliga nycklar) eller genom att överföra en offentlig nyckel. I det här exemplet genereras autentiseringsuppgifterna för tjänstkontot genom att den offentliga nyckeln överförs.

Så här genererar du tjänstkontots autentiseringsuppgifter och JWT-nyttolast:

1. Logga in på Adobe Developer Console med systemadministratörsbehörighet. Standardwebbadressen är [https://www.adobe.com/go/devs_console_ui](https://www.adobe.com/go/devs_console_ui).


   Kontrollera att du har valt rätt IMS-organisation (Stock-berättigande) i listrutan (organisation).

1. Klicka på **[!UICONTROL Create new project]**. Ett tomt projekt med ett systemgenererat namn skapas för din organisation.

   Klicka på **[!UICONTROL Edit project]**. Uppdatera **[!UICONTROL Project Title]** och **[!UICONTROL Description]** och klicka sedan på **[!UICONTROL Save]**.

1. Klicka på **[!UICONTROL Add API]** på fliken **[!UICONTROL Project overview]**.

1. Välj **[!UICONTROL Adobe Stock]** i **[!UICONTROL Add an API window]**. Klicka på **[!UICONTROL Next]**.

1. I fönstret **[!UICONTROL Configure API]** väljer du **[!UICONTROL Service Account (JWT)]** autentisering. Klicka på **[!UICONTROL Next]**.

   ![create-jwt-credentials](assets/aem-stock-jwt.png)

1. Klicka på **[!UICONTROL Upload your public key]**. Klicka på **[!UICONTROL Select a File]** och överför den publika nyckeln (.crt-filen) som du har hämtat i [hämta det publika certifikatet](#public-certificate)-avsnittet. Klicka på **[!UICONTROL Next]**.

1. Kontrollera den offentliga nyckeln och klicka på **[!UICONTROL Next]**.

1. Välj standardproduktprofilen för **[!UICONTROL Adobe Stock]** och klicka på **[!UICONTROL Save configured API]**.

1. När API:t har konfigurerats omdirigeras du till API-översiktssidan. Klicka på alternativet **[!UICONTROL Service Account (JWT)]** i den vänstra navigeringen under **[!UICONTROL Credentials]**. Här kan du visa autentiseringsuppgifter och utföra åtgärder som att generera JWT-tokens, kopiera autentiseringsuppgifter och hämta klienthemlighet.

1. Kopiera **[!UICONTROL client ID]** från fliken **[!UICONTROL Client Credentials]**.

   Klicka på **[!UICONTROL Retrieve Client Secret]** och kopiera **[!UICONTROL client secret]**.

   ![generate-jwt-credentials](assets/aem-stock-jwt-credential.png)

1. Navigera till fliken **[!UICONTROL Generate JWT]** och kopiera **[!UICONTROL JWT Payload]**-informationen.

Du kan nu använda klient-ID (API-nyckel), klienthemlighet och JWT-nyttolast till [konfigurera IMS-kontot](#create-ims-account-configuration) i [!DNL Experience Manager Assets].

### Konfigurera IMS-konto {#create-ims-account-configuration}

Du måste ha inloggningsuppgifterna för [certifikatet](#public-certificate) och [tjänstkontot (JWT)](#createnewintegration) för att konfigurera IMS-kontot.

Så här konfigurerar du IMS-kontot:

1. Öppna IMS-konfigurationen och gå till fliken **[!UICONTROL Account]**. Du höll sidan öppen medan [du hämtade det offentliga certifikatet](#public-certificate).

1. Ange en **[!UICONTROL Title]** för IMS-kontot.

   Ange URL-adressen i fältet **[!UICONTROL Authorization Server]**: [https://ims-na1.adobelogin.com/](https://ims-na1.adobelogin.com/).

   Ange klient-ID i fältet **[!UICONTROL API key]**, **[!UICONTROL Client Secret]** och **[!UICONTROL Payload]** (JWT-nyttolast) som du kopierade när du [skapade tjänstkontoanslutningen (JWT)](#createnewintegration).

1. Klicka på **[!UICONTROL Create]**. En IMS-kontokonfiguration skapas.

   ![configure-ims-account](assets/aem-stock-ims-config.png)

1. Välj IMS-kontokonfigurationen och klicka på **[!UICONTROL Check Health]**.

   Klicka på **[!UICONTROL Check]** i dialogrutan. När konfigurationen är klar visas ett meddelande om att *token har hämtats*.

   ![hälsokontroll](assets/aem-stock-healthcheck.png)


### Konfigurera molntjänsten {#configure-the-cloud-service}

Så här konfigurerar du molntjänsten [!DNL Adobe Stock]:

1. I [!DNL Experience Manager]-användargränssnittet går du till **[!UICONTROL Tools]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Adobe Stock]**.

1. Klicka på **[!UICONTROL Create]** på sidan [!DNL Adobe Stock Configurations].

1. Ange en **[!UICONTROL Title]** för molnkonfigurationen.

   Välj den IMS-konfiguration som du skapade när du konfigurerade IMS-kontot](#create-ims-account-configuration).[

   Välj språkinställning i listrutan.

   ![aem-stock-cloud-config](assets/aem-stock-cloud-config.png)

1. Klicka på **[!UICONTROL Save & Close]**.

   Din [!DNL Experience Manager Assets]-författarinstans är nu integrerad med [!DNL Adobe Stock]. Du kan skapa flera [!DNL Adobe Stock]-konfigurationer (till exempel språkbaserade konfigurationer). Du kan nu komma åt, söka efter och licensiera [!DNL Adobe Stock]-resurserna inifrån [!DNL Experience Manager]-användargränssnittet.

   ![search-stock-assets](assets/aem-stock-searchstocks.png)

   >[!NOTE]
   >
   >I det här skedet av integreringen kan bara administratörer komma åt [!DNL Adobe Stock]-resurserna, söka efter Stock-resurser (med omnissearch) och licensiera [!DNL Adobe Stock]-resurserna.
   >
   >Administratörer kan lägga till användare eller grupper ytterligare i molntjänsten [!DNL Adobe Stock] och ge dessa icke-adminanvändare i [!DNL Experience Manager] behörighet att komma åt Stock-konfigurationen.

1. Om du vill lägga till användare eller grupper väljer du molnkonfigurationen [!DNL Adobe Stock] och klickar på **[!UICONTROL Properties]**.

1. Sök för att lägga till de användare eller grupper som du har tilldelat behörighet att komma åt Adobe Stock-konfigurationen. Se [tilldela behörigheter till användargruppen](#assign-permissions-to-group).


## Tilldela behörigheter till användargruppen {#assign-permissions-to-group}

Administratörer kan skapa användargrupper och ge behörigheter till vissa användare eller grupper för åtkomst till molntjänsten [!DNL Adobe Stock].

Följande behörigheter krävs för att en användare ska kunna söka efter och licensiera Adobe Stock-resurser:

* Konfigurera sökvägen: `/conf/global/settings/stock`
* Behörigheter: `jcr:read`
* Behörighetstyp: `Allow`

Du kan skapa en användargrupp eller tilldela behörigheter till en befintlig användargrupp. Behörigheter kan tilldelas från gränssnittet [!DNL Experience Manager Assets] eller från konsolen [!DNL User Admin].

**Så här ger du åtkomst till en användargrupp från  [!DNL Experience Manager]:**

1. I [!DNL Experience Manager]-användargränssnittet går du till **[!UICONTROL Tools]** > **[!UICONTROL Security]** > **[!UICONTROL Groups]**. Skapa en användargrupp för [!DNL Adobe Stock].

1. Navigera till **[!UICONTROL Tools]** > **[!UICONTROL Security]** > **[!UICONTROL Permissions]**.

1. Sök efter användargruppen i den vänstra panelen och lägg till nya **[!UICONTROL Access Control Entry (ACE)]** för Adobe Stock.

   * Konfigurera sökvägen: `/conf/global/settings/stock`
   * Behörigheter: `jcr:read`
   * Behörighetstyp: `Allow`

   Klicka på **[!UICONTROL Add]**.

   ![användarbehörigheter](assets/aem-stock-user-permissions.png)

1. Navigera till **[!UICONTROL Tools]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Adobe Stock]**. Välj molnkonfigurationen [!DNL Adobe Stock] och klicka på **[!UICONTROL Properties]**.

1. Lägg till den nya användargruppen i [!DNL Adobe Stock]-konfigurationen. Klicka på **[!UICONTROL Save & Close]**.

   ![assign-user](assets/aem-stock-adduser.png)

**Så här ger du åtkomst till en användare från  [!DNL User Admin Console]:**

1. Öppna Admin Console [!DNL Experience Manager]. Standardwebbadressen är `http://localhost:4502/userdamin`.

1. I den vänstra panelen söker du efter användaren genom att ange `user_id` eller `name`. Dubbelklicka för att öppna användaregenskaperna.

1. Navigera till fliken **[!UICONTROL Permissions]** och tillåt `read`-behörigheter för molnkonfigurationen [!DNL Adobe Stock]: `/conf/global/settings/stock`.

   >[!CAUTION]
   >
   >Om molnkonfigurationen inte tillåts kan användaren bara komma åt **[!UICONTROL Assets]** i gränssnittet [!DNL Experience Manager].
   >
   >Om du vill tillåta åtkomst till [!UICONTROL Assets] och [!DNL Adobe Stock]-resurser kontrollerar du att molnkonfigurationen tillåts för användaren.

1. Klicka på **[!UICONTROL Save]** för att uppdatera behörigheterna.

   ![assign-user-in-user-admin](assets/aem-stock-user-admin-console.png)

1. Lägg till användaren eller gruppen i molnkonfigurationen [!DNL Adobe Stock].


## Få tillgång till Adobe Stock-resurser {#access-stock-assets}

En användare som inte är administratör och som har behörighet till molnkonfigurationen [!DNL Adobe Stock] kan söka efter och licensiera [!DNL Adobe Stock]-resurserna från gränssnittet [!DNL Experience Manager].

Användaren måste utföra ett extra steg för att aktivera molnkonfigurationen [!DNL Adobe Stock] innan [!DNL Adobe Stock]-resurserna kan nås. Det är en engångsaktivitet. Om användaren har tilldelats behörigheter för flera [!DNL Adobe Stock]-molnkonfigurationer kan användaren välja önskad konfiguration från **[!UICONTROL User Preferences]**.

Så här aktiverar du molnkonfigurationen [!DNL Adobe Stock]:

1. Logga in på [!DNL Experience Manager].

1. Klicka på användarikonen i det övre högra hörnet och klicka sedan på **[!UICONTROL My Preferences]**. Fönstret **[!UICONTROL User Preferences]** öppnas.

1. Välj **[!UICONTROL Stock Configuration]** i listrutan och klicka på **[!UICONTROL Accept]** för att aktivera konfigurationen.

   ![användarinställningar](assets/aem-stock-preferences.png)

1. Navigera till **[!UICONTROL Assets]** > **[!UICONTROL Adobe Stock]**. Nu kan du visa, söka efter och licensiera [!DNL Adobe Stock] resurser.

I följande tabell beskrivs hur användarbehörigheterna fungerar när du använder [!DNL Adobe Stock]-resurserna:

| Användare | Grupp | Behörigheter | Acceptera Stock-konfigurationen i användarinställningarna | Åtkomst till resurser | Använd Adobe Stock |
| --- | --- | --- | --- | --- | --- |
| admin | Ej tillämpligt | Alla | Ej tillämpligt | Ja | Ja |
| test-doc1 | DAM-användare | `/conf/global/settings/stock/cloud-config` | Ja | Ja | Ja |
| test-doc1 | DAM-användare | `/conf/global/settings/stock/cloud-config` | Nej | Fel: Det gick inte att läsa in data | Nej |
| test-doc1 | DAM-användare | tillåt: `/conf/global/settings/stock` neka: `/cloud-config` | Lagerkonfigurationen visas inte | Ja | Nej |


## Använd och hantera [!DNL Adobe Stock]-resurser i [!DNL Experience Manager] {#usemanage}

Med den här funktionen kan organisationer tillåta användare att arbeta med [!DNL Adobe Stock]-resurser i [!DNL Experience Manager Assets]. I [!DNL Experience Manager]-användargränssnittet kan användare söka efter [!DNL Adobe Stock]-resurser och licensiera de nödvändiga resurserna.

När en [!DNL Adobe Stock]-resurs har licensierats i [!DNL Experience Manager] kan den användas och hanteras som en vanlig resurs. I [!DNL Experience Manager] kan användarna söka efter och förhandsgranska resurserna; kopiera och publicera tillgångarna, dela resurserna på [!DNL Brand Portal], få tillgång till och använda resurserna via [!DNL Experience Manager]-datorprogrammet; och så vidare.

![Söka efter  [!DNL Adobe Stock] resurser och filtrera resultat från  [!DNL Adobe Experience Manager] arbetsytan](assets/adobe-stock-search-results-workspace.png)

**A.**[!DNL Adobe Stock] Sök efter resurser som liknar de resurser vars ID har angetts. **B.** Sök efter resurser som matchar ditt val av form eller orientering. **C.** Sök efter en eller flera resurstyper som stöds  **D.** Öppna eller dölj filtret  **E.** Licensiera och spara den markerade resursen i  [!DNL Experience Manager] **F.** Spara resursen i  [!DNL Experience Manager] med vattenstämpel  **G.**   [!DNL Adobe Stock]   ****   [!DNL Adobe Stock]   ****   **** Utforska resurser på webbplatsen som liknar den markerade resursen¥H.SökAntal markerade resurser från den markerade resursen. resultatetJ.Växla mellan kortvyn och listvyn

### Hitta resurser {#find-assets}

Dina [!DNL Experience Manager]-användare kan söka efter resurser i både, [!DNL Experience Manager] och [!DNL Adobe Stock]. När sökplatsen inte är begränsad till [!DNL Adobe Stock] visas sökresultaten från [!DNL Experience Manager] och [!DNL Adobe Stock].

* Om du vill söka efter [!DNL Adobe Stock] resurser klickar du på **[!UICONTROL Navigation]** > **[!UICONTROL Assets]** > **[!UICONTROL Search Adobe Stock]**.

* Om du vill söka efter resurser i [!DNL Adobe Stock] och [!DNL Experience Manager Assets] klickar du på sök ![sök](assets/do-not-localize/search_icon.png).

Du kan också börja skriva `Location: Adobe Stock` i sökfältet för att välja [!DNL Adobe Stock]-resurser. [!DNL Experience Manager] har avancerade filtreringsfunktioner för de sökbara resurserna, vilket gör att användarna snabbt kan nollställa de resurser som behövs med hjälp av filter, som typer av resurser som stöds, bildorientering och licensierat läge.

>[!NOTE]
>
>Resurser som söks igenom från [!DNL Adobe Stock] visas i [!DNL Experience Manager]. [!DNL Adobe Stock] resurser hämtas och lagras i  [!DNL Experience Manager] databasen först när en användare antingen  [sparar en ](/help/assets/aem-assets-adobe-stock.md#saveassets) resurslicens  [och sparar en resurs](/help/assets/aem-assets-adobe-stock.md#licenseassets). Resurser som redan är lagrade i [!DNL Experience Manager] visas och markeras för att underlätta referens och åtkomst. Dessutom sparas [!DNL Stock]-resurserna med ytterligare metadata för att ange källan som [!DNL Stock].

![Söka efter filter i  [!DNL Experience Manager] och markerade  [!DNL Adobe Stock] resurser i sökresultat](assets/aem-search-filters2.jpg)

### Spara och visa nödvändiga resurser {#saveassets}

Välj en resurs som du vill spara i [!DNL Experience Manager]. Klicka på [!UICONTROL Save] i verktygsfältet överst och ange resursens namn och plats. De olicensierade resurserna sparas lokalt med en vattenstämpel.

Nästa gång du söker efter resurser markeras de sparade resurserna med ett märke som anger att sådana resurser är tillgängliga i [!DNL Experience Manager Assets].

>[!NOTE]
>
>De nyligen tillagda resurserna visas med märket Nytt i stället för Licensierad.

### Licensiera resurser {#licenseassets}

Användare kan licensiera [!DNL Adobe Stock]-resurser genom att använda kvoten för deras [!DNL Adobe Stock] Enterprise-plan. När du licensierar en resurs sparas den utan vattenstämpel och är tillgänglig för sökning och användning i [!DNL Experience Manager Assets].

![Dialogruta där du kan licensiera och spara  [!DNL Adobe Stock] resurser  [!DNL Experience Manager Assets]](assets/aem-stock_licenseandsave.jpg)


### Få åtkomst till metadata och resursegenskaper {#access-metadata-and-asset-properties}

Användarna kan komma åt och förhandsgranska metadata, inklusive metadataegenskaperna [!DNL Adobe Stock] för resurserna som sparats i [!DNL Experience Manager], och lägga till **[!UICONTROL License References]** för en resurs. Uppdateringarna av licensreferensen synkroniseras dock inte mellan [!DNL Experience Manager]- och [!DNL Adobe Stock]-webbplatsen.

Användarna kan se egenskaperna för både, licensierade och olicensierade resurser.

![Visa och få tillgång till metadata och licensreferenser för sparade resurser](assets/metadata_properties.jpg)


## Kända begränsningar {#known-limitations}

* **Problem vid integrering med  [!DNL Experience Manager] Service Pack 6.5.7.0 och senare**: Ett oväntat fel upptäcktes under integreringen med  [!DNL Experience Manager] 6.5.7.0 och senare. Problemet testas och förväntas vara tillgängligt i [!DNL Experience Manager] 6.5.11.0. Kontakta [!DNL Customer Support] för en snabbkorrigering.

* **Funktioner som begränsar användare från licenser fungerar inte korrekt**: Alla användare som har  `read` behörighet till Stock-konfigurationen får söka efter och licensiera  [!DNL Adobe Stock] resurserna.

* **Användare som inte är administratörer måste manuellt aktivera  [!DNL Adobe Stock] molnkonfigurationen**: I  **[!UICONTROL User Preferences]** fönstret  **[!UICONTROL Stock Configuration]** visas  [!DNL Adobe Stock] molnkonfigurationen som aktiverad, men den fungerar inte för användare som inte är administratörer. Användaren måste klicka på **[!UICONTROL Accept]**-knappen för att aktivera Stock-konfigurationen. Om du inte utför det här steget visas ett felmeddelande när du försöker komma åt **[!UICONTROL Assets]**.

* **Varning om redigeringsbild visas** inte: När du licensierar en bild kan du inte kontrollera om en bild endast är för redaktionellt bruk. För att förhindra eventuell felaktig användning kan administratören stänga av åtkomsten till redaktionella mediefiler från Admin Console.

* **Fel licenstyp visas**: Det är möjligt att en felaktig licenstyp visas i  [!DNL Experience Manager] för en resurs. Användarna kan logga in på [!DNL Adobe Stock]-webbplatsen för att se licenstypen.

* **Referensfält och metadata synkroniseras** inte: När en användare uppdaterar ett licensreferensfält uppdateras licensreferensinformationen i  [!DNL Experience Manager] men inte på  [!DNL Adobe Stock] webbplatsen. Om användaren uppdaterar referensfälten på webbplatsen [!DNL Adobe Stock] synkroniseras inte uppdateringarna i [!DNL Experience Manager].

>[!MORELIKETHIS]
>
>* [Videosjälvstudiekurs om hur du  [!DNL Adobe Stock] använder resurser med [!DNL Experience Manager Assets]](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/creative-workflows/adobe-stock.html)
>* [[!DNL Adobe Stock] hjälp med Enterprise Plan](https://helpx.adobe.com/enterprise/using/adobe-stock-enterprise.html)
>* [[!DNL Adobe Stock] Vanliga frågor](https://helpx.adobe.com/stock/faq.html)



<!--old content

### Create an IMS configuration {#create-an-ims-configuration}

1. In the [!DNL Experience Manager] user interface, navigate to **[!UICONTROL Tools]** > **[!UICONTROL Security]** > **[!UICONTROL Adobe IMS Configurations]**. Click **[!UICONTROL Create]** and select **[!UICONTROL Cloud Solution]** > **[!UICONTROL Adobe Stock]**.
1. Either reuse an existing certificate or select **[!UICONTROL Create new certificate]**.
1. Click **[!UICONTROL Create certificate]**. Once created, download the public key. Click **[!UICONTROL Next]**. Leave the [!UICONTROL Adobe IMS Technical Account Configuration] screen open to provide the required values shortly.
1. Access [Adobe Developer Console](https://console.adobe.io). Ensure that your account has administrator permissions for the organization for which the integration is required.
1. Click **[!UICONTROL Create new project]** and click **[!UICONTROL Add API]**. Select **[!UICONTROL Adobe Stock]** from the list of APIs that are available to you. Select [!UICONTROL OAUTH 2.0 Web].
1. Provide **[!UICONTROL Default redirect URI]** and **[!UICONTROL Redirect URI pattern]** values. Click **[!UICONTROL Save configured API]**. Copy the generated ID and secret.
1. In [!UICONTROL Adobe IMS Technical Account Configuration] screen, provide the values in the boxes titled **[!UICONTROL Title]**, **[!UICONTROL Authorization Server]**, **[!UICONTROL API Key]**, **[!UICONTROL Client Secret]**, and **[!UICONTROL Payload]**. For detailed information about these values, see [JWT authentication quick start](https://www.adobe.io/authentication/auth-methods.html#!AdobeDocs/adobeio-auth/master/JWT/JWT.md).

-->

<!-- TBD: Update the URL to update the terminology when AIO team updates their documentation URL. Logged issue github.com/AdobeDocs/adobeio-auth/issues/63.
-->

<!--
### Create [!DNL Adobe Stock] configuration in [!DNL Experience Manager] {#create-adobe-stock-configuration-in-aem}

1. In the [!DNL Experience Manager], navigate to **[!UICONTROL Tools]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Adobe Stock]**.
1. Click **[!UICONTROL Create]** to create a configuration and associate it with your existing IMS Configuration. Select `PROD` as the environment parameter.
1. In **[!UICONTROL Licensed Assets Path]** field, leave a location as is. Do not change the location where you want to store the [!DNL Adobe Stock] assets.
1. Complete creation by adding all the required properties. Click **[!UICONTROL Save & Close]**.
1. Add [!DNL Experience Manager] users or groups, who can license the assets.

>[!NOTE]
>
>If there are multiple [!DNL Adobe Stock] configurations, select the desired configuration in [!UICONTROL User Preferences] panel. To access the panel from [!DNL Experience Manager] home page, click the user icon and then click **[!UICONTROL User Preferences]** > **[!UICONTROL Stock Configuration]**.

-->