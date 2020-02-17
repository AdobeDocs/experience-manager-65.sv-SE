---
title: WebDAV-åtkomst
seo-title: WebDAV-åtkomst
description: Läs mer om WebDAV-åtkomst i AEM.
seo-description: Läs mer om WebDAV-åtkomst i AEM.
uuid: b0ecaa5d-5454-42df-8453-404ece734c32
contentOwner: Chiradeep Majumdar
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: content
content-type: reference
discoiquuid: 1eaf7afe-a181-45df-8766-bd564b1ad22a
translation-type: tm+mt
source-git-commit: 1c1ade947f2cbd26b35920cfd10b1666b132bcbd

---


# WebDAV-åtkomst{#webdav-access}

Så här ansluter du till AEM via WebDAV med KDE:

AEM har WebDAV-stöd som gör att du kan visa och redigera databasinnehåll. Om du ansluter via WebDAV får du direktåtkomst till innehållsdatabasen via skrivbordet. Text- och PDF-filer som läggs till i databasen via WebDAV-anslutningen indexeras automatiskt i fulltext och kan sökas igenom med standardgränssnitt för sökning och via standard-Java API:er.

## Allmänt {#general}

[Detaljerade instruktioner för olika operativsystem](/help/sites-administering/webdav-access.md#connecting-via-webdav) finns i det här dokumentet, men eftersom du i stort sett ansluter till databasen via WebDAV-protokollet pekar du på följande plats:

```xml
http://localhost:4502
```

![chlimage_1-111](assets/chlimage_1-111a.png)

Den här URL:en ger WebDAV-åtkomst till standardarbetsytan ( `crx.default`) när den är ansluten från operativsystemsnivå. Eftersom det är enklare för användaren ger det dem inte större flexibilitet att ange namn på arbetsytor, vilket kan uppnås med ytterligare [WebDAV-URL:er](/help/sites-administering/webdav-access.md#webdav-urls).

AEM visar databasinnehållet på följande sätt:

* En nod av den typen `nt:folder` visas som en mapp. Noder under `nt:folder` noden visas som mappinnehåll.

* En nod av den typen `nt:file` visas som en fil. Noder under `nt:file` noden visas inte, men de utgör filens innehåll.

När du använder WebDAV för att skapa och redigera mappar och filer skapar och redigerar AEM de nödvändiga `nt:folder` och `nt:file` noderna. Om du tänker använda WebDAV för att importera och exportera innehåll kan du försöka arbeta med `nt:file` - och `nt:folder` nodtyperna så mycket som möjligt.

>[!NOTE]
>
>Kontrollera de [tekniska kraven](/help/sites-deploying/technical-requirements.md#webdav-clients)innan du konfigurerar WebDAV.

## WebDAV-URL:er {#webdav-urls}

URL:en för WebDAV-servern har följande struktur:

<table>
 <colgroup>
  <col width="100" />
  <col width="100" />
  <col width="100" />
  <col width="100" />
  <col width="100" />
 </colgroup>
 <tbody>
  <tr>
   <td>
    <code>
     <strong>URL Component</strong>
    </code></td>
   <td><code>https://&lt;host&gt;:&lt;port&gt;</code></td>
   <td><code>/&lt;crx-webapp-path&gt;</code></td>
   <td><code>/repository</code></td>
   <td><code>/&lt;workspace&gt;</code></td>
  </tr>
  <tr>
   <td>
    <code>
     <strong>Example</strong>
    </code></td>
   <td><code>http://localhost:4502</code></td>
   <td><code>/crx</code></td>
   <td><code>/repository</code></td>
   <td><code>/crx.default</code></td>
  </tr>
  <tr>
   <td><strong>Beskrivning</strong></td>
   <td>Värd och port som AEM körs på</td>
   <td>Sökväg till webbprogrammet för AEM-databasen</td>
   <td>Sökväg till vilken WebDAV-servleten mappas</td>
   <td>Arbetsytans namn</td>
  </tr>
 </tbody>
</table>

Genom att ändra arbetsytelementet i sökvägen kan du mappa andra arbetsytor än standardarbetsytan ( `crx.default`). Om du till exempel vill mappa en arbetsyta med namnet `staging`använder du följande URL:

```xml
http://localhost:4502/crx/repository/staging
```

## Ansluta via WebDAV {#connecting-via-webdav}

[För att ansluta till din databas med hjälp av WebDAV-protokollet pekar du, som nämnts ovan](/help/sites-administering/webdav-access.md#general), din WebDAV-klient till din databasplats. Beroende på vilket operativsystem du använder skiljer sig dock stegen som krävs för att ansluta klienten åt och det kan finnas en konfiguration av operativsystemet som krävs.

Instruktioner om hur du ansluter följande operativsystem:

* [Windows](/help/sites-administering/webdav-access.md#windows)
* [macOS](/help/sites-administering/webdav-access.md#macos)
* [Linux](/help/sites-administering/webdav-access.md#linux)

### Windows {#windows}

Om du vill ansluta ett Microsoft Windows 7-system (och senare) till en AEM-instans som inte är säker med SSL, måste alternativet att upprätta grundläggande autentisering över ett oskyddat nätverk uttryckligen aktiveras i Windows. Detta kräver en ändring i Windows-registret för WebClient.

När registret har uppdaterats kan AEM-instansen mappas som en enhet.

#### Konfiguration av Windows 7 och senare {#windows-and-greater-configuration}

Så här uppdaterar du registret så att grundläggande autentisering tillåts över ett oskyddat nätverk:

1. Leta reda på följande registerundernyckel:

   ```xml
   HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\WebClient\Parameters
   ```

1. Ställ in undernyckeln för registerposten till ett värde som är `BasicAuthLevel` `2` eller större.

   Lägg till undernyckeln om den inte finns.

1. Du måste starta om systemet för att registerändringen ska börja gälla.

Mer information om den här registerändringen finns i [Microsoft Support KB 841215](https://support.microsoft.com/default.aspx/kb/841215) .

Mer information om hur du förbättrar svarstiden för WebDav-klienten i Windows finns i [Microsoft Support KB 2445570](https://support.microsoft.com/kb/2445570) .

>[!NOTE]
>
>Adobe rekommenderar att du skapar en Windows-användare med samma inloggningsuppgifter som databasanvändaren, annars kan behörighetskonflikter uppstå.

#### Konfiguration av Windows 8 {#windows-configuration}

För Windows 8 måste du också ändra registerposten [enligt beskrivningen för Windows 7 och senare](/help/sites-administering/webdav-access.md#windows-and-greater-configuration). Skrivbordsmiljö måste dock vara aktiverad för att du ska kunna se registerposten innan du kan göra detta.

Om du vill aktivera Desktop Experience öppnar du **Server Manager**, **Features**, **Add Features** och sedan **Desktop Experience**.

När registerposten som beskrivs för Windows 7 har startats om är den tillgänglig. Ändra den enligt beskrivningen för Windows 7 och senare.

#### Ansluta i Windows {#connecting-in-windows}

Så här ansluter du till AEM via WebDAV i en Windows-miljö:

1. Öppna **Utforskaren** eller **Utforskaren** och klicka på **Dator** eller **Den här datorn**.

   ![chlimage_1-112](assets/chlimage_1-112a.png)

1. Klicka på **Mappa nätverksenhet** för att starta guiden.
1. Ange mappningsinformationen:

   * **Enhet**: Välj en tillgänglig bokstav
   * **Mapp**: `http://localhost:4502`
   * Kontrollera **anslutning med andra autentiseringsuppgifter**
   Klicka på Slutför

   ![chlimage_1-113](assets/chlimage_1-113a.png)

   >[!NOTE]
   >
   >Om AEM finns på en annan port använder du portnumret i stället för 4502. Om du inte kör innehållsdatabasen på den lokala datorn ersätter du `localhost` med respektive servernamn eller IP-adress.

1. Ange användarnamn `admin` och lösenord `admin`. Adobe rekommenderar att du använder det förkonfigurerade administratörskontot för testning.

   ![chlimage_1-114](assets/chlimage_1-114a.png)

1. Guiden stängs och den nyligen mappade enheten öppnas i Utforskaren i Windows eller i Utforskaren.

   ![chlimage_1-115](assets/chlimage_1-115a.png)

Nu har AEM mappats som en enhet via WebDAV och du kan använda den som vilken enhet som helst.

### macOS {#macos}

Det krävs inga konfigurationssteg för att ansluta via WebDAV i macOS. Du behöver bara ansluta till WebDAV-servern.

1. Navigera till ett **Finder** -fönster och klicka på **Gå** och **Anslut till server** eller tryck på **Kommando+k**.
1. I fönstret **Anslut till server** anger du AEM-platsen:

   * `http://localhost:4502`
   >[!NOTE]
   >
   >Om AEM finns på en annan port använder du portnumret i stället för 4502. Om du inte kör innehållsdatabasen på den lokala datorn ersätter du `localhost` med respektive servernamn eller IP-adress.

1. Ange användarnamn `admin` och lösenord `admin`när du uppmanas till autentisering. Adobe rekommenderar att du använder det förkonfigurerade administratörskontot för testning.

macOS har nu anslutit till AEM via WebDAV och du kan använda det som vilken mapp som helst på din Mac.

### Linux {#linux}

Anslutning via WebDAV i Linux kräver ingen konfiguration, men inkluderar några steg för att skapa anslutningen som varierar beroende på datormiljön.

#### GNOME {#gnome}

Så här ansluter du till AEM via WebDAV med GNOME:

1. I Nautilus (file explorer) väljer du **Platser** och väljer **Anslut till server**.
1. I fönstret **Anslut till server** väljer du WebDAV (HTTP) i Service Type.

1. In **Server**, enter `http://localhost:4502/crx/repository/crx.default`

   >[!NOTE]
   >
   >Om AEM finns på en annan port använder du portnumret i stället för 4502. Om du inte kör innehållsdatabasen på den lokala datorn ersätter du `localhost` med respektive servernamn eller IP-adress.

1. I **Mapp** anger du `/dav`
1. Ange användarnamn `admin`. Adobe rekommenderar att du använder det förkonfigurerade administratörskontot för testning.
1. Lämna porten tom och ange ett namn för anslutningen.
1. Klicka på **Anslut**. AEM ber dig ange ditt lösenord.
1. Ange lösenordet `admin` och klicka på **Anslut**.

GNOME har nu monterat AEM som en volym och du kan använda den precis som vilken annan volym som helst.

#### KDE {#kde}

1. Öppna guiden Nätverksmapp.
1. Välj **WebFolder**(webdav) och klicka på Nästa.
1. Skriv ett anslutningsnamn i **Namn**.
1. I **Användare** anger du `admin.` Adobe rekommenderar att du använder det förkonfigurerade administratörskontot.
1. In **Server**, enter `http://localhost:4502/crx/repository/crx.default`

   >[!NOTE]
   >
   >Om AEM finns på en annan port använder du portnumret i stället för 4502. Om du inte kör innehållsdatabasen på den lokala datorn ersätter du `localhost` med respektive servernamn eller IP-adress

1. I **Mapp** anger du `dav`

1. Klicka på **Spara och anslut**.
1. Ange lösenordet när du uppmanas att ange det `admin` och klicka på **Anslut**.

KDE har nu monterat AEM som en volym och du kan använda den precis som vilken annan volym som helst.
