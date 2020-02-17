---
title: Skapa anpassade formulärmappningar
seo-title: Skapa anpassade formulärmappningar
description: När du skapar en anpassad tabell i Adobe Campaign kanske du vill skapa ett formulär i AEM som mappar till den anpassade tabellen
seo-description: När du skapar en anpassad tabell i Adobe Campaign kanske du vill skapa ett formulär i AEM som mappar till den anpassade tabellen
uuid: f3bde513-6edb-4eb6-9048-40045ee08c4a
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: d5dac1db-2dde-4b75-a31b-e057b447f6e2
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Skapa anpassade formulärmappningar{#creating-custom-form-mappings}

När du skapar en anpassad tabell i Adobe Campaign kanske du vill skapa ett formulär i AEM som mappar till den anpassade tabellen.

I det här dokumentet beskrivs hur du skapar anpassade formulärmappningar. När du har slutfört stegen i det här dokumentet kommer du att förse dina användare med en eventsida där de kan registrera sig för ett kommande evenemang. Därefter följer ni upp med dessa användare via Adobe Campaign.

## Förutsättningar {#prerequisites}

Du måste ha följande installerat:

* Adobe Experience Manager
* Adobe Campaign Classic

Mer information finns i [Integrera AEM med Adobe Campaign Classic](/help/sites-administering/campaignonpremise.md) .

## Skapa anpassade formulärmappningar {#creating-custom-form-mappings-2}

Om du vill skapa anpassade formulärmappningar måste du följa dessa steg på hög nivå, som beskrivs i detalj i följande avsnitt:

1. Skapa en anpassad tabell.
1. Utöka **startvärdestabellen** .
1. Skapa en anpassad mappning.
1. Skapa en leverans baserat på den anpassade mappningen.
1. Bygg formuläret i AEM, som kommer att använda den skapade leveransen.
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

När du har skapat händelsetabellen kör du guiden **** Uppdatera databasstruktur för att skapa tabellen.

### Utöka dirigeringstabellen {#extending-the-seed-table}

I Adobe Campaign trycker/klickar du på **Lägg** till för att skapa ett nytt tillägg för tabellen **dirigeringsadresser (nms)** .

![chlimage_1-194](assets/chlimage_1-194.png)

Använd nu fälten från **händelsetabellen** för att utöka **startvärdestabellen** :

```xml
<element label="Event" name="custom_cus_event">
 <attribute name="eventname" template="cus:event:event/@eventname"/>
 <attribute name="eventdate" template="cus:event:event/@eventdate"/>
 <attribute name="email" template="cus:event:event/@email"/>
 <attribute name="seats" template="cus:event:event/@seats"/>
 </element>
```

Kör sedan guiden **** Uppdatera databas för att tillämpa ändringarna.

### Skapa anpassad målmappning {#creating-custom-target-mapping}

Gå till **Målmappningar** i **Administration/** Kampanjhantering och lägg till en ny **målmappning.**

>[!NOTE]
>
>Se till att du använder ett beskrivande namn som **internt namn**.

![chlimage_1-195](assets/chlimage_1-195.png)

### Skapa en anpassad leveransmall {#creating-a-custom-delivery-template}

I det här steget lägger du till en leveransmall som använder den skapade **målmappningen**.

I **Resurser/mallar** navigerar du till leveransmallen och duplicerar den befintliga AEM-leveransen. När du klickar på **Till** väljer du **Skapa händelsemålsmappning**.

![chlimage_1-196](assets/chlimage_1-196.png)

### Bygga formuläret i AEM {#building-the-form-in-aem}

Kontrollera att du har konfigurerat en molntjänst i **Sidegenskaper** i AEM.

På fliken **Adobe Campaign** väljer du sedan den leverans som skapades när du [skapade en anpassad leveransmall](#creating-a-custom-delivery-template).

![chlimage_1-197](assets/chlimage_1-197.png)

När du konfigurerar fälten måste du ange unika elementnamn för formulärfälten.

När fälten har konfigurerats måste du ändra mappningen manuellt.

I CRXDE-lite går du till noden **jcr:content** (på sidan) och ändrar **acMapping** -värdet till det interna namnet för **målmappningen**.

![chlimage_1-198](assets/chlimage_1-198.png)

Kontrollera att du har markerat kryssrutan för att skapa om formuläret inte finns

![chlimage_1-199](assets/chlimage_1-199.png)

### Skicka formuläret {#submitting-the-form}

Nu kan du skicka formuläret och validera om värdena sparas på Adobe Campaign-sidan.

![chlimage_1-200](assets/chlimage_1-200.png)

## Felsökning {#troubleshooting}

**&quot;Ogiltig typ för värdet &#39;02/02/2015&#39; från elementet &#39;@eventdate&#39; (dokument av typen &#39;Event ([adb:event])&#39;)&quot;**

När formuläret skickas loggas det här felet i **error.log** i AEM.

Detta beror på ett ogiltigt format för datumfältet. Du kan lösa problemet genom att ange värdet **åååå-mm-dd** .

