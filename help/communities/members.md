---
title: Hanteringskonsoler för medlemmar och grupper
description: Åtkomst till konsoler för hantering av medlemmar och grupper
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
role: Admin
exl-id: b64e24d2-8407-484c-8216-8d328ef5fa4f
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '913'
ht-degree: 0%

---


# Hanteringskonsoler för medlemmar och grupper {#members-groups-management-consoles}

## Ökning {#overview}

AEM Communities funktioner kräver ofta att besökarna är registrerade och inloggade innan de deltar i en community i publiceringsmiljön. Användarregistreringen behöver bara finnas i publiceringsmiljön och kallas vanligtvis *medlemmar* för att skilja dem från *användare* som är registrerade i författarmiljön.

### Medlemmar (användare) på Publish {#members-users-on-publish}

Med konsolerna Webbgruppsmedlemmar och -grupper kan medlemmar och medlemsgrupper som är registrerade i miljön *publish* skapas och hanteras från miljön *author* . Detta är bara möjligt när [tunneltjänsten](deploy-communities.md#tunnel-service-on-author) är aktiverad.

### Användare på författare {#users-on-author}

För att hantera användare och grupper som är registrerade i miljön *author* måste du använda plattformens säkerhetskonsol:

* Välj **[!UICONTROL Tools]** > **[!UICONTROL Security]** > **[!UICONTROL Users]** från global navigering.
* Välj **[!UICONTROL Tools]** > **[!UICONTROL Security]** > **[!UICONTROL Groups]** från global navigering.

>[!NOTE]
>
>När exempelinnehåll är distribuerat och aktiverat finns det många exempelanvändare i både författar- och publiceringsmiljöer. De här användarna kommer inte att vara närvarande när de körs med [inget exempelinnehåll, körningsläge](../../help/sites-administering/production-ready.md).

## Medlemskonsolen {#members-console}

I författarmiljön kan du nå Medlemskonsolen för att hantera medlemmar som är registrerade i publiceringsmiljön:

* Välj **[!UICONTROL Navigation]** > **[!UICONTROL Communities]** > **[!UICONTROL Members]** från global navigering

>[!CAUTION]
>
>Det går inte att använda medlemskonsolen om [tunneltjänsten](deploy-communities.md#tunnel-service-on-author) inte är aktiverad.

![Medlemskonsolen](assets/member-console1.png)

### Sök {#search-features}

Markera sidopanelsikonen till vänster om rubriken `Members` om du vill växla till att öppna söksidpanelen.

![Ikon för panelen Sök.](assets/leftpanel-icon.png)


![Filteralternativ för medlemskonsolen](assets/member-console2.png)

Välj sökikonen till vänster om rubriken `Members` om du vill växla panelen på söksidan till stängd.

### Medlemsstatistik {#member-statistics}

Kolumnerna som visar `Views`, `Posts`, `Follows` och `Likes` uppdateras när användaren är medlem i en eller flera communitywebbplatser med Adobe Analytics [enabled](sites-console.md#analytics).

### Exportera CSV {#export-csv}

Om du väljer länken `Export CSV` hämtas alla medlemmar som en lista med kommaavgränsade värden som är lämpliga för import till ett kalkylblad.

Kolumnrubrikerna är

`| Screen Name |Last Name |First Name |Status |Views |Posts |Follows |Likes |`

## Skapa ny medlem {#create-new-member}

Välj `Create Member` om du vill skapa en användare i publiceringsmiljön.

![Fönstret Skapa ny medlem](assets/create-member1.png)

### ALLMÄNT - Medlemsinformation {#general-member-details}

De flesta fält är valfria fält som medlemmen kan fylla i senare i sin profil.

* **[!UICONTROL ID]**

(*Obligatoriskt*) Det auktoriserbara ID:t är medlemmens inloggnings-ID.
Som standard är ID inställt på värdet för den e-postadress som krävs.
*När det har skapats kan ID:t inte ändras*.

* **[!UICONTROL Email Address]**

(*Obligatorisk*) Medlemmens e-postadress.
Medlemmen kan ändra sin e-postadress när profilen uppdateras.I
Om ID:t som standard är e-postadressen ändras *inte* när e-postadressen ändras.

* **[!UICONTROL Password]**

  (*Obligatoriskt*) Inloggningslösenordet.

* **[!UICONTROL Retype Password]**

  (*Obligatoriskt*) Ange lösenordet igen för verifiering.

* **[!UICONTROL Add Member to Sites]**

  (*Valfritt*) Välj bland befintliga communitysajter för att lägga till medlemmen i medlemsgruppen för communitywebbplatsen.

* **[!UICONTROL Add Member to Groups]**

  (*Valfritt*) Välj bland befintliga medlemsgrupper om du vill lägga till medlemmen i den gruppen.

* Välj **[!UICONTROL Save]**

### ALLMÄNT - Kontoinställningar {#general-account-settings}

Under Kontoinställningar kan en community-administratör:

* **[!UICONTROL Status]**
   * Banned
En medlem kan inte logga in, vilket förhindrar dem från att visa sidor eller delta i aktiviteter som kräver inloggning. De kan fortfarande anonymt besöka en öppen communitysajt.

   * Ej bannlyst
En medlem har fullständig åtkomst till communitywebbplatsen.

  Standardvärdet är `Not Banned`.

* **[!UICONTROL Contribution Limits]**

  Om det här alternativet är markerat är medlemmens möjlighet att publicera innehåll begränsad.
Standardvärdet beror på konfigurationen av bidragsgränser.
Se [Medlemmens bidragsgränser](limits.md).

* **[!UICONTROL Change Password]**

  En länk som finns när en befintlig medlem ändras. Ger en community-administratör möjlighet att återställa ett lösenord för en medlem.

### ALLMÄNT - Foto {#general-photo}

Om du vill ange en avatar för medlemmen börjar du med att markera **[!UICONTROL Upload Image]** och väljer en bild av typen .jpg, .png, .tif eller .gif. Bildens önskade storlek är 240 x 240 pixlar vid 72 dpi.

### ALLMÄNT - Lägg till medlem på webbplatser {#general-add-member-to-sites}

Medlemmen kan läggas till i en eller flera medlemsgrupper för en eller flera communityn. Börja med att ange text i textrutan.

### ALLMÄNT - Lägg till medlem i grupper {#general-add-member-to-groups}

Medlemmen kan läggas till i en eller flera medlemsgrupper. Börja med att ange text i textrutan.

### Fliken BADGES {#badges-tab}

På panelen `BADGES` kan du tilldela märken manuellt och återkalla dem. Märken kan vara till för tilldelade roller och märken som vanligtvis införskaffas.

Se även [Betygsättning och emblem](implementing-scoring.md).

![Fönstret Redigera medlemskapsinställningar](assets/create-member2.png)

* **[!UICONTROL Add badges]**
   * Börja skriva för att välja bland [tillgängliga märken](badges.md). När du har valt ett märke väljer du varje webbplats, eller alla webbplatser, där märket ska visas tillsammans med medlemmens avatar.
   * Flera märken och sajter kan väljas.
* **[!UICONTROL Remove badges]**
   * Markera papperskorgsikonen bredvid ett märke för att ta bort det.

## Konsolen Grupper {#groups-console}

Gruppkonsolen, som är tillgänglig från författarmiljön, gör det möjligt att skapa och hantera medlemsgrupper som är registrerade i publiceringsmiljön. Det är särskilt användbart för [Behöriga medlemsgrupper](users.md#privilegedmembersgroups).

Så här kommer du åt gruppkonsolen:
* Välj **[!UICONTROL Navigation]** > **[!UICONTROL Communities]** > **[!UICONTROL Groups]** från global navigering.

>[!CAUTION]
>
>Det går inte att använda gruppkonsolen om [tunneltjänsten](deploy-communities.md#tunnel-service-on-author) inte är aktiverad.

### Skapa ny grupp {#create-new-group}

Välj `Add Group` om du vill skapa en grupp i publiceringsmiljön.

![Fönstret Skapa ny grupp](assets/group-console1.png)

Följande fält krävs för att skapa en medlemsgrupp på publiceringssidan:

* **[!UICONTROL ID]**

  (*Obligatoriskt*) Gruppens unika ID.

  *När det har skapats kan ID:t inte ändras.*

* **[!UICONTROL Name]**

  (*Valfritt*) Gruppens visningsnamn.

  Standardvärdet är ID.

* **[!UICONTROL Description]**

  (*Valfritt*) En beskrivning av gruppens syfte och behörigheter.

* **[!UICONTROL Add Members To Group]**

  (*Valfritt*) Välj de medlemmar på publiceringssidan som ska inkluderas som initiala medlemmar i gruppen.

* Välj **[!UICONTROL Save]**

## Auktoriserade administratörer {#authorized-administrators}

När du arbetar med medlemmar i communitymedlemskonsolen måste du logga in som en användare med lämplig behörighet och replikeringsagenten som används av [tunneltjänsten](deploy-communities.md#tunnel-service-on-author) måste vara korrekt konfigurerad.

Om användaren inte är inloggad som `admin` måste den inloggade användaren vara medlem i användargruppen `administrators`.

Se även [Replikeringsagenter på författare](deploy-communities.md#replication-agents-on-author).
