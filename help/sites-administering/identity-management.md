---
title: Identity Management
description: Läs om hur identitetshantering fungerar i AEM.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
docset: aem65
exl-id: acb5b235-523e-4c01-9bd2-0cc2049f88e2
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '1248'
ht-degree: 0%

---


# Identity Management{#identity-management}

Enskilda besökare på din webbplats kan bara identifieras när du ger dem möjlighet att logga in. Det finns olika skäl till att du kan behöva ange en inloggningsfunktion:

* [AEM Communities](/help/communities/overview.md)Besökare på webbplatsen måste logga in för att kunna publicera innehåll i communityn.
* [Stängda användargrupper](/help/sites-administering/cug.md)

  Du kan behöva begränsa åtkomsten till din webbplats (eller delar av den) till vissa besökare.

* [Personalisering](/help/sites-administering/personalization.md) Gör det möjligt för besökare att konfigurera vissa aspekter av hur de kommer åt din webbplats.

Funktionen Logga in (och ut) tillhandahålls av en [konto med **Profil**](#profiles-and-user-accounts), som innehåller ytterligare information om den registrerade besökaren (användaren). De faktiska processerna för registrering och godkännande kan skilja sig åt:

* Självregistrering från webbplatsen

  A [Community-webbplats](/help/communities/sites-console.md) kan konfigureras så att besökare kan registrera sig själva eller logga in med sina Facebook- eller Twitter-konton.

* Registreringsförfrågan från webbplatsen

  För en sluten användargrupp kan du tillåta besökare att begära registrering, men tvinga fram auktorisering via ett arbetsflöde.

* Registrera varje konto från författarmiljön

  Om du har ett litet antal profiler, som ändå behöver behörighet, kan du välja att registrera dem direkt.

För att besökare ska kunna registrera sig kan en serie komponenter och formulär användas för att samla in den nödvändiga identifieringsinformationen, och sedan den extra (ofta valfria) profilinformationen. När de har registrerat sig bör de också kunna kontrollera och uppdatera de uppgifter de har lämnat.

Ytterligare funktioner kan konfigureras eller utvecklas:

* Konfigurera eventuell omvänd replikering som krävs.
* Tillåt att en användare tar bort sin profil genom att utveckla ett formulär tillsammans med ett arbetsflöde.

>[!NOTE]
>
>Den information som anges i profilen kan även användas för att förse användaren med riktat innehåll via [Segment](/help/sites-administering/campaign-segmentation.md) och [Kampanjer](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md).

## Registrera Forms {#registration-forms}

A [formulär](/help/sites-authoring/default-components.md#form-component) kan användas för att samla in registreringsinformation och sedan generera det nya kontot och den nya profilen.

Användare kan till exempel begära en ny profil via sidan Geometrixx
`http://localhost:4502/content/geometrixx-outdoors/en/user/register.html`

![Exempelregistreringsformulär](assets/registerform.png)

När du skickar begäran öppnas profilsidan där användaren kan ange personlig information.

![Exempel på profilsida](assets/profilepage.png)

Det nya kontot visas även i [Användarkonsol](/help/sites-administering/security.md).

## Inloggning {#login}

Inloggningskomponenten kan användas för att samla in inloggningsinformationen och sedan aktivera inloggningsprocessen.

Detta förser besökaren med standardfälten i **Användarnamn** och **Lösenord**, med **Inloggning** för att aktivera inloggningsprocessen när inloggningsuppgifterna anges.

Användare kan till exempel antingen logga in eller skapa ett konto med **Logga in** i verktygsfältet i Geometrixx där sidan används:

`http://localhost:4502/content/geometrixx-outdoors/en/user/sign-in.html`

![Exempel på inloggningssida](assets/login.png)

## Loggar ut {#logging-out}

Eftersom det finns en inloggningsmekanism krävs också en utloggningsmekanism. Det här är tillgängligt som **Logga ut** i Geometrixx.

## Visa och uppdatera en profil {#viewing-and-updating-a-profile}

Beroende på ditt registreringsformulär kan besökaren ha registrerat information i sin profil. De bör kunna visa och/eller uppdatera detta i ett senare skede. Detta kan göras med ett liknande formulär, t.ex. i Geometrixx:

```
http://localhost:4502/content/geometrixx-outdoors/en/user/profile.html
```

Om du vill se information om din profil klickar du **Min profil** i det övre högra hörnet på en sida, till exempel med `admin` konto:
`http://localhost:4502/home/users/a/admin/profile.form.html/content/geometrixx-outdoors/en/user/profile.html.`

Du kan visa en annan profil med [klientkontext](/help/sites-administering/client-context.md) (i redigeringsmiljön och med tillräcklig behörighet):

1. Öppna en Geometrixx, till exempel:

   `http://localhost:4502/cf#/content/geometrixx/en.html`

1. Klicka **Min profil** längst upp till höger. Du ser profilen för ditt aktuella konto, till exempel administratören.
1. Tryck **control-alt-C** för att öppna klientkontexten.
1. Klicka på knappen längst upp till vänster i klientkontexten **Läs in en profil** -knappen.

   ![Läsa in en profilikon](do-not-localize/loadprofile.png)

1. Välj en annan profil i listrutan i dialogrutan, till exempel **Alison Parker**.
1. Klicka **OK**.
1. Klicka igen **Min profil**. Formuläret uppdateras med Alisons information.

   ![Exempelprofil för Alison](assets/profilealison.png)

1. Nu kan du använda **Redigera profil** eller **Ändra lösenord** för att uppdatera informationen.

## Lägga till fält i profildefinitionen {#adding-fields-to-the-profile-definition}

Du kan lägga till fält i profildefinitionen. Så här lägger du till ett&quot;Favoritfärg&quot;-fält i Geometrixx:

1. Gå till Geometrixx Outdoors Site > English > User > My Profile i webbplatskonsolen.
1. Dubbelklicka på **Min profil** för att öppna den för redigering.
1. I **Komponenter** flik för sidospark expandera **Formulär** -avsnitt.
1. Dra en **Listruta** från sidosparken till formuläret, precis nedanför **Om mig** fält.
1. Dubbelklicka på **Listruta** för att öppna dialogrutan för konfiguration och ange:

   * **Elementnamn** - `favoriteColor`
   * **Titel** - `Favorite Color`
   * **Objekt** - Lägga till flera färger som objekt

   Klicka **OK** att spara.

1. Stäng sidan och gå tillbaka till **Webbplatser** och aktivera sidan Min profil.

   Nästa gång du visar en profil kan du välja en favoritfärg:

   ![Alison Parker&#39;s favorite color sample field](assets/aparkerfavcolour.png)

   Fältet sparas under **profil** i det aktuella användarkontot:

   ![Alison Parkers data i CRXDE](assets/aparkercrxdelite.png)

## Profiltillstånd {#profile-states}

Det finns flera användningsfall som kräver att du vet om en användare (eller snarare deras profil) finns i en *specifikt läge* eller inte.

Detta innebär att definiera en lämplig egenskap i användarprofilen på följande sätt:

* är synlig och tillgänglig för användaren
* definierar två lägen för varje egenskap
* möjliggör växling mellan de två definierade lägena

Detta görs med:

* [Statliga leverantörer](#state-providers)

  Om du vill hantera de två lägena för en viss egenskap och övergångarna mellan dessa.

* [Arbetsflöden](#workflows)

  Om du vill hantera åtgärder relaterade till lägena.

Flera lägen kan definieras. I Geometrixx ingår till exempel:

* prenumerera (eller avbryta prenumerationen) på meddelanden i nyhetsbrev eller kommentarstrådar
* lägga till och ta bort en anslutning till en vän

### Statliga leverantörer {#state-providers}

En lägesprovider hanterar den aktuella statusen för den aktuella egenskapen tillsammans med övergångarna mellan de två möjliga lägena.

Statliga leverantörer implementeras som komponenter, så de kan anpassas för ditt projekt. Bland Geometrixx finns följande:

* Un-/prenumerationsforum
* Lägg till/ta bort vän

### Arbetsflöden {#workflows}

Statliga leverantörer hanterar en profilegenskap och dess lägen.

Det behövs ett arbetsflöde för att implementera åtgärder som är relaterade till lägena. När du prenumererar på meddelanden hanterar arbetsflödet till exempel den faktiska prenumerationsåtgärden. När du avbryter prenumerationen på meddelanden hanterar arbetsflödet borttagningen av användaren från prenumerationslistan.

## Profiler och användarkonton {#profiles-and-user-accounts}

Profilerna lagras i innehållsdatabasen som en del av[användarkonto](/help/sites-administering/user-group-ac-admin.md).

Profilen finns under `/home/users/geometrixx`:

![Profiler enligt CRXDE](assets/chlimage_1-138.png)

I en standardinstallation (författare eller publicering) har alla läsåtkomst till all profilinformation för alla användare. alla är *Inbyggd grupp som automatiskt innehåller alla befintliga användare och grupper. Det går inte att redigera medlemslistan*&quot;.

Dessa åtkomsträttigheter definieras av följande jokertecken-ACL:

/home alla tillåter jcr:read rep:glob = &#42;/profile&#42;

Det gör att:

* forum, kommentarer eller blogginlägg för att visa information (t.ex. ikon eller fullständigt namn) från lämplig profil
* länkar till profilsidor för geometrixx

Om sådan åtkomst inte passar för installationen kan du ändra dessa standardinställningar.

Detta kan du göra med **[Åtkomstkontroll](/help/sites-administering/user-group-ac-admin.md#access-right-management)** tab:

![Hantera åtkomstkontrollistor i CRXDE](assets/aclmanager.png)

## Profilkomponenter {#profile-components}

Det finns även ett antal profilkomponenter som du kan använda för att definiera profilkraven för din plats.

### Kontrollerat lösenordsfält {#checked-password-field}

Den här komponenten ger dig två fält för:

* inmatning av ett lösenord
* en kontroll som bekräftar att lösenordet har angetts korrekt.

Med standardinställningarna visas komponenten så här:

![Dialogrutan Kontrollera lösenord](assets/dc_profiles_checkedpassword.png)

### Profil Avatar Photo {#profile-avatar-photo}

Den här komponenten ger användaren en funktion för att välja och överföra en Avatar Photo-fil.

![Avatarväljare](assets/dc_profiles_avatarphoto.png)

### Detaljerat profilnamn {#profile-detailed-name}

Med den här komponenten kan användaren ange ett detaljerat namn.

![Dialogrutan Detaljerat namn](assets/dc_profiles_detailedname.png)

### Profilkön {#profile-gender}

Med den här komponenten kan användaren ange sitt kön.

![Genusväljare](assets/dc_profiles_gender.png)
