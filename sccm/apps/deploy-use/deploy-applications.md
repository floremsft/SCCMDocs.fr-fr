---
title: "Déployer des applications | System Center Configuration Manager"
description: "Créez un type de déploiement ou simulez le déploiement d’une application à l’aide de System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2629c376-ec43-4f0e-a78b-4223cc9302bf
caps.latest.revision: 10
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: e608bcbadc82487018bb29c5e05660275d8fa275


---
# <a name="deploy-applications-with-system-center-configuration-manager"></a>Déployer des applications avec System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*



 Avant de pouvoir déployer une application System Center Configuration Manager, vous devez créer au moins un type de déploiement pour cette application. Pour plus d’informations sur la création d’applications et de types de déploiements, consultez [Créer des applications](../../apps/deploy-use/create-applications.md).  

> [!IMPORTANT]  
>  Vous pouvez déployer (c'est-à-dire installer ou désinstaller) les applications requises, mais pas les packages ni les mises à jour logicielles. Les appareils mobiles ne prennent pas en charge les simulations de déploiement.  
>   
>  De plus, les appareils mobiles ne prennent pas en charge les paramètres d'expérience utilisateur et de planification dans l'Assistant Déploiement logiciel.  

 Vous pouvez aussi simuler un déploiement d’application. Ce type de déploiement teste l’applicabilité du déploiement d’une application sur des ordinateurs, sans installation ou désinstallation de l’application. Un déploiement simulé évalue la méthode de détection, les spécifications et les dépendances d'un type de déploiement, et génère un rapport contenant les résultats dans le nœud **Déploiements** de l'espace de travail **Surveillance** . Pour plus d’informations, consultez [Simuler des déploiements d’applications](../../apps/deploy-use/simulate-application-deployments.md).  

## <a name="deploy-an-application"></a>Déployer une application  

1.  Dans la console Configuration Manager, cliquez sur **Bibliothèque de logiciels** > **Gestion des applications** > **Applications**.  

3.  Dans la liste **Applications** , sélectionnez l'application à déployer. Ensuite, sous l’onglet **Accueil** , dans le groupe **Déploiement** , cliquez sur **Déployer**.  

4.  Dans la page **Général** de l’Assistant Déploiement logiciel, spécifiez les informations suivantes :  

    -   **Logiciel** : indique l'application à déployer. Vous pouvez cliquer sur **Parcourir** pour sélectionner une autre application.  

    -   **Regroupement** : cliquez sur **Parcourir** pour sélectionner le regroupement vers lequel vous souhaitez déployer l'application.  

    -   **Utiliser des groupes de points de distribution par défaut associés à ce regroupement** : sélectionnez cette option si vous souhaitez stocker le contenu de l'application dans le groupe de points de distribution par défaut du regroupement. Si aucun groupe de points de distribution n'a été associé au regroupement sélectionné, cette option n'est pas disponible.  

    -   **Distribuer automatiquement le contenu pour les dépendances** : si cette option est activée et que l'un des types de déploiement de l'application contient des dépendances, alors le contenu de l'application dépendante sera également envoyé aux points de distribution.  

        > [!IMPORTANT]  
        >  Si vous mettez à jour l'application dépendante après le déploiement de l'application principale, les nouveaux contenus de la dépendance ne seront pas distribués automatiquement.  

    -   **Commentaires (champ facultatif)** : si vous le souhaitez, entrez une description de ce déploiement.  

5.  Dans la page **Contenu**, cliquez sur **Ajouter** pour ajouter le contenu associé à ce déploiement aux points de distribution ou aux groupes de points de distribution. Si vous avez sélectionné Utiliser des groupes de points de distribution par défaut associés à ce regroupement dans la page **Général**, cette option est automatiquement renseignée et peut uniquement être modifiée par un membre du rôle de sécurité **Administrateur d’application** .  

6.  Cliquez sur **Suivant**.  

7.  Dans la page **Paramètres de déploiement** de l’Assistant Déploiement logiciel, spécifiez les informations suivantes :  

    -   **Action** – Dans la liste déroulante, choisissez si ce déploiement est destiné à **Installer** ou à **Désinstaller** l'application.  

        > [!NOTE]  
        >  Si une application est déployée deux fois sur un appareil, une fois avec l'action **Installer** et une autre fois avec l'action **Désinstaller**, le déploiement de l'application avec l'action **Installer** aura la priorité.  
        >   
        >  Il n'est pas possible de modifier l'action d'un déploiement après sa création.  

    -   **Objet** – Dans la liste déroulante, choisissez l'une des options suivantes :  

        -   **Disponible** : si l’application est déployée sur un utilisateur, celui-ci peut voir l’application publiée dans le Centre logiciel et il peut l’installer à la demande.  

        -   **Obligatoire** : l'application est déployée automatiquement, selon le calendrier configuré. Un utilisateur peut toutefois suivre l’état du déploiement de l’application (s’il n’est pas masqué) et installer l’application avant l’échéance à partir du Centre logiciel.  

            > [!NOTE]  
            >  Lorsque l'action de déploiement est définie sur **Désinstaller**, l'objet du déploiement est automatiquement défini sur **Obligatoire** et ne peut plus être modifié.  

    -   **Déployer automatiquement en fonction du calendrier, qu'un utilisateur soit connecté ou non** : si le déploiement a pour cible un utilisateur, sélectionnez cette option afin de déployer l'application sur les appareils principaux de l'utilisateur. Ce paramètre ne nécessite pas que l'utilisateur se connecter avant que déploiement ne s'exécute. Ne sélectionnez pas cette option si l'utilisateur doit fournir une entrée pour terminer l'installation. Cette option est disponible uniquement lorsque l'objet du déploiement est **Obligatoire**.  

    -   **Envoyer des paquets de mise en éveil** : si l'objet du déploiement est défini sur **Obligatoire** et que cette option est sélectionnée, un paquet de mise en éveil est envoyé aux ordinateurs avant l'installation du déploiement, afin de sortir les ordinateurs de la veille à l'échéance de l'installation. Pour que vous puissiez utiliser cette option, les ordinateurs et les réseaux doivent être configurés pour utiliser l'éveil par appel réseau.  

    -   **Autoriser les clients avec une connexion Internet facturée à l'usage à télécharger le contenu une fois l'échéance d'installation atteinte, ce qui peut entraîner des frais supplémentaires** : cette option est disponible uniquement pour les déploiements dont l'objet est **Obligatoire**.  

    -   **Exiger l'approbation de l'administrateur si des utilisateurs demandent cette application** – Si cette option est sélectionnée, l'administrateur doit approuver toutes les requêtes d'utilisateur pour l'application avant qu'elle puisse être installée. Cette option n'est pas disponible lorsque l'objet du déploiement est **Obligatoire** , ni lorsque l'application est déployée sur un regroupement d'appareils.  

        > [!NOTE]  
        >  Les demandes d'approbation d'application sont affichées dans le nœud **Demandes d'approbation** , sous **Gestion d'applications** dans l'espace de travail **Bibliothèque de logiciels** . Si une demande ne reçoit pas d'approbation dans les 45 jours, elle est supprimée. En outre, la réinstallation du client Configuration Manager pourrait annuler des demandes d’approbation en attente.  

    -   **Mettre automatiquement à niveau toutes les versions remplacées de cette application** – Si cette option est sélectionnée, toutes les versions remplacées de l'application seront mises à niveau avec l'application de remplacement.  

8.  Dans la page **Planification** de l’Assistant Déploiement logiciel, configurez le moment où cette application sera déployée ou mise à la disposition des appareils clients.  
    Les options de cette page pourront différer selon si l'action de déploiement est définie sur **Disponible** ou sur **Obligatoire**.  

9. Si l'application que vous déployez remplace une autre application, vous pouvez définir le moment de réception de la nouvelle application comme échéance d'installation. Pour cela, utilisez le paramètre **Échéance d’installation** pour mettre à niveau les utilisateurs ou les appareils avec une application remplacée.  

10. Dans la page **Expérience utilisateur** de l’Assistant Déploiement logiciel, spécifiez des informations sur l’interaction que les utilisateurs peuvent avoir avec l’installation de l’application.
    Lorsque vous déployez des applications sur des appareils Windows Embedded dont le filtre d'écriture est activé, vous pouvez choisir d'installer l'application sur un segment de recouvrement temporaire puis de valider les modifications ultérieurement, ou de valider les modifications à l'échéance de l'installation ou au cours d'une fenêtre de maintenance. Lorsque vous validez des modifications à l'échéance de l'installation ou au cours d'une fenêtre de maintenance, un redémarrage est requis et les modifications sont conservées sur l'appareil.  
   > [!NOTE]  
   >  Lorsque vous déployez une application sur un appareil Windows Embedded, assurez-vous que l'appareil fait partie des membres d'un regroupement pour lequel une fenêtre de maintenance a été configurée. Pour plus d’informations sur l’utilisation de fenêtres de maintenance pendant le déploiement d’applications sur des appareils Windows Embedded, consultez [Créer des applications Windows Embedded](../../apps/get-started/creating-windows-embedded-applications.md).  
   >  Les options **Installation du logiciel** et **Redémarrage du système (si nécessaire pour terminer l'installation)** ne sont pas utilisées si l'objet du déploiement est défini sur **Disponible**. Vous pouvez également configurer le niveau de notification qu'un utilisateur peut voir lorsque l'application est installée.  
11. Dans la page **Alertes** de l’Assistant Déploiement logiciel, configurez comment Configuration Manager et System Center Operations Manager génèrent des alertes pour ce déploiement. Vous pouvez configurer des seuils pour les alertes de rapport et désactiver les rapports pendant la durée du déploiement.  

12. (Pour les applications iOS uniquement) - Dans la page **Stratégies de configuration des applications**, cliquez sur **Nouveau** pour associer ce déploiement à une stratégie de configuration d’application iOS (si vous en avez créé une). Pour plus d’informations sur ce type de stratégie, consultez [Configurer des applications iOS avec des stratégies de configuration des applications](../../apps/deploy-use/configure-ios-apps-with-app-configuration-policies.md).  

13. Dans la page **Résumé** de l’Assistant Déploiement logiciel, vérifiez les actions qui seront effectuées dans le cadre du déploiement, puis cliquez sur **Suivant** pour terminer l’Assistant.  

 Le nouveau déploiement sera affiché dans la liste **Déploiements** du nœud **Déploiements** de l'espace de travail **Surveillance** . Vous pouvez modifier les propriétés de ce déploiement ou le supprimer de l'onglet **Déploiements** du volet Détail de l'application.  

## <a name="delete-an-application-deployment"></a>Supprimer le déploiement d’une application  

1.  Dans la console Configuration Manager, cliquez sur **Bibliothèque de logiciels** > **Gestion des applications** > **Applications**.  

3.  Dans la liste **Applications** , sélectionnez l'application dont vous souhaitez supprimer le déploiement.  

4.  Sous l’onglet **Déploiements** de la liste *<nom_application\>*, sélectionnez le déploiement d’application à supprimer. Puis, sous l'onglet **Déploiement** , dans le groupe **Déploiement** , cliquez sur **Supprimer**.  

 Lorsque vous supprimez un déploiement d'application, les instances déjà installées de l'application ne sont pas supprimées. Pour supprimer ces applications, vous devez déployer l'application sur des ordinateurs avec l'action **Désinstaller**. Si vous supprimez un déploiement d’application ou que vous retirez une ressource du regroupement sur lequel le déploiement a lieu, l’application ne sera plus visible dans le Centre logiciel.  



<!--HONumber=Nov16_HO1-->


