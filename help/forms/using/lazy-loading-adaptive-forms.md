---
title: Förbättra prestanda för stora formulär med lat inläsningsverktyg
seo-title: Förbättra prestanda för stora formulär med lat inläsningsverktyg
description: Lazy loading förbättrar prestanda avsevärt för stora och komplexa adaptiva formulär genom att skjuta upp initieringen och inläsningen av formulärfragment tills de syns.
seo-description: Lazy loading förbättrar prestanda avsevärt för stora och komplexa adaptiva formulär genom att skjuta upp initieringen och inläsningen av formulärfragment tills de syns.
uuid: 6be3d2f0-1b2a-4090-af66-2b08487c31bc
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: a20736b7-f7b4-4da1-aa32-2408049b1209
docset: aem65
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65

---


# Förbättra prestanda för stora formulär med lat inläsningsverktyg{#improve-performance-of-large-forms-with-lazy-loading}

## Introduktion till lazy loading {#introduction-to-lazy-loading}

När formuläret blir stort och komplext med hundratals och tusentals fält får slutanvändarna lång svarstid när de återger formulär vid körning. För att minimera svarstiden gör adaptiva formulär att du kan dela upp formulär i logiska fragment och konfigurera för att skjuta upp initiering eller inläsning av fragment tills fragmentet behöver vara synligt. Det kallas för lat inläsningsarbete. Dessutom tas de fragment som konfigurerats för lazy loading bort när användaren navigerar till andra avsnitt i formuläret och fragmenten inte längre visas.

Låt oss först förstå kraven och de förberedande stegen innan du konfigurerar lazy loading.

## Förbereder för att konfigurera lazy loading {#preparing-to-configure-lazy-loading}

Innan du konfigurerar lazy loading av fragment i ditt adaptiva formulär är det viktigt att du definierar strategier för att skapa fragment, identifiera värden som används i skript eller som refereras i andra fragment samt definierar regler för att styra visningen av fält i lagerinlästa fragment.

* **Identifiera och skapa fragment** Du kan bara konfigurera adaptiva formulärfragment för lazy loading. Ett fragment är ett fristående segment som ligger utanför ett anpassningsbart formulär och kan återanvändas i olika formulär. Så det första steget mot att implementera lat inläsningsarbete är att identifiera logiska avsnitt i ett formulär och konvertera dem till fragment. Du kan skapa ett fragment från grunden eller spara en befintlig formulärpanel som fragment.

   Mer information om att skapa fragment finns i [Adaptiva formulärfragment](../../forms/using/adaptive-form-fragments.md).

* **Identifiera och markera globala värden** Formulärbaserade transaktioner innefattar dynamiska element för att hämta in relevanta data från användarna och bearbeta dem för att förenkla ifyllandet av formulären. Formuläret har till exempel fält A i fragment X vars värde bestämmer giltigheten för fält B i ett annat fragment. Om fragment X i det här fallet har markerats för lazy loading måste värdet i fält A vara tillgängligt för att validera fält B även när fragment X inte har lästs in. För att uppnå detta kan du markera fält A som globalt, vilket garanterar att dess värde är tillgängligt för validering av fält B när fragment X inte har lästs in.

   Mer information om hur du gör ett fältvärde globalt finns i [Konfigurera lazy loading](../../forms/using/lazy-loading-adaptive-forms.md#p-configuring-lazy-loading-p).

* **Skriv regler för att styra visningen av fält** Formulär innehåller fält och avsnitt som inte är tillämpliga för alla användare och under alla förhållanden. Formulärförfattare och utvecklare använder synlighets- eller displayregler för att styra sin synlighet baserat på användarindata. Fältet Kontorsadress visas t.ex. inte för användare som väljer Arbetslösa i fältet Anställningsstatus i ett formulär. Mer information om hur du skriver regler finns i [Använda regelredigeraren](../../forms/using/rule-editor.md).

   Du kan använda synlighetsregler i de lagligen inlästa fragmenten så att villkorsfält bara visas när de är obligatoriska. Markera dessutom det villkorliga fältet globalt så att det refererar till det i synlighetsuttrycket för det lagerinlästa fragmentet.

## Konfigurerar lazy loading {#configuring-lazy-loading}

Utför följande steg för att aktivera lazy loading på ett adaptivt formulärfragment:

1. Öppna det adaptiva formuläret i redigeringsläget som innehåller det fragment som du vill aktivera för lazy loading.
1. Markera det adaptiva formulärfragmentet och tryck på ![cmpr](assets/cmppr.png).
1. Aktivera Läs in fragment- **[!UICONTROL lager]** i sidofältet och tryck på **Klar**.

   ![Aktivera lazy loading för det adaptiva formulärfragmentet](assets/lazy-loading-fragment.png)

   Fragmentet är nu aktiverat för lazy loading.

Du kan markera objektvärden i det lagerinlästa fragmentet som globala så att de är tillgängliga för användning i skript när det innehållande fragmentet inte läses in. Gör följande:

1. Öppna det adaptiva formulärfragmentet i redigeringsläge.
1. Tryck på fältet vars värde du vill markera som globalt och tryck sedan på ![cmpr](assets/cmppr.png).
1. Aktivera värdet **Use (Använd) under lazy loading** i sidofältet.

   ![Lazy loading field in sidebar](assets/enable-lazy-loading.png)

   Värdet är nu markerat som globalt och kommer att vara tillgängligt för användning i skript även när det innehållande fragmentet har tagits bort.

## Överväganden och bästa praxis för konfiguration av lat inläsningsarbete {#considerations-and-best-practices-for-configuring-lazy-loading}

Vissa begränsningar, rekommendationer och viktiga punkter som du bör tänka på när du arbetar med lazy loading är följande:

* Vi rekommenderar att du använder XSD-schemabaserade adaptiva formulär över XFA-baserade adaptiva formulär för att konfigurera lazy loading på stora formulär. Prestandavinster på grund av lazy loading-implementering i XFA-baserade adaptiva formulär är relativt mindre än förstärkning i XSD-baserade adaptiva formulär.
* Konfigurera inte lazy loading på fragment i en responsiv rutnätslayout. Det kan ge försämrade prestanda.
* Vi rekommenderar att du inte konfigurerar lazy loading på fragment på den första panelen som återges när det adaptiva formuläret läses in.
* Lazy loading stöds upp till två nivåer i fragmenthierarkin.
* Se till att fält som markerats som globala är unika i ett adaptivt formulär.
* Överväg att skriva synlighetsregler för fragment som ska visas eller döljas baserat på ett villkor. Du kan till exempel visa eller dölja fragmentet med information om make/maka baserat på den civilstånd som anges av en användare.
* Komponenter för bifogade filer och villkor stöds inte i lagerinlästa fragment.

### Bästa skriptpraxis för konfigurering av lazy loading {#scripting-best-practices-for-configuring-lazy-loading}

Viktiga punkter att tänka på när du utvecklar skript för lazy loading-paneler är följande:

* Se till att initiera och beräkna skript som används i fält för ett lazy loaded fragment är idealiska. Idempotenta skript är sådana som har samma effekt även efter flera exekveringar.
* Använd den globalt tillgängliga egenskapen för fält för att göra värden för fält som finns i en lat inläsningspanel tillgängliga för alla andra paneler i ett formulär.
* Vidarebefordra inte referensvärdet för ett fält i en lat panel oavsett om fältet markeras globalt över fragment eller inte.
* Använd panelåterställningsfunktionen för att återställa allt som visas på panelen med följande klickuttryck.\
   guideBridge.resolveNode(guideBridge.getFocus({&quot;focusOption&quot;): &quot;navigablePanel&quot;}).resetData()

