---
title: Arbeta med ett formulär
seo-title: Arbeta med ett formulär
description: Visa och uppdatera formuläret som är kopplat till en uppgift eller startpunkt i appen AEM Forms
seo-description: Visa och uppdatera formuläret som är kopplat till en uppgift eller startpunkt i appen AEM Forms
uuid: 7481ca5c-a2c0-4697-9008-1e51bce2012e
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 8a5e038e-b39a-41de-88a0-47642e5bd5bf
translation-type: tm+mt
source-git-commit: d9975c0dcc02ae71ac64aadb6b4f82f7c993f32c

---


# Arbeta med ett formulär {#working-with-a-form}

Om ett formulär har aktiverats för synkronisering i formulärappen hämtas formuläret och du kan arbeta med det direkt.

Formulären hämtas till din app och är tillgängliga offline. Du driver t.ex. ett bankföretag och en kund fyller i en ansökan på er webbplats. Programmet är ett anpassat formulär som tar emot information från dina kunder och lagrar den för granskning. Administratören granskar formuläret och skapar ett verifieringsformulär i AEM-författarinstansen. Administratören aktiverar synkronisering av formuläret med appen AEM Forms. Om verifieringsformuläret är tillgängligt i appen AEM Forms kan fältagenten använda en mobil enhet för att verifiera kundens information. Den mobila enheten synkroniseras med servern och verifieringsformuläret läses in i appen. Din fältrepresentant kan besöka kunden, verifiera informationen, spara data som utkast eller skicka bekräftelseformuläret. Formuläret synkroniseras med servern varje gång appen är online.

Så här synkroniserar du formuläret i appen AEM Forms:

1. Markera ett formulär i författarinstansen och klicka på **Visa egenskaper**.
1. Klicka på **Avancerat på egenskapssidan.**
1. Aktivera alternativet under Avancerat: **Synkronisera med AEM Forms App** och tryck på **Save**.

Om du vill synkronisera flera formulär i författarinstansen markerar du flera formulär i formulärhanteraren och trycker på **Synkronisera med AEM Forms App**. När formuläret publiceras kan AEM Forms-appen ansluta till publiceringsservern och hämta formulären.

>[!NOTE]
>
>Formulär som stöds:
>
>* Anpassningsbara formulär (utan lazy loading)
>* Mobila formulär
>
>
Bifogade filer på formulärnivå stöds inte i de adaptiva formulär som har hämtats i appen AEM Forms som har synkroniserats med AEM Forms OSGi-servern. Användare kan bifoga filer i ett fält om författaren har aktiverat bilagor på fältnivå när formuläret redigeras.

**Öppna och uppdatera ett formulär**

1. Om du vill öppna ett formulär trycker du på formuläret på hemskärmen.
1. Du kan uppdatera fälten i formuläret, lägga till bilagor, spara som utkast och skicka det.

[Kontakta supporten](https://www.adobe.com/account/sign-in.supportportal.html)
