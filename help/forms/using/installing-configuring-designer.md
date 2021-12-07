---
title: Installera och konfigurera Designer
seo-title: Installing and configuring Designer
description: 'Designer finns som fristående installationsprogram och medföljer också Workbench. Lär dig hur du installerar fristående Designer.  '
seo-description: Designer is available as a stand-alone installer and is also bundled with Workbench. Learn how to install stand-alone Designer.
uuid: c5b779d1-cb6a-48f4-87d6-48464753e516
contentOwner: gtalwar
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: designer
geptopics: SG_AEMFORMS/categories/jee
discoiquuid: f3a5b5ce-2262-4d5d-a8ae-d59a3a4229e7
docset: aem65
role: Admin
exl-id: 90503d29-e079-43f4-a5dc-ce90ed7844c6
source-git-commit: a3cf926bde4a4b3a0810058e84ac01012a4a3a57
workflow-type: tm+mt
source-wordcount: '280'
ht-degree: 26%

---

# Installera och konfigurera Designer{#installing-and-configuring-designer}

## Krav {#pre-requisites}

AEM Forms Designer-installationsprogrammet kräver 32-bitarsversionen av [Visual C++ redistributable runtime package 2012](https://support.microsoft.com/en-us/topic/the-latest-supported-visual-c-downloads-2647da03-1eea-4433-9aff-95f26a218cc0) och [Visual C++ redistributable runtime package 2013](https://support.microsoft.com/en-in/help/3179560/update-for-visual-c-2013-and-visual-c-redistributable-package). Kontrollera att tidigare nämnda omdistribuerbara körtidspaket är installerade innan du startar installationen.

Du behöver administratörsbehörighet för att installera eller avinstallera Designer.

## Installera Designer {#install-designer}

Designer är tillgängligt som ett fristående installationsprogram och ingår även i WorkBench. Om du använder ett fristående installationsprogram för Designer utför du följande steg:

1. Hämta Designer från Adobe [Licenswebbplats](https://licensing.adobe.com/).

   >[!NOTE]
   >
   >Om du har en tidigare version av Designer installerad avinstallerar du den tidigare versionen innan du fortsätter.

1. Starta installationen av Designer genom att dubbelklicka på setup.exe.
1. Gå vidare genom att ange dina uppgifter samt serienummer på den anpassade skärmen.
1. Klicka på Nästa om du godkänner licensavtalet.
1. Om du vill välja vilken plats Designer ska installeras på ändrar du standardsökväg för installation (valfritt). Klicka på Nästa.
1. Klicka på Tillbaka för att ändra inställningar. Installera Designer genom att klicka på Installera.
1. Klicka på Slutför när installationen är genomförd.

Du kan också installera Designer via kommandoraden i passivt eller tyst läge.

* Passiv installation via kommandoraden: Installationsprogrammet visar en förloppsindikator som anger att installationen pågår, men inga meddelanden eller felmeddelanden visas. När du har startat programmet kan du inte avbryta installationen.

```shell
msiexec /i "<absolute path>\Designer.msi" /passive SERIALNUMBER=****-****-****-****-****-****
```

* Tyst kommandoradsinstallation: Installationsprogrammet kör installationen utan att visa något användargränssnitt. Inga uppmaningar, meddelanden eller dialogrutor visas. När du har startat programmet kan du inte avbryta installationen.

```shell
msiexec /i "<absolute path>\Designer.msi" /quiet SERIALNUMBER=****-****-****-****-****-****
```


