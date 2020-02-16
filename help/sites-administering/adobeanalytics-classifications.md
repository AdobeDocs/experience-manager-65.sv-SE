---
title: Adobe-klassificeringar
seo-title: Adobe-klassificeringar
description: Läs om Adobe Classifications.
seo-description: Läs om Adobe Classifications.
uuid: 57fb59f4-da90-4fe7-a5b1-c3bd51159a16
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 6787511a-2ce0-421a-bcfb-90d5f32ad35e
translation-type: tm+mt
source-git-commit: a833a34bbeb938c72cdb851a46b2ffd97aee9f6d

---


# Adobe-klassificeringar{#adobe-classifications}

Med Adobe Classifications exporteras klassificeringsdata till [Adobe Analytics](/help/sites-administering/adobeanalytics.md) på ett schemalagt sätt. Exportören är en implementering av en **com.adobe.cq.scheduled.exporting.Exporter**.

Så här konfigurerar du:

1. Navigera via **Verktyg, Cloud-tjänster** till avsnittet **Adobe Analytics** .
1. Lägg till en ny konfiguration. Du kommer att se att konfigurationsmallen för **Adobe Analytics-klassificeringar** visas under **Adobe Analytics Framework** -konfigurationen. Ange **titel** och **namn** :

   ![aa-25](assets/aa-25.png)

1. Klicka på **Skapa** för att konfigurera inställningarna.

   ![chlimage_1](assets/chlimage_1a.png)

   Egenskaperna är följande:

   | **Fält** | **Beskrivning** |
   |---|---|
   | Aktiverad | Välj **Ja** om du vill aktivera inställningarna för Adobe-klassificeringar. |
   | Skriv över vid konflikt | Välj **Ja** om du vill skriva över datakollisioner. Som standard är inställningen **Nej**. |
   | Ta bort bearbetade | Om du anger **Ja** tas bearbetade noder bort när de har exporterats. Standardvärdet är **False**. |
   | Exportera jobbbeskrivning | Ange en beskrivning för Adobe Classifications-jobbet. |
   | E-postmeddelande | Ange en e-postadress för Adobe Classifications-meddelanden. |
   | Report Suite | Ange den rapportsvit som du vill köra importjobbet för. |
   | Datauppsättning | Ange det datauppsättningsrelations-ID som importjobbet ska köras för. |
   | Transformator | Välj en transformatorimplementering i listrutan. |
   | Datakälla | Navigera till sökvägen för databehållaren. |
   | Exportera schema | Välj schema för exporten. Standardvärdet är var 30:e minut. |

1. Klicka på **OK** för att spara inställningarna.

## Ändra sidstorlek {#modifying-page-size}

Poster behandlas på sidor. Som standard skapas sidor med sidstorleken 1 000 i Adobe Classifications.

En sida kan vara högst 25 000 per definition i Adobe Classifications och kan ändras från Felix-konsolen. Vid exporten låses källnoden av Adobe Classifications för att förhindra samtidiga ändringar. Noden låses upp efter export, vid fel eller när sessionen stängs.

Så här ändrar du sidstorlek:

1. Gå till OSGI-konsolen på **https://&lt;värd>:&lt;port>/system/console/configMgr** och välj **Adobe AEM Classifications Exporter**.

   ![aa-26](assets/aa-26.png)

1. Uppdatera **Exportera sidstorlek** efter behov och klicka sedan på **Spara**.

## SAINTDefaultTransformer {#saintdefaulttransformer}

>[!NOTE]
>
>Adobe Classifications kallades tidigare SAINT Exporter.

En exportör kan använda en transformator för att omforma exportdata till ett visst format. För Adobe-klassificeringar har ett undergränssnitt `SAINTTransformer<String[]>` som implementerar Transformer-gränssnittet angetts. Det här gränssnittet används för att begränsa den datatyp `String[]` som används av SAINT API och för att ha ett markörgränssnitt för att hitta sådana tjänster för markering.

I standardimplementeringen SAINTDefaultTransformer behandlas de underordnade resurserna för exportörkällan som poster med egenskapsnamn som nycklar och egenskapsvärden som värden. Kolumnen **Nyckel** läggs automatiskt till som första kolumn - dess värde blir nodnamnet. Namngivna egenskaper (som innehåller `:`) ignoreras.

*Nodstruktur:*

* id-klassificering `nt:unstructured`

   * 1 `nt:unstructured`

      * Produkt = Mitt produktnamn (sträng)
      * Price = 120.90 (String)
      * Size = M (String)
      * Color = black (String)
      * Color^Code = 101 (String)

**SAINT Header &amp; Record:**

| **Nyckel** | **Produkt** | **Pris** | **Storlek** | **Färg** | **Color^Code** |
|---|---|---|---|---|---|
| 1 | Mitt produktnamn | 120.90 | M | svart | 101 |

Egenskaperna är följande:

<table>
 <tbody>
  <tr>
   <td><strong>Egenskapssökväg</strong></td>
   <td><strong>Beskrivning</strong></td>
  </tr>
  <tr>
   <td>transformator</td>
   <td>Ett klassnamn för en SAINTTransformer-implementering</td>
  </tr>
  <tr>
   <td>e-post</td>
   <td>E-postadress för avisering.</td>
  </tr>
  <tr>
   <td>reportsuites</td>
   <td>Rapportera Suite-ID:n som importjobbet ska köras för. </td>
  </tr>
  <tr>
   <td>datauppsättning</td>
   <td>Datauppsättningsrelations-ID som importjobbet ska köras för. </td>
  </tr>
  <tr>
   <td>description</td>
   <td>Jobbbeskrivning. <br /> </td>
  </tr>
  <tr>
   <td>skriv över</td>
   <td>Flagga för att skriva över datakollisioner. Standardvärdet är <strong>false</strong>.</td>
  </tr>
  <tr>
   <td>indelningar</td>
   <td>Flagga för att kontrollera om rapportsviterna är kompatibla. Standardvärdet är <strong>true</strong>.</td>
  </tr>
  <tr>
   <td>borttagen</td>
   <td>Flagga för att ta bort de bearbetade noderna efter exporten. Standardvärdet är <strong>false</strong>.</td>
  </tr>
 </tbody>
</table>

## Automatisera export av Adobe-klassificeringar {#automating-adobe-classifications-export}

Du kan skapa ett eget arbetsflöde, så att alla nya importer startar arbetsflödet för att skapa lämpliga, och korrekt strukturerade, data i **/var/export/** så att de kan exporteras till Adobe Classifications.
