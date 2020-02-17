---
title: AEM Forms on OSGi Groups and Privileges
seo-title: AEM Forms on OSGi Groups and Privileges
description: Tilldela användare till grupperna för att hantera AEM Forms på OSGi
seo-description: Tilldela användare till grupperna för att hantera AEM Forms på OSGi
uuid: f269a206-356d-4cee-b449-05c5da87121a
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
content-type: reference
topic-tags: Configuration
discoiquuid: 1717b1b4-1c2a-450e-8e79-4156a974d5fa
docset: aem65
translation-type: tm+mt
source-git-commit: 76908a565bf9e6916db39d7db23c04d2d40b3247

---


# AEM Forms on OSGi Groups and Privileges{#aem-forms-on-osgi-groups-and-privileges}

Du kan [skapa grupper](/help/sites-administering/user-group-ac-admin.md#group-administration) och tilldela profiler och [användare](/help/sites-administering/user-group-ac-admin.md#user-administration) till grupperna i AEM. Dessa profiler styr behörigheter för de användare som är en del av gruppen.

När du har installerat [AEM Forms-tilläggspaketet](../../forms/using/installing-configuring-aem-forms-osgi.md)blir de grupper som omnämns i den här artikeln automatiskt tillgängliga för tilldelning. Exempel på sådana grupper är formuläranvändare och formuläranvändare. I följande tabell visas de uppgifter som en användare kan utföra för AEM Forms på OSGi baserat på grupptilldelningarna:

<table>
 <tbody>
  <tr>
   <td>Grupp</td> 
   <td>Uppgifter</td> 
  </tr>
  <tr>
   <td>formuläranvändare <sup><a href="#main-pars-text">[1]</a></sup></td> 
   <td>
    <ul> 
     <li>Skapa, förhandsgranska, publicera och skicka adaptiva formulär</li> 
     <li>Skapa, förhandsgranska och publicera interaktiv kommunikation och dokumentfragment</li> 
     <li>Överföra resurser till en AEM-instans</li> 
     <li>Skapa teman</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>formgivare</td> 
   <td>
    <ul> 
     <li>Skapa, förhandsgranska, publicera och skicka adaptiva formulär</li> 
     <li>Skapa, förhandsgranska och publicera interaktiv kommunikation och dokumentfragment</li> 
     <li>Skapa skript för adaptiva formulär med kodredigeraren</li> 
     <li>Överför resurser inklusive skript</li> 
     <li>Skapa teman</li> 
     <li>Importera paket som innehåller XDP</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>formulär-inskickning-granskare</td> 
   <td>
    <ul> 
     <li>Granska inskickat material</li> 
     <li>Godkänn eller avslå inskickade bidrag</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>template-authors <sup><a href="#main-pars-text">[2]</a></sup></td> 
   <td>
    <ul> 
     <li>Skapa och förhandsgranska anpassningsbara formulär eller mallar för interaktiv kommunikation</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>template-power-user</td> 
   <td>
    <ul> 
     <li>Skapa och förhandsgranska anpassningsbara formulär eller mallar för interaktiv kommunikation</li> 
     <li>Skapa skript för adaptiva formulär eller interaktiva kommunikationsmallar med kodredigeraren</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td><p>fdm-authors</p> </td> 
   <td>
    <ul> 
     <li>Skapa och ändra en formulärdatamodell</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>cm-agent-users</td> 
   <td>
    <ul> 
     <li>Få åtkomst till brev från Correspondence Management eller interaktiv kommunikation med hjälp av agentens användargränssnitt</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td><p>arbetsflödesredigerare</p> </td> 
   <td>
    <ul> 
     <li>Skapa ett inkorgsprogram</li> 
     <li>Skapa en arbetsflödesmodell</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>arbetsflöde-användare</td> 
   <td>
    <ul> 
     <li>Använd AEM-inkorgsprogram<br /> <strong>Obs! </strong>Du måste ha grupptilldelningar för cm-agent-users och arbetsflödesanvändare för att få tillgång till gränssnittet för Interactive Communications Agent i AEM-inkorgen.</li> 
     <li>Hantera arbetsflödesinstanser</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>fd-administratörer</td> 
   <td>
    <ul> 
     <li>Konfigurera PDF Generator</li> 
     <li>Konfigurera bevakad mapp</li> 
     <li>Hantera arbetsflödesprogram</li> 
    </ul> </td> 
  </tr>
 </tbody>
</table>

1. Användaren med gruppbehörighet för formulär-användare kan inte skriva skript för anpassade formulär.
1. Användaren med gruppbehörighet för mallförfattare kan inte skriva skript för mallar.

