---
title: Planifier et configurer la gestion des applications | System Center Configuration Manager
description: "Implémentez et configurez les dépendances nécessaires au déploiement d’applications dans System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-app
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 2be84a1d-ebb9-47ae-8982-c66d5b92a52a
caps.latest.revision: 13
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: b1e21c2d6c90f02a1c616186b119b1a744d7f172


---
# <a name="plan-for-and-configure-application-management-in-system-center-configuration-manager"></a>Planifier et configurer la gestion des applications dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Consultez cette rubrique pour savoir comment implémenter les dépendances nécessaires au déploiement d’applications dans System Center Configuration Manager.  

## <a name="dependencies-external-to-configuration-manager"></a>Dépendances externes à Configuration Manager  

|Dépendance|Plus d'informations|  
|------------------|----------------------|  
|Internet Information Services (IIS) est nécessaire sur les serveurs de système de site qui exécutent le point du site web du catalogue des applications, le point de service web du catalogue des applications, le point de gestion et le point de distribution.|Pour plus d’informations sur cette condition, consultez [Configurations prises en charge](../../core/plan-design/configs/supported-configurations.md).|  
|Pour les appareils mobiles inscrits par Configuration Manager :|Lorsque vous signez le code d'applications en vue de les déployer sur des appareils mobiles, n'utilisez pas de certificat généré par un modèle de version 3 (**Windows Server 2008, Enterprise Edition**). Ce modèle de certificat crée un certificat qui n’est pas compatible avec les applications Configuration Manager pour appareils mobiles.<br /><br /> Si vous utilisez les services de certificat Active Directory pour signer le code des applications pour les applications d’appareils mobiles, n'utilisez pas de modèle de certificat de version 3.|  
|Les clients doivent être configurés pour auditer les événements d'ouverture de session si vous souhaitez créer automatiquement des affinités entre les utilisateurs et les appareils.|Configuration Manager lit les deux paramètres suivants dans la stratégie de sécurité locale des ordinateurs clients pour déterminer les affinités automatiques entre utilisateurs et appareils :<br /><br /> **Auditer les événements d'ouverture de session de compte**<br /><br /> **Auditer les événements d'ouverture de session**<br /><br /> Pour créer automatiquement des relations entre utilisateurs et appareils, vérifiez que ces deux paramètres sont activés sur les ordinateurs clients. Vous pouvez utiliser la stratégie de groupe Windows pour configurer ces paramètres.|  

## <a name="configuration-manager-dependencies"></a>Dépendances de Configuration Manager   

|Dépendance|Plus d'informations|  
|------------------|----------------------|  
|Point de gestion|Les clients contactent un point de gestion pour télécharger la stratégie client, localiser du contenu et se connecter au catalogue des applications.<br /><br /> Si les clients ne peuvent pas accéder à un point de gestion, ils ne peuvent pas utiliser le catalogue d'applications.|  
|Point de distribution|Pour que les applications puissent être déployées sur les clients, la hiérarchie doit contenir au moins un point de distribution. Par défaut, le serveur de site possède un rôle de système de site du point de distribution activé au cours d'une installation standard. Le nombre et l'emplacement des points de distribution dépendent des exigences propres à votre entreprise.<br /><br /> Pour plus d’informations sur l’installation des points de distribution et sur la gestion de contenu, consultez [Gérer le contenu et l’infrastructure de contenu](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).|  
|Paramètres du client|De nombreux paramètres client contrôlent la manière dont les applications sont installées sur le client, ainsi que l'expérience utilisateur offerte par ce dernier. En voici quelques-uns :<br /><br /> - Agent ordinateur<br /><br /> - Redémarrage de l’ordinateur<br /><br /> - Déploiement de logiciels<br /><br /> - Affinité entre utilisateur et périphérique<br /><br /> Pour plus d’informations sur ces paramètres client, consultez [À propos des paramètres client](../../core/clients/deploy/about-client-settings.md).<br /><br /> Pour plus d’informations sur la configuration des paramètres client, consultez [Guide pratique pour configurer les paramètres client dans Configuration Manager](../../core/clients/deploy/configure-client-settings.md).|  
|Pour le catalogue d'applications :<br /><br /> Comptes d'utilisateur découverts|Les utilisateurs doivent d’abord être découverts par Configuration Manager avant de pouvoir afficher et demander des applications du catalogue des applications. Pour plus d’informations, consultez [Exécuter la découverte](/sccm/core/servers/deploy/configure/run-discovery).|  
|Client App-V 4.6 SP1 ou version supérieure, pour l'exécution des applications virtuelles|Pour pouvoir créer des applications virtuelles dans Configuration Manager, les ordinateurs clients doivent disposer du client App-V 4.6 SP1 ou d’une version ultérieure.<br /><br /> Vous devez également mettre le client App-V à jour avec le correctif décrit dans l' [article 2645225](http://go.microsoft.com/fwlink/p/?LinkId=237322) de la base de connaissances avant de pouvoir déployer les applications virtuelles correctement.|  
|Point de service Web du catalogue des applications|Le point de service Web du catalogue des applications est un rôle de système de site qui fournit au site Web du catalogue des applications des informations sur les logiciels disponibles auprès de la bibliothèque de logiciels.<br /><br /> Pour plus d’informations sur la configuration de ce rôle de système de site, consultez [Configurer le Centre logiciel et le catalogue des applications](/sccm/apps/plan-design/plan-for-and-configure-application-management#configure-software-center-and-the-application-catalog-windows-pcs-only) dans cette rubrique.|  
|Point du site web du catalogue des applications|Le point du site Web du catalogue des applications est un rôle de système de site fournissant aux utilisateurs une liste des logiciels disponibles.<br /><br /> Pour plus d’informations sur la configuration de ce rôle de système de site, consultez [Configurer le Centre logiciel et le catalogue des applications](/sccm/apps/plan-design/plan-for-and-configure-application-management#configure-software-center-and-the-application-catalog-windows-pcs-only) dans cette rubrique.|  
|Point de Reporting Services|Pour pouvoir utiliser les rapports dans Configuration Manager pour la gestion d’applications, vous devez d’abord installer et configurer un point de Reporting Services.<br /><br /> Pour plus d’informations, consultez [Génération de rapports dans System Center Configuration Manager](../../core/servers/manage/reporting.md).|  
|Autorisations de sécurité pour la gestion d'applications|Pour pouvoir gérer des applications, vous devez disposer des autorisations de sécurité ci-dessous.<br /><br /> Le rôle de sécurité **Auteur d’application** intègre les autorisations mentionnées ci-dessus, qui sont nécessaires pour créer, modifier et mettre hors service des applications dans Configuration Manager.<br /><br /> **Pour déployer des applications :**<br /><br /> Le rôle de sécurité **Gestionnaire de déploiement d’application** intègre les autorisations mentionnées ci-dessus, qui sont nécessaires au déploiement d’applications dans Configuration Manager.<br /><br /> Le rôle de sécurité **Administrateur d'application** intègre toutes les autorisations des rôles de sécurité **Auteur d'application** et **Gestionnaire de déploiement d'application** .<br /><br /> Pour plus d’informations, consultez [Configurer l’administration basée sur des rôles](../../core/servers/deploy/configure/configure-role-based-administration.md).|  

##  <a name="configure-software-center-and-the-application-catalog-windows-pcs-only"></a>Configurer le Centre logiciel et le catalogue des applications (PC Windows uniquement)  

 Dans System Center Configuration Manager, les utilisateurs disposent désormais de deux options pour modifier les paramètres, rechercher et installer des applications :  

-   **Le nouveau Centre logiciel** : le nouveau Centre logiciel été modernisé et les applications qui seraient apparues uniquement dans le catalogue d’applications dépendant de Silverlight (applications accessibles à l’utilisateur) figurent désormais dans le Centre logiciel sous l’onglet **Applications** . Il est toujours possible d’accéder au catalogue d’applications via le lien situé sous l’onglet **État de l’installation** du Centre logiciel.  

     Vous pouvez faire en sorte que les clients utilisent le nouveau Centre logiciel en activant le paramètre client **Agent ordinateur** > **Utiliser le nouveau Centre logiciel**.  

    > [!IMPORTANT]  
    >  Même si les utilisateurs finals n’ont plus besoin de se connecter au catalogue des applications, vous devez quand même configurer le point du site web du catalogue des applications et le point de service web du catalogue des applications comme indiqué ci-dessous.  

-   **Le Centre logiciel précédent et le catalogue des applications** : par défaut, les utilisateurs continuer de se connecter à la précédente version du Centre logiciel et au catalogue des applications (moyennant un navigateur web compatible Silverlight) pour parcourir les applications disponibles.  

 Quelle que soit la version que vous choisissez d’utiliser, le Centre logiciel est installé automatiquement pendant l’installation du client Configuration Manager sur les PC Windows.  

> [!TIP]  
>  La version du Centre logiciel auxquels ont accès les utilisateurs varie en fonction des paramètres du client Configuration Manager. Vous avez ainsi tout le loisir de choisir la version qui sera utilisée à partir des paramètres client personnalisés que vous déployez sur le regroupement.  

## <a name="steps-to-install-and-configure-the-application-catalog-and-software-center"></a>Installation et configuration du catalogue des applications et du Centre logiciel  

> [!IMPORTANT]  
>  Avant d’effectuer cette procédure, vérifiez que vous respectez toutes les conditions préalables répertoriées ci-dessus.  

|Étapes|Détails|Plus d'informations|  
|-----------|-------------|----------------------|  
|**Étape 1 :** si vous souhaitez utiliser des connexions HTTPS, assurez-vous d'avoir déployé un certificat de serveur web sur les serveurs de système de site.|Déployez un certificat de serveur Web sur les serveurs de système de site qui exécuteront le point de site Web du catalogue d'applications et le point de service Web du catalogue d'applications.<br /><br /> De plus, si vous souhaitez que les clients puissent accéder au catalogue d'applications depuis Internet, déployez un certificat de serveur Web vers au moins un serveur de système de site du point de gestion et configurez-le pour les connexions client depuis Internet.|Pour plus d’informations sur la configuration requise pour les certificats, consultez [Configuration requise pour les certificats PKI](../../core/plan-design/network/pki-certificate-requirements.md).|  
|**Étape 2 :** si vous souhaitez utiliser un certificat client PKI pour les connexions à des points de gestion, déployez un certificat d'authentification client sur les ordinateurs clients.|Même si les clients ne disposent pas d'un certificat client PKI pour se connecter au catalogue d'applications, ils doivent se connecter à un point de gestion afin d'utiliser le catalogue d'applications. Vous devez déployer un certificat d'authentification client sur les ordinateurs clients dans les cas suivants :<br /><br /> - Les points de gestion sur l’intranet acceptent uniquement les connexions client HTTPS.<br /><br /> - Les clients se connecteront au catalogue des applications à partir d’Internet.|Pour plus d’informations sur la configuration requise pour les certificats, consultez [Configuration requise pour les certificats PKI](../../core/plan-design/network/pki-certificate-requirements.md).|  
|**Étape 3 :** installez et configurez le point de service web du catalogue d'applications et le site web du catalogue d'applications.|Vous devez installer ces deux rôles de système de site sur le même site. Vous n'êtes pas obligé de les installer sur le même serveur de système de site ni dans la même forêt Active Directory. Toutefois, le point de service Web du catalogue d'applications doit se trouver dans la même forêt que la base de données du site.|Pour plus d’informations sur le positionnement des rôles de système de site, consultez [Planifier des serveurs de système de site et des rôles de système de site](../../core/plan-design/hierarchy/plan-for-site-system-servers-and-site-system-roles.md).<br /><br /> Pour configurer le point de service web du catalogue des applications et le point du site web du catalogue des applications, consultez **Étape 3 : installation et configuration des rôles de système de site du catalogue des applications**.|  
|**Étape 4 :** configurez les paramètres client pour le catalogue des applications et le Centre logiciel.|Configurez les paramètres client par défaut si vous souhaitez que tous les utilisateurs aient le même paramètre. Vous pouvez aussi configurer des paramètres client personnalisés pour des regroupements spécifiques.|Pour plus d’informations sur les paramètres client, consultez [À propos des paramètres client](../../core/clients/deploy/about-client-settings.md).<br /><br /> Pour plus d’informations sur la configuration de ces paramètres client, consultez **Étape 4 : configuration des paramètres client pour le catalogue des applications et le Centre logiciel**.|  
|**Étape 5 :** vérifiez que le catalogue des applications est opérationnel.|Vous pouvez accéder au catalogue d'applications directement à partir d'un navigateur ou du Centre logiciel.|Voir **Étape 5 : vérifier que le catalogue des applications est opérationnel**.|  

## <a name="supplemental-procedures-to-install-and-configure-the-application-catalog-and-software-center"></a>Procédures supplémentaires d'installation et de configuration du catalogue des applications et du Centre logiciel  
 Utilisez les informations suivantes lorsque les étapes décrites dans le tableau précédent nécessitent des procédures supplémentaires.  

###  <a name="step-3-installing-and-configuring-the-application-catalog-site-system-roles"></a>Étape 3 : installation et configuration des rôles de système de site du catalogue des applications  
 Ces procédures configurent les rôles de système de site pour le catalogue d'applications. Selon que vous voulez installer un nouveau serveur de système de site ou utiliser un serveur de système de site existant, suivez l’une des deux procédures suivantes :  

> [!NOTE]  
>  Le catalogue d'applications ne peut pas être installé sur un site secondaire ni sur un site d'administration centrale.  

####  <a name="to-install-and-configure-the-application-catalog-site-systems-new-site-system-server"></a>Pour installer et configurer les systèmes de site du catalogue d'applications : Nouveau serveur de système de site  

1.  Dans la console Configuration Manager, cliquez sur **Administration** > **Configuration du site** > **Serveurs et rôles de système de site**.  

3.  Sur l'onglet **Accueil** , dans le groupe **Créer** , cliquez sur **Créer un serveur de système de site**.  

4.  Sur la page **Général** , spécifiez les paramètres généraux du système de site, puis cliquez sur **Suivant**.  

    > [!TIP]  
    >  Si vous souhaitez que les ordinateurs clients puissent accéder au catalogue des applications via Internet, spécifiez le nom de domaine complet Internet.  

5.  Sur la page **Sélection du rôle de système** , sélectionnez **Point de service Web du catalogue des applications** et **Point du site Web du catalogue des applications** dans la liste des rôles disponibles, puis cliquez sur **Suivant**.  

6.  Effectuez toutes les étapes de l'Assistant.  

####  <a name="to-install-and-configure-the-application-catalog-site-systems-existing-site-system-server"></a>Pour installer et configurer les systèmes de site du catalogue d'applications : Serveur de système de site existant  

1.  Dans la console Configuration Manager, cliquez sur **Administration** > **Configuration du site** > **Serveurs et rôles de système de site**, puis sélectionnez le serveur à utiliser pour le catalogue des applications.  

3.  Sous l'onglet **Accueil** , dans le groupe **Créer** , cliquez sur **Ajouter des rôles de système de site**.  

4.  Sur la page **Général** , spécifiez les paramètres généraux du système de site, puis cliquez sur **Suivant**.  

    > [!TIP]  
    >  Si vous souhaitez que les ordinateurs clients puissent accéder au catalogue des applications via Internet, spécifiez le nom de domaine complet Internet.  

5.  Sur la page **Sélection du rôle de système** , sélectionnez **Point de service Web du catalogue des applications** et **Point du site Web du catalogue des applications** dans la liste des rôles disponibles, puis cliquez sur **Suivant**.  

6.  Effectuez toutes les étapes de l'Assistant.  

 Vérifiez l'installation de ces rôles de système de site à l'aide de messages d'état et en examinant les fichiers journaux :  

1.  Messages d'état : Utiliser les composants **SMS_PORTALWEB_CONTROL_MANAGER** et **SMS_AWEBSVC_CONTROL_MANAGER**.  

     Par exemple, l'ID d'état **1015** pour **SMS_PORTALWEB_CONTROL_MANAGER** confirme que le Gestionnaire de composants de site a correctement installé le point de site Web du catalogue des applications.  

2.  Fichiers journaux : Rechercher **SMSAWEBSVCSetup.log** et **SMSPORTALWEBSetup.log**.  

     Pour plus d'informations, recherchez les fichiers journaux **awebsvcMSI.log** et **portlwebMSI.log**.  

###  <a name="step-4-configuring-the-client-settings-for-the-application-catalog-and-software-center"></a>Étape 4 : configuration des paramètres client pour le catalogue des applications et le Centre logiciel  
 Cette procédure configure les paramètres client par défaut qui s'appliqueront au catalogue des applications et au Centre logiciel pour l'ensemble des appareils de la hiérarchie. Si vous voulez appliquer ces paramètres à une sélection d'appareils uniquement, créez un paramètre client personnalisé et déployez-le sur un regroupement qui contient les appareils qui auront les paramètres spécifiques. Pour plus d'informations sur la création d'un paramètre d’appareil personnalisé, voir la section [Comment créer et déployer des paramètres client personnalisés](../../core/clients/deploy/configure-client-settings.md#BKMK_CustomClientSettings) dans la rubrique [Guide pratique pour configurer les paramètres client dans System Center Configuration Manager](../../core/clients/deploy/configure-client-settings.md) .  

1.  Dans la console Configuration Manager, cliquez sur **Administration** > **Paramètres client** > **Paramètres client par défaut**.  

3.  Dans l'onglet **Accueil** , dans le groupe **Propriétés** , cliquez sur **Propriétés**.  

4.  Consultez et configurez les paramètres relatifs aux notifications utilisateur, au catalogue d'applications et au Centre logiciel. Exemple :  

    1.  Groupe**Agent ordinateur** :  

        -   **Point de site Web du catalogue d'applications par défaut**  

        -   **Ajoute un site Web du catalogue d'applications par défaut à la zone des sites de confiance d'Internet Explorer**  

        -   **Nom d'organisation affiché dans le Centre logiciel**  

            > [!TIP]  
            >  Pour définir le nom d'organisation affiché dans le catalogue des applications et configurer le thème du site Web, utilisez l'onglet **Personnalisation** des propriétés de site Web du catalogue des applications.  

        -   **Utiliser le nouveau Centre logiciel** : choisissez la valeur **Oui** si vous voulez utiliser le nouveau Centre logiciel. Celui-ci permet aux utilisateurs finals d’effectuer des recherches parmi les applications disponibles et de les installer sans avoir à accéder au catalogue des applications (ce qui nécessite un navigateur web compatible Silverlight).  

        -   **Autorisations d'installation**  

        -   **Afficher les notifications de nouveaux déploiements**  

    2.  Groupe**Gestion de l'alimentation** :  

        -   **Autoriser les utilisateurs à exclure leur appareil de la gestion de l'alimentation**  

    3.  Groupe**Outils de contrôle à distance** :  

        -   **Les utilisateurs peuvent modifier les paramètres de stratégie ou de notification dans le Centre logiciel**  

    4.  Groupe**Affinité entre utilisateur et périphérique** :  

        -   **Autoriser les utilisateurs à définir leurs périphériques principaux**  

    > [!NOTE]  
    >  Pour plus d'informations sur les paramètres client, voir [À propos des paramètres client dans System Center Configuration Manager](../../core/clients/deploy/about-client-settings.md).  

5.  Cliquez sur **OK** pour fermer la boîte de dialogue **Paramètres client par défaut** .  

 Les ordinateurs client sont configurés avec ces paramètres lorsqu'ils téléchargent la stratégie client. Pour lancer la récupération de stratégie pour un seul client, consultez [Guide pratique pour gérer les clients](../../core/clients/manage/manage-clients.md).  

###  <a name="step-5-verify-that-the-application-catalog-is-operational"></a>Étape 5 : vérifier que le catalogue des applications est opérationnel  
 Utilisez les procédures suivantes pour vérifier que le catalogue d'applications est opérationnel. Vous pouvez accéder au catalogue d'applications directement à partir d'un navigateur ou du Centre logiciel.  

> [!NOTE]  
>  Le catalogue des applications nécessite Microsoft Silverlight, qui est automatiquement installé comme prérequis pour le client Configuration Manager. Si vous accédez au catalogue des applications directement à partir d’un navigateur sur un ordinateur dépourvu du client Configuration Manager, commencez par vérifier que Microsoft Silverlight est installé sur l’ordinateur.  

> [!TIP]  
>  L'absence de composants requis fait partie des causes les plus fréquentes de dysfonctionnements du catalogue des applications après l'installation. Vérifiez la configuration requise en matière de rôles de système de site pour les rôles de système de site du catalogue des applications. Vous pouvez pour cela vous aider de la rubrique [Configurations prises en charge](../../core/plan-design/configs/supported-configurations.md).  

> [!NOTE]  
>  Si vous êtes connecté avec un compte d’administrateur de domaine, les messages de notification en provenance du client Configuration Manager (par exemple, les messages indiquant que de nouveaux logiciels sont disponibles) ne s’affichent pas.  

### <a name="to-access-the-application-catalog-directly-from-a-browser"></a>Pour accéder au catalogue d'applications directement depuis un navigateur  

-   Dans un navigateur, tapez l'adresse du site Web du catalogue des applications et vérifiez que la page Web s'affiche et qu'elle contient trois onglets : **Catalogue d'applications**, **Mes demandes d'application**et **Mes périphériques**.  

     Sélectionnez et utilisez l’adresse adéquate indiquée ci-dessous pour le catalogue d’applications, où <serveur\> est le nom de l’ordinateur, le nom de domaine complet de l’intranet ou le nom de domaine complet Internet :  

    -   Connexions clientes HTTPS et paramètres de rôle de système de site par défaut : **https://<serveur\>/CMApplicationCatalog**  

    -   Connexions clientes HTTP et paramètres de rôle de système de site par défaut : **http://<serveur\>/CMApplicationCatalog**  

    -   Connexions clientes HTTPS et paramètres de rôle de système de site personnalisés : **https://<serveur\>:<port\>/<nom_application_web>\>**  

    -   Connexions clientes HTTP et paramètres de rôle de système de site personnalisés : **http://<serveur\>:<port\>/<nom_application_web\>**  

### <a name="to-access-the-application-catalog-from-software-center-does-not-apply-to-the-new-version-of-software-center"></a>Pour accéder au catalogue des applications à partir du Centre logiciel (ne s’applique pas à la nouvelle version du Centre logiciel)  

1.  Sur un ordinateur client, cliquez sur **Démarrer** > **Tous les programmes** > **Microsoft System Center 2012** > **Configuration Manager** > **Centre logiciel**.  

2.  Si vous avez précédemment configuré un nom d'organisation en tant que paramètre client pour le Centre logiciel, vérifiez qu'il s'affiche comme prévu.  

3.  Cliquez sur **Rechercher d'autres applications à partir du catalogue des applications** et confirmez que la page s'affiche avec les trois onglets : **Catalogue d'applications**, **Mes demandes d'application**et **Mes périphériques**.  

> [!WARNING]  
>  Après avoir installé les rôles de système de site du catalogue d'applications, celui-ci ne sera pas immédiatement visible après avoir cliqué sur le lien **Rechercher d'autres applications à partir du catalogue des applications** du Centre logiciel. Le catalogue d'applications n'est disponible depuis le Centre logiciel qu'une fois que le client a téléchargé sa stratégie client ou jusqu'à 25 heures après l'installation des rôles de système de site du catalogue d'applications.  



<!--HONumber=Nov16_HO1-->


