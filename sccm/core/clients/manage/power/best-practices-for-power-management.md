---
title: "Bewährte Methoden für die Energieverwaltung | Microsoft-Dokumentation"
description: "Erhalten Sie bewährte Methoden für die Energieverwaltung in System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9f7142e1-c972-4384-853b-2da1568cb3e3
caps.latest.revision: "5"
caps.handback.revision: "0"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: d3cc24c7923141f039dcda26ac27489cb0143e89
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="best-practices-for-power-management-in-system-center-configuration-manager"></a>Bewährte Methoden für die Energieverwaltung in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Verwenden Sie folgende bewährte Methoden für die Energieverwaltung in System Center Configuration Manager.  

## <a name="perform-the-monitoring-phase-at-a-representative-time"></a>Durchführen der Überwachungsphase zu einer repräsentativen Zeit  
 Die Überwachungsphase der Energieverwaltung bietet Ihnen Informationen zu Energieverbrauch, Aktivität, Energieverwaltungsfunktionen und Umweltbelastung der Computer in Ihrer Organisation. Achten Sie darauf, für die Überwachungsphase eine repräsentative Zeit zu wählen. Wenn Sie für die Überwachungsphase beispielsweise einen Feiertag wählen, kann kein realistischer Bericht zum Energieverbrauch erstellt werden.  

## <a name="create-a-control-collection-of-computers-with-no-power-plans-applied"></a>Erstellen einer Kontrollsammlung von Computern, auf die keine Energiesparpläne angewendet werden  
 Erstellen Sie zwei Sammlungen von Computern, mit denen Sie überwachen, wie sich die Anwendung von Energiesparplänen auf Computer auswirkt. Die erste Sammlung muss die Mehrzahl der Computer enthalten, auf die Energieeinstellungen angewendet werden sollen. Die andere Sammlung dient als Kontrollsammlung und enthält die übrigen Computer. Wenden Sie den erforderlichen Energieverwaltungsplan auf die Sammlung an, die die Mehrzahl der Computer enthält. Sie können dann Berichte ausführen, um die Computer mit Energieeinstellungen hinsichtlich Energiekosten, Energieverbrauch und Umweltbelastung mit der Kontrollsammlung ohne Energieeinstellungen zu vergleichen.  

## <a name="run-the-power-settings-report-before-you-apply-a-power-management-plan"></a>Ausführen des Berichts "Energieeinstellungen" vor dem Anwenden eines Energieverwaltungsplans  
 Bevor Sie einen Energieverwaltungsplan auf eine Computersammlung anwenden, führen Sie den Bericht **Energieeinstellungen** aus, um die Energieverwaltungseinstellungen zu erfassen, die auf den Computern der Sammlung bereits konfiguriert sind. Wenn Sie neue Energieverwaltungseinstellungen auf Computer anwenden, ohne die bestehenden Einstellungen zu untersuchen, könnte dies zu einem Anstieg im Energieverbrauch führen.  

## <a name="exclude-servers-from-power-management"></a>Ausschließen von Servern aus der Energieverwaltung  
 Die Energieverwaltung auf Computern, auf denen Windows Server ausgeführt wird, wird nicht unterstützt (obwohl Daten über den Energieverbrauch gesammelt werden). Fügen Sie einer Sammlung Server hinzu, und schließen Sie diese aus der Energieverwaltung aus.  

## <a name="exclude-computers-that-you-do-not-want-to-manage"></a>Ausschließen von Computern, die nicht verwaltet werden sollen  
 Wenn auf manche Computer keine Energieverwaltung angewendet werden soll, fügen Sie diese Computer zu einer Sammlung hinzu, die Sie von der Energieverwaltung ausschließen.  

 Beispiele für Computer, die Sie ggf. aus der Energieverwaltung ausschließen sollten:  

-   Computer, die eingeschaltet bleiben müssen.  

-   Computer, mit denen Benutzer eine Remotedesktopverbindung herstellen müssen  

-   Computer, für die die Energieverwaltung nicht verwendet werden kann  

-   Computer mit der Standortsystemrolle "Verteilungspunkt"  

-   Öffentliche Computer wie Kioskcomputer, Informationsanzeigen oder Überwachungskonsolen, bei denen Computer und Monitor stets eingeschaltet bleiben müssen  

 Weitere Informationen finden Sie unter [Configuring Power Management in Configuration Manager (Konfigurieren der Energieverwaltung in System Center Configuration Manager)](../../../../core/clients/manage/power/configuring-power-management.md).  

## <a name="first-apply-power-plans-to-a-test-collection-of-computers"></a>Anwenden von Energiesparplänen zunächst nur auf eine Testsammlung von Computern  
 Testen Sie die Auswirkungen von Energieverwaltungsplänen stets zuerst an einer Testsammlung von Computern, bevor sie die Energieverwaltungspläne auf größere Computersammlungen anwenden.  

 Energieeinstellungen, die auf Computer mit Windows XP oder Windows Server 2003 angewendet werden, werden auch dann nicht auf ihre ursprünglichen Werte zurückgesetzt, wenn die Computer aus der Energieverwaltung ausgeschlossen werden. Bei späteren Versionen von Windows bewirkt das Ausschließen eines Computers aus der Energieverwaltung, dass sämtliche Energieeinstellungen auf ihre ursprünglichen Werte zurückgesetzt werden. Es können keine einzelnen Energieeinstellungen auf ihre ursprünglichen Werte zurückgesetzt werden.  

## <a name="apply-power-plan-settings-individually"></a>Anwenden von Energiesparplaneinstellungen auf einzelne Computer  
 Überwachen Sie die Auswirkungen jeder Energieeinstellung, bevor Sie die nächste anwenden, um zu gewährleisten, dass jede Einstellung die gewünschte Wirkung hat. Weitere Informationen zu Energiesparplaneinstellungen, finden Sie unter [Available Power Management Plan Settings (Verfügbare Einstellungen des Energieverwaltungsplans)](../../../../core/clients/manage/power/create-and-apply-power-plans.md#BKMK_Plans)im Thema [How to Create and Apply Power Plans in Configuration Manager (Erstellen und Anwenden von Energiesparplänen in System Center Configuration Manager)](../../../../core/clients/manage/power/create-and-apply-power-plans.md).  

## <a name="regularly-monitor-computers-to-see-if-they-have-multiple-power-plans-applied"></a>Regelmäßige Überprüfung der Computer darauf, ob mehrere Energiesparpläne auf sie angewendet wurden  
 Die Energieverwaltung umfasst einen Bericht, der Computer anzeigt, auf die mehr als ein Energiesparplan angewendet wird.  

 Wenn ein Computer mehreren Sammlungen angehört, für die unterschiedliche Energiesparpläne verwendet werden, werden folgende Aktionen durchgeführt:  

-   Energiesparplan: Wenn auf einen Computer mehrere Werte für Energieeinstellungen angewendet werden, wird der am wenigsten restriktive Wert verwendet.  

-   Aktivierungszeit: Wenn auf einen Desktopcomputer mehrere Aktivierungszeiten angewendet werden, wird die Uhrzeit verwendet, die am nächsten an Mitternacht liegt.  

     Weitere Informationen finden Sie unter [Computers with Multiple Power Plans (Computer mit mehreren Energiesparplan)](../../../../core/clients/manage/power/monitor-and-plan-for-power-management.md#BKMK_Multiple) im Thema [How to Monitor and Plan for Power Management in Configuration Manager (Überwachen und Planen der Energieverwaltung in System Center Configuration Manager)](../../../../core/clients/manage/power/monitor-and-plan-for-power-management.md). Weitere Informationen zur Konfliktlösung durch die Energieverwaltung finden Sie unter [How to Create and Apply Power Plans in Configuration Manager (Erstellen und Anwenden von Energiesparplänen in System Center Configuration Manager)](../../../../core/clients/manage/power/create-and-apply-power-plans.md).  

## <a name="save-or-export-power-management-information-during-the-monitoring-and-planning-phase-of-power-management"></a>Speichern oder Exportieren von Energieverwaltungsinformationen während der Überwachungs- und Planungsphase der Energieverwaltung  
 Energieverwaltungsinformationen, die für Tagesberichte verwendet werden, bleiben 31 Tage lang in der Configuration Manager-Standortdatenbank gespeichert.  

 Energieverwaltungsinformationen, die für Monatsberichte verwendet werden, bleiben 13 Monate lang in der Configuration Manager-Standortdatenbank gespeichert.  

 Wenn Sie während der Überwachungs- und Planungsphase bzw. während der Kompatibilitätsphase der Energieverwaltung Berichte ausführen, dann speichern oder exportieren Sie die Ergebnisse aller Berichte, deren Daten Sie zum späteren Vergleich behalten möchten, für den Fall, dass sie später von Configuration Manager entfernt werden.  
