---
title: Säkerhetsluckor för felsökning av XXE, Konfiguration av startläge och Fjärrkodskörning för AEM Forms i JEE
description: Säkerhetsluckor för att åtgärda XXE, konfiguration och fjärrexekvering av kod för AEM Forms i JEE
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Security
geptopics: SG_AEMFORMS/categories/jee
role: Admin
exl-id: c8f3e7c1-d5a2-4e2f-8b9c-1a8d7f8e2a9b
solution: Experience Manager, Experience Manager Forms
release-date: 2025-08-05T00:00:00Z
source-git-commit: b810aadeb2741ff2fba28f81b508637f21feb8f9
workflow-type: tm+mt
source-wordcount: '676'
ht-degree: 3%

---


# Mitigating RCE (CVE-2025-49533), Struts Dev Mode Configuration (CVE-2025-54253), XXE (CVE-2025-54254) och Vulnerabilities for AEM Forms on JEE {#mitigating-xxe-configuration-rce-vulnerabilities-aem-forms}

## Snabbreferens

| **Effektnivå** | **Versioner som påverkas** | **Rekommenderad åtgärd** |
|---|---|---|
| **Kritisk** | AEM 6.5 Forms på JEE Service Pack 23 (6.5.23.0) | [Installera den senaste snabbkorrigeringen](#option-1-for-users-on-version-65230-install-latest-hotfix) |
| **Kritisk** | AEM 6.5 Forms i JEE Service Pack 18 till 22 (6.5.18.0 - 6.5.22.0) | [Installera korrigeringarna manuellt](#option-2-for-users-on-65180---65220-manual-hotfix-installation) |
| **Kritisk** | AEM 6.5 Forms i JEE Service Pack 17 (6.5.17.0) eller tidigare | Uppgradera till en Service Pack-version som stöds och använd sedan de rekommenderade reduceringsstegen för den nya versionen |
| **Påverkas inte** | AEM Forms on OSGi, Workbench, Cloud Service | Ingen åtgärd krävs |

**Säkerhetsluckor som har åtgärdats:**

- Fjärrexekvering av kod (CVE-2025-49533)
- Konfigurationssäkerhetsproblem (CVE-2025-54253)
- XML-bearbetning av extern enhet (XXE) (CVE-2025-54254)

## Ökning

### Vad som påverkas

| Sårbarhet | Effekt | Komponenter som påverkas |
|---|---|---|
| **CVE-2025-49533**: Fjärrexekvering av kod | Oautentiserad kodkörning i GetDocumentServlet | AEM 6.5 Forms i JEE Service Pack 23 (6.5.23.0) och tidigare |
| **CVE-2025-54253**: Konfigurationsproblem | Stänger utvecklingsläget som är aktiverat i administratörsgränssnittet | AEM 6.5 Forms i JEE Service Pack 23 (6.5.23.0) och tidigare |
| **CVE-2025-54254**: XXE-bearbetning | Dokumentsäkerhetsmodulen ger obehörig åtkomst | AEM 6.5 Forms i JEE Service Pack 23 (6.5.23.0) och tidigare |


### Vad som inte påverkas

- Experience Manager Forms Workbench (alla versioner)
- Experience Manager Forms on OSGi (alla versioner)
- Experience Manager Forms as a Cloud Service

## Upplösningsalternativ


### Innan du börjar

Innan du gör några ändringar bör du göra en säkerhetskopia av den EAR-fil eller DSC-fil som du håller på att ändra eller uppdatera:

- Leta reda på den ursprungliga EAR- eller DSC-filen i din distributionskatalog.
- Kopiera filen till en säker plats för säkerhetskopiering utanför distributionskatalogen.
- Kontrollera att säkerhetskopian är fullständig och tillgänglig innan du fortsätter med uppdateringarna.

Med den här säkerhetsfunktionen kan du återställa det ursprungliga läget om du stöter på problem under uppdateringsprocessen.

### Alternativ 1: (För användare i version 6.5.23.0) Installera den senaste snabbkorrigeringen

1. [Hämta snabbkorrigeringen för 6.5.23.0](/help/release-notes/aem-forms-hotfix.md).
2. Följ standardinstruktionerna för installation av [snabbkorrigering/korrigering](/help/release-notes/jee-patch-installer-65.md)
3. Om du använder dokumentsäkerhet (tidigare Rights Management) på IBM WebSphere eller Oracle WebLogic anger du följande Java-systemegenskap (JVM-argument) innan du startar AEM Forms-servern:

   ```
   -Dcom.adobe.forms.jee.services.allowDoctypeDeclaration=true
   ```

4. Starta om programservern

</details>

### Alternativ 2: (För användare på 6.5.18.0 - 6.5.22.0) Manuell Hotfix-installation


<details>
<summary><b>Manuell programfixinstallation för 6.5.18.0 - 6.5.22.0</b></summary>

**Steg 1: Hämta och extrahera snabbkorrigeringspaketet**

- Hämta [snabbkorrigeringen för 6.5.18.0 - 6.5.22.2&rbrace; från Adobe Software Distribution Portal](/help/release-notes/aem-forms-hotfix.md)
- Extrahera lokalt

**Steg 2: Navigera till rätt versionsmapp**

- Gå till den matchande mappen baserat på vilken Service Pack-version som är installerad i din miljö.

  Exempel för Service Pack 20 är:

  ```
  <extracted-hotfix>/SP20/
  ```

**Steg 3: Leta reda på distributionskatalogen**

- På din AEM Forms på JEE-server går du till:

  ```
  [AEM installation directory]/deploy
  ```

  Exempel: `adobe/adobe-experience-manager-forms/deploy`



**Steg 4: Uppdatera och ersätt EAR-filerna**

>[!BEGINTABS]

>[!TAB JBoss]

1. Öppna `adobe-core-jboss.ear` och ersätt `adminui.war` med

   ```
   adobe-xxe-configuration-hotfix/SP[version]/jboss/adminui.war
   ```

   Exempel: `adobe-xxe-configuration-hotfix/SP20/jboss/adminui.war`

2. I `adobe-core-jboss.ear` går du till mappen `lib/` och ersätter `adobe-uisupport.jar` med:

   ```
   adobe-xxe-configuration-hotfix/SP[version]/adobe-uisupport.jar
   ```

   Exempel: `adobe-xxe-configuration-hotfix/SP20/adobe-uisupport.jar`

3. Spara på EAR. Se till att ändringarna sparas korrekt.


4. Ersätt `adobe-edcserver-jboss.ear` med

   ```
   adobe-xxe-configuration-hotfix/SP[version]/jboss/adobe-edcserver-jboss.ear
   ```

   Exempel: `adobe-xxe-configuration-hotfix/SP20/jboss/adobe-edcserver-jboss.ear`

5. Ersätt `adobe-forms-jboss.ear` med

   ```
   adobe-xxe-configuration-hotfix/SP[version]/jboss/adobe-forms-jboss.ear
   ```

   Exempel: `adobe-xxe-configuration-hotfix/SP20/jboss/adobe-forms-jboss.ear`



>[!TAB WebLogic]

1. Öppna `adobe-core-weblogic.ear` och ersätt `adminui.war` med

   ```
   adobe-xxe-configuration-hotfix/SP[version]/weblogic/adminui.war
   ```

   Exempel: `adobe-xxe-configuration-hotfix/SP20/weblogic/adminui.war`

2. I `adobe-core-weblogic.ear` ersätter du `adobe-uisupport.jar` med:

   ```
   adobe-xxe-configuration-hotfix/SP[version]/adobe-uisupport.jar
   ```

   Exempel: `adobe-xxe-configuration-hotfix/SP20/adobe-uisupport.jar`

3. Spara på EAR. Se till att ändringarna sparas korrekt.


4. Ersätt `adobe-edcserver-weblogic.ear` med

   ```
   adobe-xxe-configuration-hotfix/SP[version]/weblogic/adobe-edcserver-weblogic.ear
   ```

   Exempel: `adobe-xxe-configuration-hotfix/SP20/weblogic/adobe-edcserver-weblogic.ear`

5. Ersätt `adobe-forms-weblogic.ear` med

   ```
   adobe-xxe-configuration-hotfix/SP[version]/weblogic/adobe-forms-weblogic.ear
   ```

   Exempel: `adobe-xxe-configuration-hotfix/SP20/weblogic/adobe-forms-weblogic.ear`

>[!TAB WebSphere]

1. Öppna `adobe-core-websphere.ear` och ersätt `adminui.war` med

   ```
   adobe-xxe-configuration-hotfix/SP[version]/websphere/adminui.war
   ```

   Exempel: `adobe-xxe-configuration-hotfix/SP20/websphere/adminui.war`

2. I `adobe-core-websphere.ear` ersätter du `adobe-uisupport.jar` med:

   ```
   adobe-xxe-configuration-hotfix/SP[version]/adobe-uisupport.jar
   ```

   Exempel: `adobe-xxe-configuration-hotfix/SP20/adobe-uisupport.jar`

3. Spara på EAR. Se till att ändringarna sparas korrekt.


4. Ersätt `adobe-edcserver-websphere.ear` med

   ```
   adobe-xxe-configuration-hotfix/SP[version]/websphere/adobe-edcserver-websphere.ear
   ```

   Exempel: `adobe-xxe-configuration-hotfix/SP20/websphere/adobe-edcserver-websphere.ear`

5. Ersätt `adobe-forms-websphere.ear` med

   ```
   adobe-xxe-configuration-hotfix/SP[version]/websphere/adobe-forms-websphere.ear
   ```

   Exempel: `adobe-xxe-configuration-hotfix/SP20/websphere/adobe-forms-websphere.ear`

>[!ENDTABS]



**Steg 5: Uppdatera `adobe-rightsmanagement-<appserver>-dsc.jar`filen med**

```
adobe-xxe-configuration-hotfix/SP[version]/<appserver>/adobe-rightsmanagement-<appserver>-dsc.jar
```

Exempel: `adobe-xxe-configuration-hotfix/SP20/jboss/adobe-rightsmanagement-jboss-dsc.jar`

**Steg 6: Ytterligare konfiguration för dokumentsäkerhet i WebSphere och WebLogic**:

Om du använder Dokumentsäkerhet (tidigare Rights Management) anger du följande Java-systemegenskap (JVM-argument) innan du startar AEM Forms-servern:

```
-Dcom.adobe.forms.jee.services.allowDoctypeDeclaration=true
```


**Steg 7: Kör Configuration Manager igen**

- Starta Configuration Manager för att omdistribuera den uppdaterade EAR-uppdateringen och tillämpa snabbkorrigeringen

</details>

### Alternativ 3: (För användare på 6.5.17.0 och tidigare) Uppgraderingssökväg

1. [Uppgradera till en Service Pack-version som stöds](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md)
2. Följ alternativ 1 eller alternativ 2 ovan baserat på den nya versionen

## Referenser

- [CWE-611: Felaktig begränsning av XML-extern entitetsreferens](https://cwe.mitre.org/data/definitions/611.html)
- [CWE-16: Konfiguration](https://cwe.mitre.org/data/definitions/16.html)
- [OWASP XXE Prevention Cheat Sheet](https://owasp.org/www-community/vulnerabilities/XML_External_Entity_XXE_Processing)
- [Adobe Experience Manager Forms bästa säkerhetspraxis](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/security.html)