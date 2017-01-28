---
title: "Présentation de Long-Term Servicing Branch | Microsoft Docs"
description: "Découvrez Long-Term Servicing Branch dans System Center Configuration Manager."
ms.custom: na
ms.date: 1/7/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 694bc29f-a7fd-4e06-815a-1a9c5e9ac563
caps.latest.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: a86546eb513a2ef6f95013178b141fb1833ea8ab
ms.openlocfilehash: fa4d7dd2e1edbbc0b136ebfc27560f20ab63c12e


---
# <a name="introduction-to-the-long-term-servicing-branch-of-system-center-configuration-manager"></a>Présentation de Long-Term Servicing Branch dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Long-Term Servicing Branch)*

Utilisez cette rubrique pour découvrir la branche LTSB (Long-Term Servicing Branch) de Configuration Manager et comprendre sa documentation.


LTSB est une branche distincte de Configuration Manager qui se base sur la version 1606 de Current Branch. Par rapport à Current Branch, LTSB a des [fonctionnalités réduites](#features-that-are-not-available-in-the-ltsb-of-configuration-manager). Cette branche est conçue pour les clients qui ont [autorisé l’expiration de leur contrat Software Assurance (SA) ou de droits d’abonnement équivalents](/sccm/core/understand/learn-more-editions#software-assurance-and-the-ltsb).

**Vue d’ensemble des licences :**   
Les clients qui ont un contrat Software Assurance (SA) sur les licences de System Center Configuration Manager ou qui ont des droits d’abonnement équivalents à la date du 1er octobre 2016 ont le droit d’utiliser la version 1606 d’octobre 2016 de System Center Configuration Manager. Les clients qui ont des droits pour System Center Configuration Manager au 1er octobre 2016 ou après cette date ont deux options de licence lors de l’installation : CB (Current Branch) et LTSB (Long-Term Servicing Branch).

**Spécificités des licences :**  
[Les conditions générales des produits que vous achetez par le biais des programmes de licence en volume Microsoft se trouvent ici](http://go.microsoft.com/fwlink/?LinkId=800052).

Les clients dotés de droits perpétuels sur System Center Configuration Manager, ou qui laissent leur contrat SA ou leur abonnement expirer après le 1er octobre, peuvent installer la version LTSB de System Center Configuration Manager qui est en vigueur au moment de l’expiration.
- Pour plus d’informations sur Software Assurance et les exigences en matière de licence pour System Center Configuration Manager, consultez [Licences et branches pour System Center Configuration Manager](learn-more-editions.md).
-   Pour plus d’informations sur les différences entre les différentes branches, consultez [Déterminer la branche de Configuration manager à utiliser](which-branch-should-i-use.md).

Pour installer un nouveau site ou mettre à niveau un site System Center 2012 Configuration Manager vers LTSB, vous utilisez le support de la base de référence de la version 1606. Ce média de base est disponible sous forme de DVD dans le cadre de Microsoft System Center 2016 ou de System Center Configuration Manager (Current Branch et Long-Term Servicing Branch 1606). Le support de la base de référence qui peut installer LTSB permet également d’installer la version Current Branch 1606 de Configuration Manager. Pour en savoir plus sur le support de la base de référence, consultez [Versions de base et de mise à jour](/sccm/core/servers/manage/updates#baseline-and-update-versions).

Pour plus d’informations sur la façon d’installer un site LTSB, consultez [Installer et mettre à niveau Long-Term Servicing Branch](install-the-ltsb.md). Consultez la [documentation de System Center 2016](https:\technet.microsoft.com\system-center-docs\System-Center-2016) pour plus d’informations sur l’obtention de System Center 2016.

> [!IMPORTANT]
> Tous les sites d’une hiérarchie doivent exécuter la même branche. Une hiérarchie ne peut pas comporter un mélange de LTSB et Current Branch sur des sites différents.
>
> De même, quand vous utilisez la récupération, vous devez récupérer le site ou la base de données de site dans sa branche d’origine. Vous ne pouvez pas récupérer une base de données de site Current Branch sur une installation LTSB, et vice versa.


## <a name="features-that-are-not-available-in-the-ltsb-of-configuration-manager"></a>Fonctionnalités non disponibles dans la branche LTSB de Configuration Manager
Par rapport à Current Branch, les limites de prise en charge de LTSB sont les suivantes :

- Elle ne reçoit pas de mises à jour pour les nouvelles fonctionnalités.
- Elle ne prend pas en charge l’ajout d’un abonnement Microsoft Intune, ce qui vous empêche d’utiliser :
  - Intune dans une configuration hybride de gestion des appareils mobiles
  - Gestion des appareils mobiles locale
-   Elle ne prend pas en charge l’utilisation des plans de maintenance ni du tableau de bord de maintenance de Windows 10. Elle ne prend pas non plus en charge la branche CB (Current Branch) et la branche CBB (Current Branch for Business) de Windows 10.
- Elle ne prend pas en charge les futures versions de Windows 10 LTSB ni de Windows Server.
-   Elle ne prend pas en charge Asset Intelligence.
-   Elle ne prend pas en charge les points de distribution cloud.
-   Elle ne prend pas en charge Exchange Online comme connecteur Exchange.
-   Elle ne prend en charge aucune fonctionnalité de la version préliminaire.


Bien que la prise en charge de ces fonctionnalités ne soit pas incluse dans LTSB, certaines restent visibles dans la console Configuration Manager, mais ne peuvent pas être sélectionnées ou utilisées.

De plus, les nouveaux systèmes d’exploitation ajoutés car pris en charge par Current Branch ne sont pas pris en charge par LTSB.

## <a name="documentation-for-the-ltsb"></a>Documentation de LTSB
LTSB étant basé sur la version 1606 de Current Branch, la documentation que vous utilisez pour LTSB est la [documentation en ligne applicable à Current Branch](https://docs.microsoft.com/sccm/), avec les mises en garde et limitations propres à LTSB, comme indiqué dans les rubriques suivantes :  

-   [Présentation de Long-Term Servicing Branch](introduction-to-the-ltsb.md) : (cette rubrique).

-   [Déterminer la branche de Configuration manager à utiliser](which-branch-should-i-use.md) : informations sur les différentes branches de System Center Configuration Manager, pour vous permettre d’installer celle qui répond le mieux à vos besoins.

-   [Installer Long-Term Servicing Branch](install-the-ltsb.md) : guide pratique pour installer un nouveau site LTSB ou mettre à niveau un site System Center 2012 Configuration Manager vers LTSB.

-   [Mettre à niveau Long-Term Servicing Branch vers Current Branch](convert-to-current-branch.md) : guide pratique pour convertir votre installation LTSB en installation Current Branch.

-   [Licences et branches pour System Center Configuration Manager](learn-more-editions.md) : informations sur Software Assurance et les exigences en matière de licence pour System Center Configuration Manager.
-   [Configurations prises en charge pour Long-Term Servicing Branch](supported-configurations-for-ltsb.md) : versions et configuration requise pour le système d’exploitation et les produits dépendants, comme SQL Server, que vous pouvez utiliser avec LTSB.


Pour déterminer à quelle branche une documentation spécifique s’applique, utilisez les repères suivants :  
-   Les rubriques comportant un en-tête *S’applique à : Current Branch* s’appliquent à la fois à Current Branch et à Long-Term Servicing Branch (même si certaines parties des rubriques s’appliquent uniquement à une version plus récente de Current Branch).

-   Pour identifier les parties d’une rubrique qui ne s’appliquent pas à LTSB, les fonctionnalités et modifications introduites après la version 1606 de Current Branch sont identifiées avec un libellé de type *À partir de la version 1610*. Celles-ci ayant été introduites après la version 1606 de Current Branch, elles ne sont pas disponibles avec LTSB.

### <a name="similarities-between-the-current-branch-and-the-ltsb"></a>Similitudes entre les branches Current Branch et LTSB
Étant donné que LTSB est basé sur la version 1606 de Current Branch (avec quelques exceptions comme l’intégration d’Intune et certaines fonctionnalités cloud), la plupart des tâches utilisées pour la planification du déploiement, de la configuration et de la gestion des deux branches sont identiques.

Par exemple, LTSB prend en charge les mêmes nombre de sites, types de site, clients et infrastructure générale que Current Branch. Ainsi, vous utilisez les instructions figurant dans les rubriques sur la planification et la conception de sites et de hiérarchies pour Current Branch. De même, pour les fonctionnalités prises en charge par les deux branches, comme les mises à jour logicielles ou le déploiement de système d’exploitation, vous utilisez les instructions figurant dans les sections de la documentation Current Branch en tenant compte des mises en garde liées au non-accès aux modifications introduites après la version 1606 de Current Branch.


## <a name="how-to-identify-your-branch-and-version"></a>Guide pratique pour identifier votre branche et votre version
Quand vous affichez les informations de version d’un site Configuration Manager, vous vérifiez également la branche.

Pour vérifier la version de votre site, dans la console, accédez à **À propos de System Center Configuration Manager** dans le coin supérieur gauche de la console, où **Version du site** indique **5.0.8412.1000**.

Pour vérifier la branche de votre site (LTSB ou Current Branch), dans la console, accédez à **Administration** > **Configuration du Site** > **Sites**, puis ouvrez **Paramètres de hiérarchie**.  Si vous voyez une option de conversion en Current Branch et si elle est active, le site exécute la version LTSB. Si le site exécute Current Branch, cette option est grisée.

Pour plus d’informations sur les différentes versions de Configuration Manager, consultez « Versions de base et de mise à jour » dans la rubrique [Mises à jour pour Configuration Manager](/sccm/core/servers/manage/updates).

## <a name="exceptions-for-using-the-ltsb"></a>Exceptions liées à l’utilisation de LTSB
### <a name="updates-and-servicing-of-the-ltsb"></a>Mises à jour et maintenance de LTSB
Seules les mises à jour de sécurité critiques sont disponibles en tant que mises à jour dans la console dans LTSB.

Les informations sur les mises à jour régulières des versions Current Branch ultérieures sont visibles dans la console, mais elles ne sont pas disponibles dans LTSB. Elles ne sont pas téléchargées et ne peuvent pas être installées.

Pour prendre en charge les mises à jour dans la console pour les correctifs de sécurité critiques, un site LTSB a besoin d’utiliser [le point de connexion de service](/sccm/core/servers/deploy/configure/about-the-service-connection-point). Vous pouvez configurer ce rôle de système de site en mode hors connexion ou en ligne, comme pour Current Branch. LTSB collecte et envoie les mêmes données de télémétrie et d’utilisation que Current Branch.

LTSB prend en charge l’utilisation du programme d’installation de correctif logiciel et de l’outil Inscription de la mise à jour, comme indiqué pour Current Branch.

Pour obtenir des informations générales sur les mises à jour et la maintenance, consultez [Mises à jour pour Configuration Manager](/sccm/core/servers/manage/updates).

### <a name="changes-for-site-expansion-and-the-cdlatest-folder"></a>Modifications liées au développement de site et au dossier CD.Latest
Quand vous exécutez LTSB et que vous développez un site principal autonome en installant un nouveau site d’administration centrale, vous devez utiliser le programme d’installation et les fichiers sources du support de la base de référence de la version 1606.  Pour Current Branch, vous exécutez le programme d’installation et vous utilisez les fichiers sources du dossier CD.Latest.

Bien que vous n’exécutiez pas le programme d’installation pour le développement de site à partir du dossier CD.Latest, vous continuez d’utiliser ce dossier pour la récupération de site et pour installer un nouveau site principal enfant si votre premier site LTSB était un site d’administration centrale.

Pour plus d’informations sur le développement de site, consultez [Étendre un site principal autonome](/sccm/core/servers/deploy/install/use-the-setup-wizard-to-install-sites#expand-a-stand-alone-primary-site) dans [Utiliser l’Assistant Installation pour installer des sites](/sccm/core/servers/deploy/install/use-the-setup-wizard-to-install-sites).
Pour plus d’informations sur le dossier CD.Latest, consultez [Dossier CD.Latest](/sccm/core/servers/manage/the-cd.latest-folder).



<!--HONumber=Jan17_HO2-->


