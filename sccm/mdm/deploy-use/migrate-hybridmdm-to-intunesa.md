---
title: "Faire migrer des utilisateurs et appareils MDM hybrides vers la version autonome d’Intune"
titleSuffix: Configuration Manager
description: "Découvrez comment faire migrer des utilisateurs et appareils MDM hybrides vers Intune sur Azure."
keywords: 
author: dougeby
manager: angrobe
ms.date: 09/12/2017
ms.topic: article
ms.prod: configmgr-hybrid
ms.service: 
ms.technology: 
ms.assetid: 1dd696ce-3e46-4dfa-a76d-592fe0f0320e
ms.openlocfilehash: a6e430248fdeedd310087c9a32c6d69ca1864a09
ms.sourcegitcommit: 986fc2d54f7c5fa965fd4df42f4db4ecce6b79cb
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/17/2017
---
# <a name="migrate-hybrid-mdm-users-and-devices-to-intune-standalone"></a>Faire migrer des utilisateurs et appareils MDM hybrides vers la version autonome d’Intune

*S’applique à : System Center Configuration Manager (Current Branch)*    

Lorsque vous êtes prêt à commencer la migration de la gestion hybride des appareils mobiles (MDM) (Intune intégré à Configuration Manager) vers une expérience cloud uniquement à l’aide d’Intune sur Azure, cet article est fait pour vous. Si vous hésitez encore, consultez [Choisir entre la version autonome de Microsoft Intune et la gestion hybride des appareils mobiles avec System Center Configuration Manager](https://docs.microsoft.com/sccm/mdm/understand/choose-between-standalone-intune-and-hybrid-mobile-device-management). 

Vous pouvez commencer la migration vers la version autonome d’Intune à l’aide d’une approche en plusieurs phases qui vous permet de tester un petit sous-ensemble d’utilisateurs et d’appareils tout en continuant à gérer la plupart de vos utilisateurs et appareils avec la gestion hybride des appareils mobiles. Ensuite, après avoir vérifié la fonctionnalité Intune, vous pouvez commencer la migration des autres utilisateurs vers Intune.    

Les rubriques suivantes indiquent les étapes de la migration des utilisateurs vers la version autonome d’Intune selon une approche progressive.    
  
1.  [Importer les données Configuration Manager dans Microsoft Intune](migrate-import-data.md)   
    L’outil d’importation de données Intune collecte des données sur les objets que vous sélectionnez dans votre hiérarchie Configuration Manager, fournit des détails sur les objets que vous pouvez sélectionner pour l’importation et des informations sur la raison pour laquelle un objet ne peut pas être importé, puis vous permet d’importer les objets sélectionnés dans votre locataire Microsoft Intune. Même si cette étape est facultative, elle peut vous faire gagner beaucoup de temps en automatisant le processus de recréation des objets entre Configuration Manager et Intune. 
2.  [Préparer Intune à la migration des utilisateurs](migrate-prepare-intune.md)    
    Validez les objets importés à partir de Configuration Manager, créez des objets, créez des groupes AAD et affectez des objets à ces groupes, installez les connecteurs NDES et Exchange, etc. Ces étapes et le démarrage de la migration vers la version autonome d’Intune doivent être transparents pour vos utilisateurs.  
3.  [Changer l’autorité MDM pour des utilisateurs spécifiques (autorité MDM mixte)](migrate-mixed-authority.md)    
    Configurez une autorité MDM mixte dans le même locataire en choisissant de gérer certains utilisateurs dans Intune et tous les autres appareils avec la gestion hybride des appareils mobiles (MDM) (Intune intégré à Configuration Manager). Vous pouvez tester si la fonctionnalité Intune se comporte comme prévu sur les appareils d’un petit sous-ensemble d’utilisateurs avant de commencer la migration d’autres utilisateurs. 
4.  [Remplacer l’autorité MDM par la version autonome d’Intune](change-mdm-authority.md)     
    Faites passer votre autorité MDM au niveau du locataire de Configuration Manager à Intune. Tous les utilisateurs et appareils restants migrent vers la version autonome d’Intune. Vous allez modifier votre autorité MDM au niveau du locataire après avoir soigneusement testé la fonctionnalité Intune à l’étape précédente et avoir fait migré la majorité ou la totalité de vos utilisateurs.

<!--
The following provides a typical workflow for migrating users from hybrid MDM to Intune standalone:
1.  Admin runs the Microsoft Intune Data Importer Tool, selecting which objects and assignments to import. Selected objects are imported into Intune standalone.
    1. Some objects cannot be imported because they contain settings the tool does not understand or setting that are not available in Intune standalone.
    2. Assignments are migrated. However, only if the collection an object was targeted to is based on a single Active Directory (AD) security group and the same group exists in Azure Active Directory (AAD).
    > [!Note]    
    > If you want, you can skip this step and create the objects that you want directly in Intune in the Azure portal without running the Intune Data Importer Tool. 
2.  Admin logs into the Intune on Azure portal
    1. Creates any additional objects required for their organization that were not imported by the Microsoft Intune Data Importer tool.
    2. Creates any required AAD groups and makes any additional assignments for each object to AAD groups.
    3. Installs the NDES connector on an on-premises server if using SCEP or PFX certificate deployment.
    4. Installs the Exchange connector on an on-premises server if using conditional access. 
3.  Admin ensures that all existing Intune users in their organization have an Intune license assigned to them using AAD or the Office administrator portal.
4.  Admin selects some test users to migrate to Intune standalone and removes them from the collection associated with the Intune subscription in Configuration Manager.
5.  Once removed from the collection, the user and all devices are managed by Intune in the Azure portal. Remaining users and devices continue to be managed by hybrid mobile device management in Configuration Manager. 
6.  Admin validates that things are working as expected on the device and moves more users to Intune standalone by removing them from the collection associated with the Intune subscription in Configuration Manager.
7.  Once the admin is comfortable with the functionality in Intune standalone, they can move the rest of their users and devices by switching their MDM authority to Intune standalone. This can be done by removing the Intune subscription from SCCM and choosing to change the MDM authority. Tenant level policies will be automatically migrated to Intune standalone, all objects and assignments in Intune standalone will remain, and devices will not be required to re-enroll.
-->