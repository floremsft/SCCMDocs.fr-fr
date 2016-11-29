---
title: "Surveiller des applications à partir de la console System Center Configuration Manager | System Center Configuration Manager"
description: "Surveillez le déploiement de logiciels, notamment des mises à jour, des paramètres de compatibilité et des applications à l’aide de l’espace de travail Surveillance dans Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 784c295c-b8b8-4202-ab9f-665908d49d6d
caps.latest.revision: 5
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: ca82638267d6d9e1bb4eb6855785ac383a2191e9


---
# <a name="monitor-applications-from-the-system-center-configuration-manager-console"></a>Surveiller des applications à partir de la console System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*


## <a name="introduction"></a>Introduction

System Center Configuration Manager permet de surveiller le déploiement de tous les logiciels : mises à jour logicielles, paramètres de compatibilité, applications, séquences de tâches, packages, programmes, etc. Vous pouvez surveiller les déploiements à l’aide de l’espace de travail **Surveillance** de la console Configuration Manager ou par le biais de rapports.  

 Les applications de Configuration Manager prennent en charge la surveillance basée sur l’état, laquelle vous permet de suivre le dernier état du déploiement des applications pour les utilisateurs et les appareils. Ces messages d'état affichent des informations concernant des périphériques individuels. Par exemple, si une application est déployée sur un regroupement d’utilisateurs, vous pouvez voir l’état de compatibilité du déploiement ainsi que son objet dans la console Configuration Manager.  

 L'état d'un déploiement d'application peut disposer de l'un des états de compatibilité suivants :  

-   **Opération réussie** : le déploiement d'application a réussi ou était déjà installé.  

-   **En cours** : le déploiement d'application est en cours.  

-   **Inconnu** : l'état du déploiement d'application n'a pas pu être déterminé. Cet état ne concerne pas les déploiements dont l'objet est **Disponible**. Cet état s'affiche généralement lorsque les messages d'état émanant du client n'ont pas encore été reçus.  

-   **Config non satisfaite** : l'application n'a pas été déployée, car elle n'était pas conforme à une dépendance ou à une règle de spécification, ou car le système d'exploitation sur lequel elle a été déployée n'était pas concerné.  

-   **Erreur** : le déploiement d'application a échoué à cause d'une erreur.  
  
Vous pouvez consulter des informations supplémentaires pour chaque état de compatibilité, ce qui inclut des sous-catégories de l'état de compatibilité et le nombre d'utilisateurs et de périphériques de cette catégorie. Par exemple, l'état de compatibilité **Erreur** comprend les sous-catégories suivantes :  
  
-   Erreur lors de l'évaluation de la configuration requise  

-   Erreurs liées au contenu  

-   Erreurs d'installation  

 Lorsque plusieurs états de compatibilité s'appliquent à un déploiement d'application, vous pouvez consulter l'état de l'agrégat dont la compatibilité est la plus faible. Exemple :  

-   Si un utilisateur se connecte sur deux périphériques et que l'installation de l'application réussit sur un périphérique, mais échoue sur le deuxième, l'état du déploiement de l'agrégat de l'application pour cet utilisateur a l'état **Erreur**.  

-   Si une application est déployée auprès de tous les utilisateurs ouvrant des sessions sur un ordinateur donné, vous recevez plusieurs résultats de déploiement pour cet ordinateur. Si l'un des déploiements échoue, l'état du déploiement de l'agrégat pour l'ordinateur est **Erreur**.  
  
L'état du déploiement des packages et des programmes n'est pas agrégé.  
  
 Utilisez ces sous-catégories pour vous aider à identifier rapidement tous les problèmes importants d'un déploiement d'application. Vous pouvez aussi consulter des informations complémentaires sur les périphériques qui entrent dans une sous-catégorie d'un état de compatibilité.  

 Dans Configuration Manager, la gestion des applications inclut plusieurs rapports prédéfinis qui vous permettent de surveiller des informations concernant les applications et les déploiements. Ces rapports affichent la catégorie de rapport **Distribution de logiciels – Surveillance des applications**.  

 Pour plus d’informations sur la configuration de la création de rapports dans Configuration Manager, consultez [Création de rapports dans System Center Configuration Manager](../../core/servers/manage/reporting.md).  
  
## <a name="monitor-the-state-of-an-application-in-the-configuration-manager-console"></a>Surveiller l’état d’une application dans la console Configuration Manager  
  
1.  Dans la console Configuration Manager, cliquez sur **Surveillance** > **Déploiements**.  
  
3.  Pour consulter les détails du déploiement pour chaque état de compatibilité et pour les périphériques dans cet état, sélectionnez un déploiement puis, dans l'onglet **Accueil** , dans le groupe **Déploiement** , cliquez sur **Afficher l'état** pour ouvrir le volet **État du déploiement** . Dans ce volet, vous pouvez consulter les biens de chaque état de compatibilité. Cliquez sur un bien pour obtenir des informations plus détaillées sur son état de déploiement.  

    > [!NOTE]  
    >  Le nombre d'éléments pouvant être affichés dans le volet **État du déploiement** est limité à 20 000. Si vous avez besoin de voir plus d’éléments, utilisez les rapports Configuration Manager pour afficher les données d’état.  
    >   
    >  L'état des types de déploiement est agrégé dans le volet **État du déploiement** . Pour voir des informations plus détaillées sur les types de déploiement, utilisez le rapport **Erreurs d'infrastructure de l'application** appartenant à la catégorie de rapports **Distribution de logiciels - Surveillance des applications**.  

4.  Pour consulter des informations d'état général d'un déploiement d'application, sélectionnez un déploiement, puis cliquez sur l'onglet **Résumé** de la fenêtre **Déploiement sélectionné** .  

5.  Pour consulter des informations sur le type de déploiement d'applications, sélectionnez un déploiement puis cliquez sur l'onglet **Type de déploiement** de la fenêtre **Déploiement sélectionné** .  

Les informations affichées dans le volet **État du déploiement**, après avoir cliqué sur **Afficher l’état**, sont des données transmises en temps réel depuis la base de données Configuration Manager. Les informations affichées dans les onglets **Résumé** et **Types de déploiement** sont des données résumées. Si les données affichées dans les onglets **Résumé** et **Types de déploiement** ne correspondent pas à celles affichées dans le volet **État du déploiement** , cliquez sur **Exécuter le résumé** pour mettre à jour les données figurant dans ces onglets. Vous pouvez configurer la fréquence par défaut de la synthèse du déploiement d'applications en suivant cette procédure :  
1. Dans la console Configuration Manager, cliquez sur **Administration** > **Configuration du site** > **Sites**.
2. Dans la liste **Sites** , sélectionnez le site dont vous souhaitez configurer l'intervalle de résumé, puis sous l'onglet **Accueil** , dans le groupe **Paramètres** , cliquez sur **Outils de synthèse d'état**.
3. Dans la boîte de dialogue **Outils de synthèse d'état** , cliquez sur **Outils de synthèse du déploiement d'application**, puis sur **Modifier**.  
4. Dans la boîte de dialogue **Propriétés des outils de synthèse du déploiement d'application** , configurez la fréquence de la synthèse, puis cliquez sur **OK**.  



<!--HONumber=Nov16_HO1-->


