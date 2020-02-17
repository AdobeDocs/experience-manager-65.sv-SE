---
title: Ursprungligt sandlådeinnehåll
seo-title: Ursprungligt sandlådeinnehåll
description: Skapa innehåll
seo-description: Skapa innehåll
uuid: 9810fe47-8d1a-4238-9b9c-0cc47c63d97a
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: e8f28cd5-7950-4aab-bf62-3d4ed3d33cbd
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Ursprungligt sandlådeinnehåll {#initial-sandbox-content}

I det här avsnittet skapar du följande sidor som alla använder [sidmallen](initial-app.md#createthepagetemplate):

* SCF Sandbox Site, som dirigerar om till den engelska versionen av huvudsidan

   * SCF Sandbox - Huvudsidan för den engelska versionen av webbplatsen

      * SCF Play - Underordnad den huvudsida som ska spelas upp

Även om den här självstudiekursen inte omfattar [språkkopior](../../help/sites-administering/tc-prep.md)är den utformad så att rotsidan kan implementera identifiering av det språk som användaren föredrar via HTML-rubriken och dirigera om till rätt huvudsida för språket. Konventionen är att använda landskoden med två bokstäver för sidans nodnamn, t.ex. &quot;en&quot; för engelska, &quot;fr&quot; för franska och så vidare.

## Skapa första sidor {#create-first-pages}

Nu när det finns en [sidmall](initial-app.md#createthepagetemplate)kan vi skapa webbplatsens rotsida i katalogen /content.

1. Standardgränssnittet innehåller för närvarande utkast för att skapa webbplatser. Det klassiska användargränssnittet är användbart eftersom den här självstudiekursen skapar en enkel webbplats.

   Om du vill växla till det klassiska användargränssnittet väljer du global navigering och håller pekaren över den högra sidan av projektikonen. Välj ikonen *Växla till klassiskt gränssnitt* som visas:

   ![chlimage_1-36](assets/chlimage_1-36.png)

   Möjligheten att växla till det klassiska användargränssnittet måste [aktiveras av en administratör](../../help/sites-administering/enable-classic-ui.md).

1. På den [klassiska användargränssnittets välkomstsida](http://localhost:4502/welcome.html)väljer du **[!UICONTROL Webbplatser]**.

   ![chlimage_1-37](assets/chlimage_1-37.png)

   Du kan även få tillgång till det klassiska användargränssnittet för webbplatser direkt genom att gå till [/siteAdmin.](http://localhost:4502/siteadmin)

1. Välj **[!UICONTROL Webbplatser]** i utforskarrutan och välj sedan **[!UICONTROL Ny > Ny sida]** i verktygsfältet.

   Ange följande i dialogrutan **[!UICONTROL Skapa sida]** :

   * Titel: `SCF Sandbox Site`
   * Namn: `an-scf-sandbox`
   * Välj **[!UICONTROL en SCF-sandlådeuppspelningsmall]**
   * Klicka på **[!UICONTROL Skapa]**
   ![chlimage_1-38](assets/chlimage_1-38.png)

1. Markera den sida du just skapade i Utforskarfönstret `/Websites/SCF Sandbox Site`och klicka på **[!UICONTROL Ny > Ny sida]**:

   * Titel: `SCF Sandbox`
   * Namn: `en`
   * Välj **en SCF-sandlådeuppspelningsmall **
   * Klicka på **Skapa **

1. Markera den sida du just skapade i Utforskarfönstret `/Websites/SCF Sandbox Site/SCF Sandbox`och klicka på **[!UICONTROL Ny > Ny sida]**

   * Titel: `SCF Play`
   * Namn: `play`
   * Välj **[!UICONTROL en SCF-sandlådeuppspelningsmall]**
   * Klicka på **[!UICONTROL Skapa]**

1. Så här visas webbplatsen nu i webbplatskonsolen. Observera att underordnade sidor för objektet som är markerat i utforskarrutan visas i den högra rutan där de kan hanteras.

   ![chlimage_1-39](assets/chlimage_1-39.png)

   Det här är databasvyn över vad som har skapats med webbplatsverktyget och mallen:

   ![chlimage_1-40](assets/chlimage_1-40.png)

## Lägg till designbanan {#add-the-design-path}

Egenskapen &quot; ` [/etc/designs/an-scf-sandbox](setup-website.md#setupthedesigntreeetcdesigns)`

* `cq:template="/libs/wcm/core/templates/designpage"`

har definierats, vilket ger möjlighet att referera till designresurser i ett skript med `currentDesign.getPath()`. Exempel

* &lt;% String favIcon = currentDesign.getPath() + &quot;/favicon.ico&quot;; %>


   * Namn: `cq:designPath`
   * Typ: `String`
   * Värde: `/etc/designs/an-scf-sandbox`

* Klicka på den gröna `[+] Add`

Databasen ska vara som följer:

![chlimage_1-41](assets/chlimage_1-41.png)

* Klicka på **[!UICONTROL Spara alla]**

[ Svårt att spara? Återinloggning! ]

>[!NOTE]
>
>Det är valfritt att använda cq:designPath och det har inget samband med [användningen av clientlibs](develop-app.md#includeclientlibsintemplate), vilket i huvudsak krävs eftersom SCF-komponenterna använder [klientlibs](client-customize.md#clientlibs-for-scf) för att hantera sina JS- och CSS-filer.

