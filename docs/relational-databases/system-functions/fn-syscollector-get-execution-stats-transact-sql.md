---
description: fn_syscollector_get_execution_stats (Transact-sql)
title: fn_syscollector_get_execution_stats (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: reference
f1_keywords:
- fn_syscollector_get_execution_stats
- fn_syscollector_get_execution_stats_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- fn_syscollector_get_execution_stats function
ms.assetid: 793ad72c-a992-4a8d-8584-bcb6b3b476f1
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.openlocfilehash: 940b154df600b36aab5533a0b6c986d8a3e5988d
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99196100"
---
# <a name="fn_syscollector_get_execution_stats-transact-sql"></a>fn_syscollector_get_execution_stats (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  コレクション セットまたはパッケージに関する詳細な統計 (パッケージのデータ フロー タスクによってログ記録されたエラー行の数を含む) を返します。 データフロータスクは、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] データを処理するコンポーネントです。 このデータはリレーショナル形式のため、行で構成される入力データセットと出力データセットが含まれます。  
  
 統計は、syscollector_execution_stats ビューのエントリから計算されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
fn_syscollector_get_execution_stats ( log_id )  
```  
  
## <a name="arguments"></a>引数  
 *log_id*  
 実行ログの一意なローカル識別子を指定します。 *log_id* は **int** です。  
  
## <a name="table-returned"></a>返されるテーブル  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|avg_row_count_in|**int**|パッケージのデータ フロー タスクが開始された行の平均数です。<br /><br /> 注: データフロータスクは、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] データを処理するコンポーネントです。 このデータはリレーショナル形式であるため、行で構成される入力データセットを持ちます。 これは、タスクに入力された行の数です。 データが変換されると、行で構成される結果セットとして出力されます。 データ フロー タスクでは、データを変換して行で構成される結果セットを出力します。 この出力はタスクが終了した行数です。|  
|min_row_count_in|**int**|パッケージのデータフロータスクに入力された行の最小数。|  
|max_row_count_in|**int**|パッケージのデータフロータスクに入力された行の最大数。|  
|avg_row_count_out|**int**|パッケージのデータ フロー タスクが終了した行の平均数です。|  
|min_row_count_out|**int**|パッケージのデータフロータスクを終了した行の最小数。|  
|max_row_count_out|**int**|パッケージのデータフロータスクを終了した行の最大数。|  
|avg_duration|**int**|パッケージのデータフローコンポーネントで費やされた平均時間 (ミリ秒単位)。|  
|min_duration|**int**|パッケージのデータフローコンポーネントで費やされた最小時間 (ミリ秒単位)。|  
|max_duration|**int**|パッケージのデータフローコンポーネントで費やされた最大時間 (ミリ秒単位)。|  
  
## <a name="permissions"></a>アクセス許可  
 **Dc_operator** に SELECT が必要です。  
  
## <a name="see-also"></a>参照  
 [syscollector_execution_stats &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/syscollector-execution-stats-transact-sql.md)   
 [[データ コレクション]](../../relational-databases/data-collection/data-collection.md)  
  
  
