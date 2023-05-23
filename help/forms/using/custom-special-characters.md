---
title: Anpassade specialtecken i korrespondenshantering
seo-title: Custom special characters in Correspondence Management
description: Lär dig hur du lägger till anpassade specialtecken i Correspondence Management.
seo-description: Learn how to add custom special characters in Correspondence Management.
uuid: a1890f6d-8e0c-471f-a9bd-861acf1f17e6
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
discoiquuid: 9f26565c-a7ba-4e9e-bf77-a95eb8e351f2
docset: aem65
feature: Correspondence Management
exl-id: 3e978c3e-12f2-4dc6-801d-8ab4c5df6700
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '636'
ht-degree: 0%

---

# Anpassade specialtecken i korrespondenshantering{#custom-special-characters-in-correspondence-management}

## Översikt {#overview}

Correspondence Management har inbyggt standardstöd för 210 specialtecken som du enkelt kan infoga med bokstäver.

Du kan till exempel infoga följande specialtecken:

* Valutasymboler som €,¥ och £
* Matematiska symboler som t.ex.¥, Ð och ^
* Interpunktionssymboler som ‟ och &quot;

Du kan infoga specialtecken med bokstäver:

* I [textredigerare](/help/forms/using/document-fragments.md#createtext)
* I en [redigerbar, infogad modul i korrespondens](../../forms/using/create-correspondence.md#managecontent)

![specialteckensinlinemodulen](assets/specialcharactersinlinemodule.png)

Administratören kan lägga till stöd för fler/anpassade specialtecken genom anpassning. I den här artikeln finns instruktioner om hur du kan lägga till stöd för ytterligare anpassade specialtecken.

## Lägga till eller ändra stöd för anpassade specialtecken i Correspondence Management {#creatingfolderstructure}

Följ de här stegen för att lägga till stöd för anpassade specialtecken:

1. Gå till `https://'[server]:[port]'/[ContextPath]/crx/de` och logga in som administratör.
1. Skapa en mapp med namnet i appmappen **[!UICONTROL specialcharacters]** med en sökväg/struktur som liknar specialteckenmappen (finns i mappen textEditorConfig under libs):

   1. Högerklicka på **specialtecken** mapp på följande sökväg och välj **Överläggsnod**:

      `/libs/fd/cm/ma/gui/configuration/textEditorConfig/specialcharacters`

   1. Kontrollera att dialogrutan Overlay Node har följande värden:

      **Sökväg:** /libs/fd/cm/ma/gui/configuration/textEditorConfig/specialtecken

      **Plats för övertäckning:** /apps/

      **Matcha nodtyper:** Markerad

      >[!NOTE]
      >
      >Gör inga ändringar i grenen /libs. Alla ändringar du gör kan gå förlorade eftersom den här grenen kan ändras när du:
      >
      >
      >
      >    * Uppgradera till din instans
      >    * Använd en snabbkorrigering
      >    * Installera ett funktionspaket


   1. Klicka **OK** och sedan klicka **Spara alla**. Mappen med specialtecken skapas i den angivna sökvägen.

      Kontrollera nodstrukturtaggar när du har skapat övertäckningen. Varje nod som skapas i /apps med övertäckningen ska ha samma klass och egenskaper som definieras i /libs för den noden. Om någon egenskap eller tagg saknas i nodstrukturen under /apps-platsen synkroniserar du dess taggar med motsvarande nod i /libs.

1. Se till att **[!UICONTROL textEditorConfig]** noden har följande egenskaper och värden:

   | Namn | Typ | Värde |
   |---|---|---|
   | cmConfigurationType | Sträng | cmTextEditorConfiguration |
   | cssPath | Sträng | /libs/fd/cm/ma/gui/components/admin/createasset/textcontrol/clientlibs/textcontrol |

1. Högerklicka på **[!UICONTROL specialcharacters]** mapp på följande sökväg och välj **Skapa > Underordnad nod** och sedan klicka **Spara alla**:

   /apps/fd/cm/ma/gui/configuration/textEditorConfig/specialcharacters/&lt;yourchildnode>

1. Uppdatera sidan för textredigeraren\Skapa korrespondensgränssnitt. Noden som du har lagt till är den sista i listan med specialtecken i användargränssnittet.
1. Klicka **Spara alla**.
1. Gör önskade ändringar av specialtecknen:

<table>
 <tbody>
  <tr>
   <td><strong>Till...</strong></td>
   <td><strong>Utför följande steg</strong></td>
  </tr>
  <tr>
   <td>Lägga till ett eget specialtecken</td>
   <td>
    <ol>
     <li>Lägg till en underordnad nod under "/apps/fd/cm/ma/gui/configuration/textEditorConfig/specialcharacters" med obligatoriska egenskaper.</li>
     <li>Klicka på Spara alla</li>
     <li>Uppdatera textredigeraren\Skapa korrespondensgränssnitt för att se ändringarna.</li>
    </ol> </td>
  </tr>
  <tr>
   <td>Uppdatera ett befintligt specialteckens egenskaper</td>
   <td>
    <ol>
     <li>Lägg över noden som ska uppdateras enligt ovan och verifiera taggar och klasser.</li>
     <li>Ändra alla värden, till exempel bildtext, värde, endValue och multipleCaption. </li>
     <li>Klicka på Spara alla. </li>
     <li>Uppdatera textredigeraren\Skapa korrespondensgränssnitt för att se ändringarna.</li>
    </ol> </td>
  </tr>
  <tr>
   <td>Dölja ett specialtecken</td>
   <td>
    <ol>
     <li>Täck över noden som ska döljas under "/apps/fd/cm/ma/gui/configuration/textEditorConfig/specialtecken"</li>
     <li>Lägg till egenskapen sling:hideResource (Boolean) till noden (under program) som ska döljas. </li>
     <li>Klicka på Spara alla. </li>
     <li>Uppdatera textredigeraren\Skapa korrespondensgränssnitt för att se ändringarna.<br /> </li>
    </ol> </td>
  </tr>
  <tr>
   <td>Dölj flera specialtecken</td>
   <td>
    <ol>
     <li>Lägg till egenskapen "sling:hideChildren (String eller String[])" i "/apps/fd/cm/ma/gui/configuration/textEditorConfig/specialcharacters". </li>
     <li>Lägg till nodnamn (specialtecken som ska döljas) som värden för egenskapen "sling:hideChildren". </li>
     <li>Klicka på Spara alla. </li>
     <li>Uppdatera textredigeraren\Skapa korrespondensgränssnitt för att se ändringarna.<br /> </li>
    </ol> </td>
  </tr>
  <tr>
   <td>Ordna specialtecken</td>
   <td>
    <ol>
     <li>Lägg till en underordnad nod under "/apps/fd/cm/ma/gui/configuration/textEditorConfig/specialcharacters" med obligatoriska egenskaper. </li>
     <li>Lägg till egenskapen "sling:orderBefore (String)" i den nyskapade underordnade noden. </li>
     <li>Lägg till nodnamn som ett värde innan det nya specialtecknet visas. </li>
     <li>Klicka på Spara alla. </li>
     <li>Uppdatera textredigeraren\Skapa korrespondensgränssnitt för att se ändringarna.<br /> </li>
    </ol> </td>
  </tr>
 </tbody>
</table>
