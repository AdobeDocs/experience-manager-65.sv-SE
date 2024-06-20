---
title: Användarhantering
description: Med användarhantering kan du aktivera enkel inloggning mellan AEM formulärmoduler och Netegrity SiteMinder-skyddade program med SAML. Det här dokumentet innehåller mer information om användarhantering.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_aem_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 1da1f6de-ac0d-4e0d-b8bb-956420e42699
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '472'
ht-degree: 0%

---

# Användarhantering {#user-management}

Med användarhantering kan du aktivera enkel inloggning (SSO) mellan AEM formulärmoduler och Netegrity SiteMinder-skyddade program med SAML (Security Assertion Markup Language). När enkel inloggning är implementerad är AEM inloggningssidor inte obligatoriska och visas inte om användaren redan är autentiserad via företagsportalen.

Mer information om hur du förbättrar prestanda för databas- och katalogsynkronisering för DB2 finns i [IBM DB2-databas: Kör kommandon för regelbundet underhåll](/help/forms/using/admin-help/ibm-db2-database-running-commands.md#ibm-db2-database-running-commands-for-regular-maintenance).

## Konfigurera användarhantering för en SSL-aktiverad LDAP-server {#configuring-user-management-for-an-ssl-enabled-ldap-server}

Om du har en SSL-aktiverad LDAP-server konfigurerar du användarhantering så att den fungerar med den. (Se [Konfigurera användarhantering för en SSL-aktiverad LDAP-server](/help/forms/using/admin-help/configure-user-management-ssl-enabled.md#configure-user-management-for-an-ssl-enabled-ldap-server).)

## Ställa in användarbehörighet för dokumentsäkerhet {#setting-user-privileges-for-use-with-document-security}

Skapa en administratörsanvändare som har lämplig behörighet för att skapa användare och grupper. Om din AEM innehåller dokumentskydd ger du behörighet att hantera inbjudna och lokala användare till en användare som är administratör för dessa användare. Tilldela även administratörskonsolens användarroll för att ge användaren åtkomst till administrationskonsolen. (Se [Skapa och konfigurera roller](/help/forms/using/admin-help/creating-configuring-roles.md#creating-and-configuring-roles).)

Om du vill visa användare och grupper i valda domäner under principanvändarsökningar måste en superadministratör eller administratör för principuppsättningen markera och lägga till domäner (skapade i Användarhantering) i listan över synliga användare och grupper för varje principuppsättning som skapas.

Listan med synliga användare och grupper är synlig för principuppsättningens koordinator och används för att begränsa vilka domäner slutanvändaren kan bläddra i när han eller hon väljer användare eller grupper att lägga till i profiler. Om den här åtgärden inte utförs kommer principuppsättningskoordinatorn inte att hitta några användare eller grupper att lägga till i principen. Det kan finnas fler än en principuppsättningskoordinator för en given principuppsättning.

>[!NOTE]
>
>Du måste skapa domäner innan du kan skapa profiler.

### Ange synliga användare och grupper {#set-visible-users-and-groups}

När du har installerat och konfigurerat din AEM formulärmiljö med Document Security konfigurerar du alla lämpliga domäner i Användarhantering.

1. I administrationskonsolen klickar du på Tjänster > Dokumentsäkerhet > Profiler och sedan på fliken Principuppsättningar.
1. Välj Global principuppsättning och klicka sedan på fliken Synliga användare och grupper.
1. Klicka på Lägg till domän(er) och lägg till befintliga domäner efter behov.
1. Navigera till Tjänster > Dokumentsäkerhet > Konfiguration > Mina principer och klicka på fliken Synliga användare och grupper.
1. Klicka på Lägg till domän(er) och lägg till befintliga domäner efter behov.

## Begränsningar för administratörsanvändare {#administrator-user-restrictions}

Användare med vissa typer av administratörsbehörighet kan av säkerhetsskäl inte komma åt arbetsytans slutanvändarsidor. Eftersom dessa webbsidor kan finnas utanför en brandvägg kan det utgöra en säkerhetsrisk att tillåta åtgärder på administrationsnivå. Endast användare som har behörigheten Workspace Administrator eller Workspace User har åtkomst till slutanvändarens webbsidor.

>[!NOTE]
>
>Flex Workspace är föråldrat för AEM formulärreleaser.
