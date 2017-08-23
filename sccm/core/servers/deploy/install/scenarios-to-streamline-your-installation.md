---
title: Installationsszenarios | Microsoft-Dokumentation
description: "Lernen Sie Verfahren für die Installation einer neuen Configuration Manager-Hierarchie kennen, wenn Sie ein Update oder ein Upgrade für eine Seite durchführen."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 35586a85-4af9-4c8b-925a-0e32dc8b7346
caps.latest.revision: "6"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 938b2970e4d8534fdd5f3daf0c9a5ddb1f576e60
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="scenarios-to-streamline-your-installation-of-system-center-configuration-manager"></a>Szenarien für die Optimierung Ihrer Installation von System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Mit dem Release von Updateversionen für System Center Configuration Manager (Current Branch) gibt es neue Szenarios für die Optimierung der Installation einer neuen Hierarchie mit einer Updateversion (wie Update 1610) und für ein Upgrade von Microsoft System Center 2012 Configuration Manager.

Unterstützte Szenarien:  

**Installieren einer neuen System Center Configuration Manager-Hierarchie (Current Branch)**, in der eine Updateversion ausgeführt wird.  

-   Installieren Sie nur den Standort auf oberster Ebene und unmittelbar danach ein Update, um diesen Standort mit der gewünschten Updateversion zu versehen. Anschließend können Sie zusätzliche Standorte direkt mit dieser Updateversion installieren.  
-   Bei diesem Szenario wird das Installieren zusätzlicher Standorte auf einer Baselinestufe übersprungen, die dann anschließend auf die gewünschte Updateversion aktualisiert werden müssen.  
-   Dieses Szenario überspringt die Installation von Clients mit einer Baselineversion, die dann anschließend neu installiert werden müssen, wenn Sie ein Update auf eine spätere Version durchführen.  

**Upgrade von Microsoft System Center 2012 Configuration Manager** auf eine Updateversion von System Center Configuration Manager.  

-   Führen Sie ein Upgrade für Ihren Standort der zentralen Verwaltung und alle primären Standorte auf eine Baselineversion (wie Version 1606) manuell durch, bevor Sie eine Updateversion (wie Version 1610) installieren.  
-   Führen Sie erst dann ein Upgrade für sekundäre Standorte von Microsoft System Center 2012 Configuration Manager durch, wenn Ihre primären Standorte die gewünschte Updateversion ausführen.  
-   Sie führen erst dann ein Upgrade für Clients von Microsoft System Center 2012 Configuration Manager durch, wenn Ihre primären Standorte die gewünschte Updateversion ausführen.  

## <a name="scenario-install-a-new-hierarchy-to-an-update-version"></a>Szenario: Installieren einer neuen Hierarchie mit einer Updateversion  
Installieren Sie in diesem Beispielszenario den ersten Standort einer Hierarchie mit einer Baselineversion von System Center Configuration Manager wie z.B. Version 1610. Installieren Sie dann das Update 1610, bevor Sie zusätzliche Standorte oder Clients bereitstellen.  

-   Da Sie planen, eine Updateversion (z.B. Version 1610) zu verwenden, und keine Baselineversion (z.B. Version 1606) beibehalten wollen, müssen Sie keine zusätzlichen Standorte installieren und dann upgraden. Dies gilt auch für Clients.  
-   Installieren Sie keine sekundären Standorte mit Version 1606, die Sie dann auf Version 1610 upgraden. Installieren Sie stattdessen sekundäre Standorte, wenn Ihre primären Standorte Version 1610 bereits ausführen.  

Gehen Sie wie folgt vor:  

1.  **Installieren Sie einen Standort auf oberster Ebene für Ihre neue Hierarchie** mithilfe der Baselinemedien.  

    -   Mithilfe der Baselinemedien kann nur der erste Standort einer neuen Hierarchie installiert werden.  
    -   Installieren Sie beispielsweise einen Standort auf oberster Ebene mit der Baselineversion 1606. Weitere Informationen finden Sie unter [Verwenden des Setup-Assistenten zum Installieren von Standorten](/sccm/core/servers/deploy/install/use-the-setup-wizard-to-install-sites).  

    Nach diesem Schritt wird der Standort auf oberster Ebene mit Version 1606 ausgeführt.  

2.  **Verwenden Sie Updates in der Konsole, um Ihren Standort auf oberster Ebene auf eine spätere Version zu aktualisieren.**  

    -   Vor der Installation untergeordneter Standorte oder Clients aktualisieren Sie Ihren Standort auf oberster Ebene auf die Updateversion, die Sie verwenden möchten.  
    -   Beispielsweise können Sie Ihren Standort auf oberster Ebene von Version 1606 auf Version 1610 aktualisieren. Weitere Informationen finden Sie unter [Updates für System Center Configuration Manager](../../../../core/servers/manage/updates.md).  

    Nach diesem Schritt wird der Standort auf oberster Ebene mit Version 1610 ausgeführt.  

3.  **Installieren Sie neue untergeordnete Standorte unter einem Standort der zentralen Verwaltung.**  

    -   Verwenden Sie das Installationsmedium im Ordner „CD.Latest“ auf dem Standortserver der zentralen Verwaltung, um untergeordnete primäre Standorte zu installieren. Weitere Informationen finden Sie unter [Der Ordner „CD.Latest“ für System Center Configuration Manager](../../../../core/servers/manage/the-cd.latest-folder.md).  

      Dieses Quellmedium ist erforderlich, um sicherzustellen, dass neue untergeordnete primäre Standorte der Version des Standorts der zentralen Verwaltung entsprechen.  

    Nach diesem Schritt führen Ihre neuen untergeordneten primären Standorte Version 1610 aus.  

4.  **Verwenden Sie an jedem primären Standort die Option in der Konsole, um neue sekundäre Standorte zu installieren.**  

    -   Da Sie keine sekundären Standorte installiert haben, als die primären Standorte Version 1606 aufwiesen, müssen Sie für die sekundären Standorte kein Upgrade durchführen.  
    -   Installieren Sie stattdessen neue sekundäre Standorte, die Version 1610 ausführen. Weitere Informationen finden Sie unter [Install a secondary site](/sccm/core/servers/deploy/install/use-the-setup-wizard-to-install-sites#bkmk_secondary) (Installieren eines sekundären Standorts) im Thema [Use the Setup Wizard to install sites](/sccm/core/servers/deploy/install/use-the-setup-wizard-to-install-sites) (Verwenden des Setup-Assistenten zum Installieren von Standorten).  

    Nach diesem Schritt werden neue sekundäre Standorte installiert, die Version 1610 ausführen.  

5.  **Installieren Sie neue Clients am primären Standort.**  

    -   Da Sie keine Clients installiert haben, als die primären Standorte Version 1606 aufwiesen, müssen Sie für die Clients kein Upgrade von Version 1606 auf Version 1610 durchführen.  
    -   Installieren Sie stattdessen neue Clients, die Version 1610 ausführen. Weitere Informationen finden Sie unter [Bereitstellen von Clients in System Center Configuration Manager](../../../clients/deploy/deploy-clients-to-windows-computers.md).  

    Nach diesem Schritt werden neue Clients installiert, die Version 1610 ausführen.  

## <a name="scenario-upgrade-system-center-2012-configuration-manager-to-an-update-version-of-system-center-configuration-manager-current-branch"></a>Szenario: Upgraden von System Center 2012 Configuration Manager auf eine Updateversion von System Center Configuration Manager (Current Branch)  
Führen Sie in diesem Beispielszenario für Ihre Microsoft System Center 2012 Configuration Manager-Infrastruktur ein Upgrade auf eine Updateversion von System Center Configuration Manager durch, z.B. Version 1610.  

-   Der Standort der zentralen Verwaltung und alle primären Standorte müssen auf die Baselineversion 1606 upgegradet werden, bevor Sie das Update für Version 1610 installieren.  
-   Für sekundäre Standorte und Clients erfolgt kein Upgrade auf bzw. keine Installation von Version 1606. Stattdessen werden sie direkt von Microsoft System Center 2012 Configuration Manager auf System Center Configuration Manager Version 1610 aktualisiert.  

Gehen Sie wie folgt vor:  

1.  **Upgraden Sie den Microsoft System Center 2012 Configuration Manager-Standort der obersten Ebene** auf eine Baselineversion (Current Branch), indem Sie Quellmedien für System Center Configuration Manager (wie Version 1606) verwenden. Weitere Informationen finden Sie unter [Upgrade auf System Center Configuration Manager](../../../../core/servers/deploy/install/upgrade-to-configuration-manager.md).  

    -   Wie bei herkömmlichen Upgradeszenarien aktualisieren Sie stets zuerst den Standort auf oberster Ebene einer Hierarchie und anschließend untergeordnete Standorte.  

    Nach diesem Schritt wird der Standort auf oberster Ebene mit Version 1606 ausgeführt.  

2.  **Upgraden Sie jeden untergeordneten primären Standort in Ihrer Hierarchie** ebenfalls auf diese Baselineversion.  

    -   Wenn Sie ein Upgrade von Microsoft System Center 2012 Configuration Manager durchführen, müssen Sie für jeden primären Standort manuell ein Upgrade auf eine Baselineversion von Current Branch durchführen.  
    -   Zu diesem Zeitpunkt upgraden Sie keine sekundären Standorte.  

    Nach diesem Schritt wird an jedem primären Standort Version 1606 ausgeführt.  

3.  **Legen Sie Wartungsfenster für untergeordnete primäre Standorte fest.** Nach dem Upgrade aller primären Standorte auf die Baselineversion planen Sie die Konfiguration von Wartungsfenstern, um zu steuern, wann für diese Standorte Infrastruktur-Updates installiert werden sollen. Weitere Informationen finden Sie unter [Verwenden von Wartungsfenstern in System Center Configuration Manager](../../../../core/clients/manage/collections/use-maintenance-windows.md).  (Wartungsfenster werden in Version 1606 als *Servicezeitfenster* bezeichnet.)  

    -   Ein untergeordneter primärer Standort installiert automatisch dieselben Updates, die Sie an einem Standort der zentralen Verwaltung installieren.  
    -   An sekundären Standorten werden neue Versionen nicht automatisch installiert. Sie müssen diese manuell aus der Konsole upgraden.  

  Wenn Sie nach diesem Schritt Updates am Standort der zentralen Verwaltung installieren, installieren untergeordnete primäre Standorte dieses Update, sobald ihr Wartungsfenster es zulässt.  

4.  **Installieren Sie die Updateversion am Standort auf oberster Ebene.** Dadurch wird der Standort auf oberster Ebene aktualisiert. Nachdem die Updateversion am Standort der zentralen Verwaltung installiert wurde, wird an allen untergeordneten primären Standorten das Update automatisch installiert, es sei denn die Installation wird durch ein Wartungsfenster verhindert.  

    -   Beispielsweise können Sie Ihren Standort auf oberster Ebene von Version 1606 auf Version 1610 aktualisieren. Weitere Informationen finden Sie unter [Updates für System Center Configuration Manager](../../../../core/servers/manage/updates.md).  

    Nach diesem Schritt wird an Ihrem Standort der zentralen Verwaltung und allen primären Standorten Version 1610 ausgeführt.  

5.  **Führen Sie ein Upgrade sekundärer Standorten durch.** Sobald an einem primären Standort das Update installiert wurde und Version 1610 ausgeführt wird, können Sie mithilfe der Option in der Konsole sekundäre Standorte upgraden.  

    -   Dabei werden sekundäre Standorte direkt von Microsoft System Center 2012 Configuration Manager auf die Updateversion upgegradet, die Sie am primären Standort installiert haben.  
    -   Weitere Informationen zum Upgraden eines sekundären Standorts finden Sie unter [Upgraden von Standorten](../../../../core/servers/deploy/install/upgrade-to-configuration-manager.md#bkmk_upgrade) im Thema [Upgrade auf System Center Configuration Manager](../../../../core/servers/deploy/install/upgrade-to-configuration-manager.md).  

6.  **Aktualisieren von Clients** Verwenden Sie zum Upgraden von Clients die Informationen unter [Upgraden von Clients für Windows-Computer in System Center Configuration Manager](../../../../core/clients/manage/upgrade/upgrade-clients-for-windows-computers.md).  

    -   Dabei werden Clients direkt von Microsoft System Center 2012 Configuration Manager auf die Updateversion upgegradet, die Sie am primären Standort installiert haben.  

    Nach diesem Schritt werden die Clients auf Version 1610 upgegradet, ohne dass zuvor ein Upgrade auf Version 1606 erfolgt.
