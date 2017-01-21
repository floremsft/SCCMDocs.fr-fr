---
title: Cluster SQL Server | System Center Configuration Manager
description: "Utiliser un cluster SQL Server pour héberger la base de données du site System Center Configuration Manager. Inclut des informations sur les options prises en charge."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: d09a82c6-bbd1-49ca-8ffe-e3ce87b85d33
caps.latest.revision: 10
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: e8d708cd3c138cc0f564e86073c25fa3bc519a71


---
# <a name="use-a-sql-server-cluster-for-the-system-center-configuration-manager-site-database"></a>Utiliser un cluster SQL Server pour la base de données du site System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*


 Vous pouvez utiliser un cluster SQL Server pour héberger la base de données du site System Center Configuration Manager. La base de données du site est le seul rôle de système de site pris en charge sur un cluster de serveurs.  

> [!NOTE]  
>  Pour pouvoir configurer correctement des clusters SQL Server, vous devez être familiarisé avec la configuration de clusters SQL Server et vous appuyer sur la documentation et les procédures décrites dans la bibliothèque de documentation de SQL Server.  

 L’utilisation d’un cluster permet de prendre en charge le basculement et d’améliorer la fiabilité de la base de données du site. En revanche, l’utilisation d’une base de données de site en cluster n’offre pas d’avantages supplémentaires en matière de traitement ou d’équilibrage de charge. En fait, une détérioration des performances peut résulter du fait que le serveur du site doit rechercher le nœud actif du cluster SQL Server avant de se connecter à la base de données du site.  

 Avant d’installer le Configuration Manager, vous devez préparer le cluster SQL Server pour prendre en charge Configuration Manager. (Voir les conditions préalables plus loin dans cette section.)  

 Au cours de l’installation de Configuration Manager, l’enregistreur du service VSS (service de cliché instantané des volumes) s’installe sur chaque nœud d’ordinateur physique du cluster Microsoft Windows Server pour prendre en charge la tâche de maintenance du **serveur de site de sauvegarde**.  

 Après l’installation du site, Configuration Manager vérifie la présence de modifications apportées au nœud de cluster toutes les heures, et gère automatiquement toute modification détectée qui affecte les installations de composants Configuration Manager (comme un basculement de nœud ou l’ajout d’un nouveau nœud au cluster SQL Server).  

## <a name="supported-options-for-using-a-sql-server-failover-cluster"></a>Options prises en charge pour l’utilisation d’un cluster de basculement SQL Server

-   Cluster d’instance unique  

-   Configuration d’instances multiples  

-   Nœuds actifs multiples  

-   Instances nommées ou par défaut  

**Conditions préalables :**  

-   La base de données du site doit être distante du serveur du site. (Le cluster ne peut pas inclure le serveur système du site.)  

-   Vous devez ajouter le compte d’ordinateur du serveur de site au groupe Administrateurs local de chaque serveur dans le cluster.  

-   Pour prendre en charge l’authentification Kerberos, le protocole de communication réseau **TCP/IP** doit être activé pour la connexion réseau de chaque nœud de cluster SQL Server. L’utilisation de**canaux nommés** n’est pas obligatoire, mais peut faciliter la résolution des problèmes d’authentification Kerberos. Les paramètres de protocole réseau sont configurés dans le **Gestionnaire de configuration SQL Server** sous **Configuration du réseau SQL Server**.  

-   Si vous utilisez une infrastructure PKI, voir &lt;Configuration requise des certificats PKI pour Configuration Manager> afin de connaître la configuration requise des certificats quand vous utilisez un cluster SQL Server pour la base de données du site.  

**Limitations à prendre en compte :**  

-   **Installation et configuration :**  

    -   Des sites secondaires ne peuvent pas utiliser un cluster SQL Server.  

    -   Vous n’avez pas la possibilité de spécifier des emplacements de fichier autres que les emplacements par défaut pour la base de données du site quand vous utilisez un cluster SQL Server.  

-   **Fournisseur SMS :**  

    -   L’installation d’une instance du fournisseur SMS sur un cluster SQL Server ou sur un ordinateur exécuté comme nœud SQL Server en cluster n’est pas prise en charge.  

-   **Options de réplication de données :**  

    -   Si vous utilisez des **vues distribuées**, vous ne pouvez pas utiliser un cluster SQL Server pour héberger la base de données du site.  

-   **Sauvegarde et récupération :**  

    -   Configuration Manager ne prend pas en charge la sauvegarde DPM pour un cluster SQL Server qui utilise une instance nommée, mais il prend en charge la sauvegarde DPM sur un cluster SQL Server qui utilise l'instance par défaut de SQL Server.  

## <a name="to-prepare-a-clustered-sql-server-instance-for-the-site-database"></a>Pour préparer une instance SQL Server en cluster pour la base de données du site  

-   Créez le cluster virtuel SQL Server pour héberger la base de données du site dans un environnement de cluster Windows Server existant. Pour connaître la procédure d’installation et de configuration d’un cluster SQL Server, consultez la documentation de votre version de SQL Server. Par exemple, si vous utilisez SQL Server 2008 R2, consultez  [Installation d’un cluster de basculement SQL Server 2008 R2](http://go.microsoft.com/fwlink/p/?LinkId=240231). Si vous utilisez SQL Server 2014, consultez [Installation d’un cluster de basculement SQL Server](https://technet.microsoft.com/library/hh231721\(v=sql.120\).aspx).  

-   Sur chaque ordinateur du cluster SQL Server, vous pouvez copier un fichier nommé **NO_SMS_ON_DRIVE.SMS** dans le dossier racine de chaque lecteur sur lequel vous ne voulez pas que Configuration Manager installe les composants du site. Par défaut, Configuration Manager installe certains composants sur chaque nœud physique pour prendre en charge des opérations telles que la sauvegarde.  

-   Ajoutez le compte ordinateur du serveur de site au groupe **Administrateurs locaux** de chaque ordinateur du nœud de cluster Windows Server.  

-   Dans l'instance SQL Server virtuelle, attribuez le rôle SQL Server **sysadmin** au compte utilisateur qui exécutera le programme d'installation de Configuration Manager.  

### <a name="to-install-a-new-site-using-a-clustered-sql-server"></a>Pour installer un nouveau site avec un serveur SQL Server en cluster  
 Pour installer un site qui utilise une base de données de site en cluster, exécutez le programme d’installation de Configuration Manager en suivant votre processus habituel pour installer un site, mais en apportant la modification suivante :  

-   Dans la page **Informations sur la base de données** , spécifiez le nom de l’instance de cluster SQL Server virtuelle qui doit héberger la base de données du site.  L’instance virtuelle remplace le nom de l’ordinateur qui exécute SQL Server.  

    > [!IMPORTANT]  
    >  Lorsque vous entrez le nom de l’instance de cluster SQL Server virtuelle, n’entrez pas le nom du serveur Windows Server virtuel créé par le cluster Windows Server. Si vous utilisez le nom du serveur Windows Server virtuel, la base de données du site s’installe sur le disque dur local du nœud de cluster Windows Server actif. Cela empêche le basculement en cas d’échec de ce nœud.  



<!--HONumber=Nov16_HO1-->


