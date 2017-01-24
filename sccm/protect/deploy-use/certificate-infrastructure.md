---
title: "Configuration de l’infrastructure de certificats | Microsoft Docs"
description: "Découvrez comment configurer l’inscription de certificats dans System Center Configuration Manager."
ms.custom: na
ms.date: 10/10/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 29ae59b7-2695-4a0f-a9ff-4f29222f28b3
caps.latest.revision: 7
caps.handback.revision: 0
author: Nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: bff083fe279cd6b36a58305a5f16051ea241151e
ms.openlocfilehash: 56e0a1923305c5134386623b1e306b8ebd013d53

---
# <a name="certificate-infrastructure"></a>Infrastructure de certificats

*S’applique à : System Center Configuration Manager (Current Branch)*


 Voici les étapes, détails et informations complémentaires relatifs à la configuration de l’inscription de certificats dans System Center Configuration Manager. Avant de commencer, examinez les conditions requises répertoriées dans [Configuration requise pour les profils de certificat dans System Center Configuration Manager](../../protect/plan-design/prerequisites-for-certificate-profiles.md).  

 Lorsque vous avez terminé ces étapes et vérifié l'installation, vous pouvez configurer et déployer des profils de certificat. Pour plus d’informations, consultez [Comment créer des profils de certificat dans System Center Configuration Manager](../../protect/deploy-use/create-certificate-profiles.md).  


**Étape 1 :** Installer et configurer le service d’inscription d’appareils réseau et les dépendances. Le service de rôle du service d'inscription d'appareils réseau pour les services de certificats Active Directory (AD CS) doivent s'exécuter sur le système d'exploitation Windows Server 2012 R2.
     **Important :** Vous devez suivre des étapes de configuration supplémentaires pour pouvoir utiliser le service d’inscription d’appareils réseau avec System Center Configuration Manager.
**Étape 2 :** Installer et configurer le point d’enregistrement de certificat. Vous devez installer au moins un point d'enregistrement de certificat. Ce point d'enregistrement peut être sur un site d'administration centrale ou un site principal.
**Étape 3 :** Installer le module de stratégie de System Center Configuration Manager. Installez le module de stratégie sur le serveur exécutant le service d'inscription d'appareils réseau.

## <a name="supplemental-procedures-to-configure-certificate-enrollment-in-configuration-manager"></a>Procédures supplémentaires relatives à la configuration de l'inscription de certificats dans Configuration Manager  
 Utilisez les informations suivantes lorsque les étapes décrites dans le tableau précédent nécessitent des procédures supplémentaires.  

###  <a name="step-1-install-and-configure-the-network-device-enrollment-service-and-dependencies"></a>Étape 1 : Installer et configurer le service d'inscription d'appareils réseau et les dépendances  
 Vous devez installer et configurer le service de rôle du service d'inscription d'appareils réseau pour les services de certificat Active Directory (AD CS), modifier les autorisations de sécurité sur les modèles de certificat, déployer un certificat d'authentification de client PKI et modifier le Registre pour augmenter la taille limite des URL IIS par défaut. Si nécessaire, vous devez aussi configurer l'Autorité de certification (CA) émettrice pour autoriser une période de validité personnalisée.  

> [!IMPORTANT]  
>  Avant de configurer System Center Configuration Manager pour fonctionner avec le service d’inscription d’appareils réseau, vérifiez l’installation et la configuration de ce dernier. Si ces dépendances ne fonctionnent pas correctement, vous aurez des difficultés à résoudre les problèmes d’inscription de certificats à l’aide de System Center Configuration Manager.  

##### <a name="to-install-and-configure-the-network-device-enrollment-service-and-dependencies"></a>Pour installer et configurer le service d'inscription d'appareils réseau et les dépendances  

1.  Sur un serveur exécutant Windows Server 2012 R2, installez et configurez le service de rôle du service d'inscription d'appareils réseau pour le rôle de serveur des services de certificats Active Directory. Pour plus d'informations, voir [Network Device Enrollment Service Guidance (Guide du service d'inscription d'appareils réseau)](http://go.microsoft.com/fwlink/p/?LinkId=309016) dans la bibliothèque des services de certificats Microsoft Active Directory sur TechNet.  

2.  Vérifiez et, si nécessaire, modifiez les autorisations de sécurité des modèles de certificat utilisés par le service d'inscription d'appareils réseau :  

    -   Pour le compte qui exécute la console System Center Configuration Manager : droit d’accès en **lecture**.  

         Cette autorisation est requise afin que vous puissiez rechercher et sélectionner le modèle de certificat à utiliser pour créer un profil de paramètres SCEP lorsque vous exécutez l'Assistant de création d'un profil de certificat. La sélection d'un modèle de certificat signifie que certains paramètres dans l'Assistant sont automatiquement renseignés pour vous. Les tâches de configuration sont réduites, ainsi que les risques de sélection de paramètres non compatibles avec les modèles de certificat utilisés par le service d'inscription d'appareils réseau.  

    -   Pour le compte de service SCEP que le pool d'applications du service d'inscription d'appareils réseau utilise : Autorisations **Lecture** et **Inscription** .  

         Cette exigence n’est pas spécifique à System Center Configuration Manager, mais elle fait partie de la configuration du service d’inscription d’appareils réseau. Pour plus d'informations, voir [Network Device Enrollment Service Guidance (Guide du service d'inscription d'appareils réseau)](http://go.microsoft.com/fwlink/p/?LinkId=309016) dans la bibliothèque des services de certificats Microsoft Active Directory sur TechNet.  

    > [!TIP]  
    >  Pour identifier les modèles de certificat utilisés par le service d’inscription de périphérique réseau, affichez la clé de Registre suivante sur le serveur exécutant le service d’inscription de périphérique réseau : HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Cryptography\MSCEP.  

    > [!NOTE]  
    >  Ces autorisations de sécurité sont les valeurs par défaut appropriées pour la plupart des environnements. Toutefois, vous pouvez utiliser une autre configuration de sécurité. Pour plus d’informations, consultez [Planification d’autorisations de modèles de certificat pour les profils de certificat dans System Center Configuration Manager](../../protect/plan-design/planning-for-certificate-template-permissions.md).  

3.  Déployez vers ce serveur un certificat PKI prenant en charge l'authentification du client. Vous disposez peut-être déjà d'un certificat adapté installé sur l'ordinateur, que vous pouvez utiliser, ou vous devez (ou préférez) déployer un certificat spécifique. Pour plus d’informations sur la configuration requise de ce certificat, consultez « Serveurs exécutant le module de stratégie de Configuration Manager avec le service de rôle du service d’inscription d’appareils réseau » dans la section **Certificats PKI pour serveurs** de la rubrique [Configuration requise des certificats PKI pour System Center Configuration Manager](../../core/plan-design/network/pki-certificate-requirements.md).  

    > [!TIP]  
    >  Pour obtenir de l’aide pour le déploiement de ce certificat, suivez les instructions dans la section [Déploiement du certificat client pour les points de distribution](/sccm/core/plan-design/network/example-deployment-of-pki-certificates#BKMK_clientdistributionpoint2008_cm2012), car les exigences relatives au certificat sont identiques, à une exception près :  
    >   
    >  -   N'activez pas la case à cocher **Autoriser l'exportation de la clé privée** dans l'onglet **Traitement de la demande** des propriétés du modèle de certificat.  
    >   
    >  Vous n’avez pas à exporter ce certificat avec la clé privée, car vous pouvez le rechercher dans le magasin de l’ordinateur local et le sélectionner lors de la configuration du module de stratégie de System Center Configuration Manager.  

4.  Localisez le certificat racine auquel est lié le certificat d'authentification. Exportez ensuite ce certificat d'Autorité de certification racine dans un fichier de certificat (.cer). Enregistrez ce fichier dans un emplacement sécurisé auquel vous pouvez accéder en toute sécurité lorsque plus tard vous installez et configurez le serveur de système de site du point d'enregistrement de certificat.  

5.  Sur le même serveur, utilisez l’Éditeur du Registre pour augmenter la taille limite des URL IIS par défaut en définissant les valeurs DWORD de clés de Registre suivantes dans HKEY_LOCAL_MACHINE\System\CurrentControlSet\Services\HTTP\Parameters :  

    -   Définissez la clé **MaxFieldLength** à **65534**.  

    -   Définissez la clé **MaxRequestBytes** à **16777216**.  

     Pour plus d'informations, consultez l'article [820129 : Paramètres de Registre Http.sys pour Windows](http://go.microsoft.com/fwlink/?LinkId=309013) dans la Base de connaissances Microsoft.  

6.  Sur le même serveur, dans le Gestionnaire des services Internet (IIS), modifiez les paramètres de filtrage des demandes pour l'application /certsrv/mscep, puis redémarrez le serveur. Dans la boîte de dialogue **Modifier les paramètres de filtrage des demandes** , les paramètres **Limites des demandes** doivent se présenter comme suit :  

    -   **Longueur maximale autorisée du contenu (octets)**: **30 000 000**  

    -   **Longueur maximale des URL (octets)**: **65 534**  

    -   **Longueur maximale des chaînes de requête (octets)**: **65 534**  

     Pour plus d'informations sur ces paramètres et sur la façon de les configurer, voir [Limites des demandes](http://go.microsoft.com/fwlink/?LinkId=309014) dans la bibliothèque de référence IIS.  

7.  Si vous souhaitez pouvoir demander un certificat avec une durée de validité inférieure à celle du modèle de certificat que vous utilisez : Cette configuration est désactivée par défaut pour une Autorité de certification d'entreprise. Pour activer cette option pour une Autorité de certification d'entreprise, utilisez l'outil de ligne de commande Certutil, puis arrêtez et redémarrez le service de certificats à l'aide des commandes suivantes :  

    1.  **certutil - setreg Policy\EditFlags +EDITF_ATTRIBUTEENDDATE**  

    2.  **net stop certsvc**  

    3.  **net start certsvc**  

     Pour plus d'informations, voir [Outils et paramètres des services de certificat](http://go.microsoft.com/fwlink/p/?LinkId=309015) dans la bibliothèque des technologies PKI sur TechNet.  

8.  Vérifiez que le service d'inscription d'appareils réseau fonctionne en utilisant le lien suivant comme exemple : **https://server.contoso.com/certsrv/mscep/mscep.dll**. Vous devriez voir la page Web intégrée Service d'inscription d'appareils réseau. Cette page explique ce qu'est le service et explique que les appareils réseau utilisent l'URL pour soumettre des demandes de certificat.  

 Maintenant que le service d'inscription d'appareils réseau et les dépendances sont configurés, vous êtes prêt à installer et à configurer le point d'enregistrement de certificat.  

###  <a name="step-2-install-and-configure-the-certificate-registration-point"></a>Étape 2 : Installer et configurer le point d'enregistrement de certificat  
 Vous devez installer et configurer au moins un point d’enregistrement de certificat dans la hiérarchie System Center Configuration Manager et vous pouvez installer ce rôle de système de site dans le site d’administration centrale ou dans un site principal.  

> [!IMPORTANT]  
>  Avant d'installer le point d'enregistrement de certificat, consultez la section **Configuration requise pour le système de site** de la rubrique [Configurations prises en charge pour System Center Configuration Manager](../../core/plan-design/configs/supported-configurations.md) pour la configuration de système d'exploitation requise et les dépendances du point d'enregistrement de certificat.  

##### <a name="to-install-and-configure-the-certificate-registration-point"></a>Pour installer et configurer le point d'enregistrement de certificat  

1.  Dans la console System Center Configuration Manager, cliquez sur **Administration**.  

2.  Dans l'espace de travail **Administration** , développez **Configuration du site**, cliquez sur **Serveurs et rôles de système de site**, puis sélectionnez le serveur à utiliser pour le point d'enregistrement de certificat.  

3.  Sous l'onglet **Accueil** , dans le groupe **Serveur** , cliquez sur **Ajouter des rôles de système de site**.  

4.  Sur la page **Général** , spécifiez les paramètres généraux du système de site, puis cliquez sur **Suivant**.  

5.  Sur la page **Proxy** , cliquez sur **Suivant**. Le point d'enregistrement de certificat n'utilise pas les paramètres de proxy Internet.  

6.  Sur la page **Sélection du rôle système** , sélectionnez **Point d'enregistrement de certificat** dans la liste des rôles disponibles, puis cliquez sur **Suivant**.  

7.  Sur la page **Point d'enregistrement de certificat** , acceptez ou modifiez les paramètres par défaut, puis cliquez sur **Ajouter**.  

8.  Dans la boîte de dialogue **Ajouter une URL et un certificat d'Autorité de certification racine** , spécifiez les options suivantes, puis cliquez sur **OK**:  

    1.  **URL du service d’inscription de périphériques réseau** : spécifiez l’URL au format suivant : https://*<FQDN_serveur>*/certsrv/mscep/mscep.dll. Par exemple, si le nom de domaine complet de votre serveur exécutant le service d'inscription d'appareils réseau est server1.contoso.com, entrez **https://server1.contoso.com/certsrv/mscep/mscep.dll**.  

    2.  **Certificat d'Autorité de certification racine**: Recherchez et sélectionnez le fichier de certificat (.cer) que vous avez créé et enregistré à l' **Étape 1 : Installer et configurer le service d'inscription d'appareils réseau et les dépendances**. Ce certificat d’autorité de certification racine permet au point d’enregistrement de certificat de valider le certificat d’authentification client que le module de stratégie de System Center Configuration Manager va utiliser.  

    > [!NOTE]  
    >  Si vous utilisez plusieurs serveurs exécutant le service d'inscription d'appareils réseau, cliquez sur **Ajouter** pour spécifier les détails de chaque serveur.  

9. Cliquez sur **Suivant** pour terminer l'Assistant.  

10. Attendez quelques minutes pour permettre à l'installation de se terminer, puis vérifiez que le point d'enregistrement de certificat est installé correctement, en utilisant l'une des méthodes suivantes :  

    -   Dans l'espace de travail **Surveillance** , développez **État du système**, cliquez sur **État du composant**, puis recherchez des messages d'état provenant du composant **SMS_CERTIFICATE_REGISTRATION_POINT** .  

    -   Sur le serveur de système de site, utilisez le fichier *<chemin_installation_ConfigMgr\>*\Logs\crpsetup.log et le fichier *<chemin_installation_ConfigMgr\>*\Logs\crpmsi.log. Une installation réussie renvoie un code de sortie 0.  

    -   À l’aide d’un navigateur, vérifiez que vous pouvez vous connecter à l’URL du point d’enregistrement de certificat, par exemple https://server1.contoso.com/CMCertificateRegistration. Vous devez voir une page **Erreur de serveur** pour le nom de l'application, avec une description HTTP 404.  

11. Recherchez le fichier de certificat exporté pour l’autorité de certification racine, créé automatiquement par le point d’enregistrement de certificat dans le dossier suivant sur l’ordinateur du serveur de site principal : *<chemin_installation_ConfigMgr\>*\inboxes\certmgr.box. Enregistrez ce fichier à un emplacement sécurisé auquel vous pouvez accéder en toute sécurité si vous installez plus tard le module de stratégie de System Center Configuration Manager sur le serveur exécutant le service d’inscription d’appareils réseau.  

    > [!TIP]  
    >  Ce certificat n'est pas immédiatement disponible dans ce dossier. Vous devrez peut-être attendre un certain temps (par exemple, une demi-heure) avant que System Center Configuration Manager ne copie le fichier à cet emplacement.  

 Maintenant que le point d’enregistrement de certificat est installé et configuré, vous êtes prêt à installer le module de stratégie de System Center Configuration Manager pour le service d’inscription d’appareils réseau.  

###  <a name="step-3-install-the-configuration-manager-policy-module"></a>Étape 3 : Installer le module de stratégie de Configuration Manager  
 Vous devez installer et configurer le module de stratégie de System Center Configuration Manager sur chaque serveur que vous avez spécifié à l’**étape 2 : Installer et configurer le point d’enregistrement de certificat** en tant qu’**URL du service d’inscription d’appareils réseau** dans les propriétés du point d’enregistrement de certificat.  

##### <a name="to-install-the-policy-module"></a>Pour installer le module de stratégie  

1.  Sur le serveur qui exécute le service d’inscription d’appareils réseau, connectez-vous en tant qu’administrateur de domaine et copiez les fichiers suivants du dossier <support_installation_ConfigMgr\>\SMSSETUP\POLICYMODULE\X64 sur le support d’installation System Center Configuration Manager vers un dossier temporaire :  

    -   PolicyModule.msi  

    -   PolicyModuleSetup.exe  

     En outre, si vous avez un dossier LanguagePack sur le support d'installation, copiez ce dossier et son contenu.  

2.  À partir du dossier temporaire, exécutez le fichier PolicyModuleSetup.exe pour démarrer l’Assistant Installation du module de stratégie de System Center Configuration Manager.  

3.  Sur la page initiale de l'Assistant, cliquez sur **Suivant**, acceptez le termes du contrat de licence, puis cliquez sur **Suivant**.  

4.  Sur la page **Dossier d'installation** , acceptez le dossier d'installation par défaut pour le module de stratégie ou spécifiez un autre dossier, puis cliquez sur **Suivant**.  

5.  Sur la page **Point d'enregistrement de certificat** , spécifiez l'URL du point d'enregistrement de certificat en utilisant le nom de domaine complet du serveur de système de site et le nom de l'application virtuelle qui est indiqué dans les propriétés du point d'enregistrement de certificat. Le nom de l'application virtuelle par défaut est CMCertificateRegistration. Par exemple, si le nom de domaine complet du serveur de système de site est server1.contoso.com et que vous avez utilisé le nom de l'application virtuelle par défaut, spécifiez **https://server1.contoso.com/CMCertificateRegistration**.  

6.  Acceptez le port par défaut **443** ou spécifiez l'autre numéro de port utilisé par le point d'enregistrement de certificat, puis cliquez sur **Suivant**.  

7.  Dans la page **Certificat client du module de stratégie**, recherchez et spécifiez le certificat d'authentification client que vous avez déployé à l' **Étape 1 : Installer et configurer le service d'inscription d'appareils réseau et les dépendances**, puis cliquez sur **Suivant**.  

8.  Dans la page **Certificat du point d'enregistrement de certificat** , cliquez sur **Parcourir** pour sélectionner le fichier de certificat exporté pour l'autorité de certification racine que vous avez localisé et enregistré à la fin de l' **Étape 2 : Installer et configurer le point d'enregistrement de certificat**.  

    > [!NOTE]  
    >  Si vous n’avez pas enregistré ce fichier de certificat précédemment, il se trouve dans <chemin_installation_ConfigMgr\>\inboxes\certmgr.box sur l’ordinateur du serveur de site.  

9. Cliquez sur **Suivant** pour terminer l'Assistant.  

 Maintenant que vous avez terminé les étapes de configuration pour installer le service d’inscription d’appareils réseau et les dépendances, le point d’enregistrement de certificat et le module de stratégie de System Center Configuration Manager, vous êtes prêt à déployer les certificats sur les utilisateurs et les appareils en créant et en déployant des profils de certificat. Pour plus d’informations sur la création de profils de certificat, consultez [Comment créer des profils de certificat dans System Center Configuration Manager](../../protect/deploy-use/create-certificate-profiles.md).  

 Si vous souhaitez désinstaller le module de stratégie de System Center Configuration Manager, utilisez **Programmes et fonctionnalités** dans le Panneau de configuration.  



<!--HONumber=Dec16_HO3-->


