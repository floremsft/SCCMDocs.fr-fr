---
title: "Lier des utilisateurs et des appareils avec l’affinité entre utilisateur et appareil | System Center Configuration Manager"
description: "Lier des utilisateurs et des appareils avec l’affinité entre utilisateur et appareil et déployez automatiquement des applications sur tous les appareils associés à un utilisateur."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5b30b0d5-722d-4d4b-9ed7-5a43de315461
caps.latest.revision: 7
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: bb918eb5f7a69cad47de761a3e95e92926524e3a


---
# <a name="link-users-and-devices-with-user-device-affinity-in-system-center-configuration-manager"></a>Lier des utilisateurs et des appareils avec l’affinité entre utilisateur et appareil dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

L’affinité entre utilisateur et appareil dans System Center Configuration Manager associe un utilisateur à un ou plusieurs appareils. Vous n’avez alors pas besoin de connaître les noms des appareils d’un utilisateur pour déployer une application auprès de cet utilisateur. Au lieu de déployer l’application sur chacun des appareils de l’utilisateur, vous déployez l’application auprès de l’utilisateur. Ensuite, l’affinité entre utilisateur et appareil entraîne l’installation automatique de l’application sur tous les appareils associés à cet utilisateur.  

 Vous pouvez définir des appareils principaux, qui sont généralement les appareils utilisés quotidiennement par les utilisateurs pour effectuer leur travail. Quand vous créez une affinité entre un utilisateur et un appareil, vous profitez d’un plus grand nombre d’options de déploiement d’applications. Par exemple, si un utilisateur requiert Microsoft Office Visio, vous pouvez l'installer sur l'appareil principal de l'utilisateur à l'aide d'un déploiement Windows Installer. Toutefois, sur un appareil qui n'est pas un appareil principal, vous pouvez déployer Microsoft Office Visio sous forme d'application virtuelle. Vous pouvez également utiliser l’affinité entre utilisateur et appareil pour prédéployer des logiciels sur l’appareil d’un utilisateur quand celui-ci n’est pas connecté pour que, dès que l’utilisateur se connecte, l’application soit déjà installée et prête à être utilisée.  

 Vous devez gérer les informations d'affinité entre appareil et utilisateur pour les ordinateurs. Les affinités entre appareil et utilisateur sont gérées automatiquement par Configuration Manager, pour les appareils mobiles inscrits.  

## <a name="manually-configure-user-device-affinity"></a>Configurer manuellement l’affinité entre utilisateur et appareil  

1.  Dans la console Configuration Manager, cliquez sur **Ressources et Conformité** > **Périphériques**.  

3.  Sélectionnez un appareil dans la liste. Sous l'onglet **Accueil** , dans le groupe **Appareil** , cliquez sur **Modifier les utilisateurs principaux**.  

4.  Dans la boîte de dialogue **Modifier les utilisateurs principaux** , recherchez et sélectionnez les utilisateurs que vous souhaitez ajouter en tant qu'utilisateurs principaux pour l'appareil sélectionné, puis cliquez sur **Ajouter**.  

    > [!NOTE]  
    >  La liste **Utilisateurs principaux** indique quels utilisateurs sont déjà les utilisateurs principaux de cet appareil, ainsi que la méthode par laquelle la relation entre utilisateur et appareil a été attribuée.  

## <a name="configure-primary-devices-for-a-user"></a>Configurer les appareils principaux pour un utilisateur  

1.  Dans la console Configuration Manager, cliquez sur **Ressources et Conformité** > **Utilisateurs**.  

3.  Sélectionnez un utilisateur dans la liste. Puis, sous l'onglet **Appareil** , cliquez sur **Modifier les appareils principaux**.  

4.  Dans la boîte de dialogue **Modifier les appareils principaux** , recherchez et sélectionnez les appareils que vous souhaitez ajouter en tant qu'appareils principaux pour l'utilisateur sélectionné, puis cliquez sur **Ajouter**.  

    > [!NOTE]  
    >  La liste **Appareils principaux** indique quels appareils sont déjà configurés en tant qu'appareils principaux pour cet utilisateur, ainsi que la méthode par laquelle la relation entre utilisateur et appareil a été attribuée.  

## <a name="automatically-create-user-device-affinities-windows-pcs-only"></a>Créer automatiquement des affinités entre utilisateur et appareil (ordinateurs Windows uniquement)  
 Configuration Manager lit les données sur les ouvertures de session des utilisateurs dans le journal des événements Windows. Pour pouvoir créer automatiquement des affinités entre des utilisateurs et des appareils, vous devez activer les deux paramètres suivants dans la stratégie de sécurité locale des ordinateurs clients, afin de stocker les événements d'ouverture de session dans le journal des événements.  

-   **Auditer les événements d'ouverture de session de compte**  

-   **Auditer les événements d'ouverture de session**  

 Vous pouvez utiliser la stratégie de groupe Windows pour configurer ces paramètres.  

> [!IMPORTANT]  
>  Si une erreur provoque l'ajout d'un nombre important d'entrées au journal des événements Windows, il se peut qu'un nouveau journal des événements soit créé. Dans ce cas, Configuration Manager risque de ne plus pouvoir accéder aux événements d'ouverture de session existants.  
>   
>  Soyez prudent lors de la mise en œuvre des actions **Auditer les événements de connexion aux comptes** et **Auditer les événements de connexion** dans Windows XP. Par défaut, la stratégie de rétention est de 7 jours et il est très probable que ces événements remplissent le journal des événements de sécurité. Les utilisateurs standard ne pourront pas se connecter si le journal des événements est plein. Pour éviter ce problème, définissez également la stratégie **Méthode de conservation** pour le journal de sécurité afin de **Remplacer les événements si nécessaire**. Pour autoriser des données suffisantes pour l'affinité entre utilisateur et appareil, définissez également la stratégie Taille maximale du journal de sécurité sur une valeur raisonnable, par exemple 5 à 20 Mo.  

### <a name="configure-the-site-to-automatically-create-user-device-affinities"></a>Configurer le site pour créer automatiquement des affinités entre utilisateur et appareil  

1.  Dans la console Configuration Manager, cliquez sur **Administration** > **Paramètres client**.  

3.  Pour modifier les paramètres client par défaut, sélectionnez **Paramètres client par défaut**, puis dans l'onglet **Accueil** , dans le groupe **Propriétés** , cliquez sur **Propriétés**. Pour créer des paramètres d'agent client personnalisés, sélectionnez le nœud **Paramètres client** , puis dans l'onglet **Accueil** , dans le groupe **Créer** , cliquez sur **Créer des paramètres d'appareil client personnalisés**.  

    > [!NOTE]  
    >  Si vous modifiez les paramètres client par défaut, ils seront déployés sur tous les ordinateurs de la hiérarchie. Pour plus d'informations sur la configuration des paramètres client, voir [Guide pratique pour configurer les paramètres client dans System Center Configuration Manager](../../core/clients/deploy/configure-client-settings.md).  

4.  Configurez les options suivantes pour le paramètre client **Affinité entre utilisateur et appareil**:  

    -   **Seuil de l'affinité entre utilisateur et appareil (minutes)** - Spécifiez le nombre de minutes d'utilisation avant la création d'une affinité entre utilisateur et appareil.  

    -   **Seuil de l’affinité entre utilisateur et périphérique (jours)** : spécifiez le nombre de jours pendant lesquels le seuil d’affinité basé sur l’utilisation est mesuré.  

    -   **Configurer automatiquement l'affinité entre utilisateur et appareil à partir des données d'utilisation** – Dans la liste déroulante, sélectionnez **Vrai** pour autoriser le site à créer automatiquement des affinités entre utilisateur et appareil. Si vous sélectionnez **Faux**, vous devez approuver toutes les attributions d’affinité entre utilisateur et périphérique.  

    > [!TIP]  
    >  **Exemple** : si le **Seuil de l’affinité entre utilisateur et périphérique (minutes)** est défini sur **60** minutes et que le **Seuil de l’affinité entre utilisateur et périphérique (jours)** est défini sur **5** jours, l’utilisateur doit utiliser l’appareil pendant au moins 60 minutes sur une période de 5 jours pour qu’une affinité entre utilisateur et périphérique puisse être automatiquement créée.  
   
Après la création automatique d'une affinité entre utilisateur et appareil, Configuration Manager continue de surveiller les seuils d'affinité entre utilisateur et appareil. Si l'activité de l'utilisateur pour cet appareil devient inférieure aux seuils configurés, l'affinité entre utilisateur et appareil sera supprimée. Configurez la valeur du **Seuil de l'affinité entre utilisateur et appareil (jours)** à au moins **7** jours pour éviter la suppression d'une affinité entre utilisateur et appareil automatiquement configurée lorsque l'utilisateur n'est pas connecté, par exemple pendant le week-end.  

## <a name="import-user-device-affinities-from-a-file"></a>Importer des affinités entre utilisateur et périphérique à partir d’un fichier  
 Pour créer plusieurs relations simultanément, vous pouvez importer un fichier contenant des affinités entre des utilisateurs et des appareils. Pour que cette procédure fonctionne, les appareils concernés doivent avoir été découverts et doivent faire partie des ressources de la base de données Configuration Manager.  

1.  Dans la console Configuration Manager, cliquez sur **Ressources et Conformité** > **Utilisateurs** ou **Périphériques**.  

3.  Dans l'onglet **Accueil** , dans le groupe **Créer** , cliquez sur **Importer une affinité entre utilisateur et appareil**.  

4.  Sur la page **Choisir un mappage** de l' **Assistant Importation d'affinités entre utilisateur et appareil**, spécifiez les informations suivantes :  

    -   **Nom du fichier** : spécifiez un fichier de valeurs séparées par des virgules (.csv) contenant une liste d'utilisateurs et d'appareils entre lesquels vous souhaitez créer des affinités. Dans ce fichier, chaque paire utilisateur-appareil doit se trouver sur une ligne distincte, une virgule séparant l'utilisateur et l'appareil. Utilisez le format *<Domaine>\>\\<nom_utilisateur>\>*,*<nom_NetBIOS_appareil\>*.  

    -   **Ce fichier contient des en-têtes de colonnes à titre de référence** : si le fichier de valeurs séparées par des virgules commence par une ligne d'en-tête, sélectionnez cette option pour ignorer cette ligne lors de l'importation.  

5.  Si le fichier que vous importez comporte plus de deux éléments sur chaque ligne, vous pouvez utiliser les commandes **Colonne** et **Attribuer** pour indiquer quelles colonnes représentent les utilisateurs et les appareils et quelles colonnes doivent être ignorées lors de l'importation.  

6.  Cliquez sur **Suivant** et terminez l' **Assistant Importation d'affinités entre utilisateur et appareil**.  

## <a name="let-end-users-create-a-user-device-affinity"></a>Laisser les utilisateurs finaux créer une affinité entre utilisateur et appareil  
 Utilisez ces procédures pour permettre aux utilisateurs de créer leur propre affinité entre utilisateur et périphérique depuis le Centre logiciel.  

### <a name="configure-the-site-to-allow-user-created-user-device-affinity-requests"></a>Configurer le site de façon à permettre aux utilisateurs de créer des demandes d’affinité entre utilisateur et appareil  

1.  Dans la console Configuration Manager, cliquez sur **Administration** > **Paramètres client**.  

3.  Pour modifier les paramètres client par défaut, sélectionnez **Paramètres client par défaut**, puis dans l'onglet **Accueil** , dans le groupe **Propriétés** , cliquez sur **Propriétés**. Pour créer des paramètres d'agent client personnalisés, sélectionnez le nœud **Paramètres client** , puis dans l'onglet **Accueil** , dans le groupe **Créer** , cliquez sur **Créer des paramètres utilisateur client personnalisés**.  

    > [!NOTE]  
    >  Si vous modifiez les paramètres client par défaut, ils seront déployés sur tous les ordinateurs de la hiérarchie. Pour plus d’informations sur la configuration des paramètres client, voir [Configurer les paramètres client](../../core/clients/deploy/configure-client-settings.md).  

4.  Sélectionnez le paramètre client **Affinité entre utilisateur et périphérique** puis, dans la liste déroulante **Autoriser les utilisateurs à définir leurs périphériques principaux** , sélectionnez **Vrai**.  

### <a name="configure-a-user-device-affinity"></a>Configurer une affinité entre utilisateur et appareil  

1.  Dans le catalogue d’applications, cliquez sur **Mes systèmes**.  

2.  Activez l'option **J'utilise régulièrement cet ordinateur pour faire mon travail**.  

## <a name="manage-user-device-affinity-requests-from-users"></a>Gérer les demandes d’affinité entre utilisateur et périphérique faites par les utilisateurs  
 Quand le paramètre client **Configurer automatiquement l’affinité entre utilisateur et périphérique à partir des données d’utilisation** est défini sur **Faux**, vous devez approuver toutes les attributions d’affinité entre utilisateur et périphérique.  

### <a name="approve-or-reject-a-user-device-affinity-request"></a>Pour approuver ou refuser une demande d’affinité entre utilisateur et appareil  

1.  Dans la console Configuration Manager, cliquez sur **Ressources et Conformité**.  

2.  Dans l'espace de travail **Ressources et Conformité** , sélectionnez le regroupement d'utilisateurs ou d'appareils dont vous souhaitez gérer les demandes d'affinité.  

3.  Dans l'onglet **Accueil** , dans le groupe **Regroupement** , cliquez sur **Gérer les demandes d'affinité**.  

4.  Dans la boîte de dialogue **Gérer les demandes d’affinité entre périphérique et utilisateur** , sélectionnez une demande d’affinité, puis cliquez sur **Approuver** ou **Refuser**.  



<!--HONumber=Nov16_HO1-->


