---
title: Innehållsdispositionsfilter
seo-title: Innehållsdispositionsfilter
description: Lär dig hur du använder filtret för innehållsdisposition för att förhindra XSS-attacker.
seo-description: Lär dig hur du använder filtret för innehållsdisposition för att förhindra XSS-attacker.
uuid: 145a88e0-9fa8-42db-b189-eda507c33049
contentOwner: trushton
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: Security
discoiquuid: badfaa18-472e-4777-a7dc-9c28441b38b7
exl-id: 1c3d0d48-5c31-42a8-8698-922d7c2127e9
source-git-commit: d1fc2ff44378276522c2ff3208f5b3bdc4484bba
workflow-type: tm+mt
source-wordcount: '254'
ht-degree: 0%

---

# Innehållsdispositionsfilter {#content-disposition-filter}

Dispositionsfiltret är en säkerhetsfunktion mot XSS-attacker på SVG-filer.

När filtret har installerats blockeras åtkomsten till alla resurser. Du kan till exempel inte visa en PDF online. I det här avsnittet beskrivs hur du konfigurerar filtret efter dina behov.

## Konfigurera filtret för innehållsdisposition {#configure-content-disposition-filter}

Du kan visa filtret [Apache Sling Content Disposition Filter i GitHub](https://github.com/apache/sling-org-apache-sling-security/blob/master/src/main/java/org/apache/sling/security/impl/ContentDispositionFilterConfiguration.java).

Alternativen för Innehållsdispositionsfilter innehåller följande funktioner:

* **Innehållsdispositionssökvägar:** en lista över sökvägar där filtret ska användas följt av en lista med MIME-typer som ska uteslutas på den sökvägen. Sökvägen måste vara en absolut sökväg och kan innehålla ett jokertecken (`*`) i slutet, för att matcha alla resurssökvägar med det angivna sökvägsprefixet. Till exempel: `/content/*:image/jpeg,image/svg+xml` tillämpar filtret på alla noder i `/content?` förutom jpg- och svg-bilder

* **Uteslutna resurssökvägar:** en lista över uteslutna resurser. Varje resurssökväg måste anges som en absolut och fullständig sökväg. Prefixmatchning/jokertecken stöds inte.

* **Aktivera för alla resurssökvägar:** den här flaggan anger om det här filtret ska aktiveras för alla sökvägar, utom för de uteslutna sökvägarna som definieras av Undantagna resurssökvägar. Om du anger värdet true ignoreras innehållets dispositionsbanor. Oberoende av konfigurationen täcks bara resurssökvägar som innehåller egenskapen `jcr:data` eller `jcr:content/jcr:data`.
