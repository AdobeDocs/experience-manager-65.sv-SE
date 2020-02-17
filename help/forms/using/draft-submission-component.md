---
title: Komponenten Utkast och inskickat material
seo-title: Komponenten Utkast och inskickat material
description: Komponenten Utkast och inskickningar listar formulär som är i utkastläge och som redan har skickats. Du kan anpassa komponentens utseende och stil.
seo-description: Komponenten Utkast och inskickningar listar formulär som är i utkastläge och som redan har skickats. Du kan anpassa komponentens utseende och stil.
uuid: 42c205b5-3141-4b80-85d9-dad921e223a2
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: ad71b423-02e1-4476-9c7c-f832cea6b0a6
docset: aem65
translation-type: tm+mt
source-git-commit: 23252989bb8649b2f0b96a58972c831257e0c5dc

---


# Komponenten Utkast och inskickat material{#drafts-and-submissions-component}

Komponenten Utkast och inskickningar visar alla formulär som är i utkastläge och de formulär som redan har skickats. Komponenten har separata avsnitt (flikar) för utkast och skickade formulär. Användarna kan bara visa sina utkast och skickade formulär.

## Konfigurera komponenten {#configuring-the-component}

Komponenten Utkast och överföringar har två flikar: Utkast och inskickat material.

Om du vill att ett anpassat formulär ska visas på fliken Skicka anger du åtgärden **** Skicka till **[formulärportalåtgärden](../../forms/using/configuring-submit-actions.md). Du kan också&#x200B;**aktivera alternativet Skicka i formulärportalen. När en användare skickar formuläret läggs formuläret till på fliken Skicka.

Funktionen Utkast är aktiverad direkt. När en användare klickar på **Spara** i ett anpassat formulär läggs formuläret till på fliken Utkast.

Utför följande steg för att lägga till och konfigurera en komponent för utkast och överföringar:

1. Dra och släpp komponenten **Utkast och överföringar** under kategorin Dokumenttjänster i komponentwebbläsaren till sidan.
1. Tryck på komponenten och tryck sedan på ![settings_icon](assets/settings_icon.png) för att öppna dialogrutan Redigera för komponenten.

   ![Komponenten Utkast och inskickning](assets/drafts-submissions-edit.png)

1. I dialogrutan Redigera anger du följande information och trycker på **Klar** för att spara inställningarna.

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
   <td>Anger det maximala antalet resultat som ska visas. Om antalet resultat ökar gränsen för totalt resultat visas en <strong>mer- </strong>länk längst ned i komponenten. Om du klickar på <strong>Mer </strong>visas alla formulär. </td>
  </tr>
  <tr>
   <td> </td>
   <td>Formattyp</td>
   <td>Anger komponentens format. Du kan ange <strong>Inget format</strong>, <strong>Standardformat</strong>eller <strong>Eget format</strong> för att visa formulären. För alternativet Eget format kan du ange sökvägen till den anpassade CSS-filen i <strong>fältet </strong><strong>Anpassad formatsökväg.</strong></td>
  </tr>
  <tr>
   <td> </td>
   <td>Anpassad formatsökväg</td>
   <td>Om du väljer alternativet <strong>Egen stil</strong> i fältet <strong>Formattyp</strong> använder du fältet <strong>Anpassad formatsökväg</strong> för att ange sökvägen till den anpassade CSS-filen. </td>
  </tr>
  <tr>
   <td> </td>
   <td>Visningsalternativ</td>
   <td><p>Anger vilka flikar som ska visas. Du kan välja att visa formulärutkast, skickade formulär eller både och. </p> <p><strong></strong> Obs<em>: Om du väljer något annat alternativ än <strong>Båda</strong>för <strong>visningsalternativ</strong>används inte alternativet <strong>Standardflik</strong> .</em></p> </td>
  </tr>
  <tr>
   <td> </td>
   <td>Standardflik</td>
   <td>Anger fliken som ska visas när formulärportalsidan läses in. Du kan välja mellan fliken <strong>Utkastformulär</strong> och fliken <strong></strong>Skickade formulär.</td>
  </tr>
  <tr>
   <td>Konfiguration av fliken Utkastformulär</td>
   <td>Egen titel</td>
   <td>Anger titeln på fliken <strong>Utkastformulär</strong> . Standardvärdet är <strong>Utkastformulär.</strong></td>
  </tr>
  <tr>
   <td> </td>
   <td>Layoutmall</td>
   <td>Anger den layout som ska användas för listan Utkastformulär.</td>
  </tr>
  <tr>
   <td>Konfiguration av fliken Skickade formulär</td>
   <td>Egen titel </td>
   <td>Anger titeln på <strong>fliken </strong>Skickade formulär. Standardvärdet är <strong>Skickade formulär.</strong></td>
  </tr>
  <tr>
   <td> </td>
   <td>Layoutmall</td>
   <td>Anger den layout som ska användas för<strong> listan Skickade formulär </strong>. </td>
  </tr>
 </tbody>
</table>

## Anpassa lagringen {#customizing-the-storage}

När du använder formulärportalens överföringsåtgärd eller aktiverar alternativet Lagra data i formulärportalen i anpassad form, lagras formulärdata i AEM-databasen. I en produktionsmiljö bör du inte lagra utkast eller inskickade formulärdata i AEM-databasen. Istället måste ni integrera utkasten och skicka-komponenten med en säker lagringsplats, t.ex. en företagsdatabas, för att lagra utkast och skickade formulärdata.

I Forms-portalen kan du lagra data i en lokal AEM-databas, fjärr-AEM-databas eller i en databas. Med AEM Forms kan ni anpassa implementeringen av lagring av användardata för utkast och inskickade data. Du kan åsidosätta standardmetoder för att ange hur utkast- och inskickningsdata ska lagras på ett valfritt lagringsutrymme. Du kan till exempel lagra data i ett datalager som är implementerat i din organisation.

Forms-portalen innehåller färdiga API:er för lagring av data i krx-databaser för lokala och fjärranslutna AEM Forms-publiceringsinstanser. Du kan ersätta standardimplementeringarna, som beskrivs i [Konfigurera lagringstjänster för utkast och inskickade](/help/forms/using/configuring-draft-submission-storage.md) artiklar, med anpassade implementeringar som ersätter standardfunktionerna. Mer information om vilka metoder som krävs i en anpassad implementering för att lagra innehåll på en säker plats finns i [Anpassa datatjänster](/help/forms/using/custom-draft-submission-data-services.md) för utkast och överföring samt [Anpassad lagring för komponenter för utkast och inskickning.](/help/forms/using/adding-custom-storage-provider-forms.md)

I dokumentationen för AEM Forms finns ett exempel [på hur du integrerar utkast och inskickningskomponenter med databaser](integrate-draft-submission-database.md). Du kan använda exempelimplementeringen för att utveckla en egen anpassad implementering.

## Relaterade artiklar

* [Aktivera komponenter i formulärportalen](/help/forms/using/enabling-forms-portal-components.md)
* [Skapa portalsida för formulär](/help/forms/using/creating-form-portal-page.md)
* [Visa formulär på en webbsida med API:er](/help/forms/using/listing-forms-webpage-using-apis.md)
* [Använda komponenten Utkast och inskickat material](/help/forms/using/draft-submission-component.md)
* [Anpassa lagring av utkast och inskickade formulär](/help/forms/using/draft-submission-component.md)
* [Exempel för att integrera komponent för utkast och inlämning med databas](/help/forms/using/integrate-draft-submission-database.md)
* [Anpassa mallar för komponenter i formulärportalen](/help/forms/using/customizing-templates-forms-portal-components.md)
* [Introduktion till att publicera formulär på en portal](/help/forms/using/introduction-publishing-forms.md)
