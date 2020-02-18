---
title: Textbunden formatering av adaptiva formulärkomponenter
seo-title: Inline CSS-egenskaper för adaptiva formulärkomponenter
description: Du kan använda anpassade format på ett anpassat formulär, men du kan också använda infogade CSS-egenskaper på enskilda komponenter i ett anpassat formulär.
seo-description: Du kan använda anpassade format på ett anpassat formulär, men du kan också använda infogade CSS-egenskaper på enskilda komponenter i ett anpassat formulär.
uuid: e863780e-2250-4bea-9569-22be5638d54e
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 21dec713-c76d-408b-baea-fc585377b429
docset: aem65
translation-type: tm+mt
source-git-commit: 33f73225fbb2c48353c1f34db3339c0bb79d4236

---


# Textbunden formatering av adaptiva formulärkomponenter {#inline-styling-of-adaptive-form-components}

Du kan definiera det övergripande utseendet och formatet för ett anpassat formulär genom att ange format med [temaredigeraren](../../forms/using/themes.md). Du kan också använda infogade CSS-format på enskilda adaptiva formulärkomponenter och förhandsgranska ändringarna direkt. Inline-format åsidosätter format som finns i temat.

## Använda infogade CSS-egenskaper {#apply-inline-css-properties}

Så här lägger du till infogade format i en komponent:

1. Öppna formuläret i formulärredigeraren och ändra läget till formateringsläge. Om du vill ändra läget till ett formateringsläge trycker du på ![arbetsytelistrutan](assets/canvas-drop-down.png) > **Format** i sidverktygsfältet.
1. Markera en komponent på sidan och tryck på redigeringsknappens ![redigeringsknapp](assets/edit-button.png). Stilegenskaper öppnas i sidofältet.

   Du kan också välja komponenter från formulärhierarkiträdet i sidlisten. Formulärhierarkiträdet är tillgängligt som formulärobjekt i sidlisten.

   Du kan också välja en komponent i sidofältet. I stilläget kan du se komponenter som listas under Formulärobjekt. Formulärobjektslistan i sidofältet visar dock komponenter som fält och paneler. Fält och paneler är generiska komponenter som kan innehålla komponenter som textrutor och alternativknappar.

   När du väljer en komponent i sidofältet visas alla underkomponenter i listan och egenskaperna för den markerade komponenten. Du kan markera en viss underkomponent och formatera den.

1. Klicka på en flik i sidofältet för att ange CSS-egenskaper. Du kan ange egenskaper som:

   * Mått och position (visningsinställning, utfyllnad, höjd, bredd, marginal, position, z-index, flyttal, klar, spill)
   * Text (teckensnittsfamilj, vikt, färg, storlek, radhöjd och justering)
   * Bakgrund (bild och övertoning, bakgrundsfärg)
   * Kant (bredd, stil, färg, radie)
   * Effekter (skugga, opacitet)
   * Avancerat (Gör att du kan skriva anpassad CSS för komponenten)

1. På samma sätt kan du använda format för andra delar av en komponent, till exempel widget, bildtext och Hjälp.
1. Tryck på **Klar** för att bekräfta ändringarna eller **Avbryt** för att ignorera ändringarna.

## Exempel: infogade format för en fältkomponent {#example-inline-styles-for-a-field-component}

Följande bilder visar ett textfält före och efter att infogade format har använts på det.

![Textrutekomponent innan intern formatering används](assets/no-style.png)

Textrutekomponent innan infogade formategenskaper används

Lägg märke till ändringen i textrutans format, så som visas i följande bild, när du har använt följande CSS-egenskaper.

<table>
 <tbody>
  <tr>
   <td><p>Väljare</p> </td>
   <td><p>CSS-egenskap</p> </td>
   <td><p>Värde</p> </td>
   <td><p>Effekt</p> </td>
  </tr>
  <tr>
   <td><p>Fält</p> </td>
   <td><p>border</p> </td>
   <td><p>Kantbredd =2px</p> <p>Kantstil=Heldragen</p> <p>Kantfärg=#1111</p> </td>
   <td><p>Skapar en svart 2px bred kant runt fältet</p> </td>
  </tr>
  <tr>
   <td><p>Textruta</p> </td>
   <td><p>background-color</p> </td>
   <td><p>#6495ED</p> </td>
   <td><p>Ändrar bakgrundsfärgen till CornflowerBlue (#6495ED)</p> <p>Obs! Du kan ange ett färgnamn eller dess hexadecimala kod i värdefältet.</p> </td>
  </tr>
  <tr>
   <td><p>Etikett</p> </td>
   <td><p>Mått och position &gt; bredd</p> </td>
   <td><p>100px</p> </td>
   <td><p>Fastställer bredden som 100px för etiketten</p> </td>
  </tr>
  <tr>
   <td>Ikon för fälthjälp</td>
   <td>Text &gt; Teckenfärg</td>
   <td>#2ECC40</td>
   <td>Ändrar färgen på hjälpikonens ansikte.</td>
  </tr>
  <tr>
   <td><p>Lång beskrivning</p> </td>
   <td><p>textjustering</p> </td>
   <td><p>mitten</p> </td>
   <td><p>Justerar den långa beskrivningen för att få hjälp att centrera</p> </td>
  </tr>
 </tbody>
</table>

![Textrutans format efter infogad formatering](assets/applied-style.png)

Textrutekomponent efter användning av egenskaper för infogat format

Följ stegen ovan för att markera och formatera andra komponenter, till exempel paneler, skicka-knappar och alternativknappar.

>[!NOTE]
>
>Stilegenskaperna varierar beroende på vilken komponent du väljer.

