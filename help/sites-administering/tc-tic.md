---
title: Konfigurera översättningsintegreringsramverket
seo-title: Konfigurera översättningsintegreringsramverket
description: Lär dig hur du konfigurerar TLF (Translation Integration Framework).
seo-description: Lär dig hur du konfigurerar TLF (Translation Integration Framework).
uuid: 5ecfe154-732f-4a13-96f8-92f55023c54d
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features
content-type: reference
discoiquuid: 200f51ab-f9bf-4989-91af-c3904fc673e5
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Konfigurera översättningsintegreringsramverket{#configuring-the-translation-integration-framework}

Översättningsintegreringsramverket integreras med översättningstjänster från tredje part för att samordna översättningen av AEM-innehåll.

* Anslut till översättningstjänsten.
* Skapa en konfiguration för Translation Integration Framework.
* Associera molnkonfigurationerna med sidorna.

En översikt över funktionerna för innehållsöversättning i AEM finns i [Översätta innehåll för flerspråkiga webbplatser](/help/sites-administering/translation.md).

## Ansluta till en översättningstjänstleverantör {#connecting-to-a-translation-service-provider}

Skapa en molnkonfiguration som ansluter AEM till din översättningstjänstleverantör. AEM har funktioner för att ansluta till Microsoft Translator som standard. För andra översättningsleverantörer hämtar du kopplingspaketet från [paketresurs](/help/sites-administering/package-manager.md#package-share).
Följande översättningsleverantörer tillhandahåller en implementering av det nya API:t för översättningsprojekten. Länkar för mer information om integrering och hur du hämtar från paketresurs:

* [Lera Tablet Technologies](https://marketing.adobe.com/resources/content/resources/en/exchange/marketplace/apps/clay-tablet-translation-connector-for-aem.html) (not on PackageShare, contact vendor directly)
* [Lionbridge](https://marketing.adobe.com/resources/content/resources/en/exchange/marketplace/apps/lionbridge-for-adobe-experience-manager.html)
* [Molnord](https://marketing.adobe.com/resources/content/resources/en/exchange/marketplace/apps/cloudwords-for-adobe-translations-connector.html)
* [CrossLang NV](https://marketing.adobe.com/resources/content/resources/en/exchange/marketplace/apps/crosslang-xtm-for-adobe-experience-manager.html)
* [Lingotek](https://marketing.adobe.com/resources/content/resources/en/exchange/marketplace/apps/lingotek-for-adobe-experience-manager.html)
* Microsoft (Microsoft Translator är förinstallerat i AEM)
* [Smartling](https://marketing.adobe.com/resources/content/resources/en/exchange/marketplace/apps/smartling-connector-for-adobe-experience-manager.html)
* [Translations.com](https://marketing.adobe.com/resources/content/resources/en/exchange/marketplace/apps/globallink-connect-for-adobe-experience-manager.html)
* [SDL WorldServer](https://marketing.adobe.com/resources/content/resources/en/exchange/marketplace/apps/sdlworldserver-connector.html)
* [SDL TMS](https://marketing.adobe.com/resources/content/resources/en/exchange/marketplace/apps/sdl-tms-translation-connector-for-adobe-experience-manager.html)
* [Systran](https://marketing.adobe.com/resources/content/resources/en/exchange/marketplace/apps/systran-for-adobe-experience-manager.html)
* [Altlang](https://marketing.adobe.com/resources/content/resources/en/exchange/marketplace/apps/Altlang.html)

>[!NOTE]
>
>Här hittar du en lista över de senaste leverantörerna av personal- och maskinöversättning:
>
>
>* [AEM Human Translation](https://www.adobe.com/go/aem-human-translation-connectors)
>* [AEM Machine Translation](https://www.adobe.com/go/aem-machine-translation-connectors)
>



När du har installerat ett anslutningspaket kan du skapa en molnkonfiguration för anslutaren. Vanligtvis måste du ange dina autentiseringsuppgifter för autentisering med översättningstjänsten. Mer information om hur du lägger till en molnkonfiguration för Microsoft Translator-anslutningen finns i [Integrera med Microsoft Translator](/help/sites-administering/tc-msconf.md).

Du kan skapa flera molnkonfigurationer för samma anslutning om det behövs. Skapa till exempel en konfiguration för varje konto eller projekt som du har med samma leverantör.

När du har konfigurerat en anslutning kan du skapa den konfiguration av översättningsintegreringsramverket som använder den.

## Skapa en konfiguration för översättningsintegrering {#creating-a-translation-integration-configuration}

Skapa en konfiguration för ramverk för översättningsintegrering som anger hur ditt innehåll ska översättas. Konfigurationen innehåller följande information:

* Vilken översättningstjänstleverantör som ska användas.
* Anger om översättning till människa eller dator ska utföras.
* Om annat innehåll som är associerat med en sida eller resurs ska översättas, till exempel taggar.

När du har skapat en ramverkskonfiguration associerar du molnkonfigurationen med de sidor som du vill översätta enligt konfigurationen. När översättningsprocessen startas fortsätter översättningsarbetsflödet enligt den associerade ramverkskonfigurationen.

Om olika delar av webbplatsen har olika översättningskrav skapar du flera ramverkskonfigurationer utifrån detta. En flerspråkig webbplats innehåller t.ex. engelska, spanska och japanska språkkopior. Webbplatsägaren använder två olika översättningstjänstleverantörer för spanska och japanska översättningar. Därför är två konfigurationer av ramverket konfigurerade. Varje konfiguration använder en annan översättningstjänstleverantör.

När du har konfigurerat ett ramverk för översättningsintegrering kan du [koppla det till sidorna](/help/sites-administering/tc-prep.md) som använder det.

**** Obs!En översikt över funktionerna för innehållsöversättning i AEM finns i [Översätta innehåll för flerspråkiga webbplatser](/help/sites-administering/translation.md).

En enda konfiguration av ramverket styr hur sidinnehåll, communityinnehåll och resurser ska översättas.
![chlimage_1-386](assets/chlimage_1-386.png)

### Egenskaper för platskonfiguration {#sites-configuration-properties}

Webbplatsegenskaperna styr hur översättning av sidinnehåll utförs.

<table>
 <tbody>
  <tr>
   <th>Egenskap</th>
   <th>Beskrivning</th>
  </tr>
  <tr>
   <td>Översättningsarbetsflöde</td>
   <td><p>Välj den översättningsmetod som ramverket utför för webbplatsinnehåll:</p>
    <ul>
     <li>Maskinöversättning: Översättningsprovidern utför översättningen med maskinöversättning i realtid.</li>
     <li>Translation of Human: Innehållet skickas till översättningsleverantören för översättning av översättare. </li>
     <li>Översätt inte: Innehåll skickas inte för översättning. Detta är för att hoppa över vissa innehållsgrenar som inte skulle översättas, men som skulle kunna uppdateras med det senaste innehållet.</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Översättningsprovider</td>
   <td>Välj översättningsprovidern som ska utföra översättningen. En provider visas i listan när motsvarande koppling är installerad.</td>
  </tr>
  <tr>
   <td>Innehållskategori</td>
   <td>(Endast maskinöversättning) En kategori som beskriver innehållet som du översätter. Kategorin kan påverka valet av terminologi och fraser när innehåll översätts.</td>
  </tr>
  <tr>
   <td>Översätt taggar</td>
   <td>Välj att översätta taggar som är kopplade till sidan.</td>
  </tr>
  <tr>
   <td>Översätt sidresurser</td>
   <td><p>Välj hur resurser som har lagts till i komponenter från filsystemet eller refererats från Assets ska översättas:</p>
    <ul>
     <li>Översätt inte: Sidresurser översätts inte.</li>
     <li>Använda arbetsflöde för översättning av platser: Resurser hanteras enligt konfigurationsegenskaperna på fliken Platser.</li>
     <li>Använda arbetsflöde för resursöversättning: Resurser hanteras enligt egenskapskonfigurationen på fliken Resurser.</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Automatisk översättning</td>
   <td>Välj det här alternativet om du vill köra översättningsjobb automatiskt efter att översättningsprojekt har skapats. Du har inte möjlighet att granska och omsluta översättningsjobbet när du väljer det här alternativet.</td>
  </tr>
 </tbody>
</table>

### Egenskaper för webbkonfiguration {#communities-configuration-properties}

Communities-egenskaper styr hur översättning av användargenererat innehåll utförs. Översättningen av användargenererat innehåll använder alltid maskinöversättning. Mer information finns i [Översätta användargenererat innehåll](/help/communities/translate-ugc.md).

| Egenskap | Beskrivning |
|---|---|
| Översättningsprovider | Välj översättningsprovidern som ska utföra översättningen. Providern som molnkonfigurationer skapas för visas i listan. |
| Innehållskategori | En kategori som beskriver innehållet som du översätter. Kategorin kan påverka valet av terminologi och fraser när innehåll översätts. |
| Välj en språkinställning som ska användas som globalt resurslager |  (Valfritt) Genom att välja en språkinställning för lagring av UGC, visas inlägg från alla språkkopior i en global konversation. Välj språkinställning som [basspråk](/help/communities/sites-console.md#translation) för webbplatsen. Om du väljer Ingen gemensam lagringsplats inaktiveras global översättning. Som standard är global översättning inaktiverat. |

### Egenskaper för resurskonfiguration {#assets-configuration-properties}

Resursegenskaperna styr hur resurser konfigureras. Mer information om översättning av resurser finns i [Skapa språkkopior för resurser](/help/assets/translation-projects.md).

<table>
 <tbody>
  <tr>
   <th>Egenskap</th>
   <th>Beskrivning</th>
  </tr>
  <tr>
   <td>Översättningsarbetsflöde</td>
   <td><p>Välj den typ av översättning som ramverket utför för resurser:</p>
    <ul>
     <li>Maskinöversättning: Översättningsprovidern utför översättningen omedelbart med maskinöversättning.</li>
     <li>Translation of Human: Innehållet skickas automatiskt till översättningsleverantören för manuell översättning. </li>
     <li>Översätt inte: Resurser skickas inte för översättning.</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Översättningsprovider</td>
   <td>Välj översättningsprovidern som ska utföra översättningen. En provider visas i listan när motsvarande koppling är installerad.</td>
  </tr>
  <tr>
   <td>Innehållskategori</td>
   <td>(Endast maskinöversättning) En kategori som beskriver innehållet som du översätter. Kategorin kan påverka valet av terminologi och fraser när innehåll översätts.</td>
  </tr>
  <tr>
   <td>Översätt resurser</td>
   <td>Välj om du vill inkludera resurser i översättningsprojektet. </td>
  </tr>
  <tr>
   <td>Översätt metadata</td>
   <td>Välj att översätta metadata för resursen.</td>
  </tr>
  <tr>
   <td>Översätt taggar</td>
   <td>Välj att översätta taggar som är kopplade till resursen.</td>
  </tr>
  <tr>
   <td>Automatisk översättning</td>
   <td>Välj det här alternativet om du vill köra översättningsjobb automatiskt efter att översättningsprojekt har skapats. Du har inte möjlighet att granska eller omsluta översättningsjobbet när du väljer det här alternativet.</td>
  </tr>
 </tbody>
</table>

1. Klicka eller tryck på Verktyg > Åtgärder > Moln > Molntjänster i sidofältet.
1. I området Översättningsintegrering avgör om några konfigurationer har skapats vilken länk som visas:

   * Om inga konfigurationer har skapats klickar du på eller trycker på Konfigurera nu.
   * Om det redan finns konfigurationer klickar eller trycker du på Visa konfigurationer och sedan på länken + som visas bredvid Tillgängliga konfigurationer.

1. Ange ett namn för konfigurationen och klicka eller tryck sedan på Skapa.
1. Konfigurera egenskaperna på fliken Platser, Communities och Assets och klicka sedan på OK.

## Konfigurera sidor för översättning {#configuring-pages-for-translation}

Om du vill konfigurera översättning av källsidor till andra språk associerar du sidorna med följande molnkonfigurationer:

* Den molnkonfiguration som ansluter AEM till översättningsleverantören.
* Översättningsintegrationsramverket som konfigurerar informationen för översättningen.

Observera att molnkonfigurationen för översättningsintegreringsramverket identifierar den molnkonfiguration som ska användas för att ansluta till tjänstleverantören. När du associerar en källsida med en ramverkets molnkonfiguration måste sidan associeras med tjänstleverantörens molnkonfiguration som används i ramverkets molnkonfiguration.

När du associerar en sida med en molnkonfiguration ärver de underordnade sidorna kopplingen. Om du till exempel associerar sidan /content/geometrixx/en/products med ett Translation Integration Framework, översätts sidan Produkter och alla sidor under den enligt ramverket.

Vid behov kan du åsidosätta associationen på en underordnad sida. Innehållet på en webbplats handlar till exempel mest om kläder. En av sidorna beskriver dock företaget. Webbplatsens rotsida är associerad med ett Translation Integration Framework som anger maskinöversättning med kategorin Clothing. Den gren som beskriver företaget använder ett ramverk som utför maskinöversättning med kategorin Allmänt.

Dessutom, för alla communitykomponenter [för](/help/communities/scf.md) SCF på sidorna, kommer det användargenererade innehållet (UGC) att innehålla möjligheten för användare att översätta innehåll. Mer information finns i [Översättning av användargenererat innehåll](/help/communities/translate-ugc.md).

### Koppla en sida till en översättningsleverantör {#associating-a-page-with-a-translation-provider}

Koppla en sida till översättningsleverantören som du använder för att översätta sidan och underordnade sidor.

1. På webbplatskonsolen markerar du sidan som du vill konfigurera och klickar eller trycker på Visa egenskaper.
1. Klicka eller tryck på Redigera och sedan på eller klicka på fliken Molntjänster.
1. Klicka eller tryck på Add Configuration (Lägg till konfiguration) > Translation Integration (Översättningsintegrering).
1. Välj den översättningsleverantör som ska användas och klicka eller tryck sedan på Klar.

### Associera sidor med ett översättningsintegreringsramverk {#associating-pages-with-a-translation-integration-framework}

Koppla en sida till översättningsintegreringsramverket som definierar hur du vill översätta sidan och underordnade sidor.

1. På webbplatskonsolen markerar du sidan som du vill konfigurera och klickar eller trycker på Visa egenskaper.
1. Klicka eller tryck på Redigera och sedan på eller klicka på fliken Molntjänster.
1. Klicka eller tryck på Add Configuration (Lägg till konfiguration) > Translation Integration (Översättningsintegrering).
1. Markera det översättningsintegreringsramverk som ska användas och klicka eller tryck sedan på Klar.

