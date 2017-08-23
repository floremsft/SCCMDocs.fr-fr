---
title: Von Configuration Manager verwendete Ports | Microsoft-Dokumentation
description: "Erfahren Sie mehr über die erforderlichen und anpassbaren Ports, die System Center Configuration Manager für Verbindungen verwendet."
ms.custom: na
ms.date: 3/20/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c6777fb0-0754-4abf-8a1b-7639d23e9391
caps.latest.revision: "8"
caps.handback.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 78caa69e10f5d386daab1e61e484d4d134469708
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="ports-used-in-system-center-configuration-manager"></a>In System Center Configuration Manager verwendete Ports

*Gilt für: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager ist ein verteiltes Client-/Server-System. Aufgrund der verteilten Struktur von Configuration Manager können Verbindungen zwischen Standortservern, Standortsystemen und Clients hergestellt werden. Bei einigen Verbindungen werden nicht konfigurierbare Ports verwendet, bei anderen werden benutzerdefinierte Ports unterstützt. Bei Verwendung einer Portfilterungstechnologie, z.B. Firewalls, Router, Proxyserver oder IPsec, müssen Sie überprüfen, ob die erforderlichen Ports verfügbar sind.  

> [!NOTE]  
>  Wenn Sie internetbasierte Clients über SSL-Bridging unterstützen, müssen Sie möglicherweise zusätzlich zu den Portanforderungen bestimmten HTTP-Verben und -Headern ermöglichen, ihre Firewall zu passieren.   

 Die folgenden Portauflistungen werden von Configuration Manager verwendet und beinhalten keine Informationen für Windows-Standarddienste, wie z.B. Gruppenrichtlinieneinstellungen für Active Directory Domain Services oder Kerberos-Authentifizierung. Informationen zu Diensten und Ports für Windows Server finden Sie unter [Dienstübersicht und Netzwerkportanforderungen für das Windows Server-System](http://go.microsoft.com/fwlink/p/?LinkID=123652).  

##  <a name="BKMK_ConfigurablePorts"></a> Konfigurierbare Ports  
 Configuration Manager ermöglicht die Portkonfiguration für folgende Kommunikationsarten:  

-   Anwendungskatalog-Websitepunkt zu Anwendungskatalog-Webdienstpunkt  

-   Anmeldungsproxypunkt zu Anmeldungspunkt  

-   Systeme zwischen Client und Standort, auf denen IIS ausgeführt wird  

-   Client zu Internet (als Proxyservereinstellungen)  

-   Softwareupdatepunkt zu Internet (als Proxyservereinstellungen)  

-   Softwareupdatepunkt zu WSUS-Server  

-   Standortserver zu Standortdatenbankserver  

-   Reporting Services-Punkte  

    > [!NOTE]  
    >  Die Ports, die für die Standortsystemrolle des Reporting Services-Punkts verwendet werden, werden in SQL Server Reporting Services konfiguriert. Diese Ports werden dann von Configuration Manager zur Kommunikation mit dem Reporting Services-Punkt verwendet. Achten Sie darauf, diese Ports beim Definieren der IP-Filterinformationen für IPsec-Richtlinien oder beim Konfigurieren von Firewalls zu überprüfen.  

Für die Kommunikation zwischen Client und Standortsystem werden standardmäßig HTTP-Port 80 und HTTPS-Port 443 verwendet. Die Ports für die Kommunikation zwischen Client und Standortsystem über HTTP oder HTTPS können während des Setups oder in den Standorteigenschaften für Ihren Configuration Manager-Standort geändert werden.  

Die Ports, die für die Standortsystemrolle des Reporting Services-Punkts verwendet werden, werden in SQL Server Reporting Services konfiguriert. Diese Ports werden dann von Configuration Manager zur Kommunikation mit dem Reporting Services-Punkt verwendet. Achten Sie darauf, diese Ports beim Definieren der IP-Filterinformationen für IPsec-Richtlinien oder beim Konfigurieren von Firewalls zu überprüfen.  

##  <a name="BKMK_NonConfigurablePorts"></a> Nicht konfigurierbare Ports  
Configuration Manager lässt keine Portkonfiguration für folgende Kommunikationsarten zu:  

-   Standort zu Standort  

-   Standortserver zu Standortsystem  

-   Configuration Manager-Konsole für SMS-Anbieter  

-   Configuration Manager-Konsole zu Internet  

-   Verbindungen mit Clouddiensten, z.B. Microsoft Intune und cloudbasierten Verteilungspunkten  

##  <a name="BKMK_CommunicationPorts"></a> Von Configuration Manager-Clients und Standortsystemen verwendete Ports  
In den folgenden Abschnitten sind die Ports beschrieben, die für die Kommunikation in Configuration Manager verwendet werden. Die Pfeile in den Abschnittstiteln stellen die Kommunikationsrichtung dar:  

-   -- > zeigt, dass ein Computer die Kommunikation initiiert und der andere Computer immer antwortet  

-   &lt; -- > zeigt, dass beide Computer die Kommunikation initiieren können  

###  <a name="BKMK_PortsAI"></a>Asset Intelligence-Synchronisierungspunkt -- > Microsoft  

|Beschreibung|UDP|TCP|  
|-----------------|---------|---------|  
|Secure Hypertext Transfer-Protokoll (HTTPS)|--|443|  

###  <a name="BKMK_PortsAI-to-SQL"></a> Asset Intelligence-Synchronisierungspunkt -- > SQL Server  

|Beschreibung|UDP|TCP|  
|-----------------|---------|---------|  
|SQL über TCP|--|1433 (siehe Hinweis 2, **Alternativer Port verfügbar**)|  

###  <a name="BKMK_PortsAppCatalogService-SQL"></a> Anwendungskatalog-Webdienstpunkt -- > SQL Server  

|Beschreibung|UDP|TCP|  
|-----------------|---------|---------|  
|SQL über TCP|--|1433 (siehe Hinweis 2, **Alternativer Port verfügbar**)|  

###  <a name="BKMK_PortsAppCatalogWebSitePoint_AppCatalogWebServicePoint"></a> Anwendungskatalog-Websitepunkt -- > Anwendungskatalog-Webdienstpunkt  

|Beschreibung|UDP|TCP|  
|-----------------|---------|---------|  
|Hypertext Transfer-Protokoll (HTTP)|--|80 (siehe Hinweis 2, **Alternativer Port verfügbar**)|  
|Secure Hypertext Transfer-Protokoll (HTTPS)|--|443 (siehe Hinweis 2, **Alternativer Port verfügbar**)|  

###  <a name="BKMK_PortsClient-AppCatalogWebsitePoint"></a> Client -- > Anwendungskatalog-Websitepunkt  

|Beschreibung|UDP|TCP|  
|-----------------|---------|---------|  
|Hypertext Transfer-Protokoll (HTTP)|--|80 (siehe Hinweis 2, **Alternativer Port verfügbar**)|  
|Secure Hypertext Transfer-Protokoll (HTTPS)|--|443 (siehe Hinweis 2, **Alternativer Port verfügbar**)|  

###  <a name="BKMK_PortsClient-ClientWakeUp"></a> Client -- &gt; Client  
 Zusätzlich zu den in der folgenden Tabelle aufgeführten Ports nutzt der Aktivierungsproxy auch ICMP-Echoanforderungsmeldungen (Internet Control Message Protocol) von einem Client zum anderen, sofern diese für den Aktivierungsproxy konfiguriert wurden.

Diese Kommunikation wird verwendet, um zu überprüfen, ob der andere Clientcomputer im Netzwerk aktiviert ist. ICMP (Internet Control Message Protocol) wird gelegentlich als „TCP/IP-Ping-Befehle“ bezeichnet. ICMP hat keine UDP- oder TCP-Protokollnummer und wird daher in der folgenden Tabelle nicht aufgeführt. Von allen hostbasierten Firewalls auf diesen Clientcomputern oder beteiligten Netzwerkgeräten im Subnetz muss jedoch der ICMP-Datenverkehr zugelassen werden, damit die Aktivierungsproxykommunikation erfolgreich durchgeführt werden kann.  

|Beschreibung|UDP|TCP|  
|-----------------|---------|---------|  
|-Wake-On-LAN|9 (siehe Hinweis 2, **Alternativer Port verfügbar**)|--|  
|Aktivierungsproxy|25536 (siehe Hinweis 2, **Alternativer Port verfügbar**)|--|  

###  <a name="BKMK_PortsClient-PolicyModule"></a> Client -- &gt; Configuration Manager-Richtlinienmodul (Registrierungsdienst für Netzwerkgeräte)  

|Beschreibung|UDP|TCP|  
|-----------------|---------|---------|  
|Hypertext Transfer-Protokoll (HTTP)||80|  
|Secure Hypertext Transfer-Protokoll (HTTPS)|--|443|  

###  <a name="BKMK_PortsClient-CloudDP"></a> Client -- > Cloudbasierter Verteilungspunkt  

|Beschreibung|UDP|TCP|  
|-----------------|---------|---------|  
|Secure Hypertext Transfer-Protokoll (HTTPS)|--|443|  

###  <a name="BKMK_PortsClient-DP"></a> Client -- > Verteilungspunkt  

|Beschreibung|UDP|TCP|  
|-----------------|---------|---------|  
|Hypertext Transfer-Protokoll (HTTP)|--|80 (siehe Hinweis 2, **Alternativer Port verfügbar**)|  
|Secure Hypertext Transfer-Protokoll (HTTPS)|--|443 (siehe Hinweis 2, **Alternativer Port verfügbar**)|  

###  <a name="BKMK_PortsClient-DP2"></a> Client -- > für Multicast konfigurierter Verteilungspunkt  

|Beschreibung|UDP|TCP|  
|-----------------|---------|---------|  
|Server Message Block (SMB)|--|445|  
|Multicast-Protokoll|63000-64000|--|  

###  <a name="BKMK_PortsClient-DP3"></a> Client -- > für PXE konfigurierter Verteilungspunkt  

|Beschreibung|UDP|TCP|  
|-----------------|---------|---------|  
|Dynamic Host Configuration-Protokoll (DHCP)|67 und 68|--|  
|Trivial File Transfer-Protokoll (TFTP)|69 (siehe Hinweis 4, **Daemon für „Trivial FTP“ (TFTP)**)|--|  
|Boot Information Negotiation Layer (BINL)|4011|--|  

###  <a name="BKMK_PortsClient-FSP"></a> Client -- > Fallbackstatuspunkt  

|Beschreibung|UDP|TCP|  
|-----------------|---------|---------|  
|Hypertext Transfer-Protokoll (HTTP)|--|80 (siehe Hinweis 2, **Alternativer Port verfügbar**)|  

###  <a name="BKMK_PortsClient-GCDC"></a> Client ‒ > Global Catalog-Domänencontroller  
 Ein Configuration Manager-Client stellt keine Verbindung mit einem globalen Katalogserver her, wenn er für die reine Internetkommunikation konfiguriert ist oder einen Arbeitsgruppencomputer darstellt.  

|Beschreibung|UDP|TCP|  
|-----------------|---------|---------|  
|Globales Katalog-LDAP|--|3268|  
|Globales Katalog-LDAP-SSL|--|3269|  

###  <a name="BKMK_PortsClient-MP"></a> Client -- > Verwaltungspunkt  

|Beschreibung|UDP|TCP|  
|-----------------|---------|---------|  
|Clientbenachrichtigung (Standardkommunikation vor Fallback auf HTTP oder HTTPS)|--|10123 (siehe Hinweis 2, **Alternativer Port verfügbar**)|  
|Hypertext Transfer-Protokoll (HTTP)|--|80 (siehe Hinweis 2, **Alternativer Port verfügbar**)|  
|Secure Hypertext Transfer-Protokoll (HTTPS)|--|443 (siehe Hinweis 2, **Alternativer Port verfügbar**)|  

###  <a name="BKMK_PortsClient-SUP"></a> Client -- > Softwareupdatepunkt  

|Beschreibung|UDP|TCP|  
|-----------------|---------|---------|  
|Hypertext Transfer-Protokoll (HTTP)|--|80 oder 8530 (siehe Hinweis 3, **Windows Server Update Services**)|  
|Secure Hypertext Transfer-Protokoll (HTTPS)|--|443 oder 8531 (siehe Hinweis 3, **Windows Server Update Services**)|  

###  <a name="BKMK_PortsClient-SMP"></a> Client -- > Zustandsmigrationspunkt  

|Beschreibung|UDP|TCP|  
|-----------------|---------|---------|  
|Hypertext Transfer-Protokoll (HTTP)|--|80 (siehe Hinweis 2, **Alternativer Port verfügbar**)|  
|Secure Hypertext Transfer-Protokoll (HTTPS)|--|443 (siehe Hinweis 2, **Alternativer Port verfügbar**)|  
|Server Message Block (SMB)|--|445|  

###  <a name="BKMK_PortsConsole-Client"></a> Configuration Manager-Konsole -- > Client  

|Beschreibung|UDP|TCP|  
|-----------------|---------|---------|  
|Remotesteuerung (Steuerung)|--|2701|  
|Remoteunterstützung (RDP und RTC)|--|3389|  

###  <a name="BKMK_PortsConsole-Internet"></a> Configuration Manager-Konsole -- > Internet  

|Beschreibung|UDP|TCP|  
|-----------------|---------|---------|  
|Hypertext Transfer-Protokoll (HTTP)|--|80|  

###  <a name="BKMK_PortsConsole-RSP"></a> Configuration Manager-Konsole -- > Reporting Services-Punkt  


|Beschreibung|UDP|TCP|
|-----------------|---------|---------|   
|Hypertext Transfer-Protokoll (HTTP)|--|80 (siehe Hinweis 2, **Alternativer Port verfügbar**)|  
|Secure Hypertext Transfer-Protokoll (HTTPS)|--|443 (siehe Hinweis 2, **Alternativer Port verfügbar**)|  

###  <a name="BKMK_PortsConsole-Site"></a> Configuration Manager-Konsole -- > Standortserver  

|Beschreibung|UDP|TCP|  
|-----------------|---------|---------|  
|RPC (erstes Verbinden mit WMI zur Suche des Anbietersystems)|--|135|  

###  <a name="BKMK_PortsConsole-Provider"></a> Configuration Manager-Konsole -- > SMS-Anbieter  

|Beschreibung|UDP|TCP|  
|-----------------|---------|---------|  
|RPC-Endpunktzuordnung|135|135|  
|RPC|--|DYNAMISCH (siehe Hinweis 6, **Dynamische Ports**)|  

###  <a name="BKMK_PortsCertificateRegistationPoint_PolicyModule"></a> Configuration Manager-Richtlinienmodul (Registrierungsdienst für Netzwerkgeräte) -- > Zertifikatregistrierungspunkt  

|Beschreibung|UDP|TCP|  
|-----------------|---------|---------|  
|Secure Hypertext Transfer-Protokoll (HTTPS)|--|443 (siehe Hinweis 2, **Alternativer Port verfügbar**)|  

###  <a name="BKMK_PortsDist_MP"></a> Verteilungspunkt --> Verwaltungspunkt  
 Ein Verteilungspunkt kommuniziert mit dem Verwaltungspunkt in den folgenden Szenarien:  

-   Um den Status von vorab bereitgestellten Inhalten zu melden  

-   Um die Verwendungsdatenzusammenfassung zu melden  

-   Um die Inhaltsprüfung zu melden  

-   Um den Status von Paketdownloads zu melden (Pullverteilungspunkt)

|Beschreibung|UDP|TCP|  
|-----------------|---------|---------|  
|Hypertext Transfer-Protokoll (HTTP)|--|80 (siehe Hinweis 2, **Alternativer Port verfügbar**)|  
|Secure Hypertext Transfer-Protokoll (HTTPS)|--|443 (siehe Hinweis 2, **Alternativer Port verfügbar**)|  

###  <a name="BKMK_PortsEndpointProtection_Internet"></a> Endpoint Protection-Punkt -- > Internet  

|Beschreibung|UDP|TCP|  
|-----------------|---------|---------|  
|Hypertext Transfer-Protokoll (HTTP)|--|80|  

###  <a name="BKMK_PortsEP-to-SQL"></a> Endpoint Protection-Punkt -- > SQL Server  

|Beschreibung|UDP|TCP|  
|-----------------|---------|---------|  
|SQL über TCP|--|1433 (siehe Hinweis 2, **Alternativer Port verfügbar**)|  

###  <a name="BKMK_PortsEnrollmentProxyEnrollmentPoint"></a> Anmeldungsproxypunkt -- > Anmeldungspunkt  

|Beschreibung|UDP|TCP|  
|-----------------|---------|---------|  
|Secure Hypertext Transfer-Protokoll (HTTPS)|--|443 (siehe Hinweis 2, **Alternativer Port verfügbar**)|  

###  <a name="BKMK_PortsEnrollmentEnrollmentSQL"></a> Anmeldungspunkt -- > SQL Server  

|Beschreibung|UDP|TCP|  
|-----------------|---------|---------|  
|SQL über TCP|--|1433 (siehe Hinweis 2, **Alternativer Port verfügbar**)|  

###  <a name="BKMK_PortsExchangeConnectorHosted"></a> Exchange Server-Connector -- &gt; Exchange Online  

|Beschreibung|UDP|TCP|  
|-----------------|---------|---------|  
|Windows-Remoteverwaltung über HTTPS|--|5986|  

###  <a name="BKMK_PortsExchangeConnectorOnPrem"></a> Exchange Server-Connector -- > Exchange Server (lokal)  

|Beschreibung|UDP|TCP|  
|-----------------|---------|---------|  
|Windows-Remoteverwaltung über HTTP|--|5985|  

###  <a name="BKMK_PortsMacEnrollmentProxyPoint"></a> Macintosh-Computer -- > Anmeldungsproxypunkt  

|Beschreibung|UDP|TCP|  
|-----------------|---------|---------|  
|Secure Hypertext Transfer-Protokoll (HTTPS)|--|443|  

###  <a name="BKMK_PortsMP-DC"></a> Verwaltungspunkt -- > Domänencontroller  

|Beschreibung|UDP|TCP|  
|-----------------|---------|---------|  
|Lightweight Directory Access-Protokoll (LDAP)|--|389|  
|LDAP (SSL-Verbindung [Secure Sockets Layer])|636|636|  
|Globales Katalog-LDAP|--|3268|  
|Globales Katalog-LDAP-SSL|--|3269|  
|RPC-Endpunktzuordnung|135|135|  
|RPC|--|DYNAMISCH (siehe Hinweis 6, **Dynamische Ports**)|  

###  <a name="BKMK_PortsMP-Site"></a> Verwaltungspunkt &lt; --> Standortserver  
 (siehe Hinweis 5, **Kommunikation zwischen dem Standortserver und Standortsystemen**)  

|Beschreibung|UDP|TCP|  
|-----------------|---------|---------|  
|RPC-Endpunktzuordnung|--|135|  
|RPC|--|DYNAMISCH (siehe Hinweis 6, **Dynamische Ports**)|  
|Server Message Block (SMB)|--|445|  

###  <a name="BKMK_PortsMP-SQL"></a> Verwaltungspunkt -- > SQL Server  

|Beschreibung|UDP|TCP|  
|-----------------|---------|---------|  
|SQL über TCP|--|1433 (siehe Hinweis 2, **Alternativer Port verfügbar**)|  

###  <a name="BKMK_PortsMobileDeviceClient-EnrollmentProxyPoint"></a> Mobiles Gerät -- > Anmeldungsproxypunkt  

|Beschreibung|UDP|TCP|  
|-----------------|---------|---------|  
|Secure Hypertext Transfer-Protokoll (HTTPS)|--|443|  

###  <a name="BKMK_PortsMobileDeviceClient-WindowsIntune"></a> Mobiles Gerät --> Microsoft Intune  

|Beschreibung|UDP|TCP|  
|-----------------|---------|---------|  
|Secure Hypertext Transfer-Protokoll (HTTPS)|--|443|  

###  <a name="BKMK_PortsRSP-SQL"></a> Reporting Services-Punkt -- > SQL Server  

|Beschreibung|UDP|TCP|  
|-----------------|---------|---------|  
|SQL über TCP|--|1433 (siehe Hinweis 2, **Alternativer Port verfügbar**)|  

###  <a name="BKMK_PortsIntuneConnector-WindowsIntune"></a>Dienstverbindungspunkt -- > Microsoft Intune  

|Beschreibung|UDP|TCP|  
|-----------------|---------|---------|  
|Secure Hypertext Transfer-Protokoll (HTTPS)|--|443|
Mehr Informationen finden Sie unter [Internetzugriffsanforderungen](/sccm/core/servers/deploy/configure/about-the-service-connection-point#bkmk_urls) für den Dienstverbindungspunkt.

###  <a name="BKMK_PortsAppCatalogWebServicePoint_SiteServer"></a> Standortserver &lt; -- > Anwendungskatalog-Webdienstpunkt  

|Beschreibung|UDP|TCP|  
|-----------------|---------|---------|  
|Server Message Block (SMB)|--|445|  
|RPC-Endpunktzuordnung|135|135|  
|RPC|--|DYNAMISCH (siehe Hinweis 6, **Dynamische Ports**)|  

###  <a name="BKMK_PortsAppCatalogWebSitePoint_SiteServer"></a> Standortserver &lt; -- > Anwendungskatalog-Websitepunkt  

|Beschreibung|UDP|TCP|  
|-----------------|---------|---------|  
|Server Message Block (SMB)|--|445|  
|RPC-Endpunktzuordnung|135|135|  
|RPC|--|DYNAMISCH (siehe Hinweis 6, **Dynamische Ports**)|  

###  <a name="BKMK_PortsSite-AISP"></a> Standortserver &lt; --> Asset Intelligence-Synchronisierungspunkt  

|Beschreibung|UDP|TCP|  
|-----------------|---------|---------|  
|Server Message Block (SMB)|--|445|  
|RPC-Endpunktzuordnung|135|135|  
|RPC|--|DYNAMISCH (siehe Hinweis 6, **Dynamische Ports**)|  

###  <a name="BKMK_PortsSite-Client"></a> Standortserver -- > Client  

|Beschreibung|UDP|TCP|  
|-----------------|---------|---------|  
|-Wake-On-LAN|9 (siehe Hinweis 2, **Alternativer Port verfügbar**)|--|  

###  <a name="BKMK_PortsSiteServer-CloudDP"></a> Standortserver -- > Cloudbasierter Verteilungspunkt  

|Beschreibung|UDP|TCP|  
|-----------------|---------|---------|  
|Secure Hypertext Transfer-Protokoll (HTTPS)|--|443|  

###  <a name="BKMK_PortsSite-DP"></a> Standortserver -- > Verteilungspunkt  
 (siehe Hinweis 5, **Kommunikation zwischen dem Standortserver und Standortsystemen**)  

|Beschreibung|UDP|TCP|  
|-----------------|---------|---------|  
|Server Message Block (SMB)|--|445|  
|RPC-Endpunktzuordnung|135|135|  
|RPC|--|DYNAMISCH (siehe Hinweis 6, **Dynamische Ports**)|  

###  <a name="BKMK_PortsSite-DC"></a> Standortserver -- > Domänencontroller  

|Beschreibung|UDP|TCP|  
|-----------------|---------|---------|  
|Lightweight Directory Access-Protokoll (LDAP)|--|389|  
|LDAP (SSL-Verbindung [Secure Sockets Layer])|636|636|  
|Globales Katalog-LDAP|--|3268|  
|Globales Katalog-LDAP-SSL|--|3269|  
|RPC-Endpunktzuordnung|135|135|  
|RPC|--|DYNAMISCH (siehe Hinweis 6, **Dynamische Ports**)|  

###  <a name="BKMK_PortsCertificateRegistrationPoint_SiteServer"></a> Standortserver &lt; -- > Zertifikatregistrierungspunkt  

|Beschreibung|UDP|TCP|  
|-----------------|---------|---------|  
|Server Message Block (SMB)|--|445|  
|RPC-Endpunktzuordnung|135|135|  
|RPC|--|DYNAMISCH (siehe Hinweis 6, **Dynamische Ports**)|  

###  <a name="BKMK_PortsEndpointProtection_SiteServer"></a> Standortserver &lt; -- > Endpoint Protection-Punkt  

|Beschreibung|UDP|TCP|  
|-----------------|---------|---------|  
|Server Message Block (SMB)|--|445|  
|RPC-Endpunktzuordnung|135|135|  
|RPC|--|DYNAMISCH (siehe Hinweis 6, **Dynamische Ports**)|  

###  <a name="BKMK_EnrollmentPoint_SiteServer"></a> Standortserver &lt; -- > Registrierungspunkt  

|Beschreibung|UDP|TCP|  
|-----------------|---------|---------|  
|Server Message Block (SMB)|--|445|  
|RPC-Endpunktzuordnung|135|135|  
|RPC|--|DYNAMISCH (siehe Hinweis 6, **Dynamische Ports**)|  

###  <a name="BKMK_EnrollmentProxyPoint_SiteServer"></a> Standortserver &lt; -- > Registrierungsproxypunkt  

|Beschreibung|UDP|TCP|  
|-----------------|---------|---------|  
|Server Message Block (SMB)|--|445|  
|RPC-Endpunktzuordnung|135|135|  
|RPC|--|DYNAMISCH (siehe Hinweis 6, **Dynamische Ports**)|  

###  <a name="BKMK_PortsSite-FSP"></a> Standortserver &lt; -- > Fallbackstatuspunkt  
 (siehe Hinweis 5, **Kommunikation zwischen dem Standortserver und Standortsystemen**)  

|Beschreibung|UDP|TCP|  
|-----------------|---------|---------|  
|Server Message Block (SMB)|--|445|  
|RPC-Endpunktzuordnung|135|135|  
|RPC|--|DYNAMISCH (siehe Hinweis 6, **Dynamische Ports**)|  

###  <a name="BKMK_PortSite-Internet"></a> Standortserver -- > Internet  

|Beschreibung|UDP|TCP|  
|-----------------|---------|---------|  
|Hypertext Transfer-Protokoll (HTTP)|--|80 (siehe Hinweis 1, **Proxyserverport**)|  

###  <a name="BKMK_PortsIssuingCA_SiteServer"></a> Standortserver &lt; -- > Ausstellende Zertifizierungsstelle (certificate authority, CA)  
 Diese Kommunikation wird verwendet, wenn Sie Zertifikatprofile über den Zertifikatregistrierungspunkt bereitstellen. Diese Kommunikation wird nicht für jeden Standortserver in der Hierarchie verwendet. Stattdessen wird sie nur für die Standortserver verwendet, die sich in der Hierarchie an oberster Stelle befinden.  

|Beschreibung|UDP|TCP|  
|-----------------|---------|---------|  
|RPC-Endpunktzuordnung|135|135|  
|RPC (DCOM)|--|DYNAMISCH (siehe Hinweis 6, **Dynamische Ports**)|  

###  <a name="BKMK_PortsSite-RSP"></a> Standortserver &lt; -- > Reporting Services-Punkt  
 (siehe Hinweis 5, **Kommunikation zwischen dem Standortserver und Standortsystemen**)  

|Beschreibung|UDP|TCP|  
|-----------------|---------|---------|  
|Server Message Block (SMB)|--|445|  
|RPC-Endpunktzuordnung|135|135|  
|RPC|--|DYNAMISCH (siehe Hinweis 6, **Dynamische Ports**)|  

###  <a name="BKMK_PortsSite-Site"></a> Standortserver &lt; -- > Standortserver  

|Beschreibung|UDP|TCP|  
|-----------------|---------|---------|  
|Server Message Block (SMB)|--|445|  

###  <a name="BKMK_PortsSite-SQL"></a> Standortserver -- > SQL Server  

|Beschreibung|UDP|TCP|  
|-----------------|---------|---------|  
|SQL über TCP|--|1433 (siehe Hinweis 2, **Alternativer Port verfügbar**)|  

 Während der Installation eines Standorts, der einen SQL Server-Remotehost für die Standortdatenbank verwendet, müssen Sie die folgenden Ports zwischen Standortserver und SQL-Server öffnen:  

|Beschreibung|UDP|TCP|  
|-----------------|---------|---------|  
|Server Message Block (SMB)|--|445|  
|RPC-Endpunktzuordnung|135|135|  
|RPC|--|DYNAMISCH (siehe Hinweis 6, **Dynamische Ports**)|  

###  <a name="BKMK_PortsSite-Provider"></a> Standortserver -- > SMS-Anbieter  

|Beschreibung|UDP|TCP|  
|-----------------|---------|---------|  
|Server Message Block (SMB)|--|445|  
|RPC-Endpunktzuordnung|135|135|  
|RPC|--|DYNAMISCH (siehe Hinweis 6, **Dynamische Ports**)|  

###  <a name="BKMK_PortsSite-SUP"></a> Standortserver &lt; -- > Softwareupdatepunkt  
 (siehe Hinweis 5, **Kommunikation zwischen dem Standortserver und Standortsystemen**)  

|Beschreibung|UDP|TCP|  
|-----------------|---------|---------|  
|Server Message Block (SMB)|--|445|  
|Hypertext Transfer-Protokoll (HTTP)|--|80 oder 8530 (siehe Hinweis 3, **Windows Server Update Services**)|  
|Secure Hypertext Transfer-Protokoll (HTTPS)|--|443 oder 8531 (siehe Hinweis 3, **Windows Server Update Services**)|  

###  <a name="BKMK_PortsSite-SMP"></a> Standortserver &lt; -- > Zustandsmigrationspunkt  
 (siehe Hinweis 5, **Kommunikation zwischen dem Standortserver und Standortsystemen**)  

|Beschreibung|UDP|TCP|  
|-----------------|---------|---------|  
|Server Message Block (SMB)|--|445|  
|RPC-Endpunktzuordnung|135|135|  

###  <a name="BKMK_PortsProvider-SQL"></a> SMS-Anbieter -- &gt; SQL Server  

|Beschreibung|UDP|TCP|  
|-----------------|---------|---------|  
|SQL über TCP|--|1433 (siehe Hinweis 2, **Alternativer Port verfügbar**)|  

###  <a name="BKMK_PortsSUP-Internet"></a> Softwareupdatepunkt -- > Internet  

|Beschreibung|UDP|TCP|  
|-----------------|---------|---------|  
|Hypertext Transfer-Protokoll (HTTP)|--|80 (siehe Hinweis 1, **Proxyserverport**)|  

###  <a name="BKMK_PortsSUP-WSUS"></a> Softwareupdatepunkt -- > WSUS-Upstreamserver  

|Beschreibung|UDP|TCP|  
|-----------------|---------|---------|  
|Hypertext Transfer-Protokoll (HTTP)|--|80 oder 8530 (siehe Hinweis 3, **Windows Server Update Services**)|  
|Secure Hypertext Transfer-Protokoll (HTTPS)|--|443 oder 8531 (siehe Hinweis 3, **Windows Server Update Services**)|  

###  <a name="BKMK_PortsSQL-SQL"></a> SQL Server -- &gt; SQL Server  
 Für die standortübergreifende Datenbankreplikation ist die direkte Kommunikation von SQL Server an einem Standort mit SQL Server am über- oder untergeordneten Standort erforderlich.  

|Beschreibung|UDP|TCP|  
|-----------------|---------|---------|  
|SQL Server-Dienst|--|1433 (siehe Hinweis 2, **Alternativer Port verfügbar**)|  
|SQL Server Service Broker|--|4022 (siehe Hinweis 2, **Alternativer Port verfügbar**)|  

> [!TIP]  
>  Configuration Manager erfordert keinen SQL Server-Browser, der den Port UDP 1434 verwendet.  

###  <a name="BKMK_PortsStateMigrationPoint-to-SQL"></a> Zustandsmigrationspunkt --> SQL Server  

|Beschreibung|UDP|TCP|  
|-----------------|---------|---------|  
|SQL über TCP|--|1433 (siehe Hinweis 2, **Alternativer Port verfügbar**)|  



###  <a name="BKMY_PortNotes"></a> Hinweise für von Configuration Manager-Clients und Standortsystemen verwendete Ports  

1.  **Proxyserverport**: Dieser Port kann nicht konfiguriert, aber durch einen konfigurierten Proxyserver weitergeleitet werden.  

2.  **Alternativer Port verfügbar**: Ein alternativer Port kann für diesen Wert im Configuration Manager definiert werden. Wenn ein benutzerdefinierter Port definiert wurde, ersetzen Sie diesen benutzerdefinierten Port, wenn Sie die IP-Filterinformationen für die IPsec-Richtlinien oder zum Konfigurieren von Firewalls definieren.  

3.  **Windows Server Update Services (WSUS)**: WSUS können installiert werden, um die Ports 80/443 oder 8530/8531 für die Clientkommunikation zu verwenden. Wenn Sie WSUS unter Windows Server 2012 oder Windows Server 2016 ausführen, wird WSUS standardmäßig für die Verwendung von Port 8530 für HTTP und Port 8531 für HTTPS konfiguriert.  

     Nach der Installation kann der Port geändert werden. Es ist nicht erforderlich, in der gesamten Standorthierarchie dieselbe Portnummer zu verwenden.  

    -   Wenn der HTTP-Port 80 verwendet wird, muss der HTTPS-Port 443 sein.  

    -   Wenn ein anderer HTTP-Port verwendet wird, muss der HTTPS-Port 1 oder höher sein, z.B. 8530 oder 8531.   

    > [!NOTE]  
    >  Wenn Sie den Softwareupdatepunkt zur Verwendung von HTTPS konfigurieren, muss auch der HTTP-Port geöffnet sein. Der HTTP-Port wird für unverschlüsselte Daten, z. B. den EULA für bestimmte Updates, verwendet.  

4.  **Daemon für „Trivial FTP“ (TFTP)**: Der Daemon für „Trivial FTP“(TFTP) erfordert weder einen Benutzernamen noch ein Kennwort und ist integraler Bestandteil der Windows-Bereitstellungsdienste (Windows Deployment Services, WDS). Der Daemondienst für „Trivial FTP“ unterstützt das TFTP-Protokoll, das über folgende RFCs definiert ist:  

    -   RFC 350: TFTP  

    -   RFC 2347: Optionserweiterung  

    -   RFC 2348: Blockgrößenoption  

    -   RFC 2349: Timeoutintervall und Optionen zur Übertragungsgröße  

     Das Trivial File Transfer-Protokoll wurde zur Unterstützung von Startumgebungen ohne Datenträger entwickelt. TFTP-Daemons hören den UDP-Port 69 ab, antworten jedoch von einem dynamisch zugewiesenen, hohen Port. Aus diesem Grund kann der TFTP-Dienst bei Aktivierung dieses Ports eingehende TFTP-Anfragen empfangen. Es lässt jedoch nicht zu, dass der ausgewählte Server auf diese Anfragen reagiert. Der ausgewählte TFTP-Server kann erst dann auf eingehende TFTP-Anfragen reagieren, wenn er so konfiguriert ist, dass die Antwort über Port 69 erfolgt.  

5.  **Kommunikation zwischen dem Standortserver und Standortsystemen**: Standardmäßig erfolgt zwischen dem Standortserver und Standortsystemen eine bidirektionale Kommunikation. Der Standortserver initiiert die Kommunikation zum Konfigurieren des Standortsystems. Die meisten Standortsysteme können dann wiederum eine Verbindung zum Standortserver herstellen, um Statusinformationen zu senden. Von Reporting Services-Punkten und Verteilungspunkten werden keine Statusinformationen gesendet. Wenn Sie in den Eigenschaften des Standortsystems die Option **Verbindungen mit diesem Standortsystem müssen vom Standortserver hergestellt werden** ausgewählt haben, wird das Standortsystem keine Kommunikation mit dem Standortserver initiiert. Stattdessen wird die Kommunikation vom Standortserver initiiert, wobei die Authentifizierung beim Standortsystemserver über das Installationskonto des Standortsystems erfolgt.  

6.  **Dynamische Ports**: Für dynamische Ports (auch kurzlebige Ports genannt) wird eine Reihe von Portnummern verwendet, die durch die Betriebssystemversion festgelegt ist. Weitere Informationen über die Standardportbereiche finden Sie unter [Dienstübersicht und Netzwerkportanforderungen für das Windows Server-System](http://go.microsoft.com/fwlink/p/?LinkId=317965).  

##  <a name="BKMK_AdditionalPorts"></a> Zusätzliche Portlisten  
 In den folgenden Abschnitten finden Sie zusätzliche Informationen zu von Configuration Manager verwendeten Ports.  

###  <a name="BKMK_ClientShares"></a> Client-zu-Server-Freigaben  
 Von Clients wird SMB (Server Message Block) verwendet, wenn eine Verbindung zu UNC-Freigaben hergestellt wird. Beispiel:  

-   Manuelle Clientinstallation, bei der die Befehlszeileneigenschaft CCMSetup.exe **/source:** angegeben wird  

-   Endpoint Protection-Clients, von denen Definitionsdateien über einen UNC-Pfad heruntergeladen werden

|Beschreibung|UDP|TCP|  
|-----------------|---------|---------|  
|Server Message Block (SMB)|--|445|  

###  <a name="BKMK_SQLPorts"></a> Verbindungen zu Microsoft SQL Server  
 Für die Kommunikation mit dem SQL Server-Datenbankmodul und für die standortübergreifende Replikation können Sie den SQL Server-Standardport verwenden oder benutzerdefinierte Ports angeben:  

-   Die Kommunikation zwischen Standorten erfolgt über:  

    -   SQL Server Service Broker (standardmäßig TCP-Port 4022).  

    -   SQL Server-Dienst, erfolgt standardmäßig über TCP-Port 1433.  

-   Die standortinterne Kommunikation zwischen dem SQL Server-Datenbankmodul und verschiedenen Configuration Manager-Standortsystemrollen erfolgt standardmäßig über TCP-Port 1433.  

- Configuration Manager verwendet die gleichen Ports und Protokolle zur Kommunikation mit jedem SQL-Verfügbarkeitsgruppenreplikat, das die Standortdatenbank hostet, als wäre das Replikat eine eigenständige SQL Server-Instanz.

Wenn Sie Azure verwenden und die Standortdatenbank sich hinter einem internen oder externen Lastenausgleich befindet, konfigurieren Sie die folgenden Firewallausnahmen für jedes Replikat, und fügen Sie Lastenausgleichsregeln für die folgenden Ports hinzu:
 - SQL über TCP: TCP 1433
 - SQL Server Service Broker: TCP 4022
 - Server Message Block (SMB): TCP 445
 - RPC-Endpunktzuordnung: TCP 135

> [!WARNING]  
>  Dynamische Ports werden von Configuration Manager nicht unterstützt. Da von benannten SQL Server-Instanzen standardmäßig dynamische Ports für die Verbindung mit dem Datenbankmodul verwendet werden, müssen Sie bei der Verwendung einer benannten Instanz den statischen Port, den Sie für die standortinterne Kommunikation einsetzen möchten, manuell konfigurieren.  

 Die folgenden Standortsystemrollen kommunizieren direkt mit der SQL Server-Datenbank:  

-   Anwendungskatalog-Webdienstpunkt  

-   Zertifikatregistrierungspunktrolle  

-   Anmeldungspunktrolle  

-   Verwaltungspunkt  

-   Standortserver  

-   Reporting Services-Punkt  

-   SMS-Anbieter  

-   SQL Server -- > SQL Server  

Wenn ein SQL Server Datenbanken von mehreren Standorten hostet, muss jede Datenbank eine separate SQL Server-Instanz verwenden. Jede dieser Instanzen muss mit einem eindeutigen Portsatz konfiguriert sein.  

Wenn auf dem SQL Server eine Firewall aktiviert ist, stellen Sie sicher, dass diese die Ports, die von Ihrer Bereitstellung verwendet werden, auch zulässt. Konfigurieren Sie außerdem Firewalls, die sich an zusätzlichen Standorten im Netzwerk zwischen den Computern befinden, und die mit dem SQL Server kommunizieren, so dass sie die gleichen Ports zulassen.  

Wie Sie SQL Server für die Verwendung eines bestimmten Ports konfigurieren, wird in der TechNet-Bibliothek unter [Konfigurieren eines Servers zur Überwachung eines bestimmten TCP-Ports (SQL Server-Konfigurations-Manager)](http://go.microsoft.com/fwlink/p/?LinkID=226349) anhand eines Beispiels erläutert.  


### <a name="bkmk_discovery"> </a> Ermittlung und Veröffentlichung
Die folgenden Ports werden für die Ermittlung und Veröffentlichung von Standortinformationen verwendet:
 - Lightweight Directory Access-Protokoll (LDAP): 389
 - LDAP (Secure Sockets Layer [SSL]-Verbindung): 636


 - Globales Katalog-LDAP: 3268
 - Globales Katalog-LDAP-SSL: 3269


 - RPC-Endpunktzuordnung: 135
 - RPC: Dynamisch zugewiesene, hohe TCP-Ports


 - TCP 1024: 5000
 - TCP 49152: 65535


###  <a name="BKMK_External"></a> Externe Verbindungen von Configuration Manager  
 Configuration Manager-Clients oder -Standortsysteme können die folgenden externen Verbindungen erstellen:  

-   [Asset Intelligence-Synchronisierungspunkt ‒ &gt; Microsoft](#BKMK_PortsAI)  

-   [Endpoint Protection-Punkt ‒ &gt; Internet](#BKMK_PortsEndpointProtection_Internet)  

-   [Client ‒ &gt; Global Catalog-Domänencontroller](#BKMK_PortsClient-GCDC)  

-   [Configuration Manager-Konsole ‒ &gt;Internet](#BKMK_PortsConsole-Internet)  

-   [Verwaltungspunkt ‒ &gt; Domänencontroller](#BKMK_PortsMP-DC)  

-   [Standortserver ‒ &gt; Domänencontroller](#BKMK_PortsSite-DC)  

-   [Standortserver &lt; -- &gt; Ausstellende Zertifizierungsstelle (CA)](#BKMK_PortsIssuingCA_SiteServer)  

-   [Softwareupdatepunkt ‒ &gt; Internet](#BKMK_PortsSUP-Internet)  

-   [Softwareupdatepunkt ‒ &gt; WSUS-Upstreamserver](#BKMK_PortsSUP-WSUS)  

-   [Dienstverbindungspunkt ‒ &gt; Microsoft Intune](#BKMK_PortsIntuneConnector-WindowsIntune)  

###  <a name="BKMK_IBCMports"></a> Installationsanforderungen für Standortsysteme, die internetbasierte Clients unterstützen  
 Verwaltungs- und Verteilungspunkte, die internetbasierte Clients unterstützen, sowie Softwareupdatepunkt und Fallbackstatuspunkt verwenden für Installation und Reparatur die folgenden Ports:  

-   Standortserver --> Standortsystem: RPC-Endpunktzuordnung, verwendet UDP und TCP-Port 135.  

-   Standortserver--> Standortsystem: RPC Dynamic TCP-Ports  

-   Standortserver &lt; --> Standortsystem: Server Message Blocks (SMB) verwenden TCP-Port 445

Für die Anwendungs- und Paketinstallation auf Verteilungspunkten sind die folgenden RPC-Ports erforderlich:  

-   Standortserver -- > Verteilungspunkt: RPC-Endpunktzuordnung, verwendet UDP und TCP-Port 135

-   Standortserver--> Verteilungspunkt: RPC Dynamic TCP-Ports  

Verwenden Sie IPsec zur Sicherung des Datenverkehrs zwischen dem Standortserver und den Standortsystemen. Zur Einschränkung der von RPC verwendeten dynamischen Ports können Sie das RPC-Konfigurationstool von Microsoft (rpccfg.exe) verwenden. Dieses erlaubt die Konfiguration eines Portbereichs für die RPC-Pakete. Weitere Informationen zum RPC-Konfigurationstool finden Sie unter [Konfigurieren von RPC für die Verwendung bestimmter Ports und Schützen dieser Ports mit IPsec](http://go.microsoft.com/fwlink/p/?LinkId=124096).  

> [!IMPORTANT]  
>  Überprüfen Sie vor der Installation dieser Standortsysteme, ob der Remoteregistrierungsdienst auf dem Standortsystemserver ausgeführt wird und Sie ein Standortsystem-Installationskonto angegeben haben, falls sich das Standortsystem in einer anderen Active Directory-Gesamtstruktur ohne Vertrauensstellung befindet.  

###  <a name="BKMK_PortsClientInstall"></a> Von der Configuration Manager-Clientinstallation verwendete Ports  
Welche Ports während der Clientinstallation verwendet werden, ist von der Clientbereitstellungsmethode abhängig. Eine Liste der für jede Clientbereitstellungsmethode verwendeten Ports finden Sie im Abschnitt **Bei der Configuration Manager-Clientbereitstellung verwendete Ports** des Themas [Windows-Firewall- und Porteinstellungen für Clientcomputer in Configuration Manager](../../../core/clients/deploy/windows-firewall-and-port-settings-for-clients.md). Informationen zum Konfigurieren der Windows-Firewall auf dem Client für die Clientinstallation und zur Kommunikation nach der Installation finden Sie unter [Einstellungen für Windows-Firewall und Ports für System Center Configuration Manager-Clients](../../../core/clients/deploy/windows-firewall-and-port-settings-for-clients.md).  

###  <a name="BKMK_MigrationPorts"></a> Für die Migration verwendete Ports  
Der Standortserver, der die Migration ausführt, verwendet verschiedene Ports, um die Verbindung zu entsprechenden Standorten in der Quellhierarchie herzustellen, um Daten aus der SQL Server-Datenbank der Quellstandorte zu sammeln und Verteilungspunkte freizugeben.  

 Informationen zu diesen Ports finden Sie im Abschnitt [Für die Migration erforderliche Konfigurationen](../../../core/migration/prerequisites-for-migration.md#BKMK_Required_Configurations) des Themas [Voraussetzungen für die Migration in System Center Configuration Manager](../../../core/migration/prerequisites-for-migration.md).  

###  <a name="BKMK_ServerPorts"></a> Von Windows Server verwendete Ports  
 In der folgenden Tabelle werden die wichtigsten von Windows Server verwendeten Ports mit den entsprechenden Funktionen aufgelistet. Eine umfassende Liste der Windows Server-Dienste und Netzwerkportanforderungen finden Sie unter [Dienstübersicht und Netzwerkportanforderungen für das Windows Server-System](http://go.microsoft.com/fwlink/p/?LinkID=123652).  

|Beschreibung|UDP|TCP|  
|-----------------|---------|---------|  
|Domain Name System (DNS)|53|53|  
|Dynamic Host Configuration-Protokoll (DHCP)|67 und 68|--|  
|NetBIOS-Namensauflösung|137|--|  
|NetBIOS-Datagrammdienst|138|--|  
|NetBIOS-Sitzungsdienst|--|139|  
