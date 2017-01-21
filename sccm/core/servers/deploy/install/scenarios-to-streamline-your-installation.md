---
title: "Scénarios d’installation | System Center Configuration Manager"
description: "Découvrez des techniques d’installation d’une nouvelle hiérarchie Configuration Manager lors d’une mise à jour ou d’une mise à niveau."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 35586a85-4af9-4c8b-925a-0e32dc8b7346
caps.latest.revision: 6
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 90a802cbdfd6d0acd60ec462ffbf2a08c012eaeb


---
# <a name="scenarios-to-streamline-your-installation-of-system-center-configuration-manager"></a>Scénarios pour simplifier votre installation de System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Avec la publication des versions de mise à jour pour la branche Current Branch de System Center Configuration Manager, de nouveaux scénarios sont apparus pour simplifier l’installation d’une nouvelle hiérarchie sur une version de mise à jour (par exemple, la mise à jour 1602), et pour opérer une mise à niveau à partir de Microsoft System Center 2012 Configuration Manager.  

Les scénarios pris en charge sont les suivants :  

**Installer une nouvelle hiérarchie de branche Current Branch System Center Configuration Manager** exécutant une version de mise à jour :  

-   Vous installez uniquement le site de niveau supérieur puis, immédiatement après, mettez celui-ci à jour vers la version que vous voulez utiliser. Vous pouvez ensuite installer des sites supplémentaires directement sur cette version de mise à jour.  

-   Ce scénario évite de devoir installer les sites supplémentaires à un niveau de référence, puis les mettre à jour vers la version de mise à jour que vous voulez utiliser.  

-   Ce scénario évite de devoir installer les sites supplémentaires sur une version de référence, puis les réinstaller lorsque vous mettez à jour vers une version ultérieure.  

**Mettre à niveau l’infrastructure System Center 2012 Configuration Manager** vers une version de mise à jour de System Center Configuration Manager :  

-   Vous mettez à niveau manuellement votre site d’administration centrale et chaque site principal vers une version de référence (par exemple, 1511) avant d’installer une version de mise à jour (par exemple, 1602).  

-   Vous ne mettez pas à niveau les sites secondaires à partir de Microsoft System Center 2012 Configuration Manager tant que vos sites principaux n’exécutent pas la version de mise à jour que vous voulez utiliser.  

-   Vous ne mettez pas à niveau les clients Microsoft System Center 2012 Configuration Manager tant que vos sites principaux n’exécutent pas la version de mise à jour que vous voulez utiliser.  

## <a name="scenario---install-a-new-hierarchy-to-an-update-version"></a>Scénario - Installer une nouvelle hiérarchie sur une version de mise à jour  
Dans cet exemple de scénario, vous installez le premier site d’une hiérarchie à l’aide d’une version de référence de System Center Configuration Manager, à savoir la version 1511. Ensuite, vous installez la mise à jour 1602 avant de déployer des sites ou clients supplémentaires.  

-   Étant donné que vous prévoyez d’utiliser une version de mise à jour (par exemple, 1602) et de ne pas en rester à la version de référence (par exemple, 1511), il est inutile d’installer puis de mettre à niveau des sites supplémentaires ou des clients.  

-   Vous n’installez pas de sites secondaires avec la version 1511 avant de les mettre à niveau vers la version 1602. Au lieu de cela, vous les installez une fois que vos sites principaux exécutent la version 1602.  

**Utilisez la séquence suivante :**  

1.  **Installez un site de niveau supérieur pour votre nouvelle hiérarchie** à l’aide du support de référence.  

    -   Vous pouvez utiliser un support de référence uniquement pour installer le premier site d’une nouvelle hiérarchie.  

    -   Par exemple, installez un site de niveau supérieur à l’aide de la version de référence 1511. Voir [Utiliser l’Assistant Installation pour installer des sites](/sccm/core/servers/deploy/install/use-the-setup-wizard-to-install-sites).  

    Après cette étape, votre site de niveau supérieur exécute la version 1511.  

2.  **Utilisez des mises à jour dans la console pour mettre à jour votre site de niveau supérieur vers une version ultérieure.**  

    -   Avant d’installer des sites enfants ou clients, mettez à jour votre site de niveau supérieur vers la version de mise à jour que vous prévoyez d’utiliser.  

    -   Par exemple, vous pouvez mettre à jour votre site de niveau supérieur exécutant la version 1511 vers la version 1602. Consultez [Mises à jour pour System Center Configuration Manager](../../../../core/servers/manage/updates.md).  

    Après cette étape, votre site de niveau supérieur exécute la version 1602.  

3.  **Installez les nouveaux sites principaux enfants sous un site d’administration centrale.**  

    -   Utilisez le support d’installation du dossier CD.Latest sur le serveur du site d’administration centrale pour installer les sites principaux enfants.  (Voir [Le dossier CD.Latest pour System Center Configuration Manager](../../../../core/servers/manage/the-cd.latest-folder.md).)  

        -   Ce support de source d’installation est requis pour s’assurer que la version des nouveaux sites principaux enfants corresponde à celle du site d’administration centrale.  

    Après cette étape, vos nouveaux sites principaux enfants exécutent la version 1602.  

4.  **Au niveau de chaque site principal, utilisez l’option d’installation dans la console pour installer de nouveaux sites secondaires.**  

    -   Étant donné que vous n’avez pas installé de sites secondaires quand les sites principaux en étaient au niveau de la version 1511, vous n’avez pas besoin de mettre à niveau des sites secondaires.  

    -   Au lieu de cela, vous installez des sites secondaires exécutant la version 1602. Voir *Installer un site secondaire* dans [Utiliser l’Assistant Configuration pour installer des sites](/sccm/core/servers/deploy/install/use-the-setup-wizard-to-install-sites).  

    Après cette étape, les nouveaux sites secondaires sont installés et exécutent la version 1602.  

5.  **Installez les nouveaux clients sur le site principal.**  

    -   Étant donné que vous n’avez pas installé de clients quand les sites principaux en étaient au niveau de la version 1511, vous n’avez pas besoin de mettre à niveau des clients de la version 1511 vers la version 1602.  

    -   Au lieu de cela, vous installez de nouveaux clients exécutant la version 1602. Consultez [Déployer des clients dans System Center Configuration Manager](../../../clients/deploy/deploy-clients-to-windows-computers.md).  

    Après cette étape, les nouveaux clients sont installés et exécutent la version 1602.  

## <a name="scenario---upgrade-system-center-2012-configuration-manager-to-an-update-version-of-system-center-configuration-manager-current-branch"></a>Scénario - Mettre à niveau System Center 2012 Configuration Manager vers une version de mise à jour de la branche Current Branch de System Center Configuration Manager  
Dans cet exemple de scénario, vous mettez à niveau l’infrastructure System Center 2012 Configuration Manager vers une version de mise à jour de System Center Configuration Manager, comme la version 1602.  

-   Le site d’administration centrale et chaque site principal nécessitent une mise à niveau vers la version de référence 1511 avant l’installation de la mise à jour de la version 1602.  

-   Les sites secondaires et les clients ne font l’objet d’aucune installation de la version 1511 ou de mise à niveau vers celle-ci. À la place, ils passent directement de Microsoft System Center 2012 Configuration Manager à System Center Configuration Manager version 1602.  

**Utilisez la séquence suivante :**  

1.  **Mettez à niveau votre site Microsoft System Center 2012 Configuration Manager de niveau supérieur** vers une version de référence de la branche Current Branch (comme la version 1511) à l’aide du support de source d’installation pour System Center Configuration Manager. Consultez [Mettre à niveau vers System Center Configuration Manager](../../../../core/servers/deploy/install/upgrade-to-configuration-manager.md).  

    -   Comme dans les scénarios de mise à niveau classiques, vous mettez toujours à niveau d’abord le site de niveau supérieur d’une hiérarchie, puis les sites enfants.  

    Après cette étape, votre site de niveau supérieur exécute la version 1511.  

2.  **Mettez à niveau chaque site principal enfant dans votre hiérarchie** vers cette même version de référence.  

    -   Quand vous effectuez la mise à niveau à partir de Microsoft System Center 2012 Configuration Manager, vous devez mettre à niveau manuellement chaque site principal vers une version de référence de Current Branch.  

    -   Vous ne devez pas mettre à niveau les sites secondaires pour l’instant.  

    Après cette étape, chaque site principal exécute la version 1511.  

3.  **Définissez des fenêtres de maintenance sur les sites principaux enfants.** Après avoir mis à niveau tous vos sites principaux vers la version de référence, envisagez de configurer des fenêtres de maintenance pour contrôler le moment où ces sites installent les mises à jour de l’infrastructure. Consultez [Comment utiliser les fenêtres de maintenance dans System Center Configuration Manager](../../../../core/clients/manage/collections/use-maintenance-windows.md).  (Les fenêtres de maintenance sont également appelées fenêtres de service dans la version 1511.)  

    -   Un site principal enfant installe automatiquement les mises à jour que vous installez sur un site d’administration centrale.  

    -   Les sites secondaires n’installent pas automatiquement les nouvelles versions et nécessitent une mise à niveau manuelle à partir de la console.  

    > [!NOTE]  
    >  Si vous utilisez la version 1511 et souhaitez configurer des fenêtres de service, vous devez d’abord installer le correctif à partir de la page de [l’article 3142341 de la Base de connaissances Microsoft](http://support.microsoft.com/kb/3142341). Ce problème est résolu lorsque vous installez la mise à jour 1602.  

    Après cette étape, lorsque vous installez des mises à jour sur le site d’administration centrale, les sites principaux enfants n’installent ces mises à jour que lorsque leur fenêtre de maintenance les y autorise.  

4.  **Installez la version de mise à jour sur votre site de niveau supérieur.** Cela a pour effet de mettre à jour votre site de niveau supérieur. Après que le site d’administration centrale a installé la version de mise à jour, chaque site principal enfant installe automatiquement la même mise à jour, sauf si une fenêtre de maintenance le bloque.  

    -   Par exemple, vous pouvez mettre à jour votre site de niveau supérieur de la version 1511 vers la version 1602. Consultez [Mises à jour pour System Center Configuration Manager](../../../../core/servers/manage/updates.md)  

    Après cette étape, votre site d’administration centrale et chaque site principal exécutent la version 1602.  

5.  **Mettez à niveau les sites secondaires.** Quand un site principal a installé la mise à jour et exécute la version 1602, vous utilisez l’option d’installation dans la console pour mettre à niveau les sites secondaires.  

    -   Cela a pour effet de mettre à niveau les sites secondaires directement à partir de Microsoft System Center 2012 Configuration Manager vers la version de mise à jour que vous avez installée sur le site principal.  

    -   Pour plus d’informations sur la mise à niveau d’un site secondaire, consultez [Upgrade sites](../../../../core/servers/deploy/install/upgrade-to-configuration-manager.md#bkmk_upgrade) (Mettre à niveau des sites) dans [Mettre à niveau vers System Center Configuration Manager](../../../../core/servers/deploy/install/upgrade-to-configuration-manager.md).  

6.  **Mettez à niveau les clients.** Utilisez les informations dans [Comment mettre à niveau les clients pour les ordinateurs Windows dans System Center Configuration Manager](../../../../core/clients/manage/upgrade/upgrade-clients-for-windows-computers.md).  

    -   Cela a pour effet de mettre à niveau les clients directement à partir de Microsoft System Center 2012 Configuration Manager vers la version de mise à jour que vous avez installée sur le site principal.  

    Après cette étape, les clients sont mis à niveau vers la version 1602 sans mise à niveau préalable vers la version 1511.



<!--HONumber=Nov16_HO1-->


