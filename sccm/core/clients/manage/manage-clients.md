---
title: "Gérer les clients | System Center Configuration Manager"
description: "Découvrez comment gérer les clients dans System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3986a992-c175-4b6f-922e-fc561e3d7cb7
caps.latest.revision: 17
author: Mtillman
ms.author: mtillman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: f777295958e9cbc729e3759d354521c96ae3e8ac
ms.openlocfilehash: 67a814330123a1615a0663872bf4af64e5b81a84


---
# <a name="how-to-manage-clients-in-system-center-configuration-manager"></a>Guide pratique pour gérer les clients dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Une fois qu’un client System Center Configuration Manager a été installé et attribué à un site Configuration Manager, l’appareil est affiché dans l’espace de travail **Ressources et Conformité** du nœud **Appareils**, ainsi que dans un ou plusieurs regroupements du nœud **Regroupements d’appareils**. Lorsque vous sélectionnez le périphérique ou le regroupement qui contient le périphérique, vous pouvez sélectionner plusieurs opérations de gestion. Toutefois, il existe d’autres manières de gérer le client, pouvant impliquer d’autres espaces de travail dans la console ou des tâches qui n’utilisent pas la console Configuration Manager.  

 Cette rubrique contient des informations générales sur les tâches de gestion d’un client Configuration Manager effectuées à partir de l’espace de travail **Ressources et Conformité**, ainsi que des informations plus détaillées sur d’autres tâches qui facilitent la gestion du client Configuration Manager. Pour plus d’informations sur la configuration du client, consultez [Guide pratique pour configurer les paramètres client dans System Center Configuration Manager](../../../core/clients/deploy/configure-client-settings.md)  

> [!NOTE]  
>  Il arrive qu’un client Configuration Manager installé ne s’affiche pas dans la console Configuration Manager. Cela peut être le cas si le client n’a pas encore été attribué à un site, si la console doit être actualisée ou si une appartenance au regroupement doit être mise à jour.  
>   
>  De plus, un appareil peut s’afficher dans la console quand le client Configuration Manager n’est pas installé. Cela peut se produire si l’appareil a été découvert, mais que le client Configuration Manager n’est pas installé ni attribué. Les appareils mobiles gérés à l’aide du connecteur Exchange Server n’installent pas le client Configuration Manager. Les appareils inscrits par Microsoft Intune ne l’installent pas non plus.  
>   
>  Examinez la colonne **Client** dans la console Configuration Manager pour savoir si le client Configuration Manager est installé et si vous pouvez donc le gérer à partir de la console Configuration Manager.  

##  <a name="a-namebkmkmanagingclientsdevicesnodea-manage-clients-from-the-devices-node"></a><a name="BKMK_ManagingClients_DevicesNode"></a> Gérer les clients à partir du nœud Appareils  
 La procédure et le tableau ci-après permettent de gérer un ou plusieurs périphériques à partir du nœud **Périphériques** de l'espace de travail **Ressources et Conformité** .  

> [!IMPORTANT]  
>  Selon le type de périphérique, certaines de ces options peuvent ne pas être disponibles.  

#### <a name="to-manage-clients-from-the-devices-node"></a>Pour gérer les clients à partir du nœud Périphériques  

1.  Dans la console Configuration Manager, cliquez sur **Ressources et Conformité**.  

2.  Dans l'espace de travail **Ressources et Conformité** , cliquez sur **Périphériques**.  

3.  Sélectionnez un ou plusieurs appareils, puis sélectionnez l’une des tâches de gestion du client disponibles dans le ruban ou en cliquant avec le bouton droit sur l’appareil :  

    -   **Gérer les informations relatives à l'affinité entre périphérique et utilisateur**  

         Permet de configurer les associations entre les utilisateurs et les appareils, ce qui vous permet de déployer efficacement des logiciels vers des utilisateurs.  

         Consultez [Lier des utilisateurs et des appareils avec l’affinité entre utilisateur et appareil dans System Center Configuration Manager](../../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md)  

    -   **Ajouter l’appareil à un regroupement nouveau ou existant**  

         Utilisez ces actions liées au regroupement pour ajouter rapidement l’appareil sélectionné à un regroupement à l'aide d'une règle directe.  

         [Opérations et maintenance pour les regroupements dans System Center Configuration Manager](../../../core/clients/manage/collections/operations-and-maintenance-for-collections.md)  

    -   **Installer et réinstaller le client à l'aide de l'Assistant Installation poussée du client**  

         L’Assistant Installation push du client est une méthode simple pour installer ou réinstaller le client Configuration Manager, pour pouvoir ensuite le réparer ou le reconfigurer sur des ordinateurs Windows en utilisant des options de configuration de site et des propriétés client.msi supplémentaires que vous avez spécifiées pour l’installation push du client.  

        > [!TIP]  
        >  Vous avez le choix entre plusieurs méthodes d’installation (et de réinstallation) du client Configuration Manager. L'Assistant Installation poussée du client constitue une méthode pratique d'installation du client depuis la console, mais cette méthode possède de nombreuses dépendances et n'est pas adaptée à tous les environnements. Si vous ne pouvez pas installer correctement le client à l'aide de l'installation poussée du client, d'autres méthodes d'installation du client sont disponibles. Pour plus d’informations sur les dépendances, consultez [Configuration requise pour le déploiement de clients sur des ordinateurs Windows dans System Center Configuration Manager](../../../core/clients/deploy/prerequisites-for-deploying-clients-to-windows-computers.md). Pour plus d’informations sur les autres méthodes d’installation de clients, consultez [Méthodes d’installation de clients dans System Center Configuration Manager](../../../core/clients/deploy/plan/client-installation-methods.md).  

         Consultez [Comment installer des clients Configuration Manager à l'aide de l'installation poussée du client](../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientPush).  

    -   **Réaffecter le site**  

         Vous pouvez réaffecter un ou plusieurs clients, notamment des appareils mobiles gérés, à un autre site principal de la hiérarchie. Les clients peuvent être réattribués individuellement ou tous sélectionnés et réattribués en bloc à un nouveau site.  

    -   **Administrer le client à distance**  

         Vous pouvez exécuter l'Explorateur de ressources pour afficher les informations d'inventaire matériel et logiciel d'un client Windows et les administrer à distance à l'aide du contrôle à distance, de l'assistance à distance ou du Bureau à distance.  

         Consultez [Comment utiliser l’Explorateur de ressources pour afficher l’inventaire matériel dans System Center Configuration Manager](../../../core/clients/manage/inventory/use-resource-explorer-to-view-hardware-inventory.md) et [Comment utiliser l’Explorateur de ressources pour afficher l’inventaire logiciel dans System Center Configuration Manager](../../../core/clients/manage/inventory/use-resource-explorer-to-view-software-inventory.md).  

         Consultez [Comment administrer à distance un ordinateur client Windows à l’aide de System Center Configuration Manager](../../../core/clients/manage/remote-control/remotely-administer-a-windows-client-computer.md).  

    -   **Approuver un client**  

         Lorsque le client communique avec les systèmes de site à l'aide de HTTP et d'un certificat auto-signé, vous devez approuver ces clients pour les identifier en tant qu'ordinateurs approuvés. Par défaut, la configuration du site approuve automatiquement les clients de la même forêt Active Directory et de forêts approuvées pour vous éviter d'approuver manuellement chaque client. Toutefois, vous devez approuver manuellement les ordinateurs du groupe de travail auxquels vous faites confiance et tous les autres ordinateurs auxquels vous faites confiance, mais qui ne sont pas approuvés.  

        > [!WARNING]  
        >  Certaines fonctions de gestion peuvent fonctionner pour les clients non approuvés, mais ce scénario n’est pas pris en charge pour Configuration Manager.  

         Vous ne devez pas approuver les clients qui communiquent toujours avec les systèmes de site à l'aide du protocole HTTPS au lieu de HTTP, ou les clients qui utilisent un certificat PKI lorsqu'ils communiquent avec les systèmes de site à l'aide du protocole HTTP. Ces clients établissent une relation de confiance avec Configuration Manager à l’aide des certificats PKI.  

    -   **Bloquer ou débloquer un client**  

         Bloquez un client auquel vous ne faites plus confiance pour l’empêcher de recevoir la stratégie client et empêcher les systèmes de site Configuration Manager de communiquer avec lui.  

        > [!WARNING]  
        >  Le fait de bloquer un client empêche les communications entre le client et les systèmes de site Configuration Manager uniquement. Cela n’empêche pas les communications avec d’autres appareils. De plus, lorsque le client communique avec des systèmes de site à l'aide du protocole HTTP au lieu de HTTPS, certaines contraintes de sécurité se présentent.  

         Si vous changez d'avis ultérieurement, vous pouvez débloquer un client qui a été bloqué. Toutefois, après avoir débloqué un ordinateur basé sur AMT Intel configuré pour AMT lorsqu'il était bloqué, vous devez exécuter des étapes supplémentaires pour pouvoir le gérer hors bande de nouveau.  

         Consultez [Déterminer si des clients doivent être bloqués dans System Center Configuration Manager](../../../core/clients/deploy/plan/determine-whether-to-block-clients.md).  

    -   **Effacer un déploiement PXE requis**  

         Cette option permet de redéployer les déploiements PXE requis pour l'ordinateur sélectionné.  

         Consultez [Utiliser PXE pour déployer Windows sur le réseau avec System Center Configuration Manager](../../../osd/deploy-use/use-pxe-to-deploy-windows-over-the-network.md).  

    -   **Gérer les propriétés du client**  

         Vous pouvez afficher les données de découverte et les déploiements ciblés pour le client. Vous pouvez également configurer des variables qui sont utilisées par les séquences de tâches pour déployer un système d'exploitation vers le périphérique.  

    -   **Supprimer le client**  

        > [!WARNING]  
        >  Ne supprimez pas un client si vous souhaitez désinstaller le client Configuration Manager ou le supprimer d’un regroupement.  

         L’action **Supprimer** permet de supprimer manuellement l’enregistrement client de la base de données Configuration Manager. En général, cette action est utilisée dans les scénarios de dépannage. Si vous supprimez l’enregistrement client, mais que le client Configuration Manager est toujours installé et communique avec Configuration Manager, la découverte par pulsations d’inventaire recrée l’enregistrement client, qui réapparaît dans la console Configuration Manager, mais sans l’historique du client et les associations précédentes.  

        > [!NOTE]  
        >  Si vous supprimez un client d’appareil mobile inscrit par Configuration Manager, cette action révoque également le certificat PKI émis pour l’appareil mobile. Ce certificat est alors rejeté par le point de gestion, même si IIS ne vérifie pas la liste de révocation de certificats. Les certificats sur les clients hérités d'appareils mobiles ne sont pas révoqués lorsque vous supprimez ces clients.  

         Pour désinstaller le client, voir [Désinstaller le client Configuration Manager](#BKMK_UninstalClient).  

         Pour affecter le client à un nouveau site principal, consultez [Comment affecter des clients à un site dans System Center Configuration Manager](../../../core/clients/deploy/assign-clients-to-a-site.md).  

         Pour supprimer le client d'un regroupement, reconfigurez les propriétés du regroupement. Consultez [Comment gérer des regroupements dans System Center Configuration Manager](../../../core/clients/manage/collections/manage-collections.md).  

    -   **Réinitialiser un appareil mobile**  

         Vous pouvez réinitialiser les appareils mobiles qui prennent en charge la commande de réinitialisation.  

         Cette action supprime définitivement toutes les données sur l'appareil mobile, y compris les paramètres et données personnels. En général, cette action rétablit les paramètres par défaut de l'appareil mobile. Réinitialisez un appareil mobile lorsque vous ne lui faites plus confiance; par exemple, s'il a été perdu ou volé.  

        > [!TIP]  
        >  Consultez la documentation du fabricant pour obtenir plus d’informations sur la façon dont l’appareil mobile traite les commandes de réinitialisation à distance.  

         Lorsque vous envoyez une demande de réinitialisation, l'appareil mobile reçoit la commande de réinitialisation avec un délai :  

        -   Si l’appareil mobile est inscrit par Configuration Manager ou Microsoft Intune, le client reçoit la commande de réinitialisation lors du prochain téléchargement de sa stratégie client.  

        -   Si l'appareil mobile est géré par le connecteur Exchange Server, il reçoit la commande de réinitialisation lors de la prochaine synchronisation avec Exchange.  

         Vous pouvez utiliser la colonne **État de réinitialisation** pour surveiller quand l'appareil mobile reçoit la commande de réinitialisation. Vous pouvez annuler cette commande tant que l’appareil mobile n’a pas envoyé d’accusé de réception de la réinitialisation à Configuration Manager.  

    -   **Mettre hors service un appareil mobile**  

         L’option **Mettre hors service** est prise en charge uniquement par les appareils mobiles inscrits par Intune ou par la gestion des appareils mobiles (MDM) locale.  

         Pour plus d’informations, consultez [Protéger vos données à l’aide de la réinitialisation à distance, du verrouillage à distance ou de la réinitialisation du code d’accès avec System Center Configuration Manager](../../../mdm/deploy-use/wipe-lock-reset-devices.md).  

    -   **Modifier la propriété d’un appareil**  

         Vous pouvez modifier la propriété d’un appareil à **Entreprise** ou **Personnel** si l’appareil n’est pas joint à un domaine et qu’il n’a pas le client Configuration Manager installé.  

         Vous pouvez spécifier cette valeur de propriété dans les conditions d’installation des applications pour contrôler les déploiements, et également utiliser cette configuration pour contrôler la quantité de données d’inventaire collectées des appareils des utilisateurs.  

        Pour afficher la valeur de propriété dans la liste d’appareils, vous devrez peut-être ajouter la colonne à la vue en cliquant avec le bouton droit sur n’importe quel titre de colonne et en choisissant **Propriétaire de l’appareil**.

         Pour plus d’informations, consultez [Gestion des appareils mobiles (MDM) hybride avec System Center Configuration Manager et Microsoft Intune](../../../mdm/plan-design/hybrid-mobile-device-management.md).  

##  <a name="a-namebkmkmanagingclientsdevicecollectionsnodea-manage-clients-from-the-device-collections-node"></a><a name="BKMK_ManagingClients_DeviceCollectionsNode"></a> Gérer les clients à partir du nœud Regroupements d’appareils  
 La procédure et le tableau ci-après permettent de gérer des périphériques dans un regroupement à partir du nœud **Regroupements de périphériques** de l'espace de travail **Ressources et Conformité** .  

 Un grand nombre de tâches de gestion de client que vous exécutez sur un ou plusieurs périphériques à partir du nœud **Périphériques** s'appliquent également au niveau des regroupements. Vous pouvez ainsi appliquer automatiquement la tâche de gestion à tous les périphériques éligibles dans le regroupement. Toutefois, cette méthode de gestion simultanée de plusieurs clients peut également générer de nombreux paquets réseau et augmenter l'utilisation du processeur sur le serveur de site.  

 De plus, certaines tâches de gestion du client ne peuvent être effectuées qu'au niveau du regroupement, comme indiqué dans le tableau ci-après.  

 Avant d'effectuer des tâches de gestion du client au niveau du regroupement, vous devez prendre en compte le nombre de périphériques dans le regroupement, s'ils utilisent des connexions réseau à faible bande passante, et le temps que prendra la tâche pour tous les périphériques. Lorsque vous effectuez une tâche de gestion de client, vous ne pouvez pas l'arrêter à partir de la console.  

#### <a name="to-manage-clients-from-the-device-collections-node"></a>Pour gérer les clients à partir du nœud Regroupements de périphériques  

1.  Dans la console Configuration Manager, cliquez sur **Ressources et Conformité**.  

2.  Dans l'espace de travail **Ressources et Conformité** , cliquez sur **Regroupements d’appareils**.  

3.  Sélectionnez un regroupement, puis sélectionnez l’une des tâches de gestion du client disponibles dans le ruban ou en cliquant avec le bouton droit sur le regroupement :  

    -   **Analysez les ordinateurs pour y détecter des programmes malveillants et téléchargez des fichiers de définition de logiciel anti-programme malveillant.**  

         Consultez [Endpoint Protection dans System Center Configuration Manager](../../../protect/deploy-use/endpoint-protection.md).  

    -   **Déployez des logiciels, des lignes de base de configuration et des séquences de tâches.**  

         Pour plus d'informations sur le déploiement de logiciels et de lignes de base de configuration, consultez les rubriques suivantes :  

        -   [Déployer des mises à jour logicielles dans System Center Configuration Manager](../../../sum/deploy-use/deploy-software-updates.md)  

        -   [Planifier et configurer les paramètres de conformité dans System Center Configuration Manager](../../../compliance/plan-design/plan-for-and-configure-compliance-settings.md)  

    -   **Configurez les paramètres de gestion de l'alimentation.**  

         Consultez [Comment créer et appliquer des modes de gestion de l’alimentation dans System Center Configuration Manager](../../../core/clients/manage/power/create-and-apply-power-plans.md). Les modes de gestion de l'alimentation ne peuvent être utilisés qu'avec les ordinateurs qui exécutent Windows.  

    -   **Invitez les ordinateurs à télécharger la stratégie dès que possible.**  

         Utilisez une notification de client pour inviter les clients Windows sélectionnés à télécharger la stratégie de l'ordinateur dès que possible en dehors de l'intervalle d'interrogation de stratégie client configuré.  

         Les tâches de notification de client s'affichent dans le nœud **Opérations du client** de l'espace de travail **Surveillance** .  

##  <a name="a-namebkmkclientcachea-configure-the-client-cache-for-configuration-manager-clients"></a><a name="BKMK_ClientCache"></a> Configurer le cache du client pour les clients Configuration Manager  
 Vous pouvez configurer l’emplacement du cache du client et la quantité d’espace disque que les clients Configuration Manager sur Windows utilisent pour stocker les fichiers temporaires lors de l’installation de programmes et d’applications. Les mises à jour logicielles utilisent également le cache du client, mais elles ne sont pas limitées par la taille configurée pour le cache et tenteront toujours de télécharger vers le cache. Vous pouvez configurer les paramètres du cache du client au moment où vous installez manuellement le client Configuration Manager, quand vous utilisez une installation push du client ou après que le client a été installé.

Dans Configuration Manager version 1606, vous pouvez spécifier la taille du dossier du cache en utilisant les paramètres client dans la console Configuration Manager.   

 L’emplacement par défaut pour le cache du client Configuration Manager est %*windir*%\ccmcache, et l’espace disque par défaut est de 5 120 Mo.  

> [!IMPORTANT]  
>  Ne chiffrez pas le dossier utilisé pour le cache du client. Configuration Manager ne peut pas télécharger du contenu vers un dossier chiffré.  

### <a name="about-client-cache"></a>À propos du cache du client  

Le client Configuration Manager télécharge le contenu pour les logiciels nécessaires dès qu’il reçoit le déploiement, mais il ne l’exécute pas avant l’heure planifiée du déploiement. À l’heure planifiée, le client Configuration Manager vérifie si le contenu est disponible dans le cache. Si le contenu est dans le cache et que la version en est correcte, le client utilise toujours ce contenu mis en cache. Toutefois, lorsque la version requise du contenu a été modifiée, ou si le contenu a été supprimé afin de faire de la place pour un autre package, le contenu est de nouveau téléchargé vers le cache.  

Si le client tente de télécharger du contenu pour un programme ou une application dont la taille est supérieure à celle du cache, le déploiement échoue en raison de la taille insuffisante du cache et Configuration Manager génère un message d’état (ID 10050). Si la taille du cache est augmentée par la suite, le comportement de la nouvelle tentative de téléchargement est différent pour un programme requis et pour une application requise :  

-   Pour un programme requis : le client ne retente pas automatiquement de télécharger le contenu. Vous devez redéployer le package et le programme vers le client.  
-   Pour une application requise : comme le déploiement d'une application est basé sur son état, le client tente automatiquement de télécharger le contenu lors de son prochain téléchargement de sa stratégie client.  

Si le client tente de télécharger un package dont la taille est inférieure à celle du cache, mais que le cache est plein, tous les déploiements requis continuent leurs tentatives, jusqu'à ce que l'espace du cache soit disponible et ce, jusqu'à expiration du délai de téléchargement ou jusqu'à ce que la limite du nombre de tentatives d'accès à l'espace du cache soit atteinte. Si la taille du cache augmente ultérieurement, Configuration Manager effectue une nouvelle tentative de téléchargement du package à l’intervalle suivant. Le client tente de télécharger le contenu toutes les 4 heures jusqu'à ce qu'il atteigne 18 tentatives.  

Le contenu mis en cache n'est pas automatiquement supprimé, mais reste dans le cache pendant au moins un jour après son utilisation par le client. Si vous configurez les propriétés du package avec l'option de conserver le contenu dans le cache du client, le client ne supprime pas automatiquement le contenu du package du cache. Si l'espace du cache du client est utilisé par des packages ayant été téléchargés au cours des dernières 24 heures et que le client doit télécharger de nouveaux packages, vous pouvez augmenter la taille du cache ou choisir l'option de suppression pour supprimer le contenu conservé dans le cache.  

 Utilisez les procédures suivantes pour configurer le cache du client lors de l'installation manuelle du client, ou après avoir installé le client.  

### <a name="to-configure-the-client-cache-when-you-install-clients-by-using-manual-client-installation"></a>Pour configurer le cache du client lorsque vous installez les clients à l'aide de l'installation client manuelle  

Exécutez la commande CCMSetup.exe à partir de l'emplacement source d'installation et spécifiez les propriétés suivantes dont vous avez besoin, séparées par des espaces :  

   -   DISABLECACHEOPT  

    -   SMSCACHEDIR  

    -   SMSCACHEFLAGS  

    -   SMSCACHESIZE  

        > [!NOTE]
        > Pour la version 1606, utilisez les paramètres de taille du cache disponibles dans **Paramètres client** dans la console Configuration Manager au lieu de la propriété SMSCACHESIZE. Pour plus d’informations, consultez [Paramètres du cache client](../../../core/clients/deploy/about-client-settings.md#Client-Cache-Settings) (Paramètres du cache du client).

Pour plus d’informations sur l’utilisation de ces propriétés de ligne de commande pour CCMSetup.exe, consultez [À propos des propriétés d’installation du client dans System Center Configuration Manager](../../../core/clients/deploy/about-client-installation-properties.md).  

### <a name="to-configure-the-client-cache-folder-when-you-install-clients-by-using-client-push-installation"></a>Pour configurer le dossier du cache du client lorsque vous installez les clients à l'aide de l'installation poussée du client  

1.  Dans la console Configuration Manager, cliquez sur **Administration**.  

2.  Dans l'espace de travail **Administration** , développez **Configuration du site**, puis cliquez sur **Sites**.  

3.  Dans la liste **Sites** , sélectionnez le site pour lequel vous souhaitez configurer l'installation poussée du client automatique à l'échelle du site.  

4.  Dans l'onglet **Accueil** , dans le groupe **Paramètres** , cliquez sur **Paramètres d'installation du client**, puis cliquez sur l'onglet **Propriétés de l'installation**.  

5.  Dans l'onglet **Propriétés de l'installation** , spécifiez les propriétés suivantes dont vous avez besoin, séparées par des espaces :  

    -   DISABLECACHEOPT  

    -   SMSCACHEDIR  

    -   SMSCACHEFLAGS  

    -   SMSCACHESIZE  

        > [!NOTE]
        > Pour la version 1606, utilisez les paramètres de taille du cache disponibles dans **Paramètres client** dans la console Configuration Manager au lieu de la propriété SMSCACHESIZE. Pour plus d’informations, consultez [Paramètres du cache client](../../../core/clients/deploy/about-client-settings.md#Client-Cache-Settings) (Paramètres du cache du client).

       Pour plus d’informations sur l’utilisation de ces propriétés de ligne de commande pour CCMSetup.exe, consultez [À propos des propriétés d’installation du client dans System Center Configuration Manager](../../../core/clients/deploy/about-client-installation-properties.md).  

6.  Cliquez sur **OK** pour enregistrer les propriétés que vous avez spécifiées.  

### <a name="to-configure-the-client-cache-folder-on-the-client-computer"></a>Pour configurer le dossier du cache du client sur l’ordinateur client  

1.  Sur l'ordinateur client, accédez à **Configuration Manager** dans le Panneau de configuration, puis double-cliquez pour ouvrir les propriétés.  

2.  Cliquez sur l'onglet **Cache** .  

3.  Spécifiez l'espace disque à réserver pour le cache du client.  

4.  Pour modifier l'emplacement du dossier du cache du client, cliquez sur **Modifier l'emplacement**, puis spécifiez le nouvel emplacement. L'emplacement par défaut est *%windir%*\ccmcache.  

5.  Pour supprimer les fichiers actuellement stockés dans le dossier du cache du client, cliquez sur **Supprimer les fichiers**.  

6.  Cliquez sur **OK** pour fermer les **Propriétés de Configuration Manager**.  

### <a name="to-configure-client-cache-size-in-client-settings"></a>Pour configurer la taille du cache du client dans les paramètres client

À compter de la version 1606, vous pouvez ajuster la taille du dossier du cache du client sans avoir à réinstaller le client. Pour ce faire, vous configurez la taille du cache du client dans la console Configuration Manager à l’aide des paramètres client.  

1. Dans la console Configuration Manager, accédez à **Administration** > **Paramètres client**.

2. Double-cliquez sur **Paramètres client par défaut**.
  Vous pouvez également créer des paramètres client personnalisés pour appliquer la taille du cache de manière plus sélective. Pour plus d’informations sur les paramètres client personnalisés et par défaut, consultez [Guide pratique pour configurer les paramètres client dans System Center Configuration Manager](../../../core/clients/deploy/configure-client-settings.md).

 3. Cliquez sur **Paramètres du cache des clients** et choisissez **Oui** pour **Configurer la taille du cache des clients**.

 4. Ajustez la taille maximale du cache avec les valeurs en **Mo** ou **pourcentage du disque**. La taille du cache est ajustée en fonction de la plus petite valeur.

 5. Cliquez sur **OK**.

    Le client Configuration Manager configurera la taille du cache avec ces paramètres lors du téléchargement de la stratégie client suivante.

##  <a name="a-namebkmkuninstalclienta-uninstall-the-configuration-manager-client"></a><a name="BKMK_UninstalClient"></a> Désinstaller le client Configuration Manager  
 Vous pouvez désinstaller le client Configuration Manager d’un ordinateur Windows en exécutant **CCMSetup.exe** avec la propriété **/Uninstall**. Exécutez CCMSetup.exe sur un ordinateur individuel à partir de l'invite de commande ou déployez un package et un programme pour désinstaller le client pour un regroupement d'ordinateurs.  

> [!WARNING]  
>  Il n’est pas possible de désinstaller le client Configuration Manager depuis un appareil mobile. Si vous devez supprimer le client Configuration Manager d’un appareil mobile, vous devez le réinitialiser, ce qui supprime toutes les données présentes sur l’appareil mobile.  

 Pour désinstaller le client Configuration Manager sur des ordinateurs, suivez la procédure ci-dessous.  

#### <a name="to-uninstall-the-configuration-manager-client-from-the-command-prompt"></a>Pour désinstaller le client Configuration Manager à partir de l'invite de commande  

1.  Ouvrez une invite de commandes Windows et accédez à l'emplacement du fichier CCMSetup.exe.  

2.  Entrez **Ccmsetup.exe /uninstall**, puis appuyez sur **Entrée**.  

> [!NOTE]  
>  Le processus de désinstallation est en mode silencieux et aucun résultat n'est affiché à l'écran. Pour vérifier que la désinstallation du client s'est déroulée correctement, examinez le fichier journal **CCMSetup.log** dans le dossier *%windir%\ ccmsetup* de l'ordinateur client.  

##  <a name="a-namebkmkconflictingrecordsa-manage-conflicting-records-for-configuration-manager-clients"></a><a name="BKMK_ConflictingRecords"></a> Gérer les enregistrements en conflit pour les clients Configuration Manager  
 Configuration Manager utilise l’ID du matériel pour tenter d’identifier les éventuels clients dupliqués et vous signale les conflits d’enregistrement qu’il trouve. Par exemple, si vous réinstallez un ordinateur, il est possible que l’ID du matériel soit le même, mais que le GUID utilisé par Configuration Manager soit différent.  

 Si Configuration Manager peut résoudre un conflit à l’aide de l’authentification Windows du compte d’ordinateur ou d’un certificat PKI émis par une source fiable, le conflit est résolu automatiquement. Si Configuration Manager ne peut pas résoudre le conflit, il utilise un paramètre de hiérarchie qui fusionne automatiquement les enregistrements avec le même ID de matériel qu’il a détectés (il s’agit du paramètre par défaut) ou qui vous laisse le choix de fusionner ou de bloquer les enregistrements du client, ou d’en créer d’autres. Si vous décidez de gérer manuellement les enregistrements en double, vous devez résoudre vous-même les conflits d’enregistrement à l’aide de la console Configuration Manager.  

#### <a name="to-change-the-hierarchy-setting-for-managing-conflicting-records"></a>Pour modifier le paramètre de hiérarchie pour gérer les conflits d'enregistrement  

1.  Dans la console Configuration Manager, cliquez sur **Administration**.  

2.  Dans l'espace de travail **Administration** , développez **Configuration du site**, puis cliquez sur **Sites**.  

3.  Dans le groupe **Sites** , cliquez sur **Paramètres de hiérarchie**, puis cliquez sur l'onglet **Approbation client et enregistrements en conflit** .  

4.  Cliquez sur **Résoudre automatiquement les enregistrements en conflit** pour fusionner automatiquement les enregistrements en conflit ou cliquez sur **Résoudre manuellement les enregistrements en conflit**, puis cliquez sur **OK**.  

    > [!NOTE]  
    >  Si Configuration Manager peut résoudre le conflit en utilisant le compte d’ordinateur ou un certificat PKI, ce paramètre est ignoré et le conflit est automatiquement résolu.  

#### <a name="to-manually-resolve-conflicting-records"></a>Pour résoudre manuellement les enregistrements en conflit  

1.  Dans la console Configuration Manager, cliquez sur **Surveillance**.  

2.  Dans l'espace de travail **Surveillance** , développez **État du système**, puis cliquez sur **Enregistrements en conflit**.  

3.  Dans le volet des résultats, sélectionnez un ou plusieurs enregistrements en conflit, puis cliquez sur **Enregistrement en conflit**.  

4.  Dans la boîte de dialogue **Enregistrement en conflit** , sélectionnez l'un des éléments suivants puis cliquez sur **OK**:  

    -   **Fusionner** : permet de combiner le nouvel enregistrement détecté avec l'enregistrement de client existant afin de créer un enregistrement unique.  

    -   **Nouveau** : permet de créer un nouvel enregistrement pour l'enregistrement de client en conflit.  

    -   **Bloquer** : permet de créer un nouvel enregistrement pour l'enregistrement de client en conflit, mais le marquer comme bloqué.  

##  <a name="a-namebkmkpolicyretrievala-initiate-policy-retrieval-for-a-configuration-manager-client"></a><a name="BKMK_PolicyRetrieval"></a> Lancer une récupération de stratégie pour un client Configuration Manager  
 Sur Windows, un client Configuration Manager télécharge sa stratégie client selon un calendrier que vous configurez comme paramètre du client. Toutefois, vous pouvez avoir besoin de lancer une récupération de stratégie ad hoc à partir du client, par exemple, dans un scénario de dépannage ou pour effectuer des tests.  

 Suivez les procédures décrites ci-après pour initier une récupération de stratégie ad hoc à partir du client, en dehors de l'intervalle d'interrogation planifié, à l'aide de l'onglet **Actions** du client Configuration Manager ou en exécutant un script sur l'ordinateur. Vous devez vous connecter à l'ordinateur client avec des droits d'administrateur local pour pouvoir effectuer ces procédures.  

> [!NOTE]  
>  Vous pouvez utiliser une notification de client pour lancer une récupération de stratégie de client en dehors de l'intervalle d'interrogation de stratégie de client planifié.  
>   
>  Vous pouvez gérer les clients qui exécutent Linux et UNIX. Pour plus d’informations sur la récupération des stratégies pour les clients qui exécutent Linux et UNIX, consultez [Computer policy for Linux and UNIX servers](../../../core/clients/manage/manage-clients-for-linux-and-unix-servers.md#BKMK_PolicyforLnU).  

#### <a name="to-initiate-client-policy-retrieval-by-using-client-notification"></a>Pour lancer la récupération d’une stratégie client à l’aide d’une notification de client  

1.  Dans la console Configuration Manager, cliquez sur **Ressources et Conformité**.  

2.  Dans l'espace de travail **Ressources et Conformité** , cliquez sur **Regroupements de périphériques**.  

3.  Sélectionnez le regroupement de périphériques contenant les ordinateurs dont vous souhaitez télécharger la stratégie, puis sous l'onglet **Accueil** , dans le groupe **Regroupements** , cliquez sur **Notification du client** , puis sur **Télécharger la stratégie d'ordinateur**.  

    > [!NOTE]  
    >  Vous pouvez également utiliser une notification de client pour lancer la récupération de la stratégie pour un ou plusieurs périphériques sélectionnés affichés dans un nœud de regroupement temporaire sous le nœud **Périphériques** .  

#### <a name="to-manually-initiate-client-policy-retrieval-by-using-the-actions-tab-on-the-configuration-manager-client"></a>Pour initier manuellement la récupération de stratégie du client à l'aide de l'onglet Actions du client Configuration Manager  

1.  Sélectionnez **Configuration Manager** dans le panneau de configuration de l'ordinateur.  

2.  Cliquez sur l'onglet **Actions** .  

3.  Cliquez sur **Récupération de stratégie ordinateur et cycle d’évaluation** pour lancer la stratégie ordinateur, puis sur **Exécuter maintenant**.  

4.  Cliquez sur **OK** pour confirmer l'invite.  

5.  Répétez les étapes 3 et 4 pour toutes les actions dont vous avez besoin, telles que **Récupération de stratégie utilisateur et cycle d’évaluation** pour les paramètres client utilisateur.  

6.  Cliquez sur **OK** pour fermer les **Propriétés de Configuration Manager**.  

#### <a name="to-manually-initiate-client-policy-retrieval-by-using-a-script"></a>Pour initier manuellement la récupération de stratégie du client à l'aide d'un script  

1.  Ouvrez un éditeur de texte, tel que le Bloc-notes.  

2.  Copiez et insérez le code suivant dans le fichier :  

    ```  
    on error resume next  

    dim oCPAppletMgr 'Control Applet manager object.  
    dim oClientAction 'Individual client action.  
    dim oClientActions 'A collection of client actions.  

    'Get the Control Panel manager object.  
    set  oCPAppletMgr=CreateObject("CPApplet.CPAppletMgr")  
    if err.number <> 0 then  
        Wscript.echo "Couldn't create control panel application manager"  
        WScript.Quit  
    end if  

    'Get a collection of actions.  
    set oClientActions=oCPAppletMgr.GetClientActions  
    if err.number<>0 then  
        wscript.echo "Couldn't get the client actions"  
        set oCPAppletMgr=nothing  
        WScript.Quit  
    end if  

    'Display each client action name and perform it.  
    For Each oClientAction In oClientActions  

        if oClientAction.Name = "Request & Evaluate Machine Policy" then  
            wscript.echo "Performing action " + oClientAction.Name   
            oClientAction.PerformAction  
        end if  
    next  

    set oClientActions=nothing  
    set oCPAppletMgr=nothing  
    ```  

3.  Enregistrez le fichier avec une extension .vbs.  

4.  Sur l'ordinateur client, exécutez le fichier à l'aide de l'une des méthodes ci-après :  

    -   Accédez au fichier via l'Explorateur Windows et double-cliquez sur le fichier de script.  

    -   Ouvrez une invite de commandes et tapez **cscript &lt;chemin\nom_fichier.vbs>**.  

5.  Cliquez sur **OK** dans la boîte de dialogue **Environnement d'exécution de scripts WSH (Windows Script Host)** .  



<!--HONumber=Nov16_HO1-->


