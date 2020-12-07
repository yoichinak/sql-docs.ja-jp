---
description: sp_updatestats (Transact-SQL)
title: sp_updatestats (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 09/25/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_updatestats_TSQL
- sp_updatestats
dev_langs:
- TSQL
helpviewer_keywords:
- sp_updatestats
ms.assetid: 01184651-6e61-45d9-a502-366fecca0ee4
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: dee5ef30ca260855c9df6a7823e7dce605c3ff72
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89534806"
---
# <a name="sp_updatestats-transact-sql"></a>sp_updatestats (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

`UPDATE STATISTICS`現在のデータベース内のすべてのユーザー定義テーブルと内部テーブルに対して実行します。  
  
の詳細について `UPDATE STATISTICS` は、「 [UPDATE STATISTICS &#40;transact-sql&#41;](../../t-sql/statements/update-statistics-transact-sql.md)」を参照してください。 統計の詳細については、「[統計](../../relational-databases/statistics/statistics.md)」を参照してください。  
    
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
sp_updatestats [ [ @resample = ] 'resample']  
```  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="arguments"></a>引数  
`[ @resample = ] 'resample'`**Sp_updatestats**で、 [UPDATE STATISTICS](../../t-sql/statements/update-statistics-transact-sql.md)ステートメントのリサンプリングオプションを使用することを指定します。 **' リサンプリング '** が指定されていない場合、 **sp_updatestats**は既定のサンプリングを使用して統計を更新します。 **リサンプリング** は **varchar (8)** で、既定値は NO です。  
  
## <a name="remarks"></a>解説  
 **sp_updatestats** は、 `UPDATE STATISTICS` キーワードを指定することによって、 `ALL` データベース内のすべてのユーザー定義テーブルと内部テーブルに対して実行します。 sp_updatestats の進行状況を示すメッセージが表示されます。 更新が完了すると、すべてのテーブルの統計が更新されたことが報告されます。  
  
無効な非クラスター化インデックスの統計を更新し、無効になっているクラスター化インデックスの統計を更新しません。 **sp_updatestats** 。  
  
ディスクベーステーブルの場合、 **sp_updatestats**は、 **dm_db_stats_properties**カタログビューの**modification_counter**情報に基づいて統計を更新し、少なくとも1つの行が変更されている統計を更新します。 メモリ最適化テーブルの統計は、 **sp_updatestats**の実行時に常に更新されます。 そのため、 **sp_updatestats** は必要以上に実行しないでください。  
  
**sp_updatestats** は、ストアドプロシージャまたはその他のコンパイル済みコードの再コンパイルをトリガーできます。 ただし、参照されるテーブルとそのインデックスに対してクエリプランが1つしか使用できない場合、 **sp_updatestats** は再コンパイルを発生させない可能性があります。 このような場合は、統計が更新されても再コンパイルの必要はありません。  
  
互換性レベルが90未満のデータベースの場合、 **sp_updatestats** を実行しても、特定の統計の最新の NORECOMPUTE 設定は保持されません。 互換性レベルが90以上のデータベースの場合、sp_updatestats は特定の統計の最新の NORECOMPUTE オプションを保持します。 統計の更新の無効化および再有効化について詳しくは、「[統計](../../relational-databases/statistics/statistics.md)」をご覧ください。  
  
## <a name="permissions"></a>アクセス許可  

**Sp_updatestats**を実行するには、ユーザーがデータベースの所有者 ( `dbo` ロールのメンバーではない) である `db_owner` か、sysadmin 固定サーバーロールのメンバーである必要があります。

## <a name="examples"></a>例  
次の例では、データベース内のテーブルの統計を更新し [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] ます。  
  
```sql  
USE AdventureWorks2012;  
GO  
EXEC sp_updatestats;   
```  

## <a name="automatic-index-and-statistics-management"></a>インデックスと統計の自動管理
[Adaptive Index Defrag](https://github.com/Microsoft/tigertoolbox/tree/master/AdaptiveIndexDefrag) のようなソリューションを活用し、1 つまたは複数のデータベースに対するインデックスの最適化と統計更新を自動管理します。 このプロシージャでは、断片化レベルやその他のパラメーターに基づいてインデックスを再構築または再構成するか、線形しきい値で統計を更新するかが自動的に選択されます。

## <a name="see-also"></a>参照  
 [ALTER DATABASE SET オプション &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)   
 [CREATE STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/create-statistics-transact-sql.md)   
 [DBCC SHOW_STATISTICS &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-show-statistics-transact-sql.md)   
 [DROP STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/drop-statistics-transact-sql.md)   
 [sp_autostats &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-autostats-transact-sql.md)   
 [sp_createstats &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-createstats-transact-sql.md)   
 [UPDATE STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/update-statistics-transact-sql.md)   
 [システムストアドプロシージャ](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
 
