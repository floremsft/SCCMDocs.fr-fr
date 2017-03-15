---
title: "Créer des applications | Microsoft Docs"
description: "Créez et déployez des applications et des types de déploiement avec System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: cc230ff4-7056-4339-a0a6-6a44cdbb2857
caps.latest.revision: 14
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: f9097014c7e988ec8e139e518355c4efb19172b3
ms.openlocfilehash: da86fc2f61ce8229fb0d3f58a4f8a24d1514b30e
ms.lasthandoff: 03/04/2017


---
# <a name="create-applications-with-system-center-configuration-manager"></a>Créer des applications avec System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Une application System Center Configuration Manager dispose des fichiers et informations nécessaires pour déployer des logiciels sur un appareil. Une application a un ou plusieurs types de déploiement qui comprennent les informations et fichiers d’installation nécessaires pour installer le logiciel. Le type de déploiement contient également des règles spécifiant à quel moment et selon quelle méthode le logiciel est déployé.  

 Vous pouvez créer des applications à l'aide des méthodes suivantes :  

-   Créer automatiquement les types d'application et de déploiement en lisant les fichiers d'installation de l'application.  

-   Créer manuellement l'application, puis ajouter des types de déploiement ultérieurement.  

-   Importer une application à partir d’un fichier.  

> [!NOTE]  
> La section  [Créer des applications iOS avec System Center Configuration Manager](../../mdm/deploy-use/create-applications.md) fournit des informations détaillées sur la création d’applications iOS, Windows Phone et Android.  

Procédez comme suit pour créer des applications et des types de déploiement Configuration Manager.  

## <a name="start-the-create-application-wizard"></a>Démarrer l’Assistant Création d’une application  

1.  Dans la console Configuration Manager, choisissez **Bibliothèque de logiciels** > **Gestion des applications** > **Applications**.  

3.  Sous l’onglet **Accueil**, dans le groupe **Créer**, choisissez **Créer une application**.  

## <a name="specify-whether-you-want-to-automatically-detect-application-information-or-manually-define-the-information"></a>Spécifier si vous souhaitez détecter automatiquement les informations de l'application ou définir manuellement les informations  

-   Utilisez la procédure de détection automatique des informations de l’application pour créer une application simple avec un type de déploiement unique, comme un fichier Windows Installer sans dépendances ni spécifications. Après avoir créé une application à l'aide de cette procédure, vous pouvez la modifier pour ajouter ou changer les types de déploiement et ajouter des méthodes de détection, des dépendances ou des spécifications.  

-   Utilisez la procédure de définition manuelle des informations de l’application pour créer des applications plus complexes associant plusieurs types de déploiement, dépendances, méthodes de détection et spécifications.  

### <a name="automatically-detect-application-information"></a>Détecter automatiquement les informations sur l’application  

1.  Dans la page **Général,** de l’Assistant Création d’une application, sélectionnez **Détecter automatiquement les informations de cette application à partir des fichiers d’installation**.  

2.  Dans la liste déroulante **Type** , choisissez le type de fichier d'installation d'application que vous souhaitez utiliser pour détecter les informations sur l'application. Pour plus d’informations sur les types d’installation disponibles, consultez [Types de déploiement pris en charge par Configuration Manager](/sccm/apps/deploy-use/create-applications#deployment-types-supported-by-configuration-manager) dans cette rubrique.  

3.  Dans la zone **Emplacement**, spécifiez le chemin UNC (au format *\\\\serveur\\partage\\\nom_fichier*) ou le lien du magasin du fichier d’installation d’application à utiliser pour détecter les informations sur l’application. Vous pouvez également cliquer sur **Parcourir** pour accéder au fichier d’installation.  

    > [!IMPORTANT]  
    >  Quand vous sélectionnez **Windows Installer (fichier \*.msi)** comme type d’application, tous les fichiers dans le dossier spécifié sont importés avec l’application et envoyés aux points de distribution. Vérifiez que le dossier spécifié contient uniquement les fichiers nécessaires à l’installation de l’application. Configuration Manager est testé pour prendre en charge jusqu’à 20 000 fichiers d’application dans le package d’application. Si votre application contient plus de fichiers, pensez à créer plusieurs applications avec moins de fichiers.  

    >  Vous devez avoir accès au chemin UNC qui contient l’application et à tous les sous-dossiers intégrant le contenu de l’application.  

4.  Dans la page **Importer des informations** de l’Assistant Création d’une application, consultez les informations qui ont été importées, puis choisissez **Suivant**. Si nécessaire, vous pouvez choisir **Précédent** pour revenir en arrière et corriger les erreurs éventuelles.  

5.  Dans la page **Informations générales** de l’Assistant Création d’une application, spécifiez les informations suivantes :  

    > [!NOTE]  
    >  Certaines de ces informations peuvent être déjà renseignées, si elles ont été obtenues automatiquement auprès des fichiers d'installation de l'application. En outre, les options affichées peuvent être différentes en fonction du type d'application que vous créez.  

    -   Informations générales relatives à l’application : nom, commentaires, version et éventuellement une référence qui vous aidera à référencer l’application dans la console Configuration Manager.  

    -   **Programme d’installation** : spécifiez le programme d’installation et les propriétés requises pour installer le type de déploiement d’application.  

        > [!TIP]  
        >  Si le programme d’installation n’est pas indiqué, choisissez **Parcourir** pour accéder à l’emplacement du programme d’installation.  

    -   **Comportement à l’installation** : indiquez si le type de déploiement d’application doit être installé uniquement pour l’utilisateur actuellement connecté ou pour tous les utilisateurs. Vous pouvez également indiquer si vous souhaitez que le type de déploiement soit installé pour l’ensemble des utilisateurs en cas de déploiement sur un appareil ou uniquement pour un utilisateur spécifique en cas de déploiement auprès d’un utilisateur.  

    -   **Utiliser une connexion VPN automatique (si elle est configurée)** : si un profil VPN a été déployé sur l’appareil où l’application est exécutée, lancez la connexion VPN au démarrage de l’application (Windows 8.1 et Windows Phone 8.1 uniquement).  

         Sur les appareils Windows Phone 8.1, les connexions VPN automatiques ne sont pas prises en charge si plusieurs profils VPN ont été déployés sur l'appareil.  

         Pour plus d’informations sur les profils VPN, consultez [Profils VPN](../../protect/deploy-use/vpn-profiles.md).  

6.  Choisissez **Suivant**, examinez les informations sur l’application figurant dans la page **Résumé**, puis suivez toutes les étapes de l’Assistant Création d’une application.  

La nouvelle application s’affiche dans le nœud **Applications** de la console Configuration Manager, ce qui marque la fin de la création d’une application. Si vous voulez ajouter d’autres types de déploiement à l’application, consultez [Créer des types de déploiement pour l’application](/sccm/apps/deploy-use/create-applications#create-deployment-types-for-the-application) dans cette rubrique.  

### <a name="manually-specify-application-information"></a>Définir manuellement les informations de l’application  

1.  Dans la page **Général** de l’Assistant Création d’une application, sélectionnez **Spécifier manuellement les informations de l’application**, puis choisissez **Suivant**.  

2.  Spécifiez des informations générales relatives à l’application : nom, commentaires, version et éventuellement une référence qui vous aidera à référencer l’application dans la console Configuration Manager.  

3.  Dans la page **Catalogue d’applications** de l’Assistant Création d’une application, spécifiez les informations suivantes :  

    -   **Langue sélectionnée** : dans la liste déroulante, sélectionnez la version de langue de l’application que vous souhaitez configurer. Choisissez **Ajouter/Supprimer** pour configurer d’autres langues pour cette application.  

    -   **Nom de l’application localisée** : indiquez le nom de l’application dans la langue sélectionnée dans la liste déroulante **Langue sélectionnée**.  

        > [!IMPORTANT]  
        >  Vous devez spécifier un nom d’application localisée pour chaque version de langue que vous configurez.  

    -   **Catégories d’utilisateurs** : choisissez **Modifier** pour spécifier les catégories de l’application, dans la langue sélectionnée dans la liste déroulante **Langue sélectionnée**. Les utilisateurs du Centre logiciel peuvent utiliser les catégories sélectionnées pour filtrer et trier les applications disponibles.  

    -   **Documentation utilisateur** : choisissez **Parcourir** pour spécifier l’URL ou le chemin UNC et le nom d’un fichier que les utilisateurs du Centre logiciel peuvent lire pour obtenir des informations supplémentaires sur cette application.  

    -   **Texte de lien** : spécifiez le texte qui sera affiché à la place de l’URL de l’application.  

    -   **URL de la déclaration de confidentialité de l’application** : spécifiez une URL qui accède à la déclaration de confidentialité de l’application.  

    -   **Description localisée** : entrez une description de l’application dans la langue que vous avez sélectionnée dans la liste déroulante **Langue sélectionnée**.  

    -   **Mots-clés** : entrez une liste de mots-clés dans la langue que vous avez sélectionnée dans la liste déroulante **Langue sélectionnée**. Ils permettront aux utilisateurs du Centre logiciel de rechercher l’application.  

    -   **Icône** : choisissez **Parcourir** pour sélectionner une icône pour cette application parmi les icônes disponibles. Si vous ne spécifiez pas d'icône, une icône par défaut sera utilisée pour cette application.  

    -   **Afficher en tant qu’application proposée et la mettre en exergue sur le portail de l’entreprise** : sélectionnez cette option pour afficher l’application de façon visible sur le portail de l’entreprise.  

4.  Dans la page **Types de déploiement** de l’Assistant Création d’une application, choisissez **Ajouter** pour créer un type de déploiement.  

 Pour plus d’informations, consultez [Créer des types de déploiement pour l’application](/sccm/apps/deploy-use/create-applications#create-deployment-types-for-the-application).  

5.  Choisissez **Suivant**, examinez les informations sur l’application figurant dans la page **Résumé**, puis suivez toutes les étapes de l’Assistant Création d’une application.  

La nouvelle application s’affiche dans le nœud **Applications** de la console Configuration Manager.  

##  <a name="create-deployment-types-for-the-application"></a>Créer des types de déploiement pour l'application  
 Si vous sélectionnez **Identifier automatiquement les informations sur ce type de déploiement à partir des fichiers d’installation** dans la page **Général** de l’Assistant Création d’un type de déploiement, vous n’avez pas besoin d’exécuter certaines étapes des procédures suivantes.  

## <a name="start-the-create-deployment-type-wizard"></a>Démarrer l’Assistant Création d’un type de déploiement  

1.  Dans la console Configuration Manager, choisissez **Bibliothèque de logiciels** > **Gestion des applications** > **Applications**.  

3.  Sélectionnez une application puis, sous l’onglet **Accueil**, dans le groupe **Application**, choisissez **Créer un type de déploiement**.  

> [!TIP]  
>  Vous pouvez également démarrer l’Assistant Création d’un type de déploiement à partir de l’Assistant Création d’une application et sous l’onglet **Types de déploiement** de la boîte de dialogue **Propriétés de** *nom_application\>*.  

## <a name="specify-whether-you-want-to-automatically-detect-deployment-type-information-or-manually-set-up-the-information"></a>Spécifier s’il est nécessaire de détecter automatiquement les informations sur le type de déploiement ou de configurer manuellement les informations  
 Utilisez l’une des procédures suivantes pour détecter automatiquement ou configurer manuellement les informations relatives au type de déploiement.  

### <a name="automatically-detect-deployment-type-information"></a>Détecter automatiquement les informations relatives au type de déploiement  

1.  Dans la page **Général** de l’Assistant Création d’un type de déploiement, sélectionnez **Identifier automatiquement les informations sur ce type de déploiement à partir des fichiers d’installation**.  

2.  Dans la zone **Type**, sélectionnez le type du fichier d’installation d’application à utiliser pour détecter les informations sur le type de déploiement.  

3.  Dans la zone **Emplacement**, spécifiez le chemin UNC (au format *\\\\serveur\\partage\\nom_fichier*) ou le lien du magasin vers les fichiers d’installation d’application et le contenu à utiliser pour détecter les informations sur le type de déploiement. Vous pouvez également choisir **Parcourir** pour rechercher le fichier d’installation.  

    > [!NOTE]  
    >  Vous devez avoir accès au chemin UNC qui contient l’application et à tous les sous-dossiers intégrant le contenu de l’application.  

4.  Dans la page **Importer des informations** de l’Assistant Création d’un type de déploiement, consultez les informations qui ont été importées, puis choisissez **Suivant**. Vous pouvez aussi choisir **Précédent** pour revenir en arrière et corriger les erreurs éventuelles.  

5.  Dans la page **Informations générales** de l’Assistant Création d’un type de déploiement, spécifiez les informations suivantes :  

    > [!NOTE]  
    >  Certaines informations relatives au type de déploiement peuvent déjà être présentes si elles ont été lues à partir des fichiers d'installation de l'application. En outre, les options affichées peuvent différer selon le type de déploiement que vous créez.  

    -   Informations générales sur le type de déploiement, comme le nom, les commentaires de l’administrateur et les langues disponibles.  

    -   **Programme d’installation** : spécifiez le programme d’installation et les éventuelles propriétés nécessaires pour installer le type de déploiement.  

    -   **Comportement à l’installation** : indiquez si vous souhaitez installer le type de déploiement pour l’utilisateur actuel ou tous les utilisateurs. Vous pouvez également spécifier si le type de déploiement sera installé pour tous les utilisateurs, s'il s'agit d'un déploiement vers un appareil, ou vers un utilisateur uniquement s'il s'agit d'un déploiement vers un utilisateur.  

    -   **Utiliser une connexion VPN automatique (si elle est configurée)** : si un profil VPN a été déployé sur l’appareil où l’application est exécutée, lancez la connexion VPN au démarrage de l’application (Windows 8.1 et Windows Phone 8.1 uniquement). Si plusieurs profils VPN ont été déployés sur un appareil Windows 8.1, le premier profil VPN déployé est utilisé par défaut.  

         Sur les appareils Windows Phone 8.1, les connexions VPN automatiques ne sont pas prises en charge si plusieurs profils VPN ont été déployés sur l'appareil.  

         Pour plus d’informations sur les profils VPN, consultez [Profils VPN dans System Center Configuration Manager](../../protect/deploy-use/vpn-profiles.md).  

6.  Choisissez **Suivant**, puis passez à [Spécifier les options de contenu pour le type de déploiement](/sccm/apps/deploy-use/create-applications#specify-content-options-for-the-deployment-type).  

### <a name="manually-set-up-the-deployment-type-information"></a>Configurer manuellement les informations sur le type de déploiement  

1.  Dans la page **Général,** de l’Assistant Création d’un type de déploiement, sélectionnez **Spécifier manuellement les informations sur le type de déploiement**.  

2.  Dans la zone **Type**, choisissez le type du fichier d’installation d’application à utiliser pour détecter les informations sur le type de déploiement. Vous pouvez choisir les mêmes types d’installation que vous utilisez quand vous détectez automatiquement les informations sur le type de déploiement, ainsi que spécifier un script pour installer le type de déploiement.  

3.  Dans la page **Informations générales** de l’Assistant Création d’un type de déploiement, spécifiez un nom pour le type de déploiement, une description facultative et les langues dans lesquelles vous souhaitez que ce type de déploiement soit disponible, puis choisissez **Suivant**.  

4.  Continuez avec [Spécifier les options de contenu pour le type de déploiement](/sccm/apps/deploy-use/create-applications#specify-content-options-for-the-deployment-type).  

##  <a name="specify-content-options-for-the-deployment-type"></a>Spécifier les options de contenu pour le type de déploiement  

1.  Dans la page **Contenu** de l’Assistant Création d’un type de déploiement, spécifiez les informations suivantes :  

    -   **Emplacement du contenu** : spécifiez l’emplacement du contenu pour ce type de déploiement, ou sélectionnez **Parcourir** pour choisir le dossier de contenu du type de déploiement.  

        > [!IMPORTANT]  
        >  Le compte du système de l'ordinateur du serveur de site doit disposer d'autorisations vers l'emplacement de contenu que vous spécifiez.  

    -   **Conserver le contenu dans la mémoire cache du client** : sélectionnez cette option pour spécifier si le contenu doit être conservé indéfiniment dans le cache de l’ordinateur client, même s’il a déjà été exécuté. Bien que cette option puisse être utile avec certains déploiements, comme les logiciels basés sur un programme d’installation Windows qui exigent qu’une copie de la source locale soit disponible pour appliquer les mises à jour, elle aura pour effet de réduire l’espace disponible dans le cache. Le choix de cette option peut entraîner l'échec d'un déploiement important plus tard si l'espace disponible dans le cache est insuffisant.  

    -   **Autoriser les clients à partager du contenu avec d’autres clients sur le même sous-réseau** : sélectionnez cette option pour réduire la charge sur le réseau en autorisant les clients à télécharger du contenu à partir d’autres clients locaux sur le réseau qui ont déjà téléchargé et mis en cache le contenu. Cette option utilise la technologie Windows BranchCache.  

    -   **Programme d’installation** : spécifiez le nom du programme d’installation et des paramètres d’installation requis, ou choisissez **Parcourir** pour localiser le fichier d’installation.  

    -   **Début de l’installation dans** : spécifiez éventuellement le dossier contenant le programme d’installation pour le type de déploiement. Ce dossier peut être un chemin absolu sur le client ou un chemin vers le dossier du point de distribution contenant les fichiers d’installation.  

    -   **Programme de désinstallation** : spécifiez éventuellement le nom du programme de désinstallation et tous les paramètres exigés, ou choisissez **Parcourir** pour le localiser.  

    -   **Début de la désinstallation dans** : spécifiez éventuellement le dossier contenant le programme de désinstallation pour le type de déploiement. Ce dossier peut être un chemin absolu sur le client ou un chemin relatif au dossier du point de distribution qui contient le package.  

    -   **Exécutez l’installation et désinstallez le programme en tant que processus 32 bits sur des clients 64 bits** : utilisez les emplacements de fichier et de Registre 32 bits sur des ordinateurs fonctionnant sous Windows pour exécuter le programme d’installation pour le type de déploiement.  

2.  Choisissez **Suivant**.  

## <a name="set-up-detection-methods-to-indicate-the-presence-of-the-deployment-type-windows-pcs-only"></a>Configurer des méthodes de détection pour indiquer la présence du type de déploiement (PC Windows uniquement)  
 Cette procédure configure une méthode de détection qui indique si le type de déploiement est déjà installé.  

1.  Dans la page **Méthode de détection** de l’Assistant Création d’un type de déploiement, sélectionnez **Configurer des règles pour détecter la présence de ce type de déploiement**, puis choisissez **Ajouter une clause**.  

    > [!NOTE]  
    >  Vous pouvez également sélectionner **Utiliser un script personnalisé pour détecter la présence de ce type de déploiement**. Pour plus d’informations, consultez [Utiliser un script personnalisé pour vérifier la présence d’un type de déploiement](/sccm/apps/deploy-use/create-applications#Use-a-custom-script-to-check-for-the-presence-of-a-deployment-type).  

2.  Dans la liste déroulante **Type de paramètre** de la boîte de dialogue **Règle de détection**, choisissez la méthode que vous souhaitez utiliser pour détecter la présence du type de déploiement. Vous pouvez choisir parmi les méthodes disponibles suivantes :  

    -   **Système de fichiers** : permet de détecter si un fichier ou un dossier spécifique existe sur un appareil client, indiquant ainsi que l’application est installée.  

        > [!NOTE]  
        >  Le paramètre **Système de fichiers** ne permet pas de spécifier un chemin d’accès UNC à un partage réseau dans le champ Chemin d’accès. Vous pouvez uniquement spécifier un chemin local sur l'appareil client.  
        >   
        >  Pour vérifier les emplacements de fichiers 32 bits pour le fichier ou dossier spécifié, sélectionnez d’abord l’option **Ce fichier ou dossier est associé à une application 32 bits sur des systèmes 64 bits**. Si le fichier ou dossier est introuvable, il sera cherché dans des emplacements 64 bits.  

    -   **Registre** : permet de détecter si une clé de Registre ou une valeur de Registre spécifiée existe sur un appareil client, indiquant ainsi que l’application est installée.  

        > [!NOTE]  
        >  Pour vérifier d’abord les emplacements du Registre 32 bits pour la clé de Registre spécifiée, sélectionnez d’abord l’option **Cette clé de Registre est associée à une application 32 bits sur des systèmes 64 bits**. Si la clé de Registre est introuvable, elle sera cherchée dans les emplacements 64 bits.  

    -   **Windows Installer** : permet de détecter si un fichier Windows Installer spécifique existe sur un appareil client, indiquant ainsi que l’application est installée.  

3.  Spécifiez les détails concernant l'élément que vous souhaitez utiliser pour détecter si ce type de déploiement est installé. Par exemple, vous pouvez utiliser un fichier, un dossier, une clé ou valeur de Registre ou bien un code de produit Windows Installer.  

4.  Spécifiez des détails sur la valeur que vous souhaitez évaluer par rapport à l'élément que vous utilisez pour détecter si le type de déploiement est installé. Par exemple, si vous utilisez un fichier pour vérifier si le type de déploiement est installé, vous pouvez sélectionner **Le paramètre du système de fichiers doit exister sur le système cible pour indiquer la présence de cette application**.  

5.  Choisissez **Suivant** pour fermer la boîte de dialogue **Règle de détection**.  

###  <a name="use-a-custom-script-to-check-for-the-presence-of-a-deployment-type"></a>Utiliser un script personnalisé pour vérifier la présence d’un type de déploiement  

1.  Dans la page **Méthode de détection** de l’Assistant Création d’un type de déploiement, sélectionnez **Utiliser un script personnalisé pour détecter la présence de ce type de déploiement**, puis choisissez **Modifier**.  

2.  Dans la boîte de dialogue **Éditeur de script**, sélectionnez la langue du script que vous souhaitez utiliser pour détecter le type de déploiement dans la liste déroulante **Type de script**.  

3.  Entrez le script à utiliser dans la zone **Contenu du script**. Vous pouvez également coller le contenu d’un script existant dans ce champ ou choisir **Ouvrir** pour accéder à un script existant enregistré. Configuration Manager vérifie les résultats du script en lisant les valeurs écrites dans le flux de sortie Standard Out (STDOUT), le flux de sortie Standard Error (STDERR) et le code de sortie du script. Si le code de sortie est une valeur non nulle, le script a échoué et l'état de la détection d'application est inconnu. Si le code de sortie est égal à zéro et STDOUT contient des données, l’état de la détection d’application est installé.  

 Utilisez le tableau suivant pour voir comment utiliser la sortie d’un script pour vérifier si une application est installée.  

|Code de sortie du script|Détails|
|--------------------------------|-----------------|
|0|**Données lues à partir de STDOUT** - Vide<br /><br /> **Données lues à partir de STDERR** - Vide<br /><br /> **Résultat du script** - Réussite<br /><br /> **État de détection de l’application** - Non installé|  
|0|**Données lues à partir de STDOUT** - Vide<br /><br /> **Données lues à partir de STDERR** - Non vide<br /><br /> **Résultat du script** - Échec<br /><br /> **État de détection de l’application** - Inconnu|  
|0|**Données lues à partir de STDOUT** - Non vide<br /><br /> **Données lues à partir de STDERR** - Vide<br /><br /> **Résultat du script** - Réussite<br /><br /> **État de détection de l’application** - Installé|  
|0|**Données lues à partir de STDOUT** - Non vide<br /><br /> **Données lues à partir de STDERR** - Non vide<br /><br /> **Résultat du script** - Réussite<br /><br /> **État de détection de l’application** - Installé|  
|Valeur non nulle|**Données lues à partir de STDOUT** - Vide<br /><br /> **Données lues à partir de STDERR** - Vide<br /><br /> **Résultat du script** - Échec<br /><br /> **État de détection de l’application** - Inconnu|  
|Valeur non nulle|**Données lues à partir de STDOUT** - Vide<br /><br /> **Données lues à partir de STDERR** - Non vide<br /><br /> **Résultat du script** - Échec<br /><br /> **État de détection de l’application** - Inconnu|  
|Valeur non nulle|**Données lues à partir de STDOUT** - Non vide<br /><br /> **Données lues à partir de STDERR** - Vide<br /><br /> **Résultat du script** - Échec<br /><br /> **État de détection de l’application** - Inconnu|  
|Valeur non nulle|**Données lues à partir de STDOUT** - Non vide<br /><br /> **Données lues à partir de STDERR** - Non vide<br /><br /> **Résultat du script** - Échec<br /><br /> **État de détection de l’application** - Inconnu|  

Le tableau suivant contient des exemples de script Microsoft Visual Basic (VB) que vous pouvez utiliser pour écrire vos propres scripts de détection d’application.  

|Exemple de script Visual Basic|Description|  
|--------------------------------|-----------------|  
|**WScript.Quit(1)**|Le script renvoie un code de sortie non nul, ce qui indique l'échec d'exécution correcte. Dans ce cas, l'état de la détection d'application est inconnu.|  
|**WScript.StdErr.Write "Échec du script"**<br /><br /> **WScript.Quit(0)**|Le script renvoie un code de sortie égal à zéro, mais la valeur de STDERR n'est pas vide, ce qui indique l'échec d'exécution correcte du script. Dans ce cas, l'état de la détection d'application est inconnu.|  
|**WScript.Quit(0)**|Le script renvoie un code de sortie égal à zéro, ce qui indique la réussite d'exécution. Toutefois, la valeur de STDOUT est vide, ce qui indique que l'application n'est pas installée.|  
|**WScript.StdOut.Write "L’application est installée"**<br /><br /> **WScript.Quit(0)**|Le script renvoie un code de sortie égal à zéro, ce qui indique la réussite d'exécution. La valeur de STDOUT n'est pas vide, ce qui indique que l'application est installée.|  
|**WScript.StdOut.Write "L’application est installée"**<br /><br /> **WScript.StdErr.Write "Fin"**<br /><br /> **WScript.Quit(0)**|Le script renvoie un code de sortie égal à zéro, ce qui indique la réussite d'exécution. Les valeurs de STDOUT et STDERR ne sont pas vides, ce qui indique que l'application est installée.|  

 > [!NOTE]  
 >  La taille maximale que vous pouvez utiliser pour un script est 32 Ko.  

4.  Choisissez **OK** pour fermer la boîte de dialogue **Éditeur de script**.  

## <a name="specify-user-experience-options-for-the-deployment-type"></a>Spécifier les options d’expérience utilisateur pour le type de déploiement  
 Ces paramètres définissent comment l’application va être installée sur les appareils et ce que l’utilisateur verra.  

1.  Dans la page **Expérience utilisateur** de l’Assistant Création d’un type de déploiement, spécifiez les informations suivantes :  

    -   **Comportement d’installation** : dans la liste déroulante, sélectionnez l’une des options suivantes :  

        -   **Installer pour l’utilisateur** : l’application est installée uniquement pour l’utilisateur pour lequel elle est déployée.  

        -   **Installer pour le système** : l’application est installée une seule fois et elle est disponible pour tous les utilisateurs.  

        -   **Installer pour le système si la ressource est un périphérique ; sinon installer pour l’utilisateur** : si l’application est déployée sur un appareil, elle est installée pour tous les utilisateurs. Si l'application est déployée sur un utilisateur, elle sera installée uniquement pour cet utilisateur.  

    -   **Condition d’ouverture de session** : spécifiez les conditions d’ouverture de session pour ce type de déploiement à partir des options suivantes :  

        -   **Uniquement quand un utilisateur a ouvert une session**  

        -   **Qu’un utilisateur ait ouvert une session ou non**  

        -   **Uniquement lorsqu’aucun utilisateur n’a de session ouverte**  

        > [!NOTE]  
        >  Par défaut, cette option sera définie sur **Uniquement lorsqu'un utilisateur a ouvert une session**et ne pourra pas être modifiée si vous avez sélectionné **Installer pour l'utilisateur** dans la liste déroulante **Comportement d'installation** .  

    -   **Visibilité du programme d’installation** : spécifiez le mode dans lequel le type de déploiement sera exécuté sur les appareils clients. Les options ci-dessous sont disponibles :  

        -   **Agrandie** : le type de déploiement est exécuté de manière agrandie sur les appareils clients. Les utilisateurs verront toute l'activité de l'installation.  

        -   **Normale** : le type de déploiement est exécuté en mode normal, en fonction des valeurs par défaut du système et du programme. Il s'agit du mode par défaut.  

        -   **Réduite** : le type de déploiement est exécuté de manière réduite sur les appareils clients. Les utilisateurs peuvent voir l'activité de l'installation dans la zone de notification ou dans la barre des tâches.  

        -   **Masquée** : le type de déploiement est exécuté de manière masquée sur les appareils clients et les utilisateurs ne voient aucune activité d’installation.  

    -   **Permettre aux utilisateurs d’afficher et d’interagir avec l’installation du programme** : spécifiez si un utilisateur peut interagir avec l’installation du type de déploiement pour configurer les options d’installation.  

        > [!NOTE]  
        >  Cette option est activée par défaut si l'option **Installer pour l'utilisateur** est sélectionnée dans la liste déroulante **Comportement d'installation** .  

    -   **Durée maximale d’exécution allouée (en minutes)** : spécifiez la durée maximale pendant laquelle le programme est supposé s’exécuter sur l’ordinateur client. Ce paramètre peut être spécifié comme un nombre entier supérieur à zéro. Le paramètre par défaut est de 120 minutes.  

         Cette valeur est utilisée pour :  

        -   surveiller les résultats du type de déploiement ;  

        -   vérifier si un type de déploiement sera installé une fois que des fenêtres de maintenance auront été définies sur des appareils clients. Lorsqu'une fenêtre de maintenance est activée, un programme démarre uniquement s'il reste suffisamment de temps dans la fenêtre de maintenance pour respecter l'option **Durée maximale d'exécution allouée** .  

        > [!IMPORTANT]  
        >  Un conflit peut se produire si la **durée maximale d'exécution allouée** est plus longue que celle de la fenêtre de maintenance planifiée. Si la durée maximale d'exécution définie par l'utilisateur dépasse la longueur des fenêtres de maintenance disponibles, ce type de déploiement n'est pas exécuté.  

2.  **Temps d’installation estimé (minutes)** : spécifiez la durée estimée nécessaire à l’installation du type de déploiement. Il est indiqué aux utilisateurs du Centre logiciel.  

## <a name="specify-requirements-for-the-deployment-type"></a>Spécifier des spécifications pour le type de déploiement  

1.  Dans la page **Spécifications** de l’Assistant Création d’un type de déploiement, choisissez **Ajouter** pour ouvrir la boîte de dialogue **Créer une spécification**, puis ajoutez une nouvelle spécification.  

    > [!NOTE]  
    >  Vous pouvez également ajouter de nouvelles spécifications sous l’onglet **Spécifications** de la boîte de dialogue **Propriétés** de *<nom_type_déploiement\>*.  

2.  Dans la liste déroulante **Catégorie**, indiquez si cette spécification s’applique à un appareil ou à un utilisateur, ou sélectionnez **Personnalisé** pour utiliser une condition globale préalablement créée. Quand vous sélectionnez **Personnalisé**, vous pouvez également choisir **Créer** pour créer une condition globale. Pour plus d’informations sur les conditions globales, consultez [Comment créer des conditions globales](../../apps/deploy-use/create-global-conditions.md).  

    > [!IMPORTANT]  
    >  Les spécifications relatives à la catégorie **Utilisateur** et à la condition **Périphérique principal** sont ignorées si vous déployez l’application sur un regroupement d’appareils.  
    >   
    >  Si vous avez créé une séquence de tâches ou un package et un programme Windows qui a Windows 10 comme spécification à l’aide de System Center 2012 R2 Configuration Manager SP1 et que vous effectuez une mise à niveau vers System Center Configuration Manager, la spécification relative à Windows 10 peut être supprimée. Pour résoudre ce problème, spécifiez à nouveau la spécification. Notez que bien que l’exigence ait été supprimée de l’affichage des exigences, elle est toujours traitée correctement sur les appareils.  

3.  Dans la liste déroulante **Condition** , sélectionnez la condition que vous souhaitez utiliser pour déterminer si l'utilisateur ou l'appareil répond aux spécifications de l'installation. Le contenu de cette liste varie en fonction de la catégorie sélectionnée.  

4.  Dans la liste déroulante **Opérateur** , choisissez l'opérateur qui sera utilisé pour comparer la condition sélectionnée à la valeur spécifiée, afin d'évaluer si l'utilisateur ou l'appareil répond aux spécifications de l'installation. Les opérateurs disponibles varient en fonction de la condition sélectionnée.  

    > [!IMPORTANT]  
    >  Les spécifications disponibles varient selon le type d’appareil utilisé par le type de déploiement.  

5.  Dans la zone **Valeur**, spécifiez les valeurs qui seront utilisées avec la condition et l’opérateur sélectionnés pour évaluer si l’utilisateur ou l’appareil respecte les spécifications de l’installation. Les valeurs disponibles varient en fonction de la condition et de l'opérateur sélectionnés.  

6.  Choisissez **OK** pour enregistrer la spécification et fermer la boîte de dialogue **Créer une spécification**.  

## <a name="specify-dependencies-for-the-deployment-type"></a>Spécifier des dépendances pour le type de déploiement  
 Les dépendances définissent un ou plusieurs types de déploiement d'un autre type d'application qui doivent être installés avant l'installation d'un type de déploiement. Vous pouvez configurer les types de déploiement dépendants à installer automatiquement avant l’installation d’un type de déploiement.  

> [!IMPORTANT]  
>  Dans certains cas, un type de déploiement est dépendant d’un type de déploiement qui a également des dépendances. Le nombre maximal de dépendances prises en charge dans la chaîne est de 5.  

1.  Dans la page **Dépendances** de l’Assistant Création d’un type de déploiement, choisissez **Ajouter** pour spécifier les types de déploiement à installer avant l’installation de ce type de déploiement.  

    > [!IMPORTANT]  
    >  Vous pouvez également ajouter de nouvelles dépendances sous l’onglet **Dépendances** de la boîte de dialogue **Propriétés** de *<nom_type_déploiement\>*.  

2.  Dans la boîte de dialogue **Ajouter une dépendance**, choisissez **Ajouter**.  

3.  Dans la boîte de dialogue **Spécifier l'application requise** , sélectionnez une application existante et l'un des types de déploiement d'application à utiliser en tant que dépendance.  

    > [!TIP]  
    >  Vous pouvez choisir **Afficher** pour afficher les propriétés de l’application ou du type de déploiement sélectionné.  

4.  Choisissez **OK** pour fermer la boîte de dialogue **Spécifier l’application requise**.  

5.  Si vous souhaitez qu'une application dépendante soit installée automatiquement, voir **Installation automatique** à côté de l'application dépendante.  

    > [!NOTE]  
    >  Une application dépendante n'a pas besoin être déployée pour être automatiquement installée.  

6.  Dans la boîte de dialogue **Ajouter une dépendance**, sous **Nom du groupe de dépendances**, entrez un nom pour faire référence à ce groupe de dépendances d’applications.  

7.  Vous pouvez également utiliser les boutons **Augmenter la priorité** et **Diminuer la priorité** pour modifier l'ordre dans lequel chaque dépendance est évaluée.  

8.  Choisissez **OK** pour fermer la boîte de dialogue **Ajouter une dépendance**.  

## <a name="confirm-the-deployment-type-settings-and-finish-the-wizard"></a>Confirmer les paramètres relatifs au type de déploiement et terminer l’Assistant  

1.  Dans la page **Résumé** de l’Assistant Création d’un type de déploiement, passez en revue les actions que doit prendre l’Assistant. Choisissez **Suivant** pour créer le type de déploiement ou **Précédent** pour revenir en arrière et modifier les paramètres du type de déploiement.  

2.  Après la fermeture de la page **Progression**, passez en revue les actions prises par l’Assistant, puis choisissez **Fermer** pour terminer l’Assistant.  

3.  Si vous avez démarré l’Assistant Création d’un type de déploiement à partir de l’Assistant Création d’une application, vous revenez à la page **Types de déploiement** de l’Assistant Création d’une application.  

## <a name="set-up-additional-options-for-deployment-types-that-contain-virtual-applications"></a>Configurer des options supplémentaires pour les types de déploiement qui contiennent des applications virtuelles  
 Utilisez les procédures suivantes pour configurer des options supplémentaires pour les types de déploiement qui contiennent des applications virtuelles.  

### <a name="set-up-content-options-for-application-virtualization-app-v-deployment-types"></a>Configurer les options de contenu pour les types de déploiement App-V (Application Virtualization)  

1.  Dans la console Configuration Manager, choisissez **Bibliothèque de logiciels** > **Applications**.  

2.  Dans la liste **Applications**, sélectionnez une application contenant un type de déploiement App-V. Ensuite, sous l’onglet **Accueil**, dans le groupe **Propriétés**, choisissez **Propriétés**.  

3.  Dans la boîte de dialogue **Propriétés de** *<nom_application\>*, sous l’onglet **Types de déploiement**, sélectionnez un type de déploiement App-V, puis choisissez **Modifier**.  

4.  Dans la boîte de dialogue **Propriétés de** *<Nom du type de déploiement\>*, sous l’onglet **Contenu**, configurez les options suivantes, si nécessaire :  

    -   **Conserver le contenu dans la mémoire cache du client** : sélectionnez cette option pour vérifier que le contenu de ce type de déploiement n’est pas supprimé du cache du client Configuration Manager.  

    -   **Charger le contenu dans le cache AppV avant le lancement** : sélectionnez cette option pour vérifier que tout le contenu de l’application virtuelle est chargé dans le cache App-V avant le lancement de l’application. Cette option garantit également que le contenu de l'application ne sera pas épinglé dans le cache et que celui-ci pourra être supprimé au besoin.  

5.  Cliquez sur **OK** pour fermer la boîte de dialogue **Propriétés de** *<nom_type_déploiement\>*.  

6.  Choisissez **OK** pour fermer la boîte de dialogue **Propriétés de** *<nom_application\>*.  

### <a name="set-up-publishing-options-for-app-v-deployment-types"></a>Configurer les options de publication pour les types de déploiement App-V  

1.  Dans la console Configuration Manager, choisissez **Bibliothèque de logiciels** > **Applications**.  

3.  Dans la liste **Applications**, sélectionnez une application contenant un type de déploiement App-V. Ensuite, sous l’onglet **Accueil**, dans le groupe **Propriétés**, choisissez **Propriétés**.  

4.  Dans la boîte de dialogue **Propriétés de** *<nom_application\>*, sous l’onglet **Types de déploiement**, sélectionnez un type de déploiement App-V, puis choisissez **Modifier**.  

5.  Dans la boîte de dialogue **Propriétés de** *<nom_type_déploiement\>*, sous l’onglet **Publication**, sélectionnez les éléments de l’application virtuelle à publier.  

6.  Cliquez sur **OK** pour fermer la boîte de dialogue **Propriétés de** *<nom_type_déploiement\>*.  

7.  Choisissez **OK** pour fermer la boîte de dialogue **Propriétés de** *<nom_application\>*.  

## <a name="import-an-application"></a>Importer une application  
 Utilisez la procédure ci-dessous pour importer une application dans Configuration Manager. Pour plus d’informations sur l’exportation d’une application, consultez [Tâches de gestion pour les applications System Center Configuration Manager](../../apps/deploy-use/management-tasks-applications.md).  

1.  Dans la console Configuration Manager, choisissez **Bibliothèque de logiciels** > **Gestion des applications** > **Applications**.   

3.  Sous l’onglet **Accueil**, dans le groupe **Créer**, choisissez **Importer l’application**.  

4.  Dans la page **Général** de l’**Assistant Importation de l’application**, choisissez **Parcourir**, puis spécifiez un chemin UNC au fichier .zip contenant l’application à importer.  

5.  Dans la page **Contenu du fichier**, sélectionnez l’action à effectuer quand l’application que vous essayez d’importer est un doublon d’une application existante. Vous pouvez créer une application ou ignorer la copie et ajouter une nouvelle révision à l’application existante.  

6.  Dans la page **Résumé**, passez en revue les actions à effectuer, puis terminez l’Assistant.  

 La nouvelle application s’affiche dans le nœud **Applications**.  

> [!TIP]  
>  L’applet de commande Windows PowerShell **Import-CMApplication** permet de réaliser la même opération que cette procédure. Pour plus d’informations, consultez [Import-CMApplication](https://technet.microsoft.com/library/jj821738.aspx) dans la référence sur les applets de commande Microsoft System Center 2012 Configuration Manager SP1.  

##  <a name="deployment-types-supported-by-configuration-manager"></a>Types de déploiement pris en charge par Configuration Manager  

|Nom du type de déploiement|Plus d'informations|  
|--------------------------|----------------------|  
|**Windows Installer (\*fichier .msi)**|Crée un type de déploiement à partir d'un fichier Windows Installer.|  
|**Package d’application Windows (\*.appx, \*.appxbundle)**|Crée un type de déploiement pour Windows 8, Windows RT ou version ultérieure, à partir d’un fichier de package d’application Windows ou d’un package de lots d’applications Windows.|  
|**Package d’application Windows (dans le Windows Store)**|Crée un type de déploiement pour Windows 8, Windows RT ou version ultérieure, en spécifiant un lien vers l’application dans Windows Store ou en parcourant le magasin pour sélectionner l’application dont vous avez besoin.<br /><br /> Si vous voulez déployer l'application sous forme de lien vers Windows Store, vérifiez que le paramètre de stratégie de groupe **Désactiver l'application du Store** est défini sur **Désactivé** ou sur **Non configuré**. Si ce paramètre est activé, les clients ne pourront pas se connecter à Windows Store pour télécharger et installer des applications.<br /><br /> Les types de déploiements de Windows 8 qui utilisent un lien vers un magasin sont toujours évalués avant d’autres types de déploiements, quelle que soit leur priorité.|  
|**Programme d’installation de script**|Crée un type de déploiement spécifiant un script qui s’exécute sur des appareils clients pour installer un contenu ou pour effectuer une action.|  
|**Microsoft Application Virtualization 4**|Crée un type de déploiement à partir d’un fichier manifeste Microsoft Application Virtualization 4.|  
|**Microsoft Application Virtualization 5**|Crée un type de déploiement à partir d'un fichier de package Microsoft Application Virtualization 5.|  
|**Package d’application Windows Phone (\*fichier .xap)**|Crée un type de déploiement à partir d'un fichier de package d'application Windows Phone.|  
|**Package d’application Windows Phone (dans le Windows Phone Store)**|Crée un type de déploiement en spécifiant un lien vers l’application dans le Windows Phone Store.|  
|**Fichier CAB Windows Mobile**|Crée un type de déploiement pour des appareils Windows Mobile à partir d’un fichier CAB Windows Mobile.|  
|**Package d’application pour iOS (fichier \*.ipa)**|Crée un type de déploiement à partir d'un fichier de package d'application iOS.|  
|**Package d’application pour iOS depuis l’App Store**|Crée un type de déploiement en spécifiant un lien vers l'application iOS dans l'App Store.|  
|**Package d’application pour Android (fichier \*.apk)**|Crée un type de déploiement à partir d'un fichier de package d'application Android.|  
|**Package d’application pour Android sur Google Play**|Crée un type de déploiement en spécifiant un lien vers l'application sur Google Play.|  
|**Mac OS X**|Crée un type de déploiement pour les ordinateurs Mac à partir d'un fichier .cmmac que vous avez créé à l'aide de l'outil CMAppUtil.<br /><br /> S’applique uniquement aux ordinateurs Mac exécutant le client Configuration Manager.|  
|**Application web**|Crée un type de déploiement qui spécifie un lien vers une application Web. Le type de déploiement installe un raccourci vers l'application Web sur l'appareil de l'utilisateur.<br /><br /> Si vous avez installé Intune Managed Browser sur des appareils iOS ou Android que vous gérez, vous pouvez vous assurer que les utilisateurs peuvent uniquement utiliser Managed Browser pour ouvrir l’application. Pour ce faire, utilisez un des formats suivants quand vous spécifiez un lien vers l’application, en remplaçant **http:** par **http-intunemam:** ou **https:** par **https-intunemam:**<br /><br /> - **http-intunemam://<chemin de l’application web\>**<br /><br /> - **https-intunemam://<chemin de l’application web\>**<br /><br /> Vous pouvez imposer une configuration requise pour Configuration Manager afin de vérifier que les applications à associer au navigateur Managed Browser sont installées uniquement sur des appareils iOS et Android.<br /><br /> Pour plus d’informations sur Intune Managed Browser, consultez [Gérer l’accès à Internet à l’aide de stratégies Managed Browser](../../apps/deploy-use/manage-internet-access-using-managed-browser-policies.md).|  
|**Windows Installer via la gestion des appareils mobiles (\*.msi)**|Ce type de programme d’installation vous permet de créer et déployer des applications Windows Installer sur des PC qui exécutent Windows 10.<br /><br /> Tenez compte des points suivants quand vous utilisez ce type de programme d’installation :<br><br>- Vous ne pouvez télécharger qu’un seul fichier avec l’extension .msi.<br /><br /> - Le code de produit et la version de produit du fichier sont utilisés pour la détection d’applications.<br /><br /> - Le comportement de redémarrage par défaut de l’application sera utilisé. Configuration Manager ne contrôle pas cette fonctionnalité.<br /><br /> - Les packages MSI par utilisateur sont installés pour un utilisateur unique.<br /><br /> - Les packages MSI par ordinateur sont installés pour tous les utilisateurs sur l’appareil.<br /><br /> - Actuellement, les packages MSI en mode double s’installent uniquement pour tous les utilisateurs sur l’appareil.<br /><br /> - Les mises à jour d’application sont prises en charge quand le code de produit MSI de chaque version est identique.|  

