---
title: "Auswählen von Intune Standalone oder der hybriden Verwaltung mobiler Geräte (MDM) | Microsoft-Dokumentation"
description: "Wählen Sie aus, ob Sie die hybride Verwaltung mobiler Geräte mit Intune und Configuration Manager bereitstellen oder Intune Standalone ausführen."
ms.custom: na
ms.date: 07/18/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 73ff9bb9-e605-4b68-92a1-487684fed42d
caps.latest.revision: "10"
author: dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: 26c36df77c21254c7ad2b8a45906bd3706f9ec65
ms.sourcegitcommit: 06aef618f72c700f8a716a43fb8eedf97c62a72b
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/21/2017
---
# <a name="choose-between-microsoft-intune-standalone-and-hybrid-mobile-device-management-with-system-center-configuration-manager"></a>Wählen zwischen Microsoft Intune Standalone und der hybriden Verwaltung mobiler Geräte mit System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Eine der am häufigsten gestellten Fragen bezüglich der Verwaltung mobiler Geräte (Mobile Device Management, MDM) mit Microsoft Intune ist folgende: „Sollte ich die hybride Verwaltung mobiler Geräte mit Intune und Configuration Manager bereitstellen oder Intune Standalone in der Konfiguration nur für die Cloud ausführen?“ Um diese Frage zu beantworten, sollten Sie die beiden Optionen sorgfältig gegeneinander abwägen.

## <a name="intune-standalone"></a>Intune Standalone
Intune Standalone ist die empfohlene Bereitstellungstopologie von Microsoft. Intune Standalone ist eine rein cloudbasierte MDM-Lösung, die mithilfe einer Webkonsole verwaltet wird, auf die von überall in der Welt aus zugegriffen werden kann. Intune Rechenzentren werden in Nordamerika, Europa und Asien gehostet. Da Intune ein Clouddienst ist, können Sie die Intune-Verwaltung auf Ihren Geräten in einem relativ kleinen Zeitrahmen bereitstellen.

Die meisten Kunden finden es im Allgemeinen schneller und einfacher, die eigenständige Topologie bereitzustellen, da keine Abhängigkeiten für lokale Komponenten entstehen. Intune Standalone wurde jetzt in die Microsoft Azure-Cloudplattform integriert und bietet viele erweiterte Features, wie z.B. die folgenden:
- Integrierte Verwaltungsplattform für Mobilgeräte in Unternehmen: Cloudplattform und Verwaltungsoberfläche für Intune, Azure AD Premium und Azure Information Protection sind im Azure-Portal integriert.
- Verwaltung mobiler Geräte: umfassende Funktionen für die Verwaltung mobiler Geräte und den Schutz von Informationen.
- Skalierung: Sie können mobile Geräte bereitstellen und verwalten, ohne sich um die Anzahl Gedanken machen zu müssen.
- Rollenbasierte Zugriffssteuerung: Einschränken des Zugriffs auf Verwaltungsfunktionen auf Grundlage zugewiesener Rollen und Bereiche.
- Programmgesteuerter Zugriff (API): Unterstützung für die Microsoft Graph-API plus SDK- und PowerShell-Verwaltungsoptionen.
- Webkonsole: HTML 5-basierte Konsole gemäß Webstandards mit Unterstützung für die meisten modernen Webbrowser.
- Erweiterte Berichtsfunktionen: Erstellen benutzerdefinierter Berichte.
- Agilität: Einfache Einrichtung und schnelle Bereitstellung neuer Funktionen.


## <a name="hybrid-mdm-with-configuration-manager"></a>Hybride Verwaltung mobiler Geräte (Hybrid-MDM) mit Configuration Manager
Hybrid-MDM ist eine Lösung, die die Intune-Funktionen für die Verwaltung mobiler Geräte in Configuration Manager integriert. Die Lösung nutzt Intune als Übermittlungskanal für Richtlinien, Profile und Anwendungen für Geräte und die lokale Infrastruktur von Configuration Manager, um Inhalte zu speichern und die Geräte zu verwalten. Mit einer hybriden Implementierung erhalten Sie eine Steuerzentrale für alle Elemente.  Sie können also dieselbe lokale Infrastruktur und Administratorkonsole sowohl zum Verwalten mobiler Geräte mit Intune als auch zum Verwalten von PCs und Servern mit dem herkömmlichen Configuration Manager-Client verwenden. Folgende Gründe sprechen für die Verwendung einer Hybrid-MDM-Lösung:  
- Sie möchten eine einzige gleiche Verwaltungskonsole für die Verwaltung sowohl von in Intune registrierten Geräten als auch von Geräten verwenden, die über den Configuration Manager-Client verwaltet werden.
- Ihre Infrastruktur erfordert die Verwendung mehrerer NDES-Server für die Zertifikatübermittlung an mobile Geräte.
- Ihre Infrastruktur erfordert die Verwendung von mehreren Exchange-Connectors.
- Sie benötigen Unterstützung für die S/MIME-Verschlüsselung.


## <a name="changing-the-mdm-authority-setting"></a>Ändern der MDM-Autoritätseinstellung
Sie können die MDM-Autorität ohne Unterstützung durch den Microsoft-Support und ohne Aufheben der Registrierung und erneutes Registrieren Ihrer vorhandenen verwalteten Geräte selbst ändern. Einzelheiten finden Sie unter [Umstellen der MDM-Autorität](../deploy-use/change-mdm-authority.md).

> [!NOTE]    
> Um die MDM-Autorität zu Intune Standalone zu ändern, müssen Sie über Configuration Manager Version 1610 oder höher verfügen. Wenn Sie eine frühere Version von Configuration Manager verwenden, können Sie die MDM-Autorität ändern, benötigen dafür aber Unterstützung vom Microsoft-Support und dem Betriebsteam. In diesem Fall müssen Sie nach der Änderung der MDM-Autorität auch die Registrierung aller Geräte aufheben und alle Geräte erneut registrieren.  
