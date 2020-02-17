---
title: Konfigurera delade köer
seo-title: Konfigurera delade köer
description: Lär dig hur du använder delade köer för formulärbaserade arbetsflöden i AEM Forms på OSGi.
seo-description: Lär dig hur du använder delade köer för formulärbaserade arbetsflöden i AEM Forms på OSGi.
uuid: null
topic-tags: process
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: null
docset: aem65
translation-type: tm+mt
source-git-commit: 9a250e739adcf094856f1eafa75de2649d6d3d5f

---


# Dela och begära åtkomst till inkorgsobjekt från en användare {#share-and-request-access}

En kö är en lista med objekt i AEM Inbox för en användare. Dessa kan vara objekt som tilldelats en användare eller objekt som delas med gruppen som en användare är medlem i. Du kan öppna Inkorgen för att visa och utföra åtgärder på Inkorgsobjektet. Du kan till exempel dela ett objekt med en annan användare.

Du kan också dela dina inkorgsobjekt med en annan användare. När en annan användare har åtkomst till dina inkorgsobjekt kan användaren göra anspråk på och vidta lämpliga åtgärder för delade objekt. På samma sätt kan du begära åtkomst till inkorgsobjekt från andra användare.

## Krav {#pre-requisites}

Den inloggade användaren måste vara medlem i `workflow-users` gruppen. Användaren kan bara dela objekt eller begära åtkomst till objekt från de användare som den inloggade användaren har läsbehörighet till eller bara från de användare som har aktiverat den offentliga profilen.

## Dela en enskild eller alla objekt i inkorgen med en annan användare

Med AEM Inbox kan du dela ett eller alla objekt i din inkorg med en annan användare.

### Dela alla inkorgsobjekt

Så här delar du alla objekt i en inkorg med en annan användare:

1. Logga in på din AEM-instans. Tryck på ikonen ![Inkorg](assets/bell.svg) och tryck på **[!UICONTROL Visa alla]**. En lista över dina inkorgsobjekt visas.
1. Tryck på ikonen ![Visa väljare](assets/viewlist.svg) eller ![Visa väljare](assets/calendar.svg) bredvid knappen **[!UICONTROL Skapa]** och tryck sedan på **[!UICONTROL Inställningar]**. Dialogrutan Inställningar visas.
1. Öppna fliken **[!UICONTROL Dela]** i inställningsdialogrutan.
1. Ange namnet på en användare i textrutan **[!UICONTROL Bevilja åtkomst för dina inkorgsobjekt]** och tryck på **[!UICONTROL Bevilja]**. Upprepa steget för att lägga till fler användare. Alla användare som har åtkomst till dina objekt visas under **Användarnamn** .
1. Tryck på **[!UICONTROL Spara]**.

>[!NOTE]
>
> (Endast för formulärbaserade arbetsflödesobjekt) Aktivera alternativet **[Tillåt att tilldelad kan dela via Inkorgsdelning](aem-forms-workflow-step-reference.md)**i steget **Tilldela uppgift**i arbetsflödet. Endast objekt som har det ovannämnda alternativet aktiverat visas för andra användare.

### Dela enskilda objekt

Så här delar du ett Inkorgsobjekt med en annan användare:

1. Logga in på din AEM-instans. Tryck på ikonen ![Inkorg](assets/bell.svg) och tryck på **[!UICONTROL Visa alla]**. En lista över dina inkorgsobjekt visas.
1. Markera ett objekt och tryck på **[!UICONTROL Dela]**. En dialogruta visas.
1. Ange namnet på en användare i textrutan Lägg till användare för att dela det här objektet och tryck på **[!UICONTROL Lägg till]**. Upprepa steget för att lägga till fler användare. Alla användare som har åtkomst till dina objekt visas under **[!UICONTROL Användarnamn]** .
1. Tryck på **[!UICONTROL Spara]**.


>[!NOTE]
>
> (Endast för formulärbaserade arbetsflödesobjekt) Aktivera alternativet **[Tillåt att tilldelad delar explicit i Inkorgen](aem-forms-workflow-step-reference.md)**i steget **Tilldela uppgift**i arbetsflödet. Endast objekt som har det ovannämnda alternativet aktiverat visas för andra användare.

## Begär åtkomst till inkorgsobjekt {#request-access}

Du kan begära åtkomst till inkorgsobjekten för en annan användare. När åtkomsten har beviljats kan du visa, göra anspråk på och vidta lämpliga åtgärder för delade objekt. Utför följande steg för att begära åtkomst till inkorgsobjekt från en annan användare:

1. Logga in på din AEM-instans. Tryck på ikonen ![Visa väljare](assets/bell.svg) och tryck på **[!UICONTROL Visa alla]**.
1. Tryck på ikonen ![Visa väljare](assets/viewlist.svg) eller ![Visa väljare](assets/calendar.svg) bredvid knappen **[!UICONTROL Skapa]** och tryck sedan på **[!UICONTROL Inställningar]**. Dialogrutan Inställningar visas.
1. Ange namnet på en användare i textrutan **[!UICONTROL Begär åtkomst till inkorgsobjekt för användaren]** och tryck på **[!UICONTROL Begär]**. En begäran skickas till användaren och status för begäran visas mot användarens namn. Upprepa steget för att lägga till fler användare.
1. Tryck på **[!UICONTROL Spara]**. Begäran skickas som ett inkorgsobjekt till användarna. Användaren kan markera objektet och trycka på Godkänn eller Avvisa för att bevilja eller avvisa åtkomsten.


## Göra anspråk på objekt som delas av andra användare {#claim-items}

Du kan bara börja arbeta med ett delat objekt efter att du har gjort anspråk på det. Det förhindrar att flera användare arbetar med ett enda objekt. Utför följande steg för att göra anspråk på ett objekt:

1. Logga in på din AEM-instans. Tryck på ikonen Inkorg ![Inkorg](assets/bell.svg) och tryck på **[!UICONTROL Visa alla]**.
1. Tryck på ikonen ![Endast](assets/railleft.svg) innehåll för att öppna filterväljaren.
1. Tryck på listrutan **[!UICONTROLSVälj tilldelad]** för att visa och markera användare som har delat sina inkorgsobjekt med dig.
1. Markera ett objekt och tryck på **[!UICONTROL Claim]**. Objektet läggs till i din inkorg.

## Frisläpp begärda artiklar {#release-items}

Du kan bara arbeta med ett delat objekt efter att du har gjort anspråk på det. Andra användare kan inte se eller arbeta med objekt som du har gjort anspråk på. Om du inte kan fortsätta arbeta med ett objekt kan du släppa det i poolen igen.   När du har släppt objektet kan andra göra anspråk på och arbeta med det:

Utför följande steg för att frigöra ett objekt:

1. Logga in på din AEM-instans. Tryck på ikonen Inkorg ![Inkorg](assets/bell.svg) och tryck på **[!UICONTROL Visa alla]**. En lista över dina inkorgsobjekt visas.
1. Markera objektet som ska frisläppas och tryck på **[!UICONTROL UnnClaim]**. Objektet läggs till i poolen igen. Andra kan nu göra anspråk på objektet.

## Begränsningar {#limitations}

* Det går inte att dela objekt med en grupp.
* Delning av projektaktiviteter stöds inte.
