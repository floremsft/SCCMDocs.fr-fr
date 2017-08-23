---
title: Erstellen untergeordneter Konfigurationselemente | Microsoft-Dokumentation
description: Erstellen Sie untergeordnete Konfigurationselemente in System Center Configuration Manager.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 113984fa-6150-41a1-89ed-d2a83b979732
caps.latest.revision: "5"
caps.handback.revision: "0"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 33d4a2d5a09af74e1d76ac9b34a42b749f5bf7ef
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="how-to-create-child-configuration-items-in-system-center-configuration-manager"></a>Erstellen untergeordneter Konfigurationselemente in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Untergeordnete Konfigurationselemente in System Center Configuration Manager sind Kopien von Konfigurationselementen, die eine Beziehung zum ursprünglichen Konfigurationselement beibehalten: Sie erben die ursprüngliche Konfiguration vom übergeordneten Konfigurationselement.  

Wenn Sie in der Configuration Manager-Konsole die Eigenschaften eines untergeordneten Konfigurationselements anzeigen, können Sie die geerbten Objekte und Einstellungen mit den entsprechenden Überprüfungskriterien nicht bearbeiten. Sie können jedoch dem untergeordneten Konfigurationselement zusätzliche Überprüfungskriterien hinzufügen und diese anschließend bearbeiten. Außerdem können Sie dem untergeordneten Konfigurationselement auch neue Objekte und Einstellungen hinzufügen.
Das Erstellen und Bearbeiten eines untergeordneten Konfigurationselements dient üblicherweise dazu, das ursprüngliche Konfigurationselement für Ihre Unternehmensanforderungen zu optimieren.  

> [!NOTE]  
>  Sie können untergeordnete Konfigurationselemente nur von Konfigurationselementen des Typs **Windows-Desktops und -Server (benutzerdefiniert)**erstellen.  

## <a name="to-create-a-child-configuration-item"></a>So erstellen Sie ein untergeordnetes Konfigurationselement  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Bestand und Kompatibilität** > **Kompatibilitätseinstellungen** > **Konfigurationselemente**.  

3.  Wählen Sie in der Liste **Konfigurationselemente** das Konfigurationselement aus, für das Sie ein untergeordnetes Konfigurationselement erstellen möchten, und klicken Sie dann auf der Registerkarte **Startseite** in der Gruppe **Konfigurationselement** auf **Untergeordnetes Konfigurationselement erstellen**.  

4.  Auf der Seite **Allgemein** des **Assistenten zum Erstellen untergeordneter Konfigurationselemente**können Sie eine spezifische Revision des übergeordneten Konfigurationselements auswählen, aus der das untergeordnete Konfigurationselement erstellt werden soll. Andere Schritte des Assistenten sind identisch mit denen zum Erstellen eines Standardkonfigurationselements. Weitere Informationen finden Sie unter [Erstellen benutzerdefinierter Konfigurationselemente für Windows-Desktop- und -Servercomputer](../../compliance/deploy-use/create-custom-configuration-items-for-windows-desktop-and-server-computers-managed-with-the-client.md).  

5.  Schließen Sie den Assistenten ab. Das neue untergeordnete Konfigurationselement wird in der Liste **Konfigurationselemente** angezeigt.  
