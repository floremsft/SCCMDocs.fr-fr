---
title: "Déploiement de certificats PKI | System Center Configuration Manager"
description: "Suivez un exemple de procédure pas à pas pour découvrir le processus de création et de déploiement des certificats PKI utilisé par System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 3417ff88-7177-4a0d-8967-ab21fe7eba17
caps.latest.revision: 11
author: Nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 49dfa303453b26a64c1495a1259674e0d8a6bde2


---
# <a name="step-by-step-example-deployment-of-the-pki-certificates-for-system-center-configuration-manager-windows-server-2008-certification-authority"></a>Exemple de déploiement pas à pas des certificats PKI pour System Center Configuration Manager : autorité de certification Windows Server 2008

*S’applique à : System Center Configuration Manager (Current Branch)*

Cet exemple de déploiement pas à pas utilise une autorité de certification Windows Server 2008. Il contient des procédures décrivant le processus de création et de déploiement des certificats pour infrastructure à clé publique (PKI) utilisé par System Center Configuration Manager. Ces procédures utilisent une autorité de certification d'entreprise (CA) et des modèles de certificats. Les étapes conviennent uniquement à un réseau de test utilisé à des fins de démonstration du concept.  

 Étant donné qu'il n'existe aucune méthode unique de déploiement des certificats requis, vous devez consulter la documentation de votre déploiement d'infrastructure à clés publiques (PKI) pour prendre connaissance des procédures et des meilleures pratiques liées au déploiement des certificats requis pour un environnement de production. Pour plus d’informations sur la configuration requise pour les certificats, consultez [Configuration requise des certificats PKI pour System Center Configuration Manager](../../../core/plan-design/network/pki-certificate-requirements.md).  

> [!TIP]  
>  Les instructions de cette rubrique peuvent facilement être adaptées pour les systèmes d'exploitation autres que ceux décrits dans la section Configuration réseau test. Toutefois, si vous exécutez l'autorité de certification émettrice sur Windows Server 2012, vous n'êtes pas invité à indiquer la version du modèle de certificat. Spécifiez-la plutôt sous l'onglet **Compatibilité** des propriétés du modèle, comme suit :  
>   
>  -   **Autorité de certification**: **Windows Server 2003**  
> -   **Destinataire du certificat**: **Windows XP / Server 2003**  

## <a name="in-this-section"></a>Dans cette section  
 Les sections suivantes contiennent des exemples de procédures pas à pas pour créer et déployer les certificats suivants à utiliser avec System Center Configuration Manager :  

 [Configuration requise du réseau de test](#BKMK_testnetworkenvironment)  

 [Présentation des certificats](#BKMK_overview2008)  

 [Déploiement du certificat de serveur Web pour les systèmes de site qui exécutent IIS](#BKMK_webserver2008_cm2012)  

 [Déploiement du certificat de service pour les points de distribution cloud](#BKMK_clouddp2008_cm2012)  

 [Déploiement du certificat client pour les ordinateurs Windows](#BKMK_client2008_cm2012)  

 [Déploiement du certificat client pour les points de distribution](#BKMK_clientdistributionpoint2008_cm2012)  

 [Déploiement du certificat d'inscription pour les appareils mobiles](#BKMK_mobiledevices2008_cm2012)  

 [Déploiement des certificats pour AMT](#BKMK_AMT2008_cm2012)  

 [Déploiement du certificat client pour les ordinateurs Mac](#BKMK_MacClient_SP1)  

##  <a name="a-namebkmktestnetworkenvironmenta-test-network-requirements"></a><a name="BKMK_testnetworkenvironment"></a> Configuration requise du réseau de test  
 Dans ces instructions étape par étape, les impératifs de configuration sont les suivants :  

-   Le réseau de test exécute les services de domaine Active Directory avec Windows Server 2008, et il est installé en tant que domaine unique au sein d'une même forêt.  

-   Vous disposez d'un serveur membre exécutant Windows Server 2008 Enterprise Edition sur lequel est installé le rôle de services de certificats Active Directory, et il est configuré en tant qu'autorité de certification racine d'entreprise.  

-   Un ordinateur équipé de Windows Server 2008 (Standard Edition ou Enterprise Edition, R2 ou version ultérieure) doit être désigné comme serveur membre, et les services Internet (IIS) doivent être installés sur cet ordinateur. Cet ordinateur est le serveur de système de site System Center Configuration Manager que vous configurez avec un nom de domaine complet Intranet (pour la prise en charge des connexions client sur l’Intranet) et un nom de domaine complet Internet si vous devez prendre en charge des appareils mobiles inscrits auprès de System Center Configuration Manager et de clients sur Internet.  

-   Vous disposez d'un client Windows Vista équipé du dernier Service Pack, et cet ordinateur configuré avec un nom d'ordinateur incluant des caractères ASCII est lié au domaine. Cet ordinateur est un ordinateur client System Center Configuration Manager.  

-   Vous pouvez ouvrir une session sous un compte d'administrateur de domaine racine ou d'entreprise et utiliser ce compte pour effectuer toutes les procédures présentées dans cet exemple de déploiement.  

##  <a name="a-namebkmkoverview2008a-overview-of-the-certificates"></a><a name="BKMK_overview2008"></a> Présentation des certificats  
 Le tableau suivant présente les types de certificats PKI pouvant être nécessaires pour System Center Configuration Manager et décrit leur utilisation.  

|Certificat requis|Description du certificat|  
|-----------------------------|-----------------------------|  
|Certificat de serveur Web pour les systèmes de site qui exécutent IIS|Ce certificat permet de chiffrer les données et d'authentifier le serveur auprès des clients. Il doit être installé indépendamment de System Center Configuration Manager sur des serveurs de systèmes de site qui exécutent IIS et qui sont configurés dans System Center Configuration Manager pour utiliser HTTPS.<br /><br /> Pour plus d'informations sur la procédure de configuration et installation de ce certificat, voir [Déploiement du certificat de serveur Web pour les systèmes de site qui exécutent IIS](#BKMK_webserver2008_cm2012) dans cette rubrique.|  
|Certificat de service pour la connexion des clients aux points de distribution cloud|Pour plus d’informations sur la procédure de configuration et d’installation de ce certificat, consultez [Déploiement du certificat de service pour les points de distribution cloud](#BKMK_clouddp2008_cm2012) dans cette rubrique.<br /><br /> **Important :** Ce certificat est utilisé conjointement avec le certificat de gestion Microsoft Azure. Pour plus d'informations sur le certificat de gestion, voir [Création d'un certificat de gestion](http://go.microsoft.com/fwlink/p/?LinkId=220281) et [Ajouter un certificat de gestion à un abonnement Windows Azure](http://go.microsoft.com/fwlink/?LinkId=241722) dans la section sur la plate-forme Windows Azure de la bibliothèque MSDN.|  
|Certificat client pour les ordinateurs Windows|Ce certificat est utilisé pour authentifier les ordinateurs clients System Center Configuration Manager auprès des systèmes de site qui sont configurés pour utiliser HTTPS. Sur les points de gestion et les points de migration d'état, il permet de surveiller leur état de fonctionnement lorsqu'ils sont configurés pour utiliser HTTPS. Il doit être installé indépendamment de System Center Configuration Manager sur les ordinateurs.<br /><br /> Pour plus d'informations sur les étapes permettant de configurer et d'installer ce certificat, consultez [Déploiement du certificat client pour les ordinateurs Windows](#BKMK_client2008_cm2012) dans cette rubrique.|  
|Certificat client pour les points de distribution|Ce certificat a deux objectifs :<br /><br /> Ce certificat est utilisé pour authentifier le point de distribution auprès d'un point de gestion HTTPS avant que le point de distribution n'envoie des messages d'état.<br /><br /> Lorsque l'option du point de distribution **Activer la prise en charge PXE pour les clients** est sélectionnée, le certificat est envoyé aux ordinateurs qui effectuent un démarrage PXE afin qu'ils puissent se connecter à un point de gestion HTTPS pendant le déploiement du système d'exploitation.<br /><br /> Pour plus d'informations sur la procédure de configuration et installation de ce certificat, voir [Déploiement du certificat client pour les points de distribution](#BKMK_clientdistributionpoint2008_cm2012) dans cette rubrique.|  
|Certificat d'inscription pour les appareils mobiles|Ce certificat est utilisé pour authentifier les clients d’appareils mobiles System Center Configuration Manager auprès des systèmes de site qui sont configurés pour utiliser HTTPS. Il doit être installé dans le cadre de l’inscription d’appareil mobile dans System Center Configuration Manager. Ensuite, vous sélectionnez le modèle de certificat configuré comme paramètre de client d’appareil mobile.<br /><br /> Pour plus d'informations sur les étapes permettant de configurer ce certificat, consultez [Deploying the Enrollment Certificate for Mobile Devices](#BKMK_mobiledevices2008_cm2012) dans cette rubrique.|  
|Certificats pour Intel AMT|Trois certificats relatifs à la gestion hors bande sont disponibles pour les ordinateurs Intel AMT : un certificat de configuration AMT ; un certificat de serveur Web AMT ; et en option, un certificat d'authentification client pour les réseaux filaires ou sans fil 802.1X.<br /><br /> Le certificat de configuration AMT doit être installé indépendamment de System Center Configuration Manager sur l’ordinateur de point de service hors bande. Ensuite, vous sélectionnez le certificat installé dans les propriétés du point de service hors bande. Le certificat de serveur Web AMT, ainsi que le certificat d'authentification du client sont installés pendant la configuration et la gestion d'AMT. Ensuite, vous sélectionnez les modèles de certificats configurés dans les propriétés du composant de gestion hors bande.<br /><br /> Pour plus d'informations sur la procédure de configuration de ces certificats, voir [Déploiement des certificats pour AMT](#BKMK_AMT2008_cm2012) dans cette rubrique.|  
|Certificat client pour les ordinateurs Mac|Vous pouvez obtenir et installer ce certificat à partir d’un ordinateur Mac quand vous utilisez l’inscription System Center Configuration Manager. Ensuite, vous sélectionnez le modèle de certificat configuré comme paramètre de client d’appareil mobile.<br /><br /> Pour plus d'informations sur les étapes permettant de configurer ce certificat, consultez [Deploying the Client Certificate for Mac Computers](#BKMK_MacClient_SP1) dans cette rubrique.|  

##  <a name="a-namebkmkwebserver2008cm2012a-deploying-the-web-server-certificate-for-site-systems-that-run-iis"></a><a name="BKMK_webserver2008_cm2012"></a> Déploiement du certificat de serveur Web pour les systèmes de site qui exécutent IIS  
 Les procédures de ce déploiement de certificat sont les suivantes :  

-   Création et émission du modèle de certificat de serveur Web sur l'autorité de certification  

-   Demande du certificat de serveur Web  

-   Configuration des services IIS pour l'utilisation du certificat de serveur Web  

###  <a name="a-namebkmkwebserver22008a-creating-and-issuing-the-web-server-certificate-template-on-the-certification-authority"></a><a name="BKMK_webserver22008"></a> Création et émission du modèle de certificat de serveur Web sur l'autorité de certification  
 Cette procédure crée un modèle de certificat pour les systèmes de site System Center Configuration Manager et l’ajoute à l’autorité de certification.  

##### <a name="to-create-and-issue-the-web-server-certificate-template-on-the-certification-authority"></a>Pour créer et émettre le modèle de certificat de serveur Web sur l'autorité de certification  

1.  Créez un groupe de sécurité nommé **Serveurs ConfigMgr IIS** qui contient les serveurs membres où installer les systèmes de site System Center Configuration Manager qui vont exécuter IIS.  

2.  Sur le serveur membre sur lequel les services de certificats sont installés, dans la console Autorité de certification, cliquez avec le bouton droit sur **Modèles de certificats** , puis cliquez sur **Gérer** pour charger la console **Modèles de certificats** .  

3.  Dans le volet de résultats, cliquez avec le bouton droit sur l'entrée qui affiche **Serveur Web** dans la colonne **Nom complet du modèle**, puis cliquez sur **Dupliquer le modèle**.  

4.  Dans la boîte de dialogue **Dupliquer le modèle** , assurez-vous que l'option **Windows Server 2003, Enterprise Edition** est sélectionnée, puis cliquez sur **OK**.  

    > [!IMPORTANT]  
    >  Ne sélectionnez pas **Windows Server 2008, Enterprise Edition**.  

5.  Dans la boîte de dialogue **Propriétés du nouveau modèle** , sous l'onglet **Général** , entrez un nom de modèle pour générer les certificats Web à utiliser dans les systèmes de site Configuration Manager (par exemple **Certificat de serveur Web ConfigMgr**).  

6.  Sous l'onglet **Nom d'objet** , assurez-vous de sélectionner **Fourni dans la demande** .  

7.  Sous l'onglet **Sécurité** , supprimez l'autorisation **Inscription** des groupes de sécurité **Administrateurs du domaine** et **Administrateurs de l'entreprise**.  

8.  Cliquez sur **Ajouter**, tapez **Serveurs ConfigMgr IIS** dans la zone de texte, puis cliquez sur **OK**.  

9. Sélectionnez l'autorisation **Inscription** pour ce groupe et ne désactivez pas l'autorisation **Lecture** .  

10. Cliquez sur **OK**, puis fermez la console **Modèles de certificats**.  

11. Dans la console Autorité de certification, cliquez avec le bouton droit sur **Modèles de certificats**, cliquez sur **Nouveau**, puis cliquez sur **Modèle de certificat à délivrer**.  

12. Dans la boîte de dialogue **Activer les modèles de certificat** , sélectionnez le nouveau modèle que vous venez de créer, **Certificat de serveur Web ConfigMgr**, puis cliquez sur **OK**.  

13. Si vous n'avez pas besoin de créer ou d'émettre d'autres certificats, fermez **Autorité de Certification**.  

###  <a name="a-namebkmkwebserver32008a-requesting-the-web-server-certificate"></a><a name="BKMK_webserver32008"></a> Demande du certificat de serveur Web  
 Cette procédure permet de spécifier les valeurs FQDN Intranet et Internet qui seront configurées dans les propriétés de serveur de système de site, puis installe le certificat de serveur Web sur le serveur membre qui exécute IIS.  

##### <a name="to-request-the-web-server-certificate"></a>Pour demander le certificat de serveur Web  

1.  Redémarrez le serveur membre qui exécute IIS pour vérifier que l'ordinateur peut accéder au modèle de certificat créé via les autorisations **Lecture** et **Inscription** configurées.  

2.  Cliquez sur **Démarrer**, cliquez sur **Exécuter**, puis tapez **mmc.exe.** Dans la console vide, cliquez sur **Fichier**, puis cliquez sur **Ajouter/Supprimer un composant logiciel enfichable**.  

3.  Dans la boîte de dialogue **Ajouter ou supprimer des composants logiciels enfichables** , sélectionnez **Certificats** dans la liste **Composants logiciels enfichables disponibles**, puis cliquez sur **Ajouter**.  

4.  Dans la boîte de dialogue **Composant logiciel enfichable des certificats** , cliquez sur **Compte d'ordinateur**, puis sur **Suivant**.  

5.  Dans la boîte de dialogue **Sélectionner un ordinateur** , vérifiez que **L'ordinateur local (l'ordinateur sur lequel cette console s'exécute)** est sélectionné, puis cliquez sur **Terminer**.  

6.  Dans la boîte de dialogue **Ajouter ou supprimer des composants logiciels enfichables** , cliquez sur **OK**.  

7.  Dans la console, développez **Certificats (ordinateur local)**, puis cliquez sur **Personnel**.  

8.  Cliquez avec le bouton droit sur **Certificats**, cliquez sur **Toutes les tâches**, puis cliquez sur **Demander un nouveau certificat**.  

9. Dans la page **Avant de commencer** , cliquez sur **Suivant**.  

10. Si vous voyez la page **Sélectionner la stratégie d'inscription de certificat** , cliquez sur **Suivant**.  

11. Dans la page **Demander des certificats**, identifiez le **certificat de serveur web ConfigMgr** dans la liste des certificats affichés, puis cliquez sur **L’inscription pour obtenir ce certificat nécessite des informations supplémentaires. Cliquez ici pour configurer les paramètres**.  

12. Dans la boîte de dialogue **Propriétés du certificat** , dans l'onglet **Objet** , n'apportez pas de modifications à **Nom d'objet**. Cela signifie que la zone **Valeur** de la section **Nom d'objet** reste vierge. Au lieu de cela, dans la section **Autre nom** , cliquez sur la liste déroulante **Type** , puis sélectionnez **DNS**.  

13. Dans la zone **Valeur**, spécifiez les valeurs de nom de domaine complet que vous allez indiquer dans les propriétés de système de site System Center Configuration Manager, puis cliquez sur **OK** pour fermer la boîte de dialogue **Propriétés du certificat**.  

     Exemples :  

    -   Si le système de site accepte uniquement les connexions client à partir de l'Intranet, et le nom de domaine complet Intranet du serveur de système de site est **server1.internal.contoso.com**, Tapez **server1.internal.contoso.com**, puis cliquez sur **Ajouter**.  

    -   Si le système de site accepte uniquement les connexions client à partir de l'Intranet et d'Internet, et le nom de domaine complet Intranet du serveur de système de site est **server1.internal.contoso.com** , et le nom de domaine complet Internet du serveur de système de site est **server.contoso.com**:  

        1.  Tapez **server1.internal.contoso.com**, puis cliquez sur **Ajouter**.  

        2.  Tapez **server.contoso.com**, puis cliquez sur **Ajouter**.  

        > [!NOTE]  
        >  L’ordre dans lequel vous spécifiez les noms de domaine complets pour System Center Configuration Manager n’a pas d’importance. Cependant, vérifiez que tous les appareils qui utiliseront le certificat, tels que les appareils mobiles et les serveurs web proxy peuvent utiliser un certificat SAN (Autre nom de l'objet) et plusieurs valeurs dans SAN. Si la prise en charge par les appareils des valeurs SAN dans les certificats est limitée, envisagez de modifier l'ordre des noms de domaine complets ou utilisez la valeur Objet à la place.  

14. Sur la page **Demander des certificats** , sélectionnez **Certificat de serveur Web ConfigMgr** dans la liste des certificats affichés, puis cliquez sur **Inscrire**.  

15. Sur la page **Résultats de l'installation** des certificats, attendez que le certificat soit installé, puis cliquez sur **Terminer**.  

16. Fermez la fenêtre **Certificats (ordinateur local)**.  

###  <a name="a-namebkmkwebserver42008a-configuring-iis-to-use-the-web-server-certificate"></a><a name="BKMK_webserver42008"></a> Configuration des services IIS pour l'utilisation du certificat de serveur Web  
 Cette procédure lie le certificat installé au **Site Web par défaut**IIS.  

##### <a name="to-configure-iis-to-use-the-web-server-certificate"></a>Pour configurer IIS en vue de l'utilisation du certificat de serveur Web  

1.  Sur le serveur membre avec IIS installé, cliquez sur **Démarrer**, cliquez sur **Programmes**, cliquez sur **Outils d'administration**, puis cliquez sur **Gestionnaire des services Internet (IIS)**.  

2.  Développez **Sites**, cliquez avec le bouton droit sur **Site Web par défaut**, puis sélectionnez **Modifier les liaisons**.  

3.  Cliquez sur l'entrée **https** , puis cliquez sur **Modifier**.  

4.  Dans la boîte de dialogue **Modifier la liaison de site** , sélectionnez le certificat que vous avez demandé à l'aide du modèle Certificats de serveur Web ConfigMgr, puis cliquez sur **OK**.  

    > [!NOTE]  
    >  Si vous ne savez pas quel est le certificat correct, sélectionnez-en un, puis cliquez sur **Afficher**. Cela vous permet de comparer les détails du certificat sélectionné avec les certificats qui sont affichés avec le composant logiciel enfichable Certificats. Par exemple, le composant logiciel enfichable Certificats affiche le modèle de certificat qui a été utilisé pour demander le certificat. Vous pouvez ensuite comparer l'empreinte numérique du certificat qui a été demandé à l'aide du modèle Certificats de serveur Web ConfigMgr à l'empreinte numérique du certificat actuellement sélectionné dans la boîte de dialogue **Modifier la liaison de site** .  

5.  Cliquez sur **OK** dans la boîte de dialogue **Modifier la liaison de site** , puis cliquez sur **Fermer**.  

6.  Fermez le **Gestionnaire des services Internet (IIS)**.  

 Le serveur membre contient maintenant un certificat de serveur web System Center Configuration Manager.  

> [!IMPORTANT]  
>  Quand vous installez le serveur de système de site System Center Configuration Manager sur cet ordinateur, assurez-vous de spécifier le même nom de domaine complet dans les propriétés de système de site que vous avez spécifié lors de la demande du certificat.  

##  <a name="a-namebkmkclouddp2008cm2012a-deploying-the-service-certificate-for-cloud-based-distribution-points"></a><a name="BKMK_clouddp2008_cm2012"></a> Déploiement du certificat de service pour les points de distribution cloud  

> [!NOTE]  
>  Le certificat de service pour les points de distribution cloud s’applique à System Center Configuration Manager SP1 et versions ultérieures.  

 Les procédures de ce déploiement de certificat sont les suivantes :  

-   [Création et émission d'un modèle de certificat de serveur Web personnalisé sur l'autorité de certification](#BKMK_clouddpcreating2008)  

-   [Demande du certificat de serveur Web personnalisé](#BKMK_clouddprequesting2008)  

-   [Exportation du certificat de serveur Web personnalisé pour les points de distribution cloud](#BKMK_clouddpexporting2008)  

###  <a name="a-namebkmkclouddpcreating2008a-creating-and-issuing-a-custom-web-server-certificate-template-on-the-certification-authority"></a><a name="BKMK_clouddpcreating2008"></a> Création et émission d'un modèle de certificat de serveur Web personnalisé sur l'autorité de certification  
 Cette procédure permet de créer un modèle de certificat personnalisé basé sur le modèle de certificat de serveur Web. Le certificat est destiné aux points de distribution cloud System Center Configuration Manager, et la clé privée doit être exportable. Vous devez ajouter le modèle de certificat à l'autorité de certification après sa création.  

> [!NOTE]  
>  Cette procédure utilise un modèle de certificat différent du modèle de certificat de serveur Web créé pour les systèmes de site qui exécutent IIS. En effet, les deux certificats requièrent des fonctions d'authentification du client, mais le certificat pour les points de distribution cloud requiert une valeur définie personnalisée dans le champ Nom d'objet, et la clé privée requiert l'exportation. Comme meilleure pratique de sécurité, ne configurez pas les modèles de certificats autorisant l'exportation la clé privée, sauf si cette configuration est requise. Le point de distribution cloud requiert cette configuration, car vous devez importer le certificat en tant que fichier, au lieu de le sélectionner dans le magasin de certificats.  
>   
>  En créant un nouveau modèle de certificat pour ce certificat, vous pouvez limiter les ordinateurs qui demandent un certificat autorisant l'exportation de la clé privée. Sur un réseau de production, vous pouvez également considérer d'apporter les modifications suivantes à ce certificat :  
>   
>  -   Demander l'approbation d'installer le certificat, pour plus de sécurité.  
> -   Augmenter la période de validité du certificat. Étant donné que vous devez exporter, puis importer le certificat chaque fois avant son expiration, l'augmentation de la période de validité permet de réduire la fréquence de cette procédure. Cependant, l'augmentation de la période de validité diminue la sécurité du certificat, car une personne malveillante a plus de temps pour déchiffrer la clé privée et voler le certificat.  
> -   Utilisez une valeur personnalisée dans le champ Autre nom de l'objet pour aider à identifier ce certificat parmi les certificats de serveur Web standard que vous utilisez avec IIS.  

##### <a name="to-create-and-issue-the-custom-web-server-certificate-template-on-the-certification-authority"></a>Pour créer et émettre le modèle de certificat de serveur Web personnalisé sur l'autorité de certification  

1.  Créez un groupe de sécurité nommé **Serveurs de site ConfigMgr** qui contient les serveurs membres où installer les serveurs de site principal System Center Configuration Manager qui vont gérer les points de distribution cloud.  

2.  Sur le serveur membre exécutant la console Autorité de certification, cliquez avec le bouton droit sur **Modèles de certificats**, puis cliquez sur **Gérer** pour charger la console de gestion des modèles de certificats.  

3.  Dans le volet de résultats, cliquez avec le bouton droit sur l'entrée qui affiche **Serveur Web** dans la colonne **Nom complet du modèle**, puis cliquez sur **Dupliquer le modèle**.  

4.  Dans la boîte de dialogue **Dupliquer le modèle** , assurez-vous que l'option **Windows Server 2003, Enterprise Edition** est sélectionnée, puis cliquez sur **OK**.  

    > [!IMPORTANT]  
    >  Ne sélectionnez pas **Windows Server 2008, Enterprise Edition**.  

5.  Dans la boîte de dialogue **Propriétés du nouveau modèle** , sous l'onglet **Général** , entrez un nom de modèle pour générer le certificat de serveur Web des points de distribution cloud, tel que **Certificat de point de distribution cloud ConfigMgr**.  

6.  Cliquez sur l'onglet **Traitement de la demande** et sélectionnez **Autoriser l'exportation de la clé privée**.  

7.  Cliquez sur l'onglet **Sécurité** et supprimez l'autorisation **Inscription** du groupe de sécurité **Administrateurs d'entreprise** .  

8.  Cliquez sur **Ajouter**, entrez **Serveurs de site ConfigMgr** dans la zone de texte, puis cliquez sur **OK**.  

9. Sélectionnez l'autorisation **Inscription** pour ce groupe et ne désactivez pas l'autorisation **Lecture** .  

10. Cliquez sur **OK** et fermez la **console Modèles de certificats**.  

11. Dans la console Autorité de certification, cliquez avec le bouton droit sur **Modèles de certificats**, cliquez sur **Nouveau**, puis cliquez sur **Modèle de certificat à délivrer**.  

12. Dans la boîte de dialogue **Activer les modèles de certificat** , sélectionnez le modèle que vous venez de créer ( **Certificat de point de distribution cloud ConfigMgr**), puis cliquez sur **OK**.  

13. Si vous n'avez pas besoin de créer ou d'émettre d'autres certificats, fermez **Autorité de certification**.  

###  <a name="a-namebkmkclouddprequesting2008a-requesting-the-custom-web-server-certificate"></a><a name="BKMK_clouddprequesting2008"></a> Demande du certificat de serveur Web personnalisé  
 Cette procédure permet de demander, puis d'installer le certificat de serveur Web personnalisé sur le serveur membre qui exécutera le serveur de site.  

##### <a name="to-request-the-custom-web-server-certificate"></a>Pour demander le certificat de serveur Web personnalisé  

1.  Redémarrez le serveur membre après avoir créé et configuré le groupe de sécurité **Serveurs de site ConfigMgr** pour vérifier que l'ordinateur peut accéder au modèle de certificat créé via les autorisations **Lecture** et **Inscription** configurées.  

2.  Cliquez sur **Démarrer**, cliquez sur **Exécuter**, puis tapez **mmc.exe.** Dans la console vide, cliquez sur **Fichier**, puis cliquez sur **Ajouter/Supprimer un composant logiciel enfichable**.  

3.  Dans la boîte de dialogue **Ajouter ou supprimer des composants logiciels enfichables** , sélectionnez **Certificats** dans la liste **Composants logiciels enfichables disponibles**, puis cliquez sur **Ajouter**.  

4.  Dans la boîte de dialogue **Composant logiciel enfichable des certificats** , cliquez sur **Compte d'ordinateur**, puis sur **Suivant**.  

5.  Dans la boîte de dialogue **Sélectionner un ordinateur** , vérifiez que **L'ordinateur local (l'ordinateur sur lequel cette console s'exécute)** est sélectionné, puis cliquez sur **Terminer**.  

6.  Dans la boîte de dialogue **Ajouter ou supprimer des composants logiciels enfichables** , cliquez sur **OK**.  

7.  Dans la console, développez **Certificats (ordinateur local)**, puis cliquez sur **Personnel**.  

8.  Cliquez avec le bouton droit sur **Certificats**, cliquez sur **Toutes les tâches**, puis cliquez sur **Demander un nouveau certificat**.  

9. Dans la page **Avant de commencer** , cliquez sur **Suivant**.  

10. Si vous voyez la page **Sélectionner la stratégie d'inscription de certificat** , cliquez sur **Suivant**.  

11. Dans la page **Demander des certificats**, identifiez le **certificat de point de distribution cloud ConfigMgr** dans la liste des certificats affichés, puis cliquez sur **L’inscription pour obtenir ce certificat nécessite des informations supplémentaires. Cliquez ici pour configurer les paramètres**.  

12. Dans la boîte de dialogue **Propriétés du certificat** , sous l'onglet **Objet** , sélectionnez **Nom commun**dans le champ **Nom d'objet** comme **Type**.  

13. Dans le champ **Valeur** , spécifiez un nom de service et votre nom de domaine à l'aide d'un format de nom de domaine complet. Par exemple : **clouddp1.contoso.com**.  

    > [!NOTE]  
    >  Le nom de service que vous spécifiez n'a pas d'importance, à condition qu'il soit unique dans votre espace de noms. Utilisez le système de noms de domaine pour créer un alias (enregistrement CNAME) pour mapper le nom de ce service à un identificateur (GUID) généré automatiquement et une adresse IP à partir de Windows Azure.  

14. Cliquez sur **Ajouter**, puis sur **OK** pour fermer la boîte de dialogue **Propriétés du certificat** .  

15. Sur la page **Demander des certificats** , sélectionnez **Certificat de point de distribution cloud ConfigMgr** dans la liste des certificats affichés, puis cliquez sur **Inscrire**.  

16. Sur la page **Résultats de l'installation** des certificats, attendez que le certificat soit installé, puis cliquez sur **Terminer**.  

17. Fermez la fenêtre **Certificats (ordinateur local)**.  

###  <a name="a-namebkmkclouddpexporting2008a-exporting-the-custom-web-server-certificate-for-cloud-based-distribution-points"></a><a name="BKMK_clouddpexporting2008"></a> Exportation du certificat de serveur Web personnalisé pour les points de distribution cloud  
 Cette procédure permet d'exporter le certificat de serveur Web personnalisé dans un fichier, afin qu'il puisse être importé lorsque vous créez le point de distribution cloud.  

##### <a name="to-export-the-custom-web-server-certificate-for-cloud-based-distribution-points"></a>Pour exporter le certificat de serveur Web personnalisé pour les points de distribution cloud  

1.  Dans la console **Certificats (ordinateur local)** , cliquez avec le bouton droit sur le certificat que vous venez d'installer, sélectionnez **Toutes les tâches**, puis cliquez sur **Exporter**.  

2.  Dans l'Assistant Exportation de certificats, cliquez sur **Suivant**.  

3.  Sur la page **Exporter la clé privée** , sélectionnez **Oui, exporter la clé privée**, puis cliquez sur **Suivant**.  

    > [!NOTE]  
    >  Si cette option n'est pas disponible, cela signifie que le certificat a été créé sans l'option permettant d'exporter la clé privée. Dans ce scénario, vous ne pouvez pas exporter le certificat dans le format requis. Vous devez reconfigurer le modèle de certificat pour autoriser l'exportation de la clé privée, puis redemander le certificat.  

4.  Sur la page **Format de fichier d'exportation** , assurez-vous que l'option **Personal Information Exchange - PKCS #12 (.PFX)** est sélectionnée.  

5.  Sur la page **Mot de passe** , spécifiez un mot de passe fort pour protéger le certificat exporté avec sa clé privée, puis cliquez sur **Suivant**.  

6.  Sur la page **Fichier à exporter** , spécifiez le nom du fichier que vous voulez exporter, puis cliquez sur **Suivant**.  

7.  Pour fermer l'Assistant, cliquez sur **Terminer** sur la page **Assistant Exportation de certificat** , puis cliquez sur **OK** dans la boîte de dialogue de confirmation.  

8.  Fermez la fenêtre **Certificats (ordinateur local)**.  

9. Stockez le fichier de façon sécurisée et vérifiez que vous pouvez y accéder à partir de la console System Center Configuration Manager.  

 Le certificat est prêt à l'importation dès que vous créez un point de distribution cloud.  

##  <a name="a-namebkmkclient2008cm2012a-deploying-the-client-certificate-for-windows-computers"></a><a name="BKMK_client2008_cm2012"></a> Déploiement du certificat client pour les ordinateurs Windows  
 Les procédures de ce déploiement de certificat sont les suivantes :  

-   Création et émission du modèle de certificat Authentification de station de travail sur l'autorité de certification  

-   Configuration de l'inscription automatique du modèle Authentification de station de travail à l'aide d'une stratégie de groupe  

-   Inscription automatique du certificat Authentification de station de travail et vérification de son installation sur les ordinateurs  

###  <a name="a-namebkmkclient02008a-creating-and-issuing-the-workstation-authentication-certificate-template-on-the-certification-authority"></a><a name="BKMK_client02008"></a> Création et émission du modèle de certificat Authentification de station de travail sur l'autorité de certification  
 Cette procédure crée un modèle de certificat pour les ordinateurs clients System Center Configuration Manager et l’ajoute à l’autorité de certification.  

##### <a name="to-create-and-issue-the-workstation-authentication-certificate-template-on-the-certification-authority"></a>Pour créer et émettre le modèle de certificat d’authentification de station de travail sur l’autorité de certification  

1.  Sur le serveur membre exécutant la console Autorité de certification, cliquez avec le bouton droit sur **Modèles de certificats**, puis cliquez sur **Gérer** pour charger la console de gestion des modèles de certificats.  

2.  Dans le volet de résultats, cliquez avec le bouton droit sur l'entrée qui affiche **Authentification de station de travail** dans la colonne **Nom complet du modèle**, puis cliquez sur **Dupliquer le modèle**.  

3.  Dans la boîte de dialogue **Dupliquer le modèle** , assurez-vous que l'option **Windows Server 2003, Enterprise Edition** est sélectionnée, puis cliquez sur **OK**.  

    > [!IMPORTANT]  
    >  Ne sélectionnez pas **Windows Server 2008, Enterprise Edition**.  

4.  Dans la boîte de dialogue **Propriétés du nouveau modèle** , sous l'onglet **Général** , entrez un nom de modèle pour générer les certificats clients à utiliser sur les ordinateurs clients Configuration Manager (par exemple, **Certificat client ConfigMgr**).  

5.  Cliquez sur l'onglet **Sécurité** , sélectionnez le groupe **Ordinateurs du domaine** , puis sélectionnez les autorisations supplémentaires **Lecture** et **Inscription automatique**. Ne désactivez pas l'option **Inscrire**.  

6.  Cliquez sur **OK** et fermez la **console Modèles de certificats**.  

7.  Dans la console Autorité de certification, cliquez avec le bouton droit sur **Modèles de certificats**, cliquez sur **Nouveau**, puis cliquez sur **Modèle de certificat à délivrer**.  

8.  Dans la boîte de dialogue **Activer les modèles de certificat** , sélectionnez le modèle que vous venez de créer ( **Certificat client ConfigMgr**), puis cliquez sur **OK**.  

9. Si vous n'avez pas besoin de créer ou d'émettre d'autres certificats, fermez **Autorité de Certification**.  

###  <a name="a-namebkmkclient12008a-configuring-autoenrollment-of-the-workstation-authentication-template-by-using-group-policy"></a><a name="BKMK_client12008"></a> Configuration de l'inscription automatique du modèle Authentification de station de travail à l'aide d'une stratégie de groupe  
 Cette procédure permet de configurer la stratégie de groupe pour inscrire automatiquement le certificat client sur les ordinateurs.  

##### <a name="to-configure-autoenrollment-of-the-workstation-authentication-template-by-using-group-policy"></a>Pour configurer l'inscription automatique du modèle Authentification de station de travail à l'aide d'une stratégie de groupe  

1.  Sur le contrôleur de domaine, cliquez sur **Démarrer**, pointez sur **Outils d'administration**, puis cliquez sur **Gestion des stratégies de groupe**.  

2.  Accédez à votre domaine, cliquez avec le bouton droit sur ce dernier, puis sélectionnez **Créer un objet GPO dans ce domaine, et le lier ici**.  

    > [!NOTE]  
    >  Cette étape utilise la meilleure pratique de création d'une stratégie de groupe pour des paramètres personnalisés ; elle ne modifie pas la stratégie de domaine par défaut qui est installée avec les services de domaine Active Directory. En affectant cette stratégie de groupe au niveau du domaine, vous l'appliquerez à tous les ordinateurs de ce domaine. Toutefois, dans un environnement de production, vous pouvez limiter l'inscription automatique aux ordinateurs sélectionnés en affectant la stratégie de groupe à un niveau d'unité organisationnelle, ou vous pouvez filtrer la stratégie de groupe du domaine avec un groupe de sécurité pour qu'elle s'applique uniquement aux ordinateurs du groupe. Si vous limitez l'inscription automatique, veillez à inclure le serveur configuré comme point de gestion.  

3.  Dans la boîte de dialogue **Nouvel objet GPO** , entrez un nom pour la nouvelle stratégie de groupe, par exemple **Certificats - Inscription automatique**, puis cliquez sur **OK**.  

4.  Dans le volet de résultats, sous l'onglet **Objets de stratégie de groupe liés** , cliquez avec le bouton droit sur la nouvelle stratégie de groupe, puis cliquez sur **Modifier**.  

5.  Dans la boîte de dialogue **Éditeur de gestion des stratégies de groupe**, développez **Stratégies** sous **Configuration ordinateur**, puis accédez à **Paramètres Windows** / **Paramètres de sécurité** / **Public Key Stratégies**.  

6.  Cliquez avec le bouton droit sur le type d’objet nommé **Client des services de certificats - Inscription automatique**, puis cliquez sur **Propriétés**.  

7.  Dans la liste déroulante **Modèle de configuration** , sélectionnez **Activé**, sélectionnez **Renouveler les certificats expirés, mettre à jour les certificats en attente et supprimer les certificats révoqués**, sélectionnez **Mettre à jour les certificats qui utilisent les modèles de certificats**, puis cliquez sur **OK**.  

8.  Fermez la fenêtre **Gestion des stratégies de groupe**.  

###  <a name="a-namebkmkclient22008a-automatically-enrolling-the-workstation-authentication-certificate-and-verifying-its-installation-on-computers"></a><a name="BKMK_client22008"></a> Inscription automatique du certificat Authentification de station de travail et vérification de son installation sur les ordinateurs  
 Cette procédure permet d'installer le certificat client sur les ordinateurs et de vérifier l'installation.  

##### <a name="to-automatically-enroll-the-workstation-authentication-certificate-and-verify-its-installation-on-the-client-computer"></a>Pour procéder à l'inscription automatique du certificat Authentification de station de travail et vérifier son installation sur l'ordinateur client  

1.  Redémarrez la station de travail et attendez quelques minutes avant l'ouverture de session.  

    > [!NOTE]  
    >  Le redémarrage de l'ordinateur constitue la méthode la plus fiable pour l'inscription automatique des certificats.  

2.  Ouvrez une session sous un compte bénéficiant d'autorisations d'administrateur.  

3.  Dans la zone de recherche, tapez **mmc.exe.**, puis appuyez sur **Entrée**.  

4.  Dans la console de gestion vide, cliquez sur **Fichier**, puis sur **Ajouter/Supprimer un composant logiciel enfichable**.  

5.  Dans la boîte de dialogue **Ajouter ou supprimer des composants logiciels enfichables** , sélectionnez **Certificats** dans la liste **Composants logiciels enfichables disponibles**, puis cliquez sur **Ajouter**.  

6.  Dans la boîte de dialogue **Composant logiciel enfichable des certificats** , cliquez sur **Compte d'ordinateur**, puis sur **Suivant**.  

7.  Dans la boîte de dialogue **Sélectionner un ordinateur** , vérifiez que **L'ordinateur local (l'ordinateur sur lequel cette console s'exécute)** est sélectionné, puis cliquez sur **Terminer**.  

8.  Dans la boîte de dialogue **Ajouter ou supprimer des composants logiciels enfichables** , cliquez sur **OK**.  

9. Dans la console, développez **Certificats (ordinateur local)**, développez **Personnel**, puis cliquez sur **Certificats**.  

10. Dans le volet de résultats, vérifiez qu'un certificat est affiché, avec la valeur **Authentification du client** indiquée dans la colonne **Rôle prévu** , et que **Certificat client ConfigMgr** est affiché dans la colonne **Modèle de certificat** .  

11. Fermez la fenêtre **Certificats (ordinateur local)**.  

12. Répétez les étapes 1 à 11 pour le serveur membre afin de vérifier que le serveur qui sera configuré comme point de gestion dispose également d'un certificat client.  

 L’ordinateur est maintenant configuré avec un certificat client System Center Configuration Manager.  

##  <a name="a-namebkmkclientdistributionpoint2008cm2012a-deploying-the-client-certificate-for-distribution-points"></a><a name="BKMK_clientdistributionpoint2008_cm2012"></a> Déploiement du certificat client pour les points de distribution  

> [!NOTE]  
>  Ce certificat peut également être utilisé pour les images de média qui n'utilisent pas le démarrage PXE, car la configuration requise pour le certificat est la même.  

 Les procédures de ce déploiement de certificat sont les suivantes :  

-   Création et émission d'un modèle de certificat Authentification de station de travail personnalisé sur l'autorité de certification  

-   Demande du certificat d'authentification de station de travail personnalisé  

-   Exportation du certificat client pour les points de distribution  

###  <a name="a-namebkmkclientdistributionpoint02008a-creating-and-issuing-a-custom-workstation-authentication-certificate-template-on-the-certification-authority"></a><a name="BKMK_clientdistributionpoint02008"></a> Création et émission d'un modèle de certificat Authentification de station de travail personnalisé sur l'autorité de certification  
 Cette procédure crée un modèle de certificat personnalisé pour les points de distribution System Center Configuration Manager, qui permet d’exporter la clé privée, et ajoute ce nouveau modèle à l’autorité de certification.  

> [!NOTE]  
>  Cette procédure utilise un modèle de certificat différent du modèle de certificat créé pour les ordinateurs clients. En effet, les deux certificats requièrent des fonctions d'authentification du client, mais le certificat pour les points de distribution requiert l'exportation de la clé privée. Comme meilleure pratique de sécurité, ne configurez pas les modèles de certificats autorisant l'exportation la clé privée, sauf si cette configuration est requise. Le point de distribution requiert cette configuration, car vous devez importer le certificat en tant que fichier, au lieu de le sélectionner dans le magasin de certificats.  
>   
>  En créant un nouveau modèle de certificat pour ce certificat, vous pouvez limiter les ordinateurs qui demandent un certificat autorisant l'exportation de la clé privée. Dans notre exemple de déploiement, il s’agit du groupe de sécurité que vous avez créé précédemment pour les serveurs de système de site System Center Configuration Manager qui exécutent IIS. Sur un réseau de production qui distribue les rôles de système de site IIS, envisagez de créer un groupe de sécurité pour les serveurs exécutant des points de distribution, afin de limiter le certificat à ces serveurs de système de site uniquement. Vous pouvez également considérer d'apporter les modifications suivantes à ce certificat :  
>   
>  -   Demander l'approbation d'installer le certificat, pour plus de sécurité.  
> -   Augmenter la période de validité du certificat. Étant donné que vous devez exporter, puis importer le certificat chaque fois avant son expiration, l'augmentation de la période de validité permet de réduire la fréquence de cette procédure. Cependant, l'augmentation de la période de validité diminue la sécurité du certificat, car une personne malveillante a plus de temps pour déchiffrer la clé privée et voler le certificat.  
> -   Utiliser une valeur personnalisée dans le champ Objet du certificat ou Autre nom de l'objet pour aider à identifier ce certificat parmi les certificats de client standard. Cela peut s'avérer particulièrement utile si vous utilisez le même certificat pour plusieurs points de distribution.  

##### <a name="to-create-and-issue-the-custom-workstation-authentication-certificate-template-on-the-certification-authority"></a>Pour créer et émettre le modèle de certificat Authentification de station de travail personnalisé sur l'autorité de certification  

1.  Sur le serveur membre exécutant la console Autorité de certification, cliquez avec le bouton droit sur **Modèles de certificats**, puis cliquez sur **Gérer** pour charger la console de gestion des modèles de certificats.  

2.  Dans le volet de résultats, cliquez avec le bouton droit sur l'entrée qui affiche **Authentification de station de travail** dans la colonne **Nom complet du modèle**, puis cliquez sur **Dupliquer le modèle**.  

3.  Dans la boîte de dialogue **Dupliquer le modèle** , assurez-vous que l'option **Windows Server 2003, Enterprise Edition** est sélectionnée, puis cliquez sur **OK**.  

    > [!IMPORTANT]  
    >  Ne sélectionnez pas **Windows Server 2008, Enterprise Edition**.  

4.  Dans la boîte de dialogue **Propriétés du nouveau modèle** , sous l'onglet **Général** , entrez un nom de modèle pour générer le certificat d'authentification client des points de distribution, tel que **Certificat de point de distribution client ConfigMgr**.  

5.  Cliquez sur l'onglet **Traitement de la demande** et sélectionnez **Autoriser l'exportation de la clé privée**.  

6.  Cliquez sur l'onglet **Sécurité** et supprimez l'autorisation **Inscription** du groupe de sécurité **Administrateurs d'entreprise** .  

7.  Cliquez sur **Ajouter**, tapez **Serveurs ConfigMgr IIS** dans la zone de texte, puis cliquez sur **OK**.  

8.  Sélectionnez l'autorisation **Inscription** pour ce groupe et ne désactivez pas l'autorisation **Lecture** .  

9. Cliquez sur **OK** et fermez la **console Modèles de certificats**.  

10. Dans la console Autorité de certification, cliquez avec le bouton droit sur **Modèles de certificats**, cliquez sur **Nouveau**, puis cliquez sur **Modèle de certificat à délivrer**.  

11. Dans la boîte de dialogue **Activer les modèles de certificat** , sélectionnez le modèle que vous venez de créer ( **Certificat de point de distribution client ConfigMgr**), puis cliquez sur **OK**.  

12. Si vous n'avez pas besoin de créer ou d'émettre d'autres certificats, fermez **Autorité de certification**.  

###  <a name="a-namebkmkclientdistributionpoint12008a-requesting-the-custom-workstation-authentication-certificate"></a><a name="BKMK_clientdistributionpoint12008"></a> Demande du certificat d'authentification de station de travail personnalisé  
 Cette procédure permet de demander, puis d'installer le certificat client personnalisé sur le serveur membre qui exécute IIS et qui sera configuré comme point de distribution.  

##### <a name="to-request-the-custom-workstation-authentication-certificate"></a>Pour demander le certificat d'authentification de station de travail personnalisé  

1.  Cliquez sur **Démarrer**, cliquez sur **Exécuter**, puis tapez **mmc.exe.** Dans la console vide, cliquez sur **Fichier**, puis cliquez sur **Ajouter/Supprimer un composant logiciel enfichable**.  

2.  Dans la boîte de dialogue **Ajouter ou supprimer des composants logiciels enfichables** , sélectionnez **Certificats** dans la liste **Composants logiciels enfichables disponibles**, puis cliquez sur **Ajouter**.  

3.  Dans la boîte de dialogue **Composant logiciel enfichable des certificats** , cliquez sur **Compte d'ordinateur**, puis sur **Suivant**.  

4.  Dans la boîte de dialogue **Sélectionner un ordinateur** , vérifiez que **L'ordinateur local (l'ordinateur sur lequel cette console s'exécute)** est sélectionné, puis cliquez sur **Terminer**.  

5.  Dans la boîte de dialogue **Ajouter ou supprimer des composants logiciels enfichables** , cliquez sur **OK**.  

6.  Dans la console, développez **Certificats (ordinateur local)**, puis cliquez sur **Personnel**.  

7.  Cliquez avec le bouton droit sur **Certificats**, cliquez sur **Toutes les tâches**, puis cliquez sur **Demander un nouveau certificat**.  

8.  Dans la page **Avant de commencer** , cliquez sur **Suivant**.  

9. Si vous voyez la page **Sélectionner la stratégie d'inscription de certificat** , cliquez sur **Suivant**.  

10. Sur la page **Demander des certificats** , sélectionnez **Certificat de point de distribution client ConfigMgr** dans la liste des certificats affichés, puis cliquez sur **Inscrire**.  

11. Sur la page **Résultats de l'installation** des certificats, attendez que le certificat soit installé, puis cliquez sur **Terminer**.  

12. Dans le volet de résultats, vérifiez qu'un certificat est affiché, avec la valeur **Authentification du client** indiquée dans la colonne **Rôle prévu** , et que **Certificat de point de distribution client ConfigMgr** est affiché dans la colonne **Modèle de certificat** .  

13. Ne fermez pas la fenêtre **Certificats (ordinateur local)**.  

###  <a name="a-namebkmkexportclientdistributionpoint22008a-exporting-the-client-certificate-for-distribution-points"></a><a name="BKMK_exportclientdistributionpoint22008"></a> Exportation du certificat client pour les points de distribution  
 Cette procédure exporte le certificat Authentification de station de travail personnalisé vers un fichier, afin qu'il puisse être importé dans les propriétés du point de distribution.  

##### <a name="to-export-the-client-certificate-for-distribution-points"></a>Pour exporter le certificat du client pour les points de distribution  

1.  Dans la console **Certificats (ordinateur local)** , cliquez avec le bouton droit sur le certificat que vous venez d'installer, sélectionnez **Toutes les tâches**, puis cliquez sur **Exporter**.  

2.  Dans l'Assistant Exportation de certificats, cliquez sur **Suivant**.  

3.  Sur la page **Exporter la clé privée** , sélectionnez **Oui, exporter la clé privée**, puis cliquez sur **Suivant**.  

    > [!NOTE]  
    >  Si cette option n'est pas disponible, cela signifie que le certificat a été créé sans l'option permettant d'exporter la clé privée. Dans ce scénario, vous ne pouvez pas exporter le certificat dans le format requis. Vous devez reconfigurer le modèle de certificat pour autoriser l'exportation de la clé privée, puis redemander le certificat.  

4.  Sur la page **Format de fichier d'exportation** , assurez-vous que l'option **Personal Information Exchange - PKCS #12 (.PFX)** est sélectionnée.  

5.  Sur la page **Mot de passe** , spécifiez un mot de passe fort pour protéger le certificat exporté avec sa clé privée, puis cliquez sur **Suivant**.  

6.  Sur la page **Fichier à exporter** , spécifiez le nom du fichier que vous voulez exporter, puis cliquez sur **Suivant**.  

7.  Pour fermer l'Assistant, cliquez sur **Terminer** sur la page **Assistant Exportation de certificat** , puis cliquez sur **OK** dans la boîte de dialogue de confirmation.  

8.  Fermez la fenêtre **Certificats (ordinateur local)**.  

9. Stockez le fichier de façon sécurisée et vérifiez que vous pouvez y accéder à partir de la console System Center Configuration Manager.  

 Le certificat est maintenant prêt à être importé lorsque vous configurez le point de distribution.  

> [!TIP]  
>  Vous pouvez utiliser le même fichier de certificat lors de la configuration d'images de média pour un déploiement de système d'exploitation qui n'utilise pas le démarrage PXE, et la séquence de tâches d'installation de l'image doit contacter un point de gestion qui requiert des connexions de client HTTPS.  

##  <a name="a-namebkmkmobiledevices2008cm2012a-deploying-the-enrollment-certificate-for-mobile-devices"></a><a name="BKMK_mobiledevices2008_cm2012"></a> Déploiement du certificat d'inscription pour les périphériques mobiles  
 Ce déploiement de certificat a une procédure unique pour créer et émettre le modèle de certificat d'inscription sur l'autorité de certification.  

### <a name="creating-and-issuing-the-enrollment-certificate-template-on-the-certification-authority"></a>Création et émission du modèle de certificat d'inscription sur l'autorité de certification  
 Cette procédure crée un modèle de certificat d’inscription pour les appareils mobiles System Center Configuration Manager et l’ajoute à l’autorité de certification.  

##### <a name="to-create-and-issue-the-enrollment-certificate-template-on-the-certification-authority"></a>Pour créer et émettre le modèle de certificat d'inscription sur l'autorité de certification  

1.  Créez un groupe de sécurité contenant les utilisateurs qui vont inscrire des appareils mobiles dans System Center Configuration Manager.  

2.  Sur le serveur membre sur lequel les services de certificats sont installés, dans la console Autorité de certification, cliquez avec le bouton droit sur **Modèles de certificats**, puis cliquez sur **Gérer** pour charger la console de gestion des modèles de certificats.  

3.  Dans le volet des résultats, cliquez avec le bouton droit sur l'entrée qui affiche **Session authentifiée** dans la colonne **Nom complet du modèle**, puis cliquez sur **Dupliquer le modèle**.  

4.  Dans la boîte de dialogue **Dupliquer le modèle** , assurez-vous que l'option **Windows Server 2003, Enterprise Edition** est sélectionnée, puis cliquez sur **OK**.  

    > [!IMPORTANT]  
    >  Ne sélectionnez pas **Windows Server 2008, Enterprise Edition**.  

5.  Dans la boîte de dialogue **Propriétés du nouveau modèle**, sous l’onglet **Général**, entrez un nom de modèle pour générer les certificats d’inscription pour les appareils mobiles devant être gérés par System Center Configuration Manager (par exemple, **Certificat d’inscription d'appareil mobile ConfigMgr**).  

6.  Cliquez sur l'onglet **Nom de l'objet** , vérifiez que l'option **Construire à partir de ces informations Active Directory** est sélectionnée, sélectionnez **Nom commun** comme **Format du nom de l'objet** , puis supprimez **Nom d'utilisateur principal (UPN)** de **Inclure cette information dans le nom de substitution du sujet**.  

7.  Cliquez sur l'onglet **Sécurité**, sélectionnez le groupe de sécurité qui contient les utilisateurs qui ont des appareils mobiles à inscrire et sélectionnez l'autorisation supplémentaire **Inscription**. Ne désactivez pas l'option **Lecture**.  

8.  Cliquez sur **OK** et fermez la **console Modèles de certificats**.  

9. Dans la console Autorité de certification, cliquez avec le bouton droit sur **Modèles de certificats**, cliquez sur **Nouveau**, puis cliquez sur **Modèle de certificat à délivrer**.  

10. Dans la boîte de dialogue **Activer les modèles de certificat** , sélectionnez le modèle que vous venez de créer, **Certificat d'inscription de périphérique mobile ConfigMgr**, puis cliquez sur **OK**.  

11. Si vous n'avez pas besoin de créer ou d'émettre d'autres certificats, fermez la console Autorité de certification.  

 Le modèle de certificat d'inscription d'appareil mobile est maintenant prêt à être sélectionné lorsque vous configurez un profil d'inscription d'appareil mobile dans les paramètres du client.  

##  <a name="a-namebkmkamt2008cm2012a-deploying-the-certificates-for-amt"></a><a name="BKMK_AMT2008_cm2012"></a> Déploiement des certificats pour AMT  
 Les procédures de ce déploiement de certificat sont les suivantes :  

-   Création, émission et installation du certificat de configuration AMT  

-   Création et émission du certificat de serveur Web pour les ordinateurs basés sur AMT  

-   Création et émission des certificats d'authentification du client pour les ordinateurs basés sur AMT 802.1X  

###  <a name="a-namebkmkamtprovisioning2008a-creating-issuing-and-installing-the-amt-provisioning-certificate"></a><a name="BKMK_AMTprovisioning2008"></a> Creating, Issuing, and Installing the AMT Provisioning Certificate  
 Créez le certificat de configuration avec votre autorité de certification interne lorsque les ordinateurs basés sur AMT sont configurés avec l'empreinte numérique du certificat de votre autorité de certification racine interne. Lorsque ce n’est pas le cas et que vous devez utiliser une autorité de certification externe, suivez les instructions de la société émettrice du certificat de configuration AMT, qui exige souvent le certificat du site web public de l’entreprise. Vous pouvez également trouver des instructions détaillées sur l'autorité de certification externe sur le site Intel vPro Expert Center : Microsoft vPro Manageability ([http://go.microsoft.com/fwlink/?LinkId=132001](http://go.microsoft.com/fwlink/?LinkId=132001)).  

> [!IMPORTANT]  
>  Il se peut que des autorités de certification externes ne prennent pas en charge l'identificateur d'objet de configuration Intel AMT. Dans ce cas, recourez à la méthode consistant à fournir l'attribut de l'unité d'organisation du certificat **Intel(R) Client Setup Certificate**.  

 Lorsque vous demandez un certificat de configuration AMT d'une autorité de certification externe, installez le certificat dans le magasin personnel des certificats sur le serveur membre qui va héberger le point de service hors bande.  

##### <a name="to-request-and-issue-the-amt-provisioning-certificate"></a>Pour demander et émettre le certificat de configuration AMT  

1.  Créez un groupe de sécurité qui contient les comptes d'ordinateur des serveurs de système de site qui exécuteront le point de service hors bande.  

2.  Sur le serveur membre sur lequel les services de certificats sont installés, dans la console Autorité de certification, cliquez avec le bouton droit sur **Modèles de certificats**, puis cliquez sur **Gérer** pour charger la console **Modèles de certificats** .  

3.  Dans le volet de résultats, cliquez avec le bouton droit sur l'entrée qui affiche **Serveur Web** dans la colonne **Nom complet du modèle** , puis cliquez sur **Modèle dupliqué**.  

4.  Dans la boîte de dialogue **Dupliquer le modèle** , assurez-vous que l'option **Windows Server 2003, Enterprise Edition** est sélectionnée, puis cliquez sur **OK**.  

    > [!IMPORTANT]  
    >  Ne sélectionnez pas **Windows Server 2008, Enterprise Edition**.  

5.  Sous l'onglet **Général** de la boîte de dialogue **Propriétés du nouveau modèle** , entrez un nom pour le modèle de certificat de configuration AMT (par exemple, **Configuration AMT ConfigMgr**).  

6.  Cliquez sur l'onglet **Nom d'objet** et sélectionnez **Construire à partir de ces informations Active Directory**, puis **Nom commun**.  

7.  Sous l'onglet **Extensions** , vérifiez que l'option **Stratégies d'application** est activée, puis cliquez sur **Modifier**.  

8.  Dans la boîte de dialogue **Modifier l'extension des stratégies d'application** , cliquez sur **Ajouter**.  

9. Dans la boîte de dialogue **Ajouter une stratégie d'application** , cliquez sur **Nouveau**.  

10. Dans la boîte de dialogue **Nouvelle stratégie d'application** , entrez **Configuration AMT** dans le champ **Nom** , puis le numéro suivant dans le champ **Identificateur d'objet**: **2.16.840.1.113741.1.2.3**.  

11. Cliquez sur **OK**, puis cliquez une nouvelle fois sur **OK** dans la boîte de dialogue **Ajouter une stratégie d'application** .  

12. Cliquez sur **OK** dans la boîte de dialogue **Modifier l'extension des stratégies d'application** .  

13. Dans la boîte de dialogue **Propriétés du nouveau modèle** , la description des **Stratégies d'application** doit maintenant indiquer : **Authentification du serveur** et **Configuration AMT**.  

14. Sous l'onglet **Sécurité** , supprimez l'autorisation **Inscription** des groupes de sécurité **Administrateurs du domaine** et **Administrateurs de l'entreprise**.  

15. Cliquez sur **Ajouter**, entrez le nom d'un groupe de sécurité qui contient le compte d'ordinateur pour le rôle de système de site du point de service hors bande, puis cliquez sur **OK**.  

16. Sélectionnez l'autorisation **Inscription** pour ce groupe et ne désactivez pas l'autorisation **Lecture** .  

17. Cliquez sur **OK**, puis fermez la console **Modèles de certificats** .  

18. Sous **Autorité de certification**, cliquez avec le bouton droit sur **Modèles de certificats**, cliquez sur **Nouveau**, puis cliquez sur **Modèle de certificat à délivrer**.  

19. Dans la boîte de dialogue **Activer les modèles de certificats** , sélectionnez le modèle que vous venez de créer ( **Configuration AMT ConfigMgr**), puis cliquez sur **OK**.  

    > [!NOTE]  
    >  Si vous ne pouvez pas effectuer l'étape 18 ou 19, vérifiez que vous utilisez Windows Server 2008 Enterprise Edition. Bien que vous puissiez configurer des modèles dans Windows Server Standard Edition et les services de certificats, vous ne pouvez déployer des certificats à l'aide de modèles de certificats modifiés que dans Windows Server 2008 Enterprise Edition.  

20. Ne fermez pas l' **autorité de certification**.  

 Le certificat de configuration AMT de votre autorité de certification interne est maintenant prêt à être installé sur l'ordinateur du point de service hors bande.  

##### <a name="to-install-the-amt-provisioning-certificate"></a>Pour installer le certificat de configuration AMT  

1.  Redémarrez le serveur membre qui exécute IIS pour vérifier qu'il peut accéder au modèle de certificat via l'autorisation définie.  

2.  Cliquez sur **Démarrer**, cliquez sur **Exécuter**, puis tapez **mmc.exe.** Dans la console vide, cliquez sur **Fichier**, puis cliquez sur **Ajouter/Supprimer un composant logiciel enfichable**.  

3.  Dans la boîte de dialogue **Ajouter ou supprimer des composants logiciels enfichables** , sélectionnez **Certificats** dans la liste **Composants logiciels enfichables disponibles**, puis cliquez sur **Ajouter**.  

4.  Dans la boîte de dialogue **Composant logiciel enfichable des certificats** , cliquez sur **Compte d'ordinateur**, puis sur **Suivant**.  

5.  Dans la boîte de dialogue **Sélectionner un ordinateur** , vérifiez que **L'ordinateur local (l'ordinateur sur lequel cette console s'exécute)** est sélectionné, puis cliquez sur **Terminer**.  

6.  Dans la boîte de dialogue **Ajouter ou supprimer des composants logiciels enfichables** , cliquez sur **OK**.  

7.  Dans la console, développez **Certificats (ordinateur local)**, puis cliquez sur **Personnel**.  

8.  Cliquez avec le bouton droit sur **Certificats**, cliquez sur **Toutes les tâches**, puis cliquez sur **Demander un nouveau certificat**.  

9. Dans la page **Avant de commencer** , cliquez sur **Suivant**.  

10. Si vous voyez la page **Sélectionner la stratégie d'inscription de certificat** , cliquez sur **Suivant**.  

11. Sur la page **Demander des certificats** , sélectionnez **Préparation AMT** dans la liste des certificats affichés, puis cliquez sur **Inscription**.  

12. Sur la page **Résultats de l'installation** des certificats, attendez que le certificat soit installé, puis cliquez sur **Terminer**.  

13. Fermez la fenêtre **Certificats (ordinateur local)**.  

 Le certificat de configuration AMT de votre autorité de certification interne est maintenant installé et peut être sélectionné pour les propriétés du point de service hors bande.  

### <a name="creating-and-issuing-the-web-server-certificate-for-amt-based-computers"></a>Création et émission du certificat de serveur Web pour les ordinateurs basés sur AMT  
 Procédez comme suit pour préparer les certificats de serveur Web pour les ordinateurs basés sur AMT.  

##### <a name="to-create-and-issue-the-web-server-certificate-template"></a>Pour créer et émettre le modèle de certificat du serveur Web  

1.  Créez un groupe de sécurité vide qui contiendra les comptes d’ordinateur AMT créés par System Center Configuration Manager lors de la configuration AMT.  

2.  Sur le serveur membre sur lequel les services de certificats sont installés, dans la console Autorité de certification, cliquez avec le bouton droit sur **Modèles de certificats**, puis cliquez sur **Gérer** pour charger la console **Modèles de certificats** .  

3.  Dans le volet de résultats, cliquez avec le bouton droit sur l'entrée qui affiche **Serveur Web** dans la colonne **Nom complet du modèle**, puis cliquez sur **Dupliquer le modèle**.  

4.  Dans la boîte de dialogue **Dupliquer le modèle** , assurez-vous que l'option **Windows Server 2003, Enterprise Edition** est sélectionnée, puis cliquez sur **OK**.  

    > [!IMPORTANT]  
    >  Ne sélectionnez pas **Windows Server 2008, Enterprise Edition.**  

5.  Dans l'onglet **Général** de la boîte de dialogue **Propriétés du nouveau modèle** , entrez un nom de modèle pour générer les certificats Web à utiliser pour la gestion hors bande sur les ordinateurs AMT, par exemple, **Certificat de serveur Web AMT ConfigMgr**.  

6.  Cliquez sur l'onglet **Nom de l'objet** , puis sur **Construire à partir de ces informations Active Directory**, sélectionnez **Nom commun** pour le **Format du nom de l'objet**, supprimez **Nom d'utilisateur principal (UPN)** pour l'autre nom de l'objet.  

7.  Sous l'onglet **Sécurité** , supprimez l'autorisation **Inscription** des groupes de sécurité **Administrateurs du domaine** et **Administrateurs de l'entreprise**.  

8.  Cliquez sur **Ajouter** et entrez le nom du groupe de sécurité que vous avez créé pour la configuration AMT. Cliquez ensuite sur **OK**.  

9. Sélectionnez ces autorisations **Autoriser** applicables à ce groupe de sécurité : **Lecture** et **Inscription**.  

10. Cliquez sur **OK**, puis fermez la console **Modèles de certificats** .  

11. Dans la console **Autorité de certification** , cliquez avec le bouton droit sur **Modèles de certificats**, cliquez sur **Nouveau**, puis cliquez sur **Modèle de certificat à délivrer**.  

12. Dans la boîte de dialogue **Activer les modèles de certificat** , sélectionnez le modèle que vous venez de créer ( **Certificat de serveur Web AMT ConfigMgr**), puis cliquez sur **OK**.  

13. Si vous n'avez pas besoin de créer ou d'émettre d'autres certificats, fermez **Autorité de certification**.  

 Le modèle de serveur Web AMT est maintenant prêt pour la configuration d'ordinateurs basés sur AMT avec des certificats de serveur Web. Sélectionnez ce modèle de certificat dans les propriétés du composant de gestion hors bande.  

### <a name="creating-and-issuing-the-client-authentication-certificates-for-8021x-amt-based-computers"></a>Création et émission des certificats d'authentification du client pour les ordinateurs basés sur AMT 802.1X  
 Utilisez la procédure suivante si les ordinateurs basés sur AMT utilisent des certificats clients pour les réseaux filaires ou sans fil authentifiés par 802.1X.  

##### <a name="to-create-and-issue-the-client-authentication-certificate-template-on-the-ca"></a>Pour créer et émettre le modèle de certificat d'authentification client sur l'autorité de certification  

1.  Sur le serveur membre sur lequel les services de certificats sont installés, dans la console Autorité de certification, cliquez avec le bouton droit sur **Modèles de certificats**, puis cliquez sur **Gérer** pour charger la console **Modèles de certificats** .  

2.  Dans le volet de résultats, cliquez avec le bouton droit sur l'entrée qui affiche **Authentification de station de travail** dans la colonne **Nom complet du modèle**, puis cliquez sur **Dupliquer le modèle**.  

    > [!IMPORTANT]  
    >  Ne sélectionnez pas **Windows Server 2008, Enterprise Edition.**  

3.  Sous l'onglet **Général** de la boîte de dialogue **Propriétés du nouveau modèle** , entrez un nom de modèle pour générer les certificats client à utiliser pour la gestion hors bande sur les ordinateurs AMT. Par exemple, **Certificat d'authentification client 802.1X AMT ConfigMgr**.  

4.  Dans l'onglet **Nom de l'objet** , cliquez sur **Construire à partir de ces informations Active Directory** , puis sélectionnez **Nom commun** comme **Format du nom de l'objet**. Désactivez **Nom DNS** pour l'autre nom de l'objet, et sélectionnez **Nom d'utilisateur principal (UPN)**.  

5.  Sous l'onglet **Sécurité** , supprimez l'autorisation **Inscription** des groupes de sécurité **Administrateurs du domaine** et **Administrateurs de l'entreprise**.  

6.  Cliquez sur **Ajouter** et entrez le nom du groupe de sécurité que vous spécifierez dans les propriétés du composant de gestion hors bande, pour contenir les comptes d'ordinateur des ordinateurs basés sur AMT. Cliquez ensuite sur **OK**.  

7.  Sélectionnez ces autorisations **Autoriser** applicables à ce groupe de sécurité : **Lecture** et **Inscription**.  

8.  Cliquez sur **OK**, puis refermez la console de gestion **Modèles de certificats**, **certtmpl - [Modèles de certificats]**.  

9. Dans la console de gestion **Autorité de certification** , cliquez avec le bouton droit sur **Modèles de certificats**, cliquez sur **Nouveau**, puis cliquez sur **Modèle de certificat à délivrer**.  

10. Dans la boîte de dialogue **Activer les modèles de certificat** , sélectionnez le modèle que vous venez de créer ( **Certificat d'authentification client 802.1X AMT ConfigMgr**), puis cliquez sur **OK**.  

11. Si vous n'avez pas besoin de créer ou d'émettre d'autres certificats, fermez **Autorité de Certification**.  

 Le modèle de certificat d'authentification client est maintenant prêt à émettre des certificats d'ordinateurs AMT utilisables pour l'authentification client 802.1X. Sélectionnez ce modèle de certificat dans les propriétés du composant de gestion hors bande.  

##  <a name="a-namebkmkmacclientsp1a-deploying-the-client-certificate-for-mac-computers"></a><a name="BKMK_MacClient_SP1"></a> Déploiement du certificat client pour les ordinateurs Mac  

> [!NOTE]  
>  Le certificat client pour les ordinateurs Mac s’applique à System Center Configuration Manager SP1 et versions ultérieures.  

 Ce déploiement de certificat a une procédure unique pour créer et émettre le modèle de certificat d'inscription sur l'autorité de certification.  

###  <a name="a-namebkmkmacclientcreatingissuinga-creating-and-issuing-a-mac-client-certificate-template-on-the-certification-authority"></a><a name="BKMK_MacClient_CreatingIssuing"></a> Création et émission d'un modèle de certificat de client Mac sur l'autorité de certification  
 Cette procédure crée un modèle de certificat personnalisé pour les ordinateurs Mac System Center Configuration Manager et l’ajoute à l’autorité de certification.  

> [!NOTE]  
>  Cette procédure utilise un modèle de certificat différent du modèle de certificat que vous avez peut-être créé pour des ordinateurs clients Windows ou pour des points de distribution.  
>   
>  En créant un nouveau modèle de certificat pour ce certificat, vous pouvez limiter la demande de certificat aux utilisateurs autorisés.  

##### <a name="to-create-and-issue-the-mac-client-certificate-template-on-the-certification-authority"></a>Pour créer et émettre le modèle de certificat client Mac sur l'autorité de certification  

1.  Créez un groupe de sécurité qui contient les comptes des utilisateurs administratifs qui vont inscrire le certificat sur l’ordinateur Mac à l’aide de System Center Configuration Manager.  

2.  Sur le serveur membre exécutant la console Autorité de certification, cliquez avec le bouton droit sur **Modèles de certificats**, puis cliquez sur **Gérer** pour charger la console de gestion des modèles de certificats.  

3.  Dans le volet des résultats, cliquez avec le bouton droit sur l'entrée qui affiche **Session authentifiée** dans la colonne **Nom complet du modèle**, puis cliquez sur **Dupliquer le modèle**.  

4.  Dans la boîte de dialogue **Dupliquer le modèle** , assurez-vous que l'option **Windows Server 2003, Enterprise Edition** est sélectionnée, puis cliquez sur **OK**.  

    > [!IMPORTANT]  
    >  Ne sélectionnez pas **Windows Server 2008, Enterprise Edition**.  

5.  Dans la boîte de dialogue **Propriétés du nouveau modèle** , sous l'onglet **Général** , entrez un nom de modèle pour générer le certificat de client Mac, tel que **Certificat de client Mac ConfigMgr**.  

6.  Cliquez sur l'onglet **Nom de l'objet** , vérifiez que l'option **Construire à partir de ces informations Active Directory** est sélectionnée, sélectionnez **Nom commun** comme **Format du nom de l'objet** , puis supprimez **Nom d'utilisateur principal (UPN)** de **Inclure cette information dans le nom de substitution du sujet**.  

7.  Sous l'onglet **Sécurité** , supprimez l'autorisation **Inscription** des groupes de sécurité **Administrateurs du domaine** et **Administrateurs de l'entreprise** .  

8.  Cliquez sur **Ajouter**, spécifiez le groupe de sécurité que vous avez créé à l'étape 1, puis cliquez sur **OK**.  

9. Sélectionnez l'autorisation **Inscription** pour ce groupe et ne désactivez pas l'autorisation **Lecture** .  

10. Cliquez sur **OK** et fermez la **console Modèles de certificats**.  

11. Dans la console Autorité de certification, cliquez avec le bouton droit sur **Modèles de certificats**, cliquez sur **Nouveau**, puis cliquez sur **Modèle de certificat à délivrer**.  

12. Dans la boîte de dialogue **Activer les modèles de certificat** , sélectionnez le modèle que vous venez de créer ( **Certificat client Mac ConfigMgr**), puis cliquez sur **OK**.  

13. Si vous n'avez pas besoin de créer ou d'émettre d'autres certificats, fermez **Autorité de certification**.  

 Le modèle de certificat de client Mac est maintenant prêt à être sélectionné lorsque vous configurez des paramètres client pour l'inscription.



<!--HONumber=Nov16_HO1-->


