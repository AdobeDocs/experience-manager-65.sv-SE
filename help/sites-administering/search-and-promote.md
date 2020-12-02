---
title: Integrera med Adobe Search & Promote
seo-title: Integrera med Adobe Search & Promote
description: Lär dig integrera med Adobe Search & Promote.
seo-description: Lär dig integrera med Adobe Search & Promote.
uuid: 7e9384d9-9e4f-4e00-a1c9-35547de6ceb8
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: aca444f6-418a-4c01-ae19-663b4e04fab9
docset: aem65
translation-type: tm+mt
source-git-commit: 1c1ade947f2cbd26b35920cfd10b1666b132bcbd
workflow-type: tm+mt
source-wordcount: '910'
ht-degree: 1%

---


# Integrera med Adobe Search &amp; Promote{#integrating-with-adobe-search-promote}

Gör så här för att ringa tjänsten Adobe Search &amp; Promote från din webbplats:

1. Ange URL:en för molnet.
1. Konfigurera anslutningen till Search &amp; Promote.
1. Lägg till Search &amp; Promote i Sidekick.
1. Använd komponenterna för att skapa innehållet. (Se [Lägga till Search &amp; Promote på en webbsida](/help/sites-authoring/search-and-promote.md).)
1. Lägg till banderoller på sidorna. Banderollbilder är känsliga för Search &amp; Promote data.
1. Generera en webbplatskarta som Search &amp; Promote ska använda.

>[!NOTE]
>
>Om du använder Search &amp; Promote med en anpassad proxykonfiguration måste du konfigurera både HTTP-klientproxykonfigurationer eftersom vissa funktioner i AEM använder 3.x-API:erna och andra 4.x-API:er:
>
>* 3.x har konfigurerats med [https://localhost:4502/system/console/configMgr/com.day.commons.httpclient](https://localhost:4502/system/console/configMgr/com.day.commons.httpclient)
>* 4.x har konfigurerats med [https://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator](https://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator)

>



## Ändra Search &amp; Promote tjänst-URL {#changing-the-search-promote-service-url}

Standardwebbadressen som är konfigurerad för Search &amp; Promote är `https://searchandpromote.omniture.com/px/`. Om du vill använda en annan tjänst använder du OSGi-konsolen för att ange en annan URL.

1. Öppna OSGi-konsolen och klicka på fliken Konfiguration. ([https://localhost:4502/system/console/configMgr.](https://localhost:4502/system/console/configMgr))
1. Klicka på Dag CQ Search &amp; Promote Configuration.
1. Ange URL-adressen i rutan Fjärrserverns URI och klicka på Spara.

## Konfigurerar anslutningen till Search &amp; Promote {#configuring-the-connection-to-search-promote}

Konfigurera en eller flera anslutningar till Search &amp; Promote så att dina webbsidor kan interagera med tjänsten. För att kunna ansluta måste du ha medlems-ID och kontonummer för ditt Search &amp; Promote-konto.

1. I **verktygsikonen** > **Distribution** väljer du **Cloud Services**.

   Du kommer nu till Cloud Services Dashboard. Om du använder en lokal dator ser kontrollpanelens URL ut ungefär så här:

   [https://localhost:4502/libs/cq/core/content/tools/cloudservices.html](https://localhost:4502/libs/cq/core/content/tools/cloudservices.html)

1. På sidan Cloud Services klickar du på länken Adobe Search &amp; Promote eller på ikonen Search &amp; Promote.

1. Om det är första gången du konfigurerar Adobe Search &amp; Promote klickar du på **Konfigurera nu** för att öppna panelen Skapa konfiguration.

   Om du vill veta mer om Search &amp; Promote klickar du på **Läs mer** i stället.

   ![](assets/chlimage_1-59.png)

1. Ange en **titel** som kan kännas igen av sidförfattare och ange ett unikt **namn** och klicka sedan på **Skapa**.

   Fönstret **Redigera komponent** öppnas.

   Dessutom visas den nya konfigurationen nedanför **Tillgängliga konfigurationer** på **Cloud Services-kontrollpanelen** Adobe Search &amp; Promote.

   ![](assets/chlimage_1-60.png)

1. Lägg till följande i fälten i dialogrutan **Redigera komponent**.

   * **Medlems-ID**
   * **Kontonummer**

   >[!NOTE]
   >
   >Om du vill hämta den här informationen **själv måste du först logga in**
   >
   >[https://searchandpromote.omniture.com/center/](https://searchandpromote.omniture.com/center/)
   >
   >
   >med dina giltiga Seach&amp;Promote-inloggningsuppgifter (e-post/lösenord).
   >Sedan måste du titta på din URL i din webbläsares adressfält som ska se ut ungefär så här:
   >[](https://searchandpromote.omniture.com/px/home/?sp_id=XXXXXXXX-spYYYYYYYY)
   >
   >[https://searchandpromote.omniture.com/px/home/?sp_id=XXXXXXXX-spYYYYYYYY](https://searchandpromote.omniture.com/px/home/?sp_id=XXXXXXXX-spYYYYYYYY)
   >
   >**Var:**
   >
   >    * **** XXXXXXXXmotsvarar medlems-id***
   >    * **** spYYYYYYmotsvarar ditt  **kontonummer**


1. Klicka på **Anslut till Search &amp; Promote**.

   När meddelandet om att anslutningen lyckades visas klickar du på **OK**.

   (När du har anslutit ändras knapptexten till** Återanslut till Search &amp; Promote**.)

1. Klicka på **OK**. Sidan Inställningar för Search &amp; Promote visas för den konfiguration som du just har skapat.

## Konfigurera datacentret {#configuring-the-data-center}

Om ditt Search &amp; Promote-konto finns i Asien eller Europa måste du ändra standarddatacentret så att det pekar på rätt datacenter (standarddatacentret är för nordamerikanska konton).

Så här konfigurerar du datacentret:

1. Gå till webbkonsolen på `https://localhost:4502/system/console/configMgr/com.day.cq.searchpromote.impl.SearchPromoteServiceImpl`

   ![](assets/chlimage_1-61.png)

1. Beroende på var servern finns ändrar du URI:n till något av följande:

   * Nordamerika: [https://center.atomz.com/px/](https://center.atomz.com/px/)
   * EMEA: [https://center.lon5.atomz.com/px/](https://center.lon5.atomz.com/px/)
   * APAC: [https://center.sin2.atomz.com/px/](https://center.sin2.atomz.com/px/)

1. Klicka på **Spara**.

## Lägga till Search &amp; Promote-komponenter i Sidekick {#adding-search-promote-components-to-sidekick}

I designläget redigerar du en **par**-komponent som tillåter att Search &amp; Promote i Sidekick. (Mer information finns i [dokumentationen för komponenter](/help/sites-developing/components.md#addinganewcomponenttotheparagraphsystemdesignmode).)

Mer information om hur du använder komponenterna finns i [Lägga till Search &amp; Promote på en webbsida](/help/sites-authoring/search-and-promote.md).)

## Ange vilken Search &amp; Promote som dina sidor använder {#specifying-the-search-promote-service-that-your-pages-use}

Konfigurera webbsidor så att de använder en viss Search &amp; Promote. Search &amp; Promote använder automatiskt tjänsten på sin värdsida.

När du konfigurerar sidegenskaperna för en Search &amp; Promote ärver alla underordnade sidor inställningarna. Om det behövs kan du konfigurera underordnade sidor så att de åsidosätter de ärvda inställningarna.

>[!NOTE]
>
>Tjänstanslutningen måste redan vara konfigurerad. (Se [Konfigurera anslutningen till Search &amp; Promote](#connection).)

1. Öppna dialogrutan **Sidegenskaper**. På sidan** Webbplatser** högerklickar du på sidan och klickar på **Egenskaper**.
1. Klicka på fliken **Cloud Services**.
1. Om du vill inaktivera arvet av molntjänstkonfigurationer från en överordnad sida klickar du på hänglåsikonen bredvid arvsökvägen.

   ![](assets/sandpinheritpadlock.png)

1. Klicka på **Lägg till tjänst**, välj **Adobe Search &amp; Promote** och klicka på **OK**.
1. Markera anslutningskonfigurationen för ditt Search &amp; Promote-konto och klicka sedan på **OK**.

## Produktfeed {#product-feed}

Integreringen av Search &amp; Promote gör att du kan:

* använda eCommerce API, oberoende av den underliggande databasstrukturen och handelsplattformen.
* utnyttja funktionen Index Connector i Search &amp; Promote för att ge en produktfeed i XML-format.
* utnyttja funktionen Fjärrstyrning i Search &amp; Promote för att utföra on-demand- eller schemalagda begäranden i produktflödet
* feed-generering för olika Search &amp; Promote, konfigurerad som molntjänster.

Mer information finns i [Produktfeed](/help/sites-administering/product-feed.md).
