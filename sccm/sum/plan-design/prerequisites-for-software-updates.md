---
title: "Configuration requise pour les mises à jour logicielles | Microsoft Docs"
description: "Découvrez les prérequis pour les mises à jour logicielles dans System Center Configuration Manager."
keywords: 
author: dougeby
ms.author: dougeby
manager: angrobe
ms.date: 10/06/2016
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology: configmgr-sum
ms.assetid: fdf05118-162a-411e-b72e-386b9dc9a5e1
ms.openlocfilehash: 179f076f228daa5adf612275a822cd379b0ce1e3
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/07/2017
---
# <a name="prerequisites-for-software-updates-in-system-center-configuration-manager"></a>Configuration requise pour les mises à jour logicielles dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Cette rubrique répertorie les prérequis pour les mises à jour logicielles dans System Center Configuration Manager. Pour chaque composant requis, les dépendances externes et les dépendances internes figurent dans des tableaux séparés.  

## <a name="software-update-dependencies-external-to-configuration-manager"></a>Dépendances de mise à jour logicielle externes à Configuration Manager  
 Les sections suivantes répertorient les dépendances externes des mises à jour logicielles.  

### <a name="internet-information-services-iis"></a>Internet Information Services (IIS)  
 Internet Information Services (IIS) doit se trouver sur les serveurs de système de site pour exécuter le point de mise à jour logicielle, le point de gestion et le point de distribution. Pour plus d’informations, consultez [Prérequis pour les rôles système de site](../../core/plan-design/configs/site-and-site-system-prerequisites.md).  

### <a name="windows-server-update-services-wsus"></a>Windows Server Update Services (WSUS)  
 Les services WSUS sont requis pour la synchronisation des mises à jour logicielles et les analyses de compatibilité des mises à jour logicielles sur les clients. Le serveur WSUS doit être installé avant de créer le rôle de système de site du point de mise à jour logicielle. Les versions suivantes de WSUS sont prises en charge pour un point de mise à jour logicielle :  

-   WSUS 4 (rôle dans Windows Server 2012 et Windows Server 2012 R2)  

-   WSUS 3.2 (rôle dans Windows Server 2008 R2)  

 Si vous possédez plusieurs points de mise à jour logicielle sur un même site, veillez à ce qu'ils exécutent tous la même version des services WSUS.  

> [!WARNING]  
>  La classification des mises à jour logicielles de type **Mises à niveau** n’est prise en charge qu’à partir de WSUS 4.0. Avant de synchroniser cette nouvelle classification et d’avoir la possibilité d’évaluer des ordinateurs Windows 10 dans un plan de maintenance de Windows 10, il est essentiel que vous installiez le [correctif 3095113](https://support.microsoft.com/kb/3095113) pour WSUS sur vos points de mise à jour logicielle et serveurs de site. Ce correctif permet à WSUS sur un serveur Windows Server 2012 ou Windows Server 2012 R2 de synchroniser et de distribuer des mises à niveau de fonctionnalités pour Windows 10. Pour plus d’informations, consultez [Gérer Windows as a service](../../osd/deploy-use/manage-windows-as-a-service.md).  
>   
>  Si vous synchronisez des mises à jour logicielles entrant dans la classification **Mises à niveau** avant d’installer le [correctif 3095113](https://support.microsoft.com/kb/3095113), consultez [Recover from synchronizing the Mises à niveau category before you install KB 3095113](#BKMK_RecoverUpgrades).  

### <a name="wsus-administration-console"></a>Console d'administration WSUS  
 La console d’administration WSUS est requise sur le serveur de site Configuration Manager quand le point de mise à jour logicielle se trouve sur un serveur de système de site distant et que WSUS n’est pas déjà installé sur le serveur de site.  

> [!IMPORTANT]  
>  La version WSUS du serveur de site doit être identique à la version WSUS exécutée sur les points de mise à jour logicielle.  

> [!IMPORTANT]  
>  N'utilisez pas la console d'administration WSUS pour configurer les paramètres WSUS. Configuration Manager se connecte à WSUS qui s’exécute sur le point de mise à jour logicielle et configure les paramètres appropriés.  

### <a name="windows-update-agent-wua"></a>Agent Windows Update (WUA)  
 Le client WUA est requis sur les clients, pour leur permettre de se connecter au serveur WSUS et d'extraire la liste des mises à jour logicielles dont la compatibilité doit être analysée.  

 Quand vous installez Configuration Manager, la dernière version de WUA est téléchargée. Ensuite, lors de l’installation du client Configuration Manager, WUA est mis à niveau si nécessaire. Cependant, si l'installation échoue, vous devez utiliser une autre méthode pour mettre à niveau WUA.  

## <a name="software-update-dependencies-internal-to-configuration-manager"></a>Dépendances de mise à jour logicielle internes à Configuration Manager  
 Les sections suivantes répertorient les dépendances internes pour les mises à jour logicielles dans Configuration Manager.  

### <a name="management-points"></a>Points de gestion  
 Les points de gestion transfèrent des informations entre les ordinateurs clients et le site Configuration Manager. Ils sont requis pour les mises à jour logicielles.  

### <a name="software-update-point"></a>Point de mise à jour logicielle  
 Pour pouvoir déployer des mises à jour logicielles dans Configuration Manager, vous devez installer un point de mise à jour logicielle sur le serveur WSUS. Pour plus d’informations, consultez [Installer et configurer un point de mise à jour logicielle](../get-started/install-a-software-update-point.md).

### <a name="distribution-points"></a>Points de distribution  
 Les points de distribution sont nécessaires pour stocker le contenu des mises à jour logicielles. Pour plus d’informations sur l’installation des points de distribution et sur la gestion de contenu, consultez [Gérer le contenu et l’infrastructure de contenu](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

### <a name="client-settings-for-software-updates"></a>Paramètres client pour les mises à jour logicielles  
 Par défaut, les mises à jour logicielles sont activées pour les clients. Cependant, d'autres paramètres sont à votre disposition pour contrôler quand et comment les clients doivent évaluer la compatibilité des mises à jour logicielles, et pour contrôler comment ces mises à jour doivent être installées.  

 Pour plus d'informations, consultez :  

-   [Paramètres client pour les mises à jour logicielles](../get-started/manage-settings-for-software-updates.md#a-namebkmkclientsettingsa-client-settings-for-software-updates).  

-   [Paramètres client des mises à jour logicielles](../../core/clients/deploy/about-client-settings.md#software-updates).  

### <a name="reporting-services-point"></a>Point de Reporting Services  
 Le rôle de système de site Point de Reporting Services peut afficher des rapports concernant les mises à jour logicielles. Ce rôle est facultatif, mais recommandé. Pour plus d’informations sur la création d’un point de Reporting Services, consultez [Configuration de la création de rapports](../../core/servers/manage/configuring-reporting.md).  

##  <a name="BKMK_RecoverUpgrades"></a> Récupérer d’une synchronisation de la catégorie Mises à niveau avant l’installation du correctif KB 3095113  
 Vous devez installer le [correctif 3095113](https://support.microsoft.com/kb/3095113) pour WSUS sur vos points de mise à jour logicielle et serveurs de site avant de synchroniser la classification **Mises à niveau** . Si le correctif n’est pas installé lors de l’activation de la classification **Mises à niveau** , WSUS détecte la mise à niveau de fonctionnalités de la build 1511 de Windows 10, même s’il ne peut pas correctement télécharger et déployer les packages associés. Si vous synchronisez des mises à niveau sans avoir préalablement installé le [correctif 3095113](https://support.microsoft.com/kb/3095113), cela a pour effet de remplir la base de données WSUS (SUSDB) avec des données inutilisables qui doivent être effacées avant le déploiement des mises à niveau.  Pour résoudre ce problème, procédez comme suit.  

#### <a name="to-recover-from-synchronizing-the-upgrades-classification-before-you-install-kb-3095113"></a>Pour récupérer d’une synchronisation de la classification Mises à niveau avant d’installer le correctif KB 3095113  

1.  Supprimez les mises à jour logicielles entrant dans la classification Mises à niveau. Vous pouvez utiliser un script PowerShell similaire à l’exemple suivant :  

    ```  
    $Server = Get-WSUSServer  
    $Config = $Server.GetConfiguration()  
    $Update10563 = “df4e45a3-946d-4467-b3fd-8621174bb666”  
    $UpdateGUID = New-Object Guid($Update10563)  
    $Server.DeleteUpdate($UpdateGUID)  
    ```  

    > [!IMPORTANT]  
    >  Vous devez exécuter le script sur tous les points de mise à jour logicielle dans votre hiérarchie Configuration Manager avant de passer à l’étape suivante.  

     Pour supprimer en bloc des mises à jour logicielles entrant dans la classification Mises à niveau, vous pouvez modifier le script PowerShell afin qu’il lise plusieurs GUID à partir d’un fichier txt.  

2.  Décochez la classification **Mises à niveau** dans les propriétés du composant Point de mise à jour logicielle (pour plus d’informations, consultez [Configurer les classifications et les produits](../get-started/configure-classifications-and-products.md)), puis démarrez la synchronisation des mises à jour logicielles (pour plus d’informations, consultez [Synchroniser les mises à jour logicielles](../get-started/synchronize-software-updates.md)).  

3.  Installez leez le [correctif 3095113](https://support.microsoft.com/kb/3095113) pour WSUS sur vos points de mise à jour logicielle et serveurs de site.  

4.  Cochez la classification **Mises à niveau** dans les propriétés du composant Point de mise à jour logicielle (pour plus d’informations, consultez [Configurer les classifications et les produits](../get-started/configure-classifications-and-products.md)), puis démarrez la synchronisation des mises à jour logicielles (pour plus d’informations, consultez [Synchroniser les mises à jour logicielles](../get-started/synchronize-software-updates.md)).  

## <a name="next-steps"></a>Étapes suivantes
[Préparer la gestion des mises à jour logicielles](../get-started/prepare-for-software-updates-management.md)
