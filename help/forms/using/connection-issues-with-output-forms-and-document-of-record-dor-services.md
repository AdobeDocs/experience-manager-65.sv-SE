---
title: Anslutningsproblem med Output, Forms och (Document of Record) DoR-tjänster
description: Åtgärda anslutningsfel i AEM Forms efter SP19. Stoppa, installera Microsoft Visual C++, starta om servern för en sömlös lösning. Felsök Output, Forms, DoR-tjänster.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
role: Admin
source-git-commit: cf5da092fabbc7834108dc54d65eb97e160984ce
workflow-type: tm+mt
source-wordcount: '134'
ht-degree: 0%

---


# Det går inte att använda utdatatjänsten, Forms-tjänsten eller DoR-tjänsten (Document of Record) {#unable-to-use-output-service-forms-service-or-document-of-record-service}

## Problem

När du har installerat AEM Forms 6.5 Service Pack 19 kan ett försök att använda tjänsten Output, Forms eller DoR-tjänsten (Document of Record) resultera i en `Connection to failed service` fel.

## Lösning

Så här löser du problemet:

1. Stoppa din AEM 6.5 Forms-instans.
1. Hämta och installera [64-bitarsversion av Microsoft Visual C++ Redistributable-paket för Visual Studio 2015, 2017, 2019 och 2022](https://learn.microsoft.com/en-us/cpp/windows/latest-supported-vc-redist?view=msvc-170#visual-studio-2015-2017-2019-and-2022) på den dator där AEM 6.5 Forms är installerat.
1. Starta om AEM Forms-servern.


>[!NOTE]
>
>
> Kontrollera att du har installerat Redistributable även om en tidigare version är installerad.
