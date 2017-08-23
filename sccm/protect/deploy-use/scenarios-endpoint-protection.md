---
title: "Szenario: Endpoint Protection schützt Computer vor Schadsoftware | Microsoft Docs"
description: "Erfahren Sie mehr über das Implementieren von Endpoint Protection in Configuration Manager, um Computer vor Angriffen durch Schadsoftware zu schützen."
ms.custom: na
ms.date: 03/13/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 539c7a89-3c03-4571-9cb4-02d455064eeb
caps.latest.revision: "8"
author: NathBarn
ms.author: nathbarn
manager: angrobe
ms.openlocfilehash: b98684d44874ff246e4d675039c6e443aee82a62
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="example-scenario-using-system-center-endpoint-protection-to-protect-computers-from-malware-in-system-center-configuration-manager"></a>Beispielszenario: Verwenden von Endpoint Protection zum Schutz von Computern vor Schadsoftware in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Diese Thema enthält ein Beispielszenario zur Implementierung der Endpoint Protection in Configuration Manager, um Computer in einer Organisation vor Angriffen durch Schadsoftware zu schützen.  

 John ist Configuration Manager-Administrator bei der Woodgrove Bank. Derzeit verwendet die Bank System Center Endpoint Protection für den Schutz der Computer vor Angriffen durch Schadsoftware. Darüber hinaus verwendet die Bank Windows-Gruppenrichtlinien, um sicherzustellen, dass die Windows-Firewall auf allen Computern im Unternehmen aktiviert ist und Benutzer benachrichtigt werden, wenn die Windows-Firewall ein neues Programm blockiert.  

 John soll ein Upgrade für die Antischadsoftware der Woodgrove Bank auf System Center Endpoint Protection durchführen, sodass die Bank die neuesten Antischadsoftware-Features nutzen und die Antischadsoftware-Lösung über die Configuration Manager-Konsole verwalten kann. Diese Implementierung setzt Folgendes voraus:  

-   Verwendung von Configuration Manager zum Verwalten der Einstellungen der Windows-Firewall, die derzeit von der Gruppenrichtlinie verwaltet werden  

-   Verwendung von Configuration Manager-Softwareupdates zum Herunterladen von Schadsoftwaredefinitionen auf Computer. Wenn Softwareupdates nicht verfügbar sind, z. B. für den Fall, dass der Computer nicht mit dem Unternehmensnetzwerk verbunden ist, müssen Computer die Definitionsupdates über Microsoft Update herunterladen.  

-   Tägliche Ausführung einer schnellen Prüfung auf Schadsoftware auf den Computern der Benutzer. Server müssen hingegen jeden Samstag um 1 Uhr morgens (außerhalb der Geschäftszeiten) eine vollständige Prüfung durchführen.  

-   Senden einer E-Mail-Warnung für folgende Ereignisse:  

    -   Schadsoftware wird auf einem der Computer erkannt.  

    -   Dieselbe Bedrohung durch Schadsoftware wird auf mehr als 5 Prozent der Computer gefunden.  

    -   Dieselbe Bedrohung durch Schadsoftware wurde innerhalb von 24 Stunden mehr als fünfmal gefunden.  

    -   Mehr als drei unterschiedliche Arten von Schadsoftware wurden innerhalb von 24 Stunden gefunden.  

-   Deinstallation der vorhanden Antischadsoftware-Lösung.  

 John führt dann die folgenden Schritte zur Implementierung von Endpoint Protection aus:  

##  <a name="steps-to-implement-endpoint-protection"></a>Schritte zum Implementieren von Endpoint Protection  

|Prozess|Reference|  
|-------------|---------------|  
|John liest die verfügbaren Informationen zu den grundlegenden Konzepten für Endpoint Protection in Configuration Manager.|Weitere Informationen zu Endpoint Protection finden Sie unter [Endpoint Protection in System Center Configuration Manager](endpoint-protection.md).|  
|John überprüft und implementiert die erforderlichen Voraussetzungen zur Verwendung von Endpoint Protection.|Informationen zu den erforderlichen Komponenten für Endpoint Protection finden Sie unter [Planung für Endpoint Protection](../plan-design/planning-for-endpoint-protection.md).|  
|John installiert die Endpoint Protection-Standortsystemrolle nur auf einem Standortsystemserver, der sich in der Hierarchie der Woodgrove Bank an höchster Stelle befindet.|Weitere Informationen zum Installieren der Endpoint Protection-Standortsystemrolle finden Sie unter „Voraussetzungen“ in [Konfigurieren von Endpoint Protection](configure-endpoint-protection.md).|  
|John konfiguriert Configuration Manager für die Verwendung eines SMTP-Servers zum Senden der E-Mail-Warnungen.<br /><br /> **Hinweis**: Ein SMTP-Server muss nur konfiguriert werden, wenn Sie per E-Mail benachrichtigt werden möchten, falls eine Endpoint Protection-Warnung generiert wird.|Weitere Informationen finden Sie unter [Configure alerts in Endpoint Protection (Konfigurieren von Warnungen in Endpoint Protection)](endpoint-configure-alerts.md).|  
|John erstellt eine Gerätesammlung, die alle Computer und Server für die Installation des Endpoint Protection-Clients enthält. Er weist dieser Sammlung den Namen **Alle durch Endpoint Protection geschützten Computer** zu.<br /><br /> **Tipp:** Es können keine Warnungen für Benutzersammlungen konfiguriert werden.|Weitere Informationen zum Erstellen von Sammlungen finden Sie unter [Erstellen von Sammlungen in System Center Configuration Manager](../../core/clients/manage/collections/create-collections.md)|  
|Er konfiguriert die folgenden Warnungen für die Sammlung: <br /><br />1) **Schadsoftware wurde erkannt**: John konfiguriert den Warnungsschweregrad **Kritisch**. <br /><br />2) **Derselbe Schadsoftwaretyp wird auf mehreren Computern erkannt**: John konfiguriert den Warnungsschweregrad **Kritisch** und gibt an, dass die Warnung generiert wird, wenn auf mehr als 5 Prozent der Computer Schadsoftware entdeckt wurde. <br /><br />3) **Derselbe Schadsoftwaretyp wird im angegebenen Intervall wiederholt auf einem Computer erkannt**: John konfiguriert den Warnungsschweregrad **Kritisch** und gibt an, dass die Warnung generiert wird, wenn in einem Zeitraum von 24 Stunden mehr als fünf Mal Schadsoftware erkannt wurde. <br /><br />4) **Verschiedene Schadsoftwaretypen wurden innerhalb eines angegebenen Intervalls auf demselben Computer erkannt**: John konfiguriert den Warnungsschweregrad **Kritisch** und gibt an, dass die Warnung generiert wird, wenn in einem Zeitraum von 24 Stunden mehr als drei Arten von Schadsoftware generiert wurden.<br /><br /> Der Wert für **Warnungsschweregrad** gibt die Warnungsebene an, die in der Configuration Manager-Konsole und in Warnungen angezeigt wird, die er in einer E-Mail empfängt.<br /><br /> Außerdem aktiviert er die Option **Diese Sammlung im Endpoint Protection-Dashboard anzeigen**, damit er die Warnungen in der Configuration Manager-Konsole überwachen kann.|Weitere Informationen finden Sie unter „Konfigurieren von Warnungen für Endpoint Protection“ in [Konfigurieren von Endpoint Protection in System Center Configuration Manager](endpoint-configure-alerts.md).|  
|John konfiguriert Configuration Manager-Softwareupdates, um drei Mal täglich mithilfe einer automatischen Bereitstellungsregel Definitionsupdates herunterzuladen und bereitzustellen.|Weitere Informationen finden Sie unter „Verwenden von Configuration Manager-Softwareupdates zum Bereitstellen von Definitionsupdates“ in [Use Configuration Manager software updates to deliver definition updates (Verwenden von Configuration Manager-Softwareupdates zum Bereitstellen von Definitionsupdates)](endpoint-definitions-configmgr.md).|  
|John überprüft die Einstellungen in der Standardrichtlinie für Antischadsoftware, die von Microsoft empfohlene Sicherheitseinstellungen enthält. Damit Computer täglich eine schnelle Überprüfung durchführen können, ändert er die folgenden Einstellungen:<br /><br /> 1) **Täglich eine Schnellüberprüfung auf Clientcomputern ausführen**: **Ja**.<br /><br /> 2) **Geplante Zeit für tägliche Schnellüberprüfung**: **9:00 Uhr**.<br /><br /> John bemerkt, dass **Von Microsoft Update verteilte Updates** standardmäßig als Quelle von Definitionsupdates ausgewählt ist. Dies erfüllt die Unternehmensanforderung, dass Computer Definitionen von Microsoft Update herunterladen, wenn sie keine Configuration Manager-Softwareupdates empfangen können.|Siehe [Erstellen und Bereitstellen von Richtlinien für Antischadsoftware für Endpoint Protection in System Center Configuration Manager](endpoint-antimalware-policies.md).|  
|John erstellt eine Sammlung, die nur die Woodgrove Bank-Server namens **Woodgrove Bank-Server**enthält.|Informationen hierzu finden Sie unter [Erstellen von Sammlungen in System Center Configuration Manager](../../core/clients/manage/collections/create-collections.md).|  
|John erstellt eine benutzerdefinierte Richtlinie für Antischadsoftware namens **Woodgrove Bank-Serverrichtlinie**. Er fügt nur die Einstellungen für **Geplante Überprüfung** hinzu und nimmt folgende Änderungen vor:<br /><br /> **Überprüfungstyp**:  **Vollständig**<br /><br /> **Überprüfungstag**:  **Samstag**<br /><br /> **Überprüfungszeit**: **1:00 Uhr**<br /><br /> **Täglich eine Schnellüberprüfung auf Clientcomputern ausführen**:  **Nein**.|Siehe [Erstellen und Bereitstellen von Richtlinien für Antischadsoftware für Endpoint Protection in System Center Configuration Manager](endpoint-antimalware-policies.md).|  
|John stellt die benutzerdefinierte Richtlinie für Antischadsoftware **Woodgrove Bank-Richtlinie** für die Sammlung **Woodgrove Bank-Server** bereit.|Informationen hierzu finden Sie unter „So stellen Sie eine Richtlinie für Antischadsoftware für Clientcomputer bereit“ im Thema [Erstellen und Bereitstellen von Richtlinien für Antischadsoftware für Endpoint Protection](endpoint-antimalware-policies.md).|  
|John erstellt einen neuen Satz von benutzerdefinierten Einstellungen für Clientgeräte für Endpoint Protection und nennt diese **Woodgrove Bank Endpoint Protection-Einstellungen**.<br /><br /> **Hinweis:** Wenn Sie Endpoint Protection nicht auf allen Clients in Ihrer Hierarchie installieren und aktivieren möchten, stellen Sie sicher, dass die Optionen **Endpoint Protection-Client auf Clientcomputern verwalten** und **Endpoint Protection-Client auf Clientcomputern installieren** in den Standardeinstellungen für den Client mit **Nein** konfiguriert sind.|Weitere Informationen finden Sie unter [Konfigurieren Sie benutzerdefinierte Clienteinstellungen für Endpoint Protection](endpoint-protection-configure-client.md).|  
|Er konfiguriert die folgenden Einstellungen für Endpoint Protection:<br /><br /> **Endpoint Protection-Client auf Clientcomputern verwalten**aus:  **Ja**<br /><br /> Diese Einstellung und der entsprechende Wert stellen sicher, dass jeder vorhandene Endpoint Protection-Client, der installiert ist, von Configuration Manager verwaltet wird.<br /><br /> **Endpoint Protection-Client auf Clientcomputern installieren**:  **Ja**.<br /><br /> **Vor der Installation von Endpoint Protection zuvor installierte Antischadsoftware anderer Hersteller automatisch entfernen**:  **Ja**.<br /><br /> Diese Einstellung und der entsprechende Wert erfüllen die Unternehmensanforderung, dass die vorhandene Antischadsoftware entfernt wird, bevor Endpoint Protection installiert und aktiviert wird.|Weitere Informationen finden Sie unter [Konfigurieren Sie benutzerdefinierte Clienteinstellungen für Endpoint Protection](endpoint-protection-configure-client.md).|  
|John stellt die Clienteinstellungen für **Woodgrove Bank Endpoint Protection-Einstellungen** für die Sammlung **Alle durch Endpoint Protection geschützten Computer** bereit.|Weitere Informationen finden Sie unter „Konfigurieren Sie benutzerdefinierte Clienteinstellungen für Endpoint Protection“ in [Konfigurieren von Endpoint Protection in Configuration Manager](endpoint-antimalware-policies.md).|  
|John verwendet den Assistenten zum Erstellen von Windows-Firewall-Richtlinien, um eine Richtlinie zu erstellen, indem die folgenden Einstellungen für das Domänenprofil konfiguriert werden:<br /><br /> 1) **Windows Firewall aktivieren**: **Ja**<br /><br /> 2)<br />                    **Benutzer benachrichtigen, wenn ein neues Programm von der Windows-Firewall blockiert wird**: **Ja**|Informationen hierzu finden Sie unter [Erstellen und Bereitstellen von Windows-Firewall-Richtlinien für Endpoint Protection in System Center Configuration Manager](../../protect/deploy-use/create-windows-firewall-policies.md).|  
|John stellt die neue Firewallrichtlinie für die Sammlung **Alle durch Endpoint Protection geschützten Computer** bereit, die er zuvor erstellt hat.|Weitere Informationen finden Sie unter „So stellen Sie eine Windows-Firewall-Richtlinie bereit“ in [Erstellen und Bereitstellen von Windows-Firewall-Richtlinien für Endpoint Protection in System Center Configuration Manager](create-windows-firewall-policies.md).|  
|John verwendet die verfügbaren Verwaltungsaufgaben für Endpoint Protection, um Antischadsoftware und Windows-Firewallrichtlinien zu verwalten, bedarfsgesteuerte Überprüfungen von Computern durchzuführen und auf Computern zu erzwingen, dass die neuesten Definitionen heruntergeladen werden. Außerdem werden sie dazu verwendet, um weitere Maßnahmen anzugeben, die bei der Erkennung von Schadsoftware eingeleitet werden.|Informationen hierzu finden Sie unter [Verwalten von Richtlinien für Antischadsoftware und Firewalleinstellungen für Endpoint Protection in System Center Configuration Manager](endpoint-antimalware-firewall.md).|  
|John verwendet die folgenden Methoden zum Überwachen des Status von Endpoint Protection und der von Endpoint Protection durchzuführenden Aktionen:<br /><br /> 1) Mithilfe des Knotens **Endpoint Protection-Status** unter **Sicherheit** im Arbeitsbereich **Überwachung**<br /><br /> 2) Mithilfe des Knotens **Endpoint Protection** im Arbeitsbereich **Bestand und Kompatibilität**<br /><br /> 3) Mithilfe der integrierten Configuration Manager-Berichte|Informationen finden Sie unter [Überwachen von Endpoint Protection in System Center Configuration Manager](monitor-endpoint-protection.md).|  

 John meldet seinem Vorgesetzten eine erfolgreiche Implementierung von Endpoint Protection und bestätigt, dass die Computer der Woodgrove Bank jetzt gemäß den angegebenen Unternehmensanforderungen vor Antischadsoftware geschützt sind.
