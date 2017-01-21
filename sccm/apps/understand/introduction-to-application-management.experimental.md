---
title: "Présentation de la gestion d’applications | System Center Configuration Manager"
description: "Découvrez les informations de base dont vous aurez besoin pour gérer et déployer des applications System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-app
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 08f711ba-83bf-4b5f-9520-a0778c6ae7eb
caps.latest.revision: 18
author: robstackmsft
ms.author: robstack
manager: angrobe
experimental: true
experiment_id: rob-table-161101
translationtype: Human Translation
ms.sourcegitcommit: aa985dcb947803f7bc6d770f80a89a2fe6750681
ms.openlocfilehash: bec4d6d7008d5eabc7219dc7aaa1198c6e68a4df


---
# <a name="introduction-to-application-management-in-system-center-configuration-manager"></a>Présentation de la gestion d’applications dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Dans cette rubrique, vous allez découvrir les principes de base à connaître avant de commencer à utiliser des applications System Center Configuration Manager.  

> [!TIP]  
>  Si vous savez déjà comment gérer des applications dans Configuration Manager, vous pouvez ignorer cette rubrique et passer directement à la création d’un exemple d’application. Consultez [Créer et déployer une application avec System Center Configuration Manager](../../apps/get-started/create-and-deploy-an-application.md).  

## <a name="what-is-an-application"></a>Qu’est-ce qu’une application ?  
 Bien que le terme « application » soit couramment utilisé en informatique, il a une signification particulière dans Configuration Manager. Comparez plutôt une application à une boîte. Cette boîte contient un ou plusieurs jeux de fichiers d’installation pour un package logiciel (appelé **type de déploiement**), ainsi que des instructions sur la façon de déployer le logiciel.  

 Quand l’application est déployée sur des appareils, des **spécifications** déterminent le type de déploiement qui est installé sur l’appareil.  

 Bien sûr, une application permet d’effectuer bien d’autres choses que nous passerons en revue dans ce guide. La liste suivante présente les concepts que vous devez connaître avant d’aller plus loin. Notez que vous n’aurez pas forcément recours à tous ces concepts dans chaque application que vous créez :  



- **Spécifications** Dans les versions précédentes de Configuration Manager, il était fréquent de créer un regroupement contenant les appareils sur lesquels vous souhaitiez déployer une application. Bien que vous puissiez toujours procéder de cette façon, vous pouvez désormais utiliser des spécifications pour indiquer des critères d’installation plus granulaires.<br> Par exemple, vous pouvez préciser qu’une application peut uniquement être installée sur des appareils Windows 10. Vous pouvez ensuite déployer l’application sur tous vos appareils, mais elle ne sera installée que sur les appareils Windows 10.<br> Configuration Manager évalue les spécifications pour déterminer si une application et ses types de déploiement doivent être installés. Ensuite, il détermine le type de déploiement correct selon lequel installer une application. Tous les sept jours, par défaut, les règles de spécification sont réévaluées pour garantir leur conformité en fonction du paramètre client **Planifier la réévaluation des déploiements**.<br> Pour plus d’informations, consultez [Créer et déployer une application](../../apps/get-started/create-and-deploy-an-application.md). 


- **Conditions globales** Si les spécifications s’appliquent à un type de déploiement spécifique dans une application unique, vous pouvez également créer des conditions globales, c’est-à-dire une bibliothèque de spécifications prédéfinies que vous pouvez utiliser avec n’importe quelle application et n’importe quel type de déploiement.<br> Configuration Manager contient un jeu de conditions globales intégrées, mais vous pouvez également créer vos propres conditions globales.<br> Pour plus d’informations, consultez [Créer des conditions globales](../../apps/deploy-use/create-global-conditions.md).


- **Déploiement simulé** Évalue les spécifications, la méthode de détection et les dépendances d’une application, puis signale les résultats sans réellement installer l’application.<br> Pour plus d’informations, consultez [Simuler des déploiements d’applications](../../apps/deploy-use/simulate-application-deployments.md). 


- **Action de déploiement** Spécifie si vous souhaitez installer ou désinstaller (en cas de prise en charge) l’application que vous déployez.<br> Pour plus d’informations, consultez [Déployer des applications](../../apps/deploy-use/deploy-applications.md).  


- **Objet du déploiement** Spécifie si l’application de déploiement est **Obligatoire** ou **Disponible**.<br>
**Obligatoire** signifie que l’application est déployée automatiquement selon le calendrier configuré. Un utilisateur peut toutefois suivre l'état du déploiement de l'application (s'il n'est pas masqué) et installer l'application avant l'échéance, à l'aide du Centre logiciel.<br> **Disponible** signifie que si l’application est déployée sur un utilisateur, celui-ci peut voir l’application publiée dans le Centre logiciel et la demander au besoin.<br> Pour plus d’informations, consultez [Déployer des applications](../../apps/deploy-use/deploy-applications.md).


- **Révisions** Quand vous apportez des modifications à une application ou à un type de déploiement contenu dans une application, Configuration Manager crée une nouvelle révision de l’application. Vous pouvez afficher l’historique de chaque révision de l’application, afficher ses propriétés, restaurer une révision précédente d’une application ou supprimer une ancienne révision.<br> Pour plus d’informations, consultez [Mettre à jour et mettre hors service des applications](../../apps/deploy-use/update-and-retire-applications.md).


- **Méthode de détection** Les méthodes de détection permettent de détecter si une application déployée est déjà installée. Si la méthode de détection indique que l’application est installée, Configuration Manager n’essaie pas de la réinstaller.<br> Pour plus d’informations, consultez [Créer des applications](../../apps/deploy-use/create-applications.md). 


- **Dépendances** Les dépendances définissent un ou plusieurs types de déploiement d’un autre type d’application qui doivent être installés avant l’installation d’un type de déploiement. Vous pouvez configurer les types de déploiement dépendants à installer automatiquement avant l'installation du type de déploiement.<br> Pour plus d’informations, consultez [Créer des applications](../../apps/deploy-use/create-applications.md).  


- **Remplacement** Configuration Manager vous permet de mettre à niveau ou de remplacer des applications existantes par le biais d’une relation de remplacement. Lorsque vous remplacez une application, vous pouvez spécifier un nouveau type de déploiement qui remplacera le type de déploiement de l'application remplacée. Vous pouvez aussi indiquer si vous souhaitez mettre à niveau ou désinstaller l'application remplacée avant l'installation de l'application de remplacement.<br> Pour plus d’informations, consultez [Créer des applications](../../apps/deploy-use/create-applications.md).


- **Gestion centrée sur l’utilisateur** Les applications Configuration Manager prennent en charge la gestion centrée sur l’utilisateur, ce qui vous permet d’associer des utilisateurs spécifiques à des appareils spécifiques. Au lieu de mémoriser le nom de l’appareil d’un utilisateur, vous pouvez déployer des applications sur l’utilisateur et l’appareil. Cette fonctionnalité permet de veiller à ce que les applications les plus importantes soient toujours disponibles sur chaque appareil auquel accède un utilisateur spécifique. Si un utilisateur acquiert un nouvel ordinateur, vous pouvez installer automatiquement les applications de l’utilisateur sur l’appareil avant qu’il n’ouvre une session.<br> Pour plus d’informations, consultez [Lier des utilisateurs et des appareils avec l’affinité entre utilisateur et appareil](../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md).  

## <a name="what-application-types-can-you-deploy"></a>Quels types d’applications pouvez-vous déployer ?  
 Configuration Manager vous permet de déployer les types d’application suivants :  

- Windows Installer (fichier *.msi)
- Package d’application Windows (*.appx, \*.appxbundle)
- Package d'application Windows (dans le Windows Store)
- Microsoft Application Virtualization 4
- Microsoft Application Virtualization 5
- Fichier CAB Windows Mobile
- Mac OS X  


De plus, quand vous gérez des appareils par le biais de la gestion des appareils locaux Microsoft Intune ou Configuration Manager, vous pouvez gérer ces types d’application supplémentaires :

- Package d'application Windows Phone (fichier *.xap)
- Package d'application pour iOS (fichier *.ipa)
- Package d'application pour Android (fichier *.apk)
- Package d'application pour Android sur Google Play
- Package d'application Windows Phone (dans Windows Phone Store)
- Windows Installer par le biais de la gestion des appareils mobiles
- Application Web



## <a name="state-based-applications"></a>Applications basées sur l’état  
 Les applications Configuration Manager utilisent la surveillance basée sur l’état, ce qui vous permet de suivre le dernier état du déploiement d’application pour les utilisateurs et les appareils. Les messages d'état affichent des informations concernant des appareils individuels. Par exemple, si une application est déployée sur un regroupement d’utilisateurs, vous pouvez voir l’état de compatibilité du déploiement ainsi que son objet dans la console Configuration Manager. Vous pouvez surveiller le déploiement de tous vos logiciels à l’aide de l’espace de travail **Surveillance** dans la console Configuration Manager. Les déploiements de logiciels incluent des mises à jour logicielles, des paramètres de compatibilité, des applications, des séquences de tâches, des packages et des programmes. Pour plus d’informations, consultez [Surveiller des applications](/sccm/apps/deploy-use/monitor-applications-from-the-console).  

 Les déploiements d’applications sont régulièrement réévalués par Configuration Manager. Exemple :  

-   Une application déployée est désinstallée par l'utilisateur final. Au prochain cycle d’évaluation, Configuration Manager détecte que l’application n’est pas présente et la réinstalle.  

-   Une application n'a pas été installée sur un appareil, car elle n'a pas satisfait à la configuration requise. Plus tard, une modification est apportée à l'appareil pour qu'il soit conforme à la configuration requise. Configuration Manager détecte cette modification et l’application est installée.  

 Vous pouvez configurer l'intervalle de réévaluation des déploiements d'applications à l'aide du paramètre client **Planifier la réévaluation des déploiements** . Pour plus d’informations, consultez [À propos des paramètres client](../../core/clients/deploy/about-client-settings.md).  

## <a name="get-started-creating-an-application"></a>Prendre en main la création d’une application  
 Si vous souhaitez vous lancer et commencer à créer une application, consultez la procédure pas à pas de la rubrique [Créer et déployer une application](../../apps/get-started/create-and-deploy-an-application.md) pour créer une application simple.  

 Si vous connaissez déjà les principes de base et que vous recherchez des informations de référence plus approfondies sur les options disponibles, commencez par la rubrique [Créer des applications](/sccm/apps/deploy-use/create-applications).  

## <a name="software-center-and-the-application-catalog"></a>Centre logiciel et catalogue des applications  
 Dans les versions précédentes de Configuration Manager, le Centre logiciel servait à installer et à planifier les installations de logiciels, à configurer les paramètres de contrôle à distance et à configurer les paramètres de gestion de l’alimentation. Les utilisateurs pouvaient se connecter au catalogue des applications pour rechercher et demander des logiciels, configurer certains paramètres de préférence et réinitialiser à distance leurs appareils mobiles.  

 Bien que ces paramètres soient toujours disponibles dans System Center Configuration Manager, une nouvelle version du Centre logiciel est désormais disponible. Elle vous permet de rechercher des applications sans avoir à utiliser le catalogue des applications, qui nécessite un navigateur web compatible avec Silverlight. Toutefois, les rôles de système de site Point du site web du catalogue des applications et Point de service web du catalogue des applications sont toujours nécessaires pour que les applications accessibles à l’utilisateur apparaissent dans le Centre logiciel.  

 Pour plus d’informations, consultez [Planifier et configurer la gestion des applications](../../apps/plan-design/plan-for-and-configure-application-management.md).  

## <a name="using-configuration-manager-packages-and-programs"></a>Utilisation de packages et de programmes Configuration Manager  
 Configuration Manager continue de prendre en charge les packages et les programmes utilisés dans les versions précédentes du produit. Un déploiement qui utilise des packages et des programmes peut être plus adapté qu’un déploiement qui utilise une application lors du déploiement de l’un des éléments suivants :  

-   des scripts n’installant pas d’application sur un ordinateur, tel qu’un script pour défragmenter le lecteur de l’ordinateur ;  

-   des scripts exceptionnels qui ne doivent pas être surveillés en permanence ;  

-   des scripts qui s’exécutent selon un planning défini et qui ne peuvent pas utiliser l’évaluation globale.  

 Pour plus d’informations, consultez [Packages et programmes](../../apps/deploy-use/packages-and-programs.md).  




<!--HONumber=Dec16_HO3-->


