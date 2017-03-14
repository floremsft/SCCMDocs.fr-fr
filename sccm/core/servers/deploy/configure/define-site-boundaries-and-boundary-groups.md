---
title: "Définir des limites de site | Microsoft Docs"
description: "Découvrez comment définir les emplacements réseau sur votre intranet pouvant contenir des appareils que vous souhaitez gérer."
ms.custom: na
ms.date: 2/27/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 54aa20d5-791e-4416-9db4-5aaea472c0b7
caps.latest.revision: 10
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 6d83570e3210709c5ef39b50d9c483f99017664b
ms.openlocfilehash: 13b79c920a64698660ee1c041b9166646789634c
ms.lasthandoff: 02/28/2017


---
# <a name="define-site-boundaries-and-boundary-groups-for-system-center-configuration-manager"></a>Définir des limites de site et les groupes de limites pour System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Les limites pour System Center Configuration Manager définissent les emplacements réseau sur votre intranet pouvant contenir des appareils que vous souhaitez gérer. Les groupes de limites sont des groupes logiques de limites que vous configurez. Les limites et groupes de limites sont configurés au niveau de la hiérarchie, pas pour des sites individuels.  

 Une hiérarchie peut inclure n’importe quel nombre de groupes de limites, et chaque groupe de limites peut contenir n’importe quelle combinaison des types de limites suivants :  

-   Sous-réseau IP  
-   Nom de site Active Directory  
-   Préfixe IPv6  
-   Plage d'adresses IP  

Les clients intranet évaluent leur emplacement réseau actuel, puis utilisent ces informations pour identifier les groupes de limites auxquels ils appartiennent.  

 Les clients utilisent des groupes de limites pour :  
-   **Trouver un site attribué** : les groupes de limites permettent aux clients de trouver un site principal pour l’attribution du client (attribution automatique de site).  
-   **Trouver des rôles de système de site spécifiques disponibles**  : quand vous associez un groupe de limites à certains rôles de système de site, le groupe de limites fournit aux clients la liste des systèmes de site à utiliser pour l’emplacement du contenu et en tant que points de gestion préférés.  

Les clients Internet ou les clients configurés en tant que clients Internet uniquement n’utilisent pas les informations sur les limites. Ces clients ne peuvent pas utiliser l’attribution automatique de site. Ils peuvent toujours télécharger le contenu de n’importe quel point de distribution sur leur site attribué quand le point de distribution est configuré pour autoriser les connexions clientes depuis Internet.  


##  <a name="BKMK_Boundaries"></a> Limites  
 Vous pouvez créer manuellement des limites individuelles. En outre, vous pouvez configurer la [découverte de forêts Active Directory](../../../../core/servers/deploy/configure/about-discovery-methods.md#bkmk_aboutForest) afin de détecter automatiquement et de créer des limites pour chaque sous-réseau IP et site Active Directory ainsi découverts.  

-   Chaque limite représente un emplacement réseau et est disponible de n’importe quel site de la hiérarchie.  
-   Configuration Manager ne prend pas en charge l’entrée directe d’un sur-réseau en tant que limite. À la place, utilisez le type de limite de la plage d'adresses IP.  
-   Lorsque la fonctionnalité de découverte de forêts Active Directory identifie un sur-réseau attribué à un site Active Directory, Configuration Manager convertit le sur-réseau en limite de plage d'adresses IP.  
-   La limite configurée pour un client correspond au site Active Directory ou à l’adresse IP de réseau que le client identifie. (Il n’est pas rare qu’un client utilise une adresse IP dont l’administrateur Configuration Manager n’a pas connaissance. Si l’emplacement réseau d’un client est incertain, demandez au client qu’il signale son emplacement en exécutant la commande **IPCONFIG** sur le client.)  

Quand vous créez une limite, elle reçoit automatiquement un nom basé sur son type et son étendue. Ce nom ne peut pas être modifié. Au lieu de cela, lorsque vous configurez la limite, spécifiez une description permettant de l’identifier dans la console Configuration Manager.  

 Après avoir créé une limite, vous pouvez modifier ses propriétés pour effectuer les opérations suivantes :  
-   Ajouter la limite à un ou plusieurs groupes de limites.  
-   Changer le type ou la portée de la limite.  
-   Afficher l’onglet **Systèmes de site** des limites pour savoir quels serveurs de système de site (points de distribution, points de migration d’état et points de gestion) sont associés à la limite.  

### <a name="to-create-a-boundary"></a>Pour créer une limite  

1.  Dans la console Configuration Manager, cliquez sur **Administration** > **Configuration de la hiérarchie** > **Limites**  

2.  Dans l'onglet **Accueil** , dans le groupe **Créer** , cliquez sur **Créer Boundary.**.  

3.  Dans l'onglet **Général** de la boîte de dialogue Créer une limite, vous pouvez spécifier une **Description** pour identifier une limite par un nom convivial ou une référence.  

4.  Sélectionnez un **Type** pour cette limite :  

    -   Si vous sélectionnez **Sous-réseau IP**, vous devez spécifier un **ID de sous-réseau** pour cette limite.  
        > [!TIP]  
        >  Vous pouvez spécifier le **Réseau** et le **Masque de sous-réseau** pour que l' **ID de sous-réseau** soit automatiquement spécifié. Lorsque vous enregistrez la limite, seule la valeur d'ID de sous-réseau est enregistrée.  

    -   Si vous sélectionnez **Site Active Directory**, vous devez spécifier ou **Parcourir** vers un site Active Directory dans la forêt locale du serveur de site.  

        > [!IMPORTANT]  
        >  Lorsque vous spécifiez un site Active Directory pour une limite, la limite inclut chaque sous-réseau IP membre de ce site Active Directory. Si la configuration du site Active Directory est modifiée dans Active Directory, les emplacements réseau inclus dans cette limite sont également modifiés.  

    -   Si vous sélectionnez **Préfixe IPv6**, vous devez spécifier un **Préfixe** au format de préfixe IPv6.  

    -   Si vous sélectionnez **Plage d'adresses IP**, vous devez spécifier une **Adresse IP de début** et une **Adresse IP de fin** qui inclut la partie d'un sous-réseau IP ou inclut plusieurs sous-réseaux IP.    

5.  Cliquez sur **OK** pour enregistrer la nouvelle limite.  

### <a name="to-configure-a-boundary"></a>Pour configurer une limite  

1.  Dans la console Configuration Manager, cliquez sur **Administration** > **Configuration de la hiérarchie** > **Limites**  

2.  Sélectionnez la limite à modifier.  

3.  Dans l'onglet **Accueil** , dans le groupe **Propriétés** , cliquez sur **Propriétés**.  

4.  Dans la boîte de dialogue **Propriétés** de la limite, sélectionnez l'onglet **Général** pour modifier la **Description** ou le **Type** de la limite. Vous pouvez également modifier l'étendue d'une limite en modifiant les emplacements réseau pour la limite. Par exemple, pour une limite de site Active Directory, vous pouvez spécifier un nouveau nom de site Active Directory.  

5.  Sélectionnez l'onglet **Systèmes de site** pour afficher les systèmes de site associés à cette limite. Vous ne pouvez pas modifier cette configuration à partir des propriétés d'une limite.  

    > [!TIP]  
    >  Pour qu'un serveur de système de site soit référencé comme système de site pour une limite, il faut que le serveur de système de site soit associé en tant que serveur de système de site pour au moins un groupe de limites comportant cette limite. Vous pouvez configurer cela sous l'onglet **Références** d'un groupe de limites.  

6.  Sélectionnez l'onglet **Groupes de limites** pour modifier l'appartenance au groupe de limites pour cette limite :  

    -   Pour ajouter cette limite à un ou plusieurs groupes de limites, cliquez sur **Ajouter**, cochez la case d'un ou plusieurs groupes de limites, puis cliquez sur **OK**.  

    -   Pour supprimer cette limite d'un groupe de limites, sélectionnez le groupe de limites, puis cliquez sur **Supprimer**.  

7.  Cliquez sur **OK** pour fermer les propriétés de la limite et enregistrer la configuration.  

##  <a name="BKMK_BoundaryGroups"></a> Boundary groups
> [!IMPORTANT]  
>  **Les informations contenues dans cette section sur les groupes de limites et ses sections enfants s’appliquent à la version 1610 ou ultérieure.** Ce contenu a été modifié pour refléter les modifications de conception appliquées aux groupes de limites dans cette version de mise à jour.
>
> **Si vous utilisez les versions 1511, 1602 ou 1606**, consultez [Groupes de limites pour les versions 1511, 1602 et 1606 de System Center Configuration Manager](/sccm/core/servers/deploy/configure/boundary-groups-for-1511-1602-and-1606) pour plus d’informations sur l’utilisation et la configuration des groupes de limites avec ces versions de produit.

La version 1610 apporte des modifications importantes aux groupes de limites et à leur fonctionnement avec les points de distribution. Ces modifications permettent de simplifier la conception de votre infrastructure de contenu tout en vous donnant davantage de contrôle sur quand et comment les clients doivent avoir recours à d’autres points de distribution comme emplacements sources de contenu. Cela inclut à la fois les points de distribution cloud et locaux.

**À propos des groupes de limites :**  
 Créer des groupes de limites vous permet de regrouper de façon logique des emplacements réseau (limites) pour faciliter la gestion de votre infrastructure. Vous devez attribuer des limites à des groupes de limites avant de pouvoir utiliser le groupe de limites. Les clients utilisent la configuration du groupe de limites pour les opérations suivantes :  

-   Attribution automatique du site  
-   Emplacement du contenu  
-   Points de gestion préférés (Si vous utilisez des points de gestion préférés, vous devez activer cette option pour la hiérarchie et non pas à partir de la configuration du groupe de limites. Consultez la procédure suivante [Pour activer l’utilisation des points de gestion préférés](#to-enable-use-of-preferred-management-points) dans cette rubrique.)  

Quand vous configurez un groupe de limites, vous ajoutez une ou plusieurs limites au groupe de limites, puis vous configurez des paramètres supplémentaires utilisables par les clients situés sur ces limites.  

Vous trouverez des [procédures de gestion des groupes de limites](#procedures-for-boundary-groups) plus loin dans cette rubrique.


###  <a name="BKMK_BoundarySiteAssignment"></a> À propos de l’attribution de site  
 Vous pouvez configurer chaque groupe de limites avec un site attribué pour les clients.  

-   Quand un client récemment installé utilise l’attribution automatique de site, il rejoint le site attribué d’un groupe de limites qui englobe l’emplacement réseau actuel du client.  
-   Après avoir été attribué à un site, un client ne modifie pas son attribution de site quand il change d’emplacement réseau. Par exemple, si le client se déplace vers un nouvel emplacement réseau représenté par une limite dans un groupe de limites disposant d’une attribution de site différente, le site attribué au client n’est pas modifié.  
-   Lorsque la découverte de systèmes Active Directory détecte une nouvelle ressource, les informations sur le réseau de la ressource découverte sont évaluées en fonction des limites dans les groupes de limites. Ce processus associe la nouvelle ressource à un site attribué pour une utilisation par la méthode d'installation poussée du client.  
-   Quand une limite est membre de plusieurs groupes de limites auxquels différents sites sont attribués, les clients sélectionnent l’un des sites aléatoirement.  
-   Les modifications apportées à un site attribué à des groupes de limites s’appliquent uniquement aux nouvelles actions d’attribution de site. Les clients déjà attribués à un site ne ré-évaluent pas leur attribution à un site en fonction des changements apportés à la configuration du groupe de limites (ou à leur emplacement réseau).  

Pour plus d’informations sur l’attribution de site client, consultez [Utilisation de l’attribution automatique de site pour les ordinateurs](../../../../core/clients/deploy/assign-clients-to-a-site.md#BKMK_AutomaticAssignment) dans [Guide pratique pour affecter des clients à un site dans System Center Configuration Manager](../../../../core/clients/deploy/assign-clients-to-a-site.md).  

###  <a name="BKMK_BoundaryContentLocation"></a> À propos de l’emplacement du contenu  
Quand vous configurez des groupes de limites, vous associez des limites (emplacements réseau) et des rôles de système de site, comme les points de distribution, au groupe de limites. Cela permet de lier les clients aux serveurs de système de site tels que les points de distribution qui se trouvent près des clients sur le réseau.

Vous pouvez attribuer la même limite à plusieurs groupes de limites, et les serveurs de système de site, comme les points de distribution, peuvent être associés à plusieurs groupes de limites. Cela les rend disponibles pour un grand nombre d’emplacements réseau.

-   **Lors de la distribution de logiciels**, les clients demandent un emplacement pour le contenu de déploiement. Configuration Manager envoie au client une liste de points de distribution associés à chaque groupe de limites qui inclut l’emplacement réseau actuel du client.  
-   **Durant le déploiement de système d’exploitation**, les clients demandent un emplacement où envoyer ou recevoir des informations sur la migration de leur état. Configuration Manager envoie au client une liste de points de migration d’état associés à chaque groupe de limites qui inclut l’emplacement réseau actuel du client.  

Vous définissez les relations entre groupes de limites pour configurer le comportement de secours concernant les emplacements sources de contenu. Nouveau dans la version 1610, vous configurez des relations sous le nouvel onglet **Relations** des propriétés du groupe de limites. Cet onglet évite d’avoir à configurer des systèmes de site lents ou rapides, ou à configurer un groupe de limites pour autoriser un emplacement source de secours pour le contenu.

Quand vous configurez un groupe de limites, qui est le groupe de limites **actuel**, vous ajoutez d’autres groupes de limites pour créer un lien à sens unique du groupe de limites actuel vers chaque groupe de limites que vous ajoutez. Les groupes de limites que vous ajoutez sont appelés groupes de limites **voisins**. Ensuite, pour chaque lien créé vers un voisin, vous pouvez configurer des points de distribution avec une durée de secours en minutes. Cette durée permet de déterminer le délai après lequel les clients dans le groupe de limites actuel peuvent commencer à utiliser les points de distribution dans le groupe de limites voisin s’ils ne peuvent pas trouver un emplacement source de contenu valide dans leur groupe de limites actuel.

Quand un client ne peut pas trouver le contenu et commence à effectuer des recherches dans des emplacements de groupes de limites voisins, il augmente le pool des points de distribution disponibles pour ce client de manière contrôlée.

-    Un groupe de limites peut avoir plusieurs relations. Cela vous permet de configurer le secours sur différents voisins pour qu’il intervienne après différentes périodes de temps.
-     Les clients vont uniquement utiliser en secours un groupe de limites qui est un voisin direct de leur groupe de limites actuel.
-    Quand un client est membre de plusieurs groupes de limites, le groupe de limites actuel est défini en tant qu’union de tous les groupes de limites de ce client. Ce client peut ensuite utiliser en secours un voisin de n’importe lequel de ces groupes de limites d’origine.

Outre les liens que vous définissez, il existe un lien implicite qui est créé automatiquement entre les groupes de limites que vous créez et le groupe de limites par défaut qui est automatiquement créé pour chaque site. Ce lien automatique :
-     Est utilisé par les clients qui ne sont pas dans une limite associée à un groupe de limites de votre hiérarchie. Les clients utilisent automatiquement le groupe de limites par défaut de leur site attribué pour identifier les emplacements sources de contenu valides.
-     est une option de secours par défaut entre le groupe de limites actuel et le groupe de limites de site par défaut qui est utilisé après 120 minutes.

**Quand le contenu n’est pas disponible dans un groupe de limites actuel :**  
Lorsque le contenu demandé par un client n’est pas disponible à partir d’une source de contenu valide dans un groupe de limites actuel, le client doit attendre que la période de secours pour un groupe de limites voisin ou le groupe de limites par défaut du site soit atteinte avant de pouvoir rechercher d’autres sources de contenu.

Si le contenu est distribué à la demande, mais qu’il n’est pas disponible quand il est demandé par un client, le processus de transfert du contenu commence vers un point de distribution dans la limite actuelle.  



**Exemple d’utilisation du nouveau modèle :**   
Vous créez trois groupes de limites qui ne partagent pas de limites ni de serveurs de système de site :
-    Groupe BG_A avec les points de distribution DP_A1 et DP_A2 associés au groupe
-    Groupe BG_B avec les points de distribution DP_B1 et DP_B2 associés au groupe
-    Groupe BG_C avec les points de distribution DP_C1 et DP_C2 associés au groupe

Vous ajoutez les emplacements réseau de vos clients en tant que limites uniquement au groupe de limites BG_A, puis vous configurez des relations à partir de ce groupe de limites vers les deux autres groupes de limites :
-    Vous configurez des points de distribution pour le premier groupe *voisin* (BG_B) à utiliser après 10 minutes. Ce groupe contient les points de distribution DP_B1 et DP_B2. Les deux sont correctement connectés aux emplacements des premiers groupes de limites.
-    Vous configurez le deuxième groupe *voisin* (BG_C) à utiliser après 20 minutes. Ce groupe contient les points de distribution DP_C1 et DP_C2. Les deux se trouvent sur un réseau étendu à distance des deux autres groupes de limites.
-    Vous ajoutez également un point de distribution supplémentaire qui se trouve sur le serveur de site au groupe de limites de site par défaut du site. Il s’agit de l’emplacement source de contenu que vous préférez le moins, mais il se trouve au milieu de tous les groupes de limites.

    Exemple de groupes de limites et de durées de secours :

     ![BG_Fallback](media/BG_Fallback.png)


Avec cette configuration :
-    Le client commence la recherche de contenu dans les points de distribution de son groupe de limites *actuel* (BG_A), en passant deux minutes dans chaque point avant de passer au suivant dans le groupe. Le pool des emplacements sources de contenu valides du client inclut DP_A1 et DP_A2.
-    Si le client ne parvient pas à trouver le contenu dans son groupe de limites *actuel* après une recherche de 10 minutes, il ajoute alors les points de distribution du groupe de limites BG_B à sa recherche. Il continue ensuite à rechercher le contenu dans un point de distribution de son pool combiné de points de distribution qui inclut maintenant ceux des groupes de limites BG_A et BG_B. Le client continue de contacter chaque point de distribution pendant deux minutes avant de passer au point de distribution suivant de son pool. Le pool des emplacements sources de contenu valides du client inclut DP_A1, DP_A2, DP_B1 et DP_B2.
-    Après 10 minutes supplémentaires (20 minutes au total), si le client n’a toujours pas trouvé un point de distribution avec du contenu, il étend son pool de points de distribution disponibles pour inclure ceux du deuxième groupe *voisin*, le groupe de limites BG_C. Le client dispose désormais de 6 points de distribution pour sa recherche (DP_A1, DP_A2, DP_B1, DP_B2, DP_C1 et DP_C2) et continue de changer de point de distribution toutes les deux minutes jusqu’à ce qu’il trouve le contenu.
-    Si le client n’a pas trouvé le contenu après un total de 120 minutes, il revient en arrière pour inclure le *groupe de limites de site par défaut* dans le cadre de sa recherche continue. Le pool des points de distribution inclut désormais tous les points de distribution des trois groupes de limites configurés et le point de distribution final situé sur l’ordinateur serveur de site.  Le client continue alors sa recherche de contenu, en changeant de point de distribution toutes les deux minutes jusqu’à ce qu’il trouve le contenu.

En configurant les différents groupes voisins pour être disponibles à différents moments, vous contrôlez quand des points de distribution spécifiques sont ajoutés en tant qu’emplacement source de contenu et quand, ou si, le client utilise le secours sur le groupe de limites de site par défaut comme filet de protection pour le contenu qui n’est pas disponible à partir de tout autre emplacement.




### <a name="update-existing-boundary-groups-to-the-new-model"></a>Mettre à jour des groupes de limites existants vers le nouveau modèle
Quand vous effectuez une mise à jour vers la version 1610, les configurations suivantes sont automatiquement effectuées. Elles sont destinées à vérifier que votre comportement de secours actuel reste disponible jusqu’à ce que vous configuriez de nouvelles relations et de nouveaux groupes de limites.
-    Un groupe de limites de site par défaut est créé pour chaque site principal, le nom est ***Groupe-de-limites-de-site-par-défaut&lt;code_de_site>.***
-    Les points de distribution pour lesquels la case *Autoriser l’emplacement source de secours pour le contenu* est cochée et qui sont associés à des points de migration d’état sur les sites principaux sont ajoutés au groupe de limites *Groupe-de-limites-de-site-par-défaut&lt;code_de_site>* de ce site.
-    Une copie de chaque groupe de limites existant qui inclut un serveur de site configuré avec une connexion lente est créée. Le nom du nouveau groupe est ***&lt;nom du groupe de limites d’origine>-&lt;ID du groupe de limites d’origine>*** :  
    -    Les systèmes de site qui disposent d’une connexion rapide restent dans le groupe de limites d’origine.
    -    Une copie des systèmes de site (points de distribution, points de gestion et points de migration d’état) qui ont une connexion lente est ajoutée à la copie du groupe de limites. Les systèmes de site d’origine configurés comme lents restent dans leurs groupes de limites d’origine pour la compatibilité descendante, mais ne sont pas utilisés à partir de ces groupes de limites.
    -     Cette copie du groupe de limites n’a pas de limites associées. Toutefois, un lien de secours est créé entre le groupe d’origine et la nouvelle copie du groupe de limites dont la durée de secours a la valeur zéro.  


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
Non sélectionnée | Sélectionnée        |   **Secours normal** : utilisez les points de distribution dans le groupe de limites actuel, puis ceux des groupes de limites de site par défaut et voisin

 Toutes les autres configurations de déploiement entraînent un comportement de **secours normal**.  



### <a name="changes-from-prior-versions-for-ui-and-behavior-for-content-locations"></a>Modifications des versions antérieures de l’interface utilisateur et comportement des emplacements de contenu
Voici les principales modifications apportées dans la version 1610 aux groupes de limites et à la façon dont les clients recherchent le contenu. La plupart de ces modifications et concepts fonctionnent ensemble.


-    **Les configurations rapides ou lentes sont supprimées :** vous ne configurez plus des points de distribution individuels pour être rapides ou lents.  Au lieu de cela, chaque système de site associé à un groupe de limites est traité de la même façon. En raison de cette modification, l’onglet **References** (Références) des propriétés du groupe de limites ne prend plus en charge la configuration rapide ou lente.
-     **Nouveau groupe de limites par défaut sur chaque site :** chaque site principal possède un nouveau groupe de limites par défaut nommé ***Groupe-limites-site-défaut&lt;code_site>***.  Quand un client n’est pas à un emplacement réseau qui est affecté à un groupe de limites, ce client utilise les systèmes de site associés au groupe par défaut à partir de son site affecté. Envisagez d’utiliser ce groupe de limites en remplacement de la notion d’emplacement de secours pour le contenu.      
 -    **Allow fallback source locations for content** (Autoriser les emplacements sources de secours pour le contenu) est supprimé : vous ne configurez plus explicitement un point de distribution de secours à utiliser, et les options associées sont supprimées de l’interface utilisateur.

    En outre, le résultat de la définition du paramètre **Autoriser les clients à utiliser un emplacement source de secours pour le contenu** sur un type de déploiement pour les applications a changé. Ce paramètre sur un type de déploiement permet maintenant à un client d’utiliser le groupe de limites de site par défaut comme emplacement source de contenu.

 -    **Relations de groupes de limites :** chaque groupe de limites peut être lié à un ou plusieurs groupes de limites supplémentaires. Ces liens forment des relations qui sont configurées sous le nouvel onglet des propriétés du groupe de limites nommé **Relations** :
     -    Chaque groupe de limites auquel un client est directement associé est appelé groupe de limites **actuel**.  
    -     Tout groupe de limites qu’un client peut utiliser en raison d’une association entre le groupe de limites *actuel* de ce client et un autre groupe est appelé groupe de limites **voisin**.
    -  Vous ajoutez des groupes de limites qui peuvent être utilisés comme groupe de limites *voisin* sous l’onglet **Relations**. Vous pouvez également configurer une durée en minutes qui détermine quand un client qui ne parvient pas à trouver le contenu à partir d’un point de distribution dans le groupe *actuel* doit commencer à effectuer des recherches dans les emplacements de contenu de ces groupes de limites *voisins*.

        Quand vous ajoutez ou modifiez la configuration d’un groupe de limites, vous avez la possibilité de bloquer le secours sur ce groupe de limites spécifique à partir du groupe actuel que vous configurez.

    Pour utiliser la nouvelle configuration, vous définissez des associations explicites (liens) entre un groupe de limites et un autre, et configurez tous les points de distribution de ce groupe associé avec la même durée en minutes. La durée que vous configurez détermine quand un client qui ne parvient pas à trouver une source de contenu dans son groupe de limites *actuel* peut commencer à rechercher des sources de contenu dans ce groupe de limites voisin.

    En plus des groupes de limites que vous configurez explicitement, chaque groupe de limites a un lien implicite vers le groupe de limites de site par défaut. Ce lien devient actif après 120 minutes, moment auquel le groupe de limites de site par défaut devient un groupe de limites voisin qui permet aux clients d’utiliser les points de distribution associés à ce groupe de limites comme emplacements sources de contenu.

    Ce comportement remplace ce qui était précédemment désigné sous le nom de secours pour le contenu.  Vous pouvez remplacer ce comportement par défaut de 120 minutes en associant explicitement le groupe de limites de site par défaut à un groupe *actuel* et en définissant une durée spécifique en minutes ou en bloquant totalement le secours pour empêcher son utilisation.


-     **Les clients tentent d’obtenir le contenu à partir de chaque point de distribution pendant 2 minutes au maximum :** quand un client recherche un emplacement source de contenu, il tente d’accéder à chaque point de distribution pendant 2 minutes avant d’essayer ensuite un autre point de distribution. Il s’agit d’un changement par rapport aux versions précédentes où les clients tentaient de se connecter à un point de distribution pendant 2 heures au maximum.

    - Le premier point de distribution qu’un client tente d’utiliser est sélectionné au hasard dans le pool des points de distribution disponibles du groupe (ou des groupes) de limites *actuel(s)* du client.

    - Après deux minutes, si le client n’a pas trouvé le contenu, il bascule vers un nouveau point de distribution et tente d’obtenir le contenu de ce serveur. Ce processus se répète toutes les deux minutes jusqu’à ce que le client trouve le contenu ou atteigne le dernier serveur dans son pool.

    - Si un client ne peut pas trouver un emplacement source de contenu valide dans son pool *actuel* avant la période de secours sur un groupe de limites *voisin*, le client ajoute alors les points de distribution de ce groupe *voisin* à la fin de sa liste actuelle, puis effectue des recherches dans le groupe étendu d’emplacements sources qui inclut les points de distribution des deux groupes de limites.

        > [!TIP]  
        > Quand vous créez un lien explicite entre le groupe de limites actuel et le groupe de limites de site par défaut, puis définissez une durée de secours inférieure à celle d’un lien vers un groupe de limites voisin, les clients commencent à effectuer des recherches dans les emplacements sources du groupe de limites de site par défaut avant d’inclure le groupe voisin.

    - Quand le client ne parvient pas à obtenir le contenu du dernier serveur dans le pool, il recommence le processus.





###  <a name="BKMK_PreferredMP"></a> À propos des points de gestion préférés  
 Les points de gestion préférés permettent à un client d’identifier un point de gestion associé à son emplacement réseau actuel (limite) avec celui-ci.  

-   Un client essaie d’utiliser un point de gestion préféré de son site attribué avant d’en utiliser un qui n’est pas configuré comme préféré.  
-   Pour utiliser cette option, vous devez l’activer pour la hiérarchie, puis configurer des groupes de limites au niveau de chaque site principal pour inclure les points de gestion à associer aux limites de ces groupes de limites.  
-   Quand les points de gestion préférés sont configurés et qu’un client organise sa propre liste de points de gestion, il place les points de gestion préférés en haut de sa liste de points de gestion attribués (qui comprend tous les points de gestion du site attribué du client).  

> [!NOTE]  
>  Quand un client est en itinérance (pour changer d’emplacement réseau, comme dans le cas d’un ordinateur portable déplacé vers un emplacement de bureau distant), il peut utiliser un point de gestion (ou un point de gestion proxy) du site local à son nouvel emplacement avant d’essayer d’utiliser un point de gestion de son site attribué (qui comprend les points de gestion préférés).  Consultez [Comprendre comment les clients recherchent des services et des ressources de site pour System Center Configuration Manager](../../../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md) pour plus d’informations.  

###   <a name="BKMK_BoundaryOverlap"></a> À propos du chevauchement des limites  
 Configuration Manager prend en charge les configurations de limites se chevauchant pour l’emplacement du contenu :  

-   **Quand un client demande du contenu** et que l’emplacement réseau du client appartient à plusieurs groupes de limites, Configuration Manager envoie au client une liste de tous les points de distribution qui disposent du contenu.  
-   **Quand un client demande à un serveur d’envoyer ou de recevoir des informations sur la migration de son état** et que l’emplacement réseau du client appartient à plusieurs groupes de limites, Configuration Manager envoie au client une liste de tous les points de migration d’état associés à un groupe de limites qui inclut l’emplacement réseau actuel du client.  

Ce comportement permet au client de sélectionner le serveur le plus proche depuis lequel transférer le contenu ou les informations sur la migration de l'état.  






## <a name="procedures-for-boundary-groups"></a>Procédures pour les groupes de limites
Les procédures suivantes s’appliquent à la version 1610 ou ultérieure. Si vous utilisez la version 1511, 1602 ou 1606, consultez les procédures de la section [Groupes de limites pour les versions 1511, 1602 et 1606 de System Center Configuration Manager](/sccm/core/servers/deploy/configure/boundary-groups-for-1511-1602-and-1606).


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

#### <a name="to-associate-a-content-deployment-server-or-management-point-with-a-boundary-group"></a>Pour associer un serveur de déploiement de contenu ou un point de gestion à un groupe de limites  
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


### <a name="to-enable-use-of-pre-release-features"></a>Pour permettre l’utilisation des fonctionnalités en préversion
1.  Dans la console Configuration Manager, cliquez sur **Administration** > **Configuration de site** > **Sites** puis, sous l’onglet **Accueil**, sélectionnez **Paramètres de hiérarchie**.  

2.  Sous l’onglet **Général** des paramètres de hiérarchie, sélectionnez **Accepter d’utiliser les fonctionnalités en préversion**.  

3.  Cliquez sur **OK** pour fermer la boîte de dialogue et enregistrer la configuration.  



##  <a name="BKMK_BoundaryBestPractices"></a> Meilleures pratiques en matière de limites  

-   **Utilisez une combinaison du plus petit nombre de limites qui répondent à vos besoins :**  
   Dans le passé, nous vous avons conseillé d’utiliser certains types de limites plus que d’autres. Compte-tenu des modifications apportées pour améliorer les performances, nous vous conseillons dorénavant d’utiliser le ou les types de votre choix qui fonctionnent dans votre environnement et qui vous permettent d’utiliser le plus petit nombre de limites possible pour simplifier vos tâches de gestion.      

-   **Éviter le chevauchement des limites pour l’attribution automatique de site :**  
     Chaque groupe de limites prend en charge les configurations d’attribution de site et d’emplacement du contenu, mais il est recommandé de créer un ensemble de groupes de limites à utiliser uniquement pour l’attribution de site. Cela signifie que vous devez vérifier qu’aucune limite d’un groupe de limites n’est membre d’un autre groupe de limites ayant une attribution de site différente. La raison est la suivante :  

    -   Une limite peut être incluse dans plusieurs groupes de limites.  

    -   Chaque groupe de limites peut être associé à un site principal différent pour l’attribution de site.  

    -   Un client sur une limite qui est membre de deux groupes de limites ayant des attributions de site différentes sélectionne au hasard un site auquel se joindre, site qui n’est pas nécessairement le site que vous avez prévu à cet effet.  Cette configuration est appelée chevauchement des limites.  

     Le chevauchement des limites n’est pas un problème pour l’emplacement du contenu. Il s’agit souvent d’une configuration souhaitée qui fournit aux clients des ressources ou emplacements de contenu supplémentaires qu’ils peuvent utiliser.  

