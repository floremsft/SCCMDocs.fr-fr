---
title: Hardwareinventur Sicherheit und Datenschutz | Microsoft-Dokumentation
description: "Abrufen von Sicherheits- und Datenschutzinformationen für die Hardwareinventur in System Center Configuration Manager."
ms.custom: na
ms.date: 2/22/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 62e20d86-db6d-4a1f-b14a-905a9de31698
caps.latest.revision: "6"
author: andredm7
ms.author: andredm
manager: angrobe
ms.openlocfilehash: ec182ec3102e0f4ae8bcf3d1ef843b25510b6ce6
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="security-and-privacy-for-hardware-inventory-in-system-center-configuration-manager"></a>Sicherheit und Datenschutz für die Hardwareinventur in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Dieses Thema enthält Sicherheits- und Datenschutzinformationen für die Hardwareinventur in System Center Configuration Manager.  

##  <a name="BKMK_Security_HardwareInventory"></a> Bewährte Sicherheitsmethoden für die Hardwareinventur  
 Wenden Sie die folgenden bewährten Sicherheitsmethoden beim Sammeln von Hardwareinventurdaten der Clients an:  

|Bewährte Sicherheitsmethode|Weitere Informationen|  
|----------------------------|----------------------|  
|Signieren und Verschlüsseln von Inventurdaten|Bei der Kommunikation der Clients mit Verwaltungspunkten über HTTPS werden alle von den Clients gesendeten Daten per SSL verschlüsselt. Allerdings werden Clientinventurdaten und gesammelte Dateien möglicherweise nicht signiert und unverschlüsselt gesendet, wenn auf den Clientcomputern HTTP als Protokoll für die Kommunikation mit Verwaltungspunkten im Intranet verwendet wird. Stellen Sie sicher, dass der Standort so konfiguriert ist, dass Signierung und Verschlüsselung erforderlich sind. Wählen Sie zusätzlich die Option "SHA-256 erforderlich" aus, wenn der SHA-256-Algorithmus von den Clients unterstützt wird.|  
|Sammeln Sie IDMIF- und NOIDMIF-Dateien nicht in Umgebungen mit hoher Sicherheit.|Sie können die IDMIF- und NOIDMIF-Dateisammlung verwenden, um die Hardwareinventursammlung zu erweitern. Bei Bedarf werden von Configuration Manager neue Tabellen erstellt oder vorhandene Tabellen in der Configuration Manager-Datenbank geändert, um die Eigenschaften in IDMIF- und NOIDMIF-Dateien zu berücksichtigen. Allerdings überprüft Configuration Manager IDMIF und NOIDMIF-Dateien nicht, sodass diese Dateien zum Ändern von Tabellen verwendet werden können, die nicht geändert werden sollen. Gültige Daten könnten durch ungültige Daten überschrieben werden. Darüber hinaus können große Mengen von Daten hinzugefügt werden, und die Verarbeitung dieser Daten verursacht möglicherweise Verzögerungen in allen Configuration Manager-Funktionen. Zur Verringerung dieser Risiken konfigurieren Sie für die Hardwareinventur-Clienteinstellung **MIF-Dateien sammeln** die Option **Keine**.|  

### <a name="security-issues-for-hardware-inventory"></a>Sicherheitsprobleme bei der Hardwareinventur  
 Das Sammeln der Inventur weist potenzielle Sicherheitslücken auf. Angreifer können die folgenden Aktionen ausführen:  

-   Senden von ungültigen Daten – Diese werden vom Verwaltungspunkt auch dann akzeptiert, wenn die Softwareinventur-Clienteinstellung deaktiviert und keine Dateisammlung aktiviert ist.  

-   Senden von übermäßig großen Datenmengen in einer einzigen Datei und in vielen Dateien – Dies kann zu einem DoS führen.  

-   Zugreifen auf Inventurinformationen während ihrer Übertragung an Configuration Manager  

 Da ein Benutzer mit lokalen Administratorberechtigungen alle Informationen als Inventurdaten senden kann, sollten Sie von Configuration Manager gesammelte Inventurdaten nicht als maßgebliche Datenquelle betrachten.  

 Die Hardwareinventur ist standardmäßig als Clienteinstellung aktiviert.  

##  <a name="BKMK_Privacy_HardwareInventory"></a> Informationen zum Datenschutz für die Hardwareinventur  
 Die Hardwareinventur ermöglicht das Abrufen von Informationen, die auf Configuration Manager-Clients in der Registrierung und in WMI gespeichert sind. Die Softwareinventur ermöglicht die Ermittlung aller Dateien eines bestimmten Typs oder die Sammlung bestimmter Dateien von Clients. Asset Intelligence erweitert die Inventurfunktionen, indem die Hardware- und Softwareinventur erweitert und neue Lizenzverwaltungsfunktionen hinzugefügt werden.  

 Die Hardwareinventur ist standardmäßig als Clienteinstellung aktiviert, und die gesammelten WMI-Informationen werden durch die von Ihnen ausgewählten Optionen festgelegt. Die Softwareinventur ist zwar standardmäßig aktiviert, aber Dateien werden standardmäßig nicht gesammelt. Die Asset Intelligence-Datensammlung ist zwar automatisch aktiviert, aber Sie können die zu aktivierenden Hardwareinventur-Berichtsklassen selbst auswählen.  

 Die Inventurinformationen werden nicht an Microsoft gesendet. Inventurinformationen werden in der Configuration Manager-Datenbank gespeichert. Wenn auf den Clients HTTPS für die Herstellung der Verbindung zu den Verwaltungspunkten verwendet wird, werden die vom Verwaltungspunkt an den Standort gesendeten Inventurdaten während der Übertragung verschlüsselt. Wenn auf den Clients HTTP für die Herstellung der Verbindung zu den Verwaltungspunkten verwendet wird, haben Sie die Möglichkeit, die Inventurverschlüsselung zu aktivieren. In der Datenbank werden die Inventurdaten unverschlüsselt gespeichert. Informationen werden so lange in der Datenbank gespeichert, bis sie durch die alle 90 Tage durchgeführten Standortwartungstasks **Veralteten Inventurverlauf löschen** oder **Veraltete gesammelte Dateien löschen** gelöscht werden. Sie können das Löschintervall konfigurieren.  

 Berücksichtigen Sie bei der Konfiguration der Hardware- und Softwareinventur, der Dateisammlung oder der Asset Intelligence-Datensammlung Ihre Datenschutzanforderungen.  
