---
title: "Cache d’homologue du client | System Center Configuration Manager"
description: "Utilisez le cache d’homologue pour les emplacements sources de contenu du client lors du déploiement de contenu avec System Center Configuration Manager."
ms.custom: na
ms.date: 7/31/2017
ms.reviewer: na
ms.suite: na
ms.prod: configuration-manager
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 86cd5382-8b41-45db-a4f0-16265ae22657
caps.latest.revision: 3
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: HT
ms.sourcegitcommit: 3c75c1647954d6507f9e28495810ef8c55e42cda
ms.openlocfilehash: 89fcd16887ae77299f9d18472ee6a1ba56794eca
ms.contentlocale: fr-fr
ms.lasthandoff: 07/29/2017

---

# <a name="peer-cache-for-configuration-manager-clients"></a>Cache d’homologue pour les clients Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

À compter de System Center Configuration Manager version 1610, vous pouvez utiliser le **cache d’homologue** pour faciliter la gestion du déploiement de contenu sur des clients dans des emplacements distants. Le cache d’homologue est une solution Configuration Manager intégrée qui permet aux clients de partager du contenu avec d’autres clients directement à partir de leur cache local.   

> [!TIP]  
> Depuis la version 1610, le cache d’homologue et le tableau de bord Sources de données du client sont des fonctionnalités en préversion. Pour les activer, consultez [Utiliser des fonctionnalités de préversion des mises à jour](/sccm/core/servers/manage/pre-release-features).

## <a name="overview"></a>Vue d'ensemble
Un client de cache d’homologue est un client Configuration Manager qui est activé pour utiliser le cache d’homologue. Un client de cache d’homologue qui a du contenu qu’il peut partager avec d’autres clients est une source de cache d’homologue.
 -  Vous utilisez des paramètres du client pour permettre aux clients d’utiliser le cache d’homologue.
 -  Pour partager du contenu en tant que source de cache d’homologue, un client de cache d’homologue :
    -  Les appareils doivent être joints à un domaine. Toutefois, un client qui n’est pas joint à un domaine peut obtenir du contenu à partir d’une source de cache d’homologue jointe à un domaine.
    -  Il doit être un membre du groupe de limites actuel du client qui recherche le contenu. Un client du cache d’homologue dans les groupes de limites voisins n’est pas inclus dans le pool des emplacements sources de contenu disponibles quand un client utilise une action de secours pour rechercher du contenu à partir d’un groupe de limites voisin. Pour plus d’informations sur les groupes de limites actuels et voisins, consultez [Groupes de limites](/sccm/core/servers/deploy/configure/define-site-boundaries-and-boundary-groups##a-namebkmkboundarygroupsa-boundary-groups).
 - Chaque type de contenu conservé dans le cache d’un client Configuration Manager peut être fourni à d’autres clients à l’aide du cache d’homologue.
 -  Le cache d’homologue ne remplace pas l’utilisation d’autres solutions telles que BranchCache, mais fonctionne en association avec lui afin de vous offrir davantage d’options pour l’extension de solutions de déploiement de contenu traditionnelles telles que des points de distribution. Il s’agit d’une solution personnalisée sans recours à BranchCache. Par conséquent, si vous n’activez pas ou n’utilisez pas Windows BranchCache, elle fonctionne quand même.

### <a name="operations"></a>Opérations

Après avoir déployé des paramètres du client qui activent le cache d’homologue sur un regroupement, les membres de ce regroupement peuvent agir comme source de contenu homologue pour d’autres clients du même groupe de limites :
 -  Un client qui agit en tant que source de contenu homologue envoie une liste des contenus mis en cache disponibles à son point de gestion.
 -  Ensuite, quand le client suivant dans ce groupe de limites demande ce contenu, chaque source de cache d’homologue disposant du contenu est retournée comme source de contenu potentielle avec les points de distribution et d’autres emplacements de sources de contenu dans ce groupe de limites.
 -  Selon le processus de fonctionnement normal, le client qui recherche le contenu sélectionne une source de contenu dans le pool de sources qu’il a proposé, puis continue pour essayer d’obtenir le contenu.

> [!NOTE]
> En cas de recours à un groupe de limites voisin pour le contenu, les emplacements sources de contenu de cache d’homologue à partir du groupe de limites voisin ne sont pas ajoutés au pool des emplacements de sources de contenu potentiels du client.  


Même si vous pouvez faire participer tous les clients comme sources de cache d’homologue, il est recommandé de choisir uniquement les clients les mieux adaptés pour être des sources de cache d’homologue.  L’adéquation des clients peut être évaluée en fonction du type de châssis d’un client, de l’espace disque, de la connectivité réseau, et bien plus encore. Pour plus d’informations vous permettant de sélectionner les meilleurs clients à utiliser pour le cache d’homologue, consultez [ce blog rédigé par un consultant Microsoft](https://blogs.technet.microsoft.com/setprice/2016/06/29/pe-peer-cache-custom-reporting-examples/).

**Accès limité à une source de cache d’homologue**  
À partir de la version 1702, un ordinateur source de cache d’homologue rejette une demande de contenu quand il remplit l’une des conditions suivantes :  
  -  Il est en mode de batterie faible.
  -  La charge de l’UC dépasse 80 % au moment où le contenu est demandé.
  -  Les E/S disque ont une valeur *AvgDiskQueueLength* supérieure à 10.
  -  Il n’y a plus de connexion disponible vers l’ordinateur.   

Vous pouvez configurer ces paramètres à l’aide de la classe WMI du serveur de configuration du client pour la fonctionnalité de source d’homologue (*SMS_WinPEPeerCacheConfig*) quand vous utilisez le SDK System Center Configuration Manager.

Quand l’ordinateur rejette une demande de contenu, l’ordinateur demandeur continue à rechercher le contenu dans d’autres sources de son pool d’emplacements de sources de contenu disponibles.   



### <a name="monitoring"></a>monitoring   
Pour vous aider à comprendre l’utilisation du cache d’homologue, vous pouvez afficher le tableau de bord Sources de données du client. Consultez la section relative au [tableau de bord Sources de données du client](/sccm/core/servers/deploy/configure/monitor-content-you-have-distributed#client-data-sources-dashboard).

À partir de la version 1702, vous pouvez utiliser trois rapports pour afficher l’utilisation du cache d’homologue. Dans la console, accédez à **Surveillance** > **Comptes rendus** > **Rapports**. Tous les rapports ont le type **Contenu de distribution de logiciels** :
1.  **Rejet du contenu de la source de cache d’homologue** :  
Utilisez ce rapport pour comprendre la fréquence à laquelle les sources de cache d’homologue d’un groupe de limites ont rejeté une demande de contenu.
 - **Problème connu :** lorsque vous descendez dans la hiérarchie pour accéder à des résultats comme *MaxCPULoad* ou *MaxDiskIO*, il se peut que vous receviez une erreur qui indique que le rapport ou les détails sont introuvables. Pour contourner ce problème, utilisez les deux rapports suivants, qui montrent directement les résultats.

2. **Rejet conditionnel du contenu de la source de cache d’homologue** :  
Utilisez ce rapport pour comprendre les détails du rejet pour un groupe de limites ou un type de rejet donné. Vous pouvez spécifier :

  - **Problème connu :** vous ne pouvez pas choisir parmi une liste de paramètres disponibles ; vous devez les entrer manuellement. Entrez les valeurs *Nom de groupe de limites* et *Type de rejet* comme dans le premier rapport. Par exemple, pour *Type de rejet*, vous pouvez entrer *MaxCPULoad* ou *MaxDiskIO*.

3. **Détails du rejet du contenu de la source de cache d’homologue** :   
  Utilisez ce rapport pour comprendre quel était le contenu demandé au moment du rejet.

 - **Problème connu :** vous ne pouvez pas choisir parmi une liste de paramètres disponibles ; vous devez les entrer manuellement. Entrez la valeur *Type de rejet* qui s’affiche dans le premier rapport (Rejet du contenu de la source de cache d’homologue) et entrez *l’ID de ressource* de la source de contenu sur laquelle vous souhaitez obtenir des informations.  Pour trouver l’ID de ressource de la source de contenu :  

    1. Recherchez le nom de l’ordinateur qui s’affiche comme *Source de cache d’homologue* dans les résultats du deuxième rapport (Rejet conditionnel du contenu de la source de cache d’homologue).  
    2. Ensuite, accédez à **Biens et conformité** > **Appareils**, puis recherchez ce nom d’ordinateur. Utilisez la valeur de la colonne ID de ressource.  


## <a name="requirements-and-considerations-for-peer-cache"></a>Exigences et considérations relatives au cache d’homologue
-   Le cache d’homologue est pris en charge sur tout système d’exploitation Windows pris en charge en tant que client Configuration Manager. Les systèmes d’exploitation autres que Windows ne sont pas pris en charge pour le cache d’homologue.

-   Des clients ne peuvent transférer du contenu qu’à partir de clients de cache d’homologue qui se trouvent dans leur groupe de limites actuel.

-   Avant la version 1706, chaque site où les clients utilisent le cache d’homologue doit être configuré avec un [compte d’accès réseau](/sccm/core/plan-design/hierarchy/manage-accounts-to-access-content#a-namebkmknaaa-network-access-account). Depuis la version 1706, ce compte n’est plus nécessaire, sauf dans le cas suivant :  un client utilise le cache d’homologue pour obtenir et exécuter une séquence de tâches depuis le Centre logiciel et la séquence de tâches redémarre le client en mode WinPE.  Dans ce scénario, le client a toujours besoin du compte d’accès réseau quand il est en mode WinPE pour accéder à l’ordinateur source du cache d’homologue afin d’obtenir du contenu.

    Quand il est nécessaire, le compte d’accès réseau est utilisé par l’ordinateur source du cache d’homologue pour authentifier les demandes de téléchargement provenant des homologues et nécessite pour cela seulement des autorisations d’utilisateur du domaine.

-   Étant donné que la limite actuelle d’une source de contenu de cache d’homologue est déterminée par la soumission de l’inventaire matériel de ces clients, un client qui se déplace vers un emplacement réseau et qui se trouve dans un autre groupe de limites peut toujours être considéré comme un membre de son précédent groupe de limites pour les besoins du cache d’homologue. En conséquence, un client peut se voir proposer une source de contenu de cache d’homologue qui ne se trouve pas dans son emplacement réseau immédiat. Nous vous recommandons d’empêcher les clients qui adoptent souvent cette configuration de participer à une source de cache d’homologue.

## <a name="to-configure-client-peer-cache-client-settings"></a>Pour configurer les paramètres client du cache d’homologue du client
1.  Dans la console Configuration Manager, accédez à **Administration** > **Paramètres client**, puis ouvrez l’objet des paramètres de client d’appareil que vous voulez utiliser. Vous pouvez également modifier l’objet des paramètres client par défaut.
2.  Dans la liste des paramètres disponibles, choisissez **Paramètres du cache du client**.
3.  Définissez **Permettre au client Configuration Manager exécutant le système d’exploitation complet de partager du contenu** sur **Oui**.
4.  Configurez les paramètres suivants pour définir les ports que vous souhaitez utiliser pour le cache d’homologue :  
  -  **Port pour la diffusion réseau initiale**
  -  **Activer HTTPS pour la communication d’homologues clients**
  -  **Port pour le téléchargement de contenu à partir d’un homologue (HTTP/HTTPS)**

Sur chaque ordinateur activé pour le cache d’homologue, si le Pare-feu Windows est en cours d’utilisation, Configuration Manager le configure pour autoriser l’utilisation des ports que vous configurez.

