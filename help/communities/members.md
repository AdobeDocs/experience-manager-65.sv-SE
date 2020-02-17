---
title: Hanteringskonsoler för medlemmar och grupper
seo-title: Hanteringskonsoler för medlemmar och grupper
description: Åtkomst till konsoler för hantering av medlemmar och grupper
seo-description: Åtkomst till konsoler för hantering av medlemmar och grupper
uuid: 2e93e861-a066-4189-91db-f8b784bc5aea
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: ccabf301-b417-48aa-8501-8360fd9f3e36
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Hanteringskonsoler för medlemmar och grupper {#members-groups-management-consoles}

## Översikt {#overview}

Funktionerna i AEM Communities kräver ofta att besökarna är registrerade och inloggade innan de deltar i en community i publiceringsmiljön. Användarregistreringen behöver bara finnas i publiceringsmiljön och kallas ofta *medlemmar* för att skilja dem från *användare* som är registrerade i författarmiljön.

### Medlemmar (användare) vid publicering {#members-users-on-publish}

Med konsolerna Communities Members and Groups kan medlemmar och medlemsgrupper som är registrerade i *publiceringsmiljön* skapas och hanteras från *författarmiljön* . Detta är bara möjligt när [tunneltjänsten](deploy-communities.md#tunnel-service-on-author) är aktiverad.

### Användare på författare {#users-on-author}

För att hantera användare och grupper som är registrerade i *författarmiljön* måste du använda plattformens säkerhetskonsol:

* Välj `Tools, Security, Users`
* Välj `Tools, Security, Groups`

>[!NOTE]
>
>När exempelinnehåll är distribuerat och aktiverat finns det många exempelanvändare i både författar- och publiceringsmiljöer. De här användarna kommer inte att vara närvarande när de körs med [inget innehållskörningsläge](../../help/sites-administering/production-ready.md).

## Medlemskonsolen {#members-console}

I författarmiljön kan du nå Medlemskonsolen för att hantera medlemmar som är registrerade i publiceringsmiljön:

* Från global navigering: **[!UICONTROL Navigering > Communities > Members]**

>[!CAUTION]
>
>Det går inte att använda medlemskonsolen om [tunneltjänsten](deploy-communities.md#tunnel-service-on-author) inte är aktiverad.

![chlimage_1-119](assets/chlimage_1-119.png)

### Sök {#search-features}

Markera sidopanelsikonen till vänster om sidhuvudet för att växla mellan att öppna panelen för söksidan `Members` .

![chlimage_1-120](assets/chlimage_1-120.png) ![chlimage_1-121](assets/chlimage_1-121.png)

Välj sökikonen till vänster om sidhuvudet för att växla mellan att `Members` växla panelen på söksidan till stängd.

### Medlemsstatistik {#member-statistics}

Kolumnerna som visas `Views`, `Posts`och `Follows`uppdateras när användaren är medlem i en eller flera communitywebbplatser med Adobe Analytics `Likes` aktiverat [](sites-console.md#analytics).

### Exportera CSV {#export-csv}

Om du markerar `Export CSV` länken hämtas alla medlemmar som en lista med kommaavgränsade värden som är lämpliga för import till ett kalkylblad.

Kolumnrubrikerna är

`| Screen Name |Last Name |First Name |Status |Views |Posts |Follows |Likes |`

## Skapa ny medlem {#create-new-member}

Välj `Create Member` för att skapa en användare i publiceringsmiljön.

![chlimage_1-122](assets/chlimage_1-122.png)

### ALLMÄNT - Medlemsinformation {#general-member-details}

De flesta fält är valfria fält som medlemmen kan fylla i senare i sin profil.

* **[!UICONTROL ID]**(*obligatoriskt*) Det auktoriserbara ID:t är medlemmens inloggnings-ID.
Som standard är ID inställt på värdet för den e-postadress som krävs.
   *När ID:t har skapats kan det inte ändras.*

* **[!UICONTROL E-postadress]**(*obligatoriskt*) Medlemmens e-postadress.
Medlemmen kan ändra sin e-postadress när profilen uppdateras.Om ID:t som är standard för e-postadressen ändras *inte* ID:t när e-postadressen ändras.

* **[!UICONTROL Lösenord]**(*obligatoriskt*) Inloggningslösenordet.

* **[!UICONTROL Skriv lösenordet]** igen (*obligatoriskt*). Ange lösenordet igen för verifiering.

* **[!UICONTROL Lägg till medlem i platser]**(*valfritt*) Välj bland befintliga communityplatser för att lägga till medlemmen i medlemsgruppen för communitywebbplatsen.

* **[!UICONTROL Lägg till medlem i grupper]**(*valfritt*) Välj bland befintliga medlemsgrupper för att lägga till medlemmen i den gruppen.

* Välj **[!UICONTROL Spara]**

### ALLMÄNT - Kontoinställningar {#general-account-settings}

Under Kontoinställningar kan en community-administratör

* **[!UICONTROL Status]**
   * BannedEn medlem kan inte logga in, vilket förhindrar dem från att visa sidor eller delta i aktiviteter som kräver inloggning. De kan fortfarande anonymt besöka en öppen communitysajt.

   * Inte BannedEn medlem har fullständig åtkomst till communitywebbplatsen.
   Standardvärdet är `Not Banned`.

* **[!UICONTROL Bidragsgränser]**Om det här alternativet är markerat är medlemmens möjlighet att publicera innehåll begränsad.
Standardvärdet beror på konfigurationen av bidragsgränser.
Se Gränser för [medlemsbidrag](limits.md).

* **[!UICONTROL Ändra lösenord]** En länk som finns när en befintlig medlem ändras. Ger en community-administratör möjlighet att återställa ett lösenord för en medlem.

### ALLMÄNT - Foto {#general-photo}

Om du vill ange en avatar för medlemmen börjar du med att välja **[!UICONTROL Överför bild]** och väljer en bild av typen .jpg, .png, .tif eller .gif. Den rekommenderade storleken för en bild är 240 x 240 pixlar vid 72 dpi.

### ALLMÄNT - Lägg till medlem på webbplatser {#general-add-member-to-sites}

Medlemmen kan läggas till i en eller flera medlemsgrupper för en eller flera communityplatser. Börja med att ange text i textrutan.

### ALLMÄNT - Lägg till medlem i grupper {#general-add-member-to-groups}

Medlemmen kan läggas till i en eller flera medlemsgrupper. Börja med att ange text i textrutan.

### Fliken BADGES {#badges-tab}

På `BADGES` panelen kan du tilldela och återkalla märken manuellt. Märken kan användas för tilldelade roller samt för märken som vanligtvis används.

Se även [Betygsättning och badges](implementing-scoring.md).

![chlimage_1-123](assets/chlimage_1-123.png)

* **[!UICONTROL Lägg till emblem]**
   * Börja skriva för att välja bland [tillgängliga märken](badges.md). När du har valt ett märke väljer du varje webbplats, eller alla webbplatser, där märket ska visas tillsammans med medlemmens avatar.
   * Flera märken och sajter kan väljas.
* **[!UICONTROL Ta bort emblem]**
   * Markera papperskorgsikonen bredvid ett märke för att ta bort det

## Konsolen Grupper {#groups-console}

Gruppkonsolen, som är tillgänglig från författarmiljön, gör det möjligt att skapa och hantera medlemsgrupper som är registrerade i publiceringsmiljön. Det är särskilt användbart för
* [Behöriga medlemsgrupper](users.md#privilegedmembersgroups)
* Gruppbaserad tilldelning av [aktiveringsresurser](resources.md)

Så här kommer du åt gruppkonsolen:
* Från global navigering: **[!UICONTROL Navigering > Communities > Groups]**

>[!CAUTION]
>
>Det går inte att använda gruppkonsolen om [tunneltjänsten](deploy-communities.md#tunnel-service-on-author) inte är aktiverad.

### Skapa ny grupp {#create-new-group}

Välj `Add Group` för att skapa en grupp i publiceringsmiljön.

![chlimage_1-124](assets/chlimage_1-124.png)

Följande fält krävs för att skapa en ny medlemsgrupp på publiceringssidan:

* **[!UICONTROL ID]**(*obligatoriskt*) Gruppens unika ID.
   *När ID:t har skapats kan det inte ändras.*

* **[!UICONTROL Namn]**(*valfritt*) Gruppens visningsnamn.

   Standardvärdet är ID.

* **[!UICONTROL Beskrivning]**(*valfritt*) En beskrivning av gruppens syfte och behörigheter.

* **[!UICONTROL Lägg till medlemmar i grupp]**(*valfritt*) Välj medlemmar på publiceringssidan som ska inkluderas som ursprungliga medlemmar i gruppen.

* Välj **[!UICONTROL Spara]**

## Auktoriserade administratörer {#authorized-administrators}

När du arbetar med medlemmar i communitymedlemskonsolen måste du logga in som en användare med lämplig behörighet och replikeringsagenten som används av [tunneltjänsten](deploy-communities.md#tunnel-service-on-author) måste vara korrekt konfigurerad.

Om användaren inte är inloggad som `admin`måste användaren vara medlem i `administrators` användargruppen.

Se även [Replikeringsagenter på författare](deploy-communities.md#replication-agents-on-author).
