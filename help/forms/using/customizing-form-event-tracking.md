---
title: Anpassa spårning av formulärhändelser
seo-title: Anpassa spårning av formulärhändelser
description: Om en användare spenderar mer än 60 sekunder på ett fält utlöses en fältbesökshändelse och informationen om fältet skickas till Adobe SiteCatalyst.
seo-description: Om en användare spenderar mer än 60 sekunder på ett fält utlöses en fältbesökshändelse och informationen om fältet skickas till Adobe SiteCatalyst.
uuid: 2f790085-2f1a-45be-9a69-6100c76dcae0
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
discoiquuid: 60d67c6b-5994-42ef-b159-ed6edf5cf9d4
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '476'
ht-degree: 1%

---


# Anpassa formulärhändelsespårning {#customizing-form-event-tracking}

Följande händelser spåras automatiskt i en analysaktiverad Adaptiv form:

<table>
 <tbody>
  <tr>
   <th>Händelse</th>
   <th>Tillgängliga variabler</th>
  </tr>
  <tr>
   <td>återge</td>
   <td>formName, formTitle, formInstance, källa</td>
  </tr>
  <tr>
   <td>överge</td>
   <td>formName, formTitle, formInstance, panelName, panelTitle</td>
  </tr>
  <tr>
   <td>save</td>
   <td>formName, formTitle, formInstance, panelName, source</td>
  </tr>
  <tr>
   <td>submit</td>
   <td>formName, formTitle, formInstance, källa</td>
  </tr>
  <tr>
   <td>fel</td>
   <td>formName, formTitle, fieldName, fieldTitle, panelTitle</td>
  </tr>
  <tr>
   <td>help</td>
   <td>formName, formTitle, fieldName, fieldTitle, panelTitle</td>
  </tr>
  <tr>
   <td>fieldVisit</td>
   <td>formName, formTitle, fieldName, fieldTitle, panelTitle<br /> </td>
  </tr>
  <tr>
   <td>panelBesök</td>
   <td>formName, formTitle, panelName, panelTitle</td>
  </tr>
 </tbody>
</table>

## Anpassa tidsgränsen för fältbesökshändelser {#customizing-the-field-visit-event-timeout}

Om en användare lägger mer än 60 sekunder på ett fält i standardinställningen AEM en `fieldvisit`-händelse utlöses och informationen om fältet skickas till Adobe Analytics. Du kan anpassa baslinjen för spårning av fälttid under Konfiguration av AEM Forms Analytics på AEM Configuration Console (/system/console/configMgr) för att öka eller minska tidsgränsen.

## Anpassa spårningshändelserna {#customizing-the-tracking-events}

Du kan ändra funktionen `trackEvent`som är tillgänglig i `/libs/afanalytics/js/custom.js`-filen för att anpassa händelsespårningen. När en händelse som spåras inträffar i en adaptiv form anropas funktionen `trackEvent`. Funktionen `trackEvent` accepterar två parametrar: `eventName`och `variableValueMap`.

Du kan utvärdera värdet för *eventName* och *variableValueMap*-argument om du vill ändra spårningsbeteendet för händelser. Du kan till exempel välja att skicka informationen till analysservern efter att ett visst antal felhändelser har inträffat. Du kan även välja att utföra någon av följande anpassningar:

* Du kan ange en tröskeltid innan du skickar händelsen.
* Du kan underhålla ett läge för att bestämma en åtgärd, till exempel *fieldVisit* push a dummy event based on the timestamp of the last event.
* Du kan använda funktionen `pushEvent` för att skicka händelsen till analysservern *.*

* Du kan välja att inte skicka händelsen till analysservern alls.

### Exempel {#sample}

I följande exempel behålls tillståndet för händelsen *error* för varje *fieldName*-attribut. Händelsen skickas bara till analysservern om ett fel inträffar igen.

```javascript
case 'error':
        if(errorOccurred[variableValueMap.fieldName] == true) {
            pushEvent(eventName, variableValueMap)
        }
        errorOccurred[variableValueMap.fieldName] = true;
        break;
```

## Anpassa panelbesökshändelsen {#customizing-the-panelvisit-event}

I standardinställningen för AEM Forms kontrolleras det efter var 60:e sekund om fönstret som innehåller det adaptiva formuläret är aktivt. Om fönstret är aktivt utlöses en `panelVisit`händelse till Adobe Analytics. Det hjälper till att kontrollera att dokumentet eller formuläret är aktivt och beräknar hur lång tid som har ägnats åt motsvarande formulär eller dokument.

>[!NOTE]
>
>Händelsenamnet som används för att bevara aktivitet och beräkna hur lång tid som har ägnats åt är &quot;panelVisit&quot;. Den här händelsen skiljer sig från panelbesökshändelsen som listas i tabellen ovan.

Du kan ändra funktionen scheduleHeartBeatCheck som finns i `/libs/afanalytics/js/custom.js`-filen om du vill ändra eller stoppa den här händelsen som skickas till Adobe Analytics med ett regelbundet intervall.
