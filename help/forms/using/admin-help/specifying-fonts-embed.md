---
title: Ange teckensnitt som ska bäddas in
seo-title: Ange teckensnitt som ska bäddas in
description: Lär dig hur du anger teckensnitt som ska bäddas in.
seo-description: Lär dig hur du anger teckensnitt som ska bäddas in.
uuid: 97de6f98-ed3b-4a93-854a-193a967b4672
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 4c83694c-b00f-40be-9ac4-f5785cd60741
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Ange teckensnitt som ska bäddas in {#specifying-fonts-to-embed}

Du kan ange vilka teckensnitt som alltid är inbäddade eller aldrig inbäddade med de formulär som genereras av Forms-tjänsten. När du bäddar in teckensnitt ökar formulärens filstorlek. Bädda in ovanliga teckensnitt som användarna sällan har i sina system. Bädda inte in vanliga teckensnitt som de vanligtvis har installerade.

>[!NOTE]
>
>Om du har angett en anpassad XCI-fil för Forms åsidosätter alternativet för att bädda in teckensnitt i XCI-filen dessa inställningar. (Se [Konfigurera platser för formulär](/help/forms/using/admin-help/configuring-locations-forms.md#configuring-locations-for-forms).)

1. I administrationskonsolen klickar du på **[!UICONTROL Tjänster > Formulär]**.
1. Under Inställningar **[!UICONTROL för]** teckensnittsinbäddning skriver du namnen på teckensnitten som ska bäddas in med formulären i rutan **[!UICONTROL Inkludera alltid teckensnitt]** , avgränsade med kommatecken. De teckensnitt du anger bäddas bara in i det genererade formuläret om de används i formuläret. Den här inställningen ignoreras om alternativet för att bädda in teckensnitt har aktiverats i XCI-filen som skickas till tjänsten, eftersom alla teckensnitt som används i PDF-filen i så fall alltid bäddas in.
1. I rutan **[!UICONTROL Inkludera aldrig teckensnitt]** skriver du namnen på de teckensnitt som inte ska bäddas in med formulären, avgränsade med kommatecken. De teckensnitt du anger bäddas inte in i PDF-filen, även om de används i den genererade PDF-filen. Den här inställningen ignoreras om alternativet för inbäddning av teckensnitt har inaktiverats i XCI-filen som skickas till tjänsten, eftersom inga av teckensnitten som används i PDF-filen bäddas in.
1. Click **[!UICONTROL Save]**.

