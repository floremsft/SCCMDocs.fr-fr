---
title: Principes de base de la gestion de contenu
titleSuffix: Configuration Manager
description: "Utilisez les outils et les options de System Center Configuration Manager pour gérer le contenu que vous déployez."
ms.custom: na
ms.date: 05/04/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c201be2a-692c-4d67-ac95-0a3afa5320fe
caps.latest.revision: "28"
caps.handback.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: d550d18de93f5e11c7538de24473d36c788145e6
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/12/2017
---
# <a name="fundamental-concepts-for-content-management-in-system-center-configuration-manager"></a>Principes de base de la gestion de contenu dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

System Center Configuration Manager vous propose un système d’outils et d’options efficace pour gérer le contenu que vous déployez (applications, packages, mises à jour logicielles et déploiements de système d’exploitation).  

Le contenu que vous déployez est stocké à la fois sur des serveurs de site et sur des serveurs de système de site de point de distribution. Le transfert de ce contenu d’un emplacement à un autre peut nécessiter une large bande passante réseau. Pour planifier et utiliser l’infrastructure de gestion de contenu efficacement, nous vous recommandons de vous familiariser avec les différentes options et configurations disponibles, puis de déterminer comment les utiliser au mieux en fonction de votre environnement réseau et de vos besoins en matière de déploiement de contenu.  

> [!TIP]    
> Pour en savoir plus sur le processus de distribution de contenu et obtenir de l’aide sur le diagnostic et la résolution des problèmes généraux de distribution de contenu, consultez [Compréhension et résolution des problèmes de distribution de contenu dans Microsoft Configuration Manager](https://support.microsoft.com/help/4000401/content-distribution-in-mcm) à l’adresse support.microsoft.com.

Les concepts clés de la gestion de contenu sont exposés ci-dessous. Si un concept doit être complété par des informations supplémentaires ou complexes, les liens d’accès à ces informations sont indiqués.

## <a name="accounts-used-for-content-management"></a>Comptes utilisés pour la gestion de contenu  
 Les comptes suivants peuvent être utilisés pour la gestion de contenu :  

-   **Compte d’accès réseau**: compte utilisé par les clients pour se connecter à un point de distribution et accéder au contenu. Par défaut, le compte d’ordinateur est utilisé en premier.  

     Ce compte est également utilisé par les points de distribution d’extraction pour obtenir le contenu d’un point de distribution source dans une forêt distante.  

-   **Compte d’accès au package** : par défaut, Configuration Manager permet aux utilisateurs et aux administrateurs des comptes d’accès génériques d’accéder au contenu sur un point de distribution. Toutefois, vous pouvez configurer des autorisations supplémentaires pour limiter l’accès.   

-   **Compte de connexion multidiffusion**: compte utilisé pour les déploiements de système d’exploitation.  

Pour plus d’informations sur ces comptes, consultez [Gérer les comptes pour accéder au contenu](../../../core/plan-design/hierarchy/manage-accounts-to-access-content.md).

## <a name="bandwidth-throttling-and-scheduling"></a>Limitation et planification de la bande passante  
 La limitation et la planification sont des options qui vous aident à contrôler la distribution du contenu d’un serveur de site vers des points de distribution. Cela est similaire, sans être directement lié, aux contrôles de bande passante pour la réplication de site à site basée sur des fichiers.  

 Pour plus d’informations, consultez [Gérer la bande passante réseau](/sccm/core/plan-design/hierarchy/manage-network-bandwidth).

## <a name="binary-differential-replication"></a>Réplication différentielle binaire  
 Prérequis pour les points de distribution, la réplication différentielle binaire (ou réplication delta) est automatiquement utilisée pour réduire la bande passante utilisée lors de la distribution de mises à jour à un contenu que vous avez déployé précédemment sur d’autres sites ou sur des points de distribution distants.  

 Cette fonctionnalité réduit la bande passante réseau utilisée lors de l’envoi des mises à jour du contenu distribué. En effet, elle renvoie uniquement le contenu nouveau ou modifié au lieu d’envoyer l’ensemble complet des fichiers sources de contenu chaque fois qu’une modification est apportée à ces fichiers.  

 Quand vous utilisez la réplication différentielle binaire, Configuration Manager identifie les modifications apportées aux fichiers sources pour chaque jeu de contenus précédemment distribué.  

-   Quand des fichiers sont modifiés dans le contenu source, Configuration Manager crée une version incrémentielle du jeu de contenus et ne réplique que les fichiers modifiés sur les sites de destination et les points de destination. Un fichier est considéré comme modifié s’il a été renommé ou déplacé, ou si son contenu a changé. Par exemple, si vous remplacez un fichier de pilote pour un package de déploiement du système d'exploitation précédemment distribué vers plusieurs sites, uniquement le fichier du pilote modifié est répliqué sur ces sites de destination.  

-   Configuration Manager prend en charge jusqu’à cinq versions incrémentielles d’un jeu de contenus avant de renvoyer le jeu de contenus entier. Après la cinquième mise à jour, la modification suivante du jeu de contenus amène Configuration Manager à créer une nouvelle version du jeu de contenus. Configuration Manager distribue ensuite la nouvelle version du jeu de contenus pour remplacer le jeu précédent et toutes ses versions incrémentielles. Après la distribution du jeu de contenus, les modifications incrémentielles ultérieures apportées aux fichiers sources sont de nouveau répliquées en utilisant la réplication différentielle binaire.  


La réplication différentielle binaire est prise en charge entre chaque site parent et enfant dans une hiérarchie. Au sein d’un site, elle est prise en charge entre le serveur de site et ses points de distribution standard. Toutefois, les points de distribution d’extraction et les points de distribution cloud ne prennent pas en charge la réplication différentielle binaire pour le transfert de contenu. Les points de distribution d’extraction prennent en charge les deltas de niveau fichier et le transfert de nouveaux fichiers, mais pas les blocs au sein d’un fichier.

Les applications utilisent toujours la réplication différentielle binaire. La réplication différentielle binaire est facultative pour les packages, et n'est pas activée par défaut. Pour utiliser la réplication différentielle binaire pour les packages, vous devez activer cette fonctionnalité pour chaque package. Pour cela, sélectionnez l'option **Activer la réplication différentielle binaire** lorsque vous créez un package ou lorsque vous modifiez l'onglet **Source de données** des propriétés du package.  

## <a name="branchcache"></a>BranchCache  
 Technologie Windows qui permet aux clients prenant en charge BranchCache et ayant téléchargé un déploiement configuré pour BranchCache de faire office de source de contenu pour d’autres clients BranchCache.  

 Par exemple, quand le premier ordinateur client compatible avec BranchCache demande du contenu d’un point de distribution qui exécute Windows Server 2012 et qui est configuré en tant que serveur BranchCache, l’ordinateur client télécharge ce contenu et le met en cache.  

-   Cet ordinateur client peut ensuite mettre le contenu à la disposition d’autres clients BranchCache figurant dans le même sous-réseau, qui mettent également en cache le contenu.  

-   Ainsi, les clients suivants sur le même sous-réseau n'ont pas besoin de télécharger du contenu depuis le point de distribution, et le contenu est distribué sur plusieurs clients, en vue de transferts futurs.  

## <a name="peer-cache"></a>Cache d’homologue
À partir de la version 1610, le cache d’homologue vous permet de gérer le déploiement de contenu sur les clients distants. Le cache d’homologue est une solution Configuration Manager intégrée qui permet aux clients de partager du contenu avec d’autres clients directement à partir de leur cache local.

Une fois que vous avez déployé des paramètres du client qui activent le cache d’homologue sur un regroupement, les membres de ce regroupement peuvent agir comme source de contenu homologue pour d’autres clients du même groupe de limites.

Pour plus d’informations, voir [Cache d’homologue pour les clients Configuration Manager](/sccm/core/plan-design/hierarchy/client-peer-cache).


## <a name="windows-pe-peer-cache"></a>Mise en cache d’homologue Windows PE
Quand vous déployez un nouveau système d’exploitation dans System Center Configuration Manager, les ordinateurs qui exécutent la séquence de tâches peuvent utiliser le cache d’homologue Windows PE pour obtenir du contenu à partir d’un homologue local (source de cache d’homologue) au lieu de le télécharger à partir d’un point de distribution. Cela permet de réduire le trafic du réseau étendu dans les scénarios de succursale où il n'existe aucun point de distribution local.

Pour plus d’informations, consultez [Mise en cache d’homologue Windows PE](../../../osd/get-started/prepare-windows-pe-peer-cache-to-reduce-wan-traffic.md).


## <a name="client-locations"></a>Emplacements des clients  
 Les clients accèdent au contenu à partir des emplacements suivants :  

-   **Intranet** (local) :  

    -   Les points de distribution peuvent utiliser HTTP ou HTTPS.  

    -   Utilisez uniquement un point de distribution cloud de secours quand les points de distribution locaux ne sont pas disponibles.  

-   **Internet** :  

    -   Exige des points de distribution qu’ils acceptent le protocole HTTPS.  

    -   Vous pouvez utiliser un point de distribution cloud de secours.  

-   **Groupe de travail**:  

    -   Exige des points de distribution qu’ils acceptent le protocole HTTPS.  

    -   Vous pouvez utiliser un point de distribution cloud de secours.  



## <a name="content-library"></a>Bibliothèque de contenu  
 La bibliothèque de contenu est le stockage SIS (Single Instance Store) de contenu qu’utilise Configuration Manager pour réduire la taille globale du corps de contenu combiné que vous distribuez.  

- En savoir plus sur la [bibliothèque de contenu](../../../core/plan-design/hierarchy/the-content-library.md).
- Utilisez l’[outil de nettoyage de la bibliothèque de contenu](/sccm/core/plan-design/hierarchy/content-library-cleanup-tool) pour supprimer le contenu qui n’est plus associé à une application.  


## <a name="distribution-points"></a>Points de distribution  
 Configuration Manager utilise des points de distribution pour stocker les fichiers nécessaires à l’exécution de logiciels sur les ordinateurs clients. Les clients doivent avoir accès à au moins un point de distribution à partir duquel ils peuvent télécharger les fichiers du contenu que vous déployez.  

 Le point de distribution (non spécifique) de base est communément appelé point de distribution standard. Il existe deux variantes du point de distribution standard qui reçoivent une attention particulière :  

-   **Point de distribution d’extraction** : variation d’un point de distribution où le point de distribution obtient le contenu à partir d’un autre point de distribution (point de distribution source). Ce processus est similaire à la façon dont les clients téléchargent le contenu à partir de points de distribution. Les points de distribution d’extraction peuvent vous permettre d’éviter les goulots d’étranglement de bande passante réseau qui surviennent quand le serveur de site doit distribuer directement le contenu à chaque point de distribution.  [Utiliser un point de distribution d’extraction avec System Center Configuration Manager](/sccm/core/plan-design/hierarchy/use-a-pull-distribution-point).

-   **Point de distribution cloud** : variante d’un point de distribution, installée dans Microsoft Azure. [Découvrez comment utiliser un point de distribution cloud avec System Center Configuration Manager](../../../core/plan-design/hierarchy/use-a-cloud-based-distribution-point.md).  


Les points de distribution standard prennent en charge diverses configurations et fonctionnalités, telles que la limitation et la planification, le PXE et la multidiffusion, et le contenu préparé.  

-   Vous pouvez utiliser des contrôles tels que les **planifications** ou une **limitation de bande passante** pour contrôler ce transfert.  

-   Vous pouvez également utiliser d’autres options, dont notamment le **contenu préparé** et les **points de distribution d’extraction**. En outre, vous pouvez tirer parti de **BranchCache** pour réduire la bande passante réseau utilisée quand vous déployez du contenu.  

-   Les points de distribution prennent en charge différentes configurations, telles que **[PXE](../../../osd/get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_PXEDistributionPoint)** et **[Multidiffusion](../../../osd/get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_DPMulticast)** pour les déploiements de système d’exploitation, ou des configurations pour prendre en charge des **appareils mobiles**.  

 Les points de distribution d’extraction et cloud prennent en charge un grand nombre de ces configurations, mais présentent des limitations spécifiques à chaque variante de point de distribution.  

## <a name="distribution-point-groups"></a>Groupes de points de distribution  
 Les groupes de points de distribution sont des regroupements logiques de points de distribution qui peuvent simplifier la distribution de contenu.  

 Pour plus d’informations, voir [Gérer les groupes de points de distribution](../../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_manage).

## <a name="distribution-point-priority"></a>Priorité des points de distribution  
 La valeur de priorité d’un point de distribution est basée sur le temps nécessaire au transfert des déploiements précédents vers ce point de distribution.  

-   Il s’agit d’une valeur ajustée automatiquement qui est attribuée à un point de distribution et qui aide Configuration Manager à transférer du contenu vers plus de points de distribution en un plus bref délai.  

-   Quand vous distribuez du contenu vers plusieurs points de distribution en même temps ou vers un groupe de points de distribution, Configuration Manager envoie le contenu au point de distribution ayant la priorité la plus élevée avant d’envoyer ce même contenu à un point de distribution de priorité inférieure.  

-   Cela ne remplace pas la priorité de distribution pour les packages, qui reste le facteur décisif dans la séquence de transfert des différentes distributions.  


Par exemple, si vous distribuez du contenu présentant une priorité de distribution élevée vers un point de distribution présentant une priorité de distribution basse, ce package avec la priorité de distribution élevée sera toujours transféré avant un package avec une priorité de distribution basse. La priorité de distribution s'applique même si les packages présentant une priorité de distribution basse sont distribués sur des points de distribution présentant des priorités de point de distribution élevées.

La priorité de distribution élevée du package permet à Configuration Manager de distribuer ce contenu à ses points de distribution concernés avant d’envoyer les packages ayant une priorité de distribution inférieure.  

> [!NOTE]  
>  Les points de distribution d’extraction utilisent également un concept de priorité pour ordonner la séquence de leur points de distribution source.  
>   
>  -   La priorité de point de distribution pour les transferts de contenu vers le point de distribution est différente de la priorité utilisée par les points de distribution d'extraction lors de la recherche de contenu auprès d'un point de distribution source.  
>  -   Pour plus d’informations, voir [Utiliser un point de distribution d’extraction avec System Center Configuration Manager](/sccm/core/plan-design/hierarchy/use-a-pull-distribution-point).  


## <a name="fallback"></a>Secours  
 À partir de la version 1610, plusieurs choses ont changé dans la manière dont les clients recherchent un point de distribution avec du contenu, y compris les scénarios de secours. Utilisez les informations suivantes relatives à la version que vous utilisez :

**Version 1610 et ultérieure**   
Les clients qui ne peuvent pas rechercher de contenu à partir d’un point de distribution associé à leur groupe de limites actuel peuvent avoir recours à des emplacements sources de contenu associés à des groupes de limites voisins. Pour faire office de groupe de secours, un groupe de limites voisin doit avoir une relation définie avec le groupe de limites actuel du client. Cette relation inclut une durée configurée qui doit s’écouler avant qu’un client qui ne trouve pas de contenu localement puisse inclure dans sa recherche des sources de contenu issues du groupe de limites voisin.

Les concepts de points de distribution préférés ne sont plus utilisés, et les paramètres d’**autorisation des emplacements sources de secours pour le contenu** ne sont plus disponibles ou appliqués.

Pour plus d’informations, consultez [Groupes de limites](/sccm/core/servers/deploy/configure/define-site-boundaries-and-boundary-groups#boundary-groups).


**Version 1511, 1602 et 1606**   
Les paramètres de secours sont liés à l’utilisation de **points de distribution préférés** et aux emplacements sources de contenu utilisés par les clients.

-   Par défaut, les clients téléchargent uniquement le contenu à partir d’un point de distribution préféré (qui est associé aux groupes de limites du client).  

-   Cependant, quand un point de distribution donné est configuré avec **Autoriser les clients à utiliser ce système de site en tant qu’emplacement source de secours du contenu**, ce point de distribution est proposé uniquement comme source de contenu valide aux clients qui ne peuvent pas obtenir un déploiement à partir de l’un de leurs points de distribution préférés.  


Pour plus d’informations sur les différents scénarios de secours et d’emplacement de contenu, consultez [Scénarios d’emplacement source du contenu](../../../core/plan-design/hierarchy/content-source-location-scenarios.md). Pour plus d’informations sur les groupes de limites, consultez [Groupes de limites pour les versions 1511, 1602 et 1606](/sccm/core/servers/deploy/configure/boundary-groups-for-1511-1602-and-1606).

## <a name="network-bandwidth"></a>Bande passante du réseau  
 Pour mieux gérer la largeur de la bande passante réseau utilisée quand vous distribuez du contenu, vous pouvez utiliser les options suivantes :  

-   **Contenu préparé** : processus de transfert de contenu vers un point de distribution sans passer par Configuration Manager pour distribuer le contenu sur le réseau.  

-   **Planification et limitation** : configurations qui vous aident à contrôler quand et comment le contenu est distribué aux points de distribution.  

Pour plus d’informations, consultez [Gérer la bande passante réseau](/sccm/core/plan-design/hierarchy/manage-network-bandwidth).

## <a name="network-connection-speed-to-content-source"></a>Vitesse de la connexion réseau vers la source de contenu  
À partir de la version 1610, plusieurs choses ont changé dans la façon dont les clients recherchent un point de distribution avec du contenu, y compris la vitesse de connexion réseau à une source de contenu. Utilisez les informations suivantes relatives à la version que vous utilisez :

**Version 1610 et ultérieure**   
Les vitesses de connexion réseau qui définissent un point de distribution comme **Rapide** ou **Lent** ne sont plus utilisées. Au lieu de cela, chaque système de site associé à un groupe de limites est traité de la même façon.

Pour plus d’informations, consultez [Groupes de limites](/sccm/core/servers/deploy/configure/define-site-boundaries-and-boundary-groups#boundary-groups).


**Version 1511, 1602 et 1606**   
 Vous pouvez configurer la vitesse de connexion réseau de chaque point de distribution d’un groupe de limites :  

-   Les clients utilisent cette valeur lorsqu'ils se connectent au point de distribution.

-   Par défaut, la vitesse de connexion réseau est configurée sur **Rapide**, mais elle peut également être définie sur **Lente**.  

-   La **vitesse de connexion réseau** et la configuration d’un déploiement déterminent si un client peut télécharger du contenu à partir d’un point de distribution quand le client se trouve dans un groupe de limites associé.  

Pour plus d’informations sur les différents scénarios de secours et d’emplacement de contenu, consultez [Scénarios d’emplacement source du contenu](../../../core/plan-design/hierarchy/content-source-location-scenarios.md). Pour plus d’informations sur les groupes de limites, consultez [Groupes de limites pour les versions 1511, 1602 et 1606](/sccm/core/servers/deploy/configure/boundary-groups-for-1511-1602-and-1606).

## <a name="on-demand-content-distribution"></a>Distribution de contenu à la demande  
 Vous pouvez définir cette option pour des applications et des packages (déploiements) individuels, afin de permettre la distribution de contenu à la demande vers les points de distribution préférés.  

-   Pour activer cette option pour un déploiement, activez **Distribuer le contenu pour ce package vers les points de distribution préférés**.  

-   Quand cette option est activée pour un déploiement, si un client tente de demander du contenu qui n’est disponible sur aucun de ses points de distribution préférés, Configuration Manager distribue automatiquement ce contenu aux points de distribution préférés du client.  

-   Même si cette option force Configuration Manager à distribuer automatiquement le contenu aux points de distribution préférés de ce client, le client peut obtenir ce contenu auprès d’autres points de distribution avant que ses points de distribution préférés reçoivent le déploiement. Dans ce cas, le contenu est alors disponible sur ce point de distribution pour le client suivant qui cherchera ce déploiement.  

Si vous utilisez la version 1610 ou ultérieure, consultez [Groupes de limites](/sccm/core/servers/deploy/configure/define-site-boundaries-and-boundary-groups#boundary-groups).
Si vous utilisez la version 1511, 1602 ou 1606, consultez [Scénarios d’emplacement source de contenu](../../../core/plan-design/hierarchy/content-source-location-scenarios.md) pour plus d’informations sur les différents scénarios de secours et d’emplacement de contenu.  



## <a name="package-transfer-manager"></a>Package Transfer Manager  
 Package Transfer Manager est le composant de serveur de site qui transfère le contenu vers les points de distribution situés sur d’autres ordinateurs.  

 En savoir plus sur le [Package Transfer Manager](../../../core/plan-design/hierarchy/package-transfer-manager.md).  

## <a name="preferred-distribution-point"></a>Point de distribution préféré  
 Un point de distribution préféré comprend tous les points de distribution associés aux groupes de limites actuels d’un client.  

 Vous pouvez associer chaque point de distribution avec un ou plusieurs groupes de limites :  

-   Cette association aide le client à identifier les points de distribution d’où il peut télécharger du contenu.  
-   Par défaut, les clients peuvent uniquement télécharger du contenu à partir d’un point de distribution préféré.  


Pour plus d’informations :
 - Si vous utilisez la version 1610 ou ultérieure, consultez [Groupes de limites](/sccm/core/servers/deploy/configure/define-site-boundaries-and-boundary-groups#boundary-groups).
 - Si vous utilisez la version 1511, 1602 ou 1606, consultez [Scénarios d’emplacement source du contenu](../../../core/plan-design/hierarchy/content-source-location-scenarios.md).

## <a name="prestage-content"></a>Contenu préparé  
 La préparation du contenu est un processus de transfert de contenu vers un point de distribution sans passer par Configuration Manager pour distribuer le contenu sur le réseau.  

 Pour plus d’informations, consultez [Gérer la bande passante réseau](/sccm/core/plan-design/hierarchy/manage-network-bandwidth).
