---
title: Principes de base de la gestion de contenu | System Center Configuration Manager
description: "Utilisez les outils et les options de System Center Configuration Manager pour gérer le contenu que vous déployez."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c201be2a-692c-4d67-ac95-0a3afa5320fe
caps.latest.revision: 28
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 27342ef83d877c31f39bc232e3e19e37b78e62da


---
# <a name="fundamental-concepts-for-content-management-in-system-center-configuration-manager"></a>Principes de base de la gestion de contenu dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

System Center Configuration Manager vous propose un système d’outils et d’options efficace pour gérer le contenu que vous déployez (applications, packages, mises à jour logicielles et déploiements de système d’exploitation).  

 Le contenu que vous déployez est stocké à la fois sur des serveurs de site et sur des serveurs de système de site de point de distribution. Le transfert de ce contenu d’un emplacement à un autre peut nécessiter une grande quantité de bande passante réseau.  Pour planifier et utiliser l’infrastructure de gestion de contenu efficacement, familiarisez-vous avec les différentes options et configurations disponibles, puis déterminez comment les utiliser au mieux en fonction de votre environnement réseau et de vos besoins en matière de déploiement de contenu.  

Les concepts clés pour la gestion de contenu suivent. Si un concept doit être complété par des informations supplémentaires ou complexes, les liens d’accès à ces informations sont indiqués.  

## <a name="accounts-used-for-content-management"></a>Comptes utilisés pour la gestion de contenu  
 Les comptes suivants peuvent être utilisés pour la gestion de contenu :  

-   **Compte d’accès réseau** : compte utilisé par les clients pour se connecter à un point de distribution et accéder au contenu. Par défaut, les clients essaient d’abord d’utiliser leur compte d’ordinateur.  

     Ce compte est également utilisé par les points de distribution d’extraction pour obtenir le contenu d’un point de distribution source dans une forêt distante.  

-   **Compte d’accès au package** : par défaut, Configuration Manager permet aux utilisateurs et aux administrateurs de comptes d’accès génériques d’accéder au contenu d’un point de distribution. Toutefois, vous pouvez configurer des autorisations supplémentaires pour limiter l’accès. Voir &lt;Gérer les comptes d’accès au contenu des packages\>  

-   **Compte de connexion multidiffusion** : compte utilisé pour les déploiements de système d’exploitation.  

Pour plus d’informations sur ces comptes, consultez [Gérer les comptes pour accéder au contenu](../../../core/plan-design/hierarchy/manage-accounts-to-access-content.md).

## <a name="bandwidth-throttling-and-scheduling"></a>Limitation et planification de la bande passante  
 La limitation et la planification sont des options qui vous aident à contrôler la distribution du contenu d’un serveur de site vers des points de distribution. Cela est similaire, sans être directement lié, aux contrôles de bande passante pour la réplication de site à site basée sur des fichiers.  

 Pour plus d’informations, consultez [Gérer la bande passante réseau](/sccm/core/plan-design/hierarchy/manage-network-bandwidth).

## <a name="binary-differential-replication"></a>Réplication différentielle binaire  
 Élément de configuration requis pour les points de distribution, la réplication différentielle binaire (ou réplication delta) est automatiquement utilisée pour réduire l’utilisation de la bande passante lors de la distribution de mises à jour du contenu que vous avez déployé précédemment sur d’autres sites ou sur un point de distribution distant.  

 Cette fonctionnalité réduit la bande passante réseau utilisée lors de l’envoi des mises à jour du contenu distribué. En effet, elle renvoie uniquement le contenu nouveau ou modifié au lieu d’envoyer l’ensemble complet des fichiers sources de contenu chaque fois qu’une modification est apportée à ces fichiers.  

 Quand vous utilisez la réplication différentielle binaire, Configuration Manager identifie les modifications apportées aux fichiers sources pour chaque jeu de contenus précédemment distribué.  

-   Quand des fichiers sont modifiés dans le contenu source, Configuration Manager crée une version incrémentielle du jeu de contenus et ne réplique que les fichiers modifiés sur les sites de destination et les points de destination. Un fichier est considéré comme étant modifié s'il est renommé ou déplacé ou si son contenu est modifié. Par exemple, si vous remplacez un fichier de pilote pour un package de déploiement du système d'exploitation précédemment distribué vers plusieurs sites, uniquement le fichier du pilote modifié est répliqué sur ces sites de destination.  

-   Configuration Manager prend en charge jusqu’à cinq versions incrémentielles d’un jeu de contenus avant de renvoyer le jeu de contenus entier. Après la cinquième mise à jour, la modification suivante du jeu de contenus amène Configuration Manager à créer une nouvelle version du jeu de contenus. Configuration Manager distribue ensuite la nouvelle version du jeu de contenus pour remplacer le jeu précédent et toutes ses versions incrémentielles. Après la distribution du jeu de contenus, les modifications incrémentielles ultérieures apportées aux fichiers sources sont de nouveau répliquées en utilisant la réplication différentielle binaire.  


La réplication différentielle binaire est prise en charge entre chaque site parent et enfant dans une hiérarchie. Au sein d’un site, elle est prise en charge entre le serveur de site et ses points de distribution. Cette prise en charge inclut les points de distribution d’extraction, mais n’inclut pas les points de distribution cloud. Les points de distribution cloud ne prennent pas en charge la réplication différentielle binaire pour le transfert de contenu.  

Les applications utilisent toujours la réplication différentielle binaire. La réplication différentielle binaire est facultative pour les packages, et n'est pas activée par défaut. Pour utiliser la réplication différentielle binaire pour les packages, vous devez activer cette fonctionnalité pour chaque package. Pour cela, sélectionnez l'option **Activer la réplication différentielle binaire** lorsque vous créez un package ou lorsque vous modifiez l'onglet **Source de données** des propriétés du package.  

## <a name="branchcache"></a>BranchCache  
 Technologie Windows permettant aux clients qui prennent en charge BranchCache et qui ont téléchargé un déploiement configuré pour BranchCache de rendre ensuite le contenu source disponible pour d’autres clients BranchCache.  

 Par exemple, quand le premier ordinateur client compatible avec BranchCache demande du contenu d’un point de distribution qui exécute Windows Server 2012 et qui est configuré en tant que serveur BranchCache, l’ordinateur client télécharge ce contenu et le met en cache.  

-   Cet ordinateur client peut ensuite mettre à disposition le contenu pour d’autres clients BranchCache du même sous-réseau, qui mettent également en cache le contenu.  

-   Ainsi, les clients suivants sur le même sous-réseau n'ont pas besoin de télécharger du contenu depuis le point de distribution, et le contenu est distribué sur plusieurs clients, en vue de transferts futurs.  





## <a name="windows-pe-peer-cache"></a>Mise en cache d’homologue Windows PE
Quand vous déployez un nouveau système d’exploitation dans System Center Configuration Manager, les ordinateurs qui exécutent la séquence de tâches peuvent utiliser le cache d’homologue Windows PE pour obtenir du contenu à partir d’un homologue local (source de cache d’homologue) au lieu de le télécharger à partir d’un point de distribution. Cela permet de réduire le trafic du réseau étendu dans les scénarios de succursale où il n'existe aucun point de distribution local.

Pour plus d’informations, consultez [Mise en cache d’homologue Windows PE](../../../osd/get-started/prepare-windows-pe-peer-cache-to-reduce-wan-traffic.md).


## <a name="client-locations"></a>Emplacements des clients  
 Les clients accèdent au contenu à partir des emplacements suivants :  

-   **Intranet** (local) :  

    -   Les points de distribution peuvent utiliser HTTP ou HTTPS.  

    -   Utilisez un point de distribution cloud de secours uniquement quand les points de distribution locaux ne sont pas disponibles.  

-   **Internet** :  

    -   Nécessite des points de distribution pour accepter le protocole HTTPS.  

    -   Vous pouvez utiliser un point de distribution cloud de secours.  

-   **Groupe de travail**:  

    -   Nécessite des points de distribution pour accepter le protocole HTTPS.  

    -   Vous pouvez utiliser un point de distribution cloud de secours.  



## <a name="content-library"></a>Bibliothèque de contenu  
 Stockage SIS (Single-Instance Store) de contenu qu’utilise Configuration Manager pour réduire la taille globale du corps de contenu combiné que vous distribuez.  

En savoir plus sur la [bibliothèque de contenu](../../../core/plan-design/hierarchy/the-content-library.md).


## <a name="distribution-point"></a>Point de distribution  
 Configuration Manager utilise des points de distribution pour stocker les fichiers nécessaires à l’exécution de logiciels sur les ordinateurs clients. Les clients doivent avoir accès à au moins un point de distribution à partir duquel ils peuvent télécharger les fichiers du contenu que vous déployez.  

 Le point de distribution (non spécifique) de base est communément appelé point de distribution standard.  Il existe deux variantes du point de distribution standard qui reçoivent une attention particulière :  

-   **Point de distribution d’extraction** : variation d’un point de distribution où le point de distribution obtient le contenu à partir d’un autre point de distribution (point de distribution source), tout comme les clients téléchargent le contenu à partir de points de distribution. Les points de distribution d’extraction peuvent vous aider à éviter les goulots d’étranglement de bande passante réseau qui peuvent se produire quand le serveur de site doit distribuer directement le contenu à chaque point de distribution.  [Utiliser un point de distribution d’extraction avec System Center Configuration Manager](/sccm/core/plan-design/hierarchy/use-a-pull-distribution-point)  

-   **Point de distribution cloud** : variante d’un point de distribution installé dans Microsoft Azure. [Utiliser un point de distribution cloud avec System Center Configuration Manager](../../../core/plan-design/hierarchy/use-a-cloud-based-distribution-point.md)  


Les points de distribution standard prennent en charge diverses configurations et fonctionnalités, comme la limitation et la planification, le PXE et la multidiffusion, et le contenu préparé.  

-   Vous pouvez utiliser des contrôles tels que **planifications** ou **limitation de bande passante** pour contrôler ce transfert.  

-   Vous pouvez également utiliser d’autres options telles que le **contenu préparé**, les **points de distribution d’extraction**, ou exploiter **BranchCache** pour réduire la bande passante réseau utilisée quand vous déployez du contenu.  

-   Les points de distribution prennent en charge différentes configurations telles que **[PXE](../../../osd/get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_PXEDistributionPoint)** et **[Multidiffusion](../../../osd/get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_DPMulticast)** pour les déploiements de système d’exploitation, ou des configurations pour prendre en charge des **appareils mobiles**.  

 Les points de distribution d’extraction et cloud prennent en charge la plupart de ces configurations, mais certaines limitations s’appliquent à chaque variante de point de distribution.  

## <a name="distribution-point-group"></a>Groupe de points de distribution  
 Regroupements logiques de points de distribution pour simplifier la distribution de contenu.  

 Pour plus d’informations, consultez [Gérer les groupes de points de distribution](../../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_manage).

## <a name="distribution-point-priority"></a>Priorité des points de distribution  
 La valeur de priorité d’un point de distribution est basée sur le temps nécessaire au transfert des déploiements précédents vers ce point de distribution.  

-   Ajustée automatiquement, cette valeur est affectée à un point de distribution qui permet à Configuration Manager de transférer du contenu vers plusieurs points de distribution dans un délai plus bref.  

-   Quand vous distribuez du contenu vers plusieurs points de distribution en même temps ou vers un groupe de points de distribution, Configuration Manager envoie le contenu au point de distribution ayant la priorité la plus élevée avant d’envoyer ce même contenu à un point de distribution de priorité inférieure.  

-   Cela ne remplace pas la priorité de distribution pour les packages qui reste le facteur décisif dans la séquence de transfert des différentes distributions.  


**Par exemple** , si vous distribuez du contenu présentant une priorité de distribution élevée vers un point de distribution présentant une priorité de distribution basse, le package avec la priorité de distribution élevée est toujours transféré avant un package avec une priorité de distribution inférieure. La priorité de distribution s'applique même si les packages présentant une priorité de distribution basse sont distribués sur des points de distribution présentant des priorités de point de distribution élevées. La priorité de distribution élevée du package permet à Configuration Manager de distribuer ce contenu à ses points de distribution concernés avant d’envoyer les packages ayant une priorité de distribution inférieure.  

> [!NOTE]  
>  Les points de distribution d’extraction utilisent également un concept de priorité pour ordonner la séquence de leur points de distribution source.  
>   
>  -   La priorité des points de distribution pour les transferts de contenu d’un point de distribution à un autre est différente de la priorité utilisée par les points de distribution d’extraction lors de la recherche de contenu à partir d’un point de distribution source.  
> -   Pour plus d’informations, consultez [Utiliser un point de distribution d’extraction avec System Center Configuration Manager](/sccm/core/plan-design/hierarchy/use-a-pull-distribution-point).  


## <a name="fallback"></a>Secours  
 Les paramètres de secours sont liés à l’utilisation de **points de distribution préférés** et à l’emplacement de la source de contenu utilisée par les clients.  

-   Par défaut, les clients téléchargent uniquement le contenu à partir d’un point de distribution préféré (qui est associé aux groupes limites du client).  

-   Cependant, quand un point de distribution donné est configuré avec **Autoriser les clients à utiliser ce système de site en tant qu’emplacement source de secours du contenu**, ce point de distribution est proposé uniquement comme source de contenu valide aux clients qui ne peuvent pas obtenir un déploiement à partir de l’un de leurs points de distribution préférés.  


Pour plus d’informations sur les différents emplacements de contenu et les scénarios de secours, consultez [Scénarios d’emplacement source du contenu](../../../core/plan-design/hierarchy/content-source-location-scenarios.md).

## <a name="network-bandwidth"></a>Bande passante du réseau  
 Pour mieux gérer la quantité de bande passante réseau utilisée quand vous distribuez du contenu, vous pouvez utiliser les options suivantes :  

-   Utiliser du contenu préparé : processus de transfert de contenu vers un point de distribution sans passer par Configuration Manager pour distribuer le contenu sur le réseau.  

-   Utiliser la planification et la limitation : configurations qui vous aident à contrôler quand et comment le contenu est distribué aux points de distribution.  

Pour plus d’informations, consultez [Gérer la bande passante réseau](/sccm/core/plan-design/hierarchy/manage-network-bandwidth).

## <a name="network-connection-speed-to-content-source"></a>Vitesse de la connexion réseau vers la source de contenu  
 Vous pouvez configurer la vitesse de connexion réseau de chaque point de distribution d’un groupe de limites :  

-   Les clients utilisent cette valeur pour se connecter au point de distribution.  

-   Par défaut, la vitesse de connexion réseau est configurée sur **Rapide**, mais elle peut également être définie sur **Lente**.  

-   La **vitesse de connexion réseau** et la configuration de déploiement déterminent si un client peut télécharger du contenu à partir d’un point de distribution quand le client se trouve dans un groupe de limites associé.  


Pour plus d’informations sur les différents emplacements de contenu et les scénarios de secours, consultez [Scénarios d’emplacement source du contenu](../../../core/plan-design/hierarchy/content-source-location-scenarios.md).  

## <a name="on-demand-content-distribution"></a>Distribution de contenu à la demande  
 Vous pouvez définir cette option individuellement pour les applications et les packages (déploiements) afin d’activer la distribution de contenu à la demande vers les points de distribution préférés.  

-   Pour activer cette option pour un déploiement, sélectionnez **Distribuer le contenu pour ce package vers les points de distribution préférés**.  

-   Quand cette option est activée pour un déploiement et qu’un client tente de demander du contenu qui n’est disponible sur aucun des points de distribution préférés des clients, Configuration Manager distribue automatiquement ce contenu aux points de distribution préférés des clients.  

-   Même si cette option force Configuration Manager à distribuer automatiquement le contenu aux points de distribution préférés des clients, un client peut obtenir ce contenu auprès d’autres points de distribution avant que ses points de distribution préférés reçoivent le déploiement. Dans ce cas, le contenu est alors disponible sur ce point de distribution pour que le client suivant qui cherche ce déploiement puisse l’utiliser.  


Pour plus d’informations sur les différents emplacements de contenu et les scénarios de secours, consultez [Scénarios d’emplacement source du contenu](../../../core/plan-design/hierarchy/content-source-location-scenarios.md).  


## <a name="package-transfer-manager"></a>Package Transfer Manager  
 Composant de serveur de site qui transfère le contenu vers des points de distribution situés sur d’autres ordinateurs.  

 En savoir plus sur le [Package Transfer Manager](../../../core/plan-design/hierarchy/package-transfer-manager.md).  

## <a name="preferred-distribution-point"></a>Point de distribution préféré  
 Points de distribution associés aux groupes limites actuels d’un client.  

 Vous pouvez associer chaque point de distribution avec un ou plusieurs groupes de limites :  

-   Cette association permet au client de trouver plus facilement les points de distribution d’où il peut télécharger du contenu.  

-   Par défaut, les clients peuvent uniquement télécharger du contenu à partir d’un point de distribution préféré.  


Pour plus d’informations sur les différents emplacements de contenu et les scénarios de secours, consultez [Scénarios d’emplacement source du contenu](../../../core/plan-design/hierarchy/content-source-location-scenarios.md).  

## <a name="prestage-content"></a>Contenu préparé  
 Processus de transfert de contenu vers un point de distribution sans passer par Configuration Manager pour distribuer le contenu sur le réseau.  

 Pour plus d’informations, consultez [Gérer la bande passante réseau](/sccm/core/plan-design/hierarchy/manage-network-bandwidth).



<!--HONumber=Nov16_HO1-->


