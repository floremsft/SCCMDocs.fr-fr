---
title: "Überwachen des Cloudverwaltungsgateways – Configuration Manager | Microsoft-Dokumentation"
description: 
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: 15f72f80-9850-40ce-9c3a-443ba04b6a03
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: daa0790995dc13ec2c78ae2d98a9eb38c0bcf8ae
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="monitor-cloud-management-gateway-in-configuration-manager"></a>Überwachen des Cloudverwaltungsgateways in Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Ab Version 1610 können Sie, wenn der Cloudverwaltungsgateway-Dienst ausgeführt wird und Clients über diesen eine Verbindung herstellen, Clients und Netzwerkdatenverkehr überwachen, um sicherzustellen, dass Sie wissen, wie der Dienst arbeitet.

## <a name="monitor-clients"></a>Überwachen von Clients

Clients, die über den Cloudverwaltungsgateway-Dienst verbunden sind, erscheinen genauso wie lokale Clients in der Configuration Manager-Konsole. Weitere Informationen finden Sie unter [Überwachen von Clients in System Center Configuration Manager](monitor-clients.md).

## <a name="monitor-traffic-in-the-console"></a>Überwachen von Datenverkehr in der Konsole

Sie können Datenverkehr über das Cloudverwaltungsgateway mithilfe der Configuration Manager-Konsole überwachen:

1. Gehen Sie zu **Verwaltung > Clouddienste > Cloud Management Gateway** (Cloudverwaltungsgateway).

2. Wählen Sie im Listenbereich den Cloudverwaltungsgateway-Dienst aus.

3. Sehen Sie sich die Informationen über den Datenverkehr im Detailbereich für die Cloudverwaltungsgateway-Verbindungsrolle und die Standortsystemrollen an, mit denen eine Verbindung hergestellt wird.

## <a name="set-up-outbound-traffic-alerts"></a>Einrichten von Warnungen für ausgehenden Datenverkehr

Warnungen für ausgehenden Datenverkehr helfen Ihnen beim Verständnis, wann der Datenverkehr an einen Schwellenwert von 14 Tagen (2 Wochen) gelangt. Sie erhalten die Möglichkeit, Warnungen für den Datenverkehr einzurichten, wenn Sie den Cloudverwaltungsgateway-Dienst erstellen. Wenn Sie diesen Teil übersprungen haben, können Sie noch immer die Warnungen einrichten, wenn der Dienst ausgeführt wird. Sie können ebenso die Warnungseinstellungen jederzeit anpassen.

1. Gehen Sie zu **Verwaltung > Clouddienste > Cloud Management Gateway** (Cloudverwaltungsgateway).

2. Klicken Sie mit der rechten Maustaste im Listenbereich den Cloudverwaltungsgateway-Dienst, und wählen Sie **Eigenschaften** aus.

3. Klicken Sie auf die Registerkarte „Warnungen“, und wählen Sie zum Aktivieren (oder Deaktivieren) den Schwellenwert und Warnungen aus. Geben Sie anschließend den 14-tägigen Schwellenwert (in GB) und Prozentsätze des Schwellenwerts für die Auslösung der verschiedenen Warnstufen an.

4. Klicken Sie auf **OK**, wenn Sie fertig sind.

## <a name="monitor-logs"></a>Überwachungsprotokolle

Der Cloudverwaltungsgateway-Dienst generiert Einträge in einigen Protokolldateien. Weitere Informationen finden Sie unter [Protokolldateien in System Center Configuration Manager](/sccm/core/plan-design/hierarchy/log-files).
