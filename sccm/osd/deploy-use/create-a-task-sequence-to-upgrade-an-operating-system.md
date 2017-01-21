---
title: "Créer une séquence de tâches pour mettre à niveau un système d’exploitation | Microsoft Docs"
description: "Dans System Center Configuration Manager, les séquences de tâches permettent de mettre automatiquement à niveau un système d’exploitation Windows 7 ou version ultérieure vers Windows 10."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7591e386-a9ab-4640-8643-332dce5aa006
caps.latest.revision: 12
author: Dougeby
ms.author: dougeby
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 74341fb60bf9ccbc8822e390bd34f9eda58b4bda
ms.openlocfilehash: 32af7da62bfe767a21a891338bd778ebf45f2685


---
# <a name="create-a-task-sequence-to-upgrade-an-operating-system-in-system-center-configuration-manager"></a>Créer une séquence de tâches pour mettre à niveau un système d’exploitation dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Dans System Center Configuration Manager, les séquences de tâches permettent de mettre automatiquement à niveau un système d’exploitation Windows 7 ou version ultérieure vers Windows 10 sur un ordinateur de destination. Vous créez une séquence de tâches qui fait référence à l’image de système d’exploitation que vous souhaitez installer sur l’ordinateur de destination et tout autre contenu supplémentaire, tel que des applications ou des mises à jour logicielles que vous souhaitez installer. La séquence de tâches de mise à niveau d’un système d’exploitation fait partie intégrante du scénario [Effectuer une mise à niveau de Windows vers la dernière version](upgrade-windows-to-the-latest-version.md).  

##  <a name="a-namebkmkupgradeosa-create-a-task-sequence-to-upgrade-an-operating-system"></a><a name="BKMK_UpgradeOS"></a> Créer une séquence de tâches pour mettre à niveau un système d’exploitation  
 Pour mettre à niveau le système d’exploitation sur des ordinateurs vers Windows 10, vous pouvez créer une séquence de tâches et sélectionner **Mettre à niveau un système d’exploitation à partir du package de mise à niveau** dans l’Assistant Création d’une séquence de tâches. L’Assistant ajoutera les étapes permettant de mettre à niveau le système d’exploitation, d’appliquer des mises à jour logicielles et d’installer des applications. Avant de créer la séquence de tâches, vous devez vous assurer que les conditions suivantes sont remplies :  

-   **Obligatoire**  

     - Le [package de mise à niveau du système d’exploitation](../get-started/manage-operating-system-upgrade-packages.md) Windows 10 doit être disponible dans la console Configuration Manager.  

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

    -   **Clé du produit**: spécifiez la clé de produit pour le système d’exploitation Windows à installer. Vous pouvez spécifier des clés de licence en volume codées et des clés de produit standard. Si vous utilisez une clé de produit non codée, chaque groupe de 5 caractères doit être séparé par un tiret (-). Par exemple : *XXXXX-XXXXX-XXXXX-XXXXX-XXXXX*. Quand la mise à niveau concerne une édition de licence en volume, la clé de produit n’est pas requise. Vous avez besoin d’une clé de produit seulement quand la mise à niveau concerne une édition commerciale de Windows.  

7.  Sur la page **Inclure les mises à jour** , spécifiez si vous souhaitez installer les mises à jour logicielles requises, toutes les mises à jour logicielles ou aucune mise à jour logicielle, puis cliquez sur **Suivant**. Si vous spécifiez l’installation des mises à jour logicielles, Configuration Manager installe uniquement les mises à jour logicielles ciblant les regroupements auxquels l’ordinateur de destination appartient.  

8.  Sur la page **Installer les applications** , spécifiez les applications à installer sur l'ordinateur de destination, puis cliquez sur **Suivant**. Si vous spécifiez plusieurs applications, vous pouvez également spécifier que la séquence de tâches continue si l'installation d'une application spécifique échoue.  

9. Effectuez toutes les étapes de l'Assistant.  

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



<!--HONumber=Dec16_HO3-->


