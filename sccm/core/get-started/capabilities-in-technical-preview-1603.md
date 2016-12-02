---
title: "Fonctionnalités de la version d’évaluation technique 1603 pour System Center Configuration Manager"
description: "Découvrez les fonctionnalités disponibles dans la version d’évaluation technique 1603 pour System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology:
- configmgr-other
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5f861b72-9f14-4d17-a512-4a79b660abe6
caps.latest.revision: 8
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 39a9cde3bd955c84f301d25258b413fecaa4393b
ms.openlocfilehash: ab9f71700ff80414f7cb8e79f54fba3262f810ff

---
# <a name="capabilities-in-technical-preview-1603-for-system-center-configuration-manager"></a>Fonctionnalités de la version d’évaluation technique 1603 pour System Center Configuration Manager

*S’applique à : System Center Configuration Manager (version d’évaluation technique)*

Cet article présente les fonctionnalités qui sont disponibles dans la version d’évaluation technique 1603 pour System Center Configuration Manager. Vous pouvez installer cette version pour mettre à jour et ajouter de nouvelles fonctionnalités à votre site de version d’évaluation technique de Configuration Manager. Ou bien, lorsque vous utilisez System Center Technical Preview 5, cette version s’installe comme une version de référence de la version d’évaluation technique de System Center Configuration Manager. Avant d’installer cette version d’évaluation technique, passez en revue la rubrique de présentation, [Technical Preview pour System Center Configuration Manager](../../core/get-started/technical-preview.md), pour vous familiariser avec les conditions générales et les limitations d’utilisation d’une version d’évaluation technique, la mise à jour entre les versions et l’envoi de commentaires sur les fonctionnalités dans une version d’évaluation technique.  

 **Problèmes connus relatifs à cette version d’évaluation technique :**  

-   Cette version inclut des mises à jour de fonctionnalités publiées précédemment, mais n’en introduit pas de nouvelles. Par conséquent, la page Fonctionnalités de l’Assistant Mise à jour est vide si vous avez précédemment opéré une mise à niveau vers la version 1602 et activé toutes les fonctionnalités incluses dans celle-ci.  

-   Une fois que votre serveur opère une mise à jour vers Technical Preview 1603, les clients ne peuvent pas utiliser les fonctionnalités de contrôle à distance tant qu’ils n’ont pas eux aussi procédé à la mise à jour vers la version 1603.  

 **Vous trouverez ci-dessous les nouvelles fonctionnalités propres à cette version.**  

##  <a name="a-namebkmksc1603a-improvements-to-software-center"></a><a name="BKMK_SC1603"></a> Améliorations apportées au Centre logiciel  

### <a name="new-tiled-view-for-apps"></a>Nouvel affichage en mode Mosaïque pour les applications  
 Les utilisateurs finaux ont désormais le choix entre une liste d’applications ou un affichage en mode Mosaïque des applications sous l’onglet **Applications** du Centre logiciel.  

### <a name="select-multiple-updates-in-software-center"></a>Sélection de plusieurs mises à jour dans le Centre logiciel  
 Sous l’onglet **Mises à jour** du Centre logiciel, vous pouvez désormais sélectionner plusieurs mises à jour ou sélectionner **Tout mettre à jour** pour commencer à installer plusieurs mises à jour simultanément.  

##  <a name="a-namebkmkrc1603a-improvements-to-remote-control"></a><a name="BKMK_RC1603"></a> Améliorations apportées au contrôle à distance  

### <a name="limit-shared-clipboard-access-in-a-remote-control-session"></a>Limitation de l’accès au Presse-papiers partagé dans une session de contrôle à distance  
 Vous pouvez désormais activer le nouveau paramètre du client pour les outils à distance, **Inviter l’utilisateur à accorder une autorisation de transfert de fichier de Presse-papiers partagé**, pour limiter l’accès au Presse-papiers partagé dans une session de contrôle à distance.  

 Quand ce paramètre est activé, l’utilisateur final qui partage une session à distance doit accorder au spectateur qui visionne la session l’autorisation de transférer des fichiers de celle-ci sur son ordinateur local via le Presse-papiers partagé.  

 Cela ajoute une couche de protection pour l’utilisateur final car, précédemment, si le spectateur recevait le contrôle total de l’ordinateur de l’utilisateur final, il était en mesure d’utiliser le Presse-papiers partagé pour transférer des fichiers de la session sur son ordinateur local d’une manière totalement transparente pour l’utilisateur final.  

##  <a name="a-namebkmkramdisktftpa-customize-the-ramdisk-tftp-block-size-and-window-size-on-pxe-enabled-distribution-points"></a><a name="BKMK_RamDiskTFTP"></a> Personnalisation des tailles de bloc et de fenêtre TFTP RamDisk pour les points de distribution compatibles PXE  
 Dans Technical Preview 1603, vous pouvez personnaliser les tailles de bloc et de fenêtre TFTP RamDisk pour les points de distribution compatibles PXE. Si vous avez personnalisé votre réseau, cela peut occasionner un échec de téléchargement de l’image de démarrage avec une erreur de délai d’attente résultant d’une taille excessive de bloc ou de fenêtre. La personnalisation des tailles de bloc et de fenêtre TFTP RamDisk permet d’optimiser le trafic TFTP lors de l’utilisation de PXE en réponse à des besoins réseau spécifiques.   
Vous devez tester les paramètres personnalisés dans votre environnement pour déterminer la configuration la plus efficace.  

-   **Taille de bloc TFTP**: la taille de bloc est la taille des paquets de données que le serveur envoie au client qui télécharge le fichier (comme indiqué dans RFC 2347). Plus la taille de bloc est importante, moins le serveur envoie de paquets. Il y a donc moins de délais d’aller et retour entre le serveur et le client. Toutefois, une taille de bloc importante entraîne une fragmentation des paquets, incompatible avec la plupart des implémentations du client PXE.  

-   **Taille de fenêtre TFTP**: le protocole TFTP nécessite le renvoi d’un paquet d’accusé de réception (ACK) pour chaque bloc de données envoyé. Le serveur n’envoie pas le bloc suivant dans la séquence tant qu’il n’a pas reçu le paquet ACK pour le bloc précédent. Le fenêtrage TFTP est une fonctionnalité des Services de déploiement Windows qui permet de définir le nombre de blocs de données nécessaires pour le remplissage d’une fenêtre. Le serveur envoie les blocs de données dos à dos jusqu’à ce que la fenêtre soit remplie, et le client renvoie un paquet ACK. L’augmentation de cette taille de fenêtre réduit le nombre de délais d’aller et retour entre le client et le serveur, et raccourcit le temps global nécessaire au téléchargement d’une image de démarrage.  

### <a name="try-it-out"></a>Essayez !  
 Essayez d’accomplir les tâches suivantes, puis utilisez les informations relatives à l’envoi de commentaires au début de cette rubrique pour nous faire savoir comment cela a fonctionné :  

-   Je peux personnaliser la taille de fenêtre TFTP RamDisk pour le point de distribution compatible PXE.  

-   Je peux personnaliser la taille de bloc TFTP RamDisk pour le point de distribution compatible PXE.  

### <a name="to-modify-the-ramdisk-tftp-window-size"></a>Pour modifier la taille de fenêtre TFTP RamDisk  

-   Ajoutez la clé de Registre suivante aux points de distribution compatibles PXE pour personnaliser la taille de fenêtre TFTP RamDisk :  

     **Emplacement**: HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SMS\DP  
    Nom : RamDiskTFTPWindowSize  

     **Type**: REG_DWORD  

     **Valeur**: &lt;taille de fenêtre personnalisée\>  

 La valeur par défaut est 1 (1 bloc de données remplit la fenêtre).  

### <a name="to-modify-the-ramdisk-tftp-block-size"></a>Pour modifier la taille de bloc TFTP RamDisk  

-   Ajoutez la clé de Registre suivante aux points de distribution compatibles PXE pour personnaliser la taille de fenêtre TFTP RamDisk :  

     **Emplacement**: HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SMS\DP  
    Nom : RamDiskTFTPBlockSize  

     **Type**: REG_DWORD  

     **Valeur** : &lt;taille de bloc personnalisée\>  

 La valeur par défaut est 4096 (4k).  



<!--HONumber=Nov16_HO1-->


