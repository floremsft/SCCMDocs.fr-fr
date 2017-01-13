---
title: Point de connexion de service | Microsoft Docs
description: "Découvrez ce rôle système de site Configuration Manager, puis comprenez et planifiez sa plage d’utilisations."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: bc2282d5-0571-465b-9528-a555855eaacd
caps.latest.revision: 18
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 4a8d98addcd463eb82d8b7100b44254a10d21992
ms.openlocfilehash: b5f7ad01f7a32d69d0c75b3c80a053f3c020c036


---
# <a name="about-the-service-connection-point-in-system-center-configuration-manager"></a>À propos du point de connexion de service dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Le point de connexion de service System Center Configuration Manager est un rôle système de site qui remplit plusieurs fonctions importantes pour la hiérarchie. Avant de configurer le point de connexion, évaluez et planifiez dans quelle mesure son utilisation peut influer sur la façon dont vous configurez ce rôle de système de site :  

-   **Gérer les appareils mobiles avec Microsoft Intune** : ce rôle remplace le connecteur Windows Intune utilisé par les versions précédentes de Configuration Manager et peut être configuré avec les détails de votre abonnement Intune. Voir [Gestion des appareils mobiles (MDM) hybride avec System Center Configuration Manager et Microsoft Intune](../../../../mdm/understand/hybrid-mobile-device-management.md).  

-   **Gérer les appareils mobiles avec la gestion MDM locale** : ce rôle assure la prise en charge des appareils locaux que vous gérez et qui ne se connectent pas à Internet. Voir [Gérer des appareils mobiles avec une infrastructure locale dans System Center Configuration Manager](../../../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md).  

-   **Charger les données d’utilisation à partir de votre infrastructure Configuration Manager** : vous pouvez contrôler le niveau ou la quantité de détails que vous chargez. Les données chargées nous aide à :  

    -   identifier et résoudre les problèmes de manière proactive ;  

    -   améliorer nos produits et services ;  

    -   identifier les mises à jour pour Configuration Manager applicables à la version de Configuration Manager que vous utilisez.  

  Pour plus d’informations sur les données collectées par chaque niveau et sur la façon de modifier le niveau de regroupement après l’installation du rôle, consultez [Données d’utilisation et de diagnostics](/sccm/core/plan-design/diagnostics/diagnostics-and-usage-data), puis suivez le lien correspondant à la version de Configuration Manager que vous utilisez.  

    Pour plus d’informations, consultez [Paramètres et niveaux de données d’utilisation](../../../../core/servers/deploy/install/setup-reference.md#bkmk_usage).  

-   **Télécharger les mises à jour applicables à votre infrastructure Configuration Manager** : seules les mises à jour appropriées pour votre infrastructure sont disponibles, en fonction des données d’utilisation que vous chargez.  

 **Chaque hiérarchie prend en charge une seule instance de ce rôle :**  

-   Ce rôle de système de site ne peut être installé que sur le site de niveau supérieur de votre hiérarchie (un site d’administration centrale ou le site principal autonome).  

-   Si vous étendez un site principal autonome vers une hiérarchie plus importante, vous devez désinstaller ce rôle du site principal pour pouvoir l’installer ensuite sur le site d’administration centrale.  

##  <a name="a-namebkmkmodesa-modes-of-operation"></a><a name="bkmk_modes"></a> Modes opératoires  
 Le point de connexion de service prend en charge deux modes de fonctionnement :  

-   En **mode en ligne**, le point de connexion de service vérifie automatiquement l’existence de mises à jour toutes les 24 heures et télécharge dans la console Configuration Manager les mises à jour disponibles pour la version actuelle de vos infrastructure et produits.  

-   En **mode hors connexion**, le point de connexion de service ne se connecte pas au service cloud Microsoft et vous devez manuellement [Utiliser l’outil de connexion de service pour System Center Configuration Manager](../../../../core/servers/manage/use-the-service-connection-tool.md) pour importer les mises à jour disponibles.  

Quand vous changez le mode en ligne ou hors connexion après avoir installé le point de connexion de service, vous devez redémarrer le thread SMS_DMP_DOWNLOADER du service SMS_Executive Configuration Manager pour appliquer cette modification.  Pour ce faire, utilisez le Gestionnaire de service de Configuration Manager pour redémarrer uniquement le thread SMS_DMP_DOWNLOADER du service SMS_Executive.  Vous pouvez également redémarrer le service SMS_Executive pour Configuration Manager (qui redémarre la plupart des composants de site), ou attendre une tâche planifiée comme une sauvegarde de site, qui arrête puis redémarre ultérieurement le service SMS_Executive pour vous.  

Pour utiliser le Gestionnaire de service de Configuration Manager, dans la console, accédez à **Surveillance** > **État du système** > **État du composant**, cliquez sur **Démarrer**, puis sélectionnez **Gestionnaire de service de Configuration Manager**.  Dans le Gestionnaire de service :  

-   Dans le volet de navigation, développez le site, puis **Composants**, puis sélectionnez le composant à redémarrer.  

-   Dans le volet d’informations, cliquez avec le bouton droit sur le composant, puis sélectionnez **Requête**.  

-   Une fois l’état du composant confirmé, recliquez avec le bouton droit sur le composant, puis sélectionnez **Arrêter**.  

-   Envoyez une nouvelle **requête** au composant pour confirmer qu’il est arrêté, recliquez avec le bouton droit sur le composant, puis sélectionnez **Démarrer**.  

> [!IMPORTANT]  
>  Quand vous ajoutez un abonnement Microsoft Intune au point de connexion de service, il définit automatiquement le rôle système de site en ligne. Le point de connexion de service ne prend pas en charge le mode hors connexion en cas de configuration avec un abonnement Intune.  

**Quand le rôle s’installe sur un ordinateur distant du serveur de site :**  

-   Le compte d’ordinateur du serveur de site doit être un administrateur local sur l’ordinateur qui héberge une connexion de service distant.

-   Vous devez configurer le serveur de système de site qui héberge le rôle avec un compte d’installation du système de site.  

-   Le compte d’installation du système de site est utilisé par le gestionnaire de distribution sur le serveur de site pour transférer les mises à jour à partir du point de connexion de service.

##  <a name="a-namebkmkurlsa-internet-access-requirements"></a><a name="bkmk_urls"></a> Conditions requises pour l’accès Internet  
L’ordinateur qui héberge le point de connexion de service et les éventuels pare-feu entre cet ordinateur et Internet doit transmettre les communications par le biais du **port TCP 443** aux emplacements Internet suivants. Le point de connexion de service prend également en charge l’utilisation d’un proxy web (avec ou sans authentification) pour l’accès à ces emplacements.  

**Mises à jour et maintenance**  

-   *.akamaiedge.net  

-   *.manage.microsoft.com

-   go.microsoft.com

-   blob.core.windows.net  

-   download.microsoft.com  

-   sccmconnected-a01.cloudapp.net  

**Microsoft Intune**  

-   *manage.microsoft.com  
-   https://bspmts.mp.microsoft.com/V
-   https://login.microsoftonline.com/{TenantID}


**Maintenance de Windows 10**  

-   download.microsoft.com  

-   https://go.microsoft.com/fwlink/?LinkID=619849  

## <a name="install-the-service-connection-point"></a>Installer le point de connexion de service
Quand vous exécutez le **programme d’installation** pour installer le site de plus haut niveau d’une hiérarchie, vous avez la possibilité d’installer le point de connexion de service.

Après l’exécution du programme d’installation ou si vous réinstallez le rôle de système de site, utilisez l’Assistant **Ajout des rôles de système de site** ou l’Assistant **Créer un serveur de système de Site** pour installer le système de site sur un serveur au plus haut niveau de votre hiérarchie (le site d’administration centrale ou un site principal autonome).  Les deux Assistants se trouvent sous l’onglet **Accueil** dans la console, dans **Administration** > **Configuration du site** > **Serveurs et rôles de système de Site**.



<!--HONumber=Dec16_HO5-->


