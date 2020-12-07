---
description: sp_createstats (Transact-sql)
title: sp_createstats (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_createstats_TSQL
- sp_createstats
dev_langs:
- TSQL
helpviewer_keywords:
- sp_createstats
ms.assetid: 8204f6f2-5704-40a7-8d51-43fc832eeb54
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 6c49367f78a257b1ba4e19d9916b590a67991d1a
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89536703"
---
# <a name="sp_createstats-transact-sql"></a>sp_createstats (Transact-sql)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  [CREATE statistics](../../t-sql/statements/create-statistics-transact-sql.md)ステートメントを呼び出して、統計オブジェクトの最初の列ではない列に対して単一列の統計を作成します。 統計を 1 列ずつ作成すると、ヒストグラムの数が増えて、カーディナリティの推定、クエリ プラン、およびクエリのパフォーマンスが向上します。 統計オブジェクトの最初の列にはヒストグラムがあります。その他の列にはヒストグラムがありません。  
  
 sp_createstats は、クエリの実行時間が重要であり、クエリオプティマイザーが単一列の統計を生成するのを待機できない場合のベンチマークなどのアプリケーションに役立ちます。 ほとんどの場合、sp_createstats を使用する必要はありません。クエリオプティマイザーでは、必要に応じて1列ずつの統計が生成され、 **AUTO_CREATE_STATISTICS** オプションがオンになっている場合にクエリプランが向上します。  
  
 統計の詳細については、「[統計](../../relational-databases/statistics/statistics.md)」を参照してください。 1列ずつの統計の生成の詳細については、「 [ALTER DATABASE SET Options &#40;transact-sql&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)」の**AUTO_CREATE_STATISTICS**オプションを参照してください。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_createstats   
    [   [ @indexonly =   ] { 'indexonly'   | 'NO' } ]   
    [ , [ @fullscan =    ] { 'fullscan'    | 'NO' } ]   
    [ , [ @norecompute = ] { 'norecompute' | 'NO' } ]  
    [ , [ @incremental = ] { 'incremental' | 'NO' } ]  
```  
  
## <a name="arguments"></a>引数  
`[ @indexonly = ] 'indexonly'` では、既存のインデックス内の列に対してのみ統計が作成され、インデックス定義の最初の列ではありません。 **indexonly** は **char (9)** です。 既定値は NO です。  
  
`[ @fullscan = ] 'fullscan'`[CREATE STATISTICS](../../t-sql/statements/create-statistics-transact-sql.md)ステートメントを**FULLSCAN**オプションと共に使用します。 **fullscan** は **char (9)** です。  既定値は NO です。  
  
`[ @norecompute = ] 'norecompute'`[CREATE STATISTICS](../../t-sql/statements/create-statistics-transact-sql.md)ステートメントを**NORECOMPUTE**オプションと共に使用します。 **norecompute** は **char (12)** です。  既定値は NO です。  
  
`[ @incremental = ] 'incremental'`[CREATE STATISTICS](../../t-sql/statements/create-statistics-transact-sql.md)ステートメントを**増分 = ON**オプションと共に使用します。 **増分** は **char (12)** です。  既定値は NO です。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="result-sets"></a>結果セット  
 新しい各統計オブジェクトには、作成された列と同じ名前が付けられます。  
  
## <a name="remarks"></a>解説  
 sp_createstats は、既存の統計オブジェクトの最初の列である列の統計を作成または更新しません。 これには、インデックス用に作成された統計の最初の列、AUTO_CREATE_STATISTICS オプションで生成された単一列統計を持つ列、および CREATE STATISTICS ステートメントを使用して作成された統計の最初の列が含まれます。 sp_createstats は、その列が別の有効なインデックスで使用されていない限り、無効になったインデックスの最初の列に対して統計を作成しません。 sp_createstats では、無効になっているクラスター化インデックスを持つテーブルに対する統計は作成されません。  
  
 テーブルに列セットが含まれている場合、sp_createstats ではスパース列に対する統計は作成されません。 列セットとスパース列の詳細については、「 [列セットの使用](../../relational-databases/tables/use-column-sets.md) 」および「 [スパース列の使用](../../relational-databases/tables/use-sparse-columns.md)」を参照してください。  
  
## <a name="permissions"></a>アクセス許可  
 db_owner 固定データベース ロールのメンバーシップが必要です。  
  
## <a name="examples"></a>例  
  
### <a name="a-create-single-column-statistics-on-all-eligible-columns"></a>A. 条件を満たすすべての列の統計を 1 列ずつ作成する  
 次の例では、現在のデータベースの対象となるすべての列に対して、単一列の統計を作成します。  
  
```  
EXEC sp_createstats;  
GO  
```  
  
### <a name="b-create-single-column-statistics-on-all-eligible-index-columns"></a>B. 条件を満たすすべてのインデックス列の統計を 1 列ずつ作成する  
 次の例では、インデックスに既に含まれており、インデックスの最初の列ではない、対象となるすべての列に対して単一列統計を作成します。  
  
```  
EXEC sp_createstats 'indexonly';  
GO  
```  
  
## <a name="see-also"></a>参照  
 [統計](../../relational-databases/statistics/statistics.md)   
 [CREATE STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/create-statistics-transact-sql.md)   
 [ALTER DATABASE SET オプション &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)   
 [DBCC SHOW_STATISTICS &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-show-statistics-transact-sql.md)   
 [DROP STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/drop-statistics-transact-sql.md)   
 [UPDATE STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/update-statistics-transact-sql.md)   
 [Transact-sql&#41;&#40;のストアドプロシージャのデータベースエンジン ](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
