---
title: "Étapes de séquence de tâches pour gérer la conversion du BIOS en UEFI | Configuration Manager"
description: "Découvrez comment personnaliser une séquence de tâches de déploiement de système d’exploitation afin de préparer une partition FAT32 pour la transition vers UEFI."
ms.custom: na
ms.date: 11/08/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: bd3df04a-902f-4e91-89eb-5584b47d9efa
author: Dougeby
ms.author: dougeby
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 54089ac8aa95154534d010bee8c7e2cbd70d1c7e
ms.openlocfilehash: 30838ed3ad045f781a748f96c874bf543ea05462


---
# <a name="task-sequence-steps-to-manage-bios-to-uefi-conversion"></a>Étapes de séquence de tâches pour gérer la conversion du BIOS en UEFI
À partir de Configuration Manager version 1610, vous pouvez maintenant personnaliser une séquence de tâches de déploiement de système d’exploitation avec une nouvelle variable, TSUEFIDrive, afin que l’étape **Redémarrer l’ordinateur** prépare une partition FAT32 sur le disque dur pour la transition vers UEFI. La procédure suivante fournit un exemple de création des étapes de séquence de tâches pour préparer le disque dur pour la conversion du BIOS en UEFI.

#### <a name="to-prepare-the-fat32-partition-for-the-conversion-to-uefi"></a>Pour préparer la partition FAT32 pour la conversion en UEFI :
Dans une séquence de tâches existante pour installer un système d’exploitation, vous allez ajouter un nouveau groupe avec les étapes permettant d’effectuer la conversion du BIOS en UEFI.

1. Créez un groupe de séquences de tâches après les étapes de capture des fichiers et paramètres, et avant les étapes d’installation du système d’exploitation. Par exemple, créez un groupe après le groupe **Capturer les fichiers et les paramètres** nommé **BIOS-en-UEFI**.
2. Sous l’onglet **Options** du nouveau groupe, ajoutez une nouvelle variable de séquence de tâches comme condition où **_SMSTSBootUEFI** est **différent** de **true**. Vous empêchez ainsi l’exécution des étapes dans le groupe quand un ordinateur est déjà en mode UEFI.
![Groupe BIOS-en-UEFI](../../core/get-started/media/BIOS-to-UEFI-group.png)
3. Sous le nouveau groupe, ajoutez l’étape de séquence de tâches **Redémarrer l’ordinateur**. Dans **Spécifiez l’élément à exécuter après le redémarrage**, sélectionnez **L’image de démarrage attribuée à cette séquence de tâches** pour démarrer l’ordinateur dans Windows PE.  
4. Sous l’onglet **Options**, ajoutez une variable de séquence de tâches comme condition où **_SMSTSInWinPE est égal à False**. Vous empêchez ainsi l’exécution de cette étape si l’ordinateur est déjà dans Windows PE.

    ![Étape Redémarrer l’ordinateur](../../core/get-started/media/restart-in-windows-pe.png)
5. Ajoutez une étape pour démarrer l’outil OEM qui convertira le microprogramme du BIOS en UEFI. Il s’agit en général de l’étape de séquence de tâches **Exécuter la ligne de commande** avec une ligne de commande pour démarrer l’outil OEM.
6.  Ajoutez l’étape de séquence de tâches Formater et partitionner le disque pour partitionner et formater le disque dur. Dans l’étape, procédez comme suit :
    1.  Créez la partition FAT32 qui va être convertie en UEFI avant l’installation du système d’exploitation. Choisissez **GPT** pour **Type de disque**.
    ![Étape Formater et partitionner le disque](../../core/get-started/media/format-and-partition-disk.png)
    2.  Accédez aux propriétés de la partition FAT32. Entrez **TSUEFIDrive** dans le champ **Variable**. Quand la séquence de tâches détecte cette variable, elle prépare la transition vers UEFI avant le redémarrage de l’ordinateur.
    ![Propriétés de la partition](../../core/get-started/media/partition-properties.png)
    3. Créez une partition NTFS que le moteur de séquence de tâches utilise pour enregistrer son état et pour stocker les fichiers journaux.
6.  Ajoutez l’étape de séquence de tâches **Redémarrer l’ordinateur**. Dans **Spécifiez l’élément à exécuter après le redémarrage**, sélectionnez **L’image de démarrage attribuée à cette séquence de tâches** pour démarrer l’ordinateur dans Windows PE.  



<!--HONumber=Dec16_HO3-->


