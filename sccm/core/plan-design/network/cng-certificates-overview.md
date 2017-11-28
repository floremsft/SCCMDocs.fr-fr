---
title: "Vue d’ensemble des certificats CNG"
titleSuffix: Configuration Manager
description: "Vue d’ensemble des certificats CNG dans Configuration Manager"
ms.custom: na
ms.date: 11/20/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 
author: vhorne
ms.author: victorh
manager: angrobe
ms.openlocfilehash: f5f5138270d4f14b76b2c41e41ec034a0c12a932
ms.sourcegitcommit: 12d0d53e47bbf1a0bbd85015b8404a44589d1e14
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/21/2017
---
# <a name="cng-certificates-overview"></a>Vue d’ensemble des certificats CNG
<!-- 1356191 --> 

Configuration Manager prend en charge les certificats Cryptography : Next Generation (CNG) de manière limitée. Les clients Configuration Manager peuvent utiliser un certificat d’authentification client PKI avec une clé privée dans le fournisseur de stockage de clés (KSP) CNG. La prise en charge du KSP permet aux clients Configuration Manager de prendre en charge une clé privée matérielle, comme TPM KSP pour les certificats d’authentification client PKI.

## <a name="supported-scenarios"></a>Scénarios pris en charge
Vous pouvez utiliser les modèles de certificat [Cryptography API : Next Generation (CNG)](https://msdn.microsoft.com/library/windows/desktop/bb204775.aspx) pour les scénarios suivants :

- L’inscription du client et la communication avec un point de gestion HTTPS.   
- La distribution de logiciels et le déploiement d’applications avec un point de distribution HTTPS.   
- Le déploiement de système d'exploitation.  
- Le Kit SDK de messagerie du client (avec la dernière mise à jour) et proxy ISV.   
- La configuration de passerelle de gestion cloud.  

> [!NOTE]
> CNG offre une compatibilité descendante avec Crypto API (CAPI). Les certificats CAPI continuent à être pris en charge même lorsque la prise en charge CNG est activée sur le client.

## <a name="unsupported-scenarios"></a>Scénarios non pris en charge

Les scénarios suivants ne sont pas actuellement pris en charge :

- Les rôles de service web du catalogue d’applications, de site web du catalogue d’applications, de point d’inscription et de point proxy d’inscription ne fonctionnent pas quand ils sont installés en mode HTTPS avec un certificat CNG lié au site web dans Internet Information Services (IIS). Le Centre logiciel n’affiche pas les applications et packages disponibles qui sont déployés sur des regroupements d’utilisateurs ou de groupes d’utilisateurs.

- Le point de migration d’état ne fonctionne pas quand il est installé en mode HTTPS avec un certificat CNG lié au site web dans IIS.

- Utilisation de certificats CNG pour créer un point de distribution cloud.

- La communication entre NDES Policy Module et le point d’enregistrement de certificat échoue si NDES Policy Module utilise un certificat CNG pour le certificat d’authentification client.

- La création d’un média de séquence de tâches ne parvient pas à créer un média de démarrage si un certificat CNG est spécifié.

## <a name="to-use-cng-certificates"></a>Pour utiliser des certificats CNG

Pour utiliser des certificats CNG, votre autorité de certification (CA) doit fournir des modèles de certificat CNG pour les machines cibles. Bien que les détails du modèle varient selon le scénario, les propriétés suivantes sont requises :

- Onglet **Compatibilité**

    - L’**autorité de certification** doit être Windows Server 2008 ou version ultérieure. (Windows Server 2012 recommandé)

    - Le **destinataire du certificat** doit être Windows Vista/Server 2008 ou version ultérieure. (Windows 8/Windows Server 2012 recommandé)

- Onglet **Chiffrement**

    - La **catégorie de fournisseur** doit être **Fournisseur de stockage de clés**. (obligatoire)

> [!NOTE]
> La configuration requise pour votre environnement ou votre organisation peut être différente. Contactez votre expert PKI. Le point important à ne pas négliger est qu’un modèle de certificat doit utiliser un fournisseur de stockage de clés pour tirer parti de CNG.

Pour de meilleurs résultats, nous vous recommandons de créer le nom du sujet à partir des informations Active Directory. Utilisez le nom DNS pour le **format du nom du sujet** et incluez le nom DNS dans le nom de substitution du sujet. Dans le cas contraire, vous devez fournir ces informations au moment de l’inscription de l’appareil dans le profil de certificat.