---
title: Ange XCI-konfigurationsalternativ
description: Lär dig hur du anger XCI-konfigurationsalternativ. Du kan ange anpassade XCI-filvärden för adaptiv form så att de kan användas vid formuläråtergivning.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 7cd10389-63e6-41f2-a132-92fd9e40a9b7
source-git-commit: 6caf3ef4a00275f0f73be52b6a9ccba77d277f1a
workflow-type: tm+mt
source-wordcount: '149'
ht-degree: 0%

---

# Ange XCI-konfigurationsalternativ {#specifying-xci-configuration-options}

Med Forms kan du ange en anpassad XCI-fil som kan användas för återgivning. (Se [Konfigurera platser för Forms](/help/forms/using/admin-help/configuring-locations-forms.md#configuring-locations-for-forms).) Som standard åsidosätter Forms några av de alternativ som anges i XCI-filen, bland annat följande:

* `config/present/xdp/packets`
* `config/present/pdf/creator`
* `config/present/pdf/producer`
* `config/present/pdf/compression/compressObjectStream`

Du kan välja alternativ som avbryter åsidosättningen för alternativen ovan. I så fall använder Forms värdena som anges i den anpassade XCI-filen.

1. I administrationskonsolen klickar du på **Tjänster** > **Forms**.
1. Markera eller avmarkera kryssrutan Använd XCI-standardalternativ för system. När det här alternativet är markerat använder Forms standardvärden för inställningarna för paket, skapare, producent och compressObjectStream. När det här alternativet är avmarkerat används de värden som anges i den anpassade XCI-filen.
1. Klicka **Spara**.
