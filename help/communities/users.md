---
title: Hantera användare och användargrupper
description: Användare av AEM Communities kan registrera sig själva och redigera sina profiler
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
role: Admin
exl-id: 4237085a-d70d-41de-975d-153f58336daa
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '1901'
ht-degree: 0%

---

# Hantera användare och användargrupper {#managing-users-and-user-groups}

## Ökning {#overview}

I AEM Communities kan användarna själva registrera och redigera sina profiler i publiceringsmiljön. Med rätt tillstånd kan de också

* Skapa undergrupper på communitywebbplatsen (se [communitygrupper](creating-groups.md)).

* [Måttlig](moderation.md) användargenererat innehåll (UGC).

* be [privilegierad](#privileged-members-group) för att skapa inlägg för bloggar, kalendrar, QnA och forum.

Användare som är registrerade i publiceringsmiljön kallas vanligtvis för *communitymedlemmar (medlemmar)* för att skilja dem från *användare* i redigeringsmiljön.

Behörigheter beviljas genom att medlemmar tilldelas en av [medlemsgrupper (användare)](#publish-group-roles) skapas dynamiskt när communitywebbplatsen [skapad](sites-console.md) eller [ändrad](sites-console.md#modifying-site-properties) från redigeringsmiljön. När du arbetar i redigeringsmiljön visas medlemmar i publiceringsmiljön med hjälp av [tunneltjänst](#tunnel-service).

Medlemmar och medlemsgrupper som skapats i publiceringsmiljön bör inte visas i författarmiljön. Användare och användargrupper som skapats i författarmiljön är avsedda att finnas kvar i författarmiljön.

När användare som är författare och medlemmar vid publicering kommer från samma lista med användare, t.ex. synkroniserade från samma LDAP-katalog, betraktas de inte som samma användare med samma behörigheter och gruppmedlemskap i både författar- och publiceringsmiljöer. Medlemmars och användares roll(er) måste fastställas separat vid publicering och författare.

För [publicera servergrupp](topologies.md)måste registrering och ändringar som görs i en publiceringsinstans synkroniseras med andra publiceringsinstanser för att de ska ha tillgång till samma användardata. Mer information finns på [Användarsynkronisering](sync.md), som innehåller en avsnittsbeskrivning [Vad händer när..](sync.md#what-happens-when).

### Bidragsgränser {#contribution-limits}

För att skydda mot skräppost är det möjligt att begränsa medlemmarnas frekvens för publicering av innehåll. Dessutom är det möjligt att automatiskt begränsa bidragen från nyregistrerade medlemmar.

Mer information finns i [Gränser för medlemsbidrag](limits.md).

### Dynamiskt skapade användargrupper {#dynamically-created-user-groups}

När en ny användargruppwebbplats skapas skapas nya användargrupper dynamiskt med unika id:n (uid) och behörigheter som passar för olika administrativa funktioner som krävs för att hantera communitywebbplatsen i författarmiljön (se [Författargruppsroller](#author-group-roles)) eller publiceringsmiljön (se [Publicera grupproller](#publish-group-roles)).

Namnen på grupperna genereras från namnet som anges för platsen under [communitysajt](sites-console.md#step13asitetemplate). Med de unika ID:na undviker du namnkonflikter för communitywebbplatser med liknande namn och communitygrupper på samma server.

Om platsnamnet till exempel är *engagera*&quot; för en webbplats med namnet &quot; Engage&quot; skulle en av de användargrupper som skapades vara:

* Community *Engagera* Medlemmar

## Författarmiljö {#author-environment}

### Tunneltjänst {#tunnel-service}

När du använder redigeringsmiljön för att [skapa webbplatser](sites-console.md), [ändra webbplatsegenskaper](sites-console.md#modifying-site-properties) och [hantera communitymedlemmar och medlemsgrupper](members.md)måste du ha åtkomst till användare och användargrupper som är registrerade i publiceringsmiljön.

Tunneltjänsten ger denna åtkomst med replikeringsagenten på författaren.

* Mer information finns i [konfigurationsinstruktioner](deploy-communities.md#tunnel-service-on-author) på distributionssidan.

The [Konsoler för communitymedlemmar och grupper](members.md) är avsedda endast för hantering av användare (medlemmar) och användargrupper (medlemsgrupper) som är registrerade i publiceringsmiljön.

Använd [Säkerhetskonsol](../../help/sites-administering/security.md)

### Författargruppsroller {#author-group-roles}

| Om gruppmedlem... | Primär roll |
|---|---|
| administratörer | Administratörsgruppen består av systemadministratörer som har alla funktioner som en community-administratör har och möjlighet att hantera gruppen Community Administrators. |
| Community-administratörer | Gruppen Community Administrators blir automatiskt medlem i alla communitysajter och i alla communitygrupper som skapas på webbplatsen. En inledande medlem i gruppen Community Administrators är gruppen Administratörer. I redigeringsmiljön kan communityadministratörer skapa communitysajter, hantera webbplatser, hantera medlemmar (de kan förbjuda medlemmar från communityn) och moderera innehåll. |
| Community &lt;*webbplatsnamn*> Sitecontentmanager | Content Manager för communitysajt kan utföra AEM, skapa innehåll och ändra sidor för en community-sajt. |
| Ingen | En anonym besökare får inte åtkomst till författarmiljön. |

### Systemadministratörer {#system-administrators}

Medlemmar i administratörsgruppen är systemadministratörer som kan utföra den första konfigurationen av en AEM för både författarmiljön och publiceringsmiljön.

I demonstrations- och utvecklingssyfte har administratörsgruppen en medlem vars användar-ID är *admin* och lösenordet är *admin*.

I produktionsmiljöer bör standardadministratörsgruppen ändras.

Var noga med att följa [Säkerhetschecklista](../../help/sites-administering/security-checklist.md).

## Publiceringsmiljö {#publish-environment}

### Bli medlem {#becoming-a-member}

I publiceringsmiljön, beroende på [inställningar](sites-console.md#user-management) på communitywebbplatsen kan en besökare bli medlem i communityn:

* När communitywebbplatsen är privat (stängd):
   * Efter inbjudan
   * Efter en administratörs åtgärder

* När communitywebbplatsen är offentlig (öppen):
   * Efter självregistrering
   * Efter social inloggning med Facebook och Twitter

>[!NOTE]
>
>Om en besökare registrerar sig som medlem av en öppen community-webbplats blir han/hon automatiskt medlem av andra öppna communitysajter i samma publiceringsmiljö.

### Publicera grupproller {#publish-group-roles}

| Om gruppmedlem... | Primär roll |
|---|---|
| Community &lt;*webbplatsnamn*> Medlemmar | En medlem på en community är en registrerad användare. De kan logga in, ändra sin profil, gå med i en öppen community-grupp, publicera innehåll i communityn, skicka meddelanden till andra medlemmar och följa webbplatsaktiviteter. |
| Community &lt;*webbplatsnamn*> Moderatorer | En moderator för communitywebbplatser är en betrodd community-medlem som kan moderera UGC-innehåll antingen i grupp med modereringskonsolen eller i sitt sammanhang på den sida där innehållet publiceras. |
| Community &lt;*webbplatsnamn*> &lt;*gruppnamn*> Medlemmar | En community-gruppmedlem är en community-medlem som antingen har gått med i en öppen community-grupp eller har bjudits in till en stängd community-grupp. De har funktionerna som en medlem i den communitygruppen på webbplatsen. |
| Community &lt;*webbplatsnamn*> Gruppadministratörer | En administratör för en community-webbplatsgrupp är en betrodd community-medlem som har tilldelats behörigheten att skapa och hantera undergrupper (grupper) på en community-webbplats. Möjligheten att moderera i sitt sammanhang ingår. |
| *Säkerhetsgrupp för behöriga medlemmar* | En användargrupp som skapats och underhålls manuellt för att begränsa möjligheten att skapa innehåll. Se [Grupp med behöriga medlemmar](#privileged-members-group). |
| Ingen | En anonym besökare som upptäcker webbplatsen kan visa och söka på communitysajter som tillåter anonym åtkomst. För att kunna delta och publicera innehåll måste användaren själv registrera sig (om det är tillåtet) och bli medlem i communityn. |

### Tilldela medlemmar till publiceringsgruppsroller {#assigning-members-to-publish-group-roles}

När [skapa en communitywebbplats](sites-console.md) i redigeringsmiljön, eller när [ändra platsegenskaper,](sites-console.md#modifying-site-properties) Medlemmar kan tilldelas olika roller som utförs i publiceringsmiljön, till exempel moderatorer, gruppadministratörer, resurskontakter eller behöriga medlemmar.

[Aktivera tunneltjänsten](sync.md#accessingpublishusersfromauthor) resulterar i att uppdragsalternativ visas från medlemmar vid publicering i stället för användare vid författare.

De valda medlemmarna tilldelas automatiskt till [lämplig grupp](#publish-group-roles) och deras medlemskap kommer att ingå när communitysajten publiceras (på nytt).

### Grupp med behöriga medlemmar {#privileged-members-group}

Syftet med en säkerhetsgrupp för behöriga medlemmar är att begränsa skapandet av innehåll för vissa communityfunktioner till en privilegierad delmängd av medlemmarna på en community-webbplats.

Gruppen med behöriga medlemmar är en medlemsgrupp som skapas och hanteras med [Konsol för webbgrupper](members.md).

När en privilegierad medlemsgrupp har skapats, och med [tunneltjänsten är aktiverad](sync.md#accessingpublishusersfromauthor)kan en befintlig community-webbplats vara [ändrad](sites-console.md#modify-structure) om du vill redigera konfigurationen av dess communityfunktioner till Tillåt behöriga medlemmar och lägga till den skapade gruppen.

De communityfunktioner som tillåter specificering av en eller flera privilegierade medlemsgrupper är:

* [Bloggfunktion](functions.md#blog-function) - Begränsa skapandet av nya artiklar.
* [Kalenderfunktion](functions.md#calendar-function) - Begränsa skapandet av nya händelser.
* [Forumfunktion](functions.md#forum-function) - Begränsa skapandet av nya ämnen.
* [QnA-funktion](functions.md#qna-function) - Begränsa skapandet av nya frågor.

När en communityfunktion inte är skyddad (ingen privilegierad medlemsgrupp har tilldelats), tillåts alla community-webbplatsmedlemmar att skapa funktionsinnehåll (artiklar, händelser, ämnen, frågor).

>[!NOTE]
>
>Om du lägger till en användare i en privilegierad medlemsgrupp för en communitywebbplats får användaren endast behörighet om han eller hon också är medlem på samma communitywebbplats.

## Skapa communitymedlemmar {#creating-community-members}

### Lagringsplats {#repository-location}

För att vissa funktioner ska fungera på rätt sätt måste du skapa användare och användargrupper med lämplig behörighet.

När medlemmar skapas i `/home/users/community`ärver de rätt åtkomstkontrollistor som ger läsbehörighet till medlemmarnas profiler.

På samma sätt bör anpassade användargrupper (som behöriga medlemsgrupper) skapas i `/home/groups/community`.

Använda [Konsoler för communitymedlemmar och grupper](members.md) skapar användare och grupper i de här sökvägarna.

Om du vill ange en anpassad sökväg måste du använda det klassiska säkerhetsgränssnittet, som du kommer åt på [https://&lt;server>:&lt;port>/useradmin](http://localhost:4503/useradmin).

Om du vill ge läsbehörighet för anpassade medlemssökvägar anger du åtkomstkontrollistor på alla publiceringsinstanser som liknar `/home/users/community`:

```xml
<allow
  jcr:primaryType="rep:GrantACE"
  rep:principalName="everyone"
  rep:privileges="{Name}[jcr:read]" >
  <rep:restrictions
    jcr:primaryType="rep:Restrictions"
    rep:glob="*/profile*" />
</allow>
```

Om du vill ge rätt behörighet för anpassade medlemsgruppsökvägar, till exempel /home/groups/mycompany, anger du åtkomstkontrollistor som liknar `/home/groups/community`:

```xml
<allow
  jcr:primaryType="rep:GrantACE"
  rep:principalName="community-administrators"
  rep:privileges="{Name}[jcr:read]"  />
```

### Konsoler {#consoles}

Det finns fyra separata konsoler som endast är tillgängliga i författarmiljön:

| konsol | verktyg, säkerhet, användare | Verktyg, Säkerhet, Grupper | Communities, Members | Communities, Groups |
|----------|-----------------------|------------------------|------------------------------------------------------------|------------------------------------------------------------|
| hanterar | användare i författare | användargrupper för författare | medlemmar vid publicering | medlemsgrupper vid publicering |
| kräver | administratörsbehörighet | administratörsbehörighet | administratörsbehörighet, tunneltjänst, användarsynkronisering för publiceringsgrupp | administratörsbehörighet, tunneltjänst, användarsynkronisering för publiceringsgrupp |

### Rollen Community-administratörer {#community-administrators-role}

Som anges i [Författargruppsroller](#author-group-roles) så kan medlemmar i gruppen Community Administrators skapa communitysajter, hantera webbplatser, hantera medlemmar (de kan förbjuda medlemmar från communityn) och moderera innehåll.

Följ samma steg som att skapa och tilldela en användare rollen som aktiveringshanterare, men lägg till c `ommunity-administrators` på fliken Grupper för användaren.

### LDAP-integrering {#ldap-integration}

AEM stöder användningen av LDAP för autentisering av användare och skapande av användarkonton. Detta beskrivs i [Konfigurera LDAP med AEM 6](../../help/sites-administering/ldap-config.md).

Nedan följer några konfigurationsdetaljer som är specifika för communitymedlemmar och medlemsgrupper.

1. Konfigurera LDAP för varje AEM.
2. [LDAP-identitetsleverantören](../../help/sites-administering/ldap-config.md#configuring-the-ldap-identity-provider)

   * Inga särskilda instruktioner

3. [Synkroniseringshanteraren](../../help/sites-administering/ldap-config.md#configuring-the-synchronization-handler)

   * Ange följande egenskaper:

      * **[!UICONTROL User auto membership]**: `community-<site name>-<uid>-members`
      * **[!UICONTROL User Path Prefix]**: `/community`
      * **[!UICONTROL Group Path Prefix]**: `/community`

4. [Modulen Extern inloggning](../../help/sites-administering/ldap-config.md#the-external-login-module)

   * inga särskilda instruktioner

Detta resulterar i att användare automatiskt tilldelas till medlemsgruppen för communitywebbplatsen och att databasplatsen `/home/users/community` och `/home/groups/community`så att de ärver de behörigheter som krävs för att se varandras profil.

* The `User auto membership` värdet ska vara `rep:authorizableId` -egenskap, inte `givenName` (visningsnamn) från profilen.

## Synkronisera användare bland AEM instanser {#synchronizing-users-among-aem-instances}

När en [publicera servergrupp](topologies.md)kontrollerar du att användarna har samma sökväg för varje publiceringsinstans genom att först importera användarna till en instans och [aktivera användarsynkronisering](sync.md) Sling distribuerar användarna till de andra publiceringsinstanserna.

Om du importerar användargrupper måste du importera till en instans för att se till att användargrupperna har samma sökväg för varje publiceringsinstans. [skapa ett paket](../../help/sites-administering/package-manager.md#creating-a-new-package) för export och installera paketet på alla andra publiceringsinstanser.

Synkronisering av användargrupper via användarsynkronisering kommer att ingå i en framtida release, för närvarande endast *medlemskap* för en användargrupp synkroniseras när användarsynkroniseringen körs.

## Om communitygrupper {#about-community-groups}

När man diskuterar grupper finns det två skilda ämnen:

* **[Community-grupper](overview.md#communitygroups)**

  Community-grupper är de undergrupper som kan skapas i publiceringsmiljön för en communitywebbplats som stöder skapande av communitygrupper. Om du skapar en community-grupp läggs fler sidor till på webbplatsen och hanteras på samma sätt som den överordnade communitywebbplatsen. Mer information finns på [Grundläggande om communitygrupper](essentials-groups.md) för utvecklare och [Community Group](creating-groups.md) för författare.

* **[Medlemsgrupper](../../help/sites-administering/security.md)**

  Medlemsgrupper är de grupper som medlemmar kan tillhöra och hanteras via gruppkonsolen. En stor del av diskussionen på den här sidan har hänskjutits till medlemsgrupper. Medlemsgrupper skapas automatiskt för en community-webbplats, som har prefix med *`Community`*, kan betecknas som en gemenskapsgrupp, och därför måste sammanhanget för diskussionen beaktas.
