---
description: sys.sp_xtp_bind_db_resource_pool (Transact-SQL)
title: sp_xtp_bind_db_resource_pool (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 08/03/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_xtp_bind_db_resource_pool_TSQL
- sp_xtp_bind_db_resource_pool
- sys.sp_xtp_bind_db_resource_pool_TSQL
- sys.sp_xtp_bind_db_resource_pool
dev_langs:
- TSQL
helpviewer_keywords:
- sp_xtp_bind_db_resource_pool
- sys.sp_xtp_bind_db_resource_pool
ms.assetid: c2a78073-626b-4159-996e-1808f6bfb6d2
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 436d04ea81df4b25646b4b56d8ac59ffc9fa3b91
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89540414"
---
# <a name="syssp_xtp_bind_db_resource_pool-transact-sql"></a>sys.sp_xtp_bind_db_resource_pool (Transact-SQL)
[!INCLUDE[sqlserver](../../includes/applies-to-version/sqlserver.md)]

  指定されたリソース プールに指定された[!INCLUDE[hek_2](../../includes/hek-2-md.md)] データベースをバインドします。 実行する前に、データベースとリソースプールの両方が存在している必要があり `sys.sp_xtp_bind_db_resource_pool` ます。  
  
 このシステムプロシージャは、resource_pool_name によって識別される Resource Governor プールと database_name によって識別されるデータベースとの間のバインドを作成します。 バインド時にデータベースにメモリ最適化オブジェクトが含まれている必要はありません。 メモリ最適化オブジェクトが存在しない場合、リソース プールからメモリは取得されません。 このバインドは、以下で説明するように、アロケーターによって割り当てられたメモリを管理するために Resource Governor によって使用され [!INCLUDE[hek_2](../../includes/hek-2-md.md)] ます。  
  
 指定されたデータベースのバインドが既に存在する場合、プロシージャはエラーを返します。  どのような場合でも、データベースがアクティブなバインドを複数持つことはできません。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
  
## <a name="syntax"></a>構文  
  
```sql  
sys.sp_xtp_bind_db_resource_pool 'database_name', 'resource_pool_name'  
```  
  
## <a name="arguments"></a>引数  
 database_name  
 既存の [!INCLUDE[hek_2](../../includes/hek-2-md.md)] 有効なデータベースの名前。  
  
 resource_pool_name  
 既存のリソースプールの名前。  
  
## <a name="messages"></a>メッセージ  
 エラーが発生すると、 `sp_xtp_bind_db_resource_pool` これらのメッセージのいずれかが返されます。  
  
 **データベースが存在しません**  
 Database_name は既存のデータベースを参照する必要があります。 指定した ID を持つデータベースが存在しない場合は、次のメッセージが返されます。   
*データベース ID% d は存在しません。 このバインドに有効なデータベース ID を使用してください。*  
  
```  
Msg 911, Level 16, State 18, Procedure sp_xtp_bind_db_resource_pool_internal, Line 51  
Database 'Hekaton_DB213' does not exist. Make sure that the name is entered correctly.  
```  
  
**データベースがシステム データベースである**  
 [!INCLUDE[hek_2](../../includes/hek-2-md.md)] テーブルをシステム データベースに作成することはできません。  そのため、そのようなデータベースに[!INCLUDE[hek_2](../../includes/hek-2-md.md)] メモリのバインドを作成するのは無効です。  次のエラーが返されます。  
*Database_name% s はシステムデータベースを参照しています。 リソースプールは、ユーザーデータベースにのみバインドできます。*  
  
```  
Msg 41371, Level 16, State 1, Procedure sp_xtp_bind_db_resource_pool_internal, Line 51  
Binding to a resource pool is not supported for system database 'master'. This operation can only be performed on a user database.  
```  
  
**リソースプールが存在しません**  
 Resource_pool_name によって識別されるリソースプールは、実行前に存在している必要があり `sp_xtp_bind_db_resource_pool` ます。  指定した ID のプールが存在しない場合、次のエラーが返されます。  
*リソースプール% s は存在しません。 有効なリソースプール名を入力してください。*  
  
```  
Msg 41370, Level 16, State 1, Procedure sp_xtp_bind_db_resource_pool_internal, Line 51  
Resource pool 'Pool_Hekaton' does not exist or resource governor has not been reconfigured.  
```  
  
**Pool_name が予約済みのシステム プールを参照している**  
 プール名 "INTERNAL" と "DEFAULT" は、システムプール用に予約されています。  データベースをこれらのいずれかに明示的にバインドすることは無効です。  システム プール名を入力した場合、次のエラーが返されます。  
*リソースプール% s はシステムリソースプールです。 このプロシージャを使用して、システムリソースプールを明示的にデータベースにバインドすることはできません。*  
  
```  
Msg 41373, Level 16, State 1, Procedure sp_xtp_bind_db_resource_pool_internal, Line 51  
Database 'Hekaton_DB' cannot be explicitly bound to the resource pool 'internal'. A database can only be bound only to a user resource pool.  
```  
  
**データベースは既に別のリソースプールにバインドされています**  
 データベースにバインドできるのは、1 度に 1 つのリソース プールだけです。 データベースを別のリソース プールにバインドする前に、リソース プールに対するデータベースのバインドを明示的に削除する必要があります。 「 [Sys. sp_xtp_unbind_db_resource_pool &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sys-sp-xtp-unbind-db-resource-pool-transact-sql.md)」を参照してください。  
*データベース% s は既にリソースプール% s にバインドされています。 新しいバインドを作成する前に、バインドを解除する必要があります。*  
  
```  
Msg 41372, Level 16, State 1, Procedure sp_xtp_bind_db_resource_pool_internal, Line 54  
Database 'Hekaton_DB' is currently bound to a resource pool. A database must be unbound before creating a new binding.  
```  
  
 成功すると、 `sp_xtp_bind_db_resource_pool` 次のメッセージが返されます。  
  
**バインドに成功**  
 成功すると、次の成功メッセージを返します。このメッセージは SQL ERRORLOG に記録されます。  
*ID %d のデータベースと ID %d のリソース プールの間にリソースのバインドが正常に作成されました。*  
  
## <a name="examples"></a>例  
A.  次のコード例では、データベース Hekaton_DB をリソースプール Pool_Hekaton にバインドします。  
  
```sql  
sys.sp_xtp_bind_db_resource_pool N'Hekaton_DB', N'Pool_Hekaton'  
```  
 
 バインドは、データベースが次にオンラインになったときに有効になります。  
 
 B. いくつかの基本的なチェックを含む、上記の例の拡張された例。  で次を実行します。 [!INCLUDE[tsql](../../includes/tsql-md.md)][!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]\:
 
```sql
DECLARE @resourcePool sysname = N'Pool_Hekaton';
DECLARE @database sysname = N'Hekaton_DB';

-- Check whether resource pool exists
IF NOT EXISTS (
    SELECT * FROM sys.resource_governor_resource_pools WHERE name = @resourcePool
    )
BEGIN
    SELECT N'Resource pool "' + @resourcePool + N'" does not exist or resource governor has not been reconfigured.';
END
-- Check whether database is already bound to a resource pool
ELSE IF EXISTS (
    SELECT p.name
    FROM sys.databases d
    JOIN sys.resource_governor_resource_pools p
    ON d.resource_pool_id = p.pool_id
    WHERE d.name = @database
    )
BEGIN
    SELECT N'Database "' + @database + N'" is currently bound to resource pool "' + @resourcePool  + N'". A database must be unbound before creating a new binding.';
END
-- Bind resource pool to database.
ELSE BEGIN
    EXEC sp_xtp_bind_db_resource_pool @database, @resourcePool; 
END 
``` 
  
## <a name="requirements"></a>要件  
  
-   `database_name` で指定するデータベースと `resource_pool_name` で指定するリソース プールはどちらも、バインドする前に存在している必要があります。  
  
-   CONTROL SERVER 権限が必要です。  
  
## <a name="see-also"></a>参照  
 [データベースを作成してリソース プールにバインドする方法については、「](../../relational-databases/in-memory-oltp/bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md)   
 [sys.sp_xtp_unbind_db_resource_pool &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-xtp-unbind-db-resource-pool-transact-sql.md)  
  
  
