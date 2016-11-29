---
title: "Mettre à niveau les installations d’évaluation | System Center Configuration Manager"
description: "Découvrez comment mettre à niveau une installation d’évaluation vers une installation complète de System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9a32f5a3-9917-434f-9811-106170f404be
caps.latest.revision: 3
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 0ad15c0caddeb3c200b8c663631d2993a338c7c8

---
# <a name="upgrade-an-evaluation-install-of-system-center-configuration-manager-to-a-full-install"></a>Mettre à niveau une installation d’évaluation de System Center Configuration Manager vers une installation complète

*S’applique à : System Center Configuration Manager (Current Branch)*



 Si vous avez installé une version d’évaluation de System Center Configuration Manager, à l’issue de 180 jours, la console Configuration Manager passe en lecture seule jusqu’à ce que vous activiez le produit à partir de la page **Maintenance de site** du programme d’installation. À tout moment avant ou après la période de 180 jours, vous avez la possibilité de mettre à niveau l'installation d'évaluation vers une installation complète.  

> [!NOTE]  
>  Quand vous connectez une console Configuration Manager à une installation d’évaluation de Configuration Manager, la barre de titre de la console indique le nombre de jours restants avant que l’installation d’évaluation n’expire. Le nombre de jours n'est pas actualisé automatiquement et est mis à jour uniquement lorsque vous effectuez une nouvelle connexion à un site.  

 **Vous pouvez mettre à niveau les sites suivants qui exécutent une installation d’évaluation :**  

-   Site d'administration centrale  

-   Site principal  

Dans la mesure où les sites secondaires ne sont pas considérés comme des installations d'évaluation, il est inutile de modifier un site secondaire après la mise à niveau de son site parent principal vers une installation complète.  

**Prérequis de la mise à niveau d’une édition d’évaluation vers une édition complète :**  

-   Vous devez disposer d’un produit valide à utiliser lors de la mise à niveau.  

-   Votre compte doit avoir des autorisations **administrateur** sur l’ordinateur sur lequel le site est installé.  

### <a name="to-upgrade-an-evaluation-edition-of-configuration-manager-to-a-licensed-edition"></a>Pour mettre à niveau une version d’évaluation de Configuration Manager vers une version sous licence  

1.  Sur le serveur de site, recherchez et exécutez **SETUP.exe** (programme d’installation de Configuration Manager) à partir du dossier d’installation de Configuration Manager (**%chemin%\BIN\X64**).  Vous devez exécuter la copie du programme d’installation qui se trouve sur le serveur de site dans le dossier Configuration Manager, car les options de maintenance de site ne sont pas disponibles quand vous exécutez le programme d’installation à partir du support d’installation.  

2.  Dans la page **Avant de commencer** , cliquez sur **Suivant**.  

3.  Sur la page **Mise en route** , sélectionnez **Effectuer la maintenance du site ou réinitialiser le site**, puis cliquez sur **Suivant**.  

4.  Dans la page **Maintenance de site** , sélectionnez **Passer d’une version d’évaluation à une version sous licence**, entrez une clé de produit valide, puis cliquez sur **Suivant**.  

5.  Sur la page **Termes du contrat de licence logiciel Microsoft** , lisez et acceptez les termes du contrat de licence, puis cliquez sur **Suivant**.  

6.  Sur la page **Configuration** , cliquez sur **Fermer** pour terminer l'Assistant.  

    > [!NOTE]  
    >  La barre de titre des consoles Configuration Manager qui restent connectées au site mis à niveau peut indiquer que le site est toujours une version d’évaluation jusqu’à ce que vous reconnectiez la console au site.  



<!--HONumber=Nov16_HO1-->


