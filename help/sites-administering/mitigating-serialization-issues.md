---
title: Åtgärda serialiseringsproblem i AEM
description: Lär dig hur du minskar serialiseringsproblem i AEM.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
exl-id: 01e9ab67-15e2-4bc4-9b8f-0c84bcd56862
solution: Experience Manager, Experience Manager Sites
feature: Security
role: Admin
source-git-commit: 48d12388d4707e61117116ca7eb533cea8c7ef34
workflow-type: tm+mt
source-wordcount: '904'
ht-degree: 0%

---

# Åtgärda serialiseringsproblem i AEM{#mitigating-serialization-issues-in-aem}

## Ökning {#overview}

AEM på Adobe hade ett nära samarbete med öppen källkodsprojektet [NotSoSerial](https://github.com/kantega/notsoserial) för att bidra till att minska de säkerhetsluckor som beskrivs i **CVE-2015-7501**. NotSoSerial licensieras under [Apache 2-licens](https://www.apache.org/licenses/LICENSE-2.0) och innehåller ASM-kod som licensierats separat [BSD-liknande licens](https://asm.ow2.io/).

Agentbehållaren som medföljer detta paket är distributionen av NotSoSerial efter Adobe.

NotSoSerial är en lösning på Java™-nivå till ett problem på Java™-nivå och är inte AEM. En preflight-kontroll läggs till i ett försök att avserialisera ett objekt. Den här kontrollen testar ett klassnamn mot en brandväggsliknande tillåtelselista, blockeringslista eller båda. På grund av det begränsade antalet klasser i standardvärdet blockeringslista är det osannolikt att det här testet påverkar ditt system eller din kod.

Som standard utför agenten en kontroll av blockeringslista mot aktuella kända sårbara klasser. Blockeringslista är avsett att skydda dig från den aktuella listan över explosioner som använder den här typen av sårbarhet.

Du kan konfigurera blockeringslista och tillåtelselista genom att följa instruktionerna i [Konfigurera agenten](/help/sites-administering/mitigating-serialization-issues.md#configuring-the-agent) i den här artikeln.

Medlet är avsett att bidra till att minska de senaste kända sårbara klasserna. Om ditt projekt avserialiserar otillförlitliga data kan det fortfarande vara känsligt för denial of service-attacker, slut på minnesattacker och okända framtida avserialiseringsattacker.

Adobe stöder officiellt Java™ 6, 7 och 8. Adobe förstår dock att NotSoSerial även stöder Java™ 5.

## Installera agenten {#installing-the-agent}

>[!NOTE]
>
>Om du tidigare har installerat serialiseringssnabbkorrigeringen för AEM 6.1 tar du bort agentens startkommandon från Java™-körningsraden.

1. Installera **com.adobe.cq.cq-serialization-testare** paket.

1. Gå till webbkonsolen Bundle på `https://server:port/system/console/bundles`
1. Leta efter serialiseringspaketet och starta det. När du gör det laddas NotSoSerial-agenten automatiskt.

## Installera agenten på programservrar {#installing-the-agent-on-application-servers}

NotSoSerial-agenten ingår inte i standarddistributionen av AEM för programservrar. Du kan dock extrahera den från AEM jar-distributionen och använda den med programserverkonfigurationen:

1. Ladda först ned AEM snabbstartsfil och extrahera den:

   ```shell
   java -jar aem-quickstart-6.2.0.jar -unpack
   ```

1. Gå till platsen för den uppzippade AEM snabbstarten och kopiera `crx-quickstart/opt/notsoserial/` mapp till `crx-quickstart` mapp för AEM.

1. Ändra ägarskap för `/opt` till användaren som kör servern:

   ```shell
   chown -R opt <user running the server>
   ```

1. Konfigurera och kontrollera att agenten har aktiverats korrekt enligt följande avsnitt i den här artikeln.

## Konfigurera agenten {#configuring-the-agent}

Standardkonfigurationen räcker för de flesta installationer. Den här konfigurationen innehåller en blockeringslista med kända, fjärrkörda sårbara klasser och en tillåtelselista paket där avserialisering av tillförlitliga data är säkert.

Brandväggskonfigurationen är dynamisk och kan ändras när som helst genom att:

1. Gå till webbkonsolen på `https://server:port/system/console/configMgr`
1. Söka efter och klicka **Konfiguration av brandvägg för deserialisering.**

   >[!NOTE]
   >
   >Du kan även nå konfigurationssidan direkt genom att gå till URL:en på:
   >
   >* `https://server:port/system/console/configMgr/com.adobe.cq.deserfw.impl.DeserializationFirewallImpl`

Den här konfigurationen innehåller loggning av tillåtelselista, blockeringslista och deserialisering.

**Tillåt lista**

I avsnittet Tillåt är dessa listor klasser eller paketprefix som tillåts för deserialisering. Om du avserialiserar egna klasser lägger du till antingen klasserna eller paketen i den här tillåtelselista.

**Blocklista**

I avsnittet med blocklistor är klasser som aldrig tillåts för deserialisering. Den första uppsättningen av dessa klasser är begränsad till klasser som har befunnits sårbara för attacker på fjärrbasis. Blockeringslista används före alla poster i listan över tillåtna.

**Diagnostikloggning**

I avsnittet för diagnostikloggning kan du välja flera alternativ för loggning när deserialisering sker. De här alternativen är bara inloggade första gången och loggas inte igen vid efterföljande användningar.

Standardvärdet för **class-name-only** informerar dig om de klasser som avserialiseras.

Du kan också ange **fullhög** som loggar en Java™-stack om det första deserialiseringsförsöket för att informera dig om var deserialiseringen äger rum. Det här alternativet är användbart när du vill hitta och ta bort deserialisering från din användning.

## Verifiera agentens aktivering {#verifying-the-agent-s-activation}

Du kan verifiera deserialiseringsagentens konfiguration genom att gå till URL:en på:

* `https://server:port/system/console/healthcheck?tags=deserialization`

När du har öppnat URL-adressen visas en lista med hälsokontroller som är relaterade till agenten. Du kan avgöra om agenten har aktiverats på rätt sätt genom att verifiera att hälsokontrollerna har godkänts. Om de misslyckas måste du läsa in agenten manuellt.

Mer information om felsökning av problem med agenten finns i [Hantera fel med dynamisk agentinläsning](#handling-errors-with-dynamic-agent-loading) nedan.

>[!NOTE]
>
>Om du lägger till `org.apache.commons.collections.functors` hälsokontrollen misslyckas alltid till tillåtelselista.

## Hantera fel med dynamisk agentinläsning {#handling-errors-with-dynamic-agent-loading}

Om fel visas i loggen, eller om verifieringsstegen upptäcker ett problem med att läsa in agenten, läser du in agenten manuellt. Det här arbetsflödet rekommenderas också om du använder en JRE (Java™ Runtime Environment) i stället för en JDK (Java™ Development Toolkit), eftersom verktygen för dynamisk inläsning inte är tillgängliga.

Så här läser du in agenten manuellt:

1. Redigera JVM-startparametrarna för CQ-behållaren och lägg till följande alternativ:

   ```shell
   -javaagent:<aem-installation-folder>/crx-quickstart/opt/notsoserial/notsoserial.jar
   ```

   >[!NOTE]
   >
   >Kräver att du även använder alternativet -nofork CQ/AEM, tillsammans med lämpliga JVM-minnesinställningar, eftersom agenten inte är aktiverad på en forked JVM.

   >[!NOTE]
   >
   >Adobe-distributionen av NotSoSerial Agent burk finns på `crx-quickstart/opt/notsoserial/` mapp för AEM.

1. Stoppa och starta om JVM,

1. Verifiera agentens aktivering igen genom att följa stegen ovan [Verifierar agentens aktivering](/help/sites-administering/mitigating-serialization-issues.md#verifying-the-agent-s-activation).

## Andra överväganden {#other-considerations}

Om du kör på en IBM® JVM läser du dokumentationen om stöd för Java™ Attach API på [den här platsen](https://www.ibm.com/docs/en/sdk-java-technology/8?topic=documentation-java-attach-api).
