---
title: Auswahl von zu Migrierenden Daten | Microsoft-Dokumentation
description: "Erfahren Sie, welche Daten migriert werden können und welche Daten Sie nicht zu System Center Configuration Manager migrieren können."
ms.custom: na
ms.date: 12/29/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 99222dc8-0e1e-4513-8302-7a1acf671e9b
caps.latest.revision: "6"
caps.handback.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 9dc5f6c9f58e1fc33b2dc9dd76737ae23af81993
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="determine-whether-to-migrate-data-to-system-center-configuration-manager"></a>Bestimmen, ob Daten zu System Center Configuration Manager migriert werden sollen

*Gilt für: System Center Configuration Manager (Current Branch)*

In System Center Configuration Manager bezeichnet „Migration“ einen Prozess zum Übertragen vorhandener Daten und Konfigurationen, die Sie erstellt haben, aus unterstützten Versionen von Configuration Manager in Ihre neue Hierarchie.  Damit können die folgenden Zwecke erfüllt werden:  

-   Kombinieren mehrerer Hierarchien zu einer.  

-   Verschieben von Daten und Konfigurationen aus einer Testbereitstellung in Ihre Produktionsbereitstellung.

-   Verschieben von Daten und Konfigurationen aus einer früheren Configuration Manager-Version, z.B. Configuration Manager 2007, die über keinen Upgradepfad zu System Center Configuration Manager verfügt, oder aus System Center 2012 Configuration Manager (unterstützt keinen Upgradepfad zu System Center Configuration Manager).  

Mit Ausnahme der Standortsystemrolle Verteilungspunkt und der Computer, auf denen Verteilungspunkte gehostet werden, kann keine Infrastruktur (z. B. Standorte, Standortsystemrollen oder Computer, auf denen eine Standortsystemrolle gehostet wird) migriert, übertragen oder zwischen Hierarchien freigegeben werden.  

 Obwohl Sie keine Serverinfrastrukturen migrieren können, können Sie Configuration Manager-Clients zwischen Hierarchien migrieren. Die Clientmigration umfasst das Migrieren der von Clients verwendeten Daten aus der Quell- in die Zielhierarchie und die anschließende Installation oder Neuzuweisung der Clientsoftware, wobei der Client der neuen Hierarchie unterstellt wird.

Sobald ein Client nach seiner Installation in der neuen Hierarchie seine Daten übermittelt, kann Configuration Manager mithilfe dessen eindeutiger Configuration Manager-ID den Bezug zwischen den Daten, die Sie zuvor migriert haben, und den einzelnen Clients herstellen.  

 Mithilfe dieser Migrationsfunktionalität können Sie nicht nur weiterhin von Investitionen profitieren, die bereits in Konfigurationen und Bereitstellungen erfolgt sind, sondern auch von allen wesentlichen Produktänderungen (die zuerst in System Center 2012 Configuration Manager und dann in System Center Configuration Manager eingeführt wurden). Zu den Änderungen gehören eine vereinfachte Configuration Manager-Hierarchie, die weniger Standorte und Ressourcen benötigt, und eine verbesserte Verarbeitung durch Verwenden von nativem 64-Bit-Code, der auf 64-Bit-Hardware läuft.  

 Informationen zu den Versionen von Configuration Manager, in denen die Migration unterstützt wird, finden Sie unter [Prerequisites for migration in System Center Configuration Manager (Voraussetzungen für die Migration in System Center Configuration Manager)](../../core/migration/prerequisites-for-migration.md).  

 Die folgenden Abschnitte helfen Ihnen bei der Planung für Daten, die migriert bzw. nicht migriert werden können:  

-   [Daten, die zu System Center Configuration Manager migriert werden können](#Can_Migrate)  

-   [Daten, die nicht zu System Center Configuration Manager migriert werden können](#Cannot_migrate)  

##  <a name="Can_Migrate"></a> Daten, die zu System Center Configuration Manager migriert werden können  
 Die meisten Objekte können zwischen unterstützten Configuration Manager-Hierarchien migriert werden. Die migrierten Instanzen einiger Objekte einer unterstützten Version von Configuration Manager2007 müssen geändert werden, um dem Schema- und Objektformat von System Center 2012 Configuration Manager zu entsprechen.

Diese Änderungen haben keine Auswirkungen auf die Daten in der Datenbank des Quellstandorts. Objekte, die aus einer unterstützten Version von System Center 2012 Configuration Manager oder System Center Configuration Manager migriert wurden, erfordern keine Änderungen.  

 Die folgenden Objekte auf Grundlage der Configuration Manager-Version in der Quellhierarchie migriert werden können. Einige Objekte, wie z. B. Abfragen, werden nicht migriert. Wenn Sie diese Objekte, die nicht migriert werden, weiterhin verwenden möchten, müssen Sie sie in der neuen Hierarchie neu erstellen. Andere Objekte, z.B. einige Clientdaten, werden in der neuen Hierarchie automatisch neu erstellt, wenn Sie Clients in der Hierarchie verwalten.  

### <a name="objects-that-you-can-migrate-from-system-center-2012-configuration-manager-or-system-center-configuration-manager-current-branch"></a>Folgende Objekte können Sie von System Center 2012 Configuration Manager oder Current Branch von System Center Configuration Manager migrieren:

-   Ankündigungen  

-   Anwendungen für System Center 2012 Configuration Manager und höhere Versionen  

-   Virtuelle App-V-Umgebung für System Center 2012 Configuration Manager und höhere Versionen  

-   Asset Intelligence-Anpassungen  

-   Standortgrenzen  

-   Sammlungen: Verwenden Sie einen Objektmigrationsauftrag, um Sammlungen von einer unterstützten Version von System Center 2012 Configuration Manager oder System Center Configuration Manager zu migrieren.  

-   Kompatibilitätseinstellungen:  

    -   Konfigurationsbasislinien  

    -   Konfigurationselemente  

-   Betriebssystembereitstellung:  

    -   Startabbilder  

    -   Treiberpakete  

    -   Treiber  

    -   Abbilder  

    -   Pakete  

    -   Tasksequenzen  

-   Suchergebnisse: Gespeicherte Suchkriterien  

-   Softwareupdates:  

    -   Bereitstellungen  

    -   Bereitstellungspakete  

    -   Vorlagen  

    -   Softwareupdatelisten  

-   Softwareverteilungspakete  

-   Softwaremessungsregeln  

-   Virtuelle Anwendungspakete  

### <a name="objects-that-you-can-migrate-from-configuration-manager-2007-sp2"></a>Folgende Objekte können von Configuration Manager 2007 SP2 migriert werden:

-   Ankündigungen  

-   Anwendungen für System Center 2012 Configuration Manager und höhere Versionen  

-   Virtuelle App-V-Umgebung für System Center 2012 Configuration Manager und höhere Versionen  

-   Asset Intelligence-Anpassungen  

-   Standortgrenzen  

-   Sammlungen: Sie migrieren Sammlungen von einer unterstützten Version von Configuration Manager 2007 mithilfe eines Sammlungsmigrationsauftrags.  

-   Kompatibilitätseinstellungen (in Configuration Manager 2007 als Verwaltung gewünschter Konfigurationen bezeichnet)  

    -   Konfigurationsbasislinien  

    -   Konfigurationselemente  

-   Betriebssystembereitstellung:  

    -   Startabbilder  

    -   Treiberpakete  

    -   Treiber  

    -   Abbilder  

    -   Pakete  

    -   Tasksequenzen  

-   Suchergebnisse: Suchordner  

-   Softwareupdates:  

    -   Bereitstellungen  

    -   Bereitstellungspakete  

    -   Vorlagen  

    -   Softwareupdatelisten  

-   Softwareverteilungspakete  

-   Softwaremessungsregeln  

-   Virtuelle Anwendungspakete  

##  <a name="Cannot_migrate"></a> Daten, die nicht zu System Center Configuration Manager migriert werden können  
 Folgende Objekttypen können nicht migriert werden:  

-   AMT-Client-Bereitstellungsinformationen  

-   Dateien auf Clients, einschließlich:  

    -   Clientinventur- und -verlaufsdaten  

    -   Dateien im Clientcache  

-   Abfragen  

-   Configuration Manager 2007-Sicherheitsrechte und -Instanzen für den Standort und Objekte  

-   Configuration Manager 2007-Berichte von SQL Server Reporting Services  

-   Configuration Manager 2007-Webberichte  

-   System Center 2012 Configuration Manager und System Center Configuration Manager-Berichte  

-   System Center 2012 Configuration Manager und die rollenbasierte System Center Configuration Manager-Verwaltung:  

    -   Sicherheitsrollen  

    -   Sicherheitsbereiche  
