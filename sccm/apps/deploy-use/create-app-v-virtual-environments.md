---
title: "Créer des environnements virtuels App-V | System Center Configuration Manager"
description: "Créez des environnements virtuels avec Microsoft Application Virtualization pour permettre aux applications de partager des données entre elles."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b6b86078-fcc4-46cf-87d6-4b52b914b712
caps.latest.revision: 6
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 625ea93d855089f6dbbdcc8368032e61b8a1ba0b


---
# <a name="create-app-v-virtual-environments-in-system-center-configuration-manager"></a>Créer des environnements virtuels App-V dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Dans System Center Configuration Manager, les environnements virtuels Microsoft Application Virtualization (App-V) permettent aux applications virtuelles déployées de partager le même système de fichiers et le même Registre sur les PC Windows clients. Par conséquent, contrairement aux applications virtuelles conventionnelles, ces applications peuvent partager des données entre elles. Les environnements virtuels sont créés ou modifiés sur les PC clients pendant l’installation de l’application ou ultérieurement quand les clients évaluent les applications installées. Vous pouvez contrôler ces applications de telle sorte que lorsque plusieurs applications essaient de modifier un système de fichiers ou une valeur de Registre, l'application d'ordre le plus élevé est prioritaire.  

> [!IMPORTANT]  
>  Ne vous appuyez pas sur des environnements virtuels App-V pour assurer une protection, par exemple contre les programmes malveillants.  

 Suivez la procédure ci-dessous pour créer des environnements virtuels App-V dans Configuration Manager.  

## <a name="create-an-app-v-virtual-environment"></a>Créer un environnement virtuel App-V  

1.  Dans la console Configuration Manager, cliquez sur **Bibliothèque de logiciels** > **Gestion des applications** > **Environnements virtuels App-V**.  

3.  Sous l'onglet **Accueil** , dans le groupe **Créer** , cliquez sur **Créer un environnement virtuel**.  

4.  Dans la boîte de dialogue **Créer un environnement virtuel** , spécifiez les informations suivantes :  

    -   **Nom** : spécifiez un nom unique pour l’environnement virtuel avec un maximum de 128 caractères.  

    -   **Description** : si vous le souhaitez, ajoutez une description de l’environnement virtuel.  

5.  Cliquez sur **Ajouter** pour ajouter un type de déploiement à l'environnement virtuel. Vous devez ajouter au moins un type de déploiement.  

6.  Dans la boîte de dialogue **Ajouter des applications** , spécifiez le **Nom du groupe** (128 caractères maximum). Ce nom sera utilisé pour faire référence au groupe d'applications que vous ajoutez à l'environnement virtuel.  

7.  Cliquez sur **Ajouter**, sélectionnez les applications App-V 5 et les types de déploiement que vous souhaitez ajouter au groupe, puis cliquez sur **OK**.  

8.  Dans la boîte de dialogue **Ajouter des applications** , vous pouvez cliquer sur **Ordre croissant** ou **Ordre décroissant** pour indiquer quelle application est prioritaire dans le cas où plusieurs applications essaient de modifier le système de fichiers ou les paramètres de Registre dans le même environnement virtuel.  

9. Cliquez sur **OK** pour retourner à la boîte de dialogue **Créer un environnement virtuel** .  

10. Une fois que vous avez terminé d'ajouter des groupes, cliquez sur **OK** pour créer l'environnement virtuel. Le nouvel environnement virtuel apparaît dans le nœud **Environnements virtuels App-V** de la console Configuration Manager. Vous pouvez surveiller l'état de vos environnements virtuels grâce au rapport **État de l'environnement virtuel App-V**.  

    > [!NOTE]  
    >  L’environnement virtuel est ajouté ou modifié sur les PC pendant l’installation de l’application ou ultérieurement quand le client évalue les applications installées.  



<!--HONumber=Nov16_HO1-->


