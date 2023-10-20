---
title: Konfigurera webbplatsstruktur
description: Lär dig hur du konfigurerar webbplatsstrukturen, inklusive de mappar som ska skapas.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 1f60a0d4-a272-45e8-9742-4b706be8502e
source-git-commit: f03d0ab9d0f491441378e16e1590d33651f064b5
workflow-type: tm+mt
source-wordcount: '516'
ht-degree: 1%

---

# Konfigurera webbplatsstruktur {#setup-website-structure}

Instruktionerna nedan beskriver mapparna som ska skapas på följande platser när du konfigurerar webbplatsen:

* `/apps/an-scf-sandbox`

  Här finns anpassade program och mallar.

* `/etc/designs/an-scf-sandbox`

  Här finns hämtningsbara designelement.

* `/content/an-scf-sandbox`

  Det är här som de hämtningsbara webbsidorna finns.

Koden i den här självstudiekursen beror på att huvudmappens namn är detsamma för programmet, designen och innehållet. Om du väljer något annat namn för webbplatsen ska du alltid ersätta `an-scf-sandbox` med det namn du har valt.

>[!NOTE]
>
>Om namn:
>
>* Namnen i CRXDE är nodnamn som utgör sökvägen till adresserbart innehåll.
>* Nodnamn kan innehålla mellanslag, men när de används i en URI måste utrymmet kodas antingen som %20 eller +.
>* Nodnamn kan innehålla bindestreck och understreck, men de måste kodas när de refereras som ett paketnamn i en Java™-fil. Både bindestreck och understreck escape-konverteras med understreck följt av deras Unicode-värde:
>
* bindestreck blir &#39;_002d&#39;
* understreck blir &#39;_005f&#39;

## Konfigurera programkatalogen (/apps) {#setup-the-application-directory-apps}

Katalogen /apps i databasen innehåller koden som implementerar beteendet och återgivningen av de sidor som hanteras från katalogen /content.

Katalogen /apps är skyddad och inte allmänt tillgänglig, vilket är katalogerna /content och /etc/designs.

1. Skapa `/apps/an-scf-sandbox` mapp.

   Använda **[!UICONTROL CRXDE Lite]**, i utforskarfönstret

   1. Välj `/apps` mapp.
   1. Högerklicka **[!UICONTROL Create]**... eller dra ner **[!UICONTROL Create...]** -menyn.
   1. Välj **[!UICONTROL Create Folder...]**.
   1. I **[!UICONTROL Create Folder]** dialogruta, ange `an-scf-sandbox`.
   1. Klicka på **[!UICONTROL OK]**.

1. Skapa **[!UICONTROL components]** undermapp.

   1. Välj `/apps/an-scf-sandbox` mapp.
   1. Klicka på **[!UICONTROL Create > Create Folder]**.
   1. I **[!UICONTROL Create Folder]** dialogruta, ange **[!UICONTROL components]**.
   1. Klicka på **[!UICONTROL OK]**.

1. Skapa **[!UICONTROL templates]** undermapp.

   1. Välj `/apps/an-scf-sandbox` mapp.
   1. Klicka på **[!UICONTROL Create > Create Folder]**.
   1. I **[!UICONTROL Create Folder]** dialogruta, ange **[!UICONTROL templates]**.
   1. Klicka på **[!UICONTROL OK]**.
   1. Markera igen `/apps/an-scf-sandbox`.
   1. Välj **[!UICONTROL Save All]**.

   Precis som vid alla redigeringsprocesser bör du spara ofta. Om du får problem med att ange data kan det bero på att tidsgränsen för inloggningen har överskridits, eller på att du måste spara tidigare redigeringar.

1. Strukturen i utforskarpanelen i CRXDE Lite bör nu se ut ungefär så här:

   ![crxde-template](assets/crxde-template.png)

## Konfigurera designkatalogen (/etc/designs) {#setup-the-design-directory-etc-designs}

Katalogen /etc/designs innehåller de bilder, skript och formatmallar som ska hämtas tillsammans med sidinnehållet.

1. Om du vill använda verktyget Designer i det klassiska användargränssnittet går du till [https://&lt;server>:&lt;port>/miscadmin](http://localhost:4502/miscadmin).

   Obs! Om du använder CRXDE Lite för att skapa en nod av typen Node `cq:Page`, ställs inte åtkomstkontroll och replikering in på standardinställningar för en sida.

1. I rutan Utforskaren väljer du **[!UICONTROL Designs]** mapp och klicka sedan på **[!UICONTROL New]** > **[!UICONTROL New Page]**.

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

*Efter* den [sidmall](initial-app.md#createthepagetemplate) skapas som en del av det inledande programmet, kan det inledande sidinnehållet skapas baserat på mallen..... [**Mama**](initial-app.md)
