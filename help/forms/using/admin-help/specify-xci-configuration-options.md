---
title: Ange XCI-konfigurationsalternativ
description: Lär dig hur du anger XCI-konfigurationsalternativ.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 8fbff12a-4923-4151-a758-c1e44dee9160
source-git-commit: 3885cc51f7e821cdb352737336a29f9c4f0c2f41
workflow-type: tm+mt
source-wordcount: '128'
ht-degree: 0%

---

# Ange XCI-konfigurationsalternativ {#specify-xci-configuration-options}

Med Output kan du ange en anpassad XCI-fil som används för återgivning. Se [Ange filplatser för utdata](/help/forms/using/admin-help/specify-file-locations-output.md#specify-file-locations-for-output).

Som standard åsidosätter Output några av alternativen som anges i XCI-filen, bland annat följande:

* `config/present/xdp/packets`
* `config/present/pdf/creator`
* `config/present/pdf/producer`
* `config/present/pdf/compression/compressObjectStream`

Du kan välja alternativ som avbryter åsidosättningen för de alternativ som anges ovan. I så fall används de värden som anges i den anpassade XCI-filen för utdata.

1. I administrationskonsolen klickar du på **Tjänster** > output.
1. Markera eller avmarkera kryssrutan Använd XCI-standardalternativ för system. När det här alternativet är markerat använder Output standardvärdena för inställningarna för paket, skapare, producent och compressObjectStream. När det här alternativet är avmarkerat används de värden som anges i den anpassade XCI-filen.
1. Klicka **Spara**.
