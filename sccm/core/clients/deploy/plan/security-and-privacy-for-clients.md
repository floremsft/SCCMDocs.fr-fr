---
title: Clientsicherheit und Datenschutz | Microsoft-Dokumentation
description: "Erfahren Sie mehr über Sicherheit und Datenschutz für Clients in System Center Configuration Manager."
ms.custom: na
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-client
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: c1d71899-308f-49d5-adfa-3a3ec0163ed8
caps.latest.revision: "10"
caps.handback.revision: "0"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 1d871b0e1a2897c236d17211a23c9c7d93e42313
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="security-and-privacy-for-clients-in-system-center-configuration-manager"></a>Sicherheit und Datenschutz für Clients in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Dieser Artikel enthält Informationen zur Sicherheit und zum Datenschutz von Clients in System Center Configuration Manager sowie von mobilen Geräten, die vom Exchange Server-Connector verwaltet werden:  

##  <a name="BKMK_Security_Cliients"></a> Bewährte Sicherheitsmethoden für Clients  
 Wenn Configuration Manager Daten zulässt, die von Geräten mit dem Configuration Manager-Client stammen, ist der Standort für potenzielle Angriffe durch Clients anfällig. Beispielsweise könnten falsch formatierte Inventurdaten gesendet werden, und auch eine Überlastung der Standortsysteme wäre möglich. Stellen Sie den Configuration Manager-Client nur auf vertrauenswürdigen Geräten bereit. Schützen Sie den Standort außerdem anhand der folgenden bewährten Sicherheitsmethoden vor nicht autorisierten oder gefährdeten Geräten:  

 **Verwenden Sie PKI-Zertifikate (Public Key-Infrastruktur) für die Clientkommunikation mit Standortsystemen, auf denen IIS ausgeführt werden.**  

-   Legen Sie unter **Einstellungen des Standortsystems** die Option **Nur HTTPS**als Standorteigenschaft fest.  

-   Installieren Sie Clients mit der CCMSetup-Eigenschaft **/UsePKICert** .  

-   Verwenden Sie eine Zertifikatsperrliste (Certificate Revocation List, CRL), und sorgen Sie dafür, dass sie stets für Clients und kommunizierende Servern zugänglich ist.  

 Diese Zertifikate sind für die Clients mobiler Geräte und für Clientcomputerverbindungen im Internet erforderlich. Sie werden für alle Clientverbindungen im Intranet, mit Ausnahme von Verteilungspunkten, empfohlen.  

 Weitere Informationen zu den PKI-Zertifikatanforderungen und deren Verwendung zum Schutz von Configuration Manager finden Sie unter [PKI-Zertifikatanforderungen für System Center Configuration Manager](../../../../core/plan-design/network/pki-certificate-requirements.md).  

 **Genehmigen Sie Clientcomputer aus vertrauenswürdigen Domänen automatisch, und überprüfen und genehmigen Sie andere Computer manuell.**  

 Sie können festlegen, dass die Genehmigung für die Hierarchie manuell erfolgt. Alternativ können Sie angeben, dass Computer in vertrauenswürdigen Domänen bzw. alle Computer automatisch genehmigt werden. Die sicherste Genehmigungsmethode besteht darin, Clients in vertrauenswürdigen Domänen automatisch zu genehmigen und dann alle anderen Computer manuell zu prüfen und zu genehmigen. Die automatische Genehmigung aller Clients ist nur dann empfehlenswert, wenn Sie über andere Zugriffssteuerungsmethoden verfügen, mit denen Sie verhindern können, dass nicht vertrauenswürdige Computer auf das Netzwerk zugreifen.  

 Durch die Genehmigung geben Sie an, dass ein von Ihnen als vertrauenswürdig eingestufter Computer von Configuration Manager verwaltet werden soll, falls Sie die PKI-Authentifizierung nicht verwenden können.  

 Weitere Informationen zum manuellen Genehmigen von Computern finden Sie unter [Verwalten von Clients mithilfe des Knotens „Geräte“](../../../../core/clients/manage/manage-clients.md#BKMK_ManagingClients_DevicesNode).  

 **Verlassen Sie sich nicht nur auf die Blockierung, um zu verhindern, dass Clients auf die Configuration Manager-Hierarchie zugreifen.**  

 Blockierte Clients werden von der Configuration Manager-Infrastruktur abgewiesen, sodass sie nicht mit Standortsystemen kommunizieren können, um Richtlinien herunterzuladen, Inventurdaten hochzuladen oder Zustands- bzw. Statusmeldungen zu senden. Sie sollten sich aber nicht darauf verlassen, dass die Blockierung einen ausreichenden Schutz der Configuration Manager-Hierarchie vor nicht vertrauenswürdigen Computern darstellt, wenn HTTP-Clientverbindungen von Standortsystemen akzeptiert werden. In diesem Fall könnte ein blockierter Client mit einem selbstsignierten Zertifikat und einer Hardware-ID wieder dem Standort hinzugefügt werden. Die Blockierung dient zum Blockieren verlorener oder gefährdeter Startmedien, wenn Sie ein Betriebssystem für Clients bereitstellen und HTTPS-Clientverbindungen von allen Standortsystemen akzeptiert werden. Wenn Sie eine Public Key-Infrastruktur (PKI) verwenden, von der eine Zertifikatsperrliste (Certificate Revocation List, CRL) unterstützt wird, sollte zunächst eine Zertifikatsperre zur Verteidigung gegen möglicherweise gefährdete Zertifikate in Betracht gezogen werden. Das Blockieren von Clients in Configuration Manager bietet eine zweite Stufe der Verteidigung, mit der die Standorthierarchie geschützt wird.  

 Weitere Informationen finden Sie unter [Bestimmen, ob Clients in System Center Configuration Manager blockiert werden sollen](../../../../core/clients/deploy/plan/determine-whether-to-block-clients.md).  

 **Verwenden Sie die sichersten Clientinstallationsmethoden, die für Ihre Umgebung geeignet sind:**  

-   Bei Domänencomputern sind die gruppenrichtlinienbasierte Clientinstallation und die softwareupdatebasierte Clientinstallationsmethode sicherer als die Clientpushinstallation.  

-   Die Imageerstellung und die manuelle Installation können äußerst sicher sein, wenn Sie Zugriffs- und Änderungssteuerungen anwenden.  

 Die Clientpushinstallation stellt die am wenigsten sichere Clientinstallationsmethode dar. Dies liegt an ihren zahlreichen Abhängigkeiten, darunter lokale Administratorberechtigungen, die Admin$-Freigabe und zahlreiche Firewall-Ausnahmen. Durch diese Abhängigkeiten wird die Angriffsfläche vergrößert.  

 Weitere Informationen zu den anderen Clientinstallationsmethoden finden Sie unter [Clientinstallationsmethoden in System Center Configuration Manager](../../../../core/clients/deploy/plan/client-installation-methods.md).  

 Wählen Sie außerdem nach Möglichkeit immer eine Clientinstallationsmethode, für die möglichst wenige Sicherheitsberechtigungen in Configuration Manager erforderlich sind. Schränken Sie zudem die Anzahl der Administratoren ein, deren Sicherheitsrollen Berechtigungen umfassen, die für andere Zwecke als die Clientbereitstellung eingesetzt werden könnten. Beispielsweise ist für ein automatisches Clientupgrade die Sicherheitsrolle **Hauptadministrator** erforderlich, durch die einem Administrator sämtliche Sicherheitsberechtigungen erteilt werden.  

 Weitere Informationen zu den Abhängigkeiten und Sicherheitsberechtigungen für jede Clientinstallationsmethode finden Sie im Abschnitt „Installationsmethodenabhängigkeiten“ unter [Voraussetzungen für Computerclients](../../../../core/clients/deploy/prerequisites-for-deploying-clients-to-windows-computers.md#BKMK_prereqs_computers).  

 **Falls Sie die Clientpushinstallation verwenden müssen, ergreifen Sie weitere Maßnahmen zum Schutz des Clientpushinstallationskontos.**  

 Dieses Konto muss zwar auf jedem Computer, auf dem die Configuration Manager-Clientsoftware installiert wird, der lokalen Gruppe **Administratoren** angehören, aber Sie dürfen es keinesfalls der Gruppe **Domänen-Admins** hinzufügen. Erstellen Sie stattdessen eine globale Gruppe, und fügen Sie diese globale Gruppe der lokalen Gruppe **Administratoren** auf den Clientcomputern hinzu. Sie können auch ein Gruppenrichtlinienobjekt erstellen, um eine Einstellung für eingeschränkte Gruppen hinzufügen, mit der das Clientpushinstallationskonto der lokalen Gruppe **Administratoren** hinzugefügt wird.  

 Erhöhen Sie die Sicherheit, indem Sie mehrere Clientpushinstallationskonten erstellen. Erteilen Sie jedem dieser Konten Administratorrechte für eine beschränkte Anzahl von Computern. Bei einer Gefährdung eines der Konten sind dann lediglich die Clientcomputer betroffen, auf die über dieses Konto zugegriffen werden kann.  

 **Entfernen Sie Zertifikate vor der Imageerstellung von Clientcomputern.**  

 Wenn Sie Clients mithilfe einer Imagingtechnologie bereitstellen möchten, entfernen Sie Zertifikate wie PKI-Zertifikate mit integrierter Clientauthentifizierung und selbstsignierte Zertifikate vor der Imageerstellung. Wenn Sie diese Zertifikate nicht entfernen, könnte von Clients die Identität anderer Clients angenommen werden, und Sie könnten die Daten für die einzelnen Clients nicht überprüfen.  

 Weitere Informationen zur Vorbereitung eines Computers für die Imageerstellung mit der Systemvorbereitung finden Sie in der Dokumentation zur Windows-Bereitstellung.  

 **Sorgen Sie dafür, dass die Configuration Manager-Computerclients eine autorisierte Kopie dieser Zertifikate erhalten:**  

-   Der vertrauenswürdige Configuration Manager-Stammschlüssel  

     Wenn Sie das Active Directory-Schema für Configuration Manager nicht erweitert haben und bei der Clientkommunikation mit Verwaltungspunkten keine PKI-Zertifikate verwendet werden, werden gültige Verwaltungspunkte anhand des vertrauenswürdigen Configuration Manager-Stammschlüssels authentifiziert. In diesem Fall kann nur mit dem vertrauenswürdigen Stammschlüssel festgestellt werden, ob ein Verwaltungspunkt in der Hierarchie als vertrauenswürdig eingestuft ist. Ohne den vertrauenswürdigen Stammschlüssel könnten Clients von einem geschickten Angreifer an einen nicht autorisierten Verwaltungspunkt weitergeleitet werden.  

     Wenn der vertrauenswürdige Configuration Manager-Stammschlüssel nicht aus dem globalen Katalog oder mithilfe von PKI-Zertifikaten heruntergeladen werden kann, stellen Sie den vertrauenswürdigen Stammschlüssel vorab bereit, damit Clients nicht an einen nicht autorisierten Verwaltungspunkt weitergeleitet werden können. Weitere Informationen finden Sie unter [Planning for the Trusted Root Key](../../../../core/plan-design/security/plan-for-security.md#BKMK_PlanningForRTK).  

-   Signaturzertifikat des Standortservers  

     Mit dem Signaturzertifikat des Standortservers wird von Clients geprüft, ob die von einem Verwaltungspunkt heruntergeladene Clientrichtlinie vom Standortserver signiert wurde. Dieses Zertifikat ist ein selbstsigniertes Zertifikat des Standortservers und wird in den Active Directory-Domänendiensten veröffentlicht.  

     Wenn das Signaturzertifikat des Standortservers nicht aus dem globalen Katalog heruntergeladen werden kann, wird es standardmäßig vom Verwaltungspunkt heruntergeladen. Wenn der Verwaltungspunkt in einem nicht vertrauenswürdigen Netzwerk (z. B. im Internet) verfügbar ist, installieren Sie das Signaturzertifikat des Standortservers manuell auf Clients. Damit stellen Sie sicher, dass keine Clientrichtlinien ausgeführt werden, die von einem gefährdeten Verwaltungspunkt stammen und manipuliert sind.  

     Verwenden Sie in CCMSetup die **client.msi**-Eigenschaft SMSSIGNCERT, um das Signaturzertifikat des Standortservers manuell zu installieren. Weitere Informationen finden Sie unter [Informationen zu Clientinstallationseigenschaften in System Center Configuration Manager](../../../../core/clients/deploy/about-client-installation-properties.md).  

 **Verwenden Sie die automatische Standortzuweisung nicht, wenn der vertrauenswürdige Stammschlüssel vom ersten Verwaltungspunkt heruntergeladen wird, mit dem der Client eine Verbindung herstellt.**  

 Diese bewährte Sicherheitsmethode ist mit dem vorherigen Eintrag verknüpft. Verwenden Sie die automatische Standortzuweisung nur in folgenden Szenarien, um dem Risiko vorzubeugen, dass der vertrauenswürdige Stammschlüssel durch den Client von einem nicht autorisierten Verwaltungspunkt heruntergeladen wird:  

-   Der Client kann auf Configuration Manager-Standortinformationen zugreifen, die in Active Directory Domain Services veröffentlicht sind.  

-   Sie stellen den vertrauenswürdigen Stammschlüssel für den Client im Voraus bereit.  

-   Sie verwenden PKI-Zertifikate von einer Unternehmenszertifizierungsstelle, um eine Vertrauensstellung zwischen Client und Verwaltungspunkt herzustellen.  

 Weitere Informationen zum vertrauenswürdigen Stammschlüssel finden Sie unter [Planning for the Trusted Root Key](../../../../core/plan-design/security/plan-for-security.md#BKMK_PlanningForRTK).  

 **Installieren Sie Clientcomputer mit der Client.msi-Option SMSDIRECTORYLOOKUP=NoWINS für CCMSetup.**  

 Die sicherste Dienstidentifizierungsmethode zur Suche nach Standorten und Verwaltungspunkten ist die Verwendung der Active Directory-Domänendienste. Ist dies nicht möglich, beispielsweise weil Sie das Active Directory-Schema für Configuration Manager nicht erweitern können oder weil Clients sich in einer nicht vertrauenswürdigen Gesamtstruktur oder in einer Arbeitsgruppe befinden, können Sie als Alternative die DNS-Veröffentlichung verwenden. Ist keine dieser Methoden erfolgreich, ist ein Ausweichen auf WINS möglich, wenn der Verwaltungspunkt nicht für HTTPS-Clientverbindungen konfiguriert ist.  

 Da die Veröffentlichung auf WINS weniger sicher als die anderen Veröffentlichungsmethoden ist, legen Sie durch Angabe von SMSDIRECTORYLOOKUP=NoWINS fest, dass WINS von Clientcomputern nicht als Alternative verwendet werden soll. Falls Sie WINS für die Dienstidentifizierung benötigen, verwenden Sie die Standardeinstellung SMSDIRECTORYLOOKUP=WINSSECURE. Bei dieser Einstellung wird das selbstsignierte Zertifikat des Verwaltungspunkts anhand des vertrauenswürdigen Configuration Manager-Stammschlüssels überprüft.  

> [!NOTE]  
>  Wenn der Client für SMSDIRECTORYLOOKUP=WINSSECURE konfiguriert ist und über WINS ein Verwaltungspunkt gefunden wird, wird die Clientkopie des vertrauenswürdigen Configuration Manager-Stammschlüssels in WMI überprüft. Wenn die Signatur des Verwaltungspunktzertifikats mit der Clientkopie des vertrauenswürdigen Stammschlüssels übereinstimmt, ist das Zertifikat gültig. Vom Client wird dann eine Verbindung mit dem über WINS gefundenen Verwaltungspunkt hergestellt. Wenn die Signatur des Verwaltungspunktzertifikats nicht mit der Clientkopie des vertrauenswürdigen Stammschlüssels übereinstimmt, ist das Zertifikat ungültig. Vom Client wird dann keine Verbindung mit dem über WINS gefundenen Verwaltungspunkt hergestellt.  

 **Achten Sie darauf, dass die Wartungsfenster für die Bereitstellung wichtiger Softwareupdates groß genug sind.**  

 Durch Wartungsfenster für Gerätesammlungen können Sie festlegen, dass Software nur zu bestimmten Zeiten von Configuration Manager auf diesen Geräten installiert werden kann. Wenn das Wartungsfenster zu klein ist, können wichtige Softwareupdates möglicherweise nicht vom Client installiert werden. Dies erhöht das Risiko eines Angriffs, der von diesem Softwareupdate verhindert würde.  

 **Treffen Sie für Windows Embedded-Geräte mit Schreibfiltern zusätzliche Sicherheitsvorkehrungen, um die Angriffsfläche zu verringern, wenn die Schreibfilter von Configuration Manager deaktiviert werden, um Softwareinstallationen und -änderungen beizubehalten.**  

 Wenn auf Windows Embedded-Geräten Schreibfilter aktiviert sind, dann werden Softwareinstallationen oder -änderungen nur im Overlay durchgeführt und werden nach einem Geräteneustart nicht beibehalten. Wenn Sie mithilfe von Configuration Manager die Schreibfilter für die Beibehaltung von Softwareinstallationen und -änderungen temporär deaktivieren, dann ist das Embedded-Gerät während dieses Zeitraums nicht geschützt gegen Änderungen an allen Datenträgern, inklusive der freigegebenen Ordner.  

 Obwohl der Computer in diesem Zeitraum von Configuration Manager gesperrt wird, sodass sich nur der lokale Administrator anmelden kann, sollten Sie so oft wie möglich zusätzliche Sicherheitsvorkehrungen treffen, um den Computer besser zu schützen. Aktivieren Sie beispielsweise zusätzliche Beschränkungen auf der Firewall und trennen Sie die Netzwerkverbindung des Geräts.  

 Wenn Sie Wartungsfenster verwenden, um Änderungen beizubehalten, sollten Sie diese Fenster sorgfältig einplanen, um die Zeit mit deaktivierten Schreibfiltern zu minimieren und gleichzeitig genug Zeit für die Fertigstellung von Softwareinstallationen und Neustarts zu veranschlagen.  

 **Falls Sie eine softwareupdatebasierte Clientinstallation verwenden und eine spätere Version des Clients am Standort installieren, führen Sie für das am Softwareupdatepunkt veröffentlichte Softwareupdate ein Update aus, damit die Clients die neueste Version erhalten.**  

 Falls Sie eine spätere Version des Clients am Standort installieren, beispielsweise im Rahmen eines Standortupgrades, wird für das am Softwareupdatepunkt veröffentlichte Softwareupdate für die Clientbereitstellung nicht automatisch ein Update ausgeführt. Sie müssen den Configuration Manager-Client erneut am Softwareupdatepunkt veröffentlichen und zum Aktualisieren der Versionsnummer auf **Ja** klicken.  

 Weitere Informationen finden Sie im Verfahren „So veröffentlichen Sie den Configuration Manager-Client auf dem Softwareupdatepunkt“ unter [Installieren von Configuration Manager-Clients mithilfe von auf Softwareupdate basierender Installation](../../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientSUP).  

 **Verwenden Sie die Option „Immer“ für die Einstellung „Bitlocker-PIN-Eingabe bei Neustart anhalten“ des Computer-Agent-Clientgeräts nur bei Computern, die Sie als vertrauenswürdig einstufen und auf die der physische Zugriff beschränkt ist.**  

 Wenn Sie diese Clienteinstellung auf **Immer** festlegen, kann die Softwareinstallation von Configuration Manager abgeschlossen werden. Damit sorgen Sie dafür, dass kritische Softwareupdates installiert und Dienste fortgesetzt werden. Wenn aber der Neustart von einem Angreifer abgefangen wird, könnte dieser den Computer unter seine Kontrolle bringen. Verwenden Sie diese Einstellung nur, wenn Sie den Computer als vertrauenswürdig einstufen und wenn der physische Zugriff auf den Computer beschränkt ist. Beispielsweise eignet diese Einstellung sich möglicherweise für Server in einem Rechenzentrum.  

 **Wählen Sie auf keinen Fall die Option „Umgehung“ für die Einstellung „PowerShell-Ausführungsrichtlinie“ des Computer-Agent-Clientgeräts aus.**  

 Bei dieser Clienteinstellung können nicht signierte PowerShell-Skripts vom Configuration Manager-Client ausgeführt werden. Dabei könnte Malware auf Clientcomputern ausgeführt werden. Falls Sie diese Option auswählen müssen, verwenden Sie eine benutzerdefinierte Clienteinstellung, und weisen Sie diese nur den Clientcomputern zu, die nicht signierte PowerShell-Skripts ausführen müssen.  

##  <a name="bkmk_mobile"></a> Bewährte Sicherheitsmethoden für mobile Geräte  
 **Für mobile Geräte, die Sie mit Configuration Manager registrieren und die im Internet unterstützt werden: Installieren Sie den Anmeldungsproxypunkt in einem Umkreisnetzwerk und den Anmeldungspunkt im Intranet.**  

 Diese Rollentrennung trägt zum Schutz des Anmeldungspunkts vor Angriffen bei. Wenn der Anmeldungspunkt gefährdet ist, könnte ein Angreifer Authentifizierungszertifikate abrufen und die Anmeldeinformationen von Benutzern stehlen, die ihre mobilen Geräte anmelden.  

 **Für mobile Geräte: Schützen Sie mobile Geräte durch geeignete Kennworteinstellungen vor nicht autorisiertem Zugriff.**  

 Für mobile Geräte, die mithilfe von Configuration Manager registriert werden: Legen Sie mit einem Konfigurationselement für mobile Geräte fest, dass die Kennwortkomplexität „PIN“ lauten und die minimale Kennwortlänge mindestens der Standardlänge entsprechen soll.  

 Für mobile Geräte, auf denen kein Configuration Manager-Client installiert ist, die aber vom Exchange Server-Connector verwaltet werden: Geben Sie in den **Kennworteinstellungen** für den Exchange Server-Connector an, dass die Kennwortkomplexität „PIN“ lauten und die minimale Kennwortlänge mindestens der Standardlänge entsprechen soll.  

 **Für mobile Geräte: Verhindern Sie die Manipulation von Inventur- und Statusinformationen, indem Sie die Ausführung von Anwendungen nur gestatten, wenn diese von vertrauenswürdigen Unternehmen stammen, und indem Sie die Installation nicht signierter Dateien nicht zulassen.**  

 Für weitere mobile Geräte, die mithilfe von Configuration Manager angemeldet werden: Wählen Sie mit einem Konfigurationselement für mobile Geräte unter **Nicht signierte Anwendungen** die Sicherheitseinstellung **Nicht zulässig** aus, und legen Sie die **Installation nicht signierter Dateien** auf eine vertrauenswürdige Quelle fest.  

 Für mobile Geräte, auf denen kein Configuration Manager-Client installiert ist, die aber vom Exchange Server-Connector verwaltet werden: Konfigurieren Sie in den **Anwendungseinstellungen** für den Exchange Server-Connector die Optionen **Installation nicht signierter Dateien** und **Nicht signierte Anwendungen** als **Nicht zulässig**.  

 **Für mobile Geräte: Verhindern Sie Angriffe durch Rechteerweiterungen, indem Sie das mobile Gerät sperren, wenn es nicht in Gebrauch ist.**  

 Für weitere mobile Geräte, die mithilfe von Configuration Manager angemeldet werden: Konfigurieren Sie die Kennworteinstellung **Leerlaufzeit in Minuten vor dem Sperren des mobilen Geräts** mit einem Konfigurationselement für mobile Geräte.  

 Für mobile Geräte, auf denen kein Configuration Manager-Client installiert ist, die aber vom Exchange Server-Connector verwaltet werden: Konfigurieren Sie die **Kennworteinstellungen** des Exchange Server-Connectors, um die **Leerlaufzeit in Minuten vor dem Sperren des mobilen Geräts** zu konfigurieren.  

 **Für mobile Geräte: Verhindern Sie Rechteerweiterungen, indem Sie einschränken, welche Benutzer ihre mobilen Geräte registrieren dürfen.**  

 Verwenden Sie eine benutzerdefinierte Clienteinstellung anstelle von Standardclienteinstellungen, um nur autorisierten Benutzern das Anmelden ihrer mobilen Geräte zu gestatten.  

 **Für mobile Geräte: Stellen Sie in den folgenden Szenarios keine Anwendungen für Benutzer bereit, die mobile Geräte über Configuration Manager oder Microsoft Intune registriert haben:**  

-   Wenn das mobile Gerät von mehreren Personen verwendet wird.  

-   Wenn das Gerät von einem Administrator im Namen eines Benutzers angemeldet wird.  

-   Wenn das Gerät ohne vorherige Ab- und erneute Anmeldung an eine andere Person übertragen wird.  

 Bei der Anmeldung wird eine Beziehung der Affinitäten zwischen Benutzern und Geräten hergestellt, die den Benutzer zuweist, der die Anmeldung am mobilen Gerät vornimmt. Wenn ein anderer Benutzer das mobile Gerät verwendet, kann er die Anwendungen ausführen, die Sie für den ursprünglichen Benutzer bereitgestellt haben, was zu einer Rechteerweiterung führen kann. Ebenso gilt: wenn ein Administrator das mobile Gerät für einen Benutzer anmeldet, werden die für den Benutzer bereitgestellten Anwendungen nicht auf dem mobilen Gerät bereitgestellt, sondern stattdessen Anwendungen, die für den Administrator bereitgestellt sind.  

 Abweichend von der Affinität zwischen Benutzer und Gerät für Windows-Computer können Sie die Informationen zur Affinität zwischen Benutzer und Gerät nicht für mobile Geräte definieren, die von Microsoft Intune registriert werden.  

 Beim Übertragen der Eigentumsrechte eines mobilen Geräts, das von Intune registriert wird, melden Sie das mobile Gerät von Intune ab, um die Affinität zwischen Benutzer und Gerät zu entfernen, und fordern Sie den aktuellen Benutzer auf, das Gerät erneut zu registrieren.  

 **Für mobile Geräte: Stellen Sie sicher, dass Benutzer ihre eigenen mobilen Geräte für Microsoft Intune registrieren.**  

 Da bei der Anmeldung eine Beziehung der Affinität zwischen Benutzer und Gerät hergestellt wird, welche den Benutzer zuweist, der die Anmeldung des mobilen Geräts vornimmt, gilt bei einer Anmeldung eines mobilen Geräts für einen Benutzer durch den Administrator Folgendes: Die für den Benutzer bereitgestellten Anwendungen werden nicht auf dem mobilen Gerät installiert, stattdessen werden möglicherweise die für den Administrator bereitgestellten Anwendungen installiert.  

 **Für Exchange Server-Connector: Achten Sie darauf, dass die Verbindung zwischen dem Configuration Manager-Standortserver und dem Exchange Server-Computer geschützt ist.**  

 Verwenden Sie IPsec, wenn der Exchange Server lokal gehostet ist. Bei gehostetem Exchange wird die Verbindung automatisch mithilfe von SSL gesichert.  

 **Für Exchange Server-Connector: Verfahren Sie nach dem Prinzip der geringsten Berechtigungen für den Connector.**  

 Eine Liste der mindestens erforderlichen Cmdlets für den Exchange Server-Connector finden Sie unter [Verwalten von mobilen Geräten mit System Center Configuration Manager und Exchange](../../../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md).  

##  <a name="bkmk_macs"></a> Bewährte Sicherheitsmethoden für Macs  
 **Für Macintosh-Computer: Verwenden Sie zum Speichern und Zugreifen auf die Clientquelldateien einen sicheren Speicherort.**  

 Vor der Installation oder Registrierung des Clients auf einem Macintosh-Computer werden die Clientquelldateien von Configuration Manager nicht auf eine mögliche Manipulation hin überprüft. Laden Sie diese Dateien aus einer vertrauenswürdigen Quelle herunter, und verwenden Sie einen sicheren Ort zum Speichern und für den Zugriff darauf.  

 **Für Macintosh-Computer: Überwachen und verfolgen Sie die Gültigkeitsdauer des Zertifikats, das bei Benutzern registriert ist, unabhängig von Configuration Manager.**  

 Überwachen und verfolgen Sie den Gültigkeitszeitraum der Zertifikate, die Sie für Macintosh-Computer verwenden, um eine Geschäftskontinuität sicherzustellen. Configuration Manager unterstützt die automatische Erneuerung dieses Zertifikats nicht bzw. gibt keine Warnung aus, wenn das Zertifikat abzulaufen droht. Eine typische Gültigkeitsdauer beträgt 1 Jahr.  

 Weitere Informationen zur Erneuerung des Zertifikats finden Sie unter  [Renewing the Mac Client Certificate Manually](../../../../core/clients/deploy/deploy-clients-to-macs.md#renewing-the-mac-client-certificate).  

 **Für Macintosh-Computer: Ziehen Sie zum Schutz vor einer Rechteerweiterung in Betracht, das Zertifikat einer vertrauenswürdigen Stammzertifizierungsstelle zu konfigurieren, das ausschließlich auf das SSL-Protokoll festgelegt ist.**  

 Verwenden Sie beim Registrieren von Macintosh-Computern in Kombination mit dem vertrauenswürdigen Stammzertifikat ein Benutzerzertifikat, das mit dem Stammzertifikat verbunden ist und zum Verwalten der automatischen Installation des Configuration Manager-Clients dient. Wenn Sie die Vertrauenswürdigkeit dieses Stammzertifikats ausschließlich auf das SSL-Protokoll beschränken wollen, können Sie wie folgt vorgehen.  

 Nach der Durchführung dieses Verfahrens gilt das Stammzertifikat als nicht ausreichend vertrauenswürdig für die Überprüfung anderer Protokolle als SSL – wie etwa Secure Mail (S/MIME), Extensible Authentication (EAP) oder Codesignatur.  

> [!NOTE]  
>  Sie können dieses Verfahren auch verwenden, wenn Sie das Clientzertifikat unabhängig von Configuration Manager installiert haben.  

 So beschränken Sie das Stammzertifizierungsstellen-Zertifikat allein auf das SSL-Protokoll:  

1.  Öffnen Sie auf dem Macintosh-Computer ein Terminal-Fenster.  

2.  Geben Sie den Befehl **sudo /Applications/Utilities/Keychain\ Access.app/Contents/MacOS/Keychain\ Access**ein.  

3.  Klicken Sie im Dialogfeld **Schlüsselbundverwaltung** im Abschnitt **Schlüsselbunde** auf **System**und anschließend im Abschnitt **Kategorie** auf **Zertifikate**.  

4.  Suchen Sie nach dem Zertifikat der Stammzertifizierungsstelle für das Zertifikat des Macintosh-Clients, und doppelklicken Sie darauf.  

5.  Erweitern Sie im Dialogfeld des Stammzertifikats den Abschnitt **Vertrauensstellung** , und nehmen Sie dann die folgenden Änderungen vor:  

    1.  Ändern Sie die Option **Bei Verwendung dieses Zertifikats** von der Standardeinstellung **Immer vertrauen** in **Systemstandardwerte verwenden**.  

    2.  Ändern Sie die Option **SSL (Secure Sockets Layer)** von der Einstellung **Kein Wert angegeben** in **Immer vertrauen**.  

6.  Schließen Sie das Dialogfeld, geben Sie bei entsprechender Aufforderung das Administratorkennwort ein, und klicken Sie dann auf **Einstellungen aktualisieren**.  

##  <a name="BKMK_SecurityIssues_Clients"></a> Sicherheitsprobleme bei Configuration Manager-Clients  
 Für die folgenden Sicherheitsprobleme ist keine Risikominderung vorhanden:  

-   Statusmeldungen werden nicht authentifiziert.  

     Für Statusmeldungen wird keine Authentifizierung ausgeführt. Wenn von einem Verwaltungspunkt HTTP-Clientverbindungen akzeptiert werden, können Statusmeldungen von beliebigen Geräten an den Verwaltungspunkt gesendet werden. Werden dagegen nur HTTPS-Clientverbindungen akzeptiert, muss für ein Gerät ein gültiges Clientauthentifizierungszertifikat von einer vertrauenswürdigen Zertifizierungsstelle vorliegen. Jedoch können auch dann beliebige Statusmeldungen gesendet werden. Wenn der Client eine ungültige Statusmeldung sendet, wird diese verworfen.  

     Dieses Sicherheitsrisiko kann von manchen Angriffen ausgenutzt werden. Angreifer könnten z. B. eine gefälschte Statusmeldung senden, um Mitglied einer Sammlung zu werden, die auf Statusmeldungsabfragen basiert. Jeder Client könnte einen Denial-of-Service-Angriff auf den Verwaltungspunkt ausführen, in dem er mit Statusmeldungen überflutet wird. Wenn Statusmeldungen Aktionen in der Filterregel für Statusmeldungen auslösen, könnten Angreifer die Filterregel für Statusmeldungen auslösen. Angreifer könnten außerdem eine Statusmeldung senden, die dazu führt, dass Berichtsinformationen falsch angegeben werden.  

-   Richtlinien können auf Clients umgeleitet werden, für die sie nicht bestimmt sind.  

     Angreifer verfügen über verschiedene Methoden, um eine Richtlinie auf einen anderen als den gewünschten Client anzuwenden. Beispielsweise könnte ein Angreifer von einem vertrauenswürdigen Client falsche Inventur- oder Ermittlungsinformationen senden, damit der Computer einer falschen Sammlung hinzugefügt wird, und somit alle Bereitstellungen für diese Sammlung empfangen. Es bestehen zwar Kontrollen, die verhindern, dass Angreifer Richtlinien direkt ändern. Angreifer könnten jedoch eine vorhandene Richtlinie dazu verwenden, das Betriebssystem neu zu formatieren und neu bereitzustellen, und dieses an einen anderen Computer senden, was zu einem Denial-of-Service-Angriff führt. Diese Angriffsmethoden erfordern einen genauen Zeitplan und umfassende Kenntnisse der Configuration Manager-Infrastruktur.  

-   Benutzer können auf Clientprotokolle zugreifen.  

     Für alle Clientprotokolldateien sind Benutzerlesezugriff und interaktiver Benutzerschreibzugriff zulässig. Wenn Sie die ausführliche Protokollierung aktivieren, können Angreifer die Protokolldateien anzeigen und so nach Informationen zur Kompatibilität oder Sicherheitsrisiken des Systems suchen. Prozesse, die im Kontext eines Benutzers ausgeführt werden, wie z. B. die Softwareinstallation, müssen mit einem Benutzerkonto mit geringen Rechten in Protokolle schreiben können. Dies ermöglicht es auch Angreifern, mit einem Konto mit geringsten Rechten in die Protokolle zu schreiben.  

     Das schwerwiegendste Risiko besteht darin, dass ein Angreifer aus den Protokolldateien Informationen entfernen könnte, die der Administrator für die Überwachung und Angriffserkennung benötigt.  

-   Mithilfe eines Computers können Zertifikate abgerufen werden, die für die Anmeldung mobiler Geräte bestimmt sind.  

     Beim Verarbeiten einer Registrierungsanforderung in Configuration Manager kann nicht überprüft werden, ob die Anforderung von einem mobilen Gerät oder von einem Computer übermittelt wurde. Wurde die Anforderung von einem Computer übermittelt, kann auf diesem ein PKI-Zertifikat installiert werden, das die Registrierung mit Configuration Manager ermöglicht. Verhindern Sie Angriffe durch Rechteerweiterungen in solchen Szenarien, indem Sie nur vertrauenswürdigen Benutzern die Anmeldung ihrer mobilen Geräte gestatten und Anmeldungsaktivitäten aufmerksam überwachen.  

-   Die Verbindung von einem Client zu einem Verwaltungspunkt wird nicht unterbrochen, wenn Sie einen Client blockieren, und vom blockierten Client können weiterhin Benachrichtigungspakete als Keep Alive-Meldungen an den Verwaltungspunkt geschickt werden.  

     Wenn Sie einen Client blockieren, dem Sie nicht mehr vertrauen und der eine Clientbenachrichtigungskommunikation hergestellt hat, dann wird die Sitzung nicht von Configuration Manager unterbrochen. Vom blockierten Client können weiterhin Pakete an dessen Verwaltungspunkt geschickt werden, bis die Verbindung zum Netzwerk vom Client getrennt wird. Diese Pakete sind lediglich kleine Keep Alive-Pakete, und diese Clients können nicht von Configuration Manager verwaltet werden, bevor die Blockierung aufgehoben wird.  

-   Wenn Sie ein automatisches Clientupgrade verwenden und der Client zu einem Verwaltungspunkt gesteuert wird, um die Clientquelldateien herunterzuladen, dann wird der Verwaltungspunkt nicht als vertrauenswürdige Quelle bestätigt.  

-   Wenn Benutzer ihre Macintosh-Computer zum ersten Mal anmelden, sind diese durch DNS-Spoofing gefährdet.  

     Wird während der Anmeldung die Verbindung vom Macintosh-Computer zum Anmeldungsproxypunkt hergestellt, verfügt der Macintosh-Computer wahrscheinlich noch nicht über ein Stammzertifikat. Zu diesem Zeitpunkt besteht keine Vertrauensbeziehung zwischen dem Server und dem Macintosh-Computer, und der Benutzer wird zum Fortfahren aufgefordert. Falls der vollständig qualifizierte Name des Anmeldungsproxypunkt durch einen nicht autorisierten DNS-Server aufgelöst wird, könnte der Macintosh-Computer an einen nicht autorisierten Anmeldungsproxypunkt verwiesen werden und Zertifikate von einer nicht vertrauenswürdigen Quelle installieren. Zur Minderung dieses Risikos sollten Sie die bewährten Methoden im Hinblick auf die Verhinderung von DNS-Spoofing in Ihrer Umgebung befolgen.  

-   Durch die Anmeldung von Macintosh-Computern werden Zertifikatanforderungen nicht eingeschränkt  

     Benutzer können ihre Macintosh-Computer erneut registrieren und dabei jedes Mal ein neues Clientzertifikat anfordern. Configuration Manager führt keine Überprüfung auf mehrere Anforderungen durch bzw. beschränkt nicht die Anzahl der Zertifikate, die von einem einzelnen Computer angefordert werden. Ein nicht autorisierter Benutzer können ein Skript ausführen, das die Befehlszeile der Anmeldeanforderung wiederholt, und dadurch einen DoS-Zustand (Denial-of-Service) im Netzwerk oder der ausstellenden Zertifizierungsstelle verursachen. Zur Minderung dieses Risikos sollten Sie die ausstellende Zertifizierungsstelle sorgfältig überwachen, um derartiges verdächtiges Verhalten zu erkennen. Ein Computer, auf dem sich diese Art von Verhalten zeigt, sollte umgehend aus der Configuration Manager-Hierarchie ausgesperrt werden.  

-   Eine Zurücksetzbestätigung ist kein Nachweis dafür, dass das Gerät erfolgreich zurückgesetzt wurde  

     Wenn Sie eine Zurücksetzung für ein mobiles Gerät initiieren und der Zurücksetzungsstatus in Configuration Manager als bestätigt angezeigt wird, wird durch diese Bestätigung belegt, dass die Zurücksetzungsmeldung erfolgreich von Configuration Manager an das mobile Gerät gesendet wurde, und nicht, dass der Auftrag vom Gerät ausgeführt wurde. Bei mobilen Geräten, die durch den Exchange Server-Connector verwaltet werden, wird außerdem durch eine Zurücksetzungsbestätigung belegt, dass der Befehl bei Exchange eingegangen ist, nicht auf dem Gerät.  

-   Wenn Sie die Optionen für das Ausführen von Änderungen auf Windows Embedded-Geräten verwenden, werden Konten möglicherweise früher als erwartet gesperrt.  

     Wenn auf dem Windows Embedded-Gerät ein Betriebssystem vor Windows 7 ausgeführt wird und ein Benutzer versucht, sich anzumelden, während die Schreibfilter deaktiviert sind, um von Configuration Manager vorgenommene Änderungen zu übertragen, dann wird die Anzahl der zulässigen fehlerhaften Anmeldeversuche vor Sperrung des Kontos halbiert. Wenn der **Kontosperrungsschwellenwert** beispielsweise als 6 konfiguriert ist und ein Benutzer das Kennwort dreimal falsch eingibt, wird das Konto gesperrt, was zu einer Dienstverweigerungssituation führt.  Wenn sich Benutzer in diesem Szenario an Embedded-Geräten anmelden müssen, informieren Sie sie über die Möglichkeit eines reduzierten Sperrschwellenwerts.  

##  <a name="BKMK_Privacy_Cliients"></a> Informationen zum Datenschutz für Configuration Manager-Clients  
 Wenn Sie den Configuration Manager-Client bereitstellen, aktivieren Sie Clienteinstellungen, um Configuration Manager-Verwaltungsfeatures verwenden zu können. Die für die Konfiguration der Features verwendeten Einstellungen können für alle Clients in der Configuration Manager-Hierarchie unabhängig davon gelten, ob sie direkt mit dem Unternehmensnetzwerk, über eine Remotesitzung oder mit dem Internet verbunden sind, aber von Configuration Manager unterstützt werden.  

 Clientinformationen werden in der Configuration Manager-Datenbank gespeichert und nicht an Microsoft gesendet. Die Informationen bleiben bis zum Löschen durch den Standortwartungstask **Veraltete Ermittlungsdaten löschen** in der Datenbank gespeichert. Der Löschvorgang wird alle 90 Tage ausgeführt. Sie können das Löschintervall konfigurieren.  

 Berücksichtigen Sie beim Konfigurieren des Configuration Manager-Clients Ihre Datenschutzanforderungen.  

### <a name="privacy-information-for-mobile-devices-that-are-enrolled-by-configuration-manager"></a>Datenschutzinformationen für mobile Geräte, die mithilfe von Configuration Manager angemeldet werden  
 Datenschutzinformationen im Zusammenhang mit der Registrierung mobiler Geräte mithilfe von Configuration Manager finden Sie unter [Datenschutzbestimmungen für System Center Configuration Manager – Nachtrag für mobile Geräte](../../../../core/misc/privacy/privacy-statement-mobile-device-addendum.md).  

### <a name="client-status"></a>Clientstatus  
 Configuration Manager überwacht die Aktivitäten von Clients, wertet den Configuration Manager-Client und seine Abhängigkeiten regelmäßig aus und kann bei Bedarf Probleme beheben. Der Clientstatus ist standardmäßig aktiviert, wobei serverseitige Metriken zur Überprüfung der Clientaktivitäten verwendet werden sowie clientseitige Aktionen für Selbstprüfungen, Wiederherstellungen und zum Übermitteln von Clientstatusinformationen an den Configuration Manager-Standort. Vom Client werden die Selbstprüfungen gemäß einem von Ihnen konfigurierten Zeitplan ausgeführt. Die Ergebnisse der Überprüfungen werden an den Configuration Manager-Standort übermittelt. Diese Informationen werden während der Übertragung verschlüsselt.  

 Clientstatusinformationen werden in der Configuration Manager-Datenbank gespeichert und nicht an Microsoft gesendet. In der Standortdatenbank werden die Informationen unverschlüsselt gespeichert. Diese Informationen bleiben bis zum Löschen gemäß dem für die Clientstatuseinstellung **Clientstatusverlauf für die folgende Anzahl von Tagen beibehalten** konfigurierten Wert in der Datenbank gespeichert. Der Standardwert für diese Einstellung ist 31 Tage.  

 Berücksichtigen Sie beim Installieren des Configuration Manager-Clients mit Überprüfung des Clientstatus Ihre Datenschutzanforderungen.  

##  <a name="BKMK_Privacy_ExchangeConnector"></a> Informationen zum Datenschutz für vom Exchange Server-Connector verwaltete mobile Geräte  
 Geräte, die über das ActiveSync-Protokoll mit Exchange Server verbunden sind (lokal oder gehostet), werden vom Exchange Server-Connector ermittelt und verwaltet. Die vom Exchange Server-Connector ermittelten Datensätze werden in der Configuration Manager-Datenbank gespeichert. Die Informationen werden von Exchange Server gesammelt. Dabei werden über die von den mobilen Geräten an Exchange Server übermittelten Daten hinaus keine weiteren Informationen erfasst.  

 Die Informationen zu den mobilen Geräten werden nicht an Microsoft gesendet. Anschließend werden die Informationen zu den mobilen Geräten in der Configuration Manager-Datenbank gespeichert. Die Informationen bleiben bis zum Löschen durch den Standortwartungstask **Veraltete Ermittlungsdaten löschen** in der Datenbank gespeichert. Der Löschvorgang wird alle 90 Tage ausgeführt. Sie können das Löschintervall konfigurieren.  

 Berücksichtigen Sie beim Installieren und Konfigurieren des Exchange Server-Connectors Ihre Datenschutzanforderungen.  
