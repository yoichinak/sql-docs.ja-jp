---
description: T-SQL ステートメントの実行タスク
title: T-SQL ステートメントの実行タスク | Microsoft Docs
ms.custom: ''
ms.date: 03/13/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.executetsqlstatementtask.f1
helpviewer_keywords:
- Transact-SQL statements, SSIS
- statements [Integration Services]
- Execute T-SQL Statement task [Integration Services]
ms.assetid: 7e9086ca-d27e-46c0-bfad-d61333ebd55e
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 060fa6ad9faae0fa6159eba2591623af57a41c5b
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/25/2020
ms.locfileid: "96123520"
---
# <a name="execute-t-sql-statement-task"></a>T-SQL ステートメントの実行タスク

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  T-SQL ステートメントの実行タスクは、Transact-SQL ステートメントを実行します。 詳細については、「[Transact-SQL リファレンス (データベース エンジン)](../../t-sql/language-reference.md)」および「[Integration Services (SSIS) のクエリ](../../integration-services/integration-services-ssis-queries.md)」を参照してください。  
  
 このタスクは、SQL 実行タスクと同様です。 ただし、T-SQL ステートメントの実行タスクでは、SQL 言語の Transact-SQL バージョンのみがサポートされるため、このタスクを使用して、SQL 言語の他の仕様の言語によるステートメントをサーバーで実行することはできません。 パラメーター化クエリの実行、クエリ結果の変数への保存、またはプロパティ式の使用が必要な場合は、T-SQL ステートメントの実行タスクではなく、SQL 実行タスクを使用する必要があります。 詳細については、「 [SQL 実行タスク](../../integration-services/control-flow/execute-sql-task.md)」を参照してください。  
  
## <a name="configuration-of-the-execute-t-sql-task"></a>T-SQL 実行タスクの構成  
 プロパティは、 [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーから設定できます。 このタスクは、 **デザイナーの** [ツールボックス] **の** [メンテナンス プランのタスク] [!INCLUDE[ssIS](../../includes/ssis-md.md)] に表示されます。  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーで設定できるプロパティの詳細については、次のトピックを参照してください。  
  
-   [[T-SQL ステートメントの実行タスク] (メンテナンス プラン)](../../relational-databases/maintenance-plans/execute-t-sql-statement-task-maintenance-plan.md)  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーでこれらのプロパティを設定する方法については、次のトピックを参照してください。  
  
-   [タスクまたはコンテナーのプロパティを設定する](./add-or-delete-a-task-or-a-container-in-a-control-flow.md)  
  
## <a name="see-also"></a>参照  
 [Integration Services タスク](../../integration-services/control-flow/integration-services-tasks.md)   
 [制御フロー](../../integration-services/control-flow/control-flow.md)   
 [Integration Services パッケージで MERGE を実行する](../../integration-services/control-flow/merge-in-integration-services-packages.md)  
  
