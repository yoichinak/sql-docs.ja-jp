---
description: sp_recompile (Transact-sql)
title: sp_recompile (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_recompile_TSQL
- sp_recompile
dev_langs:
- TSQL
helpviewer_keywords:
- sp_recompile
ms.assetid: 6192ca87-febd-4075-8199-14b4fa609b8c
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 3e0f32166351f80b87b28a169ea0204af97f832f
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89547608"
---
# <a name="sp_recompile-transact-sql"></a>sp_recompile (Transact-sql)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  ストアド プロシージャ、トリガー、およびユーザー定義関数が次回実行時に再コンパイルされるようにします。 これを行うには、プロシージャキャッシュから既存のプランを削除します。これにより、プロシージャまたはトリガーの次回実行時に新しいプランが作成されます。 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] コレクションでは、SP:Recompile イベントではなく SP:CacheInsert イベントがログに記録されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```sql  
  
sp_recompile [ @objname = ] 'object'  
```  
  
## <a name="arguments"></a>引数  
 [ @objname =] '*オブジェクト*'  
 現在のデータベースにあるストアド プロシージャ、トリガー、テーブル、ビュー、またはユーザー定義関数の修飾名または非修飾名を指定します。 *オブジェクト* は **nvarchar (776)**,、既定値はありません。 *オブジェクト*がストアドプロシージャ、トリガー、またはユーザー定義関数の名前である場合、ストアドプロシージャ、トリガー、または関数は、次回実行時に再コンパイルされます。 *オブジェクト*がテーブルまたはビューの名前である場合、テーブルまたはビューを参照するすべてのストアドプロシージャ、トリガー、またはユーザー定義関数は、次回の実行時に再コンパイルされます。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または0以外の数値 (失敗)  
  
## <a name="remarks"></a>解説  
 sp_recompile は、現在のデータベース内でのみオブジェクトを検索します。  
  
 ストアド プロシージャ、トリガー、およびユーザー定義関数が使用するクエリは、コンパイル時にだけ最適化されます。 データベースにインデックスを追加したり、変更を加えたりすると、統計が変化するため、コンパイルされたストアド プロシージャ、トリガー、およびユーザー定義関数の効率が低下する場合があります。 そのテーブルに作用するストアド プロシージャやトリガーを再コンパイルすることにより、クエリを再び最適化できます。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、ストアドプロシージャ、トリガー、およびユーザー定義関数を自動的に再コンパイルします。  
  
## <a name="permissions"></a>アクセス許可  
 指定されたオブジェクトに対する ALTER 権限が必要です。  
  
## <a name="examples"></a>例  
 次の例では、`Customer` テーブルを対象とするストアド プロシージャ、トリガー、およびユーザー定義関数が次回実行時に再コンパイルされます。  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_recompile N'Sales.Customer';  
GO  
```  
  
## <a name="see-also"></a>参照  
 [CREATE PROCEDURE &#40;Transact-SQL&#41;](../../t-sql/statements/create-procedure-transact-sql.md)   
 [CREATE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
