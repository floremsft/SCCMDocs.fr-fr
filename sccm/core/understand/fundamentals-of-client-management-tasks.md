---
title: Grundlagen der Clientverwaltung | Microsoft-Dokumentation
description: "Erfahren Sie mehr über Tasks, die Sie für die Verwaltung von System Center Configuration Manager-Clients ausführen können."
ms.custom: na
ms.date: 12/30/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8d4e5641-354e-4439-8b4f-620a760e233d
caps.latest.revision: "4"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 0fee4f4ba462e59859ac93c4218b67cb26bdd6f6
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="fundamentals-of-client-management-tasks-for-system-center-configuration-manager"></a>Grundlagen der Clientverwaltungsaufgaben für System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Nach der Installation von System Center Configuration Manager-Clients können Sie verschiedene Tasks zur Verwaltung der Clients ausführen.  Einige dieser Tasks werden über die Configuration Manager-Konsole ausgeführt. Andere Tasks werden über die Configuration Manager-Clientanwendung ausgeführt. Die Configuration Manager-Clientanwendung wird mit der Configuration Manager-Clientsoftware installiert.

## <a name="configuration-manager-console-tasks"></a>Tasks der Configuration Manager-Konsole
 In der Configuration Manager-Konsole können Sie verschiedene Clientverwaltungstasks ausführen:  

-   Bereitstellen von Anwendungen, Softwareupdates, Wartungsskripts und Betriebssystemen. Konfigurieren der Installation zur Ausführung zu einem bestimmten Termin, Bereitstellen der Software für die Installation an Benutzer auf Anforderung, oder Konfigurieren von Anwendungen zur Deinstallation.  

-   Schutz der Computer vor Schadsoftware und Sicherheitsrisiken sowie Ausgeben einer Warnung, wenn Probleme erkannt werden  

-   Definieren von Clientkonfigurationseinstellungen, die Sie überwachen und bei fehlender Konformität wiederherstellen möchten.  

-   Sammeln von Hardware- und Softwareinventurinformationen, darunter die Überwachung und Abstimmung von Lizenzinformationen von Microsoft  

-   Problembehandlung auf Computern mit der Remotesteuerung.  

-   Implementieren von Energieverwaltungseinstellungen zum Verwalten und Überwachen des Stromverbrauchs von Computern  

Die Configuration Manager-Konsole überwacht die vorherigen Tasks nahezu in Echtzeit. In der Configuration Manager-Konsole sind Benachrichtigungen und Statusinformationen zu jedem Task verfügbar. Verwenden Sie zum Erfassen von Daten und Auswerten historischer Trends die integrierten Berichterstattungsfunktionen von SQL Reporting Services. Clients senden Informationen als Clientstatus an den Standort.  Clientstatusinformationen liefern Daten über die Integrität des Clients sowie die Clientaktivität, und werden in der Konsole oder mithilfe der integrierten Berichte für Configuration Manager angezeigt. Mithilfe dieser Daten können Sie Computer identifizieren, die nicht reagieren, und in einigen Fällen Probleme automatisch beheben.  

 Weitere Informationen zu den Verwaltungsaufgaben für Clients finden Sie unter [Verwalten von Clients in System Center Configuration Manager](../../core/clients/manage/manage-clients.md) und [Verwalten von Clients für Linux- und UNIX-Server in System Center Configuration Manager](../../core/clients/manage/manage-clients-for-linux-and-unix-servers.md). Informationen zur Verwendung von Berichten finden Sie unter   
            [Einführung in die Berichterstellung in System Center Configuration Manager](../../core/servers/manage/introduction-to-reporting.md).  

## <a name="configuration-manager-client-application"></a>Configuration Manager-Clientanwendung  
 Wenn Sie die Configuration Manager-Clientsoftware installieren, wird die Configuration Manager-Clientanwendung ebenfalls installiert. Im Gegensatz zum Softwarecenter ist die Configuration Manager-Clientanwendung nicht für Endbenutzer bestimmt, sondern für den Helpdesk. Einige Konfigurationsoptionen erfordern lokale Administratorberechtigungen, und für die meisten Optionen sind technische Kenntnisse der Funktionsweise der Configuration Manager-Clientanwendung erforderlich. Sie können diese Anwendung verwenden, um auf einem Client die folgenden Aufgaben auszuführen:  

-   Anzeigen von Eigenschaften des Clients, z.B. die Buildnummer, der zugewiesene Standort, mit welchem Verwaltungspunkt der Client kommuniziert, und ob ein Public Key Infrastructure-Zertifikat (PKI) oder ein selbstsigniertes Zertifikat verwendet wird.  

-   Bestätigen Sie, dass der Client erfolgreich eine Clientrichtlinie heruntergeladen hat, nachdem der Client zum ersten Mal installiert wurde. Bestätigen Sie ebenfalls, dass die Clienteinstellungen wie erwartet aktiviert oder deaktiviert sind, entsprechend den Clienteinstellungen, die in der Configuration Manager-Konsole konfiguriert wurden.  

-   Starten Sie die Clientaktionen. Laden Sie z.B. die Clientrichtlinie herunter, wenn eine Änderung der Konfiguration in der Configuration Manager-Konsole vorgenommen wurde, und Sie nicht auf den nächsten geplanten Download warten möchten.  

-   Weisen Sie manuell einen Client zu einem Configuration Manager-Standort zu, oder suchen Sie nach einem Standort. Geben Sie dann das Domain Name System-Suffix (DNS) für Verwaltungspunkte an, die in DNS veröffentlichen.  

-   Konfigurieren Sie den Clientcache, in dem Dateien vorübergehend gespeichert werden. Löschen Sie anschließend Dateien im Cache, wenn Sie mehr Speicherplatz zum Installieren von Software benötigen.  

-   Konfigurieren von Einstellungen für die internetbasierte Clientverwaltung  

-   Anzeigen von Konfigurationsbasislinien, die auf dem Client bereitgestellt wurden, Initiieren der Kompatibilitätsauswertung und Anzeigen von Kompatibilitätsberichten  
