---
title: Migrieren von Daten | Microsoft-Dokumentation
description: "Erfahren Sie, wie Sie Daten aus einer Quellhierarchie in eine Zielhierarchie in System Center Configuration Manager übertragen."
ms.custom: na
ms.date: 12/29/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: cf014eb0-f8c2-4d37-b8d7-368d63a10b89
caps.latest.revision: "11"
caps.handback.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: dface33392c2a2a662522656eabf0936b52b28fc
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="migrate-data-between-hierarchies-in-system-center-configuration-manager"></a>Migrieren von Daten zwischen Hierarchien in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Verwenden Sie die Migration, um Daten aus einer unterstützten Quellhierarchie in Ihre Zielhierarchie in System Center Configuration Manager zu übertragen.  Wenn Sie Daten aus einer Quellhierarchie migrieren:  

-   Sie greifen auf Daten aus den Standortdatenbanken zu, die Sie in der Quellinfrastruktur identifizieren, und übertragen diese Daten dann in die aktuelle Umgebung.  

-   Durch eine Migration werden keine Daten in der Quellhierarchie verändert, sondern die Daten werden ermittelt, und eine Kopie davon wird in der Datenbank der Zielhierarchie gespeichert.  

Berücksichtigen Sie bei der Planung Ihrer Migrationsstrategie die folgenden Punkte:  

-   Sie können eine vorhandene Configuration Manager 2007 SP2-Infrastruktur zu System Center Configuration Manager migrieren.  

-   Sie können einige oder alle unterstützten Daten von einem Quellstandort migrieren.  

-   Sie können die Daten eines einzelnen Quellstandorts zu mehreren unterschiedlichen Standorten in der Zielhierarchie migrieren.  

-   Sie können Daten von mehreren Quellstandorten an einen einzelnen Standort in der Zielhierarchie verschieben.  

##  <a name="BKMK_MigrationConcepts"></a> Konzepte für die Migration  
 Bei einer Migration werden Ihnen möglicherweise die folgenden Konzepte und Begriffe begegnen.  

|Konzept oder Begriff|Weitere Informationen|  
|---------------------|----------------------|  
|Quellhierarchie|Eine Hierarchie mit einer unterstützten Configuration Manager-Version, in der zu migrierende Daten enthalten sind. Beim Einrichten einer Migration legen Sie die Quellhierarchie fest, wenn Sie den Standort der obersten Ebene der Quellhierarchie angeben. Nachdem Sie eine Quellhierarchie angegeben haben, werden am Standort auf oberster Ebene Daten aus der Datenbank des bezeichneten Quellstandorts gesammelt, um die überführbaren Daten zu identifizieren.<br /><br /> Weitere Informationen finden Sie im Abschnitt [Quellhierarchien](../../core/migration/planning-a-source-hierarchy-strategy.md#BKMK_Source_Hierarchies) des Themas [Planen einer Strategie für Quellhierarchien in System Center Configuration Manager](../../core/migration/planning-a-source-hierarchy-strategy.md).|  
|Quellstandorte|Standorte in der Quellhierarchie mit Daten, die zur Zielhierarchie migriert werden können.<br /><br /> Weitere Informationen finden Sie im Abschnitt [Quellstandorte](../../core/migration/planning-a-source-hierarchy-strategy.md#BKMK_Source_Sites) des Themas [Planen einer Strategie für Quellhierarchien in System Center Configuration Manager](../../core/migration/planning-a-source-hierarchy-strategy.md).|  
|Zielhierarchie|Eine Hierarchie in System Center Configuration Manager, in die bei der Migration Daten aus einer Quellhierarchie importiert werden.|  
|Datensammlung|Fortlaufender Vorgang zur Identifikation der Informationen in einer Quellhierarchie, die zur Zielhierarchie migriert werden können. Configuration Manager überprüft die Quellhierarchie nach einem Zeitplan, um Änderungen an Informationen in der Quellhierarchie zu erkennen, die zuvor migriert wurden und die möglicherweise in der Zielhierarchie aktualisiert werden sollen.<br /><br /> Weitere Informationen finden Sie im Abschnitt [Datensammlung](../../core/migration/planning-a-source-hierarchy-strategy.md#BKMK_Data_Gathering) des Themas [Planen einer Strategie für Quellhierarchien in System Center Configuration Manager](../../core/migration/planning-a-source-hierarchy-strategy.md).|  
|Migrationsaufträge|Prozess, mit dem die zu migrierenden Objekte festgelegt ^werden und die Objektmigration zur Zielhierarchie verwaltet wird.<br /><br /> Weitere Informationen finden Sie unter [Planen einer Strategie für Migrationsaufträge in System Center Configuration Manager](../../core/migration/planning-a-migration-job-strategy.md)|  
|Clientmigration|Prozess, mit dem von Clients verwendete Daten aus der Datenbank des Quellstandorts in die der Zielhierarchie übertragen werden. Auf diese Datenmigration folgt dann die Aktualisierung der auf Geräten installierten Clientsoftware auf die Version der Zielhierarchie.<br /><br /> Weitere Informationen finden Sie unter [Planen einer Strategie für Migrationsaufträge in System Center Configuration Manager](../../core/migration/planning-a-client-migration-strategy.md).|  
|Freigegebene Verteilungspunkte|Die Verteilungspunkte aus der Quellhierarchie, die in der Migrationsphase für die Zielhierarchie freigegeben werden.<br /><br /> Während der Migrationsphase können Clients, die Standorten in der Zielhierarchie zugewiesen sind, Inhalte von freigegebenen Verteilungspunkten erhalten.<br /><br /> Weitere Informationen finden Sie im Abschnitt [Freigeben von Verteilungspunkten zwischen Quell- und Zielhierarchien](../../core/migration/planning-a-content-deployment-migration-strategy.md#About_Shared_DPs_in_Migration) des Themas [Planen einer Migrationsstrategie für die Inhaltsbereitstellung in System Center Configuration Manager](../../core/migration/planning-a-content-deployment-migration-strategy.md).|  
|Migrationsüberwachung|Überwachen der Migrationsaktivitäten. Sie überwachen den Migrationsfortschritt und -erfolg im Arbeitsbereich **Verwaltung** unter dem Knoten **Migration**.<br /><br /> Weitere Informationen finden Sie unter [Planen der Überwachung der Migrationsaktivitäten in System Center Configuration Manager](../../core/migration/planning-to-monitor-migration-activity.md).|  
|Sammeln von Daten beenden|Das Beenden der Datensammlung von Quellstandorten. Wenn keine weiteren Daten mehr aus einer Quellhierarchie migriert oder die Migrationsaktivitäten angehalten werden sollen, kann die Zielhierarchie entsprechend konfiguriert werden, dass die Datensammlung in der Quellhierarchie beendet wird.<br /><br /> Weitere Informationen finden Sie im Abschnitt [Datensammlung](../../core/migration/planning-a-source-hierarchy-strategy.md#BKMK_Data_Gathering) des Themas [Planen einer Strategie für Quellhierarchien in System Center Configuration Manager](../../core/migration/planning-a-source-hierarchy-strategy.md).|  
|Bereinigung der Migrationsdaten|Das Abschließen der Migration von einer Quellhierarchie durch Entfernen von migrationsbezogenen Informationen aus der Datenbank der Zielhierarchie.<br /><br /> Weitere Informationen finden Sie unter [Planen des Abschließens der Migration in System Center Configuration Manager](../../core/migration/planning-to-complete-migration.md).|  

## <a name="typical-workflow-for-migration"></a>Typischer Workflow bei der Migration  
So richten Sie einen typischen Workflows bei der Migration ein:

1.  Geben Sie eine unterstützte Quellhierarchie an.  

2.  Richten Sie die Datensammlung ein. Mithilfe der Datensammlung kann Configuration Manager Informationen zu Daten sammeln, die aus der Quellhierarchie migriert werden können.  

     Der Prozess der Datensammlung wird bei Configuration Manager nach einem einfachen Zeitplan automatisch wiederholt, bis Sie den Vorgang beenden. Standardmäßig wird der Datensammlungsprozess alle vier Stunden wiederholt, damit Configuration Manager Änderungen der ggf. zu migrierenden Daten in der Quellhierarchie identifizieren kann. Die Datensammlung ist auch erforderlich, um Verteilungspunkte der Quellhierarchie für die Zielhierarchie freizugeben.  

3.  Erstellen Sie Migrationsaufträge zum Migrieren von Daten zwischen der Quell- und Zielhierarchie.  

4.  Sie können den Datensammlungsprozess mit dem Befehl **Sammeln von Daten beenden** jederzeit beenden. Wenn Sie das Sammeln von Daten beenden, ermittelt Configuration Manager keine Änderungen der Daten in der Quellhierarchie mehr, und Verteilungspunkte können von den Quell- und Zielhierarchien nicht mehr gemeinsam genutzt werden. Normalerweise verwenden Sie diese Aktion, wenn Sie keine Daten mehr migrieren oder Verteilungspunkte der Quellhierarchie mehr freigeben möchten.  

5.  Nachdem die Datensammlung an allen Standorten der Quellhierarchie beendet wurde, können Sie optional den Befehl **Migrationsdaten bereinigen** verwenden, um die Migrationsdaten zu bereinigen. Mit diesem Befehl werden die Verlaufsdaten der Migration aus einer Quellhierarchie aus der Datenbank der Zielhierarchie gelöscht.  

Nach dem Migrieren von Daten aus einer Configuration Manager-Quellhierarchie, die Sie nicht mehr zum Verwalten der Umgebung verwenden, können Sie die diese Quellhierarchie und Infrastruktur außer Betrieb setzen.  

##  <a name="BKMK_MigrationScenarios"></a> Migrationsszenarien  
 Configuration Manager unterstützt die folgenden Migrationsszenarien.  

> [!NOTE]  
>  Der Erweiterung einer Hierarchie, die einen eigenständigen Standort enthält, in eine Hierarchie mit einem Standort der zentralen Verwaltung wird nicht als Migration bezeichnet. Informationen zur Standorterweiterung finden Sie unter [Erweitern eines eigenständigen primären Standorts](../../core/servers/deploy/install/use-the-setup-wizard-to-install-sites.md#bkmk_expand) im Thema [Verwenden des Setup-Assistenten zum Installieren von System Center Configuration Manager-Standorten](../../core/servers/deploy/install/use-the-setup-wizard-to-install-sites.md).  

### <a name="migration-from-configuration-manager-2007-hierarchies"></a>Migration aus Configuration Manager 2007-Hierarchien  
 Durch Verwendung der Migrationsfunktion zum Migrieren von Daten aus Configuration Manager 2007 können Sie Ihre Investition in die bestehende Standortinfrastruktur sichern und die folgenden Vorteile erzielen:  

|Vorteil|Weitere Informationen|  
|-------------|----------------------|  
|Verbesserungen der Standortdatenbank|Die System Center Configuration Manager-Datenbank unterstützt Unicode uneingeschränkt.|  
|Datenbankreplikation zwischen Standorten|Die Replikation in System Center Configuration Manager basiert auf Microsoft SQL Server. Dies führt bei der Datenübertragung zwischen Standorten zu einer besseren Leistung.|  
|Benutzerzentrierte Verwaltung|Benutzer stehen im Mittelpunkt von Verwaltungstasks in System Center Configuration Manager. Beispielsweise können Sie Software an einen Benutzer verteilen, auch wenn Ihnen der Gerätename für diesen Benutzer nicht bekannt ist. Außerdem haben die Benutzer bei System Center Configuration Manager deutlich mehr Kontrolle darüber, welche Software wann auf ihren Geräten installiert wird.|  
|Vereinfachte Hierarchie|Der Standorttyp mit zentraler Verwaltung sowie Änderungen am Verhalten primärer und sekundärer Standorte in System Center Configuration Manager erlauben eine vereinfachte Standorthierarchie, die weniger Netzwerkbandbreite belegt und weniger Server erfordert.|  
|Rollenbasierte Verwaltung|Dieses zentrale Sicherheitsmodell in System Center Configuration Manager bietet hierarchieweite Sicherheit und eine Verwaltung, die Ihren administrativen und geschäftlichen Anforderungen gerecht wird.|  

> [!NOTE]  
>  Aufgrund der Designänderungen, die erstmals in System Center 2012 Configuration Manager eingeführt wurden, können Sie kein Upgrade der Configuration Manager 2007-Infrastruktur auf System Center Configuration Manager durchführen. Ein direktes Upgrade von System Center 2012 Configuration Manager auf System Center Configuration Manager wird unterstützt.  

### <a name="migration-from-configuration-manager-2012-or-another-system-center-configuration-manager-hierarchy"></a>Migration aus Configuration Manager 2012 oder einer anderen System Center Configuration Manager-Hierarchie  
 Die Prozesse für die Migration von Daten aus einer System Center 2012 Configuration Manager- oder System Center Configuration Manager-Hierarchie sind identisch. Dies beinhaltet auch das Migrieren von Daten aus mehreren Quellhierarchien zu einer einzelnen Zielhierarchie, z.B. wenn Ihr Unternehmen zusätzliche Ressourcen bereitstellt, die bereits mit Configuration Manager verwaltet werden. Außerdem können Sie Daten aus einer Testumgebung zu Ihrer Configuration Manager-Produktionsumgebung migrieren. So können Sie Ihre Investition in die Configuration Manager-Testumgebung weiter nutzen.  

## <a name="additional-topics-for-migration"></a>Zusätzliche Themen zur Migration:  

-   [Planen der Migration zu System Center Configuration Manager](../../core/migration/planning-for-migration.md)  

-   [Konfigurieren von Quellhierarchien und Quellstandorten für die Migration zu System Center Configuration Manager](../../core/migration/configuring-source-hierarchies-and-source-sites-for-migration.md)  

-   [Vorgänge der Migration zu System Center Configuration Manager](../../core/migration/operations-for-migration.md)  

-   [Sicherheit und Datenschutz für die Migration zu System Center Configuration Manager](../../core/migration/security-and-privacy-for-migration.md)  

## <a name="see-also"></a>Siehe auch  
 [Starten der Verwendung von System Center Configuration Manager](../../core/servers/deploy/start-using.md)
