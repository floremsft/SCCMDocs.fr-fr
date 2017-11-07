---
title: "Créer une séquence de tâches personnalisée"
titleSuffix: Configuration Manager
description: "Modifiez une séquence de tâches personnalisée dans System Center Configuration Manager pour y ajouter des étapes."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b9800a66-7541-47ca-8276-da8ef6cb6d1b
caps.latest.revision: "6"
caps.handback.revision: "0"
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: e25b60b64ae2ed75091c4f5b0ffa0f9eca4c6cac
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/12/2017
---
# <a name="create-a-custom-task-sequence-with-system-center-configuration-manager"></a>Créer une séquence de tâches personnalisée avec System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Quand vous créez une séquence de tâches personnalisée dans System Center Configuration Manager, elle ne contient aucune étape de séquence de tâches. Après avoir créé la séquence de tâches, vous devez la modifier et ajouter les étapes de séquence de tâches dont vous avez besoin.  

##  <a name="BKMK_CustomTS"></a> Créer une séquence de tâches personnalisée  
 Pour créer une séquence de tâches personnalisée, procédez comme suit.  

#### <a name="to-create-a-custom-task-sequence"></a>Pour créer une séquence de tâches personnalisée  

1.  Dans la console Configuration Manager, cliquez sur **Bibliothèque de logiciels**.  

2.  Dans l'espace de travail **Bibliothèque de logiciels** , développez **Systèmes d'exploitation**, puis cliquez sur **Séquences de tâches**.  

3.  Sous l'onglet **Accueil** , dans le groupe **Créer** , cliquez sur **Créer une séquence de tâches** pour démarrer l'Assistant Création d'une séquence de tâches.  

4.  Sur la page **Créer une nouvelle séquence de tâches** , sélectionnez **Créez une séquence de tâches personnalisée**.  

5.  Sur la page **Informations sur la séquence de tâches** , spécifiez un nom, une description et une image de démarrage facultative pour la séquence de tâches à utiliser, puis fermez l'Assistant.  

 Après avoir fermé l’Assistant Création d’une séquence de tâches, Configuration Manager ajoute la séquence de tâches personnalisée au nœud **Séquences de tâches**. Vous pouvez désormais modifier cette séquence de tâches pour y ajouter des étapes de séquence de tâches.  

 Pour obtenir une liste des étapes de séquence de tâches disponibles, consultez [Étapes de séquence de tâches](../understand/task-sequence-steps.md).  

 Pour plus d’informations sur la modification d’une séquence de tâches, consultez [Modifier une séquence de tâches](manage-task-sequences-to-automate-tasks.md#BKMK_ModifyTaskSequence).  

 Souvent, vous utiliserez des séquences de tâches pour automatiser des tâches de déploiement de système d’exploitation, mais vous pouvez créer une séquence de tâches personnalisée pour automatiser de nombreuses tâches. Pour plus d’informations, consultez [Créer une séquence de tâches pour les déploiements autres que les déploiements de système d’exploitation](create-a-task-sequence-for-non-operating-system-deployments.md).  

 ## <a name="next-steps"></a>Étapes suivantes
 [Déployer la séquence de tâches](manage-task-sequences-to-automate-tasks.md#BKMK_DeployTS)
