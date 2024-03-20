---
title: Omstrukturering av Forms-lager i AEM 6.5
description: Lär dig hur du gör de ändringar som krävs för att migrera till den nya databasstrukturen i AEM 6.5 för Forms.
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: repo_restructuring
feature: Upgrading
exl-id: d555422e-dc97-4d45-9525-4299d22315e2
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '519'
ht-degree: 0%

---

# Omstrukturering av Forms-lager i AEM 6.5{#forms-repository-restructuring-in-aem}

Enligt beskrivning på överordnad [Omstrukturering av lager i AEM 6.5](/help/sites-deploying/repository-restructuring.md) på denna sida bör kunder som uppgraderar till AEM 6.5 använda denna sida för att bedöma arbetsinsatsen i samband med databasändringar som påverkar AEM Forms-lösningen. Vissa ändringar kräver arbete under uppgraderingsprocessen för AEM 6.5, medan andra kan skjutas upp till en framtida uppgradering.

**Med 6.5-uppgradering**

* [Diverse](/help/sites-deploying/forms-repository-restructuring-in-aem-6-5.md#misc)

**Före framtida uppgradering**

* [Konfiguration av EchoSign-Cloud Service](/help/sites-deploying/forms-repository-restructuring-in-aem-6-5.md#echosign-cloud-service-configuration)
* [Konfigurationer av Recaptcha-Cloud Service](/help/sites-deploying/forms-repository-restructuring-in-aem-6-5.md#recaptcha-cloud-service-configurations)
* [Konfigurationer av Typekit-Cloud Service](/help/sites-deploying/forms-repository-restructuring-in-aem-6-5.md#typekit-cloud-service-configurations)
* [Diverse](/help/sites-deploying/forms-repository-restructuring-in-aem-6-5.md#misc)

## Med 6.5-uppgradering {#with-upgrade}

### Diverse {#misc}

| **Föregående plats** | `/etc/clientlibs/fd/fp` |
|---|---|
| **Ny plats** | `/libs/fd/fp/components` |
| **Omstruktureringsvägledning** | Alla explicita referenser i anpassad kod till den äldre platsen måste uppdateras till den nya platsen. |
| **Anteckningar** | Dessa klientbibliotek får inte redigeras eller utökas. |

| **Föregående plats** | `/etc/clientlibs/fd/rte` |
|---|---|
| **Ny plats** | `/libs/fd/rte` |
| **Omstruktureringsvägledning** | För resurser i klientlibs som kan refereras av absoluta sökvägar måste du använda nyare sökvägar i nya resurser. |
| **Anteckningar** | Ej tillämpligt |

| **Föregående plats** | `/etc/clientlibs/fd/af` |
|---|---|
| **Ny plats** | `/libs/fd/af/authoring/clientlibs` |
| **Omstruktureringsvägledning** | För resurser i klientlibs som kan refereras av absoluta sökvägar måste du använda nyare sökvägar i nya resurser. |
| **Anteckningar** | Ej tillämpligt |

| **Föregående plats** | `/etc/clientlibs/fd/xfaforms` |
|---|---|
| **Ny plats** | `/libs/fd/xfaforms/clientlibs/` |
| **Omstruktureringsvägledning** | För resurser i klientlibs som kan refereras av absoluta sökvägar måste du använda nyare sökvägar i nya resurser. |
| **Anteckningar** | Ej tillämpligt |

| **Föregående plats** | `/etc/clientlibs/fd/af` |
|---|---|
| **Ny plats** | `/libs/fd/af/runtime/clientlibs` |
| **Omstruktureringsvägledning** | För resurser i klientlibs som kan refereras av absoluta sökvägar måste du använda nyare sökvägar i nya resurser. |
| **Anteckningar** | Ej tillämpligt |

| **Föregående plats** | `/etc/clientlibs/fd/af` |
|---|---|
| **Ny plats** | `/libs/fd/af/runtime/clientlibs` |
| **Omstruktureringsvägledning** | För resurser i klientlibs som kan refereras av absoluta sökvägar måste du använda nyare sökvägar i nya resurser. |
| **Anteckningar** | Ej tillämpligt |

| **Föregående plats** | `/etc/clientlibs/fd/expeditor` |
|---|---|
| **Ny plats** | `/libs/fd/expeditor/clientlibs` |
| **Omstruktureringsvägledning** | För resurser i klientlibs som kan refereras av absoluta sökvägar måste du använda nyare sökvägar i nya resurser. |
| **Anteckningar** | Ej tillämpligt |

| **Föregående plats** | `/etc/clientlibs/fd/fmaddon` |
|---|---|
| **Ny plats** | `/libs/fd/fmaddon` |
| **Omstruktureringsvägledning** | Att ändra dessa klientlibs har aldrig rekommenderats eller fått stöd. Om du har gjort ändringar i dessa klientlibs bör du återställa dem så att du kan använda den AEM koden. |
| **Anteckningar** | Ej tillämpligt |

| **Föregående plats** | `/etc/aep` |
|---|---|
| **Ny plats** | `/var/fd/content/annotations` |
| **Omstruktureringsvägledning** | Att ändra dessa klientlibs har aldrig rekommenderats eller fått stöd. Om du har gjort ändringar i dessa klientlibs bör du återställa dem så att du kan använda den AEM koden. |
| **Anteckningar** | Ej tillämpligt |

## Före framtida uppgradering {#prior-to-upgrade}

### Konfiguration av EchoSign-Cloud Service {#echosign-cloud-service-configuration}

| **Föregående plats** | `/etc/cloudservices/echosign` |
|---|---|
| **Ny plats** | `/conf/<tenant>/settings/cloudconfigs/echosign` |
| **Omstruktureringsvägledning** | The [Lazy Content Migration](/help/sites-deploying/lazy-content-migration.md) verktyg som ska utlösas från Forms migreringsgränssnitt. |
| **Anteckningar** | Ej tillämpligt |

### Konfigurationer av Recaptcha-Cloud Service {#recaptcha-cloud-service-configurations}

| **Föregående plats** | `/etc/cloudservices/recaptcha` |
|---|---|
| **Ny plats** | `/conf/<tenant>/settings/cloudconfigs/recaptcha` |
| **Omstruktureringsvägledning** | The [Lazy Content Migration](/help/sites-deploying/lazy-content-migration.md) verktyg som ska utlösas från Forms migreringsgränssnitt. |
| **Anteckningar** | Ej tillämpligt |

### Konfigurationer av Typekit-Cloud Service {#typekit-cloud-service-configurations}

| **Föregående plats** | `/etc/cloudservices/typekit` |
|---|---|
| **Ny plats** | `/conf/<tenant>/settings/cloudconfigs/typekit` |
| **Omstruktureringsvägledning** | The [Lazy Content Migration](/help/sites-deploying/lazy-content-migration.md) verktyg som ska utlösas från Forms migreringsgränssnitt. |
| **Anteckningar** | Ej tillämpligt |

### Diverse {#misc-1}

| **Föregående plats** | `/etc/cloudservices/fdm` |
|---|---|
| **Ny plats** | `/conf/<tenant>/settings/cloudconfigs/fdm` |
| **Omstruktureringsvägledning** | The [Lazy Content Migration](/help/sites-deploying/lazy-content-migration.md) verktyg som ska utlösas från Forms migreringsgränssnitt. |
| **Anteckningar** | Ej tillämpligt |

| **Föregående plats** | `/etc/designs/fd/fp` |
|---|---|
| **Ny plats** | `/libs/fd/fp` |
| **Omstruktureringsvägledning** | Uppdatera referenser till mallarna /etc för att peka på dem `/libs` motpart. |
| **Anteckningar** | Ej tillämpligt |
