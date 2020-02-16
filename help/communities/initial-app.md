---
title: Ursprungligt sandlådeprogram
seo-title: Ursprungligt sandlådeprogram
description: Skapa mall, komponent och skript
seo-description: Skapa mall, komponent och skript
uuid: b0d03376-d8bc-4e98-aea2-a01744c64ccd
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: f74d225e-0245-4d5a-bb93-0ee3f31557aa
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Ursprungligt sandlådeprogram {#initial-sandbox-application}

I det här avsnittet skapar du följande:

* Den **[mall](#createthepagetemplate)**som ska användas för att skapa innehållssidor på exempelwebbplatsen
* Den **[komponent och det skript](#create-the-template-s-rendering-component)**som ska användas för att återge webbplatsens sidor

## Skapa innehållsmallen {#create-the-content-template}

En mall definierar standardinnehållet för en ny sida. Komplexa webbplatser kan använda flera mallar för att skapa olika typer av sidor på webbplatsen. Dessutom kan malluppsättningen bli en plan som används för att göra ändringar i ett kluster med servrar.

I den här övningen är alla sidor baserade på en enkel mall.

1. I utforskarfönstret i CRXDE Lite

   * select `/apps/an-scf-sandbox/templates`
   * **[!UICONTROL Skapa > Skapa mall]**

1. I dialogrutan Skapa mall skriver du följande värden och klickar sedan på **[!UICONTROL Nästa]**:

   * Etikett: `playpage`
   * Titel: `An SCF Sandbox Play Template`
   * Beskrivning: `An SCF Sandbox template for play pages`
   * Resurstyp: `an-scf-sandbox/components/playpage`
   * Rankning: &lt;lämna som standard>
   Etiketten används som nodnamn.

   Resurstypen visas som egenskap på `playpage`noden jcr:content `sling:resourceType`. Den identifierar komponenten (resursen) som återger innehållet när det begärs av en webbläsare.

   I det här fallet återges alla sidor som skapas med `playpage`mallen av `an-scf-sandbox/components/playpage` komponenten. Sökvägen till komponenten är relativ, vilket innebär att Sling kan söka efter resursen först i `/apps` mappen och, om den inte hittas, i `/libs` mappen.

   ![chlimage_1-75](assets/chlimage_1-75.png)

1. Om du använder kopiera/klistra in ska du kontrollera att värdet för Resurstyp inte har några inledande eller avslutande blanksteg.

   Click **[!UICONTROL Next]**.

1. &quot;Tillåtna sökvägar&quot; avser sökvägarna till sidor som använder den här mallen, så att mallen listas för dialogrutan **[!UICONTROL Ny sida]** .

   Om du vill lägga till en bana klickar du på plusknappen `+` och skriver `/content(/.&ast;)?` i textrutan som visas. Om du använder kopiera/klistra in ska du se till att det inte finns några inledande eller avslutande blanksteg.

   Obs!Värdet för den tillåtna egenskapen path är ett *reguljärt uttryck.* Innehållssidor som har en sökväg som matchar uttrycket kan använda mallen. I det här fallet matchar det reguljära uttrycket sökvägen till mappen **/content** och alla dess undersidor.

   När en författare skapar en sida nedan `/content`visas `playpage`mallen&quot;En SCF-sandlådesidmall&quot; i en lista med tillgängliga mallar som ska användas.

   När rotsidan har skapats från mallen kan åtkomsten till mallen begränsas till den här webbplatsen genom att ändra egenskapen så att den inkluderar rotsökvägen i det reguljära uttrycket, d.v.s..

   `/content/an-scf-sandbox(/.&ast;)?`

   ![chlimage_1-76](assets/chlimage_1-76.png)

1. Click **[!UICONTROL Next]**.

   Klicka på **[!UICONTROL Nästa]** på panelen **[!UICONTROL Tillåtna överordnade]** .

   Klicka på **[!UICONTROL Nästa]** på panelerna **[!UICONTROL Tillåtna underordnade]** .

   Click **[!UICONTROL OK]**.

1. När du har klickat på OK och skapat mallen visas röda trianglar i hörnen på egenskapsfliken för den nya `playpage`mallen. Dessa röda trianglar anger redigeringar som inte har sparats.

   Klicka på **[!UICONTROL Spara alla]** för att spara den nya mallen i databasen.

   ![chlimage_1-77](assets/chlimage_1-77.png)

### Skapa mallens återgivningskomponent {#create-the-template-s-rendering-component}

Skapa den *komponent* som definierar innehållet och återger alla sidor som skapats baserat på [spelningssidmallen](#createthepagetemplate).

1. Högerklicka i CRXDE Lite **`/apps/an-scf-sandbox/components`** och klicka på **[!UICONTROL Skapa > Komponent]**.
1. Genom att ställa in nodens namn (Label) på *uppspelningssidan*&#x200B;är sökvägen till komponenten

   `/apps/an-scf-sandbox/components/playpage`

   som motsvarar uppspelningssidmallens resurstyp (eventuellt minus den inledande **`/apps/`** delen av sökvägen).

   I dialogrutan **[!UICONTROL Skapa komponent]** skriver du följande egenskapsvärden:

   * Etikett: **uppspelningssida**
   * Titel: **En SCF-sandlåda spelar upp komponent**
   * Beskrivning: Det **här är den komponent som återger innehåll för en SCF-sandlådesida.**
   * Supertyp: *&lt;lämna tomt>*
   * Grupp:
   ![chlimage_1-78](assets/chlimage_1-78.png)

1. Klicka på **[!UICONTROL Nästa]** tills panelen **[!UICONTROL Tillåtna underordnade]** i dialogrutan visas

   * Click **[!UICONTROL OK]**
   * Klicka på **[!UICONTROL Spara alla]**

1. Kontrollera att sökvägen till komponenten och resourceType för mallen matchar.

   >[!CAUTION]
   >
   >Överensstämmelsen mellan sökvägen till uppspelningskomponenten och egenskapen sling:resourceType för uppspelningssidmallen är avgörande för att webbplatsen ska fungera korrekt.

   ![chlimage_1-79](assets/chlimage_1-79.png)