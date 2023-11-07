---
title: Konfigurera standardkomponenter i designläge
description: Konfigurera Adobe Experience Manager-komponenter i designläge.
exl-id: 5e232886-75c1-4f0f-b359-4739ae035fd3
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '914'
ht-degree: 0%

---

# Konfigurera standardkomponenter i designläge{#configuring-components-in-design-mode}

När AEM är installerad i körklart läge är ett urval av komponenter omedelbart tillgängliga i komponentwebbläsaren.

Förutom dessa finns även andra komponenter tillgängliga. Du kan använda designläget för att [aktivera/inaktivera sådana komponenter](#enable-disable-components). När det är aktiverat och finns på sidan kan du sedan använda designläget för att [konfigurera komponentdesignens aspekter](#configuring-the-design-of-a-component) genom att redigera attributparametrarna.

>[!NOTE]
>
>Försiktighet måste iakttas vid redigering av dessa komponenter. Designinställningarna är ofta en viktig del av designen för hela webbplatsen, så de bör bara ändras av någon med rätt behörighet och upplevelse, ofta en administratör eller en utvecklare. Se [Utveckla komponenter](/help/sites-developing/components.md) för mer information.

>[!NOTE]
>
>Designläget är bara tillgängligt för statiska mallar. Mallar som skapas med redigerbara mallar bör redigeras med [mallredigerare](/help/sites-authoring/templates.md).

>[!NOTE]
>
>Designläget är endast tillgängligt för designkonfigurationer som lagras som innehåll under ( `/etc`).
>
>Från och med AEM 6.4 rekommenderas att du lagrar designer som konfigurationsdata under `/apps` för att stödja scenarier för kontinuerlig driftsättning. Designer lagrade under `/apps` går inte att redigera under körning och designläget är inte tillgängligt för användare som inte är administratörer för sådana mallar.

Det innebär att du lägger till eller tar bort de komponenter som är tillåtna i sidans styckesystem. Styckesystemet ( `parsys`) är en sammansatt komponent som innehåller alla andra styckekomponenter. Med styckesystemet kan författare lägga till komponenter av olika typer på en sida eftersom det innehåller alla andra styckekomponenter. Varje stycketyp representeras som en komponent.

Innehållet på en produktsida kan till exempel innehålla ett styckesystem som innehåller följande:

* En bild av produkten (i form av en bild eller ett textimagestycke)
* Produktbeskrivningen (som ett textstycke)
* En tabell med tekniska uppgifter (som ett tabellstycke)
* En formuläranvändare fyller i (när ett formulär börjar, formulärelement och slutstycke för formulär)

>[!NOTE]
>
>Se [Utveckla komponenter](/help/sites-developing/components.md) och [Riktlinjer för användning av mallar och komponenter](/help/sites-developing/dev-guidelines-bestpractices.md#guidelines-for-using-templates-and-components) för mer information om `parsys`.

>[!CAUTION]
>
>Vi rekommenderar att du definierar design av statiska mallar genom att redigera designen i designläge enligt beskrivningen i den här artikeln
>
>Det är till exempel inte bra att ändra designen i CRX DE, och tillämpningen av den typen av design kan variera från förväntat beteende. Se utvecklardokumentet [Sidmallar - statiska](/help/sites-developing/page-templates-static.md#how-template-designs-are-applied) för mer information.

## Aktivera/inaktivera komponenter {#enable-disable-components}

Så här aktiverar eller inaktiverar du en komponent:

1. Välj **Design** läge.

   ![screen_shot_2018-03-22at103113](assets/screen_shot_2018-03-22at103113.png)

1. Tryck eller klicka på en komponent. Komponenten får en blå kantlinje när den markeras.

   ![screen_shot_2018-03-22at103204](assets/screen_shot_2018-03-22at103204.png)

1. Klicka eller tryck på **Överordnad** -ikon.

   ![Överordnad](do-not-localize/screen_shot_2018-03-22at103204.png)

   Då väljs det styckesystem som innehåller den aktuella komponenten.

1. The **Konfigurera** -ikonen för styckesystemet visas i det överordnade objektets åtgärdsfält.

   ![Konfigurera](do-not-localize/screen_shot_2018-03-22at103256.png)

   Välj det här alternativet om du vill visa dialogrutan.

1. Använd dialogrutan för att definiera de komponenter som är tillgängliga i komponentwebbläsaren när du redigerar den aktuella sidan.

   ![screen_shot_2018-03-22at103329](assets/screen_shot_2018-03-22at103329.png)

   Dialogrutan har två flikar:

   * Tillåtna komponenter
   * Inställningar

   **Tillåtna komponenter**

   På **Tillåtna komponenter** definierar du vilka komponenter som är tillgängliga för parsysen.

   * Komponenterna grupperas efter komponentgrupperna, som kan expanderas och komprimeras.
   * Du kan markera en hel grupp genom att markera gruppnamnet och avmarkera alla genom att avmarkera kryssrutan.
   * Ett minustecken representerar minst ett, men inte alla, objekt i en grupp markeras.
   * Det finns en sökning som du kan använda för att filtrera efter en komponent efter namn.
   * Antalet som visas till höger om komponentgruppens namn representerar det totala antalet valda komponenter i dessa grupper oavsett filtret.

   Du definierar konfigurationen per sidkomponent. Om underordnade sidor använder samma mall och/eller sidkomponent (vanligtvis justerad) används samma konfiguration för motsvarande styckesystem.

   >[!NOTE]
   >
   >Adaptiva formulärkomponenter är utformade för att fungera i adaptiva formulärbehållare för att använda Forms ekosystem. Därför får dessa komponenter endast användas i en anpassad formulärredigerare och de fungerar inte i sidredigeraren Platser.

   **Inställningar**

   På **Inställningar** kan du definiera ytterligare alternativ, t.ex. för att rita en ankarpunkt för varje komponent och för att definiera cellutfyllnaden för varje behållare.

1. Välj **Klar** för att spara konfigurationen.

## Konfigurera designen för en komponent {#configuring-the-design-of-a-component}

1. Välj **Design** läge.

   ![screen_shot_2018-03-22at103113-1](assets/screen_shot_2018-03-22at103113-1.png)

1. Tryck eller klicka på en komponent med en blå ram. I det här exemplet markeras en hjältebildkomponent.

   ![screen_shot_2018-03-22at103434](assets/screen_shot_2018-03-22at103434.png)

1. Använd **Konfigurera** för att öppna dialogrutan.

   ![Ikonen Konfigurera](do-not-localize/screen_shot_2018-03-22at103256-1.png)

   I designdialogrutan kan du konfigurera komponenten enligt tillgängliga designparametrar.

   ![screen_shot_2018-03-22at103530](assets/screen_shot_2018-03-22at103530.png)

   Dialogrutan har tre flikar:

   * Huvud
   * Funktioner
   * Stilar

   **Egenskaper**

   The **Egenskaper** Med -fliken kan du konfigurera komponentens viktiga designparametrar. För en bildkomponent kan du till exempel definiera den största och minsta tillåtna storleken för bilden.

   **Funktioner**

   The **Funktioner** kan du aktivera eller inaktivera ytterligare funktioner för komponenten. För en bildkomponent kan du till exempel definiera bildens orientering, tillgängliga beskärningsalternativ och om en bild kan överföras.

   **Stilar**

   The **Stilar** Med -fliken kan du definiera de CSS-klasser och -format som ska användas med komponenten.

   ![screen_shot_2018-03-22at103741](assets/screen_shot_2018-03-22at103741.png)

   Använd **Lägg till** om du vill lägga till fler poster i en flerpostsdialogrutelista.

   ![Lägg till ytterligare post](assets/chlimage_1-94.png)

   Använd **Ta bort** om du vill ta bort en post från en dialogruta med flera poster.

   ![Ta bort](do-not-localize/screen_shot_2018-03-22at103809.png)

   Använd **Flytta** om du vill ändra ordningen på posterna i en dialogruta med flera poster.

   ![Flytta](do-not-localize/screen_shot_2018-03-22at103816.png)

1. Klicka eller tryck på **Klar** -ikonen för att spara och stänga dialogrutan.
