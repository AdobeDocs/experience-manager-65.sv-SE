---
title: Omfaktorisering för SocialUtils
description: Paketet com.adobe.cq.social.ugcbase.SocialUtils har tagits bort i AEM 6.1
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 0f731ec6-a12e-4098-a1ec-ee4cd4dc1432
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 07289e891399a78568dcac957bc089cc08c7898c
workflow-type: tm+mt
source-wordcount: '297'
ht-degree: 0%

---

# Omfaktorisering för SocialUtils {#socialutils-refactoring}

## Paketet SocialUtils har tagits bort {#socialutils-package-deprecated}

Paketet `com.adobe.cq.social.ugcbase.SocialUtils` har tagits bort i AEM 6.1.

I följande tabeller visas de metoder som ska användas i stället för `SocialUtils` metoder.

## Paket för SocialResourceUtilities  {#socialresourceutilities-package}

| Metoder i com.adobe.cq.social.srp.utilities.api.SocialResourceUtilities | Anteckningar |
|---|---|
| Boolean checkPermission(ResourceResolver resolver, String path, String action) |  |
| SocialResourceProvider getSocialResourceProvider(Resurs) |  |
| SocialResourceConfiguration getStorageConfig(resurs) |  |
| Resurs getUGCResource(Resource userResource) |  |
| Resurs getUGCResource(Resource userResource, ResourceResolverFactory rf) | new |
| Resurs getUGCResource(Resource userResource, ResourceResolverFactory rf, String resourceTypeHint) | new |
| Resurs getUGCResource(Resource userResource, String resourceTypeHint) |  |
| boolesk hasModeratePermissions(Resource resource) |  |
| SträngresursToACLPath(resurs) |  |
| SträngresursToUGCStoragePath(resurs) | ersätter String resourceToUGCPath(Resource) |
| Sträng UGCToResourcePath(Resource) |  |
| Sträng UGCToResourcePath(String ugcPath) | metodsignaturen har ändrats |
| Sträng UGCToResourcePath(String ugcPath, ResourceResolver resolver) | new |

| Metoder i `com.adobe.cq.social.`utilities.resource.api.SocialResourceUtilities | Anteckningar |
|---|---|
| SocialResourceProvider getSocialResourceProvider(Resurs) | ersätter SocialResourceProvider getConfiguringProvider(Resource) |

## SCFUtilities Package {#scfutilities-package}

| Metoder i `com.adobe.cq.social.`utilities.scf.api.SCFUtilites |
|---|
| Sträng getAvatar(UserProperties userProperties) |
| Sträng getAvatar(UserProperties userProperties, int size) |
| Sträng getAvatar(UserProperties userProperties, String absoluteDefaultAvatar) |
| Sträng getAvatar(UserProperties userProperties, String absoluteDefaultAvatar, SocialUtils.AVATAR_SIZE size) |
| Page getContainingPage(Resource resource) |
| Sträng getSocialProfileURL(Stränganvändarnamn, ResourceResolver resolver, Sidsida) |
| UserProperties getUserProperties(ResourceResolver-lösare, String userId) |

## Endast för intern användning {#for-internal-use-only}

| boolesk canAddNode(session, strängsökväg) |
|---|
| Strängen createUniqueNameHint(String message) |
| Strängen createUniqueNameHint(String message, int numRandomChars) |
| Strängen generateRandomString(int length) |
| SocialResourceConfiguration getDefaultStorageConfig() |
| Page getPage(String path, ResourceResolver resolver) |
| Strängen getPagePath(resursen) |
| Sträng getPagePath(Strängsökväg) |
| Sträng getResourceTypeForIncludedResource(Resurskomponent, String defaultResourceType, String designPropertyName) |
| Sträng getResourceTypeFromDesign(resurs, String styleProperty, String defaultValue) |
| boolesk isResourceOwner(Resource resource) |
| SträngmappningUGCPath(Resursresurs) |
| SträngmappningUGCPath(String ugcPath, ResourceResolver resolver) |
| boolesk mayPost(ResourceResolver resolver, Resource resource resource) |
| Strängen prepareUserGeneratedContent(ResourceResolver resolver, String path) |

## Metoder som inte längre är tillgängliga {#methods-no-longer-available}

| Nod createNode(ResourceResolver resolver, String path, String nodeType) |
|---|
| Resurs getResourceAtPath(ResursResolver-lösare, String-sökväg) |
| Resurs getResourceAtPath(ResourceResolver-lösare, String-sökväg, String resourceType) |
| Konfiguration getStorageCloudServiceConfig(resurs) |
| TranslationManager getTranslationManager() |
| TranslationSaveQueue getTranslationSaveQueue() |
| boolesk mayAccessUGC(ResourceResolver-lösare) |
