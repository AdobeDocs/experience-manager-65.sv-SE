---
title: Felsökningsriktlinjer för arbetsytan i AEM Forms
seo-title: Felsökningsriktlinjer för arbetsytan i AEM Forms
description: Aktivera loggar och använd felsökningsfunktionen i webbläsaren för att felsöka arbetsytan i AEM Forms.
seo-description: Aktivera loggar och använd felsökningsfunktionen i webbläsaren för att felsöka arbetsytan i AEM Forms.
uuid: 07b8c8ed-f1ff-4be5-8005-251ff7b2ac85
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 5dae9ed9-77a3-44f5-a94d-ca5c355c8730
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f

---


# Felsökningsriktlinjer för arbetsytan i AEM Forms {#troubleshooting-guidelines-for-aem-forms-workspace}

I den här artikeln beskrivs hur du felsöker arbetsytan i AEM Forms genom att aktivera loggning och använda felsökningsfunktionen i en webbläsare. Här förklaras också några vanliga problem som du kan stöta på när du använder arbetsytan i AEM Forms och deras temporära lösningar.

## Det gick inte att installera AEM Forms-arbetsytans paket {#unable-to-install-aem-forms-workspace-package}

Öppna arbetsytan i AEM Forms när du har installerat korrigeringen. Om felet Ingen resurs hittades öppnar du CRX Package Manager och installerar om `adobe-lc-workspace-pkg-<version>.zip` paketet.

Utför följande steg om du råkar ut för ett fel `javax.jcr.nodetype.ConstraintViolationException: OakConstraint0025: Authorizable property rep:authorizableId may not be removed`när du installerar paketet:

1. Logga in på CRX DE lite. Standardwebbadressen är `https://[localhost]:'port'/lc/crx/de/index.jsp`
1. Ta bort följande nod:

   `/home/groups/P/PERM_WORKSPACE_USER`

1. Gå till Package Manager. Standardwebbadressen är `https://[localhost]:'port'/lc/crx/packmgr/index.jsp.`
1. Sök efter och installera `adobe-lc-workspace-pkg-[version].zip` paketet.
1. Starta om programservern.

## Loggning på arbetsytan i AEM Forms {#aem-forms-workspace-nbsp-logging}

Du kan generera loggar på olika nivåer för att optimera felsökningen. I ett komplext program kan till exempel loggning på komponentnivå hjälpa till att felsöka och felsöka specifika komponenter.

På arbetsytan i AEM Forms:

* Om du vill få loggningsinformation om en viss komponentfil lägger du till `/log/<ComponentFile>/<LogLevel>` i URL-adressen och trycker på `Enter`. All loggningsinformation för komponentfilen på den angivna loggnivån skrivs ut på konsolen.

* Om du vill ha loggningsinformation för alla komponentfiler lägger du till `/log/all/trace` i URL:en och trycker på `Enter`.

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
   <td><p>outOfficeView</p> </td>
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

### Loggnivåer tillgängliga på arbetsytan i AEM Forms {#log-levels-available-in-nbsp-aem-forms-workspace}

* FATAL
* FEL
* VARNING
* INFORMATION
* FELSÖKNING
* TRACE
* AV

## Felsökningsinformation för webbläsare {#debugging-information-for-browsers}

Skript och format kan felsökas i olika webbläsare.

* **Felsökning i IE**: Information om hur du felsöker arbetsytan i AEM Forms i IE finns i: [https://msdn.microsoft.com/en-us/library/hh772704(v=vs.85).aspx](https://msdn.microsoft.com/en-us/library/hh772704(v=vs.85).aspx).

* **Felsökning i Chrome**: Använd kortkommandot för att öppna felsökningsprogrammet i Chrome: Ctrl+Skift+I. Mer information finns i: [https://developer.chrome.com/extensions/tut_debugging.html](https://developer.chrome.com/extensions/tut_debugging.html).

* **Felsökning i Firefox**: Det finns flera tillägg för att felsöka skript och format i Firefox. Firebug är till exempel ett sådant felsökningsverktyg ([https://getfirebug.com](https://getfirebug.com)).

## Vanliga frågor {#faqs}

1. PDF-formuläret återges inte eller skickas i Google Chrome.

   1. Installera plugin-programmet Adobe® Reader®.
   1. Öppna chrome://plugins i Chrome om du vill visa tillgängliga plugin-program.
   1. Inaktivera Chrome PDF Viewer och aktivera plugin-programmet Adobe Reader.

1. SWF-formulär eller stödlinje återges inte i Google Chrome.

   1. Öppna chrome://plugins i Chrome om du vill visa tillgängliga plugin-program.
   1. Se information om plugin-programmet för Adobe Flash® Player.
   1. Inaktivera PepperFlash under Adobe Flash Player-plugin.

1. Jag har en anpassad AEM Forms-arbetsyta, men jag kan inte se ändringarna.

   Rensa webbläsarens cacheminne och öppna sedan arbetsytan i AEM Forms.

1. Vad behöver användaren göra för att formuläret ska kunna återges i HTML när det öppnas på skrivbordet?

   Välj HTML-alternativknappen för standardprofilen i tilldelningssteget när du använder Workbench.

1. Den bifogade filen visas inte när du klickar på den.

   Aktivera popup-fönster i webbläsaren om du vill visa bilagor.

1. En användare är inloggad i ett formulärprogram. Om användaren försöker logga in på arbetsytan kanske den inte läses in om användaren inte har behörighet till arbetsytan.

   Logga ut från det andra formulärprogrammet och logga sedan in på arbetsytan.

1. HTML-formulär, använda Processegenskaper i sin design, när de återges i AEM Forms-arbetsytan, visar knappen Skicka i formuläret.

   När du utformar formulär läggs en Skicka-knapp till i formuläret när du använder Processegenskaper. När knappen Skicka återges som en PDF-fil på arbetsytan för AEM Forms visas den inte för slutanvändaren. När du återger som ett HTML-formulär på arbetsytan i AEM Forms visas knappen Skicka för slutanvändaren. Om du klickar på knappen Skicka i formuläret initieras ingen åtgärd. När du klickar på knappen Skicka längst ned på arbetsytan i AEM Forms, utanför formuläret, slutförs uppgiften.

[Kontakta supporten](https://www.adobe.com/account/sign-in.supportportal.html)
