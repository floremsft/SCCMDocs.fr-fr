---
title: "Planifier la sécurité dans System Center Configuration Manager"
description: "Découvrez les bonnes pratiques et d’autres informations relatives à la sécurité dans System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2a216814-ca8c-4d2e-bcef-dc00966a3c9f
caps.latest.revision: 6
caps.handback.revision: 0
author: Nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: f38d7275a39d16f9e6cf90334a46668fcc860bc1


---
# <a name="plan-for-security-in-system-center-configuration-manager"></a>Planifier la sécurité dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Aidez-vous des informations contenues dans cette rubrique pour planifier la sécurité dans System Center Configuration Manager.  

   Pour plus d’informations sur la façon dont Configuration Manager utilise les certificats et les contrôles de chiffrement, consultez [Informations techniques de référence sur les contrôles de chiffrement pour System Center Configuration Manager](../../../protect/deploy-use/cryptographic-controls-technical-reference.md).  


##  <a name="a-namebkmkplanningforcertificatesa-planning-for-certificates-self-signed-and-pki"></a><a name="BKMK_PlanningForCertificates"></a> Planification des certificats (auto-signés et PKI)  
 Configuration Manager utilise une combinaison de certificats auto-signés et de certificats pour infrastructure à clé publique (PKI).  

 Comme meilleure pratique de sécurité, utilisez des certificats PKI dès que possible. Pour plus d’informations sur la configuration requise pour les certificats PKI, consultez [Configuration requise des certificats PKI pour System Center Configuration Manager](../../../core/plan-design/network/pki-certificate-requirements.md). Si Configuration Manager demande des certificats PKI, notamment pendant l’inscription d’appareils mobiles et la configuration AMT, vous devez utiliser les services de domaine Active Directory et une autorité de certification d’entreprise. Tous les autres certificats PKI doivent être déployés et gérés indépendamment de Configuration Manager.  

 Les certificats PKI sont également requis lorsque des ordinateurs clients se connectent à des systèmes de site basés sur Internet et il est recommandé de les utiliser lorsque des clients se connectent à des systèmes de site qui exécutent les services IIS. Pour plus d’informations sur les communications client, consultez [Guide pratique pour configurer les ports de communication des clients dans System Center Configuration Manager](../../../core/clients/deploy/configure-client-communication-ports.md).  

 Lorsque vous utilisez une infrastructure à clés publiques, vous pouvez également utiliser IPsec pour renforcer la sécurité de la communication serveur à serveur entre les systèmes de site d'un site et entre les sites et pour tout autre scénario lorsque vous transférez des données entre ordinateurs. Vous devez configurer et implémenter IPsec indépendamment de Configuration Manager.  

 Configuration Manager peut générer automatiquement des certificats auto-signés en l’absence de certificats PKI disponibles. Dans Configuration Manager, certains certificats sont toujours auto-signés. Dans la plupart des cas, Configuration Manager gère automatiquement les certificats auto-signés, et vous n’avez rien à faire de plus. Une exception possible est le certificat de signature du serveur de site. Le certificat de signature du serveur de site est toujours auto-signé et il garantit que les stratégies client que les clients téléchargent à partir du point de gestion ont été envoyées à partir du serveur de site et n'ont pas été falsifiées.  

### <a name="planning-for-the-site-server-signing-certificate-self-signed"></a>Planification du certificat de signature du serveur de site (auto-signé)  
 Les clients peuvent obtenir en toute sécurité une copie du certificat de signature du serveur de site à partir des services de domaine Active Directory et à partir de l'installation poussée du client. Si les clients ne peuvent pas obtenir une copie du certificat de signature du serveur de site selon l'un de ces mécanismes, une meilleure pratique de sécurité consiste à installer une copie du certificat de signature du serveur de site lorsque vous installez le client. Cela est particulièrement important si la première communication du client avec le site s’effectue via Internet, car le point de gestion est connecté à un réseau non approuvé et donc, vulnérable aux attaques. Si vous ne prenez pas cette mesure supplémentaire, les clients téléchargent automatiquement une copie du certificat de signature du serveur de site à partir du point de gestion.  

 Les scénarios suivants se présentent lorsque les clients ne peuvent pas obtenir une copie du certificat du serveur de site en toute sécurité :  

-   Vous n'installez pas le client de manière poussée et l'une des conditions suivantes est vraie :  

    -   Le schéma Active Directory n’est pas étendu pour Configuration Manager.  

    -   Le site du client n’est pas publié dans les services de domaine Active Directory.  

    -   Le client est issu d'une forêt non approuvée ou d'un groupe de travail.  

-   Vous installez le client lorsqu'il se trouve sur Internet.  

Pour installer des clients ainsi qu'une copie du certificat de signature du serveur de site, procédez comme suit.  

##### <a name="to-install-clients-with-a-copy-of-the-site-server-signing-certificate"></a>Pour installer des clients ainsi qu'une copie du certificat de signature du serveur de site  

1.  Recherchez le certificat de signature du serveur de site sur le serveur de site principal du client. Le certificat est stocké dans le magasin de certificats **SMS** et possède le nom d'objet **Serveur de site** et le nom convivial **Certificat de signature du serveur de site**.  

2.  Exportez le certificat sans la clé privée, stockez le fichier dans un emplacement sécurisé et accédez-y uniquement à partir d'un canal sécurisé (par exemple, en utilisant la signature SMB ou IPsec).  

3.  Installez le client en spécifiant la propriété de Client.msi **SMSSIGNCERT=***&lt;chemin_d’accès_complet_et_nom_de_fichier\>* avec CCMSetup.exe.  

###  <a name="a-namebkmkplanningforcrlsa-planning-for-pki-certificate-revocation"></a><a name="BKMK_PlanningForCRLs"></a> Planification de la révocation de certificats PKI  
Si vous utilisez des certificats PKI avec Configuration Manager, déterminez si les clients et serveurs doivent utiliser une liste de révocation des certificats (CRL) et, le cas échéant, de quelle manière, pour vérifier le certificat sur l’ordinateur connecté. La liste de révocation des certificats (CRL) est un fichier créé et signé par une autorité de certification et qui contient une liste des certificats qu'elle a émis, puis annulés. Les certificats peuvent être annulés par un administrateur d'une autorité de certification, par exemple, si un certificat émis est altéré ou suspecté de l'être.  

> [!IMPORTANT]  
>  L’emplacement de la liste de révocation des certificats est ajouté à un certificat au moment de son émission par une autorité de certification. Vous devez donc planifier la liste de révocation des certificats avant de déployer les certificats PKI utilisés par Configuration Manager.  

Par défaut, IIS vérifie toujours la liste de révocation des certificats pour les certificats clients. Ce paramètre de configuration n’est pas modifiable dans Configuration Manager. Par défaut, les clients Configuration Manager vérifient toujours la liste de révocation des certificats pour les systèmes de site. Toutefois, vous pouvez désactiver ce paramètre en spécifiant une propriété de site et une propriété CCMSetup. Lorsque vous gérez des ordinateurs Intel AMT hors bande, vous pouvez également activer la vérification de la liste de révocation des certificats pour le point de service hors bande et pour les ordinateurs qui exécutent la console de gestion hors bande.  

Si les ordinateurs utilisent la vérification de la révocation des certificats mais ne parviennent pas à localiser la liste de révocation des certificats, tous les certificats de la chaîne de certification sont considérés comme révoqués puisque leur absence de la liste ne peut pas être vérifiée. Dans ce scénario, toutes les connexions nécessitant des certificats et utilisant une liste de révocation des certificats échouent.  

Le fait de vérifier la liste de révocation des certificats chaque fois qu'un certificat est utilisé offre un niveau de sécurité supérieur par rapport à l'utilisation d'un certificat qui a été révoqué, mais ajoute un délai de connexion et de traitement sur le client. Vous êtes plus susceptible de demander cette vérification de sécurité supplémentaire lorsque les clients sont sur Internet ou sur un réseau non approuvé.  

Avec l’aide des administrateurs de votre infrastructure PKI, déterminez si les clients Configuration Manager doivent ou non vérifier la liste de révocation des certificats. Envisagez de laisser cette option activée dans Configuration Manager si les deux conditions suivantes sont réunies :  

-   Votre infrastructure PKI prend en charge une liste de révocation des certificats, et cette liste est publiée à un emplacement accessible par tous les clients Configuration Manager. N'oubliez pas que cela peut inclure des clients sur Internet si vous utilisez la gestion des clients basés sur Internet et les clients situés dans des forêts non approuvées.  

-   La nécessité de vérifier la liste de révocation des certificats pour chaque connexion sur un système de site configuré pour utiliser un certificat PKI est supérieure à la nécessité de disposer de connexions plus rapides et un traitement efficace sur le client, mais également supérieure au risque d'échec de connexion des clients sur les serveurs si la liste de révocation des certificats est introuvable.  

###  <a name="a-namebkmkplanningforrootcasa-planning-for-the-pki-trusted-root-certificates-and-the-certificate-issuers-list"></a><a name="BKMK_PlanningForRootCAs"></a> Planification des certificats racine approuvés PKI et de la liste des émetteurs de certificats  
Si vos systèmes de site IIS utilisent des certificats clients PKI pour l'authentification du client sur HTTP ou pour le chiffrement et l'authentification du client sur HTTPS, vous pouvez être amené à importer des certificats d'autorités de certification racine comme propriété de site. Les deux scénarios sont les suivants :  

-   Vous déployez des systèmes d’exploitation à l’aide de Configuration Manager, et les points de gestion acceptent uniquement les connexions de clients HTTPS.  

-   Vous utilisez des certificats clients PKI qui ne se lient pas à un certificat d'autorité de certification racine qui est approuvé par des points de gestion.  

    > [!NOTE]  
    >  Lorsque vous émettez des certificats PKI clients à partir de la même hiérarchie de certification racine que celle qui émet les certificats de serveurs que vous utilisez pour les points de gestion, il n'est pas nécessaire de spécifier ce certificat d'autorité de certification racine. Toutefois, si vous utilisez plusieurs hiérarchies d’autorité de certification et si vous n’êtes pas certain qu’elles s’approuvent mutuellement, importez l’autorité de certification racine pour la hiérarchie d’autorité de certification des clients.  

Si vous devez importer des certificats d’autorité de certification racine pour Configuration Manager, exportez-les de l’autorité de certification émettrice ou de l’ordinateur client. Si vous exportez le certificat à partir de l'autorité de certification émettrice, qui est également l'autorité de certification racine, assurez-vous que la clé privée n'est pas exportée. Stockez le fichier du certificat exporté dans un emplacement sécurisé pour empêcher toute falsification. Vous devez pouvoir accéder au fichier lorsque vous configurez le site, de sorte que si vous accédez au fichier sur le réseau, assurez-vous que la communication est protégée contre la falsification à l'aide de la signature SMB ou IPsec.  

Si l'un des certificats d'autorité de certification racine que vous importez est renouvelé, vous devez importer les certificats renouvelés.  

Ces certificats d’autorité de certification racine importés et le certificat d’autorité de certification racine de chaque point de gestion créent la liste des émetteurs de certificats que les ordinateurs Configuration Manager utilisent de la manière suivante :  

-   Quand un client se connecte à un point de gestion, le point de gestion vérifie que le certificat client est lié à un certificat racine approuvé dans la liste des émetteurs de certificats du site. Dans le cas contraire, le certificat est rejeté et la connexion PKI échoue.  

-   Lorsque des clients sélectionnent un certificat PKI, s'ils disposent d'une liste des émetteurs de certificats, ils sélectionnent un certificat lié à un certificat racine approuvé dans la liste des émetteurs de certificats. En cas d'absence de correspondance, le client ne sélectionne pas de certificat PKI. Pour plus d'informations sur le processus de certificat client, voir la section [Planning for PKI client certificate selection](#BKMK_PlanningForClientCertificateSelection) dans cette rubrique.  

Indépendamment de la configuration du site, vous pouvez également être amené à importer un certificat d'autorité de certification racine lorsque vous inscrivez des appareils mobiles ou des ordinateurs Mac, et lorsque vous configurez des ordinateurs Intel AMT pour des réseaux sans fil.  

###  <a name="a-namebkmkplanningforclientcertificateselectiona-planning-for-pki-client-certificate-selection"></a><a name="BKMK_PlanningForClientCertificateSelection"></a> Planning for PKI client certificate selection  
 Si vos systèmes de site IIS utilisent des certificats clients PKI pour l’authentification des clients sur HTTP ou pour le chiffrement et l’authentification des clients sur HTTPS, planifiez la manière dont les clients Windows vont sélectionner le certificat à utiliser pour Configuration Manager.  

> [!NOTE]  
>  Tous les appareils ne prennent pas en charge une méthode de sélection du certificat. Ils sélectionnent plutôt automatiquement le premier certificat qui répond à la configuration requise des certificats. Par exemple, les clients sur les ordinateurs Mac et les appareils mobiles ne prennent pas en charge une méthode de sélection du certificat.  

Dans de nombreux cas, la configuration par défaut et le comportement seront suffisants. Le client Configuration Manager sur les ordinateurs Windows filtre plusieurs certificats selon les critères suivants :  

1.  La liste des émetteurs de certificats : le certificat est lié à une autorité de certification racine qui est approuvée par le point de gestion.  

2.  Le certificat se trouve dans le magasin de certificats par défaut de **Personnel**.  

3.  Le certificat est valide, non révoqué, et n'a pas expiré. La vérification de la validité consiste à vérifier que la clé privée est accessible et que le certificat n’est pas créé à partir d’un modèle de certificat version 3, qui n’est pas compatible avec Configuration Manager.  

4.  Le certificat dispose d'une fonctionnalité d'authentification client ou il est émis vers le nom d'ordinateur.  

5.  Le certificat possède la plus longue période de validité.  

Les clients peuvent être configurés pour utiliser la liste des émetteurs de certificats selon les mécanismes suivants :  

-   La liste est publiée comme informations de site vers les services de domaine Active Directory.  

-   Les clients sont installés à l'aide de la poussée du client.  

-   Les clients la téléchargent à partir du point de gestion après qu'ils sont correctement affectés à leur site.  

-   Elle est spécifiée pendant l'installation du client, en tant que propriété client.msi CCMSetup de CCMCERTISSUERS.  

Si les clients ne disposent pas de la liste des émetteurs de certificats lors de leur installation initiale et s'ils ne sont pas encore affectés au site, ils ignorent cette étape. S'ils disposent de la liste des émetteurs de certificats et ne possèdent pas de certificat PKI lié à un certificat racine approuvé dans la liste des émetteurs de certificats la sélection du certificat échoue et les clients ne poursuivent pas avec les autres critères de sélection de certificat.  

Dans la plupart des cas, le client Configuration Manager identifie correctement un certificat PKI unique et approprié à utiliser. Dans le cas contraire, plutôt que de sélectionner le certificat à partir de la fonctionnalité d'authentification client, vous pouvez configurer deux autres méthodes de sélection :  

-   Une correspondance partielle des chaînes pour les valeurs Nom d'objet du certificat du client. Cette correspondance ne tient pas compte de la casse et convient parfaitement si vous utilisez le nom de domaine complet (FQDN) d’un ordinateur dans le champ Objet et souhaitez que la sélection du certificat soit basée sur le suffixe de domaine, par exemple **contoso.com**. Vous pouvez néanmoins utiliser cette méthode de sélection pour identifier une chaîne de caractères séquentiels dans le Nom d'objet du certificat qui différencie le certificat des autres dans le magasin de certificats du client.  

    > [!NOTE]  
    >  Vous ne pouvez pas utiliser la correspondance partielle des chaînes avec l'Autre nom de l'objet comme paramètre de site. Bien que vous puissiez spécifier une correspondance partielle des chaînes pour l'Autre nom de l'objet à l'aide de CCMSetup, il sera écrasé par les propriétés du site dans les scénarios suivants :  
    >   
    >  -   Les clients récupèrent les informations de site qui sont publiées dans les services de domaine Active Directory.  
    > -   Les clients sont installés à l'aide de la poussée du client.  
    >   
    >  Utilisez une correspondance partielle des chaînes dans l'Autre nom de l'objet uniquement lorsque vous installez des clients manuellement et lorsqu'ils ne récupèrent pas les informations de site à partir des services de domaine Active Directory. Par exemple, ces conditions s'appliquent aux clients qui utilisent Internet uniquement.  

-   Une correspondance pour les valeurs d'attribut Nom d'objet ou Autre nom de l'objet du certificat du client. Cette correspondance tient compte de la casse et convient parfaitement si vous utilisez un nom unique X500 ou des identificateurs d'objet équivalents (OID) conformément à la norme RFC 3280 et souhaitez que la sélection du certificat soit fondée sur les valeurs d'attribut. Vous pouvez spécifier uniquement les attributs et leurs valeurs s'ils doivent identifier de manière unique ou valider le certificat et le différencier des autres certificats du magasin de certificats.  

Le tableau suivant indique les valeurs d’attribut que Configuration Manager prend en charge pour les critères de sélection de certificat.  

|Attribut d'OID|Attribut de nom unique|Définition de l'attribut|  
|-------------------|----------------------------------|--------------------------|  
|0.9.2342.19200300.100.1.25|DC|Composant de domaine|  
|1.2.840.113549.1.9.1|E ou E-mail|Adresse de messagerie|  
|2.5.4.3|CN|Nom commun|  
|2.5.4.4|SN|Nom d'objet|  
|2.5.4.5|SERIALNUMBER|Numéro de série|  
|2.5.4.6|C|Code du pays|  
|2.5.4.7|L|Localité|  
|2.5.4.8|S ou ST|Nom de département/province|  
|2.5.4.9|STREET|Adresse|  
|2.5.4.10|O|Nom de l'organisation|  
|2.5.4.11|OU|Unité d'organisation|  
|2.5.4.12|T ou Title|Titre|  
|2.5.4.42|G ou GN ou GivenName|Prénom|  
|2.5.4.43|I ou Initials|Initiales|  
|2.5.29.17|(aucune valeur)|Autre nom de l'objet|  

Si plusieurs certificats appropriés sont détectés après application des critères de sélection, vous pouvez remplacer la configuration par défaut pour sélectionner le certificat dont la période de validité est la plus longue et spécifier au contraire qu'aucun certificat n'est sélectionné. Dans ce scénario, le client ne sera pas en mesure de communiquer avec les systèmes de site IIS à l'aide d'un certificat PKI. Le client transmet un message d'erreur au point d'état de secours qui lui est attribué pour vous prévenir de l'échec de sélection du certificat et vous permettre de modifier ou d'affiner vos critères de sélection de certificat. Le comportement du client dépend ensuite de l'emplacement de la connexion qui a échoué, à savoir sur HTTPS ou HTTP :  

-   Si la connexion qui a échoué était sur HTTPS : le client tente d’établir une connexion sur HTTP et utilise le certificat de client auto-signé.  

-   Si la connexion qui a échoué était sur HTTP : le client tente d’établir une autre connexion sur HTTP à l’aide du certificat de client auto-signé.  

Pour identifier facilement un certificat de client unique PKI, vous pouvez également spécifier un magasin personnalisé, autre que le magasin par défaut de **Personnel** dans l' **Ordinateur** . Toutefois, vous devez créer ce magasin indépendamment de Configuration Manager, mais aussi être en mesure de déployer des certificats dans ce magasin personnalisé et de les renouveler avant l’expiration de la période de validité.  

Pour plus d’informations sur la configuration des paramètres des certificats clients, consultez la section [Configurer les paramètres des certificats clients PKI](../../../core/plan-design/security/configure-security.md#BKMK_ConfigureClientPKI) dans la rubrique [Configurer la sécurité dans System Center Configuration Manager](../../../core/plan-design/security/configure-security.md).  

###  <a name="a-namebkmkplanningforpkitransitiona-planning-a-transition-strategy-for-pki-certificates-and-internet-based-client-management"></a><a name="BKMK_PlanningForPKITransition"></a> Planification d'une stratégie de transition pour les certificats PKI et la gestion des clients basés sur Internet  
Grâce aux options de configuration flexibles de Configuration Manager, vous pouvez effectuer progressivement la transition des clients et du site pour utiliser des certificats PKI et sécuriser ainsi davantage les points de terminaison des clients. Les certificats PKI fournissent une meilleure sécurité et permettent aux clients d'être gérés lorsqu'ils sont sur Internet.  

Les options et choix de configuration sont multiples dans Configuration Manager. Cela explique pourquoi il n’y a pas une méthode unique recommandée pour effectuer la transition d’un site afin que tous les clients utilisent des connexions HTTPS. Toutefois, vous pouvez suivre ces étapes comme guide :  

1.  Installez le site Configuration Manager et configurez-le de sorte que les systèmes de site acceptent les connexions client via HTTP et HTTPS.  

2.  Configurez l'onglet **Communication de l'ordinateur client** dans les propriétés du site, de sorte que les **Paramètres du système de site** soient **HTTP ou HTTPS**et cochez la case **Utiliser le certificat client PKI (fonctionnalité d'authentification client) si possible** . Configurez tous les autres paramètres dont vous avez besoin à partir de cet onglet. Pour plus d’informations, consultez la section [Configurer les paramètres des certificats clients PKI](../../../core/plan-design/security/configure-security.md#BKMK_ConfigureClientPKI) dans la rubrique [Configurer la sécurité dans System Center Configuration Manager](../../../core/plan-design/security/configure-security.md).  

3.  Pilotez un déploiement PKI pour les certificats clients. Pour obtenir un exemple de déploiement, consultez la section *Déploiement du certificat client sur les ordinateurs Windows* dans la rubrique [Exemple de déploiement pas à pas des certificats PKI pour System Center Configuration Manager : autorité de certification Windows Server 2008](/sccm/core/plan-design/network/example-deployment-of-pki-certificates).  

4.  Installez des clients à l'aide de la méthode d'installation poussée du client. Pour plus d’informations, consultez la section [Installer des clients Configuration Manager à l’aide de l’installation Push du client](../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientPush) dans la rubrique [Guide pratique pour déployer des clients sur des ordinateurs Windows dans System Center Configuration Manager](../../../core/clients/deploy/deploy-clients-to-windows-computers.md).  

5.  Surveillez le déploiement et l’état des clients à l’aide des rapports et des informations affichés dans la console Configuration Manager.  

6.  Déterminez combien de clients utilisent un certificat client PKI en affichant la colonne **Certificat client** dans l'espace de travail **Biens et conformité** , nœud **Appareils** .  

     Vous pouvez également déployer l’outil d’évaluation HTTPS Readiness (**cmHttpsReadiness.exe**) de Configuration Manager sur les ordinateurs et utiliser les rapports pour afficher le nombre d’ordinateurs susceptibles d’utiliser un certificat client PKI avec Configuration Manager.  

    > [!NOTE]  
    >  Quand le client Configuration Manager est installé sur des ordinateurs clients, l’outil **cmHttpsReadiness.exe** est installé dans le dossier *%windir%***\CCM**. Lorsque vous exécutez cet outil sur des clients, vous pouvez spécifier les options suivantes :  
    >   
    >  -   /Store:&lt;nom\>  
    > -   /Issuers:&lt;liste\>  
    > -   /Criteria:&lt;critères\>  
    > -   /SelectFirstCert  
    >   
    >  Ces options mappent aux propriétés Client.msi **CCMCERTSTORE**, **CCMCERTISSUERS**, **CCMCERTSEL**et **CCMFIRSTCERT** , respectivement. Pour plus d’informations sur ces options, consultez [À propos des propriétés d’installation du client dans System Center Configuration Manager](../../../core/clients/deploy/about-client-installation-properties.md).  

7.  Lorsque vous êtes certain qu'un nombre suffisant de clients utilisent avec succès leur certificat client PKI pour l'authentification sur HTTP, procédez comme suit :  

    1.  Déployez un certificat de serveur Web PKI sur un serveur de membre qui exécutera un point de gestion supplémentaire pour le site et configurez ce certificat dans IIS. Pour plus d’informations, consultez la section *Déploiement du certificat de serveur web pour les systèmes de site qui exécutent IIS* dans la rubrique [Exemple de déploiement pas à pas des certificats PKI pour System Center Configuration Manager : autorité de certification Windows Server 2008](/sccm/core/plan-design/network/example-deployment-of-pki-certificates).  

    2.  Installez le rôle de point de gestion sur ce serveur et configurez l'option **Connexions clients** dans les propriétés du point de gestion pour **HTTPS**.  

8.  Contrôlez et vérifiez que les clients qui possèdent un certificat PKI utilisent le nouveau point de gestion à l'aide du protocole HTTPS. Pour vérifier cela, vous pouvez utiliser le processus d'enregistrement du journal d'IIS ou les compteurs de performance.  

9. Reconfigurez d'autres rôles de système de site pour utiliser les connexions de clients HTTPS. Si vous souhaitez gérer des clients sur Internet, assurez-vous que les systèmes de site disposent d'un nom de domaine complet Internet et configurez des points de distribution et des points de gestion individuels pour accepter les connexions de clients à partir d'Internet.  

    > [!IMPORTANT]  
    >  Avant de configurer des rôles de système de site pour accepter les connexions à partir d'Internet, consultez les informations de planification et les conditions préalables pour la gestion des clients basés sur Internet. Pour plus d’informations, consultez [Communications entre points de terminaison dans System Center Configuration Manager](../../../core/plan-design/hierarchy/communications-between-endpoints.md).  

10. Déployez le certificat PKI pour les clients et les systèmes de site qui exécutent IIS et configurez les rôles de système de site pour les connexions de client HTTPS et les connexions Internet, au besoin.  

11. Pour une sécurité maximale : quand vous êtes certain que tous les clients utilisent un certificat client PKI pour l’authentification et le chiffrement, modifiez les propriétés de site pour utiliser HTTPS uniquement.  

 Lorsque vous suivez ce plan pour introduire progressivement des certificats PKI, tout d'abord pour l'authentification uniquement sur HTTP, puis pour l'authentification et le chiffrement sur HTTPS, vous réduisez le risque que les clients ne soient plus gérés. En outre, vous bénéficierez de la sécurité maximale prise en charge par Configuration Manager.  

##  <a name="a-namebkmkplanningforrtka-planning-for-the-trusted-root-key"></a><a name="BKMK_PlanningForRTK"></a> Planification de la clé racine approuvée  
La clé racine approuvée dans Configuration Manager est utilisée par les clients Configuration Manager pour vérifier que les systèmes de site appartiennent à leur hiérarchie. Chaque serveur de site génère une clé d'échange de site pour communiquer avec d'autres sites. La clé d'échange du site de niveau supérieur dans la hiérarchie est appelée clé racine approuvée.  

La clé racine approuvée dans Configuration Manager a un rôle similaire à un certificat racine dans une infrastructure à clé publique en ce sens que tout ce qui est signé par la clé privée de la clé racine approuvée est également approuvé dans le reste de la hiérarchie. Par exemple, en signant le certificat du point de gestion avec la paire clé privée/clé racine approuvée, et en effectuant une copie de la paire clé publique/clé racine approuvée qui leur est accessible, les clients peuvent distinguer les points de gestion qui se trouvent dans leur hiérarchie des points de gestion qui ne sont pas dans leur hiérarchie. Les clients utilisent WMI pour stocker une copie de la clé racine approuvée dans l'espace de noms **root\ccm\locationservices**.  

Les clients peuvent récupérer automatiquement la copie publique de la clé racine approuvée selon deux mécanismes :  

-   Le schéma Active Directory est étendu pour Configuration Manager, le site est publié dans les services de domaine Active Directory, et les clients peuvent récupérer ces informations de site à partir d’un serveur de catalogue global.  

-   Les clients sont installés à l'aide de la poussée du client.  

Si les clients ne peuvent pas récupérer la clé racine approuvée selon l'un de ces mécanismes, ils font confiance à la clé racine approuvée qui est fournie par le premier point de gestion avec lequel ils communiquent. Dans ce scénario, un client peut être redirigé vers le point de gestion d’un pirate informatique où il recevrait la stratégie à partir du point de gestion non autorisé. Cela ne peut être que l'œuvre d'un pirate chevronné et ne peut se produire qu'au cours d'une période limitée, avant que le client ne récupère la clé racine approuvée à partir d'un point de gestion valide. Toutefois, pour réduire le risque d'un acte de piraterie consistant à réacheminer les clients vers un point de gestion factice, mettez en service anticipé la clé racine approuvée sur les clients.  

Pour préconfigurer et vérifier la clé racine approuvée pour un client Configuration Manager, procédez comme suit :  

-   Mettez en service anticipé un client à l'aide de la clé racine approuvée avec un fichier.  

-   Mettez en service anticipé un client à l'aide de la clé racine approuvée sans utiliser un fichier.  

-   Vérifiez la clé racine approuvée sur un client.  

> [!NOTE]  
>  Il n'est pas nécessaire de mettre en service anticipé un client à l'aide de la clé racine approuvée s'il peut l'obtenir à partir des services de domaine Active Directory ou s'il est installé à l'aide la poussée du client. En outre, il n'est pas nécessaire de mettre en service anticipé des clients lorsqu'ils utilisent la communication HTTPS pour les points de gestion car l'approbation est établie à l'aide des certificats PKI.  

Vous pouvez supprimer la clé racine approuvée d'un client à l'aide de la propriété Client.msi **RESETKEYINFORMATION = TRUE** avec CCMSetup.exe. Pour remplacer la clé racine approuvée, réinstallez le client avec la nouvelle clé racine approuvée, par exemple en utilisant l'installation push du client ou en spécifiant la propriété Client.msi **SMSPublicRootKey** à l'aide de CCMSetup.exe.  

#### <a name="to-pre-provision-a-client-with-the-trusted-root-key-by-using-a-file"></a>Pour mettre en service anticipé un client avec la clé racine approuvée à l'aide d'un fichier  

1.  Dans un éditeur de texte, ouvrez le fichier *&lt;répertoire_Configuration_Manager\>***\bin\mobileclient.tcf**.  

2.  Recherchez l'entrée **SMSPublicRootKey=**, copiez la clé à partir de cette ligne et fermez le fichier sans effectuer aucune modification.  

3.  Créez un nouveau fichier texte et collez les informations de clé que vous avez copiées à partir du fichier mobileclient.tcf.  

4.  Enregistrez le fichier et placez-le à un endroit accessible par tous les ordinateurs, même s'il est sécurisé pour empêcher toute falsification.  

5.  Installez le client à l’aide d’une méthode d’installation qui accepte les propriétés de Client.msi. Spécifiez ensuite la propriété de Client.msi **SMSROOTKEYPATH=***&lt;chemin_complet_et_nom_de_fichier\>*.  

    > [!IMPORTANT]  
    >  Quand vous spécifiez la clé racine approuvée pour renforcer la sécurité lors de l’installation du client, vous devez également spécifier le code de site en utilisant la propriété de Client.msi **SMSSITECODE=&lt;code_site\>**.  

#### <a name="to-pre-provision-a-client-with-the-trusted-root-key-without-using-a-file"></a>Pour mettre en service anticipé un client avec la clé racine approuvée sans utiliser de fichier  

1.  Dans un éditeur de texte, ouvrez le fichier *&lt;répertoire_Configuration_Manager\>***\bin\mobileclient.tcf**.  

2.  Recherchez l'entrée SMSPublicRootKey=, notez la clé à partir de cette ligne ou copiez-la dans le Presse-papiers, puis fermez le fichier sans effectuer aucune modification.  

3.  Installez le client à l’aide d’une méthode d’installation qui accepte les propriétés de Client.msi. Spécifiez ensuite la propriété de Client.msi **SMSPublicRootKey=***&lt;clé\>*, où *&lt;clé\>* est la chaîne que vous avez copiée du fichier mobileclient.tcf.  

    > [!IMPORTANT]  
    >  Quand vous spécifiez la clé racine approuvée pour renforcer la sécurité lors de l’installation du client, vous devez également spécifier le code de site en utilisant la propriété de Client.msi **SMSSITECODE=&lt;code_site\>**  

#### <a name="to-verify-the-trusted-root-key-on-a-client"></a>Pour vérifier la clé racine approuvée sur un client  

1.  Dans le menu **Démarrer** , cliquez sur **Exécuter**, puis tapez **Wbemtest**.  

2.  Dans la boîte de dialogue **Testeur WMI** , cliquez sur **Connecter**.  

3.  Dans la boîte de dialogue **Connecter** , dans la zone **Espace de noms** , tapez **root\ccm\locationservices**, puis cliquez sur **Connecter**.  

4.  Dans la boîte de dialogue **Testeur WMI** dans la section **IWbemServices** , cliquez sur **Énumérer les Classes**.  

5.  Dans la boîte de dialogue **Informations de la superclasse** , sélectionnez **Récursive,**puis cliquez sur **OK**.  

6.  Dans la fenêtre **Résultats d’interrogation** , accédez à la fin de la liste, puis double-cliquez sur **TrustedRootKey ()**.  

7.  Dans la boîte de dialogue **Éditeur d'objets pour TrustedRootKey** , cliquez sur **Instances**.  

8.  Dans la nouvelle fenêtre **Résultats d’interrogation** qui affiche les instances de **TrustedRootKey**, double-cliquez sur **TrustedRootKey=@**  

9. Dans la boîte de dialogue **Éditeur d’objets pour TrustedRootKey=@**, dans la section **Propriétés**, accédez à **TrustedRootKey CIM_STRING**. La chaîne dans la colonne droite correspond à la clé racine approuvée. Vérifiez qu’elle correspond à la valeur **SMSPublicRootKey** dans le fichier *&lt;répertoire_Configuration_Manager\>***\bin\mobileclient.tcf**.  

##  <a name="a-namebkmkplanningforsigningencryptiona-planning-for-signing-and-encryption"></a><a name="BKMK_PlanningForSigningEncryption"></a> Planification de la signature et du chiffrement  
 Lorsque vous utilisez des certificats PKI pour toutes les communications client, vous n'avez pas à planifier la signature et le chiffrement pour contribuer à sécuriser les communications de données client. Toutefois, si vous configurez des systèmes de site qui exécutent IIS pour autoriser les connexions client HTTP, vous devez décider comment sécuriser la communication client pour le site.  

 Pour contribuer à protéger les données que les clients envoient aux points de gestion, vous pouvez exiger qu'elles soient signées. En outre, vous pouvez exiger que toutes les données signées provenant de clients qui utilisent le protocole HTTP soient signées à l'aide de l'algorithme SHA-256. Bien qu'il s'agisse d'un paramètre plus sécurisé, n'activez cette option que si tous les clients prennent en charge SHA-256. De nombreux systèmes d'exploitation offrent une prise en charge native de SHA-256, mais les systèmes d'exploitation plus anciens peuvent nécessiter une mise à jour ou un correctif logiciel. Par exemple, les ordinateurs qui exécutent Windows Server 2003 SP2 doivent installer un correctif qui est référencé dans [l'article 938397 de la Base de connaissances Microsoft](http://go.microsoft.com/fwlink/p/?LinkId=226666).  

 Bien que la signature contribue à protéger les données de la falsification, le chiffrement permet de protéger les données contre la divulgation d'informations. Vous pouvez activer le chiffrement 3DES pour les données d'inventaire et les messages d'état que les clients envoient aux points de gestion dans le site. Il n'est pas nécessaire d'installer des mises à jour sur des clients pour prendre en charge cette option, mais tenez compte de l'utilisation supplémentaire du processeur qui sera requise sur les clients et le point de gestion pour procéder au chiffrement et au déchiffrement.  

 Pour plus d’informations sur la configuration des paramètres de signature et de chiffrement, consultez la section [Configurer la signature et le chiffrement](../../../core/plan-design/security/configure-security.md#BKMK_ConfigureSigningEncryption) dans la rubrique [Configurer la sécurité dans System Center Configuration Manager](../../../core/plan-design/security/configure-security.md).  

##  <a name="a-namebkmkplanningforrbaa-planning-for-role-based-administration"></a><a name="BKMK_PlanningForRBA"></a> Planification de l’administration basée sur des rôles  
 Pour plus d’informations, consultez [Principes de base de l’administration basée sur des rôles pour System Center Configuration Manager](../../../core/understand/fundamentals-of-role-based-administration.md).  



<!--HONumber=Nov16_HO1-->


