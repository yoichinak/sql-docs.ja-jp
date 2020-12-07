---
description: sp_syscollector_create_collection_item (Transact-SQL)
title: sp_syscollector_create_collection_item (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_syscollector_create_collection_item
- sp_syscollector_create_collection_item_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_syscollector_create_collection_item
- data collector [SQL Server], stored procedures
ms.assetid: 60dacf13-ca12-4844-b417-0bc0a8bf0ddb
author: markingmyname
ms.author: maghan
ms.openlocfilehash: a99c9adb21d6c9b09d4e1e29ad845253ba3c9b19
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89538535"
---
# <a name="sp_syscollector_create_collection_item-transact-sql"></a>sp_syscollector_create_collection_item (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  ユーザー定義のコレクションセットにコレクションアイテムを作成します。 コレクションアイテムでは、収集するデータと、データの収集頻度を定義します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_syscollector_create_collection_item   
      [ @collection_set_id = ] collection_set_id   
    , [ @collector_type_uid = ] 'collector_type_uid'  
    , [ @name = ] 'name'   
    , [ [ @frequency = ] frequency ]  
    , [ @parameters = ] 'parameters'  
    , [ @collection_item_id = ] collection_item_id OUTPUT  
```  
  
## <a name="arguments"></a>引数  
 [ @collection_set_id =] *collection_set_id*  
 コレクションセットの一意なローカル識別子を設定します。 *collection_set_id* は **int**です。  
  
 [ @collector_type_uid =] '*collector_type_uid*'  
 この項目に使用するコレクター型を識別する GUID を指定します *collector_type_uid* 既定値が指定されていない **uniqueidentifier** です。 コレクター型の一覧については、syscollector_collector_types システム ビューにクエリを実行します。  
  
 [ @name =] '*name*'  
 コレクションアイテムの名前を指定します。 *名前* は **sysname** で、空の文字列または NULL にすることはできません。  
  
 *名前* は一意である必要があります。 現在のコレクション アイテムの名前の一覧については、syscollector_collection_items システム ビューにクエリを実行します。  
  
 [ @frequency =] *頻度*  
 は、このコレクションアイテムによってデータが収集される頻度を秒単位で指定するために使用します。 *frequency* は **int**,、既定値は5です。 指定できる最小値は5秒です。  
  
 コレクションセットが非キャッシュモードに設定されている場合、このモードではコレクションセットに指定されたスケジュールでデータ収集とアップロードの両方が行われるため、頻度は無視されます。 コレクションセットのコレクションモードを表示するには、 [syscollector_collection_sets](../../relational-databases/system-catalog-views/syscollector-collection-sets-transact-sql.md) システムビューに対してクエリを実行します。  
  
 [ @parameters =] '*parameters*'  
 コレクター型の入力パラメーターを指定します。 *パラメーター* は **xml** で、既定値は NULL です。 *パラメーター*スキーマは、コレクター型のパラメータースキーマと一致している必要があります。  
  
 [ @collection_item_id =] *collection_item_id*  
 コレクション セット アイテムを識別する一意な識別子を指定します。 *collection_item_id* は **int** であり、出力があります。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または **1** (失敗)  
  
## <a name="remarks"></a>解説  
 sp_syscollector_create_collection_item は、msdb システム データベースのコンテキストで実行する必要があります。  
  
 コレクションアイテムを追加するコレクションセットは、コレクションアイテムを作成する前に停止する必要があります。 コレクションアイテムをシステムコレクションセットに追加することはできません。  
  
## <a name="permissions"></a>アクセス許可  
 このプロシージャを実行するには、dc_admin (EXECUTE 権限を持つ) 固定データベースロールのメンバーシップが必要です。  
  
## <a name="examples"></a>例  
 次の例では、コレクション型に基づいてコレクションアイテムを作成 `Generic T-SQL Query Collector Type` し、という名前のコレクションセットに追加し `Simple collection set test 2` ます。 指定したコレクションセットを作成するには、 [sp_syscollector_create_collection_set &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-create-collection-set-transact-sql.md)で例 B を実行します。  
  
```  
USE msdb;  
GO  
DECLARE @collection_item_id int;  
DECLARE @collection_set_id int = (SELECT collection_set_id   
                                  FROM syscollector_collection_sets  
                                  WHERE name = N'Simple collection set test 2');  
DECLARE @collector_type_uid uniqueidentifier =   
    (SELECT collector_type_uid  
     FROM syscollector_collector_types  
     WHERE name = N'Generic T-SQL Query Collector Type');  
DECLARE @params xml =   
    CONVERT(xml, N'\<ns:TSQLQueryCollector xmlns:ns="DataCollectorType">  
            <Query>  
                <Value>SELECT * FROM sys.objects</Value>  
                <OutputTable>MyOutputTable</OutputTable>  
            </Query>  
            <Databases>   
                <Database> UseSystemDatabases = "true"   
                           UseUserDatabases = "true"  
                </Database>  
            </Databases>  
         \</ns:TSQLQueryCollector>');  
  
EXEC sp_syscollector_create_collection_item  
    @collection_set_id = @collection_set_id,  
    @collector_type_uid = @collector_type_uid,  
    @name = 'My custom TSQL query collector item',  
    @frequency = 6000,  
    @parameters = @params,  
    @collection_item_id = @collection_item_id OUTPUT;  
```  
  
## <a name="see-also"></a>参照  
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [[データ コレクション]](../../relational-databases/data-collection/data-collection.md)   
 [sp_syscollector_update_collection_item &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-update-collection-item-transact-sql.md)   
 [sp_syscollector_delete_collection_item &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-delete-collection-item-transact-sql.md)   
 [syscollector_collector_types &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/syscollector-collector-types-transact-sql.md)   
 [sp_syscollector_create_collection_set &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-create-collection-set-transact-sql.md)   
 [syscollector_collection_items &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/syscollector-collection-items-transact-sql.md)  
  
  
