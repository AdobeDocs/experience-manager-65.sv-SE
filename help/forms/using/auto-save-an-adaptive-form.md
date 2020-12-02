---
title: Spara ett anpassat formulär automatiskt
seo-title: Spara ett anpassat formulär automatiskt
description: Du kan konfigurera ett adaptivt formulär så att innehållet automatiskt börjar sparas baserat på en händelse eller ett fördefinierat tidsintervall
seo-description: Du kan konfigurera ett adaptivt formulär så att innehållet automatiskt börjar sparas baserat på en händelse eller ett fördefinierat tidsintervall
uuid: 0fe9a389-269b-438a-9489-d9d1d09558a1
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: d519ac4e-6d29-4a69-874e-792acabe87ff
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '669'
ht-degree: 0%

---


# Spara ett anpassat formulär automatiskt {#auto-save-an-adaptive-form}

Du kan konfigurera ett anpassningsbart formulär så att innehållet automatiskt börjar sparas baserat på en händelse eller ett fördefinierat tidsintervall. Som standard sparas innehållet i ett anpassat formulär när användaren gör något, t.ex. när knappen Spara trycks ned. Alternativet Spara automatiskt är användbart i:

* Spara automatiskt innehållet för anonyma och inloggade användare
* Spara innehållet i ett formulär utan att användaren behöver göra något eller inte alls
* Börja spara innehåll i ett formulär baserat på en användarhändelse
* Spara innehållet i ett formulär upprepade gånger efter ett angivet tidsintervall

## Aktivera automatiskt sparande för ett anpassat formulär {#enable-autosave-for-an-adaptive-form}

Alternativet för att spara automatiskt är inte aktiverat i ett anpassat formulär. Du kan aktivera alternativet för att spara automatiskt i avsnittet **Spara automatiskt** i egenskaperna för ett anpassat formulär. Avsnittet **Spara automatiskt** innehåller även flera andra konfigurationsalternativ. Utför följande steg för att aktivera och konfigurera alternativet för att spara automatiskt för ett anpassat formulär:

1. Om du vill öppna avsnittet Spara automatiskt i egenskaperna markerar du en komponent, trycker på ![fältnivå](assets/field-level.png) > **[!UICONTROL Adaptive Form Container]** och sedan på ![cmpr](assets/cmppr.png).
1. I avsnittet **[!UICONTROL Auto Save]** **[!UICONTROL Enable]** väljer du alternativet för att spara automatiskt.
1. I rutan **[!UICONTROL Adaptive Form Event]** anger du 1 eller TRUE för att automatiskt börja spara formuläret när formuläret läses in i webbläsaren. Du kan också ange ett villkorsuttryck för en händelse som när den aktiveras och returnerar true börjar spara formulärets innehåll.
1. Ange utlösaren. Automatiskt sparande aktiveras baserat på din konfiguration. Dina alternativ är:

   * **[!UICONTROL Time based:]** Välj alternativet för att börja spara innehållet baserat på ett visst tidsintervall.
   * **[!UICONTROL Event based:]** Välj alternativet för att börja spara innehållet baserat på när en händelse utlöses.

   När du väljer en utlösare aktiveras rutan Strategisk konfiguration. I rutan Strategisk konfiguration kan du:

   * Ange ett tidsintervall om du väljer **[!UICONTROL Time based]**-utlösare.
   * Ange ett händelsenamn om du väljer **[!UICONTROL Event based]**-utlösare.

   Du kan också skapa och lägga till en egen anpassad strategi i listan. Mer information finns i [Implementera en anpassad strategi för att automatiskt spara formulären](/help/forms/using/auto-save-an-adaptive-form.md#p-implement-a-custom-strategy-to-enable-autosave-for-adaptive-forms-p).

1. (Endast tidsbaserad autosparfunktion) Utför följande steg för att konfigurera alternativ för tidsbaserad autosparning.

   1. Ange tidsintervallet i sekunder i rutan **[!UICONTROL Auto save on this interval]**. Formuläret sparas upprepade gånger efter det antal sekunder som anges i intervallrutan.

1. (Endast händelsebaserad autosparning) Utför följande steg för att konfigurera alternativ för händelsebaserad autosparning.

   1. I rutan **Spara automatiskt efter den här händelsen** anger du en [GuideBridge](https://helpx.adobe.com/aem-forms/6/javascript-api/GuideBridge.html)-händelse. Formuläret sparas varje gång uttrycket utvärderas till TRUE.

1. (Valfritt) Om du vill spara innehållet automatiskt för anonyma användare väljer du alternativet **Aktivera automatiskt sparande för anonyma användare** och klickar på **[!UICONTROL OK]**.

   >[!NOTE]
   >
   >Om du vill att alternativet Spara automatiskt ska fungera för anonyma användare måste du konfigurera Forms Common Configuration Service så att alla användare kan förhandsgranska, verifiera och signera formulär.
   >
   >Om du vill konfigurera tjänsten går du till AEM Web Console-konfiguration på `https://server:port/system/console/configMgr` och redigerar **[!UICONTROL Forms Common Configuration Service]** för att välja alternativet **[!UICONTROL All Users]** i fältet **[!UICONTROL Allow]** och sparar konfigurationen.

## Implementera en anpassad strategi för att aktivera automatiskt sparande för adaptiva formulär {#implement-a-custom-strategy-to-enable-autosave-for-adaptive-forms}

Du kan implementera en anpassad händelse för att aktivera autosparfunktionen. Utför följande steg för att skapa och implementera den anpassade händelsen:

1. Skapa biblioteksmappar och biblioteksmappar för klienter. Detaljerade steg finns i [Using Client-Side Libraries document](/help/sites-developing/clientlibs.md).

   Följande skript använder till exempel den anpassade `emailFocusChange`händelsen för att aktivera autosparfunktionen:

   ```javascript
   window.addEventListener("bridgeInitializeStart", function (){
       guideBridge.connect(function () { guideBridge.on("elementFocusChanged", function (event,data) {
           if(data.target.name === 'Email') {
               guideBridge.trigger("emailFocusChange");
           }
       });
      });
   });
   ```

   >[!NOTE]
   >
   >En kategoriegenskap definieras när klientbiblioteksmapparna skapas. Behåll värdet som tilldelats till kategoriegenskapen.

1. Öppna det adaptiva formuläret i redigeringsläge.

1. Markera en komponent i redigeringsläget, tryck sedan på ![fältnivå](assets/field-level.png) > **[!UICONTROL Adaptive Form Container]** och sedan på ![cmpr](assets/cmppr.png).
1. Öppna avsnittet **[!UICONTROL Basic]** i egenskaperna. I rutan **[!UICONTROL Client Library Category]** anger du värdet för kategoriegenskapen som definierades när klientbiblioteksmapparna skapades.
1. Öppna avsnittet Spara automatiskt. I rutan **[!UICONTROL Auto save after this event]** anger du en anpassad händelse som redan har definierats i klientbiblioteket. Klicka på **[!UICONTROL OK]**.

