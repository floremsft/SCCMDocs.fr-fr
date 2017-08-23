---
title: Simulieren von Anwendungsbereitstellungen | Microsoft-Dokumentation
description: "Bewerten Sie die Erkennungsmethode, Anforderungen und Abhängigkeiten für einen Bereitstellungstyp, ohne die Anwendung zu installieren."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 28b240a4-d358-40ce-8006-c697b1622ece
caps.latest.revision: "6"
caps.handback.revision: "0"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: b06539ded21eac71dda7da89dae96fda7a801260
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="simulate-application-deployments-with-system-center-configuration-manager"></a>Simulieren von Anwendungsbereitstellungen mit System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Sie können simulierte Bereitstellungen verwenden, um eine Anwendungsbereitstellung zu testen, ohne die Anwendung zu installieren oder zu deinstallieren. Eine simulierte Bereitstellung bewertet die Erkennungsmethode, die Anforderungen und die Abhängigkeiten für einen Bereitstellungstyp. Zeigen Sie die Ergebnisse im Arbeitsbereich **Überwachung** im Knoten **Bereitstellungen** an. Gehen Sie zum Simulieren einer Anwendungsbereitstellung in System Center Configuration Manager (Configuration Manager) wie in diesem Thema beschrieben vor.  

> [!NOTE]  
> Die Verwendung von simulierten Bereitstellungen für Sammlungen von mobilen Geräten ist nicht möglich.  
>   
> Sie können eine Anwendung mit dem Bereitstellungszweck **Deinstallieren** nicht bereitstellen, wenn bereits eine simulierte Bereitstellung der gleichen Anwendung aktiv ist.  

## <a name="configure-a-simulated-application-deployment"></a>Konfigurieren einer simulierten Anwendungsbereitstellung

1.  Wählen Sie in der Configuration Manager-Konsole eines der folgenden Elemente aus:  
    -   Eine Sammlung von Benutzern  
    -   Eine Sammlung von Geräten  
    -   Eine Configuration Manager-Anwendung  

2.  Wählen Sie auf der Registerkarte **Startseite** in der Gruppe **Bereitstellung** die Option **Bereitstellung simulieren** aus.  

3.  Legen Sie die folgenden Details für die simulierte Bereitstellung im Assistenten zum Simulieren der Anwendungsbereitstellung fest:  

    -   **Anwendung**. Wählen Sie **Durchsuchen** aus, und wählen Sie dann die Anwendung aus, für die Sie eine simulierte Bereitstellung erstellen möchten.  

    -   **Sammlung**. Wählen Sie **Durchsuchen** aus, und wählen Sie dann die Sammlung aus, die Sie für die simulierte Bereitstellung verwenden möchten.  

    -   **Aktion**. Wählen Sie in der Dropdownliste aus, ob Sie das Installieren oder das Deinstallieren der ausgewählten Anwendung simulieren möchten.  

    -   **Automatisch mit oder ohne Benutzeranmeldung bereitstellen**. Wenn diese Option aktiviert ist, wird die simulierte Bereitstellung von den Clients unabhängig davon ausgewertet, ob diese angemeldet sind.  

4.  Klicken Sie auf **Weiter**, überprüfen Sie die Informationen auf der Seite **Zusammenfassung**, und schließen Sie dann den Assistenten zum Simulieren der Anwendungsbereitstellung ab.  

5.  Simulierte Anwendungen werden im Arbeitsbereich **Überwachung** im Knoten **Bereitstellungen** mit dem Bereitstellungszweck **Simulieren** angezeigt. Weitere Informationen zum Überwachen von Anwendungsbereitstellungen finden Sie unter [Überwachen von Anwendungen in der System Center Configuration Manager-Konsole](../../apps/deploy-use/monitor-applications-from-the-console.md).  
