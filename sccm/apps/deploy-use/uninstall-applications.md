---
title: "Désinstaller des applications | System Center Configuration Manager"
description: "Désinstaller une application à l’aide de System Center Configuration Manager"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0ea3edaa-27c6-4391-9896-cd97d9c5d06d
caps.latest.revision: 4
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 9f654d899a1e3e1603eccb3943ffc4d4c178e143


---
# <a name="uninstall-applications-with-system-center-configuration-manager"></a>Désinstaller des applications avec System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*


## <a name="introduction"></a>Introduction  
  
-   Sur la page **Contenu** de l' **Assistant Création d'un type de déploiement**, entrez la ligne de commande permettant de désinstaller le contenu du type de déploiement.  

-   Déployez l'application en utilisant l'action de déploiement **Désinstaller**.  

> [!IMPORTANT]  
>  Certains types d'application ne permettent pas la désinstallation.  

 La liste suivante offre des informations complémentaires sur le comportement de la fonctionnalité de désinstallation des applications :  

-   Quand vous désinstallez une application Configuration Manager, toutes les applications qui en dépendent ne sont pas automatiquement désinstallées.  

-   Si vous déployez une application auprès d'un utilisateur une application en utilisant l'action **Désinstaller** et que l'application a été installée pour tous les utilisateurs de l'ordinateur, la désinstallation peut échouer si le compte de l'utilisateur ne dispose pas des autorisations requises désinstaller l'application.  

-   Si vous supprimez un utilisateur ou un périphérique à partir d'un regroupement qui dispose d'une application déployée, l'application ne sera pas automatiquement supprimée du périphérique.  

-   Un déploiement dont l'objet est **Désinstaller** ne vérifie pas les règles de spécification. Si l'application est installée sur l'ordinateur sur lequel s'exécute le déploiement, elle sera désinstallée.  

> [!IMPORTANT]  
>  Pour pouvoir déployer l'application en utilisant l'action de déploiement **Désinstaller**, vous devez au préalable supprimer les déploiements existants ou les déploiements simulés d'applications sur un regroupement.  
  
 Pour plus d’informations sur la manière de créer un type de déploiement, consultez [Créer des applications](../../apps/deploy-use/create-applications.md).  
  
 Pour plus d’informations sur le déploiement d’une application, consultez [Déployer des applications](../../apps/deploy-use/deploy-applications.md).  
  
## <a name="uninstall-an-application"></a>Désinstaller une application  

1.  Configurez le type de déploiement d'application avec la ligne de commande de désinstallation en utilisant l'une des méthodes suivantes :  

    -   Sur la page **Général** de l' **Assistant Création d'un type de déploiement**sélectionnez l'option **Identifier automatiquement les informations sur ce type de déploiement à partir des fichiers d'installation**. Si les informations sont disponibles dans les fichiers d'installation, la ligne de commande de désinstallation est automatiquement ajoutée aux propriétés du type de déploiement.  

    -   Sur la page **Contenu** de l' **Assistant Création d'un type de déploiement**, dans le champ **Programme de désinstallation** , spécifiez la ligne de commande pour désinstaller l'application.  

        > [!NOTE]  
        >  La page **Contenu** ne s'affiche que si vous sélectionnez l'option **Spécifier manuellement les informations sur le type de déploiement** sur la page **Général** de l' **Assistant Création d'un type de déploiement**.  

    -   Sous l’onglet **Programmes** de la boîte de dialogue *Propriétés de***<nom_type_déploiement\>**, spécifiez la ligne de commande pour désinstaller l’application dans le champ **Programme de désinstallation**.  

2.  Déployez l'application et sélectionnez l'action de déploiement **Désinstaller** sur la page **Paramètres de déploiement** de l' **Assistant Déploiement logiciel**.  

    > [!NOTE]  
    >  Lorsque vous sélectionnez l'action de déploiement **Désinstaller**, l'objet du déploiement est automatiquement configuré comme **Obligatoire**.  



<!--HONumber=Nov16_HO1-->


