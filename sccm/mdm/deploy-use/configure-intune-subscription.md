---
title: Konfigurieren Ihres Intune-Abonnements unter Verwendung von System Center Configuration Manager | Microsoft-Dokumentation
description: Konfigurieren Ihres Intune-Abonnements unter Verwendung von System Center Configuration Manager.
ms.custom: na
ms.date: 06/02/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 99de8fe7-560e-401a-8ab2-6d87d091be17
caps.latest.revision: "18"
caps.handback.revision: "0"
author: mtillman
ms.author: mtillman
manager: angrobe
ms.openlocfilehash: 22d890c972d3166f9c7b583d8d3fa917c1897880
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="configure-your-intune-subscription-with-system-center-configuration-manager-and-microsoft-intune"></a>Konfigurieren Ihres Intune-Abonnements mit System Center Configuration Manager und Microsoft Intune

*Gilt für: System Center Configuration Manager (Current Branch)*

Das Intune-Abonnement ermöglicht die Verwaltung von Geräten über das Internet. Dazu gehört auch, Benutzersammlungen anzugeben, die Geräte registrieren können, und Informationen zu definieren, die für Benutzer angezeigt werden. Während der Erstellung des Intune-Abonnements können Sie auch Unternehmensbranding zum Intune-Unternehmensportal mit Ihrem Firmenlogo und benutzerdefinierten Farbschemata hinzufügen.

Die Intune-Abonnement dient zu folgenden Zwecken:

-   Abrufen des Zertifikats, das vom Dienstverbindungspunkt zum Herstellen einer Verbindung mit dem Intune-Dienst benötigt wird
-   Definieren der Benutzersammlung, die Benutzern das Anmelden ihrer mobilen Geräte ermöglicht
-   Definieren und Konfigurieren der mobilen Plattformen, die Sie unterstützen möchten

> [!IMPORTANT]
>  Durch das Erstellen eines Abonnements für Microsoft Intune in Configuration Manager wechselt der Dienstverbindungspunkt Ihres Standorts in den „Onlinemodus“. Weitere Informationen finden Sie unter [Informationen zum Dienstverbindungspunkt in System Center Configuration Manager](../../core/servers/deploy/configure/about-the-service-connection-point.md).

## <a name="to-create-the-microsoft-intune-subscription"></a>So erstellen Sie das Microsoft Intune-Abonnement

1.  Registrieren Sie sich für ein Microsoft Intune-Konto bei [Microsoft Intune](http://go.microsoft.com/fwlink/?LinkID=258216), falls dies noch nicht geschehen ist.  Nachdem Sie Ihr Intune-Konto erstellt haben, ist es nicht erforderlich, Benutzer dem Intune-Konto hinzuzufügen oder zusätzliche Einstellungen zu konfigurieren.

2.  Klicken Sie in der Configuration Manager-Konsole auf **Verwaltung**.

3.  Erweitern Sie im Arbeitsbereich **Verwaltung** den Bereich **Clouddienste**, und klicken Sie auf **Microsoft Intune-Abonnements**. Klicken Sie auf der Registerkarte **Startseite** auf **Microsoft Intune-Abonnement hinzufügen**.

![Erstellen eines Intune-Abonnements](../media/mdm-set-intune.png)

4.  Lesen Sie im Assistenten zum Erstellen von Microsoft Intunes-Abonnements den Text auf der Seite **Einleitung** , und klicken Sie dann auf **Weiter**.

5.  Klicken Sie auf der Seite **Abonnement** auf **Anmelden** , und melden Sie sich mit Ihrem Geschäfts- oder Schulkonto an. Aktivieren Sie im Dialogfeld **Autorität für die Verwaltung mobiler Geräte festlegen** das Kontrollkästchen für die alleinige Verwaltung mobiler Geräte mit Configuration Manager über die Configuration Manager-Konsole. Sie müssen diese Option auswählen, um den Vorgang zum Erstellen Ihres Abonnements fortsetzen zu können.

    > [!IMPORTANT]
    >  Nachdem Sie Configuration Manager als Autorität für die Verwaltung ausgewählt haben, können Sie die Autorität für die Verwaltung erst ab Configuration Manager, Version 1610 oder höher, und Microsoft Intune, Version 1705, auf Microsoft Intune umstellen, ohne den Microsoft Support um Hilfe zu bitten und ohne die Registrierung Ihrer vorhandenen verwalteten Geräten aufzuheben und sie anschließend erneut zu registrieren. Einzelheiten finden Sie unter [Umstellen der MDM-Autorität](/sccm/mdm/deploy-use/change-mdm-authority).

6.  Klicken Sie auf die Datenschutzlinks, um die entsprechenden Informationen zu lesen, und klicken Sie dann auf **Weiter**.

7.  Geben Sie auf der Seite **Allgemein** die folgenden Optionen an, und klicken Sie dann auf **Weiter**.

  -   **Sammlung**: Geben Sie eine Benutzersammlung an, in der die Benutzer enthalten sind, die ihre mobilen Geräte anmelden dürfen.

      > [!NOTE]
      >  Wird ein Benutzer aus der Sammlung entfernt, wird das Gerät des Benutzers noch bis zu 24 Stunden verwaltet, nachdem der Benutzerdatensatz aus der Benutzerdatenbank entfernt wurde.

  -   **Firmenname**: Geben Sie den Namen Ihres Unternehmens ein.

  -   **Datenschutzdokumentations-URL des Untern.**: Wenn Sie die Datenschutzinformationen Ihres Unternehmens über einen Link veröffentlichen, auf den über das Internet zugegriffen werden kann, stellen Sie einen Link bereit, auf den die Benutzer über das Unternehmensportal zugreifen können, z. B. „http://www.contoso.com/CP_privacy.html“. Aus den Datenschutzinformationen geht hervor, welche Informationen Benutzer für Ihr Unternehmen freigeben.

  -   **Farbschema für Unternehmensportal**: Sie können optional die Standardfarbe Blau für Unternehmensportale ändern.

  -   **Configuration Manager-Standortcode**: Geben Sie einen Standortcode für einen primären Standort zum Verwalten der mobilen Geräte an.

    > [!NOTE]
    >  Das Ändern des Standortcodes wirkt sich nur auf neue Anmeldungen aus und beeinflusst gegenwärtig angemeldete Geräte nicht.

8.  Geben Sie auf der Seite **Kontaktdaten des Unternehmens** die Kontaktdaten des Unternehmens an, die unter **An IT-Abteilung wenden** in der Unternehmensportal-App angezeigt werden. Geben Sie Kontaktinformationen für Ihr Unternehmen ein, und klicken Sie dann auf **Weiter**.

9. Auf der Seite **Firmenlogo** können Sie wählen, ob Logos im Unternehmensportal angezeigt werden sollen. Klicken Sie dann auf **Weiter**.

10. Schließen Sie den Assistenten ab.

> [!div class="button"]
[< Vorheriger Schritt](confirm-dns.md) [Nächster Schritt >](terms-and-conditions.md)
