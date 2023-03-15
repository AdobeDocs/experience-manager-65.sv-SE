---
title: Ursprungligt sandlådeprogram
seo-title: Initial Sandbox Application
description: Skapa mall, komponent och skript
seo-description: Create template, component, and script
uuid: b0d03376-d8bc-4e98-aea2-a01744c64ccd
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: f74d225e-0245-4d5a-bb93-0ee3f31557aa
exl-id: cbf9ce36-53a2-4f4b-a96f-3b05743f6217
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '583'
ht-degree: 1%

---

# Ursprungligt sandlådeprogram {#initial-sandbox-application}

I det här avsnittet skapar du följande:

* The **[mall](#createthepagetemplate)** som ska användas för att skapa innehållssidor på exempelwebbplatsen.
* The **[komponent och skript](#create-the-template-s-rendering-component)** som kommer att användas för att återge webbplatsens sidor.

## Skapa innehållsmallen {#create-the-content-template}

En mall definierar standardinnehållet för en ny sida. Komplexa webbplatser kan använda flera mallar för att skapa olika typer av sidor på webbplatsen. Dessutom kan malluppsättningen bli en plan som används för att göra ändringar i ett kluster med servrar.

I den här övningen är alla sidor baserade på en enkel mall.

1. I utforskarfönstret i CRXDE Lite:

   * Välj `/apps/an-scf-sandbox/templates`
   * **[!UICONTROL Create]** > **[!UICONTROL Create Template]**

1. I dialogrutan Skapa mall skriver du följande värden och klickar sedan på **[!UICONTROL Next]**:

   * Etikett: `playpage`
   * Titel: `An SCF Sandbox Play Template`
   * Beskrivning: `An SCF Sandbox template for play pages`
   * Resurstyp: `an-scf-sandbox/components/playpage`
   * Rankning: &lt;leave as=&quot;&quot; default=&quot;&quot;>

   Etiketten används som nodnamn.

   Resurstypen visas på `playpage`&#39;s jcr:content node as the property `sling:resourceType`. Den identifierar komponenten (resursen) som återger innehållet när det begärs av en webbläsare.

   I det här fallet skapas alla sidor med `playpage` mallen återges av `an-scf-sandbox/components/playpage` -komponenten. Sökvägen till komponenten är relativ, vilket gör att Sling kan söka efter resursen först i `/apps` och, om den inte hittas, i `/libs` mapp.

   ![create-content-template](assets/create-content-template-1.png)

1. Om du använder kopiera/klistra in ska du kontrollera att värdet för Resurstyp inte har några inledande eller avslutande blanksteg.

   Klicka på **[!UICONTROL Next]**.

1. &quot;Tillåtna sökvägar&quot; avser sökvägarna till sidor som använder den här mallen, så att mallen visas för **[!UICONTROL New Page]** -dialogrutan.

   Klicka på plustecknet om du vill lägga till en bana `+` och text `/content(/.&ast;)?` i textrutan som visas. Om du använder kopiera/klistra in ska du se till att det inte finns några inledande eller avslutande blanksteg.

   Obs! Värdet för den tillåtna sökvägsegenskapen är en *reguljärt uttryck*. Innehållssidor som har en sökväg som matchar uttrycket kan använda mallen. I det här fallet matchar det reguljära uttrycket sökvägen för **/content** och alla dess undersidor.

   När en författare skapar en sida nedan `/content`, `playpage` Mallen &quot;En SCF Sandbox-sidmall&quot; visas i en lista med tillgängliga mallar som ska användas.

   När rotsidan har skapats från mallen kan åtkomsten till mallen begränsas till den här webbplatsen genom att ändra egenskapen så att den inkluderar rotsökvägen i det reguljära uttrycket, dvs.

   `/content/an-scf-sandbox(/.&ast;)?`

   ![configure-template-path](assets/configure-template-path.png)

1. Klicka på **[!UICONTROL Next]**.

   Klicka **[!UICONTROL Next]** i **[!UICONTROL Allowed Parents]** -panelen.

   Klicka **[!UICONTROL Next]** i **[!UICONTROL Allowed Children]** paneler.

   Klicka på **[!UICONTROL OK]**.

1. När du har klickat på OK och skapat mallen visas röda trianglar i hörnen på fliken Egenskaper för den nya `playpage` mall. Dessa röda trianglar anger redigeringar som inte har sparats.

   Klicka **[!UICONTROL Save All]** för att spara den nya mallen i databasen.

   ![verify-content-template](assets/verify-content-template.png)

### Skapa mallens återgivningskomponent {#create-the-template-s-rendering-component}

Skapa *komponent* som definierar innehållet och återger sidor som skapats baserat på [playpage-mall](#createthepagetemplate).

1. Högerklicka i CRXDE Lite **`/apps/an-scf-sandbox/components`** och klicka **[!UICONTROL Create > Component]**.
1. Genom att ange nodens namn (Label) till *playpage*, banan till komponenten är

   `/apps/an-scf-sandbox/components/playpage`

   som motsvarar uppspelningssidmallens resurstyp (eventuellt minus den ursprungliga) **`/apps/`** del av banan).

   I **[!UICONTROL Create Component]** skriver du följande egenskapsvärden:

   * Etikett: **playpage**
   * Titel: **En SCF-sandlådeuppspelningskomponent**
   * Beskrivning: **Det här är den komponent som återger innehåll för en SCF-sandlådesida.**
   * Supertyp: *&lt;leave blank=&quot;&quot;>*
   * Grupp: *&lt;leave blank=&quot;&quot;>*

   ![create-template-component](assets/create-template-component.png)

1. Klicka **[!UICONTROL Next]** tills **[!UICONTROL Allowed Children]** visas:

   * Klicka på **[!UICONTROL OK]**.
   * Klicka på **[!UICONTROL Save All]**.

1. Kontrollera att sökvägen till komponenten och resourceType för mallen matchar.

   >[!CAUTION]
   >
   >Överensstämmelsen mellan sökvägen till uppspelningskomponenten och egenskapen sling:resourceType för uppspelningssidmallen är avgörande för att webbplatsen ska fungera korrekt.

   ![verify-template-component](assets/verify-template-component.png)
