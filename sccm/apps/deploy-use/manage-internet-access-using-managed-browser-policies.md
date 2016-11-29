---
title: "Gérer l’accès à Internet à l’aide de stratégies Managed Browser | System Center Configuration Manager"
description: "Déployez Intune Managed Browser pour gérer et limiter l’accès à Internet."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 735c45b8-a545-4805-84e5-46204fabd1a6
caps.latest.revision: 6
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: e5efee7b94f5c61a610fd9f9fa278c992f9c64b8


---
# <a name="manage-internet-access-using-managed-browser-policies-with-system-center-configuration-manager"></a>Gérer l’accès à Internet à l’aide de stratégies Managed Browser avec System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Dans System Center Configuration Manager, vous pouvez déployer Intune Managed Browser, application de navigation web, puis l’associer à une stratégie Managed Browser. La stratégie Managed Browser configure une liste autorisée ou une liste bloquée qui restreint les sites web auxquels les utilisateurs de Managed Browser ont accès.  
  
 Comme il s'agit d'une application gérée, vous pouvez aussi lui appliquer des stratégies de gestion des applications mobiles, notamment pour contrôler l'utilisation des fonctions couper, copier et coller, pour empêcher les captures d'écran ou encore pour vous assurer que les liens vers du contenu sur lesquels les utilisateurs cliquent s'ouvrent uniquement dans d'autres applications gérées. Pour plus d’informations, consultez [Protection d’applications à l’aide de stratégies de gestion des applications mobiles](../../apps/deploy-use/protect-apps-using-mam-policies.md).  
  
> [!IMPORTANT]  
>  Si les utilisateurs installent eux-mêmes l'application Managed Browser, celle-ci ne sera pas gérée par les stratégies que vous spécifiez. Pour vérifier que le navigateur est géré par Configuration Manager, ils doivent désinstaller l’application avant de la déployer en tant qu’application gérée.  

 Vous pouvez créer des stratégies Managed Browser pour les types d'appareils suivants :  

-   appareils qui exécutent Android 4 et versions ultérieures ;  

-   appareils qui exécutent iOS 7 et versions ultérieures.  

> [!NOTE]  
>  Pour plus d’informations sur l’application Managed Browser Intune et pour la télécharger, consultez [iTunes](https://itunes.apple.com/us/app/microsoft-intune-managed-browser/id943264951?mt=8) pour iOS et [Google Play](https://play.google.com/store/apps/details?id=com.microsoft.intune.mam.managedbrowser&hl=en) pour Android.  
  
## <a name="create-a-managed-browser-policy"></a>Créer une stratégie Managed Browser  

1.  Dans la console Configuration Manager, cliquez sur **Bibliothèque de logiciels** > **Gestion des applications** > **Stratégies de gestion d’application**.  

3.  Sous l'onglet **Accueil** , dans le groupe **Créer** , cliquez sur **Créer une stratégie de gestion d'application**.  

4.  Dans la page **Général** , entrez le nom et la description de la stratégie, puis cliquez sur **Suivant**.  

5.  Dans la page **Type de stratégie** , sélectionnez la plateforme, sélectionnez **Managed Browser** pour le type de stratégie, puis cliquez sur **Suivant**.  

     Dans la page **Managed Browser** , sélectionnez l'une des options suivantes :  

    -   **Autoriser Managed Browser à ouvrir uniquement les URL ci-dessous (liste autorisée)** : spécifiez une liste d'URL pouvant être ouvertes par Managed Browser.  

    -   **Empêcher Managed Browser d'ouvrir les URL ci-dessous (liste bloquée)** : spécifiez une liste d'URL ne pouvant pas être ouvertes par Managed Browser.  

    > [!NOTE]  
    >  Vous ne pouvez pas inclure des URL autorisées et bloquées dans la même stratégie Managed Browser.  

     Pour plus d’informations sur les formats d’URL que vous pouvez spécifier, consultez **Format des URL autorisées et des URL bloquées** dans cette rubrique.  

    > [!NOTE]  
    >  La stratégie **Général** vous permet de modifier les fonctionnalités des applications que vous déployez pour les adapter aux stratégies de sécurité et de conformité de votre entreprise. Par exemple, vous pouvez limiter les opérations Couper, Copier et Coller dans une application restreinte. Pour plus d’informations sur le type de stratégie Général, consultez [Protéger des applications à l’aide de stratégies de gestion des applications mobiles](../../apps/deploy-use/protect-apps-using-mam-policies.md).  

6.  Effectuez toutes les étapes de l'Assistant.  

 La nouvelle stratégie s'affiche dans le nœud **Stratégies de gestion d'application** de l'espace de travail **Bibliothèque de logiciels** .  

## <a name="create-a-software-deployment-for-the-managed-browser-app"></a>Créer un déploiement de logiciel pour l'application Managed Browser  
 Après avoir créé la stratégie Managed Browser, vous pouvez créer un type de déploiement de logiciel pour l'application Managed Browser. Vous devez associer une stratégie Général et une stratégie Managed Browser à l'application Managed Browser.  
  
 Pour plus d’informations, consultez [Créer des applications](../../apps/deploy-use/create-applications.md).  
  
## <a name="security-and-privacy-for-the-managed-browser"></a>Sécurité et confidentialité de Managed Browser  

-   Sur les appareils iOS, les utilisateurs ne peuvent pas ouvrir les sites web possédant un certificat qui a expiré ou qui n'est pas approuvé.  

-   Les paramètres du navigateur intégré définis par les utilisateurs sur leur appareil ne sont pas utilisés par Managed Browser. Cela est dû au fait que Managed Browser n'a pas accès à ces paramètres.  

-   Si vous configurez l'option **Demander un code confidentiel simple pour l'accès** ou **Exiger des informations d'identification d'entreprise pour l'accès** dans une stratégie de gestion des applications mobiles associée à Managed Browser et qu'un utilisateur clique sur le lien d'aide dans la page d'authentification, l'utilisateur peut visiter n'importe quel site Internet, même si celui-ci a été ajoutée à une liste bloquée dans la stratégie Managed Browser.  

-   Managed Browser peut uniquement bloquer l'accès aux sites qui font l'objet d'un accès direct. Il ne peut pas bloquer l'accès quand des services intermédiaires (tels qu'un service de traduction) sont utilisés pour accéder au site.  

## <a name="reference-information"></a>Informations de référence  
  
###  <a name="url-format-for-allowed-and-blocked-urls"></a>Format des URL autorisées et des URL bloquées  

Utilisez les informations suivantes pour en savoir plus sur les formats et les caractères génériques que vous pouvez utiliser pour spécifier des URL dans les listes autorisées et les listes bloquées.  

-   Vous pouvez utiliser le caractère générique «**\***» selon les règles de la liste de modèles autorisés ci-dessous.  

-   Veillez à faire précéder toutes les URL du préfixe **http** ou **https** quand vous les entrez dans la liste.  

-   Vous pouvez spécifier des numéros de port dans l'adresse. Si vous ne spécifiez pas un numéro de port, les valeurs suivantes sont utilisées :  

    -   Port 80 pour http  

    -   Port 443 pour https  

     Vous ne pouvez pas utiliser de caractères génériques pour le numéro de port. Par exemple, **http://www.contoso.com:\*** et **http://www.contoso.com: /\***  

-   Utilisez le tableau suivant pour en savoir plus sur les modèles autorisés que vous pouvez utiliser pour spécifier des URL :  

    |Adresse URL|Correspond à|Ne correspond pas à|  
    |---------|-------------|--------------------|  
    |http://www.contoso.com<br /><br /> Correspond à une page unique|www.contoso.com|host.contoso.com<br /><br /> www.contoso.com/images<br /><br /> contoso.com/|  
    |http://contoso.com<br /><br /> Correspond à une page unique|contoso.com/|host.contoso.com<br /><br /> www.contoso.com/images<br /><br /> www.contoso.com|  
    |http://www.contoso.com/*<br /><br /> Correspond à toutes les URL commençant par www.contoso.com|www.contoso.com<br /><br /> www.contoso.com/images<br /><br /> www.contoso.com/videos/tvshows|host.contoso.com<br /><br /> host.contoso.com/images|  
    |http://*.contoso.com/\*<br /><br /> Correspond à tous les sous-domaines sous contoso.com|developer.contoso.com/resources<br /><br /> news.contoso.com/images<br /><br /> news.contoso.com/videos|contoso.host.com|  
    |http://www.contoso.com/images<br /><br /> Correspond à un dossier unique|www.contoso.com/images|www.contoso.com/images/dogs|  
    |http://www.contoso.com:80<br /><br /> Correspond à une page unique avec un numéro de port|http://www.contoso.com:80||  
    |https://www.contoso.com<br /><br /> Correspond à une page unique sécurisée|https://www.contoso.com|http://www.contoso.com|  
    |http://www.contoso.com/images/*<br /><br /> Correspond à un dossier unique et à tous ses sous-dossiers|www.contoso.com/images/dogs<br /><br /> www.contoso.com/images/cats|www.contoso.com/videos|  

-   Voici quelques exemples de certaines entrées que vous ne pouvez pas spécifier :  

    -   *.com  

    -   *.contoso/\*  

    -   www.contoso.com/*images  

    -   www.contoso.com/*images\*pigs  

    -   www.contoso.com/page*  

    -   Adresses IP  

    -   https://*  

    -   http://*  

    -   http://www.contoso.com:*  

    -   http://www.contoso.com: /*  

> [!NOTE]  
>  *.microsoft.com est toujours autorisé.  
  
### <a name="how-conflicts-between-the-allow-and-block-list-are-resolved"></a>Résolution des conflits entre la liste autorisée et la liste bloquée  
 Si plusieurs stratégies Managed Browser sont déployées sur un appareil et qu'un conflit se produit entre les paramètres, le mode (autorisé ou bloqué) et les listes d'URL sont évalués pour déterminer les conflits. En cas de conflit, le comportement suivant s'applique :  

-   Si les modes dans chaque stratégie sont les mêmes, mais que les listes d'URL sont différentes, les URL ne sont pas appliquées sur l'appareil.  

-   Si les modes dans chaque stratégie sont différents, mais que les listes d'URL sont les mêmes, les URL ne sont pas appliquées sur l'appareil.  

-   Si un appareil reçoit des stratégies Managed Browser pour la première fois et qu'un conflit se produit entre deux stratégies, les URL ne sont pas appliquées sur l'appareil. Utilisez le nœud **Conflits de stratégies** de l'espace de travail **Stratégie** pour afficher les conflits.  

-   Si un appareil a déjà reçu une stratégie Managed Browser et qu'une deuxième stratégie est déployée avec des paramètres en conflit, les paramètres d'origine restent sur l'appareil. Utilisez le nœud **Conflits de stratégies** de l'espace de travail **Stratégie** pour afficher les conflits.  



<!--HONumber=Nov16_HO1-->


