---
title: Visa användarens avatar
seo-title: Visa användarens avatar
description: Hur man anpassar arbetsytan i AEM Forms så att bilden för en inloggad användare visas.
seo-description: Hur man anpassar arbetsytan i AEM Forms så att bilden för en inloggad användare visas.
uuid: 2961dc93-f0d0-4842-80f1-3c239a20e348
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: aec03ea5-17a6-4775-92cb-2ad361895fdf
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Visa användarens avatar {#displaying-the-user-avatar}

Avatar för den inloggade användaren visas i det övre högra hörnet på arbetsytan i AEM Forms. Variatarerna för direkta rapporter i organisationshierarkin visas också i hanterarvyn. Du kan konfigurera arbetsytan för AEM Forms så att du kan välja användarbilder från din databas, till exempel LDAP-server.

>[!NOTE]
>
>De proportioner som stöds för användarbilderna är 1:1.

1. Skapa en DSC med hjälp av de uppgifter som anges i nästa steg. Mer information finns i avsnittet&quot;Utveckla komponenter för AEM Forms&quot; i [Programmering med AEM Forms](https://www.adobe.com/go/learn_aemforms_programming_63) -guiden.
1. I DSC definierar du en ny SPI som visar metoderna getCurrentUserImageUrl och getUserImageUrl för att hämta en bild-URL för en AEM Forms-användare. Här följer ett exempel på ett Java™-kodfragment:

   ```as3
   public class DemoUserImageURLProviderService {
     public String getCurrentUserImageUrl()
     {
        // return the URL for profile Image of logged in user
     }
     public String getUserImageUrl(String principalOid)
     {
         // return the URL for profile Image for user represented by this principal Oid
      }
   }
   ```

1. Skapa en component.xml-fil. Kontrollera att spec-id är som det visas i kodfragmentet nedan.

   Följande kodfragment är ett exempel. Anpassa den efter dina specifika behov.

   ```as3
   <component xmlns="https://adobe.com/idp/dsc/component/document">
       <component-id>com.adobe.sample.DemoUsersComponent</component-id>
       <version>1.1</version>
       <supports-export>false</supports-export>
       <descriptor-class>com.adobe.idp.dsc.component.impl.DefaultPOJODescriptorImpl</descriptor-class>
       <services>
           <service name="DemoUserImageURLProviderService" title="Demo User ImageURL provider service" orchestrateable="false">
           <auto-deploy service-id="DemoUserImageURLProviderService" category-id="Demo Users Component DSC" major-version="1" minor-version="0" />
           <description>Service for resolving user image url.</description>
            <specifications>
            <specification spec-id="com.adobe.idp.taskmanager.dsc.enterprise.UserImageUrlProvider"/>
            </specifications>
           <specification-version>1.0</specification-version>
           <implementation-class>com.adobe.sample.demousers.DemoUserImageURLProviderService</implementation-class>
           <request-processing-strategy>single_instance</request-processing-strategy>
           <supported-connectors>default</supported-connectors>
           <operation-config>
               <operation-name>*</operation-name>
               <transaction-type>Container</transaction-type>
               <transaction-propagation>supports</transaction-propagation>
               <!--transaction-timeout>3000</transaction-timeout-->
           </operation-config>
           <operations>
               <operation anonymous-access="false" name="getCurrentUserImageUrl" method="getCurrentUserImageUrl">
                   <output-parameter name="result" type="java.lang.String"/>
               </operation>
               <operation anonymous-access="false" name="getUserImageUrl"
   method="getUserImageUrl">
               <input-parameter name="principalOid" type="java.lang.String"/>
               <output-parameter name="result" type="java.lang.String"/>
               </operation>
           </operations>
           </service>
       </services>
   </component>
   ```

1. Distribuera DSC via Workbench. Starta om `ProcessManagementClientSessionService` tjänsten.
1. Du kan behöva uppdatera webbläsaren eller logga ut/logga in med användaren igen.

[Kontakta supporten](https://www.adobe.com/account/sign-in.supportportal.html)
