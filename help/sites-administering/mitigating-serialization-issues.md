---
title: Åtgärda serialiseringsproblem i AEM
seo-title: Åtgärda serialiseringsproblem i AEM
description: Lär dig hur du undviker serialiseringsproblem i AEM.
seo-description: Lär dig hur du undviker serialiseringsproblem i AEM.
uuid: c3989dc6-c728-40fd-bc47-f8427ed71a49
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: f3781d9a-421a-446e-8b49-40744b9ef58e
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Åtgärda serialiseringsproblem i AEM{#mitigating-serialization-issues-in-aem}

## Översikt {#overview}

AEM-teamet på Adobe har samarbetat nära med öppen källkodsprojektet [NotSoSerial](https://github.com/kantega/notsoserial) för att hjälpa till att minska säkerhetsluckorna som beskrivs i **CVE-2015-7501**. NotSoSerial licensieras under [Apache 2-licensen](https://www.apache.org/licenses/LICENSE-2.0) och innehåller ASM-kod som licensieras under dess egen [BSD-liknande licens](https://asm.ow2.org/license.html).

Agentbehållaren som ingår i paketet är Adobes ändrade distribution av NotSoSerial.

NotSoSerial är en Java-nivålösning på ett Java-nivåproblem och är inte AEM-specifikt. En preflight-kontroll läggs till i ett försök att avserialisera ett objekt. Med den här kontrollen testas ett klassnamn mot en vitlista och/eller svartlista i brandväggsstil. På grund av det begränsade antalet klasser i standardsvartlistan är det osannolikt att detta påverkar dina system eller din kod.

Som standard utför agenten en svartlistningskontroll mot aktuella kända sårbara klasser. Denna svarta lista är avsedd att skydda dig från den aktuella listan över explosioner som använder denna typ av sårbarhet.

Svartlistan och vitlistan kan konfigureras genom att följa instruktionerna i avsnittet [Konfigurera agenten](/help/sites-administering/mitigating-serialization-issues.md#configuring-the-agent) i den här artikeln.

Medlet är avsett att bidra till att minska de senaste kända sårbara klasserna. Om ditt projekt avserialiserar otillförlitliga data kan det fortfarande vara känsligt för denial of service-attacker, slut på minnesattacker och okända framtida avserialiseringsattacker.

Adobe har officiellt stöd för Java 6, 7 och 8, men vi har förstått att NotSoSerial även har stöd för Java 5.

## Installera agenten {#installing-the-agent}

>[!NOTE]
>
>Om du tidigare har installerat serialiseringsuppdateringen för AEM 6.1 tar du bort agentens startkommandon från din java-körningsrad.

1. Installera **com.adobe.cq.cq-serialization-testpaketet** .

1. Gå till webbkonsolen Bundle på `https://server:port/system/console/bundles`
1. Leta efter serialiseringspaketet och starta det. Detta bör automatiskt läsa in NotSoSerial-agenten.

## Installera agenten på programservrar {#installing-the-agent-on-application-servers}

NotSoSerial-agenten ingår inte i standarddistributionen av AEM för programservrar. Du kan dock extrahera den från AEM jar-distributionen och använda den med programserverkonfigurationen:

1. Ladda först ned AEM QuickStart-filen och extrahera den:

   ```shell
   java -jar aem-quickstart-6.2.0.jar -unpack
   ```

1. Gå till platsen för den uppzippade AEM-snabbstarten och kopiera `crx-quickstart/opt/notsoserial/` mappen till `crx-quickstart` mappen för AEM-programserverinstallationen.

1. Ändra ägarskap för `/opt` till användaren som kör servern:

   ```shell
   chown -R opt <user running the server>
   ```

1. Konfigurera och kontrollera att agenten har aktiverats korrekt enligt följande avsnitt i den här artikeln.

## Konfigurera agenten {#configuring-the-agent}

Standardkonfigurationen räcker för de flesta installationer. Detta inkluderar en svart lista över kända sårbara klasser för fjärrexekvering och en vitlista över paket där avserialisering av tillförlitliga data bör vara relativt säker.

Brandväggskonfigurationen är dynamisk och kan ändras när som helst genom att:

1. Gå till webbkonsolen på `https://server:port/system/console/configMgr`
1. Söker efter och klickar på **Brandväggskonfiguration för deserialisering.**

   >[!NOTE]
   >
   >Du kan även nå konfigurationssidan direkt genom att gå till URL:en på:
   >
   >* `https://server:port/system/console/configMgr/com.adobe.cq.deserfw.impl.DeserializationFirewallImpl`


Den här konfigurationen innehåller loggning av vitlista, svartlista och deserialisering.

**Vitlista**

I vitlistningsavsnittet är dessa klasser eller paketprefix som tillåts för deserialisering. Observera att om du avserialiserar egna klasser måste du lägga till antingen klasserna eller paketen i den här vitlistan.

**Blacklisting**

I avsnittet med svartlistning är klasser som aldrig tillåts för deserialisering. Den första uppsättningen av dessa klasser är begränsad till klasser som har befunnits sårbara för attacker på fjärrbasis. Svartlistan används före alla vitlistade poster.

**Diagnostikloggning**

I avsnittet för diagnostikloggning kan du välja flera alternativ för loggning när deserialisering sker. Dessa är endast inloggade första gången och loggas inte igen vid efterföljande användningar.

Standardvärdet för **class-name-only** kommer att informera dig om de klasser som avserialiseras.

Du kan också ange alternativet för **högar** som loggar en java-stack från det första deserialiseringsförsöket för att informera dig om var deserialiseringen sker. Detta kan vara användbart för att hitta och ta bort deserialisering från din användning.

## Verifiera agentens aktivering {#verifying-the-agent-s-activation}

Du kan verifiera deserialiseringsagentens konfiguration genom att gå till URL:en på:

* `https://server:port/system/console/healthcheck?tags=deserialization`

När du har åtkomst till URL:en visas en lista med hälsokontroller för agenten. Du kan avgöra om agenten har aktiverats på rätt sätt genom att verifiera att hälsokontrollerna har godkänts. Om de inte fungerar kan du behöva läsa in agenten manuellt.

Mer information om felsökning av problem med agenten finns i [Hantera fel med dynamisk agentinläsning](#handling-errors-with-dynamic-agent-loading) nedan.

>[!NOTE]
>
>Om du lägger `org.apache.commons.collections.functors` till i vitlistan misslyckas alltid hälsokontrollen.

## Hantera fel med dynamisk agentinläsning {#handling-errors-with-dynamic-agent-loading}

Om fel visas i loggen, eller om verifieringsstegen upptäcker ett problem med att läsa in agenten, kan du behöva läsa in agenten manuellt. Detta rekommenderas också om du använder en JRE (Java Runtime Environment) i stället för en JDK (Java Development Toolkit), eftersom verktygen för dynamisk inläsning inte är tillgängliga.

Följ instruktionerna nedan för att läsa in agenten manuellt:

1. Ändra startparametrarna för JVM för CQ-behållaren och lägg till följande alternativ:

   ```shell
   -javaagent:<aem-installation-folder>/crx-quickstart/opt/notsoserial/notsoserial.jar
   ```

   >[!NOTE]
   >
   >Detta kräver att även CQ/AEM-alternativet -nofork används, tillsammans med lämpliga JVM-minnesinställningar, eftersom agenten inte aktiveras på en forked JVM.

   >[!NOTE]
   >
   >Adobe-distributionen av NotSoSerial Agent-behållaren finns i mappen `crx-quickstart/opt/notsoserial/` i din AEM-installation.

1. Stoppa och starta om JVM,

1. Verifiera agentens aktivering igen genom att följa stegen ovan i [Verifiera agentens aktivering](/help/sites-administering/mitigating-serialization-issues.md#verifying-the-agent-s-activation).

## Andra överväganden {#other-considerations}

Om du kör på en IBM JVM läser du dokumentationen om stöd för Java Attach API på [den här platsen](https://www.ibm.com/support/knowledgecenter/SSSTCZ_2.0.0/com.ibm.rt.doc.20/user/attachapi.html).

