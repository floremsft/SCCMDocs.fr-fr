---
title: "Sicherheit und Datenschutz für die Betriebssystembereitstellung | Microsoft-Dokumentation"
description: "Hier finden Sie Informationen zu Sicherheit und Datenschutz für die Betriebssystembereitstellung in System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5ee5928f-3d72-4b00-8156-1e0d1030a96c
caps.latest.revision: "6"
caps.handback.revision: "0"
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: 5632a753fc565312a80b2ed69ce438335b3fad50
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="security-and-privacy-for-operating-system-deployment-in-system-center-configuration-manager"></a>Sicherheit und Datenschutz bei der Betriebssystembereitstellung in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Dieses Thema enthält Informationen zur Sicherheit und zum Datenschutz für die Betriebssystembereitstellung in System Center Configuration Manager.  

##  <a name="BKMK_Security_HardwareInventory"></a> Bewährte Sicherheitsmethoden für die Betriebssystembereitstellung  
 Wenden Sie die folgenden bewährten Sicherheitsmethoden für die Bereitstellung von Betriebssystemen mit Configuration Manager an:  

-   **Implementieren Sie Zugriffssteuerungen zum Schutz startbarer Medien.**  

     Wenn Sie startbare Medien erstellen, weisen Sie zum Schutz der Medien immer ein Kennwort zu. Selbst mit einem Kennwort werden aber nur Dateien verschlüsselt, die sensible Informationen enthalten, und alle Dateien können überschrieben werden.  

     Kontrollieren Sie den physischen Zugriff auf die Medien, um zu verhindern, dass ein Angreifer mithilfe kryptografischer Angriffe Zugang zum Clientauthentifizierungszertifikat erhält.  

     Auf den Inhalt wird ein Hashwert angewendet, und der Inhalt muss mit der Originalrichtlinie verwendet werden, um zu verhindern, dass von einem Client Inhalt oder eine Clientrichtlinie installiert wird, der bzw. die manipuliert wurde.  Wenn für den Inhaltshash ein Fehler auftritt oder die Überprüfung der Übereinstimmung des Inhalts mit der Richtlinie nicht erfolgreich ist, werden die startbaren Medien vom Client nicht verwendet. Nur der Inhalt wird mit einem Hashwert versehen. Für die Richtlinie gilt dies nicht, aber die Richtlinie wird verschlüsselt und geschützt, wenn Sie ein Kennwort angeben. So wird Angreifern das Ändern der Richtlinie erschwert.  

-   **Verwenden Sie einen sicheren Speicherort, wenn Sie Medien für Betriebssystemimages erstellen.**  

     Wenn nicht autorisierte Benutzer Zugriff auf den Speicherort haben, können sie die von Ihnen erstellten Dateien manipulieren und den gesamten verfügbaren Speicherplatz in Anspruch nehmen, sodass bei der Medienerstellung ein Fehler auftritt.  

-   **Schützen Sie Zertifikatdateien (.pfx) durch ein sicheres Kennwort. Falls Sie diese Dateien im Netzwerk speichern, achten Sie beim Importieren der Dateien in Configuration Manager darauf, dass der Netzwerkkanal sicher ist.**  

     Wenn für das Importieren des Clientauthentifizierungszertifikats, das Sie für startbare Medien verwenden, ein Kennwort erforderlich ist, ist das Zertifikat vor Angriffen geschützt.  

     Verwenden Sie SMB-Signaturen oder IPsec zwischen Netzwerkspeicherort und Standortserver, um einen Angreifer an der Manipulation der Zertifikatdatei zu hindern.  

-   **Ist das Clientzertifikat beschädigt, blockieren Sie es über Configuration Manager, und sperren Sie es, falls es sich um ein PKI-Zertifikat handelt.**  

     Zum Bereitstellen eines Betriebssystems mithilfe startbarer Medien und PXE-Start benötigen Sie ein Clientauthentifizierungszertifikat mit einem privaten Schlüssel. Sollte das Zertifikat gefährdet sein, blockieren Sie es im Arbeitsbereich **Verwaltung** über die Knoten **Zertifikate** und **Sicherheit** .  

-   **Wenn sich der SMS-Anbieter auf einem anderen Computer als dem Standortserver befindet, sichern Sie den Kommunikationskanal zum Schutz von Startimages.**  

     Wenn Startabbilder geändert werden und der SMS-Anbieter auf einem anderen Server als dem Standortserver ausgeführt wird, sind die Startabbilder anfällig für Angriffe. Schützen Sie den Netzwerkkanal zwischen diesen Computern mithilfe von SMB-Signaturen oder IPsec.  

-   **Aktivieren Sie Verteilungspunkte für die PXE-Clientkommunikation nur in sicheren Netzwerksegmenten.**  

     Wenn von einem Client eine PXE-Startanforderung gesendet wird, haben Sie keine Möglichkeit sicherzustellen, dass die Anforderung von einem gültigen PXE-fähigen Verteilungspunkt beantwortet wird. In diesem Szenario bestehen die folgenden Sicherheitsrisiken:  

    -   Von einem nicht autorisierten Verteilungspunkt, von dem PXE-Anforderungen beantwortet werden, könnte ein manipuliertes Abbild an Clients bereitgestellt werden.  

    -   Ein Angreifer könnte einen Man-in-the-Middle-Angriff gegen das von PXE verwendete TFTP-Protokoll starten und schädlichen Code mit den Betriebssystemdateien senden oder einen nicht autorisierten Client erstellen, von dem TFTP-Anforderungen direkt an den PXE-Dienstpunkt gesendet werden.  

    -   Ein Angreifer könnte einen schädlichen Client verwenden, um einen DoS-Angriff gegen den Verteilungspunkt zu starten.  

     Sorgen Sie bei Netzwerksegmenten, in denen im Zusammenhang mit PXE-Anforderungen von Clients auf Verteilungspunkte zugegriffen wird, für einen umfassendem Schutz.  

    > [!WARNING]  
    >  Wegen dieser Sicherheitsrisiken wird von der Aktivierung eines Verteilungspunkts für die PXE-Kommunikation abgeraten, wenn er sich in einem nicht vertrauenswürdigen Netzwerk (z. B. ein Umkreisnetzwerk) befindet.  

-   **Konfigurieren Sie PXE-fähige Verteilungspunkte so, dass diese nur an bestimmten Netzwerkschnittstellen auf PXE-Anforderungen reagieren.**  

     Wenn Sie zulassen, dass die Reaktion des Verteilungspunkts auf PXE-Anforderungen an allen Netzwerkschnittstellen möglich ist, wird der PXE-Dienst möglicherweise für nicht vertrauenswürdige Netzwerke verfügbar.  

-   **Legen Sie fest, dass für den PXE-Start ein Kennwort erforderlich ist.**  

     Wenn Sie festlegen, dass für den PXE-Start ein Kennwort erforderlich ist, wird die Sicherheit des PXE-Startprozesses verbessert, und der Beitritt nicht autorisierter Clients zur Configuration Manager-Hierarchie wird verhindert.  

-   **Schließen Sie in ein Image, das für einen PXE-Start oder Multicast vorgesehen ist, keine Branchenanwendungen oder Software mit sensiblen Daten ein.**  

     Mit dem PXE-Start und Multicast sind grundsätzlich Sicherheitsrisiken verbunden. Verringern Sie daher das Risiko für den Fall, dass das Betriebssystemabbild von einem nicht autorisierten Computer heruntergeladen wird.  

-   **Schließen Sie in Softwarepakete, die mithilfe von Tasksequenzvariablen installiert werden, keine Branchenanwendungen oder Software mit sensiblen Daten ein.**  

     Wenn Sie Softwarepakete mithilfe von Tasksequenzvariablen bereitstellen, ist eine Installation der Software auf Geräten und für Benutzer möglich, die nicht zum Empfangen dieser Software autorisiert sind.  

-   **Sichern Sie beim Migrieren des Benutzerstatus den Netzwerkkanal zwischen dem Client und dem Statusmigrationspunkt mithilfe von SMB-Signaturen oder IPsec.**  

     Nachdem die erste Verbindung über HTTP hergestellt wurde, werden die Migrationsdaten für den Benutzerzustand mithilfe von SMB übertragen.  Wenn Sie den Netzwerkkanal nicht sichern, können diese Daten von einem Angreifer gelesen und geändert werden.  

-   **Verwenden Sie die aktuelle Version von Windows-EasyTransfer (früher USMT), die von Configuration Manager unterstützt wird.**  

     Die aktuelle Version von Windows-EasyTransfer umfasst Sicherheitsverbesserungen und bessere Steuerungsmöglichkeiten für die Migration von Benutzerzustandsdaten.  

-   **Löschen Sie Ordner auf dem Statusmigrationspunkt manuell, wenn sie außer Betrieb gesetzt werden.**  

     Wenn Sie einen Ordner für einen Statusmigrationspunkt in der Configuration Manager-Konsole in den Eigenschaften des Statusmigrationspunkts entfernen, bleibt der physische Ordner weiter bestehen. Sie müssen die Netzwerkfreigabe manuell entfernen und den Ordner löschen, um zu verhindern, dass die Migrationsdaten für den Benutzerzustand offengelegt werden.  

-   **Konfigurieren Sie die Löschrichtlinie so, dass der Benutzerstatus nicht sofort gelöscht wird.**  

     Wenn Sie die Löschrichtlinie auf dem Zustandsmigrationspunkt so konfigurieren, dass zum Löschen markierte Daten sofort gelöscht werden, und es einem Angreifer vor dem gültigen Computer gelingt, die Benutzerzustandsdaten abzurufen, werden die Benutzerzustandsdaten sofort gelöscht. Legen Sie das Intervall **Löschen nach** auf eine Dauer fest, die dafür ausreicht, die erfolgreiche Wiederherstellung der Benutzerzustandsdaten zu überprüfen.  

-   **Löschen Sie Computerzuordnungen manuell, wenn die Wiederherstellung der Migrationsdaten für den Benutzerstatus abgeschlossen ist und überprüft wurde.**  

     Computerzuordnungen werden von Configuration Manager nicht automatisch entfernt. Schützen Sie die Identität von Benutzerzustandsdaten, indem Sie Computerzuordnungen, die nicht mehr benötigt werden, manuell löschen.  

-   **Sichern Sie die Migrationsdaten für den Benutzerstatus auf dem Statusmigrationspunkt manuell.**  

     Die Migrationsdaten für den Benutzerstatus werden bei der Configuration Manager-Sicherung nicht berücksichtigt.  

-   **Denken Sie daran, nach der Installation des Betriebssystems BitLocker zu aktivieren.**  

     Wenn BitLocker von einem Computer unterstützt wird und Sie das Betriebssystem unbeaufsichtigt installieren möchten, müssen Sie BitLocker mithilfe eines Tasksequenzschritts deaktivieren. Nach der Installation des Betriebssystems wird BitLocker von Configuration Manager nicht aktiviert, und Sie müssen es daher manuell erneut aktivieren.  

-   **Implementieren Sie Zugriffssteuerungen zum Schutz der vorab bereitgestellten Medien.**  

     Kontrollieren Sie den physischen Zugriff auf die Medien, um zu verhindern, dass ein Angreifer mithilfe kryptografischer Angriffe Zugang zum Clientauthentifizierungszertifikat und zu sensiblen Daten erhält.  

-   **Implementieren Sie Zugriffssteuerungen zum Schutz des Imageerstellungsprozesses auf dem Referenzcomputer.**  

     Sorgen Sie dafür, dass sich der zur Erfassung von Betriebssystemabbildern verwendete Referenzcomputer in einer sicheren Umgebung befindet und die angemessenen Zugriffssteuerungen implementiert sind, damit unerwartete Software oder Malware nicht installiert und versehentlich ins aufgenommene Abbild einbezogen werden kann. Sorgen Sie bei der Erfassung des Abbilds dafür, dass der Dateifreigabepfad des Zielnetzwerks sicher ist, damit das Abbild nach der Erfassung nicht manipuliert werden kann.  

-   **Installieren Sie immer die neuesten Sicherheitsupdates auf dem Referenzcomputer.**  

     Wenn die aktuellen Sicherheitsupdates auf dem Referenzcomputer vorhanden sind, werden die Sicherheitsrisiken beim ersten Start neuer Computer reduziert.  

-   **Wenn Sie Betriebssysteme für einen unbekannten Computer bereitstellen müssen, implementieren Sie Zugriffssteuerungen, um zu verhindern, dass von nicht autorisierten Computer eine Verbindung mit dem Netzwerk hergestellt wird.**  

     Die Bereitstellung unbekannter Computer kann sich bei der bedarfsgesteuerten Bereitstellung neuer Computer zwar als praktisch erweisen, birgt jedoch auch die Gefahr, dass Angreifer sich im Netzwerk als vertrauenswürdige Clients anmelden. Schränken Sie den physischen Zugriff auf das Netzwerk ein, und überwachen Sie Clients, um nicht autorisierte Computer zu erkennen. Zudem können auf Computern, die PXE-initiierte Betriebssystembereitstellungen verwenden, während der Betriebssystembereitstellung alle Daten zerstört werden. Dies kann dazu führen, dass unabsichtlich neu formatierte Systeme nicht mehr verfügbar sind.  

-   **Aktivieren Sie die Verschlüsselung für Multicastpakete.**  

     Sie haben bei jedem Paket der Betriebssystembereitstellung die Möglichkeit, die Verschlüsselung zu aktivieren, wenn das Paket von Configuration Manager mithilfe von Multicast übertragen wird. Auf diese Weise verhindern Sie die Teilnahme nicht autorisierter Computer an der Multicastsitzung sowie die Manipulation der Übertragung durch Angreifer.  

-   **Überwachen Sie das System auf nicht autorisierte, multicastfähige Verteilungspunkte.**  

     Wenn Angreifer Zugriff auf Ihr Netzwerk erhalten, können sie nicht autorisierte Multicastserver konfigurieren, um die Betriebssystembereitstellung zu spoofen.  

-   **Wenn Sie Tasksequenzen an einen Netzwerkspeicherort exportieren, sichern Sie den Speicherort und den Netzwerkkanal.**  

     Schränken Sie die Anzahl der Personen ein, die auf den Netzwerkordner zugreifen können.  

     Verwenden Sie SMB-Signaturen oder IPsec zwischen Netzwerkspeicherort und Standortserver, um einen Angreifer an der Manipulation der exportierten Tasksequenz zu hindern.  

-   **Sichern Sie den Kommunikationskanal, wenn Sie eine virtuelle Festplatte zu Virtual Machine Manager hochladen.**  

     Vermeiden Sie die Manipulation von Daten bei der Übertragung im Netzwerk, indem Sie zwischen dem Computer, auf dem die Configuration Manager-Konsole ausgeführt wird, und jenem, auf dem Virtual Machine Manager ausgeführt wird, das IPsec- (Internetprotokollsicherheit) oder das SMB-Protokoll (Server Message Block) verwenden.  

-   **Falls Sie das ausführende Konto für die Tasksequenz verwenden müssen, treffen Sie zusätzliche Sicherheitsvorkehrungen.**  

     Treffen Sie die folgenden Sicherheitsvorkehrungen, wenn Sie das ausführende Konto für die Tasksequenz verwenden:  

    -   Verwenden Sie ein Konto mit geringstmöglichen Berechtigungen.  

    -   Verwenden Sie für dieses Konto nicht das Netzwerkzugriffskonto.  

    -   Versehen Sie das Konto niemals mit Domänenadministratorrechten.  

     Beachten Sie auch Folgendes:  

    -   Konfigurieren Sie niemals servergespeicherte Profile für dieses Konto. Wenn die Tasksequenz ausgeführt wird, wird das servergespeicherte Profil für das Konto heruntergeladen, sodass es anfällig für einen Zugriff auf dem lokalen Computer wird.  

    -   Beschränken Sie den Kontoumfang. Erstellen Sie beispielsweise für jede Tasksequenz ein anderes ausführendes Konto, sodass bei der Gefährdung eines Kontos nur die Clientcomputer betroffen sind, auf die dieses Konto Zugriff hat. Wenn für die Befehlszeile Administratorrechte auf dem Computer erforderlich sind, erwägen Sie die Erstellung eines lokalen Administratorkontos lediglich für das ausführende Konto für die Tasksequenz auf allen Computern, von denen die Tasksequenz ausgeführt wird. Löschen Sie das Konto, sobald es nicht mehr benötigt wird.  

-   **Überwachen Sie die Administratoren, denen die Sicherheitsrolle „Betriebssystembereitstellungs-Manager“ zugewiesen wurde, und beschränken Sie ihre Anzahl.**  

     Administratoren, denen die Sicherheitsrolle „Betriebssystembereitstellungs-Manager“ zugewiesen wurde, können selbstsignierte Zertifikate erstellen, mit deren Hilfe die Identität eines Clients angenommen und die Clientrichtlinie von Configuration Manager abgerufen werden kann.  

### <a name="security-issues-for-operating-system-deployment"></a>Sicherheitsprobleme bei der Betriebssystembereitstellung  
 Obwohl die Betriebssystembereitstellung eine bequeme Methode zur Bereitstellung der sichersten Betriebssysteme und Konfigurationen für Computer in Ihrem Netzwerk darstellt, ist sie mit den folgenden Sicherheitsrisiken verbunden:  

-   Offenlegung von Informationen und Denial-of-Service  

     Sollte ein Angreifer Kontrolle über Ihre Configuration Manager-Infrastruktur erhalten, könnte er beliebige Tasksequenzen ausführen und zum Beispiel die Festplatten auf allen Clientcomputern formatieren. Tasksequenzen können so konfiguriert werden, dass sie vertrauliche Informationen wie Konten mit Berechtigungen zum Domänenbeitritt und Volumenlizenzschlüssel enthalten.  

-   Identitätsvortäuschung und Rechteerweiterungen  

     Mit Tasksequenzen kann der Beitritt eines Computers zu einer Domäne bewirkt werden, und hierdurch kann ein nicht autorisierter Computer möglicherweise einen authentifizierten Netzwerkzugriff erhalten. Ein weiterer Aspekt, der bei der Sicherheit der Betriebssystembereitstellung beachtet werden muss, ist der Schutz des Clientauthentifizierungszertifikats, das für startbare Tasksequenzmedien und für die Bereitstellung mit PXE-Start verwendet wird. Wenn Sie ein Clientauthentifizierungszertifikat erfassen, hat ein Angreifer die Gelegenheit, den privaten Schlüssel im Zertifikat abzurufen und dann die Identität eines gültigen Clients im Netzwerk anzunehmen.  

     Wenn das Clientauthentifizierungszertifikat, das für startbare Tasksequenzmedien und für die Bereitstellung mit PXE-Start verwendet wird, von einem Angreifer abgerufen wird, kann er gegenüber Configuration Manager die Identität eines gültigen Clients annehmen. In diesem Fall kann von dem nicht autorisierten Computer die Richtlinie, die möglicherweise sensible Daten enthält, heruntergeladen werden.  

     Wenn das Netzwerkzugriffskonto von Clients zum Zugreifen auf Daten verwendet wird, die auf dem Zustandsmigrationspunkt gespeichert sind, verfügen diese Clients praktisch über dieselbe Identität und können auf Zustandsmigrationsdaten eines anderen Clients zugreifen, von dem das Netzwerkzugriffskonto genutzt wird. Die Daten werden verschlüsselt, damit sie nur vom ursprünglichen Client gelesen werden können. Es ist jedoch möglich, die Daten zu manipulieren oder zu löschen.  

-   Die Clientauthentifizierung für den Statusmigrationspunkt wird mithilfe eines Configuration Manager-Tokens durchgeführt, das vom Verwaltungspunkt ausgegeben wird.  

     Außerdem wird der Umfang der auf dem Statusmigrationspunkt gespeicherten Daten von Configuration Manager weder eingeschränkt noch verwaltet. Ein Angreifer könnte den verfügbaren Speicherplatz gänzlich in Anspruch nehmen und einen DoS-Zustand (Denial-of-Service) verursachen.  

-   Wenn Sie Sammlungsvariablen verwenden, können lokale Administratoren potenziell vertrauliche Informationen lesen.  

     Obwohl Sammlungsvariablen ein flexibles Verfahren zum Bereitstellen von Betriebssystemen darstellen, kann dies zur Offenlegung von Informationen führen.  

##  <a name="BKMK_Privacy_HardwareInventory"></a> Informationen zum Datenschutz für die Betriebssystembereitstellung  
 Neben dem Bereitstellen von Betriebssystemen für Computer ohne Betriebssystem können mit Configuration Manager Benutzerdateien und -einstellungen von einem Computer zu einem anderen migriert werden. Der Administrator konfiguriert, welche Informationen übertragen werden. Dies umfasst persönliche Datendateien, Konfigurationseinstellungen und Browsercookies.  

 Die Informationen werden auf einem Zustandsmigrationspunkt gespeichert und bei der Übertragung und Speicherung verschlüsselt. Die Informationen können vom neuen, den Zustandsinformationen zugeordneten Computer abgerufen werden. Verliert der neue Computer den Schlüssel zum Abruf der Informationen, kann ein Configuration Manager-Administrator mit dem Recht „Wiederherstellungsinformationen anzeigen“ für Computerzuordnungsinstanzobjekte auf die Informationen zugreifen und sie einem neuen Computer zuordnen. Nachdem der neue Computer die Zustandsinformationen wiederhergestellt hat, werden die Daten standardmäßig nach einem Tag gelöscht. Sie können konfigurieren, wann der Zustandsmigrationspunkt zum Löschen markierte Daten entfernt. Die Zustandsmigrationsinformationen werden nicht in der Standortdatenbank gespeichert und nicht an Microsoft gesendet.  

 Wenn Sie Startmedien für die Bereitstellung von Betriebssystemabbildern verwenden, achten Sie darauf, stets die Standardoption für den Kennwortschutz der Startmedien zu verwenden. Mit dem Kennwort werden alle in der Tasksequenz gespeicherten Variablen verschlüsselt. Alle nicht in einer Variablen gespeicherten Informationen können aber Sicherheitsrisiken ausgesetzt sein.  

 Bei der Betriebssystembereitstellung können mithilfe von Tasksequenzen viele verschiedene Tasks wie die Installation von Anwendungen und Softwareupdates ausgeführt werden. Wenn Sie Tasksequenzen konfigurieren, berücksichtigen Sie auch die mit der Installation von Software verbundenen Auswirkungen auf den Datenschutz.  

 Wenn Sie eine virtuelle Festplatte in Virtual Machine Manager hochladen, ohne das Abbild zuvor mithilfe von Sysprep bereinigt zu haben, können auf der hochgeladenen virtuellen Festplatte persönliche Daten aus dem Ursprungsabbild enthalten sein.  

 Die Betriebssystembereitstellung wird von Configuration Manager nicht standardmäßig implementiert. Es müssen mehrere Konfigurationsschritte ausgeführt werden, bevor Sie Benutzerstatusdaten sammeln oder Tasksequenzen bzw. Startimages erstellen können.  

 Denken Sie über Ihre Datenschutzanforderungen nach, bevor Sie die Betriebssystembereitstellung konfigurieren.  
