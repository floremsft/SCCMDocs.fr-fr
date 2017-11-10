---
title: Planifier la passerelle de gestion cloud
titleSuffix: Configuration Manager
description: 
ms.date: 10/06/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: 2dc8c9f1-4176-4e35-9794-f44b15f4e55f
author: arob98
ms.author: angrobe
manager: angrobe
ms.openlocfilehash: ffe7b2aa025b20d5b1d1a718e0eaa045817a66ee
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/12/2017
---
# <a name="plan-for-the-cloud-management-gateway-in-configuration-manager"></a>Planifier la passerelle de gestion cloud dans Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

À compter de la version 1610, la passerelle de gestion cloud fournit un moyen simple de gérer les clients Configuration Manager sur Internet. Le service de passerelle de gestion cloud est déployé sur Microsoft Azure et nécessite un abonnement Azure. Il se connecte à votre infrastructure Configuration Manager locale à l’aide d’un nouveau rôle appelé point de connexion de la passerelle de gestion cloud. Une fois le service déployé et configuré, les clients peuvent accéder aux rôles de système de site Configuration Manager locaux, qu’ils se trouvent sur le réseau privé interne ou sur Internet.

> [!TIP]  
> Depuis la version 1610, la passerelle de gestion cloud est une fonctionnalité en préversion. Pour savoir comment l’activer, consultez [Utiliser des fonctionnalités de préversion des mises à jour](/sccm/core/servers/manage/pre-release-features).

Utilisez la console Configuration Manager pour déployer le service sur Azure, ajouter le rôle de point de connexion de la passerelle de gestion cloud et configurer les rôles de système de site pour autoriser le trafic de la passerelle de gestion cloud. La passerelle de gestion cloud ne prend actuellement en charge que les rôles de point de gestion et de point de mise à jour logicielle.

Les certificats clients et les certificats Secure Socket Layer (SSL) sont requis pour authentifier les ordinateurs et chiffrer les communications entre les différents niveaux du service. En règle générale, les ordinateurs clients reçoivent un certificat client via la mise en œuvre d’une stratégie de groupe. Pour chiffrer le trafic entre les clients et le serveur de système de site hébergeant les rôles, vous devez créer un certificat SSL personnalisé à partir de l’autorité de certification. Vous devez également configurer un certificat de gestion sur Azure pour permettre à Configuration Manager de déployer le service de passerelle de gestion cloud.

## <a name="requirements-for-cloud-management-gateway"></a>Exigences pour la passerelle de gestion cloud

-   Les ordinateurs clients et le serveur de système de site doivent exécuter le point de connexion de la passerelle de gestion cloud.

-   Certificats SSL personnalisés provenant de l’autorité de certification interne : utilisés pour chiffrer la communication en provenance des ordinateurs clients et authentifier l’identité du service de passerelle de gestion cloud.

-   Abonnement Azure pour les services cloud.

-   Certificat de gestion Azure : utilisé pour authentifier Configuration Manager auprès d’Azure.

## <a name="specifications-for-cloud-management-gateway"></a>Spécifications de la passerelle de gestion cloud

- Chaque instance de la passerelle de gestion cloud prend en charge 4 000 clients.
- Nous vous recommandons de créer au moins deux instances de la passerelle de gestion cloud pour améliorer la disponibilité.
- La passerelle de gestion cloud ne prend en charge que les rôles de point de gestion et de point de mise à jour logicielle.
-   Les fonctionnalités de Configuration Manager suivantes ne sont pas actuellement prises en charge pour la passerelle de gestion cloud :

    -   Déploiement des clients
    -   Attribution automatique du site
    -   Catalogue d’applications (notamment les demandes d’approbation de logiciels)
    -   Déploiement de système d’exploitation (OSD) complet
    -   Séquences de tâches (toutes)
    -   Console Configuration Manager
    -   outils de contrôle à distance.
    -   Site web de création de rapports
    -   Éveil par appel réseau
    -   Clients Mac, Linux et UNIX
    -   Azure Resource Manager
    -   Cache d’homologue
    -   Gestion des appareils mobiles (MDM) locale

## <a name="cost-of-cloud-management-gateway"></a>Coût de la passerelle de gestion cloud

>[!IMPORTANT]
>Les informations suivantes sur les coûts sont données à titre d’estimation seulement. Votre environnement peut avoir d’autres variables qui affectent le coût total d’utilisation de la passerelle de gestion cloud.

La passerelle de gestion cloud utilise les fonctionnalités Microsoft Azure suivantes, celles-ci donnant lieu à des frais qui sont imputés au compte d’abonnement Azure :

-   Machine virtuelle

    -   La passerelle de gestion cloud nécessite actuellement une machine virtuelle Standard\_A2. Quand vous créez le service, vous pouvez sélectionner le nombre de machines virtuelles pour assurer la prise en charge du service (une machine virtuelle par défaut).

    -   À titre d’estimation seulement, une machine virtuelle Azure Standard\_A2 peut prendre en charge environ 2 000 clients basés sur Internet en même temps.

    -   Pour vous aider à déterminer les coûts potentiels, consultez la [calculatrice de prix Azure](https://azure.microsoft.com/en-us/pricing/calculator/).

      >[!NOTE]
      >Les coûts des machines virtuelles varient selon la région.

-   Transfert de données sortantes

    -   Le flux de données sortantes en provenance du service génère des frais. Pour vous aider à déterminer les coûts potentiels, consultez les [détails de la tarification de la bande passante](https://azure.microsoft.com/pricing/details/bandwidth/).

    -   À titre d’estimation seulement, prévoyez environ 100 Mo par client par mois pour les clients basés sur Internet effectuant des actualisations de la stratégie toutes les heures.

    >[!NOTE]
    > Si vous réalisez d’autres actions prises en charge par le biais de la passerelle de gestion cloud (comme le déploiement de mises à jour logicielles ou d’applications), la quantité de données sortantes en provenance d’Azure augmente.

-   Stockage de contenu

    -   Les clients basés sur Internet qui sont gérés avec la passerelle de gestion cloud reçoivent le contenu des mises à jour logicielles de Windows Update sans frais.

    -   Tout autre contenu nécessaire (comme des applications) doit être distribué à un point de distribution cloud. À l’heure actuelle, la passerelle de gestion cloud ne prend en charge que le point de distribution cloud pour l’envoi de contenu aux clients.

    - Pour plus de détails, consultez le coût d’utilisation d’une [distribution cloud](/sccm/core/plan-design/hierarchy/use-a-cloud-based-distribution-point#cost-of-using-cloud-based-distribution).

## <a name="frequently-asked-questions-about-the-cloud-management-gateway-cmg"></a>Forum aux questions sur la passerelle de gestion cloud (CMG, Cloud Management Gateway)

### <a name="why-use-the-cloud-management-gateway"></a>Pourquoi utiliser la passerelle de gestion cloud ?

Utilisez ce rôle pour simplifier la gestion des clients basés Internet en trois étapes à partir de la console Configuration Manager.

1. Déployez la passerelle CMG sur Azure à l’aide de l[’Assistant Créer une passerelle de gestion cloud](/sccm/core/clients/manage/setup-cloud-management-gateway).
2. Configurez le rôle de système de site du [point de connexion de la passerelle de gestion cloud](/sccm/core/servers/deploy/configure/install-site-system-roles).
3. [Configurez les rôles pour le trafic de la passerelle de gestion cloud](/sccm/core/clients/manage/setup-cloud-management-gateway#step-7-configure-roles-for-cloud-management-gateway-traffic), notamment le point de gestion et le point de mise à jour logicielle.

### <a name="how-does-the-cloud-management-gateway-work"></a>Comment la passerelle de gestion cloud fonctionne-t-elle ?

- Le point de connexion de la passerelle de gestion cloud permet une connexion stable et très performante depuis Internet vers la passerelle de gestion cloud.
- Configuration Manager transmet les paramètres à la passerelle CMG, notamment les informations de connexion et les paramètres de sécurité.
- La passerelle CMG authentifie et transfère les demandes des clients Configuration Manager au point de connexion de la passerelle de gestion cloud. Ces demandes sont transmises aux rôles dans le réseau d’entreprise selon les mappages d’URL.

### <a name="how-is-the-cloud-management-gateway-deployed"></a>Comment la passerelle de gestion cloud est-elle déployée ?

Le composant de gestionnaire de service cloud sur le point de connexion de service gère toutes les tâches de déploiement CMG. En outre, il surveille et transmet les informations d’intégrité du service et de journalisation à partir d’Azure AD. Vérifiez que votre point de connexion de service est en [mode en ligne](/sccm/core/servers/deploy/configure/about-the-service-connection-point#bkmk_modes).

#### <a name="certificate-requirements"></a>Conditions de certificat

Les certificats suivants sont nécessaires pour sécuriser la passerelle de gestion cloud :

- **Certificat de gestion** - Vous pouvez utiliser tout type de certificat, y compris des certificats auto-signés. Vous pouvez utiliser un certificat public téléchargé sur Azure AD ou un [fichier PFX avec une clé privée](/sccm/mdm/deploy-use/create-pfx-certificate-profiles) importé dans Configuration Manager pour permettre l’authentification auprès d’Azure AD.
- **Certificat de service Web** - Nous vous recommandons d’utiliser un certificat public délivré par une autorité de certification afin d’obtenir une approbation native par les clients. Créez l’enregistrement CName dans le bureau d’enregistrement DNS public. Les certificats génériques ne sont pas pris en charge.
- **Certificats racine/SubCA téléchargés sur la passerelle CMG** - La passerelle CMG doit effectuer une validation complète de la chaîne sur les certificats client PKI. Si vous utilisez une autorité de certification d’entreprise pour émettre des certificats client PKI et que leur autorité de certification racine ou secondaire n’est pas disponible sur Internet, vous devez également télécharger ces certificats sur la passerelle CMG.

#### <a name="deployment-process"></a>Processus de déploiement

Le déploiement s’effectue en deux phases :

- Déployer le service cloud
    - Télécharger votre fichier de [schéma de définition du service Azure](https://msdn.microsoft.com/library/azure/ee758711.aspx) (csdef)
    - Téléchargez votre fichier de [schéma de configuration du service Azure](https://msdn.microsoft.com/library/azure/ee758710.aspx) (cscfg).
- Configurer le composant CMG sur votre serveur Azure AD et configurer les points de terminaison, les gestionnaires HTTP et les services dans Internet Information Services (IIS)

Si vous modifiez la configuration de la passerelle CMG, un déploiement de configuration est lancé sur CMG.

### <a name="where-do-i-set-up-the-cloud-management-gateway"></a>Où puis-je configurer la passerelle de gestion cloud ?
Vous pouvez créer la passerelle de gestion cloud sur le site de niveau supérieur de votre hiérarchie. S’il s’agit d’un site d’administration centrale, vous pouvez créer des points de connexion de passerelle de gestion cloud sur les sites principaux enfants.

### <a name="how-does-the-cloud-management-gateway-help-ensure-security"></a>Comment la passerelle de gestion cloud garantit-elle la sécurité ?

La passerelle CMG garantit la sécurité de plusieurs façons :

- Accepte et gère les connexions à partir des points de connexion CMG, y compris l’authentification mutuelle SSL à l’aide de certificats internes et d’ID de connexion.
- Accepte et transfère les demandes des clients
    - Authentifie au préalable les connexions à l’aide d’un protocole SSL mutuel sur le certificat client PKI.
    - La liste des certificats de confiance vérifie la racine du certificat client PKI. Vous pouvez spécifier ce paramètre dans les paramètres de communication du client au niveau des propriétés du site. Effectue également la même validation que le point de gestion pour le client.
    - Valide les URL reçues
    - Filtre les URL reçues pour vérifier si un point de connexion CMG peut répondre à la demande de l’URL.  
    - Vérifie la longueur du contenu pour chaque point de terminaison de publication.
    - Utilise un système de tourniquet (round-robin) pour équilibrer la charge entre les points de connexion CMG du même site.

- Sécurise le point de connexion CMG
    - Crée des connexions HTTP/TCP cohérentes pour toutes les instances virtuelles de la passerelle CMG qui se connecte. Vérifie et gère les connexions toutes les minutes.
    - Authentifie mutuellement la connexion SSL avec la passerelle de gestion cloud à l’aide de certificats internes.
    - Transfère les requêtes HTTP basées sur des mappages d’URL.
    - Indique l’état de la connexion pour afficher l’état d’intégrité du service d’administration.
    - Indique le rapport de trafic du point de terminaison pour chaque point de terminaison toutes les cinq minutes.

- Sécurisez les rôles du côté du client Configuration Manager du point de terminaison de publication, notamment le point de gestion et les points de terminaison hôtes de mise à jour logicielle dans IIS afin de traiter les demandes des clients. Chaque point de terminaison publié sur la passerelle CMG comporte un mappage d’URL.
L’URL externe est celle que le client utilise pour communiquer avec la passerelle CMG.
L’URL interne est le point de connexion CMG utilisé pour transférer les demandes vers le serveur interne.

#### <a name="example"></a>Exemple :
Lorsque vous activez le trafic CMG sur un point de gestion, Configuration Manager crée un ensemble de mappages d’URL en interne pour chaque serveur de point de gestion, par exemple ccm_system, ccm_incoming et sms_mp.
L’URL externe du point de terminaison du point de gestion ccm_system se présente sous la forme **https://<CMG service name>/CCM_Proxy_MutualAuth/<MP Role ID>/CCM_System**.
L’URL est unique pour chaque point de gestion. Le client Configuration Manager ajoute ensuite le nom du point de gestion de la passerelle CMG, par exemple **<CMG service name>/CCM_Proxy_MutualAuth/<MP Role ID>** dans sa liste de points de gestion internet.
Toutes les URL externes publiées sont téléchargées automatiquement sur la passerelle CMG, qui peut alors filtrer ces URL. Tous les mappages d’URL sont répliqués vers un point de connexion CMG afin de pouvoir transférer ces URL vers des serveurs internes en fonction de l’URL externe demandée par le client.

### <a name="what-ports-are-used-by-the-cloud-management-gateway"></a>Quels sont les ports utilisés par la passerelle de gestion cloud ?

- Aucun port entrant n’est nécessaire pour le réseau local. Le déploiement de CMG crée automatiquement un ensemble de passerelles CMG.
- Outre le port 443, certains ports sortants sont requis par le point de connexion CMG.

|||||
|-|-|-|-|
|Flux de données|Serveur|Ports du serveur|Client|
|Déploiement CMG|Azure|443|Point de connexion de service Configuration Manager|
|Générer le canal CMG|CMG|Instance de machine virtuelle : 1 Port : 443<br>Instance de machine virtuelle : N (N>=2 et N<= 16) Ports : 10124~N 10140~N|Point de connexion CMG|
|Client vers CMG|CMG|443|Client|
|Connecteur CMG au rôle de site (actuellement les points de gestion et les points de mise à jour logicielle)|Rôle de site|Protocole/ports configurés sur le rôle de site|Point de connexion CMG|

### <a name="how-can-you-improve-performance-of-the-cloud-management-gateway"></a>Comment améliorer les performances de la passerelle de gestion cloud ?

- Si possible, configurez la passerelle CMG, le point de connexion CMG et le serveur de site Configuration Manager dans la même région pour réduire la latence du réseau.
- Actuellement, la connexion entre le client Configuration Manager et la passerelle CMG ne tient pas compte de la région.
- Pour obtenir une disponibilité optimale, nous vous recommandons d’utiliser au moins deux instances virtuelles de la passerelle CMG et deux points de connexion CMG par site
- Vous pouvez faire évoluer la passerelle CMG pour prendre en charge davantage de clients en ajoutant d’autres instances de machine virtuelle. Leur charge est équilibrée par l’équilibreur de charge Azure AD.
- Créez plusieurs points de connexion CMG pour répartir la charge entre ces points. La passerelle CMG acheminera via un système de tourniquet (round-robin) le trafic vers ses points de connexion CMG.
- Le nombre de clients pris en charge par instance de machine virtuelle CMG est de 6 000 dans la version 1702. Lorsque le canal CMG est soumis à une forte charge, la demande est toujours gérée mais son traitement peut prendre plus longtemps que prévu.

### <a name="how-can-you-monitor-the-cloud-management-gateway"></a>Comment surveiller la passerelle de gestion cloud ?

Pour résoudre les problèmes de déploiement, utilisez **CloudMgr.log** et **CMGSetup.log**.
Pour la résolution des problèmes d’intégrité du service, utilisez **CMGService.log** et **SMS_CLOUD_PROXYCONNECTOR.log**.
Pour résoudre les problèmes de trafic client, utilisez **CMGHttpHandler.log**, **CMGService.log** et **SMS_CLOUD_PROXYCONNECTOR.log**.

Pour obtenir la liste de tous les fichiers journaux liés à la passerelle CMG, consultez [Fichiers journaux dans Configuration Manager](https://docs.microsoft.com/sccm/core/plan-design/hierarchy/log-files#cloud-management-gateway)

## <a name="next-steps"></a>Étapes suivantes

[Configurer la passerelle de gestion cloud](setup-cloud-management-gateway.md)
