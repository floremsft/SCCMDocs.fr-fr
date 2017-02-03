---
title: Planifier la passerelle de gestion cloud | Microsoft Docs
description: 
ms.date: 12/19/2016
ms.prod: configuration-manager
ms.technology:
- configmgr-client
ms.assetid: 2dc8c9f1-4176-4e35-9794-f44b15f4e55f
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1df2d8bcd73633ac1d37cc3ef31343be9c5bc95d
ms.openlocfilehash: 6e2895565e868eb80a8f4f4b46b8a28eb4961e28

---

# <a name="plan-for-cloud-management-gateway-in-configuration-manager"></a>Configurer la passerelle de gestion cloud dans Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

À compter de la version 1610, la passerelle de gestion cloud fournit un moyen simple de gérer les clients Configuration Manager sur Internet. Le service de passerelle de gestion cloud est déployé sur Microsoft Azure et nécessite un abonnement Azure. Il se connecte à votre infrastructure Configuration Manager locale à l’aide d’un nouveau rôle appelé point de connexion de la passerelle de gestion cloud. Une fois le service déployé et configuré, les clients peuvent accéder aux rôles de système de site Configuration Manager locaux, qu’ils se trouvent sur le réseau privé interne ou sur Internet.

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

    -   Mise à niveau et déploiement du client par le biais de l’installation Push du client
    -   Attribution automatique du site
    -   Stratégies utilisateur
    -   Catalogue d’applications (notamment les demandes d’approbation de logiciels)
    -   Déploiement de système d’exploitation (OSD) complet
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
>Les informations sur les coûts fournies ci-dessous sont données à titre d’estimation seulement. Votre environnement peut avoir d’autres variables qui affectent le coût total d’utilisation de la passerelle de gestion cloud.

La passerelle de gestion cloud utilise les fonctionnalités Microsoft Azure suivantes, celles-ci donnant lieu à des frais qui sont imputés au compte d’abonnement Azure :

-   Machine virtuelle

    -   La passerelle de gestion cloud nécessite actuellement une machine virtuelle Standard\_A2. Quand vous créez le service, vous pouvez sélectionner le nombre de machines virtuelles pour assurer la prise en charge du service (une machine virtuelle par défaut).

    -   À titre d’estimation seulement, une machine virtuelle Azure Standard\_A2 peut prendre en charge environ 2 000 clients basés sur Internet en même temps.

    -   Pour vous aider à déterminer les coûts potentiels, consultez la [calculatrice de prix Azure](https://azure.microsoft.com/en-us/pricing/calculator/).

      >[!NOTE]
      >Les coûts des machines virtuelles varient selon la région.

-   Transfert de données sortantes

    -   Le flux de données sortantes en provenance du service génère des frais. Pour vous aider à déterminer les coûts potentiels, consultez les [détails de la tarification de la bande passante](https://azure.microsoft.com/en-us/pricing/details/bandwidth/).

    -   À titre d’estimation seulement, prévoyez environ 100 Mo par client par mois pour les clients basés sur Internet effectuant des actualisations de la stratégie toutes les heures.

    >[!NOTE]
    > Si vous réalisez d’autres actions prises en charge par le biais de la passerelle de gestion cloud (comme le déploiement de mises à jour logicielles ou d’applications), la quantité de données sortantes en provenance d’Azure augmente.

-   Stockage de contenu

    -   Les clients basés sur Internet qui sont gérés avec la passerelle de gestion cloud reçoivent le contenu des mises à jour logicielles de Windows Update sans frais.

    -   Tout autre contenu nécessaire (comme des applications) doit être distribué à un point de distribution cloud. À l’heure actuelle, la passerelle de gestion cloud ne prend en charge que le point de distribution cloud pour l’envoi de contenu aux clients.

    - Pour plus de détails, consultez le coût d’utilisation d’une [distribution cloud](/sccm/core/plan-design/hierarchy/use-a-cloud-based-distribution-point#cost-of-using-cloud-based-distribution).

## <a name="next-steps"></a>Étapes suivantes

[Configurer la passerelle de gestion cloud](setup-cloud-management-gateway.md)



<!--HONumber=Dec16_HO3-->


