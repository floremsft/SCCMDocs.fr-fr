---
title: Erstellen eines Dienstverbindungspunkts unter Verwendung von System Center Configuration Manager | Microsoft-Dokumentation
description: Erstellen eines Dienstverbindungspunkts unter Verwendung von System Center Configuration Manager.
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 617abb22-d22f-41fb-a76b-1c4259e419d2
caps.latest.revision: "18"
caps.handback.revision: "0"
author: mtillman
ms.author: mtillman
manager: angrobe
ms.openlocfilehash: 9a21d02cb2a50162e5de50481f0f27f2dd7a616c
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="create-a-service-connection-point-with-system-center-configuration-manager-and-microsoft-intune"></a>Erstellen eines Dienstverbindungspunkts mit System Center Configuration Manager und Microsoft Intune

*Gilt für: System Center Configuration Manager (Current Branch)*

Nachdem Sie Ihr Abonnement erstellt haben, können Sie die Standortsystemrolle „Dienstverbindungspunkt“ installieren, die es Ihnen ermöglicht, eine Verbindung mit dem Intune-Dienst herzustellen. Von dieser Standortsystemrolle werden Einstellungen und Anwendungen mittels Push an den Intune-Dienst übertragen.

 Vom Dienstverbindungspunkt werden Einstellungen und Softwarebereitstellungsinformationen an Configuration Manager gesendet sowie Status- und Inventurmeldungen von mobilen Geräten abgerufen. Der Configuration Manager-Dienst fungiert als Gateway, das mit mobilen Geräten kommuniziert und Einstellungen speichert.

> [!NOTE]
>  Die Standortsystemrolle „Dienstverbindungspunkt“ kann nur an einem Standort der zentralen Verwaltung oder an einem eigenständigen primären Standort installiert werden. Der Dienstverbindungspunkt muss über Internetzugriff verfügen.


## <a name="configure-the-service-connection-point-role"></a>Konfigurieren der Rolle „Dienstverbindungspunkt“

1.  Klicken Sie in der Configuration Manager-Konsole auf **Verwaltung**.

2.  Erweitern Sie im Arbeitsbereich **Verwaltung** den Bereich **Standorte**, und klicken Sie dann auf **Server und Standortsystemrollen**.

3.  Fügen Sie einem neuen oder vorhandenen Standortsystemserver die Rolle **Dienstverbindungspunkt** wie folgt hinzu:

    -   Neuer Standortsystemserver: Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Erstellen** auf **Standortsystemserver erstellen** , um den Assistenten zum Erstellen von Standortsystemservern zu starten.

    -   Bestehender Standortsystemserver: Klicken Sie auf den Server, auf dem die Rolle „Dienstverbindungspunkt“ installiert werden soll. Klicken Sie dann auf der Registerkarte **Startseite** in der Gruppe **Server** auf **Standortsystemrollen hinzufügen** , um den Assistenten zum Hinzufügen von Standortsystemrollen zu starten.

4.  Wählen Sie auf der Seite **Systemrollenauswahl** die Option **Dienstverbindungspunkt**, und klicken Sie auf **Weiter**.
![Erstellen eines Dienstverbindungspunkts](../media/mdm-service-connection-point.png)

* Schließen Sie den Assistenten ab.

## <a name="how-does-the-service-connection-point-authenticate-with-the-microsoft-intune-service"></a>Wie authentifiziert sich der Dienstverbindungspunkt beim Microsoft Intune-Dienst?
 Der Systemverbindungspunkt erweitert den Configuration Manager, indem er eine Verbindung mit dem cloudbasierten Intune-Dienst herstellt, der mobile Geräte über das Internet verwaltet. Die Authentifizierung des Dienstverbindungspunkts beim Intune-Dienst geschieht auf folgende Weise:

1.  Beim Erstellen eines Intune-Abonnements in der Configuration Manager-Konsole wird der Configuration Manager-Administrator durch Herstellen einer Verbindung mit Azure Active Directory authentifiziert. Dadurch erfolgt eine Umleitung zum jeweiligen AD FS-Server, der zur Eingabe des Benutzernamens und Kennworts auffordert. Anschließend stellt Intune ein Zertifikat für den Mandanten aus.

2.  Das Zertifikat aus Schritt 1 wird in der Standortrolle „Dienstverbindungspunkt“ installiert und zum Authentifizieren und Autorisieren der gesamten weiteren Kommunikation mit dem Microsoft Intune-Dienst verwendet.

> [!div class="button"]
[< Vorheriger Schritt](terms-and-conditions.md) [Nächster Schritt >](enable-platform-enrollment.md)
