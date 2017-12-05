---
title: "Récupération sans assistance"
titleSuffix: Configuration Manager
description: "Utilisez un script pour récupérer vos sites dans System Center Configuration Manager."
ms.custom: na
ms.date: 6/5/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 828c31d1-3d70-4412-b1a8-c92e7e504d39
caps.latest.revision: 
author: mestew
ms.author: mstewart
manager: angrobe
ms.openlocfilehash: be561de1fd14245e3cf52148683611a307484d3d
ms.sourcegitcommit: daa080cf220835f157a23e8c8e2bd2781b869bb7
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/04/2017
---
# <a name="unattended-site-recovery-for-configuration-manager"></a>Récupération de site sans assistance pour Configuration Manager   

*S’applique à : System Center Configuration Manager (Current Branch)* Pour effectuer une [récupération sans assistance](/sccm/protect/understand/recover-sites#site-recovery-procedures) d’un site principal ou d’un site d’administration centrale Configuration Manager, vous pouvez créer un script d’installation sans assistance et utiliser le programme d’installation avec l’option de commande **/script**. Le script fournit le même type d'informations que les invites de l'Assistant Installation ; la seule différence est qu'il n'existe pas de paramètres par défaut. Toutes les valeurs doivent être indiquées pour les clés d'installation qui s'appliquent au type de récupération choisi.

 Pour utiliser l'option de ligne de commande d'installation /script, vous devez créer un fichier d'initialisation et en spécifier le nom après l'option de ligne de commande d'installation /script. Le nom du fichier n'a pas importance tant qu'il est suivi de l'extension de fichier **.ini**. Lorsque vous référencez le fichier d'initialisation d'installation à partir de la ligne de commande, vous devez fournir le chemin d'accès complet au fichier. Par exemple, si votre fichier d'initialisation d'installation s'appelle *setup.ini* et qu'il est stocké dans le *dossier C:\setup*, votre ligne de commande serait :

 **setup /script c:\setup\setup.ini**.

> [!IMPORTANT]  
>  Vous devez disposer de droits d'administrateur pour exécuter le programme d'installation. Lorsque vous exécutez le programme d'installation avec le script sans assistance, démarrez l'invite de commande dans un contexte d'administrateur à l'aide de l'option **Exécuter en tant qu'administrateur**.

 Le script contient les noms de section, les noms de clé et les valeurs. Les noms des clés de section requis varient en fonction du type de récupération faisant l'objet du script. L’ordre des clés dans les sections et l’ordre des sections dans le fichier n’ont pas d’importance. Les clés ne tiennent pas compte de la casse. Lorsque vous attribuez des valeurs aux clés, le nom de la clé doit être suivi du signe égal (=) et de la valeur de la clé.

 Utilisez les sections suivantes pour créer votre script de récupération de site en mode sans assistance. Les tableaux répertorient les clés de script d'installation disponibles ainsi que leurs valeurs correspondantes, indiquent si elles sont obligatoires ou non, le type d'installation pour lequel elles sont utilisées, ainsi qu'une brève description de la clé.

## <a name="recover-a-central-administration-site-unattended"></a>Récupérer un site d’administration centrale sans assistance
 Utilisez les informations suivantes pour configurer un fichier de script d’installation sans assistance afin de récupérer un site d’administration centrale.

 **Identification**

-   **Nom de clé :** Action

    -   **Obligatoire :** Oui
    -   **Valeurs :** RecoverCCAR
    -   **Détails :** récupère un site d’administration centrale


-   **Nom de la clé :** CDLatest

    -   **Obligatoire :** Oui, uniquement en cas d’utilisation de médias du dossier CD.Latest.
    -   **Valeurs :** 1. Toute autre valeur est considérée comme signifiant que CD.Latest ne doit pas être utilisé.
    -   **Détails :** Le script doit inclure cette clé et cette valeur en cas d’exécution de l’installation à partir de médias du dossier CD.Latest dans le cadre de l’installation d’un site principal ou d’administration centrale, ou de la récupération d’un site principal ou d’administration centrale. Cette valeur indique au programme d’installation que des médias de CD.Latest sont utilisés.

**RecoveryOptions**   
-   **Nom de clé :** ServerRecoveryOptions   

    -   **Obligatoire :** Oui
    -   **Valeurs :** 1, 2 ou 4  
         1 = Serveur de site de récupération et SQL Server.   
         2 = Récupérer le serveur de site uniquement.  
         4 = Récupérer SQL Server uniquement.
    -   **Détails :** spécifie si le programme d’installation doit récupérer le serveur de site, SQL Server ou les deux. Les clés associées sont requises lorsque vous définissez la valeur suivante pour le paramètre ServerRecoveryOptions :  
        -   **Valeur = 1** : vous avez la possibilité de spécifier une valeur pour la clé **SiteServerBackupLocation** afin de récupérer le site en utilisant une sauvegarde de site. Si vous ne spécifiez pas de valeur, le site est réinstallé sans être restauré à partir d'un jeu de sauvegarde.

             la clé **BackupLocation** est requise lorsque vous configurez la valeur **10** pour la clé **DatabaseRecoveryOptions** , qui consiste à restaurer la base de données de site à partir de la sauvegarde.

        -   **Valeur = 2** : vous avez la possibilité de spécifier une valeur pour la clé **SiteServerBackupLocation** afin de récupérer le site en utilisant une sauvegarde de site. Si vous ne spécifiez pas de valeur, le site est réinstallé sans être restauré à partir d'un jeu de sauvegarde.

        -   **Valeur = 4** la clé **BackupLocation** est requise lorsque vous configurez la valeur **10** pour la clé **DatabaseRecoveryOptions** , qui consiste à restaurer la base de données de site à partir de la sauvegarde.

-   **Nom de clé :** DatabaseRecoveryOptions

    -   **Obligatoire :** peut-être
    -   **Valeurs :** 10, 20, 40, 80  
         10 = Restaurer la base de données du site à partir d'une sauvegarde.  
         20 = Utiliser une base de données de site qui a été récupérée manuellement à l'aide d'une autre méthode.   
         40 = Créer une nouvelle base de données de site. Utilisez cette option lorsqu'aucune sauvegarde de base de données de site n'est disponible. Les données globales et de site sont récupérées via la réplication à partir d'autres sites.  
         80 = Ignorer la récupération de base de données.
    -   **Détails :** spécifie comment le programme d’installation va récupérer la base de données de site dans SQL Server. Cette clé est requise lorsque la valeur du paramètre **ServerRecoveryOptions** est **1** ou **4**.


-   **Nom de clé :** ReferenceSite  

    -   **Obligatoire :** peut-être
    -   **Valeurs :** &lt;nom_domaine_complet_site_référence\>
    -   **Détails :** spécifie le site principal de référence que le site d’administration centrale utilise pour récupérer des données globales si la sauvegarde de la base de données est antérieure à la période de rétention du suivi des modifications ou quand vous récupérez le site sans sauvegarde.

         Quand vous ne spécifiez pas de site de référence et que la sauvegarde est antérieure à la période de rétention du suivi des modifications, tous les sites principaux sont réinitialisés avec les données restaurées à partir du site d’administration centrale.

         Lorsque vous ne spécifiez pas de site de référence, et que la sauvegarde est comprise dans la période de rétention du suivi des modifications, seules les modifications apportées depuis la dernière sauvegarde sont répliquées à partir des sites principaux. Lorsqu'il existe des conflits entre des modifications issues de différents sites principaux, le site d'administration centrale utilise la première modification reçue.

         Cette clé est requise lorsque le paramètre **DatabaseRecoveryOptions** a la valeur **40**.

-   **Nom de clé :** SiteServerBackupLocation

    -   **Obligatoire :** non
    -   **Valeurs :** &lt;chemin_vers_jeu_sauvegarde_serveur_site\>
    -   **Détails :** spécifie le chemin vers le jeu de sauvegarde du serveur de site. Cette clé est optionnelle lorsque la valeur du paramètre **ServerRecoveryOptions** est **1** ou **2**. Spécifiez une valeur pour la clé **SiteServerBackupLocation** pour récupérer le site à l'aide d'une sauvegarde de site. Si vous ne spécifiez pas de valeur, le site est réinstallé sans être restauré à partir d'un jeu de sauvegarde.


-   **Nom de clé :** BackupLocation

    -   **Obligatoire :** peut-être
    -   **Valeurs :** &lt;chemin_vers_jeu_sauvegarde_base_de_données_site\>
    -   **Détails :** spécifie le chemin d’accès au jeu de sauvegarde de la base de données du site. La clé **BackupLocation** est requise lorsque vous configurez une valeur de **1** ou **4** pour la clé **ServerRecoveryOptions** , et une valeur de **10** pour la clé **DatabaseRecoveryOptions** .


**Options**

-   **Nom de clé :** ProductID
    -   **Obligatoire :** Oui
    -   **Valeurs :**   
         xxxxx-xxxxx-xxxxx-xxxxx-xxxxx  
          Eval
    -   **Détails :** clé de produit de l’installation de Configuration Manager avec les tirets. Entrez **Eval** pour installer la version d’évaluation de Configuration Manager.  


-   **Nom de clé :** SiteCode

    -   **Obligatoire :** Oui
    -   **Valeurs :** &lt;code_de_site\>
    -   **Détails :** trois caractères alphanumériques identifiant le site de façon univoque dans votre hiérarchie. Vous devez définir le code de site utilisé par le site avant la défaillance.


-   **Nom de clé :** SiteName

    -   **Obligatoire :** Oui
    -   **Valeurs :** nom_site
    -   **Détails :** description de ce site.


-   **Nom de clé :** SMSInstallDir

    -   **Obligatoire :** Oui
    -   **Valeurs :** &lt;*CheminInstallationConfigMgr*>
    -   **Détails :** spécifie le dossier d’installation des fichiers programmes de Configuration Manager.
        > [!NOTE]   
        >  Vous pouvez spécifier le chemin d’origine ou un nouveau chemin à utiliser pour l’installation de Configuration Manager.

-   **Nom de clé :** SDKServer

    -   **Obligatoire :** Oui
    -   **Valeurs :** &lt;*nom de domaine complet du fournisseur SMS*>
    -   **Détails :** spécifie le FQDN du serveur qui héberge le fournisseur SMS. Vous devez spécifier le serveur qui hébergeait le fournisseur SMS avant la défaillance.

         Vous pouvez configurer d'autres fournisseurs SMS pour le site après l'installation initiale.

-   **Nom de clé :** PrerequisiteComp

    -   **Obligatoire :** Oui
    -   **Valeurs :** 0 ou 1  
         0 = téléchargement   
         1 = déjà téléchargé
    -   **Détails :** spécifie si les fichiers d’installation prérequis ont déjà été téléchargés. Par exemple, si vous utilisez la valeur 0, le programme d'installation va télécharger les fichiers.  


-   **Nom de clé :** PrerequisitePath

    -   **Obligatoire :** Oui
    -   **Valeurs :** &lt;*chemin_fichiers_requis_programme_installation*>
    -   **Détails :** spécifie le chemin vers les fichiers d’installation prérequis. Selon la valeur **PrerequisiteComp** , le programme d'installation utilise ce chemin d'accès pour stocker les fichiers téléchargés ou pour localiser des fichiers précédemment téléchargés.

-   **Nom de clé :** AdminConsole

    -   **Obligatoire :** peut-être
    -   **Valeurs :** 0 ou 1 0 = ne pas installer   
         1 = installer
    -   **Détails :** spécifie si la console Configuration Manager doit ou non être installée. Cette clé est obligatoire sauf quand le paramètre **ServerRecoveryOptions** a la valeur **4**.


-   **Nom de clé :** JoinCEIP

    -   **Obligatoire :** Oui
    -   **Valeurs :** 0 ou 1  
         0 = ne pas joindre  
         1 = joindre
    -   **Détails :** spécifie si vous voulez vous joindre au programme d’amélioration de l’expérience utilisateur.

**SQLConfigOptions**

-   **Nom de clé :** SQLServerName

    -   **Obligatoire :** Oui
    -   **Valeurs :** *&lt;nom_SQLServer\>*
    -   **Détails :** nom du serveur ou nom de l’instance en cluster exécutant SQL Server, et devant héberger la base de données de site. Vous devez spécifier le serveur qui a hébergé la base de données de site avant la défaillance.


-   **Nom de clé :** DatabaseName

    -   **Obligatoire :** Oui
    -   **Valeurs :** *&lt;nom_base_de_données_site\>* ou *&lt;nom_instance\>*\\*&lt;nom_base_de_données_site\>*
    -   **Détails :** nom de la base de données SQL Server à créer ou à utiliser pour installer la base de données du site d’administration centrale. Vous devez spécifier le nom de base de données qui était utilisé avant la défaillance.

        > [!IMPORTANT]  
        >  Si vous n'utilisez pas l'instance par défaut, vous devez spécifier le nom d'instance et le nom de base de données de site.

-   **Nom de clé :** SQLSSBPort

    -   **Obligatoire :** non
    -   **Valeurs :** &lt;*numéro_port_SSB*>
    -   **Détails :** spécifiez le port SQL Server Service Broker (SSB) utilisé par SQL Server. Généralement, SSB est configuré pour utiliser le port TCP 4022, mais d'autres ports sont pris en charge. Vous devez définir le même port SSB utilisé avant la défaillance.

## <a name="recover-a-primary-site-unattended"></a>Récupérer un site principal en mode sans assistance
 Utilisez les informations suivantes pour configurer un fichier de script d’installation sans assistance afin de récupérer un site d’administration centrale.

 **Identification**

-   **Nom de clé :** Action

    -   **Obligatoire :** Oui
    -   **Valeurs :** site_principal_à_récupérer
    -   **Détails :** récupère un site principal


-   **Nom de la clé :** CDLatest

    -   **Obligatoire :** Oui, uniquement en cas d’utilisation de médias du dossier CD.Latest.
    -   **Valeurs :** 1. Toute autre valeur est considérée comme signifiant que CD.Latest ne doit pas être utilisé.
    -   **Détails :** Le script doit inclure cette clé et cette valeur en cas d’exécution de l’installation à partir de médias du dossier CD.Latest dans le cadre de l’installation d’un site principal ou d’administration centrale, ou de la récupération d’un site principal ou d’administration centrale. Cette valeur indique au programme d’installation que des médias de CD.Latest sont utilisés.

**RecoveryOptions**

-   **Nom de clé :** ServerRecoveryOptions

    -   **Obligatoire :** Oui
    -   **Valeurs :** 1, 2 ou 4    
         1 = Serveur de site de récupération et SQL Server.   
         2 = Récupérer le serveur de site uniquement.  
         4 = Récupérer SQL Server uniquement.
    -   **Détails :** spécifie si le programme d’installation doit récupérer le serveur de site, SQL Server ou les deux. Les clés associées sont requises lorsque vous définissez la valeur suivante pour le paramètre ServerRecoveryOptions :

        -   **Valeur = 1** : vous avez la possibilité de spécifier une valeur pour la clé **SiteServerBackupLocation** afin de récupérer le site en utilisant une sauvegarde de site. Si vous ne spécifiez pas de valeur, le site est réinstallé sans être restauré à partir d'un jeu de sauvegarde.

             la clé **BackupLocation** est requise lorsque vous configurez la valeur **10** pour la clé **DatabaseRecoveryOptions** , qui consiste à restaurer la base de données de site à partir de la sauvegarde.

        -   **Valeur = 2** : vous avez la possibilité de spécifier une valeur pour la clé **SiteServerBackupLocation** afin de récupérer le site en utilisant une sauvegarde de site. Si vous ne spécifiez pas de valeur, le site est réinstallé sans être restauré à partir d'un jeu de sauvegarde.

        -   **Valeur = 4** la clé **BackupLocation** est requise lorsque vous configurez la valeur **10** pour la clé **DatabaseRecoveryOptions** , qui consiste à restaurer la base de données de site à partir de la sauvegarde.

-   **Nom de clé :** DatabaseRecoveryOptions

    -   **Obligatoire :** peut-être
    -   **Valeurs :** 10, 20, 40, 80  
         10 = Restaurer la base de données du site à partir d'une sauvegarde.  
         20 = Utiliser une base de données de site qui a été récupérée manuellement à l'aide d'une autre méthode.     
         40 = Créer une nouvelle base de données de site. Utilisez cette option lorsqu'aucune sauvegarde de base de données de site n'est disponible. Les données globales et de site sont récupérées via la réplication à partir d'autres sites.  
         80 = Ignorer la récupération de base de données.
    -   **Détails :** spécifie comment le programme d’installation va récupérer la base de données de site dans SQL Server. Cette clé est requise lorsque la valeur du paramètre **ServerRecoveryOptions** est **1** ou **4**.


-   **Nom de clé :** SiteServerBackupLocation

    -   **Obligatoire :** non
    -   **Valeurs :** &lt;chemin_vers_jeu_sauvegarde_serveur_site\>
    -   **Détails :** spécifie le chemin vers le jeu de sauvegarde du serveur de site. Cette clé est optionnelle lorsque la valeur du paramètre **ServerRecoveryOptions** est **1** ou **2**. Spécifiez une valeur pour la clé **SiteServerBackupLocation** pour récupérer le site à l'aide d'une sauvegarde de site. Si vous ne spécifiez pas de valeur, le site est réinstallé sans être restauré à partir d'un jeu de sauvegarde.     


-   **Nom de clé :** BackupLocation

    -   **Obligatoire :** peut-être
    -   **Valeurs :** &lt;chemin_vers_jeu_sauvegarde_base_de_données_site\>
    -   **Détails :** spécifie le chemin d’accès au jeu de sauvegarde de la base de données du site. La clé **BackupLocation** est requise lorsque vous configurez une valeur de **1** ou **4** pour la clé **ServerRecoveryOptions** , et une valeur de **10** pour la clé **DatabaseRecoveryOptions** .

**Options**

-   **Nom de clé :** ProductID

    -   **Obligatoire :** Oui
    -   **Valeurs :**     
         xxxxx-xxxxx-xxxxx-xxxxx-xxxxx  
         Eval     
    -   **Détails :** clé de produit de l’installation de Configuration Manager avec les tirets. Entrez **Eval** pour installer la version d’évaluation de Configuration Manager.  


-   **Nom de clé :** SiteCode

    -   **Obligatoire :** Oui
    -   **Valeurs :** &lt;code_de_site\>
    -   **Détails :** trois caractères alphanumériques identifiant le site de façon univoque dans votre hiérarchie. Vous devez définir le code de site utilisé par le site avant la défaillance.


-   **Nom de clé :** SiteName

    -   **Obligatoire :** Oui
    -   **Valeurs :** nom_site
    -   **Détails :** description de ce site.


-   **Nom de clé :** SMSInstallDir

    -   **Obligatoire :** Oui
    -   **Valeurs :** &lt;*CheminInstallationConfigMgr*>
    -   **Détails :** spécifie le dossier d’installation des fichiers programmes de Configuration Manager.

        > [!NOTE]   
        >  Vous pouvez spécifier le chemin d’origine ou un nouveau chemin à utiliser pour l’installation de Configuration Manager.

-   **Nom de clé :** SDKServer

    -   **Obligatoire :** Oui
    -   **Valeurs :** &lt;*nom de domaine complet du fournisseur SMS*>
    -   **Détails :** spécifie le FQDN du serveur qui héberge le fournisseur SMS. Vous devez spécifier le serveur qui hébergeait le fournisseur SMS avant la défaillance.

         Vous pouvez configurer d'autres fournisseurs SMS pour le site après l'installation initiale.

-   **Nom de clé :** PrerequisiteComp

    -   **Obligatoire :** Oui
    -   **Valeurs :** 0 ou 1    
         0 = téléchargement   
         1 = déjà téléchargé   
    -   **Détails :** spécifie si les fichiers d’installation prérequis ont déjà été téléchargés. Par exemple, si vous utilisez la valeur 0, le programme d'installation va télécharger les fichiers.


-   **Nom de clé :** PrerequisitePath

    -   **Obligatoire :** Oui
    -   **Valeurs :** &lt;*chemin_fichiers_requis_programme_installation*>
    -   **Détails :** spécifie le chemin vers les fichiers d’installation prérequis. Selon la valeur **PrerequisiteComp** , le programme d'installation utilise ce chemin d'accès pour stocker les fichiers téléchargés ou pour localiser des fichiers précédemment téléchargés.


-   **Nom de clé :** AdminConsole

    -   **Obligatoire :** peut-être
    -   **Valeurs :** 0 ou 1  
         0 = ne pas installer   
         1 = installer  
    -   **Détails :** spécifie si la console Configuration Manager doit ou non être installée. Cette clé est obligatoire sauf quand le paramètre **ServerRecoveryOptions** a la valeur **4**.

-   **Nom de clé :** JoinCEIP

    -   **Obligatoire :** Oui
    -   **Valeurs :** 0 ou 1    
         0 = ne pas joindre  
         1 = joindre
    -   **Détails :** spécifie si vous voulez vous joindre au programme d’amélioration de l’expérience utilisateur.


**SQLConfigOptions**

-   **Nom de clé :** SQLServerName

    -   **Obligatoire :** Oui
    -   **Valeurs :** *&lt;nom_SQLServer\>*
    -   **Détails :** nom du serveur ou nom de l’instance en cluster exécutant SQL Server, et devant héberger la base de données de site. Vous devez spécifier le serveur qui a hébergé la base de données de site avant la défaillance.


-   **Nom de clé :** DatabaseName

    -   **Obligatoire :** Oui
    -   **Valeurs :** *&lt;nom_base_de_données_site\>* ou *&lt;nom_instance\>*\\*&lt;nom_base_de_données_site\>*
    -   **Détails :** nom de la base de données SQL Server à créer ou à utiliser pour installer la base de données du site d’administration centrale. Vous devez spécifier le nom de base de données qui était utilisé avant la défaillance.

        > [!IMPORTANT]    
        >  Si vous n'utilisez pas l'instance par défaut, vous devez spécifier le nom d'instance et le nom de base de données de site.

-   **Nom de clé :** SQLSSBPort

    -   **Obligatoire :** non
    -   **Valeurs :** &lt;*numéro_port_SSB*>
    -   **Détails :** spécifiez le port SQL Server Service Broker (SSB) utilisé par SQL Server. Généralement, SSB est configuré pour utiliser le port TCP 4022, mais d'autres ports sont pris en charge. Vous devez définir le même port SSB utilisé avant la défaillance.

**Option d’extension de hiérarchie**

-   **Nom de clé :** CCARSiteServer

    -   **Obligatoire :** peut-être
    -   **Valeurs :** &lt;*code_site_pour_site_administration_centrale*>
    -   **Détails :** spécifie le site d’administration centrale auquel un site principal s’attache quand il rejoint la hiérarchie Configuration Manager. Ce paramètre est requis si le site principal était attaché à un site d'administration centrale avant la défaillance. Vous devez spécifier le code de site qui était utilisé pour le site d'administration centrale avant la défaillance.

-   **Nom de clé :** CASRetryInterval

    -   **Obligatoire :** non
    -   **Valeurs :** &lt;*intervalle*>
    -   **Détails :** spécifie l’intervalle (en minutes) avant une nouvelle tentative de connexion au site d’administration centrale après un échec de connexion. Par exemple, en cas d'échec de la connexion au site d'administration centrale, le site principal attend le nombre de minutes que vous avez spécifié pour CASRetryInterval et essaie de nouveau d'établir une connexion.


-   **Nom de clé :** WaitForCASTimeout

    -   **Obligatoire :** non
    -   **Valeurs :** &lt;*délai d’attente*>
    -   **Détails :** spécifie la valeur maximale du délai d’attente (en minutes) pour qu’un site principal se connecte au site d’administration centrale. Par exemple, si un site principal ne parvient pas à se connecter à un site d'administration centrale, le site principal essaie de nouveau d'établir une connexion selon la valeur de CASRetryInterval jusqu'à ce que le délai WaitForCASTimeout soit atteint. Vous pouvez spécifier une valeur de 0 à 100.
