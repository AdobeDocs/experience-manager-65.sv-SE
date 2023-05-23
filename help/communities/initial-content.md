---
title: Ursprungligt sandlådeinnehåll
seo-title: Initial Sandbox Content
description: Skapa innehåll
seo-description: Create content
uuid: 9810fe47-8d1a-4238-9b9c-0cc47c63d97a
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: e8f28cd5-7950-4aab-bf62-3d4ed3d33cbd
exl-id: 068a0fff-ca48-4847-ba3f-d78416c97f6d
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '434'
ht-degree: 2%

---

# Ursprungligt sandlådeinnehåll {#initial-sandbox-content}

I det här avsnittet skapar du följande sidor som alla använder [sidmall](initial-app.md#createthepagetemplate):

* SCF Sandbox Site, som dirigerar om till den engelska versionen av huvudsidan.

   * SCF Sandbox - Huvudsidan för den engelska versionen av webbplatsen.

   * SCF Play - Underordnad till den huvudsida som ska spelas upp.

Även om den här självstudiekursen inte går in på [språkversioner](../../help/sites-administering/tc-prep.md)är den utformad så att rotsidan kan implementera identifiering av det språk som användaren föredrar via sidhuvudet i HTML och dirigera om till rätt huvudsida för språket. Konventionen är att använda landskoden med två bokstäver för sidans nodnamn, t.ex. &quot;en&quot; för engelska, &quot;fr&quot; för franska och så vidare.

## Skapa första sidor {#create-first-pages}

Nu finns det en [sidmall](initial-app.md#createthepagetemplate)kan vi skapa webbplatsens rotsida i katalogen /content.

1. Standardgränssnittet innehåller för närvarande utkast för att skapa webbplatser. Det klassiska användargränssnittet är användbart eftersom den här självstudiekursen skapar en enkel webbplats.

   Om du vill växla till det klassiska användargränssnittet väljer du global navigering och håller pekaren över den högra sidan av projektikonen. Välj *Växla till klassiskt gränssnitt* ikon som visas:

   ![classic-ui](assets/classic-ui.png)

   Möjligheten att växla till det klassiska användargränssnittet måste vara [aktiveras av en administratör](../../help/sites-administering/enable-classic-ui.md).

1. Från [välkomstsida för klassiskt användargränssnitt](http://localhost:4502/welcome.html), markera **[!UICONTROL Websites]**.

   ![classic-ui-website](assets/classic-ui-website.png)

   Du kan även få tillgång till det klassiska användargränssnittet för webbplatser direkt genom att gå till [/siteadmin.](http://localhost:4502/siteadmin)

1. Välj **[!UICONTROL Websites]** och sedan i verktygsfältet **[!UICONTROL New]** > **[!UICONTROL New Page]**.

   I **[!UICONTROL Create Page]** anger du följande:

   * Titel: `SCF Sandbox Site`
   * Namn: `an-scf-sandbox`
   * Välj **[!UICONTROL An SCF Sandbox Play Template]**
   * Klicka på **[!UICONTROL Create]**

   ![classic-ui-create-page](assets/classic-ui-create-page.png)

1. Markera den sida du just skapade i Utforskarfönstret. `/Websites/SCF Sandbox Site`och klicka **[!UICONTROL New]** > **[!UICONTROL New Page]**:

   * Titel: `SCF Sandbox`
   * Namn: `en`
   * Välj **[!UICONTROL An SCF Sandbox Play Template]**
   * Klicka på **[!UICONTROL Create]**

1. Markera den sida du just skapade i Utforskarfönstret. `/Websites/SCF Sandbox Site/SCF Sandbox`och klicka **[!UICONTROL New]** > **[!UICONTROL New Page]**

   * Titel: `SCF Play`
   * Namn: `play`
   * Välj **[!UICONTROL An SCF Sandbox Play Template]**
   * Klicka på **[!UICONTROL Create]**

1. Så här visas webbplatsen nu i webbplatskonsolen. Observera att underordnade sidor för objektet som är markerat i utforskarrutan visas i den högra rutan där de kan hanteras.

   ![classic-ui-website-page](assets/classic-ui-website-page.png)

   Det här är databasvyn över vad som har skapats med webbplatsverktyget och mallen:

   ![classic-ui-database-view](assets/classic-ui-repository-view.png)

## Lägg till designbanan {#add-the-design-path}

När ` [/etc/designs/an-scf-sandbox](setup-website.md#setupthedesigntreeetcdesigns)` skapades med designavsnittet i verktygskonsolen, egenskapen &quot;

* `cq:template="/libs/wcm/core/templates/designpage"`

har definierats, vilket ger möjlighet att referera till designresurser i ett skript med `currentDesign.getPath()`. Till exempel

* `% String favIcon = currentDesign.getPath() + "/favicon.ico"; %`


   * Namn: `cq:designPath`
   * Typ: `String`
   * Värde: `/etc/designs/an-scf-sandbox`

* Klicka på den gröna `[+] Add`

Databasen ska vara som följer:

![classic-ui-database-path](assets/classic-ui-repository-path.png)

* Klicka på **[!UICONTROL Save All]**

Om det uppstår problem när konfigurationen sparas kan du logga in igen och konfigurera igen.

>[!NOTE]
>
>Användning av `cq:designPath` är valfritt och har ingen koppling till [användning av klientlibs](develop-app.md#includeclientlibsintemplate), som i huvudsak krävs eftersom SCF-komponenterna använder [klientlibs](client-customize.md#clientlibs-for-scf) för att hantera JS och CSS.
