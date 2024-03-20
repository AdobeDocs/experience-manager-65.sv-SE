---
title: Grundläggande hantering
description: Översikt över grundläggande hantering när du använder Adobe Experience Manager redigeringsmiljö. Den använder platskonsolen som grund.
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
exl-id: 2981dc20-b2ba-4ea2-a53b-8b5fe526aa9c
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '1161'
ht-degree: 0%

---

# Grundläggande hantering{#basic-handling}

>[!NOTE]
>
>* Den här sidan är avsedd att ge en översikt över grundläggande hantering när du använder Adobe Experience Manager (AEM) redigeringsmiljö. Den använder **Webbplatser** som bas.
>
>* Vissa funktioner är inte tillgängliga i alla konsoler och ytterligare funktioner är tillgängliga i vissa konsoler. Specifik information om de enskilda konsolerna och deras relaterade funktioner beskrivs mer ingående på andra sidor.
>* Kortkommandon är tillgängliga i hela AEM. I synnerhet när [använda konsoler](/help/sites-classic-ui-authoring/author-env-keyboard-shortcuts.md) och [redigera sidor](/help/sites-classic-ui-authoring/classic-page-author-keyboard-shortcuts.md).
>

## Välkomstskärmen {#the-welcome-screen}

Det klassiska användargränssnittet innehåller ett urval av konsoler, med välkända metoder för att navigera och initiera åtgärder, bland annat klicka, dubbelklicka och [snabbmenyer](#context-menus).

När du har loggat in visas välkomstskärmen. Här finns en lista med länkar till konsoler och tjänster:

![screen_shot_2012-01-30at61745pm](assets/screen_shot_2012-01-30at61745pm.png)

## Konsoler {#consoles}

Huvudkonsolerna är:

<table>
 <tbody>
  <tr>
   <td><strong>Konsol</strong></td>
   <td><strong>Syfte</strong></td>
  </tr>
  <tr>
   <td><strong>Välkommen</strong></td>
   <td>Ger en översikt och direkt åtkomst (via länkar) till AEM huvudfunktioner.</td>
  </tr>
  <tr>
   <td><strong>Digital Assets</strong><br /> </td>
   <td>Med dessa konsoler kan du importera och <a href="/help/sites-classic-ui-authoring/classicui-assets.md">hantera digitala resurser</a> som bilder, videor, dokument och ljudfiler. Dessa resurser kan sedan användas av alla webbplatser som körs på samma AEM. </td>
  </tr>
  <tr>
   <td><strong>Launches</strong></td>
   <td>Detta hjälper dig att hantera dina <a href="/help/sites-classic-ui-authoring/classic-launches.md">starter</a>; dessa gör att du kan utveckla innehållet för en framtida release av en eller flera aktiverade webbsidor.<br /> <i>Obs! I det beröringskänsliga användargränssnittet finns mycket av samma funktionalitet i webbplatskonsolen, tillsammans med referenslisten.</i> <i>Om det behövs är konsolen tillgänglig från verktygskonsolen. Välj Åtgärder och starta sedan.</i></td>
  </tr>
  <tr>
   <td><strong>Inkorg </strong></td>
   <td>Oftast är det olika personer som är inblandade i underuppgifterna i ett arbetsflöde och varje person måste slutföra sitt steg innan han eller hon kan lämna jobbet till nästa person. I Inkorgen kan du se meddelanden som rör sådana uppgifter. Se <a href="/help/sites-administering/workflows.md">Arbeta med arbetsflöden</a>. <br /> </td>
  </tr>
  <tr>
   <td><strong>Taggar</strong></td>
   <td>Med taggningskonsolerna kan du administrera taggar. Taggar är korta namn eller fraser som du kan använda för att klassificera och kommentera innehållsdelar, vilket gör det enklare att hitta och ordna dem. Mer information finns i <a href="/help/sites-classic-ui-authoring/classic-feature-tags.md">Använda och hantera taggar</a>.</td>
  </tr>
  <tr>
   <td><strong>verktyg</strong></td>
   <td>The <a href="/help/sites-administering/tools-consoles.md">Verktygskonsoler</a> ger tillgång till flera specialiserade verktyg och konsoler som hjälper dig att administrera dina webbplatser, digitala resurser och andra aspekter av innehållsdatabasen.</td>
  </tr>
  <tr>
   <td><strong>Användare</strong></td>
   <td>Med dessa konsoler kan du hantera åtkomsträttigheter för användare och grupper. Mer information finns i <a href="/help/sites-administering/security.md">Användaradministration och -säkerhet</a>.<br /> </td>
  </tr>
  <tr>
   <td><strong>Webbplatser</strong></td>
   <td>Med konsolerna Webbplatser/Webbplatser kan du <a href="/help/sites-classic-ui-authoring/classic-page-author.md">skapa, visa och hantera webbplatser</a> som körs på din AEM. Med dessa konsoler kan du skapa, kopiera, flytta och ta bort webbsidor, starta arbetsflöden och aktivera (publicera) sidor. Du kan också öppna en sida för redigering.<br /> </td>
  </tr>
  <tr>
   <td><strong>Arbetsflöden</strong></td>
   <td>Ett arbetsflöde är en definierad serie steg som beskriver processen att slutföra en uppgift. Ofta är flera personer inblandade i en uppgift och varje person måste slutföra sitt steg innan han eller hon kan lämna jobbet till nästa person. Med arbetsflödeskonsolen kan du skapa arbetsflödesmodeller och hantera arbetsflödesinstanser som körs. Se <a href="/help/sites-administering/workflows.md">Arbeta med arbetsflöden</a>.<br /> </td>
  </tr>
 </tbody>
</table>

The **Webbplatser** I konsolen finns två rutor där du kan navigera och hantera dina sidor:

* Vänster ruta

  Här visas trädstrukturen för dina webbplatser och sidorna på dessa webbplatser.

  Här visas även information om andra aspekter eller AEM, bland annat projekt, ritningar och resurser.

* Höger ruta

  Här visas sidorna (på den plats som är markerad i den vänstra rutan) och de kan användas för att vidta åtgärder.

Härifrån kan du [hantera sidor](/help/sites-authoring/managing-pages.md) med verktygsfältet, en snabbmeny eller genom att öppna en sida för ytterligare åtgärder.

>[!NOTE]
>
>Den grundläggande hanteringen är densamma i alla konsoler. Det här avsnittet koncentreras på **Webbplatser** som den primära konsolen som används vid redigering.

![chlimage_1-9](assets/chlimage_1-9a.png)

## Få hjälp {#accessing-help}

På olika konsoler (till exempel Webbplatser) kan du **Hjälp** är tillgänglig. Klicka **Hjälp** öppnar antingen Package Share eller dokumentationswebbplatsen.

![chlimage_1-10](assets/chlimage_1-10a.png)

När du redigerar en sida [sidekick har även en knapp för att komma åt hjälpen](/help/sites-classic-ui-authoring/classic-page-author-env-tools.md#accessing-help).

## Navigera med webbplatskonsolen {#navigating-with-the-websites-console}

The **Webbplatser** konsolen visar sidorna i en trädstruktur (vänster ruta). För att underlätta navigeringen kan delar av trädstrukturen expanderas (+) eller komprimeras (-) efter behov:

* När du klickar på sidnamnet i den vänstra rutan händer följande:

   * Visar de underordnade sidorna i den högra rutan
   * Expanderar strukturen i den vänstra rutan.

     Av prestandaskäl beror den här åtgärden på antalet underordnade noder. Med en standardinstallation fungerar den här utbyggnadsmetoden när det finns `30` eller färre underordnade noder.

* Om du dubbelklickar på sidnamnet (den vänstra rutan) expanderas trädet, men eftersom sidan öppnas samtidigt är effekten inte så självklar.

>[!NOTE]
>
>Det här standardvärdet ( `30`) kan ändras per konsol i dina programspecifika konfigurationer av webbplatsadmin-widgeten:
>
>På noden siteAdmin:
>
>Ange egenskapens värde:
>`treeAutoExpandMax`
>den:
>`/apps/wcm/core/content/siteadmin`
>
>Eller globalt i temat:
>Ange värdet för:
>`TREE_AUTOEXPAND_MAX`
>in:
>`/apps/cq/ui/widgets/themes/default/widgets/wcm/SiteAdmin.js`
>
>Se [SiteAdmin i CQ Widget API](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.wcm.SiteAdmin) för mer information.

## Sidinformation på webbplatskonsolen {#page-information-on-the-websites-console}

Den högra rutan i **Webbplatser** konsolen innehåller en listvy med information om sidor:

![page-info](assets/page-info.png)

Följande är tillgängliga. En delmängd av dessa fält visas som standard:

<table>
 <tbody>
  <tr>
   <td><strong>Kolumn</strong></td>
   <td><strong>Beskrivning</strong></td>
  </tr>
  <tr>
   <td>Miniatyrbild</td>
   <td>Visar en miniatyrbild för sidan.</td>
  </tr>
  <tr>
   <td>Titel</td>
   <td>Titeln som visas på sidan</td>
  </tr>
  <tr>
   <td>Namn</td>
   <td>Namnet AEM refererar till sidan</td>
  </tr>
  <tr>
   <td>Publicerad</td>
   <td>Anger om sidan har publicerats och anger publiceringsdatum och -tid.</td>
  </tr>
  <tr>
   <td>Ändrad</td>
   <td>Anger om sidan har ändrats och anger ändringsdatum och -tid. Om du vill spara en ändring måste du aktivera sidan.</td>
  </tr>
  <tr>
   <td>Scene7 Publish</td>
   <td>Anger om sidan har publicerats till Scene7.<br /> </td>
  </tr>
  <tr>
   <td>Status</td>
   <td>Anger sidans status, t.ex. om sidan är en del av ett arbetsflöde eller en livekopia, eller om en sida är låst.</td>
  </tr>
  <tr>
   <td>Impressions</td>
   <td>Visar aktiviteten på en sida i antal träffar.</td>
  </tr>
  <tr>
   <td>Mall</td>
   <td>Anger mallen som en sida baseras på.</td>
  </tr>
  <tr>
   <td>I arbetsflöde</td>
   <td>Anger när sidan är i ett arbetsflöde.</td>
  </tr>
  <tr>
   <td>Låst av</td>
   <td>Visar när en sida har låsts och användarkontot som har låst den.</td>
  </tr>
  <tr>
   <td>Live Copy</td>
   <td>Anger när sidan ingår i en live-kopia.</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Om du vill markera kolumnerna som ska visas håller du musen över en kolumnrubrik. En nedrullningsbar meny visas, och härifrån kan du använda **Kolumner** alternativ.

Färgerna bredvid sidorna i **Publicerad** och **Ändrad** kolumner anger publiceringsstatus:

| **Kolumn** | **Färg** | **Beskrivning** |
|---|---|---|
| Publicerad | Grön | Publiceringen lyckades. Innehåll publiceras. |
| Publicerad | Gul | Publicering väntar. Systemet har ännu inte bekräftat publiceringen. |
| Publicerad | Röd | Publiceringen misslyckades. Det finns ingen anslutning till publiceringsinstansen. Det kan också betyda att innehållet inaktiverades. |
| Publicerad | *blank* | Den här sidan har aldrig publicerats. |
| Ändrad | Blå | Sidan har ändrats sedan den senaste publikationen. |
| Ändrad | *blank* | Den här sidan har aldrig ändrats eller så har den inte ändrats sedan den senaste publikationen. |

## Snabbmenyer {#context-menus}

Det klassiska användargränssnittet använder välkända metoder för att navigera och initiera åtgärder, inklusive att klicka och dubbelklicka. Beroende på den aktuella situationen finns det även en rad snabbmenyer (som öppnas med höger musknapp):

![chlimage_1-11](assets/chlimage_1-11a.png)
