---
title: Omfaktorisering för SocialUtils
seo-title: Omfaktorisering för SocialUtils
description: Paketet com.adobe.cq.social.ugcbase.SocialUtils har tagits bort i AEM 6.1
seo-description: Paketet com.adobe.cq.social.ugcbase.SocialUtils har tagits bort i AEM 6.1
uuid: 54a0d98e-5ead-4c12-850f-8252ea9b3263
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 4ade0d6b-041e-4a2f-98f8-3b8fcae0fb29
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Omfaktorisering för SocialUtils {#socialutils-refactoring}

## Paketet SocialUtils har tagits bort {#socialutils-package-deprecated}

Paketet **com.adobe.cq.social.ugcbase.SocialUtils** har tagits bort i AEM 6.1.

I följande tabell visas de metoder som ska användas i stället för SocialUtils-metoder.

## Paket för SocialResourceUtilities {#socialresourceutilities-package}

| Metoder i com.adobe.cq.social.srp.utilities.api.SocialResourceUtilities |
|---|
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

| Metoder i `com.adobe.cq.social.`utilities.resource.api.SocialResourceUtilities |
|---|
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

