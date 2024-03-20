---
title: Administrera arbetsflöden
description: Lär dig automatisera Adobe Experience Manager-aktiviteter med arbetsflöden.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
exl-id: 10eecfb8-d43d-4f01-9778-87c752dee64c
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '779'
ht-degree: 0%

---

# Administrera arbetsflöden{#administering-workflows}

Med arbetsflöden kan du automatisera Adobe Experience Manager-aktiviteter (AEM). Arbetsflöden:

* Består av en serie steg som körs i en viss ordning.

   * Varje steg utför en distinkt aktivitet, till exempel väntar på användarindata, aktiverar en sida eller skickar ett e-postmeddelande.

* Kan samverka med resurser i databasen, användarkonton och AEM.
* Kan samordna komplicerade aktiviteter som omfattar alla aspekter av AEM.

De affärsprocesser som din organisation har etablerat kan representeras som arbetsflöden. Processen med att publicera webbplatsinnehåll omfattar till exempel vanligtvis steg för godkännande och godkännande av olika intressenter. Dessa processer kan implementeras som AEM arbetsflöden och tillämpas på innehållssidor och resurser.

* [Starta arbetsflöden](/help/sites-administering/workflows-starting.md)
* [Administrera arbetsflödesinstanser](/help/sites-administering/workflows-administering.md)
* [Hantera åtkomst till arbetsflöden](/help/sites-administering/workflows-managing.md)

>[!NOTE]
>
>Mer information finns i:
>
>* Använda och delta i arbetsflöden: [Arbeta med arbetsflöden](/help/sites-authoring/workflows.md).
>* Skapa arbetsflödesmodeller och utöka arbetsflödesfunktioner: [Utveckla och utöka arbetsflöden](/help/sites-developing/workflows.md).
>* Förbättra prestanda för arbetsflöden som använder betydande serverresurser: [Samtidig bearbetning av arbetsflöden](/help/sites-deploying/configuring-performance.md#concurrent-workflow-processing).
>

## Arbetsflödesmodeller och instanser {#workflow-models-and-instances}

[Arbetsflödesmodeller](/help/sites-developing/workflows.md#model) AEM representeras och implementeras affärsprocesser:

* Vanligtvis arbetar de med sidor eller resurser för att uppnå ett visst resultat.
* Dessa sidor och/eller resurser kallas arbetsflödets nyttolast.
* Arbetsflödesmodeller består av en serie steg som utför en viss uppgift.
* Nyttolasten överförs från steg till steg när arbetsflödet fortskrider.

När en arbetsflödesmodell startas (körs) skapas en arbetsflödesinstans. En arbetsflödesmodell kan startas flera gånger, varje gång en distinkt arbetsflödesinstans genereras. För varje instans körs stegen som definieras av arbetsflödesmodellen.

>[!CAUTION]
>
>Stegen som utförs är de som definieras av arbetsflödesmodellen *när instansen genereras*. Se [Utveckla arbetsflöden](/help/sites-developing/workflows.md#model) för mer information.

Arbetsflödesinstanser går igenom följande livscykel:

1. Arbetsflödesmodellen startas och en arbetsflödesinstans skapas och körs.

   1. Arbetsflödesinstansens nyttolast identifieras när modellen startas.
   1. Instansen är i själva verket en kopia av modellen (som när den skapades).
   1. AEM kan skapa arbetsflödesmodeller.

1. Det första steget i arbetsflödesmodellen körs.
1. Stegen slutförs och arbetsflödesmotorn använder modellen för att bestämma nästa steg som ska köras.
1. De följande stegen i arbetsflödesmodellen körs och slutförs.
1. När det sista steget har slutförts slutförs arbetsflödesinstansen och arkiveras därför.

Många användbara arbetsflödesmodeller medföljer AEM. Dessutom kan utvecklarna i organisationen skapa anpassade arbetsflödesmodeller som är anpassade efter affärsprocessernas specifika behov.

## Arbetsflödessteg {#workflow-steps}

När arbetsflödessteg körs kopplas de till en arbetsflödesinstans. Historiken för en arbetsflödesinstans innehåller information om varje steg som har körts för instansen. Den här informationen är användbar för att undersöka problem som uppstår under utförandet.

Antingen utför en användare eller tjänst arbetsflödessteg beroende på typ av steg:

* När en användare utför ett steg tilldelas han/hon en arbetspost som placeras i sin inkorg. Användaren ansvarar för att slutföra steget manuellt så att arbetsflödesinstansen fortskrider.
* När en tjänst utför ett steg, fortsätter arbetsflödesinstansen automatiskt till nästa steg när den är klar.

>[!NOTE]
>
>Om ett fel inträffar bör tjänste-/stegimplementeringen hantera beteendet för ett felscenario. Arbetsflödesmotorn själv försöker utföra jobbet igen, loggar sedan ett fel och stoppar instansen.

## Arbetsflödets status och åtgärder {#workflow-status-and-actions}

Ett arbetsflöde kan ha någon av följande statusar:

* **KÖRS**: Arbetsflödesinstansen körs.
* **SLUTFÖRD**: Arbetsflödesinstansen har avslutats.

* **UPPHÄVD**: Märker upp arbetsflödet som pausat. Se dock varningsmeddelandet nedan om ett känt problem med det här läget.
* **ABORTERAD**: Arbetsflödesinstansen har avslutats.
* **STAL**: Progression för arbetsflödesinstansen kräver att ett bakgrundsjobb körs, men jobbet kan inte hittas i systemet. Detta kan inträffa när ett fel inträffar när arbetsflödet körs.

>[!NOTE]
>
>När körningen av ett processteg resulterar i fel visas steget i administratörens inkorg och arbetsflödets status är **KÖRS**.

Beroende på status kan du utföra åtgärder för att köra arbetsflödesinstanser när du måste ingripa i den normala förloppet för en arbetsflödesinstans:

* **Gör uppehåll**: När du gör uppehåll ändras arbetsflödets status till Pausat. Se Varning nedan:

>[!CAUTION]
>
>Det finns ett känt fel när ett arbetsflödesläge markeras som Pausa. I det här läget är det möjligt att agera på pausade arbetsflödesobjekt i en Inkorg.

* **Återuppta**: Startar om ett pausat arbetsflöde på samma plats där det pausades, med samma konfiguration.
* **Avsluta**: Avslutar arbetsflödets körning och ändrar tillståndet till **ABORTERAD**. En avbruten arbetsflödesinstans kan inte startas om.
