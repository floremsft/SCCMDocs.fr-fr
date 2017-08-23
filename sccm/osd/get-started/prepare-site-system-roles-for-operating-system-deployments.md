---
title: "Vorbereiten von Standortsystemrollen für Betriebssystembereitstellungen | Microsoft-Dokumentation"
description: Konfigurieren Sie die Standortsystemrollen vor der Bereitstellung von Betriebssystemen in System Center Configuration Manager.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 0ef5f3ce-b0e4-4775-b5c2-b245e45b4194
caps.latest.revision: "11"
caps.handback.revision: "0"
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: 11c0f169afebdb071fefb5ce300fd1ae3481a94f
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="prepare-site-system-roles-for-operating-system-deployments-with-system-center-configuration-manager"></a>Vorbereiten von Standortsystemrollen für Betriebssystembereitstellungen mit System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Zum Bereitstellen von Betriebssystemen in System Center Configuration Manager müssen Sie zuerst die folgenden Standortsystemrollen vorbereiten, die besondere Konfigurationen und Überlegungen erfordern.

##  <a name="BKMK_DistributionPoints"></a> Verteilungspunkte  
 Die Standortsystemrolle „Verteilungspunkt“ enthält Quelldateien, die von Clients heruntergeladen werden können, darunter Anwendungsinhalt, Softwareupdates, Betriebssystemabbilder und Startabbilder. Sie können die Inhaltsverteilung mithilfe der Optionen für Bandbreite, Einschränkung und Zeitplanung steuern.  

 Sie benötigen unbedingt genügend Verteilungspunkte, um die Bereitstellung von Betriebssystemen auf Computern zu unterstützen. Außerdem ist es wichtig, die Platzierung dieser Verteilungspunkte in Ihrer Hierarchie zu planen. Einen Großteil der Informationen zur Planung finden Sie unter [Verwalten von Inhalt und Inhaltsinfrastruktur](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md). Es gibt jedoch einige zusätzliche Überlegungen zur Planung von Verteilungspunkten, die sich auf die Betriebssystembereitstellung beziehen.  

###  <a name="BKMK_AdditionalPlanning"></a> Zusätzliche Überlegungen zur Planung von Verteilungspunkten  
 Im Folgenden weitere Aspekte, die bei der Planung von Verteilungspunkten berücksichtigt werden sollten:  

-   **Wie kann ich unerwünschte Betriebssystembereitstellungen verhindern?**  

     Configuration Manager unterscheidet nicht zwischen Standortservern und anderen Zielcomputern in einer Sammlung. Wenn Sie eine erforderliche Tasksequenz für eine Sammlung bereitstellen, die einen Standortserver enthält, wird die Tasksequenz auf dem Standortserver genauso wie auf allen anderen Computern in der Sammlung ausgeführt. Stellen Sie sicher, dass die Betriebssystembereitstellung eine Sammlung mit den Clients verwendet, für die die Bereitstellung ausgeführt werden soll.  

     Sie können das Verhalten für Tasksequenzbereitstellungen mit hohem Risiko verwalten. Eine Bereitstellung mit hohem Risiko wird automatisch auf einem Client installiert und kann zu unerwünschten Ergebnissen führen. Ein Beispiel ist eine Tasksequenz, die als Zweck „Erforderlich“ aufweist und ein Betriebssystem bereitstellt. Um das Risiko einer unbeabsichtigten Bereitstellung mit hohem Risiko zu reduzieren, können Sie Einstellungen zur Bereitstellungsüberprüfung konfigurieren. Weitere Informationen finden Sie unter [Einstellungen zum Verwalten risikoreicher Bereitstellungen](../../protect/understand/settings-to-manage-high-risk-deployments.md).  

-   **Wie viele Computer können gleichzeitig ein Betriebssystemabbild von einem einzelnen Verteilungspunkt empfangen?**  

     Um die benötigte Anzahl von Verteilungspunkten zu schätzen, müssen die Verarbeitungsgeschwindigkeit und die E/A-Kapazität des Datenträgers am Verteilungspunkt, die verfügbare Netzwerkbandbreite sowie die Auswirkungen der Abbildpaketgröße auf diese Ressourcen berücksichtigt werden. Beispiel: In einem Ethernet-Netzwerk mit einer Übertragungsrate von 100 Megabit/s kann ein 4 GB großes Abbildpaket in einer Stunde theoretisch von maximal 11 Computern verarbeitet werden. Bei diesem Wert sind jedoch keine anderen Serverressourcenfaktoren berücksichtigt.  

     `100 Megabits/sec = 12.5 Megabytes/sec = 750 Megabytes/min = 45 Gigabytes/hour = 11 images @ 4GB per image.`  

     Falls Sie ein Betriebssystem innerhalb eines bestimmten Zeitrahmens auf einer bestimmten Anzahl von Computern bereitstellen müssen, verteilen Sie das Abbild auf eine geeignete Anzahl von Verteilungspunkten.  

-   **Kann ein Betriebssystem auf einem Verteilungspunkt bereitgestellt werden?**  

     Sie können ein Betriebssystem auf einem Verteilungspunkt bereitstellen, allerdings muss das Betriebssystemabbild von einem anderen Verteilungspunkt empfangen werden.  

###  <a name="BKMK_PXEDistributionPoint"></a> Konfigurieren von Verteilungspunkten zum Akzeptieren von PXE-Anforderungen  
 Zum Bereitstellen von Betriebssystemen für Configuration Manager-Clients, die PXE-Startanforderungen ausführen, müssen Sie mindestens einen Verteilungspunkt so konfigurieren, dass er PXE-Anforderungen akzeptiert. Sobald der Verteilungspunkt konfiguriert ist, reagiert er auf PXE-Startanforderungen und ermittelt die geeigneten Bereitstellungsaktionen.

> [!IMPORTANT]  
>  [Windows Deployment Services](../plan-design/infrastructure-requirements-for-operating-system-deployment.md#BKMK_WDS) muss auf allen PXE-fähigen Verteilungspunkten installiert sein.  

 Wenden Sie das folgende Verfahren an, um einen vorhandenen Verteilungspunkt so zu ändern, dass PXE-Anforderungen von ihm akzeptiert werden. Informationen zum Installieren eines neuen Verteilungspunkts finden Sie unter [Install or modify a distribution point](../../core/servers/deploy/configure/install-and-configure-distribution-points.md).  

#### <a name="to-modify-an-existing-distribution-point-to-accept-pxe-requests"></a>So ändern Sie einen vorhandenen Verteilungspunkt, damit PXE-Anforderungen akzeptiert werden  

1.  In der Configuration Manager-Konsole auf **Verwaltung**, erweitern Sie **Übersicht**, und klicken Sie auf **Verteilungspunkte**.  

2.  Wählen Sie den zu konfigurierenden Verteilungspunkt aus, und klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Eigenschaften** auf **Eigenschaften**.  

3.  Klicken Sie auf der Seite "Eigenschaften" für den Verteilungspunkt auf die Registerkarte **PXE** . Wählen Sie **PXE-Unterstützung für Clients aktivieren** aus, um PXE auf diesem Verteilungspunkt zu aktivieren.  

4.  Aktivieren Sie das Kontrollkästchen **Für PXE erforderliche Ports überprüfen** auf **Ja** , um zu bestätigen, dass Sie PXE aktivieren möchten. Configuration Manager konfiguriert die Standardports einer Windows-Firewall automatisch. Sie müssen die Ports manuell konfigurieren, wenn Sie eine andere Firewall verwenden.  

    > [!NOTE]  
    >  Wenn WDS und DHCP auf demselben Server installiert sind, müssen Sie WDS für das Lauschen an einem anderen Port konfigurieren (da DHCP am selben Port lauscht). Weitere Informationen finden Sie unter [Aspekte, wenn sich der Windows-Bereitstellungsdienst und DHCP auf demselben Server befinden](../plan-design/infrastructure-requirements-for-operating-system-deployment.md#BKMK_WDSandDHCP).  

5.  Wählen Sie **Antwort auf eingehende PXE-Anforderungen durch diesen Verteilungspunkt zulassen** aus, um WDS zu aktivieren und die Beantwortung eingehender PXE-Dienstanforderungen zu ermöglichen. Sie können Sie den Dienst mithilfe dieser Einstellung aktivieren oder deaktivieren, ohne die PXE-Funktionalität vom Verteilungspunkt zu entfernen.  

6.  Wählen Sie **Unterstützung für unbekannte Computer aktivieren** aus, um Betriebssysteme auf nicht von Configuration Manager verwalteten Computern bereitzustellen.  

7.  Wählen Sie **Kennwort erforderlich, wenn PXE von Computern verwendet wird**aus, und geben Sie ein sicheres Kennwort an, um die Sicherheit für Ihre PXE-Bereitstellungen zusätzlich zu erhöhen.  

8.  In the **Affinität zwischen Benutzer und Gerät** aus, wie der Verteilungspunkt Benutzer dem Zielcomputer für PXE-Bereitstellungen zuordnen soll.  

    -   Wählen Sie **Affinität zwischen Benutzer und Gerät nicht verwenden** aus, wenn Benutzer dem Zielcomputer nicht zugeordnet werden sollen.  

    -   Wählen Sie **Affinität zwischen Benutzer und Gerät nach manueller Genehmigung zulassen** aus, wenn für die Zuordnung von Benutzern und Zielcomputer die Genehmigung eines Administrators erforderlich sein soll.  

    -   Wählen Sie **Affinität zwischen Benutzer und Gerät nach automatischer Genehmigung zulassen** aus, um eine automatische Zuordnung von Benutzern und Zielcomputern ohne die Genehmigung eines Administrators zuzulassen.  

     Weitere Informationen finden Sie unter [Zuordnen von Benutzern zu einem Zielcomputer](../get-started/associate-users-with-a-destination-computer.md).  

9. Geben Sie an, ob vom Verteilungspunkt auf PXE-Anforderungen von allen oder nur von bestimmten Netzwerkschnittstellen geantwortet werden soll. Wenn der Verteilungspunkt nur auf bestimmte Netzwerkschnittstellen antworten soll, geben Sie die MAC-Adressen für jede Schnittstelle an.  

10. Geben Sie die Länge der Verzögerung (in Sekunden) an, bevor vom Verteilungspunkt auf Computeranforderungen reagiert wird, wenn mehrere PXE-fähige Verteilungspunkte verwendet werden.  

11. Klicken Sie auf **OK** , um die Eigenschaften des Verteilungspunkts zu aktualisieren.  

###  <a name="BKMK_RamDiskTFTP"></a> Anpassen der RamDisk-TFTP-Blockgröße und der Fenstergröße auf PXE-fähigen Verteilungspunkten  
Sie können die RamDisk-TFTP-Blockgröße und ab Configuration Manager Version 1606 die Fenstergröße für PXE-fähige Verteilungspunkte anpassen. Wenn Sie Ihr Netzwerk angepasst haben, kann dies wegen übermäßiger Block- oder Fenstergröße zu einem Timeout beim Herunterladen des Startimages führen. Durch Anpassen der RamDisk-TFTP-Blockgröße und der Fenstergröße können Sie den TFTP-Datenverkehr bei Verwendung von PXE für Ihre spezifischen Netzwerkanforderungen optimieren.   
Sie müssen die benutzerdefinierten Einstellungen in Ihrer Umgebung testen, um die effizienteste Einstellung zu ermitteln.  

-   **TFTP-Blockgröße:**Die Blockgröße ist die Größe der Datenpakete, die vom Server an den Client gesendet werden, der die Datei herunterlädt (wie in RFC 2347 erörtert). Mit einer größeren Blockgröße kann der Server weniger Pakete senden, sodass weniger Roundtripverzögerungen zwischen dem Server und dem Client auftreten. Große Blöcke führen jedoch zu fragmentierten Paketen, die von den meisten PXE-Clientimplementierungen nicht unterstützt werden.  

-   **TFTP-Fenstergröße:**TFTP erfordert ein Bestätigungspaket (acknowledgment packet; ACK) für jeden gesendeten Datenblock. Der Server sendet den nächsten Block in der Sequenz erst, wenn er das ACK-Paket für den vorherigen Block empfangen hat. TFTP-Fenster sind ein Feature in den Windows-Bereitstellungsdiensten, mit dem Sie definieren können, wie viele Datenblöcke ein Fenster füllen. Der Server sendet die Datenblöcke nach dem Back-to-Back-Prinzip, bis das Fenster gefüllt ist. Anschließend sendet der Client ein ACK-Paket. Durch Erhöhen diese Fenstergröße reduzieren Sie die Anzahl von Roundtripverzögerungen zwischen Client und Server und verringern die Gesamtzeit, die zum Herunterladen eines Startimages erforderlich ist.  


#### <a name="to-modify-the-ramdisk-tftp-window-size"></a>So ändern Sie die RamDisk-TFTP-Fenstergröße  

-   Fügen Sie auf PXE-fähigen Verteilungspunkten den folgenden Registrierungsschlüssel hinzu, um die RamDisk-TFTP-Fenstergröße anzupassen:  

     **Speicherort:**HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SMS\DP  
    Name: RamDiskTFTPWindowSize  

     **Typ:**REG_DWORD  

     **Wert**: &lt;angepasste Fenstergröße>  

 Der Standardwert ist 1 (1 Datenblock füllt das Fenster aus)  

#### <a name="to-modify-the-ramdisk-tftp-block-size"></a>So ändern Sie die RamDisk-TFTP-Blockgröße  

-   Fügen Sie auf PXE-fähigen Verteilungspunkten den folgenden Registrierungsschlüssel hinzu, um die RamDisk-TFTP-Fenstergröße anzupassen:  

     **Speicherort:**HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SMS\DP  
    Name: RamDiskTFTPBlockSize  

     **Typ:**REG_DWORD  

     **Wert**: &lt;angepasste Blockgröße>  

 Der Standardwert ist 4096 (4 KB).  


###  <a name="BKMK_DPMulticast"></a> Konfigurieren von Verteilungspunkten für die Multicastunterstützung  
 Multicast ist eine Netzwerkoptimierungsmethode, die Sie für Verteilungspunkte verwenden können, wenn von mehreren Clients wahrscheinlich das gleiche Betriebssystemabbild gleichzeitig heruntergeladen wird. Bei Verwendung von Multicast wird das Betriebssystemabbild vom Verteilungspunkt mithilfe von Multicast übertragen und kann von mehreren Computern gleichzeitig heruntergeladen werden, anstatt dass vom Verteilungspunkt über jeweils eine separate Verbindung Kopien der Daten an jeden Client gesendet werden. Sie müssen mindestens einen Verteilungspunkt für die Multicastunterstützung konfigurieren. Weitere Informationen finden Sie unter [Verwenden von Multicast zum Bereitstellen von Windows über das Netzwerk](../deploy-use/use-multicast-to-deploy-windows-over-the-network.md).  

 Sie müssen einen Verteilungspunkt für die Multicastunterstützung konfigurieren, bevor Sie das Betriebssystem bereitstellen. Ändern Sie einen vorhandenen Verteilungspunkt mithilfe des folgenden Verfahrens so, dass Multicast unterstützt wird. Informationen zum Installieren eines neuen Verteilungspunkts finden Sie unter [Installieren und Konfigurieren von Verteilungspunkten](../../core/servers/deploy/configure/install-and-configure-distribution-points.md).

#### <a name="to-enable-multicast-for-a-distribution-point"></a>So aktivieren Sie Multicast für einen Verteilungspunkt  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Verwaltung**.  

2.  Erweitern Sie im Arbeitsbereich **Verwaltung** den Eintrag **Übersicht**, und wählen Sie dann den Knoten **Verteilungspunkte** aus.  

3.  Wählen Sie den Verteilungspunkt aus, den Sie zum Multicast des Betriebssystemabbilds verwenden möchten.  

4.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Eigenschaften** auf **Eigenschaften**.  

5.  Wählen Sie die Registerkarte **Multicast** aus, und konfigurieren Sie die folgenden Optionen:  

    -   **Multicast aktivieren**: Sie müssen diese Option auswählen, damit Multicast vom Verteilungspunkt unterstützt wird.  

    -   **Multicastverbindungskonto**: Geben Sie ein Konto für die Verbindung mit der Standortdatenbank an.  

    -   **Multicastadresseinstellungen**: Geben Sie die IP-Adressen an, die zum Senden von Daten an die Zielcomputer verwendet werden sollen. Standardmäßig wird die IP-Adresse von einem DHCP-Server vergeben, der für die Verteilung von Multicastadressen aktiviert ist. Je nach Netzwerkumgebung können Sie IP-Adressen im Bereich zwischen 239.0.0.0 und 239.255.255.255 angeben.  

        > [!IMPORTANT]  
        >  Diese IP-Adressen müssen für die Zielcomputer, von denen das Betriebssystemabbild angefordert wird, zugänglich sein. Daher müssen die Router und Firewalls zwischen dem Zielcomputer und dem Standortserver so konfiguriert sein, dass Multicastdatenverkehr zugelassen wird.  

    -   **UDP-Portbereich**: Geben Sie den Bereich der UDP-Ports an, der zum Senden von Daten an die Zielcomputer verwendet werden soll.  

        > [!IMPORTANT]  
        >  Diese Ports müssen für die Zielcomputer, von denen das Betriebssystemabbild angefordert wird, zugänglich sein. Daher müssen die Router und Firewalls zwischen dem Zielcomputer und dem Standortserver so konfiguriert sein, dass Multicastdatenverkehr zugelassen wird.  

    -   **Geplanten Multicast aktivieren**: Geben Sie an, wie Configuration Manager die Startzeit der Bereitstellung des Betriebssystems für Zielcomputer steuert. Aktivieren Sie das Kontrollkästchen **Geplanten Multicast aktivieren**, und wählen Sie dann die folgenden Optionen aus.  

         Geben Sie im Feld **Startverzögerung für Sitzungen** an, wie viele Minuten Configuration Manager warten soll, bis auf die erste Bereitstellungsanforderung reagiert wird.  

         **Minimale Sitzungsgröße:** Geben Sie an, wie viele Anforderungen empfangen werden müssen, bevor Configuration Manager das Betriebssystem bereitstellt.  

    -   **Übertragungsrate**: Wählen Sie die Clientübertragungsrate zum Herunterladen von Daten auf die Zielcomputer aus.  

    -   **Max. Anzahl von Clients**: Geben Sie die maximale Anzahl von Zielcomputern, von denen das Betriebssystem von diesem Verteilungspunkt heruntergeladen werden kann, an.  

6.  Klicken Sie auf **OK**.  

##  <a name="BKMK_StateMigrationPoints"></a> Zustandsmigrationspunkt  
 Vom Zustandsmigrationspunkt werden die auf einem Computer erfassten Benutzerdaten gespeichert und anschließend auf einem anderen Computer wiederhergestellt. Wenn Sie jedoch Benutzereinstellungen für eine Betriebssystembereitstellung auf dem gleichen Computer erfassen, z. B. zur Aktualisierung des Betriebssystems auf dem Zielcomputer, können Sie die Daten auf dem gleichen Computer unter Verwendung von festen Links oder auf dem Zustandsmigrationspunkt speichern. Wenn Sie den Statusspeicher erstellen, wird von Configuration Manager bei einigen Computerbereitstellungen automatisch eine Zuordnung zwischen Statusspeicher und Zielcomputer erstellt. Berücksichtigen Sie bei der Planung des Zustandsmigrationspunkts die folgenden Faktoren:  

### <a name="user-state-size"></a>Größe des Benutzerzustands  
 Die Größe des Benutzerzustands hat direkte Auswirkungen auf den Speicherplatz auf dem Zustandsmigrationspunkt und die Netzwerkleistung während der Migration. Berücksichtigen Sie die Größe des Benutzerzustands und die Anzahl der zu migrierenden Computer. Überlegen Sie genau, welche Einstellungen vom Computer migriert werden müssen. Wenn beispielsweise bereits eine Sicherungskopie des Ordners **Eigene Dateien** auf einem Server erstellt wurde, braucht dieser Ordner im Rahmen der Abbildbereitstellung möglicherweise nicht migriert zu werden. Durch Vermeidung unnötiger Migrationen kann die Gesamtgröße des Benutzerzustands kleiner gehalten und die Auswirkung auf die Netzwerkleistung und den Speicherplatz auf dem Zustandsmigrationspunkt verringert werden.  

### <a name="user-state-migration-tool"></a>Windows-EasyTransfer (früher USMT)  
 Sie müssen ein Paket für Windows-EasyTransfer (früher USMT) verwenden, in dem auf Windows-EasyTransfer-Quelldateien verwiesen wird, um den Benutzerzustand während der Betriebssystembereitstellung erfassen und wiederherstellen zu können. Configuration Manager erstellt dieses Paket in der Configuration Manager-Konsole unter **Softwarebibliothek** > **Anwendungsverwaltung** > **Pakete**. Configuration Manager verwendet USMT 10.0, das über das Windows Assessment and Deployment Kit (Windows ADK) verteilt wird, damit der Benutzerzustand in einem Betriebssystem erfasst und in einem anderen Betriebssystem wiederhergestellt werden kann.  

 Eine Beschreibung verschiedener Migrationsszenarien für USMT 10.0 finden Sie unter [Häufige Migrationsszenarien](https://technet.microsoft.com/library/mt299169\(v=vs.85\).aspx).  

### <a name="retention-policy"></a>Aufbewahrungsrichtlinie  
 Beim Konfigurieren des Zustandsmigrationspunkts können Sie angeben, wie lange die auf dem Statusmigrationspunkt gespeicherten Benutzerzustandsdaten beibehalten werden sollen. Die Beibehaltungsdauer der auf dem Zustandsmigrationspunkt gespeicherten Daten hängt von zwei Faktoren ab:  

-   Auswirkung der gespeicherten Daten auf den Speicherplatz  

-   Mögliche Anforderung zur längeren Beibehaltung der Daten für den Fall, dass diese erneut migriert werden müssen  

 Die Zustandsmigration erfolgt in zwei Phasen: Erfassen der Daten und Wiederherstellen der Daten. Wenn Sie Daten erfassen, werden die Benutzerzustandsdaten gesammelt und auf dem Zustandsmigrationspunkt gespeichert. Wenn Sie die Daten wiederherstellen, werden die Benutzerzustandsdaten vom Zustandsmigrationspunkt abgerufen und auf den Zielcomputer geschrieben. Anschließend werden die gespeicherten Daten mithilfe des Tasksequenzschritts **Zustandsspeicher freigeben** freigegeben. Sobald die Daten freigegeben sind, wird der Beibehaltungszeitgeber gestartet. Wenn Sie die Option zum sofortigen Löschen der migrierten Daten ausgewählt haben, werden die Benutzerzustandsdaten sofort nach der Freigabe gelöscht. Wenn Sie die Option zum zeitlich begrenzten Beibehalten der Daten ausgewählt haben, werden die freigegebenen Daten nach Ablauf des festgelegten Zeitraums gelöscht. Je länger der festgelegte Beibehaltungszeitraum ist, desto mehr Speicherplatz wird voraussichtlich benötigt.  

### <a name="select-drive-to-store-user-state-migration-data"></a>Auswählen des Laufwerks zum Speichern von Daten zur Benutzerzustandsmigration  
 Wenn Sie den Zustandsmigrationspunkt konfigurieren, müssen Sie das Laufwerk auf dem Server angeben, auf dem die Benutzerzustandsmigrationsdaten gespeichert werden. Die Auswahl des Laufwerks erfolgt über eine vorgegebene Liste von Laufwerken. Einige dieser Laufwerke sind jedoch möglicherweise schreibgeschützte Laufwerke (z. B. CD-Laufwerke) oder Laufwerke ohne Netzwerkfreigabe. Darüber hinaus sind einige der Laufwerkbuchstaben möglicherweise überhaupt keinem Laufwerk auf dem Computer zugeordnet. Wenn Sie den Zustandsmigrationspunkt konfigurieren, müssen Sie ein beschreibbares, freigegebenes Laufwerk angeben.  

### <a name="configure-a-state-migration-point"></a>Konfigurieren eines Zustandsmigrationspunkts  
 Mithilfe der folgenden Methoden können Sie einen Zustandsmigrationspunkt zum Speichern der Benutzerzustandsdaten konfigurieren:  

-   Verwenden Sie den Assistenten zum Erstellen von ****  Standortsystemservern, um einen neuen Standortsystemserver für den Zustandsmigrationspunkt zu erstellen.  

-   Verwenden Sie den Assistenten zum Hinzufügen von ****  Standortsystemrollen, um einem vorhandenen Server einen Zustandsmigrationspunkt hinzuzufügen.  

 Wenn Sie diese Assistenten verwenden, werden Sie aufgefordert, die folgenden Angaben zum Zustandsmigrationspunkt zu machen:  

-   Die Ordner, in denen die Benutzerzustandsdaten gespeichert werden  

-   Die maximale Anzahl von Clients, von denen Daten auf dem Zustandsmigrationspunkt gespeichert werden können  

-   Der für einen Zustandsmigrationspunkt zum Speichern der Benutzerzustandsdaten mindestens erforderliche freie Speicherplatz  

-   Die Löschrichtlinie für die Rolle. Sie können angeben, ob die Benutzerzustandsdaten sofort oder erst nach Ablauf einer bestimmten Anzahl von Tagen nach ihrer Wiederherstellung auf einem Computer gelöscht werden.  

-   Ob vom Zustandsmigrationspunkt nur Anforderungen zum Wiederherstellen von Benutzerzustandsdaten beantwortet werden. Wenn Sie diese Option aktivieren, können Sie den Zustandsmigrationspunkt nicht zum Speichern von Benutzerzustandsdaten verwenden.  

 Die Schritte zum Installieren einer Standortsystemrolle finden Sie unter [Hinzufügen von Standortsystemrollen](../../core/servers/deploy/configure/add-site-system-roles.md).  
