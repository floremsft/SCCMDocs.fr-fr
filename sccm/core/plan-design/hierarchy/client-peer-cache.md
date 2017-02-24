
---
title: "Cache d’homologue du client | System Center Configuration Manager"
description: "Utilisez le cache d’homologue pour les emplacements sources de contenu du client lors du déploiement de contenu avec System Center Configuration Manager."
ms.custom: na
ms.date: 2/13/2017
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
translationtype: Human Translation
ms.sourcegitcommit: 2dd898c9b022c6f0bc243623835af0eece94128f
ms.openlocfilehash: 95d1671501f672e1d5abe3f0fbbd7d2dfb21e0a3

---
# <a name="peer-cache-for-configuration-manager-clients"></a>Cache d’homologue pour les clients Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

À compter de System Center Configuration Manager version 1610, vous pouvez utiliser le **cache d’homologue** pour faciliter la gestion du déploiement de contenu sur des clients dans des emplacements distants. Le cache d’homologue est une solution Configuration Manager intégrée qui permet aux clients de partager du contenu avec d’autres clients directement à partir de leur cache local.   

> [!TIP]  
> Avec la version 1610, le cache d’homologue et le tableau de bord Sources de données du client sont des fonctionnalités en préversion. Pour les activer, consultez [Utiliser des fonctionnalités de préversion des mises à jour](/sccm/core/servers/manage/install-in-console-updates#bkmk_prerelease).

 -     Vous utilisez des paramètres du client pour permettre aux clients d’utiliser le cache d’homologue.
 -     Pour partager du contenu, les clients du cache d’homologue doivent être membres du groupe de limites actuel du client qui recherche le contenu. Les clients du cache d’homologue dans les groupes de limites voisins ne sont pas inclus dans le pool des emplacements sources de contenu disponibles quand un client utilise une action de secours pour rechercher du contenu à partir d’un groupe de limites voisin. Pour plus d’informations sur les groupes de limites actuels et voisins, consultez [Groupes de limites](/sccm/core/servers/deploy/configure/define-site-boundaries-and-boundary-groups##a-namebkmkboundarygroupsa-boundary-groups).
 - Les clients non activés pour le cache d’homologue mais qui font partie du groupe de limites actuel avec des clients activés pour le cache d’homologue peuvent obtenir du contenu de la part du client activé pour le cache d’homologue.  
 - Chaque type de contenu conservé dans le cache d’un client Configuration Manager peut être fourni à d’autres clients à l’aide du cache d’homologue.
 -    Le cache d’homologue ne remplace pas l’utilisation d’autres solutions telles que BranchCache, mais fonctionne en association avec lui afin de vous offrir davantage d’options pour l’extension de solutions de déploiement de contenu traditionnelles telles que des points de distribution. Il s’agit d’une solution personnalisée sans recours à BranchCache. Par conséquent, si vous n’activez pas ou n’utilisez pas Windows BranchCache, elle fonctionne quand même.

Après avoir déployé des paramètres du client qui activent le cache d’homologue sur un regroupement, les membres de ce regroupement peuvent agir comme source de contenu homologue pour d’autres clients du même groupe de limites :
 -    Un client qui agit en tant que source de contenu homologue envoie une liste des contenus mis en cache disponibles à son point de gestion.
 -    Ensuite, quand le client suivant dans ce groupe de limites demande ce contenu, chaque source de cache d’homologue disposant du contenu est retournée comme source de contenu potentielle avec les points de distribution et d’autres emplacements de sources de contenu dans ce groupe de limites.
 -    Selon le processus de fonctionnement normal, le client qui recherche le contenu sélectionne une source de contenu dans le pool de sources qu’il a proposé, puis continue pour essayer d’obtenir le contenu.

> [!NOTE]
> En cas de recours à un groupe de limites voisin pour le contenu, les emplacements sources de contenu de cache d’homologue à partir du groupe de limites voisin ne sont pas ajoutés au pool des emplacements de sources de contenu potentiels du client.  

Même si vous pouvez faire participer tous les clients au cache d’homologue, il est recommandé de choisir uniquement les clients les mieux adaptés pour être des sources de cache d’homologue.  L’adéquation des clients peut être évaluée en fonction du type de châssis d’un client, de l’espace disque, de la connectivité réseau, et bien plus encore. Pour plus d’informations vous permettant de sélectionner les meilleurs clients à utiliser pour le cache d’homologue, consultez [ce blog rédigé par un consultant Microsoft](https://blogs.technet.microsoft.com/setprice/2016/06/29/pe-peer-cache-custom-reporting-examples/).

Pour vous aider à comprendre l’utilisation du cache d’homologue, vous pouvez afficher le tableau de bord Sources de données du client. Consultez la section relative au [tableau de bord Sources de données du client](/sccm/core/servers/deploy/configure/monitor-content-you-have-distributed#client-data-sources-dashboard).


## <a name="requirements-and-considerations-for-peer-cache"></a>Exigences et considérations relatives au cache d’homologue
- Le cache d’homologue est pris en charge sur tout système d’exploitation Windows pris en charge en tant que client Configuration Manager. Les systèmes d’exploitation autres que Windows ne sont pas pris en charge pour le cache d’homologue.

- Des clients ne peuvent transférer du contenu qu’à partir de clients de cache d’homologue qui se trouvent dans leur groupe de limites actuel.

-     Étant donné que la limite actuelle d’une source de contenu de cache d’homologue est déterminée par la soumission de l’inventaire matériel de ces clients, un client qui se déplace vers un emplacement réseau et qui se trouve dans un autre groupe de limites peut toujours être considéré comme un membre de son précédent groupe de limites pour les besoins du cache d’homologue. En conséquence, un client peut se voir proposer une source de contenu de cache d’homologue qui ne se trouve pas dans son emplacement réseau immédiat. Nous vous recommandons d’empêcher les clients qui adoptent souvent cette configuration de participer à une source de cache d’homologue.

## <a name="to-configure-client-peer-cache-client-settings"></a>Pour configurer les paramètres client du cache d’homologue du client
1.    Dans la console Configuration Manager, accédez à **Administration** > **Paramètres client**, puis ouvrez l’objet des paramètres de client d’appareil que vous voulez utiliser. Vous pouvez également modifier l’objet des paramètres client par défaut.
2.    Dans la liste des paramètres disponibles, choisissez **Paramètres du cache du client**.
3.    Définissez **Permettre au client Configuration Manager exécutant le système d’exploitation complet de partager du contenu** sur **Oui**.
4.    Configurez les paramètres suivants pour définir les ports que vous souhaitez utiliser pour le cache d’homologue :  
  -  **Port pour la diffusion réseau initiale**
  -  **Activer HTTPS pour la communication d’homologues clients**
  -  **Port pour le téléchargement de contenu à partir d’un homologue (HTTP/HTTPS)**

Sur chaque ordinateur activé pour le cache d’homologue, si le Pare-feu Windows est en cours d’utilisation, Configuration Manager le configure pour autoriser l’utilisation des ports que vous configurez.



<!--HONumber=Feb17_HO4-->


