---
title: Spara ett HTML5-formulär som ett utkast
seo-title: Spara ett HTML5-formulär som ett utkast
description: Spara ett HTML5-formulär som ett utkast och fortsätt fylla i formuläret i ett senare skede.
seo-description: Spara ett HTML5-formulär som ett utkast och fortsätt fylla i formuläret i ett senare skede.
uuid: 70cd5f6f-f125-470c-8cee-ee14d2127713
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 445e24af-cd1a-414d-bd01-9feb6631bbef
feature: Mobile Forms
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '325'
ht-degree: 2%

---


# Spara ett HTML5-formulär som ett utkast {#saving-an-html-form-as-a-draft}

Du kan spara ett HTML5-formulär som ett utkast och fortsätta fylla i formuläret i ett senare skede. Med Forms Portal kan alla användare spara och återställa ett HTML5-formulär. Om du vill aktivera funktionen Spara som utkast lägger du till följande konfigurationer i profilnoden:

## Anpassad profil som tillåter funktionen Spara som utkast {#custom-profile-to-allow-save-as-draft-feature}

AEM Forms har en **Spara som utkast**-profil. Du kan återge ett formulär med profilen Spara som utkast för att aktivera utkastsfunktioner för ett HTML5-formulär. Du kan ange HTML-återgivningsprofil för ett formulär i [Forms Manager](/help/forms/using/introduction-managing-forms.md).

Om du vill aktivera funktionen Spara som utkast för din befintliga [anpassade profil](/help/forms/using/custom-profile.md) lägger du till följande egenskaper i din anpassade profilnod:

<table>
 <tbody>
  <tr>
   <td><strong>Egenskapsnamn</strong></td>
   <td><strong>Typ</strong></td>
   <td><strong>Värde</strong></td>
   <td><strong>Beskrivning</strong></td>
  </tr>
  <tr>
   <td>mfAllowFPDraft</td>
   <td>Sträng</td>
   <td>true</td>
   <td><p>Aktiverar Spara som utkast</p> <p>för den här profilen.</p> </td>
  </tr>
  <tr>
   <td>mfAllowAttachments</td>
   <td>Sträng</td>
   <td>true</td>
   <td><p>Tillåter överföring av bilagor</p> <p>med den här profilen.</p> </td>
  </tr>
 </tbody>
</table>

## Utkastlagring och lista {#drafts-storage-and-listing}

När funktionen Spara som utkast har aktiverats för ett formulär. när formuläret sparas visas det i [Komponenten Utkast och överföring](/help/forms/using/draft-submission-component.md). Du kan hämta och börja fylla i det sparade formuläret från komponenten Utkast och Skicka.

Om du vill aktivera formulärlistor för komponenterna Utkast och Skicka lägger du till följande egenskap i profilnoden:

<table>
 <tbody>
  <tr>
   <td><strong>Egenskapsnamn</strong></td>
   <td><strong>Typ</strong></td>
   <td><strong>Värde</strong></td>
   <td><strong>Beskrivning</strong></td>
  </tr>
  <tr>
   <td>fp.enablePortalSubmit</td>
   <td>Sträng</td>
   <td>true</td>
   <td>Aktivera att utkast och formulär listas i <br /> Forms Portal-komponenten Utkast och inskickningar efter inskickning</td>
  </tr>
 </tbody>
</table>

Som standard lagrar AEM Forms användardata som är kopplade till utkastet och överföringen av ett formulär i noden /content/forms/fp i publiceringsinstansen. Du kan lägga till din anpassade lagringsleverantör. Mer information finns i [Anpassad lagring för komponenten Utkast och överföringar](/help/forms/using/adding-custom-storage-provider-forms.md).
