---
title: "Créer et déployer une application | System Center Configuration Manager"
description: "Créez et déployez une application contenant une application métier et apprenez à gérer efficacement les applications."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3bd1e487-ea18-43c1-b7c3-acbd9b86d429
caps.latest.revision: 15
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 12653342e2e311a9bbfc2a7aad3101c0e7f0bce0


---
# <a name="create-and-deploy-an-application-with-system-center-configuration-manager"></a>Créer et déployer une application avec System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Cette rubrique vous montre de façon concrète comment créer une application avec System Center Configuration Manager. Dans cet exemple, vous allez créer et déployer une application qui contient une application métier pour PC Windows appelée **Contoso.msi** . Cette application doit ensuite être déployée sur tous les PC exécutant Windows 10 qui sont installés dans votre entreprise. Au fil des étapes, vous allez découvrir de nombreuses façons de gérer plus efficacement les applications.  

 Cette procédure est destinée à vous donner une vue d’ensemble de la manière de créer et déployer des applications Configuration Manager. Elle ne couvre pas toutes les options que vous pouvez configurer, ni le processus de création et de déploiement d’applications pour d’autres plateformes.  

 Pour obtenir des détails spécifiques adaptés à chaque plateforme, consultez l’une des rubriques suivantes :  

-   [Créer des applications Windows](../../apps/get-started/creating-windows-applications.md)  
-   [Créer des applications iOS](../../apps/get-started/creating-ios-applications.md)  
-   [Créer des applications Android](../../apps/get-started/creating-android-applications.md)  
-   [Créer des applications Windows Phone](../../apps/get-started/creating-windows-phone-applications.md)  
-   [Créer des applications pour ordinateurs Mac](../../apps/get-started/creating-mac-computer-applications.md)  
-   [Créer des applications serveur Linux et UNIX](../../apps/get-started/creating-linux-and-unix-server-applications.md) 
-   [Créer des applications Windows Embedded](../../apps/get-started/creating-windows-embedded-applications.md) 

  
Si vous êtes déjà familiarisé avec les applications Configuration Manager, vous pouvez ignorer cette rubrique. En revanche, vous pouvez consulter la rubrique [Créer des applications](../../apps/deploy-use/create-applications.md) pour découvrir toutes les options disponibles au moment de créer et déployer des applications.  
  
## <a name="before-you-start"></a>Avant de commencer  

Veillez à prendre connaissance des informations contenues dans la rubrique de [présentation de la gestion des applications](/sccm/apps/understand/introduction-to-application-management) de façon à préparer votre site à l’installation d’applications et à comprendre la terminologie employée dans cette rubrique.  

 Vérifiez aussi que les fichiers d’installation de l’application **Contoso.msi** se trouvent à un emplacement accessible sur votre réseau.  
  
## <a name="create-the-configuration-manager-application"></a>Créer l’application Configuration Manager  
  
### <a name="start-the-create-application-wizard-and-create-the-application"></a>Démarrer l’Assistant Création d’une application et créer l’application  
  
1.  Dans la console Configuration Manager, cliquez sur **Bibliothèque de logiciels** > **Gestion des applications** > **Applications**.  
  
3.  Dans l'onglet **Accueil** , dans le groupe **Créer** , cliquez sur **Créer une application**.  

4.  Dans la page **Général** de l’ **Assistant Création d’une application**, sélectionnez **Détecter automatiquement les informations de cette application à partir des fichiers d’installation**. Cette option permet de préremplir certaines informations dans l’Assistant avec les informations extraites du fichier d’installation .msi. Spécifiez ensuite les informations suivantes :  

    -   **Type** : choisissez **Windows Installer (fichier \*.msi)**.  

    -   **Emplacement** : entrez l’emplacement du fichier d’installation **Contoso.msi** (ou cliquez sur **Parcourir**pour le sélectionner). Notez que l’emplacement doit être spécifié sous la forme *\\\Serveur\Partage\Fichier* pour permettre à Configuration Manager de trouver les fichiers d’installation.  
  
    Le résultat doit ressembler à la capture d’écran suivante :  
  
    ![Page Général de l’Assistant Gestion des applications](/sccm/apps/get-started/media/App-management-wizard-general-page.png)  
  
5.  Cliquez sur **Suivant**. La page **Importer des informations** affiche des informations sur l’application et tous les fichiers associés qui ont été importés dans Configuration Manager. Quand vous avez terminé, cliquez encore sur **Suivant** .  

6.  Dans la page **Informations générales**, vous pouvez fournir des informations complémentaires sur l’application pour faciliter le tri et sa localisation dans la console Configuration Manager.  

     De plus, vous pouvez spécifier, dans le champ Programme d’installation, la ligne de commande complète à utiliser pour installer l’application sur les PC. Vous pouvez modifier ce champ pour ajouter les propriétés souhaitées (par exemple, **/q** pour effectuer une installation sans assistance).  

    > [!TIP]  
    >  Certains champs de cette page de l’Assistant peuvent avoir été renseignés automatiquement au moment où vous avez importé les fichiers d’installation de l’application.  

     Le résultat doit ressembler à la capture d’écran suivante :  
  
     ![Page Informations générales de l’Assistant Gestion des applications](/sccm/apps/get-started/media/App-management-wizard-general-information-page.png)  
  
7.  Cliquez sur **Suivant**. Dans la page Résumé, vous pouvez vérifier vos paramètres d’application, puis terminer l’Assistant.  

 Vous avez fini de créer l’application. Pour la trouver, dans l’espace de travail **Bibliothèque de logiciels** , développez **Gestion d’applications**, puis cliquez sur **Applications**. Pour cet exemple, vous verrez ceci :  
  
 ![Graphique de l’application finale](/sccm/apps/get-started/media/Final-app-graphic.png)  
  
## <a name="examine-the-properties-of-the-application-and-its-deployment-type"></a>Examiner les propriétés de l’application et son type de déploiement  

Après avoir créé une application, vous pouvez ajuster les paramètres de l’application, si nécessaire. Pour afficher les propriétés de l’application, sélectionnez l’application et, sous l’onglet **Accueil** , dans le groupe **Propriétés** , cliquez sur **Propriétés**.  

 La boîte de dialogue **Propriétés de l’application <Contoso\>** contient beaucoup d’éléments que vous pouvez configurer pour ajuster le comportement de l’application. Pour plus d’informations sur tous les paramètres configurables, consultez [Créer des applications](../../apps/deploy-use/create-applications.md). Pour cet exemple, vous allez seulement modifier quelques propriétés du type de déploiement de l’application.  
  
 Cliquez sur l’onglet **Types de déploiement** , sélectionnez le type de déploiement **Application Contoso** , puis cliquez sur **Modifier**.   
Une boîte de dialogue similaire à celle-ci s’affiche :  
 
![Page de propriétés de l’application dans la gestion des applications](/sccm/apps/get-started/media/App-management-app-properties-page.png)  
  
## <a name="add-a-requirement-to-the-deployment-type"></a>Ajouter une spécification pour le type de déploiement  
 Les spécifications indiquent les conditions devant être remplies pour qu’une application soit installée sur un appareil.  Vous pouvez choisir des spécifications prédéfinies ou créer les vôtres. Dans cet exemple, vous allez ajouter une spécification pour que l’application s’installe uniquement sur les PC exécutant Windows 10.  
  
1.  Dans la page de propriétés du type de déploiement que vous venez d’ouvrir, cliquez sur l’onglet **Spécifications** .  

2.  Cliquez sur **Ajouter** pour ouvrir la boîte de dialogue **Créer une spécification** .  

3.  Dans la boîte de dialogue **Créer une spécification** , indiquez les informations suivantes :  

    -   **Catégorie** - **Appareil**  

    -   **Condition** - **Système d’exploitation**  

    -   **Type de règle** - **Valeur**  

    -   **Opérateur** - **L’un des**  

    -   Dans la liste des systèmes d’exploitation, sélectionnez **Windows 10**.  
  
    Vous obtenez une boîte de dialogue similaire à celle-ci :  
  
    ![Page de spécifications dans la gestion des applications](/sccm/apps/get-started/media/App-management-requirements-page.png)  
  
4.  Cliquez sur **OK** pour fermer chaque page de propriétés ouverte, puis revenez à la liste **Applications** dans la console Configuration Manager.  

> [!TIP]  
>  Les spécifications peuvent permettre de réduire le nombre de regroupements Configuration Manager dont vous avez besoin. Sachant que vous avez indiqué que l’application ne peut s’installer que sur des PC exécutant Windows 10, si vous la déployez par la suite dans un regroupement qui comporte des PC exécutant divers systèmes d’exploitation, l’application s’installera uniquement sur les PC Windows 10.  
  
## <a name="add-the-application-content-to-a-distribution-point"></a>Ajouter le contenu de l’application à un point de distribution  

Pour réussir le déploiement de l’application sur des PC, vous devez ensuite vérifier que le contenu de l’application est bien copié sur un point de distribution. Les PC accéderont au point de distribution pour installer l’application.  

> [!TIP]  
>  Pour plus d’informations sur les points de distribution et la gestion de contenu dans Configuration Manager, consultez [Gérer le contenu et l’infrastructure de contenu](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  
  
1.  Dans la console Configuration Manager, cliquez sur **Bibliothèque de logiciels**.  

2.  Dans l’espace de travail **Bibliothèque de logiciels** , développez **Applications** puis, dans la liste des applications, sélectionnez l’ **application Contoso** que vous avez créée.  

3.  Dans l'onglet **Accueil** , dans le groupe **Déploiement** , cliquez sur **Distribuer du contenu**.  

4.  Dans la page **Général** de l’ **Assistant Distribuer du contenu**, vérifiez que le nom de l’application est correct, puis cliquez sur **Suivant**.  

5.  Dans la page **Contenu** , vérifiez les informations qui seront copiées sur le point de distribution, puis cliquez sur **Suivant**.  

6.  Dans la page **Destination du contenu** , cliquez sur Ajouter pour sélectionner un ou plusieurs points de distribution ou bien les groupes de points de distribution sur lesquels le contenu de l’application doit être installé.  

7.  Effectuez toutes les étapes de l'Assistant.  

 Vous pouvez vérifier que le contenu de l’application a bien été copié sur le point de distribution via l’espace de travail **Analyse** , sous **État de distribution** > **État du contenu**.  
  
## <a name="deploy-the-application"></a>Déployer l'application  

Ensuite, déployez l’application sur un regroupement de périphériques de votre hiérarchie. Pour cet exemple, vous déploierez l’application dans le regroupement de périphériques **Tous les systèmes** .  

> [!TIP]  
>  N’oubliez pas que seuls les ordinateurs Windows 10 installeront l’application du fait des spécifications que vous avez sélectionnées précédemment.  
  
1.  Dans la console Configuration Manager, cliquez sur **Bibliothèque de logiciels** > **Gestion des applications** > **Applications**.  
  
3.  Dans la liste d’applications, sélectionnez l’application que vous avez créée précédemment, à savoir **Application Contoso**puis, sous l’onglet **Accueil** , dans le groupe **Déploiement** , cliquez sur **Déployer**.  

4.  Dans la page **Général** de l’ **Assistant Déploiement logiciel**, cliquez sur **Parcourir** pour sélectionner le regroupement de périphériques **Tous les systèmes** .  

5.  Dans la page **Contenu**, vérifiez que le point de distribution à partir duquel les PC doivent installer l’application est bien sélectionné.  

6.  Dans la page **Paramètres de déploiement**, vérifiez que l’action de déploiement définie est **Installer** et que l’objectif du déploiement est **Obligatoire**.  

    > [!TIP]  
    >  En définissant l’objectif de déploiement **Obligatoire**, vous avez l’assurance que l’application sera installée sur des PC conformes aux spécifications que vous avez définies. Si vous définissez la valeur **Disponible**, les utilisateurs peuvent installer l’application à la demande à partir du Centre logiciel.  

7.  Dans la page **Planification** , vous pouvez configurer à quel moment l’application sera installée. Pour cet exemple, sélectionnez **Dès que possible après le délai disponible**.  

8.  Dans la page **Expérience utilisateur**, cliquez sur **Suivant** pour accepter les valeurs par défaut.  

9. Effectuez toutes les étapes de l'Assistant.  

 Consultez la section **Surveiller l’application** ci-dessous pour savoir comment identifier l’état du déploiement de votre application.  
  
## <a name="monitor-the-application"></a>Surveiller l’application  
 Cette section vous explique comment examiner en un coup d’œil l’état du déploiement de l’application que vous venez de déployer.  
  
### <a name="to-review-the-deployment-status"></a>Pour consulter l’état du déploiement  
  
1.  Dans la console Configuration Manager, cliquez sur **Surveillance** > **Déploiements**.  
  
3.  Dans la liste des déploiements, sélectionnez **Application Contoso**.  

4.  Dans l'onglet **Accueil** , du groupe **Déploiement** , cliquez sur **Afficher l'état**.  

5.  Sélectionnez l’un des onglets suivants pour en savoir plus sur l’état du déploiement de l’application :  

    -   **Opération réussie** : l’application a bien été installée sur les PC indiqués.  

    -   **En cours** : l’installation de l’application n’est pas encore terminée.  

    -   **Erreur** : une erreur s’est produite pendant l’installation de l’application sur les PC indiqués. Des informations complémentaires sur l’erreur sont aussi affichées.  

    -   **Configuration non conforme** : l’installation de l’application sur les appareils indiqués n’a pas eu lieu, car ils n’étaient pas conformes aux spécifications que vous aviez configurées (en l’occurrence, ils n’exécutaient pas Windows 10).  

    -   **Inconnu** : Configuration Manager n’a pas pu communiquer l’état du déploiement. Faites une nouvelle vérification ultérieurement.  

> [!TIP]  
>  Il existe plusieurs façons de surveiller les déploiements d’applications. Pour plus d’informations, consultez [Surveiller les applications](/sccm/apps/deploy-use/monitor-applications-from-the-console).  
  
## <a name="end-user-experience"></a>Expérience de l’utilisateur final  

Les utilisateurs dotés de PC exécutant Windows 10 et dont la gestion est assurée par Configuration Manager verront apparaître un message les invitant à installer l’application Contoso. L’application s’installera dès lors qu’ils auront accepté l’installation.  



<!--HONumber=Nov16_HO1-->


