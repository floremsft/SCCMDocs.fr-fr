---
title: Verwalten der iOS-Aktivierungssperre | Microsoft-Dokumentation
description: Die iOS-Aktivierungssperre kann mit System Center Configuration Manager verwaltet werden.
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e2745bac-e1b4-4dac-8ac7-32f1c820bc9c
caps.latest.revision: "9"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 88bef04a52f716ae13afc21c25d33dea06a3fc9c
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="manage-ios-activation-lock-with-system-center-configuration-manager"></a>Verwalten der iOS-Aktivierungssperre mit System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*


System Center Configuration Manager kann Sie beim Verwalten der iOS-Aktivierungssperre unterstützen, einem Feature der App „Mein iPhone suchen“ für iOS 7.1 und höher. Wenn die Aktivierungssperre aktiviert ist, müssen die Apple-ID und das Kennwort des Benutzers eingegeben werden, bevor folgende Vorgänge möglich sind:

- Deaktivieren von „Mein iPhone suchen“
- Löschen des Geräts
- Reaktivieren des Geräts

Auf **nicht überwachten** Geräten wird die Aktivierungssperre automatisch aktiviert, wenn die App „Mein iPhone suchen“ verwendet wird.

Auf **überwachten** Geräten müssen Sie die Aktivierungssperre aktivieren, indem Sie die Kompatibilitätseinstellungen von Configuration Manager verwenden.

> [!TIP]
> Im überwachten Modus für iOS-Geräte können Sie mit dem Apple Configurator Tool ein Gerät sperren, um die Funktionen auf bestimmte geschäftliche Zwecke einzuschränken. Der überwachte Modus ist in der Regel nur für firmeneigene Geräte vorgesehen.

Obwohl die Aktivierungssperre zum Schutz von iOS-Geräten beiträgt und die Chancen einer Wiederherstellung bei Verlust oder Diebstahl erhöht, kann diese Funktion Sie als IT-Administrator vor eine Reihe von Herausforderungen stellen. Beispiel:

- Einer Ihrer Benutzer richtet die Aktivierungssperre auf einem Gerät ein. Anschließend verlässt der Benutzer das Unternehmen und gibt das Gerät zurück. Ohne die Apple-ID und das Kennwort des Benutzers gibt es keine Möglichkeit, das Gerät zu reaktivieren, auch wenn Sie es zurücksetzen.
- Sie benötigen einen Bericht über alle Geräte, bei denen die Aktivierungssperre aktiviert ist.
- Während einer Geräteaktualisierung in Ihrem Unternehmen möchten Sie einige Geräte einer anderen Abteilung zuweisen. Es können nur Geräte neu zugewiesen werden, bei denen die Aktivierungssperre nicht aktiviert ist.


Apple hat zur Behebung dieser Probleme eine Umgehung der Aktivierungssperre in iOS 7.1 eingeführt. Auf diese Weise können Sie die Aktivierungssperre von überwachten Geräten ohne Apple-ID und Kennwort des Benutzers entfernen. Überwachte Geräte können einen gerätespezifischen Umgehungscode für die Aktivierungssperre generieren, der auf dem Aktivierungsserver von Apple gespeichert wird.

Sie können [hier](https://support.apple.com/HT201365)mehr zur Aktivierungssperre erfahren.

## <a name="how-configuration-manager-helps-you-manage-activation-lock"></a>Hilfe von Configuration Manager zur Verwaltung der Aktivierungssperre

Configuration Manager hilft Ihnen dabei, die Aktivierungssperre zu verwalten. Dazu gibt es zwei Möglichkeiten:

1. Aktivieren der Aktivierungssperre auf überwachten Geräten.
2. Umgehen der Aktivierungssperre auf überwachten Geräten.

> [!IMPORTANT]
> Sie können die Aktivierungssperre auf nicht überwachten Geräten nicht umgehen.

Die Geschäftsvorteile für firmeneigene Geräte sind:



- Der Benutzer erhält die Sicherheitsvorteile der App „Mein iPhone suchen“.
- Sie können es dem Benutzer ermöglichen, seine Arbeit zu erledigen, in dem Wissen, dass Sie das Gerät außer Kraft setzen oder entsperren können, wenn es einem neuen Zweck zugewiesen werden soll.


## <a name="enable-activation-lock-on-supervised-devices"></a>Aktivieren der Aktivierungssperre auf überwachten Geräten

Sie verwenden die Kompatibilitätseinstellungen von Configuration Manager, um ein Konfigurationselement des Typs **iOS und Mac OS X** zu erstellen und bereitzustellen, um die Aktivierungssperre auf überwachten Geräten zu aktivieren:

1. Verwenden Sie die Informationen im Thema [Erstellen von Konfigurationselementen für iOS- und Mac OS X-Geräte, die ohne den System Center Configuration Manager-Client verwaltet werden](/sccm/compliance/deploy-use/create-configuration-items-for-ios-and-mac-os-x-devices-managed-without-the-client) zum Erstellen eines Konfigurationselements vom Typ **iOS und Mac OS X**.
2. Konfigurieren Sie auf der Seite **System Security** (Systemsicherheit) des Assistenten zum Erstellen von Konfigurationselementen die Einstellung **Allow Activation Lock (supervised mode only)** (Aktivieren der Aktivierungssperre (ausschließlich überwachter Modus)) auf **Allowed**(Zulässig).
3. [Erstellen von Konfigurationsbasislinien in System Center Configuration Manager](/sccm/compliance/deploy-use/create-configuration-baselines)
4. [Bereitstellen von Konfigurationsbasislinien in System Center Configuration Manager](/sccm/compliance/deploy-use/deploy-configuration-baselines) an eine Sammlung, die die iOS-Geräte enthält, die für die Aktivierungssperre aktiviert werden soll.

> [!IMPORTANT]
> Stellen Sie sicher, dass das Gerät physisch verfügbar ist, bevor Sie dieses Verfahren ausführen. Falls dies nicht der Fall ist, wird die Aktivierungssperre umgangen. Derjenige, der im Besitz des Geräts ist, verfügt dann über Vollzugriff und kann so „Mein iPhone suchen“ ausschalten, das Gerät auf Werkseinstellung zurücksetzen oder es reaktivieren.

Sie können die Aktivierungssperre nur umgehen oder den Umgehungscode der Aktivierungssperre auf überwachten Geräten abrufen. Wenn Sie versuchen, die Aktivierungssperre auf einem nicht überwachten Gerät zu umgehen oder die Ergebnisse des Umgehungscodes anzuzeigen, tritt ein Fehler auf.



## <a name="view-the-activation-lock-bypass-code"></a>Anzeigen des Codes für die Umgehung der Aktivierungssperre

1. Klicken Sie in der Configuration Manager-Konsole auf **Bestand und Kompatibilität**.
2. Klicken Sie im Arbeitsbereich **Bestand und Kompatibilität** auf **Geräte**.
3. Wählen Sie ein registriertes Gerät aus, das sich im überwachten Modus befindet und eine aktive Aktivierungssperre besitzt.
4. Klicken Sie auf der Registerkarte **Start** in der **Gerätegruppe** auf **Remotegeräteaktionen** > **Umgehungscode für Aktivierungssperre anzeigen**.
5. Im Dialogfeld **Umgehungscode für die Aktivierungssperre** wird der Umgehungscode für das ausgewählte Gerät angezeigt.

## <a name="bypass-activation-lock"></a>Umgehen der Aktivierungssperre

1. Klicken Sie in der Configuration Manager-Konsole auf **Bestand und Kompatibilität**.
2. Klicken Sie im Arbeitsbereich **Bestand und Kompatibilität** auf **Geräte**.
3. Wählen Sie ein registriertes Gerät aus, das sich im überwachten Modus befindet und eine aktive Aktivierungssperre besitzt.
3. Klicken Sie auf der Registerkarte **Start** in der **Gerätegruppe** auf **Remotegeräteaktionen** > **Aktivierungssperre umgehen**.
5. Lesen Sie die Meldungen im Warnungsdialogfeld, und klicken Sie auf **Ja** , wenn Sie bereit sind, fortzufahren.
6. Sie können den Status der Entsperranforderung überprüfen:

    - In den Ermittlungsdaten für das Gerät im Dialogfeld mit den Geräteeigenschaften.
    - In der Spalte **Umgehungsstatus für Aktivierungssperre** in der Ansicht **Geräte** (diese Spalte ist standardmäßig ausgeblendet).
    - Im Abschnitt **Remote Device Actions Information** (Informationen über Remotegeräteaktionen) auf der Registerkarte **Summary** (Zusammenfassung) im Detailbereich (wenn ein Gerät ausgewählt wurde).
