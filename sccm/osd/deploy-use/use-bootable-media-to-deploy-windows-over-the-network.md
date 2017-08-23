---
title: "Verwenden startbarer Medien zum Bereitstellen von Windows über das Netzwerk | Microsoft-Dokumentation"
description: Verwenden Sie Bereitstellungen mit startbaren Medien in System Center Configuration Manager zum Bereitstellen des Betriebssystem beim Starten des Zielcomputers.
ms.custom: na
ms.date: 6/16/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 999b5409-7e72-48d2-8554-4d44427ce383
caps.latest.revision: "5"
author: mattbriggs
ms.author: mattbriggs
manager: angrobe
ms.openlocfilehash: 9b20e5e2a66d92038033e816e6fc701581c48a7f
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="use-bootable-media-to-deploy-windows-over-the-network-with-system-center-configuration-manager"></a>Verwenden startbarer Medien zum Bereitstellen von Windows über das Netzwerk mit System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Sie können das Betriebssystem bereitstellen, wenn der Zielcomputer mithilfe einer Bereitstellung mit startbaren Medien gestartet wird. Die Medien enthalten einen Zeiger auf die Tasksequenz, das Betriebssystemabbild und andere erforderliche Inhalte aus dem Netzwerk. Beim Starten des Zielcomputers ruft der Computer die Elemente ab, auf die im Zeiger verwiesen wird. Wenn die startbaren Medien ohne Inhalt sind, können Sie das Ziel aktualisieren, ohne es auf den Medien ersetzen zu müssen.

Sie können in den folgenden Szenarien für die Betriebssystembereitstellung die Betriebssysteme mithilfe von Multicast über das Netzwerk bereitstellen:

-   [Aktualisieren eines vorhandenen Computers mit einer neuen Version von Windows](refresh-an-existing-computer-with-a-new-version-of-windows.md)

-   [Installieren einer neuen Version von Windows auf einem neuen Computer (Bare-Metal)](install-new-windows-version-new-computer-bare-metal.md)  

-   [Ersetzen eines vorhandenen Computers und Übertragen von Einstellungen](replace-an-existing-computer-and-transfer-settings.md)  

Führen Sie die Schritte in einem der Betriebssystembereitstellungsszenarien aus, und verwenden Sie dann die folgenden Abschnitte, um startbare Medien zum Bereitstellen des Betriebssystems zu verwenden.  

## <a name="configure-deployment-settings"></a>Konfigurieren von Bereitstellungseinstellungen  
Wenn Sie startbare Medien verwenden, um den Bereitstellungsprozess für das Betriebssystem zu starten, konfigurieren Sie die Bereitstellung so, dass das Betriebssystem für die Medien zur Verfügung gestellt wird. Sie können diese Option auf der Seite **Bereitstellungseinstellungen** im Assistenten zum Bereitstellen von Software oder auf der Registerkarte **Bereitstellungseinstellungen** in den Eigenschaften der Bereitstellung konfigurieren. Konfigurieren Sie eine der folgenden Optionen für die Einstellung **Verfügbar machen für** :

-   Configuration Manager-Clients, Medien und PXE

-   Nur Medien und PXE

-   Nur Medien und PXE (ausgeblendet)

## <a name="create-the-bootable-media"></a>Erstellen der startbaren Medien
Sie können angeben, ob das startbare Medium ein USB-Flashlaufwerk oder ein CD/DVD-Satz ist. Der Computer, der die Medien startet, muss die Option unterstützen, die Sie als startbares Laufwerk auswählen. Weitere Informationen finden Sie unter [Erstellen startbarer Medien](create-bootable-media.md).  

##  <a name="BKMK_Deploy"></a> Installieren des Betriebssystems von startbaren Medien  
Legen Sie die startbaren Medien in ein startfähiges Laufwerk des Computer ein. Schalten Sie dann den Computer ein, um das Betriebssystem zu installieren.
