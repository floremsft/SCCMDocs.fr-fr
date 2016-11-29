---
title: "Utiliser le Centre logiciel pour déployer Windows sur le réseau | System Center Configuration Manager"
description: "Vous pouvez déployer un système d’exploitation dans le Centre logiciel afin d’actualiser un ordinateur existant avec une nouvelle version de Windows ou afin d’effectuer une mise à niveau de Windows vers la version la plus récente."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 919e3636-53fe-4119-ad14-2d03702b391b
caps.latest.revision: 5
author: Dougeby
ms.author: dougeby
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 189fdac38760b75eb3795348f6af4ef7e83c3f20


---
# <a name="use-software-center-to-deploy-windows-over-the-network-with-system-center-configuration-manager"></a>Utiliser le Centre logiciel pour déployer Windows sur le réseau avec System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

La séquence de tâches pour installer un système d’exploitation dans System Center Configuration Manager peut être mise à disposition dans le Centre logiciel. Vous pouvez déployer un système d’exploitation dans le Centre logiciel dans les scénarios de déploiement de système d’exploitation suivants :  

-   [Actualiser un ordinateur existant avec une nouvelle version de Windows](refresh-an-existing-computer-with-a-new-version-of-windows.md)  

-   [Effectuer une mise à niveau de Windows vers la dernière version](upgrade-windows-to-the-latest-version.md)  

 Effectuez les étapes de l’un des scénarios de déploiement de système d’exploitation, puis utilisez les sections suivantes pour vous préparer à effectuer les déploiements qui sont disponibles dans le Centre logiciel.  

## <a name="configure-deployment-settings"></a>Configurer les paramètres de déploiement  
 Quand vous souhaitez que le déploiement de système d’exploitation soit disponible dans le Centre logiciel, vous devez configurer le déploiement pour rendre le système d’exploitation accessible aux clients Configuration Manager. Vous pouvez configurer cela dans la page **Paramètres de déploiement** de l’Assistant Déploiement logiciel ou sous l’onglet **Paramètres de déploiement** dans les propriétés du déploiement.  Pour le paramètre **Rendre disponible aux éléments suivants** , sélectionnez **Clients Configuration Manager uniquement** ou **Clients, média et environnement PXE Configuration Manager**. Une fois le système d’exploitation déployé, il est affiché dans le Centre logiciel pour les membres du regroupement cible.  

##  <a name="a-namebkmkdeploya-deploy-the-task-sequence-to-computers"></a><a name="BKMK_Deploy"></a>Déployer la séquence de tâches sur les ordinateurs  
 Déployez le système d’exploitation dans un regroupement cible. Pour plus d'informations, voir [Déployer une séquence de tâches](manage-task-sequences-to-automate-tasks.md#BKMK_DeployTS). Quand vous déployez des systèmes d’exploitation pour le Centre logiciel, vous pouvez configurer si le déploiement est obligatoire ou disponible.  

-   **Déploiement obligatoire**: les déploiements obligatoires rendent le système d’exploitation accessible dans le Centre logiciel, mais il est démarré automatiquement conformément au calendrier d’attribution configurée.  

-   **Déploiement disponible**: le système d’exploitation est disponible dans le Centre logiciel et l’utilisateur peut l’installer à la demande.  



<!--HONumber=Nov16_HO1-->


