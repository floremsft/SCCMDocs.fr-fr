---
title: "Einführung in Asset Intelligence | Microsoft-Dokumentation"
description: "Erhalten Sie eine Einführung in Asset Intelligence in System Center Configuration Manager."
ms.custom: na
ms.date: 2/22/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 0bdfdef5-390f-4099-8bde-de51d9a89175
caps.latest.revision: "7"
caps.handback.revision: "0"
author: andredm7
ms.author: andredm
manager: angrobe
ms.openlocfilehash: 879dc3f04f361af955afbc4db180d097073e8d41
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="introduction-to-asset-intelligence-in-system-center-configuration-manager"></a>Einführung in Asset Intelligence in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Mit Asset Intelligence in System Center Configuration Manager können Sie die Softwarelizenzverwendung im gesamten Unternehmen mithilfe des Asset Intelligence-Katalogs verwalten und inventarisieren. Mit vielen Hardwareinventur-WMI-Klassen (Windows-Verwaltungsinstrumentation) wird der Umfang der Informationen, die zu verwendeten Hardware- und Softwaretiteln gesammelt werden, verbessert. Diese Informationen werden durch mehr als 60 Berichte in einem einfach zu verwendenden Format dargestellt. Viele dieser Berichte sind mit detaillierteren Berichten verknüpft, sodass Sie allgemeine Informationen abfragen und dann per Drilldown ausführlichere Informationen anzeigen können. Sie können benutzerdefinierte Informationen wie Softwarekategorien, Softwarefamilien, Softwarebezeichnungen und Hardwareanforderungen zum Asset Intelligence-Katalog hinzufügen. Darüber hinaus können Sie eine Verbindung zu System Center Online herstellen, um den Asset Intelligence-Katalog mit den neuesten verfügbaren Informationen zu aktualisieren. Microsoft-Kunden können die Verwendung von Unternehmenssoftwarelizenzen mit erworbenen Softwarelizenzen abstimmen, die verwendet werden, indem Softwarelizenzinformationen in die Configuration Manager-Standortdatenbank importiert werden.  

##  <a name="BKMK_AssetIntelligenceCatalog"></a> Asset Intelligence-Katalog  

 Der Asset Intelligence-Katalog in Configuration Manager besteht aus in der Standortdatenbank gespeicherten Datenbanktabellen, in denen Kategorisierungs- und Identifikationsinformationen von über 300.000 Softwaretiteln und -versionen enthalten sind. Diese Datenbanktabellen werden auch verwendet, um die Hardwareanforderungen bestimmter Softwaretitel zu verwalten.  

 Der Asset Intelligence-Katalog bietet Softwarelizenzinformationen für verwendete Softwaretitel, sowohl für Software von Microsoft als auch von Drittanbietern. Der Asset Intelligence-Katalog enthält vordefinierte Hardwareanforderungen von Softwaretiteln, und Sie können auf Basis Ihrer individuellen Anforderungen neue benutzerdefinierte Hardwareanforderungsinformationen erstellen. Zusätzlich können Sie Informationen im Asset Intelligence-Katalog anpassen und Softwaretitelinformationen zur Kategorisierung an System Center Online hochladen.  

 Asset Intelligence-Katalogupdates, die neu veröffentlichten Software umfassen, können in regelmäßigen Abständen heruntergeladen werden, um Massenkatalogupdates auszuführen. Der Katalog kann mit der Standortsystemrolle "Asset Intelligence-Synchronisierungspunkt" auch dynamisch aktualisiert werden.  

###  <a name="BKMK_SoftwareCategories"></a> Softwarekategorien  
 Asset Intelligence-Softwarekategorien werden zur groben Kategorisierung inventarisierter Softwaretitel verwendet sowie zum allgemeinen Gruppieren von spezifischeren Softwarefamilien. Eine Softwarekategorie könnte beispielsweise ein Energieversorgungsunternehmen sein und eine Softwarefamilie innerhalb dieser Softwarekategorie beispielsweise Öl und Gas oder Wasserenergie. Viele Softwarekategorien sind im Asset Intelligence-Katalog vordefiniert. Es können außerdem benutzerdefinierte Kategorien hinzugefügt werden, um die inventarisierte Software zusätzlich zu definieren. Der Überprüfungszustand aller vordefinierten Softwarekategorien lautet immer **Überprüft**, während dem Asset Intelligence-Katalog hinzugefügte benutzerdefinierte Softwarekategorieinformationen als **Benutzerdefiniert**angegeben werden. Weitere Informationen zum Verwalten von Softwarekategorien finden Sie unter [Konfigurieren von Asset Intelligence in System Center Configuration Manager](../../../../core/clients/manage/asset-intelligence/configuring-asset-intelligence.md).  

> [!NOTE]  
>  Vordefinierte Softwarekategorieinformationen, die im Asset Intelligence-Katalog gespeichert sind, sind schreibgeschützt und können nicht geändert oder gelöscht werden. Administratoren können benutzerdefinierte Softwarekategorien hinzufügen, ändern und löschen.  

###  <a name="BKMK_SoftwareFamilies"></a> Softwarefamilien  
 Mithilfe von Asset Intelligence-Softwarefamilien werden inventarisierte Softwaretitel innerhalb von Softwarekategorien definiert. Viele Softwarefamilien sind im Asset Intelligence-Katalog vordefiniert. Es können außerdem benutzerdefinierte Kategorien hinzugefügt werden, um die inventarisierte Software zusätzlich zu definieren. Der Überprüfungszustand aller vordefinierten Softwarefamilien lautet immer **Überprüft**, während dem Asset Intelligence-Katalog hinzugefügte benutzerdefinierte Softwarefamilien als **Benutzerdefiniert**angegeben werden. Weitere Informationen zum Verwalten von Softwarefamilien finden Sie unter [Konfigurieren von Asset Intelligence in System Center Configuration Manager](../../../../core/clients/manage/asset-intelligence/configuring-asset-intelligence.md).  

> [!NOTE]  
>  Vordefinierte Softwarefamilieninformationen sind schreibgeschützt und können nicht geändert werden. Administratoren können benutzerdefinierte Softwarefamilien hinzufügen, ändern und löschen.  

###  <a name="BKMK_CustomLabels"></a> Softwarebezeichnungen  
 Mit benutzerdefinierten Softwarebezeichnungen können Sie in Asset Intelligence Filter zum Gruppieren von Softwaretiteln und zum Anzeigen der Softwaretitel in Asset Intelligence-Berichten erstellen. Sie können Softwarebezeichnungen zum Erstellen benutzerdefinierter Gruppen von Softwaretiteln mit einem gemeinsamen Attribut verwenden. Beispielsweise können Sie die Softwarebezeichnung "Shareware" erstellen und mit den inventarisierten Sharewaretiteln verknüpfen und anschließend einen Bericht ausführen, in dem alle der Softwarebezeichnung "Shareware" zugeordneten Softwaretitel aufgeführt werden. Softwarebezeichnungen sind nicht vordefiniert. Der Überprüfungszustand für Softwarebezeichnungen ist immer **Benutzerdefiniert**. Weitere Informationen zum Verwalten von Softwarebezeichnungen finden Sie unter [Konfigurieren von Asset Intelligence in System Center Configuration Manager](../../../../core/clients/manage/asset-intelligence/configuring-asset-intelligence.md).  

###  <a name="BKMK_HardwareRequirements"></a> Hardwareanforderungen  
 Mithilfe von Hardwareanforderungen kann überprüft werden, ob Computer die Hardwareanforderungen für Softwaretitel erfüllen, bevor auf ihnen Softwarebereitstellungen vorgenommen werden. Die Hardwareanforderungen für Softwaretitel können im Arbeitsbereich **Bestand und Kompatibilität** im Knoten **Hardwareanforderungen** unter dem Knoten **Asset Intelligence** verwaltet werden. Viele Hardwareanforderungen sind im Asset Intelligence-Katalog vordefiniert, und es können neue benutzerdefinierte Hardwareanforderungsinformationen erstellt werden, um benutzerdefinierten Anforderungen zu entsprechen. Der Überprüfungszustand aller vordefinierten Hardwareanforderungen lautet immer **Überprüft**, während dem Asset Intelligence-Katalog hinzugefügte benutzerdefinierte Hardwareanforderungen als **Benutzerdefiniert**angegeben werden. Weitere Informationen zum Verwalten von Hardwareanforderungen finden Sie unter [Konfigurieren von Asset Intelligence in System Center Configuration Manager](../../../../core/clients/manage/asset-intelligence/configuring-asset-intelligence.md).  

> [!NOTE]  
>  Die in der Configuration Manager-Konsole angezeigten Hardwareanforderungen werden vom Asset Intelligence-Katalog abgerufen und basieren nicht auf inventarisierten Informationen zu Softwaretiteln von System Center 2012 Configuration Manager-Clients. Die Hardwareanforderungsinformationen werden nicht als Teil der Synchronisierung mit System Center Online aktualisiert. Sie können benutzerdefinierte Hardwareanforderungen für inventarisierte Software erstellen, der keine Hardwareanforderungen zugeordnet sind.  

 In der Standardeinstellung werden für jede aufgeführte Hardwareanforderung die folgenden Informationen angezeigt:  

-   **Softwaretitel**: Gibt den Softwaretitel an, der der Hardwareanforderungen zugeordnet ist.  

-   **Mindesttaktfrequenz der CPU (MHz)**: Gibt die Mindestprozessorgeschwindigkeit in Megahertz (MHz) an, die vom Softwaretitel benötigt wird.  

-   **Mindestgröße des RAM (KB)**: Gibt die Mindestgröße des Arbeitsspeichers in Kilobytes (KB) an, die vom Softwaretitel benötigt wird.  

-   **Mindestspeicherplatz auf dem Datenträger (KB)**: Gibt den freien Mindestspeicherplatz auf der Festplatte in KB an, der vom Softwaretitel benötigt wird.  

-   **Mindestgröße des Datenträgers (KB)**: Gibt die für den Softwaretitel erforderliche Mindestgröße des Festplattenspeicherplatzes in KB an.  

-   **Überprüfungszustand**: Gibt den Überprüfungszustand für die Hardwareanforderung an.  

 Im Asset Intelligence-Katalog gespeicherte vordefinierte Hardwareanforderungen sind schreibgeschützt und können nicht gelöscht werden.  Administratoren können benutzerdefinierte Hardwareanforderungen für Softwaretitel hinzufügen, ändern und löschen, welche nicht im Asset Intelligence-Katalog gespeichert sind.  

##  <a name="BKMK_InventoriedSoftwareTitles"></a> Inventarisierte Softwaretitel  
 Die inventarisierten Softwaretitelinformationen können im Arbeitsbereich **Bestand und Kompatibilität** im Knoten **Inventarisierte Software** unter dem Knoten **Asset Intelligence** angezeigt werden. Die inventarisierten Softwareinformationen werden vom Hardwareinventurclient-Agent von Configuration Manager-Clients auf Basis der Softwaretitel gesammelt, welche im Asset Intelligence-Katalog gespeichert sind.  

> [!WARNING]  
>  Vom Hardwareinventurclient-Agent werden Inventurdaten auf Basis der aktivierten Berichtsklassen der Asset Intelligence-Hardwareinventur gesammelt. Weitere Informationen zum Aktivieren von Berichterstellungsklassen finden Sie unter [Konfigurieren von Asset Intelligence in System Center Configuration Manager](../../../../core/clients/manage/asset-intelligence/configuring-asset-intelligence.md).  

 In der Standardeinstellung werden für jeden inventarisierten Softwaretitel die folgenden Informationen angezeigt:  

-   **Name**: Gibt den Namen des inventarisierten Softwaretitels an.  

-   **Hersteller**: Gibt den Namen des Herstellers an, der den inventarisierten Softwaretitel entwickelt hat.  

-   **Version**: Gibt die Produktversion des inventarisierten Softwaretitels an.  

-   **Kategorie**: Gibt die Softwarekategorie an, die dem inventarisierten Softwaretitel derzeit zugewiesen ist.  

-   **Familie**: Gibt die Softwarefamilie an, die dem inventarisierten Softwaretitel derzeit zugewiesen ist.  

-   **Bezeichnung** [**1**, **2**und **3**]: Gibt die benutzerdefinierten Bezeichnungen an, die dem Softwaretitel zugeordnet sind. Inventarisierten Softwaretiteln können bis zu drei benutzerdefinierte Bezeichnungen zugeordnet sein.  

-   **Anzahl**: Gibt die Anzahl der Configuration Manager-Clients an, bei denen der Softwaretitel inventarisiert ist.  

-   **Status**: Gibt den Überprüfungszustand für den inventarisierten Softwaretitel an.  

> [!NOTE]  
>  Die Kategorisierungsinformationen (Produktname, Hersteller, Softwarekategorie und Softwarefamilie) können bei inventarisierter Software nur am Standort der obersten Ebene der Hierarchie geändert werden. Wenn Kategorisierungsinformationen für vordefinierte Software geändert werden, wird der Überprüfungszustand für die Software von **Überprüft** auf **Benutzerdefiniert**geändert.  

##  <a name="AssetIntelligenceSycnronizationPoint"></a> Asset Intelligence-Synchronisierungspunkt  
 Beim Asset Intelligence-Synchronisierungspunkt handelt es sich um eine Configuration Manager-Standortsystemrolle, die verwendet wird, um über TCP-Port 443 eine Verbindung mit System Center Online herzustellen und dynamische Updates von Asset Intelligence-Kataloginformationen zu verwalten. Diese Standortrolle kann nur am Standort der obersten Ebene der Hierarchie installiert werden. Sie müssen alle Asset Intelligence-Kataloganpassungen unter Verwendung einer mit dem Standort der obersten Ebene verbundenen Configuration Manager-Konsole konfigurieren. Alle Updates müssen zwar am Standort der obersten Ebene konfiguriert werden, Asset Intelligence-Kataloginformationen werden jedoch auf andere Standorte in der Hierarchie repliziert. Unter Verwendung der Standortrolle des Asset Intelligence-Synchronisierungspunkts können außerplanmäßige Katalogsynchronisierungen mit System Center Online angefordert oder eine automatische Katalogsynchronisierung geplant werden. Zusätzlich zum Herunterladen neuer Asset Intelligence-Kataloginformationen können vom Asset Intelligence-Synchronisierungspunkt Informationen zu benutzerdefinierten Softwaretiteln zur Kategorisierung in System Center Online hochgeladen werden. Microsoft behandelt alle Softwaretitel, die zur Kategorisierung in System Center Online hochgeladen wurden, als öffentliche Informationen. Achten Sie daher darauf, dass Ihre benutzerdefinierten Softwaretitel keine vertraulichen oder proprietären Informationen enthalten.  

> [!NOTE]  
>  Nach der Übermittlung eines nicht kategorisierten Softwaretitels identifizieren und kategorisieren Entwicklungsmitarbeiter von System Center Online den Softwaretitel und stellen die Informationen zur Softwaretitelkategorisierung dann für alle Kunden zur Verfügung, die den Onlinedienst verwenden. Voraussetzung ist, dass mindestens vier Kategorisierungsanforderungen von Kunden für diesen Softwaretitel vorliegen. Die Softwaretitel, für die die meisten Kategorisierungsanforderungen vorliegen, werden bei der Kategorisierung am höchsten priorisiert. Benutzerdefinierte Software und Branchenanwendungen erhalten i. d. R. keine Kategorie. Es empfiehlt sich daher, diese Softwaretitel nicht zur Kategorisierung an Microsoft zu senden.  

> [!NOTE]  
>  Damit eine Verbindung mit System Center Online hergestellt werden kann, muss dem Asset Intelligence-Synchronisierungspunkt eine Standortsystemrolle zugewiesen sein. Weitere Informationen zum Installieren eines Asset Intelligence-Synchronisierungspunkts finden Sie im Abschnitt [Konfigurieren von Asset Intelligence in System Center Configuration Manager](../../../../core/clients/manage/asset-intelligence/configuring-asset-intelligence.md).  

##  <a name="BKMK_AssetIntelligenceHomePage"></a> Asset Intelligence-Startseite  
 Der Knoten **Asset Intelligence** im Arbeitsbereich **Bestand und Kompatibilität** dient als Startseite für Asset Intelligence in Configuration Manager. Auf der **Asset Intelligence** -Startseite wird eine Zusammenfassung von Asset Intelligence-Kataloginformationen angezeigt.  

> [!NOTE]  
>  Die **Asset Intelligence** -Startseite wird während der Anzeige nicht automatisch aktualisiert.  

 Auf der **Asset Intelligence** -Startseite sind die folgenden Bereiche enthalten:  

-   **Katalogsynchronisierung**: Enthält Informationen darüber, ob Asset Intelligence aktiviert ist, und gibt den aktuellen Status des Asset Intelligence-Synchronisierungspunkts an. Der Abschnitt enthält zudem den Synchronisierungszeitplan und folgende Informationen: Ob die Kundenlizenzzusammenfassung importiert wird, wann der Status zuletzt aktualisiert wurde, den Zeitpunkt des nächsten geplanten Updates und die Anzahl der vorgenommenen Änderungen seit der Installation der Asset Intelligence-Synchronisierungspunkt-Standortsystems.  

    > [!NOTE]  
    >  Der Synchronisierungsabschnitt des Asset Intelligence-Katalogs auf der **Asset Intelligence** -Startseite wird nur angezeigt, wenn eine Asset Intelligence-Synchronisierungspunkt-Standortsystemrolle installiert wurde.  

-   **Status für inventarisierte Software**: Enthält die Anzahl und den Prozentsatz inventarisierter Software, Softwarekategorien und Softwarefamilien, die von Microsoft oder einem Administrator identifiziert wurden, deren Onlineidentifikation aussteht oder die nicht identifiziert sind und deren Onlineidentifikation nicht ausstehend ist. Die Informationen im Tabellenformat repräsentieren die jeweilige Anzahl, die Informationen im Diagramm den jeweiligen Prozentsatz.  

##  <a name="BKMK_AssetIntelligenceReports"></a> Asset Intelligence-Berichte  
 Sie finden die Asset Intelligence-Berichte in der Configuration Manager-Konsole im Arbeitsbereich **Überwachung** im Ordner „Asset Intelligence“ im Knoten **Berichterstattung**. Die Berichte enthalten Informationen zu Hardware, Lizenzverwaltung und Software. Weitere Informationen zu Berichten in Configuration Manager finden Sie unter [Berichterstellung in System Center Configuration Manager](../../../../core/servers/manage/reporting.md).  

> [!NOTE]  
>  Mit welcher Genauigkeit die Anzahl installierter Softwaretitel und Lizenzinformationen in den Asset Intelligence-Berichten angegeben werden, kann zwischen der tatsächlichen Anzahl installierter Softwaretitel oder den in der Umgebung verwendeten Lizenzen variieren. Diese Variation ist auf die komplexen Abhängigkeiten und Einschränkungen bei der Inventarisierung von Softwarelizenzinformationen für Softwaretitel zurückzuführen, die in Unternehmensumgebungen installiert sind. Die Asset Intelligence-Berichte dürfen bei der Prüfung der erworbenen Softwarelizenzen nicht als alleinige Quelle herangezogen werden.  

###  <a name="BKMK_HardwareReports"></a> Asset Intelligence-Hardwareberichte  
 Asset Intelligence-Hardwareberichte enthalten Informationen zum Hardwarebestand in der Organisation. Auf der Basis von Informationen zum Hardwareinventar (Prozessorgeschwindigkeit, Speicher, Peripheriegeräte usw.) können in Asset Intelligence-Hardwareberichten Informationen zu USB-Geräten, zu upgradebedürftiger Hardware und sogar zu Computern, die für ein bestimmtes Softwareupgrade nicht bereit sind, angezeigt werden.  

> [!NOTE]  
>  Einige Benutzerdaten in den Asset Intelligence-Hardwareberichten werden dem Sicherheitsereignisprotokoll des Systems entnommen. Für eine erhöhte Genauigkeit der Berichte wird empfohlen, das Protokoll zu löschen, wenn ein Computer einem neuen Benutzer zugewiesen wird.  

###  <a name="BKMK_LicenseManagementReports"></a> Asset Intelligence-Lizenzverwaltungsberichte  
 Asset Intelligence-Lizenzverwaltungsberichte enthalten Daten über die verwendeten Lizenzen. Der Lizenzregisterbericht enthält installierte Microsoft-Anwendungen in einem der Microsoft-Lizenzübersicht (MLS) vergleichbaren Format. Dies bietet eine praktische Methode zur Abstimmung neuer und bereits vorhandener Lizenzen. Andere Lizenzverwaltungsberichte enthalten Informationen zu Computern, die als Server zum Ausführen des Schlüsselverwaltungsdiensts (Key Management Service, KMS) für Aktivierungsstatistiken des Betriebssystems fungieren.  

> [!IMPORTANT]  
>  Einige der Asset Intelligence-Berichte enthalten Informationen zur Funktion des KMS, einer Methode zum Verwalten der Volumenlizenzierung. Wenn kein KMS-Server implementiert wurde, werden von einigen Berichten möglicherweise keine Daten zurückgegeben. Weitere Informationen zum KMS finden Sie im [Microsoft TechNet](http://go.microsoft.com/fwlink/?linkid=3225), indem Sie nach "KMS" suchen.  

###  <a name="BKMK_SoftwareReports"></a> Asset Intelligence-Softwareberichte  
 Asset Intelligence-Softwareberichte enthalten Informationen zu Softwarefamilien, Softwarekategorien und bestimmten Softwaretiteln, die auf Computern in der Organisation installiert sind. Die Softwareberichte enthalten Informationen zu Browserhilfsobjekten, automatisch startender Software und mehr. Diese Berichte können zum Identifizieren von Adware, Spyware und anderer Schadsoftware sowie zum Identifizieren von Softwareredundanz verwendet werden, um den Softwarekauf und die Softwareunterstützung zu vereinfachen.  

###  <a name="BKMK_SoftwareIdTagReports"></a> Berichte zu Asset Intelligence-Softwarerkennungstags  
 Berichte zu Asset Intelligence-Softwarerkennungstags liefern Informationen zu Software, die ein mit ISO/IEC 19770-2 kompatibles Softwarekennungstag enthält. Softwarekennungstags stellen autoritative Informationen bereit, mit deren Hilfe die installierte Software identifiziert wird. Wenn Sie die Hardwareinventur-Berichterstellungsklasse „SMS_SoftwareTag“ aktivieren, sammelt Configuration Manager mithilfe von Softwareerkennungstags Informationen zur Software. Die folgenden Berichte stellen Informationen zur Software bereit:  

-   **Software 14A – Suche nach softwareerkennungstagfähiger Software**: Dieser Bericht gibt an, wie viel Software mit aktiviertem Softwareerkennungstag installiert ist.  

-   **Software 14B - Computer auf denen eine bestimmte softwareerkennungstagfähige Software installiert ist**: Dieser Bericht listet alle Computer auf, auf denen Software mit einem bestimmten, aktivierten Softwareerkennungstag installiert ist.  

-   **Software 14C - Installierte softwareerkennungstagfähige Software auf einem bestimmten Computer**: Dieser Bericht listet die gesamte installierte Software mit einem bestimmten, aktivierten Softwarerkennungstag auf einem bestimmten Computer auf.  

###  <a name="BKMK_ReportingLImitations"></a> Einschränkungen bei der Asset Intelligence-Berichterstattung  
 In Asset Intelligence-Berichten können große Mengen an Informationen zu installierten Softwaretiteln sowie erworbenen und verwendeten Softwarelizenzen zusammengestellt werden. Diese Berichte sollten jedoch bei der Prüfung der erworbenen Softwarelizenzen nicht als alleinige Quelle herangezogen werden.  

####  <a name="BKMK_ExampleDependencies"></a> Beispielabhängigkeiten  
 Die Genauigkeit, mit der die Anzahl installierter Softwaretitel und die Lizenzinformationen in den Asset Intelligence-Berichten angegeben ist, kann von den aktuellen, tatsächlich verwendeten Mengen abweichen. Diese Variation ist auf die komplexen Abhängigkeiten bei der Inventarisierung von Softwarelizenzinformationen für Softwaretitel zurückzuführen, die in Unternehmensumgebungen verwendet werden. Im Folgenden finden Sie Beispiele für Abhängigkeiten, die bei der Inventur installierter Software in Unternehmen unter Verwendung von Asset Intelligence auftreten und die Genauigkeit von Asset Intelligence-Berichten beeinflussen können:  

 **Abhängigkeiten bezüglich der Clienthardwareinventur**  
 Asset Intelligence-Berichte zu installierter Software basieren auf Daten, die von Configuration Manager-Clients durch die Erweiterung der Hardwareinventur zum Aktivieren der Asset Intelligence-Berichterstellung gesammelt wurden. Aufgrund dieser Abhängigkeit von der Hardwareinventurberichterstellung geben Asset Intelligence-Berichten nur Daten von Configuration Manager-Clients wieder, die Hardwareinventurprozesse erfolgreich mit den erforderlichen aktivierten Asset Intelligence-WMI-Berichterstellungsklassen abschließen. Darüber hinaus kann es bei der Datenberichterstattung zu einer Verzögerung mit Einfluss auf die Genauigkeit von Asset Intelligence-Berichten kommen, da die Hardwareinventurprozesse von Configuration Manager-Clients gemäß einem vom Administrator definierten Zeitplan ausgeführt werden. Beispielsweise kann ein inventarisierter lizenzierter Softwaretitel deinstalliert werden, nachdem der Client einen erfolgreichen Hardwareinventurzyklus abgeschlossen hat. Allerdings wird der Softwaretitel in Asset Intelligence-Berichten bis zum nächsten geplanten Hardwareinventur-Berichterstattungszyklus des Clients als installiert angezeigt.  

 **Abhängigkeiten bezüglich der Softwarepakete**  
 Da Asset Intelligence-Berichte auf Daten zu installierten Softwaretiteln basieren, die mit standardmäßigen Hardwareinventurprozessen des Configuration Manager-Clients gesammelt werden, kann es vorkommen, dass einige Daten zu Softwaretiteln nicht richtig erfasst werden. Beispielsweise können Asset Intelligence-Berichte aufgrund von Softwareinstallationen, die nicht den Standardinstallationsprozessen entsprechen oder die vor der Installation geändert wurden, Ungenauigkeiten enthalten.  

####  <a name="BKMK_LegalLimitations"></a> Rechtliche Einschränkungen  
 Die in Asset Intelligence-Berichten angezeigten Informationen unterliegen vielen Einschränkungen und dürfen nicht als rechtlicher, buchhaltungstechnischer oder professioneller Rat angesehen werden. Die mithilfe von Asset Intelligence-Berichten bereitgestellten Informationen dienen lediglich Informationszwecken und sollten bei der Prüfung der Softwarelizenzverwendung nicht als alleinige Quelle herangezogen werden.  

 Im Folgenden finden Sie Beispiele für Einschränkungen, die bei der Inventur der Verwendung installierter Software und Lizenzen in Unternehmen unter Verwendung von Asset Intelligence auftreten und die Genauigkeit von Asset Intelligence-Berichten beeinflussen könnten.  

 **Einschränkungen bezüglich der Anzahl der verwendeten Microsoft-Lizenzen**  
 -   Die Anzahl der verwendeten Microsoft-Softwarelizenzen basiert auf von Administratoren zur Verfügung gestellten Informationen und sollte aufmerksam geprüft werden, um sicherzustellen, dass die richtige Anzahl an Softwarelizenzen angegeben wird.  

-   Die gemeldete Anzahl der Microsoft-Softwarelizenzen umfasst nur Informationen zu Microsoft-Softwarelizenzen, die durch Volumenlizenzierungsprogramme erworben wurden. Informationen zu im Einzelhandel, durch OEMs oder über andere Vertriebskanäle für Softwarelizenzen erworbenen Lizenzen sind nicht enthalten.  

-   In den letzten 45 Tagen erworbene Softwarelizenzen sind in der gemeldeten Anzahl der Microsoft-Softwarelizenzen möglicherweise aufgrund der Anforderungen und Zeitpläne für die Berichterstellung durch Softwarehändler nicht inbegriffen.  

-   Übertragungen von Softwarelizenzen nach Unternehmenszusammenschlüssen oder -akquisitionen sind in der Anzahl der Microsoft-Softwarelizenzen ggf. nicht enthalten.  

-   Sonderbedingungen in Microsoft-Volumenlizenzierungsvereinbarungen haben eventuell Einfluss auf die Anzahl gemeldeter Softwarelizenzen und können daher einer zusätzlichen Prüfung durch einen Microsoft-Berater unterliegen.  

 **Einschränkungen bezüglich der Anzahl der installierten Softwaretitel**  
 Configuration Manager-Clients müssen die Hardwareinventur-Berichterstattungszyklen erfolgreich abschließen, damit die Anzahl installierter Softwaretitel in den Asset Intelligence-Berichten exakt wiedergegeben wird. Darüber hinaus kann es zwischen der Installation oder Deinstallation eines lizenzierten Softwaretitels nach einem erfolgreichen Hardwareinventur-Berichterstattungszyklus zu einer Verzögerung kommen, die in Asset Intelligence-Berichten, die ausgeführt wurden, bevor der Client die nächste geplante Hardwareinventur meldet, nicht berücksichtigt wurde.  

 **Einschränkungen bezüglich der Lizenzabgleiche**  
 Der Abgleich der Anzahl installierter Softwaretitel mit der Anzahl erworbener Softwaretitel wird durch einen Vergleich der vom Administrator angegebenen Anzahl an Lizenzen und der Anzahl installierter Softwaretitel erstellt, die durch Hardwareinventuren der Configuration Manager-Clients auf Grundlage des vom Administrator festgelegten Zeitplans gesammelt wurden. Dieser Vergleich stellt keine endgültige Entscheidung zu Lizenzpositionen von Microsoft dar. Die tatsächliche Lizenzposition ist von der bestimmten Softwaretitellizenz sowie den durch die Lizenzbedingungen gewährten Verwendungsrechten abhängig.  

##  <a name="BKMK_ValidationStates"></a> Asset Intelligence-Überprüfungszustände  
 Die Asset Intelligence-Überprüfungszustände geben den Quell- und den aktuellen Überprüfungszustand von Asset Intelligence-Kataloginformationen an. In der folgenden Tabelle werden mögliche Asset Intelligence-Überprüfungszustände und Administratoraktionen, durch die sie verursacht werden können, angezeigt.  

|**Status**|**Definition**|**Administratoraktion**|**Kommentar**|  
|---------------|--------------------|------------------------------|-----------------|  
|**Überprüft**|Das Katalogelement wurde von System Center Online-Forschern definiert.|Keine|Der optimale Zustand.|  
|**Benutzerdefiniert**|Das Katalogelement wurde nicht von System Center Online-Forschern definiert.|Die lokalen Kataloginformationen wurden angepasst.|Dieser Zustand wird in Asset Intelligence-Berichten angezeigt.|  
|**Ausstehend**|Das Katalogelement wurde nicht von System Center Online-Forschern definiert, aber zur Kategorisierung an System Center Online übermittelt.|Die Kategorisierung durch System Center Online wurde angefordert.|Das Katalogelement bleibt in diesem Zustand, bis System Center Online-Mitarbeiter das Element kategorisieren und der Asset Intelligence-Katalog synchronisiert wird.|  
|**Aktualisierbar**|Ein benutzerdefiniertes Katalogelement wurde von System Center Online während einer nachfolgenden Katalogsynchronisierung anders kategorisiert.|Der lokale Asset Intelligence-Katalog wurde so angepasst, dass ein Element als benutzerdefiniert kategorisiert wurde.|Sie können mithilfe der Aktion "Konflikt beheben" entscheiden, ob die neuen Kategorisierungsinformationen oder der vorherige benutzerdefinierte Wert verwendet werden sollen. Weitere Informationen zum Lösen von Konflikten finden Sie unter [Konfigurieren von Asset Intelligence in System Center Configuration Manager](../../../../core/clients/manage/asset-intelligence/operations-for-asset-intelligence.md).|  
|**Nicht kategorisiert**|Das Katalogelement wurde weder von System Center Online-Forschern definiert noch zur Kategorisierung an System Center Online übermittelt, und der Administrator hat ihm keinen benutzerdefinierten Wert zugewiesen.|Keine|Fordern Sie die Kategorisierung an, oder passen Sie die lokalen Kataloginformationen an.<br /><br /> Weitere Informationen zum Lösen von Konflikten finden Sie unter [Konfigurieren von Asset Intelligence in System Center Configuration Manager](../../../../core/clients/manage/asset-intelligence/operations-for-asset-intelligence.md).<br /><br /> Weitere Informationen zum Lösen von Konflikten finden Sie unter [Vorgänge für Asset Intelligence in System Center Configuration Manager](../../../../core/clients/manage/asset-intelligence/operations-for-asset-intelligence.md).|  

> [!NOTE]  
>  Katalogelemente, die an System Center Online zur Kategorisierung übermittelt wurden, haben zwar den Überprüfungszustand **Ausstehend** am zentralen Verwaltungsstandort, werden jedoch an untergeordneten primären Standorten mit dem Überprüfungszustand **Nicht kategorisiert** angezeigt.  

> [!NOTE]  
>  Nach der Auflösung eines Kategorisierungskonflikts wird das Element nicht mehr als in Konflikt stehend überprüft, es sei denn, durch nachfolgende Kategorisierungsaktualisierungen werden neue Informationen über das Element hinzugefügt.  

 Beispiele für das Szenario eines möglichen Übergangs von einem Überprüfungszustand in einen anderen finden Sie unter [Beispiel-Überprüfungszustandsübergänge für Asset Intelligence in System Center Configuration Manager](../../../../core/clients/manage/asset-intelligence/example-validation-state-transitions-for-asset-intelligence.md).  
