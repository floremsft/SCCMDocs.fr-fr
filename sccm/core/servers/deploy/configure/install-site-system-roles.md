---
title: "Installer des rôles système de site | System Center Configuration Manager"
description: "Les Assistants vous aident à ajouter des rôles système de site à un serveur de système de site existant ou nouveau dans le site."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 61f5c774-7667-44ae-b8e4-a4951318b183
caps.latest.revision: 4
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 780ef516ddc641d53e1d2d4a5f559795cfd22cbb

---
# <a name="install-site-system-roles-for-system-center-configuration-manager"></a>Installer des rôles de système de site pour System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

La console System Center Configuration Manager comporte deux Assistants, que vous pouvez utiliser pour installer des rôles système de site :  

-   **Assistant Ajout de rôles de système de site**: utilisez cet Assistant pour ajouter des rôles de système de site à un serveur de système de site existant dans le site.  

-   **Assistant Création d'un serveur de système de site**: utilisez cet Assistant pour spécifier un nouveau serveur comme un serveur de système de site, puis installez un ou plusieurs rôles de système de site sur le serveur. Cet Assistant est le même que l' **Assistant Ajout de rôles de système de site**, sauf que sur la première page, vous devez spécifier le nom du serveur à utiliser et le site dans lequel vous souhaitez l'installer.  

Lorsque vous installez un rôle de système de site sur un ordinateur distant (y compris une instance du fournisseur SMS), le compte d'ordinateur de l'ordinateur distant est ajouté à un groupe local du serveur de site. Quand le site est installé sur un contrôleur de domaine, le groupe du serveur de site est un groupe de domaine et non un groupe local. Par ailleurs, le rôle système de site distant n’est pas opérationnel tant que l’ordinateur du rôle système de site n’a pas redémarré ou que le ticket Kerberos du compte figurant dans les [Comptes utilisés dans System Center Configuration Manager](../../../../core/plan-design/hierarchy/accounts.md) des ordinateurs distants n’a pas été actualisé.  

Juste avant d’installer le rôle système de site, Configuration Manager vérifie si l’ordinateur de destination satisfait aux prérequis des rôles système de site que vous avez sélectionnés. Lors de l’installation des rôles de système de site :  

-   Par défaut, quand Configuration Manager installe un rôle système de site, les fichiers d’installation sont installés sur le premier lecteur de disque formaté NTFS disponible dont l’espace libre disponible est le plus grand. Pour que Configuration Manager n’effectue pas l’installation sur des lecteurs spécifiques, créez un fichier vide **no_sms_on_drive.sms** et copiez-le dans le dossier racine du lecteur avant d’installer le serveur de système de site.  

-   Configuration Manager utilise le **compte d’installation du système de site** pour installer les rôles système de site. Vous spécifiez ce compte lorsque vous exécutez l'Assistant applicable pour créer un nouveau serveur de système de site ou ajouter des rôles de système de site à un serveur de système de site existant. Par défaut, ce compte est le compte de système local de l'ordinateur du serveur de site, mais vous pouvez spécifier un compte d'utilisateur de domaine à utiliser comme le compte d'installation du système de site. Pour plus d’informations, consultez le compte d’installation du système de site dans la rubrique [Comptes utilisés dans System Center Configuration Manager](../../../../core/plan-design/hierarchy/accounts.md).  

##  <a name="a-namebkmkinstalla-to-install-site-system-roles-on-an-existing-site-system-server"></a><a name="bkmk_Install"></a> Pour installer des rôles système de site sur un serveur de système de site existant  

1.  Dans la console Configuration Manager, cliquez sur **Administration**.  

2.  Dans l'espace de travail **Administration** , développez **Configuration du site**, cliquez sur **Serveurs et rôles de système de site**, puis sélectionnez le serveur que vous souhaitez utiliser pour les nouveaux rôles de système de site.  

3.  Sous l'onglet **Accueil** , dans le groupe **Serveur** , cliquez sur **Ajouter des rôles de système de site**.  

4.  Sur la page **Général** , vérifiez les paramètres, puis cliquez sur **Suivant**.  

    > [!TIP]  
    >  Pour accéder au rôle de système de site à partir d'Internet, veillez à spécifier un nom de domaine complet Internet.  

5.  Sur la page **Proxy** , spécifiez les paramètres d'un serveur proxy si les rôles de système de site qui s'exécutent sur ce serveur de système de site ont besoin d'un serveur proxy pour se connecter à des emplacements sur Internet, puis cliquez sur **Suivant**.  

6.  Sur la page **Sélection du rôle système** , sélectionnez les rôles de système de site que vous souhaitez ajouter, puis cliquez sur **Suivant**.  

7.  Effectuez toutes les étapes de l'Assistant.  

> [!TIP]  
>  L'applet de commande Windows PowerShell, New-CMSiteSystemServer, assure la même fonction que cette procédure. Pour plus d’informations, consultez [New-CMSiteSystemServer](http://go.microsoft.com/fwlink/p/?LinkID=271414) dans la documentation de référence des applets de commande System Center 2012 Configuration Manager SP1.  

## <a name="to-install-site-system-roles-on-a-new-site-system-server"></a>Pour installer des rôles de système de site sur un nouveau serveur de système de site  

1.  Dans la console Configuration Manager, cliquez sur **Administration**.  

2.  Dans l'espace de travail **Administration** , développez **Configuration du site**, puis cliquez sur **Serveurs et rôles de système de site**.  

3.  Sur l'onglet **Accueil** , dans le groupe **Créer** , cliquez sur **Créer un serveur de système de site**.  

4.  Sur la page **Général** , spécifiez les paramètres généraux du système de site, puis cliquez sur **Suivant**.  

    > [!TIP]  
    >  Pour accéder au nouveau rôle de système de site à partir d'Internet, veillez à spécifier un nom de domaine complet Internet.  

5.  Sur la page **Proxy** , spécifiez les paramètres d'un serveur proxy si les rôles de système de site qui s'exécutent sur ce serveur de système de site ont besoin d'un serveur proxy pour se connecter à des emplacements sur Internet, puis cliquez sur **Suivant**.  

6.  Sur la page **Sélection du rôle système** , sélectionnez les rôles de système de site que vous souhaitez ajouter, puis cliquez sur **Suivant**.  

7.  Effectuez toutes les étapes de l'Assistant.  

> [!TIP]  
>  L'applet de commande Windows PowerShell, New-CMSiteSystemServer, assure la même fonction que cette procédure. Pour plus d’informations, consultez [New-CMSiteSystemServer](http://go.microsoft.com/fwlink/p/?LinkID=271414) dans la documentation de référence des applets de commande System Center 2012 Configuration Manager SP1.  



<!--HONumber=Nov16_HO1-->


