---
description: catalog.execution_data_statistics
title: catalog.execution_data_statistics | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: 6f51407e-0e4e-4b44-af33-db14c9d40ded
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 24452ceffc1660e57b087395ded3923e47802314
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/25/2020
ms.locfileid: "96129479"
---
# <a name="catalogexecution_data_statistics"></a>catalog.execution_data_statistics 

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  このビューは、特定のパッケージ実行で、データ フロー コンポーネントが下流コンポーネントへデータを送信するたびに 1 行を表示します。 このビューの情報が使用して、コンポーネントのデータ スループットを計算できます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|data_stats_id|**bigint**|データの一意識別子 (ID)。|  
|execution_id|**bigint**|実行のインスタンスの一意の ID。|  
|package_name|**nvarchar(260)**|実行中に開始された最初のパッケージの名前。|  
|task_name|**nvarchar (4000)**|データ フロー タスクの名前。|  
|dataflow_path_id_string|**nvarchar (4000)**|データ フロー パスの識別文字列です。|  
|dataflow_path_name|**nvarchar (4000)**|データ フロー パスの名前。|  
|source_component_name|**nvarchar (4000)**|データを送信したデータ フロー コンポーネントの名前。|  
|destination_component_name|**nvarchar (4000)**|データを受信したデータ フロー コンポーネントの名前。|  
|rows_sent|**bigint**|送信元コンポーネントから送信された行の数。|  
|created_time|**datatimeoffset(7)**|値の取得時刻。|  
|execution_path|**nvarchar(max)**|コンポーネントの実行パス。|  
  
## <a name="remarks"></a>解説  
  
-   コンポーネントから複数の出力がある場合、出力ごとに 1 行追加されます。  
  
-   既定では、実行開始時には、送信される行数に関する情報はログに記録されません。  
  
-   特定のパッケージ実行のこのデータを表示するには、ログ記録レベルを **Verbose** に設定します。 詳細については、「 [SSIS サーバーでのパッケージ実行のログ記録を有効にする](../../integration-services/performance/integration-services-ssis-logging.md#server_logging)」を参照してください。  
  
## <a name="permissions"></a>アクセス許可  
 このビューには、次の権限のいずれかが必要です。  
  
-   実行のインスタンスの READ 権限  
  
-   **ssis_admin** データベース ロールのメンバーシップ  
  
-   **sysadmin** サーバー ロールのメンバーシップ  
  
> [!NOTE]  
>  サーバー上で操作を実行する権限がある場合は、操作に関する情報を表示する権限もあります。 行レベルのセキュリティが適用されるため、表示する権限がある行のみが表示されます。  
  
  
