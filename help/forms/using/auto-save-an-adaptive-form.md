---
title: Spara ett anpassat formulär automatiskt
seo-title: Auto-save an adaptive form
description: Du kan konfigurera ett adaptivt formulär så att innehållet automatiskt börjar sparas baserat på en händelse eller ett fördefinierat tidsintervall
seo-description: You can configure an adaptive form to automatically start saving the content based on an event or a pre-defined time-interval
uuid: 0fe9a389-269b-438a-9489-d9d1d09558a1
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: d519ac4e-6d29-4a69-874e-792acabe87ff
feature: Adaptive Forms
exl-id: 948b2c12-895d-49e3-a943-d8fe87174fc4
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '645'
ht-degree: 0%

---

# Spara ett anpassat formulär automatiskt {#auto-save-an-adaptive-form}

Du kan konfigurera ett anpassningsbart formulär så att innehållet automatiskt börjar sparas baserat på en händelse eller ett fördefinierat tidsintervall. Som standard sparas innehållet i ett anpassat formulär när användaren gör något, t.ex. när knappen Spara trycks ned. Alternativet Spara automatiskt är användbart i:

* Spara automatiskt innehållet för anonyma och inloggade användare
* Spara innehållet i ett formulär utan att användaren behöver göra något eller inte alls
* Börja spara innehåll i ett formulär baserat på en användarhändelse
* Spara innehållet i ett formulär upprepade gånger efter ett angivet tidsintervall

## Aktivera automatiskt sparande för ett anpassat formulär {#enable-autosave-for-an-adaptive-form}

Alternativet för att spara automatiskt är inte aktiverat i ett anpassat formulär. Du kan aktivera alternativet för att spara automatiskt på **Spara automatiskt** i egenskaperna för ett adaptivt formulär. The **Spara automatiskt** innehåller även flera andra konfigurationsalternativ. Utför följande steg för att aktivera och konfigurera alternativet för att spara automatiskt för ett anpassat formulär:

1. Markera en komponent och tryck sedan på ![fältnivå](assets/field-level.png) > **[!UICONTROL Adaptive Form Container]** och sedan trycka ![cmppr](assets/cmppr.png).
1. I **[!UICONTROL Auto Save]** sektion, **[!UICONTROL Enable]** alternativet för att spara automatiskt.
1. I **[!UICONTROL Adaptive Form Event]** anger du 1 eller TRUE för att automatiskt börja spara formuläret när formuläret läses in i webbläsaren. Du kan också ange ett villkorsuttryck för en händelse som när den aktiveras och returnerar true börjar spara formulärets innehåll.
1. Ange utlösaren. Automatiskt sparande aktiveras baserat på din konfiguration. Dina alternativ är:

   * **[!UICONTROL Time based:]** Välj alternativet för att börja spara innehållet baserat på ett visst tidsintervall.
   * **[!UICONTROL Event based:]** Välj alternativet för att börja spara innehållet baserat på när en händelse utlöses.

   När du väljer en utlösare aktiveras rutan Strategisk konfiguration. I rutan Strategisk konfiguration kan du:

   * Ange ett tidsintervall om du väljer **[!UICONTROL Time based]** utlösare.
   * Ange ett händelsenamn om du väljer **[!UICONTROL Event based]** utlösare.

   Du kan också skapa och lägga till en egen anpassad strategi i listan. Mer information finns i [Implementera en anpassad strategi för att automatiskt spara formulären](/help/forms/using/auto-save-an-adaptive-form.md#p-implement-a-custom-strategy-to-enable-autosave-for-adaptive-forms-p).

1. (Endast tidsbaserad autosparfunktion) Utför följande steg för att konfigurera alternativ för tidsbaserad autosparning.

   1. I **[!UICONTROL Auto save on this interval]** anger du tidsintervallet i sekunder. Formuläret sparas upprepade gånger efter det antal sekunder som anges i intervallrutan.

1. (Endast händelsebaserad autosparning) Utför följande steg för att konfigurera alternativ för händelsebaserad autosparning.

   1. I **Spara automatiskt efter den här händelsen** ruta, ange [GuideBridge](https://helpx.adobe.com/aem-forms/6/javascript-api/GuideBridge.html) -händelse. Formuläret sparas varje gång uttrycket utvärderas till TRUE.

1. (Valfritt) Om du vill spara innehållet automatiskt för anonyma användare väljer du **Aktivera Spara automatiskt för anonyma användare** och klicka **[!UICONTROL OK]**.

   >[!NOTE]
   >
   >Om du vill att alternativet Spara automatiskt ska fungera för anonyma användare måste du konfigurera Forms Common Configuration Service så att alla användare kan förhandsgranska, verifiera och signera formulär.
   >
   >Om du vill konfigurera tjänsten går du till AEM Web Console-konfiguration på `https://server:port/system/console/configMgr` och redigera **[!UICONTROL Forms Common Configuration Service]** för att välja **[!UICONTROL All Users]** i **[!UICONTROL Allow]** och spara konfigurationen.

## Implementera en anpassad strategi för att aktivera automatiskt sparande för anpassningsbara formulär {#implement-a-custom-strategy-to-enable-autosave-for-adaptive-forms}

Du kan implementera en anpassad händelse för att aktivera autosparfunktionen. Utför följande steg för att skapa och implementera den anpassade händelsen:

1. Skapa biblioteksmappar och biblioteksmappar för klienter. Detaljerade anvisningar finns i [Använda biblioteksdokument på klientsidan](/help/sites-developing/clientlibs.md).

   Följande skript använder till exempel den anpassade `emailFocusChange`-händelse som utlöser autosparfunktionen:

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

1. Markera en komponent i redigeringsläget och tryck sedan på ![fältnivå](assets/field-level.png) > **[!UICONTROL Adaptive Form Container]** och sedan trycka ![cmppr](assets/cmppr.png).
1. I egenskaperna öppnar du **[!UICONTROL Basic]** -avsnitt. I **[!UICONTROL Client Library Category]** anger du värdet för kategoriegenskapen som definierades när klientbiblioteksmapparna skapades.
1. Öppna avsnittet Spara automatiskt. I **[!UICONTROL Auto save after this event]** anger du en anpassad händelse som redan definierats i klientbiblioteket. Klicka på **[!UICONTROL OK]**.
