---
title: "Gérer les séquences de tâches pour automatiser des tâches | Microsoft Docs"
description: "Vous pouvez créer, modifier, déployer, importer et exporter des séquences de tâches pour les gérer dans votre environnement System Center Configuration Manager."
ms.custom: na
ms.date: 03/24/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a1f099f1-e9b5-4189-88b3-f53e3b4e4add
caps.latest.revision: 10
author: Dougeby
ms.author: dougeby
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: dab5da5a4b5dfb3606a8a6bd0c70a0b21923fff9
ms.openlocfilehash: 113fa73bf0bd1b3b8a4754eb1e96549c520d7995
ms.lasthandoff: 03/27/2017


---
# <a name="manage-task-sequences-to-automate-tasks-in-system-center-configuration-manager"></a>Gérer les séquences de tâches pour automatiser des tâches dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Utilisez des séquences de tâches pour automatiser des étapes dans votre environnement System Center Configuration Manager. Ces étapes peuvent déployer une image du système d’exploitation sur un ordinateur de destination, créer et capturer une image du système d’exploitation à partir d’un ensemble de fichiers d’installation de système d’exploitation, et capturer et restaurer des informations d’état utilisateur. Les séquences de tâches sont affichées dans la console Configuration Manager, dans **Bibliothèque de logiciels** > **Systèmes d’exploitation** > **Séquence de tâches**. Le nœud **Séquence de tâches**, contenant les sous-dossiers que vous créez, est répliqué dans toute la hiérarchie Configuration Manager. Pour plus d’informations sur la planification, consultez [Considérations relatives à la planification de l’automatisation des tâches](../plan-design/planning-considerations-for-automating-tasks.md).  

 Aidez-vous des informations des sections suivantes pour gérer vos séquences de tâches.

##  <a name="BKMK_CreateTaskSequence"></a> Créer des séquences de tâches  
 Créez des séquences de tâches à l'aide de l'Assistant Création d'une séquence de tâches. Cet Assistant peut créer les types de séquences de tâches suivants :  

|Type de séquence de tâches|Plus d'informations|  
|------------------------|----------------------|  
|[Séquence de tâches pour installer un système d’exploitation](create-a-task-sequence-to-install-an-operating-system.md)|Ce type de séquence de tâches crée les étapes nécessaires pour installer un système d’exploitation, ainsi que l’option pour migrer des données utilisateur, inclure des mises à jour logicielles et installer des applications.|  
|[Séquence de tâches pour mettre à niveau un système d’exploitation](create-a-task-sequence-to-upgrade-an-operating-system.md)|Ce type de séquence de tâches crée les étapes nécessaires pour mettre à niveau un système d’exploitation, ainsi que l’option pour inclure des mises à jour logicielles et installer des applications.|  
|[Séquence de tâches pour capturer un système d’exploitation](create-a-task-sequence-to-capture-an-operating-system.md)|Ce type de séquence de tâches crée les étapes nécessaires pour générer et capturer un système d’exploitation à partir d’un ordinateur de référence. Vous pouvez inclure des mises à jour logicielles et installer des applications sur l’ordinateur de référence avant que l’image ne soit capturée.|  
|[Séquence de tâches pour capturer et restaurer l’état utilisateur](create-a-task-sequence-to-capture-and-restore-user-state.md)|Cette séquence de tâches fournit les étapes à ajouter à une séquence de tâches pour capturer et restaurer des données d’état utilisateur.|  
|[Séquence de tâches pour gérer des disques durs virtuels](use-a-task-sequence-to-manage-virtual-hard-disks.md)|Ce type de séquence de tâches contient les étapes pour créer un disque dur virtuel, notamment pour installer un système d’exploitation et des applications que vous pouvez publier dans System Center Virtual Machine Manager (VMM) à partir de la console Configuration Manager.|  
|[Séquence de tâches personnalisée](create-a-custom-task-sequence.md)|Ce type de séquence de tâches n’ajoute aucune étape à la séquence de tâches. Vous devez modifier la séquence de tâches et ajouter des étapes à la séquence de tâches après sa création.|  

## <a name="return-to-previous-page-when-a-task-sequence-fails"></a>Revenir à la page précédente en cas d’échec d’une séquence de tâches
À partir de Configuration Manager version 1702, vous pouvez revenir à une page précédente quand vous exécutez une séquence de tâches qui échoue. Avant cette version, vous deviez redémarrer la séquence de tâches en cas d’échec. Par exemple, vous pouvez utiliser le bouton **Précédent** dans les scénarios suivants :

- Quand un ordinateur démarre dans Windows PE, la boîte de dialogue d’amorçage de la séquence de tâches peut s’afficher avant que la séquence de tâches ne soit disponible. Quand vous cliquez sur Suivant dans ce scénario, la dernière page de la séquence de tâches s’affiche avec un message indiquant qu’aucune séquence de tâches n’est disponible. À présent, vous pouvez cliquer sur **Précédent** pour relancer la recherche des séquences de tâches disponibles. Vous pouvez répéter ce processus jusqu’à ce que la séquence de tâches soit disponible.
- Quand vous exécutez une séquence de tâches, mais que les packages de contenu dépendants ne sont pas encore disponibles sur les points de distribution, la séquence de tâches échoue. Vous pouvez désormais distribuer le contenu manquant (s’il ne l’a pas encore été) ou attendre qu’il soit disponible sur les points de distribution, puis cliquer sur **Précédent** pour que la séquence de tâches recherche une nouvelle fois le contenu.

##  <a name="BKMK_ModifyTaskSequence"></a> Modifier une séquence de tâches  
 Vous pouvez modifier une séquence de tâches en ajoutant ou en supprimant des étapes ou des groupes de séquence de tâches, ou bien en modifiant l'ordre des étapes. Pour modifier une séquence de tâches existante, procédez comme suit.  

> [!IMPORTANT]  
>  Lorsque vous modifiez une séquence de tâches qui avait été créée à l'aide de l'Assistant Création d'une séquence de tâches, le nom de l'étape peut être l'action de l'étape ou le type de l'étape. Par exemple, vous pouvez voir une étape appelée « Partitionner le disque 0 », qui désigne l’action d’une étape de type [Formater et partitionner le disque](../understand/task-sequence-steps.md#BKMK_FormatandPartitionDisk). Toutes les étapes de séquence de tâches sont documentées par leur type, pas nécessairement par le nom de l'étape qui est affichée dans l'éditeur.  

#### <a name="to-edit-a-task-sequence"></a>Pour modifier une séquence de tâches  

1.  Dans la console Configuration Manager, cliquez sur **Bibliothèque de logiciels**.  

2.  Dans l'espace de travail **Bibliothèque de logiciels** , développez **Systèmes d'exploitation**, puis cliquez sur **Séquences de tâches**.  

3.  Dans la liste **Séquence de tâches** , sélectionnez la séquence de tâches que vous souhaitez modifier.  

4.  Sous l'onglet **Accueil** , dans le groupe **Séquence de tâches** , cliquez sur **Modifier**, puis effectuez l'une des opérations suivantes :  

    -   Pour ajouter une étape de séquence de tâches, cliquez sur **Ajouter**, sélectionnez le type d'étape, puis cliquez sur la séquence de tâches à ajouter. Par exemple, pour ajouter l'étape Exécuter la ligne de commande, cliquez sur **Ajouter**, sélectionnez **Général**, puis cliquez sur **Exécuter la ligne de commande**.  

         Pour obtenir une liste de toutes les étapes de séquence de tâches et leur type, consultez le tableau qui suit cette procédure.  

    -   Pour ajouter un groupe à la séquence de tâches, cliquez sur **Ajouter**, puis cliquez sur **Nouveau groupe**. Après avoir ajouté un groupe, vous pouvez ajouter des étapes au groupe.  

    -   Pour modifier l'ordre des étapes et des groupes de la séquence de tâches, sélectionnez l'étape ou le groupe que vous souhaitez réorganiser, puis utilisez les icônes **Déplacer l'élément vers le haut** ou **Déplacer l'élément vers le bas** . Vous pouvez déplacer une seule étape ou un seul groupe à la fois.  

    -   Pour supprimer une étape ou un groupe, sélectionnez l'étape ou le groupe, puis cliquez sur **Supprimer**.  

5.  Cliquez sur **OK** pour enregistrer les modifications.  

 Pour obtenir une liste des étapes de séquence de tâches disponibles, consultez [Étapes de séquence de tâches](../understand/task-sequence-steps.md).  

## <a name="configure-high-impact-task-sequence-settings"></a>Configurer des paramètres de séquence de tâches à fort impact
À partir de Configuration Manager version 1702, vous pouvez définir une séquence de tâches à fort impact et personnaliser les messages envoyés aux utilisateurs lorsqu’ils exécutent la séquence de tâches.

### <a name="set-a-task-sequence-as-a-high-impact-task-sequence"></a>Définir une séquence de tâches comme séquence de tâches à fort impact
Appliquez la procédure suivante pour définir une séquence de tâches à fort impact.
> [!NOTE]
> Toute séquence de tâches qui remplit certaines conditions est définie automatiquement comme séquence à fort impact. Pour plus d’informations, consultez [Paramètres pour gérer les déploiements à haut risque pour System Center Configuration Manager](http://docs.microsoft.com/sccm/protect/understand/settings-to-manage-high-risk-deployments).

1. Dans la console Configuration Manager, accédez à **Bibliothèque de logiciels** > **Systèmes d’exploitation** > **Séquences de tâches**.
2. Sélectionnez la séquence de tâches à modifier, puis cliquez sur **Propriétés**.
3. Sous l’onglet **Notification utilisateur**, sélectionnez **Il s’agit d’une séquence de tâches avec un impact élevé**.

### <a name="create-a-custom-notification-for-high-risk-deployments"></a>Créer une notification personnalisée pour les déploiements à haut risque
Utilisez la procédure suivante pour créer une notification personnalisée pour les déploiements à fort impact.
1. Dans la console Configuration Manager, accédez à **Bibliothèque de logiciels** > **Systèmes d’exploitation** > **Séquences de tâches**.
2. Sélectionnez la séquence de tâches à modifier, puis cliquez sur **Propriétés**.
3. Sous l’onglet **Notification utilisateur**, sélectionnez **Utiliser du texte personnalisé**.
>  [!NOTE]
>  Vous pouvez définir le texte de notification utilisateur uniquement quand **Il s’agit d’une séquence de tâches avec un impact élevé** est sélectionné.

4. Configurez les paramètres suivants (maximum 255 caractères pour chaque zone de texte) :

  **Texte du titre de la notification utilisateur** : spécifie le texte en bleu qui s’affiche sur la notification utilisateur du Centre logiciel. Par exemple, dans la notification utilisateur par défaut, cette section contient quelque chose comme « Confirmez que vous voulez mettre à niveau le système d’exploitation sur cet ordinateur ».

  **Texte du message de la notification utilisateur** : trois zones de texte fournissent le corps de la notification personnalisée. Toutes les zones de texte nécessitent la saisie d’un texte.
  - Première zone de texte : spécifie le corps principal du texte, contenant généralement des instructions destinées à l’utilisateur. Par exemple, dans la notification utilisateur par défaut, cette section contient quelque chose comme « La mise à niveau du système d’exploitation peut prendre un certain temps et entraîner plusieurs redémarrages de votre ordinateur ».
  - Deuxième zone de texte : spécifie le texte en gras dans le corps principal du texte. Par exemple, dans la notification utilisateur par défaut, cette section contient quelque chose comme « Cette mise à niveau sur place installe le nouveau système d’exploitation et migre automatiquement vos applications, vos données et vos paramètres ».
  - Troisième zone de texte : spécifie la dernière ligne de texte sous le texte en gras. Par exemple, dans la notification utilisateur par défaut, cette section contient quelque chose comme « Cliquez sur Installer pour commencer. Sinon, cliquez sur Annuler. ».   

  Supposons que vous configurez la notification personnalisée suivante dans les propriétés.

    ![Notification personnalisée pour une séquence de tâches](..\media\user-notification.png)

    Le message de notification suivant s’affiche quand l’utilisateur final ouvre l’installation à partir du Centre logiciel.

    ![Notification personnalisée pour une séquence de tâches](..\media\user-notification-enduser.png)

### <a name="configure-software-center-properties"></a>Configurer les propriétés du Centre logiciel
Appliquez la procédure suivante pour configurer les détails de la séquence de tâches affichés dans le Centre logiciel. Ces détails sont fournis uniquement à titre d’informations.  
1. Dans la console Configuration Manager, accédez à **Bibliothèque de logiciels** > **Systèmes d’exploitation** > **Séquences de tâches**.
2. Sélectionnez la séquence de tâches à modifier, puis cliquez sur **Propriétés**.
3. Sous l’onglet **Général**, les paramètres suivants du Centre logiciel sont disponibles :
  - **Redémarrage requis** : indique à l’utilisateur si un redémarrage est nécessaire lors de l’installation.
  - **Taille du téléchargement (Mo)** : spécifie le nombre de mégaoctets affichés dans le Centre logiciel pour la séquence de tâches.  
  - **Durée d’exécution estimée (minutes)** : spécifie la durée d’exécution estimée, en minutes, affichée dans le Centre logiciel pour la séquence de tâches.

##  <a name="BKMK_DistributeTS"></a> Distribuer du contenu référencé par une séquence de tâches  
 Avant que les clients exécutent une séquence de tâches qui référence du contenu, vous devez distribuer ce contenu aux points de distribution. À tout moment, vous pouvez sélectionner la séquence de tâches et distribuer son contenu pour créer une nouvelle liste de packages de référence pour la distribution. Si vous apportez des modifications à la séquence de tâches avec du contenu mis à jour, vous devez redistribuer le contenu avant de le mettre à la disposition des clients. Pour distribuer le contenu qui est référencé par une séquence de tâches, procédez comme suit.  

#### <a name="to-distribute-referenced-content-to-distribution-points"></a>Pour distribuer le contenu référencé sur des points de distribution  

1.  Dans la console Configuration Manager, cliquez sur **Bibliothèque de logiciels**.  

2.  Dans l'espace de travail **Bibliothèque de logiciels** , développez **Systèmes d'exploitation**, puis cliquez sur **Séquences de tâches**.  

3.  Dans la liste **Séquence de tâches** , sélectionnez la séquence de tâches que vous souhaitez distribuer.  

4.  Sous l'onglet **Accueil** , dans le groupe **Déploiement** , cliquez sur **Distribuer du contenu** pour démarrer l'Assistant Distribuer du contenu.  

5.  Sur la page **Général** , vérifiez que la séquence de tâches correcte est sélectionnée pour la distribution, puis cliquez sur **Suivant**.  

6.  Sur la page **Contenu** , vérifiez le contenu à distribuer, tel que l'image de démarrage référencée par la séquence de tâches, puis cliquez sur **Suivant**.  

7.  Sur la page **Destination du contenu** , spécifiez les regroupements, le point de distribution ou le groupe de points de destination où vous souhaitez distribuer le contenu de séquence de tâches, puis cliquez sur **Suivant**.  

    > [!IMPORTANT]  
    >  Si la séquence de tâches que vous avez sélectionnée référence du contenu qui est déjà distribué sur un point de distribution spécifique, ce point de distribution n'est pas répertorié par l'Assistant.  

8.  Effectuez toutes les étapes de l'Assistant.  

 Vous pouvez préparer le contenu référencé dans la séquence de tâches. Configuration Manager crée un fichier de contenu compressé et préparé qui contient les fichiers, les dépendances associées et les métadonnées associées pour le contenu que vous sélectionnez. Vous pouvez ensuite importer manuellement le contenu au niveau d'un serveur de site, d'un site secondaire ou d'un point de distribution. Pour plus d’informations sur la façon de préparer des fichiers de contenu, consultez [Préparer du contenu](../../core/servers/deploy/configure/deploy-and-manage-content.md#a-namebkmkprestagea-use-prestaged-content).  

##  <a name="BKMK_DeployTS"></a> Déployer une séquence de tâches  
 Pour déployer une séquence de tâches sur les ordinateurs d'un regroupement, procédez comme suit.  

> [!WARNING]  
>  Vous pouvez gérer le comportement des déploiements de séquences de tâches à haut risque. Un déploiement à haut risque est un déploiement qui est installé automatiquement et qui est susceptible d'entraîner des résultats indésirables. Par exemple, une séquence de tâches avec comme objectif **Obligatoire** qui déploie un système d'exploitation est considérée comme un déploiement à haut risque. Pour plus d’informations, consultez [Paramètres de gestion des déploiements à haut risque](../../protect/understand/settings-to-manage-high-risk-deployments.md).  

> [!NOTE]  
>  Les messages d'état pour le déploiement d'une séquence de tâches sont affichés dans la fenêtre Message sur un site principal, mais ils ne sont pas affichés sur un site d'administration centrale.  

#### <a name="to-deploy-a-task-sequence"></a>Pour déployer une séquence de tâches  

1.  Dans la console Configuration Manager, cliquez sur **Bibliothèque de logiciels**.  

2.  Dans l'espace de travail **Bibliothèque de logiciels** , développez **Systèmes d'exploitation**, puis cliquez sur **Séquences de tâches**.  

3.  Dans la liste **Séquence de tâches** , sélectionnez la séquence de tâches que vous voulez déployer.  

4.  Dans l'onglet **Accueil** , dans le groupe **Déploiement** , cliquez sur **Déployer**.  

    > [!NOTE]  
    >  Si **Déployer** n'est pas disponible, la séquence de tâches a une référence qui n'est pas valide.  Corrigez la référence, puis tentez de déployer à nouveau la séquence de tâches.  

5.  Sur la page **Général** , spécifiez les informations suivantes, puis cliquez sur **Suivant**.  

    -   **Séquence de tâches**: Spécifiez la séquence de tâches que vous souhaitez déployer. Par défaut, cette zone affiche la séquence de tâches que vous avez sélectionnée.  

    -   **Regroupement**: Spécifiez le regroupement contenant les ordinateurs qui exécuteront la séquence de tâches.  

         Ne déployez pas de séquences de tâches qui installent des systèmes d'exploitation sur des regroupements inappropriés, tels que le regroupement **Tous les systèmes** . N'oubliez pas que le regroupement que vous sélectionnez contient uniquement les ordinateurs que vous souhaitez voir exécuter la séquence de tâches.  

        > [!NOTE]  
        >  Quand vous effectuez un déploiement à haut risque, par exemple un système d’exploitation, la fenêtre **Sélectionner un regroupement** affiche uniquement les regroupements personnalisés satisfaisant aux paramètres de vérification de déploiement configurés dans les propriétés du site. Les déploiements à haut risque sont toujours limités aux regroupements personnalisés, aux regroupements que vous créez et au regroupement **Ordinateurs inconnus** intégré. Quand vous créez un déploiement à haut risque, vous ne pouvez pas sélectionner un regroupement intégré tel que **Tous les systèmes**. Désactivez le paramètre **Masquer les regroupements avec un nombre de membres supérieur à la configuration de la taille minimale du site** pour afficher tous les regroupements personnalisés qui contiennent moins de clients que la taille maximale configurée. Pour plus d’informations, consultez [Paramètres de gestion des déploiements à haut risque](../../protect/understand/settings-to-manage-high-risk-deployments.md).  
        >   
        >  Les paramètres de vérification de déploiement sont basés sur l'appartenance actuelle du regroupement. Une fois que vous avez déployé la séquence de tâches, l'appartenance du regroupement n'est pas réévaluée pour les paramètres de déploiement à haut risque.  
        >   
        >  Supposons que vous affectez la valeur 100 à **Taille par défaut** et la valeur 1000 à **Taille maximale**. Quand vous créez un déploiement à haut risque, la fenêtre **Sélectionner un regroupement** affiche uniquement les regroupements qui contiennent moins de 100 clients. Si vous désactivez le paramètre **Masquer les regroupements avec un nombre de membres supérieur à la configuration de la taille minimale du site**, la fenêtre affiche les regroupements qui contiennent moins de 1 000 clients.  
        >   
        >  Quand vous sélectionnez un regroupement qui contient un rôle de site, ce qui suit s'applique :  
        >   
        >  -   Si le regroupement contient un serveur de système de site et que dans les paramètres de vérification de déploiement vous choisissez de bloquer les regroupements contenant des serveurs de système de site, une erreur se produit et vous ne pouvez pas continuer.  
        > -   Si le regroupement contient un serveur de système de site et que dans les paramètres de vérification de déploiement vous choisissez d'afficher un avertissement dans le cas où des regroupements contiennent des serveurs de système de site, si  le regroupement dépasse la valeur de taille par défaut, ou si le regroupement contient un serveur, l'Assistant Déploiement logiciel affiche un avertissement de risque élevé. Vous devez accepter de créer un déploiement à risque élevé et un message d'état d'audit est créé.  

    -   **Commentaires (facultatif) :**spécifiez des informations supplémentaires qui décrivent ce déploiement de la séquence de tâches.  

6.  Sur la page **Paramètres de déploiement** , spécifiez les informations suivantes, puis cliquez sur **Suivant**.  

    -   **Objet**: dans la liste déroulante, choisissez l’une des options suivantes :  

        -   **Disponible**: si la séquence de tâches est déployée auprès d’un utilisateur, celui-ci peut voir la séquence de tâches publiée dans le catalogue des applications et il peut la demander. Si la séquence de tâches est déployée sur un appareil, l'utilisateur peut la voir dans le Centre logiciel et l'installer à la demande.  

        -   **Obligatoire**: la séquence de tâches est déployée automatiquement, d’après le calendrier configuré. Un utilisateur peut toutefois suivre l'état du déploiement de la séquence de tâches (s'il n'est pas masqué) et installer cette séquence de tâches avant l'échéance, à l'aide du Centre logiciel.  

    -   **Déployer automatiquement selon le calendrier avec ou sans connexion de l’utilisateur**: cette option n’est pas disponible quand vous déployez une séquence de tâches.  

    -   **Envoyer des paquets de mise en éveil**: si l’objet du déploiement est défini sur **Obligatoire** et que cette option est sélectionnée, un paquet de mise en éveil est envoyé aux ordinateurs avant l’installation du déploiement, pour sortir les ordinateurs de la veille à l’échéance de l’installation. Pour que vous puissiez utiliser cette option, les ordinateurs et les réseaux doivent être configurés pour utiliser l'éveil par appel réseau.  

    -   **Autoriser les clients avec une connexion Internet facturée à l’usage à télécharger le contenu une fois l’échéance d’installation atteinte, ce qui peut entraîner des frais supplémentaires**: quand votre séquence de tâches installe une application mais ne déploie pas de système d’exploitation, vous pouvez spécifier s’il faut autoriser les clients à télécharger du contenu après l’échéance d’installation quand ils utilisent des connexions Internet facturées à l’usage. Les fournisseurs Internet facturent parfois en fonction de la quantité de données que vous envoyez et recevez lorsque vous utilisez une connexion Internet facturée à l'usage.  

        > [!NOTE]  
        >  L'utilisation d'une connexion Internet facturée à l'usage pourrait fonctionner avec les séquences de tâches qui ne déploient pas de système d'exploitation, mais cette possibilité n'est pas prise en charge.  

    -   **Exiger l’approbation de l’administrateur si des utilisateurs demandent cette application**: cette option n’est pas disponible quand vous déployez une séquence de tâches.  

    -   **Rendre disponible aux éléments suivants** : spécifiez si la séquence de tâches est disponible pour les clients Configuration Manager, les médias ou les environnements PXE.  

        > [!IMPORTANT]  
        >  Utilisez le paramètre **Média et environnement PXE uniquement (masqué)** pour les déploiements de séquence de tâches automatisés. Sélectionnez **Autoriser le déploiement du système d'exploitation de manière autonome** et définissez la variable SMSTSPreferredAdvertID à inclure dans le média, de sorte que l'ordinateur démarre automatiquement le déploiement sans l'intervention de l'utilisateur. Pour plus d’informations sur les variables de séquence de tâches, consultez [Variables intégrées de séquence de tâches](../understand/task-sequence-built-in-variables.md)  

7.  Sur la page **Planification** , spécifiez les informations suivantes, puis cliquez sur **Suivant**.  

    > [!IMPORTANT]  
    >  Quand un client Windows PE démarre à partir du média de démarrage ou de l'environnement PXE, il n'évalue pas les plannings de déploiement (heures de démarrage ou d'expiration ou échéance). Vous ne devez configurer des plannings de déploiements que sur les clients qui démarrent à partir du système d'exploitation Windows complet. Appliquez d'autres méthodes, telles que des fenêtres de maintenance, pour contrôler les séquences de tâches actives déployées sur les clients qui démarrent à partir de Windows PE.  

    -   **Planifier la disponibilité de ce déploiement**: spécifiez la date et l’heure auxquelles la séquence de tâches est disponible pour s’exécuter sur l’ordinateur de destination. Lorsque vous activez la case à cocher **UTC** , ce paramètre s'assure que la séquence de tâches est disponible pour plusieurs ordinateurs de destination en même temps plutôt qu'à des heures différentes, en fonction de l'heure locale sur les ordinateurs de destination.  

         Si l'heure de début est antérieure à l'heure requise, le client télécharge la séquence de tâches à l'heure de début que vous spécifiez.  

    -   **Planifier la disponibilité de ce déploiement**: spécifiez la date et l’heure d’expiration de la séquence de tâches sur l’ordinateur de destination. Lorsque vous activez la case à cocher **UTC** , ce paramètre s'assure que la séquence de tâches expire sur plusieurs ordinateurs de destination en même temps plutôt qu'à des heures différentes, en fonction de l'heure locale sur les ordinateurs de destination.  

    -   **Calendrier d’attribution**: spécifiez quand la séquence de tâches requise est exécutée sur l’ordinateur de destination. Vous pouvez ajouter plusieurs calendriers.  

         Vous pouvez spécifier la date et l'heure auxquelles le calendrier démarre, si la séquence de tâches s'exécute toutes les semaines, tous les mois ou à un intervalle personnalisé, et si la séquence de tâches s'exécute après un événement tel qu'une ouverture ou une fermeture de session sur l'ordinateur.  

        > [!NOTE]  
        >  Si vous planifiez une heure de début pour une séquence de tâches requise antérieure à la date et à l’heure auxquelles la séquence de tâches est disponible, le client Configuration Manager télécharge la séquence de tâches à l’heure de début planifiée, même si elle est disponible plus tôt.  

    -   **Comportement de réexécution**: spécifiez quand la séquence de tâches est réexécutée. Vous pouvez spécifier l'une des options suivantes.  

        -   **Ne jamais exécuter à nouveau un programme déployé**: la séquence de tâches n’est pas réexécutée sur le client si elle a été précédemment exécutée sur le client. La séquence de tâches ne se réexécute pas même si elle a échoué à l'origine ou si les fichiers de séquence de tâches ont été modifiés.  

        -   **Toujours exécuter à nouveau le programme**: la séquence de tâches est toujours réexécutée sur le client quand le déploiement est planifié, même si elle a été exécutée avec succès précédemment. Ce paramètre est particulièrement utile lorsque vous utilisez des déploiements périodiques dans lesquels la séquence de tâches est mise régulièrement à jour.  

            > [!IMPORTANT]  
            >  Même si cette option est définie par défaut, elle n'a aucun effet tant que vous n'attribuez pas un déploiement requis. Des déploiements disponibles peuvent toujours être réexécutés par un utilisateur.  

        -   **Exécuter à nouveau en cas d’échec de la tentative précédente**: la séquence de tâches est réexécutée quand le déploiement est planifié uniquement si son exécution a échoué précédemment. Ce paramètre est particulièrement utile pour les déploiements requis afin qu'ils réessaient automatiquement de s'exécuter conformément au calendrier d'attribution si la dernière tentative d'exécution a échoué.  

        -   Exécuter à nouveau en cas de réussite de la tentative précédente : la séquence de tâches est réexécutée uniquement si elle a déjà été exécutée correctement sur le client. Ce paramètre est utile lorsque vous utilisez des déploiements périodiques dans lesquels la séquence de tâches est mise régulièrement à jour, et chaque mise à jour requiert que la précédente mise à jour soit installée avec succès.  

        > [!NOTE]  
        >  Comme un utilisateur peut réexécuter un déploiement de séquence de tâches disponible, avant de déployer une séquence de tâches disponible dans un environnement produit, assurez-vous d'évaluer et de tester scrupuleusement ce qui se passe si un utilisateur réexécute la séquence de tâches plusieurs fois.  

8.  Sur la page **Expérience utilisateur** , spécifiez les informations suivantes, puis cliquez sur **Suivant**.  

    -   **Autoriser les utilisateurs à exécuter le programme indépendamment des attributions**: spécifiez si l’utilisateur est autorisé à exécuter une séquence de tâches obligatoire indépendamment des attributions de déploiement.  

    -   **Afficher la progression de la séquence de tâches** : spécifiez si le client Configuration Manager affiche la progression de la séquence de tâches.  

    -   **Installation du logiciel**: spécifiez si l’utilisateur est autorisé à installer le logiciel en dehors de fenêtres de maintenance configurées après l’heure planifiée.  

    -   **Redémarrage du système (si nécessaire pour terminer l’installation)**: spécifiez si l’utilisateur est autorisé à redémarrer l’ordinateur après une installation de logiciel en dehors d’une fenêtre de maintenance configurée après l’heure d’attribution.  

    -   **Autoriser la séquence de tâches à s’exécuter pour le client sur Internet** : spécifiez si la séquence de tâches est autorisée à s’exécuter sur un client basé sur Internet que Configuration Manager a détecté comme étant sur Internet. Les opérations qui installent le logiciel, tel qu'un système d'exploitation, ne sont pas prises en charge avec ce paramètre. Utilisez cette option uniquement pour les séquences de tâches basées sur des scripts génériques qui effectuent des opérations dans le système d'exploitation standard.  

9. Sur la page **Alertes** , spécifiez les paramètres d'alerte que vous souhaitez pour ce déploiement de séquence de tâches, puis cliquez sur **Suivant**.  

10. Sur la page **Points de distribution** , spécifiez les informations suivantes, puis cliquez sur **Suivant**.  

    -   **Options de déploiement**: spécifiez l’une des options suivantes :  

        > [!NOTE]  
        >  Lorsque vous utilisez la multidiffusion pour déployer un système d'exploitation, le contenu doit être téléchargé sur les ordinateurs de destination soit lorsque la séquence en a besoin, soit avant l'exécution de la séquence de tâches.  

        -   Demandez à ce que les clients téléchargent le contenu du point de distribution vers l'ordinateur de destination au moment où la séquence de tâches en a besoin.  

        -   Demandez à ce que les clients téléchargent l'intégralité du contenu du point de distribution vers l'ordinateur de destination avant l'exécution de la séquence de tâches. Cette option ne s'affiche pas si vous avez indiqué que la séquence de tâches est disponible dans l'environnement PXE et dans les déploiements de média de démarrage (voir la page **Paramètres de déploiement** ).  

        -   Demandez à ce que les clients exécutent le contenu à partir du point de distribution. Cette option est disponible uniquement lorsque tous les packages associés à la séquence de tâches sont configurés pour utiliser un partage de package sur le point de distribution. Pour que le contenu utilise un partage de package, consultez l'onglet **Accès aux données** dans les **Propriétés** de chaque package.  

    -   **Quand aucun point de distribution local n’est disponible, utiliser un point de distribution distant**: spécifiez si les clients peuvent utiliser les points de distribution qui se trouvent sur des réseaux lents et peu fiables pour télécharger le contenu exigé par la séquence de tâches.  

11. Effectuez toutes les étapes de l'Assistant.  

##  <a name="BKMK_ExportImport"></a> Exporter et importer des séquences de tâches  
 Vous pouvez exporter et importer des séquences de tâches avec ou sans leurs objets liés, tels qu'une image du système d'exploitation, une image de démarrage, un package de l'agent du client, un package de pilotes et des applications qui ont des dépendances.  

 Considérez les éléments suivants lorsque vous exportez et importez des séquences de tâches.  

-   Les mots de passe stockés dans la séquence de tâches ne sont pas exportés. Si vous exportez et importez une séquence de tâches qui contient des mots de passe, vous devez modifier la séquence de tâches importée et spécifier de nouveau les mots de passe. Veillez à spécifier des mots de passe pour les actions [Joindre le domaine ou le groupe de travail](../understand/task-sequence-steps.md#BKMK_JoinDomainorWorkgroup), [Connexion à un dossier réseau](../understand/task-sequence-steps.md#BKMK_ConnectToNetworkFolder)et [Exécuter la ligne de commande](../understand/task-sequence-steps.md#BKMK_RunCommandLine).  

- Quand vous exportez une séquence de tâches avec l’étape **Définir des variables dynamiques**, aucune valeur n’est exportée pour les variables qui sont configurées avec le paramètre **Valeur secrète**. Vous devez entrer de nouveau les valeurs pour ces variables après avoir importé la séquence de tâches.

-   Quand vous avez plusieurs sites principaux, nous vous recommandons d'importer des séquences de tâches sur le site d'administration centrale.  

 Utilisez les procédures suivantes pour exporter et importer une séquence de tâches.  

#### <a name="to-export-task-sequences"></a>Pour exporter des séquences de tâches  

1.  Dans la console Configuration Manager, cliquez sur **Bibliothèque de logiciels**.  

2.  Dans l'espace de travail **Bibliothèque de logiciels** , développez **Systèmes d'exploitation**, puis cliquez sur **Séquences de tâches**.  

3.  Dans la liste **Séquence de tâches** , sélectionnez les séquences de tâches que vous voulez exporter. Si vous sélectionnez plusieurs séquences de tâches, elles sont stockées dans un seul fichier d'exportation.  

4.  Dans l'onglet **Accueil** , dans le groupe **Séquence de tâches** , cliquez sur **Exporter** pour démarrer l'Assistant Exportation de séquence de tâches.  

5.  Sur la page **Général** , spécifiez les paramètres suivants et cliquez sur **Suivant**.  

    -   Dans la zone **Fichier** , spécifiez l'emplacement et le nom du fichier d'exportation. Si vous entrez directement le nom de fichier, veillez à inclure l'extension .zip au nom du fichier. Si vous indiquez l'emplacement du fichier d'exportation, l'Assistant ajoute automatiquement cette extension de fichier.  

    -   Désactivez la case à cocher **Exporter toutes les dépendances de séquences de tâches** si vous ne voulez pas exporter les dépendances de séquences de tâches. Par défaut, l'Assistant analyse tous les objets liés et les exporte avec la séquence de tâches. Cela inclut toutes les dépendances des applications.  

    -   Désactivez la case à cocher **Exporter tout le contenu pour les séquences de tâches et dépendances sélectionnées** si vous ne voulez pas copier le contenu de la source du package vers l'emplacement d'exportation. Si cette case à cocher est activée, l'Assistant Importation de séquence de tâches utilise le chemin d'importation comme nouvel emplacement de la source du package.  

    -   Dans la zone **Commentaires de l'administrateur** , ajoutez une description des séquences de tâches à exporter.  

6.  Effectuez toutes les étapes de l'Assistant.  

 L'Assistant crée les fichiers de sortie suivants :  

-   Si vous n'exportez pas de contenu : un fichier .zip.  

-   Si vous exportez du contenu : un fichier .zip et un dossier nommé *exportation*_files, où *exportation* est le nom du fichier .zip qui contient le contenu exporté.  

 Si vous incluez le contenu lorsque vous exportez une séquence de tâches, veillez à copier le fichier .zip et le dossier *exportation*_files, ou l'importation échouera.  

#### <a name="to-import-task-sequences"></a>Pour importer des séquences de tâches  

1.  Dans la console Configuration Manager, cliquez sur **Bibliothèque de logiciels**.  

2.  Dans l'espace de travail **Bibliothèque de logiciels** , développez **Systèmes d'exploitation**, puis cliquez sur **Séquences de tâches**.  

3.  Dans l'onglet **Accueil** , dans le groupe **Créer** , cliquez sur **Importer une séquence de tâches** pour démarrer l'Assistant Importation de séquence de tâches.  

4.  Sur la page **Général** , spécifiez le fichier .zip exporté, puis cliquez sur **Suivant**.  

5.  Sur la page **Contenu du fichier** , sélectionnez l'action dont vous avez besoin pour chaque objet que vous importez. Cette page affiche tous les objets que Configuration Manager doit importer.  

    -   Si l'objet n'a jamais été importé, sélectionnez **Créer nouveau**.  

    -   Si l'objet a été importé précédemment, sélectionnez l'une des actions suivantes :  

        -   **Ignorer le doublon** (par défaut) : cette action n’importe pas l’objet. Au lieu de cela, l'Assistant lie l'objet existant à la séquence de tâches.  

        -   **Remplacer**: cette action remplace l’objet existant par l’objet importé. Pour les applications, vous pouvez ajouter une révision pour mettre à jour l'application existante ou créer une nouvelle application.  

6.  Effectuez toutes les étapes de l'Assistant.  

 Après avoir importé la séquence de tâches, modifiez-la pour spécifier les mots de passe qui se trouvaient dans la séquence de tâches d'origine. Pour des raisons de sécurité, les mots de passe ne sont pas exportés.  

##  <a name="BKMK_CreateTSVariables"></a> Créer des variables de séquence de tâches pour les ordinateurs et les regroupements  
 Vous pouvez définir des variables de séquence de tâches personnalisées pour des ordinateurs et des regroupements. Les variables qui sont définies pour un ordinateur sont appelées variables de séquence de tâches par ordinateur. Les variables définies pour un regroupement sont appelées variables de séquence de tâches par regroupement. S'il existe un conflit, les variables par ordinateur ont préséance sur les variables par regroupement. Cela signifie que les variables de séquence de tâches attribuées à un ordinateur spécifique disposent automatiquement d'une priorité plus importante que celles attribuées au regroupement contenant l'ordinateur.  

 Par exemple, si une variable est attribuée au regroupement ABC et qu'une variable avec le même nom est attribuée à l'ordinateur XYZ, qui est un membre du regroupement ABC, la variable attribuée à l'ordinateur XYZ reçoit une priorité plus élevée que celle attribuée au regroupement ABC.  

 Vous pouvez masquer les variables par ordinateur et par regroupement pour qu’elles ne soient pas visibles dans la console Configuration Manager. Si vous ne souhaitez plus que ces variables soient masquées, vous devez les supprimer et les redéfinir sans sélectionner l'option pour les masquer. Quand vous utilisez l'option **Ne pas afficher cette valeur dans la console Configuration Manager**, la valeur de la variable n'est pas affichée, mais elle peut encore être utilisée par la séquence de tâches lors de son exécution.  

 Vous pouvez gérer les variables par ordinateur sur un site principal ou sur un site d'administration centrale. Configuration Manager ne prend pas en charge plus de 1 000 variables attribuées pour un même ordinateur.  

> [!WARNING]  
>  Lorsque vous utilisez des variables par regroupement pour des séquences de tâches, considérez les éléments suivants :  
>   
>  -   Comme les modifications apportées aux regroupements sont toujours répliquées dans toute la hiérarchie, toutes les modifications que vous apportez à des variables de regroupement ne seront pas appliquées uniquement au site actuel, mais à tous les membres du regroupement dans toute la hiérarchie.  
> -   Lorsque vous supprimez un regroupement, cette action supprime également les variables de séquence de tâches qui sont configurées pour le regroupement.  

 Utilisez les procédures suivantes pour créer des variables de séquence de tâches pour un ordinateur ou un regroupement.  

#### <a name="to-create-task-sequence-variables-for-a-computer"></a>Pour créer des variables de séquence de tâches pour un ordinateur  

1.  Dans la console Configuration Manager, cliquez sur **Ressources et Conformité**.  

2.  Dans l'espace de travail **Ressources et Conformité** , développez le regroupement qui contient l'ordinateur que vous souhaitez ajouter la variable.  

3.  Sélectionnez l'ordinateur, puis cliquez sur **Propriétés**.  

4.  Dans la boîte de dialogue **Propriétés** , cliquez sur l'onglet **Variables** .  

5.  Pour chaque variable à créer, cliquez sur l’icône **Nouveau** dans la boîte de dialogue **<Nouvelle\>Variable**, et spécifiez le nom et la valeur de la variable de séquence de tâches. Décochez la case **Ne pas afficher cette valeur dans la console Configuration Manager** si vous voulez masquer les variables pour qu’elles ne soient pas visibles dans la console Configuration Manager.  

6.  Après avoir ajouté toutes les variables à l'ordinateur, cliquez sur **OK**.  

#### <a name="to-create-task-sequence-variables-for-a-collection"></a>Pour créer des variables de séquence de tâches pour un regroupement  

1.  Dans la console Configuration Manager, cliquez sur **Ressources et Conformité**.  

2.  Dans l'espace de travail **Ressources et Conformité** , sélectionnez le regroupement auquel vous voulez ajouter la variable, puis cliquez sur **Propriétés**.  

3.  Dans la boîte de dialogue **Propriétés** , cliquez sur l'onglet **Variables du regroupement** .  

4.  Pour chaque variable à créer, cliquez sur l’icône **Nouveau** dans la boîte de dialogue **<Nouvelle\>Variable**, et spécifiez le nom et la valeur de la variable de séquence de tâches. Décochez la case **Ne pas afficher cette valeur dans la console Configuration Manager** si vous voulez masquer les variables pour qu’elles ne soient pas visibles dans la console Configuration Manager.  

5.  Si vous le souhaitez, spécifiez la priorité que Configuration Manager doit utiliser quand les variables de séquence de tâches sont évaluées.  

6.  Après avoir ajouté toutes les variables au regroupement, cliquez sur **OK**.  

##  <a name="BKMK_AdditionalActionsTS"></a> Actions supplémentaires pour gérer des séquences de tâches  
 Vous pouvez gérer des séquences de tâches en utilisant des actions supplémentaires lorsque vous sélectionnez la séquence de tâches à l'aide de la procédure suivante.  

#### <a name="to-select-a-task-sequence-to-manage"></a>Pour sélectionner une séquence de tâches à gérer  

1.  Dans la console Configuration Manager, cliquez sur **Bibliothèque de logiciels**.  

2.  Dans l'espace de travail **Bibliothèque de logiciels** , développez **Systèmes d'exploitation** , puis cliquez sur **Séquences de tâches**.  

3.  Dans la liste **Séquence de tâches** , sélectionnez la séquence de tâches que vous voulez gérer et sélectionnez l'une des options disponibles.  

 Pour plus d'informations sur certaines des actions supplémentaires afin de gérer des séquences de tâches, utilisez le tableau suivant.  

|Action|Description|  
|------------|-----------------|  
|**Copier**|Effectue une copie de la séquence de tâches sélectionnée. Cette action peut vous être utile lorsque vous voulez créer une nouvelle séquence de tâches basée sur une séquence de tâches existante.<br /><br /> Lorsque vous faites une copie d'une séquence de tâches dans un dossier, la copie est répertoriée dans ce dossier jusqu'à ce que vous actualisiez le nœud de séquence de tâches.  Après l'actualisation, la copie s'affiche dans le dossier racine.|  
|**Désactiver**|Désactive la séquence de tâches afin qu'elle ne puisse pas s'exécuter sur des ordinateurs. Des séquences de tâches désactivées peuvent être déployées sur des ordinateurs, mais les ordinateurs n'exécutent pas la séquence de tâches tant qu'elle n'est pas activée.|  
|**Activer**|Active la séquence de tâches afin qu'elle puisse être exécutée. Il est inutile de redéployer une séquence de tâches déployée une fois qu'elle est activée.|  
|**Créer un fichier de contenu préparé**|Démarre l'Assistant Création du fichier de contenu préparé pour préparer le contenu de séquence de tâches. Pour plus d’informations sur la création d’un fichier de contenu préparé, consultez [Préparer du contenu](../../core/servers/deploy/configure/deploy-and-manage-content.md#a-namebkmkprestagea-use-prestaged-content).|  
|**Déplacer**|Déplace la séquence de tâches sélectionnée vers un autre dossier.|  
|**Propriétés**|Ouvre la boîte de dialogue **Propriétés** pour la séquence de tâches sélectionnée. Utilisez cette boîte de dialogue pour modifier le comportement de l'objet de séquence de tâches. Toutefois, vous ne pouvez pas modifier les étapes de la séquence de tâches à l'aide de cette boîte de dialogue.|  

## <a name="next-steps"></a>Étapes suivantes
[Scénarios de déploiement de systèmes d’exploitation d’entreprise](scenarios-to-deploy-enterprise-operating-systems.md)

