---
title: "Standortsystemrollen für Clients | Microsoft Docs"
description: "Ermitteln Sie die Standortsystemrollen für Clients in System Center Configuration Manager."
ms.custom: na
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-client
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 984e8d92-7327-4b08-9228-0c955e6ac778
caps.latest.revision: "9"
caps.handback.revision: "0"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 9f2dda834f23b2ee85c4c301c7e1b6a3a54ebc97
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="determine-the-site-system-roles-for-system-center-configuration-manager-clients"></a>Ermitteln der Standortsystemrollen für System Center Configuration Manager-Clients

*Gilt für: System Center Configuration Manager (Current Branch)*

Die Informationen in diesem Thema können Ihnen beim Bestimmen der Standortsystemrollen helfen, die zum Bereitstellen von Configuration Manager-Clients erforderlich sind:  

 Weitere Informationen zum Installationsort der erforderlichen Standortsystemrollen in der Hierarchie finden Sie unter [Entwerfen einer Hierarchie von Standorten für System Center Configuration Manager](../../../../core/plan-design/hierarchy/design-a-hierarchy-of-sites.md).  

 Weitere Informationen zur Installation und Konfiguration der erforderlichen Standortsystemrollen finden Sie unter [Install site system roles (Installieren von Standortsystemrollen)](../../../../core/servers/deploy/configure/install-site-system-roles.md).  

##  <a name="determine-if-you-need-a-management-point"></a>Bestimmen, ob ein Verwaltungspunkt erforderlich ist  
 Standardmäßig wird für alle Windows-Clientcomputer ein Verteilungspunkt für die Installation des Configuration Manager-Clients verwendet. Wenn ein Verteilungspunkt nicht verfügbar ist, ist ein Fallback auf einen Verwaltungspunkt möglich. Mithilfe der CCMSetup-Befehlszeileneigenschaft **/source:<Pfad\>** können Windows-Clients jedoch auch von einer alternativen Quelle aus auf Computern installiert werden. So können Sie beispielsweise beim Installieren von Clients im Internet vorgehen. Vielleicht möchten Sie aber auch das Senden von Netzwerkpaketen zwischen dem Computer und dem Verwaltungspunkt bei der Clientinstallation vermeiden, weil die erforderlichen Ports durch eine Firewall blockiert werden oder Sie über eine Verbindung mit geringer Bandbreite verfügen. Allerdings ist für alle Clients die Kommunikation mit einem Verwaltungspunkt erforderlich, damit sie einem Standort zugewiesen und von Configuration Manager verwaltet werden können.  

 Weitere Informationen zur CCMSetup-Befehlszeileneigenschaft **/source:<Path\>** finden Sie unter [Informationen zu Clientinstallationseigenschaften in System Center Configuration Manager](../../../../core/clients/deploy/about-client-installation-properties.md).  

 Wenn Sie mehrere Verwaltungspunkte in der Hierarchie installieren, stellen Clients basierend auf ihrer Gesamtstrukturmitgliedschaft und Netzwerkadresse automatisch eine Verbindung mit einem Punkt her. Sie können an einem sekundären Standort nicht mehr als einen Verwaltungspunkt installieren.  

 Macintosh-Computerclients und mobile Geräteclients, die Sie bei Configuration Manager registrieren, erfordern für die Clientinstallation immer einen Verwaltungspunkt. Dieser Verwaltungspunkt muss sich an einem primären Standort befinden, für die Unterstützung mobiler Geräte konfiguriert sein und Clientverbindungen über das Internet akzeptieren. Für diese Clients können keine Verwaltungspunkte an sekundären Standorten verwendet werden, und es kann keine Verbindung mit Verwaltungspunkten an anderen primären Standorten hergestellt werden.  

##  <a name="determine-if-you-need-a-fallback-status-point"></a>Bestimmen, ob ein Fallbackstatuspunkt erforderlich ist  
 Sie können einen Fallbackstatuspunkt verwenden, um die Clientbereitstellung für Windows-Computer zu überwachen. Sie können auch die Windows-Computerclients ermitteln, die nicht verwaltet werden, weil die Kommunikation mit einem Verwaltungspunkt nicht möglich ist. Für Macintosh-Computer, mobile Geräte, die mithilfe von Configuration Manager registriert wurden, und mobile Geräte, die über den Exchange Server-Connector verwaltet werden, wird kein Fallbackstatuspunkt verwendet.  

 Ein Fallbackstatuspunkt ist nicht erforderlich, um Clientaktivität und Clientintegrität zu überwachen.  

 Die Kommunikation zwischen Fallbackstatuspunkt und Clients erfolgt immer über HTTP, wobei nicht authentifizierte Verbindungen verwendet und Daten im Klartext gesendet werden. Dadurch ist der Fallbackstatuspunkt insbesondere dann für Angriffe anfällig, wenn er in der internetbasierten Clientverwaltung verwendet wird. Sie können die Angriffsfläche verringern, indem Sie immer einen eigenen Server verwenden, der den Fallbackstatuspunkt ausführt, und auf diesem Server in einer Produktionsumgebung keine andere Standortsystemrollen installieren.  

 Installieren Sie einen Fallbackstatuspunkt, wenn Folgendes zutrifft:  

-   Sie möchten erreichen, dass Clientkommunikationsfehler von Windows-Computern auch dann an den Standort gesendet werden, wenn diese Clientcomputer nicht mit einem Verwaltungspunkt kommunizieren können.  

-   Sie möchten die Configuration Manager-Berichte zur Clientbereitstellung nutzen, in denen die vom Fallbackstatuspunkt gesendeten Daten angezeigt werden.  

-   Sie verfügen über einen dedizierten Server für diese Standortsystemrolle und haben zusätzliche Sicherheitsmaßnahmen zum Schutz des Servers vor Angreifern ergriffen.  

-   Die Vorteile der Verwendung eines Fallbackstatuspunkts überwiegen im Vergleich mit den Sicherheitsrisiken durch nicht authentifizierte Verbindungen und Klartextübertragungen über HTTP-Verkehr.  

 Verzichten Sie auf die Installation eines Fallbackstatuspunkts, wenn die Sicherheitsrisiken der Ausführung einer Website mit nicht authentifizierten Verbindungen und Klartextübertragungen im Vergleich zu den Vorteilen der Identifizierung von Problemen bei der Clientkommunikation überwiegen.  

##  <a name="determine-whether-you-need-a-reporting-services-point"></a>Bestimmen, ob ein Reporting Services-Punkt erforderlich ist  
 Mit Configuration Manager stehen viele Berichte zur Verfügung, mit denen Installation, Zuweisung und Verwaltung von Clients in der Configuration Manager-Konsole vereinfacht werden. Für einige Berichte zur Clientbereitstellung ist es erforderlich, dass Clients einem Fallbackstatuspunkt zugewiesen werden.  

 Obwohl die Berichte für die Clientbereitstellung nicht erforderlich sind und einige Bereitstellungsinformationen in der Configuration Manager-Konsole angezeigt sowie in ausführlicherer Form aus den Clientprotokolldateien abgerufen werden können, enthalten die Berichte wertvolle Informationen, die das Überwachen und die Problembehebung der Clientbereitstellung vereinfachen.  

##  <a name="determine-if-you-need-an-enrollment-point-and-an-enrollment-proxy-point"></a>Bestimmen, ob ein Anmeldungspunkt und ein Anmeldungsproxypunkt erforderlich sind  
 Für Configuration Manager sind der Anmeldungspunkt und der Anmeldungsproxypunkt erforderlich, um mobile Geräte und Zertifikate für Macintosh-Computer anzumelden. Diese Standortsystemrollen sind nicht erforderlich, wenn Sie mobile Geräte mit dem Exchange Server-Connector verwalten, den Legacyclient für mobile Geräte (z.B. für Windows CE) installieren oder das Clientzertifikat auf Macintosh-Computern unabhängig von Configuration Manager anfordern und installieren.  

##  <a name="determine-if-you-need-a-distribution-point"></a>Ermitteln, ob ein Verteilungspunkt erforderlich ist  
 Für die Installation von Configuration Manager-Clients auf Windows-Computern ist kein Verteilungspunkt erforderlich. In Configuration Manager wird jedoch standardmäßig ein Verteilungspunkt verwendet, um die Clientquelldateien auf Windows-Computern zu installieren. Es ist jedoch auch möglich, diese Dateien von einem Verwaltungspunkt herunterzuladen. Verteilungspunkte werden nicht verwendet, um Clients für mobile Geräte zu installieren, die mithilfe von Configuration Manager angemeldet wurden. Sie werden allerdings bei der Installation des Legacyclients für mobile Geräte verwendet. Wenn Sie den Configuration Manager-Client im Rahmen einer Betriebssystembereitstellung installieren, wird das Betriebssystem auf einem Verteilungspunkt gespeichert und von dort abgerufen.  

 Obwohl Verteilungspunkte für die Installation der meisten Configuration Manager-Clients nicht erforderlich sind, benötigen Sie sie, um Software wie Anwendungen und Softwareupdates auf den Clients zu installieren.  

##  <a name="determine-if-you-need-an-application-catalog-website-point-and-an-application-catalog-web-services-point"></a>Bestimmen, ob ein Anwendungskatalog-Websitepunkt und ein Anwendungskatalog-Webdienstpunkt erforderlich sind  
 Der Anwendungskatalog-Websitepunkt und der Anwendungskatalog-Webdienstpunkt sind für die Clientbereitstellung nicht erforderlich. Allerdings kann es dennoch sinnvoll sein, sie im Rahmen der Clientbereitstellung zu installieren, damit Benutzer nach der Installation des Configuration Manager-Clients auf Windows-Computern die folgenden Aktionen ausführen können:  

-   Zurücksetzen mobiler Geräte  

-   Suchen und Installieren von Anwendungen aus dem Anwendungskatalog  

-   Bereitstellen von Anwendungen für Benutzer und Geräte mit dem Bereitstellungszweck **Verfügbar**  

##  <a name="determine-whether-you-require-a-cloud-management-gateway-connector-point"></a>Bestimmen, ob ein Cloudverwaltungsgateway-Connectorpunkt erforderlich ist 

Ein Cloudverwaltungsgateway-Connectorpunkt ist erforderlich, wenn Sie ein [Cloudverwaltungsgateway](/sccm/core/clients/manage/setup-cloud-management-gateway) zum [Verwalten von Clients im Internet](/sccm/core/clients/manage/manage-clients-internet) einrichten.


 