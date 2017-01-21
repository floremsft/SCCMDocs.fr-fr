---
title: "Paramètres Windows Hello Entreprise | Microsoft Docs"
description: "Découvrez comment intégrer Windows Hello Entreprise dans System Center Configuration Manager."
ms.custom: na
ms.date: 10/10/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a95bc292-af10-4beb-ab56-2a815fc69304
caps.latest.revision: 17
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: bff083fe279cd6b36a58305a5f16051ea241151e
ms.openlocfilehash: 1f254ee31bae1c3d7b1506e68c40baf78793bf66


---
# <a name="windows-hello-for-business-settings-in-system-center-configuration-manager"></a>Les paramètres Windows Hello Entreprise dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

System Center Configuration Manager permet d’intégrer Windows Hello Entreprise (anciennement Microsoft Passport pour Windows), qui constitue une méthode alternative de connexion pour les appareils Windows 10. Hello Entreprise utilise Active Directory ou un compte Azure Active Directory pour remplacer un mot de passe, une carte à puce ou une carte à puce virtuelle.  

Hello Entreprise vous permet d’utiliser un **geste utilisateur** pour vous connecter, au lieu d’un mot de passe. Un geste utilisateur peut être un simple code confidentiel, une authentification biométrique ou un appareil externe tel qu’un lecteur d’empreintes digitales.  

 Configuration Manager s’intègre avec Windows Hello Entreprise de deux manières :  

-   Vous pouvez utiliser Configuration Manager pour contrôler les gestes que les utilisateurs peuvent et ne peuvent pas utiliser pour se connecter.  

-   Vous pouvez stocker des certificats d’authentification dans le fournisseur de stockage de clés Windows Hello Entreprise. Pour plus d’informations, consultez [Profils de certificat](introduction-to-certificate-profiles.md).  

- Vous pouvez déployer des stratégies Windows Hello Entreprise sur des appareils Windows 10 joints à un domaine qui exécutent le client Configuration Manager. Cette configuration est décrite dans [Configurer Windows Hello Entreprise sur des appareils Windows 10 joints à un domaine](#configure-windows-hello-for-business-on-domain-joined-windows-10-devices), ci-dessous. Lorsque vous utilisez Configuration Manager avec Intune (hybride), vous pouvez configurer ces paramètres sur les appareils Windows 10 et Windows 10 Mobile, mais pas sur les appareils joints à un domaine qui exécutent le client Configuration Manager.   

## <a name="configure-windows-hello-for-business-settings-hybrid"></a>Configurer les paramètres Windows Hello Entreprise (hybride)  

1.  Dans la console Configuration Manager, cliquez sur **Administration** > **Services cloud** > **Abonnements Microsoft Intune**.  

3.  Dans la liste, sélectionnez votre abonnement Microsoft Intune, puis, sous l’onglet **Accueil** , dans le groupe **Abonnement** , cliquez sur **Configurer des plateformes** > **Windows (MDM)**.  

4.  Sous l’onglet **Windows Hello Entreprise** de la boîte de dialogue **Propriétés de l’abonnement Microsoft Intune** , choisissez parmi les valeurs suivantes celles que vous voulez appliquer à tous les appareils Windows 10 et Windows 10 Mobile inscrits :  

    -   **Désactiver Windows Hello Entreprise sur les appareils inscrits** ou **Activer Windows Hello Entreprise sur les appareils inscrits** : active ou désactive l’utilisation de Windows Hello Entreprise sur tous les appareils Windows 10 et Windows 10 Mobile inscrits.  

    -   **Utiliser un module de plateforme sécurisée (TPM)** : une puce de module de plateforme sécurisée (TPM) fournit une couche supplémentaire de sécurité des données. Choisissez l'une des valeurs suivantes :  

        -   **Requis** (par défaut) : seuls les appareils avec un module de plateforme sécurisée accessible peuvent configurer Windows Hello Entreprise.  

        -   **Préféré** : les appareils tentent d’abord d’utiliser un module de plateforme sécurisée. Si ce n’est pas possible, ils peuvent utiliser un chiffrement logiciel.  

    -   **Exiger une longueur minimale du code confidentiel** : spécifiez le nombre minimal de caractères nécessaire pour le code confidentiel Windows Hello Entreprise. Vous devez utiliser au moins 4 caractères (la valeur par défaut est 6 caractères).  

    -   **Exiger une longueur maximale du code confidentiel** : spécifiez le nombre maximal de caractères autorisé pour le code confidentiel Windows Hello Entreprise. Vous pouvez entrer jusqu’à 127 caractères.  

    -   **Exiger des minuscules dans le code confidentiel** : spécifie si des lettres minuscules doivent être utilisées dans le code confidentiel Windows Hello Entreprise. Choisissez parmi :  

        -   **Autorisé** : les utilisateurs peuvent utiliser des minuscules dans leur code confidentiel.  

        -   **Requis** : les utilisateurs doivent inclure au moins un caractère en minuscule dans leur code confidentiel.  

        -   **Non autorisé** (par défaut) : les utilisateurs ne doivent pas utiliser de caractères minuscules dans leur code confidentiel.  

    -   **Exiger des majuscules dans le code confidentiel** : spécifie si des lettres majuscules doivent être utilisées dans le code confidentiel Windows Hello Entreprise. Choisissez parmi :  

        -   **Autorisé** : les utilisateurs peuvent utiliser des majuscules dans leur code confidentiel.  

        -   **Requis** : les utilisateurs doivent inclure au moins un caractère en majuscule dans leur code confidentiel.  

        -   **Non autorisé** (par défaut) : les utilisateurs ne doivent pas utiliser de caractères majuscules dans leur code confidentiel.  

    -   **Exiger des caractères spéciaux** : spécifie l’utilisation de caractères spéciaux dans le code confidentiel. Choisissez parmi :  

        -   **Autorisé** : les utilisateurs peuvent utiliser des caractères spéciaux dans leur code confidentiel.  

        -   **Requis** : les utilisateurs doivent inclure au moins un caractère spécial dans leur code confidentiel.  

        -   **Non autorisé** (par défaut) : les utilisateurs ne doivent pas utiliser de caractères spéciaux dans leur code confidentiel (ce comportement vaut également si le paramètre n’est pas configuré).  

         Les caractères spéciaux incluent : **! " # $ % & ’ ( ) \* + , - . / : ; < = > ? @ [ \ ] ^ _ ` { &#124; } ~**.  

    -   **Exiger un délai d’expiration du code confidentiel (en jours)** : spécifie le nombre de jours avant de devoir modifier le code confidentiel de l’appareil. La valeur par défaut est 41 jours.  

    -   **Empêcher la réutilisation de codes confidentiels précédents** : utilisez ce paramètre pour limiter la réutilisation des codes confidentiels précédemment utilisés. Par défaut, les 5 derniers codes confidentiels utilisés ne peuvent pas être réutilisés.  

    -   **Activer les mouvements biométriques** : permet d’utiliser l’authentification biométrique, telle que la reconnaissance des visages ou les empreintes digitales, à la place d’un code confidentiel pour Windows Hello Entreprise. Les utilisateurs doivent toujours configurer un code confidentiel professionnel en cas d’échec de l’authentification biométrique.  

         Si vous choisissez **Activé**, Windows Hello Entreprise autorise l’authentification biométrique.  Si vous choisissez **Désactivé**, Windows Hello Entreprise empêche l’authentification biométrique (pour tous les types de compte).  

    -   **Utiliser la détection d’usurpation avancée, si disponible** : détermine si la détection d’usurpation avancée est utilisée sur les appareils qui la prennent en charge.  

         Si cette option est définie sur **Activé**, Windows nécessite que tous les utilisateurs utilisent la détection d’usurpation pour les fonctions de reconnaissance faciale, si disponible.  

    -   **Utiliser Remote Passport** : si cette option a la valeur **Activé**, les utilisateurs peuvent utiliser un appareil Remote Passport comme appareil mobile pour l’authentification d’ordinateur du bureau. L’ordinateur de bureau doit être joint à Azure Active Directory, et l’appareil mobile doit être configuré avec un code confidentiel Windows Hello Entreprise.  

5.  Lorsque vous avez terminé, cliquez sur **OK**.  


## <a name="configure-windows-hello-for-business-on-domain-joined-windows-10-devices"></a>Configurer Windows Hello Entreprise sur les appareils Windows 10 joints à un domaine
Vous pouvez contrôler les paramètres Windows Hello Entreprise sur les appareils Windows 10 joints à un domaine de trois façons :

- Vous pouvez créer et déployer un profil Windows Hello Entreprise. Il s’agit de l’approche recommandée.
- Vous pouvez utiliser une stratégie de groupe.  
- Vous pouvez utiliser un script PowerShell.

Notez qu’en plus de cette configuration, vous devez déployer un profil de certificat, comme cela est décrit dans [Configurer un profil de certificat](#configure-a-certificate-profile).

### <a name="recommended-approach----configure-a-windows-hello-for-business-profile"></a>Approche recommandée – Configurer un profil Windows Hello Entreprise  

Dans la console d’administration, sous **Accès aux ressources de l’entreprise**, cliquez avec le bouton droit sur **Profils Windows Hello for business** et choisissez **Nouveau** pour démarrer l’Assistant de création de profil. Fournissez les paramètres demandés par l’Assistant, passez en revue et confirmez les paramètres de la dernière page, puis cliquez sur **Fermer**. Voici un exemple de ce à quoi vos paramètres peuvent ressembler :  

![Paramètres Windows Hello Entreprise](../media/Hello-for-Business-settings.png)

### <a name="configure-windows-hello-for-business-with-group-policy-in-active-directory"></a>Configurer Windows Hello Entreprise à l’aide d’une stratégie de groupe dans Active Directory  

Vous pouvez utiliser une stratégie de groupe Active Directory pour configurer vos appareils Windows 10 joints à un domaine afin de fournir les informations d’identification Hello Entreprise des utilisateurs quand ceux-ci se connectent à Windows :

1.  Sur un ordinateur Windows Server, ouvrez le Gestionnaire de serveur et accédez à **Outils** > **Gestion des stratégies de groupe**.    

2.  Dans la boîte de dialogue **Gestion des stratégies de groupe** , développez le domaine dans lequel vous souhaitez activer la jonction d’espace de travail automatique.    

3.  Cliquez avec le bouton droit sur **Objets de stratégie de groupe**, puis cliquez sur **Nouveau**.  

4.  Dans la boîte de dialogue **Nouvel objet GPO**, entrez un nom pour le nouvel objet de stratégie de groupe, par exemple **Activer Windows Hello Entreprise**, puis cliquez sur **OK**.  

5.  Dans le nœud **Objets de stratégie de groupe** , cliquez avec le bouton droit sur l’objet que vous avez créé, puis cliquez sur **Modifier**.  

6.  Dans la boîte de dialogue **Éditeur de gestion des stratégies de groupe**, accédez à **Configuration ordinateur** > **Stratégies** > **Modèles d’administration** > **Composants Windows** > **Windows Hello Entreprise**.  

7.  Cliquez avec le bouton droit sur **Activer Windows Hello Entreprise**, puis cliquez sur **Modifier**.   

8.  Sélectionnez **Activé**, cliquez sur **Appliquer**, puis cliquez sur **OK**.

Vous pouvez maintenant lier l’objet de stratégie de groupe que vous venez de créer à l’emplacement de votre choix. Exemple :    

   Une unité d’organisation (OU) spécifique dans Active Directory où se trouveront des ordinateurs Windows 10 joints au domaine    

   Un groupe de sécurité spécifique contenant des ordinateurs Windows 10 joints au domaine qui seront automatiquement inscrits auprès d’Azure AD    

#### <a name="configure-windows-hello-for-business-by-deploying-a-powershell-script-with-configuration-manager"></a>Configurer Windows Hello Entreprise en déployant un script PowerShell avec Configuration Manager    
Vous pouvez créer et déployer le script PowerShell suivant à l’aide de la gestion d’applications Configuration Manager.    

```    
powershell.exe -ExecutionPolicy Bypass -NoLogo -NoProfile -Command "& {New-ItemProperty "HKLM:\Software\Policies\Microsoft\PassportForWork" -Name "Enabled" -Value 1 -PropertyType "DWord" -Force}"  
```  

Pour plus d’informations sur la gestion d’applications Configuration Manager, consultez [Présentation de la gestion d’applications dans System Center Configuration Manager](/sccm/apps/understand/introduction-to-application-management).  

## <a name="configure-a-certificate-profile-to-enroll-the-windows-hello-for-business-enrollment-certificate-in-configuration-manager"></a>Configurer un profil de certificat pour inscrire le certificat d’inscription Windows Hello Entreprise dans Configuration Manager  
 Si vous souhaitez utiliser l’ouverture de session basée sur certificat Windows Hello Entreprise, ou Microsoft Hello, configurez ce qui suit :  

-   Un profil de certificat Configuration Manager.  

-   Dans le profil de certificat, sélectionnez un modèle qui recourt à l’utilisation de clé étendue pour l’ouverture de session avec carte à puce.  

 Pour plus d’informations, consultez [Profils de certificat](introduction-to-certificate-profiles.md).  

### <a name="see-also"></a>Voir aussi  
 [Protéger les données et l’infrastructure des sites avec System Center Configuration Manager](../../protect/understand/protect-data-and-site-infrastructure.md)

 [Gérer la vérification d’identité à l’aide de Windows Hello Entreprise](https://technet.microsoft.com/itpro/windows/keep-secure/manage-identity-verification-using-microsoft-passport).  



<!--HONumber=Dec16_HO3-->


