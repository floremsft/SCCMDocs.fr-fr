---
title: Benutzerdefinierte Datenbank-Dateispeicherorte | Microsoft-Dokumentation
description: "Erfahren Sie, wie Sie benutzerdefinierte Speicherorte für SQL Server-Datenbankdateien angeben."
ms.custom: na
ms.date: 10/06/2016
ms.reviewer: na
ms.suite: na
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 500a9aa6-68aa-44eb-bf49-350c1314a697
caps.latest.revision: "3"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: cfac2c03c1b71b40c68d8acd5fbd96c5e98caaa9
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="custom-locations-for-system-center-configuration-manager-site-database-files"></a>Benutzerdefinierte Dateispeicherorte für Standortdatenbanken mit System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

 System Center Configuration Manager unterstützt benutzerdefinierte Speicherorte für SQL Server-Datenbankdateien.  

> [!NOTE]  
>  Die Option zur Angabe der vom Standard abweichenden Speicherorte ist nicht verfügbar, wenn Sie einen SQL Server-Cluster verwenden.  

 **Während des Setups** eines neuen primären Standorts oder eines Standorts der zentralen Verwaltung haben Sie folgende Möglichkeiten:  

-   **Angeben nicht standardmäßiger Dateispeicherorte für die Standortdatenbank**: Das Configuration Manager-Setup erstellt dann die Standortdatenbank anhand dieser Speicherorte.  

-   **Angeben der Nutzung einer vorab erstellten SQL Server-Datenbank, die benutzerdefinierte Dateispeicherorte verwendet**: Das Configuration Manager-Setup nutzt dann diese vorab erstellte Datenbank und ihre vorkonfigurierten Dateispeicherorte.  

**Nach dem Setup** können Sie den Speicherort der Standortdatenbankdateien ändern. Dazu müssen Sie den Standort beenden und den Dateispeicherort in SQL Server bearbeiten:  

-   Beenden Sie auf dem Configuration Manager-Standortserver den Dienst **SMS_Executive**.  

-   Verwenden Sie die Dokumentation für Ihre Version von SQL Server, in der Sie Anweisungen zum Verschieben einer Benutzerdatenbank finden. Wenn Sie beispielsweise SQL Server 2014 nutzen, lesen Sie [Verschieben von Benutzerdatenbanken](https://technet.microsoft.com/library/ms345483\(v=sql.120\).aspx) in TechNet.  

-   Starten Sie nach dem Verschieben der Datenbankdateien den Dienst **SMS_Executive** auf dem Configuration Manager-Standortserver neu.  
