---
title: Konfigurera slutpunkter för Aktivitetshanteraren
seo-title: Configuring Task Manager endpoints
description: Lär dig hur du konfigurerar slutpunkter för Task Manager.
seo-description: Learn how to configure Task Manager endpoints.
uuid: 07604b10-0bd7-4bce-9624-7ebac4754f56
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_endpoints
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 9c55feb9-23d8-4798-a3c5-70ec736df3ad
exl-id: 8495a3d7-6ac9-41f5-b1f9-31decaba118a
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 0%

---

# Konfigurera slutpunkter för Aktivitetshanteraren {#configuring-task-manager-endpoints}

Med slutpunkterna i Task Manager kan Workspace-användare anropa tjänsten.

**Slutpunktsinställningar för Aktivitetshanteraren**

Använd följande inställningar för att konfigurera en Task Manager-slutpunkt.

**Namn:** (Obligatoriskt) Identifierar slutpunkten. Namnet visas i kortvyn i Workspace. Ta inte med ett &lt;-tecken eftersom det kortar av namnet som visas i arbetsytan. Om du anger en URL som namn på slutpunkten kontrollerar du att den överensstämmer med de syntaxregler som anges i RFC1738.

**Beskrivning:** En beskrivning av slutpunkten. Ta inte med ett &lt;-tecken eftersom det kortar av beskrivningen som visas i Arbetsyta.

**Uppgiftsanvisningar:** Instruktioner för den användare som startar det här arbetsflödet.

**Processägare:** Namnet på den person som är ansvarig för processen.

**Användaren kan vidarebefordra uppgiften:** Låter användaren vidarebefordra den inledande uppgiften.

**Visa fönster för bifogade filer:** Låter användaren se fönstret för bilagor.

**Tillåt tillägg av bifogad fil:** Tillåter användaren att lägga till bilagor och anteckningar.

**Aktiviteten är låst:** Låser den inledande uppgiften.

**Lägg till åtkomstkontrollistor för delade köer:** Den inledande uppgiften skapas med åtkomstkontrollistor för användare i delade köer.

**Kategorisering:** (Obligatoriskt) Den kategori där användaren ska se formuläret i Workspace. Välj en kategori i listan eller välj Ny kategori om du vill lägga till en kategori.

**Åtgärdsnamn:** (Obligatoriskt) En lista över åtgärder som kan tilldelas till slutpunkten.
