---
title: "Verwenden eigenständiger Medien zum Bereitstellen von Windows ohne Verwendung des Netzwerks | Microsoft-Dokumentation"
description: "Verwenden Sie eigenständige Medien in Configuration Manager zum Bereitstellen von Betriebssystemen, bei denen die Bandbreite eingeschränkt ist, oder als eine Option zum Auffrischen, Installieren oder Upgraden von Computern."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 58a0d2ae-de76-401f-b854-7a5243949033
caps.latest.revision: "16"
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: 30ae794381c6894e11b21a8167d0af60463c5279
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="use-stand-alone-media-to-deploy-windows-without-using-the-network-in-system-center-configuration-manager"></a>Verwenden eigenständiger Medien zum Bereitstellen von Windows ohne Verwendung des Netzwerks in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Eigenständige Medien in System Center Configuration Manager enthalten alles, was zur Bereitstellung des Betriebssystems auf einem Computer erforderlich ist. Hierzu gehören das Startabbild, das Betriebssystemabbild und die Tasksequenz zum Installieren des Betriebssystems sowie von Anwendungen, Treibern usw. Mit eigenständigen Medienbereitstellungen können Sie unter folgenden Umständen Betriebssysteme bereitstellen:  

-   In Umgebungen, in denen es nicht praktikabel ist, ein Betriebssystemabbild oder anderen große Pakete über das Netzwerk zu kopieren;  

-   in Umgebungen ohne Netzwerkverbindung oder mit geringer Netzwerkbandbreite.  

Sie können eigenständige Medien in folgenden Szenarien für die Betriebssystembereitstellung verwenden:  

-   [Aktualisieren eines vorhandenen Computers mit einer neuen Version von Windows](refresh-an-existing-computer-with-a-new-version-of-windows.md)  

-   [Installieren einer neuen Version von Windows auf einem neuen Computer (Bare-Metal)](install-new-windows-version-new-computer-bare-metal.md)  

-   [Upgrade von Windows auf die neueste Version](upgrade-windows-to-the-latest-version.md)  

 Führen Sie die Schritte in einem der Betriebssystembereitstellungsszenarien aus, und lesen Sie dann die folgenden Abschnitte, um die eigenständigen Medien vorzubereiten und zu erstellen.  

## <a name="task-sequence-actions-not-supported-when-using-stand-alone-media"></a>Tasksequenzaktionen, die bei Verwendung eigenständiger Medien nicht unterstützt werden  
 Wenn Sie die Schritte in einem der unterstützten Szenarien für die Betriebssystembereitstellung abgeschlossen haben, wurde die Tasksequenz zum Bereitstellen bzw. Aktualisieren des Betriebssystems erstellt, und alle dazugehörigen Inhalte wurden an einen Verteilungspunkt verteilt. Wenn Sie eigenständige Medien verwenden, werden die folgenden Aktionen in der Tasksequenz nicht unterstützt:  

-   Der Schritt „Treiber automatisch anwenden“ in der Tasksequenz. Die automatische Anwendung von Gerätetreibern aus dem Treiberkatalog wird nicht unterstützt, Sie können aber den Schritt „Treiberpaket anwenden“ auswählen, um Windows Setup eine angegebene Gruppe von Treibern verfügbar zu machen.  

-   Installieren von Softwareupdates  

-   Installieren von Software vor dem Bereitstellen des Betriebssystems  

-   Zuweisen von Benutzern zum Zielcomputer, um die Affinität zwischen Benutzer und Gerät zu unterstützen  

-   Dynamische Paketinstallationen über den Task „Pakete installieren“.  

-   Dynamische Anwendungsinstallationen über den Task „Anwendung installieren“.  

> [!NOTE]  
>  Wenn die Tasksequenz zum Bereitstellen eines Betriebssystems den Schritt [Paket installieren](../understand/task-sequence-steps.md#BKMK_InstallPackage) enthält und Sie die eigenständigen Medien an einem Standort der zentralen Verwaltung erstellen, kann ein Fehler auftreten. Der Standort der zentralen Verwaltung verfügt nicht über die erforderlichen Clientkonfigurationsrichtlinien, die während der Ausführung der Tasksequenz zum Aktivieren des Softwareverteilungs-Agents benötigt werden. In der Datei „CreateTsMedia.log“ wird möglicherweise der folgenden Fehler angezeigt:  
>   
>  `"WMI method SMS_TaskSequencePackage.GetClientConfigPolicies failed (0x80041001)"`
>   
>  Sie müssen eigenständige Medien, die den Schritt **Paket installieren** aufweisen, an einem primären Standort erstellen, für den der Softwareverteilungs-Agent aktiviert ist. Alternativ dazu können Sie den Schritt [Befehlszeile ausführen](../understand/task-sequence-steps.md#BKMK_RunCommandLine) nach dem Schritt [Windows und ConfigMgr einrichten](../understand/task-sequence-steps.md#BKMK_SetupWindowsandConfigMgr) und vor dem ersten Schritt **Paket installieren** hinzufügen. Im Schritt **Befehlszeile ausführen** wird ein WMIC-Befehl ausgeführt, um den Softwareverteilungs-Agent vor der Ausführung des ersten Schritts "Paket installieren" zu aktivieren. Sie können im Tasksequenzschritt **Befehlszeile ausführen** Folgendes verwenden:  
>   
>  **Command Line**: **WMIC /namespace:\\\root\ccm\policy\machine\requestedconfig path ccm_SoftwareDistributionClientConfig CREATE ComponentName="Enable SWDist", Enabled="true", LockSettings="TRUE", PolicySource="local", PolicyVersion="1.0", SiteSettingsKey="1" /NOINTERACTIVE**  

## <a name="configure-deployment-settings"></a>Konfigurieren von Bereitstellungseinstellungen  
 Wenn Sie eigenständige Medien verwenden, um den Bereitstellungsprozess für das Betriebssystem zu starten, müssen Sie die Bereitstellung konfigurieren, um das Betriebssystem für die Medien zur Verfügung zu stellen. Sie können dies auf der Seite der **Bereitstellungseinstellungen** des Assistenten oder der Registerkarte für die **Bereitstellungseinstellungen** in den Eigenschaften für die Bereitstellung konfigurieren.  Konfigurieren Sie eine der folgenden Optionen für die Einstellung **Verfügbar machen für** :  

-   **Configuration Manager-Clients, Medien und PXE**  

-   **Nur Medien und PXE**  

-   **Nur Medien und PXE (ausgeblendet)**  

## <a name="create-the-stand-alone-media"></a>Erstellen der eigenständigen Medien  
 Sie können angeben, ob das eigenständige Medium ein USB-Flashlaufwerk oder ein CD/DVD-Satz ist. Der Computer, der die Medien startet, muss die Option unterstützen, die Sie als startbares Laufwerk auswählen. Weitere Informationen finden Sie unter [Erstellen eigenständiger Medien](create-stand-alone-media.md).  

## <a name="install-the-operating-system-from-stand-alone-media"></a>Installieren des Betriebssystems von eigenständigen Medien  
 Legen Sie die eigenständigen Medien in ein startfähiges Laufwerk des Computers ein. Schalten Sie dann den Computer ein, um das Betriebssystem zu installieren.  
