---
title: "Übliche Tasks für die Konformitätsverwaltung von clientverwalteten Geräten | Microsoft-Dokumentation"
description: "Erfahren Sie mehr über System Center Configuration Manager-Kompatibilitätseinstellungen, indem Sie einige Szenarios durcharbeiten."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4e345791-74db-41ad-b472-024ce6521daf
caps.latest.revision: "8"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 2012ab5e55da8d707fd668e0163b42fe7d56c72f
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="common-tasks-for-managing-compliance-on-devices-with-the-system-center-configuration-manager-client"></a>Allgemeine Aufgaben zur Verwaltung der Kompatibilität auf Geräten mit dem System Center Configuration Manager-Client

*Gilt für: System Center Configuration Manager (Current Branch)*

Die Szenarios in diesem Thema dienen zur Einführung in das Verwenden der System Center Configuration Manager-Kompatibilitätseinstellungen, indem Sie einige gängige Szenarios durcharbeiten, die auftreten könnten.  

 Wenn Sie bereits mit den Kompatibilitätseinstellungen vertraut sind, finden Sie eine ausführliche Dokumentation zu allen verwendbaren Features im Abschnitt [Konfigurationselemente für Geräte, die mit dem System Center Configuration Manager-Client verwaltet werden](../../compliance/deploy-use/configuration-items-for-devices-managed-with-the-client.md).  

 Bevor Sie beginnen, lesen Sie [Erste Schritte mit Kompatibilitätseinstellungen](../../compliance/get-started/get-started-with-compliance-settings.md), um einige Grundlagen der Kompatibilitätseinstellungen zu erfahren, und lesen Sie zudem [Planen und Konfigurieren von Kompatibilitätseinstellungen](../../compliance/plan-design/plan-for-and-configure-compliance-settings.md), um jegliche notwendigen Voraussetzungen zu implementieren.  

## <a name="general-information-for-each-scenario"></a>Allgemeine Informationen für jedes Szenario  
 In jedem Szenario erstellen Sie ein Konfigurationselement, das eine bestimmte Aufgabe ausführt. Öffnen Sie den Assistenten zum Erstellen von Konfigurationselementen, und führen Sie die folgenden Schritte aus:  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Bestand und Kompatibilität** > **Kompatibilitätseinstellungen** > **Konfigurationselemente**.  

3.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Erstellen** auf **Konfigurationselement erstellen**.  

4.  Geben Sie auf der Registerkarte **Allgemein** des nachstehend gezeigten Assistenten zum Erstellen von Konfigurationselementen einen Namen und eine Beschreibung des Konfigurationselements an. Wählen Sie dann den für jedes Szenario geeigneten Konfigurationselementtyp.  

     ![Zeigt die Seite „Allgemein“ des Assistenten zum Erstellen von Konfigurationselementen](/sccm/compliance/plan-design/media/Compliance-Settings-Wizard---1.png)  

## <a name="scenarios-for-windows-10-devices-managed-with-the-configuration-manager-client"></a>Szenarien für Windows 10-Geräte, die mit dem Configuration Manager-Client verwaltet werden  

### <a name="scenario-disable-the-use-of-bluetooth-on-windows-10-devices"></a>Szenario: Deaktivieren von Bluetooth auf Windows 10-Geräten  
 In diesem Szenario hat Ihre Sicherheitsabteilung festgestellt, dass die Bluetooth-Funktion auf Geräten als Mittel genutzt werden kann, um vertrauliche Unternehmensdaten aus dem Unternehmen zu schmuggeln. Sie haben vor Kurzem alle Ihre PCs auf Windows 10 aktualisiert und sich entschieden, die Bluetooth-Funktion auf diesen Geräten zu deaktivieren.  

1.  Wählen Sie im Assistenten zum Erstellen von Konfigurationselementen auf der Seite **Allgemein** den Konfigurationselementtyp **Windows 10** aus, und klicken Sie auf **Weiter**.  

2.  Wählen Sie auf der Seite **Unterstützte Plattformen** des Assistenten alle Windows 10-Plattformen aus.  

3.  Wählen Sie auf der Seite **Geräteeinstellungen** die Option **Gerät**aus, und klicken Sie dann auf **Weiter**.  

4.  Wählen Sie auf der Seite **Sicherheit** die Option **Nicht zulässig** als Einstellung für **Bluetooth**aus.  

5.  Wählen Sie **Nicht kompatible Einstellungen wiederherstellen** aus, um sicherzustellen, dass die Änderung auf alle Windows 10-Geräte angewendet wird.  

6.  Schließen Sie den Assistenten ab, um das neue Konfigurationselement zu erstellen.  

 Sie können nun die Informationen im Thema [Allgemeine Aufgaben zum Erstellen und Bereitstellen von Konfigurationsbaselines mit System Center Configuration Manager](../../compliance/plan-design/common-tasks-for-creating-and-deploying-configuration-baselines.md) verwenden, die Ihnen beim Bereitstellen der von Ihnen erstellten Konfiguration auf Geräten helfen.  

## <a name="scenarios-for-windows-desktop-and-server-computers-managed-with-the-configuration-manager-client"></a>Szenarien für Windows-Desktop- und -Servercomputer, die mit dem Configuration Manager-Client verwaltet werden  
 Auf Macintosh-Computern mit ausgeführtem Configuration Manager-Client haben Sie zwei Optionen zur Bewertung der Kompatibilität:  

-   Auswerten einer Datei mit Einstellungen für Mac OS X (.plist)  

-   Verwenden eines benutzerdefinierten Skripts und Auswerten der vom Skript zurückgegeben Ergebnisse  

 Mehr Informationen finden Sie unter [Erstellen von Konfigurationselementen für Mac OS X-Geräte, die mit dem System Center Configuration Manager-Client verwaltet werden](../../compliance/deploy-use/create-configuration-items-for-mac-os-x-devices-managed-with-the-client.md).  

### <a name="scenario-remediate-an-incorrect-registry-value-on-windows-desktop-computers"></a>Szenario: Wiederherstellen eines falschen Registrierungswerts auf Windows-Desktopcomputern  
 In diesem Szenario erkennen Sie, dass eine wichtige Sparten-App auf einigen von Ihnen verwalteten Computern mit Windows 8.1. nicht ordnungsgemäß funktioniert. Die Untersuchung ergibt, dass der Wert des Registrierungsschlüssels **HKEY_LOCAL_MACHINE\SOFTWARE\Woodgrove\LOB App\Configuration\Configuration1** auf einigen Computern auf **0** festgelegt ist. Damit die Sparten-App ordnungsgemäß funktioniert, muss dieser Wert auf **1**festgelegt werden.  

 Bei diesem Verfahren erstellen Sie ein Konfigurationselement, das eine Überwachung auf falsche Registrierungsschlüsselwerte vornimmt und diese automatisch korrigiert.  

1.  Wählen Sie im Assistenten zum Erstellen von Konfigurationselementen auf der Seite **Allgemein** den Konfigurationselementtyp **Windows-Desktop oder -Server (benutzerdefiniert)** aus, und klicken Sie auf **Weiter**.  

2.  Wählen Sie auf der Seite **Unterstützte Plattformen** des Assistenten **Windows 8.1** aus (um sicherzustellen, dass das Konfigurationselement nur für betroffene Computer gilt).  

3.  Klicken Sie auf der Seite **Einstellungen** auf **Neu** , um eine neue Einstellung zu erstellen.  

4.  Konfigurieren Sie auf der Registerkarte **Allgemein** des Dialogfelds **Einstellung erstellen** die folgenden Informationen:  

    -   **Name** > **Beispieleinstellung**  

    -   **Einstellungstyp** > **Registrierungswert**  

    -   **Datentyp** > **Ganze Zahl** (da der Wert nur eine Zahl enthält)  

    -   **Struktur** > **HKEY_LOCAL_MACHINE**  

    -   **Schlüssel** > **SOFTWARE\Woodgrove\LOB App\Configuration\Configuration1**  

    -   **Wert** > **1** (der erforderliche Wert)  

5.  Klicken Sie im Dialogfeld **Einstellung erstellen** auf der Registerkarte **Kompatibilitätsregeln** auf **Neu**, und konfigurieren Sie dann im Dialogfeld **Regel erstellen** Folgendes:  

    -   **Name** > **Beispielregel**  

    -   **Ausgewählte Einstellung** – Überprüfen, ob die ausgewählte Einstellung **Beispieleinstellung**ist.  

    -   **Regeltyp** > **Wert**  

    -   **Die folgende Regel muss von der Einstellung erfüllt werden** – Stellen Sie sicher, dass der Name der Einstellung richtig ist, und konfigurieren Sie die Option, um anzugeben, dass der Einstellungswert **1**sein muss.  

    -   **Nicht kompatible Regeln wiederherstellen, falls dies unterstützt wird** – Aktivieren Sie dieses Kontrollkästchen, um sicherzustellen, dass Configuration Manager den Wert des Registrierungsschlüssels auf den richtigen Wert zurücksetzt, wenn er falsch ist.  

6.  Schließen Sie den Assistenten ab, um das neue Konfigurationselement zu erstellen.  

 Sie können nun die Informationen im Thema [Allgemeine Aufgaben zum Erstellen und Bereitstellen von Konfigurationsbaselines](../../compliance/plan-design/common-tasks-for-creating-and-deploying-configuration-baselines.md) verwenden, die Ihnen beim Bereitstellen der von Ihnen erstellten Konfiguration auf Geräten helfen.  
