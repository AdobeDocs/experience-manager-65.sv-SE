---
title: Grundläggande om communitysajter
seo-title: Grundläggande om communitysajter
description: Exportera och ta bort communitysajter och skapa anpassade webbplatsmallar
seo-description: Exportera och ta bort communitysajter och skapa anpassade webbplatsmallar
uuid: f0ec0e71-64e9-415a-b14a-939a9b1611c1
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: dc7a085e-d6de-4bc8-bd7e-6b43f8d172d2
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '568'
ht-degree: 1%

---


# Grundläggande om communitywebbplats {#community-site-essentials}

## Anpassad webbplatsmall {#custom-site-template}

En anpassad webbplatsmall kan anges separat för varje språkkopia av en communitywebbplats.

Så här gör du:

* Skapa en anpassad mall.
* Lägg över standardsökvägen för webbplatsmallen.
* Lägg till den anpassade mallen i överläggsbanan.
* Ange den anpassade mallen genom att lägga till en `page-template`-egenskap till noden `configuration`.

**Standardmall**:

`/libs/social/console/components/hbs/sitepage/sitepage.hbs`

**Anpassad mall i övertäckningssökväg**:

`/apps/social/console/components/hbs/sitepage/template-name.hbs`

**Egenskap**: page-template

**Typ**: Sträng

**Värde**:  `template-name` (inget tillägg)

**Konfigurationsnod**:

`/content/community site path/lang/configuration`

Till exempel: `/content/sites/engage/en/configuration`

>[!NOTE]
>
>Alla noder i den överlagda sökvägen behöver bara vara av typen `Folder`.

>[!CAUTION]
>
>Om den anpassade mallen får namnet *sitepage.hbs*, anpassas alla communitywebbplatser.

### Exempel på anpassad webbplatsmall {#custom-site-template-example}

Som ett exempel är `vertical-sitepage.hbs` en webbplatsmall som leder till att menylänkar placeras lodrätt nedåt till vänster på sidan, i stället för vågrätt nedanför banderollen.

[Hämta ](assets/vertical-sitepage.hbs)
filPlacera den anpassade platsmallen i överläggsmappen:

`/apps/social/console/components/hbs/sitepage/vertical-sitepage.hbs`

Identifiera den anpassade mallen genom att lägga till en `page-template`-egenskap till konfigurationsnoden:

`/content/sites/sample/en/configuration`

![crxde-siteconfiguration](assets/crxde-siteconfiguration.png)

Var noga med att **spara alla** och replikera anpassad kod till alla AEM instanser (anpassad kod inkluderas inte när innehållet för communityplatsen publiceras från konsolen).

Rekommenderad metod för att replikera anpassad kod är att [skapa ett paket](../../help/sites-administering/package-manager.md#creating-a-new-package) och distribuera det på alla instanser.

## Exportera en community-plats {#exporting-a-community-site}

När en communitywebbplats har skapats kan du exportera webbplatsen som ett AEM paket som lagras i pakethanteraren och som är tillgängligt för hämtning och överföring.

Det här är tillgängligt från [webbgruppskonsolen](sites-console.md#exporting-the-site).

Observera att UGC och anpassad kod inte ingår i communitywebbplatspaketet.

Om du vill exportera UGC använder du [AEM Communities UGC-migreringsverktyget](https://github.com/Adobe-Marketing-Cloud/communities-ugc-migration), ett migreringsverktyg med öppen källkod som är tillgängligt på GitHub.

## Tar bort en community-plats {#deleting-a-community-site}

Från och med AEM Communities 6.3 Service Pack 1 visas ikonen Ta bort plats när du hovrar över communityplatsen från **[!UICONTROL Communities]** > **[!UICONTROL Sites]**-konsolen. Om du vill ta bort en community-webbplats och börja om från början kan du använda den här funktionen. Om du tar bort en community-webbplats tas följande objekt som är kopplade till den platsen bort:

* [UGC](#user-generated-content)
* [Användargrupper](#community-user-groups)
* [Assets](#enablement-assets)
* [Databasposter](#database-records)

### Unikt plats-ID för community {#community-unique-site-id}

Så här identifierar du det unika plats-ID som är kopplat till communityplatsen med hjälp av CRXDE:

* Navigera till webbplatsens språkrot, till exempel `/content/sites/*<site name>*/en/rep:policy`.

* Hitta `allow<#>`-noden med `rep:principalName` i det här formatet `rep:principalName = *community-enable-nrh9h-members*`.

* Plats-ID är den tredje komponenten i `rep:principalName`

   Om `rep:principalName = community-enable-nrh9h-members`

   * **platsnamn** =  *aktivera*
   * **site ID** =  *nrh9h*
   * **unikt webbplats-ID** =  *enable-nrh9h*

### Användargenererat innehåll {#user-generated-content}

Hämta projektet Community-srp-tools från Github:

* [https://github.com/Adobe-Marketing-Cloud/communities-srp-tools](https://github.com/Adobe-Marketing-Cloud/communities-srp-tools)

Det här innehåller en servett som tar bort all UGC från en SRP.

All UGC kan tas bort eller för en specifik plats, till exempel:

* `path=/content/usergenerated/asi/mongo/content/sites/engage`

Detta tar endast bort användargenererat innehåll (som anges vid publicering) och inte redigerat innehåll (anges av författaren). Därför påverkas inte [skuggnoder](srp.md#shadownodes).

### Användargrupper för Community {#community-user-groups}

På alla författare- och publiceringsinstanser går du till [säkerhetskonsolen](../../help/sites-administering/security.md) och letar reda på och tar bort de [användargrupper](users.md) som är:

* Förfixat med `community`
* Följd av [unikt plats-ID](#community-unique-site-id)

Till exempel, `community-engage-x0e11-members`.

### Aktivera resurser {#enablement-assets}

Från huvudkonsolen:

* Välj **[!UICONTROL Assets]**.
* Ange **[!UICONTROL Select]**-läge.
* Välj en mapp med namnet [unikt plats-ID](#community-unique-site-id).
* Välj **[!UICONTROL Delete]** (kan behöva välja från **[!UICONTROL More...]**).

### Databasposter {#database-records}

Det finns inget verktyg för att selektivt ta bort databasposter för en specifik aktiveringscommunitywebbplats.

När alla communitysajter tas bort, släpper du aktiveringsdb och scormenginedb med MySQL Workbench.
