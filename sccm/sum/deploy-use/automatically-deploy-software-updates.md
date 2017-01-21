---
title: "Déployer automatiquement des mises à jour logicielles | Documents Microsoft"
description: "Déployez automatiquement des mises à jour logicielles en ajoutant de nouvelles mises à jour logicielles à un groupe de mises à jour qui est associé à un déploiement actif ou en utilisant des règles ADR."
keywords: 
author: dougeby
ms.author: dougeby
manager: angrobe
ms.date: 12/07/2016
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology:
- configmgr-sum
ms.assetid: b27682de-adf8-4edd-9572-54886af8f7fb
translationtype: Human Translation
ms.sourcegitcommit: 78524abd4c45f0b7402d6f1e85afc60bb72ab0ee
ms.openlocfilehash: 34b0819957ffcc3711ee354a5b821d78fa7445cb

---

#  <a name="a-namebkmkautodeploya-automatically-deploy-software-updates"></a><a name="BKMK_AutoDeploy"></a> Déployer automatiquement des mises à jour logicielles  

*S’applique à : System Center Configuration Manager (Current Branch)*

 Vous pouvez déployer automatiquement des mises à jour logicielles en ajoutant de nouvelles mises à jour logicielles à un groupe de mises à jour qui est associé à un déploiement actif ou vous pouvez utiliser une règle de déploiement automatique (ADR, Automatic Deployment Rule). D’une manière générale, vous utilisez des règles ADR pour déployer les mises à jour logicielles mensuelles (généralement appelées mises à jour Patch Tuesday) et pour la gestion des mises à jour de définitions. Si vous avez besoin d’aide pour déterminer la méthode de déploiement qui vous convient, voir [Déployer des mises à jour logicielles](deploy-software-updates.md).

##  <a name="a-namebkmkaddupdatestoexistinggroupa-add-software-updates-to-a-deployed-update-group"></a><a name="BKMK_AddUpdatesToExistingGroup"></a> Ajouter des mises à jour logicielles à un groupe de mises à jour déployé  
Après avoir créé et déployé un groupe de mises à jour logicielles, vous pouvez ajouter des mises à jour logicielles au groupe de mises à jour ; elles sont déployées automatiquement.  

> [!IMPORTANT]  
>  Lorsque vous ajoutez des mises à jour logicielles à un groupe de mises à jour logicielles existant qui a déjà été déployé, l'ajout des mises à jour logicielles supplémentaires au déploiement peut prendre plusieurs minutes.  

Pour ajouter des mises à jour logicielles à un groupe de mises à jour existant, procédez comme suit.  

#### <a name="to-add-software-updates-to-an-existing-software-update-group"></a>Pour ajouter des mises à jour logicielles à un groupe de mises à jour logicielles existant  

1.  Dans la console Configuration Manager, accédez à **Bibliothèque de logiciels** > **Vue d’ensemble** > **Mises à jour logicielles**.  

2.  Sélectionnez les mises à jour logicielles à ajouter au nouveau groupe de mises à jour logicielles.  

3.  Dans l'onglet **Accueil** , dans le groupe **Mise à jour** , cliquez sur **Modifier l'adhésion**.  

4.  Sélectionnez le groupe de mises à jour logicielles auquel ajouter les mises à jour logicielles en tant que membres.  

5.  Cliquez sur le nœud **Groupes de mises à jour logicielles** pour afficher le groupe de mises à jour logicielles.  

6.  Cliquez sur le groupe de mises à jour logicielles et, dans l'onglet **Accueil** , dans le groupe **Mise à jour** , cliquez sur **Afficher les membres** pour afficher une liste des mises à jour logicielles dans le groupe.  

##  <a name="a-namebkmkcreateautomaticdeploymentrulea-create-an-automatic-deployment-rule-adr"></a><a name="BKMK_CreateAutomaticDeploymentRule"></a> Créer une règle de déploiement automatique (ADR)  
Vous pouvez approuver et déployer automatiquement des mises à jour logicielles en utilisant une règle ADR. Vous pouvez faire en sorte que la règle ajoute des mises à jour logicielles à un nouveau groupe de mises à jour logicielles chaque fois qu'elle s'exécute ou vous pouvez ajouter des mises à jour logicielles à un groupe existant. Lorsqu'une règle s'exécute et ajoute des mises à jour logicielles à un groupe existant, elle supprime toutes les mises à jour logicielles du groupe, puis elle ajoute au groupe les mises à jour logicielles qui répondent aux critères que vous définissez. Par exemple, pour exécuter une règle ADR dans le but de rechercher les nouvelles mises à jour logicielles chaque jour et les déployer sur les clients, vous devez choisir l’option de création d’un nouveau groupe de mises à jour logicielles au lieu d’ajouter les mises à jour logicielles à un groupe existant.  

> [!WARNING]  
>  Avant de créer une règle ADR pour la première fois, vérifiez que la synchronisation des mises à jour logicielles est terminée sur le site. Cela s'avère particulièrement important lorsque vous exécutez Configuration Manager dans une langue autre que l'anglais, car les classifications des mises à jour logicielles s'affichent en anglais avant la première synchronisation, puis elles s'affichent dans la langue localisée une fois la synchronisation des mises à jour logicielles terminée. Les règles que vous créez avant de synchroniser les mises à jour logicielles risquent ne pas fonctionner correctement après la synchronisation car la chaîne de texte peut ne pas correspondre.  

 Utilisez la procédure suivante pour créer une règle ADR.  

#### <a name="to-create-an-adr"></a>Pour créer une règle ADR  

1.  Dans la console Configuration Manager, accédez à **Bibliothèque de logiciels****Vue d’ensemble** > **Mises à jour logicielles** > **Règles de déploiement automatique**.  

2.  Dans l'onglet **Accueil** , dans le groupe **Créer** , cliquez sur **Créer une règle de déploiement automatique**. L'Assistant Création d'une règle de déploiement automatique s'ouvre.  

3.  Sur la page **Général** , configurez les paramètres suivants :  

    -   **Nom :**spécifiez le nom de la règle ADR. Le nom doit être unique, permettre de décrire l'objectif de la règle et être identifiable parmi d'autres dans le site Configuration Manager.  

    -   **Description :**spécifiez une description pour la règle ADR. La description doit fournir une vue d'ensemble de la règle de déploiement et toutes autres informations pertinentes permettant de l'identifier et de la différencier des autres dans le site Configuration Manager. Le champ de description facultatif est limité à 256 caractères et est vierge par défaut.  

    -   **Sélectionner un modèle de déploiement**: indiquez si un modèle de déploiement enregistré précédemment doit être appliqué. Vous pouvez configurer un modèle de déploiement de sorte qu’il contienne plusieurs propriétés de déploiement de mises à jour logicielles communes, utilisables par la suite pour créer des règles ADR. Ces modèles permettent de garantir la cohérence entre des déploiements similaires et de gagner du temps.  

         Vous pouvez opter pour l’un des modèles de déploiement de mises à jour logicielles prédéfinis à partir de l’Assistant Création d’une règle de déploiement automatique. Le modèle **Mises à jour de définitions** fournit des paramètres communs à utiliser lorsque vous déployez des mises à jour logicielles de définitions. Le modèle **Patch Tuesday** fournit des paramètres communs à utiliser lorsque vous déployez des mises à jour logicielles selon un cycle mensuel.  

    -   **Regroupement**: indique le regroupement cible à utiliser pour le déploiement. Les membres du regroupement reçoivent les mises à jour logicielles définies dans le déploiement.  

    -   déterminer si des mises à jour logicielles seront ajoutées à un groupe de mises à jour logicielles nouveau ou existant. Dans la plupart des cas, vous choisirez probablement de créer un nouveau groupe de mises à jour logicielles au moment d’exécuter la règle ADR. Toutefois, vous pouvez choisir d'utiliser un groupe existant, si la règle s'exécute selon une planification plus agressive. Par exemple, si vous exécutez la règle quotidiennement pour des mises à jour de définitions, vous pouvez ajouter les mises à jour logicielles à un groupe de mises à jour logicielles existant.  

    -   **Activer le déploiement après l’exécution de cette règle**: indiquez si le déploiement des mises à jour logicielles doit être activé après l’exécution de la règle ADR. En ce qui concerne cette spécification, tenez compte des éléments suivants :  

        -   Lors de l'activation du déploiement, les mises à jour logicielles qui répondent aux critères définis dans la règle sont ajoutées à un groupe de mises à jour logicielles, le contenu des mises à jour logicielles est téléchargé si besoin, le contenu est copié vers les points de distribution spécifiés, puis les mises à jour logicielles sont déployées sur les clients dans le regroupement cible.  

        -   Lorsque vous n'activez pas le déploiement, les mises à jour logicielles qui répondent aux critères définis dans la règle sont ajoutées à un groupe de mises à jour logicielles et la stratégie de déploiement des mises à jour logicielles est configurée, mais les mises à jour logicielles ne sont pas téléchargées ni déployées sur les clients. Cette situation vous laisse le temps suffisant pour préparer le déploiement des mises à jour logicielles, vérifier que les mises à jour logicielles répondant aux critères sont adéquates, puis activer ultérieurement le déploiement.  

4.  Sur la page Paramètres de déploiement, configurez les paramètres suivants :  

    -   **Utiliser Wake-on-LAN pour réveiller les clients pour les déploiements requis**: indique si l’éveil par appel réseau (Wake On LAN) doit être activé à l’échéance pour envoyer des paquets de mise en éveil aux ordinateurs qui nécessitent une ou plusieurs mises à jour logicielles du déploiement. Tous les ordinateurs en mode veille à l'échéance de l'installation sont mis en éveil pour que l'installation des mises à jour logicielles puisse démarrer. Les clients en mode veille qui ne nécessitent pas les mises à jour logicielles incluses dans le déploiement ne sont pas démarrés. Par défaut, ce paramètre n'est pas activé.  

        > [!WARNING]  
        >  Avant de pouvoir utiliser cette option, vous devez configurer les ordinateurs et les réseaux pour l'éveil par appel réseau.  

    -   **Niveau de détail**: indiquez le niveau de détail pour les messages d’état qui sont signalés par les ordinateurs clients.  

        > [!IMPORTANT]  
        >  Lorsque vous déployez des mises à jour de définitions, affectez au niveau de détails la valeur **Erreur uniquement** pour que le client envoie un message d'état uniquement lorsqu'une mise à jour de définition ne lui est pas remise. Sinon, le client envoie un grand nombre de messages d'état pouvant avoir un effet sur les performances du serveur de site.  

    -   **Paramètre du contrat de licence**: indiquez si les mises à jour logicielles doivent être déployées automatiquement avec un contrat de licence associé. Certaines mises à jour logicielles comprennent un contrat de licence, dans le cas d'un Service Pack par exemple. Lorsque vous déployez automatiquement des mises à jour logicielles, le contrat de licence ne s'affiche pas et il n'est pas possible d'accepter le contrat de licence. Vous pouvez choisir de déployer automatiquement toutes les mises à jour logicielles indépendamment d'un contrat de licence associé ou de déployer uniquement les mises à jour logicielles qui ne sont associées à aucun contrat de licence.  

        > [!NOTE]  
        >  Pour consulter le contrat de licence d'une mise à jour logicielle, vous pouvez sélectionner la mise à jour logicielle dans le nœud **Toutes les mises à jour logicielles** de l'espace de travail **Bibliothèque de logiciels** , puis, sur l'onglet **Accueil** , dans le groupe **Mise à jour** , cliquez sur **Consulter le contrat de licence**.  
        >   
        >  Pour trouver des mises à jour logicielles avec un contrat de licence associé, vous pouvez ajouter la colonne **Termes du contrat de licence** au volet des résultats dans le nœud **Toutes les mises à jour logicielles** , puis cliquer sur l'en-tête de la colonne pour effectuer un tri selon les mises à jour logicielles associées à un contrat de licence.  

5.  Dans la page Mises à jour logicielles, configurez les critères des mises à jour logicielles que la règle ADR récupère et ajoute au groupe de mises à jour logicielles.  

    > [!IMPORTANT]  
    >  Dans une règle ADR, le nombre limite de mises à jour logicielles est de 1 000. Pour veiller à ce que les critères spécifiés sur cette page permettent de récupérer moins de 1 000 mises à jour logicielles, envisagez de définir les mêmes critères sur le nœud **Toutes les mises à jour logicielles** dans l'espace de travail **Bibliothèque de logiciels** .  

    > [!NOTE]
    > Depuis Configuration Manager version 1610, vous pouvez filtrer sur la taille du contenu des mises à jour logicielles dans les règles de déploiement automatique. Par exemple, vous pouvez définir le filtre **Taille du contenu (Ko)** sur **< 2048** pour télécharger uniquement les mises à jour logicielles inférieures à 2 Mo. Ce filtre empêche le téléchargement automatique des mises à jour logicielles volumineuses pour une meilleure prise en charge de la maintenance de bas niveau Windows simplifiée lorsque la bande passante du réseau est limitée. Pour plus d’informations, consultez [Configuration Manager et maintenance Windows simplifiée sur des systèmes d’exploitation de bas niveau](https://blogs.technet.microsoft.com/enterprisemobility/2016/10/07/configuration-manager-and-simplified-windows-servicing-on-down-level-operating-systems/).

6.  Dans la page Calendrier d’évaluation, indiquez si l’exécution de la règle ADR doit obéir à un calendrier. Si elle est activée, cliquez sur **Personnaliser** pour définir le calendrier périodique.  

    > [!IMPORTANT]  
    >  Le calendrier de synchronisation du point de mise à jour logicielle s'affiche pour vous aider à déterminer la fréquence du calendrier d'évaluation. Il est préférable de ne jamais définir le calendrier d'évaluation selon une fréquence supérieure au calendrier de synchronisation des mises à jour logicielles. La configuration de l'heure de début du calendrier se base sur l'heure locale de l'ordinateur qui exécute la console Configuration Manager.  

    > [!NOTE]  
    >  Pour exécuter manuellement la règle ADR, sélectionnez la règle, puis cliquez sur **Exécuter maintenant** sous l’onglet **Accueil** dans le groupe **Règle de déploiement automatique** . Avant d’exécuter manuellement la règle ADR, vérifiez que la synchronisation des mises à jour logicielles a été exécutée depuis la dernière exécution de la règle.  

    > [!IMPORTANT]  
    >  La règle ADR peut être évaluée jusqu’à trois fois par jour.  

7.  Sur la page Calendrier de déploiement, configurez les paramètres suivants :  

    -   **Calendrier d’évaluation** : indiquez si Configuration Manager évalue la durée disponible et la date d’échéance de l’installation à l’heure UTC ou à l’heure locale de l’ordinateur exécutant la console Configuration Manager.  

        > [!NOTE]  
        >  Si vous sélectionnez l’heure locale, puis **Dès que possible** pour le **Temps disponible du logiciel** ou **Échéance d’installation**, l’heure actuelle sur l’ordinateur exécutant la console Configuration Manager est utilisée pour évaluer quand les mises à jour sont disponibles ou quand elles sont installées sur un client. Si le client est dans un autre fuseau horaire, ces actions se produisent quand l’heure du client atteint l’heure de l’évaluation.  

    -   **Temps disponible du logiciel**: sélectionnez l’un des paramètres suivants pour spécifier le moment où les mises à jour logicielles sont disponibles pour les clients :  

        -   **Dès que possible**: sélectionnez ce paramètre pour permettre aux ordinateurs clients d’accéder dès que possible aux mises à jour logicielles incluses dans le déploiement. Quand vous créez le déploiement avec ce paramètre sélectionné, Configuration Manager met à jour la stratégie client. Ensuite, au prochain cycle d'interrogation de la stratégie client, les clients prennent connaissance du déploiement et peuvent obtenir les mises à jour disponibles à l'installation.  

        -   **Heure spécifique**: sélectionnez ce paramètre pour permettre aux ordinateurs clients d’accéder aux mises à jour logicielles incluses dans le déploiement à une date et heure précises. Quand vous créez le déploiement avec ce paramètre activé, Configuration Manager met à jour la stratégie client. Ensuite, au prochain cycle d'interrogation de la stratégie client, les clients prennent connaissance du déploiement. Toutefois, les mises à jour logicielles incluses dans le déploiement ne sont pas disponibles à l'installation avant la date et l'heure configurées.  

    -   **Échéance d’installation**: sélectionnez l’un des paramètres suivants pour spécifier l’échéance d’installation des mises à jour logicielles incluses dans le déploiement :  

        -   **Dès que possible**: sélectionnez ce paramètre pour installer automatiquement les mises à jour logicielles incluses dans le déploiement dès que possible.  

        -   **Heure spécifique**: sélectionnez ce paramètre pour installer automatiquement les mises à jour logicielles incluses dans le déploiement à une date et une heure spécifiques. Configuration Manager détermine l’échéance d’installation des mises à jour logicielles en ajoutant l’intervalle **Heure spécifique** configuré au **Temps disponible du logiciel**.  

        > [!NOTE]  
        >  L'heure d'échéance de l'installation réelle est l'heure d'échéance affichée plus un laps de temps aléatoire pouvant atteindre 2 heures. Elle permet de réduire l'impact lié à l'installation simultanée, par tous les ordinateurs clients du regroupement de destination, des mises à jour logicielles incluses dans le déploiement.  
        >   
        >  Vous pouvez configurer le paramètre client **Agent ordinateur** , **Désactiver la randomisation des échéances** , pour désactiver le délai de randomisation de l’installation des mises à jour logicielles requises. Pour plus d’informations, voir [Computer Agent](../../core/clients/deploy/about-client-settings.md#computer-agent).  

8. Sur la page Expérience utilisateur, configurez les paramètres suivants :  

    -   **Notifications à l’utilisateur**: indiquez si vous souhaitez afficher les notifications des mises à jour logicielles dans le Centre logiciel sur l’ordinateur client selon la valeur **Temps disponible du logiciel** configuré et si les notifications à l’utilisateur doivent s’afficher sur les ordinateurs clients.  

    -   **Comportement à l’échéance**: spécifiez le comportement qui doit se produire lorsque l’échéance est atteinte pour le déploiement des mises à jour logicielles. Indiquez si vous souhaitez installer les mises à jour logicielles incluses dans le déploiement. Spécifiez également si un redémarrage du système doit être effectué après l'installation des mises à jour logicielles, quelle que soit la fenêtre de maintenance configurée. Pour plus d’informations sur les fenêtres de maintenance, consultez [Guide pratique pour utiliser les fenêtres de maintenance](../../core/clients/manage/collections/use-maintenance-windows.md).  

    -   **Comportement de redémarrage du périphérique**: indiquez si le redémarrage du système sur les serveurs et stations de travail doit être supprimé une fois les mises à jour logicielles installées et si un redémarrage du système est nécessaire pour terminer l’installation.  

        > [!IMPORTANT]  
        >  La suppression du redémarrage système peut s'avérer utile dans les environnements de serveurs ou lorsque vous ne souhaitez pas que les ordinateurs qui installent les mises à jour logicielles redémarrent par défaut. Toutefois, elle peut laisser les ordinateurs dans un état non sécurisé, alors que l'autorisation d'un redémarrage forcé contribue à garantir l'exécution immédiate de l'installation des mises à jour logicielles.  

    -   **Traitement des filtres d’écriture pour les appareils Windows Embedded**: quand vous déployez des mises à jour logicielles sur des appareils Windows Embedded pour lesquels le filtre d’écriture est activé, vous pouvez choisir d’installer la mise à jour logicielle sur le segment de recouvrement temporaire et valider les modifications ultérieurement ou à l’échéance de l’installation ou bien pendant une fenêtre de maintenance. Lorsque vous validez des modifications à l'échéance de l'installation ou au cours d'une fenêtre de maintenance, un redémarrage est requis et les modifications sont conservées sur l'appareil.  

        > [!NOTE]  
        >  Lorsque vous déployez une mise à jour logicielle sur un appareil Windows Embedded, assurez-vous que l'appareil fait partie des membres d'un regroupement pour lequel une fenêtre de maintenance a été configurée.  

    - **Comportement de réévaluation du déploiement des mises à jour logicielles après le redémarrage** : à compter de Configuration Manager version 1606, sélectionnez ce paramètre pour configurer les déploiements de mises à jour logicielles de façon à ce que les clients exécutent une analyse de conformité des mises à jour logicielles immédiatement après avoir installé celles-ci et redémarré. Cela permet au client de vérifier la disponibilité de mises à jour logicielles supplémentaires devenues applicables après le redémarrage, puis de les installer (et devenir ainsi conforme) au cours d’une même fenêtre de maintenance.

9. Sur la page Alertes, configurez la manière dont Configuration Manager et System Center Operations Manager génèreront des alertes pour ce déploiement.  

    > [!NOTE]  
    >  Vous pouvez consulter les récentes alertes de mises à jour logicielles à partir du nœud **Mises à jour logicielles** dans l'espace de travail **Bibliothèque de logiciels** .  

10. Sur la page Paramètres de téléchargement, configurez les paramètres suivants :  

    -   Indiquez si le client va télécharger et installer les mises à jour logicielles quand il est connecté à un réseau lent ou utilise un emplacement de secours pour le contenu.  

    -   Indiquez si le client doit télécharger et installer les mises à jour logicielles à partir d'un point de distribution de secours quand le contenu pour les mises à jour logicielles n'est pas disponible sur un point de distribution préféré.  

    -   **Autoriser les clients à partager du contenu avec d’autres clients sur le même sous-réseau**: indiquez si vous souhaitez activer l’utilisation de BranchCache pour les téléchargements du contenu. Pour plus d’informations sur BrandCache, consultez [Concepts for content management](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#branchcache).  

    -   Indiquez si les clients connectés à l’intranet doivent télécharger les mises à jour logicielles à partir de Microsoft Update si elles ne sont pas disponibles sur des points de distribution.  

    -   Indiquez si vous souhaitez autoriser le téléchargement aux clients après l'échéance d'une installation lorsqu'ils utilisent des connexions Internet facturée à l'usage. Les fournisseurs Internet facturent parfois en fonction de la quantité de données que vous envoyez et recevez lorsque vous utilisez une connexion Internet facturée à l'usage.  

    > [!NOTE]  
    >  Les clients demandent l'emplacement du contenu à partir d'un point de gestion pour les mises à jour logicielles dans un déploiement. Le comportement de téléchargement dépend de la manière dont vous avez configuré le point de distribution, le package de déploiement et les paramètres sur cette page. Pour plus d'informations, voir [Content source location scenarios](../../core/plan-design/hierarchy/content-source-location-scenarios.md).  

11. Sur la page Package de déploiement, sélectionnez un package de déploiement existant ou configurez les paramètres suivants pour créer un package de déploiement :  

    1.  **Nom**: spécifiez le nom du package de déploiement. Celui-ci doit être un nom unique qui décrit le contenu du package. Il est limité à 50 caractères.  

    2.  **Description**: spécifiez une description qui fournit des informations sur le package de déploiement. La description est limitée à 127 caractères.  

    3.  **Source du package**: spécifie l’emplacement des fichiers sources des mises à jour logicielles.  Tapez un chemin réseau pour l’emplacement source, par exemple **\\\serveur\nom_partage\chemin**ou cliquez sur **Parcourir** pour rechercher l’emplacement réseau. Vous devez créer le dossier partagé pour les fichiers sources du package de déploiement avant de passer à la page suivante.  

        > [!NOTE]  
        >  L'emplacement source du package de déploiement que vous spécifiez ne peut pas être utilisé par un autre package de déploiement de logiciel.  

        > [!IMPORTANT]  
        >  Le compte d'ordinateur du fournisseur SMS et l'utilisateur qui exécute l'Assistant Téléchargement des mises à jour logicielles nécessitent des autorisations NTFS en **Écriture** sur l'emplacement de téléchargement. Vous devez soigneusement limiter l'accès à l'emplacement de téléchargement pour éviter que des personnes malintentionnées ne falsifient les fichiers sources des mises à jour logicielles.  

        > [!IMPORTANT]  
        >  Une fois que le package de déploiement a été créé par Configuration Manager, vous pouvez modifier l’emplacement source du package de déploiement dans les propriétés du package. Mais le cas échéant, vous devez d'abord copier le contenu à partir de la source du package d'origine vers le nouvel emplacement source du package.  

    4.  **Priorité d’expédition**: spécifiez la priorité d’envoi pour le package de déploiement. Configuration Manager utilise la priorité d’expédition du package de déploiement quand il envoie le package aux points de distribution. Les packages de déploiement sont envoyés par ordre de priorité : Haute, Moyenne ou Faible. Les packages disposant de priorités identiques sont transmis dans l'ordre dans lequel ils ont été créés. En l'absence de backlog, le package est immédiatement traité quelle que soit sa priorité.  

12. Sur la page Points de distribution, spécifiez les points de distribution ou les groupes de points de distribution qui vont héberger les fichiers de mise à jour logicielle. Pour plus d’informations sur les points de distribution, consultez [Configurations des points de distribution](../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_configs).  

    > [!NOTE]  
    >  Cette page est disponible uniquement lorsque vous créez un nouveau package de déploiement de mise à jour logicielle.  

13. Sur la page Emplacement de téléchargement, indiquez si les fichiers de mise à jour logicielle doivent être téléchargés à partir d'Internet ou de votre réseau local. Configurez les paramètres suivants :  

    -   **Télécharger les mises à jour logicielles depuis Internet**: sélectionnez ce paramètre pour télécharger les mises à jour logicielles à partir d’un emplacement spécifié sur Internet. Ce paramètre est activé par défaut.  

    -   **Télécharger les mises à jour logicielles à partir d’un emplacement sur le réseau local**: sélectionnez ce paramètre pour télécharger les mises à jour logicielles à partir d’un répertoire local ou d’un dossier partagé. Ce paramètre s'avère utile lorsque l'ordinateur exécutant l'Assistant ne dispose d'aucun accès à Internet. N'importe quel ordinateur connecté à Internet peut préalablement télécharger les mises à jour logicielles et les stocker à un emplacement sur le réseau local qui est accessible à partir de l'ordinateur qui exécute l'Assistant.  

14. Sur la page Sélection de la langue, sélectionnez les langues pour lesquelles les mises à jour logicielles sélectionnées sont téléchargées. Les mises à jour logicielles sont téléchargées uniquement si elles sont disponibles dans les langues sélectionnées. Les mises à jour logicielles qui ne sont spécifiques à aucune langue sont toujours téléchargées. Par défaut, l'Assistant sélectionne les langues que vous avez configurées dans les propriétés du point de mise à jour logicielle. Au moins une langue doit être sélectionnée avant de passer à la page suivante. Quand vous sélectionnez uniquement des langues qui ne sont pas prises en charge par une mise à jour logicielle, le téléchargement échoue pour cette mise à jour logicielle.  

15. Sur la page Résumé, passez en revue les paramètres. Pour enregistrer les paramètres dans un modèle de déploiement, cliquez sur **Enregistrer comme modèle**, entrez un nom et sélectionnez les paramètres à inclure dans le modèle, puis cliquez sur **Enregistrer**. Pour modifier un paramètre configuré, cliquez sur la page de l'Assistant associée et modifiez le paramètre.  

    > [!NOTE]  
    >  Le nom du modèle peut comporter des caractères ASCII alphanumériques ainsi que les caractères **\\** (barre oblique inverse) ou **‘** (guillemet-apostrophe).  

16. Cliquez sur **Suivant** pour créer la règle ADR.  

 La règle ADR s’exécute une fois que vous avez terminé l’Assistant. Elle permet d'ajouter les mises à jour logicielles qui correspondent aux critères spécifiés à un groupe de mises à jour logicielles, de télécharger les mises à jour logicielles dans la bibliothèque de contenu sur le serveur de site, de distribuer les mises à jour logicielles aux points de distribution configurés, puis de déployer le groupe de mises à jour logicielles sur les clients du regroupement cible.  

##  <a name="a-namebkmkadddeploymenttoadra-add-a-new-deployment-to-an-existing-adr"></a><a name="BKMK_AddDeploymentToADR"></a> Ajouter un nouveau déploiement à une règle ADR existante  
 Après avoir créé une règle ADR, vous pouvez y ajouter des déploiements supplémentaires. Cela peut vous aider à gérer la complexité liée au déploiement de différentes mises à jour vers différents regroupements. Chaque nouveau déploiement possède la gamme complète de fonctionnalités et d'expérience de surveillance de déploiement.  

#### <a name="to-add-a-new-deployment-to-an-existing-adr"></a>Pour ajouter un nouveau déploiement à une règle ADR existante  

1.  Dans la console Configuration Manager, accédez à **Bibliothèque de logiciels** > **Vue d’ensemble** > **Mises à jour logicielles** > **Règles de déploiement automatique**, puis sélectionnez la règle de votre choix.  

2.  Sous l’onglet **Accueil** , dans le groupe **Règle de déploiement automatique** , cliquez sur **Ajouter un déploiement**. L’Assistant Ajout de déploiement s’ouvre.  

3.  Dans la page **Regroupement** , configurez les paramètres suivants :  

    -   **Regroupement**: indique le regroupement cible à utiliser pour le déploiement. Les membres du regroupement reçoivent les mises à jour logicielles définies dans le déploiement.  

    -   **Activer le déploiement après l’exécution de cette règle**: indiquez si le déploiement des mises à jour logicielles doit être activé après l’exécution de la règle ADR. En ce qui concerne cette spécification, tenez compte des éléments suivants :  

        -   Lors de l'activation du déploiement, les mises à jour logicielles qui répondent aux critères définis dans la règle sont ajoutées à un groupe de mises à jour logicielles, le contenu des mises à jour logicielles est téléchargé si besoin, le contenu est copié vers les points de distribution spécifiés, puis les mises à jour logicielles sont déployées sur les clients dans le regroupement cible.  

        -   Lorsque vous n'activez pas le déploiement, les mises à jour logicielles qui répondent aux critères définis dans la règle sont ajoutées à un groupe de mises à jour logicielles et la stratégie de déploiement des mises à jour logicielles est configurée, mais les mises à jour logicielles ne sont pas téléchargées ni déployées sur les clients. Cette situation vous laisse le temps suffisant pour préparer le déploiement des mises à jour logicielles, vérifier que les mises à jour logicielles répondant aux critères sont adéquates, puis activer ultérieurement le déploiement.  

4.  Sur la page Paramètres de déploiement, configurez les paramètres suivants :  

    -   **Utiliser Wake-on-LAN pour réveiller les clients pour les déploiements requis**: indique si l’éveil par appel réseau (Wake On LAN) doit être activé à l’échéance pour envoyer des paquets de mise en éveil aux ordinateurs qui nécessitent une ou plusieurs mises à jour logicielles du déploiement. Tous les ordinateurs en mode veille à l'échéance de l'installation sont mis en éveil pour que l'installation des mises à jour logicielles puisse démarrer. Les clients en mode veille qui ne nécessitent pas les mises à jour logicielles incluses dans le déploiement ne sont pas démarrés. Par défaut, ce paramètre n'est pas activé.  

        > [!WARNING]  
        >  Avant de pouvoir utiliser cette option, vous devez configurer les ordinateurs et les réseaux pour l'éveil par appel réseau.  

    -   **Niveau de détail**: indiquez le niveau de détail pour les messages d’état qui sont signalés par les ordinateurs clients.  

        > [!IMPORTANT]  
        >  Lorsque vous déployez des mises à jour de définitions, affectez au niveau de détails la valeur **Erreur uniquement** pour que le client envoie un message d'état uniquement lorsqu'une mise à jour de définition ne lui est pas remise. Sinon, le client envoie un grand nombre de messages d'état pouvant avoir un effet sur les performances du serveur de site.  

5.  Sur la page Calendrier de déploiement, configurez les paramètres suivants :  

    -   **Calendrier d’évaluation** : indiquez si Configuration Manager évalue la durée disponible et la date d’échéance de l’installation à l’heure UTC ou à l’heure locale de l’ordinateur exécutant la console Configuration Manager.  

        > [!NOTE]  
        >  Si vous sélectionnez l’heure locale, puis **Dès que possible** pour le **Temps disponible du logiciel** ou **Échéance d’installation**, l’heure actuelle sur l’ordinateur exécutant la console Configuration Manager est utilisée pour évaluer quand les mises à jour sont disponibles ou quand elles sont installées sur un client. Si le client est dans un autre fuseau horaire, ces actions se produisent quand l’heure du client atteint l’heure de l’évaluation.  

    -   **Temps disponible du logiciel**: sélectionnez l’un des paramètres suivants pour spécifier le moment où les mises à jour logicielles sont disponibles pour les clients :  

        -   **Dès que possible**: sélectionnez ce paramètre pour permettre aux ordinateurs clients d’accéder dès que possible aux mises à jour logicielles incluses dans le déploiement. Quand vous créez le déploiement avec ce paramètre sélectionné, Configuration Manager met à jour la stratégie client. Ensuite, au prochain cycle d'interrogation de la stratégie client, les clients prennent connaissance du déploiement et peuvent obtenir les mises à jour disponibles à l'installation.  

        -   **Heure spécifique**: sélectionnez ce paramètre pour permettre aux ordinateurs clients d’accéder aux mises à jour logicielles incluses dans le déploiement à une date et heure précises. Quand vous créez le déploiement avec ce paramètre activé, Configuration Manager met à jour la stratégie client. Ensuite, au prochain cycle d'interrogation de la stratégie client, les clients prennent connaissance du déploiement. Toutefois, les mises à jour logicielles incluses dans le déploiement ne sont pas disponibles à l'installation avant la date et l'heure configurées.  

    -   **Échéance d’installation**: sélectionnez l’un des paramètres suivants pour spécifier l’échéance d’installation des mises à jour logicielles incluses dans le déploiement :  

        -   **Dès que possible**: sélectionnez ce paramètre pour installer automatiquement les mises à jour logicielles incluses dans le déploiement dès que possible.  

        -   **Heure spécifique**: sélectionnez ce paramètre pour installer automatiquement les mises à jour logicielles incluses dans le déploiement à une date et une heure spécifiques. Configuration Manager détermine l’échéance d’installation des mises à jour logicielles en ajoutant l’intervalle **Heure spécifique** configuré au **Temps disponible du logiciel**.  

        > [!NOTE]  
        >  L'heure d'échéance de l'installation réelle est l'heure d'échéance affichée plus un laps de temps aléatoire pouvant atteindre 2 heures. Elle permet de réduire l'impact lié à l'installation simultanée, par tous les ordinateurs clients du regroupement de destination, des mises à jour logicielles incluses dans le déploiement.  
        >   
        >  Vous pouvez configurer le paramètre client **Agent ordinateur** , **Désactiver la randomisation des échéances** , pour désactiver le délai de randomisation de l’installation des mises à jour logicielles requises. Pour plus d’informations, voir [Computer Agent](../../core/clients/deploy/about-client-settings.md#computer-agent).  

6.  Sur la page Expérience utilisateur, configurez les paramètres suivants :  

    -   **Notifications à l’utilisateur**: indiquez si vous souhaitez afficher les notifications des mises à jour logicielles dans le Centre logiciel sur l’ordinateur client selon la valeur **Temps disponible du logiciel** configuré et si les notifications à l’utilisateur doivent s’afficher sur les ordinateurs clients.  

    -   **Comportement à l’échéance**: spécifiez le comportement qui doit se produire lorsque l’échéance est atteinte pour le déploiement des mises à jour logicielles. Indiquez si vous souhaitez installer les mises à jour logicielles incluses dans le déploiement. Spécifiez également si un redémarrage du système doit être effectué après l'installation des mises à jour logicielles, quelle que soit la fenêtre de maintenance configurée. Pour plus d’informations sur les fenêtres de maintenance, consultez [Guide pratique pour utiliser les fenêtres de maintenance](../../core/clients/manage/collections/use-maintenance-windows.md).  

    -   **Comportement de redémarrage du périphérique**: indiquez si le redémarrage du système sur les serveurs et stations de travail doit être supprimé une fois les mises à jour logicielles installées et si un redémarrage du système est nécessaire pour terminer l’installation.  

        > [!IMPORTANT]  
        >  La suppression du redémarrage système peut s'avérer utile dans les environnements de serveurs ou lorsque vous ne souhaitez pas que les ordinateurs qui installent les mises à jour logicielles redémarrent par défaut. Toutefois, elle peut laisser les ordinateurs dans un état non sécurisé, alors que l'autorisation d'un redémarrage forcé contribue à garantir l'exécution immédiate de l'installation des mises à jour logicielles.  

    -   **Traitement des filtres d’écriture pour les appareils Windows Embedded**: quand vous déployez des mises à jour logicielles sur des appareils Windows Embedded pour lesquels le filtre d’écriture est activé, vous pouvez choisir d’installer la mise à jour logicielle sur le segment de recouvrement temporaire et valider les modifications ultérieurement ou à l’échéance de l’installation ou bien pendant une fenêtre de maintenance. Lorsque vous validez des modifications à l'échéance de l'installation ou au cours d'une fenêtre de maintenance, un redémarrage est requis et les modifications sont conservées sur l'appareil.  

        > [!NOTE]  
        >  Lorsque vous déployez une mise à jour logicielle sur un appareil Windows Embedded, assurez-vous que l'appareil fait partie des membres d'un regroupement pour lequel une fenêtre de maintenance a été configurée.  

7.  Sur la page Alertes, configurez la manière dont Configuration Manager et System Center Operations Manager génèreront des alertes pour ce déploiement.  

    > [!WARNING]  
    >  Vous pouvez consulter les récentes alertes de mises à jour logicielles à partir du nœud **Mises à jour logicielles** dans l'espace de travail **Bibliothèque de logiciels** .  

8. Sur la page Paramètres de téléchargement, configurez les paramètres suivants :  

    -   Indiquez si le client va télécharger et installer les mises à jour logicielles quand il est connecté à un réseau lent ou utilise un emplacement de secours pour le contenu.  

    -   Indiquez si le client doit télécharger et installer les mises à jour logicielles à partir d'un point de distribution de secours quand le contenu pour les mises à jour logicielles n'est pas disponible sur un point de distribution préféré.  

    -   **Autoriser les clients à partager du contenu avec d’autres clients sur le même sous-réseau**: indiquez si vous souhaitez activer l’utilisation de BranchCache pour les téléchargements du contenu. Pour plus d’informations sur BrandCache, consultez [Concepts for content management](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#branchcache).  

    -   Indiquez si les clients connectés à l’intranet doivent télécharger les mises à jour logicielles à partir de Microsoft Update si elles ne sont pas disponibles sur des points de distribution.  

    -   Indiquez si vous souhaitez autoriser le téléchargement aux clients après l'échéance d'une installation lorsqu'ils utilisent des connexions Internet facturée à l'usage. Les fournisseurs Internet facturent parfois en fonction de la quantité de données que vous envoyez et recevez lorsque vous utilisez une connexion Internet facturée à l'usage.  

    > [!NOTE]  
    >  Les clients demandent l'emplacement du contenu à partir d'un point de gestion pour les mises à jour logicielles dans un déploiement. Le comportement de téléchargement dépend de la manière dont vous avez configuré le point de distribution, le package de déploiement et les paramètres sur cette page. Pour plus d'informations, voir [Content source location scenarios](../../core/plan-design/hierarchy/content-source-location-scenarios.md).  

Pour plus d’informations sur le processus de déploiement, consultez [Software update deployment process](../../sum/understand/software-updates-introduction.md#BKMK_DeploymentProcess).

## <a name="next-steps"></a>Étapes suivantes
[Surveiller les mises à jour logicielles](monitor-software-updates.md)



<!--HONumber=Dec16_HO3-->


