---
title: Konfigurieren von Wake-on-LAN | Microsoft-Dokumentation
description: "Wählen Sie Wake-On-LAN-Einstellungen in System Center Configuration Manager aus."
ms.custom: na
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b475a0c8-85d6-4cc4-b11f-32c0cc98239e
caps.latest.revision: "7"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 9c920651ba1dc6e0a28df458d28956126ddbaff0
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="how-to-configure-wake-on-lan-in-system-center-configuration-manager"></a>Konfigurieren von Wake-On-LAN in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Geben Sie Einstellungen für Wake-On-LAN für System Center Configuration Manager an, wenn Sie Computer aus dem Standbymodus reaktivieren möchten, um die erforderliche Software (Softwareupdates, Anwendungen, Tasksequenzen, Programme usw.) zu installieren.

Sie können Wake-On-LAN erweitern, indem Sie die Clienteinstellungen für den Aktivierungsproxy nutzen. Zum Nutzen des Aktivierungsproxys müssen Sie jedoch zuerst Wake-On-LAN für den Standort aktivieren und **Nur Aktivierungspakete verwenden** sowie die Option **Unicast** für die Wake-On-LAN-Übertragungsmethode angeben. Bei dieser Aktivierungslösung werden auch Ad-hoc-Verbindungen unterstützt, z. B. eine Remotedesktopverbindung.

Verwenden Sie das erste Verfahren, um einen primären Standort für Wake-On-LAN zu konfigurieren. Verwenden Sie das zweite Verfahren, um die Clienteinstellungen für den Aktivierungsproxy zu konfigurieren. Mithilfe des zweiten Verfahrens werden die Clientstandardeinstellungen für die Aktivierungsproxy-Einstellungen konfiguriert, die für alle Computer der Hierarchie gelten. Wenn diese Einstellungen nur auf ausgewählte Computer angewendet werden sollen, erstellen Sie eine benutzerdefinierte Geräteeinstellung und weisen diese einer Sammlung mit den Computern zu, die Sie für den Aktivierungsproxy konfigurieren möchten. Weitere Informationen zum Erstellen benutzerdefinierter Clienteinstellungen finden Sie unter [Konfigurieren von Geräteclienteinstellungen in System Center Configuration Manager](../../../core/clients/deploy/configure-client-settings.md).

Ein Computer, der die Clienteinstellungen des Aktivierungsproxys erhält, wird seine Netzwerkverbindung wahrscheinlich für 1-3 Sekunden unterbrechen. Der Grund hierfür ist, dass der Client die Netzwerkschnittstellenkarte zurücksetzen muss, um den Treiber des Aktivierungsproxys zuzulassen.

> [!WARNING]
> Werten Sie den Aktivierungsproxy zur Vermeidung unerwarteter Störungen der Netzwerkdienste zuerst in einer isolierten und repräsentativen Netzwerkinfrastruktur aus. Verwenden Sie anschließend die benutzerdefinierten Clienteinstellungen, um den Test auf eine ausgewählte Gruppe von Computern in mehreren Subnetzen auszudehnen. Weitere Informationen zur Funktionsweise des Aktivierungsproxys finden Sie unter [Plan how to wake up clients in System Center Configuration Manager (Planen der Aktivierung von Clients in System Center Configuration Manager)](../../../core/clients/deploy/plan/plan-wake-up-clients.md).

## <a name="to-configure-wake-on-lan-for-a-site"></a>So konfigurieren Sie Wake-on-LAN für einen Standort

1. Wechseln Sie in der Configuration Manager-Konsole zu **Verwaltung > Standortkonfiguration > Standorte**.
2. Klicken Sie zum Konfigurieren auf den primären Standort, und klicken Sie dann auf **Eigenschaften**.
3. Klicken Sie auf die Registerkarte **Wake-On-LAN**, und konfigurieren Sie die Optionen für diesen Standort. Stellen Sie zum Unterstützen des Aktivierungsproxys sicher, dass Sie die Optionen **Nur Aktivierungspakete verwenden** und **Unicast** aktivieren. Weitere Informationen finden Sie unter [Plan how to wake up clients in System Center Configuration Manager (Planen der Aktivierung von Clients in System Center Configuration Manager)](../../../core/clients/deploy/plan/plan-wake-up-clients.md).
4. Klicken Sie auf **OK**, und wiederholen Sie diesen Vorgang für alle primären Standorte in der Hierarchie.

## <a name="to-configure-wake-up-proxy-client-settings"></a>So konfigurieren Sie die Clienteinstellungen für den Aktivierungsproxy

1. Navigieren Sie in der Configuration Manager-Konsole zu **Verwaltung > Clienteinstellungen**.
2. Klicken Sie auf **Clientstandardeinstellungen**, und klicken Sie auf **Eigenschaften**.
3. Wählen Sie **Energieverwaltung** aus, und wählen Sie dann für **Aktivierungsproxy zulassen**, **Ja** aus.
4. Überprüfen und konfigurieren Sie ggf. weitere Einstellungen für den Aktivierungsproxy. Weitere Informationen zu diesen Einstellungen finden Sie unter [Power management settings (Konfigurieren der Energieverwaltungseinstellungen)](../../../core/clients/deploy/about-client-settings.md#power-management).
5. Klicken Sie auf **OK**, um das Dialogfeld zu schließen, und klicken Sie dann erneut auf **OK**, um das Dialogfeld Clientstandardeinstellungen zu schließen.

Sie können die folgenden Wake-On-LAN-Berichte zum Überwachen der Installation und Konfiguration des Aktivierungsproxys verwenden:

- Zusammenfassung des Aktivierungsproxy-Bereitstellungszustands
- Details zum Aktivierungsproxy-Bereitstellungszustand

> [!TIP]
> Mit einer Verbindung zu einem Computer im Standbymodus können Sie testen, ob der Aktivierungsproxy funktioniert. Stellen Sie beispielsweise eine Verbindung mit einem freigegebenen Ordner auf diesem Computer her, oder versuchen Sie, per Remotedesktop eine Verbindung zu dem Computer herzustellen. Stellen Sie bei Verwendung von DirectAccess sicher, dass die IPv6-Präfixe funktionieren, indem Sie die gleichen Tests für einen Computer im Standbymodus durchführen, der sich momentan im Internet befindet.
