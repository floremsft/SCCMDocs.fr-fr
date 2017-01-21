---
title: "Utiliser PXE pour déployer Windows sur le réseau | Documents Microsoft"
description: "Utilisez des déploiements de système d’exploitation établis par PXE pour actualiser le système d’exploitation d’un ordinateur ou installer une nouvelle version de Windows sur un nouvel ordinateur."
ms.custom: na
ms.date: 12/07/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: da5f8b61-2386-4530-ad54-1a5c51911f07
caps.latest.revision: 19
caps.handback.revision: 0
author: Dougeby
ms.author: dougeby
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 3f44505c977b511223a083a960f871371c0ff133
ms.openlocfilehash: b22cdbd42693078caa47f41182ce73ea881c3515


---
# <a name="use-pxe-to-deploy-windows-over-the-network-with-system-center-configuration-manager"></a>Utiliser PXE pour déployer Windows sur le réseau avec System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Les déploiements de système d’exploitation établis par PXE dans System Center Configuration Manager permettent aux ordinateurs clients de demander des systèmes d’exploitation et de les déployer sur le réseau. Dans ce scénario de déploiement de système d’exploitation, l’image du système d’exploitation et une image de démarrage Windows PE x86 et x64 sont envoyées à un point de distribution configuré pour accepter les demandes de démarrage PXE.  

> [!NOTE]  
>  Quand vous créez un déploiement de système d’exploitation qui cible seulement des ordinateurs avec un BIOS x64, les deux images de démarrage x64 et x86 doivent être disponibles sur le point de distribution.  

 Vous pouvez utiliser des déploiements de système d’exploitations établis par PXE dans les scénarios de déploiement de système d’exploitation suivants :  

-   [Actualiser un ordinateur existant avec une nouvelle version de Windows](refresh-an-existing-computer-with-a-new-version-of-windows.md)  

-   [Installer une nouvelle version de Windows sur un nouvel ordinateur (système nu)](install-new-windows-version-new-computer-bare-metal.md)  

 Effectuez les étapes de l’un des scénarios de déploiement de système d’exploitation, puis utilisez les sections suivantes pour préparer les déploiements établis par PXE.  

##  <a name="a-namebkmkconfigurea-configure-at-least-one-distribution-point-to-accept-pxe-requests"></a><a name="BKMK_Configure"></a> Configurer au moins un point de distribution qui peut répondre aux demandes PXE  
 Pour déployer des systèmes d'exploitation sur des clients Configuration Manager qui effectuent des requêtes de démarrage PXE, vous devez utiliser un ou plusieurs points de distribution qui sont configurés pour répondre aux requêtes de démarrage PXE.  Pour savoir comment activer PXE sur un point de distribution, voir [Configuration de points de distribution pour accepter des requêtes PXE](../get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_PXEDistributionPoint).  

## <a name="prepare-a-pxe-enabled-boot-image"></a>Préparer une image de démarrage compatible PXE  
 Pour utiliser PXE pour déployer un système d’exploitation, vous avez besoin d’images de démarrage compatibles PXE x86 et x64 qui sont distribuées à un ou plusieurs points de distribution compatibles PXE. Utilisez les informations pour activer PXE sur une image de démarrage et distribuez l’image de démarrage sur des points de distribution :  

-   Pour activer PXE sur une image de démarrage, sélectionnez  **Déployer cette image de démarrage depuis le point de distribution PXE** sous l’onglet **Source de données** dans les propriétés de l’image de démarrage.  

-   Si vous modifiez les propriétés de l’image de démarrage, redistribuez-la sur les points de distribution. Pour plus d’informations, consultez [Distribuer du contenu](../../core/servers/deploy/configure/deploy-and-manage-content.md#a-namebkmkdistributea-distribute-content).  

##  <a name="a-namebkmkpxeexclusionlista-create-an-exclusion-list-for-pxe-deployments"></a><a name="BKMK_PXEExclusionList"></a> Créer une liste d’exclusion pour les déploiements PXE  
 Quand vous utilisez PXE pour déployer des systèmes d’exploitation, vous pouvez créer une liste d’exclusion sur chaque point de distribution pour ignorer les demandes de démarrage PXE reçues d’ordinateurs figurant dans la liste d’exclusion. La liste d’exclusion contient les adresses MAC des ordinateurs qui doivent être ignorés par le point de distribution. Ces ordinateurs ne recevront pas les séquences de tâches de déploiement que Configuration Manager utilise pour le déploiement PXE.  

 Utilisez les étapes suivantes pour créer la liste d'exclusion PXE.  

#### <a name="to-create-the-exclusion-list"></a>Pour créer la liste d'exclusion  

1.  Créez un fichier texte sur le point de distribution qui est activé pour PXE. Par exemple, nommez ce fichier texte **pxeExceptions.txt**.  

2.  Utilisez un éditeur de texte standard, tel que le bloc-notes, et ajoutez les adresses MAC des ordinateurs qui doivent être ignorés par le point de distribution compatible PXE. Séparez les valeurs des adresses MAC par un signe deux-points et entrez chaque adresse sur une ligne distincte. Exemple : `01:23:45:67:89:ab`.  

3.  Enregistrez le fichier texte sur le serveur de système de site du point de distribution compatible PXE. Le fichier texte peut être enregistré dans n'importe quel emplacement sur le serveur.  

4.  Modifiez le Registre du point de distribution compatible PXE pour créer une clé de Registre **MACIgnoreListFile** qui contient la valeur de chaîne du chemin d'accès complet au fichier texte sur le serveur de système de site du point de distribution compatible PXE. Utilisez les chemins d'accès au Registre suivants :  

     **HKLM\Software\Microsoft\SMS\DP**  

    > [!WARNING]  
    >  Une utilisation incorrecte de l'Éditeur du Registre peut éventuellement provoquer de graves problèmes, lesquels nécessitent parfois la réinstallation complète du système d'exploitation. Microsoft ne garantit pas la résolution des erreurs résultant d'une utilisation incorrecte de l'Éditeur du Registre. Les opérations exécutées dans l'Éditeur du Registre le sont à vos propres risques.  

     Il est inutile de redémarrer le serveur après avoir effectué cette modification au niveau du Registre.  

##  <a name="a-namebkmkramdisktftparamdisk-tftp-block-size-and-window-size"></a><a name="BKMK_RamDiskTFTP"></a>Taille de bloc et de fenêtre RamDisk TFTP  
Vous pouvez personnaliser la taille de bloc TFTP RamDisk et, à compter de Configuration Manager version 1606, la taille de fenêtre pour les points de distribution compatibles PXE. Si vous avez personnalisé votre réseau, cela peut occasionner un échec de téléchargement de l’image de démarrage avec une erreur de délai d’attente résultant d’une taille excessive de bloc ou de fenêtre. La personnalisation des tailles de bloc et de fenêtre TFTP RamDisk permet d’optimiser le trafic TFTP lors de l’utilisation de PXE en réponse à des besoins réseau spécifiques. Vous devez tester les paramètres personnalisés dans votre environnement pour déterminer la configuration la plus efficace. Pour plus d’informations, voir [Personnalisation des tailles de bloc et de fenêtre TFTP RamDisk pour les points de distribution compatibles PXE](../get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_RamDiskTFTP).

## <a name="configure-deployment-settings"></a>Configurer les paramètres de déploiement  
 Pour utiliser un déploiement de système de d’exploitation initié par PXE, vous devez configurer le déploiement pour rendre le système d’exploitation accessible aux demandes de démarrage PXE. Vous pouvez configurer cela dans la page **Paramètres de déploiement** de l’Assistant Déploiement logiciel ou sous l’onglet **Paramètres de déploiement** dans les propriétés du déploiement.  Pour le paramètre **Rendre disponible aux éléments suivants** , sélectionnez l’une des options suivantes :  

-   Clients, média et environnement PXE Configuration Manager  

-   Média et environnement PXE uniquement  

-   Média et environnement PXE uniquement (masqué)  

##  <a name="a-namebkmkdeploya-deploy-the-task-sequence"></a><a name="BKMK_Deploy"></a> Déployer la séquence de tâches  
 Déployez le système d’exploitation dans un regroupement cible. Pour plus d'informations, voir [Déployer une séquence de tâches](manage-task-sequences-to-automate-tasks.md#BKMK_DeployTS). Quand vous déployez des systèmes d’exploitation à l’aide de PXE, vous pouvez configurer si le déploiement est obligatoire ou disponible.  

-   **Déploiement obligatoire**: les déploiements obligatoires utilisent PXE et ne nécessitent aucune intervention de l’utilisateur. L'utilisateur ne pourra pas contourner le démarrage PXE. Toutefois, si l'utilisateur annule le démarrage PXE avant que le point de distribution réponde, le système d'exploitation ne sera pas déployé.  

-   **Déploiement disponible**: les déploiements disponibles nécessitent l’intervention de l’utilisateur sur l’ordinateur de destination. L’utilisateur doit appuyer sur la touche F12 pour poursuivre le processus de démarrage PXE. Si cette touche F12 n'est pas actionnée, l'ordinateur démarrera soit avec le système d'exploitation actuel, soit à partir du périphérique de démarrage suivant disponible.  

 Vous pouvez redéployer un déploiement PXE requis en désactivant l'état du dernier déploiement PXE affecté à un ordinateur ou à un regroupement Configuration Manager. Cette action réinitialise l'état de ce déploiement et déploie de nouveau les déploiements requis les plus récents.  

> [!IMPORTANT]  
>  Le protocole PXE n'est pas sécurisé. Assurez-vous que le serveur PXE et le client PXE se trouvent sur un réseau sécurisé physiquement, tel qu'un centre de données, afin d'éviter l'accès non autorisé à votre site.  

##  <a name="how-is-the-boot-image-selected-for-clients-booting-with-pxe"></a>Comment l’image de démarrage est-elle sélectionnée pour les clients qui démarrent avec PXE ?
Lorsqu’un client démarre avec PXE, Configuration Manager lui fournit une image de démarrage à utiliser. Depuis Configuration Manager version 1606, Configuration Manager utilise une image de démarrage avec correspondance exacte d’architecture si une telle image est disponible. Si une image de démarrage avec correspondance exacte d’architecture n’est pas disponible, Configuration Manager utilise une image de démarrage avec une architecture compatible. La liste ci-dessous indique de quelle manière une image de démarrage est sélectionnée pour les clients qui démarrent avec PXE.
1. Configuration Manager recherche dans la base de données du site l’enregistrement système qui correspond à l’adresse MAC ou au SMBIOS du client qui essaie de démarrer.
    > [!NOTE]
    > Si un ordinateur qui est affecté à un site démarre via PXE pour un site de différent, les stratégies ne sont pas visibles pour l’ordinateur. Par exemple, si un client est déjà affecté au site A, le point de gestion et le point de distribution sur le site B ne peuvent pas accéder aux stratégies à partir du site A, et le client ne peut pas démarrer via PXE.
2. Configuration Manager recherche les séquences de tâches qui sont déployées sur l’enregistrement système trouvé à l’étape 1.
3. Dans la liste des séquences de tâches trouvées à l’étape 2, Configuration Manager recherche une image de démarrage qui correspond à l’architecture du client qui tente de démarrer. Si une image de démarrage est trouvée avec la même architecture, celle-ci est utilisée.

4. Si une image de démarrage n’est pas trouvée avec la même architecture, Configuration Manager recherche une image de démarrage (à partir de la liste des séquences de tâches trouvées à l’étape 2) qui soit compatible avec l’architecture du client qui tente de démarrer. Par exemple, un client 64 bits est compatible avec des images de démarrage 32 bits et 64 bits. Un client 32 bits est compatible uniquement avec des images de démarrage 32 bits. Un client UEFI est compatible uniquement avec des images de démarrage 64 bits.



<!--HONumber=Dec16_HO3-->


