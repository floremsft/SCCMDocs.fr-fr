---
title: "Mettre à niveau Long-Term Servicing Branch vers Current Branch | Microsoft Docs"
description: "Apprenez à convertir un site Long-Term Servicing Branch en site Current Branch."
ms.custom: na
ms.date: 2/8/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ec5b54cf-62b7-4ed1-9bb3-e8c63b9641c8
caps.latest.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 60631bc0346bd78d704e7129bb755af504c59b1b
ms.openlocfilehash: 6e7edc85630d22c5bbba1ff66bd1199903db76db

---


# <a name="upgrade-the-long-term-servicing-branch-to-the-current-branch"></a>Mettre à niveau Long-Term Servicing Branch vers Current Branch

*S’applique à : System Center Configuration Manager (Long-Term Servicing Branch)*

Cette rubrique est destinée à vous apprendre à mettre à niveau (convertir) un site et une hiérarchie qui exécutent une installation Long-Term Servicing Branch (LTSB) de Configuration Manager vers la version Current Branch.

Si vous avez souscrit un contrat Software Assurance (ou des droits de licence similaires) qui vous donnent le droit d’utiliser Current Branch, vous pouvez convertir votre installation LTSB en version Current Branch.  Il s’agit d’une conversion unidirectionnelle, car la conversion d’un site Current Branch en LTSB n’est pas prise en charge.

Si vous avez plusieurs sites, il vous suffit de convertir le site de niveau supérieur de votre hiérarchie. Dès lors que le site de niveau supérieur est converti :
- les sites principaux enfants sont convertis automatiquement ;
-    vous devez procéder à une mise à jour manuelle des sites secondaires dans la console Configuration Manager.

## <a name="run-setup-to-convert-the-long-term-servicing-branch"></a>Exécuter le programme d’installation pour convertir Long-Term Servicing Branch
Sur le site de niveau supérieur de votre hiérarchie, vous pouvez exécuter le programme d’installation de Configuration Manager à partir du media de base de référence éligible et sélectionner **Maintenance de site**.  Ensuite, une fois dans la page de licence, sélectionnez l’option Current Branch, puis terminez l’Assistant.

Une fois votre site converti en version Current Branch, vous avez accès à des fonctions et fonctionnalités qui n’étaient pas disponibles auparavant.

> [!NOTE]  
> Le média de ligne de base éligible est un média qui contient une version équivalente ou postérieure à votre installation LTSB.

Par exemple, sachant que LTSB est basé sur la version 1606, vous ne pouvez pas utiliser le média de ligne de base 1511 pour une conversion vers Current Branch. Vous devez exécuter le programme d’installation du média de base de référence de la version 1606 dont vous vous êtes servi pour installer le site LTSB, puis choisir l’option de licence correspondant à Current Branch.  Autrement, si une base de référence ultérieure de Current Branch a été publiée, vous pouvez exécuter le programme d’installation à partir de ce média de base de référence.

Pour obtenir la liste des versions de ligne de base, consultez **Versions de base et de mise à jour** dans [Mises à jour pour Configuration Manager](/sccm/core/servers/manage/updates).

## <a name="use-the-configuration-manager-console-to-convert-the-long-term-servicing-branch"></a>Utiliser la console Configuration Manager pour convertir Long-Term Servicing Branch
Si votre site s’exécute LTSB, vous pouvez utiliser l’option suivante dans la console Configuration Manager pour convertir Current Branch :

 1. Dans la console, accédez à **Administration** > **Configuration du site** > **Sites**, puis ouvrez **Paramètres de hiérarchie**.  

 2. Sélectionnez l’option de conversion vers Current Branch, puis choisissez **Appliquer**.  

Une fois votre site converti en version Current Branch, vous avez accès à des fonctions et fonctionnalités qui n’étaient pas disponibles auparavant.



<!--HONumber=Feb17_HO2-->


