---
title: Delta i arbetsflöden
description: Arbetsflödena omfattar vanligtvis steg som kräver att en person utför en aktivitet på en sida eller en resurs. Arbetsflödet väljer en användare eller grupp som ska utföra aktiviteten och tilldelar en arbetsuppgift till den personen eller gruppen.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
exl-id: 2f1a3a73-7a20-48c7-8f3e-54252f5fb71c
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '541'
ht-degree: 3%

---

# Delta i arbetsflöden{#participating-in-workflows}

Arbetsflödena omfattar vanligtvis steg som kräver att en person utför en aktivitet på en sida eller en resurs. Arbetsflödet väljer en användare eller grupp som ska utföra aktiviteten och tilldelar en arbetsuppgift till den personen eller gruppen.

## Bearbetar dina arbetsuppgifter {#processing-your-work-items}

Du kan utföra följande åtgärder för att bearbeta ett arbetsobjekt:

* **Complete**

  Du kan slutföra ett objekt så att arbetsflödet kan fortsätta till nästa steg.

* **Delegera**

  Om du har tilldelats ett steg, men av någon anledning inte kan utföra någon åtgärd, kan du delegera steget till en annan användare eller grupp.

  Vilka användare som är tillgängliga för delegering beror på vem som har tilldelats arbetsposten:

   * Om arbetsuppgiften har tilldelats en grupp är gruppmedlemmarna tillgängliga.
   * Om arbetsuppgiften har tilldelats en grupp och sedan delegerats till en användare, är gruppmedlemmarna och gruppen tillgängliga.
   * Om arbetsuppgiften har tilldelats en enskild användare kan arbetsuppgiften inte delegeras.

* **Gå bakåt**

  Om du upptäcker att ett steg, eller en serie steg, måste upprepas, kan du stega tillbaka. På så sätt kan du välja ett steg som inträffade tidigare i arbetsflödet för ombearbetning. Arbetsflödet återgår till det steg du anger och fortsätter sedan därifrån.

## Delta i ett arbetsflöde {#participating-in-a-workflow}

### Meddelanden om tilldelade arbetsflödesåtgärder {#notifications-of-assigned-workflow-actions}

När du tilldelas en arbetsuppgift (till exempel **Godkänn innehåll**) visas olika varningar och/eller meddelanden:

* The **Status** -kolumnen i webbplatskonsolen anger när en sida är i ett arbetsflöde:

  ![arbetsflödenstatus-1](assets/workflowstatus-1.png)

* När du, eller en grupp som du tillhör, tilldelas en arbetsuppgift som en del av ett arbetsflöde, visas arbetsuppgiften i AEM arbetsflödesinkorg.

  ![arbetsflödewinbox](assets/workflowinbox.png)

### Slutför ett deltagarsteg {#completing-a-participant-step}

När du har vidtagit den angivna åtgärden kan du slutföra arbetsuppgiften och på så sätt tillåta arbetsflödet att fortsätta. Använd följande procedur för att slutföra arbetsuppgiften.

1. Välj arbetsflödessteget och klicka på **Complete** i det övre navigeringsfältet.
1. I dialogrutan som visas väljer du **Nästa steg**, d.v.s. steget som ska köras nästa. En nedrullningsbar lista visar alla lämpliga destinationer. A **Kommentar** kan också anges.

   ![arbetsflöde slutfört](assets/workflowcomplete.png)

   Hur många steg som visas beror på arbetsflödesmodellens design.

1. Klicka **OK** för att bekräfta åtgärden.

### Delegera ett deltagarsteg {#delegating-a-participant-step}

Använd följande procedur för att delegera en arbetsuppgift.

1. Klicka på **Delegera** i det övre navigeringsfältet.
1. I dialogrutan använder du listrutan för att välja **Användare** att delegera arbetsuppgiften till. Du kan också lägga till en **Kommentar**.

   ![arbetsflödesdelegat](assets/workflowdelegate.png)

1. Klicka **OK** för att bekräfta åtgärden.

### Stega bakåt i ett deltagarsteg {#performing-step-back-on-a-participant-step}

Använd följande procedur för att stega bakåt.

1. Klicka på knappen Stega bakåt i det övre navigeringsfältet.
1. Välj Föregående steg i den dialogruta som visas, d.v.s. det steg som ska köras nästa gång, även om det är ett steg som inträffar tidigare i arbetsflödet. En nedrullningsbar lista visar alla lämpliga destinationer.

   ![screen_shot_2018-08-10at155325](assets/screen_shot_2018-08-10at155325.jpg)

1. Bekräfta åtgärden genom att klicka på OK.
