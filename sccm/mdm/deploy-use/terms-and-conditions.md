---
title: "Geschäftsbedingungen von System Center Configuration Manager | Microsoft-Dokumentation"
description: "Stellen Sie Geschäftsbedingungen für Benutzergruppen in System Center Configuration Manager bereit."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4d3f9e6b-4d71-4fc4-9b91-47f1bfbd8c70
caps.latest.revision: "9"
author: nathbarn
ms.author: nathbarn
manager: angrobe
ms.openlocfilehash: 20be68496099a67ad2d475067f073da2cef16c86
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="add-terms-and-conditions-with-system-center-configuration-manager"></a>Hinzufügen von Geschäftsbedingungen mit System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Sie können die Geschäftsbedingungen von System Center Configuration Manager für Benutzergruppen zur Erläuterung bereitstellen, wie sich die Geräteregistrierung, der Zugriff auf Arbeitsressourcen und die Verwendung des Unternehmensportals auf Geräte und Benutzer auswirken. Benutzer müssen die Geschäftsbedingungen akzeptieren, bevor sie sich über das Unternehmensportal registrieren und auf ihre Arbeit zugreifen können.  

 ## <a name="working-with-terms-and-conditions-policies-in-system-center-configuration-manager"></a>Arbeiten mit Geschäftsbedingungsrichtlinien in System Center Configuration Manager  
 Sie können mehrere Sätze von Geschäftsbedingungen erstellen und bereitstellen. Sie können auch Versionen derselben Nutzungsbedingungen in verschiedenen Sprachen erstellen und diese dann für die entsprechenden Gruppen bereitstellen.  

## <a name="to-create-a-terms-and-conditions"></a>So erstellen Sie Geschäftsbedingungen  

1.  Wechseln Sie in der Configuration Manager-Konsole zu **Bestand und Kompatibilität** > **Übersicht** > **Kompatibilitätseinstellungen** > **Geschäftsbedingungen**.  

2.  Klicken Sie auf **Geschäftsbedingungen erstellen** , um neue Geschäftsbedingungen zu erstellen.  

3.  Geben Sie auf der Seite **Allgemein** die folgenden Informationen an:  

    -   **Name**: Ein eindeutiger Name, der in der Configuration Manager-Konsole angezeigt wird  

    -   **Beschreibung**: Details, die Ihnen dabei helfen, die Geschäftsrichtlinien in der Configuration Manager-Konsole zu identifizieren  

     Klicken Sie dann auf **Weiter**.  

4.  Geben Sie auf der Seite für die **Bestimmungen** die folgenden Informationen an:  

    -   **Titel** : Der für Benutzer im Unternehmensportal angezeigte Titel.  

    -   **Text der Nutzungsbedingungen** : Die für Benutzer im Unternehmensportal angezeigten Geschäftsbedingungen.  

    -   **Text zur Erläuterung der Bedeutung, wenn der Benutzer zustimmt** : Die für Benutzer angezeigte Bezeichnung hinsichtlich der Zustimmung. **Beispiel:** „Ich stimme den Nutzungsbedingungen zu.“  

     Klicken Sie dann auf **Weiter**.  

5.  Schließen Sie den Assistenten ab, um die neuen Geschäftsbedingungen zu erstellen. Die neuen Geschäftsbedingungen werden im Knoten für die Geschäftsbedingungen im Arbeitsbereich „Bestand und Kompatibilität“ angezeigt.  

## <a name="to-deploy-a-terms-and-conditions"></a>So stellen Sie Geschäftsbedingungen bereit  

1.  Wechseln Sie in der Configuration Manager-Konsole zu **Bestand und Kompatibilität** > **Übersicht** > **Kompatibilitätseinstellungen** > **Geschäftsbedingungen**.  

2.  Wählen Sie in der Liste der **Geschäftsbedingungen** das bereitzustellende Element aus, und klicken Sie dann auf **Bereitstellen**.  

3.  **Navigieren** Sie zur **Sammlung** , für die Sie die Geschäftsbedingungen bereitstellen möchten, und klicken Sie dann auf **OK**.  

     Wenn die vorgesehenen Geräte auf die Unternehmensportal-App zugreifen, werden die bereitgestellten Geschäftsbedingungen angezeigt. Benutzer müssen diese Nutzungsbedingungen akzeptieren, bevor sie Zugriff auf Unternehmensressourcen erhalten.  

    > [!NOTE]  
    >  Wenn Sie eine Reihe von Geschäftsbedingungen für mehrere Benutzersammlungen bereitstellen, denen ein Benutzer angehört, werden diesem Benutzer beim Öffnen des Unternehmensportals mehrere Kopien identischer Geschäftsbedingungen angezeigt. Da Benutzer jeweils nur alle Geschäftsbedingungen annehmen oder ablehnen können, besteht keine Gefahr, dass sich ein mehrdeutiger Zustand ergibt, in dem der Benutzer Geschäftsbedingungen sowohl angenommen als auch abgelehnt hat. Der Akzeptanzbericht für die Geschäftsbedingungen umfasst nur eine Zeile für jeden Satz von Geschäftsbedingungen für den jeweiligen Benutzer, damit in dem Bericht kein Fehler auftritt.  

## <a name="to-monitor-terms-and-conditions"></a>So überwachen Sie die Geschäftsbedingungen  

1.  Sie können Bereitstellungen von Geschäftsbedingungen in der Configuration Manager-Konsole überwachen. Wechseln Sie in der Configuration Manager-Konsole zu **Überwachung** > **Übersicht** > **Bereitstellungen**.  

2.  Wählen Sie die Bereitstellung der Geschäftsbedingungen in der Liste der Bereitstellungen aus.  

     Der Zusammenfassungsbereich enthält die folgenden Statistiken:  

    -   **Kompatibel** : Benutzer haben die neueste Version der Geschäftsbedingungen akzeptiert.  

    -   **Fehler**  

    -   **Nicht Kompatibel** : Benutzer haben eine Version der Geschäftsbedingungen, aber nicht die neueste akzeptiert.  

    -   **Unbekannt** : Benutzer haben die Geschäftsbedingungen nie akzeptiert, einschließlich derjenigen ohne registriertes Gerät.  

3.  Wählen Sie eine Bereitstellung von Geschäftsbedingungen und dann **Zusammenfassung ausführen** aus, um den Bereitstellungsstatus einzelner Benutzer anzuzeigen.  

     Auf dem Bildschirm „Bereitstellungsstatus“ können Sie die Statusregisterkarten auswählen, um Benutzer mit dem jeweiligen Status anzuzeigen. Klicken Sie zum Aktualisieren der Daten in der gesamten Hierarchie auf **Zusammenfassung ausführen** . Klicken Sie zum Aktualisieren von Daten in der Konsole auf **Aktualisieren** .  

## <a name="to-view--a-terms-and-conditions-report"></a>So zeigen Sie einen Bericht zu den Geschäftsbedingungen an  

1.  Wechseln Sie in der Configuration Manager-Konsole zu **Überwachung** > **Übersicht** > **Berichterstellung** > **Bericht**.  

2.  Wählen Sie **Bestimmungen akzeptieren** aus, und klicken Sie anschließend auf **Ausführen**. Der Bericht für die Akzeptanz von Geschäftsbedingungen wird geöffnet. Der Bericht zeigt alle Benutzer, denen die Geschäftsbedingungen bereitgestellt wurden. Es gibt u. a. die folgenden Felder:  

    -   Name der Geschäftsbedingungen  

    -   Benutzername  

    -   Akzeptierte Version  

    -   Datum der Annahme  

    -   Neueste akzeptiert  

## <a name="updates-and-version-control-for-terms-and-conditions"></a>Updates und Versionskontrolle für Geschäftsbedingungen  
 Beim Bearbeiten vorhandener Geschäftsbedingungen können Sie das Verhalten für die Bereitstellung der Geschäftsbedingungen auswählen. Verwenden Sie das folgende Verfahren, das Sie beim Aktualisieren vorhandener Geschäftsbedingungen unterstützt.  

### <a name="how-to-work-with-multiple-versions-of-terms-and-conditions"></a>Arbeiten mit mehreren Versionen der Nutzungsbedingungen  

1.  Wechseln Sie in der Configuration Manager-Konsole zu **Bestand und Kompatibilität** > **Übersicht** > **Kompatibilitätseinstellungen** > **Geschäftsbedingungen**.  

2.  Wählen Sie die Instanz der zu bearbeitenden Geschäftsbedingungen aus, und doppelklicken Sie dann darauf, um sie zu öffnen.  

3.  Sie können den Inhalt auf der Seite **Allgemeine** oder **Bestimmungen** ändern, sofern eine Bearbeitung erforderlich ist.  

4.  Auf der Seite für die **Bestimmungen** können Sie dann angeben, ob diese neue Version erfordert, dass die Geschäftsbedingungen von allen Benutzern angenommen werden, oder es ausreicht, wenn die neue Version nur neuen Benutzern angezeigt wird.  

     Es wird empfohlen, dass Sie die Versionsnummer erhöhen und jedes Mal die Zustimmung zu den Geschäftsbedingungen anfordern, wenn Sie wichtige Änderungen an den Geschäftsbedingungen vornehmen. Behalten Sie die aktuelle Versionsnummer bei, wenn Sie z. B. Tippfehler korrigieren oder die Formatierung ändern.

> [!div class="button"]
[< Vorheriger Schritt](configure-intune-subscription.md) [Nächster Schritt >](create-service-connection-point.md)
