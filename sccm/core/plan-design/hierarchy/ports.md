---
title: Ports | System Center Configuration Manager
description: "Découvrez les ports requis et personnalisables qu’utilise System Center Configuration Manager pour les connexions."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c6777fb0-0754-4abf-8a1b-7639d23e9391
caps.latest.revision: 8
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 2e0ccf8cc419545abe8c87c8d9379618f13f47b1


---
# <a name="ports-used-in-system-center-configuration-manager"></a>Ports utilisés dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

System Center Configuration Manager est un système client/serveur distribué. Du fait de la nature distribuée de Configuration Manager, il est possible d’établir des connexions entre les serveurs de site, les systèmes de site et les clients. Certaines connexions utilisent des ports qui ne sont pas configurables et certaines prennent en charge des ports personnalisés que vous spécifiez. Si vous utilisez une technologie de filtrage de port, telle que des pare-feu, des routeurs, des serveurs proxy ou IPSec, vous devez vérifier que les ports requis sont disponibles.  

> [!NOTE]  
>  Si vous prenez en charge les clients Internet par pontage SSL, parallèlement aux exigences de port, vous devrez peut-être également autoriser certains verbes et en-têtes HTTP pour traverser le pare-feu. .  

 Les listes de ports ci-après sont utilisées par Configuration Manager et ne comportent aucune information relative aux services Windows standard, tels que les paramètres Stratégie de groupe pour les services de domaine Active Directory et l’authentification Kerberos. Pour plus d'informations sur les ports et les services de Windows Server, voir [Vue d'ensemble des services et exigences du port réseau pour le système Windows Server](http://go.microsoft.com/fwlink/p/?LinkID=123652).  

##  <a name="a-namebkmkconfigurableportsa-ports-you-can-configure"></a><a name="BKMK_ConfigurablePorts"></a> Ports configurables  
 Configuration Manager vous permet de configurer les ports pour les types de communication suivants :  

-   Point du site Web du catalogue des applications vers point de service Web du catalogue des applications  

-   Point proxy d'inscription vers point d'inscription  

-   Client vers systèmes de site exécutant IIS  

-   Client à Internet (sous forme de paramètres du serveur proxy)  

-   Point de mise à jour logicielle à Internet (sous forme de paramètres du serveur proxy)  

-   Point de mise à jour logicielle à serveur WSUS  

-   Serveur de site à serveur de base de données de site  

-   Points de Reporting Services  

    > [!NOTE]  
    >  Les ports utilisés pour le rôle de système de site du point de Reporting Services sont configurés dans SQL Server Reporting Services. Ces ports sont ensuite utilisés par Configuration Manager pendant les communications à destination du point de Reporting Services. Veillez à passer en revue ces ports qui définissent les informations de filtre IP pour les stratégies IPsec ou pour la configuration des pare-feu.  

Par défaut, le port HTTP utilisé pour la communication entre le client et le système de site est le port 80 et le port HTTPS par défaut est 443. Vous pouvez modifier les ports de communication entre le client et le système de site via HTTP ou HTTPS pendant l’installation ou dans les propriétés de votre site Configuration Manager.  

Les ports utilisés pour le rôle de système de site du point de Reporting Services sont configurés dans SQL Server Reporting Services. Ces ports sont ensuite utilisés par Configuration Manager pendant les communications à destination du point de Reporting Services. Veillez à passer en revue ces ports qui définissent les informations de filtre IP pour les stratégies IPsec ou pour la configuration des pare-feu.  

##  <a name="a-namebkmknonconfigurableportsa-non-configurable-ports"></a><a name="BKMK_NonConfigurablePorts"></a> Ports non configurables  
Configuration Manager ne vous autorise pas à configurer des ports pour les types de communication suivants :  

-   Site à site  

-   Serveur de site à système de site  

-   Console Configuration Manager vers le fournisseur SMS  

-   Console Configuration Manager vers Internet  

-   Connexions aux services cloud tels que Microsoft Intune et les points de distribution cloud  

##  <a name="a-namebkmkcommunicationportsa-ports-used-by-configuration-manager-clients-and-site-systems"></a><a name="BKMK_CommunicationPorts"></a> Ports utilisés par les clients Configuration Manager et les systèmes de site  
Les sections suivantes détaillent les ports utilisés pour la communication dans Configuration Manager. Les flèches dans le titre de section, entre les ordinateurs, représentent le sens de la communication :  

-   -- > indique qu'un ordinateur lance la communication et que l'autre ordinateur répond toujours  

-   &lt; -- > indique que les deux ordinateurs peuvent lancer la communication  

###  <a name="a-namebkmkportsaia-asset-intelligence-synchronization-point----microsoft"></a><a name="BKMK_PortsAI"></a> Point de synchronisation Asset Intelligence  -- &gt; Microsoft  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS (Secure Hypertext Transfer Protocol)|--|443|  

###  <a name="a-namebkmkportsai-to-sqla-asset-intelligence-synchronization-point----sql-server"></a><a name="BKMK_PortsAI-to-SQL"></a> Point de synchronisation Asset Intelligence --&gt; SQL Server  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|SQL sur TCP|--|1433 (Voir la remarque 2, **Port alternatif disponible**)|  

###  <a name="a-namebkmkportsappcatalogservice-sqla-application-catalog-web-service-point----sql-server"></a><a name="BKMK_PortsAppCatalogService-SQL"></a> Point de service Web du catalogue des applications --  SQL Server  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|SQL sur TCP|--|1433 (Voir la remarque 2, **Port alternatif disponible**)|  

###  <a name="a-namebkmkportsappcatalogwebsitepointappcatalogwebservicepointa-application-catalog-website-point----application-catalog-web-service-point"></a><a name="BKMK_PortsAppCatalogWebSitePoint_AppCatalogWebServicePoint"></a> Point du site Web du catalogue des applications -- &gt; Point de service Web du catalogue des applications  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP (Hypertext Transfer Protocol)|--|80 (Voir la remarque 2, **Port alternatif disponible**)|  
|HTTPS (Secure Hypertext Transfer Protocol)|--|443 (Voir la remarque 2, **Port alternatif disponible**)|  

###  <a name="a-namebkmkportsclient-appcatalogwebsitepointa-client----application-catalog-website-point"></a><a name="BKMK_PortsClient-AppCatalogWebsitePoint"></a> Client -- &gt; Point du site Web du catalogue des applications  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP (Hypertext Transfer Protocol)|--|80 (Voir la remarque 2, **Port alternatif disponible**)|  
|HTTPS (Secure Hypertext Transfer Protocol)|--|443 (Voir la remarque 2, **Port alternatif disponible**)|  

###  <a name="a-namebkmkportsclient-clientwakeupa-client----client"></a><a name="BKMK_PortsClient-ClientWakeUp"></a> Client -- &gt; Client  
 En plus des ports figurant dans le tableau ci-dessous, le proxy de mise en éveil utilise également des messages de demande d'écho ICMP (Internet Control Message Protocol) entre deux clients, lorsque ceux-ci sont configurés pour utiliser le proxy de mise en éveil. Cette communication permet de savoir si l'autre ordinateur client est en éveil sur le réseau. ICMP est parfois appelé commandes ping TCP/IP. ICMP ne dispose pas d'un numéro de protocole UDP ou TCP, et par conséquent, il ne figure pas dans le tableau suivant. Toutefois, les pare-feu d'hôte de ces ordinateurs clients ou les appareils réseau intervenant sur le sous-réseau doivent autoriser le trafic ICMP pour que la communication avec le proxy de mise en éveil aboutisse.  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|Éveil par appel réseau|9 (Voir la remarque 2, **Port alternatif disponible**)|--|  
|Proxy de mise en éveil|25536 (Voir la remarque 2, **Port alternatif disponible**)|--|  

###  <a name="a-namebkmkportsclient-policymodulea-client----configuration-manager-policy-module-network-device-enrollment-service"></a><a name="BKMK_PortsClient-PolicyModule"></a> Client --&gt; Module de stratégie de Configuration Manager (service d'inscription d'appareils réseau)  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP (Hypertext Transfer Protocol)||80|  
|HTTPS (Secure Hypertext Transfer Protocol)|--|443|  

###  <a name="a-namebkmkportsclient-clouddpa-client----cloud-based-distribution-point"></a><a name="BKMK_PortsClient-CloudDP"></a> Client -- &gt; Point de distribution cloud  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS (Secure Hypertext Transfer Protocol)|--|443|  

###  <a name="a-namebkmkportsclient-dpa-client----distribution-point"></a><a name="BKMK_PortsClient-DP"></a> Client -- &gt; Point de distribution  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP (Hypertext Transfer Protocol)|--|80 (Voir la remarque 2, **Port alternatif disponible**)|  
|HTTPS (Secure Hypertext Transfer Protocol)|--|443 (Voir la remarque 2, **Port alternatif disponible**)|  

###  <a name="a-namebkmkportsclient-dp2a-client----distribution-point-configured-for-multicast"></a><a name="BKMK_PortsClient-DP2"></a> Client -- &gt; Point de distribution configuré pour la multidiffusion  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|SMB (Server Message Block)|--|445|  
|Protocole de multidiffusion|63000-64000|--|  

###  <a name="a-namebkmkportsclient-dp3a-client----distribution-point-configured-for-pxe"></a><a name="BKMK_PortsClient-DP3"></a> Client -- &gt; Point de distribution configuré pour PXE  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|DHCP (Dynamic Host Configuration Protocol)|67 et 68|--|  
|TFTP (Trivial File Transfer Protocol)|69 (Voir remarque 4, **Trivial FTP (TFTP) Daemon**)|--|  
|BINL (Boot Information Negotiation Layer)|4011|--|  

###  <a name="a-namebkmkportsclient-fspa-client----fallback-status-point"></a><a name="BKMK_PortsClient-FSP"></a> Client -- &gt; Point d'état de secours  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP (Hypertext Transfer Protocol)|--|80 (Voir la remarque 2, **Port alternatif disponible**)|  

###  <a name="a-namebkmkportsclient-gcdca-client----global-catalog-domain-controller"></a><a name="BKMK_PortsClient-GCDC"></a> Client -- &gt; Contrôleur de domaine de catalogue global  
 Un client Configuration Manager ne contacte pas de serveur de catalogue global lorsqu'il s'agit d'un ordinateur d'un groupe de travail ou lorsqu'il est configuré pour les communications Internet uniquement.  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|LDAP de catalogue global|--|3268|  
|SSL LDAP de catalogue global|--|3269|  

###  <a name="a-namebkmkportsclient-mpa-client----management-point"></a><a name="BKMK_PortsClient-MP"></a> Client -- &gt; Point de gestion  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|Notification du client (communication par défaut avant le basculement en HTTP ou HTTPS)|--|10123 (Voir la remarque 2, **Port alternatif disponible**)|  
|HTTP (Hypertext Transfer Protocol)|--|80 (Voir la remarque 2, **Port alternatif disponible**)|  
|HTTPS (Secure Hypertext Transfer Protocol)|--|443 (Voir la remarque 2, **Port alternatif disponible**)|  

###  <a name="a-namebkmkportsclient-supa-client----software-update-point"></a><a name="BKMK_PortsClient-SUP"></a> Client -- &gt; Point de mise à jour logicielle  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP (Hypertext Transfer Protocol)|--|80 ou 8530 (Voir la remarque 3, **Windows Server Update Services**)|  
|HTTPS (Secure Hypertext Transfer Protocol)|--|443 ou 8531 (Voir la remarque 3, **Windows Server Update Services**)|  

###  <a name="a-namebkmkportsclient-smpa-client----state-migration-point"></a><a name="BKMK_PortsClient-SMP"></a> Client -- &gt; Point de migration de l'état  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP (Hypertext Transfer Protocol)|--|80 (Voir la remarque 2, **Port alternatif disponible**)|  
|HTTPS (Secure Hypertext Transfer Protocol)|--|443 (Voir la remarque 2, **Port alternatif disponible**)|  
|SMB (Server Message Block)|--|445|  

###  <a name="a-namebkmkportsconsole-clienta-configuration-manager-console----client"></a><a name="BKMK_PortsConsole-Client"></a> Console Configuration Manager -- &gt; Client  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|Contrôle à distance (contrôle)|--|2701|  
|Assistance à distance (RDP et RTC)|--|3389|  

###  <a name="a-namebkmkportsconsole-interneta-configuration-manager-console----internet"></a><a name="BKMK_PortsConsole-Internet"></a> Console Configuration Manager --&gt; Internet  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP (Hypertext Transfer Protocol)|--|80|  

###  <a name="a-namebkmkportsconsole-rspa-configuration-manager-console----reporting-services-point"></a><a name="BKMK_PortsConsole-RSP"></a> Console Configuration Manager -- &gt; Point Reporting Services  

||||  
|-|-|-|  
|Description|UDP|TCP|  
|HTTP (Hypertext Transfer Protocol)|--|80 (Voir la remarque 2, **Port alternatif disponible**)|  
|HTTPS (Secure Hypertext Transfer Protocol)|--|443 (Voir la remarque 2, **Port alternatif disponible**)|  

###  <a name="a-namebkmkportsconsole-sitea-configuration-manager-console----site-server"></a><a name="BKMK_PortsConsole-Site"></a> Console Configuration Manager -- &gt; Serveur de site  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|RPC (connexion initiale à WMI pour localiser le système fournisseur)|--|135|  

###  <a name="a-namebkmkportsconsole-providera-configuration-manager-console----sms-provider"></a><a name="BKMK_PortsConsole-Provider"></a> Console Configuration Manager --&gt;  Fournisseur SMS  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|Mappeur de point de terminaison RPC|135|135|  
|RPC|--|DYNAMIQUE (voir la note 6, **Ports dynamiques**)|  

###  <a name="a-namebkmkportscertificateregistationpointpolicymodulea-configuration-manager-policy-module-network-device-enrollment-service----certificate-registration-point"></a><a name="BKMK_PortsCertificateRegistationPoint_PolicyModule"></a> Module de stratégie de Configuration Manager (service d'inscription d'appareils réseau)--&gt; Point d'enregistrement de certificat  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS (Secure Hypertext Transfer Protocol)|--|443 (Voir la remarque 2, **Port alternatif disponible**)|  

###  <a name="a-namebkmkportsdistmpa-distribution-point----management-point"></a><a name="BKMK_PortsDist_MP"></a> Point de distribution --&gt; Point de gestion  
 Un point de distribution communique avec le point de gestion dans les scénarios suivants :  

-   Pour signaler l'état du contenu préparé  

-   Pour signaler les données de synthèse d'utilisation  

-   Pour signaler la validation du contenu  

-   Un point de distribution d'extraction signale l'état du téléchargement de package  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP (Hypertext Transfer Protocol)|--|80 (Voir la remarque 2, **Port alternatif disponible**)|  
|HTTPS (Secure Hypertext Transfer Protocol)|--|443 (Voir la remarque 2, **Port alternatif disponible**)|  

###  <a name="a-namebkmkportsendpointprotectioninterneta-endpoint-protection-point----internet"></a><a name="BKMK_PortsEndpointProtection_Internet"></a> Point Endpoint Protection -- &gt; Internet  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP (Hypertext Transfer Protocol)|--|80|  

###  <a name="a-namebkmkportsep-to-sqla-endpoint-protection-point----sql-server"></a><a name="BKMK_PortsEP-to-SQL"></a> Point de protection de point de terminaison --&gt; SQL Server  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|SQL sur TCP|--|1433 (Voir la remarque 2, **Port alternatif disponible**)|  

###  <a name="a-namebkmkportsenrollmentproxyenrollmentpointa-enrollment-proxy-point----enrollment-point"></a><a name="BKMK_PortsEnrollmentProxyEnrollmentPoint"></a> Point proxy d'inscription -- &gt; Point d'inscription  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS (Secure Hypertext Transfer Protocol)|--|443 (Voir la remarque 2, **Port alternatif disponible**)|  

###  <a name="a-namebkmkportsenrollmentenrollmentsqla-enrollment-point----sql-server"></a><a name="BKMK_PortsEnrollmentEnrollmentSQL"></a> Point d'inscription -- &gt; SQL Server  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|SQL sur TCP|--|1433 (Voir la remarque 2, **Port alternatif disponible**)|  

###  <a name="a-namebkmkportsexchangeconnectorhosteda-exchange-server-connector----exchange-online"></a><a name="BKMK_PortsExchangeConnectorHosted"></a> Connecteur du serveur Exchange Server -- &gt; Exchange Online  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|Gestion à distance de Windows via HTTPS|--|5986|  

###  <a name="a-namebkmkportsexchangeconnectoronprema-exchange-server-connector----on-premises-exchange-server"></a><a name="BKMK_PortsExchangeConnectorOnPrem"></a> Connecteur du serveur Exchange Server -- &gt; Serveur Exchange Server sur site  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|Gestion à distance de Windows via HTTP|--|5985|  

###  <a name="a-namebkmkportsmacenrollmentproxypointa-mac-computer----enrollment-proxy-point"></a><a name="BKMK_PortsMacEnrollmentProxyPoint"></a> Ordinateur Mac -- &gt; Point proxy d'inscription  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS (Secure Hypertext Transfer Protocol)|--|443|  

###  <a name="a-namebkmkportsmp-dca-management-point----domain-controller"></a><a name="BKMK_PortsMP-DC"></a> Point de gestion -- &gt; Contrôleur de domaine  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|LDAP (Lightweight Directory Access Protocol)|--|389|  
|LDAP (connexion SSL [Secure Sockets Layer])|636|636|  
|LDAP de catalogue global|--|3268|  
|SSL LDAP de catalogue global|--|3269|  
|Mappeur de point de terminaison RPC|135|135|  
|RPC|--|DYNAMIQUE (voir la note 6, **Ports dynamiques**)|  

###  <a name="a-namebkmkportsmp-sitea-management-point-lt----site-server"></a><a name="BKMK_PortsMP-Site"></a> Point de gestion &lt; -- > Serveur de site  
 (Voir remarque 5, **Communications entre le serveur de site et les systèmes de site**)  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|Mappeur de point de terminaison RPC|--|135|  
|RPC|--|DYNAMIQUE (voir la note 6, **Ports dynamiques**)|  
|SMB (Server Message Block)|--|445|  

###  <a name="a-namebkmkportsmp-sqla-management-point----sql-server"></a><a name="BKMK_PortsMP-SQL"></a> Point de gestion -- &gt; SQL Server  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|SQL sur TCP|--|1433 (Voir la remarque 2, **Port alternatif disponible**)|  

###  <a name="a-namebkmkportsmobiledeviceclient-enrollmentproxypointa-mobile-device----enrollment-proxy-point"></a><a name="BKMK_PortsMobileDeviceClient-EnrollmentProxyPoint"></a> Appareil mobile -- &gt; Point proxy d'inscription  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS (Secure Hypertext Transfer Protocol)|--|443|  

###  <a name="a-namebkmkportsmobiledeviceclient-windowsintunea-mobile-device----microsoft-intune"></a><a name="BKMK_PortsMobileDeviceClient-WindowsIntune"></a> Appareil mobile --&gt; Microsoft Intune  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS (Secure Hypertext Transfer Protocol)|--|443|  

###  <a name="a-namebkmkportsrsp-sqla-reporting-services-point----sql-server"></a><a name="BKMK_PortsRSP-SQL"></a> Point de Reporting Services -- &gt; SQL Server  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|SQL sur TCP|--|1433 (Voir remarque 2, Port alternatif disponible)|  

###  <a name="a-namebkmkportsintuneconnector-windowsintunea-service-connection-point----microsoft-intune"></a><a name="BKMK_PortsIntuneConnector-WindowsIntune"></a> Point de connexion de service --&gt; Microsoft Intune  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS (Secure Hypertext Transfer Protocol)|--|443|
Pour plus d’informations, consultez [Conditions requises pour l’accès Internet](/sccm/core/servers/deploy/configure/about-the-service-connection-point#bkmk_urls) pour le point de connexion de service.

###  <a name="a-namebkmkportsappcatalogwebservicepointsiteservera-site-server-lt----application-catalog-web-service-point"></a><a name="BKMK_PortsAppCatalogWebServicePoint_SiteServer"></a> Serveur de site &lt; -- > Point de service web du catalogue des applications  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|SMB (Server Message Block)|--|445|  
|Mappeur de point de terminaison RPC|135|135|  
|RPC|--|DYNAMIQUE (voir la note 6, **Ports dynamiques**)|  

###  <a name="a-namebkmkportsappcatalogwebsitepointsiteservera-site-server-lt----application-catalog-website-point"></a><a name="BKMK_PortsAppCatalogWebSitePoint_SiteServer"></a> Serveur de site &lt; -- > Point du site web du catalogue des applications  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|SMB (Server Message Block)|--|445|  
|Mappeur de point de terminaison RPC|135|135|  
|RPC|--|DYNAMIQUE (voir la note 6, **Ports dynamiques**)|  

###  <a name="a-namebkmkportssite-aispa-site-server-lt----asset-intelligence-synchronization-point"></a><a name="BKMK_PortsSite-AISP"></a> Serveur de site &lt; -- > Point de synchronisation Asset Intelligence  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|SMB (Server Message Block)|--|445|  
|Mappeur de point de terminaison RPC|135|135|  
|RPC|--|DYNAMIQUE (voir la note 6, **Ports dynamiques**)|  

###  <a name="a-namebkmkportssite-clienta-site-server----client"></a><a name="BKMK_PortsSite-Client"></a> Serveur de site -- &gt; Client  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|Éveil par appel réseau|9 (Voir la remarque 2, **Port alternatif disponible**)|--|  

###  <a name="a-namebkmkportssiteserver-clouddpa-site-server----cloud-based-distribution-point"></a><a name="BKMK_PortsSiteServer-CloudDP"></a> Serveur de site -- &gt; Point de distribution cloud  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS (Secure Hypertext Transfer Protocol)|--|443|  

###  <a name="a-namebkmkportssite-dpa-site-server----distribution-point"></a><a name="BKMK_PortsSite-DP"></a> Serveur de site -- &gt; Point de distribution  
 (Voir remarque 5, **Communications entre le serveur de site et les systèmes de site**)  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|SMB (Server Message Block)|--|445|  
|Mappeur de point de terminaison RPC|135|135|  
|RPC|--|DYNAMIQUE (voir la note 6, **Ports dynamiques**)|  

###  <a name="a-namebkmkportssite-dca-site-server----domain-controller"></a><a name="BKMK_PortsSite-DC"></a> Serveur de site -- &gt; Contrôleur de domaine  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|LDAP (Lightweight Directory Access Protocol)|--|389|  
|LDAP (connexion SSL [Secure Sockets Layer])|636|636|  
|LDAP de catalogue global|--|3268|  
|SSL LDAP de catalogue global|--|3269|  
|Mappeur de point de terminaison RPC|135|135|  
|RPC|--|DYNAMIQUE (voir la note 6, **Ports dynamiques**)|  

###  <a name="a-namebkmkportscertificateregistrationpointsiteservera-site-server-lt----certificate-registration-point"></a><a name="BKMK_PortsCertificateRegistrationPoint_SiteServer"></a> Serveur de site &lt; -- > Point d’enregistrement de certificat  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|SMB (Server Message Block)|--|445|  
|Mappeur de point de terminaison RPC|135|135|  
|RPC|--|DYNAMIQUE (voir la note 6, **Ports dynamiques**)|  

###  <a name="a-namebkmkportsendpointprotectionsiteservera-site-server-lt----endpoint-protection-point"></a><a name="BKMK_PortsEndpointProtection_SiteServer"></a> Serveur de site &lt; -- > Point Endpoint Protection  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|SMB (Server Message Block)|--|445|  
|Mappeur de point de terminaison RPC|135|135|  
|RPC|--|DYNAMIQUE (voir la note 6, **Ports dynamiques**)|  

###  <a name="a-namebkmkenrollmentpointsiteservera-site-server-lt----enrollment-point"></a><a name="BKMK_EnrollmentPoint_SiteServer"></a> Serveur de site &lt; -- > Point d’inscription  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|SMB (Server Message Block)|--|445|  
|Mappeur de point de terminaison RPC|135|135|  
|RPC|--|DYNAMIQUE (voir la note 6, **Ports dynamiques**)|  

###  <a name="a-namebkmkenrollmentproxypointsiteservera-site-server-lt----enrollment-proxy-point"></a><a name="BKMK_EnrollmentProxyPoint_SiteServer"></a> Serveur de site &lt; -- > Point proxy d’inscription  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|SMB (Server Message Block)|--|445|  
|Mappeur de point de terminaison RPC|135|135|  
|RPC|--|DYNAMIQUE (voir la note 6, **Ports dynamiques**)|  

###  <a name="a-namebkmkportssite-fspa-site-server-lt----fallback-status-point"></a><a name="BKMK_PortsSite-FSP"></a> Serveur de site &lt; -- > Point d’état de secours  
 (Voir remarque 5, **Communications entre le serveur de site et les systèmes de site**)  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|SMB (Server Message Block)|--|445|  
|Mappeur de point de terminaison RPC|135|135|  
|RPC|--|DYNAMIQUE (voir la note 6, **Ports dynamiques**)|  

###  <a name="a-namebkmkportsite-interneta-site-server----internet"></a><a name="BKMK_PortSite-Internet"></a> Serveur de site -- &gt; Internet  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP (Hypertext Transfer Protocol)|--|80 (Voir remarque 1, **Port de serveur proxy**)|  

###  <a name="a-namebkmkportsissuingcasiteservera-site-server-lt----issuing-certification-authority-ca"></a><a name="BKMK_PortsIssuingCA_SiteServer"></a> Serveur de site &lt; -- > Autorité de certification (AC) émettrice  
 Cette communication est utilisée lorsque vous déployez des profils de certificat à l'aide du point d'enregistrement de certificat. La communication n'est pas utilisée pour chaque serveur de site de la hiérarchie ; Il est utilisé uniquement pour le serveur de site en haut de la hiérarchie.  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|Mappeur de point de terminaison RPC|135|135|  
|RPC (DCOM)|--|DYNAMIQUE (voir la note 6, **Ports dynamiques**)|  

###  <a name="a-namebkmkportssite-rspa-site-server-lt----reporting-services-point"></a><a name="BKMK_PortsSite-RSP"></a> Serveur de site &lt; -- > Point de Reporting Services  
 (Voir remarque 5, **Communications entre le serveur de site et les systèmes de site**)  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|SMB (Server Message Block)|--|445|  
|Mappeur de point de terminaison RPC|135|135|  
|RPC|--|DYNAMIQUE (voir la note 6, **Ports dynamiques**)|  

###  <a name="a-namebkmkportssite-sitea-site-server-lt----site-server"></a><a name="BKMK_PortsSite-Site"></a> Serveur de site &lt; -- > Serveur de site  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|SMB (Server Message Block)|--|445|  

###  <a name="a-namebkmkportssite-sqla-site-server----sql-server"></a><a name="BKMK_PortsSite-SQL"></a> Serveur de site -- &gt; SQL Server  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|SQL sur TCP|--|1433 (Voir la remarque 2, **Port alternatif disponible**)|  

 Lors de l'installation d'un site qui utilisera une instance distante de SQL Server pour héberger la base de données de site, vous devez ouvrir les ports suivants entre le serveur de site et l'instance de SQL Server :  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|SMB (Server Message Block)|--|445|  
|Mappeur de point de terminaison RPC|135|135|  
|RPC|--|DYNAMIQUE (voir la note 6, **Ports dynamiques**)|  

###  <a name="a-namebkmkportssite-providera-site-server----sms-provider"></a><a name="BKMK_PortsSite-Provider"></a> Serveur de site -- &gt; Fournisseur SMS  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|SMB (Server Message Block)|--|445|  
|Mappeur de point de terminaison RPC|135|135|  
|RPC|--|DYNAMIQUE (voir la note 6, **Ports dynamiques**)|  

###  <a name="a-namebkmkportssite-supa-site-server-lt----software-update-point"></a><a name="BKMK_PortsSite-SUP"></a> Serveur de site &lt; -- > Point de mise à jour logicielle  
 (Voir remarque 5, **Communications entre le serveur de site et les systèmes de site**)  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|SMB (Server Message Block)|--|445|  
|HTTP (Hypertext Transfer Protocol)|--|80 ou 8530 (Voir remarque 3, Windows Server Update Services)|  
|HTTPS (Secure Hypertext Transfer Protocol)|--|443 ou 8531 (Voir la remarque 3, Windows Server Update Services)|  

###  <a name="a-namebkmkportssite-smpa-site-server-lt----state-migration-point"></a><a name="BKMK_PortsSite-SMP"></a> Serveur de site &lt; -- > Point de migration d’état  
 (Voir remarque 5, **Communications entre le serveur de site et les systèmes de site**)  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|SMB (Server Message Block)|--|445|  
|Mappeur de point de terminaison RPC|135|135|  

###  <a name="a-namebkmkportsprovider-sqla-sms-provider----sql-server"></a><a name="BKMK_PortsProvider-SQL"></a> Fournisseur SMS -- &gt; SQL Server  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|SQL sur TCP|--|1433 (Voir remarque 2, Port alternatif disponible)|  

###  <a name="a-namebkmkportssup-interneta-software-update-point----internet"></a><a name="BKMK_PortsSUP-Internet"></a> Point de mise à jour logicielle -- &gt; Internet  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP (Hypertext Transfer Protocol)|--|80 (Voir remarque 1, **Port de serveur proxy**)|  

###  <a name="a-namebkmkportssup-wsusa-software-update-point----upstream-wsus-server"></a><a name="BKMK_PortsSUP-WSUS"></a> Point de mise à jour logicielle -- &gt; Serveur WSUS en amont  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP (Hypertext Transfer Protocol)|--|80 ou 8530 (Voir la remarque 3, **Windows Server Update Services**)|  
|HTTPS (Secure Hypertext Transfer Protocol)|--|443 ou 8531 (Voir la remarque 3, **Windows Server Update Services**)|  

###  <a name="a-namebkmkportssql-sqla-sql-server----sql-server"></a><a name="BKMK_PortsSQL-SQL"></a> SQL Server --&gt; SQL Server  
 La réplication intersite de base de données requiert que le serveur SQL Server d'un site communique directement avec le serveur SQL Server de son site parent ou enfant.  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|Service SQL Server|--|1433 (Voir remarque 2, Port alternatif disponible)|  
|Service Broker SQL Server|--|4022 (Voir la remarque 2, Port alternatif disponible)|  

> [!TIP]  
>  Configuration Manager ne nécessite pas le navigateur SQL Server, qui utilise le port UDP 1434.  

###  <a name="a-namebkmkportsstatemigrationpoint-to-sqla-state-migration-point----sql-server"></a><a name="BKMK_PortsStateMigrationPoint-to-SQL"></a> Point de migration d'état --&gt; SQL Server  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|SQL sur TCP|--|1433 (Voir la remarque 2, **Port alternatif disponible**)|  



###  <a name="a-namebkmyportnotesa-notes-for-ports-used-by-configuration-manager-clients-and-site-systems"></a><a name="BKMY_PortNotes"></a> Notes pour les ports utilisés par les clients Configuration Manager et les systèmes de site  

1.  **Port de serveur proxy**: ce port ne peut pas être configuré, mais il peut être routé par le biais d’un serveur proxy configuré.  

2.  **Port alternatif disponible** : un port différent peut être défini dans Configuration Manager pour cette valeur. Si un port personnalisé a été défini, remplacez-le lorsque vous définissez les informations de filtre IP pour les stratégies IPsec ou pour configurer les pare-feu.  

3.  **Windows Server Update Services**: WSUS peut être installé sur le site web par défaut (port 80) ou sur un site web personnalisé (port 8530).  

     Ce port peut être modifié après l'installation. Vous n'avez pas à utiliser le même numéro de port dans l'ensemble de la hiérarchie du site.  

    -   Si le numéro de port HTTP est 80, le numéro de port HTTPS doit être 443.  

    -   S’il s’agit d’un autre numéro de port HTTP, le numéro de port HTTPS doit être supérieur de 1 (par exemple, 8530 et 8531).  

    > [!NOTE]  
    >  Quand vous configurez le point de mise à jour logicielle pour utiliser HTTPS, le port HTTP doit également être ouvert. Les données non chiffrées, telles que le CLUF pour les mises à jour spécifiques, utilisent le port HTTP.  

4.  **Trivial FTP (TFTP) Daemon**: le Service Trivial FTP ne nécessite pas de nom d’utilisateur ou de mot de passe et il fait partie intégrante des Services de déploiement Windows (WDS). Le Service Trivial FTP met en œuvre la prise en charge du protocole TFTP défini par les normes RFC suivantes :  

    -   RFC 350 - TFTP  

    -   RFC 2347 - Extension d’option  

    -   RFC 2348 - Option de taille de bloc  

    -   RFC 2349 - Options d’intervalle de délai d’attente et de taille de transfert  

     Le protocole Trivial FTP est conçu pour prendre en charge les environnements de démarrage sans disque. Les services Trivial FTP écoutent au port UDP 69 mais répondent à partir d'un port à numéro élevé alloué de manière dynamique. Ainsi, l'activation de ce port permettra au service TFTP de recevoir les requêtes TFTP entrantes mais n'autorisera pas le serveur sélectionné à répondre à ces requêtes. Il n'est pas possible de permettre au serveur sélectionné de répondre aux requêtes TFTP si le serveur TFTP n'est pas configuré de manière à répondre à partir du port 69.  

5.  **Communications entre le serveur de site et les systèmes de site**: par défaut, les communications entre le serveur de site et les systèmes de site sont bidirectionnelles. Le serveur de site initialise la communication pour configurer le système de site, puis la plupart des systèmes de site se connectent à leur tour au serveur de site pour envoyer des informations d'état. Les points de Reporting Services et les points de distribution n'envoient pas d'informations d'état. Si vous sélectionnez **Exiger que le serveur de site établisse des connexions vers ce système de site** dans les propriétés du système de site, après son installation, ce dernier n'établira pas de communication vers le système de site. Au lieu de cela, le serveur de site établit les connexions et utilise le compte d'installation du système de site pour l'authentification au niveau du serveur de système de site.  

6.  **Ports dynamiques**: les ports dynamiques (également appelés ports éphémères) utilisent une plage de numéros de port qui est définie par la version du système d’exploitation. Pour plus d'informations sur les plages de port par défaut, voir [Vue d'ensemble des services et exigences de ports réseau pour le système Windows Server](http://go.microsoft.com/fwlink/p/?LinkId=317965).  

##  <a name="a-namebkmkadditionalportsa-additional-lists-of-ports"></a><a name="BKMK_AdditionalPorts"></a> Listes de ports supplémentaires  
 Les sections suivantes fournissent des informations supplémentaires sur les ports utilisés par Configuration Manager.  

###  <a name="a-namebkmkclientsharesa-client-to-server-shares"></a><a name="BKMK_ClientShares"></a> Client vers partages serveur  
 Les clients utilisent le protocole SMB (Server Message Block) à chaque fois qu'ils se connectent à des partages UNC. Exemple :  

-   Installation de client manuelle spécifiant la propriété de ligne de commande CCMSetup.exe **/source:** .  

-   Clients Endpoint Protection téléchargeant des fichiers de définition à partir d'un chemin UNC.  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|SMB (Server Message Block)|--|445|  

###  <a name="a-namebkmksqlportsa-connections-to-microsoft-sql-server"></a><a name="BKMK_SQLPorts"></a> Connexions à Microsoft SQL Server  
 Pour la communication vers le moteur de base de données SQL Server et pour la réplication intersite, vous pouvez utiliser le port de SQL Server par défaut ou spécifier des ports personnalisés :  

-   Utilisation des communications intersites :  

    -   SQL Server Service Broker, qui utilise par défaut le port TCP 4022.  

    -   Service SQL Server, qui utilise par défaut le port TCP 1433.  

-   Les communications intrasites entre le moteur de base de données SQL Server et divers rôles de systèmes de site Configuration Manager utilisent par défaut le port TCP 1433.  

> [!WARNING]  
>  Configuration Manager ne prend pas en charge les ports dynamiques. Étant donné que les instances nommées de SQL Server utilisent par défaut des ports dynamiques pour les connexions au moteur de base de données, lorsque vous utilisez une instance nommée, vous devez configurer manuellement le port statique que vous souhaitez utiliser pour la communication intrasite.  

 Les rôles de système de site suivants communiquent directement avec la base de données SQL Server :  

-   Point de service Web du catalogue des applications  

-   Rôle de point d'enregistrement de certificat  

-   Rôle de point d'inscription  

-   Point de gestion  

-   Serveur de site  

-   Point de Reporting Services  

-   fournisseur SMS  

-   SQL Server --> SQL Server  

Lorsqu'un SQL Server héberge une base de données provenant de plusieurs sites, chaque base de données doit utiliser une instance distincte de SQL Server, et chaque instance doit être configurée avec un ensemble de ports unique.  

Si un pare-feu est activé sur l'ordinateur SQL Server, assurez-vous qu'il est configuré pour autoriser les ports utilisés par votre déploiement et, pour tous les emplacements du réseau, entre les ordinateurs qui communiquent avec le serveur SQL Server.  

Si vous souhaitez voir un exemple illustrant comment configurer SQL Server pour utiliser un port spécifique, consultez [Configurer un serveur pour écouter un port TCP spécifique (Gestionnaire de configuration SQL Server)](http://go.microsoft.com/fwlink/p/?LinkID=226349) dans la bibliothèque TechNet relative à SQL Server.  


### <a name="bkmk_discovery"> </a> Découverte et publication
Les ports suivants sont utilisés pour la découverte et la publication d’informations de site :
 - LDAP (Lightweight Directory Access Protocol) - 389
 - LDAP (connexion SSL [Secure Sockets Layer]) - 636


 - LDAP de catalogue global - 3268
 - SSL LDAP de catalogue global - 3269


 - Mappeur de point de terminaison RPC - 135
 - RPC - Ports TCP à numéro élevé alloués dynamiquement


 - TCP : 1024 - 5000
 - TCP : 49152 - 65535


###  <a name="a-namebkmkexternala-external-connections-made-by-configuration-manager"></a><a name="BKMK_External"></a> Connexions externes effectuées par Configuration Manager  
 Les clients ou les systèmes de site Configuration Manager peuvent établir les connexions externes suivantes :  

-   [Point de synchronisation Asset Intelligence -- &gt; Microsoft](#BKMK_PortsAI)  

-   [Point Endpoint Protection -- &gt; Internet](#BKMK_PortsEndpointProtection_Internet)  

-   [Client -- &gt; Contrôleur de domaine de catalogue global](#BKMK_PortsClient-GCDC)  

-   [Console Configuration Manager -- &gt; Internet](#BKMK_PortsConsole-Internet)  

-   [Point de gestion -- &gt; Contrôleur de domaine](#BKMK_PortsMP-DC)  

-   [Serveur de site -- &gt; Contrôleur de domaine](#BKMK_PortsSite-DC)  

-   [Serveur de site &lt; -- &gt; Autorité de certification (CA) émettrice](#BKMK_PortsIssuingCA_SiteServer)  

-   [Point de mise à jour logicielle -- &gt; Internet](#BKMK_PortsSUP-Internet)  

-   [Point de mise à jour logicielle -- &gt; Serveur WSUS en amont](#BKMK_PortsSUP-WSUS)  

-   [Point de connexion de service -- &gt; Microsoft Intune](#BKMK_PortsIntuneConnector-WindowsIntune)  

###  <a name="a-namebkmkibcmportsa-installation-requirements-for-site-systems-that-support-internet-based-clients"></a><a name="BKMK_IBCMports"></a> Configuration requise pour les systèmes de site qui prennent en charge les clients Internet  
 Les points de gestion et les points de distribution qui prennent en charge les clients Internet, le point de mise à jour de logiciels et le point d'état de secours utilisent les ports suivants pour l'installation et la réparation :  

-   Serveur de site --> système de site : mappeur de point de terminaison RPC à l’aide du port UDP et du port TCP 135.  

-   Serveur de site --> système de site : ports TCP RPC dynamiques.  

-   Serveur de site &lt; --> système de site : protocole SMB (Server Message Blocks) utilisant le port TCP 445.  

Les installations d'applications et de packages sur les points de distribution nécessitent les ports RPC suivants :  

-   Serveur de site --> point de distribution : mappeur de point de terminaison RPC à l’aide du port UDP et du port TCP 135.  

-   Serveur de site --> point de distribution : ports TCP RPC dynamiques  

Utilisez IPsec pour sécuriser le trafic entre le serveur de site et les systèmes de site. Si vous devez restreindre les ports dynamiques utilisés par RPC, vous pouvez employer l'outil de configuration Microsoft RPC (rpccfg.exe) pour configurer une plage de ports limitée à ces paquets RPC. Pour plus d'informations sur l'outil de configuration RPC, voir [Comment configurer RPC pour qu'il utilise certains ports et comment sécuriser ces ports à l'aide d'IPsec](http://go.microsoft.com/fwlink/p/?LinkId=124096).  

> [!IMPORTANT]  
>  Avant d'installer ces systèmes de site, vérifiez que le service d'accès à distance au Registre est en cours d'exécution sur le serveur de système de site et que vous avez spécifié un compte d'installation du système de site si le système de site est situé dans une autre forêt Active Directory sans relation d'approbation.  

###  <a name="a-namebkmkportsclientinstalla-ports-used-by-configuration-manager-client-installation"></a><a name="BKMK_PortsClientInstall"></a> Ports utilisés par l’installation du client Configuration Manager  
Les ports utilisés lors de l'installation du client dépendent de la méthode de déploiement du client. Consultez **Ports utilisés lors du déploiement du client Configuration Manager** dans la rubrique [Paramètres de port et de pare-feu Windows pour les clients dans System Center Configuration Manager](../../../core/clients/deploy/windows-firewall-and-port-settings-for-clients.md) pour obtenir la liste des ports utilisés pour chaque méthode de déploiement de client. Pour plus d’informations sur la configuration du Pare-feu Windows sur le client pour l’installation du client et la communication après l’installation, consultez [Paramètres de port et de pare-feu Windows pour les clients dans System Center Configuration Manager](../../../core/clients/deploy/windows-firewall-and-port-settings-for-clients.md).  

###  <a name="a-namebkmkmigrationportsa-ports-used-by-migration"></a><a name="BKMK_MigrationPorts"></a> Ports utilisés par la migration  
Le serveur de site qui exécute la migration utilise plusieurs ports pour se connecter aux sites applicables dans la hiérarchie source, pour recueillir des données à partir de la base de données SQL Server des sites sources et partager des points de distribution.  

 Pour plus d’informations sur ces ports, consultez [Configurations requises pour la migration](../../../core/migration/prerequisites-for-migration.md#BKMK_Required_Configurations) dans la section Prérequis de la rubrique [Prérequis de la migration dans System Center Configuration Manager](../../../core/migration/prerequisites-for-migration.md).  

###  <a name="a-namebkmkserverportsa-ports-used-by-windows-server"></a><a name="BKMK_ServerPorts"></a> Ports utilisés par Windows Server  
 Le tableau suivant répertorie certains des principaux ports utilisés par Windows Server, ainsi que leur fonction respective. Pour une liste plus complète des services Windows Server et les exigences des ports réseau, voir [Vue d'ensemble des services et exigences du port réseau pour le système Windows Server](http://go.microsoft.com/fwlink/p/?LinkID=123652).  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|DNS (Domain Name System)|53|53|  
|DHCP (Dynamic Host Configuration Protocol)|67 et 68|--|  
|Résolution de noms Netbios|137|--|  
|Service de datagramme NetBIOS|138|--|  
|Service de session NETBIOS|--|139|  



<!--HONumber=Nov16_HO1-->


