---
title: Innehållsdispositionsfilter
description: Lär dig hur du använder filtret för innehållsdisposition för att förhindra XSS-attacker.
contentOwner: trushton
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: Security
exl-id: 1c3d0d48-5c31-42a8-8698-922d7c2127e9
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '225'
ht-degree: 0%

---

# Innehållsdispositionsfilter {#content-disposition-filter}

Dispositionsfiltret är en säkerhetsfunktion mot XSS-attacker mot SVG-filer.

När filtret har installerats blockeras åtkomsten till alla resurser. Du kan till exempel inte visa PDF online. I det här avsnittet beskrivs hur du konfigurerar filtret efter dina behov.

## Konfigurera filtret för innehållsdisposition {#configure-content-disposition-filter}

Du kan visa [Apache Sling Content Disposition Filter i GitHub](https://github.com/apache/sling-org-apache-sling-security/blob/master/src/main/java/org/apache/sling/security/impl/ContentDispositionFilterConfiguration.java).

Alternativen för Innehållsdispositionsfilter innehåller följande funktioner:

* **Sökvägar för innehållsdisposition:** En lista med sökvägar där filtret används följt av en lista med MIME-typer som ska uteslutas på den sökvägen. Sökvägen måste vara en absolut sökväg och kan innehålla jokertecken (`*`) i slutet så att alla resurssökvägar matchar det angivna sökvägsprefixet. Till exempel: `/content/*:image/jpeg,image/svg+xml` använder filtret på alla noder i `/content?` utom JPG och SVG.

* **Uteslutna resurssökvägar:** En lista över uteslutna resurser. Varje resurssökväg måste anges som en absolut och fullständig sökväg. Prefixmatchning/jokertecken stöds inte.

* **Aktivera för alla resurssökvägar:** Den här flaggan styr om det här filtret ska aktiveras för alla sökvägar, förutom för de uteslutna sökvägarna som definieras av Uteslutna resurssökvägar. Om du anger flaggan som true ignoreras innehållets dispositionssökvägar. Oberoende av konfigurationen täcks bara resurssökvägar som innehåller en egenskap med namnet `jcr:data` eller `jcr:content/jcr:data`.
