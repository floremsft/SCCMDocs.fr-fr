---
title: "Vérifications de la configuration requise | System Center Configuration Manager"
description: "Passez en revue les vérifications de la configuration requise pour System Center Configuration Manager. Inclut des vérifications des droits de sécurité."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6a279624-ffc9-41aa-8132-df1809708dd5
caps.latest.revision: 12
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 96787d5c4ad92d86ad9172fcfacb92fe4138c7ba


---
# <a name="list-of-prerequisite-checks-for-system-center-configuration-manager"></a>Liste des vérifications de la configuration requise pour System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Les sections suivantes détaillent les vérifications de la configuration requise disponibles.  


 Pour obtenir des informations sur l’utilisation de l’outil de vérification de la configuration requise, voir [Outil de vérification de la configuration requise](prerequisite-checker.md).  

##  <a name="a-namebkmksecuritya-prerequisite-checks-for-security-rights"></a><a name="BKMK_Security"></a> Vérifications de la configuration requise pour les droits de sécurité  
 Ci-après figure la liste des contrôles qu’effectue l’outil de vérification de la configuration requise en relation avec les droits de sécurité.  

 **Droits d’administration sur le site d’administration centrale** - Vérifie que le compte d’utilisateur exécutant le programme d’installation de Configuration Manager dispose des droits **Administrateur** local sur l’ordinateur du site d’administration centrale.  

-   **Gravité :** Erreur  

-   **Mise en application :**  
      -   Site principal  

**Droits d’administration sur le site principal développé** - Vérifie que l’utilisateur exécutant le programme d’installation dispose des droits ** Administrateur** local sur le site principal autonome qui sera étendu.  

-   **Gravité :** Erreur  

-   **Mise en application :**  

    -   Site d'administration centrale  

**Droits d’administration sur le système de site** - Vérifie que le compte d’utilisateur exécutant le programme d’installation de Configuration Manager dispose des droits **Administrateur** local sur l’ordinateur serveur de site.  

-   **Gravité :** Erreur  

-   **Mise en application :**  

    -   Site d'administration centrale  
    -   Site principal  
    -   Site secondaire  

**Droits d’administration de l’ordinateur du site d’administration centrale sur le site principal développé** - Vérifie que le compte d’ordinateur du site d’administration centrale dispose des droits **Administrateur** local sur le site principal autonome qui sera étendu.  

-   **Gravité :** Erreur  

-   **Mise en application :**  

    -   Site d'administration centrale  

**Connexion à SQL Server sur le site d’administration centrale** - Vérifie que le compte d’utilisateur exécutant le programme d’installation de Configuration Manager sur le site principal pour rejoindre une hiérarchie existante possède le rôle **sysadmin** sur l’instance SQL Server du site d’administration centrale.  

-   **Gravité :** Erreur  

-   **Mise en application :**  

    -   Site principal  

**Droits d’administration du compte de l’ordinateur serveur de site** - Vérifie que le compte de l’ordinateur serveur de site dispose de droits d’administration sur les ordinateurs SQL Server et de point de gestion.  

-   **Gravité :** Erreur  

-   **Mise en application :**  

    -   Site principal  
    -   SQL Server  

**Communication du système de site au serveur SQL Server** - Vérifie qu’un nom de principal du service (SPN) valide est inscrit dans les services de domaine Active Directory pour le compte configuré pour exécuter le service SQL Server pour l’instance SQL Server utilisée pour héberger la base de données du site Configuration Manager. Un SPN valide doit être enregistré dans les services de domaine Active Directory pour prendre en charge l'authentification Kerberos.  

-   **Gravité :** Avertissement  

-   **Mise en application :**  

    -   Site secondaire  
    -   Point de gestion  

**Mode de sécurité de SQL Server** - Vérifie que SQL Server est configuré pour la sécurité d’authentification Windows.  

-   **Gravité :** Avertissement  

-   **Mise en application :**  

    -   SQL Server  

**Droits d’administrateur système SQL Server** - Vérifie que le compte d’utilisateur exécutant le programme d’installation de Configuration Manager possède le rôle **sysadmin** sur l’instance SQL Server sélectionnée pour l’installation de la base de données du site. Cette vérification échoue également lorsque le programme d'installation ne peut pas accéder à l'instance pour que SQL Server vérifie les autorisations.  

-   **Gravité :** Erreur  

-   **Mise en application :**  

    -   SQL Server  

**Droits d’administrateur système SQL Server pour le site de référence** - Vérifie que le compte d’utilisateur exécutant le programme d’installation de Configuration Manager possède le rôle **sysadmin** sur l’instance de rôle SQL Server sélectionnée comme base de données du site de référence.  Des autorisations de rôle d' **administrateur système** SQL Server sont nécessaires pour modifier la base de données de site.  

-   **Gravité :** Erreur  

-   **Mise en application :**  

    -   SQL Server  

##  <a name="a-namebkmkdependenciesa-prerequisite-checks-for-configuration-manager-dependencies"></a><a name="BKMK_Dependencies"></a> Vérifications de la configuration requise pour les dépendances de Configuration Manager  
 Les vérifications de la configuration requise suivantes sont effectuées par l’outil de vérification de la configuration requise au niveau des dépendances de Configuration Manager.  

**Mappages de migration actifs sur le site principal cible**  

 Vérifie qu'il n'existe pas de mappages de migration actifs aux sites principaux.  

-   **Gravité :** Erreur  

-   **Mise en application :**  

    -   Site d'administration centrale  

**Réplica de point de gestion actif** - Vérifie s’il existe un réplica de point de gestion actif.  

-   **Gravité :** Erreur  

-   **Mise en application :**  

    -   Site principal  

**Droits d’administration sur le point de distribution** - Vérifie que l’utilisateur exécutant le programme d’installation dispose des droits **Administrateur** local sur l’ordinateur du point de distribution.  

-   **Gravité :** Avertissement  

-   **Mise en application :**  

    -   Point de distribution  

**Droits d’administration sur le point de gestion** - Vérifie que le compte de l’ordinateur serveur de site dispose des droits **Administrateur** sur l’ordinateur du point de gestion et du point de distribution.  

-   **Gravité :** Avertissement  

-   **Mise en application :**  

    -   Point de gestion  

**Partage administratif (Système de site)** - Vérifie que les partages administratifs obligatoires sont présents sur l’ordinateur du système de site.  

-   **Gravité :** Avertissement  

-   **Mise en application :**  

    -   Point de gestion  

**Compatibilité des applications** - Vérifie que les applications actuelles sont compatibles avec le schéma d’application.  

-   **Gravité :** Avertissement  

-   **Mise en application :**  

    -   Site d'administration centrale    
    -   Site principal  

**Compatible BITS** - Vérifie que le Service de transfert intelligent en arrière-plan (BITS) est installé sur l’ordinateur du système de site du point de gestion. L'échec de cette vérification signifie que le service BITS n'est pas installé, que le composant de compatibilité IIS 6 WMI pour IIS7 n'est pas installé sur l'ordinateur ou l'hôte IIS distant ou que le programme d'installation n'a pas pu vérifier les paramètres IIS distants, car les composants communs IIS n'étaient pas installés sur l'ordinateur serveur de site.  

-   **Gravité :** Erreur  

-   **Mise en application :**  

    -   Point de gestion  

**Service BITS installé** - Vérifie que le Service de transfert intelligent en arrière-plan (BITS) est installé dans Internet Information Services (IIS).  

-   **Gravité :** Avertissement  

-   **Mise en application :**  

    -   Point de gestion  

**Classement insensible à la casse sur SQL Server** - Vérifie que l’installation de SQL Server utilise un classement qui ne respecte pas la casse ; par exemple, SQL_Latin1_General_CP1_CI_AS.  

-   **Gravité :** Erreur  

-   **Mise en application :**  

    -   SQL Server  

**Déterminer la version et le code du site principal autonome** - Vérifie que le site principal que vous envisagez d’étendre est un site principal autonome, et qu’il dispose de la même version de Configuration Manager, mais d’un code de site différent de celui du site d’administration centrale à installer.  

-   **Gravité :** Erreur  

-   **Mise en application :**  

    -   Site d'administration centrale    
    -   Site principal  

**Vérifier les références de regroupement incompatibles** - Au cours d’une mise à niveau, cette vérification contrôle que les regroupements font uniquement référence à d’autres regroupements du même type.  

-   **Gravité :** Erreur  

-   **Mise en application :**  

    -   Site d'administration centrale  

**Version du client sur l’ordinateur du point de gestion** - Vérifie que vous installez le point de gestion sur un ordinateur dont la version ne diffère pas de celle du client Configuration Manager installé.  

-   **Gravité :** Erreur  

-   **Mise en application :**  

    -   Point de gestion  

**Configuration de l’utilisation de mémoire de SQL Server** - Vérifie si SQL Server est configuré pour une utilisation de mémoire illimitée. Vous devez configurer la mémoire de SQL Server avec une limite maximale.  

-   **Gravité :** Avertissement  

-   **Mise en application :**  

    -   SQL Server  

**Instance SQL Server dédiée** - Vérifie si une instance dédiée du serveur SQL Server est configurée pour héberger la base de données du site Configuration Manager. Si un autre site utilise l'instance, vous devez sélectionner une autre instance pour le nouveau site à utiliser. Vous pouvez également désinstaller l'autre site ou déplacer sa base de données vers une autre instance du serveur SQL Server.  

-   **Gravité :** Erreur  

-   **Mise en application :**  

    -   Site d'administration centrale    
    -   Site principal    
    -   Site secondaire  

**Composants serveur Configuration Manager existants sur le serveur** - Vérifie qu’un rôle de serveur de site ou de système de site n’est pas déjà installé sur l’ordinateur sélectionné pour l’installation du site.  

-   **Gravité :** Erreur  

-   **Mise en application :**  

    -   Site d'administration centrale    
    -   Site principal    
    -   Site secondaire  

**Exception de pare-feu pour SQL Server** - Vérifie si le Pare-feu Windows est désactivé ou s’il existe une exception de Pare-feu Windows pertinente pour SQL Server. Vous devez autoriser l'accès à distance à sqlservr.exe ou aux ports TCP requis. Par défaut, SQL Server écoute le port TCP 1433 et SQL Broker Service utilise le port TCP 4022.  

-   **Gravité :** Erreur  

-   **Mise en application :**  

    -   Site d'administration centrale    
    -   Site principal    
    -   Site secondaire    
    -   Point de gestion  

**Exception de pare-feu pour SQL Server (site principal autonome)** - Vérifie si le Pare-feu Windows est désactivé ou s’il existe une exception de Pare-feu Windows pertinente pour SQL Server. Vous devez autoriser l'accès à distance à sqlservr.exe ou aux ports TCP requis. Par défaut, SQL Server écoute le port TCP 1433 et SQL Broker Service utilise le port TCP 4022.  

-   **Gravité :** Avertissement  

-   **Mise en application :**  

    -   Site principal (autonome uniquement)  

**Exception de pare-feu pour SQL Server pour le point de gestion** - Vérifie si le Pare-feu Windows est désactivé ou s’il existe une exception de Pare-feu Windows pertinente pour SQL Server.  

-   **Gravité :** Avertissement  

-   **Mise en application :**  

    -   Point de gestion  

**Configuration HTTPS IIS** - Vérifie les liaisons de site web Internet Information Services (IIS) pour le protocole de communication HTTPS. Lorsque vous choisissez d'installer des rôles de site qui requièrent HTTPS, vous devez configurer les liaisons de site IIS sur le serveur spécifié avec un certificat PKI valide.  

-   **Gravité :** Avertissement  

-   **Mise en application :**  

    -   Point de gestion    
    -   Point de distribution  

**Service IIS en cours d’exécution** - Vérifie qu’Internet Information Services (IIS) est installé et en cours d’exécution sur l’ordinateur pour installer le point de gestion ou le point de distribution.  

-   **Gravité :** Erreur  

-   **Mise en application :**  

    -   Point de gestion    
    -   Point de distribution  

**Reproduire le classement du site principal développé** - Vérifie que la base de données du site pour le site principal autonome que vous allez étendre possède le même classement que la base de données du site au niveau du site d’administration centrale.  

-   **Gravité :** Erreur  

-   **Mise en application :**  

    -   Site d'administration centrale  

**Bibliothèque RDC (compression différentielle à distance) de Microsoft enregistrée** - Vérifie que la bibliothèque RDC (compression différentielle à distance) de Microsoft est enregistrée sur le serveur de site Configuration Manager.  

-   **Gravité :** Erreur  

-   **Mise en application :**  

    -   Site d'administration centrale    
    -   Site principal    
    -   Site secondaire  

**Microsoft Windows Installer** - Vérifie la version de Windows Installer. L'échec de cette vérification signifie que le programme d'installation n'a pas pu vérifier la version ou que la version installée n'est pas conforme à la configuration minimale requise de Windows Installer version 4.5.  

-   **Gravité :** Erreur  

-   **Mise en application :**  

    -   Site d'administration centrale    
    -   Site principal    
    -   Site secondaire  

**Microsoft XML Core Services 6.0 (MSXML60)** - Vérifie que Microsoft Core XML Services (MSXML) version 6.0 ou ultérieure est installé sur l’ordinateur.  

-   **Gravité :** Avertissement  

-   **Mise en application :**  

    -   Site d'administration centrale    
    -   Site principal    
    -   Site secondaire    
    -   Console Configuration Manager    
    -   Point de gestion    
    -   Point de distribution  

**Version minimale de .NET Framework pour la console** - Vérifie si Microsoft .NET Framework version 4.0 est installé sur l’ordinateur de la console Configuration Manager. Vous pouvez télécharger Microsoft .NET Framework version 4.0 à partir du [Centre de téléchargement Microsoft](http://go.microsoft.com/fwlink/p/?LinkId=189149).  

-   **Gravité :** Erreur  

-   **Mise en application :**  

    -   Console Configuration Manager  

**Version minimale de .NET Framework pour la console** - Vérifie si Microsoft .NET Framework version 3.5 est installé sur l’ordinateur de la console Configuration Manager. Pour Windows Server 2008, vous pouvez télécharger la version 3.5 de Microsoft .NET Framework depuis le [Centre de téléchargement Microsoft](http://go.microsoft.com/fwlink/p/?LinkId=185604). Pour Windows Server 2008 R2, vous pouvez activer Microsoft .NET Framework version 3.5 en tant que fonctionnalité dans le Gestionnaire de serveur.  

-   **Gravité :** Erreur  

-   **Mise en application :**  

    -   Site d'administration centrale    
    -   Site principal    
    -   Site secondaire  

**Version .NET Framework minimale pour l’installation de l’édition SQL Server Express pour un site secondaire Configuration Manager** - Vérifie que Microsoft .NET Framework version 4.0 est installé sur les ordinateurs du site secondaire Configuration Manager pour l’installation de SQL Server Express Edition.  

-   **Gravité :** Erreur  

-   **Mise en application :**  

    -   Site secondaire  

**Classement de base de données parent/enfant** - Vérifie que le classement de la base de données du site correspond au classement de la base de données du site parent. Tous les sites d'une même hiérarchie doivent utiliser le même classement de base de données.  

-   **Gravité :** Erreur  

-   **Mise en application :**  

    -   Site principal    
    -   Site secondaire  

**PowerShell 2.0 sur le serveur de site** - Vérifie que Windows PowerShell version 2.0 ou ultérieure est installé sur le serveur de site pour le connecteur Exchange de Configuration Manager. Pour plus d'informations sur PowerShell 2.0, consultez [l'article 968930](http://go.microsoft.com/fwlink/p/?LinkId=226450) de la base de connaissances Microsoft.  

-   **Gravité :** Avertissement  

-   **Mise en application :**  

    -   Site principal  

**Nom de domaine complet principal** - Vérifie que le nom NetBIOS de l’ordinateur correspond au nom d’hôte local (première étiquette du nom de domaine complet) de l’ordinateur.  

-   **Gravité :** Erreur  

-   **Mise en application :**  

    -   Site d'administration centrale    
    -   Site principal    
    -   Site secondaire    
    -   SQL Server  

**Connexion à distance avec WMI sur le site secondaire** - Vérifie si le programme d’installation peut établir une connexion à distance avec WMI sur le serveur de site secondaire.  

-   **Gravité :** Avertissement  

-   **Mise en application :**  

    -   Site secondaire  

**Classement SQL Server requis** - Vérifie que l’instance pour SQL Server et la base de données du site Configuration Manager, si elle est installée, est configurée pour utiliser le classement SQL_Latin1_General_CP1_CI_AS, sauf si vous utilisez un système d’exploitation de langue chinoise qui nécessite la prise en charge de la norme GB18030.  

 Pour plus d'informations sur la modification des classements de votre instance SQL Server et des bases de données, voir [Définition et modification des classements](http://go.microsoft.com/fwlink/p/?LinkID=234541) dans la documentation en ligne de SQL Server 2008 R2.  Pour plus d’informations sur l’activation de la prise en charge de la norme GB18030, consultez [Prise en charge internationale dans System Center Configuration Manager](../../../../core/plan-design/hierarchy/international-support.md).  

-   **Gravité :** Erreur  

-   **Mise en application :**  

    -   Site d'administration centrale    
    -   Site principal    
    -   Site secondaire  

**Dossier source d’installation** - Vérifie que le compte d’ordinateur du site secondaire dispose d’autorisations de système de fichiers NFTS en **Lecture** et d’autorisations de partage en **Lecture** sur le dossier source d’installation et le partage.  

> [!NOTE]  
>  Le compte d'ordinateur de site secondaire doit être un administrateur sur l'ordinateur si vous utilisez des partages administratifs (par exemple, C$ et D$).  

-   **Gravité :** Erreur  

-   **Mise en application :**  

    -   Site secondaire  

**Version de la source d’installation** - Vérifie que la version de Configuration Manager dans le dossier source que vous avez spécifié pour l’installation du site secondaire correspond à la version de Configuration Manager du site principal.  

-   **Gravité :** Erreur  

-   **Mise en application :**  

    -   Site secondaire  

**Code de site en cours d’utilisation** - Vérifie que le code de site que vous avez spécifié n’est pas en cours d’utilisation dans la hiérarchie Configuration Manager. Vous devez spécifier un code de site unique pour ce site.  

-   **Gravité :** Erreur  

-   **Mise en application :**  

    -   Site principal  

**L’ordinateur du fournisseur SMS a le même domaine que le serveur de site** - Vérifie si un ordinateur exécutant une instance du fournisseur SMS a le même domaine que le serveur de site.  

-   **Gravité :** Erreur  

-   **Mise en application :**  

    -   fournisseur SMS  

**Édition SQL Server** - Vérifie que l’édition de SQL Server sur le site n’est pas SQL Server Express.  

-   **Gravité :** Erreur  

-   **Mise en application :**  

    -   SQL Server  

**SQL Server Express sur un site secondaire** - Vérifie que SQL Server Express peut s’installer correctement sur l’ordinateur serveur de site pour un site secondaire.  

-   **Gravité :** Erreur  

-   **Mise en application :**  

    -   Site secondaire  

**SQL Server sur l’ordinateur du site secondaire** - Vérifie que SQL Server est installé sur l’ordinateur du site secondaire. L'installation de SQL Server sur un système de site distant n'est pas prise en charge.  

> [!WARNING]  
>  Cette vérification s'applique uniquement lorsque vous indiquez au programme d'installation d'utiliser une instance existante de SQL Server.  

-   **Gravité :** Erreur  

-   **Mise en application :**  

    -   Site secondaire  

**Allocation de mémoire pour le processus SQL Server** - Vérifie que SQL Server réserve un minimum de 8 Go de mémoire pour le site d’administration centrale et le site principal, ainsi qu’un minimum de 4 Go de mémoire pour le site secondaire. Pour plus d'informations sur la définition d'une quantité fixe de mémoire à l'aide de SQL Server Management Studio, consultez [Procédure : définir une quantité fixe de mémoire (SQL Server Management Studio)](http://go.microsoft.com/fwlink/p/?LinkId=233759).  

> [!NOTE]  
>  Cette vérification n'est pas applicable à SQL Server Express sur un site secondaire qui est limité à 1 Go de mémoire réservée.  

-   **Gravité :** Avertissement  

-   **Mise en application :**  

    -   SQL Server  

**Compte en cours d’exécution du service SQL Server** - Vérifie que le compte d’ouverture de session pour le service SQL Server n’est pas un compte d’utilisateur local ou SERVICE LOCAL. Vous devez configurer le service SQL Server pour utiliser un compte de domaine valide, SERVICE RÉSEAU ou SYSTÈME LOCAL.  

-   **Gravité :** Erreur  

-   **Mise en application :**  

    -   Site d'administration centrale    
    -   Site principal    
    -   Site secondaire  

**Port TCP SQL Server** - Vérifie que le protocole TCP est activé pour SQL Server et qu’il est configuré pour utiliser un port statique.  

-   **Gravité :** Erreur  

-   **Mise en application :**  

    -   SQL Server  

**Version de SQL Server** - Vérifie qu’une version prise en charge de SQL Server est installée sur le serveur de bases de données du site spécifié. Pour plus d’informations, consultez [Prise en charge des versions de SQL Server pour System Center Configuration Manager](../../../../core/plan-design/configs/support-for-sql-server-versions.md).  

-   **Gravité :** Erreur  

-   **Mise en application :**  

    -   SQL Server  

**Version de système d’exploitation de système de site non prise en charge pour la mise à niveau** - Pendant une mise à niveau, cette règle vérifie si des rôles de système de site autres que des points de distribution sont installés sur les ordinateurs exécutant Windows Server 2008 ou une version antérieure.  

> [!NOTE]  
>  Étant donné que cette vérification ne peut pas résoudre l’état des rôles de système de site installés dans Azure ou pour le stockage cloud utilisé par Microsoft Intune quand vous intégrez Intune avec Configuration Manager, vous pouvez ignorer les avertissements pour ces rôles comme faux positifs.  

-   **Gravité :** Avertissement  

-   **Mise en application :**  

    -   Site principal    
    -   Site secondaire  

**Rôle de système de site « Point de synchronisation Asset Intelligence » non pris en charge sur le site principal développé** - Vérifie que le rôle de système de site de point de synchronisation Asset Intelligence n’est pas installé sur le site principal autonome que vous développez.  

-   **Gravité :** Erreur  

-   **Mise en application :**  

    -   Site d'administration centrale  

**Rôle de système de site « Point Endpoint Protection » non pris en charge sur le site principal développé** - Vérifie que le rôle de système de site de point Endpoint Protection n’est pas installé sur le site principal autonome que vous développez.  

-   **Gravité :** Erreur  

-   **Mise en application :**  

    -   Site d'administration centrale  

<a name="-head"></a><<<<<<< HEAD
=======

>>>>>>> 5e8e486ea74f66a92696c65e3367aec2e592b001 **Rôle de système de site « Connecteur Microsoft Intune » non pris en charge sur le site principal développé** - Vérifie que le rôle de système site « Connecteur Microsoft Intune » n’est pas installé sur le site principal autonome que vous développez.  

-   **Gravité :** Erreur  

-   **Mise en application :**  

    -   Site d'administration centrale  

**Outil de migration utilisateur (USMT) installé** - Vérifie si le composant Outil de migration utilisateur (USMT) du Kit de déploiement et d’évaluation Windows (ADK) pour Windows 8.1 est installé.  

-   **Gravité :** Erreur  

-   **Mise en application :**  

    -   Site d'administration centrale    
    -   Site principal (autonome uniquement)  

**Valider le nom de domaine complet de l’ordinateur SQL Server** - Vérifie que le nom de domaine complet spécifié pour l’ordinateur SQL Server est valide.  

-   **Gravité :** Erreur  

-   **Mise en application :**  

    -   SQL Server  

**Vérifier la version du site d’administration centrale** - Vérifie que le site d’administration centrale dispose de la même version de Configuration Manager.  

-   **Gravité :** Erreur  

-   **Mise en application :**  

    -   Site principal  

**Vérifier que le serveur de site dispose des autorisations requises pour être publié dans Active Directory** - Vérifie que le compte d’ordinateur du serveur de site dispose des autorisations **Contrôle total** sur le conteneur **System Management** dans le domaine Active Directory. Pour plus d’informations sur les options de configuration des autorisations requises, consultez [Étendre le schéma Active Directory pour System Center Configuration Manager](../../../../core/plan-design/network/extend-the-active-directory-schema.md).  

> [!NOTE]  
>  Vous pouvez ignorer cet avertissement si vous avez vérifié manuellement les autorisations.  

-   **Gravité :** Avertissement  

-   **Mise en application :**  

    -   Site d'administration centrale    
    -   Site principal    
    -   Site secondaire  

**Outils de déploiement Windows installés** - Vérifie si le composant Outils de déploiement Windows du Kit de déploiement et d’évaluation Windows (ADK) pour Windows 10 est installé.  

-   **Gravité :** Erreur  

-   **Mise en application :**  

    -   fournisseur SMS  

**Cluster de basculement Windows** - Vérifie que les ordinateurs avec un point de gestion ou un point de distribution ne font pas partie d’un cluster Windows.  

-   **Gravité :** Erreur  

-   **Mise en application :**  

    -   Point de gestion    
    -   Point de distribution  

**Environnement de préinstallation Windows installé** - Vérifie si le composant Environnement de préinstallation Windows du Kit de déploiement et d’évaluation Windows (ADK) pour Windows 10 est installé.  

-   **Gravité :** Erreur  

-   **Mise en application :**  

    -   fournisseur SMS  

**Gestion à distance de Windows (WinRM) version 1.1** - Vérifie que WinRM v1.1 est installé sur le serveur de site principal ou sur l’ordinateur de la console Configuration Manager pour exécuter la console de gestion hors bande. Pour plus d'informations sur le téléchargement de WinRM 1.1, voir [l'article 936059](http://go.microsoft.com/fwlink/p/?LinkId=247166) de la base de connaissances Microsoft.  

-   **Gravité :** Avertissement  

-   **Mise en application :**  

    -   Site principal    
    -   Console Configuration Manager  

**WSUS sur le serveur de site** - Vérifie que Windows Server Update Services (WSUS) version 3.0 Service Pack 2 est installé sur le serveur de site. Lorsque vous utilisez un point de mise à jour logicielle sur un ordinateur autre que le serveur de site, vous devez installer la console d'administration WSUS sur le serveur de site. Pour plus d'informations sur WSUS, voir la page Web [Windows Server Update Services (Services de mise à jour de Windows Server)](http://go.microsoft.com/fwlink/p/?LinkID=79477) .  

-   **Gravité :** Avertissement  

-   **Mise en application :**  

    -   Site d'administration centrale    
    -   Site principal  

##  <a name="a-namebkmkrequirementsa-prerequisite-checks-for-system-requirements"></a><a name="BKMK_Requirements"></a> Vérifications de la configuration système requise  
 Ci-après figure la liste des contrôles qu’effectue l’outil de vérification de la configuration requise en relation avec la configuration système requise.  

**Vérification du niveau fonctionnel du domaine Active Directory** - Vérifie que le niveau fonctionnel du domaine Active Directory est au moins Windows Server 2008 R2.  

-   **Gravité :** Avertissement  

-   **Mise en application :**  

    -   Site d'administration centrale    
    -   Site principal  

**Vérifier que le service de serveur est en cours d’exécution** - Vérifie que le service de serveur est démarré.  

-   **Gravité :** Erreur  

-   **Mise en application :**  

    -   Site d'administration centrale    
    -   Site principal    
    -   Site secondaire  

**Appartenance au domaine** - Vérifie que l’ordinateur Configuration Manager est membre d’un domaine Windows.  

-   **Gravité :** Erreur  

-   **Mise en application :**  

    -   Site d'administration centrale    
    -   Site principal    
    -   Site secondaire    
    -   Fournisseur SMS    
    -   SQL Server  

**Appartenance au domaine** - Vérifie que l’ordinateur Configuration Manager est membre d’un domaine Windows.  

-   **Gravité :** Avertissement  

-   **Mise en application :**  

    -   Point de gestion    
    -   Point de distribution  

**Lecteur FAT sur le serveur de site** - Vérifie si le lecteur de disque est formaté avec le système de fichiers FAT. Installez les composants de serveur de site sur les disques formatés avec le système de fichiers NTFS pour une meilleure sécurité.  

-   **Gravité :** Avertissement  

-   **Mise en application :**  

    -   Site principal  

**Espace disque disponible sur le serveur de site** - L’ordinateur du serveur de site doit disposer d’au moins 5 Go d’espace disque disponible pour installer le serveur de site. Vous devez disposer de 1 Go d'espace disponible supplémentaire si vous installez le rôle de système de site de fournisseur SMS sur le même ordinateur.  

-   **Gravité :** Erreur  

-   **Mise en application :**  

    -   Site d'administration centrale    
    -   Site principal    
    -   Site secondaire  

**Redémarrage du système en attente** - Vérifie si un autre programme nécessite le redémarrage du serveur avant d’exécuter le programme d’installation.  

-   **Gravité :** Erreur  

-   **Mise en application :**  

    -   Site d'administration centrale    
    -   Site principal    
    -   Site secondaire  
    -   Console Configuration Manager    
    -   fournisseur SMS    
    -   SQL Server    
    -   Point de gestion    
    -   Point de distribution  

**Contrôleur de domaine en lecture seule** - Les serveurs de bases de données du site et les serveurs de site secondaire ne sont pas pris en charge sur un contrôleur de domaine en lecture seule (RODC). Pour plus d'informations, voir [Vous pouvez rencontrer des problèmes lors de l'installation de SQL Server sur un contrôleur de domaine](http://go.microsoft.com/fwlink/p/?LinkId=264856) dans la Base de connaissances Microsoft.  

-   **Gravité :** Erreur  

-   **Mise en application :**  

    -   Site d'administration centrale    
    -   Site principal    
    -   Site secondaire  

**Extensions de schéma** - Détermine si le schéma des services de domaine Active Directory a été étendu et, le cas échéant, la version des extensions de schéma utilisées. Les extensions de schéma Active Directory de Configuration Manager ne sont pas requises pour installer le serveur de site, mais sont recommandées pour prendre pleinement en charge l'utilisation des fonctionnalités de Configuration Manager. Pour plus d’informations sur les avantages offerts par l’extension du schéma, consultez [Étendre le schéma Active Directory pour System Center Configuration Manager](../../../../core/plan-design/network/extend-the-active-directory-schema.md).  

-   **Gravité :** Avertissement  

-   **Mise en application :**  

    -   Site d'administration centrale    
    -   Site principal  

**Longueur du nom de domaine complet du serveur de site** - Vérifie la longueur du nom de domaine complet de l’ordinateur du serveur de site.  

-   **Gravité :** Erreur  

-   **Mise en application :**  

    -   Site d'administration centrale    
    -   Site principal    
    -   Site secondaire  

**Système d’exploitation de la console Configuration Manager non pris en charge** - Vérifie que les consoles Configuration Manager peuvent être installées sur des ordinateurs exécutant une version prise en charge du système d’exploitation. Pour plus d’informations, voir [Systèmes d’exploitation pris en charge pour les consoles System Center Configuration Manager](/sccm/core/plan-design/configs/supported-operating-systems-consoles).  

-   **Gravité :** Erreur  

-   **Mise en application :**  

    -   Console Configuration Manager  

**Version du système d’exploitation du serveur de site non prise en charge pour l’installation** - Vérifie qu’un système d’exploitation pris en charge s’exécute sur le serveur. Pour plus d’informations, consultez [Systèmes d’exploitation pris en charge pour les sites et les clients pour System Center Configuration Manager](/sccm/core/plan-design/configs/supported-operating-systems-for-site-system-servers).  

-   **Gravité :** Erreur  

-   **Mise en application :**  

    -   Site d'administration centrale    
    -   Site principal    
    -   Site secondaire    
    -   Console Configuration Manager    
    -   Point de gestion    
    -   Point de distribution  

**Vérifier la cohérence de la base de données** - À partir la version 1602, ce contrôle vérifie la cohérence de la base de données.  

-   **Gravité :** Erreur  

-   **Mise en application :**  

    -   Site d'administration centrale    
    -   Site principal  



<!--HONumber=Nov16_HO1-->


