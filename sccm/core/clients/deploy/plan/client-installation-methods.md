---
title: "Méthodes d’installation du client | Microsoft Docs"
description: "Découvrez les méthodes d’installation du client pour System Center Configuration Manager."
ms.custom: na
ms.date: 04/25/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 51b5964b-374d-4abc-8619-414a9fffad2d
caps.latest.revision: 9
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.translationtype: Human Translation
ms.sourcegitcommit: d94acac84f052a01de9d9c9f65f237c0006c45b8
ms.openlocfilehash: edca31249cc2bb3e0c67265962815c82e3f4711e
ms.contentlocale: fr-fr
ms.lasthandoff: 05/17/2017


---
# <a name="client-installation-methods-in-system-center-configuration-manager"></a>Méthodes d’installation du client dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Vous pouvez utiliser différentes méthodes pour installer le logiciel client Configuration Manager. Vous pouvez utiliser une méthode ou une combinaison de méthodes. Passez en revue cette rubrique pour déterminer la méthode la mieux adaptée à votre organisation.  

## <a name="client-push-installation"></a>Installation poussée du client  

 **Plateforme cliente prise en charge :** Windows  

 **Avantages**  

-   Peut être utilisée pour installer le client sur un seul ordinateur, un regroupement d'ordinateurs ou pour les résultats d'une requête.  

-   Peut être utilisée pour installer automatiquement le client sur tous les ordinateurs découverts.  

-   Utilise automatiquement les propriétés d'installation du client définies sous l'onglet **Client** de la boîte de dialogue **Propriétés de l'installation poussée du client** .  

 **Inconvénients**  

-   Une installation poussée vers des regroupements volumineux peut entraîner un trafic réseau excessif.  

-   Peut être utilisée uniquement sur les ordinateurs ayant été découverts par Configuration Manager.  

-   Ne peut pas être utilisée pour installer des clients dans un groupe de travail.  

-   Vous devez spécifier un compte d'installation poussée du client disposant des droits d'administration sur l'ordinateur client souhaité.  

-   Le Pare-feu Windows doit être configuré sur les ordinateurs clients avec des exceptions permettant d'effectuer l'installation poussée du client.  

-   Il n'est pas possible d'annuler une installation poussée du client. Lorsque vous utilisez cette méthode d’installation du client pour un site, Configuration Manager tente d’installer le client sur toutes les ressources découvertes et tente à nouveau toutes les opérations ayant échoué pendant 7 jours.  

 Pour plus d’informations sur cette méthode d’installation, consultez [Comment déployer des clients sur les ordinateurs Windows dans System Center Configuration Manager](../../../../core/clients/deploy/deploy-clients-to-windows-computers.md).  

## <a name="software-update-point-based-installation"></a>Installation basée sur un point de mise à jour logicielle  
 **Plateforme cliente prise en charge :** Windows  

 **Avantages :**  

-   Peut utiliser votre infrastructure de mises à jour logicielles existante pour gérer le logiciel client.  

-   Peut installer automatiquement le logiciel client sur de nouveaux ordinateurs si Windows Server Update Services (WSUS) et les paramètres de stratégie de groupe dans les services de domaine Active Directory sont correctement configurés.  

-   N'exige pas la découverte des ordinateurs avant l'installation du client.  

-   Les ordinateurs peuvent lire les propriétés de l'installation du client ayant été publiées dans les services de domaine Active Directory.  

-   Réinstalle le logiciel client si celui-ci est supprimé.  

-   Ne nécessite pas de configuration ni la présence d'un compte d'installation pour l'ordinateur client choisi.  

 **Inconvénients :**  

-   Nécessite une infrastructure de mises à jour logicielles opérationnelle.  

-   Doit utiliser le même serveur pour l'installation du client et les mises à jour logicielles. Ce serveur doit résider sur un site principal.  

-   Pour installer de nouveaux clients, vous devez configurer un objet de stratégie de groupe (GPO) pour les services de domaine Active Directory, ainsi que le port et le point de mise à jour logicielle actifs du client.  

-   Si le schéma Active Directory n’est pas étendu pour Configuration Manager, vous devez utiliser les paramètres de stratégie de groupe pour fournir les propriétés d’installation du client aux ordinateurs.  

 Pour plus d’informations sur cette méthode d’installation, consultez [Comment déployer des clients sur les ordinateurs Windows dans System Center Configuration Manager](../../../../core/clients/deploy/deploy-clients-to-windows-computers.md).  

## <a name="group-policy-installation"></a>Installation via la stratégie de groupe  
 **Plateforme cliente prise en charge :** Windows  

 **Avantages :**  

-   N'exige pas la découverte des ordinateurs avant l'installation du client.  

-   Peut être utilisée pour l'installation de nouveaux clients ou pour les mises à niveau.  

-   Les ordinateurs peuvent lire les propriétés de l'installation du client ayant été publiées dans les services de domaine Active Directory.  

-   Ne nécessite pas de configuration ni la présence d'un compte d'installation pour l'ordinateur client choisi.  

 **Inconvénients :**  

-   Peut entraîner un trafic réseau excessif s'il est nécessaire d'installer un grand nombre de clients.  

-   Si le schéma Active Directory n’est pas étendu pour Configuration Manager, vous devez utiliser les paramètres de stratégie de groupe pour ajouter les propriétés d’installation du client sur les ordinateurs de votre site.  

 Pour plus d’informations sur cette méthode d’installation, consultez [Comment déployer des clients sur les ordinateurs Windows dans System Center Configuration Manager](../../../../core/clients/deploy/deploy-clients-to-windows-computers.md).  

## <a name="logon-script-installation"></a>Installation via un script d'ouverture de session  
 **Plateforme cliente prise en charge :** Windows  

 **Avantages :**  

-   N'exige pas la découverte des ordinateurs avant l'installation du client.  

-   Prend en charge les propriétés de ligne de commande de CCMSetup.  

 **Inconvénients :**  

-   Peut entraîner un trafic réseau excessif s'il est nécessaire d'installer un grand nombre de clients sur une courte période.  

-   Le temps nécessaire à l'installation sur tous les ordinateurs clients peut être long si des utilisateurs se connectent rarement au réseau.  

 Pour plus d’informations sur cette méthode d’installation, consultez [Comment déployer des clients sur les ordinateurs Windows dans System Center Configuration Manager](../../../../core/clients/deploy/deploy-clients-to-windows-computers.md).  

## <a name="manual-installation"></a>Installation manuelle  
 **Plateformes clientes prises en charge :** Windows, UNIX/Linux, Mac OS X  

 **Avantages :**  

-   N'exige pas la découverte des ordinateurs avant l'installation du client.  

-   Peut être utile dans le cadre de tests.  

-   Prend en charge les propriétés de ligne de commande de CCMSetup.  

 **Inconvénients :**  

-   Aucune automatisation, peut prendre du temps.  

 Pour plus d’informations sur la façon d’installer manuellement le client sur chaque plateforme, voir les rubriques suivantes :  

-   [Guide pratique pour déployer des clients sur des ordinateurs Windows dans System Center Configuration Manager](../../../../core/clients/deploy/deploy-clients-to-windows-computers.md)  

-   [Guide pratique pour déployer des clients sur des serveurs UNIX et Linux dans System Center Configuration Manager](../../../../core/clients/deploy/deploy-clients-to-unix-and-linux-servers.md)  

-   [Guide pratique pour déployer des clients sur des ordinateurs Mac dans System Center Configuration Manager](../../../../core/clients/deploy/deploy-clients-to-macs.md)  

