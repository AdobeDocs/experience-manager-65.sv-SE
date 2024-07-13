---
title: Anpassade HTTP-huvuden
description: Lär dig hur du konfigurerar anpassade HTTP-rubriker i Adobe Experience Manager Commerce.
exl-id: 834aadac-c3be-4e7a-a3cb-349608810b40
solution: Experience Manager,Commerce
feature: Commerce Integration Framework
role: Admin, Developer
source-git-commit: 10268f617b8a1bb22f1f131cfd88236e7d5beb47
workflow-type: tm+mt
source-wordcount: '267'
ht-degree: 0%

---

# Anpassade HTTP-huvuden {#custom-http-headers}

## Ökning {#overview}

För att få bättre kontroll över sin serverdel kan författarna konfigurera anpassade HTTP-rubriker som skickas till e-handelsmotorn, tillsammans med de som redan skickats av CIF. Vanliga användningsfall är bland annat multibutiksinställningar där du kan använda HTTP-huvuden för att styra svaret från e-handelsserverdelen.

>[!NOTE]
>
>Utvecklare kan alltid konfigurera anpassade HTTP-huvuden med hjälp av GraphQL klientkonfiguration.
>

## Konfiguration {#configuration}

Om du vill konfigurera anpassade HTTP-huvuden måste du först definiera dem. De anpassade HTTP-rubrikerna måste först definieras genom att de läggs till i tjänstkonfigurationen `com.adobe.cq.cif.http.internal.HttpHeadersConfigProviderImpl` med en OSGi-konfiguration.

Du kan konfigurera värdena för HTTP-rubrikerna på Cloud Servicens konfigurationssida för ditt projekt:

1. Gå till konfigurationssidan för Cloud Servicen under Verktyg > Cloud Services > CIF Konfiguration.
1. Öppna en befintlig konfiguration eller skapa en.
1. Gå till fliken &quot;Avancerat&quot; och leta upp det anpassade fältet för HTTP-rubriker. Du kan markera rubrikerna som du definierade tidigare och tilldela dem värden.

Komponenterna som använder molntjänstkonfigurationen ovan skickar dessa HTTP-huvuden med alla GraphQL-förfrågningar.

## Begränsningar {#restrictions}

Även om tjänsten tillåter att rubriknamn definieras, inklusive standardnamn, är de inte tillgängliga för konfigurering. Du kan alltså inte åsidosätta de vanliga HTTP-rubrikerna med den här funktionen. En lista med begränsade rubriknamn finns [här](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers). Det finns ytterligare två rubriker som inte kan användas:

* &quot;Store&quot; - används av CIF för att identifiera Adobe Commerce Store
* &quot;Preview-Version&quot; - används av CIF för att hämta mellanprodukter
