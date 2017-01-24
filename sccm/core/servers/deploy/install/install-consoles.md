---
title: Installer des consoles | Microsoft Docs
description: "Découvrez comment installer des consoles Configuration Manager pour vous connecter à un site d’administration centrale ou à un site principal."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d39c201f-d364-4e7b-bde4-faa76d747f33
caps.latest.revision: 3
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 10b1010ccbf3889c58c55b87e70b354559243c90
ms.openlocfilehash: e3bc8341b384be975098d1b9d7824ef117a47ccb

---
# <a name="install-system-center-configuration-manager-consoles"></a>Installer des consoles System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*


Les utilisateurs administratifs se servent de la console System Center Configuration Manager pour gérer l’environnement Configuration Manager. Vous pouvez connecter une console Configuration Manager à un site d’administration centrale ou à un site principal, mais pas à un site secondaire.


> [!NOTE]  
>  Les objets présentés à l'utilisateur administratif exécutant la console varient en fonction des droits qui lui sont attribués. Pour plus d’informations sur l’administration basée sur des rôles, consultez [Principes de base de l’administration basée sur des rôles pour System Center Configuration Manager](../../../../core/understand/fundamentals-of-role-based-administration.md).  

 Vous pouvez installer la console Configuration Manager en même temps que le serveur de site avec l’Assistant Installation, ou exécuter l’application autonome.  

 Utilisez la procédure suivante pour installer une console Configuration Manager à l’aide de l’application autonome.  

## <a name="to-install-a-configuration-manager-console"></a>Pour installer une console Configuration Manager  

1.  Vérifiez que l’utilisateur administratif qui va exécuter l’application de la console Configuration Manager possède les droits de sécurité suivants :  

    -   Droits d’**administrateur local** sur l’ordinateur sur lequel exécuter la console.  

    -   Autorisation de **lecture** pour le dossier des fichiers d’installation de la console Configuration Manager.  

2.  Accédez à l'un des emplacements suivants :  

    -   À partir du média source de Configuration Manager, accédez à **&lt;Fichiers_source_ConfigMgr\>\Smssetup\Bin\I386**  

    -   Sur le serveur de site, accédez à **&lt;Chemin_installation_serveur_de_site_ConfigMgr\>\Tools\ConsoleSetup**  

    > [!TIP]  
    >  Il est recommandé de lancer l’installation de la console Configuration Manager à partir d’un serveur de site plutôt que du média d’installation de System Center Configuration Manager. La méthode d’installation du serveur de site copie les fichiers d’installation de la console Configuration Manager et les modules linguistiques pris en charge pour le site dans le sous-dossier **Tools\ConsoleSetup**. Si vous installez la console Configuration Manager à partir du média d’installation, cette méthode installe toujours la version anglaise, quels que soient les langues prises en charge sur le serveur de site ou les paramètres de langue du système d’exploitation s’exécutant sur l’ordinateur. Vous pouvez éventuellement copier le dossier **ConsoleSetup** vers un autre emplacement pour démarrer l’installation.  

3.  Double-cliquez sur **consolesetup.exe**. L'Assistant Installation de la console Configuration Manager s'ouvre.  

    > [!IMPORTANT]  
    >  Installez toujours la console Configuration Manager à l’aide de la commande consolesetup.exe. Il est possible d’installer la console Configuration Manager en exécutant AdminConsole.msi, mais cette méthode n’effectuant pas de vérification des conditions préalables ou des dépendances, il se peut que l’installation ne se déroule pas correctement.  

4.  Sur la page d'accueil, cliquez sur **Suivant**.  

5.  Dans la page **Serveur de site**, spécifiez le nom de domaine complet (FQDN) du serveur de site auquel la console Configuration Manager doit se connecter.  

6.  Dans la page **Dossier d’installation**, spécifiez le dossier de l’installation de la console Configuration Manager. Le chemin du dossier ne doit pas contenir d'espaces de fin ni de caractères Unicode.  

7.  Dans la page **Programme d’amélioration des services** , indiquez si vous souhaitez participer à ce programme.  

8.  Dans la page **Prêt pour l’installation**, cliquez sur **Installer** pour installer la console Configuration Manager.  

## <a name="to-install-a-configuration-manager-console-from-a-command-prompt"></a>Pour installer une console Configuration Manager à partir d'une invite de commandes  

1.  Sur le serveur à partir duquel vous installez la console Configuration Manager, ouvrez une fenêtre d’invite de commandes et accédez à l’un des emplacements suivants :  

    -   **&lt;Chemin_installation_serveur_de_site_ConfigMgr\>\Tools\ConsoleSetup**  

    -   **&lt;Média_installation_ConfigMgr\>\SMSSETUP\BIN\I386**  

    > [!TIP]  
    >  Quand vous installez une console Configuration Manager à partir d’une invite de commandes, la version anglaise est toujours installée, quel que soit le paramètre de langue défini pour le système d’exploitation s’exécutant sur l’ordinateur. Pour installer la console Configuration Manager dans une autre langue, utilisez la procédure précédente.  

2.  Tapez **consolesetup.exe** , puis choisissez parmi les options de ligne de commande suivantes.  

|  Option de ligne de commande     | Description     |
  | :------------- | :------------- |
  |/q|Installe la console Configuration Manager sans assistance. Les options **EnableSQM**, **TargetDir**et **DefaultSiteServerName** sont obligatoires avec cette option.|  
  |/uninstall|Désinstalle la console Configuration Manager. Vous devez spécifier cette option en premier lorsque vous utilisez l’option **/q** .|  
  |LangPackDir|Spécifie le chemin d'accès au dossier qui contient les fichiers de langue. Vous pouvez utiliser le **téléchargeur d’installation** pour télécharger les fichiers de langue. Si vous n'utilisez pas cette option, le programme d'installation recherche le dossier de langue dans le dossier actuel. Si le dossier de langue n'est pas trouvé, le programme d'installation poursuit l'installation en anglais uniquement. Pour plus d’informations, consultez [Téléchargeur d’installation](/sccm/core/servers/deploy/install/setup-downloader).|  
  |TargetDir|Spécifie le dossier où installer la console Configuration Manager. Vous devez spécifier cette option lorsque vous utilisez l’option **/q** .|  
  |EnableSQM|Permet de préciser si vous souhaitez vous joindre au programme d'amélioration de l'expérience utilisateur. Indiquez la valeur 1 pour participer au programme, ou la valeur 0 pour ne pas participer au programme. Vous devez spécifier cette option lorsque vous utilisez l’option **/q** .|  
  |DefaultSiteServerName|Spécifie le nom de domaine complet du serveur de site auquel la console se connecte à son ouverture. Vous devez spécifier cette option lorsque vous utilisez l’option **/q** .|  


  **Exemples d’utilisation** :  
  -  **consolesetup.exe /q TargetDir="D:\Program Files\ConfigMgr" EnableSQM=1 DefaultSiteServerName=MyServer.Contoso.com**  

  -  **consolesetup.exe /q LangPackDir=C:\Downloads\ConfigMgr TargetDir="D:\Program Files\ConfigMgr" Console EnableSQM=1 DefaultSiteServerName=MyServer.Contoso.com**  

  -  **consolesetup.exe /uninstall /q**  



<!--HONumber=Dec16_HO3-->


