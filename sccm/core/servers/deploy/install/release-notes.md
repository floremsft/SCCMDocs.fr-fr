---
title: 'Notes de publication '
titleSuffix: Configuration Manager
description: "Consultez ces notes pour les problèmes urgents qui ne sont pas encore résolus dans le produit ou traités dans un article de la Base de connaissances Microsoft."
ms.custom: na
ms.date: 02/14/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 030947fd-f5e0-4185-8513-2397fb2ec96f
caps.latest.revision: 
caps.handback.revision: 
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 53685ef2647cfd87c2fcb603097186360f1c96a5
ms.sourcegitcommit: fbd4a9d2fa8ed4ddd3a0fecc4a2ec4fc0ccc3d0c
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/19/2018
---
# <a name="release-notes-for-system-center-configuration-manager"></a>Notes de publication de System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Avec Configuration Manager, les notes de publication de produit se limitent aux problèmes urgents. Ces problèmes ne sont pas encore résolus dans le produit ou traités dans un article de la Base de connaissances Microsoft.  

La documentation spécifique aux fonctionnalités inclut des informations sur les problèmes connus qui affectent les scénarios de base.  

> [!TIP]  
>  Cette rubrique contient les notes de publication pour l’édition actuelle de Configuration Manager. Pour obtenir des informations sur l’édition Technical Preview, consultez [Technical Preview pour System Center Configuration Manager](../../../../core/get-started/technical-preview.md)  

Pour plus d’informations sur les nouvelles fonctionnalités introduites dans les différentes versions, consultez les articles suivants :
- [Nouveautés dans la version 1710](/sccm/core/plan-design/changes/whats-new-in-version-1710)
- [Nouveautés dans la version 1706](/sccm/core/plan-design/changes/whats-new-in-version-1706)  
- [Nouveautés dans la version 1702](/sccm/core/plan-design/changes/whats-new-in-version-1702)



## <a name="setup-and-upgrade"></a>Installation et mise à niveau  


### <a name="when-installing-a-long-term-service-branch-site-using-version-1606-a-current-branch-site-is-installed"></a>Quand vous installez un site Long-Term Service Branch à l’aide de la version 1606, un site Current Branch est installé
<!-- Consider move to core content  -->
Quand vous utilisez le média de base de référence de la version 1606 publiée en octobre 2016 pour installer un site Long-Term Servicing Branch (LTSB), le programme d’installation installe un site Current Branch à la place. Ce comportement se produit car l’option d’installation d’un point de connexion de service avec l’installation du site n’est pas sélectionnée.

 - Bien qu’un point de connexion ne soit pas obligatoire, son installation doit être sélectionnée pendant l’installation d’un site LTSB.

Une fois l’installation terminée, vous pouvez désinstaller le point de connexion de service. Toutefois, vous devez disposer d’un point de connexion de service en mode hors connexion ou en ligne pour envoyer les données de télémétrie et obtenir des mises à jour de sécurité pour les sites Current Branch et LTSB.

Si votre site a été installé comme un site Current Branch alors que vous souhaitiez installer LTSB, vous pouvez désinstaller le site, puis le réinstaller. Vous pouvez également appeler le [Centre d’aide et de support Microsoft](http://go.microsoft.com/fwlink/?LinkId=243064) pour obtenir de l’aide.  

Pour vérifier quelle branche a été installée, dans la console, accédez à **Administration** > **Configuration du Site** > **Sites**, puis ouvrez **Paramètres de hiérarchie**. L’option permettant de convertir le site en site Current Branch est uniquement disponible quand le site exécute LTSB.  

**Solution de contournement :** aucune.   


### <a name="an-update-persists-in-downloading-state-in-the-updates-and-servicing-node-of-the-console"></a>Une mise à jour reste en état Téléchargement dans le nœud Mises à jour et maintenance de la console  
<!-- Source bug pending. Consider move to core content.  8/15 Seeking validation of issue from Dev.  -->
Pendant le téléchargement automatique des mises à jour par un point de connexion de service en ligne, une mise à jour peut se trouver bloquée avec un état Téléchargement. Lorsque le téléchargement d’une mise à jour est bloqué, des entrées similaires aux suivantes apparaissent dans les fichiers journaux indiqués :  

DMPdownloader.log :  
`ERROR: Failed to download redist for 037cd17e-4d7b-40e1-802b-14bb682364c7 with command  /RedistUrl http://go.microsoft.com/fwlink/?LinkID=724436 /LnManifestUrl http://go.microsoft.com/fwlink/?LinkID=724434 /RedistVersion 112015 /NoUI  "D:\ConfigMgr\EasySetupPayload\037cd17e-4d7b-40e1-802b-14bb682364c7\redist"`  

ConfigMgrSetup.log :  
`Error: failed to verify 'd:\ConfigMgr\EasySetupPayload\037cd17e-4d7b-40e1-802b-14bb682364c7\redist\sqlncli.msi' authenticode signature.`  
`Error: file signature check failed for 'd:\ConfigMgr\EasySetupPayload\037cd17e-4d7b-40e1-802b-14bb682364c7\redist\sqlncli.msi`  

**Solution de contournement** : sur le serveur du site, modifiez la clé de registre ci-dessous sur la valeur suivante :  

-   **Clé à modifier** : HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\WinTrust\Trust Providers\Software Publishing  

-   **Valeur de l’état** : définie sur **146944** décimal ou sur **0x00023e00** hexadécimal  

Puis redémarrez le service SMS_Executive ou attendez jusqu’à 24 heures le prochain cycle de téléchargement automatique.

### <a name="when-using-redistributable-files-from-the-cdlatest-folder-setup-fails-with-a-manifest-verification-error"></a>Lors de l’utilisation de fichiers redistribuables à partir du dossier CD.Latest, le programme d’installation échoue avec une erreur de vérification du manifeste
<!-- Source bug pending    8/15 Seeking validation of issue from Dev.   -->

Quand vous exécutez le programme d’installation à partir du dossier CD.Latest créé pour la version 1606 et que vous utilisez les fichiers redistribuables inclus avec ce dossier CD.Latest, le programme d’installation échoue avec les erreurs suivantes dans le journal d’installation de Configuration Manager :

  `ERROR: File hash check failed for defaultcategories.dll`  
  `ERROR: Manifest verification failed. Wrong version of manifest?`

**Solution de contournement :** utilisez l’une des options suivantes :
 - Pendant l’installation, choisissez de télécharger les fichiers redistribuables de Microsoft les plus récents. Utilisez les fichiers redistribuables les plus récents à la place des fichiers inclus dans le dossier CD.Latest.
 - Supprimez manuellement le dossier *cd.latest\redist\languagepack\zhh*, puis réexécutez le programme d’installation.



<!-- ## Backup and recovery  -->


## <a name="client-deployment-and-upgrade"></a>Mise à niveau et déploiement du client  

### <a name="client-installation-fails-with-error-code-0x8007064c"></a>L’installation du client échoue avec le code d’erreur 0x8007064c
<!--- SMS 486973  applies 1606 to 1706. Not yet fixed. -->
*Le problème suivant s’applique à toutes les versions actives de Configuration Manager.*  

Lorsque vous déployez le client sur des ordinateurs Windows, l’installation échoue. Le fichier ccmsetup.log contient les entrées suivantes : 

`File 'C:\WINDOWS\ccmsetup\Silverlight.exe' returned failure exit code 1612. Fail the installation`  
`InstallFromManifest failed 0x8007064c`

**Solution de contournement** : cette erreur est due à une version endommagée de Silverlight, précédemment installée. Pour résoudre ce problème, exécutez l’outil suivant sur l’ordinateur concerné : [Résoudre les problèmes qui empêchent l’installation ou la suppression de programmes](https://support.microsoft.com/help/17588/fix-problems-that-block-programs-from-being-installed-or-removed).

## <a name="operating-system-deployment"></a>Déploiement du système d'exploitation  

### <a name="servicing-plans-create-many-duplicate-software-update-groups-and-deployments-by-default"></a>Les plans de maintenance créent un grand nombre de groupes et de déploiements de mises à jour logicielles en double  
Par défaut, l’Assistant Créer un plan de maintenance s’exécute actuellement après chaque synchronisation des mises à jour logicielles. Chaque fois que l’Assistant s’exécute, il crée un groupe et un déploiement de mises à jour logicielles. Si vous avez une planification de la synchronisation des mises à jour logicielles qui s’exécute plusieurs fois par jour, l’Assistant Créer un plan de maintenance génère quotidiennement plusieurs groupes et déploiements de mises à jour logicielles.  

**Solution de contournement** : après avoir créé un plan de maintenance, ouvrez les propriétés de celui-ci, accédez à l’onglet **Calendrier d’évaluation**, sélectionnez **Exécuter la règle dans un calendrier**, cliquez sur **Personnaliser**, puis créez un calendrier personnalisé. Par exemple, vous pouvez faire en sorte que le plan de maintenance s’exécute tous les 60 jours.  



## <a name="software-updates"></a>Mises à jour logicielles

### <a name="importing-an-office-365-client-settings-from-a-configuration-file-fails-when-it-contains-unsupported-languages"></a>L’importation des paramètres d’un client Office 365 à partir d’un fichier de configuration échoue s’il contient des langages non pris en charge
<!-- 489258  Fixed in 1706  -->
*Le problème suivant s’applique à la version 1702 et aux versions antérieures.*   

Lorsque vous importez les paramètres d’un client Office 365 à partir d’un fichier de configuration XML existant et que le fichier contient des langues qui ne sont pas prises en charge par le client Office 365 ProPlus, une erreur se produit. Pour plus d’informations, consultez : [Déployer des applications Office 365 sur des clients depuis le tableau de bord Gestion des clients Office 365](/sccm/sum/deploy-use/manage-office-365-proplus-updates#to-deploy-office-365-apps-to-clients-from-the-office-365-client-management-dashboard).

**Solution de contournement** : utilisez uniquement les [langues prises en charge par le client Office 365 ProPlus](https://technet.microsoft.com/library/cc179219&#40;v=office.16&#41;.aspx) dans le fichier de configuration XML.  



## <a name="mobile-device-management"></a>Gestion des appareils mobiles  

### <a name="beginning-with-version-1710-you-can-no-longer-deploy-windows-phone-81-vpn-profiles-to-windows-10------503274--should-be-fixed-by-1802-if-not-sooner---"></a>À compter de la version 1710, vous ne pouvez plus déployer de profils VPN Windows Phone 8.1 sur Windows 10   <!-- 503274  Should be fixed by 1802, if not sooner -->
Dans la version 1710, il n’est plus possible de créer un profil VPN à l’aide du workflow Windows Phone 8.1 qui s’applique aussi aux appareils Windows 10. Pour ces profils, la page Plateformes prises en charge ne s’affiche plus dans l’Assistant de création. Windows Phone 8.1 est sélectionné automatiquement sur le serveur principal. La page Plateformes prises en charge est disponible dans les propriétés du profil, mais n’affiche pas les options de Windows 10.

**Solution de contournement** : Utilisez le workflow du profil VPN Windows 10 pour les appareils Windows 10. Si ce n’est pas possible pour votre environnement, contactez le support technique. Le support technique peut vous aider à ajouter le ciblage Windows 10.


### <a name="full-wipe-disables-windows-10-devices-with-less-than-4-gb-of-memory"></a>Une réinitialisation complète désactive les appareils Windows 10 avec moins de 4 Go de mémoire
L’exécution d’une réinitialisation complète sur les appareils Windows 10, version 1507, avec moins de 4 Go de RAM peut rendre l’appareil inutilisable. Après une tentative de réinitialisation de l’appareil, il ne peut pas démarrer et ne répond pas.

**Solution de contournement** : vérifiez que les appareils Windows 10 ont au moins 4 Go de mémoire disponible avant d’effectuer une réinitialisation complète. Pour afficher le numéro de version des appareils Windows 10, entrez « winver » à partir d’une invite de commandes. Si vous avez déjà réinitialisé l’appareil, et que celui-ci n’est plus réactif, utilisez un lecteur USB Windows 10 démarrable pour récupérer l’appareil.


### <a name="when-a-user-belongs-to-two-or-more-user-collections-to-which-you-deploy-a-terms-and-conditions-policy-the-user-sees-multiple-sets-of-the-same-terms"></a>Quand un utilisateur appartient à plusieurs regroupements d’utilisateurs pour lesquels une stratégie de conditions générales est déployée, l’utilisateur voit plusieurs ensembles des mêmes conditions générales  
<!-- 454394    -->
Si vous déployez un ensemble de conditions générales dans plusieurs regroupements d’utilisateurs et qu’un utilisateur est membre de plusieurs de ces regroupements, plusieurs copies identiques des conditions générales lui sont présentées quand il ouvre le Portail d’entreprise. Par exemple :
- Un utilisateur nommé « SampleUser » est membre de deux regroupements d’utilisateurs différents, « CompanyEmployeesFTE » et « CompanyEmployeesNA »
- Vous déployez les conditions générales « CompanyTerms » vers CompanyEmployeesFTE et CompanyEmployeesNA
- SampleUser voit deux ensembles identiques de CompanyTerms sur la page d’acceptation des conditions générales dans le Portail d’entreprise. 

Les utilisateurs peuvent uniquement accepter ou refuser l’ensemble des conditions générales. Par conséquent, il n’existe aucun risque d’état d’acceptation ambigu. (Cet état ambigu se produit lorsque l’utilisateur accepte et rejette les mêmes conditions générales). Le rapport d’acceptation des conditions générales comprend une seule ligne par ensemble de conditions générales et par utilisateur. Il ne contient donc aucune erreur. La seule conséquence est que l’utilisateur voit deux ensembles de conditions générales dans la page d’acceptation.  

**Solution de contournement**: assurez-vous que chaque utilisateur appartient à un seul regroupement où les conditions générales sont déployées.  


<!-- ## Reports and monitoring    -->
<!-- ## Conditional access   -->
<!-- ## Endpoint Protection -->
