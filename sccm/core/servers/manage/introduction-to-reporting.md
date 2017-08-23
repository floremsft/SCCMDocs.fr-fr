---
title: "Einführung in die Berichterstellung | Microsoft-Dokumentation"
description: "Erfahren Sie mehr zu den Tools und Ressourcen, die Ihnen für die Verwaltung der Berichterstattung in Configuration Manager zur Verfügung stehen."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 230be984-d2cd-4d53-bd7a-bc24dd93fc22
caps.latest.revision: "7"
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: 5846ca3c91626491b03b36dd17b454bb9382a8dc
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="introduction-to-reporting-in-system-center-configuration-manager"></a>Einführung in die Berichterstellung in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Mit der Berichterstattung in System Center Configuration Manager stehen Ihnen eine Reihe von Tools und Ressourcen zur Verfügung, mit deren Hilfe Sie die erweiterten Berichterstattungsfunktionen von SQL Server Reporting Services (SSRS) sowie die umfassenden Gestaltungsmöglichkeiten des Berichts-Generators von Reporting Services nutzen können. Mithilfe der Berichterstattung von Configuration Manager können Sie Informationen zu Benutzern, Hardware- und Softwareinventur, Softwareupdates, Anwendungen, Standortstatus und anderen Configuration Manager-Operationen in Ihrer Organisation erfassen, organisieren und darstellen. Mit der Berichterstattung stehen Ihnen eine Reihe vordefinierter Berichte zur Verfügung, die Sie unverändert verwenden oder bei Bedarf an Ihre Anforderungen anpassen können, und Sie können zudem benutzerdefinierte Berichte erstellen. In den folgenden Abschnitten finden Sie Informationen zum Verwalten der Berichterstellung in Configuration Manager.  

##  <a name="BKMK_SQLServerReportingServices"></a> SQL Server Reporting Services  
 In SQL Server Reporting Services steht Ihnen eine vollständige Palette verwendungsbereiter Tools und Dienste zur Verfügung, mit deren Hilfe Sie Berichte für Ihr Unternehmen erstellen, bereitstellen und verwalten können, sowie Programmierungsfunktionen zum Erweitern und Anpassen der verfügbaren Berichterstattungsfunktionen. Reporting Services ist eine serverbasierte Berichterstattungsplattform, die umfassende Berichterstattungsfunktionen für zahlreiche Datenquellen bietet.  

 Configuration Manager verwendet SQL Server Reporting Services als Berichterstattungslösung. Die Integration mit Reporting Services bietet die folgenden Vorteile:  

-   Verwendet ein Industriestandard-Berichterstattungssystem zum Abfragen der Configuration Manager-Datenbank.  

-   Zeigt Berichte mithilfe der Configuration Manager-Berichtsanzeige an oder mithilfe des Berichts-Managers, einer webbasierten Verbindung mit dem Bericht.  

-   Bietet hohe Leistung, Verfügbarkeit und Skalierbarkeit.  

-   Ermöglicht das Abonnieren von Berichten. Beispielsweise kann ein Manager automatisch per E-Mail einen täglichen Bericht über den Status einer Softwareupdatebereitstellung erhalten.  

-   Exportiert Berichte, die Benutzer in einer Vielzahl von häufig verwendeten Formaten auswählen können.  

 Weitere Informationen zu Reporting Services finden Sie unter [SQL Server Reporting Services](http://go.microsoft.com/fwlink/p/?LinkID=212032) in der SQL Server 2008-Onlinedokumentation.  

##  <a name="BKMK_ReportingServicesPoint"></a> Reporting Services-Punkt  
 Der Reporting Services-Punkt ist eine Standortsystemrolle, die auf einem Server installiert wird, auf dem Microsoft SQL Server Reporting Services ausgeführt wird. Der Reporting Services-Punkt kopiert die Configuration Manager-Berichtsdefinitionen an Reporting Services, erstellt auf Berichtskategorien basierende Berichtsordner und die Sicherheitsrichtlinie für Berichtsordner und berichtet anhand der rollenbasierten Berechtigungen für Configuration Manager-Administratoren. Alle zehn Minuten wird vom Reporting Services-Punkt eine Verbindung mit Reporting Services hergestellt, um die Sicherheitsrichtlinie erneut anzuwenden, falls diese, zum Beispiel durch die Verwendung des Berichts-Managers, geändert wurde. Weitere Informationen zum Planen und Installieren eines Reporting Services-Punkts finden Sie in der folgenden Dokumentation:  

-   [Planen der Berichterstellung in System Center Configuration Manager](planning-for-reporting.md)  

-   [Konfigurieren der Berichterstellung in System Center Configuration Manager](configuring-reporting.md)  

##  <a name="BKMK_ConfigurationManagerReports"></a> Configuration Manager-Berichte  
 Configuration Manager stellt Berichtsdefinitionen für über 400 Berichte in über 50 Berichtsordnern bereit, die während der Installation des Reporting Services-Punkts in den Berichtsstammordner in SQL Server Reporting Services kopiert werden. Die Berichte werden in der Configuration Manager-Konsole angezeigt und dort anhand der Berichtskategorie in Unterordnern organisiert. Berichte werden in der Configuration Manager-Hierarchie nicht nach oben oder unten übermittelt. Sie werden nur für die Datenbank des Standorts ausgeführt, an dem sie erstellt werden. Da in Configuration Manager jedoch globale Daten über die gesamte Hierarchie repliziert werden, können Sie auf hierarchieweite Informationen zugreifen. Wenn für einen Bericht Daten aus einer Standortdatenbank abgerufen werden, liegen Zugriffsrechte für die Standortdaten von den aktuellen und untergeordneten Standorten sowie für globale Daten aller Standorte in der Hierarchie vor. Wie bei anderen Configuration Manager-Objekten benötigen Administratoren auch zum Ausführen und Ändern von Berichten die entsprechenden Berechtigungen. Administratoren müssen über die Berechtigung **Bericht ausführen** für das Objekt verfügen, um einen Bericht ausführen zu können. Administratoren müssen über die Berechtigung **Bericht ändern** für das Objekt verfügen, um einen Bericht erstellen oder ändern zu können.  

###  <a name="BKMK_CreatingReports"></a> Erstellen und Ändern von Berichten  
 Configuration Manager verwendet den Berichts-Generator von SQL Server für modellbasierte und SQL-basierte Berichte als ausschließliches Erstellungs- und Bearbeitungstool. Beim Erstellen oder Bearbeiten eines Berichts in der Configuration Manager-Konsole wird der Berichts-Generator geöffnet. Weitere Informationen zur Verwaltung von Berichten finden Sie unter [Vorgänge und Wartungstasks für die Berichterstellung in System Center Configuration Manager](operations-and-maintenance-for-reporting.md).  

###  <a name="BKMK_RunningReports"></a> Ausführen von Berichten  
 Wenn Sie einen Bericht in der Configuration Manager-Konsole ausführen, wird die Berichtsanzeige geöffnet und eine Verbindung mit Reporting Services hergestellt. Nachdem Sie alle erforderlichen Berichtsparameter angegeben haben, werden die Daten von Reporting Services abgerufen, und das Ergebnis wird im Viewer angezeigt. Sie können auch eine Verbindung mit SQL Services Reporting Services und mit der Datenquelle für den Standort herstellen und dann Berichte ausführen.  

###  <a name="BKMK_ReportPrompts"></a> Berichtaufforderungen  
 Berichtaufforderungen oder Berichtsparameter in Configuration Manager sind Berichtseigenschaften, die beim Erstellen oder Ändern eines Berichts konfiguriert werden können. Berichtaufforderungen werden zum Begrenzen oder Auswählen der Zieldaten verwendet, die ein Bericht abruft. Ein Bericht kann mehrere Aufforderungen enthalten, solange die Namen der Aufforderungen eindeutig sind und nur alphanumerische Zeichen verwendet werden, die den Regeln für SQL Server-Bezeichner entsprechen.  

 Beim Ausführen eines Berichts wird ein Wert für einen erforderlichen Parameter vom Benutzer angefordert, und auf Grundlage dieses Werts werden die Berichtsdaten abgerufen. So werden für den Bericht **Computerinformationen für einen bestimmten Computer** beispielsweise die Computerinformationen für einen bestimmten Computer abgerufen, und der Administrator wird aufgefordert, einen Computernamen einzugeben. Der angegebene Wert wird von Reporting Services an eine Variable weitergegeben, die in der SQL-Anweisung für den Bericht definiert ist.  

###  <a name="BKMK_ReportLinks"></a> Berichtslinks  
 Berichtlinks in Configuration Manager werden in einem Quellbericht dazu verwendet, Administratoren einen einfachen Zugriff auf zusätzliche Daten zu ermöglichen, z.B. auf genauere Informationen zu den Elementen im Quellbericht. Wenn zum Ausführen des Zielberichts eine oder mehrere Aufforderungen erforderlich sind, muss der Quellbericht eine Spalte mit den entsprechenden Werten für jede Aufforderung enthalten. Sie müssen die Nummer der Spalte angeben, die den Wert für die Aufforderung enthält. Es ist z. B. möglich, einen Bericht mit Computern, die kürzlich erkannt wurden, mit einem Bericht zu verknüpfen, der alle aktuellen Meldungen zu einem bestimmten Computer enthält. Beim Erstellen des Links können Sie angeben, dass z. B. Spalte 2 des Quellberichts Computernamen enthält, die an der Aufforderung des Zielberichts eingegeben werden müssen. Wenn Sie den Quellbericht ausführen, werden links neben jeder Datenzeile Verknüpfungssymbole angezeigt. Wenn Sie in einer Zeile auf ein Symbol klicken, wird der Wert in der angegebenen Spalte der Berichtsanzeige als Aufforderungswert übermittelt, der für die Anzeige des Zielberichts erforderlich ist. Sie können einen Bericht nur mit einem einzigen Link konfigurieren, über den eine Verbindung mit einer einzigen Zielressource hergestellt werden kann.  

> [!WARNING]  
>  Wenn Sie einen Zielbericht in einen anderen Berichtsordner verschieben, ändert sich der Speicherort für den Zielbericht. Der Berichtslink im Quellbericht wird nicht automatisch mit dem neuen Speicherort aktualisiert, sodass der Berichtslink im Quellbericht einen Fehler verursacht.  

##  <a name="BKMK_ReportFolders"></a> Berichtsordner  
 Berichtsordner in System Center Configuration Manager bieten eine Methode für das Sortieren und Filtern von Berichten, die in Reporting Services gespeichert sind. Berichtordner sind besonders nützlich, wenn Sie viele Berichte verwalten müssen. Wenn Sie einen Reporting Services-Punkt installieren, werden Berichte in Reporting Services kopiert und in über 50 Berichtsordnern organisiert. Die Berichtsordner sind schreibgeschützt. Sie können sie in der Configuration Manager-Konsole nicht ändern.  

##  <a name="BKMK_ReportSubscriptions"></a> Berichtsabonnements  
 Ein Berichtsabonnement in Reporting Services ist eine wiederholte Anfrage zur Übermittlung eines Berichts zu einem bestimmten Zeitpunkt oder bei Eintreten eines bestimmten Ereignisses. Das gewünschte Anwendungsdateiformat für den Bericht kann für das Abonnement angegeben werden. Abonnements sind eine Alternative zum Ausführen eines Berichts bei Bedarf. Bei der Berichterstattung bei Bedarf muss der Bericht immer wieder aktiv ausgewählt werden, um ihn anzeigen zu können. Mit Abonnements ist dagegen die geplante automatische Übermittlung eines Berichts möglich.  

 Sie können Berichtsabonnements in der Configuration Manager-Konsole verwalten. Sie werden auf dem Berichtsserver verarbeitet. Die Abonnements werden mithilfe von Übermittlungserweiterungen verteilt, die auf dem Server bereitgestellt werden. Standardmäßig können Sie Abonnements erstellen, um Berichte in einen freigegebenen Ordner oder an eine E-Mail-Adresse senden zu lassen. Weitere Informationen zur Verwaltung von Berichtabonnements finden Sie unter [Vorgänge und Wartungstasks für die Berichterstellung in System Center Configuration Manager](operations-and-maintenance-for-reporting.md).  

##  <a name="BKMK_ReportBuilder"></a> Report Builder  
 Configuration Manager verwendet den Berichts-Generator von Microsoft SQL Server Reporting Services sowohl für modellbasierte als auch für SQL-basierte Berichte als ausschließliches Erstellungs- und Bearbeitungstool. Beim Erstellen oder Bearbeiten eines Berichts in der Configuration Manager-Konsole wird der Berichts-Generator geöffnet. Report Builder wird automatisch installiert, wenn Sie zum ersten Mal einen Bericht erstellen oder ändern. Die Version von Report Builder, die der installierten Version von SQL Server zugeordnet ist, wird beim Ausführen oder Bearbeiten von Berichten geöffnet.  

 Bei der Installation von Report Builder wird Unterstützung für mehr als 20 Sprachen hinzugefügt. Beim Ausführen von Report Builder werden Daten in der Sprache des Betriebssystems angezeigt, das auf dem lokalen Computer ausgeführt wird. Wenn diese Sprache von Report Builder nicht unterstützt wird, werden die Daten auf Englisch angezeigt. Von Report Builder wird der gesamte Funktionsumfang von SQL Server 2008 Reporting Services unterstützt, darunter die folgenden Funktionen:  

-   Intuitive Umgebung zum Erstellen von Berichten, die Microsoft Office ähnlich ist  

-   Flexibles Berichtslayout der Berichtsdefinitionssprache (RDL) von SQL Server 2008  

-   Verschiedene Formen der Datenvisualisierung, darunter Diagramme und Anzeigen  

-   Textfelder mit umfassenden Formatierungsmöglichkeiten  

-   Exportieren nach Microsoft Word  

 Sie können Report Builder auch aus SQL Server Reporting Services öffnen.  

##  <a name="BKMK_ReportModels"></a> Berichtsmodelle in SQL Server Reporting Services  
 Administratoren werden von SQL Reporting Services in Configuration Manager mithilfe von Berichtsmodellen bei der Auswahl von Elementen aus der Datenbank unterstützt, die in modellbasierte Berichte eingeschlossen werden sollen. Dem Administrator, der den Bericht aufbaut, stehen mit Berichtsmodellen nur bestimmte Ansichten und Elemente zur Auswahl. Zur Erstellung von modellbasierten Berichten muss mindestens ein Berichtsmodell zur Verfügung stehen. Berichtsmodelle bieten die folgenden Features:  

-   Sie können Datenbankfeldern und Ansichten logische Unternehmensnamen zuweisen, um die Erstellung von Berichten zu vereinfachen. Kenntnisse der Datenbankstruktur sind zum Erstellen von Berichten nicht erforderlich.  

-   Sie können Elemente logisch gruppieren.  

-   Sie können Beziehungen zwischen Elementen definieren.  

-   Sie können Modellelemente sichern, sodass Administratoren nur die Daten angezeigt werden, für die sie die Berechtigung zum Anzeigen haben.  

 Zwar sind in Configuration Manager Beispielmodellberichte enthalten, aber Sie können auch eigene Berichtsmodelle definieren, die Ihre speziellen Unternehmensanforderungen erfüllen. Weitere Informationen zum Erstellen von Berichtsmodellen finden Sie unter [Erstellen benutzerdefinierter Berichtsmodelle für System Center Configuration Manager in SQL Server Reporting Services](creating-custom-report-models-in-sql-server-reporting-services.md).  

## <a name="next-steps"></a>Nächste Schritte
[Planen der Berichterstellung](planning-for-reporting.md)
