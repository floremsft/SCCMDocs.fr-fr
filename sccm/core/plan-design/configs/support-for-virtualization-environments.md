---
title: Prise en charge de la virtualisation | System Center Configuration Manager
description: "Découvrez la configuration requise pour l’installation des rôles système de site et du client System Center Configuration Manager dans un environnement de virtualisation."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1098e8c5-9676-4c2b-841b-ec88bd04e495
caps.latest.revision: 6
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: be32ccee17bc4829888d42dfff3f2818f4fc2810


---
# <a name="support-for-virtualization-environments-for-system-center-configuration-manager"></a>Prise en charge des environnements de virtualisation pour System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Configuration Manager prend en charge l’installation de rôles système de site ou de clients sur les systèmes d’exploitation pris en charge qui s’exécutent comme machine virtuelle dans les environnements de virtualisation suivants. Cette prise en charge se fait même quand l'hôte de la machine virtuelle (environnement de virtualisation) n'est pas pris en charge comme client ou comme serveur de site.  

 **Par exemple**, si vous utilisez Microsoft Hyper-V Server 2012 pour héberger une machine virtuelle qui exécute Windows Server 2012, vous pouvez installer les rôles de système de site ou de client sur la machine virtuelle (Windows Server 2012), mais pas sur l’hôte (Microsoft Hyper-V Server 2012).  

|Environnement de virtualisation|  
|--------------------------------|  
|Windows Server 2008 R2|  
|Microsoft Hyper-V Server 2008 R2|  
|Windows Server 2012|  
|Microsoft Hyper-V Server 2012|  
|Windows Server 2012 R2|  

 Chaque machine virtuelle que vous utilisez doit correspondre ou être supérieure à la configuration matérielle et logicielle que vous utiliseriez pour un ordinateur Configuration Manager physique.  

 Vous pouvez vérifier que votre environnement de virtualisation est bien pris en charge pour Configuration Manager à l’aide du programme SVVP (Server Virtualization Validation Program) et de son Assistant Stratégie de prise en charge du programme de virtualisation en ligne. Pour plus d’informations sur le programme SVVP (Server Virtualization Validation Program), consultez [Programme SVVP (Server Virtualization Validation Program) de Windows Server](https://www.windowsservercatalog.com/svvp.aspx).  

> [!NOTE]  
>  Configuration Manager ne prend pas en charge les systèmes d’exploitation invités Virtual PC ou Virtual Server exécutés sur un Mac.  

Configuration Manager ne peut pas gérer les machines virtuelles, sauf si elles sont en ligne. Il n’est pas possible de mettre à jour une image d’ordinateur virtuel déconnecté, ni de collecter un inventaire via le client Configuration Manager sur l’ordinateur hôte.  

Aucune attention particulière n'est accordée aux machines virtuelles. Par exemple, si la mise à jour d’une image de machine virtuelle est arrêtée puis redémarrée sans que l’état de la machine virtuelle à laquelle la mise à jour a été appliquée ne soit enregistré, il est possible que Configuration Manager ne détermine pas s’il est nécessaire de réappliquer cette mise à jour.  

##  <a name="a-namebkmkazurea-microsoft-azure-virtual-machines"></a><a name="bkmk_Azure"></a> Machines virtuelles Microsoft Azure  
 Configuration Manager peut s’exécuter sur des machines virtuelles Microsoft Azure, de la même manière que localement sur votre réseau physique d’entreprise. Vous pouvez utiliser Configuration Manager sur des machines virtuelles Microsoft Azure dans les scénarios suivants :  

-   **Scénario 1 :** vous pouvez exécuter Configuration Manager sur une machine virtuelle Microsoft Azure et l’utiliser pour gérer des clients installés sur d’autres machines virtuelles Microsoft Azure.  

-   **Scénario 2 :** vous pouvez exécuter Configuration Manager sur une machine virtuelle Microsoft Azure, et l’utiliser pour gérer des clients qui ne s’exécutent pas dans Microsoft Azure.  

-   **Scénario 3** : vous pouvez exécuter différents rôles système de site Configuration Manager sur des machines virtuelles Microsoft Azure tout en exécutant d’autres rôles sur votre réseau physique d’entreprise (avec une connectivité réseau appropriée pour les communications).  

La même configuration requise de System Center Configuration Manager en matière de réseaux, de configurations prises en charge et de matériel, applicable à l’installation locale de Configuration Manager sur votre réseau d’entreprise physique, s’applique également à l’installation sur Microsoft Azure.  

> [!IMPORTANT]  
>  Les sites et les clients Configuration Manager qui s’exécutent sur des machines virtuelles Azure sont soumis aux mêmes exigences de licence que les installations locales.  



<!--HONumber=Nov16_HO1-->


