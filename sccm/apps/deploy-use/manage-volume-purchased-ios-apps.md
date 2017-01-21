---
title: "Gérer des applications iOS achetées en volume | System Center Configuration Manager"
description: "Déployez, gérez et suivez les licences d’applications que vous avez achetées via l’App Store iOS."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b5e7cead-e257-405b-a2aa-b0130e48dc40
caps.latest.revision: 23
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 4289f4853f77392df420e44e179961609f83683f


---
# <a name="manage-volume-purchased-ios-apps-with-system-center-configuration-manager"></a>Gérer des applications iOS achetées en volume avec System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*



 L’App Store iOS vous permet d’acheter plusieurs licences d’une application que vous souhaitez utiliser dans votre entreprise. Vous pouvez ainsi réduire les coûts d’administration liés au suivi de plusieurs copies d’application achetées.  

 System Center Configuration Manager facilite le déploiement et la gestion des applications iOS que vous avez achetées via le programme en important les informations de licence depuis l’App Store et en effectuant le suivi du nombre de licences que vous avez utilisées.  

## <a name="manage-volume-purchased-apps-for-ios-devices"></a>Gérer les applications pour appareils iOS achetées en volume  
 Vous pouvez acheter plusieurs licences pour des applications iOS via le Programme d’achat en volume (VPP) Apple. Cela implique de configurer un compte Apple VPP sur le site web Apple et de charger le jeton Apple VPP sur Configuration Manager, qui offre les possibilités suivantes :  

-   synchronisation des informations sur les achats en volume avec Configuration Manager ;  

-   affichage des applications achetées dans la console Configuration Manager ;  

-   déploiement et surveillance de ces applications et suivi du nombre de licences utilisés pour chaque application ;  

-   quand cela s’avère nécessaire, récupération de licences en désinstallant les applications achetées en volume qui ont été déployées pour les utilisateurs.  

## <a name="before-you-start"></a>Avant de commencer  
 Avant de commencer, vous devez vous procurer un jeton VPP auprès d’Apple et le charger sur Configuration Manager.  

> [!IMPORTANT]  
>  -   À l’heure actuelle, chaque organisation ne peut avoir qu’un seul compte et jeton VPP.  
> -   Seul le Programme d’achat en volume Apple pour les entreprises est pris en charge.  
> -   Une fois que vous associez un compte Apple VPP à Intune, vous ne pouvez pas associer un autre compte. C’est la raison pour laquelle il est très important que plusieurs personnes possèdent les détails du compte que vous utilisez.  
> -   Si vous avez précédemment utilisé un jeton VPP avec un autre produit MDM dans votre compte Apple VPP existant, vous devez en générer un nouveau pour l’utiliser avec Configuration Manager.  
> -   Chaque jeton est valide pendant un an.  
> -   Par défaut, Configuration Manager se synchronise avec le service Apple VPP deux fois par jour pour vérifier que vos licences sont synchronisées avec Configuration Manager.  
>   
>      Seules les modifications apportées à vos licences sont synchronisées. Cependant, une synchronisation complète est assurée une fois tous les 7 jours.  
>   
>      Quand vous cliquez sur **Synchroniser** pour effectuer une synchronisation manuelle, celle-ci est toujours complète.  
> -   Si vous avez besoin de récupérer ou restaurer votre base de données Configuration Manager, nous vous recommandons d’effectuer une synchronisation manuelle après cette opération pour être certain que vos données de licence synchronisées sont à jour.  
> -   Même si vous pouvez déployer des applications iOS achetées en volume sur des regroupements d’utilisateurs ou d’appareils, les applications VPP que vous déployez sur un appareil sans utilisateur (par exemple, un appareil que vous avez inscrit sans affinité utilisateur via le Programme d’inscription des appareils (DEP) ou Apple Configurator) ne sont pas installées.  

 De plus, vous devez avoir importé un certificat du service de notifications Push Apple (APNs) pour pouvoir gérer des appareils iOS, ce qui inclut le déploiement d’applications. Pour plus d’informations, consultez [Configurer la gestion des appareils iOS hybride](../../mdm/deploy-use/set-up-ios-hybrid-device-management.md).  

## <a name="step-1---to-get-and-upload-an-apple-vpp-token"></a>Étape 1 : obtenir et charger un jeton Apple VPP  
  
1.  Dans la console Configuration Manager, cliquez sur **Administration** > **Services cloud** > **Jetons du programme d’achat en volume (VPP) Apple**.   
  
3.  Sous l’onglet **Accueil**, dans le groupe **Jetons du programme d’achat en volume (VPP) Apple**, cliquez sur **Ajouter un jeton du programme d’achat en volume (VPP) Apple**.  

4.  Dans la page **Général** de l’Assistant **Ajouter un jeton du programme d’achat en volume (VPP) Apple**, configurez les éléments suivants :   

    -   **Nom** : attribuez un nom à ce jeton tel qu’il s’affichera dans la console Configuration Manager.  

    -   **Jeton** : cliquez sur **Parcourir** et sélectionnez le jeton VPP que vous avez téléchargé sur le site web Apple.  

         Cliquez sur le lien **See Apple VPP account** (Voir le compte VPP Apple) et, si ce n’est déjà fait, souscrivez à un programme d’achats en volume pour les entreprises ou l’enseignement. Une fois inscrit, téléchargez le jeton Apple VPP pour votre compte.  

    -   **Description** : si vous le souhaitez, entrez une description pour faciliter l’identification du jeton VPP dans la console Configuration Manager.  

    -   **Catégories attribuées pour améliorer la recherche et le filtrage** : si vous le souhaitez, vous pouvez attribuer des catégories au jeton VPP pour faciliter sa recherche dans la console Configuration Manager.  

5.  Cliquez sur **Suivant**, puis complétez l’Assistant.  
  
À partir du nœud **Jetons du programme d’achat en volume (VPP) Apple**, vous pouvez maintenant consulter les informations sur le jeton Apple VPP et déterminer notamment quand ont eu lieu ses dernières mise à jour et synchronisation, ainsi que sa date d’expiration. 
  
Vous pouvez à tout moment synchroniser entièrement les données détenues par Apple à l’aide de Configuration Manager en cliquant sur **Synchroniser** sous l’onglet **Accueil**, dans le groupe **Synchroniser**.  
  
## <a name="step-2---deploy-a-volume-purchased-app"></a>Étape 2 : déployer une application achetée en volume  

1.  Dans la console Configuration Manager, cliquez sur **Bibliothèque de logiciels** > **Gestion des applications** > **Informations de licence pour les applications du Store**.  

3.  Choisissez l’application que vous voulez déployez puis, sous l’onglet **Accueil**, dans le groupe **Créer**, cliquez sur **Créer une application**.
Une application Configuration Manager contenant l’application du Windows Store pour Entreprises est alors créée. Vous pouvez ensuite déployer et surveiller cette application comme n’importe quelle autre application Configuration Manager.

    > [!IMPORTANT]  
    > Vous devez choisir l’objectif de déploiement **Obligatoire**. Les installations disponibles ne sont pas prises en charge actuellement.

 Quand vous déployez l’application, une licence est utilisée par chaque utilisateur qui installe l’application.  

 Pour récupérer une licence, remplacez l’action de déploiement par **Désinstaller**. La licence est récupérée une fois l’application désinstallée.  

## <a name="step-3---monitor-ios-vpp-apps"></a>Étape 3 : surveiller les applications VPP iOS  
 Le nœud **Informations de licence pour les applications du Store** de l’espace de travail **Bibliothèque de logiciels** affiche des informations sur vos applications iOS achetées en volume, notamment le nombre total de licences qui vous appartiennent et celles qui ont été déployés.

 Vous pouvez aussi surveiller l’utilisation des licences de toutes les applications VPP que vous avez achetées à l’aide du rapport **Applications du programme d’achat en volume (VPP) Apple pour iOS avec les nombres de licences**.  

 Ce rapport affiche le nom de chaque application, ainsi que le nombre total de licences achetées, le nombre de licences disponibles et d’autres informations.  

 Pour obtenir de l’aide sur l’exécution des rapports Configuration Manager, consultez [Génération de rapports dans System Center Configuration Manager](../../core/servers/manage/reporting.md).  



<!--HONumber=Nov16_HO1-->


