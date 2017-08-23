---
title: "Hinzufügen von Updates zu einer Updategruppe – Configuration Manager | Microsoft-Dokumentation"
description: "Manuelles oder Automatisches hinzufügen von Softwareupdates zu einer Softwareupdategruppe in Ihrer Umgebung."
keywords: 
author: dougeby
ms.author: dougeby
manager: angrobe
ms.date: 01/23/2017
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology: configmgr-sum
ms.assetid: a0767664-fd60-46a8-9da5-86cc431ce53c
ms.openlocfilehash: 02e30ba48f3564fa8a31f21793c145054e02e002
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="add-software-updates-to-an-update-group"></a>Hinzufügen von Softwareupdates zu einer Updategruppe  

*Gilt für: System Center Configuration Manager (Current Branch)*

 Mithilfe von Softwareupdategruppen können Sie Softwareupdates in Ihrer Umgebung auf wirksame Weise organisieren. Sie können Softwareupdates einer Softwareupdategruppe manuell hinzufügen. Mit einer automatischen Bereitstellungsregel können Softwareupdates einer Softwareupdategruppe auch automatisch hinzugefügt werden. Eine Softwareupdategruppe wiederum kann entweder manuell oder mithilfe einer automatischen Bereitstellungsregel automatisch bereitgestellt werden. Nach der Bereitstellung einer Softwareupdategruppe können Sie der Gruppe neue Softwareupdates hinzufügen, die von Configuration Manager automatisch bereitgestellt werden. Gehen Sie wie folgt vor, um einer neuen oder bereits vorhandenen Softwareupdategruppe Softwareupdates hinzuzufügen.  

#### <a name="to-add-software-updates-to-a-new-software-update-group"></a>So fügen Sie Softwareupdates einer neuen Softwareupdategruppe hinzu  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Softwarebibliothek**.  

2.  Erweitern Sie im Arbeitsbereich „Softwarebibliothek“ den Eintrag **Softwareupdates**, und klicken Sie auf **Alle Softwareupdates**.  

3.  Wählen Sie die Softwareupdates aus, die der neuen Softwareupdategruppe hinzugefügt werden sollen.  

4.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Update** auf **Softwareupdategruppe erstellen**.  

5.  Geben Sie den Namen und optional eine Beschreibung für die Softwareupdategruppe ein. Achten Sie darauf, dass der Name und die Beschreibung aussagekräftig sind, damit Sie den Typ der einzelnen Softwareupdates in der Softwareupdategruppe schnell ermitteln können. Klicken Sie auf **Erstellen**, um den Vorgang fortzusetzen.  

6.  Klicken Sie auf **Softwareupdategruppe** , um die neue Softwareupdategruppe anzuzeigen.  

7.  Wählen Sie die Softwareupdategruppe aus. Klicken Sie dann auf der Registerkarte **Startseite** in der Gruppe **Update** auf **Mitglieder anzeigen** , um eine Liste der Softwareupdates in der Gruppe anzuzeigen.  

#### <a name="to-add-software-updates-to-an-existing-software-update-group"></a>So fügen Sie Softwareupdates einer vorhandenen Softwareupdategruppe hinzu  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Softwarebibliothek**.  

2.  Erweitern Sie im Arbeitsbereich „Softwarebibliothek“ den Eintrag **Softwareupdates**, und klicken Sie auf **Alle Softwareupdates**.  

3.  Wählen Sie die Softwareupdates aus, die Sie der neuen Softwareupdategruppe hinzufügen möchten.  

    > [!NOTE]  
    >  Im Knoten **Alle Softwareupdates** werden von Configuration Manager standardmäßig nur Softwareupdates angezeigt, die die Klassifizierungen **Kritisch** und **Sicherheit** aufweisen, und in den letzten 30 Tagen veröffentlicht wurden.  

4.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Update** auf **Mitgliedschaft bearbeiten**.  

5.  Wählen Sie die Softwareupdategruppe aus, der Sie die Softwareupdates hinzufügen möchten.  

6.  Klicken Sie auf den Knoten **Softwareupdategruppen** , um die Softwareupdategruppe anzuzeigen.  

7.  Wählen Sie die Softwareupdategruppe aus. Klicken Sie dann auf der Registerkarte **Startseite** in der Gruppe **Update** auf **Mitglieder anzeigen** , um eine Liste der Softwareupdates in der Softwareupdategruppe anzuzeigen.  
