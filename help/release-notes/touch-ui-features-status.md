---
title: Funktionsstatus för Touch UI
description: Versionsinformation som är specifik för [!DNL Adobe Experience Manager] Pekaktiverat användargränssnitt.
exl-id: 7b71e8db-e8c6-4470-bc22-db3d4600b7fc
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1063'
ht-degree: 1%

---

# Funktionsstatus för Touch UI {#touch-ui-feature-status}

AEM 6.4 och framåt [Klassiskt användargränssnitt är föråldrat](../release-notes/deprecated-removed-features.md). Adobe kommer inte att göra några ytterligare förbättringar av det klassiska användargränssnittet, och användare uppmanas att utnyttja de nya kraftfulla funktionerna i det beröringskänsliga användargränssnittet.

Från och med version 6.0 har AEM introducerat ett nytt användargränssnitt som kallas &quot;användargränssnittet med pekfunktion&quot; (kallas helt enkelt &quot;användargränssnittet&quot;) som är anpassat till [!DNL Adobe Experience Cloud] och de allmänna riktlinjerna för användargränssnittet i Adobe. Med nästan samma funktionsparitet har detta blivit standardgränssnittet i AEM med det äldre skrivbordsorienterade gränssnittet som kallas &quot;klassiskt användargränssnitt&quot;.

De flesta funktioner finns i det beröringskänsliga användargränssnittet, men det finns funktioner som ännu inte är fullständiga och som kommer att läggas till i framtida versioner.

Följande lista visar aktuell status för funktionerna som implementerats i AEM 6.5.

Rekommendationer för kunder som uppgraderar till AEM 6.5 finns på [Rekommendationer för användargränssnitt](/help/sites-deploying/ui-recommendations.md).

>[!NOTE]
>
>Den här sidan täcker endast funktionsparitet med klassiskt användargränssnitt. Funktioner som lagts till i och är unika för det Touch-aktiverade användargränssnittet som inte finns i det klassiska användargränssnittet visas inte.

>[!NOTE]
>
>Denna lista strävar efter att vara fullständig, men är inte uttömmande.

## Förklaring {#legend}

* **Slutförd**: Funktionen är helt tillgänglig i det beröringskänsliga användargränssnittet.
* **Mest**: Funktionen är oftast tillgänglig i det beröringskänsliga användargränssnittet.
* **Saknas**: Funktionen finns inte i det beröringsaktiverade användargränssnittet, det klassiska användargränssnittet måste användas för att utföra den här åtgärden.
* **Ersatt**: Funktionen har ersatts med en ny implementering som fungerar annorlunda.
* **Borttagen**: Funktionen finns inte längre i det beröringskänsliga användargränssnittet och kommer inte att ersättas.

## Funktionsstatus: Webbplatsadministratör {#feature-status-sites-admin}

Det här är en lista över funktioner som den klassiska administratören för användargränssnittets webbplats (`/siteadmin`) har och status i det beröringskänsliga användargränssnittet (`/sites.html`).

| Funktion | Status | Kommentar |
|--- |--- |--- |
| Navigera i webbplatshierarkin | Slutförd | AEM 6.4 införde [vyn för innehållsträd](/help/sites-authoring/basic-handling.md#content-tree). |
| Starta arbetsflöde | Slutförd |  |
| Skapa ny sida | Slutförd |  |
| Skapa ny plats | Slutförd |  |
| Skapa ny start | Slutförd |  |
| Skapa ny livecopy | Slutförd |  |
| Skapa mapp | Slutförd |  |
| Visa publiceringsstatus | Slutförd | Från och med AEM 6.5 visas arbetsflödets status i listvyn. |
| Sökning | Slutförd |  |
| Kopiera och klistra in sida (duplicera) | Slutförd |  |
| Flytta sida/sidor | Slutförd |  |
| Publicera sidor | Slutförd |  |
| Publicera sidor utan replikeringsrättigheter | Slutförd |  |
| Publicera senare | Slutförd |  |
| Publiceringsträd | Slutförd |  |
| Avpublicera sidor | Slutförd |  |
| Avpublicera sidor utan replikeringsrättigheter | Slutförd |  |
| Avpublicera senare | Slutförd |  |
| Ta bort | Slutförd |  |
| Lås/lås upp | Slutförd |  |
| Visa/redigera egenskaper | Slutförd |  |
| Ange behörigheter på sidor | Slutförd |  |
| Versionshistorik | Slutförd |  |
| Återställ version | Slutförd |  |
| Återställ träd och återställ borttagna sidor | Saknas | Använd klassiskt gränssnitt. |
| Visa skillnad mellan gammal och aktuell version | Slutförd |  |
| Livecopy-åtgärder (utrullning) | Slutförd |  |
| Se språkkopior | Slutförd |  |
| Sök och ersätt | Saknas | Använd klassiskt gränssnitt. |
| Inkorgen för meddelanden (JCR-händelser) | Saknas | Använd klassiskt gränssnitt. Ersätts med annan implementering. |
| Referenser | Slutförd | Visa inkommande sidlänkar som lagts till i AEM 6.5. |

## Funktionsstatus: Page Editor {#feature-status-page-editor}

Det här är en lista över funktioner i den klassiska sidredigeraren i användargränssnittet (`/cf#`) har och status i beröringsaktiverad (`/editor.html`).

| Funktion | Status | Kommentar |
|--- |--- |--- |
| Redigera webbsidor | Slutförd |  |
| Redigera mobilwebbsidor | Slutförd |  |
| Redigera innehåll som importerats via Design Importer | Slutförd |  |
| Redigera e-post | Slutförd |  |
| Redigera hybrida mobilappar | Slutförd |  |
| Redigera Forms | Slutförd |  |
| Redigera erbjudanden | Slutförd |  |
| Redigera arbetsflödesmodeller | Slutförd |  |
| Läge: Redigera och förhandsgranska | Slutförd |  |
| Responsiv förhandsgranskning | Slutförd |  |
| Läge: Redigera design | Slutförd |  |
| Läge: Ställning | Slutförd |  |
| Läge: Live Copy-status | Slutförd |  |
| Lägg till anteckningar | Slutförd |  |
| Redigera egenskaper | Slutförd |  |
| Rullande sida | Slutförd |  |
| Starta och visa arbetsflöde | Slutförd |  |
| Hantering av arbetsflödespaket | Mest | Helt åtkomligt i användargränssnittet med pekfunktion. Flera arbetsflödesnyttolaster visas fortfarande i det klassiska användargränssnittet. |
| Lås/lås upp sida | Slutförd |  |
| Publicera sida | Slutförd |  |
| Avpublicera sida | Slutförd |  |
| Kopiera sida | Borttagen | Använd Webbplatsadministratör för att [kopiera sidor](/help/sites-authoring/managing-pages.md#copying-and-pasting-a-page). |
| Flytta sida | Borttagen | Använd Webbplatsadministratör för att [flytta sidor](/help/sites-authoring/managing-pages.md#moving-or-renaming-a-page). |
| Ta bort sida | Borttagen | Använd Webbplatsadministratör för att [ta bort sidor](/help/sites-authoring/managing-pages.md#deleting-a-page). |
| Visa referenser | Borttagen | Använd Webbplatsadministratör för att se [detaljerad referenslista](/help/sites-authoring/author-environment-tools.md#references). |
| Granskningslogg | Borttagen | Använd Webbplatsadministratör och [öppen aktivitetsaxel](/help/sites-authoring/author-environment-tools.md#events-timeline). |
| Skapa version | Borttagen | Använd Webbplatsadministratör för att [skapa nya versioner](/help/sites-authoring/working-with-page-versions.md#creating-a-new-version). |
| Återställ version | Borttagen | Använd Webbplatsadministratör för att [återställa versioner](/help/sites-authoring/working-with-page-versions.md#reverting-to-a-page-version). |
| Växla startprogram | Borttagen | Använd Webbplatsadministratör för att [växla mellan starter](/help/sites-authoring/launches-promoting.md). |
| Översätt sida | Borttagen | Använd Webbplatsadministratör för att [lägga till sida i översättningsprojekt](/help/sites-administering/tc-manage.md). |
| Timewarp (välj datum/tid och bläddra på webbplatsen efter utseendet) | Slutförd |  |
| Ange behörigheter | Slutförd |  |
| Användargränssnitt för klientkontext | Ersatt | Använd [ContextHub](/help/sites-authoring/ch-previewing.md) Gränssnittet går framåt. |
| Content Finder för de olika medietyperna | Slutförd |  |
| Komponentlista | Slutförd |  |
| Kopiera och klistra in komponenter | Slutförd |  |
| Lista över komponenter i Urklipp | Saknas |  |
| Ångra/Gör om | Slutförd |  |
| Dra innehåll till komponentplatshållaren | Slutförd |  |
| Dra innehåll direkt till en platshållare för parsys med automatisk komponentgenerering | Slutförd |  |

## Funktionsstatus: Text-, tabell- och bildredigerare {#feature-status-text-table-and-image-editors}

Det här är en lista över funktioner som det klassiska användargränssnittet för text, tabell och bildredigering har och status i det beröringskänsliga användargränssnittet.

| Funktion | Status | Kommentar |
|--- |--- |--- |
| RTF-redigerare | Slutförd | Kan användas på plats, i dialogrutor och i helskärmsläge. |
| Aktivera/inaktivera RTE-plugin-program | Slutförd | Kan göras med [Mallredigerare](/help/sites-authoring/templates.md). |
| Använd RTE för oformaterad text | Slutförd |  |
| RTE-plugin: Länkar och ankare | Slutförd |  |
| RTE-plugin: Teckenuppsättning | Slutförd |  |
| RTE-plugin: Kopiera/klistra in | Slutförd |  |
| RTE-plugin: Klistra in från Microsoft Word | Slutförd |  |
| RTE-plugin: Sök och ersätt | Slutförd |  |
| RTE-plugin: Textformat (fet, ...) | Slutförd |  |
| RTE-plugin: Under- och upphöjd text | Slutförd |  |
| RTE-plugin: Justera | Slutförd |  |
| RTE-plugin: Listor (punkt / nummer) | Slutförd |  |
| RTE-plugin: Styckeformat | Slutförd |  |
| RTE-plugin: Textformat | Slutförd |  |
| RTE-plugin: Källredigeraren (Redigera HTML) | Slutförd | Endast tillgängligt i dialogruta och i helskärmsläge. |
| RTE-plugin: Stavningskontroll | Slutförd |  |
| RTE-plugin: Tabell (inbäddad tabellredigerare) | Slutförd |  |
| RTE-plugin: Ångra/Gör om | Slutförd |  |
| RTE-plugin: Tillåt textbundna bilder | Slutförd |  |
| Tabellredigerare | Slutförd | Kan användas på plats, i dialogrutor och i helskärmsläge. |
| Dra bild till tabellcell | Slutförd | Användbart online |
| Bildredigeraren | Slutförd | Kan användas på plats, i dialogrutor och i helskärmsläge. |
| Aktivera/inaktivera IPE-plugin-program | Slutförd | I AEM 6.3 introducerades ett gränssnitt i [Mallredigerare](/help/sites-authoring/templates.md). |
| IPE-plugin: Beskär | Slutförd |  |
| IPE-plugin: Vänd | Slutförd |  |
| IPE-plugin: Ångra/Gör om | Slutförd |  |
| IPE-plugin: Bildschema | Slutförd |  |
| IPE-plugin: Rotera | Slutförd |  |
| IPE-plugin: Zooma | Slutförd |  |

## Funktionsstatus: verktyg {#feature-status-tools}

Det här är en lista över olika verktyg som det klassiska användargränssnittet har och status i det beröringsaktiverade användargränssnittet.

| Funktion | Status | Kommentar |
|--- |--- |--- |
| Aktivitetshantering | Ersatt | 6.0 innehåller projekt och uppgifter. |
| Inkorgen för arbetsflöde | Slutförd |  |
| Konfiguration av arbetsflöde till sidmall (`/etc/workflow/wcm/templates.html`) | Saknas | Använd klassiskt gränssnitt. |
| Taggning av administratörsgränssnitt | Slutförd |  |
| MSM/Blueprint Control Center | Slutförd |  |
| Gränssnitt för BluPrint Manager | Slutförd |  |
| Gränssnitt för konfiguration av utrullning | Saknas | Använd klassiskt gränssnitt. |
| Användargränssnitt, grupper och behörigheter | Mest komplett | Använd Classic UI om du vill ha mer behörighet. |
| Rensa versioner (`/etc/versioning/purge.html`) | Saknas | Använd klassiskt gränssnitt. |
| Extern länkkontroll (`/etc/linkchecker.html`) | Saknas | Använd klassiskt gränssnitt. |
| Massredigeraren (`/etc/importers/bulkeditor.html`) | Saknas | Använd klassiskt gränssnitt. |
| Överför miniatyrbilder för att lägga till eller skriva över dem | Saknas | Använd klassiskt gränssnitt. |
