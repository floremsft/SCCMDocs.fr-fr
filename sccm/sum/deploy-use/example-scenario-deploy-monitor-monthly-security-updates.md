---
title: "Beispielszenario für die Bereitstellung und Überwachung von Sicherheitssoftwareupdates | Microsoft-Dokumentation"
description: "Verwenden Sie dieses Beispielszenario zum Verwenden von Softwareupdates in Configuration Manager, um die von Microsoft monatlich veröffentlichten Sicherheitssoftwareupdates bereitzustellen und zu überwachen."
keywords: 
author: dougeby
ms.author: dougeby
manager: angrobe
ms.date: 10/06/2016
ms.topic: article
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.service: 
ms.assetid: c32f757a-02da-43f2-b055-5cfd097d8c43
ms.openlocfilehash: 0e6e2b3a9455bb6eda437eb1325aaaadb3d83420
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="example-scenario-for-using-system-center-configuration-manager-to-deploy-and-monitor-the-security-software-updates-released-monthly-by-microsoft"></a>Beispielszenario für die Verwendung von System Center Configuration Manager zum Bereitstellen und Überwachen der monatlichen Sicherheitsupdates von Microsoft

*Gilt für: System Center Configuration Manager (Current Branch)*

In diesem Thema wird ein Beispielszenario angegeben, wie Sie Softwareupdates in System Center Configuration Manager verwenden können, um die von Microsoft monatlich veröffentlichten Sicherheitssoftwareupdates bereitzustellen und zu überwachen.  

 In diesem Szenario ist John der Configuration Manager-Administrator bei der Woodgrove Bank. John muss eine Bereitstellungsstrategie für ein Softwareupdate mit folgenden Bedingungen und Anforderungen erstellen:  

-   Eine aktive Softwareupdatebereitstellung wird eine Woche nach Veröffentlichung der Sicherheitssoftwareupdates durch Microsoft, jeden zweiten Dienstag des Monats, durchgeführt. Dieses Ereignis wird in der Regel als Patch-Dienstag bezeichnet.  

-   Softwareupdates werden heruntergeladen und auf Verteilungspunkten bereitgestellt. Dann wird die Bereitstellung an einer Teilmenge von Clients getestet, bevor John die Softwareupdates vollständig in seiner Produktionsumgebung bereitstellt.  

-   John muss die Kompatibilität der Softwareupdates pro Monat oder Jahr überwachen können.  

 In diesem Szenario wird davon ausgegangen, dass die Infrastruktur der Softwareupdatepunkte bereits implementiert wurde. Verwenden Sie die folgenden Informationen zum Planen und Konfigurieren von Softwareupdates in Configuration Manager.  

|Prozess|Reference|  
|-------------|---------------|  
|Überprüfen der wichtigsten Konzepte für die Softwareupdates.|[Einführung zu Softwareupdates](../understand/software-updates-introduction.md)|  
|Einplanen von Softwareupdates. Diese Informationen helfen Ihnen beim Planen im Hinblick auf Kapazitätsüberlegungen, bei der Ermittlung der Infrastruktur der Softwareupdatepunkte, der Installation von Softwareupdatepunkten, bei Synchronisierungseinstellungen sowie den Clienteinstellungen für Softwareupdates.|[Planen von Softwareupdates](../plan-design/plan-for-software-updates.md)|  
|Konfigurieren von Softwareupdates. Diese Informationen helfen Ihnen beim Installieren und Konfigurieren von Softwareupdatepunkten in der Hierarchie sowie beim Konfigurieren und Synchronisieren von Softwareupdates.<br /><br /> In diesem Szenario konfiguriert John den Zeitplan für die Softwareupdatesynchronisierung so, dass diese am zweiten Mittwoch eines jeden Monats ausgeführt wird, um sicherzustellen, dass immer die aktuellsten Sicherheitssoftwareupdates von Microsoft abgerufen werden.|[Synchronisieren von Softwareupdates](../get-started/synchronize-software-updates.md)|  

 In den folgenden Abschnitten in diesem Thema wird eine beispielhafte Schritt-für-Schritt-Anleitung zur Verfügung gestellt, um Ihnen beim Bereitstellen und Überwachen der Sicherheitssoftwareupdates für Configuration Manager in Ihrem Unternehmen zu helfen.

##  <a name="BKMK_Step1"></a> Schritt 1: Erstellen einer Softwareupdategruppe für jährliche Kompatibilität  
 John erstellt eine Softwareupdategruppe, die er zur Überwachung aller 2016 von ihm veröffentlichten Sicherheitssoftwareupdates verwenden kann. Er führt die Schritte in der folgenden Tabelle aus.  

|Prozess|Reference|  
|-------------|---------------|  
|John fügt Kriterien im Knoten **Alle Softwareupdates** in der Configuration Manager-Konsole hinzu, um nur Sicherheitssoftwareupdates anzuzeigen, die im Jahr 2015 veröffentlicht oder überarbeitet wurden und folgenden Kriterien entsprechen:<br /><br /><ul><li>**Kriterien**: Veröffentlichungs- oder Überarbeitungsdatum</li><li>**Bedingung**: stimmt mit einem bestimmten Datum überein oder liegt danach<br />**Wert**: 1.1.2015</li><li>**Kriterien**: Updateklassifizierung<br />**Wert**: Sicherheitsupdates</li><li>**Kriterien**: Abgelaufen <br />**Wert**: Nein</li></ul>|Keine zusätzlichen Informationen|
|John fügt alle gefilterten Softwareupdates zur neuen Softwareupdategruppe mit folgenden Anforderungen hinzu:<br /><br /><ul><li>**Name**: Kompatibilitätsgruppe – Microsoft-Sicherheitsupdates 2015</li><li>**Beschreibung**: Softwareupdates|[Hinzufügen von Softwareupdates zu einer Updategruppe](add-software-updates-to-an-update-group.md)|  

##  <a name="BKMK_Step2"></a> Schritt 2: Erstellen einer automatischen Bereitstellungsregel für den aktuellen Monat  
 John erstellt eine automatische Bereitstellungsregel für Sicherheitsoftwareupdates, die von Microsoft für den laufenden Monat veröffentlicht werden. Er führt die Schritte in der folgenden Tabelle aus.  

|Prozess|Reference|  
|-------------|---------------|  
|John erstellt eine automatische Bereitstellungsregel mit folgenden Anforderungen:<br /><br /><ol><li>Auf der Registerkarte **Allgemein** nimmt John folgende Konfiguration vor:<br /> <ul><li>Er legt **Monatliche Sicherheitsupdates** für den Namen fest.</li><li>Er wählt eine Testsammlung mit einer begrenzten Anzahl von Clients aus.</li><li>Er wählt **Erstellen einer neuen Softwareupdategruppe** aus.</li><li>Er stellt sicher, dass **Bereitstellen nach Ausführung dieser Regel aktivieren** nicht aktiviert ist.</li></ul></li><li>Auf der Registerkarte **Bereitstellungseinstellungen** wählt John die Standardeinstellungen aus.</li><li>Auf der Seite der **Softwareupdates** konfiguriert John folgende Eigenschaftsfilter und Suchkriterien:<br /><ul><li>Veröffentlichungs- oder Überarbeitungsdatum **Letzter Monat**.</li><li>Updateklassifizierung **Sicherheitsupdates**.</li></ul></li><li>Auf der Seite **Auswertung** aktiviert John die Regel zur Ausführung am **zweiten Donnerstag** jeden **Monats**. Außerdem stellt John sicher, dass sein Synchronisierungszeitplan so eingestellt ist, dass er am **zweiten Mittwoch** jeden **Monats** ausgeführt wird.</li><li>John verwendet die Standardeinstellungen auf den Seiten für Bereitstellungszeitplan, Benutzerfreundlichkeit, Warnungen und Downloadeinstellungen.</li><li>Auf der Seite **Bereitstellungspakete** legt John ein neues Bereitstellungspaket fest.</li><li>John verwendet die Standardeinstellungen auf den Seiten für Downloadort und Sprachauswahl.</li></ol>|[Automatisches Bereitstellen von Softwareupdates](automatically-deploy-software-updates.md)|  

##  <a name="BKMK_Step3"></a> Schritt 3: Überprüfen, ob Softwareupdates bereitgestellt werden können  
 Jeden zweiten Donnerstag jedes Monats überprüft John, ob die Softwareupdates bereitgestellt werden können. Er führt die folgenden Aktionen aus.  

|Prozess|Reference|  
|-------------|---------------|  
|John stellt sicher, dass die Synchronisierung der Softwareupdates erfolgreich abgeschlossen wurde.|[Status der Softwareupdatesynchronisierung](monitor-software-updates.md#BKMK_SUSyncStatus)|  

##  <a name="BKMK_Step4"></a> Schritt 4: Bereitstellen der Softwareupdategruppe  
 Nachdem er überprüft hat, ob die Softwareupdates bereitgestellt werden können, stellt er diese bereit. Er führt die Schritte in der folgenden Tabelle aus.  

|Prozess|Reference|  
|-------------|---------------|  
|John erstellt zwei Testbereitstellungen für die neue Softwareupdategruppe. Er erwägt für jede Bereitstellung die folgenden Umgebungen:<br /><br /> **Arbeitsstation-Testbereitstellung**: John berücksichtigt Folgendes für die Testbereitstellung der Arbeitsstation:<br /><br /><ul><li>Er gibt eine Bereitstellungssammlung an, die eine Teilmenge der Arbeitsstationsclients enthält, um die Bereitstellung zu überprüfen.</li><li>Er konfiguriert die Bereitstellungseinstellungen, die für die Arbeitsstationsclients in seiner Umgebung zutreffen.</li></ul><br />**Servertestbereitstellung**: John berücksichtigt Folgendes für die Servertestbereitstellung:<br /><br /><ul><li>Er gibt eine Bereitstellungssammlung an, die eine Teilmenge der Serverclients enthält, um die Bereitstellung zu überprüfen.</li><li>Er konfiguriert die Bereitstellungseinstellungen, die für die Serverclients in seiner Umgebung zutreffen.</li></ul>|[Bereitstellen von Softwareupdates](deploy-software-updates.md)|  
|John überprüft, ob die Testbereitstellungen erfolgreich bereitgestellt wurden.|[Status der Softwareupdatebereitstellung](monitor-software-updates.md#BKMK_SUDeployStatus)|  
|John aktualisiert die zwei Bereitstellungen mit neuen Sammlungen, die seine Produktionsarbeitsstationen und -server beinhalten.|Keine zusätzlichen Informationen|  

##  <a name="BKMK_Step5"></a> Schritt 5: Überwachen der Kompatibilität für bereitgestellte Softwareupdates  
 John überwacht die Kompatibilität seiner Softwareupdatebereitstellungen. Er führt den Schritt in der folgenden Tabelle aus.  

|Prozess|Reference|  
|-------------|---------------|  
|John überwacht den Status der Softwareupdatebereitstellung in der Configuration Manager-Konsole und überprüft die in der Konsole verfügbaren Berichte zur Softwareupdatebereitstellung.|[Überwachen von Softwareupdates in System Center Configuration Manager](../../sum/deploy-use/monitor-software-updates.md)|  

##  <a name="BKMK_Step6"></a> Schritt 6: Hinzufügen monatlicher Softwareupdates zur jährlichen Updategruppe  
 John fügt die Softwareupdates aus der monatlichen Softwareupdategruppe zur jährlichen Softwareupdategruppe hinzu. Er führt den Schritt in der folgenden Tabelle aus.  

|Prozess|Reference|  
|-------------|---------------|  
|John wählt die Softwareupdates aus der monatlichen Softwareupdategruppe aus und fügt die Softwareupdates zu der Softwareupdategruppe hinzu, die er für die jährliche Kompatibilität erstellt hat. Er verfolgt die Softwareupdatekompatibilität und erstellt verschiedene Berichte für die Geschäftsleitung.|[Hinzufügen von Softwareupdates zu einer bereitgestellten Updategruppe](add-software-updates-to-an-update-group.md)|  

John hat seine monatliche Bereitstellung für Sicherheitssoftwareupdates erfolgreich abgeschlossen. Er überwacht weiterhin die Kompatibilität der Softwareupdates und erstellt Meldungen dazu, um sicherzustellen, dass sich die Clients in seiner Umgebung innerhalb der zulässigen Kompatibilitätsstufen bewegen.  

##  <a name="BKMK_MonthlyProcess"></a> Regelmäßiger monatlicher Prozess zur Bereitstellung von Softwareupdates  
 Nach dem ersten Monat, in dem John Softwareupdates bereitgestellt hat, führt er die Schritte 3 bis 6 aus, um die von Microsoft veröffentlichten Sicherheitssoftwareupdates bereitzustellen.  
