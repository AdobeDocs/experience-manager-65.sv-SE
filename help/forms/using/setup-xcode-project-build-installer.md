---
title: Konfigurera Xcode-projektet och bygg iOS-appen
description: Beskriver hur du skapar AEM Forms standardprogram för iOS.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
docset: aem65
exl-id: 78ce6107-8821-47d6-86ab-7ab968945e7c
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '758'
ht-degree: 0%

---

# Konfigurera Xcode-projektet och bygg iOS-appen{#set-up-the-xcode-project-and-build-the-ios-app}

AEM Forms tillhandahåller den fullständiga källkoden för AEM Forms-appen. Källan innehåller alla komponenter som behövs för att skapa en anpassad AEM Forms-app. Källkodsarkivet, `adobe-lc-mobileworkspace-src-<version>.zip` är en del av `adobe-aemfd-forms-app-src-pkg-<version>.zip` paket om programvarudistribution.

Så här hämtar du programkällan för AEM Forms:

1. Öppna [Programvarudistribution](https://experience.adobe.com/downloads). Du behöver en Adobe ID för att logga in på Software Distribution.
1. Välj **[!UICONTROL Adobe Experience Manager]** finns i rubrikmenyn.
1. I **[!UICONTROL Filters]** avsnitt:
   1. Välj **[!UICONTROL Forms]** från **[!UICONTROL Solution]** listruta.
   2. Välj version och typ för paketet. Du kan också använda **[!UICONTROL Search Downloads]** för att filtrera resultaten.
1. Välj det paketnamn som gäller för operativsystemet och välj **[!UICONTROL Accept EULA Terms]** och markera **[!UICONTROL Download]**.
1. Öppna [Pakethanteraren](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html)  och klicka **[!UICONTROL Upload Package]** för att överföra paketet.
1. Markera paketet och klicka på **[!UICONTROL Install]**.

1. Öppna om du vill hämta källkodsarkivet `https://<server>:<port>/crx/de/content/forms/mobileapps/src/adobe-lc-mobileworkspace-src-<version>.zip` i webbläsaren.
Källpaketet hämtas till din enhet.

I följande bild visas det extraherade innehållet i `adobe-lc-mobileworkspace-src-<version>.zip`.

![mws-content](assets/mws-content.png)

Innehållet i följande tabell `adobe-lc-mobileworkspace-src-[version]/ios` mapp.

<table>
 <tbody>
  <tr>
   <th><p>Katalog</p> </th>
   <th><p>Innehåll</p> </th>
  </tr>
  <tr>
   <td><p><code>CordovaLib</code></p> </td>
   <td><p>PhoneGap SDK 6.4.0</p> </td>
  </tr>
  <tr>
   <td><p><code>AEM Forms</code></p> </td>
   <td><p>Resurser, plugin-program för PhoneGap och programmets huvudmodul</p> </td>
  </tr>
  <tr>
   <td><p><code>AEM Forms.xcodeproj</code></p> </td>
   <td><p>Xcode project for AEM Forms app</p> </td>
  </tr>
  <tr>
   <td><p><code>www</code></p> </td>
   <td><p>HTML, CSS, bilder och JavaScript-filer för AEM Forms-appprojektet</p> </td>
  </tr>
 </tbody>
</table>

Mer information om kodsignering och hur du lägger till enheter i iOS Provisioning Portal finns i [iOS Code Signing Setup, Process, and Troubleshooting](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppDistributionGuide/MaintainingCertificates/MaintainingCertificates.html).

## Bygg AEM Forms standardapp {#set-up-the-xcode-project}

1. Utför följande steg för att konfigurera ett projekt i Xcode och ange en signeringsidentitet:

   Logga in på den Mac-dator där Xcode och iOS SDK är installerade och konfigurerade.

1. Kopiera `adobe-lc-mobileworkspace-src-<version>.zip` arkivera från nedladdningsmappen till `[User_Home]/Projects/`.
1. Extrahera arkivet i `[User_Home]/Projects/[your-project]`katalog.
1. Navigera till ` [User_Home]/Projects/ `[ditt projekt]`/adobe-lc-mobileworkspace-src-[version]/ios` katalog.
1. Öppna `AEM Forms.xcodeproj` projekt i Xcode.
1. Klicka **AEM Forms**, under **MÅLGRUPPER**, markera **AEM Forms**. Välj **Inställningar för bygge** -fliken, leta upp **Kodsigneringsberättigande** och gör något av följande i fälten Felsök och Frigör:

   * Lämna fälten ospecificerade för att skapa en standardapp för mobil arbetsyta
   * Ange fälten som ska anges i [Skapa en säker AEM Forms-app för iOS](/help/forms/using/building-secure-mobile-workspace-app.md) för att skapa en säker AEM Forms-app.

1. I **Inställningar för bygge** flik, klicka **Alla** och sedan klicka **Kombinerad**.
1. Från **Inställningar** lista, expandera **Kodsignering**.
1. För **Kodsigneringsidentitet** väljer du lämplig signatur. Mer information om hur du skapar nya signaturer finns i [Skapa och hämta provisioneringsprofiler för utveckling](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppStoreDistributionTutorial/CreatingYourTeamProvisioningProfile/CreatingYourTeamProvisioningProfile.html).
1. Se till att samma signatur är vald för **Felsök**, **Frigör** och **Alla iOS SDK**.
1. Ersätt följande kod i `AEM Forms-info.plist` fil:

   ```xml
   <key>NSAppTransportSecurity</key>
   <dict>
   <key>NSAllowsArbitraryLoads</key>
   <true/>
   </dict>
   ```

   med följande vid ersättning `yourserver.com` med ett lämpligt värdnamn för servern.

   ```xml
   <key>NSAppTransportSecurity</key>
   <dict>
   <key>NSExceptionDomains</key>
   <dict>
   <key>yourserver.com</key>
   <dict>
   <!-Include to allow subdomains->
   <key>NSIncludesSubdomains</key>
   <true/>
   <!-Include to allow HTTP requests->
   <key>NSTemporaryExceptionAllowsInsecureHTTPLoads</key>
   <true/>
   <!-Include to support forward secrecy->
   <key>NSExceptionRequiresForwardSecrecy</key>
   <false/>
   <!-Include to specify minimum TLS version->
   <key>NSTemporaryExceptionMinimumTLSVersion</key>
   <string>TLSv1.1</string>
   </dict>
   </dict>
   </dict>
   ```

   >[!NOTE]
   >
   >Det här steget krävs bara om AEM Forms-appen behöver ansluta till en server som inte uppfyller kraven för App Transport Security.

1. Under **PROJEKT**, markera **AEM Forms** och se till att rätt signatur väljs för **Kodsigneringsidentitet**, **Felsök**, **Frigör** och **Alla iOS SDK**.
1. Anslut en etablerad iPad till en Mac-dator.
1. Välj den tilldelade enheten för **AEM Forms** projekt.

   ![ipad](assets/ipad.png)

   En etablerad enhet, iPad Air 2, har valts.

1. Välj **Produkt** > **Ren**.
1. Välj **Produkt** > **Bygge**.

## Skapa installationsprogrammet för AEM Forms-appen {#build-the-installer-for-the-mobile-workspace-app}

Du måste arkivera Xcode-projektet för att skapa installationsprogrammet (en IPA-fil) och en egenskapslista (en PLIST-fil). Egenskapslistfilen innehåller konfigurationsinformation för det värdbaserade interna programmet, till exempel namnet och appens värdplats. Mer information om egenskapslistfilen finns i [Om egenskapslistfiler för information](https://developer.apple.com/library/ios/#documentation/general/Reference/InfoPlistKeyReference/Articles/AboutInformationPropertyListFiles.html).

1. Anslut en etablerad iPad till en Mac-dator. Mer information om hur du etablerar ett iPad finns i [Skapa och hämta provisioneringsprofiler för utveckling](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppStoreDistributionTutorial/CreatingYourTeamProvisioningProfile/CreatingYourTeamProvisioningProfile.html)
1. Välj den tilldelade enheten för **AEM Forms** projekt.

   ![ipad-1](assets/ipad-1.png)

   En etablerad enhet, iPad Air 2, har valts.

1. Välj **Produkt** > **Ren**.
1. Välj **Produkt** > **Bygge**.
1. Välj **Produkt** > **Arkiv**.
1. I Sorteraren - Arkiv väljer du det senaste arkivet för ditt projekt och klickar på **Distribuera**.
1. Välj **Spara för företag eller Ad hoc-distribution** som distributionsmetod och klicka **Nästa**.
1. Välj lämplig **Kodsigneringsidentitet** och klicka **Nästa**. Klicka **Tillåt** för att använda signaturen.
1. Ange namnet på appen och välj **Spara för företagsdistribution**.
1. Ange **Program-URL** för appen. Om du till exempel vill lägga appen på en CRX-server anger du en URL `https://[LC_host]:'port'/lc/content/distribution/mobileworkspace/APP_NAME.ipa`.
1. I **Titel** anger du AEM Forms.
1. Klicka **Spara** och stäng Xcode.

   En installationsfil, `AEM Forms.ipa`och egenskapslistefil, `AEM Forms-info.plist`, skapas på den angivna platsen.

1. Öppna `AEM Forms-info.plist` i en redigerare.
1. Ersätt alla blanksteg i URL:en för din .ipa-fil med %20.
1. Spara och stäng `AEM Forms-info.plist` -fil.
