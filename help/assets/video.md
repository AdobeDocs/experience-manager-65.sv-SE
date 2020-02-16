---
title: Video
description: Lär dig hur du arbetar med video i Dynamic Media
uuid: 97f311a3-a227-479a-91bf-fb54ecd1a55d
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: 1103b849-0042-4e11-b170-38ee81dd0157
docset: aem65
translation-type: tm+mt
source-git-commit: 569c552686e6312ecae0d500147a8b65354c303d

---


# Video {#video}

I det här avsnittet beskrivs hur du arbetar med video i Dynamic Media.

## Snabbstart: Videor {#quick-start-videos}

Följande steg-för-steg-beskrivning av arbetsflödet hjälper dig att komma igång snabbt med anpassningsbara videouppsättningar i Dynamic Media. Efter varje steg finns korsreferenser till ämnesrubriker där du kan hitta mer information.

>[!NOTE]
>
>Innan du arbetar med video i Dynamic Media måste du kontrollera att AEM-administratören redan har aktiverat och konfigurerat Dynamic Media Cloud Services i läget Dynamic Media - Scene7 eller Dynamic Media - Hybrid.
>
>* Se [Konfigurera Dynamic Media Cloud-tjänster](/help/assets/config-dms7.md#configuring-dynamic-media-cloud-services) i Konfigurera Dynamic Media - Scene7-läge och [Felsökning av Dynamic Media - Scene7-läge.](/help/assets/troubleshoot-dms7.md)
   >
   >
* Se [Konfigurera Dynamic Media Cloud-tjänster](/help/assets/config-dynamic.md#configuring-dynamic-media-cloud-services) i Konfigurera Dynamic Media - hybrid-läge.
>



1. **Ladda upp dina dynamiska medievideor** genom att göra följande:

   * Skapa en egen videokodningsprofil. Du kan också helt enkelt använda den fördefinierade _adaptiva videokodningsprofilen_ som medföljer Dynamic Media.

      * [Skapa en videokodningsprofil](/help/assets/video-profiles.md#creating-a-video-encoding-profile-for-adaptive-streaming).
      * Läs mer om [Bästa tillvägagångssätt för videokodning](#best-practices-for-encoding-videos).
   * Koppla videobearbetningsprofilen till en eller flera mappar där du ska överföra dina mastervideor.

      * [Tillämpa en videoprofil på mappar](/help/assets/video-profiles.md#applying-a-video-profile-to-folders).
      * Läs mer om [de bästa sätten att ordna digitala resurser för bearbetning av profiler](/help/assets/organize-assets.md).
      * Läs mer om [att ordna digitala resurser](/help/assets/organize-assets.md).
   * Överför dina huvudvideor till mapparna. Du kan överföra videofiler på upp till 20 GB vardera. När du lägger till videofilmer i mappen kodas de enligt den videobearbetningsprofil som du tilldelade mappen.

      * [Ladda upp videor](/help/assets/managing-video-assets.md#uploadingandpreviewingvideoassets).
      * Läs mer om [indatafilformat](/help/assets/assets-formats.md#supported-multimedia-formats)som stöds.
   * Övervaka hur [videokodningen fortskrider](#monitoring-video-encoding-and-youtube-publishing-progress) antingen från resursen eller arbetsflödesvyn.




1. **Hantera dina dynamiska medievideor** genom att göra något av följande:

   * Ordna, bläddra bland och söka efter videomaterial

      * [Organisera digitalt material](/help/assets/organize-assets.md)Läs mer om [Bästa metoder för att ordna digitala resurser för att använda bearbetningsprofiler](organize-assets.md)

      * [Söka efter videomaterial](search-assets.md#custompredicates) eller [söka resurser](managing-assets-touch-ui.md#search-assets)
   * Förhandsgranska och publicera videomaterial

      * Visa källvideon och de kodade återgivningarna av videon tillsammans med tillhörande miniatyrer:
         [Förhandsgranska videoklipp](managing-video-assets.md#upload-and-preview-video-assets) eller [förhandsgranska resurser](previewing-assets.md)
         [Visa videoåtergivningar](video-renditions.md)
         [Hantera videoåtergivningar](managing-assets-touch-ui.md#managing-renditions)

      * [Hantera förinställningar för visningsprogram](managing-viewer-presets.md)
      * [Publicera resurser](publishing-dynamicmedia-assets.md)
   * Arbeta med videometadata

      * Visa egenskaperna för en kodad videoåtergivning, t.ex. bildrutefrekvens, ljud- och videobithastighet samt kodek:
         [Visa egenskaper för videoåtergivning](video-renditions.md)

      * Redigera egenskaperna för video, till exempel titel, beskrivning och taggar, anpassade metadatafält:
         [Redigera videoegenskaper](managing-assets-touch-ui.md#editing-properties)

      * [Hantera metadata för digitala resurser](metadata.md)
      * [Metadata-scheman](metadata-schemas.md)
   * Granska, godkänn och kommentera videoklipp och behåll fullständig versionskontroll

      * [Anteckna videoklipp](managing-video-assets.md#annotate-video-assets) eller [anteckningsresurser](managing-assets-touch-ui.md#annotating)

      * [Skapa en version](managing-assets-touch-ui.md#asset-versioning)
      * [Tillämpa arbetsflöden på resurser](assets-workflow.md) eller se [Starta ett arbetsflöde på en resurs](managing-assets-touch-ui.md#starting-a-workflow-on-an-asset)

      * [Granska mappresurser](bulk-approval.md)
      * [Projekt](../sites-authoring/projects.md)




1. **Publicera dina Dynamic Media-videor** genom att göra något av följande:

   * Om du använder Adobe Experience Manager som webbinnehållshanteringssystem kan du lägga till videofilmer direkt på dina webbsidor.

      * [Lägga till videoklipp på webbsidor](adding-dynamic-media-assets-to-pages.md).
   * Om du använder ett webbinnehållshanteringssystem från en annan leverantör kan du länka eller bädda in videor på dina webbsidor.

      * Integrera video med URL:
         [Länka URL:er till webbprogrammet](linking-urls-to-yourwebapplication.md).

      * Integrera video med inbäddad kod på webbsidan:
         [Bädda in videovisningsprogrammet på en webbsida](embed-code.md).
   * [Publicera videor på YouTube](#publishing-videos-to-youtube).
   * [Genererar videorapporter](#viewing-video-reports).

   * [Lägga till bildtexter i videon](#adding-captions-to-video).



## Arbeta med video i Dynamic Media {#working-with-video-in-dynamic-media}

Video in Dynamic Media är en totallösning som gör det enkelt att publicera högkvalitativ adaptiv video för direktuppspelning på flera skärmar, inklusive datorer, iOS, Android, Blackberry och Windows-enheter. En adaptiv videouppsättning grupperar versioner av samma video som är kodade med olika bithastigheter och format som 400 kbit/s, 800 kbit/s och 1 000 kbit/s. Den stationära datorn eller mobila enheten känner av den tillgängliga bandbredden.

På en iOS-mobil enhet upptäcker den till exempel en bandbredd som 3G, 4G eller Wi-Fi. Sedan väljs automatiskt rätt kodad video bland de olika videobithastigheterna i den adaptiva videouppsättningen. Videon strömmas till datorer, mobila enheter eller surfplattor.

Dessutom ändras videokvaliteten dynamiskt automatiskt om nätverksförhållandena ändras på datorn eller den mobila enheten. Om en kund går över till helskärmsläge på en stationär dator svarar den adaptiva videouppsättningen med en bättre upplösning, vilket förbättrar kundens tittarupplevelse. Med adaptiva videouppsättningar får du bästa möjliga uppspelning för kunder som spelar upp Dynamic Media-video på flera skärmar och enheter.

Den logik som en videospelare använder för att avgöra vilken kodad video som ska spelas upp eller väljas under uppspelningen baseras på följande algoritm:

1. Videospelaren läser in det inledande videofragmentet baserat på den bithastighet som ligger närmast värdet som är inställt för&quot;inledande bithastighet&quot; i spelaren.
1. Videospelaren växlar baserat på ändringar av bandbreddshastigheten med följande kriterier:

   1. Spelaren väljer den högsta bandbreddsströmmen under eller lika med den beräknade bandbredden.
   1. Spelaren hanterar bara 80 % av den tillgängliga bandbredden. Men om den byter upp sig är det mer försiktigt med bara 70 % för att undvika överskattning och omedelbart gå tillbaka.

Detaljerad teknisk information om algoritmen finns på [https://android.googlesource.com/platform/frameworks/av/+/master/media/libstagefright/httplive/LiveSession.cpp](https://android.googlesource.com/platform/frameworks/av/+/master/media/libstagefright/httplive/LiveSession.cpp)

Följande stöds för hantering av enstaka video och adaptiva videouppsättningar:

* Överföra video från ett antal videoformat och ljudformat som stöds och koda video till MP4 H.264-format för uppspelning på flera skärmar. Du kan använda fördefinierade adaptiva videoförinställningar, enskilda videokodningsförinställningar eller anpassa din egen kodning för att styra videons kvalitet och storlek.

   * När en adaptiv videouppsättning genereras innehåller den MP4-videor.
   * **Obs**: Huvud-/källvideor läggs inte till i en adaptiv videouppsättning.

* Videobildtext i alla HTML5-videovisningsprogram.
* Ordna, bläddra bland och sök videoklipp med fullt stöd för metadata för effektiv hantering av videomaterial.
* Leverera adaptiva videouppsättningar till webben, datorer och mobila enheter som iPhone, iPad, Android, Blackberry och Windows Phone.

Adaptiv videoströmning stöds på flera olika iOS-plattformar. Se [Referenshandbok](https://marketing.adobe.com/resources/help/en_US/s7/viewers_ref/c_html5_video_reference.html)för Scene7-visningsprogram.

Dynamic Media har stöd för videouppspelning i mobiler för MP4 H.264-video. Du kan hitta Blackberry-enheter som stöder det här videoformatet på följande sätt: Videoformat [som stöds på Blackberry](https://support.blackberry.com/kb/articleDetail?ArticleNumber=000005482).

Windows-enheter som stöder det här videoformatet finns på följande plats: Videoformat [som stöds på Windows Phone](https://msdn.microsoft.com/library/windows/apps/ff462087%28v=vs.105%29.aspx)

* Spela upp videon med Dynamic Media Video Viewer Presets, inklusive följande:

   * Enstaka videovisningsprogram.
   * Visningsprogram för blandade media som kombinerar både video- och bildinnehåll.

* Konfigurera videospelare för att tillgodose era varumärkesbehov.
* Integrera video på webbplatsen, mobilsajten eller mobilapplikationen med en enkel URL eller inbäddningskod.

Se Exempel på [dynamisk](https://s7d9.scene7.com/s7/uvideo.jsp?asset=GeoRetail/Mop_AVS&config=GeoRetail/Universal_Video1&stageSize=640,480) videouppspelning.

Se även [visningsprogram för AEM och Scene7](https://marketing.adobe.com/resources/help/en_US/s7/viewers_ref/c_html5_s7_aem_asset_viewers.html) och [visningsprogram för AEM-resurser endast](https://marketing.adobe.com/resources/help/en_US/s7/viewers_ref/c_html5_aem_asset_viewers.html) i referenshandboken för Adobe Scene7-visningsprogram.

## Bästa praxis: Använda videovisningsprogrammet för HTML5 {#best-practice-using-the-html-video-viewer}

Förinställningarna för visningsprogrammet för Dynamic Media HTML5-video är robusta videospelare. Du kan använda dem för att undvika många vanliga problem som är kopplade till videouppspelning i HTML5 och problem som är kopplade till mobila enheter, som brist på adaptiv strömning och begränsad webbläsarräckvidd för stationära datorer.

På designsidan av spelaren kan du utforma alla videospelarens funktioner med standardverktyg för webbutveckling. Du kan till exempel utforma knappar, kontroller och anpassad förhandsgranskningsbildbakgrund med HTML5 och CSS så att du kan nå dina kunder med ett anpassat utseende.

På visningsprogrammets uppspelningssida identifieras webbläsarens videokapacitet automatiskt. Sedan visas videon med HLS (HTTP Live Streaming), som också kallas adaptiv videoströmning. Om leveransmetoderna saknas används i stället HTML5 progressiv.

Genom att i en enda spelare kombinera möjligheten att utforma uppspelningskomponenterna med HTML5 och CSS, ha inbäddad uppspelning och använda adaptiv och progressiv strömning beroende på webbläsarens kapacitet, kan du utöka räckvidden för ditt multimedieinnehåll till både dator- och mobilanvändare och säkerställa en smidig videoupplevelse.

Se även [Om HTML5-visningsprogram](https://marketing.adobe.com/resources/help/en_US/s7/viewers_ref/c_html5_viewers_about.html) i referenshandboken för Adobe Scene7-visningsprogram.

### Uppspelning av video på stationära datorer och mobila enheter med HTML5-videovisningsprogrammet {#playback-of-video-on-desktop-computers-and-mobile-devices-using-the-html-video-viewer}

För strömning av anpassningsbara video för datorer och mobilenheter baseras de videor som används för växling av bithastighet på alla MP4-videor i den adaptiva videouppsättningen.

Videouppspelning sker med HLS eller progressiv videohämtning. I tidigare versioner av AEM, som 6.0, 6.1 och 6.2, strömmades videor via HTTP.

I AEM 6.3 och senare direktuppspelas videor nu via HTTPS (dvs. HLS) eftersom DM-gatewaytjänstens URL alltid använder HTTPS. Observera att det här standardbeteendet inte påverkar kunderna. Det innebär att direktuppspelning av video alltid sker via HTTPS, såvida det inte stöds av webbläsaren. (se följande tabell). Därför returnerar

* Om du har en HTTPS-webbplats med HTTPS-videoströmning går det bra att strömma.
* Om du har en HTTP-webbplats med HTTPS-videoströmning går det bra att strömma och det finns inga blandade innehållsproblem i webbläsaren.

HLS är en Apple-standard för adaptiv videoströmning som automatiskt justerar uppspelningen baserat på nätverkets bandbreddskapacitet. Man kan också &quot;söka&quot; till valfri punkt i videon utan att behöva vänta på att resten av videon ska laddas ned.

Progressiv video levereras genom att videon hämtas och lagras lokalt på en användares dator eller mobila enhet.

I följande tabell beskrivs enheten, webbläsaren och uppspelningsmetoden för videoklipp på stationära datorer och mobila enheter med Scene7 Video Viewer.

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
   <td>I Windows 8 och Windows 10 - Tvinga användning av HTTPS när HLS begärs. Känd begränsning: HTTP på HLS fungerar inte i den här kombinationen<br /> av webbläsare/operativsystem <br /> i Windows 7 - progressiv nedladdning. Använder standardlogik för att välja HTTP- eller HTTPS-protokoll.</td>
  </tr>
  <tr>
   <td>Skrivbord</td>
   <td>Firefox 23-44</td>
   <td>Progressiv nedladdning.</td>
  </tr>
  <tr>
   <td>Skrivbord</td>
   <td>Firefox 45 eller senare</td>
   <td>HLS</td>
  </tr>
  <tr>
   <td>Skrivbord</td>
   <td>Krom</td>
   <td>HLS</td>
  </tr>
  <tr>
   <td>Skrivbord</td>
   <td>Safari (Mac)</td>
   <td>HLS</td>
  </tr>
  <tr>
   <td>Mobil</td>
   <td>Chrome (Android 6 eller tidigare)</td>
   <td>Progressiv nedladdning.</td>
  </tr>
  <tr>
   <td>Mobil</td>
   <td>Chrome (Android 7 eller senare)</td>
   <td>HLS</td>
  </tr>
  <tr>
   <td>Mobil</td>
   <td>Android (standardwebbläsare)</td>
   <td>Progressiv nedladdning.</td>
  </tr>
  <tr>
   <td>Mobil</td>
   <td>Safari (iOS)</td>
   <td>HLS</td>
  </tr>
  <tr>
   <td>Mobil</td>
   <td>Chrome (iOS)</td>
   <td>HLS</td>
  </tr>
  <tr>
   <td>Mobil</td>
   <td>Blackberry</td>
   <td>HLS</td>
  </tr>
 </tbody>
</table>

## Arkitektur för Dynamic Media Video Solution {#architecture-of-dynamic-media-video-solution}

Följande bild visar det övergripande arbetsflödet för redigering av videoklipp som har överförts och kodats med hjälp av DMGGateway (i Dynamic Media Hybrid-läge) och som har gjorts tillgängliga för offentlig användning.

![chlimage_1-427](assets/chlimage_1-427.png)

## Hybrid publiceringsarkitektur för videor {#hybrid-publishing-architecture-for-videos}

![chlimage_1-428](assets/chlimage_1-428.png)

## Bästa tillvägagångssätt för att koda videofilmer {#best-practices-for-encoding-videos}

Arbetsflödet **Dynamic Media Encode Video** kodar video om du har aktiverat dynamiska media och konfigurerat videolmolntjänster. Det här arbetsflödet innehåller information om arbetsflödets processhistorik och fel. Se [Övervaka videokodning och Publiceringsförloppet](#monitoring-video-encoding-and-youtube-publishing-progress)på YouTube. Om du har aktiverat dynamiska media och konfigurerat videolmolntjänster börjar arbetsflödet för **[!UICONTROL dynamisk Media Encode-video]** automatiskt att gälla när du överför en video. (Om du inte använder dynamiska medier träder arbetsflödet för **[!UICONTROL DAM-uppdatering av resurser]** i kraft.)

Nedan följer några tips om hur du kodar källvideofiler.

Mer information om videokodning finns i:

* [Direktuppspelning 101: Grundläggande - kodekar, bandbredd, datahastighet och upplösning](https://www.adobe.com/go/learn_s7_streaming101_en).
* [Grunderna](https://www.adobe.com/go/learn_s7_encoding_en)i videokodning.

### Källvideofiler {#source-video-files}

När du kodar en videofil ska du använda en källvideofil med högsta möjliga kvalitet. Undvik att använda tidigare kodade videofiler eftersom dessa filer redan är komprimerade, och ytterligare kodning skapar en video med delkvalitet.

I följande tabell beskrivs rekommenderad storlek, proportioner och lägsta bithastighet som källvideofilerna ska ha innan du kodar dem:

| Storlek | Proportioner | Minsta bithastighet |
|--- |--- |--- |
| 1024 x 768 | 4:3 | 4 500 kbit/s för de flesta videoklipp. |
| 1280 x 720 | 16:9 | 3 000 - 6 000 kbit/s, beroende på mängden rörelse i videon. |
| 1920 x 1080 | 16:9 | 6000 - 8 000 kbit/s, beroende på mängden rörelse i videon. |

### Hämta metadata för en fil {#obtaining-a-file-s-metadata}

Du kan hämta metadata för en fil genom att visa dess metadata med ett videoredigeringsverktyg eller med ett program som utformats för att hämta metadata. Nedan följer instruktioner om hur du använder MediaInfo, ett tredjepartsprogram, för att hämta videofilens metadata:

1. Gå till den här webbsidan: [https://mediainfo.sourceforge.net/en/Download](https://mediainfo.sourceforge.net/en/Download).
1. Välj och hämta installationsprogrammet för den grafiska användargränssnittsversionen och följ installationsanvisningarna.
1. Efter installationen högerklickar du på videofilen (endast Windows) och väljer MediaInfo, eller öppnar MediaInfo och drar videofilen till programmet. Alla metadata som är associerade med videofilen, inklusive bredd, höjd och fps, visas.

### Proportioner {#aspect-ratio}

När du väljer eller skapar en förinställning för videokodning för huvudvideofilen måste du se till att förinställningen har samma proportioner som huvudvideofilen. Proportionerna är proportionerna mellan videons bredd och höjd.

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

* **[!UICONTROL Konstant bithastighetskodning]** (CBR) - Under CBR-kodning är bithastigheten eller antalet bitar per sekund densamma under hela kodningsprocessen. CBR-kodning bevarar den angivna datahastigheten enligt inställningen för hela videon. CBR-kodning optimerar inte heller mediefiler för kvalitet utan sparar på lagringsutrymmet.
Använd CBR om videon innehåller en liknande rörelsenivå i hela videon. CBR används oftast för direktuppspelat videoinnehåll. Se även [Använda egna videokodningsparametrar](/help/assets/video-profiles.md#using-custom-added-video-encoding-parameters).

* **[!UICONTROL VBR-kodning (Variable Bitrate Encoding]** ) - VBR-kodning justerar datahastigheten nedåt och till den övre gräns du anger, baserat på de data som krävs av kompressorn. Detta innebär att under en VBR-kodningsprocess ökar eller minskar bithastigheten för mediefilen dynamiskt beroende på mediefilens behov av bithastighet.
VBR tar längre tid att koda men ger det mest fördelaktiga resultatet. mediefilens kvalitet är överlägsen. VBR används oftast för http-progressiv leverans av videoinnehåll.

När ska du använda VBR jämfört med CRB?
När det gäller att välja VBR eller CBR rekommenderar vi nästan alltid att du använder VBR för dina mediefiler. VBR ger filer av högre kvalitet med konkurrenskraftiga bithastigheter. När du använder VBR måste du vara säker på att du använder kodning i två omgångar och ställa in den maximala bithastigheten till 1,5 gånger målvideobithastigheten.

När du väljer en förinställning för videokodning ska du ta hänsyn till slutanvändarens anslutningshastighet. Välj en förinställning med en datahastighet som är 80 % av den hastigheten. Om målanvändarens anslutningshastighet till exempel är 1 000 kbit/s är den bästa förinställningen en med en videodatahastighet på 800 kbit/s.

I den här tabellen beskrivs datahastigheten för typiska anslutningshastigheter.

| Hastighet (kbit/s) | Anslutningstyp |
|--- |--- |
| 256 | Uppringd anslutning. |
| 800 | Vanlig mobilanslutning. För den här anslutningen anger du en datahastighet mellan 400 och maximalt 800 för 3G-upplevelser som mål. |
| 2000 | Vanlig anslutning till stationär bredbandsuppkoppling. För den här anslutningen anger du en datahastighet i intervallet 800-2000 kbit/s med de flesta mål som är i genomsnitt 1200-1500 kbit/s. |
| 5000 | Vanlig bredbandsanslutning. Kodning i det här övre intervallet rekommenderas inte eftersom videoleverans i den här hastigheten inte är tillgänglig för de flesta konsumenter. |

### Upplösning {#resolution}

**Upplösning **beskriver en videofils höjd och bredd i pixlar. Den mesta källvideon lagras med hög upplösning (till exempel 1 920 x 1 080). Vid direktuppspelning komprimeras källvideo till en lägre upplösning (640 x 480 eller lägre).

Upplösning och datahastighet är två sammankopplade faktorer som avgör videokvaliteten. Om du vill behålla samma videokvalitet måste datahastigheten vara högre ju fler pixlar en videofil har (ju högre upplösning). Ta till exempel antalet pixlar per bildruta i en 320 x 240-upplösning och en 640 x 480-upplösningsvideofil:

| Upplösning | Pixlar per bildruta |
|--- |--- |
| 320 x 240 | 76,800 |
| 640 x 480 | 307,200 |

Filen på 640 x 480 har fyra gånger fler pixlar per bildruta. För att uppnå samma datahastighet för dessa två exempelupplösningar tillämpar du fyra gånger komprimeringen på 640 x 480-filen, vilket kan minska videons kvalitet. En videodatahastighet på 250 kbit/s ger därför en högkvalitativ bild med upplösningen 320 x 240, men inte med upplösningen 640 x 480.

I allmänhet gäller att ju högre datahastighet du använder, desto bättre utseende ser videon ut och ju högre upplösning du använder, desto högre datahastighet behöver du för att upprätthålla visningskvaliteten (jämfört med lägre upplösningar).

Eftersom upplösning och datahastighet är länkade finns det två alternativ när du kodar video:

* Välj en datahastighet och koda sedan med den högsta upplösningen som ser bra ut med den datahastighet du väljer.
* Välj en upplösning och koda sedan med den datahastighet som krävs för att få en video med hög kvalitet med den upplösning du väljer.

När du väljer (eller skapar) en förinställning för videokodning för huvudvideofilen använder du den här tabellen för att ange rätt upplösning:

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

Välj en förinställning för videokodning som matchar fps-hastigheten för huvudvideofilen. Om huvudvideon till exempel är 25 fps väljer du en kodningsförinställning med 25 fps. Som standard används mastervideofilens fps för all anpassad kodning. Därför behöver du inte uttryckligen ange fps-inställningen när du skapar en förinställning för videokodning.

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

## Publicera videor på YouTube {#publishing-videos-to-youtube}

Du kan publicera lokala AEM-videor direkt till en YouTube-kanal som du tidigare har skapat.

Om du vill publicera videomaterial på YouTube skapar du AEM Assets med taggar. Du kopplar dessa taggar till en YouTube-kanal. Om taggen för en videoresurs matchar taggen för en YouTube-kanal publiceras videon på YouTube. Publicera på YouTube sker tillsammans med en normal publicering av videon så länge som en associerad tagg används.

YouTube gör sin egen kodning. Den ursprungliga videofilen som överfördes till AEM publiceras på YouTube i stället för en videoåtergivning som Dynamic Medias kodning har skapat. Även om det inte krävs för att bearbeta videofilmer med Dynamic Media, förväntas de göra det om en visningsförinställning behövs för uppspelning.

När du åsidosätter videobearbetningsprofilen och publicerar direkt på YouTube innebär det helt enkelt att din videoresurs i AEM Asset kanske inte får en miniatyrbild som kan visas. Det innebär också att om du kör i körningslägena dynamicmedia eller dynamicmedia_scene7 kommer videor som inte är kodade inte att fungera med någon av resurstyperna för Dynamic Media.

När du publicerar videomaterial till YouTube-servrar utför du följande uppgifter för att säkerställa säker server-till-server-autentisering med YouTube:

1. [Konfigurera inställningar för Google Cloud](#configuring-google-cloud-settings)
1. [Skapa en YouTube-kanal](#creating-a-youtube-channel)
1. [Lägga till taggar för publicering](#adding-tags-for-publishing)
1. [Aktivera YouTube Publish Replication Agent](#enabling-the-youtube-publish-replication-agent)
1. [Konfigurera YouTube i AEM](#setting-up-youtube-in-aem)
1. [(Valfritt) Automatisera inställningen av YouTube-standardegenskaper för dina överförda videofilmer](#optional-automating-the-setting-of-default-youtube-properties-for-your-uploaded-videos)
1. [Publicera videor i din YouTube-kanal](#publishing-videos-to-your-youtube-channel)
1. [(Valfritt) Verifiera den publicerade videon på YouTube](/help/assets/video.md#optional-verifying-the-published-video-on-youtube)
1. [Länka YouTube-URL:er till ditt webbprogram](#linking-youtube-urls-to-your-web-application)

Du kan också [avpublicera videoklipp för att ta bort dem från YouTube](#unpublishing-videos-to-remove-them-from-youtube).

### Konfigurera inställningar för Google Cloud {#configuring-google-cloud-settings}

För att kunna publicera på YouTube behöver du ett Google-konto. Om du har ett GMAIL-konto har du redan ett Google-konto; Om du inte har något Google-konto kan du enkelt skapa ett. Du behöver kontot eftersom du behöver inloggningsuppgifter för att publicera videoresurser på YouTube. Om du redan har skapat ett konto hoppar du över den här uppgiften och fortsätter direkt till [Skapa en YouTube-kanal](#creating-a-youtube-channel).

Kontot som används med Google Cloud och Google-kontot som används för YouTube behöver inte vara samma.

Tänk på att Google regelbundet ändrar användargränssnittet. Stegen för att publicera videor på YouTube kan därför variera något från vad som beskrivs nedan. Denna caveat gäller även YouTube när du försöker kontrollera om videoklipp har överförts till den.

>[!NOTE]
>
>Följande steg var korrekta när detta skrevs. Google uppdaterar dock regelbundet sina webbplatser utan föregående meddelande. De här stegen kan därför vara något annorlunda.

Så här konfigurerar du Google Cloud-inställningar:

1. Skapa ett nytt Google-konto.
   [https://accounts.google.com/SignUp?service=mail](https://accounts.google.com/SignUp?service=mail)

   Om du redan har ett Google-konto går du vidare till nästa steg.

1. Gå till [https://cloud.google.com/](https://cloud.google.com/).
1. På Google Cloud-sidan, nära det övre högra hörnet, klickar du på **[!UICONTROL Konsol]**.

   Om det behövs kan du behöva **[!UICONTROL logga in]** med inloggningsuppgifterna för ditt Google-konto för att se alternativet **[!UICONTROL Konsol]** .

1. Klicka på listrutan Projekt till höger om **[!UICONTROL Google Cloud Platform]** på sidan Kontrollpanel för att öppna dialogrutan Välj ett projekt.
1. Tryck på **[!UICONTROL Nytt projekt]** i dialogrutan Välj ett projekt.

   ![6_5_googleaccount-newproject](assets/6_5_googleaccount-newproject.png)

1. Skriv namnet på det nya projektet i fältet Projektnamn i dialogrutan Nytt projekt.

   Observera att ditt projekt-ID baseras på ditt projektnamn. Välj projektnamnet noggrant. den kan inte ändras efter att den har skapats. Du måste även ange samma projekt-ID igen när du konfigurerar YouTube i AEM senare den; kanske du vill skriva ner det.

1. Klicka på **[!UICONTROL Skapa]**.

1. Gör något av följande:

   * På ditt projekts Dashboard går du till kortet Komma igång och trycker på **[!UICONTROL Utforska och aktiverar API:er]**.
   * I Dashboard för projektet trycker du på **[!UICONTROL Gå till API:er-översikt]** på API:n på API:kortet.
   ![6_5_googleaccount-apis-enable2](assets/6_5_googleaccount-apis-enable2.png)

1. I början av sidan API:er och tjänster trycker du på **[!UICONTROL Aktivera API:er och tjänster]**.
1. Tryck på **[!UICONTROL YouTube]** på sidan API-bibliotek på vänster sida under **[!UICONTROL Kategori]**. Tryck på **[!UICONTROL YouTube Data API]** till höger på sidan.
1. Tryck på **[!UICONTROL Aktivera]** på YouTube Data API v3-sidan.

   ![6_5_googleaccount-apis-enable3](assets/6_5_googleaccount-apis-enable3.png)

1. Om du vill använda API:t kan du behöva inloggningsuppgifter. Om det behövs klickar du på **[!UICONTROL Skapa autentiseringsuppgifter]**.

   ![6_5_googleaccount-apis-createcredentials](assets/6_5_googleaccount-apis-createcredentials.png)

1. Gör följande på sidan **[!UICONTROL Lägg till inloggningsuppgifter till projektsidan]** , steg 1:

   * Från **[!UICONTROL Vilket API använder du?]** väljer du **[!UICONTROL YouTube Data API v3]**.

   * Från **[!UICONTROL Var ska du ringa API:t från?]** nedrullningsbar lista, välj **[!UICONTROL Webbserver (t.ex. node.js, Tomcat)]**

   * Från **[!UICONTROL Vilka data ska du komma åt?]** i den nedrullningsbara listan trycker du på **[!UICONTROL Användardata]**.
   ![6_5_googleaccount-apis-createcredentials2](assets/6_5_googleaccount-apis-createcredentials2.png)

1. Tryck på **[!UICONTROL Vilka autentiseringsuppgifter behöver jag?]**
1. På sidan **[!UICONTROL Lägg till inloggningsuppgifter till ditt projekt]** , steg 2, under rubriken **[!UICONTROL Skapa ett OAuth 2.0-klient-ID]** , i fältet Namn, anger du ett unikt namn om så önskas. Du kan också använda standardnamnet som anges av Google.
1. Under rubriken **[!UICONTROL Authorized Javascript origin]** anger du följande sökväg i textfältet, ersätter din egen domän och portnummer i sökvägen och trycker sedan på **[!UICONTROL Retur]** för att lägga till sökvägen i listan:

   `https://<servername.domain>:<port_number>`

   Exempel, `https://1a2b3c.mycompany.com:4321`

   **Obs**: Banexemplet ovan är endast avsett för illustrationsändamål.

   ![6_5_googleaccount-apis-createcredentials-oauth](assets/6_5_googleaccount-apis-createcredentials-oauth.png)

1. Under rubriken **[!UICONTROL Godkända omdirigerings-URI:er]** anger du följande sökväg i textfältet, ersätter din egen domän och portnummer i sökvägen och trycker sedan på **[!UICONTROL Retur]** för att lägga till sökvägen i listan:

   `https://<servername.domain>:<port_number>/etc/cloudservices/youtube.youtubecredentialcallback.json`

   Exempel, `https://1a2b3c.mycompany.com:4321/etc/cloudservices/youtube.youtubecredentialcallback.json`

   **Obs**: Banexemplet ovan är endast avsett för illustrationsändamål.

1. Klicka på **[!UICONTROL Skapa OAuth-klient-ID]**.
1. På sidan **[!UICONTROL Lägg till inloggningsuppgifter till ditt projekt]** , steg 3, under rubriken **** Konfigurera OAuth 2.0-medgivande, väljer du den Gmail-e-postadress som du använder för närvarande.

   ![6_5_googleaccount-apis-createcredentials-consentscreen](assets/6_5_googleaccount-apis-createcredentials-consentscreen.png)

1. Under **[!UICONTROL Produktnamnet som visas för användarna]** , i textfältet, anger du vad du vill visa på godkännandeskärmen.

   Medgivandeskärmen visas för AEM-administratören när de autentiserar på YouTube. AEM kontaktar YouTube för tillstånd.

1. Klicka på **[!UICONTROL Fortsätt]**.
1. Gå till sidan Lägg till inloggningsuppgifter för ditt projekt, steg 4, tryck på **[!UICONTROL Hämta]** under rubriken **[!UICONTROL Hämta inloggningsuppgifter]**.

   ![6_5_googleaccount-apis-createcredentials-downloadcredentials](assets/6_5_googleaccount-apis-createcredentials-downloadcredentials.png)

1. Spara `client_id.json` filen.

   Du behöver den här hämtade JSON-filen när du konfigurerar YouTube i Adobe Experience Manager senare.

1. Klicka på **[!UICONTROL Klar]**.

   Logga ut från ditt Google-konto. Du kommer nu att skapa en YouTube-kanal.

### Skapa en YouTube-kanal {#creating-a-youtube-channel}

Du måste ha en eller flera kanaler för att kunna publicera videofilmer på YouTube. Om du redan har skapat en YouTube-kanal kan du hoppa över den här uppgiften och gå till [Lägga till taggar för publicering](/help/assets/video.md#adding-tags-for-publishing).

>[!CAUTION]
>
>Kontrollera att du redan har konfigurerat en eller flera kanaler på YouTube *innan* du lägger till kanaler under YouTube-inställningar i AEM (se [Konfigurera YouTube i AEM](#setting-up-youtube-in-aem) nedan). Om du inte gör detta får du ingen varning om att det inte finns några befintliga kanaler. Google-autentisering sker dock fortfarande när du lägger till en kanal, men det finns inget alternativ för att välja vilken kanal videon skickas till.

Så här skapar du en YouTube-kanal:

1. Gå till [https://www.youtube.com](https://www.youtube.com/) och logga in med inloggningsuppgifterna för ditt Google-konto.
1. Klicka på din profilbild i det övre högra hörnet på YouTube-sidan (kan också visas som en bokstav i en fylld färgad cirkel) och klicka sedan på **[!UICONTROL YouTube-inställningar]** (rund kugghjulsikon).
1. På sidan Översikt, under rubriken Ytterligare funktioner, klickar du på **[!UICONTROL Visa alla mina kanaler eller skapar en ny kanal]**.
1. Klicka på **[!UICONTROL Skapa en ny kanal]** på sidan Kanaler.
1. På sidan Varumärkeskonto anger du ett företagsnamn eller ett annat kanalnamn som du väljer där du vill publicera videomaterialet i fältet Märkeskontonamn. Klicka sedan på **[!UICONTROL Skapa]**.

   Kom ihåg det namn du anger här eftersom du måste ange det igen när du konfigurerar YouTube i AEM.

1. (Valfritt) Lägg till fler kanaler om det behövs.

   Nu ska du lägga till taggar för publicering.

### Lägga till taggar för publicering {#adding-tags-for-publishing}

Om du vill publicera till dina videor på YouTube associerar AEM taggar till en eller flera YouTube-kanaler. Mer information om hur du lägger till taggar för publicering finns i [Administrera taggar](/help/sites-administering/tags.md).

Om du tänker använda standardtaggarna i AEM kan du hoppa över den här uppgiften och gå till [Aktivera YouTube Publish-replikeringsagenten](#enabling-the-youtube-publish-replication-agent).

### Aktivera YouTube Publish-replikeringsagenten {#enabling-the-youtube-publish-replication-agent}

Om du vill testa anslutningen till Google Cloud-kontot trycker du på **[!UICONTROL Testa anslutning]** när du har aktiverat replikeringsagenten för YouTube-publicering. Anslutningsresultaten visas på en flik i webbläsaren. Om du har lagt till YouTube-kanaler visas en lista över dessa som en del av testet.

1. I det övre vänstra hörnet av AEM klickar du på AEM-logotypen och sedan på **[!UICONTROL Verktyg]** > **[!UICONTROL Distribution]** > **[!UICONTROL Replikering]** > **[!UICONTROL Agenter på författare]**.
1. På sidan Agents of Author klickar du på **[!UICONTROL YouTube Publish (youtube)]**.
1. Klicka på **[!UICONTROL Redigera]** i verktygsfältet till höger om Inställningar.
1. Markera kryssrutan **[!UICONTROL Aktiverad]** för att aktivera replikeringsagenten.
1. Click **[!UICONTROL OK]**.

   Nu ska du konfigurera YouTube i AEM.

### Konfigurera YouTube i AEM {#setting-up-youtube-in-aem}

Från och med AEM 6.4 introducerades en ny pekgränssnittsmetod för att konfigurera YouTube-publicering i AEM. Baserat på den installerade instansen av AEM som du använder gör du något av följande:

* Information om hur du konfigurerar YouTube i AEM före 6.4 finns i [Konfigurera YouTube i AEM före 6.4](/help/assets/video.md#setting-up-youtube-in-aem-before).
* Information om hur du konfigurerar YouTube i AEM 6.4 eller senare finns i [Konfigurera YouTube i AEM 6.4 och senare](#setting-up-youtube-in-aem-and-later).

#### Konfigurera YouTube i AEM 6.4 och senare {#setting-up-youtube-in-aem-and-later}

1. Se till att du loggar in på din instans av Dynamic Media som administratör.
1. I det övre vänstra hörnet av AEM trycker du på AEM-logotypen och sedan på **[!UICONTROL Verktyg]**(hamikon) > **[!UICONTROL Molntjänster]** > **[!UICONTROL YouTube Publishing Configuration]** i det vänstra hörnet.
1. Tryck på **[!UICONTROL global]** (markera inte den).

1. I det övre högra hörnet av den globala sidan trycker du på **[!UICONTROL Skapa]**.
1. På sidan Skapa YouTube-konfiguration, under Google Cloud Platform Settings, i fältet **[!UICONTROL Programnamn]** , anger du Google Project ID.

   Du angav projekt-ID när du konfigurerade Google Cloud-inställningarna tidigare.
Lämna sidan Skapa YouTube-konfiguration öppen; kommer du tillbaka till den om en stund.

   ![6_5_youtubepublish-createUtubeConfiguration](assets/6_5_youtubepublish-createyoutubeconfiguration.png)

1. Öppna JSON-filen som du hämtade och sparade tidigare i uppgiften [Konfigurera inställningarna](/help/assets/video.md#configuring-google-cloud-settings)för Google Cloud med en vanlig textredigerare.
1. Markera och kopiera hela JSON-texten.
1. Återgå till dialogrutan YouTube-kontoinställningar. Klistra in JSON-texten i fältet **[!UICONTROL JSON-konfiguration]** .
1. I det övre högra hörnet av sidan trycker du på **[!UICONTROL Spara]**.

   Du kommer nu att konfigurera YouTube-kanaler i AEM.

1. Tryck på **[!UICONTROL Lägg till kanal]**.
1. I fältet Kanalnamn anger du namnet på kanalen som du skapade i uppgiften **[!UICONTROL Lägga till en eller flera kanaler till YouTube]** tidigare.

   Om du vill kan du lägga till en beskrivning.

1. Tryck på **[!UICONTROL Lägg till]**.
1. YouTube/Google-autentisering visas. Om du inte redan är inloggad på Google Cloud-kontot hoppar du över det här steget.

   * Ange det Google-användarnamn och lösenord som är kopplat till Googles projekt-ID och JSON-texten ovan.
   * Beroende på hur många kanaler ditt konto har visas två eller flera objekt. Välj en kanal. Ange inte e-postadressen. det är inte en kanal.
   * På nästa sida trycker du på **[!UICONTROL Godkänn]** för att tillåta åtkomst till den här kanalen.

1. Tryck på **[!UICONTROL Tillåt]**.

   Du kommer nu att konfigurera taggar för publicering.

1. **[!UICONTROL Konfigurera taggar för publicering]** - På sidan Cloud Services > YouTube trycker du på pennikonen för att redigera listan med taggar som du vill använda.
1. Tryck på listruteikonen (upp-och-ned-cirkumflex) för att visa listan med tillgängliga taggar i AEM.
1. Tryck på en eller flera taggar för att lägga till dem.

   Om du vill ta bort en tagg som du har lagt till markerar du taggen och trycker på **[!UICONTROL X]**.

1. När du är klar med att lägga till de taggar du vill ha trycker du på **[!UICONTROL Spara]**.

   Nu kan du publicera videor i din YouTube-kanal.

#### Konfigurera YouTube i AEM före 6.4 {#setting-up-youtube-in-aem-before}

1. Se till att du loggar in på din instans av Dynamic Media som administratör.

1. I det övre vänstra hörnet av AEM trycker du på AEM-logotypen och sedan på **[!UICONTROL Verktyg]** (hamikon) > **[!UICONTROL Distribution]** > **[!UICONTROL Cloud-tjänster]** i det vänstra hörnet.
1. Under rubriken Tredjepartstjänster, under YouTube, trycker du på **[!UICONTROL Konfigurera nu]**.
1. I dialogrutan Skapa konfiguration anger du en rubrik (obligatoriskt) och ett namn (valfritt) i respektive fält.
1. Tryck på **[!UICONTROL Skapa]**.
1. I dialogrutan YouTube-kontoinställningar anger du ditt projekt-ID för Google i fältet **[!UICONTROL Programnamn]** .

   Du angav projekt-ID när du först [konfigurerade Google Cloud-inställningar](/help/assets/video.md#configuring-google-cloud-settings) .
Lämna dialogrutan YouTube-kontoinställning öppen; kommer du tillbaka till den om en stund.

1. Öppna JSON-filen som du hämtade och sparade tidigare i uppgiften Konfigurera inställningarna för Google Cloud med en vanlig textredigerare.
1. Markera och kopiera hela JSON-texten.
1. Återgå till dialogrutan YouTube-kontoinställningar. Klistra in JSON-texten i fältet **[!UICONTROL JSON-konfiguration]** .
1. Tryck på **[!UICONTROL OK]**.

   Du kommer nu att konfigurera YouTube-kanaler i AEM.

1. Till höger om **[!UICONTROL Tillgängliga kanaler]** trycker du på **+** (plusteckenikonen).
1. I dialogrutan YouTube-kanalinställningar anger du namnet på kanalen som du skapade i uppgiften **[!UICONTROL Lägga till en eller flera kanaler till YouTube]** tidigare i fältet Titel.

   Om du vill kan du lägga till en beskrivning.

1. Tryck på **[!UICONTROL OK]**.
1. YouTube/Google-autentisering visas. Om du inte redan är inloggad på Google Cloud-kontot hoppar du över det här steget.

   * Ange det Google-användarnamn och lösenord som är kopplat till Googles projekt-ID och JSON-texten ovan.
   * Beroende på hur många kanaler ditt konto har visas två eller flera objekt. Välj en kanal. Ange inte e-postadressen. det är inte en kanal.
   * På nästa sida trycker du på **[!UICONTROL Godkänn]** för att tillåta åtkomst till den här kanalen.

1. Tryck på **[!UICONTROL Tillåt]**.

   Du kommer nu att konfigurera taggar för publicering.

1. **[!UICONTROL Konfigurera taggar för publicering]** - På sidan Cloud Services > YouTube trycker du på pennikonen för att redigera listan med taggar som du vill använda.
1. Tryck på listruteikonen (upp-och-ned-cirkumflex) för att visa listan med tillgängliga taggar i AEM.
1. Tryck på en eller flera taggar för att lägga till dem.

   Om du vill ta bort en tagg som du har lagt till markerar du taggen och trycker på **X**.

1. När du är klar med att lägga till de taggar du vill ha trycker du på **[!UICONTROL OK]**.

   Nu kan du publicera videor i din YouTube-kanal.

### (Valfritt) Automatisera inställningen av YouTube-standardegenskaper för dina överförda videofilmer {#optional-automating-the-setting-of-default-youtube-properties-for-your-uploaded-videos}

Du kan även automatisera inställningen av YouTube-egenskaper när du överför videoklipp. Du uppnår detta genom att skapa en metadatabearbetningsprofil i AEM.

Om du vill skapa en metadatabearbetningsprofil kopierar du först värden från fältetiketten **[!UICONTROL ,]** Mappa till egenskap **[!UICONTROL och]** valfälten **** , som alla finns i Metadatascheman för video. Sedan skapar du din YouTube-metadatabearbetningsprofil för video genom att lägga till dessa värden.

Så här automatiserar du inställningen av YouTube-standardegenskaper för dina överförda videofilmer:

1. I det övre vänstra hörnet av AEM klickar du på AEM-logotypen och sedan på **[!UICONTROL Verktyg]** (hamikon) > **[!UICONTROL Resurser]** > **[!UICONTROL Metadata Schemas]** i det vänstra hörnet.
1. Click **[!UICONTROL default]**. (Lägg inte till en bockmarkering i markeringsrutan till vänster om &quot;standard&quot;.)
1. På **[!UICONTROL standardsidan]** markerar du kryssrutan till vänster om **[!UICONTROL videon]** och klickar sedan på **Redigera]**.
1. Klicka på fliken **[!UICONTROL Avancerat]** på sidan Redigerare för metadataschema.
1. Under rubriken YouTube Publishing klickar du på **[!UICONTROL YouTube-kategorin]**.
1. Till höger på sidan, under fliken **[!UICONTROL Inställningar]** , gör du följande:

   * Markera och kopiera värdet i textfältet **[!UICONTROL Koppla till egenskap]** .
Klistra in det kopierade värdet i den öppna textredigeraren. Du kommer att behöva det här värdet senare när du skapar din metadatabearbetningsprofil. Låt textredigeraren vara öppen.

   * Under **[!UICONTROL Alternativ]**markerar och kopierar du det standardvärde som du vill använda (till exempel Folk &amp; bloggar eller Vetenskap och teknik).
Klistra in det kopierade värdet i den öppna textredigeraren. Du kommer att behöva det här värdet senare när du skapar din metadatabearbetningsprofil. Låt textredigeraren vara öppen.

1. Under rubriken YouTube Publishing klickar du på **[!UICONTROL YouTube Privacy]**.
1. Till höger på sidan, under fliken **[!UICONTROL Inställningar]** , gör du följande:

   * Markera och kopiera värdet i textfältet **[!UICONTROL Koppla till egenskap]** .
Klistra in det kopierade värdet i den öppna textredigeraren. Du kommer att behöva det här värdet senare när du skapar din metadatabearbetningsprofil. Låt textredigeraren vara öppen.

   * Under **[!UICONTROL Alternativ]**markerar och kopierar du det standardvärde som du vill använda. Observera att alternativen grupperas i par om två. Det undre fältet i paret är standardvärdet som du vill kopiera, till exempel public, unlisted eller private.
Klistra in det kopierade värdet i den öppna textredigeraren. Du kommer att behöva det här värdet senare när du skapar din metadatabearbetningsprofil. Låt textredigeraren vara öppen.

1. Klicka på **[!UICONTROL Avbryt]** i det övre högra hörnet på sidan för redigering av metadatamatchning.
1. I det övre vänstra hörnet av AEM trycker du på AEM-logotypen och sedan på **[!UICONTROL Verktyg]** (hamikon) > **[!UICONTROL Resurser]** > **[!UICONTROL Metadataprofiler]** i det vänstra hörnet.

1. Klicka på **[!UICONTROL Skapa]** på sidan Metadataprofiler, i det övre högra hörnet på sidan.
1. I dialogrutan Lägg till metadataprofil anger du namnet i textfältet **[!UICONTROL Profiltitel]** `YouTube Video` och klickar sedan på **[!UICONTROL Skapa]**.
1. Klicka på fliken **[!UICONTROL Avancerat]** på sidan för metadataprofilredigeraren.
1. Lägg till de kopierade YouTube-publiceringsvärdena i profilen genom att göra följande:

   * Klicka på fliken **[!UICONTROL Skapa formulär]** till höger på sidan.
   * (Valfritt) Dra komponenten **[!UICONTROL Avsnittshuvud]** till vänster och släpp den i formulärområdet.
   * (Valfritt) Klicka på **[!UICONTROL Fältetikett]** för att markera komponenten.
   * (Valfritt) Till höger på sidan anger du `YouTube Publishing`under fliken Inställningar i textfältet Fältetikett.
   * Klicka på fliken **[!UICONTROL Skapa formulär]** och dra sedan komponenten **[!UICONTROL Flervärdestext]** och släpp den under rubriken **[!UICONTROL YouTube Publishing]** som du nyss skapade.

   * Klicka på **[!UICONTROL-fältetikett** för att markera komponenten.
   * Till höger på sidan, under fliken Inställningar, klistrar du in de YouTube-publiceringsvärden (värdet Fältetikett och värdet för Mappa till egenskap) som du kopierade tidigare, i respektive fält i formuläret. Klistra in alternativvärdet i fältet Standardvärde.

1. Lägg till de kopierade sekretessvärdena för YouTube till profilen genom att göra följande:

   * Klicka på fliken **[!UICONTROL Skapa formulär]** till höger på sidan.
   * (Valfritt) Dra komponenten **[!UICONTROL Avsnittshuvud]** till vänster och släpp den i formulärområdet.
   * (Valfritt) Klicka på **[!UICONTROL Fältetikett]** för att markera komponenten.
   * (Valfritt) Till höger på sidan anger du `YouTube Privacy`under fliken Inställningar i textfältet Fältetikett.
   * Klicka på fliken **[!UICONTROL Skapa formulär]** och dra sedan komponenten **[!UICONTROL MultiValue Text]** och släpp den under rubriken **[!UICONTROL YouTube Privacy]** som du just skapat.

   * Markera komponenten genom att klicka på **[!UICONTROL Fältetikett]** .
   * Till höger på sidan, under fliken Inställningar, klistrar du in de YouTube-publiceringsvärden (värdet Fältetikett och värdet för Mappa till egenskap) som du kopierade tidigare, i respektive fält i formuläret. Klistra in alternativvärdet i fältet Standardvärde.

1. Klicka på **[!UICONTROL Spara]** i det övre högra hörnet på sidan.
1. Använd metadataprofilen YouTube Publishing på de mappar där du ska överföra videoklipp. Du måste ha både metadataprofilen och videoprofilen inställda.

   Se [Metadataprofiler](/help/assets/metadata-profiles.md) och [Videoprofiler](/help/assets/video-profiles.md).

### Publicera videor i din YouTube-kanal {#publishing-videos-to-your-youtube-channel}

Nu kopplar du taggarna som du lade till tidigare till videoresurser. Denna process låter AEM veta vilka resurser som ska publiceras i din YouTube-kanal.

>[!NOTE]
>
>När du kör i läget Dynamic Media - Scene7 bör du tänka på att publicering direkt inte automatiskt publicerar på YouTube. När läget Dynamic Media - Scene7 är inställt finns det två publiceringsalternativ att välja mellan: **[!UICONTROL Omedelbart]** eller **[!UICONTROL vid aktivering]**.
>
>**[!UICONTROL Publicera omedelbart]** innebär att den överförda resursen - när den har synkroniserats med IPS - publiceras automatiskt i leveranssystemet. Det gäller Dynamic Media, men inte YouTube. Om du vill publicera på YouTube måste du publicera med hjälp av AEM Author.

>[!NOTE]
>
>För att publicera innehåll från YouTube använder AEM arbetsflödet **[!UICONTROL Publicera på YouTube]** , som gör att du kan övervaka förloppet och visa felinformation.
>
>Se [Övervaka videokodning och Publiceringsförloppet](#monitoring-video-encoding-and-youtube-publishing-progress)på YouTube.
>
>Mer detaljerad förloppsinformation finns i YouTube-loggen under replikering. Tänk dock på att en sådan övervakning kräver administratörsåtkomst.

Så här publicerar du videor till din YouTube-kanal:

1. I AEM navigerar du till en videoresurs som du vill publicera i din YouTube-kanal.
1. Välj videoresurs (den adaptiva videouppsättningen).
1. Klicka på **[!UICONTROL Egenskaper]** i verktygsfältet.
1. Klicka på **[!UICONTROL Öppna dialogrutan]** Markering till höger om fältet Taggar på fliken Grundläggande under rubriken Metadata.
1. På sidan Välj taggar navigerar du till de taggar du vill använda och markerar sedan en eller flera taggar.

   Kom ihåg att taggarna måste kopplas till YouTube-kanalen.

1. Klicka på **[!UICONTROL Markera]** i det övre högra hörnet på sidan.
1. Klicka på **[!UICONTROL Spara och stäng]** i det övre högra hörnet på egenskapssidan för videon.
1. Klicka på **[!UICONTROL Snabbpublicering]** i verktygsfältet.

   Se även [Använda Publication Management med AEM Sites](https://helpx.adobe.com/experience-manager/kt/sites/using/publication-management-feature-video-use.html).

   Du kan även verifiera den publicerade videon på din YouTube-kanal.

### (Valfritt) Verifiera den publicerade videon på YouTube {#optional-verifying-the-published-video-on-youtube}

Du kan också övervaka förloppet för din YouTube-publicering (eller avpublicering).

Se [Övervaka videokodning och Publiceringsförloppet](#monitoring-video-encoding-and-youtube-publishing-progress)på YouTube.

Publiceringstiderna kan variera avsevärt beroende på olika faktorer, bland annat huvudvideons format, filstorlek och överföringstrafik. Publiceringsprocessen kan ta från några minuter till flera timmar. Tänk också på att format med högre upplösning återges mycket långsammare. 720p och 1080p tar till exempel betydligt längre tid att visa än 480p.

Efter åtta timmar om du fortfarande ser ett statusmeddelande som säger **[!UICONTROL Överförd (bearbetas, vänta)]** kan du försöka ta bort videon från vår webbplats och överföra den igen.

### Länka YouTube-URL:er till ditt webbprogram {#linking-youtube-urls-to-your-web-application}

Du kan hämta en YouTube URL-sträng som genereras av Dynamic Media när du har publicerat videon. När du kopierar YouTube-URL:en markeras den i Urklipp så att du kan klistra in den på sidorna på webbplatsen eller i programmet.

>[!NOTE]
>
>YouTube-URL:en är inte tillgänglig för kopiering förrän du har publicerat videoresursen på YouTube.

Så här länkar du YouTube-URL:er till ditt webbprogram:

1. Navigera till den *YouTube-publicerade* videoresurs vars URL du vill kopiera och markera den.

   Kom ihåg att YouTube-URL:er endast är tillgängliga för kopiering *när* du först har *publicerat* videomaterialet på YouTube.

1. Klicka på **[!UICONTROL Egenskaper]** i verktygsfältet.
1. Klicka på fliken **[!UICONTROL Avancerat]** .
1. Under rubriken YouTube Publishing (YouTube Publishing) i YouTubes URL-lista markerar och kopierar du URL-texten till webbläsaren för att förhandsgranska resursen eller lägga till den på webbinnehållssidan.

### Avpublicera videoklipp för att ta bort dem från YouTube {#unpublishing-videos-to-remove-them-from-youtube}

När du avpublicerar en videoresurs i AEM tas videon bort från YouTube.

>[!CAUTION]
>
>Om du tar bort en video direkt från YouTube känner AEM inte av det och fortsätter bete sig som om videon fortfarande publiceras på YouTube. Avpublicera alltid en videoresurs från YouTube med hjälp av AEM.

>[!NOTE]
>
>För att ta bort innehåll från YouTube använder AEM arbetsflödet **[!UICONTROL Unpublish från YouTube]** , som gör att du kan övervaka förloppet och visa felinformation.
>
>Se [Övervaka videokodning och Publiceringsförloppet](#monitoring-video-encoding-and-youtube-publishing-progress)på YouTube.

Så här avpublicerar du videoklipp för att ta bort dem från YouTube:

1. Navigera till de videoresurser som du vill avpublicera från din YouTube-kanal.
1. Välj en eller flera publicerade videoresurser i ett resursurvalsläge.
1. Klicka på **[!UICONTROL Hantera publikation]** i verktygsfältet. Du kan behöva trycka på ikonen med tre punkter (. . .) i verktygsfältet för att se **[!UICONTROL Hantera publikation]**.
1. Tryck på **[!UICONTROL Avpublicera]** på sidan Hantera publikation.
1. Tryck på **[!UICONTROL Nästa]** i det övre högra hörnet på sidan.
1. Tryck på **[!UICONTROL Avpublicera]** i det övre högra hörnet på sidan.

## Övervaka videokodning och YouTubes publiceringsförlopp {#monitoring-video-encoding-and-youtube-publishing-progress}

När du överför en ny video till en mapp där videokodning används eller publicerar videon på Youtube, kan du övervaka hur videokodningen/Youtube-publiceringen fortskrider (eller misslyckas) på flera olika sätt. Det faktiska publiceringsförloppet för YouTube är endast tillgängligt via loggarna, men om det misslyckas eller lyckas visas på ytterligare sätt som beskrivs i följande procedur. Dessutom kan du få e-postmeddelanden när ett publiceringsarbetsflöde eller videokodning från YouTube har slutförts eller avbrutits.

### Övervaka förlopp {#monitoring-progress}

Så här övervakar du förloppet (inklusive misslyckad kodning/YouTube-publicering):

1. Visa kodningsförloppet för video i resursmappen:

   * I kortvyn visas videokodningsförloppet för resursen i procent. Om ett fel uppstår visas även den här informationen på resursen.
   ![chlimage_1-429](assets/chlimage_1-429.png)

   * I listvyn visas förloppet för videokodning i kolumnen **[!UICONTROL Bearbetningsstatus]** . Om ett fel uppstår visas det här meddelandet i samma kolumn.
   ![chlimage_1-430](assets/chlimage_1-430.png)

   Den här kolumnen visas inte som standard. Om du vill aktivera kolumnen väljer du **[!UICONTROL Visa inställningar]** i listrutan Vyer och lägger till kolumnen **[!UICONTROL Bearbetningsstatus]** och trycker eller klickar på **[!UICONTROL Uppdatera]**.

   ![chlimage_1-431](assets/chlimage_1-431.png)

1. Visa förloppet i tillgångsinformationen. När du trycker eller klickar på en resurs öppnar du den nedrullningsbara menyn och väljer **[!UICONTROL Tidslinje]**. Om du vill begränsa det till arbetsflödesaktiviteter som kodning eller YouTube-publicering väljer du **[!UICONTROL Arbetsflöden]**.

   ![chlimage_1-432](assets/chlimage_1-432.png)

   All arbetsflödesinformation, till exempel kodning, visas på tidslinjen. För YouTube-publicering innehåller tidslinjen i arbetsflödet även namnet på YouTube-kanalen och YouTubes video-URL. Dessutom visas felmeddelanden på tidslinjen i arbetsflödet när publiceringen är klar.

   >[!NOTE]
   >
   >Det kan ta lång tid innan fel-/felmeddelanden slutligen registreras på grund av flera arbetsflödeskonfigurationer för **[!UICONTROL återförsök]**, **[!UICONTROL återförsöksfördröjning]** och **[!UICONTROL timeout]** från [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr), till exempel:
   >
   >    * Konfiguration av Apache Sling-jobbkö
   >    * Extern processhanterare för Adobe Granite-arbetsflöde
   >    * Timeoutkö för Granite-arbetsflöde
   >
   >Du kan justera **[!UICONTROL återförsök]**, **[!UICONTROL återförsöksfördröjning]** och **[!UICONTROL timeout]** -egenskaper i dessa konfigurationer.

1. Information om pågående arbetsflöden finns i Arbetsflödesinstanser som är tillgängliga från **[!UICONTROL Verktyg]** > **[!UICONTROL Arbetsflöde]** > **[!UICONTROL Instanser]**.

   >[!NOTE]
   >
   >Du kan behöva administratörsbehörighet för att komma åt **[!UICONTROL Verktyg]** -menyn.

   ![chlimage_1-432](assets/chlimage_1-433.png)

   Markera instansen och tryck eller klicka på **[!UICONTROL Öppna historik]**.

   ![chlimage_1-434](assets/chlimage_1-434.png)

   I området Arbetsflödesinstanser kan du även göra uppehåll i, avsluta eller byta namn på arbetsflöden. Mer information finns i [Administrera arbetsflöden](/help/sites-administering/workflows-administering.md) .

1. Information om misslyckade jobb finns i Arbetsflödesfel i **[!UICONTROL Verktyg]** > **[!UICONTROL Arbetsflöde]** > **[!UICONTROL Fel]**. I **[!UICONTROL Arbetsflödesfelet]** visas alla misslyckade arbetsflödesaktiviteter.

   >[!NOTE]
   >
   >Du kan behöva administratörsbehörighet för att komma åt **[!UICONTROL Verktyg]** -menyn.

   ![chlimage_1-435](assets/chlimage_1-435.png)

   >[!NOTE]
   >
   >Det kan ta lång tid innan felmeddelandet slutligen spelas in på grund av flera arbetsflödeskonfigurationer för **[!UICONTROL återförsök]**, **[!UICONTROL återförsöksfördröjning]** och **[!UICONTROL timeout]** från [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr), till exempel:
   >
   >
   >
   >    * Konfiguration av Apache Sling-jobbkö
   >    * Extern processhanterare för Adobe Granite-arbetsflöde
   >    * Timeoutkö för Granite-arbetsflöde
   >
   >
   >Du kan justera **[!UICONTROL återförsök]**, **[!UICONTROL återförsöksfördröjning]** och **[!UICONTROL timeout]** -egenskaper i dessa konfigurationer.

1. Information om slutförda arbetsflöden finns i Arbetsflödesarkiv som finns under **[!UICONTROL Verktyg]** > **[!UICONTROL Arbetsflöde]** > **[!UICONTROL Arkiv]**. I **[!UICONTROL Arbetsflödesarkivet]** visas alla slutförda arbetsflödesaktiviteter.

   >[!NOTE]
   >
   >Du kan behöva administratörsbehörighet för att komma åt **[!UICONTROL Verktyg]** -menyn.

   ![chlimage_1-436](assets/chlimage_1-436.png)

1. Du kan få e-postmeddelanden om avbrutna eller misslyckade arbetsflödesjobb. Dessa e-postmeddelanden kan konfigureras av en administratör. Se [Konfigurera e-postmeddelanden](#configuring-e-mail-notifications).

#### Konfigurera e-postmeddelanden {#configuring-e-mail-notifications}

>[!NOTE]
>
>Du kan behöva administratörsbehörighet för att komma åt **[!UICONTROL Verktyg]** -menyn.

Hur du konfigurerar meddelanden beror på om du vill ha meddelanden om kodningsjobb eller YouTube-publiceringsjobb:

* För kodningsjobb kan du komma åt konfigurationssidan för alla e-postmeddelanden för AEM-arbetsflöden på **[!UICONTROL Verktyg]** > **[!UICONTROL Åtgärder]** > **[!UICONTROL Webbkonsol]** och genom att söka efter **[!UICONTROL Day CQ Workflow Email Service]**. Se [Konfigurera e-postmeddelande i AEM](/help/sites-administering/notification.md). Du kan markera eller avmarkera kryssrutorna för **[!UICONTROL Notify on Abort]** eller **[!UICONTROL Notify on Complete]** .

* Gör följande för YouTube-publiceringsjobb:

1. I AEM trycker du på **[!UICONTROL Verktyg]** > **[!UICONTROL Arbetsflöde]** > **[!UICONTROL Modeller]**.
1. På sidan Arbetsflödesmodeller väljer du **[!UICONTROL Publicera på YouTube]** och sedan trycker du på **[!UICONTROL Redigera]** i verktygsfältet.
1. Tryck på **[!UICONTROL Redigera]** i det övre högra hörnet på sidan Publicera på YouTube-arbetsflöde.
1. Håll muspekaren på YouTube-komponenten Upload och tryck sedan en gång för att visa det textbundna verktygsfältet.

   ![6_5_publishingUtubeworkflow](assets/6_5_publishtoyoutubeworkflow.png)

1. Tryck på ikonen Konfiguration (skiftnyckel) i det textbundna verktygsfältet. Klicka på fliken **[!UICONTROL Argument]** .

   ![6_5_publishtoyoutubeworkflow-configurationicon](assets/6_5_publishtoyoutubeworkflow-configurationicon.png)

1. I dialogrutan YouTube-överföringsprocess - stegegenskaper trycker du på fliken **[!UICONTROL Argument]** .

   ![6_5_publishtoyoutubeworkflow-arguments-tab](assets/6_5_publishtoyoutubeworkflow-arguments-tab.png)

1. Du kan markera eller avmarkera följande kryssrutor:

   * Publicera start
   * Publiceringsfel
   * Slutförd publicering - innehåller information om kanaler och URL:er
   Om du rensar en kryssruta innebär det att du inte får det angivna e-postmeddelandet från YouTubes publiceringsarbetsflöde.

   >[!NOTE]
   >
   >Dessa e-postmeddelanden är specifika för YouTube och är utöver de allmänna e-postmeddelandena för arbetsflöden. Du kan därför få två uppsättningar e-postmeddelanden - det allmänna meddelandet som finns i **[!UICONTROL Day CQ Workflow Email Notification Service]** och ett som är specifikt för YouTube beroende på dina konfigurationsinställningar.

1. När du är klar trycker du på ikonen **[!UICONTROL Klar]** (bockmarkering) i dialogrutans övre högra hörn.
1. Tryck på **[!UICONTROL Synkronisera]** i det övre högra hörnet på sidan Publicera på YouTube-arbetsflöde.

## Visa videorapporter {#viewing-video-reports}

>[!NOTE]
>
>Videorapporter är bara tillgängliga när du kör Dynamic Media - hybrid-läge.

Videorapporter visar flera sammanställda mätvärden under en angiven tidsperiod för att hjälpa dig att övervaka att *publicerade *enskilda och sammanställda videor fungerar som förväntat. Följande viktigaste mätdata samlas in för alla publicerade videor på hela webbplatsen:

* Video börjar
* Slutförandefrekvens
* Genomsnittlig tid för video
* Total tid för video
* Videor per besök

En tabell över alla *publicerade* videoklipp listas också så att du kan spåra de mest visade videoklippen på din webbplats baserat på den totala videostarten.

När du trycker på ett videonamn i listan visas videons rapport för att behålla (lämna av) publik i form av ett linjediagram. Diagrammet visar antalet vyer för en given tidpunkt under videouppspelning. När du spelar upp videon synkroniseras det lodräta strecket med tidsindikatorn i spelaren. Släppningar i linjediagramdata indikerar var publiken slutar intressera sig.

Om videon kodades utanför Adobe Experience Manager Dynamic Media är inte data om målgruppsinnehållande (bortfall) och uppspelningsprocent i tabellen tillgängliga.

Se även [Konfigurera Dynamic Media Cloud-tjänster](/help/assets/config-dynamic.md).

>[!NOTE]
>
>Spårnings- och rapportdata baseras uteslutande på användningen av Dynamic Medias egen videospelare och tillhörande videospelarförinställning. Därför kan du inte spåra och rapportera om videofilmer som spelas upp med andra videospelare.

Första gången du anger Videorapporter visas som standard videodata från och med den första i den aktuella månaden och till och med den aktuella månadens datum. Du kan dock åsidosätta standarddatumintervallet genom att ange ett eget datumintervall. Nästa gång du anger Videorapporter används det datumintervall du har angett.

För att videorapporter ska fungera på rätt sätt skapas ett Report Suite-ID automatiskt när Dynamic Media Cloud Services konfigureras. Samtidigt skickas Report Suite-ID:t till publiceringsservern så att det är tillgängligt för funktionen Kopiera URL när du förhandsgranskar resurser. Detta kräver dock att publiceringsservern redan har konfigurerats. Om publiceringsservern inte är konfigurerad kan du fortfarande publicera för att se videorapporten, men du måste gå tillbaka till Dynamic Media Cloud Configuration och trycka på **[!UICONTROL OK]**.

Så här visar du videorapporter:

1. I det övre vänstra hörnet av AEM trycker du på AEM-logotypen och sedan på **[!UICONTROL Verktyg]** (hamikon) > **[!UICONTROL Resurser]** > **[!UICONTROL Videorapporter]** i det vänstra hörnet.
1. Gör något av följande på sidan Videorapporter:

   * I närheten av det övre högra hörnet trycker du på ikonen **Uppdatera videorapport **.
Du behöver bara använda Uppdatera om rapportens slutdatum är den aktuella dagen. På så sätt ser du den videospårning som har utförts sedan du senast körde rapporten.

   * I det övre högra hörnet trycker du på ikonen **Datumväljaren **.
Ange start- och slutdatumintervallet som du vill ha videodata för och tryck sedan på **[!UICONTROL Kör rapport]**.
   I grupprutan Top Metrics (Toppvärden) identifieras olika aggregerade mått för alla *publicerade *videor på webbplatsen.

1. I tabellen som visar de publicerade videoklippen trycker du på ett videonamn för att spela upp videon och ser även videons återgivningsrapport.

### Visa videorapporter baserade på ett videovisningsprogram som du har skapat med Scene7 HTML5 Viewer SDK {#viewing-video-reports-based-on-a-video-viewer-that-you-created-using-the-scene-hmtl-viewer-sdk}

Om du använder ett visningsprogram som inte är installerat från Dynamic Media, eller om du har skapat en anpassad visningsförinställning baserad på ett videoredigeringsprogram som inte är i kartong, krävs inga ytterligare steg för att visa videorapporter. Om du har skapat ett eget videovisningsprogram baserat på SDK:t för Scene7 HTML5 Viewer ska du följa de här stegen för att se till att videovisningsprogrammet skickar spårningshändelser till videorapporter för dynamiska media.

Använd Scene7 Viewer Reference och Scene7 HTML5 Viewer SDK för att skapa egna videovisningsprogram.

Se [Referenshandbok](https://marketing.adobe.com/resources/help/en_US/s7/viewers_ref/index.html)för Scene7-visningsprogram.

Hämta Scene7 HTML Viewer SDK från Adobe Developer Connection.

Se [Adobe Developer Connection](https://help.adobe.com/en_US/scene7/using/WSef8d5860223939e2-43dedf7012b792fc1d5-8000.html).

Så här visar du videorapporter baserade på ett videovisningsprogram som du har skapat med SDK:n för HTML5-visningsprogrammet för Scene7:

1. Navigera till alla publicerade videoresurser.
1. I den nedrullningsbara listan i det övre vänstra hörnet av resursens sida väljer du **[!UICONTROL Visare]**.
1. Välj en förinställning för visningsprogrammet och kopiera inbäddningskoden.
1. I inbäddningskoden söker du efter raden med följande:

   `videoViewer.setParam("config2", "<value>");`

   Parametern `config2` aktiverar spårning i HTML5-visningsprogram. Det är också en företagsspecifik förinställning som innehåller konfigurationsinformationen för Videorapportering och för kundspecifika Adobe Analytics-konfigurationer.

   Rätt värde för parametern config2 finns både i funktionen **Embed Code **och i funktionen copy **URL **function. I URL:en från kommandot **URL **är parametern som ska sökas efter `&config2=<value>` . Värdet är nästan alltid `companypreset`men i vissa fall kan det också vara `companypreset-1`, `companypreset-2`o.s.v.

1. Lägg till AppMeasurementBridge .jsp på visningsprogramsidan i din anpassade videovisningsprogramkod genom att göra följande:

   * Börja med att bestämma om du behöver `&preset` parametern.
Om `config2` parametern är `companypreset`behöver du inte * `&preset=parameter`.
Om `config2` det är något annat anger du parametern preset till samma som `config2` parametern. Om du `config2=companypreset-2`till exempel lägger `&param2=companypreset-2` till i URL:en AppMeasurmentBridge.jsp.

   * Lägg sedan till skriptet AppMeasurementBridge.jsp:
      `<script language="javascript" type="text/javascript" src="https://s7d1.scene7.com/s7viewers/AppMeasurementBridge.jsp?company=robindallas&preset=companypreset-2"></script>`

1. Skapa komponenten TrackingManager genom att göra följande:

   * När du har anropat `s7sdk.Utils.init();` skapar du en TrackingManager-instans för att spåra händelser genom att lägga till följande:
      `var trackingManager = new s7sdk.TrackingManager();`

   * Koppla komponenter till TrackingManager genom att göra följande:
I händelsehanteraren kopplar du den komponent som du vill spåra till TrackingManager. `s7sdk.Event.SDK_READY` 
Om komponenten är `videoPlayer`lägger du till
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

   Mer information finns i *Använda komponenten* TrackingManager i *Scene7 HTML5 Viewer SDK-användarhandboken* som kan hämtas från [Adobe Developer Connection](https://help.adobe.com/en_US/scene7/using/WSef8d5860223939e2-43dedf7012b792fc1d5-8000.html).

## Lägga till bildtexter i video {#adding-captions-to-video}

Du kan utöka räckvidden för dina videor till globala marknader genom att lägga till bildtexter till enskilda videor eller till adaptiva videouppsättningar. Genom att lägga till bildtext undviker du behovet av att duplicera ljudet, eller behovet av att använda inbyggda högtalare för att spela in ljudet igen för varje språk. Videon spelas upp på det språk den spelades in på. Undertexter på främmande språk visas så att personer på olika språk fortfarande kan förstå ljuddelen.

Bildtext ger också bättre tillgänglighet genom att använda undertexter för personer som är döva eller hörselskadade.

>[!NOTE]
>
>Den videospelare som du använder måste ha stöd för visning av bildtexter.

Dynamic Media kan konvertera bildtextfiler till JSON-format (JavaScript Object Notation). Den här konverteringen innebär att du kan bädda in JSON-texten på en webbsida som en dold men fullständig utskrift av videon. Sökmotorerna kan sedan crawla och indexera innehållet så att videoklippen blir lättare att hitta och ge kunderna ytterligare information om videoinnehållet.

Mer information om hur du använder JSON-funktionen i en URL finns i [Servera statiskt (icke-bildinnehåll](https://marketing.adobe.com/resources/help/en_US/s7/is_ir_api/is_api/c_serving_static_nonimage_contents.html) ) i API-hjälpen *för* Scene7 Image Serving.

Så här lägger du till bildtexter eller undertexter till video:

1. Använd ett program eller en tjänst från tredje part för att skapa en undertextningsfil för video.

   Kontrollera att filen du skapar följer standarden WebVTT (Web Video Text Tracks). Bildtextens filnamnstillägg är .vtt. Du kan läsa mer om bildtextstandarden WebVTT.

   Se [WebVTT: Textspårningsformatet](https://dev.w3.org/html5/webvtt/)för webbvideo.

   Det finns både kostnadsfria och premiumverktyg och tjänster som du kan använda för att skapa bildtexter/undertexter utanför Dynamic Media. Om du till exempel vill skapa en enkel videobeskrivningsfil utan formatering kan du använda följande kostnadsfria redigerings- och redigeringsverktyg för bildtexter online:

   [WebVTT Caption Maker](https://testdrive-archive.azurewebsites.net/Graphics/CaptionMaker/Default.html)

   Du får bäst resultat om du använder verktyget i Internet Explorer 9 eller senare, Google Chrome eller Safari.

   I verktyget, i fältet **[!UICONTROL Ange URL för videofilen]** , klistrar du in den kopierade URL-adressen för videofilen och klickar sedan på **[!UICONTROL Load**. Se [Hämta en URL för en resurs](/help/assets/linking-urls-to-yourwebapplication.md#obtaining-a-url-for-an-asset) för att hämta URL-adressen till själva videofilen som du sedan kan klistra in i **[!UICONTROL Ange URL-adressen för videofilsfältet]**. Internet Explorer, Chrome eller Safari kan sedan spela upp videon direkt.

   Följ nu instruktionerna på skärmen för att skapa och spara WebVTT-filen. När du är klar kopierar du bildtextfilens innehåll och klistrar in det i en vanlig textredigerare och sparar det med filnamnstillägget .vtt.

   >[!NOTE]
   >
   >Om du vill ha globalt stöd för videoundertexter på flera språk måste du skapa separata VTT-filer och anropa varje språk som du vill ha stöd för.

   I allmänhet vill du ge bildtexten ett namn som är detsamma som videofilen och bifoga den med språkinställningen -EN, -FR eller -DE osv. Genom att göra det kan det hjälpa dig att automatisera genereringen av video-URL:er med ditt befintliga system för hantering av webbinnehåll.

1. I AEM överför du din WebVTT-bildtextfil till DAM.
1. Navigera till den *publicerade *videoresurs som du vill associera med bildtextfilen som du överförde.

   Kom ihåg att URL-adresser endast är tillgängliga att kopiera *när* du först har *publicerat* resurserna.

   Se [Publicera resurser.](/help/assets/publishing-dynamicmedia-assets.md)

1. Gör något av följande:

   * Tryck på **[!UICONTROL URL]** om du vill visa ett videoklipp på popup-skärmen. I dialogrutan URL-adress markerar och kopierar du URL-adressen till Urklipp och sedan förbi URL-adressen till en enkel textredigerare. Lägg till den kopierade URL:en för videon med följande syntax:

      `&caption=<server_path>/is/content/<path_to_caption.vtt_file,1>`

      Lägg märke till `,1` i slutet av bildtextbanan. Omedelbart efter tillägget .vtt i sökvägen kan du aktivera (aktivera) eller inaktivera (inaktivera) den stängda bildtextsknappen i videospelarfältet genom att ställa in på `,1` respektive `,0`.

   * Om du vill visa en inbäddad video trycker du på **[!UICONTROL Embed Code (Bädda in kod]**). I dialogrutan Bädda in kod markerar och kopierar du den inbäddade koden till Urklipp och klistrar sedan in koden i en enkel textredigerare. Lägg till den kopierade inbäddningskoden med följande syntax:

      `videoViewer.setParam("caption","<path_to_caption.vtt_file,1>");`

      Lägg märke till `,1` i slutet av bildtextbanan. Omedelbart efter tillägget .vtt i sökvägen kan du aktivera (aktivera) eller inaktivera (inaktivera) den stängda bildtextsknappen i videospelarfältet genom att ställa in på `,1` respektive `,0`.

## Lägga till kapitelmarkörer i video {#adding-chapter-markers-to-video}

Du kan göra det enklare att titta på och navigera i videoklipp med långa formulär genom att lägga till kapitelmarkörer i enstaka videor eller i adaptiva videouppsättningar. När en användare spelar upp videon kan han/hon klicka på kapitelmarkörerna på tidslinjen (kallas även videoscubbaren) för att enkelt navigera till sin intressanta punkt eller omedelbart hoppa till nytt innehåll, demonstrationer, självstudiekurser och så vidare.

>[!NOTE]
>
>Den videospelare som används måste ha stöd för kapitelmarkörer. Dynamiska mediespelare har stöd för kapitelmarkörer, men det kanske inte går att använda tredjepartsvideospelare.

Om du vill kan du skapa och märka ut ett eget anpassat visningsprogram med kapitel i stället för att använda en förinställning för visningsprogrammet för video. Instruktioner om hur du skapar ett eget HTML5-visningsprogram med kapitelnavigering finns i handboken Adobe Scene7 Viewer SDK för HTML5 under klasserna `s7sdk.video.VideoPlayer` och `s7sdk.video.VideoScrubber`. Adobe Scene7 Viewer SDK kan hämtas från [Adobe Developer Connection](https://help.adobe.com/en_US/scene7/using/WSef8d5860223939e2-43dedf7012b792fc1d5-8000.html).

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

I exemplet ovan `Chapter 1` är det en referensidentifierare som är valfri. Referenstiden för `00:00:000 --> 01:04:364` anger kapitlets start- och sluttid i `00:00:000` format. De sista tre siffrorna är millisekunder och kan lämnas som `000`, om det passar. Kapiteltiteln för `The bicycle store behind it all` är den faktiska beskrivningen av kapitlets innehåll. Referensidentifieraren, startreferenstiden och kapiteltiteln visas alla i ett popup-fönster i videospelaren när en användare håller muspekaren över en visuell referenspunkt i videons tidslinje.

Eftersom du använder ett HTML5-videovisningsprogram bör du kontrollera att den kapitelfil du skapar följer standarden WebVTT (Web Video Text Tracks). Kapitelfilnamnstillägget är .vtt. Du kan läsa mer om bildtextstandarden WebVTT.

Se [WebVTT: Textspår för webbvideo](https://dev.w3.org/html5/webvtt/)

**Så här lägger du till kapitelmarkörer i video:**

1. Spara VTT-filen i UTF8-kodning för att undvika problem med teckenåtergivning i kapiteltiteltexten.

   Vanligtvis vill du ge kapitlet VTT-filen samma namn som videofilen och bifoga den med kapitel. Genom att göra det kan det hjälpa dig att automatisera genereringen av video-URL:er med ditt befintliga system för hantering av webbinnehåll.
1. I AEM överför du din WebVTT-kapitelfil.

   Se [Överföra resurser](/help/assets/managing-assets-touch-ui.md#uploading-assets).

1. Gör något av följande:

   <table>
     <tbody>
      <tr>
       <td>För en popup-video</td>
       <td>
       <ol>
       <li>Navigera till den <i>publicerade </i>videoresurs som du vill associera med den kapitelfil som du överförde. Kom ihåg att URL-adresser endast är tillgängliga att kopiera <i>när</i> du först har <i>publicerat</i> resurserna. Se <a href="/help/assets/publishing-dynamicmedia-assets.md">Publicera resurser.</a></li>
       <li>Klicka eller tryck på <strong>Visare</strong>i listrutan.</li>
       <li>Tryck eller klicka på förinställningsnamnet för videovisningsprogrammet i den vänstra listen. En förhandsgranskning av videon öppnas på en separat sida.</li>
       <li>Klicka på <strong>URL</strong>längst ned i den vänstra listen.</li>
       <li>I dialogrutan URL-adress markerar och kopierar du URL-adressen till Urklipp och sedan förbi URL-adressen till en enkel textredigerare.</li>
       <li><br /> Lägg till den kopierade URL:en för videon med följande syntax för att koppla den till den kopierade URL:en till din kapitelfil: <br /> <code>&navigation=<<i>full_copied_URL_path_to_chapter_file</i>.vtt></code><br /> </li>
       </ol> </td>
      </tr>
      <tr>
       <td>För en inbäddad videoupplevelse<br /> </td>
       <td>
       <ol>
       <li>Navigera till den <i>publicerade </i>videoresurs som du vill associera med den kapitelfil som du överförde. Kom ihåg att URL-adresser endast är tillgängliga att kopiera <i>när</i> du först har <i>publicerat</i> resurserna. Se <a href="/help/assets/publishing-dynamicmedia-assets.md">Publicera resurser.</a></li>
       <li>Klicka eller tryck på <strong>Visare</strong>i listrutan.</li>
       <li>Tryck eller klicka på förinställningsnamnet för videovisningsprogrammet i den vänstra listen. En förhandsgranskning av videon öppnas på en separat sida.</li>
       <li>Klicka på <strong>Bädda</strong>längst ned i den vänstra listen.</li>
       <li>I dialogrutan Bädda in kod markerar och kopierar du hela koden till Urklipp och klistrar in den i en enkel textredigerare.</li>
       <li>Lägg till videons inbäddningskod med följande syntax för att koppla den till den kopierade URL:en till din kapitelfil:<br /> <br /> <code>videoViewer.setParam("navigation","&lt;<i>full_copied_URL_path_to_chapter_file</i>.vtt&gt;"</code></li>
       </ol> </td>
      </tr>
     </tbody>
   </table>

## Om videominiatyrer i Dynamic Media - Scene7-läge {#about-video-thumbnails-in-dynamic-media-scene-mode}

En videominiatyr är en version med reducerad storlek av en videobildruta eller en bildresurs som representerar videon för kunden. Miniatyrbilden bör uppmuntra kunden att klicka på videon.

Alla videor i AEM måste ha en tillhörande miniatyrbild; Du kan inte ta bort en miniatyrbild utan att ersätta den. Som standard används den första bildrutan som miniatyrbild när du överför en video till AEM. Du kan dock anpassa miniatyrbilden för exempelvis varumärke eller visuell sökning. När du anpassar en videominiatyr kan du antingen spela upp videon och göra paus i den bildruta som du vill använda eller välja en bildresurs som du redan har överfört och *publicerat* i resurshanteraren.

Observera att en anpassad videominiatyrbild som du väljer från en video inte extraheras och sparas i DAM som en separat och distinkt resurs. En anpassad videominiatyr som du väljer från en befintlig bildresurs sparas dock i JCR-filen. Sökvägen för den valda resursen lagras under videoresursens nod som i följande exempelsökväg:

`/content/dam/*<folder_name*>/<*video_name*>/jcr:content/manualThumbnail`

Möjligheten att anpassa en videominiatyr är endast tillgänglig efter att du har tillämpat en videoprofil på den mapp där videon finns.

Se även [Om videominiatyrer i läget](#about-video-thumbnails-in-dynamic-media-hybrid-mode)Dynamic Media - Hybrid.

### Lägga till en anpassad videominiatyr {#adding-a-custom-video-thumbnail}

Dessa steg gäller endast för Dynamic Media som körs i läget &quot;DynamicMedia_Scene7&quot;.

Om du **vill lägga till en anpassad videominiatyr**,

1. Kontrollera att du redan har gjort följande:

   * Skapade en mapp för dina videoresurser.
   * [En videoprofil har använts på mappen](/help/assets/video-profiles.md#applying-a-video-profile-to-folders).

   * [Dina videoklipp har överförts till mappen](/help/assets/managing-video-assets.md#uploadingandpreviewingvideoassets).

1. Navigera till en överförd videoresurs vars miniatyrbild du vill ändra.
1. Tryck på videoresursen i **[!UICONTROL listvyn]** eller **[!UICONTROL kortvyn]**.
1. Tryck på ikonen **[!UICONTROL Properties** (en cirkel med &quot;i&quot;) i verktygsfältet.
1. Tryck på **[!UICONTROL Ändra miniatyrbild]** på videons egenskapssida.
1. Gör något av följande på sidan Ändra miniatyrbild:

   * Så här använder du en bildruta från videon som ny miniatyrbild:

      * Tryck på **[!UICONTROL Välj bildruta från video]** i verktygsfältet.
      * Tryck på uppspelningsknappen och tryck sedan på pausknappen på bildrutan som du vill spela in som videons nya miniatyrbild.
   * Så här använder du en bildresurs som ny miniatyrbild:

      * Tryck på **[!UICONTROL Välj miniatyrbild från resurser]** i verktygsfältet.
      * Tryck på **[!UICONTROL Välj miniatyrbild]**.
      * Navigera till en tidigare överförd och publicerad bildresurs som du vill använda. Observera att resursens storlek automatiskt ändras så att den fungerar som en miniatyrbild för videon.
      * Markera bildresursen och tryck sedan på **[!UICONTROL Välj]**.


1. Tryck på **[!UICONTROL Spara ändring]** på sidan Ändra miniatyrbild.
1. Tryck på **[!UICONTROL Spara och stäng]** på egenskapssidan för videon i det övre högra hörnet.

## Om videominiatyrer i Dynamic Media - hybrid-läge {#about-video-thumbnails-in-dynamic-media-hybrid-mode}

Du kan välja mellan en av tio miniatyrbilder som har genererats automatiskt av Dynamic Media och lägga till dem i videon. Videospelaren visar den valda miniatyrbilden när en videoresurs används med komponenten Dynamic Media i redigeringsmiljön på AEM Sites, AEM Mobile eller AEM Screens. Miniatyrbilden fungerar som en statisk bild som bäst motsvarar innehållet i hela videon och uppmuntrar dessutom användarna att klicka på knappen Spela upp.

Baserat på den totala tiden för videon hämtar Dynamic Media tio (standard) miniatyrbilder med 1 %, 11 %, 21 %, 31 %, 41 %, 51 %, 61 %, 71 %, 81 % och 91 % i videon. De tio miniatyrbilderna finns kvar, vilket innebär att om du väljer en annan miniatyrbild senare behöver du inte återskapa serien. Du förhandsgranskar de tio miniatyrbilderna och väljer sedan den som du vill använda med videon. Om du vill ändra till standard kan du använda CRXDE Lite för att konfigurera det tidsintervall som miniatyrbilder genereras. Om du till exempel bara vill generera en serie med fyra miniatyrbilder med jämna mellanrum från videon kan du konfigurera intervalltiden till 24 %, 49 %, 74 % och 99 %.

Helst kan du lägga till en videominiatyr när som helst efter att du har överfört videon, men innan du publicerar videon på webbplatsen.

Om du vill kan du välja att överföra en anpassad miniatyrbild för videon i stället för att använda en miniatyrbild som genererats av Dynamic Media. Du kan till exempel skapa en anpassad miniatyrbild med videons titel, en iögonfallande öppningsbild eller en mycket specifik bild som hämtats från videon. Den anpassade videominiatyrbilden som du överför ska ha en maximal upplösning på 1 280 x 720 pixlar (minsta bredd på 640 pixlar) och inte vara större än 2 MB.

Se även [Om videominiatyrer i Dynamic Media - Scene7-läge](/help/assets/video.md#about-video-thumbnails-in-dynamic-media-scene-mode).

### Lägga till en videominiatyr {#adding-a-video-thumbnail}

De här stegen gäller endast för Dynamic Media som körs i hybridläge.

Om du **vill lägga till en videominiatyr**

1. Navigera till en överförd videoresurs som du vill lägga till en videominiatyr.
1. I resursurvalsläget, antingen från listvyn eller kortvyn, trycker du på videoresursen.
1. Tryck på ikonen **[!UICONTROL Visa egenskaper]** (en cirkel med&quot;i&quot;) i verktygsfältet.
1. Tryck på **[!UICONTROL Ändra miniatyrbild]** på videons egenskapssida.
1. På sidan Ändra miniatyrbild i verktygsfältet trycker du på **[!UICONTROL Välj bildruta]**.

   Dynamic Media genererar en serie miniatyrbilder från videon baserat på det standardtidsintervall eller tidsintervall som du har anpassat.

1. Förhandsgranska de genererade miniatyrbilderna och välj sedan den som du vill lägga till i videon.
1. Tryck på **[!UICONTROL Spara ändring]**.

   Videons miniatyrbild uppdateras till att använda den miniatyrbild du valde. Om du senare bestämmer dig för att ändra miniatyrbilden kan du gå tillbaka till sidan **[!UICONTROL Ändra miniatyrbild]** och välja en ny.

   Om du har konfigurerat nya standardtidsintervall, eller om du har överfört en ny video för att ersätta den befintliga videon, måste du generera om miniatyrbilderna.

   Se [Konfigurera det standardtidsintervall som videominiatyrer genererar](#configuring-the-default-time-interval-that-video-thumbnails-are-generated).

#### Konfigurera standardtidsintervallet som videominiatyrbilder genereras {#configuring-the-default-time-interval-that-video-thumbnails-are-generated}

När du konfigurerar och sparar det nya standardtidsintervallet gäller ändringen automatiskt endast videoklipp som du överför i framtiden. Den nya standardinställningen tillämpas inte automatiskt på videoklipp som du tidigare överfört. För befintliga videofilmer måste du återskapa miniatyrbilderna.

Se [Lägga till en videominiatyr](#adding-a-video-thumbnail).

**Om du vill konfigurera det standardtidsintervall som videominiatyrbilder genereras,**

1. I AEM trycker du på **[!UICONTROL Verktyg]** > **[!UICONTROL Allmänt]** > **[!UICONTROL CRXDE Lite]**.

1. På sidan CRXDE Lite navigerar du till `o etc/dam/imageserver/configuration/jcr:content/settings.`

   Om katalogpanelen inte visas kan du behöva trycka på ikonen >> till vänster om fliken Hem.

1. Dubbeltryck på den nedre högra panelen på fliken Egenskaper `thumbnailtime`.
1. I dialogrutan Redigera miniatyrtid använder du textfälten för att ange intervallvärden som procentvärden.

   * Tryck på plustecknet (+) för att lägga till ett eller flera intervallvärdesfält. Du kan behöva rulla längst ned i dialogrutan för att se ikonen.
   * Tryck på minustecknet (-) till höger om ett intervallvärdesfält för att ta bort det från listan.
   * Tryck på ikonen med uppilen eller nedpilen för att ändra ordningen på intervallvärdena.

1. Tryck på **[!UICONTROL OK]** för att återgå till fliken Egenskaper.
1. I det övre vänstra hörnet av CRXDE Lite-sidan trycker du på **[!UICONTROL Spara alla]** och sedan på ikonen Bakåt i det övre vänstra hörnet för att återgå till AEM.

   Se [Lägga till en videominiatyr.](#adding-a-video-thumbnail)

### Lägga till en anpassad videominiatyr {#adding-a-custom-video-thumbnail-1}

De här stegen gäller endast för Dynamic Media som körs i hybridläge.

Om du **vill lägga till en anpassad videominiatyr**,

1. Navigera till en överförd videoresurs som du vill lägga till en anpassad videominiatyr.
1. I resursurvalsläget, antingen från listvyn eller kortvyn, trycker du på videoresursen.
1. Tryck på ikonen **[!UICONTROL Visa egenskaper]** (en cirkel med&quot;i&quot;) i verktygsfältet.
1. Tryck på **[!UICONTROL Ändra miniatyrbild]** på videons egenskapssida.
1. På sidan Ändra miniatyrbild i verktygsfältet trycker du på **[!UICONTROL Överför ny miniatyrbild]**.
1. Navigera till en miniatyrbild som du vill använda, markera den och tryck sedan på **[!UICONTROL Öppna]** för att börja överföra bilden till AEM. Efter överföringen måste du publicera bilden.
1. När du har överfört och publicerat bilden trycker du på **[!UICONTROL Spara ändringar]** på sidan Ändra miniatyrbild.

   Den anpassade miniatyrbilden läggs till i videon.

