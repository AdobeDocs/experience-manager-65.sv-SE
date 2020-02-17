---
title: Konfigurera inställningar för frånvaro
seo-title: Konfigurera inställningar för frånvaro
description: Konfigurera inställningar för frånvaro
seo-description: Konfigurera inställningar för frånvaro
translation-type: tm+mt
source-git-commit: 52e4564ecab61cedaf3aca3d10339f6bcee2f71e

---



# Konfigurera frånvaroinställningar {#configure-out-of-office-settings}

Om du tänker vara utanför kontoret kan du ange vad som ska hända med artiklar som har tilldelats dig för den perioden.

Du kan ange startdatum och -tid och slutdatum och sluttid så att dina inställningar som inte är på kontoret börjar gälla. Om du befinner dig i en annan tidszon än servern används den tidszon som klienten använder.

Du kan ange en standardperson som alla dina objekt skickas till. Du kan också ange undantag för objekt från specifika processer som ska skickas till en annan användare eller behållas i inkorgen tills du kommer tillbaka. Om den utsedda personen även är utanför kontoret, skickas objektet till användaren som han/hon har utsett. Om objektet inte kan tilldelas till en användare som inte är utanför kontoret finns objektet kvar i din inkorg.

Du kan dela upp objektdelegering baserat på arbetsflödesmodellerna. Du kan till exempel tilldela ett objekt som är relaterat till arbetsflöde A till användare A och tilldela ett objekt som är relaterat till arbetsflöde B till användare B.


>[!NOTE]
>
> * När du aktiverar inställningen Frånvarande finns alla objekt som är tillgängliga i Inkorgen, innan inställningen aktiveras, kvar i Inkorgen. Endast objekt som tagits emot efter att inställningen aktiverats delegeras.
> * När du inaktiverar inställningen Frånvarande tilldelas de delegerade objekten inte tillbaka till dig automatiskt. Du kan använda anspråksfunktionen för att tilldela objekt till dig.
> * När Användare A delegerar objekt till Användare B och Användare B delegerar vidare till Användare C, tilldelas objekten bara Användare C och inte Användare B.
> * När det finns en slinga i uppdraget stannar uppgifterna kvar hos den ursprungliga användaren. När Användare A till exempel delegerar objekt till Användare B till Användare C, Användare C delegerar till Användare D och Användare D delegerar till Användare B skapas en slinga. I sådana fall behålls objektet av den ursprungliga användaren. Användare A är ursprunglig användare i ovanstående exempel.


## Aktivera inställningen Frånvarande för ditt konto {#enable-out-of-office}

Utför följande steg för att aktivera inställningen Frånvarande för ditt konto och delegera dina inkorgsobjekt till en annan användare:

1. Logga in på din AEM-instans. Tryck på ikonen ![Inkorg](assets/bell.svg) och tryck på **[!UICONTROL Visa alla]**. En lista över dina inkorgsobjekt visas.
1. Tryck på ikonen ![Visa väljare](assets/viewlist.svg) eller ![Visa väljare](assets/calendar.svg) bredvid knappen **[!UICONTROL Skapa]** och tryck sedan på **[!UICONTROL Inställningar]**. Dialogrutan Inställningar visas.
1. Öppna fliken **[!UICONTROL Frånvarande]** i dialogrutan med inställningar.
1. Tryck på knappen **[!UICONTROL Aktivera/inaktivera]** för att aktivera inställningen Frånvarande.
1. Ange **[!UICONTROL starttid]** och **[!UICONTROL sluttid]** för inställningen. Objekten delegeras endast under den angivna perioden. Lämna fältet **[!UICONTROL Sluttid]** tomt om du vill delegera objekt för en obegränsad tidsperiod.
1. Markera kryssrutan **[!UICONTROL Vidarebefordra mina objekt under den här perioden]** . Om du inte markerar alternativet och inte anger en tilldelad användare, vidarebefordras inte objekten till någon användare. Även om du är borta och inställningen är aktiverad finns objekten kvar i Inkorgen.
1. Tryck på **[!UICONTROL Lägg till tilldelad]**. Ange en användare i fältet **[!UICONTROL Tilldelning]** som objekten ska delegeras till. Ange den **[!UICONTROL arbetsflödesmodell]** som ska delegeras till den angivna användaren. Du kan välja mer än en arbetsflödesmodell.

   Om du dessutom vill tilldela alla objekt, oavsett arbetsflödesmodell, till en viss användare väljer du **[!UICONTROL Alla arbetsflöden]** i listrutan Arbetsflödesmodell. <br>

   Om du vill tilldela objekt till en viss användare för alla arbetsflödesmodeller utom ett fåtal, väljer du **[!UICONTROL Alla arbetsflöden]** i listrutan Arbetsflödesmodell, trycker på **[!UICONTROL + Lägg till undantag]**och anger vilka arbetsflödesmodeller som ska utelämnas.
   <br>

   Upprepa steget för att lägga till fler tilldelningar. <br>

   [!NOTE]
   >Tilldelningsordningen är viktig. När ett objekt tilldelas en användare som har aktiverat inställningen Frånvarande utvärderas objektet mot den angivna listan över tilldelningar i den ordning som tilldelningarna läggs till. När ett objekt matchar villkoret tilldelas det till den som tilldelats objektet och nästa tilldelande kontrolleras inte.

1. Tryck på **[!UICONTROL Spara]**. Inställningen börjar gälla vid angivet startdatum och angiven starttid. Om du loggar in när du inte är på kontoret beaktas du inte på kontoret förrän du ändrar dina inställningar.

Nu tilldelas objekt som du har tilldelats under frånvaroperioden automatiskt till den angivna tilldelade personen.\
![Utanför kontoret](assets/out-of-office.png)

[!NOTE]
>(Endast för formulärbaserade arbetsflödesobjekt) Aktivera alternativet **Tillåt att tilldelad delegerar med alternativet** Frånvarande i steget **Tilldela uppgift** i arbetsflödet. Endast objekt som har det ovannämnda alternativet aktiverat delegeras till andra användare.
> 
## Begränsningar {#limitations}

* Det går inte att tilldela objekt till en grupp.
* Det går för närvarande inte att aktivera frånvaro för projektaktiviteter.
