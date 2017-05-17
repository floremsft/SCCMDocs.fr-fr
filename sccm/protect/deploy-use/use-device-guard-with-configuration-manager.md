---
title: "Gérer Windows Device Guard | Microsoft Docs"
description: "Découvrez comment gérer Windows Device Guard avec System Center Configuration Manager."
ms.custom: na
ms.date: 04/14/2017
ms.prod: configuration-manager
ms.reviewer: dudeso
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5e5d854c-9cc1-4dd8-b33f-0fcac675b395
caps.latest.revision: 13
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.translationtype: Human Translation
ms.sourcegitcommit: 49599f529bb409f40caf9057989762e759f1c0ac
ms.openlocfilehash: 113dddb2939fedf24e8d489ff4443bd5e3e72c65
ms.contentlocale: fr-fr
ms.lasthandoff: 05/17/2017


---


# <a name="device-guard-management-with-configuration-manager"></a>Gestion de Device Guard avec Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

## <a name="introduction"></a>Introduction
Windows Device Guard est un groupe de fonctionnalités Windows 10 qui sont conçues pour protéger les ordinateurs contre les logiciels malveillants et d’autres logiciels non autorisés. Il empêche le code malveillant de s’exécuter en s’assurant que seul le code approuvé, que vous connaissez, peut être exécuté.

Device Guard englobe les fonctionnalités de sécurité basées aussi bien sur des logiciels que sur des matériels. L’intégrité du code configurable est une couche de sécurité logicielle qui applique une liste explicite de logiciels autorisés à s’exécuter sur un ordinateur. Seule, l’intégrité du code configurable n’a pas de prérequis matériels ou logiciels. Les stratégies Device Guard déployées avec Configuration Manager activent une stratégie d’intégrité du code configurable sur les PC dans des collections ciblées qui satisfont les exigences décrites ci-dessous (version minimale de Windows et référence SKU). Si vous le souhaitez, la protection basée sur un hyperviseur des stratégies d’intégrité du code déployées via Configuration Manager peut être activée par le biais de la stratégie de groupe sur le matériel compatible.

Pour en savoir plus sur Device Guard, consultez [Guide de déploiement de Device Guard](https://technet.microsoft.com/itpro/windows/keep-secure/device-guard-deployment-guide).

Vous pouvez utiliser Configuration Manager pour déployer une stratégie Device Guard qui vous permet de configurer le mode dans lequel Device Guard s’exécute sur les PC dans une collection. 

Vous pouvez configurer l’un des modes suivants :

1.    **Mise en conformité activée** : seuls les exécutables approuvés sont autorisés à s’exécuter.
2.    **Audit uniquement** : autorisez tous les exécutables à s’exécuter, mais journalisez les exécutables non fiables qui s’exécutent dans le journal local des événements du client.

>[!TIP]
>Dans cette version de Configuration Manager, Device Guard est une fonctionnalité en préversion. Pour l’activer, consultez [Fonctionnalités en version préliminaire dans System Center Configuration Manager](/sccm/core/servers/manage/pre-release-features).

### <a name="what-can-run-when-you-deploy-a-device-guard-policy"></a>Quels composants peuvent s’exécuter lorsque vous déployez une stratégie Device Guard ?

Windows Device Guard vous permet de contrôler précisément les composants qui peuvent s’exécuter sur les ordinateurs que vous gérez. Cela peut être particulièrement utile pour les PC des services de haute sécurité, où il est vital que les logiciels indésirables ne soient pas autorisés à s’exécuter.

Lorsque vous déployez une stratégie, en règle générale, les exécutables suivants sont autorisés à s’exécuter :

- Composants du système d’exploitation Windows
- Pilotes du Centre de développement matériel (qui ont des signatures Windows Hardware Quality Labs)
- Applications du Windows Store
- Client Configuration Manager 
- Tous les logiciels déployés par le biais de Configuration Manager que le PC installe après le traitement de la stratégie Device Guard. 
- Mises à jour des composants Windows à partir de :
    - Windows Update
    - Windows Update for Business
    - Windows Server Update Services
    - Configuration Manager

>[!IMPORTANT]
>Ceux-ci n’incluent pas les logiciels qui ne sont **pas** intégrés à Windows et qui se mettent à jour automatiquement à partir d’Internet ou de mises à jour logicielles tierces en cas d’installation via un des mécanismes de mise à jour mentionnés ci-dessus, ou à partir d’Internet. Seules les modifications logicielles déployées au moyen du client Configuration Manager sont autorisées à s’exécuter.

## <a name="before-you-start"></a>Avant de commencer

Avant de configurer ou de déployer des stratégies Device Guard, lisez les informations suivantes :

- La gestion Device Guard est une fonctionnalité en préversion pour Configuration Manager. Elle est susceptible de changer.
- Pour utiliser Device Guard, les PC que vous gérez doivent exécuter Windows 10 pour les entreprises avec la mise à jour Creators Update ou ultérieure.
- Une fois qu’une stratégie est correctement traitée sur un PC client, Configuration Manager est configuré comme un programme d’installation managé sur ce client et les logiciels déployés via SCCM après le traitement de la stratégie sont automatiquement approuvés. Les logiciels installés par Configuration Manager avant le traitement de la stratégie Device Guard ne sont pas approuvés automatiquement.
- Dans cette préversion, une fois qu’un PC client reçoit le déploiement d’une stratégie Device Guard, il rend aléatoire le temps de traitement de cette stratégie sur une période de deux heures. 
- Les PC clients doivent être connectés à leur contrôleur de domaine pour que la stratégie Device Guard soit traitée correctement.
- L’évaluation de la conformité par défaut pour les stratégies Device Guard, configurable pendant le déploiement, s’effectue quotidiennement. Si des problèmes de traitement de la stratégie sont observés, il peut être avantageux de configurer une planification plus fréquente de l’évaluation de la conformité, par exemple toutes les heures. Cette planification détermine la fréquence à laquelle les clients réessayent de traiter une stratégie Device Guard en cas de défaillance.
- Quel que soit le mode de mise en conformité que vous sélectionnez lorsque vous déployez une stratégie Device Guard, les PC clients ne sont pas en mesure d’exécuter des applications HTML avec l’extension .hta.

## <a name="how-to-create-a-device-guard-policy"></a>Créer une stratégie Device Guard
1.    Dans la console Configuration Manager, cliquez sur **Ressources et Conformité**.
2.    Dans l’espace de travail **Ressources et Conformité** , développez **Endpoint Protection**, puis cliquez sur **Stratégies de protection des appareils**.
3.    Sous l’onglet **Accueil**, dans le groupe **Créer**, cliquez sur **Créer une stratégie Device Guard**.
4.    Dans la page **Général** de l’**Assistant Créer une stratégie Device Guard**, spécifiez les informations suivantes :
    - **Nom** : attribuez un nom unique à la stratégie Device Guard. 
    - **Description** : si vous le souhaitez, entrez une description pour faciliter l’identification de la stratégie dans la console Configuration Manager.
    - **Mode de mise en conformité** : choisissez une des méthodes de mise en conformité suivantes pour Device Guard sur le PC client.
        - **Mise en conformité activée** : seuls les exécutables approuvés sont autorisés à s’exécuter.
        - **Audit uniquement** : autorisez tous les exécutables à s’exécuter, mais journalisez les exécutables non fiables qui s’exécutent dans le journal local des événements du client.
5.    Cliquez sur **Suivant**, puis fermez l’Assistant.

## <a name="how-to-deploy-a-device-guard-policy"></a>Déployer une stratégie Device Guard
1.    Dans la console Configuration Manager, cliquez sur **Ressources et Conformité**.
2.    Dans l’espace de travail **Ressources et Conformité** , développez **Endpoint Protection**, puis cliquez sur **Stratégies de protection des appareils**.
3.    Dans la liste des stratégies, sélectionnez la stratégie que vous souhaitez déployer, puis, sous l’onglet **Accueil**, dans le groupe **Déploiement**, cliquez sur **Déployer**.
4.    Dans la boîte de dialogue **Déployer une stratégie Device Guard**, sélectionnez la collection dans laquelle vous souhaitez déployer la stratégie, configurez une planification de l’évaluation de la stratégie par les clients, puis indiquez si le client peut évaluer la stratégie en dehors des fenêtres de maintenance configurées.
5.    Lorsque vous avez terminé, cliquez sur **OK** pour déployer la stratégie. 

Une fois que la stratégie est traitée sur un PC client, un redémarrage est planifié sur ce client selon les **paramètres clients** relatifs au **redémarrage de l’ordinateur**.
**La stratégie ne prend pas effet tant que l’ordinateur client n’a pas redémarré.**

## <a name="how-to-monitor-a-device-guard-policy"></a>Surveiller une stratégie Device Guard

Utilisez les informations de la rubrique [Surveiller les paramètres de conformité](/sccm/compliance/deploy-use/monitor-compliance-settings) pour vous aider à surveiller la stratégie déployée afin de vérifier qu’elle a été correctement appliquée à tous les PC.

Utilisez le fichier journal suivant sur les PC clients pour le traitement d’une stratégie Device Guard :

**%WINDIR%\CCM\Logs\DeviceGuardHandler.log**

Pour vérifier le logiciel bloqué ou audité, consultez les journaux d’événements suivants du client local. Dans l’Observateur d’événements, les journaux pertinents sont les suivants :

1.    Pour le blocage et l’audit des fichiers exécutables, utilisez **Journaux des applications et des services** > **Microsoft** > **Windows** > **Intégrité du code** > **Opérationnel**.
2.    Pour le blocage et l’audit du programme d’installation Windows et des fichiers de script, utilisez **Journaux des applications et des services** > **Microsoft** > **Windows** > **AppLocker** > **MSI et Script**.

## <a name="security-and-privacy-information-for-device-guard"></a>Informations sur la sécurité et la confidentialité pour Device Guard

- Dans cette préversion, ne déployez pas de stratégies Device Guard avec le mode de mise en conformité **Audit uniquement** dans un environnement de production. Ce mode est conçu pour vous aider à tester la capacité dans un environnement de laboratoire uniquement.
- Les appareils qui ont une stratégie déployée en mode **Audit uniquement** ou **Mise en conformité activée** et qui n’ont pas encore été redémarrés pour appliquer la stratégie sont vulnérables aux logiciels non autorisés dont l’installation est en cours.
Dans ce cas, le logiciel peut continuer à être autorisé à s’exécuter même en cas de redémarrage de l’appareil ou il reçoit une stratégie en mode **Mise en conformité activée**.
- Pour vérifier que la stratégie Device Guard est effective, préparez l’appareil dans un environnement de laboratoire, déployez la stratégie **Mise en conformité activée**, puis redémarrez l’appareil avant de le donner à un utilisateur final.
- Ne déployez pas une stratégie **Mise en conformité activée** puis plus tard une stratégie **Audit uniquement** sur le même appareil. Il se peut dans ce cas que des logiciels non autorisés soient autorisés à s’exécuter.
- Lorsque vous utilisez Configuration Manager pour activer l’intégrité du code configurable sur les PC clients avec les stratégies Device Guard, notez que la stratégie n’empêche **pas** les utilisateurs disposant de droits d’administrateur local de contourner la stratégie Device Guard ou d’exécuter des logiciels non autorisés. 
- La seule façon d’empêcher les utilisateurs dotés de droits d’administrateur local de désactiver l’intégrité du code configurable consiste à déployer une stratégie binaire signée, ce qui est possible via la stratégie de groupe, mais n’est pas actuellement pris en charge dans Configuration Manager.
- Le paramétrage de Configuration Manager en tant que programme d’installation managé sur les PC clients utilise la stratégie AppLocker. AppLocker est utilisé uniquement pour identifier les programmes d’installation managés et la mise en conformité se produit avec l’intégrité du code configurable. 





