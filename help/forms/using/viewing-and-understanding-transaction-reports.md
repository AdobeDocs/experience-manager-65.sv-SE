---
title: Visa och förstå transaktionsrapporter
seo-title: Visa och förstå transaktionsrapporter
description: Använd transaktionsrapporter för att fatta ett välgrundat beslut om produktanvändningen och ombalansera investeringar i maskinvara och programvara.
seo-description: Använd transaktionsrapporter för att fatta ett välgrundat beslut om produktanvändningen och ombalansera investeringar i maskinvara och programvara.
uuid: 56d9f01d-4778-47c9-bbb2-6650a73a3f59
topic-tags: forms-manager
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: c04c488b-73f3-49ba-9e89-f97497965757
docset: aem65
exl-id: 3c7cbe1f-ac81-4df9-96b2-662cbc5f2075
source-git-commit: 75e1697c301dca3a649833a45caa1753fdc81514
workflow-type: tm+mt
source-wordcount: '883'
ht-degree: 0%

---

# Visa och förstå transaktionsrapporter{#viewing-and-understanding-transaction-reports}

Med transaktionsrapporter kan du samla in och spåra antalet skickade formulär, bearbetade dokument och återgivna dokument. Målet med att spåra dessa transaktioner är att fatta ett välgrundat beslut om produktanvändningen och att balansera investeringar i maskinvara och programvara. Mer information finns i [AEM Forms Transaction Reports Overview](../../forms/using/transaction-reports-overview.md).

## Ställa in transaktionsrapporter  {#setting-up-transaction-reports}

Funktionen för transaktionsrapporter är tillgänglig som en del av AEM paket. Information om hur du installerar tilläggspaketet på alla författare- och publiceringsinstanser finns i [Installera och konfigurera AEM formulär](/help/forms/using/installing-configuring-aem-forms-osgi.md). När du har AEM tilläggspaket för formulär installerat gör du följande:

* Aktivera omvänd replikering för alla publiceringsinstanser
* Aktivera transaktionsrapporter
* Ange rättigheter för att visa en transaktionsrapport
* (Valfritt) Konfigurera tömningsperiod och utkorgar för transaktioner [](/help/forms/using/installing-configuring-aem-forms-osgi.md)

>[!NOTE]
>
>* AEM Forms transaktionsrapporter stöder inte topologier som bara innehåller publiceringsinstanser.
>* Innan du använder transaktionsrapportering måste du se till att omvänd replikering är aktiverat för alla publiceringsinstanser.
>* Transaktionsdata återreplikeras från en publiceringsinstans till endast motsvarande författare eller bearbetningsinstans. Författaren eller bearbetningsinstansen kan inte replikera data till en annan instans.

>



### Aktivera omvänd replikering för alla publiceringsinstanser {#enable-reverse-replication-on-all-the-publish-instances}

Transaktionsrapporter använder omvänd replikering för att konsolidera antalet transaktioner från publiceringsinstanser till författarinstanser. Konfigurera omvänd replikering för alla publiceringsinstanser. Detaljerade anvisningar om hur du konfigurerar omvänd replikering finns i [replikering](/help/sites-deploying/replication.md).

### Aktivera transaktionsrapporter {#enable-transaction-reports}

Transaktionsrapporter är inaktiverade som standard. Du kan aktivera rapporter från AEM webbkonsol. Om du vill aktivera transaktionsrapporter i en AEM Forms-miljö utför du följande steg på alla författare- och publiceringsinstanser:

1. Logga in på en AEM som administratör. Gå till **Verktyg** > **Åtgärder** > **Webbkonsol**.
1. Leta reda på och öppna tjänsten **Forms Transaction Reporting**.
1. Markera kryssrutan Posttransaktioner. Klicka på **Spara**.

   Upprepa steg 1-3 för alla författare- och publiceringsinstanser.

### Ange rättigheter för att visa en transaktionsrapport {#provide-rights-to-view-a-transaction-report}

Det är bara medlemmar i gruppen som har administratörer som kan visa transaktionsrapporter. Om du vill att en användare ska kunna visa transaktionsrapporter måste användaren vara medlem i gruppen med dvd-administratörer. Instruktioner om hur du gör en användare till medlem i en AEM grupp finns i [Administrera användare, grupp och åtkomsträttigheter](/help/sites-administering/user-group-ac-admin.md).

### (Valfritt) Konfigurera tömningsperiod och utkorgar för transaktioner {#optional-configure-transaction-flush-period-and-outboxes}

Transaktioner cachelagras i minnet innan de lagras i databasen. Processen utförs för att säkerställa att det inte ofta förekommer några skrivningar i databasen. Som standard är cachelagringsperioden (perioden för tömning av transaktion) inställd på 60 sekunder. Du kan ändra standardperioden så att den passar din miljö. Utför följande steg för att ändra standardcachelagringsperioden:

1. Logga in för att skapa instanser som administratör. Gå till **Verktyg** > **Åtgärder** > **Webbkonsol**.
1. Leta reda på och öppna tjänsten **Forms Transaction Repository Storage Provider**.
1. Ange antalet sekunder i fältet **Tömningsperiod för transaktion**. Klicka på **Spara**.

Omvänd replikering kopierar transaktionsdata till författarinstansens standardutkorg. Du kan placera transaktionsdata i en anpassad utkorg. Gör så här för att ange en anpassad utkorg:

1. Logga in för att skapa instanser som administratör. Gå till **Verktyg** > **Åtgärder** > **Webbkonsol**.
1. Leta reda på och öppna tjänsten **Forms Transaction Repository Storage Provider**.
1. Ange namnet på den anpassade utkorgen i fältet **Utkorgar**. Klicka på **Spara**. En utkorg med det angivna namnet skapas för alla författarinstanser.

## Visa transaktionsrapporten {#viewing-the-transaction-report}

Du kan visa transaktionsrapporter om författare eller publiceringsinstanser. Transaktionsrapporten för författarinstansen ger en aggregerad summa av alla transaktioner som äger rum på den konfigurerade författaren och publiceringsinstansen. Transaktionsrapporten för publiceringsinstansen ger ett antal transaktioner som bara äger rum på den underliggande publiceringsinstansen. Följ de här stegen för att visa rapporten:

1. Logga in på AEM Forms-servern på `https://[hostname]:'port'`.
1. Navigera till **Verktyg** > **Forms****Visa transaktionsrapport**.

## Förstå rapporten {#understanding-the-report}

AEM Forms visar transaktionsrapporter sedan det konfigurerade datumet, vilket visas i en sammanfattningsrapport nedan:

![sample-transaction-report-author](assets/sample-transaction-report-author.png)

* Använd alternativen **Återställ datumet till idag** om du vill återställa transaktionsposter. När du återställer datumet till i dag går alla tidigare transaktionsposter förlorade. När du återställer datumet för en författarinstans påverkar ändringen inte transaktionsrapporter för publiceringsinstanser och omvänt.
* Använd **Visa transaktioner för enbart publiceringsinstanser** för att visa alla transaktioner som bara inträffade på den konfigurerade publiceringsinstansen eller publiceringsgruppen.
* Använd kategorierna: **Dokument som bearbetas**, **Dokument som återges** och **Forms har skickats** för att visa motsvarande transaktioner. Information om vilken typ av transaktioner som ingår i dessa kategorier finns i [API:er för fakturerbara transaktionsrapporter](../../forms/using/transaction-reports-billable-apis.md).

## Visa transaktionsrapporteringsloggar {#view-transaction-reporting-logs}

Transaktionsrapportering placerar all information som visas i rapporten och viss ytterligare information i loggarna. Informationen i loggarna är användbar för avancerade användare. I loggar delas transaktioner upp i flera detaljerade kategorier jämfört med tre konsoliderade kategorier som visas i rapporten. Loggarna är tillgängliga i filen `error.log` i katalogen `/crx-repository/logs/`. Loggarna är tillgängliga även om du inte aktiverar transaktionsrapporterna från AEM Web Console.

## Relaterade artiklar {#related-articles}

* [Översikt över transaktionsrapporter](../../forms/using/transaction-reports-overview.md)
* [Fakturerbara API:er för transaktionsrapporter](../../forms/using/transaction-reports-billable-apis.md)
* [Registrera en transaktion för anpassade implementeringar](/help/forms/using/record-transaction-custom-implementation.md)
