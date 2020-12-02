---
title: Skapa en stängd användargrupp
seo-title: Skapa en stängd användargrupp
description: Lär dig hur du skapar en stängd användargrupp.
seo-description: Lär dig hur du skapar en stängd användargrupp.
uuid: dc3c7dbd-2e86-43f9-9377-3b75053203b3
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: 6ae57874-a9a1-4208-9001-7f44a1f57cbe
docset: aem65
translation-type: tm+mt
source-git-commit: 29328ff7fde4ed0e7f9728af1be911133259dc6c
workflow-type: tm+mt
source-wordcount: '808'
ht-degree: 0%

---


# Skapa en stängd användargrupp{#creating-a-closed-user-group}

Stängda användargrupper (CUG) används för att begränsa åtkomst till specifika sidor som finns på en publicerad webbplats. Sådana sidor kräver att de tilldelade medlemmarna loggar in och anger säkerhetsuppgifter.

Om du vill konfigurera ett sådant område på din webbplats:

* [skapa den faktiska stängda användargruppen och tilldela medlemmar](#creating-the-user-group-to-be-used).

* [tillämpa denna grupp på de önskade ](#applying-your-closed-user-group-to-content-pages) sidorna och välja (eller skapa) inloggningssidan som ska användas av medlemmarna i CUG, anges också när en CUG används på en innehållssida.

* [skapa en länk, av någon form, till minst en sida inom det skyddade området](#linking-to-the-realm), annars visas den inte.
* [konfigurera ](#configure-dispatcher-for-cugs) Dispatcherif som används.

>[!CAUTION]
>
>Stängda användargrupper (CUG) bör alltid skapas med prestandahänsyn i åtanke.
>
>Även om antalet användare och grupper i en CUG inte är begränsat, kan ett stort antal CUG-filer på en sida försämra återgivningsprestanda.
>
>Effekten av användargränssnitten bör alltid beaktas vid prestandatestning.

## Skapar användargruppen som ska användas {#creating-the-user-group-to-be-used}

Så här skapar du en sluten användargrupp:

1. Gå till **Verktyg - Säkerhet** från AEM hemskärm.

   >[!NOTE]
   >
   >Mer information om hur du skapar och konfigurerar användare och grupper finns i [Hantera användare och grupper](/help/sites-administering/security.md#managing-users-and-groups).

1. Välj kortet **Grupper** på nästa skärm.

   ![screenshot_2018-10-30at145502](assets/screenshot_2018-10-30at145502.png)

1. Tryck på knappen **Skapa** i det övre högra hörnet för att skapa en ny grupp.
1. Namnge din nya grupp; till exempel `cug_access`.

   ![screenshot_2018-10-30at151459](assets/screenshot_2018-10-30at151459.png)

1. Gå till fliken **Medlemmar** och tilldela de användare som krävs till den här gruppen.

   ![screenshot_2018-10-30at151808](assets/screenshot_2018-10-30at151808.png)

1. Aktivera användare som du har tilldelat din CUG; i det här fallet alla medlemmar i `cug_access`.
1. Aktivera den slutna användargruppen så att den är tillgänglig i publiceringsmiljön. i det här exemplet är `cug_access`.

## Använda din stängda användargrupp på innehållssidor {#applying-your-closed-user-group-to-content-pages}

Så här använder du CUG-filen på en sida:

1. Navigera till rotsidan för det begränsade avsnitt som du vill tilldela din CUG.
1. Markera sidan genom att klicka på dess miniatyrbild och sedan på **Egenskaper** i den övre panelen.

   ![screenshot_2018-10-30at162632](assets/screenshot_2018-10-30at162632.png)

1. I följande fönster går du till fliken **Avancerat**.
1. Bläddra nedåt och aktivera kryssrutan i **Autentiseringskrav**-avsnittet.

1. Lägg till konfigurationssökvägen nedan och tryck sedan på Save.
1. Gå sedan till fliken **Behörigheter** och tryck på knappen **Redigera stängd användargrupp**.

   ![screenshot_2018-10-30at163003](assets/screenshot_2018-10-30at163003.png)

   >[OBS!]
   >
   > Observera att CUG-filer på fliken Behörigheter inte kan återställas från utkast till Live-kopior. Se till att du undviker detta när du konfigurerar Live Copy.
   >
   > Mer information finns i [den här sidan](closed-user-groups.md#aem-livecopy).

1. Sök efter och lägg till din CUG i följande fönster - lägg i det här fallet till gruppen **cug_access**. Tryck slutligen på **Save**.
1. Klicka på **Aktiverad** för att definiera att den här sidan (och alla underordnade sidor) tillhör en CUG.
1. Ange **inloggningssidan** som medlemmar i gruppen ska använda; till exempel:

   `/content/geometrixx/en/toolbar/login.html`

   Detta är valfritt. Om det lämnas tomt används standardinloggningssidan.

1. Lägg till **Tillåtna grupper**. Använd + för att lägga till grupper eller - för att ta bort. Endast medlemmar i dessa grupper tillåts logga in och få åtkomst till sidorna.
1. Tilldela en **sfär** (ett namn för sidgrupperna) om det behövs. Lämna tomt om du vill använda sidrubriken.
1. Klicka på **OK** för att spara specifikationen.

Se [Identity Management](/help/sites-administering/identity-management.md) om du vill ha information om profiler i publiceringsmiljön och om hur du loggar in och ut.

## Länka till sfären {#linking-to-the-realm}

Eftersom målet för länkar till CUG-miljön inte är synligt för den anonyma användaren, kommer länkkontrollen att ta bort sådana länkar.

För att undvika detta bör du skapa oskyddade omdirigeringssidor som pekar mot sidor i CUG-serien. Navigeringsposterna återges sedan utan att länkkontrollen orsakar några problem. Det är bara när användaren faktiskt kommer åt omdirigeringssidan som omdirigeras inuti CUG-butiken, efter att inloggningsuppgifterna har angetts.

## Konfigurera Dispatcher för CUG:er {#configure-dispatcher-for-cugs}

Om du använder Dispatcher måste du definiera en Dispatcher-servergrupp med följande egenskaper:

* [virtualhosts](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html#identifying-virtual-hosts-virtualhosts): Matchar sökvägen till sidorna som CUG gäller för.
* \sessionshantering: se nedan.
* [cache](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html#configuring-the-dispatcher-cache-cache): En cachekatalog som är dedikerad till de filer som CUG gäller för.

### Konfigurerar Hantering av dispatcher-session för CUG:er {#configuring-dispatcher-session-management-for-cugs}

Konfigurera [sessionshantering i dispatchern.alla filer](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html#enabling-secure-sessions-sessionmanagement) för CUG:n. Den autentiseringshanterare som används när åtkomst begärs för CUG-sidor avgör hur du konfigurerar sessionshanteringen.

```xml
/sessionmanagement
    ...
    /header "Cookie:login-token"
    ...
```

>[!NOTE]
>
>När en Dispatcher-servergrupp har sessionshantering aktiverat cachelagras inte alla sidor som servergruppen hanterar. Om du vill cachelagra sidor som ligger utanför CUG skapar du en andra grupp i dispatcher.any
>som hanterar icke-CUG-sidor.

1. Konfigurera [/sessionmanagement](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html#enabling-secure-sessions-sessionmanagement) genom att definiera `/directory`; till exempel:

   ```xml
   /sessionmanagement
     {
     /directory "/usr/local/apache/.sessions"
     ...
     }
   ```

1. Ange [/allowAuthorized](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html#caching-when-authentication-is-used) till `0`.

