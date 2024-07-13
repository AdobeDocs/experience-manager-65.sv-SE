---
title: Grundläggande om communityn
description: Exportera och ta bort communitywebbplatser och skapa anpassade webbplatsmallar
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 1dc568cd-315c-4944-9a3e-e5d7794e5dc0
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '486'
ht-degree: 0%

---

# Grundläggande om communityn {#community-site-essentials}

## Anpassad webbplatsmall {#custom-site-template}

En anpassad webbplatsmall kan anges separat för varje språkkopia av en communitywebbplats.

Så här gör du:

* Skapa en anpassad mall.
* Lägg över standardsökvägen för webbplatsmallen.
* Lägg till den anpassade mallen i överläggsbanan.
* Ange den anpassade mallen genom att lägga till en `page-template`-egenskap i noden `configuration`.

**Standardmall**:

`/libs/social/console/components/hbs/sitepage/sitepage.hbs`

**Anpassad mall i övertäckningssökväg**:

`/apps/social/console/components/hbs/sitepage/template-name.hbs`

**Egenskap**: sidmall

**Typ**: Sträng

**Värde**: `template-name` (inget tillägg)

**Konfigurationsnod**:

`/content/community site path/lang/configuration`

Till exempel: `/content/sites/engage/en/configuration`

>[!NOTE]
>
>Alla noder i den överlagda sökvägen behöver bara vara av typen `Folder`.

>[!CAUTION]
>
>Om den anpassade mallen ges namnet *sitepage.hbs* anpassas alla communitywebbplatser.

### Exempel på anpassad webbplatsmall {#custom-site-template-example}

`vertical-sitepage.hbs` är till exempel en webbplatsmall som placerar menylänkar lodrätt nedåt till vänster på sidan i stället för vågrätt nedanför banderollen.

[Hämta fil](assets/vertical-sitepage.hbs)
Placera den anpassade platsmallen i överläggsmappen:

`/apps/social/console/components/hbs/sitepage/vertical-sitepage.hbs`

Identifiera den anpassade mallen genom att lägga till en `page-template`-egenskap till konfigurationsnoden:

`/content/sites/sample/en/configuration`

![crxde-siteconfiguration](assets/crxde-siteconfiguration.png)

Se till att **Spara alla** och replikera anpassad kod till alla Adobe Experience Manager-instanser (AEM) (anpassad kod inkluderas inte när communityplatsinnehållet publiceras från konsolen).

Rekommenderad metod för replikering av anpassad kod är att [skapa ett paket](../../help/sites-administering/package-manager.md#creating-a-new-package) och distribuera det på alla instanser.

## Exportera en community-plats {#exporting-a-community-site}

När en communitywebbplats har skapats kan du exportera webbplatsen som ett AEM paket som lagras i Package Manager och som är tillgängligt för hämtning och överföring.

Det här är tillgängligt från konsolen [Webbplatser för ](sites-console.md#exporting-the-site).

UGC och anpassad kod ingår inte i communityplatspaketet.

Om du vill exportera UGC använder du [AEM Communities UGC-migreringsverktyget](https://github.com/Adobe-Marketing-Cloud/aem-communities-ugc-migration), ett migreringsverktyg med öppen källkod som är tillgängligt på GitHub.

## Ta bort en communitywebbplats {#deleting-a-community-site}

Från och med AEM Communities 6.3 Service Pack 1 visas ikonen Ta bort plats när du hovrar över communitywebbplatsen från **[!UICONTROL Communities]** > **[!UICONTROL Sites]**-konsolen. Om du vill ta bort en community-webbplats och börja om från början kan du använda den här funktionen. Om du tar bort en community-webbplats tas följande objekt som är kopplade till den platsen bort:

* [UGC](#user-generated-content)
* [Användargrupper](#community-user-groups)
* [Databasposter](#database-records)

### Unikt plats-ID för community {#community-unique-site-id}

Så här identifierar du det unika plats-ID som är kopplat till communityplatsen med hjälp av CRXDE:

* Navigera till webbplatsens språkrot, till exempel `/content/sites/*<site name>*/en/rep:policy`.

* Hitta noden `allow<#>` med en `rep:principalName` i det här formatet `rep:principalName = *community-enable-nrh9h-members*`.

* Plats-ID är den tredje komponenten i `rep:principalName`

  Om `rep:principalName = community-enable-nrh9h-members` till exempel

   * **platsnamn** = *aktivera*
   * **plats-ID** = *nrh9h*
   * **unikt plats-ID** = *enable-nrh9h*

### Användargenererat innehåll {#user-generated-content}

Hämta communityn-srp-tools-projektet från GitHub:

* [https://github.com/Adobe-Marketing-Cloud/aem-communities-srp-tools](https://github.com/Adobe-Marketing-Cloud/aem-communities-srp-tools)

Det här innehåller en servett som tar bort all UGC från en SRP.

All UGC kan tas bort eller för en specifik plats, till exempel:

* `path=/content/usergenerated/asi/mongo/content/sites/engage`

Detta tar endast bort användargenererat innehåll (som anges vid publicering) och inte redigerat innehåll (anges av författaren). Därför påverkas inte [skuggnoderna](srp.md#shadownodes).

### Användargrupper {#community-user-groups}

På alla författare- och publiceringsinstanser från [säkerhetskonsolen](../../help/sites-administering/security.md) letar du upp och tar bort de [användargrupper](users.md) som är:

* Har prefixats med `community`
* Följd av [unikt webbplats-ID](#community-unique-site-id)

Exempel: `community-engage-x0e11-members`.
