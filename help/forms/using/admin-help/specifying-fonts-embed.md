---
title: Ange teckensnitt som ska bäddas in
description: Lär dig hur du anger teckensnitt som ska bäddas in i ett anpassat formulär. Du kan ange vilka teckensnitt som är inbäddade eller aldrig inbäddade med formulär som genereras av Forms-tjänsten.
uuid: 97de6f98-ed3b-4a93-854a-193a967b4672
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 4c83694c-b00f-40be-9ac4-f5785cd60741
exl-id: b2cbf5f3-ee13-47bf-bf7f-f6a1884cee66
source-git-commit: 6caf3ef4a00275f0f73be52b6a9ccba77d277f1a
workflow-type: tm+mt
source-wordcount: '258'
ht-degree: 0%

---

# Ange teckensnitt som ska bäddas in {#specifying-fonts-to-embed}

Du kan ange vilka teckensnitt som alltid är inbäddade eller aldrig inbäddade med de formulär som genereras av Forms-tjänsten. När du bäddar in teckensnitt ökar formulärens filstorlek. Bädda in ovanliga teckensnitt som användarna sällan har i sina system. Bädda inte in vanliga teckensnitt som de vanligtvis har installerade.

>[!NOTE]
>
>Om du har angett en anpassad XCI-fil för Forms åsidosätter alternativet för att bädda in teckensnitt i XCI-filen dessa inställningar. (Se [Konfigurera platser för Forms](/help/forms/using/admin-help/configuring-locations-forms.md#configuring-locations-for-forms).)

1. I administrationskonsolen klickar du på **[!UICONTROL Services > Forms]**.
1. Under **[!UICONTROL Font Embedding Settings]**, i **[!UICONTROL Always Embed Fonts]** skriver du namnen på teckensnitten som ska bäddas in med formulären, avgränsade med kommatecken. De teckensnitt du anger bäddas bara in i det genererade formuläret om de används i formuläret. Den här inställningen ignoreras om alternativet för att bädda in teckensnitt har aktiverats i XCI-filen som skickas till tjänsten, eftersom alla teckensnitt som används i PDF alltid bäddas in.
1. I **[!UICONTROL Never Embed Fonts]** anger du namnen på teckensnitten som inte ska bäddas in med formulären, avgränsade med kommatecken. De teckensnitt du anger bäddas inte in i PDF, även om de används i det genererade PDF. Den här inställningen ignoreras om alternativet för inbäddning av teckensnitt har inaktiverats i XCI-filen som skickas till tjänsten, eftersom inga av teckensnitten som används i PDF är inbäddade.
1. Klicka på **[!UICONTROL Save]**.
