---
title: "Utiliser un média de démarrage pour déployer Windows sur le réseau | Microsoft Docs"
description: "Utilisez des déploiements de médias de démarrage dans System Center Configuration Manager pour déployer le système d’exploitation au démarrage de l’ordinateur de destination."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 999b5409-7e72-48d2-8554-4d44427ce383
caps.latest.revision: 5
author: Dougeby
ms.author: dougeby
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 74341fb60bf9ccbc8822e390bd34f9eda58b4bda
ms.openlocfilehash: beb730efbe4d9bae7c4c97f4e587c8919bd79049


---
# <a name="use-bootable-media-to-deploy-windows-over-the-network-with-system-center-configuration-manager"></a>Utiliser un média de démarrage pour déployer Windows sur le réseau avec System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Les déploiements de médias de démarrage dans System Center Configuration Manager vous permettent de déployer le système d’exploitation au démarrage de l’ordinateur de destination. Au démarrage de l'ordinateur de destination, il récupère la séquence de tâches, l'image du système d'exploitation et tout autre contenu requis à partir du réseau. Étant donné que le contenu n'est pas inclus sur le média, vous pouvez mettre à jour le contenu sans avoir à recréer le média.  

 Vous pouvez déployer des systèmes d’exploitation sur le réseau en utilisant la multidiffusion dans les scénarios de déploiement de système d’exploitation suivants :  

-   [Actualiser un ordinateur existant avec une nouvelle version de Windows](refresh-an-existing-computer-with-a-new-version-of-windows.md)  

-   [Installer une nouvelle version de Windows sur un nouvel ordinateur (système nu)](install-new-windows-version-new-computer-bare-metal.md)  

-   [Remplacer un ordinateur existant et transférer des paramètres](replace-an-existing-computer-and-transfer-settings.md)  

 Effectuez les étapes de l’un des scénarios de déploiement de système d’exploitation, puis utilisez les sections suivantes pour utiliser un média de démarrage pour déployer le système d’exploitation.  

## <a name="configure-deployment-settings"></a>Configurer les paramètres de déploiement  
 Quand vous utilisez un média de démarrage pour démarrer le processus de déploiement de système d’exploitation, vous devez configurer le déploiement pour rendre le système d’exploitation accessible au média. Vous pouvez configurer cela dans la page **Paramètres de déploiement** de l’Assistant Déploiement logiciel ou sous l’onglet **Paramètres de déploiement** dans les propriétés du déploiement.  Pour le paramètre **Rendre disponible aux éléments suivants** , sélectionnez l’une des options suivantes :  

-   **Clients, média et environnement PXE Configuration Manager**  

-   **Média et environnement PXE uniquement**  

-   **Média et environnement PXE uniquement (masqué)**  

## <a name="create-the-bootable-media"></a>Créer le média de démarrage  
 Vous pouvez spécifier si le média de démarrage est un disque mémoire flash USB ou un ensemble CD/DVD. L’ordinateur qui démarre le média doit prendre en charge l’option que vous choisissez comme lecteur de démarrage. Pour plus d’informations, consultez [Créer un média de démarrage](create-bootable-media.md).  

##  <a name="a-namebkmkdeploya-install-the-operating-system-from--bootable-media"></a><a name="BKMK_Deploy"></a> Installer le système d’exploitation à partir d’un média de démarrage  
 Insérez le média de démarrage dans un lecteur de démarrage sur l’ordinateur, puis mettez-le sous tension pour installer le système d’exploitation.  



<!--HONumber=Dec16_HO3-->


