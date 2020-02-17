---
title: Ange XCI-konfigurationsalternativ
seo-title: Ange XCI-konfigurationsalternativ
description: Lär dig hur du anger XCI-konfigurationsalternativ.
seo-description: Lär dig hur du anger XCI-konfigurationsalternativ.
uuid: 5d3c10c1-4a93-4336-b311-20faaf835b9f
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 162c9fda-f4d4-4ad5-a9ab-7554828e821c
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Ange XCI-konfigurationsalternativ {#specifying-xci-configuration-options}

Med Forms kan du ange en anpassad XCI-fil som ska användas för återgivning. (Se [Konfigurera platser för formulär](/help/forms/using/admin-help/configuring-locations-forms.md#configuring-locations-for-forms).) Som standard åsidosätter Forms några av alternativen som anges i XCI-filen, bland annat följande:

* `config/present/xdp/packets`
* `config/present/pdf/creator`
* `config/present/pdf/producer`
* `config/present/pdf/compression/compressObjectStream`

Du kan välja alternativ som avbryter åsidosättningen för alternativen ovan. I så fall använder Forms värdena som anges i den anpassade XCI-filen.

1. Klicka på Tjänster > Formulär i administrationskonsolen.
1. Markera eller avmarkera kryssrutan Använd XCI-standardalternativ för system. När det här alternativet är markerat används standardvärdena för inställningarna för paket, skapare, producent och compressObjectStream. När det här alternativet är avmarkerat används de värden som anges i den anpassade XCI-filen.
1. Klicka på Spara.

