---
description: DBCC SHOWRESULTCACHESPACEUSED (Transact-SQL)
title: DBCC SHOWRESULTCACHESPACEUSED (Transact-SQL)
ms.custom: ''
ms.date: 07/03/2019
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 73f598cf-b02a-4dba-8d89-9fc0b55a12b8
author: XiaoyuMSFT
ms.author: xiaoyul
monikerRange: = azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: 3bf7994b1b7091bb95800ab1d8e3034f4bafef76
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/14/2020
ms.locfileid: "92037745"
---
# <a name="dbcc-showresultcachespaceused-transact-sql"></a>DBCC SHOWRESULTCACHESPACEUSED (Transact-SQL)

[!INCLUDE [asa](../../includes/applies-to-version/asa.md)]

Azure [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] データベースの記憶域スペースで使用されている結果セットのキャッシュが表示されます。
  
![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則 &#40;Transact-SQL&#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>構文  
  
```syntaxsql
DBCC SHOWRESULTCACHESPACEUSED  
[;]  
```  

[!INCLUDE[synapse-analytics-od-unsupported-syntax](../../includes/synapse-analytics-od-unsupported-syntax.md)]

## <a name="remarks"></a>解説

`DBCC SHOWRESULTCACHESPACEUSED` コマンドは、パラメーターがなく、このコマンドを実行したデータベースで使用されるスペースが返されます。

## <a name="permissions"></a>アクセス許可

VIEW SERVER STATE 権限が必要です。
  
## <a name="result-sets"></a>結果セット  
  
|列|データ型|説明|  
|------------|---------------|-----------------|  
|reserved_space|bigint|データベースに使用されている合計領域 (KB 単位)。 この数値は、キャッシュされた結果セットの増加に応じて変化します。|  
|data_space|bigint|データに使用されている領域 (KB 単位)。|  
|index_space|bigint|インデックスに使用されている領域 (KB 単位)。|  
|unused_space|bigint|予約済み領域の一部で使用されていない領域 (KB 単位)。|  

## <a name="see-also"></a>参照

[結果セットのキャッシュを使用したパフォーマンスのチューニング](/azure/sql-data-warehouse/performance-tuning-result-set-caching)</br>
[ALTER DATABASE SET のオプション &#40;Transact-SQL&#41;](../statements/alter-database-transact-sql-set-options.md?view=azure-sqldw-latest)</br>
[ALTER DATABASE &#40;Transact-SQL&#41;](../statements/alter-database-transact-sql.md?view=azure-sqldw-latest)</br>
[SET RESULT SET CACHING &#40;Transact-SQL&#41;](../statements/set-result-set-caching-transact-sql.md)</br>
[DBCC DROPRESULTSETCACHE  &#40;Transact-SQL&#41;](./dbcc-dropresultsetcache-transact-sql.md)