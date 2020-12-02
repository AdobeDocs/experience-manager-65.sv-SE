---
title: Komma igång med arbetsytan i AEM Forms
seo-title: Komma igång med arbetsytan i AEM Forms
description: Så här kommer du igång med att använda arbetsytan i LiveCycle AEM Forms för att hantera era automatiserade affärsprocesser.
seo-description: Så här kommer du igång med att använda arbetsytan i LiveCycle AEM Forms för att hantera era automatiserade affärsprocesser.
uuid: 35ca1a51-92c3-40d8-8de3-604be8704752
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: fa6e0246-6bd2-4ffb-b54c-15eda605f213
translation-type: tm+mt
source-git-commit: 49da3dbe590f70b98185a6bc330db6077dc864c0
workflow-type: tm+mt
source-wordcount: '1016'
ht-degree: 0%

---


# Komma igång med AEM Forms arbetsyta {#getting-started-with-aem-forms-workspace}

Du kan använda AEM Forms arbetsyta för att utföra följande uppgifter:

* Påbörja en affärsprocess
* Visa och agera på uppgifter som har tilldelats dig eller andra Att göra-listor som du har tillgång till
* Spåra uppgifter som ingår i de processer du påbörjade eller deltog i

## Navigera på arbetsytan i AEM Forms {#navigating-html-workspace}

Olika objekt i AEM Forms arbetsytans användargränssnitt visas beroende på vilken process och åtgärd du arbetar med. Du kan se flikarna Sammanfattning, Forms, Detaljer, Historik, Bilagor eller Anteckningar eller alla knappar som alltid beskrivs i den här hjälpen.

Du kan navigera i AEM Forms huvudgränssnitt på arbetsytan på något av följande sätt:

* Klicka på objekten i det övre navigeringsfältet för att komma åt alternativet Starta process, Att göra-lista, Inställningar, Spårning, Hjälp och Logga ut.
* Klicka på fliken Starta process, Att göra eller Spärra/knip för att komma åt de tre huvudarbetsytorna.
* På flikarna Starta process, Att göra och Spärra/knip klickar du på objekten i listan i den vänstra panelen för att få tillgång till favoriter, processkategorier, sökmallar, utkast eller tilldelade uppgifter. Använd rullningslisten för att se fler objekt i listan.
* Alla åtgärdsknappar - Godkänn, Avvisa, Framåt, Konsult, Lås och Dela - visas i både dokumentet och ägarskapet.
* Klicka på ikonen Alla alternativ i navigeringsfältet, längst ned på sidan, om du vill vidarebefordra uppgiften till en annan användare, dela uppgiften med en annan användare, om du vill fråga om uppgiften med en annan användare eller om du vill låsa uppgiften.
* På fliken Historik väljer du en uppgift som visar flikarna Bifogade filer och Uppdrag för den uppgiften.
* Använd tabbtangenten, piltangenterna och blankstegstangenten för att navigera på arbetsytan i AEM Forms utan att använda en mus.

## Använda AEM Forms arbetsyta med skärmläsare {#using-html-workspace-with-screen-readers}

AEM Forms arbetsyta är ett webbaserat HTML-program som är kompatibelt med skärmläsare. Du kan navigera i AEM Forms arbetsyta med hjälp av tangentbordet.

Om du vill använda AEM Forms-arbetsytan med en skärmläsare bör du tänka på följande:

* AEM Forms arbetsyta är ett standard-HTML-program som uppfyller alla vanliga skärmläsarverktyg. Du behöver inga specifika skript för att köra ett skärmläsarverktyg.
* All navigering på arbetsytan i AEM Forms sker via ankartaggar, som du enkelt kommer åt via flikar.
* Forms kan ta några sekunder att ladda. Skärmläsaren talar inte hörbart om att formuläret läses in och att du måste vänta.

## Navigera på AEM Forms-arbetsytan med ett tangentbord {#navigating-html-workspace-using-a-keyboard}

När du navigerar på AEM Forms arbetsyta med hjälp av ett tangentbord följer navigeringen HTML-tillgänglighetskonventionerna. I vissa situationer följer tabbordningen inte den vanliga vanliga ordningen. Följande tips hjälper dig att navigera i gränssnittet:

* Om du har problem med att tabba ut från verktygsfälten längst upp i webbläsaren trycker du på Ctrl+Tabb för att tabba in innehållet i webbläsarfönstret.
* Hjälp om arbetsytan i AEM Forms öppnas i ett separat webbläsarfönster. När du har visat hjälpen återgår fokus till webbläsarfönstret som innehåller AEM Forms-arbetsytan. Hjälpmenyn förblir fokuserad när fokus återgår.
* När du öppnar ett formulär för att starta en process eller slutföra en åtgärd behåller fokus det befintliga elementet och ändras inte till formuläret. Använd fliken för att flytta fokus till formuläret och bläddra igenom det. Tabbordningen i formuläret beror på formulärets typ och design.

   För PDF forms går markören till adressfältet i webbläsaren när du bläddrar fram till formulärets slut eller skickar formuläret. Du måste gå igenom menyerna en gång till (men inte hela formuläret) för att gå till formuläråtgärdsknapparna, till exempel Spara som utkast och Fullständigt. Om formuläret fortfarande är öppet kan du även tabba förbi knapparna och tillbaka till formuläret.

## Hantera inställningar {#managing-preferences}

Du kan ange olika inställningar för AEM Forms-arbetsytan i följande kategorier:

**Frånvarande:** Ange inställningar för hur uppgifter ska tilldelas andra personer när du inte är på kontoret. Se [Ange inställningar utanför kontoret](todo-lists.md#setting-out-of-office-preferences).

**köer:** Ange inställningar för att dela din Att göra-lista med andra användare eller för att begära åtkomst till en annan användares lista. Se [Arbeta med uppgifter från grupper och delade köer](todo-lists.md#working-with-tasks-from-group-and-shared-queues).

**gränssnittsinställningar:** Ange inställningar för hur du interagerar med AEM Forms arbetsyta. Se [Ange inställningar för användargränssnitt](#set-user-interface-preferences).

### Ange inställningar för användargränssnittet {#set-user-interface-preferences}

Ange gränssnittsinställningarna på fliken Inställningar > Användargränssnittsinställningar. Följande inställningar är tillgängliga.

* **Startplats:** Anger vilken sida som ska visas när du loggar in på arbetsytan i AEM Forms. De fyra tillgängliga alternativen är Starta process, Att göra, Spårning och Favoriter.
* **Utloggningsfråga:** Anger om du uppmanas att bekräfta att du vill logga ut när du klickar på Logga ut.
* **Datumformat:** Anger vilket datumvisningsformat som ska användas på AEM Forms arbetsyta.
* **Tidsformat**: Anger vilket tidsvisningsformat som används på AEM Forms arbetsyta.
* **Meddela aktivitetshändelser via e-post:** Anger om du får e-postmeddelanden för aktivitetshändelser, inklusive aktivitetstilldelningar, påminnelser och deadlines för uppgifter i din Att göra-lista och i gruppAtt göra-listor som du tillhör.
* **Bifoga Forms i e-postmeddelande:** Anger om en kopia av formuläret bifogas till e-postmeddelanden. Bifogade filer stöds bara för PDF- och XDP-formulär.
* **Spara utkast periodiskt:** Anger om dina formulärutkast sparas automatiskt regelbundet eller inte. Om du vill spara dina utkast regelbundet aktiverar du det här alternativet och anger hur länge du vill spara automatiskt från 1 till 30 minuter. När Spara automatiskt är aktiverat och en användare arbetar med ett utkast, sparas utkastet regelbundet efter det angivna antalet minuter. Utkastet sparas bara automatiskt när det finns en ändring i utkastet sedan det senast sparades eller sparades automatiskt. När utkastet sparas visas ett varningsmeddelande på skärmen.
