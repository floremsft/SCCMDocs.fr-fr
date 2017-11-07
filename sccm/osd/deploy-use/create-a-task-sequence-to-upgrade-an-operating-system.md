---
title: "Créer une séquence de tâches pour mettre à niveau un système d’exploitation"
titleSuffix: Configuration Manager
description: "Dans System Center Configuration Manager, les séquences de tâches permettent de mettre automatiquement à niveau un système d’exploitation Windows 7 ou version ultérieure vers Windows 10."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7591e386-a9ab-4640-8643-332dce5aa006
caps.latest.revision: "12"
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: 2787c8a692321a49cf287fc2f09858690360dc25
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/12/2017
---
# <a name="create-a-task-sequence-to-upgrade-an-operating-system-in-system-center-configuration-manager"></a>Créer une séquence de tâches pour mettre à niveau un système d’exploitation dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Dans System Center Configuration Manager, les séquences de tâches permettent de mettre automatiquement à niveau un système d’exploitation Windows 7 ou version ultérieure vers Windows 10, ou Windows Server 2012 ou version ultérieure vers Windows Server 2016, sur un ordinateur de destination. Vous créez une séquence de tâches qui fait référence à l’image de système d’exploitation que vous souhaitez installer sur l’ordinateur de destination et tout autre contenu supplémentaire, tel que des applications ou des mises à jour logicielles que vous souhaitez installer. La séquence de tâches de mise à niveau d’un système d’exploitation fait partie intégrante du scénario [Effectuer une mise à niveau de Windows vers la dernière version](upgrade-windows-to-the-latest-version.md).  

##  <a name="BKMK_UpgradeOS"></a> Créer une séquence de tâches pour mettre à niveau un système d’exploitation  
 Pour mettre à niveau le système d’exploitation sur des ordinateurs, vous pouvez créer une séquence de tâches et sélectionner **Mettre à niveau un système d’exploitation à partir du package de mise à niveau** dans l’Assistant Création d’une séquence de tâches. L’Assistant ajoute les étapes permettant de mettre à niveau le système d’exploitation, d’appliquer des mises à jour logicielles et d’installer des applications. Avant de créer la séquence de tâches, vous devez vous assurer que les conditions suivantes sont remplies :    

-   **Obligatoire**  

     - Le [package de mise à niveau du système d’exploitation](../get-started/manage-operating-system-upgrade-packages.md) doit être disponible dans la console Configuration Manager.
     - Lorsque vous mettez à niveau vers Windows Server 2016, vous devez sélectionner le paramètre **Ignore any dismissable compatibility messages** (Ignorer les messages de compatibilité révocables) lors de l’étape de la séquence de tâches Mettre à niveau le système d’exploitation ou la mise à niveau échoue.

-   **Obligatoire (si utilisé)**  

    -   Les [mises à jour logicielles](../../sum/get-started/synchronize-software-updates.md) doivent être synchronisées dans la console Configuration Manager.  

    -   Les [applications](../../apps/deploy-use/create-applications.md) doivent être ajoutées à la console Configuration Manager.  

#### <a name="to-create-a-task-sequence-that-upgrades-an-operating-system"></a>Pour créer une séquence de tâches qui met à niveau un système d’exploitation  

1.  Dans la console Configuration Manager, cliquez sur **Bibliothèque de logiciels**.  

2.  Dans l'espace de travail **Bibliothèque de logiciels** , développez **Systèmes d'exploitation**, puis cliquez sur **Séquences de tâches**.  

3.  Sous l'onglet **Accueil** , dans le groupe **Créer** , cliquez sur **Créer une séquence de tâches** pour démarrer l'Assistant Création d'une séquence de tâches.  

4.  Dans la page **Créer une séquence de tâches** , sélectionnez **Mettre à niveau un système d’exploitation à partir du package de mise à niveau**, puis cliquez sur **Suivant**.  

5.  Sur la page **Informations sur la séquence de tâches** , spécifiez les paramètres suivants et cliquez sur **Suivant**.  

    -   **Nom de la séquence de tâches**: spécifiez un nom qui identifie la séquence de tâches.  

    -   **Description**: spécifiez une description de la tâche qui est effectuée par la séquence de tâches.  

6.  Dans la page **Mettre à niveau le système d’exploitation Windows** , spécifiez les paramètres suivants et cliquez sur **Suivant**.  

    -   **Mettre à niveau le package**: spécifiez le package de mise à niveau qui contient les fichiers sources de mise à niveau du système d’exploitation. Vous pouvez vérifier que vous avez sélectionné le bon package de mise à niveau en examinant les informations contenues dans le volet **Propriétés** . Pour plus d’informations, consultez [Gérer les packages de mise à niveau de système d’exploitation](../get-started/manage-operating-system-upgrade-packages.md).  

    -   **Index d’édition**: si plusieurs index d’édition de système d’exploitation sont disponibles dans le package, sélectionnez l’index d’édition souhaité. Par défaut, le premier élément est sélectionné.  

    -   **Clé du produit**: spécifiez la clé de produit pour le système d’exploitation Windows à installer. Vous pouvez spécifier des clés de licence en volume codées et des clés de produit standard. Si vous utilisez une clé de produit non codée, chaque groupe de cinq caractères doit être séparé par un tiret (-). Par exemple : *XXXXX-XXXXX-XXXXX-XXXXX-XXXXX*. Quand la mise à niveau concerne une édition de licence en volume, la clé de produit n’est pas requise. Vous avez besoin d’une clé de produit seulement quand la mise à niveau concerne une édition commerciale de Windows.  

    -   **Ignore any dismissable compatibility messages** (Ignorer les messages de compatibilité révocables) : sélectionnez ce paramètre si vous effectuez la mise à niveau vers Windows Server 2016. Si vous ne sélectionnez pas ce paramètre, l’exécution de la séquence de tâches échoue car le programme d’installation de Windows attend que l’utilisateur clique sur **Confirmer** dans la boîte de dialogue de compatibilité d’une application Windows.   

7.  Sur la page **Inclure les mises à jour** , spécifiez si vous souhaitez installer les mises à jour logicielles requises, toutes les mises à jour logicielles ou aucune mise à jour logicielle, puis cliquez sur **Suivant**. Si vous spécifiez l’installation des mises à jour logicielles, Configuration Manager installe uniquement les mises à jour logicielles ciblant les regroupements auxquels l’ordinateur de destination appartient.  

8.  Sur la page **Installer les applications** , spécifiez les applications à installer sur l'ordinateur de destination, puis cliquez sur **Suivant**. Si vous spécifiez plusieurs applications, vous pouvez également spécifier que la séquence de tâches continue si l'installation d'une application spécifique échoue.  

9. Effectuez toutes les étapes de l'Assistant.  



## <a name="configure-pre-cache-content"></a>Configurer la mise en cache préalable du contenu
À partir de la version 1702, vous pouvez choisir d’utiliser la fonctionnalité de mise en cache préalable pour les déploiements disponibles des séquences de tâches. Ainsi, les clients téléchargent uniquement le contenu approprié avant toute installation de contenu par l’utilisateur.
> [!TIP]  
> La mise en cache préalable, introduite avec la version 1702, est en version préliminaire. Pour savoir comment l’activer, consultez [Utiliser des fonctionnalités de préversion des mises à jour](/sccm/core/servers/manage/pre-release-features).

Supposons que vous souhaitiez déployer une séquence de tâches de mise à niveau sur place de Windows 10, que vous ne vouliez qu’une seule séquence de tâches pour tous les utilisateurs, et que vous ayez plusieurs architectures et/ou langues. Avant la version 1702, si vous créez un déploiement disponible et que l’utilisateur clique sur **Installer** dans le Centre logiciel, le contenu est téléchargé à ce moment-là. Ceci a pour effet de retarder la disponibilité de l’installation. Par ailleurs, tout le contenu référencé dans la séquence de tâches est téléchargé. (c’est-à-dire tous les packages de mise à niveau du système d’exploitation pour chaque langue et chaque architecture). Si chaque package fait environ 3 Go, le package de téléchargement peut être très volumineux.

La mise en cache préalable du contenu permet au client de télécharger uniquement le contenu applicable dès qu’il reçoit le déploiement. Ainsi, quand l’utilisateur clique sur **Installer** dans le Centre logiciel, le contenu est prêt et l’installation démarre rapidement, car le contenu se trouve sur le disque dur local.

### <a name="to-configure-the-pre-cache-feature"></a>Pour configurer la fonctionnalité de mise en cache préalable

1. Créez des packages de mise à niveau du système d’exploitation pour des architectures et des langues spécifiques. Spécifiez l’architecture et la langue sous l’onglet **Source de données** du package. Pour la langue, utilisez la conversion décimale (par exemple, pour l’anglais, 1033 est l’identifiant décimal et 0x0409 l’identifiant hexadécimal). Pour plus d’informations, consultez [Créer une séquence de tâches pour mettre à niveau un système d’exploitation](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system).

    Les valeurs de l’architecture et de la langue sont mises en correspondance avec les conditions de la séquence de tâches que vous créez à l’étape suivante pour déterminer si le package de mise à niveau du système d’exploitation doit être préalablement mis en cache.
2. Créez une séquence de tâches avec des étapes conditionnelles pour les différentes langues et architectures. Par exemple, pour la version anglaise, vous pouvez créer une étape comme suit :

    ![propriétés de mise en cache préalable](../media/precacheproperties2.png)

    ![options de mise en cache préalable](../media/precacheoptions2.png)  

3. déployer la séquence de tâches. Pour configurer la fonctionnalité de mise en cache préalable, configurez ce qui suit :
    - Sous l’onglet **Général**, sélectionnez **Prétélécharger le contenu pour cette séquence de tâches**.
    - Sous l’onglet **Paramètres de déploiement**, configurez la séquence de tâches avec **Disponible** comme **Objectif**. Si vous créez un déploiement **Exigé**, la fonctionnalité de mise en cache préalable ne fonctionne pas.
    - Sous l’onglet **Planification**, pour le paramètre **Planifier la disponibilité de ce déploiement**, choisissez une heure future qui donne aux clients le temps de mettre préalablement en cache le contenu avant que le déploiement ne soit accessible aux utilisateurs. Par exemple, vous pouvez définir un délai de 3 heures pour allouer suffisamment de temps à la mise en cache préalable du contenu.  
    - Sous l’onglet **Points de distribution**, configurez les paramètres **Options de déploiement**. Si le contenu n’est pas préalablement mis en cache sur un client avant le démarrage de l’installation, ces paramètres sont utilisés.


### <a name="user-experience"></a>Expérience utilisateur
- Quand le client reçoit la stratégie de déploiement, il commence la mise en cache préalable du contenu. Il s’agit du contenu référencé (tout autre type de package) et du package de mise à niveau du système d’exploitation correspondant au client (en fonction des conditions définies dans la séquence de tâches).
- Une fois le déploiement accessible aux utilisateurs (paramètre défini sous l’onglet **Planification** du déploiement), une notification s’affiche pour informer les utilisateurs du nouveau déploiement. Le déploiement apparaît alors dans le Centre logiciel. L’utilisateur peut accéder au Centre logiciel et cliquer sur **Installer** pour démarrer l’installation.
- Si tout le contenu n’est pas préalablement mis en cache, les paramètres spécifiés sous l’onglet **Option de déploiement** du déploiement sont utilisés. Nous vous recommandons de définir un délai suffisant entre la création du déploiement et l’heure à laquelle le déploiement est accessible aux utilisateurs pour que les client aient le temps de mettre préalablement en cache le contenu.



## <a name="download-package-content-task-sequence-step"></a>Étape de séquence de tâches Télécharger le contenu du package  
 Vous pouvez exécuter l’étape [Télécharger le contenu du package](../understand/task-sequence-steps.md#BKMK_DownloadPackageContent) avant l’étape **Mettre à niveau le système d’exploitation** dans les scénarios suivants :  

-   Vous utilisez une seule séquence de tâches de mise à niveau qui peut fonctionner avec les plateformes x86 et x64. Pour cela, incluez deux étapes **Télécharger le contenu du package** dans le groupe **Préparer pour la mise à niveau** avec des conditions pour détecter l’architecture du client et télécharger uniquement le package de mise à niveau de système d’exploitation approprié. Configurez chaque étape **Télécharger le contenu du package** pour utiliser la même variable et utilisez cette variable pour le chemin du support à l’étape **Mettre à niveau le système d’exploitation** .  

-   Pour télécharger dynamiquement un package de pilotes applicable, utilisez deux étapes **Télécharger le contenu du package** avec des conditions pour détecter le type de matériel approprié pour chaque package de pilotes. Configurez chaque étape **Télécharger le contenu du package** pour utiliser la même variable et utilisez cette variable pour la valeur **Contenu intermédiaire** dans la section des pilotes à l’étape **Mettre à niveau le système d’exploitation** .  

   > [!NOTE]
   > Quand il existe plusieurs packages, Configuration Manager ajoute un suffixe numérique au nom de la variable. Par exemple, si vous spécifiez une variable %mon_contenu% en tant que variable personnalisée, il s’agit de la racine de l’emplacement de stockage de l’ensemble du contenu référencé (qui peut correspondre à plusieurs packages). Quand vous faites référence à la variable dans une étape de sous-séquence, comme Mettre à niveau le système d’exploitation, elle est utilisée avec un suffixe numérique. Dans cet exemple, le numéro dans %mon_contenu01% ou %mon_contenu02% correspond à l’ordre d’apparition du package dans cette étape.

## <a name="optional-post-processing-task-sequence-steps"></a>Étapes de séquence de tâches post-traitement facultatives  
 Une fois la séquence de tâches créée, vous pouvez ajouter des étapes supplémentaires pour désinstaller des applications présentant des problèmes de compatibilité connus, ou ajouter des actions de post-traitement à exécuter une fois que l’ordinateur a redémarré et que la mise à niveau vers Windows 10 a réussi. Ajoutez ces étapes supplémentaires dans le groupe Post-traitement de la séquence de tâches.  

> [!NOTE]  
>  Cette séquence de tâches n’étant pas linéaire, des conditions applicables à certaines étapes peuvent affecter les résultats de la séquence de tâches, selon que la mise à niveau de l’ordinateur client a réussi ou qu’elle a échoué et que la version initiale du système d’exploitation a été restaurée sur l’ordinateur client.  

## <a name="optional-rollback-task-sequence-steps"></a>Étapes de séquence de tâches de restauration facultatives  
 En cas de problème durant le processus de mise à niveau après le redémarrage de l’ordinateur, le programme d’installation annule la mise à niveau et restaure le système d’exploitation précédent, et la séquence de tâches se poursuit avec les étapes du groupe Restauration. Après avoir créé la séquence de tâches, vous pouvez ajouter des étapes facultatives au groupe Restauration.  

## <a name="folder-and-files-removed-after-computer-restart"></a>Dossier et fichiers supprimés après le redémarrage de l’ordinateur  
 À la fin de la séquence de tâches de mise à niveau d’un système d’exploitation vers Windows 10 et toutes les autres étapes de la séquence de tâches, les scripts de post-traitement et de restauration ne sont pas supprimés tant que l’ordinateur n’a pas redémarré.  Ces fichiers de script ne contiennent pas d’informations sensibles.  
