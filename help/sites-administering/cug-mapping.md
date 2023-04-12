---
title: Mappning av anpassade användargrupper i AEM 6.5
seo-title: Custom User Group Mapping in AEM 6.5
description: Läs om hur anpassad mappning av användargrupper fungerar i AEM.
seo-description: Lear how Custom User Group Mapping works in AEM.
uuid: 7520351a-ab71-4661-b214-a0ef012c0c93
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: 13085dd3-d283-4354-874b-cd837a9db9f9
docset: aem65
exl-id: 661602eb-a117-454d-93d3-a079584f7a5d
feature: Security
source-git-commit: 2981f11565db957fac323f81014af83cab2c0a12
workflow-type: tm+mt
source-wordcount: '478'
ht-degree: 0%

---

# Mappning av anpassade användargrupper i AEM 6.5 {#custom-user-group-mapping-in-aem}

## Jämförelse av JCR-innehåll relaterat till CUG (anpassad användargrupp) {#comparison-of-jcr-content-related-to-cug}

<table>
 <tbody>
  <tr>
   <td><strong>Äldre AEM versioner</strong></td>
   <td><strong>AEM 6.5</strong></td>
   <td><strong>Kommentarer</strong></td>
  </tr>
  <tr>
   <td><p>Egenskap: cq:cugEnabled</p> <p>Deklarerar nodtyp: N/A, övrig egendom</p> </td>
   <td><p>Behörighet:</p> <p>Nod: rep:cugPolicy för nodtypen rep:CugPolicy</p> <p>Deklarerar nodtyp: rep:CugMixin</p> <p> </p> <p> </p> <p> </p> Autentisering:</p> <p>Blandningstyp: granit:AuthenticationRequired</p> </td>
   <td><p>För att begränsa läsåtkomst tillämpas en dedikerad CUG-princip på målnoden.</p> <p>OBS! Profiler kan bara tillämpas på de sökvägar som har konfigurerats och stöds.</p> <p>Noder med namnet rep:cugPolicy och typen rep:CugPolicy är skyddade och kan inte skrivas med vanliga JCR API-anrop; använd JCR-åtkomstkontroll i stället.</p> <p>Se <a href="https://jackrabbit.apache.org/oak/docs/security/authorization/cug.html">den här sidan</a> för mer information.</p> <p>För att framtvinga autentiseringskrav på en nod räcker det att lägga till blandningstypen granite:AuthenticationRequired.</p> <p>OBS! Endast respekterad under de sökvägar som stöds.</p> </td>
  </tr>
  <tr>
   <td><p>Egenskap: cq:cugPrincipals</p> <p>Deklarerar nodtyp: NA, övrig egendom</p> </td>
   <td><p>Egenskap: rep:mainNames</p> <p>Deklarerar nodtyp: rep:CugPolicy</p> </td>
   <td><p>Egenskapen som innehåller namnen på de principer som får läsa innehållet under den begränsade CUG:n är skyddad och kan inte skrivas med vanliga JCR API-anrop. använd JCR-åtkomstkontroll i stället.</p> <p>Se <a href="https://jackrabbit.apache.org/api/2.12/org/apache/jackrabbit/api/security/authorization/PrincipalSetPolicy.html">den här sidan</a> för mer information om implementeringen.</p> </td>
  </tr>
  <tr>
   <td><p>Egenskap: cq:cugLoginPage</p> <p>Deklarerar nodtyp: NA, övrig egendom</p> </td>
   <td><p>Egenskap: granite:loginPath (valfritt)</p> <p>Deklarerar nodtyp: granit:AuthenticationRequired</p> </td>
   <td><p>En JCR-nod som har blandningstypen granite:AuthenticationRequired definierad kan eventuellt definiera en alternativ inloggningssökväg.</p> <p>OBS! Endast respekterad under de sökvägar som stöds.</p> </td>
  </tr>
  <tr>
   <td><p>Egenskap: cq:cugRealm</p> <p>Deklarerar nodtyp: NA, övrig egendom</p> </td>
   <td>NA</td>
   <td>Stöds inte längre med den nya implementeringen.</td>
  </tr>
 </tbody>
</table>

## Jämförelse av OSGi-tjänster {#comparison-of-osgi-services}

**Äldre AEM versioner**

Etikett: Stöd för CUG (Adobe Granite Closed User Group)

Namn: com.day.cq.auth.impl.CugSupportImpl

**AEM 6.5**

* Etikett: Konfiguration av Apache Jackrabbit Oak CUG

   Namn: org.apache.jackrabbit.oak.spi.security.permission.cug.impl.CugConfiguration

   ConfigurationPolicy = REQUIRED

* Etikett: Apache Jackrabbit Oak CUG Exclude List

   Namn: org.apache.jackrabbit.oak.spi.security.permission.cug.impl.CugExcludeImpl

   ConfigurationPolicy = REQUIRED

* Namn: com.adobe.granite.auth.requirements.impl.RequirementService
* Etikett: Autentiseringskrav och hanterare för inloggningssökväg för Adobe Granite

   Namn: com.adobe.granite.auth.requirements.impl.DefaultRequirementHandler

   ConfigurationPolicy = REQUIRED

**Kommentarer**

* Konfiguration av CUG-auktoriseringen och aktivera/inaktivera utvärderingen.
Tjänst för att konfigurera exkluderingslista för huvudobjekt som inte ska påverkas av CUG-auktoriseringen.

   >[!NOTE]
   > 
   >Om `CugExcludeImpl` är inte konfigurerad, `CugConfiguration` återgår till standardinställningen.

   Det går att koppla en anpassad CugExclude-implementering om det finns särskilda behov.

* OSGi-komponenten som implementerar LoginPathProvider som visar en matchande inloggningssökväg för LoginSelectorHandler. Den har en obligatorisk referens till en RequirementHandler som används för att registrera observatören som lyssnar på ändrade autentiseringskrav som lagras i innehållet med hjälp av blandningstypen granite:AuthenticationRequired.
* OSGi-komponenten som implementerar RequirementHandler som meddelar SlingAuthenticator om ändringar i auktoriseringskrav.

   Eftersom konfigurationsprincipen för den här komponenten är NÖDVÄNDIG aktiveras den bara om en uppsättning sökvägar som stöds har angetts.

   Om tjänsten aktiveras startas RequirementService.

<!-- nested tables not supported - text above is the table>
<table>
 <tbody>
  <tr>
   <td><strong>Older AEM Versions</strong></td>
   <td><strong>AEM 6.5</strong></td>
   <td><strong>Comments</strong></td>
  </tr>
  <tr>
   <td><p>Label: Adobe Granite Closed User Group (CUG) Support</p> <p>Name: com.day.cq.auth.impl.CugSupportImpl</p> </td>
   <td><p>Label: Apache Jackrabbit Oak CUG Configuration</p> <p>Name: org.apache.jackrabbit.oak.spi.security.authorization.cug.impl.CugConfiguration</p> <p>ConfigurationPolicy = REQUIRED</p> </td>
    <td><p>Label: Apache Jackrabbit Oak CUG Exclude List</p> <p>Name: org.apache.jackrabbit.oak.spi.security.authorization.cug.impl.CugExcludeImpl</p> <p>ConfigurationPolicy = REQUIRED</p> <p> </p> <p> </p> <p> </p> <p> </p> </td>
      </tr>
      <tr>
       <td>Name: com.adobe.granite.auth.requirement.impl.RequirementService</td>
      </tr>
      <tr>
       <td><p>Label: Adobe Granite Authentication Requirement and Login Path Handler</p> <p>Name: com.adobe.granite.auth.requirement.impl.DefaultRequirementHandler</p> <p>ConfigurationPolicy = REQUIRED</p> </td>
      </tr>
     </tbody>
    </table> </td>
   <td>
     <tbody>
      <tr>
       <td>Configuration of the CUG authorization and enable/disable the evaluation.</td>
      </tr>
      <tr>
       <td><p>Service to configure exclusion list of principals which should not be affected by the CUG authorization.</p> <p>NOTE: If the CugExcludeImpl is not configured, the CugConfiguration will fall back to the default.</p> <p>It is possible to plug a custom CugExclude implementation in case of special needs.</p> </td>
      </tr>
      <tr>
       <td>OSGi component implementing LoginPathProvider that exposes a matching login path to the LoginSelectorHandler. It has a mandatory reference to a RequirementHandler which is used to register the observer that listens to changed auth requirements stored in the content by the means of the granite:AuthenticationRequired mixin type. </td>
      </tr>
      <tr>
       <td><p>OSGi component implementing RequirementHandler that notifies the SlingAuthenticator about changes to authrequirements.</p> <p>As configuration policy for this component is REQUIRE it will only be activated if a set of supported paths is specified.</p> <p>Enabling the service will launch the RequirementService.</p> </td>
      </tr>
     </tbody>
     </td>
  </tr>
  <tr>
   <td> </td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td> </td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td> </td>
   <td> </td>
   <td> </td>
  </tr>
 </tbody>
</table>
-->
