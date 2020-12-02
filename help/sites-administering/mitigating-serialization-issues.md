---
title: Åtgärda serialiseringsproblem i AEM
seo-title: Åtgärda serialiseringsproblem i AEM
description: Lär dig hur du minskar serialiseringsproblem i AEM.
seo-description: Lär dig hur du minskar serialiseringsproblem i AEM.
uuid: c3989dc6-c728-40fd-bc47-f8427ed71a49
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: f3781d9a-421a-446e-8b49-40744b9ef58e
translation-type: tm+mt
source-git-commit: 3cbbad3ce9d93a353f48fc3206df989a8bf1991a
workflow-type: tm+mt
source-wordcount: '969'
ht-degree: 0%

---


# Åtgärda serialiseringsproblem i AEM{#mitigating-serialization-issues-in-aem}

## Översikt {#overview}

AEM på Adobe har samarbetat nära med öppen källkodsprojektet [NotSoSerial](https://github.com/kantega/notsoserial) för att bidra till att minska säkerhetsluckorna som beskrivs i **CVE-2015-7501**. NotSoSerial licensieras under [Apache 2-licensen](https://www.apache.org/licenses/LICENSE-2.0) och innehåller ASM-kod licensierad under sin egen [BSD-liknande licens](https://asm.ow2.org/license.html).

Agentbehållaren som medföljer detta paket är distributionen av NotSoSerial efter Adobe.

NotSoSerial är en Java-nivålösning på ett Java-nivåproblem och är inte AEM specifik. En preflight-kontroll läggs till i ett försök att avserialisera ett objekt. Den här kontrollen testar ett klassnamn mot en brandvägg som tillåtelselista och/eller blockeringslista. På grund av det begränsade antalet klasser i standardversionen av blockeringslista är det osannolikt att detta påverkar dina system eller din kod.

Som standard utför agenten en blockeringslista-kontroll mot aktuella kända sårbara klasser. Blockeringslista är avsett att skydda dig från den aktuella listan över explosioner som använder denna typ av sårbarhet.

Du kan konfigurera blockeringslista och tillåtelselista genom att följa instruktionerna i [Konfigurera agenten](/help/sites-administering/mitigating-serialization-issues.md#configuring-the-agent) i den här artikeln.

Medlet är avsett att bidra till att minska de senaste kända sårbara klasserna. Om ditt projekt avserialiserar otillförlitliga data kan det fortfarande vara känsligt för denial of service-attacker, slut på minnesattacker och okända framtida avserialiseringsattacker.

Adobe har officiellt stöd för Java 6, 7 och 8, men vi är överens om att NotSoSerial även har stöd för Java 5.

## Installera agenten {#installing-the-agent}

>[!NOTE]
>
>Om du tidigare har installerat serialiseringssnabbkorrigeringen för AEM 6.1 tar du bort agentens startkommandon från din java-körningsrad.

1. Installera **com.adobe.cq.cq-serialization-testpaketet**.

1. Gå till webbkonsolen Bundle på `https://server:port/system/console/bundles`
1. Leta efter serialiseringspaketet och starta det. Detta bör automatiskt läsa in NotSoSerial-agenten.

## Installera agenten på programservrar {#installing-the-agent-on-application-servers}

NotSoSerial-agenten ingår inte i standarddistributionen av AEM för programservrar. Du kan dock extrahera den från AEM jar-distributionen och använda den med programserverkonfigurationen:

1. Ladda först ned AEM snabbstartfil och extrahera den:

   ```shell
   java -jar aem-quickstart-6.2.0.jar -unpack
   ```

1. Gå till platsen för den uppzippade AEM snabbstarten och kopiera mappen `crx-quickstart/opt/notsoserial/` till mappen `crx-quickstart` i AEM programserverinstallation.

1. Ändra ägarskapet för `/opt` till användaren som kör servern:

   ```shell
   chown -R opt <user running the server>
   ```

1. Konfigurera och kontrollera att agenten har aktiverats korrekt enligt följande avsnitt i den här artikeln.

## Konfigurerar agenten {#configuring-the-agent}

Standardkonfigurationen räcker för de flesta installationer. Detta omfattar en blockeringslista av kända sårbara klasser för fjärrexekvering och en tillåtelselista av paket där avserialisering av tillförlitliga data bör vara relativt säker.

Brandväggskonfigurationen är dynamisk och kan ändras när som helst genom att:

1. Gå till webbkonsolen på `https://server:port/system/console/configMgr`
1. Söker efter och klickar på **Brandväggskonfiguration för deserialisering.**

   >[!NOTE]
   >
   >Du kan även nå konfigurationssidan direkt genom att gå till URL:en på:
   >
   >* `https://server:port/system/console/configMgr/com.adobe.cq.deserfw.impl.DeserializationFirewallImpl`


Den här konfigurationen innehåller loggning av tillåtelselista, blockeringslista och deserialisering.

**Tillåt lista**

I avsnittet Tillåt är dessa klasser eller paketprefix som tillåts för deserialisering. Observera att om du avserialiserar egna klasser måste du lägga till antingen klasserna eller paketen i tillåtelselista.

**Blocklista**

I avsnittet med blocklistor är klasser som aldrig tillåts för deserialisering. Den första uppsättningen av dessa klasser är begränsad till klasser som har befunnits sårbara för attacker på fjärrbasis. Blockeringslista används före alla tillåtna poster i listan.

**Diagnostikloggning**

I avsnittet för diagnostikloggning kan du välja flera alternativ för loggning när deserialisering sker. Dessa är endast inloggade första gången och loggas inte igen vid efterföljande användningar.

Standardvärdet **class-name-only** informerar dig om de klasser som avserialiseras.

Du kan också ange alternativet **full-stack** som loggar en java-stack om det första deserialiseringsförsöket för att informera dig om var deserialiseringen sker. Detta kan vara användbart för att hitta och ta bort deserialisering från din användning.

## Verifierar agentens aktivering {#verifying-the-agent-s-activation}

Du kan verifiera deserialiseringsagentens konfiguration genom att gå till URL:en på:

* `https://server:port/system/console/healthcheck?tags=deserialization`

När du har åtkomst till URL:en visas en lista med hälsokontroller för agenten. Du kan avgöra om agenten har aktiverats på rätt sätt genom att verifiera att hälsokontrollerna har godkänts. Om de inte fungerar kan du behöva läsa in agenten manuellt.

Mer information om felsökning av agentproblem finns i [Hantera fel med dynamisk agentinläsning](#handling-errors-with-dynamic-agent-loading) nedan.

>[!NOTE]
>
>Om du lägger till `org.apache.commons.collections.functors` i tillåtelselista misslyckas alltid hälsokontrollen.

## Hantera fel med inläsning av dynamisk agent {#handling-errors-with-dynamic-agent-loading}

Om fel visas i loggen, eller om verifieringsstegen upptäcker ett problem med att läsa in agenten, kan du behöva läsa in agenten manuellt. Detta rekommenderas också om du använder en JRE (Java Runtime Environment) i stället för en JDK (Java Development Toolkit), eftersom verktygen för dynamisk inläsning inte är tillgängliga.

Följ instruktionerna nedan för att läsa in agenten manuellt:

1. Ändra startparametrarna för JVM för CQ-behållaren och lägg till följande alternativ:

   ```shell
   -javaagent:<aem-installation-folder>/crx-quickstart/opt/notsoserial/notsoserial.jar
   ```

   >[!NOTE]
   >
   >Detta kräver att du även använder alternativet -nofork CQ/AEM tillsammans med lämpliga JVM-minnesinställningar, eftersom agenten inte aktiveras på en förankrad JVM.

   >[!NOTE]
   >
   >Adobe-distributionen av NotSoSerial Agent jar finns i mappen `crx-quickstart/opt/notsoserial/` i din AEM.

1. Stoppa och starta om JVM,

1. Verifiera agentens aktivering igen genom att följa stegen ovan i [Verifiera agentens aktivering](/help/sites-administering/mitigating-serialization-issues.md#verifying-the-agent-s-activation).

## Andra överväganden {#other-considerations}

Om du kör på en IBM JVM läser du dokumentationen om stöd för Java Attach API på [den här platsen](https://www.ibm.com/support/knowledgecenter/SSSTCZ_2.0.0/com.ibm.rt.doc.20/user/attachapi.html).
