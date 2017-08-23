---
title: "Erste Schritte mit Konformitätseinstellungen | Microsoft-Dokumentation"
description: "Erfahren Sie, wie Sie Kompatibilitätseinstellungen in System Center Configuration Manager verwenden. Lernen Sie außerdem wichtige Konzepte kennen, über die Sie Bescheid wissen müssen."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: a2742d52-851e-4abc-b623-d12d91684c0b
caps.latest.revision: "11"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: f16c87dfd0c4f80d96aedf7f5f7497f2bbd4752a
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="get-started-with-compliance-settings-in-system-center-configuration-manager"></a>Erste Schritte mit Kompatibilitätseinstellungen in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Bevor Sie beginnen, System Center Configuration Manager-Konfigurationselemente zu erstellen, sollten Sie dieses Thema lesen, damit Sie verstehen, wie Kompatibilitätseinstellungen funktionieren, und etwas über die grundlegenden Konzepte erfahren, die Sie kennen müssen.  

## <a name="how-compliance-settings-works"></a>So funktionieren Kompatibilitätseinstellungen  
 Mit den Kompatibilitätseinstellungen können Sie die Konfiguration und Kompatibilität von Servern, Laptops, Desktopcomputern und mobilen Geräten in Ihrer Organisation verwalten.  

 Konfigurationselemente werden in zwei Hauptkategorien unterteilt:  

-   **Einstellungen für Geräte, die mit dem Configuration Manager-Client verwaltet werden**: Diese Geräte sind üblicherweise Geräte, auf denen Sie Configuration Manager-Clientsoftware installiert haben, mit der Sie das jeweilige Gerät verwalten können.  

-   **Einstellungen für Geräte, die ohne den Configuration Manager-Client verwaltet werden**: Diese Geräte sind üblicherweise Geräte, die mit Microsoft Intune oder lokaler Configuration Manager-Geräteverwaltung verwaltet werden.  

## <a name="what-devices-are-supported"></a>Welche Geräte werden unterstützt?  


|Gerätetyp|Weitere Informationen|  
|------------|----------------------|  
|Windows-PCs (mit dem Configuration Manager-Client)|Ermöglicht es Ihnen, benutzerdefinierte Konfigurationselemente zu erstellen, mit denen Sie Elemente wie Registrierungsschlüssel, Dateien und Active Directory-Attribute bewerten können.<br /><br /> Wenn Sie den Windows 10-Konfigurationselementtyp verwenden, wählen Sie die gewünschten Einstellungen in einer vordefinierten Liste aus.|  
|Windows PCs (bei Microsoft Intune registriert)|Wählen Sie die gewünschten Einstellungen in einer vordefinierten Liste aus.|  
|iOS-Geräte (bei Microsoft Intune registriert)|Wählen Sie die gewünschten Einstellungen in einer vordefinierten Liste aus.|  
|Android-Geräte (bei Microsoft Intune registriert)|Wählen Sie die gewünschten Einstellungen in einer vordefinierten Liste aus.|  
|Windows Phone-Geräte (bei Microsoft Intune registriert)|Wählen Sie die gewünschten Einstellungen in einer vordefinierten Liste aus.|  
|Macintosh-Computer (mit dem Configuration Manager-Client)|Ermöglicht es Ihnen, benutzerdefinierte Konfigurationselemente zu erstellen, mit denen Sie Elemente wie Werte für Einstellungen für Mac OS X (Eigenschaftenliste) sowie die Ergebnisse beurteilen können, die von einem Skript zurückgegeben werden.|  
|Macintosh-Computer (bei Microsoft Intune registriert)|Wählen Sie die gewünschten Einstellungen in einer vordefinierten Liste aus.|  

## <a name="what-is-a-configuration-item"></a>Was ist ein Konfigurationselement?  
 Ein Konfigurationselement können Sie sich als Container vorstellen, in dem folgende Informationen gespeichert sind (die Informationen, die Sie konfigurieren, hängen vom Konfigurationselementtyp ab):  

-   **Informationen zur Erkennungsmethode** (für Windows-Konfigurationselemente, die nur Anwendungseinstellungen enthalten): Hieran können Sie feststellen, ob eine Anwendung durch Erkennen der Windows-Installationsdatei für die Anwendung oder mithilfe eines benutzerdefinierten Skripts installiert wird.  

-   **Einstellungen** : Einstellungen stellen die geschäftlichen oder technischen Bedingungen dar, die verwendet werden, um die Kompatibilität von Clientgeräten zu bewerten. Sie können eine neue Einstellung konfigurieren oder eine bestehende Einstellung auf einem Referenzcomputer verwenden.  

-   **Kompatibilitätsregeln** : Mit Kompatibilitätsregeln werden die Bedingungen angegeben, mit denen die Kompatibilität einer Konfigurationselementeinstellung definiert wird. Damit eine Einstellung auf Kompatibilität bewertet werden kann, muss sie über mindestens eine Kompatibilitätsregel verfügen. Einige Einstellungen ermöglichen es Ihnen, Werte zu korrigieren, die als nicht kompatibel ermittelt wurden. Sie können neue Regeln erstellen oder eine vorhandene Einstellung innerhalb eines beliebigen Konfigurationselements suchen, um darin enthaltene Regeln auszuwählen.  

-   **Unterstützte Plattformen** : Dies sind die von Ihnen definierten Geräteplattformen, auf denen das Konfigurationselement auf Kompatibilität ausgewertet wird. Wenn Sie ein Konfigurationselement auf einem Gerät bereitstellen, das nicht in der Liste der unterstützten Plattformen enthalten ist, wird das Gerät nicht auf Kompatibilität bewertet.  

## <a name="what-is-a-configuration-baseline"></a>Was ist eine Konfigurationsbasislinie?  
 Kompatibilität wird durch Definieren einer Konfigurationsbasislinie bewertet, die die zu bewertenden Konfigurationselemente sowie Einstellungen und Regeln enthält, in denen die erforderliche Kompatibilitätsstufe beschrieben wird. Sie können diese Konfigurationsdaten aus dem Internet in Microsoft System Center Configuration Manager-Konfigurationspaketen importieren, bewährte Verfahren, die von Microsoft und anderen Herstellern in Configuration Manager definiert sind, und anschließend in Configuration Manager importieren. Alternativ können Sie neue Konfigurationselemente und Konfigurationsbasislinien erstellen.  

 Nachdem eine Konfigurationsbasislinie definiert ist, kann sie über Sammlungen für Benutzer und Geräte bereitgestellt und entsprechend einem Zeitplan auf Kompatibilität ausgewertet werden. Es ist möglich, mehrere Konfigurationsbasislinien auf einem Gerät bereitzustellen. Dies bietet Ihnen ein hohes Maß an Kontrolle.  

 Von Clientgeräten wird die Kompatibilität anhand jeder zugewiesenen Konfigurationsbasislinie ausgewertet. Die Ergebnisse werden dem Standort sofort über Zustands- und Statusmeldungen gemeldet. Wenn ein Clientgerät derzeit nicht mit einem Netzwerk verbunden ist, aber die Konfigurationselemente, auf die in den bereitgestellten Konfigurationsbasislinien verwiesen wird, bereits heruntergeladen wurden, wird die Konfigurationsbasislinie auf Kompatibilität bewertet. Die Kompatibilitätsinformationen werden beim erneuten Herstellen einer Verbindung gesendet.  

 Im Knoten **Bereitstellungen** des Arbeitsbereichs **Überwachung** in der Configuration Manager-Konsole können Sie die Ergebnisse der Kompatibilitätsbewertung der Konfigurationsbasislinie überwachen. Darin werden die häufigsten Ursachen für Nichtkompatibilität, Fehler und die Anzahl der betroffenen Benutzer und Geräte angezeigt. Sie können auch Berichte für Kompatibilitätseinstellungen ausführen, um zusätzliche Informationen anzuzeigen, z. B. welche Geräte kompatibel bzw. nicht kompatibel sind und welches Element der Konfigurationsbasislinie dazu führt, dass ein Computer nicht kompatibel ist. Sie können die Ergebnisse einer Kompatibilitätsbewertung auch auf Windows-Computern anzeigen, auf denen die Configuration Manager-Clientsoftware ausgeführt wird. Dazu verwenden Sie die Registerkarte **Konfigurationen** in **Configuration Manager** in der Systemsteuerung.  

## <a name="user-data-and-profiles-configuration-items"></a>Konfigurationselemente für Benutzerdaten und Profile  
 Konfigurationselemente für Benutzerdaten und Profile enthalten Einstellungen, mit denen gesteuert wird, wie Benutzer in einer Hierarchie die Ordnerumleitung, Offlinedateien und servergespeicherten Profile auf Computern mit Windows 8 und höher verwalten. Sie können diese Konfigurationselemente für Benutzersammlungen bereitstellen und dann deren Kompatibilität in der Configuration Manager-Konsole im Knoten **Überwachung** überwachen. Im Gegensatz zu anderen Konfigurationselementen fügen Sie diese nicht zu Konfigurationsbasislinien hinzu, bevor Sie sie bereitstellen. Sie können die Konfigurationselemente direkt über das Dialogfeld **Konfigurationselemente für Benutzerdaten und Profile bereitstellen** bereitstellen.  

 Ausführlichere Informationen finden Sie unter [Erstellen von Konfigurationselementen für Benutzerdaten und -profile](/sccm/compliance/deploy-use/create-user-data-and-profiles-configuration-items).  

## <a name="remote-connection-profiles"></a>Remoteverbindungsprofile  
 Remoteverbindungsprofile stellen eine Reihe von Tools und Ressourcen zur Verfügung, mit deren Hilfe Sie Remoteverbindungeinstellungen für Geräte in Ihrer Organisation erstellen, bereitstellen und überwachen können. Durch Bereitstellen dieser Einstellungen erleichtern Sie den Endbenutzern das Herstellen einer Verbindung mit dem Unternehmensnetzwerk.  

Ausführlichere Informationen finden Sie unter [Erstellen von Remoteverbindungsprofilen](/sccm/compliance/deploy-use/create-remote-connection-profiles).  

## <a name="windows-edition-upgrade"></a>Upgrade von Windows-Edition
Die Upgraderichtlinie für die Edition ermöglicht das automatische Upgrade von Geräten, die bestimmte Versionen von Windows 10 ausführen, auf eine neuere Version durch Bereitstellung eines neuen Produktschlüssels oder einer Lizenzdatei.

Ausführlichere Informationen finden Sie unter [Upgrade Windows devices with the edition upgrade policy (Einstellungen der Upgraderichtlinie für die Windows-Edition in Microsoft Intune)](/sccm/compliance/deploy-use/upgrade-windows-version)
