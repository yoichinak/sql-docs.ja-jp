---
description: sp_table_privileges_ex (Transact-sql)
title: sp_table_privileges_ex (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_table_privileges_ex
- sp_table_privileges_ex_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_table_privileges_ex
ms.assetid: b58d4a07-5c40-4f17-b66e-6d6b17188dda
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 33deb78c83c59599540b6ed91893b11bc1ae201e
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89551173"
---
# <a name="sp_table_privileges_ex-transact-sql"></a>sp_table_privileges_ex (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  指定したリンク サーバーから、指定したテーブルの特権情報を返します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_table_privileges_ex [ @table_server = ] 'table_server'   
     [ , [ @table_name = ] 'table_name' ]   
     [ , [ @table_schema = ] 'table_schema' ]   
     [ , [ @table_catalog = ] 'table_catalog' ]  
     [ , [@fUsePattern =] 'fUsePattern']  
```  
  
## <a name="arguments"></a>引数  
`[ @table_server = ] 'table_server'` 情報を返すリンクサーバーの名前を指定します。 *table_server* は **sysname**であり、既定値はありません。  
  
`[ @table_name = ] 'table_name']` テーブルの特権情報を提供するテーブルの名前を指定します。 *table_name* は **sysname**,、既定値は NULL です。  
  
`[ @table_schema = ] 'table_schema'` テーブルスキーマを示します。 これは、一部の DBMS 環境ではテーブルの所有者です。 *table_schema* は **sysname**,、既定値は NULL です。  
  
`[ @table_catalog = ] 'table_catalog'` 指定した *table_name* が存在するデータベースの名前を指定します。 *table_catalog* は **sysname**,、既定値は NULL です。  
  
`[ @fUsePattern = ] 'fUsePattern'` 文字 ' _ '、'% '、' ['、および '] ' がワイルドカード文字として解釈されるかどうかを判断します。 有効な値は 0 (パターン一致がオフ) および 1 (パターン一致がオン) です。 *Fusepattern* は **ビット**,、既定値は1です。  
  
## <a name="return-code-values"></a>リターン コードの値  
 なし  
  
## <a name="result-sets"></a>結果セット  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**TABLE_CAT**|**sysname**|テーブル修飾子の名前。 さまざまな DBMS 製品では、3つの要素で構成するテーブル (_修飾子_) がサポート**しています。**_所有者_**。**_名前_)。 では [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、この列はデータベース名を表します。 一部の製品では、テーブルのデータベース環境のサーバー名を表します。 このフィールドは NULL にすることができます。|  
|**TABLE_SCHEM**|**sysname**|テーブル所有者の名前。 では、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] この列は、テーブルを作成したデータベースユーザーの名前を表します。 このフィールドは常に値を返します。|  
|**TABLE_NAME**|**sysname**|テーブル名。 このフィールドは常に値を返します。|  
|**権限**|**sysname**|**一覧表示された**権限付与対象ユーザーに対し、この**TABLE_NAME**に対する権限を許可したデータベースユーザー名です。 で [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は、この列は常に **TABLE_OWNER**と同じです。 このフィールドは常に値を返します。 また、権限の許可者の列は、データベース所有者 (**TABLE_OWNER**) か、grant ステートメントで WITH GRANT OPTION 句を使用してデータベース所有者が権限を許可したユーザーのいずれかである可能性があります。|  
|**GRANTEE**|**sysname**|**一覧表示された**権限付与者によって、この**TABLE_NAME**に対する権限が許可されたデータベースユーザー名です。 このフィールドは常に値を返します。|  
|**持っ**|**varchar (** 32 **)**|使用可能なテーブル権限の 1 つ。 テーブル権限は、次の値のいずれか、または実装が定義されている場合にデータソースでサポートされるその他の値のいずれかになります。<br /><br /> SELECT = 権限付与対象ユーザーは、1つまたは複数の列のデータを取得**できます。**<br /><br /> INSERT = 権限付与対象ユーザーは、1つまたは複数の列に新しい行のデータを提供**できます。**<br /><br /> UPDATE = 権限付与対象ユーザーは、1つまたは複数の列の既存のデータを変更**できます。**<br /><br /> DELETE = 権限付与対象ユーザーは、テーブルから **行を削除** できます。<br /><br /> REFERENCES = 権限付与対象ユーザーは、主キー/外部キーのリレーションシップで外部テーブルの列を参照**できます。** で [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は、主キー/外部キーのリレーションシップはテーブル制約を使用して定義されます。<br /><br /> 特定 **のテーブル特権によって** 権限付与対象ユーザーに与えられるアクションのスコープは、データソースによって異なります。 たとえば、更新権限が **与えられている場合** 、権限付与対象ユーザーは、1つのデータソース上のテーブル内のすべての列を更新できます。また、権限付与対象ユーザーが別のデータソースに対する update 権限 **を持って** いる列だけを更新することもできます。|  
|**IS_GRANTABLE**|**varchar (** 3 **)**|権限付与対象 **ユーザーに対し、他** のユーザーに権限を許可することを許可するかどうかを示します。 これは、"許可の許可" 権限と呼ばれることがあります。 YES、NO、または NULL を指定できます。 不明、つまり NULL の場合は、"許可の許可" が適用されないデータ ソースを示します。|  
  
## <a name="remarks"></a>解説  
 返される結果は、 **TABLE_QUALIFIER**、 **TABLE_OWNER**、 **TABLE_NAME**、および **特権**によって並べ替えられます。  
  
## <a name="permissions"></a>アクセス許可  
 スキーマに対する SELECT 権限が必要です。  
  
## <a name="examples"></a>例  
 次の例では、 `Product` [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 指定したリンクサーバーから、データベースので始まる名前のテーブルに関する特権情報を返し `Seattle1` ます。 ( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] はリンクサーバーと見なされます)。  
  
```  
EXEC sp_table_privileges_ex @table_server = 'Seattle1',   
   @table_name = 'Product%',   
   @table_schema = 'Production',  
   @table_catalog ='AdventureWorks2012';  
```  
  
## <a name="see-also"></a>参照  
 [sp_column_privileges_ex &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-column-privileges-ex-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [分散クエリストアドプロシージャ &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/distributed-queries-stored-procedures-transact-sql.md)  
  
  
