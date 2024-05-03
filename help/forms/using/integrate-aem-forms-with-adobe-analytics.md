---
title: Hur integrerar man AEM Forms med Adobe Analytics?
description: AEM Forms kan integreras med Adobe Analytics för att inhämta och spåra prestandamått för era publicerade formulär.
docset: aem65
exl-id: 030fe9f2-cd41-4290-b8a6-2f9ade6b5789
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '1561'
ht-degree: 0%

---

# Analyser med [!DNL Adobe Launch] {#analyticsusingadobelaunch}

AEM Forms kan integreras med [Adobe Analytics](https://experienceleague.adobe.com/docs/analytics-learn/tutorials/overview.html?lang=en) så att ni kan hämta in och spåra resultatvärden för era publicerade formulär. Syftet med att analysera dessa värden är att göra det möjligt för företagsanvändare att få insikter i slutanvändarnas beteende och optimera datainhämtningsupplevelsen. Du kan fånga in och spåra beteenden hos både inloggade och ej inloggade (anonyma) användare via Adobe Analytics för Adaptiv Forms.

Du kan också utföra analyser med Cloud Service Framework. Mer information om hur du integrerar AEM Forms med Cloud Service Framework finns i [Analyser med hjälp av Cloud Service Framework](/help/forms/using/configure-analytics-forms-documents.md). Den största fördelen med att använda Adobe Launch framför Analytics med Cloud Service Framework är att du även kan definiera anpassade händelser, utöver dessa i paketet-händelser. De anpassade händelserna definieras med regelredigeraren eller kundklienten och mappas till händelser i [!DNL Adobe Analytics].

När du har utfört de åtgärder som nämns i den här artikeln kan du konfigurera och visa rapporter i [!DNL Adobe Analytics], vilket visas i följande video:

>[!VIDEO](https://video.tv.adobe.com/v/337262)

Du kan använda [!DNL Adobe Analytics] för att upptäcka interaktionsmönster och problem som användare möter när de använder adaptiva formulär. Ut ur lådan, [!DNL Adobe Analytics] spårar och lagrar information om följande händelser:

* **Återgivning**: Antal gånger ett formulär öppnas.

* **Skicka**: Antal gånger ett formulär skickas.

* **Abandon**: Antal gånger som användarna lämnar utan att fylla i formuläret.

* **Fel**: Antal fel som påträffats på panelen och i panelens fält.

* **Hjälp**: Antal gånger en användare öppnar hjälpen för en panel och fälten på panelen.

* **Fältbesök**: Antal gånger en användare besöker ett fält i formuläret.

* **Spara**: Antal gånger som användare sparar ett formulär på Forms Portal.

Förutom de här out-of-box-händelserna kan du även definiera anpassade händelser.

Följande bild visar vilka åtgärder du behöver utföra innan du visar rapporter i [!DNL Adobe Analytics]:

![Analytics - översikt](/help/forms/using/assets/analyticsworkflow.png)

## 1. Konfigurera [!DNL Adobe Analytics] {#Configure-adobe-analytics}

Före konfigurering [!DNL Adobe Analytics], skapa:

* En Adobe ID att logga in på [Adobe Experience Cloud](https://experience.adobe.com/#/home).
* A [rapportsvit](https://experienceleague.adobe.com/docs/analytics/admin/manage-report-suites/new-report-suite/t-create-a-report-suite.html).


### Installera AEM Forms och [!DNL Adobe Analytics] tillägg {#install-extensions}

Så här konfigurerar du AEM Forms och [Adobe Analytics](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/analytics/overview.html) tillägg:

1. Logga in på Adobe Experience Cloud och välj ett namn för företaget.

1. Välj **[!UICONTROL Launch/Data Collection]** och markera **[!UICONTROL Go to Launch/Data Collection]**.

1. Välj **[!UICONTROL New property]** och ange ett namn för konfigurationen.

1. Ange ett domännamn och välj **[!UICONTROL Save]** för att spara egenskapen.

1. Välj det konfigurationsnamn som finns i listan Taggegenskaper.

1. I **[!UICONTROL Authoring]** avsnitt, markera **[!UICONTROL Extensions]**.

1. Välj **[!UICONTROL Catalog]** och markera **[!UICONTROL Install]** för **[!UICONTROL Adobe Experience Manager Forms]** tillägg. **[!UICONTROL Adobe Experience Manager Forms]** visas i listan över installerade tillägg som är tillgängliga i **Installerad** -fliken.

1. Välj **[!UICONTROL Install]** för **[!UICONTROL Adobe Analytics]** tillägg.
1. Välj rapportsvitens namn i dialogrutan **[!UICONTROL Development Report Suites]**, **[!UICONTROL Staging Report Suites]** och **[!UICONTROL Product Report Suites]** nedrullningsbara listor och välj **[!UICONTROL Save]** för att spara tillägget.

### Konfigurera dataelement {#configure-data-elements}

Du kan välja vilket som helst av de konfigurerade dataelementen i en regel som skapas för en händelse. När en händelse inträffar i ett adaptivt formulär skickar AEM Forms dessa dataelement till [!DNL Adobe Analytics].

När du har installerat **[!UICONTROL Adobe Experience Manager Forms]** kan du skapa följande dataelement:

<table>
 <tbody>
  <tr>
   <td>FieldName</th>
   <td>FieldTitle</th>
   <td>FormInstance</th>
  </tr>
  <tr>
   <td>FormName<br /> </td>
   <td>FormTitle<br /> </td>
   <td>PageName</td>
  </tr>
  <tr>
   <td>PageURL<br /> </td>
   <td>PanelTitle<br /> </td>
   <td>TimeSpent</td>
  </tr>
 </tbody>
</table>

Utför följande steg för att konfigurera dataelement:

1. I **[!UICONTROL Authoring]** avsnitt, markera **[!UICONTROL Data Elements]**.

1. Välj **[!UICONTROL Create New Data Element]**.

1. Ange ett namn för dataelementet. Exempel: Formulärtitel för dataelementtypen FormTitle.

1. Ange **[!UICONTROL Adobe Experience Manager Forms]** som tilläggsnamn.

1. Välj **[!UICONTROL Data Element Type]**.

1. Välj **[!UICONTROL Save]** för att spara dataelementet.

   >[!VIDEO](https://video.tv.adobe.com/v/337472)

### Konfigurera regler {#configure-rules}

Utför följande steg för att skapa regler baserade på **[!UICONTROL Adobe Experience Manager Forms]** tillägg:

1. I **[!UICONTROL Authoring]** avsnitt, markera **[!UICONTROL Rules]**.

1. Välj **[!UICONTROL Create New Rule]**.

1. Ange ett namn för regeln. Till exempel Skicka formulär för att registrera formulärinskickade formulär.

1. I **[!UICONTROL Events]** avsnitt, markera **[!UICONTROL Add]**.

1. Ange **[!UICONTROL Adobe Experience Manager Forms]** som tilläggsnamn.

1. Välj händelsetyp. Indata för **[!UICONTROL Name]** fylls i automatiskt baserat på den valda händelsetypen.

1. Välj **[!UICONTROL Keep Changes]** för att spara händelsen.

1. I **[!UICONTROL Actions]** avsnitt, markera **[!UICONTROL Add]**.

1. Ange **[!UICONTROL Adobe Analytics]** som tilläggsnamn.

1. Välj **[!UICONTROL Set Variables]** som åtgärdstyp. De alternativ som är tillgängliga i listrutan är bland annat:

   * **[!UICONTROL Set Variables]**: Använd den här åtgärdstypen för att definiera den händelsetyp som de markerade dataelementen skickas från AEM Forms till [!DNL Adobe Analytics].

   * **[!UICONTROL Send Beacon]**: Använd den här åtgärdstypen för att skicka data från AEM Forms till [!DNL Adobe Analytics].

   * **[!UICONTROL Clear Variables]**: Använd den här åtgärdstypen för att rensa dataspårningen så att händelsen bara registreras en gång i [!DNL Adobe Analytics].

     Rekommenderad metod är att använda **[!UICONTROL Set Variables]** åtgärdstyp för att konfigurera händelsen och dataelementen och sedan använda **[!UICONTROL Send Beacon]** för att skicka data och sedan använda **[!UICONTROL Clear Variables]** för att rensa dataspårningen.

1. I **[!UICONTROL Props]** mappa de alternativ för rapportsviten som finns i listrutan med dataelementen som definieras med [Konfigurera dataelement](#configure-data-elements).

   Till exempel att skicka **Formulärtitel** dataelement från AEM Forms [!DNL Adobe Analytics] när du skickar in ett formulär:
   1. I **[!UICONTROL Props]** väljer du ett utkast för Formulärtitel i rapportsviten och väljer sedan ![Databasikon](/help/forms/using/assets/database-icon.svg) för att mappa det till en formulärtitel som skapats i [Konfigurera dataelement](#configure-data-elements).

      ![define-props](/help/forms/using/assets/define-props.png)

   1. Välj **[!UICONTROL Add Another]** om du vill lägga till fler dataelement i listan.

1. I **[!UICONTROL Events]** väljer du en händelse bland de tillgängliga alternativen i rapportsviten och väljer **[!UICONTROL Keep Changes]**.

1. I **[!UICONTROL Actions]** väljer du + och anger **[!UICONTROL Adobe Analytics]** som tilläggsnamn.

1. Välj **[!UICONTROL Send Beacon]** som åtgärdstyp. Välj i den högra rutan **[!UICONTROL s.t()]** skicka data till [!DNL Adobe Analytics] och hantera det som en sidvy eller **[!UICONTROL s.tl()]** skicka data till [!DNL Adobe Analytics] och behandla det inte som en sidvy. Välj **[!UICONTROL Keep Changes]**.

1. I **[!UICONTROL Actions]** väljer du + och anger **[!UICONTROL Adobe Analytics]** som tilläggsnamn.

1. Välj **[!UICONTROL Clear Variables]** som åtgärdstyp. Välj **[!UICONTROL Keep Changes]**. När du har utfört dessa steg **[!UICONTROL Actions]** visas som:
   ![Åtgärdskonfiguration](/help/forms/using/assets/actions-config.png)

   Anpassa **[!UICONTROL Actions]** enligt dina krav. Du kan till exempel definiera två **Skicka Beacon** steg i ett åtgärdsflöde för att skicka data till [!DNL Adobe Analytics] och behandla det som en sidvy i ett enda steg och skicka data till [!DNL Adobe Analytics] och behandla det inte som en sidvy i det andra steget.

   ![Åtgärdskonfiguration](/help/forms/using/assets/actions-config-2.png)

1. Välj **[!UICONTROL Save]** för att spara regeln.

   Du kan skapa regler för alla händelsetyper, till exempel överge, Fel, fältbesök, Hjälp, Återge, Spara och Skicka.

   >[!VIDEO](https://video.tv.adobe.com/v/337425)


### Publiceringsflöden {#publish-flow}

När du har skapat dataelementen och använt dem i regler publicerar du konfigurationen för att samla in formulärdata i [!DNL Adobe Analytics].

Utför följande steg för att publicera konfigurationen:

1. I **[!UICONTROL Publishing]** avsnitt, markera **[!UICONTROL Publishing Flow]**.

1. Välj **[!UICONTROL Add Library]** och ange ett namn och välj miljö för biblioteket.

1. Välj **[!UICONTROL Add All Changed Resources]** och sedan **[!UICONTROL Save & Build to Development]**.

1. I **[!UICONTROL Development]** avsnitt, markera ![Fler alternativ](/help/forms/using/assets/more-options-icon.svg) och sedan **[!UICONTROL Approve & Publish to Production]**.

1. Bekräfta ändringarna och publiceringsflödet visas snart i **[!UICONTROL Published]** -avsnitt.

![Publiceringsflöde](/help/forms/using/assets/publish-flow.png)

## 2. Konfigurera AEM Forms {#configure-aem-forms}

Skapa en [Adobe IMS-konfiguration med Adobe Launch som molnlösning](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/integrations/experience-platform-launch/connect-aem-launch-adobe-io.html).

### Skapa startkonfiguration för Adobe {#create-adobe-launch-configuration}

Så här skapar du en konfiguration för Adobe Launch:

1. I AEM Forms Author går du till **[!UICONTROL Tools]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Adobe Launch Configurations]**.

1. Välj en mapp för att skapa konfigurationen och välj **[!UICONTROL Create]**.

1. Ange en rubrik för konfigurationen i dialogrutan **[!UICONTROL Title]** fält.

1. Välj [associerad Adobe IMS-konfiguration](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/integrations/experience-platform-launch/connect-aem-launch-adobe-io.html).

1. Välj namnet på företaget som användes när [konfigurera Adobe Analytics](#Configure-adobe-analytics).

1. Markera namnet på den egenskap som skapades när [konfigurera Adobe Analytics](#install-extensions).

1. Välj **[!UICONTROL Save & Close]**.

1. Publicera konfigurationen.

### Aktivera [!DNL Adobe Analytics] för en adaptiv blankett {#enable-analytics-adaptive-form}

Används [!DNL Adobe Launch] i en befintlig adaptiv form:

1. I AEM Forms Author går du till **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms & Documents]**.
1. Markera det adaptiva formuläret och välj **[!UICONTROL Properties]**.
1. I **[!UICONTROL Basic]** väljer du [konfigurationsbehållare](#create-adobe-launch-configuration) används när konfigurationen för Adobe Launch skapas.
1. Välj **[!UICONTROL Save & Close]**. Det adaptiva formuläret är aktiverat för [!DNL Adobe Analytics].
1. Publicera formuläret.

När du har aktiverat [!DNL Adobe Analytics] för ett anpassningsbart formulär kan du [validera](https://experienceleague.adobe.com/docs/launch-learn/implementing-in-websites-with-launch/implement-solutions/analytics.html?lang=en#validate-the-page-view-beacon) om ett datahändelseflöde finns mellan AEM Forms och [!DNL Adobe Analytics]. Integreringen av AEM Forms med Adobe Analytics är klar. Nu kan du [konfigurera och visa rapporter i Adobe Analytics](#view-reports-adobe-analytics).

>[!NOTE]
>Om båda [Analyser med hjälp av Cloud Service Framework](/help/forms/using/configure-analytics-forms-documents.md) och **Analyser med Adobe Launch** funktioner aktiveras samtidigt, **Analyser med Adobe Launch** har företräde.
> 

### Skapa regler för att hämta anpassade händelser (valfritt) {#capture-custom-events}

Skapa regler för specifika fält i ett adaptivt formulär med regelredigeraren för att skicka analysdata från ett adaptivt formulär till [!DNL Adobe Analytics].

I en tvåstegsprocess definierar du en regel för ett fält i ett anpassningsbart format. Regeln skickar en händelse. Namnet på händelsen mappas till en anpassad hämtningshändelse i Adobe Launch.

Så här skapar du regler med hjälp av regelredigeraren i ett anpassat format:

1. Markera fältet och välj ![Regelredigeraren](/help/forms/using/assets/rule-editor-icon.svg) för att öppna sidan för regelredigeraren.
1. Definiera ett villkor i [!UICONTROL When] -delen av regeln.
1. I [!UICONTROL Then] regelavsnitt, markera **[!UICONTROL Dispatch Event]** från **[!UICONTROL Select Action]** listruta.
1. Ange namnet på händelsen i **[!UICONTROL Type Event Name]** fält.

Om födelsedatumet till exempel är före ett visst datum skickar AEM Forms **Säkerhet** -händelse.

![Utsändningshändelse](/help/forms/using/assets/security-event.png)

Mappa händelsen till en anpassad hämtningshändelse i [!DNL Adobe Analytics]:

1. [Skapa en regel](#configure-rules).

1. I **[!UICONTROL Events]** avsnitt, markera **[!UICONTROL Add]**.

1. Ange **[!UICONTROL Adobe Experience Manager Forms]** som tilläggsnamn.

1. Välj **[!UICONTROL Capture Custom Event]** från **[!UICONTROL Event Type]** listruta.

1. Ange namnet på händelsen som du angav i steg 4 när du skapade en regel med regelredigeraren.

1. Välj **Behåll ändringar** och utför resten av åtgärderna som anges i [Konfigurera regler](#configure-rules).

## 3. Konfigurera och visa rapporter i [!DNL Adobe Analytics] {#view-reports-adobe-analytics}

När ett adaptivt formulär har konfigurerats för att skicka händelsedata till [!DNL Adobe Analytics]kan du börja visa rapporter i [!DNL Adobe Analytics]:

1. Välj ![Välj produkt](/help/forms/using/assets/select-analytics.png) och markera **[!UICONTROL Analytics]**.

1. Välj **[!UICONTROL Create Project]** och markera **[!UICONTROL Blank project]**.

1. Välj rapportsvitens namn i listrutan högst upp till höger på frihandsformuläret.

1. Ange **Formulärtitel** i **[!UICONTROL Search dimension items]** text för att visa alla formulärtitlar.

1. Släpp den anpassningsbara formulärtiteln på **[!UICONTROL Drop a segment here (or any other component)]** textruta.

1. Från **[!UICONTROL Metrics]** -avsnitt, släppa händelser att spåra till **[!UICONTROL Drop a metric here (or any other component)]** textruta.

1. Välj ![Visualiseringar](/help/forms/using/assets/visualization-icon.svg) och släpp en diagramtyp i avsnittet Frihand. På samma sätt kan du lägga till flera diagramtyper i avsnittet Frihand.

1. Välj Ctrl + S och ange ett namn för att spara projektet.

Detaljerad information om hur du visar analysrapporter för formulär finns i [Visa och förstå AEM Forms analysrapporter](../../forms/using/view-understand-aem-forms-analytics-reports.md).
