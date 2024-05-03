---
title: Spara en uppgift eller ett formulär som ett utkast
description: Steg för att spara ett utkast av en uppgift eller ett formulär i AEM Forms-appen
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
exl-id: b4a23b2e-ab18-402c-8dfa-2533ee692912
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '492'
ht-degree: 0%

---

# Spara en uppgift eller ett formulär som ett utkast {#saving-a-task-or-form-as-a-draft}

Alternativet Spara som utkast sparar en ögonblicksbild av en uppgift eller ett formulär tillsammans med de data som är ifyllda i det associerade formuläret. Du kan också skapa ett utkast från en mall. Utkasten sparas i den mobila enheten och synkroniseras med Adobe Experience Manager Forms-servern för senare hämtning.

Du kan [uppdatera formuläret](/help/forms/using/working-with-form.md), [kommentera det](/help/forms/using/add-attachments.md) med foton och klottrar. När du fortsätter att uppdatera ett formulär bör du spara det som ett utkast. I situationer där du bestämmer dig för att skicka ett ifyllt formulär vid ett senare tillfälle är det bra att spara det som ett utkast.

Information om hur du aktiverar funktionen Spara som utkast för formulär som sparats på formulärportalen finns i [Spara ett HTML5-formulär som ett utkast](/help/forms/using/saving-html5-form-draft.md).
Information om hur du konfigurerar sändning av adaptiva formulär finns i [Komponenten Utkast och inskickat material](/help/forms/using/draft-submission-component.md). (Gäller inte för formulär som synkroniseras med AEM Forms JEE-servern.)

Om du vill skapa ett utkast öppnar du formuläret och väljer **Spara som utkast** ![spara som utkast](assets/save-as-draft.png). Ange namnet på utkastet och välj **Spara**. Utkastet sparas i mappen Utkast och synkroniseras med servern. Den sparas i Utkorgen om programmet är offline.

Om du uppdaterar formuläret efteråt återspeglas ändringarna direkt. När AEM Forms-appen synkroniseras med AEM Forms-servern överförs utkastet till AEM Forms-servern. Dessutom flyttas utkastet från Utkorgen till mappen Åtgärder eller Utkast. En redigeringsikon visas bredvid den.

När du fortsätter att arbeta med flera uppgifter och startpunkter och sparar dem sparas utkasten. Varje gång appen synkroniseras med AEM Forms-servern sparas utkastet på servern. Det ser till att du när som helst kan återställa utkasten baserat på det senast sparade datumet och den senaste tidpunkten. Om du till exempel installerar om appen eller ändrar din mobila enhet kan du hämta utkastet från servern.

## Ta bort ett utkast {#delete-a-draft}

I mappen Utkast visas alla utkast. Du kan använda alternativet Ta bort utkast för att permanent ta bort utkast från den mobila enheten och servern.

Alternativet att ta bort utkast som skapats från en uppgift är inte tillgängligt. När du tar bort ett utkast som skapats från en uppgift överges uppgiften.

Du kan ta bort utkast både offline och online. När utkast tas bort i offlineläge tas de bort från servern endast när anslutningen till servern återställs.

Så här tar du bort ett utkast:

1. I AEM Forms går du till **Forms.**
1. Välj **Utkast** i listrutan bredvid Sök.
1. Ett formulär med ikonen Redigera ![edit-draft-app](assets/edit-draft-app.png) betecknar ett utkast. Markera den vågräta ellipsen bredvid utkastet.
1. Välj de alternativ som visas när du markerar den vågräta ellipsen **Ta bort utkast**.
