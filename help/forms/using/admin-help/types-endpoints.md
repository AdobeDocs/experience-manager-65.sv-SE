---
title: Typer av slutpunkter
seo-title: Typer av slutpunkter
description: Lär dig mer om de olika typerna av slutpunkter.
seo-description: Lär dig mer om de olika typerna av slutpunkter.
uuid: c899245c-14cc-4035-9440-95a5b6c1e47f
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_endpoints
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 8fe572e0-8a53-4129-940f-3fdb990073fe
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '448'
ht-degree: 0%

---


# Typer av slutpunkter {#types-of-endpoints}

Innan en tjänst kan användas måste du konfigurera och aktivera en slutpunkt. En slutpunkt anger hur en tjänst ska anropas.

>[!NOTE]
>
>I Workbench kallas slutpunkter för startpunkter.

Följande typer av slutpunkter kan läggas till i tjänster. Alla tjänster har inte stöd för alla slutpunkter:

**E-post:** Gör det möjligt för en användare att anropa en tjänst genom att skicka ett e-postmeddelande med en eller flera bifogade filer till ett angivet e-postkonto. Innan du konfigurerar en e-postslutpunkt måste du konfigurera de e-postkonton som krävs. (Se Konfigurera e-postslutpunkter.)

**Bevakad mapp:** Gör det möjligt för en användare att anropa en tjänst genom att placera en fil i en mapp som skannas enligt ett angivet intervall. (Se Konfigurera bevakade mappslutpunkter.)

**TaskManager:** Gör det möjligt för en arbetsyteanvändare att anropa tjänsten.

**Remoting:** Gör att ett program som skapats med Flex kan anropa tjänsten med AEM (borttaget för AEM formulär) Remoting. En fjärrslutpunkt skapas automatiskt för varje aktiverad tjänst. Ett Flex-mål som har samma namn som slutpunkten skapas, och Flex-klienter kan skapa fjärrobjekt som pekar på det här målet för att anropa åtgärder på den aktuella tjänsten.

**SOAP:** Gör att ett klientprogram som utvecklats med API:er för AEM formulär kan anropa tjänsten i SOAP-läge. En SOAP-slutpunkt skapas automatiskt för varje aktiverad tjänst.

**Obs**!  *Dokumentskydd kan tas bort från dokumentsäkerhetsdokument när SOAP-slutpunkten används när dokumenten visas i Adobe Acrobat eller Adobe Reader. Mer information om hur du inaktiverar SOAP-slutpunkter i dina LCRM-dokument finns i [Inaktivera SOAP-slutpunkter för dokumentsäkerhetsdokument](/help/forms/using/admin-help/configuring-client-server-options.md#disable-soap-endpoints-for-document-security-documents)*

**EJB:** Aktiverar ett klientprogram som utvecklats med AEM API:er för formulärprogrammering för att anropa tjänsten i Enterprise JavaBeans-läge (EJB). En EJB-slutpunkt skapas automatiskt för varje aktiverad tjänst.

**WSDL:** Gör att ett klientprogram som utvecklats med API:er för AEM formulär kan anropa tjänsten med hjälp av WSDL (Web Service Definition Language). Sidan Core Configurations innehåller ett alternativ för att aktivera WSDL-generering för alla tjänster som är en del av AEM formulär. (Se Konfigurera allmänna AEM formulärinställningar.)

**REST:** Processer som skapas i Workbench kan konfigureras så att du kan anropa dem via REST-begäranden (Representational State Transfer). REST-begäranden skickas från HTML-sidor. Det innebär att du kan anropa en AEM formulärprocess direkt från en webbsida med hjälp av en REST-begäran.

Slutpunkterna Email, TaskManager, Watched Folder och Remoting visar bara en viss åtgärd för tjänsten. För att lägga till dessa slutpunkter krävs ett andra konfigurationssteg för att välja en metod för att anropa tjänsten, ange konfigurationsparametrar och ange in- och utdataparametermappningar.
