---
title: Konfigurera Xcode-projektet och bygg iOS-appen
seo-title: Konfigurera Xcode-projektet och bygg iOS-appen
description: Beskriver hur du skapar en standardapp för AEM Forms för iOS.
seo-description: Beskriver hur du skapar en standardapp för AEM Forms för iOS.
uuid: 29779bbb-06b4-4ece-9f29-786afab59eaf
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 88555db2-712f-4ef9-bf47-76c7ba83d964
docset: aem65
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f

---


# Konfigurera Xcode-projektet och bygg iOS-appen{#set-up-the-xcode-project-and-build-the-ios-app}

AEM Forms tillhandahåller den fullständiga källkoden för appen AEM Forms. Källan innehåller alla komponenter för att skapa en anpassad AEM Forms-app. Källkodsarkivet, `adobe-lc-mobileworkspace-src-<version>.zip` är en del av paketet för `adobe-aemfd-forms-app-src-pkg-<version>.zip` paketresursen.

Så här hämtar du AEM Forms-appkällan:

1. Navigera till paketets shareURL: `https://<server>:<port>/crx/packageshare`.

1. Hämta källpaketet. När du hämtar paketet läggs det till i din AEM Forms-pakethanterare.
1. När nedladdningen är klar går du till: `https://<server>:<port>/crx/packmgr/index.jsp`, och installera `adobe-aemfd-forms-app-src-pkg-<version>.zip`.

1. Om du vill hämta källkodsarkivet öppnar du `https://<server>:<port>/crx/de/content/forms/mobileapps/src/adobe-lc-mobileworkspace-src-<version>.zip` i webbläsaren.
Källpaketet hämtas till din enhet.

I följande bild visas det extraherade innehållet i `adobe-lc-mobileworkspace-src-<version>.zip`.

![mws-content](assets/mws-content.png)

Följande tabell innehåller information om innehållet i `adobe-lc-mobileworkspace-src-[version]/ios` mappen.

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

Detaljerad information om kodsignering och hur du lägger till enheter till iOS Provisioning Portal finns i [iOS Code Signing Setup, Process och Troubleshooting](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppDistributionGuide/MaintainingCertificates/MaintainingCertificates.html).

## Bygg standardappen AEM Forms {#set-up-the-xcode-project}

1. Utför följande steg för att konfigurera ett projekt i Xcode och ange en signeringsidentitet:

   Logga in på en Mac-dator som har Xcode och iOS SDK installerat och konfigurerat.

1. Kopiera `adobe-lc-mobileworkspace-src-<version>.zip` arkivet från nedladdningsmappen till `[User_Home]/Projects/`.
1. Extrahera arkivet i `[User_Home]/Projects/[your-project]`katalogen.
1. Navigera till ` [User_Home]/Projects/ `[projektkatalogen]`/adobe-lc-mobileworkspace-src-[version]/ios` .
1. Öppna `AEM Forms.xcodeproj` projektet i Xcode.
1. Klicka på **AEM Forms** och välj **AEM Forms** under **MÅL**. Välj fliken **Build Settings **och gå till avsnittet **Code Signing Entitlement** . I fälten Debug and Release gör du något av följande:

   * Lämna fälten ospecificerade för att skapa en standardapp för mobil arbetsyta
   * Ange fälten som ska visas i [Skapa en säker AEM Forms-app för iOS](/help/forms/using/building-secure-mobile-workspace-app.md) för att skapa en säker AEM Forms-app.

1. Klicka på **Alla** på fliken **Bygginställningar** och sedan på **Kombinerad**.
1. Expandera **Kodsignering i listan** Inställningar ****.
1. Välj lämplig signatur för **Kodsigneringsidentitet**. Mer information om hur du skapar nya signaturer finns i [Skapa och hämta provisioneringsprofiler](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppStoreDistributionTutorial/CreatingYourTeamProvisioningProfile/CreatingYourTeamProvisioningProfile.html)för utveckling.
1. Se till att samma signatur är markerad för **Felsök**, **Frigör** och **Valfri iOS SDK**.
1. Ersätt följande kod i `AEM Forms-info.plist` filen:

   ```java
   <key>NSAppTransportSecurity</key>
   <dict>
   <key>NSAllowsArbitraryLoads</key>
   <true/>
   </dict>
   ```

   med följande när du ersätter `yourserver.com` med ett lämpligt värdnamn för servern.

   ```java
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
   >Det här steget krävs bara om appen AEM Forms behöver ansluta till en server som inte uppfyller kraven för App Transport Security.

1. Under **PROJEKT** väljer du **AEM Forms** och ser till att rätt signatur är markerat för **kodsigneringsidentitet**, **felsökning**, **release** **** och¥Any iOS SDK.
1. Anslut en provisionerad iPad till en Mac-dator.
1. Välj den tilldelade enheten för **AEM Forms** -projektet.

   ![ipad](assets/ipad.png)

   En etablerad enhet, iPad Air 2, har valts.

1. Välj **Produkt** > **Rengör**.
1. Välj **Produkt** > **Skapa**.

## Skapa installationsprogrammet för appen AEM Forms {#build-the-installer-for-the-mobile-workspace-app}

Du måste arkivera Xcode-projektet för att skapa installationsprogrammet (en IPA-fil) och en egenskapslista (en PLIST-fil). Egenskapslistfilen innehåller konfigurationsinformation för det värdbaserade interna programmet, till exempel namnet och appens värdplats. Mer information om egenskapslistfiler finns i [Om egenskapslistefiler](https://developer.apple.com/library/ios/#documentation/general/Reference/InfoPlistKeyReference/Articles/AboutInformationPropertyListFiles.html).

1. Anslut en provisionerad iPad till en Mac-dator. Mer information om hur du etablerar en iPad finns i [Skapa och hämta provisioneringsprofiler för utveckling](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppStoreDistributionTutorial/CreatingYourTeamProvisioningProfile/CreatingYourTeamProvisioningProfile.html)
1. Välj den tilldelade enheten för **AEM Forms** -projektet.

   ![ipad-1](assets/ipad-1.png)

   En etablerad enhet, iPad Air 2, har valts.

1. Välj **Produkt** > **Rengör**.
1. Välj **Produkt** > **Skapa**.
1. Välj **Produkt** > **Arkiv**.
1. I Sorteraren - Arkiv väljer du det senaste arkivet för projektet och klickar på **Distribuera**.
1. Välj **Spara för företag eller Ad-hoc-distribution** som distributionsmetod och klicka på **Nästa**.
1. Välj lämplig **kodsigneringsidentitet** och klicka på **Nästa**. Klicka på **Tillåt** för att använda signaturen.
1. Ange appens namn och välj **Spara för företagsdistribution**.
1. Ange programmets **program-URL** . Ange till exempel URL om du vill ha programmet på en CRX-server `https://[LC_host]:'port'/lc/content/distribution/mobileworkspace/APP_NAME.ipa`.
1. Ange AEM-formulär i fältet **Titel** .
1. Klicka på **Spara** och stäng Xcode.

   En installationsfil `AEM Forms.ipa`och egenskapslistefil `AEM Forms-info.plist`skapas på den angivna platsen.

1. Öppna `AEM Forms-info.plist` filen i en redigerare.
1. Ersätt alla blanksteg i URL:en för din .ipa-fil med %20.
1. Spara och stäng `AEM Forms-info.plist` filen.