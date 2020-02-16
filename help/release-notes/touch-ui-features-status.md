---
title: Funktionsstatus för Touch UI
description: Versionsinformation som är specifik för Adobe Experience Manager Touch-aktiverat användargränssnitt.
uuid: ceb081cc-7c33-4408-8032-3ac83d461268
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5
discoiquuid: f736581d-e6ea-4ec8-bfc7-16b9aa592097
docset: aem65
translation-type: tm+mt
source-git-commit: 57bad4e74b2dfd9e389643bfe58ef25564c5c545

---


# Funktionsstatus för Touch UI{#touch-ui-feature-status}

>[!CAUTION]
>
>[Klassiskt användargränssnitt har tagits bort](../release-notes/deprecated-removed-features.md) sedan AEM 6.4. Adobe planerar inte att göra fler förbättringar av det klassiska användargränssnittet och användarna uppmuntras att utnyttja de nya kraftfulla funktionerna som finns i det pekaktiverade användargränssnittet.

Från och med version 6.0 har AEM introducerat ett nytt användargränssnitt som kallas &quot;pekaktiverat användargränssnitt&quot; (kallas även&quot;pekgränssnitt&quot;) som är anpassat till Adobe Marketing Cloud och till de allmänna riktlinjerna för Adobes användargränssnitt. Med nästan samma funktionsparitet har detta blivit standardgränssnittet i AEM med det äldre skrivbordsorienterade gränssnittet som kallas&quot;klassiskt användargränssnitt&quot;.

De flesta funktioner finns i det beröringskänsliga användargränssnittet, men det finns funktioner som ännu inte är fullständiga och som kommer att läggas till i framtida versioner.

Följande lista visar aktuell status för funktionerna som implementerats i AEM 6.5.

Rekommendationer för kunder som uppgraderar till AEM 6.5 finns i [Användargränssnittsrekommendationer för kunder](/help/sites-deploying/ui-recommendations.md) .

>[!NOTE]
>
>Observera att den här sidan endast omfattar funktionsparitet med klassiskt användargränssnitt.
>
>Funktioner som lagts till och är unika för det beröringsaktiverade användargränssnittet och som inte finns i det klassiska användargränssnittet visas inte.

>[!NOTE]
>
>Denna förteckning skall vara fullständig, men skall inte anses uttömmande.

## Förklaring {#legend}

* **Fullständigt**: Funktionen är helt tillgänglig i det beröringskänsliga användargränssnittet
* **Mest**: Funktionen är oftast tillgänglig i det beröringskänsliga användargränssnittet.
* **Saknas**: Funktionen finns inte i det beröringsaktiverade användargränssnittet, det klassiska användargränssnittet måste användas för att utföra den här åtgärden.
* **Ersatt**: Funktionen har ersatts med en ny implementering som fungerar annorlunda.
* **Borttagen**: Funktionen finns inte längre i det beröringskänsliga användargränssnittet och kommer inte att ersättas.

## Funktionsstatus: Webbplatsadministratör {#feature-status-sites-admin}

Det här är en lista över funktioner som den klassiska användargränssnittsadministratören ( `/siteadmin`) har och status i det beröringskänsliga användargränssnittet ( `/sites.html`).

<table>
 <tbody>
  <tr>
   <td><strong>Funktion<br /> </strong></td>
   <td><strong>Status<br /> </strong></td>
   <td><strong>Kommentar</strong></td>
  </tr>
  <tr>
   <td>Navigera i webbplatshierarkin</td>
   <td>Slutförd<br /> </td>
   <td>I AEM 6.4 introducerades en <a href="/help/sites-authoring/basic-handling.md#content-tree">innehållsträdsvy</a>.</td>
  </tr>
  <tr>
   <td>Starta arbetsflöde</td>
   <td>Slutförd<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Skapa ny sida</td>
   <td>Slutförd</td>
   <td> </td>
  </tr>
  <tr>
   <td>Skapa ny plats</td>
   <td>Slutförd</td>
   <td> </td>
  </tr>
  <tr>
   <td>Skapa ny start</td>
   <td>Slutförd</td>
   <td> </td>
  </tr>
  <tr>
   <td>Skapa ny livecopy <br /> </td>
   <td>Slutförd<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Skapa mapp</td>
   <td>Slutförd</td>
   <td> </td>
  </tr>
  <tr>
   <td>Visa publiceringsstatus</td>
   <td>Slutförd</td>
   <td>Från och med AEM 6.5 visas arbetsflödets status i listvyn</td>
  </tr>
  <tr>
   <td>Sök</td>
   <td>Slutförd<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Kopiera/klistra in sida (duplicera)</td>
   <td>Slutförd</td>
   <td> </td>
  </tr>
  <tr>
   <td>Flytta sida/sidor</td>
   <td>Slutförd</td>
   <td> </td>
  </tr>
  <tr>
   <td>Publicera sidor</td>
   <td>Slutförd</td>
   <td> </td>
  </tr>
  <tr>
   <td>Publicera sidor utan replikeringsrättigheter</td>
   <td>Slutförd</td>
   <td> </td>
  </tr>
  <tr>
   <td>Publicera senare</td>
   <td>Slutförd</td>
   <td> </td>
  </tr>
  <tr>
   <td>Publiceringsträd</td>
   <td>Slutförd</td>
   <td> </td>
  </tr>
  <tr>
   <td>Avpublicera sidor</td>
   <td>Slutförd</td>
   <td> </td>
  </tr>
  <tr>
   <td>Avpublicera sidor utan replikeringsrättigheter</td>
   <td>Slutförd</td>
   <td> </td>
  </tr>
  <tr>
   <td>Avpublicera senare</td>
   <td>Slutförd<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Ta bort</td>
   <td>Slutförd</td>
   <td> </td>
  </tr>
  <tr>
   <td>Lås/lås upp</td>
   <td>Slutförd</td>
   <td> </td>
  </tr>
  <tr>
   <td>Visa/redigera egenskaper</td>
   <td>Slutförd</td>
   <td> </td>
  </tr>
  <tr>
   <td>Ange behörigheter på sidor</td>
   <td>Slutförd</td>
   <td> </td>
  </tr>
  <tr>
   <td>Versionshistorik</td>
   <td>Slutförd</td>
   <td> </td>
  </tr>
  <tr>
   <td>Återställ version</td>
   <td>Slutförd<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Återställ träd och återställa borttagna sidor</td>
   <td>Saknas</td>
   <td>Använd klassiskt gränssnitt.</td>
  </tr>
  <tr>
   <td>Visa skillnad mellan gammal och aktuell version<br /> </td>
   <td>Slutförd<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Livecopy-åtgärder (utrullning)</td>
   <td>Slutförd</td>
   <td> </td>
  </tr>
  <tr>
   <td>Se språkkopior</td>
   <td>Slutförd</td>
   <td> </td>
  </tr>
  <tr>
   <td>Sök och ersätt</td>
   <td>Saknas<br /> </td>
   <td>Använd klassiskt gränssnitt.</td>
  </tr>
  <tr>
   <td>Inkorgen för meddelanden (JCR-händelser)</td>
   <td>Saknas</td>
   <td>Använd klassiskt gränssnitt. Ersätts med annan implementering.</td>
  </tr>
  <tr>
   <td>Referenser</td>
   <td>Slutförd</td>
   <td>Visa inkommande sidlänkar som lagts till i AEM 6.5.<br /> </td>
  </tr>
 </tbody>
</table>

## Funktionsstatus: Page Editor {#feature-status-page-editor}

Det här är en lista över funktioner som den klassiska sidredigeraren i användargränssnittet ( `/cf#`) har och status för den beröringsaktiverade ( `/editor.html`).

<table>
 <tbody>
  <tr>
   <td><strong>Funktion</strong></td>
   <td><strong>Status</strong></td>
   <td><strong>Kommentar</strong></td>
  </tr>
  <tr>
   <td>Redigera webbsidor</td>
   <td>Slutförd</td>
   <td> </td>
  </tr>
  <tr>
   <td>Redigera mobilwebbsidor<br /> </td>
   <td>Slutförd<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Redigera innehåll som importerats via Design Importer<br /> </td>
   <td>Slutförd</td>
   <td> </td>
  </tr>
  <tr>
   <td>Redigera e-post</td>
   <td>Slutförd</td>
   <td> </td>
  </tr>
  <tr>
   <td>Redigera hybrida mobilappar</td>
   <td>Slutförd<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Redigera formulär</td>
   <td>Slutförd<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Redigera erbjudanden</td>
   <td>Slutförd<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Redigera arbetsflödesmodeller<br /> </td>
   <td>Slutförd</td>
   <td> </td>
  </tr>
  <tr>
   <td>kod: Redigera och förhandsgranska</td>
   <td>Slutförd</td>
   <td> </td>
  </tr>
  <tr>
   <td>Responsiv förhandsgranskning<br /> </td>
   <td>Slutförd</td>
   <td> </td>
  </tr>
  <tr>
   <td>Läge: Redigera design</td>
   <td>Slutförd</td>
   <td> </td>
  </tr>
  <tr>
   <td>Läge: Ställning</td>
   <td>Slutförd</td>
   <td> </td>
  </tr>
  <tr>
   <td>Läge: Live Copy-status<br /> </td>
   <td>Slutförd</td>
   <td> </td>
  </tr>
  <tr>
   <td>Lägg till anteckningar</td>
   <td>Slutförd</td>
   <td> </td>
  </tr>
  <tr>
   <td>Redigera egenskaper<br /> </td>
   <td>Slutförd</td>
   <td> </td>
  </tr>
  <tr>
   <td>Rullande sida</td>
   <td>Slutförd<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Starta och visa arbetsflöde</td>
   <td>Slutförd</td>
   <td> </td>
  </tr>
  <tr>
   <td>Hantering av arbetsflödespaket</td>
   <td>Mest</td>
   <td>Helt åtkomligt i användargränssnittet med pekfunktion. Flera arbetsflödesnyttolaster visas fortfarande i det klassiska användargränssnittet.<br /> </td>
  </tr>
  <tr>
   <td>Lås/lås upp sida</td>
   <td>Slutförd</td>
   <td> </td>
  </tr>
  <tr>
   <td>Publicera sida <br /> </td>
   <td>Slutförd<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Avpublicera sida</td>
   <td>Slutförd</td>
   <td> </td>
  </tr>
  <tr>
   <td>Kopiera sida</td>
   <td>Borttagen<br /> </td>
   <td>Använd Webbplatsadministratör för att <a href="/help/sites-authoring/managing-pages.md#copying-and-pasting-a-page">kopiera sidor</a>.<br /> </td>
  </tr>
  <tr>
   <td>Flytta sida</td>
   <td>Borttagen</td>
   <td>Använd Webbplatsadministratör för att <a href="/help/sites-authoring/managing-pages.md#moving-or-renaming-a-page">flytta sidor</a>.<br /> </td>
  </tr>
  <tr>
   <td>Ta bort sida</td>
   <td>Borttagen</td>
   <td>Använd Webbplatsadministratör för att <a href="/help/sites-authoring/managing-pages.md#deleting-a-page">ta bort sidor</a>.<br /> </td>
  </tr>
  <tr>
   <td>Visa referenser</td>
   <td>Borttagen</td>
   <td>Använd Webbplatsadministratör för att <a href="/help/sites-authoring/author-environment-tools.md#references">se den detaljerade referenslistan</a>.<br /> </td>
  </tr>
  <tr>
   <td>Granskningslogg</td>
   <td>Borttagen</td>
   <td>Använd Webbplatsadministratör och <a href="/help/sites-authoring/author-environment-tools.md#events-timeline">öppen aktivitetsfältet</a>.<br /> </td>
  </tr>
  <tr>
   <td>Skapa version</td>
   <td>Borttagen</td>
   <td>Använd Webbplatsadministratör för att <a href="/help/sites-authoring/working-with-page-versions.md#creating-a-new-version">skapa nya versioner</a>.<br /> </td>
  </tr>
  <tr>
   <td>Återställ version</td>
   <td>Borttagen</td>
   <td>Använd Webbplatsadministratör för att <a href="/help/sites-authoring/working-with-page-versions.md#reverting-to-a-page-version">återställa versioner</a>.</td>
  </tr>
  <tr>
   <td>Växla startprogram</td>
   <td>Borttagen</td>
   <td>Använd Webbplatsadministratör för att <a href="/help/sites-authoring/launches-promoting.md">växla mellan starter</a>.<br /> </td>
  </tr>
  <tr>
   <td>Översätt sida</td>
   <td>Borttagen</td>
   <td>Använd Webbplatsadministratör för att <a href="/help/sites-administering/tc-manage.md">lägga till sidor i översättningsprojekt</a>.<br /> </td>
  </tr>
  <tr>
   <td>Timewarp (välj datum/tid och bläddra på webbplatsen efter utseendet)<br /> </td>
   <td>Slutförd</td>
   <td> </td>
  </tr>
  <tr>
   <td>Ange behörigheter</td>
   <td>Slutförd</td>
   <td> </td>
  </tr>
  <tr>
   <td>Användargränssnitt för klientkontext<br /> </td>
   <td>Ersatt</td>
   <td>Använd <a href="/help/sites-authoring/ch-previewing.md">ContextHub</a> -gränssnittet framåt.</td>
  </tr>
  <tr>
   <td>Content Finder för de olika medietyperna<br /> </td>
   <td>Slutförd</td>
   <td> </td>
  </tr>
  <tr>
   <td>Komponentlista</td>
   <td>Slutförd<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Kopiera och klistra in komponenter<br /> </td>
   <td>Slutförd</td>
   <td> </td>
  </tr>
  <tr>
   <td>Lista över komponenter i Urklipp</td>
   <td>Saknas</td>
   <td> </td>
  </tr>
  <tr>
   <td>Ångra/Gör om</td>
   <td>Slutförd</td>
   <td> </td>
  </tr>
  <tr>
   <td>Dra och släpp innehåll i komponentplatshållaren</td>
   <td>Slutförd</td>
   <td> </td>
  </tr>
  <tr>
   <td>Dra-och-släpp material direkt i en platshållare med automatisk komponentframtagning<br /> </td>
   <td>Slutförd</td>
   <td> </td>
  </tr>
 </tbody>
</table>

## Funktionsstatus: Text-, tabell- och bildredigerare {#feature-status-text-table-and-image-editors}

Det här är en lista över funktioner som det klassiska användargränssnittet för text, tabell och bildredigering har och status i det beröringskänsliga användargränssnittet.

<table>
 <tbody>
  <tr>
   <td><strong>Funktion</strong></td>
   <td><strong>Status </strong></td>
   <td><strong>Kommentar<br /> </strong></td>
  </tr>
  <tr>
   <td>RTF-redigerare</td>
   <td>Slutförd</td>
   <td>Kan användas på plats, i dialogrutor och i helskärmsläge.</td>
  </tr>
  <tr>
   <td>Aktivera/inaktivera RTE-plugin-program</td>
   <td>Slutförd<br /> </td>
   <td>Kan göras med <a href="/help/sites-authoring/templates.md">mallredigeraren</a>.</td>
  </tr>
  <tr>
   <td>Använd RTE för oformaterad text</td>
   <td>Slutförd<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td>RTE-plugin: Länkar och ankarpunkt</td>
   <td>Slutförd</td>
   <td> </td>
  </tr>
  <tr>
   <td>RTE-plugin: Teckenuppsättning</td>
   <td>Slutförd</td>
   <td> </td>
  </tr>
  <tr>
   <td>RTE-plugin: Kopiera/klistra in</td>
   <td>Slutförd</td>
   <td> </td>
  </tr>
  <tr>
   <td>RTE-plugin: Klistra in från Microsoft Word<br /> </td>
   <td>Slutförd</td>
   <td> </td>
  </tr>
  <tr>
   <td>RTE-plugin:Sök och ersätt</td>
   <td>Slutförd</td>
   <td> </td>
  </tr>
  <tr>
   <td>RTE-plugin: Textformat (fet, ...)</td>
   <td>Slutförd<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td>RTE-plugin: Under och upphöjd text</td>
   <td>Slutförd</td>
   <td> </td>
  </tr>
  <tr>
   <td>RTE-plugin: Justera</td>
   <td>Slutförd<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td>RTE-plugin: Listor (punkt / nummer)</td>
   <td>Slutförd</td>
   <td> </td>
  </tr>
  <tr>
   <td>RTE-plugin: Styckeformat</td>
   <td>Slutförd<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td>RTE-plugin: Textformat</td>
   <td>Slutförd</td>
   <td> </td>
  </tr>
  <tr>
   <td>RTE-plugin: Källredigeraren (Redigera HTML)<br /> </td>
   <td>Slutförd<br /> </td>
   <td>Endast tillgängligt i dialogruta och i helskärmsläge.<br /> </td>
  </tr>
  <tr>
   <td>RTE-plugin:Stavningskontroll</td>
   <td>Slutförd</td>
   <td> </td>
  </tr>
  <tr>
   <td>RTE-plugin: Tabell (inbäddad tabellredigerare)</td>
   <td>Slutförd</td>
   <td> </td>
  </tr>
  <tr>
   <td>RTE-plugin: Ångra/Gör om<br /> </td>
   <td>Slutförd</td>
   <td> </td>
  </tr>
  <tr>
   <td>RTE-plugin: Tillåt textbundna bilder</td>
   <td>Slutförd</td>
   <td> </td>
  </tr>
  <tr>
   <td>Tabellredigerare</td>
   <td>Slutförd</td>
   <td>Kan användas på plats, i dialogrutor och i helskärmsläge.<br /> </td>
  </tr>
  <tr>
   <td>Dra och släpp bild i tabellcell<br /> </td>
   <td>Slutförd</td>
   <td>Användbart online</td>
  </tr>
  <tr>
   <td>Bildredigeraren<br /> </td>
   <td>Slutförd</td>
   <td>Kan användas på plats, i dialogrutor och i helskärmsläge.<br /> </td>
  </tr>
  <tr>
   <td>Aktivera/inaktivera IPE-plugin-program</td>
   <td>Slutförd</td>
   <td>I AEM 6.3 introducerades ett gränssnitt i <a href="/help/sites-authoring/templates.md">mallredigeraren</a>.</td>
  </tr>
  <tr>
   <td>IPE-plugin: Beskär</td>
   <td>Slutförd</td>
   <td> </td>
  </tr>
  <tr>
   <td>IPE-plugin: Vänd</td>
   <td>Slutförd<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td>IPE-plugin: Ångra/Gör om</td>
   <td>Slutförd<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td>IPE-plugin: Bildschema</td>
   <td>Slutförd</td>
   <td> </td>
  </tr>
  <tr>
   <td>IPE-plugin: Rotera</td>
   <td>Slutförd</td>
   <td> </td>
  </tr>
  <tr>
   <td>IPE-plugin: Zooma</td>
   <td>Slutförd<br /> </td>
   <td> </td>
  </tr>
 </tbody>
</table>

## Funktionsstatus: verktyg {#feature-status-tools}

Det här är en lista över olika verktyg som det klassiska användargränssnittet har och status i det beröringsaktiverade användargränssnittet.

<table>
 <tbody>
  <tr>
   <td><strong>Funktion<br /> </strong></td>
   <td><strong>Status<br /> </strong></td>
   <td><strong>Kommentar</strong></td>
  </tr>
  <tr>
   <td>Aktivitetshantering</td>
   <td>Ersatt</td>
   <td>6.0 introducerade <a href="/help/sites-authoring/projects.md">projekt och uppgifter</a>.<br /> </td>
  </tr>
  <tr>
   <td>Inkorgen för arbetsflöde<br /> </td>
   <td>Slutförd</td>
   <td> </td>
  </tr>
  <tr>
   <td>Konfiguration av arbetsflöde till sidmall (<code>/etc/workflow/wcm/templates.html</code>)</td>
   <td>Saknas<br /> </td>
   <td>Använd klassiskt gränssnitt.</td>
  </tr>
  <tr>
   <td>Taggning av administratörsgränssnitt<br /> </td>
   <td>Slutförd</td>
   <td> </td>
  </tr>
  <tr>
   <td>MSM/Blueprint Control Center</td>
   <td>Slutförd</td>
   <td> </td>
  </tr>
  <tr>
   <td>Gränssnitt för BluPrint Manager</td>
   <td>Slutförd</td>
   <td> </td>
  </tr>
  <tr>
   <td>Gränssnitt för konfiguration av utrullning</td>
   <td>Saknas</td>
   <td>Använd klassiskt gränssnitt.</td>
  </tr>
  <tr>
   <td>Användargränssnitt för användare, grupper och behörigheter<br /> </td>
   <td>Mest komplett<br /> </td>
   <td>Använd Classic UI om du vill ha mer behörighet.<br /> </td>
  </tr>
  <tr>
   <td>Rensa versioner (<code>/etc/versioning/purge.html</code>)</td>
   <td>Saknas</td>
   <td>Använd klassiskt gränssnitt.</td>
  </tr>
  <tr>
   <td>Extern länkkontroll (<code>/etc/linkchecker.html</code>)</td>
   <td>Saknas</td>
   <td>Använd klassiskt gränssnitt.<br /> </td>
  </tr>
  <tr>
   <td>Massredigerare (<code>/etc/importers/bulkeditor.html</code>)</td>
   <td>Saknas<br /> </td>
   <td>Använd klassiskt gränssnitt.</td>
  </tr>
  <tr>
   <td>Överför miniatyrbilder för att lägga till eller skriva över dem<br /> </td>
   <td>Saknas</td>
   <td>Använd klassiskt gränssnitt.</td>
  </tr>
 </tbody>
</table>

