---
title: Länkkontrollen
description: Länkkontrollen hjälper till att validera både interna och externa länkar och tillåter att länkar skrivs om.
translation-type: tm+mt
source-git-commit: 8a551cce581056cb274b1d8567f579fc73a95d3c
workflow-type: tm+mt
source-wordcount: '986'
ht-degree: 0%

---


# Länkkontrollen {#the-link-checker}

Innehållsförfattare behöver inte bekymra sig om att validera alla länkar som de inkluderar på sina innehållssidor.

Länkkontrollen körs automatiskt så att skribenterna får hjälp med sina länkar:

* Validera länkar när de läggs till i innehållet
* Visar en lista över alla externa länkar i innehållet
* Utföra länktomformningar

Länkkontrollen har ett antal [konfigurationsalternativ](#configuring) som att definiera den interna valideringen, tillåta att vissa länkar eller länkmönster utelämnas från verifieringen och skriva om regler för länkrementering.

Länkkontrollen verifierar både [interna länkar](#internal) och [externa länkar.](#external)

>[!NOTE]
>
>Eftersom länkkontrollen används för att kontrollera länkarna på alla innehållssidor kan länkkontrollen påverka prestanda för stora databaser. I sådana fall kan du behöva [konfigurera hur ofta Länkkontrollen körs](#configuring) eller [inaktivera den.](#disabling)

## Intern länkkontroll {#internal}

Interna länkar är länkar till annat innehåll i AEM. Du kan lägga till interna länkar med sökvägsväljaren i textredigeraren eller med en anpassad komponent. Till exempel:

* Sidan `/content/wknd/us/en/adventures/ski-touring.html`
* Innehåller en länk till `/content/wknd/us/en/adventures/extreme-ironing.html` i en [textkomponent.](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/text.html)

Interna länkar valideras så snart innehållsförfattaren lägger till en intern länk på en sida. Om länken blir ogiltig:

* Den tas bort från utgivaren. Länktexten finns kvar, men själva länken tas bort.
* Den visas som en bruten länk i redigeringsgränssnittet.

![Bruten intern länk vid redigering av en sida](assets/link-checker-invalid-link-internal.png)

## Kontroll av extern länk {#external}

Externa länkar är länkar till innehåll utanför AEM. Externa länkar kan läggas till med RTE eller med en anpassad komponent. Till exempel:

* Sidan `/content/wknd/us/en/adventures/ski-touring.html`
* Innehåller en länk till `https://bunwarmerthermalunderwear.com` i en [textkomponent.](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/text.html)

Externa länkar valideras för syntax och genom att deras tillgänglighet kontrolleras. Den här kontrollen utförs asynkront på en konfigurerbar intern. Om länkkontrollen hittar en ogiltig extern länk:

* Den tas bort från utgivaren. Länktexten finns kvar, men själva länken tas bort.
* Den visas som en bruten länk i redigeringsgränssnittet.

![Bruten intern länk vid redigering av en sida](assets/link-checker-invalid-link-external.png)

Dessutom ger gränssnittet [External Link Checker](#external-link-checker) en översikt över alla externa länkar på innehållssidorna.

### Använda extern länkkontroll {#external-link-checker}

Så här använder du den externa länkkontrollen:

1. Använd **Navigering**, välj **Verktyg** och sedan **Platser**.
1. Välj **Extern länkkontroll** och en lista över alla externa länkar visas.

![Fönstret External Link Checker](assets/external-link-checker.png)

Följande information visas:

* **Status**  - Valideringsstatusen för länken, som kan vara något av följande:
   * **Giltig**  - Den externa länken kan nås av länkkontrollen
   * **Väntande**  - Den externa länken lades till i webbplatsinnehållet, men har ännu inte validerats av Länkkontrollen
   * **Ogiltig**  - den externa länken kan inte nås av länkkontrollen
* **URL**  - den externa länken
* **Referent**  - Innehållssidan som innehåller den externa länken
   * Detta är bara ifyllt [om det är konfigurerat.](#configuring)
* **Senast markerad**  - Senaste gången länkkontrollen verifierade den externa länken
   * Hur ofta länkar kontrolleras [kan konfigureras.](#configuring)
* **Senaste status**  - Den senaste HTML-statuskoden som returnerades när länken senast kontrollerades
* **Senast tillgänglig**  - Tid sedan länken senast var tillgänglig för länkkontrollen
* **Senast använd**  - tid sedan sidan med den externa länken senast öppnades i redigeringsgränssnittet

Du kan ändra innehållet i fönstret genom att använda de två knapparna högst upp i länklistan:

* **Uppdatera**  - Uppdatera innehållet i listan
* **Markera**  - Om du vill kontrollera en enskild extern länk som är markerad i listan

### Så här fungerar den externa länkkontrollen {#how-it-works}

Extern länkkontroll är lätt att använda men är beroende av ett antal tjänster och du kan lättare förstå hur den fungerar om du vill [konfigurera länkkontrollen](#configuring) efter dina behov.

1. När en innehållsförfattare sparar en länk till en sida aktiveras en händelsehanterare.
1. Händelsehanteraren går igenom allt innehåll under `/content` och söker efter nya eller uppdaterade länkar och lägger till dem i ett cacheminne för Länkkontrollen.
1. Tjänsten **Day CQ Link Checker** körs sedan regelbundet för att kontrollera om posterna i cachen har giltig syntax.
1. Syntaxvaliderade länkar visas sedan i fönstret [External Link Checker](#external-link-checker). De kommer dock att vara i ett **väntande**-läge.
1. **CQ Link Checker Task** körs sedan regelbundet för att validera länkarna genom att ringa ett GET-anrop.
1. **CQ Link Checker Task** uppdaterar sedan posterna i fönstret External Link Checker med resultatet av GET-anropen.

## Konfigurera länkkontrollen {#configuring}

Länkkontrollen är automatiskt tillgänglig i AEM. Det finns dock ett antal OSGi-konfigurationer som kan ändras för att ändra dess beteende:

* **Dag CQ Link Checker Info Storage Service**  - Den här tjänsten definierar storleken på cache-minnet för Länkkontroll i databasen.
* **Dag CQ Link Checker Service**  - Den här tjänsten utför asynkron kontroll av syntaxen för externa länkar. Du kan bland annat definiera kontrollperioden och vilka typer av länkar som ignoreras av kontrollfunktionen.
* **CQ Link Checker-aktivitet**  för Dag - Den här tjänsten utför GET-validering av externa länkar. Det gör att olika definitioner av intervall kan kontrollera dåliga och bra länkar bland andra alternativ.
* **Dag CQ Link Checker Transformer**  - Gör det möjligt att konvertera länkar baserat på en användardefinierad regeluppsättning.

Mer information om hur du ändrar OSGi-inställningar finns i dokumentet [OSGi Configuration Settings](/help/sites-deploying/osgi-configuration-settings.md).

## Inaktiverar länkkontrollen {#disabling}

Du kan välja att inaktivera länkkontrollen helt. Så här gör du:

1. Öppna OSGi-konsolen.
1. Redigera **Dag CQ Link Checker Transformer**
1. Markera de alternativ du vill inaktivera:
   * **Inaktivera kontroll**  för att inaktivera validering av länkar
   * **Inaktivera omskrivning**  för att inaktivera länktomformningar

>[!NOTE]
>
>Om du inaktiverar länkkontroll efter att du har börjat skapa ditt innehåll kan du fortfarande se poster i fönstret [External Link Checker](#external-link-checker), men de kommer inte längre att uppdateras.
