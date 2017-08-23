---
title: "Verknüpfen von Benutzern und Geräten mit Affinität zwischen Benutzer und Gerät | Microsoft-Dokumentation"
description: "Verknüpfen Sie Benutzer und Geräte mit Affinität zwischen Benutzer und Gerät, und stellen Sie Apps automatisch auf Geräten bereit, die einem Benutzer zugeordnet sind."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5b30b0d5-722d-4d4b-9ed7-5a43de315461
caps.latest.revision: "7"
caps.handback.revision: "0"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 4e8e677851ad9ae7d027ab685e842a8ff5e35573
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="link-users-and-devices-with-user-device-affinity-in-system-center-configuration-manager"></a>Verknüpfen von Benutzern und Geräten mit Affinität zwischen Benutzer und Gerät in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Durch die Affinität zwischen Benutzer und Gerät in System Center Configuration Manager (Configuration Manager) wird ein Benutzer einem oder mehreren Geräten zugeordnet. Dadurch ist es zum Bereitstellen einer Anwendung für den Benutzer nicht erforderlich, die Namen seiner Geräte zu kennen. Anstatt die Anwendung für jedes einzelne Gerät eines Benutzers bereitzustellen, stellen Sie sie für den Benutzer bereit. Mithilfe der Affinität zwischen Benutzer und Gerät wird dann automatisch sichergestellt, dass die Anwendung auf allen Geräten installiert wird, die dem Benutzer zugeordnet sind.  

 Sie können primäre Geräte definieren, wobei es sich in der Regel um solche Geräte handelt, die Benutzer täglich für die Ausführung ihrer Arbeit verwenden. Durch das Erstellen einer Affinität zwischen einem Benutzer und einem Gerät bieten sich zusätzliche Optionen für die Bereitstellung von Apps. Wenn ein Benutzer beispielsweise Microsoft Visio benötigt, können Sie es mithilfe einer Windows Installer-Bereitstellung auf dem primären Gerät des Benutzers installieren. Auf Geräten, bei denen es sich nicht um ein primäres Gerät handelt, können Sie Visio dagegen als virtuelle Anwendung bereitstellen. Sie können mithilfe der Affinität zwischen Benutzer und Gerät Software auf dem Gerät eines Benutzers auch vorab bereitstellen, während der Benutzer nicht angemeldet ist. Wenn sich der Benutzer dann anmeldet, ist die Anwendung bereits installiert und betriebsbereit.  

 Sie müssen die Informationen zur Affinität zwischen Benutzer und Gerät für Computer verwalten. Die Affinitäten zwischen Benutzern und Geräten werden von Configuration Manager bei den von ihm angemeldeten mobilen Geräten automatisch verwaltet.  

## <a name="manually-set-up-user-device-affinity"></a>Manuelles Einrichten der Affinität zwischen Benutzer und Gerät  

1.  Wählen Sie in der Configuration Manager-Konsole **Bestand und Konformität** > **Geräte** aus.  

3.  Wählen Sie in der Liste ein Gerät aus. Wählen Sie auf der Registerkarte **Startseite** in der Gruppe **Gerät** dann **Primäre Benutzer bearbeiten** aus.  

4.  Wählen Sie im Dialogfeld **Primäre Benutzer bearbeiten** die Benutzer aus, die dem ausgewählten Gerät als primäre Benutzer hinzugefügt werden sollen. Wählen Sie dann **Hinzufügen** aus.  

    > [!NOTE]  
    > In der Liste **Primäre Benutzer** sind Benutzer, die bereits primäre Benutzer dieses Geräts sind, mit der jeweils zum Zuweisen der Beziehung zwischen Benutzer und Gerät verwendeten Methode aufgelistet.  

## <a name="set-up-primary-devices-for-a-user"></a>Einrichten primärer Geräte für einen Benutzer  

1.  Wählen Sie in der Configuration Manager-Konsole **Bestand und Konformität** > **Benutzer** aus.  

3.  Wählen Sie in der Liste einen Benutzer aus. Wählen Sie auf der Registerkarte **Gerät** dann **Primäre Geräte bearbeiten** aus.  

4.  Wählen Sie im Dialogfeld **Primäre Geräte bearbeiten** die Geräte aus, die dem ausgewählten Benutzer als primäre Geräte hinzugefügt werden sollen. Wählen Sie dann **Hinzufügen** aus.  

    > [!NOTE]  
    > In der Liste **Primäre Geräte** sind Geräte, die bereits als primäre Geräte für diesen Benutzer eingerichtet sind, mit der jeweils zum Zuweisen der Beziehung zwischen Benutzer und Gerät verwendeten Methode aufgelistet.  

## <a name="automatically-create-user-device-affinities-windows-pcs-only"></a>Automatisches Erstellen von Affinitäten zwischen Benutzern und Geräten (nur Windows-PCs)  
 Von Configuration Manager werden Daten zu Benutzeranmeldungen aus dem Windows-Ereignisprotokoll ausgelesen. Zum Nutzen der automatischen Erstellung von Affinitäten zwischen Benutzer und Gerät müssen Sie die folgenden beiden Einstellungen in der lokalen Sicherheitsrichtlinie auf Clientcomputern aktivieren, damit Anmeldeereignisse im Windows-Ereignisprotokoll gespeichert werden:  

-   **Anmeldeversuche überwachen**  
-   **Anmeldeereignisse überwachen**  

 Sie können diese Einstellungen mithilfe von Windows-Gruppenrichtlinien konfigurieren.  

> [!IMPORTANT]  
> Wenn ein Fehler bewirkt, dass im Windows-Ereignisprotokoll eine große Zahl von Einträgen generiert wird, kann dies dazu führen, dass ein neues Ereignisprotokoll erstellt wird. In diesem Fall sind vorhandene Anmeldeereignisse für Configuration Manager möglicherweise nicht mehr verfügbar.  
>   
> Gehen Sie beim Aktivieren der Einstellungen **Audit account logon events** (Anmeldeversuche überwachen) und **Audit logon events** (Anmeldeereignisse überwachen) in Windows XP vorsichtig vor. Standardmäßig ist die Beibehaltungsrichtlinie auf sieben Tage festgelegt, und es ist äußerst wahrscheinlich, dass die betreffenden Ereignisse das Sicherheitsereignisprotokoll innerhalb dieses Zeitraums füllen. Standardbenutzer können sich nicht mehr anmelden, wenn das Ereignisprotokoll voll ist. Um dieses Problem zu verhindern, sollten Sie auch den Wert der Richtlinie **Retention Method** (Aufbewahrungsmethode) für das Sicherheitsereignisprotokoll auf **Overwrite events as needed** (Ereignisse bei Bedarf überschreiben) festlegen. Sollen ausreichend Daten für die Affinität zwischen Benutzer und Gerät zur Verfügung stehen, legen Sie die Richtlinie „Maximale Größe des Sicherheitsereignisprotokolls“ auf einen Wert wie z.B. 5 bis 20 MB fest.  

### <a name="set-up-the-site-to-automatically-create-user-device-affinities"></a>Einrichten des Standorts für das automatische Erstellen von Affinitäten zwischen Benutzer und Gerät  

1.  Wählen Sie in der Configuration Manager-Konsole **Verwaltung** > **Clienteinstellungen** aus.  

2.  Wählen Sie zum Ändern der Clientstandardeinstellungen **Clientstandardeinstellungen** und anschließend auf der Registerkarte **Startseite** in der Gruppe **Eigenschaften** **Eigenschaften** aus. Wählen Sie zum Erstellen von benutzerdefinierten Client-Agent-Einstellungen den Knoten **Clienteinstellungen**, und anschließend auf der Registerkarte **Startseite** in der Gruppe **Erstellen** **Benutzerdefinierte Geräteclienteinstellungen erstellen** aus.  

    > [!NOTE]  
    > Wenn Sie die Clientstandardeinstellungen ändern, werden sie auf allen Computern in der Hierarchie bereitgestellt. Weitere Informationen zum Konfigurieren von Clienteinstellungen finden Sie unter [Konfigurieren von Clienteinstellungen in System Center Configuration Manager](../../core/clients/deploy/configure-client-settings.md).  

3.  Legen Sie für **Affinität zwischen Benutzer und Gerät** Folgendes fest:  

    -   **User device affinity threshold (minutes)** (Schwellenwert (Minuten) für Affinität zwischen Benutzer und Gerät). Legen Sie die Anzahl von Minuten der Gerätenutzung fest, bevor eine Affinität zwischen Benutzer und Gerät erstellt wird.  

    -   **User device affinity threshold (days)** (Schwellenwert (Tage) für Affinität zwischen Benutzer und Gerät). Geben Sie die Anzahl von Tagen an, über die der Schwellenwert für die Affinität zwischen Benutzer und Gerät gemessen wird.  

    -   **Affinität zwischen Benutzer und Gerät automatisch aus Verwendungsdaten konfigurieren**. Damit der Standort automatisch Affinität zwischen Benutzer und Gerät erstellen kann, wählen Sie in der Dropdownliste **Wahr** aus. Wenn Sie **Falsch**auswählen, müssen Sie alle Zuweisungen der Affinität zwischen Benutzer und Gerät genehmigen.  

    > [!TIP]  
    > **Beispiel:** Wenn Sie für **User device affinity threshold (minutes)** (Nutzungsschwellenwert (Minuten) für Affinität zwischen Benutzer und Gerät) einen Wert von **60** Minuten und für **User device affinity threshold (days)** (Nutzungsschwellenwert (Tage) für Affinität zwischen Benutzer und Gerät) einen Wert von **5** Tagen angeben, muss der Benutzer das Gerät über einen Zeitraum von 5 Tagen insgesamt mindestens 60 Minuten lang nutzen, damit eine Affinität zwischen Benutzer und Gerät automatisch erstellt wird.  

Nachdem eine Affinität zwischen Benutzer und Gerät automatisch erstellt wurde, werden die Schwellenwerte für die Affinität zwischen Benutzer und Gerät weiterhin von Configuration Manager überwacht. Wenn die Aktivität des Benutzers auf dem Gerät die festgelegten Schwellenwerte unterschreitet, wird die Affinität zwischen Benutzer und Gerät entfernt. Legen Sie für **User device affinity threshold (days)** (Nutzungsschwellenwert (Tage) für Affinität zwischen Benutzer und Gerät) einen Wert von mindestens **7** Tagen fest, um zu verhindern, dass eine automatisch konfigurierte Affinität zwischen Benutzer und Gerät verlorengeht, wenn der Benutzer sich über einen längeren Zeitraum (z.B. während des Wochenendes) nicht anmeldet.  

## <a name="import-user-device-affinities-from-a-file"></a>Importieren von Affinitäten zwischen Benutzer und Gerät aus einer Datei  
 Sie können eine Datei importieren, die Affinitäten zwischen Benutzern und Geräten enthält, um viele Beziehungen gleichzeitig zu erstellen. Für dieses Verfahren müssen die entsprechenden Geräte bereits ermittelt worden und in der Configuration Manager-Datenbank als Ressourcen vorhanden sein, da andernfalls ein Fehler auftritt.  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Bestand und Konformität** > **Benutzer** oder **Geräte**.  

2.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Erstellen** auf **Affinität zwischen Benutzer und Gerät importieren**.  

3.  Geben Sie im Assistenten zum Importieren von Affinität zwischen Benutzer und Gerät auf der Seite **Zuordnung wählen** die folgenden Informationen an:  

    -   **Dateiname**. Geben Sie eine CSV-Datei (kommagetrennte Werte) an, die eine Liste mit Benutzern und Geräten enthält, zwischen denen eine Affinität erstellt werden soll. In der Datei muss jedes Paar aus Benutzer und Gerät in einer separaten Zeile stehen, und die Werte müssen durch ein Komma getrennt sein. Verwenden Sie folgendes Format: <*Domäne*>&#92;<*Benutzername*>,<*NetBIOS-Name des Geräts*>.  

    -   **Diese Datei enthält zu Referenzzwecken Spaltenüberschriften**. Wenn die CSV-Datei eine Zeile mit einer Überschrift enthält, wählen Sie diese Option aus, damit die Kopfzeile beim Importieren ignoriert wird.  

4.  Wenn die zu importierende Datei mehr als zwei Elemente pro Zeile enthält, können Sie mithilfe der Optionen **Spalte** und **Zuweisen** angeben, welche Spalten Benutzer und Geräte enthalten und welche Spalten beim Importieren ignoriert werden sollen.  

5.  Wählen Sie **Weiter** aus, und schließen Sie dann den Assistenten zum Importieren von Affinität zwischen Benutzer und Gerät ab.  

## <a name="let-users-create-their-own-device-affinities"></a>Benutzern ermöglichen, eigene Geräteaffinitäten zu erstellen  
 Mithilfe der folgenden Verfahren können Sie es Benutzern ermöglichen, eigene Affinitäten zwischen Benutzer und Gerät über die Softwarecenter-App zu erstellen.  

### <a name="set-up-the-site-to-allow-user-created-user-device-affinity-requests"></a>Einrichten des Standorts, um von Benutzern erstellte Affinitätsanforderungen zwischen Benutzer und Gerät zu gestatten  

1.  Wählen Sie in der Configuration Manager-Konsole **Verwaltung** > **Clienteinstellungen** aus.  

2.  Wählen Sie zum Ändern der Clientstandardeinstellungen **Clientstandardeinstellungen** und anschließend auf der Registerkarte **Startseite** in der Gruppe **Eigenschaften** **Eigenschaften** aus. Zum Erstellen von benutzerdefinierten Client-Agent-Einstellungen wählen Sie den Knoten **Clienteinstellungen** und anschließend auf der Registerkarte **Startseite** in der Gruppe **Erstellen** **Benutzerdefinierte Benutzerclienteinstellungen erstellen** aus.  

    > [!NOTE]  
    > Wenn Sie die Clientstandardeinstellungen ändern, werden sie auf allen Computern in der Hierarchie bereitgestellt. Informationen zum Konfigurieren der Clienteinstellungen finden Sie unter [Konfigurieren von Clienteinstellungen in Configuration Manager](../../core/clients/deploy/configure-client-settings.md).  

3.  Wählen Sie die Clienteinstellung **Affinität zwischen Benutzer und Gerät** und dann aus der Dropdownliste **Benutzer das Festlegen primärer Geräte gestatten** den Wert **True**aus.  

### <a name="set-up-a-user-device-affinity"></a>Einrichten einer Affinität zwischen Benutzer und Gerät  

1.  Wählen Sie im Anwendungskatalog **My Systems** (Eigene Systeme) aus.  

2.  Wählen Sie die Option **Ich nutze diesen Computer regelmäßig für meine Arbeit** aus.  

## <a name="manage-user-device-affinity-requests-from-users"></a>Verwalten von Affinitätsanforderungen zwischen Benutzer und Gerät  
 Wenn die Clienteinstellung **Affinität zwischen Benutzer und Gerät automatisch aus Verwendungsdaten konfigurieren** auf den Wert **Falsch**festgelegt ist, müssen Sie alle Affinitätszuweisungen zwischen Benutzern und Geräten genehmigen.  

### <a name="approve-or-reject-a-user-device-affinity-request"></a>Genehmigen oder Ablehnen einer Affinitätsanforderung zwischen Benutzer und Gerät  

1.  Wählen Sie in der Configuration Manager-Konsole **Bestand und Kompatibilität** aus.  

2.  Wählen Sie im Arbeitsbereich **Bestand und Kompatibilität** die Benutzer- oder Gerätesammlung aus, für die Sie Affinitätsanforderungen verwalten möchten.  

3.  Wählen Sie auf der Registerkarte **Startseite** in der Gruppe **Sammlung** **Affinitätsanforderungen verwalten** aus.  

4.  Wählen Sie im Dialogfeld **Affinitätsanforderungen zwischen Benutzer und Gerät verwalten** eine Affinitätsanforderungen und anschließend **Genehmigen** oder **Ablehnen** aus.  
