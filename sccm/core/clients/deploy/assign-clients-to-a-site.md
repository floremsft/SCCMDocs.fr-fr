---
title: "Affecter des clients à un site | System Center Configuration Manager"
description: "Affecter des clients à un site dans System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: ba9b623f-6e86-4006-93f2-83d563de0cd0
caps.latest.revision: 10
author: Mtillman
ms.author: mtillman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 3540b178bf8d7c6473b94a7300578ed7cf0dce29

---
# <a name="how-to-assign-clients-to-a-site-in-system-center-configuration-manager"></a>Comment affecter des clients à un site dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Une fois un client System Center Configuration Manager installé, il doit rejoindre un site principal Configuration Manager avant de pouvoir être géré. Le site qu'un client a rejoint est le site auquel il est attribué. Les clients ne peuvent pas être attribués à un site d'administration centrale ou à un site secondaire.  

 Le processus d'attribution se produit une fois le client correctement installé et détermine quel site gérera l'ordinateur client. Lorsque vous installez le client d'appareil mobile lors de l'inscription de Configuration Manager, ce processus attribue automatiquement l'appareil mobile à un site. Lorsque vous installez le client sur un ordinateur, vous pouvez également attribuer le client à un site ou choisir uniquement de l'installer sans l'attribuer à un site. Toutefois, lorsque le client est installé mais pas attribué, client n'est pas géré tant que l'attribution de site n'a pas été menée à bien.  

 Pour attribuer un ordinateur client, vous avez le choix entre une attribution directe à un site et une attribution automatique de site. Dans ce cas, le client trouve automatiquement un site approprié, en fonction de son emplacement réseau actuel, ou un site de secours qui a été configuré pour la hiérarchie.  

> [!NOTE]  
>  Attribuez toujours des clients à des sites utilisant la même version de Configuration Manager. Évitez d’attribuer un client Configuration Manager d’une version plus récente à un site d’une version antérieure.   Si nécessaire, mettez à jour le site principal vers la version de Configuration Manager que vous utilisez pour les clients.  

 Une fois le client attribué à un site, il y reste associé même dans les cas où il modifie son adresse IP ou se déplace vers un autre site. Seul un administrateur peut, par la suite, attribuer manuellement le client à un autre site ou supprimer l'attribution du client.  

> [!WARNING]  
>  Le client ne reste pas attribué à un site si vous attribuez ce client sur un appareil Windows Embedded et que les filtres d'écriture sont activés, ce qui constitue une exception. Si vous ne désactivez pas les filtres d'écriture avant d'attribuer le client, celui-ci retrouve son état d'attribution de site initial au prochain redémarrage de l’appareil.  
>   
>  Par exemple, si le client est configuré pour l'attribution automatique de site, il fera l'objet d'une réattribution au démarrage et pourra être attribué à un site différent. Si le client n'est pas configuré pour l'attribution automatique de site, mais qu'il nécessite une attribution de site manuelle, vous devez le réattribuer manuellement après le démarrage pour pouvoir le gérer à nouveau à l'aide de Configuration Manager.  
>   
>  Pour éviter ce comportement, désactivez les filtres d'écriture avant d'attribuer le client sur des appareils embarqués, puis activez-les après avoir vérifié que l'attribution de site a abouti.  

 Si le client ne peut pas être attribué à un site, le logiciel client reste installé, mais ne sera pas géré. Un client est considéré non géré lorsqu'il est installé mais pas attribué à un site ou lorsqu'il est attribué à un site, mais ne peut pas communiquer avec un point de gestion.  

##  <a name="a-namebkmkmanualassignmenta-using-manual-site-assignment-for-computers"></a><a name="BKMK_ManualAssignment"></a> Utilisation de l'attribution manuelle de site pour les ordinateurs  
 Vous pouvez attribuer des ordinateurs clients à un site manuellement en employant l'une des deux méthodes suivantes :  

-   Utilisez une propriété d'installation du client qui spécifie le code de site.  

-   Dans le panneau de configuration, dans **Configuration Manager**, indiquez le code de site.  

> [!NOTE]  
>  Si vous attribuez manuellement un ordinateur client à un code de site Configuration Manager qui n'existe pas, l'attribution de site échoue. Le client reste installé, mais non géré tant qu'il n'est pas attribué à un site Configuration Manager valide.  

##  <a name="a-namebkmkautomaticassignmenta-using-automatic-site-assignment-for-computers"></a><a name="BKMK_AutomaticAssignment"></a> Utilisation de l'attribution automatique de site pour les ordinateurs  
 L'attribution automatique de site peut se produire lors du déploiement du client ou lorsque vous cliquez sur **Rechercher un site** sous l'onglet **Avancé** des **Propriétés du Configuration Manager** dans le panneau de configuration. Le client Configuration Manager compare son propre emplacement réseau avec les limites qui sont configurées dans la hiérarchie Configuration Manager. Lorsque l'emplacement réseau du client se situe dans un groupe de limites qui est activé pour l'attribution de site ou lorsque la hiérarchie est configurée pour un site de secours, le client est automatiquement affecté à ce site sans que vous deviez spécifier un code de site.  

 Vous pouvez configurer des limites à l'aide de l'un ou de plusieurs des éléments suivants :  

-   Sous-réseau IP  

-   Site Active Directory  

-   Préfixe IP v6  

-   Plage d'adresses IP  

> [!NOTE]  
>  Si un client Configuration Manager possède plusieurs cartes réseau (éventuellement une carte réseau LAN et un modem d'accès à distance) et donc plusieurs adresses IP, l'adresse IP utilisée pour évaluer l'attribution de site client n'est pas déterminante.  

 Pour plus d’informations sur la configuration de groupes de limites pour l’attribution de site et sur la configuration d’un site de secours pour l’attribution automatique de site, consultez [Define site boundaries and boundary groups for System Center Configuration Manager](../../../core/servers/deploy/configure/define-site-boundaries-and-boundary-groups.md).  

 Les clients Configuration Manager qui utilisent l'attribution automatique de site tentent de trouver les groupes de limites qui sont publiés dans les services de domaine Active Directory. Si cette méthode échoue (par exemple, si le schéma Active Directory n'est pas étendu pour Configuration Manager, ou si les clients sont des ordinateurs de groupes de travail), les clients peuvent trouver les informations sur les groupes de limites à partir d'un point de gestion.  

 Vous pouvez spécifier un point de gestion pour les ordinateurs clients lorsqu'ils sont installés, ou les clients peuvent localiser un point de gestion à l'aide de la publication DNS ou WINS.  

 Si le client ne trouve pas de site associé à un groupe de limites qui contient son emplacement réseau et que la hiérarchie ne dispose pas d'un site de secours, le client essaie de nouveau toutes les 10 minutes jusqu'à ce qu'il puisse être attribué à un site.  

 Les ordinateurs clients Configuration Manager ne peuvent pas être attribués automatiquement à un site si l'un des scénarios suivants s'applique et doivent être attribués manuellement :  

-   Ils sont actuellement attribués à un site.  

-   Ils se trouvent sur Internet ou sont configurés comme des clients Internet uniquement.  

-   Leur emplacement réseau ne tombe pas dans l'un des groupes de limites configurés dans la hiérarchie de Configuration Manager et il n'existe aucun site de secours pour la hiérarchie.  

##  <a name="a-namebkmksitecompatibilitya-completing-site-assignment-by-checking-site-compatibility"></a><a name="BKMK_SiteCompatibility"></a> Fin de l'attribution de site par la vérification de la compatibilité du site  
 Dès lors qu'un client a trouvé le site auquel il est attribué, la version et le système d'exploitation du client sont vérifiés pour s'assurer qu'un site Configuration Manager peut le gérer. Par exemple, Configuration Manager ne peut pas gérer les clients Configuration Manager 2007, System Center 2012 Configuration Manager ou les clients qui exécutent Windows 2000.  

 Si vous attribuez un client exécutant Windows 2000 à un site Configuration Manager, l’attribution de site échoue. En revanche, si vous attribuez un client Configuration Manager 2007 ou un client Configuration Manager 2012 à un site Configuration Manager (Current Branch), l’attribution de site parvient à prendre en charge la mise à niveau automatique du client. Toutefois, tant qu’un client de génération antérieure n’est pas mis à niveau vers un client Configuration Manager (Current Branch), Configuration Manager ne peut pas gérer ce client en utilisant des paramètres, applications ou mises à jour logicielles du client.  

> [!NOTE]  
>  Pour prendre en charge l’attribution de site d’un site Configuration Manager 2007 ou d’un client System Center 2012 Configuration Manager à un site Configuration Manager (Current Branch), vous devez configurer la mise à niveau automatique des clients pour la hiérarchie. Pour plus d’informations, consultez [Comment mettre à niveau les clients pour les ordinateurs Windows dans System Center Configuration Manager](../../../core/clients/manage/upgrade/upgrade-clients-for-windows-computers.md).  

 Configuration Manager vérifie également que vous avez attribué le client Configuration Manager (Current Branch) à un site qui le prend en charge. Les scénarios suivants peuvent se produire durant une migration à partir de versions précédentes de Configuration Manager.  

-   Scénario : Vous avez utilisé une attribution automatique de site et vos limites chevauchent celles définies dans une version précédente de Configuration Manager.  

     Dans ce cas, le client essaie automatiquement de trouver un site Configuration Manager (Current Branch).  

     Le client vérifie d’abord les services de domaine Active Directory et, s’il trouve un site Configuration Manager (Current Branch) publié, l’attribution de site réussit. Si l’opération échoue (par exemple si le site Configuration Manager (Current Branch) n’est pas publié ou si l’ordinateur est un client de groupe de travail), le client recherche les informations de site sur le point de gestion qui lui est attribué.  

    > [!NOTE]  
    >  Vous pouvez attribuer un point de gestion au client lors de l’installation de celui-ci en utilisant la propriété Client.msi **SMSMP=&lt;nom_serveur**.  

     Si ces deux méthodes échouent, l'attribution de site échoue et vous devez attribuer le client manuellement.  

-   Scénario : Vous avez attribué le client Configuration Manager (Current Branch) en utilisant un code de site spécifique au lieu d’utiliser l’attribution automatique de site, et spécifié par erreur un code de site pour une version de Configuration Manager antérieure à System Center 2012 R2 Configuration Manager.  

     Dans ce cas, l’attribution de site échoue et vous devez réattribuer manuellement le client à un site Configuration Manager (Current Branch).  

 La vérification de la compatibilité du site requiert l'une des conditions suivantes :  

-   Le client peut accéder aux informations de site publiées dans les services de domaine Active Directory.  

-   Le client peut communiquer avec un point de gestion du site.  

 Si la vérification de la compatibilité du site échoue avant la fin de l'opération, l'attribution de site échoue et le client reste non géré, jusqu'à ce que la vérification de la compatibilité du site soit terminée sans problème lors de l'exécution suivante.  

 La seule exception à cette vérification de la compatibilité du site survient lorsqu'un client est configuré pour un point de gestion Internet. Dans ce scénario, aucune vérification de la compatibilité du site n'est effectuée. Si vous attribuez des clients à un site qui contient des systèmes de site Internet et que vous spécifiez un point de gestion Internet, assurez-vous d'attribuer le client au site approprié. Si vous attribuez le client à un site Configuration Manager 2007, un site System Center 2012 Configuration Manager ou un site Configuration Manager qui n’a pas de rôle de système de site basé sur Internet, le client n’est pas géré.  

##  <a name="a-namebkmklocatingmpsa-locating-management-points"></a><a name="BKMK_LocatingMPs"></a> Localisation de points de gestion  
 Une fois qu'un client est correctement attribué à un site, il localise un point de gestion dans le site.  

 Les ordinateurs clients téléchargent la liste des points de gestion du site auxquels ils peuvent se connecter. Ce processus intervient à chaque redémarrage du client, c'est-à-dire toutes les 25 heures, et lorsque le client détecte un changement sur le réseau (par exemple, déconnexion et reconnexion de l'ordinateur sur le réseau ou attribution d'une nouvelle adresse IP). La liste répertorie les points de gestion présents sur l'intranet et indique s'ils acceptent les connexions client via HTTP ou HTTPS. Lorsque l'ordinateur client est sur Internet et qu'il ne dispose pas encore d'une liste de points de gestion, il se connecte au point de gestion Internet spécifié pour obtenir une liste de points de gestion. Lorsque le client dispose d'une liste de points de gestion pour son site attribué, il en sélectionne un auquel se connecter :  

-   Lorsque le client se trouve sur l'intranet et qu'il possède un certificat PKI valide qu'il peut utiliser, il choisit les points de gestion HTTPS avant les points de gestion HTTP. Il localise ensuite le point de gestion le plus proche, en fonction de son appartenance à une forêt.  

-   Lorsque le client se trouve sur Internet, il choisit de façon non déterminante l'un des points de gestion basés sur Internet.  

 Les clients d'appareil mobile inscrits par Configuration Manager se connectent à un seul point de gestion du site auquel ils sont attribués et ne se connectent jamais aux points de gestion de sites secondaires. Ces clients se connectent toujours via HTTPS et le point de gestion doit être configuré pour accepter les connexions client sur Internet. Lorsque le site principal propose plusieurs points de gestion pour les clients d'appareil mobile, Configuration Manager en choisit un sans déterminisme pendant l'attribution et le client d'appareil mobile continue d'utiliser le même point de gestion.  

 Une fois que le client a téléchargé la stratégie du client depuis un point de gestion du site, il devient un client géré.  

##  <a name="a-namebkmkdownloadsitesettingsa-downloading-site-settings"></a><a name="BKMK_DownloadSiteSettings"></a> Téléchargement des paramètres du site  
 Une fois que le site est attribué et que le client a trouvé un point de gestion, un ordinateur client utilisant les services de domaine Active Directory pour la vérification de sa compatibilité avec le site télécharge les paramètres client du site auquel il est attribué. Ces paramètres incluent les critères de sélection de certificat du client, s'il faut utiliser une liste de révocation de certificat et les numéros de port de demande de client. Le client continue de vérifier régulièrement ces paramètres.  

 Lorsque les ordinateurs clients ne peuvent pas obtenir les paramètres du site auprès des services de domaine Active Directory, ils les téléchargent à partir de leur point de gestion. Les ordinateurs clients peuvent également obtenir les paramètres du site lorsqu'ils sont installés à l'aide de l'installation poussée du client ou que vous les spécifiez manuellement à l'aide de CCMSetup.exe et des propriétés d'installation du client. Pour plus d’informations sur les propriétés d’installation du client, consultez [À propos des propriétés d’installation du client dans System Center Configuration Manager](../../../core/clients/deploy/about-client-installation-properties.md).  

##  <a name="a-namebkmkdownloadclientsettingsa-downloading-client-settings"></a><a name="BKMK_DownloadClientSettings"></a> Téléchargement des paramètres du client  
 Tous les clients téléchargent la stratégie de paramètres client par défaut, ainsi que toute stratégie de paramètres client personnalisée. Le Centre logiciel repose sur ces stratégies de configuration du client pour les ordinateurs Windows et informe les utilisateurs que le Centre logiciel ne peut pas fonctionner correctement tant que ces informations de configuration ne sont pas téléchargées. En fonction des paramètres client configurés, le téléchargement initial des paramètres client peut prendre un certain temps et certaines tâches de gestion risquent de ne pas s'exécuter tant que ce processus n'est pas terminé.  

##  <a name="a-namebkmkverifyassignmenta-verifying-site-assignment"></a><a name="BKMK_VerifyAssignment"></a> Vérification de l'attribution de site  
 Vous pouvez vérifier que l'attribution de site a abouti en employant l'une des méthodes suivantes :  

-   Pour les clients sur ordinateurs Windows, utilisez Configuration Manager dans le Panneau de configuration et vérifiez que le code de site est correctement affiché sous l'onglet **Site**.  

-   Pour les ordinateurs clients, dans l'espace de travail **Ressources et compatibilité** , utilisez le nœud **Périphériques** pour vérifier que l'ordinateur affiche **Oui** pour la colonne **Client** et le code de site principal correct pour la colonne **Code de site** .  

-   Pour les clients d'appareil mobile, dans l'espace de travail **Ressources et compatibilité** , utilisez le nœud **Tous les périphériques mobiles** pour vérifier que l'appareil mobile affiche **Oui** pour la colonne **Client** et le code de site principal correct pour la colonne **Code de site** .  

-   Utilisez les rapports pour l'attribution de client et l'inscription d'appareil mobile.  

-   Pour les ordinateurs clients, utilisez le fichier LocationServices.log sur le client.  

##  <a name="a-namebkmkroaminga-roaming-to-other-sites"></a><a name="BKMK_Roaming"></a> Itinérance vers d'autres sites  
 Lorsque des ordinateurs clients de l'intranet sont attribués à un site principal, mais que leur emplacement réseau change au profit d'un groupe de limites configuré pour un autre site, ils ont été déplacés vers un autre site (itinérance). Lorsque ce site est un site secondaire du site auquel ils sont attribués, les clients peuvent utiliser un point de gestion du site secondaire pour télécharger la stratégie client et les données client, ce qui évite l'envoi de ces données via un réseau potentiellement lent. Toutefois, si ces clients itinérants sont déplacés dans les limites d'un autre site principal ou d'un site secondaire qui n'est pas un site enfant du site auquel ils sont attribués, ces clients utilisent toujours un point de gestion du site auquel ils sont attribués pour télécharger la stratégie client et les données vers leur site.  

 Ces ordinateurs clients itinérants qui sont déplacés vers d'autres sites (tous les sites principaux et tous les sites secondaires) peuvent toujours utiliser les points de gestion d'autres sites pour les demandes d'emplacement du contenu. Les points de gestion du site actuel peuvent fournir aux clients une liste des points de distribution qui disposent du contenu demandé par les clients.  

 Pour les ordinateurs clients configurés pour être gérés via Internet uniquement et pour les ordinateurs Mac et les appareils mobiles inscrits par Configuration Manager, ces clients communiquent uniquement avec les points de gestion du site auxquels ils sont attribués. Ces clients ne communiquent jamais avec les points de gestion de sites secondaires ou d'autres sites principaux.  



<!--HONumber=Nov16_HO1-->


