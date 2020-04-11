---
title: Arbeta i offlineläge
seo-title: Arbeta i offlineläge
description: Ta din mobila enhet offline utanför ditt AEM Forms-nätverk eller i offlineläge och arbeta med appen AEM Forms
seo-description: Ta din mobila enhet offline utanför ditt AEM Forms-nätverk eller i offlineläge och arbeta med appen AEM Forms
uuid: b900a0f8-90ce-486a-bde6-6cdf11bd2801
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 9a3c6ab4-8bb9-40c7-8c56-59153b364887
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317

---


# Arbeta i offlineläge {#working-in-the-offline-mode}

Med offlineläget i appen AEM Forms kan du arbeta smidigt även om appen är offline. Du kan öppna, uppdatera och skicka ett formulär utan att behöva ansluta till nätverket.

Du börjar arbeta med appen AEM Forms genom att synkronisera appen med AEM Forms-servern. Alla formulär som du har tilldelats hämtas i din app. För AEM Forms på JEE hämtas uppgifter på fliken Åtgärder och startpunkter som är kopplade till formulär och andra formulär på fliken Formulär. För AEM Forms på OSGi läses endast Forms in på fliken Forms.

Mer information om hur du synkroniserar appen finns i [Synkronisera appen](/help/forms/using/sync-app.md).

## Göra formulär tillgängliga offline {#making-forms-available-offline}

När du synkroniserar din app med AEM Forms-servern hämtas formulären till din mobila enhet. Som standard hämtas dock inte de bilagor som är kopplade till formuläret. Det innebär att om du är online kan du visa de bifogade filerna. Om du vill se den bifogade filen i offlineläge kan du dock ändra standardinställningarna i programmet.

Om du vill vara säker på att de associerade bilagorna hämtas med varje formulär anger du ON för Hämta bilagor. Mer information finns i [Uppdatera allmänna inställningar](/help/forms/using/update-general-settings.md).

Eftersom nedladdning av data på den mobila enheten kan påverka enhetens prestanda är inställningen Hämta bilagor inställd på AV som standard. Bifogade filer hämtas till enheten för varje åtgärd som hämtas från servern efter att inställningen har uppdaterats till PÅ. I offlineläget kan en användare sedan arbeta med alla uppgifter som hämtas till en enhet efter att ha angett alternativet **Hämta bilagor** till PÅ.

## Konfigurera offlinetjänst för appen AEM Forms {#configuring-offline-service-for-aem-forms-app-br}

AEM Forms-appen offline identifierar de resurser som används i ett formulär. Appen AEM Forms förlitar sig på den här tjänsten för att få information om formulärberoenden. Information om formulärberoenden krävs för att aktivera offlinefunktioner. Offlinetjänsten för AEM Forms-appen cachelagrar sökvägarna eller URL:erna för resurserna som används i ett formulär. Cachen uppdateras baserat på ändringarna i formuläret och giltighetsperioden som konfigurerats för offlinetjänsten. Cachelagring av sökvägar eller URL:er för resurserna som används i ett formulär förbättrar prestandan på serversidan.

Så här konfigurerar du offlinekomponenten på serversidan i AEM Forms-appen:

1. I författarinstansen går du till **Adobe Experience Manager** >**Verktyg** > **Formulär** > **Konfigurera Forms App Offline Service**.

   Webbadress: `https://<server>:<port>/<context-path>/libs/fd/workspace-offline/gui/content/config.html`

1. Under Allmänna inställningar kan du göra följande:

   * **Rensa cache**: Rensar serversidans cache för formulärberoenden.
   * **Återställ konfiguration**: Återställer AEM Forms-appens offlinekonfiguration.
   * **Cache Validity**: Specifies the validity period for the server-side offline cache.
   * **Resource Observation Paths**: Specifies paths where the offline service monitors for resource changes. If any changes occur in the specified paths, the offline cache of all dependent forms is updated. Exempel, `/etc/clientlibs/fd,/content/dam/images`.

1. In the **Manual Resource Cache** tab, specify the form dependencies offline service cannot identify. You can specify resources such as images loaded from within JavaScript. AEM Forms app will download these resources as well for the offline mode.
