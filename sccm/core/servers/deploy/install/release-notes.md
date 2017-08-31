---
title: "Notes de publication - Configuration Manager | Microsoft Docs"
description: "Consultez ces notes pour les problèmes urgents qui ne sont pas encore résolus dans le produit ou traités dans un article de la Base de connaissances Microsoft."
ms.custom: na
ms.date: 08/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 030947fd-f5e0-4185-8513-2397fb2ec96f
caps.latest.revision: "41"
caps.handback.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: e54c2cd1c3e83609bff6a8cb64fb3c23b26a4eaa
ms.sourcegitcommit: 974fbc4408028c8be28911e5cd646efcf47c7f15
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/28/2017
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

### <a name="after-you-update-a-configuration-manager-console-using-consolesetupexe-from-the-site-server-folder-recent-language-pack-changes-are-not-available"></a>Après avoir mis à jour une console Configuration Manager à l’aide du fichier ConsoleSetup.exe du dossier du serveur de site, les dernières modifications du pack linguistique ne sont pas disponibles
<!--  SMS 486420  Applicability should be 1610 and 1702.  -->
*Les éléments suivants s’appliquent aux versions 1610 et 1702.*   
Après une mise à jour sur place exécutée sur une console à l’aide du fichier ConsoleSetup.exe d’un dossier d’installation de serveurs de site, il est possible que les modules linguistiques récemment installés ne soient pas disponibles. Cela se produit lorsque :
- Votre site exécute la version 1610 ou 1702.
- La console est mise à jour sur place à l’aide du fichier ConsoleSetup.exe du dossier d’installation du serveur de site.

Lorsque ce problème se produit, la console réinstallée n’utilise pas la dernière série de modules linguistiques qui ont été configurés. Aucune erreur n’est retournée, mais les modules linguistiques disponibles dans la console n’auront pas changé.  

**Solution de contournement :** désinstallez la console actuelle et réinstallez la console en tant que nouvelle installation. Vous pouvez utiliser le fichier ConsoleSetup.exe du dossier d’installation des serveurs de site. Pendant l’installation, veillez à sélectionner les fichiers du pack linguistique que vous souhaitez utiliser.


### <a name="with-version-1702-the-default-site-boundary-group-is-configured-for-use-for-site-assignment"></a>Avec la version 1702, le groupe de limites de site par défaut est configuré pour une utilisation dans le cadre d’une attribution de site
<!--  SMS 486380   Applicability should only be to 1702. -->
*Les éléments suivants s’appliquent à la version 1702.*  
L’onglet Référence des groupes de limites de site par défaut affiche une coche pour l’option **Utiliser ce groupe de limites pour l'attribution de site**, répertorie le site en tant que **site attribué** et apparaît en grisé indiquant que la configuration ne peut pas être modifiée ou supprimée.

**Solution de contournement :** aucune. Vous pouvez ignorer ce paramètre. Même si le groupe est activé pour l’attribution de site, le groupe de limites de site par défaut n’est pas utilisé pour l’attribution de site. Avec la version 1702, cette configuration garantit que le groupe de limites de site par défaut est associé au site approprié.



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


### <a name="service-connection-tool-throws-an-exception-when-sql-server-is-remote-or-when-shared-memory-is-disabled"></a>L’outil de connexion de service lève une exception quand le serveur SQL Server est distant ou quand la mémoire partagée est désactivée
<!-- 479223   Fixed in 1702 and later   -->
*Les éléments suivants s’appliquent à la version 1610 et versions antérieures.*  
L’outil de connexion de service génère une exception si l’une des conditions suivantes s’applique :  
 -  Votre base de données de site est distante de l’ordinateur qui héberge le point de connexion de service et utilise un port non standard (autre que le port 1433)
 -  Votre base de données de site se trouve sur le même serveur que le point de connexion de service, mais l’option **Mémoire partagée** du protocole SQL est désactivée

L’exception est semblable à la suivante :
 - *Exception non prise en charge : System.Data.SqlClient.SqlException : Une erreur liée au réseau ou spécifique à l’instance s’est produite lors de l’établissement d’une connexion à SQL Server. Le serveur est introuvable ou n’est pas accessible. Vérifiez que le nom de l’instance est correct et que SQL Server est configuré pour autoriser les connexions distantes. (fournisseur : Fournisseur de canaux nommés, erreur : 40 - Impossible d’ouvrir une connexion à SQL Server) --*

**Solution de contournement** : quand vous utilisez l’outil, vous devez modifier le Registre du serveur qui héberge le point de connexion de service de manière à inclure des informations sur le port SQL Server :

   1.   Avant d’utiliser l’outil, modifiez la clé de Registre suivante et ajoutez le numéro du port utilisé au nom du serveur SQL Server :
    - Clé : HKLM\Microsoft\SMS\COMPONENTS\SMS_DMP_UPLOADER\
      - Valeur : &lt;nom du serveur SQL Server>
    - Ajoutez : **,&lt;PORT>**

    Par exemple, pour ajouter le port *15001* à un serveur nommé *testserver.test.net*, la clé résultante est la suivante : ***HKLM\Software\Microsoft\SMS\COMPONENTS\SMS_DMP_UPLOADER\testserver.test.net,15001***

   2.   Une fois le port ajouté au Registre, l’outil doit fonctionner normalement.  

   3.   Quand vous avez terminé d’utiliser l’outil, pour les étapes **-connect** et **-import**, rétablissez la valeur d’origine de la clé de Registre.  


<!-- ## Backup and recovery  -->


## <a name="client-deployment-and-upgrade"></a>Mise à niveau et déploiement du client  

### <a name="client-installation-fails-with-error-code-0x8007064c"></a>L’installation du client échoue avec le code d’erreur 0x8007064c
<!--- SMS 486973  applies 1606 to 1706. Not yet fixed. -->
*Les éléments suivants s’appliquent à toutes les versions actives de Configuration Manager.*   
Lorsque vous déployez le client sur des ordinateurs Windows, l’installation échoue. Le fichier ccmsetup.log contient une entrée « File 'C:\WINDOWS\ccmsetup\Silverlight.exe' returned failure exit code 1612. Fail the installation » suivie de "InstallFromManifest failed 0x8007064c ».

**Solution de contournement** Cette erreur est due à une version endommagée de Silverlight, précédemment installée. Vous pouvez essayer d’exécuter l’outil suivant sur l’ordinateur concerné pour résoudre ce problème : [https://support.microsoft.com/help/17588/fix-problems-that-block-programs-from-being-installed-or-removed](https://support.microsoft.com/help/17588/fix-problems-that-block-programs-from-being-installed-or-removed)

## <a name="operating-system-deployment"></a>Déploiement du système d'exploitation  

### <a name="if-the-boot-image-contains-drivers-the-image-fails-to-reload-the-current-windows-pe-version-from-the-windows-assessment-and-deployment-kit-adk"></a>Si l’image de démarrage contient des pilotes, l’image ne parvient pas à recharger la version actuelle de Windows PE à partir du Kit de déploiement et d’évaluation Windows (ADK)
<!-- 495087 -->
Vous pouvez utiliser l’Assistant Mise à jour de point de distribution pour mettre à jour les points de distribution grâce à une image de démarrage stockée avec la dernière version de Windows PE dans le répertoire d’installation du Kit de déploiement et d’évaluation Windows (ADK). Pour effectuer la mise à jour, ouvrez l’Assistant Mise à jour de point de distribution et sélectionnez **Recharger cette image de démarrage avec la version actuelle de PE à partir de Windows ADK**.

Toutefois, si votre image de démarrage contient des pilotes, la mise à jour échoue. L’Assistant recharge l’image à partir de l’ADK et affiche une boîte de dialogue d’exception, que l’utilisateur peut ignorer, puis un écran de réussite. Toutefois, les derniers composants du client Gestionnaire de configuration ne seront pas ajoutés à l’image de démarrage. Celle-ci ne sera pas mise à jour sur le point de distribution.

**Solution de contournement** : exécutez deux fois l’Assistant Mise à jour de point de distribution.

1. Exécutez l’Assistant en sélectionnant **Recharger cette image de démarrage avec la version actuelle de Windows PE à partir de Windows ADK**. Vous obtiendrez la dernière version de Windows PE.
2. Exécutez à nouveau l’Assistant sans sélectionner **Recharger cette image de démarrage avec la version actuelle de Windows PE à partir de Windows ADK**. Vous obtiendrez la dernière version des binaires du client, et l’image de démarrage sera mise à jour sur le point de distribution.

### <a name="servicing-plans-create-a-lot-of-duplicate-software-update-groups-and-deployments-by-default"></a>Les plans de maintenance créent un grand nombre de groupes et de déploiements de mises à jour logicielles en double  
Par défaut, l’Assistant Créer un plan de maintenance s’exécute actuellement après chaque synchronisation des mises à jour logicielles. Chaque fois que l’Assistant s’exécute, il crée un groupe et un déploiement de mises à jour logicielles. Par exemple, si vous avez une planification de la synchronisation des mises à jour logicielles qui s’exécute plusieurs fois par jour, l’Assistant Créer un plan de maintenance génère quotidiennement plusieurs groupes et déploiements de mises à jour logicielles, probablement identiques.  

**Solution de contournement** :    
après avoir créé un plan de maintenance, ouvrez les propriétés de celui-ci, accédez à l’onglet **Calendrier d’évaluation**, sélectionnez **Exécuter la règle dans un calendrier**, cliquez sur **Personnaliser**, puis créez un calendrier personnalisé. Par exemple, vous pouvez faire en sorte que le plan de maintenance s’exécute tous les 60 jours.  


### <a name="when-a-high-risk-deployment-dialog-is-visible-to-a-user-subsequent-high-risk-dialogs-with-a-sooner-deadline-are-not-displayed"></a>Quand une boîte de dialogue de déploiement à haut risque est visible pour l’utilisateur, les boîtes de dialogue à haut risque ultérieures avec une échéance plus courte ne sont pas affichées
<!-- Fixed in 1702 and later -->
*Les éléments suivants s’appliquent à la version 1610 et versions antérieures.*   
Une fois que vous avez créé et déployé un déploiement de tâches à haut risque sur les utilisateurs, une boîte de dialogue à haut risque s’affiche pour l’utilisateur. Si l’utilisateur ne ferme pas la boîte de dialogue et que vous créez et déployez un autre déploiement à haut risque avec une échéance plus courte que la première, l’utilisateur ne reçoit pas de boîte de dialogue mise à jour tant qu’il ne ferme pas la boîte de dialogue d’origine. Les déploiements continuent de s’exécuter selon les échéances configurées.

**Solution de contournement** :  
L’utilisateur doit fermer la boîte de dialogue pour que le premier déploiement à haut risque affiche la boîte de dialogue du déploiement à haut risque suivant.



## <a name="software-updates"></a>Mises à jour logicielles

### <a name="importing-an-office-365-client-settings-from-a-configuration-file-fails-when-it-contains-unsupported-languages"></a>L’importation des paramètres d’un client Office 365 à partir d’un fichier de configuration échoue s’il contient des langages non pris en charge
<!-- 489258  Fixed in 1706  -->
*Les éléments suivants s’appliquent à la version 1702 et versions antérieures.*   
Lorsque vous importez les paramètres d’un client Office 365 à partir d’un fichier de configuration XML existant et que le fichier contient des langues qui ne sont pas prises en charge par le client Office 365 ProPlus, une erreur se produit. Pour plus d’informations, voir [Déployer des applications Office 365 sur des clients depuis le tableau de bord Gestion des clients Office 365](/sccm/sum/deploy-use/manage-office-365-proplus-updates#to-deploy-office-365-apps-to-clients-from-the-office-365-client-management-dashboard).

**Solution de contournement** :    
Utilisez uniquement les [langues prises en charge par le client Office 365 ProPlus](https://technet.microsoft.com/library/cc179219&#40;v=office.16&#41;.aspx) dans le fichier de configuration XML.  



## <a name="mobile-device-management"></a>Gestion des appareils mobiles  

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


## <a name="endpoint-protection"></a>Endpoint Protection

### <a name="antimalware-policy-fails-to-apply-on-windows-server-2016-core"></a>La stratégie de logiciel anti-programme malveillant ne parvient pas à s’appliquer sur Windows Server 2016 Core
<!--  Product Studio bug 485370 added 04 19 2017   Fixed in 1702 -->
*Les éléments suivants s’appliquent à la version 1610 et versions antérieures.*  
La stratégie de logiciel anti-programme malveillant ne parvient pas à s’appliquer sur Windows Server 2016 Core.  Le code d’erreur est 0x80070002.  Il existe une dépendance manquante pour ConfigSecurityPolicy.exe.

**Solution de contournement :** Ce problème est résolu par [l’article 4019472 de la Base de connaissances](https://support.microsoft.com/help/4019472/windows-10-update-kb4019472) publié le 9 mai 2017.


### <a name="windows-defender-advanced-threat-protection-policies-fail-on-older-client-agents"></a>Les stratégies Windows Defender Advanced Threat Protection (ATP) échouent sur les agents de clients plus anciens
<!-- Product Studio bug 462286 added  05 25 2017 and valid until July 2017 GA release      Fixed in 1610 -->
Les stratégies Windows Defender Advanced Threat Protection créées à partir d’un serveur de site Configuration Manager 1610 ou version ultérieure ne seront pas appliquées à Configuration Manager version 1606 et les clients antérieurs.  Les clients ne sont pas embarqués et l’évaluation de la stratégie signale une erreur. L**’état du déploiement** dans la configuration Windows Defender Advanced Threat Protection affiche **Erreur**.

**Solution de contournement** : mettez à niveau le client Configuration Manager avec la version 1610 ou ultérieure.
