---
title: 'Ytterligare steg för att hämta e-post med bifogad fil '
description: 'Ytterligare steg för att hämta e-post med bifogad fil   '
source-git-commit: 9ee8e79777b89fbf4d6e5b5fd1dbb1ef3bc9ad5d
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 0%

---

# Det går inte att hämta e-post med bilagor för AEM Forms på JEE-plattformar{#unable-to-get-email-with-attachments}

Problemet gäller följande version:
* Experience Manager 6.5 Forms

## Problem {#issue}

Användaren kan inte utföra åtgärder som Skicka PDF via e-post eller Inkludera bilagor med inskickningskonfiguration.

## Lösning {#solution}

1. Ladda ned jar som [java.mail-1.0.jar](/help/forms/using/java.mail-1.0.jar) och packa upp den hämtade burkfilen för att få fram manifestfilen.

1. Använd manifestfilen för `java.mail-1.0.jar` som hämtats från steg 1 för att skapa en ny egen jar-fil som `java.mail-1.5.jar`.

1. Öppna manifestfilen och ersätt alla förekomster av `1.5.0` med `1.5.6` och `Bundle-Version: 1.0` med `Bundle-Version:1.5`

1. Skapa en ny egen burk (`java.mail-1.5.jar`) med hjälp av följande kommando i `C:\Adobe\Adobe_Experience_Manager_Forms\java\jdk\bin` mapp som:
   `jar -cfm java.mail-1.5.jar manifest.mf`

   I ovanstående kommando *manifest.mf* är namnet på manifestfilen och *java.mail-1.5.jar* är namnet på den fil som skulle skapas när ovanstående kommando kördes.

1. Hämta [javax.mail-1.5.6.redhat-1.jar](https://mvnrepository.com/artifact/com.sun.mail/javax.mail/1.5.6.redhat-1).

1. Navigera till `http://<server name>:<port>/lc/system/console/bundles`och ta bort paketet med ett namn som `JavaMail API (com.sun.mail.javax.mail) version 1.6.2`.

1. Installera `java.mail-1.5.jar` som erhållits från steg 3.  Det här steget startar om slingegenskaperna för JEE-distributionen. Vänta på de installerade paketen på `http://<server name>:<port>/lc/system/console/bundles` för att visa status som **Aktiv**.

   >Obs! Om statusen fortfarande är **InActive** starta om   **JBoss** från **Services Console**.


1. Installera `javax.mail-1.5.6.redhat-1.jar`filen laddades ned i steg 5.

1. Stoppa **JBoss** från **Services Console** och lägg till följande egenskaper i **Sling.properties** fil:
   * `org.osgi.framework.system.packages.extra=javax.activation; version\=1.2.0`
   * `sling.bootdelegation.activation=javax.activation.*`

1. Starta om **JBoss**.