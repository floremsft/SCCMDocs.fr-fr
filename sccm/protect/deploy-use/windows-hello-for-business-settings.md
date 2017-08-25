---
title: "Paramètres Windows Hello Entreprise | Microsoft Docs"
description: "Découvrez comment intégrer Windows Hello Entreprise dans System Center Configuration Manager."
ms.custom: na
ms.date: 08/10/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a95bc292-af10-4beb-ab56-2a815fc69304
caps.latest.revision: "17"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 696edcf33936c705984d1168b2f15dd862d90d0e
ms.sourcegitcommit: 4ec2fccb2d471ba9a91fe73df01b7e96efc62594
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/11/2017
---
# <a name="windows-hello-for-business-settings-in-system-center-configuration-manager"></a>Les paramètres Windows Hello Entreprise dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

System Center Configuration Manager permet d’intégrer Windows Hello Entreprise (anciennement Microsoft Passport pour Windows), qui constitue une méthode alternative de connexion pour les appareils Windows 10. Hello Entreprise utilise Active Directory ou un compte Azure Active Directory pour remplacer un mot de passe, une carte à puce ou une carte à puce virtuelle.  

Hello Entreprise vous permet d’utiliser un **geste utilisateur** pour vous connecter, au lieu d’un mot de passe. Un geste utilisateur peut être un simple code confidentiel, une authentification biométrique ou un appareil externe tel qu’un lecteur d’empreintes digitales.

[En savoir plus sur Windows Hello Entreprise](https://docs.microsoft.com/windows/access-protection/hello-for-business/hello-identity-verification)

 Configuration Manager s’intègre avec Windows Hello Entreprise de deux manières :  

-   Vous pouvez utiliser Configuration Manager pour contrôler les gestes que les utilisateurs peuvent et ne peuvent pas utiliser pour se connecter.  

-   Vous pouvez stocker des certificats d’authentification dans le fournisseur de stockage de clés Windows Hello Entreprise. Pour plus d’informations, consultez [Profils de certificat](introduction-to-certificate-profiles.md).  

- Vous pouvez déployer des stratégies Windows Hello Entreprise sur des appareils Windows 10 joints à un domaine qui exécutent le client Configuration Manager. Cette configuration est décrite dans [Configurer Windows Hello Entreprise sur des appareils Windows 10 joints à un domaine](#configure-windows-hello-for-business-on-domain-joined-windows-10-devices), ci-dessous. Lorsque vous utilisez Configuration Manager avec Microsoft Intune (hybride), vous pouvez configurer ces paramètres sur les appareils Windows 10 et Windows 10 Mobile. Pour en savoir plus, voir [Configurer les paramètres de Windows Hello Entreprise (hybride)](../../mdm/deploy-use/windows-hello-for-business-settings.md).

## <a name="configure-windows-hello-for-business-on-domain-joined-windows-10-devices"></a>Configurer Windows Hello Entreprise sur les appareils Windows 10 joints à un domaine
Vous pouvez contrôler les paramètres Windows Hello Entreprise sur les appareils Windows 10 joints à un domaine en créant et en déployant un profil Windows Hello Entreprise. Il s’agit de l’approche recommandée.


Si vous utilisez l’authentification par certificat, vous devez également déployer un profil de certificat, comme le décrit la section [Configurer un profil de certificat](#configure-a-certificate-profile). Si vous utilisez l’authentification par clé, il est inutile de déployer un profil de certificat.

## <a name="configure-a-windows-hello-for-business-profile"></a>Configurer un profil Windows Hello Entreprise  

Dans la console de Configuration Manager, sous **Accès aux ressources de l’entreprise**, cliquez avec le bouton droit sur **Profils Windows Hello for business** et choisissez **Nouveau** pour démarrer l’Assistant de création de profil. Fournissez les paramètres demandés par l’Assistant, passez en revue et confirmez les paramètres de la dernière page, puis cliquez sur **Fermer**. Voici un exemple de ce à quoi vos paramètres peuvent ressembler :  

![Paramètres Windows Hello Entreprise](../media/Hello-for-Business-settings.png)

## <a name="configure-a-certificate-profile-to-enroll-the-windows-hello-for-business-enrollment-certificate-in-configuration-manager"></a>Configurer un profil de certificat pour inscrire le certificat d’inscription Windows Hello Entreprise dans Configuration Manager  
 Si vous souhaitez utiliser l’ouverture de session par certificat Windows Hello Entreprise, configurez les éléments suivants :  

-   Un profil de certificat Configuration Manager.  

-   Dans le profil de certificat, sélectionnez un modèle qui recourt à l’utilisation de clé étendue pour l’ouverture de session avec carte à puce.  

-   Si vous envisagez de stocker des profils de certificat dans le conteneur de clés Windows Hello Entreprise et que le profil de certificat utilise l’utilisation améliorée de la clé pour **l’ouverture de session avec carte à puce**, vous devez configurer les autorisations suivantes pour enregistrer cette clé et garantir que le certificat est validé correctement.
Vous devez avoir au préalable créé le groupe **Administrateurs de clé** et ajouté tous les ordinateurs de point de gestion Configuration Manager comme membres de ce groupe.

Il est possible que certaines configurations ne requièrent pas de configuration des autorisations ou qu’elles nécessitent des configurations supplémentaires. Consultez le tableau suivant pour obtenir une aide supplémentaire :

|||||
|-|-|-|-|
|Version du client Windows|Configuration Manager 1602 ou 1606|Configuration Manager 1610|Configuration Manager 1702 ou version ultérieure|
|Mise à jour anniversaire Windows 10|Pas de correctif logiciel requis<br><br>Pas d’autorisation requise<br><br>Pas de mise à jour de schéma Windows requise|Pas de correctif logiciel requis<br><br>Pas d’autorisation requise<br><br>Pas de mise à jour de schéma Windows requise|Aucune action requise|
|Windows 10 Creators Update ou version ultérieure|Non pris en charge|Installer [ce correctif logiciel](https://support.microsoft.com/help/4010155/update-rollup-for-system-center-configuration-manager-current-branch-v)<br><br>Configurer les autorisations<br><br>Appliquer le schéma de Windows Server 2016 à Active Directory|Configurer les autorisations<br><br>Appliquer le schéma de Windows Server 2016 à Active Directory|

## <a name="to-configure-permissions"></a>Configurer les autorisations

1.  Connectez-vous à un contrôleur de domaine ou à des stations de travail de gestion avec l’administrateur de domaine ou des informations d’identification équivalentes.
2.  Ouvrez **Utilisateurs et ordinateurs Active Directory**.
3.  Dans le volet de navigation, cliquez avec le bouton droit sur votre nom de domaine, puis cliquez sur **Propriétés**.
4.  Sous l’onglet **Sécurité** de la boîte de dialogue **Propriétés** *<domain name>*, cliquez sur **Avancé**. Si l’onglet **Sécurité** n’apparaît pas, activez les **Fonctionnalités avancées** dans le menu **Affichage** de **Utilisateurs et ordinateurs Active Directory**.
5.  Cliquez sur **Ajouter**.
6.  Dans la boîte de dialogue **Saisie des autorisations pour** *<domain name>*, cliquez sur **Sélectionner un principal**.
7.  Dans la boîte de dialogue **Sélectionner un utilisateur, un ordinateur, un compte de service ou un groupe**, tapez **Administrateurs de clé** dans la zone de texte **Entrer le nom de l’objet à sélectionner**.  Cliquez sur **OK**.
8.  Dans la liste **S’applique à**, sélectionnez **Objets utilisateur descendants**.
9.  Faites défiler jusqu’au bas de la page et cliquez sur **Effacer tout**.
10. Dans la section **Propriétés**, sélectionnez **Lire msDS-KeyCredentialLink**.
11. Cliquez sur **OK** trois fois pour terminer la tâche.


## <a name="next-steps"></a>Étapes suivantes

Pour plus d’informations, consultez [Profils de certificat](introduction-to-certificate-profiles.md).  




