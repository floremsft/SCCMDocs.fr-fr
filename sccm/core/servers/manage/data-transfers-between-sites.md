---
title: "Transferts de données | System Center Configuration Manager"
description: "Découvrez comment Configuration Manager déplace les données entre les sites et comment vous pouvez gérer le transfert de ces données sur votre réseau."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: dc526e8d-fac3-4bb5-b206-03ad29b0ae11
caps.latest.revision: 12
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 1abd28aa4ce4f946f6328f8f7924b5f5a81e640c


---
# <a name="data-transfers-between-sites-in-system-center-configuration-manager"></a>Transfert de données entre sites dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

System Center Configuration Manager utilise la **réplication basée sur les fichiers** et la **réplication de base de données** pour transférer différents types d’informations entre les sites.  Les sujets de cette rubrique peuvent vous aider à comprendre comment Configuration Manager déplace les données entre les sites et comment vous pouvez gérer le transfert de ces données sur votre réseau.  


##  <a name="a-namebkmkfileroutea-file-based-replication"></a><a name="bkmk_fileroute"></a> Réplication basée sur les fichiers  
 Configuration Manager utilise la réplication basée sur les fichiers pour transférer des données basées sur les fichiers entre les sites dans votre hiérarchie. Ces données incluent du contenu, par exemple, des applications et des packages que vous voulez déployer sur des points de distribution dans des sites enfants, ainsi que des enregistrements de données de découverte non traités qui sont transférés vers des sites parents pour le traitement.  

 La communication basée sur les fichiers entre les sites utilise le protocole **SMB (Server Message Block)** sur le port **TCP/IP 445**. Vous pouvez spécifier des configurations avec limitation de bande passante et mode impulsion pour contrôler la quantité de données transférées sur le réseau, ainsi que des planifications pour contrôler à quel moment les données sont envoyées via le réseau.  

###  <a name="a-namebkmkroutesa-file-replication-routes"></a><a name="bkmk_routes"></a> Itinéraires de réplication de fichiers  
 Les informations suivantes peuvent vous aider à configurer et à utiliser les itinéraires de réplication de fichiers :  

 **de réplication de fichiers** : chaque route de réplication de fichiers identifie un site de destination vers lequel les données basées sur des fichiers peuvent être transférées. Chaque site prend en charge un seul itinéraire de réplication de fichiers vers un site de destination spécifique.  

 Configuration Manager prend en charge les configurations suivantes pour les itinéraires de réplication de fichiers :  

-   **Compte de réplication de fichiers** : ce compte permet d’établir une connexion au site de destination et d’écrire des données dans le partage **SMS_SITE** de ce site. Les données écrites dans ce partage sont traitées par le site de réception. Par défaut, quand un site est ajouté à la hiérarchie, Configuration Manager attribue le compte d’ordinateur du serveur de site du nouveau site en tant que **Compte de réplication de fichiers**de ce site. Ce compte est ensuite ajouté au groupe **SMS_SiteToSiteConnection_&lt;code_site\>** du site de destination, qui est un groupe local sur l’ordinateur accordant l’accès au partage **SMS_SITE**. Vous pouvez modifier ce compte en un compte d'utilisateur Windows. Si vous changez le compte, vérifiez que vous ajoutez le nouveau compte au groupe **SMS_SiteToSiteConnection_&lt;code_site\>** du site de destination.  

    > [!NOTE]  
    >  Les sites secondaires utilisent toujours le compte d'ordinateur du serveur de site secondaire en tant que **Compte de réplication de fichiers**.  

-   **Planification**: vous pouvez configurer le calendrier de chaque itinéraire de réplication de fichiers pour restreindre le type de données et l'heure de transfert des données vers le site de destination.  

-   **Limites du taux de transfert**: vous pouvez configurer les limites du taux de transfert pour chaque itinéraire de réplication de fichiers pour contrôler la bande passante réseau utilisée lorsque le site transfère les données vers le site de destination :  

    -   Utilisez l'option **Mode impulsion** pour spécifier la taille des blocs de données envoyés vers le site de destination. Vous pouvez également spécifier un délai entre l'envoi de chaque bloc de données. Utilisez cette option lorsque vous devez envoyer des données via une connexion réseau de très faible bande passante vers le site de destination. Par exemple, vous pouvez forcer l'envoi de 1 Ko de données toutes les cinq secondes, mais empêcher l'envoi de 1 Ko toutes les trois secondes, quelle que soit la vitesse de la liaison ou son utilisation.  

    -   Utilisez l'option **Limité aux taux de transfert maximaux indiqués par heure** pour permettre à un site d'envoyer des données vers un site de destination en utilisant uniquement le pourcentage de temps spécifié. Quand vous utilisez cette option, Configuration Manager n’identifie pas la bande passante disponible du réseau, mais divise plutôt le temps pendant lequel il peut envoyer des données en périodes plus petites. Ensuite, les données sont envoyées en une courte plage horaire, suivie de plages horaires pendant lesquelles aucune donnée n'est envoyée. Par exemple, si le taux maximal est fixé à **50 %**, Configuration Manager transmet les données pendant une durée, suivie d’une période d’une durée égale pendant laquelle aucune donnée n’est envoyée. La taille effective des donnés ou la taille des blocs de données ne sont pas gérées. En revanche, seule la durée pendant laquelle des données sont envoyées est gérée.  

        > [!CAUTION]  
        >  Par défaut, un site peut utiliser jusqu'à trois **envois simultanés** pour transférer des données vers un site de destination. Lorsque vous définissez des limites de taux pour un itinéraire de réplication de fichiers, les **envois simultanés** dans le cadre de l'envoi de données vers ce site sont limités à un. Cela s'applique même lorsque l'option **Limiter la bande passante disponible (%)** est définie sur **100 %**. Par exemple, si vous utilisez les paramètres par défaut pour l'expéditeur, le taux de transfert vers le site de destination est réduit à un tiers de la capacité par défaut.  

-   Vous pouvez configurer un itinéraire de réplication de fichiers entre deux sites secondaires pour acheminer du contenu basé sur des fichiers entre ces sites.  

Pour gérer un itinéraire de réplication de fichiers, dans l'espace de travail **Administration** , développez le nœud **Configuration de la hiérarchie** , puis sélectionnez **Réplication de fichiers**.  

**Expéditeur** : chaque site a un expéditeur. L'expéditeur gère la connexion réseau entre un site et un site de destination et peut établir des connexions vers plusieurs sites à la fois. Pour se connecter à un site, l'expéditeur utilise l'itinéraire de réplication de fichiers vers le site pour identifier le compte à utiliser pour établir la connexion réseau. L’expéditeur utilise également ce compte pour écrire des données sur le partage **SMS_SITE** du site de destination.  

 Par défaut, l'expéditeur écrit des données sur un site de destination en utilisant plusieurs **envois simultanés**, généralement appelés « thread ». Chaque envoi simultané (ou « thread ») peut transférer un objet basé sur un fichier différent vers le site de destination. Par défaut, lorsque l'expéditeur commence à envoyer un objet, il continue d'écrire des blocs de données pour cet objet jusqu'à la fin de l'envoi de l'objet complet. Une fois que toutes les données de l'objet ont été envoyées, l'envoi d'un nouvel objet peut commencer sur ce thread.  

 Vous pouvez configurer les paramètres suivants pour un expéditeur :  

-   **Nombre maximal d'envois simultanés**: par défaut, chaque site est configuré pour utiliser cinq **envois simultanés**, dont trois peuvent utilisés dans le cadre de l'envoi de données vers un site de destination quelconque. En augmentant ce nombre, vous pouvez augmenter le débit des données échangées entre les sites en permettant à Configuration Manager de transférer davantage de fichiers à la fois. Cela a également pour effet d'augmenter la demande en bande passante entre les sites.  

-   **Paramètres de nouvelle tentative**: par défaut, chaque site est configuré pour effectuer deux nouvelles tentatives de connexion en cas de problème avec un délai d'une minute entre chaque essai. Vous pouvez modifier le nombre de tentatives de connexion du site, ainsi que le temps d'attente entre les tentatives.  

Pour gérer l'expéditeur pour un site, développez le nœud **Configuration du site** dans l'espace de travail **Administration** , sélectionnez le nœud **Sites** , puis cliquez sur **Propriétés** pour le site à gérer. Cliquez dans l'onglet **Expéditeur** pour modifier la configuration de l'expéditeur.  

##  <a name="a-namebkmkdbrepa-database-replication"></a><a name="bkmk_dbrep"></a> Réplication de base de données  
La réplication de base de données Configuration Manager utilise SQL Server pour transférer des données et fusionner les modifications apportées à la base de données d’un site avec les informations stockées dans la base de données sur d’autres sites de la hiérarchie.  

-   Cela permet à tous les sites de partager les mêmes informations.  

-   Quand vous installez un site dans une hiérarchie, la réplication de base de données est configurée automatiquement entre le nouveau site et son site parent désigné.  

-   Une fois l’installation du site terminée, la réplication de base de données démarre automatiquement.  

Quand vous ajoutez un nouveau site à une hiérarchie, Configuration Manager crée une base de données générique sur le nouveau site. Ensuite, le site parent crée un instantané des données appropriées de sa base de données et transfère cet instantané vers le nouveau site par réplication basée sur des fichiers. Le nouveau site utilise ensuite un programme de copie en bloc de SQL Server pour charger les informations dans sa copie locale de la base de données Configuration Manager. Une fois l'instantané chargé, chaque site effectue une réplication de base de données avec l'autre site.  

Pour répliquer des données entre les sites, Configuration Manager utilise son propre service de réplication de base de données. Le service de réplication de base de données utilise le suivi des modifications de SQL Server pour contrôler les modifications apportées à la base de données du site local, puis procède à la réplication de ces modifications sur les autres sites à l’aide de **SQL Server Service Broker**. Par défaut, ce processus utilise le port **TCP/IP 4022**.  

Configuration Manager regroupe les données répliquées par la réplication de base de données dans différents groupes de réplication.  

-   À chaque groupe de réplication correspond une planification de réplication fixe et distincte qui détermine la fréquence de réplication vers d'autres sites des modifications apportées aux données.  

     Par exemple, une modification de configuration apportée à une configuration d'administration basée sur des rôles est répliquée rapidement vers d'autres sites pour assurer que ces modifications sont appliquées dès que possible. Par contre, une modification de configuration de moindre priorité, par exemple, une demande d’installation d’un nouveau site secondaire, est répliquée avec moins d’urgence, et la demande prend quelques minutes avant d’arriver au site principal de destination.  

-   Vous pouvez modifier les éléments suivants pour la réplication de base de données :  

    -   **liens de réplication de base de données** vous permettent de contrôler à quel moment le réseau reçoit un trafic spécifique.  

    -   Les**vues distribuées** correspondent à une configuration des liens de réplication permettant aux demandes formulées sur un site d’administration centrale relatives à des données de site sélectionnées d’accéder à ces données directement à partir de la base de données d’un site principal enfant.  

    -   Les**planifications** vous permettent de spécifier quand un lien de réplication doit être utilisé et quand différents types de données de site sont répliqués.  

    -   La**synthèse** des données sur le trafic réseau qui traverse les liens de réplication a lieu toutes les 15 minutes, par défaut, et est utilisée dans les rapports pour la réplication de base de données.  

    -   Les**seuils de réplication de base de données** définissent à quels moments les liens sont signalés comme détériorés ou en échec. Vous pouvez également configurer le moment où Configuration Manager déclenche des alertes sur les liens de réplication dont l'état est Détérioré ou Échec.  

Configuration Manager classe les données qu’il réplique via la réplication de base de données en tant que données globales ou données de site. Lorsqu'une réplication de base de données se produit, les modifications apportées aux données globales et aux données de site sont transférées via le lien de réplication de base de données. Les données globales peuvent être répliquées vers un site parent ou enfant, tandis qu'un site est répliqué uniquement vers un site parent. Un troisième type de données, les données locales, n'est pas répliqué vers d'autres sites. Les données locales incluent des informations qui ne sont pas requises par les autres sites :  

-   **Données globales**: Les données globales font référence aux objets créés par l'administrateur et qui sont répliquées sur tous les sites dans la hiérarchie, bien que les sites secondaires reçoivent uniquement un sous-ensemble des données globales, en tant que données globales proxy. Les déploiements logiciels, les mises à jour logicielles, les définitions de regroupement et les étendues de sécurité de l'administration basée sur des rôles sont autant d'exemples de données globales. Les administrateurs peuvent créer des données globales sur des sites d'administration centrale et des sites principaux.  

-   **Données de site** : Les données de site font référence aux informations opérationnelles créées par les sites principaux Configuration Manager et les clients qui sont sous la hiérarchie de sites principaux. Les données de site sont répliquées vers le site d'administration centrale mais pas vers d'autres sites principaux. Les données d'inventaire matériel, les messages d'états, les alertes et les résultats de regroupements basés sur des requêtes sont des exemples de données de site. Les données de site ne peuvent être consultées que sur le site d'administration centrale et le site principal d'où proviennent les données. Les données de site ne peuvent être modifiées que sur le site principal sur lequel elles ont été créées.  

     Toutes les données de site sont répliquées vers le site d'administration centrale. Par conséquent, le site d'administration centrale peut procéder à l'administration et au reporting pour toute la hiérarchie.  

Les sections suivantes détaillent les configurations disponibles pour gérer la réplication de base de données.  

###  <a name="a-namebkmkdblinksa-database-replication-links"></a><a name="bkmk_Dblinks"></a> Liens de réplication de base de données  
Quand vous installez un nouveau site dans une hiérarchie, Configuration Manager crée automatiquement un lien de réplication de base de données entre les deux sites. Un seul lien est créé pour connecter le nouveau site au site parent.  

Chaque lien de réplication de base de données prend en charge les configurations pour faciliter le contrôle du transfert de données via le lien de réplication. Chaque lien de réplication prend en charge des configurations distinctes. Les contrôles pour les liens de réplication de base de données sont les suivants :  

-   Utilisez des vues distribuées pour arrêter la réplication de données de site sélectionnées d'un site principal vers le site d'administration centrale et permettez au site d'administration centrale d'accéder directement à ces données à partir de la base de données du site principal.  

-   Planifiez le moment où les données de site sélectionnées sont transférées d'un site principal enfant vers le site d'administration centrale.  

-   Définissez les paramètres qui déterminent dans quelles circonstances un lien de réplication de base de données a l'état Détérioré ou Échec.  

-   Configurez à quel moment déclencher des alertes dans le cas d'un lien de réplication en échec.  

-   Spécifiez la fréquence à laquelle Configuration Manager résume les données sur le trafic de réplication qui utilise le lien de réplication. Ces données sont utilisées dans les rapports.  

Pour configurer un lien de réplication de base de données, vous devez modifier les propriétés du lien dans la console Configuration Manager à partir du nœud **Réplication de la base de données**. Ce nœud apparaît dans l’espace de travail **Surveillance** et sous le nœud **Configuration de la hiérarchie** dans l’espace de travail **Administration** . Vous pouvez modifier un lien de réplication à partir du site parent ou du site enfant du lien de réplication.  

> [!TIP]  
>  Vous pouvez modifier les liens de réplication de base de données à partir du nœud **Réplication de la base de données** dans chaque espace de travail. En revanche, lorsque vous utilisez le nœud **Réplication de la base de données** dans l'espace de travail **Surveillance** , vous pouvez également consulter l'état de réplication de base de données des liens de réplication et accéder à l'outil Analyseur de lien de réplication, qui peut vous aider à identifier les problèmes de réplication de base de données.  

Pour plus d'informations sur la configuration des liens de réplication, voir [Contrôles de réplication de la base de données du site](#BKMK_DBRepControls). Pour plus d’informations sur la surveillance de la réplication, consultez la section [Comment surveiller des liens de réplication de la base de données et l’état de la réplication](../../../core/servers/manage/monitor-hierarchy-and-replication-infrastructure.md#BKMK_MonitorRepLinksAndStatuss) dans la rubrique [Surveiller l’infrastructure de la hiérarchie et de la réplication dans System Center Configuration Manager](../../../core/servers/manage/monitor-hierarchy-and-replication-infrastructure.md).  

Pour planifier des liens de réplication de base de données, aidez-vous des informations figurant dans les sections suivantes.  

###  <a name="a-namebkmkdistviewsa-distributed-views"></a><a name="bkmk_distviews"></a> Vues distribuées  
Les vues distribuées permettent aux demandes formulées sur un site d'administration centrale relatives à des données de site sélectionnées d'accéder à ces données directement à partir de la base de données d'un site principal enfant. Cet accès direct évite d'avoir à répliquer ces données de site du site principal vers le site d'administration centrale. Comme chaque lien de réplication est indépendant des autres liens de réplication, vous pouvez activer les vues distribuées uniquement sur les liens de réplication de votre choix. Les vues distribuées ne sont pas prises en charge entre un site principal et un site secondaire.  

Les vues distribuées peuvent offrir les avantages suivants :  

-   Diminution de la charge processeur lors du traitement des modifications apportées à la base de données sur le site d'administration centrale et les sites principaux.  

-   Réduction de la quantité de données transférées sur le réseau à destination du site d'administration centrale.  

-   Amélioration des performances du serveur SQL Server hébergeant la base de données du site d'administration centrale.  

-   Diminution de l'espace disque utilisé par la base de données sur le site d'administration centrale.  

Vous pouvez envisager d'utiliser des vues distribuées lorsqu'un site principal est situé à proximité du site d'administration centrale sur le réseau et que les deux sites sont toujours actifs et connectés. En effet, les vues distribuées remplacent la réplication des données sélectionnées entre les sites par des connexions directes entre les serveurs SQL Server de chaque site. Cette connexion directe est établie chaque fois qu'une demande portant sur ces données est formulée sur le site d'administration centrale. En règle générale, les demandes de données que vous pouvez autoriser pour les vues distribuées sont formulées lorsque vous exécutez des rapports ou des requêtes, affichez des informations dans l'Explorateur de ressources et par l'évaluation des regroupements lorsque ceux-ci incluent des règles basées sur les données de site.  

Par défaut, les vues distribuées sont désactivées pour chaque lien de réplication. Lorsque vous activez les vues distribuées pour un lien de réplication, vous sélectionnez les données de site qui ne seront pas répliquées sur le site d'administration centrale via ce lien, et vous autorisez le site d'administration centrale à accéder à ces données directement à partir de la base de données du site principal enfant qui partage le lien. Pour les vues distribuées, vous pouvez configurer les types de données de site suivants :  

-   Données d'inventaire matériel des clients  

-   Données d'inventaire et de contrôle de logiciel des clients  

-   Messages d'état en provenance des clients, du site principal et de tous les sites secondaires  

Sur le plan opérationnel, les vues distribuées sont invisibles pour un utilisateur administratif qui consulte des données dans la console Configuration Manager ou dans des rapports. Quand une requête est effectuée pour des données activées pour les vues distribuées, le serveur SQL Server qui héberge la base de données du site d'administration centrale accède directement au serveur SQL Server du site principal enfant afin d'extraire les informations. Par exemple, vous utilisez une console Configuration Manager au niveau du site d’administration centrale pour demander des informations sur l’inventaire matériel de deux sites alors qu’un seul des deux possède un inventaire matériel compatible avec une vue distribuée. Les informations d'inventaire pour les clients du site qui n'est pas configuré pour les vues distribuées sont extraites de la base de données au niveau du site d'administration centrale. Les informations d'inventaire pour les clients du site qui n'est pas configuré pour les vues distribuées sont accessibles à partir de la base de données au niveau du site principal enfant. Ces informations apparaissent dans la console Configuration Manager ou un rapport sans distinction par rapport à la source.  

Tant qu'un lien de réplication comporte un type de données activé pour les vues distribuées, le site principal enfant ne réplique pas ces données sur le site d'administration centrale. Dès que vous désactivez les vues distribuées pour un type de données, le site principal enfant reprend la réplication de ces données sur le site d'administration centrale dans le cadre d'une réplication normale des données. Toutefois, pour que ces données soient disponibles au niveau du site d'administration centrale, les groupes de réplication qui les contiennent doivent se réinitialiser entre le site principal et le site d'administration centrale. De même, après la désinstallation d'un site principal dont les vues distribuées sont activées, le site d'administration centrale doit effectuer la réinitialisation de ses données pour que vous puissiez accéder aux données activées pour les vues distribuées sur le site d'administration centrale.  

> [!IMPORTANT]  
>  Lorsque vous utilisez des vues distribuées sur un lien de réplication dans la hiérarchie, vous devez les désactiver pour tous les liens de réplication avant de désinstaller un site principal. Pour plus d’informations, consultez [Désinstaller un site principal configuré avec des vues distribuées](../../../core/servers/deploy/install/uninstall-sites-and-hierarchies.md#BKMK_UninstallPrimaryDistViews).  

**Conditions préalables et limitations des vues distribuées :**  

-   Les vues distribuées sont prises en charge uniquement sur des liens de réplication entre un site d'administration centrale et un site principal.  

-  Le site d’administration centrale doit utiliser une édition Enterprise de SQL Server. Le site principal n’a pas cette exigence.

-   Le site d'administration centrale peut disposer d'une seule instance du fournisseur SMS installée, et cette instance doit être installée sur le serveur de base de données du site. Cette contrainte sert à prendre en charge l'authentification Kerberos requise pour activer le serveur SQL Server au niveau du site d'administration centrale afin d'accéder au serveur SQL Server au niveau du site principal enfant. Il n'existe aucune limitation sur le fournisseur SMS au niveau du site principal enfant.  

-   Le site d'administration centrale peut disposer d'un seul point SQL Server Reporting Services installé, et ce dernier doit se trouver sur le serveur de base de données du site. Cette contrainte sert à prendre en charge l'authentification Kerberos requise pour activer le serveur SQL Server au niveau du site d'administration centrale afin d'accéder au serveur SQL Server au niveau du site principal enfant.  

-   La base de données du site ne peut pas être hébergée sur un cluster SQL Server.  

-   La base de données du site ne peut pas être hébergé sur un groupe de disponibilité SQL Server AlwaysOn.  

-   Le compte d'ordinateur du serveur de base de données du site d'administration centrale requiert des autorisations **Read** sur la base de données du site principal.  

> [!IMPORTANT]  
>  Les vues distribuées et les planifications relatives aux dates de réplication des données sont des configurations qui s'excluent mutuellement pour un lien de réplication de la base de données.  

###  <a name="a-namebkmkschedulesa-schedule-transfers-of-site-data-on-database-replication-links"></a><a name="BKMK_schedules"></a> Planifier les transferts de données de site sur les liens de réplication de la base de données  
Pour mieux contrôler la bande passante réseau utilisée pour répliquer les données de site depuis un site principal enfant vers son site d'administration centrale, vous pouvez planifier le moment auquel un lien de réplication est utilisé, ainsi que spécifier quand les différents types de données de site se répliquent. Vous pouvez contrôler le moment auquel le site principal réplique les messages d'état, l'inventaire et les données de contrôle. Les liens de réplication de la base de données des sites secondaires ne prennent pas en charge les planifications des données de site. Le transfert de données globales ne peut pas être planifié.  

Quand vous configurez une planification de lien de réplication de la base de données, vous pouvez restreindre le transfert des données de site sélectionnées depuis le site principal vers le site d'administration centrale et vous pouvez configurer différentes heures pour répliquer des types différents de données de site.  

> [!IMPORTANT]  
>  Les vues distribuées et les planifications relatives aux dates de réplication des données sont des configurations qui s'excluent mutuellement pour un lien de réplication de la base de données.  

###  <a name="a-namebkmksummarizedbreplicationa-summarization-of-database-replication-traffic"></a><a name="BKMK_SummarizeDBReplication"></a> Synthèse du trafic de réplication de la base de données  
Chaque site réalise régulièrement une synthèse des données sur le trafic réseau qui traverse les liens de réplication de la base de données qui incluent le site. Ces données résumées sont utilisées dans les rapports pour la réplication de la base de données. Les deux sites sur un lien de réplication résument le trafic réseau qui traverse le lien de réplication. Le résumé des données est effectué par le serveur SQL Server qui héberge la base de données du site. Après le résumé des données, ces informations se répliquent sur d'autres sites en tant que données globales.  

Par défaut, le résumé se produit toutes les 15 minutes. Vous pouvez modifier la fréquence du résumé du trafic réseau en modifiant la valeur **Intervalle de résumé** dans les propriétés du lien de réplication de la base de données. La fréquence du résumé affecte les informations affichées dans les rapports sur la réplication de la base de données. Vous pouvez définir cet intervalle entre 5 et 60 minutes. Lorsque vous augmentez la fréquence du résumé, vous augmentez la charge de traitement sur le serveur SQL Server au niveau de chaque site sur le lien de réplication.  

###  <a name="a-namebkmkdbrepthresholdsa-database-replication-thresholds"></a><a name="BKMK_DBRepThresholds"></a> Seuils de réplication de la base de données  
Les seuils de réplication de la base de données définissent le moment auquel un lien de réplication de la base de données est signalé comme étant détérioré ou en état d'échec. Par défaut, un lien est défini comme détérioré quand l'un des groupes de réplication ne parvient pas à terminer la réplication à l'issue de 12 tentatives consécutives ; il est en état d'échec quand l'un des groupes de réplication ne parvient pas à se répliquer à l'issue de 24 tentatives consécutives.  

Vous pouvez spécifier des valeurs personnalisées pour ajuster le moment auquel Configuration Manager signale qu’un lien de réplication est détérioré ou en état d’échec. L’ajustement du moment auquel Configuration Manager signale chaque état de vos liens de réplication de la base de données peut vous aider à surveiller l’intégrité de la réplication de la base de données avec précision.  

Étant donné qu'il est possible qu'un seul ou plusieurs groupes de réplication ne parviennent pas à se répliquer alors que d'autres continuent de le faire correctement, prévoyez de vérifier l'état de réplication d'un lien de réplication dès qu'un état détérioré est signalé. S'il existe des délais récurrents pour des groupes de réplication et qu'ils ne présentent pas de problème, où lorsque la liaison réseau entre les sites dispose d'une faible bande passante disponible, envisagez de modifier le nombre de nouvelles tentatives pour l'état détérioré ou en échec du lien. Quand vous augmentez le nombre de nouvelles tentatives avant que le lien ne soit défini comme détérioré ou en état d'échec, vous pouvez éliminer les faux avertissements liés aux problèmes connus, ce qui vous permet de suivre l'état du lien de manière plus précise.  

Vous devez également appréhender l'intervalle de synchronisation de réplication pour chaque groupe de réplication pour comprendre la fréquence à laquelle la réplication de ce groupe se produit. Vous pouvez afficher la valeur **Intervalle de synchronisation** des groupes de réplication sous l'onglet **Détail de la réplication** d'un lien de réplication dans le nœud **Réplication de la base de données** de l'espace de travail **Surveillance** .  

Pour plus d’informations sur la surveillance de la réplication de base de données, notamment l’affichage de l’état de réplication, consultez la section [Comment surveiller des liens de réplication de la base de données et l’état de la réplication](../../../core/servers/manage/monitor-hierarchy-and-replication-infrastructure.md#BKMK_MonitorRepLinksAndStatuss) de la rubrique [Comment surveiller des liens de réplication de la base de données et l’état de la réplication](../../../core/servers/manage/monitor-hierarchy-and-replication-infrastructure.md#BKMK_MonitorRepLinksAndStatuss).  

Pour plus d'informations sur la configuration des seuils de réplication de base de données, voir [Contrôles de réplication de la base de données du site](#BKMK_DBRepControls).  

##  <a name="a-namebkmkdbrepcontrolsa-site-database-replication-controls"></a><a name="BKMK_DBRepControls"></a> Contrôles de réplication de la base de données du site  
Chaque base de données du site prend en charge des configurations qui peuvent vous aider à contrôler la bande passante réseau utilisée pour la réplication de la base de données. Ces configurations s'appliquent uniquement à la base de données du site dans laquelle vous configurez les paramètres, et elles sont toujours utilisées lorsque le site réplique des données par réplication de la base de données sur un autre site.  

Les contrôles de réplication pour chaque base de données de site sont les suivants :  

-   Modifiez le port que Configuration Manager utilise pour SQL Server Service Broker.  

-   Configurez le délai d'attente avant que les échecs de réplication ne déclenchent la réinitialisation de la copie de la base de données du site.  

-   Configurez une base de données de site afin qu'elle compresse les données qu'elle réplique par réplication de base de données. Les données sont compressées uniquement pour le transfert entre les sites et non pour le stockage dans la base de données du site sur l'un des sites.  

Pour configurer les contrôles de réplication d’une base de données de site, vous devez modifier les propriétés de la base de données de site dans la console Configuration Manager à partir du nœud **Réplication de la base de données**. Ce nœud apparaît sous le nœud **Configuration de la hiérarchie** dans l'espace de travail **Administration** et également dans l' **espace de travail Surveillance**. Pour modifier les propriétés de la base de données du site, sélectionnez le lien de réplication entre les sites, puis ouvrez soit **Propriétés de la base de données parent** , soit **Propriétés de la base de données enfant**.  

> [!TIP]  
>  Vous pouvez configurer les contrôles de réplication de la base de données à partir du nœud **Réplication de la base de données** dans l'un ou l'autre espace de travail. En revanche, lorsque vous utilisez le nœud **Réplication de la base de données** dans l'espace de travail **Surveillance** , vous pouvez également afficher l'état de réplication de la base de données d'un lien de réplication, puis accéder à l'outil Analyseur de lien de réplication, lequel peut vous aider à rechercher les problèmes de réplication.  



<!--HONumber=Nov16_HO1-->


