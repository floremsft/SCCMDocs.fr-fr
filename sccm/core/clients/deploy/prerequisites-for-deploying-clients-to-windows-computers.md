---
title: "Prérequis au déploiement de clients Windows | Microsoft Docs"
description: "Découvrez la configuration requise pour déployer des clients sur des ordinateurs Windows dans System Center Configuration Manager."
ms.custom: na
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-client
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 1a2a9b48-a95b-4643-b00c-b3079584ae2e
caps.latest.revision: "16"
caps.handback.revision: "0"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 6636ce4d929326fad0210407d7634ea585eb0a2d
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/07/2017
---
# <a name="prerequisites-for-deploying-clients-to-windows-computers-in-system-center-configuration-manager"></a>Configuration requise pour le déploiement de clients sur des ordinateurs Windows dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Le déploiement de clients Configuration Manager dans votre environnement présente des dépendances externes et internes au produit, comme décrit ci-dessous. En outre, chaque méthode de déploiement client possède ses propres dépendances qui doivent être respectées pour le bon déroulement des installations clients.  

  Consultez également la rubrique [Configurations prises en charge pour System Center Configuration Manager](../../../core/plan-design/configs/supported-configurations.md) pour vous assurer que les appareils présentent la configuration minimale requise (matériel et système d’exploitation) pour le client Configuration Manager.  

 Pour plus d’informations sur la configuration requise pour le client Configuration Manager pour Linux et UNIX, consultez [Planification du déploiement de clients sur des ordinateurs Linux et UNIX dans System Center Configuration Manager](../../../core/clients/deploy/plan/planning-for-client-deployment-to-linux-and-unix-computers.md).  

> [!NOTE]  
>  Les numéros de version de logiciel mentionnés dans cet article indiquent uniquement les numéros de version minimale requise.  

##  <a name="BKMK_prereqs_computers"></a> Conditions préalables pour les clients d’ordinateurs  
 Aidez-vous des informations suivantes pour déterminer la configuration requise pour installer le client Configuration Manager sur des ordinateurs.  

### <a name="dependencies-external-to-configuration-manager"></a>Dépendances externes à Configuration Manager  

|||  
|-|-|  
|Windows Installer version 3.1.4000.2435|Obligatoire pour prendre en charge l'utilisation des fichiers de mise à jour (.msp) Windows Installer pour les packages et les mises à jour logicielles.|  
|[KB2552033](http://go.microsoft.com/fwlink/p/?LinkId=240048)|Installez ce correctif sur les serveurs de site exécutant Windows Server 2008 R2 quand l’installation Push du client est activée.|  
|Service Microsoft BITS (Background Intelligent Transfer Service) version 2.5|Requis pour autoriser le transfert contrôlé des données entre l’ordinateur client et les systèmes de site Configuration Manager. BITS n'est pas automatiquement téléchargé lors de l'installation du client. Lorsque le service BITS est installé sur les ordinateurs, un redémarrage est généralement nécessaire pour terminer l'installation.<br /><br /> La plupart des systèmes d’exploitation intègrent le service BITS. Si cela n’est pas le cas, comme Windows Server 2003 R2 SP2, par exemple, vous devez installer ce service avant d’installer le client Configuration Manager.|  
|Planificateur de tâches Microsoft|Activez ce service sur le client pour accomplir l’installation du client.|  

### <a name="dependencies-external-to-configuration-manager-and-automatically-downloaded-during-installation"></a>Dépendances extérieures à Configuration Manager et téléchargées automatiquement lors de l'installation  
 Le client Configuration Manager présente plusieurs dépendances externes potentielles. Ces dépendances dépendent du système d'exploitation et du logiciel installé sur l'ordinateur client.  

 Si elles sont nécessaires à l'installation du client, ces dépendances sont installées automatiquement avec le logiciel client.  

|||  
|-|-|  
|Agent Windows Update version 7.0.6000.363|Requis par Windows pour prendre en charge la détection et le déploiement des mises à jour.|  
|Microsoft Core XML Services (MSXML) version 6.20.5002 ou supérieure|Obligatoire pour prendre en charge le traitement des documents XML dans Windows.|  
|Microsoft Remote Differential Compression (RDC)|Requis pour optimiser la transmission de données sur le réseau.|  
|Microsoft Visual C++ 2013 Redistributable version 12.0.21005.1|Requis pour prendre en charge les opérations de clients. Lorsque cette mise à jour est installée sur les ordinateurs clients, un redémarrage peut être nécessaire pour terminer l'installation.|  
|Microsoft Visual C++ 2005 Redistributable version 8.0.50727.42|Pour la version 1606 et les versions antérieures, exigé pour prendre en charge les opérations de Microsoft SQL Server Compact.|  
|API d'image Windows 6.0.6001.18000|Requis pour permettre à Configuration Manager de gérer les fichiers image Windows (.wim).|  
|Microsoft Policy Platform 1.2.3514.0|Requis pour autoriser les clients à évaluer les paramètres de conformité.|  
|Microsoft Silverlight 5.1.41212.0 (à compter de Configuration Manager version 1602)|Requis pour prendre en charge l'expérience utilisateur du site Web du catalogue d'applications.|  
|Microsoft .NET Framework version 4.5.2.|Requis pour prendre en charge les opérations de clients. Installé automatiquement sur l’ordinateur client si le Microsoft .NET Framework 4.5 ou version ultérieure n’est pas installé. Pour plus d’informations, consultez [Détails supplémentaires sur Microsoft .NET Framework version 4.5.2](#dotNet).|  
|Composants Microsoft SQL Server Compact 3.5 SP2|Requis pour conserver les informations liées aux opérations du client.|  
|Microsoft Windows Imaging Components|Requis par Microsoft .NET Framework 4.0 pour Windows Server 2003 ou Windows XP SP2 pour les ordinateurs 64 bits.|
|Client logiciel PC Microsoft Intune|Vous ne pouvez pas exécuter le client logiciel Intune PC et le client Configuration Manager sur le même ordinateur. Assurez-vous que le client Intune a été supprimé avant d’installer le client Configuration Manager.|

####  <a name="dotNet"></a> Informations supplémentaires sur Microsoft .NET Framework version 4.5.2  

> [!NOTE]  
>  Le 12 janvier 2016, la prise en charge de .NET 4.0, 4.5 et 4.5.1 a expiré. Pour plus d’informations, consultez [Forum Aux Questions sur la politique de support - Microsoft .NET Framework](https://support.microsoft.com/gp/framework_faq?WT.mc_id=azurebg_email_Trans_943_NET452_Update) à l’adresse support.microsoft.com.  

 Un redémarrage peut être nécessaire pour achever l’installation de Microsoft .NET Framework version 4.5.2. Une notification **Redémarrage requis** sera affichée dans la barre d’état système.  Scénarios courants qui nécessitent le redémarrage des ordinateurs clients :  

-   Des services ou des applications .NET sont en cours d’exécution sur l’ordinateur.  

-   Il manque une ou plusieurs mises à jour logicielles nécessaires pour l’installation de .NET.  

-   L’ordinateur doit être redémarré suite à une précédente installation de mises à jour logicielles du .NET Framework.  

 Après l’installation du .NET Framework 4.5.2, des mises à jour supplémentaires peuvent être installées par la suite et nécessiter des redémarrages de l’ordinateur.  

### <a name="configuration-manager-dependencies"></a>Dépendances de Configuration Manager  
 Pour plus d’informations sur les rôles de système de site suivants, consultez [Déterminer les rôles de système de site pour les clients System Center Configuration Manager](../../../core/clients/deploy/plan/determine-the-site-system-roles-for-clients.md)  

|||  
|-|-|  
|Point de gestion|Un point de gestion n’est pas nécessaire pour déployer le client Configuration Manager, mais il l’est pour transférer des informations entre les ordinateurs clients et les serveurs Configuration Manager. Sans point de gestion, vous ne pouvez pas gérer les ordinateurs clients.|  
|Point de distribution|Le point de distribution est un rôle de système de site facultatif, mais recommandé dans le cadre du déploiement de clients. Tous les points de distribution hébergent les fichiers sources du client, ce qui permet aux ordinateurs de trouver le point de distribution le plus proche auprès duquel ils peuvent télécharger ces fichiers sources au cours du déploiement. Si le site ne possède pas de point de distribution, les ordinateurs téléchargent les fichiers sources du client auprès de leur point de gestion.|  
|Point d'état de secours|Le point d'état de secours est un rôle de système de site facultatif, mais recommandé dans le cadre du déploiement de clients. Le point d’état de secours surveille le déploiement des clients et permet aux ordinateurs du site Configuration Manager d’envoyer des messages d’état quand ils ne peuvent pas communiquer avec un point de gestion.|  
|Point de Reporting Services|Le point de Reporting Services est un rôle de système de site, facultatif mais recommandé, qui peut afficher des rapports liés au déploiement et à la gestion du client. Pour plus d’informations, consultez [Génération de rapports dans System Center Configuration Manager](../../../core/servers/manage/reporting.md).|  

### <a name="installation-method-dependencies"></a>Dépendances liées aux méthodes d'installation  
 Les conditions requises suivantes sont spécifiques aux différentes méthodes d'installation du client.  

-   Installation poussée du client  

    -   Les comptes d'installation poussée du client sont utilisés pour se connecter aux ordinateurs pour l'installation du client et sont spécifiés dans l'onglet **Comptes** de la boîte de dialogue **Propriétés de l'installation poussée du client** . Le compte doit être membre du groupe d'administrateurs local sur l'ordinateur de destination.  

         Si vous ne spécifiez pas de compte d'installation poussée du client, le compte d'ordinateur du serveur de site sera utilisé.  

    -   L’ordinateur sur lequel vous installez le client doit avoir été découvert par au moins une méthode de découverte de Configuration Manager.  

    -   L'ordinateur dispose d'un partage ADMIN$.  

    -   L’option **Activer l’installation push du client aux ressources attribuées** doit être sélectionnée dans la boîte de dialogue **Propriétés de l’installation push du client** si vous souhaitez transférer (push) automatiquement le client Configuration Manager vers les ressources découvertes.  

    -   L'ordinateur client doit être capable de contacter un point de distribution ou un point de gestion pour télécharger les fichiers de prise en charge.  

     Vous devez disposer des autorisations de sécurité suivantes pour installer le client Configuration Manager à l’aide de l’installation push du client :  

    -   Pour configurer le compte d’installation poussée du client : autorisation **Modifier** et Lire pour l’objet **Site** .  

    -   Pour utiliser l’installation poussée du client pour installer le client sur les regroupements, les appareils et les requêtes : autorisation **Modifier la ressource** et **Lire** pour l’objet Collection.  

     Le rôle de sécurité **Administrateur d'infrastructure** comprend les autorisations requises pour la gestion de l'installation poussée du client.  

-   Installation basée sur un point de mise à jour logicielle  

    -   Si le schéma Active Directory n'a pas été étendu ou si vous installez des clients depuis une autre forêt, les propriétés d'installation de CCMSetup.exe doivent être configurées dans le Registre de l'ordinateur à l'aide d'une stratégie de groupe. Pour plus d’informations, consultez  [How to Provision Client Installation Properties (Group Policy and Software Update-Based Client Installation)](../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_Provision).  

    -   Le client Configuration Manager doit être publié sur le point de mise à jour logicielle.  

    -   L'ordinateur client doit être capable de contacter un point de distribution ou un point de gestion pour télécharger les fichiers de prise en charge.  

     Pour en savoir plus sur les autorisations de sécurité nécessaires à la gestion des mises à jour logicielles dans Configuration Manager, consultez [Prérequis pour les mises à jour logicielles dans System Center Configuration Manager](../../../sum/plan-design/prerequisites-for-software-updates.md).  

-   Installation basée sur une stratégie de groupe  

    -   Si le schéma Active Directory n'a pas été étendu ou si vous installez des clients depuis une autre forêt, les propriétés d'installation de CCMSetup.exe doivent être configurées dans le Registre de l'ordinateur à l'aide d'une stratégie de groupe. Pour plus d’informations, consultez  [How to Provision Client Installation Properties (Group Policy and Software Update-Based Client Installation)](../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_Provision).  

    -   L'ordinateur client doit être en mesure de contacter un point de gestion pour télécharger les fichiers de prise en charge.  

-   Installation basée sur un script d'ouverture de session  

     L’ordinateur client doit pouvoir contacter un point de distribution ou un point de gestion pour télécharger les fichiers de prise en charge, sauf si, sur l’invite de commande, vous avez spécifié CCMSetup.exe avec la propriété de ligne de commande **ccmsetup /source**.  

-   Installation manuelle  

     L’ordinateur client doit pouvoir contacter un point de distribution ou un point de gestion pour télécharger les fichiers de prise en charge, sauf si, sur l’invite de commande, vous avez spécifié CCMSetup.exe avec la propriété de ligne de commande **ccmsetup /source**.  

-   Installation d'ordinateurs d'un groupe de travail  

     Pour accéder aux ressources du domaine du serveur de site Configuration Manager, le compte d’accès réseau doit être configuré pour le site.  

     Pour plus d’informations sur la configuration du compte d’accès réseau, consultez [Concepts fondamentaux de la gestion de contenu dans System Center Configuration Manager](../../plan-design/hierarchy/fundamental-concepts-for-content-management.md).  

-   Installation basée sur la distribution de logiciels (pour les mises à niveau uniquement)  

    -   Si le schéma Active Directory n'a pas été étendu ou si vous installez des clients depuis une autre forêt, les propriétés d'installation de CCMSetup.exe doivent être configurées dans le Registre de l'ordinateur à l'aide d'une stratégie de groupe. Pour plus d’informations, consultez [How to Provision Client Installation Properties (Group Policy and Software Update-Based Client Installation)](../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_Provision).  

    -   L'ordinateur client doit être capable de contacter un point de distribution ou un point de gestion pour télécharger les fichiers de prise en charge.  

     Pour en savoir plus sur les autorisations de sécurité nécessaires à la mise à niveau du client Configuration Manager à l’aide de la gestion d’applications, consultez [Sécurité et confidentialité pour la gestion des applications](../../../apps/plan-design/security-and-privacy-for-application-management.md).  

-   Mises à niveau automatiques des clients  

     Vous devez avoir le rôle de sécurité **Administrateur complet** pour pouvoir configurer des mises à niveau automatiques des clients.  

### <a name="firewall-requirements"></a>Configuration requise du pare-feu  
 S’il existe un pare-feu entre les serveurs du système de site et les ordinateurs sur lesquels vous souhaitez installer le client Configuration Manager, consultez [Paramètres de port et de pare-feu Windows pour les clients dans System Center Configuration Manager](../../../core/clients/deploy/windows-firewall-and-port-settings-for-clients.md).  

##  <a name="BKMK_prereqs_mobiledevices"></a> Conditions préalables pour les clients d’appareils mobiles  
 Aidez-vous des informations suivantes pour déterminer la configuration requise pour installer le client Configuration Manager sur des appareils mobiles et pour inscrire ces appareils à l’aide de Configuration Manager.  

### <a name="dependencies-external-to-configuration-manager"></a>Dépendances externes à Configuration Manager  

-   Autorité de certification d'entreprise Microsoft avec des modèles de certificats pour déployer et gérer les certificats requis pour les appareils mobiles.  

     L'autorité de certification émettrice doit automatiquement approuver les demandes de certificat de la part d'utilisateurs d'appareils mobiles lors du processus d'inscription.  

     Pour plus d’informations sur la configuration requise pour les certificats, consultez [Sécurité et confidentialité pour les profils de certificat dans System Center Configuration Manager](../../../protect/plan-design/security-and-privacy-for-certificate-profiles.md).  

-   Groupe de sécurité qui contient les utilisateurs pouvant inscrire leurs appareils mobiles.  

     Ce groupe de sécurité est utilisé pour configurer le modèle de certificat utilisé lors de l'inscription d'appareils mobiles.  

-   Facultatif mais recommandé : alias DNS (enregistrement CNAME) nommé **ConfigMgrEnroll** configuré pour le nom du serveur du système de site sur lequel vous installerez le point proxy d’inscription.  

     Cet alias DNS est nécessaire pour prendre en charge la découverte automatique du service d’inscription : si vous ne configurez pas cet enregistrement DNS, les utilisateurs doivent spécifier manuellement le nom du serveur du système de site du point proxy d'inscription lors du processus d'inscription.  

-   Dépendances du rôle du système de site pour les ordinateurs qui exécuteront les rôles du système de site point d'inscription et point proxy d'inscription.  

     Consultez [Systèmes d’exploitation pris en charge pour les serveurs de système de site](../../../core/plan-design/configs/supported-operating-systems-for-site-system-servers.md).  

### <a name="configuration-manager-dependencies"></a>Dépendances de Configuration Manager  
 Pour plus d’informations sur les rôles de système de site suivants, consultez [Déterminer les rôles de système de site pour les clients System Center Configuration Manager](../../../core/clients/deploy/plan/determine-the-site-system-roles-for-clients.md).  

-   Point de gestion configuré pour les connexions client HTTPS et activé pour les appareils mobiles  

     Un point de gestion est toujours nécessaire pour installer le client Configuration Manager sur des appareils mobiles. En plus de la configuration requise du protocole HTTPS et d'être activé pour les appareils mobiles, le point de gestion doit être configuré avec un nom de domaine complet Internet et accepter les connexions client depuis Internet.  

-   Point d'inscription et point proxy d'inscription  

     Un point proxy d'inscription gère les demandes d'inscription de la part d'appareils mobiles et le point d'inscription termine le processus d'inscription. Le point d'inscription doit être dans la même forêt Active Directory que le serveur de site, mais le point proxy d'inscription peut être dans une autre forêt.  

-   Paramètres client pour l'inscription d'appareils mobiles  

     Configurez des paramètres client pour permettre aux utilisateurs d'inscrire des appareils mobiles et de configurer au moins un profil d'inscription.  

-   Point de Reporting Services  

     Le point de Reporting Services est un rôle de système de site, facultatif mais recommandé, qui peut afficher des rapports liés à l'inscription d'appareils mobiles et à la gestion de clients.  

     Pour plus d’informations, consultez [Génération de rapports dans System Center Configuration Manager](../../../core/servers/manage/reporting.md).  

-   Pour configurer l'inscription pour les appareils mobiles, vous devez disposer des autorisations de sécurité suivantes :  

    -   Pour ajouter, modifier et supprimer les rôles de système de site d’inscription : autorisation **Modifier** pour l’objet **Site** .  

    -   Pour configurer les paramètres clients de l’inscription : les paramètres clients par défaut nécessitent l’autorisation **Modifier** pour l’objet **Site** et les paramètres clients personnalisés nécessitent des autorisations **Agent client**  .  

     Le rôle de sécurité **Administrateur complet** comprend les autorisations requises pour configurer les rôles de système de site d'inscription.  

     Pour gérer des appareils mobiles inscrits, vous devez disposer des autorisations de sécurité suivantes :  

    -   Pour réinitialiser ou retirer un appareil mobile : **Supprimer la ressource** pour l’objet **Collection** .  

    -   Pour annuler une réinitialisation ou retirer une commande : **Supprimer la ressource** pour l’objet **Collection** .  

    -   Pour autoriser et bloquer des appareils mobiles : **Modifier la ressource** pour l’objet **Collection** .  

    -   Pour verrouiller à distance ou réinitialiser le mot de passe sur un appareil mobile : **Modifier la ressource** pour l’objet **Collection** .  

     Le rôle de sécurité **Administrateur d'opérations** comprend les autorisations nécessaires pour la gestion des appareils mobiles.  

     Pour plus d’informations sur la façon de configurer les autorisations de sécurité, consultez [Principes de base de l’administration basée sur des rôles pour System Center Configuration Manager](../../../core/understand/fundamentals-of-role-based-administration.md) et [Configure role-based administration for System Center Configuration Manager](../../../core/servers/deploy/configure/configure-role-based-administration.md).  

### <a name="firewall-requirements"></a>Configuration requise du pare-feu  
 Les appareils réseau intervenants, tels que des routeurs et des pare-feu, ainsi que le Pare-feu Windows, le cas échéant, doivent autoriser le trafic associé à l'inscription d'appareils mobiles :  

-   Entre les appareils mobiles et le point proxy d'inscription : HTTPS (par défaut, TCP 443)  

-   Entre le point proxy d'inscription et le point d'inscription : HTTPS (par défaut, TCP 443)  

 Si vous utilisez un serveur Web proxy, il doit être configuré pour un tunnel SSL. Le pontage SSL n'est pas pris en charge pour les appareils mobiles.  
