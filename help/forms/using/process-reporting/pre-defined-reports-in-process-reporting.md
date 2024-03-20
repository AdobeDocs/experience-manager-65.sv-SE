---
title: Fördefinierade rapporter i processrapportering
description: Fråga efter AEM Forms om JEE-processdata om du vill skapa rapporter om långvariga processer, processens varaktighet och arbetsflödets volym
content-type: reference
topic-tags: process-reporting
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
exl-id: 34e55676-6332-4616-aecc-bcc8cc1e8a29
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '691'
ht-degree: 0%

---

# Fördefinierade rapporter i processrapportering {#pre-defined-reports-in-process-reporting}

## Fördefinierade rapporter i processrapportering {#pre-defined-reports-in-process-reporting-1}

AEM Forms Process Reporting levereras med följande *körklar* rapporter:

* **[Långa processer](#long-running-processes)**: En rapport över alla AEM Forms-processer som tog mer än en angiven tid att slutföra
* **[Process Duration Chart](#process-duration-report)**: En rapport över en angiven AEM Forms-process utifrån varaktighet
* **[Arbetsflödesvolym](#workflow-volume-report)**: En rapport över pågående och slutförda instanser av angiven process per datum

## Långa processer {#long-running-processes}

Rapporten Långa processer visar de AEM Forms-processer som tagit mer än en angiven tid att slutföra.

### Så här kör du en rapport över en process som körs länge {#to-execute-a-long-running-process-report}

1. Om du vill visa en lista över fördefinierade rapporter i processrapportering går du till **Processrapportering** trädvyn, klicka på **Rapporter** nod.
1. Klicka på **Långa processer** rapportnod.

   ![long_running_node](assets/long_running_node.png)

   När du väljer en rapport visas **Rapportparametrar** Panelen visas till höger om trädvyn.

   ![lång körningsprocess, rapportparameterpanel](assets/report_parameters_panel.png)

   Parametrar:

   * **Varaktighet** (*obligatoriskt*): Ange varaktighet och tidsenhet. Visa alla AEM Forms-processer som har körts under mer än den angivna varaktigheten.
   * **Startades efter** (*valfri*): Välj ett datum. Filtrera rapporten så att processinstanser som har startats efter det angivna datumet visas.
   * **Startades före** (*valfri*): Välj ett datum. Filtrera rapporten så att processinstanser som startats före det angivna datumet visas.

1. Klicka **Gå** för att köra rapporten.

   Rapporten visas i **Rapport** till höger om **Processrapportering** -fönstret.

   ![long_running_processes](assets/long_running_processes.png)

   Använd alternativen i det övre högra hörnet av **Rapport** för att utföra följande åtgärder på rapporten.

   * **Uppdatera**: Uppdaterar rapporten med de senaste data som finns i lagringen
   * **Ändra förklaringsfärg**: Markera och ändra färgen på rapportförklaringen
   * **Exportera till CSV**: Exportera och hämta data från rapporten till en kommaavgränsad fil

## Processvaraktighet - rapport  {#process-duration-report}

Processvaraktighetsrapporten visar antalet instanser av en Forms-process i antal dagar som varje instans har körts.

### Så här kör du en rapport för processvaraktighet {#to-execute-a-process-duration-report}

1. Om du vill visa de fördefinierade rapporterna i Process Reporting går du till **Processrapportering** trädvyn, klicka på **Rapporter** nod.
1. Klicka på **Processernas varaktighet** rapportnod.

   ![process_duration_node](assets/process_duration_node.png)

   När du väljer en rapport visas **Rapportparametrar** Panelen visas till höger om trädvyn.

   ![lång körningsprocess, rapportparameterpanel](assets/process_duration_params.png)

   Parametrar:

   * **Välj process** (*obligatoriskt*): Välj en AEM Forms-process.

1. Klicka **Gå** för att köra rapporten.

   Rapporten visas i **Rapport** till höger om fönstret Processrapportering.

   ![process_duration_report](assets/process_duration_report.png)

   Använd alternativen i det övre högra hörnet av **Rapport** för att utföra följande åtgärder på rapporten.

   * **Uppdatera**: Uppdaterar rapporten med de senaste data som finns i lagringen
   * **Ändra förklaringsfärg**: Markera och ändra färgen på rapportförklaringen
   * **Exportera till CSV**: Exportera och hämta data från rapporten till en kommaavgränsad fil

## Rapport över arbetsflödesvolym {#workflow-volume-report}

Volymrapporten Arbetsflöde visar antalet pågående och slutförda instanser av en AEM Forms-process per kalenderdag.

### Så här kör du en arbetsflödesvolymrapport {#to-execute-a-workflow-volume-report}

1. Om du vill visa de fördefinierade rapporterna i Process Reporting går du till **Processrapportering** trädvyn, klicka på **Rapporter** nod.
1. Klicka på **Arbetsflödesvolym** rapportnod.

   ![workflow_volume_node](assets/workflow_volume_node.png)

   När du väljer en rapport visas **Rapportparametrar** Panelen visas till höger om trädvyn.

   ![lång körningsprocess, rapportparameterpanel](assets/workflow_volume_params.png)

   Parametrar:

   * **Välj process** (*obligatoriskt*): Välj en AEM Forms-process.

   * **Startades efter** (*valfri*): Välj ett datum. Filtrerar rapporten så att processinstanser som startats efter det angivna datumet visas.

   * **Startades före** (*valfri*): Välj ett datum. Filtrerar rapporten så att processinstanser som påbörjats före det angivna datumet visas.

1. Klicka **Gå** för att köra rapporten.

   Rapporten visas i **Rapport** till höger om **Processrapportering** -fönstret.

   ![workflow_volume_report](assets/workflow_volume_report.png)

   Använd alternativen i det övre högra hörnet av **Rapport** för att utföra följande åtgärder på rapporten.

   * **Uppdatera**: Uppdaterar rapporten med de senaste data som finns i lagringen
   * **Ändra förklaringsfärg**: Markera och ändra färgen på rapportförklaringen
   * **Exportera till CSV**: Exportera och hämta data från rapporten till en kommaavgränsad fil
