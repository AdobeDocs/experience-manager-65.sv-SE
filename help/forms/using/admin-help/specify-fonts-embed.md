---
title: Ange teckensnitt som ska bäddas in
seo-title: Ange teckensnitt som ska bäddas in
description: Lär dig hur du anger teckensnitt som ska bäddas in.
seo-description: Lär dig hur du anger teckensnitt som ska bäddas in.
uuid: 02da5c00-0467-4633-a076-c36725cbfbad
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 180f0448-d507-4b6d-bb8a-d12a434e1250
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Ange teckensnitt som ska bäddas in{#specify-fonts-to-embed}

Du kan ange vilka teckensnitt som alltid är inbäddade eller aldrig inbäddade med de formulär som används i Output. När du bäddar in teckensnitt ökar formulärens filstorlek. Bädda in ovanliga teckensnitt som användarna troligtvis inte har i sina system och bädda inte in vanliga teckensnitt som de har installerat.

>[!NOTE]
>
>Om du har angett en anpassad XCI-fil för Output åsidosätter alternativet för inbäddning av teckensnitt i XCI-filen dessa inställningar. (Se [Ange filplatser för utdata](/help/forms/using/admin-help/specify-file-locations-output.md#specify-file-locations-for-output).)

1. Klicka på Tjänster > Utdata i administrationskonsolen.
1. Under Inställningar för teckensnittsinbäddning skriver du namnen på teckensnitten som ska bäddas in med formulären, avgränsade med kommatecken, i rutan Inkludera alltid teckensnitt. De teckensnitt du anger bäddas bara in i det genererade formuläret om de används i formuläret. Den här inställningen ignoreras om alternativet för att bädda in teckensnitt har aktiverats i XCI-filen som skickas till tjänsten. I så fall bäddas alla teckensnitt som används i PDF-filen alltid in.
1. I rutan Inkludera aldrig teckensnitt skriver du namnen på de teckensnitt som inte ska bäddas in med formulären, avgränsade med kommatecken. De teckensnitt du anger bäddas inte in i PDF-filen, även om de används i den genererade PDF-filen. Den här inställningen ignoreras om alternativet för att bädda in teckensnitt har inaktiverats i XCI-filen som skickas till tjänsten. I så fall bäddas inget av teckensnitten som används i PDF-filen in.
1. Klicka på Spara.

