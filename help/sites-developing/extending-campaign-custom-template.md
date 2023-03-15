---
title: Skapa en anpassad AEM med Adobe Campaign Form Components
seo-title: Creating Custom AEM Page Template with Adobe Campaign Form Components
description: Skapa en anpassad sidmall som använder Adobe Campaign Form-komponenter
seo-description: Build a custom page template that uses Adobe Campaign Form components
uuid: 8162ace2-b661-4c39-b0fb-288e1c035b9c
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: c3f6eed4-bbda-454a-88ce-c7f2041d4217
exl-id: de5c634a-c0d7-4e69-b941-d2fbfe83117d
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '238'
ht-degree: 1%

---

# Skapa en anpassad AEM med Adobe Campaign Form Components{#creating-custom-aem-page-template-with-adobe-campaign-form-components}

På den här sidan beskrivs hur du skapar en anpassad sidmall som använder [Adobe Campaign Form](/help/sites-authoring/adobe-campaign-components.md) genom att undersöka hur mallen för Geometrixx utomhus ( `/apps/geometrixx-outdoors/components/page_campaign_profile`) är implementerat och pekar på viktig information som du kan behöva när du skapar en egen anpassad mall.

>[!NOTE]
>
>[E-post och formulärexempel är bara tillgängliga i Geometrixx](/help/sites-developing/we-retail.md). Hämta exempelinnehåll för Geometrixx från paketresurs.

Om du vill skapa en anpassad AEM sidmall med hjälp av Adobe Campaign Form-komponenter måste du ha följande:

1. **Korrigera resourceSuperType**

   Kontrollera att sidkomponenten ärver från `mcm/campaign/components/profile`.

   Detta krävs för att servletarna ska kunna hämta och spara information

   * `com.day.cq.mcm.campaign.servlets.TemplateListServlet`
   * `com.day.cq.mcm.campaign.servlets.SaveProfileServlet`

   ![chlimage_1-201](assets/chlimage_1-201.png)

1. **Inställningar för ClientContext**

   När du tittar på klientkontextinställningarna ( `/etc/designs/geometrixx-outdoors/jcr:content/page_campaign_profile`) visas följande inställningar:

   * ClientContext pekar på `/etc/clientcontext/campaign`
   * Det finns även en extra *config* nod.

   ![chlimage_1-202](assets/chlimage_1-202.png)

1. **head.jsp (/apps/geometrixx-outdoors/components/page_campaign_profile/head.jsp)**

   I **head.jsp** visas följande rader som använder **clientcontext-config** och **cloudservice-krok**:

   ```
   <cq:include path="config" resourceType="cq/personalization/components/clientcontext_optimized/config"/>
   <sling:include path="contexthub" resourceType="granite/contexthub/components/contexthub"/>
   <cq:include script="/libs/cq/cloudserviceconfigs/components/servicelibs/servicelibs.jsp"/>
   ```

1. **body.jsp (/apps/geometrixx-outdoors/components/page_campaign_profile/body.jsp)**

   I **body.jsp**, läses molntjänsterna in längst ned på sidan:

   ```
   <cq:include path="cloudservices" resourceType="cq/cloudserviceconfigs/components/servicecomponents"/>
   ```

1. **Egenskaper för kampanjsida**

   För att kunna välja en Adobe Campaign-mall utökas sidegenskaperna med **Campaign** tab:

   `/apps/geometrixx-outdoors/components/page_campaign_profile/dialog/items/tabs/items/campaign`

   ![chlimage_1-203](assets/chlimage_1-203.png)

1. **Mallinställningar**.

   I mallen ( `/apps/geometrixx-outdoors/templates/campaign_profile/jcr:content`) visas följande standardvärden:

   | **acMapping** | mapRecipient (för Adobe Campaign 6.1), profile (för Adobe Campaign Standard) |
   |---|---|
   | **acTemplateId** | mail |

   ![chlimage_1-204](assets/chlimage_1-204.png)
