---
title: Publicera och avpublicera formulär och dokument
seo-title: Publicera och avpublicera formulär och dokument
description: Du kan schemalägga publicering och avpublicering av formulär. Publicerade formulär replikeras på publiceringsinstansen.
seo-description: Du kan schemalägga publicering och avpublicering av formulär. Publicerade formulär replikeras på publiceringsinstansen.
uuid: 0bad5608-b7a8-4599-81cc-2cd0a3dc7dd5
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
content-strategy: max-2018
discoiquuid: 32a7a50c-74f4-49bc-a0bd-a9ec142527cb
docset: aem65
translation-type: tm+mt
source-git-commit: f9ed171c188a4dfb71f12ae9c98105a4c1895542

---


# Publicera och avpublicera formulär och dokument{#publishing-and-unpublishing-forms-and-documents}

Med AEM Forms kan du enkelt skapa, publicera och avpublicera formulär. Mer information om AEM Forms finns i [Introduktion till hantering av formulär](../../forms/using/introduction-managing-forms.md).

AEM Forms-servern innehåller två instanser: Skapa och publicera. Författarinstans används för att skapa och hantera formulärresurser och resurser. Publiceringsinstansen används för att hålla resurser och relaterade resurser tillgängliga för slutanvändare. Du kan importera XDP- och PDF-formulär i redigeringsläget. Mer information finns i [Hämta XDP- och PDF-dokument i AEM-formulär](../../forms/using/get-xdp-pdf-documents-aem.md).

## Resurser som stöds {#supported-assets-nbsp}

AEM Forms stöder följande typer av resurser:

* Anpassningsbara formulär
* Anpassningsbara dokument
* Anpassningsbara formulärfragment
* Teman
* Formulärmallar (XFA-formulär)
* PDF-formulär
* Dokument (platta PDF-dokument)
* Formuläruppsättningar
* Resurs (bilder, scheman och formatmallar)

Till att börja med är alla resurser bara tillgängliga i Author-instansen. En administratör eller formulärförfattare kan publicera alla resurser utom resurser.

När du markerar ett formulär och publicerar det publiceras även dess relaterade resurser och resurser. Beroende resurser publiceras dock inte. I det här sammanhanget är relaterade resurser och resurser resurser som en publicerad tillgång använder eller refererar till. Beroende resurser är resurser som refererar till en publicerad resurs.

Dina adaptiva formulär kan använda vissa konfigurationer, inställningar och anpassningar som inte publiceras automatiskt. Vi rekommenderar att du publicerar eller aktiverar dessa resurser innan du publicerar ett anpassat formulär.

* Redigerbara adaptiva formulärmallar
* Konfigurationer av molntjänster för Adobe Sign, Typekit, reCAPTCHA och formulärdatamodeller
* Andra konfigurationer av molntjänster aktiveras bara om användaren har administratörsbehörighet.
* Anpassningar. Dessa omfattar, men är inte begränsade till:

   * Anpassade layouter
   * Anpassade utseenden
   * CSS-fil - används som indata i dialogrutan med egenskaper för adaptiv formulärbehållare
   * Kategori för klientbibliotek - tas som indata i dialogrutan med egenskaper för behållare för adaptiva formulär
   * Alla andra klientbibliotek som kan ingå i mallen för adaptiva formulär.
   * Designbanor

## Tillgångstillstånd {#asset-states}

En resurs kan ha följande lägen:

* **** Opublicerad: En resurs som aldrig har publicerats (det opublicerade läget gäller endast Forms-resurser. Resurser för korrespondenshantering har inte ett opublicerat läge.)
* **Publicerat**: En resurs som har publicerats och är tillgänglig i publiceringsinstansen
* **Ändrad**: En resurs som ändras efter att ha publicerats

## Publicera en resurs {#publish-an-asset}

1. Logga in på AEM Forms-servern.
1. Använd något av följande för att välja och publicera en resurs.

   1. Flytta pekaren över en resurs och tryck på **[!UICONTROL Publish]** ![aem6forms_globe](assets/aem6forms_globe.pngasset.png).
   1. Gör något av följande och tryck sedan på Publicera:

      * Om du är i kortvyn trycker du på **[!UICONTROL Enter Selection]** ![aem6forms_check-circle](assets/aem6forms_check-circle.png)och sedan på resursen. Resursen har valts.
      * Om du är i listvyn markerar du kryssrutan för en resurs. Resursen har valts.
      * Tryck på en resurs för att visa dess information.
      * Visa egenskaperna för en resurs genom att trycka på Visa ![visningsegenskaper](assets/viewproperties.png).
      >[!NOTE]
      >
      >Markera inte flera resurser. Det går inte att publicera flera resurser samtidigt.


1. När publiceringsprocessen startar visas en bekräftelsedialogruta med en lista över alla relaterade resurser och resurser. Tryck på **[!UICONTROL Publicera]** i dialogrutan som innehåller relaterade resurser. Resursen publiceras och dialogrutan Publicera resurser har slutförts visas.

   >[!NOTE]
   >
   >För adaptiva formulär, tillsammans med relaterade resurser, visas även sidnamnet Adaptivt formulär.

   ![En bekräftelsedialogruta med alla relaterade resurser och resurser](assets/p4.png)

   En bekräftelsedialogruta med alla relaterade resurser och resurser.

   >[!NOTE]
   >
   >Om användaren inte har behörighet att publicera resurserna i listan i Forms Manager är åtgärden Publicera inaktiverad. En resurs som kräver extra behörigheter visas i rött.

   När en resurs har publicerats kopieras resursens metadataegenskaper till publiceringsinstansen och resursens status ändras till Publicerad. Statusen för beroende resurser som publiceras ändras också till Publicerad.

   När du har publicerat en resurs kan du använda Forms Portal för att visa alla resurser på en webbsida. Mer information finns i Introduktion [till att publicera formulär på en portal](../../forms/using/introduction-publishing-forms.md).

## Publicera alla Correspondence Management Assets {#publish-all-the-correspondence-management-assets}

Med AEM Forms kan du publicera alla Correspondence Management-resurser på en server på en gång. De publicerade resurserna innehåller alla Correspondence Management-resurser och relaterade beroenden.

Följ de här stegen för att publicera alla Correspondence Management-resurser på en server:

1. Logga in på AEM Forms-servern.
1. Tryck på **Adobe Experience Manager** i det globala navigeringsfältet.
1. Tryck på ![verktygen](assets/tools.png)och sedan på **Formulär**.
1. Tryck på **Publicera Correspondence Management Assets**.

   ![publish-cmp-assets](assets/publish-cmp-assets.png)

   Sidan Publicera alla resurser för hantering av korrespondenshantering visas och visar information om den senaste gången som processen Publicera resurser för korrespondenshantering försökte utföras.

   ![publish-last-run-details](assets/publish-last-run-details.png)

1. Tryck på **Publicera** och tryck på **OK** i bekräftelsemeddelandet.

   När en gruppbearbetning är klar kan du visa information om den senaste körningen. Detta inkluderar information som administratörsinloggning och om batchkörningen lyckades eller misslyckades.

   >[!NOTE]
   >
   >Publiceringsprocessen kan inte avbrytas när den väl har initierats. När publiceringsåtgärden pågår ska du inte skapa, ta bort, ändra eller publicera några resurser eller initiera åtgärden Exportera alla resurser för korrespondenshantering.

## Automatisera publicering och avpublicering för formulär och dokument {#automate-publishing-and-unpublishing-for-forms-amp-documents}

Med AEM Forms kan du schemalägga resurspublicering och avpublicering för formulär och dokument. Du kan ange schemat i metadataredigeraren. Mer information om hur du hanterar metadata för formulär finns i [Hantera metadata för formulär.](../../forms/using/manage-form-metadata.md)

Följ de här stegen för att schemalägga datum och tid för publicering och avpublicering av Forms &amp; Documents-resurser:

1. Markera en resurs och tryck på **[!UICONTROL Visa egenskaper]**. Sidan Metadataegenskaper öppnas.
1. På sidan Metadataegenskaper trycker du på **[!UICONTROL Avancerat]** och sedan på **[!UICONTROL Redigera]** ![illustrator_penciltool_cur_edit_2_17](assets/illustratorcc_penciltool_cur_edit_2_17.png).
1. Välj datum och tid i fälten **[!UICONTROL Publicera i tid]** och **[!UICONTROL Publicera i tid]** .\
   Tryck på **[!UICONTROL Done]** ![aem6forms_check](assets/aem6forms_check.png).

## Avpublicera en resurs {#unpublish-an-asset}

1. Markera en publicerad resurs och tryck på **[!UICONTROL Avpublicera]** ![avpublicering](assets/unpublish.png).
1. Använd något av följande för att välja och avpublicera en resurs.

   1. Flytta pekaren över en resurs och tryck på **[!UICONTROL Avpublicera]** ![avpublicering](assets/unpublish.png).
   1. Gör något av följande och tryck sedan på Avpublicera:

      * Om du är i kortvyn trycker du på **[!UICONTROL Enter Selection]** ![aem6forms_check-circle](assets/aem6forms_check-circle.png)och sedan på resursen. Resursen har valts.

      * Om du är i listvyn håller du pekaren över en resurs och trycker på ![markeringen](assets/selectassetcheckmark.png) selectAsset. Resursen har valts.

      * Tryck på en resurs för att visa dess information.
      * Visa egenskaperna för en resurs genom att trycka på Visa ![visningsegenskaper](assets/viewproperties.png).

1. När avpubliceringsprocessen startar visas en bekräftelsedialogruta. Tryck på **[!UICONTROL Avpublicera]**.

   >[!NOTE]
   >
   >Endast den markerade resursen avpubliceras och dess underordnade och refererade resurser, om det finns några, avpubliceras inte.

## Återställa en resurs eller ett brev till den tidigare publicerade versionen {#revert-an-asset-or-letter-to-the-previously-published-version}

Varje gång du publicerar en resurs eller ett brev efter att ha redigerat den skapas en version av resursen eller brevet. Du kan återställa en resurs eller ett brev till en tidigare publicerad version. Du kan behöva göra det om något blir fel med den aktuella versionen av resursen eller dokumentet.

>[!NOTE]
>
>Återställ inte ett brev till ett senast publicerat tillstånd om någon beroende resurs som används i det publicerade brevet tas bort från systemet.

1. Markera en resurs och tryck på **[!UICONTROL Återgå till tidigare publicerad version]** ![återställ tidigare publicerad version](assets/reverttopreviouslypublishedversion.png).
1. Innan resursen återställs visas en bekräftelsedialogruta. Tryck på **[!UICONTROL Återställ]**.

   Resursen eller bokstaven återställs till den tidigare publicerade versionen.

## Ta bort en resurs {#delete-an-asset}

>[!NOTE]
>
>Om du tar bort en resurs tas den bort från publiceringsinstansen. När du tar bort ett objekt tas även dess versionshistorik bort, förutom basversionen.

1. Markera en resurs och tryck på **[!UICONTROL Ta bort]** ![borttagning](assets/delete.png).

   >[!NOTE]
   >
   >Alternativet Ta bort är också tillgängligt när du visar resursinformation genom att trycka på en resurs eller genom att trycka på ![Visa egenskaper](assets/viewproperties.png)för en resurs.

1. Innan resursen tas bort visas en bekräftelsedialogruta. Tryck på **[!UICONTROL Ta bort]**.

   >[!NOTE]
   >
   >Endast den markerade resursen tas bort och de beroende resurserna tas inte bort. Om du vill kontrollera referenser till en resurs trycker du på ![referenser](assets/references.png) och väljer sedan en resurs.
   >
   >
   >Om den resurs du försöker ta bort är underordnad en annan resurs tas den inte bort. Om du vill ta bort en sådan resurs tar du bort referenser till den från andra resurser och försöker sedan igen.

## Skyddade adaptiva formulär {#protected-adaptive-forms}

Du kan aktivera autentisering för formulär som du vill att valda användare ska ha åtkomst till. När du aktiverar autentisering för dina formulär visas en inloggningsskärm innan användarna kan komma åt dem. Endast användare med autentiseringsuppgifter som är behöriga kan komma åt formulären.

Så här aktiverar du autentisering för dina formulär:

1. Öppna configMgr i publiceringsinstansen i webbläsaren.\
   Webbadress: `https://<hostname>:<PublishPort>/system/console/configMgr`

1. Klicka på **Apache Sling Authentication Service** i webbkonsolkonfigurationen för Adobe Experience Manager för att konfigurera den.
1. I dialogrutan Apache Sling Authentication Service som visas använder du **+** -knappen för att lägga till sökvägar.\
   När du lägger till en sökväg aktiveras autentiseringstjänsten för formulär i den sökvägen.
