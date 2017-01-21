---
title: "Outil de vérification des conditions préalables | System Center Configuration Manager"
description: "Apprenez à utiliser l’outil de vérification des conditions préalables pour identifier et résoudre les problèmes susceptibles de bloquer l’installation d’un site ou d’un rôle de système de site."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: aaf13bb8-4ba2-4bd7-9fac-d36a9d88a1b6
caps.latest.revision: 3
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 4c2322ed0805b5f087409ec487ebec9d7c4f10d5

---
# <a name="prerequisite-checker-for-system-center-configuration-manager"></a>Outil de vérification des conditions préalables pour System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*


 Avant d’exécuter le programme d’installation pour installer ou mettre à niveau un site System Center Configuration Manager, ou avant d’installer un rôle de système de site sur un nouveau serveur, vous pouvez utiliser cette application autonome (**Prereqchk.exe**) de la version de Configuration Manager que vous voulez utiliser pour vérifier l’état de préparation du serveur. L’outil de vérification des conditions préalables permet d’identifier et de résoudre les problèmes susceptibles de bloquer l’installation d’un site ou d’un rôle de système de site.  

> [!NOTE]  
>  L’outil de vérification des conditions préalables s’exécute toujours dans le cadre de l’installation.  

Par défaut, quand l’outil de vérification des conditions préalables s’exécute :  

-   Il valide le serveur sur lequel il s’exécute.  

-   Il recherche la présence d’un serveur de site sur l’ordinateur local et il exécute uniquement les vérifications applicables au site.  

-   S’il ne détecte aucun site existant, il exécute toutes les règles de vérification des conditions préalables.  

-   Il vérifie les règles pour s’assurer de la présence des logiciels et des paramètres nécessaires à l’installation. Il est possible qu’un logiciel requis nécessite des configurations ou des mises à jour logicielles supplémentaires qui ne sont pas vérifiées par l’outil de vérification des conditions préalables.  

-   Il enregistre ses résultats dans le fichier journal **ConfigMgrPrereq.log** sur le lecteur système de l’ordinateur. Le fichier journal peut contenir des informations supplémentaires qui ne s'affichent pas dans l'interface utilisateur.  

Quand vous exécutez l’outil de vérification des conditions préalables à l’invite de commandes et spécifiez des options de ligne de commande :  

-   L’outil de vérification des conditions préalables effectue uniquement les vérifications associées au serveur de site ou aux systèmes de site que vous avez spécifiés dans la ligne de commande.  

-   Pour vérifier un ordinateur distant, votre compte d’utilisateur doit disposer des droits d’administration sur cet ordinateur.  

Pour plus d’informations sur les vérifications effectuées par l’outil de vérification des conditions préalables, consultez [Liste des vérifications des conditions préalables pour System Center Configuration Manager](../../../../core/servers/deploy/install/list-of-prerequisite-checks.md).  

## <a name="copy-prerequisite-checker-files-to-another-computer"></a>Copier les fichiers de l’outil de vérification des conditions préalables vers un autre ordinateur  

1.  Dans l'Explorateur Windows, accédez à l'un des emplacements suivants :  

    -   **&lt;Média_Installation_ConfigMgr\>\SMSSETUP\BIN\X64**  

    -   **&lt;Chemin_Installation_ConfigMgr\>\BIN\X64**  

2.  Copiez les fichiers suivants vers le dossier de destination sur l'autre ordinateur :  

    -   Prereqchk.exe  

    -   Prereqcore.dll  

    -   Basesql.dll  

    -   Basesvr.dll  

    -   Baseutil.dll  

##  <a name="run-prerequisite-checker-with-default-checks"></a>Exécuter l’outil de vérification des conditions préalables avec les vérifications par défaut  

1.  Dans l'Explorateur Windows, accédez à l'un des emplacements suivants :  

    -   **&lt;Média_Installation_ConfigMgr\>\SMSSETUP\BIN\X64**  

    -   **&lt;Chemin_Installation_ConfigMgr\>\BIN\X64**  

2.  Exécutez **prereqchk.exe** pour démarrer l’outil de vérification des conditions préalables.   
    L'outil de vérification des conditions préalables détecte les sites existants et, une fois identifiés, vérifie s'ils sont prêts pour une mise à niveau. Si aucun site n'est trouvé, toutes les vérifications sont effectuées. La colonne **Type de site** fournit des informations sur le serveur de site ou le système de site auquel la règle est associée.  

##  <a name="run-prerequisite-checker-from-a-command-prompt-for-all-default-checks"></a>Exécuter l’outil de vérification des conditions préalables à partir d’une invite de commandes pour toutes les vérifications par défaut  

1.  Ouvrez une fenêtre d’invite de commandes, puis accédez à l’un des répertoires suivants :  

    -   **&lt;Média_Installation_ConfigMgr\>\SMSSETUP\BIN\X64**  

    -   **&lt;Chemin_Installation_ConfigMgr\>\BIN\X64**  

2.  Entrez  **prereqchk.exe /LOCAL** pour démarrer l’outil de vérification des conditions préalables et effectuer toutes les vérifications requises sur le serveur.  

## <a name="run-prerequisite-checker-from-a-command-prompt-for-specified-options"></a>Exécuter l’outil de vérification des conditions préalables à partir d’une invite de commandes pour les options spécifiées  

1.  Ouvrez une fenêtre d’invite de commandes, puis accédez à l’un des répertoires suivants :  

    -   **&lt;Média_Installation_ConfigMgr\>\SMSSETUP\BIN\X64**  

    -   **&lt;Chemin_Installation_ConfigMgr\>\BIN\X64**  

2.  Entrez **prereqchk.exe** en ajoutant une ou plusieurs des options de ligne de commande suivantes.  

    Par exemple, pour vérifier un site principal, vous pouvez entrer la ligne de commande suivante :  

    -   **prereqchk.exe [/NOUI] /PRI /SQL &lt;Nom de domaine complet de SQL Server\> /SDK &lt;Nom de domaine complet du fournisseur SMS\> [/JOIN &lt;Nom de domaine complet du site d’administration centrale\>] [/MP &lt;Nom de domaine complet du point de gestion\>] [/DP &lt;Nom de domaine complet du point de distribution\>]**  

    **Serveur de site d’administration centrale** :  

    -   **/NOUI**  

         Non obligatoire - Démarre l’outil de vérification des conditions préalables sans afficher l’interface utilisateur. Vous devez spécifier cette option avant toute autre option dans la ligne de commande.  

    -   **/CAS**  

         Obligatoire - Vérifie que l’ordinateur local présente la configuration requise pour le site d’administration centrale.  

    -   **/SQL &lt;*Nom de domaine complet de SQL Server*>**  

         Obligatoire - Vérifie que l’ordinateur spécifié présente la configuration requise pour que SQL Server puisse héberger la base de données du site Configuration Manager.  

    -   **/SDK &lt;*Nom de domaine complet du fournisseur SMS*>**  

         Obligatoire - Vérifie que l’ordinateur spécifié présente la configuration requise pour le fournisseur SMS.  

    -   **/Ssbport**  

         Non obligatoire - Vérifie qu’une exception de pare-feu est configurée pour permettre la communication sur le port SSB. La valeur par défaut est le port numéro 4022.  

    -   **Rép_Install&lt;*Chemin_Installation_ConfigMgr*>**  

         Non obligatoire - Vérifie l’espace disque minimum requis pour l’installation du site.  

    **Serveur de site principal** :  

    -   **/NOUI**  

        Non obligatoire - Démarre l’outil de vérification des conditions préalables sans afficher l’interface utilisateur. Vous devez spécifier cette option avant toute autre option dans la ligne de commande.  

    -   **/PRI**  

         Obligatoire - Vérifie que l’ordinateur local présente la configuration requise pour le site principal.  

    -   **/SQL &lt;*Nom de domaine complet de SQL Server*>**  

         Obligatoire - Vérifie que l’ordinateur spécifié présente la configuration requise pour que SQL Server puisse héberger la base de données du site Configuration Manager.  

    -   **/SDK &lt;*Nom de domaine complet du fournisseur SMS*>**  

         Obligatoire - Vérifie que l’ordinateur spécifié présente la configuration requise pour le fournisseur SMS.  

    -   **/JOIN &lt;*Nom de domaine complet du site d’administration centrale*>**  

         Non obligatoire - Vérifie que l’ordinateur local présente la configuration requise pour se connecter au serveur de site d’administration centrale.  

    -   **/MP &lt;*Nom de domaine complet du point de gestion*>**  

         Non obligatoire - Vérifie que l’ordinateur spécifié présente la configuration requise pour le rôle système de site de point de gestion. Cette option est prise en charge uniquement avec l’option **/PRI** .  

    -   **/DP &lt;*Nom de domaine complet du point de distribution*>**  

         Non obligatoire - Vérifie que l’ordinateur spécifié présente la configuration requise pour le rôle système de site de point de distribution. Cette option est prise en charge uniquement avec l’option **/PRI** .  

    -   **/Ssbport**  

         Non obligatoire - Vérifie qu’une exception de pare-feu est configurée pour permettre la communication sur le port SSB. La valeur par défaut est le port numéro 4022.  

    -   **Rép_Install&lt;*Chemin_Installation_ConfigMgr*>**  

         Non obligatoire - Vérifie l’espace disque minimum requis pour l’installation du site.  

    **Serveur de site secondaire** :  

    -   **/NOUI**  

         Non obligatoire - Démarre l’outil de vérification des conditions préalables sans afficher l’interface utilisateur. Vous devez spécifier cette option avant toute autre option dans la ligne de commande.  

    -   **/SEC &lt;*Nom de domaine complet du serveur de site secondaire*>**  

         Obligatoire - Vérifie que l’ordinateur spécifié présente la configuration requise pour le site secondaire.  

    -   **/INSTALLSQLEXPRESS**  

         Non obligatoire - Vérifie que SQL Server Express peut être installé sur l’ordinateur spécifié.  

    -   **/Ssbport**  

         Non obligatoire -      
        Vérifie qu'une exception de pare-feu est en place pour autoriser la communication pour le port SQL Server Service Broker (SSB). La valeur par défaut est le port numéro 4022.  

    -   **/Sqlport**  

         Non obligatoire - Vérifie qu’une exception de pare-feu est configurée pour permettre la communication pour le port de service SQL Server et que le port n’est pas utilisé par une autre instance nommée de SQL Server. Le port par défaut est 1433.  

    -   **Rép_Install&lt;*Chemin_Installation_ConfigMgr*>**  

         Non obligatoire - Vérifie l’espace disque minimum requis pour l’installation du site.  

    -   **/SourceDir**  

         Non obligatoire - Vérifie que le compte d’ordinateur du site secondaire peut accéder au dossier hébergeant les fichiers sources d’installation.  

     **Console Configuration Manager** :  

    -   **/Adminui**  

         Obligatoire - Vérifie que l’ordinateur local présente la configuration requise pour l’installation de Configuration Manager.  

3.  L’interface utilisateur de l’outil de vérification des conditions préalables affiche la liste des problèmes détectés dans la section **Résultat de la vérification de configuration requise** .  

    -   Cliquez sur un élément de la liste pour obtenir plus d'informations sur la façon de résoudre le problème.  

    -   Vous devez résoudre tous les éléments de la liste qui présentent un état **Erreur** avant d’installer le serveur de site, le système de site ou la console Configuration Manager.  

    -   Vous pouvez également ouvrir le fichier **ConfigMgrPrereq.log** à la racine du lecteur système pour examiner les résultats de l’outil de vérification des conditions préalables. Le fichier journal peut contenir des informations supplémentaires qui ne s'affichent pas dans l'interface utilisateur.  



<!--HONumber=Nov16_HO1-->


