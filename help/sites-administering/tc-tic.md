---
title: Konfigurera översättningsintegreringsramverket
description: Lär dig hur du konfigurerar översättningsintegreringsramverket i Adobe Experience Manager.
contentOwner: Guillaume Carlino
feature: Language Copy
exl-id: 7562754b-d9fd-441b-8ae5-c7eebe458cef
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: b7082aaee83fba88b47447b8553563264eedb713
workflow-type: tm+mt
source-wordcount: '1493'
ht-degree: 0%

---

# Konfigurera översättningsintegreringsramverket{#configuring-the-translation-integration-framework}

Översättningsintegreringsramverket integreras med översättningstjänster från tredje part för att samordna översättningen av AEM.

* Anslut till översättningstjänsten.
* Skapa en konfiguration för Translation Integration Framework.
* Associera molnkonfigurationerna med sidorna.

En översikt över funktionerna för översättning av innehåll i AEM finns i [Översätta innehåll för flerspråkiga platser](/help/sites-administering/translation.md).

## Ansluta till en översättningstjänstleverantör {#connecting-to-a-translation-service-provider}

Skapa en molnkonfiguration som ansluter AEM till översättningstjänstleverantören. AEM kan ansluta till Microsoft Translator som standard.
Följande översättningsleverantörer tillhandahåller en implementering av det nya API:t för översättningsprojekten. Länkar för mer information om integrationen:

* [Translations.com](https://exchange.adobe.com/experiencecloud.details.90104.globallink-connect-plus-for-aem.html)
* [Lera surfplattetekniker](https://exchange.adobe.com/experiencecloud.details.90064.clay-tablet-translation-for-experience-manager.html)
* [Lionbridge](https://exchange.adobe.com/experiencecloud.details.100064.lionbridge-connector-for-experience-manager-63.html)
* [Memsource](https://exchange.adobe.com/experiencecloud.details.103166.memsource-connector-for-adobe-experience-manager.html)
* [Molnord](https://exchange.adobe.com/experiencecloud.details.90019.html)
* [XTM Cloud](https://exchange.adobe.com/experiencecloud.details.105037.xtm-connect-for-adobe-experience-manager.html)
* [Lingotek](https://exchange.adobe.com/experiencecloud.details.90088.lingotek-collaborative-translation-platform.html)
* [RWS](https://exchange.adobe.com/apps/ec/108277/rws-language-cloud)
* [Smartling](https://www.smartling.com/software/integrations/adobe-experience-manager/)
* [Systran](https://exchange.adobe.com/experiencecloud.details.90233.systran-for-adobe-experience-manager.html)
* [Altlang](https://exchange.adobe.com/experiencecloud.details.90222.altlang.html)
* Microsoft (Microsoft Translator är förinstallerat i AEM)

>[!NOTE]
>
>Här hittar du en lista över de senaste leverantörerna av personal- och maskinöversättning:
>
>
>* [AEM mänsklig översättning](https://www.adobe.com/go/aem-human-translation-connectors)
>* [AEM maskinöversättning](https://www.adobe.com/go/aem-machine-translation-connectors)
>

När du har installerat ett kopplingspaket kan du skapa en molnkonfiguration för anslutningen. Vanligtvis måste du ange dina autentiseringsuppgifter för autentisering med översättningstjänsten. Mer information om hur du lägger till en molnkonfiguration för Microsoft Translator-anslutningen finns i [Integrera med Microsoft Translator](/help/sites-administering/tc-msconf.md).

Du kan skapa flera molnkonfigurationer för samma anslutning om det behövs. Skapa till exempel en konfiguration för varje konto eller projekt som du har med samma leverantör.

När du har konfigurerat en anslutning kan du skapa den konfiguration av översättningsintegreringsramverket som använder den.

## Skapa en konfiguration för översättningsintegrering {#creating-a-translation-integration-configuration}

Skapa en konfiguration för ramverk för översättningsintegrering som anger hur ditt innehåll ska översättas. Konfigurationen innehåller följande information:

* Vilken översättningstjänstleverantör som ska användas.
* Anger om översättning till människa eller dator ska utföras.
* Om annat innehåll som är associerat med en sida eller resurs ska översättas, till exempel taggar.

När du har skapat en ramverkskonfiguration associerar du molnkonfigurationen med de sidor som du vill översätta enligt konfigurationen. När översättningsprocessen startas fortsätter översättningsarbetsflödet enligt den associerade ramverkskonfigurationen.

Om olika delar av webbplatsen har olika översättningskrav skapar du flera ramverkskonfigurationer utifrån detta. En flerspråkig webbplats innehåller t.ex. engelska, spanska och japanska språkkopior. Webbplatsägaren använder två olika översättningstjänstleverantörer för spanska och japanska översättningar. Därför är två konfigurationer av ramverket konfigurerade. Varje konfiguration använder en annan översättningstjänstleverantör.

När du har konfigurerat ett ramverk för översättningsintegrering kan du [associera det med sidorna](/help/sites-administering/tc-prep.md) som använder det.

**Obs!** En översikt över funktionerna för innehållsöversättning i AEM finns i [Översätta innehåll för flerspråkiga platser](/help/sites-administering/translation.md).

En enda konfiguration av ramverket styr hur sidinnehåll, communityinnehåll och resurser ska översättas.
![chlimage_1-386](assets/translation-config-65.jpg)

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
     <li>Human Translation: Content is sent to the translation provider to be translators. </li>
     <li>Översätt inte: Innehållet skickas inte för översättning. Detta är för att hoppa över vissa innehållsgrenar som inte skulle översättas, men som skulle kunna uppdateras med det senaste innehållet.</li>
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
   <td>Översätt komponentsträngar</td>
   <td>Välj det här alternativet om du vill översätta komponentsträngar för komponenter som är kopplade till sidan.</td>
  </tr>
  <tr>
   <td>Översätt taggar</td>
   <td>Välj att översätta taggar som är kopplade till sidan.</td>
  </tr>
  <tr>
   <td>Översätt sida Assets</td>
   <td><p>Välj hur du vill översätta resurser som har lagts till i komponenter från filsystemet eller som refereras från Assets:</p>
    <ul>
     <li>Översätt inte: Sidresurser översätts inte.</li>
     <li>Använda arbetsflöde för översättning av platser: Assets hanteras enligt konfigurationsegenskaperna på fliken Platser.</li>
     <li>Använda Assets arbetsflöde för översättning: Assets hanteras enligt egenskapskonfigurationen på fliken Assets.</li>
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
| Välj ett språk som ska användas som globalt resurslager | (Valfritt) Genom att välja en språkinställning för lagring av UGC, visas inlägg från alla språkkopior i en global konversation. Välj språkinställning för [basspråket](/help/communities/sites-console.md#translation) för webbplatsen som standard. Om du väljer Ingen gemensam lagringsplats inaktiveras global översättning. Som standard är global översättning inaktiverat. |

### Egenskaper för Assets-konfiguration {#assets-configuration-properties}

Assets-egenskaper styr hur resurser konfigureras. Mer information om översättning av resurser finns i [Skapa språkkopior för Assets](/help/assets/translation-projects.md).

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
     <li>Översättning av människor: Innehållet skickas automatiskt till översättningsleverantören för manuell översättning. </li>
     <li>Översätt inte: Assets skickas inte för översättning.</li>
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
   <td>Översätt Assets</td>
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

1. Klicka på Verktyg > Åtgärder > Moln > Cloud Service i sidlisten.
1. I området Översättningsintegrering avgör om några konfigurationer har skapats vilken länk som visas:

   * Om inga konfigurationer har skapats klickar du på Konfigurera nu.
   * Om det redan finns konfigurationer klickar du på Visa konfigurationer och sedan på länken + som visas bredvid Tillgängliga konfigurationer.

1. Ange ett namn för konfigurationen och klicka sedan på Skapa.
1. Konfigurera egenskaperna på fliken Webbplatser, Communities och Assets och klicka sedan på OK.

## Konfigurera sidor för översättning {#configuring-pages-for-translation}

Om du vill konfigurera översättning av källsidor till andra språk associerar du sidorna med följande molnkonfigurationer:

* Den molnkonfiguration som ansluter AEM till översättningsleverantören.
* Översättningsintegrationsramverket som konfigurerar informationen för översättningen.

Konfigurationen av översättningsintegreringsramverket i molnet identifierar den molnkonfiguration som ska användas för att ansluta till tjänstleverantören. När du associerar en källsida med en ramverkets molnkonfiguration måste sidan associeras med tjänstleverantörens molnkonfiguration som används i ramverkets molnkonfiguration.

När du associerar en sida med en molnkonfiguration ärver de underordnade sidorna kopplingen. Om du till exempel associerar sidan /content/geometrixx/en/products med ett Translation Integration Framework, översätts sidan Produkter och alla sidor under den enligt ramverket.

Vid behov kan du åsidosätta associationen på en underordnad sida. Innehållet på en webbplats handlar till exempel mest om kläder. En av sidorna beskriver dock företaget. Webbplatsens rotsida är associerad med ett Translation Integration Framework som anger maskinöversättning med kategorin Clothing. Den gren som beskriver företaget använder ett ramverk som utför maskinöversättning med kategorin Allmänt.

Dessutom, för alla communities [SCF-komponenter](/help/communities/scf.md) på sidorna, kommer det användargenererade innehållet (UGC) att innehålla möjligheten för användare att översätta innehåll. Mer information finns i [Översättning av användargenererat innehåll](/help/communities/translate-ugc.md).

### Koppla en sida till en översättningsleverantör {#associating-a-page-with-a-translation-provider}

Koppla en sida till översättningsleverantören som du använder för att översätta sidan och underordnade sidor.

1. På webbplatskonsolen markerar du sidan som ska konfigureras och klickar på Visa egenskaper.
1. Klicka på Redigera och sedan på fliken Cloud Service.
1. Klicka på Lägg till konfiguration > Översättningsintegrering.
1. Markera översättningsprovidern som ska användas och klicka sedan på Klar.

### Associera sidor med ett översättningsintegreringsramverk {#associating-pages-with-a-translation-integration-framework}

Koppla en sida till översättningsintegreringsramverket som definierar hur du vill översätta sidan och underordnade sidor.

1. På webbplatskonsolen markerar du sidan som ska konfigureras och klickar på Visa egenskaper.
1. Klicka på Redigera och sedan på fliken Cloud Service.
1. Klicka på Lägg till konfiguration > Översättningsintegrering.
1. Välj det ramverk för översättningsintegrering som ska användas och klicka sedan på Klar.
