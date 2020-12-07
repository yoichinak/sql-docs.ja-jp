---
description: sp_column_privileges (Transact-SQL)
title: sp_column_privileges (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_column_privileges_TSQL
- sp_column_privileges
dev_langs:
- TSQL
helpviewer_keywords:
- sp_column_privileges
ms.assetid: a3784301-2517-4b1d-bbd9-47404483fad0
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 44097fb7340dd61f467b4bb08e0b4a718d6ab323
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89528534"
---
# <a name="sp_column_privileges-transact-sql"></a>sp_column_privileges (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  現在の環境内の1つのテーブルの列権限情報を返します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_column_privileges [ @table_name = ] 'table_name'   
     [ , [ @table_owner = ] 'table_owner' ]   
     [ , [ @table_qualifier = ] 'table_qualifier' ]   
     [ , [ @column_name = ] 'column' ]  
```  
  
## <a name="arguments"></a>引数  
 [ @table_name =] '*table_name*'  
 カタログ情報を返すために使用するテーブルを指定します。 *table_name* は **sysname**であり、既定値はありません。 ワイルドカードのパターンマッチングはサポートされていません。  
  
 [ @table_owner =] '*table_owner*'  
 カタログ情報を返すために使用するテーブルの所有者を示します。 *table_owner* は **sysname**,、既定値は NULL です。 ワイルドカードのパターンマッチングはサポートされていません。 *Table_owner*が指定されていない場合は、基になるデータベース管理システム (DBMS) の既定のテーブル可視性ルールが適用されます。  
  
 指定した名前のテーブルを現在のユーザーが所有している場合は、そのテーブルの列が返されます。 *Table_owner*が指定されておらず、現在のユーザーが指定された*table_name*のテーブルを所有していない場合、sp_column 権限は、データベース所有者が所有する、指定された*table_name*を持つテーブルを検索します。 存在する場合は、そのテーブルの列が返されます。  
  
 [ @table_qualifier =] '*table_qualifier*'  
 テーブル修飾子の名前を指定します。 *table_qualifier* は *sysname*,、既定値は NULL です。 さまざまな DBMS 製品では、3つの要素で構成するテーブル (_修飾子_) がサポート**しています。**_所有者_**。**_名前_)。 では [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、この列はデータベース名を表します。 一部の製品では、テーブルのデータベース環境のサーバー名を表します。  
  
 [ @column_name =] '*column*'  
 カタログ情報の列を1つだけ取得する場合に使用する単一の列を示します。 *列* は **nvarchar (** 384 **)**,、既定値は NULL です。 *列*が指定されていない場合は、すべての列が返されます。 では [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、 *列* は、テーブルに示されている列名を表します。 *列* には、基になる DBMS のワイルドカードパターンを使用したワイルドカード文字を含めることができます。 相互運用性を最大にするために、ゲートウェイクライアントは ISO 標準のパターン照合 (% と _ ワイルドカード文字) のみを想定する必要があります。  
  
## <a name="result-sets"></a>結果セット  
 sp_column_privileges は、ODBC の SQLColumnPrivileges に相当します。 返される結果は、TABLE_QUALIFIER、TABLE_OWNER、TABLE_NAME、COLUMN_NAME、PRIVILEGE の順序に従って並べ替えられます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|TABLE_QUALIFIER|**sysname**|テーブル修飾子の名前。 このフィールドは NULL にすることができます。|  
|TABLE_OWNER|**sysname**|テーブル所有者の名前。 このフィールドは常に値を返します。|  
|TABLE_NAME|**sysname**|テーブル名。 このフィールドは常に値を返します。|  
|COLUMN_NAME|**sysname**|返される TABLE_NAME の各列の名前。 このフィールドは常に値を返します。|  
|GRANTOR|**sysname**|COLUMN_NAME に対する権限を、表示される GRANTEE に与えたデータベース ユーザーの名前。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、この列は常に TABLE_OWNER と同じです。 このフィールドは常に値を返します。<br /><br /> GRANTOR 列の値は、データベース所有者 (TABLE_OWNER) か、GRANT ステートメントで WITH GRANT OPTION 句を使用して、データベース所有者が権限を許可したユーザーになります。|  
|GRANTEE|**sysname**|COLUMN_NAME に対する権限を、表示される GRANTOR によって与えられたデータベース ユーザーの名前。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、この列には常に、sysusers テーブルに記録されているデータベース ユーザーが格納されます。 このフィールドは常に値を返します。|  
|PRIVILEGE|**varchar (** 32 **)**|使用可能な列権限の1つ。 列権限は、次の値のいずれかになります (または、実装が定義されている場合に、データソースによってサポートされるその他の値)。<br /><br /> SELECT。GRANTEE は、列からデータを取得できます。<br /><br /> INSERT。GRANTEE は、テーブルに新しい行を挿入したときにこの列のデータを設定できます。<br /><br /> UPDATE。GRANTEE は、列内の既存のデータを修正できます。<br /><br /> REFERENCES。GRANTEE は、主キー/外部キーのリレーションシップで外部テーブル内の列を参照できます。 主キー/外部キーのリレーションシップは、テーブル制約を使用して定義されます。|  
|IS_GRANTABLE|**varchar (** 3 **)**|権限付与対象ユーザーに対し、他のユーザーに対する権限の許可を許可するかどうかを示します ("grant with grant" 権限と呼ばれることもあります)。 YES、NO、または NULL を指定できます。 不明な値または NULL の場合は、"許可の許可" が適用されないデータ ソースであることを示します。|  
  
## <a name="remarks"></a>解説  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、権限は GRANT ステートメントで与え、REVOKE ステートメントで取り消します。  
  
## <a name="permissions"></a>アクセス許可  
 スキーマに対する SELECT 権限が必要です。  
  
## <a name="examples"></a>例  
 次の例では、特定の列の列権限情報を返します。  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_column_privileges @table_name = 'Employee'   
    ,@table_owner = 'HumanResources'  
    ,@table_qualifier = 'AdventureWorks2012'  
    ,@column_name = 'SalariedFlag';  
```  
  
## <a name="see-also"></a>参照  
 [GRANT &#40;Transact-SQL&#41;](../../t-sql/statements/grant-transact-sql.md)   
 [REVOKE &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
