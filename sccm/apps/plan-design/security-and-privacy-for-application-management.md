---
title: "Sicherheit und Datenschutz für die Anwendungsverwaltung | Microsoft Docs"
description: "Bewährte Sicherheits- und Datenschutzmethoden für die Anwendungsverwaltung in System Center Configuration Manager"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4d26deed-3b16-4116-b640-f618f2c20f5a
caps.latest.revision: "8"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 6ee99fa0c07676f004e41a50bf16d0d17604e790
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="security-and-privacy-for-application-management-in-system-center-configuration-manager"></a>Sicherheit und Datenschutz für die Anwendungsverwaltung in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*


##  <a name="security-best-practices-for-application-management"></a>Bewährte Sicherheitsmethoden für die Anwendungsverwaltung  

|Bewährte Sicherheitsmethode|Weitere Informationen|  
|----------------------------|----------------------|  
|Konfigurieren Sie die Anwendungskatalogpunkte für die Verwendung von HTTPS-Verbindungen, und klären Sie die Benutzer über die Gefahren schädlicher Websites auf.|Konfigurieren Sie Anwendungskatalog-Websitepunkt sowie Anwendungskatalog-Webdienstpunkt so, dass HTTPS-Verbindungen von ihnen akzeptiert werden. Hierdurch wird der Server für die Benutzer authentifiziert, und übertragene Daten werden vor Manipulationen und Zugriffen geschützt. Beugen Sie Social-Engineering-Angriffen vor, indem Sie die Benutzer dazu anhalten, nur Verbindungen zu vertrauenswürdigen Websites herzustellen.<br /><br /> Verwenden Sie die Konfigurationsoptionen für das Branding, mit denen der Name Ihrer Organisation als Identitätsnachweis im Anwendungskatalog angezeigt wird, nur dann, wenn Sie HTTPS verwenden.|  
|Verwenden Sie die Rollentrennung, und installieren Sie den Websitepunkt und den Dienstpunkt des Anwendungskatalogs auf separaten Servern.|Wenn der Anwendungskatalog-Websitepunkt gefährdet ist, installieren Sie ihn auf einem anderen Server als den Anwendungskatalog-Webdienstpunkt. Dies trägt zum Schutz der Configuration Manager-Clients und der Configuration Manager-Infrastruktur bei. Dies ist vor allem dann wichtig, wenn vom Anwendungskatalog-Websitepunkt Clientverbindungen aus dem Internet akzeptiert werden, da der Server hierdurch anfällig für Angriffe wird.|  
|Halten Sie die Benutzer dazu an, nach Verwendung des Anwendungskatalogs das Browserfenster zu schließen.|Wenn Benutzer eine externe Website in dem gleichen Browserfenster aufrufen wie zuvor den Anwendungskatalog, werden die Sicherheitseinstellungen für vertrauenswürdige Orte im Intranet vom Browser beibehalten.|  
|Geben Sie die Affinität zwischen Benutzer und Gerät manuell an, anstatt zuzulassen, dass Benutzer ihr primäres Gerät selbst angeben. Aktivieren Sie die verwendungsbasierte Konfiguration nicht.|Betrachten Sie Informationen, die von Benutzern oder Geräten erfasst werden, nicht als maßgeblich. Wenn Sie Software mithilfe einer Affinität zwischen Benutzer und Gerät bereitstellen, die nicht von einem vertrauenswürdigen Administrator angegeben wurde, ist eine Installation der Software auf Geräten und für Benutzer möglich, die nicht zum Empfangen der Software autorisiert sind.|  
|Konfigurieren Sie Bereitstellungen stets so, dass Inhalt nicht auf den Verteilungspunkten ausgeführt, sondern nur von ihnen heruntergeladen wird.|Wenn Sie Bereitstellungen so konfigurieren, dass Inhalt von Verteilungspunkten heruntergeladen und lokal ausgeführt wird, wird der Hashwert des Pakets nach dem Herunterladen zunächst auf dem Configuration Manager-Client überprüft. Wenn der Hashwert nicht mit dem Wert in der Richtlinie übereinstimmt, wird das Paket verworfen. Wenn Sie die Bereitstellung dagegen so konfigurieren, dass sie direkt auf einem Verteilungspunkt ausgeführt wird, wird der Hashwert des Pakets nicht vom Configuration Manager-Client überprüft. Eine Installation von manipulierter Software durch den Configuration Manager-Client wird hierdurch ermöglicht.<br /><br /> Wenn Sie Bereitstellungen direkt auf Verteilungspunkten ausführen müssen, verwenden Sie die niedrigsten NTFS-Berechtigungen für die Pakete auf den Verteilungspunkten, und sichern Sie die Kanäle zwischen Client und Verteilungspunkten sowie zwischen Verteilungspunkten und Standortserver mithilfe von Internetprotokollsicherheit (Internet Protocol security, IPsec).|  
|Lassen Sie keine Benutzerinteraktionen mit Programmen zu, wenn die Option **Mit Administratorrechten ausführen** erforderlich ist.|Beim Konfigurieren eines Programms können Sie die Option **Benutzerinteraktion mit dem Programm zulassen** auswählen, sodass die Benutzer auf alle nötigen Aufforderungen in der Benutzeroberfläche reagieren können. Ist das Programm auch für **Mit Administratorrechten ausführen**konfiguriert, kann ein Angreifer auf den Computer, auf dem das Programm ausgeführt wird, die Benutzeroberfläche verwenden, um die Berechtigungen für den Clientcomputer auszuweiten.<br /><br /> Verwenden Sie für Softwarebereitstellungen, für die Administratoranmeldeinformationen erforderlich sind, Programme, die Windows Installer für das Setup und benutzerbezogen erhöhte Rechte verwenden. Das Setup muss im Kontext eines Benutzers ausgeführt werden, der über keine Administratoranmeldeinformationen verfügt. Die Verwendung von benutzerspezifisch erhöhten Windows Installer-Rechten stellt die sicherste Möglichkeit dar, Anwendungen mit dieser Anforderung bereitzustellen.|  
|Legen Sie anhand der Clienteinstellung **Installationsberechtigungen** fest, ob Benutzer Software interaktiv installieren können.|Konfigurieren Sie unter **Computer-Agent** mit der Clientgeräteeinstellung **Installationsberechtigungen** die Benutzertypen, die zu Softwareinstallationen mithilfe des Anwendungskatalogs oder von Softwarecenter berechtigt sind. Erstellen Sie beispielsweise eine benutzerdefinierte Clienteinstellung, indem Sie für **Installationsberechtigungen** die Einstellung **Nur Administratoren**festlegen. Wenden Sie diese Clienteinstellung dann auf eine Serversammlung an, um Benutzer ohne Administratorberechtigungen an einer Installation von Software auf diesen Computern zu hindern.|  
|Stellen Sie für mobile Geräte nur Anwendungen bereit, die signiert sind.|Stellen Sie Anwendungen für mobile Geräte nur bereit, wenn diese über eine Codesignatur von einer Zertifizierungsstelle (Certification Authority, CA) verfügen, die vom mobilen Gerät als vertrauenswürdig eingestuft wird. Beispiel:<br /><br /><ul><li>Eine Anwendung eines Anbieters, die von einer bekannten Zertifizierungsstelle wie VeriSign signiert ist</li><li>Eine interne Anwendung, die Sie unabhängig von Configuration Manager von einer eigenen Zertifizierungsstelle signieren lassen</li><li>Eine interne Anwendung, die Sie mithilfe von Configuration Manager signieren, wenn Sie den Anwendungstyp erstellen und ein Signaturzertifikat verwenden</li></ul>|  
|Wenn Sie Anwendungen für mobile Geräte mithilfe des **Assistenten zum Erstellen von Anwendungen** in Configuration Manager signieren, sichern Sie den Speicherort der Signaturzertifikatdatei sowie den Kommunikationskanal.|Speichern Sie als Schutz vor Rechteerweiterungen sowie „Man-in-the-middle“-Angriffen die Signaturzertifikatsdatei in einem gesicherten Ordner, und verwenden Sie IPsec oder SMB (Server Message Block) zwischen den folgenden Computern:<br /><br /><ul><li>Computer, auf dem die Configuration Manager-Konsole ausgeführt wird</li><li>Computer, auf dem die Signaturzertifikatsdatei gespeichert ist</li><li>Computer, auf dem die Quelldateien der Anwendung gespeichert sind</li></ul> Signieren Sie die Anwendung alternativ unabhängig von Configuration Manager, bevor Sie den **Assistenten zum Erstellen von Anwendungen** ausführen.|  
|Implementieren Sie Zugriffssteuerungen zum Schutz von Referenzcomputern.|Vergewissern Sie sich, dass Referenzcomputer, die von Administratoren zum Konfigurieren der Erkennungsmethode in einem Bereitstellungstyp verwendet werden, nicht gefährdet sind.|  
|Überwachen Sie die Administratoren, denen rollenbasierte Sicherheitsrollen im Zusammenhang mit der Anwendungsverwaltung gewährt werden, und beschränken Sie ihre Anzahl.<br /><br /><ul><li>**Anwendungsadministrator**</li><li>**Anwendungsautor**</li><li> **Anwendungsbereitstellungs-Manager**</li></ul>|Selbst wenn Sie eine rollenbasierte Verwaltung festgelegt haben, verfügen Administratoren, die Anwendungen erstellen und bereitstellen, möglicherweise über mehr Berechtigungen, als Ihnen bewusst ist. Administratoren, die beispielsweise eine Anwendung erstellen oder ändern, können abhängige Anwendungen auch außerhalb ihres Sicherheitsbereichs auswählen.|  
|Wenn Sie virtuelle App-V-Umgebungen (Microsoft Application Virtualization) konfigurieren, wählen Sie Anwendungen aus, die dieselbe Vertrauensebene in der virtuellen Umgebung aufweisen.|Da Anwendungen in einer virtuellen App-V-Umgebung Ressourcen wie die Zwischenablage gemeinsam verwenden können, konfigurieren Sie die virtuelle Umgebung so, dass die ausgewählten Anwendungen dieselbe Vertrauensebene aufweisen.<br /><br /> Weitere Informationen finden Sie unter [Erstellen von virtuellen App-V-Umgebungen](../../apps/deploy-use/create-app-v-virtual-environments.md).|  
|Stellen Sie bei der Bereitstellung von Anwendungen für Macintosh-Computer sicher, dass die Quelldateien aus einer vertrauenswürdigen Quelle stammen.|Die Signatur des Quellpakets wird vom CMAppUtil-Tool nicht überprüft, daher müssen Sie sicherstellen, dass der Herkunft des Pakets vertraut werden kann. Mit dem CMAppUtil-Tool lässt sich nicht erkennen, ob die Dateien manipuliert wurden.|  
|Wenn Sie Anwendungen für Macintosh-Computer bereitstellen, sichern Sie den Speicherort der **CMMAC**-Datei und den Kommunikationskanal, wenn Sie diese Datei in Configuration Manager importieren.|Die **CMMAC**-Datei, die mit dem CMAppUtil-Tool erstellt wurde und die Sie in Configuration Manager importieren, ist weder signiert noch geprüft. Um eine Manipulation der Datei zu verhindern, sollten Sie sie in einem gesicherten Ordner speichern und IPsec oder SMB zwischen den folgenden Computern verwenden:<br /><br /><ul><li>Computer, auf dem die Configuration Manager-Konsole ausgeführt wird</li><li>Computer, auf dem die **CMMAC**-Datei gespeichert wird</li></ul>.|  
|Wenn Sie einen Bereitstellungstyp für Webanwendungen konfigurieren, verwenden Sie HTTPS anstellen von HTTP, um die Verbindung zu schützen.|Wenn Sie eine Webanwendung über einen HTTP-Link und nicht über einen HTTPS-Link bereitstellen, könnte das Gerät auf einen nicht autorisierten Server umgeleitet werden, und zwischen dem Gerät und dem Server übertragene Daten könnten manipuliert werden.|  

##  <a name="security-issues-for-application-management"></a>Sicherheitsprobleme bei der Anwendungsverwaltung  

-   Benutzer mit geringsten Rechten können Dateien aus dem Cache des Clientcomputers kopieren.  

     Benutzer können den Clientcache zwar lesen, aber nicht in ihn schreiben. Mit Leseberechtigungen können Benutzer Anwendungsinstallationsdateien von einem Computer auf einen anderen kopieren.  

-   Benutzer mit geringen Rechten können Dateien ändern, die den Softwarebereitstellungsverlauf auf dem Clientcomputer aufzeichnen.  

     Benutzer können Dateien ändern, die Informationen über den Installationszustand von Anwendungen enthalten, da Informationen zum Anwendungsverlauf nicht geschützt sind.  

-   App-V-Pakete sind nicht signiert.  

     Eine Signierung zur Überprüfung, ob der Inhalt aus einer vertrauenswürdigen Quelle stammt und bei der Übertragung nicht verändert wurde, wird von App-V-Paketen in Configuration Manager nicht unterstützt. Für dieses Sicherheitsproblem ist keine Risikominderung vorhanden. Befolgen Sie auf jeden Fall die Best Practise zur Sicherheit für das Herunterladen des Inhalts von einer vertrauenswürdigen Quelle und von einem sicheren Speicherort.  

-   Veröffentlichte App-V-Anwendungen können von allen Benutzern auf dem Computer installiert werden.  

     Wenn eine App-V-Anwendung auf einem Computer veröffentlicht wird, können alle Benutzer, die sich auf diesem Computer anmelden, diese Anwendung installieren. Dies bedeutet, dass Sie nicht einschränken können, welche Benutzer die Anwendung nach der Veröffentlichung installieren können.  

-   Sie können die Installationsberechtigungen für das Unternehmensportal nicht einschränken.  

     Sie können zwar Clienteinstellungen konfigurieren, um Installationsberechtigungen einzuschränken, z.B. auf die primären Benutzer von Geräten oder auf lokale Administratoren, aber diese Einstellung ist im Unternehmensportal nicht wirksam. Dadurch könnte es zu einer Rechteerweiterung kommen, da Benutzer eine App installieren könnten, ohne dazu berechtigt zu sein.  

##  <a name="BKMK_CertificatesSilverlight5"></a> Zertifikate für Microsoft Silverlight 5 und für den Anwendungskatalog erforderlicher Modus mit höherer Vertrauensstellung  
 Für Configuration Manager-Clients ist Microsoft Silverlight 5 erforderlich, das im Modus mit höherer Vertrauensstellung ausgeführt werden muss, damit Benutzer Software aus dem Anwendungskatalog installieren können. Standardmäßig werden Silverlight-Anwendungen im Modus mit teilweiser Vertrauensstellung ausgeführt, um den Zugriff von Anwendungen auf Benutzerdaten zu verhindern. Microsoft Silverlight 5 wird von Configuration Manager automatisch auf Clients installiert, wenn es noch nicht installiert ist. Standardmäßig wird die Computer-Agent-Clienteinstellung **Ausführen von Silverlight-Anwendungen im Modus mit höherer Vertrauensstellung zulassen** von Configuration Manager auf **Ja** festgelegt. Mit dieser Einstellung können signierte und vertrauenswürdige Silverlight-Anwendungen den Modus mit höherer Vertrauensstellung anfordern.  

 Wenn Sie die Standortsystemrolle des Anwendungskatalog-Websitepunkts installieren, wird im Computer-Zertifikatspeicher für vertrauenswürdige Herausgeber auf jedem Configuration Manager-Clientcomputer ein Microsoft-Signaturzertifikat installiert. Mit diesem Zertifikat können Silverlight-Anwendungen, die mit diesem Zertifikat signiert sind, im Modus mit höherer Vertrauensstellung ausgeführt werden, der für Computer erforderlich ist, um Software aus dem Anwendungskatalog zu installieren. Configuration Manager verwaltet das Signaturzertifikat automatisch. Entfernen oder verschieben Sie dieses Microsoft-Signaturzertifikat zur Sicherung der Dienstkontinuität nicht.  

> [!WARNING]  
>  Bei aktivierter Clienteinstellung **Ausführen von Silverlight-Anwendungen im Modus mit höherer Vertrauensstellung zulassen** können alle Silverlight-Anwendungen, die mit Zertifikaten aus dem Zertifikatspeicher für vertrauenswürdige Herausgeber im Computerspeicher oder im Benutzerspeicher signiert sind, im Modus mit erhöhter Vertrauensstellung ausgeführt werden. Über die Clienteinstellung kann der Modus mit höherer Vertrauensstellung nicht speziell für den Configuration Manager-Anwendungskatalog oder den Zertifikatspeicher für vertrauenswürdige Herausgeber im Computerspeicher aktiviert werden. Wenn dem Speicher für vertrauenswürdige Herausgeber von Schadsoftware, z. B. im Benutzerspeicher, ein Rogue-Zertifikat hinzugefügt wird, kann Schadsoftware, von der eine eigene Silverlight-Anwendung verwendet wird, nun auch im Modus mit erhöhter Vertrauensstellung ausgeführt werden.  

 Wenn Sie die Clienteinstellung **Ausführen von Silverlight-Anwendungen im Modus mit höherer Vertrauensstellung zulassen** auf **Nein** festlegen, wird das Microsoft-Signaturzertifikat nicht von den Clients entfernt.  

 Weitere Informationen zu vertrauenswürdigen Anwendungen in Silverlight finden Sie unter [Trusted Applications ](http://go.microsoft.com/fwlink/p/?LinkId=252842) (Vertrauenswürdige Anwendungen).  

##  <a name="privacy-information-for-application-management"></a>Datenschutzinformationen zur Anwendungsverwaltung  
 Mit der Anwendungsverwaltung können Sie Anwendungen, Programme oder Skripts auf jedem Clientcomputer oder jedem mobilen Clientgerät in der Hierarchie ausführen. Welche Typen von Anwendungen, Programmen oder Skripts Sie ausführen und welche Informationen übertragen werden, kann von Configuration Manager nicht gesteuert werden. Beim Anwendungsbereitstellungsprozess werden von Configuration Manager möglicherweise Informationen übertragen, anhand derer die Geräte- und Anmeldekonten zwischen Clients und Servern identifiziert werden können.  

 In Configuration Manager werden Statusinformationen zum Softwarebereitstellungsprozess verwaltet. Diese Statusinformationen zum Softwarebereitstellungsprozess sind bei der Übertragung nicht verschlüsselt, wenn vom Client kein HTTPS zur Kommunikation verwendet wird. In der Datenbank werden die Statusinformationen unverschlüsselt gespeichert.  

 Für das Verwenden der Configuration Manager-Installation zur interaktiven, unbeaufsichtigten oder Remoteinstallation von Software auf Clients gelten möglicherweise die Lizenzbedingungen der Software. Diese unterscheiden sich von den Softwarelizenzbedingungen für System Center Configuration Manager. Bevor Sie Software mit Configuration Manager bereitstellen, müssen Sie stets die Softwarelizenzbedingungen lesen und akzeptieren.  

 Die Anwendungsbereitstellung wird nicht standardmäßig ausgeführt. Zur Ausführung sind mehrere Konfigurationsschritte erforderlich.  

 Zwei optionale Funktionen zur Vereinfachung effizienter Softwarebereitstellung sind die Affinität zwischen Benutzer und Gerät und der Anwendungskatalog:  

-   Mithilfe der Affinität zwischen Benutzer und Gerät werden Geräte Benutzern zugeordnet, sodass ein Configuration Manager-Administrator Software für einen Benutzer bereitstellen kann und diese Software automatisch auf einem oder mehreren Computern installiert wird, die der Benutzer am häufigsten verwendet.  

-   Der Anwendungskatalog ist eine Website, über die Benutzer Softwareinstallationen anfordern können.  

 In den folgenden Abschnitten finden Sie Datenschutzinformationen zur Affinität zwischen Benutzer und Gerät sowie zum Anwendungskatalog.  

 Berücksichtigen Sie beim Konfigurieren der Anwendungsverwaltung Ihre Datenschutzanforderungen.  

##  <a name="user-device-affinity"></a>Affinität zwischen Benutzer und Gerät  
-  Von Configuration Manager werden möglicherweise Informationen zwischen Clients und Verwaltungspunkt-Standortsystemen übertragen. Anhand der Informationen können unter Umständen die Computer und Anmeldekonten sowie die Verwendungszusammenfassung zu den Anmeldekonten identifiziert werden.  
-  Die zwischen Client und Server übertragenen Daten werden nur dann verschlüsselt, wenn aufgrund der Konfiguration des Verwaltungspunkts eine Clientkommunikation über HTTPS erforderlich ist.  
-  Die Computerinformationen und Verwendungsinformationen zum Anmeldekonto, die zur Zuordnung von Benutzern und Geräten verwendet werden, werden auf den Clientcomputern gespeichert, an Verwaltungspunkte gesendet und dann in der Configuration Manager-Datenbank gespeichert. Die alten Informationen werden standardmäßig nach 90 Tagen aus der Datenbank gelöscht. Das Löschverhalten können Sie konfigurieren, indem Sie den Standortwartungstask **Veraltete Daten zur Affinität zwischen Benutzer und Gerät löschen** festlegen.
-  Configuration Manager verwaltet Statusinformationen zur Affinität zwischen Benutzer und Gerät. Statusinformationen werden bei der Übertragung nur dann verschlüsselt, wenn die Clients für die Kommunikation mit Verwaltungspunkten über HTTPS konfiguriert sind. In der Datenbank werden die Statusinformationen unverschlüsselt gespeichert.  
-  Computerinformationen, Verwendungsinformationen zum Anmeldekonto und Statusinformationen werden nicht an Microsoft gesendet.  
-  Computerinformationen und Verwendungsinformationen zum Anmeldekonto, die zum Festlegen von Affinitäten zwischen Benutzern und Geräten verwendet werden, sind stets aktiviert. Außerdem können auch Benutzer und Administratoren Informationen zur Affinität zwischen Benutzern und Geräten beitragen.  

##  <a name="application-catalog"></a>Anwendungskatalog  
-  Mithilfe des Anwendungskatalogs kann der Configuration Manager-Administrator beliebige Anwendungen, Programme und Skripts zur Ausführung durch die Benutzer veröffentlichen. Welche Typen von Programmen oder Skripts im Katalog veröffentlicht und welche Informationen übertragen werden, kann von Configuration Manager nicht gesteuert werden.    
-  Von Configuration Manager werden möglicherweise Informationen zwischen Clients und den Standortsystemrollen „Anwendungskatalog“ übertragen. Anhand der Informationen können unter Umständen die Computer und die Anmeldekonten identifiziert werden. Informationen werden bei der Übertragung zwischen Clients und Servern nur dann verschlüsselt, wenn eine Verbindung der Clients über HTTPS aufgrund der Konfiguration dieser Standortsystemrollen erforderlich ist.  
-  Die Informationen zu Genehmigungsanforderungen für Anwendungen werden in der Configuration Manager-Datenbank gespeichert. Abgebrochene oder abgelehnte Anforderungen und die zugehörigen Einträge zum Anforderungsverlauf werden standardmäßig nach 30 Tagen gelöscht. Sie können das Löschverhalten konfigurieren, indem Sie den Standortwartungstask **Veraltete Anwendungsanforderungsdaten löschen** einstellen. Zugelassene und ausstehende Genehmigungsanforderungen für Anwendungen werden nie gelöscht.  
-  Informationen, die an den Anwendungskatalog gesendet und von ihm empfangen werden, werden nicht an Microsoft gesendet.  
-  Der Anwendungskatalog wird nicht standardmäßig installiert. Für diese Installation sind mehrere Konfigurationsschritte erforderlich.  
