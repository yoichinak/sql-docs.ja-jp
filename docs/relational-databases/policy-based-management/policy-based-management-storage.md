---
description: ポリシー ベースの管理のストレージ
title: ポリシー ベースの管理のストレージ | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Policy-Based Management, storage
ms.assetid: d0cbf214-fc2e-4917-8d31-1d71c9ffa61d
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: fed38dee8c9b8d242ea223c8c0d0576959a2e83d
ms.sourcegitcommit: f30b5f61c514437ea58acc5769359c33255b85b5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/29/2021
ms.locfileid: "99076494"
---
# <a name="policy-based-management-storage"></a>ポリシー ベースの管理のストレージ
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  ポリシーは msdb データベースに格納されます。 ポリシーまたは条件を変更した後、msdb をバックアップする必要があります。 詳細については、「[システム データベースのバックアップと復元 &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-and-restore-of-system-databases-sql-server.md)」を参照してください。  
  
## <a name="storing-policies"></a>ポリシーの保存  
 [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] には、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンスの監視に使用できるポリシーが用意されています。 これらのポリシーは、[!INCLUDE[ssDE](../../includes/ssde-md.md)]に既定でインストールされませんが、既定のインストール場所である C:\Program Files (x86)\Microsoft SQL Server\140\Tools\Policies\DatabaseEngine\1033 からインポートできます。  
  
 ポリシーを直接作成するには、 **[ファイル] メニューの [新規作成]** を使用して、ポリシーをファイルに保存します。 これにより、 [!INCLUDE[ssDE](../../includes/ssde-md.md)]インスタンスに接続していないときにポリシーを作成できます。  
  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)] の現在のインスタンスで評価されたポリシーのポリシー履歴は、msdb システム テーブルに格納されます。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] のその他のインスタンスに適用されたポリシーまたは [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] や [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] に適用されたポリシーのポリシー履歴は保持されません。  
  
  
