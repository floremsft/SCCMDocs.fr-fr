---
title: "Sicherheit und Datenschutz für die Migration | Microsoft-Dokumentation"
description: "Hier finden Sie bewährte Sicherheitsmethoden und Datenschutzinformationen für die Migration zur System Center Configuration Manager-Umgebung."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6893fce1-7ad5-4151-9ba9-3096871e8e4a
caps.latest.revision: "5"
caps.handback.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 8aa6971d75924ab5bcacd70c330913097ecf8717
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="security-and-privacy-for-migration-to-system-center-configuration-manager"></a>Sicherheit und Datenschutz für die Migration zu System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Dieses Thema enthält bewährte Sicherheitsmethoden und Datenschutzinformationen zur Migration zur System Center Configuration Manager-Umgebung.  

## <a name="security-best-practices-for-migration"></a>Bewährte Sicherheitsmethoden für die Migration  
 Wenden Sie die folgende bewährte Sicherheitsmethode bei der Migration an.  

|Bewährte Sicherheitsmethode|Weitere Informationen|  
|----------------------------|----------------------|  
|Verwenden Sie statt eines Benutzerkontos das Computerkonto für SMS-Anbieterkonto und SQL Server-Konto des Quellstandorts.|Wenn Sie zur Migration ein Benutzerkonto verwenden müssen, entfernen Sie nach Abschluss der Migration die Kontodetails.|  
|Verwenden Sie IPsec, wenn Sie Inhalte von einem Verteilungspunkt an einem Quellstandort zu einem Verteilungspunkt Ihres Zielstandorts migrieren.|Auf die migrierten Inhalte wird zwar ein Hashwert angewendet, um Manipulationen festzustellen, doch wenn die Daten während der Übertragung geändert werden, kann die Migration nicht ausgeführt werden.|  
|Überwachen Sie die Administratoren, die Migrationsaufträge erstellen können, und beschränken Sie ihre Anzahl.|Die Integrität der Zielhierarchiedatenbank hängt von der Integrität der Daten ab, die der Administrator für den Import aus der Quellhierarchie auswählt. Außerdem kann dieser Administrator alle Daten der Quellhierarchie lesen.|  

### <a name="security-issues-for-migration"></a>Sicherheitsprobleme bei der Migration  
Die Migration birgt folgende Sicherheitsprobleme:  

-   Clients, für die der Zugriff auf einen Quellstandort gesperrt ist, können ggf. der Zielhierarchie zugewiesen werden, bevor ihr Clientdatensatz migriert wird.  

     Obwohl Configuration Manager den Status „Gesperrt“ eines Clients bei der Migration beibehält, kann der Client der Zielhierarchie zugewiesen werden, wenn die Zuweisung erfolgt, bevor die Migration des Clientdatensatzes abgeschlossen ist.  

-   Überwachungsmeldungen werden nicht migriert.  

Wenn Sie Daten von einem Quellstandort zu einem Zielstandort migrieren, gehen alle Überwachungsinformationen der Quellhierarchie verloren.  

## <a name="privacy-information-for-migration"></a>Datenschutzinformationen zur Migration  
 Bei der Migration werden Informationen in den Standortdatenbanken ermittelt, die Sie in einer Quellinfrastruktur identifizieren, und in der Datenbank der Zielhierarchie gespeichert. Welche Informationen von System Center Configuration Manager für einen Quellstandort oder eine Quellhierarchie ermittelt werden können, richtet sich nach den Features, die in der Quellumgebung aktiviert wurden. Außerdem ist dies von den Verwaltungsvorgängen abhängig, die in der Quellumgebung ausgeführt wurden.  

 Weitere Informationen zu Sicherheit und Datenschutz finden Sie unter folgenden Themen:  

-   Weitere Informationen zum Configuration Manager 2007-Datenschutz finden Sie unter [Sicherheit und Datenschutz für Configuration Manager 2007](http://go.microsoft.com/fwlink/p/?LinkId=216450) in der Configuration Manager 2007-Dokumentationsbibliothek.  

-   Weitere Informationen zum System Center 2012 Configuration Manager-Datenschutz finden Sie unter [Sicherheit und Datenschutz für System Center 2012 Configuration Manager](https://technet.microsoft.com/library/gg682033.aspx) in der System Center 2012 Configuration Manager-Dokumentationsbibliothek.  

-   Weitere Informationen zum System Center Configuration Manager-Datenschutz finden Sie unter [Sicherheit und Datenschutz für System Center Configuration Manager](../../core/plan-design/security/security-and-privacy.md).  

Sie können einige oder alle unterstützten Daten von einem Quellstandort zu einer Zielhierarchie migrieren.  

Die Migration ist in der Standardeinstellung nicht aktiviert und erfordert mehrere Konfigurationsschritte. Es werden keine Migrationsinformationen an Microsoft gesendet.  

Berücksichtigen Sie Ihre Datenschutzanforderungen, bevor Sie Daten aus einer Quellhierarchie migrieren.  
