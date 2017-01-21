---
title: Installation via la ligne de commande | System Center Configuration Manager
description: "Découvrez comment exécuter le programme d’installation de System Center Configuration Manager à partir d’une invite de commandes pour diverses installations de site."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e7cdb1a9-140a-436e-ac71-72d083110223
caps.latest.revision: 3
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: ea097188351cd60a13659e2860c5e0a2bac2c069

---
# <a name="use-a-command-line-to-install-system-center-configuration-manager-sites"></a>Utiliser une ligne de commande pour installer des sites de System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

 Si vous le souhaitez, vous pouvez exécuter le programme d’installation de System Center Configuration Manager à partir d’une invite de commandes pour diverses installations de site.

 ## <a name="supported-tasks-for-command-line-installs"></a>Tâches prises en charge pour des installations via la ligne de commande
 Cette méthode consistant à exécuter le programme d’installation prend en charge les tâches d’installation de site et de maintenance de site suivantes :

-   **Installez un site d’administration centrale ou un site principal à partir d’une ligne de commande :**  
  Consultez la rubrique [Options de ligne de commande pour le programme d’installation](../../../../core/servers/deploy/install/command-line-options-for-setup.md).

 -  **Modifiez les langues utilisées sur un site d’administration centrale ou un site principal :**  
    Pour modifier les langues installées sur un site à partir d’une ligne de commande (y compris les langues d’appareils mobiles), procédez comme suit :  

     -   Exécutez le programme d’installation à partir de **&lt;chemin_installation_Configuraton_Manager\>\Bin\X64** sur le serveur de site.
     -   Utilisez l’option de ligne de commande **/MANAGELANGS**
     -   Spécifiez un fichier de jeu de caractères définissant les langues à ajouter ou supprimer.  

    Par exemple, utilisez la syntaxe de commande suivante : **setupwpf.exe /MANAGELANGS &lt;fichier de script de langue\>**.  

    Pour créer le fichier de script de langue, utilisez les informations fournies dans [Options de ligne de commande pour gérer les langues](../../../../core/servers/deploy/install/command-line-options-for-setup.md#bkmk_Lang).  

 -  **Utilisez un fichier de script d’installation pour les installations sans assistance de site ou la récupération de site :**  
    Vous pouvez exécuter le programme d’installation à partir d’une ligne de commande en demandant au programme d’installation d’utiliser un script d’installation et d’effectuer une installation sans assistance de site. Vous pouvez aussi utiliser cette option pour récupérer un site.    

    Pour utiliser un script avec le programme d’installation :  

    -   Exécutez le programme d’installation avec l’option de ligne de commande **/SCRIPT** et spécifiez un fichier de script.  

    -   Le fichier de script doit être configuré avec les clés et valeurs requises.  

    Pour effectuer une installation sans assistance d’un site d’administration centrale ou d’un site principal, le fichier de script doit être configuré avec les sections suivantes :  

    -   Identification    
    -   Options    
    -   SQLConfigOptions    
    -   HierarchyOptions    

    -   CloudConnectorOptions  

    Pour récupérer un site, vous devez configurer les sections suivantes du fichier de script :  

    -   Identification  

    -   Récupération

     Pour plus d’informations sur la sauvegarde et la récupération, consultez la section « Clés du fichier de script de récupération de site sans assistance » dans la rubrique « Sauvegarde et récupération dans Configuration Manager ».  

    Consultez [Clés du fichier de script d’installation sans assistance](../../../../core/servers/deploy/install/command-line-options-for-setup.md#bkmk_Unattended) pour obtenir la liste des clés et des valeurs à utiliser dans un fichier de script d’installation sans assistance.  

## <a name="about-the-command-line-script-file"></a>À propos du fichier de script de ligne de commande  

 Pour réaliser une installation sans assistance de Configuration Manager, vous pouvez exécuter le programme d’installation avec l’option de ligne de commande **/SCRIPT** et spécifier un fichier de script contenant les options d’installation. Avec cette méthode, vous pouvez effectuer les tâches suivantes :  

-   Installer un site d’administration centrale  

-   Installer un site principal  

-   Installer une console Configuration Manager  

-   Récupérer un site  

> [!NOTE]  
>  Vous ne pouvez pas utiliser le fichier de script d’installation sans assistance pour mettre à niveau un site d’évaluation vers une installation sous licence de Configuration Manager.  

**Pour créer le script** :  
Le script d’installation est automatiquement créé lorsque vous [exécutez le programme d’installation pour installer un site à l’aide de l’interface utilisateur](../../../../core/servers/deploy/install/use-the-setup-wizard-to-install-sites.md).  Quand vous confirmez les paramètres dans la page **Résumé** de l’Assistant :  

-   Le programme d’installation crée le script **%TEMP%\ConfigMgrAutoSave.ini**.  Vous pouvez renommer ce fichier avant de l’utiliser, en veillant à conserver l’extension de fichier .ini.  

-   Le script d'installation sans assistance contient les paramètres que vous avez sélectionnés dans l'Assistant.  

-   Une fois que le script est créé, vous pouvez le modifier pour installer d'autres sites dans votre hiérarchie.  

-   Vous pouvez ensuite utiliser ce script pour effectuer une installation sans assistance de Configuration Manager.  

Le fichier de script fournit les mêmes informations que l’Assistant Installation demande, à l’exception des paramètres par défaut.   
Toutes les valeurs doivent être spécifiées pour les clés d'installation qui s'appliquent au type d'installation utilisé.  

Lorsque le programme d'installation crée le script d'installation sans assistance, il est rempli avec la valeur de clé de produit que vous entrez pendant l'installation. Cette valeur peut être une clé de produit valide, ou être égale à EVAL si vous installez une version d’évaluation de Configuration Manager. Le script est rempli avec la valeur de clé de produit pour permettre la vérification requise finale.  

Lorsque le programme d'installation démarre l'installation effective du site, le script créé automatiquement fait l'objet d'une nouvelle écriture pour effacer la valeur de clé de produit dans le script créé. Avant d’utiliser le script pour une installation sans assistance d’un nouveau site, vous pouvez modifier le script pour fournir une clé de produit valide ou spécifier une installation d’évaluation de Configuration Manager.  

**Le script contient les noms de section, les noms de clé et les valeurs :**  

-   Les noms de clés de section requis varient en fonction du type d’installation faisant l’objet du script.  

-   L’ordre des clés dans les sections et l’ordre des sections dans le fichier n’ont pas d’importance.  

-   Les clés ne respectent pas la casse.  

-   Lorsque vous attribuez une valeur à une clé, le nom de celle-ci doit être suivi du signe égal (=) et de la valeur de la clé.  

> [!TIP]  
>  Pour connaître l’ensemble complet des options, consultez [Options de ligne de commande pour le programme d’installation et les scripts](../../../../core/servers/deploy/install/command-line-options-for-setup.md).  

## <a name="to-use-the-script-setup-command-line-option"></a>Pour utiliser l’option de ligne de commande /SCRIPT du programme d’installation :

-   Utilisez un fichier de script d’installation et spécifiez le nom du fichier après l’option de ligne de commande **/SCRIPT** du programme d’installation.  

    -   Le nom du fichier doit avoir l’extension de nom de fichier **.ini** .  

    -   Quand vous faites référence au fichier de script du programme d’installation à l’invite de commandes, indiquez le chemin complet du fichier. Par exemple, si votre fichier d’initialisation du programme d’installation est nommé Setup.ini et se trouve dans le dossier C:\Setup, à l’invite de commandes, tapez ce qui suit :  **setup /script c:\setup\setup.ini**  

-   Le compte qui exécute le programme d’installation doit avoir les autorisations d’administration sur l’ordinateur. Si vous exécutez le programme d’installation avec le script sans assistance, démarrez l’invite de commandes en utilisant **Run as administrator**.  



<!--HONumber=Nov16_HO1-->


