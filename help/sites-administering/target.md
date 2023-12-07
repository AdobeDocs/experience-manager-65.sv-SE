---
title: Integrera med Adobe Target
description: Lär dig integrera Adobe Experience Manager med Adobe Target.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
exl-id: 2b17d8cd-a43c-4d54-b990-a6f0cb1db22b
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '567'
ht-degree: 0%

---

# Integrera med Adobe Target{#integrating-with-adobe-target}

Som en del av Adobe Marketing Cloud [Adobe Target](https://www.adobe.com/ro/solutions/testing-targeting/testandtarget.html) gör att ni kan öka innehållets relevans genom målinriktning och mätning över alla kanaler. Adobe Target används av marknadsförare för att utforma och genomföra onlinetester, skapa direktsända målgruppssegment (baserat på beteende) och automatisera målgruppsanpassningen av innehåll och onlineupplevelser. AEM har antagit målarbetsflödet som används i Adobe Target Standard. Om du använder Target kommer du att känna till målredigeringsmiljön i AEM.

Integrera era AEM med Adobe Target för att personalisera innehåll på era sidor:

* Implementera målinriktning av innehåll.
* Använd målgrupper för att skapa personaliserade upplevelser.
* Skicka kontextdata till Target när besökarna interagerar med era sidor.
* Spåra konverteringsgrader.

Utför följande uppgifter för att integrera med Target:

1. [Utför nödvändiga uppgifter](/help/sites-administering/target-requirements.md): Registrera dig hos Adobe Target och konfigurera vissa aspekter av AEM författarinstans. Ditt Adobe Target-konto måste ha minst **godkännarbehörighet **level. Dessutom måste du skydda aktivitetsinställningarna på publiceringsnoden så att den inte är tillgänglig för användarna.

1. Antingen:

   1. [Anmäl dig till Adobe Target](/help/sites-administering/opt-in.md): Guiden för deltagande tar emot din målkontoinformation och skapar en molnkonfiguration för Adobe Target och ett Target Framework. Guiden kopplar även dina webbplatser till Target Framework. Om guiden inte kan ansluta till målet kan du läsa [anslutningsfelsökning](/help/sites-administering/target-configuring.md#troubleshooting-target-connection-problems) -avsnitt. Då kan du [Ändra standardkonfigurationerna för molnet](/help/sites-administering/target-configuring.md#modifying-the-opt-in-wizard-configurations): Ändra vid behov molnkonfigurationen och ramverket som avanmälningsguiden skapade. Ändra till exempel ramverket för att skicka ytterligare kontextdata till Target. Om du vill använda Adobe Analytics som rapportkälla för Adobe Target måste du ändra molnkonfigurationen så att den pekar på A4T-konfigurationen.
   1. [Integrera manuellt med Adobe Target](/help/sites-administering/target-configuring.md#manually-integrating-with-adobe-target).

1. [Konfigurera aktiviteter](/help/sites-authoring/activitylib.md): Associera dina aktiviteter med målmolnkonfigurationen.

>[!NOTE]
>
>Se även [Integrera AEM med Adobe Target och Adobe Analytics med DTM](https://helpx.adobe.com/experience-manager/using/integrate-digital-marketing-solutions.html).

>[!NOTE]
>
>Om du använder Target med en anpassad proxykonfiguration måste du konfigurera både HTTP-klientproxykonfigurationer eftersom vissa funktioner i AEM använder 3.x-API:erna och andra 4.x-API:er:
>
>* 3.x har konfigurerats med [http://localhost:4502/system/console/configMgr/com.day.commons.httpclient](http://localhost:4502/system/console/configMgr/com.day.commons.httpclient)
>* 4.x har konfigurerats med [http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator](http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator)
>

>[!CAUTION]
>
>Skydda noden för aktivitetsinställningar **cq:ActivitySettings** på publiceringsinstansen så att den inte är tillgänglig för vanliga användare. Noden för aktivitetsinställningar ska bara vara tillgänglig för tjänsten som hanterar aktivitetssynkroniseringen till Adobe Target.
>
>Se [Krav för integrering med Adobe Target](/help/sites-administering/target-requirements.md#securing-the-activity-settings-node) för detaljerad information.

När integreringen är klar kan du [skapa riktat innehåll](/help/sites-authoring/content-targeting-touch.md) som skickar besöksdata till Adobe Target. Observera att sidkomponenter kräver specifik kod för att aktivera målinriktning av innehåll. (Se [Utveckla för riktat innehåll](/help/sites-developing/target.md).)

>[!NOTE]
>
>När du riktar in dig på en komponent i AEM författare gör komponenten ett antal serveranrop till Adobe Target för att registrera kampanjen, konfigurera erbjudanden och hämta Adobe Target-segment (om de är konfigurerade). Inga anrop på serversidan görs från AEM publicera till Adobe Target.

## Källor för bakgrundsinformation {#background-information-sources}

Att integrera AEM med Adobe Target kräver kunskap om Adobe Target, AEM och AEM. Du bör känna till följande information:

* Adobe Target (se [Adobe Target-dokumentation](https://experienceleague.adobe.com/docs/target/using/target-home.html)).
* Konsolen AEM aktiviteter (se [Hantera aktiviteter](/help/sites-authoring/activitylib.md)).
* AEM målgrupper (se [Hantera målgrupper](/help/sites-authoring/managing-audiences.md)).

>[!NOTE]
>
>När du arbetar med Adobe Target är det högsta antalet artefakter som tillåts i en kampanj:
>
>* 50 platser
>* 2 000 upplevelser
>* 50-tal
>* 50 rapporteringssegment
>
