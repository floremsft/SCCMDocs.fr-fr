---
title: "Préparer des serveurs Windows | Microsoft Docs"
description: "Vérifiez qu’un ordinateur remplit les conditions préalables pour l’utiliser comme serveur de site ou serveur de système de site pour System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 2aca914f-641e-4bc8-98d4-bbf0a2a5276f
caps.latest.revision: 10
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 6ed317d45d90758832d4157985dd95d5e253c6fc
ms.openlocfilehash: bd89f97f4252ddea2d1bf7ab329417477c77868d


---
# <a name="prepare-windows-servers-to-support-system-center-configuration-manager"></a>Préparer des serveurs Windows pour prendre en charge System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Avant de pouvoir utiliser comme prévu un ordinateur Windows comme serveur de système de site ou de serveur de site pour System Center Configuration Manager, vous devez vérifier qu’il remplit bien les conditions préalables à cet usage.  

-   Ces conditions incluent souvent plusieurs fonctionnalités ou rôles Windows qui sont activés à l’aide du Gestionnaire de serveur des ordinateurs.  

-   Étant donné que la méthode d’activation des fonctionnalités et rôles Windows diffère en fonction des systèmes d’exploitation, reportez-vous à la documentation de votre système d’exploitation pour plus d’informations sur la configuration appropriée.  

Les informations contenues dans cet article offrent une vue d’ensemble des différents types de configurations Windows nécessaires à la prise en charge des systèmes de site Configuration Manager. Pour plus d’informations sur la configuration des rôles de système de site spécifiques, consultez [Prérequis des sites et systèmes de site](/sccm/core/plan-design/configs/site-and-site-system-prerequisites).

##  <a name="a-namebkmkwinfeaturesa-windows-features-and-roles"></a><a name="BKMK_WinFeatures"></a> Rôles et fonctionnalités Windows  
 Quand vous configurez des rôles et fonctionnalités Windows sur un ordinateur, il se peut que vous deviez redémarrer l’ordinateur pour terminer la configuration. Par conséquent, avant d’installer un site ou serveur de système de site Configuration Manager, nous vous recommandons de déterminer sur quels ordinateurs les différents rôles de système de site seront hébergés.
### <a name="features"></a>Fonctionnalités  
 Les fonctionnalités Windows suivantes sont nécessaires sur certains serveurs de système de site et doivent être configurées avant l’installation d’un rôle de système de site sur cet ordinateur.  

-   **.NET Framework** : incluant  

    -   ASP.NET  
    -   Activation HTTP  
    -   Activation non-HTTP  
    -   Services WCF  

    Différentes versions de .NET Framework sont requises par les différents rôles de système de site.  

    Microsoft .NET Framework 4.0 et les versions ultérieures n’offrent pas de compatibilité descendante pour remplacer les versions 3.5 et antérieures. Si différentes versions sont répertoriées comme requises, vous devez donc prévoir d’activer chaque version sur le même ordinateur.  

-   **Service de transfert intelligent en arrière-plan (BITS)** : les points de gestion ont besoin du service BITS (et des options sélectionnées automatiquement) pour prendre en charge la communication avec les appareils gérés.  

-   **BranchCache** : les points de distribution peuvent être configurés avec BranchCache pour prendre en charge les clients qui utilisent BranchCache.  

-   **Déduplication des données** : les points de distribution peuvent être configurés avec la déduplication des données et en tirer parti.  

-   **Compression différentielle à distance (RDC)** : chaque ordinateur qui héberge un serveur de site ou un point de distribution a besoin de la compression différentielle à distance.   
    Celle-ci est utilisée pour générer des signatures de package et effectuer des comparaisons de signatures.  

### <a name="roles"></a>Rôles  
 Les rôles Windows suivants sont requis pour prendre en charge des fonctionnalités spécifiques, telles que les mises à jour logicielles et les déploiements de système d’exploitation. IIS est requis par les principaux rôles de système de site.  

 -   **Service d’inscription de périphérique réseau** (relevant des services de certificats Active Directory) : ce rôle Windows est une condition préalable à l’utilisation de profils de certificat dans Configuration Manager.  

 -   **Serveur web (IIS)**, avec notamment :  
    -   Fonctionnalités HTTP communes >  
        -   Redirection HTTP  
    -   Développement d’applications >  
        -   Extensibilité .NET  
        -   ASP.NET  
        -   Extensions ISAPI  
        -   Filtres ISAPI  
    -   Outils de gestion >  
        -   IIS 6 Management Compatibility  
        -   Compatibilité avec la métabase de données IIS 6  
        -   Compatibilité WMI d'IIS 6  
    -   Sécurité >  
        -   Filtrage des demandes  
        -   Authentification Windows  

 Les rôles de système de site suivants utilisent une ou plusieurs des configurations IIS répertoriées :  
    -   Point de service Web du catalogue des applications  
    -   Point du site web du catalogue des applications  
    -   Point de distribution  
    -   Point d'inscription  
    -   Point proxy d'inscription  
    -   Point d’état de secours  
    -   Point de gestion  
    -   Point de mise à jour logicielle  
    -   Point de migration d'état     

    La version minimale d’IIS requise est la version fournie avec le système d’exploitation du serveur de site.  

    En plus de ces configurations IIS, il se peut que vous deviez configurer [Filtrage des demandes IIS pour les points de distribution](#BKMK_IISFiltering).  

-   **Services de déploiement Windows** : ce rôle est utilisé pour le déploiement de système d’exploitation.  
-   **Windows Server Update Services** : ce rôle est nécessaire pour le déploiement de mises à jour logicielles.  

##  <a name="a-namebkmkiisfilteringa-iis-request-filtering-for-distribution-points"></a><a name="BKMK_IISFiltering"></a> Filtrage des demandes IIS pour les points de distribution  
 Par défaut, IIS utilise le filtrage des demandes pour bloquer l’accès via la communication HTTP ou HTTPS à plusieurs extensions de nom de fichier et emplacements de dossier. Sur un point de distribution, cela empêche les clients de télécharger des packages qui contiennent des extensions ou des emplacements de dossier bloqués.  

 Si vos fichiers sources de package contiennent des extensions qui sont bloquées dans IIS par votre configuration de filtrage des demandes, vous devez configurer le filtrage des demandes pour les autoriser. Pour cela, vous devez [configurer le filtrage des demandes](https://technet.microsoft.com/library/hh831621.aspx) dans le Gestionnaire des services IIS sur vos ordinateurs de point de distribution.  

 Par ailleurs, Configuration Manager utilise les extensions de nom de fichier suivantes pour les packages et les applications. Vérifiez que vos configurations de filtrage des demandes ne bloquent pas ces extensions de fichier :  

-   .PCK  
-   .PKG  
-   .STA  
-   .TAR  

Par exemple, dans le cadre d’un déploiement logiciel, vous pouvez avoir des fichiers sources incluant un dossier nommé **bin**ou contenant un fichier avec l’extension **.mdb** .  

-   Par défaut, le filtrage des demandes IIS bloque l’accès à ces éléments (**bin** est bloqué en tant que segment masqué et **.mdb** est bloqué en tant qu’extension de nom de fichier).  

-   Quand vous utilisez la configuration IIS par défaut sur un point de distribution, les clients qui utilisent BITS ne peuvent pas télécharger ce déploiement logiciel à partir du point de distribution et indiquent qu’ils attendent du contenu.  

-   Pour permettre aux clients de télécharger ce contenu, sur chaque point de distribution applicable, modifiez l’option **Filtrage des demandes** dans le Gestionnaire des services IIS pour autoriser l’accès aux extensions de fichier et aux dossiers contenus dans les packages et applications que vous déployez.  

> [!IMPORTANT]  
>  Les modifications apportées au filtre de demande peuvent augmenter la surface exposée aux attaques de l’ordinateur.  
>   
>  -   Les modifications apportées au niveau du serveur s’appliquent à tous les sites web sur le serveur.  
> -   Les modifications apportées à un site web particulier s’appliquent uniquement à ce site web.  
>   
>  La bonne pratique à suivre sur le plan de la sécurité consiste à exécuter Configuration Manager sur un serveur web dédié. Si vous devez exécuter d’autres applications sur le serveur web, utilisez un site web personnalisé pour Configuration Manager. Pour plus d’informations, consultez [Sites web pour les serveurs de système de site dans System Center Configuration Manager](../../../core/plan-design/network/websites-for-site-system-servers.md).  

## <a name="http-verbs"></a>Verbes HTTP
**Points de gestion** : pour garantir une communication fonctionnelle entre les clients et un point de gestion, sur le serveur de point de gestion, vérifiez que les verbes HTTP suivants sont autorisés :  
 - GET
 - POST
 - CCM_POST
 - HEAD
 - PROPFIND

**Points de distribution** : les points de distribution exigent l’autorisation des verbes HTTP suivants :
 - GET
 - HEAD
 - PROPFIND

Pour plus d’informations sur la configuration du filtrage des demandes, consultez [Configurer le filtrage des demandes dans IIS](https://technet.microsoft.com/library/hh831621.aspx#Verbs) sur TechNet ou une documentation similaire qui vaut pour la version de Windows Server qui héberge votre point de gestion.



<!--HONumber=Dec16_HO3-->


