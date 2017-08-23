---
title: "Allgemeine Aufgaben für Konfigurationsbaselines – Configuration Manager | Microsoft-Dokumentation"
description: Erfahren Sie, wie Sie System Center Configuration Manager-Konfigurationsbaselines erstellen und bereitstellen.
ms.custom: na
ms.date: 07/12/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4bb6afeb-d267-4f9b-ade2-26e5400c223b
caps.latest.revision: "6"
caps.handback.revision: "0"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 5bf4457af6bedf7bc9cd73c879f1857209c0725d
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="common-tasks-for-creating-and-deploying-configuration-baselines-with-system-center-configuration-manager"></a>Allgemeine Aufgaben zum Erstellen und Bereitstellen von Konfigurationsbaselines mit System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Dieses Thema enthält häufige Szenarios, mit deren Hilfe Sie mehr über das Erstellen und Bereitstellen von System Center Configuration Manager-Konfigurationsbaselines erfahren.  

 Wenn Sie bereits mit Konformitätseinstellungen vertraut sind, finden Sie eine ausführliche Dokumentation zu allen verwendbaren Funktionen in den Themen [Erstellen von Konfigurationsbaselines](../../compliance/deploy-use/create-configuration-baselines.md) und [Bereitstellen von Konfigurationsbaselines](../../compliance/deploy-use/deploy-configuration-baselines.md).  

 Bevor Sie beginnen, lesen Sie [Erste Schritte mit Konformitätseinstellungen](../../compliance/get-started/get-started-with-compliance-settings.md), um einige Grundlagen zu Konformitätseinstellungen zu erhalten. Lesen Sie zudem [Planen und Konfigurieren von Konformitätseinstellungen](../../compliance/plan-design/plan-for-and-configure-compliance-settings.md), um erforderliche Voraussetzungen zu implementieren.  

## <a name="create-a-configuration-baseline"></a>Erstellen einer Konfigurationsbaseline  
 In diesem Beispiel haben Sie ein Konfigurationselement ausschließlich für Windows 10-PCs erstellt, auf denen der Configuration Manager-Client ausgeführt wird.  

 Dieses Konfigurationselement erzwingt ein erforderliches Kennwort mit mindestens 6 Zeichen auf Windows 10-PCs. Das Konfigurationselement hat den Namen **Windows 10 Password Enforcement**.  

Mit dem folgenden Verfahren fügen Sie dieses Konfigurationselement zu einer Konfigurationsbaseline hinzu, um es für die Bereitstellung vorzubereiten.  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Assets und Konformität** > **Konformitätseinstellungen** > **Konfigurationsbaselines**.  

3.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Erstellen** auf **Konfigurationsbaseline erstellen**.  

4.  Konfigurieren Sie im Dialogfeld **Konfigurationsbaseline erstellen** die folgenden Einstellungen:  

    -   **Name** : Geben Sie **Windows 10 Passwords** (oder einen anderen Namen Ihrer Wahl) ein.  

5.  Klicken Sie auf **Hinzufügen** > **Konfigurationselemente**.  

6.  Wählen Sie im Dialogfeld **Konfigurationselemente hinzufügen** das zuvor erstellte Konfigurationselement **Windows 10 Password Enforcement** aus, und klicken Sie dann auf **Hinzufügen**.  

7.  Klicken Sie auf „OK“, um das Dialogfeld **Konfigurationselemente hinzufügen** zu schließen und zum Dialogfeld **Konfigurationsbaseline erstellen** zurückzukehren.

8.  Klicken Sie auf **OK** , um das Dialogfeld **Konfigurationsbaseline erstellen** zu schließen.  

 Sie sehen die Konfigurationsbaseline jetzt im Knoten **Konfigurationsbaselines** der Configuration Manager-Konsole.  

## <a name="deploy-the-configuration-baseline"></a>Bereitstellen der Konfigurationsbaseline  
 In diesem Beispiel stellen Sie die im vorherigen Verfahren erstellte Konfigurationsbaseline für eine Sammlung von Computern bereit.  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Assets und Konformität** > **Konformitätseinstellungen** > **Konfigurationsbaselines**.  

3.  Wählen Sie aus der Liste der Konfigurationsbaselines **Windows 10 Passwords**aus.  

4.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Bereitstellung** auf **Bereitstellen**.  

5.  Konfigurieren Sie im Dialogfeld **Konfigurationsbaselines bereitstellen** die folgenden Einstellungen:  

    -   **Ausgewählte Konfigurationsbaselines** : Stellen Sie sicher, dass die Konfigurationsbaseline **Windows 10 Passwords** automatisch dieser Liste hinzugefügt wurde.  

    -   **Nicht konforme Regeln wiederherstellen, falls dies unterstützt wird**: Aktivieren Sie dieses Kontrollkästchen, um sicherzustellen, dass die Einstellungen von Configuration Manager wiederhergestellt werden, falls auf Zielgeräten nicht die richtigen Einstellungen vorhanden sind.  

    -   **Sammlung**: Klicken Sie auf **Durchsuchen**, um die Sammlung von Computern auszuwählen, auf denen die Konfigurationsbaseline ausgewertet und die Konformität wiederhergestellt wird. In diesem Beispiel wurde die Konfigurationsbaseline für die integrierte Sammlung **Alle Desktop- und Serverclients** bereitgestellt.  

        > [!TIP]  
        >  Es ist unerheblich, ob die ausgewählte Sammlung Computer oder Geräte enthält, auf denen nicht Windows 10 ausgeführt wird. Solange Sie im erstellten Konfigurationselement unterstützte Plattformen konfiguriert haben, wird nur die Konformität von Windows 10-PCs ausgewertet.  

    -   Konfigurieren Sie bei Bedarf den Zeitplan, nach dem die Konfigurationsbaseline ausgewertet wird. Andernfalls behalten Sie die Standardeinstellung **7 Tage**bei.  

7.  Klicken Sie auf **OK** , um das Dialogfeld **Konfigurationsbaselines bereitstellen** zu schließen und die Bereitstellung zu erstellen.  

 Um einen kurzen Blick auf die Konformitätsstatistik für diese Bereitstellung zu werfen, klicken Sie im Arbeitsbereich **Überwachung** auf **Bereitstellungen**. Am unteren Bildschirmrand wird ein Diagramm zur **Konformitätsstatistik** angezeigt.  

## <a name="next-steps"></a>Nächste Schritte 

Ausführlichere Informationen zum Überwachen von Konfigurationsbaselines finden Sie unter [Überwachen von Konformitätseinstellungen](../../compliance/deploy-use/monitor-compliance-settings.md).  
