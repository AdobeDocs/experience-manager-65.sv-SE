---
title: Ange teckensnitt som ska bäddas in
seo-title: Specify fonts to embed
description: Lär dig hur du anger teckensnitt som ska bäddas in.
seo-description: Learn how to specify fonts to embed.
uuid: 02da5c00-0467-4633-a076-c36725cbfbad
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 180f0448-d507-4b6d-bb8a-d12a434e1250
exl-id: 02c28b2c-0cab-4431-9fab-fa332c96e092
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '251'
ht-degree: 0%

---

# Ange teckensnitt som ska bäddas in{#specify-fonts-to-embed}

Du kan ange vilka teckensnitt som alltid är inbäddade eller aldrig inbäddade med de formulär som används i Output. När du bäddar in teckensnitt ökar formulärens filstorlek. Bädda in ovanliga teckensnitt som användarna troligtvis inte har i sina system och bädda inte in vanliga teckensnitt som de har installerat.

>[!NOTE]
>
>Om du har angett en anpassad XCI-fil för Output åsidosätter alternativet för inbäddning av teckensnitt i XCI-filen dessa inställningar. (Se [Ange filplatser för utdata](/help/forms/using/admin-help/specify-file-locations-output.md#specify-file-locations-for-output).)

1. Klicka på Tjänster > Utdata i administrationskonsolen.
1. Under Inställningar för teckensnittsinbäddning skriver du namnen på teckensnitten som ska bäddas in med formulären, avgränsade med kommatecken, i rutan Inkludera alltid teckensnitt. De teckensnitt du anger bäddas bara in i det genererade formuläret om de används i formuläret. Den här inställningen ignoreras om alternativet för att bädda in teckensnitt har aktiverats i XCI-filen som skickas till tjänsten. I så fall bäddas alla teckensnitt som används i PDF alltid in.
1. I rutan Inkludera aldrig teckensnitt skriver du namnen på de teckensnitt som inte ska bäddas in med formulären, avgränsade med kommatecken. De teckensnitt du anger bäddas inte in i PDF, även om de används i det genererade PDF. Den här inställningen ignoreras om alternativet för att bädda in teckensnitt har inaktiverats i XCI-filen som skickas till tjänsten. I så fall bäddas inget av teckensnitten som används i PDF in.
1. Klicka på Spara.
