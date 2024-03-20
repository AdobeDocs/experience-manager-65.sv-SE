---
title: Konfigurationsegenskaper för interaktiv kommunikation
description: Redigera standardkonfigurationsegenskaper för interaktiv kommunikation
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
content-type: reference
topic-tags: interactive-communications
docset: aem65
feature: Interactive Communication
exl-id: 09eeade6-e16d-4159-b26a-803c7201097a
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '610'
ht-degree: 0%

---

# Konfigurationsegenskaper för interaktiv kommunikation{#interactive-communications-configuration-properties}

Interaktiv kommunikation innehåller egenskaper som konfigureras automatiskt efter installation av [AEM Forms-tillägg](../../forms/using/installing-configuring-aem-forms-osgi.md) paket. Författare av interaktiv kommunikation kan redigera dessa standardkonfigurationsegenskaper med **Konfiguration av Adobe Experience Manager Web Console** sida.

Öppna **Konfiguration av Adobe Experience Manager Web Console** sida med följande URL:

`https:/[server]:[port]/<contextPath>/system/console/configMgr`

Konfigurationsegenskaperna omfattar:

* [Konfiguration av dokumentfragment](#document-fragments-configuration)
* [Skapa korrespondenskonfiguration](#create-correspondence-configuration)
* [Konfiguration av webbkanal för adaptiv form och interaktiv kommunikation](#adaptive-form-and-interactive-communication-web-channel-configuration)
* [Konfiguration av tema för adaptiv form och interaktiv kommunikation - webbkanal](#adaptive-form-and-interactive-communication-web-channel-theme-configuration)

## Konfiguration av dokumentfragment {#document-fragments-configuration}

Välj **Konfiguration av dokumentfragment** på **Konfiguration av Adobe Experience Manager Web Console** för att visa konfigurationsegenskaperna för dokumentfragment.

<table>
 <tbody> 
  <tr> 
   <td>Egenskap</td> 
   <td>Beskrivning</td> 
   <td>Standard</td> 
   <td>Godtagbara värden</td> 
  </tr> 
  <tr> 
   <td>Datavisningsformat</td> 
   <td>Språkområdesspecifikt visningsformat för fält, variabler och formulärdatamodellelement som är tillgängliga när du skapar en interaktiv kommunikation för tryck- och webbkanaler.</td> 
   <td> 
    <ul> 
     <li>locale = en_US, de_DE, fr_FR och ja_JP</li> 
     <li>dateFormat = dd-MM-yyy</li> 
     <li>numberDecimalSeparator = .</li> 
     <li>numberGroupSeparator = ,</li> 
     <li>numberUseGroupSeparator = true</li> 
    </ul> </td> 
   <td><p>—</p> </td> 
  </tr> 
  <tr> 
   <td>Indrag</td> 
   <td>Bredden på en enskild indragsenhet som används för text i listdokumentfragment.</td> 
   <td>12,7 mm</td> 
   <td>Nummer</td> 
  </tr> 
  <tr> 
   <td>Minsta bredd för romerska siffror</td> 
   <td>Minsta bredd som ska användas på punkt- eller nummerfältet när latinska nummer används i listdokumentfragment. </td> 
   <td>12,7 mm</td> 
   <td>Nummer</td> 
  </tr> 
  <tr> 
   <td>Minsta numerisk bredd</td> 
   <td>Minsta bredd som ska användas på punkt- eller nummerfältet när numrerade listor används, förutom latinska nummer i listdokumentfragment.</td> 
   <td>8,0 mm</td> 
   <td>Nummer</td> 
  </tr> 
 </tbody> 
</table>

## Skapa korrespondenskonfiguration {#create-correspondence-configuration}

Välj **Skapa korrespondenskonfiguration** på **Konfiguration av Adobe Experience Manager Web Console** för att visa konfigurationsegenskaperna för agentens användargränssnitt.

<table>
 <tbody> 
  <tr> 
   <td>Egenskap</td> 
   <td>Beskrivning</td> 
   <td>Standard</td> 
   <td>Godtagbara värden</td> 
  </tr> 
  <tr> 
   <td>Visa löst innehåll för redigering</td> 
   <td>Markera kryssrutan om du vill visa löst innehåll (faktiska värden i stället för platshållare) när du redigerar textmodulen i agentgränssnittet.</td> 
   <td>Inte markerad</td> 
   <td>Ej tillämpligt</td> 
  </tr> 
  <tr> 
   <td>Använd vattenstämpel vid förhandsvisning</td> 
   <td>Markera kryssrutan om du vill använda vattenstämpel på kanalen Skriv ut i interaktiv kommunikation i förhandsgranskningsläget.</td> 
   <td>Inte markerad</td> 
   <td>Ej tillämpligt</td> 
  </tr> 
  <tr> 
   <td>Aktivera teckensnittsinbäddning i PDF</td> 
   <td><p>Markera kryssrutan om du vill aktivera inbäddning av teckensnitt i PDF-dokument. När du har valt det här alternativet kan du bädda in nya teckensnitt när du har genererat eller förhandsgranskat PDF-dokument med hjälp av agentgränssnittet. Använd tryckkanalen i Interactive Communication för att generera och förhandsgranska PDF-dokument.</p> <p>Det är praktiskt att bädda in teckensnitt i ett PDF-dokument om det finns ett teckensnitt på en dator som används för att generera PDF och inte är tillgängligt på klientdatorn som använder PDF.</p> <p>Mer information om hur du bäddar in teckensnitt finns i <a href="../../forms/using/customize-text-editor.md" target="_blank">Anpassa textredigeraren</a>.</p> </td> 
   <td>Inte markerad</td> 
   <td>Ej tillämpligt</td> 
  </tr> 
 </tbody> 
</table>

## Konfiguration av webbkanal för adaptiv form och interaktiv kommunikation {#adaptive-form-and-interactive-communication-web-channel-configuration}

Välj **Konfiguration av webbkanal för adaptiv form och interaktiv kommunikation** på **Konfiguration av Adobe Experience Manager Web Console** för att visa konfigurationsegenskaperna för webbkanalen Adaptive Forms och Interactive Communications. I följande tabell beskrivs egenskaperna för interaktiv kommunikation:

| Egenskap | Beskrivning | Standard | Godtagbara värden |
|---|---|---|---|
| Visa platshållare | Markera kryssrutan för att aktivera visning av platshållare för fält som ingår i adaptiva formulär och interaktiv kommunikation. | Markerad | Ej tillämpligt |
| Maximalt antal cacheposter | Ange det maximala antalet adaptiva formulär och interaktiv kommunikation som kan hämtas med cacheminnet. | 100 | Nummer |
| Gör filnamnet unikt | Markera kryssrutan om du vill ha unika namn för filer inkluderade som bilagor i Adaptive Forms och Interactive Communications. | Inte markerad | Ej tillämpligt |

## Konfiguration av tema för adaptiv form och interaktiv kommunikation - webbkanal {#adaptive-form-and-interactive-communication-web-channel-theme-configuration}

Välj **Konfiguration av tema för adaptiv form och interaktiv kommunikation - webbkanal** på **Konfiguration av Adobe Experience Manager Web Console** för att visa konfigurationsegenskaperna för teman för adaptiva Forms- och interaktiva kommunikationskanaler.

<table>
 <tbody> 
  <tr> 
   <td>Egenskap</td> 
   <td>Beskrivning</td> 
   <td>Standard</td> 
   <td>Godtagbara värden</td> 
  </tr> 
  <tr> 
   <td>Namn på teckensnittslista</td> 
   <td>Lista över teckensnitt som kan användas när Adaptive Forms och Interactive Communications skapas.</td> 
   <td><p>Georgien</p> <p>Book Antiqua</p> <p>Times New Roman</p> <p>Arial</p> <p>Arial Black</p> <p>Effekt</p> <p>Palation Linotype</p> </td> 
   <td>Alla giltiga Adobe-serverteckensnitt</td> 
  </tr> 
 </tbody> 
</table>
