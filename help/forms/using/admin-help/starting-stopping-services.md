---
title: Starta och stoppa tjänster
seo-title: Starta och stoppa tjänster
description: Lär dig hur du startar och stoppar tjänster som är kopplade till AEM Forms-modulerna samt programservern och databasen.
seo-description: Lär dig hur du startar och stoppar tjänster som är kopplade till AEM Forms-modulerna samt programservern och databasen.
uuid: 8c831cb2-4165-4118-8a09-764cec4e5e05
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_services
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: b93060bd-c6e1-40d2-8acd-ccafb8ed56da
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Starta och stoppa tjänster {#starting-and-stopping-services}

Det finns två typer av tjänster som ingår i AEM-formulär:

* Tjänster som styr AEM-formulärens programserver och databas.
* Tjänster som styr AEM-formulärmoduler

## Starta eller stoppa tjänster som är kopplade till AEM-formulärmoduler {#start-or-stop-the-services-associated-with-aem-forms-modules}

AEM-formulärmoduler (till exempel Forms, Rights Management, Output) fungerar som tjänster. Ibland kan du behöva stoppa eller starta tjänsterna för dessa AEM-formulärmoduler. Du måste till exempel stoppa och sedan starta om en AEM-formulärtjänst när du har ändrat en inställning för tjänsten.

1. I administrationskonsolen klickar du på **Tjänster** > **Program och tjänster** > **Tjänsthantering**.
1. Markera kryssrutan bredvid tjänsten som ska stoppas eller startas på sidan Tjänsthantering och klicka på Stopp eller Start.

## Starta eller stoppa tjänster för programservern och databasen {#start-or-stop-services-for-the-application-server-and-database}

En komplett implementering av AEM-formulär innefattar en programserver och databastjänster:

* *`[application server]`* för AEM-formulär
* *`[database]`* för AEM-formulär

I Windows är dessa tjänster tillgängliga via **Administrationsverktyg** > **Tjänster**. Om du t.ex. har installerat AEM-formulär på JBoss med körningsmetoden är följande tjänster tillgängliga på datorn:

* JBoss för Adobe Experience Manager-formulär
* MySQL för Adobe Experience Manager-formulär

Starta eller stoppa dessa tjänster genom att markera dem i listan på panelen Tjänster och sedan klicka på lämplig åtgärdsknapp på panelen.

I UNIX® eller Linux anger du följande text från en kommandorad, där *`[service name]`* är namnet på den tjänst du verifierar:

```as3
     ps -A | grep [service name]
```

