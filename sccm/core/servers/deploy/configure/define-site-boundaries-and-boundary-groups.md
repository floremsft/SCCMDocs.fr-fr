---
title: "Définir des limites de site | System Center Configuration Manager"
description: "Découvrez comment définir les emplacements réseau sur votre intranet pouvant contenir des appareils que vous souhaitez gérer."
ms.custom: na
ms.date: 10/06/2016
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
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 9df8b5d5fd67a5ced5860771295d05dfb56a3982


---
# <a name="define-site-boundaries-and-boundary-groups-for-system-center-configuration-manager"></a>Définir des limites de site et les groupes de limites pour System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

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


##  <a name="a-namebkmkboundariesa-boundaries"></a><a name="BKMK_Boundaries"></a> Limites  
 Vous pouvez créer manuellement des limites individuelles. En outre, vous pouvez configurer la [découverte de forêts Active Directory](../../../../core/servers/deploy/configure/about-discovery-methods.md#bkmk_aboutForest) afin de détecter automatiquement et de créer des limites pour chaque sous-réseau IP et site Active Directory ainsi découverts.  

-   Chaque limite représente un emplacement réseau et est disponible de n’importe quel site de la hiérarchie.  

-   Configuration Manager ne prend pas en charge l’entrée directe d’un sur-réseau en tant que limite. À la place, utilisez le type de limite de la plage d'adresses IP.  

-   Lorsque la fonctionnalité de découverte de forêts Active Directory identifie un sur-réseau attribué à un site Active Directory, Configuration Manager convertit le sur-réseau en limite de plage d'adresses IP.  

-   La limite configurée pour un client correspond au site Active Directory ou à l’adresse IP de réseau que le client identifie. (Il n’est pas rare qu’un client utilise une adresse IP dont l’administrateur Configuration Manager n’a pas connaissance. Si l’emplacement réseau d’un client est incertain, demandez au client qu’il signale son emplacement en exécutant la commande **IPCONFIG** sur le client.)  

Quand vous créez une limite, elle reçoit automatiquement un nom basé sur son type et son étendue. Ce nom ne peut pas être modifié. Au lieu de cela, lorsque vous configurez la limite, spécifiez une description permettant de l’identifier dans la console Configuration Manager.  

 Après avoir créé une limite, vous pouvez modifier ses propriétés pour effectuer les opérations suivantes :  

-   Ajouter la limite à un ou plusieurs groupes de limites.  

-   Changer le type ou la portée de la limite.  

-   Afficher l’onglet **Systèmes de site** des limites pour savoir quels serveurs de système de site (points de distribution, points de migration d’état et points de gestion) sont associés à la limite.  

#### <a name="to-create-a-boundary"></a>Pour créer une limite  

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

#### <a name="to-configure-a-boundary"></a>Pour configurer une limite  

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

##  <a name="a-namebkmkboundarygroupsa-boundary-groups"></a><a name="BKMK_BoundaryGroups"></a> Boundary groups  
 Créer des groupes de limites vous permet de regrouper de façon logique des emplacements réseau (limites) pour faciliter la gestion de votre infrastructure. Vous devez attribuer des limites à des groupes de limites avant de pouvoir utiliser le groupe de limites. Les clients utilisent la configuration du groupe de limites pour les opérations suivantes :  

-   Attribution automatique du site  

-   Emplacement du contenu  

-   Points de gestion préférés (Si vous utilisez des points de gestion préférés, vous devez activer cette option pour la hiérarchie et non pas à partir de la configuration du groupe de limites. Consultez la procédure suivante *Pour activer l’utilisation des points de gestion préférés*.)  

Quand vous configurez un groupe de limites, vous ajoutez une ou plusieurs limites au groupe de limites, puis vous configurez des paramètres supplémentaires utilisables par les clients situés sur ces limites.  

#### <a name="to-create-a-boundary-group"></a>Pour créer un groupe de limites  

1.  Dans la console Configuration Manager, cliquez sur **Administration** > **Configuration de la hiérarchie** >  **Groupes de limites**.  

2.  Dans l'onglet **Accueil** , dans le groupe **Créer** , cliquez sur **Créer un groupe limite**.  

3.  Dans la boîte de dialogue **Créer un groupe limite** , sélectionnez l'onglet **Général** et spécifiez un **Nom** pour ce groupe de limites.  

4.  Cliquez sur **OK** pour enregistrer le nouveau groupe de limites.  

#### <a name="to-configure-a-boundary-group"></a>Pour configurer un groupe de limites  

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

    3.  Pour modifier la vitesse de connexion réseau d'un serveur de système de site pour ce groupe de limites, sélectionnez le serveur, puis cliquez sur **Modifier la connexion**.  

         Par défaut, la vitesse de connexion pour chaque système de site est **Rapide**, mais peut être modifiée sur **Lente**. La vitesse de connexion réseau et la configuration d'un déploiement déterminent si un client peut télécharger du contenu à partir du serveur.  

6.  Cliquez sur **OK** pour fermer les propriétés du groupe de limites et enregistrer la configuration.  

#### <a name="to-associate-a-content-deployment-server-or-management-point-with-a-boundary-group"></a>Pour associer un serveur de déploiement de contenu ou un point de gestion à un groupe de limites  

1.  Dans la console Configuration Manager, cliquez sur **Administration** > **Configuration de la hiérarchie** >  **Groupes de limites**.  

2.  Sélectionnez le groupe de limites à modifier.  

3.  Dans l'onglet **Accueil** , dans le groupe **Propriétés** , cliquez sur **Propriétés**.  

4.  Dans la boîte de dialogue **Propriétés** du groupe de limites, sélectionnez l'onglet **Références** .  

5.  Sous **Sélectionner des serveurs de système de site**, cliquez sur **Ajouter**, cochez la case des serveurs de système de site que vous souhaitez associer à ce groupe de limites, puis cliquez sur **OK**.  

6.  Cliquez sur **OK** pour fermer la boîte de dialogue et enregistrer la configuration du groupe de limites.  

#### <a name="to-enable-use-of-preferred-management-points"></a>Pour activer l’utilisation des points de gestion préférés  

1.  Dans la console Configuration Manager, cliquez sur **Administration** > **Configuration de site** > **Sites** puis, sous l’onglet **Accueil**, sélectionnez **Paramètres de hiérarchie**.  

2.  Sous l’onglet **Général** des paramètres de hiérarchie, sélectionnez **Les clients préfèrent utiliser les points de gestion spécifiés dans les groupes de limites**.  

3.  Cliquez sur **OK** pour fermer la boîte de dialogue et enregistrer la configuration.  

#### <a name="to-configure-a-fallback-site-for-automatic-site-assignment"></a>Pour configurer un site de secours pour l'attribution automatique de site  

1.  Dans la console Configuration Manager, cliquez sur **Administration** > **Configuration de site** >  **Sites**.  

2.  Dans l'onglet **Accueil** , dans le groupe **Sites** , cliquez sur **Paramètres de hiérarchie**.  

3.  Dans l'onglet **Général** , cochez la case **Utiliser un site de secours**, puis sélectionnez un site dans la liste déroulante **Site de secours** .  

4.  Cliquez sur **OK** pour enregistrer la configuration.  

 Les sections suivantes fournissent des détails supplémentaires sur les configurations de groupes de limites.  

###  <a name="a-namebkmkboundarysiteassignmenta-about-site-assignment"></a><a name="BKMK_BoundarySiteAssignment"></a> À propos de l’attribution de site  
 Vous pouvez configurer chaque groupe de limites avec un site attribué pour les clients.  

-   Quand un client récemment installé utilise l’attribution automatique de site, il rejoint le site attribué d’un groupe de limites qui englobe l’emplacement réseau actuel du client.  

-   Après avoir été attribué à un site, un client ne modifie pas son attribution de site quand il change d’emplacement réseau. Par exemple, si le client se déplace vers un nouvel emplacement réseau représenté par une limite dans un groupe de limites disposant d’une attribution de site différente, le site attribué au client n’est pas modifié.  

-   Lorsque la découverte de systèmes Active Directory détecte une nouvelle ressource, les informations sur le réseau de la ressource découverte sont évaluées en fonction des limites dans les groupes de limites. Ce processus associe la nouvelle ressource à un site attribué pour une utilisation par la méthode d'installation poussée du client.  

-   Quand une limite est membre de plusieurs groupes de limites auxquels différents sites sont attribués, les clients sélectionnent l’un des sites aléatoirement.  

-   Les modifications apportées à un site attribué à des groupes de limites s’appliquent uniquement aux nouvelles actions d’attribution de site. Les clients déjà attribués à un site ne ré-évaluent pas leur attribution à un site en fonction des changements apportés à la configuration du groupe de limites (ou à leur emplacement réseau).  

Pour plus d’informations sur l’attribution de site client, consultez [Utilisation de l’attribution automatique de site pour les ordinateurs](../../../../core/clients/deploy/assign-clients-to-a-site.md#BKMK_AutomaticAssignment) dans [Guide pratique pour affecter des clients à un site dans System Center Configuration Manager](../../../../core/clients/deploy/assign-clients-to-a-site.md).  

###  <a name="a-namebkmkboundarycontentlocationa-about-content-location"></a><a name="BKMK_BoundaryContentLocation"></a> À propos de l’emplacement du contenu  
 Vous pouvez configurer chaque groupe de limites avec un ou plusieurs points de distribution et points de migration d’état, mais aussi associer les mêmes points de distribution et points de migration d’état à plusieurs groupes de limites.  

-   **Lors de la distribution de logiciels**, les clients demandent un emplacement pour le contenu de déploiement. Configuration Manager envoie au client une liste de points de distribution associés à chaque groupe de limites qui inclut l’emplacement réseau actuel du client.  

-   **Durant le déploiement de système d’exploitation** , les clients demandent un emplacement où envoyer ou recevoir des informations sur la migration de leur état. Configuration Manager envoie au client une liste de points de migration d’état associés à chaque groupe de limites qui inclut l’emplacement réseau actuel du client.  

Ce comportement permet au client de sélectionner le serveur le plus proche depuis lequel transférer le contenu ou les informations sur la migration de l'état.  

###  <a name="a-namebkmkpreferredmpa-about-preferred-management-points"></a><a name="BKMK_PreferredMP"></a> À propos des points de gestion préférés  
 Les points de gestion préférés permettent à un client d’identifier un point de gestion associé à son emplacement réseau actuel (limite) avec celui-ci.  

-   Un client essaie d’utiliser un point de gestion préféré de son site attribué avant d’en utiliser un qui n’est pas configuré comme préféré.  

-   Pour utiliser cette option, vous devez l’activer pour la hiérarchie, puis configurer des groupes de limites au niveau de chaque site principal pour inclure les points de gestion à associer aux limites de ces groupes de limites.  

-   Quand les points de gestion préférés sont configurés et qu’un client organise sa propre liste de points de gestion, il place les points de gestion préférés en haut de sa liste de points de gestion attribués (qui comprend tous les points de gestion du site attribué du client).  

> [!NOTE]  
>  Quand un client est en itinérance (pour changer d’emplacement réseau, comme dans le cas d’un ordinateur portable déplacé vers un emplacement de bureau distant), il peut utiliser un point de gestion (ou un point de gestion proxy) du site local à son nouvel emplacement avant d’essayer d’utiliser un point de gestion de son site attribué (qui comprend les points de gestion préférés).  Consultez [Comprendre comment les clients recherchent des services et des ressources de site pour System Center Configuration Manager](../../../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md) pour plus d’informations.  

###  <a name="a-namebkmkboundaryoverlapa-about-overlapping-boundaries"></a><a name="BKMK_BoundaryOverlap"></a> À propos du chevauchement des limites  
 Configuration Manager prend en charge les configurations de limites se chevauchant pour l’emplacement du contenu :  

-   **Quand un client demande du contenu** et que l’emplacement réseau du client appartient à plusieurs groupes de limites, Configuration Manager envoie au client une liste de tous les points de distribution qui disposent du contenu.  

-   **Quand un client demande à un serveur d’envoyer ou de recevoir des informations sur la migration de son état** et que l’emplacement réseau du client appartient à plusieurs groupes de limites, Configuration Manager envoie au client une liste de tous les points de migration d’état associés à un groupe de limites qui inclut l’emplacement réseau actuel du client.  

Ce comportement permet au client de sélectionner le serveur le plus proche depuis lequel transférer le contenu ou les informations sur la migration de l'état.  

###  <a name="a-namebkmkboudnarynetworkspeeda-about-network-connection-speed"></a><a name="BKMK_BoudnaryNetworkSpeed"></a> À propos de la vitesse de connexion réseau  
 Vous pouvez définir la vitesse de connexion réseau pour chaque serveur de système de site dans un groupe de limites. Ce paramètre s’applique aux clients qui se connectent à un système de site basé sur cette configuration de groupes de limites. Le même serveur de système de site peut avoir une autre vitesse de connexion définie dans des groupes de limites différents.  

 Par défaut, la vitesse de connexion réseau est configurée sur **Rapide**, mais elle peut également être configurée sur **Lente**. La vitesse de connexion réseau et la configuration de déploiement déterminent si un client peut télécharger du contenu à partir d'un point de distribution lorsque le client est dans un groupe de limites associé.  

 Pour plus d’informations sur les effets de la vitesse de connexion réseau sur l’obtention du contenu par les clients, consultez [Scénarios d’emplacement source de contenu](../../../../core/plan-design/hierarchy/content-source-location-scenarios.md).  

##  <a name="a-namebkmkboundarybestpracticesa-best-practices-for-boundaries"></a><a name="BKMK_BoundaryBestPractices"></a> Meilleures pratiques en matière de limites  

-   **Utilisez le type de limite de plage d’adresses IP uniquement quand les autres types de limites ne peuvent pas être utilisés :**  

     Lorsque vous concevez votre stratégie de limite, nous vous recommandons d'utiliser des limites basées sur des sites Active Directory avant d'utiliser d'autres types de limites. Lorsqu'il n'est pas possible d'utiliser des limites basées sur des sites Active Directory, utilisez le sous-réseau IP ou des limites IPv6. Si aucune de ces options n'est disponible, exploitez les limites de plage d'adresses IP. Cela est dû au fait que le site évalue régulièrement les membres des limites et la requête requise pour évaluer les membres d'une plage d'adresses IP nécessite une utilisation des ressources SQL Server beaucoup plus importante que les requêtes qui évaluent les membres d'autres types de limites.  

-   **Éviter le chevauchement des limites pour l’attribution automatique de site :**  

     Chaque groupe de limites prend en charge les configurations d’attribution de site et d’emplacement du contenu, mais il est recommandé de créer un ensemble de groupes de limites à utiliser uniquement pour l’attribution de site. Cela signifie que vous devez vérifier qu’aucune limite d’un groupe de limites n’est membre d’un autre groupe de limites ayant une attribution de site différente. La raison est la suivante :  

    -   Une limite peut être incluse dans plusieurs groupes de limites.  

    -   Chaque groupe de limites peut être associé à un site principal différent pour l’attribution de site.  

    -   Un client sur une limite qui est membre de deux groupes de limites ayant des attributions de site différentes sélectionne au hasard un site auquel se joindre, site qui n’est pas nécessairement le site que vous avez prévu à cet effet.  Cette configuration est appelée chevauchement des limites.  

     Le chevauchement des limites n’est pas un problème pour l’emplacement du contenu. Il s’agit souvent d’une configuration souhaitée qui fournit aux clients des ressources ou emplacements de contenu supplémentaires qu’ils peuvent utiliser.  



<!--HONumber=Nov16_HO1-->


