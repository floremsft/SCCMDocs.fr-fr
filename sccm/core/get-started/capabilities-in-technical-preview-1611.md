---
title: "Fonctionnalités de Technical Preview 1611 Configuration Manager"
description: "Découvrez les fonctionnalités disponibles dans la version d’évaluation technique 1611 pour System Center Configuration Manager."
ms.custom: na
ms.date: 01/23/2017
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.prod: configuration-manager
ms.technology:
- configmgr-other
ms.topic: article
ms.assetid: d2ad00e8-9f10-41b6-816a-d8542c23a22e
caps.latest.revision: 2
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 5d08d1f9ccd995d544c3c21c4af52ede73343077
ms.openlocfilehash: 5e77ebbfd3f3d573d903fe58024a22feb9884e4a

---
# <a name="capabilities-in-technical-preview-1611-for-system-center-configuration-manager"></a>Fonctionnalités de la version d’évaluation technique 1611 pour System Center Configuration Manager

*S’applique à : System Center Configuration Manager (version d’évaluation technique)*



Cet article présente les fonctionnalités disponibles dans la version d’évaluation technique 1611 pour System Center Configuration Manager. Vous pouvez installer cette version pour mettre à jour et ajouter de nouvelles fonctionnalités à votre site de version d’évaluation technique Configuration Manager. Avant d’installer cette version d’évaluation technique, passez en revue la rubrique de présentation, [Technical Preview pour System Center Configuration Manager](../../core/get-started/technical-preview.md), pour vous familiariser avec les conditions générales et les limitations d’utilisation d’une version d’évaluation technique, la mise à jour entre les versions et l’envoi de commentaires sur les fonctionnalités dans une version d’évaluation technique.    

**Problèmes connus dans cette version d’évaluation technique :**   
- ***État des prérequis*** : Quand vous installez la version 1611, l’état global des prérequis peut indiquer une installation réussie avec des avertissements. Toutefois, les prérequis à l’origine des avertissements ne sont pas répertoriés. Cela peut être dû aux deux prérequis suivants :
  - Options de création d’index en mémoire SQL
  - Vérifications de la version de SQL Server prise en charge  

 Comme il s’agit uniquement d’avertissements, vous pouvez les ignorer.

- ***PowerShell*** : quand vous vous connectez à Windows PowerShell à partir de la console Configuration Manager, vous pouvez recevoir l’erreur suivante : **Microsoft.ConfigurationManagement.PowerShell.Types.ps1xml n’est pas signé numériquement**.  

   Vous pouvez résoudre ce problème en remplaçant certains fichiers par les versions signées de la version 1610. Copiez tous les fichiers avec les extensions suivantes qui figurent dans le dossier **&lt;répertoire_installation>\AdminConsole\bin\** de l’installation de la version 1610 : **.psd1**, **.ps1xml** et **.psm1**. Collez-les dans le dossier **&lt;répertoire_installation>\AdminConsole\bin\* * de l’installation de la version d’évaluation technique 1611, en remplaçant la version 1611 des fichiers.


**Vous trouverez ci-dessous les nouvelles fonctionnalités propres à cette version.**  

## <a name="pre-cache-content-for-available-deployments-and-task-sequences"></a>Mettre préalablement en cache le contenu pour les déploiements et les séquences de tâches disponibles
Cette version d’évaluation technique propose une fonctionnalité de mise en cache préalable des séquences de tâches et des déploiements disponibles. De cette façon, les clients téléchargent uniquement le contenu approprié avant toute installation de contenu par l’utilisateur.

Supposons que vous souhaitiez déployer une séquence de tâches de mise à niveau sur place de Windows 10, que vous ne vouliez qu’une seule séquence de tâches pour tous les utilisateurs, et que vous ayez plusieurs architectures et/ou langues. Dans Current Branch, si vous créez un déploiement disponible et que l’utilisateur clique sur **Installer** dans le Centre logiciel, le contenu est téléchargé à ce moment-là. Ceci a pour effet de retarder la disponibilité de l’installation. Si vous choisissez de créer un déploiement de séquence de tâches disponible dans Current Branch, tout le contenu référencé dans la séquence de tâches est téléchargé (c’est-à-dire tous les packages de mise à niveau du système d’exploitation pour chaque langue et chaque architecture). Si chaque package fait environ 3 Go, le package de téléchargement peut être très volumineux.

La fonctionnalité de mise en cache préalable du contenu permet au client de télécharger uniquement le contenu applicable dès qu’il reçoit le déploiement. Ainsi, quand l’utilisateur clique sur **Installer** dans le Centre logiciel, le contenu est prêt et l’installation démarre rapidement, car le contenu se trouve sur le disque dur local.

### <a name="to-configure-the-pre-cache-feature"></a>Pour configurer la fonctionnalité de mise en cache préalable

1. Créez des packages de mise à niveau du système d’exploitation pour des architectures et des langues spécifiques. Spécifiez l’architecture et la langue sous l’onglet **Source de données** du package. Pour la langue, utilisez la conversion décimale (par exemple, pour l’anglais, 1033 est l’identifiant décimal et 0x0409 l’identifiant hexadécimal). Pour plus d’informations, consultez [Créer une séquence de tâches pour mettre à niveau un système d’exploitation](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system).

    Les valeurs de l’architecture et de la langue sont mises en correspondance avec les conditions de la séquence de tâches que vous allez créer à l’étape suivante pour déterminer si le package de mise à niveau du système d’exploitation doit être préalablement mis en cache.
2. Créez une séquence de tâches avec des étapes conditionnelles pour les différentes langues et architectures. Par exemple, pour la version anglaise, vous pouvez créer une étape comme suit :

    ![propriétés de mise en cache préalable](media/precacheproperties2.png)

    ![options de mise en cache préalable](media/precacheoptions2.png)  

3. déployer la séquence de tâches. Pour configurer la fonctionnalité de mise en cache préalable, configurez ce qui suit :
    - Sous l’onglet **Général**, sélectionnez **Prétélécharger le contenu pour cette séquence de tâches**.
    - Sous l’onglet **Paramètres de déploiement**, configurez la séquence de tâches avec **Disponible** comme **Objectif**. Si vous créez un déploiement **Exigé**, la fonctionnalité de mise en cache préalable ne fonctionne pas.
    - Sous l’onglet **Planification**, pour le paramètre **Planifier la disponibilité de ce déploiement**, choisissez une heure future qui donne aux clients le temps de mettre préalablement en cache le contenu avant que le déploiement ne soit accessible aux utilisateurs. Par exemple, vous pouvez définir un délai de 3 heures pour allouer suffisamment de temps à la mise en cache préalable du contenu.  
    - Sous l’onglet **Points de distribution**, configurez les paramètres **Options de déploiement**. Si le contenu n’est pas préalablement mis en cache sur un client avant le démarrage de l’installation, ces paramètres sont utilisés.


### <a name="user-experience"></a>Expérience utilisateur
- Quand le client reçoit la stratégie de déploiement, il commence la mise en cache préalable du contenu. Il s’agit du contenu référencé (tout autre type de package) et du package de mise à niveau du système d’exploitation correspondant au client (en fonction des conditions définies dans la séquence de tâches).
- Une fois le déploiement accessible aux utilisateurs (paramètre défini sous l’onglet **Planification** du déploiement), une notification s’affiche pour informer les utilisateurs du nouveau déploiement. Le déploiement apparaît alors dans le Centre logiciel. L’utilisateur peut accéder au Centre logiciel et cliquer sur **Installer** pour démarrer l’installation.
- Si tout le contenu n’est pas préalablement mis en cache, les paramètres spécifiés sous l’onglet **Option de déploiement** du déploiement sont utilisés. Nous vous recommandons de définir un délai suffisant entre la création du déploiement et l’heure à laquelle le déploiement est accessible aux utilisateurs pour que les client aient le temps de mettre préalablement en cache le contenu.


## <a name="see-also"></a>Voir aussi
[Technical Preview pour System Center Configuration Manager](../../core/get-started/technical-preview.md)



<!--HONumber=Jan17_HO4-->


