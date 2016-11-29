---
title: "Déployer des applications virtuelles App-V | System Center Configuration Manager"
description: "Examinez les éléments à prendre en compte quand vous créez et déployez des applications virtuelles."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ddcad9f2-a542-4079-83ca-007d7cb44995
caps.latest.revision: 11
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: d6e787d5968b281afe4e4b475287944563c8a77f


---
# <a name="deploy-app-v-virtual-applications-with-system-center-configuration-manager"></a>Déployer des applications virtuelles App-V avec System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

En plus des autres exigences et procédures System Center Configuration Manager à observer pour créer une application, vous devez aussi prendre en compte les éléments suivants au moment de créer et de déployer des applications virtuelles.  

 Lorsque vous utilisez Configuration Manager pour gérer des applications virtuelles, vous bénéficiez des avantages suivants :  

-   utilisation d'une infrastructure de gestion unique ;  

-   fonctionnalités d'évolutivité, de déploiement et de distribution de contenu, telles que les collections et l'affinité utilisateur/appareil ;  

-   fonctionnalités de gestion des applications avancées offertes par Configuration Manager ;  

-   utilisation des fonctionnalités de Configuration Manager, telles que le déploiement de système d’exploitation, l’inventaire logiciel et matériel, le contrôle de logiciel et Asset Intelligence, pour prendre en charge les applications virtuelles.  

Pour plus d'informations sur la création et le séquençage d'applications avec App-V, voir [Virtualisation de l'application](https://technet.microsoft.com/library/cc843848.aspx) dans la bibliothèque TechNet.  

Pour déployer des applications virtuelles sur des ordinateurs, vous devez avoir installé le client Configuration Manager et le client App-V sur vos ordinateurs. Les appareils clients peuvent consister en des ordinateurs de bureau et des ordinateurs portables, ainsi que des clients VDI (Virtual Desktop Infrastructure). Les logiciels clients Configuration Manager et App-V œuvrent ensemble pour remettre, localiser et lancer les packages d’applications virtuelles. Le client Configuration Manager gère la remise des packages d’applications virtuelles au client App-V. Le client App-V exécute l'application virtuelle sur le client.  

-   Pour déployer une application virtuelle, vous devez d'abord créer l'application virtuelle avec App-V Application Virtualization Sequencer. Le séquenceur surveille le processus d'installation et de configuration d'une application et enregistre les informations requises pour que l'application puisse s'exécuter dans un environnement virtuel. Vous pouvez également utiliser le séquenceur pour configurer quels fichiers et configurations sont applicables à tous les utilisateurs et quelles configurations les utilisateurs peuvent personnaliser.  

-   Quand vous séquencez une application, vous devez enregistrer le package sur un emplacement auquel Configuration Manager peut accéder. Vous pouvez ensuite créer un déploiement d'application qui contient cette application virtuelle.  

-   Configuration Manager ne prend pas en charge l’utilisation de la fonctionnalité de cache en lecture seule partagé d’App-V.  

-   Configuration Manager prend en charge la fonctionnalité de magasin de contenu partagé App-V 5.  

-   Lorsque vous créez un type de déploiement pour une application virtuelle, Configuration Manager crée le type de déploiement à l’aide du contenu du fichier de manifeste de l’application. Il s'agit d'un fichier XML qui contient des informations sur l'application virtuelle. De plus, Configuration Manager crée des spécifications pour le type de déploiement en fonction du contenu du fichier App-V .osd qui contient des informations sur les systèmes d’exploitation pris en charge pour l’application virtuelle.  

-   Pour déployer des applications virtuelles dans Configuration Manager, les ordinateurs clients doivent disposer au minimum du client App-V 4.6 SP1 ou d’une version ultérieure.  

-   Vous devez également mettre à jour le client App-V à jour avec le correctif décrit dans l'article [2645225](https://support.microsoft.com/kb/2645225)de la Base de connaissances pour pouvoir déployer les applications virtuelles correctement.  
  
-   Si vous utilisez des groupes de connexion dans Microsoft Application Virtualization 5.0, vos applications virtuelles déployées peuvent partager le même système de fichiers et le même Registre sur les ordinateurs clients. Contrairement aux applications virtuelles conventionnelles, ces applications peuvent partager des données entre elles. En outre, les groupes de connexion conservent les paramètres utilisateur pour les applications qu'ils contiennent. Les environnements virtuels App-V dans Configuration Manager permettent de configurer des groupes de connexion sur les ordinateurs clients. Les environnements virtuels sont créés ou modifiés sur les ordinateurs clients au moment de l'installation de l'application ou lorsque les clients réalisent ensuite une évaluation des applications installées. Vous pouvez hiérarchiser ces applications de telle sorte que lorsque plusieurs applications essaient de modifier un système de fichiers ou une valeur de Registre, l'application d'ordre le plus élevé est prioritaire. Pour plus d’informations, consultez [Créer des environnements virtuels App-V](../../apps/deploy-use/create-app-v-virtual-environments.md).  

##  <a name="supported-app-v-versions"></a>Versions d’App-V prises en charge  
 Configuration Manager prend en charge les versions suivantes d’App-V :  

-   **App-V 4.6 :** pour utiliser des applications virtuelles dans Configuration Manager, le client App-V 4.6 SP1, App-V 4.6 SP2 ou App-V 4.6 SP3 doit être installé sur les ordinateurs clients.  

     Vous devez également mettre à jour le client App-V 4.6 SP1 avec le correctif décrit dans l'article [2645225](http://go.microsoft.com/fwlink/p/?LinkId=237322) de la Base de connaissances pour pouvoir déployer correctement des applications virtuelles.  

-   **App-V 5, App-V 5.0 SP1, App-V 5.0 SP2, App-V 5.0 SP3 et App-V 5.1 :** pour App-V 5.0 SP2, vous devez installer le [Package de correctif logiciel 5](https://support.microsoft.com/en-us/kb/2963211) ou utiliser App-V 5.0 SP3.  

##  <a name="steps-to-manage-app-v-virtual-applications"></a>Étapes de gestion des applications virtuelles App-V  
 Pour gérer les applications virtuelles App-V, procédez comme suit :  

-   **Séquencement** : le séquencement est le processus qui consiste à convertir une application en application virtuelle à l'aide du séquenceur App-V.  

-   **Création d’applications Configuration Manager** : utilisez l’Assistant Création d’un type de déploiement pour importer l’application séquencée dans un type de déploiement Configuration Manager que vous pouvez ensuite ajouter à une application. Vous pouvez également créer des environnements virtuels qui permettent à plusieurs applications virtuelles de partager des paramètres.  

-   **Distribution** : la distribution est le processus qui consiste à mettre à disposition des applications App-V sur des points de distribution Configuration Manager.  

-   **Déploiement** : le déploiement est le processus qui consiste à mettre à disposition l'application sur des ordinateurs clients. On emploie le terme « émission en continu » dans une infrastructure complète App-V. Configuration Manager fournit deux options pour le déploiement d’applications virtuelles : **Émission en continu** et **Télécharger et exécuter**.  

##  <a name="configuration-manager-virtual-application-delivery-methods"></a>Méthodes de remise des applications virtuelles Configuration Manager  
 Configuration Manager prend en charge deux méthodes pour la remise des applications virtuelles aux clients : la remise sous forme d’émission en continu et la remise locale (Télécharger et exécuter) :  

-   **Remise sous forme d'émission en continu**  

     Lorsque vous utilisez Configuration Manager pour gérer le client App-V, il prend en charge la diffusion en continu des applications virtuelles via le protocole HTTP ou HTTPS à partir d’un point de distribution. L'émission en continu via HTTP ou HTTPS est activée par défaut et configurée dans la boîte de dialogue des propriétés du point de distribution. Lorsque vous déployez une application virtuelle sur des ordinateurs clients et qu’un utilisateur exécute l’application virtuelle, le client Configuration Manager contacte un point de gestion pour déterminer quel point de distribution utiliser ; l’application est ensuite émise en continu à partir du point de distribution.  

-   **Remise locale (Télécharger et exécuter)**  

     Lorsque vous utilisez cette méthode de remise, le client Configuration Manager télécharge dans un premier temps l’intégralité du package d’application virtuelle dans la mémoire cache du client Configuration Manager, puis il donne instruction au client App-V d’émettre l’application en continu de la mémoire cache Configuration Manager vers la mémoire cache App-V. Si vous déployez une application virtuelle sur des ordinateurs clients et que son contenu ne se trouve pas dans la mémoire cache App-V, le client App-V émet en continu le contenu de l’application de la mémoire cache du client Configuration Manager vers la mémoire cache App-V, puis il exécute l’application. Dès lors que l’application s’est exécutée correctement, vous pouvez configurer le client Configuration Manager afin que les anciennes versions du package soient supprimées au prochain cycle de suppression ou conservées dans la mémoire cache du client Configuration Manager.  

 Au moment de choisir la méthode de remise d’application virtuelle Configuration Manager à utiliser, mettez en balance les besoins limités en espace disque de la remise sous forme d’émission en continu et la disponibilité garantie des applications App-V offerte par la remise locale. La quantité d'espace disque accrue que nécessite le mode de remise locale sur le client peut être préférable à la diffusion en continu de la remise, dans le sens où l'application reste toujours accessible aux utilisateurs, où qu'ils se trouvent.  

 Pour choisir la méthode de remise la mieux adaptée à votre cas, aidez-vous des informations figurant dans les tableaux ci-dessous.  

 **Remise sous forme d'émission en continu**  

|Avantages|Inconvénients|  
|----------------|-------------------|  
|Cette méthode utilise les protocoles réseau standard pour émettre en continu le contenu des packages à partir de points de distribution.<br /><br /> Étant donné que les raccourcis de programmes représentant des applications virtuelles appellent une connexion au point de distribution, la remise des applications virtuelles s'effectue à la demande.<br /><br /> Cette méthode s'adresse particulièrement aux clients disposant d'une connexion haut débit aux points de distribution.<br /><br /> Les applications virtuelles mises à jour qui sont distribuées à l'échelle de l'entreprise sont disponibles dès lors que les clients reçoivent une stratégie les informant que la version actuelle est remplacée et que seules sont téléchargées les modifications apportées à la version précédente.<br /><br /> Les autorisations d'accès sont définies au niveau du point de distribution pour empêcher les utilisateurs d'accéder à des applications ou des packages non autorisés.|Les applications virtuelles ne sont pas émises en continu tant que l'utilisateur n'exécute pas l'application une première fois. Dans ce scénario, un utilisateur peut recevoir des raccourcis de programme d'applications virtuelles et se déconnecter ensuite du réseau avant d'avoir exécuté les applications virtuelles pour la première fois. Si l’utilisateur tente d’exécuter l’application virtuelle alors que le client est hors connexion, l’utilisateur obtient une erreur et ne peut pas exécuter l’application virtualisée, car aucun point de distribution Configuration Manager n’est disponible pour émettre en continu l’application. L'application sera indisponible tant que l'utilisateur ne se sera pas reconnecté au réseau et exécuté l'application.<br /><br /> Pour éviter ce problème, vous pouvez utiliser la méthode de remise locale pour remettre les applications virtuelles aux clients ou activer la gestion des clients via Internet pour une remise sous forme d'émission en continu.|  

 **Remise locale**  

|Avantages|Inconvénients|  
|----------------|-------------------|  
|La fonctionnalité de point de distribution standard est utilisée pour télécharger le package à l'aide du service de transfert intelligent en arrière-plan (BITS).<br /><br /> Le contenu des packages d'applications virtuelles est remis localement au client, ce qui signifie que les utilisateurs peuvent les exécuter lorsque leur ordinateur n'est pas connecté au réseau.<br /><br /> Cette méthode convient pour les connexions réseau lentes ou peu fiables et les ordinateurs qui ne se connectent qu'occasionnellement au réseau.<br /><br /> Configuration Manager fait appel à la compression différentielle à distance (RDC) pour envoyer aux clients uniquement les octets des fichiers qui ont été modifiés lors de la mise à jour du contenu des packages d’applications virtuelles. Le client Configuration Manager utilise RDC pour générer une nouvelle version d’un package d’application virtuelle basée sur la version actuelle du package et les modifications éventuelles envoyées au client.<br /><br /> Cette méthode assure une résilience des applications pour les utilisateurs mobiles ou déconnectés. Les administrateurs peuvent choisir de conserver le package dans la mémoire cache Configuration Manager après la remise si l’application virtuelle a été déployée avec une action d’installation. Le package contenu dans la mémoire cache du client Configuration Manager sert de source d’émission en continu locale et fiable pour le client App-V, qui l’extrait dans sa mémoire cache.|L’espace disque nécessaire sur le client lorsque l’application virtuelle est conservée dans la mémoire cache Configuration Manager représente jusqu’à deux fois la taille du package de l’application virtuelle.|  

 Vous pouvez aussi préinstaller des applications virtuelles sur un ordinateur pour ensuite créer une image de cet ordinateur qui sera déployée sur d'autres ordinateurs. Toutefois, si le package de l'application virtuelle a été créé sur un site différent, la réplication delta binaire ne sera pas utilisée pour télécharger les mises à jour de l'application. Cette option peut être utile dans une infrastructure VDI (Virtual Desktop Infrastructure) si vous voulez que les applications soient immédiatement disponibles et éviter aux utilisateurs de les télécharger après avoir ouvert une session.  

##  <a name="migrating-from-an-app-v-infrastructure-to-a-configuration-manager-and-app-v-infrastructure"></a>Migration d’une infrastructure App-V vers une infrastructure Configuration Manager et App-V  
 Pour planifier la migration d’une infrastructure App-V existante vers une gestion des applications virtuelles avec Configuration Manager, aidez-vous du tableau suivant.  

|Étape|Plus d'informations|  
|----------|----------------------|  
|Examinez vos applications virtuelles actuelles pour choisir celles que vous souhaitez migrer dans votre infrastructure Configuration Manager.|Aucune information supplémentaire.|  
|Déterminez vers quels utilisateurs et appareils les applications virtuelles seront déployées.|Créez des regroupements Configuration Manager afin de regrouper les utilisateurs et les appareils vers lesquels vous souhaitez déployer les applications virtuelles. Pour plus d’informations, consultez [Présentation des regroupements](/sccm/core/clients/manage/collections/introduction-to-collections).|  
|Migrez les groupes de connexion App-V 5 vers des environnements virtuels Configuration Manager.|Pour plus d’informations, consultez la section [Migrer les groupes de connexion App-V 5 vers des environnements virtuels Configuration Manager](/sccm/apps/get-started/deploying-app-v-virtual-applications#migrate-app-v-5-connection-groups-to-configuration-manager-virtual-environments) de cette rubrique.|  
|Déterminez si certaines de vos applications virtuelles existent en tant qu’applications complètes dans votre infrastructure Configuration Manager.|Pour une gestion simplifiée, vous pouvez ajouter l'application virtuelle en tant que nouveau type de déploiement à l'application complète existante. Pour plus d’informations sur la manière de créer des types de déploiement, consultez [Créer des applications](../../apps/deploy-use/create-applications.md).|  
|Créez des applications pour remplacer les packages App-V existants.|Pour plus d’informations sur la manière de créer des applications Configuration Manager, consultez [Introduction à la gestion des applications](/sccm/apps/understand/introduction-to-application-management) et [Créer des applications](../../apps/deploy-use/create-applications.md).|  
|Configuration Manager commence à gérer les applications virtuelles sur un client après le premier déploiement d’une application virtuelle. Après quoi, toutes les applications App-V présentes sur l’ordinateur doivent être gérées par Configuration Manager.|Aucune information supplémentaire.|  
|Distribuez le contenu aux points de distribution appropriés pour permettre la remise locale des applications.|Pour plus d’informations, consultez [Gérer le contenu et l’infrastructure de contenu](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).|  
|Déployez l’application sur les clients Configuration Manager.<br /><br /> Si l'application App-V a été créée avec une version antérieure du séquenceur qui ne crée pas de fichier manifeste XML, vous pouvez l'ouvrir et l'enregistrer dans une version plus récente du séquenceur pour créer le fichier. Ce fichier est nécessaire au déploiement d’applications virtuelles avec Configuration Manager.<br /><br /> App-V prend en charge les packages d'applications virtuelles créés avec le séquenceur SoftGrid version 4.1 SP1 ou 4.2.<br /><br /> Si les applications étaient déjà installées en local, vous devez les désinstaller avant de déployer une version virtuelle de l'application.|Pour plus d’informations, consultez [Déployer des applications](../../apps/deploy-use/deploy-applications.md).|  
|System Center Configuration Manager ne prend plus en charge l’utilisation de packages et de programmes contenant des applications virtuelles. Lorsque vous migrez de Configuration Manager 2007 à System Center Configuration Manager, Configuration Manager convertit ces packages en applications.<br /><br /> Les publications Configuration Manager 2007 sont converties vers les types de déploiement suivants :<br /><br /> - Migration de packages App-V sans publication : un type de déploiement utilisant les paramètres du type de déploiement par défaut.<br /><br /> - Migration de packages App-V avec une publication : un type de déploiement utilisant les mêmes paramètres que la <br />                publication de Configuration Manager 2007.<br /><br /> - Migration de packages App-V avec plusieurs publications : un type de déploiement pour chaque <br />                publication de Configuration Manager 2007, qui utilise les paramètres de cette publication.|Pour plus d’informations, consultez [Planification de la migration d’objets Configuration Manager vers System Center Configuration Manager](../../core/migration/planning-for-the-migration-of-objects.md).|  

##  <a name="migrate-app-v-5-connection-groups-to-configuration-manager-virtual-environments"></a>Migrer des groupes de connexion App-V 5 vers des environnements virtuels Configuration Manager  
 Dans Configuration Manager, les environnements virtuels App-V permettent aux applications virtuelles que vous avez déployées de partager les mêmes système de fichiers et Registre sur les ordinateurs clients. Par conséquent, contrairement aux applications virtuelles conventionnelles, ces applications peuvent partager des données entre elles. Les environnements virtuels sont créés ou modifiés sur les ordinateurs clients au moment de l'installation de l'application ou lorsque les clients réalisent ensuite une évaluation des applications installées. Les environnements virtuels sont similaires aux groupes de connexions d'App-V 5 en mode autonome.  

 Lorsque vous migrez des groupes de connexions de App-V 5 en mode autonome vers des environnements virtuels Configuration Manager, vous devez vous assurer que les groupes de connexions qui existent déjà sur les ordinateurs clients sont correctement gérés par Configuration Manager et que l’environnement utilisateur est préservé au sein de ces groupes de connexions.  

 Pour convertir des groupes de connexion App-V 5 dans des environnements virtuels Configuration Manager, exécutez la procédure suivante.  
  
### <a name="convert-app-v-5-connection-groups-to-configuration-manager-virtual-environments"></a>Convertir des groupes de connexion App-V 5 en environnements virtuels Configuration Manager  
  
1.  Créez des applications Configuration Manager pour toutes les applications qui existaient dans App-V.  

2.  Déployez les applications auprès des utilisateurs ou des appareils en utilisant l'objet de déploiement **Obligatoire**. Les déploiements auprès des utilisateurs doivent cibler les utilisateurs qui utilisaient l'application dans App-V. De même, les déploiements auprès des ordinateurs doivent cibler les ordinateurs qui disposaient de l'application dans App-V.  

3.  Une fois le déploiement terminé, créez des environnements virtuels qui correspondent aux groupes de connexion qui sont publiés dans la version autonome d'App-V. L'environnement virtuel doit contenir les mêmes packages, plus spécifiquement les types de déploiement App-V 5, dans le même ordre.  

Pour plus d’informations sur la création d’un environnement virtuel App-V, consultez [Guide pratique pour créer des environnements virtuels App-V](../../apps/deploy-use/create-app-v-virtual-environments.md).  

Vous pouvez également supprimer tous les groupes de connexion du client App-V avant de commencer à déployer des applications avec Configuration Manager. Dans ce cas, les paramètres éventuellement enregistrés par les utilisateurs dans les groupes de connexion App-V seront perdus.  

##  <a name="dynamic-suite-composition-in-app-v-46"></a>Composition de suite dynamique dans App-V 4.6  
 La fonctionnalité de composition de suite dynamique permet d'indiquer qu'un package d'application virtuelle possède une dépendance vis-à-vis d'un autre package d'application virtuelle. Lorsque l'application est exécutée, le client App-V héberge le package principal et le package dépendant dans le même environnement virtuel d'application.  

 Pour utiliser cette fonctionnalité avec Configuration Manager, les deux packages doivent être déployés et enregistrés avec le client App-V. Pour que le contenu du package dépendant soit hébergé localement sur l'ordinateur client, activez la remise locale pour le déploiement d'application (téléchargement et exécution).  

 Pour plus d'informations sur la composition de suite dynamique App-V, consultez la documentation d'App-V.  

##  <a name="convert-app-v-46-applications-to-app-v-5-applications"></a>Convertir des applications App-V 4.6 en applications App-V 5  
 Le format de package d'application a changé entre App-V 4.6 et App-V 5. Les applications qui ont été séquencées à l'aide d'App-V 4.6 ne sont plus prises en charge. Toutefois, App-V 5 dispose d'un outil de conversion de package que vous pouvez utiliser pour convertir des applications. Pour plus d'informations, voir la [documentation d'App-V 5](http://technet.microsoft.com/library/jj713472.aspx).  

 Suivez la procédure ci-dessous pour convertir des applications App-V 4.6 en applications App-V 5 :  

1.  Convertissez ou reséquencez les packages App-V 4.6 au format App-V 5.  

2.  Déployez le client App-V 5 sur les ordinateurs de votre hiérarchie.  

3.  Créez de nouvelles applications contenant les types de déploiement de vos applications App-V 5 et créez des règles de remplacement pour remplacer les applications App-V 4.6.  

4.  Créez des environnements virtuels si nécessaire.  

5.  Déployez les nouvelles applications App-V 5 sur les ordinateurs.  

##  <a name="user-and-deployment-configuration-files"></a>Fichiers de configuration d’utilisateur et de déploiement  
 Les fichiers de configuration d'utilisateur et de déploiement contiennent des paramètres qui influent sur le comportement d'une application. Vous pouvez utiliser ces fichiers pour modifier les paramètres d'application sans reséquencer l'application.  

 Une application App-V 5 standard peut contenir les fichiers suivants :  

-   Fichier de package d'application (.appv).  

-   Fichier de configuration d'utilisateur.  

-   Fichier de configuration de déploiement.  

 Le fichier de configuration d'utilisateur contient des paramètres qui s'appliquent uniquement à l'utilisateur connecté. Vous pouvez par exemple modifier les fichiers de configuration de façon à modifier les informations sur le raccourci d'application déployé auprès des utilisateurs. Vous pouvez également créer une application Configuration Manager possédant plusieurs types de déploiement (chacun d’entre eux pouvant contenir un fichier de configuration d’utilisateur spécifique) et utiliser des règles de spécification pour installer ces fichiers auprès des utilisateurs concernés.  

 Le fichier de configuration de déploiement contient des paramètres qui s'appliquent à l'ordinateur (paramètres de Registre, par exemple). Il peut également contenir des paramètres utilisateur, qui seront appliqués à tous les utilisateurs.  

 Si vous souhaitez déployer des applications virtuelles App-V 5 avec Configuration Manager, les trois fichiers doivent être présents dans le même dossier lorsque vous créez le type de déploiement App-V 5. Si le dossier contient plusieurs fichiers, Configuration Manager utilise le fichier le plus récent.  

 Pour plus d'informations, voir la [documentation d'App-V 5](http://technet.microsoft.com/library/jj713466.aspx).  

##  <a name="app-v-local-interaction"></a>Interaction locale App-V  
 Dans certains scénarios de déploiement d'application, des applications sont installées localement sur les ordinateurs clients, tandis que d'autres sont déployées sous forme d'applications virtuelles sur ces mêmes ordinateurs clients. Par défaut, les applications qui ont été installées localement ne peuvent pas voir les applications virtualisées ni communiquer directement avec elles. Il s'agit du comportement souhaité de la fonctionnalité d'isolation des applications fournie par App-V. L'interaction locale est une fonctionnalité du client App-V que vous pouvez activer pour chaque application, pour que les applications installées localement et exécutées sur un ordinateur client puissent voir les applications virtualisées et communiquer avec elles. Configuration Manager et App-V prennent intégralement en charge l’interaction locale.  

 Pour plus d'informations sur la fonctionnalité d'interaction locale d'App-V, voir la documentation d'App-V.  

##  <a name="app-v-5-shared-content-store"></a>Magasin de contenu partagé App-V 5  
 La fonctionnalité de magasin de contenu partagé App-V 5 est prise en charge par Configuration Manager. Pour plus d'informations, consultez [Planification du déploiement d'App-V 5.0 Sequencer et Client](http://technet.microsoft.com/library/jj713431.aspx).  

##  <a name="monitor-virtual-applications"></a>Surveiller les applications virtuelles  

### <a name="virtual-application-reports"></a>Rapports sur les applications virtuelles  
 Vous pouvez utiliser les rapports suivants pour surveiller App-V dans votre environnement Configuration Manager :  

|Nom du rapport|Description|  
|-----------------|-----------------|  
|Résultats de l'environnement virtuel App-V|Affiche des informations sur un environnement virtuel sélectionné qui se trouve dans un état spécifique pour un regroupement particulier (App-V 5 uniquement).|  
|Résultats de l'environnement virtuel App-V pour un composant|Affiche des informations sur un environnement virtuel sélectionné pour un composant spécifique et tous les types de déploiement pour l'environnement virtuel sélectionné (App-V 5 uniquement).|  
|État de l'environnement virtuel App-V|Affiche les informations de compatibilité d'un environnement virtuel sélectionné pour un regroupement particulier. La colonne **Conservé** de ce rapport indique les composants dans lesquels un environnement virtuel précédemment configuré n'est plus applicable, mais qui ont été conservés pour transférer les paramètres utilisateur des applications qui s'exécutent dans l'environnement virtuel (App-V 5 uniquement).|  
|Ordinateurs avec une application virtuelle spécifique|Affiche un récapitulatif des ordinateurs pour lesquels le raccourci de l'application App-V est spécifié comme utilisant Application Virtualization Management Sequencer (App-V 4.6 uniquement).|  
|Ordinateurs avec un package d'application virtuelle spécifique|Affiche la liste des ordinateurs sur lesquels le package d'application App-V spécifié est installé (App-V 4.6 uniquement).|  
|Total des instances de packages d'application virtuelle|Affiche le nombre total de packages d'application App-V détectés (App-V 4.6 uniquement).|  
|Total des instances d'applications virtuelles|Affiche le nombre total d'applications App-V détectées (App-V 4.6 uniquement).|  

## <a name="log-files"></a>Fichiers journaux  
 Configuration Manager enregistre dans des fichiers journaux diverses informations sur les déploiements d’applications virtuelles. Pour plus d’informations sur les fichiers journaux qui sont utilisés par les applications virtuelles et la gestion d’applications Configuration Manager, consultez [Fichiers journaux dans System Center Configuration Manager](../../core/plan-design/hierarchy/log-files.md).  

 Par ailleurs, vous trouverez les journaux du client App-V aux emplacements suivants :  

-   Windows Vista, Windows 7 et Windows 8 : **C:\ProgramData\Microsoft\Application Virtualization Client**  



<!--HONumber=Nov16_HO1-->


