---
title: "Mettre à niveau Windows vers la dernière version | Microsoft Docs"
description: "Découvrez comment utiliser le média autonome ou le Centre logiciel dans Configuration Manager pour mettre à niveau un système d’exploitation depuis Windows 7 ou version ultérieure vers Windows 10."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c21eec87-ad1c-4465-8e45-5feb60b92707
caps.latest.revision: 13
author: Dougeby
ms.author: dougeby
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 74341fb60bf9ccbc8822e390bd34f9eda58b4bda
ms.openlocfilehash: 147841212dbb85dd9d4ee7c8a79ca7869584fd99


---
# <a name="upgrade-windows-to-the-latest-version-with-system-center-configuration-manager"></a>Mettre à niveau Windows vers la dernière version avec System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Cette rubrique indique les étapes à suivre dans System Center Configuration Manager pour mettre à niveau un système d’exploitation sur un ordinateur depuis Windows 7 ou version ultérieure vers Windows 10. Vous pouvez choisir parmi différentes méthodes de déploiement, telles qu’un média autonome ou le Centre logiciel. Le scénario de mise à niveau sur place vers Windows 10 :  

-   Met à niveau le système d’exploitation sur les ordinateurs qui exécutent actuellement Windows 7, Windows 8 ou Windows 8.1. Vous pouvez également effectuer des mises à niveau de build à build de Windows 10. Par exemple, vous pouvez mettre à niveau Windows 10 RTM vers Windows 10 version 1511.  

-   Conserve les applications, les paramètres et les données utilisateur sur l’ordinateur.  

-   N’a aucune dépendance externe, telles que Windows ADK.  

-   Est généralement plus rapide et plus fiable que les déploiements de système d’exploitation traditionnels.  

 Suivez les sections ci-dessous pour déployer des systèmes d’exploitation sur le réseau à l’aide d’une séquence de tâches.  

##  <a name="a-namebkmkplana-plan"></a><a name="BKMK_Plan"></a> Plan  

-   **Passer en revue les limitations de la séquence de tâches pour mettre à niveau un système d’exploitation**  

     Passez en revue les exigences et limitations suivantes de la séquence de tâches pour mettre à niveau un système d’exploitation pour vous assurer qu’elle répond à vos besoins :  

    -   Vous devez ajouter uniquement des étapes de séquence de tâches associées à la tâche principale de déploiement de systèmes d’exploitation et de configuration des ordinateurs après l’installation de l’image. Cela comprend les étapes qui installent des packages, des applications ou des mises à jour et celles qui exécutent des lignes de commande, des commandes PowerShell, ou qui définissent des variables dynamiques.  

    -   Passez en revue les pilotes et les applications installés sur les ordinateurs pour vérifier qu’ils sont compatibles avec Windows 10 avant de déployer la séquence de tâches de mise à niveau.  

    -   Les tâches suivantes ne sont pas compatibles avec la mise à niveau sur place et vous obligent à effectuer des déploiements de système d’exploitation classiques :  

        -   Modification de l’appartenance de domaine des ordinateurs ou mise à jour du groupe Administrateurs locaux.  

        -   Implémentation d’une modification fondamentale sur l’ordinateur, y compris un partitionnement de disque, le passage d’une architecture x86 à x64, l’implémentation d’UEFI ou la modification de la langue de base du système d’exploitation.  

        -   Vous avez des besoins personnalisés, notamment l’utilisation d’une image personnalisée de base ou du chiffrement de disque <sup>tiers</sup>, ou vous exigez des opérations hors connexion WinPE.  

-   **Planifier et implémenter la configuration requise pour l’infrastructure**  

     La seule condition préalable pour le scénario de mise à niveau est que vous disposiez d’un point de distribution disponible pour le package de mise à niveau de système d’exploitation et pour les autres packages que vous incluez dans la séquence de tâches. Pour plus d’informations, consultez [Installer ou modifier un point de distribution](../../core/servers/deploy/configure/install-and-configure-distribution-points.md).

##  <a name="a-namebkmkconfigurea-configure"></a><a name="BKMK_Configure"></a> Configurerr  

1.  **Préparer le package de mise à niveau de système d’exploitation**  

     Le package de mise à niveau Windows 10 contient les fichiers sources nécessaires pour mettre à niveau le système d’exploitation sur l’ordinateur de destination. Le package de mise à niveau doit être de la même édition, architecture et langue que les clients que vous mettrez à niveau.  Pour plus d’informations, consultez [Gérer les packages de mise à niveau de système d’exploitation](../get-started/manage-operating-system-upgrade-packages.md).  

2.  **Créer une séquence de tâches pour mettre à niveau le système d’exploitation**  

     Utilisez les étapes indiquées dans [Créer une séquence de tâches pour mettre à niveau un système d’exploitation](create-a-task-sequence-to-upgrade-an-operating-system.md) pour automatiser la mise à niveau du système d’exploitation.  

    > [!NOTE]  
    >  En général, vous utiliserez les étapes indiquées dans [Créer une séquence de tâches pour mettre à niveau un système d’exploitation](create-a-task-sequence-to-upgrade-an-operating-system.md) pour créer une séquence de tâches pour mettre à niveau un système d’exploitation Windows 10. La séquence de tâches comprend l’étape Mettre à niveau le système d’exploitation, ainsi que d’autres groupes et étapes recommandés pour gérer le processus de mise à niveau de bout en bout. Toutefois, vous pouvez créer une séquence de tâches personnalisée et ajouter l’étape de séquence de tâches [Mettre à niveau le système d’exploitation](../understand/task-sequence-steps.md#BKMK_UpgradeOS) pour mettre à niveau le système d’exploitation. Il s’agit de la seule étape requise pour mettre à niveau le système d’exploitation vers Windows 10. Si vous choisissez cette méthode, ajoutez également l’étape [Redémarrer l’ordinateur](../understand/task-sequence-steps.md#a-namebkmkrestartcomputera-restart-computer) après l’étape Mettre à niveau le système d’exploitation pour terminer la mise à niveau. Veillez à activer le paramètre **Le système d’exploitation par défaut installé actuellement** pour redémarrer l’ordinateur dans le système d’exploitation installé, et non dans Windows PE.  

##  <a name="a-namebkmkdeploya-deploy"></a><a name="BKMK_Deploy"></a> Déployer  

-   Pour déployer le système d’exploitation, appliquez l’une des méthodes de déploiement suivantes :  

    -   [Utiliser le Centre logiciel pour déployer Windows sur le réseau](use-software-center-to-deploy-windows-over-the-network.md)  

    -   [Utiliser un média autonome pour déployer Windows sans utiliser le réseau](use-stand-alone-media-to-deploy-windows-without-using-the-network.md)  

## <a name="monitor"></a>Analyse  

-   **Surveiller le déploiement de la séquence de tâches**  

     Pour surveiller le déploiement de la séquence de tâches permettant de mettre à niveau le système d’exploitation, consultez [Surveiller les déploiements de système d’exploitation](monitor-operating-system-deployments.md).  



<!--HONumber=Dec16_HO3-->


