---
title: Funktionsstatus för Touch UI
description: Versionsinformation som är specifik för  [!DNL Adobe Experience Manager] användargränssnittet som har aktiverats för pekfunktioner.
exl-id: 7b71e8db-e8c6-4470-bc22-db3d4600b7fc
solution: Experience Manager
feature: Release Information
role: User,Admin,Architect,Developer
source-git-commit: 10268f617b8a1bb22f1f131cfd88236e7d5beb47
workflow-type: tm+mt
source-wordcount: '1076'
ht-degree: 0%

---

# Funktionsstatus för Touch UI {#touch-ui-feature-status}

Adobe Experience Manager (AEM) 6.4 och framåt [Klassiskt användargränssnitt är föråldrat](../release-notes/deprecated-removed-features.md). Adobe gör inga fler förbättringar av det klassiska användargränssnittet och användare uppmanas att använda de nya kraftfulla funktionerna i det beröringskänsliga användargränssnittet.

Från och med version 6.0 har AEM introducerat ett nytt användargränssnitt som kallas &quot;pekaktiverat användargränssnitt&quot; (kallas &quot;Touch-användargränssnitt&quot;) som är anpassat till [!DNL Adobe Experience Cloud] och de övergripande riktlinjerna för användargränssnittet i Adobe. Med nästan samma funktionsparitet har detta blivit standardgränssnittet i AEM med det äldre skrivbordsorienterade gränssnittet som kallas &quot;klassiskt gränssnitt&quot;.

De flesta funktioner finns i det beröringskänsliga användargränssnittet, men det finns funktioner som ännu inte är fullständiga och som kommer att läggas till i framtida versioner.

Följande lista visar statusen för funktionerna som implementerats i AEM 6.5.

Rekommendationer för kunder som uppgraderar till AEM 6.5 finns i [Rekommendationer för användargränssnitt för kunder](/help/sites-deploying/ui-recommendations.md).

>[!NOTE]
>
>Den här sidan täcker endast funktionsparitet med klassiskt användargränssnitt. Funktioner som lagts till i och är unika för det Touch-aktiverade användargränssnittet som inte finns i det klassiska användargränssnittet visas inte.

>[!NOTE]
>
>Denna lista strävar efter att vara fullständig, men är inte uttömmande.

## Förklaring {#legend}

* **Fullständigt**: Funktionen är helt tillgänglig i det beröringsaktiverade användargränssnittet.
* **Mest**: Funktionen är oftast tillgänglig i det beröringskänsliga användargränssnittet.
* **Saknas**: Funktionen finns inte i det beröringsaktiverade användargränssnittet. Det klassiska användargränssnittet måste användas för att utföra den här åtgärden.
* **Ersatt**: Funktionen har ersatts med en ny implementering som fungerar på ett annat sätt.
* **Borttagen**: Funktionen finns inte längre i det beröringsaktiverade användargränssnittet och kommer inte att ersättas.

## Funktionsstatus: Webbplatsadministratör {#feature-status-sites-admin}

Det här är en lista över funktioner som den klassiska användargränssnittsadministratören (`/siteadmin`) har och status i det beröringskänsliga användargränssnittet (`/sites.html`).

| Funktion | Status | Kommentar |
|--- |--- |--- |
| Navigera i webbplatshierarkin | Complete | AEM 6.4 introducerade en [innehållsträdsvy](/help/sites-authoring/basic-handling.md#content-tree). |
| Starta arbetsflöde | Complete |  |
| Skapa ny sida | Complete |  |
| Skapa ny plats | Complete |  |
| Skapa ny start | Complete |  |
| Skapa ny live-kopia | Complete |  |
| Skapa mapp | Complete |  |
| Visa publiceringsstatus | Complete | Från och med AEM 6.5 visas arbetsflödets status i listvyn. |
| Sök | Complete |  |
| Kopiera och klistra in sida (duplicera) | Complete |  |
| Flytta sidor | Complete |  |
| Publish sidor | Complete |  |
| Publish-sidor utan replikeringsrättigheter | Complete |  |
| Publish senare | Complete |  |
| Publish | Complete |  |
| Avpublicera sidor | Complete |  |
| Avpublicera sidor utan replikeringsrättigheter | Complete |  |
| Avpublicera senare | Complete |  |
| Ta bort | Complete |  |
| Lås/lås upp | Complete |  |
| Visa/redigera egenskaper | Complete |  |
| Ange behörigheter på sidor | Complete |  |
| Versionshantering | Complete |  |
| Återställ version | Complete |  |
| Återställ träd och återställ borttagna sidor | Saknas | Använd klassiskt användargränssnitt. |
| Visa skillnad mellan gammal och aktuell version | Complete |  |
| Live copy-åtgärder (utrullning) | Complete |  |
| Se språkkopior | Complete |  |
| Sök och ersätt | Saknas | Använd klassiskt användargränssnitt. |
| Inkorgen för meddelanden (JCR-händelser) | Saknas | Använd klassiskt användargränssnitt. Ersätts med en annan implementering i framtiden. |
| Referenser | Complete | Visa inkommande sidlänkar som lagts till i AEM 6.5. |

## Funktionsstatus: sidredigeraren {#feature-status-page-editor}

Det här är en lista över funktioner som den klassiska sidredigeraren i användargränssnittet (`/cf#`) har och status i den beröringsaktiverade (`/editor.html`).

| Funktion | Status | Kommentar |
|--- |--- |--- |
| Redigera webbsidor | Complete |  |
| Redigera mobilwebbsidor | Complete |  |
| Redigera innehåll som importerats via Design Importer | Complete |  |
| Redigera e-post | Complete |  |
| Redigera hybrida mobilappar | Complete |  |
| Redigera Forms | Complete |  |
| Redigera erbjudanden | Complete |  |
| Redigera arbetsflödesmodeller | Complete |  |
| Läge: Redigera och förhandsgranska | Complete |  |
| Responsiv förhandsgranskning | Complete |  |
| Läge: Redigera design | Complete |  |
| Läge: Ställning | Complete |  |
| Läge: Live Copy-status | Complete |  |
| Lägg till anteckningar | Complete |  |
| Redigera egenskaper | Complete |  |
| Rullande sida | Complete |  |
| Starta och visa arbetsflöde | Complete |  |
| Hantering av arbetsflödespaket | Mest | Finns i det pekaktiverade användargränssnittet. Flera arbetsflödesnyttolaster visas fortfarande i det klassiska användargränssnittet. |
| Lås/lås upp sida | Complete |  |
| Publish Page | Complete |  |
| Avpublicera sida | Complete |  |
| Kopiera sida | Borttagen | Använd Webbplatsadministratör för att [kopiera sidor](/help/sites-authoring/managing-pages.md#copying-and-pasting-a-page). |
| Flytta sida | Borttagen | Använd Webbplatsadministratör för att [flytta sidor](/help/sites-authoring/managing-pages.md#moving-or-renaming-a-page). |
| Ta bort sida | Borttagen | Använd Webbplatsadministratör för att [ta bort sidor](/help/sites-authoring/managing-pages.md#deleting-a-page). |
| Visa referenser | Borttagen | Använd Webbplatsadministratör för att se [detaljerad referenslista](/help/sites-authoring/author-environment-tools.md#references). |
| Granskningslogg | Borttagen | Använd Webbplatsadministratör och [öppna aktivitetsfältet](/help/sites-authoring/author-environment-tools.md#events-timeline). |
| Skapa version | Borttagen | Använd Webbplatsadministratör för att [skapa nya versioner](/help/sites-authoring/working-with-page-versions.md#creating-a-new-version). |
| Återställ version | Borttagen | Använd Webbplatsadministratör för att [återställa versioner](/help/sites-authoring/working-with-page-versions.md#reverting-to-a-page-version). |
| Växla startprogram | Borttagen | Använd Webbplatsadministratör för att [växla mellan starter](/help/sites-authoring/launches-promoting.md). |
| Översätt sida | Borttagen | Använd Webbplatsadministratör för att [lägga till sida i översättningsprojekt](/help/sites-administering/tc-manage.md). |
| Timewarp (välj datum/tid och bläddra på webbplatsen efter utseendet) | Complete |  |
| Ange behörigheter | Complete |  |
| Användargränssnitt för klientkontext | Ersatt | Använd användargränssnittet [ContextHub](/help/sites-authoring/ch-previewing.md) som fortsätter framåt. |
| Content Finder för de olika medietyperna | Complete |  |
| Komponentlista | Complete |  |
| Kopiera och klistra in komponenter | Complete |  |
| Lista över komponenter i Urklipp | Saknas |  |
| Ångra/Gör om | Complete |  |
| Dra innehåll till komponentplatshållaren | Complete |  |
| Dra innehåll direkt till en platshållare för parsys med automatisk komponentgenerering | Complete |  |

## Funktionsstatus: Text-, tabell- och bildredigerare {#feature-status-text-table-and-image-editors}

Det här är en lista över funktioner som det klassiska användargränssnittet för text, tabell och bildredigering har och status i det beröringskänsliga användargränssnittet.

| Funktion | Status | Kommentar |
|--- |--- |--- |
| RTF-redigerare | Complete | Kan användas på plats, i dialogrutor och i helskärmsläge. |
| Aktivera/inaktivera RTE-plugin-program | Complete | Du kan göra det med [mallredigeraren](/help/sites-authoring/templates.md). |
| Använd RTE för normal text | Complete |  |
| RTE-plugin: Länkar och ankarpunkt | Complete |  |
| RTE Plug-in: Teckenuppsättning | Complete |  |
| RTE-plugin: Kopiera/Klistra in | Complete |  |
| RTE-plugin: Klistra in från Microsoft® Word | Complete |  |
| RTE-plugin: Sök och ersätt | Complete |  |
| RTE-plugin: Textformat (fet, ...) | Complete |  |
| RTE Plug-in: Under och upphöjd | Complete |  |
| RTE-plugin: Justera | Complete |  |
| RTE-plugin: Listor (punkter/nummer) | Complete |  |
| RTE-plugin: Styckeformat | Complete |  |
| RTE-plugin: Textformat | Complete |  |
| RTE-plugin: Source Editor (Edit HTML) | Complete | Endast tillgängligt i dialogruta och i helskärmsläge. |
| RTE-plugin: stavningskontroll | Complete |  |
| RTE-plugin: Tabell (inbäddad tabellredigerare) | Complete |  |
| RTE-plugin: Ångra/Gör om | Complete |  |
| RTE-plugin: Tillåt textbundna bilder | Complete |  |
| Tabellredigerare | Complete | Kan användas på plats, i dialogrutor och i helskärmsläge. |
| Dra bild till tabellcell | Complete | Användbart online |
| Bildredigeraren | Complete | Kan användas på plats, i dialogrutor och i helskärmsläge. |
| Aktivera/inaktivera IPE-plugin-program | Complete | AEM 6.3 introducerade ett användargränssnitt i [mallredigeraren](/help/sites-authoring/templates.md). |
| IPE-plugin: Beskär | Complete |  |
| Plugin-programmet IPE: Flip | Complete |  |
| IPE-plugin: Ångra/Gör om | Complete |  |
| IPE Plug-in: Bildschema | Complete |  |
| IPE-plugin: Rotera | Complete |  |
| Plugin-programmet IPE: Zooma | Complete |  |

## Funktionsstatus: Verktyg {#feature-status-tools}

Det här är en lista över olika verktyg som det klassiska användargränssnittet har och status i det beröringsaktiverade användargränssnittet.

| Funktion | Status | Kommentar |
|--- |--- |--- |
| Aktivitetshantering | Ersatt | 6.0 innehåller projekt och uppgifter. |
| Inkorgen för arbetsflöde | Complete |  |
| Konfiguration av arbetsflöde till sidmall (`/etc/workflow/wcm/templates.html`) | Saknas | Använd klassiskt användargränssnitt. |
| Taggning av administratörsgränssnitt | Complete |  |
| MSM/Blueprint Control Center | Complete |  |
| Gränssnitt för BluPrint Manager | Complete |  |
| Gränssnitt för konfiguration av utrullning | Saknas | Använd klassiskt användargränssnitt. |
| Användargränssnitt, grupper och behörigheter | Mest komplett | Använd Classic UI om du vill ha mer behörighet. |
| Rensa versioner (`/etc/versioning/purge.html`) | Saknas | Använd klassiskt användargränssnitt. |
| Extern länkkontroll (`/etc/linkchecker.html`) | Saknas | Använd klassiskt användargränssnitt. |
| Massredigerare (`/etc/importers/bulkeditor.html`) | Saknas | Använd klassiskt användargränssnitt. |
| Överför miniatyrbilder för att lägga till eller skriva över dem | Saknas | Använd klassiskt användargränssnitt. |
