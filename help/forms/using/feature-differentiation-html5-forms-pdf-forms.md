---
title: Skillnaden mellan HTML5-formulär och PDF forms
seo-title: Skillnaden mellan HTML5-formulär och PDF forms
description: Funktion som stöds i HTML5-formulär och PDF forms
seo-description: Funktion som stöds i HTML5-formulär och PDF forms
uuid: 6ddee197-d108-4897-9976-77d115a06504
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: bdd97c20-d1f2-4898-9862-1a6a8071be88
docset: aem65
feature: Mobile Forms
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '462'
ht-degree: 2%

---


# Skillnaden mellan HTML5-formulär och PDF forms {#feature-differentiation-between-html-forms-and-pdf-forms}

Följande tabell anger vilka funktioner som stöds för HTML5-formulär och PDF forms:

<table>
 <tbody>
  <tr>
   <th>Funktion</th>
   <th>HTML5 Forms</th>
   <th>PDF</th>
  </tr>
  <tr>
   <td>Streckkoder<br /> </td>
   <td>Inte tillgängligt på användargränssnittsnivå. </td>
   <td>Stöds</td>
  </tr>
  <tr>
   <td>Signaturfält<br /> </td>
   <td><strong>Digitala </strong> signaturer stöds inte, men ett nytt  <strong>klottrigt </strong> signaturfält läggs till för papper som signaturer. Man kan klottra sin signatur i formuläret med fältet <strong>Klottsignatur</strong>. Signaturen sparas i formuläret som en bild. Du kan spara geopositioneringsinformation i fältet <strong>Klottsignatur</strong>.</td>
   <td>Signaturfält är tillgängligt för <strong>digitala signaturer</strong>.</td>
  </tr>
  <tr>
   <td>Datasammanfogning</td>
   <td>Stöds</td>
   <td>Stöds</td>
  </tr>
  <tr>
   <td>Bilder</td>
   <td>Data-URI-schemat används för att visa bilder. Alla moderna versioner av webbläsare har stöd för det här schemat, men det finns skillnader i det intervall med bildformat som varje webbläsare har stöd för.<br /> </td>
   <td>Formaten .gif, .png, .jpeg, .bmp och .tiff stöds.</td>
  </tr>
  <tr>
   <td>Sidnumrering<br /> </td>
   <td><p>Ett HTML5-formulär är uppdelat i paneler och rutor för att ge det ett utseende som liknar PDF forms. Sidstorleken beräknas dynamiskt. Om allt innehåll på en sida i ett HTML5-formulär tas bort eller markeras som dolt, döljs den tomma sidan och inget tomt utrymme (blanksteg) visas mellan sidorna ovanför och under den tomma sidan.</p> <p>Om datasammanfogning eller skript lägger till innehåll på en sida utökas sidans längd så att det nya innehållet får plats. Inga nya sidor läggs till i formuläret så att det nya innehållet får plats. </p> <p><strong>Obs!</strong> När allt innehåll på en sida i ett HTML5-formulär tas bort eller markeras som dolt, förblir den tomma sidan (tomt utrymme) synlig mellan första och andra sidan, men inte mellan andra sidor.</p> </td>
   <td>Sidnumrering i PDF-dokument beror på det sammanfogade datainnehållet eller på om användarinnehållet och antalet sidor ökar eller minskar baserat på det.</td>
  </tr>
  <tr>
   <td>Sidhuvuden/sidfötter </td>
   <td>Stöds. <br /> <br /> Eftersom mobilformulär i HTML5 inte stöder sidbrytningar visas sidhuvuden och sidfötter endast en gång. Du kan dock konfigurera dem i layouten så att de visas på flera ställen i förhandsgranskningen av mobilformulär.<br /> </td>
   <td>Stöds.</td>
  </tr>
  <tr>
   <td>Anpassade widgetar</td>
   <td>Du kan anpassa widgetar för att förbättra användarupplevelsen på mobila enheter.<br /> </td>
   <td>Alla widgetar är låsta och ingen anpassad widget kan kopplas.<br /> </td>
  </tr>
  <tr>
   <td>XFA Script API</td>
   <td>Stöder de vanligaste XFA-skriptkonstruktionerna. Mer information finns i <a href="/help/forms/using/scripting-support.md">skriptstöd</a>.</td>
   <td>Stöder alla XFA-skriptkonstruktioner.</td>
  </tr>
  <tr>
   <td>Acrobat Script API:er </td>
   <td>HTML5-formulär har stöd för de vanligaste API:erna. Mer information finns i <a href="/help/forms/using/scripting-support.md">skriptstöd</a>.</td>
   <td>Om PDF-filen öppnas i Acrobat eller Reader stöds även alla skript-API:er som finns i Acrobat.</td>
  </tr>
  <tr>
   <td>Stöd för höger-till-vänster-språk </td>
   <td>Stöds</td>
   <td>Stöds</td>
  </tr>
 </tbody>
</table>

<!--Follow the best practices to enable a form template for HTML5 renditions and ensure that the behavior and appearance of HTML5 forms and XFA-based PDF is consistent. For detailed list of best practices, see [Best practices to design an HTML5 form.](/help/forms/using/best-practices-design-html5-forms.md)-->
