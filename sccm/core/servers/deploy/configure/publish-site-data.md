---
title: "Publier des données de site | System Center Configuration Manager"
description: "Découvrez comment publier des sites Configuration Manager dans les services de domaine Active Directory."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 17cf034f-eaff-43ce-bc8e-917213c1db74
caps.latest.revision: 8
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: cda87a3bdcbba342f111b68af75369ca14744441


---
# <a name="publish-site-data-for-system-center-configuration-manager"></a>Publication de données de site pour System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Après avoir développé le schéma Active Directory pour System Center Configuration Manager, vous pouvez publier des sites Configuration Manager vers les services de domaine Active Directory (AD DS) pour que les ordinateurs Active Directory puissent récupérer en toute sécurité des informations du site à partir d’une source approuvée. La publication des informations du site sur AD DS n’est pas obligatoire pour les fonctionnalités de base de Configuration Manager, mais cette configuration contribue à réduire la surcharge administrative.  

-   **Quand un site est configuré pour publier dans AD DS**, les clients Configuration Manager peuvent trouver automatiquement des points de gestion via la publication Active Directory à l’aide d’une requête LDAP adressée à un serveur de catalogue global.  

-   **Quand un site ne publie pas dans AD DS**, les clients doivent utiliser une autre méthode pour rechercher leur point de gestion par défaut.  

Pour plus d’informations sur la façon dont les clients trouvent un point de gestion, consultez [Comprendre comment les clients recherchent des services et des ressources de site pour System Center Configuration Manager](../../../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md).  

## <a name="configure-sites-to-publish-to-ad-ds"></a>Configuration des sites à publier dans AD DS  
 Les étapes principales sont les suivantes :  

-   Vous devez [étendre le schéma Active Directory pour System Center Configuration Manager](../../../../core/plan-design/network/extend-the-active-directory-schema.md) dans chaque forêt où vous allez publier des données de site, puis vérifier que le conteneur **System Management** est présent.  

-   Vous devez accorder au compte d’ordinateur de chaque site principal devant publier des données le   **contrôle intégral** sur le conteneur **System Management** et tous ses objets enfants.  

#### <a name="to-enable-a-configuration-manager-site-to-publish-site-information-to-active-directory-forest"></a>Pour autoriser un site Configuration Manager à publier des informations de site vers une forêt Active Directory :  

1.  Dans la console Configuration Manager, cliquez sur **Administration**.  

2.  Dans l'espace de travail **Administration** , développez **Configuration du site** , puis cliquez sur **Sites**. Sélectionnez le site que vous souhaitez configurer pour qu'il puisse publier ses données de site, puis sous l'onglet **Accueil** , dans le groupe **Propriétés** , cliquez sur **Propriétés**.  

3.  Sous l'onglet **Publication** des propriétés du site, sélectionnez les forêts vers lesquelles ce site devra publier les données de site.  

4.  Cliquez sur **OK** pour enregistrer la configuration.  

 Pour configurer une forêt Active Directory pour la publication, procédez comme suit :  

#### <a name="to-configure-active-directory-forests-for-publishing"></a>Pour configurer des forêts Active Directory pour la publication :  

1.  Dans la console Configuration Manager, cliquez sur **Administration**.  

2.  Dans l'espace de travail **Administration** , cliquez sur **Forêts Active Directory**. Si la découverte de forêts Active Directory a été exécutée précédemment, vous pouvez voir chaque forêt découverte dans le volet des résultats. La forêt locale et toutes les forêts approuvées sont découvertes lorsque la Découverte de forêts Active Directory s'exécute. Seules les forêts non approuvées doivent être ajoutées manuellement.  

    -   Pour configurer une forêt ayant déjà été découverte, sélectionnez la forêt dans le volet des résultats, puis dans l'onglet **Accueil** , dans le groupe **Propriétés** , cliquez sur **Propriétés** pour ouvrir les propriétés de la forêt. Passez à l'étape 3.  

    -   Pour configurer une nouvelle forêt qui n'est pas répertoriée, dans l'onglet **Accueil** , dans le groupe **Créer** , cliquez sur **Ajouter une forêt** pour ouvrir la boîte de dialogue **Ajouter une forêt** . Passez à l'étape 3.  

3.  Dans l'onglet **Général** , remplissez les configurations pour la forêt que vous souhaitez découvrir et spécifiez le **Compte de forêt Active Directory**.  

    > [!NOTE]  
    >  La découverte de forêts Active Directory requiert un compte global pour découvrir et publier les forêts non approuvées. Si vous n'utilisez pas le compte d'ordinateur du serveur du site, vous pouvez uniquement sélectionner un compte global.  

4.  Si vous prévoyez d'autoriser des sites à publier des données de site pour cette forêt, dans l'onglet **Publication** , remplissez la configuration de la publication de cette forêt.  

    > [!NOTE]  
    >  Si vous autorisez des sites à publier vers une forêt, vous devez étendre le schéma Active Directory pour cette forêt pour Configuration Manager et le compte de forêt Active Directory doit disposer d'autorisations Contrôle intégral dans le conteneur système de cette forêt.  

5.  Lorsque vous terminez la configuration de cette forêt pour une utilisation avec la Découverte de forêts Active Directory, cliquez sur **OK** pour enregistrer la configuration.  



<!--HONumber=Nov16_HO1-->


