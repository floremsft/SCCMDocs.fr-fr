---
title: "Vorbereiten auf Bereitstellungen für unbekannte Computer | Microsoft-Dokumentation"
description: Erfahren Sie, wie Sie Betriebssysteme auf Computern bereitstellen, die nicht von Configuration Manager in der System Center Configuration Manager-Umgebung verwaltet werden.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9e447e34-0943-49ed-b6ba-3efebf3566c1
caps.latest.revision: "10"
caps.handback.revision: "0"
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: 445e76950f0605da917f3d0e7e71557d969e3c2d
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="prepare-for-unknown-computer-deployments-in-system-center-configuration-manager"></a>Vorbereiten auf Bereitstellungen für unbekannte Computer in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Verwenden Sie die Informationen in diesem Thema, um Betriebssysteme für unbekannte Computer in Ihrer System Center Configuration Manager-Umgebung bereitzustellen. Ein unbekannter Computer ist ein Computer, der nicht von Configuration Manager verwaltet wird. Für diese Computer gibt es in der Configuration Manager-Datenbank keine Einträge. Zu unbekannten Computern gehören die folgenden:  

-   Computer, auf denen kein Configuration Manager-Client installiert ist  

-   Computer, die nicht in Configuration Manager importiert wurden  

-   Computer, die von Configuration Manager nicht ermittelt wurden  

 Sie können Betriebssysteme mit den folgenden Bereitstellungsmethoden für unbekannte Computer bereitstellen:  

-   [Verwenden von PXE zum Bereitstellen von Windows über das Netzwerk](../deploy-use/use-pxe-to-deploy-windows-over-the-network.md)  

-   [Verwenden startbarer Medien zum Bereitstellen eines Betriebssystems](../deploy-use/create-bootable-media.md)  

-   [Verwenden vorab bereitgestellter Medien zum Bereitstellen eines Betriebssystems](../deploy-use/create-prestaged-media.md)  

## <a name="unknown-computer-deployment-workflow"></a>Bereitstellungsworkflow bei unbekannten Computern  
 Im Folgenden wird der grundlegende Workflow zum Bereitstellen eines Betriebssystems für einen unbekannten Computer beschrieben:  

-   Wählen Sie ein unbekanntes Computerobjekt aus, das Sie für die Bereitstellung verwenden möchten. Sie können das Betriebssystem einem der unbekannten Computerobjekte in der Sammlung **Alle unbekannten Computer** hinzufügen, oder Sie können die Objekte in der Sammlung **Alle unbekannten Computer** einer anderen Sammlung hinzufügen. In Configuration Manager gibt es in der Sammlung **Alle unbekannten Computer** zwei unbekannte Computerobjekte. Eins davon ist für x86-Computer, das andere für x64-Computer.  

    > [!NOTE]  
    >  Das Objekt **x 86 unbekannter Computer** ist für Computer, die nur x86-fähig sind. Das Objekt **x64 Unbekannter Computer** ist für Computer bestimmt, die x86- und x64-fähig sind. Mit anderen Worten, diese Objekte beschreiben die Architektur des Zielcomputers. Es wird nicht das Betriebssystem beschrieben, das Sie auf dem Zielcomputer bereitstellen möchten.  

-   Konfigurieren Sie einen PXE-fähigen Verteilungspunkt, oder erstellen Sie ein Medium zur Unterstützung von Bereitstellungen für unbekannte Computer.  

-   Stellen Sie die Tasksequenz zum Installieren des Betriebssystems bereit.  

## <a name="unknown-computer-installation-process"></a>Installationsprozess eines unbekannten Computers  
 Wenn ein Computer erstmals von PXE oder Medien gestartet wird, wird von Configuration Manager geprüft, ob in der Configuration Manager-Datenbank ein Eintrag für diesen Computer besteht. Ist dies der Fall, wird von Configuration Manager geprüft, ob Tasksequenzen für diesen Eintrag bereitgestellt wurden. Besteht kein Eintrag, wird von Configuration Manager geprüft, ob Tasksequenzen für ein unbekanntes Computerobjekt bereitgestellt wurden. In beiden Fällen wird von Configuration Manager eine der folgenden Aktionen ausgeführt:  

-   Wenn eine Tasksequenz verfügbar ist, wird der Benutzer von Configuration Manager dazu aufgefordert, die Tasksequenz auszuführen.  

-   Wenn eine erforderliche Tasksequenz verfügbar ist, wird die Tasksequenz von Configuration Manager automatisch ausgeführt.  

-   Wenn für einen Eintrag keine Tasksequenz bereitgestellt wurde, wird von Configuration Manager eine entsprechende Fehlermeldung generiert.  

 Wenn ein unbekannter Computer gestartet wird, wird er von Configuration Manager nicht als unbekannter Computer, sondern als nicht bereitgestellter Computer erkannt. Das bedeutet, dass der Computer nun die Tasksequenzen erhalten kann, die dem unbekannten Computerobjekt bereitgestellt wurden. Von der bereitgestellten Tasksequenz wird anschließend ein Betriebssystemimage installiert, das den Configuration Manager-Client enthalten muss.  

 Nach der Installation des Configuration Manager-Clients wird ein Eintrag für den Computer erstellt, und der Computer wird in der entsprechenden Configuration Manager-Sammlung angezeigt. Wenn beim Installieren des Betriebssystemimages oder des Configuration Manager-Clients ein Fehler auftritt, wird für den Computer ein Eintrag „Unbekannt“ erstellt, und der Computer wird in der Sammlung **Alle Systeme** angezeigt.  

> [!NOTE]  
>  Beim Installieren des Betriebssystemabbilds können Variablen der Sammlung, nicht jedoch Computervariablen von diesem Computer durch die Tasksequenz abgerufen werden.  

##  <a name="BKMK_EnablingUnknown"></a> Aktivieren der Unterstützung für unbekannte Computer  
 Verwenden Sie die folgenden Angaben, um die Unterstützung für unbekannte Computer zu aktivieren, wenn Sie ein Betriebssystem unter Verwendung von PXE, startbaren Medien und vorab bereitgestellten Medien bereitstellen:  

-   **PXE**  

     Aktivieren Sie bei einem PXE-fähigen Verteilungspunkt auf der Registerkarte **PXE** das Kontrollkästchen **Unterstützung für unbekannte Computer aktivieren** . Weitere Informationen finden Sie unter [Configuring distribution points to accept PXE requests](prepare-site-system-roles-for-operating-system-deployments.md#BKMK_PXEDistributionPoint) (Konfigurieren von Verteilungspunkten zur Annahme von PXE-Anforderungen).  

-   **Startbare Medien**  

     Wählen Sie im Assistenten zum Erstellen von Tasksequenzmedien auf der Seite **Sicherheit** das Kontrollkästchen **Unterstützung für unbekannte Computer aktivieren** . Weitere Informationen finden Sie unter [Configuring distribution points to accept PXE requests](prepare-site-system-roles-for-operating-system-deployments.md#BKMK_PXEDistributionPoint) (Konfigurieren von Verteilungspunkten zur Annahme von PXE-Anforderungen) und [Verwenden von PXE zum Bereitstellen von Windows über das Netzwerk mit System Center Configuration Manager](../deploy-use/use-pxe-to-deploy-windows-over-the-network.md).  

-   **Vorab bereitgestellte Medien**  

     Wählen Sie im Assistenten zum Erstellen von Tasksequenzmedien auf der Seite **Sicherheit** das Kontrollkästchen **Unterstützung für unbekannte Computer aktivieren** . Weitere Informationen finden Sie unter [Create prestaged media with System Center Configuration Manager](../deploy-use/create-prestaged-media.md).  
