---
title: "Erstellen eines Images für ein OEM-Vorinstallations- oder lokales Depot | Microsoft-Dokumentation"
description: "Verwenden Sie vorab bereitgestellte Medienbereitstellungen zum Reduzieren des Netzwerkverkehrs, während Sie ein Betriebssystem für Computer bereitstellen, die nicht vollständig bereitgestellt sind."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a7d3df90-062d-4d57-9e9d-e137d3e7cd7f
caps.latest.revision: "8"
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: 07aba04fb1b845e389a5f75b115d536136c1569c
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="create-an-image-for-an-oem-in-factory-or-a-local-depot-with-system-center-configuration-manager"></a>Erstellen eines Images für ein OEM-Vorinstallations- oder lokales Depot mit System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Bei Bereitstellungen mit vorab bereitgestellten Medien in System Center Configuration Manager können Sie ein Betriebssystem für Computer bereitstellen, die nicht vollständig bereitgestellt sind. Bei vorab bereitgestellten Medien handelt es sich um eine WIM-Datei (Windows Imaging Format), die vom Hersteller (OEM) auf einem Computer ohne Betriebssystem oder im Staging Center eines Unternehmens ohne Verbindung zur Configuration Manager-Umgebung installiert werden kann. Später wird der Computer in der Configuration Manager-Umgebung mithilfe des auf den Medien bereitgestellten Startimages gestartet, auf den vorab bereitgestellten Medien wird eine Hashüberprüfung ausgeführt, um die Gültigkeit sicherzustellen, und wird der Computer mit dem Verwaltungspunkt des Standorts verbunden und der Downloadvorgang mithilfe der dort verfügbaren Tasksequenzen abgeschlossen.


Durch diese Bereitstellungsmethode wird der Netzwerkdatenverkehr reduziert, da das Startabbild und Betriebssystemabbild bereits auf dem Zielcomputer vorhanden sind. Sie können auch Anwendungen, Pakete und Treiberpakete als vorab bereitgestellte Medien angeben. Nachdem das Betriebssystem auf dem Computer installiert wurde, wird der Cache der Tasksequenz zunächst auf Anwendungen, Pakete oder Treiberpakete geprüft. Wenn kein Inhalt gefunden oder der Inhalt geprüft wurde, wird er von einem Verteilungspunkt heruntergeladen, der in dem vorab bereitgestellten Medium konfiguriert wurde, und anschließend installiert.  

 Sie können vorab bereitgestellte Medien in den folgenden Szenarios für die Betriebssystembereitstellung verwenden:  

-   [Installieren einer neuen Version von Windows auf einem neuen Computer (Bare-Metal)](install-new-windows-version-new-computer-bare-metal.md)  

-   [Ersetzen eines vorhandenen Computers und Übertragen von Einstellungen](replace-an-existing-computer-and-transfer-settings.md)  

 Führen Sie die Schritte in einem der Betriebssystembereitstellungsszenarien aus, und verwenden Sie dann die folgenden Abschnitte, um die vorab bereitgestellten Medien vorzubereiten und zu erstellen.  

## <a name="configure-deployment-settings"></a>Konfigurieren von Bereitstellungseinstellungen  
 Wenn Sie vorab bereitgestellte Medien verwenden, um den Bereitstellungsprozess für das Betriebssystem zu starten, müssen Sie die Bereitstellung konfigurieren, um das Betriebssystem für die Medien zur Verfügung zu stellen. Sie können dies auf der Seite der **Bereitstellungseinstellungen** des Assistenten oder der Registerkarte für die **Bereitstellungseinstellungen** in den Eigenschaften für die Bereitstellung konfigurieren.  Konfigurieren Sie eine der folgenden Optionen für die Einstellung **Verfügbar machen für** :  

-   **Configuration Manager-Clients, Medien und PXE**  

-   **Nur Medien und PXE**  

-   **Nur Medien und PXE (ausgeblendet)**  

## <a name="create-the-prestaged-media"></a>Erstellen der vorab bereitgestellten Medien  
 Erstellen der vorab bereitgestellten Mediendatei zum Versand an den OEM oder Ihr lokales Depot. Weitere Informationen finden Sie unter [Create prestaged media with System Center Configuration Manager](create-prestaged-media.md).  

## <a name="send-the-prestaged-media-file-to-the-oem-or-local-depot"></a>Senden der vorab bereitgestellten Mediendatei an den OEM oder Ihr lokales Depot  
 Senden Sie die Medien an den OEM oder Ihr lokales Depot, um die Computer vorab bereitzustellen. Die vorab bereitgestellte Mediendatei wird auf einer formatierten Festplatte auf dem Computer installiert.  

## <a name="start-the-computer-to-install-the-operating-system"></a>Starten des Computers, um das Betriebssystem zu installieren  
 Die vorab bereitgestellte Mediendatei wird auf Computern installiert. Beim erstmaligen Starten des Computers wird die Betriebssysteminstallation gestartet.  
