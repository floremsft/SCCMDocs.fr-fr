---
title: "Présentation des profils de certificat | Microsoft Docs"
description: "Découvrez le fonctionnement des profils de certificat dans System Center Configuration Manager avec les services de certificats Active Directory."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 41dcc259-f147-4420-bff2-b65bdf8cff77
caps.latest.revision: 7
author: Nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: bff083fe279cd6b36a58305a5f16051ea241151e
ms.openlocfilehash: 25d57d25ca683608bbe9a0695b2463ad5b9a0833


---
# <a name="introduction-to-certificate-profiles-in-system-center-configuration-manager"></a>Présentation des profils de certificat dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*


Les profils de certificat dans System Center Configuration Manager s’intègrent aux services de certificats Active Directory et au rôle du service d’inscription de périphérique réseau afin d’approvisionner des certificats d’authentification pour des appareils gérés afin que les utilisateurs puissent accéder sans interruption aux ressources de l’entreprise. Par exemple, vous pouvez créer et déployer des profils de certificat pour fournir les certificats nécessaires aux utilisateurs pour établir des connexions VPN et sans fil.  

 Les profils de certificat dans System Center Configuration Manager fournissent les fonctionnalités de gestion suivantes :  

-   Inscription et renouvellement de certificats auprès d’une autorité de certification d’entreprise pour les appareils exécutant iOS, Windows 8.1, Windows RT 8.1, Windows 10 Desktop et Mobile, et Android. Ces certificats peuvent ensuite être utilisés pour les connexions Wi-Fi et VPN.  

-   Déploiement de certificats d'autorité de certification racine approuvés et de certificats d'autorité de certification intermédiaires pour configurer une chaîne d'approbation sur les appareils pour les connexions VPN et Wi-Fi, lorsque l'authentification du serveur est requise.  

-   Analyse et rapport sur les certificats installés.  

 Les profils de certificat peuvent automatiquement configurer des appareils d'utilisateur pour que les ressources d'entreprise, telles que les réseaux Wi-Fi et les serveurs VPN, soient accessibles sans avoir à installer manuellement des certificats ou à utiliser un processus hors bande. Les profils de certificat peuvent également contribuer à sécuriser les ressources d'entreprise, car vous pouvez utiliser les paramètres plus sécurisés pris en charge par votre infrastructure à clé publique (PKI) d'entreprise. Par exemple, vous pouvez exiger l'authentification du serveur pour toutes les connexions VPN et Wi-Fi car vous avez provisionné les certificats requis sur les appareils gérés.  

 **Exemple :** Tous les employés doivent pouvoir se connecter à des points d'accès Wi-Fi répartis à différents endroits dans l'entreprise. Pour cela, vous pouvez déployer les certificats requis pour établir la connexion Wi-Fi et également déployer des profils Wi-Fi dans System Center Configuration Manager qui référencent le certificat approprié à utiliser pour que la connexion Wi-Fi s’établisse de façon homogène pour les utilisateurs.  

 **Exemple :** Vous disposez d'une PKI en place et voulez adopter une méthode plus flexible et sécurisée pour configurer les certificats qui permettent aux utilisateurs d'accéder aux ressources d'entreprise à partir de leurs appareils personnels sans compromettre la sécurité. Pour ce faire, vous pouvez configurer des profils de certificat avec les paramètres et les protocoles qui sont pris en charge pour la plate-forme d'appareil spécifique. Les appareils peuvent ensuite demander automatiquement ces certificats depuis un serveur d'inscription via Internet. Vous pouvez ensuite configurer des profils VPN pour utiliser ces certificats afin que l'appareil puisse accéder aux ressources d'entreprise.  

## <a name="types-of-certificate-profile"></a>Types de profil de certificat  
 Vous pouvez créer trois types de profils de certificat dans System Center Configuration Manager :  

-   **Certificat d'Autorité de certification approuvé** : vous permet de déployer un certificat d'autorité de certification racine ou intermédiaire approuvé pour former une chaîne d'approbation des certificats lorsque l'appareil doit authentifier un serveur.  

-   **Protocole SCEP (Simple Certificate Enrollment Protocol)** : vous permet de demander un certificat pour un appareil ou un utilisateur à l’aide du protocole SCEP et du service d’inscription de périphérique réseau sur un serveur exécutant Windows Server 2012 R2.
-   -   **Échange d’informations personnelles (.pfx)** : vous permet de demander un certificat pour un appareil ou un utilisateur à l’aide du protocole SCEP et du service d’inscription de périphérique réseau sur un serveur exécutant Windows Server 2012 R2.

    > [!NOTE]  
    >  Vous devez créer un profil de certificat du type **Certificat d'Autorité de certification approuvé** avant de pouvoir créer un profil de certificat du type **Paramètres SCEP (Simple Certificate Enrollment Protocol)**.  

## <a name="requirements-and-supported-platforms"></a>Configuration requise et plates-formes prises en charge  
 Pour déployer des profils de certificat qui utilisent le protocole SCEP, vous devez installer le point d'enregistrement de certificat sur un serveur de système de site sur le site d'administration centrale ou sur un site principal. Vous devez également installer un module de stratégie pour le service d'inscription d'appareil réseau, le module de stratégie de Configuration Manager, sur un serveur exécutant Windows Server 2012 R2 avec le rôle de services de certificats Active Directory et un service d'inscription d'appareil réseau accessible aux appareils qui requièrent les certificats. Pour les appareils inscrits par Microsoft Intune, le service d’inscription de périphérique réseau doit être accessible sur Internet, par exemple, dans un sous-réseau filtré (également appelé DMZ).  

 Pour plus d’informations sur la façon dont le service d’inscription de périphérique réseau prend en charge un module de stratégie pour que System Center Configuration Manager puisse déployer des certificats, consultez [Using a Policy Module with the Network Device Enrollment Service (Utilisation d’un module de stratégie avec le service d’inscription de périphérique réseau)](http://go.microsoft.com/fwlink/p/?LinkId=328657).  

 System Center Configuration Manager prend en charge le déploiement des certificats sur des magasins de certificats différents, en fonction de la configuration requise, du type d’appareil et du système d’exploitation. Les appareils et les systèmes d'exploitation suivants sont pris en charge :  

-   Windows RT 8.1  

-   Windows 8.1  

-   Windows Phone 8.1  

-   Windows 10 Desktop et Mobile  

-   iOS  

-   Android  

> [!IMPORTANT]  
>  Pour déployer des profils sur des appareils Android, iOS, Windows Phone et sur des appareils Windows 8.1 ou version ultérieure inscrits, ces appareils doivent être inscrits dans Microsoft Intune. Pour plus d'informations sur la façon d'inscrire vos appareils, consultez [Gérer les appareils mobiles avec Microsoft Intune](https://technet.microsoft.com/en-us/library/dn646962.aspx).  

 Un scénario type pour System Center Configuration Manager consiste à installer des certificats d’autorité de certification racine approuvés pour authentifier des serveurs Wi-Fi et VPN lorsque la connexion utilise les protocoles d’authentification EAP-TLS, EAP-TTLS et PEAP, ainsi que les protocoles de tunneling IKEv2, L2TP/IPsec et Cisco IPsec VPN.  

 Vous devez vous assurer qu'un certificat d'autorité de certification racine d'entreprise est installé sur l'appareil avant que l'appareil puisse demander des certificats à l'aide d'un profil de certificat SCEP.  

 Vous pouvez spécifier divers paramètres dans un profil de certificat SCEP pour demander des certificats personnalisés pour différents environnements ou besoins en connectivité. L' **Assistant Créer un profil de certificat** comporte deux pages pour les paramètres d'inscription. La première, **Inscription SCEP**, contient les paramètres de la demande d'inscription et l'emplacement où installer le certificat. La seconde, **Propriétés du certificat**, décrit le certificat demandé.  

## <a name="deploying-certificate-profiles"></a>Déploiement de profils de certificat  
 Lorsque vous déployez un profil de certificat, les fichiers de certificat dans le profil sont installés sur des appareils clients. Tous les paramètres SCEP sont également déployés et les demandes SCEP sont traitées sur l'appareil client. Vous pouvez déployer des profils de certificat sur des regroupements d'utilisateurs ou d'appareils et spécifier la banque de destination pour chaque certificat. Les règles de mise en application déterminent si les certificats peuvent être installés sur l’appareil. Lors du déploiement de profils de certificat sur des regroupements d’utilisateurs, l’affinité entre appareil et utilisateur détermine quels appareils d’utilisateur installeront les certificats. Lors du déploiement de profils de certificat contenant des certificats d’utilisateur sur des regroupements d’appareils, par défaut, les certificats sont installés sur chacun des appareils d’utilisateur principaux. Vous pouvez modifier ce comportement pour installer le certificat sur l’un des appareils d’utilisateur dans la page **Inscription SCEP** de l’**Assistant Créer un profil de certificat**. En outre, les certificats d'utilisateur ne seront pas déployés sur les appareils s'il s'agit d'ordinateurs de groupe de travail.  

## <a name="monitoring-certificate-profiles"></a>Surveillance des profils de certificat  
 Vous pouvez surveiller les déploiements de profils de certificat à partir du nœud **Déploiements** de l’espace de travail **Surveillance** dans la console System Center Configuration Manager.  

 Vous pouvez également utiliser un des rapports de System Center Configuration Manager suivants pour surveiller des profils de certificat :  

-   **Historique des certificats émis par le point d'enregistrement de certificat**  

-   **Liste de biens par état d'émission de certificat pour les certificats inscrits par le point d'enregistrement de certificat**  

-   **Liste de biens dont la date d'expiration des certificats approche**  

## <a name="automatic-revocation-of-certificates"></a>Révocation automatique de certificats  
 System Center Configuration Manager révoque automatiquement les certificats utilisateur et ordinateur qui ont été déployés à l’aide de profils de certificat dans les circonstances suivantes :  

-   L’appareil est mis hors service depuis la gestion de System Center Configuration Manager.  

-   Une réinitialisation sélective est appliquée à l'appareil.  

-   L’appareil est bloqué depuis la hiérarchie System Center Configuration Manager.  

 Pour révoquer les certificats, le serveur de site envoie une commande de révocation à l'autorité de certification émettrice. Le motif de révocation est la **cessation de fonctionnement**.  



<!--HONumber=Dec16_HO3-->


