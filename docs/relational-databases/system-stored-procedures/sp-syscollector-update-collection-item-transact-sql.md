---
description: sp_syscollector_update_collection_item (Transact-sql)
title: sp_syscollector_update_collection_item (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_syscollector_update_collection_item
- sp_syscollector_update_collection_item_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- data collector [SQL Server], stored procedures
- sp_syscollector_update_collection_item
ms.assetid: 7a0d36c8-c6e9-431d-a5a4-6c1802bce846
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 2dc7d6967f4bfa7aa1c22f4cfa5c55e06127455b
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89534866"
---
# <a name="sp_syscollector_update_collection_item-transact-sql"></a>sp_syscollector_update_collection_item (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  ユーザー定義のコレクション アイテムのプロパティまたは名前の変更に使用されます。  
  
 
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_syscollector_update_collection_item   
      [ [ @collection_item_id = ] collection_item_id ]  
    , [ [ @name = ] 'name' ]  
    , [ [ @new_name = ] 'new_name' ]  
    , [ [ @frequency = ] frequency ]  
    , [ [ @parameters = ] 'parameters' ]  
```  
  
## <a name="arguments"></a>引数  
 [ @collection_item_id =] *collection_item_id*  
 コレクションアイテムを識別する一意の識別子を指定します。 *collection_item_id* は **int** で、既定値は NULL です。 *名前*が NULL の場合、 *collection_item_id*には値が必要です。  
  
 [ @name =] '*name*'  
 コレクションアイテムの名前を指定します。 *名前* は **sysname** で、既定値は NULL です。 *collection_item_id*が NULL の場合、*名前*には値を指定する必要があります。  
  
 [ @new_name =] '*new_name*'  
 コレクション アイテムの新しい名前を指定します。 *new_name* は **sysname**であり、使用する場合、空の文字列にすることはできません。  
  
 *new_name* は一意である必要があります。 現在のコレクション アイテムの名前の一覧については、syscollector_collection_items システム ビューにクエリを実行します。  
  
 [ @frequency =] *頻度*  
 このコレクション アイテムによってデータを収集する頻度を秒単位で指定します。 *frequency* は **int**,、既定値は 5,、最小値を指定できます。  
  
 [ @parameters =] '*parameters*'  
 コレクション アイテムの入力パラメーターを指定します。 *パラメーター* は **xml** で、既定値は NULL です。 *パラメーター*スキーマは、コレクター型のパラメータースキーマと一致している必要があります。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または 1 (失敗)  
  
## <a name="remarks"></a>解説  
 コレクション セットが非キャッシュ モードに設定されている場合、このモードではコレクション セットに指定されたスケジュールでデータ収集とアップロードが行われるため、頻度を変更しても無視されます。 コレクションセットの状態を表示するには、次のクエリを実行します。 `<collection_item_id>` は、更新するコレクション アイテムの ID に置き換えてください。  
  
```  
USE msdb;  
GO  
SELECT cs.collection_set_id, collection_set_uid, cs.name   
    ,'is running' = CASE WHEN is_running =  0 THEN 'No' ELSE 'Yes' END  
    ,'cache mode' = CASE WHEN collection_mode = 0 THEN 'Cached mode' ELSE 'Non-cached mode' END  
FROM syscollector_collection_sets AS cs  
JOIN syscollector_collection_items AS ci   
ON ci.collection_set_id = cs.collection_set_id  
WHERE collection_item_id = <collection_item_id>;  
```  
  
## <a name="permissions"></a>アクセス許可  
 このプロシージャを実行するには、(EXECUTE 権限を持つ) dc_admin または dc_operator 固定データベース ロールのメンバーシップが必要です。 dc_operator ロールのメンバーがこのストアド プロシージャで更新できるのは、その権限で変更できるプロパティに限られます。 次のプロパティについては、dc_admin のみ変更できます。  
  
-   @new_name  
  
-   @parameters  
  
## <a name="examples"></a>例  
 次の例は、「 [sp_syscollector_create_collection_item &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-create-collection-item-transact-sql.md)」で定義されている例で作成したコレクションアイテムに基づいています。  
  
### <a name="a-changing-the-collection-frequency"></a>A. 収集頻度を変更する  
 次の例では、指定したコレクション アイテムの収集頻度を変更します。  
  
```  
USE msdb;  
GO  
EXEC sp_syscollector_update_collection_item   
@name = N'My custom TSQL query collector item',  
@frequency = 3000;  
GO  
```  
  
### <a name="b-renaming-a-collection-item"></a>B. コレクションアイテムの名前の変更  
 次の例では、コレクション アイテムの名前を変更します。  
  
```  
USE msdb;  
GO  
EXEC sp_syscollector_update_collection_item   
@name = N'My custom TSQL query collector item',  
@new_name = N'My modified TSQL item';  
GO  
```  
  
### <a name="c-changing-the-parameters-of-a-collection-item"></a>C. コレクション アイテムのパラメーターを変更する  
 次の例では、コレクションアイテムに関連付けられているパラメーターを変更します。 `<Value>` 属性内で定義されているステートメントを変更し、`UseSystemDatabases` 属性を false に設定します。 このアイテムの現在のパラメーターを表示するには、syscollector_collection_items システム ビューの parameters 列にクエリを実行します。 の値を変更することが必要になる場合があり `@collection_item_id` ます。  
  
```  
USE msdb;  
GO  
EXEC sp_syscollector_update_collection_item   
@collection_item_id = 9,   
@parameters = '  
    \<ns:TSQLQueryCollector xmlns:ns="DataCollectorType">  
        <Query>  
            <Value>SELECT * FROM sys.dm_db_index_usage_stats</Value>  
            <OutputTable>MyOutputTable</OutputTable>  
        </Query>  
        <Databases>  
            <Database> UseSystemDatabases = "false"   
                       UseUserDatabases = "true"</Database>  
        </Databases>  
    \</ns:TSQLQueryCollector>';  
GO  
```  
  
## <a name="see-also"></a>参照  
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [[データ コレクション]](../../relational-databases/data-collection/data-collection.md)   
 [sp_syscollector_create_collection_item &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-create-collection-item-transact-sql.md)   
 [syscollector_collection_items &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/syscollector-collection-items-transact-sql.md)  
  
  
