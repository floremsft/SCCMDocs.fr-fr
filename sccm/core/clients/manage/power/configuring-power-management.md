---
title: Konfigurieren der Energieverwaltung | Microsoft-Dokumentation
description: Konfigurieren Sie die Energieverwaltung in System Center Configuration Manager.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 435c923c-ea30-4dce-8afd-48962ed85502
caps.latest.revision: "5"
caps.handback.revision: "0"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: e111ac2545dd9e0b96a50c10246bb75d286a737a
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="configuring-power-management-in-system-center-configuration-manager"></a>Konfigurieren der Energieverwaltung in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Bevor Sie die Energieverwaltung in System Center Configuration Manager verwenden können, müssen Sie die folgenden Konfigurationsschritte ausführen.  

## <a name="enable-and-configure-power-management-client-settings"></a>Aktivieren und Konfigurieren von Clienteinstellungen zur Energieverwaltung  
 Mithilfe dieses Verfahrens werden die Clientstandardeinstellungen für die Energieverwaltung konfiguriert. Es gilt für alle Computer in der Hierarchie. Wenn diese Einstellungen nur auf manche Computer angewendet werden sollen, erstellen Sie eine benutzerdefinierte Geräteclienteinstellung, und weisen Sie diese einer Sammlung mit den Computern zu, auf denen die Energieverwaltung verwendet werden soll. Weitere Informationen zum Erstellen benutzerdefinierter Geräteeinstellungen finden Sie unter [How to configure client settings in System Center Configuration Manager (Konfigurieren von Clienteinstellungen in System Center Configuration Manager)](../../../../core/clients/deploy/configure-client-settings.md).  

#### <a name="to-enable-power-management-and-configure-client-settings"></a>So aktivieren Sie die Energieverwaltung und konfigurieren die Clienteinstellungen  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Verwaltung**.  

2.  Klicken Sie im Arbeitsbereich **Verwaltung** auf **Clienteinstellungen**.  

3.  Klicken Sie auf **Clientstandardeinstellungen**.  

4.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Eigenschaften** auf **Eigenschaften**.  

5.  Klicken Sie im Dialogfeld **Clientstandardeinstellungen** auf **Energieverwaltung**.  

6.  Konfigurieren Sie den folgenden Wert für die Clienteinstellungen zur Energieverwaltung:  

    -   **Energieverwaltung von Geräten zulassen** – Wählen Sie aus der Dropdownliste den Wert **Wahr** aus, um die Energieverwaltung zu aktivieren.  

7.  Konfigurieren Sie die erforderlichen Clienteinstellungen. Eine Liste der Clienteinstellungen zur Energieverwaltung, die Sie konfigurieren können, finden Sie im Abschnitt [Power Management](../../../../core/clients/deploy/about-client-settings.md#power-management) des Themas [About client settings in System Center Configuration Manager (Informationen zu Clienteinstellungen in System Center Configuration Manager)](../../../../core/clients/deploy/about-client-settings.md).  

8.  Klicken Sie auf **OK** , um das Dialogfeld **Clientstandardeinstellungen** zu schließen.  

 Die Clientcomputer werden beim nächsten Clientrichtliniendownload mit diesen Einstellungen konfiguriert. Informationen zum Initiieren des Abrufens von Richtlinien für einen einzelnen Client finden Sie unter [How to manage clients in System Center Configuration Manager](../../../../core/clients/manage/manage-clients.md).  

## <a name="exclude-computers-from-power-management"></a>Ausschließen von Computern aus der Energieverwaltung  
 Sie können verhindern, dass von Computersammlungen Energieverwaltungseinstellungen empfangen werden. Wenn ein Computer Mitglied einer Sammlung ist, die aus den Energieverwaltungseinstellungen ausgeschlossen wurde, werden auf diesen Computer keine Energieverwaltungseinstellungen angewendet. Dies gilt auch, wenn er gleichzeitig Mitglied einer anderen Sammlung ist, auf die Energieverwaltungseinstellungen angewendet werden.  

 Möglicherweise möchten Sie Computer aus folgenden Gründen aus der Energieverwaltung ausschließen:  

-   Aufgrund einer Unternehmensanforderung müssen Computer ständig eingeschaltet sein.  

-   Sie haben eine Kontrollsammlung von Computern erstellt, auf die Sie keine Energieverwaltungseinstellungen anwenden möchten.  

-   Bei einigen Computern ist es nicht möglich, Energieverwaltungseinstellungen anzuwenden.  

-   Sie möchten Computer, auf denen Windows Server ausgeführt wird, aus der Energieverwaltung ausschließen.  

> [!NOTE]  
>  Wenn die Option **Benutzern das Ausschließen ihres Geräts aus der Energieverwaltung gestatten** in den Clienteinstellungen konfiguriert ist, können Benutzer ihre Computer über das Softwarecenter aus der Energieverwaltung ausschließen.  

 Führen Sie den Bericht **Ausgeschlossene Computer**aus, um herauszufinden, welche Computer aus der Energieverwaltung ausgeschlossen wurden. Weitere Informationen zu diesem Bericht finden Sie unter [Computers Excluded (Ausgeschlossene Computer)](../../../../core/clients/manage/power/monitor-and-plan-for-power-management.md#BKMK_Excluded) im Thema [How to Monitor and Plan for Power Management in Configuration Manager (Überwachen und Planen der Energieverwaltung in System Center Configuration Manager)](../../../../core/clients/manage/power/monitor-and-plan-for-power-management.md).  

> [!IMPORTANT]  
>  Energieeinstellungen, die auf Computer mit Windows XP oder Windows Server 2003 angewendet werden, werden auch dann nicht auf ihre ursprünglichen Werte zurückgesetzt, wenn Sie die Computer aus der Energieverwaltung ausschließen. Bei späteren Versionen von Windows bewirkt das Ausschließen eines Computers aus der Energieverwaltung, dass sämtliche Energieeinstellungen auf ihre ursprünglichen Werte zurückgesetzt werden. Es können keine einzelnen Energieeinstellungen auf ihre ursprünglichen Werte zurückgesetzt werden.  

#### <a name="to-exclude-a-collection-of-computers-from-power-management"></a>So schließen Sie eine Computersammlung aus der Energieverwaltung aus  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Bestand und Kompatibilität**.  

2.  Klicken Sie im Arbeitsbereich **Bestand und Kompatibilität** auf **Gerätesammlungen**.  

3.  Wählen Sie in der Liste **Gerätesammlungen** die Sammlung aus, die Sie aus der Energieverwaltung ausschließen möchten. Klicken Sie dann auf der Registerkarte **Startseite** in der Gruppe **Eigenschaften** auf **Eigenschaften**.  

4.  Wählen Sie im Dialogfeld **Eigenschaften** von *Sammlungsname\>* auf der Registerkarte  **Energieverwaltung** die Option **Energieverwaltungseinstellungen nie auf Computer in dieser Sammlung anwenden**.  

5.  Klicken Sie auf **OK**, um das **Dialogfeld** Eigenschaften von *Sammlungsname\>* zu schließen und die Einstellungen zu speichern.  
