---
title: Hantera projekt
seo-title: Hantera projekt
description: Med projekt kan du ordna ditt projekt genom att gruppera resurser i en enhet som kan nås och hanteras i projektkonsolen
seo-description: Med projekt kan du ordna ditt projekt genom att gruppera resurser i en enhet som kan nås och hanteras i projektkonsolen
uuid: ac937582-181f-429b-9404-3c71d1241495
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: projects
content-type: reference
discoiquuid: fb354c72-debb-4fb6-9ccf-56ff5785c3ae
translation-type: tm+mt
source-git-commit: 58fa0f05bae7ab5ba51491be3171b5c6ffbe870d

---


# Hantera projekt{#managing-projects}

Med projekt kan du ordna ditt projekt genom att gruppera resurser i en enhet.

I **projektkonsolen** får du tillgång till och kan vidta åtgärder för dina projekt:

![chlimage_1-255](assets/chlimage_1-255.png)

I Projekt kan du skapa ett projekt, associera resurser med projektet och även ta bort en projekt- eller resurslänkar. Du kan öppna en platta om du vill visa dess innehåll och lägga till objekt i en platta. I det här avsnittet beskrivs dessa procedurer.

>[!NOTE]
>
>6.2 har gjort det möjligt att ordna projekt i mappar. På sidan Projekt kan du skapa ett projekt eller en mapp.
>
>Om en mapp skapas kommer användaren till den mappen där han/hon kan skapa en annan mapp eller ett projekt. Det hjälper dig att ordna projekt i mappar baserat på kategorier som produktkampanjer, plats, översättningsspråk och så vidare.
>
>Projekt och mappar kan visas i en listvy och även sökas igenom.

>[!CAUTION]
>
>För användare i projekt som vill se andra användare/grupper när de använder projektfunktioner som att skapa projekt, skapa uppgifter/arbetsflöden, se och hantera team, måste dessa användare ha läsåtkomst på **/hem/användare** och **/hem/grupper**. Det enklaste sättet att implementera detta är att ge **projekt-användare** -gruppen läsåtkomst till **/hem/användare** och **/hem/grupper**.

## Skapa ett projekt {#creating-a-project}

När du skapar ett projekt innehåller AEM följande mallar som du kan välja mellan:

* Enkelt projekt
* Medieprojekt
* Fotoprojekt för produkt
* Översättningsprojekt

Du skapar ett projekt på samma sätt, från projekt till projekt. Skillnaden mellan projekttyperna inkluderar tillgängliga [användarroller](/help/sites-authoring/projects.md) och [arbetsflöden](/help/sites-authoring/projects-with-workflows.md).  Så här skapar du ett nytt projekt:

1. I **Projekt**: tryck/klicka på **Skapa** för att öppna guiden **Skapa projekt** :
1. Välj en mall. Enkelt projekt, medieprojekt, [översättningsprojekt](/help/sites-administering/tc-manage.md)och fotoprodukter [](/help/sites-authoring/managing-product-information.md) finns tillgängliga i kartongen och klicka på **Nästa**.

   ![chlimage_1-256](assets/chlimage_1-256.png)

1. Definiera **titel** och **beskrivning** och lägg till en **miniatyrbild** om det behövs. Du kan också lägga till eller ta bort användare och vilken grupp de tillhör. Klicka dessutom på **Avancerat** för att lägga till ett namn som används i URL:en.

   ![chlimage_1-257](assets/chlimage_1-257.png)

1. Tryck/klicka på **Skapa**. Bekräftelsen frågar om du vill öppna det nya projektet eller gå tillbaka till konsolen.

### Associera resurser med ditt projekt {#associating-resources-with-your-project}

När du kan gruppera resurser i en enhet i projekt vill du koppla resurser till projektet. Resurserna kallas **plattor**. De typer av resurser du kan lägga till beskrivs i [Projektfiler](/help/sites-authoring/projects.md#project-tiles).

Så här associerar du resurser med ditt projekt:

1. Öppna projektet från **projektkonsolen** .
1. Tryck/klicka på **Lägg till platta** och välj den platta som du vill länka till projektet. Du kan markera flera typer av rutor.

   ![chlimage_1-258](assets/chlimage_1-258.png)

   >[!NOTE]
   >
   >Projekttitlar som kan kopplas till ett projekt beskrivs i detalj i [Projekttitlar.](/help/sites-authoring/projects.md#project-tiles)

1. Tryck/klicka på **Skapa**. Resursen är länkad till ditt projekt och från och med nu kan du komma åt den från ditt projekt.

### Ta bort ett projekt eller en resurslänk {#deleting-a-project-or-resource-link}

Samma metod används för att ta bort ett projekt från konsolen eller en länkad resurs från ditt projekt:

1. Navigera till rätt plats:

   * Om du vill ta bort ett projekt går du till den översta nivån i **projektkonsolen** .
   * Om du vill ta bort en resurslänk i ett projekt öppnar du projektet i **projektkonsolen** .

1. Ange markeringsläge genom att klicka på **Välj** och välja projekt- eller resurslänken.
1. Tryck/klicka på **Ta bort**.

1. Du måste bekräfta borttagningen i en dialogruta. Om den bekräftas tas projekt- eller resurslänken bort. Tryck/klicka på **Avmarkera** för att avsluta markeringsläget.

>[!NOTE]
>
>När du skapar projektet och lägger till användare till de olika rollerna skapas grupper som är kopplade till projektet automatiskt för att hantera associerade behörigheter. Ett projekt med namnet Myproject skulle till exempel ha tre grupper, **Myproject Owners**, **Myproject Editors**, **Myproject Observers**. Om projektet däremot tas bort tas de grupperna inte bort automatiskt. En administratör måste ta bort grupperna manuellt i **Verktyg** > **Dokumentskydd** > **Grupper**.

### Lägga till objekt i en platta {#adding-items-to-a-tile}

I vissa rutor kanske du vill lägga till mer än ett objekt. Du kan till exempel ha flera arbetsflöden som körs samtidigt eller fler än en upplevelse.

Så här lägger du till objekt i en platta:

1. Gå till projektet i **Projekt** och klicka på ikonen Lägg till + på den ruta där du vill lägga till ett objekt.

   ![chlimage_1-259](assets/chlimage_1-259.png)

1. Lägg till ett objekt i rutan på samma sätt som när du skapar en ny platta. Projektpaneler beskrivs [här](/help/sites-authoring/projects.md#project-tiles). I det här exemplet har ett annat arbetsflöde lagts till.

   ![chlimage_1-260](assets/chlimage_1-260.png)

### Öppna en platta {#opening-a-tile}

Du kanske vill se vilka objekt som ingår i en aktuell platta eller ändra eller ta bort objekt i plattan.

Så här öppnar du en platta så att du kan visa eller ändra objekt:

1. Tryck/klicka på ellipserna (..) i projektkonsolen

   ![chlimage_1-261](assets/chlimage_1-261.png)

1. AEM listar objekten i den rutan. Du kan gå in i markeringsläge för att ändra eller ta bort objekten.

   ![chlimage_1-262](assets/chlimage_1-262.png)

## Visa projektstatistik {#viewing-project-statistics}

Om du vill visa projektstatistik går du till **projektkonsolen** och klickar på **Visa statistikvy**. Slutförandenivån för varje projekt visas. Klicka på **Visa statistikvy** igen för att gå till **projektkonsolen** .

![chlimage_1-263](assets/chlimage_1-263.png)

### Visa en projekttidslinje {#viewing-a-project-timeline}

Projektets tidslinje innehåller information om när resurser i projektet senast användes. Om du vill visa projekttidslinjen klickar/trycker du på **tidslinjen**, anger ett markeringsläge och väljer projektet. Resurser visas i den vänstra rutan. Klicka/tryck på **Tidslinjen** för att gå tillbaka till **projektkonsolen** .

![chlimage_1-264](assets/chlimage_1-264.png)

### Visa aktiva/inaktiva projekt {#viewing-active-inactive-projects}

Om du vill växla mellan dina aktiva och inaktiva projekt klickar du på **Växla aktiva projekt** i konsolen **Projekt**. Om ikonen har en bockmarkering visas de aktiva projekten.

![chlimage_1-265](assets/chlimage_1-265.png)

Om ikonen har ett x bredvid visas de inaktiva projekten.

![chlimage_1-266](assets/chlimage_1-266.png)

## Göra projekt inaktiva eller aktiva {#making-projects-inactive-or-active}

Du kanske vill göra ett projekt inaktivt om du har slutfört det men ändå vill behålla informationen om projektet.

Så här gör du ett projekt inaktivt (eller aktivt):

1. Öppna projektet i **projektkonsolen** och hitta sedan rutan **Projektinformation** .

   >[!NOTE]
   Du kan behöva lägga till den här panelen om den inte redan finns i ditt projekt. Se [Lägga till rutor](#adding-items-to-a-tile).

1. Tryck/klicka på **Redigera**.
1. Ändra väljaren från **Aktiv** till **Inaktiv** (eller tvärtom).

   ![chlimage_1-267](assets/chlimage_1-267.png)

1. Tryck/klicka på **Klar** för att spara ändringarna.

