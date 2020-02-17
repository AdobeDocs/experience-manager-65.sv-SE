---
title: Skriva anpassad skickaåtgärd för anpassningsbara formulär
seo-title: Skriva anpassad skickaåtgärd för anpassningsbara formulär
description: Med AEM Forms kan du skapa anpassade Skicka-åtgärder för adaptiva formulär. I den här artikeln beskrivs hur du lägger till anpassad skickaåtgärd för adaptiva formulär.
seo-description: Med AEM Forms kan du skapa anpassade Skicka-åtgärder för adaptiva formulär. I den här artikeln beskrivs hur du lägger till anpassad skickaåtgärd för adaptiva formulär.
uuid: fd8e1dac-b997-4e86-aaf6-3507edcb3070
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
discoiquuid: 2a2e1156-4a54-4b0a-981c-d527fe22a27e
docset: aem65
translation-type: tm+mt
source-git-commit: dfa983db4446cbb0cbdeb42297248aba55b3dffd

---


# Skriva anpassad skickaåtgärd för anpassningsbara formulär{#writing-custom-submit-action-for-adaptive-forms}

För adaptiva formulär krävs Skicka-åtgärder för att bearbeta användarspecificerade data. En Skicka-åtgärd avgör vilken uppgift som utförs på de data som du skickar med ett anpassat formulär. Adobe Experience Manager (AEM) innehåller [OOTB-överföringsåtgärder](../../forms/using/configuring-submit-actions.md) som demonstrerar anpassade uppgifter som du kan utföra med hjälp av data som skickas av användaren. Du kan till exempel utföra uppgifter som att skicka e-post eller lagra data.

## Arbetsflöde för en Skicka-åtgärd {#workflow-for-a-submit-action}

Flödesdiagrammet visar arbetsflödet för en Skicka-åtgärd som aktiveras när du klickar på knappen **[!UICONTROL Skicka]** i ett anpassat formulär. Filerna i komponenten Bifogad fil överförs till servern och formulärdata uppdateras med URL:erna för de överförda filerna. I klienten lagras data i JSON-format. Klienten skickar en Ajax-begäran till en intern server som masserar de data du har angett och returnerar dem i XML-format. Klienten samlar in dessa data med åtgärdsfält. Den skickar data till den sista servern (Guide Submit servlet) via en åtgärd för att skicka formulär. Sedan vidarebefordrar servern kontrollen till åtgärden Skicka. Åtgärden Skicka kan vidarebefordra begäran till en annan försäljningsresurs eller dirigera om webbläsaren till en annan URL.

![Flödesschema som visar arbetsflödet för åtgärden Skicka](assets/diagram1.png)

### XML-dataformat {#xml-data-format}

XML-data skickas till servern med hjälp av parametern request **`jcr:data`** . Skicka-åtgärder kan komma åt parametern för att bearbeta data. I följande kod beskrivs formatet för XML-data. De fält som är bundna till formulärmodellen visas i **`afBoundData`** avsnittet. Obundna fält visas i `afUnoundData`avsnittet. Mer information om `data.xml` filens format finns i [Introduktion till förifyllning av adaptiva formulärfält](../../forms/using/prepopulate-adaptive-form-fields.md).

```xml
<?xml ?>
<afData>
<afUnboundData>
<data>
<field1>value</field2>
<repeatablePanel>
    <field2>value</field2>
</repeatablePanel>
<repeatablePanel>
    <field2>value</field2>
</repeatablePanel>
</data>
</afUnboundData>
<afBoundData>
<!-- xml corresponding to the Form Model /XML Schema -->
</afBoundData>
</afData>
```

### Åtgärdsfält {#action-fields}

En Skicka-åtgärd kan lägga till dolda indatafält (med HTML- [indatataggen](https://developer.mozilla.org/en/docs/Web/HTML/Element/Input) ) i det återgivna HTML-formuläret. Dessa dolda fält kan innehålla värden som behövs när formulärinlämningen behandlas. När formuläret skickas bokförs dessa fältvärden som begärandeparametrar som åtgärden Skicka kan använda vid överföringshantering. Indatafälten kallas åtgärdsfält.

En Skicka-åtgärd som även fångar upp den tid det tar att fylla i ett formulär kan t.ex. lägga till dolda inmatningsfält `startTime` och `endTime`.

Ett skript kan innehålla värdena för `startTime` - och `endTime` -fälten när formuläret återges och före formuläröverföringen. Skriptet för åtgärden Skicka `post.jsp` kan sedan komma åt dessa fält med hjälp av frågeparametrar och beräkna den totala tid som krävs för att fylla i formuläret.

### Bifogade filer {#file-attachments}

Skicka-åtgärder kan även använda de bifogade filer som du överför med komponenten Bifogad fil. Skicka funktionsmakroskript kan komma åt dessa filer med [API:t](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/request/RequestParameter.html)för sling RequestParameter. Metoden [isFormField](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/request/RequestParameter.html#isFormField()) i API:t hjälper till att identifiera om parametern request är en fil eller ett formulärfält. Du kan iterera över parametrarna för begäran i en Skicka-åtgärd för att identifiera parametrar för bifogade filer.

Följande exempelkod identifierar de bifogade filerna i begäran. Därefter läses data in i filen med [Get API](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/request/RequestParameter.html#get()). Slutligen skapas ett Document-objekt med hjälp av data och läggs till i en lista.

```java
RequestParameterMap requestParameterMap = slingRequest.getRequestParameterMap();
for (Map.Entry<String, RequestParameter[]> param : requestParameterMap.entrySet()) {
    RequestParameter rpm = param.getValue()[0];
    if(!rpm.isFormField()) {
        fileAttachments.add(new Document(rpm.get()));
    }
}
```

### Vidarebefordra sökväg och omdirigerings-URL {#forward-path-and-redirect-url}

När du har utfört den nödvändiga åtgärden vidarebefordrar servern Skicka begäran till den framåtriktade sökvägen. En åtgärd använder API:t setForwardPath för att ställa in framåtsökvägen på tjänsten Skicka stödlinje.

Om åtgärden inte har någon framåtriktad sökväg dirigeras webbläsaren om med hjälp av omdirigerings-URL:en. Författaren konfigurerar omdirigerings-URL:en med hjälp av Tack-sidan i dialogrutan Redigera anpassat formulär. Du kan också konfigurera omdirigerings-URL:en via åtgärden Submit eller API:t setRedirectUrl i webbplansguiden. Du kan också konfigurera de Request-parametrar som skickas till Redirect URL med API:t setRedirectParameters i guiden Submit.

>[!NOTE]
>
>En författare tillhandahåller en omdirigerings-URL (med hjälp av Tack-sidkonfigurationen). [OOTB-överföringsåtgärder](../../forms/using/configuring-submit-actions.md) använder omdirigerings-URL:en för att dirigera om webbläsaren från resursen som sökvägen refererar till.
>
>Du kan skriva en anpassad Skicka-åtgärd som vidarebefordrar en begäran till en resurs eller server. Adobe rekommenderar att det skript som utför resurshantering för vidarebefordringssökvägen omdirigerar begäran till omdirigerings-URL:en när bearbetningen är klar.

## Skicka åtgärd {#submit-action}

En Skicka-åtgärd är en sling:Mapp som innehåller följande:

* **addfields.jsp**: Skriptet innehåller de åtgärdsfält som läggs till i HTML-filen under återgivningen. Använd det här skriptet för att lägga till dolda indataparametrar som krävs vid överföring i skriptet post.POST.jsp.
* **dialog.xml**: Det här skriptet liknar dialogrutan CQ Component. Det innehåller konfigurationsinformation som författaren anpassar. Fälten visas på fliken Skicka åtgärder i dialogrutan Redigera anpassat formulär när du väljer åtgärden Skicka.
* **post.POST.jsp**: Submit-servern anropar det här skriptet med data som du skickar och ytterligare data i föregående avsnitt. Om du kör en åtgärd på den här sidan måste du köra skriptet post.POST.jsp. Om du vill registrera åtgärden Submit med de adaptiva formulär som ska visas i dialogrutan Redigera anpassat formulär lägger du till dessa egenskaper i sling:Folder:

   * **guideComponentType** av typen String och value **fd/af/components/guideSubmitType**
   * **guideDataModel** av typen String som anger vilken typ av adaptivt formulär som åtgärden Submit gäller för. **xfa** stöds för XFA-baserade adaptiva formulär medan **xsd** stöds för XSD-baserade adaptiva formulär. **basic** stöds för adaptiva formulär som inte använder XDP eller XSD. Om du vill visa åtgärden på flera typer av adaptiva formulär lägger du till motsvarande strängar. Avgränsa varje sträng med kommatecken. Om du till exempel vill göra en åtgärd synlig i XFA- och XSD-baserade adaptiva formulär anger du värdena **xfa** respektive **xsd** .

   * **jcr:description** av typen String. Värdet för den här egenskapen visas i listan med överföringsåtgärder på fliken Skicka-åtgärder i dialogrutan Redigera anpassat formulär. OTB-åtgärderna finns i CRX-databasen på platsen **/libs/fd/af/components/guideSubmit**.

## Skapa en anpassad skickaåtgärd {#creating-a-custom-submit-action}

Utför följande steg för att skapa en anpassad Skicka-åtgärd som sparar data i CRX-databasen och sedan skickar ett e-postmeddelande till dig. Det adaptiva formuläret innehåller innehållet i OTB-sändningsåtgärden i Store (föråldrat) som sparar data i CRX-databasen. Dessutom innehåller CQ ett [e-post](https://docs.adobe.com/docs/en/cq/current/javadoc/com/day/cq/mailer/package-summary.html) -API som kan användas för att skicka e-post. Innan du använder e-post-API:t [konfigurerar]du tjänsten Day CQ Mail via systemkonsolen (https://docs.adobe.com/docs/en/cq/current/administering/notification.html?wcmmode=disabled#Configuring). Du kan återanvända åtgärden Lagra innehåll (föråldrat) för att lagra data i databasen. Åtgärden Lagra innehåll (borttaget) finns på platsen /libs/fd/af/components/guideSubittype/store i CRX-databasen.

1. Logga in på CRXDE Lite på URL:en https://&lt;server>:&lt;port>/crx/de/index.jsp. Skapa en nod med egenskapen sling:Folder och name store_and_mail i mappen /apps/custom_submit_action. Skapa mappen custom_submit_action om den inte redan finns.

   ![Skärmbild som visar hur en nod skapas med egenskapen sling:Folder](assets/step1.png)

1. **Ange de obligatoriska konfigurationsfälten.**

   Lägg till den konfiguration som krävs för Store-åtgärden. Kopiera **cq:dialog** -noden för Store-åtgärden från /libs/fd/af/components/guideSubittype/store till åtgärdsmappen på /apps/custom_submit_action/store_and_email.

   ![Skärmbild som visar kopiering av dialognoden till åtgärdsmappen](assets/step2.png)

1. **Ange konfigurationsfält som uppmanar författaren att ange e-postkonfigurationen.**

   Det adaptiva formuläret innehåller även en e-poståtgärd som skickar e-post till användarna. Anpassa den här åtgärden baserat på dina behov. Gå till /libs/fd/af/components/guideSubmitType/email/dialog. Kopiera noderna i cq:dialog-noden till cq:dialog-noden i din Submit-åtgärd (/apps/custom_submit_action/store_and_email/dialog).

   ![Anpassa e-poståtgärden](assets/step3.png)

1. **Gör åtgärden tillgänglig i dialogrutan Redigera anpassat formulär.**

   Lägg till följande egenskaper i noden store_and_email:

   * **guideComponentType** av typen **String** och value **fd/af/components/guideSubmitType**

   * **guideDataModel** av typen **String** och value **xfa, xsd, basic**

   * **jcr:beskrivning** av typen **String** och value **Store och Email Action**

1. Öppna ett anpassat formulär. Klicka på knappen **Redigera** bredvid **Start** för att öppna dialogrutan **Redigera** för den adaptiva formulärbehållaren. Den nya åtgärden visas på fliken **Skicka åtgärder** . Om du väljer **Store och Email Action** (E-poståtgärd) visas konfigurationen som lagts till i noden dialog.

   ![Dialogrutan Skicka åtgärdskonfiguration](assets/store_and_email_submit_action_dialog.jpg)

1. **Använd åtgärden för att slutföra en uppgift.**

   Lägg till skriptet post.POST.jsp i åtgärden. (/apps/custom_submit_action/store_and_mail/).

   Kör åtgärden OTB Store (skriptet post.POST.jsp). Använd API:t [FormsHelper.runAction](https://docs.adobe.com/docs/en/cq/current/javadoc/com/day/cq/wcm/foundation/forms/FormsHelper.html#runAction(java.lang.String, java.lang.String, org.apache.sling.api.resource, org.apache.sling.api.SlingHttpServletRequest, org.apache.sling.api.SlingHttpServletResponse) som innehåller CQ i koden för att köra Store-åtgärden. Lägg till följande kod i JSP-filen:

   `FormsHelper.runAction("/libs/fd/af/components/guidesubmittype/store", "post", resource, slingRequest, slingResponse);`

   För att skicka e-postmeddelandet läser koden mottagarens e-postadress från konfigurationen. Om du vill hämta konfigurationsvärdet i åtgärdens skript läser du egenskaperna för den aktuella resursen med följande kod. På samma sätt kan du läsa andra konfigurationsfiler.

   `ValueMap properties = ResourceUtil.getValueMap(resource);`

   `String mailTo = properties.get("mailTo");`

   Använd slutligen CQ Mail API för att skicka e-postmeddelandet. Använd [klassen SimpleEmail](https://commons.apache.org/proper/commons-email/apidocs/org/apache/commons/mail/SimpleEmail.html) för att skapa e-postobjektet enligt nedan:

   >[!NOTE]
   >
   >Kontrollera att JSP-filen har namnet post.POST.jsp.

   ```java
   <%@include file="/libs/fd/af/components/guidesglobal.jsp" %>
   <%@page import="com.day.cq.wcm.foundation.forms.FormsHelper,
          org.apache.sling.api.resource.ResourceUtil,
          org.apache.sling.api.resource.ValueMap,
                   com.day.cq.mailer.MessageGatewayService,
     com.day.cq.mailer.MessageGateway,
     org.apache.commons.mail.Email,
                   org.apache.commons.mail.SimpleEmail" %>
   <%@taglib prefix="sling"
                   uri="https://sling.apache.org/taglibs/sling/1.0" %>
   <%@taglib prefix="cq"
                   uri="https://www.day.com/taglibs/cq/1.0"
   %>
   <cq:defineObjects/>
   <sling:defineObjects/>
   <%
           String storeContent =
                       "/libs/fd/af/components/guidesubmittype/store";
           FormsHelper.runAction(storeContent, "post", resource,
                                   slingRequest, slingResponse);
    ValueMap props = ResourceUtil.getValueMap(resource);
    Email email = new SimpleEmail();
    String[] mailTo = props.get("mailto", new String[0]);
    email.setFrom((String)props.get("from"));
           for (String toAddr : mailTo) {
               email.addTo(toAddr);
      }
    email.setMsg((String)props.get("template"));
    email.setSubject((String)props.get("subject"));
    MessageGatewayService messageGatewayService =
                       sling.getService(MessageGatewayService.class);
    MessageGateway messageGateway =
                   messageGatewayService.getGateway(SimpleEmail.class);
    messageGateway.send(email);
   %>
   ```

   Markera åtgärden i det adaptiva formuläret. Åtgärden skickar ett e-postmeddelande och lagrar data.

