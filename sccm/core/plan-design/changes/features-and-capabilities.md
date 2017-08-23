---
title: Features und Funktionen | Microsoft-Dokumentation
description: "Erfahren Sie mehr über die primären Verwaltungsfunktionen von System Center Configuration Manager."
ms.custom: na
ms.date: 12/29/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5d388399-07ca-431c-a9b2-56c69771aa87
caps.latest.revision: "18"
caps.handback.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 4691f43dccdf73936107f4635321897b9779bead
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="features-and-capabilities-of-system-center-configuration-manager"></a>Features und Funktionen von System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Im Folgenden finden Sie die primären Verwaltungsfunktionen von System Center Configuration Manager. Für jede Funktion gelten individuelle Voraussetzungen, und die von Ihnen gewünschten Funktionen können sich auf den Entwurf und die Implementierung Ihrer Configuration Manager-Hierarchie auswirken. Wenn Sie beispielsweise Software auf Geräten in Ihrer Hierarchie bereitstellen möchten, müssen Sie die Standortsystemrolle „Verteilungspunkt“ installieren.  

 Weitere Informationen zum Planen und Installieren von Configuration Manager zur Unterstützung dieser Verwaltungsfunktionen in Ihrer Umgebung finden Sie unter [Vorbereiten auf System Center Configuration Manager](../../../core/plan-design/get-ready.md).  

 **Anwendungsverwaltung**  

 Zu dieser Funktion gehören mehrere Tools und Ressourcen, mit denen Sie Anwendungen auf vielen verschiedenen von Ihnen verwalteten Geräten erstellen, verwalten, bereitstellen und überwachen können. Darüber hinaus bietet Configuration Manager Tools, mit denen Sie Ihre Unternehmensdaten in den Apps der Benutzer schützen können. Informationen hierzu finden Sie unter [Einführung in die Anwendungsverwaltung](/sccm/apps/understand/introduction-to-application-management).

 **Zugriff auf Unternehmensressourcen**  

 Zu dieser Funktion gehört eine Reihe von Tools und Ressourcen, mit deren Hilfe Sie Benutzern in Ihrer Organisation Zugriff auf Daten und Anwendungen über Remotestandorte gewähren können. Diese Tools umfassen WLAN-Profile, VPN-Profile, Zertifikatprofile und den bedingten Zugriff auf Exchange und SharePoint Online. Informationen hierzu finden Sie unter [Schützen von Daten und Standortinfrastruktur mit System Center Configuration Manager](../../../protect/understand/protect-data-and-site-infrastructure.md) und [Verwalten des Zugriffs auf Dienste in System Center Configuration Manager](../../../protect/deploy-use/manage-access-to-services.md).  

 **Kompatibilitätseinstellungen**  

 Zu dieser Funktion gehören mehrere Tools und Ressourcen, mit deren Hilfe Sie die Konfigurationskompatibilität von Clientgeräten im Unternehmen bewerten, verfolgen und korrigieren können. Darüber hinaus können Sie Kompatibilitätseinstellungen verwenden, um eine Reihe von Features und Sicherheitseinstellungen auf Geräten zu konfigurieren, die Sie verwalten. Informationen hierzu finden Sie unter [Sicherstellen der Gerätekompatibilität mit System Center Configuration Manager](../../../compliance/understand/ensure-device-compliance.md).  

 **Endpoint Protection**  

 Zu dieser Funktion gehören Verwaltungsfunktionen für Sicherheit, Antischadsoftware und Windows-Firewall für Computer in Ihrem Unternehmen. Informationen hierzu finden Sie unter [Endpoint Protection in System Center Configuration Manager](../../../protect/deploy-use/endpoint-protection.md).  

 **Inventur**  

 Zu dieser Funktion gehören mehrere Tools zum Identifizieren und Überwachen von Beständen:  

-   **Hardwareinventur**: Mit dieser Funktion werden detaillierte Informationen zur Hardware der Geräte in Ihrem Unternehmen gesammelt. Informationen hierzu finden Sie unter [Einführung in die Hardwareinventur in System Center Configuration Manager](../../../core/clients/manage/inventory/introduction-to-hardware-inventory.md).  

-   **Softwareinventur**: Mit dieser Funktion werden Informationen zu den auf Clientcomputern Ihres Unternehmens gespeicherten Dateien gesammelt und entsprechende Berichte erstellt. Informationen hierzu finden Sie unter [Einführung in die Softwareinventur in System Center Configuration Manager](../../../core/clients/manage/inventory/introduction-to-software-inventory.md).  

-   **Asset Intelligence**: Zu dieser Funktion gehören Tools zum Sammeln von Inventurdaten und zur Überwachung von Softwarelizenzen in Ihrem Unternehmen. Informationen hierzu finden Sie unter [Einführung in Asset Intelligence in System Center Configuration Manager](../../../core/clients/manage/asset-intelligence/introduction-to-asset-intelligence.md).  

**Verwaltung mobiler Geräte mit Microsoft Intune**  

 Mit Configuration Manager können Sie iOS-, Android- (einschließlich Samsung KNOX Standard), Windows Phone- und Windows-Geräte mithilfe des Microsoft Intune-Diensts über das Internet verwalten.

 Obwohl Sie den Intune-Dienst verwenden, werden Verwaltungstasks mithilfe der Standortsystemrolle „Dienstverbindungspunkt“ ausgeführt, die über die Configuration Manager-Konsole verfügbar ist. Informationen hierzu finden Sie unter [Hybride Verwaltung mobiler Geräte (MDM) mit System Center Configuration Manager und Microsoft Intune](../../../mdm/understand/hybrid-mobile-device-management.md).  

 **Lokale Verwaltung mobiler Geräte**  

 Registriert und verwaltet PCs und mobile Geräte mithilfe der lokalen Configuration Manager-Infrastruktur und -Verwaltungsfunktionalität, die in die Geräteplattformen integriert ist (anstatt mit einem getrennt installierten Configuration Manager-Client zu arbeiten). Derzeit unterstützt wird die Verwaltung von Windows 10 Enterprise- und Windows 10 Mobile-Geräten. Informationen hierzu finden Sie unter [Verwalten mobiler Geräte mit lokaler Infrastruktur in System Center Configuration Manager](../../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md).  

 **Betriebssystembereitstellung**  

 Zu dieser Funktion gehört ein Tool zum Erstellen von Betriebssystemabbildern. Sie können diese Images verwenden, um die Betriebssysteme mittels PXE-Start oder mithilfe von startfähigen Medien wie CD-Sets, DVDs oder USB-Speichersticks auf Computern bereitzustellen. Beachten Sie, dass dies auch für Computer, die durch Configuration Manager verwaltet werden, sowie für nicht verwaltete Computer gilt. Informationen hierzu finden Sie unter [Einführung in die Bereitstellung von Betriebssystemen in System Center Configuration Manager](../../../osd/understand/introduction-to-operating-system-deployment.md).  

 **Energieverwaltung**  

 Zu dieser Funktion gehören mehrere Tools und Ressourcen, mit denen Sie den Stromverbrauch von Clientcomputern im Unternehmen verwalten und überwachen können. Informationen hierzu finden Sie unter [Einführung in die Energieverwaltung in System Center Configuration Manager](../../../core/clients/manage/power/introduction-to-power-management.md).  

 **Abfragen**  

 Zu dieser Funktion gehört ein Tool, mit dessen Hilfe Sie Informationen zu Ressourcen in Ihrer Hierarchie sowie zu Inventurdaten und Statusmeldungen abrufen können. Anschließend können Sie diese Informationen verwenden, um Berichte zu erstellen, oder Sammlungen von Geräten oder Benutzern für Softwarebereitstellungs- und Konfigurationseinstellungen zu definieren. Informationen hierzu finden Sie unter [Einführung in Abfragen in System Center Configuration Manager](../../../core/servers/manage/introduction-to-queries.md).  

 **Remoteverbindungsprofile**  

 Zu dieser Funktion gehört eine Reihe von Tools und Ressourcen, mit deren Hilfe Sie Remoteverbindungeinstellungen für Geräte in Ihrer Organisation erstellen, bereitstellen und überwachen können. Durch Bereitstellen dieser Einstellungen erleichtern Sie den Benutzern das Herstellen einer Verbindung zu ihren Computern über das Unternehmensnetzwerk. Informationen hierzu finden Sie unter [Arbeiten mit Remoteverbindungsprofile in System Center Configuration Manager](/sccm/compliance/deploy-use/create-remote-connection-profiles).  

 **Konfigurationselemente für Benutzerdaten und -profile**  

 Konfigurationselemente für Benutzerdaten und -profile in Configuration Manager enthalten Einstellungen, mit denen die Ordnerumleitung, Offlinedateien und Roamingprofile auf Computern mit Windows 8 und höher für Benutzer in Ihrer Hierarchie verwaltet werden können. Informationen hierzu finden Sie unter [Arbeiten mit Konfigurationselementen für Benutzerdaten und -profile in System Center Configuration Manager](/sccm/compliance/deploy-use/create-user-data-and-profiles-configuration-items).  

 **Remotesteuerung**  

 Stellt Tools zur Remoteverwaltung von Clientcomputern über die Configuration Manager-Konsole bereit. Informationen hierzu finden Sie unter [Einführung in die Remotesteuerung in System Center Configuration Manager](../../../core/clients/manage/remote-control/introduction-to-remote-control.md).  

 **Berichterstellung**  

 Stellt mehrere Tools und Ressourcen bereit, mit denen Sie die erweiterten Berichterstellungsfunktionen von SQL Server Reporting Services über die Configuration Manager-Konsole nutzen können. Informationen hierzu finden Sie unter [Einführung in die Berichterstellung in System Center Configuration Manager](../../../core/servers/manage/introduction-to-reporting.md).  

 **Softwaremessung**  

 Stellt Tools zum Überwachen und Sammeln von Softwarenutzungsdaten von Configuration Manager-Clients bereit. Informationen finden Sie unter [Überwachen der App-Nutzung mit der Softwaremessung in System Center Configuration Manager](../../../apps/deploy-use/monitor-app-usage-with-software-metering.md).  

 **Softwareupdates**  

 Zu dieser Funktion gehören mehrere Tools und Ressourcen, mit denen Sie Softwareupdates im Unternehmen verwalten, bereitstellen und überwachen können. Informationen hierzu finden Sie unter [Einführung zu Softwareupdates in System Center Configuration Manager](/sccm/sum/understand/software-updates-introduction).  
