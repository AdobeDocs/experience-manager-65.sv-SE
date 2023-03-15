---
title: Anpassa välkomstkonsolen (Classic UI)
seo-title: Customizing the Welcome Console (Classic UI)
description: Välkomstkonsolen innehåller en lista med länkar till de olika konsolerna och funktionerna i AEM
seo-description: The Welcome console provides a list of links to the various consoles and functionality within AEM
uuid: 4ef20cef-2d7a-417d-b36b-ed4fa56cd511
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: 2e408acb-3802-4837-8619-688cfc3abfa7
exl-id: 9e171b62-8efb-4143-a202-ba6555658d4b
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '464'
ht-degree: 4%

---

# Anpassa välkomstkonsolen (Classic UI){#customizing-the-welcome-console-classic-ui}

>[!CAUTION]
>
>Den här sidan behandlar det klassiska användargränssnittet.
>
>Se [Anpassa konsolerna](/help/sites-developing/customizing-consoles-touch.md) om du vill ha information om det pekaktiverade användargränssnittet.

Välkomstkonsolen innehåller en lista med länkar till de olika konsolerna och funktionerna i AEM.

![cq_welcomescreen](assets/cq_welcomescreen.png)

Det går att konfigurera synliga länkar. Detta kan definieras för specifika användare och/eller grupper. Vilka åtgärder som ska vidtas beror på måltypen (som motsvarar den del av konsolen som de finns i):

* [Huvudkonsoler](#links-in-main-console-left-pane) - Länkar i huvudkonsolen (vänster ruta)
* [Resurser, dokumentation och referenser, funktioner](#links-in-sidebar-right-pane) - Länkar i sidlisten (den högra rutan)

## Länkar i huvudkonsolen (vänster ruta) {#links-in-main-console-left-pane}

Här visas huvudkonsolerna för AEM.

![cq_welcomescreenmainconsole](assets/cq_welcomescreenmainconsole.png)

### Konfigurera om huvudkonsollänkar är synliga {#configuring-whether-main-console-links-are-visible}

Nodnivåbehörigheter avgör om länken kan ses eller inte. De aktuella noderna är:

* **Webbplatser:** `/libs/wcm/core/content/siteadmin`

* **Digital Assets:** `/libs/wcm/core/content/damadmin`

* **Community:** `/libs/collab/core/content/admin`

* **Kampanjer:** `/libs/mcm/content/admin`

* **Inkorg:** `/libs/cq/workflow/content/inbox`

* **Användare:** `/libs/cq/security/content/admin`

* **Systemutvärdering:** `/libs/wcm/core/content/misc`

* **Taggning:** `/libs/cq/tagging/content/tagadmin`

Till exempel:

* Begränsa åtkomsten till **verktyg**, ta bort läsåtkomst från

   `/libs/wcm/core/content/misc`

Se [Security section](/help/sites-administering/security.md) om du vill ha mer information om hur du anger behörigheter.

### Länkar i sidofältet (höger ruta) {#links-in-sidebar-right-pane}

![cq_welcomescreensidebar](assets/cq_welcomescreensidebar.png)

Länkarna bygger på att det finns *och* läsåtkomst till noder under följande sökväg:

`/libs/cq/core/content/welcome`

Det finns tre avsnitt (med ett mellanrum) som standard:

<table>
 <tbody>
  <tr>
   <td><strong>Resurser</strong></td>
   <td> </td>
  </tr>
  <tr>
   <td> Cloud Services</td>
   <td><code>/libs/cq/core/content/welcome/resources/cloudservices</code></td>
  </tr>
  <tr>
   <td> Arbetsflöden</td>
   <td><code>/libs/cq/core/content/welcome/resources/workflows</code></td>
  </tr>
  <tr>
   <td> Aktivitetshantering</td>
   <td><code>/libs/cq/core/content/welcome/resources/taskmanager</code></td>
  </tr>
  <tr>
   <td> Replikering</td>
   <td><code>/libs/cq/core/content/welcome/resources/replication</code></td>
  </tr>
  <tr>
   <td> Rapporter</td>
   <td><code>/libs/cq/core/content/welcome/resources/reports</code></td>
  </tr>
  <tr>
   <td> Publikationer</td>
   <td><code>/libs/cq/core/content/welcome/resources/publishingadmin</code></td>
  </tr>
  <tr>
   <td> Manuscript</td>
   <td><code>/libs/cq/core/content/welcome/resources/manuscriptsadmin</code></td>
  </tr>
  <tr>
   <td><strong>Dokumentation och referens</strong></td>
   <td> </td>
  </tr>
  <tr>
   <td> Dokumentation</td>
   <td><code>/libs/cq/core/content/welcome/docs/docs</code></td>
  </tr>
  <tr>
   <td> Resurser för utvecklare</td>
   <td><code>/libs/cq/core/content/welcome/docs/dev</code></td>
  </tr>
  <tr>
   <td><strong>Funktioner</strong></td>
   <td> </td>
  </tr>
  <tr>
   <td> CRXDE Lite</td>
   <td><code>/libs/cq/core/content/welcome/features/crxde</code></td>
  </tr>
  <tr>
   <td> Paket</td>
   <td><code>/libs/cq/core/content/welcome/features/packages</code></td>
  </tr>
  <tr>
   <td> Paketdelning</td>
   <td><code>/libs/cq/core/content/welcome/features/share</code></td>
  </tr>
  <tr>
   <td> Klustring</td>
   <td><code>/libs/cq/core/content/welcome/features/cluster</code></td>
  </tr>
  <tr>
   <td> Säkerhetskopiering</td>
   <td><code>/libs/cq/core/content/welcome/features/backup</code></td>
  </tr>
  <tr>
   <td> Webbkonsol<br /> </td>
   <td><code>/libs/cq/core/content/welcome/features/config</code></td>
  </tr>
  <tr>
   <td> Statusdump för webbkonsol<br /> </td>
   <td><code>/libs/cq/core/content/welcome/features/statusdump</code></td>
  </tr>
 </tbody>
</table>

#### Konfigurera om sidofältslänkar är synliga {#configuring-whether-sidebar-links-are-visible}

Du kan dölja en länk för specifika användare eller grupper genom att ta bort läsåtkomst till de noder som representerar länken.

* Resurser - ta bort åtkomst till:

   `/libs/cq/core/content/welcome/resources/<link-target>`

* Dokument - ta bort åtkomst till:

   `/libs/cq/core/content/welcome/docs/<link-target>`

* Funktioner - ta bort åtkomst till:

   `/libs/cq/core/content/welcome/features/<link-target>`

Till exempel:

* Ta bort länken till **Rapporter**, ta bort läsåtkomst från

   `/libs/cq/core/content/welcome/resources/reports`

* Ta bort länken till **Paket**, ta bort läsåtkomst från

   `/libs/cq/core/content/welcome/features/packages`

Se [Security section](/help/sites-administering/security.md) om du vill ha mer information om hur du anger behörigheter.

### Länkmarkeringsmekanism {#link-selection-mechanism}

I `/libs/cq/core/components/welcome/welcome.jsp` används [ConsoleUtil](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/ConsoleUtil.html), som kör en fråga på noder som har egenskapen:

* `jcr:mixinTypes` med värdet: `cq:Console`

>[!NOTE]
>
>Kör följande fråga för att se den befintliga listan:
>
>* `select * from cq:Console`
>


När en användare eller grupp inte har läsbehörighet för en nod med `cq:Console`, den noden hämtas inte av `ConsoleUtil` sökning, därför visas den inte på konsolen.

### Lägga till ett anpassat objekt {#adding-a-custom-item}

The [länkmarkeringsmekanism](#link-selection-mechanism) kan användas för att lägga till egna anpassade objekt i länklistan.

Lägg till ditt anpassade objekt i listan genom att lägga till `cq:Console` mixin i widgeten eller resursen. Detta görs genom att definiera egenskapen:

* `jcr:mixinTypes` med värdet: `cq:Console`
