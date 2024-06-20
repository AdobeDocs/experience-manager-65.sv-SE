---
title: Komponenten Utkast och inskickat material
description: Komponenten Utkast och inskickningar listar formulär som är i utkastläge och som redan har skickats. Du kan anpassa komponentens utseende och stil.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
docset: aem65
exl-id: f3f013a7-a399-4178-a901-d4a8c65ddbd3
solution: Experience Manager, Experience Manager Forms
feature: Forms Portal
role: Admin, User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '744'
ht-degree: 0%

---

# Komponenten Utkast och inskickat material{#drafts-and-submissions-component}

Komponenten Utkast och inskickningar visar alla formulär som är i utkastläge och de formulär som redan har skickats. Komponenten har separata avsnitt (flikar) för utkast och skickade formulär. Användarna kan bara visa sina utkast och skickade formulär.

## Konfigurera komponenten {#configuring-the-component}

Komponenten Utkast och inskickningar har två flikar: Utkast och inskickningar.

Om du vill att ett anpassat formulär ska kunna skickas på fliken Skicka anger du **Skicka åtgärd** till **[Forms Portal Submit Action](../../forms/using/configuring-submit-actions.md). Alternativt** aktivera alternativet Forms Portal Submit. När en användare skickar formuläret läggs formuläret till på fliken Skicka.

Funktionen Utkast är aktiverad direkt. När en användare klickar **Spara** i ett adaptivt formulär läggs formuläret till på fliken Utkast.

Utför följande steg för att lägga till och konfigurera en komponent för utkast och överföringar:

1. Dra och släpp **Utkast och inskickat material** -komponenten i kategorin Document Services i komponentwebbläsaren på sidan.
1. Markera komponenten och markera sedan ![settings_icon](assets/settings_icon.png) för att öppna dialogrutan Redigera för komponenten.

   ![Komponenten Utkast och inskickning](assets/drafts-submissions-edit.png)

1. I dialogrutan Redigera anger du följande information och väljer **Klar** för att spara inställningarna.

<table>
 <tbody>
  <tr>
   <th>Tabb</th>
   <th>Konfiguration</th>
   <th>Beskrivning</th>
  </tr>
  <tr>
   <td>Allmänt</td>
   <td>Totalt resultat</td>
   <td>Anger det maximala antalet resultat som ska visas. Om antalet resultat ökar gränsen för totalt resultat, visas ett <strong>Mer </strong>-länken visas längst ned i komponenten. Klicka <strong>Mer </strong>visar alla formulär. </td>
  </tr>
  <tr>
   <td> </td>
   <td>Formattyp</td>
   <td>Anger komponentens format. Du kan ange <strong>Inget format</strong>, <strong>Standardformat</strong>, eller <strong>Eget format</strong> för att lista formulären. För alternativet Eget format kan du ange sökvägen till en anpassad CSS-fil i dialogrutan <strong>Anpassad formatsökväg </strong>fält<strong>.</strong></td>
  </tr>
  <tr>
   <td> </td>
   <td>Anpassad formatsökväg</td>
   <td>Om du väljer <strong>Eget format</strong> i <strong>Formattyp</strong> fält, använd <strong>Anpassad formatsökväg</strong> för att ange sökvägen till den anpassade CSS-filen. </td>
  </tr>
  <tr>
   <td> </td>
   <td>Visningsalternativ</td>
   <td><p>Anger vilka flikar som ska visas. Du kan välja att visa formulärutkast, skickade formulär eller både och. </p> <p><strong>Anteckning</strong>:<em> För <strong>Visningsalternativ</strong>om du väljer ett annat alternativ än <strong>Båda</strong>, <strong>Standardflik</strong> fältalternativet används inte.</em></p> </td>
  </tr>
  <tr>
   <td> </td>
   <td>Standardflik</td>
   <td>Anger fliken som ska visas när formulärportalsidan läses in. Du kan välja mellan <strong>Utkast till Forms-flik</strong> och <strong>Forms Tab skickat</strong>.</td>
  </tr>
  <tr>
   <td>Utkast till Forms Tab Configuration</td>
   <td>Egen titel</td>
   <td>Anger titeln på <strong>Utkast till Forms</strong> -fliken. Standardvärdet är <strong>Utkast till Forms.</strong></td>
  </tr>
  <tr>
   <td> </td>
   <td>Layoutmall</td>
   <td>Anger layouten som ska användas för listan med utkast till Forms.</td>
  </tr>
  <tr>
   <td>Inskickad Forms-flikkonfiguration</td>
   <td>Egen titel </td>
   <td>Anger titeln på <strong>Forms har skickats </strong>-fliken. Standardvärdet är <strong>Forms har skickats in.</strong></td>
  </tr>
  <tr>
   <td> </td>
   <td>Layoutmall</td>
   <td>Anger vilken layout som ska användas för skickad Forms<strong> </strong>lista. </td>
  </tr>
 </tbody>
</table>

## Anpassa lagringen {#customizing-the-storage}

När du använder Forms Portal-åtgärden för att skicka eller aktiverar alternativet Lagra data i formulärportalen i anpassad form, lagras formulärdata i AEM. I en produktionsmiljö bör du inte lagra utkast eller skickade formulärdata i AEM. Istället måste ni integrera utkasten och skicka-komponenten med en säker lagringsplats, t.ex. en företagsdatabas, för att lagra utkast och skickade formulärdata.

Med Forms Portal kan du lagra data på en lokal AEM, AEM eller i en databas. Med AEM Forms kan ni anpassa implementeringen av lagring av användardata för utkast och inskickade data. Du kan åsidosätta standardmetoder för att ange hur utkast- och inskickningsdata ska lagras på ett valfritt lagringsutrymme. Du kan till exempel lagra data i ett datalager som är implementerat i din organisation.

Forms Portal innehåller färdiga API:er för lagring av data i krx-databaser för AEM Forms publiceringsinstanser lokalt och på fjärrbasis. Du kan ersätta standardimplementeringarna enligt [Konfigurera lagringstjänster för utkast och överföringar](/help/forms/using/configuring-draft-submission-storage.md) artikel, med anpassade implementeringar som ersätter standardfunktioner. Mer information om vilka metoder som krävs i en anpassad implementering för att lagra innehåll på en säker plats finns i [Anpassa datatjänster för utkast och överföring](/help/forms/using/custom-draft-submission-data-services.md) och [Anpassad lagring för utkast och inskickningskomponenter.](/help/forms/using/adding-custom-storage-provider-forms.md)

AEM Forms dokumentation innehåller en [Exempel för att integrera komponent för utkast och inlämning med databas](integrate-draft-submission-database.md). Du kan använda exempelimplementeringen för att utveckla en egen anpassad implementering.

## Relaterade artiklar

* [Aktivera komponenter i formulärportalen](/help/forms/using/enabling-forms-portal-components.md)
* [Skapa portalsida för formulär](/help/forms/using/creating-form-portal-page.md)
* [Visa formulär på en webbsida med API:er](/help/forms/using/listing-forms-webpage-using-apis.md)
* [Använda komponenten Utkast och inskickat material](/help/forms/using/draft-submission-component.md)
* [Anpassa lagring av utkast och inskickade formulär](/help/forms/using/draft-submission-component.md)
* [Exempel för att integrera komponent för utkast och inlämning med databas](/help/forms/using/integrate-draft-submission-database.md)
* [Anpassa mallar för komponenter i formulärportalen](/help/forms/using/customizing-templates-forms-portal-components.md)
* [Introduktion till att publicera formulär på en portal](/help/forms/using/introduction-publishing-forms.md)
