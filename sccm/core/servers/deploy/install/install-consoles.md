---
title: Installer la console
titleSuffix: Configuration Manager
description: "Découvrez comment installer la console Configuration Manager pour vous connecter à un site d’administration centrale ou à un site principal."
ms.custom: na
ms.date: 1/3/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d39c201f-d364-4e7b-bde4-faa76d747f33
caps.latest.revision: "3"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: f367f94f809863403ed562a65cf44f21de698005
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/12/2017
---
# <a name="install-the-system-center-configuration-manager-console"></a>Installer la console System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Les utilisateurs administratifs se servent de la console System Center Configuration Manager pour gérer l’environnement Configuration Manager. Chaque console Configuration Manager peut se connecter à un site d’administration centrale ou à un site principal, mais pas à un site secondaire.

> [!NOTE]  
>  Les objets visibles par l’administrateur qui exécute la console dépendent des autorisations attribuées à son compte d’utilisateur. Pour plus d’informations sur l’administration basée sur des rôles, consultez [Principes de base de l’administration basée sur des rôles pour System Center Configuration Manager](../../../../core/understand/fundamentals-of-role-based-administration.md).  

 Vous pouvez installer la console Configuration Manager pendant l’installation du serveur de site via l’Assistant Installation, ou vous pouvez exécuter une application d’installation autonome qui utilise l’Assistant Installation.  

 Procédez comme suit pour installer une console Configuration Manager à l’aide de l’application autonome.  

## <a name="to-install-the-configuration-manager-console-by-using-the-setup-wizard"></a>Pour installer la console Configuration Manager à l’aide de l’Assistant Installation  

1.  Vérifiez que vous disposez des droits suivants :  

    -  Les droits d’**Administrateur local** sur l’ordinateur sur lequel la console doit s’exécuter.  

    -   Les droits de **Lecture** sur l’emplacement des fichiers d’installation de la console Configuration Manager.  

2.  Accédez à l’un des emplacements suivants :  

    -   Sur le serveur de site, accédez à **<*Chemin d’installation du serveur de site Configuration Manager*>\Tools\ConsoleSetup**.  

    -   À partir du média source de Configuration Manager, accédez à **<*Fichiers sources de Configuration Manager*>\Smssetup\Bin\I386**.  

    > [!TIP]  
    >  Nous vous recommandons de lancer l’installation de la console Configuration Manager à partir d’un serveur de site plutôt que du média d’installation de System Center Configuration Manager. La méthode d’installation du serveur de site copie les fichiers d’installation de la console Configuration Manager et les modules linguistiques pris en charge pour le site dans le sous-dossier **Tools\ConsoleSetup**. L’installation de la console Configuration Manager à partir du média d’installation installe toujours la version anglaise, indépendamment des langues prises en charge sur le serveur de site ou des paramètres de langue du système d’exploitation s’exécutant sur l’ordinateur. Vous pouvez éventuellement copier le dossier **ConsoleSetup** vers un autre emplacement pour démarrer l’installation.

3.  Pour ouvrir l’Assistant Installation de la console Configuration Manager, double-cliquez sur **consolesetup.exe**.  

    > [!IMPORTANT]  
    >  Installez toujours la console Configuration Manager à l’aide de la commande consolesetup.exe. Même si vous pouvez installer la console Configuration Manager en exécutant adminconsole.msi, cette méthode ne vérifie pas les prérequis ou les dépendances, et l’installation risque de ne pas se dérouler correctement.  

4.  Dans l’Assistant, sélectionnez **Suivant**.  

5.  Dans la page **Serveur de site**, entrez le nom de domaine complet (FQDN) du serveur de site auquel la console Configuration Manager doit se connecter.  

6.  Dans la page **Dossier d’installation**, entrez le dossier d’installation de la console Configuration Manager. Le chemin du dossier ne doit pas contenir d'espaces de fin ni de caractères Unicode.  

7.  Dans la page **Programme d’amélioration des services**, indiquez si vous voulez participer à ce programme.  

8.  Dans la page **Prêt pour l’installation**, cliquez sur **Installer** pour installer la console Configuration Manager.  

## <a name="to-install-the-configuration-manager-console-from-a-command-prompt"></a>Pour installer la console Configuration Manager à partir d’une invite de commandes  

1.  Sur le serveur à partir duquel vous installez la console Configuration Manager, ouvrez une fenêtre d’invite de commandes et accédez à l’un des emplacements suivants :  

    -   **<*Chemin d’installation du serveur de site Configuration Manager*>\Tools\ConsoleSetup**  

    -   **<*Média d’installation de Configuration Manager*>\SMSSETUP\BIN\I386**  

    > [!TIP]  
    >  Quand vous installez une console Configuration Manager à partir d’une invite de commandes, la version anglaise est toujours installée, quel que soit le paramètre de langue défini pour le système d’exploitation s’exécutant sur l’ordinateur. Pour installer la console Configuration Manager dans une langue autre que l’anglais, vous devez [installer la console Configuration Manager à l’aide de l’Assistant Installation](#to-install-the-configuration-manager-console-by-using-the-setup-wizard).  

2.  À partir de l’invite de commandes, tapez **consolesetup.exe**. Choisissez l’une des options de ligne de commande suivantes.  

|  Option de ligne de commande     | Description     |
  | :------------- | :------------- |
  |/q|Installe la console Configuration Manager sans assistance. Les options **EnableSQM**, **TargetDir**et **DefaultSiteServerName** sont obligatoires avec cette option.|  
  |/uninstall|Désinstalle la console Configuration Manager. Vous devez spécifier cette option en premier lorsque vous utilisez l’option **/q** .|  
  |LangPackDir|Spécifie le chemin d'accès au dossier qui contient les fichiers de langue. Vous pouvez utiliser le **téléchargeur d’installation** pour télécharger les fichiers de langue. Si vous n'utilisez pas cette option, le programme d'installation recherche le dossier de langue dans le dossier actuel. Si le dossier de langue n'est pas trouvé, le programme d'installation poursuit l'installation en anglais uniquement. Pour plus d’informations, consultez [Téléchargeur d’installation](setup-downloader.md).|  
  |TargetDir|Spécifie le dossier où installer la console Configuration Manager. Vous devez spécifier cette option lorsque vous utilisez l’option **/q** .|  
  |EnableSQM|Permet de préciser si vous souhaitez vous joindre au programme d'amélioration de l'expérience utilisateur. Utilisez la valeur **1** pour participer au programme d’amélioration des services et la valeur **0** pour ne pas participer au programme. Vous devez spécifier cette option lorsque vous utilisez l’option **/q** .|  
  |DefaultSiteServerName|Spécifie le nom de domaine complet du serveur de site auquel la console se connecte à son ouverture. Vous devez spécifier cette option lorsque vous utilisez l’option **/q** .|  


  **Exemples :**

  -  **consolesetup.exe /q TargetDir="D:\Program Files\ConfigMgr" EnableSQM=1 DefaultSiteServerName=MyServer.Contoso.com**  

  -  **consolesetup.exe /q LangPackDir=C:\Downloads\ConfigMgr TargetDir="D:\Program Files\ConfigMgr" Console EnableSQM=1 DefaultSiteServerName=MyServer.Contoso.com**  

  -  **consolesetup.exe /uninstall /q**  
