---
title: "Integritätsnachweis | Microsoft-Dokumentation"
description: "Erfahren Sie mehr zum Integritätsnachweis, der in der Configuration Manager-Konsole angezeigt werden kann."
ms.custom: na
ms.date: 03/27/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 91f9de33-b277-4500-acd6-e7d90a2947c9
caps.latest.revision: "17"
author: NathBarn
ms.author: nathbarn
manager: angrobe
ms.openlocfilehash: 54b3433a002b8ef29059bab04458138348f95d66
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="health-attestation-for-system-center-configuration-manager"></a>Integritätsnachweis für System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Administratoren können den Status des [Windows 10-Nachweises zur Geräteintegrität](https://technet.microsoft.com/library/mt592023.aspx) in der Configuration Manager-Konsole anzeigen.  Mit dem Nachweis der Geräteintegrität kann der Administrator sicherstellen, dass Clientcomputer über die folgenden aktivierten vertrauenswürdigen BIOS-, TPM- und Startsoftwarekonfigurationen verfügen:  

-   Antischadsoftware-Frühstart – Antischadsoftware-Frühstart (Early Launch Anti-Malware, ELAM) schützt Ihren Computer beim Starten und bevor Drittanbietertreiber initialisiert werden. [Informationen zum Aktivieren von ELAM](https://gallery.technet.microsoft.com/How-to-turn-on-Early-84552ec5)  
-   BitLocker – Mit der Windows-BitLocker-Laufwerkverschlüsselungs-Software können Sie alle Daten verschlüsseln, die auf dem Windows-Betriebssystemvolume gespeichert sind.  [How to turn on BitLocker (Informationen zum Aktivieren von BitLocker)](https://gallery.technet.microsoft.com/How-to-turn-on-BitLocker-34294d3d)  
-   Sicherer Start – Sicherer Start ist ein Sicherheitsstandard, der von Mitgliedern der PC-Industrie entwickelt wurde, um sicherzustellen, dass Ihr PC nur mit Software startet, die der PC-Hersteller als vertrauenswürdig eingestuft hat. [Weitere Informationen zu Sicherer Start](https://technet.microsoft.com/library/hh824987.aspx)  
-   Codeintegrität – Codeintegrität ist ein Feature, das die Sicherheit des Betriebssystems verbessert, indem es die Integrität einer Treiber- oder Systemdatei jedes Mal überprüft, wenn sie in den Arbeitsspeicher geladen wird. [Erfahren Sie mehr über Codeintegrität](https://technet.microsoft.com/library/dd348642.aspx)  

Diese Funktion ist für PCs und lokale Ressourcen verfügbar, die von Configuration Manager verwaltet werden sowie für mobile Geräte, die von Microsoft Intune verwaltet werden. Administratoren können angeben, ob die Berichterstellung über die Cloud oder über die lokale Infrastruktur durchgeführt wird. Die lokale Überwachung des Nachweises der Geräteintegrität ermöglicht dem Administrator die Überwachung des Client-PCs ohne Internetzugriff.

## <a name="enable-health-attestation"></a>Aktivieren des Integritätsnachweises

 **Anforderungen:**  

-   Clientgeräte unter Windows 10 Version 1607 oder Windows Server 2016 Version 1607 mit [Nachweis der Geräteintegrität aktiviert](https://technet.microsoft.com/windows-server-docs/security/device-health-attestation)
-    TPM 1.2 oder TPM 2-fähige Geräte
-   Kommunikation zwischen dem Configuration Manager-Client-Agent und dem „has.spserv.microsoft.com“ (Port 443) Integritätsnachweisdienst (Cloud-Verwaltung) oder mit dem aktivierten Verwaltungspunkt des Nachweises der Geräteintegrität (lokal)

### <a name="how-to-enable-health-attestation-service-communication-on-configuration-manager-client-computers"></a>Aktivieren der Kommunikation mit dem Integritätsnachweisdienst auf Configuration Manager-Clientcomputern

Verwenden Sie dieses Verfahren, um die Überwachung des Nachweises der Geräteintegrität für Geräte zu aktivieren, die mit dem Internet verbunden sind.

1.  Wählen Sie in der Configuration Manager-Konsole **Verwaltung** > **Übersicht** > **Clienteinstellungen**aus.  Wählen Sie die Registerkarte für **Computer-Agent** -Einstellungen aus.  
2.  Wählen Sie im Dialogfeld **Standardeinstellungen**  **Computer-Agent** aus, und scrollen Sie nach unten zu **Kommunikation mit Integritätsnachweisdienst aktivieren**.  
3.  Legen Sie **Kommunikation mit Integritätsnachweisdienst aktivieren** auf **Ja**fest, und klicken Sie anschließend auf **OK**.  
4. Zielsammlungen von Geräten, die die Geräteintegrität melden sollen.

### <a name="how-to-enable-on-premises-health-attestation-service-communication-on-configuration-manager-client-computers"></a>Aktivieren der lokalen Kommunikation mit dem Integritätsnachweisdienst auf Configuration Manager-Clientcomputern
Verwenden Sie dieses Verfahren, um die Überwachung des Nachweises der Geräteintegrität für lokale Geräte zu aktivieren, die nicht mit dem Internet verbunden sind.

Ab Configuration Manager 1702 kann die lokale Dienst-URL des Nachweises der Geräteintegrität auf dem Verwaltungspunkt zur Unterstützung von Client-Geräten ohne Zugriff auf das Internet konfiguriert werden.

1. Navigieren Sie in der Configuration Manager-Konsole zu **Verwaltung** > **Übersicht** > **Standortkonfiguration** > **Standorte**.
2. Klicken Sie mit der rechten Maustaste auf den primären oder sekundären Standort mit dem Verwaltungspunkt, der lokale Clients für den Nachweis der Geräteintegrität unterstützt, und wählen Sie **Standortkomponenten konfigurieren** > **Verwaltungspunkt** aus. Die Seite **Eigenschaften der Verwaltungspunktkomponente** öffnet sich.
3. Wählen Sie auf der Registerkarte **Erweiterte Optionen** **Hinzufügen** aus, und geben Sie eine gültige lokale Dienst-URL für den Nachweis der Geräteintegrität an. Sie können mehrere URLs hinzufügen. Wenn mehrere lokale URLs angegeben sind, erhalten Clients den vollständigen Satz und wählen nach dem Zufallsprinzip aus, welche sie verwenden.
4.  Wählen Sie in der Configuration Manager-Konsole **Verwaltung** > **Übersicht** > **Clienteinstellungen**aus.  Wählen Sie die Registerkarte für **Computer-Agent** -Einstellungen aus.  
5.  Wählen Sie im Dialogfeld **Standardeinstellungen** **Computer-Agent** aus, scrollen Sie anschließend nach unten zu **Use on-premises Health Attestation Service** (Verwenden des lokalen Integritätsnachweisdiensts), und legen Sie dies auf **Ja** fest.
6. Setzen Sie die Sammlung von Geräten als Ziel, die die Geräteintegrität mit den Client-Agent-Einstellungen melden sollen, um die Berichterstattung für den Nachweis der Geräteintegrität zu aktivieren.

Sie können die Dienst-URLs für den Nachweis der Geräteintegrität auch **bearbeiten** oder **entfernen**.

> [!NOTE]
> Wenn Sie den Nachweis der Geräteintegrität vor dem Upgrade auf Configuration Manager 1702 verwendet haben, werden die in den Einstellungen des Client-Agent angegebenen lokalen URLs vorab während des Upgrades in den Eigenschaften des Verwaltungspunkts eingefügt. Lokale Clients werden weiterhin die URL verwenden, die in den Einstellungen des Client-Agents angegeben werden, bis sie aktualisiert werden. Sie werden dann auf eine der im Verwaltungspunkt angegebenen URLs umschalten.

## <a name="monitor-device-health-attestation"></a>Überwachung des Nachweises der Geräteintegrität

1.  Wechseln Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Überwachung** , klicken Sie auf den Knoten **Sicherheit** und anschließend auf **Integritätsnachweis**, um den Nachweis der Geräteintegrität anzuzeigen.  
2.  Der Nachweis der Geräteintegrität wird angezeigt.  

Der Configuration Manager-Geräteintegritätsnachweis zeigt Folgendes an:  

-   **Integritätsnachweisstatus** – Zeigt die Anteile der Geräte in kompatiblem, nicht kompatiblem, Fehler- und unbekanntem Status an  
-   **Geräte mit Health Attestation-Unterstützung** – Zeigt den Prozentsatz der Geräte an, die den Integritätsnachweisstatus berichten  
-   **Nicht kompatible Geräte nach Clienttyp** – Zeigt den Anteil an mobilen Geräten und Computern an, die nicht kompatibel sind  
-   **Wichtigste fehlende Integritätsnachweiseinstellungen** – Zeigt nach Einstellungen gelistet die Anzahl von Geräte an, für die die Health Attestation-Einstellung fehlt

Der Status des Nachweises der Clientgeräteintegrität kann verwendet werden, um in den Konformitätsrichtlinien für Geräte, die von Configuration Manager mit Microsoft Intune verwaltet werden, Regeln für den bedingten Zugriff zu definieren. Weitere Informationen finden Sie unter [Verwalten von Kompatibilitätsrichtlinien für Geräte in System Center Configuration Manager](/sccm/protect/deploy-use/device-compliance-policies).  
