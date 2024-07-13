---
title: Skapa en anpassad AEM med Adobe Campaign Form Components
description: Skapa en anpassad sidmall som använder Adobe Campaign Form-komponenter
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
exl-id: de5c634a-c0d7-4e69-b941-d2fbfe83117d
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: ad8f849384e58511de97611d1b26c4fc96022062
workflow-type: tm+mt
source-wordcount: '313'
ht-degree: 2%

---

# Skapa en anpassad AEM med Adobe Campaign Form Components{#creating-custom-aem-page-template-with-adobe-campaign-form-components}

På den här sidan beskrivs hur du skapar en anpassad sidmall som använder [Adobe Campaign Form](/help/sites-authoring/adobe-campaign-components.md) -komponenter genom att undersöka hur mallen för utomhusaktiviteter (`/apps/geometrixx-outdoors/components/page_campaign_profile`) implementeras, och den pekar dig på viktig information som du kan behöva när du skapar en egen anpassad mall.

>[!NOTE]
>
>[E-post och formulärexempel är bara tillgängliga i Geometrixx](/help/sites-developing/we-retail.md). Hämta exempelinnehåll för Geometrixx från paketresurs.

>[!CAUTION]
>
>AEM e-postkomponenter har tagits bort. På grund av e-postens natur, som sammanfogar innehåll och format, blir de e-postkomponenter som AEM tillhandahåller direkt i kartong av begränsad återanvändning för kunderna på grund av behovet av att implementera anpassade format i de komponenter som behövs för projekt.
>
>E-postkomponenter kan implementeras på projektnivå och de borttagna AEM e-postkomponenterna visar hur man kan uppnå detta. Använd dock inte de här inaktuella komponenterna i projekt.


Om du vill skapa en anpassad AEM sidmall med hjälp av Adobe Campaign Form-komponenter måste du ha följande:

1. **Korrigera resourceSuperType**

   Kontrollera att sidkomponenten ärver från `mcm/campaign/components/profile`.

   Detta krävs för att servletarna ska kunna hämta och spara information

   * `com.day.cq.mcm.campaign.servlets.TemplateListServlet`
   * `com.day.cq.mcm.campaign.servlets.SaveProfileServlet`

   ![chlimage_1-201](assets/chlimage_1-201.png)

1. **Inställningar för ClientContext**

   När du tittar på klientkontextinställningarna ( `/etc/designs/geometrixx-outdoors/jcr:content/page_campaign_profile`) ser du följande inställningar:

   * ClientContexten pekar på `/etc/clientcontext/campaign`
   * Det finns även en extra *config*-nod.

   ![chlimage_1-202](assets/chlimage_1-202.png)

1. **head.jsp (/apps/geometrixx-outdoors/components/page_campaign_profile/head.jsp)**

   I **head.jsp** ser du följande rader som använder **clientcontext-config** och **cloudservice-kroken**:

   ```
   <cq:include path="config" resourceType="cq/personalization/components/clientcontext_optimized/config"/>
   <sling:include path="contexthub" resourceType="granite/contexthub/components/contexthub"/>
   <cq:include script="/libs/cq/cloudserviceconfigs/components/servicelibs/servicelibs.jsp"/>
   ```

1. **body.jsp (/apps/geometrixx-outdoors/components/page_campaign_profile/body.jsp)**

   I **body.jsp** läses molntjänsterna in längst ned på sidan:

   ```
   <cq:include path="cloudservices" resourceType="cq/cloudserviceconfigs/components/servicecomponents"/>
   ```

1. **Egenskaper för kampanjsida**

   Om du vill kunna välja en Adobe Campaign-mall utökas sidegenskaperna med fliken **Campaign** :

   `/apps/geometrixx-outdoors/components/page_campaign_profile/dialog/items/tabs/items/campaign`

   ![chlimage_1-203](assets/chlimage_1-203.png)

1. **Mallinställningar**.

   I mallen ( `/apps/geometrixx-outdoors/templates/campaign_profile/jcr:content`) visas följande standardvärden:

   | **acMapping** | mapRecipient (för Adobe Campaign 6.1), profile (för Adobe Campaign Standard) |
   |---|---|
   | **acTemplateId** | mail |

   ![chlimage_1-204](assets/chlimage_1-204.png)
