---
title: VPN-Profile in System Center Configuration Manager | Microsoft-Dokumentation
description: "So verwenden Sie VPN-Profile in System Center Configuration Manager, um Benutzern in Ihrer Organisation Einstellungen für VPN bereitzustellen."
ms.custom: na
ms.date: 11/27/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c0f094f1-852e-4606-91db-97846d8f0772
caps.latest.revision: "6"
caps.handback.revision: "0"
author: arob98
ms.author: angrobe
manager: angrobe
ms.openlocfilehash: e07a80c1a59043b74cda7219f78c5fef66989ba8
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="vpn-profiles-in-system-center-configuration-manager"></a>VPN-Profile in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*


Verwenden Sie VPN-Profile in System Center Configuration Manager (auch als ConfigMgr oder SCCM bekannt), um Benutzern in Ihrer Organisation Einstellungen für VPN bereitzustellen. Durch Bereitstellen dieser Einstellungen erleichtern Sie dem Endbenutzer das Verbinden mit Ressourcen im Unternehmensnetzwerk.  

 Sie möchten z.B. allen Geräten, auf denen das Windows RT-Betriebssystem ausgeführt wird, die Einstellungen zur Verfügung stellen, die zum Verbinden mit einer Dateifreigabe im Unternehmensnetzwerk erforderlich sind. Sie können ein VPN-Profil mit den zum Verbinden mit dem Unternehmensnetzwerk erforderlichen Einstellungen erstellen und dieses Profil dann für alle Benutzer mit Geräten unter Windows RT in der Hierarchie bereitstellen. Benutzer von Windows RT-Geräten sehen die VPN-Verbindung in der Liste der verfügbaren Netzwerke und können sich mühelos mit diesem Netzwerk verbinden.  

 Wenn Sie ein VPN-Profil erstellen, können Sie eine Vielzahl von Sicherheitseinstellungen aufnehmen, darunter auch Zertifikate für die Serverüberprüfung und Clientauthentifizierung, die mit System Center Configuration Manager-Zertifikatprofilen bereitgestellt wurden. Weitere Informationen zu Zertifikatprofilen finden Sie unter [Zertifikatprofile in System Center Configuration Manager](introduction-to-certificate-profiles.md).  

 In diesem Abschnitt wird erklärt, welche Geräte Sie mit VPN-Profilen konfigurieren können, wenn Sie Configuration Manager verwenden.

 Unter [VPN profiles on mobile devices (VPN-Profile auf mobilen Geräten)](/sccm/mdm/deploy-use/create-vpn-profiles) finden Sie Informationen dazu, wie Sie Geräte überprüfen, die Sie unter Verwendung von Configuration Manager mit Microsoft Intune konfigurieren können.  

## <a name="vpn-profiles-when-using-configuration-manager"></a>VPN-Profile bei der Verwendung von Configuration Manager  
 Die folgende Tabelle beschreibt die VPN-Profile, die Sie für verschiedene Geräteplattformen konfigurieren können.  

|Verbindungstyp|Windows 8.1|Windows RT|Windows RT 8.1|Windows 10|  
|---------------------|-----------------|----------------|--------------------|----------------|  
|**Cisco AnyConnect**|Nein|Nein|Nein|Nein|  
|**Pulse Secure**|Ja|Nein|Ja|Ja|  
|**F5 Edge Client**|Ja|Nein|Ja|Ja|  
|**Dell SonicWALL Mobile Connect**|Ja|Nein|Ja|Ja|  
|**Prüfpunkt für mobiles VPN**|Ja|Nein|Ja|Ja|  
|**Microsoft SSL (SSTP)**|Ja|Ja|Ja|Nein|  
|**Microsoft Automatic**|Ja|Ja|Ja|Nein|  
|**IKEv2**|Ja|Ja|Ja|Nein|  
|**PPTP**|Ja|Ja|Ja|Nein|  
|**L2TP**|Ja|Ja|Ja|Nein|  

### <a name="next-steps"></a>Nächste Schritte  
 Die folgenden Themen helfen Ihnen beim Planen, Konfigurieren, Betreiben und Warten von VPN-Profilen in Configuration Manager.  

-   [Prerequisites for VPN profiles in System Center Configuration Manager (Voraussetzungen für VPN-Profile in System Center Configuration Manager)](../plan-design/prerequisites-for-wifi-vpn-profiles.md)  

-   [Security and privacy for VPN profiles in System Center Configuration Manager (Sicherheit und Datenschutz für VPN-Profile in System Center Configuration Manager)](../plan-design/security-and-privacy-for-wifi-vpn-profiles.md)
