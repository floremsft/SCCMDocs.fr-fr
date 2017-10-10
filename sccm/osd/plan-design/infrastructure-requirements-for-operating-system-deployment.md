---
title: "Configuration requise de l’infrastructure pour le déploiement de système d’exploitation | Microsoft Docs"
description: "Prenez connaissance de toutes les dépendances externes et internes au produit avant d’utiliser System Center 2012 Configuration Manager pour le déploiement de système d’exploitation."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 1dc74219-7ff5-4e3b-b4f6-5aad663bb75b
caps.latest.revision: "24"
author: mattbriggs
ms.author: mabrigg
manager: angrobe
ms.openlocfilehash: 523c7e7fd406274b0c0d88fcc4bd6b6247fa34e8
ms.sourcegitcommit: c145e515843a0f37c2e5ca5dbd22072a219d06b4
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/03/2017
---
# <a name="infrastructure-requirements-for-operating-system-deployment-in-system-center-configuration-manager"></a>Configuration requise de l’infrastructure pour le déploiement de système d’exploitation dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Le déploiement de système d’exploitation dans System Center 2012 Configuration Manager présente des dépendances externes et internes au produit. Utilisez les sections suivantes pour vous aider à préparer le déploiement de système d’exploitation.  

##  <a name="BKMK_ExternalDependencies"></a> Dépendances externes à Configuration Manager  
 Vous trouverez ci-dessous des informations sur les outils externes, les kits d’installation et les systèmes d’exploitation nécessaires au déploiement des systèmes d’exploitation dans Configuration Manager.  

### <a name="windows-adk-for-windows-10"></a>Windows ADK pour Windows 10  
 Windows ADK regroupe des outils et des documents permettant de configurer et de déployer des systèmes d'exploitation Windows. Configuration Manager utilise Windows ADK pour automatiser les installations de Windows, capturer des images Windows, migrer des données et profils utilisateur, et effectuer diverses autres opérations.  

 Les composants suivants de Windows ADK doivent être installés sur le serveur de site du site de niveau supérieur de la hiérarchie, sur le serveur de site de chaque site principal de la hiérarchie et sur le serveur de système de site du fournisseur SMS :  

-   Outil de migration de l'état utilisateur (USMT) <sup>1</sup>  

-   Outils de déploiement Windows  

-   Environnement de préinstallation Windows (Windows PE)

Pour obtenir la liste des versions du Windows 10 ADK que vous pouvez utiliser avec différentes versions de Configuration Manager, consultez [Prise en charge de Windows 10 comme client](https://docs.microsoft.com/sccm/core/plan-design/configs/support-for-windows-10#windows-10-adk).

 <sup>1</sup> USMT n'est pas requis sur le serveur de système de site du fournisseur SMS.  

> [!NOTE]  
>  Avant d’installer le site Configuration Manager, vous devez installer manuellement Windows ADK sur tous les ordinateurs qui hébergeront un serveur de site d’administration centrale ou un serveur de site principal.  

 Pour plus d'informations, voir :  

-   [Windows ADK pour les scénarios Windows 10 pour les informaticiens](https://technet.microsoft.com/library/mt280162\(v=vs.85\).aspx)  

-   [Télécharger le kit Windows ADK pour Windows 10](https://msdn.microsoft.com/windows/hardware/dn913721.aspx#adkwin10)  

-   [Prise en charge pour Windows 10](/sccm/core/plan-design/configs/support-for-windows-10)  


### <a name="user-state-migration-tool-usmt"></a>Outil de migration de l'état utilisateur (USMT)  
 Configuration Manager utilise un package USMT qui contient les fichiers sources USMT 10 pour capturer et restaurer l’état utilisateur dans le cadre du déploiement de votre système d’exploitation. Quand le programme d’installation de Configuration Manager est exécuté sur le site de niveau supérieur, il crée automatiquement le package USMT. USMT 10 peut capturer l’état utilisateur auprès de Windows 7, Windows 8, Windows 8.1 et Windows 10. USMT 10 est distribué dans le Kit de déploiement et d’évaluation Windows (Windows ADK) pour Windows 10.  

 Pour plus d'informations, voir :  

-   [Scénarios de migration courants pour USMT 10](https://technet.microsoft.com/library/mt299169\(v=vs.85\).aspx)  

-   [Gérer l’état utilisateur](../get-started/manage-user-state.md)  

### <a name="windows-pe"></a>Windows PE  
 Windows PE est utilisé pour les images de démarrage pour démarrer un ordinateur. C’est un système d’exploitation Windows offrant des services limités, qui est utilisé au cours de la pré-installation et du déploiement de systèmes d’exploitation Windows. Vous trouverez ci-dessous des informations sur la version de Configuration Manager, la version prise en charge de Windows ADK, la version de Windows PE sur laquelle l’image de démarrage est basée et qui peut être personnalisée à partir de la console Configuration Manager, ainsi que les versions de Windows PE sur lesquelles l’image de démarrage est basée et que vous pouvez personnaliser à l’aide de DISM avant d’ajouter l’image à la version spécifiée de Configuration Manager.  

#### <a name="configuration-manager-version-1511"></a>Configuration Manager version 1511  
 Vous trouverez ci-dessous des informations sur la version prise en charge de Windows ADK, la version de Windows PE sur laquelle l’image de démarrage est basée et qui peut être personnalisée à partir de la console Configuration Manager, ainsi que les versions de Windows PE sur lesquelles l’image de démarrage est basée et que vous pouvez personnaliser à l’aide de DISM avant d’ajouter l’image à Configuration Manager.  

-   **Version de Windows ADK**  

     Windows ADK pour Windows 10  

-   **Versions de Windows PE pour les images de démarrage personnalisables à partir de la console Configuration Manager**  

     Windows PE 10  

-   **Versions prises en charge de Windows PE pour les images de démarrage non personnalisables à partir de la console Configuration Manager**  

     Windows PE 3.1<sup>1</sup> et Windows PE 5  

     <sup>1</sup> Vous pouvez ajouter une image de démarrage à Configuration Manager uniquement si elle est basée sur Windows PE 3.1. Installez le supplément Windows AIK pour Windows 7 SP1 pour mettre à niveau Windows AIK pour Windows 7 (basé sur Windows PE 3) avec le supplément Windows AIK pour Windows 7 SP1 (basé sur Windows PE 3.1). Vous pouvez télécharger le supplément Windows AIK pour Windows 7 SP1 depuis le [Centre de téléchargement Microsoft](http://www.microsoft.com/download/details.aspx?id=5188).  

     Par exemple, si vous utilisez Configuration Manager, vous pouvez personnaliser les images de démarrage de Windows ADK pour Windows 10 (basées sur Windows PE 10) depuis la console Configuration Manager. Toutefois, si les images de démarrage basées sur Windows PE 5 sont prises en charge, vous devez les personnaliser depuis un autre ordinateur et utiliser la version de DISM installée avec Windows ADK pour Windows 8. Ensuite, vous pouvez ajouter l’image de démarrage à la console Configuration Manager. Pour plus d’informations sur la procédure à suivre pour personnaliser une image de démarrage (ajouter des composants et pilotes facultatifs), activer la prise en charge des commandes pour l’image de démarrage, ajouter l’image de démarrage à la console Configuration Manager et mettre à jour les points de distribution avec l’image de démarrage, consultez [Personnaliser les images de démarrage](../get-started/customize-boot-images.md). Pour plus d’informations sur les images de démarrage, consultez [Gérer les images de démarrage](../get-started/manage-boot-images.md).  

### <a name="windows-server-update-services-wsus"></a>Windows Server Update Services (WSUS)  
Vous devez installer les correctifs logiciels WSUS 4.0 suivants :
  - [Hotfix 3095113](https://support.microsoft.com/kb/3095113) est nécessaire pour la maintenance de Windows 10, qui utilise l’infrastructure des mises à jour logicielles pour obtenir les mises à niveau des fonctionnalités de Windows 10. Si vous avez WSUS 3.2, vous devez utiliser des séquences de tâches pour mettre à niveau Windows 10. Pour plus d’informations, consultez [Gérer WaaS (Windows as a Service)](../deploy-use/manage-windows-as-a-service.md).  
  - Le [correctif logiciel 3159706](https://support.microsoft.com/kb/3159706) est nécessaire si vous souhaitez utiliser la fonctionnalité de maintenance de Windows 10 pour mettre à niveau des ordinateurs avec la mise à jour anniversaire Windows 10 ou une version ultérieure. Pour installer ce correctif logiciel, vous devez effectuer manuellement certaines étapes, comme décrit dans l’article du support technique. Pour plus d’informations, consultez [Gérer WaaS (Windows as a Service)](../deploy-use/manage-windows-as-a-service.md).


### <a name="internet-information-services-iis-on-the-site-system-servers"></a>Internet Information Services (IIS) sur les serveurs de système de site  
 IIS est requis pour le point de distribution, le point de migration d’état et le point de gestion. Pour plus d’informations sur cette spécification, consultez [Prérequis des sites et systèmes de site](../../core/plan-design/configs/site-and-site-system-prerequisites.md).  

### <a name="windows-deployment-services-wds"></a>Services de déploiement Windows (WDS)  
 WDS est nécessaire pour les déploiements PXE, quand vous utilisez la multidiffusion pour optimiser la bande passante dans vos déploiements, et pour la maintenance hors connexion des images. Si le fournisseur est installé sur un serveur distant, vous devez installer WDS sur le serveur de site et le fournisseur distant. Pour plus d’informations, consultez [Services de déploiement Windows](#BKMK_WDS) dans cette rubrique.  

### <a name="dynamic-host-configuration-protocol-dhcp"></a>DHCP (Dynamic Host Configuration Protocol)  
 DHCP est obligatoire dans le cadre des déploiements PXE. Pour pouvoir déployer des systèmes d'exploitation à l'aide de PXE, vous devez disposer d'un serveur DHCP fonctionnant correctement et disposant d'un hôte actif. Pour plus d’informations sur les déploiements PXE, consultez [Utiliser PXE pour déployer Windows sur le réseau](../deploy-use/use-pxe-to-deploy-windows-over-the-network.md).  

### <a name="supported-operating-systems-and-hard-disk-configurations"></a>Systèmes d'exploitation et configurations de disque dur pris en charge  
 Pour plus d’informations sur les versions des systèmes d’exploitation et les configurations de disque dur prises en charge par Configuration Manager quand vous déployez des systèmes d’exploitation, consultez [Systèmes d’exploitation pris en charge](#BKMK_SupportedOS) et [Configurations de disque dur prises en charge](#BKMK_SupportedDiskConfig).  

### <a name="windows-device-drivers"></a>Pilotes de périphérique Windows  
 Des pilotes de périphérique Windows peuvent être utilisés lorsque vous installez le système d'exploitation sur l'ordinateur de destination et lorsque vous exécutez Windows PE à partir d'une image de démarrage. Pour plus d’informations sur les pilotes de périphérique, consultez [Gérer les pilotes](../get-started/manage-drivers.md).  

##  <a name="BKMK_InternalDependencies"></a> Dépendances de Configuration Manager  
 Vous trouverez ci-dessous des informations sur la configuration requise pour le déploiement de système d’exploitation dans Configuration Manager.  

### <a name="operating-system-image"></a>Image du système d'exploitation  
 Les images de système d’exploitation dans Configuration Manager sont stockées au format de fichier WIM (Windows Imaging Format) et représentent un regroupement compressé de fichiers et de dossiers de référence nécessaires pour installer et configurer avec succès un système d’exploitation sur un ordinateur. Pour plus d’informations, consultez [Gérer les images de système d’exploitation](../get-started/manage-operating-system-images.md).  

### <a name="driver-catalog"></a>Catalogue de pilotes  
 Pour déployer un pilote de périphérique, vous devez importer le pilote de périphérique, l’activer et le rendre disponible sur un point de distribution auquel le client Configuration Manager a accès. Pour plus d’informations sur le catalogue de pilotes, consultez [Gérer les pilotes](../get-started/manage-drivers.md).  

### <a name="management-point"></a>Point de gestion  
 Les points de gestion transfèrent des informations entre les ordinateurs clients et le site Configuration Manager. Le client utilise un point de gestion pour exécuter les séquences de tâches qui sont nécessaires pour terminer le déploiement de systèmes d'exploitation.  

 Pour plus d’informations sur les séquences de tâches, consultez [Considérations relatives à la planification de l’automatisation des tâches](planning-considerations-for-automating-tasks.md).  

### <a name="distribution-point"></a>Point de distribution  
 Des points de distribution sont utilisés dans la plupart des déploiements pour stocker les données qui sont utilisées pour déployer un système d'exploitation, telles que les packages d'images du système d'exploitation ou de pilotes de périphérique. En général, les séquences de tâches récupèrent des données à partir d'un point de distribution pour déployer le système d'exploitation.  

 Pour plus d’informations sur l’installation de points de distribution et sur la gestion de contenu, consultez [Gérer le contenu et l’infrastructure de contenu](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

### <a name="pxe-enabled-distribution-point"></a>Point de distribution PXE  
 Pour déployer des déploiements initiés par PXE, vous devez configurer un point de distribution pour accepter les demandes PXE des clients. Pour plus d’informations sur la configuration du point de distribution, consultez [Configurer un point de distribution](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#pxe).  

### <a name="multicast-enabled-distribution-point"></a>Point de distribution multidiffusion  
 Pour optimiser vos déploiements de système d'exploitation en utilisant la multidiffusion, vous devez configurer un point de distribution pour prendre en charge la multidiffusion. Pour plus d’informations sur la configuration du point de distribution, consultez [Configurer un point de distribution](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#multicast).   

### <a name="state-migration-point"></a>Point de migration d'état  
 Lorsque vous capturez et restaurez des données d'état utilisateur pour les déploiements côte à côte et d'actualisation, vous devez configurer un point de migration d'état pour stocker les données d'état utilisateur sur un autre ordinateur.  

 Pour plus d’informations sur la configuration du point de migration d’état, consultez [Point de migration d’état](../get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_StateMigrationPoints).  

 Pour plus d’informations sur la capture et la restauration de l’état utilisateur, consultez [Gérer l’état utilisateur](../get-started/manage-user-state.md).  

### <a name="service-connection-point"></a>point de connexion de service  
 Quand vous utilisez Waas (Windows as a Service) pour déployer la CB (Current Branch) de Windows 10, vous devez disposer du point de connexion de service installé. Pour plus d’informations, consultez [Gérer WaaS (Windows as a Service)](../deploy-use/manage-windows-as-a-service.md).  

### <a name="reporting-services-point"></a>Point de Reporting Services  
 Pour utiliser des rapports Configuration Manager pour les déploiements de système d’exploitation, vous devez installer et configurer un point de Reporting Services. Pour plus d’informations, consultez [Création de rapports](../../core/servers/manage/reporting.md).  

### <a name="security-permissions-for-operating-system-deployments"></a>Autorisations de sécurité pour les déploiements de système d'exploitation  
 Le rôle de sécurité **Gestionnaire de déploiement de systèmes d'exploitation** est un rôle prédéfini qui ne peut pas être modifié. Toutefois, vous pouvez copier le rôle, y apporter des modifications et les enregistrer sous un nouveau rôle de sécurité personnalisé. Voici quelques-unes des autorisations qui s'appliquent directement aux déploiements de système d'exploitation :  

-   **Package d’images de démarrage**: Créer, Supprimer, Modifier, Modifier un dossier, Déplacer un objet, Lire, Définir l’étendue de sécurité  

-   **Pilotes de périphériques**: Créer, Supprimer, Modifier, Modifier un dossier, Modifier le rapport, Déplacer un objet, Lire, Exécuter le rapport  

-   **Package de pilotes**: Créer, Supprimer, Modifier, Modifier un dossier, Déplacer un objet, Lire, Définir l’étendue de sécurité  

-   **Image de système d’exploitation**: Créer, Supprimer, Modifier, Modifier un dossier, Déplacer un objet, Lire, Définir l’étendue de sécurité  

-   **Package d’installation de système d’exploitation**: Créer, Supprimer, Modifier, Modifier un dossier, Déplacer un objet, Lire, Définir l’étendue de sécurité  

-   **Package de séquences de tâches**: Créer, Créer un média de séquence de tâches, Supprimer, Modifier, Modifier un dossier, Modifier le rapport, Déplacer un objet, Lire, Exécuter le rapport, Définir l’étendue de sécurité  

 Pour plus d’informations sur les rôles de sécurité personnalisés, consultez [Créer des rôles de sécurité personnalisés](../../core/servers/deploy/configure/configure-role-based-administration.md#BKMK_CreateSecRole).  

### <a name="security-scopes-for-operating-system-deployments"></a>Étendues de sécurité pour les déploiements de système d'exploitation  
 Utilisez des étendues de sécurité pour permettre aux utilisateurs administratifs d'accéder aux objets sécurisables utilisés dans les déploiements de système d'exploitation, tels que des images du système d'exploitation et de démarrage, des packages de pilotes et des packages de séquences de tâches. Pour plus d’informations, consultez [Sécurité et audit](../../core/understand/fundamentals-of-role-based-administration.md#bkmk_PlanScope).  

##  <a name="BKMK_WDS"></a> Services de déploiement Windows  
 Les Services de déploiement Windows (WDS) doivent être installés sur le même serveur que les points de distribution que vous configurez pour prendre en charge PXE ou la multidiffusion. WDS est inclus dans le système d’exploitation du serveur. Pour les déploiements PXE, WDS est le service qui effectue le démarrage PXE. Lorsque le point de distribution est installé et activé pour PXE, Configuration Manager installe un fournisseur dans WDS qui utilise les fonctions de démarrage PXE de WDS.  

> [!NOTE]  
>  Si le serveur nécessite un redémarrage, l’installation de WDS peut échouer. 

 Parmi les autres configurations WDS qui doivent être prises en compte, citons :  

-   Pour installer WDS sur le serveur, l'administrateur doit être membre du groupe Administrateurs local.  

-   Le serveur WDS doit être membre d'un domaine Active Directory ou contrôleur de domaine d'un domaine Active Directory. Toutes les configurations de forêts et de domaines Windows prennent en charge WDS.  

-   Si le fournisseur est installé sur un serveur distant, vous devez installer WDS sur le serveur de site et le fournisseur distant.  

###  <a name="BKMK_WDSandDHCP"></a> Considérations quand vous avez WDS et DHCP sur le même serveur  
 Tenez compte des problèmes de configuration suivants si vous envisagez de faire cohabiter le point de distribution sur un serveur exécutant DHCP.  

-   Vous devez disposer d'un serveur DHCP opérationnel avec une étendue active. Les Services de déploiement Windows utilisent PXE, qui nécessite un serveur DHCP.  

-   Le serveur DHCP et les Services de déploiement Windows utilisent tous deux le port numéro 67. Si vous hébergez à la fois les Services de déploiement Windows et un serveur DHCP, vous pouvez déplacer sur un autre serveur le serveur DHCP ou le point de distribution configuré pour PXE. Vous pouvez également suivre la procédure ci-dessous pour configurer le serveur des Services de déploiement Windows en vue d'écouter un autre port.  

    #### <a name="to-configure-the-windows-deployment-services-server-to-listen-on-a-different-port"></a>Pour configurer le serveur des Services de déploiement Windows en vue d'écouter un autre port  

    1.  Modifiez la clé de registre suivante :  

         **HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\WDSServer\Providers\WDSPXE**  

    2.  Définissez la valeur de Registre à : **UseDHCPPorts = 0**  

    3.  Pour que la nouvelle configuration prenne effet, exécutez la commande suivante sur le serveur :  

         `WDSUTIL /Set-Server /UseDHCPPorts:No /DHCPOption60:Yes`  

-   Un serveur DNS est requis pour exécuter les Services de déploiement Windows.  

-   Les ports UDP suivants doivent être ouverts sur le serveur des Services de déploiement Windows.  

    -   Port 67 (DHCP)  

    -   Port 69 (TFTP)  

    -   Port 4011 (PXE)  

    > [!NOTE]  
    >  En outre, si une autorisation DHCP est requise sur le serveur, vous devez ouvrir sur le serveur le port 68 du client DHCP.  

##  <a name="BKMK_SupportedOS"></a> Systèmes d’exploitation pris en charge  
 Tous les systèmes d’exploitation Windows répertoriés comme systèmes d’exploitation clients pris en charge dans [Systèmes d’exploitation pris en charge pour les clients et appareils](../../core/plan-design/configs/supported-operating-systems-for-clients-and-devices.md) sont pris en charge pour les déploiements de système d’exploitation.  

##  <a name="BKMK_SupportedDiskConfig"></a> Configurations de disque prises en charge  
 Le tableau suivant présente les combinaisons de configurations de disque dur sur les ordinateurs de référence et de destination qui sont prises en charge pour le déploiement de système d’exploitation dans Configuration Manager.  

|Configuration de disque dur de l'ordinateur de référence|Configuration de disque dur de l'ordinateur de destination|  
|------------------------------------------------|--------------------------------------------------|  
|Disque de base|Disque de base|  
|Volume simple sur un disque dynamique|Volume simple sur un disque dynamique|  

 Configuration Manager prend en charge la capture d’une image de système d’exploitation uniquement sur les ordinateurs configurés avec des volumes simples. Il n'existe pas de prise en charge pour les configurations de disque dur suivantes :  

-   Volumes fractionnés  

-   Volumes agrégés par bandes (RAID 0)  

-   Volumes en miroir (RAID 1)  

-   Volumes de parité (RAID 5)  

 Le tableau suivant présente une configuration de disque dur supplémentaire sur les ordinateurs de référence et de destination qui n’est pas prise en charge avec le déploiement de système d’exploitation dans Configuration Manager.  

|Configuration de disque dur de l'ordinateur de référence|Configuration de disque dur de l'ordinateur de destination|  
|------------------------------------------------|--------------------------------------------------|  
|Disque de base|Disque dynamique|  

## <a name="next-steps"></a>Étapes suivantes
[Préparer un déploiement de système d’exploitation](../get-started/prepare-for-operating-system-deployment.md)
