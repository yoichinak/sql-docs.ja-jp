---
description: snapshots.fn_trace_getdata (Transact-SQL)
title: snapshots.fn_trace_getdata (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: reference
f1_keywords:
- snapshots.fn_trace_getdata
dev_langs:
- TSQL
helpviewer_keywords:
- snapshots.fn_trace_getdata function
ms.assetid: ac28ef48-f4f4-4bf2-ba22-d44e1be88172
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.openlocfilehash: 5ce872efff2eff679d02c56985783fd2d70b2082
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99194500"
---
# <a name="snapshotsfn_trace_getdata-transact-sql"></a>snapshots.fn_trace_getdata (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  この関数は、指定されたトレースに対してキャプチャされたすべてのイベントを返します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
snapshots.fn_trace_gettable ( trace_info_id, start_time, end_time )  
```  
  
## <a name="arguments"></a>引数  
 *trace_info_id*  
 管理データウェアハウスデータベースの snapshots.trace_info テーブルの主キーの一意の識別子。 *trace_info_id* は **int** です。  
  
 *start_time*  
 トレースが開始された時刻。 *start_time* は **datetime** です。  
  
 *end_time*  
 トレースが終了した時刻。 *end_time* は **datetime** です。  
  
## <a name="table-returned"></a>返されるテーブル  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|\<All trace columns>|\<Varies>|管理データ ウェアハウス データベースの snapshots.trace_data テーブルからのトレース データ。<br /><br /> 次のクエリを使用して、指定したトレースの列の一覧を取得できます。<br /><br /> `SELECT * FROM sys.trace_columns`<br /><br /> **注:** Snapshots.fn_trace_gettable 関数によって返される列は、sys.trace_columns システムビューの [名前] 列の値に対応します。 この関数から GroupID 列が返されない点のみが異なります。|  
  
## <a name="permissions"></a>アクセス許可  
 mdw_reader に対する SELECT 権限が必要です。  
  
## <a name="see-also"></a>参照  
 [[データ コレクション]](../../relational-databases/data-collection/data-collection.md)  
  
  
