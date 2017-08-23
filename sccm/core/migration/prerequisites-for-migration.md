---
title: "Voraussetzungen für die Migration | Microsoft-Dokumentation"
description: "Hier erhalten Sie Informationen zu den unterstützten Versionen von Configuration Manager, zu den unterstützten Quellstandortsprachen sowie zu den erforderlichen Konfigurationen für die Migration."
ms.custom: na
ms.date: 3/7/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ec976930-7467-4d3c-b33c-991bf408a74a
caps.latest.revision: "10"
caps.handback.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: cd90f5462ac4bb4c0a2021e6d5dde65161b9c5f6
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="prerequisites-for-migration-in-system-center-configuration-manager"></a>Voraussetzungen für die Migration in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Zur Durchführung einer Migration aus einer unterstützten Quellhierarchie müssen Sie Zugriff auf alle relevanten Configuration Manager-Quellstandorte haben und am System Center Configuration Manager-Zielstandort über die Berechtigungen für Konfigurations- und Migrationsvorgänge verfügen.  

 Verwenden Sie die Informationen in den folgenden Abschnitten für die zur Migration unterstützen Configuration Manager-Versionen und die erforderlichen Konfigurationen.  

-   [Versionen von Configuration Manager, die für die Migration unterstützt werden](#BKMK_SupportedMigrationVersions)  

-   [Quellstandortsprachen, die für die Migration unterstützt werden](#BKMK_SorceSiteLanguage)  

-   [Erforderliche Konfigurationen für die Migration](#BKMK_Required_Configurations)  

##  <a name="BKMK_SupportedMigrationVersions"></a> Versionen von Configuration Manager, die für die Migration unterstützt werden  
 Sie können Daten aus einer Quellhierarchie migrieren, in der eine der folgenden Versionen von Configuration Manager ausgeführt wird:  

-   Configuration Manager 2007 SP2 (Im Rahmen der Migration werden Configuration Manager 2007 R2 oder R3 am Quellstandort nicht berücksichtigt. Solange am Quellstandort SP2 ausgeführt wird, werden Standorte mit installiertem R2- oder R3-Add-On für die Migration zu System Center Configuration Manager unterstützt).  

-   System Center 2012 Configuration Manager SP2 oder System Center 2012 R2 Configuration Manager SP1.  

    > [!TIP]  
    >  Zusätzlich zur Migration können Sie bei Standorten, an denen System Center 2012 Configuration Manager ausgeführt wird, ein direktes Upgrade auf System Center Configuration Manager verwenden.  

-   Eine System Center Configuration Manager-Hierarchie mit derselben oder einer niedrigeren Version von System Center Configuration Manager.  

  Wenn Sie z.B. über eine Zielhierarchie verfügen, die System Center Configuration Manager 1606 ausführt, können Sie Migration verwenden, um Daten aus einer Quellhierarchie zu kopieren, die die Version 1606 oder 1602 ausführt. Sie können jedoch keine Daten aus einer Quellhierarchie migrieren, die 1610 ausführt.  


##  <a name="BKMK_SorceSiteLanguage"></a> Quellstandortsprachen, die für die Migration unterstützt werden  
 Wenn Sie Daten zwischen Configuration Manager-Hierarchien migrieren, werden die Daten in der Zielhierarchie in einem sprachunabhängigen Format für System Center Configuration Manager gespeichert. Da in Configuration Manager 2007 Daten nicht in einem sprachunabhängigen Format gespeichert werden, müssen Objekte während der Migration von Configuration Manager 2007 vom Migrationsprozess in dieses Format umgewandelt werden. Daher werden nur Configuration Manager 2007-Quellstandorte für die Migration unterstützt, die mit folgenden Sprachen installiert sind:  

-   Englisch  

-   Französisch  

-   Deutsch  

-   Japanisch  

-   Koreanisch  

-   Russisch  

-   Chinesisch (vereinfacht)  

-   Chinesisch (traditionell)  

Wenn Sie Daten aus einer System Center 2012 Configuration Manager- oder System Center Configuration Manager-Hierarchie migrieren, gibt es keine Einschränkungen hinsichtlich der Quellstandortsprache. Objekte in der Datenbank des Quellstandorts befinden sich bereits in einem sprachunabhängigen Format.  

##  <a name="BKMK_Required_Configurations"></a> Erforderliche Konfigurationen für die Migration  
Folgende Konfigurationen sind für Migration und Migrationsvorgänge erforderlich:  

-   **So konfigurieren, starten und überwachen Sie die Migration in der Configuration Manager-Konsole:**  

     Am Zielstandort muss Ihrem Konto die rollenbasierte Verwaltungssicherheitsrolle **Infrastrukturadministrator**zugewiesen sein. Mit dieser Sicherheitsrolle verfügen Sie über die Berechtigungen, sämtliche Migrationsvorgänge zu verwalten. Dazu gehören die Erstellung von Migrationsaufträgen, Bereinigung, Überwachung sowie das Freigeben und Aktualisieren von Verteilungspunkten.  

-   **Datensammlung:**  

     Für das Sammeln von Daten durch den Zielstandort müssen Sie die folgenden zwei Zugriffskonten des Zielstandorts zur Verwendung mit beiden Quellstandorten konfigurieren:  

    -   **Konto des Quellstandorts:** Dieses Konto wird für den Zugriff auf den SMS-Anbieter des Quellstandorts verwendet.  

        -   Für einen Configuration Manager 2007 SP2-Quellstandort benötigt dieses Konto die Berechtigung **Lesen** für alle Quellstandortsobjekte.  

        -   Für einen System Center 2012 Configuration Manager- oder System Center Configuration Manager-Quellstandort muss dieses Konto über die Berechtigung **Lesen** für alle Quellstandortobjekte verfügen. Sie weisen dem Konto diese Berechtigung über die rollenbasierte Verwaltung zu. Informationen zur Verwendung der rollenbasierten Verwaltung finden Sie unter [Fundamentals of role-based administration for System Center Configuration Manager](../../core/understand/fundamentals-of-role-based-administration.md).  

    -   **Konto der Datenbank des Quellstandorts:** Dieses Konto wird für den Zugriff auf die SQL Server-Datenbank des Quellstandorts verwendet und muss über die Berechtigungen **Connect**, **Execute**und **Select** für die Datenbank des Quellstandorts verfügen.  

    Sie können diese Konten dann konfigurieren, wenn Sie eine neue Quellhierarchie oder eine Datensammlung für einen zusätzlichen Quellstandort konfigurieren oder wenn Sie die Anmeldeinformationen für einen Quellstandort erneut konfigurieren. Für diese Konten kann ein Domänenbenutzerkonto verwendet werden, oder Sie können das Computerkonto des Standorts auf der obersten Ebene der Zielhierarchie angeben.  

    > [!IMPORTANT]  
    >  Wenn Sie das Configuration Manager-Computerkonto verwenden, vergewissern Sie sich, dass dieses Konto Mitglied der Sicherheitsgruppe **Distributed COM-Benutzer** in der Domäne mit dem Quellstandort ist.  

    Bei der Datensammlung werden folgende Netzwerkprotokolle und Ports verwendet:  

    -   NetBIOS/SMB – 445 (TCP)  

    -   RPC (WMI) – 135 (TCP)  

    -   SQL Server – Die sowohl von Quell- als auch von Zielstandortdatenbank verwendeten TCP-Ports.  

-   **Migrieren von Softwareupdates:**  

     Bevor Sie Softwareupdates migrieren, müssen Sie die Zielhierarchie mit einem Softwareupdatepunkt konfigurieren. Weitere Informationen finden Sie unter [Planen der Migration von Softwareupdates](../../core/migration/planning-for-the-migration-of-objects.md#Plan_migrate_Software_updates).  

-   **Freigeben von Verteilungspunkten:**  

     Damit Verteilungspunkte von einem Quellstandort erfolgreich freigegeben werden können, müssen von mindestens einem primären Standort oder dem Standort der zentralen Verwaltung dieselben Portnummern für Clientanforderungen wie beim Quellstandort verwendet werden. Weitere Informationen zu Clientanforderungsports finden Sie unter [Konfigurieren von Clientkommunikationsports in System Center Configuration Manager](../../core/clients/deploy/configure-client-communication-ports.md).  

     Für jeden Quellstandort werden nur Verteilungspunkte freigegeben, die auf den mit einem FQDN konfigurierten Servern des Standortsystems installiert sind.  

     Außerdem muss das **Konto des Quellstandorts** (über das auf den SMS-Anbieter für den Quellstandortserver zugegriffen wird) über die Berechtigung **Ändern** für das Objekt **Standort** am Quellstandort verfügen, um einen Verteilungspunkt von einem System Center 2012 Configuration Manager- oder System Center Configuration Manager-Quellstandort freizugeben. Sie erteilen dem Konto diese Berechtigung mithilfe der rollenbasierten Verwaltung. Informationen zur Verwendung der rollenbasierten Verwaltung finden Sie unter [Fundamentals of role-based administration for System Center Configuration Manager](../../core/understand/fundamentals-of-role-based-administration.md).  


-   **Aktualisieren oder erneutes Zuweisen von Verteilungspunkten:**  

     Das für das Sammeln von Daten beim SMS-Anbieter des Quellstandorts konfigurierte **Zugriffskonto des Quellstandorts** muss über folgende Berechtigungen verfügen:  

    -   Für das Aktualisieren eines Verteilungspunkts von Configuration Manager 2007 müssen für das Konto die Berechtigungen **Lesen**, **Ausführen** und **Löschen** der **Standort**-Klasse auf dem Standortserver von Configuration Manager 2007 vorliegen, um den Verteilungspunkt erfolgreich vom Configuration Manager 2007-Quellstandort entfernen zu können.  

    -   Damit ein System Center 2012 Configuration Manager- oder System Center Configuration Manager-Verteilungspunkt neu zugewiesen werden kann, muss das Konto über die Berechtigung **Ändern** für das **Website**-Objekt am Quellstandort verfügen. Sie erteilen dem Konto diese Berechtigung mithilfe der rollenbasierten Verwaltung. Informationen zur Verwendung der rollenbasierten Verwaltung finden Sie unter [Fundamentals of role-based administration for System Center Configuration Manager](../../core/understand/fundamentals-of-role-based-administration.md).  

     Soll ein Verteilungspunkt erfolgreich aktualisiert oder einer neuen Hierarchie zugewiesen werden, müssen die für Clientanforderungen konfigurierten Ports am Standort, an dem der Verteilungspunkt in der Quellhierarchie verwaltet wird, den für Clientanforderungen konfigurierten Ports am Zielstandort entsprechen, an dem der Verteilungspunkt verwaltet wird. Weitere Informationen zu Clientanforderungsports finden Sie unter [Konfigurieren von Clientkommunikationsports in System Center Configuration Manager](../../core/clients/deploy/configure-client-communication-ports.md).  
