---
title: Konfigurera analyser och rapporter
description: Lär dig hur du konfigurerar Adobe Analytics för att upptäcka interaktionsmönster och problem som användare ställs inför när de använder adaptiva formulär, adaptiva dokument och HTML5-formulär.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: integrations
docset: aem65
exl-id: 72f0f8e3-e70b-4f78-aa0e-b31768b536f7
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '1531'
ht-degree: 0%

---

# Analyser med hjälp av Cloud Service Framework {#analyticsusingcloudframework}

AEM Forms kan integreras med Analytics så att ni kan hämta in och spåra prestandamått för era publicerade formulär och dokument. Syftet med att analysera dessa värden är att fatta välgrundade beslut baserat på uppgifter om de ändringar som krävs för att göra formulär eller dokument mer användbara.

>[!NOTE]
>
>Analysfunktionen i AEM Forms ingår i AEM Forms tilläggspaket. Mer information om hur du installerar tilläggspaketet finns i [Installera och konfigurera AEM Forms](../../forms/using/installing-configuring-aem-forms-osgi.md).
>
>Utöver tilläggspaketet behöver du ett Adobe Analytics-konto och administratörsbehörighet för AEM. Information om lösningen finns i [Adobe Analytics](https://www.adobe.com/solutions/digital-analytics.html).

Du kan också utföra analyser med Adobe Launch. Mer information om hur du integrerar AEM Forms med Adobe Launch finns i [Analyser med Adobe Launch](/help/forms/using/integrate-aem-forms-with-adobe-analytics.md).

## Ökning {#overview}

Du kan använda Adobe Analytics för att upptäcka interaktionsmönster och problem som användare ställs inför när de använder adaptiva formulär, HTML5-formulär och interaktiv kommunikation. Med Adobe kan man spåra och lagra information om följande parametrar:

* **Genomsnittlig fyllningstid**: Genomsnittlig tid för att fylla i formuläret.
* **Återgivningar**: Antal gånger ett formulär öppnas.
* **Utkast**: Antal gånger ett formulär sparas i utkastläget.
* **Inlämningar**: Antal gånger ett formulär skickas.
* **Avbryt**: Antal gånger som användarna lämnar utan att fylla i formuläret.

Du kan anpassa Adobe Analytics för att lägga till/ta bort fler parametrar. Tillsammans med ovanstående information innehåller rapporten följande information om samtliga paneler i HTML 5 och anpassningsbar form:

* **Tid**: Tid som har ägnats åt panelen och panelens fält.
* **Fel**: Antal fel som påträffats på panelen och i panelens fält.
* **Hjälp**: Antal gånger en användare öppnar hjälpen för en panel och fälten på panelen.

## Skapar rapportsvit {#creating-report-suite}

Analysdata lagras i kundspecifika databaser som kallas rapportsviter. Om du vill skapa en rapportserie och använda Adobe Analytics måste du ha ett giltigt Adobe Marketing Cloud-konto. Kontrollera att du har ett giltigt Adobe Marketing Cloud-konto innan du utför följande steg.

Utför följande steg för att skapa en rapportserie.

1. Logga in på [https://sc.omniture.com/login/](https://sc.omniture.com/login/)
1. I Marketing Cloud väljer du **Administratör** > **Admin Console** > **Rapportsviter**.
1. Välj **Skapa nytt** > **Report Suite** i Report Suite Manager.

   ![Skapa ny rapportsvit](assets/newreportsuite_new.png)

   Skapa ny rapportsvit

1. Kontrollera att den första listrutan är inställd på **Skapa från en mall** och sedan **Handel**.
1. Leta reda på **Report Suite-ID** och lägg till ett nytt Report Suite-ID. Till exempel JEsquire. Ett rapportsvit-ID visas under fältet för rapportsvitens-ID. Det innehåller ett automatiskt prefix, som ofta är företagsnamnet.
1. Lägg till ny **Platsrubrik**. JJEsquire Getting Started Suite. Den här titeln används i analysgränssnittet. Använd rapportsvitens ID i koden.
1. Välj en **Tidszon** i listrutan. Alla data som ingår i den här rapportsviten registreras baserat på den definierade tidszonen.
1. Lämna **Bas-URL** och **Standardsida** fält är tomma. Dessa två värden används bara från Adobe Marketing Cloud gränssnitt för att länka till din webbplats.
1. Lämna **Go Live Date** till idag. Startdatumet avgör vilken dag rapportsviten aktiveras.
1. I **Beräknade sidvisningar per dag** fält, typ 100. Använd det här fältet för att uppskatta antalet sidvisningar som du förväntar dig för din webbplats per dag. Denna uppskattning gör att Adobe kan installera lämplig mängd maskinvara för att bearbeta de data som ska samlas in.
1. Välj en **Basvaluta** i listrutan. Alla valutadata som ingår i den här rapportsviten konverteras och lagras i det här valutaformatet.
1. Klicka **Skapa rapport** Suite. Du bör se uppdateringen av sidan med ett meddelande om att rapportsviten har skapats.
1. Välj den nya rapportsviten. Navigera till **Redigera inställningar** > **Allmänt** > **Allmänna kontoinställningar**.

   ![Allmänna kontoinställningar](assets/geographic_settings.png)

   Allmänna kontoinställningar

1. På skärmen för allmänna kontoinställningar aktiverar du **Geografisk rapportering** och klicka **Spara.**
1. Navigera till **Redigera inställningar** > **Trafik** > **Trafikvariabler**.
1. Konfigurera och aktivera följande trafikvariabler i rapportsviten.

   * **formName**: Identifierare för ett adaptivt formulär.
   * **formInstance**: Identifierare för en instans av ett adaptivt formulär. Aktivera sökvägsrapporter för variabeln.
   * **fieldName**: Identifierare för ett adaptivt formulärfält. Aktivera sökvägsrapporter för variabeln.
   * **panelName**: Identifierare för en anpassad formulärpanel. Aktivera sökvägsrapporter för variabeln.
   * **formTitle**: Formulärets namn.
   * **fieldTitle**: Formulärfältets namn.
   * **panelTitle**: Formulärpanelens namn.
   * **analyticsVersion**: Version av formuläranalys.

1. Navigera till **Redigera inställningar** > **Konvertering** > **Success Events**. Definiera och aktivera följande lyckade händelser:

   | Händelsen Slutfört | Typ |
   |---|---|
   | överge | Räknare |
   | återge | Räknare |
   | panelBesök | Räknare |
   | fieldVisit | Räknare |
   | spara | Räknare |
   | fel | Räknare |
   | help | Räknare |
   | skicka | Räknare |
   | timeSpent | Numeriskt |

   >[!NOTE]
   >
   >Ett händelsenummer och ett prop-nummer som används för att konfigurera AEM Forms-analys måste skilja sig från det händelsenummer och det prop-nummer som används i [AEM](/help/sites-administering/adobeanalytics.md) konfiguration.

1. Logga ut från Adobe Marketing Cloud-kontot.

## Skapar konfiguration av Cloud Service {#creating-cloud-service-configuration}

Konfigurationen av Cloud Servicen är information om ditt Adobe Analytics-konto. Med konfigurationen kan Adobe Experience Manager (AEM) ansluta till Adobe Analytics. Skapa en separat konfiguration för varje Analytics-konto som du använder.

1. Logga in på AEM författarinstans som administratör.
1. Klicka på i det övre vänstra hörnet **Adobe Experience Manager** > **verktyg** ![hamikon](/help/forms/using/assets/tools.png) > **Cloud Service** > **Äldre Cloud Service**.
1. Sök **Adobe Analytics** -ikon. Klicka **Visa konfigurationer** och sedan fortsätta klicka **[+]** för att lägga till ny konfiguration.

   Om du är förstagångsanvändare klickar du på **Konfigurera nu**.

1. Lägg till en titel i den nya konfigurationen (det är valfritt att fylla i fältet Namn). Till exempel Min analyskonfiguration. Klicka **Skapa**.

1. När panelen Redigera öppnas på konfigurationssidan fyller du i fälten:

   * **Företag**: Ditt företags namn visas på Adobe Analytics.
   * **Användarnamn**: Namnet som används för att logga in på Adobe Analytics.
   * **Lösenord**: Adobe Analytics-lösenordet för ovanstående konto.
   * **Datacenter**: Datacentret för ditt Adobe Analytics-konto.

1. Klicka **Anslut till Analytics**. En dialogruta visas med ett meddelande om att anslutningen lyckades. Klicka **OK**.

## Skapar Cloud Service Framework {#creating-cloud-service-framework}

Ett Adobe Analytics-ramverk är en uppsättning mappningar mellan Adobe Analytics-variabler och AEM. Använd ett ramverk för att konfigurera hur formulären fyller i data i Adobe Analytics-rapporter. Ramverk är kopplade till en Adobe Analytics-konfiguration. Du kan skapa flera ramverk för varje konfiguration.

1. På AEM molntjänstkonsol klickar du på **Visa konfigurationer**, under Adobe Analytics.
1. Klicka på **[+]** länk bredvid din Analytics-konfiguration.

   ![Adobe Analytics-konfiguration](assets/adobe-analytics-cloud-services.png)

   Adobe Analytics-konfiguration

1. Skriv a **Titel** och **Namn** för ramverket väljer du **Adobe Analytics** Framework och klicka på **Skapa**. Ramverket öppnas för redigering.
1. Klicka på i delen Rapportsviter på sidopanelen **Lägg till objekt** använder du sedan listrutan för att välja det Report Suite-ID (till exempel JEsquire) som ramverket ska interagera med.
1. Bredvid Report Suite-ID markerar du de serverinstanser som du vill skicka information till Report Suite.

   ![information_to_send_to_report_suite](assets/information_to_send_to_report_suite.png)

1. Dra en **Form Analytics-komponent** från **övriga** från Sidekick till ramverket.
1. Om du vill mappa Analytics-variabler med variabler som är definierade i komponenten drar du en variabel från AEM Content Finder till ett fält i spårningskomponenten.

   ![Mappa AEM variabler med Adobe Analytics-variabler](assets/analytics_new.png)

1. Aktivera ramverket med **fliken page** i sidosparken, klicka **Aktivera ramverk**.

## Konfigurationstjänsten för AEM Forms Analytics konfigureras {#configuring-aem-forms-analytics-configuration-service}

1. Öppna konfigurationshanteraren AEM Web Console på `https://<server>:<port>;/system/console/configMgr`.
1. Leta rätt på och öppna AEM Forms Analytics-konfigurationen

   ![Konfigurationstjänst för AEM Forms Analytics](assets/analytics_configuration.png)

   Konfigurationstjänst för AEM Forms Analytics

1. Ange lämpliga värden för följande fält och klicka på **Spara**.

   * **SiteCatalyst Framework**: Välj ramverket/konfigurationen som du definierade i avsnittet Konfigurera ett ramverk för spårning.
   * **Fälttidsspårning - baslinje**: Ange hur länge (i sekunder) som fältbesöket ska spåras. Standardvärdet är 0. När värdet är större än 0 (noll) skickas två separata spårningshändelser till Adobe Analytics-servern. Den första händelsen instruerar analysservern att sluta spåra det avslutade fältet. Den andra händelsen skickas efter att den angivna längden har gått. Den andra händelsen instruerar analysservern att börja spåra det besökta fältet. Genom att använda två olika händelser kan du mäta tiden som läggs på ett fält på ett korrekt sätt. När värdet är 0 (noll) skickas en enda spårningshändelse till Adobe Analytics-servern.

   * **Synkroniseringscron för analysrapport**: Ange cron-uttryck för att hämta rapporter från Adobe Analytics. Standardvärdet är 0 0 2 ? &#42; &#42;.

   * **Tidsgräns för hämtning av rapport:** Ange hur länge (i sekunder) som servern ska svara på analysrapporten. Standardtiden är 120 sekunder.

   >[!NOTE]
   >
   >Det kan ta upp till 10 sekunder till att tidsgränsen för hämtning av rapporter överskrids, sedan det angivna antalet sekunder.

1. Upprepa steg 1-3 på publiceringsinstansen för att konfigurera analyser.

Nu kan ni aktivera analyser för formulär och generera en analysrapport.

## Aktivera analys för ett formulär eller dokument {#enabling-analytics-for-a-form-or-document}

1. Logga in på AEM portal på `https://[hostname]:'port'`.
1. Klicka **Forms > Forms &amp; Documents**, markera ett formulär eller dokument och klicka på **Aktivera analys**. Analysen är aktiverad.

   ![Aktivera analys för ett formulär eller dokument](assets/enable-analytics-1.png)

   Aktivera analys för ett formulär

   **S.** Knappen Aktivera analys **B.** Markerat formulär

   Detaljerad information om hur du visar analysrapporter för formulär finns i [Visa och förstå AEM Forms analysrapporter](../../forms/using/view-understand-aem-forms-analytics-reports.md).
