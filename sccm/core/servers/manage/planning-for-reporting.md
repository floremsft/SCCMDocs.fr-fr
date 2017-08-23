---
title: Planen der Berichterstellung | Microsoft-Dokumentation
description: "Die Berichterstellung in Configuration Manager zu planen ist wichtig. Dies gilt von Installationsdetails über die Sicherheit bis hin zur Netzwerkbandbreite."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: ff920c84-d5c8-458c-b67f-bc7219b05690
caps.latest.revision: "6"
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: 119f501057bf44e483be31db20b88326b3d05ebb
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="planning-for-reporting-in-system-center-configuration-manager"></a>Planen der Berichterstellung in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Zur Berichterstellung in System Center Configuration Manager gehören mehrere Tools und Ressourcen, mit deren Hilfe Sie die erweiterten Berichterstellungsfunktionen von SQL Server Reporting Services nutzen können. Anhand der folgenden Abschnitte können Sie die Berichterstellung in Configuration Manager planen.  

##  <a name="BKMK_InstallReportingServicesPoint"></a> Bestimmen des Installationsorts für den Reporting Services-Punkt  
 Beim Ausführen von Configuration Manager-Berichten an einem Standort sind die Informationen in der Standortdatenbank für die Berichte zugänglich. Anhand der folgenden Abschnitte können Sie festlegen, wo der Reporting Services-Punkt installiert und welche Datenquelle verwendet werden soll.  

> [!NOTE]  
>  Weitere Informationen zur Planung der Standortsysteme finden Sie unter [Hinzufügen von Standortsystemrollen](../deploy/configure/add-site-system-roles.md).  

###  <a name="BKMK_SupportedSiteServers"></a> Unterstützte Standortsystemserver  
 Sie können den Reporting Services-Punkt an einem Standort der zentralen Verwaltung und an primären Standorten sowie auf mehreren Standortsystemen an einem Standort und an anderen Standorten in der Hierarchie installieren. Der Reporting Services-Punkt wird nicht an sekundären Standorten unterstützt. Der erste Reporting Services-Punkt an einem Standort wird als Standardberichtsserver konfiguriert. Sie können einem Standort zwar weitere Reporting Services-Punkte hinzufügen, für die Configuration Manager-Berichte wird jedoch der Standardberichtsserver jedes Standorts aktiv verwendet. Sie können den Reporting Services-Punkt auf dem Standortserver oder einem Remote-Standortsystem installieren. Aus Leistungsgründen wird jedoch empfohlen, die Reporting Services auf einem Remote-Standortsystemserver zu verwenden.  

###  <a name="BKMK_DataReplication"></a> Überlegungen zur Datenreplikation  
 Von Configuration Manager replizierte Daten werden entweder als globale Daten oder als Standortdaten klassifiziert. Als globale Daten werden Objekte bezeichnet, die von Administratoren erstellt wurden und die an alle Standorte innerhalb der Hierarchie repliziert werden. Sekundäre Standorte erhalten dagegen nur eine Untergruppe globaler Daten. Zu den globalen Daten werden beispielsweise Softwarebereitstellungen, Softwareupdates, Sammlungen und rollenbasierte Verwaltungssicherheitsbereiche gezählt. Als Standortdaten werden Betriebsinformationen bezeichnet, die von primären Configuration Manager-Standorten und den Clients, die primären Standorten unterstellt sind, erstellt werden. Standortdaten werden am Standort der zentralen Verwaltung repliziert, jedoch nicht an anderen Standorten. Zu den Standortdaten werden beispielsweise Hardwareinventurdaten, Statusmeldungen, Warnungen und die Ergebnisse von abfragebasierten Sammlungen gezählt. Standortdaten können nur am Standort der zentralen Verwaltung und an dem primären Standort, von dem sie stammen, angezeigt werden.  

 Berücksichtigen Sie bei der Entscheidung, wo die Reporting Services-Punkte installiert werden soll, folgende Faktoren:  

-   Einem Reporting Services-Punkt mit der Datenbank des Standorts der zentralen Verwaltung als Berichtsdatenquelle ist der Zugriff auf alle globalen Daten und alle Standortdaten in der Configuration Manager-Hierarchie möglich. Wenn Sie Berichte benötigen, in denen Standortdaten mehrerer Standorte einer Hierarchie enthalten sind, erwägen Sie, den Reporting Services-Punkt auf einem Standortsystem des Standorts der zentralen Verwaltung zu installieren und die Datenbank des Standorts der zentralen Verwaltung als Berichtsdatenquelle zu verwenden.  

-   Einem Reporting Services-Punkt mit der untergeordneten primären Standortdatenbank als Datenquelle ist nur der Zugriff auf die globalen Daten und Standortdaten des lokalen primären Standorts und ggf. von untergeordneten sekundären Standorten möglich. Die Standortdaten anderer primärer Standorte in der Configuration Manager-Hierarchie werden nicht am primären Standort repliziert und sind für Reporting Services daher nicht verfügbar. Wenn Sie Berichte mit Standortdaten eines bestimmten Standorts oder mit globalen Daten benötigen, den Berichtbenutzern jedoch keinen Zugriff auf Standortdaten anderer primärer Standorte gewähren möchten, installieren Sie einen Reporting Services-Punkt auf einem Standortsystem am primären Standort, und verwenden Sie die Datenbank des primären Standorts als Berichtsdatenquelle.  

###  <a name="BKMK_NetworkBandwidth"></a> Überlegungen zur Netzwerkbandbreite  
 Die Kommunikation zwischen Standortsystemservern des gleichen Standorts erfolgt je nach Ihrer Standortkonfiguration über SMB (Server Message Block), HTTP oder HTTPS. Diese Kommunikation wird nicht verwaltet und kann jederzeit ohne Steuerung der Netzwerkbandbreite erfolgen. Prüfen Sie daher die verfügbare Netzwerkbandbreite, bevor Sie den Reporting Services-Punkt auf einem Standortsystem installieren.  

> [!NOTE]  
>  Weitere Informationen zur Planung der Standortsysteme finden Sie unter [Hinzufügen von Standortsystemrollen](../deploy/configure/add-site-system-roles.md).  

##  <a name="BKMK_RoleBaseAdministration"></a> Planen der rollenbasierten Verwaltung von Berichten  
 Das Sicherheitskonzept bei der Berichterstattung ist mit dem vieler anderer Objekte in Configuration Manager vergleichbar: Sie können Sicherheitsrollen und Berechtigungen an Administratoren vergeben. Administratoren können nur Berichte ausführen und ändern, bei denen sie über die entsprechenden Sicherheitsrechte verfügen. Zum Ausführen der Berichte in der Configuration Manager-Konsole benötigen Sie das Recht **Lesen** für die Berechtigung **Standort** sowie konfigurierte Berechtigungen für bestimmte Objekte.  

 Im Gegensatz zu anderen Objekten in Configuration Manager müssen die Sicherheitsrechte, die Sie in der Configuration Manager-Konsole für Administratoren festlegen, auch in Reporting Services konfiguriert werden. Beim Konfigurieren der Sicherheitsrechte in der Configuration Manager-Konsole wird vom Reporting Services-Punkt eine Verbindung mit Reporting Services hergestellt, und es werden entsprechende Berechtigungen für die Berichte eingeholt. Beispielsweise sind der Sicherheitsrolle **Softwareupdate-Manager** die Berechtigungen **Bericht ausführen** und **Bericht ändern** zugeordnet. Administratoren, denen nur die Rolle **Softwareupdate-Manager** zugewiesen ist, können nur Berichte für Softwareupdates ausführen und ändern. Berichte für andere Objekte werden in der Configuration Manager-Konsole nicht angezeigt. Die einzige Ausnahme besteht darin, dass einige Berichte keinen bestimmten sicherungsfähigen Configuration Manager-Objekten zugeordnet sind. Bei solchen Berichten benötigen Administratoren das Recht **Schreiben** für die Berechtigung **Standort** , um die Berichte auszuführen, und das Recht **Ändern** für die Berechtigung **Standort** , um die Berichte zu ändern.  

 Berichte sind für die rollenbasierte Verwaltung komplett aktiviert. Bei allen in Configuration Manager verfügbaren Berichten werden die Daten auf Basis der Berechtigungen des Administrators gefiltert, der den Bericht ausführt. Administratoren mit eng festgelegten Rollen können nur für die jeweilige Rolle definierte Informationen anzeigen.  

 Weitere Informationen zu Sicherheitsrechten für die Berichterstellung finden Sie unter [Konfigurieren der Berichterstellung](configuring-reporting.md).  

 Weitere Informationen zur rollenbasierten Verwaltung in Configuration Manager finden Sie unter [Konfigurieren einer rollenbasierten Verwaltung](../deploy/configure/configure-role-based-administration.md).  

## <a name="next-steps"></a>Nächste Schritte  
 Bei der Planung der Berichterstellung in Configuration Manager sind folgende zusätzliche Themen hilfreich:  

-   [Voraussetzungen für die Berichterstellung in System Center Configuration Manager](../../../core/servers/manage/prerequisites-for-reporting.md)  
-   [Bewährte Methoden für die Berichterstellung in System Center Configuration Manager](../../../core/servers/manage/best-practices-for-reporting.md)  
