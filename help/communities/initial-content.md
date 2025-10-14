---
title: Ursprungligt sandlådeinnehåll
description: Lär dig hur du använder sidmallen i sandlådan för att skapa en huvudsida för en engelsk version av en webbplats och en underordnad sida utanför huvudsidan.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 068a0fff-ca48-4847-ba3f-d78416c97f6d
solution: Experience Manager
feature: Communities
role: Developer
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '454'
ht-degree: 0%

---

# Ursprungligt sandlådeinnehåll {#initial-sandbox-content}

I det här avsnittet skapar du följande sidor som alla använder [sidmallen](initial-app.md#createthepagetemplate):

* SCF Sandbox Site, som dirigerar om till den engelska versionen av huvudsidan.

   * SCF Sandbox - Huvudsidan för den engelska versionen av webbplatsen.

   * SCF Play - Underordnad till den huvudsida som ska spelas upp.

Den här självstudiekursen tas inte bort i [språkkopior](../../help/sites-administering/tc-prep.md). Istället är den utformad så att rotsidan kan implementera identifiering av det språk som användaren föredrar via sidhuvudet i HTML och dirigera om till rätt huvudsida för språket. Konventionen är att använda landskoden med två bokstäver för sidans nodnamn, till exempel &quot;en&quot; för engelska och &quot;fr&quot; för franska.

## Skapa första sidor {#create-first-pages}

Nu när det finns en [sidmall](initial-app.md#createthepagetemplate) kan du skapa webbplatsens rotsida i katalogen /content.

1. Standardgränssnittet innehåller för närvarande utkast för att skapa webbplatser. Det klassiska användargränssnittet är användbart eftersom den här självstudiekursen skapar en enkel webbplats.

   Om du vill växla till det klassiska användargränssnittet väljer du global navigering och håller pekaren över den högra sidan av projektikonen. Välj ikonen *Byt till klassiskt gränssnitt* som visas:

   ![classic-ui](assets/classic-ui.png)

   Möjligheten att växla till det klassiska användargränssnittet måste vara [aktiverat av en administratör](../../help/sites-administering/enable-classic-ui.md).

1. Välj **[!UICONTROL Websites]** på [den klassiska användargränssnittets välkomstsida](http://localhost:4502/welcome.html).

   ![classic-ui-website](assets/classic-ui-website.png)

   Du kan även få tillgång till det klassiska användargränssnittet för webbplatser direkt genom att gå till [/siteAdmin.](http://localhost:4502/siteadmin)

1. Välj **[!UICONTROL Websites]** i utforskarrutan och välj sedan **[!UICONTROL New]** > **[!UICONTROL New Page]** i verktygsfältet.

   Ange följande i dialogrutan **[!UICONTROL Create Page]**:

   * Titel: `SCF Sandbox Site`
   * Namn: `an-scf-sandbox`
   * Välj **[!UICONTROL An SCF Sandbox Play Template]**
   * Klicka på **[!UICONTROL Create]**

   ![classic-ui-create-page](assets/classic-ui-create-page.png)

1. I utforskarrutan markerar du sidan som du skapade, `/Websites/SCF Sandbox Site`, och klickar på **[!UICONTROL New]** > **[!UICONTROL New Page]**:

   * Titel: `SCF Sandbox`
   * Namn: `en`
   * Välj **[!UICONTROL An SCF Sandbox Play Template]**
   * Klicka på **[!UICONTROL Create]**

1. I utforskarrutan markerar du sidan som du skapade, `/Websites/SCF Sandbox Site/SCF Sandbox`, och klickar på **[!UICONTROL New]** > **[!UICONTROL New Page]**

   * Titel: `SCF Play`
   * Namn: `play`
   * Välj **[!UICONTROL An SCF Sandbox Play Template]**
   * Klicka på **[!UICONTROL Create]**

1. Så här visas webbplatsen nu i webbplatskonsolen. Observera att underordnade sidor för objektet som är markerat i utforskarrutan visas i den högra rutan där de kan hanteras.

   ![classic-ui-website-page](assets/classic-ui-website-page.png)

   Det här är databasvyn över vad som har skapats med webbplatsverktyget och mallen:

   ![classic-ui-database-view](assets/classic-ui-repository-view.png)

## Lägg till designbanan {#add-the-design-path}

När ` [/etc/designs/an-scf-sandbox](setup-website.md#setupthedesigntreeetcdesigns)` skapades med designavsnittet i verktygskonsolen är egenskapen &quot;

* `cq:template="/libs/wcm/core/templates/designpage"`

Definierades, vilket ger möjlighet att referera till designresurser i ett skript med `currentDesign.getPath()`. Till exempel

* `% String favIcon = currentDesign.getPath() + "/favicon.ico"; %`


   * Namn: `cq:designPath`
   * Typ: `String`
   * Värde: `/etc/designs/an-scf-sandbox`

* Klicka på den gröna `[+] Add`

Databasen ska visas så här:

![classic-ui-database-path](assets/classic-ui-repository-path.png)

* Klicka på **[!UICONTROL Save All]**

Om det blir problem med att spara konfigurationen loggar du in igen och konfigurerar igen.

>[!NOTE]
>
>Användningen av `cq:designPath` är valfri och har inget samband med [användningen av clientlibs](develop-app.md#includeclientlibsintemplate) som krävs eftersom SCF-komponenterna använder [&#x200B; clientlibs](client-customize.md#clientlibs-for-scf) för att hantera sina JS- och CSS-filer.
