---
title: Skapa anpassade formulärmappningar
description: När du skapar en anpassad tabell i Adobe Campaign kanske du vill skapa ett formulär i AEM som mappar till den anpassade tabellen
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
exl-id: bce6c586-9962-4217-82cb-c837e479abc0
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '534'
ht-degree: 2%

---

# Skapa anpassade formulärmappningar{#creating-custom-form-mappings}

När du skapar en anpassad tabell i Adobe Campaign kanske du vill skapa ett formulär i AEM som mappar till den anpassade tabellen.

I det här dokumentet beskrivs hur du skapar anpassade formulärmappningar. När du har slutfört stegen i det här dokumentet kommer du att förse dina användare med en eventsida där de kan registrera sig för ett kommande evenemang. Därefter följer du upp med dessa användare via Adobe Campaign.

## Förutsättningar {#prerequisites}

Du måste ha följande installerat:

* Adobe Experience Manager
* Adobe Campaign Classic

Se [Integrera AEM med Adobe Campaign Classic](/help/sites-administering/campaignonpremise.md) för mer information.

## Skapa anpassade formulärmappningar {#creating-custom-form-mappings-2}

Om du vill skapa anpassade formulärmappningar måste du följa de här stegen på hög nivå, som beskrivs i detalj i följande avsnitt:

1. Skapa en anpassad tabell.
1. Utöka **frö** tabell.
1. Skapa en anpassad mappning.
1. Skapa en leverans baserat på den anpassade mappningen.
1. Bygg formuläret i AEM, som ska använda den skapade leveransen.
1. Skicka formuläret för att testa det.

### Skapa en anpassad tabell i Adobe Campaign {#creating-the-custom-table-in-adobe-campaign}

Börja med att skapa en anpassad tabell i Adobe Campaign. I det här exemplet använder vi följande definition för att skapa en händelsetabell:

```xml
<element autopk="true" label="Event" labelSingular="Event" name="event">
 <attribute label="Event Date" name="eventdate" type="date"/>
 <attribute label="Event Name" name="eventname" type="string"/>
 <attribute label="Email" name="email" type="string"/>
 <attribute label="Number of Seats" name="seats" type="long"/>
</element>
```

När du har skapat händelsetabellen kör du **Guiden Uppdatera databasstruktur** för att skapa tabellen.

### Utöka dirigerad tabell {#extending-the-seed-table}

I Adobe Campaign: **Lägg till** för att skapa ett tillägg till **Fröadresser (nms)** tabell.

![chlimage_1-194](assets/chlimage_1-194.png)

Använd fälten från **event** tabell som utökar **frö** tabell:

```xml
<element label="Event" name="custom_cus_event">
 <attribute name="eventname" template="cus:event:event/@eventname"/>
 <attribute name="eventdate" template="cus:event:event/@eventdate"/>
 <attribute name="email" template="cus:event:event/@email"/>
 <attribute name="seats" template="cus:event:event/@seats"/>
 </element>
```

Efter detta körs **Guiden Uppdatera databas** för att tillämpa ändringarna.

### Skapa anpassad målmappning {#creating-custom-target-mapping}

I **Administration/kampanjhantering** t, gå till **Målmappningar** och lägga till ett nytt T **Målmappning.**

>[!NOTE]
>
>Se till att du använder ett beskrivande namn för **Internt namn**.

![chlimage_1-195](assets/chlimage_1-195.png)

### Skapa en anpassad leveransmall {#creating-a-custom-delivery-template}

I det här steget lägger du till en leveransmall som använder den skapade **Målmappning**.

I **Resurser/mallar** navigerar du till leveransmallen och duplicerar den befintliga AEM. När du klickar **Till**, välj händelsen create **Målmappning**.

![chlimage_1-196](assets/chlimage_1-196.png)

### Skapa formuläret i AEM {#building-the-form-in-aem}

I AEM kontrollerar du att du har konfigurerat en Cloud Service i **Sidegenskaper**.

Sedan i **Adobe Campaign** väljer du leveransen som skapades i [Skapa en anpassad leveransmall](#creating-a-custom-delivery-template).

![chlimage_1-197](assets/chlimage_1-197.png)

När du konfigurerar fälten måste du ange unika elementnamn för formulärfälten.

När fälten har konfigurerats måste du ändra mappningen manuellt.

I CRXDE-lite, gå till **jcr:innehåll** (på sidan) och ändra **acMapping** värdet till det interna namnet på **Målmappning**.

![chlimage_1-198](assets/chlimage_1-198.png)

Kontrollera att du har markerat kryssrutan för att skapa om formuläret inte finns

![chlimage_1-199](assets/chlimage_1-199.png)

### Skicka formuläret {#submitting-the-form}

Nu kan du skicka formuläret och validera om värdena sparas på Adobe Campaign-sidan.

![chlimage_1-200](assets/chlimage_1-200.png)

## Felsökning {#troubleshooting}

**&quot;Ogiltig typ för värdet &#39;02/02/2015&#39; från elementet &#39;@eventdate&#39; (dokument av typen &#39;Event ([adb:event])&#39;)&quot;**

När formuläret skickas loggas det här felet i **error.log** AEM.

Detta beror på ett ogiltigt format för datumfältet. Lösningen är att tillhandahålla **yyyy-mm-dd** som värdet.
