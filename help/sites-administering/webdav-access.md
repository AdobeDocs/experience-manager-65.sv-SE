---
title: WebDAV-åtkomst
description: Läs om hur du får åtkomst till Adobe Experience Manager med WebDAV.
contentOwner: Chiradeep Majumdar
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: content
content-type: reference
exl-id: 891ee66c-e49c-4561-8fef-e6e448a8aa1c
solution: Experience Manager, Experience Manager Sites
feature: Administering
role: Admin
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '1118'
ht-degree: 1%

---

# WebDAV-åtkomst{#webdav-access}

Så här ansluter du till AEM via WebDAV med KDE:

AEM har WebDAV-stöd som gör att du kan visa och redigera databasinnehåll. Om du ansluter via WebDAV får du direktåtkomst till innehållsdatabasen via skrivbordet. Text- och PDF-filer som läggs till i databasen via WebDAV-anslutningen indexeras automatiskt i fulltext och kan sökas igenom med standardsökgränssnitten och via Java™-API:erna.

## Allmänt {#general}

[Detaljerade instruktioner per operativsystem](/help/sites-administering/webdav-access.md#connecting-via-webdav) ingår i det här dokumentet, men för att ansluta till databasen med WebDAV-protokollet pekar du din WebDAV-klient på följande plats:

```xml
http://localhost:4502
```

![chlimage_1-111](assets/chlimage_1-111a.png)

Den här URL:en ger WebDAV-åtkomst till standardarbetsytan när den är ansluten från operativsystemsnivå ( `crx.default`). Eftersom det är enklare för användaren ger det dem inte större flexibilitet att ange namn på arbetsytor, vilket kan göras med ytterligare [WebDAV-URL](/help/sites-administering/webdav-access.md#webdav-urls).

AEM visar databasinnehållet på följande sätt:

* En nod av typen `nt:folder` visas som en mapp. Noder under `nt:folder` noden visas som mappinnehåll.

* En nod av typen `nt:file` visas som en fil. Noder under `nt:file` noden visas inte, men utgör filens innehåll.

När du använder WebDAV för att skapa och redigera mappar och filer skapar och redigerar AEM de nödvändiga `nt:folder` och `nt:file` noder. Om du tänker använda WebDAV för att importera och exportera innehåll kan du försöka arbeta med `nt:file` och `nt:folder` nodtyper så mycket som möjligt.

>[!NOTE]
>
>Innan du konfigurerar WebDAV bör du kontrollera [Tekniska krav](/help/sites-deploying/technical-requirements.md#webdav-clients).

## WebDAV-URL {#webdav-urls}

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
   <td>Sökväg till webbprogrammet AEM databasen</td>
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

[Såsom nämns ovan](/help/sites-administering/webdav-access.md#general)för att ansluta till din databas med hjälp av WebDAV-protokollet pekar du din WebDAV-klient till din databasplats. Beroende på vilket operativsystem du använder skiljer sig dock stegen som används för att ansluta klienten åt och det kan finnas en nödvändig konfiguration av operativsystemet.

Anvisningar om hur du ansluter följande operativsystem finns:

* [Windows](/help/sites-administering/webdav-access.md#windows)
* [macOS](/help/sites-administering/webdav-access.md#macos)
* [Linux](/help/sites-administering/webdav-access.md#linux)

### Windows {#windows}

Om du vill ansluta ett Microsoft® Windows 7-system (och senare) till en AEM som inte är säker med SSL, måste du uttryckligen aktivera alternativet att upprätta grundläggande autentisering över ett oskyddat nätverk i Windows. Den här funktionen kräver en ändring i Windows-registret för WebClient.

När registret har uppdaterats kan den AEM instansen mappas som en enhet.

#### Konfiguration av Windows 7 och senare {#windows-and-greater-configuration}

Så här uppdaterar du registret så att grundläggande autentisering tillåts över ett oskyddat nätverk:

1. Leta reda på följande registerundernyckel:

   ```xml
   HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\WebClient\Parameters
   ```

1. Ange `BasicAuthLevel` undernyckel till registerpost till värdet `2` eller större.

   Lägg till undernyckeln om den inte finns.

1. Starta om systemet för att registerändringen ska börja gälla.

>[!NOTE]
>
>Adobe rekommenderar att du skapar en Windows-användare med samma inloggningsuppgifter som databasanvändaren, annars kan behörighetskonflikter uppstå.

#### Konfiguration av Windows 8 {#windows-configuration}

För Windows 8 ändrar du registerposten [enligt beskrivning för Windows 7 och senare](/help/sites-administering/webdav-access.md#windows-and-greater-configuration). Skrivbordsmiljö måste dock aktiveras för att registerposten ska kunna visas innan du utför den här åtgärden.

Om du vill aktivera Skrivbordsmiljö öppnar du **Serverhanteraren** sedan **Funktioner** sedan **Lägg till funktioner** sedan **Skrivbordsmiljö**.

Efter omstart är registerposten som beskrivs för Windows 7 och senare tillgänglig. Ändra den enligt beskrivningen för Windows 7 och senare.

#### Ansluta i Windows {#connecting-in-windows}

Så här ansluter du till AEM via WebDAV i en Windows-miljö:

1. Öppna **Utforskaren** eller **Utforskaren** och klicka **Dator** eller **Den här datorn**.

   ![chlimage_1-112](assets/chlimage_1-112a.png)

1. Starta guiden genom att klicka **Mappa nätverksenhet**.
1. Ange mappningsinformationen:

   * **Drive**: Välj en tillgänglig bokstav
   * **Mapp**: `http://localhost:4502`
   * Kontrollera **Anslut med olika autentiseringsuppgifter**

   Klicka på Slutför

   ![chlimage_1-113](assets/chlimage_1-113a.png)

   >[!NOTE]
   >
   >Om AEM finns på en annan port använder du portnumret i stället för 4502. Om du inte kör innehållsdatabasen på den lokala datorn ersätter du `localhost` med respektive servernamn eller IP-adress.

1. Ange användarnamn `admin` och lösenord `admin`. Adobe rekommenderar att du använder det förkonfigurerade administratörskontot för testning.

   ![chlimage_1-114](assets/chlimage_1-114a.png)

1. Guiden stängs och den nyligen mappade enheten öppnas i Utforskaren i Windows eller i Utforskaren.

   ![chlimage_1-115](assets/chlimage_1-115a.png)

Windows har nu mappat AEM som en enhet via WebDAV och du kan använda den som vilken enhet som helst.

### macOS {#macos}

Det krävs inga konfigurationssteg för att ansluta via WebDAV på macOS. Du kan ansluta till WebDAV-servern.

1. Navigera till alla **Finder** fönster och klicka **Gå** och **Anslut till server** eller tryck **Kommando+k**.
1. I **Anslut till server** anger du AEM plats:

   * `http://localhost:4502`

   >[!NOTE]
   >
   >Om AEM finns på en annan port använder du portnumret i stället för 4502. Om du inte kör innehållsdatabasen på den lokala datorn ersätter du `localhost` med respektive servernamn eller IP-adress.

1. Ange användarnamn när du uppmanas till autentisering `admin` och lösenord `admin`. Adobe rekommenderar att du använder det förkonfigurerade administratörskontot för testning.

macOS har nu anslutit till AEM via WebDAV och du kan använda det som vilken mapp som helst på din Mac.

### Linux® {#linux}

Anslutning via WebDAV i Linux® kräver ingen konfiguration, men det krävs några steg för att skapa anslutningen som varierar beroende på datormiljön.

#### GNOME {#gnome}

Så här ansluter du till AEM via WebDAV med GNOME:

1. I Nautilus (file explorer) väljer du **Platser** och markera **Anslut till server**.
1. I **Anslut till server** väljer du WebDAV (HTTP) i Service Type.

1. I **Server**, ange `http://localhost:4502/crx/repository/crx.default`

   >[!NOTE]
   >
   >Om AEM finns på en annan port använder du portnumret i stället för 4502. Om du inte kör innehållsdatabasen på den lokala datorn ersätter du `localhost` med respektive servernamn eller IP-adress.

1. I **Mapp**, ange `/dav`
1. Ange användarnamnet `admin`. Adobe rekommenderar att du använder det förkonfigurerade administratörskontot för testning.
1. Lämna porten tom och ange ett namn för anslutningen.
1. Klicka **Anslut**. AEM ber dig ange ditt lösenord.
1. Ange lösenordet `admin` och klicka **Anslut**.

GNOME har nu monterat AEM som en volym och du kan använda den som vilken annan volym som helst.

#### KDE {#kde}

1. Öppna guiden Nätverksmapp.
1. Välj **WebFolder**(webdav) och klicka på Nästa.
1. I **Namn** skriver du ett anslutningsnamn.
1. I **Användare**, ange `admin.` Adobe rekommenderar att du använder det förkonfigurerade administratörskontot.
1. I **Server**, ange `http://localhost:4502/crx/repository/crx.default`

   >[!NOTE]
   >
   >Om AEM finns på en annan port använder du portnumret i stället för 4502. Om du inte kör innehållsdatabasen på den lokala datorn ersätter du `localhost` med respektive servernamn eller IP-adress

1. I **Mapp**, ange `dav`

1. Klicka **Spara och anslut**.
1. Ange lösenordet när du uppmanas att ange ditt lösenord `admin` och klicka **Anslut**.

KDE har nu monterat AEM som en volym och du kan använda den som vilken annan volym som helst.
