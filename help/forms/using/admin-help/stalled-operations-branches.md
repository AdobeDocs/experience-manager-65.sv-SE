---
title: Arbeta med fasta operationer och grenar
seo-title: Arbeta med fasta operationer och grenar
description: Sidan Installerade åtgärder och sidan Installerade grenar visar de processer som har avstannat.
seo-description: Sidan Installerade åtgärder och sidan Installerade grenar visar de processer som har avstannat.
uuid: 5f6202b0-79c2-4c3c-847a-236c0366e60b
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms_workflow
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 8c2567f3-7220-436a-b9f2-2824a98c1ccc
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Arbeta med fasta operationer och grenar {#working-with-stalled-operations-and-branches}

Sidan Installerade åtgärder och sidan Installerade grenar visar de processer som har avstannat. En process kan hänga sig när ett fel inträffar under eller efter en åtgärd eller på grund av en avsiktlig avbrottsåtgärd i processen:

* Åtgärderna kan stanna på grund av ett oförutsett fel. En Stall Branch-åtgärd i en process stoppar avsiktligt en process från att köras ytterligare och kräver att administratören gör något.
* Förgreningar kan hänga mellan åtgärder under en regelutvärdering.

När en process avbryts körs inga fler åtgärder förrän problemet har åtgärdats och åtgärden eller grenen har startats om.

För varje objekt som inte är installerade visas följande information i listan:

**** Åtgärdsnamn eller grennamn: Namnet på åtgärden eller grenen.

**** Status: STALLERAD för fasta objekt.

**** Fel: En kort beskrivning av problemet.

**** Process-ID: Det positiva heltal som formulärarbetsflödet tilldelar när processen initieras (det vill säga när en användare eller ett automatiskt steg initierar en process). Du kan använda den här identifieraren för att spåra processinstansen genom dess livscykel.

**** Processnamn - version: Namnet på processen som tilldelats i Workbench.

**** Stängt den: Datum och tid då åtgärden eller grenen stoppades.

Du kan göra följande på sidan Installerade åtgärder eller Stängda grenar:

* Välj ett fel om du vill visa information om det. När du väljer ett fel visas sidan Felinformation.
* Avsluta eller försök med fasta åtgärder eller försök med fasta grenar igen.

## Avsluta eller göra om fasta operationer eller förgreningar {#terminating-or-retrying-stalled-operations-or-branches}

På sidan Installerade åtgärder kan du avsluta de processinstanser som visas.

När du avslutar en processinstans avbryts körningen och inga fler åtgärder utförs. Du avslutar vanligtvis bara en process om den blockeras eller inte kan användas på grund av ett fel och inte kan korrigeras och startas om.

Du kan försöka utföra åtgärden eller grenen igen på sidan Installerade åtgärder eller på sidan Staplade grenar.

När du försöker utföra en åtgärd på nytt skickas en begäran om att starta om åtgärden. Om felet som orsakade att processen stals har åtgärdats och begäran om nytt försök har slutförts, börjar processen köras igen från den punkt där den hade stannat och dess status ändras till RUNNING. Om åtgärden inte kan startas om, förblir den STALLED och du kan behöva avsluta den.

### Avsluta en fast åtgärd {#terminate-a-stalled-operation}

1. I administrationskonsolen klickar du på Tjänster > Formulärarbetsflöde > Installerade åtgärdsfel.
1. På sidan Installerade åtgärder markerar du det objekt som du vill avsluta och klickar på Avsluta.

### Försök igen med en fast åtgärd eller en gren {#retry-a-stalled-operation-or-branch}

1. I administrationskonsolen klickar du på Tjänster > arbetsflöde för formulär och sedan på Installerade operationsfel eller Installerade grenfel.
1. Markera det objekt du vill försöka igen på sidan Installerade åtgärder eller Installerade grenar och klicka sedan på Försök igen.

## Visa felinformation om fasta åtgärder eller grenar {#viewing-error-details-about-stalled-operations-or-branches}

Om du väljer ett fel i listan över installerade objekt på sidan Installerade åtgärder eller Installerade grenar visas sidan Felinformation med information om felet som kan hjälpa dig att felsöka problemet.

Rutan längst ned på sidan innehåller felinformationen.

Du kan också avsluta eller försöka utföra fasta åtgärder igen, och göra om fasta grenar, från sidan Felinformation.

## Processen stoppas inte när eskaleringsanvändaren inte finns {#process-does-not-stall-when-escalation-user-does-not-exist}

Fel uppstår när åtgärden Tilldela uppgift i tjänsten AEM-formuläranvändare har konfigurerats att eskalera uppgiften till en annan användare efter en viss tidsperiod, och eskaleringsanvändaren tas bort efter att åtgärden Tilldela uppgift körs men innan eskaleringen inträffar.

När den här situationen inträffar ändras inte processens och aktivitetens tillstånd vid den konfigurerade eskaleringstiden, och eskaleringen sker inte, men processen avbryts inte. Följande meddelande visas i serverloggen:

&quot;Huvudkontot som har angetts för eskalering är inte giltigt för taskID: Angivet *nummer*, angiven kö: *tal*.&quot;

Om eskaleringsanvändaren tas bort innan aktiviteten genereras (innan Tilldela uppgift-åtgärden körs) avbryts processen eller InvalidPrincipal-undantagshändelsen.

Om du vill förhindra det här problemet ska du söka efter uppgifter som tillhör användaren och hantera dem i enlighet med detta när du tar bort en användare. (Se [Arbeta med uppgifter](/help/forms/using/admin-help/tasks.md#working-with-tasks).)
