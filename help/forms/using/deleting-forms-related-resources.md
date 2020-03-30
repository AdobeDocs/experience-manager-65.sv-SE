---
title: Ta bort formulär och relaterade resurser
seo-title: Ta bort formulär och relaterade resurser
description: Så här tar du bort ett formulär eller en resurs i AEM Forms och hur det påverkar refererade och refererade tillgångar och XFA-formulär.
seo-description: Så här tar du bort ett formulär eller en resurs i AEM Forms och hur det påverkar refererade och refererade tillgångar och XFA-formulär.
uuid: df522b87-59d8-4678-922d-c9aab82b1381
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-manager
discoiquuid: c8519eec-f841-4867-baa9-a9e03042755e
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f

---


# Ta bort formulär och relaterade resurser {#deleting-forms-and-related-resources}

Du kan ta bort formulären och resurserna för att ta bort dessa resurser från databasen. Borttagningsåtgärden fungerar för alla resurstyper och mappar.

Om du tar bort en resurs från författarinstansen tas även resursen bort från publiceringsinstansen. AEM Forms-servern består av författare och publiceringsinstanser. Instansen Författare används för att skapa och hantera formulärresurser och -resurser. Publiceringsinstansen innehåller publicerade formulärresurser och relaterade resurser som är tillgängliga för slutanvändare.

## Så här tar du bort ett formulär {#how-to-delete-a-form}

1. Logga in i användargränssnittet för AEM Forms via `https://[hostname]:'port'/aem/forms.html.`
1. Navigera till och markera det formulär som du vill ta bort. Klicka på Ta bort ![aem6forms_delete2](assets/aem6forms_delete2.png) i verktygsfältet och bekräfta borttagningsåtgärden.

   >[!NOTE]
   >
   >Det går endast att ta bort ett formulär åt gången. Ta bort flera formulär individuellt eller ta bort den överordnade mappen.

1. Innan du tar bort en resurs söker AEM Forms efter referenser och begär en explicit bekräftelse. Klicka på Tvinga borttagning om du vill ta bort resursen oavsett relationsstatus.

   >[!NOTE]
   >
   >Om du tar bort en resurs som refereras av andra resurser kan det orsaka funktionella problem.

   >[!NOTE]
   >
   >Om den markerade resursen är en mapp och den innehåller en sådan resurs i sin hierarki kan du ta bort andra resurser antingen separat eller ta bort hela mappen.

## Effekten av att ta bort ett refererat XFA-formulär {#impact-of-deleting-a-referenced-xfa-form}

I AEM Forms kan en XFA-formulärmall refereras av ett adaptivt formulär eller en annan XFA-formulärmall. En mall kan även referera till en resurs eller en annan XFA-mall.

Det är inte tillrådligt att ta bort ett XFA-formulär som refereras av ett adaptivt formulär, eftersom det kan skada det adaptiva formuläret. När ett adaptivt formulär refererar till ett XFA-formulär är fälten bundna. När XFA har tagits bort kan det adaptiva formuläret inte synkronisera sina fält med XFA-fälten och ett felmeddelande visas för sådana fält. Mer information om effekten av XFA-borttagning och om felaktiga AF:er finns i [Uppdatera refererade XFA-formulär](/help/forms/using/get-xdp-pdf-documents-aem.md#p-updating-referenced-xfa-forms-p).

Om du vill ta bort ett sådant XFA-formulär uppdaterar du det adaptiva formuläret och tar bort bindningarna med XFA-fälten.
