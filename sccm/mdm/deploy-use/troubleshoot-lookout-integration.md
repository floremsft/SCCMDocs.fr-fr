---
title: Behandeln von Problemen bei der Lookout-Integration | System Center Configuration Manager
description: "Dieses Thema beschreibt die Behandlung von Problemen, die häufig bei der Lookout-Integration auftreten."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e36b98c7-d0f4-4dd6-bac3-6a6c4b4bf841
caps.latest.revision: 
author: mtillman
ms.author: mtillman
manager: angrobe
ms.openlocfilehash: 4fd2d3b8aae6a2f42e7c6a87723d16368be30984
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="troubleshoot-lookout-integration-with-intune"></a>Behandeln von Problemen bei der Lookout-Integration mit Intune

*Gilt für: System Center Configuration Manager (Current Branch)*

## <a name="troubleshoot-login-errors"></a>Problembehandlung für Fehler beim Anmelden
### <a name="403-errors"></a>403-Fehler
Möglicherweise wird ein 403-Fehler angezeigt, wenn Sie sich bei der [Lookout-MTP-Konsole](https://aad.lookout.com) anmelden: **you are not authorized to access the service** (Sie sind nicht zum Zugriff auf den Dienst berechtigt.). Dies kann passieren, wenn der angegebene Benutzername kein Mitglied der Azure Active Directory-Gruppe (Azure AD) ist, die für den Zugriff auf Lookout MTP konfiguriert ist.

Lookout MTP ist so konfiguriert, dass nur Benutzer von einer konfigurierten Azure AD-Gruppe Zugriff haben. Wenn Sie nicht sicher sind, welche Gruppe mit Zugriff auf Lookout MTP konfiguriert ist, wenden Sie sich an den Lookout Support.

Sie können den Lookout Support über die folgenden Methoden kontaktieren:

* E-Mail: enterprisesupport@lookout.com
* Melden Sie sich bei der [MTP-Konsole](http://aad.lookout.com) an, und navigieren Sie zum Modul **Support**.
* Wechseln Sie zu: https://enterprise.support.lookout.com/hc/en-us/requests, und stellen Sie eine Supportanfrage.

### <a name="unable-to-sign-in"></a>Anmelden nicht möglich
Möglicherweise wird der folgende Fehler angezeigt, wenn der globale Administrator von Azure AD das ursprüngliche Lookout-Setup nicht akzeptiert hat.

![Screenshot des Lookout-Anmeldebildschirms, in dem ein Anmeldefehler angezeigt wird](media/lookout-consent-not-accepted-error.png)

Um dieses Problem zu beheben, muss sich der globale Administrator bei https://aad.lookout.com/les?action=consent anmelden und die Eingabeaufforderung akzeptieren, um das Setup zu initiieren. Ausführlichere Informationen finden Sie im Thema [Einrichten eines Abonnements mit Lookout MTP](set-up-your-subscription-with-lookout.md)

## <a name="troubleshoot-device-status-issues"></a>Behandlung von Gerätestatusproblemen

### <a name="device-not-showing-up-in-the-lookout-mtp-console-device-list"></a>Gerät wird nicht in der Lookout MTP Konsolen-Geräteliste angezeigt

Dies kann in den folgenden Szenarios auftreten:
* Wenn sich der Benutzer, der dieses Gerät besitzt, nicht in der **Registrierungsgruppe** befindet, die in der **Lookout-MTP-Konsole** angegeben ist.  Wechseln Sie im Modul **System** auf die Registerkarte **Intune Connector**, und sehen Sie sich die Einstellungen für **Registrierungsverwaltung** an.  Sie sollten eine oder mehrere Azure AD-Gruppen für die Registrierung konfiguriert sehen.  Stellen Sie sicher, dass der Benutzer, der das fehlende Gerät besitzt, Teil einer der angegebenen Azure AD-Gruppen ist.  Sobald ein neuer Benutzer der Registrierungsgruppe hinzugefügt wird, dauert es bis zum konfigurierten Abfrageintervall (5 Minuten ist die Standardeinstellung), bis das Gerät im Modul **Geräte** der Lookout MTP-Konsole angezeigt wird.

* Wenn das Gerät nicht von Lookout MTP unterstützt wird.  Nicht unterstützte Geräte erscheinen im Abschnitt **Verwaltete Geräte** der Connector-Einstellungen auf der Lookout MTP-Konsole.

### <a name="device-continues-to-be-reported-as-pending"></a>Gerät weiterhin als **ausstehend** gemeldet

Ein Gerät, das **ausstehend** anzeigt, bedeutet, dass der Endbenutzer nicht die Lookout for Work App geöffnet und die Schaltfläche **Aktivieren** angetippt hat. Weitere Informationen zur Geräteaktivierung mit der Lookout for Work App finden Sie unter folgendem Thema:

[Sie werden zur Installation von Lookout for Work auf Ihrem Android-Gerät aufgefordert](http://docs.microsoft.com/intune/enduser/you-are-prompted-to-install-lookout-for-work-android)

### <a name="in-the-lookout-mtp-console-a-device-is-showing-as-active-but-does-not-have-a-device-id"></a>In der Lookout MTP-Konsole wird ein Gerät als aktiv angezeigt, hat aber keine Geräte-ID.
Dies bedeutet, dass sich der Benutzer, der dieses Gerät besitzt, nicht in der Registrierungsgruppe befindet, die in der Lookout MTP-Konsole angegeben ist.   Ein Gerät kann in diesen Zustand kommen, wenn der Benutzer, der das Gerät besitzt, aus der Registrierungsgruppe entfernt wurde oder die Registrierungsgruppe, zu der der Benutzer gehört, entfernt wurde.

Wechseln Sie auf dem Modul **System** auf der Lookout MTP-Konsole auf die Registerkarte **Intune Connector**, und prüfen Sie die Einstellungen für die **Registrierung**.  Sie sollten eine oder mehrere Azure AD-Gruppen für die Registrierung konfiguriert sehen.  Stellen Sie sicher, dass der Benutzer, der das Gerät besitzt, Teil einer der angegebenen Azure AD-Gruppen ist.

Während ein Gerät in diesem Zustand ist, wird Lookout weiterhin den Benutzer über alle erfassten Bedrohungen informieren, jedoch keine Bedrohungsinformationen an Intune senden.

### <a name="device-shows-disconnected-state"></a>Gerät zeigt getrennten Zustand an

Getrennt bedeutet, dass Lookout MTP über ein vorkonfiguriertes Zeitintervall nichts mehr vom Gerät gehört hat (Standardeinstellung ist 30 Tage bei einem Minimum von 7 Tagen). Das bedeutet, dass entweder die Unternehmensportal-App oder die Lookout for Work-App nicht auf dem Gerät installiert oder deinstalliert wurde. Die Neuinstallation der Apps sollte dieses Problem beheben. Wenn der Benutzer Lookout for Work öffnet und die App aktiviert, resynchronisiert das Gerät mit Lookout MTP und Intune.

### <a name="forcing-a-resync-on-the-device"></a>Erzwingen einer Resynchronisierung auf dem Gerät
Über das Modul **Geräte** der Lookout MTP-Konsole kann der Administrator das Gerät auswählen und löschen.   Das nächste Mal, wenn der Geräteeigentümer die Lookout for Work-App öffnet und auf **Aktivieren** tippt, führt der Gerätezustand eine vollständige Resynchronisierung durch.

### <a name="the-owner-of-the-device-is-no-longer-using-this-device"></a>Der Geräteeigentümer verwendet das Gerät nicht mehr
Sie müssen das Gerät zurücksetzen und den neuen Benutzer auffordern, sich neu zu registrieren, wie in [diesem Thema](https://docs.microsoft.com/en-us/sccm/mdm/deploy-use/wipe-lock-reset-devices#full-wipe) beschrieben.


Sie können auch das Modul **Geräte** der Lookout MTP-Konsole aufrufen und **Löschen** auswählen.

Solange sich der neue Benutzer in einer der Registrierungsgruppen befindet, die in der Lookout MTP-Konsole angegeben sind, wird das Gerät angezeigt, sobald Azure AD das Gerät dem neuen Benutzer zuordnet.

## <a name="compliance-remediation-workflows"></a>Workflows zur Konformitätswiederherstellung
[Sie werden zur Installation von Lookout for Work auf Ihrem Android-Gerät aufgefordert]( http://docs.microsoft.com/intune/enduser/you-are-prompted-to-install-lookout-for-work-android)

[Sie müssen eine Bedrohung beheben, die Lookout for Work auf Ihrem Android-Gerät gefunden hat](http://docs.microsoft.com/intune/enduser/you-need-to-resolve-a-threat-found-by-lookout-for-work-android)
