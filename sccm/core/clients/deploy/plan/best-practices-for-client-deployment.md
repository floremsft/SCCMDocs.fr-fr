---
title: "Bonnes pratiques pour le déploiement de clients | System Center Configuration Manager"
description: "Bonnes pratiques pour le déploiement de clients dans System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: a933d69c-5feb-4b2b-84e8-56b3b64d5947
caps.latest.revision: 11
author: Mtillman
ms.author: mtillman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 22a34dce45e655dca1ddcb3dfe1bb0105c4026c1


---
# <a name="best-practices-for-client-deployment-in-system-center-configuration-manager"></a>Bonnes pratiques pour le déploiement de clients dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Pour déployer des clients sur des ordinateurs dans System Center Configuration Manager, tenez compte des bonnes pratiques suivantes.  

## <a name="use-software-update-based-client-installation-for-active-directory-computers"></a>Utilisation de l'installation de client basée sur des mises à jour logicielles sur les ordinateurs Active Directory  
 Cette méthode de déploiement du client présente l'avantage d'utiliser les technologies Windows existantes, s'intègre avec votre infrastructure Active Directory et ne nécessite qu'une configuration minimale dans Configuration Manager. Elle est la plus facile pour configurer le pare-feu et la plus sûre. À l'aide de groupes de sécurité et du filtrage WMI pour la configuration de stratégie de groupe, vous disposez d'une grande flexibilité pour contrôler quels ordinateurs installent le client Configuration Manager.  

 Pour plus d’informations, voir [Comment installer des clients Configuration Manager à l'aide d'une installation basée sur les mises à jour logicielles](../../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientSUP).  

## <a name="extend-the-active-directory-schema-and-publish-the-site-so-that-you-can-run-ccmsetup-without-command-line-options"></a>Développement du schéma Active Directory et publication du site afin de pouvoir exécuter CCMSetup sans options de ligne de commande  
 Lorsque vous étendez le schéma Active Directory pour Configuration Manager et que le site est publié dans les services de domaine Active Directory, de nombreuses propriétés d'installation du client sont publiées dans les services de domaine Active Directory. Si un ordinateur peut localiser ces propriétés d'installation du client, il peut les utiliser au cours du déploiement du client Configuration Manager. Ces informations étant générées automatiquement, le risque d'erreur humaine propre à la saisie manuelle des propriétés d'installation est éliminé.  

 Pour plus d’informations, consultez [À propos de la publication des propriétés d’installation du client sur les services de domaine Active Directory dans System Center Configuration Manager](../../../../core/clients/deploy/about-client-installation-properties-published-to-active-directory-domain-services.md).  

## <a name="when-you-have-many-clients-to-deploy-plan-a-phased-rollout-outside-business-hours"></a>Planification d'un déploiement échelonné hors des heures de travail pour le déploiement de nombreux clients  
 Réduisez les besoins de traitement par le processeur sur le serveur de site en planifiant un déploiement échelonné des clients pendant une période. Déployez des clients hors des heures de travail pour assurer que les services métier critiques disposent de plus de bande passante pendant la journée et éviter de perturber le travail des utilisateurs en cas de ralentissement ou de redémarrage des ordinateurs pour terminer l'installation.  

## <a name="enable-automatic-upgrade-after-your-main-client-deployment-has-finished"></a>Activation de la mise à niveau automatique après le déploiement client principal  
 Les mises à niveau automatiques du client sont utiles lorsque vous souhaitez mettre à niveau un petit nombre d'ordinateurs clients qui peuvent avoir été omis par votre méthode d'installation principale du client. Par exemple, si vous avez terminé une mise à niveau initiale du client, mais que certains clients étaient hors ligne pendant le déploiement de la mise à niveau. Dans ce cas, vous utilisez cette méthode pour mettre à niveau le client sur ces ordinateurs lors de leur activation suivante.  

> [!NOTE]  
>  Les améliorations des performances dans Configuration Manager vous permettent d’utiliser les mises à niveau automatiques comme méthode principale de mise à niveau des clients. Toutefois, les performances dépendent de l'infrastructure de votre hiérarchie, par exemple, le nombre de clients.  

 Pour plus d’informations sur la méthode de mise à niveau automatique des clients, consultez [Comment mettre à niveau les clients pour les ordinateurs Windows dans System Center Configuration Manager](../../../../core/clients/manage/upgrade/upgrade-clients-for-windows-computers.md).  

## <a name="use-smsmp-and-fsp-if-you-install-the-client-with-clientmsi-properties"></a>Utilisation de SMSMP et FSP pour l'installation du client avec les propriétés client.msi  
 La propriété SMSMP définit le point de gestion initial avec lequel le client communique et supprime la dépendance sur les solutions d'emplacement de service telles que les services de domaine Active Directory, DNS et WINS.  

 Utilisez la propriété FSP et installez un point d'état de secours afin de pouvoir surveiller l'installation et l'affectation du client, et identifier les problèmes de communication.  

 Pour plus d’informations sur ces options, consultez [À propos des propriétés d’installation du client dans System Center Configuration Manager](../../../../core/clients/deploy/about-client-installation-properties.md).  

## <a name="if-you-want-to-use-client-languages-other-than-english-install-the-client-language-packs-before-you-install-the-clients"></a>Pour l'utilisation de langues de client autres que l'anglais, effectuer l'installation du module linguistique client avant d'installer les clients  
 Si vous installez des modules linguistiques client sur un site après l'installation des clients, vous devez réinstaller ces derniers afin qu'ils puissent utiliser les langues supplémentaires. Pour les clients d’appareils mobiles, cela signifie que vous devez réinitialiser les appareils mobiles et les inscrire de nouveau.  

 Pour plus d’informations sur la façon d’ajouter la prise en charge d’autres langues client, consultez [Modules linguistiques dans System Center Configuration Manager](../../../../core/servers/deploy/install/language-packs.md).  

## <a name="plan-and-prepare-any-required-pki-certificates-in-advance"></a>Planifier et préparer les certificats PKI requis à l’avance  
 Pour gérer des appareils sur Internet, des appareils mobiles inscrits et des ordinateurs Mac, vous devez disposer de certificats PKI sur les systèmes de site (points de gestion et points de distribution) et les appareils clients. Pour de nombreux clients, une planification et une préparation à l'avance sont requises, en particulier si une équipe distincte est chargée de gérer votre infrastructure à clé publique. Sur les réseaux de production, l'approbation de la gestion des modifications peut être requise pour utiliser de nouveaux certificats et redémarrer les serveurs de système de site. Sinon, les utilisateurs devront devront fermer la session et la rouvrir pour appliquer l'appartenance au nouveau groupe. En outre, vous devrez laisser suffisamment de temps pour la réplication des autorisations de sécurité et pour les nouveaux modèles de certificat.  

 Pour plus d’informations sur les certificats PKI nécessaires, consultez [Configuration requise des certificats PKI pour System Center Configuration Manager](../../../../core/plan-design/network/pki-certificate-requirements.md).  

## <a name="before-you-install-clients-configure-any-required-client-settings-and-maintenance-windows"></a>Configuration des paramètres client et des fenêtres de maintenance requis avant l'installation de clients  
 Même si vous pouvez configurer les paramètres client et les fenêtres de maintenance avant ou après l'installation des clients, configurez les paramètres requis avant d'installer les clients pour pouvoir utiliser ces paramètres dès que le client est installé. Pour plus d'informations, consultez [Guide pratique pour configurer les paramètres client dans System Center Configuration Manager](../../../../core/clients/deploy/configure-client-settings.md).  

 Configurez des fenêtres de maintenance pour les serveurs et les appareils Windows Embedded, afin de garantir un fonctionnement ininterrompu de ces ordinateurs souvent critiques. Par exemple, les fenêtres de maintenance veillent à ce que les mises à jour logicielles et les logiciels anti-programme malveillant requis ne redémarrent pas l'ordinateur pendant les heures de bureau.  

> [!IMPORTANT]  
>  Pour les ordinateurs Windows 10 que vous souhaitez protéger avec le Filtre d’écriture unifié (UWF), vous devez configurer le périphérique pour UWF avant d’installer le client. Cela permet à Configuration Manager d’installer le client avec un fournisseur d’informations d’identification personnalisées qui empêche des utilisateurs aux droits restreints de se connecter à l’appareil en mode maintenance.  

## <a name="for-mac-computers-and-mobile-devices-that-are-enrolled-by-configuration-manager-plan-your-user-enrollment-experience"></a>Planification de l'expérience utilisateur d'inscription pour les ordinateurs Mac et les appareils mobiles inscrits auprès de Configuration Manager  
 Si les utilisateurs peuvent inscrire leurs ordinateurs Mac et leurs appareils mobiles à l'aide de Configuration Manager, vous devez planifier et préparer l'expérience utilisateur. Par exemple, vous pouvez créer un script pour le processus d'installation et d'inscription en utilisant une page Web sur laquelle les utilisateurs indiquent les informations strictement nécessaires qui vous permettent de leur envoyer les instructions via un lien par courrier électronique.  

## <a name="when-you-manage-windows-embedded-devices-use-file-based-write-filters-fbwf-rather-than-enhanced-write-filters-ewf-for-higher-scalability"></a>Utilisation de filtres d’écriture basés sur des fichiers (FBWF) au lieu de filtres d’écriture améliorés (EWF) pour une évolutivité plus élevée pendant la gestion d’appareils Windows Embedded  
 Les appareils embarqués qui utilisent des filtres d'écriture améliorés (EWF) peuvent rencontrer des resynchronisations de messages d'état. Si vous n'avez que quelques appareils embarqués qui utilisent des filtres d'écriture améliorés, il est possible que vous ne vous en rendiez pas compte. Par contre, si vous en avez beaucoup qui resynchronisent leurs informations, par exemple qui envoient un inventaire complet plutôt qu'un inventaire différentiel, cela risque de générer une augmentation détectable des paquets réseau et un traitement par le processeur plus élevé sur le serveur de site.  

 Si vous avez le choix du type de filtre d’écriture à activer, choisissez des filtres d’écriture basés sur des fichiers et configurez des exceptions pour conserver l’état du client et les données d’inventaire entre redémarrages d’appareil et préserver l’efficacité du réseau et du processeur sur le client Configuration Manager. Pour plus d’informations sur les filtres d’écriture, consultez   [Planification du déploiement de clients sur des appareils Windows Embedded dans System Center Configuration Manager](../../../../core/clients/deploy/plan/planning-for-client-deployment-to-windows-embedded-devices.md).  

 Pour plus d’informations sur le nombre maximal de clients Windows Embedded pris en charge par un site principal, consultez [Systèmes d’exploitation pris en charge pour les clients et les appareils](../../../../core/plan-design/configs/supported-operating-systems-for-clients-and-devices.md).  



<!--HONumber=Nov16_HO1-->


