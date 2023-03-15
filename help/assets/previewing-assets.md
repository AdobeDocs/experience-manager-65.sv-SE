---
title: Förhandsgranska resurser
description: Lär dig hur du förhandsgranskar resurser i Dynamic Media.
uuid: 09e97245-373b-4d50-8ba3-5d1034a29988
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: bb8c355c-4475-45ec-9096-0975f0ce2c27
docset: aem65
feature: Asset Management
role: User, Admin
exl-id: 84f0c406-4ab6-48c7-8223-61a8c3ade363
source-git-commit: 363e5159d290ecfbf4338f6b9793e11b613389a5
workflow-type: tm+mt
source-wordcount: '1357'
ht-degree: 1%

---

# Förhandsgranska resurser med hjälp av programgränssnittet {#previewing-assets}

Du kan använda Förhandsgranska för att se hur en digital resurs som du har överfört ser ut när den visas av en kund i deras egen webbläsare. Standardvisningsprogrammet för inbäddade enheter som är tilldelade resursen används för förhandsvisningen.

Ett visningsprogram är en samling med olika inställningar eller *förinställningar*, t.ex. visningsprogrammets visningsstorlek, zoombeteende, färgscheman, kanter och teckensnitt. Dessa förinställningar avgör hur användare visar mediefiler på sina datorskärmar och mobila enheter.

Förutom att använda den dedikerade förhandsvisningsfunktionen för video, snurra och bilduppsättningar kan du även förhandsgranska en resurs med de förinställningar för visningsprogram som du har skapat. Du kan också använda bildförinställningar för att förhandsgranska återgivningar av bilder.

* [Använd bildförinställningar](/help/assets/image-presets.md)
* [Använd förinställningar för visningsprogram](/help/assets/viewer-presets.md)

>[!NOTE]
>
>När du är på en webbsida (Sites) i Adobe Experience Manager kan du inte förhandsgranska resurser i **Redigera** läge. Gå till förhandsgranskningsläget genom att klicka på **[!UICONTROL Preview]** i det övre högra hörnet på sidan.

Information om hur du aktiverar eller inaktiverar visningsförinställningar i användargränssnittet finns i [Hantera visningsförinställningar](/help/assets/managing-viewer-presets.md).

**Så här förhandsgranskar du resurser med hjälp av programgränssnittet:**

1. Från **[!UICONTROL Adobe Experience Manager]**, på **[!UICONTROL Navigation]** sida, markera **[!UICONTROL Assets]** sedan **[!UICONTROL Files]** för att få tillgång till resurser.
1. Nära sidans övre högra hörn, från sidans övre högra hörn **[!UICONTROL View]** nedrullningsbar lista, välja **[!UICONTROL List View]**.
1. (Valfritt) Använd **[!UICONTROL Type]** för att sortera resurserna efter den typ som du vill förhandsgranska.
1. Under **[!UICONTROL Title]** klickar du på titelnamnet (inte miniatyrbilden) för resursen som du vill förhandsvisa.
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
      <li>Klicka på ikonen i det övre vänstra hörnet av sidan så att listrutan visas. Välj <strong>Tittare</strong> i listan och välj sedan Dimensional Viewer.</li>
      <li>Välj <strong>Återställ</strong> om du vill återställa bilden till den ursprungliga zoomningen.</li>
      <li>Välj <strong>Helskärm</strong> för att maximera visningsprogrammet på visningsenheten.</li>
      </ul>
      <p><strong>Navigera i 3D-scenen</strong></p>
      <ul>
      <li><p><strong>Vrid din 3D-kamera</strong> - Rotera vyn runt 3D-motivet och objekten.</p> Mus: Vänsterklicka + dra </p> Pekskärm: Tryck + dra</p></li>
      <li><p><strong>Panorera kameran</strong> - Panorera vyn åt vänster, åt höger, uppåt och nedåt.</p> Mus: Högerklicka + dra </p> Pekskärm: Tryck med två fingrar och dra</p></li>
      <li><p><strong>Zooma kameran</strong> - Zooma kameran så att du kan flytta in och ut från områden i 3D-scenen.</p> Mus: Rullhjul </p> Pekskärm: Fingernypa</p></li>
      <li><p><strong>Ange kameran igen</strong> - Rotera vyn runt 3D-motivet och objekten.</p> Mus: Dubbelklicka </p> Pekskärm: Dubbelknacka</li></ul></td>
      </tr>
      <tr>
      <td><p>Bild</p> </td>
      <td>Ja</td>
      <td>Ja</td>
      <td><p><strong>Så här förhandsgranskar du en resurs i en viss återgivning</strong></p>
      <ul>
      <li>Klicka på ikonen i det övre vänstra hörnet av sidan så att listrutan visas. Välj <strong>Återgivningar </strong>i listan väljer du en viss återgivning som du vill förhandsgranska.</li>
      </ul> <p><strong>Förhandsgranska resurs i ett visst visningsprogram</strong></p>
      <ul>
      <li>Klicka på ikonen i det övre vänstra hörnet av sidan så att listrutan visas. Välj <strong>Tittare</strong> i listan väljer du sedan ett visningsprogram som du vill använda för resursen.</li>
      </ul> <p>Använd <strong>+</strong> och <strong>-</strong> ikoner för att öka respektive minska zoomningen i den markerade bilden. Välj <strong>Återställ</strong> om du vill återställa bilden till den ursprungliga zoomningen.<br /> Om du använder en pekskärm kan du zooma in steg för att dubbeltrycka på bilden. När du har uppnått maximal zoom dubbeltrycker du på bilden igen för att återställa zoomläget. Dra över bilden för att panorera.</p> </td>
      </tr>
      <tr>
      <td>Multimedia</td>
      <td>Ja</td>
      <td>Ja</td>
      <td><p><strong>Så här förhandsgranskar du en resurs i en viss återgivning</strong></p>
      <ul>
      <li>Klicka på ikonen i det övre vänstra hörnet av sidan så att listrutan visas. Välj <strong>Återgivningar </strong>i listan väljer du en viss återgivning som du vill förhandsgranska.</li>
      </ul> <p>Om du väljer en videoåtergivning med högre upplösning för förhandsgranskning kan videon bli trunkerad. Problemet beror på att återgivningsförhandsvisningen visar exakt den upplösning som dina kunder kommer att se alla i kontexten för det inbäddade visningsprogrammet som används för förhandsgranskningen.</p> <p>När du förhandsgranskar en adaptiv videouppsättning på resursnivå grupperas återgivningarna i en uppspelningsupplevelse. Det innebär att den anpassningsbara videon storleksanpassas för visning och uppspelning med den bästa upplösningen för visningsenheten och anslutningshastigheten.<br /> </p> <p><strong>Förhandsgranska en resurs i ett visst visningsprogram</strong></p>
      <ul>
      <li>Klicka på ikonen i det övre vänstra hörnet av sidan så att listrutan visas. Välj <strong>Tittare</strong> i listan väljer du sedan ett visningsprogram som du vill använda för resursen.</li>
      </ul> </td>
      </tr>
      <tr>
      <td>Bilduppsättning</td>
      <td>Nej</td>
      <td>Ja</td>
      <td><p><strong>Förhandsgranska en resurs i ett visst visningsprogram</strong></p>
      <ul>
      <li>Klicka på ikonen i det övre vänstra hörnet av sidan så att listrutan visas. Välj <strong>Tittare</strong> i listan väljer du sedan ett visningsprogram som du vill använda för resursen.</li>
      </ul> <p>Använd <strong>+</strong> och <strong>-</strong> ikoner så att du kan öka eller minska zoomningen för den markerade bilden. Välj <strong>Återställ</strong> om du vill återställa bilden till den ursprungliga zoomningen.<br /> Om du använder en pekskärm kan du zooma in steg för att dubbeltrycka på bilden. När du har uppnått maximal zoom dubbeltrycker du på bilden igen för att återställa zoomläget. Dra över bilden för att panorera.</p> </td>
      </tr>
      <tr>
      <td>Rotation</td>
      <td>Nej</td>
      <td>Ja</td>
      <td><p><strong>Förhandsgranska en resurs i ett visst visningsprogram</strong></p>
      <ul>
      <li>Klicka på ikonen i det övre vänstra hörnet av sidan så att listrutan visas. Välj <strong>Tittare</strong> i listan väljer du sedan ett visningsprogram som du vill använda för resursen.</li>
      </ul> <p>Använd <strong>+</strong> och <strong>-</strong> ikoner för att öka respektive minska zoomningen i den markerade bilden. Välj <strong>Återställ</strong> om du vill återställa bilden till den ursprungliga zoomningen.<br /> Om du använder en pekskärm kan du zooma in steg för att dubbeltrycka på bilden. När du har uppnått maximal zoom dubbeltrycker du på bilden igen för att återställa zoomläget. Dra över bilden för att panorera.</p> </td>
      </tr>
      <tr>
      <td>Blandad medieuppsättning</td>
      <td>Nej</td>
      <td>Ja</td>
      <td><p><strong>Förhandsgranska en resurs i ett visst visningsprogram</strong></p>
      <ul>
      <li>Klicka på ikonen i det övre vänstra hörnet av sidan så att listrutan visas. Välj <strong>Tittare</strong> i listan väljer du sedan ett visningsprogram som du vill använda för resursen.</li>
      </ul> <p>Använd <strong>+</strong> och <strong>-</strong> ikoner för att öka respektive minska zoomningen i den markerade bilden. Välj <strong>Återställ</strong> om du vill återställa bilden till den ursprungliga zoomningen.<br /> Om du använder en pekskärm kan du zooma in steg för att dubbeltrycka på bilden. När du har uppnått maximal zoom dubbeltrycker du på bilden igen för att återställa zoomläget. Dra över bilden för att panorera.</p> </td>
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
      <li>I närheten av sidans övre vänstra hörn markerar du ikonen så att listrutan visas. Välj <strong>Återgivningar</strong>väljer du sedan den återgivning som du vill förhandsgranska.</li>
      </ul> <p><strong>Förhandsgranska resurs i ett visst visningsprogram</strong></p>
      <ul>
      <li>I närheten av sidans övre vänstra hörn markerar du ikonen så att listrutan visas. Välj <strong>Tittare</strong>väljer du sedan ett visningsprogram som du vill använda på resursen.</li>
      </ul> <p>Använd <strong>+</strong> och <strong>-</strong> ikoner för att öka respektive minska zoomningen i den markerade bilden. Välj <strong>Återställ</strong> om du vill återställa bilden till den ursprungliga zoomningen.<br /> Om du använder en pekskärm kan du zooma in steg för att dubbeltrycka på bilden. När du har uppnått maximal zoom dubbeltrycker du på bilden igen för att återställa zoomläget. Dra över bilden för att panorera.</p> </td>
      </tr>
    </tbody>
    </table>

## Förhandsgranska resurser med ett tangentbord {#keyboard-navigation-asset-preview}

1. Navigera från användargränssnittet Resurser till en mapp som innehåller en resurs som du vill förhandsgranska.

1. I mappen trycker du på `<Tab>` på tangentbordet för att välja resursen.

1. Tryck `<Enter>` så att du kan öppna den markerade resursen i förhandsgranskningsläge.

1. Gör något av följande:

   * Om du vill zooma in trycker du på `<Tab>` om du vill flytta fokus till ikonen för inzoomning (+) trycker du på `<Enter>` en eller flera gånger för att zooma in stegvis.
   * Om du vill zooma ut trycker du på `<Tab>` för att flytta fokus till ikonen för att zooma ut (-) och sedan trycka på `<Enter>` en eller flera gånger för att zooma ut stegvis.
   * Flytta vyn för en *zoomad* resurs vågrätt eller lodrätt, tryck på respektive piltangent.
   * Tryck `<Shift>` + `<Tab>` så att du kan återställa vyn och placera fokus tillbaka på resursen.
