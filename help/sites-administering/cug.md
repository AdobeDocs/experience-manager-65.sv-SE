---
title: Skapa en stängd användargrupp
seo-title: Creating a Closed User Group
description: Lär dig hur du skapar en stängd användargrupp.
seo-description: Learn how to create a Closed User Group.
uuid: dc3c7dbd-2e86-43f9-9377-3b75053203b3
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: 6ae57874-a9a1-4208-9001-7f44a1f57cbe
docset: aem65
exl-id: 9efba91d-45e8-42e1-9db6-490d21bf7412
source-git-commit: 64d174cc824c8bf200cece4e29f60f946ee5560e
workflow-type: tm+mt
source-wordcount: '753'
ht-degree: 0%

---

# Skapa en stängd användargrupp{#creating-a-closed-user-group}

Stängda användargrupper (CUG) används för att begränsa åtkomst till specifika sidor som finns på en publicerad webbplats. Sådana sidor kräver att de tilldelade medlemmarna loggar in och anger säkerhetsuppgifter.

Om du vill konfigurera ett sådant område på din webbplats:

* [skapa den faktiska stängda användargruppen och tilldela medlemmar](#creating-the-user-group-to-be-used).

* [använd den här gruppen på de obligatoriska sidorna](#applying-your-closed-user-group-to-content-pages) och välja (eller skapa) inloggningssidan som ska användas av medlemmarna i CUG-gruppen, anges också när en CUG används på en innehållssida.

* [skapa en länk, av någon form, till minst en sida inom det skyddade området](#linking-to-the-cug-pages), annars syns den inte.

* [konfigurera Dispatcher](#configure-dispatcher-for-cugs) om den används.

>[!CAUTION]
>
>Stängda användargrupper (CUG) bör alltid skapas med prestandahänsyn i åtanke.
>
>Även om antalet användare och grupper i en CUG inte är begränsat, kan ett stort antal CUG-filer på en sida försämra återgivningsprestanda.
>
>Effekten av användargränssnitten bör alltid beaktas vid prestandatestning.

## Skapa användargruppen som ska användas {#creating-the-user-group-to-be-used}

Så här skapar du en sluten användargrupp:

1. Gå till **Verktyg - Säkerhet** från AEM hemskärm.

   >[!NOTE]
   >
   >Se [Hantera användare och grupper](/help/sites-administering/security.md#managing-users-and-groups) om du vill ha fullständig information om hur du skapar och konfigurerar användare och grupper.

1. Välj **Grupper** från nästa skärm.

   ![screenshot_2018-10-30at145502](assets/screenshot_2018-10-30at145502.png)

1. Tryck på **Skapa** i det övre högra hörnet för att skapa en ny grupp.
1. Namnge din nya grupp; till exempel `cug_access`.

   ![screenshot_2018-10-30at151459](assets/screenshot_2018-10-30at151459.png)

1. Gå till **Medlemmar** och tilldela de användare som krävs till den här gruppen.

   ![screenshot_2018-10-30at151808](assets/screenshot_2018-10-30at151808.png)

1. Aktivera användare som du har tilldelat din CUG; i detta fall alla medlemmar i `cug_access`.
1. Aktivera den slutna användargruppen så att den är tillgänglig i publiceringsmiljön. i det här exemplet `cug_access`.

## Använda din stängda användargrupp på innehållssidor {#applying-your-closed-user-group-to-content-pages}

Så här använder du CUG-filen på en sida eller sidor:

1. Navigera till rotsidan för det begränsade avsnitt som du vill tilldela din CUG.
1. Markera sidan genom att klicka på dess miniatyrbild och sedan markera **Egenskaper** i det övre verktygsfältet.

   ![screenshot_2018-10-30at162632](assets/screenshot_2018-10-30at162632.png)

1. I följande fönster öppnar du **Avancerat** -fliken.

1. Bläddra nedåt till **Autentiseringskrav** -avsnitt.

   1. Aktivera **Aktivera** kryssruta.

   1. Lägg till sökvägen till **Inloggningssida**.
Detta är valfritt. Om det lämnas tomt används standardinloggningssidan.

   ![CUG har lagts till](assets/cug-authentication-requirement.png)

1. Gå till **Behörigheter** och markera **Redigera stängd användargrupp**.

   ![screenshot_2018-10-30at163003](assets/screenshot_2018-10-30at163003.png)

   >[!NOTE]
   >
   >CUG-filer på fliken Behörigheter kan inte rullas ut till Live-kopior från utkast. Se till att du undviker detta när du konfigurerar Live Copy.
   >
   >Mer information finns i [den här sidan](closed-user-groups.md#aem-livecopy).

1. The **Redigera stängd användargrupp** öppnas. Här kan du söka efter och välja din CUG och sedan bekräfta gruppmarkeringen med **Spara**.

   Gruppen skall läggas till i förteckningen. till exempel gruppen **cug_access**.

   ![CUG har lagts till](assets/cug-added.png)

1. Bekräfta ändringarna med **Spara och stäng**.

>[!NOTE]
>
>Se [Identity Management](/help/sites-administering/identity-management.md) om du vill ha information om profiler i publiceringsmiljön och om hur du loggar in och ut.

## Länka till CUG-sidor {#linking-to-the-cug-pages}

Eftersom målet för länkarna till CUG-sidorna inte är synligt för den anonyma användaren kommer länkkontrollen att ta bort sådana länkar.

För att undvika detta bör du skapa oskyddade omdirigeringssidor som pekar mot sidor i CUG-området. Navigeringsposterna återges sedan utan att länkkontrollen orsakar några problem. Det är bara när användaren faktiskt kommer åt omdirigeringssidan som omdirigeras inuti CUG-området, efter att inloggningsuppgifterna har angetts.

## Konfigurera Dispatcher för CUG:er {#configure-dispatcher-for-cugs}

Om du använder Dispatcher måste du definiera en Dispatcher-servergrupp med följande egenskaper:

* [virtualhosts](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=en#identifying-virtual-hosts-virtualhosts): Matchar sökvägen till sidorna som CUG gäller för.
* \sessionshantering: se nedan.
* [cache](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=en#configuring-the-dispatcher-cache-cache): En cachekatalog som är dedikerad till de filer som CUG gäller för.

### Konfigurera Dispatcher Session Management för CUG:er {#configuring-dispatcher-session-management-for-cugs}

Konfigurera [sessionshantering i dispatcher.alla filer](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=en#enabling-secure-sessions-sessionmanagement) för CUG. Den autentiseringshanterare som används när åtkomst begärs för CUG-sidor avgör hur du konfigurerar sessionshanteringen.

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

1. Konfigurera [/sessionmanagement](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=en#enabling-secure-sessions-sessionmanagement) efter definition `/directory`; till exempel:

   ```xml
   /sessionmanagement
     {
     /directory "/usr/local/apache/.sessions"
     ...
     }
   ```

1. Ange [/allowAuthorized](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=en#caching-when-authentication-is-used) till `0`.
