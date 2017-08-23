---
title: WLAN- und VPN-Profile Sicherheit und Datenschutz | Microsoft-Dokumentation
description: "Erfahren Sie mehr über bewährte Sicherheitsmethoden für die Verwaltung von WLAN- und VPN-Profilen für Geräte in System Center Configuration Manager."
ms.custom: na
ms.date: 12/28/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ef3ab519-9cf7-47fc-8831-d400e0e96df8
caps.latest.revision: "4"
caps.handback.revision: "0"
author: Nbigman
ms.author: nbigman
manager: angrobe
ms.openlocfilehash: 6d1d0a393a2ce614ae5f819475bd47b05e699b45
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="security-and-privacy-for-wi-fi-and-vpn-profiles-in-system-center-configuration-manager"></a>Sicherheit und Datenschutz für WLAN- und VPN-Profile in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

##  <a name="security-best-practices-for-wi-fi--and-vpn-profiles"></a>Bewährte Sicherheitsmethoden für WLAN- und VPN-Profile  
 Verwenden Sie die folgenden bewährten Sicherheitsmethoden bei der Verwaltung von WLAN- und VPN-Profilen für Geräte.  

|Bewährte Sicherheitsmethode|Weitere Informationen|  
|----------------------------|----------------------|  
|Wählen Sie nach Möglichkeit die sichersten Optionen aus, die von der WLAN- und VPN-Infrastruktur sowie den Clientbetriebssystemen unterstützt werden.|WLAN- und VPN-Profile stellen eine praktische Methode dar, um von Ihren Geräten bereits unterstützte WLAN- und VPN-Einstellungen zentral zu verteilen und zu verwalten. Configuration Manager bietet keine zusätzlichen WLAN- oder VPN-Funktionen.<br /><br /> Bestimmen, implementieren und beachten Sie die bewährten Sicherheitsmethoden, die für Ihre Geräte und die Infrastruktur empfohlen wurden.|  

## <a name="privacy-information-for-wi-fi-profiles"></a>Datenschutzinformationen für WLAN-Profile  
 Sie können WLAN- und VPN-Profile verwenden, um Clientgeräte für die Verbindung mit WLAN- und VPN-Servern zu konfigurieren, und dann auswerten, ob diese Geräte nach der Anwendung der Profile Kompatibilität erreichen. Vom Verwaltungspunkt werden Kompatibilitätsinformationen an den Standortserver gesendet, die dann in der Standortdatenbank gespeichert werden. Die Informationen werden verschlüsselt, wenn sie von Geräten an den Verwaltungspunkt gesendet werden, sie werden aber nicht in einem verschlüsselten Format in der Standortdatenbank gespeichert. Die Informationen verbleiben in der Datenbank, bis sie mit dem Standortwartungstask **Veraltete Konfigurationsverwaltungsdaten löschen** gelöscht werden. Das Löschintervall beträgt standardmäßig 90 Tage, kann aber geändert werden. Die Kompatibilitätsinformationen werden nicht an Microsoft gesendet.  

 Standardmäßig werden WLAN- und VPN-Profile nicht von Geräten ausgewertet. Darüber hinaus müssen Sie die Profile konfigurieren und sie dann für Benutzer bereitstellen.  

 Berücksichtigen Sie vor dem Konfigurieren der WLAN- und VPN-Profile Ihre Datenschutzanforderungen.  
