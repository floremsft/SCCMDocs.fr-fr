---
title: "Présentation des profils de certificat | Microsoft Docs"
description: "Découvrez le fonctionnement des profils de certificat dans System Center Configuration Manager avec les services de certificats Active Directory."
ms.custom: na
ms.date: 12/28/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 41dcc259-f147-4420-bff2-b65bdf8cff77
caps.latest.revision: 7
author: arob98
ms.author: angrobe
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 8a5dc7361da34f3e6b926acd35c72c0c0767ce70
ms.openlocfilehash: d51670b47aab77cc4e630a6aeaa0744f916bf3b9
ms.lasthandoff: 12/29/2016


---
# <a name="introduction-to-certificate-profiles-in-system-center-configuration-manager"></a>Présentation des profils de certificat dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*


Les profils de certificat fonctionnent avec les services de certificats Active Directory et le rôle Service d’inscription d’appareil réseau pour configurer des certificats d’authentification pour les appareils gérés afin que les utilisateurs puissent accéder en toute transparence aux ressources d’entreprise. Par exemple, vous pouvez créer et déployer des profils de certificat pour fournir les certificats nécessaires aux utilisateurs pour établir des connexions VPN et sans fil. 

Les profils de certificat peuvent automatiquement configurer des appareils d'utilisateur pour que les ressources d'entreprise, telles que les réseaux Wi-Fi et les serveurs VPN, soient accessibles sans avoir à installer manuellement des certificats ou à utiliser un processus hors bande. Les profils de certificat peuvent également contribuer à sécuriser les ressources d'entreprise, car vous pouvez utiliser les paramètres plus sécurisés pris en charge par votre infrastructure à clé publique (PKI) d'entreprise. Par exemple, vous pouvez exiger l'authentification du serveur pour toutes les connexions VPN et Wi-Fi car vous avez provisionné les certificats requis sur les appareils gérés.   

Les profils de certificat fournissent les fonctionnalités de gestion suivantes :  

-   Inscription et renouvellement de certificats auprès d’une autorité de certification d’entreprise pour les appareils exécutant iOS, Windows 8.1, Windows RT 8.1, Windows 10 Desktop et Mobile, et Android. Ces certificats peuvent ensuite être utilisés pour les connexions VPN et Wi-Fi.  

-   Déploiement de certificats d'autorité de certification racine approuvés et de certificats d'autorité de certification intermédiaires pour configurer une chaîne d'approbation sur les appareils pour les connexions VPN et Wi-Fi, lorsque l'authentification du serveur est requise.  

-   Analyse et rapport sur les certificats installés.  

**Exemple :** Tous les employés doivent pouvoir se connecter à des points d'accès Wi-Fi répartis à différents endroits dans l'entreprise. Déployez les certificats nécessaires pour se connecter au Wi-Fi et déployez les profils Wi-Fi qui référencent le certificat pour permettre une connexion fluide de l’utilisateur.  

**Exemple :** Vous disposez d'une PKI en place et voulez adopter une méthode plus flexible et sécurisée pour configurer les certificats qui permettent aux utilisateurs d'accéder aux ressources d'entreprise à partir de leurs appareils personnels sans compromettre la sécurité. Configurez des profils de certificat avec les paramètres et protocoles pris en charge par la plateforme d’appareil spécifique. Les appareils peuvent ensuite demander automatiquement ces certificats depuis un serveur d'inscription via Internet. Ensuite, configurez des profils VPN pour utiliser ces certificats afin que l’appareil puisse accéder aux ressources d’entreprise.  

## <a name="types-of-certificate-profiles"></a>Types de profil de certificat  
 Il existe trois types de profil de certificat :  

-   **Certificat d'Autorité de certification approuvé** : vous permet de déployer un certificat d'autorité de certification racine ou intermédiaire approuvé pour former une chaîne d'approbation des certificats lorsque l'appareil doit authentifier un serveur.  

-   **Protocole SCEP (Simple Certificate Enrollment Protocol)** : vous permet de demander un certificat pour un appareil ou un utilisateur à l’aide du protocole SCEP et du service d’inscription d’appareil réseau sur un serveur exécutant Windows Server 2012 R2.
-   -   **Échange d’informations personnelles (.pfx)** : vous permet de demander un certificat .pfx (également appelé PKCS #12) pour un appareil ou un utilisateur.

    > [!NOTE]  
    >  Vous devez créer un profil de certificat du type **Certificat d’autorité de certification approuvé** avant de pouvoir créer un profil de certificat du type **Protocole SCEP (Simple Certificate Enrollment Protocol)**.  

## <a name="requirements-and-supported-platforms"></a>Configuration requise et plateformes prises en charge  
 Pour déployer des profils de certificat qui utilisent le protocole SCEP, vous devez installer le point d’enregistrement de certificat sur un serveur de système de site du site d’administration centrale ou d’un site principal. Vous devez également installer un module de stratégie pour NDES, le module de stratégie de Configuration Manager, sur un serveur exécutant Windows Server 2012 R2 avec le rôle de services de certificats Active Directory et un service NDES accessible aux appareils qui nécessitent les certificats. Pour les appareils inscrits par Microsoft Intune, le service NDES doit être accessible sur Internet, par exemple, dans un sous-réseau filtré (également appelé DMZ).  

 Pour plus d’informations sur la façon dont le service NDES prend en charge un module de stratégie pour que Configuration Manager puisse déployer des certificats, consultez [Utilisation d’un module de stratégie avec le service d’inscription de périphérique réseau](http://go.microsoft.com/fwlink/p/?LinkId=328657).  

 Configuration Manager prend en charge le déploiement de certificats sur différents magasins de certificats, en fonction de la configuration requise, du type d’appareil et du système d’exploitation. Les appareils et les systèmes d'exploitation suivants sont pris en charge :  

-   Windows RT 8.1  

-   Windows 8.1  

-   Windows Phone 8.1  

-   Windows 10 Desktop et Mobile  

-   iOS  

-   Android  

> [!IMPORTANT]  
>  Pour déployer des profils sur des appareils Android, iOS, Windows Phone et sur des appareils Windows 8.1 ou version ultérieure inscrits, ces appareils doivent être [inscrits dans Microsoft Intune](https://technet.microsoft.com/en-us/library/dn646962.aspx).   

Un scénario type pour System Center Configuration Manager consiste à installer des certificats d’autorité de certification racine approuvés pour authentifier des serveurs Wi-Fi et VPN lorsque la connexion utilise les protocoles d’authentification EAP-TLS, EAP-TTLS et PEAP, ainsi que les protocoles de tunneling IKEv2, L2TP/IPsec et Cisco IPsec VPN.  

Vous devez vous assurer qu'un certificat d'autorité de certification racine d'entreprise est installé sur l'appareil avant que l'appareil puisse demander des certificats à l'aide d'un profil de certificat SCEP.  

Vous pouvez spécifier divers paramètres dans un profil de certificat SCEP pour demander des certificats personnalisés pour différents environnements ou besoins en connectivité. L' **Assistant Créer un profil de certificat** comporte deux pages pour les paramètres d'inscription. La première, **Inscription SCEP**, contient les paramètres de la demande d'inscription et l'emplacement où installer le certificat. La seconde, **Propriétés du certificat**, décrit le certificat demandé.  

## <a name="deploying-certificate-profiles"></a>Déploiement de profils de certificat  
 Lorsque vous déployez un profil de certificat, les fichiers de certificat dans le profil sont installés sur des appareils clients. Tous les paramètres SCEP sont également déployés et les demandes SCEP sont traitées sur l'appareil client. Vous pouvez déployer des profils de certificat sur des regroupements d’utilisateurs ou d’appareils, et spécifier le magasin de destination pour chaque certificat. Les règles de mise en application déterminent si les certificats peuvent être installés sur l’appareil. Quand vous déployez des profils de certificat sur des regroupements d’utilisateurs, l’affinité entre appareil et utilisateur détermine les appareils d’utilisateur qui doivent installer les certificats. Quand des profils de certificat contenant des certificats d’utilisateur sont déployés sur des regroupements d’appareils, par défaut, les certificats sont installés sur chacun des appareils principaux de l’utilisateur. Vous pouvez modifier ce comportement pour installer le certificat sur l’un des appareils de l’utilisateur dans la page **Inscription SCEP** de l’**Assistant Création d’un profil de certificat**. En outre, les certificats d'utilisateur ne seront pas déployés sur les appareils s'il s'agit d'ordinateurs de groupe de travail.  

## <a name="monitoring-certificate-profiles"></a>Surveillance des profils de certificat  

Vous pouvez surveiller les déploiements de profil de certificat en affichant les résultats ou les rapports de conformité. Ces approches sont décrites dans [Guide pratique pour surveiller des profils de certificat](/sccm/protect/deploy-use/monitor-certificate-profiles).


## <a name="automatic-revocation-of-certificates"></a>Révocation automatique de certificats  
 System Center Configuration Manager révoque automatiquement les certificats utilisateur et ordinateur qui ont été déployés à l’aide de profils de certificat dans les circonstances suivantes :  

-   L’appareil est mis hors service depuis la gestion de System Center Configuration Manager.  

-   Une réinitialisation sélective est appliquée à l'appareil.  

-   L’appareil est bloqué depuis la hiérarchie System Center Configuration Manager.  

 Pour révoquer les certificats, le serveur de site envoie une commande de révocation à l'autorité de certification émettrice. Le motif de révocation est la **cessation de fonctionnement**.  

