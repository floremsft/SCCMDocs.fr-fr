---
title: "Überwachen von Softwareupdates | Microsoft-Dokumentation"
description: "Die System Center Configuration Manager-Konsole stellt Warnungen und Status zum Überwachen von Updates und Kompatibilität bereit."
keywords: 
author: dougeby
ms.author: dougeby
manager: angrobe
ms.date: 11/10/2016
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology: configmgr-sum
ms.assetid: 9afd7b0f-5c8e-48bc-9a65-1f7d74103688
ms.openlocfilehash: 956ef263a1c178b5ab5926705859f4b2d0ae5bc7
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="monitor-software-updates-in-system-center-configuration-manager"></a>Überwachen von Softwareupdates in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

In der System Center Configuration Manager-Konsole stehen viele Hilfsmittel zur Überwachung von Objekten, Prozessen und Kompatibilitätsinformationen im Zusammenhang mit Softwareupdates zur Verfügung. Verwenden Sie die folgenden Bereiche, um Softwareupdates zu überwachen.

## <a name="software-updates-dashboard"></a>Dashboard „Softwareupdatepunkt“
Ab Version 1610 von Configuration Manager können Sie jetzt das Dashboard „Softwareupdatepunkt“ verwenden, um den aktuellen Konformitätsstatus von Geräten in Ihrer Organisation anzuzeigen, und schnell Daten analysieren, um anzuzeigen, welche Geräte gefährdet sind. Navigieren Sie zum Anzeigen des Dashboards zu **Überwachung** > **Überblick** > **Sicherheit** > **Software Updates Dashboard** (Dashboard „Softwareupdatepunkt“).   

##  <a name="BKMK_SUAlerts"></a> Warnungen zu Softwareupdates  
 Sie können Warnungen zu Softwareupdates konfigurieren, mit denen Administratoren benachrichtigt werden, wenn die Kompatibilitätsstufen von Softwareupdatebereitstellungen unter dem konfigurierten Prozentsatz liegen. Sie können Warnungen zu Softwareupdatebereitstellungen an den folgenden Stellen konfigurieren:  

-   ADR-Einstellung: Sie können die Warnungseinstellungen im Assistenten zum Erstellen automatischer Bereitstellungsregeln und in den ADR-Eigenschaften (Automatic Deployment Rule, ADR) konfigurieren.  

-   Bereitstellungseinstellung: Sie können die Warnungseinstellungen im Assistenten zum Bereitstellen von Softwareupdates und in den Bereitstellungseigenschaften konfigurieren.  

Nachdem Sie die Warnungseinstellungen konfiguriert haben, wird von Configuration Manager eine Warnung ausgegeben, wenn die angegebenen Bedingungen erfüllt sind. Sie können die Warnungen zu Softwareupdates an den folgenden Stellen prüfen:  

1.  Prüfen Sie die letzten Warnungen im Arbeitsbereich **Softwarebibliothek** im Knoten **Softwareupdates** .  

2.  Verwalten Sie die konfigurierten Warnungen im Arbeitsbereich **Überwachung** im Knoten **Warnungen** .  

##  <a name="BKMK_SUSyncStatus"></a> Status der Softwareupdatesynchronisierung  
 Nach dem Start der Synchronisierung können Sie den Synchronisierungsprozess in der Configuration Manager-Konsole für alle Softwareupdatepunkte in der Hierarchie überwachen. Gehen Sie wie folgt vor, um die Softwareupdatesynchronisierung zu überwachen.  

#### <a name="to-monitor-the-software-updates-synchronization-process"></a>So überwachen Sie die Softwareupdatesynchronisierung  

- Wechseln Sie in der Configuration Manager-Konsole zu **Überwachung** > **Übersicht** > **Synchronisierungsstatus der Softwareupdatepunkte**.  

    Die Softwareupdatepunkte in der Configuration Manager-Hierarchie werden im Ergebnisbereich angezeigt. Von hier können Sie den Synchronisierungsstatus aller Softwareupdatepunkte überwachen. Ausführlichere Informationen zum Synchronisierungsprozess enthält die Datei „wsyncmgr.log“, die sich auf jedem Standortserver unter <*ConfigMgr-Installationspfad*>\Logs befindet.  

##  <a name="BKMK_SUDeployStatus"></a> Status der Softwareupdatebereitstellung  
 Nach der Bereitstellung der Softwareupdates in einer Softwareupdategruppe bzw. nach der Bereitstellung eines einzelnen Softwareupdates können Sie den Bereitstellungsstatus überwachen. Gehen Sie wie folgt vor, um den Bereitstellungsstatus einer Softwareupdategruppe oder eines Softwareupdates zu überwachen.  

#### <a name="to-monitor-deployment-status"></a>So überwachen Sie den Bereitstellungsstatus  

1.  Wechseln Sie in der Configuration Manager-Konsole zu **Überwachung** > **Übersicht** > **Bereitstellungen**.  

2.  Klicken Sie auf die Softwareupdategruppe oder das Softwareupdate, dessen Bereitstellungsstatus Sie überwachen möchten.  

3.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Bereitstellung** auf **Status anzeigen**.  

##  <a name="BKMK_SUReports"></a> Softwareupdateberichte  
 Die Zustandsmeldungen zu Softwareupdates enthalten Informationen zur Kompatibilität von Softwareupdates sowie zu Bewertung und Erzwingungszustand von Softwareupdatebereitstellungen. Zum Anzeigen der Zustandsmeldungen können Sie Softwareupdateberichte ausführen. Mehr als 30 vordefinierte Softwareupdateberichte sind verfügbar. Sie sind in verschiedene Kategorien unterteilt und können dazu verwendet werden, Informationen zu bestimmten Aspekten von Softwareupdates und -bereitstellungen zu liefern. Zusätzlich zu den vorkonfigurierten Berichten können Sie auch benutzerdefinierte Softwareupdateberichte erstellen, die auf die Anforderungen Ihres Unternehmens zugeschnitten sind. Weitere Informationen finden Sie unter [Vorgänge und Wartungstasks für die Berichterstellung](../../core/servers/manage/operations-and-maintenance-for-reporting.md).  

##  <a name="BKMK_MonitorContent"></a> Überwachen von Inhalt  
 Sie können den Inhalt in der Configuration Manager-Konsole überwachen, und so den Status aller Pakettypen im Zusammenhang mit den zugeordneten Verteilungspunkten prüfen. Dies kann den Inhaltsprüfungsstatus des Paketinhalts, den Status von Inhalt, der einer bestimmten Verteilungspunktgruppe zugeordnet ist, den Zustand von Inhalt, der einem Verteilungspunkt zugeordnet ist, und den Status optionaler Funktionen jedes Verteilungspunkts (Inhaltsprüfung, PXE und Multicast) umfassen.  

###  <a name="BKMK_ContentStatus"></a> Überwachung des Inhaltsstatus  
 Im Arbeitsbereich **Überwachung** finden Sie im Knoten **Inhaltsstatus** Informationen zu Inhaltspaketen. Sie können allgemeine Informationen zum Paket, den Verteilungsstatus des Pakets sowie detaillierte Statusinformationen zum Paket prüfen. Gehen Sie wie folgt vor, um den Inhaltsstatus anzuzeigen.  

#### <a name="to-monitor-content-status"></a>So überwachen Sie den Inhaltsstatus  

1.  Wechseln Sie in der Configuration Manager-Konsole zu **Überwachung** > **Übersicht** > **Verteilungsstatus** > **Inhaltsstatus**. Die Pakete werden angezeigt.  

2.  Wählen Sie das Paket aus, für das Sie detaillierte Statusinformationen anzeigen möchten.  

3.  Klicken Sie auf der Registerkarte **Startseite** auf **Status anzeigen**. Detaillierte Statusinformationen zum Paket werden angezeigt.  

###  <a name="BKMK_DPGroupStatus"></a> Status der Verteilungspunktgruppe  
 Im Arbeitsbereich **Überwachung** finden Sie im Knoten **Status der Verteilungspunktgruppe** Informationen zu Verteilungspunktgruppen. Sie können allgemeine Informationen zur Verteilungspunktgruppe, wie beispielsweise den Status der Verteilungspunktgruppe und die Kompatibilitätsstufe, sowie detaillierte Informationen zur Verteilungspunktgruppe anzeigen. Gehen Sie wie folgt vor, um den Status einer Verteilungspunktgruppe anzuzeigen.  

#### <a name="to-monitor-distribution-point-group-status"></a>So überwachen Sie den Status einer Verteilungspunktgruppe  

1.  Wechseln Sie in der Configuration Manager-Konsole zu **Überwachung** > **Übersicht** > **Verteilungsstatus** > **Status der Verteilungspunktgruppe**. Die Verteilungspunktgruppen werden angezeigt.  

2.  Wählen Sie die Verteilungspunktgruppe aus, für die detaillierte Statusinformationen angezeigt werden sollen.  

3.  Klicken Sie auf der Registerkarte **Startseite** auf **Status anzeigen**. Detaillierte Statusinformationen zur Verteilungspunktgruppe werden angezeigt.  

###  <a name="BKMK_DPConfigStatus"></a> Status der Verteilungspunktkonfiguration  
 Im Arbeitsbereich **Überwachung** finden Sie im Knoten **Status der Verteilungspunktkonfiguration** Informationen zum Verteilungspunkt. Sie können prüfen, welche Attribute für den Verteilungspunkt aktiviert sind, wie z. B. PXE, Multicast und Inhaltsprüfung. Außerdem können Sie detaillierte Statusinformationen zum Verteilungspunkt anzeigen. Gehen Sie wie folgt vor, um den Status einer Verteilungspunktkonfiguration anzuzeigen.  

#### <a name="to-monitor-distribution-point-configuration-status"></a>So überwachen Sie den Status einer Verteilungspunktkonfiguration  

1.  Wechseln Sie in der Configuration Manager-Konsole zu **Überwachung** > **Übersicht** > **Verteilungsstatus** > **Status der Verteilungspunktkonfiguration**. Die Verteilungspunkte werden angezeigt.  

2.  Wählen Sie den Verteilungspunkt aus, für den Statusinformationen angezeigt werden sollen.  

3.  Klicken Sie im Ergebnisbereich auf die Registerkarte **Details** . Statusinformationen zum Verteilungspunkt werden angezeigt.  
