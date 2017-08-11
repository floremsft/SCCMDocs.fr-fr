---
title: "Définir des groupes de limites | Microsoft Docs"
description: "Découvrez les groupes de limites qui lient les clients aux systèmes de site dans System Center Configuration Manager."
ms.custom: na
ms.date: 7/31/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 5db2926f-f03e-49c7-b44b-e89b1a5a6779
caps.latest.revision: 10
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: HT
ms.sourcegitcommit: 3c75c1647954d6507f9e28495810ef8c55e42cda
ms.openlocfilehash: 5debc6559f4b1c213e8ca513d685941c9e669063
ms.contentlocale: fr-fr
ms.lasthandoff: 07/29/2017

---
# <a name="configure-boundary-groups-for-system-center-configuration-manager"></a>Configurer les groupes de limites pour System Center Configuration Manager


*S’applique à : System Center Configuration Manager (Current Branch)*

Les groupes de limites de System Center Configuration Manager vous permettent de regrouper de façon logique des emplacements réseau ([limites](/sccm/core/servers/deploy/configure/boundaries)) pour faciliter la gestion de votre infrastructure. Une fois des limites attribuées à des groupes de limites, vous pouvez utiliser le groupe de limites.

Par défaut, Configuration Manager crée un groupe de limites de site par défaut sur chaque site.

> [!IMPORTANT]  
>  **Les informations contenues dans cette section sur les groupes de limites et ses sections enfants s’appliquent à la version 1610 ou ultérieure.** Ce contenu a été modifié pour refléter les modifications de conception appliquées aux groupes de limites dans cette version de mise à jour.
>
> **Si vous utilisez des versions antérieures à 1610**, consultez la page [Groupes de limites pour les versions 1511, 1602 et 1606 de System Center Configuration Manager](/sccm/core/servers/deploy/configure/boundary-groups-for-1511-1602-and-1606) pour plus d’informations sur l’utilisation et la configuration des groupes de limites avec ces versions de produit.

Pour configurer des groupes de limites, on associe des limites (emplacements réseau) et des rôles de système de site, comme les points de distribution, au groupe de limites. Cela permet d’associer les clients aux serveurs de système de site tels que les points de distribution qui se trouvent près des clients sur le réseau.

Quand vous affectez la même limite à plusieurs groupes de limites, et les mêmes serveurs de système de site, par exemple des points de distribution, à plusieurs groupes de limites, vous augmentez la disponibilité des systèmes de site sur un large éventail d’emplacements réseau.

Les clients utilisent un groupe de limites pour les applications suivantes :  

-   Attribution automatique du site  
-   Recherche d’un serveur de système de site capable de fournir un service, notamment :
    - Points de distribution pour l’emplacement du contenu
    -   Points de mise à jour logicielle (à partir de la version 1702)
    - Points de migration de l'état
    - Points de gestion préférés (Si vous utilisez des points de gestion préférés, vous devez activer cette option pour la hiérarchie et non pas à partir de la configuration du groupe de limites. Consultez la section [Activer l’utilisation des points de gestion préférés](#to-enable-use-of-preferred-management-points) de cette rubrique.)

##  <a name="boundary-groups-and-relationships"></a>Relations et groupes de limites
Pour chaque groupe de limites de votre hiérarchie, vous pouvez affecter :

-  Une ou plusieurs limites. Lorsqu’un client se trouve sur un emplacement réseau défini comme limite affectée à un groupe de limites donné, celui-ci est appelé groupe de limites **actif**. Un client peut avoir plusieurs groupes de limites actifs.
- Un ou plusieurs rôles de système de site.  Les clients peuvent toujours utiliser des rôles de système de site associés à leur groupe de limites actif. En fonction des configurations supplémentaires, ils peuvent dans certains cas utiliser les rôles de système de site dans les groupes de limites supplémentaires.  

Pour chaque groupe de limites créé, vous pouvez configurer un lien à sens unique vers un autre groupe de limites. Ce lien est appelé **relation**. Les groupes de limites vers lequel pointent ces liens sont appelés groupes de limites **voisins**. Un groupe de limites peut avoir plusieurs relations, chacune avec un groupe de limites voisin spécifique.

La configuration de chaque relation détermine quand un client qui ne parvient pas à trouver un serveur de système de site disponible dans son groupe de limites actif peut commencer à chercher un système de site disponible dans un groupe de limites voisin. Cette recherche dans des groupes supplémentaires est appelée **secours**.

## <a name="fallback"></a>Secours
Pour éviter des problèmes dans le cas où les clients ne trouvent pas de système de site disponible dans leur groupe de limites actif, vous définissez une relation entre les groupes de limites qui définit le comportement de l’action de secours. Le secours permet à un client d’étendre sa recherche à des groupes de limites supplémentaires pour trouver un système de site disponible.

Les relations sont configurées dans l’onglet **Relations** des propriétés du groupe de limites. Lorsque vous configurez une relation, vous définissez un lien vers un groupe de limites voisin. Pour chaque type de rôle de système de site pris en charge, vous pouvez configurer des paramètres indépendants pour le recours à ce groupe de limites voisin. Par exemple, lorsque vous configurez une relation vers un groupe de limites donné, vous pouvez définir le déclenchement du secours après 20 minutes au lieu des 120 minutes par défaut pour les points de distribution. Consultez la page [Exemple d’utilisation des groupes de limites](#example-of-using-boundary-groups) pour voir un exemple plus complet.

Si un client ne trouve pas un rôle de système de site disponible dans son groupe de limites actif, il utilise le délai de secours en minutes pour déterminer combien de temps il doit attendre avant de commencer à rechercher un système de site disponible associé à ce groupe de limites voisin.  

Lorsqu’un client ne trouve pas de système de site disponible et commence à rechercher dans les emplacements de groupes de limites voisins, il augmente le pool de systèmes de site disponibles utilisables d’une manière définie par la configuration des groupes de limites et de leurs relations.

- Un groupe de limites peut avoir plusieurs relations. Au moyen de plusieurs relations, vous pouvez configurer l’action de secours pour chaque type de système de site sur différents voisins de sorte qu’ils interviennent après différents délais.    
- Les clients utilisent uniquement en secours un groupe de limites qui est un voisin direct de leur groupe de limites actuel.
- Quand un client est membre de plusieurs groupes de limites, le groupe de limites actuel est défini en tant qu’union de tous les groupes de limites de ce client. Ce client peut ensuite recourir à des voisins de n’importe lequel de ces groupes de limites d’origine.

### <a name="the-default-site-boundary-group"></a>Le groupe de limites de site par défaut
Outre les groupes de limites que vous créez, chaque site possède un groupe de limites de site par défaut créé par Configuration Manager. Ce groupe est nommé ***Default-Site-Boundary-Group&lt;sitecode>***. Par exemple, le groupe du site ABC s’appellerait *Default-Site-Boundary-Group&lt;ABC>.*

Pour chaque groupe de limites que vous créez, Configuration Manager crée automatiquement un lien implicite vers chacun des groupes de limites de site par défaut de la hiérarchie.
-   Le lien implicite est une option de secours par défaut d’un groupe de limites actif vers le groupe de limites de site par défaut, qui a un délai de secours par défaut de 120 minutes.
-   Les clients qui ne sont pas sur une limite associée à un groupe de limites de votre hiérarchie utilisent automatiquement le groupe de limites par défaut du site qui leur a été affecté pour identifier des rôles de système de site valides utilisables.

Pour gérer le recours au groupe de limites de site par défaut :
- Vous pouvez accéder aux propriétés du groupe de limites de site par défaut et modifier les valeurs de l’onglet **Comportement par défaut**. Les modifications apportées ici s’appliquent à *tous* les liens implicites vers ce groupe de limites. Ces paramètres peuvent être remplacés lorsque vous configurez le lien explicite vers ce groupe de limites de site par défaut à partir d’un autre groupe de limites.
- Vous pouvez accéder aux propriétés d’un groupe de limites que vous avez créé et modifier les valeurs du lien explicite vers un groupe de limites de site par défaut. Lorsque vous définissez un nouveau délai de secours ou de secours en bloc en minutes, cette modification affecte uniquement le lien que vous configurez. Les configurations du lien explicite remplacent ceux de l’onglet **Comportement par défaut** d’un groupe de limites de site par défaut.


## <a name="site-assignment"></a>Attribution de site  
 Vous pouvez configurer chaque groupe de limites avec un site attribué pour les clients.  

-   Quand un client récemment installé utilise l’attribution automatique de site, il rejoint le site attribué d’un groupe de limites qui englobe l’emplacement réseau actuel du client.  
-   Après avoir été attribué à un site, un client ne modifie pas son attribution de site quand il change d’emplacement réseau. Par exemple, si le client se déplace vers un nouvel emplacement réseau représenté par une limite dans un groupe de limites disposant d’une attribution de site différente, le site attribué au client n’est pas modifié.  
-   Lorsque la découverte de systèmes Active Directory détecte une nouvelle ressource, les informations sur le réseau de la ressource découverte sont évaluées en fonction des limites dans les groupes de limites. Ce processus associe la nouvelle ressource à un site attribué pour une utilisation par la méthode d'installation poussée du client.  
-   Quand une limite est membre de plusieurs groupes de limites auxquels différents sites sont attribués, les clients sélectionnent l’un des sites de manière aléatoire.  
-   Les modifications apportées à un site attribué à des groupes de limites s’appliquent uniquement aux nouvelles actions d’attribution de site. Les clients déjà attribués à un site ne réévaluent pas leur attribution à un site en fonction des changements apportés à la configuration du groupe de limites (ou à leur emplacement réseau).  

Pour plus d’informations sur l’attribution de site client, consultez [Utilisation de l’attribution automatique de site pour les ordinateurs](../../../../core/clients/deploy/assign-clients-to-a-site.md#BKMK_AutomaticAssignment) dans [Guide pratique pour affecter des clients à un site dans System Center Configuration Manager](../../../../core/clients/deploy/assign-clients-to-a-site.md).  

## <a name="distribution-points"></a>Points de distribution

Lorsqu’un client demande l’emplacement d’un point de distribution, Configuration Manager envoie au client une liste qui comprend les systèmes de site du type approprié associés à chaque groupe de limites qui inclut l’emplacement réseau actuel du client :

-   **Lors de la distribution de logiciels**, les clients demandent un emplacement pour le contenu de déploiement disponible à partir d’un point de distribution, ou une autre source de contenu valide (par exemple, un client configuré pour le cache d’homologue).

-   **Durant le déploiement de système d’exploitation**, les clients demandent un emplacement où envoyer ou recevoir des informations sur la migration de leur état.  

Lors du déploiement de contenu, si un client demande du contenu qui n’est pas disponible à partir d’une source de son groupe de limites actif, le client continue de demander ce contenu en essayant différentes sources de contenu dans son groupe de limites actif, jusqu’à ce que la période de secours d’un groupe de limites voisin ou du groupe de limites de site par défaut soit atteinte. Si le client n’a pas encore trouvé de contenu, il étend ensuite sa recherche de sources de contenu aux groupes de limites voisins.

Toutefois, si le contenu est distribué à la demande et non disponible sur un point de distribution au moment où le client le demande, le processus de transfert du contenu vers ce point de distribution commence, et il est possible que le client trouve ce serveur comme source de contenu avant d’utiliser un groupe de limites voisin en secours.

## <a name="software-update-points"></a>Points de mise à jour logicielle
À partir de la version 1702, les clients utilisent des groupes de limites pour rechercher un nouveau point de mise à jour logicielle. Vous pouvez ajouter des points de mise à jour logicielle individuels à différents groupes de limites pour contrôler les serveurs qu’un client peut trouver.

Si vous effectuez la mise à jour à partir d’une version antérieure à la version 1702, tous les points de mise à jour logicielle existants sont ajoutés au groupe de limites de site par défaut de chaque site. Cela permet de conserver le comportement d’avant la mise à jour, selon lequel les clients sélectionnent un point de mise à jour logicielle dans le pool de points de mise à jour logicielle disponibles que vous avez configuré pour votre hiérarchie.  Ce comportement est conservé tant que vous ne choisissez pas d’ajouter des points de mise à jour logicielle propres à chaque groupe de limites pour une sélection contrôlée et un comportement de secours.

Si vous installez un nouveau site qui exécute la version 1702 ou une version ultérieure, des points de mise à jour logicielle ne sont pas ajoutés au groupe de limites de site par défaut. Attribuez des points de mise à jour logicielle à un groupe de limites afin que les clients puissent les trouver et les utiliser.

### <a name="fallback-for-software-update-points"></a>Action de secours pour les points de mise à jour logicielle
Pour les points de mise à jour logicielle, le secours est configuré comme les autres rôles de système de site, mais avec les restrictions suivantes :
- **Les nouveaux clients utilisent des groupes de limites pour sélectionner les points de mise à jour logicielle.** Une fois la version 1702 installée, les nouveaux clients installés sélectionnent un point de mise à jour logicielle parmi ceux qui sont associés aux groupes de limites que vous avez configurés. Ce comportement vient remplacer celui qui consistait, pour les clients, à sélectionner un point de mise à jour logicielle de manière aléatoire dans la liste des points partageant la même forêt du client.

- **Les clients continuent d’utiliser un dernier point de mise à jour logicielle correct connu jusqu’à ce qu’ils en recherchent un nouveau une fois l’action de secours lancée.** Les clients qui disposent déjà d’un point de mise à jour logicielle continuent d’utiliser ce point jusqu’à ce que ce serveur ne soit plus accessible.  Cela comprend la poursuite de l’utilisation d’un point de mise à jour logicielle non associé au groupe de limites actif du client.

  Le fait qu’un point de mise à jour logicielle existant soit utilisé même si ce serveur ne se trouve pas dans le groupe de limites actif du client est intentionnel. En effet, le changement de point de mise à jour logicielle peut entraîner une utilisation importante de la bande passante, car le client synchronise ses données avec le nouveau point de mise à jour logicielle. Ce délai se révèle donc utile. Le délai de transition peut permettre d’éviter la saturation du réseau, si tous vos clients devaient basculer vers un nouveau point de mise à jour logicielle en même temps.

- **Un client tente toujours d’atteindre son dernier point de mise à jour logicielle correct connu pendant 120 minutes avant de démarrer l’action de secours.** Après 120 minutes, si le client n’a pas établi de contact, il démarre l’action de secours. Quand l’action de secours démarre, le client reçoit la liste de tous les points de mise à jour logicielle à partir de son groupe de limites actif. Des points de mise à jour logicielle supplémentaires à partir de groupes de limites voisins et du groupe de limites de site par défaut sont disponibles en fonction des configurations de l’action de secours.

### <a name="fallback-configurations-for-software-update-points"></a>Configurations de l’action de secours pour les points de mise à jour logicielle
#### <a name="beginning-with-version-1706"></a>Depuis la version 1706   
Vous pouvez configurer des **durées avant repli (en minutes)** inférieures à 120 minutes pour les points de mise à jour logicielle. Toutefois, le client doit toujours essayer d’atteindre son point de mise à jour logicielle d’origine pendant 120 minutes avant qu’il n’étende sa recherche à des serveurs supplémentaires. Étant donné que les actions de secours des groupes de limites démarrent dès que le client ne parvient pas à atteindre le serveur d’origine, tous les groupes de limites qui sont configurés pour une durée inférieure à 120 minutes sont fournis au client quand il étend sa recherche après n’être pas parvenu à atteindre son serveur d’origine pendant 120 minutes.

Vous pouvez configurer **Jamais d’action de secours** pour bloquer l’action de secours pour un point de mise à jour logicielle vers un groupe de limites voisin.

Après avoir échoué pendant deux heures à atteindre le serveur d’origine, le client utilise un cycle plus court pour établir une connexion à un nouveau point de mise à jour logicielle. Ainsi, le client peut explorer rapidement la liste croissante des points de mise à jour logicielle potentiels.

 -  **Exemple d’action de secours :**  
    Le groupe de limites actuel d’un client a, pour les points de mise à jour logicielle, une action de secours dont la configuration est la suivante : *10* minutes pour le groupe de limites *A* et *130* minutes pour le groupe de limites *B*. Quand le client ne parvient pas à atteindre son dernier point de mise à jour logicielle correct connu :
    -   Le client tente d’atteindre uniquement son serveur d’origine pendant les 120 minutes suivantes.  Après 10 minutes, les points de mise à jour logicielle du groupe de limites A sont ajoutés au pool de serveurs disponibles. Toutefois, le client ne peut pas tenter de contacter ces derniers ou tout autre serveur jusqu’à ce que se soit écoulée la période initiale de 120 minutes de reconnexion au serveur d’origine.
    -   Après avoir essayé de localiser ce point de mise à jour logicielle d’origine pendant 120 minutes, le client peut étendre sa recherche. À ce stade, les serveurs dans le groupe de limites actuel du client et tous les groupes de limites voisins qui sont configurés avec une durée inférieure ou égale à 120 minutes sont ajoutés au pool disponible des points de mise à jour logicielle. Cela inclut les serveurs du groupe de limites A qui ont été ajoutés au pool de serveurs disponibles.
    -       Après 10 minutes supplémentaires (soit un total de 130 minutes après le premier échec du client dans sa tentative d’atteindre son dernier point de mise à jour logicielle correct connu), le client étend la recherche pour inclure les points de mise à jour logicielle du groupe de limites B.  

#### <a name="prior-to-version-1706"></a>Avant la version 1706
Avant la version 1706, les configurations de l’action de secours pour les points de mise à jour logicielle ne gèrent pas une période configurable en minutes. Le comportement de l’action de secours est limité comme suit :

  - **Délai de secours (en minutes) :** cette option est grisée pour les points de mise à jour logicielle et n’est pas configurable. Elle est définie sur 120 minutes.
  -     **Ne jamais activer le secours :** vous pouvez bloquer le secours pour un point de mise à jour logicielle vers un groupe de limites voisin lorsque vous utilisez cette configuration.

Lorsqu’un client qui possède déjà un point de mise à jour logicielle ne parvient pas à l’atteindre, il peut en chercher un autre en secours. En cas d’utilisation du secours, le client reçoit la liste de tous les points de mise à jour logicielle à partir de son groupe de limites actif. S’il ne trouve pas de serveur disponible en 120 minutes, il a ensuite recours à ses groupes de limites voisin et au groupe de limites de site par défaut. Le recours aux deux groupes de limites se produit en même temps, car le délai de secours des points de mise à jour logicielle vers les groupes voisins est défini sur 120 minutes et n’est pas modifiable. 120 minutes correspond également à la durée par défaut utilisée pour le recours au groupe de limites de site par défaut. Lorsque le client a recours à la fois à un groupe de limites voisin et au groupe de limites de site par défaut, il tente de contacter les points de mise à jour logicielle du groupe de limites voisin avant d’essayer d’utiliser ceux du groupe de limites de site par défaut.

### <a name="manually-switch-to-a-new-software-update-point"></a>Basculer manuellement vers un nouveau point de mise à jour logicielle
Outre l’action de secours, vous pouvez utiliser *Notification du client* pour forcer manuellement un appareil à basculer vers un nouveau point de mise à jour logicielle.

Quand vous basculez vers un nouveau serveur, les appareils utilisent l’action de secours pour rechercher ce serveur. C’est pourquoi vous devez passer en revue vos configurations de groupe de limites et vérifiez que vos points de mise à jour logicielle sont dans les groupes de limites appropriés avant de procéder à ce changement.

Pour plus d’informations, consultez [Basculer manuellement les clients vers un nouveau point de mise à jour logicielle](/sccm/sum/plan-design/plan-for-software-updates#manually-switch-clients-to-a-new-software-update-point).


## <a name="preferred-management-points"></a>Points de gestion préférés

 Les points de gestion préférés permettent à un client d’identifier un point de gestion associé à son emplacement réseau actuel (limite) avec celui-ci.  

-   Un client essaie d’utiliser un point de gestion préféré de son site attribué avant d’en utiliser un qui n’est pas configuré comme préféré.  
-   Pour utiliser cette option, vous devez l’activer pour la hiérarchie, puis configurer des groupes de limites au niveau de chaque site principal pour inclure les points de gestion à associer aux limites de ces groupes de limites.  
-   Quand les points de gestion préférés sont configurés et qu’un client organise sa propre liste de points de gestion, il place les points de gestion préférés en haut de sa liste de points de gestion affectés (qui comprend tous les points de gestion du site affecté au client).  

> [!NOTE]  
>  Quand un client est en itinérance (pour changer d’emplacement réseau, comme dans le cas d’un ordinateur portable déplacé vers un emplacement de bureau distant), il peut utiliser un point de gestion (ou un point de gestion proxy) du site local à son nouvel emplacement avant d’essayer d’utiliser un point de gestion de son site attribué (qui comprend les points de gestion préférés).  Consultez [Comprendre comment les clients recherchent des services et des ressources de site pour System Center Configuration Manager](../../../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md) pour plus d’informations.  

### <a name="overlapping-boundaries"></a>Chevauchement des limites  
 Configuration Manager prend en charge les configurations de limites se chevauchant pour l’emplacement du contenu :  

-   **Quand un client demande du contenu** et que l’emplacement réseau du client appartient à plusieurs groupes de limites, Configuration Manager envoie au client une liste de tous les points de distribution qui disposent du contenu.  
-   **Quand un client demande à un serveur d’envoyer ou de recevoir des informations sur la migration de son état** et que l’emplacement réseau du client appartient à plusieurs groupes de limites, Configuration Manager envoie au client une liste de tous les points de migration d’état associés à un groupe de limites qui inclut l’emplacement réseau actuel du client.  

Ce comportement permet au client de sélectionner le serveur le plus proche depuis lequel transférer le contenu ou les informations sur la migration de l'état.  



## <a name="example-of-using-boundary-groups"></a>Exemple d’utilisation de groupes de limites
L’exemple suivant utilise un client qui recherche du contenu sur un point de distribution. Cet exemple peut s’appliquer à d’autres rôles de système de site qui utilisent des groupes de limites. Toutefois, en ce qui concerne les points de mise à jour logicielle, n’oubliez pas qu’ils ne prennent pas en charge la configuration d’un délai en minutes pour le recours à un groupe voisin, et qu’ils utilisent toujours une période de 120 minutes.

Vous créez trois groupes de limites qui ne partagent pas de limites ni de serveurs de système de site :
-   Groupe BG_A avec les points de distribution DP_A1 et DP_A2 associés au groupe
-   Groupe BG_B avec les points de distribution DP_B1 et DP_B2 associés au groupe
-   Groupe BG_C avec les points de distribution DP_C1 et DP_C2 associés au groupe

Vous ajoutez les emplacements réseau de vos clients en tant que limites uniquement au groupe de limites BG_A, puis vous configurez des relations à partir de ce groupe de limites vers les deux autres groupes de limites :
-   Vous configurez des points de distribution pour le premier groupe *voisin* (BG_B) à utiliser après 10 minutes. Ce groupe contient les points de distribution DP_B1 et DP_B2. Les deux sont correctement connectés aux emplacements des premiers groupes de limites.
-   Vous configurez le deuxième groupe *voisin* (BG_C) à utiliser après 20 minutes. Ce groupe contient les points de distribution DP_C1 et DP_C2. Les deux se trouvent sur un réseau étendu à distance des deux autres groupes de limites.
-   Vous ajoutez également un point de distribution supplémentaire qui se trouve sur le serveur de site au groupe de limites de site par défaut du site. Il s’agit de l’emplacement source de contenu que vous préférez le moins, mais il se trouve au milieu de tous les groupes de limites.

    Exemple de groupes de limites et de durées de secours :

     ![BG_Fallback](media/BG_Fallback.png)


Avec cette configuration :
-   Le client commence la recherche de contenu dans les points de distribution de son groupe de limites *actuel* (BG_A), en passant deux minutes dans chaque point avant de passer au suivant dans le groupe. Le pool des emplacements sources de contenu valides du client inclut DP_A1 et DP_A2.
-   Si le client ne parvient pas à trouver le contenu dans son groupe de limites *actuel* après une recherche de 10 minutes, il ajoute alors les points de distribution du groupe de limites BG_B à sa recherche. Il continue ensuite à rechercher le contenu dans un point de distribution de son pool combiné de points de distribution qui inclut maintenant ceux des groupes de limites BG_A et BG_B. Le client continue de contacter chaque point de distribution pendant deux minutes avant de passer au point de distribution suivant de son pool. Le pool des emplacements sources de contenu valides du client inclut DP_A1, DP_A2, DP_B1 et DP_B2.
-   Après 10 minutes supplémentaires (20 minutes au total), si le client n’a toujours pas trouvé un point de distribution avec du contenu, il étend son pool de points de distribution disponibles pour inclure ceux du deuxième groupe *voisin*, le groupe de limites BG_C. Le client dispose désormais de 6 points de distribution pour sa recherche (DP_A1, DP_A2, DP_B1, DP_B2, DP_C1 et DP_C2) et continue de changer de point de distribution toutes les deux minutes jusqu’à ce qu’il trouve le contenu.
-   Si le client n’a pas trouvé le contenu après un total de 120 minutes, il revient en arrière pour inclure le *groupe de limites de site par défaut* dans le cadre de sa recherche continue. Le pool des points de distribution inclut désormais tous les points de distribution des trois groupes de limites configurés et le point de distribution final situé sur l’ordinateur serveur de site.  Le client continue alors sa recherche de contenu, en changeant de point de distribution toutes les deux minutes jusqu’à ce qu’il trouve le contenu.

En configurant les différents groupes voisins pour être disponibles à différents moments, vous contrôlez quand des points de distribution spécifiques sont ajoutés en tant qu’emplacement source de contenu et quand, ou si, le client utilise le secours sur le groupe de limites de site par défaut comme filet de protection pour le contenu qui n’est pas disponible à partir de tout autre emplacement.






### <a name="update-existing-boundary-groups-to-the-new-model"></a>Mettre à jour des groupes de limites existants vers le nouveau modèle
Quand vous effectuez une mise à jour vers une version antérieure à la version 1610, les configurations suivantes sont automatiquement effectuées. Elles sont destinées à vérifier que votre comportement de secours actuel reste disponible jusqu’à ce que vous configuriez de nouvelles relations et de nouveaux groupes de limites.

-   Un groupe de limites de site par défaut est créé pour chaque site principal, le nom est ***Groupe-de-limites-de-site-par-défaut&lt;code_de_site>.***
  - Les points de distribution pour lesquels la case *Autoriser l’emplacement source de secours pour le contenu* est cochée et qui sont associés à des points de migration d’état sur les sites principaux sont ajoutés au groupe de limites *Groupe-de-limites-de-site-par-défaut&lt;code_de_site>* de ce site.
  - À partir de la version 1702, les points de mise à jour logicielle sont ajoutés à chaque *Default-Site-Boundary-Group&lt;sitecode>* de site.
-   Une copie de chaque groupe de limites existant qui inclut un serveur de site configuré avec une connexion lente est créée. Le nom du nouveau groupe est ***&lt;nom du groupe de limites d’origine>-&lt;ID du groupe de limites d’origine>*** :  
    -   Les systèmes de site qui disposent d’une connexion rapide restent dans le groupe de limites d’origine.
    -   Une copie des systèmes de site (points de distribution et points de gestion) qui ont une connexion lente est ajoutée à la copie du groupe de limites. Les systèmes de site d’origine configurés comme lents restent dans leurs groupes de limites d’origine pour la compatibilité descendante, mais ne sont pas utilisés à partir de ces groupes de limites.
    - Cette copie du groupe de limites n’a pas de limites associées. Toutefois, un lien de secours est créé entre le groupe d’origine et la nouvelle copie du groupe de limites dont la durée de secours a la valeur zéro.  


- **Propre aux sites secondaires :**
  - Un groupe de limites est créé si un site secondaire a au moins un point de distribution pour lequel la case *Autoriser l’emplacement source de secours pour le contenu* est cochée ou un point de migration d’état. Le nom du groupe de limites est ***voisin-du-site-secondaire--Tmp&lt;code_de_site>.***
  - Tous les points de distribution pour lesquels la case *Autoriser l’emplacement source de secours pour le contenu* est cochée et qui ont des points de migration d’état sont ajoutés au groupe de limites du site secondaire nouvellement créé.
  - Un lien de secours est créé entre le groupe de limites d’origine et le nouveau groupe de limites voisin, et la durée de secours a la valeur zéro.


 Le tableau suivant identifie le nouveau comportement de secours que vous pouvez attendre de la combinaison des configurations des points de distribution et des paramètres de déploiement d’origine :

Configuration du déploiement d’origine pour « Ne pas exécuter le programme » sur un réseau lent  |Configuration du point de distribution d’origine pour « Allow client to use a fallback source location for content » (Autoriser le client à utiliser un emplacement source de secours pour le contenu)  |Nouveau comportement de secours  
---------|---------|---------
Sélectionnée     |  Sélectionnée    |  **Pas de secours** : utilisez uniquement les points de distribution dans le groupe de limites actuel       
Sélectionnée     |  Non sélectionnée|  **Pas de secours** : utilisez uniquement les points de distribution dans le groupe de limites actuel       
Non sélectionnée |  Non sélectionnée|  **Secours sur le voisin** : utilisez les points de distribution dans le groupe de limites actuel, puis ajoutez les points de distribution du groupe de limites voisin. Sauf si un lien explicite vers le groupe de limites de site par défaut est configuré, les clients ne vont pas utiliser ce groupe en secours.    
Non sélectionnée | Sélectionnée     |   **Secours normal** : utilisez les points de distribution dans le groupe de limites actuel, puis ceux des groupes de limites de site par défaut et voisin

 Toutes les autres configurations de déploiement entraînent un comportement de **secours normal**.  




## <a name="changes-from-prior-versions-for-ui-and-behavior-for-content-locations"></a>Modifications des versions antérieures de l’interface utilisateur et comportement des emplacements de contenu
Voici les principales modifications apportées aux groupes de limites et à la manière dont les clients recherchent le contenu. Ces modifications ont été introduites avec la version 1610. La plupart de ces modifications et concepts fonctionnent ensemble.


-   **Les configurations rapides ou lentes sont supprimées :** vous ne configurez plus des points de distribution individuels pour être rapides ou lents.  Au lieu de cela, chaque système de site associé à un groupe de limites est traité de la même façon. En raison de cette modification, l’onglet **References** (Références) des propriétés du groupe de limites ne prend plus en charge la configuration rapide ou lente.
-   **Nouveau groupe de limites par défaut sur chaque site :** chaque site principal possède un nouveau groupe de limites par défaut nommé ***Groupe-limites-site-défaut&lt;code_site>***.  Quand un client n’est pas à un emplacement réseau qui est affecté à un groupe de limites, ce client utilise les systèmes de site associés au groupe par défaut à partir de son site affecté. Envisagez d’utiliser ce groupe de limites en remplacement de la notion d’emplacement de secours pour le contenu.      
 -  **Allow fallback source locations for content** (Autoriser les emplacements sources de secours pour le contenu) est supprimé : vous ne configurez plus explicitement un point de distribution de secours à utiliser, et les options associées sont supprimées de l’interface utilisateur.

    En outre, le résultat de la définition du paramètre **Autoriser les clients à utiliser un emplacement source de secours pour le contenu** sur un type de déploiement pour les applications a changé. Ce paramètre sur un type de déploiement permet maintenant à un client d’utiliser le groupe de limites de site par défaut comme emplacement source de contenu.

 -  **Relations de groupes de limites :** chaque groupe de limites peut être lié à un ou plusieurs groupes de limites supplémentaires. Ces liens forment des relations qui sont configurées sous le nouvel onglet des propriétés du groupe de limites nommé **Relations** :
    -   Chaque groupe de limites auquel un client est directement associé est appelé groupe de limites **actuel**.  
    -   Tout groupe de limites qu’un client peut utiliser en raison d’une association entre le groupe de limites *actuel* de ce client et un autre groupe est appelé groupe de limites **voisin**.
    -  Vous ajoutez des groupes de limites qui peuvent être utilisés comme groupe de limites *voisin* sous l’onglet **Relations**. Vous pouvez également configurer une durée en minutes qui détermine quand un client qui ne parvient pas à trouver le contenu à partir d’un point de distribution dans le groupe *actuel* doit commencer à effectuer des recherches dans les emplacements de contenu de ces groupes de limites *voisins*.

        Quand vous ajoutez ou modifiez la configuration d’un groupe de limites, vous avez la possibilité de bloquer le secours sur ce groupe de limites spécifique à partir du groupe actuel que vous configurez.

    Pour utiliser la nouvelle configuration, vous définissez des associations explicites (liens) entre un groupe de limites et un autre, et configurez tous les points de distribution de ce groupe associé avec la même durée en minutes. La durée que vous configurez détermine quand un client qui ne parvient pas à trouver une source de contenu dans son groupe de limites *actuel* peut commencer à rechercher des sources de contenu dans ce groupe de limites voisin.

    En plus des groupes de limites que vous configurez explicitement, chaque groupe de limites a un lien implicite vers le groupe de limites de site par défaut. Ce lien devient actif après 120 minutes, moment auquel le groupe de limites de site par défaut devient un groupe de limites voisin qui permet aux clients d’utiliser les points de distribution associés à ce groupe de limites comme emplacements sources de contenu.

    Ce comportement remplace ce qui était précédemment désigné sous le nom de secours pour le contenu.  Vous pouvez remplacer ce comportement par défaut de 120 minutes en associant explicitement le groupe de limites de site par défaut à un groupe *actuel* et en définissant une durée spécifique en minutes ou en bloquant totalement le secours pour empêcher son utilisation.


-   **Les clients tentent d’obtenir le contenu à partir de chaque point de distribution pendant 2 minutes au maximum :** quand un client recherche un emplacement source de contenu, il tente d’accéder à chaque point de distribution pendant 2 minutes avant d’essayer ensuite un autre point de distribution. Il s’agit d’un changement par rapport aux versions précédentes où les clients tentaient de se connecter à un point de distribution pendant 2 heures au maximum.

    - Le premier point de distribution qu’un client tente d’utiliser est sélectionné au hasard dans le pool des points de distribution disponibles du groupe (ou des groupes) de limites *actuel(s)* du client.

    - Après deux minutes, si le client n’a pas trouvé le contenu, il bascule vers un nouveau point de distribution et tente d’obtenir le contenu de ce serveur. Ce processus se répète toutes les deux minutes jusqu’à ce que le client trouve le contenu ou atteigne le dernier serveur dans son pool.

    - Si un client ne trouve pas d’emplacement source de contenu valide dans son pool *actif* avant la fin du délai de secours vers un groupe de limites *voisin*, il ajoute alors les points de distribution de ce groupe *voisin* à la fin de sa liste actuelle, puis effectue des recherches dans le groupe étendu d’emplacements sources qui inclut les points de distribution des deux groupes de limites.

        > [!TIP]  
        > Quand vous créez un lien explicite entre le groupe de limites actuel et le groupe de limites de site par défaut, puis définissez une durée de secours inférieure à celle d’un lien vers un groupe de limites voisin, les clients commencent à effectuer des recherches dans les emplacements sources du groupe de limites de site par défaut avant d’inclure le groupe voisin.

    - Quand le client ne parvient pas à obtenir le contenu du dernier serveur dans le pool, il recommence le processus.


## <a name="procedures-for-boundary-groups"></a>Procédures pour les groupes de limites
Les procédures suivantes s’appliquent à la version 1610 ou ultérieure. Si vous utilisez une version antérieure à la version 1610, consultez les procédures de la section [Groupes de limites pour les versions 1511, 1602 et 1606 de System Center Configuration Manager](/sccm/core/servers/deploy/configure/boundary-groups-for-1511-1602-and-1606).


### <a name="to-create-a-boundary-group"></a>Pour créer un groupe de limites  
1.  Dans la console Configuration Manager, cliquez sur **Administration** > **Configuration de la hiérarchie** >  **Groupes de limites**.  

2.  Dans l'onglet **Accueil** , dans le groupe **Créer** , cliquez sur **Créer un groupe limite**.  

3.  Dans la boîte de dialogue **Créer un groupe limite** , sélectionnez l'onglet **Général** et spécifiez un **Nom** pour ce groupe de limites.  

4.  Cliquez sur **OK** pour enregistrer le nouveau groupe de limites.  


### <a name="to-configure-a-boundary-group"></a>Pour configurer un groupe de limites  
 1.  Dans la console Configuration Manager, cliquez sur **Administration** > **Configuration de la hiérarchie** >  **Groupes de limites**.  

 2.  Sélectionnez le groupe de limites à modifier.  

 3.  Dans l'onglet **Accueil** , dans le groupe **Propriétés** , cliquez sur **Propriétés**.  

 4.  Dans la boîte de dialogue **Propriétés** du groupe de limites, sélectionnez l'onglet **Général** pour modifier les limites membres de ce groupe de limites :  

     -   Pour ajouter des limites, cliquez sur **Ajouter**, cochez la case d'une ou plusieurs limites et cliquez sur **OK**.  

     -   Pour supprimer des limites, sélectionnez la limite à supprimer, puis cliquez sur **Supprimer**.  

 5.  Sélectionnez l'onglet **Références** pour modifier l'attribution de site et la configuration de serveur de système de site associée :  

     -   Pour autoriser ce groupe de limites à être utilisé par les clients pour l'attribution de site, cochez la case **Utiliser ce groupe limite pour l'attribution de site**, puis sélectionnez un site dans la liste déroulante **Site attribué** .  

     -   Pour configurer les serveurs de système de site associés à ce groupe de limites  

     1.  Cliquez sur **Ajouter**, puis cochez la case d'un ou plusieurs serveurs. Les serveurs sont ajoutés en tant que serveurs de système de site associés à ce groupe de limites. Seuls les serveurs sur lesquels un rôle de système de site pris en charge est installé sont disponibles.  

         > [!NOTE]  
         >  Vous pouvez sélectionner n'importe quelle combinaison de systèmes de site disponibles à partir de n'importe quel site dans la hiérarchie. Les systèmes de site sélectionnés figurent sous l'onglet **Systèmes de site** des propriétés de chaque limite appartenant à ce groupe de limites.  

     2.  Pour supprimer un serveur de ce groupe de limites, sélectionnez le serveur, puis cliquez sur **Supprimer**.  

         > [!NOTE]  
         >  Pour ne plus utiliser ce groupe de limites pour l'association des systèmes de site, vous devez supprimer tous les serveurs répertoriés en tant que serveurs de système de site associés.  

 6.  Sélectionnez l’onglet **Relations** pour configurer le comportement de secours :  

     - Cliquez sur **Ajouter**, puis sélectionnez le groupe de limites à configurer.

     - Définissez une durée de secours pour les points de distribution. Après cette période de temps, les clients dans le groupe de limites pour lequel vous configurez des relations peuvent commencer à rechercher du contenu à partir des points de distribution du groupe de limites que vous ajoutez.

     - Pour ne pas avoir recours à un groupe de limites spécifique, notamment le *groupe de limites du site par défaut* qui est configuré par défaut, sélectionnez le groupe de limites et cochez la case **Ne jamais activer le secours**.   

 7.  Cliquez sur **OK** pour fermer les propriétés du groupe de limites et enregistrer la configuration.  

#### <a name="to-associate-a-site-systme-server-with-a-boundary-group"></a>Pour associer un serveur de système de site à un groupe de limites  
 1.  Dans la console Configuration Manager, cliquez sur **Administration** > **Configuration de la hiérarchie** >  **Groupes de limites**.  

 2.  Sélectionnez le groupe de limites à modifier.  

 3.  Dans l'onglet **Accueil** , dans le groupe **Propriétés** , cliquez sur **Propriétés**.  

 4.  Dans la boîte de dialogue **Propriétés** du groupe de limites, sélectionnez l'onglet **Références** .  

 5.  Sous **Sélectionner des serveurs de système de site**, cliquez sur **Ajouter**, cochez la case des serveurs de système de site que vous souhaitez associer à ce groupe de limites, puis cliquez sur **OK**.  

 6.  Cliquez sur **OK** pour fermer la boîte de dialogue et enregistrer la configuration du groupe de limites.  


#### <a name="to-configure-a-fallback-site-for-automatic-site-assignment"></a>Pour configurer un site de secours pour l'attribution automatique de site  

  1.  Dans la console Configuration Manager, cliquez sur **Administration** > **Configuration de site** >  **Sites**.  

  2.  Dans l'onglet **Accueil** , dans le groupe **Sites** , cliquez sur **Paramètres de hiérarchie**.  

  3.  Dans l'onglet **Général** , cochez la case **Utiliser un site de secours**, puis sélectionnez un site dans la liste déroulante **Site de secours** .  

  4.  Cliquez sur **OK** pour enregistrer la configuration.  

#### <a name="to-enable-use-of-preferred-management-points"></a>Pour activer l’utilisation des points de gestion préférés  

 1.  Dans la console Configuration Manager, cliquez sur **Administration** > **Configuration de site** > **Sites** puis, sous l’onglet **Accueil**, sélectionnez **Paramètres de hiérarchie**.  

 2.  Sous l’onglet **Général** des paramètres de hiérarchie, sélectionnez **Les clients préfèrent utiliser les points de gestion spécifiés dans les groupes de limites**.  

 3.  Cliquez sur **OK** pour fermer la boîte de dialogue et enregistrer la configuration.  

