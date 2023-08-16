---
title: Kompatibilitetspaket
seo-title: Compatibility Package
description: Genom att installera Kompatibilitetspaketet på AEM Forms 6.5 kan du använda Correspondence Management-resurser från AEM Forms 6.4 och tidigare versioner samt inaktuella adaptiva formulärmallar och sidor
seo-description: Installing the Compatibility package on AEM Forms 6.4 lets you use the Correspondence Management assets from AEM Forms 6.4 and deprecated adaptive forms templates and pages
uuid: b49633d6-2cb3-422c-a314-25f3b8a37b7f
contentOwner: gtalwar
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management, installing
geptopics: SG_AEMFORMS/categories/jee
discoiquuid: 73e8ccc6-f857-493e-b6e3-878f93e2a356
docset: aem65
role: Admin
exl-id: bb16017c-a1bf-40d8-a78d-827c05b7ee2e
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 0%

---

# Kompatibilitetspaket{#compatibility-package}

## Översikt {#overview}

Interaktiv kommunikation är standardmetoden och rekommenderas för att skapa kundkommunikation i AEM Forms 6.5. Om du vill fortsätta använda brev i AEM Forms 6.5 måste du installera den senaste [AEMFD-kompatibilitetspaket](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html).

Med paketet AEMFD-kompatibilitet kan du [använda följande resurser från AEM Forms 6.4, 6.3 och 6.2 i AEM Forms 6.5:](../../forms/using/compatibility-package.md#add-support-for-aem-forms-and-assets-in-aem-forms)

* Dokumentfragment
* Bokstäver
* Dataordlistor
* Mallar och sidor för anpassade formulär har tagits bort

Mer information finns i [Resurser som gjorts kompatibla med AEM Forms 6.5 genom att installera kompatibilitetspaketet](../../forms/using/compatibility-package.md#assetsmadecompatible).

## Lägg till stöd för AEM Forms 6.4, 6.3 och 6.2-material i AEM Forms 6.5 {#add-support-for-aem-forms-and-assets-in-aem-forms}

När du har utfört en uppgradering gör du följande för att installera AEMFD-kompatibilitetspaketet och göra dina resurser kompatibla med 6.5:

Se till att du har [AEM](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html) förinstallerat.

1. Installera senaste 6.5 [Kompatibilitetspaket](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html).

   Mer information om hur du överför och installerar paketet finns i [Arbeta med paket](/help/sites-administering/package-manager.md).

1. Starta om servern när loggarna har stabiliserats.
1. Använd flyttningsverktyget för att göra dina resurser kompatibla med 6.5.

   Mer information finns i [migreringsverktyg](../../forms/using/migration-utility.md).

## Resurser som gjorts kompatibla med AEM Forms 6.5 genom att installera kompatibilitetspaketet {#assetsmadecompatible}

Genom att installera Kompatibilitetspaketet kan du göra följande resurser och mallar kompatibla med AEM Forms 6.5:

* Correspondence Management Assets från AEM 6.4 och tidigare:

   * [Bokstäver](../../forms/using/create-letter.md)
   * [Dataordlistor](/help/forms/using/data-dictionary.md)
   * Dokumentfragment

* Mallar som inte längre används för anpassade formulär:

   * /libs/fd/af/templates/blankTemplate2
   * /libs/fd/af/templates/simpleEnrollmentTemplate
   * /libs/fd/af/templates/simpleEnrollmentTemplate2
   * /libs/fd/af/templates/surveyTemplate
   * /libs/fd/af/templates/surveyTemplate2
   * /libs/fd/af/templates/tabbedEnrollmentTemplate
   * /libs/fd/af/templates/tabbedEnrollmentTemplate2
   * /libs/fd/afaddon/templates/advancedEnrollmentTemplate
   * /libs/fd/afaddon/templates/advancedEnrollmentTemplate2

* Sidor med adaptiva formulär har tagits bort:

   * /libs/fd/af/components/page/survey
   * /libs/fd/af/components/page/tabbedenrollment
   * /libs/fd/afaddon/components/page/advancedRotering
