---
title: "Sélectionner des méthodes de découverte | Microsoft Docs"
description: "Passez en revue les considérations relatives aux méthodes à utiliser et aux sites sur lesquels les exécuter."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 127ce713-d085-430f-ac7b-2701637fe126
caps.latest.revision: 9
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 10b1010ccbf3889c58c55b87e70b354559243c90
ms.openlocfilehash: 54beff9bc8624d67efda7393db6334ebc96937d7

---
# <a name="select-discovery-methods-to-use-for-system-center-configuration-manager"></a>Sélectionner des méthodes de découverte à utiliser pour System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Pour utiliser correctement et efficacement la découverte pour System Center Configuration Manager, vous devez prendre en compte les méthodes à utiliser et les sites sur lesquels les exécuter.  

 La découverte peut générer un volume de trafic réseau considérable, et les enregistrements de données de découverte obtenus peuvent entraîner la consommation extensive des ressources du processeur pendant le traitement. Vous devez donc limiter l’utilisation des méthodes de découverte à celles qui sont nécessaires pour répondre à vos objectifs. Vous pouvez commencer par n’utiliser qu’une ou deux méthodes de découverte, avant d’éventuellement en activer d’autres de manière contrôlée par la suite pour étendre le niveau de découverte dans votre environnement. Les informations fournies dans cette rubrique peuvent vous aider à prendre des décisions éclairées.  

 Pour plus d’informations sur les différentes méthodes de découverte, consultez [À propos des méthodes de découverte pour System Center Configuration Manager](../../../../core/servers/deploy/configure/about-discovery-methods.md).  

## <a name="select-methods-to-discover-different-things"></a>Sélectionner des méthodes pour découvrir des choses différentes  
 Pour découvrir des ordinateurs clients Configuration Manager potentiels ou des ressources utilisateur, vous devez activer les méthodes de découverte appropriées. Vous pouvez utiliser différentes combinaisons de méthodes de découverte pour localiser différentes ressources et découvrir des informations supplémentaires sur ces ressources. Les méthodes employées déterminent le type de ressources découvertes, ainsi que les services et agents Configuration Manager utilisés dans le processus de découverte. Elles déterminent également le type d'informations concernant les ressources que vous pouvez découvrir.  

 **Découverte d’ordinateurs**   
Quand vous voulez découvrir des ordinateurs, vous pouvez utiliser la découverte de systèmes Active Directory ou la découverte du réseau.  

 Par exemple, si vous souhaitez découvrir des ressources qui peuvent installer le client Configuration Manager avant d’utiliser l’installation poussée du client, vous pouvez exécuter la découverte de systèmes Active Directory. Alternativement, vous pouvez exécuter la découverte du réseau et utiliser ses options pour découvrir le système d'exploitation des ressources (requis pour utiliser l'installation poussée du client plus tard). Toutefois, en utilisant la découverte de systèmes Active Directory, non seulement vous découvrez la ressource, mais aussi des informations de base et pouvez découvrir des informations étendues à partir des services de domaine Active Directory. Ces informations peuvent être utiles pour créer des requêtes et des regroupements complexes à utiliser dans l'attribution de paramètres de client ou le déploiement de contenu. D'un autre côté, la découverte du réseau vous fournit des informations sur la topologie de votre réseau que vous ne pouvez pas obtenir avec les autres méthodes de découverte. Toutefois, la découverte du réseau ne fournit pas d'informations sur votre environnement Active Directory.  

 Il est également possible d'utiliser uniquement la découverte par pulsations d'inventaire pour forcer la découverte des clients que vous avez installés à l'aide de méthodes autres que l'installation poussée du client. Cependant, contrairement aux autres méthodes de découverte, la découverte par pulsations d’inventaire ne peut pas découvrir des ordinateurs qui ne disposent pas d’un client Configuration Manager actif et renvoie un ensemble limité d’informations. Elle est conçue pour gérer un enregistrement de base de données existant et non pour servir de base de cet enregistrement. Les informations soumises par la découverte par pulsations d'inventaire peuvent ne pas suffire à construire des requêtes ou des regroupements complexes.  

 Si vous utilisez la découverte de groupes Active Directory pour découvrir l'appartenance d'un groupe spécifique, vous pouvez découvrir des informations limitées sur le système ou l'ordinateur. Cela ne remplace pas une découverte complète des ordinateurs, mais peut fournir des informations de base. Ces informations de base sont insuffisantes pour l'installation poussée du client.  

 **Découverte d’utilisateurs**   
Quand vous voulez découvrir des informations sur les utilisateurs, vous pouvez utiliser la découverte d'utilisateurs Active Directory. Tout comme la découverte de systèmes Active Directory, cette méthode découvre des utilisateurs à partir d'Active Directory et inclut des informations de base en plus des informations étendues Active Directory. Vous pouvez utiliser ces informations pour générer des requêtes et des regroupements complexes similaires à ceux des ordinateurs.  

 **Découverte d’informations de groupe**   
Quand vous voulez découvrir des informations sur les groupes et les appartenances aux groupes, utilisez la découverte de groupes Active Directory. Cette méthode de découverte crée des enregistrements de ressources pour les groupes de sécurité.  

 Vous pouvez utiliser cette méthode pour rechercher un groupe spécifique d'Active Directory afin d'identifier les membres de ce groupe, ainsi que les groupes imbriqués dans ce groupe. Cette méthode permet également de rechercher des groupes dans un emplacement Active Directory et de rechercher, de manière récursive, chaque conteneur enfant de cet emplacement dans les services de domaine Active Directory.  

 Cette méthode de découverte peut également rechercher l'appartenance des groupes de distribution. Elle permet également d'identifier les relations de groupe des utilisateurs et des ordinateurs.  

 Lorsque vous découvrez un groupe, vous pouvez également découvrir des informations limitées sur ses membres. Cela ne remplace pas la découverte de systèmes Active Directory ou la découverture d'utilisateurs Active Directory, et ne suffit généralement pas pour créer des requêtes et des regroupements complexes ou pour servir de base pour une installation poussée du client.  

 **Découverte d’infrastructure**   
Il existe deux méthodes pour découvrir l'infrastructure du réseau, la découverte de forêts Active Directory et la découverte du réseau.  

 Vous pouvez utiliser la découverte de forêts Active Directory pour rechercher des informations sur les sous-réseaux et les configurations de site Active Directory dans une forêt Active Directory. Ces configurations peuvent ensuite être automatiquement entrées dans Configuration Manager en tant qu’emplacements limites.  

 Lorsque vous souhaitez découvrir la topologie de votre réseau, utilisez la découverte du réseau. Les autres méthodes de découverte renvoient des informations liées aux services de domaine Active Directory et peuvent identifier l'emplacement réseau actuel d'un client, mais elles ne peuvent pas fournir des informations d'infrastructure basées sur la topologie des sous-réseaux ou du routeur de votre réseau.  

##  <a name="a-namebkmkshareda-discovery-data-is-shared-between-sites"></a><a name="bkmk_shared"></a> Les données de découverte sont partagées entre les sites  
 Une fois que Configuration Manager a ajouté des données de découverte à une base de données, elles sont rapidement partagées entre tous les sites de la hiérarchie. Comme il n’y a généralement pas d’avantage à découvrir les mêmes informations sur plusieurs sites de votre hiérarchie, il peut être judicieux de configurer une seule instance de chaque méthode de découverte que vous utilisez, pour qu’elle s’exécute sur un seul site, plutôt que d’exécuter plusieurs instances d’une seule méthode sur différents sites.  

 Il peut toutefois être utile, pour certains environnements, d’attribuer la même méthode de découverte à plusieurs sites, avec une configuration et une planification distinctes à chaque fois. Cela tien t au fait que les configurations d’exécution d’une méthode de découverte sont spécifiques à un site unique. Cela vous permet d’exécuter la découverte sur un site, puis de partager les résultats avec d’autres sites ou d’utiliser la même méthode sur deux sites différents, lorsque la découverte s’exécute sur une ressource locale et n’essaie pas de découvrir des informations à partir d’emplacements sur un réseau WAN.  Par exemple, cela est souvent utile lorsque vous utilisez la découverte du réseau et dirigez chaque site pour découvrir son réseau local au lieu d’essayer d’exécuter la découverte de tous les emplacements réseau sur un réseau WAN. Si vous configurez plusieurs instances des mêmes méthodes de découverte pour qu’elles s’exécutent sur différents sites, planifiez avec soin la configuration de chaque site pour éviter que plusieurs sites ne découvrent les mêmes ressources à partir de votre réseau ou d’Active Directory. La découverte d’emplacements et de ressources identiques sur plusieurs sites peut consommer plus de bande passante réseau et créer des doublons d’enregistrements de données de découverte pour les ressources, qui ne présentent pas d’intérêt mais qui doivent tout de même être traités par vos serveurs de site.  

 Le tableau suivant identifie sur quels sites vous pouvez configurer les différentes méthodes de découverte.  

|Méthode de découverte|Emplacements pris en charge|  
|----------------------|-------------------------|  
|Découverte de forêts Active Directory|Site d'administration centrale<br /><br /> Site principal|  
|Découverte de groupes Active Directory|Site principal|  
|Découverte de systèmes Active Directory|Site principal|  
|Découverte d’utilisateurs Active Directory|Site principal|  
|Découverte par pulsations d’inventaire<sup>1</sup>|Site principal|  
|Découverte du réseau|Site principal<br /><br /> Site secondaire|  

 <sup>1</sup> Les sites secondaires ne peuvent pas configurer la découverte par pulsations d’inventaire, mais peuvent recevoir l’enregistrement de données de découverte par pulsation de la part d’un client.  

 Lorsque des sites secondaires exécutent la découverte du réseau, ou reçoivent des DDR de découverte par pulsations d'inventaire, ils transfèrent le DDR par réplication basée sur les fichiers vers leur site principal parent. Ceci est dû au fait que seuls les sites principaux et les sites d’administration centrale peuvent traiter les enregistrements de données de découverte. Pour plus d’informations sur le traitement des enregistrements de données de découverte, consultez [À propos des enregistrements de données de découverte](../../../../core/servers/deploy/configure/run-discovery.md#BKMK_DDRs).  

## <a name="considerations-for-different-discovery-methods"></a>Éléments à prendre en compte pour différentes méthodes de découverte  
 Comme chaque serveur de site et chaque environnement réseau sont différents, limitez vos configurations initiales pour la découverte, puis surveillez de près chaque serveur de site pour connaître sa capacité à traiter les données de découverte générées.  

-   Lorsque vous utilisez une méthode de découverte Active Directory pour les systèmes, les utilisateurs ou les groupes :  

    -   Exécutez la découverte sur un site qui dispose d'une connexion réseau rapide pour vos contrôleurs de domaine.  

    -   Pensez à la topologie de réplication Active Directory pour vous assurer que la découverte peut accéder aux informations les plus récentes.  

    -   Pensez à l'étendue de la configuration de la découverte et limitez la découverte aux emplacements et groupes Active Directory que vous souhaitez découvrir.  

-   Si vous utilisez la découverte du réseau :  

    -   Utilisez une configuration initiale limitée pour identifier votre topographie réseau.  

    -   Après avoir identifié votre topographie réseau, configurez la découverte du réseau pour qu'elle s'exécute sur des sites spécifiques, qui jouent un rôle central pour les zones du réseau que vous souhaitez découvrir plus en détail.  

-   Dans la mesure où la découverte par pulsations d'inventaire ne s'exécute pas sur un site spécifique, vous n'avez pas besoin de prendre en compte le lieu de l'exécution dans la planification générale.  

-   Comme chaque serveur de site et chaque environnement réseau est différent, limitez les configurations de la découverte initiale et surveillez attentivement chaque serveur de site pour connaître sa capacité à traiter les données de découverte ainsi générées.  

##  <a name="a-namebkmkbesta-best-practices-for-discovery"></a><a name="bkmk_best"></a> Bonnes pratiques pour la découverte  
 **Réalisez une découverte de systèmes Active Directory et une découverte d’utilisateurs Active Directory avant de procéder à une découverte de groupes Active Directory :**  

 Lorsqu'une découverte de groupes Active Directory identifie en tant que membre d'un groupe un ordinateur ou un utilisateur jusqu'alors inconnu, elle tente de découvrir les détails de base concernant cet utilisateur ou cet ordinateur. Comme la découverte de groupes Active Directory n'est pas optimisée pour ce type de découverte, ce processus peut provoquer un ralentissement de la découverte de groupes Active Directory. Par ailleurs, la découverte de groupes Active Directory identifie uniquement les informations de base sur les utilisateurs et ordinateurs, et ne crée pas d'enregistrement complet de découverte d'utilisateurs ou d'ordinateurs. Lorsque vous procédez à une découverte de systèmes Active Directory et à une découverte d'utilisateurs Active Directory, les attributs Active Directory supplémentaires de chaque type d'objet sont disponibles. Par conséquent, la découverte de groupes Active Directory est plus performante.  

 **Lorsque vous configurez la découverte de groupes Active Directory, spécifiez uniquement les groupes que vous utilisez avec Configuration Manager :**  

 Pour mieux contrôler les ressources utilisées par le processus de découverte de groupes Active Directory, spécifiez uniquement les groupes que vous utilisez avec Configuration Manager. En effet, la découverte de groupes Active Directory recherche de manière récursive les utilisateurs, les ordinateurs et les groupes imbriqués dans chaque groupe qu'elle découvre. La recherche dans chaque groupe imbriqué peut élargir l'étendue de la découverte de groupes Active Directory et réduire les performances. En outre, lorsque vous configurez la découverte delta pour la découverte de groupes Active Directory, la méthode de découverte surveille les modifications apportées à chaque groupe. Les performances sont ainsi d'autant plus ralenties lorsque la méthode doit rechercher des groupes qui ne sont pas nécessaires.  

 **Configurez les méthodes de découverte de telle sorte que l’intervalle entre les découvertes complètes soit plus long et que les découvertes delta soient plus fréquentes :**  

 La découverte delta consomme moins de ressources qu'un cycle de découverte complète et peut identifier les ressources nouvelles ou modifiées dans Active Directory. Par conséquent, en utilisant une découverte delta, vous pouvez réduire la fréquence des cycles de découverte complète à un par semaine ou moins. La découverte delta de la découverte de systèmes Active Directory, de la découverte d'utilisateurs Active Directory et de la découverte de groupes Active Directory identifie presque toutes les modifications apportées aux objets Active Directory et peut conserver des données de découverte exactes concernant les ressources.  

 **Exécutez les méthodes de découverte Active Directory sur le site principal dont l’emplacement réseau est le plus proche de votre contrôleur de domaine Active Directory :**  

 Pour améliorer les performances de la découverte Active Directory, il est recommandé de l'exécuter sur un site principal connecté aux contrôleurs de domaine via une connexion réseau rapide. Si vous exécutez la même méthode de découverte Active Directory sur plusieurs sites, il est recommandé de configurer chaque méthode de découverte pour éviter les chevauchements. Contrairement aux versions antérieures de Configuration Manager, les données de découverte sont partagées entre les sites. Par conséquent, il n'est pas nécessaire de procéder à la découverte des mêmes informations sur plusieurs sites. Pour plus d’informations, consultez [Les données de découverte sont partagées entre les sites](../../../../core/servers/deploy/configure/select-discovery-methods-to-use.md#bkmk_shared).  

 **Procédez à une découverte de forêts Active Directory sur un seul site quand vous envisagez de créer automatiquement des limites à partir des données de découverte :**  

 Si vous réalisez une découverte de forêts Active Directory sur plusieurs sites d'une hiérarchie, il est recommandé d'activer les options permettant de créer automatiquement des limites uniquement sur un site. En effet, lorsqu’une découverte de forêts Active Directory est réalisée sur chaque site et crée des limites, Configuration Manager ne peut pas fusionner ces limites en un objet de limite unique. Si vous configurez la découverte de forêts Active Directory de façon à ce qu’elle crée automatiquement des limites sur plusieurs sites, vous risquez de créer des objets de limite en double dans la console Configuration Manager.  



<!--HONumber=Dec16_HO3-->


