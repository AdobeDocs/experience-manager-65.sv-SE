---
title: Administrera arbetsflöden
seo-title: Administrera arbetsflöden
description: Lär dig hur du administrerar arbetsflöden i AEM.
seo-description: Lär dig hur du administrerar arbetsflöden i AEM.
uuid: d000a13c-97cb-4b1b-809e-6c3eb0d675e8
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 4b09cd44-434e-4834-bc0d-c9c082a4ba5a
translation-type: tm+mt
source-git-commit: 5a99daa208d1d109d2736525fdca3accdcfb4dd1
workflow-type: tm+mt
source-wordcount: '788'
ht-degree: 0%

---


# Administrera arbetsflöden{#administering-workflows}

Med arbetsflöden kan du automatisera Adobe Experience Manager-aktiviteter (AEM). Arbetsflöden:

* Består av en serie steg som körs i en viss ordning.

   * Varje steg har en egen verksamhet. som att vänta på användarindata, aktivera en sida eller skicka ett e-postmeddelande.

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
>* Förbättra prestanda för arbetsflöden som använder betydande serverresurser: [Samtidig arbetsflödesbearbetning](/help/sites-deploying/configuring-performance.md#concurrent-workflow-processing).

>



## Arbetsflödesmodeller och instanser {#workflow-models-and-instances}

[Arbetsflödesmodelli ](/help/sites-developing/workflows.md#model) AEM representerar och implementerar affärsprocesser:

* Vanligtvis arbetar de med sidor eller resurser för att uppnå ett visst resultat.
* Dessa sidor och/eller resurser kallas arbetsflödets nyttolast.
* Arbetsflödesmodeller består av en serie steg som utför en viss uppgift.
* Nyttolasten överförs från steg till steg när arbetsflödet fortskrider.

När en arbetsflödesmodell startas (körs) skapas en arbetsflödesinstans. En arbetsflödesmodell kan startas flera gånger, varje gång en distinkt arbetsflödesinstans genereras. För varje instans körs stegen som definieras av arbetsflödesmodellen.

>[!CAUTION]
>
>Stegen som utförs är de som definieras av arbetsflödesmodellen *när instansen skapas*. Mer information finns i [Utveckla arbetsflöden](/help/sites-developing/workflows.md#model).

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
>Om ett fel inträffar bör tjänste-/stegimplementeringen hantera beteendet för ett felscenario. Arbetsflödesmotorn kommer själv att försöka utföra jobbet igen, logga ett fel och stoppa instansen.

## Arbetsflödesstatus och åtgärder {#workflow-status-and-actions}

Ett arbetsflöde kan ha någon av följande status:

* **KÖRS**: Arbetsflödesinstansen körs.
* **SLUTFÖRT**: Arbetsflödesinstansen har avslutats.

* **UPPSKJUTEN**: Markerar arbetsflödet som pausat. Se dock varningsmeddelandet nedan om du har några problem med det här läget.
* **AVBRUTEN**: Arbetsflödesinstansen har avslutats.
* **STAL**: Progression av arbetsflödesinstansen kräver att ett bakgrundsjobb körs, men jobbet kan inte hittas i systemet. Detta kan inträffa när ett fel inträffar när arbetsflödet körs.

>[!NOTE]
>
>När körningen av ett processsteg resulterar i fel visas steget i administratörens inkorg och arbetsflödets status är **RUNNING**.

Beroende på aktuell status kan du utföra åtgärder för att köra arbetsflödesinstanser när du behöver ingripa i den normala förloppet för en arbetsflödesinstans:

* **Gör uppehåll**: När du gör uppehåll ändras arbetsflödets status till Pausat. Se Varning nedan:

>[!CAUTION]
>
>Det finns ett känt fel när ett arbetsflödesläge markeras som Pausa. I det här läget är det möjligt att vidta åtgärder för pausade arbetsflödesobjekt i en Inkorg.

* **Återuppta**: Startar om ett pausat arbetsflöde på samma plats där det pausades, med samma konfiguration.
* **Avsluta**: Avslutar arbetsflödets körning och ändrar tillståndet till  **ABORTED**. En avbruten arbetsflödesinstans kan inte startas om.

