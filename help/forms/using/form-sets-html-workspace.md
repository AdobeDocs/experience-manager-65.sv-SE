---
title: Arbeta med formulär i AEM Forms arbetsyta
seo-title: Working with Formsets in AEM Forms workspace
description: En formuläruppsättning är en samling HTML5-formulär som grupperas och presenteras som en enda formuläruppsättning för slutanvändarna. Lär dig hur du kan arbeta med formatuppsättningar i AEM Forms arbetsyta.
seo-description: A formset is a collection of HTML5 forms grouped and presented as a single set of forms to end users. Learn how you can work with formsets in AEM Forms workspace.
uuid: 1a5f3ce8-1d6a-497e-90d0-49765e40cf3b
contentOwner: vishgupt
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: f550b747-2def-4317-9ef7-dc6c1e7bb404
docset: aem65
exl-id: 76a8f93f-eb8a-4e68-8626-efa6dc67668f
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '346'
ht-degree: 0%

---

# Arbeta med formulär i AEM Forms arbetsyta{#working-with-formsets-in-aem-forms-workspace}

En formuläruppsättning är en samling HTML5-formulär som grupperas och presenteras som en enda formuläruppsättning för slutanvändarna. När slutanvändarna börjar fylla i en formuläruppsättning, överförs de smidigt från ett formulär till ett annat. Formuläruppsättningen kan sedan skickas med bara ett klick. Mer information om formuläruppsättningar och hur du konfigurerar dem finns i [Formuppsättning i AEM Forms](../../forms/using/formset-in-aem-forms.md).

AEM Forms arbetsyta stöder formatuppsättningar. Med formuläruppsättningar kan flera formulär som är kopplade till en tjänst eller process grupperas för att automatisera en affärsprocess och presenteras för slutanvändarna. I ett sådant scenario kan användarna fylla i hela uppsättningen som ett och det finns inget behov av att arkivera, skicka och spåra enskilda formulär eller processer.

## Koppla en formuläruppsättning till startpunkten i en AEM Forms-arbetsyteapp {#attaching-a-formset-to-startpoint-in-an-aem-forms-workspace-app-br}

1. Skapa affärsprocessarbetsflödet i Workbench. Mer information finns i [Workbench - hjälp](https://www.adobe.com/go/learn_aemforms_workbench_63).
1. Välj bland processegenskaperna för startpunkten **Använd en CRX-resurs** i presentationer och data.

   ![1-3](assets/1-3.png)

1. Klicka ![bläddra](assets/browse.png) (Bläddra) bredvid resurssökvägen för CRX. Dialogrutan Välj formulärresurs visas.

   ![2-1](assets/2-1.png)

1. Klicka på **Format** väljer du den relevanta formuppsättningen i listan och klickar sedan på **OK**.

1. Distribuera programmet efter uppdatering av andra relevanta processegenskaper.

## Använda formatuppsättningar i AEM Forms arbetsyta {#using-formset-in-nbsp-aem-forms-workspace}

När en formuläruppsättning är kopplad till en startpunkt kan startpunkten anropas från arbetsytan i AEM Forms, precis som vilken startpunkt som helst.

De åtgärder som stöds för formatuppsättningar via arbetsytan i AEM Forms är:

* Spara som utkast
* Lås
* Abandon
* Skicka
* Lägg till bifogade filer
* Lägg till anteckningar
* Flytta mellan formulär i en formuläruppsättning med knapparna Bakåt eller Nästa

![3-1](assets/3-1.png)

>[!NOTE]
>
>Om du vill förbättra prestandan när du flyttar från föregående och nästa formulär i en formuläruppsättning, ska du använda alla arbetsyteknappar (Bakåt, Nästa, Spara, Skicka och ... (Mer) inaktiveras tills det aktuella formuläret återges fullständigt.
