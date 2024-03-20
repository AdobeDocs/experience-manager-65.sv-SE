---
title: Krav för integrering med Adobe Target
description: Läs om förutsättningarna för integrering med Adobe Target.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
docset: aem65
exl-id: 30813c44-51ac-4e6e-8ee6-4e8baacb1ff9
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '528'
ht-degree: 0%

---

# Krav för integrering med Adobe Target{#prerequisites-for-integrating-with-adobe-target}

Som en del av [integrering av AEM och Adobe Target](/help/sites-administering/target.md)måste du registrera dig hos Adobe Target, konfigurera replikeringsagenten och säkra aktivitetsinställningar på publiceringsnoden.

## Registrering hos Adobe Target {#registering-with-adobe-target}

För att kunna integrera AEM med Adobe Target måste du ha ett giltigt Adobe Target-konto. Det här kontot måste ha **godkännare** minst nivåbehörigheter. När du registrerar dig hos Adobe Target får du en klientkod. Du behöver klientkoden och inloggningsnamnet och lösenordet för Adobe Target för att kunna ansluta AEM till Adobe Target.

Klientkoden identifierar Adobe Target-kundkontot när Adobe Target-servern anropas.

>[!NOTE]
>
>Ditt konto måste också aktiveras av Target-teamet för att integreringen ska kunna användas.
>
>Om så inte är fallet, kontakta [Adobe kundtjänst](https://experienceleague.adobe.com/docs/target/using/cmp-resources-and-contact-information.html).

## Aktivera målreplikeringsagenten {#enabling-the-target-replication-agent}

Test och Target [replikeringsagent](/help/sites-deploying/replication.md) måste vara aktiverat på författarinstansen. Observera att den här replikeringsagenten inte är aktiverad som standard om du använde [nosamplingContent](/help/sites-deploying/configure-runmodes.md#using-samplecontent-and-nosamplecontent) körningsläge för AEM. Mer information om hur du skyddar din produktionsmiljö finns i [Säkerhetschecklista](/help/sites-administering/security-checklist.md).

1. På AEM startsida klickar du på **verktyg** > **Distribution** > **Replikering**.
1. Klicka **Agenter på författare**.
1. Klicka på **Test och Target (test och target)** replikeringsagent och klicka sedan på **Redigera**.
1. Välj alternativet Aktiverad och klicka sedan på **OK**.

   >[!NOTE]
   >
   >När du konfigurerar replikeringsagenten Test och Target finns det i **Transport** -tabben, anges URI som standard till **tnt:///**. Ersätt inte denna URI med **https://admin.testandtarget.omniture.com**.
   >
   >Om du försöker testa anslutningen med **tnt:///**, genereras ett fel. Detta beteende förväntas eftersom denna URI endast är avsedd för internt bruk. Använd inte med **Testanslutning**.

## Skydda noden Aktivitetsinställningar {#securing-the-activity-settings-node}

Skydda noden för aktivitetsinställningar **cq:ActivitySettings** på publiceringsinstansen så att den inte är tillgänglig för vanliga användare. Noden för aktivitetsinställningar ska bara vara tillgänglig för tjänsten som hanterar aktivitetssynkroniseringen till Adobe Target.

The **cq:ActivitySettings** noden är tillgänglig i CRXDE lite under `/content/campaigns/*nameofbrand*`* *under aktiviteterna jcr:innehållsnod;* *till exempel `/content/campaign/we-retail/master/myactivity/jcr:content/cq:ActivitySettings`. Den här noden skapas bara efter att du har angett en komponent som mål.

The **cq:ActivitySettings** nod under aktivitetens jcr:innehåll skyddas av följande åtkomstkontrollistor:

* Neka alla för alla
* Tillåt jcr:read,rep:write för&quot;target-activity-authors&quot; (författaren är medlem i den här gruppen utanför rutan)
* Tillåt jcr:read,rep:write för &quot;target service&quot;

Dessa inställningar ser till att normala användare inte har tillgång till nodegenskaperna. Använd samma åtkomstkontrollista vid författare och publicering. Se [Användaradministration och -säkerhet](/help/sites-administering/security.md) för mer information.

## Konfigurera AEM Link Externalizer {#configuring-the-aem-link-externalizer}

När du redigerar en aktivitet i Adobe Target pekar URL:en på **localhost** såvida du inte ändrar URL:en på AEM författarnod. Du kan konfigurera AEM Link Externalizer om du vill att det exporterade innehållet ska peka mot ett visst *publicera* domän.

>[!NOTE]
>
>Se även [Lägg till molnkonfigurationen](/help/sites-administering/experience-fragments-target.md#add-the-cloud-configuration).

Så här konfigurerar du AEM externalizer:

>[!NOTE]
>
>Mer information finns i [Extern URL](/help/sites-developing/externalizer.md).

1. Navigera till OSGi-webbkonsolen på **https://&lt;server>:&lt;port>/system/console/configMgr.**
1. Sök **Day CQ Link Externalizer** och ange författarnodens domän.

   ![Day CQ Link Externalizer](assets/aem-externalizer-01.png)
