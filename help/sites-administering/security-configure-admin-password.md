---
title: Konfigurera administratörslösenordet vid installationen
seo-title: Configure the Admin Password on Installation
description: Lär dig hur du ändrar administratörslösenordet vid AEM.
seo-description: Learn how to change the Admin Password on AEM Installation.
uuid: 06da9890-ed63-4fb6-88d5-fd0e16bc4ceb
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: 00806e6e-3578-4caa-bafa-064f200a871f
exl-id: b55ff9d5-8139-4ecf-ba09-5cf88207c5c4
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '305'
ht-degree: 0%

---

# Konfigurera administratörslösenordet vid installationen{#configure-the-admin-password-on-installation}

## Översikt {#overview}

Sedan version 6.3 tillåter AEM att administratörslösenordet anges med kommandoraden när en ny instans installeras.

I tidigare versioner av AEM behövde lösenordet för administratörskontot samt lösenordet för olika andra konsoler ändras efter installationen.

Den här funktionen lägger till möjligheten att ange ett nytt administratörslösenord för databasen och servermotorn under installationen av en AEM, vilket eliminerar behovet av att göra det manuellt efteråt.

>[!CAUTION]
>
>Observera att funktionen inte omfattar Felix Console, där lösenordet måste ändras manuellt. Mer information finns i relevanta [Avsnittet Säkerhetschecklista](/help/sites-administering/security-checklist.md#change-default-passwords-for-the-aem-and-osgi-console-admin-accounts).

## Hur använder jag den? {#how-do-i-use-it}

Den här funktionen aktiveras automatiskt om du väljer att installera AEM via kommandoraden, i stället för att dubbelklicka på JAR från en filsystemutforskare.

Den allmänna syntaxen för att köra en AEM från kommandoraden är:

```shell
java -jar aem6.3.jar
```

När du kör instansen från kommandoraden får du alternativet att ändra administratörslösenordet under installationen:

![chlimage_1-116](assets/chlimage_1-116a.png)

>[!NOTE]
>
>Uppmaningen att ändra administratörslösenordet visas bara under installationen av en ny AEM.

## Använda flaggan -nointeractive {#using-the-nointeractive-flag}

Du kan också välja att ange lösenordet från en egenskapsfil. Detta görs genom att använda `-nointeractive` flagga kombinerat med`-Dadmin.password.file` system, egenskap.

Nedan visas ett exempel:

```shell
java -Dadmin.password.file =/path/to/passwordfile.properties -jar aem6.3.jar -nointeractive
```

Lösenordet i `passwordfile.properties` filen måste ha följande format:

```xml
admin.password = 12345678
```

>[!NOTE]
>
>Om du bara använder `-nointeractive` parametern utan `-Dadmin.password.file` system property, AEM använder administratörslösenordet utan att be dig ändra det, vilket i stort sett replikerar beteendet från tidigare versioner. Det här icke-interaktiva läget kan användas för automatiska installationer med kommandoraden i ett installationsskript.
