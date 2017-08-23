---
title: Erstellen von Remoteverbindungsprofilen | Microsoft-Dokumentation
description: "Verwenden Sie Remoteverbindungsprofile für System Center Configuration Manager, um Ihren Benutzern das Herstellen einer Remoteverbindung zu Ihren Arbeitscomputern zu ermöglichen."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8c6eabc4-5dda-4682-b03e-3a450e6ef65a
caps.latest.revision: "8"
caps.handback.revision: "0"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 72fc94c6449649656a7e8b81659c2b5cc2551107
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="remote-connection-profiles-in-system-center-configuration-manager"></a>Remoteverbindungsprofile in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Verwenden Sie Remoteverbindungsprofile für System Center Configuration Manager, um Benutzern das Herstellen von Remoteverbindungen mit Arbeitscomputern zu ermöglichen, wenn keine Verbindung mit der Domäne besteht oder ihre PCs mit dem Internet verbunden sind.  

 Benutzer können über die folgenden Gerätetypen eine Verbindung mit ihrem Arbeits-PC herstellen:  

-   Computer, auf denen Microsoft Windows ausgeführt wird  

-   Geräte, auf denen iOS ausgeführt wird  

-   Geräte, auf denen Android ausgeführt wird  

Mit Remoteverbindungsprofilen können Sie Benutzern die Einstellungen für die Remotedesktopverbindung in Ihrer Configuration Manager-Hierarchie bereitstellen. Benutzer können dann mithilfe des Unternehmensportals über Remotedesktop unter Verwendung der vom Unternehmensportal bereitgestellten Einstellungen der Remotedesktopverbindung auf ihre primären Arbeitscomputer zugreifen.  

Wenn Sie möchten, dass Benutzer mithilfe des Unternehmensportals eine Verbindung mit ihrem Arbeits-PC herstellen können, ist Microsoft Intune erforderlich. Wenn Sie Intune nicht verwenden, können Benutzer die Informationen aus dem Remoteverbindungsprofil dennoch zum Herstellen einer Verbindung mit ihrem Arbeits-PC verwenden, indem sie Remotedesktop über eine VPN-Verbindung nutzen.  

> [!IMPORTANT]  
>  Beim Angeben von Einstellungen für Remoteverbindungsprofile über die Configuration Manager-Konsole werden diese in der lokalen Richtlinie des Clientcomputers gespeichert. Durch diese Einstellungen können die von einer anderen Anwendung konfigurierten Remotedesktop-Einstellungen außer Kraft gesetzt werden. Wenn Sie die Remotedesktopeinstellungen mit der Windows-Gruppenrichtlinie konfigurieren, setzen die in der Gruppenrichtlinie angegebenen Einstellungen zudem die mithilfe von Configuration Manager konfigurierten Einstellungen außer Kraft.  

 Beim Installieren von Configuration Manager wird die neue Sicherheitsgruppe **Remotecomputerverbindung** erstellt. Diese Gruppe wird aufgefüllt, wenn Sie ein Remoteverbindungsprofil mit den primären Benutzern des Computers bereitstellen, auf dem Sie das Profil bereitstellen. Der lokale Administrator kann dieser Gruppe zwar Benutzernamen hinzufügen, aber diese Benutzer werden bei der nächsten Kompatibilitätsauswertung der bereitgestellten Remoteverbindungsprofile aus der Gruppe entfernt.  

 Wenn Sie dieser Gruppe einen Benutzer manuell hinzufügen, kann der Benutzer Remoteverbindungen initiieren, aber die Verbindungsinformationen werden nicht im Unternehmensprotal veröffentlicht.  

 Wenn Sie einen Benutzer manuell aus der Gruppe entfernen, der von Configuration Manager hinzugefügt wurde, wird diese Änderung von Configuration Manager automatisch rückgängig gemacht, indem der Benutzer bei der nächsten Kompatibilitätsauswertung des Remoteverbindungsprofils wieder hinzugefügt wird.  

> [!IMPORTANT]  
>  Wenn sich die Affinität zwischen Benutzer und Gerät ändert (wenn beispielsweise der Computer, mit dem ein Benutzer eine Verbindung herstellt, nicht mehr das primäre Gerät des Benutzers ist), werden das Remoteverbindungsprofil und die Windows-Firewall-Einstellungen von Configuration Manager deaktiviert, um zu verhindern, dass Verbindungen mit dem Computer hergestellt werden.  

## <a name="prerequisites"></a>Voraussetzungen  

### <a name="external-dependencies"></a>Externe Abhängigkeiten  

|Abhängigkeit|Weitere Informationen|  
|----------------|----------------------|  
|Remotedesktop-Gatewayserver.|Falls Sie Benutzern die Möglichkeit einräumen möchten, von außerhalb der Unternehmensdomäne über das Internet eine Verbindung herzustellen, müssen Sie einen Remotedesktop-Gatewayserver installieren und konfigurieren.<br /><br /> Werden die Einstellungen für Remotedesktop oder Terminaldienste über eine andere Anwendung oder Gruppenrichtlinieneinstellungen verwaltet, funktionieren Remoteverbindungsprofile eventuell nicht ordnungsgemäß. Beim Bereitstellen von Remoteverbindungsprofilen über die Configuration Manager-Konsole werden die Einstellungen in der lokalen Richtlinie des Clientcomputers gespeichert. Durch diese Einstellungen können die von einer anderen Anwendung konfigurierten Remotedesktop-Einstellungen außer Kraft gesetzt werden. Wenn Sie die Remotedesktopeinstellungen mit Gruppenrichtlinieneinstellungen konfigurieren, werden mit den in den Gruppenrichtlinieneinstellungen angegebenen Einstellungen zudem die von Configuration Manager konfigurierten Einstellungen außer Kraft gesetzt.<br /><br /> Weitere Informationen zum Installieren und Konfigurieren des Remotedesktop-Gatewayservers finden Sie in der Dokumentation zu Windows Server.|  
|Wenn auf Clientcomputern eine hostbasierte Firewall ausgeführt wird, muss die Ausführung von „mstsc.exe“ zugelassen sein.|Beim Konfigurieren eines Remoteverbindungsprofils müssen Sie die Einstellung **Windows-Firewall-Ausnahme für Windows-Domänen und in privaten Netzwerken Verbindungen zulassen** aktivieren. Ist diese Einstellung aktiviert, wird die Windows-Firewall von Configuration Manager automatisch so konfiguriert, dass die Ausführung von „mstsc.exe“ zugelassen wird. Wird auf den Clientcomputern allerdings eine andere hostbasierte Firewall ausgeführt, müssen Sie die betreffende Firewallabhängigkeit manuell konfigurieren.<br /><br /> Durch die Gruppenrichtlinieneinstellungen für die Konfiguration der Windows-Firewall kann die in Configuration Manager eingerichtete Konfiguration außer Kraft gesetzt werden. Wenn Sie zum Konfigurieren der Windows-Firewall eine Gruppenrichtlinie verwenden, sollten Sie sicherstellen, dass die entsprechenden Einstellungen die Ausführung von „mstsc.exe“ nicht blockieren.|  

### <a name="configuration-manager-dependencies"></a>Abhängigkeiten in Configuration Manager  

|Abhängigkeit|Weitere Informationen|  
|----------------|----------------------|  
|Configuration Manager muss mit Microsoft Intune verbunden sein (eine sogenannte Hybridkonfiguration).|Weitere Informationen zum Herstellen einer Verbindung zwischen Configuration Manager und Microsoft Intune finden Sie unter „Verwalten von mobilen Geräten mit Configuration Manager und Microsoft Intune“.|  
|Benutzer können nur dann eine Verbindung mit einem Arbeitscomputer im Unternehmensnetzwerk aufbauen, wenn es sich bei dem betreffenden Rechner um das primäre Gerät des Benutzers handelt.|Weitere Informationen zur Affinität zwischen Benutzer und Gerät finden Sie unter [Verknüpfen von Benutzern und Geräten mit Affinität zwischen Benutzer und Gerät](/sccm/apps/deploy-use/link-users-and-devices-with-user-device-affinity).|  
|Für die Verwaltung von Remoteverbindungsprofilen sind spezielle Sicherheitsberechtigungen erforderlich.|In der Sicherheitsrolle **Kompatibilitätseinstellungs-Manager** sind die erforderlichen Berechtigungen zum Verwalten von Remoteverbindungsprofilen enthalten. Weitere Informationen finden Sie unter <br />[Konfigurieren der rollenbasierten Verwaltung](/sccm/core/servers/deploy/configure/configure-role-based-administration).|  

## <a name="security-and-privacy-considerations-for-remote-connection-profiles"></a>Überlegungen zu Sicherheit und Datenschutz für Remoteverbindungsprofile  

### <a name="security-considerations"></a>Sicherheitsüberlegungen  

|Bewährte Sicherheitsmethode|Weitere Informationen|  
|----------------------------|----------------------|  
|Geben Sie manuell die Affinität zwischen Benutzer und Gerät an, statt zuzulassen, dass die Benutzer das primäre Gerät selbst bestimmen. Aktivieren Sie darüber hinaus die verwendungsbasierte Konfiguration nicht.|Da Sie die Option **Allen primären Benutzern des Arbeitscomputers Remoteverbindungen gestatten** aktivieren müssen, bevor Sie ein Remoteverbindungsprofil bereitstellen können, geben Sie die Affinität zwischen Benutzer und Gerät immer manuell an. Betrachten Sie die Informationen, die von Benutzern oder Geräten gesammelt werden, nicht als autorisierend. Wenn Sie Remoteverbindungsprofile bereitstellen und die Affinität zwischen Benutzer und Gerät nicht von einem vertrauenswürdigen Administrator angegeben wurde, kann dies zu Rechteerweiterungen führen, und nicht autorisierte Benutzer können nachfolgend möglicherweise Remoteverbindungen mit Computern herstellen.<br /><br /> Wenn Sie eine nutzungsbasierte Konfiguration aktivieren, werden diese Informationen über Statusmeldungen erfasst, für die von Configuration Manager keine Sicherheit geboten wird. Sie können diese Bedrohung durch SMB-Signaturen (Server Message Block) oder IPsec (Internet Protocol Security) zwischen Clientcomputern und dem Verwaltungspunkt verringern.|  
|Schränken Sie lokale Administratorrechte auf dem Standortservercomputer ein.|Ein Benutzer mit lokalen Administratorrechten für den Standortserver kann der Sicherheitsgruppe „Remotecomputerverbindung“, die von Configuration Manager automatisch erstellt und verwaltet wird, manuell Mitglieder hinzufügen. Dies kann zu einer Rechteerweiterung führen, da Mitgliedern, die dieser Gruppe hinzugefügt wurden, in der Folge Remotedesktopberechtigungen erteilt werden.|  

### <a name="privacy-considerations"></a>Überlegungen zum Datenschutz  

-   Wenn ein Benutzer über das Unternehmensportal eine Verbindung mit einem Arbeitscomputer initiiert, wird eine Datei mit der Erweiterung RDP oder WSRDP heruntergeladen, die den Gerätenamen und den Namen des Remotedesktop-Gatewayservers enthält, der für den Aufbau der Remotedesktopverbindung erforderlich ist. Die Dateierweiterung hängt vom Betriebssystem des Geräts ab. Beispielsweise wird von den Betriebssystemen Windows 7 und Windows 8 eine RDP-Datei verwendet, während bei Windows 8.1 eine WSRDP-Datei verwendet wird.  

-   Der Benutzer kann die RDP-Datei wahlweise öffnen oder speichern. Falls er die RDP-Datei öffnet, wird sie je nach Beibehaltungseinstellungen des Browsers möglicherweise im Cache des Webbrowsers gespeichert. Wenn der Benutzer entscheidet, die Datei zu speichern, wird die Datei nicht im Browsercache gespeichert. Die Datei wird gespeichert, bis der Benutzer sie manuell löscht.  

-   Die WSRDP-Datei wird heruntergeladen und automatisch lokal gespeichert. Bei der nächsten Ausführung einer Remotedesktopverbindung wird die Datei überschrieben.  

-   Berücksichtigen Sie beim Konfigurieren von Remoteverbindungsprofilen Ihre Datenschutzanforderungen.  


## <a name="create-a-remote-connection-profile"></a>Erstellen eines Remoteverbindungsprofils

1.  Klicken Sie in der Configuration Manager-Konsole auf **Bestand und Kompatibilität** > **Kompatibilitätseinstellungen** > **Remoteverbindungsprofile**.  

3.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Erstellen** auf **Remoteverbindungsprofil erstellen**.  

4.  Geben Sie auf der Seite **Allgemein** des **Assistenten zum Erstellen von Remoteverbindungsprofilen**einen Namen und optional eine Beschreibung für das Profil ein (jeweils maximal 256 Zeichen).  

5.  Geben Sie auf der Seite mit den **Profileinstellungen** die folgenden Einstellungen für das Remoteverbindungsprofil ein:  

    -   **Vollständiger Name und Port des Remotedesktop-Gatewayservers (optional)** : Geben Sie den Namen des Remotedesktop-Gatewayservers an, der für Verbindungen verwendet wird.  

        > [!NOTE]  
        >  Die Verwendung eines internationalisierten Domänennamens zur Angabe eines Servers in diesem Feld wird in Configuration Manager nicht unterstützt.  
        >   
        >  Der Servername darf nicht länger als 256 Zeichen sein. Er darf Groß- und Kleinbuchstaben, Ziffern und die Zeichen **–** und **_** enthalten, die durch Punkte voneinander getrennt sind.  

    -   **Verbindungen nur von Computern zulassen, auf denen Remotedesktop mit Authentifizierung auf Netzwerkebene ausgeführt wird**  

6.  Wählen Sie für jede der folgenden Verbindungseinstellungen **Aktiviert** oder **Deaktiviert** aus:  

    -   **Remoteverbindungen mit Arbeitscomputern zulassen**  

    -   **Allen primären Benutzern des Arbeitscomputers Remoteverbindungen gestatten**  

    -   **Windows-Firewallausnahme für Verbindungen in Windows-Domänen und privaten Netzwerken zulassen**  

    > [!IMPORTANT]  
    >  Sie können erst mit der nächsten Seite des Assistenten fortfahren, wenn alle drei Einstellungen identisch sind.  

7.  Überprüfen Sie auf der Seite **Zusammenfassung** die durchzuführenden Aktionen, und schließen Sie dann den Assistenten ab.  

 Das neue Remoteverbindungsprofil wird im Arbeitsbereich **Bestand und Kompatibilität** im Knoten **Remoteverbindungsprofile** angezeigt.  

Bereitstellen eines Remoteverbindungsprofils  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Bestand und Kompatibilität** > **Kompatibilitätseinstellungen** > **Remoteverbindungsprofile**.  

3.  Wählen Sie in der Liste **Remoteverbindungsprofile** das Remoteverbindungsprofil aus, das Sie bereitstellen möchten, und klicken Sie dann auf der Registerkarte **Startseite** in der Gruppe **Bereitstellung** auf **Bereitstellen**.  

4.  Geben Sie im Dialogfeld **Remoteverbindungsprofil bereitstellen** die folgenden Informationen an:  

    -   **Sammlung** : Klicken Sie auf **Durchsuchen** , um die Benutzersammlung auszuwählen, in der Sie das Remoteverbindungsprofil bereitstellen möchten.  

    -   **Nicht kompatible Regeln wiederherstellen, falls dies unterstützt wird:** Aktivieren Sie diese Option, damit das Remoteverbindungsprofil automatisch wiederhergestellt wird, wenn auf einem Gerät Inkompatibilitäten erkannt werden, z.B. weil es nicht vorhanden ist.  

    -   **Wiederherstellung außerhalb des Wartungsfensters zulassen:** Wenn ein Wartungsfenster für die Sammlung konfiguriert wurde, für die das Remoteverbindungsprofil bereitgestellt wird, aktivieren Sie diese Option, damit das Profil außerhalb des Wartungsfensters von Configuration Manager wiederhergestellt werden kann. Weitere Informationen zu Wartungsfenstern finden Sie unter [Verwenden von Wartungsfenstern](/sccm/core/clients/manage/collections/use-maintenance-windows).  

    -   **Warnung generieren** : Aktivieren Sie diese Option zum Konfigurieren einer Warnung, die generiert wird, sobald die Kompatibilität eines Remoteverbindungsprofils zu einem bestimmten Datum und einer bestimmten Uhrzeit unterhalb eines angegebenen Prozentsatzes liegt. Sie können außerdem angeben, ob eine Warnung an System Center Operations Manager gesendet werden soll.  

    -   **Geben Sie den Zeitplan für die Kompatibilitätsauswertung dieser Konfigurationsbasislinie an** : Geben Sie den Zeitplan an, nach dem das bereitgestellte Remoteverbindungsprofil auf Geräten ausgewertet wird. Sie können wahlweise einen einfachen oder einen benutzerdefinierten Zeitplan angeben.  

    > [!TIP]  
    >  Wenn ein Gerät aus einer Sammlung ausscheidet, in der ein Remoteverbindungsprofil bereitgestellt wurde, werden die Einstellungen diese Profils auf dem Gerät deaktiviert. Dieser Vorgang kann jedoch nur dann ordnungsgemäß ausgeführt werden, wenn Sie zuvor wenigstens ein Konfigurationselement oder eine Konfigurationsbasislinie bereitgestellt haben, die ein Konfigurationselement von Ihrem Standort enthält.  
    >   
    >  Das Profil wird von Geräten ausgewertet, wenn sich der Benutzer anmeldet.  
    >   
    >  Wenn zwei Remoteverbindungsprofile für die gleiche Gerätesammlung bereitgestellt werden, bei denen in einem Fall die Option **Nicht kompatible Regeln wiederherstellen, falls dies unterstützt wird** aktiviert ist, im anderen Fall jedoch nicht, und beide Remoteverbindungsprofile unterschiedliche Verbindungseinstellungen enthalten, werden die Einstellungen des Profils mit aktivierter Option möglicherweise von dem anderen Profil außer Kraft gesetzt. Diese Art der Remoteverbindungsprofil-Bereitstellung wird von Configuration Manager nicht unterstützt.  

5.  Klicken Sie auf **OK** , um das Dialogfeld **Remoteverbindungsprofile bereitstellen** zu schließen und die Bereitstellung zu erstellen.  

## <a name="monitor-a-remote-connection-profile"></a>Überwachen eines Remoteverbindungsprofils  

### <a name="view-compliance-results-in-the-configuration-manager-console"></a>Anzeigen von Kompatibilitätsergebnissen in der Configuration Manager-Konsole  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Überwachung** > **Bereitstellungen**.  

3.  Wählen Sie in der Liste **Bereitstellungen** die Bereitstellung der Remoteverbindungsprofile aus, für die Sie die Kompatibilitätsinformationen prüfen möchten.  

4.  Zusammenfassende Informationen zur Kompatibilität der Bereitstellung der Remoteverbindungsprofile finden Sie auf der Hauptseite. Wählen Sie zum Anzeigen ausführlicherer Informationen die Bereitstellung der Remoteverbindungsprofile aus, und klicken Sie dann auf der Registerkarte **Startseite** in der Gruppe **Bereitstellung** auf **Status anzeigen** , um die Seite **Bereitstellungsstatus** anzuzeigen.  

     Auf der Seite **Bereitstellungsstatus** sind die folgenden Registerkarten enthalten:  

    -   **Kompatibel:** Hiermit wird die Kompatibilität des Remoteverbindungsprofils basierend auf der Anzahl der betroffenen Bestände angezeigt. Sie können auf eine Regel doppelklicken, um im Arbeitsbereich **Bestand und Kompatibilität** unter dem Knoten **Benutzer** einen temporären Knoten zu erstellen. In diesem Knoten sind alle Geräte enthalten, die mit dem Remoteverbindungsprofil kompatibel sind. Im Bereich **Bestandsdetails** werden zudem die Geräte angezeigt, die mit diesem Profil kompatibel sind. Doppelklicken Sie auf ein Gerät in der Liste, um weitere Informationen anzuzeigen.  

        > [!IMPORTANT]  
        >  Ein Remoteverbindungsprofil wird nicht ausgewertet, wenn es für ein Clientgerät nicht gilt. Es wird jedoch als kompatibel zurückgegeben.  

    -   **Fehler:** Hiermit wird eine Liste aller Fehler für die ausgewählte Bereitstellung des Remoteverbindungsprofils basierend auf der Anzahl der betroffenen Bestände angezeigt. Sie können auf eine Regel doppelklicken, um im Arbeitsbereich **Bestand und Kompatibilität** unter dem Knoten **Benutzer** einen temporären Knoten zu erstellen. In diesem Knoten sind alle Geräte enthalten, für die bei diesem Profil Fehler erzeugt wurden. Wenn Sie ein Gerät auswählen, werden im Bereich **Bestandsdetails** die Geräte angezeigt, die vom ausgewählten Problem betroffen sind. Doppelklicken Sie auf ein Gerät in der Liste, um weitere Informationen zum Problem anzuzeigen.  

    -   **Nicht kompatibel:** Hiermit wird eine Liste aller nicht kompatiblen Regeln im Remoteverbindungsprofil basierend auf der Anzahl der betroffenen Bestände angezeigt. Sie können auf eine Regel doppelklicken, um im Arbeitsbereich **Bestand und Kompatibilität** unter dem Knoten **Benutzer** einen temporären Knoten zu erstellen. In diesem Knoten sind alle Geräte enthalten, für die bei diesem Profil Fehler erzeugt wurden. Wenn Sie ein Gerät auswählen, werden im Bereich **Bestandsdetails** die Geräte angezeigt, die vom ausgewählten Problem betroffen sind. Doppelklicken Sie auf ein Gerät in der Liste, um weitere Informationen zum Problem anzuzeigen.  

    -   **Unbekannt:** Hiermit wird eine Liste aller Geräte angezeigt, von denen keine Kompatibilität der ausgewählten Bereitstellung des Remoteverbindungsprofils zusammen mit dem aktuellen Clientstatus von Geräten gemeldet wurde.  

5.  Auf der Seite **Bereitstellungsstatus** finden Sie ausführliche Informationen zur Kompatibilität des bereitgestellten Remoteverbindungsprofils. Unter dem Knoten **Bereitstellungen** wird ein temporärer Knoten erstellt, mit dessen Hilfe Sie die Informationen schnell wiederfinden können.  

### <a name="view-compliance-results-with-reports"></a>Anzeigen von Kompatibilitätsergebnissen mit Berichten  
 Configuration Manager enthält integrierte Berichte, mit deren Hilfe Sie Informationen zu Remoteverbindungsprofilen überwachen können. Diese Berichte verfügen über die Berichtskategorie **Kompatibilitäts- und Einstellungsverwaltung**.  

> [!IMPORTANT]  
>  Sie müssen ein Platzhalterzeichen (%) verwenden, wenn Sie in Berichten zu Kompatibilitätseinstellungen die Parameter **Gerätefilter** und **Benutzerfilter** eingestellt haben.  

 Weitere Informationen zum Konfigurieren der Berichterstellung in Configuration Manager finden Sie unter [Berichterstellung in System Center Configuration Manager](/sccm/core/servers/manage/reporting).  
