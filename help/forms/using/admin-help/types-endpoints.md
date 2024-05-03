---
title: Typer av slutpunkter
description: Lär dig mer om de olika typerna av slutpunkter. Olika typer av slutpunkter, som e-post, bevakad mapp och många fler, kan läggas till i tjänster.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_endpoints
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 380cab7f-e7f7-4cb7-bd20-ea530a349fac
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '455'
ht-degree: 0%

---

# Typer av slutpunkter {#types-of-endpoints}

Innan en tjänst kan användas måste du konfigurera och aktivera en slutpunkt. En slutpunkt anger hur en tjänst ska anropas.

>[!NOTE]
>
>I Workbench kallas slutpunkter för startpunkter.

Följande typer av slutpunkter kan läggas till i tjänster. Alla tjänster har inte stöd för alla slutpunkter:

**E-post:** Gör det möjligt för en användare att anropa en tjänst genom att skicka ett e-postmeddelande med en eller flera bifogade filer till ett angivet e-postkonto. Innan du konfigurerar en e-postslutpunkt måste du konfigurera de e-postkonton som krävs. (Se Konfigurera e-postslutpunkter.)

**Bevakad mapp:** Gör det möjligt för en användare att anropa en tjänst genom att placera en fil i en mapp som skannas med ett definierat intervall. (Se Konfigurera bevakade mappslutpunkter.)

**TaskManager:** Gör att en Workspace-användare kan anropa tjänsten.

**Remoting:** Gör att ett program som skapats med Flex kan anropa tjänsten med (borttaget för AEM formulär) AEM form Remoting. En fjärrslutpunkt skapas automatiskt för varje aktiverad tjänst. Ett Flex-mål som har samma namn som slutpunkten skapas, och Flex-klienter kan skapa fjärrobjekt som pekar på det här målet för att anropa åtgärder på den aktuella tjänsten.

**SOAP:** Gör att ett klientprogram som utvecklats med AEM API:er för formulärprogrammering kan anropa tjänsten i SOAP-läge. En SOAP-slutpunkt skapas automatiskt för varje aktiverad tjänst.

**anteckning**: *Dokumentskydd kan tas bort från dokumentsäkerhetsdokument när SOAP-slutpunkten används när dokumenten visas i Adobe Acrobat eller Adobe Reader. Mer information om hur du inaktiverar SOAP-punkter i dina LCRM-dokument finns i [Inaktivera SOAP-slutpunkter för dokumentsäkerhetsdokument](/help/forms/using/admin-help/configuring-client-server-options.md#disable-soap-endpoints-for-document-security-documents)*

**EJB:** Gör att ett klientprogram som utvecklats med AEM API:er för formulärprogrammering kan anropa tjänsten i Enterprise JavaBeans-läge (EJB). En EJB-slutpunkt skapas automatiskt för varje aktiverad tjänst.

**WSDL:** Gör att ett klientprogram som utvecklats med AEM API:er för formulärprogrammering kan anropa tjänsten med hjälp av WSDL (Web Service Definition Language). Sidan Core Configurations innehåller ett alternativ för att aktivera WSDL-generering för alla tjänster som ingår i AEM formulär. (Se Konfigurera allmänna AEM formulärinställningar.)

**REST:** Processer som skapas i Workbench kan konfigureras så att du kan anropa dem via REST-begäranden (Representational State Transfer). REST-begäranden skickas från HTML-sidor. Det innebär att du kan anropa en AEM formulärprocess direkt från en webbsida med hjälp av en REST-begäran.

Slutpunkterna Email, TaskManager, Watched Folder och Remoting visar bara en viss åtgärd för tjänsten. För att lägga till dessa slutpunkter krävs ett andra konfigurationssteg för att välja en metod för att anropa tjänsten, ange konfigurationsparametrar och ange in- och utdataparametermappningar.
