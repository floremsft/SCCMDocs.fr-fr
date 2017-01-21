---
title: "Sécurité et confidentialité de la gestion du contenu | System Center Configuration Manager"
description: "Optimisez la sécurité et la confidentialité pour la gestion du contenu dans System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5f38b726-dc00-433a-ba05-5b7dbb0d8e99
caps.latest.revision: 8
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: fcc3c74e50a4cdac9337178f5fcfe710f0fa17a5


---
# <a name="security-and-privacy-for-content-management-for-system-center-configuration-manager"></a>Sécurité et confidentialité pour la gestion du contenu dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Cette rubrique contient des informations de sécurité et de confidentialité pour la gestion du contenu dans System Center Configuration Manager. Lisez-le conjointement aux rubriques suivantes :  

-   [Sécurité et confidentialité pour la gestion des applications dans System Center Configuration Manager](../../../apps/plan-design/security-and-privacy-for-application-management.md)  

-   [Sécurité et confidentialité pour les mises à jour logicielles dans System Center Configuration Manager](/sccm/sum/plan-design/security-and-privacy-for-software-updates)  

-   [Sécurité et confidentialité du déploiement de systèmes d’exploitation dans System Center Configuration Manager](../../../osd/plan-design/security-and-privacy-for-operating-system-deployment.md)  

##  <a name="a-namebkmksecuritycontentmanagementa-security-best-practices-for-content-management"></a><a name="BKMK_Security_ContentManagement"></a> Meilleures pratiques de sécurité pour la gestion de contenu  
 Utilisez les meilleures pratiques de sécurité suivantes pour la gestion de contenu :  

 **Pour les points de distribution sur intranet, prenez en considération les avantages et les inconvénients liés à l’utilisation de HTTP et HTTPS** : dans la plupart des cas, l’utilisation du protocole HTTP et des comptes d’accès aux packages pour l’autorisation est plus sûre que l’utilisation du protocole HTTPS avec chiffrement, mais sans autorisation. Toutefois, si des données sensibles se trouvent dans votre contenu que vous souhaitez chiffrer lors du transfert, utilisez le protocole HTTPS.  

-   **Quand vous utilisez HTTPS pour un point de distribution**, Configuration Manager n’utilise pas les comptes d’accès aux packages pour autoriser l’accès au contenu, mais le contenu est chiffré pendant son transfert sur le réseau.  

-   **Quand vous utilisez HTTP pour un point de distribution**, vous pouvez utiliser des comptes d’accès aux packages pour l’autorisation, mais le contenu n’est pas chiffré pendant son transfert sur le réseau.  


**Si vous utilisez un certificat d’authentification de client PKI plutôt qu’un certificat auto-signé pour le point de distribution, protégez le fichier de certificat (.pfx) avec un mot de passe fort. Si vous stockez le fichier sur le réseau, sécurisez le canal du réseau quand vous importez le fichier dans Configuration Manager** - Quand vous avez besoin d’un mot de passe pour importer le certificat d’authentification du client permettant au point de distribution de communiquer avec les points de gestion, vous pouvez de cette façon protéger le certificat contre les utilisateurs malveillants. Utilisez la signature SMB ou IPsec entre l'emplacement réseau et le serveur de site pour empêcher un intrus de falsifier le fichier de certificat.  

**Supprimez le rôle de point de distribution du serveur de site** - Par défaut, un point de distribution est installé sur le même serveur que le serveur de site. Les clients n'ont pas besoin de communiquer directement avec le serveur de site, ainsi, pour réduire la surface d'attaque, attribuez le rôle de point de distribution à d'autres systèmes de site et retirez-le du serveur de site.  

**Sécurisez le contenu au niveau de l’accès aux packages** - Le partage de point de distribution autorise un accès en lecture à tous les utilisateurs. Pour restreindre les utilisateurs pouvant accéder au contenu, utilisez les comptes d'accès aux packages lorsque le point de distribution est configuré pour le protocole HTTP. Cette consigne ne s’applique pas aux points de distribution cloud, qui ne prennent pas en charge les comptes d’accès aux packages. Pour plus d’informations sur le compte d’accès aux packages, consultez [Gérer les comptes pour accéder au contenu](../../../core/plan-design/hierarchy/manage-accounts-to-access-content.md).


**Si Configuration Manager installe IIS au moment où vous ajoutez un rôle de système de site de point de distribution, désactivez la redirection HTTP et les scripts et outils de gestion IIS à l’issue de l’installation du point de distribution** - Le point de distribution n’a pas besoin de la redirection HTTP ni des scripts et outils de gestion IIS. Pour réduire la surface d'attaque, supprimez ces services de rôle pour le rôle de serveur Web (IIS).  Pour plus d'informations sur les services de rôle pour le rôle de serveur web (IIS) pour les points de distribution, voir [Prérequis des sites et systèmes de site](/sccm/core/plan-design/configs/site-and-site-system-prerequisites).  

**Définissez les autorisations d’accès au package au moment de sa création** - Sachant que les modifications apportées aux comptes d’accès dans les fichiers de package ne deviennent effectives qu’à partir du moment où vous redistribuez le package, définissez les autorisations d’accès au package avec précaution au moment où vous créez le package. Cela est particulièrement important lorsque le package est volumineux ou distribués à de nombreux points de distribution, et lorsque la capacité de la bande passante réseau pour la distribution de contenu est limitée.  

**Implémentez des contrôles d’accès pour protéger le média qui contient le contenu préparé** - Le contenu préparé est compressé mais pas chiffré. Une personne malveillante pourrait alors lire et modifier les fichiers qui sont téléchargés vers des appareils. Les clients Configuration Manager rejetteront le contenu qui a été falsifié, mais ils le téléchargeront malgré tout.  

**Importez le contenu préparé en utilisant uniquement l’outil en ligne de commande ExtractContent (ExtractContent.exe) intégré à Configuration Manager et vérifiez qu’il est signé par Microsoft** - Pour éviter une falsification et une élévation de privilèges, utilisez uniquement l’outil en ligne de commande autorisé intégré à Configuration Manager.  

**Sécurisez le canal de communication entre le serveur de site et l’emplacement source du package** - Utilisez une signature IPsec ou SMB entre le serveur de site et l’emplacement source du package au moment où vous créez des applications et des packages. Cela permet d'empêcher un individu mal intentionné de falsifier les fichiers sources.  

**Si vous modifiez l’option de configuration du site pour utiliser un site web personnalisé plutôt que le site web par défaut après l’installation de rôles de point de distribution, supprimez les répertoires virtuels par défaut** - Quand vous choisissez d’utiliser un site web personnalisé à la place du site web par défaut, Configuration Manager ne supprime pas les anciens répertoires virtuels. Supprimez les répertoires virtuels que Configuration Manager a créés initialement sous le site web par défaut :  

-   SMS_DP_SMSPKG$  

-   SMS_DP_SMSSIG$  

-   NOCERT_SMS_DP_SMSPKG$  

-   NOCERT_SMS_DP_SMSSIG$  

**Pour les points de distribution cloud, protégez vos informations d’abonnement et vos certificats** - Quand vous utilisez des points de distribution cloud, protégez les éléments importants, notamment le nom d’utilisateur et le mot de passe de votre abonnement Azure, le certificat de gestion Azure et le certificat de service de point de distribution cloud. Stockez les certificats en lieu sûr. Si vous y accédez via le réseau lors de la configuration du point de distribution cloud, utilisez une authentification IPsec ou SMB entre le serveur de système de site et l'emplacement source.  

**Pour assurer la continuité de service des points de distribution cloud, surveillez la date d’expiration des certificats** - Configuration Manager ne vous avertit pas lorsque les certificats importés pour la gestion du service du point de distribution cloud sont sur le point d’expirer. Vous devez donc surveiller les dates d'expiration indépendamment de Configuration Manager et penser à renouveler puis à importer le nouveau certificat avant la date d'expiration. Cette opération est particulièrement importante si vous faites l'acquisition d'un certificat de service de point de distribution cloud Configuration Manager auprès d'une autorité de certification externe, car l'obtention d'un certificat renouvelé peut prendre plus de temps.  

 En cas d'expiration d'un certificat, le **Gestionnaire de services cloud** génère l'ID de message d'état **9425** . Une entrée contenant la date d'expiration exprimée au format UTC est alors ajoutée au fichier **CloudMgr.log** , pour indiquer que le certificat a expiré ( **is in expired state**).  

## <a name="security-considerations-for-content-management"></a>Considérations de sécurité pour la gestion de contenu  
Tenez compte des points suivant au moment de planifier la gestion de contenu :  

-   Les clients ne valident pas le contenu jusqu'au téléchargement de celui-ci  

     Les clients Configuration Manager ne valident le hachage du contenu qu'après le téléchargement de celui-ci dans leur cache client. Si un individu mal intentionné falsifie la liste des fichiers à télécharger ou le contenu lui-même, le processus de téléchargement peut consommer une quantité importante de bande passante réseau pour que le client supprime ensuite le contenu lorsqu'il rencontre le hachage invalide.  

-   Quand vous utilisez des points de distribution cloud, l’accès au contenu est automatiquement limité à votre entreprise et vous ne pouvez pas le limiter de façon plus précise en sélectionnant des utilisateurs ou des groupes.  

-   Quand vous utilisez des points de distribution cloud, les clients sont authentifiés par le point de gestion, puis ils utilisent un jeton Configuration Manager pour accéder aux points de distribution cloud. Le jeton est valable pendant huit heures. Par conséquent, si vous bloquez un client parce qu'il n'est plus approuvé, il peut continuer à télécharger du contenu à partir d'un point de distribution cloud, jusqu'à la fin de la période de validité du jeton. À ce stade, le point de gestion n'émettra pas d'autre jeton pour le client, puisque celui-ci aura été bloqué.  

     Pour empêcher un client bloqué de télécharger du contenu pendant cette période de huit heures, vous pouvez arrêter le service cloud à partir du nœud **Cloud**, **Configuration de la hiérarchie**, dans l'espace de travail **Administration** de la console Configuration Manager.  

##  <a name="a-namebkmkprivacycontentmanagementa-privacy-information-for-content-management"></a><a name="BKMK_Privacy_ContentManagement"></a> Informations de confidentialité pour la gestion de contenu  
 Configuration Manager n'inclut pas de données utilisateur dans les fichiers de contenu, même si un utilisateur administratif peut choisir d'en ajouter.  

 Avant de configurer la gestion de contenu, pensez à vos besoins en matière de confidentialité.  



<!--HONumber=Nov16_HO1-->


