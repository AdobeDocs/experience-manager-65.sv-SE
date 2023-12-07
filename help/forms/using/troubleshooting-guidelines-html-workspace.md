---
title: Felsökningsriktlinjer för arbetsytan i AEM Forms
description: Aktivera loggar och använd felsökningsfunktionen i webbläsaren för att felsöka AEM Forms arbetsyta.
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: a054b60a-5e89-4c98-87bc-35669988d160
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '704'
ht-degree: 0%

---

# Felsökningsriktlinjer för arbetsytan i AEM Forms {#troubleshooting-guidelines-for-aem-forms-workspace}

I den här artikeln beskrivs hur du felsöker arbetsytan i AEM Forms genom att aktivera loggning och använda felsökningsfunktionen i en webbläsare. Här förklaras också några vanliga problem som du kan stöta på när du använder AEM Forms arbetsyta och deras temporära lösningar.

## Det går inte att installera AEM Forms-arbetsytans paket {#unable-to-install-aem-forms-workspace-package}

Öppna arbetsytan i AEM Forms när du har installerat korrigeringen. Om felet Ingen resurs hittades öppnar du CRX Package Manager och installerar om `adobe-lc-workspace-pkg-<version>.zip` paket.

Om ett fel uppstår när paketet installeras `javax.jcr.nodetype.ConstraintViolationException: OakConstraint0025: Authorizable property rep:authorizableId may not be removed`utför du följande steg:

1. Logga in på CRXDE Lite. Standardwebbadressen är `https://[localhost]:'port'/lc/crx/de/index.jsp`
1. Ta bort följande nod:

   `/home/groups/P/PERM_WORKSPACE_USER`

1. Gå till Package Manager. Standardwebbadressen är `https://[localhost]:'port'/lc/crx/packmgr/index.jsp.`
1. Sök efter och installera `adobe-lc-workspace-pkg-[version].zip` paket.
1. Starta om programservern.

## Logga på arbetsytan i AEM Forms {#aem-forms-workspace-nbsp-logging}

Du kan generera loggar på olika nivåer för att optimera felsökningen. I ett komplext program kan till exempel loggning på komponentnivå hjälpa till att felsöka och felsöka specifika komponenter.

I AEM Forms:

* Om du vill hämta loggningsinformation om en viss komponentfil lägger du till `/log/<ComponentFile>/<LogLevel>` i webbadressen och tryck på `Enter`. All loggningsinformation för komponentfilen på den angivna loggnivån skrivs ut på konsolen.

* Om du vill hämta loggningsinformation för alla komponentfiler lägger du till `/log/all/trace` i webbadressen och tryck på `Enter`.

* Loggformat: `<Component file> <Date>:<Time>: <Log Level> : <Log Message>`

>[!NOTE]
>
>Som standard är loggnivån för alla komponenter inställd på INFO.

* Loggnivån som angetts av användaren bevaras endast för den webbläsarsessionen. När användaren uppdaterar sidan ställs loggnivån in på sitt ursprungliga värde för alla komponenter.

### Lista över komponentfiler på arbetsytan i AEM Forms {#list-of-component-files-in-nbsp-aem-forms-workspace}

<table>
 <tbody>
  <tr>
   <td><p>allcategoryModel</p> </td>
   <td><p>processinstanceModel</p> </td>
   <td><p>tasklistModel</p> </td>
  </tr>
  <tr>
   <td><p>appnavigationModel</p> </td>
   <td><p>processInstanceView</p> </td>
   <td><p>aktivitetslistaVisa</p> </td>
  </tr>
  <tr>
   <td><p>appnavigationView</p> </td>
   <td><p>procesnamelistModel</p> </td>
   <td><p>taskModel</p> </td>
  </tr>
  <tr>
   <td><p>ccategoryListModel</p> </td>
   <td><p>procesnamelistView</p> </td>
   <td><p>taskView</p> </td>
  </tr>
  <tr>
   <td><p>categoryListView</p> </td>
   <td><p>processnameModel</p> </td>
   <td><p>teamqueuesView</p> </td>
  </tr>
  <tr>
   <td><p>categoryModel</p> </td>
   <td><p>processnameView</p> </td>
   <td><p>todoView</p> </td>
  </tr>
  <tr>
   <td><p>categoryView</p> </td>
   <td><p>sökmallarinformationVisa</p> </td>
   <td><p>trackingView</p> </td>
  </tr>
  <tr>
   <td><p>favoritkategoriModell</p> </td>
   <td><p>sharequeueModel</p> </td>
   <td><p>uisettingsModel</p> </td>
  </tr>
  <tr>
   <td><p>filterlistView</p> </td>
   <td><p>sharequeueView</p> </td>
   <td><p>uisettingsView</p> </td>
  </tr>
  <tr>
   <td><p>filterView</p> </td>
   <td><p>startpointlistModel</p> </td>
   <td><p>userinfoModel</p> </td>
  </tr>
  <tr>
   <td><p>outofofficeModel</p> </td>
   <td><p>startpointlistView</p> </td>
   <td><p>userinfoView</p> </td>
  </tr>
  <tr>
   <td><p>outtofofficeView</p> </td>
   <td><p>startpointModel</p> </td>
   <td><p>usersearchModel</p> </td>
  </tr>
  <tr>
   <td><p>preferencesView</p> </td>
   <td><p>startpointView</p> </td>
   <td><p>usersearchView</p> </td>
  </tr>
  <tr>
   <td><p>procesinstancehistoryView</p> </td>
   <td><p>startProcessView</p> </td>
   <td><p>wserrorModel</p> </td>
  </tr>
  <tr>
   <td><p>processinstancelistModel</p> </td>
   <td><p>starprocessView</p> </td>
   <td><p>wserrorView</p> </td>
  </tr>
  <tr>
   <td><p>procesinstancelistView</p> </td>
   <td><p>uppgifterinformationVisa</p> </td>
   <td><p>wsmessageView</p> </td>
  </tr>
 </tbody>
</table>

### Loggnivåer som är tillgängliga på arbetsytan i AEM Forms {#log-levels-available-in-nbsp-aem-forms-workspace}

* FATAL
* FEL
* VARNING
* INFO
* FELSÖKNING
* TRACE
* AV

## Felsökningsinformation för webbläsare {#debugging-information-for-browsers}

Skript och format kan felsökas i olika webbläsare.

* **Felsökning i IE**: Information om hur du felsöker AEM Forms arbetsyta i IE finns i: [https://learn.microsoft.com/en-us/office/dev/add-ins/testing/debug-add-ins-using-f12-tools-ie](https://learn.microsoft.com/en-us/office/dev/add-ins/testing/debug-add-ins-using-f12-tools-ie).

* **Felsökning i Chrome**: Om du vill öppna felsökningsprogrammet i Chrome använder du kortkommandot: Ctrl+Skift+I. Mer information finns i: [https://developer.chrome.com/docs/extensions/mv3/tut_debugging/](https://developer.chrome.com/docs/extensions/mv3/tut_debugging/).

* **Felsöka i Firefox**: Flera tillägg finns tillgängliga för felsökning av skript och format i Firefox. Firebug är till exempel ett sådant felsökningsverktyg ([https://getfirebug.com](https://getfirebug.com)).

## Vanliga frågor {#faqs}

1. Formuläret PDF återges inte eller skickas i Google Chrome.

   1. Installera plugin-programmet Adobe® Reader®.
   1. Öppna chrome://plugins i Chrome om du vill visa tillgängliga plugin-program.
   1. Inaktivera Chrome PDF Viewer-plugin och aktivera Adobe Reader-plugin.

1. Formuläret eller stödlinjen SWF återges inte i Google Chrome.

   1. Öppna chrome://plugins i Chrome om du vill visa tillgängliga plugin-program.
   1. Mer information finns i Adobe Flash® Player.
   1. Inaktivera PepperFlash under plugin-programmet för Adobe Flash Player.

1. Jag har anpassat AEM Forms-arbetsytan men kan inte se ändringarna.

   Rensa webbläsarens cacheminne och öppna sedan arbetsytan i AEM Forms.

1. Vad behöver användaren göra för att formuläret ska kunna återges i HTML när det öppnas på skrivbordet?

   Markera alternativknappen HTML för standardprofil i tilldelningssteget när du använder Workbench.

1. Den bifogade filen visas inte när du klickar på den.

   Aktivera popup-fönster i webbläsaren om du vill visa bilagor.

1. En användare är inloggad i ett formulärprogram. Om användaren försöker logga in på arbetsytan kanske den inte läses in om användaren inte har behörighet till arbetsytan.

   Logga ut från det andra formulärprogrammet och logga sedan in på arbetsytan.

1. HTML-formulär, använda Processegenskaper i sin design, när de återges i AEM Forms arbetsyta, visar Skicka-knappen i formuläret.

   När du utformar formulär läggs en Skicka-knapp till i formuläret när du använder Processegenskaper. När knappen Skicka återges som en PDF i AEM Forms-arbetsytan visas den inte för slutanvändaren. När du återger formuläret HTML i AEM Forms visas knappen Skicka för slutanvändaren. Om du klickar på knappen Skicka i formuläret initieras ingen åtgärd. Slutför uppgiften genom att klicka på Skicka längst ned på arbetsytan i AEM Forms utanför formuläret.
