---
title: "System Center Configuration Manager-Datenschutzbestimmungen – Zusatzinformationen | Microsoft-Dokumentation"
description: "Erfahren Sie mehr darüber, wie Microsoft Daten aus einer Bereitstellung von System Center Configuration Manager sammelt und verwendet."
ms.custom: na
ms.date: 12/30/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1fcc921f-085f-4b0b-9c53-1e0707211076
caps.latest.revision: "5"
caps.handback.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
translation.priority.ht:
- cs-cz
- de-de
- en-gb
- es-es
- fr-fr
- hu-hu
- it-it
- ja-jp
- ko-kr
- nl-nl
- pl-pl
- pt-br
- pt-pt
- ru-ru
- sv-se
- tr-tr
- zh-cn
- zh-tw
ms.openlocfilehash: ef7b3656f9b4a31e07227aa4e864448d0dd1fcdc
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="additional-information-about-privacy-for-system-center-configuration-manager"></a>Weitere Informationen zum Datenschutz für System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*


## <a name="updates-and-servicing"></a>Updates und Wartung
System Center Configuration Manager führt ein neues Updatemodell ein, das Sie beim Beibehalten des aktuellen Stands Ihrer Configuration Manager-Bereitstellung mit den neuesten Updates und Features unterstützt. Wenn dieses Feature installiert ist, fügt es eine neue Standortsystemrolle, den Dienstverbindungspunkt, auf einem Standortserver hinzu, den ein Administrator ausgewählt hat. Weitere Einzelheiten dazu, welche Informationen gesammelt und wie diese verwendet werden, finden Sie im Abschnitt „Nutzungsdaten“ in diesem Artikel.


## <a name="usage-data"></a>Nutzungsdaten
System Center Configuration Manager sammelt Diagnose- und Nutzungsdaten über sich selbst, mit deren Hilfe Microsoft Anwendungsinstallation, Qualität und Sicherheit künftiger Releases verbessert.
Diagnose- und Nutzungsdaten sind für jede System Center Configuration Manager-Hierarchie aktiviert. Sie bestehen aus SQL Server-Abfragen, die wöchentlich an jedem primären Standort und am Standort der zentralen Verwaltung ausgeführt werden. Wenn die Hierarchie einen Standort der zentralen Verwaltung verwendet, werden die Daten von primären Standorten dann an diesen Standort repliziert. Am obersten Standort Ihrer Hierarchie sendet der Dienstverbindungspunkt diese Informationen, wenn er prüft, ob Updates vorhanden sind. Wenn sich der Dienstverbindungspunkt im Offlinemodus befindet, werden die Informationen mithilfe des Dienstverbindungstools übertragen.

Configuration Manager sammelt Daten nur von der SQL Server-Datenbank des Standorts und nicht direkt von Clients oder Standortservern.

Administratoren können die Ebene der Datensammlung in der Einstellung **Nutzungsdaten** der Configuration Manager-Konsole ändern.

Weitere Informationen finden Sie in den „Erfahren Sie mehr“-Artikeln zu Ebenen und Einstellungen für Nutzungsdaten im Artikel [Diagnose- und Nutzungsdaten für System Center Configuration Manager](http://go.microsoft.com/fwlink/?LinkID=626566).


## <a name="customer-experience-improvement-program"></a>Programm zur Verbesserung der Benutzerfreundlichkeit
Das Programm zur Verbesserung der Benutzerfreundlichkeit (Customer Experience Improvement Program, CEIP) sammelt über die Configuration Manager-Konsole Informationen zu Ihrer Hardwarekonfiguration sowie Ihrer Verwendung unserer Software und unserer Dienste, um Trends und Gebrauchsmuster zu identifizieren. Das CEIP erfasst zudem den Typ und die Anzahl der auftretenden Fehler, die Software- und Hardwareleistung sowie die Geschwindigkeit der Dienste. Ihr Name, Ihre Adresse oder andere Kontaktdaten werden nicht erfasst. Es werden keine CEIP-Daten von Client-Computern gesammelt.

Wir verwenden diese Informationen, um die Qualität, Zuverlässigkeit und Leistung von Microsoft-Software und -Diensten zu verbessern.

Weitere Informationen zu den Daten, die das CEIP sammelt, verarbeitet oder überträgt, finden Sie in der [Datenschutzerklärung zum Microsoft-Programm zur Verbesserung der Benutzerfreundlichkeit](http://go.microsoft.com/fwlink/?LinkID=525211).

## <a name="operations-management-suite-connector"></a>Operations Management Suite-Connector
Der Microsoft Operations Management Suite-Connector synchronisiert Daten, z.B. Sammlungen, von System Center Configuration Manager und Microsoft Operations Management Suite. Die Microsoft Azure-Abonnement-ID und der geheime Schlüssel werden in der Configuration Manager-Datenbank gespeichert, wenn ein Administrator die Funktion konfiguriert. Sowohl der Azure Active Directory-Clientschlüssel als auch der gemeinsam verwendete Schlüssel des Microsoft Operations Management Suite-Arbeitsbereichs werden in der lokalen System Center Configuration Manager-Datenbank gespeichert. Die gesamte Kommunikation zwischen System Center Configuration Manager und Microsoft Operations Management Suite verwendet HTTPS. Außer zufälligen Telemetriedaten werden Microsoft keine zusätzlichen Informationen über die Sammlungen zur Verfügung gestellt. Einzelheiten zu den Informationen, die Microsoft Operations Management Suite sammelt, finden Sie unter [Log Analytics-Datensicherheit](http://go.microsoft.com/fwlink/?LinkId=823545).

## <a name="asset-intelligence"></a>Asset Intelligence
Mit Asset Intelligence können IT-Administratoren die Konformität mit Konfigurationsstandards definieren, nachverfolgen und proaktiv verwalten. Durch Messungen und Berichterstattung zu Bereitstellung und Verwendung sowohl physischer als auch virtueller Anwendungen werden den Organisationen gute Geschäftsentscheidungen zur Softwarelizenzierung und die Einhaltung von Lizenzverträgen erleichtert. Nach dem Sammeln von Nutzungsdaten von Configuration Manager-Clients stehen Administratoren verschiedene Features zur Verfügung, mit denen sie die Daten, einschließlich Sammlungen, Abfragen und Berichte, anzeigen können.

Bei jeder Synchronisierung wird ein Katalog bekannter Software von Microsoft heruntergeladen. IT-Administratoren können wahlweise Informationen über nicht kategorisierte Softwaretitel, die in ihrer Organisation gefunden wurden, an Microsoft senden, um entsprechende Recherchen durchzuführen und die Informationen dem Katalog hinzuzufügen. Vor dem Hochladen dieser Informationen werden in einem Dialogfeld die Daten angezeigt, die hochgeladen werden sollen. Hochgeladene Daten können nicht zurückgerufen werden. Von Asset Intelligence werden keine Benutzer-, Computer oder Lizenzverwendungsinformationen an Microsoft gesendet.

Nachdem ein Softwaretitel hochgeladen wurde, können die Microsoft-Mitarbeiter diesen identifizieren und kategorisieren und danach dieses Wissen allen anderen Kunden, die dieses Feature verwenden, sowie anderen Kunden des Katalogs zur Verfügung stellen. Alle hochgeladenen Softwaretitel werden öffentlich. Die Anwendung und ihre Kategorisierung werden Teil des Katalogs und können für andere Kunden des Katalogs heruntergeladen werden. Berücksichtigen Sie beim Konfigurieren der Asset Intelligence-Datensammlung und bei der Entscheidung, ob Informationen an System Center Online übermittelt werden sollen, die Datenschutzanforderungen Ihrer Organisation.

Asset Intelligence ist in System Center Configuration Manager standardmäßig nicht aktiviert. Nicht kategorisierte Titel werden nie automatisch hochgeladen. Im System kann dieser Task auch nicht automatisiert werden. Sie müssen den Upload jedes Softwaretitels manuell auswählen und genehmigen.

## <a name="endpoint-protection"></a>Endpoint Protection
Microsoft Cloud Protection Service wurde früher als Microsoft Active Protection Service oder MAPS bezeichnet.
Die relevanten Produkte sind System Center Endpoint Protection und das Endpoint Protection-Feature von System Center Configuration Manager (für die Verwaltung von System Center Endpoint Protection und Windows Defender für Windows 10). Diese Funktion ist für System Center Endpoint Protection für Linux oder System Center Endpoint Protection für Mac nicht implementiert.

Die Microsoft Cloud Protection Service-Antimalware-Community ist eine freiwillige weltweite Online-Community, die System Center Endpoint Protection-Benutzer umfasst. Wenn Sie Microsoft Cloud Protection Service beitreten, sendet System Center Endpoint Protection automatisch Informationen an Microsoft. Anhand dieser Informationen bestimmt Microsoft die Software, die auf mögliche Bedrohungen prüft und zur Verbesserung der Effektivität von System Center Endpoint Protection beiträgt. Diese Community hilft bei der Eindämmung neuer Infektionen mit Schadsoftware. Wenn ein Microsoft Cloud Protection Service-Bericht Details zu Schadsoftware oder potenziell unerwünschter Software enthält, die möglicherweise vom Endpoint Protection-Client entfernt werden kann, lädt Microsoft Cloud Protection Service die jüngste Signatur herunter, um für Abhilfe zu sorgen. Von Microsoft Cloud Protection Service werden auch „falsch positive Ergebnisse“ ermittelt (ein Element wurde ursprünglich als Schadsoftware identifiziert, obwohl es keine war) und behoben.

Microsoft Cloud Protection Service-Berichte enthalten Informationen zu potenziellen Schadsoftwaredateien, wie z.B. Dateinamen, kryptografische Hashwerte, Anbieter, Größe und Datumsstempel. Darüber hinaus sammelt Microsoft Cloud Protection Service möglicherweise vollständige URLs, um den Ursprung der Datei anzugeben. Die URLs können gelegentlich persönliche Informationen wie Suchbegriffe oder in Formularen eingegebene Daten enthalten. Berichte können auch die Aktionen enthalten, die Sie vorgenommen haben, wenn Endpoint Protection Sie über unerwünschte Software informiert hat. Microsoft Cloud Protection Service-Berichte enthalten diese Informationen, damit Microsoft beurteilen kann, wie effektiv Endpoint Protection Malware und potenziell unerwünschte Software erkennen und entfernen kann und versuchen kann, neue Malware zu identifizieren.

Sie können Microsoft Cloud Protection Service beitreten, wenn Sie eine einfache Mitgliedschaft oder eine Premiummitgliedschaft besitzen. In einfachen Mitgliederberichten sind die oben beschriebenen Informationen enthalten. Premiummitgliederberichte sind umfangreicher und können zusätzliche Details über die von Endpoint Protection erkannte Software enthalten, darunter den Speicherort der Software, Dateinamen, die Funktionsweise der Software sowie deren Auswirkungen auf den Computer. Anhand dieser Berichte und der Berichte anderer Endpoint Protection-Benutzer, die an Microsoft Cloud Protection Service teilnehmen, können Microsoft-Mitarbeiter neue Bedrohungen schneller erkennen. Anschließend werden Schadsoftwaredefinitionen für Programme erstellt, die den Analysekriterien entsprechen, und als aktualisierte Definitionen allen Benutzern über Microsoft Update zugänglich gemacht.

Zur besseren Erkennung und Behebung bestimmter Infektionen mit Schadsoftware sendet das Produkt regelmäßig Informationen zum Sicherheitszustand des PCs an Microsoft Cloud Protection Service. Diese Informationen umfassen Details zu den Sicherheitseinstellungen des PCs sowie Protokolldateien, in denen die Treiber und andere Software beschrieben sind, die beim Starten des PCs geladen werden.
Eine Nummer, die Ihren PC eindeutig identifiziert, wird ebenfalls gesendet. Möglicherweise werden von Microsoft Cloud Protection Service die IP-Adressen gesammelt, mit denen die potenziellen Schadsoftwaredateien eine Verbindung herstellen.

Microsoft Cloud Protection Service-Berichte werden zur Verbesserung der Softwareprodukte und Dienste von Microsoft verwendet. Die Berichte können außerdem zu Statistik-, Test- oder Analysezwecken sowie zur Erstellung von Definitionen verwendet werden. Nur Mitarbeiter, Auftragnehmer, Partner und Lieferanten von Microsoft, die diese Berichte für ihre Arbeit benötigen, erhalten Zugriff darauf.

Die Erfassung persönlicher Informationen durch Microsoft Cloud Protection Service erfolgt nicht absichtlich. Die von Microsoft Cloud Protection Service unbeabsichtigt erfassten persönlichen Informationen werden von Microsoft nicht verwendet, um Sie zu identifizieren oder zu kontaktieren.

Weitere Einzelheiten zu den gesammelten Daten finden Sie in der Produktdokumentation unter [Endpoint Protection in System Center Configuration Manager](http://go.microsoft.com/fwlink/?LinkId=823547).

## <a name="site-hierarchy--geographical-view-with-bing-maps"></a>Standorthierarchie – geografische Ansicht mit Bing Maps
Mit „Standorthierarchie – geografische Ansicht“ können Sie die physische Configuration Manager-Servertopologie mithilfe von Karten anzeigen, die von Microsoft Bing Maps bereitgestellt werden. Zum Aktivieren dieses Features werden von Ihnen bereitgestellte Standortinformationen von Ihrem Server an den Webdienst Bing Maps übertragen.

Microsoft verwendet die Informationen, um Microsoft Bing Maps sowie andere Websites und Dienste zu betreiben und zu verbessern. Weitere Informationen finden Sie in der [Datenschutzerklärung von Microsoft](http://go.microsoft.com/fwlink/?LinkId=823548).
Sie haben die Wahl, die geografische Ansicht der Standorthierarchie nicht zu verwenden. Die Hierarchiediagrammansicht ermöglicht Ihnen, die Hierarchie anzusehen, ohne den Dienst Bing Maps zu verwenden.

## <a name="microsoft-intune-subscription"></a>Microsoft Intune-Abonnement
Kunden, die ein Abonnement für Microsoft Intune gekauft haben, können Configuration Manager zum Verwalten ihrer über Microsoft Intune verbundenen mobilen Geräte verwenden. [Datenschutzbestimmungen für Microsoft Online Services](http://go.microsoft.com/fwlink/?LinkId=262214) gilt für die Microsoft Online Services, einschließlich Microsoft Intune. Wenn Kunden auch ein Microsoft Intune-Abonnement haben, sollte die [Onlinedatenschutzbestimmungen für Online Dienste von Microsoft ](http://go.microsoft.com/fwlink/?LinkId=262214) in Verbindung mit dieser Datenschutzerklärung gelesen werden.

Für die gesamte Microsoft Intune-Kommunikation wird HTTPS verwendet. Zum Konfigurieren des Microsoft Intune-Abonnements und Herunterladen der Zertifikatsignieranforderung (Certificate Signing Request, CSR), die für die Konfiguration der iOS-Unterstützung erforderlich ist, muss sich ein Administrator über ein Unternehmenskonto unter Angabe des dazugehörigen Kennworts bei Microsoft Intune anmelden. Die betreffenden Anmeldeinformationen werden nicht in Configuration Manager gespeichert. Die übrige Kommunikation mit Microsoft Intune wird über PKI-Zertifikate authentifiziert, die automatisch von Microsoft Intune generiert werden.

Zur Verwaltung von Geräten, die mit Microsoft Intune verbunden sind, werden bestimmte Informationen mit Microsoft Intune ausgetauscht. Zu diesen Informationen gehören der Benutzerprinzipalname (UPN) aller Benutzer, die dem Dienst zugewiesen wurden, sowie Inventarinformationen der Geräte, die von Microsoft Intune verwaltet werden. Metadaten (z.B. Anwendungsname, Herausgeber und Version) für Inhalte, die Manage.Microsoft.com-Verteilungspunkten zugewiesen wurden, werden an Microsoft Intune gesendet. Die einem Manage.Microsoft.com-Verteilungspunkt zugewiesenen eigentlichen Binärinhalte werden vor dem Hochladen an Microsoft Intune verschlüsselt.

Diese Option wird standardmäßig nicht konfiguriert. Administratoren steuern, welche Inhalte an Manage.microsoft.com-Verteilungspunkte übertragen und welche Benutzer dem Dienst zugewiesen werden. Das Feature kann jederzeit entfernt werden.
