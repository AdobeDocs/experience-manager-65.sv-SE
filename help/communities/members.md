---
title: Hanteringskonsoler för medlemmar och grupper
seo-title: Members & Groups Management Consoles
description: Åtkomst till konsoler för hantering av medlemmar och grupper
seo-description: How to access Members and Groups Management consoles
uuid: 2e93e861-a066-4189-91db-f8b784bc5aea
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: ccabf301-b417-48aa-8501-8360fd9f3e36
role: Admin
exl-id: b64e24d2-8407-484c-8216-8d328ef5fa4f
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '905'
ht-degree: 0%

---

# Hanteringskonsoler för medlemmar och grupper {#members-groups-management-consoles}

## Översikt {#overview}

AEM Communities funktioner kräver ofta att besökarna är registrerade och inloggade innan de deltar i en community i publiceringsmiljön. Användarregistreringen behöver bara finnas i publiceringsmiljön och kallas ofta för *medlemmar* att skilja dem från *användare* som registrerats i författarmiljön.

### Medlemmar (användare) vid publicering {#members-users-on-publish}

Använda konsolerna Communities Members and Groups, medlemmar och medlemsgrupper som är registrerade i *publicera* kan skapas och hanteras från *författare* miljö. Detta är bara möjligt om [tunneltjänst](deploy-communities.md#tunnel-service-on-author) är aktiverat.

### Användare på författare {#users-on-author}

För hantering av användare och grupper som är registrerade i *författare* -miljön är nödvändig för att använda plattformens säkerhetskonsol:

* Från global navigering väljer du **[!UICONTROL Tools]** > **[!UICONTROL Security]** > **[!UICONTROL Users]**.
* Från global navigering väljer du **[!UICONTROL Tools]** > **[!UICONTROL Security]** > **[!UICONTROL Groups]**.

>[!NOTE]
>
>När exempelinnehåll är distribuerat och aktiverat finns det många exempelanvändare i både författar- och publiceringsmiljöer. De här användarna kommer inte att vara närvarande när de körs med [nosamplingInnehåll, körningsläge](../../help/sites-administering/production-ready.md).

## Medlemskonsolen {#members-console}

I författarmiljön kan du nå Medlemskonsolen för att hantera medlemmar som är registrerade i publiceringsmiljön:

* Från global navigering väljer du **[!UICONTROL Navigation]** > **[!UICONTROL Communities]** > **[!UICONTROL Members]**

>[!CAUTION]
>
>Det går inte att använda medlemskonsolen om [tunneltjänst](deploy-communities.md#tunnel-service-on-author) är inte aktiverat.

![member-console1](assets/member-console1.png)

### Sökning {#search-features}

Markera sidpanelsikonen till vänster på sidan `Members` för att växla mellan att öppna panelen på söksidan.

![](assets/leftpanel-icon.png)


![member-console2](assets/member-console2.png)

Välj sökikonen till vänster i dialogrutan `Members` för att växla till att växla panelen på söksidan stängd.

### Medlemsstatistik {#member-statistics}

Kolumnerna som visas `Views`, `Posts`, `Follows` och `Likes` uppdateras när användaren är medlem i en eller flera communitysajter med Adobe Analytics [aktiverad](sites-console.md#analytics).

### Exportera CSV {#export-csv}

Markera `Export CSV` leder till att alla medlemmar hämtas som en lista med kommaavgränsade värden som är lämpliga för import till ett kalkylblad.

Kolumnrubrikerna är

`| Screen Name |Last Name |First Name |Status |Views |Posts |Follows |Likes |`

## Skapa ny medlem {#create-new-member}

Välj `Create Member` för att skapa en användare i publiceringsmiljön.

![create-member1](assets/create-member1.png)

### ALLMÄNT - Medlemsinformation {#general-member-details}

De flesta fält är valfria fält som medlemmen kan fylla i senare i sin profil.

* **[!UICONTROL ID]**

(*Obligatoriskt*) Behörighetsbart ID är medlemmens inloggnings-ID.
Som standard är ID inställt på värdet för den e-postadress som krävs.
*När ID:t har skapats får det inte ändras*.

* **[!UICONTROL Email Address]**

(*Obligatoriskt*) Medlemmens e-postadress.
Medlemmen kan ändra sin e-postadress när profilen uppdateras.I Om ID:t som standard är e-postadressen, kommer ID:t att *not* ändras när e-postadressen ändras.

* **[!UICONTROL Password]**

   (*Obligatoriskt*) Inloggningslösenordet.

* **[!UICONTROL Retype Password]**

   (*Obligatoriskt*) Ange lösenordet igen för verifiering.

* **[!UICONTROL Add Member to Sites]**

   (*Valfritt*) Välj bland befintliga communitysajter för att lägga till medlemmen i communityplatsens medlemsgrupp.

* **[!UICONTROL Add Member to Groups]**

   (*Valfritt*) Välj bland befintliga medlemsgrupper för att lägga till medlemmen i gruppen.

* Välj **[!UICONTROL Save]**

### ALLMÄNT - Kontoinställningar {#general-account-settings}

Under Kontoinställningar kan en community-administratör:

* **[!UICONTROL Status]**
   * Banned En medlem kan inte logga in, vilket förhindrar dem från att visa sidor eller delta i aktiviteter som kräver inloggning. De kan fortfarande anonymt besöka en öppen communitysajt.

   * Ej förbjuden En medlem har fullständig åtkomst till communitywebbplatsen.

   Standard är `Not Banned`.

* **[!UICONTROL Contribution Limits]**

   Om det här alternativet är markerat är medlemmens möjlighet att publicera innehåll begränsad.
Standardvärdet beror på konfigurationen av bidragsgränser.
Se [Gränser för medlemsbidrag](limits.md).

* **[!UICONTROL Change Password]**

   En länk som finns när en befintlig medlem ändras. Ger en community-administratör möjlighet att återställa ett lösenord för en medlem.

### ALLMÄNT - Foto {#general-photo}

Börja med att välja en avatar för medlemmen **[!UICONTROL Upload Image]** och väljer en bild av typen .jpg, .png, .tif eller .gif. Den rekommenderade storleken för en bild är 240 x 240 pixlar vid 72 dpi.

### ALLMÄNT - Lägg till medlem på webbplatser {#general-add-member-to-sites}

Medlemmen kan läggas till i en eller flera medlemsgrupper för en eller flera communityplatser. Börja med att ange text i textrutan.

### ALLMÄNT - Lägg till medlem i grupper {#general-add-member-to-groups}

Medlemmen kan läggas till i en eller flera medlemsgrupper. Börja med att ange text i textrutan.

### Fliken BADGES {#badges-tab}

The `BADGES` kan du tilldela och återkalla märken manuellt. Märken kan användas för tilldelade roller samt för märken som vanligtvis används.

Se även [Betygsättning och emblem](implementing-scoring.md).

![create-member2](assets/create-member2.png)

* **[!UICONTROL Add badges]**
   * Börja skriva för att välja bland [tillgängliga märken](badges.md). När du har valt ett märke väljer du varje webbplats, eller alla webbplatser, där märket ska visas tillsammans med medlemmens avatar.
   * Flera märken och sajter kan väljas.
* **[!UICONTROL Remove badges]**
   * Markera papperskorgsikonen bredvid ett märke för att ta bort det.

## Konsolen Grupper {#groups-console}

Gruppkonsolen, som är tillgänglig från författarmiljön, gör det möjligt att skapa och hantera medlemsgrupper som är registrerade i publiceringsmiljön. Det är särskilt användbart för
* [Behöriga medlemsgrupper](users.md#privilegedmembersgroups)
* Gruppbaserad tilldelning av [aktiveringsresurser](resources.md)

Så här kommer du åt gruppkonsolen:
* Från global navigering väljer du **[!UICONTROL Navigation]** > **[!UICONTROL Communities]** > **[!UICONTROL Groups]**.

>[!CAUTION]
>
>Det går inte att använda gruppkonsolen om [tunneltjänst](deploy-communities.md#tunnel-service-on-author) är inte aktiverat.

### Skapa ny grupp {#create-new-group}

Välj `Add Group` för att skapa en grupp i publiceringsmiljön.

![group-console1](assets/group-console1.png)

Följande fält krävs för att skapa en ny medlemsgrupp på publiceringssidan:

* **[!UICONTROL ID]**

   (*Obligatoriskt*) Gruppens unika ID.

   *När ID:t har skapats kan det inte ändras.*

* **[!UICONTROL Name]**

   (*Valfritt*) Gruppens visningsnamn.

   Standardvärdet är ID.

* **[!UICONTROL Description]**

   (*Valfritt*) En beskrivning av gruppens syfte och behörigheter.

* **[!UICONTROL Add Members To Group]**

   (*Valfritt*) Välj medlemmar på publiceringssidan som ska inkluderas som initiala medlemmar i gruppen.

* Välj **[!UICONTROL Save]**

## Auktoriserade administratörer {#authorized-administrators}

När du arbetar med medlemmar i Communities-medlemskonsolen måste du logga in som en användare med lämplig behörighet och för den replikeringsagent som används av [tunneltjänst](deploy-communities.md#tunnel-service-on-author) att konfigureras korrekt.

Om inte inloggad som `admin`måste den inloggade användaren vara medlem i `administrators` användargrupp.

Se även [Replikeringsagenter på författare](deploy-communities.md#replication-agents-on-author).
