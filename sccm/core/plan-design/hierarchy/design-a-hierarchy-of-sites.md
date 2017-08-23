---
title: "Entwurf einer Standorthierarchie – Configuration Manager | Microsoft-Dokumentation"
description: "Grundlegendes zu den verfügbaren Topologien und Verwaltungsoptionen für System Center Configuration Manager, damit Sie Ihre Standorthierarchie planen können."
ms.custom: na
ms.date: 6/16/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 07ce872e-1558-42ad-b5ad-582c5b1bdbb4
caps.latest.revision: "22"
caps.handback.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 4710b1b89eb50cb7bcf4c4ee50c12a96b6561bc9
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="design-a-hierarchy-of-sites-for-system-center-configuration-manager"></a>Entwerfen einer Hierarchie von Standorten für System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Vor der Installation des ersten Standorts einer neuen System Center Configuration Manager-Hierarchie sollten Sie sich mit den verfügbaren Topologien für Configuration Manager, den Typen der verfügbaren Standorte, ihren Beziehungen untereinander und dem Verwaltungsbereich vertraut machen, den jeder Standorttyp bereitstellt.
Nachdem Sie die Content Management-Optionen abgewogen haben, die die Anzahl der zu installierenden Standorte reduzieren können, können Sie eine Topologie planen, die effizient an Ihren aktuellen geschäftlichen Bedarf angepasst ist, und diese später erweitern, um zukünftiges Wachstum zu verwalten.  

> [!NOTE]
> Achten Sie bei der Planung einer neuen Configuration Manager-Installation auf die [Versionsanmerkungen]( /sccm/core/servers/deploy/install/release-notes), die aktuelle Probleme in den aktiven Versionen behandeln. Die Versionsanmerkungen gelten für alle Branches von Configuration Manager.  Wenn Sie allerdings [Technical Preview]( /sccm/core/get-started/technical-preview) verwenden, finden Sie in der Dokumentation für jede Version von Technical Preview Probleme, die nur für diesen Branch spezifisch sind.  

##  <a name="bkmk_topology"></a> Hierarchietopologie  
 Hierarchietopologien reichen von einzelnen eigenständigen primären Standorten bis zu einer Gruppe von verbundenen primären und sekundären Standorten mit einem zentralen Verwaltungsstandort am obersten Standort (obere Leiste) der Hierarchie.   Der Schlüsseltreiber für den Typ und die Anzahl der Standorte, die Sie in einer Hierarchie verwenden, entspricht normalerweise der Anzahl und der Art von Geräten, die Sie unterstützen müssen wie folgt:   

 **Ein eigenständiger primärer Standort:** Verwenden Sie einen eigenständigen primären Standort, wenn ein einziger primärer Standort die Verwaltung all Ihrer Geräte und Benutzer unterstützen kann (siehe [Sizing and scale numbers (Anpassen der Größe und Skalierung von Zahlen))](/sccm/core/plan-design/configs/size-and-scale-numbers). Diese Topologie ist auch erfolgreich, wenn für die unterschiedlichen geografischen Standorte Ihres Unternehmens ein einzelner primärer Standort ausreicht.  Sie können zur Verwaltung des Netzwerkverkehrs bevorzugte Verwaltungspunkte und eine sorgfältig geplante Inhaltsinfrastruktur verwenden (Informationen finden Sie unter [Grundlegende Konzepte für die Inhaltsverwaltung in System Center Configuration Manager](../../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md)).  

 Diese Topologie bietet u.a. folgende Vorteile:  

-   vereinfachter Verwaltungsaufwand  

-   vereinfachte Clientstandortzuweisung und Ermittlung der verfügbaren Ressourcen und Dienste  

-   Beseitigung möglicher Verzögerungen durch die Einführung der Datenbankreplikation zwischen Standorten

-   Option zum Erweitern einer eigenständigen primären Hierarchie in eine größere Hierarchie mit einem zentralen Verwaltungsstandort Dadurch können Sie neue primäre Standorte installieren, um den Umfang Ihrer Bereitstellung zu erweitern.  


**Ein Standort der zentralen Verwaltung mit mindestens einem untergeordneten primären Standorten:** Verwenden Sie diese Topologie, wenn Sie mehr als einen primären Standort benötigen, um die Verwaltung all Ihrer Geräte und Benutzer zu unterstützen.  Sie ist erforderlich, wenn Sie mehr als einen primären Standort verwenden müssen. Diese Topologie bietet u.a. folgende Vorteile:  


-   Sie unterstützt bis zu 25 primäre Standorte, durch die Sie den Umfang Ihrer Hierarchie erweitern können.  

-   Daher verwenden Sie immer den Standort der zentralen Verwaltung (sofern Sie Ihre Standorte nicht neu installieren). Dies ist eine dauerhafte Option. Sie können einen untergeordneten primären Standort nicht trennen, damit er zum eigenständigen primären Standort wird.

 Die folgenden Abschnitte können Ihnen dabei helfen zu verstehen, wann eine bestimmte Standort- oder Content Management-Option anstelle eines zusätzlichen Standorts verwendet werden sollte.  

##  <a name="BKMK_ChooseCAS"></a> Ermitteln des Zeitpunkts für die Verwendung eines Standorts der zentralen Verwaltung  
 Mithilfe eines Standorts der zentralen Verwaltung können Sie hierarchieweite Einstellungen konfigurieren und alle Standorte sowie Objekte in der Hierarchie überwachen. Von diesem Standorttyp werden Clients nicht direkt verwaltet, jedoch wird die Datenreplikation zwischen Standorten koordiniert. Auch die hierarchieweite Konfiguration von Standorten und Clients ist darin eingeschlossen.  

**Die folgenden Informationen können Sie bei der Entscheidung unterstützen, wann ein Standort der zentralen Verwaltung installiert werden sollte:**  

-   Der Standort der zentralen Verwaltung ist der Standort der obersten Ebene einer Hierarchie.  

-   Wenn Sie eine Hierarchie mit mehr als einem primären Standort konfigurieren, müssen Sie einen Standort der zentralen Verwaltung installieren. Wenn Sie sofort zwei oder mehr primäre Standorte benötigen, installieren Sie zuerst den Standort der zentralen Verwaltung. Wenn Sie bereits über einen primären Standort verfügen und dann einen Standort der zentralen Verwaltung installieren möchten, müssen Sie [den eigenständigen primären Standort erweitern](/sccm/core/servers/deploy/install/prerequisites-for-installing-sites#bkmk_expand), um den Standort der zentralen Verwaltung zu installieren. 

-   Es werden nur primäre Standorte als untergeordnete Standorte vom Standort der zentralen Verwaltung unterstützt.  

-   Es ist nicht möglich, dem Standort der zentralen Verwaltung Clients zuzuweisen.  

-   Der Standort der zentralen Verwaltung unterstützt keine Standortsystemrollen, die eine direkte Unterstützung für Clients bieten, z.B. Verwaltungspunkte und Verteilungspunkte.  

-   Mithilfe einer Configuration Manager-Konsole, die mit dem Standort der zentralen Verwaltung verbunden ist, können Sie alle Clients in der Hierarchie verwalten und Standortverwaltungstasks für jeden untergeordneten Standort ausführen. Dies kann das Installieren von Verwaltungspunkten oder anderen Standortsystemrollen an untergeordneten primären oder sekundären Standorten einbeziehen.  

-   Wenn Sie einen Standort der zentralen Verwaltung verwenden, ist dies der einzige Ort, an dem Sie Standortdaten von sämtlichen Standorten in Ihrer Hierarchie einsehen können. Hierin sind auch Informationen wie Inventurdaten und Statusmeldungen eingeschlossen.  

-   Sie können vom Standort der zentralen Verwaltung aus hierarchieweite Ermittlungsvorgänge konfigurieren, indem Sie Ermittlungsmethoden zur Ausführung an einzelnen Standorten zuweisen.  

-   Sie können die Sicherheit hierarchieweit verwalten, indem Sie verschiedenen Administratoren entsprechende Sicherheitsrollen, Sicherheitsbereiche und Sammlungen zuweisen. Diese Konfigurationen sind an jedem Standort in der Hierarchie gültig.  

-   Sie können eine Datei- und Datenbankreplikation konfigurieren, um die Kommunikation zwischen Standorten in der Hierarchie zu steuern. Dies umfasst die Planung der Datenbankreplikation für Standortdaten und die Verwaltung der Bandbreite für die Übertragung dateibasierter Daten zwischen Standorten.  

##  <a name="BKMK_ChoosePriimary"></a> Ermitteln des Zeitpunkts für die Verwendung eines primären Standorts  
 Verwenden Sie primäre Standorte, um Clients zu verwalten. Sie können einen primären Standort als untergeordneten primären Standort unter einem Standort der zentralen Verwaltung oder als ersten Standort einer neuen Hierarchie installieren. Wird ein primärer Standort als erster Standort einer Hierarchie installiert, dann bildet dieser einen eigenständigen primären Standort. Sekundäre Standorte als untergeordnete Standorte des primären Standorts werden sowohl von untergeordneten primären Standorten als auch von eigenständigen primären Standorten unterstützt.  

 Erwägen Sie die Verwendung eines primären Standorts aus einem der folgenden Gründe:  

-   zum Verwalten von Geräten und Benutzern  

-   zum Erhöhen der Anzahl von Geräten, die mit einer einzelnen Hierarchie verwaltet werden können  

-   zum Bereitstellen eines zusätzlichen Konnektivitätspunkts zur Verwaltung Ihrer Bereitstellung  

-   Sie möchten die Verwaltungsanforderungen Ihrer Organisation erfüllen. Beispielsweise könnten Sie einen primären Standort an einem Remotestandort installieren, um die Übertragung von Bereitstellungsinhalt über ein Netzwerk mit geringer Bandbreite zu verwalten. Sie können allerdings in System Center Configuration Manager bei der Übertragung von Daten an einen Verteilungspunkt die Optionen zur Drosselung der Netzwerkbandbreitenauslastung verwenden. Diese Inhaltsverwaltungsfunktion kann es überflüssig machen, zusätzliche Standorte zu installieren.  


**Die folgenden Informationen können Sie bei der Entscheidung unterstützen, wann ein primärer Standort installiert werden sollte:**  

-   Bei einem primären Standort kann es sich um einen eigenständigen primären Standort oder um einen untergeordneten primären Standort in einer größeren Hierarchie handeln. Wenn ein primärer Standort Mitglied einer Hierarchie mit einem Standort der zentralen Verwaltung ist, wird von den Standorten die Datenbankreplikation verwendet, um Daten zwischen den Standorten zu replizieren. Sofern Sie nicht mehr Clients und Geräte unterstützen müssen, als dies mit einem einzelnen primären Standort möglich ist, sollten Sie die Installation eines eigenständigen primären Standorts in Betracht ziehen.  Nachdem ein eigenständiger primärer Standort installiert wurde, können Sie diesen erweitern, um an einen neuen Standort der zentralen Verwaltung zu berichten, um für Ihre Bereitstellung zentral hochzuskalieren.  

-   Von einem primären Standort wird nur ein Standort der zentralen Verwaltung als übergeordneter Standort unterstützt.  

-   Von einem primären Standort werden nur sekundäre Standorte als untergeordnete Standorte unterstützt. Es können dabei auch mehrere sekundäre Standorte unterstützt werden.  

-   An primären Standorten werden alle Clientdaten der zugewiesenen Clients verarbeitet.  

-   Mithilfe der Datenbankreplikation erfolgt eine direkte Kommunikation der primären Standorte mit dem Standort der zentralen Verwaltung (dies wird beim Installieren eines neuen Standorts automatisch konfiguriert).  

##  <a name="BKMK_ChooseSecondary"></a> Ermitteln des Zeitpunkts für die Verwendung eines sekundären Standorts  
 Verwenden Sie sekundäre Standorte, um die Übertragung von Bereitstellungsinhalten und Clientdaten über Netzwerke mit geringer Bandbreite zu verwalten.  

 Ein sekundärer Standort wird mithilfe seines direkt übergeordneten primären Standorts oder mithilfe eines Standorts der zentralen Verwaltung verwaltet. Sekundäre Standorte müssen mit einem primären Standort verbunden sein. Sie können nicht zu einem anderen übergeordneten Standort verschoben werden, sondern müssen stattdessen deinstalliert und als untergeordneter Standort unter dem neuen primären Standort installiert werden.

Sie können jedoch Inhalt zwischen zwei sekundären Peer-Standorten weiterleiten, um die dateibasierte Replikation von Bereitstellunginhalt zu verwalten. Clientdaten werden vom sekundären Standort mithilfe von dateibasierter Replikation an einen primären Standort übertragen. Die dateibasierte Replikation wird vom sekundären Standort auch zur Kommunikation mit dem übergeordneten primären Standort verwendet.  

 Erwägen Sie die Installation eines sekundären Standorts, wenn eine der folgenden Bedingungen erfüllt ist:  

-   Sie benötigen keinen lokalen Verbindungspunkt für einen Administrator.  

-   Sie müssen die Übertragung von Bereitstellungsinhalt an Standorte verwalten, die sich in der Hierarchie weiter unten befinden.  

-   Sie müssen Clientinformationen verwalten, die an Standorte gesendet werden, die sich in der Hierarchie weiter oben befinden.  

 Wenn Sie keinen sekundären Standort installieren möchten und es Clients an Remotestandorten gibt, erwägen Sie den Einsatz von Windows BranchCache oder das Installieren von Verteilungspunkten, die für die Bandbreitensteuerung und Planung aktiviert sind. Nach Wunsch können Sie diese Inhaltsverwaltungsoptionen mit sekundären Standorten kombinieren. Außerdem können Sie mit diesen Optionen die Anzahl der Standorte und Server reduzieren, die Sie installieren müssen. Informationen zu Inhaltsverwaltungsoptionen in Configuration Manager finden Sie unter [Ermitteln des Zeitpunkts für die Verwendung der Optionen für die Inhaltsverwaltung](#BKMK_ChooseSecondaryorDP).  


**Die folgenden Informationen können Sie bei der Entscheidung unterstützen, wann ein sekundärer Standort installiert werden sollte:**  

-   Falls keine lokale SQL Server-Instanz verfügbar ist, wird SQL Server Express im Rahmen der Standortinstallation von sekundären Standorten automatisch installiert.  

-   Die Installation des sekundären Standorts wird über die Configuration Manager-Konsole eingeleitet, anstatt das Setup direkt auf einem Computer auszuführen.  

-   Sekundäre Standorte verwenden eine Teilmenge der Informationen in der Standortdatenbank, wodurch die Datenmenge verringert wird, die bei der Datenbankreplikation zwischen den übergeordneten primären und sekundären Standort repliziert wird.  

-   Das Routing dateibasierter Inhalte an andere sekundäre Standorte mit dem gleichen übergeordneten primären Standort wird von sekundären Standorten unterstützt.  

-   Bei der Installation eines sekundären Standorts werden auf dem sekundären Standortserver automatisch ein Verwaltungspunkt und ein Verteilungspunkt bereitgestellt.  

##  <a name="BKMK_ChooseSecondaryorDP"></a> Ermitteln des Zeitpunkts für die Verwendung der Optionen für die Inhaltsverwaltung  
 Falls es Clients an Remotenetzwerkorten gibt, sollten Sie erwägen, anstatt eines primären oder sekundären Standorts einige Inhaltsverwaltungsoptionen zu verwenden. Die Anforderung zur Installation eines Standorts kann häufig beseitigt werden, wenn Sie Windows BranchCache verwenden, Verteilungspunkte zur Steuerung der Bandbreite konfigurieren oder Inhalte manuell auf Verteilungspunkte kopieren (Inhalte vorab bereitstellen).  


**Erwägen Sie, einen Verteilungspunkt bereitzustellen, anstatt einen weiteren Standort zu installieren, falls Folgendes zutrifft:**  

-   Dank der verfügbaren Netzwerkbandbreite ist die Kommunikation zwischen Clientcomputern an einem Remotestandort und an einem Verwaltungspunkt möglich. Von den Clientcomputern können Clientrichtlinien heruntergeladen sowie Inventurdaten, Statusberichte und Ermittlungsinformationen gesendet werden.  

-   Die von Background Intelligent Transfer Service (BITS) bereitgestellte Bandbreitensteuerung deckt sich nicht mit Ihren Netzwerkanforderungen.  

 Weitere Informationen zu Content Management-Optionen in Configuration Manager finden Sie unter [Grundlegende Konzepte für die Inhaltsverwaltung in System Center Configuration Manager](../../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md).  

##  <a name="bkmk_beyond"></a> Jenseits der Hierarchietopologie  
 Bedenken Sie, welche Dienste oder Funktionen zusätzlich zu einer anfänglichen Hierarchietopologie von verschiedenen Standorten in der Hierarchie (Standortsystemrollen) zur Verfügung gestellt werden, und wie hierarchieweite Konfigurationen und Funktionen in Ihrer Infrastruktur verwaltet werden. Die folgenden allgemeinen Überlegungen werden in separaten Themen behandelt. Diese sind wichtig, da sie Ihren Hierarchieentwurf beeinflussen, oder von diesem beeinflusst werden können:  

-   Wenn Sie die [Verwaltung von Computern und Geräten mit System Center Configuration Manager](/sccm/core/clients/manage/manage-clients) vorbereiten, sollten Sie berücksichtigen, ob die von Ihnen verwalteten Geräte sich an Ihrem Standort oder in der Cloud befinden, oder ob eigene Geräte der Benutzer darunter sind (BYOD).  Berücksichtigen Sie darüber hinaus Ihre Vorgehensweise beim Verwalten von Geräten, die von verschiedenen Verwaltungsoptionen unterstützt werden, z.B. Windows 10-Computer, die direkt von Configuration Manager oder über die Integration mit Microsoft Intune verwaltet werden können.  

-   Vergegenwärtigen Sie sich die möglichen Auswirkungen Ihrer verfügbaren Netzwerkinfrastruktur auf den Datenfluss zwischen Remotestandorten (siehe [Vorbereiten der Netzwerkumgebung für System Center Configuration Manager](/sccm/core/plan-design/network/configure-firewalls-ports-domains)). Berücksichtigen Sie auch, wo sich von Ihnen verwaltete Benutzer und Geräte geografisch befinden, und ob diese über Ihre Unternehmensdomäne oder das Internet auf Ihre Infrastruktur zugreifen.  

-   Planen Sie eine Inhaltsinfrastruktur, um die von Ihnen bereitgestellten Informationen (Dateien und Apps) effizient an von Ihnen verwaltete Geräte zu verteilen (siehe [Verwalten von Inhalt und Inhaltsinfrastruktur für System Center Configuration Manager](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md)).  

-   Ermitteln Sie, welche [Features und Funktionen von System Center Configuration Manager](../../../core/plan-design/changes/features-and-capabilities.md) Sie verwenden möchten, welche Standortsystemrollen oder Windows-Infrastruktur sie erfordern, und auf welchen Standorten in einer Hierarchie mit mehreren Standorten Sie sie für die effizienteste Nutzung Ihrer Netzwerk- und Serverressourcen bereitstellen können.  

-   Berücksichtigen Sie die Daten- und Gerätesicherheit, einschließlich der Verwendung einer PKI. Informationen hierzu finden Sie unter [PKI-Zertifikatanforderungen für System Center Configuration Manager](../../../core/plan-design/network/pki-certificate-requirements.md).  


**Überprüfen Sie die folgenden Ressourcen für standortspezifische Konfigurationen:**  

-   [Planen des SMS-Anbieters für System Center Configuration Manager](../../../core/plan-design/hierarchy/plan-for-the-sms-provider.md)  

-   [Planen der Standortdatenbank für System Center Configuration Manager](../../../core/plan-design/hierarchy/plan-for-the-site-database.md)  

-   [Planen für Standortsystemserver und Standortsystemrollen für System Center Configuration Manager](../../../core/plan-design/hierarchy/plan-for-site-system-servers-and-site-system-roles.md)  

-   [Planen der Sicherheit in System Center Configuration Manager](../../../core/plan-design/security/plan-for-security.md)  

-   [Managing network bandwidth](../../../core/plan-design/hierarchy/manage-network-bandwidth.md) bei der Bereitstellung von Inhalten innerhalb eines Standorts  


**Betrachten Sie die Konfigurationen, die Standorte und Hierarchien umfassen:**  

-   [Hochverfügbarkeitsoptionen für System Center Configuration Manager](/sccm/protect/understand/high-availability-options) für Standorte und Hierarchien

-   [Erweitern Sie das Active Directory-Schema für System Center Configuration Manager](../../../core/plan-design/network/extend-the-active-directory-schema.md) und konfigurieren Sie Standorte, um [Standortdaten für System Center Configuration Manager zu veröffentlichen](../../../core/servers/deploy/configure/publish-site-data.md).  

-   [Datenübertragungen zwischen Standorten in System Center Configuration Manager](../../../core/servers/manage/data-transfers-between-sites.md)  

-   [Grundlagen der rollenbasierten Verwaltung für System Center Configuration Manager](../../../core/understand/fundamentals-of-role-based-administration.md)
