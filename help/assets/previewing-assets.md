---
title: Förhandsgranska resurser
description: Lär dig förhandsgranska resurser i Dynamic Media
uuid: 09e97245-373b-4d50-8ba3-5d1034a29988
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: bb8c355c-4475-45ec-9096-0975f0ce2c27
docset: aem65
feature: Resurshantering
role: Affärsledare, administratör
translation-type: tm+mt
source-git-commit: 2e734041bdad7332c35ab41215069ee696f786f4
workflow-type: tm+mt
source-wordcount: '1338'
ht-degree: 2%

---


# Förhandsgranska resurser med programgränssnittet {#previewing-assets}

Du kan använda Förhandsgranska för att se hur en digital resurs som du har överfört ser ut när den visas av en kund i deras egen webbläsare. Standardvisningsprogrammet för inbäddade enheter som är tilldelade resursen används för förhandsvisningen.

Ett visningsprogram är en samling med olika inställningar eller&quot;förinställningar&quot;, t.ex. visningsprogrammets visningsstorlek, zoombeteende, färgscheman, kanter, teckensnitt osv., som avgör hur användare visar mediefiler på datorskärmar och mobila enheter.

Förutom att använda den dedikerade förhandsvisningsfunktionen för video, snurra och bilduppsättningar kan du även förhandsgranska en resurs med de förinställningar för visningsprogram som du har skapat. Du kan också använda bildförinställningar för att förhandsgranska återgivningar av bilder.

* [Använda bildförinställningar](/help/assets/image-presets.md)
* [Använda visningsförinställningar](/help/assets/viewer-presets.md)

>[!NOTE]
>
>När du är på en webbsida (Sites) i AEM kan du inte förhandsgranska resurser i **redigeringsläget**. Du måste gå till läget **Förhandsgranska** genom att klicka på **Förhandsgranska** i det övre högra hörnet på sidan.

Information om hur du aktiverar eller inaktiverar visningsförinställningar i användargränssnittet finns i [Hantera visningsförinställningar](/help/assets/managing-viewer-presets.md).

**Förhandsgranska resurser med hjälp av programgränssnittet**

1. Från **[!UICONTROL Adobe Experience Manager]**, på sidan **[!UICONTROL Navigation]**, tryck på **[!UICONTROL Assets]** och sedan **[!UICONTROL Files]** för att komma åt resurser.
1. Tryck på **[!UICONTROL List View.]** i den nedrullningsbara listan **[!UICONTROL View]** i sidans övre högra hörn
1. (Valfritt) Använd kolumnen **[!UICONTROL Type]** för att sortera resurserna efter den typ som du vill förhandsgranska.
1. Klicka på titelnamnet (inte miniatyrbilden) för resursen som du vill förhandsgranska i kolumnen **[!UICONTROL Title]**.
1. Beroende på vilken resurstyp du klickade på gör du något av följande:


   <table>
    <tbody>
      <tr>
      <td><strong>Resurstyp som du klickade på</strong><br /> </td>
      <td><strong>Kan du förhandsgranska mediefilen i en viss återgivning?</strong></td>
      <td><strong>Kan du förhandsgranska resurser i ett visningsprogram?</strong></td>
      <td> </td>
      </tr>
      <tr>
      <td><p>3D</p> </td>
      <td>Nej</td>
      <td>Ja</td>
      <td><p><strong>Förhandsgranska en 3D-resurs i Dimensional Viewer</strong></p>
      <ul>
      <li>Klicka på ikonen i det övre vänstra hörnet av sidan så att listrutan visas. Klicka på <strong>Visningsprogram</strong> i listan och välj sedan Dimensional Viewer.</li>
      <li>Tryck på <strong>Återställ</strong> om du vill återställa bilden till den ursprungliga zoomningen.</li>
      <li>Tryck på <strong>Helskärm</strong> för att maximera visningsprogrammet på visningsenheten.</li>
      </ul>
      <p><strong>Navigera i 3D-scenen</strong></p>
      <ul>
      <li><p><strong>Vrid din 3D-kamera</strong>  - rotera din vy runt 3D-motivet och objekten.</p> Mus: Vänsterklicka och dra. </p> Pekskärm: Tryck på + dra.</p></li>
      <li><p><strong>Panorera kameran</strong>  - Panorera åt vänster, åt höger, uppåt och nedåt.</p> Mus: Högerklicka och dra. </p> Pekskärm: Tryck med två fingrar och dra.</p></li>
      <li><p><strong>Zooma kameran</strong>  - Zooma kameran för att flytta in och ut i områden i 3D-scenen.</p> Mus: Rullningshjul. </p> Pekskärm: Fingernyp.</p></li>
      <li><p><strong>Centrera kameran</strong>  igen - Ändra visningsläget runt 3D-scenen och -objekten.</p> Mus: Dubbelklicka. </p> Pekskärm: Dubbeltryck.</li></ul></td>
      </tr>
      <tr>
      <td><p>Bild</p> </td>
      <td>Ja</td>
      <td>Ja</td>
      <td><p><strong>Så här förhandsgranskar du en resurs i en viss återgivning</strong></p>
      <ul>
      <li>Klicka på ikonen i det övre vänstra hörnet av sidan så att listrutan visas. Klicka på <strong>Återgivningar </strong>i listan och välj sedan en viss återgivning som du vill förhandsgranska.</li>
      </ul> <p><strong>Förhandsgranska resurs i ett visst visningsprogram</strong></p>
      <ul>
      <li>Klicka på ikonen i det övre vänstra hörnet av sidan så att listrutan visas. Klicka på <strong>Tittare</strong> i listan och välj sedan ett visningsprogram som du vill använda för resursen.</li>
      </ul> <p>Använd ikonerna <strong>+</strong> och <strong>-</strong> för att öka respektive minska zoomningen för den markerade bilden. Klicka på <strong>Återställ</strong> om du vill återställa bilden till den ursprungliga zoomningen.<br /> Om du använder en pekskärm kan du zooma in steg för att dubbeltrycka på bilden. När du har uppnått maximal zoom dubbeltrycker du på bilden igen för att återställa zoomläget. Dra över bilden för att panorera.</p> </td>
      </tr>
      <tr>
      <td>Multimedia</td>
      <td>Ja</td>
      <td>Ja</td>
      <td><p><strong>Så här förhandsgranskar du en resurs i en viss återgivning</strong></p>
      <ul>
      <li>Klicka på ikonen i det övre vänstra hörnet av sidan så att listrutan visas. Klicka på <strong>Återgivningar </strong>i listan och välj sedan en viss återgivning som du vill förhandsgranska.</li>
      </ul> <p>Om du väljer en videoåtergivning med högre upplösning för förhandsgranskning kan videon bli trunkerad. Det beror på att återgivningsförhandsvisningen visar exakt den upplösning som kunderna kommer att se, allt i kontexten för det inbäddade visningsprogrammet som används för förhandsgranskningen.</p> <p>När du förhandsgranskar en adaptiv videouppsättning på resursnivå grupperas återgivningarna i en uppspelningsupplevelse. Det innebär att den adaptiva videon har rätt storlek för visning och uppspelning med den bästa upplösningen i visningsenhetens kontext och anslutningshastigheten.<br /> </p> <p><strong>Förhandsgranska en resurs i ett visst visningsprogram</strong></p>
      <ul>
      <li>Klicka på ikonen i det övre vänstra hörnet av sidan så att listrutan visas. Klicka på <strong>Tittare</strong> i listan och välj sedan ett visningsprogram som du vill använda för resursen.</li>
      </ul> </td>
      </tr>
      <tr>
      <td>Bilduppsättning</td>
      <td>Nej</td>
      <td>Ja</td>
      <td><p><strong>Förhandsgranska en resurs i ett visst visningsprogram</strong></p>
      <ul>
      <li>Klicka på ikonen i det övre vänstra hörnet av sidan så att listrutan visas. Klicka på <strong>Tittare</strong> i listan och välj sedan ett visningsprogram som du vill använda för resursen.</li>
      </ul> <p>Använd ikonerna <strong>+</strong> och <strong>-</strong> för att öka respektive minska zoomningen för den markerade bilden. Klicka på <strong>Återställ</strong> om du vill återställa bilden till den ursprungliga zoomningen.<br /> Om du använder en pekskärm kan du zooma in steg för att dubbeltrycka på bilden. När du har uppnått maximal zoom dubbeltrycker du på bilden igen för att återställa zoomläget. Dra över bilden för att panorera.</p> </td>
      </tr>
      <tr>
      <td>Rotation</td>
      <td>Nej</td>
      <td>Ja</td>
      <td><p><strong>Förhandsgranska en resurs i ett visst visningsprogram</strong></p>
      <ul>
      <li>Klicka på ikonen i det övre vänstra hörnet av sidan så att listrutan visas. Klicka på <strong>Tittare</strong> i listan och välj sedan ett visningsprogram som du vill använda för resursen.</li>
      </ul> <p>Använd ikonerna <strong>+</strong> och <strong>-</strong> för att öka respektive minska zoomningen för den markerade bilden. Klicka på <strong>Återställ</strong> om du vill återställa bilden till den ursprungliga zoomningen.<br /> Om du använder en pekskärm kan du zooma in steg för att dubbeltrycka på bilden. När du har uppnått maximal zoom dubbeltrycker du på bilden igen för att återställa zoomläget. Dra över bilden för att panorera.</p> </td>
      </tr>
      <tr>
      <td>Blandad medieuppsättning</td>
      <td>Nej</td>
      <td>Ja</td>
      <td><p><strong>Förhandsgranska en resurs i ett visst visningsprogram</strong></p>
      <ul>
      <li>Klicka på ikonen i det övre vänstra hörnet av sidan så att listrutan visas. Klicka på <strong>Tittare</strong> i listan och välj sedan ett visningsprogram som du vill använda för resursen.</li>
      </ul> <p>Använd ikonerna <strong>+</strong> och <strong>-</strong> för att öka respektive minska zoomningen för den markerade bilden. Klicka på <strong>Återställ</strong> om du vill återställa bilden till den ursprungliga zoomningen.<br /> Om du använder en pekskärm kan du zooma in steg för att dubbeltrycka på bilden. När du har uppnått maximal zoom dubbeltrycker du på bilden igen för att återställa zoomläget. Dra över bilden för att panorera.</p> </td>
      </tr>
      <tr>
      <td>Carousel set</td>
      <td>Nej</td>
      <td>Ja</td>
      <td><strong>Förhandsgranska en resurs i ett visst visningsprogram</strong>
      <ul>
      <li>Klicka på ikonen i det övre vänstra hörnet av sidan så att listrutan visas. Välj ett visningsprogram som du vill använda för resursen.</li>
      </ul> </td>
      </tr>
      <tr>
      <td>360-video<br /> </td>
      <td>Ja</td>
      <td>Ja</td>
      <td><p><strong>Så här förhandsgranskar du en resurs i en viss återgivning</strong></p>
      <ul>
      <li>I närheten av sidans övre vänstra hörn trycker du på ikonen så att listrutan visas. Välj <strong>Återgivningar</strong> och välj sedan den återgivning som du vill förhandsgranska.</li>
      </ul> <p><strong>Förhandsgranska resurs i ett visst visningsprogram</strong></p>
      <ul>
      <li>I närheten av sidans övre vänstra hörn trycker du på ikonen så att listrutan visas. Välj <strong>Visare</strong> och välj sedan ett visningsprogram som du vill använda för resursen.</li>
      </ul> <p>Använd ikonerna <strong>+</strong> och <strong>-</strong> för att öka respektive minska zoomningen för den markerade bilden. Klicka på <strong>Återställ</strong> om du vill återställa bilden till den ursprungliga zoomningen.<br /> Om du använder en pekskärm kan du zooma in steg för att dubbeltrycka på bilden. När du har uppnått maximal zoom dubbeltrycker du på bilden igen för att återställa zoomläget. Dra över bilden för att panorera.</p> </td>
      </tr>
    </tbody>
    </table>

## Förhandsgranska resurser med ett tangentbord {#keyboard-navigation-asset-preview}

1. Navigera från användargränssnittet Resurser till en mapp som innehåller en resurs som du vill förhandsgranska.

1. Tryck på `<Tab>`-tangenten eller piltangenterna på tangentbordet för att markera resursen i mappen.

1. Tryck på `<Enter>` för att öppna den markerade resursen i förhandsgranskningsläge.

1. Gör något av följande:

   * Om du vill zooma in trycker du på `<Tab>` för att flytta fokus till ikonen för inzoomning (+) och sedan på `<Enter>` en eller flera gånger för att zooma in inkrementellt.

   * Om du vill zooma ut trycker du på `<Tab>` för att flytta fokus till ikonen för att zooma ut (-) och sedan på `<Enter>` en eller flera gånger för att zooma ut stegvis.

   * Om du vill flytta vyn för en *zoomad*-resurs vågrätt eller lodrätt trycker du på respektive piltangent.

   * Tryck på `<Shift>` + `<Tab>` för att återställa vyn och placera fokus på resursen igen.
