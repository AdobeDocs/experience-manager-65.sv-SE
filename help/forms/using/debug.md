---
title: Felsöka HTML5-formulär
seo-title: Felsöka HTML5-formulär
description: Dokumentlistan innehåller steg för att felsöka olika kända problem.
seo-description: Dokumentlistan innehåller steg för att felsöka olika kända problem.
uuid: df1835aa-6033-4ecb-97c8-4c3b7b96b943
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 5260d981-da40-40ab-834e-88e091840813
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Felsöka HTML5-formulär {#debugging-html-forms}

Det här dokumentet innehåller flera felsökningsscenarier. För varje scenario anges några steg för att felsöka problemet. Följ de här stegen och om problemet kvarstår konfigurerar du loggboken så att du kan hämta och granska loggar för fel/varningar. Mer information om loggning av HTML5-formulär finns i [Generera loggar för HTML5-formulär](/help/forms/using/enable-logs.md).

## Problem: När formuläret återges visas undantagssidan för org.apache.sling.api.SlingException {#problem-when-rendering-the-form-i-see-org-apache-sling-api-slingexception-exception-page}

Sök efter ord **som** orsakats i undantagsinformationen.

Den troliga orsaken är att en eller flera parametrar i URL:en är felaktiga.

Kontrollera följande parametrar:

<table>
 <tbody>
  <tr>
   <td><strong>Parameter</strong></td>
   <td><strong>Beskrivning</strong></td>
  </tr>
  <tr>
   <td>template</td>
   <td>Mallens filnamn</td>
  </tr>
  <tr>
   <td>contentRoot</td>
   <td>Sökvägen där mall och associerade resurser finns</td>
  </tr>
  <tr>
   <td>dataRef</td>
   <td>Absolut sökväg till datafilen som sammanfogas med mallen.<br /> Obs! Sökvägen definierar den absoluta sökvägen för datafilen.</td>
  </tr>
  <tr>
   <td>data</td>
   <td>UTF-8-kodade databyte som sammanfogas med mallen.</td>
  </tr>
 </tbody>
</table>

## Problem: Det går inte att återge ett formulär (ett felmeddelande visas) {#problem-unable-to-render-a-form-an-error-message-is-displayed}

1. Kontrollera att de angivna parametrarna är korrekta. Mer information om parametrar finns i [Återgivningsparametrar](/help/forms/using/debug.md#main-pars-table).
1. Logga in på CRX Package Manager (på https://&lt;server>:&lt;port>/crx/packmgr/index.jsp) och kontrollera om följande paket är korrekt installerade:

   * adobe-lc-forms-content-pkg-&lt;version>.zip
   * adobe-lc-forms-runtime-pkg-&lt;version>.zip

1. Logga in på CQ Web Console (Felix Console) på https://&lt;server>:&lt;port>/system/console/bundles.

   Kontrollera att status för följande paket är &quot;aktiv&quot;:

   * scala-lang.bundle [osgi]
   (com.adobe.livecyclescala-lang.bundle)

   * Adobe XFA Forms Renderer
   (com.adobe.livecycle.adobe-lc-forms-core)

   * Adobe XFA Forms LC Connector
   (com.adobe.livecycle.adobe-lc-forms-lc-connector)

## Problem: Formuläråtergivning utan format {#problem-form-renders-without-styles}

1. Öppna **Utvecklarverktyg** i webbläsaren. Kontrollera att profile.css är tillgänglig.
1. Om filen profile.css inte är tillgänglig loggar du in på CRX DE på https://&lt;server>:&lt;port>/crx/de.
1. I mapphierarkin till vänster går du till /etc/clientlibs/fd/xfaforms/. Öppna css.txt-filer i mapparna.

   * profil
   * runtime
   * scrollnav
   * toolbar
   * xfalib

1. Kontrollera att filerna som omnämns i css.txt finns i CRX DE lite på /libs/fd/xfaforms/clientlibs/xfalib/css.

   ```css
   #base=css
   application.css
   dialog.css
   datepicker.css
   scribble.css
   listboxwidget.css
   ```

1. Om filerna inte är tillgängliga installerar du paketet adobe-lc-forms-runtime-pkg-&lt;version>.zip igen.

### Problem: Ett oväntat fel påträffades {#problem-unexpected-error-encountered}

1. I formulärets URL lägger du till en frågeparameter, debugClientLibs, och anger värdet till true (till exempel: https://&lt;server>:&lt;port>/content/xfaforms/profiles/test.html?contentRoot=&lt;sökväg>&amp;template=&lt;namn på xdp-fil>&amp;log=1-a9-b9-c9&amp;debugClientLibs=true)
1. Gå till Utvecklarverktyg -> Konsol i webbläsaren som Chrome.
1. Öppna loggarna för att identifiera feltypen. Mer information om loggar finns i [loggar för HTML5-formulär](/help/forms/using/enable-logs.md).
1. Gå till Developer Tools -> Console. Använd stackspårning för att hitta koden som orsakar felet. Felsök felet för att lösa problemet.

   >[!NOTE]
   >
   >Om det är ett skriptfel ska du även kontrollera om samma problem uppstår under PDF-återgivningen av formuläret. Om ja, finns det ett problem i skriptlogiken.

## Problem: Det går inte att skicka formuläret {#problem-unable-to-submit-the-form}

1. Kontrollera att du har behörighet att komma åt AEM-servern och att du är ansluten till servern.
1. Kontrollera att parametern submitUrl är korrekt.
1. Aktivera loggarna på klientsidan enligt [loggarna för HTML5-formulären](/help/forms/using/enable-logs.md) med felsökningsalternativet **1-a5-b5-c5**. Återge sedan formuläret och klicka på Skicka. Öppna webbläsarens felsökningskonsol och kontrollera om det finns något fel.
1. Leta reda på serverloggarna som anges i [Logs för HTML5-formulären](/help/forms/using/enable-logs.md). Kontrollera om det uppstod något fel i serverloggarna under överföringen.

## Problem: Lokaliserade felmeddelanden visas inte {#problem-localized-error-messages-do-not-display}

1. Rendera formuläret med den extra frågeparametern **debugClientLibs=true** i webbläsaren på skrivbordet och gå sedan till Developer Tools -> Resources och sök efter filen I18N.css.
1. Om filen inte är tillgänglig loggar du in på CRX DE på https://&lt;server>:&lt;port>/crx/de.
1. I mapphierarkin till vänster går du till /libs/fd/xfaforms/clientlibs/I18N och kontrollerar att följande filer och mappar finns:

   * Namespace.js
   * LogMessages.js
   * Mappar för språk

1. Om någon av filerna eller mapparna ovan inte finns installerar du paketet **adobe-lc-forms-runtime-pkg-&lt;version>.zip** igen.
1. Navigera till mappen som har samma namn som namnet på språkinställningen och kontrollera innehållet i den. Mappen måste innehålla följande filer:

   * I18N.js
   * js.txt

1. Kontrollera innehållet i js.txt och se till att det har följande poster.

   ```
   ../Namespace.js
   I18N.js
   ../LogMessages.js
   ```

## Problem: Bilden visas inte {#problem-image-not-showing-up}

1. Kontrollera att bild-URL:en är korrekt.
1. Kontrollera om webbläsaren stöder den här typen av bild.
1. Sök efter ord **som** orsakats i undantagsinformationen.

   Den troliga orsaken är att en eller flera parametrar i URL:en är felaktiga.

   Kontrollera följande parametrar:Stega text

<table>
 <tbody>
  <tr>
   <td><strong>Parameter</strong></td>
   <td><strong>Beskrivning</strong></td>
  </tr>
  <tr>
   <td>template</td>
   <td>Mallens filnamn</td>
  </tr>
  <tr>
   <td>contentRoot</td>
   <td>Sökvägen där mall och associerade resurser finns</td>
  </tr>
  <tr>
   <td>dataRef</td>
   <td>Absolut sökväg till datafilen som sammanfogas med mallen.<br /> Obs! Sökvägen definierar den absoluta sökvägen för datafilen.</td>
  </tr>
  <tr>
   <td>data</td>
   <td>UTF-8-kodade databyte som sammanfogas med mallen.</td>
  </tr>
 </tbody>
</table>

1. I webbläsaren går du till Utvecklarverktyg -> Resurser.

   Markera till vänster i Bildrutor om bilden visas.

[Kontakta supporten](https://www.adobe.com/account/sign-in.supportportal.html)
