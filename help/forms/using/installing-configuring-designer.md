---
title: Installera och konfigurera Designer
description: Designer finns som fristående installationsprogram och medföljer också Workbench. Lär dig installera fristående Designer.
contentOwner: gtalwar
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: designer
geptopics: SG_AEMFORMS/categories/jee
docset: aem65
role: Admin
exl-id: 90503d29-e079-43f4-a5dc-ce90ed7844c6
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '471'
ht-degree: 0%

---

# Installera och konfigurera Designer{#installing-and-configuring-designer}

## Krav {#pre-requisites}

* Installera 32-bitarsversionen av  [Visual C++ 2019 Redistributable (x86)](https://learn.microsoft.com/en-us/cpp/windows/latest-supported-vc-redist?view=msvc-170). Kontrollera att tidigare nämnda omdistribuerbara körtidspaket är installerade innan du startar installationen.
* En användare med administratörsbehörighet för att installera eller avinstallera AEM Forms Designer.

## Installera AEM Forms Designer {#install-designer}

Designer är tillgängligt som ett fristående installationsprogram och ingår även i WorkBench. Om du använder ett fristående installationsprogram för AEM Forms Designer utför du följande steg:

1. Avinstallera den tidigare versionen av AEM Forms Designer, om den redan är installerad.
1. Hämta Designer från [Adobe licenswebbplats](https://licensing.adobe.com/).

   >[!NOTE]
   >
   > * Adobe Experience Manager 6.5 Forms Service Pack 15 (6.5.15.0) och senare Forms Designer-version innehåller även Service Pack-versionen. Exempel: för Service Pack 15 är versionsnumret 6.5.15.2022112.1.0. I det här exemplet är 6.5.15 Service Pack-version.

1. Starta installationsprogrammet för AEM Forms Designer genom att dubbelklicka på setup.exe.
1. Fortsätt och ange dina uppgifter och serienumret på skärmen Personalisering.
1. Om du godkänner licensavtalet fortsätter du genom att klicka på Nästa.
1. (Valfritt) ändra standardinstallationssökvägen om du vill installera Designer på en valfri plats. Klicka på Nästa.
1. Klicka på Föregående om du vill ändra några inställningar. Klicka på Installera om du vill installera Designer.
1. Klicka på Slutför när installationen är klar.

Du kan också installera AEM Forms Designer via kommandoraden i passivt eller tyst läge.

* Passiv installation via kommandoraden: Installationsprogrammet visar en förloppsindikator som anger att installationen pågår, men inga meddelanden eller felmeddelanden visas. När du har startat programmet kan du inte avbryta installationen.

```shell
msiexec /i "<absolute path>\Designer.msi" /passive SERIALNUMBER=****-****-****-****-****-****
```

* Tyst kommandoradsinstallation: Installationsprogrammet kör installationen utan att visa ett användargränssnitt. Inga uppmaningar, meddelanden eller dialogrutor visas. När du har startat programmet kan du inte avbryta installationen.

```shell
msiexec /i "<absolute path>\Designer.msi" /quiet SERIALNUMBER=****-****-****-****-****-****
```

## Uppdatera AEM Forms Designer {#update-forms-designer}

Det finns två fall när den senaste versionen av AEM Forms Designer 6.5.16.0 uppdateras:

* **Fall 1**: När användaren har en tidigare version av AEM Forms Designer än 6.5.15.0.
* **Fall 2**: När användaren har version 6.5.15.0 av AEM Forms Designer.

+++**När användaren har en tidigare version av AEM Forms Designer än 6.5.15.0.**

Om du använder ett fristående installationsprogram för AEM Forms Designer utför du följande steg:

1. Före installation **AEM Forms Designer 6.5.16.0** måste användare avinstallera tidigare versioner.
1. Hämta och installera [AEM Forms Designer 6.5.15.0](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html) på sidan AEM formulärreleaser.
1. När installationen av **AEM Forms Designer 6.5.15.0**, hämta och installera [AEM Forms Designer 6.5.16.0](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html) genom att dubbelklicka på den hämtade installationsfilen.

+++

+++**När användaren har version 6.5.15.0 av AEM Forms Designer**

Om du använder ett fristående installationsprogram för AEM Forms Designer utför du följande steg:
1. Hämta den senaste versionen av AEM Forms Designer från [Programdistributionsportal](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html).
1. Installera den senaste versionen av AEM Forms Designer genom att dubbelklicka på den hämtade installationsfilen.

+++