---
title: "Bibliothèque de contenu| System Center Configuration Manager"
description: "Découvrez la bibliothèque de contenu qu’utilise System Center Configuration Manager pour réduire la taille globale du contenu distribué."
ms.custom: na
ms.date: 10/06/2016
ms.reviewer: na
ms.suite: na
ms.prod: configuration-manager
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 65c88e54-3574-48b0-a127-9cc914a89dca
caps.latest.revision: 4
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 5406dcbc8b1ca04f2754e19b171c55ab20a00d46

---
# <a name="the-content-library-in-system-center-configuration-manager"></a>Bibliothèque de contenu System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

La bibliothèque de contenu est l’emplacement de stockage SIS (Single-Instance Store) qu’utilise Configuration Manager pour réduire la taille globale de l’ensemble du contenu que vous distribuez. La bibliothèque de contenu stocke tous les fichiers de contenu pour le déploiement des mises à jour logicielles, des applications, du système d'exploitation, etc.

 - Une copie de la bibliothèque de contenu est automatiquement créée et gérée sur chaque **serveur de site** et chaque **point de distribution**.
 - Avant de télécharger les fichiers de contenu vers le serveur de site ou de copier les fichiers sur les points de distribution, Configuration Manager vérifie si chaque fichier de contenu se trouve déjà dans la bibliothèque de contenu.
 - Si le fichier de contenu est disponible, Configuration Manager ne le copie pas et associe le fichier de contenu existant à l’application ou au package.

Sur les ordinateurs sur lesquels vous installez un point de distribution, vous pouvez configurer les éléments suivants :
- les lecteurs de disque sur lesquels vous voulez créer la bibliothèque de contenu ;
- une priorité pour chaque lecteur que vous utilisez.

Quand Configuration Manager copie des fichiers de contenu, il les copie sur le lecteur présentant la plus haute priorité, sauf si ce lecteur dispose d’une quantité d’espace libre inférieure à la quantité minimale spécifiée.
- Vous configurez les paramètres de lecteur au moment de l’installation du point de distribution.
- Vous ne pouvez pas configurer les paramètres de lecteur dans les propriétés du point de distribution une fois l’installation terminée.


Pour plus d’informations sur la configuration des paramètres de lecteur pour le point de distribution, consultez [Gérer le contenu et l’infrastructure de contenu pour System Center Configuration Manager](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  


>  [!IMPORTANT]  
>  Pour déplacer la bibliothèque de contenu à un autre emplacement sur un point de distribution après l’installation, utilisez l’**outil de transfert de bibliothèque de contenu** dans la boîte à outils de System Center 2012 R2 Configuration Manager. Vous pouvez télécharger les outils depuis le [Centre de téléchargement Microsoft](http://go.microsoft.com/fwlink/?LinkId=279566).  

## <a name="about-the-content-library-on-the-central-administration-site"></a>À propos de la bibliothèque de contenu sur le site d’administration centrale  
 Par défaut, Configuration Manager crée une bibliothèque de contenu sur le site d’administration centrale pendant l’installation du site. La bibliothèque de contenu est placée sur le lecteur du serveur de site possédant l'espace disponible le plus important. Étant donné que vous ne pouvez pas installer un point de distribution sur le site d'administration centrale, vous ne pouvez pas attribuer une priorité aux lecteurs à utiliser pour la bibliothèque de contenu. Comme la bibliothèque de contenu sur d'autres serveurs de site ou sur des points de distribution, lorsque le lecteur contenant la bibliothèque de contenu n'a plus d'espace disponible, la bibliothèque de contenu s'étend sur le lecteur disponible suivant.  

 Configuration Manager utilise la bibliothèque de contenu sur le site d’administration centrale dans les scénarios suivants :  

-   Lorsque vous créez un contenu sur le site d'administration centrale.  

-   Lorsque vous migrez le contenu depuis un autre site Configuration Manager et affectez le site d'administration centrale comme site de gestion du contenu.  

> [!NOTE]  
>  Lorsque vous créez un contenu sur un site principal, puis le distribuez à un autre site principal ou à un site secondaire sous un autre site principal, le site d'administration centrale stocke temporairement ce contenu dans la boîte de réception du planificateur sur le site d'administration centrale, sans toutefois ajouter ce contenu à sa bibliothèque de contenu.  

 Utilisez les options suivantes pour gérer la bibliothèque de contenu sur le site d'administration centrale :  

-   Pour empêcher la bibliothèque de contenu de s'installer sur un lecteur spécifique, créez un fichier vide intitulé **no_sms_on_drive.sms** et copiez-le vers le dossier racine du lecteur avant la création de la bibliothèque de contenu.  

-   Après avoir créé la bibliothèque de contenu, utilisez l’**outil de transfert de bibliothèque de contenu** de la boîte à outils System Center 2012 R2 Configuration Manager pour gérer l’emplacement de la bibliothèque de contenu. Vous pouvez télécharger les outils depuis le [Centre de téléchargement Microsoft](http://go.microsoft.com/fwlink/?LinkId=279566).  



<!--HONumber=Nov16_HO1-->


