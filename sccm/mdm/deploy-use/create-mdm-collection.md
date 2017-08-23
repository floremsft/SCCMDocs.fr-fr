---
title: Erstellen einer MDM-Sammlung unter Verwendung von System Center Configuration Manager | Microsoft-Dokumentation
description: Erstellen einer MDM-Sammlung unter Verwendung von System Center Configuration Manager.
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d1b4337f-85e8-45e6-8bbe-9f18b49041c7
caps.latest.revision: "18"
caps.handback.revision: "0"
author: mtillman
ms.author: mtillman
manager: angrobe
ms.openlocfilehash: fabbcfd2d5656d4fa8cb87feffe87e17998df145
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="create-an-mdm-collection-with-system-center-configuration-manager-and-microsoft-intune"></a>Erstellen einer MDM-Sammlung mit System Center Configuration Manager und Microsoft Intune

*Gilt für: System Center Configuration Manager (Current Branch)*

Zum Angeben der Benutzer, die Geräte in der Verwaltung registrieren können, ist eine Configuration Manager-Benutzersammlung erforderlich. Es können nur Benutzersammlungen (keine Gerätesammlungen) verwendet werden, da Intune-Lizenzen nach Benutzer zugewiesen werden.

> [!NOTE]
> Zum Registrieren von Geräten mit Intune ist es nicht erforderlich, im Office 365-Portal oder im Azure Active Directory-Portal Benutzern Lizenzen zuzuweisen. Sie müssen lediglich die Benutzer in eine Sammlung einbinden, die (in einem [späteren Schritt](configure-intune-subscription.md)) dem Intune-Abonnement zugeordnet wird.

Sie können zu Testzwecken eine **Direktregel** einrichten und bestimmte Benutzer hinzufügen, die Geräte registrieren können. Wählen Sie an der Configuration Manager-Konsole **Bestand und Kompatibilität** > **Benutzersammlungen** aus, und klicken Sie auf die Registerkarte **Startseite** > Gruppe **Erstellen** und dann auf **Benutzersammlung erstellen**. Verwenden Sie für eine größer angelegte Verteilung **Abfrageregeln**, um Benutzer zu definieren. Weitere Informationen zu Sammlungen finden Sie unter [Erstellen von Sammlungen](https://technet.microsoft.com/library/mt629371.aspx).

![Erstellen einer Benutzersammlung für MDM](../media/mdm-create-user-collection.png)

> [!div class="button"]
[Nächster Schritt >](confirm-dns.md)
