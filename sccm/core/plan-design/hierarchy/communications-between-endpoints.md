---
title: "Datenübertragungen zwischen Endpunkten | Microsoft-Dokumentation"
description: "Erfahren Sie, wie System Center Configuration Manager-Standortsysteme und -Komponenten über ein Netzwerk kommunizieren."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 68fe0e7e-351e-4222-853a-877475adb589
caps.latest.revision: "10"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: cd94f9ccc7e196b30e5dc7ae9368d073b7cff5d2
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="communications-between-endpoints-in-system-center-configuration-manager"></a>Datenübertragungen zwischen Endpunkten in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*


##  <a name="Planning_Intra-site_Com"></a> Kommunikation zwischen Standortsystemen in einem Standort  
 Wenn Configuration Manager-Standortsysteme oder -Komponenten über das Netzwerk mit anderen Standortsystemen oder Configuration Manager-Komponenten kommunizieren, wird in Abhängigkeit davon, wie Sie den Standort konfiguriert haben, eines der folgenden Protokolle verwendet:  

-   Server Message Block (SMB)  

-   HTTP  

-   HTTPS  

Die Kommunikation zwischen den Servern an einem Standort kann jederzeit und ohne Steuerung der Netzwerkbandbreite auftreten. Dies trifft nicht auf die Kommunikation zwischen dem Standortserver und einem Verteilungspunkt zu. Da Sie die Kommunikation zwischen Standortsystemen nicht steuern können, achten Sie darauf, die Standortsystemserver an Orten mit schnellen Netzwerken mit guter Verbindung zu installieren.  

Für die Verwaltung der Inhaltsübertragung vom Standortserver zu Verteilungspunkten haben Sie folgende Möglichkeiten:  

-   Konfigurieren Sie den Verteilungspunkt für die Steuerung und Planung der Netzwerkbandbreite. Diese Steuerelemente ähneln den von standortübergreifenden Adressen verwendeten Konfigurationen. Häufig können Sie diese Konfiguration verwenden, anstatt einen weiteren Configuration Manager-Standort zu installieren, falls die Übertragung von Inhalt an Remotenetzwerkorte bei der Bandbreite Priorität hat.  

-   Sie können einen Verteilungspunkt als vorab bereitgestellten Verteilungspunkt installieren. Mithilfe eines vorab bereitgestellten Verteilungspunkts können Sie Inhalt verwenden, der auf dem Verteilungspunktserver manuell abgelegt wird. Die Notwendigkeit, Inhaltsdateien über das Netzwerk zu übertragen, entfällt damit.  

Weitere Informationen finden Sie unter [Verwalten von Netzwerk-Bandbreite für das Content Management in System Center Configuration Manager](manage-network-bandwidth.md).


##  <a name="Planning_Client_to_Site_System"></a> Kommunikation von Clients mit Standortsystemen und Diensten  
Clients initiieren die Kommunikation mit Standortsystemrollen, Active Directory-Domänendiensten und Onlinediensten. Damit diese Kommunikation möglich ist, müssen die Firewalls den Netzwerkdatenverkehr zwischen Clients und dem Endpunkt der Kommunikation zulassen. Endpunkte können Folgendes sein:  

-   **Anwendungskatalog-Websitepunkt**: Unterstützt HTTP- und HTTPS-Kommunikation

-   **Cloudbasierte Ressourcen**: Dazu gehören Microsoft Azure und Microsoft Intune  

-   **Configuration Manager-Richtlinienmodul (NDES)**: Unterstützt HTTP- und HTTPS-Kommunikation

-   **Verteilungspunkte**: Unterstützt HTTP- und HTTPS-Kommunikation, und HTTPS ist für cloudbasierte Verteilungspunkte erforderlich  

-   **Fallbackstatuspunkt**: Unterstützt HTTP-Kommunikation  

-   **Verwaltungspunkt**: Unterstützt HTTP- und HTTPS-Kommunikation  

-   **Microsoft Update**  

-   **Softwareupdatepunkte**: Unterstützt HTTP- und HTTPS-Kommunikation  

-   **Zustandsmigrationspunkt**: Unterstützt HTTP- und HTTPS-Kommunikation  

-   **Verschiedene Domänendienste**  

Bevor ein Client mit einer Standortsystemrolle kommunizieren kann, verwendet der Client die Dienstidentifizierung, um nach einer Standortsystemrolle zu suchen, die das Protokoll des Clients (HTTP oder HTTPS) unterstützt. Clients verwenden standardmäßig die sicherste Methode, die ihnen zur Verfügung steht:  

-   Zur Verwendung von HTTPS müssen Sie über eine Public Key-Infrastruktur (PKI) verfügen und PKI-Zertifikate auf Clients und Servern installieren. Informationen zum Verwenden von Zertifikaten finden Sie unter [PKI-Zertifikatanforderungen für System Center Configuration Manager](../../../core/plan-design/network/pki-certificate-requirements.md).  

-   Wenn Sie eine Standortsystemrolle bereitstellen, die Internetinformationsdienst (IIS) verwendet und die Kommunikation von Clients unterstützt, müssen Sie angeben, ob Clients eine Verbindung mit dem Standortsystem über HTTP oder HTTPS herstellen. Falls Sie sich für HTTP entscheiden, müssen Sie auch Signierungs- und Verschlüsselungsoptionen erwägen. Weitere Informationen finden Sie unter [Planen von Signierung und Verschlüsselung](../../../core/plan-design/security/plan-for-security.md#BKMK_PlanningForSigningEncryption) in [Planen der Sicherheit in System Center Configuration Manager](../../../core/plan-design/security/plan-for-security.md).  

Weitere Informationen zur Dienstidentifizierung durch Clients finden Sie unter [Verstehen, wie Clients Standortressourcen und -dienste für System Center Configuration Manager suchen](../../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md).  

Details zu Ports und Protokollen, die von Clients verwendet werden, wenn diese mit den Endpunkten kommunizieren, finden Sie unter [In System Center Configuration Manager verwendete Ports](../../../core/plan-design/hierarchy/ports.md).  

###  <a name="BKMK_clientspan"></a> Überlegungen zur Clientkommunikation aus dem Internet oder einer nicht vertrauenswürdigen Gesamtstruktur  
Die folgenden, an primären Standorten installierten Standortsystemrollen unterstützen Verbindungen von Clients, die sich an nicht vertrauenswürdigen Standorten wie dem Internet oder einer nicht vertrauenswürdigen Gesamtstruktur befinden. (Sekundäre Standorte unterstützen Clientverbindungen von nicht vertrauenswürdigen Standorten nicht):  

-   Anwendungskatalog-Websitepunkt  

-   Configuration Manager-Richtlinienmodul  

-   Verteilungspunkt (HTTPS ist für cloudbasierte Verteilungspunkte erforderlich)  

-   Anmeldungsproxypunkt  

-   Fallbackstatuspunkt  

-   Verwaltungspunkt  

-   Softwareupdatepunkt  

**Informationen zu Standortsystemen mit Internetzugriff:**   
Eine Vertrauensstellung zwischen der Gesamtstruktur eines Clients und des Standortsystemservers ist nicht erforderlich. Wenn die Gesamtstruktur jedoch mit einem Standortsystem mit Internetzugriff der Gesamtstruktur vertraut, die die Benutzerkonten enthält, unterstützt diese Konfiguration benutzerbasierte Richtlinien für Geräte im Internet, wenn Sie die **Clientrichtlinie**-Clienteinstellung **Benutzerrichtlinienanforderungen von Internetclients aktivieren** aktivieren.  

Aus den nachstehenden Konfigurationsbeispielen geht hervor, unter welchen Umständen Benutzerrichtlinien für Geräte im Internet von der internetbasierten Clientverwaltung unterstützt werden:  

-   Der internetbasierte Verwaltungspunkt befindet sich im Umkreisnetzwerk, wo der Benutzer von einem schreibgeschützten Domänencontroller authentifiziert wird und Active Directory-Pakete von einer beteiligten Firewall zugelassen werden.  

-   Das Benutzerkonto befindet sich in Gesamtstruktur A (im Internet) und der internetbasierte Verwaltungspunkt in Gesamtstruktur B (im Umkreisnetzwerk). Gesamtstruktur A wird von Gesamtstruktur B als vertrauenswürdig eingestuft, und die Authentifizierungspakete werden von einer beteiligten Firewall zugelassen.  

-   Das Benutzerkonto und der internetbasierte Verwaltungspunkt befinden sich in Gesamtstruktur A (im Intranet). Der Verwaltungspunkt wird über einen Webproxyserver im Internet veröffentlicht (wie Forefront Threat Management Gateway).  

> [!NOTE]  
>  Sollte die Kerberos-Authentifizierung nicht möglich sein, wird automatisch die Authentifizierung über NTLM versucht.  

Wie aus dem vorstehenden Beispiel hervorgeht, können Sie internetbasierte Standortsysteme im Intranet platzieren, wenn diese über einen Webproxyserver wie ISA Server und Forefront Threat Management Gateway im Internet veröffentlicht werden. Sie können für diese Standortsysteme festlegen, dass Clientverbindungen nur aus dem Internet oder sowohl aus dem Intranet als auch aus dem Internet unterstützt werden. Einen Webproxyserver können Sie für SSL-zu-SSL-Bridging (Secure Sockets Layer) oder SSL-Tunneling wie folgt konfigurieren (wobei von Ersterem ein höheres Maß an Sicherheit geboten wird):  

-   **SSL-zu-SSL-Bridging:**   
    Wenn Sie Proxywebserver bei der internetbasierten Clientverwaltung einsetzen, ist SSL-zu-SSL-Bridging empfehlenswert, bei dem ein SSL-Tunnelabschluss mit Authentifizierung verwendet wird. Die Authentifizierung von Clientcomputern muss über die Computerauthentifizierung erfolgen. Die Authentifizierung der Legacyclients mobiler Geräte erfolgt über die Benutzerauthentifizierung. SSL-Bridging wird von mobilen Geräten, die mithilfe von Configuration Manager angemeldet wurden, nicht unterstützt.  

     Der SSL-Tunnelabschluss für den Proxywebserver hat den Vorteil, dass Pakete aus dem Internet überprüft werden, bevor sie an das interne Netzwerk weitergeleitet werden. Die vom Client eingehende Verbindung wird vom Proxywebserver authentifiziert und beendet, und dann wird eine neue authentifizierte Verbindung mit dem internetbasierten Standortsystem hergestellt. Wenn von Configuration Manager-Clients ein Proxywebserver verwendet wird, wird die Clientidentität (Client-GUID) sicher als Bestandteil der Paketnutzdaten transportiert, sodass der Proxywebserver vom Verwaltungspunkt nicht als Client betrachtet wird. In Configuration Manager wird kein HTTP-zu-HTTPS- oder HTTPS-zu-HTTP-Bridging unterstützt.  

-   **Tunneling**:   
    Falls die Anforderungen für SSL-Bridging vom Proxywebserver nicht erfüllt werden können oder falls Sie die Internetunterstützung für mobile Geräte, die mithilfe von Configuration Manager registriert wurden, konfigurieren möchten, wird auch SSL-Tunneling unterstützt. Diese Option ist weniger sicher, da die SSL-Pakete aus dem Internet ohne SSL-Tunnelabschluss an die Standortsysteme weitergeleitet werden und daher nicht auf schädliche Inhalte überprüft werden können. Bei der Verwendung von SSL-Tunneling müssen vom Proxywebserver keine Zertifikatanforderungen erfüllt werden.  

##  <a name="Plan_Com_X-Forest"></a> Kommunikation zwischen Active Directory-Gesamtstrukturen  
System Center Configuration Manager unterstützt Standorte und Hierarchien, die mehrere Active Directory-Gesamtstrukturen umfassen.  

Configuration Manager unterstützt auch Domänencomputer, die sich nicht in der gleichen Active Directory-Gesamtstruktur wie der Standortserver befinden, sowie Computer in Arbeitsgruppen:  

-   **Um Domänencomputer in einer Gesamtstruktur zu unterstützen, die für die Gesamtstruktur Ihres Standortservers nicht vertrauenswürdig ist**, haben Sie folgenden Möglichkeiten:  

    -   Installieren von Standortsystemrollen in dieser nicht vertrauenswürdigen Gesamtstruktur mit der Option, Standortinformationen an diese Active Directory-Gesamtstruktur zu veröffentlichen  

    -   Verwalten Sie diese Computer, als wären sie Arbeitsgruppencomputer.  

  Wenn Sie Standortsystemserver in einer nicht vertrauenswürdigen Active Directory-Gesamtstruktur installieren, erfolgt die Kommunikation zwischen Clients und Servern dieser Gesamtstruktur ausschließlich in der Gesamtstruktur, und Configuration Manager kann die Computer über Kerberos authentifizieren. Wenn Sie Standortinformationen in der Gesamtstruktur des Clients veröffentlichen, hat dies Vorteile für die Clients, denn Standortinformationen, beispielsweise eine Liste verfügbarer Verwaltungspunkte, werden aus ihrer Active Directory-Gesamtstruktur abgerufen und müssen nicht vom ihnen zugewiesenen Verwaltungspunkt heruntergeladen werden.  

  > [!NOTE]  
  >  Wenn Sie Geräte im Internet verwalten möchten, können Sie internetbasierte Standortsystemrollen in Ihrem Umkreisnetzwerk installieren, wenn sich die Standortsystemserver in einer Active Directory-Gesamtstruktur befinden. Für dieses Szenario ist keine bidirektionale Vertrauensstellung zwischen dem Umkreisnetzwerk und der Gesamtstruktur des Standortservers erforderlich.  

-   **Damit Computer in einer Arbeitsgruppe unterstützt werden**, ist Folgendes erforderlich:  

    -   Manuelles Genehmigen von Arbeitsgruppencomputern, wenn für diese HTTP-Clientverbindungen mit Standortsystemrollen verwendet werden. Dies ist erforderlich, weil Configuration Manager diese Computer nicht über Kerberos authentifizieren kann.  

    -   Konfigurieren von Arbeitsgruppenclients, sodass sie das Netzwerkzugriffskonto verwenden, damit diese Computer Inhalte vom Verteilungspunkt abrufen können.  

    -   Bereitstellen eines alternativen Mechanismus für Arbeitsgruppenclients, über den sie nach Verwaltungspunkten suchen können. Sie können die DNS-Veröffentlichung oder WINS verwenden oder einen Verwaltungspunkt direkt zuweisen. Dies ist erforderlich, weil diese Clients keine Standortinformationen aus Active Directory-Domänendiensten abrufen können.  

    Zugehörige Ressourcen in dieser Inhaltsbibliothek:  

    -   [Verwalten von in Konflikt stehenden Datensätzen bei Configuration Manager-Clients](../../../core/clients/manage/manage-clients.md#BKMK_ConflictingRecords)  

    -   [Netzwerkzugriffskonto](../../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#accounts-used-for-content-management)  

    -   [Installieren von Configuration Manager-Clients auf Arbeitsgruppencomputern](../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientWorkgroup)  

###  <a name="bkmk_span"></a> Szenarien zum Unterstützen eines Standorts oder einer Hierarchie, der oder die sich über mehrere Domänen und Gesamtstrukturen erstreckt  

#### <a name="communication-between-sites-in-a-hierarchy-that-spans-forests"></a>Kommunikation zwischen Standorten in einer Hierarchie, die mehrere Gesamtstrukturen umfasst:  
Dieses Szenario erfordert eine bidirektionale Vertrauensstellung, die die Kerberos-Authentifizierung unterstützt.  Falls keine bidirektionale Gesamtstrukturvertrauensstellung vorhanden ist, die die Kerberos-Authentifizierung unterstützt, wird von Configuration Manager kein untergeordneter Standort in der Remotegesamtstruktur unterstützt.  

 **Configuration Manager unterstützt das Installieren eines untergeordneten Standorts in einer Remotegesamtstruktur, die über die erforderliche bidirektionale Vertrauensstellung mit der Gesamtstruktur des übergeordneten Standorts verfügt.**  

-   Beispiel: Sie können einen sekundären Standort in einer Gesamtstruktur platzieren, die nicht mit seinem übergeordneten primären Standort identisch ist, sofern die erforderliche Vertrauensstellung vorliegt.  

> [!NOTE]  
>  Bei einem untergeordneten Standort kann es sich um einen primären Standort (wobei der Standort der zentralen Verwaltung der übergeordnete Standort ist) oder um einen sekundären Standort handeln.  

Für die standortübergreifende Kommunikation werden in Configuration Manager die Datenbankreplikation und dateibasierte Übertragungen verwendet. Beim Installieren eines Standorts müssen Sie ein Konto angeben, mit dem Sie den Standort auf dem gewünschten Server installieren. Über dieses Konto wird auch die Kommunikation zwischen Standorten hergestellt und verwaltet.  

Nachdem der Standort erfolgreich installiert wurde und dateibasierte Übertragungen sowie die Datenbankreplikation initiiert wurden, ist die Konfiguration der Kommunikation für diesen Standort abgeschlossen.  

**Wenn eine bidirektionale Vertrauensstellung zwischen Gesamtstrukturen gegeben ist, sind in Configuration Manager keine weiteren Konfigurationsschritte erforderlich.**  

Bei der Installation eines neuen Standorts, der einem anderen Standort untergeordnet ist, wird von Configuration Manager standardmäßig Folgendes konfiguriert:  

-   Eine Route für die standortübergreifende, dateibasierte Replikation an jedem Standort, von der das Computerkonto des Standortservers verwendet wird. Configuration Manager fügt das Computerkonto jedes Computers zur Gruppe **SMS_SiteToSiteConnection_&lt;Standortcode\>** auf dem Zielcomputer hinzu.  

-   Datenbankreplikation zwischen SQL Server an jedem Standort  

Außerdem muss Folgendes konfiguriert werden:  

-   Die von Configuration Manager benötigten Netzwerkpakete müssen von beteiligten Firewalls und Netzwerkgeräten zugelassen werden.  

-   Die Namensauflösung muss zwischen den Gesamtstrukturen möglich sein.  

-   Zum Installieren eines Standorts oder einer Standortsystemrolle müssen Sie ein Konto mit lokalen Administratorrechten auf dem angegebenen Computer angeben.  

#### <a name="communication-in-a-site-that-spans-forests"></a>Kommunikation an einem Standort, der mehrere Gesamtstrukturen umfasst  
Dieses Szenario erfordert keine bidirektionale Vertrauensstellung.  

**Primäre Standorte unterstützen die Installation von Standortsystemrollen auf Computern in Remotegesamtstrukturen**.  

-   Der Anwendungskatalog-Webdienstpunkt ist die einzige Ausnahme.  Er wird nur in derselben Gesamtstruktur wie der Standortserver unterstützt.  

-   Wenn von einer Standortsystemrolle Verbindungen aus dem Internet akzeptiert werden, wird empfohlen, diese Standortsystemrollen an einem Standort zu installieren, an dem die Gesamtstrukturgrenze Schutz für den Standortserver bereitstellt (z. B. in einem Umkreisnetzwerk).  

**So installieren Sie eine Standortsystemrolle auf einem Computer in einer nicht vertrauenswürdigen Gesamtstruktur:**  

-   Geben Sie ein **Standortsystem-Installationskonto** an, das verwendet wird, um die Standortsystemrolle zu installieren. (Dieses Konto benötigt lokale Administratoranmeldeinformationen für die Verbindung.) Danach installieren Sie Standortsystemrollen auf dem angegebenen Computer.  

-   Sie müssen die Standortsystemoption **Verbindungen mit diesem Standortsystem müssen vom Standortserver hergestellt werden**aktivieren. Damit müssen vom Standortserver Verbindungen mit dem Standortsystemserver hergestellt werden, um Daten zu übertragen. Dies verhindert, dass der Computer am nicht vertrauenswürdigen Standort einen Kontakt mit dem Standortserver initiiert, der sich in Ihrem vertrauenswürdigen Netzwerk befindet. Diese Verbindungen verwenden das **Standortsystem-Installationskonto**.  

**Wenn Sie eine Standortsystemrolle verwenden möchten, die in einer nicht vertrauenswürdigen Gesamtstruktur installiert war,** müssen Firewalls den Netzwerkdatenverkehr zulassen, und zwar selbst dann, wenn der Standortserver die Datenübertragung initiiert.  

Außerdem benötigen die folgenden Standortsystemrollen einen direkten Zugriff auf die Standortdatenbank. Aus diesem Grund müssen Firewalls entsprechenden Datenverkehr aus der nicht vertrauenswürdigen Gesamtstruktur an den SQL Server des Standorts zulassen:  

-   Asset Intelligence-Synchronisierungspunkt  

-   Endpoint Protection-Punkt  

-   Anmeldungspunkt  

-   Verwaltungspunkt  

-   Reporting Services-Punkt  

-   Zustandsmigrationspunkt  

Weitere Informationen finden Sie unter [In System Center Configuration Manager verwendete Ports](../../../core/plan-design/hierarchy/ports.md).  

**Sie müssen möglicherweise den Zugriff der Standortsystemrolle auf die Standortdatenbank konfigurieren:**  

Von beiden Standortsystemrollen „Verwaltungspunkt“ und „Anmeldungspunkt“ wird eine Verbindung mit der Standortdatenbank hergestellt.  

-   Bei der Installation dieser Standortsystemrollen wird das Computerkonto des neuen Standortsystemservers von Configuration Manager standardmäßig als Verbindungskonto für die Standortsystemrolle konfiguriert und dann der entsprechenden SQL Server-Datenbankrolle hinzugefügt.  

-   Wenn Sie diese Standortsystemrollen in einer nicht vertrauenswürdigen Domäne installieren, müssen Sie das Verbindungskonto der Standortsystemrolle konfigurieren, damit von der Standortsystemrolle Informationen aus der Datenbank abgerufen werden können.  

Wenn Sie ein Domänenbenutzerkonto so konfigurieren, dass es das Verbindungskonto für diese Standortsystemrollen ist, müssen Sie darauf achten, dass das Domänenbenutzerkonto geeignete Zugriffsrechte für die SQL Server-Datenbank am Standort hat:  

-   Verwaltungspunkt: **Verwaltungspunkt-Datenbankverbindungskonto**  

-   Anmeldungspunkt: **Anmeldungspunkt-Verbindungskonto**  

Erwägen Sie beim Planen von Standortsystemrollen in anderen Gesamtstrukturen auch die folgenden Punkte:  

-   Legen Sie bei Verwendung von Windows-Firewall in den entsprechenden Firewall-Profilen fest, dass die Kommunikation zwischen dem Standortdatenbankserver und Computern, auf den Remote-Standortsystemrollen installiert sind, zulässig ist. Informationen zu Firewall-Profilen finden Sie unter [Grundlegendes zu Firewall-Profilen](http://go.microsoft.com/fwlink/p/?LinkId=233629).  

-   Wenn die Gesamtstruktur, die die Benutzerkonten enthält, von den internetbasierten Verwaltungspunkten als vertrauenswürdig eingestuft wird, werden Benutzerrichtlinien unterstützt. Wenn keine Vertrauensstellung vorhanden ist, werden nur Computerrichtlinien unterstützt.  

#### <a name="communication-between-clients-and-site-system-roles-when-the-clients-are-not-in-the-same-active-directory-forest-as-their-site-server"></a>Kommunikation zwischen Clients und Standortsystemrollen, wenn die Clients nicht der gleichen Active Directory-Gesamtstruktur wie der zugehörige Standortserver angehören  
Configuration Manager unterstützt die folgenden Szenarios für Clients, die sich nicht in derselben Gesamtstruktur wie der Standortserver ihres Standorts befinden:  

-   Zwischen der Gesamtstruktur des Clients und der Gesamtstruktur des Standortservers besteht eine bidirektionale Vertrauensstellung.  

-   Der Standortsystemrollenserver befindet sich in der gleichen Gesamtstruktur wie der Client.  

-   Der Client befindet sich auf einem Domänencomputer ohne bidirektionale Vertrauensstellung mit der Gesamtstruktur, und es sind keine Standortsystemrollen in der Gesamtstruktur des Clients installiert.  

-   Der Client befindet sich auf einem Arbeitsgruppencomputer.  

Die Active Directory-Domänendienste können von Clients auf einem zur Domäne gehörenden Computer zur Dienstidentifizierung verwendet werden, sofern der entsprechende Standort in der Active Directory-Gesamtstruktur veröffentlicht wurde.  

Um Standortinformationen in einer anderen Active Directory-Gesamtstruktur zu veröffentlichen, müssen Sie folgende Aktionen ausführen:  

-   Angeben der Gesamtstruktur und dann Aktivieren der Veröffentlichung in dieser Gesamtstruktur im Arbeitsbereich **Verwaltung** im Knoten **Active Directory-Gesamtstrukturen** .  

-   Konfigurieren jedes Standorts, sodass er seine Daten in Active Directory-Domänendiensten veröffentlicht. Von den Clients in dieser Gesamtstruktur können dann Standortinformationen abgerufen und Verwaltungspunkte gefunden werden. Für Clients, von denen Active Directory Domain Services nicht zur Dienstidentifizierung verwendet werden kann, besteht die Möglichkeit, DNS, WINS oder den Verwaltungspunkt zu verwenden, der dem Client zugewiesen wurde.  

###  <a name="bkmk_xchange"></a> Anordnen des Exchange Server-Connectors in einer Remotegesamtstruktur  
Damit dieser Fall unterstützt wird, müssen Sie darauf achten, dass die Namensauflösung zwischen Gesamtstrukturen funktioniert (konfigurieren Sie beispielsweise DNS-Weiterleitung), und geben Sie beim Konfigurieren des Exchange Server-Connectors die Intranet-FQDN von Exchange Server an. Weitere Informationen finden Sie unter [Verwalten von mobilen Geräten mit System Center Configuration Manager und Microsoft Intune](../../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md).  
