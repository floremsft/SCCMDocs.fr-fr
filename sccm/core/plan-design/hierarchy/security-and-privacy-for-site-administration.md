---
title: "Sicherheit und Datenschutz für die Standortverwaltung | Microsoft-Dokumentation"
description: "Optimieren Sie Sicherheit und Datenschutz für die Standortverwaltung in System Center Configuration Manager."
ms.custom: na
ms.date: 3/1/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1d58176e-abc0-4087-8583-ce70deb4dcf5
caps.latest.revision: "8"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: a60b8c103a303dcae0bd66f3060d5a8f17d1cef9
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="security-and-privacy-for-site-administration-in-system-center-configuration-manager"></a>Sicherheit und Datenschutz für die Standortverwaltung in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Diese Thema enthält Sicherheits- und Datenschutzinformationen für System Center Configuration Manager-Standorte und die Hierarchie.

##  <a name="BKMK_Security_Sites"></a> Bewährte Sicherheitsmethoden für die Standortverwaltung  
 Wenden Sie die folgenden bewährten Sicherheitsmethoden an, um System Center Configuration Manager-Standorte und die Hierarchie zu sichern.  

 **Führen Sie Setup nur von einer vertrauenswürdigen Quelle aus aus, und sichern Sie den Kommunikationskanal zwischen Setupmedien und Standortserver.**  

 Führen Sie Setup nur von einer vertrauenswürdigen Quelle aus aus, um Manipulationen der Quelldateien zu vermeiden. Wenn Sie die Dateien im Netzwerk speichern, Sichern Sie den Speicherort im Netzwerk.  

 Wenn Sie Setup von einem Speicherort im Netzwerk aus ausführen, verwenden Sie IPsec oder Server Message Block (SMB)-Signaturen zwischen dem Quellspeicherort der Setupdateien und dem Standortserver, um Manipulationen an den Dateien während der Übertragung über das Netzwerk zu verhindern.  

 Wenn Sie das Setup-Downloadprogramm zum Herunterladen der für Setup erforderlichen Dateien verwenden, sichern Sie auch den Ort, an dem diese Dateien gespeichert werden, sowie den Kommunikationskanal mit diesem Speicherort, wenn Sie Setup ausführen.  

 **Erweitern Sie das Active Directory-Schema für System Center Configuration Manager, und veröffentlichen Sie die Standorte in Active Directory Domain Services.**  

 Schemaerweiterungen sind zum Ausführen von System Center Configuration Manager nicht erforderlich, jedoch lässt sich die Sicherheit der Umgebung durch sie erhöhen, da so ein Abrufen von Informationen durch Configuration Manager-Clients und Standortserver aus vertrauenswürdigen Quellen ermöglicht wird.  

 Stellen Sie bei Clients in einer nicht vertrauenswürdigen Domäne die folgenden Standortsystemrollen in den Domänen der Clients bereit:  

-   Verwaltungspunkt  

-   Verteilungspunkt  

-   Anwendungskatalog-Websitepunkt  

> [!NOTE]  
>  Eine vertrauenswürdige Domäne für den Configuration Manager erfordert Kerberos-Authentifizierung. Daher werden Clients in einer anderen Gesamtstruktur ohne bidirektionale Vertrauensstellung mit der Gesamtstruktur des Standortservers als Clients in einer nicht vertrauenswürdigen Domäne betrachtet. Eine externe Vertrauensstellung ist für diesen Zweck nicht ausreichend.  

 **Verwenden Sie IPsec zum Sichern der Kommunikation zwischen Standortsystemservern und Standorten.**  

 Die Kommunikation zwischen Standortserver und dem Computer, auf dem SQL Server ausgeführt wird, wird von Configuration Manager gesichert. Die Kommunikation zwischen Standortsystemrollen und SQL Server wird von Configuration Manager jedoch nicht gesichert. Es können nur einige Standortsysteme (Anmeldungspunkt und Anwendungskatalog-Webdienstpunkt) für die Verwendung von HTTPS zur standortinternen Kommunikation konfiguriert werden.  

 Wenn Sie keine zusätzlichen Kontrollmaßnahmen zum Sichern dieser Kanäle zwischen Servern verwenden, können Angreifer verschiedene Spoofing- und Man-in-the-middle-Angriffe gegen Standortsysteme richten. Verwenden Sie SMB-Signaturen, wenn Sie IPsec nicht verwenden können.  

> [!NOTE]  
>  Es ist besonders wichtig, den Kommunikationskanal zwischen Standortserver und dem Quellserver der Pakete zu sichern. Diese Kommunikation erfolgt über SMB. Wenn Sie IPsec nicht verwenden können, um die Kommunikation zu sichern, verwenden Sie SMB-Signaturen, um zu gewährleisten, dass die Dateien nicht manipuliert sind, wenn sie von den Clients heruntergeladen und ausgeführt werden.  

 **Nehmen Sie keine Änderungen an den Sicherheitsgruppen vor, die von Configuration Manager erstellt und zur Kommunikation im Standortsystem verwaltet werden.**  

 Sicherheitsgruppen:  

-   **SMS_SiteSystemToSiteServerConnection_MP_&lt;Standortcode\>**  

-   **SMS_SiteSystemToSiteServerConnection_SMSProv_&lt;Standortcode\>**  

-   **SMS_SiteSystemToSiteServerConnection_Stat_&lt;Standortcode\>**  

Diese Sicherheitsgruppen werden von Configuration Manager automatisch erstellt und verwaltet. Hierin ist das Entfernen von Computerkonten, wenn eine Standortsystemrolle entfernt wird, eingeschlossen.  

Bearbeiten Sie diese Gruppen nicht manuell, um die Dienstkontinuität und das Prinzip der geringsten Berechtigungen nicht zu gefährden.  

**Wenn eine Abfrage von Configuration Manager-Informationen vom globalen Katalogserver durch die Clients nicht möglich ist, verwalten Sie den Bereitstellungsprozess des vertrauenswürdigen Stammschlüssels.**  

Wenn eine Abfrage von Configuration Manager-Informationen vom globalen Katalog durch die Clients nicht möglich ist, ist der vertrauenswürdige Stammschlüssel zur Authentifizierung gültiger Verwaltungspunkte erforderlich. Der vertrauenswürdige Stammschlüssel wird in der Clientregistrierung gespeichert und kann mithilfe der Gruppenrichtlinie oder manuell konfiguriert werden.  

Wenn der Client beim ersten Kontakt mit einem Verwaltungspunkt keine Kopie des vertrauenswürdigen Stammschlüssels aufweist, wird dem ersten Verwaltungspunkt vertraut, mit dem kommuniziert wird. Sie können für den Client im Voraus einen vertrauenswürdigen Stammschlüssel bereitstellen, um das Risiko zu reduzieren, dass Clients von einem Angreifer an einen nicht autorisierten Verwaltungspunkt umgeleitet werden. Weitere Informationen finden Sie unter [Planning for the trusted root key (Planen des vertrauenswürdigen Stammschlüssels)](../../../core/plan-design/security/plan-for-security.md#BKMK_PlanningForRTK).  

**Verwenden Sie nicht die Standardportnummern.**  

Aus Sicherheitsgründen sollten Sie Portnummern verwenden, die nicht der Standardeinstellung entsprechen. Dadurch wird Angreifern die Erkundung der Umgebung zur Vorbereitung eines Angriffs erschwert. Wenn Sie sich für die Verwendung von Portnummern entscheiden, die nicht der Standardeinstellung entsprechen, planen Sie diese Nummern, bevor Sie Configuration Manager installieren, und verwenden Sie diese Nummern konsistent in allen Standorten der Hierarchie. Portnummern, die nicht der Standardeinstellung entsprechen, können Sie beispielsweise als Clientanforderungsports und für Wake-On-LAN verwenden.  

**Verwenden Sie die Rollentrennung für Standortsysteme.**  

Sie können zwar sämtliche Standortsystemrollen auf einem einzigen Computer installieren, doch wird dieses Vorgehen in Produktionsnetzwerken selten verwendet, weil damit ein einziger Fehlerpunkt erstellt wird.  

**Verringern Sie die Angriffsfläche.**  

Wenn Sie jede Standortserverrolle auf einem anderen Server installieren, reduzieren Sie damit das Risiko, dass ein Angriff gegen Schwachstellen in einem Standortsystem auch gegen ein anderes Standortsystem verwendet werden kann. Für viele Standortsystemrollen ist die Installation von Internetinformationsdiensten (IIS) auf dem Standortsystem erforderlich. Dadurch vergrößert sich die Angriffsfläche. Wenn Sie Standortsystemrollen kombinieren müssen, um die Hardwareausgaben zu reduzieren, sollten Sie IIS-Standortsystemrollen nur mit Rollen kombinieren, für die ebenfalls IIS erforderlich sind.  

> [!IMPORTANT]  
>  Für die Fallbackstatuspunkt-Rolle gilt eine Ausnahme. Von dieser Standortsystemrolle werden nicht authentifizierte Daten von Clients akzeptiert, daher sollte die Fallbackstatuspunkt-Rolle niemals einer anderen Configuration Manager-Standortsystemrolle zugewiesen werden.  


**Befolgen Sie die bewährten Sicherheitsmethoden für Windows Server, und führen Sie auf allen Standortsystemen den Sicherheitskonfigurations-Assistenten aus.**  

Mithilfe des Sicherheitskonfigurations-Assistenten können Sie eine Sicherheitsrichtlinie erstellen und auf alle Server im Netzwerk anwenden. Nach der Installation der System Center Configuration Manager-Vorlage erkennt SCW Configuration Manager-Standortsystemrollen, -dienste, -ports und -anwendungen. Danach wird die Kommunikation, die für Configuration Manager erforderlich ist, zugelassen, und die nicht erforderliche Kommunikation wird blockiert.  

Der Sicherheitskonfigurations-Assistent ist im Toolkit für System Center 2012 Configuration Manager enthalten, das Sie im Microsoft Download Center herunterladen können: [System Center 2012 – Add-Ons und Erweiterungen für Configuration Manager-Komponente](http://go.microsoft.com/fwlink/p/?LinkId=251931).  

**Konfigurieren Sie statische IP-Adressen für Standortsysteme.**  

Statische IP-Adressen können leichter vor Namensauflösungsangriffen geschützt werden.  

Statische IP-Adressen erleichtern auch die Konfiguration von IPsec. Die Verwendung von IPsec ist eine bewährte Sicherheitsmethode zur Kommunikationssicherung zwischen Standortsystemen in Configuration Manager.  

**Installieren Sie keine anderen Anwendungen auf Standortsystemservern.**  

Wenn Sie andere Anwendungen auf Standortsystemservern installieren, vergrößern Sie die Angriffsfläche von Configuration Manager und erhöhen das Risiko von Kompatibilitätsproblemen.  

**Fordern Sie Signaturen an, und aktivieren Sie Verschlüsselung als Standortoption.**  

Aktivieren Sie die Signierungs- und Verschlüsselungsoptionen für den Standort. Vergewissern Sie sich, dass der SHA-256-Hashalgorithmus von allen Clients unterstützt wird, und aktivieren Sie dann die Option **SHA-256 erforderlich**.  

**Überwachen Sie Configuration Manager-Administratoren, beschränken Sie ihre Anzahl, und verwenden Sie die rollenbasierte Verwaltung, um diesen Benutzern die minimal erforderlichen Berechtigungen zu erteilen.**  

Gewähren Sie nur vertrauenswürdigen Benutzern administrativen Zugriff auf Configuration Manager, und befolgen Sie das Prinzip der minimal erforderlichen Berechtigungen, indem Sie die integrierten Sicherheitsrollen verwenden oder anpassen. Administratoren, die Anwendungen, Tasksequenzen, Softwareupdates, Konfigurationsobjekte und Konfigurationsbaselines erstellen, ändern und bereitstellen können, können die Geräte in der Configuration Manager-Hierarchie möglicherweise steuern.  

Überwachen Sie kontinuierlich die Administratorzuweisungen und die Autorisierungsebenen, um erforderliche Änderungen zu überprüfen.  

Weitere Informationen zum Konfigurieren der rollenbasierten Verwaltung finden Sie unter [Configure role-based administration for System Center Configuration Manager](../../../core/servers/deploy/configure/configure-role-based-administration.md).  

**Sichern Sie die Configuration Manager-Sicherungen sowie den Kommunikationskanal, wenn Sie Sicherungen und Wiederherstellungen ausführen.**  

Beim Wiederherstellen von Configuration Manager sind Informationen erforderlich, in denen auch Zertifikate und andere sensible Daten enthalten sind. Diese Daten könnten von Angreifern zur Identitätsvortäuschung verwendet werden.  

Verwenden Sie SMB-Signaturen oder IPsec, wenn Sie solche Daten im Netzwerk übertragen, und sichern Sie auch das Sicherungsverzeichnis.  

**Sichern Sie beim Exportieren und Importieren von Objekten zwischen Configuration Manager-Konsole und einem Netzwerkspeicherort den Speicherort und den Netzwerkkanal.**  

Schränken Sie die Anzahl der Personen ein, die auf den Netzwerkordner zugreifen können.  

Verwenden Sie SMB-Signaturen oder IPsec zwischen Netzwerkspeicherort und Standortserver sowie zwischen dem Computer, auf dem die Configuration Manager-Konsole ausgeführt wird, und dem Standortserver, um Manipulationen an den exportierten Daten zu verhindern. Verwenden Sie IPsec zum Verschlüsseln der Daten im Netzwerk, um die Offenlegung von Informationen zu verhindern.  

**Wenn ein Standortsystem nicht richtig deinstalliert wird oder bei Funktionsausfall nicht wiederhergestellt werden kann, entfernen Sie die Configuration Manager-Zertifikate für diesen Server manuell von anderen Configuration Manager-Servern.**  

Zum Entfernen von PeerTrust, das ursprünglich mit dem Standortsystem und den Standortsystemrollen erstellt wurde, entfernen Sie die Configuration Manager-Zertifikate für den ausgefallenen Server im Zertifikatspeicher **Vertrauenswürdige Personen** auf anderen Standortsystemservern manuell. Dies ist besonders dann wichtig, wenn Sie den Server ohne Neuformatieren wiederverwenden.  

Weitere Informationen zu diesen Zertifikaten finden Sie im Abschnitt **Kryptografische Steuerelemente für die Serverkommunikation** unter [Technische Referenz für kryptografische Steuerelemente](../../../protect/deploy-use/cryptographic-controls-technical-reference.md).  

**Konfigurieren Sie internetbasierte Standortsysteme nicht als Brücke zu Umkreisnetzwerk und Intranet.**  

Konfigurieren Sie Standortsystemserver nicht so, dass sie mehrfach vernetzt und sowohl mit dem Umkreisnetzwerk als auch mit dem Intranet verbunden sind. Durch eine solche Konfiguration können von internetbasierten Standortsystemen zwar Clientverbindungen aus dem Internet und dem Intranet angenommen werden, aber es wird eine Sicherheitsgrenze zwischen dem Umkreisnetzwerk und dem Intranet aufgehoben.  

**Wenn sich der Standortsystemserver in einem nicht vertrauenswürdigen Netzwerk (wie einem Umkreisnetzwerk) befindet, konfigurieren Sie den Standortserver für das Initiieren von Verbindungen mit dem Standortsystem.**  

Von den Standortsystemen werden standardmäßig Verbindungen mit dem Standortserver zur Datenübertragung hergestellt. Dies kann ein Sicherheitsrisiko darstellen, wenn die Verbindung von einem nicht vertrauenswürdigen Netzwerk mit dem vertrauenswürdigen Netzwerk hergestellt wird. Wenn von den Standortsystemen Verbindungen aus dem Internet akzeptiert werden oder sich die Standortsysteme in einer nicht vertrauenswürdigen Struktur befinden, konfigurieren Sie die Standortsystemoption **Verbindungen mit diesem Standortsystem müssen vom Standortserver hergestellt werden** , sodass nach der Installation von Standortsystem und Standortsystemrollen alle Verbindungen vom vertrauenswürdigen Netzwerk initiiert werden.  

**Wenn Sie für die internetbasierte Clientverwaltung einen Webproxyserver verwenden, verwenden Sie SSL-zu-SSL-Bridging mit Tunnelabschluss und Authentifizierung.**  

 Wenn Sie den SSL-Tunnelabschluss für den Proxywebserver konfigurieren, werden Pakete aus dem Internet überprüft, bevor sie an das interne Netzwerk weitergeleitet werden. Die vom Client eingehende Verbindung wird vom Proxywebserver authentifiziert und beendet, und dann wird eine neue authentifizierte Verbindung mit dem internetbasierten Standortsystem hergestellt.  

 Wenn von Configuration Manager-Clientcomputern ein Proxywebserver verwendet wird, um eine Verbindung mit internetbasierten Standortsystemen herzustellen, wird die Clientidentität (Client-GUID) sicher als Bestandteil der Paketnutzdaten transportiert, sodass der Proxywebserver vom Verwaltungspunkt nicht als Client angesehen wird. Wenn von Ihrem Proxywebserver die Voraussetzungen für die Unterstützung von SSL-Bridging nicht erfüllt werden, steht Ihnen als weitere Möglichkeit die Verwendung von SSL-Tunneling zur Verfügung. Diese Option ist weniger sicher, da die SSL-Pakete aus dem Internet ohne Tunnelabschluss an die Standortsysteme weitergeleitet werden und daher nicht auf schädlichen Inhalt überprüft werden können.  

 Wenn von Ihrem Proxywebserver die Voraussetzungen für die Unterstützung von SSL-Bridging nicht erfüllt werden, können Sie auch SSL-Tunneling verwenden. Diese Option ist jedoch weniger sicher, da die SSL-Pakete aus dem Internet ohne Tunnelabschluss an die Standortsysteme weitergeleitet werden und daher nicht auf schädlichen Inhalt überprüft werden können.  

> [!WARNING]  
>  SSL-Bridging wird von mobilen Geräten, die mithilfe von Configuration Manager angemeldet wurden, nicht unterstützt, sodass hierbei nur SSL-Tunneling verwendet werden kann.  

**Empfohlene Konfigurationen, wenn Sie den Standort zum Aktivieren von Computern für die Softwareinstallation konfigurieren.**  

-   Wenn Sie herkömmliche Aktivierungspakete verwenden, bevorzugen Sie Unicast gegenüber subnetzgesteuerten Broadcasts.  

-   Wenn subnetzgesteuerte Broadcasts verwendet werden müssen, konfigurieren Sie die Router so, dass IP-gesteuerte Broadcasts nur über den Standortserver und nur über eine nicht standardmäßig konfigurierte Portnummer möglich sind.  

Weitere Informationen zu den verschiedenen Wake-On-LAN-Technologien finden Sie unter [Planning how to wake up clients in System Center Configuration Manager (Planen der Aktivierung von Clients in System Center Configuration Manager)](../../../core/clients/deploy/plan/plan-wake-up-clients.md).

**Wenn Sie E-Mail-Benachrichtigungen verwenden, konfigurieren Sie einen authentifizierten Zugriff auf den SMTP-E-Mail-Server.**  

Verwenden Sie nach Möglichkeit einen E-Mail-Server mit Unterstützung für authentifizierten Zugriff, und authentifizieren Sie den Zugriff mithilfe des Computerkontos des Standortservers. Falls Sie ein Benutzerkonto für die Authentifizierung angeben müssen, verwenden Sie eines mit den geringsten Berechtigungen.  

##  <a name="BKMK_Security_SiteServer"></a> Bewährte Sicherheitsmethoden für den Standortserver  
 Wenden Sie die folgenden bewährten Sicherheitsmethoden an, um den Configuration Manager-Standortserver zu sichern.  

 **Installieren Sie Configuration Manager auf einem Mitgliedsserver anstatt auf einem Domänencontroller.**  

 Die Configuration Manager-Standortserver und -Standortsysteme müssen nicht auf einem Domänencontroller installiert werden. Domänencontroller verfügen neben der Domänendatenbank über keine andere lokale SAM-Datenbank (Security Accounts Management). Wenn Sie Configuration Manager auf einem Mitgliedsserver installieren, können Sie die Configuration Manager-Konten in der lokalen SAM-Datenbank anstelle der Domänendatenbank warten.  

 Außerdem verringern Sie mit dieser Verfahrensweise die Angriffsfläche Ihrer Domänencontroller.  

 **Vermeiden Sie es beim Installieren sekundärer Standorte, die Dateien über das Netzwerk auf den sekundären Standortserver zu kopieren.**  

 Wenn Sie das Setup ausführen und einen sekundären Standort erstellen, aktivieren Sie nicht die Option zum Kopieren der Dateien vom übergeordneten in den sekundären Standort, und verwenden Sie keinen Quellspeicherort im Netzwerk. Wenn Sie Dateien über das Netzwerk kopieren, könnte ein geschickter Angreifer auf das Installationspaket des sekundären Standorts zugreifen und die darin enthaltenen Dateien vor der Installation manipulieren, auch wenn die zeitliche Organisation eines solchen Angriffs schwierig wäre. Dieses Risiko können Sie minimieren, indem Sie beim Übertragen der Dateien IPsec oder SMB verwenden.  

 Kopieren Sie die Quelldateien auf dem sekundären Standortserver aus dem Medienordner in einen lokalen Ordner, anstatt sie über das Netzwerk zu kopieren. Wenn Sie dann das Setup ausführen, um einen sekundären Standort zu erstellen, wählen Sie auf der Seite **Installationsquelldateien** die Option **Quelldateien in folgendem lokalen Speicherort auf dem sekundären Standortcomputer verwenden (am sichersten)** aus, und geben Sie diesen Ordner an.  

 Weitere Informationen finden Sie unter [Install a secondary site](../../../core/servers/deploy/install/use-the-setup-wizard-to-install-sites.md#bkmk_secondary) (Installieren eines sekundären Standorts) im Thema [Use the Setup Wizard to install sites](../../../core/servers/deploy/install/use-the-setup-wizard-to-install-sites.md) (Verwenden des Setup-Assistenten zum Installieren von Standorten).  

##  <a name="BKMK_Security_SQLServer"></a> Bewährte Sicherheitsmethoden für SQL Server  
 Configuration Manager verwendet SQL Server als Back-End-Datenbank. Wenn die Datenbank beschädigt ist, können Angreifer Configuration Manager umgehen und direkt auf SQL Server zugreifen, um Angriffe über Configuration Manager zu starten. Angriffe auf SQL Server müssen als hochriskant angesehen werden, und es müssen entsprechende Vorkehrungen getroffen werden.  

 Wenden Sie die folgenden bewährten Sicherheitsmethoden an, um SQL Server für Configuration Manager zu sichern.  

 **Verwenden Sie den Configuration Manager-Standortdatenbankserver nicht, um andere SQL Server-Anwendungen auszuführen.**  

 Je mehr Zugriffsmöglichkeiten auf den Configuration Manager-Standortdatenbankserver bestehen, desto größer ist das Risiko für Ihre Configuration Manager-Daten. Zudem sind auch andere Anwendungen auf dem gleichen SQL Server-Computer einem Risiko ausgesetzt, wenn die Configuration Manager-Standortdatenbank gefährdet ist.  

 **Konfigurieren Sie SQL Server für die Verwendung der Windows-Authentifizierung.**  

 Der Zugriff von Configuration Manager auf die Standortdatenbank erfolgt zwar über ein Windows-Konto und mithilfe der Windows-Authentifizierung, aber es ist dennoch möglich, SQL Server für die Verwendung des gemischten Modus von SQL Server zu konfigurieren. Durch den gemischten Modus von SQL Server werden zusätzliche SQL-Anmeldungen für den Zugriff auf die Datenbank ermöglicht. Dies ist jedoch nicht erforderlich und vergrößert zudem die Angriffsfläche.  

 **Unternehmen Sie zusätzliche Schritte, um zu gewährleisten, dass an sekundären Standorten, an denen SQL Server Express verwendet wird, die neuesten Softwareupdates verfügbar sind.**  

 Wenn Sie einen primären Standort installieren, wird SQL Server Express durch Configuration Manager vom Microsoft Download Center heruntergeladen, und die Dateien werden auf den primären Standortserver kopiert. Wenn Sie einen sekundären Standort installieren und die Option zum Installieren von SQL Server Express auswählen, wird die zuvor heruntergeladene Version von Configuration Manager installiert. Eine Prüfung, ob neue Versionen verfügbar sind, findet nicht statt. Führen Sie eines der folgenden Verfahren aus, um sicherzustellen, dass am sekundären Standort die neuesten Versionen verfügbar sind:  

-   Wenn der sekundäre Standort installiert ist, führen Sie Windows Update auf dem sekundären Standortserver aus.  

-   Installieren Sie zunächst SQL Server Express manuell auf dem Computer, auf dem der sekundäre Standortserver ausgeführt werden soll, bevor Sie den sekundären Standort installieren. Achten Sie darauf, die aktuellste Version und alle verfügbaren Softwareupdates zu installieren. Installieren Sie dann den sekundären Standort, und wählen Sie die Option zum Verwenden einer vorhandenen SQL Server-Instanz aus.  

Führen Sie in regelmäßigen Abständen Windows Update für diese Standorte und alle installierten Versionen von SQL Server aus, um zu gewährleisten, dass jeweils die aktuellsten Softwareupdates installiert sind.  

**Wenden Sie die bewährten Methoden für SQL Server an.**  

Identifizieren Sie die bewährten Methoden für Ihre Version von SQL Server, und wenden Sie sie an. Berücksichtigen Sie jedoch die folgenden Anforderungen für Configuration Manager:  

-   Das Computerkonto des Standortservers muss Mitglied der Administratorgruppe auf dem Computer sein, auf dem SQL Server ausgeführt wird. Wenn Sie der SQL Server-Empfehlung nachkommen, die Administratorprinzipale explizit bereitzustellen, muss das Konto, das zur Ausführung von Setup auf dem Standortserver verwendet wird, Mitglied der SQL-Benutzergruppe sein.  

-   Wenn Sie SQL Server mithilfe eines Domänenbenutzerkontos installieren, vergewissern Sie sich, dass das Computerkonto des Standortservers für einen Dienstprinzipalnamen (Service Principal Name, SPN), der in den Active Directory-Domänendiensten veröffentlicht wird, konfiguriert ist. Ohne den SPN treten bei der Kerberos-Authentifizierung und bei Configuration Manager-Setup Fehler auf.  

##  <a name="BKMK_Security_IIS"></a> Bewährte Sicherheitsmethoden für Standortsysteme, die IIS ausführen  
Mehrere Standortsystemrollen in Configuration Manager erfordern IIS. Wenn Sie IIS sichern, ist ein ordnungsgemäßer Betrieb von Configuration Manager möglich, und das Gefahrenpotenzial in Bezug auf Sicherheitsprobleme wird verringert. Minimieren Sie die Anzahl der Server, für die IIS erforderlich sind. Führen Sie beispielsweise nur so viele Verwaltungspunkte aus, wie Sie für Ihre Client-Basis benötigen. Berücksichtigen Sie dabei Faktoren wie hohe Verfügbarkeit und Netzwerkisolation für internetbasierte Clientverwaltung.  

 Wenden Sie die folgenden bewährten Sicherheitsmethoden zur Sicherung von Standortsystemen an, von denen IIS ausgeführt werden.  

 **Deaktivieren Sie IIS-Funktionen, die Sie nicht benötigen.**  

 Installieren Sie nur einen minimalen IIS-Funktionsumfang für die Standortsystemrolle, die Sie installieren. Weitere Informationen finden Sie unter [Site and site system prerequisites for System Center Configuration Manager](../../../core/plan-design/configs/site-and-site-system-prerequisites.md) (Standort- und Standortsystemanforderungen für System Center Configuration Manager).  

 **Konfigurieren Sie die Standortsystemrollen zum Erzwingen von HTTPS.**  

 Wenn von Clients eine Verbindung mit einem Standortsystem über HTTP statt HTTPS hergestellt wird, wird die Windows-Authentifizierung verwendet. Dies kann dazu führen, dass keine Kerberos-Authentifizierung, sondern NTLM-Authentifizierung verwendet wird. In diesem Fall können von den Clients Verbindungen mit einem nicht autorisierten Server hergestellt werden.  

 Eine Ausnahme von dieser bewährten Sicherheitsmethode gilt für Verteilungspunkte, da Paketzugriffskonten nicht funktionsfähig sind, wenn der Verteilungspunkt für HTTPS konfiguriert ist. Bei Paketzugriffskonten erfolgt eine Autorisierung für den Inhalt, sodass Sie den Zugriff auf den Inhalt auf bestimmte Benutzer beschränken können. Weitere Informationen finden Sie unter [Security best practices for content management (Bewährte Sicherheitsmethoden für die Inhaltsverwaltung)](../../../core/plan-design/hierarchy/security-and-privacy-for-content-management.md#BKMK_Security_ContentManagement).  

**Konfigurieren Sie für Standortsystemrollen eine Zertifikatvertrauensliste (Certificate Trust List, CTL) in IIS.**  

Standortsystemrollen:  

-   Verteilungspunkte, die für HTTPS konfiguriert sind  

-   Verwaltungspunkte, die für HTTPS konfiguriert und für die Unterstützung von mobilen Geräten aktiviert sind

Eine Zertifikatvertrauensliste (Certificate Trust List, CTL) ist eine definierte Liste von vertrauenswürdigen Stammzertifizierungsstellen. Wenn Sie eine Zertifikatvertrauensliste zusammen mit einer Gruppenrichtlinie und einer Public-Key-Infrastruktur (PKI)-Bereitstellung verwenden, können Sie die vorhandenen vertrauenswürdigen Stammzertifizierungsstellen ergänzen, die im Netzwerk konfiguriert sind (beispielsweise von Microsoft Windows automatisch installiert oder durch Windows-Unternehmens-Stammzertifizierungsstellen hinzugefügt). Ist in IIS jedoch eine Zertifikatvertrauensliste konfiguriert, wird eine Teilmenge der vertrauenswürdigen Stammzertifizierungsstellen durch diese definiert.  

Hierdurch haben Sie mehr Kontrolle über die Sicherheit, da von der Zertifikatvertrauensliste nur solche Zertifikate zugelassen werden, die von den aufgelisteten Zertifizierungsstellen ausgestellt wurden. Windows wird beispielsweise mit einer Anzahl von bekannten Zertifikaten von Drittanbieter-Zertifizierungsstellen geliefert, z.B. VeriSign und Thawte.

Zertifikate von diesen bekannten Zertifizierungsstellen werden von Computern mit IIS standardmäßig als vertrauenswürdig eingestuft. Wenn Sie IIS nicht mit einer Zertifikatvertrauensliste für die aufgelisteten Standortsystemrollen konfigurieren, werden alle Geräte mit Clientzertifikaten dieser Zertifizierungsstellen als gültige Configuration Manager-Clients zugelassen. Wenn Sie IIS mit einer CTL konfigurieren, die diese Zertifizierungsstellen nicht enthält, werden Clientverbindungen mit Zertifikaten dieser Zertifizierungsstellen abgelehnt. Damit Configuration Manager-Clients jedoch für die aufgelisteten Standortsystemrollen zugelassen werden, müssen Sie IIS mit einer CTL konfigurieren, die die von Configuration Manager-Clients verwendeten Zertifizierungsstellen angibt.  

> [!NOTE]  
>  Die Konfiguration einer Zertifikatvertrauensliste in IIS ist nur für die aufgelisteten Standortsystemrollen erforderlich. Für Clientcomputer, die mit HTTPS-Verwaltungspunkten verbunden werden, wird diese Funktionalität über die Liste der Zertifikataussteller bereitgestellt, die von Configuration Manager für Verwaltungspunkte verwendet wird.  

Weitere Informationen zum Konfigurieren einer Liste von vertrauenswürdigen Zertifizierungsstellen in IIS finden Sie in der IIS-Dokumentation.  

**Installieren Sie den Standortserver nicht auf einem Computer mit IIS.**  

Mit der Rollentrennung verringern Sie die Angriffsfläche und verbessern die Wiederherstellbarkeit. Zudem sind dem Computerkonto des Standortservers normalerweise Administratorberechtigungen auf allen Standortsystemrollen (und möglicherweise auf Configuration Manager-Clients, wenn Sie Clientpushinstallation verwenden) erteilt.  

**Verwenden dedizierter IIS-Server für Configuration Manager.**  

Sie können zwar mehrere webbasierte Anwendungen auf den IIS-Servern hosten, die auch von Configuration Manager verwendet werden, doch durch dieses Vorgehen kann die Angriffsfläche erheblich vergrößert werden. Ein Angreifer könnte aufgrund einer unzureichend konfigurierten Anwendung die Kontrolle über ein Configuration Manager-Standortsystem und in der Folge auch über die Hierarchie gewinnen.  

Wenn Sie andere webbasierte Anwendungen auf Configuration Manager-Standortsystemen ausführen müssen, erstellen Sie eine benutzerdefinierte Website für Configuration Manager-Standortsysteme.  

**Verwenden Sie eine benutzerdefinierte Website.**  

Sie können Configuration Manager für Standortsysteme, von denen IIS ausgeführt werden, so konfigurieren, dass statt der Standardwebsite für IIS eine benutzerdefinierte Website verwendet wird. Wenn das Ausführen anderer Webanwendungen auf dem Standortsystem erforderlich ist, müssen Sie eine benutzerdefinierte Website verwenden. Diese Einstellung ist nicht auf ein bestimmtes Standortsystem beschränkt, sondern gilt für den gesamten Standort.  

Wenn Sie andere Webanwendungen auf dem Standortsystem ausführen, müssen Sie nicht nur zusätzliche Sicherheit bereitstellen, sondern auch eine benutzerdefinierte Website verwenden.  

**Wenn Sie nach der Installation von Verteilungspunktrollen von der Standardwebsite zu einer benutzerdefinierten Website wechseln, entfernen Sie die virtuellen Standardverzeichnisse.**  

Wenn Sie von der Standardwebsite zu einer benutzerdefinierten Website wechseln, werden die alten virtuellen Verzeichnisse nicht von Configuration Manager entfernt. Entfernen Sie die virtuellen Verzeichnisse, die ursprünglich von Configuration Manager unter der Standardwebsite erstellt wurden.  

Bei einem Verteilungspunkt müssen Sie beispielsweise die folgenden virtuellen Verzeichnisse entfernen:  

-   SMS_DP_SMSPKG$  

-   SMS_DP_SMSSIG$  

-   NOCERT_SMS_DP_SMSPKG$  

-   NOCERT_SMS_DP_SMSSIG$  

**Wenden Sie die bewährten Methoden für IIS-Server an.**  

Ermitteln Sie die bewährten Methoden für Ihre Version von IIS-Server, und wenden Sie sie an. Berücksichtigen Sie jedoch alle Anforderungen, die unter Configuration Manager für bestimmte Standortsystemrollen gelten. Weitere Informationen finden Sie unter [Site and site system prerequisites for System Center Configuration Manager](../../../core/plan-design/configs/site-and-site-system-prerequisites.md) (Standort- und Standortsystemanforderungen für System Center Configuration Manager).  

##  <a name="BKMK_Security_ManagementPoint"></a> Bewährte Sicherheitsmethoden für den Verwaltungspunkt  
 Verwaltungspunkte sind die primäre Schnittstelle zwischen Geräten und Configuration Manager. Angriffe auf den Verwaltungspunkt und auf den Server, auf dem der Verwaltungspunkt ausgeführt wird, sind hochriskant. Es müssen daher entsprechende Vorkehrungen getroffen werden. Wenden Sie alle entsprechenden bewährten Sicherheitsmethoden an, und führen Sie eine Überwachung auf ungewöhnliche Aktivitäten hin aus.  

 Wenden Sie die folgenden bewährten Sicherheitsmethoden an, um Verwaltungspunkte in Configuration Manager zu sichern.  

**Wenn Sie einen Configuration Manager-Client am Verwaltungspunkt installieren, weisen Sie ihn dem Standort dieses Verwaltungspunkts zu.**  

 Achten Sie darauf, die Configuration Manager-Clients im Standortsystem eines Verwaltungspunkts ausschließlich dem Standort des Verwaltungspunkts zuzuweisen.  

 Wenn Sie von einer früheren Version zu System Center Configuration Manager migrieren, migrieren Sie so bald wie möglich die Clientsoftware auf dem Verwaltungspunkt zu System Center Configuration Manager.  

##  <a name="BKMK_Security_FSP"></a> Bewährte Sicherheitsmethoden für den Fallbackstatuspunkt  
 Wenden Sie die folgenden bewährten Sicherheitsmethoden an, wenn Sie einen Fallbackstatuspunkt in Configuration Manager installieren.  

 Weitere Informationen zu den Sicherheitserwägungen beim Installieren eines Fallbackstatuspunkts finden Sie unter [Determine Whether You Require a Fallback Status Point](../../../core/clients/deploy/plan/determine-the-site-system-roles-for-clients.md#determine-if-you-need-a-fallback-status-point).  


**Führen Sie keine anderen Standortsystemrollen auf dem Standortsystem aus, und installieren Sie den Fallbackstatuspunkt nicht auf einem Domänencontroller.**  

 Der Fallbackstatuspunkt ist darauf ausgelegt, nicht authentifizierte Kommunikation von beliebigen Computern zu akzeptieren. Daher wird das Gefahrenpotenzial in Bezug auf Sicherheitsprobleme für den betreffenden Server beträchtlich erhöht, wenn Sie diese Standortsystemrolle auf einem Domänencontroller oder zusammen mit anderen Standortsystemrollen ausführen.  

**Wenn Sie PKI-Zertifikate für die Clientkommunikation in Configuration Manager verwenden, installieren Sie den Fallbackstatuspunkt, bevor Sie die Clients installieren.**  

 Wenn von den Configuration Manager-Standortsystemen keine HTTP-Clientkommunikation akzeptiert wird, bemerken Sie möglicherweise nicht, dass Clients ggf. aufgrund von Problemen mit PKI-Zertifikaten nicht verwaltet werden. Wenn die Clients jedoch einem Fallbackstatuspunkt zugewiesen sind, werden solche Zertifikatsprobleme vom Fallbackstatuspunkt gemeldet.  

 Aus Sicherheitsgründen können Sie Clients nach deren Installation keinen Fallbackstatuspunkt mehr zuweisen. Diese Rolle können Sie nur während der Installation der Clients zuweisen.  

**Verwenden Sie den Fallbackstatuspunkt nicht im Umkreisnetzwerk.**  

 Es ist beabsichtigt, dass Daten von beliebigen Clients vom Fallbackstatuspunkt akzeptiert werden. Durch das Platzieren des Fallbackstatuspunkts im Umkreisnetzwerk kann die Problembehandlung bei internetbasierten Clients erleichtert werden. Diesen Vorteil müssen Sie jedoch gegen die Risiken abwägen, die entstehen, wenn vom Standortsystem nicht authentifizierte Daten in einem öffentlich zugänglichen Netzwerk akzeptiert werden.  

 Wenn Sie den Fallbackstatuspunkt doch im Umkreisnetzwerk oder in einem nicht vertrauenswürdigen Netzwerk installieren, verwenden Sie nicht die Standardeinstellung, bei der vom Fallbackstatuspunkt eine Verbindung mit dem Standortserver initiiert werden kann. Konfigurieren Sie stattdessen den Standortserver so, dass Datenübertragungen von diesem initiiert werden.  

##  <a name="BKMK_SecurityIssues_Clients"></a> Sicherheitsprobleme bei der Standortverwaltung  
 Überprüfen Sie die folgenden Sicherheitsprobleme für Configuration Manager:  

-   In Configuration Manager ist kein Schutz gegen autorisierte Administratoren verfügbar, die Configuration Manager zum Angriff auf das Netzwerk verwenden. Nicht autorisierte Administratoren stellen ein hohes Sicherheitsrisiko dar. Sie könnten zahlreiche Angriffe unternehmen, darunter die folgenden Strategien:  

    -   Verwenden der Softwarebereitstellung zum automatischen Installieren und Ausführen von Schadsoftware auf jedem Configuration Manager-Clientcomputer im Unternehmen  

    -   Verwenden der Remotesteuerung zum Steuern eines Configuration Manager-Clients ohne dessen Erlaubnis  

    -   Konfigurieren schneller Abrufintervalle und großer Inventarmengen, um Denial-of-Service-Angriffe gegen Clients und Server auszuführen  

    -   Verwenden eines Standorts der Hierarchie, um in die Active Directory-Daten eines anderen Standorts zu schreiben  

    Die Standorthierarchie ist die Sicherheitsgrenze. Betrachten Sie Standorte nur als Verwaltungsgrenzen.  

    Überwachen Sie alle Administratoraktivitäten, und überprüfen Sie die Überwachungsprotokolle regelmäßig. Unterziehen Sie alle Configuration Manager-Administratoren vor der Einstellung einer zwingenden Hintergrundüberprüfung, und machen Sie regelmäßige erneute Überprüfungen zur Bedingung für die Beschäftigung.  

-   Wenn der Anmeldungspunkt gefährdet ist, könnte ein Angreifer Authentifizierungszertifikate abrufen und die Anmeldeinformationen von Benutzern stehlen, die ihre mobilen Geräte anmelden.  

    Zwischen Anmeldungspunkt und Zertifizierungsstelle findet Kommunikation statt, und vom Anmeldungspunkt können Active Directory-Objekte erstellt, geändert und gelöscht werden. Installieren Sie einen Anmeldungspunkt niemals im Umkreisnetzwerk. Überwachen Sie den Anmeldungspunkt immer auf ungewöhnliche Aktivitäten hin.  

-   Wenn Sie Benutzerrichtlinien für die internetbasierte Clientverwaltung zulassen oder den Anwendungskatalog-Websitepunkt für die Verwendung durch Benutzer mit Internetzugang konfigurieren, erhöhen Sie die Angriffsfläche.  

    Bei diesen Konfigurationen werden Verbindungen zwischen Clients und Server über PKI-Zertifikate hergestellt, und es ist zudem eine Windows-Authentifizierung erforderlich, sodass möglicherweise die NTLM-Authentifizierung statt der Kerberos-Authentifizierung verwendet wird. Die NTLM-Authentifizierung ist anfällig für Identitätswechsel und Wiederholungsangriffe. Sie müssen Verbindungen zwischen dem internetbasierten Standortsystemserver und einem Domänencontroller zulassen, um Benutzer im Internet erfolgreich zu authentifizieren.  

-   Auf Standortsystemservern ist die Freigabe Admin$ erforderlich.  

    Der Configuration Manager-Standortserver verwendet die Admin$-Freigabe, um eine Verbindung mit Standortsystemen herzustellen und Dienstvorgänge auf diesen auszuführen. Deaktivieren Sie die Freigabe Admin$ nicht, und entfernen Sie sie nicht.  

-   Verbindungen mit anderen Computern werden in Configuration Manager mithilfe von Namensauflösungsdiensten hergestellt. Es ist schwierig, diese Dienste vor Angriffen wie Spoofing, Verfälschungen, Nichtanerkennung, Veröffentlichung von Informationen, Denial-of-Service oder Rechteerweiterungen zu schützen.  

    Identifizieren und befolgen Sie alle bewährten Sicherheitsmethoden für die Version von DNS und WINS, die Sie zur Namensauflösung verwenden.  

##  <a name="BKMK_Privacy_Cliients"></a> Datenschutzinformationen zur Ermittlung  
 Bei der Ermittlung werden Datensätze für Netzwerkressourcen erstellt und in der System Center Configuration Manager-Datenbank gespeichert. Discovery Data Records (DDRs) enthalten Computerinformationen wie IP-Adressen, Betriebssysteme und Computernamen. Außerdem können Active Directory-Ermittlungsmethoden zur Ermittlung jeglicher in den Active Directory-Domänendiensten gespeicherter Informationen konfiguriert werden.  

 Die einzige standardmäßig aktivierte Ermittlungsmethode ist die Frequenzermittlung. Hiermit werden jedoch nur Computer ermittelt, auf denen die System Center Configuration Manager-Clientsoftware bereits installiert ist.  

 Die ermittelten Informationen werden nicht an Microsoft gesendet. Sie werden stattdessen in der Configuration Manager-Datenbank gespeichert. Die Informationen verbleiben bis zum Löschen durch den Standortwartungstask **Veraltete Ermittlungsdaten löschen** in der Datenbank. Der Löschvorgang wird alle 90 Tage ausgeführt.  

 Berücksichtigen Sie beim Konfigurieren zusätzlicher Ermittlungsmethoden oder beim Erweitern der Active Directory-Ermittlung Ihre Datenschutzanforderungen.  
