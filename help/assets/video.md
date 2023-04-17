---
title: Video i Dynamic Media
description: Lär dig hur du arbetar med video i Dynamic Media, till exempel de bästa sätten att koda videofilmer, publicera videofilmer i YouTube och visa videorapporter. Lär dig även hur du lägger till undertexter eller kapitelmarkörer i videofilmer.
mini-toc-levels: 3
uuid: 97f311a3-a227-479a-91bf-fb54ecd1a55d
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: 1103b849-0042-4e11-b170-38ee81dd0157
docset: aem65
feature: Asset Management
role: User, Admin
exl-id: 28cf9e39-cab4-4278-b6c9-e84cc31964db
source-git-commit: c704397f08e163a58ee6ac1dbaefc3171298864e
workflow-type: tm+mt
source-wordcount: '7993'
ht-degree: 2%

---

# Video i Dynamic Media {#video}

I det här avsnittet beskrivs hur du arbetar med video i Dynamic Media.

## Snabbstart: Videor {#quick-start-videos}

Följande steg-för-steg-beskrivning av arbetsflödet hjälper dig att komma igång snabbt med anpassningsbara videouppsättningar i Dynamic Media. Efter varje steg finns det korsreferenser till ämnesrubriker där du kan hitta mer information.

>[!IMPORTANT]
>
>Innan du arbetar med video i Dynamic Media måste Adobe Experience Manager-administratören ha aktiverat och konfigurerat Dynamic Media-Cloud Services i Dynamic Media - Scene7-läge eller Dynamic Media - hybrid-läge.
>
>* Se [Konfigurera Dynamic Media-Cloud Services](/help/assets/config-dms7.md#configuring-dynamic-media-cloud-services) i Konfigurera Dynamic Media - Scene7-läge och [Felsöka Dynamic Media - Scene7-läge](/help/assets/troubleshoot-dms7.md).
>
>* Se [Konfigurera Dynamic Media-Cloud Services](/help/assets/config-dynamic.md#configuring-dynamic-media-cloud-services) i Konfigurera Dynamic Media - hybrid-läge.
>
>Problem med videouppspelning i Dynamic Media *endast på Experience Manager 6.5.9.0*:
>
>* Om en publicerad video uppdateras måste den publiceras igen för att återspegla leveransändringar.
>


1. **Ladda upp dina Dynamic Media-filmer** genom att göra följande:

   * Skapa en egen videokodningsprofil. Du kan också helt enkelt använda den fördefinierade _Adaptiv videokodning_ profil som medföljer Dynamic Media.

      * [Skapa en videokodningsprofil](/help/assets/video-profiles.md#creating-a-video-encoding-profile-for-adaptive-streaming).
      * Läs mer om [Bästa tillvägagångssätt för videokodning](#best-practices-for-encoding-videos).
   * Koppla videobearbetningsprofilen till en eller flera mappar där du ska överföra dina primära källvideor.

      * [Använda en videoprofil på mappar](/help/assets/video-profiles.md#applying-a-video-profile-to-folders).
      * Läs mer om [Bästa tillvägagångssätt för att ordna digitala resurser för att använda bearbetningsprofiler](/help/assets/organize-assets.md).
      * Läs mer om [Ordna digitala resurser](/help/assets/organize-assets.md).
   * Överför dina primära källvideor till mapparna. När du lägger till videofilmer i mappen kodas de enligt den videobearbetningsprofil som du tilldelade mappen.

      * Dynamic Media har främst stöd för videoklipp i kort form med en maxlängd på 30 minuter och en minimiupplösning på mer än 25 x 25.
      * Du kan överföra videofiler som är upp till 15 GB vardera.
      * [Ladda upp videor](/help/assets/managing-video-assets.md#upload-and-preview-video-assets).
      * Läs mer om [Indatafilformat som stöds](/help/assets/assets-formats.md#supported-multimedia-formats).
   * Övervaka hur [videokodning pågår](#monitoring-video-encoding-and-youtube-publishing-progress) antingen från resursen eller arbetsflödesvyn.




1. **Hantera dina Dynamic Media-filmer** genom att göra något av följande:

   * Ordna, bläddra bland och söka efter videomaterial

      * [Ordna digitala resurser](/help/assets/organize-assets.md)
Läs mer om [Bästa tillvägagångssätt för att ordna digitala resurser för att använda bearbetningsprofiler](organize-assets.md)

      * [Sök videoresurser](search-assets.md#custompredicates) eller [Sök resurser](/help/assets/search-assets.md)
   * Förhandsgranska och publicera videomaterial

      * Visa källvideon och de kodade återgivningarna av videon tillsammans med tillhörande miniatyrer:
         [Förhandsgranska videoklipp](managing-video-assets.md#upload-and-preview-video-assets) eller [Förhandsgranska resurser](previewing-assets.md)
         [Visa videoåtergivningar](video-renditions.md)
         [Hantera videoåtergivningar](manage-assets.md#managing-renditions)

      * [Hantera förinställningar för visningsprogram](managing-viewer-presets.md)
      * [Publicera resurser](publishing-dynamicmedia-assets.md)
   * Arbeta med videometadata

      * Visa egenskaperna för en kodad videoåtergivning, t.ex. bildrutefrekvens, ljud- och videobithastighet samt kodek:
         [Visa egenskaper för videoåtergivning](video-renditions.md)

      * Redigera egenskaperna för video, till exempel titel, beskrivning och taggar, anpassade metadatafält:
         [Redigera videoegenskaper](manage-assets.md#editing-properties)

      * [Hantera metadata för digitala resurser](metadata.md)
      * [Metadata-scheman](metadata-schemas.md)
   * Granska, godkänn och kommentera videoklipp och behåll fullständig versionskontroll

      * [Kommentera videoklipp](managing-video-assets.md#annotate-video-assets) eller [Anteckna resurser](manage-assets.md#annotating)

      * [Skapa en version](manage-assets.md#asset-versioning)
      * [Tillämpa arbetsflöden på resurser](assets-workflow.md) eller se [Starta ett arbetsflöde för en resurs](manage-assets.md#starting-a-workflow-on-an-asset)

      * [Granska mappresurser](bulk-approval.md)
      * [Projekt](../sites-authoring/projects.md)




1. **Publicera dina Dynamic Media-filmer** genom att göra något av följande:

   * Om du använder Adobe Experience Manager som webbinnehållshanteringssystem kan du lägga till videofilmer direkt på dina webbsidor.

      * [Lägga till videoklipp på webbsidor](adding-dynamic-media-assets-to-pages.md).
   * Om du använder ett webbinnehållshanteringssystem från en annan leverantör kan du länka eller bädda in videor på dina webbsidor.

      * Integrera video med URL:
         [Länka URL:er till ditt webbprogram](linking-urls-to-yourwebapplication.md).

      * Integrera video med inbäddad kod på webbsidan:
         [Bädda in videovisningsprogrammet på en webbsida](embed-code.md).
   * [Generera videorapporter](#viewing-video-reports).

   * [Lägga till bildtexter i video](#adding-captions-to-video).



## Arbeta med video i Dynamic Media {#working-with-video-in-dynamic-media}

Video i Dynamic Media är en totallösning som gör det enkelt att publicera högkvalitativ adaptiv video för direktuppspelning på flera skärmar, inklusive datorer, iOS, Android™, BlackBerry® och Windows-enheter. En adaptiv videouppsättning grupperar versioner av samma video som är kodade med olika bithastigheter och format som 400 kbit/s, 800 kbit/s och 1 000 kbit/s. Den stationära datorn eller mobila enheten känner av den tillgängliga bandbredden.

På en mobilenhet från iOS identifieras t.ex. en bandbredd som 3G, 4G eller Wi-Fi. Sedan väljs automatiskt rätt kodad video bland de olika videobithastigheterna i den adaptiva videouppsättningen. Videon strömmas till datorer, mobila enheter eller surfplattor.

Dessutom ändras videokvaliteten dynamiskt automatiskt om nätverksförhållandena ändras på datorn eller den mobila enheten. Om en kund går över till helskärmsläge på en stationär dator svarar den adaptiva videouppsättningen med en bättre upplösning, vilket förbättrar kundens tittarupplevelse. Med adaptiva videouppsättningar får du bästa möjliga uppspelning för kunder som spelar upp Dynamic Media-video på flera skärmar och enheter.

Den logik som en videospelare använder för att avgöra vilken kodad video som ska spelas upp eller väljas under uppspelningen baseras på följande algoritm:

1. Videospelaren läser in det inledande videofragmentet baserat på den bithastighet som ligger närmast värdet som är inställt för&quot;inledande bithastighet&quot; i spelaren.
1. Videospelaren växlar baserat på ändringar av bandbreddshastigheten med följande kriterier:

   1. Spelaren väljer den högsta bandbreddsströmmen under eller lika med den beräknade bandbredden.
   1. Spelaren hanterar bara 80 % av den tillgängliga bandbredden. Men om den byter upp sig är det mer försiktigt med bara 70 % för att undvika överskattning och omedelbart gå tillbaka.

Detaljerad teknisk information om algoritmen finns i [https://android.googlesource.com/platform/frameworks/av/+/master/media/libstagefright/httplive/LiveSession.cpp](https://android.googlesource.com/platform/frameworks/av/+/master/media/libstagefright/httplive/LiveSession.cpp)

Följande stöds för hantering av enstaka video och adaptiva videouppsättningar:

* Ladda upp video från ett antal videoformat och ljudformat som stöds och koda video till MP4 H.264-format för uppspelning på flera skärmar. Du kan använda fördefinierade adaptiva videoförinställningar, enskilda videokodningsförinställningar eller anpassa din egen kodning för att styra videons kvalitet och storlek.

   * När en adaptiv videouppsättning genereras innehåller den MP4-videor.
   * **Anteckning**: Överordnad videoklipp/källvideoklipp läggs inte till i en adaptiv videouppsättning.

* Videobildtext i alla HTML5-videovisningsprogram.
* Ordna, bläddra bland och sök videoklipp med fullt stöd för metadata för effektiv hantering av videomaterial.
* Leverera adaptiva videouppsättningar till webben, datorer och mobila enheter som iPhone, iPad, Android™, BlackBerry® och Windows Phone.

Adaptiv videoströmning stöds på olika iOS-plattformar. Se [Referenshandbok för Dynamic Media Viewer](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/video/c-html5-video-reference.html#video).

Dynamic Media har stöd för videouppspelning i mobiler för MP4 H.264-video. Du kan hitta BlackBerry®-enheter som stöder det här videoformatet på följande: [Videoformat som stöds på BlackBerry®](https://support.blackberry.com/kb/articleDetail?ArticleNumber=000005482).

Windows-enheter som stöder det här videoformatet finns på följande plats: [Media-codec som stöds för Windows Phone 8](https://learn.microsoft.com/en-us/windows/uwp/audio-video-camera/supported-codecs)



* Spela upp videon med Dynamic Media Video Viewer Presets, inklusive följande:

   * Enstaka videovisningsprogram.
   * Visningsprogram för blandade media som kombinerar både video- och bildinnehåll.

* Konfigurera videospelare för att tillgodose era varumärkesbehov.
* Integrera video på webbplatsen, mobilsajten eller mobilapplikationen med en enkel URL eller inbäddningskod.

<!-- See [Dynamic video playback](https://s7d9.scene7.com/s7/uvideo.jsp?asset=GeoRetail/Mop_AVS&config=GeoRetail/Universal_Video1&stageSize=640,480) sample. -->

Se även [Tittare för Experience Manager Assets och Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/c-html5-s7-aem-asset-viewers.html#viewers-aem-assets-dmc) och [Endast visningsprogram för Experience Manager-resurser](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/c-html5-aem-asset-viewers.html#viewers-for-aem-assets-only).

## Bästa praxis: Använda videovisningsprogrammet för HTML5 {#best-practice-using-the-html-video-viewer}

Förinställningarna för videovisningsprogrammet i Dynamic Media HTML 5 är robusta videospelare. Du kan använda dem för att undvika många vanliga problem som är kopplade till HTML5-videouppspelning. Och även problem med mobila enheter som brist på strömmande bithastighet och begränsad webbläsarräckvidd.

På designsidan av spelaren kan du utforma videospelarens funktioner med standardverktyg för webbutveckling. Du kan till exempel utforma knapparna, kontrollerna och den anpassade bakgrunden för förhandsvisningsbilder med HTML5 och CSS så att du kan nå dina kunder med ett anpassat utseende.

På visningsprogrammets uppspelningssida identifieras webbläsarens videokapacitet automatiskt. Sedan visas videon med HLS (HTTP Live Streaming) eller DASH (Dynamic Adaptive Streaming over HTTP), som också kallas för strömning med adaptiv bithastighet. Om leveransmetoderna inte finns används HTML5 progressiv i stället.

Genom att kombinera följande i en enda spelare:

* Möjlighet att utforma uppspelningskomponenterna med HTML 5 och CSS
* Har inbäddad uppspelning
* Använd adaptiv och progressiv strömning beroende på webbläsarens kapacitet

Ni kan nå ut med ert multimediematerial till både dator- och mobilanvändare och få en smidig videoupplevelse.

Se även [Om HTML5-visningsprogram](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/c-html5-aem-asset-viewers.html#viewers-for-aem-assets-only).

### Uppspelning av video på stationära datorer och mobila enheter med videovisningsprogrammet HTML5 {#playback-of-video-on-desktop-computers-and-mobile-devices-using-the-html-video-viewer}

För strömning av anpassningsbara video för datorer och mobilenheter baseras de videor som används för växling av bithastighet på alla MP4-videor i den adaptiva videouppsättningen.

Videouppspelning sker med DASH eller HLS, eller progressiv videohämtning. I tidigare versioner av Experience Manager, som 6.0, 6.1 och 6.2, strömmades videofilmer via HTTP.

I Experience Manager 6.3 och senare direktuppspelas videor via HTTPS (dvs. DASH eller HLS) eftersom DM-gatewaytjänstens URL alltid använder HTTPS. Det här standardbeteendet påverkar inte kunderna. Det innebär att direktuppspelning av video alltid sker via HTTPS, såvida det inte stöds av webbläsaren. (se följande tabell). Därför

* Om du har en HTTPS-webbplats med HTTPS-videoströmning går det bra att strömma.
* Om du har en HTTP-webbplats med HTTPS-videoströmning går det bra att strömma och det finns inga blandade innehållsproblem i webbläsaren.

DASH är den internationella standarden och HLS är en Apple-standard. Båda används för adaptiv videoströmning. Och båda teknikerna justerar automatiskt uppspelningen baserat på bandbreddskapaciteten i nätverket. Man kan också &quot;söka&quot; till valfri punkt i videon utan att behöva vänta på att resten av videon ska laddas ned.

Progressiv video levereras genom att videon hämtas och lagras lokalt på en användares dator eller mobila enhet.

I följande tabell beskrivs enheten, webbläsaren och uppspelningsmetoden för videofilmer på stationära datorer och mobila enheter med Dynamic Media Video Viewer.

<table>
 <tbody>
  <tr>
   <td><strong>Enhet</strong></td>
   <td><strong>Webbläsare</strong></td>
   <td><strong>Videouppspelningsläge</strong></td>
  </tr>
  <tr>
   <td>Skrivbord</td>
   <td>Internet Explorer 9 och 10</td>
   <td>Progressiv nedladdning.</td>
  </tr>
  <tr>
   <td>Skrivbord</td>
   <td>Internet Explorer 11+</td>
   <td>I Windows 8 och Windows 10 - Tvinga användning av HTTPS när DASH* eller HLS begärs. Känd begränsning: HTTP på DASH* eller HLS fungerar inte i den här kombinationen av webbläsare/operativsystem<br /> <br /> I Windows 7 - progressiv nedladdning. Använder standardlogik för att välja HTTP- eller HTTPS-protokoll.</td>
  </tr>
  <tr>
   <td>Skrivbord</td>
   <td>Firefox 23-44</td>
   <td>Progressiv nedladdning.</td>
  </tr>
  <tr>
   <td>Skrivbord</td>
   <td>Firefox 45 eller senare</td>
   <td>DASH* eller HLS adaptiv bithastighetsströmning.</td>
  </tr>
  <tr>
   <td>Skrivbord</td>
   <td>Krom</td>
   <td>DASH* eller HLS adaptiv bithastighetsströmning.</td>
  </tr>
  <tr>
   <td>Skrivbord</td>
   <td>Safari (Mac)</td>
   <td>HLS adaptiv bithastighetsströmning.</td>
  </tr>
  <tr>
   <td>Mobil</td>
   <td>Chrome (Android™ 6 eller tidigare)</td>
   <td>Progressiv nedladdning.</td>
  </tr>
  <tr>
   <td>Mobil</td>
   <td>Chrome (Android™ 7 eller senare)</td>
   <td>DASH* eller HLS adaptiv bithastighetsströmning.</td>
  </tr>
  <tr>
   <td>Mobil</td>
   <td>Android™ (standardwebbläsare)</td>
   <td>Progressiv nedladdning.</td>
  </tr>
  <tr>
   <td>Mobil</td>
   <td>Safari (iOS)</td>
   <td>HLS adaptiv bithastighetsströmning.</td>
  </tr>
  <tr>
   <td>Mobil</td>
   <td>Chrome (iOS)</td>
   <td>HLS adaptiv bithastighetsströmning.</td>
  </tr>
  <tr>
   <td>Mobil</td>
   <td>BlackBerry®</td>
   <td>DASH* eller HLS adaptiv bithastighetsströmning./td&gt;
  </tr>
 </tbody>
</table>

>[!IMPORTANT]
>
>*Om du vill använda DASH för dina videor måste det först aktiveras av Adobe tekniska support på ditt konto. Se [Aktivera DASH på ditt konto](#enable-dash).

## Arkitektur för Dynamic Media videolösning {#architecture-of-dynamic-media-video-solution}

Följande bild visar det övergripande arbetsflödet för redigering av videoklipp som har överförts och kodats med hjälp av DMGGateway (i Dynamic Media Hybrid-läge) och som har gjorts tillgängliga för offentlig användning.

![chlimage_1-427](assets/chlimage_1-427.png)

## Hybrid publiceringsarkitektur för videor {#hybrid-publishing-architecture-for-videos}

![chlimage_1-428](assets/chlimage_1-428.png)

## Bästa tillvägagångssätt för att koda videofilmer {#best-practices-for-encoding-videos}

The **Dynamic Media Encode Video** arbetsflödet kodar video om du har aktiverat Dynamic Media och konfigurerat videolmolntjänster. Det här arbetsflödet innehåller information om arbetsflödets processhistorik och fel. Om du har aktiverat Dynamic Media och konfigurerat videolmolntjänster kan du **[!UICONTROL Dynamic Media Encode Video]** arbetsflödet aktiveras automatiskt när du överför en video. (Om du inte använder Dynamic Media **[!UICONTROL DAM Update Asset]** arbetsflödet börjar gälla.)

<!-- DEAD The following are best-practice tips for encoding source video files.

For advice about video encoding, see [Video Encoding Basics](https://www.adobe.com/go/learn_s7_encoding_en).

* [Streaming 101: The Basics — Codecs, Bandwidth, Data Rate, and Resolution](https://www.adobe.com/go/learn_s7_streaming101_en). -->

### Källvideofiler {#source-video-files}

När du kodar en videofil ska du använda en källvideofil med högsta möjliga kvalitet. Undvik att använda tidigare kodade videofiler eftersom dessa filer redan är komprimerade, och ytterligare kodning skapar en video med delkvalitet.

* Dynamic Media har främst stöd för videoklipp i kort form med en maxlängd på 30 minuter och en minimiupplösning på mer än 25 x 25.
* Du kan överföra primära källvideofiler på upp till 15 GB vardera.

I följande tabell beskrivs rekommenderad storlek, proportioner och lägsta bithastighet som källvideofilerna måste ha innan du kodar dem:

| Storlek | Proportioner | Minsta bithastighet |
|--- |--- |--- |
| 1024 x 768 | 4:3 | 4 500 kbit/s för de flesta videoklipp. |
| 1280 x 720 | 16:9 | 3 000 - 6 000 kbit/s, beroende på mängden rörelse i videon. |
| 1920 x 1080 | 16:9 | 6000 - 8 000 kbit/s, beroende på mängden rörelse i videon. |

### Hämta metadata för en fil {#obtaining-a-file-s-metadata}

Du kan hämta metadata för en fil genom att visa dess metadata med ett videoredigeringsverktyg eller med ett program som utformats för att hämta metadata. Nedan följer instruktioner om hur du använder MediaInfo, ett tredjepartsprogram, för att hämta videofilens metadata:

1. Gå till [MediaInfo-hämtning](https://mediaarea.net/en/MediaInfo/Download).
1. Välj och hämta installationsprogrammet för den grafiska användargränssnittsversionen och följ installationsanvisningarna.
1. Efter installationen högerklickar du på videofilen (endast Windows) och väljer MediaInfo, eller öppnar MediaInfo och drar videofilen till programmet. Alla metadata som är associerade med videofilen, inklusive bredd, höjd och fps, visas.

### Proportioner {#aspect-ratio}

När du väljer eller skapar en förinställning för videokodning för den primära källvideofilen måste du se till att förinställningen har samma proportioner som den primära källvideofilen. Proportionerna är proportionerna mellan videons bredd och höjd.

Om du vill ta reda på videofilens proportioner hämtar du filens metadata och noterar filens bredd och höjd (se Hämta filens metadata ovan). Använd sedan den här formeln för att bestämma proportionerna:

width/height = aspect ratio

I följande tabell beskrivs hur formelresultaten översätts till vanliga alternativ för proportioner:

| Formelresultat | Proportioner |
|--- |--- |
| 1.33 | 4:3 |
| 0.75 | 3:4 |
| 1.78 | 16:9 |
| 0.56 | 9:16 |

En video som till exempel är 1440 bredd x 1080 höjd har proportionerna 1440/1080 eller 1,33. I det här fallet väljer du en förinställning för videokodning med 4:3-proportioner för att koda videofilen.

### Bithastighet {#bitrate}

Bithastighet är den mängd data som kodas för att skapa en enda sekund av videouppspelning. Bithastigheten mäts i kilobit per sekund (kbit/s).

>[!NOTE]
>
>Eftersom förlustgivande komprimering används för alla kodekar är bithastigheten den viktigaste faktorn i videokvaliteten. Ju mer du komprimerar en videofil desto sämre blir kvaliteten. Därför är alla andra egenskaper lika (upplösning, bildrutehastighet och kodek), ju lägre bithastighet, desto lägre kvalitet får den komprimerade filen.

När du väljer en bithastighetskodning kan du välja mellan två typer:

* **[!UICONTROL Constant Bitrate Encoding]** (CBR) - Under CBR-kodning är bithastigheten eller antalet bitar per sekund densamma under hela kodningsprocessen. CBR-kodning bevarar den angivna datahastigheten enligt inställningen för hela videon. CBR-kodning optimerar inte heller mediefiler för kvalitet utan sparar på lagringsutrymmet.
Använd CBR om videon innehåller en liknande rörelsenivå i hela videon. CBR används oftast för direktuppspelat videoinnehåll. Se även [Använda egna parametrar för videokodning](/help/assets/video-profiles.md#using-custom-added-video-encoding-parameters).

* **[!UICONTROL Variable Bitrate Encoding]** (VBR) - VBR-kodning justerar datahastigheten nedåt och till den övre gräns som du anger, baserat på de data som krävs av kompressorn. Den här funktionen innebär att under en VBR-kodningsprocess ökar eller minskar bithastigheten för mediefilen dynamiskt beroende på mediafilens behov av bithastighet.
VBR tar längre tid att koda men ger det mest fördelaktiga resultatet. mediefilens kvalitet är överlägsen. VBR används oftast för http-progressiv leverans av videoinnehåll.

När använder du VBR jämfört med CRB?
När du väljer VBR jämfört med CBR rekommenderar vi nästan alltid att du använder VBR för dina mediefiler. VBR ger filer av högre kvalitet med konkurrenskraftiga bithastigheter. När du använder VBR måste du vara säker på att du använder kodning i två omgångar och ställa in den maximala bithastigheten till 1,5 gånger målvideobithastigheten.

När du väljer en förinställning för videokodning bör du komma ihåg målanvändarens anslutningshastighet. Välj en förinställning med en datahastighet som är 80 % av den hastigheten. Om målanvändarens anslutningshastighet till exempel är 1000 kbit/s är den bästa förinställningen en med en videodatahastighet på 800 kbit/s.

I den här tabellen beskrivs datahastigheten för typiska anslutningshastigheter.

| Hastighet (kbit/s) | Anslutningstyp |
|--- |--- |
| 256 | Uppringd anslutning. |
| 800 | Vanlig mobilanslutning. För den här anslutningen anger du en datahastighet mellan 400 och maximalt 800 för 3G-upplevelser som mål. |
| 2000 | Vanlig anslutning till stationär bredbandsuppkoppling. För den här anslutningen anger du en datahastighet i intervallet 800-2000 kbit/s med de flesta mål som är i genomsnitt 1200-1500 kbit/s. |
| 5000 | Vanlig bredbandsanslutning. Kodning i det här övre intervallet rekommenderas inte eftersom videoleverans i den här hastigheten inte är tillgänglig för de flesta konsumenter. |

### Upplösning {#resolution}

**Upplösning** beskriver en videofils höjd och bredd i pixlar. Den mesta källvideon lagras med hög upplösning (till exempel 1 920 x 1 080). Vid direktuppspelning komprimeras källvideo till en lägre upplösning (640 x 480 eller lägre).

Upplösning och datahastighet är två sammankopplade faktorer som avgör videokvaliteten. Om du vill behålla samma videokvalitet måste datahastigheten vara högre ju fler pixlar en videofil har (ju högre upplösning). Ta till exempel antalet pixlar per bildruta i en 320 x 240-upplösning och en 640 x 480-upplösningsvideofil:

| Upplösning | Pixlar per bildruta |
|--- |--- |
| 320 x 240 | 76,800 |
| 640 x 480 | 307,200 |

Filen på 640 x 480 har fyra gånger fler pixlar per bildruta. För att uppnå samma datahastighet för dessa två exempelupplösningar tillämpar du fyra gånger komprimeringen på 640 x 480-filen, vilket kan minska videons kvalitet. En videodatahastighet på 250 kbit/s ger därför en högkvalitativ bild med upplösningen 320 x 240, men inte med upplösningen 640 x 480.

I allmänhet gäller att ju högre datahastighet du använder, desto bättre utseende på videon och ju högre upplösning du använder, desto högre datahastighet måste du behålla visningskvaliteten (jämfört med lägre upplösningar).

Eftersom upplösning och datahastighet är länkade finns det två alternativ när du kodar video:

* Välj en datahastighet och koda sedan med den högsta upplösningen som ser bra ut med den datahastighet du väljer.
* Välj en upplösning och koda sedan med den datahastighet som krävs för att få en video med hög kvalitet med den upplösning du väljer.

När du väljer (eller skapar) en förinställning för videokodning för den primära källvideofilen använder du den här tabellen för att ange rätt upplösning:

| Upplösning | Höjd (pixlar) | Skärmstorlek |
|--- |--- |--- |
| 240p | 240 | Liten skärm |
| 300p | 300 | Liten skärm för mobila enheter |
| 360p | 360 | Liten skärm |
| 480p | 480 | Medelstor skärm |
| 720p | 720 | Stor skärm |
| 1080p | 1080 | Stor HD-skärm |

### Fps (bildrutor per sekund) {#fps-frames-per-second}

I USA och Japan spelas de flesta videoklipp in med 29,97 bildrutor per sekund (fps). i Europa spelas de flesta videoklipp in med 25 bildrutor per sekund. Film filmas med 24 fps.

Välj en förinställning för videokodning som matchar fps-hastigheten för den primära källvideofilen. Om den primära källvideon till exempel är 25 fps väljer du en kodningsförinställning med 25 fps. Som standard används den primära källvideofilens fps för all anpassad kodning. Därför behöver du inte uttryckligen ange fps-inställningen när du skapar en förinställning för videokodning.

### Videokodningsdimensioner {#video-encoding-dimensions}

För bästa resultat väljer du kodningsdimensioner så att källvideon är en hel multipel av alla dina kodade videor.

Om du vill beräkna förhållandet dividerar du källbredden med den kodade bredden för att få breddförhållandet. Sedan dividerar du källhöjden med kodad höjd för att få höjdförhållandet.

Om förhållandet är ett heltal betyder det att videon är optimalt skalad. Om den resulterande kvoten inte är ett heltal påverkas videokvaliteten genom att kvarvarande pixelartefakter lämnas kvar på skärmen. Effekten märks mest när videon innehåller text.

Anta till exempel att källvideon är 1 920 x 1 080. I följande tabell ger de tre kodade videoklippen de optimala kodningsinställningarna som kan användas.

| Videotyp | Bredd x höjd | Breddförhållande | Höjdförhållande |
|--- |--- |--- |--- |
| Källa | 1920 x 1080 | 1 | 1 |
| Kodad | 960 x 540 | 2 | 2 |
| Kodad | 640 x 360 | 3 | 3 |
| Kodad | 480 x 270 | 4 | 4 |

### Kodat videofilformat {#encoded-video-file-format}

Dynamic Media rekommenderar att du använder MP4 H.264-videokodningsförinställningar. Eftersom MP4-filer använder H.264-videokodeken ger den video med hög kvalitet men i en komprimerad filstorlek.

### Aktivera DASH på ditt konto {#enable-dash}

DASH (Digital Adaptive Streaming over HTTP) är den internationella standarden för direktuppspelad video och används i stor utsträckning av olika videovisningsprogram. När DASH är aktiverat för ditt konto kan du välja mellan DASH eller HLS för adaptiv videoströmning. Eller så kan du välja båda med automatisk växling mellan spelare när **[!UICONTROL auto]** är valt som uppspelningstyp i visningsförinställningen.

Några viktiga fördelar med att aktivera DASH på ditt konto är följande:

* Paketera DASH-strömvideo för strömning med adaptiv bithastighet. Den här metoden leder till ökad effektivitet vid leverans. Adaptiv strömning ger bästa möjliga tittarupplevelse för dina kunder.
* Webbläsaroptimerad direktuppspelning med Dynamic Media-spelare växlar mellan HLS- och DASH-strömning för att säkerställa bästa möjliga servicekvalitet. Videospelaren växlar automatiskt till HLS när en Safari-webbläsare används.
* Du kan konfigurera den direktuppspelningsmetod (HLS eller DASH) som du föredrar genom att redigera visningsförinställningen för videon.
* Optimerad videokodning säkerställer att ingen ytterligare lagring används samtidigt som DASH-funktionen aktiveras. En enda uppsättning videokodningar skapas för både HLS och DASH för att optimera lagringskostnaderna för video.
* Gör videomaterialet mer tillgängligt för kunderna.
* Hämta URL:en för direktuppspelning via API:er också.

   >[!IMPORTANT]
   >
   >Du kan för närvarande bara aktivera DASH på ditt konto i Asien-Stillahavsområdet och Nordamerika. kommer snart i Europa-Mellanöstern-Afrika.

Om du vill aktivera DASH på ditt konto krävs två steg:

* Konfigurera Dynamic Media att använda DASH som du enkelt kan göra själv.
* Konfigurera Experience Manager 6.5 för att använda DASH, vilket sker via ett kundsupportärende från Adobe som du skapar och skickar in.

**Så här aktiverar du DASH på ditt konto:**

1. **Konfigurera Dynamic Media** - I Dynamic Media på Experience Manager 6.5 navigerar du till [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr).
1. Sök efter **AEM Assets Dynamic Media Video Advanced Streaming** funktionsflagga.
1. Markera kryssrutan för att aktivera (aktivera) DASH.
1. Välj **[!UICONTROL Save]**.
1. **Konfigurera Experience Manager 6.5** - [Använd Admin Console för att börja skapa ett nytt supportärende](https://helpx.adobe.com/enterprise/using/support-for-experience-cloud.html).
1. Följ instruktionerna för att skapa ett supportärende och försäkra dig om att du anger följande information:

   * Primärt kontaktnamn, e-postadress, telefon.
   * Namn på ditt Dynamic Media-konto.
   * Ange att du vill att DASH ska aktiveras på Experience Manager 6.5.

1. Adobe kundsupport lägger till dig i DASH-kundens väntelista baserat på i vilken ordning begäranden skickas.
1. När Adobe är redo att hantera din begäran kontaktar kundsupporten dig för att koordinera och ange ett måldatum för aktivering av DASH.
1. Du meddelas när du är klar av kundsupporten.
1. Skapa [videovisningsförinställning](/help/assets/managing-viewer-presets.md#creating-a-new-viewer-preset) som vanligt.

## Visa videorapporter {#viewing-video-reports}

>[!NOTE]
>
>Videorapporter är bara tillgängliga när du kör Dynamic Media - hybrid-läge.

Videorapporter visar flera aggregerade mått över en viss tid, så att du kan övervaka att *publicerad* individuella och aggregerade videor fungerar som förväntat. Följande viktigaste mätdata samlas in för alla publicerade videor på hela webbplatsen:

* Video börjar
* Slutförandefrekvens
* Genomsnittlig tid för video
* Total tid för video
* Videor per besök

En tabell med alla *publicerad* videofilmer visas också i en lista så att du kan spåra de mest visade videofilmerna på webbplatsen baserat på hur många videostarter som har gjorts.

När du trycker på ett videonamn i listan visas videons rapport om målgruppsinnehållande (bortfall) i form av ett linjediagram. Diagrammet visar antalet vyer för en given tidpunkt under videouppspelning. När du spelar upp videon synkroniseras det lodräta strecket med tidsindikatorn i spelaren. Släppningar i linjediagramdata indikerar var publiken slutar intressera sig.

Om videon kodades utanför Adobe Experience Manager Dynamic Media är inte data för målgruppsinnehållande (bortfall) och uppspelningsprocent tillgängliga i tabellen.

Se även [Konfigurera Dynamic Media-Cloud Services](/help/assets/config-dynamic.md).

>[!NOTE]
>
>Spårnings- och rapportdata baseras uteslutande på användningen av Dynamic Medias egen videospelare och tillhörande videospelarförinställning. Därför kan du inte spåra och rapportera om videofilmer som spelas upp med andra videospelare.

Första gången du anger Videorapporter visas som standard videodata från och med den första i den aktuella månaden och till och med den aktuella månadens datum. Du kan dock åsidosätta standarddatumintervallet genom att ange ett eget datumintervall. Nästa gång du anger Videorapporter används det datumintervall du har angett.

För att videorapporter ska fungera på rätt sätt skapas ett Report Suite-ID automatiskt när Dynamic Media-Cloud Services konfigureras. Samtidigt skickas Report Suite-ID:t till publiceringsservern så att det är tillgängligt för funktionen Kopiera URL när du förhandsgranskar resurser. Den här funktionen kräver dock att publiceringsservern redan har konfigurerats. Om publiceringsservern inte är konfigurerad kan du fortfarande publicera för att se videorapporten. Du måste dock gå tillbaka till Dynamic Media Cloud Configuration och trycka på **[!UICONTROL OK]**.

**Så här visar du videorapporter:**

1. Tryck på logotypen Experience Manager i det övre vänstra hörnet av Experience Manager och tryck sedan på **[!UICONTROL Tools]** (hammarikon) > **[!UICONTROL Assets]** > **[!UICONTROL Video Reports]**.
1. Gör något av följande på sidan Videorapporter:

   * I det övre högra hörnet trycker du på **Uppdatera videorapport** ikon.
Använd bara Uppdatera om rapportens slutdatum är den aktuella dagen. Om du gör det ser du till att du ser videospårningen som har utförts sedan du senast körde rapporten.

   * I det övre högra hörnet trycker du på **Datumväljaren** ikon.
Ange start- och slutdatumintervallet som du vill ha videodata för och tryck sedan på **[!UICONTROL Run Report]**.

   Grupprutan Övre mått identifierar olika aggregerade mått för alla *publicerad* videor på hela webbplatsen.

1. I tabellen som visar de publicerade videoklippen trycker du på ett videonamn för att spela upp videon och ser även videons återgivningsrapport.

### Visa videorapporter baserade på ett videovisningsprogram som du har skapat med Dynamic Media HTML5 Viewer SDK {#viewing-video-reports-based-on-a-video-viewer-that-you-created-using-the-scene-hmtl-viewer-sdk}

Om du använder ett användningsklart visningsprogram från Dynamic Media, eller om du har skapat en anpassad visningsförinställning baserad på ett användningsklart videovisningsprogram, krävs inga ytterligare steg för att visa videorapporter. Om du har skapat ett eget videovisningsprogram baserat på SDK-API:t för visningsprogrammet för HTML5, ska du följa de här stegen för att se till att videovisningsprogrammet skickar spårningshändelser till Dynamic Media videorapporter.

Använd [Referenshandbok för Adobe Dynamic Media-visningsprogram](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources.html) och [HTML5 Viewer SDK API](https://s7d1.scene7.com/s7sdk/3.10/docs/jsdoc/index.html) för att skapa egna videovisningsprogram.

**Så här visar du videorapporter baserade på ett videovisningsprogram som du har skapat med Dynamic Media HTML5 Viewer SDK:**

1. Navigera till alla publicerade videoresurser.
1. I listrutan i det övre vänstra hörnet på resursens sida väljer du **[!UICONTROL Viewers]**.
1. Välj en förinställning för visningsprogrammet och kopiera inbäddningskoden.
1. I inbäddningskoden söker du efter raden med följande:

   `videoViewer.setParam("config2", "<value>");`

   The `config2` -parametern aktiverar spårning i visningsprogram för HTML5. Det är också en företagsspecifik förinställning som innehåller konfigurationsinformationen för Videorapportering och för kundspecifika Adobe Analytics-konfigurationer.

   Det korrekta värdet för parametern config2 finns både i **[!UICONTROL Embed Code]** och i kopieringsfunktionen **[!UICONTROL URL]**. I URL:en från kopieringskommandot **[!UICONTROL URL]** letar du efter parametern `&config2=<value>`. Värdet är nästan alltid `companypreset`, men i vissa fall kan det också vara `companypreset-1`, `companypreset-2` osv.

1. Lägg till AppMeasurementBridge .jsp på visningsprogramsidan i din anpassade videovisningsprogramkod genom att göra följande:

   * Först avgör du om du behöver `&preset` parameter.

      Om `config2` parametern är `companypreset`det gör du *not* behov `&preset=parameter`.

      If `config2` är vad som helst, ställ in parametern preset på samma sätt som `config2` parameter. Om `config2=companypreset-2`, lägga till `&param2=companypreset-2` till URL:en AppMeasurmentBridge.jsp.

   * Lägg sedan till skriptet AppMeasurementBridge.jsp:

      `<script language="javascript" type="text/javascript" src="https://s7d1.scene7.com/s7viewers/AppMeasurementBridge.jsp?company=robindallas&preset=companypreset-2"></script>`

1. Skapa komponenten TrackingManager genom att göra följande:

   * Efter att du har ringt `s7sdk.Util.init();`skapar du en TrackingManager-instans för att spåra händelser genom att lägga till följande:

      `var trackingManager = new s7sdk.TrackingManager();`

   * Koppla komponenter till TrackingManager genom att göra följande:

      I `s7sdk.Event.SDK_READY` -händelsehanteraren kopplar du komponenten som du vill spåra till TrackingManager.

      Om komponenten till exempel är `videoPlayer`, lägga till

      `trackingManager.attach(videoPlayer);`

      för att bifoga komponenten till trackingManager. Om du vill spåra flera visningsprogram på en sida använder du flera komponenter för spårningshanteraren.

   * Skapa AppMeasurementBridge-objektet genom att lägga till följande:

      ```
      var appMeasurementBridge = new AppMeasurementBridge(); appMeasurementBridge.setVideoPlayer(videoPlayer);
      ```

   * Lägg till spårningsfunktionen genom att lägga till följande:

      ```
      trackingManager.setCallback(appMeasurementBridge.track, 
       appMeasurementBridge);
      ```
   AppMeasurementBridge-objektet har en inbyggd spårfunktion. Du kan dock ge dig ett eget stöd för flera spårningssystem eller andra funktioner.

<!--    For more information, see *Using the TrackingManager Component* in the *Scene7 HTML5 Viewer SDK User Guide* available for download from [Adobe Developer Connection](https://help.adobe.com/en_US/scene7/using/WSef8d5860223939e2-43dedf7012b792fc1d5-8000.html). -->

## Lägga till undertexter till video {#adding-captions-to-video}

Du kan utöka räckvidden för dina videor till globala marknader genom att lägga till undertexter till enskilda videor eller till adaptiva videouppsättningar. Genom att lägga till undertextning slipper du att duplicera ljudet eller att du behöver använda inbyggda högtalare för att spela in ljudet igen för varje språk. Videon spelas upp på det språk den spelades in på. Undertexter på främmande språk visas så att personer på olika språk fortfarande kan förstå ljuddelen.

Undertexter ger också bättre tillgänglighet för människor som är döva eller hörselskadade.

>[!NOTE]
>
>Den videospelare som du använder måste ha stöd för visning av bildtexter.

Se även [Tillgänglighet i Dynamic Media](/help/assets/accessibility-dm.md).

Dynamic Media konverterar bildtextfiler till JSON-format (JavaScript Object Notation). Den här konverteringen innebär att du kan bädda in JSON-texten på en webbsida som en dold men fullständig utskrift av videon. Sökmotorerna kan sedan crawla och indexera innehållet så att videoklippen blir lättare att hitta och ge kunderna ytterligare information om videoinnehållet.

Se [Hantera statiskt innehåll (inte bildinnehåll)](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/c-serving-static-nonimage-contents.html#image-serving-api) i *Hjälp om Dynamic Media Image Serving and Rendering API* om du vill ha mer information om hur du använder JSON-funktionen i en URL.

**Så här lägger du till bildtexter eller undertexter till video:**

1. Använd ett program eller en tjänst från tredje part för att skapa en undertextningsfil för video.

   Kontrollera att filen du skapar följer standarden WebVTT (Web Video Text Tracks). Bildtextens filnamnstillägg är .vtt. Du kan läsa mer om bildtextstandarden WebVTT.

   Se [WebVTT: Textspår för webbvideo](https://w3c.github.io/webvtt/).

   Det finns både kostnadsfria och premiumverktyg och tjänster som du kan använda för att skapa bildtexter/undertexter utanför Dynamic Media. Om du till exempel vill skapa en enkel videobeskrivningsfil utan formatering kan du använda följande kostnadsfria redigerings- och redigeringsverktyg för bildtexter online:

   [WebVTT Caption Maker](https://testdrive-archive.azurewebsites.net/Graphics/CaptionMaker/Default.html)

   Du får bäst resultat om du använder verktyget i Internet Explorer 9 eller senare, Google Chrome eller Safari.

   I verktyget **[!UICONTROL Enter URL of video file]** -fält, klistra in den kopierade URL-adressen för videofilen och klicka sedan på **[!UICONTROL Load]**. Se [Hämta en URL för en resurs](/help/assets/linking-urls-to-yourwebapplication.md#obtaining-a-url-for-an-asset) för att hämta URL:en till själva videofilen som du sedan kan klistra in i **[!UICONTROL Enter URL of video file field]**. Internet Explorer, Chrome och Safari kan sedan spela upp videon direkt.

   Följ nu instruktionerna på skärmen för att skapa och spara WebVTT-filen. När du är klar kopierar du bildtextfilens innehåll och klistrar in det i en vanlig textredigerare och sparar det med en `.vtt` filnamnstillägg.

   >[!NOTE]
   >
   >För globalt stöd för videoundertexter på flera språk kräver WebVTT-standarden att du skapar separata VTT-filer och anropar varje språk som du vill ha stöd för.

   Vanligtvis vill du ge bildtexten VTT ett namn som är detsamma som videofilen och bifoga den med språkinställningen -EN, -FR eller -DE. Genom att göra det kan det hjälpa dig att automatisera genereringen av video-URL:er med ditt befintliga system för hantering av webbinnehåll.

1. I Experience Manager överför du WebVTT-bildtextfilen till DAM.
1. Navigera till *publicerad* videoresurs som du vill associera med bildtextfilen som du överförde.

   Kom ihåg att URL:er endast går att kopiera *efter* att du har *publicerat* resurserna.

   Se [Publicera resurser](/help/assets/publishing-dynamicmedia-assets.md).

1. Gör något av följande:

   * Tryck på **[!UICONTROL URL]**. I dialogrutan URL-adress markerar och kopierar du URL-adressen till Urklipp och sedan förbi URL-adressen till en enkel textredigerare. Lägg till den kopierade URL:en för videon med följande syntax:

      `&caption=<server_path>/is/content/<path_to_caption.vtt_file,1>`

      Anteckna `,1` i slutet av bildtextbanan. Omedelbart efter `.vtt` filnamnstillägget i sökvägen kan du aktivera (aktivera) eller inaktivera (inaktivera) den stängda bildtextknappen i videospelarfältet genom att ange `,1` eller `,0`, respektive.

   * Om du vill visa en inbäddad video trycker du **[!UICONTROL Embed Code]**. I dialogrutan Bädda in kod markerar och kopierar du den inbäddade koden till Urklipp och klistrar sedan in koden i en enkel textredigerare. Lägg till den kopierade inbäddningskoden med följande syntax:

      `videoViewer.setParam("caption","<path_to_caption.vtt_file,1>");`

      Anteckna `,1` i slutet av bildtextbanan. Omedelbart efter `.vtt` filnamnstillägget i sökvägen kan du aktivera (aktivera) eller inaktivera (inaktivera) den stängda bildtextknappen i videospelarfältet genom att ange `,1` eller `,0`, respektive.

## Lägga till kapitelmarkörer i video {#adding-chapter-markers-to-video}

Du kan göra det enklare att titta på och navigera i videoklipp med långa formulär genom att lägga till kapitelmarkörer i enstaka videor eller i adaptiva videouppsättningar. När en användare spelar upp videon kan han/hon klicka på kapitelmarkörerna på tidslinjen (kallas även videobandskrubbaren) för att enkelt navigera till sin intressepunkt. Eller så går de direkt till nytt innehåll, demonstrationer och självstudiekurser.

>[!NOTE]
>
>Den videospelare som används måste ha stöd för kapitelmarkörer. Dynamic Media videospelare har stöd för kapitelmarkörer, men det är inte säkert att tredjepartsvideospelare används.

Om du vill kan du skapa och märka ut ett eget anpassat visningsprogram med kapitel i stället för att använda en förinställning för visningsprogrammet för video. Instruktioner om hur du skapar ett eget visningsprogram för HTML5 med kapitelnavigering finns i SDK-API:t för visningsprogrammet för Adobe HTML5, under klasserna&quot;Anpassa beteendet med modifierare&quot; `s7sdk.video.VideoPlayer` och `s7sdk.video.VideoScrubber`. Se [HTML5 Viewer SDK API](https://s7d1.scene7.com/s7sdk/3.10/docs/jsdoc/index.html) dokumentation.

<!-- If desired, you can create and brand your own custom video viewer with chapters instead of using a video viewer preset. For instructions on creating your own HTML5 viewer with chapter navigation, in the Adobe Scene7 Viewer SDK for HTML5 guide, reference the heading "Customizing Behavior Using Modifiers" under the classes `s7sdk.video.VideoPlayer` and `s7sdk.video.VideoScrubber`. The Adobe Scene7 Viewer SDK is available as a download from [Adobe Developer Connection](https://help.adobe.com/en_US/scene7/using/WSef8d5860223939e2-43dedf7012b792fc1d5-8000.html). -->

Du skapar en kapitellista för videon på ungefär samma sätt som du skapar bildtexter. Det innebär att du skapar en WebVTT-fil. Observera dock att den här filen måste vara separat från alla WebVTT-beskrivningsfiler som du också använder. du kan inte kombinera bildtexter och kapitel i en WebVTT-fil.

Du kan använda följande exempel som exempel på det format du använder för att skapa en WebVTT-fil med kapitelnavigering:

### WebVTT-fil med videokapitelnavigering {#webvtt-file-with-video-chapter-navigation}

```xml
WEBVTT
Chapter 1
00:00.000 --> 01:04.364
The bicycle store behind it all.
Chapter 2
01:04.364 --> 02:00.944
Creative Cloud.
Chapter 3
02:00.944 --> 03:02.937
Ease of management for a working solution.
Chapter 4
03:02.937 --> 03:35.000
Cost-efficient access to rapidly evolving technology.
```

I exemplet ovan `Chapter 1` är referensidentifieraren och är valfri. Referenstiden för `00:00:000 --> 01:04:364` anger kapitlets starttid och sluttid, i `00:00:000` format. De tre sista siffrorna är millisekunder och kan lämnas som `000`, om så önskas. Kapiteltiteln för `The bicycle store behind it all` är den faktiska beskrivningen av kapitlets innehåll. Referensidentifieraren, startreferenstiden och kapiteltiteln visas alla i en videospelares popup när en användare håller muspekaren över en visuell referenspunkt i videons tidslinje.

Eftersom du använder ett HTML5-videovisningsprogram bör du kontrollera att den kapitelfil du skapar följer standarden WebVTT (Web Video Text Tracks). Kapitelfilnamnstillägget är `.vtt`. Du kan läsa mer om bildtextstandarden WebVTT.

Se [WebVTT: Textspår för webbvideo](https://w3c.github.io/webvtt/)

**Så här lägger du till kapitelnavigering:**

1. Spara `.vtt` i UTF8-kodning så att du slipper problem med teckenåtergivning i kapiteltiteltexten.

   Vanligtvis vill du ge kapitlet VTT-filen samma namn som videofilen och bifoga den med kapitel. Genom att göra det kan det hjälpa dig att automatisera genereringen av video-URL:er med ditt befintliga system för hantering av webbinnehåll.
1. Ladda upp din WebVTT-kapitelfil i Experience Manager.

   Se [Överför resurser](/help/assets/manage-assets.md#uploading-assets).

1. Gör något av följande:

   <table>
     <tbody>
      <tr>
       <td>För en popup-video</td>
       <td>
       <ol>
       <li>Navigera till <i>publicerad </i>videoresurs som du vill associera med den kapitelfil som du har överfört. Kom ihåg att URL:er endast går att kopiera <i>efter</i> att du har <i>publicerat</i> resurserna. Se <a href="/help/assets/publishing-dynamicmedia-assets.md">Publicera resurser.</a></li>
       <li>Klicka eller tryck på i listrutan <strong>Tittare</strong>.</li>
       <li>Tryck eller klicka på förinställningsnamnet för videovisningsprogrammet i den vänstra listen. En förhandsgranskning av videon öppnas på en separat sida.</li>
       <li>Klicka på längst ned i den vänstra listen <strong>URL</strong>.</li>
       <li>I dialogrutan URL-adress markerar och kopierar du URL-adressen till Urklipp och sedan förbi URL-adressen till en enkel textredigerare.</li>
       <li>Lägg till den kopierade URL:en för videon med följande syntax så att du kan koppla den till den kopierade URL:en till din kapitelfil:<br /> <br /> <code>&navigation=<<i>full_copied_URL_path_to_chapter_file</i>.vtt></code><br /> </li>
       </ol> </td>
      </tr>
      <tr>
       <td>För en inbäddad videoupplevelse<br /> </td>
       <td>
       <ol>
       <li>Navigera till <i>publicerad </i>videoresurs som du vill associera med den kapitelfil som du har överfört. Kom ihåg att URL:er endast går att kopiera <i>efter</i> att du har <i>publicerat</i> resurserna. Se <a href="/help/assets/publishing-dynamicmedia-assets.md">Publicera resurser.</a></li>
       <li>Klicka eller tryck på i listrutan <strong>Tittare</strong>.</li>
       <li>Tryck eller klicka på förinställningsnamnet för videovisningsprogrammet i den vänstra listen. En förhandsgranskning av videon öppnas på en separat sida.</li>
       <li>Klicka på längst ned i den vänstra listen <strong>Bädda in</strong>.</li>
       <li>I dialogrutan Bädda in kod markerar och kopierar du hela koden till Urklipp och klistrar sedan in den i en enkel textredigerare.</li>
       <li>Lägg till videofilens inbäddningskod med följande syntax så att du kan koppla den till den kopierade URL:en till din kapitelfil:<br /> <br /> <code>videoViewer.setParam("navigation","&lt;<i>full_copied_URL_path_to_chapter_file</i>.vtt&gt;"</code></li>
       </ol> </td>
      </tr>
     </tbody>
   </table>

## Om videominiatyrer i Dynamic Media - Scene7-läge {#about-video-thumbnails-in-dynamic-media-scene-mode}

En videominiatyr är en version med reducerad storlek av en videobildruta eller en bildresurs som representerar videon för kunden. Miniatyrbilden får kunden att klicka på videon.

Alla videofilmer i Experience Manager måste ha en tillhörande miniatyrbild. Du kan inte ta bort en miniatyrbild utan att ersätta den. Som standard används den första bildrutan som miniatyrbild när du överför en video till Experience Manager. Du kan dock anpassa miniatyrbilden för exempelvis varumärke eller visuell sökning. När du anpassar en videominiatyr kan du spela upp videon och pausa den bildruta som du vill använda. Du kan också välja en bildresurs som du redan har överfört och *publicerad* i er Digital Asset Manager.

En anpassad videominiatyrbild som du väljer från en video extraheras inte och sparas i DAM som en separat och distinkt resurs. En anpassad videominiatyr som du väljer från en befintlig bildresurs sparas dock i JCR-filen. Sökvägen för den valda resursen lagras under videoresursens nod som i följande exempelsökväg:

`/content/dam/*<folder_name*>/<*video_name*>/jcr:content/manualThumbnail`

Möjligheten att anpassa en videominiatyr är endast tillgänglig efter att du har tillämpat en videoprofil på den mapp där videon finns.

Se även [Om videominiatyrer i Dynamic Media - hybrid-läge](#about-video-thumbnails-in-dynamic-media-hybrid-mode).

### Lägga till en anpassad videominiatyr {#adding-a-custom-video-thumbnail}

De här stegen gäller endast för Dynamic Media som körs i läget&quot;Dynamicmedia_Scene7&quot;.

**Så här lägger du till en anpassad videominiatyr:**

1. Kontrollera att du redan har gjort följande:

   * Skapade en mapp för dina videoresurser.
   * [Använda en videoprofil på mappen](/help/assets/video-profiles.md#applying-a-video-profile-to-folders).

   * [Dina videoklipp har överförts till mappen](/help/assets/managing-video-assets.md#upload-and-preview-video-assets).

1. Navigera till en överförd videoresurs vars miniatyrbild du vill ändra.
1. I resursurvalsläget antingen från **[!UICONTROL List View]** eller **[!UICONTROL Card View]**, trycker du på videoresursen.
1. Tryck på **[!UICONTROL Properties]** (en cirkel med&quot;i&quot;).
1. Tryck på på egenskapssidan för videon **[!UICONTROL Change Thumbnail]**.
1. Gör något av följande på sidan Ändra miniatyrbild:

   * Så här använder du en bildruta från videon som ny miniatyrbild:

      * Tryck på i verktygsfältet **[!UICONTROL Select Frame from video]**.
      * Tryck på uppspelningsknappen och tryck sedan på pausknappen på bildrutan som du vill spela in som videons nya miniatyrbild.
   * Så här använder du en bildresurs som ny miniatyrbild:

      * Tryck på i verktygsfältet **[!UICONTROL Select Thumbnail from Assets]**.
      * Tryck på **[!UICONTROL Select Thumbnail]**.
      * Navigera till en tidigare överförd och publicerad bildresurs som du vill använda. Resursens storlek ändras automatiskt så att den fungerar som en miniatyrbild för videon.
      * Markera bildresursen och tryck sedan på **[!UICONTROL Select]**.


1. Tryck på Ändra miniatyrbild **[!UICONTROL Save Change]**.
1. Tryck på egenskapssidan för videon i det övre högra hörnet **[!UICONTROL Save & Close]**.

## Om videominiatyrer i Dynamic Media - hybrid-läge {#about-video-thumbnails-in-dynamic-media-hybrid-mode}

Du kan välja mellan en av tio miniatyrbilder som har genererats automatiskt av Dynamic Media och lägga till dem i videon. Videospelaren visar den valda miniatyrbilden när en videoresurs används med Dynamic Media-komponenten i redigeringsmiljön i Experience Manager Sites, Experience Manager Mobile eller Experience Manager Screens. Miniatyrbilden fungerar som en statisk bild som bäst motsvarar innehållet i hela videon och uppmuntrar dessutom användarna att klicka på knappen Spela upp.

Baserat på den totala tiden för videon tar Dynamic Media tio (standard) miniatyrbilder. Bilderna spelas in i videon med 1 %, 11 %, 21 %, 31 %, 41 %, 51 %, 61 %, 71 %, 81 % och 91 %. De tio miniatyrbilderna finns kvar, vilket innebär att om du väljer en annan miniatyrbild senare behöver du inte återskapa serien. Du förhandsgranskar de tio miniatyrbilderna och väljer sedan den som du vill använda med videon. Om du vill ändra till standardvärdet kan du använda CRXDE Lite för att konfigurera det tidsintervall som miniatyrbilderna genereras i. Om du till exempel bara vill generera en serie med fyra miniatyrbilder med jämna mellanrum från videon kan du konfigurera intervalltiden till 24 %, 49 %, 74 % och 99 %.

Helst kan du lägga till en videominiatyr när som helst efter att du har överfört videon, men innan du publicerar videon på webbplatsen.

Om du vill kan du välja att överföra en anpassad miniatyrbild för videon i stället för att använda en miniatyrbild som genererats av Dynamic Media. Du kan till exempel skapa en anpassad miniatyrbild med videons titel, en iögonfallande öppningsbild eller en viss bild som hämtats från videon. Den anpassade videominiatyrbilden som du överför måste ha en maximal upplösning på 1 280 x 720 pixlar (minsta bredd på 640 pixlar) och inte vara större än 2 MB.

Se även [Om videominiatyrer i Dynamic Media - Scene7-läge](/help/assets/video.md#about-video-thumbnails-in-dynamic-media-scene-mode).

### Lägga till en videominiatyr {#adding-a-video-thumbnail}

De här stegen gäller endast för Dynamic Media som körs i hybridläge.

**Så här lägger du till en videominiatyr:**

1. Navigera till en överförd videoresurs som du vill lägga till en videominiatyr.
1. I resursurvalsläget, antingen från listvyn eller kortvyn, trycker du på videoresursen.
1. Tryck på **[!UICONTROL View Properties]** (en cirkel med&quot;i&quot;).
1. Tryck på på egenskapssidan för videon **[!UICONTROL Change Thumbnail]**.
1. På sidan Ändra miniatyrbild trycker du på **[!UICONTROL Select Frame]**.

   Dynamic Media genererar en serie miniatyrbilder från videon baserat på det standardtidsintervall eller tidsintervall som du har anpassat.

1. Förhandsgranska de genererade miniatyrbilderna och välj sedan den som du vill lägga till i videon.
1. Tryck på **[!UICONTROL Save Change]**.

   Videons miniatyrbild uppdateras till att använda den miniatyrbild du valde. Om du senare bestämmer dig för att ändra miniatyrbilden kan du gå tillbaka till **[!UICONTROL Change Thumbnail]** och välj en ny sida.

   Om du har konfigurerat nya standardtidsintervall, eller om du har överfört en ny video som ska ersätta den befintliga videon, bör du låta Dynamic Media generera om miniatyrbilderna.

   Se [Konfigurera det standardtidsintervall som videominiatyrbilder genereras](#configuring-the-default-time-interval-that-video-thumbnails-are-generated).

#### Konfigurera det standardtidsintervall som videominiatyrbilder genereras {#configuring-the-default-time-interval-that-video-thumbnails-are-generated}

När du konfigurerar och sparar det nya standardtidsintervallet gäller ändringen automatiskt endast videoklipp som du överför i framtiden. Den nya standardinställningen tillämpas inte automatiskt på videoklipp som du tidigare överfört. För befintliga videofilmer måste du återskapa miniatyrbilderna.

Se [Lägga till en videominiatyr](#adding-a-video-thumbnail).

**Så här konfigurerar du det standardtidsintervall som videominiatyrbilder genereras:**

1. I Experience Manager: tryck **[!UICONTROL Tools]** > **[!UICONTROL General]** > **[!UICONTROL CRXDE Lite]**.

1. På CRXDE Lite-sidan i katalogpanelen till vänster navigerar du till `o etc/dam/imageserver/configuration/jcr:content/settings.`

   om katalogpanelen inte visas trycker du på ikonen >> till vänster om fliken Hem.

1. Dubbeltryck på den nedre högra panelen på fliken Egenskaper `thumbnailtime`.
1. I **[!UICONTROL Edit thumbnailtime]** använder du textfälten för att ange intervallvärden som procentvärden.

   * Tryck på plustecknet (+) om du vill lägga till ett eller flera intervallvärdesfält. Om det behövs bläddrar du till dialogrutans nedre del för att se ikonen.
   * Tryck på minustecknet (-) till höger om ett intervallvärdesfält om du vill ta bort det från listan.
   * Tryck på uppilsikonen och nedpilsikonen om du vill ändra ordningen på intervallvärdena.

1. Tryck **[!UICONTROL OK]** och återgå till fliken Egenskaper.
1. I närheten av det övre vänstra hörnet på CRXDE Lite-sidan trycker du på **[!UICONTROL Save All]** och sedan trycka på ikonen Bakåt i det övre vänstra hörnet för att gå tillbaka till Experience Manager.

   Se [Lägga till en videominiatyr](#adding-a-video-thumbnail).

### Lägga till en anpassad videominiatyr {#adding-a-custom-video-thumbnail-1}

De här stegen gäller endast för Dynamic Media som körs i hybridläge.

**Så här lägger du till en anpassad videominiatyr:**

1. Navigera till en överförd videoresurs som du vill lägga till en anpassad videominiatyr.
1. I resursurvalsläget, antingen från listvyn eller kortvyn, trycker du på videoresursen.
1. Tryck på **[!UICONTROL View Properties]** (en cirkel med&quot;i&quot;).
1. Tryck på på egenskapssidan för videon **[!UICONTROL Change Thumbnail]**.
1. På sidan Ändra miniatyrbild trycker du på **[!UICONTROL Upload New Thumbnail]**.
1. Navigera till en miniatyrbild som du vill använda, markera den och tryck sedan på **[!UICONTROL Open]** för att börja överföra bilden till Experience Manager. Efter överföringen måste du publicera bilden.
1. När du har överfört och publicerat bilden trycker du på **[!UICONTROL Save Changes]**.

   Den anpassade miniatyrbilden läggs till i videon.

## Ändra Dynamic Media URL för Dynamic Media-resurser {#manifest-urls}

Videor som bearbetas till Dynamic Media kan användas i färdiga visningsprogram och även genom direktåtkomst till manifest-URL:er och uppspelning via egna visningsprogram. Nedan följer API:t för hämtning av manifest-URL:er för en video.

### Om API:t getVideoManifestURI

The `getVideoManifestURI`API exponeras via c`q-scene7-api:com.day.cq.dam.scene7.api` och kan användas för att generera följande manifest-URL:er:

```java
/**   
* Returns the manifest url for videos 
* @param resource video resource 
* @param manifestType type of video streaming manifest being requested 
* @param onlyIfPublished return a manifest only if the video is published 
* @return the manifest url for videos 
* 
* @throws Exception 
*/
@Nullable 
String getVideoManifestURI(Resource resource, ManifestType manifestType, boolean onlyIfPublished) throws Exception;
```

#### getVideoManifestURI API-parametrar

Detta API har följande tre parametrar:

| Parameter | Beskrivning |
| --- | --- |
| `resource` | Resursen som motsvarar videon som Dynamic Media har inhämtat. |
| `manifestType` | Kan vara antingen `ManifestType.DASH` eller `ManifestType.HLS` |
| `onlyIfPublished` | Ange som true om manifest-URI bara genereras om den är publicerad och tillgänglig på leveransnivån. |

Om du vill hämta manifest-URL:er för videofilmer med metoden ovan lägger du till en [videokodningsprofil](/help/assets/video-profiles.md#creating-a-video-encoding-profile-for-adaptive-streaming) till mappen&quot;upload videos&quot;. Dynamic Media bearbetar dessa videofilmer baserat på kodningarna i den videokodningsfil som tilldelats mappen. Nu kan du anropa ovanstående API för att hämta manifest-URL:er för de överförda videoklippen.

### Felscenarier

API:t returnerar null om det finns fel. Undantag loggas i felloggarna i Experience Manager. Alla sådana loggade fel börjar med `Could not generate Video Manifest URI`. Följande scenarier kan orsaka sådana fel:

* An `IllegalArgumentException` loggas för något av följande:

   * The `resource` parametern som skickades är null.
   * The `resource` Den skickade parametern är inte en video.
   * The `manifestType` parametern som skickades är null.
   * The `onlyIfPublished` -parametern skickas som true, men videon publiceras inte.
   * Videon har inte importerats med en adaptiv videouppsättning från Dynamic Media.

* `IOException` loggas när det uppstår ett problem med att ansluta till Dynamic Media.
* `UnsupportedOperationException` loggas när en `manifestType` parametern som skickas är `ManifestType.DASH`, medan videon inte har bearbetats i DASH-format.

Nedan följer ett exempel på ovanstående API med hjälp av servrar skrivna i *HTTPWhiteBoard* -specifikation. Välj varje flik för kodsyntaxen.

>[!BEGINTABS]

>[!TAB Lägg till beroende i pom.xml]

+++**Lägg till beroende i pom.xml**

```java
dependency> 
     <groupId>com.day.cq.dam</groupId> 
     <artifactId>cq-scene7-api</artifactId> 
     <version>5.12.64</version> 
     <scope>provided</scope> 
</dependency> 
```

+++

>[!TAB Exempel på serverlet]

+++**Exempel på serverlet**

```java
@Component
        service = Servlet.class 
) 
@HttpWhiteboardServletPattern(value = ManifestServlet.SERVLET_PATTERN) 
@HttpWhiteboardContextSelect(value = Constants.SERVLET_CONTEXT_SELECTOR) 
public class ManifestServlet extends HttpServlet { 

   private static final Logger LOGGER = LoggerFactory.getLogger(ManifestServlet.class); 

   private final ObjectMapper objectMapper; 

    @Reference 
    private Scene7Service scene7Service; 

   public static final String SERVLET_PATTERN = Constants.VIDEO_API_PREFIX + "/manifestUrl"; 

   public ManifestServlet() {
         this.objectMapper = new ObjectMapper(); 
         objectMapper.setSerializationInclusion(JsonInclude.Include.NON_NULL); 
   }

   @Override 

   protected void doGet(HttpServletRequest request, HttpServletResponse response) throws IOException {
        final ResourceResolver resolver = getResourceResolver(request); 
        String assetPath = request.getParameter("assetPath"); 
        String manifest = request.getParameter("manifestType"); 
        String onlyIfPublished = request.getParameter("onlyIfPublished"); 
        Resource resource = resolver.getResource(assetPath); 
        response.setCharacterEncoding(StandardCharsets.UTF_8.toString()); 
        response.setContentType("application/json"); 
        if(resource == null) { 
            LOGGER.info("could not retrieve the resource from JCR"); 
            error("could not retrieve the resource from JCR", response); 
            return; 
        }

        String manifestUri = null; 

        try{ 
            ManifestType manifestType =  ManifestType.DASH; 
            if(manifest != null) { 
                manifestType = ManifestType.valueOf(manifest); 
            } 
            manifestUri = scene7Service.getVideoManifestURI(resource, manifestType, onlyIfPublished != null); 
            objectMapper.writeValue(response.getWriter(), new ManifestUrl(manifestUri)); 
            response.setContentType("application/json"); 
        } catch (Exception e) { 
            LOGGER.error(e.getMessage(), e); 
            error(String.format("Unable to get the manifest url for %s. %s", assetPath, e.getMessage()), response); 
        } 
    } 

    private ResourceResolver getResourceResolver(HttpServletRequest request) { 
        Object rr = request.getAttribute(AuthenticationSupport.REQUEST_ATTRIBUTE_RESOLVER); 
        if (!(rr instanceof ResourceResolver)) { 
            throw new IllegalStateException( 
                    "The request does not seem to have been created via Apache Sling's authentication mechanism."); 
        } else { 
            return (ResourceResolver) rr; 
        } 
    } 

    private void error(String errorMessage, HttpServletResponse response) throws IOException { 
        ManifestUrl errorManifest = new ManifestUrl(null); 
        errorManifest.setErrorMessage(errorMessage); 
        response.setStatus(HttpServletResponse.SC_INTERNAL_SERVER_ERROR); 
        objectMapper.writeValue(response.getWriter(), errorManifest); 
    } 
} 
```

+++

>[!TAB Svarsklass för serverlet]

+++**Svarsklass för serverlet**

```java
public class ManifestUrl extends VideoResponse { 
     String manifestUrl; 
     public ManifestUrl(String manifestUrl) { 
         this.manifestUrl = manifestUrl; 
     } 
     public String getManifestUrl() { 
         return manifestUrl; 
     } 
} 

public abstract class VideoResponse { 
     String errorString; 

     public String getErrorString() { 
         return errorString; 
     } 

     public void setErrorMessage(String errorString) { 
         this.errorString = errorString; 
     } 
} 
```

+++

>[!TAB Konstanter som serverleten refererar till]

+++**Konstanter som serverleten refererar till**

```java
public final class Constants { 

     private Constants() { 
     } 

     public static final String VIDEO_API_PREFIX = "/dynamicmedia/video"; 
     public static final String SERVLET_CONTEXT_SELECTOR = "(" + HttpWhiteboardConstants.HTTP_WHITEBOARD_CONTEXT_NAME + "=" + 
             DMSampleApiHttpContext.CONTEXT_NAME + ")"; 

 } 
```

+++

>[!TAB ServletContext]

+++**ServletContext**

Montera ovanstående servett med en `servletContext`. Följande är ett exempel på `servletContext`.

```java
public class DMSampleApiHttpContext extends ServletContextHelper { 

 public static final String CONTEXT_NAME = "com.adobe.dmSample"; 
 public static final String CONTEXT_PATH = "/dmSample"; 

 private final MimeTypeService mimeTypeService; 

 private final AuthenticationSupport authenticationSupport; 

 /** 
  * Constructs a new context that will use the given dependencies. 
  * 
  * @param mimeTypeService Used when providing mime type of requests. 
  * @param authenticationSupport Used to authenticate requests with sling. 
  */ 
 @Activate 
 public DMSampleApiHttpContext(@Reference final MimeTypeService mimeTypeService, 
                               @Reference final AuthenticationSupport authenticationSupport) { 
     this.mimeTypeService = mimeTypeService; 
     this.authenticationSupport = authenticationSupport; 
 } 

 // ---------- HttpContext interface ---------------------------------------- 
 /** 
  * Returns the MIME type as resolved by the <code>MimeTypeService</code> or 
  * <code>null</code> if the service is not available. 
  */ 
 @Override 
 public String getMimeType(String name) { 
     MimeTypeService mtservice = mimeTypeService; 
     if (mtservice != null) { 
         return mtservice.getMimeType(name); 
     } 
     return null; 
 } 

 /** 
  * Returns the real context path that is used to mount this context. 
  * @param req servlet request 
  * @return the context path 
  */ 
 public static String getRealContextPath(HttpServletRequest req) { 
     final String path = req.getContextPath(); 
     if (path.equals(CONTEXT_PATH)) { 
         return ""; 
     } 
     return path.substring(CONTEXT_PATH.length()); 
 } 

 /** 
  * Returns a request wrapper that transforms the context path back to the original one 
  * @param req request 
  * @return the request wrapper 
  */ 
 public static HttpServletRequest createContextPathAdapterRequest(HttpServletRequest req) { 
     return new HttpServletRequestWrapper(req) { 

         @Override 
         public String getContextPath() { 
             return getRealContextPath((HttpServletRequest) getRequest()); 
         } 

     }; 

 } 

 /** 
  * Always returns <code>null</code> because resources are all provided 
  * through individual endpoint implementations. 
  */ 
 @Override 
 public URL getResource(String name) { 
     return null; 
 } 

 /** 
  * Tries to authenticate the request using the 
  * <code>SlingAuthenticator</code>. If the authenticator or the Repository 
  * is missing this method returns <code>false</code> and sends a 503/SERVICE 
  * UNAVAILABLE status back to the client. 
  */ 
 @Override 
 public boolean handleSecurity(HttpServletRequest request, 
                               HttpServletResponse response) throws IOException { 

     final AuthenticationSupport authenticator = this.authenticationSupport; 
     if (authenticator != null) { 
         return authenticator.handleSecurity(createContextPathAdapterRequest(request), response); 
     } 

     // send 503/SERVICE UNAVAILABLE, flush to ensure delivery 
     response.sendError(HttpServletResponse.SC_SERVICE_UNAVAILABLE, 
             "AuthenticationSupport service missing. Cannot authenticate request."); 
     response.flushBuffer(); 

     // terminate this request now 
     return false; 
 } 
}
```

+++

>[!ENDTABS]

### Använda exempelservleten

Du anropar servern genom att utföra en `GET` operation at `/dmSample/dynamicmedia/video/manifestUrl`. Följande frågeparametrar skickas:

| Frågeparameter | Beskrivning |
| --- | --- |
| `assetPath` | Obligatoriskt. Sökvägen till videon som `manifestUrl` genereras. |
| `manifestType` | Valfritt. Parametern kan vara DASH eller HLS. Om det inte skickas blir standardvärdet DASH. |
| `onlyIfPublished` | Valfritt. Om det skickas `manifestUrl` returneras bara om videon publiceras. |

I det här exemplet antar vi följande inställningar:

* Företaget är `samplecompany`.
* Redigeringsinstansen är `http://sample-aem-author.com`.
* Mappen `/content/dam/video-example` har en videokodningsprofil tillämpad på den.
* Videon `scenery.mp4` överförs till mappen `/content/dam/video-example`.

Du kan anropa servleten på följande sätt:

| Typ | Beskrivning |
| :--- | --- |
| HLS | `http://sample-aem-author.com/dmSample/dynamicmedia/video/manifestUrl?manifestType=HLS&assetPath=/content/dam/video-example/scenery.mp4`<br><br>Om DASH-leverans är aktiverad:<br>`{"manifestUrl":"https://s7d1.scene7.com/is/content/samplecompany/scenery-AVS.m3u8?packagedStreaming=true"}`<br><br>Om DASH-leverans är inaktiverad:<br>`{"manifestUrl":"https://s7d1.scene7.com/is/content/samplecompany/scenery-AVS.m3u8"}` |
| DASH | `http://sample-aem-author.com/dmSample/dynamicmedia/video/manifestUrl?manifestType=DASH&assetPath=/content/dam/video-example/scenery.mp4`<br><br>Om DASH-leverans är aktiverad:<br>`{"manifestUrl":"https://s7d1.scene7.com/is/content/samplecompany/scenery-AVS.mpd"}`<br><br>Om DASH-leverans är inaktiverad:<br>`{}` |
| Fel: resurssökvägen är felaktig | `http://sample-aem-author.com/dmSample/dynamicmedia/video/manifestUrl?manifestType=DASH&assetPath=/content/dam/video-example/scennnnnnery.mp4`<br><br>`{"errorString":"could not retrieve the resource from JCR"}` |


