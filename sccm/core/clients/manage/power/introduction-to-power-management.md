---
title: "Einführung in die Energieverwaltung | Microsoft-Dokumentation"
description: "Erhalten Sie eine Einführung in die Energieverwaltung in System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3ddff2a7-99eb-4ef8-b969-f3f7f24053db
caps.latest.revision: "4"
caps.handback.revision: "0"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: f46c9479021c814b1102d72c7d493f21a7243bf1
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="introduction-to-power-management-in-system-center-configuration-manager"></a>Einführung in die Energieverwaltung in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Die Energieverwaltung in System Center Configuration Manager entspricht dem Bedarf zahlreicher Organisationen, den Energieverbrauch ihrer Computer zu überwachen und zu senken. Von der Funktion werden die Energieverwaltungsfunktionen von Windows genutzt, um relevante sowie konsistente Einstellungen auf die Computer der Organisation anzuwenden. Innerhalb und außerhalb der Geschäftszeiten lassen sich unterschiedliche Energieeinstellungen auf die Computer anwenden. Beispielsweise kann außerhalb der Geschäftszeiten ein restriktiverer Energiesparplan erwünscht sein. Wenn es Computer gibt, die stets eingeschaltet bleiben sollen, können Sie verhindern, dass die Energieverwaltungseinstellungen angewendet werden.  

 In der Energieverwaltung in Configuration Manager sind verschiedene Berichte enthalten, um die Analyse von Energieverbrauch und Energieeinstellungen der Computer Ihrer Organisation zu vereinfachen. Die Berichte können auch zur Problembehandlung bei der Energieverwaltung verwendet werden.  

 Einen ausführlichen Workflow zum Konfigurieren und Verwenden der Energieverwaltung finden Sie unter [Administratorcheckliste für die Energieverwaltung in System Center Configuration Manager](../../../../core/clients/manage/power/administrator-checklist-for-power-management.md).  

> [!IMPORTANT]  
>  Die Configuration Manager-Energieverwaltung wird nicht auf virtuellen Computern unterstützt. Auf virtuelle Maschinen lassen sich keine Energiesparpläne anwenden, und von virtuellen Maschinen werden keine Energieberichtsdaten geliefert.  

## <a name="the-power-management-workflow"></a>Workflow bei der Energieverwaltung  
 Planen Sie die Energieverwaltung, und implementieren Sie sie in den folgenden drei Phasen in Configuration Manager.  

### <a name="monitoring-and-planning-phase"></a>Überwachungs- und Planungsphase  
 Von der Energieverwaltung wird die Configuration Manager-Hardwareinventur zum Sammeln von Daten über Verwendung und Energieeinstellungen der Standortcomputer verwendet. Sie können mehrere Berichte verwenden, um diese Daten zu analysieren und die optimalen Energieverwaltungseinstellungen für die Computer zu bestimmen. Beispielsweise können Sie in der Überwachungs- und Planungsphase des Energieverwaltungs-Workflows Sammlungen auf Basis der Daten erstellen, die im Bericht **Energiefunktionen** enthalten sind, und sie zur Identifikation von Computern verwenden, bei denen keine Energieverwaltung möglich ist. Dann können Sie diese Computer von der Energieverwaltung ausschließen.  

> [!IMPORTANT]  
>  Wenden Sie keine Energiesparpläne auf Computer in Ihrem Standort an, bevor Sie die Energiedaten der Clientcomputer gesammelt und ausgewertet haben. Wenn Sie neue Energieverwaltungseinstellungen auf Computer anwenden, ohne die bestehenden Einstellungen zu untersuchen, könnten Sie einen Anstieg im Energieverbrauch erleben.  

### <a name="enforcement-phase"></a>Erzwingungsphase  
 Mit der Energieverwaltung können Sie Energiesparpläne erstellen und auf Sammlungen von Computern des Standorts anwenden. Von diesen Energiesparplänen werden die Einstellungen der Windows-Energieverwaltung auf den Computern konfiguriert. Sie können die Energiesparpläne verwenden, die in Configuration Manager integriert sind, oder Ihre eigenen benutzerdefinierten Energiesparpläne konfigurieren. Sie können die Energiedaten, die in der Überwachungs- und Planungsphase gesammelt wurden, als Basislinie verwenden, um die Energieeinsparungen nach Anwendung des Energiesparplans auf die Computer zu beurteilen. Weitere Informationen finden Sie unter [Administratorcheckliste für die Energieverwaltung in System Center Configuration Manager](../../../../core/clients/manage/power/administrator-checklist-for-power-management.md).  

### <a name="compliance-phase"></a>Kompatibilitätsphase  
 In der Kompatibilitätsphase können Sie Berichte ausführen, die Ihnen bei der Beurteilung des Energieverbrauchs und der Energiekosteneinsparungen in Ihrem Unternehmen helfen. Zudem können Sie Berichte ausführen, die Optimierungen beim CO2-Ausstoß von Computern dokumentieren. Anhand weiterer Berichte können Sie überprüfen, ob die Energieeinstellungen korrekt auf die Computer angewendet wurden. Sie können die Berichte auch zur Problembehandlung bei der Energieverwaltungsfunktion nutzen.  
