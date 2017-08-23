---
title: "Sicherheit und Datenschutz für die Softwareinventur | Microsoft-Dokumentation"
description: "Rufen Sie Sicherheits- und Datenschutzinformationen für die Softwareinventur in System Center Configuration Manager ab."
ms.custom: na
ms.date: 2/22/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8e68e1fb-a8ec-4543-bb8a-cbbaf184a418
caps.latest.revision: "5"
caps.handback.revision: "0"
author: andredm7
ms.author: andredm
manager: angrobe
ms.openlocfilehash: 7652e46d2168e2de623fa8e6d5b8663701764244
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="security-and-privacy-for-software-inventory-in-system-center-configuration-manager"></a>Sicherheit und Datenschutz für die Softwareinventur in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Dieses Thema enthält Sicherheits- und Datenschutzinformationen für die Softwareinventur in System Center Configuration Manager.  

##  <a name="BKMK_Security_HardwareInventory"></a> Bewährte Sicherheitsmethoden für die Softwareinventur  
 Wenden Sie die folgenden bewährten Sicherheitsmethoden beim Sammeln von Softwareinventurdaten der Clients an:  

|Bewährte Sicherheitsmethode|Weitere Informationen|  
|----------------------------|----------------------|  
|Signieren und Verschlüsseln von Inventurdaten|Bei der Kommunikation der Clients mit Verwaltungspunkten über HTTPS werden alle von den Clients gesendeten Daten per SSL verschlüsselt. Allerdings werden Clientinventurdaten und gesammelte Dateien möglicherweise nicht signiert und unverschlüsselt gesendet, wenn auf den Clientcomputern HTTP als Protokoll für die Kommunikation mit Verwaltungspunkten im Intranet verwendet wird. Stellen Sie sicher, dass der Standort so konfiguriert ist, dass Signierung und Verschlüsselung erforderlich sind. Wählen Sie zusätzlich die Option "SHA-256 erforderlich" aus, wenn der SHA-256-Algorithmus von den Clients unterstützt wird.|  
|Verwenden Sie zum Sammeln wichtiger Dateien oder sensibler Informationen keine Dateisammlung.|Von der Configuration Manager-Softwareinventur werden alle Rechte des Kontos „LocalSystem“ verwendet, mit dem Kopien kritischer Systemdateien, wie z.B. der Registrierung oder von Sicherheitskontodatenbanken, gesammelt werden können. Wenn diese Dateien auf dem Standortserver zur Verfügung stehen, kann eine Person mit Leserechten für Ressourcen oder NTFS-Rechten am Speicherort der Datei den Inhalt analysieren, u. U. wichtige Details des Clients ermitteln und damit die Sicherheit kompromittiert.|  
|Einschränken lokaler Administratorrechte auf Clientcomputern|Ein Benutzer mit lokalen Administratorrechten kann ungültige Daten als Inventurinformationen senden.|  

### <a name="security-issues-for-software-inventory"></a>Sicherheitsprobleme bei der Softwareinventur  
 Das Sammeln der Inventur weist potenzielle Sicherheitslücken auf. Angreifer können die folgenden Aktionen ausführen:  

-   Senden von ungültigen Daten – Diese werden vom Verwaltungspunkt auch dann akzeptiert, wenn die Softwareinventur-Clienteinstellung deaktiviert und keine Dateisammlung aktiviert ist.  

-   Senden von übermäßig großen Datenmengen in einer einzigen Datei und in vielen Dateien – Dies kann zu einem DoS führen.  

-   Zugreifen auf Inventurinformationen während ihrer Übertragung an Configuration Manager  

 Wenn Benutzer wissen, dass sie eine ausgeblendete Datei namens **Skpswi.dat** erstellen und im Stammverzeichnis einer Clientfestplatte speichern können, um sie so aus der Softwareinventur auszuschließen, können Sie von diesem Computer keine Softwareinventurdaten sammeln.  

 Da ein Benutzer mit lokalen Administratorberechtigungen alle Informationen als Inventurdaten senden kann, sollten Sie von Configuration Manager gesammelte Inventurdaten nicht als maßgebliche Datenquelle betrachten.  

 Die Softwareinventur ist standardmäßig als Clienteinstellung aktiviert.  

##  <a name="BKMK_Privacy_HardwareInventory"></a> Informationen zum Datenschutz für die Softwareinventur  
 Die Hardwareinventur ermöglicht das Abrufen von Informationen, die auf Configuration Manager-Clients in der Registrierung und in WMI gespeichert sind. Die Softwareinventur ermöglicht die Ermittlung aller Dateien eines bestimmten Typs oder die Sammlung bestimmter Dateien von Clients. Asset Intelligence erweitert die Inventurfunktionen, indem die Hardware- und Softwareinventur erweitert und neue Lizenzverwaltungsfunktionen hinzugefügt werden.  

 Die Hardwareinventur ist standardmäßig als Clienteinstellung aktiviert, und die gesammelten WMI-Informationen werden durch die von Ihnen ausgewählten Optionen festgelegt. Die Softwareinventur ist zwar standardmäßig aktiviert, aber Dateien werden standardmäßig nicht gesammelt. Die Asset Intelligence-Datensammlung ist zwar automatisch aktiviert, aber Sie können die zu aktivierenden Hardwareinventur-Berichtsklassen selbst auswählen.  

 Die Inventurinformationen werden nicht an Microsoft gesendet. Inventurinformationen werden in der Configuration Manager-Datenbank gespeichert. Wenn auf den Clients HTTPS für die Herstellung der Verbindung zu den Verwaltungspunkten verwendet wird, werden die vom Verwaltungspunkt an den Standort gesendeten Inventurdaten während der Übertragung verschlüsselt. Wenn auf den Clients HTTP für die Herstellung der Verbindung zu den Verwaltungspunkten verwendet wird, haben Sie die Möglichkeit, die Inventurverschlüsselung zu aktivieren. In der Datenbank werden die Inventurdaten unverschlüsselt gespeichert. Informationen werden so lange in der Datenbank gespeichert, bis sie durch die alle 90 Tage durchgeführten Standortwartungstasks **Veralteten Inventurverlauf löschen** oder **Veraltete gesammelte Dateien löschen** gelöscht werden. Sie können das Löschintervall konfigurieren.  

 Berücksichtigen Sie bei der Konfiguration der Hardware- und Softwareinventur, der Dateisammlung oder der Asset Intelligence-Datensammlung Ihre Datenschutzanforderungen.  
