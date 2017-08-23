---
title: Konfigurieren des Clientstatus | Microsoft-Dokumentation
description: "Wählen Sie die Clientstatuseinstellungen in System Center Configuration Manager aus."
ms.custom: na
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-client
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: a2275ba2-c83d-43e7-90ed-418963a707fe
caps.latest.revision: "6"
caps.handback.revision: "0"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 060d63ab8bce9c3bb39d2db404580b9f59416d33
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="how-to-configure-client-status-in-system-center-configuration-manager"></a>Konfigurieren des Clientstatus in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Sie müssen zunächst für Ihren Standort die Parameter einrichten, anhand derer Clients als inaktiv gekennzeichnet werden, und Benachrichtigungsoptionen für den Fall konfigurieren, dass ein angegebener Schwellenwert von einer Clientaktivität unterschritten wird, damit Sie den System Center Configuration Manager-Clientstatus überwachen und aufgetretene Probleme beheben können. Sie können außerdem Computer daran hindern, Clientstatusprobleme automatisch zu beheben.  

##  <a name="BKMK_1"></a> So konfigurieren Sie den Clientstatus  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Überwachung**.  

2.  Klicken Sie im Arbeitsbereich **Überwachung** auf **Clientstatus**und dann auf der Registerkarte **Startseite** in der Gruppe **Clientstatus** auf **Client-Statuseinstellungen**.  

3.  Geben Sie im Dialogfeld **Eigenschaften der Clientstatuseinstellungen** die folgenden Werte zum Bestimmen der Clientaktivität an:  

    > [!NOTE]  
    >  Wenn keine dieser Einstellungen zutrifft, wird der Client als inaktiv gekennzeichnet.  

    -   **Clientrichtlinienanforderungen innerhalb der folgenden Tage:** Geben Sie die Anzahl von Tagen seit der letzten Richtlinienanforderung durch einen Client an. Der Standardwert ist **7** Tage.  

    -   **Taktermittlung innerhalb der folgenden Tage:** Geben Sie die Anzahl von Tagen seit der letzten Übermittlung eines Frequenzermittlungsdatensatzes an die Standortdatenbank durch den Clientcomputer an. Der Standardwert ist **7** Tage.  

    -   **Hardwareinventur innerhalb der folgenden Tage:** Geben Sie die Anzahl von Tagen seit der letzten Übermittlung eines Hardwareinventurdatensatzes an die Standortdatenbank durch den Clientcomputer an. Der Standardwert ist **7** Tage.  

    -   **Softwareinventur innerhalb der folgenden Tage:** Geben Sie die Anzahl von Tagen seit der letzten Übermittlung eines Softwareinventurdatensatzes an die Standortdatenbank durch den Clientcomputer an. Der Standardwert ist **7** Tage.  

    -   **Statusmeldungen innerhalb der folgenden Tage:** Geben Sie die Anzahl von Tagen seit der letzten Übermittlung von Statusmeldungen an die Standortdatenbank durch den Clientcomputer an. Der Standardwert ist **7** Tage.  

4.  Geben Sie im Dialogfeld **Eigenschaften der Clientstatuseinstellungen** die folgenden Werte an, um festzulegen, wie lange Verlaufsdaten für den Clientstatus beibehalten werden:  

    -   **Clientstatusverlauf für die folgende Anzahl von Tagen beibehalten:** Geben Sie an, wie lange der Clientstatusverlauf in der Standortdatenbank gespeichert werden soll. Der Standardwert ist **31** Tage.  

5.  Klicken Sie auf **OK** , um die Eigenschaften zu speichern und das Dialogfeld **Eigenschaften der Clientstatuseinstellungen** zu schließen.  

##  <a name="BKMK_Schedule"></a> So konfigurieren Sie den Zeitplan für den Clientstatus  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Überwachung**.  

2.  Klicken Sie im Arbeitsbereich **Überwachung** auf **Clientstatus**und dann auf der Registerkarte **Startseite** in der Gruppe **Clientstatus** auf **Aktualisierung des Clientstatus planen**.  

3.  Konfigurieren Sie im Dialogfeld **Aktualisierung des Clientstatus planen** das Intervall für die Aktualisierung des Clientstatus, und klicken Sie dann auf "OK".  

    > [!NOTE]  
    >  Wenn Sie den Zeitplan für Clientstatusaktualisierungen ändern, treten die Änderungen erst mit der nächsten geplanten Clientstatusaktualisierung (nach dem zuvor konfigurierten Zeitplan) in Kraft.  

##  <a name="BKMK_2"></a> So konfigurieren Sie Warnungen für den Clientstatus  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Bestand und Kompatibilität**.  

2.  Klicken Sie im Arbeitsbereich **Bestand und Kompatibilität** auf **Gerätesammlungen**.  

3.  Wählen Sie in der Liste **Gerätesammlungen** die Sammlung aus, für die Sie Warnungen konfigurieren möchten, und klicken Sie dann auf der Registerkarte **Startseite** in der Gruppe **Eigenschaften** auf **Eigenschaften**.  

    > [!NOTE]  
    >  Es können keine Benachrichtigungen für Benutzersammlungen konfiguriert werden.  

4.  Klicken Sie auf der Registerkarte **Warnungen** des Dialogfelds **Eigenschaften** von *&lt;Sammlungsname\>* auf **Hinzufügen**.  

    > [!NOTE]  
    >  Die Registerkarte **Warnungen** wird nur angezeigt, wenn die Ihnen zugewiesene Sicherheitsrolle über Berechtigungen für Warnungen verfügt.  

5.  Wählen Sie im Dialogfeld **Neue Sammlungswarnungen hinzufügen** die Warnungen aus, die beim Unterschreiten bestimmter Clientstatuswerte generiert werden sollen, und klicken Sie dann auf **OK**.  

6.  Wählen Sie auf der Registerkarte **Warnungen** in der Liste **Bedingungen** die einzelnen Clientstatuswarnungen aus, und geben Sie für jede Warnung die folgenden Informationen an:  

    -   **Warnungsname** – Übernehmen Sie den Standardnamen, oder geben Sie einen neuen Namen für die Warnung ein.  

    -   **Warnungsschweregrad** – Wählen Sie in der Dropdownliste den Schweregrad aus, der in der Configuration Manager-Konsole angezeigt werden soll.  

    -   **Warnung auslösen** – Geben Sie den Schwellenwert für die Warnung in Prozent an.  

7.  Klicken Sie auf **OK**, um das Dialogfeld **Eigenschaften** von *&lt;Sammlungsname\>* zu schließen.  

##  <a name="BKMK_3"></a> So schließen Sie Computer von der automatischen Wiederherstellung aus  

1.  Öffnen Sie auf dem Clientcomputer, für den die automatische Wiederherstellung deaktiviert werden soll, den Registrierungs-Editor.  

    > [!WARNING]  
    >  Durch eine unsachgemäße Verwendung des Registrierungs-Editors können schwerwiegende Fehler auftreten, die möglicherweise eine Neuinstallation des Betriebssystems erforderlich machen. Microsoft kann nicht garantieren, dass Probleme, die aufgrund einer unsachgemäßen Verwendung des Registrierungs-Editors entstehen, behoben werden können. Die Verwendung des Registrierungs-Editors erfolgt auf eigene Gefahr.  

2.  Wechseln Sie zu **HKEY_LOCAL_MACHINE\Software\Microsoft\CCM\CcmEval\NotifyOnly**.  

3.  Geben Sie einen der folgenden Werte für diesen Registrierungsschlüssel an:  

    -   **True** – Auf dem Clientcomputer aufgetretene Probleme werden nicht automatisch behoben. Sie werden aber auch weiterhin im Arbeitsbereich **Überwachung** über Probleme bei diesem Client informiert.  

    -   **False** – Auf dem Clientcomputer aufgetretene Probleme werden automatisch behoben, und Sie werden im Arbeitsbereich **Überwachung** darüber informiert. Dies ist die Standardeinstellung.  

4.  Schließen Sie den Registrierungs-Editor.  

 Sie können Clients auch mithilfe der CCMSetup-Installationseigenschaft **NotifyOnly** installieren, um sie von der automatischen Wiederherstellung auszuschließen. Weitere Informationen zu den Clientinstallationseigenschaften finden Sie unter [Informationen zu Clientinstallationseigenschaften in System Center Configuration Manager](../../../core/clients/deploy/about-client-installation-properties.md).  
