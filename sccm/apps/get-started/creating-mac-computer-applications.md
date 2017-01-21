---
title: "Créer des applications pour ordinateurs Mac | Microsoft Docs"
description: "Examinez les éléments à prendre en compte quand vous créez et déployez des applications pour des ordinateurs Mac."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ab1aecdd-d943-44f5-b0a9-e8fe7439e5d6
caps.latest.revision: 9
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 8dcf9f310a4ea8e2f43f2fe79e5e3cfa2c8aeb61
ms.openlocfilehash: c2feffad39a20519fd86ca9348b0855a51e05aa9


---
# <a name="create-mac-computer-applications-with-system-center-configuration-manager"></a>Créer des applications pour ordinateurs Mac avec System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

En plus des autres exigences et procédures System Center Configuration Manager à observer pour créer une application, vous devez aussi prendre en compte les éléments suivants au moment de créer et de déployer des applications pour des ordinateurs Mac.  

> [!IMPORTANT]  
>  Les procédures décrites dans cette rubrique abordent des informations sur le déploiement d’applications sur un ordinateur Mac sur lequel vous avez installé le client Configuration Manager. Les ordinateurs Mac que vous avez inscrits auprès de Microsoft Intune ne prennent pas en charge le déploiement d’applications.  

## <a name="general-considerations"></a>Éléments généraux à prendre en compte  
 Vous pouvez utiliser System Center Configuration Manager pour déployer des applications sur les ordinateurs Mac qui exécutent le client Configuration Manager pour Mac. La procédure de déploiement de logiciels sur les ordinateurs Mac est similaire à celle utilisée pour le déploiement de logiciels sur les ordinateurs Windows. Toutefois, avant de créer et déployer des applications pour des ordinateurs Mac gérés par Configuration Manager, tenez compte des points suivants :  

-   Pour pouvoir déployer des packages d’application Mac sur des ordinateurs Mac, vous devez vous servir de l’outil **CMAppUtil** sur un ordinateur Mac pour convertir ces applications dans un format lisible par Configuration Manager.  

-   Configuration Manager ne prend pas en charge le déploiement d’applications Mac vers les utilisateurs ; ces déploiements doivent être dirigés vers un appareil. De même, pour les déploiements d’applications Mac, Configuration Manager ne prend pas en charge l’option **Prédéployer des logiciels sur le périphérique principal de l’utilisateur** proposée sur la page **Paramètres de déploiement** de l’Assistant Déploiement logiciel.  

-   Les applications Mac prennent en charge les déploiements simulés.  

-   Vous ne pouvez pas déployer d'applications sur des ordinateurs Mac dont l'objet est **Disponible**.  

-   L'option d'envoi de paquets de mise en éveil lors du déploiement de logiciels n'est pas prise en charge pour les ordinateurs Mac.  

-   Les ordinateurs Mac ne prennent pas en charge le service de transfert intelligent en arrière-plan (BITS) pour le téléchargement de contenu d'application. Si le téléchargement d'une application échoue, il redémarre entièrement.  

-   Configuration Manager ne prend pas en charge les conditions globales lorsque vous créez des types de déploiement pour ordinateurs Mac.  

## <a name="steps-to-create-and-deploy-an-application"></a>Procédure de création et de déploiement d'une application  
 Le tableau suivant présente la procédure, des détails et des informations complémentaires pour créer et déployer des applications pour ordinateurs Mac.  

|Étape|Détails|  
|----------|-------------|  
|Étape 1 : préparer les applications Mac pour Configuration Manager|Pour pouvoir créer des applications Configuration Manager à partir de packages logiciels Mac, vous devez vous servir de l’outil **CMAppUtil** sur un ordinateur Mac pour convertir le logiciel Mac en fichier **.cmmac** Configuration Manager.|  
|Étape 2 : créer une application Configuration Manager contenant le logiciel Mac|Utilisez l'Assistant Création d'une application pour créer une application pour le logiciel Mac.|  
|Étape 3 : créer un type de déploiement pour l’application Mac|Cette étape n'est nécessaire que si vous n'avez pas importé automatiquement ces informations à partir de l'application.|  
|Étape 4 : déployer l’application Mac|Utilisez l'Assistant Déploiement logiciel pour déployer l'application sur les ordinateurs Mac.|  
|Étape 5 : contrôler le déploiement de l’application Mac|Assurez-vous que les déploiements d'application sur les ordinateurs Mac aboutissent.|  

## <a name="supplemental-procedures-to-create-and-deploy-applications-for-mac-computers"></a>Procédures supplémentaires de création et de déploiement d’applications pour ordinateurs Mac  
 Les procédures suivantes permettent de créer et déployer des applications pour les ordinateurs Mac gérés par Configuration Manager.  

###  <a name="step-1-prepare-mac-applications-for-configuration-manager"></a>Étape 1 : préparer les applications Mac pour Configuration Manager  
 La procédure à suivre pour créer des applications Configuration Manager et les déployer sur des ordinateurs Mac est similaire à la procédure de déploiement applicable aux ordinateurs Windows. Toutefois, avant de créer des applications Configuration Manager contenant des types de déploiements Mac, vous devez préparer les applications à l’aide de l’outil **CMAppUtil**. Cet outil est téléchargé en même temps que les fichiers d'installation du client Mac. L'outil **CMAppUtil** peut recueillir des informations sur l'application, notamment des données de détection issues des packages Mac suivants :  

-   Image disque Apple (.dmg)  

-   Fichier métapaquet (.mpkg)  

-   Paquet d'installation Mac OS X (.pkg)  

-   Application Mac OS X (.app)  

Après avoir recueilli les informations sur l'application, **CMAppUtil** crée un fichier avec l'extension **.cmmac**. Ce fichier contient les fichiers d'installation du logiciel Mac et des informations sur les méthodes de détection pouvant être utilisées pour déterminer si l'application est déjà installée. **CMAppUtil** peut également traiter des fichiers **.dmg** qui contiennent plusieurs applications Mac et créer différents types de déploiement pour chaque application.  

1.  Copiez le package d'installation du logiciel Mac dans le dossier de l'ordinateur Mac dans lequel vous avez extrait le contenu du fichier **macclient.dmg** que vous avez téléchargé à partir du Centre de téléchargement Microsoft.  

2.  Sur ce même ordinateur Mac, ouvrez une fenêtre de terminal et accédez au dossier dans lequel vous avez extrait le contenu du fichier **macclient.dmg** .  

3.  Accédez au dossier **Outils** , puis entrez la ligne de commande suivante :  

     **./CMAppUtil** *<propriétés\>*  

     Par exemple, supposez que vous souhaitez convertir le contenu d'un fichier image de disque Apple nommé **MySoftware.dmg** stocké dans le dossier Desktop de l'utilisateur en fichier **cmmac** dans le même dossier et que vous souhaitez créer des fichiers **cmmac** pour toutes les applications se trouvant dans le fichier image de disque. Pour cela, utilisez la ligne de commande suivante :  

     **./CMApputil –c /Users/** *<nom_utilisateur\>* **/Desktop/MySoftware.dmg -o /Users/** *<nom_utilisateur\>* **/Desktop -a**  

    > [!NOTE]  
    >  Le nom de l'application ne doit pas dépasser 128 caractères.  

     Pour configurer les options de **CMAppUtil**, utilisez les propriétés de ligne de commande décrites dans le tableau suivant :  

    |Propriété|Plus d'informations|  
    |--------------|----------------------|  
    |**-h**|Affiche les propriétés de ligne de commande disponibles.|  
    |**-r**|Génère **detection.xml** du fichier **.cmmac** fourni à **stdout**. La sortie contient les paramètres de détection et la version de **CMAppUtil** qui a été utilisée pour créer le fichier **.cmmac** .|  
    |**-c**|Permet de spécifier le fichier source à convertir.|  
    |**-o**|Cette propriété doit être utilisée conjointement avec la propriété –c pour spécifier le chemin de sortie.|  
    |**-a**|Utilisez cette propriété conjointement avec la propriété –c et le fichier image de disque (**.dmg**) pour créer automatiquement des fichiers .cmmac pour l'ensemble des applications et des packages se trouvant dans le fichier image de disque.|  
    |**-s**|Ignore la génération de **detection.xml** si aucun paramètre de détection n'est trouvé et force la création du fichier **.cmmac** sans le fichier **detection.xml** .|  
    |**-v**|Affiche une sortie plus détaillée de l'outil **CMAppUtil** , ainsi que des informations de diagnostic.|  

4.  Assurez-vous que le fichier **.cmmac** a été créé dans le dossier de sortie que vous avez spécifié.  

###  <a name="create-a-configuration-manager-application-that-contains-the-mac-software"></a>créer une application Configuration Manager contenant le logiciel Mac  

La procédure suivante permet de créer une application pour les ordinateurs Mac gérés par Configuration Manager.  

1.  Dans la console Configuration Manager, cliquez sur **Bibliothèque de logiciels** > **Gestion des applications** > **Applications**.  

3.  Dans l'onglet **Accueil** , dans le groupe **Créer** , cliquez sur **Créer une application**.  

4.  Sur la page **Général,** de l'Assistant Création d'une application, sélectionnez **Détecter automatiquement les informations de cette application à partir des fichiers d'installation**.  

    > [!NOTE]  
    >  Sélectionnez **Spécifier manuellement les informations de l'application** si vous souhaitez spécifier vous-même des informations sur l'application. Pour plus d’informations sur la façon de spécifier manuellement les informations, consultez [Comment créer des applications avec System Center Configuration Manager](../../apps/deploy-use/create-applications.md).  

5.  Dans la liste déroulante **Type** , sélectionnez **Mac OS X**.  

6.  Dans le champ **Emplacement**, spécifiez le chemin UNC au format *\\\\<serveur\>\\<partage\>\\<nom_fichier\>* du fichier d’installation de l’application pour Mac (fichier **.cmmac**) qui détectera les informations de l’application. Sinon, cliquez sur **Parcourir** pour rechercher et spécifier l'emplacement du fichier d'installation.  

    > [!NOTE]  
    >  Vous devez avoir accès au chemin d'accès UNC qui contient l'application.  

7.  Cliquez sur **Suivant**.  

8.  Sur la page **Importer des informations** de l'Assistant Création d'une application, examinez les informations qui ont été importées. Si nécessaire, vous pouvez cliquer sur **Précédent** pour revenir en arrière et corriger les erreurs éventuelles. Cliquez sur **Suivant** pour continuer.  

9. Sur la page **Informations générales** de l’Assistant Création d’une application, spécifiez des informations sur l’application, telles que le nom d’application, des commentaires, la version et éventuellement une référence qui vous aidera à retrouver l’application dans la console Configuration Manager.  

    > [!NOTE]  
    >  Certaines informations de l'application peuvent déjà être présentes sur cette page si elles ont été obtenues préalablement à partir des fichiers d'installation de l'application.  

10. Cliquez sur **Suivant**, examinez les informations sur l'application figurant sur la page **Résumé** , puis suivez toutes les étapes de l'Assistant Création d'une application.  

11. La nouvelle application s’affiche dans le nœud **Applications** de la console Configuration Manager.  

###  <a name="step-3-create-a-deployment-type-for-the-mac-application"></a>Étape 3 : créer un type de déploiement pour l’application Mac  
 La procédure suivante permet de créer un type de déploiement pour les ordinateurs Mac gérés par Configuration Manager.  

> [!NOTE]  
>  Si vous avez importé automatiquement des informations sur l'application dans l'Assistant Création d'une application, il se peut qu'un type de déploiement ait déjà été créé pour l'application.  

1.  Dans la console Configuration Manager, cliquez sur **Bibliothèque de logiciels** > **Gestion des applications** > **Applications**.  

3.  Sélectionnez une application puis, sous l'onglet **Accueil** , dans le groupe **Application** , cliquez sur **Créer un type de déploiement** pour créer un nouveau type de déploiement pour cette application.  

    > [!NOTE]  
    >  Vous pouvez également démarrer l’Assistant Création d’un type de déploiement à partir de l’Assistant Création d’une application et sous l’onglet **Types de déploiement** de la boîte de dialogue *Propriétés de***<nom_application\>**.  

4.  Sur la page **Général** de l'Assistant Création d'un type de déploiement, dans la liste déroulante **Type** , sélectionnez **Mac OS X**.  

5.  Dans le champ **Emplacement**, spécifiez le chemin UNC au format \\\\<serveur\>\\<partage\>\\<nom_fichier\> du fichier d’installation de l’application (fichier **.cmmac**). Sinon, cliquez sur **Parcourir** pour rechercher et spécifier l'emplacement du fichier d'installation.  

    > [!NOTE]  
    >  Vous devez avoir accès au chemin d'accès UNC qui contient l'application.  

6.  Cliquez sur **Suivant**.  

7.  Sur la page **Importer des informations** de l' **Assistant Création d'un type de déploiement**, examinez les informations qui ont été importées. Si nécessaire, cliquez sur **Précédent** pour revenir en arrière et corriger les erreurs éventuelles. Cliquez sur Suivant pour continuer.  

8.  Sur la page **Informations générales** de l' **Assistant Création d'un type de déploiement**, spécifiez des informations sur l'application, telles que le nom de l'application, des commentaires et les langues dans lesquelles le type de déploiement est disponible.  

    > [!NOTE]  
    >  Certaines des informations sur le type de déploiement peuvent déjà être présentes sur cette page si elles ont été obtenues préalablement à partir des fichiers d'installation de l'application.  

9. Cliquez sur **Suivant**.  

10. Sur la page **Spécifications** de l'Assistant Création d'un type de déploiement, vous pouvez spécifier les conditions à remplir pour que le type de déploiement puisse être installé sur des ordinateurs Mac.  

11. Cliquez sur **Ajouter** pour ouvrir la boîte de dialogue **Créer une spécification** , puis ajoutez une nouvelle spécification.  

    > [!NOTE]  
    >  Vous pouvez également ajouter de nouvelles spécifications sous l’onglet **Spécifications** de la boîte de dialogue *Propriétés de***<nom_type_déploiement\>**.  

12. Dans la liste déroulante **Catégorie** , indiquez que cette spécification concerne un périphérique.  

13. Dans la liste déroulante **Condition** , sélectionnez la condition que vous souhaitez utiliser pour déterminer si l'ordinateur Mac répond aux spécifications de l'installation. Le contenu de cette liste varie en fonction de la catégorie sélectionnée.  

14. Dans la liste déroulante **Opérateur** , choisissez l'opérateur qui sera utilisé pour comparer la condition sélectionnée à la valeur spécifiée, afin d'évaluer si l'utilisateur ou le périphérique répond aux spécifications de l'installation. Les opérateurs disponibles varient en fonction de la condition sélectionnée.  

15. Dans le champ **Valeur** , indiquez les valeurs qui seront utilisées avec l'opérateur et la condition sélectionnés si l'utilisateur ou le périphérique respecte les exigences d'installation.  Les valeurs disponibles varient en fonction de la condition et de l'opérateur sélectionnés.  

16. Cliquez sur **OK** pour enregistrer la règle de spécification et fermer la boîte de dialogue **Créer une spécification** .  

17. Sur la page **Spécifications** de l' **Assistant Création d'un type de déploiement**, cliquez sur **Suivant**.  

18. Sur la page **Résumé** de l' **Assistant Création d'un type de déploiement**, passez en revue les actions que doit prendre l'Assistant.  Si nécessaire, cliquez sur **Précédent** pour revenir en arrière et modifier les paramètres du type de déploiement. Cliquez sur **Suivant** pour créer le type de déploiement.  

19. Après la fermeture de la page **Progression**, passez en revue les actions qui ont été prises, puis cliquez sur **Fermer** pour terminer l’**Assistant Création d’un type de déploiement**.  

20. Si vous avez démarré cet Assistant à partir de l’**Assistant Création d’une application**, vous revenez à la page **Types de déploiement**.  

###  <a name="deploy-the-mac-application"></a>déployer l'application Mac  
 La procédure à suivre pour déployer une application sur des ordinateurs Mac est identique à celle applicable aux ordinateurs Windows, à l'exception des points suivants :  

-   Le déploiement d'applications à destination des utilisateurs n'est pas pris en charge.  

-   Les déploiements dont l'objet est **Disponible** ne sont pas pris en charge.  

-   L'option **Prédéployer des logiciels sur le périphérique principal de l'utilisateur** de la page **Paramètres de déploiement** de l'Assistant Déploiement logiciel n'est pas prise en charge.  

-   Les ordinateurs Mac ne prenant pas en charge le Centre logiciel, le paramètre **Notifications à l'utilisateur** de la page **Expérience utilisateur** de l'Assistant Déploiement logiciel est ignoré.  

-   L'option d'envoi de paquets de mise en éveil lors du déploiement de logiciels n'est pas prise en charge pour les ordinateurs Mac.  

> [!NOTE]  
>  Vous pouvez créer un regroupement contenant uniquement des ordinateurs Mac. Pour ce faire, créez un regroupement qui utilise une règle de requête et utilisez l’exemple de requête WQL figurant dans la rubrique [Guide pratique pour créer des requêtes](../../core/servers/manage/create-queries.md).  

 Pour plus d’informations, consultez [Déployer des applications](../../apps/deploy-use/deploy-applications.md).  

###  <a name="step-5-monitor-the-deployment-of-the-mac-application"></a>Étape 5 : contrôler le déploiement de l'application Mac  
 Pour contrôler les déploiements d'applications sur les ordinateurs Mac, vous pouvez suivre la même procédure que celle applicable aux déploiements d'applications sur les ordinateurs Windows.  

 Pour plus d’informations, consultez [Surveiller des applications](/sccm/apps/deploy-use/monitor-applications-from-the-console).  



<!--HONumber=Dec16_HO3-->


