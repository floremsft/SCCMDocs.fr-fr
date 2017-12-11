---
title: 'Notes de publication '
titleSuffix: Configuration Manager
description: "Consultez ces notes pour les problèmes urgents qui ne sont pas encore résolus dans le produit ou traités dans un article de la Base de connaissances Microsoft."
ms.custom: na
ms.date: 11/28/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 030947fd-f5e0-4185-8513-2397fb2ec96f
caps.latest.revision: "41"
caps.handback.revision: "0"
author: mestew
ms.author: mstewart
manager: angrobe
ms.openlocfilehash: 8030ce7f98ebb34d9581ad036513b9b1c879c0ad
ms.sourcegitcommit: daa080cf220835f157a23e8c8e2bd2781b869bb7
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/04/2017
---
# <a name="release-notes-for-system-center-configuration-manager"></a>Notes de publication de System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Avec System Center Configuration Manager, les notes de publication de produit sont limitées aux problèmes urgents qui n’ont pas encore été résolus dans le produit (disponibles par le biais d’une mise à jour dans la console) ou détaillés dans un article de la Base de connaissances Microsoft.  

Les informations sur les problèmes connus qui affectent des scénarios de base sont transmises dans la documentation du produit en ligne accessible dans la bibliothèque de documentation de System Center Configuration Manager.  

> [!TIP]  
>  Cette rubrique contient les notes de publication de la branche CB (Current Branch) de System Center Configuration Manager. Pour la préversion technique de System Center Configuration Manager, consultez [Technical Preview pour System Center Configuration Manager](../../../../core/get-started/technical-preview.md).  

Pour plus d’informations sur les nouvelles fonctionnalités introduites dans les différentes versions, consultez les rubriques suivantes :
- [Nouveautés dans la version 1706](/sccm/core/plan-design/changes/whats-new-in-version-1706)  
- [Nouveautés dans la version 1702](/sccm/core/plan-design/changes/whats-new-in-version-1702)
- [Nouveautés dans la version 1610](/sccm/core/plan-design/changes/whats-new-in-version-1610)



## <a name="setup-and-upgrade"></a>Installation et mise à niveau  


### <a name="when-installing-a-long-term-service-branch-site-using-version-1606-a-current-branch-site-is-installed"></a>Quand vous installez un site Long-Term Service Branch à l’aide de la version 1606, un site Current Branch est installé
<!-- Consider move to core content  -->
Quand vous utilisez le média de base de référence de la version 1606 publiée en octobre 2016 pour installer un site Long-Term Servicing Branch (LTSB), le programme d’installation installe un site Current Branch à la place. Cela se produit car l’option d’installation d’un point de connexion de service avec l’installation du site n’est pas sélectionnée.

 - Bien qu’un point de connexion ne soit pas obligatoire, son installation doit être sélectionnée pendant l’installation d’un site LTSB.

Une fois l’installation terminée, vous pouvez désinstaller le point de connexion de service.  Toutefois, vous devez disposer d’un point de connexion de service en mode hors connexion ou en ligne pour envoyer les données de télémétrie et obtenir des mises à jour de sécurité pour les sites Current Branch et LTSB.

Si votre site a été installé comme un site Current Branch alors que vous souhaitiez installer LTSB, vous pouvez désinstaller le site, puis le réinstaller. Vous pouvez également appeler le [Centre d’aide et de support Microsoft](http://go.microsoft.com/fwlink/?LinkId=243064) pour obtenir de l’aide.  

Pour vérifier quelle branche a été installée, dans la console, accédez à **Administration** > **Configuration du Site** > **Sites**, puis ouvrez **Paramètres de hiérarchie**. L’option permettant de convertir le site en site Current Branch est uniquement disponible quand le site exécute LTSB.  

**Solution de contournement :**  aucune.   


### <a name="an-update-is-stuck-with-a-state-of-downloading-in-the-updates-and-servicing-node-of-the-configuration-manager-console"></a>Une mise à jour est bloquée avec un état Téléchargement dans le nœud Mises à jour et maintenance de la console Configuration Manager  
<!-- Source bug pending. Consider move to core content.  8/15 Seeking validation of issue from Dev.  -->
Pendant le téléchargement automatique des mises à jour par un point de connexion de service en ligne, une mise à jour peut se trouver bloquée avec un état Téléchargement. Lorsque le téléchargement d’une mise à jour est bloqué, des entrées similaires aux suivantes apparaissent dans les fichiers journaux indiqués :  

DMPdownloader.log :  

-   ERROR: Failed to download redist for 037cd17e-4d7b-40e1-802b-14bb682364c7 with command  /RedistUrl http://go.microsoft.com/fwlink/?LinkID=724436 /LnManifestUrl http://go.microsoft.com/fwlink/?LinkID=724434 /RedistVersion 112015 /NoUI  "D:\ConfigMgr\EasySetupPayload\037cd17e-4d7b-40e1-802b-14bb682364c7\redist"  

ConfigMgrSetup.log :  

-   Error: failed to verify ’d:\ConfigMgr\EasySetupPayload\037cd17e-4d7b-40e1-802b-14bb682364c7\redist\sqlncli.msi’ authenticode signature.  

-   Error: file signature check failed for ’d:\ConfigMgr\EasySetupPayload\037cd17e-4d7b-40e1-802b-14bb682364c7\redist\sqlncli.msi  

**Solution de contournement** : sur le serveur de site, modifiez la clé de Registre suivante comme ci-après, puis redémarrez le service SMS_Executive ou attendez jusqu’à 24 heures le prochain cycle de téléchargement automatique.  

-   **Clé à modifier** : HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\WinTrust\Trust Providers\Software Publishing  

-   **Valeur de l’état** : définie sur **146944** décimal ou sur **0x00023e00** hexadécimal  


###  <a name="setup-fails-when-using-redist-files-from-the-cdlatest-folder-with-a-manifest-verification-error"></a>Le programme d’installation échoue lors de l’utilisation de fichiers redist à partir du dossier CD.Latest avec une erreur de vérification du manifeste
<!-- Source bug pending    8/15 Seeking validation of issue from Dev.   -->

Quand vous exécutez le programme d’installation à partir d’un dossier CD.Latest créé pour la version 1606 et que vous utilisez les fichiers redist inclus avec ce dossier CD.Latest, le programme d’installation échoue avec les erreurs suivantes dans le journal d’installation de Configuration Manager :

  - ERROR: File hash check failed for defaultcategories.dll (ERREUR : Échec de la vérification du hachage de fichier pour defaultcategories.dll)
  - ERROR: Manifest verification failed. Wrong version of manifest? (ERREUR : Échec de la vérification du manifeste. Version de manifeste incorrecte ?)

**Solution de contournement :** procédez de l’une des manières suivantes :
 - Pendant l’installation, téléchargez les fichiers redist les plus récents de Microsoft à utiliser à la place de ceux figurant dans le dossier CD.Latest.
 - Supprimez manuellement le dossier *cd.latest\redist\languagepack\zhh*, puis réexécutez le programme d’installation.



<!-- ## Backup and recovery  -->


## <a name="client-deployment-and-upgrade"></a>Mise à niveau et déploiement du client  

### <a name="client-installation-fails-with-error-code-0x8007064c"></a>L’installation du client échoue avec le code d’erreur 0x8007064c
<!--- SMS 486973  applies 1606 to 1706. Not yet fixed. -->
*Les éléments suivants s’appliquent à toutes les versions actives de Configuration Manager.*   
Lorsque vous déployez le client sur des ordinateurs Windows, l’installation échoue. Le fichier ccmsetup.log contient une entrée « File 'C:\WINDOWS\ccmsetup\Silverlight.exe' returned failure exit code 1612. Fail the installation » suivie de "InstallFromManifest failed 0x8007064c ».

**Solution de contournement** Cette erreur est due à une version endommagée de Silverlight, précédemment installée. Vous pouvez essayer d’exécuter l’outil suivant sur l’ordinateur concerné pour résoudre ce problème : [https://support.microsoft.com/help/17588/fix-problems-that-block-programs-from-being-installed-or-removed](https://support.microsoft.com/help/17588/fix-problems-that-block-programs-from-being-installed-or-removed)

## <a name="operating-system-deployment"></a>Déploiement du système d'exploitation  

### <a name="servicing-plans-create-a-lot-of-duplicate-software-update-groups-and-deployments-by-default"></a>Les plans de maintenance créent un grand nombre de groupes et de déploiements de mises à jour logicielles en double  
Par défaut, l’Assistant Créer un plan de maintenance s’exécute actuellement après chaque synchronisation des mises à jour logicielles. Chaque fois que l’Assistant s’exécute, il crée un groupe et un déploiement de mises à jour logicielles. Par exemple, si vous avez une planification de la synchronisation des mises à jour logicielles qui s’exécute plusieurs fois par jour, l’Assistant Créer un plan de maintenance génère quotidiennement plusieurs groupes et déploiements de mises à jour logicielles, probablement identiques.  

**Solution de contournement** :    
après avoir créé un plan de maintenance, ouvrez les propriétés de celui-ci, accédez à l’onglet **Calendrier d’évaluation**, sélectionnez **Exécuter la règle dans un calendrier**, cliquez sur **Personnaliser**, puis créez un calendrier personnalisé. Par exemple, vous pouvez faire en sorte que le plan de maintenance s’exécute tous les 60 jours.  



## <a name="software-updates"></a>Mises à jour logicielles

### <a name="importing-an-office-365-client-settings-from-a-configuration-file-fails-when-it-contains-unsupported-languages"></a>L’importation des paramètres d’un client Office 365 à partir d’un fichier de configuration échoue s’il contient des langages non pris en charge
<!-- 489258  Fixed in 1706  -->
*Les éléments suivants s’appliquent à la version 1702 et versions antérieures.*   
Lorsque vous importez les paramètres d’un client Office 365 à partir d’un fichier de configuration XML existant et que le fichier contient des langues qui ne sont pas prises en charge par le client Office 365 ProPlus, une erreur se produit. Pour plus d’informations, voir [Déployer des applications Office 365 sur des clients depuis le tableau de bord Gestion des clients Office 365](/sccm/sum/deploy-use/manage-office-365-proplus-updates#to-deploy-office-365-apps-to-clients-from-the-office-365-client-management-dashboard).

**Solution de contournement** :    
Utilisez uniquement les [langues prises en charge par le client Office 365 ProPlus](https://technet.microsoft.com/library/cc179219&#40;v=office.16&#41;.aspx) dans le fichier de configuration XML.  



## <a name="mobile-device-management"></a>Gestion des appareils mobiles  

### <a name="beginning-with-version-1710-you-can-no-longer-deploy-windows-phone-81-vpn-profiles-to-windows-10------503274--should-be-fixed-by-1802-if-not-sooner---"></a>À compter de la version 1710, vous ne pouvez plus déployer de profils VPN Windows Phone 8.1 sur Windows 10   <!-- 503274  Should be fixed by 1802, if not sooner -->
Dans la version 1710, il n’est plus possible de créer un profil VPN à l’aide du workflow Windows Phone 8.1 qui s’applique aussi aux appareils Windows 10. Pour ces profils, la page Plateformes prises en charge n’est plus affichée dans l’Assistant Création et Windows Phone 8.1 est automatiquement sélectionné sur le back-end ; dans les pages de propriétés, la page Plateformes prises en charge est disponible, mais les options Windows 10 ne sont pas affichées.

**Solution de contournement** : Utilisez le workflow du profil VPN Windows 10 pour les appareils Windows 10. Si ce n’est pas possible pour votre environnement, contactez le support technique. Si nécessaire, le support technique peut vous aider à ajouter le ciblage Windows 10.


### <a name="full-wipe-disables-windows-10-devices-with-less-than-4-gb-ram"></a>Une réinitialisation complète désactive les appareils Windows 10 avec moins de 4 Go de RAM
L’exécution d’une réinitialisation complète sur les appareils Windows 10 RTM (versions antérieures à la version 1511) avec moins de 4 Go de RAM peut rendre l’appareil inutilisable. Après une tentative de réinitialisation de l’appareil, il ne peut pas démarrer et ne répond pas.

**Solution de contournement** : vérifiez que les PC Windows 10 RTM ont au moins 4 Go de RAM disponible avant d’effectuer une réinitialisation complète de l’appareil. Pour afficher le numéro de version des appareils Windows 10, entrez « winver » à partir d’une invite de commandes. Si l’appareil a déjà été réinitialisé et n’est plus réactif, utilisez un lecteur USB Windows 10 démarrable pour démarrer et récupérer l’accès à l’appareil.


### <a name="when-a-user-belongs-to-two-or-more-user-collections-that-a-terms-and-conditions-policy-is-deployed-to-the-user-sees-multiple-sets-of-the-same-terms"></a>Quand un utilisateur appartient à plusieurs regroupements d’utilisateurs pour lesquels une stratégie de conditions générales est déployée, l’utilisateur voit plusieurs ensembles des mêmes conditions générales  
<!-- 454394    -->
Quand un administrateur déploie un ensemble de conditions générales dans plusieurs regroupements d’utilisateurs et qu’un utilisateur est membre de plusieurs de ces regroupements, plusieurs copies identiques des conditions générales lui sont présentées quand il ouvre le portail d’entreprise.  Par exemple, si un utilisateur nommé « Exemple_Utilisateur » est membre de deux regroupements d’utilisateurs différents, l’un nommé « EmployésSociétéFTE » et l’autre « EmployésSociétéNA », et que les conditions générales nommées « ConditionsGénérales » sont déployées vers EmployésSociétéFTE et vers EmployésSociétéNA, Exemple_Utilisateur verra deux ensembles identiques de ConditionsGénérales dans la page d’acceptation des conditions générales. Étant donné que les utilisateurs peuvent uniquement accepter ou refuser toutes les conditions générales, il n’existe aucun risque d’être dans un état d’acceptation ambigu (où l’utilisateur aurait à la fois accepté et refusé les conditions générales). Le rapport d’acceptation des conditions générales comprend une seule ligne par ensemble de conditions générales et par utilisateur. Il ne contient donc aucune erreur. La seule conséquence est que l’utilisateur verra deux ensembles de conditions générales dans la page d’acceptation.  

**Solution de contournement**: assurez-vous que chaque utilisateur appartient à un seul regroupement où les conditions générales sont déployées.  


### <a name="android-for-work-email-profiles-that-use-certificate-authentication-are-not-applied-to-devices"></a>Les profils de messagerie Android for Work qui utilisent l’authentification par certificat ne sont pas appliqués aux appareils
<!--  487657      -->
Lorsqu’un profil de messagerie Android for Work est créé, deux options d’authentification sont disponibles. L’une utilise le nom d’utilisateur et le mot de passe, et l’autre des certificats. À ce stade, l’option des certificats ne fonctionne pas. Si le profil est créé avec la méthode d’authentification définie sur des **certificats**, le profil n’est pas appliqué à l’appareil et l’utilisateur sera invité à saisir manuellement les détails du compte.

**Solution de contournement** : aucune. Les administrateurs doivent utiliser l’option **Nom d’utilisateur et mot de passe**, ou attendre que le problème soit résolu.



<!-- ## Reports and monitoring    -->
<!-- ## Conditional access   -->
<!-- ## Endpoint Protection -->
