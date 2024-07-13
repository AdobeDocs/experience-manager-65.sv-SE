---
title: Spara ett HTML5-formulär som ett utkast
description: Spara ett HTML5-formulär som ett utkast och fortsätt fylla i formuläret i ett senare skede.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 445e24af-cd1a-414d-bd01-9feb6631bbef
feature: HTML5 Forms,Mobile Forms
exl-id: a9879445-d626-4279-8a95-a9009294b483
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '299'
ht-degree: 0%

---

# Spara ett HTML5-formulär som ett utkast {#saving-an-html-form-as-a-draft}

Du kan spara ett HTML 5-formulär som ett utkast och sedan fortsätta att fylla i formuläret i ett senare skede. Med Forms Portal kan alla användare spara och återställa ett HTML5-formulär. Om du vill aktivera funktionen Spara som utkast lägger du till följande konfigurationer i profilnoden:

## Anpassad profil som tillåter funktionen Spara som utkast {#custom-profile-to-allow-save-as-draft-feature}

AEM Forms tillhandahåller en **Spara som utkast**-profil. Du kan återge ett formulär med profilen Spara som utkast om du vill aktivera utkastsfunktionen för ett HTML5-formulär. Du kan ange återgivningsprofilen HTML för ett formulär i [Forms Manager](/help/forms/using/introduction-managing-forms.md).

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

## Utkastlagring och listning {#drafts-storage-and-listing}

När du har aktiverat funktionen Spara som utkast för ett formulär. När formuläret sparas visas det i komponenten [Utkast och överföring](/help/forms/using/draft-submission-component.md). Du kan hämta och börja fylla i det sparade formuläret med komponenterna Utkast och Skicka.

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
   <td>Så här aktiverar du utkast och formulär att listas i <br /> Forms Portal Drafts &amp; Submissions-komponent efter överföring</td>
  </tr>
 </tbody>
</table>

Som standard lagrar AEM Forms användardata som är kopplade till utkastet och inskickandet av ett formulär i noden /content/forms/fp i Publish-instansen. Du kan lägga till din anpassade lagringsleverantör. Mer information finns i [Anpassad lagring för komponenten Utkast och överföringar](/help/forms/using/adding-custom-storage-provider-forms.md).
