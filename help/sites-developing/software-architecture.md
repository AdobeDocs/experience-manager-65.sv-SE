---
title: Programvaruarkitektur
seo-title: Programvaruarkitektur
description: Bästa tillvägagångssätt för att skapa programvara
seo-description: Bästa tillvägagångssätt för att skapa programvara
uuid: a557f6ca-c3f1-486e-a45e-6e1f986fab41
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 92971747-1c74-4917-b5a0-7b79b3ae1e68
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Programvaruarkitektur{#software-architecture}

## Design för uppgraderingar {#design-for-upgrades}

När du utökar OTB-beteenden är det viktigt att tänka på uppgraderingarna. Använd alltid anpassningar i katalogen /apps och lägg antingen över motsvarande noder i katalogen /libs eller använd sling:resourceSuperType för att utöka beteendet utanför rutan. Även om vissa ändringar kan behövas för att stödja en ny AEM-version, bör den nya versionen inte skriva över dina anpassningar om den här metoden följs.

### Återanvänd mallar och komponenter när det är möjligt {#reuse-template-and-components-when-possible}

På så sätt kan webbplatsen få ett mer konsekvent utseende och känsla och förenkla kodunderhållet. När en ny mall behövs måste du se till att utöka från en delad basmall så att globala krav som klientlib-inkludering kan kodas på ett ställe. När en ny komponent behövs letar du efter möjligheter att utöka från en befintlig komponent.

### Designa mallar {#design-template-designs}

Genom att definiera vilka komponenter som kan inkluderas i varje parsys på sidan kan du styra enhetligheten i webbplatsens utseende och känsla. Genom att begränsa åtkomsten till designen på sidor kan superförfattare ändra de tillåtna komponenterna per sida utan att behöva göra något från utvecklaren samtidigt som de säkerställer att de andra författarna följer företagets standarder.

### Utveckla en SOLID-arkitektur {#develop-a-solid-architecture}

SOLID är en förkortning som beskriver fem arkitektoniska principer som bör följas:

* **Principen om** ett enda ansvar - varje modul, klass, metod osv. ska bara göra en sak.
* ****&#x200B;Öppen/stängd princip - modulerna bör vara öppna för utökning och stängda för ändring.
* **Liskov** Substitution Principle - Typerna ska kunna ersättas av sina undertyper.
* **Princip för** gränssnittssegmentering - ingen klient ska tvingas att vara beroende av metoder som den inte använder.
* **Princip för** beroendekonvertering - moduler på hög nivå bör inte vara beroende av moduler på låg nivå. Båda bör vara beroende av abstraktioner. Abstraktioner bör inte vara beroende av detaljer. Detaljer bör vara beroende av abstraktioner.

Att sträva efter att följa dessa fem principer bör leda till ett system som är strikt åtskilt från oron.

### Följ tillförlitlighetsprincipen {#follow-the-robustness-principle}

Robusitetsprincipen säger att vi bör vara konservativa i det vi skickar, men vara liberala i det vi accepterar. Med andra ord, när vi skickar meddelanden till en tredje part bör vi helt och hållet följa specifikationerna, men när vi tar emot meddelanden från en tredje part bör vi acceptera meddelanden som inte överensstämmer så länge som meddelandets betydelse är tydlig.

### Implementera toppar i sina egna moduler {#implement-spikes-in-their-own-modules}

Taggar och testkod är en integrerad del av alla Agile-programimplementeringar, men vi vill försäkra oss om att de inte kommer in i vår produktionskodbas utan lämplig nivå av övervakning. Därför rekommenderar vi att du skapar toppar i en egen modul.

### Implementera skript för datamigrering i sin egen modul {#implement-data-migration-scripts-in-their-own-module}

Skript för datamigrering körs vanligtvis bara en gång när en webbplats startas första gången. Så fort sajten är publicerad blir den därför död. För att säkerställa att vi inte bygger implementeringskod som är beroende av migreringsskripten, bör de implementeras i sin egen modul. Detta gör att vi kan ta bort och kassera koden direkt efter start, vilket eliminerar den döda koden från systemet.

### Följ publicerade Maven-konventioner i POM-filer {#follow-published-maven-conventions-in-pom-files}

Apache har publicerat formatkonventioner på [https://maven.apache.org/developers/conventions/code.html](https://maven.apache.org/developers/conventions/code.html). Det är bäst att följa de här konventionerna eftersom det blir enklare för nya resurser att komma igång snabbt.
