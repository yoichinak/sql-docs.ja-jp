---
description: sp_execute_remote (Azure SQL Database)
title: sp_execute_remote (Azure SQL Database) |Microsoft Docs
ms.custom: ''
ms.date: 02/01/2017
ms.service: sql-database
ms.reviewer: ''
ms.topic: conceptual
f1_keywords:
- sp_execute_remote
- sp_execute_remote_TSQL
helpviewer_keywords:
- remote execution
- queries, remote execution
ms.assetid: ca89aa4c-c4c1-4c46-8515-a6754667b3e5
author: markingmyname
ms.author: maghan
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: dd5b35e6c999f69b7adda16fd4590942cd2da63b
ms.sourcegitcommit: 04cf7905fa32e0a9a44575a6f9641d9a2e5ac0f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/07/2020
ms.locfileid: "91810248"
---
# <a name="sp_execute_remote-azure-sql-database"></a>sp_execute_remote (Azure SQL Database)
[!INCLUDE[Azure SQL Database Azure SQL Managed Instance](../../includes/applies-to-version/asdb-asdbmi.md)]

  [!INCLUDE[tsql](../../includes/tsql-md.md)]シャードとして機能する単一のリモート Azure SQL Database またはデータベースのセットに対して、行方向のパーティション構成でステートメントを実行します。  
  
 このストアドプロシージャは、エラスティッククエリ機能の一部です。  「 [エラスティックデータベースクエリの概要](/azure/azure-sql/database/elastic-query-overview) 」および「 [シャーディングのエラスティックデータベースクエリ (行方向のパーティション分割)」を](/azure/azure-sql/database/elastic-query-horizontal-partitioning)参照して Azure SQL Database ください。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
sp_execute_remote [ @data_source_name = ] datasourcename  
[ , @stmt = ] statement  
[   
  { , [ @params = ] N'@parameter_name data_type [,...n ]' }   
     { , [ @param1 = ] 'value1' [ ,...n ] }  
]  
```  
  
## <a name="arguments"></a>引数  
 [ \@ data_source_name =] *datasourcename*  
 ステートメントが実行される外部データソースを識別します。 「 [CREATE EXTERNAL DATA SOURCE &#40;transact-sql&#41;](../../t-sql/statements/create-external-data-source-transact-sql.md)」を参照してください。 外部データソースの種類は、"RDBMS" または "SHARD_MAP_MANAGER" にすることができます。  
  
 [ \@ stmt =] *ステートメント*  
 ステートメントまたはバッチを含む Unicode 文字列を指定し [!INCLUDE[tsql](../../includes/tsql-md.md)] ます。 \@stmt は、Unicode 定数または Unicode 変数のいずれかである必要があります。 + 演算子で 2 つの文字列を連結するなどの複雑な Unicode 式は使用できません。 文字定数も使用できません。 Unicode 定数を指定する場合は、先頭に **N**を付ける必要があります。たとえば、Unicode 定数 **N ' sp_who '** は有効ですが、文字定数 **' sp_who '** は有効ではありません。 文字列のサイズは、使用可能なデータベースサーバーのメモリによってのみ制限されます。 64ビットサーバーでは、文字列のサイズは、最大サイズである **nvarchar (max)** の 2 GB に制限されています。  
  
> [!NOTE]  
>  \@stmt には、変数名と同じ形式のパラメーターを含めることができます。次に例を示します。 `N'SELECT * FROM HumanResources.Employee WHERE EmployeeID = @IDParameter'`  
  
 Stmt に含まれる各パラメーターには、 \@ \@ params パラメーター定義リストとパラメーター値リストの両方に対応するエントリが必要です。  
  
 [ \@ params =] N ' \@*parameter_name * * data_type* [,... *n* ] '  
 Stmt に埋め込まれているすべてのパラメーターの定義を含む1つの文字列を指定 \@ します。文字列は、Unicode 定数または Unicode 変数のいずれかである必要があります。 各パラメーター定義は、パラメーター名とデータ型で構成されます。 *n* は、追加のパラメーター定義を示すプレースホルダーです。 Stmtmust で指定されたすべてのパラメーター \@ は、params で定義され \@ ます。 [!INCLUDE[tsql](../../includes/tsql-md.md)]Stmt のステートメントまたはバッチにパラメーターが含まれていない場合 \@ 、 \@ params は必要ありません。 このパラメーターの既定値は NULL です。  
  
 [ \@ param1 =] '*value1*'  
 パラメーター文字列に定義する最初のパラメーターの値を指定します。 Unicode 定数または Unicode 変数を指定できます。 Stmt に含まれるすべてのパラメーターにパラメーター値が指定されている必要があり \@ ます。 [!INCLUDE[tsql](../../includes/tsql-md.md)] Stmt のステートメントまたはバッチにパラメーターがない場合、値は必要ありません \@ 。  
  
 *n*  
 追加のパラメーターの値のプレースホルダーです。 定数または変数のみを指定できます。 値には、関数や演算子を使用して作成された式など、より複雑な式を指定することはできません。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または0以外 (失敗)  
  
## <a name="result-sets"></a>結果セット  
 最初の SQL ステートメントから結果セットを返します。  
  
## <a name="permissions"></a>アクセス許可  
 `ALTER ANY EXTERNAL DATA SOURCE` 権限が必要です。  
  
## <a name="remarks"></a>注釈  
 `sp_execute_remote` パラメーターは、前の「構文」セクションで説明されているように、特定の順序で入力する必要があります。 パラメーターが順序どおりに入力されていない場合は、エラーメッセージが表示されます。  
  
 `sp_execute_remote` には、バッチと名前のスコープに関して、 [transact-sql&#41;の実行 &#40;](../../t-sql/language-elements/execute-transact-sql.md) と同じ動作があります。 Sp_execute_remote * \@ stmt*パラメーター内の transact-sql ステートメントまたはバッチは、sp_execute_remote ステートメントが実行されるまでコンパイルされません。  
  
 `sp_execute_remote` 行を生成したリモートデータベースの名前を含む ' $ShardName ' という名前の結果セットに列を追加します。  
  
 `sp_execute_remote` は、 [transact-sql&#41;&#40;sp_executesql ](../../relational-databases/system-stored-procedures/sp-executesql-transact-sql.md)と同様に使用できます。  
  
## <a name="examples"></a>例  
### <a name="simple-example"></a>簡単な例  
 次の例では、リモートデータベースに対して単純な SELECT ステートメントを作成して実行します。  
  
```sql  
EXEC sp_execute_remote  
    N'MyExtSrc',  
    N'SELECT COUNT(w_id) AS Count_id FROM warehouse'   
```  
  
### <a name="example-with-multiple-parameters"></a>複数のパラメーターを使用した例  
ユーザーデータベースにデータベーススコープの資格情報を作成し、master データベースの管理者の資格情報を指定します。 マスターデータベースを指す外部データソースを作成し、データベーススコープの資格情報を指定します。 次に、ユーザーデータベースの例では、 `sp_set_firewall_rule` master データベースでプロシージャを実行します。 この `sp_set_firewall_rule` プロシージャには3つのパラメーターが必要であり、 `@name` パラメーターは Unicode である必要があります。

```
EXEC sp_execute_remote @data_source_name  = N'PointToMaster', 
@stmt = N'sp_set_firewall_rule @name, @start_ip_address, @end_ip_address', 
@params = N'@name nvarchar(128), @start_ip_address varchar(50), @end_ip_address varchar(50)',
@name = N'TempFWRule', @start_ip_address = '0.0.0.2', @end_ip_address = '0.0.0.2';
```

## <a name="see-also"></a>参照:

[CREATE DATABASE SCOPED CREDENTIAL](../../t-sql/statements/create-database-scoped-credential-transact-sql.md)  
[CREATE EXTERNAL DATA SOURCE (Transact-SQL)](../../t-sql/statements/create-external-data-source-transact-sql.md)  
