---
title: Översättningsförbättringar
seo-title: Översättningsförbättringar
description: Översättningsförbättringar i AEM.
seo-description: Översättningsförbättringar i AEM.
uuid: 0563603f-327b-48f1-ac14-6777c06734b9
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features
content-type: reference
discoiquuid: 42df2db3-4d3c-4954-a03e-221e2f548305
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Översättningsförbättringar{#translation-enhancements}

Den här sidan innehåller stegvisa förbättringar och förbättringar av funktionerna för hantering av AEM-översättning.

## Automatisering av översättningsprojekt {#translation-project-automation}

Alternativ för att förbättra produktiviteten när du arbetar med översättningsprojekt har lagts till, t.ex. automatiskt för att befordra och ta bort starter för översättningar och schemalägga återkommande körningar av ett översättningsprojekt.

1. Klicka eller tryck på ellipsen längst ned i rutan **Översättningssammanfattning** i översättningsprojektet.

   ![screen_shot_2018-04-19at22622](assets/screen_shot_2018-04-19at222622.jpg)

1. Växla till fliken **Avancerat** . Längst ned kan du välja Befordra översättningsstarter **automatiskt**.

   ![screen_shot_2018-04-19at223430](assets/screen_shot_2018-04-19at223430.jpg)

1. Du kan också välja om översättningar ska befordras automatiskt och tas bort när du har tagit emot översatt innehåll.

   ![screen_shot_2018-04-19at224033](assets/screen_shot_2018-04-19at224033.jpg)

1. Om du vill välja den återkommande körningen av ett översättningsprojekt väljer du frekvensen i listrutan under **Upprepa översättning**. Återkommande projektkörning skapar och kör automatiskt översättningsjobb inom angivna intervall.

   ![screen_shot_2018-04-19at223820](assets/screen_shot_2018-04-19at223820.jpg)

## Flerspråkiga översättningsprojekt {#multilingual-translation-projects}

Det går att konfigurera flera målspråk i ett översättningsprojekt, vilket minskar det totala antalet översättningsprojekt som skapas.

1. Klicka eller tryck på punkterna längst ned i rutan **Översättningssammanfattning** i översättningsprojektet.

   ![screen_shot_2018-04-19at22622](assets/screen_shot_2018-04-19at222622.jpg)

1. Växla till fliken **Avancerat** . Du kan lägga till flera språk under **Målspråk**.

   ![screen_shot_2018-04-22at212601](assets/screen_shot_2018-04-22at212601.jpg)

1. Om du initierar översättning via referenslinjen i Sites, lägger du till språk och väljer **Skapa flerspråkigt översättningsprojekt**.

   ![screen_shot_2018-04-22at212941](assets/screen_shot_2018-04-22at212941.jpg)

1. Översättningsjobb skapas i projektet för alla målspråk. De kan startas antingen en i taget i projektet, eller alla i ett svep genom att projektet körs globalt i Projektadministratör.

   ![screen_shot_2018-04-22at213854](assets/screen_shot_2018-04-22at213854.jpg)

## Uppdateringar av översättningsminne {#translation-memory-updates}

Manuella redigeringar av översatt innehåll kan synkroniseras tillbaka till översättningshanteringssystemet (TMS) för att utbilda översättningsminnet.

1. När du har uppdaterat textinnehåll på en översatt sida i webbplatskonsolen väljer du **Uppdatera översättningsminne**.

   ![screen_shot_2018-04-22at234430](assets/screen_shot_2018-04-22at234430.jpg)

1. I en listvy visas en jämförelse sida vid sida av källan och översättningen för alla textkomponenter som redigerades. Välj vilka översättningsuppdateringar som ska synkroniseras med översättningsminnet och välj **Uppdatera minne**.

   ![screen_shot_2018-04-22at235024](assets/screen_shot_2018-04-22at235024.jpg)

   >[!NOTE]
   >
   >AEM skickar tillbaka de markerade strängarna till översättningshanteringssystemet.

## Språkkopior på flera nivåer {#language-copies-on-multiple-levels}

Språkrötter kan nu grupperas under noder, till exempel efter region, samtidigt som de fortfarande identifieras som rötter i språkkopior.

![screen_shot_2018-04-23at144012](assets/screen_shot_2018-04-23at144012.jpg)

>[!CAUTION]
>
>Endast en nivå tillåts. Följande tillåter till exempel inte att sidan&quot;es&quot; tolkas som en språkkopia:
>
>* `/content/we-retail/language-masters/en`
>* `/content/we-retail/language-masters/americas/central-america/es`
>
>
Den här `es` språkkopian kommer inte att identifieras eftersom den ligger två nivåer (amerika/central-amerika) bort från `en` noden.

>[!NOTE]
>
>Språkrötter kan ha vilket sidnamn som helst, inte bara språkets ISO-kod. AEM kontrollerar alltid sökvägen och namnet först, men om sidnamnet inte identifierar något språk, kontrollerar AEM egenskapen cq:language för sidan för att se om språket är identifierat.

## Översättningsstatusrapportering {#translation-status-reporting}

En egenskap kan nu väljas i platslistevyn som visar om en sida har översatts, är i översättning eller ännu inte har översatts. Så här visar du den:

1. I Platser växlar du till **listvyn.**

   ![screen_shot_2018-04-23at130646](assets/screen_shot_2018-04-23at130646.jpg)

1. Klicka på eller tryck på **Visa inställningar**.

   ![screen_shot_2018-04-23at130844](assets/screen_shot_2018-04-23at130844.jpg)

1. Markera **kryssrutan Översatt** under **Översättning** och tryck/klicka på **Uppdatera**.

   ![screen_shot_2018-04-23at130955](assets/screen_shot_2018-04-23at130955.jpg)

Du kan nu se en **översatt** kolumn som visar sidornas översättningsstatus.

![screen_shot_2018-04-23at133821](assets/screen_shot_2018-04-23at133821.jpg)

