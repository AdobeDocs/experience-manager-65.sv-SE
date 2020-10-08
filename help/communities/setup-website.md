---
title: Konfigurera webbplatsstruktur
seo-title: Konfigurera webbplatsstruktur
description: Konfigurera kataloger
seo-description: Konfigurera kataloger
uuid: a31edcd5-dab8-4a42-953b-1d076c2182b2
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: d18c0ece-4c4f-499c-ac94-a9aaa7f883c4
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '510'
ht-degree: 2%

---


# Konfigurera webbplatsstruktur {#setup-website-structure}

Instruktionerna nedan beskriver mapparna som ska skapas på följande platser när du konfigurerar webbplatsen:

* `/apps/an-scf-sandbox`

   Här finns anpassade program och mallar.

* `/etc/designs/an-scf-sandbox`

   Här finns hämtningsbara designelement.

* `/content/an-scf-sandbox`

   Det är här som de hämtningsbara webbsidorna finns.

Koden i den här självstudien är beroende av att huvudmappnamnet är samma för programmet, designen och innehållet. Om du väljer något annat namn för webbplatsen ska du alltid ersätta `an-scf-sandbox` med det namn du har valt.

>[!NOTE]
>
>Om namn:
>
>* Namnen i CRXDE är nodnamn som utgör sökvägen till adresserbart innehåll.
>* Nodnamn kan innehålla mellanslag, men när de används i en URI måste utrymmet kodas antingen som %20 eller +.
>* Nodnamn kan innehålla bindestreck och understreck, men de måste kodas när de refereras som ett paketnamn i en Java-fil. Både bindestreck och understreck escape-konverteras med understreck följt av deras unicode-värde:

   >
   >   
   * bindestreck blir &#39;_002d&#39;
   >   * understreck blir &#39;_005f&#39;


## Konfigurera programkatalogen (/apps) {#setup-the-application-directory-apps}

Katalogen /apps i databasen innehåller koden som implementerar beteendet och återgivningen av de sidor som hanteras från katalogen /content.

Katalogen /apps är skyddad och inte allmänt tillgänglig, vilket är katalogerna /content och /etc/designs.

1. Skapa `/apps/an-scf-sandbox` mapp.

   Använda **[!UICONTROL CRXDE Lite]** i utforskarrutan

   1. Markera `/apps` mappen.
   1. Högerklicka **[!UICONTROL Create]**.. eller dra ned på **[!UICONTROL Create...]** menyn.
   1. Välj **[!UICONTROL Create Folder...]**.
   1. In the **[!UICONTROL Create Folder]** dialog, enter `an-scf-sandbox`.
   1. Klicka på **[!UICONTROL OK]**.

1. Skapa **[!UICONTROL components]** undermapp.

   1. Markera `/apps/an-scf-sandbox` mappen.
   1. Klicka på **[!UICONTROL Create > Create Folder]**.
   1. In the **[!UICONTROL Create Folder]** dialog, enter **[!UICONTROL components]**.
   1. Klicka på **[!UICONTROL OK]**.

1. Skapa **[!UICONTROL templates]** undermapp.

   1. Markera `/apps/an-scf-sandbox` mappen.
   1. Klicka på **[!UICONTROL Create > Create Folder]**.
   1. In the **[!UICONTROL Create Folder]** dialog, enter **[!UICONTROL templates]**.
   1. Klicka på **[!UICONTROL OK]**.
   1. Markera igen `/apps/an-scf-sandbox`.
   1. Välj **[!UICONTROL Save All]**.

   Spara ofta, precis som med andra redigeringsprocesser. Om du får problem med att ange data kan det bero på att tidsgränsen för inloggningen har överskridits eller på att du måste spara tidigare redigeringar.

1. Strukturen i utforskarpanelen i CRXDE Lite bör nu se ut ungefär så här:

   ![crxde-template](assets/crxde-template.png)

## Konfigurera designkatalogen (/etc/designs) {#setup-the-design-directory-etc-designs}

Katalogen /etc/designs innehåller de bilder, skript och formatmallar som ska hämtas tillsammans med sidinnehållet.

1. Om du vill använda verktyget Designer i det klassiska användargränssnittet går du till [https://&lt;server>:&lt;port>/miscadmin](http://localhost:4502/miscadmin).

   Obs! Om du använder CRXDE Lite för att skapa en nod av typen `cq:Page`ställs åtkomstkontroll och replikering inte in på standardinställningar för en sida.

1. Markera **[!UICONTROL Designs]** mappen i Utforskarfönstret och klicka sedan på **[!UICONTROL New]** > **[!UICONTROL New Page]**.

   Ange:

   * Titel: **[!UICONTROL An SCF Sandbox]**
   * Namn: **[!UICONTROL an-scf-sandbox]**
   * Välj **[!UICONTROL Design Page Template]**

   Klicka på **[!UICONTROL Create]**.

   ![design-template](assets/design-template.png)

1. Uppdatera utforskarfönstret om mappen &quot;An SCF Sandbox&quot; inte visas.

1. Gå tillbaka till CRXDE Lite (http:// localhost:4502/crx/de) och expandera /etc/designs för att se noden med namnet&quot;an-scf-sandbox&quot;.

   I den nedre högra rutan av CRXDE kan du visa fliken Egenskaper, fliken Åtkomstkontroll och fliken Replikering för att se vad som har definierats med hjälp av designsidmallen.

   ![crxde-configure-template](assets/crxde-configure-template.png)

## Konfigurera innehållskatalogen (/content) {#setup-the-content-directory-content}

Katalogen /content i databasen är den plats där webbplatsinnehållet finns. Sökvägarna under /content utgör sökvägarna till webbadressen för webbläsarbegäranden.

*När* [sidmallen](initial-app.md#createthepagetemplate) har skapats som en del av det inledande programmet kan det inledande sidinnehållet skapas baserat på mallen.... [**Mama**](initial-app.md)
