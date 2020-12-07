---
description: DBCC FREESYSTEMCACHE (Transact-SQL)
title: DBCC FREESYSTEMCACHE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 02/25/2020
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- FREESYSTEMCACHE_TSQL
- DBCC_FREESYSTEMCACHE_TSQL
- DBCC FREESYSTEMCACHE
- FREESYSTEMCACHE
dev_langs:
- TSQL
helpviewer_keywords:
- clearing unused cache entries
- DBCC FREESYSTEMCACHE statement
- unused cache entries
- releasing unused cache entries
- freeing unused cache entries
- cleaning unused cache entries
ms.assetid: 4b5c460b-e4ad-404a-b4ca-d65aba38ebbb
author: pmasl
ms.author: umajay
ms.openlocfilehash: 0069e1fc2a6991df71291fd377aaa76e10f23256
ms.sourcegitcommit: b09f069c6bef0655b47e9953a4385f1b52bada2b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/27/2020
ms.locfileid: "92734631"
---
# <a name="dbcc-freesystemcache-transact-sql"></a>DBCC FREESYSTEMCACHE (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

キャッシュ全体から未使用のすべてのキャッシュ エントリを解放します。 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]では、未使用のキャッシュ エントリをバックグラウンドで事前にクリーンアップし、メモリを現在のエントリで使用できるようにします。 ただし、このコマンドを使用できるのは、各キャッシュまたは指定したリソース ガバナー プール キャッシュから未使用のキャッシュ エントリを手動で削除する場合です。
  
![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>構文  
```syntaxsql
DBCC FREESYSTEMCACHE   
    ( 'ALL' [, pool_name ] )   
    [WITH   
    { [ MARK_IN_USE_FOR_REMOVAL ] , [ NO_INFOMSGS ]  }  
    ]  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>引数
( 'ALL' [, _pool\_name_ ] )  
ALL はサポートされるすべてのキャッシュを指定します。  
_pool\_name_ はリソース ガバナー プール キャッシュを指定します。 このプールに関連付けられたエントリだけが解放されます。 使用可能なプール名を一覧表示するには、次のように実行します。

```sql
SELECT name FROM sys.dm_os_memory_clerks
```

このコマンドを使用すると、すべてではありませんが、ほとんどのキャッシュを個別に解放できます。
  
MARK_IN_USE_FOR_REMOVAL  
現在使用しているエントリが使用されなくなったら、それぞれのキャッシュから非同期に解放します。 DBCC FREESYSTEMCACHE WITH MARK_IN_USE_FOR_REMOVAL の実行後、キャッシュ内に作成された新しいエントリには影響ありません。  
  
NO_INFOMSGS  
すべての情報メッセージを表示しないようにします。  
  
## <a name="remarks"></a>解説  
DBCC FREESYSTEMCACHE を実行すると、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスのプラン キャッシュが消去されます。 プラン キャッシュが消去されると、後続のすべての実行プランが再コンパイルされ、場合によっては、クエリ パフォーマンスが一時的に急激に低下します。 プラン キャッシュ内のキャッシュ ストアが消去されるたびに、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エラー ログに次のような通知メッセージが記録されます。

>`SQL Server has encountered %d occurrence(s) of cachestore flush for the '%s' cachestore (part of plan cache) due to 'DBCC FREEPROCCACHE' or 'DBCC FREESYSTEMCACHE' operations.`

 このメッセージは、5 分以内にキャッシュがフラッシュされる限り、5 分間隔でログに記録されます。

## <a name="result-sets"></a>結果セット  
DBCC FREESYSTEMCACHE は次のメッセージを返します。"DBCC の実行が完了しました。 DBCC がエラー メッセージを出力した場合は、システム管理者に相談してください。"
  
## <a name="permissions"></a>アクセス許可  
サーバーに対する ALTER SERVER STATE 権限が必要です。
  
## <a name="examples"></a>例  
  
### <a name="a-releasing-unused-cache-entries-from-a-resource-governor-pool-cache"></a>A. リソース ガバナー プール キャッシュから未使用のキャッシュ エントリを解放する  
次の例は、指定したリソース ガバナー リソース プール専用のキャッシュを消去する方法を示しています。
  
```sql
-- Clean all the caches with entries specific to the resource pool named "default".  
DBCC FREESYSTEMCACHE ('ALL', default);  
```  
  
### <a name="b-releasing-entries-from-their-respective-caches-after-they-become-unused"></a>B. エントリが使用されなくなったらそれぞれのキャッシュから解放する  
次の例では、MARK_IN_USE_FOR_REMOVAL 句を使用して、エントリが使用されなくなったら現在のすべてのキャッシュから解放します。
  
```sql
DBCC FREESYSTEMCACHE ('ALL') WITH MARK_IN_USE_FOR_REMOVAL;  
```  
  
## <a name="see-also"></a>参照  
[DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)  
[DBCC FREEPROCCACHE &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-freeproccache-transact-sql.md)  
[DBCC FREESESSIONCACHE &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-freesessioncache-transact-sql.md)  
[リソース ガバナー](../../relational-databases/resource-governor/resource-governor.md)
  
  
