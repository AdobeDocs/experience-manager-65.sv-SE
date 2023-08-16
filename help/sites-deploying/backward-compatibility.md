---
title: Bakåtkompatibilitet i AEM 6.5
seo-title: Backward Compatibility in AEM 6.5
description: Lär dig hur du kan göra dina program och konfigurationer kompatibla med AEM 6.5
seo-description: Learn how to keep your apps and configurations compatible with AEM 6.5
uuid: 81dc2771-f59b-4b24-8932-9e938cba05e0
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: upgrading
content-type: reference
discoiquuid: f3b4ec1d-9054-47d4-afcb-0a0121b94190
docset: aem65
feature: Upgrading
exl-id: c432a014-2dab-4c49-a25b-e4f461d13f9b
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '499'
ht-degree: 1%

---

# Bakåtkompatibilitet i AEM 6.5{#backward-compatibility-in-aem}

## Översikt {#overview}

>[!NOTE]
>
>En lista över innehåll- och konfigurationsändringar som inte omfattas av kompatibilitetspaketet finns i [Omstrukturering av lager i AEM](/help/sites-deploying/repository-restructuring.md).

I AEM 6.5 har alla funktioner utvecklats med bakåtkompatibilitet i åtanke.

I de flesta fall behöver inte kunder som kör AEM 6.3 ändra koden eller anpassningarna när de gör uppgraderingen. För AEM 6.1- och 6.2-kunder finns det inga ytterligare brytningsförändringar än vad man skulle få vid en uppgradering till 6.3.

För undantag där funktioner inte kan hållas bakåtkompatibla kan bakåtinkompatibilitetsproblem för paket och innehåll minskas genom installation av ett kompatibilitetspaket för 6.4 (se hur du konfigurerar nedan för mer information om var du ska hämta). Kompileringspaketet återställer i de flesta fall kompatibiliteten för program som är kompatibla med AEM 6.4.

Med Kompatibilitetspaketet kan du köra AEM i kompatibilitetsläge och skjuta upp anpassad utveckling mot nya AEM funktioner:

>[!NOTE]
>
>Observera att kompatibilitetspaketet bara är en tillfällig lösning för att skjuta upp den utveckling som krävs för att vara AEM 6.5-kompatibel. Det rekommenderas bara som ett sista alternativ om du inte kan hantera kompatibilitetsproblem direkt efter uppgraderingen. Vi rekommenderar att du växlar till inbyggt läge och avinstallerar kompatibilitetspaketet när du har valt att fortsätta med 6.5-baserad anpassad utveckling och att du har tillgång till alla 6.5-funktioner.

![sase](assets/sase.png)

Kompatibilitetspaketet har två lägen: **Routning aktiverad** och **Routning inaktiverad**.

Detta gör att AEM 6.5 kan köras i tre lägen:

**Ursprungligt läge:**

Det inbyggda läget är till för kunder som vill använda alla nya funktioner i AEM 6.5 och är redo att göra en del av utvecklingen för att få anpassningarna att fungera med alla nya funktioner.

Det innebär att du kan behöva göra ändringar i programmet omedelbart efter uppgraderingen.

**Kompatibilitetsläge: Kompatibilitetspaket installerat med routning aktiverat**

Kompatibilitetsläget är avsett för kunder som har anpassat gränssnitt som inte är bakåtkompatibla. Detta gör att AEM kan köras i kompatibilitetsläge och skjuta upp den anpassade utvecklingen mot nya AEM funktioner som inte är kompatibla med en del av din anpassade kod.

**Äldre läge: Kompatibilitetspaket installerat med routning inaktiverat**

Äldre läge är för kunder som har anpassade gränssnitt som baseras på äldre eller inaktuell kod från AEM som har flyttats ut i kompatibilitetspaketet.

![sapte](assets/sapte.png)

## Konfigurera {#how-to-set-up}

The **AEM 6.4 Kompatibilitetspaket för 6.5** kan installeras som ett paket med pakethanteraren. Du kan ladda ned [AEM 6.4 Compatability Pack for 6.5 from the Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?fulltext=compat*&amp;orderby=%40jcr%3Acontent%2Fjcr%3AlastModified&amp;orderby.sort=desc&amp;layout=list&amp;p.offset=0&amp;p.limit=20&amp;package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Fcompatpack%2Faem-compat-cq65-to-cq64) webbplats.

När Kompatibilitetspaketet har installerats kan routningen aktiveras eller inaktiveras med en växel i OSGI-konfigurationen enligt nedan:

![Jämför växlar](assets/compat-switches.png)

När Kompatibilitetspaketet har installerats och konfigurerats används funktionerna baserat på det kompatibilitetsläge som har valts.
