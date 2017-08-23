---
title: "Windows-Firewall-Richtlinien für Endpoint Protection | Microsoft-Dokumentation"
description: "Hier erfahren Sie, wie Firewallrichtlinien für Endpoint Protection in System Center 2012 Configuration Manager erstellt und bereitgestellt werden."
ms.custom: na
ms.date: 03/07/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6ecdfad1-6305-45a8-ae75-3f33b967cb8f
caps.latest.revision: "5"
author: NathBarn
ms.author: nathbarn
manager: angrobe
ms.openlocfilehash: acd75a8b22d050970b8c1176f725ddb4445633aa
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="create-and-deploy-windows-firewall-policies-for-endpoint-protection-in-system-center-configuration-manager"></a>Erstellen und Bereitstellen von Windows-Firewall-Richtlinien für Endpoint Protection in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Mithilfe von Firewallrichtlinien für Endpoint Protection in System Center 2012 Configuration Manager können Sie grundlegende Konfigurations- und Wartungstasks an der Windows-Firewall auf Clientcomputern in der Hierarchie ausführen. Über die Windows-Firewall-Richtlinien können Sie die folgenden Tasks ausführen:  

-   Steuern, ob die Windows-Firewall aktiviert oder deaktiviert ist  

-   Steuern, ob eingehende Verbindungen auf Clientcomputern zulässig sind  

-   Steuern, ob Benutzer benachrichtigt werden, wenn von der Windows-Firewall ein neues Programm blockiert wird  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Bestand und Kompatibilität**.  

2.  Erweitern Sie im Arbeitsbereich **Bestand und Kompatibilität** den Knoten **Endpoint Protection**, und klicken Sie anschließend auf **Windows-Firewall-Richtlinien**.  

3.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Erstellen** auf **Windows-Firewall-Richtlinie erstellen**.  

4.  Geben Sie auf der Seite **Allgemein** unter **Assistent zum Erstellen von Windows-Firewall-Richtlinien**einen Namen und optional eine Beschreibung für diese Firewallrichtlinie ein, und klicken Sie dann auf **Weiter**.  

5.  Konfigurieren Sie auf der Seite **Profileinstellungen** des Assistenten die folgenden Einstellungen für jedes Netzwerkprofil:  

    > [!IMPORTANT]  
    >  Wenn Sie Windows-Firewall-Richtlinien auf Computern bereitstellen möchten, auf denen Windows Server 2008 und Windows Vista Service Pack 1 ausgeführt werden, müssen Sie auf diesen Computern zuvor den [Hotfix KB971800](http://go.microsoft.com/fwlink/p/?LinkId=231239) installieren.  

    > [!NOTE]  
    >  Weitere Informationen zu Netzwerkprofilen finden Sie in der Windows-Dokumentation.  

    -   **Windows-Firewall aktivieren**  

        > [!NOTE]  
        >  Wenn **Windows-Firewall aktivieren** nicht aktiviert ist, sind die weiteren Einstellungen auf dieser Seite des Assistenten nicht verfügbar.  

    -   **Alle eingehenden Verbindungen blockieren, einschließlich der in der Liste der zugelassenen Programme**  

    -   **Benutzer benachrichtigen, wenn ein neues Programm von der Windows-Firewall blockiert wird**  

6.  Überprüfen Sie auf der Seite **Zusammenfassung** des Assistenten die durchzuführenden Aktionen, und schließen Sie dann den Assistenten ab.  

7.  Überprüfen Sie, ob die neue Windows-Firewall-Richtlinie in der Liste **Windows-Firewall-Richtlinien** angezeigt wird.  

##  <a name="BKMK_Assign"></a> So stellen Sie eine Windows-Firewall-Richtlinie bereit  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Bestand und Kompatibilität**.  

2.  Erweitern Sie im Arbeitsbereich **Bestand und Kompatibilität** den Knoten **Endpoint Protection**, und klicken Sie anschließend auf **Windows-Firewall-Richtlinien**.  

3.  Wählen Sie aus der Liste **Windows-Firewall-Richtlinien** die Windows-Firewall-Richtlinie aus, die Sie bereitstellen möchten.  

4.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Bereitstellung** auf **Bereitstellen**.  

5.  Geben Sie im Dialogfeld **Windows-Firewall-Richtlinie bereitstellen** die Sammlung an, der Sie diese Windows-Firewall-Richtlinie zuweisen möchten, und legen Sie einen Zuweisungszeitplan fest. Die Windows-Firewall-Richtlinie wird mithilfe dieses Zeitplans auf Kompatibilität bewertet, und die Windows-Firewall-Einstellungen auf den Clients werden neu konfiguriert, damit sie mit der Windows-Firewall-Richtlinie übereinstimmen.  

6.  Klicken Sie auf **OK** , um das Dialogfeld **Windows-Firewall-Richtlinie bereitstellen** zu schließen und die Windows-Firewall-Richtlinie bereitzustellen.  

    > [!IMPORTANT]  
    >  Wenn Sie eine Windows-Firewall-Richtlinie auf einer Sammlung bereitstellen, wird diese Richtlinie auf den Computern in zufälliger Reihenfolge über einen Zeitraum von 2 Stunden angewendet, um ein Überfluten des Netzwerks zu verhindern.
