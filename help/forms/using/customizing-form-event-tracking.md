---
title: Anpassa spårning av formulärhändelser
description: Om en användare spenderar mer än 60 sekunder på ett fält utlöses en fältbesökshändelse och informationen om fältet skickas till Adobe SiteCatalyst.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
exl-id: d0280a15-5d0d-49cf-bce9-ad1c40530eae
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '449'
ht-degree: 0%

---

# Anpassa spårning av formulärhändelser {#customizing-form-event-tracking}

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
   <td>spara</td>
   <td>formName, formTitle, formInstance, panelName, source</td>
  </tr>
  <tr>
   <td>skicka</td>
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

Om en användare tillbringar mer än 60 sekunder på ett fält AEM standardinställningen är `fieldvisit` -händelsen aktiveras och informationen om fältet skickas till Adobe Analytics. Du kan anpassa baslinjen för spårning av fälttid under Konfiguration av AEM Forms Analytics på AEM Configuration Console (/system/console/configMgr) för att öka eller minska tidsgränsen.

## Anpassa spårningshändelser {#customizing-the-tracking-events}

Du kan ändra `trackEvent`funktion finns i `/libs/afanalytics/js/custom.js` fil för att anpassa händelsespårningen. När en händelse som spåras inträffar i en adaptiv form är `trackEvent`funktionen anropas. The `trackEvent` funktionen accepterar två parametrar: `eventName`och `variableValueMap`.

Du kan utvärdera värdet för *eventName* och *variableValueMap* argument för att ändra spårningsbeteendet för händelser. Du kan till exempel välja att skicka informationen till analysservern efter att ett visst antal felhändelser har inträffat. Du kan även välja att utföra någon av följande anpassningar:

* Du kan ange en tröskeltid innan du skickar händelsen.
* Du kan behålla ett läge för att bestämma åtgärd, till exempel *fieldVisit* överför en dummy-händelse baserat på tidsstämpeln för den senaste händelsen.
* Du kan använda `pushEvent` funktion som skickar händelsen till analysservern *.*

* Du kan välja att inte skicka händelsen till analysservern alls.

### Exempel {#sample}

I följande exempel är läget för *fel* händelse för varje *fieldName* -attributet bevaras. Händelsen skickas bara till analysservern om ett fel inträffar igen.

```javascript
case 'error':
        if(errorOccurred[variableValueMap.fieldName] == true) {
            pushEvent(eventName, variableValueMap)
        }
        errorOccurred[variableValueMap.fieldName] = true;
        break;
```

## Anpassa panelbesökshändelsen {#customizing-the-panelvisit-event}

I standardinställningen för AEM Forms kontrolleras det efter var 60:e sekund om fönstret som innehåller det adaptiva formuläret är aktivt. Om fönstret är aktivt visas en `panelVisit`-händelsen utlöses för Adobe Analytics. Det hjälper till att kontrollera att dokumentet eller formuläret är aktivt och beräknar hur lång tid som har ägnats åt motsvarande formulär eller dokument.

>[!NOTE]
>
>Händelsenamnet som används för att bevara aktivitet och beräkna hur lång tid som har ägnats åt är &quot;panelVisit&quot;. Den här händelsen skiljer sig från panelbesökshändelsen som listas i tabellen ovan.

Du kan ändra funktionen scheduleHeartBeatCheck som finns i `/libs/afanalytics/js/custom.js` om du vill ändra eller stoppa den här händelsen som skickas till Adobe Analytics med ett regelbundet intervall.
