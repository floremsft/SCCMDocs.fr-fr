---
title: "Notions de base de la sécurité | System Center Configuration Manager"
description: "En savoir plus sur les couches de sécurité pour System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 035b7f73-8b78-4ed1-835e-a31f9a5c4a02
caps.latest.revision: 5
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: cb84efcaac281aa8c9338cd69ce32054ea775de3


---
# <a name="fundamentals-of-security-for-system-center-configuration-manager"></a>Notions de base de la sécurité pour System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

La sécurité pour System Center Configuration Manager se compose de plusieurs couches. La première couche est fournie par les fonctionnalités de sécurité Windows tant pour le système d’exploitation que pour le réseau, qui incluent :  

-   le partage de fichiers pour transférer les fichiers entre des composants Configuration Manager ;  

-   des listes de contrôle d'accès pour sécuriser les fichiers et les clés de Registre ;  

-   le protocole IPsec pour sécuriser les communications ;  

-   une stratégie de groupe pour définir une stratégie de sécurité ;  

-   les autorisations DCOM pour les applications distribuées, telles que la console Configuration Manager ;  

-   des services de domaine Active Directory pour stocker les entités de sécurité ;  

-   la sécurité de compte Windows, notamment certains groupes qui sont créés pendant la configuration de Configuration Manager.  

Des composants de sécurité supplémentaires (pare-feu, fonctionnalité de détection d'intrusions, par exemple) assurent une excellente protection de l'ensemble de votre environnement. Les certificats émis par les infrastructures à clé publique (PKI) standard permettent d'assurer l'authentification, la signature et le chiffrement.  

Outre la sécurité fournie par l’infrastructure réseau et de serveur Windows, Configuration Manager contrôle l’accès à la console Configuration Manager et à ses ressources de plusieurs façons. Par défaut, seuls les administrateurs locaux disposent des droits d’accès aux fichiers et aux clés de Registre nécessaires à l’exécution de la console Configuration Manager sur les ordinateurs où elle est installée.  

La couche de sécurité suivante est basée sur l’accès à l’aide de WMI (Windows Management Instrumentation), en particulier le **fournisseur SMS**. Le fournisseur SMS est un composant Configuration Manager qui octroie un accès à un utilisateur pour interroger la base de données du site afin d’obtenir des informations. Par défaut, l’accès au fournisseur est restreint aux membres du groupe **Administrateurs SMS** local. À l’origine, ce groupe contient uniquement l’utilisateur qui a installé Configuration Manager. Pour accorder d'autres autorisations de compte à l'emplacement de stockage CIM (Common Information Model) et au fournisseur SMS, ajoutez les autres comptes au groupe Administrateurs SMS.  

Les autorisations d'accès aux objets de la base de données de site constituent la dernière couche de sécurité. Par défaut, le compte système local et le compte d’utilisateur que vous utilisez pour installer Configuration Manager peuvent administrer tous les objets de la base de données du site. Vous pouvez accorder et limiter les autorisations à des utilisateurs administratifs supplémentaires à partir de la console Configuration Manager à l’aide de l’**administration basée sur des rôles**.  

Le reste de cette rubrique traite des aspects de la sécurité liés à Configuration Manager.  

## <a name="role-based-administration"></a>Administration basée sur des rôles  
 Configuration Manager utilise l’administration basée sur des rôles pour sécuriser les objets (regroupements, déploiements, sites, etc.). Ce modèle d'administration définit et gère de façon centralisée les paramètres d'accès de sécurité à l'échelle de la hiérarchie pour tous les sites et les paramètres du site. Les rôles de sécurité sont attribués aux utilisateurs administratifs et regroupent les autorisations pour différents types d’objet Configuration Manager, par exemple les autorisations permettant de créer ou de modifier des paramètres client. Les étendues de sécurité regroupent des instances d’objets spécifiques qu’un utilisateur administrateur est chargé de gérer, par exemple, une application qui installe Microsoft Office. La combinaison des rôles de sécurité, des étendues de sécurité et des regroupements définit les objets qu'un utilisateur administrateur peut afficher et gérer. Configuration Manager installe des rôles de sécurité par défaut pour les tâches de gestion classiques. Vous pouvez toutefois créer vos propres rôles de sécurité, en fonction des besoins propres à votre activité.  

 Pour plus d’informations, consultez [Configurer l’administration basée sur des rôles pour System Center Configuration Manager](../../core/servers/deploy/configure/configure-role-based-administration.md).  

## <a name="securing-client-endpoints"></a>Sécurisation des points de terminaison des clients  
 La communication du client vers les rôles de système de site est sécurisée à l'aide de certificats auto-signés ou à l'aide de certificats d'infrastructure à clé publique (PKI). Les ordinateurs clients dont Configuration Manager détecte qu’ils sont sur Internet et les clients d’appareils mobiles doivent utiliser des certificats PKI afin que les points de terminaison des clients soient sécurisés à l’aide du protocole HTTPS. Les rôles de système de site auxquels les clients se connectent peuvent être configurés pour utiliser les protocoles HTTPS ou HTTP dans le cadre de la communication avec les clients. Les ordinateurs clients communiquent toujours par la méthode disponible la plus sécurisée et utilisent le protocole HTTP (moins sécurisé) sur l'intranet uniquement si vos rôles de système de site autorisent la communication HTTP.  

 Pour plus d’informations, consultez [Informations techniques de référence sur les contrôles de chiffrement pour System Center Configuration Manager](../../protect/deploy-use/cryptographic-controls-technical-reference.md)  

## <a name="configuration-manager-accounts-and-groups"></a>Comptes et groupes de Configuration Manager  
 Configuration Manager utilise le compte **Système local** pour la plupart des opérations de site. Toutefois, certaines tâches de gestion peuvent nécessiter la création et la gestion des comptes supplémentaires. Différents groupes par défaut et rôles SQL Server sont créés pendant l'installation. Toutefois, vous devrez ajouter manuellement des comptes d'ordinateur ou des comptes d'utilisateur à ces groupes par défaut et à ces rôles.  

 Pour plus d’informations, consultez [Comptes utilisés dans System Center Configuration Manager](../../core/plan-design/hierarchy/accounts.md).  

## <a name="privacy"></a>Confidentialité  
 Bien que les produits de gestion d'entreprise offrent de nombreux avantages, car ils permettent de gérer efficacement un grand nombre de clients, vous devez également être conscient de l'impact de ces logiciels sur la confidentialité des utilisateurs de votre organisation. System Center Configuration Manager propose de nombreux outils pour collecter des données et surveiller les appareils, dont certains peuvent créer des problèmes de confidentialité.  

 Par exemple, quand vous installez le client Configuration Manager, de nombreux paramètres de gestion sont activés par défaut. Ainsi, le logiciel client envoie des informations au site Configuration Manager. Les informations sur le client sont stockées dans la base de données Configuration Manager et ne sont pas envoyées à Microsoft. Avant d’implémenter System Center Configuration Manager, pensez à vos exigences en matière de confidentialité.  



<!--HONumber=Nov16_HO1-->


