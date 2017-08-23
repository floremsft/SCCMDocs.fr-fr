---
title: "Unterstützung für Windows-Features | Microsoft-Dokumentation"
description: "Hier erfahren Sie, welche Windows-und Netzwerkfeatures in System Center Configuration Manager unterstützt werden."
ms.custom: na
ms.date: 3/30/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0cf4bacb-6b6d-4d4f-8640-b13fe15873de
caps.latest.revision: "8"
caps.handback.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: e040552dab21ba9a71e06a78f6acc2ffe1b0eb61
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="support-for-windows-features-and-networks-in-system-center-configuration-manager"></a>Unterstützung für Windows-Features und -Netzwerke in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

In diesem Thema wird beschrieben, welche allgemeinen Windows- und Netzwerkfeatures von System Center Configuration Manager unterstützt werden.  


##  <a name="bkmk_branchcache"></a> BranchCache  
Sie können Windows BranchCache mit Configuration Manager verwenden, wenn Sie BranchCache auf Verteilungspunkten aktivieren und Clients zum Verwenden von BranchCache im Modus „Verteilter Cache“ konfigurieren.

Sie können die BranchCache-Einstellungen bei einem Bereitstellungstyp für Anwendungen, bei der Bereitstellung für ein Paket und für Tasksequenzen konfigurieren.  

Wenn die Voraussetzungen für BranchCache erfüllt sind, können mithilfe dieser Funktion Inhalte von lokalen Clients abgerufen werden, auf denen die Inhalte zwischengespeichert sind.  

Beispiel: Wenn der erste Clientcomputer mit aktivierter BranchCache-Funktion Inhalt von einem Verteilungspunkt anfordert, der als BranchCache-Server konfiguriert ist, lädt der Clientcomputer den Inhalt herunter und speichert ihn im Cache zwischen. Dieser Inhalt wird dann für Clients in dem Subnetz verfügbar, das den Inhalt auch angefordert hat.

Diese Clients führen auch eine Zwischenspeicherung des Inhalts durch. Auf diese Weise muss der Inhalt von Clients im gleichen Subnetz später nicht erneut vom Verteilungspunkt heruntergeladen werden, und der Inhalt ist bei späteren Übertragungen über mehrere Clients verteilt.  

**Anforderungen, um BranchCache mit Configuration Manager zu unterstützen:**  
-   **Konfigurieren von Verteilungspunkten:**  
    Fügen Sie das Feature **Windows BranchCache** dem Standortsystemserver hinzu, der als Verteilungspunkt konfiguriert ist.    

    -   Für Verteilungspunkte auf Servern, die für die Unterstützung von BranchCache konfiguriert sind, ist keine zusätzliche Konfiguration erforderlich.   
    -   Sie können Windows BranchCache nicht einem cloudbasierten Verteilungspunkt hinzufügen, aber cloudbasierte Verteilungspunkte unterstützen das Herunterladen von Inhalten durch Clients, die für Windows BranchCache konfiguriert sind.  

-   **Konfigurieren von Clients:**    
    -   Die Clients, die BranchCache unterstützen können, müssen für den BranchCache-Modus „Verteilter Cache“ konfiguriert werden.  
    -   Die Betriebssystemeinstellung für BITS-Clienteinstellungen muss zur Unterstützung von BranchCache aktiviert sein.   <br /> <br />
        
    Hinweise, wie Sie Clients zur Unterstützung von BranchCache konfigurieren können, finden Sie im Abschnitt [Configure clients (Konfigurieren von Clients)](https://technet.microsoft.com/itpro/windows/manage/waas-branchcache#configure-clients-for-branchcache) unter [Configure BranchCache for Windows 10 updates (Konfigurieren von BranchCache für Windows 10-Updates)](https://technet.microsoft.com/itpro/windows/manage/waas-branchcache).


**Configuration Manager unterstützt die folgenden Clientbetriebssysteme mit Windows BranchCache:**  

|Betriebssystem|Details zur Unterstützung|  
|----------------------|---------------------|  
|Windows 7 mit SP1|Standardmäßig unterstützt|  
|Windows 8|Standardmäßig unterstützt|  
|Windows 8.1|Standardmäßig unterstützt|  
|Windows 10|Standardmäßig unterstützt|  
|Windows Server 2008 mit SP2|**Erfordert BITS 4.0**: Sie können BITS 4.0 mithilfe von Softwareupdates oder Softwareverteilung auf Configuration Manager-Clients installieren. Weitere Informationen zur Version BITS 4.0 finden Sie unter [Windows Management Framework](http://go.microsoft.com/fwlink/p/?LinkId=181979).<br /><br /> Die BranchCache-Clientfunktion wird unter diesem Betriebssystem für die Softwareverteilung, die vom Netzwerk aus ausgeführt wird, oder für SMB-Dateiübertragungen nicht unterstützt. Darüber hinaus kann dieses Betriebssystem nicht die BranchCache-Funktionalität mit cloudbasierten Verteilungspunkten verwenden.|  
|Windows Server 2008 R2|Standardmäßig unterstützt|  
|Windows Server 2012|Standardmäßig unterstützt|  
|Windows Server 2012 R2|Standardmäßig unterstützt|  

 Weitere Informationen zu BranchCache finden Sie unter [BranchCache für Windows](http://go.microsoft.com/fwlink/p/?LinkId=177945) in der Dokumentation zu Windows Server.  

##  <a name="bkmk_Workgroups"></a> Computer in Arbeitsgruppen  
Configuration Manager stellt Unterstützung für Clients in Arbeitsgruppen bereit.  

-   Configuration Manager unterstützt das Verschieben eines Clients aus einer Arbeitsgruppe in eine Domäne bzw. aus einer Domäne in eine Arbeitsgruppe. Weitere Informationen finden Sie im Abschnitt [How to Install Configuration Manager Clients on Workgroup Computers (Installieren von Configuration Manager-Clients auf Arbeitsgruppencomputern)](../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientWorkgroup) im Thema [How to deploy clients to Windows computers in System Center Configuration Manager (Bereitstellen von Clients für Windows-Computer in System Center Configuration Manager)](../../../core/clients/deploy/deploy-clients-to-windows-computers.md).  

> [!NOTE]  
>  Obwohl Clients in Arbeitsgruppen unterstützt werden, müssen alle Standortsysteme Mitglieder einer unterstützten Active Directory-Domäne sein.  


##  <a name="bkmmk_datadedup"></a> Datendeduplizierung  
Configuration Manager unterstützt die Verwendung der Datendeduplizierung mit Verteilungspunkten unter den folgenden Betriebssystemen:  

-   Windows Server 2012 R2  

-   Windows Server 2012 R2  

> [!IMPORTANT]  
>  Das Volume, das Paketquelldateien hostet, kann nicht für die Datendeduplizierung gekennzeichnet werden. Dies liegt daran, dass die Datendeduplizierung Analysepunkte verwendet und Configuration Manager die Verwendung eines Inhaltsquellspeicherorts mit Dateien, die auf Analysepunkten gespeichert sind, nicht unterstützt.  

Weitere Informationen finden Sie unter [Configuration Manager-Verteilungspunkte und Windows Server 2012-Datendeduplizierung](http://blogs.technet.com/b/configmgrteam/archive/2014/02/18/configuration-manager-distribution-points-and-windows-server-2012-data-deduplication.aspx) im Configuration Manager-Teamblog und unter [Datendeduplizierung: Übersicht](http://technet.microsoft.com/library/hh831602.aspx) in der TechNet-Bibliothek für Windows Server.  

##  <a name="bkmk_DA"></a> DirectAccess  
Configuration Manager unterstützt das DirectAccess-Feature in Windows Server 2008 R2 und höher für die Kommunikation zwischen Clients und Standortserversystemen.  

-   Wenn alle Voraussetzungen für DirectAccess erfüllt sind, ermöglicht DirectAccess Configuration Manager-Clients, im Internet so mit ihrem zugewiesenen Standort zu kommunizieren, als befänden sie sich im Intranet.  

-   Für serverseitig initiierte Aktionen, wie z. B. Remotesteuerung und Clientpushinstallation, muss auf dem initiierenden Computer (z. B. dem Standortserver) IPv6 ausgeführt werden, und dieses Protokoll muss von allen beteiligten Netzwerkgeräten unterstützt werden.  

Configuration Manager bietet keine DirectAccess-Unterstützung für folgende Aktionen:  

-   Bereitstellung von Betriebssystemen  

-   Kommunikation zwischen Configuration Manager-Standorten  

-   Kommunikation zwischen Configuration Manager-Standortsystemservern innerhalb eines Standorts  

##  <a name="bkmk_dualboot"></a> Dual-Boot-Computer  
 Configuration Manager kann nur jeweils ein Betriebssystem pro Computer verwalten. Wenn auf einem zu verwaltenden Computer mehr als ein Betriebssystem installiert ist, müssen Sie die Ermittlungs- und Installationsmethoden so anpassen, dass der Configuration Manager-Client nur unter dem zu verwaltenden Betriebssystem installiert wird.  

##  <a name="bkmk_IPv6"></a> Internet Protocol, Version 6  
 Configuration Manager unterstützt sowohl Internetprotokoll Version 4 (IPv4) als auch Internetprotokoll Version 6 (IPv6). Dabei gelten folgende Ausnahmen:  

|Funktion| Ausnahmen bei der IPv6-Unterstützung|  
|--------------|-------------------------------|  
|Cloudbasierte Verteilungspunkte|IPv4 ist erforderlich, um Microsoft Azure- und cloudbasierte Verteilungspunkte zu unterstützen.|  
|Mobilgeräte, die von Microsoft Intune und dem Microsoft-Dienstconnector registriert werden|IPv4 ist für die Unterstützung mobiler Geräte erforderlich, die von Microsoft Intune und dem Microsoft-Dienstconnector registriert werden.|  
|Netzwerkermittlung|IPv4 ist erforderlich, wenn Sie für die Suche bei der Netzwerkermittlung einen DHCP-Server konfigurieren.|  
|Betriebssystembereitstellung|IPv4 ist zur Unterstützung der Betriebssystembereitstellung erforderlich.|  
|Aktivierungsproxykommunikation|IPv4 ist für die Unterstützung von Aktivierungsproxypaketen auf dem Client erforderlich.|  
|Windows CE|IPv4 ist für die Unterstützung des Configuration Manager-Clients auf Windows CE-Geräten erforderlich.|  

##  <a name="bkmk_NAT"></a> Netzwerkadressübersetzung (Netzwerkadressübersetzung (Network Address Translation, NAT), NAT)  
 Die Netzwerkadressenübersetzung wird in Configuration Manager nicht unterstützt, es sei denn, der Standort unterstützt Clients aus dem Internet und der Client erkennt, dass er mit dem Internet verbunden ist. Weitere Informationen zur internetbasierten Clientverwaltung finden Sie unter [Planen der Verwaltung internetbasierter Clients in System Center Configuration Manager](../../../core/clients/deploy/plan/plan-for-managing-internet-based-clients.md).  

##  <a name="bkmk_storage"></a> Spezielle Speichertechnologien  
 Configuration Manager ist für die Hardware ausgelegt, die auf der Windows-Hardwarekompatibilitätsliste für die unterstützte Version des Betriebssystems zertifiziert ist, auf dem die Configuration Manager-Komponente installiert ist.

Für Standortserverrollen ist das NTFS-Dateisystem erforderlich, damit Verzeichnis- und Dateiberechtigungen festgelegt werden können. Da der Besitz des logischen Laufwerks vollständig von Configuration Manager beansprucht wird, ist die gemeinsame Nutzung einer logischen Partition durch Standortsysteme auf separaten Computern mit beliebiger Speichertechnologie nicht möglich. Allerdings kann von jedem Computer eine separate logische Partition auf der gleichen physischen Partition eines gemeinsam genutzten Speichergeräts verwendet werden.  

 **Aspekte für die Unterstützung:**  

-   **Storage Area Network (SAN)**: Ein SAN wird unterstützt, wenn ein unterstützter Windows-basierter Server direkt mit dem vom SAN gehosteten Volume verbunden ist.  

-   **Single Instance Storage (SIS)**: Das Konfigurieren von Verteilungspunktpaketen und Signaturordnern in einem SIS-fähigen (Single Instance Storage) Volume wird von Configuration Manager nicht unterstützt.  

     Darüber hinaus wird der Configuration Manager-Clientcache auf einem SIS-fähigen Volume nicht unterstützt.  

-   **Laufwerk mit Wechselmedien**: Die Installation von Configuration Manager-Standortsystemen oder -Clients auf einem Laufwerk mit Wechselmedien wird von Configuration Manager nicht unterstützt.  
