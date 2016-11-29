---
title: "Désinstaller des sites | System Center Configuration Manager"
description: "Utilisez ces informations comme référence lorsque quand vous devez désinstaller un site System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d466edd2-97f0-44c1-a73e-d71abbdbf4a8
caps.latest.revision: 6
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: db203f6b8b76df28b2cd03f5ebd931c520294ba6


---
# <a name="uninstall-sites-and-hierarchies-in-system-center-configuration-manager"></a>Désinstaller des sites et des hiérarchies dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Utilisez les informations suivantes comme référence quand vous devez désinstaller un site System Center Configuration Manager.  

Pour retirer une hiérarchie comportant plusieurs sites, l’ordre de suppression est important :  

-   Commencez par désinstaller les sites en bas de la hiérarchie, puis remontez la hiérarchie.  

-   Tout d’abord, supprimez les sites secondaires rattachés aux sites principaux.  

-   Ensuite, supprimez les sites principaux.  

-   Une fois tous les sites principaux supprimés, vous pouvez désinstaller le site d’administration centrale.  


##  <a name="a-namebkmkremovesecondarysitea-remove-a-secondary-site-from-a-hierarchy"></a><a name="BKMK_RemoveSecondarysite"></a> Supprimer un site secondaire d’une hiérarchie  
Vous ne pouvez pas déplacer ou réattribuer des sites secondaires vers un nouveau site principal parent. Pour supprimer un site secondaire d'une hiérarchie, il doit être supprimé de son site parent direct. Pour ce faire, utilisez l’Assistant Suppression d’un site secondaire de la console Configuration Manager. Lors de la suppression d'un site secondaire, vous devez choisir entre le supprimer et le désinstaller :  

-   **Désinstaller le site secondaire**: utilisez cette option pour supprimer un site secondaire fonctionnel accessible à partir du réseau. Cette option désinstalle Configuration Manager du serveur de site secondaire et supprime toutes les informations relatives au site et ses ressources de la hiérarchie Configuration Manager. Si Configuration Manager a installé SQL Server Express dans le cadre de l’installation du site secondaire, SQL Express est désinstallé en même temps que le site secondaire. En revanche, si SQL Server Express a été installé avant le site secondaire, Configuration Manager ne désinstalle pas SQL Server Express.  

-   **Supprimer le site secondaire**: utilisez cette option dans l’un des cas de figure suivants :  

    -   L'installation d'un site secondaire a échoué.  

    -   Le site secondaire continue de figurer dans la console Configuration Manager après sa désinstallation.  

    Cette option supprime toutes les informations relatives au site et ses ressources de la hiérarchie Configuration Manager, mais laisse Configuration Manager installé sur le serveur de site secondaire.  

    > [!NOTE]  
    >  Vous pouvez également utiliser l’outil de maintenance hiérarchique et l’option **/DELSITE** pour supprimer un site secondaire. Pour plus d’informations, consultez [Outil de maintenance hiérarchique (Preinst.exe) pour System Center Configuration Manager](../../../../core/servers/manage/hierarchy-maintenance-tool-preinst.exe.md).  

#### <a name="to-uninstall-or-delete-a-secondary-site"></a>Pour désinstaller ou supprimer un site secondaire  

1.  Vérifiez que l'utilisateur administratif exécutant le programme d'installation possède les droits de sécurité suivants :  

    -   Droits d'administration sur l'ordinateur de site secondaire.  

    -   Droits d'administrateur local sur le serveur de base de données de site distant pour le site principal, s'il est distant  

    -   Rôle de sécurité d'administrateur d'infrastructure ou d'administrateur complet sur le site principal parent.  

    -   Droits d'administrateur système sur la base de données de site du site secondaire.  

2.  Dans la console Configuration Manager, cliquez sur **Administration**.  

3.  Dans l'espace de travail **Administration** , développez **Configuration du site**, puis cliquez sur **Sites**.  

4.  Sélectionnez le serveur de site secondaire à supprimer.  

5.  Sous l' onglet **Accueil** , dans le groupe **Site** , cliquez sur **Supprimer**.  

6.  Sur la page **Général** , indiquez si vous souhaitez désinstaller ou supprimer le site secondaire, puis cliquez sur **Suivant**.  

7.  Vérifiez les paramètres de la page **Résumé** , puis cliquez sur **Suivant**.  

8.  Sur la page **Dernière étape** , cliquez sur **Fermer** pour quitter l'Assistant.  

##  <a name="a-namebkmkuninstallprimarya-uninstall-a-primary-site"></a><a name="BKMK_UninstallPrimary"></a> Désinstaller un site principal  
Vous pouvez exécuter le programme d’installation de Configuration Manager pour désinstaller un site principal auquel aucun site secondaire n’est associé. Avant de désinstaller un site principal, prenez connaissance des remarques suivantes :  

-   Quand des clients Configuration Manager se trouvent dans les limites configurées au niveau du site et que le site principal fait partie d’une hiérarchie Configuration Manager, envisagez d’ajouter les limites à un autre site principal de la hiérarchie avant de désinstaller le site principal.  

-   Lorsque le serveur de site principal n'est plus disponible, vous devez utiliser l'outil de maintenance hiérarchique au niveau du site d'administration centrale afin de supprimer le site principal de la base de données de site. Pour plus d’informations, consultez [Outil de maintenance hiérarchique (Preinst.exe) pour System Center Configuration Manager](../../../../core/servers/manage/hierarchy-maintenance-tool-preinst.exe.md).  

Pour désinstaller un site principal, suivez les instructions ci-dessous.  

#### <a name="to-uninstall-a-primary-site"></a>Pour désinstaller un site principal  

1.  Vérifiez que l'utilisateur administratif exécutant le programme d'installation possède les droits de sécurité suivants :  

    -   Droits d'administrateur local sur le serveur de site d'administration centrale  

    -   Droits d'administrateur local sur le serveur de base de données de site distant pour le site d'administration centrale, s'il est distant  

    -   Droits d'administrateur système sur la base de données du site d'administration centrale.  

    -   Droits d'administrateur local sur l'ordinateur de site principal  

    -   Droits d'administrateur local sur le serveur de base de données de site distant pour le site principal, s'il est distant  

    -   Nom d'utilisateur associé au rôle de sécurité Administrateur d'infrastructure ou le rôle Administrateur complet sur le site d'administration centrale  

2.  Démarrez le programme d’installation de Configuration Manager sur le serveur de site principal en utilisant l’une des méthodes suivantes :  

    -   Dans le menu **Démarrer**, cliquez sur **Installation de Configuration Manager**.  

    -   Ouvrez Setup.exe à partir de &lt;*SupportInstallationConfigMgr*>\SMSSETUP\BIN\X64.  

    -   Ouvrez Setup.exe à partir de &lt;*CheminInstallationConfigMgr*>\BIN\X64.  

3.  Dans la page **Avant de commencer** , cliquez sur **Suivant**.  

4.  Sur la page **Mise en route** , sélectionnez **Désinstaller le site Configuration Manager**, puis cliquez sur **Suivant**.  

5.  Dans la page **Désinstaller le site Configuration Manager**, indiquez si vous souhaitez supprimer la base de données de site du serveur de site principal et si vous souhaitez supprimer la console Configuration Manager. Par défaut, le programme d'installation supprime les deux éléments.  

    > [!IMPORTANT]  
    >  Lorsqu'un site secondaire est associé au site principal, vous devez au préalable supprimer le site secondaire pour pouvoir désinstaller le site principal.  

6.  Cliquez sur **Oui** pour confirmer la désinstallation du site principal Configuration Manager.  

##  <a name="a-namebkmkuninstallprimarydistviewsa-uninstall-a-primary-site-that-is-configured-with-distributed-views"></a><a name="BKMK_UninstallPrimaryDistViews"></a> Désinstaller un site principal configuré avec des vues distribuées  
 Pour pouvoir désinstaller un site principal enfant dont le lien de réplication vers le site d'administration centrale contient des vues distribuées, vous devez désactiver les vues distribuées dans votre hiérarchie. Avant de désinstaller un site principal, aidez-vous des informations ci-dessous pour désactiver les vues distribuées.  

#### <a name="to-uninstall-a-primary-site-that-is-configured-with-distributed-views"></a>Pour désinstaller un site principal configuré avec des vues distribuées  

1.  Avant de désinstaller un site principal, vous devez désactiver les vues distribuées sur chaque lien de la hiérarchie reliant le site d'administration centrale et un site principal.  

2.  Après avoir désactivé les vues distribuées sur chaque lien, vérifiez que les données du site principal sont bien réinitialisées au niveau du site d'administration centrale. Vous pouvez surveiller l’initialisation des données en affichant le lien dans le nœud **Réplication de la base de données** de l’espace de travail **Surveillance** de la console Configuration Manager.  

3.  Une fois les données réinitialisées auprès du site d'administration centrale, vous pouvez désinstaller le site principal. Pour désinstaller un site principal, voir la section [Désinstaller un site principal](#BKMK_UninstallPrimary) dans cette rubrique.  

4.  Une fois que le site principal a été entièrement désinstallé, vous pouvez reconfigurer les vues distribuées sur les liens vers les sites principaux.  

    > [!IMPORTANT]  
    >  Si vous désinstallez le site principal avant de désactiver les vues distribuées de chaque site ou avant de réinitialiser les données du site principal au niveau du site d'administration centrale, la réplication des données entre les sites principaux et le site d'administration centrale risque d'échouer. Dans ce scénario, vous devez désactiver les vues distribuées pour chaque lien de la hiérarchie, puis une fois que les données ont bien été réinitialisées au niveau du site d'administration centrale, vous pouvez reconfigurer les vues distribuées.  

##  <a name="a-namebkmkuninstallcasa-uninstall-the-central-administration-site"></a><a name="BKMK_UninstallCAS"></a> Désinstaller le site d’administration centrale  
 Vous pouvez exécuter le programme d’installation de Configuration Manager pour désinstaller un site d’administration centrale qui ne possède pas de sites principaux enfants. Pour désinstaller un site d'administration centrale, suivez les instructions ci-dessous.  

#### <a name="to-uninstall-a-central-administration-site"></a>Pour désinstaller un site d'administration centrale  

1.  Vérifiez que l'utilisateur administratif exécutant le programme d'installation possède les droits de sécurité suivants :  

    -   Droits d'administrateur local sur le serveur de site d'administration centrale  

    -   Droits d'administrateur local sur le serveur de base de données de site pour le site d'administration centrale, lorsque le serveur de base de données de site n'est pas installé sur le serveur de site  

2.  Démarrez le programme d’installation de Configuration Manager sur le serveur de site d’administration centrale en utilisant l’une des méthodes suivantes :  

    -   Dans le menu **Démarrer**, cliquez sur **Installation de Configuration Manager**.  

    -   Ouvrez Setup.exe à partir de &lt;*SupportInstallationConfigMgr*>\SMSSETUP\BIN\X64.  

    -   Ouvrez Setup.exe à partir de &lt;*CheminInstallationConfigMgr*>\BIN\X64.  

3.  Dans la page **Avant de commencer** , cliquez sur **Suivant**.  

4.  Sur la page **Mise en route** , sélectionnez **Désinstaller le site Configuration Manager**, puis cliquez sur **Suivant**.  

5.  Dans la page **Désinstaller le site Configuration Manager**, indiquez si vous souhaitez supprimer la base de données de site du serveur de site d’administration centrale et si vous souhaitez supprimer la console Configuration Manager. Par défaut, le programme d'installation supprime les deux éléments.  

    > [!IMPORTANT]  
    >  Si un site principal est associé au site d'administration centrale, vous devez désinstaller le site principal pour pouvoir désinstaller le site d'administration centrale.  

6.  Cliquez sur **Oui** pour confirmer la désinstallation du site d’administration centrale Configuration Manager.  



<!--HONumber=Nov16_HO1-->


