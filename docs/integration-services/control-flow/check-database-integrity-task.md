---
description: データベースの整合性確認タスク
title: データベースの整合性確認タスク | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.checkdatabaseintegritytask.f1
helpviewer_keywords:
- data integrity [Integration Services]
- Check Database Integrity task [Integration Services]
- checking database consistency
- database consistency checks [Integration Services]
- verifying database consistency
- integrity checking [Integration Services]
ms.assetid: 5a82fe99-4503-429f-9337-e6bac7649fe4
author: chugugrace
ms.author: chugu
ms.openlocfilehash: af37de7c5192cb0fe2f113205b5569430e507acc
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/25/2020
ms.locfileid: "96123595"
---
# <a name="check-database-integrity-task"></a>データベースの整合性確認タスク

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  データベースの整合性確認タスクは、指定されたデータベース内のすべてのオブジェクトの割り当てと構造上の整合性をチェックします。 このタスクは、単一のデータベースまたは複数のデータベースをチェックできます。また、データベースのインデックスもチェックするかどうかを選択できます。  
  
 データベースの整合性確認タスクは、DBCC CHECKDB ステートメントをカプセル化します。 詳細については、「[DBCC CHECKDB (Transact-SQL)](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md)」を参照してください。  
  
## <a name="configuration-of-the-check-database-integrity-task"></a>データベースの整合性確認タスクの構成  
 プロパティは、 [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーから設定できます。 このタスクは、 **デザイナーの** [ツールボックス] **の** [メンテナンス プランのタスク] [!INCLUDE[ssIS](../../includes/ssis-md.md)] に表示されます。  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーで設定できるプロパティの詳細については、次のトピックを参照してください。  
  
-   [[データベースの整合性確認タスク] (メンテナンス プラン)](../../relational-databases/maintenance-plans/check-database-integrity-task-maintenance-plan.md)  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーでこれらのプロパティを設定する方法については、次のトピックを参照してください。  
  
-   [タスクまたはコンテナーのプロパティを設定する](./add-or-delete-a-task-or-a-container-in-a-control-flow.md)  
  
