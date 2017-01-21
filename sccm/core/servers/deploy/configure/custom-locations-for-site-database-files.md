---
title: "Emplacements des fichiers de base de données personnalisés | Microsoft Docs"
description: "Découvrez comment spécifier des emplacements personnalisés pour des fichiers de base de données SQL Server."
ms.custom: na
ms.date: 10/06/2016
ms.reviewer: na
ms.suite: na
ms.prod: configuration-manager
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 500a9aa6-68aa-44eb-bf49-350c1314a697
caps.latest.revision: 3
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 10b1010ccbf3889c58c55b87e70b354559243c90
ms.openlocfilehash: 3de4d4138c377c1a231947ece956ed6748dacd1f

---
# <a name="custom-locations-for-system-center-configuration-manager-site-database-files"></a>Emplacements personnalisés pour les fichiers de base de données du site System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

 System Center Configuration Manager prend en charge les emplacements personnalisés pour les fichiers de base de données SQL Server.  

> [!NOTE]  
>  Cette possibilité de spécifier des emplacements de fichiers autres que les emplacements par défaut n'est pas disponible quand vous utilisez un cluster SQL Server.  

 **Lors de l’installation** d’un nouveau site principal ou d’un site d’administration centrale, vous pouvez :  

-   Spécifier des emplacements de fichiers autres que ceux par défaut pour la base de données du site : le programme d’installation de Configuration Manager crée alors la base de données du site en utilisant ces emplacements.  

-   Spécifier l’utilisation d’une base de données SQL Server déjà créée qui utilise des emplacements de fichiers personnalisés : le programme d’installation de Configuration Manager utilise alors cette base de données déjà créée et ses emplacements de fichiers préconfigurés.  

**Après l’installation** , vous pouvez modifier l’emplacement des fichiers de base de données du site. Pour ce faire, vous devez arrêter le site et modifier l’emplacement du fichier dans SQL Server :  

-   Sur le serveur de site Configuration Manager, arrêtez le service **SMS_Executive**.  

-   Consultez la documentation de la version de SQL Server que vous utilisez pour savoir comment déplacer une base de données utilisateur. Par exemple, si vous utilisez SQL Server 2014, consultez [Déplacer des bases de données utilisateur](https://technet.microsoft.com/library/ms345483\(v=sql.120\).aspx) sur TechNet.  

-   Après avoir déplacé le fichier de base de données, redémarrez le service SMS_Executive sur le serveur de site Configuration Manager.  



<!--HONumber=Dec16_HO3-->


