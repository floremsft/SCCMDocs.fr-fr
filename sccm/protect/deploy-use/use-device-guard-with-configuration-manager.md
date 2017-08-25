---
title: "Gérer Windows Device Guard | Microsoft Docs"
description: "Découvrez comment gérer Windows Device Guard avec System Center Configuration Manager."
ms.custom: na
ms.date: 07/31/2017
ms.prod: configuration-manager
ms.reviewer: dudeso
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5e5d854c-9cc1-4dd8-b33f-0fcac675b395
caps.latest.revision: "13"
caps.handback.revision: "0"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 3921748d3c99c2a35b670f3ca121dc7ab92d43bc
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/07/2017
---
# <a name="device-guard-management-with-configuration-manager"></a>Gestion de Device Guard avec Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

## <a name="introduction"></a>Introduction
Device Guard est un groupe de fonctionnalités Windows 10 qui sont conçues pour protéger les ordinateurs contre les logiciels malveillants et d’autres logiciels non autorisés. Il empêche le code malveillant de s’exécuter en s’assurant que seul le code approuvé, que vous connaissez, peut être exécuté.

Device Guard englobe les fonctionnalités de sécurité basées aussi bien sur des logiciels que sur du matériel. L’intégrité du code configurable est une couche de sécurité logicielle qui applique une liste explicite de logiciels autorisés à s’exécuter sur un PC. Seule, l’intégrité du code configurable n’a pas de prérequis matériels ou logiciels. Les stratégies Device Guard déployées avec Configuration Manager activent une stratégie d’intégrité du code configurable sur les PC de collections ciblées qui répondent aux exigences décrites dans cette rubrique (version minimale de Windows et référence SKU). Si vous le souhaitez, vous pouvez activer la protection basée sur un hyperviseur des stratégies d’intégrité du code déployées par le biais de Configuration Manager au moyen de la stratégie de groupe sur le matériel compatible.

Pour en savoir plus sur Device Guard, consultez le [Guide de déploiement de Device Guard](https://technet.microsoft.com/itpro/windows/keep-secure/device-guard-deployment-guide).

## <a name="using-device-guard-with-configuration-manager"></a>Utilisation de Device Guard avec Configuration Manager

Vous pouvez utiliser Configuration Manager pour déployer une stratégie Device Guard qui vous permet de configurer le mode dans lequel Device Guard s’exécute sur les PC d’une collection. 

Vous pouvez configurer l’un des modes suivants :

1.  **Mise en conformité activée** : seuls les exécutables approuvés sont autorisés à s’exécuter.
2.  **Audit uniquement** : autorisez tous les exécutables à s’exécuter, mais journalisez les exécutables non fiables qui s’exécutent dans le journal local des événements du client.

>[!TIP]
>Dans cette version de Configuration Manager, Device Guard est une fonctionnalité en préversion. Pour l’activer, consultez [Fonctionnalités en version préliminaire dans System Center Configuration Manager](/sccm/core/servers/manage/pre-release-features).

## <a name="what-can-run-when-you-deploy-a-device-guard-policy"></a>Quels composants peuvent s’exécuter lorsque vous déployez une stratégie Device Guard ?

Windows Device Guard vous permet de contrôler précisément les composants qui peuvent s’exécuter sur les ordinateurs que vous gérez. Cette fonctionnalité peut être utile pour les PC des services de haute sécurité, où il est vital que les logiciels indésirables ne puissent pas s’exécuter.

Quand vous déployez une stratégie, les exécutables suivants peuvent généralement s’exécuter :

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
>Ces éléments n’incluent pas les logiciels qui *ne sont pas* intégrés à Windows et qui se mettent à jour automatiquement à partir d’Internet ou de mises à jour logicielles tierces en cas d’installation par le biais d’un des mécanismes de mise à jour mentionnés précédemment, ou à partir d’Internet. Seuls les changements logiciels déployés au moyen du client Configuration Manager peuvent s’exécuter.

## <a name="before-you-start"></a>Avant de commencer

Avant de configurer ou de déployer des stratégies Device Guard, lisez les informations suivantes :

- La gestion Device Guard est une fonctionnalité en préversion pour Configuration Manager. Elle est susceptible de changer.
- Pour utiliser Device Guard avec Configuration Manager, les PC que vous gérez doivent exécuter Windows 10 Entreprise version 1703 ou ultérieure.
- Une fois qu’une stratégie est traitée sur un PC client, Configuration Manager est configuré comme un programme d’installation managé sur ce client et les logiciels déployés par le biais de SCCM après le traitement de la stratégie sont automatiquement approuvés. Les logiciels installés par Configuration Manager avant le traitement de la stratégie Device Guard ne sont pas approuvés automatiquement.
- Les PC clients doivent être connectés à leur contrôleur de domaine pour que la stratégie Device Guard soit traitée correctement.
- L’évaluation de la conformité par défaut pour les stratégies Device Guard, configurable pendant le déploiement, s’effectue quotidiennement. Si des problèmes de traitement de la stratégie sont observés, il peut être avantageux de configurer une planification plus fréquente de l’évaluation de la conformité, par exemple toutes les heures. Cette planification détermine la fréquence à laquelle les clients réessayent de traiter une stratégie Device Guard en cas d’échec.
- Quel que soit le mode de mise en conformité que vous sélectionnez quand vous déployez une stratégie Device Guard, les PC clients ne peuvent pas exécuter des applications HTML avec l’extension .hta.

## <a name="how-to-create-a-device-guard-policy"></a>Créer une stratégie Device Guard
1.  Dans la console Configuration Manager, cliquez sur **Ressources et Conformité**.
2.  Dans l’espace de travail **Ressources et Conformité** , développez **Endpoint Protection**, puis cliquez sur **Stratégies de protection des appareils**.
3.  Sous l’onglet **Accueil**, dans le groupe **Créer**, cliquez sur **Créer une stratégie Device Guard**.
4.  Dans la page **Général** de l’**Assistant Création d’une stratégie Device Guard**, spécifiez les paramètres suivants :
    - **Nom** : attribuez un nom unique à la stratégie Device Guard. 
    - **Description** : si vous le souhaitez, entrez une description pour faciliter l’identification de la stratégie dans la console Configuration Manager.
    - **Mode de mise en conformité** : choisissez une des méthodes de mise en conformité suivantes pour Device Guard sur le PC client.
        - **Mise en conformité activée** : seuls les exécutables approuvés sont autorisés à s’exécuter.
        - **Audit uniquement** : autorisez tous les exécutables à s’exécuter, mais journalisez les exécutables non fiables qui s’exécutent dans le journal local des événements du client.
5.  Sous l’onglet **Inclusions** de l’**Assistant Création d’une stratégie Device Guard**, cliquez sur **Ajouter** si vous souhaitez ajouter une approbation pour des fichiers ou des dossiers spécifiques sur les PC. 
6.  Dans la boîte de dialogue **Ajouter fichier ou dossier approuvé**, spécifiez les informations sur le fichier ou dossier que vous souhaitez approuver. Vous pouvez spécifier un chemin d’accès de dossier ou de fichier local, ou vous connecter à un appareil distant auquel vous êtes autorisé à vous connecter et spécifier un chemin d’accès de fichier ou de dossier sur cet appareil.
Quand vous ajoutez une approbation pour des fichiers ou des dossiers spécifiques dans une stratégie Device Guard, vous pouvez :
    - Résoudre les problèmes avec les comportements des programmes d’installation gérés
    - Approuver les applications métier qui ne peuvent pas être déployées avec Configuration Manager
    - Approuver des applications qui sont incluses dans une image de déploiement de système d’exploitation. 
7.  Cliquez sur **Suivant**, puis fermez l’Assistant.

>[!IMPORTANT]
>L’inclusion de fichiers ou de dossiers approuvés n’est prise en charge que sur les PC clients équipés de la version 1706 ou d’une version ultérieure du client Gestionnaire de configuration. Si toutes les règles d’inclusion sont comprises dans une stratégie Device Guard et que celle-ci est ensuite déployée sur un PC client équipé d’une version antérieure du client Gestionnaire de configuration, elle ne sera pas appliquée. Pour résoudre ce problème, il suffit de mettre à niveau ces anciennes versions de clients. Les stratégies qui ne comprennent aucune règle d’inclusion peuvent toujours être appliquées sur des versions antérieures du client Gestionnaire de configuration.

## <a name="how-to-deploy-a-device-guard-policy"></a>Déployer une stratégie Device Guard
1.  Dans la console Configuration Manager, cliquez sur **Ressources et Conformité**.
2.  Dans l’espace de travail **Ressources et Conformité** , développez **Endpoint Protection**, puis cliquez sur **Stratégies de protection des appareils**.
3.  Dans la liste des stratégies, sélectionnez la stratégie que vous souhaitez déployer, puis, sous l’onglet **Accueil**, dans le groupe **Déploiement**, cliquez sur **Déployer**.
4.  Dans la boîte de dialogue **Déployer la stratégie Device Guard**, sélectionnez la collection sur laquelle vous souhaitez déployer la stratégie. Ensuite, configurez une planification pour définir à quel moment les clients évaluent la stratégie. Enfin, indiquez si le client peut évaluer la stratégie en dehors des fenêtres de maintenance configurées.
5.  Lorsque vous avez terminé, cliquez sur **OK** pour déployer la stratégie. 

Une fois que la stratégie est traitée sur un PC client, un redémarrage est planifié sur ce client selon les **paramètres clients** relatifs au **redémarrage de l’ordinateur**.
La stratégie ne prend pas effet tant que l’ordinateur client n’a pas redémarré.**

## <a name="how-to-monitor-a-device-guard-policy"></a>Surveiller une stratégie Device Guard

Utilisez les informations de la rubrique [Surveiller les paramètres de conformité](/sccm/compliance/deploy-use/monitor-compliance-settings) pour vérifier que la stratégie a été correctement déployée sur tous les PC.

Pour surveiller le traitement d’une stratégie Device Guard, utilisez le fichier journal suivant sur les PC clients :

**%WINDIR%\CCM\Logs\DeviceGuardHandler.log**

Pour vérifier le logiciel bloqué ou audité, consultez les journaux d’événements suivants du client local :

1.  Pour le blocage et l’audit des fichiers exécutables, utilisez **Journaux des applications et des services** > **Microsoft** > **Windows** > **Intégrité du code** > **Opérationnel**.
2.  Pour le blocage et l’audit du programme d’installation Windows et des fichiers de script, utilisez **Journaux des applications et des services** > **Microsoft** > **Windows** > **AppLocker** > **MSI et Script**.

## <a name="security-and-privacy-information-for-device-guard"></a>Informations sur la sécurité et la confidentialité pour Device Guard

- Dans cette préversion, ne déployez pas de stratégies Device Guard avec le mode de mise en conformité **Audit uniquement** dans un environnement de production. Ce mode est conçu pour vous aider à tester la capacité dans un environnement de laboratoire uniquement.
- Les appareils qui ont une stratégie déployée en mode **Audit uniquement** ou **Mise en conformité activée** et qui n’ont pas encore été redémarrés pour appliquer la stratégie sont vulnérables aux logiciels non autorisés dont l’installation est en cours.
Dans ce cas, le logiciel peut continuer à être autorisé à s’exécuter même en cas de redémarrage de l’appareil ou il reçoit une stratégie en mode **Mise en conformité activée**.
- Pour vérifier que la stratégie Device Guard est appliquée, préparez l’appareil dans un environnement lab. Ensuite, déployez la stratégie **Mise en conformité activée**. Pour terminer, redémarrez l’appareil avant de donner l’appareil à un utilisateur final.
- Ne déployez pas une stratégie **Mise en conformité activée** puis plus tard une stratégie **Audit uniquement** sur le même appareil. Il se peut que des logiciels non autorisés soient autorisés à s’exécuter à cause de cette configuration.
- Quand vous utilisez Configuration Manager pour activer l’intégrité du code configurable sur les PC clients avec des stratégies Device Guard, la stratégie n’empêche pas les utilisateurs disposant de droits d’administrateur local de contourner la stratégie Device Guard ou d’exécuter des logiciels non autorisés. 
- La seule façon d’empêcher les utilisateurs dotés de droits d’administrateur local de désactiver l’intégrité du code configurable consiste à déployer une stratégie binaire signée. Ce déploiement est possible par le biais de la stratégie de groupe, mais il n’est pas pris en charge dans Configuration Manager pour le moment.
- Le paramétrage de Configuration Manager en tant que programme d’installation managé sur les PC clients utilise la stratégie AppLocker. AppLocker est utilisé uniquement pour identifier les programmes d’installation managés et la mise en conformité se produit avec l’intégrité du code configurable. 




