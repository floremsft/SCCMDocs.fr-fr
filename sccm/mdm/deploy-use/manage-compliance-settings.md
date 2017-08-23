---
title: "Verwalten der Kompatibilität auf mit Intune verwalteten Geräten | Microsoft-Dokumentation"
description: "Erfahren Sie mehr über System Center Configuration Manager-Kompatibilitätseinstellungen, indem Sie einige Szenarios durcharbeiten."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9e83007f-e81c-4b7e-b47e-b01d7b19cfbc
caps.latest.revision: "5"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: b3a63f6c55c317c9c84d4394dfdcb9f1cbbbc90b
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="managing-compliance-on-devices-managed-with-intune"></a>Verwalten der Kompatibilität auf mit Intune verwalteten Geräten

*Gilt für: System Center Configuration Manager (Current Branch)*

Diese Szenarios dienen zur Einführung in das Verwenden von System Center Configuration Manager-Kompatibilitätseinstellungen.  

 Wenn Sie bereits mit den Kompatibilitätseinstellungen vertraut sind, finden Sie eine ausführliche Dokumentation zu allen verwendbaren Features im Abschnitt [Configuration items for devices managed with Intune (Konfigurationselemente für Geräte, die mit Intune verwaltet werden)](#configuration-items-for-devices-managed-with-intune).  

 In [Erste Schritte mit Kompatibilitätseinstellungen](../../compliance/get-started/get-started-with-compliance-settings.md) erfahren Sie mehr über einige Grundlagen der Kompatibilitätseinstellungen, und lesen Sie zudem [Planen und Konfigurieren von Kompatibilitätseinstellungen](../../compliance/plan-design/plan-for-and-configure-compliance-settings.md), um jegliche notwendigen Voraussetzungen zu implementieren.  

## <a name="general-information-for-each-scenario"></a>Allgemeine Informationen für jedes Szenario  
 In jedem Szenario erstellen Sie ein Konfigurationselement, das eine bestimmte Aufgabe ausführt. Öffnen Sie den Assistenten zum Erstellen von Konfigurationselementen, und führen Sie die folgenden Schritte aus:  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Bestand und Kompatibilität** > **Kompatibilitätseinstellungen** > **Konfigurationselemente**.  

3.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Erstellen** auf **Konfigurationselement erstellen**.  

4.  Geben Sie auf der Registerkarte **Allgemein** des nachstehend gezeigten Assistenten zum Erstellen von Konfigurationselementen einen Namen und eine Beschreibung des Konfigurationselements an. Wählen Sie dann den für jedes Szenario geeigneten Konfigurationselementtyp.  

     ![Zeigt die Seite „Allgemein“ des Assistenten zum Erstellen von Konfigurationselementen](media/Compliance-Settings-Wizard---1.png)  

## <a name="scenarios-for-windows-81-and-windows-10-devices-managed-with-intune"></a>Szenarios für Windows 8.1 und Windows 10-Geräte, die mit Intune verwaltet werden  

### <a name="scenario-restrict-access-to-the-app-store-on-all-windows-pcs"></a>Szenario: Einschränken des Zugriffs auf den App Store auf allen Windows-PCs  
 In diesem Szenario sind Sie der IT-Administrator eines Unternehmens, das mit hochsensiblen Daten arbeitet. Aus diesem Grund schränken Sie die Apps ein, die Benutzer installieren dürfen. Sie möchten, dass Benutzer aller Windows 10-PCs keine Apps mehr aus dem Windows Store herunterladen können. Deshalb führen Sie die folgenden Schritte aus.  

1.  Wählen Sie im Assistenten zum Erstellen von Konfigurationselementen auf der Seite **Allgemein** den Konfigurationselementtyp **Windows 8.1 und Windows 10** aus, und klicken Sie auf **Weiter**.  

2.  Wählen Sie auf der Seite **Unterstützte Plattformen** alle Windows 10-Plattformen aus.  

3.  Wählen Sie auf der Seite **Geräteeinstellungen** die Option **Store**aus, und klicken Sie dann auf **Weiter**.  

4.  Wählen Sie auf der Seite **Store** die Option **Nicht zulässig** als Einstellung für **App Store**aus.  

5.  Wählen Sie **Nicht kompatible Einstellungen wiederherstellen** aus, um sicherzustellen, dass die Änderung auf alle PCs angewendet wird.  

6.  Schließen Sie den Assistenten ab, um das neue Konfigurationselement zu erstellen.  

 Sie können nun die Informationen im Thema [Allgemeine Aufgaben zum Erstellen und Bereitstellen von Konfigurationsbaselines](../../compliance/plan-design/common-tasks-for-creating-and-deploying-configuration-baselines.md) verwenden, die Ihnen beim Bereitstellen der von Ihnen erstellten Konfiguration auf Geräten helfen.  

## <a name="scenarios-for-windows-phone-devices-managed-with-intune"></a>Szenarios für Windows Phone-Geräte, die mit Intune verwaltet werden  

### <a name="scenario-disable-the-use-of-screen-capture-on-a-windows-phone"></a>Szenario: Deaktivieren von Bildschirmaufnahmen auf einem Windows Phone  
 In diesem Szenario werden in Ihrem Unternehmen Windows Phone 8.1-Geräte verwendet. Auf diesen Geräten läuft eine Vertriebs-App, die vertrauliche Informationen enthält. Zum Schutz Ihres Unternehmens möchten Sie Bildschirmaufnahmen auf dem Gerät deaktivieren, die potenziell dazu genutzt werden können, um vertrauliche Informationen aus Ihrem Unternehmen zu schmuggeln.  

1.  Wählen Sie im Assistenten zum Erstellen von Konfigurationselementen auf der Seite **Allgemein** den Konfigurationselementtyp **Windows Phone** aus, und klicken Sie auf **Weiter**.  

2.  Wählen Sie auf der Seite **Unterstützte Plattformen** **Alle Windows 8.1-Plattformen** aus.  

3.  Wählen Sie auf der Seite **Geräteeinstellungen** die Option **Gerät**aus, und klicken Sie dann auf **Weiter**.  

4.  Wählen Sie auf der Seite **Gerät** die Option **Deaktiviert** als Einstellung für **Bildschirmaufnahme**aus.  

5.  Wählen Sie **Nicht kompatible Einstellungen wiederherstellen** aus, um sicherzustellen, dass die Änderung auf alle Windows Phone 8.1-Geräte angewendet wird.  

6.  Schließen Sie den Assistenten ab, um das neue Konfigurationselement zu erstellen.  

 Sie können nun die Informationen im Thema [Allgemeine Aufgaben zum Erstellen und Bereitstellen von Konfigurationsbaselines mit System Center Configuration Manager](../../compliance/plan-design/common-tasks-for-creating-and-deploying-configuration-baselines.md) verwenden, die Ihnen beim Bereitstellen der von Ihnen erstellten Konfiguration auf Geräten helfen.  

## <a name="scenarios-for-ios-and-mac-os-x-devices-managed-with-intune"></a>Szenarios für iOS und Mac OS X-Geräte, die mit Intune verwaltet werden  

### <a name="scenario-disable-the-camera-on-ios-devices"></a>Szenario: Deaktivieren der Kamera auf iOS-Geräten  
 In diesem Szenario erzeugt Ihr Unternehmen Pläne für neue Produktentwicklungen mit vertraulichen Informationen, die geheim bleiben müssen. Da Ihr Unternehmen allen Mitarbeitern iPhones oder iPads zur Verfügung stellt, möchten Sie die Kamera auf diesen Geräten deaktivieren, um zu verhindern, dass die Pläne fotografiert werden.  

1.  Wählen Sie im Assistenten zum Erstellen von Konfigurationselementen auf der Seite **Allgemein** den Konfigurationselementtyp **iOS und Mac OS X** aus, und klicken Sie auf **Weiter**.  

2.  Wählen Sie auf der Seite **Unterstützte Plattformen** alle iPhone- und iPad-Geräteplattformen aus.  

3.  Wählen Sie auf der Seite **Geräteeinstellungen** die Option **Sicherheit**aus, und klicken Sie dann auf **Weiter**.  

4.  Wählen Sie auf der Seite **Sicherheit** die Option **Nicht zulässig** als Einstellung für **Kamera**aus.  

5.  Wählen Sie **Nicht kompatible Einstellungen wiederherstellen** aus, um sicherzustellen, dass die Änderung auf alle iOS-Geräte angewendet wird.  

6.  Schließen Sie den Assistenten ab, um das neue Konfigurationselement zu erstellen.  

 Sie können nun die Informationen im Thema [Allgemeine Aufgaben zum Erstellen und Bereitstellen von Konfigurationsbaselines mit System Center Configuration Manager](../../compliance/plan-design/common-tasks-for-creating-and-deploying-configuration-baselines.md) verwenden, die Ihnen beim Bereitstellen der von Ihnen erstellten Konfiguration auf Geräten helfen.  

## <a name="scenarios-for-android-and-samsung-knox-standard-devices-managed-with-intune"></a>Szenarios für Android- und Samsung KNOX Standard-Geräte, die mit Intune verwaltet werden  

### <a name="scenario-require-a-password-on-all-android-5-devices"></a>Szenario: Anfordern eines Kennworts auf allen Android 5-Geräten  
 In diesem Szenario erstellen Sie ein Konfigurationselement nur für Android 5-Geräte, das Benutzern auffordert, auf ihren Geräten ein Kennwort mit mindestens 6 Zeichen zu konfigurieren. Wenn ein Benutzer zudem fünfmal ein falsches Kennwort eingibt, wird das Gerät zurückgesetzt.  

1.  Wählen Sie im Assistenten zum Erstellen von Konfigurationselementen auf der Seite **Allgemein** den Konfigurationselementtyp **Android und Samsung KNOX** aus, und klicken Sie auf **Weiter**.  

2.  Wählen Sie auf der Seite **Unterstützte Plattformen** nur **Android 5** aus (um sicherzustellen, dass die Einstellungen nur für diese Plattform gelten).  

3.  Wählen Sie auf der Seite **Geräteeinstellungen** die Option **Kennwort**aus, und klicken Sie dann auf **Weiter**.  

4.  Konfigurieren Sie auf der Seite **Kennwort** die folgenden Einstellungen:  

    -   **Kennworteinstellungen auf Geräten erforderlich** > **Erforderlich**  

    -   **Minimale Kennwortlänge (Zeichen)** > **6**  

    -   **Anzahl der gescheiterten Anmeldeversuche vor dem Zurücksetzen eines Geräts** > **5**  

5.  Schließen Sie den Assistenten ab, um das neue Konfigurationselement zu erstellen.  

 Sie können nun die Informationen im Thema [Allgemeine Aufgaben zum Erstellen und Bereitstellen von Konfigurationsbaselines](../../compliance/plan-design/common-tasks-for-creating-and-deploying-configuration-baselines.md) verwenden, die Ihnen beim Bereitstellen der von Ihnen erstellten Konfiguration auf Geräten helfen.  

## <a name="configuration-items-for-devices-managed-with-intune"></a>Konfigurationselementen für Geräte, die mit Intune verwaltet werden

Folgende Configuration Manager-Konfigurationselementtypen sind für Geräte verfügbar, die nicht vom Configuration Manager-Client verwaltet werden, z.B. Geräte, die bei Microsoft Intune registriert sind.  

 -   [How to create configuration items for Windows 8.1 and Windows 10 devices managed with Intune (Erstellen von Konfigurationselementen für Windows 8.1 und Windows 10-Geräte, die mit Intune verwaltet werden)](create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client.md)  

 -   [How to create configuration items for Windows Phone devices managed with Intune (Erstellen von Konfigurationselementen für Windows Phone-Geräte, die mit Intune verwaltet werden)](create-configuration-items-for-windows-phone-devices-managed-without-the-client.md)  

 -   [How to create configuration items for iOS and Mac OS X devices managed with Intune (Erstellen von Konfigurationselementen für iOS und Mac OS X-Geräte, die mit Intune verwaltet werden)](create-configuration-items-for-ios-and-mac-os-x-devices-managed-without-the-client.md)  

 -   [How to create configuration items for iOS and Mac OS X devices managed with Intune (Erstellen von Konfigurationselementen für Android- und Samsung KNOX Standard-Geräte, die mit Intune verwaltet werden)](create-configuration-items-for-android-and-samsung-knox-devices-managed-without-the-client.md)  
