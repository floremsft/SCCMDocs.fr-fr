---
title: "Configurer la découverte | Microsoft Docs"
description: "Configurez les méthodes de découverte à exécuter sur un site Configuration Manager pour rechercher les ressources que vous pouvez gérer à partir de votre infrastructure réseau et d’Active Directory."
ms.custom: na
ms.date: 2/17/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 49505eb1-d44d-4121-8712-e0f3d8b15bf5
caps.latest.revision: 5
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 860815010068422f2d8854ed2d574c24cc386891
ms.openlocfilehash: 63a3c2ef66c80d1da9b50e67166a2196cf1b081b

---
# <a name="configure-discovery-methods-for-system-center-configuration-manager"></a>Configurer les méthodes de découverte pour System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*


Vous configurez les méthodes de découverte à exécuter sur un site System Center Configuration Manager pour rechercher les ressources que vous pouvez gérer à partir de votre infrastructure réseau et d’Active Directory. Pour cela, vous devez activer et configurer chaque méthode à utiliser pour explorer votre environnement. (Vous pouvez aussi désactiver une méthode en suivant la même procédure que pour l’activer.)  La découverte par pulsations d’inventaire et la découverte de serveur constituent les seules exceptions :  

-   Par défaut, la découverte par pulsations d’inventaire est déjà activée quand vous installez un site principal Configuration Manager et est configurée pour s’exécuter selon une planification de base. Il est recommandé de maintenir activée la découverte par pulsations d’inventaire, car cette méthode garantit que les enregistrements de données de découverte (DDR) des appareils sont à jour. Pour plus d’informations sur la découverte par pulsations d’inventaire, consultez [Découverte par pulsations d’inventaire](../../../../core/servers/deploy/configure/about-discovery-methods.md#bkmk_aboutHeartbeat).  

-   La découverte de serveur est une méthode automatique qui recherche les ordinateurs que vous utilisez comme systèmes de site. Elle n’est ni configurable ni désactivable.  

**Pour activer une méthode de découverte configurable :**  

1.  Dans la console Configuration Manager, cliquez sur **Administration** > **Configuration de la hiérarchie**, puis sur **Méthodes de découverte**.  

2.  Sélectionnez la méthode de découverte pour le site sur lequel vous voulez activer la découverte.  

3.  Dans l’onglet **Accueil** puis dans le groupe **Propriétés**, choisissez **Propriétés**. Ensuite, dans l’onglet **Général**, activez la case à cocher **Enable&lt;discovery method (Activer méthode de découverte)\>**.  

     Si cette case à cocher est déjà activée, vous pouvez la désélectionner pour désactiver la méthode de découverte.  

4.  Choisissez **OK** pour enregistrer la configuration.  


##  <a name="a-namebkmkconfigadforestdisca-configure-active-directory-forest-discovery"></a><a name="BKMK_ConfigADForestDisc"></a> Configurer la découverte de forêts Active Directory  
Pour finaliser la configuration de la découverte des forêts Active Directory, vous devez configurer des paramètres dans deux emplacements :  

-   Dans le nœud **Méthodes de découverte**, vous pouvez :

    - Activer cette méthode de découverte.
    - Définir un calendrier d’interrogation.
    - Indiquez si la découverte doit créer automatiquement des limites pour les sites Active Directory et les sous-réseaux qui sont découverts.  

-   Dans le nœud **Forêts Active Directory**, vous pouvez :

    - Ajouter les forêts à découvrir.
    - Activer la découverte des sites et sous-réseaux Active Directory dans cette forêt.
    - Configurer les paramètres permettant aux sites Configuration Manager de publier leurs informations de site dans la forêt.
    - Attribuer un compte à utiliser comme compte de forêt Active Directory pour chaque forêt.  

Utilisez les procédures suivantes pour activer la découverte de forêts Active Directory et configurer chaque forêt à utiliser avec la découverte de forêts Active Directory.  

#### <a name="to-enable-active-directory-forest-discovery"></a>Pour activer la découverte de forêts Active Directory  

1.  Dans la console Configuration Manager, choisissez **Administration** > **Configuration de la hiérarchie**, puis **Méthodes de découverte**.  

2.  Sélectionnez la méthode Découverte de forêts Active Directory pour le site sur lequel vous voulez configurer la découverte.  

3.  Sous l’onglet **Accueil**, dans le groupe **Propriétés**, choisissez **Propriétés**.  

4.  Dans l’onglet **Général**, activez la case à cocher pour activer la découverte. Vous pouvez aussi configurer la découverte maintenant et l’activer ultérieurement.  

5.  Spécifiez les options nécessaires pour créer des limites de site des emplacements découverts.  

6.  Spécifiez une planification du moment d'exécution de la découverte.  

7.  Après avoir terminé la configuration de la découverte de forêts Active Directory pour ce site, choisissez **OK** pour enregistrer la configuration.  

#### <a name="to-configure-a-forest-for-active-directory-forest-discovery"></a>Pour configurer une forêt pour la découverte de forêts Active Directory  

1.  Dans l’espace de travail **Administration**, choisissez **Forêts Active Directory**. Si la découverte de forêts Active Directory a été exécutée précédemment, vous pouvez voir chaque forêt découverte dans le volet des résultats. La forêt locale et toutes les forêts approuvées sont découvertes lorsque la Découverte de forêts Active Directory s'exécute. Seules les forêts non approuvées doivent être ajoutées manuellement.  

    -   Pour configurer une forêt déjà découverte, sélectionnez-la dans le volet de résultats. Ensuite, dans l’onglet **Accueil** et dans le groupe **Propriétés**, choisissez **Propriétés** pour ouvrir les propriétés de la forêt. Passez à l'étape 3.  

    -   Pour configurer une nouvelle forêt non répertoriée, dans l’onglet **Accueil** et dans le groupe **Créer**, choisissez **Ajouter une forêt** pour ouvrir la boîte de dialogue **Ajouter une forêt**. Passez à l'étape 3.  

2.  Dans l’onglet **Général**, finalisez la configuration de forêt que vous souhaitez découvrir et spécifiez le **Compte de forêt Active Directory**.  

    > [!NOTE]  
    >  La découverte de forêts Active Directory requiert un compte global pour découvrir et publier les forêts non approuvées. Si vous n’utilisez pas le compte d’ordinateur du serveur de site, vous ne pouvez sélectionner qu’un compte global.  

3.  Si vous prévoyez d’autoriser des sites à publier des données de site dans cette forêt, dans l’onglet **Publication**, terminez la configuration de la publication dans cette forêt.  

    > [!NOTE]  
    >  Si vous autorisez les sites à publier dans une forêt, vous devez étendre le schéma Active Directory de cette forêt à Configuration Manager. Le compte de forêt Active Directory doit avoir des autorisations Contrôle total sur le conteneur système dans cette forêt.  

4.  Lorsque vous terminez la configuration de cette forêt à utiliser avec la Découverte de forêts Active Directory, choisissez **OK** pour enregistrer la configuration.  

##  <a name="a-namebkmkconfigaddiscgenerala-configure-active-directory-discovery-for-computers-users-or-groups"></a><a name="BKMK_ConfigADDiscGeneral"></a> Configurer la découverte Active Directory pour les ordinateurs, les utilisateurs ou les groupes  
 Utilisez les informations des sections suivantes pour configurer la découverte des ordinateurs, des utilisateurs ou des groupes. Vous allez utiliser les méthodes de découverte suivantes :  

-   Découverte de groupes Active Directory  

-   Découverte de systèmes Active Directory  

-   Découverte d’utilisateurs Active Directory  

> [!NOTE]  
>  Les informations dans cette section ne s'appliquent pas à la découverte de forêts Active Directory.  

 Bien qu’indépendantes, ces méthodes de découverte partagent des options similaires. Pour plus d’informations sur ces options de configuration, consultez [Options partagées pour la découverte des groupes, systèmes et utilisateurs](../../../../core/servers/deploy/configure/about-discovery-methods.md#bkmk_shared).  

> [!WARNING]  
>  Le processus d'interrogation Active Directory par chacune de ces méthodes de découverte peut entraîner un trafic réseau important. Pensez à planifier l'exécution de chaque méthode de découverte à des moments où ce trafic ne risque pas de nuire à l'usage commercial de votre réseau.  

#### <a name="to-configure-active-directory-group-discovery"></a>Pour configurer la découverte de groupes Active Directory  

1.  Dans la console Configuration Manager, choisissez **Administration** > **Configuration de la hiérarchie**, puis **Méthodes de découverte**.  

2.  Sélectionnez la méthode **Découverte de groupes Active Directory** pour le site sur lequel vous voulez configurer la découverte.  

3.  Sous l’onglet **Accueil**, dans le groupe **Propriétés**, choisissez **Propriétés**.  

4.  Dans l’onglet **Général**, activez la case à cocher pour activer la découverte. Vous pouvez aussi configurer la découverte maintenant et l’activer ultérieurement.  

5.  Choisissez **Ajouter** pour configurer une étendue de découverte, sélectionnez **Groupes** ou **Emplacement**, puis terminez les configurations suivantes dans la boîte de dialogue **Ajouter des groupes** ou **Ajouter un emplacement Active Directory** :  

    1.  Spécifiez un **Nom** pour cette étendue de découverte.  

    2.  Spécifiez un **Domaine Active Directory** ou un **Emplacement** à rechercher :  

        -   Si vous avez choisi **Groupes**, spécifiez un ou plusieurs groupes Active Directory à découvrir.  

        -   Si vous avez choisi **Emplacement**, spécifiez un conteneur Active Directory comme emplacement à découvrir. Vous pouvez également activer une recherche récursive des conteneurs enfants Active Directory pour cet emplacement.  

    3.  Spécifiez le **Compte de découverte de groupes Active Directory** utilisé pour rechercher cette étendue de découverte.  

    4.  Choisissez **OK** pour enregistrer la configuration de l’étendue de découverte.  

6.  Répétez l'étape 6 pour chaque étendue de découverte supplémentaire à définir.  

7.  Dans l'onglet **Calendrier d'interrogation** , configurez le calendrier d'interrogation de découverte complet et la découverte delta.  

8.  Le cas échéant, dans l’onglet **Option**, vous pouvez configurer des options pour filtrer ou exclure les enregistrements d’ordinateur obsolètes de la découverte et découvrir les membres des groupes de distribution.  

    > [!NOTE]  
    >  Par défaut, le processus de découverte de groupes Active Directory ne découvre que l'appartenance aux groupes de sécurité.  

9. Après avoir terminé la configuration de la découverte des groupes Active Directory, choisissez **OK** pour enregistrer la configuration.  

#### <a name="to-configure-active-directory-system-discovery"></a>Pour configurer la découverte de systèmes Active Directory  

1.  Dans la console Configuration Manager, choisissez **Administration** > **Configuration de la hiérarchie**, puis **Méthodes de découverte**.  

2.  Sélectionnez la méthode pour le site sur lequel vous voulez configurer la découverte.  

3.  Sous l’onglet **Accueil**, dans le groupe **Propriétés**, choisissez **Propriétés**.  

4.  Dans l’onglet **Général**, activez la case à cocher pour activer la découverte. Vous pouvez aussi configurer la découverte maintenant et l’activer ultérieurement.  

5.  Choisissez l’icône **Nouveau** ![Icône Nouveau](media/Disc_new_Icon.gif) pour spécifier un nouveau conteneur Active Directory. Dans la boîte de dialogue **Conteneur Active Directory**, finalisez les configurations suivantes :  

    1.  Spécifiez un ou plusieurs emplacements à rechercher.  

    2.  Pour chaque emplacement, spécifiez les options qui modifient le comportement de la recherche.  

    3.  Pour chaque emplacement, spécifiez le compte à utiliser en tant que **Compte de découverte Active Directory**.  

        > [!TIP]  
        >  Pour chaque emplacement spécifié, vous pouvez configurer un ensemble d'options de découverte et un compte de découverte Active Directory unique.  

    4.  Choisissez **OK** pour enregistrer la configuration du conteneur Active Directory.  

6.  Dans l'onglet **Calendrier d'interrogation** , configurez le calendrier d'interrogation de découverte complet et la découverte delta.  

7.  Le cas échéant, dans l'onglet **Attributs Active Directory** , vous pouvez configurer des attributs Active Directory supplémentaires pour les ordinateurs à découvrir. Les attributs d'objets par défaut sont également répertoriés.  

8.  Le cas échéant, dans l’onglet **Option**, vous pouvez configurer des options pour filtrer ou exclure les enregistrements d’ordinateur obsolètes de la découverte.  

9. Après avoir terminé la configuration de la découverte de systèmes Active Directory pour ce site, choisissez **OK** pour enregistrer la configuration.  

#### <a name="to-configure-active-directory-user-discovery"></a>Pour configurer la découverte d'utilisateurs Active Directory  

1.  Dans la console Configuration Manager, choisissez **Administration** > **Configuration de la hiérarchie**, puis **Méthodes de découverte**.  

2.  Choisissez la méthode **Découverte d’utilisateurs Active Directory** pour le site sur lequel vous voulez configurer la découverte.  

3.  Sous l’onglet **Accueil**, dans le groupe **Propriétés**, choisissez **Propriétés**.  

4.  Dans l’onglet **Général**, activez la case à cocher pour activer la découverte. Vous pouvez aussi configurer la découverte maintenant et l’activer ultérieurement.  

5.  Choisissez l’icône **Nouveau** ![Icône Nouveau](media/Disc_new_Icon.gif) pour spécifier un nouveau conteneur Active Directory. Dans la boîte de dialogue **Conteneur Active Directory**, finalisez les configurations suivantes :  

    1.  Spécifiez un ou plusieurs emplacements à rechercher.  

    2.  Pour chaque emplacement, spécifiez les options qui modifient le comportement de la recherche.  

    3.  Pour chaque emplacement, spécifiez le compte à utiliser en tant que **Compte de découverte Active Directory**.  

        > [!NOTE]  
        >  Pour chaque emplacement spécifié, vous pouvez configurer un ensemble d'options de découverte et un compte de découverte Active Directory uniques.  

    4.  Choisissez **OK** pour enregistrer la configuration du conteneur Active Directory.  

6.  Dans l'onglet **Calendrier d'interrogation** , configurez le calendrier d'interrogation de découverte complet et la découverte delta.  

7.  Le cas échéant, dans l'onglet **Attributs Active Directory** , vous pouvez configurer des attributs Active Directory supplémentaires pour les ordinateurs à découvrir. Les attributs d'objets par défaut sont également répertoriés.  

8.  Après avoir terminé la configuration de la découverte d’utilisateurs Active Directory, choisissez **OK** pour enregistrer la configuration.  

##  <a name="a-namebkmkconfighbdisca-configure-heartbeat-discovery"></a><a name="BKMK_ConfigHBDisc"></a> Configurer la découverte par pulsations d’inventaire  
 Par défaut, la découverte par pulsations d’inventaire est activée au moment où vous installez un site principal Configuration Manager. Par conséquent, il vous suffit de configurer la fréquence selon laquelle les clients envoient l’enregistrement des données de la découverte par pulsations d’inventaire au point de gestion, si vous ne voulez pas utiliser la valeur par défaut (tous les sept jours).  

> [!NOTE]  
>  Si la tâche d'installation poussée du client et la tâche de maintenance de site pour **Remettre à zéro l'indicateur d'installation** sont activées sur le même site, définissez la planification de la découverte par pulsations d'inventaire à une valeur inférieure à la **Période de redécouverte client** de la tâche de maintenance de site **Remettre à zéro l'indicateur d'installation** . Pour plus d’informations sur les tâches de maintenance de site, consultez [Tâches de maintenance pour System Center Configuration Manager](../../../../core/servers/manage/maintenance-tasks.md).  

#### <a name="to-configure-the-heartbeat-discovery-schedule"></a>Pour configurer la planification de découverte par pulsations d'inventaire  

1.  Dans la console Configuration Manager, choisissez **Administration** > **Configuration de la hiérarchie**, puis **Méthodes de découverte**.  

2.  Sélectionnez **Découverte par pulsations d’inventaire** pour le site sur lequel vous souhaitez exécuter la découverte par pulsations d’inventaire.  

3.  Sous l’onglet **Accueil**, dans le groupe **Propriétés**, choisissez **Propriétés**.  

4.  Configurez la fréquence de l’envoi d’un enregistrement de données de découverte par pulsations d’inventaire par les clients, puis choisissez **OK** pour enregistrer la configuration.  

##  <a name="a-namebkmkconfignetworkdisca-configure-network-discovery"></a><a name="BKMK_ConfigNetworkDisc"></a> Configurer la découverte du réseau  
 Utilisez les informations dans les sections suivantes pour configurer la découverte du réseau.  

###  <a name="a-namebkmkaboutconfignetworkdisca-about-configuring-network-discovery"></a><a name="BKMK_AboutConfigNetworkDisc"></a> À propos de la configuration de la découverte du réseau  
 Avant de configurer la découverte du réseau, vous devez comprendre les points suivants :  

-   Niveaux disponibles de découverte du réseau  

-   Options disponibles de découverte du réseau  

-   Limitation de la découverte du réseau sur le réseau  

Pour plus d’informations, consultez la section [Découverte du réseau](../../../../core/servers/deploy/configure/about-discovery-methods.md#bkmk_aboutNetwork).  

 Les sections suivantes fournissent des informations sur les configurations courantes pour la découverte du réseau. Vous pouvez configurer une ou plusieurs de ces configurations pour l'utilisation pendant la même exécution de la découverte. Si vous utilisez plusieurs configurations, vous devez tenir compte des interactions pouvant affecter les résultats de la découverte.  

 Vous pouvez, par exemple, vouloir découvrir tous les appareils SNMP (Simple Network Management Protocol) qui utilisent un nom de communauté SNMP spécifique. De plus, vous pouvez désactiver la découverte sur un sous-réseau spécifique pour la même exécution de la découverte. Lors de l'exécution de la découverte, la découverte du réseau ne découvre pas les périphériques SNMP avec le nom de communauté spécifié sur le sous-réseau que vous avez désactivé.  

####  <a name="a-namebkmkdeterminenettopologya-determine-your-network-topology"></a><a name="BKMK_DetermineNetTopology"></a> Déterminer la topologie de votre réseau  
 La découverte pour la topologie uniquement vous permet de mapper votre réseau. Ce type de découverte ne découvre pas les clients potentiels. La découverte du réseau pour la topologie uniquement s'appuie sur SNMP.  

 Lors du mappage de la topologie de votre réseau, vous devez configurer le **Nombre maximal de sauts** dans l’onglet **SNMP** de la boîte de dialogue **Propriétés de la découverte du réseau**. Quelques sauts permettent de contrôler la bande passante du réseau utilisée lors de l'exécution de la découverte. À mesure que vous découvrez votre réseau, vous pouvez augmenter le nombre de sauts pour mieux comprendre la topologie de votre réseau.  

 Une fois que vous avez compris la topologie de votre réseau, vous pouvez configurer des propriétés supplémentaires permettant à la découverte du réseau de découvrir des clients potentiels et leurs systèmes d'exploitation, pendant que vous utilisez les configurations disponibles pour limiter le nombre de segments réseau que la découverte du réseau peut rechercher.  

####  <a name="a-namebkmklimitbysubneta-limit-searches-by-using-subnets"></a><a name="BKMK_LimitBySubnet"></a> Limiter les recherches en utilisant des sous-réseaux  
 Vous pouvez configurer la découverte du réseau pour rechercher des sous-réseaux spécifiques au cours d'une opération de découverte. Par défaut, la découverte du réseau recherche le sous-réseau du serveur qui exécute la découverte. Tous les sous-réseaux supplémentaires que vous configurez et activez ne s’appliquent qu’aux options de recherche SNMP et DHCP (Dynamic Host Configuration Protocol). Lorsque la découverte du réseau recherche les domaines, elle n'est pas limitée par les configurations des sous-réseaux.  

 Si vous spécifiez un ou plusieurs sous-réseaux dans l'onglet **Sous-réseaux** de la boîte de dialogue **Propriétés de la découverte du réseau** , la recherche s'applique uniquement aux sous-réseaux marqués **Activé** .  

 Lorsque vous désactivez un sous-réseau, il est exclu de la découverte, et les conditions suivantes s'appliquent :  

-   Les requêtes SNMP ne s’exécutent pas sur le sous-réseau.  

-   Les serveurs DHCP ne renvoient pas une liste des ressources situées sur le sous-réseau.  

-   Les requêtes basées sur le domaine peuvent découvrir des ressources situées sur le sous-réseau.  

####  <a name="a-namebkmksearchbydomaina-search-a-specific-domain"></a><a name="BKMK_SearchByDomain"></a> Rechercher dans un domaine spécifique  
 La découverte du réseau peut être configurée pour rechercher dans un domaine spécifique ou dans plusieurs domaines au cours d'une opération de découverte. Par défaut, la découverte du réseau recherche dans le domaine local du serveur qui exécute la découverte.  

 Si vous spécifiez un ou plusieurs domaines sous l'onglet **Domaines** de la boîte de dialogue **Propriétés de la découverte du réseau**, la recherche s'applique uniquement aux domaines marqués **Activé**.  

 Lorsque vous désactivez un domaine, il est exclu de la découverte, et les conditions suivantes s'appliquent :  

-   La découverte du réseau n’interroge pas les contrôleurs de domaine situés dans ce domaine.  

-   Les requêtes SNMP s’exécutent sur les sous-réseaux du domaine.  

-   Les serveurs DHCP renvoient toujours une liste des ressources situées dans le domaine.  

####  <a name="a-namebkmklimitbysnmpnamea-limit-searches-by-using-snmp-community-names"></a><a name="BKMK_LimitBySNMPname"></a> Limiter les recherches en utilisant des noms de communautés SNMP  
 La découverte du réseau peut être configurée pour rechercher une communauté SNMP spécifique ou plusieurs communautés au cours d'une opération de découverte. Par défaut, le nom de communauté dit **Public** est configuré pour l'utilisation.  

 La fonction de découverte du réseau utilise des noms de communautés pour accéder à des routeurs qui constituent des périphériques SNMP. Un routeur permet d'informer le service de découverte du réseau sur les autres routeurs et les sous-réseaux liés au premier routeur.  

> [!NOTE]  
>  Les noms de communautés SNMP sont semblables aux mots de passe. Le service de découverte du réseau peut uniquement obtenir des informations d'un périphérique SNMP pour lequel vous avez spécifié un nom de communauté. Chaque périphérique SNMP peut disposer de son propre nom de communauté mais souvent, plusieurs périphériques partagent le même nom de communauté. En outre, la plupart des périphériques SNMP disposent d'un nom de communauté par défaut dit **Public**. Toutefois, certaines organisations suppriment le nom de communauté **Public** de leurs appareils pour des raisons de sécurité.  

 Si plusieurs communautés SNMP s’affichent dans l’onglet **SNMP** de la boîte de dialogue **Propriétés de la découverte du réseau**, les recherches effectuées par la découverte du réseau s’effectuent dans l’ordre d’affichage des communautés. Afin de réduire l'impact sur le trafic réseau généré par les tentatives de contact avec un périphérique en utilisant différents noms, assurez-vous que les noms les plus fréquemment utilisés sont en haut de la liste.  

> [!NOTE]  
>  Outre le nom de communauté SNMP, vous pouvez spécifier l’adresse IP ou le nom pouvant être résolu d’un périphérique SNMP. Pour ce faire, utilisez l’onglet **Périphériques SNMP** de la boîte de dialogue **Propriétés de la découverte du réseau**.  

####  <a name="a-namebkmksearchbydhcpa-search-a-specific-dhcp-server"></a><a name="BKMK_SearchByDHCP"></a> Rechercher sur un serveur DHCP spécifique  
 La découverte du réseau peut être configurée pour utiliser un serveur DHCP spécifique ou plusieurs serveurs en vue de découvrir des clients DHCP au cours d'une opération de découverte.  

 La découverte du réseau recherche sur chaque serveur DHCP que vous spécifiez sous l'onglet **DHCP** de la boîte de dialogue **Propriétés de la découverte du réseau**. Si le serveur qui exécute la découverte loue son adresse IP à un serveur DHCP, vous pouvez configurer la découverte pour qu’elle effectue la recherche sur ce serveur DHCP en activant la case à cocher **Inclure le serveur DHCP pour lequel le serveur de site est configuré**.  

> [!NOTE]  
>  Pour configurer avec succès un serveur DHCP dans la découverte du réseau, votre environnement doit prendre en charge IPv4. Vous ne pouvez pas configurer la découverte du réseau de sorte qu'elle utilise un serveur DHCP dans un environnement IPv6 natif.  

###  <a name="a-namebkmkhowtoconfignetdisca-how-to-configure-network-discovery"></a><a name="BKMK_HowToConfigNetDisc"></a> Guide pratique pour configurer la découverte du réseau  
 Procédez comme suit pour d'abord découvrir uniquement la topologie de votre réseau, puis configurer la découverte du réseau afin de découvrir des clients potentiels à l'aide de l'une ou de plusieurs options disponibles de découverte du réseau.  

##### <a name="to-determine-your-network-topology"></a>Pour déterminer la topologie de votre réseau  

1.  Dans la console Configuration Manager, choisissez **Administration** > **Configuration de la hiérarchie**, puis **Méthodes de découverte**.  

2.  Choisissez **Découverte du réseau** pour le site sur lequel vous souhaitez exécuter la découverte du réseau.  

3.  Sous l’onglet **Accueil**, dans le groupe **Propriétés**, choisissez **Propriétés**.  

    -   Dans l’onglet **Général**, activez la case à cocher **Activer la découverte du réseau**, puis choisissez **Topologie** dans **Type de découverte**.  

    -   Dans l’onglet **Sous-réseaux**, activez la case à cocher **Rechercher les sous-réseaux locaux**.  

        > [!TIP]  
        >  Si vous connaissez les sous-réseaux qui constituent votre réseau, vous pouvez désactiver la case **Rechercher les sous-réseaux locaux** et utiliser l’icône **Nouveau** ![Icône Nouveau](media/Disc_new_Icon.gif) pour ajouter les sous-réseaux qui doivent faire l’objet de la recherche. Pour les réseaux de grande taille, il est souvent préférable d'effectuer la recherche uniquement dans un ou deux sous-réseaux à la fois, afin de minimiser l'utilisation de la bande passante du réseau.  

    -   Dans l’onglet **Domaines**, activez la case à cocher **Rechercher dans le domaine local**.  

    -   Dans l'onglet **SNMP** , utilisez la liste déroulante **Nombre maximal de sauts** pour déterminer le nombre de sauts de routeur que la découverte du réseau doit effectuer lors du mappage de votre topologie.  

        > [!TIP]  
        >  Lorsque vous mappez la topologie de votre réseau pour la première fois, configurez quelques sauts de routeur pour réduire l'utilisation de la bande passante du réseau.  

4.  Dans l’onglet **Calendrier**, choisissez l’icône **Nouveau** ![Icône Nouveau](media/Disc_new_Icon.gif) pour définir le calendrier d’exécution de la découverte du réseau.  

    > [!NOTE]  
    >  Vous ne pouvez pas attribuer une configuration de découverte différente à des planifications de découverte du réseau distinctes. La découverte du réseau utilise la configuration de découverte en cours à chaque exécution.  

5.  Choisissez **OK** pour accepter la configuration. La découverte du réseau s'exécute à l'heure planifiée.  

##### <a name="to-configure-network-discovery"></a>Pour configurer la découverte du réseau  

1.  Dans la console Configuration Manager, choisissez **Administration** > **Configuration de la hiérarchie**, puis **Méthodes de découverte**.  

2.  Choisissez **Découverte du réseau** pour le site sur lequel vous souhaitez exécuter la découverte du réseau.  

3.  Sous l’onglet **Accueil**, dans le groupe **Propriétés**, choisissez **Propriétés**.  

4.  Dans l’onglet **Général**, activez la case à cocher **Activer la découverte du réseau**, puis sélectionnez le type de découverte à exécuter dans **Type de découverte**.  

5.  Pour configurer la découverte afin de rechercher les sous-réseaux, cliquez sur l’onglet **Sous-réseaux**, puis configurez une ou plusieurs des options suivantes :  

    -   Pour lancer la découverte sur les sous-réseaux locaux de l’ordinateur exécutant la découverte, activez la case à cocher **Rechercher les sous-réseaux locaux**.  

    -   Pour rechercher un sous-réseau spécifique, celui-ci doit figurer dans la liste **Sous-réseaux à rechercher** et son paramètre **Rechercher** doit avoir pour valeur **Activé** :  

        1.  Si le sous-réseau ne figure pas dans la liste, choisissez l’icône **Nouveau** ![Icône Nouveau](media/Disc_new_Icon.gif). Dans la boîte de dialogue **Nouvelle attribution de sous-réseau**, renseignez les champs **Sous-réseau** et **Masque**, puis choisissez **OK**. Par défaut, un nouveau sous-réseau est activé pour la recherche.  

        2.  Pour modifier la valeur **Rechercher** d’un sous-réseau figurant dans la liste, sélectionnez-le, puis choisissez l’icône **Basculer** afin de remplacer la valeur **Désactivé** par la valeur **Activé** (ou inversement).  

6.  Pour configurer la découverte et rechercher les domaines, cliquez sur l’onglet **Domaines**, puis configurez une ou plusieurs des options suivantes :  

    -   Pour lancer la découverte sur le domaine de l’ordinateur exécutant la découverte, activez la case à cocher **Rechercher dans le domaine local**.  

    -   Pour rechercher un domaine spécifique, vérifiez que celui-ci figure dans la liste **Domaines** et que son paramètre **Rechercher** a pour valeur **Activé** :  

        1.  Si le domaine ne figure pas dans la liste, choisissez l’icône **Nouveau** ![Icône Nouveau](media/Disc_new_Icon.gif). Dans la boîte de dialogue **Propriétés de domaine**, renseignez le champ **Domaine**, puis choisissez **OK**. Par défaut, un nouveau domaine est activé pour la recherche.  

        2.  Pour modifier la valeur **Rechercher** d’un domaine figurant dans la liste, sélectionnez le domaine, puis choisissez l’icône **Basculer** afin de remplacer la valeur **Désactivé** par la valeur **Activé** (ou inversement).  

7.  Pour configurer la découverte afin de rechercher des noms de communautés SNMP, choisissez l’onglet **SNMP**, puis configurez une ou plusieurs des options suivantes :  

    -   Pour ajouter un nom de communauté SNMP dans la liste **Noms de communautés SNMP**, choisissez l’icône **Nouveau** ![Icône Nouveau](media/Disc_new_Icon.gif). Dans la boîte de dialogue **Nouveau nom de communauté SNMP**, indiquez le **Nom** de la communauté SNMP, puis choisissez **OK**.  

    -   Pour supprimer un nom de communauté SNMP, sélectionnez-le, puis choisissez l’icône **Supprimer** ![Icône Supprimer](media/Disc_delete_Icon.gif).  

    -   Pour modifier l’ordre de recherche des noms de communautés SNMP, sélectionnez un nom de communauté, puis choisissez l’icône **Déplacer l’élément vers le haut** ![Icône Déplacer l’élément vers le haut](media/Disc_moveUp_Icon.gif) ou **Déplacer l’élément vers le bas** ![Icône Déplacer l’élément vers le bas](media/Disc_moveDown_Icon.gif). Lors de l'exécution de la découverte, la recherche des noms de communauté est effectuée dans un ordre de haut en bas. Gardez à l’esprit les points suivants.

        > [!NOTE]  
        >  Le service de découverte du réseau utilise les noms des communautés SNMP pour accéder à des routeurs correspondant à des périphériques SNMP. Un routeur permet d'informer le service de découverte du réseau sur les autres routeurs et les sous-réseaux liés au premier routeur.  

        -   Les noms de communautés SNMP sont semblables aux mots de passe.  

        -   Le service de découverte du réseau peut uniquement obtenir des informations d'un périphérique SNMP pour lequel vous avez spécifié un nom de communauté.  

        -   Chaque périphérique SNMP peut disposer de son propre nom de communauté mais souvent, plusieurs périphériques partagent le même nom de communauté.  

        -   La plupart des périphériques SNMP ont un nom de communauté par défaut, qui est **Public**. Vous pouvez l’utiliser si vous n’en connaissez pas d’autres. Toutefois, certaines organisations suppriment le nom de communauté **Public** de leurs périphériques pour des raisons de sécurité.  

8.  Pour configurer le nombre maximal de sauts de routeur pour les recherches SNMP, choisissez l’onglet **SNMP**, puis sélectionnez le nombre maximal de sauts dans la liste déroulante **Nombre maximal de sauts**.  

9. Pour configurer un périphérique SNMP, choisissez l’onglet **Périphériques SNMP**. Si le périphérique ne figure pas dans la liste, choisissez l’icône **Nouveau** ![Icône Nouveau](media/Disc_new_Icon.gif). Dans la boîte de dialogue **Nouvelle unité SNMP**, tapez l’adresse IP ou le nom du périphérique SNMP, puis choisissez **OK**.  

    > [!NOTE]  
    >  Si vous spécifiez un nom de périphérique, Configuration Manager doit pouvoir résoudre le nom NetBIOS en adresse IP.  

10. Pour configurer la découverte afin d’interroger certains serveurs DHCP de clients DHCP, choisissez l’onglet **DHCP**, puis configurez une ou plusieurs des options suivantes :  

    -   Pour interroger le serveur DHCP sur l’ordinateur exécutant la découverte, activez la case à cocher **Always use the site server’s DHCP server (Toujours utiliser le serveur DHCP du serveur de site)**.  

        > [!NOTE]  
        >  Pour utiliser cette option, le serveur doit louer son adresse IP à un serveur DHCP, et il ne peut pas utiliser une adresse IP statique.  

    -   Pour interroger un serveur DHCP spécifique, choisissez l’icône **Nouveau** ![Icône Nouveau](media/Disc_new_Icon.gif). Dans la boîte de dialogue **Nouveau serveur DHCP**, entrez l’adresse IP ou le nom du serveur DHCP, puis choisissez **OK**.  

        > [!NOTE]  
        >  Si vous spécifiez un nom de serveur, Configuration Manager doit pouvoir résoudre le nom NetBIOS en adresse IP.  

11. Pour configurer à quel moment la découverte s’exécute, cliquez sur l’onglet **Calendrier**, puis choisissez l’icône **Nouveau** ![Icône Nouveau](media/Disc_new_Icon.gif) afin de définir le calendrier d’exécution de la découverte du réseau.  

     Vous pouvez configurer plusieurs calendriers récurrents et plusieurs calendriers non récurrents.  

    > [!NOTE]  
    >  Si plusieurs calendriers s’affichent dans l’onglet **Calendrier**, tous exécutent la découverte du réseau à l’heure indiquée. Cela s'applique également aux planifications périodiques.  

12. Choisissez **OK** pour enregistrer vos configurations.  

###  <a name="a-namebkmkhowtoverifynetdisca-how-to-verify-that-network-discovery-has-finished"></a><a name="BKMK_HowToVerifyNetDisc"></a> Guide pratique pour vérifier que la découverte du réseau est terminée  
 La durée d’exécution de la découverte du réseau peut varier selon plusieurs facteurs, dont un ou plusieurs des points suivants :  

-   Taille de votre réseau  

-   Topologie de votre réseau  

-   Nombre maximal de sauts configurés pour la recherche de routeurs sur le réseau  

-   Type de découverte en cours d'exécution  

La découverte du réseau ne génère pas de message d'alerte signalant qu'elle est terminée, vous devez donc le vérifier à l'aide de la procédure suivante.  

##### <a name="to-verify-that-network-discovery-has-finished"></a>Pour vérifier qu'une découverte du réseau est terminée  

1.  Dans la console Configuration Manager, choisissez **Surveillance**.  

2.  Dans l’espace de travail **Surveillance**, développez **État du système**, puis choisissez **Requêtes sur les messages d’état**.  

3.  Choisissez **All Status Messages (Tous les messages d’état)**.  

4.  Dans l’onglet **Accueil** puis dans le groupe **Requêtes sur les messages d’état**, choisissez **Afficher les messages**.  

5.  Dans la liste déroulante **Sélectionner la date et l’heure**, sélectionnez une valeur indiquant depuis combien de temps a démarré la découverte, puis choisissez **OK** pour ouvrir la boîte de dialogue **Afficheur des messages d’état de Configuration Manager**.  

    > [!TIP]  
    >  Vous pouvez également utiliser l'option **Spécifier la date et l'heure** pour sélectionner la date et l'heure auxquelles vous avez exécuté la découverte. Cette option s'avère utile si vous avez exécuté une découverte du réseau à une date donnée et que vous voulez récupérer uniquement les messages ayant été générés à cette date.  

6.  Pour valider que la découverte du réseau est terminée, recherchez un message d'état contenant les détails suivants :  

    -   ID de message : **502**  

    -   Composant : **SMS_NETWORK_DISCOVERY**  

    -   Description : **Ce composant s'est arrêté.**  

    Si ce message d'état ne s'affiche pas, la découverte de réseau n'est pas terminée.  

7.  Pour valider le moment de démarrage de la découverte du réseau, recherchez un message d'état contenant les détails suivants :  

    -   ID de message : **500**  

    -   Composant : **SMS_NETWORK_DISCOVERY**  

    -   Description : **Ce composant a démarré.**  

    Ces informations vérifient que la découverte du réseau a démarré. Si ces informations ne s'affichent pas, replanifiez une découverte du réseau.  



<!--HONumber=Feb17_HO3-->


