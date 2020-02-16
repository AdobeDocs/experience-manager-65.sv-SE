---
title: Söker efter processinstanser
seo-title: Söker efter processinstanser
description: Använd sidan Processsökning för att ange sökvillkor för att hitta en processinstans.
seo-description: Använd sidan Processsökning för att ange sökvillkor för att hitta en processinstans.
uuid: 4a9c5b05-add5-4278-9c6f-d1928b6860d2
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms_workflow
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 88b634bb-8f6c-4830-ad01-821668609615
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Söker efter processinstanser{#searching-for-process-instances}

Använd sidan Processsökning för att ange sökvillkor för att hitta en processinstans. Du kommer åt sidan Processsökning från sidan för formulärarbetsflöde eller genom att klicka på Sök på sidan Processinstans.

Du kan ange grundläggande villkor för att utföra en allmän sökning, särskilda attribut för att utföra en detaljerad sökning eller en kombination av grundläggande villkor och specifika attribut för att utföra en kombinerad sökning.

## Utför en allmän sökning {#perform-a-general-search}

En allmän sökning efter en process är lämpligast om du känner till process-ID:t för processinstansen, om du söker efter en grupp med relaterade processinstanser eller om bara ett fåtal processinstanser körs.

Ange grundläggande villkor för att utföra en allmän sökning. Om du anger flera villkor utförs sökningen med ett underförstått AND-villkor.

1. I administrationskonsolen klickar du på Tjänster > Formulärarbetsflöde > Processsökning.
1. Ange följande villkor under Allmän sökning på sidan Processsökning:

   * **** Process-ID: Det positiva heltal som identifierar varje unik processinstans.
   * **** Processstatus: Välj en status i listan.
   * **** Program: Välj ett program i listan. Endast distribuerade program visas.
   * **** Processnamn - version: Välj ett processnamn på menyn. Endast distribuerade processer visas.

1. Klicka på Sök. Sidan Processinstans visas med en lista över de hittade instanserna.

## Utför en detaljerad sökning efter en process {#perform-a-detailed-search-for-a-process}

Du kan ange specifika attribut för att göra en detaljerad sökning. En detaljerad sökning är lämpligast om du har många processinstanser igång och du måste begränsa antalet möjliga sökningar efter vissa villkor.

1. I administrationskonsolen klickar du på Tjänster > Formulärarbetsflöde > Processsökning.
1. Ange din första villkorsuppsättning under Detaljerad sökning på sidan Processsökning:

   * Välj ett attribut i attributlistan.
   * Välj en operator i filterlistan.
   * I rutan Värde anger du ett värde som passar det attribut du har valt.

1. Om du vill lägga till ytterligare en rad väljer du Fler filter. En annan uppsättning med attribut-, filter- och värdeslistor visas, liksom en villkorslista.
1. Välj OCH eller ELLER under Villkor. Upprepa steg 1-3 om det behövs för att begränsa sökningen ytterligare.
1. Om du vill lägga till eller ta bort rader klickar du på Fler filter eller Färre filter. Du kan ha mellan en och fyra rader.
1. Klicka på Sök. Sidan Processinstans visas med en lista över de hittade instanserna.

[Om processinstansstatus](/help/forms/using/admin-help/processes.md#about-process-instance-statuses)

## Utför en kombinerad sökning efter en process {#perform-a-combined-search-for-a-process}

Om du vill skapa en sökning baserad på både en allmän sökning och en detaljerad sökning, med en underförstådd OCH mellan områdena, anger du sökvillkoren i både området Allmän sökning och Detaljerad sökning på sidan Processsökning.

Om sökningen är för smal hittas inga förekomster.
